# KOMB60.prg

- Jobs: [129](#jobs)
- Tables: [28](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | KOMBI E60 |
| ORIGIN | BMW TI-431 Nau |
| REVISION | 3.007 |
| AUTHOR | Eurospace EE-42 Kugelmann, BMW EE-42 Cogiel, Eurospace EE-42 Kuppe, BMW TI-431 Nau |
| COMMENT | SGBD fuer Kombiinstrument E60 |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
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
- [STEUERGERAETE_RESET_DELAY](#job-steuergeraete-reset-delay) - Seuergeraete reset mit Delay ausloesen KWP2000: $11 ECUReset .        $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT bzw. Info zum Argument DELAY.
- [SG_RESET_OHNE_UHR_DATUM](#job-sg-reset-ohne-uhr-datum) - Steuergeraete Reset ausloesen Uhrzeit und Datum bleibt dabei im Kombi erhalten KWP2000: $11, $FA
- [UHRZEIT_DATUM_STELLEN](#job-uhrzeit-datum-stellen) - Uhrzeit und Datum stellen . die Daten werden vom PC bzw. Tester uebernommen KWP2000: $3B,$8E
- [CODIERDATEN_LESEN](#job-codierdaten-lesen)
- [C_CHECKSUMME](#job-c-checksumme) - Checksumme generieren und in BINAER_BUFFER schreiben Optionaler Codierjob
- [STEUERN_LEUCHTEN](#job-steuern-leuchten) - Kontrolleuchten im Kombi ansteuern Fuer Service-und Testzwecke Uebergeben werden 4 Argument im Bereich von 0x00-0xFF Dieser Argumente definieren die Leuchten Im Kombi LH Teil 3.2 Kapitel "Diagnose" sind die Uebergabeparameter des Diagnosebefehls $30 ausfuehrlich dokumentiert KWP2000: $30 $27 $06 InputOutputControlByLocalIdentifier . Hinweise: - gleichzeitig duerfen nicht mehr als 16 Leuchten . angesteuert werden! - DUO-LEDs duerfen nicht zweifarbig angesteuert werden - KL Blinker koennen nicht angesteuert werden
- [STEUERN_LEUCHTEN_BLAU](#job-steuern-leuchten-blau) - Blaue Leuchten im Kombi ansteuern Fuer Service-und Testzwecke . KWP2000: $30 $27 $06 InputOutputControlByLocalIdentifier
- [STEUERN_LEUCHTEN_GELB](#job-steuern-leuchten-gelb) - Gelbe Leuchten im Kombi ansteuern Fuer Service-und Testzwecke Ansteuerung inklusive Displaybeleuchtung KWP2000: $30 $27 $06 InputOutputControlByLocalIdentifier
- [STEUERN_LEUCHTEN_GRUEN](#job-steuern-leuchten-gruen) - Gruene Leuchten im Kombi ansteuern Fuer Service-und Testzwecke Zusaetzlich mit KL fuer Blinker . KWP2000: $30 $27 $06 InputOutputControlByLocalIdentifier
- [STEUERN_LEUCHTEN_ORANGE](#job-steuern-leuchten-orange) - Gelbe Leuchten im Kombi ansteuern Fuer Service-und Testzwecke Ansteuerung inklusive Displaybeleuchtung KWP2000: $30 $27 $06 InputOutputControlByLocalIdentifier
- [STEUERN_LEUCHTEN_ROT](#job-steuern-leuchten-rot) - Rote Leuchten im Kombi ansteuern Fuer Service-und Testzwecke Ansteuerung inklusive Displaybeleuchtung KWP2000: $30 $27 $06 InputOutputControlByLocalIdentifier
- [STEUERN_LEUCHTE_AUS](#job-steuern-leuchte-aus) - Wenn vorher der Job STEUERN_LEUCHTEN aufgerufen wurde wird die Ansteuerung der KL durch Diagnose vorgegeben STEUERN_LEUCHTE_AUS gibt die Kontrolle wieder an das Kombi zurueck HINWEIS: loescht nach Beendigung auch den Blinker . (wird bei _LEUCHTEN_GRUEN mit angesteuert!)  KWP2000: $30 $27 $00 InputOutputControlByLocalIdentifier
- [STEUERN_BLINKER](#job-steuern-blinker) - Blinker ansteuern, fuer Service-und Testzwecke Es muessen immer alle zwei Argumente uebergeben werden Dieser Jobs muss durch STEUERN_BLINKER_AUS beendet werden KWP2000: $30 $2B  Beschreibung der Arumente: BYTE 0: 1 = Normalblinken .       2 = Defektblinken .       3 = Doppelblinken .       4 = Blinker statisch ein  BYTE 1: 0 = Beide Blinker aus .       1 = Linker Blinker .       2 = Rechter Blinker .       3 = Beide Blinker
- [STEUERN_BLINKER_AUS](#job-steuern-blinker-aus) - Wenn vorher der Job STEUERN_BLINKER aufgerufen wurde wird die Ansteuerung der KL durch Diagnose vorgegeben STEUERN_BLINKER_ENDE gibt die Kontrolle wieder an das Kombi zurueck KWP2000: $30, $2B, $00
- [STEUERN_SELBSTTEST_EIN](#job-steuern-selbsttest-ein) - Schaltet den Selbttest ein Beschreibung der Arumente BYTE 0: 0  =  0000 0000   Test aus .       1  =  0000 0001   Nur 1 Durchlauf .       2  =  0000 0010   Dauerlauf KWP2000: $31, $23
- [STEUERN_SELBSTTEST_AUS](#job-steuern-selbsttest-aus) - Schaltet den Selbsttest wieder aus KWP2000: $31, $23, $00
- [STEUERN_TACHO](#job-steuern-tacho) - Tacho auf beliebige Geschwindigkeit (0..340) setzen KWP2000: $30 InputOutputControlByLocalIdentifier
- [STEUERN_TACHO_AUS](#job-steuern-tacho-aus) - Schaltet den Tacho-Vorgabemodus wieder aus KWP2000: $30, $20, $00
- [STEUERN_DREHZAHL](#job-steuern-drehzahl) - DrehZahlMesser in 1/min vorgeben KWP2000: $30 InputOutputControlByLocalIdentifier
- [STEUERN_DREHZAHL_AUS](#job-steuern-drehzahl-aus) - Schaltet den DZM-Vorgabemodus wieder aus KWP2000: $30, $21, $00
- [STEUERN_KVA](#job-steuern-kva) - Momentanverbrauch in L/100km vorgeben KWP2000: $30 InputOutputControlByLocalIdentifier
- [STEUERN_KVA_AUS](#job-steuern-kva-aus) - Schaltet den KVA-Vorgabemodus wieder aus KWP2000: $30, $23, $00
- [STEUERN_OELTEMP](#job-steuern-oeltemp) - Oeltemperatur in Grad Celsius vorgeben KWP2000: $30 InputOutputControlByLocalIdentifier
- [STEUERN_OELTEMP_AUS](#job-steuern-oeltemp-aus) - Schaltet den Oeltemperatur-Vorgabemodus wieder aus KWP2000: $30, $23, $00
- [STEUERN_TANK](#job-steuern-tank) - Tankinhalt in % vorgeben KWP2000: $30 InputOutputControlByLocalIdentifier
- [STEUERN_TANK_AUS](#job-steuern-tank-aus) - Schaltet den Tank-Vorgabemodus wieder aus KWP2000: $30, $22, $00
- [STEUERN_ACC_ZEIGER](#job-steuern-acc-zeiger) - Geschwindigkeit fuer ACC-Zeiger in km/h vorgeben KWP2000: $30 InputOutputControlByLocalIdentifier
- [STEUERN_ACC_ZEIGER_AUS](#job-steuern-acc-zeiger-aus) - Schaltet den ACC-Zeiger-Vorgabemodus wieder aus KWP2000: $30, $24, $00
- [STEUERN_VWF](#job-steuern-vwf) - Drehzahl fuer DZM-Vorwarnfeld-Zeiger in 1/min vorgeben KWP2000: $30 InputOutputControlByLocalIdentifier
- [STEUERN_VWF_AUS](#job-steuern-vwf-aus) - Schaltet den VWF-Zeiger-Vorgabemodus wieder aus KWP2000: $30, $25, $00
- [STATUS_TANKINHALT](#job-status-tankinhalt) - Literwerte der Tank-Hebelgeber 1 und 2, Summenwert ungedaempft und gedaempft sowie Tankphase KWP2000: $21 ReadDataByLocalIdentifier .        $0A Tankinhalt
- [STATUS_WASCHWASSER](#job-status-waschwasser) - Digitalen Eingang Waschwasser lesen Fuer Service-und Testzwecke KWP2000: $21 ReadDataByLocalIdentifier .        $23 Waschwasser
- [STATUS_KUEHLMITTELSTAND](#job-status-kuehlmittelstand) - Digitalen Eingang Kuehlmittelstand lesen Fuer Service-und Testzwecke KWP2000: $21 ReadDataByLocalIdentifier .        $24 Kuehlmittel
- [STATUS_PARKBREMSE](#job-status-parkbremse) - Zustand der Parkbremse lesen Fuer Service-und Testzwecke KWP2000: $21 ReadDataByLocalIdentifier .        $25 Parkbremse
- [STATUS_A_TEMP_LESEN](#job-status-a-temp-lesen) - A-Temp, Anzeige und Rohwert lesen Fuer Service-und Testzwecke KWP2000: $21 ReadDataByLocalIdentifier .        $22 A-Temp
- [GWSZ_RESET](#job-gwsz-reset) - GWSZ Korrektur-Offset aendern
- [STATUS_ABSOLUTER_GWSZ](#job-status-absoluter-gwsz) - liefert den absoluten GWSZ KWP2000 0x21, 0x0B
- [STATUS_GWSZ_OFFSET](#job-status-gwsz-offset) - liefert den GWSZ-Offset KWP2000 0x21, 0x17
- [STATUS_GWSZ_ANZEIGE](#job-status-gwsz-anzeige) - liefert den angezeigeten GWSZ KWP2000 0x21, 0x0B KWP2000 0x21, 0x17
- [LESEN_AKTUELLES_UIF](#job-lesen-aktuelles-uif) - aktuelles UIF lesen KWP2000: $1A ReadECUIdentification .        $86 currentUIFDataTable
- [LESEN_HW_NUMMER](#job-lesen-hw-nummer) - HW-Nummer lesen KWP2000: $1A ReadECUIdentification .        $87 physicalECUHardwareNumber
- [LESEN_EEPROM_DATENINDEX](#job-lesen-eeprom-datenindex) - EEPROM-Datenindex lesen KWP2000: $1A ReadECUIdentification .        $8A (systemSupplierSpecific) E60: EEPROM-Datenindex
- [LESEN_VARIANTENINDEX](#job-lesen-variantenindex) - Variantenindex lesen KWP2000: $1A ReadECUIdentification .        $97 SystemName
- [LESEN_HW_AENDERUNGSINDEX](#job-lesen-hw-aenderungsindex) - Hardware-Aenderungsindex lesen KWP2000: $1A ReadECUIdentification .        $9A vehicleManufacturerECUHardwareVersionNumber
- [LESEN_DIAGNOSEINDEX](#job-lesen-diagnoseindex) - Diagnoseindex lesen KWP2000: $1A ReadECUIdentification .        $9C vehicleManufacturerDiagnosticIndex
- [LESEN_FERTIGUNGSDATUM](#job-lesen-fertigungsdatum) - Fertigungsdatum lesen KWP2000: $1A ReadECUIdentification .        $9D DateofECUManufacturing
- [LESEN_LIEFEREANTENNUMMER](#job-lesen-liefereantennummer) - Lieferantennummer lesen KWP2000: $1A ReadECUIdentification .        $9E systemSupplierIndex
- [LESEN_SW_LAYER_VERSION](#job-lesen-sw-layer-version) - SW-Layer Versionen lesen KWP2000: $1A ReadECUIdentification .        $9F vehicleManufECUSoftwareLayerVersionNumbers
- [STATUS_TACHO_LESEN](#job-status-tacho-lesen) - gibt die Anzeigegeschwindigleit aus (Einheit km/h) KWP2000: $21 ReadDataByLocalIdentifier .        $05 Geschwindigkeit
- [STATUS_DREHZAHL_LESEN](#job-status-drehzahl-lesen) - gibt die Motordrehzahl aus (Einheit Umdrehungen/min) KWP2000: $21 ReadDataByLocalIdentifier .        $06 Drehzahl lesen
- [STATUS_LENKSTOCK](#job-status-lenkstock) - gibt den Status des Lenkstockschalters aus KWP2000: $21 ReadDataByLocalIdentifier .        $07 Status Lenkstockschalter
- [STATUS_KL30_H_OFFSET](#job-status-kl30-h-offset) - Klemme 30 Stundenzaehler Offset auslesen KWP2000: $21 ReadDataByLocalIdentifier .        $0C Kl.30 Stundenzaehler Offset
- [STATUS_KL30_H_ZAEHLER](#job-status-kl30-h-zaehler) - Klemme 30 Stundenzaehler auslesen KWP2000: $21 ReadDataByLocalIdentifier .        $0D Kl.30 Stundenzaehler
- [CALC_KL30_H_OFFSET](#job-calc-kl30-h-offset) - Klemme 30 Stundenzaehler Offset ab dem momentanen Datum berechnen Dieser Job wird nur in der BMW-Fertigung im Rahmen der Codierung aufgerufen Hinweis: Schaltjahresberechnung falsch ab 2100
- [SET_KL30_OFFSET2AKT_DATE](#job-set-kl30-offset2akt-date) - Berechnet den Klemme 30 Stundenzaehler Offset ab dem momentanen Datum und schreibt diesen in das EEPROM des KOMBI CBS funtioniert nur richtig, wenn der KL30_H_OFFSET richtig gesetzt ist. Daher sollte der Job immer aufgerufen werden wenn das Fahrzeug an den Taster angeschlossen wird KWP2000: $3B, $0C Hinweis: Schaltjahresberechnung falsch ab 2100
- [STATUS_DATE_LAST_CODING_SESSION](#job-status-date-last-coding-session) - Datum, gibt an, wann das Kombi zum letzten mal codiert wurde (bei BMW) KWP2000: $21, $08
- [STATUS_KLEMMEN](#job-status-klemmen) - Klemmenstati auslesen KWP2000: $21, $0E
- [C_FG_LESEN2](#job-c-fg-lesen2) - Fahrgestellnummer lesen modifizierter Standard Codierjob (andere Diagnosefunktion) KWP2000: $21 ReadDataByLocalIdentifier .        $90 Vehicle Identification Number Modus  : Default
- [STATUS_KLEMMENSPANNUNG](#job-status-klemmenspannung) - liefert Wert der Kombi-Versorgungsspannung KWP2000: $21 ReadDataByLocalIdentifier .        $21 Klemmenspannung
- [STATUS_CHECKCONTROL_LESEN](#job-status-checkcontrol-lesen) - gibt die ID Nummern der momentan aktiven CC-Meldungen aus KWP2000: $21, $09
- [STATUS_BETRIEBSDATEN_HEADER](#job-status-betriebsdaten-header) - gibt den KM Stand aus CBS Betriebsdaten Header aus KWP2000 $21 $B0
- [STATUS_BETRIEBSDATEN_LESEN](#job-status-betriebsdaten-lesen) - liest ausgewaehlte Daten aus CBS Betriebsdaten aus KWP2000 $21 $B1 bis $BF
- [STATUS_ZEITSTRAHL](#job-status-zeitstrahl) - gibt CBS Daten fuer den Annahmerechner in der Reihenfolge Header CBS Umpfaenge, CC Umpfaenge KWP2000 $21 $C0/$C1/$C2 Fuer die exakte Beschreiung der CBS Zeitstrahldaten siehe LH Teil 3 Kapitel Diagnose, Beschreibung zu $21
- [STEUERN_CBS_KM_PER_YEAR](#job-steuern-cbs-km-per-year) - Vorgabe Km/Jahr fuer CBS KWP2000 $3B $16
- [STEUERN_BOS_CODIERUNG](#job-steuern-bos-codierung) - BOS Codierung fuer alle einzelnen BOS Groessen. Fuer CBS3-Layout.
- [STEUERN_CBS_SC_CODIERUNG](#job-steuern-cbs-sc-codierung) - CBS Servicecall Enable/Disable Codierung. Fuer CBS3-Layout.
- [STATUS_CBS_WOCHEN_KM](#job-status-cbs-wochen-km) - gibt die Daten des KM pro Woche-Algorithmus aus CBS Betriebsdaten Header aus KWP2000 $21 $B0
- [MOTORTYP](#job-motortyp) - im Kombi codierten Motortyp ermitteln KWP2000: $22 ReadDataByCommonIdentifier Job ermittelt Motortyp aus Kombi
- [STEUERN_TESTBITMAP](#job-steuern-testbitmap) - Testbitmap im Display darstellen KWP2000: $30 InputOutputControlByLocalIdentifier
- [STEUERN_TESTBITMAP_AUS](#job-steuern-testbitmap-aus) - Testbitmap im Display wieder abschalten KWP2000: $30 InputOutputControlByLocalIdentifier
- [STATUS_CHECKCONTROL_HISTORY](#job-status-checkcontrol-history) - CC-Meldungsspeicher aus Kombi lesen KWP2000: $21, $0F
- [STATUS_BOS_CODIERUNG](#job-status-bos-codierung) - BOS Codierung fuer alle einzelnen BOS Groessen. Fuer CBS3-Layout.
- [STATUS_GLOBAL_KM](#job-status-global-km) - liest den GWSZ aus KI RAM, EEPROM & CAS
- [STATUS_KI](#job-status-ki) - Liest Block.
- [LESEN_RINGBUF](#job-lesen-ringbuf) - Liest den Ringbuffer Inhalt
- [RINGBUF_INIT](#job-ringbuf-init) - Initialisiert den Ringbuffer
- [LESEN_CODIERBLOCK](#job-lesen-codierblock) - Codierdatenblock aus EEPROM auslesen
- [CSUMBL_3001](#job-csumbl-3001) - Checksumme in Block 3001 berechnen

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
| BOS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, ZKrz, Sic, Kfl, TUV, AU, Ueb Werte externe Umfaenge: Oel, Br_v, Br_h, Filt, CSF, Batt, VTG Defaultwert: 0x00 (ungueltig) |
| BOS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, kein Rueckstellen: 255 Defaultwert: 100 |
| BOS_ANZAHL_SERVICE | int | Anzahl der durchgefuehrten Services: 0-30 Schalter, keine Aenderung: 31 Defaultwert: 31 |
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

<a id="job-steuergeraete-reset-delay"></a>
### STEUERGERAETE_RESET_DELAY

Seuergeraete reset mit Delay ausloesen KWP2000: $11 ECUReset .        $01 PowerOn Modus  : Default  Nach dem Job muss die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT bzw. Info zum Argument DELAY.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DELAY | long | Anzahl zu wartender Sekunden Maximalwert: 255 (bzw. 256) Ohne Angabe: keine Wartezeit Wird als Delayzeit 256 angegeben, wird die notwendige Wartezeit aus dem Kombi ausgelesen. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sg-reset-ohne-uhr-datum"></a>
### SG_RESET_OHNE_UHR_DATUM

Steuergeraete Reset ausloesen Uhrzeit und Datum bleibt dabei im Kombi erhalten KWP2000: $11, $FA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-uhrzeit-datum-stellen"></a>
### UHRZEIT_DATUM_STELLEN

Uhrzeit und Datum stellen . die Daten werden vom PC bzw. Tester uebernommen KWP2000: $3B,$8E

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_NR | unsigned int | HEX-Wert muss folgendermassen eingegeben werden: 0x"Wert" Werte im Bereich 0x3000...0x3FFF" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| CODIERDATENBLOCK | binary | Enthaelt den Codierdatenblock |
| _TEL_ANTWORT | binary | Antwort von SG |

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
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| OUT_BUFFER | binary | Als Result wird der gefuellte Binaerbuffer zurueckgegeben Der Binaerbuffer hat den Aufbau von BINAER_BUFFER |

<a id="job-steuern-leuchten"></a>
### STEUERN_LEUCHTEN

Kontrolleuchten im Kombi ansteuern Fuer Service-und Testzwecke Uebergeben werden 4 Argument im Bereich von 0x00-0xFF Dieser Argumente definieren die Leuchten Im Kombi LH Teil 3.2 Kapitel "Diagnose" sind die Uebergabeparameter des Diagnosebefehls $30 ausfuehrlich dokumentiert KWP2000: $30 $27 $06 InputOutputControlByLocalIdentifier . Hinweise: - gleichzeitig duerfen nicht mehr als 16 Leuchten . angesteuert werden! - DUO-LEDs duerfen nicht zweifarbig angesteuert werden - KL Blinker koennen nicht angesteuert werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | kann beliebig verwendet werden |
| BYTE2 | int | kann beliebig verwendet werden |
| BYTE3 | int | kann beliebig verwendet werden |
| BYTE4 | int | kann beliebig verwendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-leuchten-blau"></a>
### STEUERN_LEUCHTEN_BLAU

Blaue Leuchten im Kombi ansteuern Fuer Service-und Testzwecke . KWP2000: $30 $27 $06 InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-leuchten-gelb"></a>
### STEUERN_LEUCHTEN_GELB

Gelbe Leuchten im Kombi ansteuern Fuer Service-und Testzwecke Ansteuerung inklusive Displaybeleuchtung KWP2000: $30 $27 $06 InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-leuchten-gruen"></a>
### STEUERN_LEUCHTEN_GRUEN

Gruene Leuchten im Kombi ansteuern Fuer Service-und Testzwecke Zusaetzlich mit KL fuer Blinker . KWP2000: $30 $27 $06 InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-leuchten-orange"></a>
### STEUERN_LEUCHTEN_ORANGE

Gelbe Leuchten im Kombi ansteuern Fuer Service-und Testzwecke Ansteuerung inklusive Displaybeleuchtung KWP2000: $30 $27 $06 InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-leuchten-rot"></a>
### STEUERN_LEUCHTEN_ROT

Rote Leuchten im Kombi ansteuern Fuer Service-und Testzwecke Ansteuerung inklusive Displaybeleuchtung KWP2000: $30 $27 $06 InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-leuchte-aus"></a>
### STEUERN_LEUCHTE_AUS

Wenn vorher der Job STEUERN_LEUCHTEN aufgerufen wurde wird die Ansteuerung der KL durch Diagnose vorgegeben STEUERN_LEUCHTE_AUS gibt die Kontrolle wieder an das Kombi zurueck HINWEIS: loescht nach Beendigung auch den Blinker . (wird bei _LEUCHTEN_GRUEN mit angesteuert!)  KWP2000: $30 $27 $00 InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-blinker"></a>
### STEUERN_BLINKER

Blinker ansteuern, fuer Service-und Testzwecke Es muessen immer alle zwei Argumente uebergeben werden Dieser Jobs muss durch STEUERN_BLINKER_AUS beendet werden KWP2000: $30 $2B  Beschreibung der Arumente: BYTE 0: 1 = Normalblinken .       2 = Defektblinken .       3 = Doppelblinken .       4 = Blinker statisch ein  BYTE 1: 0 = Beide Blinker aus .       1 = Linker Blinker .       2 = Rechter Blinker .       3 = Beide Blinker

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Steuert Blinkfrequenz |
| BYTE1 | int | links, rechts, aus, beide |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-blinker-aus"></a>
### STEUERN_BLINKER_AUS

Wenn vorher der Job STEUERN_BLINKER aufgerufen wurde wird die Ansteuerung der KL durch Diagnose vorgegeben STEUERN_BLINKER_ENDE gibt die Kontrolle wieder an das Kombi zurueck KWP2000: $30, $2B, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-selbsttest-ein"></a>
### STEUERN_SELBSTTEST_EIN

Schaltet den Selbttest ein Beschreibung der Arumente BYTE 0: 0  =  0000 0000   Test aus .       1  =  0000 0001   Nur 1 Durchlauf .       2  =  0000 0010   Dauerlauf KWP2000: $31, $23

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Test ein/aus, 1x oder Dauerlauf |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-selbsttest-aus"></a>
### STEUERN_SELBSTTEST_AUS

Schaltet den Selbsttest wieder aus KWP2000: $31, $23, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tacho"></a>
### STEUERN_TACHO

Tacho auf beliebige Geschwindigkeit (0..340) setzen KWP2000: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Geschwindigkeitsvorgabe in km/h (0..Tachoendwert) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| TACHOGRENZE | unsigned int | aus Kombi ermittelte maximaler Tachowert in km/h |
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

DrehZahlMesser in 1/min vorgeben KWP2000: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Drehzahlvorgabe in 1/min . Minimaldrehzahl = 0 . Maximaldrehzahl wird aus Kombi bestimmt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DREHZAHLGRENZE | unsigned int | aus Kombi ermittelte maximale Drehzahl in 1/min |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-drehzahl-aus"></a>
### STEUERN_DREHZAHL_AUS

Schaltet den DZM-Vorgabemodus wieder aus KWP2000: $30, $21, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kva"></a>
### STEUERN_KVA

Momentanverbrauch in L/100km vorgeben KWP2000: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Verbrauch in l/100km |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| KVAGRENZE | real | aus Kombi ermittelte maximale KVA-Wert in l/100km |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-kva-aus"></a>
### STEUERN_KVA_AUS

Schaltet den KVA-Vorgabemodus wieder aus KWP2000: $30, $23, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-oeltemp"></a>
### STEUERN_OELTEMP

Oeltemperatur in Grad Celsius vorgeben KWP2000: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Oeltemperatur in Grad C |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| OELTEMP_MIN | unsigned int | aus Kombi ermittelte minimalere Wert der Oeltemperatur in Grad C |
| OELTEMP_MAX | unsigned int | aus Kombi ermittelte maximalere Wert der Oeltemperatur in Grad C |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-oeltemp-aus"></a>
### STEUERN_OELTEMP_AUS

Schaltet den Oeltemperatur-Vorgabemodus wieder aus KWP2000: $30, $23, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tank"></a>
### STEUERN_TANK

Tankinhalt in % vorgeben KWP2000: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Tankinhalt in %  Wertebereich: 0...100 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-tank-aus"></a>
### STEUERN_TANK_AUS

Schaltet den Tank-Vorgabemodus wieder aus KWP2000: $30, $22, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-acc-zeiger"></a>
### STEUERN_ACC_ZEIGER

Geschwindigkeit fuer ACC-Zeiger in km/h vorgeben KWP2000: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Geschwindigkeit in km/h |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ACCGRENZE | unsigned int | aus Kombi ermittelter ACC-Endwert in km/h |
| _TEL_ANTWORT | binary | Antwor t von SG |

<a id="job-steuern-acc-zeiger-aus"></a>
### STEUERN_ACC_ZEIGER_AUS

Schaltet den ACC-Zeiger-Vorgabemodus wieder aus KWP2000: $30, $24, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vwf"></a>
### STEUERN_VWF

Drehzahl fuer DZM-Vorwarnfeld-Zeiger in 1/min vorgeben KWP2000: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | Drehzahl in 1/min . Minimal- und Maximalwert wird aus Kombi bestimmt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| VWF_UNTERGRENZE | unsigned int | aus Kombi ermittelte Minimalwert in 1/min |
| VWF_OBERGRENZE | unsigned int | aus Kombi ermittelte Maximalwert in 1/min |
| _TEL_ANTWORT | binary | Antwor t von SG |

<a id="job-steuern-vwf-aus"></a>
### STEUERN_VWF_AUS

Schaltet den VWF-Zeiger-Vorgabemodus wieder aus KWP2000: $30, $25, $00

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tankinhalt"></a>
### STATUS_TANKINHALT

Literwerte der Tank-Hebelgeber 1 und 2, Summenwert ungedaempft und gedaempft sowie Tankphase KWP2000: $21 ReadDataByLocalIdentifier .        $0A Tankinhalt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HEBELGEBER1_WERT | real | Zahlenwert Hebelgeber 1 |
| STAT_HEBELGEBER2_WERT | real | Zahlenwert Hebelgeber 2 |
| STAT_SUMMENWERT_WERT | real | Zahlenwert Summe aus Hebelgeber1 und 2 |
| STAT_GEDAEMPFT_ANZ_WERT | real | Zahlenwert gedaempfter Summenwert aus Hebelgeber 1 und 2 |
| STAT_HEBELGEBER_EINH | string | Einheit von Hebelgeber 1 und 2, Summenwert und Anzeigewert |
| STAT_TANKPHASE | int | Tankphase: 1 = i.O , 2 = mind. 1 Hebelgeber n.i.O. .          3 = wie 2 und zusaetzlich kein Verbrauchssignal |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-waschwasser"></a>
### STATUS_WASCHWASSER

Digitalen Eingang Waschwasser lesen Fuer Service-und Testzwecke KWP2000: $21 ReadDataByLocalIdentifier .        $23 Waschwasser

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WASCHWASSER | int | 0x00 = Leer, 0xFE = Voll, 0xFF = Fehler |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-kuehlmittelstand"></a>
### STATUS_KUEHLMITTELSTAND

Digitalen Eingang Kuehlmittelstand lesen Fuer Service-und Testzwecke KWP2000: $21 ReadDataByLocalIdentifier .        $24 Kuehlmittel

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KUEHLMITTELSTAND | int | 0x00 = Leer, 0xFE = Voll, 0xFF = Fehler |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-parkbremse"></a>
### STATUS_PARKBREMSE

Zustand der Parkbremse lesen Fuer Service-und Testzwecke KWP2000: $21 ReadDataByLocalIdentifier .        $25 Parkbremse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PARKBREMSE | int | 00 = lose, 01 = angezogen |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-a-temp-lesen"></a>
### STATUS_A_TEMP_LESEN

A-Temp, Anzeige und Rohwert lesen Fuer Service-und Testzwecke KWP2000: $21 ReadDataByLocalIdentifier .        $22 A-Temp

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_A_TEMP_ANZEIGE | real | Anzeigewert der Aussentemperatur Aufloesung 0,5 Grad C |
| STAT_A_TEMP_ROHWERT | real | Rohwert der Aussentemperatur Aufloesung 0,5 Grad C |
| STAT_A_TEMP_EINH | string | Einheit der Aussentemperatur-Werte |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-gwsz-reset"></a>
### GWSZ_RESET

GWSZ Korrektur-Offset aendern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-absoluter-gwsz"></a>
### STATUS_ABSOLUTER_GWSZ

liefert den absoluten GWSZ KWP2000 0x21, 0x0B

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GWSZ_WERT | long | Absoluter Kilometerstand |
| STAT_GWSZ_EINH | string | immer "km" |
| STAT_KM_SCHWELLE | string | GROESSER_255 oder KLEINER_GLEICH_255 (in km) |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-gwsz-offset"></a>
### STATUS_GWSZ_OFFSET

liefert den GWSZ-Offset KWP2000 0x21, 0x17

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GWSZ_OFFSET_WERT | long | Wert des GWSZ-Offset |
| STAT_GWSZ_OFFSET_EINH | string | immer "km" |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-status-gwsz-anzeige"></a>
### STATUS_GWSZ_ANZEIGE

liefert den angezeigeten GWSZ KWP2000 0x21, 0x0B KWP2000 0x21, 0x17

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GWSZ_ANZEIGE_WERT | long | Absoluter Kilometerstand |
| STAT_GWSZ_ANZEIGE_EINH | string | immer "km" |
| _TEL_ANTWORT | binary | Antwort von SG |
| _TEL_ANTWORT2 | binary | Antwort von SG auf 2. Anfrage |

<a id="job-lesen-aktuelles-uif"></a>
### LESEN_AKTUELLES_UIF

aktuelles UIF lesen KWP2000: $1A ReadECUIdentification .        $86 currentUIFDataTable

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| AIF_OFFSET | int | Offset (E60: 0x00,0x01,0x12,0xFF) . 0x00 =   0 freier Eintrag . 0x01 =   1 letzter Eintrag, ueberschreibbar . 0x12 =  18 Eintrag belegt . 0xFF = 255 freier Eintrag |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-hw-nummer"></a>
### LESEN_HW_NUMMER

HW-Nummer lesen KWP2000: $1A ReadECUIdentification .        $87 physicalECUHardwareNumber

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei DATEN_INKONSISTENT  wenn Daten fehlerhaft table JobResult STATUS_TEXT |
| HARDWARENUMMER | string | Hardwarenummer 12-stellig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-eeprom-datenindex"></a>
### LESEN_EEPROM_DATENINDEX

EEPROM-Datenindex lesen KWP2000: $1A ReadECUIdentification .        $8A (systemSupplierSpecific) E60: EEPROM-Datenindex

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| EEPROM_DATENINDEX_EEPROM | unsigned int | Datenindex der Codierdaten im EEPROM als Zahl |
| EEPROM_DATENINDEX_ROM | unsigned int | erwarteter Datenindex der Codierdaten aus ROM als Zahl |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-variantenindex"></a>
### LESEN_VARIANTENINDEX

Variantenindex lesen KWP2000: $1A ReadECUIdentification .        $97 SystemName

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| VARIANTENINDEX | string | Variantenindex 2-stellig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-hw-aenderungsindex"></a>
### LESEN_HW_AENDERUNGSINDEX

Hardware-Aenderungsindex lesen KWP2000: $1A ReadECUIdentification .        $9A vehicleManufacturerECUHardwareVersionNumber

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HW_AENDERUNGSINDEX | string | Variantenindex 2-stellig mit Punkt (x.y) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-diagnoseindex"></a>
### LESEN_DIAGNOSEINDEX

Diagnoseindex lesen KWP2000: $1A ReadECUIdentification .        $9C vehicleManufacturerDiagnosticIndex

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DIAGNOSEINDEX | string | Diagnoseindex 4-stellig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-fertigungsdatum"></a>
### LESEN_FERTIGUNGSDATUM

Fertigungsdatum lesen KWP2000: $1A ReadECUIdentification .        $9D DateofECUManufacturing

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FERTIGUNGSDATUM | string | Programmierdatum (TT.MM.JJJJ) |
| FERTIGUNGSDATUM_JAHR | int | Programmierdatum (Jahr) |
| FERTIGUNGSDATUM_MONAT | int | Programmierdatum (Monat) |
| FERTIGUNGSDATUM_TAG | int | Programmierdatum (Tag) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-liefereantennummer"></a>
### LESEN_LIEFEREANTENNUMMER

Lieferantennummer lesen KWP2000: $1A ReadECUIdentification .        $9E systemSupplierIndex

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| LIEFEREANTENNUMMER | string | Lieferantennummer 2-stellig (hex) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lesen-sw-layer-version"></a>
### LESEN_SW_LAYER_VERSION

SW-Layer Versionen lesen KWP2000: $1A ReadECUIdentification .        $9F vehicleManufECUSoftwareLayerVersionNumbers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| NACHRICHTENKATALOG | string | Nachrichtenkatalogversion  3 Stellen mit Punkten (x.y.z) |
| SW_VERSION | string | Softwareversion  3 Stellen mit Punkten (x.y.z) |
| BETRIEBSSYSTEM | string | Betriebssystemversion  3 Stellen mit Punkten (x.y.z) |
| RESERVE | string | reserved_by_document  3 Stellen mit Punkten (x.y.z) wird nicht verwendet! (KWP2000: "currently unused") |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tacho-lesen"></a>
### STATUS_TACHO_LESEN

gibt die Anzeigegeschwindigleit aus (Einheit km/h) KWP2000: $21 ReadDataByLocalIdentifier .        $05 Geschwindigkeit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GESCHWINDIGKEIT_WERT | int | ZAHLENWERT von Geschwindigkeit |
| STAT_GESCHWINDIGKEIT_EINH | string | Einheit von Geschwindigkeit |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drehzahl-lesen"></a>
### STATUS_DREHZAHL_LESEN

gibt die Motordrehzahl aus (Einheit Umdrehungen/min) KWP2000: $21 ReadDataByLocalIdentifier .        $06 Drehzahl lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DREHZAHL_WERT | int | Zahlenwert von Drehzahl |
| STAT_DREHZAHL_EINH | string | Einheit von Drehzahl |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lenkstock"></a>
### STATUS_LENKSTOCK

gibt den Status des Lenkstockschalters aus KWP2000: $21 ReadDataByLocalIdentifier .        $07 Status Lenkstockschalter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CC_TASTE | int | gueltige Rueckgabewerte fuer CC_TASTE 0x00 ='0'   =  CC Taste nicht gedrueckt 0xFE ='254' =  CC Taste gedrueckt 0xFF ='255' =  Signal ungueltig |
| STAT_BC_TASTE | int | gueltige Rueckgabewerte fuer BC_TASTE 0x00 ='0'   =  BC Taste nicht gedrueckt 0xFE ='254' =  BC Taste gedrueckt 0xFF ='255' =  Signal ungueltig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kl30-h-offset"></a>
### STATUS_KL30_H_OFFSET

Klemme 30 Stundenzaehler Offset auslesen KWP2000: $21 ReadDataByLocalIdentifier .        $0C Kl.30 Stundenzaehler Offset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KL30_H_OFFSET_WERT | long | ZAHLENWERT von KL30 Stundenzaehler Offset |
| STAT_KL30_H_OFFSET_EINH | string | Einheit von KL30 Stundenzaehler Offset |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kl30-h-zaehler"></a>
### STATUS_KL30_H_ZAEHLER

Klemme 30 Stundenzaehler auslesen KWP2000: $21 ReadDataByLocalIdentifier .        $0D Kl.30 Stundenzaehler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KL30_H_ZAEHLER_WERT | long | ZAHLENWERT von KL30 Stundenzaehler |
| STAT_KL30_H_ZAEHLER_EINH | string | Einheit von KL30 Stundenzaehler |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-calc-kl30-h-offset"></a>
### CALC_KL30_H_OFFSET

Klemme 30 Stundenzaehler Offset ab dem momentanen Datum berechnen Dieser Job wird nur in der BMW-Fertigung im Rahmen der Codierung aufgerufen Hinweis: Schaltjahresberechnung falsch ab 2100

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| KL30_H_OFFSET_WERT | string | ZAHLENWERT von KL30 Stundenzaehler Offset als String in Hex Darstellung |
| KL30_H_OFFSET_EINH | string | EINHEIT von KL30 Stundenzaehler Offset (String in Hex Darstellung) |

<a id="job-set-kl30-offset2akt-date"></a>
### SET_KL30_OFFSET2AKT_DATE

Berechnet den Klemme 30 Stundenzaehler Offset ab dem momentanen Datum und schreibt diesen in das EEPROM des KOMBI CBS funtioniert nur richtig, wenn der KL30_H_OFFSET richtig gesetzt ist. Daher sollte der Job immer aufgerufen werden wenn das Fahrzeug an den Taster angeschlossen wird KWP2000: $3B, $0C Hinweis: Schaltjahresberechnung falsch ab 2100

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-date-last-coding-session"></a>
### STATUS_DATE_LAST_CODING_SESSION

Datum, gibt an, wann das Kombi zum letzten mal codiert wurde (bei BMW) KWP2000: $21, $08

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TAG | int | Zahlenwert letztes Codierdatum Tag |
| STAT_MONAT | int | Zahlenwert letztes Codierdatum Tag |
| STAT_JAHR | int | Zahlenwert letzes Codierdatum |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klemmen"></a>
### STATUS_KLEMMEN

Klemmenstati auslesen KWP2000: $21, $0E

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KLR_WERT | char | ZAHLENWERT von Klemmenstatus KL R |
| STAT_KL15_WERT | char | ZAHLENWERT von Klemmenstatus KL 15 |
| STAT_KL50_WERT | char | ZAHLENWERT von Klemmenstatus KL50 |
| STAT_KLR_EINH | string | Einheit von Klemmenstatus KL R |
| STAT_KL15_EINH | string | Einheit von Klemmenstatus KL 15 |
| STAT_KL50_EINH | string | Einheit von Klemmenstatus KL50 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fg-lesen2"></a>
### C_FG_LESEN2

Fahrgestellnummer lesen modifizierter Standard Codierjob (andere Diagnosefunktion) KWP2000: $21 ReadDataByLocalIdentifier .        $90 Vehicle Identification Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klemmenspannung"></a>
### STATUS_KLEMMENSPANNUNG

liefert Wert der Kombi-Versorgungsspannung KWP2000: $21 ReadDataByLocalIdentifier .        $21 Klemmenspannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KLEMMENSPANNUNG_WERT | int | Zahlenwert der Klemmenspannung |
| STAT_KLEMMENSPANNUNG_EINH | string | Einheit der Klemmenspannung (normalerweise mV) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-checkcontrol-lesen"></a>
### STATUS_CHECKCONTROL_LESEN

gibt die ID Nummern der momentan aktiven CC-Meldungen aus KWP2000: $21, $09

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CC_ID_ANZAHL | int | Anzahl der aktiven CC-Meldungen |
| STAT_CC_NUMMERN | binary | Eine Liste von Nummern der aktiven CC-Meldungen (pro Nummer 2 Byte) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betriebsdaten-header"></a>
### STATUS_BETRIEBSDATEN_HEADER

gibt den KM Stand aus CBS Betriebsdaten Header aus KWP2000 $21 $B0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AKT_KM_STAND_WERT | long | km-Stand mit Aufloesung von 20 km |
| STAT_AKT_KM_STAND_EINH | string |  |
| STAT_BLOCK_KM_PER_WEEK | binary | Block KM/Woche aus CBS Betriebsdaten Header |
| STAT_TAGESZAEHLER_WERT | long | Tageszaehler (Kl.30 Stundenzaehler + Offset) |
| STAT_TAGESZAEHLER_EINH | string |  |
| STAT_AVKM_W | long | Kilometer/Woche Quartalswert mit Aufloesung von 10 km |
| STAT_AVKM_START | long | Startwert der km pro Woche Berechnung (aus Block 3009) |
| STAT_AKTUELLES_DATUM_WERT | long | Tageszaehler abgeleitet vom Datum |
| STAT_AKTUELLES_DATUM_EINH | string |  |
| STAT_MODE_WERT | int | CBS-Mode |
| STAT_MODE_TEXT | string |  |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG (Block 3009h, Einheit: 40km) |

<a id="job-status-betriebsdaten-lesen"></a>
### STATUS_BETRIEBSDATEN_LESEN

liest ausgewaehlte Daten aus CBS Betriebsdaten aus KWP2000 $21 $B1 bis $BF

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE0 | int | CBS ID 1..30h |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ID | int | CBS ID zu der die Betriebsdaten gehoehren |
| STAT_EINHEIT_ID | int | 0 bis 2 0=Prozent, 1=Weg, 2=Zeit, 3=Fehler |
| STAT_FARB_ID | int | 0 bis 3 0=gruen, 1=gelb, 2=rot, 3=Fehler |
| STAT_SC_NOTIFIED_ID | int | 0 oder 1 0=nicht_gemeldet, 1=gemeldet |
| STAT_RANG_ID | int | 0 bis 31 |
| STAT_VERFUEGBAR_ID | int | 0...100 oder 255 (Fehlerwert) |
| STAT_SERV_ZAEHL_ID | int | 0...30 oder 31 (Fehlerwert) |
| STAT_UNIT_ABSTAND_ID | int | 0 bis 3 Siehe Diagnose-LH |
| STAT_WERT_ABSTAND_ID | int | -63 bis +63, -64 = Fehlerwert |
| STAT_WERT_ID | int | -327670 bis 327670,  -327670 = Fehlerwert |
| STAT_WERT_D_ID | int | -32767 bis 32767 |
| STAT_ZIEL_MONAT_ID | int | 1...12, 15 (Fehler), 0 (Sperre) |
| STAT_ZIEL_JAHR_ID | int | zweistellig oder 255 (Fehler) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zeitstrahl"></a>
### STATUS_ZEITSTRAHL

gibt CBS Daten fuer den Annahmerechner in der Reihenfolge Header CBS Umpfaenge, CC Umpfaenge KWP2000 $21 $C0/$C1/$C2 Fuer die exakte Beschreiung der CBS Zeitstrahldaten siehe LH Teil 3 Kapitel Diagnose, Beschreibung zu $21

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BLOCK_C0 | binary | Block 0 der CBS Zeitstrahldaten |
| STAT_BLOCK_C1 | binary | Block 1 der CBS Zeitstrahldaten |
| STAT_BLOCK_C2 | binary | Block 2 der CBS Zeitstrahldaten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-cbs-km-per-year"></a>
### STEUERN_CBS_KM_PER_YEAR

Vorgabe Km/Jahr fuer CBS KWP2000 $3B $16

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KM_VALUE | int | CBS Kilometervorgabe in Aufloesung 1000km Gueltige Werte: 0... 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-bos-codierung"></a>
### STEUERN_BOS_CODIERUNG

BOS Codierung fuer alle einzelnen BOS Groessen. Fuer CBS3-Layout.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BOS_ID | int | CBS ID 1..30h |
| BOS_CODIERUNG | int | Codierung passend zu BOS_ID, 0=Anzeige, 1=Sperre, 2=Erprobung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |
| _TEL_ANTWORT2 | binary | Antwort von SG |

<a id="job-steuern-cbs-sc-codierung"></a>
### STEUERN_CBS_SC_CODIERUNG

CBS Servicecall Enable/Disable Codierung. Fuer CBS3-Layout.

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
| _TEL_ANTWORT2 | binary | Antwort von SG |

<a id="job-status-cbs-wochen-km"></a>
### STATUS_CBS_WOCHEN_KM

gibt die Daten des KM pro Woche-Algorithmus aus CBS Betriebsdaten Header aus KWP2000 $21 $B0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WOCHENDURCHSCHNITT_1_WERT | int | Ringspeicher, 1. Wochendurchschnitt in Aufloesung 40km |
| STAT_WOCHENDURCHSCHNITT_2_WERT | int | Ringspeicher, 2. Wochendurchschnitt in Aufloesung 40km |
| STAT_WOCHENDURCHSCHNITT_3_WERT | int | Ringspeicher, 3. Wochendurchschnitt in Aufloesung 40km |
| STAT_WOCHENDURCHSCHNITT_4_WERT | int | Ringspeicher, 4. Wochendurchschnitt in Aufloesung 40km |
| STAT_WOCHENDURCHSCHNITT_5_WERT | int | Ringspeicher, 5. Wochendurchschnitt in Aufloesung 40km |
| STAT_WOCHENDURCHSCHNITT_6_WERT | int | Ringspeicher, 6. Wochendurchschnitt in Aufloesung 40km |
| STAT_WOCHENDURCHSCHNITT_7_WERT | int | Ringspeicher, 7. Wochendurchschnitt in Aufloesung 40km |
| STAT_WOCHENDURCHSCHNITT_8_WERT | int | Ringspeicher, 8. Wochendurchschnitt in Aufloesung 40km |
| STAT_WOCHENDURCHSCHNITT_EINHEIT | string | Einheit der Wochendurchschnitte |
| STAT_QUARTALSDURCHSCHNITT_1_WERT | int | Ringspeicher, 1. Quartalsdurchschnitt in Aufloesung 200km |
| STAT_QUARTALSDURCHSCHNITT_2_WERT | int | Ringspeicher, 2. Quartalsdurchschnitt in Aufloesung 200km |
| STAT_QUARTALSDURCHSCHNITT_3_WERT | int | Ringspeicher, 3. Quartalsdurchschnitt in Aufloesung 200km |
| STAT_QUARTALSDURCHSCHNITT_4_WERT | int | Ringspeicher, 4. Quartalsdurchschnitt in Aufloesung 200km |
| STAT_QUARTALSDURCHSCHNITT_EINHEIT | string | Einheit der Quartalsdurchschnitte |
| STAT_TAGESZAEHLER_WERT | long | Tageszaehler (Kl.30 Stundenzaehler + Offset) |
| STAT_TAGESZAEHLER_EINH | string | immer Tage |
| STAT_AVKM_WW_WERT | long | Kilometer/Woche Wochenwert mit Aufloesung von 10 km |
| STAT_AVKM_WW_EINHEIT | string | immer in km |
| STAT_AVKM_QW_WERT | long | Kilometer/Woche Quartalswert mit Aufloesung von 10 km |
| STAT_AVKM_QW_EINHEIT | string | immer in km |
| STAT_WOCHENZAEHLER | long | Wochenzaehler zur Initialisierung des Wochen-Ringspeichers |
| STAT_LETZTE_FAHRWOCHE | int | Woche der letzten Fahrt |
| STAT_LETZTES_FAHRQUARTAL | int | Quartal der letzten Fahrt |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-motortyp"></a>
### MOTORTYP

im Kombi codierten Motortyp ermitteln KWP2000: $22 ReadDataByCommonIdentifier Job ermittelt Motortyp aus Kombi

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| MOTORTYP | int | Typ des Motors (0...3): . 0 = Otto . 1 = Gas (Vorhalt) . 2 = Diesel . 3 = Vorhalt oder Fehler Achtung: . Ergebnis ist nur korrekt, wenn der . Motortyp im Kombi korrekt codiert ist! |
| TACHOGRENZE | unsigned int | aus Kombi ermittelte maximaler Tachowert in km/h |
| ACCGRENZE | unsigned int | aus Kombi ermittelter ACC-Endwert in km/h Fehlerwert wenn kein ACC-Zeiger verbaut ist: 0xFFFF = -1 |
| DREHZAHLGRENZE | unsigned int | aus Kombi ermittelte maximale Drehzahl in 1/min |
| VWF_UNTERGRENZE | unsigned int | aus Kombi ermittelte Minimalwert in 1/min |
| VWF_OBERGRENZE | unsigned int | aus Kombi ermittelte Maximalwert in 1/min |
| KVAGRENZE | real | aus Kombi ermittelte maximale KVA-Wert in l/100km Fehlerwert wenn kein KVA-Zeiger verbaut ist: 0xFFFF als real |
| OELTEMP_MIN | unsigned int | aus Kombi ermittelte minimalere Wert der Oeltemperatur in Grad C Fehlerwert wenn kein Oeltemp-Zeiger verbaut ist: 0xFFFF |
| OELTEMP_MAX | unsigned int | aus Kombi ermittelte maximalere Wert der Oeltemperatur in Grad C Fehlerwert wenn kein Oeltemp-Zeiger verbaut ist: 0xFFFF |
| _TEL_ANTWORT | binary | Antwort von SG (abhaengig von den ermittelten Groessen) |

<a id="job-steuern-testbitmap"></a>
### STEUERN_TESTBITMAP

Testbitmap im Display darstellen KWP2000: $30 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BILD | int | Bildauswahl (0...10) .  0 = Schachbrett .  1 = Schachbrett invers .  2 = Graustufenverlauf .  3 = Graustufenverlauf integral .  4 = Positionsrahmen .  5 = Zeilen .  6 = Spalten .  7 = Graustufe 3 (hell) .  8 = Graustufe 2 .  9 = Graustufe 1 . 10 = Graustufe 0 (dunkel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-steuern-testbitmap-aus"></a>
### STEUERN_TESTBITMAP_AUS

Testbitmap im Display wieder abschalten KWP2000: $30 InputOutputControlByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-checkcontrol-history"></a>
### STATUS_CHECKCONTROL_HISTORY

CC-Meldungsspeicher aus Kombi lesen KWP2000: $21, $0F

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CC_ID | int | ID der CC-Meldung |
| STAT_GWSZ_STAND_WERT | unsigned int | Kilometerstand beim Auftreten der CC-Meldung Aufloesung: 8km HINWEIS: als Wert wird maximal 524280 ausgegeben. |
| STAT_GWSZ_STAND_EINH | string | Einheit des GWSZ-Standes HINWEIS: immer km |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bos-codierung"></a>
### STATUS_BOS_CODIERUNG

BOS Codierung fuer alle einzelnen BOS Groessen. Fuer CBS3-Layout.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BOS_ID | int | BOS ID 1..30h |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BOS_CODIERUNG | int | Codierung passend zu BOS_ID, 0=Anzeige, 1=Sperre, 2=Erprobung, 3= ungueltig/Fehler |
| _TEL_ANTWORT | binary | Antwort von SG |

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

<a id="job-status-ki"></a>
### STATUS_KI

Liest Block.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BLOCK | binary | Inhalt des Blocks. |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-lesen-ringbuf"></a>
### LESEN_RINGBUF

Liest den Ringbuffer Inhalt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-ringbuf-init"></a>
### RINGBUF_INIT

Initialisiert den Ringbuffer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-lesen-codierblock"></a>
### LESEN_CODIERBLOCK

Codierdatenblock aus EEPROM auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HIGHBYTE | int | Highbyte der Blocknummer Eingabe als HEX: 0xFF |
| LOWBYTE | int | Lowbyte der Blocknummer Eingabe als HEX: 0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CODIERBLOCK | binary | Inhalt des Codierdatenblocks als HEX Folge |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |

<a id="job-csumbl-3001"></a>
### CSUMBL_3001

Checksumme in Block 3001 berechnen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Antwort von SG |
| _TEL_ANTWORT2 | binary | Antwort von SG |
| _TEL_ANTWORT3 | binary | Antwort von SG |

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
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [CBSKENNUNG](#table-cbskennung) (16 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (11 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (70 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (15 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (11 × 9)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [INQ_LST](#table-inq-lst) (12 × 2)
- [RDA_LST](#table-rda-lst) (10 × 2)
- [KRIT_LST](#table-krit-lst) (3 × 2)
- [ID_LST](#table-id-lst) (2 × 2)
- [AL_ID_LST](#table-al-id-lst) (3 × 2)
- [AL_ID_SARS_LST](#table-al-id-sars-lst) (4 × 2)
- [AL_ID_KO_LST](#table-al-id-ko-lst) (5 × 2)
- [AL_ID_CS_LST](#table-al-id-cs-lst) (5 × 2)
- [RINGBUF_CODES](#table-ringbuf-codes) (26 × 2)

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

<a id="table-cbskennung"></a>
### CBSKENNUNG

Dimensions: 16 rows × 3 columns

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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 11 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x01 | DATEN_INKONSISTENT |
| 0x02 | ERROR_ANZAHL_ARGUMENTE |
| 0x03 | ERROR_BEREICH_ARGUMENTE |
| 0x04 | ERROR_ARGUMENT |
| 0x05 | ERROR_ZEIGER_NICHT_VORHANDEN |
| 0x06 | ERROR_PARAMETER_FALSCH |
| 0x07 | ERROR_PARAMETER_CODIERUNG_FALSCH |
| 0x08 | ERROR_PARAMETER_ID_FALSCH |
| 0x09 | ERROR_SW_VERSION |
| 0x0A | ERROR_EEPROM_DATEN |
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

Dimensions: 70 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x9312 | Energiesparmode aktiv |
| 0x9313 | TEMPERATURFUEHLER_LCD |
| 0x9314 | Kurzschluss Kombitaster |
| 0x9315 | GWSZ_FEHLER_CAS_ODER_KOMBI |
| 0x9316 | GWSZ_FEHLER_EEPROM |
| 0x9317 | EEPROM: Fehler Codierdaten BMW |
| 0x9319 | HEBELGEBER1 |
| 0x931A | HEBELGEBER2 |
| 0x931B | AUSSENTEMPERATURSENSOR |
| 0x931C | KURZSCHUSS_DISPLAYHEIZUNG |
| 0x931D | BORDNETZSPANNUNG, UEBERSPANNUNG ODER UNTERSPANNUNG |
| 0x931E | EEPROM: Fehler Codierdaten Lieferant |
| 0xA3A8 | CAN_NO ID |
| 0xA3A9 | CAN_ID_1EE_ERROR_Ausfall_Botschaft_LSS |
| 0xA3AA | CAN_ID_1D2_ERROR_Botschaft_Getriebedaten |
| 0xA3AB | CAN_ID_190_ERROR_Ausfall_Botschaft_Anzeige_ACC |
| 0xA3AC | CAN_ID_1A6_ERROR_Ausfall_Botschaft_Wegstrecke |
| 0xA3AD | CAN_ID_1D0_ERROR_Ausfall_Botschaft_Motordaten |
| 0xA3AE | CAN_ID_0AA_ERROR_Ausfall_Botschaft_Drehzahl_Leerlauf |
| 0xA3AF | CAN_ID_200_ERROR_Ausfall_Botschaft_Regelgeschw_Stufentempomat |
| 0xA3B0 | CAN_ID_202_ERROR_Ausfall_Botschaft_Dimmung |
| 0xA3B1 | CAN_ID_1F6_ERROR_Ausfall_Botschaft_Blinken |
| 0xA3B2 | CAN_ID_130_ERROR_Ausfall_Botschaft_Klemmenstatus |
| 0xA3B3 | CAN_ID_0BE_ERROR_Ausfall_Botschaft_ARS_Alive_Zaehler_oder_SFY |
| 0xA3B4 | CAN_ID_21A_ERROR_Ausfall_Botschaft_Lampenzustand |
| 0xA3B6 | CAN_ID_5C0_ERROR_Ausfall_Botschaft_CAS_Antwort_RDA_DATEN_fehlen |
| 0xA3B9 | CAN_ID_19E_ERROR_Ausfall_Botschaft_Status_DSC |
| 0xA3BB | CAN_ID_2FC_ERROR_Ausfall_Botschaft_ZV_Klappenzustand |
| 0xA3BC | NO_ANSWER_TO_REQUEST (580h+60h) |
| 0xA3BD | CAN_ID_0C0_ERROR_Ausfall_Botschaft_Alive_Zentrales_Gateway |
| 0xA3BE | CAS_AUSFALL_NETZWERKMANAGMENT |
| 0xA3C0 | AHM_AUSFALL_NETZWERKMANAGMENT |
| 0xA3C1 | LM_AUSFALL_NETZWERKMANAGMENT |
| 0xA3C3 | RDC_AUSFALL_NETZWERKMANAGMENT |
| 0xA3C4 | ID_Ausfall oder Alive ACC |
| 0xA3C5 | ID_Ausfall oder Alive SFY |
| 0xA3C6 | Konsistenzfehler Getriebeposition |
| 0xA3C7 | Luftfeder_AUSFALL_NETZWERKMANAGMENT |
| 0xA548 | ID_Ausfall 1FCh AFS |
| 0xA549 | ID_Ausfall 315h Fahrzeugmodus |
| 0xA54A | Checksummenfehler Antwort CAS auf CAN-Anfrage ID 394h |
| 0xA54D | ID_Ausfall oder Alive EKP |
| 0xA54E | ID_Ausfall oder Alive Sitzlehnenverriegelung Fahrer |
| 0xA54F | ID_Ausfall oder Alive Sitzlehnenverriegelung Beifahrer |
| 0xA550 | ID_Ausfall 1A0h Geschwindigkeit |
| 0xA553 | CBS-EEPROM-Lesefehler |
| 0xA554 | Alive Telefon |
| 0xA555 | Sitzbelegung Gurtkontakte |
| 0xA556 | Ausfall HDC-Anzeige |
| 0xA557 | Debuginfo Kombi |
| 0xA559 | Klemme30g_f_Abschaltung |
| 0xA55A | ID_Ausfall oder Alive TLC |
| 0xA55B | ID_Ausfall oder Alive Airbag |
| 0xA55C | WD Anzeige Abschaltung |
| 0xA55D | Fehler Anzeige Getriebeposition |
| 0xA55E | WD Fehler |
| 0xA560 | ID_Ausfall Anzeige shift indicator |
| 0xE104 | CAN LOW ERROR |
| 0xE105 | CAN HIGH ERROR |
| 0xE106 | GROUND SHIFT ERROR |
| 0xE107 | CAN BUS OFF |
| 0xE13C | CAN Fehlerwert_erhalten |
| 0xE13D | CAN unplausibles_Signal |
| 0xE13E | CAN Telegramm_Timeout |
| 0xE13F | CAN Fehler_Empfang_NM-Botschaft |
| 0xE140 | CAN Fehler_von_KI_gesendet |
| 0xE141 | CAN unplausibles_Signal_gesendet |
| 0xE142 | CAN Telegramm_Timeout_senden |
| 0xE143 | CAN Fehler_Senden_NM-Botschaft |
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

Dimensions: 15 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x9317 | 0x01 | 0x09 | - | - |
| 0x931E | 0x01 | 0x09 | - | - |
| 0xA3AA | 0x01 | 0x0D | - | - |
| 0xA3AB | 0x01 | 0x0C | - | - |
| 0xA3AD | 0x01 | 0x0B | - | - |
| 0xA3B3 | 0x01 | 0x0E | - | - |
| 0xA3B6 | 0x10 | - | - | - |
| 0xA3B9 | 0x01 | 0x0B | - | - |
| 0xA3BC | 0x1A | - | - | - |
| 0xA3BD | 0x01 | 0x0B | - | - |
| 0xA548 | 0x01 | 0x0B | - | - |
| 0xA54D | 0x01 | 0x0B | - | - |
| 0xA54E | 0x01 | 0x0B | - | - |
| 0xA54F | 0x01 | 0x0B | - | - |
| default | 0x01 | 0xFE | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 11 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | BORDNETZSPANNUNG | VOLT | - | u c | - | 1 | 10 | 0 |
| 0x09 | Fehlerschwere | 0-n | - | 0x0F | KRIT_LST | - | - | - |
| 0x0A | Botschaftenfehler | 0-n | - | 0xFF | ID_LST | - | - | - |
| 0x0B | Botschaftenfehler | 0-n | - | 0xFF | AL_ID_LST | - | - | - |
| 0x0C | Botschaftenfehler | 0-n | - | 0xFF | AL_ID_CS_LST | - | - | - |
| 0x0D | Botschaftenfehler | 0-n | - | 0xFF | AL_ID_KO_LST | - | - | - |
| 0x0E | Botschaftenfehler | 0-n | - | 0xFF | AL_ID_SARS_LST | - | - | - |
| 0x10 | Fehler RDA | 0-n | h | 0xFFFF | RDA_LST | - | - | - |
| 0x1A | Anfrage unbeantwortet | 0-n | h | 0xFFFF | INQ_LST | - | - | - |
| 0xFE | OHNE BEDEUTUNG | 1 | - | u c | - | 1 | 1 | 0 |
| 0xXY | UNBEKANNTE UW | 1 | - | s l | - | 1 | 1 | 0 |

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

<a id="table-inq-lst"></a>
### INQ_LST

Dimensions: 12 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 570 | Status Funkschluessel |
| 752 | Status Klima Standfunktion |
| 759 | Einheiten |
| 787 | Status Service Call Teleservice |
| 822 | Anzeige CC-Meldung |
| 860 | Status Bordcomputer |
| 864 | Daten Bordcomputer |
| 896 | Fahrgestellnummer |
| 897 | Elektronischer Oelmessstab |
| 904 | Fahrzeugtyp |
| 65535 | Signal ungueltig |
| xy | Eintrag unplausibel |

<a id="table-rda-lst"></a>
### RDA_LST

Dimensions: 10 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0001 | GWSZ |
| 0x0002 | ZUENDKERZEN |
| 0x0004 | SICHTPRUEFUNG |
| 0x0008 | BREMSFLUESSIGKEIT |
| 0x0010 | KUEHLWASSER |
| 0x0020 | HU |
| 0x0040 | AU |
| 0x0080 | INTERVALL VERKUERZUNG |
| 0x0100 | INTERVALL VERKUERZUNG |
| xy | Eintrag unplausibel |

<a id="table-krit-lst"></a>
### KRIT_LST

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0 | kritischer Fehler |
| 0x1 | unkritischer Fehler |
| xy | Eintrag unplausibel |

<a id="table-id-lst"></a>
### ID_LST

Dimensions: 2 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | keine ID |
| xy | Eintrag unplausibel |

<a id="table-al-id-lst"></a>
### AL_ID_LST

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | keine ID |
| 0x02 | ALIVE Fehler |
| xy | Eintrag unplausibel |

<a id="table-al-id-sars-lst"></a>
### AL_ID_SARS_LST

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | keine ID |
| 0x02 | ALIVE Fehler Sicherheitssystem |
| 0x04 | ALIVE Fehler ARS |
| xy | Eintrag unplausibel |

<a id="table-al-id-ko-lst"></a>
### AL_ID_KO_LST

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | keine ID |
| 0x02 | ALIVE Fehler |
| 0x04 | Komplement Fehler |
| 0x08 | Konsistenzfehler |
| xy | Eintrag unplausibel |

<a id="table-al-id-cs-lst"></a>
### AL_ID_CS_LST

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | keine ID |
| 0x02 | ALIVE Fehler |
| 0x04 | Checksummen Fehler |
| 0x08 | Signalfehler |
| xy | Eintrag unplausibel |

<a id="table-ringbuf-codes"></a>
### RINGBUF_CODES

Dimensions: 26 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xF100 | Normal reset |
| 0xE101 | Reset without clock |
| 0xD102 | Watchdog reset |
| 0xE401 | Stack size 75 |
| 0xE301 | Stack size 90 |
| 0xC103 | Power on reset |
| 0xB104 | HW standby reset |
| 0xA105 | External pin reset |
| 0x9106 | Reset-bit reset |
| 0xF200 | Power fail |
| 0xF500 | Read length overflow |
| 0xE501 | Write length overflow |
| 0xD502 | ODO invalid |
| 0xC503 | Application length error |
| 0xB504 | Start address out of range |
| 0xA505 | Write 1st verify fail |
| 0x9506 | Write max verify fail |
| 0x8007 | Address error ID 0 |
| 0x8207 | Size error ID 0 |
| 0x8407 | Content error ID 0 |
| 0xF600 | Read command from TST error |
| 0xE601 | Write command from TST error |
| 0xD602 | Read for TST error |
| 0xC603 | Write for TST error |
| 0xB604 | CC message 60 set by error |
| xy | unbekannter Eintrag |
