# MSS70.prg

- Jobs: [365](#jobs)
- Tables: [70](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MSS70 fuer S54  |
| ORIGIN | BMW ZS-M-57 Dr. Wittmack |
| REVISION | 1.003 |
| AUTHOR | BMW ZS-M-57 Dr. Wittmack, VFTIS EA-24 Ruff, VFTIS EA-24 Ginella |
| COMMENT | SGBD für MSS70 B-Muster  |
| PACKAGE | 1.29 |
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
- [HS_LESEN](#job-hs-lesen) - Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default
- [HS_LOESCHEN](#job-hs-loeschen) - Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [STATUS_MESSWERTBLOCK_LESEN](#job-status-messwertblock-lesen) - Lesen eines Messwertblockes Es muss immer das BlockSchreibenFlag und mindestens ein MESSWERT uebergeben werden. KWP2000: $2C DynamicallyDefinedLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier $04 ClearDynamicallyDefinedLocalIdentifier KWP2000: $2C DynamicallyDefinedLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier $02 DefineByCommonIdentifier KWP2000: $21 ReadDataByLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier Modus  : Default
- [CBS_INFO](#job-cbs-info) - Ausgabe der CBS-Version
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (fuer CBS-Version 4) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS-Version 4) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)
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
- [_STATUS_OBD_MODE_01](#job-status-obd-mode-01) - Auslesen der Motor-Diagnosedaten nach Mode 01 PID 01  
- [_STATUS_OBD_MODE_03](#job-status-obd-mode-03) - Auslesen der P-Codes nach Mode 3  
- [_STATUS_OBD_MODE_07](#job-status-obd-mode-07) - Auslesen der P-Codes nach Mode 7  
- [SET_BAUDRATE](#job-set-baudrate) - Initialisierung der Kommunikationsparameter mit bestimmter Baudrate
- [SET_PARAMETER](#job-set-parameter) - Aenderung der Kommunikationsparameter bei Long-Parametersätzen
- [INTERFACETYPE](#job-interfacetype) - Interface-Typ bestimmen und ausgeben Es wird der Name des Interfaces übergeben Wichtig für Baudratenumschaltung weil bei ADS, EADS und OBD sind nur 115200 Baud möglich, bei EDIC nur 125000 Baud möglich
- [ACCESS_TIMING_PARAMETER](#job-access-timing-parameter) - Aenderung der Timingparameter im SG
- [ACCESS_TIMING_PARAMETER_DEFAULT](#job-access-timing-parameter-default) - Default-Timingparameter im SG
- [FS_LESEN_HEX](#job-fs-lesen-hex) - Fehlerspeicher auslesen als Hex Dump
- [MESSWERTBLOCK_LESEN](#job-messwertblock-lesen) - $2C F0 02 DDLI Messwerte aus Übergabestring definieren
- [STATUS_MESSWERTE_VANOS](#job-status-messwerte-vanos) - $2C F0 02 DDLI Messwerte CAM_IN und CAM_EX auf Wunsch von VS-22
- [FS_LESEN_FREEZE_FRAME](#job-fs-lesen-freeze-frame) - Fehlerspeicher auslesen mit SAE Werten Umwelt und P-Code
- [STATUS_MESSWERTE_KD](#job-status-messwerte-kd) - $2C F0 02 DDLI Messwerte nach Wunsch VS-22
- [IDENT_AIF](#job-ident-aif) - Identdaten mit KWP2000: $1A ReadECUIdentification Anwender Informations Felder mit KWP 2000: $23 ReadMemoryByAddress
- [STATUS_OBD](#job-status-obd) - $21 05 Monitoring Funktionen und Status Bits
- [STATUS_READINESS](#job-status-readiness) - $21 05 Monitoring Funktionen und Status Bits
- [EWS_EMPFANG](#job-ews-empfang) - EWS-Empfangsstatus auslesen
- [STATUS_FGR](#job-status-fgr) - $21 07 MFL MultiFunktionsLekrad STATE_MSW_CAN
- [DISTANCE_MIL_ON](#job-distance-mil-on) - Auslesen Fahrstrecke mit MIL-eingeschaltet KWP 2000* $21 09 DIST_ACT_MIL ReadDataByLocalIdentifier
- [STATUS_SYSTEMCHECK_SEK_LUFT](#job-status-systemcheck-sek-luft) - Stand der Diagnose KWP 2000* $21 20 Status Systemtest SLS SekundärLuftSystem
- [STATUS_SYSTEMCHECK_TEV_FUNC](#job-status-systemcheck-tev-func) - Status und Messströme KWP 2000* $21 22 RequestRoutineResultsByLocalIdentifier
- [STATUS_SYSTEMCHECK_TEV](#job-status-systemcheck-tev) - Stand der Diagnose KWP 2000* $21 22 TEV ReadDataByLocalIdentifier
- [STATUS_SYSTEMCHECK_EVAUSBL](#job-status-systemcheck-evausbl) - welches EV-Ventil ist abgeschaltet KWP 2000* $21 25 RequestRoutineResultsByLocalIdentifier
- [STATUS_SYSTEMCHECK_VVT_ANSCHLAG](#job-status-systemcheck-vvt-anschlag) - Stand der Diagnose KWP 2000* $21 27 VVT ReadDataByLocalIdentifier
- [STATUS_DIGITAL_3](#job-status-digital-3) - Statusbit KOmpressorRELais KWP 2000* $21 36 LV_ACCOUT_RLY ReadDataByLocalIdentifier
- [STATUS_DIGITAL_4](#job-status-digital-4) - Statusbit LeerLauf KWP 2000* $21 3F LV_IS ReadDataByLocalIdentifier
- [STATUS_L_SONDE_HEIZUNG_H_2](#job-status-l-sonde-heizung-h-2) - Auslesen des Reglerzustands der Sondenheizung KWP 2000* $21 41 STATE_LSH_DOWN_2 ReadDataByLocalIdentifier
- [STATUS_L_SONDE_HEIZUNG_H_1](#job-status-l-sonde-heizung-h-1) - Auslesen des Reglerzustands der Sondenheizung KWP 2000* $21 42 STATE_LSH_DOWN_1 ReadDataByLocalIdentifier
- [STATUS_L_SONDE_HEIZUNG_V_2](#job-status-l-sonde-heizung-v-2) - Auslesen des Reglerzustands der Sondenheizung KWP 2000* $21 43 STATE_LSH_UP_2 ReadDataByLocalIdentifier
- [STATUS_L_SONDE_HEIZUNG_V_1](#job-status-l-sonde-heizung-v-1) - Auslesen des Reglerzustands der Sondenheizung KWP 2000* $21 44 STATE_LSH_UP_1 ReadDataByLocalIdentifier
- [STATUS_EWS_LOCK](#job-status-ews-lock) - Statusbit LV_LOCK_IMOB = 1 blockt Zündung und Einspritzung KWP 2000* $21 49 ReadDataByLocalIdentifier
- [STATUS_ZEIT_EINSPRITZ](#job-status-zeit-einspritz) - Auslesen der Einspritzzeit Zyl. 1 KWP 2000* $21 4C BIOS_TI_0
- [STATUS_ZUENDWINKEL](#job-status-zuendwinkel) - Auslesen des Zündwinkels Zylinder 1 KWP 2000* $21 56 IGA_IGC_0 ReadDataByLocalIdentifier
- [STATUS_DROSSELKLAPPE](#job-status-drosselklappe) - Auslesen des Drosselklappen Winkels KWP 2000* $21 57 TPS_AV ReadDataByLocalIdentifier
- [STATUS_KLOPFEN](#job-status-klopfen) - Auslesen des Status Klopfen erkannt 0/1 KWP 2000* $21 71 LV_KNK ReadDataByLocalIdentifier
- [STATUS_KVA](#job-status-kva) - Auslesen Faktor KVA KWP 2000* $21 C1 kva-faktor ReadDataByLocalIdentifier
- [STATUS_BETRIEBSSTUNDENZAEHLER](#job-status-betriebsstundenzaehler) - $ 21 C3 Status Betriebsstundenzaehler auslesen
- [STATUS_SYSTEMCHECK_DMTL](#job-status-systemcheck-dmtl) - Stand der Diagnose KWP 2000* $21 DA DMTL ReadDataByLocalIdentifier
- [STATUS_SYSTEMCHECK_L_SONDE](#job-status-systemcheck-l-sonde) - Stand der Diagnose KWP 2000* $21 DF vertauschte L-Sonden ReadDataByLocalIdentifier
- [STATUS_LEISTUNGSSTUFE](#job-status-leistungsstufe) - Auslesen der Codierung Obere/Untere Leistungsstufe KWP2000: $22 ReadDataByCommonIdentifier $3020 RecordCommonIdentifier
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Auslesen der Motordrehzahl und LL-Sollwert KWP 2000* $22 40 00 Auszug
- [STATUS_DFMONITOR](#job-status-dfmonitor) - Generator Belastung KWP2000: $22 40 01 ReadDataByCommonIdentifier dfmonitor
- [STATUS_DIGITAL_1](#job-status-digital-1) - Status Schaltzustaende
- [STATUS_MOTORLAUFUNRUHE](#job-status-motorlaufunruhe) - $22 40 03 Laufunruhe fuer 6 Zylinder lesen
- [STATUS_GEBERRAD_ADAPTION](#job-status-geberrad-adaption) - $2C F0 02 DDLI Messwerte für NWG-Adaptionen auslesen
- [STATUS_NOCKENWELLE_ADAPTION](#job-status-nockenwelle-adaption) - $22 40 06 Nockenwellen Adaptionen
- [STATUS_DIGITAL_0](#job-status-digital-0) - Status Schaltzustaende $22 40 07 Betriebszustaende
- [STATUS_FUNKTIONS](#job-status-funktions) - Status Schaltzustaende $22 40 07 Betriebszustaende
- [STATUS_ADAPTION_DK](#job-status-adaption-dk) - $22 40 08 Adaption DK lesen
- [STATUS_ADAPTION_GEMISCH](#job-status-adaption-gemisch) - $22 40 0A Adaption Lambda Regelung lesen
- [STATUS_FASTA_COMMON](#job-status-fasta-common) - Messwerteblock lesen KWP2000: $2C F0 02 DynamicallyDefinedLocalIdentifier
- [ECU_CONFIG](#job-ecu-config) - $22 5F F2 Fahrzeug Varianten lesen
- [SPEICHER_LESEN_ASCII](#job-speicher-lesen-ascii) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [ECU_CONFIG_RESET](#job-ecu-config-reset) - $22 5F F2 04 gelernte FahrzeugVarianten löschen
- [STATUS_ADD](#job-status-add) - Auslesen der additiven Korrektur Bank 1 KWP 2000*  MFF_AD_ADD_MMV_REL[1]
- [STATUS_ADD_2](#job-status-add-2) - Auslesen der additiven Korrektur Bank 2 KWP 2000*  MFF_AD_ADD_MMV_REL[2]
- [STATUS_MUL](#job-status-mul) - Auslesen des Korrekturfaktors Bank 1 KWP 2000*  MFF_AD_FAC_MMV_REL[1]
- [STATUS_MUL_2](#job-status-mul-2) - Auslesen des Korrekturfaktors Bank 1 KWP 2000*  MFF_AD_FAC_MMV_REL[2]
- [STATUS_INT](#job-status-int) - Auslesen des Integrator Bank 1 KWP 2000*  TI_LAM_COR[1]
- [STATUS_INT_2](#job-status-int-2) - Auslesen des Integrator Bank 1 KWP 2000*  TI_LAM_COR[1]
- [STATUS_LL_ABGLEICH](#job-status-ll-abgleich) - LL-Abgleichswerte lesen
- [STEUERN_LL_ABGLEICH](#job-steuern-ll-abgleich) - LL-Abgleich vorgegeben -256 bis +254
- [STEUERN_LLABG_PROG](#job-steuern-llabg-prog) - LL-Abgleichswerte werden vorgegeben
- [FLASH_CRC_PRUEFEN](#job-flash-crc-pruefen) - Codier Checksumme pruefen KWP2000: $31 StartRoutineByLocalIdentifier $01 Checksum
- [DME_STARTWERT_ABGLEICH](#job-dme-startwert-abgleich) - Kopiert die ISN auf beide Wechselcodes KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $20 Modus  : Default
- [START_SYSTEMCHECK_SEK_LUFT](#job-start-systemcheck-sek-luft) - $31 20 Systemdiagnose SLS SekundärLuftSystem starten
- [START_SYSTEMCHECK_TEV_FUNC](#job-start-systemcheck-tev-func) - $31 22 Systemdiagnose TEVstarten
- [START_SYSTEMCHECK_EVAUSBL](#job-start-systemcheck-evausbl) - $31 25 Systemdiagnose Einspritzventil abschalten
- [START_SYSTEMCHECK_LLERH](#job-start-systemcheck-llerh) - $31 26 Systemdiagnose EOL LL-Erhöhen starten
- [START_SYSTEMCHECK_VVT_ANSCHLAG](#job-start-systemcheck-vvt-anschlag) - $31 27 Systemdiagnose VVT-Anschläge lernen starten
- [EWS_STARTWERT](#job-ews-startwert) - EWS-Startwertinitialisierung
- [START_SYSTEMCHECK_L_REGELUNG_AUS](#job-start-systemcheck-l-regelung-aus) - $31 D9 01 Systemdiagnose LambdaRegelung abschalten
- [STOP_SYSTEMCHECK_L_REGELUNG_AUS](#job-stop-systemcheck-l-regelung-aus) - $31 D9 01 Systemdiagnose LambdaRegelung einschalten
- [START_SYSTEMCHECK_DMTL](#job-start-systemcheck-dmtl) - $31 DA Systemdiagnose DMTL starten
- [START_SYSTEMCHECK_L_SONDE](#job-start-systemcheck-l-sonde) - $31 DF Systemdiagnose vertauschte L-Sonden starten
- [RESET_CRU_OFF](#job-reset-cru-off) - $31 F4 STATE_CRU_OFF_IRR und STATE_CRU_OFF_REV löschen
- [START_SYSTEMCHECK_VVT_SOLLWERT](#job-start-systemcheck-vvt-sollwert) - $31 FE Systemdiagnose VVT Steuerung ueber CAN freigeben
- [STOP_SYSTEMCHECK_VVT_SOLLWERT](#job-stop-systemcheck-vvt-sollwert) - $31 FE Systemdiagnose VVT Steuerung ueber CAN freigeben
- [STOP_SYSTEMCHECK_SEK_LUFT](#job-stop-systemcheck-sek-luft) - $32 20 Systemdiagnose SekundärLuftSystem beenden
- [STOP_SYSTEMCHECK_TEV_FUNC](#job-stop-systemcheck-tev-func) - $32 22 Systemdiagnose TEV beenden
- [STOP_SYSTEMCHECK_EVAUSBL](#job-stop-systemcheck-evausbl) - $32 25 Ende Systemtest Ventil Abschalten
- [STOP_SYSTEMCHECK_LLERH](#job-stop-systemcheck-llerh) - $32 26 EOL-Test LL-Anheben beenden
- [STOP_SYSTEMCHECK_VVT_ANSCHLAG](#job-stop-systemcheck-vvt-anschlag) - $32 27 Systemdiagnose VVT-Anschläge lernen starten
- [STOP_SYSTEMCHECK_DMTL](#job-stop-systemcheck-dmtl) - $32 DA Systemdiagnose DMTL beenden
- [STOP_SYSTEMCHECK_L_SONDE](#job-stop-systemcheck-l-sonde) - $32 DF Systemdiagnose vertauschte L-Sonden beenden
- [STATUS_SYSTEMCHECK_SEK_LAMBDA_WERT](#job-status-systemcheck-sek-lambda-wert) - Status und Luftmassen KWP 2000* $33 20 RequestRoutineResultsByLocalIdentifier 
- [STATUS_SYSTEMCHECK_TEV_WERT](#job-status-systemcheck-tev-wert) - Status und Messströme KWP 2000* $33 22 RequestRoutineResultsByLocalIdentifier
- [STATUS_SYSTEMCHECK_LLERH_WERT](#job-status-systemcheck-llerh-wert) - aktuelle Drehzahl N KWP 2000* $33 26 RequestRoutineResultsByLocalIdentifier
- [STATUS_SYSTEMCHECK_DMTL_WERT](#job-status-systemcheck-dmtl-wert) - Status und Messströme KWP 2000* $33 DA RequestRoutineResultsByLocalIdentifier
- [STATUS_SYSTEMCHECK_L_SONDE_WERTE](#job-status-systemcheck-l-sonde-werte) - Status und Messwerte KWP 2000* $33 DF RequestRoutineResultsByLocalIdentifier
- [STEUERN_KVA](#job-steuern-kva) - Faktor KVA Korrektur vorgeben KWP 2000* $3B C1 kva-faktor WriteDataByLocalIdentifier
- [STATUS_ANALOG](#job-status-analog) - Analogen Messwert periodisch lesen KWP2000: $2C F0 02 DynamicallyDefinedLocalIdentifier
- [STATUS_FASTA2](#job-status-fasta2) - $2C F0 02 DDLI Messwerte nach Wunsch EA-36
- [STATUS_MESSWERTE_NL](#job-status-messwerte-nl) - $2C F0 02 DDLI Messwerte Klopfen nach Wunsch VS-22
- [STATUS_MESSWERTBLOCK_ADC](#job-status-messwertblock-adc) - $21 F0 DDLI Messwerteblock lesen der zuletzt mit $2C F0 definiert wurde
- [IDENT_IBS](#job-ident-ibs) - $22 40 21 BMW Nr, Seriennummer, SW/HW Index
- [STATUS_SYSTEMCHECK_PM_INFO_1](#job-status-systemcheck-pm-info-1) - $22 40 22 Bytefeld 1 Batterie Powermanagement lesen
- [STATUS_SYSTEMCHECK_PM_INFO_2](#job-status-systemcheck-pm-info-2) - $22 40 23 Bytefeld 2 Batterie Powermanagement lesen
- [STEUERN_PM_HISTOGRAM_RESET](#job-steuern-pm-histogram-reset) - $30 F5 04 Loeschen von pminfo1 index 23-30
- [ADAP_SELEKTIV_LOESCHEN](#job-adap-selektiv-loeschen) - Löschen von Adaptionen und gelernte Varianten KWP 2000 $31 30 xx xx xx Loeschen der Adaptionswerte
- [STEUERN_BATTERIETAUSCH_REGISTRIEREN](#job-steuern-batterietausch-registrieren) - KWP 2000 $31 30 00 10 00 Bit setzen Batterietausch registrieren
- [START_SYSTEMCHECK_PM_MESSEMODE](#job-start-systemcheck-pm-messemode) - $31 F6 Systemdiagnose BatterieSensor reset
- [STOP_SYSTEMCHECK_PM_MESSEMODE](#job-stop-systemcheck-pm-messemode) - $32 F6 Systemdiagnose BatterieSensor reset beenden
- [FLASH_PARAMETER_LESEN](#job-flash-parameter-lesen) - Gibt die SG-spezifischen Flash-Parameter zurück
- [FLASH_PARAMETER_SETZEN](#job-flash-parameter-setzen) - Setzt die SG-spezifischen Flash-Parameter
- [INNENTEMP_LESEN](#job-innentemp-lesen) - 0x301001     Steuergeraete-Innentemperatur auslesen NO_CON keine Vorraussetzungen
- [STATUS_AGK](#job-status-agk) - 0x30C101     Abgasklappe auslesen NO_CON keine Vorraussetzungen
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - 0x300A01     Ansauglufttemperatur 1 auslesen NO_CON keine Vorraussetzungen
- [STATUS_ANWS](#job-status-anws) - 0x30EE01     Vanos Auslass Ventil auslesen NO_CON keine Vorraussetzungen
- [STATUS_ANWSF](#job-status-anwsf) - 0x30A201     Ventil Vanos Auslass Frueh auslesen NO_CON keine Vorraussetzungen
- [STATUS_ANWSS](#job-status-anwss) - 0x30A301     Ventil Vanos Auslass Spaet auslesen NO_CON keine Vorraussetzungen
- [STATUS_AVS](#job-status-avs) - 0x30C001     Absperrventil Saugstrahlpumpe auslesen NO_CON keine Vorraussetzungen
- [STATUS_BLS](#job-status-bls) - 0x300201     Bremslichtschalter auslesen NO_CON keine Vorraussetzungen
- [STATUS_BLTS](#job-status-blts) - 0x300301     Bremslichttestschalter auslesen NO_CON keine Vorraussetzungen
- [STATUS_CO_ABGLEICH](#job-status-co-abgleich) - 0x225FF1     Abgleichwert CO (Kohlenmonoxid) auslesen
- [STATUS_CODIERUNG_IGR](#job-status-codierung-igr) - 0x223210     Codierung fuer IGR (Intelligente Generator-Regelung) auslesen
- [STATUS_CODIERUNG_KAT](#job-status-codierung-kat) - 0x223001     Codierung fuer Katalysator auslesen
- [STATUS_CODIERUNG_MIL](#job-status-codierung-mil) - 0x223000     Codierung fuer MIL (Malfunction Indication Lamp) auslesen
- [STATUS_CODIERUNG_OEL](#job-status-codierung-oel) - 0x223200     Codierung fuer Oelwechselintervall auslesen
- [STATUS_CODIERUNG_VMAX](#job-status-codierung-vmax) - 0x223010     Codierung fuer maximale Geschwindigkeit auslesen
- [STATUS_CODIERUNG_XENON](#job-status-codierung-xenon) - 0x223211     Codierung fuer Xenon-Lichtverbau auslesen
- [STATUS_DFV1A](#job-status-dfv1a) - 0x3328     Auslesen Diagnosefunktion Auslass A-Vanostest 1 (Verstellzeit)
- [STATUS_DFV1E](#job-status-dfv1e) - 0x3323     Auslesen Diagnosefunktion Einlass E-Vanostest 1 (Verstellzeit)
- [STATUS_DFV2A](#job-status-dfv2a) - 0x3329     Auslesen Diagnosefunktion Auslass A-Vanostest 2 (Dichtigkeit)
- [STATUS_DFV2E](#job-status-dfv2e) - 0x3324     Auslesen Diagnosefunktion Einlass E-Vanostest 2 (Dichtigkeit)
- [STATUS_DFVFA](#job-status-dfvfa) - 0x33D3     Auslesen Diagnosefunktion Auslass A-Vanostest Fruehanschlag
- [STATUS_DFVFE](#job-status-dfvfe) - 0x33D1     Auslesen Diagnosefunktion Einlass E-Vanostest Fruehanschlag
- [STATUS_DFVSA](#job-status-dfvsa) - 0x33D4     Auslesen Diagnosefunktion Auslass A-Vanostest Spaetanschlag
- [STATUS_DFVSE](#job-status-dfvse) - 0x33D2     Auslesen Diagnosefunktion Einlass E-Vanostest Spaetanschlag
- [STATUS_DKP_VOLT](#job-status-dkp-volt) - 0x302A01     Drosselklappe auslesen NO_CON keine Vorraussetzungen
- [STATUS_DMTL_HEIZUNG](#job-status-dmtl-heizung) - 0x30CE01     Diagnosemodul-Tank Leckage Heizung auslesen NO_CON keine Vorraussetzungen
- [STATUS_DMTL_P](#job-status-dmtl-p) - 0x30CC01     Diagnosemodul-Tank Leckage Pumpe auslesen NO_CON keine Vorraussetzungen
- [STATUS_DMTL_V](#job-status-dmtl-v) - 0x30CD01     Diagnosemodul-Tank Leckage Ventil auslesen NO_CON keine Vorraussetzungen
- [STATUS_E_LUEFTER](#job-status-e-luefter) - 0x30DA01     E-Luefter auslesen NO_CON keine Vorraussetzungen
- [STATUS_EBL](#job-status-ebl) - 0x30C801     E-Box-Luefter auslesen NO_CON keine Vorraussetzungen
- [STATUS_EISYGD](#job-status-eisygd) - 0x33E1     Auslesen Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403)
- [STATUS_EISYUGD](#job-status-eisyugd) - 0x33E0     Auslesen Eisy-Adaptionswerte (ungedrosselt) (Anforderung aus CP5403)
- [STATUS_EKP](#job-status-ekp) - 0x30D801     Elektrische Kraftstoffpumpe 1 auslesen NO_CON keine Vorraussetzungen
- [STATUS_EML](#job-status-eml) - 0x30D601     EML (Engine Malfunction Lamp) auslesen NO_CON keine Vorraussetzungen
- [STATUS_ENERGIESPARMODE](#job-status-energiesparmode) - 0x22100A     Status Energiesparmode START-8B
- [STATUS_ENWS](#job-status-enws) - 0x30ED01     Vanos Einlass Ventil auslesen NO_CON keine Vorraussetzungen
- [STATUS_ENWSF](#job-status-enwsf) - 0x30A001     Ventil Vanos Einlass Frueh auslesen NO_CON keine Vorraussetzungen
- [STATUS_ENWSS](#job-status-enwss) - 0x30A101     Ventil Vanos Einlass Spaet auslesen NO_CON keine Vorraussetzungen
- [STATUS_EV1](#job-status-ev1) - 0x30E101     Einspritzventil 1 auslesen NO_CON keine Vorraussetzungen
- [STATUS_EV2](#job-status-ev2) - 0x30E201     Einspritzventil 2 auslesen NO_CON keine Vorraussetzungen
- [STATUS_EV3](#job-status-ev3) - 0x30E301     Einspritzventil 3 auslesen NO_CON keine Vorraussetzungen
- [STATUS_EV4](#job-status-ev4) - 0x30E401     Einspritzventil 4 auslesen NO_CON keine Vorraussetzungen
- [STATUS_EV5](#job-status-ev5) - 0x30E501     Einspritzventil 5 auslesen NO_CON keine Vorraussetzungen
- [STATUS_EV6](#job-status-ev6) - 0x30E601     Einspritzventil 6 auslesen NO_CON keine Vorraussetzungen
- [STATUS_EWAP](#job-status-ewap) - 0x30BF01     elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) auslesen NO_CON keine Vorraussetzungen
- [STATUS_FGRL](#job-status-fgrl) - 0x30D501     Fahrgeschwindigkeitsregler-Lampe auslesen NO_CON keine Vorraussetzungen
- [STATUS_FWV1](#job-status-fwv1) - 0x301E01     Fahrerwunschversorgung 1 auslesen NO_CON keine Vorraussetzungen
- [STATUS_FWV2](#job-status-fwv2) - 0x301F01     Fahrerwunschversorgung 2 auslesen NO_CON keine Vorraussetzungen
- [STATUS_GLF](#job-status-glf) - 0x30C301     Gesteuerte Luftfuehrung auslesen NO_CON keine Vorraussetzungen
- [STATUS_HFMS](#job-status-hfms) - 0x302E01     Sekundaerluft HFM (Heissfilm Luftmassenmesser) auslesen NO_CON keine Vorraussetzungen
- [STATUS_KB1](#job-status-kb1) - 0x303001     Klopfbaustein 1 auslesen NO_CON keine Vorraussetzungen
- [STATUS_KB2](#job-status-kb2) - 0x303101     Klopfbaustein 2 auslesen NO_CON keine Vorraussetzungen
- [STATUS_KFT](#job-status-kft) - 0x30C901     Kennfeldthermostat auslesen NO_CON keine Vorraussetzungen
- [STATUS_KGEH](#job-status-kgeh) - 0x30AD01     Kurbelgehaeuseentlueftungsheizung auslesen NO_CON keine Vorraussetzungen
- [STATUS_KOREL](#job-status-korel) - 0x30C701     Klimakompressor-Relais auslesen NO_CON keine Vorraussetzungen
- [STATUS_KRANN](#job-status-krann) - 0x33E3     Auslesen Krann-Adaptionswerte (Anforderung aus CP5404)
- [STATUS_KUP](#job-status-kup) - 0x300401     Kupplungsschalter auslesen NO_CON keine Vorraussetzungen
- [STATUS_L_SONDE](#job-status-l-sonde) - 0x302101     Lambdasonde vor Kat Bank1 auslesen NO_CON keine Vorraussetzungen
- [STATUS_L_SONDE_2](#job-status-l-sonde-2) - 0x302301     Lambdasonde vor Kat Bank2 auslesen NO_CON keine Vorraussetzungen
- [STATUS_L_SONDE_2_H](#job-status-l-sonde-2-h) - 0x302401     Lambdasonde hinter Kat Bank2 auslesen NO_CON keine Vorraussetzungen
- [STATUS_L_SONDE_H](#job-status-l-sonde-h) - 0x302201     Lambdasonde hinter Kat Bank1 auslesen NO_CON keine Vorraussetzungen
- [STATUS_LLS](#job-status-lls) - 0x309F01     Leerlaufsteller auslesen NO_CON keine Vorraussetzungen
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - 0x302501     Luftmassenmesser 1 auslesen NO_CON keine Vorraussetzungen
- [STATUS_LRP](#job-status-lrp) - 0x225FF7     Laufruhepruefung auslesen
- [STATUS_LSH1](#job-status-lsh1) - 0x30D001     Lambdasondenheizung vor Kat Bank1 auslesen NO_CON keine Vorraussetzungen
- [STATUS_LSH2](#job-status-lsh2) - 0x30D101     Lambdasondenheizung hinter Kat Bank1 auslesen NO_CON keine Vorraussetzungen
- [STATUS_LSH3](#job-status-lsh3) - 0x30D201     Lambdasondenheizung vor Kat Bank2 auslesen NO_CON keine Vorraussetzungen
- [STATUS_LSH4](#job-status-lsh4) - 0x30D301     Lambdasondenheizung hinter Kat Bank2 auslesen NO_CON keine Vorraussetzungen
- [STATUS_MESSWERTE_LRP](#job-status-messwerte-lrp) - 0x22402D     Messwerte Laufruhepruefung auslesen
- [STATUS_MIL](#job-status-mil) - 0x30D401     MIL (Malfunction Indicator Lamp) auslesen NO_CON keine Vorraussetzungen
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - 0x300C01     Motortemperatur auslesen NO_CON keine Vorraussetzungen
- [STATUS_ODS](#job-status-ods) - 0x300501     Oeldruckschalter auslesen NO_CON keine Vorraussetzungen
- [STATUS_OEL](#job-status-oel) - 0x300E01     Oelsensor auslesen NO_CON keine Vorraussetzungen
- [STATUS_PWG_POTI_SPANNUNG](#job-status-pwg-poti-spannung) - 0x302801     Fahrerwunsch 1 auslesen NO_CON keine Vorraussetzungen
- [STATUS_PWG2](#job-status-pwg2) - 0x302901     Fahrerwunsch 2 auslesen NO_CON keine Vorraussetzungen
- [STATUS_RBMMODE9](#job-status-rbmmode9) - 0x224026     Rate Based Monitoring Mode 9 auslesen (Ausgabe der Werte wie im Scantool Mode 9)
- [STATUS_RBMMS1](#job-status-rbmms1) - 0x224027     Rate Based Monitoring Motorsteuerung MS... Block 1 auslesen (Vorhalt)
- [STATUS_RBMMS2](#job-status-rbmms2) - 0x224028     Rate Based Monitoring Motorsteuerung MS... Block 2 auslesen (Vorhalt)
- [STATUS_SLP](#job-status-slp) - 0x30CB01     Sekundaerluftpumpe auslesen NO_CON keine Vorraussetzungen
- [STATUS_SOK](#job-status-sok) - 0x30C201     Soundklappe auslesen NO_CON keine Vorraussetzungen
- [STATUS_SPT](#job-status-spt) - 0x300601     Sporttaster auslesen NO_CON keine Vorraussetzungen
- [STATUS_SR](#job-status-sr) - 0x30C401     Startrelais auslesen NO_CON keine Vorraussetzungen
- [STATUS_TEV](#job-status-tev) - 0x30CF01     Tankentlueftungsventil auslesen NO_CON keine Vorraussetzungen
- [STATUS_TKA](#job-status-tka) - 0x300D01     Kuehlerauslasstemperatur auslesen NO_CON keine Vorraussetzungen
- [STATUS_TTEMP](#job-status-ttemp) - 0x302F01     Taster Tempomat auslesen NO_CON keine Vorraussetzungen
- [STATUS_UBAT](#job-status-ubat) - 0x302701     Batteriesensor auslesen NO_CON keine Vorraussetzungen
- [STATUS_UBATT](#job-status-ubatt) - 0x301C01     Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) auslesen NO_CON keine Vorraussetzungen
- [STATUS_UDF](#job-status-udf) - 0x301701     Umgebungsdruck auslesen NO_CON keine Vorraussetzungen
- [STATUS_UGEN](#job-status-ugen) - 0x303201     Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) auslesen NO_CON keine Vorraussetzungen
- [STATUS_UKL15](#job-status-ukl15) - 0x301B01     Kl.15 Spannung auslesen NO_CON keine Vorraussetzungen
- [STEUERN_AGK](#job-steuern-agk) - 0x30C107     Abgasklappe ansteuern NO_CON keine Vorraussetzungen
- [STEUERN_ANWS](#job-steuern-anws) - 0x30EE07     Vanos Auslass Ventil ansteuern CON_N_MIN nur bei erhoeter Motordrehzahl
- [STEUERN_ANWSF](#job-steuern-anwsf) - 0x30A207     Ventil Vanos Auslass Frueh ansteuern CON_N_MIN nur bei erhoeter Motordrehzahl
- [STEUERN_ANWSR](#job-steuern-anwsr) - 0x2E5FFA07     Anschlagsadaption Auslass Vanos ruecksetzen vorgeben  ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden.  N_LL nur bei Leerlauf-Drehzahl
- [STEUERN_ANWSS](#job-steuern-anwss) - 0x30A307     Ventil Vanos Auslass Spaet ansteuern CON_N_MIN nur bei erhoeter Motordrehzahl
- [STEUERN_AVS](#job-steuern-avs) - 0x30C007     Absperrventil Saugstrahlpumpe ansteuern V_EQ_ZERO nur bei Fahrzeuggeschwindigkeit v=0
- [STEUERN_CO_ABGLEICH_PROGRAMMIEREN](#job-steuern-co-abgleich-programmieren) - 0x2E5FF108     Abgleichwert CO (Kohlenmonoxid) programmieren NO_CON keine Vorraussetzungen
- [STEUERN_CO_ABGLEICH_RESET](#job-steuern-co-abgleich-reset) - 0x2E5FF104     Abgleichwert CO (Kohlenmonoxid) loeschen NO_CON keine Vorraussetzungen
- [STEUERN_CO_ABGLEICH_VERSTELLEN](#job-steuern-co-abgleich-verstellen) - 0x2E5FF107     Abgleichwert CO (Kohlenmonoxid) vorgeben NO_CON keine Vorraussetzungen
- [STEUERN_CODIERUNG_IGR](#job-steuern-codierung-igr) - 0x2E3210     Codierung fuer IGR (Intelligente Generator-Regelung) vorgeben
- [STEUERN_CODIERUNG_KAT](#job-steuern-codierung-kat) - 0x2E3001     Codierung fuer Katalysator vorgeben
- [STEUERN_CODIERUNG_MIL](#job-steuern-codierung-mil) - 0x2E3000     Codierung fuer MIL (Malfunction Indication Lamp) vorgeben
- [STEUERN_CODIERUNG_OEL](#job-steuern-codierung-oel) - 0x2E3200     Codierung fuer Oelwechselintervall vorgeben
- [STEUERN_CODIERUNG_VMAX](#job-steuern-codierung-vmax) - 0x2E3010     Codierung fuer maximale Geschwindigkeit vorgeben
- [STEUERN_CODIERUNG_XENON](#job-steuern-codierung-xenon) - 0x2E3211     Codierung fuer Xenon-Lichtverbau vorgeben
- [STEUERN_DFV1A](#job-steuern-dfv1a) - 0x3128     Ansteuern Diagnosefunktion Auslass A-Vanostest 1 (Verstellzeit)
- [STEUERN_DFV1E](#job-steuern-dfv1e) - 0x3123     Ansteuern Diagnosefunktion Einlass E-Vanostest 1 (Verstellzeit)
- [STEUERN_DFV2A](#job-steuern-dfv2a) - 0x3129     Ansteuern Diagnosefunktion Auslass A-Vanostest 2 (Dichtigkeit)
- [STEUERN_DFV2E](#job-steuern-dfv2e) - 0x3124     Ansteuern Diagnosefunktion Einlass E-Vanostest 2 (Dichtigkeit)
- [STEUERN_DFVFA](#job-steuern-dfvfa) - 0x31D3     Ansteuern Diagnosefunktion Auslass A-Vanostest Fruehanschlag
- [STEUERN_DFVFE](#job-steuern-dfvfe) - 0x31D1     Ansteuern Diagnosefunktion Einlass E-Vanostest Fruehanschlag
- [STEUERN_DFVSA](#job-steuern-dfvsa) - 0x31D4     Ansteuern Diagnosefunktion Auslass A-Vanostest Spaetanschlag
- [STEUERN_DFVSE](#job-steuern-dfvse) - 0x31D2     Ansteuern Diagnosefunktion Einlass E-Vanostest Spaetanschlag
- [STEUERN_DK](#job-steuern-dk) - 0x302A07     Drosselklappe ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0
- [STEUERN_DMTL_HEIZUNG](#job-steuern-dmtl-heizung) - 0x30CE07     Diagnosemodul-Tank Leckage Heizung ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0
- [STEUERN_DMTL_P](#job-steuern-dmtl-p) - 0x30CC07     Diagnosemodul-Tank Leckage Pumpe ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0
- [STEUERN_DMTL_V](#job-steuern-dmtl-v) - 0x30CD07     Diagnosemodul-Tank Leckage Ventil ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - 0x30DA07     E-Luefter ansteuern CON_ELUE nur bei Motortemperatur TMOT kleiner 115gradCelsius
- [STEUERN_EBL](#job-steuern-ebl) - 0x30C807     E-Box-Luefter ansteuern NO_CON keine Vorraussetzungen
- [STEUERN_EISYGD](#job-steuern-eisygd) - 0x31E1     Ansteuern Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403)
- [STEUERN_EISYUGD](#job-steuern-eisyugd) - 0x31E0     Ansteuern Eisy-Adaptionswerte (ungedrosselt) (Anforderung aus CP5403)
- [STEUERN_EKP](#job-steuern-ekp) - 0x30D807     Elektrische Kraftstoffpumpe 1 ansteuern     Elektrische Kraftstoffpumpe 1 Deaktivierung aufheben N_EQ_ZERO nur bei Motordrehzahl n=0
- [STEUERN_EML](#job-steuern-eml) - 0x30D607     EML (Engine Malfunction Lamp) ansteuern NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_AGK](#job-steuern-ende-agk) - 0x30C100     Abgasklappe Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_ANWS](#job-steuern-ende-anws) - 0x30EE00     Vanos Auslass Ventil Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_ANWSF](#job-steuern-ende-anwsf) - 0x30A200     Ventil Vanos Auslass Frueh Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_ANWSR](#job-steuern-ende-anwsr) - 0x2E5FFA00     Anschlagsadaption Auslass Vanos ruecksetzen Vorgeben beenden  ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden.  NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_ANWSS](#job-steuern-ende-anwss) - 0x30A300     Ventil Vanos Auslass Spaet Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_AVS](#job-steuern-ende-avs) - 0x30C000     Absperrventil Saugstrahlpumpe Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_DFV1A](#job-steuern-ende-dfv1a) - 0x3228     Ende Diagnosefunktion Auslass A-Vanostest 1 (Verstellzeit)
- [STEUERN_ENDE_DFV1E](#job-steuern-ende-dfv1e) - 0x3223     Ende Diagnosefunktion Einlass E-Vanostest 1 (Verstellzeit)
- [STEUERN_ENDE_DFV2A](#job-steuern-ende-dfv2a) - 0x3229     Ende Diagnosefunktion Auslass A-Vanostest 2 (Dichtigkeit)
- [STEUERN_ENDE_DFV2E](#job-steuern-ende-dfv2e) - 0x3224     Ende Diagnosefunktion Einlass E-Vanostest 2 (Dichtigkeit)
- [STEUERN_ENDE_DFVFA](#job-steuern-ende-dfvfa) - 0x32D3     Ende Diagnosefunktion Auslass A-Vanostest Fruehanschlag
- [STEUERN_ENDE_DFVFE](#job-steuern-ende-dfvfe) - 0x32D1     Ende Diagnosefunktion Einlass E-Vanostest Fruehanschlag
- [STEUERN_ENDE_DFVSA](#job-steuern-ende-dfvsa) - 0x32D4     Ende Diagnosefunktion Auslass A-Vanostest Spaetanschlag
- [STEUERN_ENDE_DFVSE](#job-steuern-ende-dfvse) - 0x32D2     Ende Diagnosefunktion Einlass E-Vanostest Spaetanschlag
- [STEUERN_ENDE_DK](#job-steuern-ende-dk) - 0x302A00     Drosselklappe Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_DMTL_HEIZUNG](#job-steuern-ende-dmtl-heizung) - 0x30CE00     Diagnosemodul-Tank Leckage Heizung Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_DMTL_P](#job-steuern-ende-dmtl-p) - 0x30CC00     Diagnosemodul-Tank Leckage Pumpe Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_DMTL_V](#job-steuern-ende-dmtl-v) - 0x30CD00     Diagnosemodul-Tank Leckage Ventil Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_E_LUEFTER](#job-steuern-ende-e-luefter) - 0x30DA00     E-Luefter Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_EBL](#job-steuern-ende-ebl) - 0x30C800     E-Box-Luefter Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_EKP](#job-steuern-ende-ekp) - 0x30D800     Elektrische Kraftstoffpumpe 1 Ansteuerung beenden     Elektrische Kraftstoffpumpe 1 Deaktivierung aufheben NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_EML](#job-steuern-ende-eml) - 0x30D600     EML (Engine Malfunction Lamp) Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_ENWS](#job-steuern-ende-enws) - 0x30ED00     Vanos Einlass Ventil Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_ENWSF](#job-steuern-ende-enwsf) - 0x30A000     Ventil Vanos Einlass Frueh Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_ENWSR](#job-steuern-ende-enwsr) - 0x2E5FF900     Anschlagsadaption Einlass Vanos ruecksetzen Vorgeben beenden  ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden.  NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_ENWSS](#job-steuern-ende-enwss) - 0x30A100     Ventil Vanos Einlass Spaet Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_EV1](#job-steuern-ende-ev1) - 0x30E100     Einspritzventil 1 Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_EV2](#job-steuern-ende-ev2) - 0x30E200     Einspritzventil 2 Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_EV3](#job-steuern-ende-ev3) - 0x30E300     Einspritzventil 3 Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_EV4](#job-steuern-ende-ev4) - 0x30E400     Einspritzventil 4 Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_EV5](#job-steuern-ende-ev5) - 0x30E500     Einspritzventil 5 Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_EV6](#job-steuern-ende-ev6) - 0x30E600     Einspritzventil 6 Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_EWAP](#job-steuern-ende-ewap) - 0x30BF00     elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_FGRL](#job-steuern-ende-fgrl) - 0x30D500     Fahrgeschwindigkeitsregler-Lampe Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_GLF](#job-steuern-ende-glf) - 0x30C300     Gesteuerte Luftfuehrung Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_KFT](#job-steuern-ende-kft) - 0x30C900     Kennfeldthermostat Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_KGEH](#job-steuern-ende-kgeh) - 0x30AD00     Kurbelgehaeuseentlueftung Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_KOREL](#job-steuern-ende-korel) - 0x30C700     Klimakompressor-Relais Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_LLS](#job-steuern-ende-lls) - 0x309F00     Leerlaufsteller Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_LRP](#job-steuern-ende-lrp) - 0x2E5FF700     Laufruhepruefung Vorgeben beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_LSH1](#job-steuern-ende-lsh1) - 0x30D000     Lambdasondenheizung vor Kat Bank1 Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_LSH2](#job-steuern-ende-lsh2) - 0x30D100     Lambdasondenheizung hinter Kat Bank1 Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_LSH3](#job-steuern-ende-lsh3) - 0x30D200     Lambdasondenheizung vor Kat Bank2 Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_LSH4](#job-steuern-ende-lsh4) - 0x30D300     Lambdasondenheizung hinter Kat Bank2 Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_MIL](#job-steuern-ende-mil) - 0x30D400     MIL (Malfunction Indicator Lamp) Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_SLP](#job-steuern-ende-slp) - 0x30CB00     Sekundaerluftpumpe Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_SOK](#job-steuern-ende-sok) - 0x30C200     Soundklappe Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_SR](#job-steuern-ende-sr) - 0x30C400     Startrelais Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_TEV](#job-steuern-ende-tev) - 0x30CF00     Tankentlueftungsventil Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_UGEN](#job-steuern-ende-ugen) - 0x303200     Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENDE_UVSG](#job-steuern-ende-uvsg) - 0x301C00     Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) Ansteuerung beenden NO_CON keine Vorraussetzungen
- [STEUERN_ENERGIESPARMODE](#job-steuern-energiesparmode) - 0x310C     Energiesparmode aktivieren START-97
- [STEUERN_ENWS](#job-steuern-enws) - 0x30ED07     Vanos Einlass Ventil ansteuern CON_N_MIN nur bei erhoeter Motordrehzahl
- [STEUERN_ENWSF](#job-steuern-enwsf) - 0x30A007     Ventil Vanos Einlass Frueh ansteuern CON_N_MIN nur bei erhoeter Motordrehzahl
- [STEUERN_ENWSR](#job-steuern-enwsr) - 0x2E5FF907     Anschlagsadaption Einlass Vanos ruecksetzen vorgeben  ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden.  N_LL nur bei Leerlauf-Drehzahl
- [STEUERN_ENWSS](#job-steuern-enwss) - 0x30A107     Ventil Vanos Einlass Spaet ansteuern CON_N_MIN nur bei erhoeter Motordrehzahl
- [STEUERN_EV1](#job-steuern-ev1) - 0x30E107     Einspritzventil 1 ansteuern CON_EV nur bei Motordrehzahl n=0 und EKP aus
- [STEUERN_EV2](#job-steuern-ev2) - 0x30E207     Einspritzventil 2 ansteuern CON_EV nur bei Motordrehzahl n=0 und EKP aus
- [STEUERN_EV3](#job-steuern-ev3) - 0x30E307     Einspritzventil 3 ansteuern CON_EV nur bei Motordrehzahl n=0 und EKP aus
- [STEUERN_EV4](#job-steuern-ev4) - 0x30E407     Einspritzventil 4 ansteuern CON_EV nur bei Motordrehzahl n=0 und EKP aus
- [STEUERN_EV5](#job-steuern-ev5) - 0x30E507     Einspritzventil 5 ansteuern CON_EV nur bei Motordrehzahl n=0 und EKP aus
- [STEUERN_EV6](#job-steuern-ev6) - 0x30E607     Einspritzventil 6 ansteuern CON_EV nur bei Motordrehzahl n=0 und EKP aus
- [STEUERN_EWAP](#job-steuern-ewap) - 0x30BF07     elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) ansteuern CON_EWAP nur bei Fahrzeuggeschwindigkeit v=0 und Motortemperatur TMOT kleiner 115gradCelsius und Batteriespannung UBAT groesser 10Volt
- [STEUERN_EWAP_SF](#job-steuern-ewap-sf) - 0x30BF07     Sonderfunktionen elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) ansteuern CON_EWAP nur bei Fahrzeuggeschwindigkeit v=0 und Motortemperatur TMOT kleiner 115gradCelsius und Batteriespannung UBAT groesser 10Volt
- [STEUERN_FGRL](#job-steuern-fgrl) - 0x30D507     Fahrgeschwindigkeitsregler-Lampe ansteuern NO_CON keine Vorraussetzungen
- [STEUERN_GLF](#job-steuern-glf) - 0x30C307     Gesteuerte Luftfuehrung ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0
- [STEUERN_KFT](#job-steuern-kft) - 0x30C907     Kennfeldthermostat ansteuern NO_CON keine Vorraussetzungen
- [STEUERN_KGEH](#job-steuern-kgeh) - 0x30AD07     Kurbelgehaeuseentlueftung ansteuern NO_CON keine Vorraussetzungen
- [STEUERN_KOREL](#job-steuern-korel) - 0x30C707     Klimakompressor-Relais ansteuern NO_CON keine Vorraussetzungen
- [STEUERN_KRANN](#job-steuern-krann) - 0x31E3     Ansteuern Krann-Adaptionswerte (Anforderung aus CP5404)
- [STEUERN_LEISTUNGSSTUFE](#job-steuern-leistungsstufe) - 0x2E3020     Codierung fuer Leistungsstufe vorgeben
- [STEUERN_LLS](#job-steuern-lls) - 0x309F07     Leerlaufsteller ansteuern NO_CON keine Vorraussetzungen
- [STEUERN_LRP](#job-steuern-lrp) - 0x2E5FF707     Laufruhepruefung vorgeben NO_CON keine Vorraussetzungen
- [STEUERN_LSH1](#job-steuern-lsh1) - 0x30D007     Lambdasondenheizung vor Kat Bank1 ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0
- [STEUERN_LSH2](#job-steuern-lsh2) - 0x30D107     Lambdasondenheizung hinter Kat Bank1 ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0
- [STEUERN_LSH3](#job-steuern-lsh3) - 0x30D207     Lambdasondenheizung vor Kat Bank2 ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0
- [STEUERN_LSH4](#job-steuern-lsh4) - 0x30D307     Lambdasondenheizung hinter Kat Bank2 ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0
- [STEUERN_MIL](#job-steuern-mil) - 0x30D407     MIL (Malfunction Indicator Lamp) ansteuern NO_CON keine Vorraussetzungen
- [STEUERN_PROGRAMM_LRP](#job-steuern-programm-lrp) - 0x2E5FF708     Laufruhepruefung programmieren NO_CON keine Vorraussetzungen
- [STEUERN_SLP](#job-steuern-slp) - 0x30CB07     Sekundaerluftpumpe ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0
- [STEUERN_SOK](#job-steuern-sok) - 0x30C207     Soundklappe ansteuern NO_CON keine Vorraussetzungen
- [STEUERN_SR](#job-steuern-sr) - 0x30C407     Startrelais ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0
- [STEUERN_TEV](#job-steuern-tev) - 0x30CF07     Tankentlueftungsventil ansteuern NO_CON keine Vorraussetzungen
- [STEUERN_UGEN](#job-steuern-ugen) - 0x303207     Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) ansteuern N_LL nur bei Leerlauf-Drehzahl
- [STEUERN_UVSG](#job-steuern-uvsg) - 0x301C07     Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) ansteuern V_N_EQ_ZERO nur bei Fahrzeuggeschwindigkeit v=0 und Motordrehzahl n=0

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

<a id="job-hs-lesen"></a>
### HS_LESEN

Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table HOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hs-loeschen"></a>
### HS_LOESCHEN

Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default

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

<a id="job-status-messwertblock-lesen"></a>
### STATUS_MESSWERTBLOCK_LESEN

Lesen eines Messwertblockes Es muss immer das BlockSchreibenFlag und mindestens ein MESSWERT uebergeben werden. KWP2000: $2C DynamicallyDefinedLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier $04 ClearDynamicallyDefinedLocalIdentifier KWP2000: $2C DynamicallyDefinedLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier $02 DefineByCommonIdentifier KWP2000: $21 ReadDataByLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | Wenn 'JA' wird der Messwertblock im SG gelöscht neu ins SG geschrieben und dann gelesen Wenn 'NEIN' wird der Messwertblock im SG nicht gelöscht Es wird der im SG gespeicherte Messwertblock gelesen table MesswerteMode TEXT KOMMENTAR |
| MESSWERT | string | Dynamische Argumente Es können bis zu 42 Argumente übergeben werden Es muss mindestens ein Argument übergeben werden Er wird das zugehörige Result table MesswerteTab ARG RESULTNAME erzeugt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |

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

CBS Daten auslesen (fuer CBS-Version 4) KWP2000: $22 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Hex-String |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| ANZ_CBS | int | Anzahl der CBS - Umfaenge im Steuergeraet |
| ID_FN_CBS_MESS_WERT | int | CBS-Kennung als Zahl |
| ID_FN_CBS_MESS_HEX | string | CBS-Kennung als Hex-String |
| ID_FN_CBS_MESS_TEXT | string | table CbsKennung CBS_K CBS_K_TEXT CBS-Kennung im Klartext |
| RMMI_CBS_WERT | int | Restlaufleistung |
| RMMI_CBS_EINH | string | Information zur Restlaufleistung |
| ST_UN_CBS_WERT | int | Einheit Restlaufleistung als Zahl |
| ST_UN_CBS_HEX | string | Einheit Restlaufleistung als Hex-String |
| ST_UN_CBS_TEXT | string | Einheit Restlaufleistung im Klartext |
| COU_RSTG_CBS_MESS_WERT | int | Servicezaehler |
| COU_RSTG_CBS_MESS_EINH | string | Zaehler |
| AVAI_CBS_WERT | int | Verfuegbarkeit in % |
| AVAI_CBS_EINH | string | % |
| AVAI_CBS_WERT_OEL | int | Verfuegbarkeit OEL in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_CSF | int | Verfuegbarkeit CSF in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BATT | int | Verfügbarkeit BATT in %, für Prüfablauf Bandende |
| AVAI_CBS_WERT_VTG | int | Verfügbarkeit VTG in %, für Prüfablauf Bandende |
| AVAI_CBS_WERT_FILT | int | Verfuegbarkeit FILT in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BR_V | int | Verfuegbarkeit BR_V in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BR_H | int | Verfuegbarkeit BR_H in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BRFL | int | Verfuegbarkeit BRFL in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_ZKRZ | int | Verfuegbarkeit ZKRZ in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_SIC | int | Verfuegbarkeit SIC in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_KFL | int | Verfuegbarkeit KFL in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_UEB | int | Verfuegbarkeit UEB in %, fuer Pruefablauf Bandende |
| ZIEL_MM_WERT | int | Ziel-Monat |
| ZIEL_MM_EINH | string | Monat |
| ZIEL_YY_WERT | int | Ziel-Jahr |
| ZIEL_YY_EINH | string | Jahr |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall |
| FRC_INTM_WAY_CBS_EINH | string | Information zur Prognose Wegintervall |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall |
| MANIP_CBS | int | Manipulationsbyte |
| MANIP_CBS_TEXT | string | Manipulationsbyte im Klartext |
| Res_Byte | int | Reserve Byte (noch unbenutzt) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cbs-reset"></a>
### CBS_RESET

CBS Daten Zuruecksetzen (fuer CBS-Version 4) KWP2000: $2E WriteDataByCommonIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CBS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, ZKrz, Sic, Kfl, TUV, AU, Ueb Werte externe Umfaenge: Oel, Br_v, Br_h, Filt, CSF, Batt, VTG Defaultwert: 0x00 (ungueltig) |
| CBS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, keine Aenderung: 255 Defaultwert: 100 |
| CBS_ANZAHL_SERVICE | int | Anzahl der durchgefuehrten Services: 0-30 Schalter, Erhoehung der Anzahl um +1: 31 Defaultwert: 31 |
| CBS_ZIEL_MONAT | int | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter, keine Aenderung: 255 Defaultwert: 255 |
| CBS_ZIEL_JAHR | int | Ziel-Jahr (HU/AU) 2000-2239: 0-239 Schalter, keine Aenderung: 255 Defaultwert: 255 |
| RMM_CBS_WERT | int | Restlaufleistung in km oder % (siehe Argument Einheit) Schalter, keine Aenderung: 8000h Defaultwert: 8000h |
| ST_UN_CBS_RSTG | int | Einheit Restlaufleistung 0hex -&gt; % 1hex -&gt; km*10 Fhex -&gt; d.c. Defaultwert: Fh |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall Umrechnung 1-254*1000km Schalter, setzt auf Defaultwert zurueck: 0h Schalter, keine Aenderung: FFh Defaultwert: FFh |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall 0-254 Monate Schalter, keine Aenderung: FFh Defaultwert: FFh |
| Res_Byte | int | Reserve Byte (noch unbenutzt) Defaultwert: 00h |

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

<a id="job-status-obd-mode-01"></a>
### _STATUS_OBD_MODE_01

Auslesen der Motor-Diagnosedaten nach Mode 01 PID 01  

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MIL_TEXT | string | Ansteuerstatus der MIL (An=1, Aus=0) |
| STAT_MIL_WERT | int | Ansteuerstatus der MIL (An=1, Aus=0) |
| STAT_ANZAHL_PCODE_WERT | int | Anzahl gespeicherter P-Codes |
| STAT_MONITOR_CC_TEXT | string | Überwachung Comprehensive Components (übrige Komponenten) Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_MONITOR_CC_WERT | int | Überwachung Comprehensive Components (übrige Komponenten) Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_READINESS_CC_TEXT | string | Überwachung Comprehensive Components (übrige Komponenten) Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_READINESS_CC_WERT | int | Überwachung Comprehensive Components (übrige Komponenten) Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_MONITOR_KSS_TEXT | string | Überwachung KraftStoffSystem Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_MONITOR_KSS_WERT | int | Überwachung KraftStoffSystem Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_READINESS_KSS_TEXT | string | Überwachung KraftStoffSystem Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_READINESS_KSS_WERT | int | Überwachung KraftStoffSystem Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_MONITOR_VA_TEXT | string | Überwachung VerbrennungsAussetzer Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_MONITOR_VA_WERT | int | Überwachung VerbrennungsAussetzer Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_READINESS_VA_TEXT | string | Überwachung VerbrennungsAussetzer Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_READINESS_VA_WERT | int | Überwachung VerbrennungsAussetzer Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_MONITOR_ARS_TEXT | string | Überwachung AbgasRückführungsSystem Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_MONITOR_ARS_WERT | int | Überwachung AbgasRückführungsSystem Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_READINESS_ARS_TEXT | string | Überwachung AbgasRückführungsSystem Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_READINESS_ARS_WERT | int | Überwachung AbgasRückführungsSystem Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_MONITOR_LSH_TEXT | string | Überwachung LambdaSondenHeizung Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_MONITOR_LSH_WERT | int | Überwachung LambdaSondenHeizung Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_READINESS_LSH_TEXT | string | Überwachung LambdaSondenHeizung Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_READINESS_LSH_WERT | int | Überwachung LambdaSondenHeizung Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_MONITOR_LS_TEXT | string | Überwachung LambdaSonde Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_MONITOR_LS_WERT | int | Überwachung LambdaSonde Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_READINESS_LS_TEXT | string | Überwachung LambdaSonde Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_READINESS_LS_WERT | int | Überwachung LambdaSonde Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_MONITOR_KLIMA_TEXT | string | Überwachung Klimaanlage Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_MONITOR_KLIMA_WERT | int | Überwachung Klimaanlage Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_READINESS_KLIMA_TEXT | string | Überwachung Klimaanlage Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_READINESS_KLIMA_WERT | int | Überwachung Klimaanlage Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_MONITOR_SLS_TEXT | string | Überwachung SekundärLuftSystem Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_MONITOR_SLS_WERT | int | Überwachung SekundärLuftSystem Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_READINESS_SLS_TEXT | string | Überwachung SekundärLuftSystem Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_READINESS_SLS_WERT | int | Überwachung SekundärLuftSystem Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_MONITOR_TEV_TEXT | string | Überwachung Tankentlüftungssystem Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_MONITOR_TEV_WERT | int | Überwachung Tankentlüftungssystem Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_READINESS_TEV_TEXT | string | Überwachung Tankentlüftungssystem Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_READINESS_TEV_WERT | int | Überwachung Tankentlüftungssystem Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_MONITOR_KH_TEXT | string | Überwachung KatalysatorHeizung Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_MONITOR_KH_WERT | int | Überwachung KatalysatorHeizung Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_READINESS_KH_TEXT | string | Überwachung KatalysatorHeizung Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_READINESS_KH_WERT | int | Überwachung KatalysatorHeizung Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_MONITOR_KAT_TEXT | string | Überwachung Katalysator Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_MONITOR_KAT_WERT | int | Überwachung Katalysator Test wird durch dieses Modul unterstützt=1, Test wird durch dieses Modul nicht unterstützt=0 |
| STAT_READINESS_KAT_TEXT | string | Überwachung Katalysator Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| STAT_READINESS_KAT_WERT | int | Überwachung Katalysator Test nicht abgeschlossen=1, Test abgeschlossen oder nicht anwendbar=0 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-obd-mode-03"></a>
### _STATUS_OBD_MODE_03

Auslesen der P-Codes nach Mode 3  

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PCODE_1_HEX | string | 1. P-Code als Hex-Wert |
| STAT_PCODE_1_TEXT | string | 1. P-Code als Text |
| STAT_PCODE_M3_ANZAHL | int | Anzahl gespeicherter P-Codes |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-obd-mode-07"></a>
### _STATUS_OBD_MODE_07

Auslesen der P-Codes nach Mode 7  

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PCODE_1_HEX | string | 1. P-Code als Hex-Wert |
| STAT_PCODE_1_TEXT | string | 1. P-Code als Text |
| STAT_PCODE_M7_ANZAHL | int | Anzahl gespeicherter P-Codes (0 - 6) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-set-baudrate"></a>
### SET_BAUDRATE

Initialisierung der Kommunikationsparameter mit bestimmter Baudrate

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BAUDRATE | string | die gewuenschte Baudrate |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-set-parameter"></a>
### SET_PARAMETER

Aenderung der Kommunikationsparameter bei Long-Parametersätzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KONZEPT | string | Konzept |
| BAUDRATE | string | Baudrate |
| TIMEOUT | string | Timeout in ms |
| REGENERATIONSZEIT | string | Regenerationszeit in ms |
| TELEGRAMMENDEZEIT | string | Telegrammendezeit in ms |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-interfacetype"></a>
### INTERFACETYPE

Interface-Typ bestimmen und ausgeben Es wird der Name des Interfaces übergeben Wichtig für Baudratenumschaltung weil bei ADS, EADS und OBD sind nur 115200 Baud möglich, bei EDIC nur 125000 Baud möglich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| INTERFACE_TYP | string | Rueckmeldung des Interface-Typs |

<a id="job-access-timing-parameter"></a>
### ACCESS_TIMING_PARAMETER

Aenderung der Timingparameter im SG

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| P2MIN | int | P2min, Einheit: 0.5 ms |
| P2MAX | int | P2max, Einheit: 25 ms |
| P3MIN | int | P3min, Einheit: 0.5 ms |
| P3MAX | int | P3max, Einheit: 250 ms |
| P4MIN | int | P4min, Einheit: 0.5 ms |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-access-timing-parameter-default"></a>
### ACCESS_TIMING_PARAMETER_DEFAULT

Default-Timingparameter im SG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-hex"></a>
### FS_LESEN_HEX

Fehlerspeicher auslesen als Hex Dump

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLERNR | int | Eingabe der FehlerNummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| F_ORT_NR | long | Nummer des Fehlers soll FEHLERNR sein |
| F_NR_INT | int | Anzahl der eingetragenen Fehler |
| F_ORT_TEXT | string | Fehlernummer im Speicher |
| FS_ZEILE1 | string | Byte  0 -  8 des Fehlerspeichers als Dump |
| FS_ZEILE2 | string | Byte  9 - 16 des Fehlerspeichers als Dump |
| FS_ZEILE3 | string | Byte 17 - 24 des Fehlerspeichers als Dump |
| FS_ZEILE4 | string | Byte 25 - 28 des Fehlerspeichers als Dump |

<a id="job-messwertblock-lesen"></a>
### MESSWERTBLOCK_LESEN

$2C F0 02 DDLI Messwerte aus Übergabestring definieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STRING_IN | string | Werte aus DDLI Liste Format 0x58XX,0x42YY,0x43ZZ,... |
| TRENNZEICHEN | string | Werte aus DDLI Liste Format 0x58XX,0x42YY,0x43ZZ,... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an  SG Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG Block löschen |
| _TEL_AUFTRAG | binary | Hex-Auftrag an  SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an  SG Block lesen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG Block lesen |
| STAT_ANZAHL_WERTE | int | Anzahl Messwerte 0 bis n dezimal ansteigend |
| STAT_MESSWERT0_WERT | real | real Wert |
| STAT_MESSWERT0_STRING | string | String mit 9 signifikanten Stellen |
| STAT_MESSWERT0_TEXT | string | Text der Variablen aus INFO |
| STAT_MESSWERT0_EINH | string | Einheit der Variablen |

<a id="job-status-messwerte-vanos"></a>
### STATUS_MESSWERTE_VANOS

$2C F0 02 DDLI Messwerte CAM_IN und CAM_EX auf Wunsch von VS-22

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an SG alten Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG alten Block löschen |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an SG  Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_EINLASS_WERT | real | VANOS Einlass Istwert 60 bis 155,6 |
| STAT_EINLASS_TEXT | string |  |
| STAT_EINLASS_EINH | string | °KW |
| STAT_EINLASS_SOLL_WERT | real | VANOS Einlass Sollwert 60 bis 155,6 |
| STAT_EINLASS_SOLL_TEXT | string |  |
| STAT_EINLASS_SOLL_EINH | string | °KW |
| STAT_AUSLASS_WERT | real | VANOS Auslass Istwert -135,6 bis -40 |
| STAT_AUSLASS_TEXT | string |  |
| STAT_AUSLASS_EINH | string | °KW |
| STAT_AUSLASS_SOLL_WERT | real | VANOS Auslass Sollwert -135,6 bis -40 |
| STAT_AUSLASS_SOLL_TEXT | string |  |
| STAT_AUSLASS_SOLL_EINH | string | °KW |
| STAT_ANZAHL_WERTE | int |  |

<a id="job-fs-lesen-freeze-frame"></a>
### FS_LESEN_FREEZE_FRAME

Fehlerspeicher auslesen mit SAE Werten Umwelt und P-Code

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | die Nummer des zu lesenden Fehlers eingeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei, Tabelle JobResult STATUS_TEXT |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Anforderung an SG |
| F_ART_ANZ | int | Anzahl der eingetragenen Fehler |
| F_ORT_NR | long | Fehlercode des SG als Index == F_CODE |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_SYMPTOM_NR | int | Gibt die Nummer der Fehlerart aus(StatusOfDTC) |
| F_SYMPTOM_TEXT | string | Interpretiert die Fehlerart |
| F_READY_NR | int | Gibt an, ob Readiness gesetzt |
| F_READY_TEXT | string | gibt einen Text zur Readiness aus |
| F_VORHANDEN_NR | int | Gibt die Nummer des Eintragstatuses aus |
| F_VORHANDEN_TEXT | string | gibt die Eintragsentprellung des Fehlers an |
| F_WARNUNG_NR | int | Gibt die Nummer fuer MIL EIN aus |
| F_WARNUNG_TEXT | string | gibt an, ob die MIL angesteuert wird |
| F_ZYKLUS_FLAG | string | gibt an, ob Zyklus-Flag gesetzt wurden ist |
| F_AKTIV_FLAG | string | gibt an, ob Diagnose laeuft |
| F_STOP_FLAG | string | gibt an, ob Stopbedingungen vorliegen |
| F_ERROR_FLAG | string | zeigt Error-Flag an |
| F_MIL_FLAG | string | zeigt den MIL-Status an |
| F_ENTPRELL_FLAG | string | gibt den MIL-Entprellstatus an |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_PCODE | int | P-Code Zahl entsprechend FO und FA |
| F_PCODE_STRING | string | P-Code Zahl als P0123 entsprechend FO und FA |
| F_PCODE_TEXT | string | P-Code Text entsprechend FO und FA |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_UW_KM | string | Km-Stand bei Erst-, Zweit- Letzmaligen Auftreten |
| F_UW1_NR | int | 1.Satz Umweltbedingung 1 Index (Ersterkennung) |
| F_UW1_TEXT | string | 1.Satz UW1 Text zur Umweltbedingung |
| F_UW1_EINH | string | 1.Satz UW1 Einheit |
| F_UW2_NR | int | 1.Satz Umweltbedingung 2 Index (Ersterkennung) |
| F_UW2_TEXT | string | 1.Satz UW2 Text zur Umweltbedingung |
| F_UW2_EINH | string | 1.Satz UW2 Einheit |
| F_UW3_NR | int | 1.Satz Umweltbedingung 3 Index (Ersterkennung) |
| F_UW3_TEXT | string | 1.Satz UW3 Text zur Umweltbedingung |
| F_UW3_EINH | string | 1.Satz UW3 Einheit |
| F_UW4_NR | int | 1.Satz Umweltbedingung 4 Index (Ersterkennung) |
| F_UW4_TEXT | string | 1.Satz UW4 Text zur Umweltbedingung |
| F_UW4_EINH | string | 1.Satz UW4 Einheit |
| F_HLC | int | Entprellvorgaenge Fahrzyklen HLC |
| F_CLA | string | Klasse |
| F_FLC | int | Entprellzähler  ( MIL an) FLC |
| F_DLC | int | Entprellvorgaenge DLC |
| F_LZ | int | Zähler Aufwärmzyklen DLC |
| F_FF0_TEXT | string | Freeze Frame Umweltbedingung 0 Text |
| F_FF0_WERT | string | Freeze Frame Umweltbedingung 0 Status Lambda Bank1 |
| F_FF1_TEXT | string | Freeze Frame Umweltbedingung 1 Text |
| F_FF1_WERT | string | Freeze Frame Umweltbedingung 1 Status Lambda Bank2 |
| F_FF2_TEXT | string | Freeze Frame Umweltbedingung 2 Text |
| F_FF2_EINH | string | Freeze Frame Umweltbedingung 2 Einheit |
| F_FF2_WERT | real | Freeze Frame Umweltbedingung 2 Lastfaktor |
| F_FF3_TEXT | string | Freeze Frame Umweltbedingung 3 Text |
| F_FF3_EINH | string | Freeze Frame Umweltbedingung 3 EINH |
| F_FF3_WERT | real | Freeze Frame Umweltbedingung 3 KuehlerTemperatur |
| F_FF4_TEXT | string | Freeze Frame Umweltbedingung 4 Text |
| F_FF4_EINH | string | Freeze Frame Umweltbedingung 4 EINH |
| F_FF4_WERT | real | Freeze Frame Umweltbedingung 4 Control Bank1 |
| F_FF5_TEXT | string | Freeze Frame Umweltbedingung 5 Text |
| F_FF5_EINH | string | Freeze Frame Umweltbedingung 5 EINH |
| F_FF5_WERT | real | Freeze Frame Umweltbedingung 5 Aadaption Bank1 |
| F_FF6_TEXT | string | Freeze Frame Umweltbedingung 6 Text |
| F_FF6_EINH | string | Freeze Frame Umweltbedingung 6 EINH |
| F_FF6_WERT | real | Freeze Frame Umweltbedingung 6 Control Bank2 |
| F_FF7_TEXT | string | Freeze Frame Umweltbedingung 7 Text |
| F_FF7_EINH | string | Freeze Frame Umweltbedingung 7 EINH |
| F_FF7_WERT | real | Freeze Frame Umweltbedingung 7 Adaption Bank2 |
| F_FF8_TEXT | string | Freeze Frame Umweltbedingung 8 Text |
| F_FF8_EINH | string | Freeze Frame Umweltbedingung 8 EINH |
| F_FF8_WERT | real | Freeze Frame Umweltbedingung 8 Ansaugdruck |
| F_FF9_TEXT | string | Freeze Frame Umweltbedingung 9 Text |
| F_FF9_EINH | string | Freeze Frame Umweltbedingung 9 EINH |
| F_FF9_WERT | real | Freeze Frame Umweltbedingung 9 Drehzahl |
| F_FF10_TEXT | string | Freeze Frame Umweltbedingung 10 Text |
| F_FF10_EINH | string | Freeze Frame Umweltbedingung 10 EINH |
| F_FF10_WERT | real | Freeze Frame Umweltbedingung 10 Fahrzeug Geschwindigkeit |

<a id="job-status-messwerte-kd"></a>
### STATUS_MESSWERTE_KD

$2C F0 02 DDLI Messwerte nach Wunsch VS-22

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an SG alten Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG alten Block löschen |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_ANZAHL_WERTE | int | Anzahl Messwerte 0 bis 16 |
| STAT_MESSWERT0_WERT | real | Messwert (Word) |
| STAT_MESSWERT0_STRING | string | Messwert (Word) |
| STAT_MESSWERT0_TEXT | string | Messwert |
| STAT_MESSWERT0_EINH | string | Messwert |
| STAT_MESSWERT1_WERT | real | Messwert (Word) |
| STAT_MESSWERT1_STRING | string | Messwert (Word) |
| STAT_MESSWERT1_TEXT | string | Messwert |
| STAT_MESSWERT1_EINH | string | Messwert |
| STAT_MESSWERT2_WERT | real | Messwert (Word) |
| STAT_MESSWERT2_STRING | string | Messwert (Word) |
| STAT_MESSWERT2_TEXT | string | Messwert |
| STAT_MESSWERT2_EINH | string | Messwert |
| STAT_MESSWERT3_WERT | real | Messwert (Word) |
| STAT_MESSWERT3_STRING | string | Messwert (Word) |
| STAT_MESSWERT3_TEXT | string | Messwert |
| STAT_MESSWERT3_EINH | string | Messwert |
| STAT_MESSWERT4_WERT | real | Messwert (Word) |
| STAT_MESSWERT4_STRING | string | Messwert (Word) |
| STAT_MESSWERT4_TEXT | string | Messwert |
| STAT_MESSWERT4_EINH | string | Messwert |
| STAT_MESSWERT5_WERT | real | Messwert (Word) |
| STAT_MESSWERT5_STRING | string | Messwert (Word) |
| STAT_MESSWERT5_TEXT | string | Messwert |
| STAT_MESSWERT5_EINH | string | Messwert |
| STAT_MESSWERT6_WERT | real | Messwert (Word) |
| STAT_MESSWERT6_STRING | string | Messwert (Word) |
| STAT_MESSWERT6_TEXT | string | Messwert |
| STAT_MESSWERT6_EINH | string | Messwert |
| STAT_MESSWERT7_WERT | real | Messwert (Word) |
| STAT_MESSWERT7_STRING | string | Messwert (Word) |
| STAT_MESSWERT7_TEXT | string | Messwert |
| STAT_MESSWERT7_EINH | string | Messwert |
| STAT_MESSWERT8_WERT | real | Messwert (Word) |
| STAT_MESSWERT8_STRING | string | Messwert (Word) |
| STAT_MESSWERT8_TEXT | string | Messwert |
| STAT_MESSWERT8_EINH | string | Messwert |
| STAT_MESSWERT9_WERT | real | Messwert (Word) |
| STAT_MESSWERT9_STRING | string | Messwert (Word) |
| STAT_MESSWERT9_TEXT | string | Messwert |
| STAT_MESSWERT9_EINH | string | Messwert |
| STAT_MESSWERT10_WERT | real | Messwert (Word) |
| STAT_MESSWERT10_STRING | string | Messwert (Word) |
| STAT_MESSWERT10_TEXT | string | Messwert |
| STAT_MESSWERT10_EINH | string | Messwert |
| STAT_MESSWERT11_WERT | real | Messwert (Word) |
| STAT_MESSWERT11_STRING | string | Messwert (Word) |
| STAT_MESSWERT11_TEXT | string | Messwert |
| STAT_MESSWERT11_EINH | string | Messwert |
| STAT_MESSWERT12_WERT | real | Messwert (Word) |
| STAT_MESSWERT12_STRING | string | Messwert (Word) |
| STAT_MESSWERT12_TEXT | string | Messwert |
| STAT_MESSWERT12_EINH | string | Messwert |
| STAT_MESSWERT13_WERT | real | Messwert (Word) |
| STAT_MESSWERT13_STRING | string | Messwert (Word) |
| STAT_MESSWERT13_TEXT | string | Messwert |
| STAT_MESSWERT13_EINH | string | Messwert |
| STAT_MESSWERT14_WERT | int | Messwert (Word) |
| STAT_MESSWERT14_STRING | string | Messwert (Word) |
| STAT_MESSWERT14_TEXT | string | Messwert |
| STAT_MESSWERT14_EINH | string | Messwert |
| STAT_MESSWERT15_WERT | real | Messwert (Word) |
| STAT_MESSWERT15_STRING | string | Messwert (Word) |
| STAT_MESSWERT15_TEXT | string | Messwert |
| STAT_MESSWERT15_EINH | string | Messwert |

<a id="job-ident-aif"></a>
### IDENT_AIF

Identdaten mit KWP2000: $1A ReadECUIdentification Anwender Informations Felder mit KWP 2000: $23 ReadMemoryByAddress

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
| ID_LIEF_TEXT | string | Lieferanten-Text nach Tabelle Lieferanten |
| ID_SW_NR_MCV | string | Softwarenummer (message catalogue version) |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| ID_SW_NR_OSV | string | Softwarenummer (operating system version) |
| ID_SW_NR_RES | string | Softwarenummer (reserved - currently unused) |
| AIF_ADRESSE | long | AIF Adresse |
| AIF_FAHRGESTELL_NR | string | Fahrgestellnummer 7-stellig |
| AIF_PROGRAMMIER_DATUM | string | Datum der SG-Programmierung in der Form JJJJ.MM.TT |
| AIF_ZUSAMMENBAU_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_DATENSATZ_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_TESTER_NR | string | Tester Seriennummer |
| AIF_KM_STAND | long | km-Stand bei der Programmierung |
| AIF_PROGRAMM_STAND | string | Programmstandsnummer |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ANZ_DATEN | int | Groesse des AIF-Eintrags |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-status-obd"></a>
### STATUS_OBD

$21 05 Monitoring Funktionen und Status Bits

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_MISSFIRE_MONITOR | int | Statusbit Fehlzuendungen werden ueberwacht 1=Nein / 0=Ja |
| STAT_MISSFIRE | int | Fehlzuendungen Ueberwachung 0=Bereit / 1=Start |
| STAT_FUELSYSTEM_MONITOR | int | Kraftstoffsystem Diagnose vorhanden 1=Nein / 0=Ja |
| STAT_FUELSYSTEM | int | Kraftstoffsystem Diagnose 0=Bereit / 1=Start |
| STAT_COMPREHENSIVE_MONITOR | int | Umfassende Komponentenueberwachung vorhanden 1=Nein / 0=Ja |
| STAT_COMPREHENSIVE | int | Umfassende KomponentenUeberwachung 0=Bereit / 1=Start |
| STAT_KAT_UEBERWACHUNG_MONITOR | int | Katalysator Diagnose 0=Ein / 1=Aus |
| STAT_KAT_UEBERWACHUNG | int | Katalysator Ueberwachung 0=Bereit / 1=Start |
| STAT_KAT_HEIZUNG_MONITOR | int | Katheizung Diagnose 0=Ein / 1=Aus |
| STAT_KAT_HEIZUNG | int | Umfassende Katheizung Ueberwachung 0=Bereit / 1=Start |
| STAT_EVAPORATE_MONITOR | int | TankentlueftungsSystem Diagnose 0=Ein / 1=Aus |
| STAT_EVAPORATE | int | TankentlueftungsSystemUeberwachung 0=Bereit / 1=Start |
| STAT_SEC_AIR_MONITOR | int | Sekundaerluft Diagnose 0=Ein / 1=Aus |
| STAT_SEC_AIR | int | SekundaerluftSystemUeberwachung 0=Bereit / 1=Start |
| STAT_AC_SYSTEM_MONITOR | int | KlimaSystem Diagnose 0=Ein / 1=Aus |
| STAT_AC_SYSTEM | int | KlimaSystemUeberwachung 0=Bereit / 1=Start |
| STAT_LAMBDA_MONITOR | int | LambdaSonden Diagnose 0=Ein / 1=Aus |
| STAT_LAMBDA | int | LambdaSondenUeberwachung 0=Bereit / 1=Start |
| STAT_LAMBDA_HEATER_MONITOR | int | LambdasondenHeizungs Diagnose 0=Ein / 1=Aus |
| STAT_LAMBDA_HEATER | int | LambdasondenHeizungsUeberwachung 0=Bereit / 1=Start |
| STAT_EGR_MONITOR | int | AbgasRueckfuehrungsDiagnose 0=Ein / 1=Aus |
| STAT_EGR | int | AbgasRueckfuehrungsSystemUeberwachung 0=Bereit / 1=Start |

<a id="job-status-readiness"></a>
### STATUS_READINESS

$21 05 Monitoring Funktionen und Status Bits

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_KATRDY_EIN | int | Katalysator Readiness gesetzt 0=Nein / 1=Ja |
| STAT_HKATRDY_EIN | int | Umfassende Katheizung Readiness gesetzt 0=Nein / 1=Ja |
| STAT_TESRDY_EIN | int | Tankentlueftung Readiness gesetzt 0=Nein / 1=Ja |
| STAT_SLSRDY_EIN | int | Sekundaerluft Readiness gesetzt 0=Nein / 1=Ja |
| STAT_KLIMARDY_EIN | int | KlimaSystem Readiness gesetzt 0=Nein / 1=Ja |
| STAT_LSRDY_EIN | int | LambdaSonden Readiness gesetzt 0=Nein / 1=Ja |
| STAT_HSRDY_EIN | int | LambdasondenHeizung Readiness gesetzt 0=Nein / 1=Ja |
| STAT_AGRRDY_EIN | int | AbgasRueckfuehrung Readiness gesetzt 0=Nein / 1=Ja |

<a id="job-ews-empfang"></a>
### EWS_EMPFANG

EWS-Empfangsstatus auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| EWS_EMPFANGSSTATUS | string | Rueckgabestatus bei der Startwertinitialisierung |
| EWS_STATUS_VALUE | int | Rueckgabestatus bei der Startwertinitialisierung |

<a id="job-status-fgr"></a>
### STATUS_FGR

$21 07 MFL MultiFunktionsLekrad STATE_MSW_CAN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_MSW_CAN | string | Status STATE_MSW_CAN 0 bis 6 |
| STAT_PLUS | int | Status 01 + 0=Nein / 1=Ja |
| STAT_MINUS | int | Status 02 - 0=Nein / 1=Ja |
| STAT_SET | int | Status 03 Set 0=Nein / 1=Ja |
| STAT_OFF | int | Status 04 I/O 0=Nein / 1=Ja |

<a id="job-distance-mil-on"></a>
### DISTANCE_MIL_ON

Auslesen Fahrstrecke mit MIL-eingeschaltet KWP 2000* $21 09 DIST_ACT_MIL ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DISTANZ_MIL_WERT | real | Fahrstrecke mit MIL an 0 - 214.748.364,7 km Auflösung 0,1 km |
| STAT_DISTANZ_MIL_EINH | string | Einheit km |

<a id="job-status-systemcheck-sek-luft"></a>
### STATUS_SYSTEMCHECK_SEK_LUFT

Stand der Diagnose KWP 2000* $21 20 Status Systemtest SLS SekundärLuftSystem

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DIAGNOSE_WERT | int | Zahlenwert Diagnose Ablauf |
| STAT_SYSTEMCHECK_SEK_LUFT_WERT | int | Zahlenwert Diagnose Ablauf |
| STAT_DIAGNOSE_TEXT | string | Text Diagnose Ablauf 0=läuft 1=Start verhindert 5=stop 8=Ende ohne Fehler |

<a id="job-status-systemcheck-tev-func"></a>
### STATUS_SYSTEMCHECK_TEV_FUNC

Status und Messströme KWP 2000* $21 22 RequestRoutineResultsByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DIAGNOSE_WERT | int | 0=Init ... |
| STAT_SYSTEMCHECK_TEV_FUNC_WERT | int | 0=Init ... |
| STAT_DIAGNOSE_TEXT | string | 0=Init ... |

<a id="job-status-systemcheck-tev"></a>
### STATUS_SYSTEMCHECK_TEV

Stand der Diagnose KWP 2000* $21 22 TEV ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DIAGNOSE_WERT | int | Zahlenwert Diagnose Ablauf |
| STAT_DIAGNOSE_TEXT | string | Text Diagnose Ablauf 0=aktiv ... |

<a id="job-status-systemcheck-evausbl"></a>
### STATUS_SYSTEMCHECK_EVAUSBL

welches EV-Ventil ist abgeschaltet KWP 2000* $21 25 RequestRoutineResultsByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DIAGNOSE_WERT | int | 0=Init ... |
| STAT_DIAGNOSE_TEXT | string | 0=Init ... |

<a id="job-status-systemcheck-vvt-anschlag"></a>
### STATUS_SYSTEMCHECK_VVT_ANSCHLAG

Stand der Diagnose KWP 2000* $21 27 VVT ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_VVT_ANSCHL_WERT | int | Status des Lernens Bank1 0 bis 9 |
| STAT_VVT_ANSCHL_TEXT | string | Status des Lernens Bank1 als Text |

<a id="job-status-digital-3"></a>
### STATUS_DIGITAL_3

Statusbit KOmpressorRELais KWP 2000* $21 36 LV_ACCOUT_RLY ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_KO_EIN | int | Relais angezogen 0=nein 1=ja |

<a id="job-status-digital-4"></a>
### STATUS_DIGITAL_4

Statusbit LeerLauf KWP 2000* $21 3F LV_IS ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_LL_EIN | int | LeerLauf aktiv 0=nein 1=ja |

<a id="job-status-l-sonde-heizung-h-2"></a>
### STATUS_L_SONDE_HEIZUNG_H_2

Auslesen des Reglerzustands der Sondenheizung KWP 2000* $21 41 STATE_LSH_DOWN_2 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_L_SONDE_HEIZUNG_WERT | int | Status Wert 0=aus bis 5 Überspannungsschutz |
| STAT_L_SONDE_HEIZUNG_EINH | string | Einheit ohne |
| STAT_L_SONDE_HEIZUNG_TEXT | string | Text Regelzustand L-Sonde Heizung |

<a id="job-status-l-sonde-heizung-h-1"></a>
### STATUS_L_SONDE_HEIZUNG_H_1

Auslesen des Reglerzustands der Sondenheizung KWP 2000* $21 42 STATE_LSH_DOWN_1 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_L_SONDE_HEIZUNG_WERT | int | Status Wert 0=aus bis 5 Überspannungsschutz |
| STAT_L_SONDE_HEIZUNG_EINH | string | Einheit ohne |
| STAT_L_SONDE_HEIZUNG_TEXT | string | Text Regelzustand L-Sonde Heizung |

<a id="job-status-l-sonde-heizung-v-2"></a>
### STATUS_L_SONDE_HEIZUNG_V_2

Auslesen des Reglerzustands der Sondenheizung KWP 2000* $21 43 STATE_LSH_UP_2 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_L_SONDE_HEIZUNG_WERT | int | Status Wert 0=aus bis 6 Temperaturschutz |
| STAT_L_SONDE_HEIZUNG_EINH | string | Einheit ohne |
| STAT_L_SONDE_HEIZUNG_TEXT | string | Text Regelzustand L-Sonde Heizung |

<a id="job-status-l-sonde-heizung-v-1"></a>
### STATUS_L_SONDE_HEIZUNG_V_1

Auslesen des Reglerzustands der Sondenheizung KWP 2000* $21 44 STATE_LSH_UP_1 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_L_SONDE_HEIZUNG_WERT | int | Status Wert 0=aus bis 6 Temperaturschutz |
| STAT_L_SONDE_HEIZUNG_EINH | string | Einheit ohne |
| STAT_L_SONDE_HEIZUNG_TEXT | string | Text Regelzustand L-Sonde Heizung |

<a id="job-status-ews-lock"></a>
### STATUS_EWS_LOCK

Statusbit LV_LOCK_IMOB = 1 blockt Zündung und Einspritzung KWP 2000* $21 49 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_EWS_LOCK_WERT | int | EWS/CAS blockiert Zündung/Einspritzung 0=nein 1=ja |

<a id="job-status-zeit-einspritz"></a>
### STATUS_ZEIT_EINSPRITZ

Auslesen der Einspritzzeit Zyl. 1 KWP 2000* $21 4C BIOS_TI_0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_ZEIT_WERT | real | Wert von V_PVS_1 |
| STAT_ZEIT_EINH | string | Einheit in ms |

<a id="job-status-zuendwinkel"></a>
### STATUS_ZUENDWINKEL

Auslesen des Zündwinkels Zylinder 1 KWP 2000* $21 56 IGA_IGC_0 ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_ZUENDWINKEL_WERT | real | Wert von Zuendwinkel Zylinder 1 |
| STAT_ZUENDWINKEL_EINH | string | Einheit °KW |

<a id="job-status-drosselklappe"></a>
### STATUS_DROSSELKLAPPE

Auslesen des Drosselklappen Winkels KWP 2000* $21 57 TPS_AV ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DROSSELKLAPPE_WERT | real | Wert von TPS_AV |
| STAT_DROSSELKLAPPE_EINH | string | Einheit von TPS_AV |

<a id="job-status-klopfen"></a>
### STATUS_KLOPFEN

Auslesen des Status Klopfen erkannt 0/1 KWP 2000* $21 71 LV_KNK ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_KLOPFEN_WERT | int | Wert von Zuendwinkel Zylinder 1 |
| STAT_KLOPFEN_EINH | string | Einheit °KW |

<a id="job-status-kva"></a>
### STATUS_KVA

Auslesen Faktor KVA KWP 2000* $21 C1 kva-faktor ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_KVA_WERT | real | Wert von vsa_adp |
| STAT_KVA_EINH | string | Einheit von vsa_adp |

<a id="job-status-betriebsstundenzaehler"></a>
### STATUS_BETRIEBSSTUNDENZAEHLER

$ 21 C3 Status Betriebsstundenzaehler auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_BSZ_WERT | int | Status Betriebsstundenzaehler lesen 0 = &lt;10h, 1= &gt;= 10h, 2 = unbekannt |
| STAT_BSZ_TEXT | string | Status Betriebsstundenzaehler |
| STAT_TRT_WERT | real | Status Betriebsstundenzaehler lesen Variable TotalRunningTime |
| STAT_TRT_EINH | string | 1/10 s |

<a id="job-status-systemcheck-dmtl"></a>
### STATUS_SYSTEMCHECK_DMTL

Stand der Diagnose KWP 2000* $21 DA DMTL ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DIAGNOSE_WERT | int | Zahlenwert Diagnose Ablauf |
| STAT_SYSTEMCHECK_DMTL_WERT | int | Zahlenwert Diagnose Ablauf |
| STAT_DIAGNOSE_TEXT | string | Text Diagnose Ablauf 0=aktiv ... |

<a id="job-status-systemcheck-l-sonde"></a>
### STATUS_SYSTEMCHECK_L_SONDE

Stand der Diagnose KWP 2000* $21 DF vertauschte L-Sonden ReadDataByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DIAGNOSE_WERT | int | Zahlenwert Diagnose Ablauf |
| STAT_SYSTEMCHECK_L_SONDE_WERT | int | Zahlenwert Diagnose Ablauf |
| STAT_DIAGNOSE_TEXT | string | Text Diagnose Ablauf 1=läuft 3=Werte gültig 6=Start verhindert 7=nicht gestartet |

<a id="job-status-leistungsstufe"></a>
### STATUS_LEISTUNGSSTUFE

Auslesen der Codierung Obere/Untere Leistungsstufe KWP2000: $22 ReadDataByCommonIdentifier $3020 RecordCommonIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LEISTUNGSSTUFE_WERT | int | Codierung für Leistungsstufe als Integer (0 = UL, 1 = ML, 2 = OL) |
| STAT_LEISTUNGSSTUFE_TEXT | string | Codierung für Leistungsstufe als Text |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Auslesen der Motordrehzahl und LL-Sollwert KWP 2000* $22 40 00 Auszug

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_MOTORDREHZAHL_WERT | real | Wert von Motordrehzahl |
| STAT_SOLL_MOTORDREHZAHL_WERT | real | Wert von LeerLaufSollDrehzahl |
| STAT_MOTORDREHZAHL_EINH | string | Einheit von Motordrehzahl |

<a id="job-status-dfmonitor"></a>
### STATUS_DFMONITOR

Generator Belastung KWP2000: $22 40 01 ReadDataByCommonIdentifier dfmonitor

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_AUSGANG_WERT | real | DF-Monitor Wert 0 - 100% |
| STAT_AUSGANG_EINH | string | DF-Monitor Einheit % |
| STAT_AUSGANG_TEXT | string | DF-Monitor Text |

<a id="job-status-digital-1"></a>
### STATUS_DIGITAL_1

Status Schaltzustaende

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | $22 40 02 Schalterpositionen |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_KL15_EIN | int | Schalter Zuendung aktiv 0=Nein / 1=Ja Ignition Key Position on LV_IGK |
| STAT_MOTOR_AUS | int | Motor steht, LV_ESTART an 0=Nein / 1=Ja |
| STAT_KUPPL_EIN | int | Schalter Kupplung aktiv 0=Nein / 1=Ja Clutch Switch on LV_CS |
| STAT_BLS_EIN | int | Schalter BremsLicht aktiv 0=Nein / 1=Ja Brake Light Switch on LV_IM_BLS |
| STAT_BLTS_EIN | int | Schalter BLTS aktiv 0=Nein / 1=Ja Brake Test Switch on LV_IM_BTS |
| STAT_KO_EIN | int | Anforderung Klimabereitschaft LV_ACCOUT_RLY 0=Aus / 1=Ein |
| STAT_AC_EIN | int | Kopie von STAT_KO_EIN |

<a id="job-status-motorlaufunruhe"></a>
### STATUS_MOTORLAUFUNRUHE

$22 40 03 Laufunruhe fuer 6 Zylinder lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MOTORLAUFUNRUHE_EINH | string | dimensionslos |
| STAT_ZYL1_WERT | real | gefilterte Laufunruhe Zylinder 1 Wertebereich 0 bis 40 |
| STAT_ZYL1_TEXT | string | Beschreibungstext |
| STAT_ZYL2_WERT | real | gefilterte Laufunruhe Zylinder 2 Wertebereich 0 bis 40 |
| STAT_ZYL2_TEXT | string | Beschreibungstext |
| STAT_ZYL3_WERT | real | gefilterte Laufunruhe Zylinder 3 Wertebereich 0 bis 40 |
| STAT_ZYL3_TEXT | string | Beschreibungstext |
| STAT_ZYL4_WERT | real | gefilterte Laufunruhe Zylinder 4 Wertebereich 0 bis 40 |
| STAT_ZYL4_TEXT | string | Beschreibungstext |
| STAT_ZYL5_WERT | real | gefilterte Laufunruhe Zylinder 5 Wertebereich 0 bis 40 |
| STAT_ZYL5_TEXT | string | Beschreibungstext |
| STAT_ZYL6_WERT | real | gefilterte Laufunruhe Zylinder 6 Wertebereich 0 bis 40 |
| STAT_ZYL6_TEXT | string | Beschreibungstext |
| STAT_VLS_UP_WERT1 | real | Spannung Lambdasonde Bank1 VK 0 bis 5V (FFC0 = 3FF*64) |
| STAT_VLS_UP_TEXT1 | string | Beschreibungstext |
| STAT_VLS_UP_WERT2 | real | Spannung Lambdasonde Bank2 VK 0 bis 5V (FFC0 = 3FF*64) |
| STAT_VLS_UP_TEXT2 | string | Beschreibungstext |
| STAT_GEBERRAD_ADAPTION_WERT | int | Kurbelwelle Segmentadaption beendet 0=nein / 1=ja |

<a id="job-status-geberrad-adaption"></a>
### STATUS_GEBERRAD_ADAPTION

$2C F0 02 DDLI Messwerte für NWG-Adaptionen auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an SG alten Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG alten Block löschen |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |
| STAT_ANZAHL_WERTE | int | Anzahl Messwerte 0 bis 1 |
| STAT_GEBERRAD_ADAPTION_VSA_WERT | real | Wert von vsa_adp |
| STAT_GEBERRAD_ADAPTION_VSA_TEXT | string | Text von vsa_adp |
| STAT_GEBERRAD_ADAPTION_VSE_WERT | real | Wert von vse_adp |
| STAT_GEBERRAD_ADAPTION_VSE_TEXT | string | Text von vse_adp |
| STAT_GEBERRAD_ADAPTION_EINH | string | Einheit in Grd KW |
| STAT_SEG_AD_WERT | int | Kurbelwelle Segmentadaption beendet 0=nein / 1=ja |

<a id="job-status-nockenwelle-adaption"></a>
### STATUS_NOCKENWELLE_ADAPTION

$22 40 06 Nockenwellen Adaptionen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_EINH | string | Einheit der Werte ° Kurbelwelle |
| STAT_PSN_EDGE_AD_CAM_IN | real | Adaptierte Werte NW Einlass 1 Werte -32 bis +32 |
| STAT_PSN_EDGE_AD_CAM_IN_TEXT | string | Beschreibungstext |
| STAT_PSN_EDGE_AD_CAM_EX | real | Adaptierte Werte NW Auslass 1 Werte -32 bis +32 |
| STAT_PSN_EDGE_AD_CAM_EX_TEXT | string | Beschreibungstext |
| STAT_NC_PSN_EDGE_CAM_IN | real | Position zu TDC0 NW-Einlass Werte 0 bis 720 |
| STAT_NC_PSN_EDGE_CAM_IN_TEXT | string | Beschreibungstext |
| STAT_NC_PSN_EDGE_CAM_EX | real | Position zu TDC0 NW-Einlass Werte 0 bis 720 |
| STAT_NC_PSN_EDGE_CAM_EX_TEXT | string | Beschreibungstext |

<a id="job-status-digital-0"></a>
### STATUS_DIGITAL_0

Status Schaltzustaende $22 40 07 Betriebszustaende

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_LL_EIN | int | Leerlauf LV_LL 0=Nein / 1=Ja |
| STAT_SBBHK2 | int | Lambdaregelung Bank2 hinter Kat LV_DOWN_LS_2 0=aus, 1=ein |
| STAT_SBBHK | int | Lambdaregelung Bank1 hinter Kat LV_DOWN_LS_1 0=aus, 1=ein |
| STAT_SBBVK2 | int | Lambdaregelung Bank2 vor Kat LV_UP_LS_2 0=aus, 1=ein |
| STAT_SBBVK | int | Lambdaregelung Bank1 vor Kat LV_UP_LS_1 0=aus, 1=ein |

<a id="job-status-funktions"></a>
### STATUS_FUNKTIONS

Status Schaltzustaende $22 40 07 Betriebszustaende

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_LL_EIN | int | Leerlauf LV_LL 0=Nein / 1=Ja |
| STAT_TEILLAST_EIN | int | Teillast 0=Nein / 1=Ja, wenn LL=0 und VL=0 |
| STAT_VL_EIN | int | BeschleunigungsanreicherungLV_FL  0=Aus / 1=Ein |
| STAT_LSHK2_EIN | int | Lambdaregelung Bank2 hinter Kat LV_DOWN_LS_2 0=aus, 1=ein |
| STAT_LSHK1_EIN | int | Lambdaregelung Bank1 hinter Kat LV_DOWN_LS_1 0=aus, 1=ein |
| STAT_LSVK2_EIN | int | Lambdaregelung Bank2 vor Kat LV_UP_LS_2 0=aus, 1=ein |
| STAT_LSVK1_EIN | int | Lambdaregelung Bank1 vor Kat LV_UP_LS_1 0=aus, 1=ein |
| STAT_LS2_REGELUNG | int | Regelkreis Bank 2 geschlossen LV_LSCL_2 0=Nein / 1=Ja |
| STAT_LS1_REGELUNG | int | Regelkreis Bank 1 geschlossen LV_LSCL_1 0=Nein / 1=Ja |
| STAT_KICKDOWN | int | Kickdown erkannt 0=nein / 1=ja |
| STAT_FAHRSTUFE | int | Gang eingelegt ,nicht Park/Neutral |
| STAT_SCHUBAB | int | Schubabschaltung 0=Aus / 1=Ein |
| STAT_DK_ABGLEICH | int | DK Abgleich neu lernen 0=nein / 1=erforderlich |
| STAT_DYN_LIM_1 | int | EGAS 1 Notlauf Limit dynamic 1 0=Aus / 1=Ein |
| STAT_DYN_LIM_2 | int | EGAS 2 Notlauf Limit dynamic 2 0=Aus / 1=Ein |
| STAT_FEHLER_CLSW | int | Fehler Kupplungsschalter 0=nein / 1=ja |
| STAT_FEHLER_MFL | int | Fehler MFL 0=nein / 1=ja |
| STAT_TIMEOUT_EGS1 | int | Timeout EGS 1 0=nein / 1=ja |
| STAT_FEHLER_BREMSE | int | Fehler Bremse 0=nein / 1=ja |
| STAT_MON_LEVEL2 | int | Monitoring Ebene 2 0=nein / 1=ja |
| STAT_V_PLAUSIBEL | int | Geschwindigkeit plausibel 0=nein / 1=ja |
| STAT_NOTLAUF_LL | int | Notlauf LL Steller 0=nein / 1=ja |
| STAT_NOTLAUF_DK | int | Notlauf DK Steller 0=nein / 1=ja |
| STAT_FEHLER_VS | int | Fehler Geschwindigkeit 0=nein / 1=ja |
| STAT_ASR_TIMEOUT | int | ASR meldet sich nicht 0=nein / 1=ja |
| STAT_EGAS_NOTLAUF | int | EGAS im Notbetrieb 0=nein / 1=ja |
| STAT_VS_DIF_HOCH | int | Geschw. Differenz zu hoch 0=nein / 1=ja |
| STAT_UEBERN_LANG | int | Übernahme zu lange 0=nein / 1=ja |
| STAT_VS_SP_MAX | int | Sollwert maximale Geschw. zu lang 0=nein / 1=ja |
| STAT_EXT_MOMENT | int | Externe Momenten Funktionseingriff 0=nein / 1=ja |
| STAT_MFL_AUS | int | MFL ausgeschaltet 0=nein / 1=ja |
| STAT_VS_CAN_LANG | int | CAN Geschwindigkeit Botschaft zu lang 0=nein / 1=ja |
| STAT_BESCHL_MON | int | Beschleunigungs Überwachung 0=aus / 1=ein |
| STAT_HOCHDREH_S | int | Run up lock Hochdrehsicherung 0=nein / 1=ja |
| STAT_TAKEOVER_VS | int | Übernehmen und Maximalgeschwindigkeit aktiv 0=nein / 1=ja |
| STAT_VS_FIL_LOW | int | Geschwindigkeit zu gering 0=nein / 1=ja |
| STAT_DREHZAHL_BEG | int | Drehzahlbegrenzer  0=nein / 1=ja |
| STAT_BREMSE_AKTIV | int | Bremsen festgestellt 0=nein / 1=ja |
| STAT_MFL_HARD_OFF | int | MFL Notaus 0=nein / 1=ja |

<a id="job-status-adaption-dk"></a>
### STATUS_ADAPTION_DK

$22 40 08 Adaption DK lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_FAC_EINH | string | Einheit ist % |
| STAT_ADD_EINH | string | Einheit ist cm² |
| STAT_DK_ADD_WERT | real | Adaption Leerlaufsteller Offset +-29,3 qcm |
| STAT_DK_ADD_TEXT | string | Beschreibungstext |
| STAT_DK_FAC_WERT | real | Adaption Leerlaufsteller multiplikativ +-50% |
| STAT_DK_FAC_TEXT | string | Beschreibungstext |

<a id="job-status-adaption-gemisch"></a>
### STATUS_ADAPTION_GEMISCH

$22 40 0A Adaption Lambda Regelung lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_ADD_WERT1 | real | Adaption Gemisch additiv Bank1 |
| STAT_ADD_TEXT1 | string | Beschreibungstext |
| STAT_ADD_WERT2 | real | Adaption Gemisch additiv Bank2 |
| STAT_ADD_TEXT2 | string | Beschreibungstext |
| STAT_ADD_EINH | string | Einheit |
| STAT_FAC_WERT1 | real | Adaption Gemisch multiplikativ Bank1 |
| STAT_FAC_TEXT1 | string | Beschreibungstext |
| STAT_FAC_WERT2 | real | Adaption Gemisch multiplikativ Bank2 |
| STAT_FAC_TEXT2 | string | Beschreibungstext |
| STAT_FAC_EINH | string | Einheit |
| STAT_PWM_UP_WERT1 | real | PWM vor Kat Bank1 |
| STAT_PWM_UP_WERT2 | real | PWM vor Kat Bank2 |
| STAT_PWM_DOWN_WERT1 | real | PWM hinter Kat Bank1 |
| STAT_PWM_DOWN_WERT2 | real | PWM hinter Kat Bank2 |
| STAT_PWM_EINH | string | Einheit % |
| STAT_PWM_UP_TEXT1 | string | vor Kat Bank 1 |
| STAT_PWM_UP_TEXT2 | string | vor Kat Bank 2 |
| STAT_PWM_DOWN_TEXT1 | string | vor Kat Bank 1 |
| STAT_PWM_DOWN_TEXT2 | string | vor Kat Bank 2 |

<a id="job-status-fasta-common"></a>
### STATUS_FASTA_COMMON

Messwerteblock lesen KWP2000: $2C F0 02 DynamicallyDefinedLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an SG alten Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG alten Block löschen |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_AMP_MES_WERT | real | Umgebungsdruck |
| STAT_AMP_MES_EINH | string | Einheit hPa |
| STAT_DIST_ACT_MIL_WERT | real | Fahrstrecke mit MIL an |
| STAT_DIST_ACT_MIL_EINH | string | Einheit km |
| STAT_OZOELKM_WERT | real | km seit letztem Service |
| STAT_OZOELKM_EINH | string | Einheit km |
| STAT_OZKVBSM_UL_WERT | real | Kraftstoff-Verbrauch seit letztem Service |
| STAT_OZKVBSM_UL_EINH | string | Einheit l |
| STAT_N_WERT | real | Motor Drehzahl |
| STAT_N_EINH | string | Einheit rpm |
| STAT_N_SP_IS_WERT | real | Leerlauf Solldrehzahl |
| STAT_N_SP_IS_EINH | string | Einheit rpm |
| STAT_T_ES_WERT | real | Motorabstellzeit |
| STAT_T_ES_EINH | string | Einheit min |
| STAT_TCO_WERT | real | Kühlwassertemperatur |
| STAT_TCO_EINH | string | Einheit C |
| STAT_TCO_2_WERT | real | Kuehlerauslasstemperatur |
| STAT_TCO_2_EINH | string | Einheit C |
| STAT_TCO_ST_WERT | real | Motortemperatur beim Start |
| STAT_TCO_ST_EINH | string | Einheit C |
| STAT_TIA_WERT | real | Ansauglufttemperatur |
| STAT_TIA_EINH | string | Einheit C |
| STAT_TOEL_WERT | real | Öltemperatur |
| STAT_TOEL_EINH | string | Einheit C |
| STAT_VB_BAS_KWP_WERT | real | Spannung Kl. 87 |
| STAT_VB_BAS_KWP_EINH | string | Einheit C |
| STAT_STATE_ETC_LIH_WERT | real | Status Drosselklappe Notlauf |
| STAT_STATE_ETC_LIH_EINH | string | Einheit keine |
| STAT_CAM_SP_IVVT_EX_WERT | real | Nockenwelle Auslass Sollwert |
| STAT_CAM_SP_IVVT_EX_EINH | string | Einheit °CRK |
| STAT_CAM_SP_IVVT_IN_WERT | real | Nockenwelle Einlass Sollwert |
| STAT_CAM_SP_IVVT_IN_EINH | string | Einheit °CRK |
| STAT_ER_CYL_0_WERT | real | Laufunruhe Zylinder 1 |
| STAT_ER_CYL_0_EINH | string | Einheit keine |
| STAT_ER_CYL_1_WERT | real | Laufunruhe Zylinder 5 |
| STAT_ER_CYL_1_EINH | string | Einheit keine |
| STAT_ER_CYL_2_WERT | real | Laufunruhe Zylinder 3 |
| STAT_ER_CYL_2_EINH | string | Einheit keine |
| STAT_ER_CYL_3_WERT | real | Laufunruhe Zylinder 6 |
| STAT_ER_CYL_3_EINH | string | Einheit keine |
| STAT_ER_CYL_4_WERT | real | Laufunruhe Zylinder 2 |
| STAT_ER_CYL_4_EINH | string | Einheit keine |
| STAT_ER_CYL_5_WERT | real | Laufunruhe Zylinder 4 |
| STAT_ER_CYL_5_EINH | string | Einheit keine |
| STAT_IGA_IGC_0_WERT | real | Zündwinkel Zylinder 1 |
| STAT_IGA_IGC_0_EINH | string | Einheit keine |
| STAT_LSHPWM_UP_1_WERT | real | Lambdasondenheizung PWM vor Kat Bank 1 |
| STAT_LSHPWM_UP_1_EINH | string | Einheit % |
| STAT_LSHPWM_UP_2_WERT | real | Lambdasondenheizung PWM vor Kat Bank 2 |
| STAT_LSHPWM_UP_2_EINH | string | Einheit % |
| STAT_LSHPWM_DOWN_1_WERT | real | Lambdasondenheizung PWM nach Kat Bank 1 |
| STAT_LSHPWM_DOWN_1_EINH | string | Einheit % |
| STAT_LSHPWM_DOWN_2_WERT | real | Lambdasondenheizung PWM nach Kat Bank 2 |
| STAT_LSHPWM_DOWN_2_EINH | string | Einheit % |
| STAT_MAF_KGH_MES_BAS_WERT | real | Luftmasse |
| STAT_MAF_KGH_MES_BAS_EINH | string | Einheit kg/h |
| STAT_TQ_DIF_I_IS_MON_WERT | real | I-Anteil Momentdifferenz Überwachung und Modell |
| STAT_TQ_DIF_I_IS_MON_EINH | string | Einheit Nm |

<a id="job-ecu-config"></a>
### ECU_CONFIG

$22 5F F2 Fahrzeug Varianten lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_AT | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_AT_TEXT | string | Automatik Getriebe |
| STAT_AC | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_AC_TEXT | string | KlimaAnlage |
| STAT_AMT | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_AMT_TEXT | string | SMG Sequentielles Manuelles Getriebe |
| STAT_ARS | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_ARS_TEXT | string | Roll Stabilisierung |
| STAT_ASR | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_ASR_TEXT | string | ASR Anti Schlupf Regelung |
| STAT_DUMMY | int | not used yet |
| STAT_DUMMY_TEXT | string | Not used yet |
| STAT_BN_MSW | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_BN_MSW_TEXT | string | Multifunktions Lenkrad über CAN vorhanden |
| STAT_DCC | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_DCC_TEXT | string | Entfernungs-Überwachung vorhanden |
| STAT_EBOX_CFA | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_EBOX_CFA_TEXT | string | E-Box Lüfter vorhanden |
| STAT_ETCU | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_ETCU_TEXT | string | SMG/EGS Steuergerät vorhanden |
| STAT_ICL | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_ICL_TEXT | string | Kombi über CAN vorhanden |
| STAT_MSW | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_MSW_TEXT | string | MultiFunktionsLenkrad vorhanden |
| STAT_PSTE | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_PSTE_TEXT | string | elektrische Lenkung vorhanden |
| STAT_SOF | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_SOF_TEXT | string | Soundklappe vorhanden |
| STAT_SOF_SWI | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_SOF_SWI_TEXT | string | Sport-Taster vorhanden |
| STAT_GEAR | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_GEAR_TEXT | string | Komfort-Start vorhanden |
| STAT_DUMMY1 | int | not used yet |
| STAT_DUMMY_TEXT1 | string | not used yet |
| STAT_VEH | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_VEH_TEXT | string | Fahrzeugvariante mit Power Modul (E60/E65) erkannt - nur BN 2000 |
| STAT_SAP_VORHANDEN | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_SAP_VORHANDEN_TEXT | string | Sekundär Luft Pumpe vorhanden |
| STAT_EF | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_EF_TEXT | string | Abgas-Klappe vorhanden |
| STAT_ECRAS | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_ECRAS_TEXT | string | Kühler Jalousie vorhanden |
| STAT_RLY_ACCOUT | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_RLY_ACCOUT_TEXT | string | KlimaRelais vorhanden |
| STAT_SAV | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_SAV_TEXT | string | SecundaryAir Ventil vorhanden |
| STAT_RLY_ST | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_RLY_ST_TEXT | string | Starter Relais vorhanden |
| STAT_ASR3 | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_ASR3_TEXT | string | ASR3 Bauteil vorhanden |
| STAT_BN_LDM | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_BN_LDM_TEXT | string | LDM detected (E9x only) |
| STAT_BN_LTG_HDLP_L | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_BN_LTG_HDLP_L_TEXT | string | Dipped Beam via CAN recognized (BN2000 only) |
| STAT_LSH_DOWN | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_LSH_DOWN_TEXT | string | variant for CAT/exahust type |
| STAT_LSH_UP | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_LSH_UP_TEXT | string | variant for CAT/exahust type |
| STAT_ASR_4 | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_ASR_4_TEXT | string | ASC4 device recognized |
| STAT_MAF | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_MAF_TEXT | string | variant mass air flow meter |
| STAT_PST_2 | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_PST_2_TEXT | string | LV power steering detected - BN2000 |
| STAT_BN_EFP | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_BN_EFP_TEXT | string | EFP via CAN recognized (BN2000 only) |
| STAT_SENS_BAT_SMT_DET | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_SENS_BAT_SMT_DET_TEXT | string | IBS has been detected |
| STAT_BN_TRL | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_BN_TRL_TEXT | string | TRL detected |
| STAT_BN_HIV | int | Status der Variante 0=nicht vorhanden / 1=vorhanden |
| STAT_BN_HIV_TEXT | string | HI-valve detected |

<a id="job-speicher-lesen-ascii"></a>
### SPEICHER_LESEN_ASCII

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
| DATEN_ASCII | string | ausgelesene Daten als ASCII Format |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecu-config-reset"></a>
### ECU_CONFIG_RESET

$22 5F F2 04 gelernte FahrzeugVarianten löschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE_1 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_2 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_3 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_4 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_5 | int | Bit=1 löscht Bit=0 behält alten Wert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-add"></a>
### STATUS_ADD

Auslesen der additiven Korrektur Bank 1 KWP 2000*  MFF_AD_ADD_MMV_REL[1]

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_ADD_WERT | real | +-694,5 Wert von MFF_AD_ADD_MMV_REL[1] |
| STAT_ADD_EINH | string | Einheit in mg/Hub |

<a id="job-status-add-2"></a>
### STATUS_ADD_2

Auslesen der additiven Korrektur Bank 2 KWP 2000*  MFF_AD_ADD_MMV_REL[2]

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_ADD_2_WERT | real | +-694,5 Wert von MFF_AD_ADD_MMV_REL[2] |
| STAT_ADD_EINH | string | Einheit in mg/Hub |

<a id="job-status-mul"></a>
### STATUS_MUL

Auslesen des Korrekturfaktors Bank 1 KWP 2000*  MFF_AD_FAC_MMV_REL[1]

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_MUL_WERT | real | +-50 Wert von MFF_AD_FAC_MMV_REL[1] |
| STAT_MUL_EINH | string | Einheit in % |

<a id="job-status-mul-2"></a>
### STATUS_MUL_2

Auslesen des Korrekturfaktors Bank 1 KWP 2000*  MFF_AD_FAC_MMV_REL[2]

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_MUL_2_WERT | real | +-50 Wert von MFF_AD_FAC_MMV_REL[2] |
| STAT_MUL_EINH | string | Einheit in % |

<a id="job-status-int"></a>
### STATUS_INT

Auslesen des Integrator Bank 1 KWP 2000*  TI_LAM_COR[1]

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_INT_WERT | real | +-50 Wert von TI_LAM_COR[1] |
| STAT_INT_EINH | string | Einheit in % |

<a id="job-status-int-2"></a>
### STATUS_INT_2

Auslesen des Integrator Bank 1 KWP 2000*  TI_LAM_COR[1]

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_INT_2_WERT | real | +-50 Wert von TI_LAM_COR[1] |
| STAT_INT_EINH | string | Einheit in % |

<a id="job-status-ll-abgleich"></a>
### STATUS_LL_ABGLEICH

LL-Abgleichswerte lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFS_ACC_DRI | int | Abgleichswert LL mit Klima und Fahrbedingung |
| STAT_OFS_DRI | int | Abgleichswert LL mit Fahrstufe |
| STAT_OFS | int | Abgleichswert LL |
| STAT_OFS_ACC | int | Abgleichswert LL mit Klimaanlage |
| STAT_OFS_VB | int | Abgleichswert LL mit niedriger UBatt |
| STAT_OFS_EINH | string | Einheit LL-Drehzahl immer 1/min |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwort vom SG |
| _TEL_AUFTRAG | binary | Auftrag an SG |

<a id="job-steuern-ll-abgleich"></a>
### STEUERN_LL_ABGLEICH

LL-Abgleich vorgegeben -256 bis +254

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFS_ACC_DRI | int | Abgleichswert LL mit Klima und Fahrbedingung |
| STAT_OFS_DRI | int | Abgleichswert LL mit Fahrstufe |
| STAT_OFS | int | Abgleichswert LL |
| STAT_OFS_ACC | int | Abgleichswert LL mit Klimaanlage |
| STAT_OFS_VB | int | Abgleichswert LL mit niedriger UBatt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwort vom SG |
| _TEL_AUFTRAG | binary | Auftrag an SG |

<a id="job-steuern-llabg-prog"></a>
### STEUERN_LLABG_PROG

LL-Abgleichswerte werden vorgegeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFS_ACC_DRI | int | Abgleichswert LL mit Klima und Fahrbedingung |
| STAT_OFS_DRI | int | Abgleichswert LL mit Fahrstufe |
| STAT_OFS | int | Abgleichswert LL |
| STAT_OFS_ACC | int | Abgleichswert LL mit Klimaanlage |
| STAT_OFS_VB | int | Abgleichswert LL mit niedriger UBatt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_ANTWORT | binary | Antwort vom SG |
| _TEL_AUFTRAG | binary | Auftrag an SG |

<a id="job-flash-crc-pruefen"></a>
### FLASH_CRC_PRUEFEN

Codier Checksumme pruefen KWP2000: $31 StartRoutineByLocalIdentifier $01 Checksum

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZEIT | int | Zeit in Sekunden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-dme-startwert-abgleich"></a>
### DME_STARTWERT_ABGLEICH

Kopiert die ISN auf beide Wechselcodes KWP2000: $31 StartRoutineByLocalIdentifier LocalIdentifier $20 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-sek-luft"></a>
### START_SYSTEMCHECK_SEK_LUFT

$31 20 Systemdiagnose SLS SekundärLuftSystem starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-tev-func"></a>
### START_SYSTEMCHECK_TEV_FUNC

$31 22 Systemdiagnose TEVstarten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-evausbl"></a>
### START_SYSTEMCHECK_EVAUSBL

$31 25 Systemdiagnose Einspritzventil abschalten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VENTIL_NR | int | Zylinder 1 bis 6 Ventil ausgeblenden oder 63 alle |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-llerh"></a>
### START_SYSTEMCHECK_LLERH

$31 26 Systemdiagnose EOL LL-Erhöhen starten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LL_WERT | int | LL-Sollwert 0 bis 2000 1/min |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-vvt-anschlag"></a>
### START_SYSTEMCHECK_VVT_ANSCHLAG

$31 27 Systemdiagnose VVT-Anschläge lernen starten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARAMETER | int | 1 unten lernen, 6 beide lernen, 2 Byte Befehl sonst |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ews-startwert"></a>
### EWS_STARTWERT

EWS-Startwertinitialisierung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| EWS_STATUS | string | Rueckgabestatus bei der Startwertinitialisierung |
| STAT_EWS_WERT | int | Rueckgabewert bei der Startwertinitialisierung |

<a id="job-start-systemcheck-l-regelung-aus"></a>
### START_SYSTEMCHECK_L_REGELUNG_AUS

$31 D9 01 Systemdiagnose LambdaRegelung abschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-l-regelung-aus"></a>
### STOP_SYSTEMCHECK_L_REGELUNG_AUS

$31 D9 01 Systemdiagnose LambdaRegelung einschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-dmtl"></a>
### START_SYSTEMCHECK_DMTL

$31 DA Systemdiagnose DMTL starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-l-sonde"></a>
### START_SYSTEMCHECK_L_SONDE

$31 DF Systemdiagnose vertauschte L-Sonden starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-reset-cru-off"></a>
### RESET_CRU_OFF

$31 F4 STATE_CRU_OFF_IRR und STATE_CRU_OFF_REV löschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-vvt-sollwert"></a>
### START_SYSTEMCHECK_VVT_SOLLWERT

$31 FE Systemdiagnose VVT Steuerung ueber CAN freigeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-vvt-sollwert"></a>
### STOP_SYSTEMCHECK_VVT_SOLLWERT

$31 FE Systemdiagnose VVT Steuerung ueber CAN freigeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-sek-luft"></a>
### STOP_SYSTEMCHECK_SEK_LUFT

$32 20 Systemdiagnose SekundärLuftSystem beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-tev-func"></a>
### STOP_SYSTEMCHECK_TEV_FUNC

$32 22 Systemdiagnose TEV beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-evausbl"></a>
### STOP_SYSTEMCHECK_EVAUSBL

$32 25 Ende Systemtest Ventil Abschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-llerh"></a>
### STOP_SYSTEMCHECK_LLERH

$32 26 EOL-Test LL-Anheben beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-vvt-anschlag"></a>
### STOP_SYSTEMCHECK_VVT_ANSCHLAG

$32 27 Systemdiagnose VVT-Anschläge lernen starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-dmtl"></a>
### STOP_SYSTEMCHECK_DMTL

$32 DA Systemdiagnose DMTL beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-l-sonde"></a>
### STOP_SYSTEMCHECK_L_SONDE

$32 DF Systemdiagnose vertauschte L-Sonden beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-sek-lambda-wert"></a>
### STATUS_SYSTEMCHECK_SEK_LAMBDA_WERT

Status und Luftmassen KWP 2000* $33 20 RequestRoutineResultsByLocalIdentifier 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DIAGNOSE_LAMBDA_WERT | int | Systemdiagnose SLS mit linearer Lambdasonde |
| STAT_DIAGNOSE_LAMBDA_TEXT | string | 0=Init ... |
| STAT_SUM_AFL_VLS_DIAG_SA_1_WERT | real | Lambdawert 0 -65535 |
| STAT_SUM_AFL_VLS_DIAG_SA_1_TEXT | string |  |
| STAT_SUM_AFL_VLS_DIAG_SA_1_EINH | string |  |
| STAT_SUM_AFL_VLS_DIAG_SA_2_WERT | real | Lambdawert 0 -65535 |
| STAT_SUM_AFL_VLS_DIAG_SA_2_TEXT | string |  |
| STAT_SUM_AFL_VLS_DIAG_SA_2_EINH | string |  |

<a id="job-status-systemcheck-tev-wert"></a>
### STATUS_SYSTEMCHECK_TEV_WERT

Status und Messströme KWP 2000* $33 22 RequestRoutineResultsByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DIAGNOSE_WERT | int | 0=Init ... |
| STAT_DIAGNOSE_TEXT | string | 0=Init ... |
| STAT_SYSTEMCHECK_TEV_FUNC_1_WERT | int | Zyklus 0 - 255 |
| STAT_SYSTEMCHECK_TEV_FUNC_1_TEXT | string |  |
| STAT_SYSTEMCHECK_TEV_FUNC_2_WERT | int | Zyklus 0 - 255 |
| STAT_SYSTEMCHECK_TEV_FUNC_2_TEXT | string |  |

<a id="job-status-systemcheck-llerh-wert"></a>
### STATUS_SYSTEMCHECK_LLERH_WERT

aktuelle Drehzahl N KWP 2000* $33 26 RequestRoutineResultsByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_SYSTEMCHECK_LLERH_WERT | int | LL Drehzahl |
| STAT_SYSTEMCHECK_LLERH_TEXT | string |  |

<a id="job-status-systemcheck-dmtl-wert"></a>
### STATUS_SYSTEMCHECK_DMTL_WERT

Status und Messströme KWP 2000* $33 DA RequestRoutineResultsByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DIAGNOSE_WERT | int | 0=Start ... C=Ende |
| STAT_DIAGNOSE_TEXT | string | 0=Start ... |
| STAT_STROM_REF_WERT | real | Messwert 0 - 400 mA |
| STAT_STROM_REF_EINH | string | Einheit mA |
| STAT_STROM_REF_TEXT | string | Strom Referenzleck |
| STAT_STROM_GROB_WERT | real | Messwert 0 - 400 mA |
| STAT_STROM_GROB_EINH | string | Einheit mA |
| STAT_STROM_GROB_TEXT | string | Strom Grobleck |
| STAT_STROM_WERT | real | Messwert 0 - 400 mA |
| STAT_STROM_EINH | string | Einheit mA |
| STAT_STROM_TEXT | string | Strom aktueller Wert |

<a id="job-status-systemcheck-l-sonde-werte"></a>
### STATUS_SYSTEMCHECK_L_SONDE_WERTE

Status und Messwerte KWP 2000* $33 DF RequestRoutineResultsByLocalIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_DIAGNOSE_1_WERT | int | 0=Init ... |
| STAT_DIAGNOSE_1_TEXT | string | 0=Init ... |
| STAT_SYSTEMCHECK_L_SONDE_WERT | int | Zahlenwert Diagnose Ablauf |
| STAT_DIAGNOSE_2_WERT | int | Zahlenwert Diagnose Ablauf |
| STAT_DIAGNOSE_2_TEXT | string | 0=Init ... |
| STAT_LAMB_LS_UP_AFR_EOL_1_WERT | real | Lambdawert vor Kat Bank 1 0 - 32 |
| STAT_LAMB_LS_UP_AFR_EOL_1_EINH | string | V |
| STAT_LAMB_LS_UP_AFR_EOL_1_TEXT | string |  |
| STAT_LAMB_LS_UP_AFR_EOL_2_WERT | real | Lambdawert vor Kat Bank 1 0 - 32 |
| STAT_LAMB_LS_UP_AFR_EOL_2_EINH | string | V |
| STAT_LAMB_LS_UP_AFR_EOL_2_TEXT | string |  |
| STAT_LAMB_LS_UP_AFL_EOL_1_WERT | real | Lambdawert vor Kat Bank 1 0 - 32 |
| STAT_LAMB_LS_UP_AFL_EOL_1_EINH | string | V |
| STAT_LAMB_LS_UP_AFL_EOL_1_TEXT | string |  |
| STAT_LAMB_LS_UP_AFL_EOL_2_WERT | real | Lambdawert vor Kat Bank 1 0 - 32 |
| STAT_LAMB_LS_UP_AFL_EOL_2_EINH | string | V |
| STAT_LAMB_LS_UP_AFL_EOL_2_TEXT | string |  |
| STAT_VLS_DOWN_AFR_EOL_1_WERT | real | Spannung vor Kat Bank 1 0 - 5 V |
| STAT_VLS_DOWN_AFR_EOL_1_EINH | string | V |
| STAT_VLS_DOWN_AFR_EOL_1_TEXT | string |  |
| STAT_VLS_DOWN_AFR_EOL_2_WERT | real | Spannung vor Kat Bank 2 0 - 5 V |
| STAT_VLS_DOWN_AFR_EOL_2_EINH | string | V |
| STAT_VLS_DOWN_AFR_EOL_2_TEXT | string |  |
| STAT_VLS_DOWN_AFL_EOL_1_WERT | real | Spannung vor Kat Bank 1 0 - 5 V |
| STAT_VLS_DOWN_AFL_EOL_1_EINH | string | V |
| STAT_VLS_DOWN_AFL_EOL_1_TEXT | string |  |
| STAT_VLS_DOWN_AFL_EOL_2_WERT | real | Spannung vor Kat Bank 2 0 - 5 V |
| STAT_VLS_DOWN_AFL_EOL_2_EINH | string | V |
| STAT_VLS_DOWN_AFL_EOL_2_TEXT | string |  |
| STAT_MAF_INT_MIN_VLS_EOL_WERT | real | Luftmasse 0 - 1820 g |
| STAT_MAF_INT_MIN_VLS_EOL_EINH | string | g |
| STAT_MAF_INT_MIN_VLS_EOL_TEXT | string |  |

<a id="job-steuern-kva"></a>
### STEUERN_KVA

Faktor KVA Korrektur vorgeben KWP 2000* $3B C1 kva-faktor WriteDataByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KVA_WERT | int | Faktor KVA 80 - 7F = -0,128 - 0,127 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Analogen Messwert periodisch lesen KWP2000: $2C F0 02 DynamicallyDefinedLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DEVICE | string | Nummer nach DDLI Liste |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an SG alten Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG alten Block löschen |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_ANALOG_TEXT | string | Beschreibung der Variablen |
| STAT_ANALOG_WERT | real | Wert skaliert nach DDLI Liste |
| STAT_ANALOG_EINH | string | Einheit aus DDLI Liste |

<a id="job-status-fasta2"></a>
### STATUS_FASTA2

$2C F0 02 DDLI Messwerte nach Wunsch EA-36

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an SG alten Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG alten Block löschen |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_N_SP_IS_WERT | real | Sollwert Leerlauf |
| STAT_RL_WERT | real | relative Last |
| STAT_BIOS_TI_0_WERT | real | EinspritzZeit Zyl.1 |
| STAT_TPS_AV_WERT | real | Position Drosselklappe |
| STAT_TPS_SP_WERT | real | Sollwert Drosselklappe |
| STAT_PV_AV_RAW_WERT | real | Fahrpedalwert |
| STAT_IGA_IGC_0_WERT | real | Zündzeitpunkt Zyl.1 |
| STAT_OZOELKM_WERT | real | km seit letztem Service |
| STAT_OZKVBSM_UL_WERT | real | Spritverbrauch seit letztem Service |

<a id="job-status-messwerte-nl"></a>
### STATUS_MESSWERTE_NL

$2C F0 02 DDLI Messwerte Klopfen nach Wunsch VS-22

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an SG alten Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG alten Block löschen |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_ANZAHL_WERTE | int | Anzahl Messwerte 0 bis 16 |
| STAT_MESSWERT0_WERT | real | Messwert (Word) |
| STAT_MESSWERT0_STRING | string | Messwert (Word) |
| STAT_MESSWERT0_TEXT | string | Messwert |
| STAT_MESSWERT0_EINH | string | Messwert |
| STAT_MESSWERT1_WERT | real | Messwert (Word) |
| STAT_MESSWERT1_STRING | string | Messwert (Word) |
| STAT_MESSWERT1_TEXT | string | Messwert |
| STAT_MESSWERT1_EINH | string | Messwert |
| STAT_MESSWERT2_WERT | real | Messwert (Word) |
| STAT_MESSWERT2_STRING | string | Messwert (Word) |
| STAT_MESSWERT2_TEXT | string | Messwert |
| STAT_MESSWERT2_EINH | string | Messwert |
| STAT_MESSWERT3_WERT | real | Messwert (Word) |
| STAT_MESSWERT3_STRING | string | Messwert (Word) |
| STAT_MESSWERT3_TEXT | string | Messwert |
| STAT_MESSWERT3_EINH | string | Messwert |
| STAT_MESSWERT4_WERT | real | Messwert (Word) |
| STAT_MESSWERT4_STRING | string | Messwert (Word) |
| STAT_MESSWERT4_TEXT | string | Messwert |
| STAT_MESSWERT4_EINH | string | Messwert |
| STAT_MESSWERT5_WERT | real | Messwert (Word) |
| STAT_MESSWERT5_STRING | string | Messwert (Word) |
| STAT_MESSWERT5_TEXT | string | Messwert |
| STAT_MESSWERT5_EINH | string | Messwert |

<a id="job-status-messwertblock-adc"></a>
### STATUS_MESSWERTBLOCK_ADC

$21 F0 DDLI Messwerteblock lesen der zuletzt mit $2C F0 definiert wurde

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_D | binary | Hex-Auftrag an SG delete |
| _TEL_AUFTRAG_W | binary | Hex-Auftrag an SG write |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_D | binary | Hex-Antwort von SG loeschen |
| _TEL_ANTWORT_W | binary | Hex-Antwort von SG schreiben |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_MESSWERT0_WERT | real | Messwert (Word) |
| STAT_MESSWERT0_TEXT | string | Messwert |
| STAT_MESSWERT0_EINH | string | Messwert |
| STAT_MESSWERT1_WERT | real | Messwert (Word) |
| STAT_MESSWERT1_TEXT | string | Messwert |
| STAT_MESSWERT1_EINH | string | Messwert |
| STAT_MESSWERT2_WERT | real | Messwert (Word) |
| STAT_MESSWERT2_TEXT | string | Messwert |
| STAT_MESSWERT2_EINH | string | Messwert |
| STAT_MESSWERT3_WERT | real | Messwert (Word) |
| STAT_MESSWERT3_TEXT | string | Messwert |
| STAT_MESSWERT3_EINH | string | Messwert |
| STAT_MESSWERT4_WERT | real | Messwert (Word) |
| STAT_MESSWERT4_TEXT | string | Messwert |
| STAT_MESSWERT4_EINH | string | Messwert |
| STAT_MESSWERT5_WERT | real | Messwert (Word) |
| STAT_MESSWERT5_TEXT | string | Messwert |
| STAT_MESSWERT5_EINH | string | Messwert |
| STAT_MESSWERT6_WERT | real | Messwert (Word) |
| STAT_MESSWERT6_TEXT | string | Messwert |
| STAT_MESSWERT6_EINH | string | Messwert |
| STAT_MESSWERT7_WERT | real | Messwert (Word) |
| STAT_MESSWERT7_TEXT | string | Messwert |
| STAT_MESSWERT7_EINH | string | Messwert |
| STAT_MESSWERT8_WERT | real | Messwert (Word) |
| STAT_MESSWERT8_TEXT | string | Messwert |
| STAT_MESSWERT8_EINH | string | Messwert |
| STAT_MESSWERT9_WERT | real | Messwert (Word) |
| STAT_MESSWERT9_TEXT | string | Messwert |
| STAT_MESSWERT9_EINH | string | Messwert |
| STAT_MESSWERTA_WERT | real | Messwert (Word) |
| STAT_MESSWERTA_TEXT | string | Messwert |
| STAT_MESSWERTA_EINH | string | Messwert |
| STAT_MESSWERTB_WERT | real | Messwert (Word) |
| STAT_MESSWERTB_TEXT | string | Messwert |
| STAT_MESSWERTB_EINH | string | Messwert |
| STAT_MESSWERTC_WERT | real | Messwert (Word) |
| STAT_MESSWERTC_TEXT | string | Messwert |
| STAT_MESSWERTC_EINH | string | Messwert |
| STAT_MESSWERTD_WERT | real | Messwert (Word) |
| STAT_MESSWERTD_TEXT | string | Messwert |
| STAT_MESSWERTD_EINH | string | Messwert |
| STAT_MESSWERTE_WERT | real | Messwert (Word) |
| STAT_MESSWERTE_TEXT | string | Messwert |
| STAT_MESSWERTE_EINH | string | Messwert |
| STAT_MESSWERTF_WERT | real | Messwert (Word) |
| STAT_MESSWERTF_TEXT | string | Messwert |
| STAT_MESSWERTF_EINH | string | Messwert |
| STAT_MESSWERT10_WERT | real | Messwert (Word) |
| STAT_MESSWERT10_TEXT | string | Messwert |
| STAT_MESSWERT10_EINH | string | Messwert |
| STAT_MESSWERT11_WERT | real | Messwert (Word) |
| STAT_MESSWERT11_TEXT | string | Messwert |
| STAT_MESSWERT11_EINH | string | Messwert |
| STAT_MESSWERT12_WERT | real | Messwert (Word) |
| STAT_MESSWERT12_TEXT | string | Messwert |
| STAT_MESSWERT12_EINH | string | Messwert |
| STAT_MESSWERT13_WERT | real | Messwert (Word) |
| STAT_MESSWERT13_TEXT | string | Messwert |
| STAT_MESSWERT13_EINH | string | Messwert |

<a id="job-ident-ibs"></a>
### IDENT_IBS

$22 40 21 BMW Nr, Seriennummer, SW/HW Index

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ID_BMW_NR | string | BMW-Teilenummer 7 stellig |
| SERIENNUMMER | unsigned long | BMW-Seriennummer |
| ZIF_PROGRAMMSTAND | int | Programm referenz |
| ZIF_STATUS | int | Programm Revision |
| HW_REF | int | Hardware Referenz |

<a id="job-status-systemcheck-pm-info-1"></a>
### STATUS_SYSTEMCHECK_PM_INFO_1

$22 40 22 Bytefeld 1 Batterie Powermanagement lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_RUHESTROMANALYSE_MODE_WERT | int | Modus der Ruhestromanalyse (1 = als Histogramm (nicht Layer), 2 = Bitcodiert für 32 Zyklen (Layer)) |
| STAT_RUHESTROMANALYSE_MODE_TEXT | string | Modus der Ruhestromanalyse (1 = als Histogramm (nicht Layer), 2 = Bitcodiert für 32 Zyklen (Layer)) |
| STAT_BATTERIELADUNG_BILANZ_WERT | real | Differenz LADUNG - ENTLADUNG in Ah 0 - 19088 |
| STAT_BATTERIELADUNG_BILANZ_EINH | string | Einheit |
| STAT_BATTERIELADUNG_GESAMT_WERT | real | Batterie Ladungen in Ah 0 - 19088 |
| STAT_BATTERIELADUNG_GESAMT_EINH | string | Einheit |
| STAT_BATTERIEENTLADUNG_GESAMT_WERT | real | Batterie Ladungen in Ah 0 - 19088 |
| STAT_BATTERIEENTLADUNG_GESAMT_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_0_20_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_0_20_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_20_40_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_20_40_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_40_60_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_40_60_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_60_80_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_60_80_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_80_100_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_80_100_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_0_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_0_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_0_20_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_0_20_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_20_40_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_20_40_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_40_60_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_40_60_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_AB_60_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_AB_60_EINH | string | Einheit |
| STAT_KM_STAND_AKTUELL_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_AKTUELL_EINH | string | Einheit |
| STAT_KM_STAND_VOR_1_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_1_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_2_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_2_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_3_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_3_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_4_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_4_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_5_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_5_TAG_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_LETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_LETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_DRITTLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_DRITTLETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_VIERTLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_VIERTLETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_FUENFTLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_FUENFTLETZTER_EINH | string | Einheit |
| STAT_BATTENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_WERT | real | 0 - 19088 Ah |
| STAT_BATTENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_EINH | string | Einheit Ah |
| STAT_RUHESTROM_AKTUELL | string |  |
| STAT_RUHESTROM_VOR_1_ZYKLUS | string |  |
| STAT_RUHESTROM_VOR_2_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_3_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_4_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_5_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_6_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_7_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_8_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_9_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_10_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_11_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_12_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_13_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_14_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_15_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_16_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_17_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_18_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_19_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_20_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_21_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_22_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_23_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_24_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_25_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_26_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_27_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_28_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_29_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_30_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_31_ZYKLEN | string |  |
| STAT_IBS_FEHLERZAEHLER_BSD_PARITY_WERT | real | Anzahl 0 - 65535 |
| STAT_IBS_FEHLERZAEHLER_BSD_PARITY_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_WATCHDOG_RESET_WERT | real | Anzahl 0 - 65535 |
| STAT_IBS_FEHLERZAEHLER_WATCHDOG_RESET_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_POWER_ON_RESET_WERT | real | Anzahl 0 - 65535 |
| STAT_IBS_FEHLERZAEHLER_POWER_ON_RESET_EINH | string | Einheit |
| STAT_KTBS_FEHLERZAEHLER_BSD_ERWEITERT_WERT | real | Anzahl 0 - 65535 |
| STAT_KTBS_FEHLERZAEHLER_BSD_ERWEITERT_EINH | string | Einheit |
| STAT_KTIBS_FEHLERZAEHLER_BSD_WERT | real | Anzahl 0 - 65535 |
| STAT_KTIBS_FEHLERZAEHLER_BSD_EINH | string | Einheit |
| STAT_KTIBS_FEHLERZAEHLER_EBSD_CHECKSUMME_WERT | real | Anzahl 0 - 65535 |
| STAT_KTIBS_FEHLERZAEHLER_EBSD_CHECKSUMME_EINH | string | Einheit |

<a id="job-status-systemcheck-pm-info-2"></a>
### STATUS_SYSTEMCHECK_PM_INFO_2

$22 40 23 Bytefeld 2 Batterie Powermanagement lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_BATTERIE_KAPAZITAET_WERT | real | Batterie Kapazitaet in Ah 0 - 255 |
| STAT_BATTERIE_KAPAZITAET_EINH | string | Einheit |
| STAT_SOH_WERT | real | Bereich -50% - 49,6% |
| STAT_SOH_EINH | string | Einheit |
| STAT_SOC_FIT_WERT | real | Bereich 0-100% |
| STAT_SOC_FIT_EINH | string | Einheit |
| STAT_TEMP_SAISON_WERT | real | Bereich -128C - 127C |
| STAT_TEMP_SAISON_EINH | string | Einheit C |
| STAT_KALIBRIER_EVENT_CNT_WERT | real | Kalibrieranzahl 0 - 255 |
| STAT_KALIBRIER_EVENT_CNT_EINH | string | Einheit |
| STAT_Q_SOC_AKTUELL_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_AKTUELL_EINH | string | Einheit |
| STAT_Q_SOC_VOR_1_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_1_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_2_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_2_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_3_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_3_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_4_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_4_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_5_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_5_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_AKTUELL_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_AKTUELL_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_DOWNLOAD_CHECKSUMME_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_DOWNLOAD_CHECKSUMME_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_EEPROM_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_EEPROM_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_RAM_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_RAM_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_PROM_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_PROM_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_I2C_NAC_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_I2C_NAC_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_I2C_BUS_COLLISION_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_I2C_BUS_COLLISION_EINH | string | Einheit |

<a id="job-steuern-pm-histogram-reset"></a>
### STEUERN_PM_HISTOGRAM_RESET

$30 F5 04 Loeschen von pminfo1 index 23-30

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adap-selektiv-loeschen"></a>
### ADAP_SELEKTIV_LOESCHEN

Löschen von Adaptionen und gelernte Varianten KWP 2000 $31 30 xx xx xx Loeschen der Adaptionswerte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE_1 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_2 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_3 | int | Bit=1 löscht Bit=0 behält alten Wert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-batterietausch-registrieren"></a>
### STEUERN_BATTERIETAUSCH_REGISTRIEREN

KWP 2000 $31 30 00 10 00 Bit setzen Batterietausch registrieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-pm-messemode"></a>
### START_SYSTEMCHECK_PM_MESSEMODE

$31 F6 Systemdiagnose BatterieSensor reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-pm-messemode"></a>
### STOP_SYSTEMCHECK_PM_MESSEMODE

$32 F6 Systemdiagnose BatterieSensor reset beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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

<a id="job-innentemp-lesen"></a>
### INNENTEMP_LESEN

0x301001     Steuergeraete-Innentemperatur auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_TSG_WERT | real | ADC-Wert Steuergeraete-Innentemperatur V_TECU |
| STAT_ADC_TSG_EINH | string | V |
| SG_INNENTEMP_WERT | real | Temperatur Steuergeraete-Innentemperatur TECU |
| SG_INNENTEMP_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-agk"></a>
### STATUS_AGK

0x30C101     Abgasklappe auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_AGK | unsigned long | Status Abgasklappe LV_EF |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

0x300A01     Ansauglufttemperatur 1 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_TANS1_WERT | real | ADC-Wert Ansauglufttemperatur 1 V_TIA |
| STAT_ADC_TANS1_EINH | string | V |
| STAT_AN_LUFTTEMPERATUR_WERT | real | Temperatur Ansauglufttemperatur 1 TIA_MES |
| STAT_AN_LUFTTEMPERATUR_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-anws"></a>
### STATUS_ANWS

0x30EE01     Vanos Auslass Ventil auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ANWS_WERT | real | Status Vanos_A Ventil IVVTPWM_1 |
| STAT_STAT_ANWS_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-anwsf"></a>
### STATUS_ANWSF

0x30A201     Ventil Vanos Auslass Frueh auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ANWSF_WERT | real | Status Ventil Vanos Auslass Frueh 1BYTE in 0 bis 100 Prozent |
| STAT_STAT_ANWSF_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-anwss"></a>
### STATUS_ANWSS

0x30A301     Ventil Vanos Auslass Spaet auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ANWSS_WERT | real | Status Ventil Vanos Auslass Spaet 1BYTE in 0 bis 100 Prozent |
| STAT_STAT_ANWSS_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-avs"></a>
### STATUS_AVS

0x30C001     Absperrventil Saugstrahlpumpe auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_AVS_WERT | real | Status Absperrventil Saugstrahlpumpe 1BYTE in 0 bis 100 Prozent |
| STAT_STAT_AVS_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bls"></a>
### STATUS_BLS

0x300201     Bremslichtschalter auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_BLS | unsigned long | Status Bremslichtschalter LV_IM_BLS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-blts"></a>
### STATUS_BLTS

0x300301     Bremslichttestschalter auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_BLTS | unsigned long | Status Bremslichttestschalter LV_IM_BTS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-co-abgleich"></a>
### STATUS_CO_ABGLEICH

0x225FF1     Abgleichwert CO (Kohlenmonoxid) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LV_FAC_MFF_ADD_EXT_ADJ_NVMY | unsigned long | Logical value for storing CO correction in NVMY LV_FAC_MFF_ADD_EXT_ADJ_NVMY |
| STAT_LV_RST_MFF_ADD_EXT_ADJ_NVMY | unsigned long | Flag to reset external MFF correction to 0 LV_RST_MFF_ADD_EXT_ADJ_NVMY |
| STAT_CO_ABGLEICH_WERT | real | Status Abgleichwert CO (Kohlenmonoxid) FAC_MFF_ADD_EXT_ADJ |
| STAT_CO_ABGLEICH_EINH | string | percent |
| STAT_MFF_ADD_EXT_ADJ_1_WERT | real | Mass fuel flow for CO adjustment at idling, value for injection correction MFF_ADD_EXT_ADJ[1] |
| STAT_MFF_ADD_EXT_ADJ_1_EINH | string | mgperstk |
| STAT_MFF_ADD_EXT_ADJ_2_WERT | real | Mass fuel flow for CO adjustment at idling, value for injection correction MFF_ADD_EXT_ADJ[2] |
| STAT_MFF_ADD_EXT_ADJ_2_EINH | string | mgperstk |
| STAT_MFF_ADD_EXT_ADJ_NVMY_WERT | real | Mass fuel flow for CO adjustment at idling, value for storing in NVMY MFF_ADD_EXT_ADJ_NVMY |
| STAT_MFF_ADD_EXT_ADJ_NVMY_EINH | string | mgperstk |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-igr"></a>
### STATUS_CODIERUNG_IGR

0x223210     Codierung fuer IGR (Intelligente Generator-Regelung) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_IGR | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-kat"></a>
### STATUS_CODIERUNG_KAT

0x223001     Codierung fuer Katalysator auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_KAT | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-mil"></a>
### STATUS_CODIERUNG_MIL

0x223000     Codierung fuer MIL (Malfunction Indication Lamp) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_MIL | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-oel"></a>
### STATUS_CODIERUNG_OEL

0x223200     Codierung fuer Oelwechselintervall auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_OEL_1 | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |
| STAT_CODIERUNG_OEL_2 | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-vmax"></a>
### STATUS_CODIERUNG_VMAX

0x223010     Codierung fuer maximale Geschwindigkeit auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_VMAX | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-xenon"></a>
### STATUS_CODIERUNG_XENON

0x223211     Codierung fuer Xenon-Lichtverbau auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_XENON | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dfv1a"></a>
### STATUS_DFV1A

0x3328     Auslesen Diagnosefunktion Auslass A-Vanostest 1 (Verstellzeit)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFV1A | unsigned long | FUNKTIONSSTATUS DFV1A 1BYTE in 0 bis 255 |
| STAT_AVANOS_VERSTELLZEIT_FRUEH_WERT | unsigned long | Ergebnis Verstellzeitmessung (A2L-Name: Vsa_verstellzt_frueh) VSA_VERSTELLZT_FRUEH |
| STAT_AVANOS_VERSTELLZEIT_FRUEH_EINH | string | ms |
| STAT_AVANOS_VERSTELLZEIT_SPAET_WERT | unsigned long | Ergebnis Verstellzeitmessung (A2L-Name: Vsa_verstellzt_spaet) VSA_VERSTELLZT_SPAET |
| STAT_AVANOS_VERSTELLZEIT_SPAET_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dfv1e"></a>
### STATUS_DFV1E

0x3323     Auslesen Diagnosefunktion Einlass E-Vanostest 1 (Verstellzeit)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFV1E | unsigned long | FUNKTIONSSTATUS DFV1E 1BYTE in 0 bis 255 |
| STAT_EVANOS_VERSTELLZEIT_FRUEH_WERT | unsigned long | Ergebnis Verstellzeitmessung (A2L-Name: Vse_verstellzt_frueh) VSE_VERSTELLZT_FRUEH |
| STAT_EVANOS_VERSTELLZEIT_FRUEH_EINH | string | ms |
| STAT_EVANOS_VERSTELLZEIT_SPAET_WERT | unsigned long | Ergebnis Verstellzeitmessung (A2L-Name: Vse_verstellzt_spaet) VSE_VERSTELLZT_SPAET |
| STAT_EVANOS_VERSTELLZEIT_SPAET_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dfv2a"></a>
### STATUS_DFV2A

0x3329     Auslesen Diagnosefunktion Auslass A-Vanostest 2 (Dichtigkeit)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFV2A | unsigned long | FUNKTIONSSTATUS DFV2A 1BYTE in 0 bis 255 |
| STAT_AVANOS_ISTWERT_WERT | real | Istwert Auslassspreizung variable NWS (A2L-Name: Vsa_spri) VSA_SPRI |
| STAT_AVANOS_ISTWERT_EINH | string | degree_KW |
| STAT_AVANOS_SOLLWERT_WERT | real | Sollwert Auslassspreizung variable NWS (A2L-Name: Vsa_sprs) VSA_SPRS |
| STAT_AVANOS_SOLLWERT_EINH | string | degree_KW |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dfv2e"></a>
### STATUS_DFV2E

0x3324     Auslesen Diagnosefunktion Einlass E-Vanostest 2 (Dichtigkeit)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFV2E | unsigned long | FUNKTIONSSTATUS DFV2E 1BYTE in 0 bis 255 |
| STAT_EVANOS_ISTWERT_WERT | real | Istwert Einlassspreizung variable NWS (A2L-Name: Vse_spri) VSE_SPRI |
| STAT_EVANOS_ISTWERT_EINH | string | degree_KW |
| STAT_EVANOS_SOLLWERT_WERT | real | Sollwert Einlassspreizung variable NWS (A2L-Name: Vse_sprs) VSE_SPRS |
| STAT_EVANOS_SOLLWERT_EINH | string | degree_KW |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dfvfa"></a>
### STATUS_DFVFA

0x33D3     Auslesen Diagnosefunktion Auslass A-Vanostest Fruehanschlag

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFVFA | unsigned long | FUNKTIONSSTATUS DFVFA 1BYTE in 0 bis 255 |
| STAT_AVANOS_ISTWERT_WERT | real | Istwert Auslassspreizung variable NWS (A2L-Name: Vsa_spri) VSA_SPRI |
| STAT_AVANOS_ISTWERT_EINH | string | degree_KW |
| STAT_AVANOS_SOLLWERT_WERT | real | Sollwert Auslassspreizung variable NWS (A2L-Name: Vsa_sprs) VSA_SPRS |
| STAT_AVANOS_SOLLWERT_EINH | string | degree_KW |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dfvfe"></a>
### STATUS_DFVFE

0x33D1     Auslesen Diagnosefunktion Einlass E-Vanostest Fruehanschlag

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFVFE | unsigned long | FUNKTIONSSTATUS DFVFE 1BYTE in 0 bis 255 |
| STAT_EVANOS_ISTWERT_WERT | real | Istwert Einlassspreizung variable NWS (A2L-Name: Vse_spri) VSE_SPRI |
| STAT_EVANOS_ISTWERT_EINH | string | degree_KW |
| STAT_EVANOS_SOLLWERT_WERT | real | Sollwert Einlassspreizung variable NWS (A2L-Name: Vse_sprs) VSE_SPRS |
| STAT_EVANOS_SOLLWERT_EINH | string | degree_KW |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dfvsa"></a>
### STATUS_DFVSA

0x33D4     Auslesen Diagnosefunktion Auslass A-Vanostest Spaetanschlag

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFVSA | unsigned long | FUNKTIONSSTATUS DFVSA 1BYTE in 0 bis 255 |
| STAT_AVANOS_ISTWERT_WERT | real | Istwert Auslassspreizung variable NWS (A2L-Name: Vsa_spri) VSA_SPRI |
| STAT_AVANOS_ISTWERT_EINH | string | degree_KW |
| STAT_AVANOS_SOLLWERT_WERT | real | Sollwert Auslassspreizung variable NWS (A2L-Name: Vsa_sprs) VSA_SPRS |
| STAT_AVANOS_SOLLWERT_EINH | string | degree_KW |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dfvse"></a>
### STATUS_DFVSE

0x33D2     Auslesen Diagnosefunktion Einlass E-Vanostest Spaetanschlag

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFVSE | unsigned long | FUNKTIONSSTATUS DFVSE 1BYTE in 0 bis 255 |
| STAT_EVANOS_ISTWERT_WERT | real | Istwert Einlassspreizung variable NWS (A2L-Name: Vse_spri) VSE_SPRI |
| STAT_EVANOS_ISTWERT_EINH | string | degree_KW |
| STAT_EVANOS_SOLLWERT_WERT | real | Sollwert Einlassspreizung variable NWS (A2L-Name: Vse_sprs) VSE_SPRS |
| STAT_EVANOS_SOLLWERT_EINH | string | degree_KW |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dkp-volt"></a>
### STATUS_DKP_VOLT

0x302A01     Drosselklappe auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DKP_VOLT_WERT | real | ADC-Wert1 Drosselklappe V_TPS_1 |
| STAT_DKP_VOLT_EINH | string | V |
| STAT_ADC2_DK_WERT | real | ADC-Wert2 Drosselklappe V_TPS_2 |
| STAT_ADC2_DK_EINH | string | V |
| STAT_STAT_DK_WERT | real | Status Drosselklappe TPS_AV |
| STAT_STAT_DK_EINH | string | degreeTPS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dmtl-heizung"></a>
### STATUS_DMTL_HEIZUNG

0x30CE01     Diagnosemodul-Tank Leckage Heizung auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_DMTLH | unsigned long | Status Diagnosemodul-Tank Leckage Heizung LV_HDMTL_ON |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dmtl-p"></a>
### STATUS_DMTL_P

0x30CC01     Diagnosemodul-Tank Leckage Pumpe auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_DMTL_P | unsigned long | Status Diagnosemodul-Tank Leckage Pumpe LV_DMTL_PUMP |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dmtl-v"></a>
### STATUS_DMTL_V

0x30CD01     Diagnosemodul-Tank Leckage Ventil auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_DMTL_V | unsigned long | Status Diagnosemodul-Tank Leckage Ventil LV_DMTLS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-e-luefter"></a>
### STATUS_E_LUEFTER

0x30DA01     E-Luefter auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ELUE_WERT | real | Status E-Luefter ECFPWM[0] |
| STAT_STAT_ELUE_EINH | string | percent |
| STAT_PHY_TCO_WERT | real | Kuehlmitteltemperatur (Dieser Wert wurde zusaetzlich zum geforderten Umfang eingefuegt) TCO |
| STAT_PHY_TCO_EINH | string | degreeC |
| STAT_PHY_TCO_2_WERT | real | Kuehlmitteltemperatur am Kuehlerausgang (Dieser Wert wurde zusaetzlich zum geforderten Umfang eingefuegt) TCO_2 |
| STAT_PHY_TCO_2_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ebl"></a>
### STATUS_EBL

0x30C801     E-Box-Luefter auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_EBL | unsigned long | Status E-Box-Luefter LV_EBOX_CFA |
| STAT_PHY_TECU_WERT | real | Steuergeraetetemperatur DME (Dieser Wert wurde zusaetzlich zum geforderten Umfang eingefuegt) TECU |
| STAT_PHY_TECU_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eisygd"></a>
### STATUS_EISYGD

0x33E1     Auslesen Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_EISYGD_TEXT | string | Adaption Massenstromregler auf DK erstmalig erfolgt 1BYTE EISY-Adaption abgelaufen |
| STAT_FS_EISYGD_WERT | int |  |
| STAT_MRNN_TEST_DK_WERT | real | Massenstromregler-Adaptionswert NN im GD - Betrieb ueber Test gelesen MRNN_TEST_DK |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eisyugd"></a>
### STATUS_EISYUGD

0x33E0     Auslesen Eisy-Adaptionswerte (ungedrosselt) (Anforderung aus CP5403)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_EISYUGD_TEXT | string | Adaption Massenstromregler auf Hub erstmalig erfolgt 1BYTE EISY-Adaption abgelaufen |
| STAT_FS_EISYUGD_WERT | int |  |
| STAT_MRNN_TEST_VVT_WERT | real | Massenstromregler-Adaptionswert NN im VVT Betrieb ueber Test gelesen MRNN_TEST_VVT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ekp"></a>
### STATUS_EKP

0x30D801     Elektrische Kraftstoffpumpe 1 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_EKP1_WERT | real | Status Elektrische Kraftstoffpumpe 1 EFPPWM |
| STAT_STAT_EKP1_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eml"></a>
### STATUS_EML

0x30D601     EML (Engine Malfunction Lamp) auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_EML | unsigned long | Status EML (Engine Malfunction Lamp) LV_WAL_1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-energiesparmode"></a>
### STATUS_ENERGIESPARMODE

0x22100A     Status Energiesparmode START-8B

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENERGIESPARMODE_TEXT | string | Status Energiesparmode  01= Fertigung, 02= Transport, 03= Werkstatt STATE_EGY_MIN_KWP |
| STAT_ENERGIESPARMODE_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-enws"></a>
### STATUS_ENWS

0x30ED01     Vanos Einlass Ventil auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ENWS_WERT | real | Status Vanos_E Ventil IVVTPWM_0 |
| STAT_STAT_ENWS_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-enwsf"></a>
### STATUS_ENWSF

0x30A001     Ventil Vanos Einlass Frueh auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ENWSF_WERT | real | Status Ventil Vanos Einlass Frueh 1BYTE in 0 bis 100 Prozent |
| STAT_STAT_ENWSF_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-enwss"></a>
### STATUS_ENWSS

0x30A101     Ventil Vanos Einlass Spaet auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ENWSS_WERT | real | Status Ventil Vanos Einlass Spaet 1BYTE in 0 bis 100 Prozent |
| STAT_STAT_ENWSS_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ev1"></a>
### STATUS_EV1

0x30E101     Einspritzventil 1 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_EV1_WERT | real | Einspritzzeit Einspritzventil 1 ti_1_0 |
| STAT_PHY_EV1_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ev2"></a>
### STATUS_EV2

0x30E201     Einspritzventil 2 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_EV2_WERT | real | Einspritzzeit Einspritzventil 2 ti_1_4 |
| STAT_PHY_EV2_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ev3"></a>
### STATUS_EV3

0x30E301     Einspritzventil 3 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_EV3_WERT | real | Einspritzzeit Einspritzventil 3 ti_1_2 |
| STAT_PHY_EV3_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ev4"></a>
### STATUS_EV4

0x30E401     Einspritzventil 4 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_EV4_WERT | real | Einspritzzeit Einspritzventil 4 ti_1_5 |
| STAT_PHY_EV4_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ev5"></a>
### STATUS_EV5

0x30E501     Einspritzventil 5 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_EV5_WERT | real | Einspritzzeit Einspritzventil 5 ti_1_1 |
| STAT_PHY_EV5_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ev6"></a>
### STATUS_EV6

0x30E601     Einspritzventil 6 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_EV6_WERT | real | Einspritzzeit Einspritzventil 6 ti_1_3 |
| STAT_PHY_EV6_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ewap"></a>
### STATUS_EWAP

0x30BF01     elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_EWAP_WERT | real | Status elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) (Ausnahme fuer Rueckwaertskompatibilitaet SGBD MSV70) 1BYTE in 0 bis 100 Prozent |
| STAT_STAT_EWAP_EINH | string | percent |
| STAT_PHY_TCO_WERT | real | Kuehlmitteltemperatur (Dieser Wert wurde zusaetzlich zum geforderten Umfang eingefuegt) TCO |
| STAT_PHY_TCO_EINH | string | degreeC |
| STAT_PHY_TCO_2_WERT | real | Coolant temperature (radiator outlet) (A2L-Name: tco_2) TCO_2 |
| STAT_PHY_TCO_2_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fgrl"></a>
### STATUS_FGRL

0x30D501     Fahrgeschwindigkeitsregler-Lampe auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_FGRL | unsigned long | Status Fahrgeschwindigkeitsregler-Lampe LV_CRU_MAIN_SWI |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fwv1"></a>
### STATUS_FWV1

0x301E01     Fahrerwunschversorgung 1 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_FWV1_WERT | real | ADC-Wert Fahrerwunschversorgung 1 VCC_PVS_1 |
| STAT_ADC_FWV1_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fwv2"></a>
### STATUS_FWV2

0x301F01     Fahrerwunschversorgung 2 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_FWV2_WERT | real | ADC-Wert Fahrerwunschversorgung 2 VCC_PVS_2 |
| STAT_ADC_FWV2_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-glf"></a>
### STATUS_GLF

0x30C301     Gesteuerte Luftfuehrung auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_GLF | unsigned long | Status Gesteuerte Luftfuehrung LV_ECRAS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hfms"></a>
### STATUS_HFMS

0x302E01     Sekundaerluft HFM (Heissfilm Luftmassenmesser) auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_HFMS_WERT | real | ADC-Wert Sekundaerluft HFM (Heissfilm Luftmassenmesser) V_SAF |
| STAT_ADC_HFMS_EINH | string | V |
| STAT_PHY_HFMS_WERT | real | Luftmasse Sekundaerluft HFM (Heissfilm Luftmassenmesser) SAF_KGH_MES_BAS |
| STAT_PHY_HFMS_EINH | string | kgperh |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kb1"></a>
### STATUS_KB1

0x303001     Klopfbaustein 1 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_KB1_WERT | real | ADC-Wert Klopfbaustein 1 KNKS[0] |
| STAT_ADC_KB1_EINH | string | V |
| STAT_STAT_KB1_WERT | real | Status Klopfbaustein 1 KNKS_REL_NL_0 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kb2"></a>
### STATUS_KB2

0x303101     Klopfbaustein 2 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_KB2_WERT | real | ADC-Wert Klopfbaustein 2 KNKS[5] |
| STAT_ADC_KB2_EINH | string | V |
| STAT_STAT_KB2_WERT | real | Status Klopfbaustein 2 KNKS_REL_NL_5 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kft"></a>
### STATUS_KFT

0x30C901     Kennfeldthermostat auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_KFT_WERT | real | Status Kennfeldthermostat ECTPWM |
| STAT_STAT_KFT_EINH | string | percent |
| STAT_PHY_TCO_WERT | real | Kuehlmitteltemperatur (Dieser Wert wurde zusaetzlich zum geforderten Umfang eingefuegt) TCO |
| STAT_PHY_TCO_EINH | string | degreeC |
| STAT_PHY_TCO_2_WERT | real | Kuehlmitteltemperatur am Kuehlerausgang (Dieser Wert wurde zusaetzlich zum geforderten Umfang eingefuegt) TCO_2 |
| STAT_PHY_TCO_2_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kgeh"></a>
### STATUS_KGEH

0x30AD01     Kurbelgehaeuseentlueftungsheizung auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_KGEH | unsigned long | Status Kurbelgehaeuseentlueftungsheizung LV_RLY_CRCV_HEAT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-korel"></a>
### STATUS_KOREL

0x30C701     Klimakompressor-Relais auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_KOREL | unsigned long | Status Klimakompressor-Relais LV_ACCOUT_RLY |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-krann"></a>
### STATUS_KRANN

0x33E3     Auslesen Krann-Adaptionswerte (Anforderung aus CP5404)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KRNN_TEST_WERT | real | Zuendwinkelaenderung aus Adaption Klopfregelung fuer Testerabfrage KRNN_TEST |
| STAT_KRNN_TEST_EINH | string | degree |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kup"></a>
### STATUS_KUP

0x300401     Kupplungsschalter auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_KUP | unsigned long | Status Kupplungsschalter LV_CS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde"></a>
### STATUS_L_SONDE

0x302101     Lambdasonde vor Kat Bank1 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_SONDE_WERT | real | ADC-Wert Lambdasonde vor Kat Bank1 VLS_UP[1] |
| STAT_L_SONDE_EINH | string | V |
| STAT_PHY_LSVK1_WERT | real | Lambdawert Lambdasonde vor Kat Bank1 LAMB_LS_UP[1] |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde-2"></a>
### STATUS_L_SONDE_2

0x302301     Lambdasonde vor Kat Bank2 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_SONDE_2_WERT | real | ADC-Wert Lambdasonde vor Kat Bank2 VLS_UP[2] |
| STAT_L_SONDE_2_EINH | string | V |
| STAT_PHY_LSVK2_WERT | real | Lambdawert Lambdasonde vor Kat Bank2 LAMB_LS_UP[2] |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde-2-h"></a>
### STATUS_L_SONDE_2_H

0x302401     Lambdasonde hinter Kat Bank2 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_SONDE_2_H_WERT | real | ADC-Wert Lambdasonde hinter Kat Bank2 VLS_DOWN[2] |
| STAT_L_SONDE_2_H_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde-h"></a>
### STATUS_L_SONDE_H

0x302201     Lambdasonde hinter Kat Bank1 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_SONDE_H_WERT | real | ADC-Wert Lambdasonde hinter Kat Bank1 VLS_DOWN[1] |
| STAT_L_SONDE_H_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lls"></a>
### STATUS_LLS

0x309F01     Leerlaufsteller auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_LLS_WERT | real | Status Leerlaufsteller 1BYTE in 0 bis 100 Prozent |
| STAT_STAT_LLS_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

0x302501     Luftmassenmesser 1 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_LMM1_WERT | real | ADC-Wert Luftmassenmesser 1 V_MAF |
| STAT_ADC_LMM1_EINH | string | V |
| STAT_LMM_MASSE_WERT | real | Durchsatz Luftmassenmesser 1 MAF_KGH_MES_BAS |
| STAT_LMM_MASSE_EINH | string | kgperh |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lrp"></a>
### STATUS_LRP

0x225FF7     Laufruhepruefung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ZUENDWINKELEINGRIFF_AKTIV | unsigned long | Zuendwinkeleingriff (1= deaktiviert  0=aktiviert) 1BYTE IDENTICAL HEX |
| STAT_STAT_GEMISCHEINGRIFF_AKTIV | unsigned long | Gemischeingriff (1= deaktiviert  0=aktiviert) 1BYTE IDENTICAL HEX |
| STAT_STAT_HUBEINGRIFF_AKTIV | unsigned long | zylinderselektiver Hubeingriff (1= deaktiviert  0=aktiviert) 1BYTE IDENTICAL HEX |
| STAT_STAT_MINHUBEINGRIFF_AKTIV | unsigned long | Minhubeingriff (1= deaktiviert  0=aktiviert) 1BYTE IDENTICAL HEX |
| STAT_STAT_ZUENDWINKELEINGRIFF_FREIGEGEBEN | unsigned long | Zuendwinkeleingriff (1= freigegeben  0=nicht freigegeben) 1BYTE IDENTICAL HEX |
| STAT_STAT_GEMISCHEINGRIFF_FREIGEGEBEN | unsigned long | Gemischeingriff (1= freigegeben  0=nicht freigegeben) 1BYTE IDENTICAL HEX |
| STAT_STAT_HUBEINGRIFF_FREIGEGEBEN | unsigned long | zylinderselektiver Hubeingriff (1= freigegeben  0=nicht freigegeben) 1BYTE IDENTICAL HEX |
| STAT_STAT_MINHUBEINGRIFF_FREIGEGEBEN | unsigned long | Minhubeingriff (1= freigegeben  0=nicht freigegeben) 1BYTE IDENTICAL HEX |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lsh1"></a>
### STATUS_LSH1

0x30D001     Lambdasondenheizung vor Kat Bank1 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_LSH1_WERT | real | Status Lambdasondenheizung vor Kat Bank1 LSHPWM_UP[1] |
| STAT_STAT_LSH1_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lsh2"></a>
### STATUS_LSH2

0x30D101     Lambdasondenheizung hinter Kat Bank1 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_LSH2_WERT | real | Status Lambdasondenheizung hinter Kat Bank1 LSHPWM_DOWN[1] |
| STAT_STAT_LSH2_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lsh3"></a>
### STATUS_LSH3

0x30D201     Lambdasondenheizung vor Kat Bank2 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_LSH3_WERT | real | Status Lambdasondenheizung vor Kat Bank2 LSHPWM_UP[2] |
| STAT_STAT_LSH3_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lsh4"></a>
### STATUS_LSH4

0x30D301     Lambdasondenheizung hinter Kat Bank2 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_LSH4_WERT | real | Status Lambdasondenheizung hinter Kat Bank2 LSHPWM_DOWN[2] |
| STAT_STAT_LSH4_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-lrp"></a>
### STATUS_MESSWERTE_LRP

0x22402D     Messwerte Laufruhepruefung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ST_VBRVS_AUS | unsigned long | Statuswort Verbrennungsregelung fuer Service (A2L-Name: St_vbrvs_aus) ST_VBRVS_AUS |
| STAT_ST_VBRVS_EIN | unsigned long | Statuswort Verbrennungsregelung vom Tester (A2L-Name: St_vbrvs_ein) ST_VBRVS_EIN |
| STAT_AMO_05_WERT | real | Gesamte DFT 0,5 Motorordnung (A2L-Name: Amo_05) AMO_05 |
| STAT_AMO_10_WERT | real | Gesamte DFT 1,0 Motorordnung (A2L-Name: Amo_10) AMO_10 |
| STAT_AMO_15_WERT | real | Gesamte DFT 1,5 Motorordnung (A2L-Name: Amo_15) AMO_15 |
| STAT_AMO_20_WERT | real | Gesamte DFT 2,0 Motorordnung (A2L-Name: Amo_20) AMO_20 |
| STAT_EXWINKKOR_WERT | real | Korrekturwinkel Excenterwelle zur Hubkorrektur (A2L-Name: Exwinkkor) EXWINKKOR |
| STAT_EXWINKKOR_EINH | string | degree |
| STAT_ZYLHUBKOR | unsigned long | Fuer Hubkorrektur ausgewaehlter Zylinder (A2L-Name: Zylhubkor) ZYLHUBKOR |
| STAT_MINHUB_WERT | real | Tatsaechlich wirksamer Minhub (nach Ein-/Ausblendungsfakoren) (A2L-Name: Minhub) MINHUB |
| STAT_MINHUB_EINH | string | mm |
| STAT_F_MINHUB_WERT | real | Faktor Ein-/Ausblendung Minhub ueber Tmot und Nkw (A2L-Name: F_minhub) F_MINHUB |
| STAT_MINHUB_ROH_WERT | real | Minhubrohwert aus Adaption (A2L-Name: Minhub_roh) MINHUB_ROH |
| STAT_MINHUB_ROH_EINH | string | mm |
| STAT_MINHUBVS_WERT | real | Vorgabe Minhub ueber Tester (A2L-Name: Minhubvs) MINHUBVS |
| STAT_MINHUBVS_EINH | string | mm |
| STAT_MINHUBVS_IST_WERT | real | Tatsaechlich wirksamer Minhub aus Verstelleingriff (vor Ein-/Ausblendungsfaktoren) (A2L-Name: Minhubvs_ist) MINHUBVS_IST |
| STAT_MINHUBVS_IST_EINH | string | mm |
| STAT_MINHUBVSNV_WERT | real | dauerhaft fest programmierter Minhub (A2L-Name: Minhubvsnv) MINHUBVSNV |
| STAT_MINHUBVSNV_EINH | string | mm |
| STAT_S_VSMNHB | unsigned long | Schalter fuer Testereingriff (A2L-Name: S_vsmnhb) S_VSMNHB |
| STAT_S_VSMNHBNV | unsigned long | Schalter fuer Testereingriff (A2L-Name: S_vsmnhbnv) S_VSMNHBNV |
| STAT_F_TIKORRVR_0_WERT | real | Zylinderselektive Gemischkorrektur (A2L-Name: F_tikorrvr) F_TIKORRVR_[0] |
| STAT_LURABS_F_0_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (A2L-Name: Lurabs_f) LURABS_F_[0] |
| STAT_LURDIF_F_0_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[0] |
| STAT_ZW_OFFKORRVR_0_WERT | real | Zuendwinkeloffset fuer Verbrennungsregelung (A2L-Name: Zw_offkorrvr) ZW_OFFKORRVR_[0] |
| STAT_ZW_OFFKORRVR_0_EINH | string | degree |
| STAT_F_TIKORRVR_1_WERT | real | Zylinderselektive Gemischkorrektur (A2L-Name: F_tikorrvr) F_TIKORRVR_[1] |
| STAT_LURABS_F_1_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (A2L-Name: Lurabs_f) LURABS_F_[1] |
| STAT_LURDIF_F_1_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[1] |
| STAT_ZW_OFFKORRVR_1_WERT | real | Zuendwinkeloffset fuer Verbrennungsregelung (A2L-Name: Zw_offkorrvr) ZW_OFFKORRVR_[1] |
| STAT_ZW_OFFKORRVR_1_EINH | string | degree |
| STAT_F_TIKORRVR_2_WERT | real | Zylinderselektive Gemischkorrektur (A2L-Name: F_tikorrvr) F_TIKORRVR_[2] |
| STAT_LURABS_F_2_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (A2L-Name: Lurabs_f) LURABS_F_[2] |
| STAT_LURDIF_F_2_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[2] |
| STAT_ZW_OFFKORRVR_2_WERT | real | Zuendwinkeloffset fuer Verbrennungsregelung (A2L-Name: Zw_offkorrvr) ZW_OFFKORRVR_[2] |
| STAT_ZW_OFFKORRVR_2_EINH | string | degree |
| STAT_F_TIKORRVR_3_WERT | real | Zylinderselektive Gemischkorrektur (A2L-Name: F_tikorrvr) F_TIKORRVR_[3] |
| STAT_LURABS_F_3_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (A2L-Name: Lurabs_f) LURABS_F_[3] |
| STAT_LURDIF_F_3_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[3] |
| STAT_ZW_OFFKORRVR_3_WERT | real | Zuendwinkeloffset fuer Verbrennungsregelung (A2L-Name: Zw_offkorrvr) ZW_OFFKORRVR_[3] |
| STAT_ZW_OFFKORRVR_3_EINH | string | degree |
| STAT_F_TIKORRVR_4_WERT | real | Zylinderselektive Gemischkorrektur (A2L-Name: F_tikorrvr) F_TIKORRVR_[4] |
| STAT_LURABS_F_4_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (A2L-Name: Lurabs_f) LURABS_F_[4] |
| STAT_LURDIF_F_4_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[4] |
| STAT_ZW_OFFKORRVR_4_WERT | real | Zuendwinkeloffset fuer Verbrennungsregelung (A2L-Name: Zw_offkorrvr) ZW_OFFKORRVR_[4] |
| STAT_ZW_OFFKORRVR_4_EINH | string | degree |
| STAT_F_TIKORRVR_5_WERT | real | Zylinderselektive Gemischkorrektur (A2L-Name: F_tikorrvr) F_TIKORRVR_[5] |
| STAT_LURABS_F_5_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (A2L-Name: Lurabs_f) LURABS_F_[5] |
| STAT_LURDIF_F_5_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[5] |
| STAT_ZW_OFFKORRVR_5_WERT | real | Zuendwinkeloffset fuer Verbrennungsregelung (A2L-Name: Zw_offkorrvr) ZW_OFFKORRVR_[5] |
| STAT_ZW_OFFKORRVR_5_EINH | string | degree |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mil"></a>
### STATUS_MIL

0x30D401     MIL (Malfunction Indicator Lamp) auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_MIL | unsigned long | Status MIL (Malfunction Indicator Lamp) LV_MIL |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

0x300C01     Motortemperatur auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_TMOT_WERT | real | ADC-Wert Motortemperatur V_TCO |
| STAT_ADC_TMOT_EINH | string | V |
| STAT_MOTORTEMPERATUR_WERT | real | Temperatur Motortemperatur TCO_MES |
| STAT_MOTORTEMPERATUR_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ods"></a>
### STATUS_ODS

0x300501     Oeldruckschalter auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ODS | unsigned long | Status Oeldruckschalter LV_POIL_SWI |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-oel"></a>
### STATUS_OEL

0x300E01     Oelsensor auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_TOEL_WERT | real | Oeltemperatur TOEL |
| STAT_PHY_TOEL_EINH | string | degreeC |
| STAT_PHY_NIVOEL_WERT | real | Oelniveau OZ_NIVAKT |
| STAT_PHY_QOEL_WERT | real | Oelqualitaet OZ_PERMAKT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pwg-poti-spannung"></a>
### STATUS_PWG_POTI_SPANNUNG

0x302801     Fahrerwunsch 1 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PWG_POTI_SPANNUNG_1_WERT | real | ADC-Wert Fahrerwunsch 1 V_PVS_1 |
| STAT_PWG_POTI_SPANNUNG_1_EINH | string | V |
| STAT_STAT_PWG1_WERT | real | Status Fahrerwunsch 1 PV_AV_1 |
| STAT_STAT_PWG1_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pwg2"></a>
### STATUS_PWG2

0x302901     Fahrerwunsch 2 auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_PWG2_WERT | real | ADC-Wert Fahrerwunsch 2 V_PVS_2 |
| STAT_ADC_PWG2_EINH | string | V |
| STAT_STAT_PWG2_WERT | real | Status Fahrerwunsch 2 PV_AV_2 |
| STAT_STAT_PWG2_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbmmode9"></a>
### STATUS_RBMMODE9

0x224026     Rate Based Monitoring Mode 9 auslesen (Ausgabe der Werte wie im Scantool Mode 9)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OBDCOND | unsigned long | OBD Monitoring Conditions Encountered Counts (general denominator) CTR_CDN_OBD_RBM |
| STAT_IGNCNTR | unsigned long | Ignition Counter CTR_IGK_CYC_RBM |
| STAT_CATCOMP1 | unsigned long | Catalyst Monitor Completion Counts Bank 1 (Numerator) CTR_COMP_RBM_CAT_DIAG_1 |
| STAT_CATCOND1 | unsigned long | Catalyst Monitor Conditions Encountered Counts Bank 1 (Denominator) CTR_CDN_RBM_CAT_DIAG_1 |
| STAT_CATCOMP2 | unsigned long | Catalyst Monitor Completion Counts Bank 2 (Numerator) CTR_COMP_RBM_CAT_DIAG_2 |
| STAT_CATCOND2 | unsigned long | Catalyst Monitor Conditions Encountered Counts Bank 2 (Denominator) CTR_CDN_RBM_CAT_DIAG_2 |
| STAT_O2SCOMP1 | unsigned long | O2 Sensor Monitor Completion Counts Bank 1 (Numerator) 2BYTE in 0 bis 65534 |
| STAT_O2SCOND1 | unsigned long | O2 Sensor Monitor Conditions Encountered Counts Bank 1 (Denominator) 2BYTE in 0 bis 65534 |
| STAT_O2SCOMP2 | unsigned long | O2 Sensor Monitor Completion Counts Bank 2 (Numerator) 2BYTE in 0 bis 65534 |
| STAT_O2SCOND2 | unsigned long | O2 Sensor Monitor Conditions Encountered Counts Bank 2 (Denominator) 2BYTE in 0 bis 65534 |
| STAT_EGRCOMP | unsigned long | EGR Monitor Completion Condition Counts (Numerator) 2BYTE in 0 bis 65534 |
| STAT_EGRCOND | unsigned long | EGR Monitor Conditions Encountered Counts (Denominator) 2BYTE in 0 bis 65534 |
| STAT_AIRCOMP1 | unsigned long | AIR Monitor Completion Condition Counts Bank 1 (Secondary Air) (Numerator) 2BYTE in 0 bis 65534 |
| STAT_AIRCOND1 | unsigned long | AIR Monitor Conditions Encountered Counts Bank 1 (Secondary Air) (Denominator) 2BYTE in 0 bis 65534 |
| STAT_AIRCOMP2 | unsigned long | AIR Monitor Completion Condition Counts Bank 2 (Secondary Air) (Numerator) 2BYTE in 0 bis 65534 |
| STAT_AIRCOND2 | unsigned long | AIR Monitor Conditions Encountered Counts Bank 2 (Secondary Air) (Denominator) 2BYTE in 0 bis 65534 |
| STAT_EVAPCOMP | unsigned long | EVAP Monitor Completion Condition Counts (Numerator) 2BYTE in 0 bis 65534 |
| STAT_EVAPCOND | unsigned long | EVAP Monitor Conditions Encountered Counts (Denominator) 2BYTE in 0 bis 65534 |
| STAT_VVTCOMP1 | unsigned long | Variable Valve Timing (VANOS) Monitor Completion Condition Counts Bank 1 (Numerator) 2BYTE in 0 bis 65534 |
| STAT_VVTCOND1 | unsigned long | Variable Valve Timing (VANOS) Monitor Conditions Encountered Counts Bank 1 (Denominator) 2BYTE in 0 bis 65534 |
| STAT_VVTCOMP2 | unsigned long | Variable Valve Timing (VANOS) Monitor Completion Condition Counts Bank 2 (Numerator) 2BYTE in 0 bis 65534 |
| STAT_VVTCOND2 | unsigned long | Variable Valve Timing (VANOS) Monitor Conditions Encountered Counts Bank 2 (Denominator) 2BYTE in 0 bis 65534 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbmms1"></a>
### STATUS_RBMMS1

0x224027     Rate Based Monitoring Motorsteuerung MS... Block 1 auslesen (Vorhalt)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CTR_COMP_RBM_CAT_DIAG_1 | unsigned long | Diagnose Katalysator Sauerstoffspeicherfaehigkeit Bank 1 (Numerator) CTR_COMP_RBM_CAT_DIAG_1 |
| STAT_CTR_CDN_RBM_CAT_DIAG_1 | unsigned long | Diagnose Katalysator Sauerstoffspeicherfaehigkeit Bank 1 (Denominator) CTR_CDN_RBM_CAT_DIAG_1 |
| STAT_CTR_COMP_RBM_CAT_DIAG_2 | unsigned long | Diagnose Katalysator Sauerstoffspeicherfaehigkeit Bank 2 (Numerator) CTR_COMP_RBM_CAT_DIAG_2 |
| STAT_CTR_CDN_RBM_CAT_DIAG_2 | unsigned long | Diagnose Katalysator Sauerstoffspeicherfaehigkeit Bank 2 (Denominator) CTR_CDN_RBM_CAT_DIAG_2 |
| STAT_CTR_COMP_RBM_DYN_VLD_LS_UP_1 | unsigned long | Diagnose Dynamikpruefung lineare Lamdasonden Bank 1 (Numerator) CTR_COMP_RBM_DYN_VLD_LS_UP_1 |
| STAT_CTR_CDN_RBM_DYN_VLD_LS_UP_1 | unsigned long | Diagnose Dynamikpruefung lineare Lamdasonden Bank 1 (Denominator) CTR_CDN_RBM_DYN_VLD_LS_UP_1 |
| STAT_CTR_COMP_RBM_DYN_VLD_LS_UP_2 | unsigned long | Diagnose Dynamikpruefung lineare Lamdasonden Bank 2 (Numerator) CTR_COMP_RBM_DYN_VLD_LS_UP_2 |
| STAT_CTR_CDN_RBM_DYN_VLD_LS_UP_2 | unsigned long | Diagnose Dynamikpruefung lineare Lamdasonden Bank 2 (Denominator) CTR_CDN_RBM_DYN_VLD_LS_UP_2 |
| STAT_CTR_COMP_RBM_SHIFT_AFL_LSL_UP_1 | unsigned long | Diagnose Lamdasondensignalverschiebung mager Bank 1 (Numerator) CTR_COMP_RBM_SHIFT_AFL_LSL_UP_1 |
| STAT_CTR_CDN_RBM_SHIFT_AFL_LSL_UP_1 | unsigned long | Diagnose Lamdasondensignalverschiebung mager Bank 1 (Denominator) CTR_CDN_RBM_SHIFT_AFL_LSL_UP_1 |
| STAT_CTR_COMP_RBM_SHIFT_AFL_LSL_UP_2 | unsigned long | Diagnose Lamdasondensignalverschiebung mager Bank 2 (Numerator) CTR_COMP_RBM_SHIFT_AFL_LSL_UP_2 |
| STAT_CTR_CDN_RBM_SHIFT_AFL_LSL_UP_2 | unsigned long | Diagnose Lamdasondensignalverschiebung mager Bank 2 (Denominator) CTR_CDN_RBM_SHIFT_AFL_LSL_UP_2 |
| STAT_CTR_COMP_RBM_SHIFT_AFR_LSL_UP_1 | unsigned long | Diagnose Lamdasondensignalverschiebung fett Bank 1 (Numerator) CTR_COMP_RBM_SHIFT_AFR_LSL_UP_1 |
| STAT_CTR_CDN_RBM_SHIFT_AFR_LSL_UP_1 | unsigned long | Diagnose Lamdasondensignalverschiebung fett Bank 1 (Denominator) CTR_CDN_RBM_SHIFT_AFR_LSL_UP_1 |
| STAT_CTR_COMP_RBM_SHIFT_AFR_LSL_UP_2 | unsigned long | Diagnose Lamdasondensignalverschiebung fett Bank 2 (Numerator) CTR_COMP_RBM_SHIFT_AFR_LSL_UP_2 |
| STAT_CTR_CDN_RBM_SHIFT_AFR_LSL_UP_2 | unsigned long | Diagnose Lamdasondensignalverschiebung fett Bank 2 (Denominator) CTR_CDN_RBM_SHIFT_AFR_LSL_UP_2 |
| STAT_CTR_COMP_RBM_AIR_LSL_UP_1 | unsigned long | Diagnose lineare Lamdasonde korrekt verbaut Bank 1 (Numerator) CTR_COMP_RBM_AIR_LSL_UP_1 |
| STAT_CTR_CDN_RBM_AIR_LSL_UP_1 | unsigned long | Diagnose lineare Lamdasonde korrekt verbaut Bank 1 (Denominator) CTR_CDN_RBM_AIR_LSL_UP_1 |
| STAT_CTR_COMP_RBM_AIR_LSL_UP_2 | unsigned long | Diagnose lineare Lamdasonde korrekt verbaut Bank 2 (Numerator) CTR_COMP_RBM_AIR_LSL_UP_2 |
| STAT_CTR_CDN_RBM_AIR_LSL_UP_2 | unsigned long | Diagnose lineare Lamdasonde korrekt verbaut Bank 2 (Denominator) CTR_CDN_RBM_AIR_LSL_UP_2 |
| STAT_CTR_COMP_RBM_DIAGCPS | unsigned long | Diagnose Tankentlueftungssystem (Numerator) CTR_COMP_RBM_DIAGCPS |
| STAT_CTR_CDN_RBM_DIAGCPS | unsigned long | Diagnose Tankentlueftungssystem (Denominator) CTR_CDN_RBM_DIAGCPS |
| STAT_CTR_COMP_RBM_SMALL_LEAK | unsigned long | Diagnose Tankfeinleckpruefung (DMTL) (Numerator) CTR_COMP_RBM_SMALL_LEAK |
| STAT_CTR_CDN_RBM_SMALL_LEAK | unsigned long | Diagnose Tankfeinleckpruefung (DMTL) (Denominator) CTR_CDN_RBM_SMALL_LEAK |
| STAT_CTR_COMP_RBM_ROUGH_LEAK | unsigned long | Diagnose Tankgrobleckpruefung (DMTL) (Numerator) CTR_COMP_RBM_ROUGH_LEAK |
| STAT_CTR_CDN_RBM_ROUGH_LEAK | unsigned long | Diagnose Tankgrobleckpruefung (DMTL) (Denominator) CTR_CDN_RBM_ROUGH_LEAK |
| STAT_CTR_COMP_RBM_DMTLM | unsigned long | Diagnosemodul Tankleckage (DMTL) (Numerator) CTR_COMP_RBM_DMTLM |
| STAT_CTR_CDN_RBM_DMTLM | unsigned long | Diagnosemodul Tankleckage (DMTL) (Denominator) CTR_CDN_RBM_DMTLM |
| STAT_CTR_COMP_RBM_REF_CRK_CAM_IN_1 | unsigned long | Diagnose Veraenderung der Steuerzeiten Nockenwelleneinlass (Numerator) CTR_COMP_RBM_REF_CRK_CAM_IN_1 |
| STAT_CTR_CDN_RBM_REF_CRK_CAM_IN_1 | unsigned long | Diagnose Veraenderung der Steuerzeiten Nockenwelleneinlass (Denominator) CTR_CDN_RBM_REF_CRK_CAM_IN_1 |
| STAT_CTR_COMP_RBM_REF_CRK_CAM_EX_1 | unsigned long | Diagnose Veraenderung der Steuerzeiten Nockenwellenauslass (Numerator) CTR_COMP_RBM_REF_CRK_CAM_EX_1 |
| STAT_CTR_CDN_RBM_REF_CRK_CAM_EX_1 | unsigned long | Diagnose Veraenderung der Steuerzeiten Nockenwellenauslass (Denominator) CTR_CDN_RBM_REF_CRK_CAM_EX_1 |
| STAT_CTR_COMP_RBM_MEC_IVVT_IN | unsigned long | Diagnose mechanische Schwergaengigkeit VANOS (Einlass) (Numerator) CTR_COMP_RBM_MEC_IVVT_IN |
| STAT_CTR_CDN_RBM_MEC_IVVT_IN | unsigned long | Diagnose mechanische Schwergaengigkeit VANOS (Einlass) (Denominator) CTR_CDN_RBM_MEC_IVVT_IN |
| STAT_CTR_COMP_RBM_MEC_IVVT_EX | unsigned long | Diagnose mechanische Schwergaengigkeit VANOS (Auslass) (Numerator) CTR_COMP_RBM_MEC_IVVT_EX |
| STAT_CTR_CDN_RBM_MEC_IVVT_EX | unsigned long | Diagnose mechanische Schwergaengigkeit VANOS (Auslass) (Denominator) CTR_CDN_RBM_MEC_IVVT_EX |
| STAT_CTR_COMP_RBM_SA_SYS | unsigned long | Diagnose Sekundaerluftsystem (Numerator) CTR_COMP_RBM_SA_SYS |
| STAT_CTR_CDN_RBM_SA_SYS | unsigned long | Diagnose Sekundaerluftsystem (Denominator) CTR_CDN_RBM_SA_SYS |
| STAT_CTR_COMP_RBM_SA_SAFM | unsigned long | Diagnose Sekundaerluftsystem Heissfilmluftmassenmesser (Mini-HFM) (Numerator) CTR_COMP_RBM_SA_SAFM |
| STAT_CTR_CDN_RBM_SA_SAFM | unsigned long | Diagnose Sekundaerluftsystem Heissfilmluftmassenmesser (Mini-HFM) (Denominator) CTR_CDN_RBM_SA_SAFM |
| STAT_CTR_COMP_RBM_SA_SAV | unsigned long | Diagnose Sekundaerluftventil (Numerator) CTR_COMP_RBM_SA_SAV |
| STAT_CTR_CDN_RBM_SA_SAV | unsigned long | Diagnose Sekundaerluftventil (Denominator) CTR_CDN_RBM_SA_SAV |
| STAT_CTR_COMP_RBM_SA_SAP | unsigned long | Diagnose Sekundaerluftpumpe (Numerator) CTR_COMP_RBM_SA_SAP |
| STAT_CTR_CDN_RBM_SA_SAP | unsigned long | Diagnose Sekundaerluftpumpe (Denominator) CTR_CDN_RBM_SA_SAP |
| STAT_CTR_COMP_RBM_SA_SAV_LSL | unsigned long | Diagnose Sekundaerluftsystem durch Signalaenderung Lambdasonde vor Katalysator Bank 1 und 2 (Numerator) CTR_COMP_RBM_SA_SAV_LSL |
| STAT_CTR_CDN_RBM_SA_SAV_LSL | unsigned long | Diagnose Sekundaerluftsystem durch Signalaenderung Lambdasonde vor Katalysator Bank 1 und 2 (Denominator) CTR_CDN_RBM_SA_SAV_LSL |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbmms2"></a>
### STATUS_RBMMS2

0x224028     Rate Based Monitoring Motorsteuerung MS... Block 2 auslesen (Vorhalt)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CTR_COMP_RBM_TH | unsigned long | Diagnose Thermostat (Numerator) CTR_COMP_RBM_TH |
| STAT_CTR_CDN_RBM_TH | unsigned long | Diagnose Thermostat (Denominator) CTR_CDN_RBM_TH |
| STAT_CTR_COMP_RBM_TCO_PLAUS | unsigned long | Diagnose Motortemperatur Plausibilitaet (Numerator) CTR_COMP_RBM_TCO_PLAUS |
| STAT_CTR_CDN_RBM_TCO_PLAUS | unsigned long | Diagnose Motortemperatur Plausibilitaet (Denominator) CTR_CDN_RBM_TCO_PLAUS |
| STAT_CTR_COMP_RBM_TCO_STUCK | unsigned long | Diagnose Motortemperatur haengendes Sensorsignal (Numerator) CTR_COMP_RBM_TCO_STUCK |
| STAT_CTR_CDN_RBM_TCO_STUCK | unsigned long | Diagnose Motortemperatur haengendes Sensorsignal (Denominator) CTR_CDN_RBM_TCO_STUCK |
| STAT_CTR_COMP_RBM_TCO_2_PLAUS | unsigned long | Diagnose Kuehlerauslasstemperatur Plausibilitaet (Numerator) CTR_COMP_RBM_TCO_2_PLAUS |
| STAT_CTR_CDN_RBM_TCO_2_PLAUS | unsigned long | Diagnose Kuehlerauslasstemperatur Plausibilitaet (Denominator) CTR_CDN_RBM_TCO_2_PLAUS |
| STAT_CTR_COMP_RBM_TAM_PLAUS | unsigned long | Diagnose Umgebungstemperatur Plausibilitaet (Numerator) CTR_COMP_RBM_TAM_PLAUS |
| STAT_CTR_CDN_RBM_TAM_PLAUS | unsigned long | Diagnose Umgebungstemperatur Plausibilitaet (Denominator) CTR_CDN_RBM_TAM_PLAUS |
| STAT_CTR_COMP_RBM_VS_PLAUS | unsigned long | Diagnose Geschwindigkeit Plausibilitaet (Numerator) CTR_COMP_RBM_VS_PLAUS |
| STAT_CTR_CDN_RBM_VS_PLAUS | unsigned long | Diagnose Geschwindigkeit Plausibilitaet (Denominator) CTR_CDN_RBM_VS_PLAUS |
| STAT_CTR_COMP_RBM_FTL_OBD | unsigned long | Diagnose Tankfuellstand (Numerator) CTR_COMP_RBM_FTL_OBD |
| STAT_CTR_CDN_RBM_FTL_OBD | unsigned long | Diagnose Tankfuellstand (Denominator) CTR_CDN_RBM_FTL_OBD |
| STAT_CTR_COMP_RBM_OBD_LSH_DOWN_1 | unsigned long | Diagnose Lamdasondenheizung nach Katalysator Bank 1 (Numerator) CTR_COMP_RBM_OBD_LSH_DOWN_1 |
| STAT_CTR_CDN_RBM_OBD_LSH_DOWN_1 | unsigned long | Diagnose Lamdasondenheizung nach Katalysator Bank 1 (Denominator) CTR_CDN_RBM_OBD_LSH_DOWN_1 |
| STAT_CTR_COMP_RBM_OBD_LSH_DOWN_2 | unsigned long | Diagnose Lamdasondenheizung nach Katalysator Bank 2 (Numerator) CTR_COMP_RBM_OBD_LSH_DOWN_2 |
| STAT_CTR_CDN_RBM_OBD_LSH_DOWN_2 | unsigned long | Diagnose Lamdasondenheizung nach Katalysator Bank 2 (Denominator) CTR_CDN_RBM_OBD_LSH_DOWN_2 |
| STAT_CTR_COMP_RBM_OBD_VLD_LSH_UP_1 | unsigned long | Diagnose Alterung lineare Lamdasonde Bank 1 (Numerator) CTR_COMP_RBM_OBD_VLD_LSH_UP_1 |
| STAT_CTR_CDN_RBM_OBD_VLD_LSH_UP_1 | unsigned long | Diagnose Alterung lineare Lamdasonde Bank 1 (Denominator) CTR_CDN_RBM_OBD_VLD_LSH_UP_1 |
| STAT_CTR_COMP_RBM_OBD_VLD_LSH_UP_2 | unsigned long | Diagnose Alterung lineare Lamdasonde Bank 2 (Numerator) CTR_COMP_RBM_OBD_VLD_LSH_UP_2 |
| STAT_CTR_CDN_RBM_OBD_VLD_LSH_UP_2 | unsigned long | Diagnose Alterung lineare Lamdasonde Bank 2 (Denominator) CTR_CDN_RBM_OBD_VLD_LSH_UP_2 |
| STAT_CTR_COMP_RBM_CS | unsigned long | Diagnose Kupplungsschalter (Numerator) CTR_COMP_RBM_CS |
| STAT_CTR_CDN_RBM_CS | unsigned long | Diagnose Kupplungsschalter (Denominator) CTR_CDN_RBM_CS |
| STAT_CTR_COMP_RBM_ISC | unsigned long | Diagnose Leerlaufregler (Numerator) CTR_COMP_RBM_ISC |
| STAT_CTR_CDN_RBM_ISC | unsigned long | Diagnose Leerlaufregler (Denominator) CTR_CDN_RBM_ISC |
| STAT_CTR_COMP_RBM_MAF | unsigned long | Diagnose Luftmassenmesser (Numerator) CTR_COMP_RBM_MAF |
| STAT_CTR_CDN_RBM_MAF | unsigned long | Diagnose Luftmassenmesser (Denominator) CTR_CDN_RBM_MAF |
| STAT_CTR_COMP_RBM_TIA_PLAUS | unsigned long | Diagnose Ansauglufttemperatur Plausibilitaet (Numerator) CTR_COMP_RBM_TIA_PLAUS |
| STAT_CTR_CDN_RBM_TIA_PLAUS | unsigned long | Diagnose Ansauglufttemperatur Plausibilitaet (Denominator) CTR_CDN_RBM_TIA_PLAUS |
| STAT_CTR_COMP_RBM_AMP_PLAUS | unsigned long | Diagnose Umgebungsdruck Plausibilitaet (Numerator) CTR_COMP_RBM_AMP_PLAUS |
| STAT_CTR_CND_RBM_AMP_PLAUS | unsigned long | Diagnose Umgebungsdruck Plausibilitaet (Denominator) CTR_CDN_RBM_AMP_PLAUS |
| STAT_CTR_COMP_RBM_LOAD_TPS_PLAUS | unsigned long | Diagnose Plausibilitaet Drosselklappeposition zu Signal Luftmassenmesser (Numerator) CTR_COMP_RBM_LOAD_TPS_PLAUS |
| STAT_CTR_CDN_RBM_LOAD_TPS_PLAUS | unsigned long | Diagnose Plausibilitaet Drosselklappeposition zu Signal Luftmassenmesser (Denominator) CTR_CDN_RBM_LOAD_TPS_PLAUS |
| STAT_CTR_COMP_RBM_MAP_DIP_PLAUS | unsigned long | Diagnose Differenzdrucksensor Sauganlage zu Umgebung Plausibilitaet (Numerator) CTR_COMP_RBM_MAP_DIP_PLAUS |
| STAT_CTR_CDN_RBM_MAP_DIP_PLAUS | unsigned long | Diagnose Differenzdrucksensor Sauganlage zu Umgebung Plausibilitaet (Denominator) CTR_CDN_RBM_MAP_DIP_PLAUS |
| STAT_CTR_COMP_RBM_VLS_DOWN_DIF_1 | unsigned long | Diagnose Abweichung Lambdaregelung Bank 1 (Numerator) CTR_COMP_RBM_VLS_DOWN_DIF_1 |
| STAT_CTR_CDN_RBM_VLS_DOWN_DIF_1 | unsigned long | Diagnose Abweichung Lambdaregelung Bank 1 (Denominator) CTR_CDN_RBM_VLS_DOWN_DIF_1 |
| STAT_CTR_COMP_RBM_VLS_DOWN_DIF_2 | unsigned long | Diagnose Abweichung Lambdaregelung Bank 2 (Numerator) CTR_COMP_RBM_VLS_DOWN_DIF_2 |
| STAT_CTR_CDN_RBM_VLS_DOWN_DIF_2 | unsigned long | Diagnose Abweichung Lambdaregelung Bank 2 (Denominator) CTR_CDN_RBM_VLS_DOWN_DIF_2 |
| STAT_CTR_COMP_RBM_CHK_LS_DOWN_1 | unsigned long | Diagnose binaere Lamdasonde nach Katalysator Bank 1 (Numerator) CTR_COMP_RBM_CHK_LS_DOWN_1 |
| STAT_CTR_CDN_RBM_CHK_LS_DOWN_1 | unsigned long | Diagnose binaere Lamdasonde nach Katalysator Bank 1 (Denominator) CTR_CDN_RBM_CHK_LS_DOWN_1 |
| STAT_CTR_COMP_RBM_CHK_LS_DOWN_2 | unsigned long | Diagnose binaere Lamdasonde nach Katalysator Bank 2 (Numerator) CTR_COMP_RBM_CHK_LS_DOWN_2 |
| STAT_CTR_CDN_RBM_CHK_LS_DOWN_2 | unsigned long | Diagnose binaere Lamdasonde nach Katalysator Bank 2 (Denominator) CTR_CDN_RBM_CHK_LS_DOWN_2 |
| STAT_CTR_COMP_RBM_SWT_LS_DOWN_1 | unsigned long | Diagnose Schaltzeit binaere Lamdasonde Bank 1 (Numerator) CTR_COMP_RBM_SWT_LS_DOWN_1 |
| STAT_CTR_CDN_RBM_SWT_LS_DOWN_1 | unsigned long | Diagnose Schaltzeit binaere Lamdasonde Bank 1 (Denominator) CTR_CDN_RBM_SWT_LS_DOWN_1 |
| STAT_CTR_COMP_RBM_SWT_LS_DOWN_2 | unsigned long | Diagnose Schaltzeit binaere Lamdasonde Bank 2 (Numerator) CTR_COMP_RBM_SWT_LS_DOWN_2 |
| STAT_CTR_CDN_RBM_SWT_LS_DOWN_2 | unsigned long | Diagnose Schaltzeit binaere Lamdasonde Bank 2 (Denominator) CTR_CDN_RBM_SWT_LS_DOWN_2 |
| STAT_CTR_COMP_RBM_T_ES | unsigned long | Diagnose Abstellzeit (Numerator) CTR_COMP_RBM_T_ES |
| STAT_CTR_CDN_RBM_T_ES | unsigned long | Diagnose Abstellzeit (Denominator) CTR_CDN_RBM_T_ES |
| STAT_CTR_COMP_RBM_TPS | unsigned long | Diagnose Drosselklappenlagesensoren (Numerator) CTR_COMP_RBM_TPS |
| STAT_CTR_CDN_RBM_TPS | unsigned long | Diagnose Drosselklappenlagesensoren (Denominator) CTR_CDN_RBM_TPS |
| STAT_CTR_COMP_RBM_ANG_INST_AD_VVL | unsigned long | Diagnose Adaption Excenterwellensensor (Numerator) CTR_COMP_RBM_ANG_INST_AD_VVL |
| STAT_CTR_CDN_RBM_ANG_INST_AD_VVL | unsigned long | Diagnose Adaption Excenterwellensensor (Denominator) CTR_CDN_RBM_ANG_INST_AD_VVL |
| STAT_CTR_COMP_RBM_ANG_CHK_MAX_VVL | unsigned long | Diagnose maximaler Hub VVT (Numerator) CTR_COMP_RBM_ANG_CHK_MAX_VVL |
| STAT_CTR_CDN_RBM_ANG_CHK_MAX_VVL | unsigned long | Diagnose maximaler Hub VVT (Denominator) CTR_CDN_RBM_ANG_CHK_MAX_VVL |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-slp"></a>
### STATUS_SLP

0x30CB01     Sekundaerluftpumpe auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_SLP | unsigned long | Status Sekundaerluftpumpe LV_SAP |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sok"></a>
### STATUS_SOK

0x30C201     Soundklappe auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_SOK | unsigned long | Status Soundklappe LV_SOF |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spt"></a>
### STATUS_SPT

0x300601     Sporttaster auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_SPT_WERT | real | ADC-Wert Sporttaster V_SOF_SWI |
| STAT_ADC_SPT_EINH | string | V |
| STAT_STAT_SPT | unsigned long | Status Sporttaster LV_SOF_SWI |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sr"></a>
### STATUS_SR

0x30C401     Startrelais auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_SR | unsigned long | Status Startrelais LV_RLY_ST |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tev"></a>
### STATUS_TEV

0x30CF01     Tankentlueftungsventil auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_TEV_WERT | real | Status Tankentlueftungsventil CPPWM_CPS |
| STAT_STAT_TEV_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tka"></a>
### STATUS_TKA

0x300D01     Kuehlerauslasstemperatur auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_TKA_WERT | real | ADC-Wert Kuehlerauslasstemperatur V_TCO_2 |
| STAT_ADC_TKA_EINH | string | V |
| STAT_PHY_TKA_WERT | real | Temperatur Kuehlerauslasstemperatur TCO_2_MES |
| STAT_PHY_TKA_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ttemp"></a>
### STATUS_TTEMP

0x302F01     Taster Tempomat auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_TTEMP_TEXT | string | BITFELD Taster Tempomat STATE_MSW_CAN |
| STAT_STAT_TTEMP_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ubat"></a>
### STATUS_UBAT

0x302701     Batteriesensor auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_UBAT_WERT | real | ADC-Wert Batteriesensor VB_BAS |
| STAT_ADC_UBAT_EINH | string | V |
| STAT_PHY_UBAT_WERT | real | Spannung Batteriesensor U_BATT |
| STAT_PHY_UBAT_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

0x301C01     Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_UVSG_WERT | real | ADC-Wert Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) VB_BAS |
| STAT_ADC_UVSG_EINH | string | V |
| STAT_UBATT_WERT | real | Spannung Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) VB |
| STAT_UBATT_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-udf"></a>
### STATUS_UDF

0x301701     Umgebungsdruck auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_UDF_WERT | real | ADC-Wert Umgebungsdruck V_AMP |
| STAT_ADC_UDF_EINH | string | V |
| STAT_PHY_UDF_WERT | real | Druck Umgebungsdruck AMP_MES |
| STAT_PHY_UDF_EINH | string | hPa |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ugen"></a>
### STATUS_UGEN

0x303201     Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_UGEN_WERT | real | Spannung Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) V_ALTER_SP |
| STAT_PHY_UGEN_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ukl15"></a>
### STATUS_UKL15

0x301B01     Kl.15 Spannung auslesen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_UKL15_WERT | real | ADC-Wert Kl.15 Spannung V_IGK_BAS |
| STAT_ADC_UKL15_EINH | string | V |
| STAT_PHY_UKL15_WERT | real | Spannung Kl.15 Spannung V_IGK_MES |
| STAT_PHY_UKL15_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-agk"></a>
### STEUERN_AGK

0x30C107     Abgasklappe ansteuern NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_AGK_WERT | unsigned long | Sollwert LV_ACT_EF_EXT_ADJ |
| SW_TO_AGK_WERT | unsigned long | Timeout 0 bis 508s 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-anws"></a>
### STEUERN_ANWS

0x30EE07     Vanos Auslass Ventil ansteuern CON_N_MIN nur bei erhoeter Motordrehzahl

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ANWS_WERT | real | Sollwert Vanos_A Ventil CAM_SP_EX_EXT_ADJ |
| SW_TO_ANWS_WERT | unsigned long | Timeout Vanos_A Ventil 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-anwsf"></a>
### STEUERN_ANWSF

0x30A207     Ventil Vanos Auslass Frueh ansteuern CON_N_MIN nur bei erhoeter Motordrehzahl

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ANWSF_WERT | unsigned long | Tastverhaeltniss Ventil Vanos Auslass Frueh 2BYTE_in_0_65534ms |
| SW_TO_ANWSF_WERT | unsigned long | Timeout Ventil Vanos Auslass Frueh 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-anwsr"></a>
### STEUERN_ANWSR

0x2E5FFA07     Anschlagsadaption Auslass Vanos ruecksetzen vorgeben  ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden.  N_LL nur bei Leerlauf-Drehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-anwss"></a>
### STEUERN_ANWSS

0x30A307     Ventil Vanos Auslass Spaet ansteuern CON_N_MIN nur bei erhoeter Motordrehzahl

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ANWSS_WERT | unsigned long | Tastverhaeltniss Ventil Vanos Auslass Spaet 2BYTE_in_0_65534ms |
| SW_TO_ANWSS_WERT | unsigned long | Timeout Ventil Vanos Auslass Spaet 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-avs"></a>
### STEUERN_AVS

0x30C007     Absperrventil Saugstrahlpumpe ansteuern V_EQ_ZERO nur bei Fahrzeuggeschwindigkeit v=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_AVS_WERT | unsigned long | Tastverhaeltniss Absperrventil Saugstrahlpumpe LV_BSUP_EXT_ADJ |
| SW_TO_AVS_WERT | unsigned long | Timeout Absperrventil Saugstrahlpumpe 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-co-abgleich-programmieren"></a>
### STEUERN_CO_ABGLEICH_PROGRAMMIEREN

0x2E5FF108     Abgleichwert CO (Kohlenmonoxid) programmieren NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-co-abgleich-reset"></a>
### STEUERN_CO_ABGLEICH_RESET

0x2E5FF104     Abgleichwert CO (Kohlenmonoxid) loeschen NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-co-abgleich-verstellen"></a>
### STEUERN_CO_ABGLEICH_VERSTELLEN

0x2E5FF107     Abgleichwert CO (Kohlenmonoxid) vorgeben NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CO_ABGLEICH_WERT | real | Abgleichwert CO (Kohlenmonoxid) FAC_MFF_ADD_EXT_ADJ |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-igr"></a>
### STEUERN_CODIERUNG_IGR

0x2E3210     Codierung fuer IGR (Intelligente Generator-Regelung) vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_IGR_WERT | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-kat"></a>
### STEUERN_CODIERUNG_KAT

0x2E3001     Codierung fuer Katalysator vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_KAT_WERT | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-mil"></a>
### STEUERN_CODIERUNG_MIL

0x2E3000     Codierung fuer MIL (Malfunction Indication Lamp) vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_MIL_WERT | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-oel"></a>
### STEUERN_CODIERUNG_OEL

0x2E3200     Codierung fuer Oelwechselintervall vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_OEL_1_WERT | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |
| STAT_CODIERUNG_OEL_2_WERT | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-vmax"></a>
### STEUERN_CODIERUNG_VMAX

0x2E3010     Codierung fuer maximale Geschwindigkeit vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_VMAX_WERT | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-xenon"></a>
### STEUERN_CODIERUNG_XENON

0x2E3211     Codierung fuer Xenon-Lichtverbau vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_XENON_WERT | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dfv1a"></a>
### STEUERN_DFV1A

0x3128     Ansteuern Diagnosefunktion Auslass A-Vanostest 1 (Verstellzeit)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dfv1e"></a>
### STEUERN_DFV1E

0x3123     Ansteuern Diagnosefunktion Einlass E-Vanostest 1 (Verstellzeit)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dfv2a"></a>
### STEUERN_DFV2A

0x3129     Ansteuern Diagnosefunktion Auslass A-Vanostest 2 (Dichtigkeit)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dfv2e"></a>
### STEUERN_DFV2E

0x3124     Ansteuern Diagnosefunktion Einlass E-Vanostest 2 (Dichtigkeit)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dfvfa"></a>
### STEUERN_DFVFA

0x31D3     Ansteuern Diagnosefunktion Auslass A-Vanostest Fruehanschlag

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dfvfe"></a>
### STEUERN_DFVFE

0x31D1     Ansteuern Diagnosefunktion Einlass E-Vanostest Fruehanschlag

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dfvsa"></a>
### STEUERN_DFVSA

0x31D4     Ansteuern Diagnosefunktion Auslass A-Vanostest Spaetanschlag

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dfvse"></a>
### STEUERN_DFVSE

0x31D2     Ansteuern Diagnosefunktion Einlass E-Vanostest Spaetanschlag

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dk"></a>
### STEUERN_DK

0x302A07     Drosselklappe ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DK_WERT | real | Sollwert Drosselklappe TPS_SP_EXT_ADJ |
| SW_TO_DK_WERT | unsigned long | Timeout Drosselklappe 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-heizung"></a>
### STEUERN_DMTL_HEIZUNG

0x30CE07     Diagnosemodul-Tank Leckage Heizung ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTLH_WERT | unsigned long | Sollwert Diagnosemodul-Tank Leckage Heizung LV_ACT_DMTLH_EXT_ADJ |
| SW_TO_DMTLH_WERT | unsigned long | Timeout Diagnosemodul-Tank Leckage Heizung 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-p"></a>
### STEUERN_DMTL_P

0x30CC07     Diagnosemodul-Tank Leckage Pumpe ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTL_P_WERT | unsigned long | Sollwert Diagnosemodul-Tank Leckage Pumpe LV_ACT_DMTL_PUMP_EXT_ADJ |
| SW_TO_DMTL_P_WERT | unsigned long | Timeout Diagnosemodul-Tank Leckage Pumpe 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-v"></a>
### STEUERN_DMTL_V

0x30CD07     Diagnosemodul-Tank Leckage Ventil ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTL_V_WERT | unsigned long | Sollwert Diagnosemodul-Tank Leckage Ventil LV_ACT_DMTLS_EXT_ADJ |
| SW_TO_DMTL_V_WERT | unsigned long | Timeout Diagnosemodul-Tank Leckage Ventil 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

0x30DA07     E-Luefter ansteuern CON_ELUE nur bei Motortemperatur TMOT kleiner 115gradCelsius

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ELUE_WERT | real | Tastverhaeltniss E-Luefter ECFPWM_ECF_EXT_ADJ |
| SW_TO_ELUE_WERT | unsigned long | Timeout E-Luefter 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ebl"></a>
### STEUERN_EBL

0x30C807     E-Box-Luefter ansteuern NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EBL_WERT | unsigned long | Sollwert E-Box-Luefter LV_ACT_EBOX_CFA_EXT_ADJ |
| SW_TO_EBL_WERT | unsigned long | Timeout E-Box-Luefter 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eisygd"></a>
### STEUERN_EISYGD

0x31E1     Ansteuern Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_WERT | long | Drehzahl NKW_SOLL |
| VSE_SPRI_WERT | real | Istwert Einlassspreizung variable NWS VSE_SPRI |
| VSA_SPRI_WERT | real | Istwert Auslassspreizung variable NWS VSA_SPRI |
| WDK_IST_WERT | real | Aktueller Drosselklappenwinkel WDK_IST |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eisyugd"></a>
### STEUERN_EISYUGD

0x31E0     Ansteuern Eisy-Adaptionswerte (ungedrosselt) (Anforderung aus CP5403)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_WERT | long | Drehzahl NKW_SOLL |
| VSE_SPRI_WERT | real | Istwert Einlassspreizung variable NWS VSE_SPRI |
| VSA_SPRI_WERT | real | Istwert Auslassspreizung variable NWS VSA_SPRI |
| HUBEV_IST_WERT | real | Istwert Einlassventilhub HUBEV_IST |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

0x30D807     Elektrische Kraftstoffpumpe 1 ansteuern     Elektrische Kraftstoffpumpe 1 Deaktivierung aufheben N_EQ_ZERO nur bei Motordrehzahl n=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EKP1_WERT | unsigned long | Sollwert Elektrische Kraftstoffpumpe 1  (Ausnahme fuer Rueckwaertskompatibilitaet SGBD MSV70) 1BYTE 0x00-0xFF in 0 oder 1 |
| SW_TO_EKP1_WERT | unsigned long | Timeout Elektrische Kraftstoffpumpe 1 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eml"></a>
### STEUERN_EML

0x30D607     EML (Engine Malfunction Lamp) ansteuern NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EML_WERT | unsigned long | Sollwert EML (Engine Malfunction Lamp) LV_ACT_WAL_1_EXT_ADJ |
| SW_TO_EML_WERT | unsigned long | Timeout EML (Engine Malfunction Lamp) 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-agk"></a>
### STEUERN_ENDE_AGK

0x30C100     Abgasklappe Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-anws"></a>
### STEUERN_ENDE_ANWS

0x30EE00     Vanos Auslass Ventil Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-anwsf"></a>
### STEUERN_ENDE_ANWSF

0x30A200     Ventil Vanos Auslass Frueh Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-anwsr"></a>
### STEUERN_ENDE_ANWSR

0x2E5FFA00     Anschlagsadaption Auslass Vanos ruecksetzen Vorgeben beenden  ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden.  NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-anwss"></a>
### STEUERN_ENDE_ANWSS

0x30A300     Ventil Vanos Auslass Spaet Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-avs"></a>
### STEUERN_ENDE_AVS

0x30C000     Absperrventil Saugstrahlpumpe Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dfv1a"></a>
### STEUERN_ENDE_DFV1A

0x3228     Ende Diagnosefunktion Auslass A-Vanostest 1 (Verstellzeit)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dfv1e"></a>
### STEUERN_ENDE_DFV1E

0x3223     Ende Diagnosefunktion Einlass E-Vanostest 1 (Verstellzeit)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dfv2a"></a>
### STEUERN_ENDE_DFV2A

0x3229     Ende Diagnosefunktion Auslass A-Vanostest 2 (Dichtigkeit)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dfv2e"></a>
### STEUERN_ENDE_DFV2E

0x3224     Ende Diagnosefunktion Einlass E-Vanostest 2 (Dichtigkeit)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dfvfa"></a>
### STEUERN_ENDE_DFVFA

0x32D3     Ende Diagnosefunktion Auslass A-Vanostest Fruehanschlag

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dfvfe"></a>
### STEUERN_ENDE_DFVFE

0x32D1     Ende Diagnosefunktion Einlass E-Vanostest Fruehanschlag

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dfvsa"></a>
### STEUERN_ENDE_DFVSA

0x32D4     Ende Diagnosefunktion Auslass A-Vanostest Spaetanschlag

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dfvse"></a>
### STEUERN_ENDE_DFVSE

0x32D2     Ende Diagnosefunktion Einlass E-Vanostest Spaetanschlag

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dk"></a>
### STEUERN_ENDE_DK

0x302A00     Drosselklappe Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-heizung"></a>
### STEUERN_ENDE_DMTL_HEIZUNG

0x30CE00     Diagnosemodul-Tank Leckage Heizung Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-p"></a>
### STEUERN_ENDE_DMTL_P

0x30CC00     Diagnosemodul-Tank Leckage Pumpe Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-v"></a>
### STEUERN_ENDE_DMTL_V

0x30CD00     Diagnosemodul-Tank Leckage Ventil Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-e-luefter"></a>
### STEUERN_ENDE_E_LUEFTER

0x30DA00     E-Luefter Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ebl"></a>
### STEUERN_ENDE_EBL

0x30C800     E-Box-Luefter Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ekp"></a>
### STEUERN_ENDE_EKP

0x30D800     Elektrische Kraftstoffpumpe 1 Ansteuerung beenden     Elektrische Kraftstoffpumpe 1 Deaktivierung aufheben NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-eml"></a>
### STEUERN_ENDE_EML

0x30D600     EML (Engine Malfunction Lamp) Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-enws"></a>
### STEUERN_ENDE_ENWS

0x30ED00     Vanos Einlass Ventil Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-enwsf"></a>
### STEUERN_ENDE_ENWSF

0x30A000     Ventil Vanos Einlass Frueh Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-enwsr"></a>
### STEUERN_ENDE_ENWSR

0x2E5FF900     Anschlagsadaption Einlass Vanos ruecksetzen Vorgeben beenden  ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden.  NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-enwss"></a>
### STEUERN_ENDE_ENWSS

0x30A100     Ventil Vanos Einlass Spaet Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev1"></a>
### STEUERN_ENDE_EV1

0x30E100     Einspritzventil 1 Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev2"></a>
### STEUERN_ENDE_EV2

0x30E200     Einspritzventil 2 Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev3"></a>
### STEUERN_ENDE_EV3

0x30E300     Einspritzventil 3 Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev4"></a>
### STEUERN_ENDE_EV4

0x30E400     Einspritzventil 4 Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev5"></a>
### STEUERN_ENDE_EV5

0x30E500     Einspritzventil 5 Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev6"></a>
### STEUERN_ENDE_EV6

0x30E600     Einspritzventil 6 Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ewap"></a>
### STEUERN_ENDE_EWAP

0x30BF00     elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-fgrl"></a>
### STEUERN_ENDE_FGRL

0x30D500     Fahrgeschwindigkeitsregler-Lampe Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-glf"></a>
### STEUERN_ENDE_GLF

0x30C300     Gesteuerte Luftfuehrung Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-kft"></a>
### STEUERN_ENDE_KFT

0x30C900     Kennfeldthermostat Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-kgeh"></a>
### STEUERN_ENDE_KGEH

0x30AD00     Kurbelgehaeuseentlueftung Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-korel"></a>
### STEUERN_ENDE_KOREL

0x30C700     Klimakompressor-Relais Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lls"></a>
### STEUERN_ENDE_LLS

0x309F00     Leerlaufsteller Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lrp"></a>
### STEUERN_ENDE_LRP

0x2E5FF700     Laufruhepruefung Vorgeben beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh1"></a>
### STEUERN_ENDE_LSH1

0x30D000     Lambdasondenheizung vor Kat Bank1 Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh2"></a>
### STEUERN_ENDE_LSH2

0x30D100     Lambdasondenheizung hinter Kat Bank1 Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh3"></a>
### STEUERN_ENDE_LSH3

0x30D200     Lambdasondenheizung vor Kat Bank2 Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh4"></a>
### STEUERN_ENDE_LSH4

0x30D300     Lambdasondenheizung hinter Kat Bank2 Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-mil"></a>
### STEUERN_ENDE_MIL

0x30D400     MIL (Malfunction Indicator Lamp) Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-slp"></a>
### STEUERN_ENDE_SLP

0x30CB00     Sekundaerluftpumpe Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-sok"></a>
### STEUERN_ENDE_SOK

0x30C200     Soundklappe Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-sr"></a>
### STEUERN_ENDE_SR

0x30C400     Startrelais Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-tev"></a>
### STEUERN_ENDE_TEV

0x30CF00     Tankentlueftungsventil Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ugen"></a>
### STEUERN_ENDE_UGEN

0x303200     Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-uvsg"></a>
### STEUERN_ENDE_UVSG

0x301C00     Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) Ansteuerung beenden NO_CON keine Vorraussetzungen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-energiesparmode"></a>
### STEUERN_ENERGIESPARMODE

0x310C     Energiesparmode aktivieren START-97

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EGY_WERT | unsigned long | recordLocalID 1BYTE IDENTICAL DEC EGY |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENERGIESPARMODE_TEXT | string | Status Energiesparmode  01= Fertigung, 02= Transport, 03= Werkstatt STATE_EGY_MIN_KWP |
| STAT_ENERGIESPARMODE_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-enws"></a>
### STEUERN_ENWS

0x30ED07     Vanos Einlass Ventil ansteuern CON_N_MIN nur bei erhoeter Motordrehzahl

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ENWS_WERT | real | Sollwert Vanos_E Ventil CAM_SP_IN_EXT_ADJ |
| SW_TO_ENWS_WERT | unsigned long | Timeout Vanos_E Ventil 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-enwsf"></a>
### STEUERN_ENWSF

0x30A007     Ventil Vanos Einlass Frueh ansteuern CON_N_MIN nur bei erhoeter Motordrehzahl

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ENWSF_WERT | unsigned long | Tastverhaeltniss Ventil Vanos Einlass Frueh 2BYTE_in_0_65534ms |
| SW_TO_ENWSF_WERT | unsigned long | Timeout Ventil Vanos Einlass Frueh 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-enwsr"></a>
### STEUERN_ENWSR

0x2E5FF907     Anschlagsadaption Einlass Vanos ruecksetzen vorgeben  ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden.  N_LL nur bei Leerlauf-Drehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-enwss"></a>
### STEUERN_ENWSS

0x30A107     Ventil Vanos Einlass Spaet ansteuern CON_N_MIN nur bei erhoeter Motordrehzahl

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ENWSS_WERT | unsigned long | Tastverhaeltniss Ventil Vanos Einlass Spaet 2BYTE_in_0_65534ms |
| SW_TO_ENWSS_WERT | unsigned long | Timeout Ventil Vanos Einlass Spaet 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev1"></a>
### STEUERN_EV1

0x30E107     Einspritzventil 1 ansteuern CON_EV nur bei Motordrehzahl n=0 und EKP aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV1_WERT | unsigned long | Periodendauer Einspritzventil 1 1BYTE in 0 bis 2550ms |
| SW_TV_EV1_WERT | real | Sollwert Einspritzventil 1 IV_EXT_ADJ[0] |
| SW_TO_EV1_WERT | unsigned long | Timeout Einspritzventil 1 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev2"></a>
### STEUERN_EV2

0x30E207     Einspritzventil 2 ansteuern CON_EV nur bei Motordrehzahl n=0 und EKP aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV2_WERT | unsigned long | Periodendauer Einspritzventil 2 1BYTE in 0 bis 2550ms |
| SW_TV_EV2_WERT | real | Sollwert Einspritzventil 2 IV_EXT_ADJ[4] |
| SW_TO_EV2_WERT | unsigned long | Timeout Einspritzventil 2 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev3"></a>
### STEUERN_EV3

0x30E307     Einspritzventil 3 ansteuern CON_EV nur bei Motordrehzahl n=0 und EKP aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV3_WERT | unsigned long | Periodendauer Einspritzventil 3 1BYTE in 0 bis 2550ms |
| SW_TV_EV3_WERT | real | Sollwert Einspritzventil 3 IV_EXT_ADJ[2] |
| SW_TO_EV3_WERT | unsigned long | Timeout Einspritzventil 3 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev4"></a>
### STEUERN_EV4

0x30E407     Einspritzventil 4 ansteuern CON_EV nur bei Motordrehzahl n=0 und EKP aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV4_WERT | unsigned long | Periodendauer Einspritzventil 4 1BYTE in 0 bis 2550ms |
| SW_TV_EV4_WERT | real | Sollwert Einspritzventil 4 IV_EXT_ADJ[5] |
| SW_TO_EV4_WERT | unsigned long | Timeout Einspritzventil 4 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev5"></a>
### STEUERN_EV5

0x30E507     Einspritzventil 5 ansteuern CON_EV nur bei Motordrehzahl n=0 und EKP aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV5_WERT | unsigned long | Periodendauer Einspritzventil 5 1BYTE in 0 bis 2550ms |
| SW_TV_EV5_WERT | real | Sollwert Einspritzventil 5 IV_EXT_ADJ[1] |
| SW_TO_EV5_WERT | unsigned long | Timeout Einspritzventil 5 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev6"></a>
### STEUERN_EV6

0x30E607     Einspritzventil 6 ansteuern CON_EV nur bei Motordrehzahl n=0 und EKP aus

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV6_WERT | unsigned long | Periodendauer Einspritzventil 6 1BYTE in 0 bis 2550ms |
| SW_TV_EV6_WERT | real | Sollwert Einspritzventil 6 IV_EXT_ADJ[3] |
| SW_TO_EV6_WERT | unsigned long | Timeout Einspritzventil 6 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ewap"></a>
### STEUERN_EWAP

0x30BF07     elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) ansteuern CON_EWAP nur bei Fahrzeuggeschwindigkeit v=0 und Motortemperatur TMOT kleiner 115gradCelsius und Batteriespannung UBAT groesser 10Volt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EWAP_WERT | real | Sollwert elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) N_REL_CWP_SP_EXT_ADJ |
| SW_TO_EWAP_WERT | unsigned long | Timeout elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ewap-sf"></a>
### STEUERN_EWAP_SF

0x30BF07     Sonderfunktionen elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) ansteuern CON_EWAP nur bei Fahrzeuggeschwindigkeit v=0 und Motortemperatur TMOT kleiner 115gradCelsius und Batteriespannung UBAT groesser 10Volt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EWAP_WERT | unsigned long | Periodendauer elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) 1BYTE in 0 bis 2550ms |
| SW_TV_EWAP_SF_WERT | string | Sonderfunktionen elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) 1BYTE EWAP SF |
| SW_TO_EWAP_WERT | unsigned long | Timeout elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fgrl"></a>
### STEUERN_FGRL

0x30D507     Fahrgeschwindigkeitsregler-Lampe ansteuern NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_FGRL_WERT | unsigned long | Sollwert Fahrgeschwindigkeitsregler-Lampe LV_ACT_CRU_EXT_ADJ |
| SW_TO_FGRL_WERT | unsigned long | Timeout Fahrgeschwindigkeitsregler-Lampe 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-glf"></a>
### STEUERN_GLF

0x30C307     Gesteuerte Luftfuehrung ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_GLF_WERT | unsigned long | Sollwert Gesteuerte Luftfuehrung LV_ACT_ECRAS_EXT_ADJ |
| SW_TO_GLF_WERT | unsigned long | Timeout Gesteuerte Luftfuehrung 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kft"></a>
### STEUERN_KFT

0x30C907     Kennfeldthermostat ansteuern NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_KFT_WERT | real | Sollwert Kennfeldthermostat ECTPWM_EXT_ADJ |
| SW_TO_KFT_WERT | unsigned long | Timeout Kennfeldthermostat 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kgeh"></a>
### STEUERN_KGEH

0x30AD07     Kurbelgehaeuseentlueftung ansteuern NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_KGEH_WERT | unsigned long | Sollwert Kurbelgehaeuseentlueftung LV_EVC_CRCV_OFF_EXT_ADJ |
| SW_TO_KGEH_WERT | unsigned long | Timeout Kurbelgehaeuseentlueftung 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-korel"></a>
### STEUERN_KOREL

0x30C707     Klimakompressor-Relais ansteuern NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_KOREL_WERT | unsigned long | Sollwert Klimakompressor-Relais LV_ACT_ACCOUT_RLY_EXT_ADJ |
| SW_TO_KOREL_WERT | unsigned long | Timeout Klimakompressor-Relais 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-krann"></a>
### STEUERN_KRANN

0x31E3     Ansteuern Krann-Adaptionswerte (Anforderung aus CP5404)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_WERT | long | Drehzahl NKW_SOLL |
| RF_WERT | real | Relative Luftfuellung RF |
| TANS_WERT | real | Ansauglufttemperatur TANS |
| TMOT_WERT | real | Kuehlwassertemperatur TMOT |
| BA_IST_WERT | string | Istbetriebsart BA_IST |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-leistungsstufe"></a>
### STEUERN_LEISTUNGSSTUFE

0x2E3020     Codierung fuer Leistungsstufe vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LEISTUNGSSTUFE_WERT | unsigned long | Ausgabe 1 Byte in dezimaler Form, ohne Umrechnung 1BYTE in 0 bis 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lls"></a>
### STEUERN_LLS

0x309F07     Leerlaufsteller ansteuern NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LLS_WERT | real | Tastverhaeltniss Leerlaufsteller ISAPWM_EXT_ADJ |
| SW_TO_LLS_WERT | unsigned long | Timeout Leerlaufsteller 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lrp"></a>
### STEUERN_LRP

0x2E5FF707     Laufruhepruefung vorgeben NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_GEMISCHEINGRIFF_INAKTIV_WERT | unsigned long | Gemischeingriff (1= deaktivieren  0=aktivieren) 1BYTE IDENTICAL HEX |
| SW_ZUENDWINKELEINGRIFF_INAKTIV_WERT | unsigned long | Zuendwinkeleingriff (1= deaktivieren  0=aktivieren) 1BYTE IDENTICAL HEX |
| SW_MINHUBEINGRIFF_INAKTIV_WERT | unsigned long | Minhubeingriff (1= deaktivieren  0=aktivieren) 1BYTE IDENTICAL HEX |
| SW_HUBEINGRIFF_INAKTIV_WERT | unsigned long | zylinderselektiver Hubeingriff (1= deaktivieren  0=aktivieren) 1BYTE IDENTICAL HEX |
| SW_LRP_BIT4_WERT | unsigned long | not used 1BYTE IDENTICAL HEX |
| SW_LRP_BIT5_WERT | unsigned long | not used 1BYTE IDENTICAL HEX |
| SW_LRP_BIT6_WERT | unsigned long | not used 1BYTE IDENTICAL HEX |
| SW_LRP_BIT7_WERT | unsigned long | not used 1BYTE IDENTICAL HEX |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh1"></a>
### STEUERN_LSH1

0x30D007     Lambdasondenheizung vor Kat Bank1 ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH1_WERT | real | Tastverhaeltniss Lambdasondenheizung vor Kat Bank1 LSHPWM_UP_EXT_ADJ[1] |
| SW_TO_LSH1_WERT | unsigned long | Timeout Lambdasondenheizung vor Kat Bank1 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh2"></a>
### STEUERN_LSH2

0x30D107     Lambdasondenheizung hinter Kat Bank1 ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH2_WERT | real | Tastverhaeltniss Lambdasondenheizung hinter Kat Bank1 LSHPWM_DOWN_EXT_ADJ[1] |
| SW_TO_LSH2_WERT | unsigned long | Timeout Lambdasondenheizung hinter Kat Bank1 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh3"></a>
### STEUERN_LSH3

0x30D207     Lambdasondenheizung vor Kat Bank2 ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH3_WERT | real | Tastverhaeltniss Lambdasondenheizung vor Kat Bank2 LSHPWM_UP_EXT_ADJ[2] |
| SW_TO_LSH3_WERT | unsigned long | Timeout Lambdasondenheizung vor Kat Bank2 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh4"></a>
### STEUERN_LSH4

0x30D307     Lambdasondenheizung hinter Kat Bank2 ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH4_WERT | real | Tastverhaeltniss Lambdasondenheizung hinter Kat Bank2 LSHPWM_DOWN_EXT_ADJ[2] |
| SW_TO_LSH4_WERT | unsigned long | Timeout Lambdasondenheizung hinter Kat Bank2 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mil"></a>
### STEUERN_MIL

0x30D407     MIL (Malfunction Indicator Lamp) ansteuern NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_MIL_WERT | unsigned long | Sollwert MIL (Malfunction Indicator Lamp) LV_ACT_MIL_EXT_ADJ |
| SW_TO_MIL_WERT | unsigned long | Timeout MIL (Malfunction Indicator Lamp) 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-lrp"></a>
### STEUERN_PROGRAMM_LRP

0x2E5FF708     Laufruhepruefung programmieren NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_GEMISCHEINGRIFF_INAKTIV_WERT | unsigned long | Gemischeingriff (1= deaktivieren  0=aktivieren) 1BYTE IDENTICAL HEX |
| SW_ZUENDWINKELEINGRIFF_INAKTIV_WERT | unsigned long | Zuendwinkeleingriff (1= deaktivieren  0=aktivieren) 1BYTE IDENTICAL HEX |
| SW_MINHUBEINGRIFF_INAKTIV_WERT | unsigned long | Minhubeingriff (1= deaktivieren  0=aktivieren) 1BYTE IDENTICAL HEX |
| SW_HUBEINGRIFF_INAKTIV_WERT | unsigned long | zylinderselektiver Hubeingriff (1= deaktivieren  0=aktivieren) 1BYTE IDENTICAL HEX |
| SW_LRP_BIT4_WERT | unsigned long | not used 1BYTE IDENTICAL HEX |
| SW_LRP_BIT5_WERT | unsigned long | not used 1BYTE IDENTICAL HEX |
| SW_LRP_BIT6_WERT | unsigned long | not used 1BYTE IDENTICAL HEX |
| SW_LRP_BIT7_WERT | unsigned long | not used 1BYTE IDENTICAL HEX |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-slp"></a>
### STEUERN_SLP

0x30CB07     Sekundaerluftpumpe ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_SLP_WERT | unsigned long | Sollwert Sekundaerluftpumpe LV_ACT_SAP_EXT_ADJ |
| SW_TO_SLP_WERT | unsigned long | Timeout Sekundaerluftpumpe 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sok"></a>
### STEUERN_SOK

0x30C207     Soundklappe ansteuern NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_SOK_WERT | unsigned long | Sollwert Soundklappe LV_ACT_SOF_EXT_ADJ |
| SW_TO_SOK_WERT | unsigned long | Timeout Soundklappe 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sr"></a>
### STEUERN_SR

0x30C407     Startrelais ansteuern N_EQ_ZERO nur bei Motordrehzahl n=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_SR_WERT | unsigned long | Sollwert Startrelais LV_ACT_RLY_ST_EXT_ADJ |
| SW_TO_SR_WERT | unsigned long | Timeout Startrelais 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

0x30CF07     Tankentlueftungsventil ansteuern NO_CON keine Vorraussetzungen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_TEV_WERT | real | TastverhaeltnissTankentlueftungsventil CPPWM_EXT_ADJ |
| SW_TO_TEV_WERT | unsigned long | Timeout Tankentlueftungsventil 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ugen"></a>
### STEUERN_UGEN

0x303207     Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) ansteuern N_LL nur bei Leerlauf-Drehzahl

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PHY_UGEN_WERT | real | Spannung Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) V_ALTER_SP_EXT_ADJ |
| SW_TO_UGEN_WERT | unsigned long | Timeout Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-uvsg"></a>
### STEUERN_UVSG

0x301C07     Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) ansteuern V_N_EQ_ZERO nur bei Fahrzeuggeschwindigkeit v=0 und Motordrehzahl n=0

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_UVSG_WERT | unsigned long | Sollwert Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) LV_RLY_MAIN_EXT_ADJ |
| SW_TO_UVSG_WERT | unsigned long | Timeout Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) 1BYTE in 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (4 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (76 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [HARTTEXTE](#table-harttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [MESSWERTEMODE](#table-messwertemode) (14 × 3)
- [CBSKENNUNG](#table-cbskennung) (16 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (3 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (11 × 3)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [FARTSTATUSTEXTE](#table-fartstatustexte) (9 × 2)
- [FARTERWTEXTE](#table-farterwtexte) (8 × 2)
- [BITS](#table-bits) (95 × 4)
- [LAMBDASTATUS](#table-lambdastatus) (7 × 2)
- [BETRIEBSSTUNDENSTATUS](#table-betriebsstundenstatus) (4 × 2)
- [STATE_GEAR](#table-state-gear) (9 × 2)
- [STATE_TQ_CAN_PLAUS](#table-state-tq-can-plaus) (8 × 2)
- [TPS_AD_STEP](#table-tps-ad-step) (12 × 2)
- [_CNV_S_3_STATE_RLY__396](#table-cnv-s-3-state-rly-396) (4 × 2)
- [STATE_CP](#table-state-cp) (9 × 2)
- [STATE_SA](#table-state-sa) (13 × 2)
- [VAL_MO3_ERR_CODE_MU](#table-val-mo3-err-code-mu) (22 × 2)
- [VAL_MO3_ERR_CODE_MC](#table-val-mo3-err-code-mc) (14 × 2)
- [CONF_SOF_SWI](#table-conf-sof-swi) (4 × 2)
- [STATE_MSW_CAN](#table-state-msw-can) (8 × 2)
- [EWSSTART](#table-ewsstart) (5 × 2)
- [EWSEMPFANGSSTATUS](#table-ewsempfangsstatus) (10 × 2)
- [STATE_DIAGCPS](#table-state-diagcps) (7 × 2)
- [FUNKTIONSTATUS](#table-funktionstatus) (7 × 2)
- [DIAGNOSE_STATUS](#table-diagnose-status) (5 × 2)
- [DIAGNOSE_DMTL_WERT](#table-diagnose-dmtl-wert) (26 × 2)
- [STATUS_EOL](#table-status-eol) (6 × 2)
- [EOL_STATUS](#table-eol-status) (10 × 2)
- [SYSTEMCHECK_STATE_CHK_LS](#table-systemcheck-state-chk-ls) (5 × 2)
- [STATE_DIAG_SA_LS](#table-state-diag-sa-ls) (10 × 2)
- [STATE_VLS_EOL](#table-state-vls-eol) (13 × 2)
- [STATUS_REGLER_LSH_DOWN](#table-status-regler-lsh-down) (7 × 2)
- [STATUS_REGLER_LSH_UP](#table-status-regler-lsh-up) (8 × 2)
- [GROBNAME](#table-grobname) (48 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (230 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (444 × 9)
- [FORTTEXTE](#table-forttexte) (247 × 2)
- [FARTTYP](#table-farttyp) (243 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (230 × 2)
- [MESSWERTETAB](#table-messwertetab) (444 × 12)
- [_CNV_S_10_STATE_EOL__351](#table-cnv-s-10-state-eol-351) (11 × 2)
- [_CNV_S_11_EGCP_RANGE_657](#table-cnv-s-11-egcp-range-657) (12 × 2)
- [_CNV_S_14_TMO3_ERR_C_364](#table-cnv-s-14-tmo3-err-c-364) (15 × 2)
- [_CNV_S_21_TMO3_ERR_C_365](#table-cnv-s-21-tmo3-err-c-365) (22 × 2)
- [_CNV_S_4_EGCP_RANGE_661](#table-cnv-s-4-egcp-range-661) (5 × 2)
- [_CNV_S_4_EGCP_RANGE_668](#table-cnv-s-4-egcp-range-668) (5 × 2)
- [_CNV_S_5_LACO_RANGE_694](#table-cnv-s-5-laco-range-694) (6 × 2)
- [_CNV_S_6_RANGE_STAT_105](#table-cnv-s-6-range-stat-105) (7 × 2)
- [_CNV_S_6_RANGE_STAT_146](#table-cnv-s-6-range-stat-146) (7 × 2)
- [_CNV_S_6_RANGE_STAT_304](#table-cnv-s-6-range-stat-304) (7 × 2)
- [_CNV_S_7_DEF_BA_400](#table-cnv-s-7-def-ba-400) (8 × 2)
- [_CNV_S_7_EGCP_RANGE_639](#table-cnv-s-7-egcp-range-639) (8 × 2)
- [_CNV_S_7_RANGE_ECU__142](#table-cnv-s-7-range-ecu-142) (8 × 2)
- [_CNV_S_7_RANGE_STAT_325](#table-cnv-s-7-range-stat-325) (8 × 2)
- [_CNV_S_8_RANGE_STAT_18](#table-cnv-s-8-range-stat-18) (9 × 2)
- [STAT_RUHESTROM](#table-stat-ruhestrom) (17 × 2)

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

Dimensions: 76 rows × 2 columns

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

<a id="table-harttexte"></a>
### HARTTEXTE

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

<a id="table-messwertemode"></a>
### MESSWERTEMODE

Dimensions: 14 rows × 3 columns

| TEXT | WERT | KOMMENTAR |
| --- | --- | --- |
| ein | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| aus | 0 | Argument ARG.   Messwertblock nur lesen |
| ja | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| nein | 0 | Argument ARG.   Messwertblock nur lesen |
| yes | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| no | 0 | Argument ARG.   Messwertblock nur lesen |
| on | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| off | 0 | Argument ARG.   Messwertblock nur lesen |
| 1 | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| 0 | 0 | Argument ARG.   Messwertblock nur lesen |
| 3 | 3 | Argument ID.    Messwertblock im SG löschen, neu schreiben und lesen |
| 2 | 2 | Argument ID.    Messwertblock nur lesen |
| 5 | 5 | Argument LABEL. Messwertblock im SG löschen, neu schreiben und lesen |
| 4 | 4 | Argument LABEL. Messwertblock nur lesen |

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

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 3 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| 2 | BMW-FAST |
| 1 | KWP2000* |
| 3 | KWP2000 |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | 00654301 |
| F_PCODE | ja |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 11 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxxx0 | 10 | Diagnose läuft nicht |
| xxxxxxx1 | 11 | Diagnose läuft |
| xxxxx0xx | 30 | Zyklus-Flag nicht gesetzt |
| xxxxx1xx | 31 | Zyklus-Flag gesetzt |
| xxxx0xxx | 40 | kein Fehler durch Tester |
| xxxx1xxx | 41 | Fehler durch Tester |
| xxx0xxxx | 50 | MIL aus |
| xxx1xxxx | 51 | MIL ein |
| xx0xxxxx | 60 | Fehler in Entprellphase |
| xx1xxxxx | 61 | Fehler entprellt, keine Scan Tool Ausgabe |
| xxxxxxxx | 0 | -- |

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

<a id="table-fartstatustexte"></a>
### FARTSTATUSTEXTE

Dimensions: 9 rows × 2 columns

| BITNR | BITTEXT |
| --- | --- |
| 0x00 | nicht aktiv |
| 0x01 | Fehler momentan vorhanden |
| 0x02 | Fehler geprueft |
| 0x11 | E-Flag entprellt |
| 0x12 | CARB-entprellt |
| 0x13 | SCATT-aktiv |
| 0x14 | MIL ein |
| 0x15 | MIL blink |
| 0x16 | Fehler sporadisch |

<a id="table-farterwtexte"></a>
### FARTERWTEXTE

Dimensions: 8 rows × 2 columns

| BITNR | BITTEXT |
| --- | --- |
| 0x00 | nicht aktiv             |
| 0x11 | Diagnose aktiv          |
| 0x12 | Diagnose gestoppt       |
| 0x13 | Zyklus-Flag gesetzt     |
| 0x14 | Error-Flag gesetzt      |
| 0x15 | MIL ein                 |
| 0x16 | Fehler in Entprellphase |
| 0xXY | Status unbekannt |

<a id="table-bits"></a>
### BITS

Dimensions: 95 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| STAT_KL15_EIN | 0 | 0x01 | 0x01 |
| STAT_MOTOR_AUS | 0 | 0x02 | 0x02 |
| STAT_KUPPL_EIN | 0 | 0x04 | 0x04 |
| STAT_BLS_EIN | 0 | 0x08 | 0x08 |
| STAT_BTS_EIN | 0 | 0x10 | 0x10 |
| STAT_KO_EIN | 0 | 0x80 | 0x80 |
| OBD_MIL | 0 | 0x80 | 0x80 |
| OBD_VERBRENNUNGSAUSSETZER_MONITOR | 1 | 0x01 | 0x01 |
| OBD_KRAFTSTOFFSYSTEM_MONITOR | 1 | 0x02 | 0x02 |
| OBD_KOMPONENTEN_MONITOR | 1 | 0x04 | 0x04 |
| OBD_VERBRENNUNGSAUSSETZER_READINESS | 1 | 0x10 | 0x10 |
| OBD_KRAFTSTOFFSYSTEM_READINESS | 1 | 0x20 | 0x20 |
| OBD_KOMPONENTEN_READINESS | 1 | 0x40 | 0x40 |
| OBD_KAT_UEBERWACHUNG_MONITOR | 2 | 0x01 | 0x01 |
| OBD_KAT_HEIZUNG_MONITOR | 2 | 0x02 | 0x02 |
| OBD_TANKENTLUEFTUNG_MONITOR | 2 | 0x04 | 0x04 |
| OBD_SEKUNDAERLUFTSYSTEM_MONITOR | 2 | 0x08 | 0x08 |
| OBD_KLIMA_MONITOR | 2 | 0x10 | 0x10 |
| OBD_LAMBDASONDE_MONITOR | 2 | 0x20 | 0x20 |
| OBD_LAMBDASONDENHEIZUNG_MONITOR | 2 | 0x40 | 0x40 |
| OBD_ABGASRUECKFUEHRUNG_MONITOR | 2 | 0x80 | 0x80 |
| OBD_KAT_UEBERWACHUNG_READINESS | 3 | 0x01 | 0x01 |
| OBD_KAT_HEIZUNG_READINESS | 3 | 0x02 | 0x02 |
| OBD_TANKENTLUEFTUNG_READINESS | 3 | 0x04 | 0x04 |
| OBD_SEKUNDAERLUFTSYSTEM_READINESS | 3 | 0x08 | 0x08 |
| OBD_KLIMA_READINESS | 3 | 0x10 | 0x10 |
| OBD_LAMBDASONDE_READINESS | 3 | 0x20 | 0x20 |
| OBD_LAMBDASONDENHEIZUNG_READINESS | 3 | 0x40 | 0x40 |
| OBD_ABGASRUECKFUEHRUNG_READINESS | 3 | 0x80 | 0x80 |
| OBD_MISSFIRE_MONITOR | 0 | 0x01 | 0x01 |
| OBD_FUEL_MONITOR | 0 | 0x02 | 0x02 |
| OBD_COMPREHENSIVE_MONITOR | 0 | 0x04 | 0x04 |
| OBD_MISSFIRE | 0 | 0x10 | 0x10 |
| OBD_FUELSYSTEM | 0 | 0x20 | 0x20 |
| OBD_COMPREHENSIVE | 0 | 0x40 | 0x40 |
| OBD_KAT_UEBERWACHUNG | 1 | 0x01 | 0x01 |
| OBD_KAT_HEIZUNG | 1 | 0x02 | 0x02 |
| OBD_EVAPORATE | 1 | 0x04 | 0x04 |
| OBD_SEC_AIR | 1 | 0x08 | 0x08 |
| OBD_AC_SYSTEM | 1 | 0x10 | 0x10 |
| OBD_LAMBDA | 1 | 0x20 | 0x20 |
| OBD_LAMBDA_HEATER | 1 | 0x40 | 0x40 |
| OBD_EGR | 1 | 0x80 | 0x80 |
| OBD_KAT_UEBERWACHUNG_MONITOR | 2 | 0x01 | 0x01 |
| OBD_KAT_HEIZUNG_MONITOR | 2 | 0x02 | 0x02 |
| OBD_EVAPORATE_MONITOR | 2 | 0x04 | 0x04 |
| OBD_SEC_AIR_MONITOR | 2 | 0x08 | 0x08 |
| OBD_AC_SYSTEM_MONITOR | 2 | 0x10 | 0x10 |
| OBD_LAMBDA_MONITOR | 2 | 0x20 | 0x20 |
| OBD_LAMBDA_HEATER_MONITOR | 2 | 0x40 | 0x40 |
| OBD_EGR_MONITOR | 2 | 0x80 | 0x80 |
| STAT_STATE_MSW_CAN_PLUS | 0 | 0x03 | 0x01 |
| STAT_STATE_MSW_CAN_MINUS | 0 | 0x03 | 0x02 |
| STAT_STATE_MSW_CAN_SET | 0 | 0x03 | 0x03 |
| STAT_STATE_MSW_CAN_OFF | 0 | 0x04 | 0x04 |
| STAT_LL_EIN | 0 | 0x01 | 0x01 |
| STAT_TEILLAST_EIN | 0 | 0x03 | 0x00 |
| STAT_VL_EIN | 0 | 0x02 | 0x02 |
| STAT_LSHK2_EIN | 0 | 0x04 | 0x04 |
| STAT_LSHK1_EIN | 0 | 0x08 | 0x08 |
| STAT_LSVK2_EIN | 0 | 0x10 | 0x10 |
| STAT_LSVK1_EIN | 0 | 0x20 | 0x20 |
| STAT_LS2_REGELUNG | 0 | 0x40 | 0x40 |
| STAT_LS1_REGELUNG | 0 | 0x80 | 0x80 |
| STAT_KICKDOWN | 1 | 0x04 | 0x04 |
| STAT_FAHRSTUFE | 1 | 0x08 | 0x08 |
| STAT_SCHUBAB | 1 | 0x40 | 0x40 |
| STAT_DK_ABGLEICH | 1 | 0x80 | 0x80 |
| STAT_DYN_LIM_1 | 2 | 0x01 | 0x01 |
| STAT_DYN_LIM_2 | 2 | 0x02 | 0x02 |
| STAT_FEHLER_CLSW | 2 | 0x04 | 0x04 |
| STAT_FEHLER_MFL | 2 | 0x08 | 0x08 |
| STAT_TIMEOUT_EGS1 | 2 | 0x10 | 0x10 |
| STAT_FEHLER_BREMSE | 2 | 0x20 | 0x20 |
| STAT_MON_LEVEL2 | 3 | 0x01 | 0x01 |
| STAT_V_PLAUSIBEL | 3 | 0x02 | 0x02 |
| STAT_NOTLAUF_LL | 3 | 0x04 | 0x04 |
| STAT_NOTLAUF_DK | 3 | 0x08 | 0x08 |
| STAT_FEHLER_VS | 3 | 0x10 | 0x10 |
| STAT_ASR_TIMEOUT | 3 | 0x20 | 0x20 |
| STAT_EGAS_NOTLAUF | 3 | 0x40 | 0x40 |
| STAT_VS_DIF_HOCH | 4 | 0x01 | 0x01 |
| STAT_UEBERN_LANG | 4 | 0x02 | 0x02 |
| STAT_VS_SP_MAX | 4 | 0x04 | 0x04 |
| STAT_EXT_MOMENT | 4 | 0x08 | 0x08 |
| STAT_MFL_AUS | 4 | 0x10 | 0x10 |
| STAT_VS_CAN_LANG | 5 | 0x01 | 0x01 |
| STAT_BESCHL_MON | 5 | 0x02 | 0x02 |
| STAT_HOCHDREH_S | 5 | 0x04 | 0x04 |
| STAT_TAKEOVER_VS | 5 | 0x08 | 0x08 |
| STAT_VS_FIL_LOW | 5 | 0x10 | 0x10 |
| STAT_DREHZAHL_BEG | 5 | 0x20 | 0x20 |
| STAT_BREMSE_AKTIV | 5 | 0x40 | 0x40 |
| STAT_MFL_HARD_OFF | 5 | 0x80 | 0x80 |
| STAT_FS | 1 | 0x04 | 0x04 |

<a id="table-lambdastatus"></a>
### LAMBDASTATUS

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | 1 Regelung AUS, Einschaltbedingung noch nicht erfuellt |
| 0x02 | 2 Regelung EIN |
| 0x04 | 3 Regelung AUS wegen Fahrbedingung |
| 0x08 | 4 Regelung AUS wegen erkanntem Fehler |
| 0x10 | 5 Regelung EIN mit Einschraenkung (Sensor Fehler) |
| 0xXY | Status unbekannt |

<a id="table-betriebsstundenstatus"></a>
### BETRIEBSSTUNDENSTATUS

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Betriebsstundenzaehler verstanden und akzeptiert (top_w &lt; 10h) |
| 0x01 | Betriebsstundenzaehler verstanden aber nicht akzeptiert (top_w &gt; 10h) |
| 0x02 | Betriebsstundenzaehler nicht verstanden und nicht akzeptiert |
| 0xXY | Betriebsstundenzaehler kann nicht ausgegeben werden |

<a id="table-state-gear"></a>
### STATE_GEAR

Dimensions: 9 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 0 Neutral oder Park/Neutral |
| 0x01 | 1. Gang |
| 0x02 | 2. Gang |
| 0x03 | 3. Gang |
| 0x04 | 4. Gang |
| 0x05 | 5. Gang |
| 0x06 | 6. Gang |
| 0x07 | R  Rückwärtsgang |
| 0xFF | FF unbekanntes Getriebe |

<a id="table-state-tq-can-plaus"></a>
### STATE_TQ_CAN_PLAUS

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 00 kein externer Eingriff |
| 0x01 | 01 Traktionskontrolle |
| 0x02 | 02 Sequentielles Manuelles Getriebe |
| 0x04 | 04 Getriebesteuerung |
| 0x08 | 08 Abstandsregelung |
| 0x10 | 10 Anti Roll Stabilisierung |
| 0x20 | 20 Servolenkung Typ 2 |
| 0xFF | FF unbekannter Eingriff |

<a id="table-tps-ad-step"></a>
### TPS_AD_STEP

Dimensions: 12 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 |  0 Position Notlauf 1 |
| 0x01 |  1 Position oberer Anschlag |
| 0x02 |  2 Position Notlauf 2 |
| 0x03 |  3 Positionen Ende |
| 0x04 |  4 Adaption Notlauf 1 |
| 0x05 |  5 Adaption oberer Anschlag |
| 0x06 |  6 Adaption Notlauf 2 |
| 0x07 |  7 Adaption unterer Ansschlag |
| 0x08 |  8 Adaption Notlauf |
| 0x09 |  9 Adaption Notlauf 3 |
| 0x0A | 10 Adaption Ende |
| 0xFF | FF Status unbekannt |

<a id="table-cnv-s-3-state-rly-396"></a>
### _CNV_S_3_STATE_RLY__396

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 |  Was soll ich hier nur ausgeben ? |
| 0x01 | Relais offen |
| 0x02 | Relais geschlossen |
| 0xFF | FF Status unbekannt |

<a id="table-state-cp"></a>
### STATE_CP

Dimensions: 9 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 |  0 Tankentlüftung nicht aktiv |
| 0x01 |  1 Tankentlüftung keine |
| 0x02 |  2 Tankentlüftung Minimum |
| 0x03 |  3 Tankentlüftung öffnen |
| 0x04 |  4 Tankentlüftung schnell öffnen |
| 0x05 |  5 Tankentlüftung Maximum |
| 0x06 |  6 Tankentlüftung schliessen |
| 0x07 |  7 Tankentlüftung warten auf offen |
| 0xFF | FF Status unbekannt |

<a id="table-state-sa"></a>
### STATE_SA

Dimensions: 13 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 |  0 Systemtest Sekundärluft nicht aktiv |
| 0x01 |  1 Systemtest Sekundärluft verzögert |
| 0x02 |  2 Systemtest Sekundärluft aktiv |
| 0x03 |  3 Systemtest Sekundärluft Unterbrechung |
| 0x04 |  4 Systemtest Sekundärluft Pumpe verzögert |
| 0x05 |  5 Systemtest Sekundärluft nicht aktiv |
| 0x06 |  6 Systemtest Sekundärluft abgebrochen |
| 0x07 |  7 Sekundärluft externe Ansteuerung |
| 0x08 |  8 Sekundärluft externe Ansteuerung beendet |
| 0x09 |  9 Bandendetest Sekundärluft aktiv |
| 0x0A | 10 Bandendetest Sekundärluft Pumpe |
| 0x0B | 11 Bandendetest Sekundärluft  Ende |
| 0xFF | FF Status unbekannt |

<a id="table-val-mo3-err-code-mu"></a>
### VAL_MO3_ERR_CODE_MU

Dimensions: 22 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 |  0 kein Fehler |
| 0x01 |  1 Falscher Header in der Kommunikation |
| 0x02 |  2 Fehler Prüfsumme in Kommunikation |
| 0x03 |  3 Fehler Ausgang Extension |
| 0x04 |  4 MU passt nicht zu MC Software |
| 0x05 |  5 Timeout Fehler Maximum |
| 0x06 |  6 Timeout Fehler Minimum |
| 0x07 |  7 RAM Fehler |
| 0x08 |  8 ROM Fehler |
| 0x09 |  9 Fehler Level 2 |
| 0x0A | 10 Redundant switch off path was triggerd by MC |
| 0x0B | 11 Programmablauf Überwachung 1 |
| 0x0C | 12 Programmablauf Überwachung 2 |
| 0x0D | 13 Programmablauf Überwachung 3 |
| 0x0E | 14 Programmablauf Überwachung 4 |
| 0x0F | 15 Programmablauf Überwachung 5 |
| 0x10 | 16 Programmablauf Überwachung 6 |
| 0x11 | 17 Programmablauf Überwachung 7 |
| 0x12 | 18 Programmablauf Überwachung 8 |
| 0x13 | 19 Watchdog Fehler |
| 0x14 | 20 Fehler Kommunikation, falsches enable Byte |
| 0xFF | FF Status unbekannt |

<a id="table-val-mo3-err-code-mc"></a>
### VAL_MO3_ERR_CODE_MC

Dimensions: 14 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 |  0 kein Fehler |
| 0x01 |  1 Fehler Prüfsumme in Kommunikation |
| 0x02 |  2 Falscher Header von MU |
| 0x03 |  3 Predrive Check: MU schaltet Endstufen nicht ab |
| 0x04 |  4 SW Referenz: MU sendet falsche SW Version |
| 0x05 |  5 SW Referenz: MU sendet falschen Varianten code |
| 0x06 |  6 Kopie Prozessüberwachung: MU incrementiert nicht ABC_CPM_MU |
| 0x07 |  7 Kopie Prozessüberwachung: MU incrementiert nicht Frage |
| 0x08 |  8 Programmablauf: MU ändert nicht die Kontrollbits |
| 0x09 |  9 ROM Test Level 2 |
| 0x0A | 10 RAM Test Level 2 |
| 0x0B | 11 ROM Test Level 1 |
| 0x0C | 12 ROM Test Level 2 |
| 0xFF | FF Status unbekannt |

<a id="table-conf-sof-swi"></a>
### CONF_SOF_SWI

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 0 kein Sporttaster |
| 0x01 | 1 Sporttaster vorhanden |
| 0x02 | 2 Sporttaster mit SSG |
| 0xFF | FFStatus unbekannt |

<a id="table-state-msw-can"></a>
### STATE_MSW_CAN

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 0 keine Taste gedrückt |
| 0x01 | 1 Beschleunigen / Taste+ |
| 0x02 | 2 Verlangsamen / Taste- |
| 0x03 | 3 Taste Setzen / Wiederaufnahme |
| 0x04 | 4 Taste I/O |
| 0x06 | 6 Fehler |
| 0x07 | 7 kein Text in Spec |
| 0xFF | FFStatus unbekannt |

<a id="table-ewsstart"></a>
### EWSSTART

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | DME bereit Startwert zu empfangen |
| 0x01 | kein freier Startwert Speicherplatz vorhanden |
| 0x02 | noch kein Startwert gespeichert |
| 0x03 | Startwert nicht plausibel |
| 0xXY | unbekannter Status |

<a id="table-ewsempfangsstatus"></a>
### EWSEMPFANGSSTATUS

Dimensions: 10 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Startwert verstanden und akzeptiert |
| 0x01 | Startwert verstanden aber nicht akzeptiert |
| 0x02 | Startwert nicht verstanden |
| 0x03 | Interfacefehler: Frame oder Parity oder Timeout |
| 0x04 | Prozess laeuft |
| 0x05 | Startwert Programmierung/Synchronisation wird nicht ausgefuehrt in diesem Zyklus |
| 0x06 | Dieselbe Zufallszahl wie beim letzten Start |
| 0x07 | Kein Startwert programmiert |
| 0x21 | 2 aus 3 Startwert im Flasch nicht ok |
| 0xXY | unbekannter Status |

<a id="table-state-diagcps"></a>
### STATE_DIAGCPS

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 00 Systemtest TEV Initialisierung |
| 0x01 | 01 Systemtest TEV Schritt 1 |
| 0x02 | 02 Systemtest TEV Schritt 2 |
| 0x03 | 03 Systemtest TEV Schritt 3 |
| 0x04 | 04 Systemtest TEV Rampe |
| 0x05 | 05 Systemtest TEV abgeschlossen LOCK_STEP |
| 0xXY | FF Systemtest TEV unbekannter Wert |

<a id="table-funktionstatus"></a>
### FUNKTIONSTATUS

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 0 Funktion nicht aktiv |
| 0x01 | 1 Systemtest kann nicht gestartet werden |
| 0x05 | 5 Systemtest ist nicht gestartet |
| 0x06 | 6 Systemtest ist beendet |
| 0x07 | 7 Externe Ansteuerung gestartet |
| 0x08 | 8 Externe Ansteuerung beendet |
| 0xXY | Status kann nicht ausgegeben werden |

<a id="table-diagnose-status"></a>
### DIAGNOSE_STATUS

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | 01 Systemtest läuft |
| 0x03 | 03 Systemtest beendet, Messwerte gültig |
| 0x06 | 06 Systemtest Start nicht möglich |
| 0x07 | 07 Systemtest nicht gestartet |
| 0xXY | FF Systemtest unbekannter Wert |

<a id="table-diagnose-dmtl-wert"></a>
### DIAGNOSE_DMTL_WERT

Dimensions: 26 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 0 Start |
| 0x01 | 1 Referenzleck Messung |
| 0x02 | 2 Grobleck Messung Start |
| 0x03 | 3 Grobleck Messung erweitert |
| 0x04 | 4 Grobleck Messung beendet |
| 0x05 | 5 Feinleck Messung Start |
| 0x06 | 6 Feinleck Messung erweitert |
| 0x07 | 7 2. Referenzleck Messung |
| 0x08 | 8 Tank geprüft |
| 0x09 | 9 Feinleck |
| 0x0A | A Grobleck |
| 0x0B | B Modulfehler |
| 0x0C | C Ende |
| 0x11 | 11 Batteriespannung aus gültigem Bereich |
| 0x12 | 12 elektrischer Fehler |
| 0x21 | 21 Tank Nachfüllen festgestellt |
| 0x22 | 22 Tankverschluss offen |
| 0x23 | 23 Batteriespannung Fluktuation zu hoch |
| 0x24 | 24 Diagnose maximale Zeit erreicht |
| 0x25 | 25 Fluktuationen Referenzstrom zu hoch |
| 0x26 | 26 Pumpenstrom abgefallen während der Messung |
| 0x0100 | 1 Funktion läuft |
| 0x0300 | 3 Werte gültig |
| 0x0600 | 6 Start verhindert |
| 0x0700 | 7 nicht gestartet |
| 0xXY | XY Status kann nicht ausgegeben werden |

<a id="table-status-eol"></a>
### STATUS_EOL

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | 01 Systemtest läuft |
| 0x03 | 03 Systemtest beendet, Messwerte gültig |
| 0x05 | 05 Systemtest abgebrochen, keine Werte |
| 0x06 | 06 Systemtest Start nicht möglich |
| 0x07 | 07 Systemtest nicht gestartet |
| 0xXY | FF Systemtest unbekannter Wert |

<a id="table-eol-status"></a>
### EOL_STATUS

Dimensions: 10 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 0 Funktionstest läuft |
| 0x01 | 1 Startbedingungen nicht erfüllt |
| 0x02 | 2 Übergabeparameter nicht plausibel |
| 0x03 | 3 Funktion wartet auf Freigabe |
| 0x05 | 5 Funktion noch nicht gestartet |
| 0x06 | 6 Funktion beendet |
| 0x07 | 7 Funktion abgebrochen |
| 0x08 | 8 Funktion durchlaufen und kein Fehler erkannt |
| 0x09 | 9 Funktion durchlaufen und Fehler erkannt |
| 0xFF | FF Status kann nicht ausgegeben werden |

<a id="table-systemcheck-state-chk-ls"></a>
### SYSTEMCHECK_STATE_CHK_LS

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 |  0 Diagnose Anfang |
| 0x01 |  1 Diagnose Schritt FETT |
| 0x02 |  2 Diagnose Schritt MAGER |
| 0x03 |  3 Diagnose Ende |
| 0xFF | XY Status kann nicht ausgegeben werden |

<a id="table-state-diag-sa-ls"></a>
### STATE_DIAG_SA_LS

Dimensions: 10 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 0 Systemtest SLS nicht aktiv |
| 0x01 | 1 Systemtest SLS wartet |
| 0x02 | 2 Systemtest SLS Luftmassen Überwachung |
| 0x03 | 3 Systemtest SLS Diagnose unterbrochen |
| 0x04 | 4 Systemtest SLS wartet auf Ventil Diagnose |
| 0x05 | 5 Systemtest SLS Ventil Diagnose |
| 0x06 | 6 Systemtest SLS in Prüfung |
| 0x07 | 7 Systemtest SLS beendet |
| 0x08 | 8 Systemtest SLS abgebrochen |
| 0xFF | XY Status kann nicht ausgegeben werden |

<a id="table-state-vls-eol"></a>
### STATE_VLS_EOL

Dimensions: 13 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 0 Diagnose nicht aktiv |
| 0x01 | 1 Diagnose Schritt 1 |
| 0x02 | 2 Diagnose Schritt 2 |
| 0x10 | 10 Diagnose beendet, Sonden OK |
| 0x11 | 11 Diagnose beendet, Sonden vor Kat vertauscht |
| 0x12 | 12 Diagnose beendet, Sonden nach Kat vertauscht |
| 0x13 | 13 Diagnose beendet, Sonden vor und nach Kat vertauscht |
| 0x14 | 14 Diagnose beendet, Sonden vor Kat Bank 1 nicht plausibel |
| 0x15 | 15 Diagnose beendet, Sonden vor Kat Bank 2 nicht plausibel |
| 0x16 | 16 Diagnose beendet, Sonden nach Kat Bank 1 nicht plausibel |
| 0x17 | 17 Diagnose beendet, Sonden nach Kat Bank 2 nicht plausibel |
| 0x18 | 18 Diagnose beendet, keine brauchbaren Ergebnisse |
| 0xFF | FF Status kann nicht ausgegeben werden |

<a id="table-status-regler-lsh-down"></a>
### STATUS_REGLER_LSH_DOWN

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 00 Heizung aus |
| 0x01 | 01 Heizung Vorheizphase |
| 0x02 | 02 Heizung langsam herunterregeln |
| 0x03 | 03 Heizung schnell herunterregelm |
| 0x04 | 04 Heizung langsam heraufregeln |
| 0x05 | 05 Batteriespannung Schutz |
| 0xXY | FF Heizung unbekannter Wert |

<a id="table-status-regler-lsh-up"></a>
### STATUS_REGLER_LSH_UP

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 00 Heizung aus |
| 0x01 | 01 Heizung langsam heraufregeln |
| 0x02 | 02 Heizung schnell herunterregelm |
| 0x03 | 03 Heizung langsam herunterregeln |
| 0x04 | 04 Heizung Regelung aktiv |
| 0x05 | 05 Batteriespannung Schutz |
| 0x06 | 06 Temperatur Schutz |
| 0xXY | FF Heizung unbekannter Wert |

<a id="table-grobname"></a>
### GROBNAME

Dimensions: 48 rows × 2 columns

| ADR | GROBNAME |
| --- | --- |
| 0x00 | JBBF |
| 0x01 | MRS |
| 0x12 | DME/DDE |
| 0x13 | DME/DDE |
| 0x16 | AFS |
| 0x17 | EKP |
| 0x18 | EGS |
| 0x19 | VGSG |
| 0x1C | LDM |
| 0x1D | FFP |
| 0x20 | RDC |
| 0x21 | ACC |
| 0x24 | CVM |
| 0x27 | PGS |
| 0x29 | DSC |
| 0x30 | EPS |
| 0x35 | SVS |
| 0x36 | TEL |
| 0x37 | AMP |
| 0x38 | EHC |
| 0x3B | NAV |
| 0x3C | CDC |
| 0x3F | ASK |
| 0x40 | CAS |
| 0x41 | DWA |
| 0x44 | SHD/MDS |
| 0x47 | ANTTU |
| 0x4B | VIDEO |
| 0x50 | SINE |
| 0x54 | RADIO |
| 0x56 | FZD |
| 0x60 | KOMBI |
| 0x61 | FBI |
| 0x62 | MOSTGW |
| 0x63 | MASK/CCC |
| 0x64 | PDC |
| 0x67 | ZBE |
| 0x6D | FAS |
| 0x6E | BFS |
| 0x71 | AHM |
| 0x72 | FRM |
| 0x73 | CID |
| 0x78 | KLIMA |
| 0xA0 | CCC |
| 0x90 | VIRTSG90 |
| 0x91 | VIRTSG91 |
| 0x92 | VIRTSG92 |
| 0xXY | ???? |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 230 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x0000 | 0x58FF | 0x58FF | 0x58FF | 0x58FF |
| 0x29CC | 0x5824 | 0x5834 | 0x583C | 0x586D |
| 0x29CD | 0x581F | 0x58E5 | 0x58E6 | 0x58E7 |
| 0x29CE | 0x581F | 0x58E5 | 0x58E6 | 0x58E7 |
| 0x29CF | 0x581F | 0x58E5 | 0x58E6 | 0x58E7 |
| 0x29D0 | 0x581F | 0x58E5 | 0x58E6 | 0x58E7 |
| 0x29D1 | 0x581F | 0x58E5 | 0x58E6 | 0x58E7 |
| 0x29D2 | 0x581F | 0x58E5 | 0x58E6 | 0x58E7 |
| 0x29D9 | 0x5811 | 0x586D | 0x581F | 0x583B |
| 0x29DA | 0x5811 | 0x583C | 0x58F8 | 0x58F9 |
| 0x29DB | 0x5811 | 0x581F | 0x5818 | 0x583C |
| 0x29DC | 0x581F | 0x5818 | 0x5811 | 0x583B |
| 0x29F4 | 0x5811 | 0x5818 | 0x581F | 0x581E |
| 0x29F5 | 0x5811 | 0x5818 | 0x581F | 0x581E |
| 0x2A12 | 0x5834 | 0x5874 | 0x587C | 0x583C |
| 0x2A13 | 0x5834 | 0x5874 | 0x587C | 0x583C |
| 0x2A15 | 0x583B | 0x5859 | 0x585A | 0x588D |
| 0x2A16 | 0x583B | 0x5859 | 0x585B | 0x588D |
| 0x2A17 | 0x583B | 0x5859 | 0x5867 | 0x5824 |
| 0x2A18 | 0x5834 | 0x5874 | 0x587C | 0x583C |
| 0x2A19 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A1A | 0x581F | 0x5818 | 0x5811 | 0x584D |
| 0x2A1B | 0x583B | 0x5859 | 0x585B | 0x588D |
| 0x2A1C | 0x580D | 0x5815 | 0x583B | 0x5867 |
| 0x2A2E | 0x581F | 0x5818 | 0x5811 | 0x58E2 |
| 0x2A2F | 0x581F | 0x5818 | 0x5811 | 0x58E2 |
| 0x2A80 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A82 | 0x5811 | 0x581A | 0x581B | 0x581F |
| 0x2A85 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A87 | 0x5811 | 0x581C | 0x581D | 0x581F |
| 0x2A92 | 0x580A | 0x5812 | 0x5814 | 0x58FF |
| 0x2A93 | 0x580A | 0x5812 | 0x5814 | 0x58FF |
| 0x2A94 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A95 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A96 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A97 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A98 | 0x5811 | 0x5832 | 0x5822 | 0x583C |
| 0x2A99 | 0x5811 | 0x5832 | 0x5822 | 0x583C |
| 0x2A9A | 0x5811 | 0x5832 | 0x5822 | 0x583C |
| 0x2A9B | 0x5811 | 0x5832 | 0x5822 | 0x583C |
| 0x2A9C | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A9E | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A9F | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2AA0 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2AA1 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2AA2 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2AA3 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2AAD | 0x5832 | 0x583C | 0x587C | 0x58AF |
| 0x2AAE | 0x5832 | 0x583C | 0x587C | 0x58AF |
| 0x2AB2 | 0x5811 | 0x5821 | 0x587C | 0x583C |
| 0x2AB3 | 0x5811 | 0x5821 | 0x587C | 0x583C |
| 0x2AB4 | 0x5811 | 0x5821 | 0x587C | 0x583C |
| 0x2AB5 | 0x5811 | 0x5821 | 0x587C | 0x583C |
| 0x2AB6 | 0x5811 | 0x5821 | 0x587C | 0x583C |
| 0x2AC6 | 0x5811 | 0x580D | 0x583C | 0x587C |
| 0x2AC7 | 0x5811 | 0x580D | 0x583C | 0x587C |
| 0x2ACB | 0x588B | 0x584A | 0x587C | 0x583C |
| 0x2ACC | 0x5843 | 0x584A | 0x587C | 0x583C |
| 0x2AD0 | 0x5832 | 0x5881 | 0x587C | 0x583C |
| 0x2ADF | 0x5811 | 0x5812 | 0x5813 | 0x5814 |
| 0x2AE0 | 0x5811 | 0x5812 | 0x5882 | 0x5815 |
| 0x2AE1 | 0x5811 | 0x5818 | 0x580E | 0x58D1 |
| 0x2AE5 | 0x5811 | 0x5812 | 0x5882 | 0x5815 |
| 0x2AE6 | 0x5811 | 0x5812 | 0x5882 | 0x5815 |
| 0x2AE7 | 0x5811 | 0x5812 | 0x5882 | 0x5815 |
| 0x2C24 | 0x5805 | 0x588B | 0x5845 | 0x5848 |
| 0x2C27 | 0x588C | 0x5849 | 0x5871 | 0x5845 |
| 0x2C28 | 0x588F | 0x584B | 0x5873 | 0x5848 |
| 0x2C2B | 0x588C | 0x5849 | 0x5871 | 0x5845 |
| 0x2C2C | 0x588F | 0x584B | 0x5873 | 0x5848 |
| 0x2C2D | 0x58FF | 0x5845 | 0x587D | 0x588C |
| 0x2C2E | 0x58FF | 0x5848 | 0x587E | 0x588F |
| 0x2C31 | 0x5849 | 0x5845 | 0x5878 | 0x58F5 |
| 0x2C32 | 0x584B | 0x5848 | 0x5879 | 0x58F6 |
| 0x2C39 | 0x582E | 0x5845 | 0x5830 | 0x588C |
| 0x2C3A | 0x582F | 0x5848 | 0x5831 | 0x588F |
| 0x2C3B | 0x588B | 0x5849 | 0x5845 | 0x588C |
| 0x2C3C | 0x588B | 0x584B | 0x5848 | 0x588F |
| 0x2C3D | 0x5871 | 0x589B | 0x5845 | 0x588C |
| 0x2C3E | 0x5873 | 0x589C | 0x5848 | 0x588F |
| 0x2C3F | 0x5837 | 0x5815 | 0x5845 | 0x5827 |
| 0x2C40 | 0x5838 | 0x5815 | 0x5848 | 0x5828 |
| 0x2C41 | 0x589B | 0x582C | 0x5845 | 0x5815 |
| 0x2C42 | 0x589C | 0x582D | 0x5848 | 0x5815 |
| 0x2C6A | 0x581F | 0x588B | 0x5849 | 0x584B |
| 0x2C6B | 0x5845 | 0x585C | 0x5811 | 0x5849 |
| 0x2C6C | 0x5848 | 0x585D | 0x5811 | 0x584B |
| 0x2C6D | 0x5896 | 0x585C | 0x5811 | 0x5849 |
| 0x2C6E | 0x5897 | 0x585D | 0x5811 | 0x584B |
| 0x2C73 | 0x5896 | 0x585C | 0x5849 | 0x588B |
| 0x2C74 | 0x5897 | 0x585D | 0x584B | 0x588B |
| 0x2C75 | 0x5896 | 0x585C | 0x5849 | 0x588B |
| 0x2C76 | 0x5897 | 0x585D | 0x584B | 0x588B |
| 0x2C77 | 0x5896 | 0x585C | 0x5849 | 0x588B |
| 0x2C78 | 0x5897 | 0x585D | 0x584B | 0x588B |
| 0x2C7B | 0x5896 | 0x585C | 0x5849 | 0x5845 |
| 0x2C7C | 0x5897 | 0x585D | 0x584B | 0x5848 |
| 0x2C7E | 0x5849 | 0x5845 | 0x5878 | 0x58F5 |
| 0x2C7F | 0x584B | 0x5848 | 0x5879 | 0x58F6 |
| 0x2C92 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x2C93 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x2C9C | 0x588C | 0x588B | 0x5815 | 0x5827 |
| 0x2C9D | 0x588F | 0x588B | 0x5815 | 0x5828 |
| 0x2C9E | 0x5896 | 0x585C | 0x5849 | 0x5829 |
| 0x2C9F | 0x5897 | 0x585D | 0x584B | 0x582A |
| 0x2CA6 | 0x5894 | 0x5815 | 0x5827 | 0x588C |
| 0x2CA7 | 0x5895 | 0x5815 | 0x5828 | 0x588F |
| 0x2CA8 | 0x5896 | 0x585C | 0x5829 | 0x5849 |
| 0x2CA9 | 0x5897 | 0x585D | 0x582A | 0x584B |
| 0x2CEC | 0x5858 | 0x583F | 0x5843 | 0x583C |
| 0x2CED | 0x5858 | 0x583F | 0x5843 | 0x583C |
| 0x2CEE | 0x5858 | 0x583F | 0x5843 | 0x583C |
| 0x2CEF | 0x5858 | 0x583F | 0x587C | 0x583C |
| 0x2CF6 | 0x58AB | 0x5812 | 0x584C | 0x584E |
| 0x2CF7 | 0x58AC | 0x5812 | 0x584C | 0x584E |
| 0x2CF9 | 0x584E | 0x584C | 0x5843 | 0x583C |
| 0x2CFA | 0x584E | 0x584C | 0x5843 | 0x583C |
| 0x2CFB | 0x584E | 0x584C | 0x58B0 | 0x583C |
| 0x2D06 | 0x5811 | 0x58FF | 0x58FF | 0x5812 |
| 0x2D07 | 0x584E | 0x584C | 0x5843 | 0x583C |
| 0x2D09 | 0x5811 | 0x581E | 0x581F | 0x587C |
| 0x2D0F | 0x584F | 0x5811 | 0x5858 | 0x58FF |
| 0x2D1B | 0x5846 | 0x5847 | 0x5843 | 0x583C |
| 0x2D1C | 0x5846 | 0x5847 | 0x5854 | 0x583C |
| 0x2D1D | 0x5843 | 0x5854 | 0x5846 | 0x583C |
| 0x2D1E | 0x5843 | 0x5854 | 0x5847 | 0x583C |
| 0x2D1F | 0x5843 | 0x5854 | 0x5846 | 0x5847 |
| 0x2D20 | 0x5846 | 0x5847 | 0x5843 | 0x5814 |
| 0x2D50 | 0x58B8 | 0x580D | 0x58B7 | 0x5881 |
| 0x2D51 | 0x58BD | 0x5818 | 0x58CF | 0x58B8 |
| 0x2D52 | 0x58B8 | 0x58C0 | 0x58C1 | 0x5832 |
| 0x2D53 | 0x58B8 | 0x58B9 | 0x587C | 0x5839 |
| 0x2D54 | 0x58D9 | 0x58DA | 0x58DB | 0x58DC |
| 0x2D55 | 0x58B8 | 0x5814 | 0x5846 | 0x5847 |
| 0x2D56 | 0x58C7 | 0x58C8 | 0x58C9 | 0x58CA |
| 0x2D57 | 0x58BF | 0x5881 | 0x5893 | 0x583C |
| 0x2D58 | 0x58D4 | 0x58D6 | 0x58CD | 0x5832 |
| 0x2D59 | 0x58B8 | 0x5832 | 0x58CF | 0x58D0 |
| 0x2D5A | 0x5811 | 0x5832 | 0x58CF | 0x58D1 |
| 0x2D5C | 0x58B8 | 0x5847 | 0x5854 | 0x583C |
| 0x2DB5 | 0x580D | 0x587A | 0x5832 | 0x587C |
| 0x2DB6 | 0x580D | 0x587A | 0x5832 | 0x587C |
| 0x2DB7 | 0x580D | 0x587A | 0x5832 | 0x587C |
| 0x2DBE | 0x580D | 0x5811 | 0x5832 | 0x587C |
| 0x2DC0 | 0x5811 | 0x5813 | 0x5832 | 0x5891 |
| 0x2DC6 | 0x580D | 0x5815 | 0x583B | 0x5867 |
| 0x2DC8 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x2DC9 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x2DCC | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x2DCD | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x2DCE | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x2DD0 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x2DD1 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x2DD2 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x2DD3 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x2DE0 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x2E18 | 0x5811 | 0x5812 | 0x58B1 | 0x583C |
| 0x2E19 | 0x5811 | 0x5812 | 0x58B5 | 0x583C |
| 0x2E1A | 0x5811 | 0x5812 | 0x58B3 | 0x583C |
| 0x2E1B | 0x5811 | 0x5812 | 0x58B6 | 0x583C |
| 0x2E1C | 0x5811 | 0x5812 | 0x58B2 | 0x583C |
| 0x2E1D | 0x5811 | 0x5812 | 0x58B4 | 0x583C |
| 0x2E24 | 0x5811 | 0x5812 | 0x58B1 | 0x583C |
| 0x2E25 | 0x5811 | 0x5812 | 0x58B5 | 0x583C |
| 0x2E26 | 0x5811 | 0x5812 | 0x58B3 | 0x583C |
| 0x2E27 | 0x5811 | 0x5812 | 0x58B6 | 0x583C |
| 0x2E28 | 0x5811 | 0x5812 | 0x58B2 | 0x583C |
| 0x2E29 | 0x5811 | 0x5812 | 0x58B4 | 0x583C |
| 0x2E30 | 0x5811 | 0x581F | 0x5832 | 0x583C |
| 0x2E31 | 0x5811 | 0x581F | 0x5832 | 0x583C |
| 0x2E32 | 0x5811 | 0x581F | 0x5832 | 0x583C |
| 0x2E33 | 0x5811 | 0x581F | 0x5832 | 0x583C |
| 0x2E34 | 0x5811 | 0x581F | 0x5832 | 0x583C |
| 0x2E35 | 0x5811 | 0x581F | 0x5832 | 0x583C |
| 0x2E68 | 0x5811 | 0x5812 | 0x5883 | 0x5885 |
| 0x2E69 | 0x5811 | 0x5812 | 0x5886 | 0x5888 |
| 0x2E77 | 0x580D | 0x583C | 0x5811 | 0x5832 |
| 0x2E7C | 0x5811 | 0x583C | 0x5867 | 0x587C |
| 0x2E8B | 0x587C | 0x5824 | 0x586A | 0x583C |
| 0x2E8C | 0x587C | 0x5824 | 0x586A | 0x583C |
| 0x2E8D | 0x587C | 0x5824 | 0x586A | 0x583C |
| 0x2E8E | 0x587C | 0x5824 | 0x586A | 0x583C |
| 0x2E97 | 0x5811 | 0x5898 | 0x587C | 0x583C |
| 0x2E98 | 0x5811 | 0x580D | 0x583C | 0x587C |
| 0x2E9F | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2EA1 | 0x5811 | 0x580D | 0x583C | 0x587C |
| 0x2EE0 | 0x5850 | 0x581F | 0x5824 | 0x581E |
| 0x2EE1 | 0x581F | 0x5820 | 0x583C | 0x58FF |
| 0x2EE2 | 0x581F | 0x5820 | 0x5824 | 0x5882 |
| 0x2EE3 | 0x581F | 0x5820 | 0x5824 | 0x587F |
| 0x2EEA | 0x5852 | 0x5820 | 0x5824 | 0x581E |
| 0x2EEB | 0x5820 | 0x581F | 0x5824 | 0x58FF |
| 0x2EEC | 0x5820 | 0x5882 | 0x581F | 0x5832 |
| 0x2EF4 | 0x5824 | 0x5882 | 0x5820 | 0x5811 |
| 0x2EF5 | 0x581F | 0x5820 | 0x5832 | 0x583C |
| 0x2EFE | 0x5820 | 0x587F | 0x5832 | 0x583C |
| 0x2EFF | 0x5824 | 0x587F | 0x583C | 0x5820 |
| 0x2F08 | 0x5851 | 0x581E | 0x5824 | 0x583C |
| 0x2F09 | 0x581E | 0x583A | 0x5824 | 0x581F |
| 0x2F12 | 0x5811 | 0x580D | 0x581F | 0x583C |
| 0x2F44 | 0x5811 | 0x583C | 0x587C | 0x588B |
| 0x2F45 | 0x5811 | 0x583C | 0x587C | 0x588B |
| 0x2F46 | 0x5811 | 0x583C | 0x587C | 0x588B |
| 0x2F47 | 0x5811 | 0x583C | 0x587C | 0x588B |
| 0x2F4E | 0x5811 | 0x5832 | 0x583C | 0x5881 |
| 0x2F4F | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2F58 | 0x588B | 0x584A | 0x5853 | 0x583C |
| 0x2F63 | 0x58CE | 0x58B7 | 0x587C | 0x584A |
| 0x2F64 | 0x58CE | 0x58B7 | 0x587C | 0x584A |
| 0x2F65 | 0x5814 | 0x5824 | 0x581A | 0x58FF |
| 0x2F66 | 0x5814 | 0x5824 | 0x581A | 0x58FF |
| 0x2F67 | 0x5811 | 0x580D | 0x5832 | 0x5818 |
| 0x2F71 | 0x5811 | 0x581E | 0x5821 | 0x580D |
| 0x2F76 | 0x5821 | 0x5834 | 0x5870 | 0x587C |
| 0x2F77 | 0x5834 | 0x5870 | 0x5833 | 0x5824 |
| 0x2F7B | 0x5811 | 0x5822 | 0x581F | 0x583C |
| 0x2F80 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2F85 | 0x5841 | 0x5821 | 0x5824 | 0x583C |
| 0x2F8F | 0x58B7 | 0x580D | 0x5814 | 0x58CE |
| 0x2F94 | 0x5811 | 0x580D | 0x581F | 0x583C |
| 0x2F99 | 0x5824 | 0x5833 | 0x5882 | 0x5820 |
| 0x2F9A | 0x5824 | 0x5833 | 0x581E | 0x587C |
| 0x2F9E | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2FA3 | 0x5811 | 0x583C | 0x587C | 0x588B |
| 0x2FA4 | 0x5811 | 0x583C | 0x587C | 0x588B |
| 0x2FC6 | 0x580D | 0x583C | 0x5811 | 0x5832 |
| 0xCD87 | 0x5811 | 0x5832 | 0x583C | 0x587C |
| 0xCD8B | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCD8F | 0x5811 | 0x5832 | 0x583C | 0x587C |
| 0xFFFF | 0x58FF | 0x58FF | 0x58FF | 0x58FF |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 444 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4200 | Ansauglufttemperatur 1 | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x4201 | Umgebungsdruck | hPa | - | unsigned integer | - | 0,0829175263643265 | 1 | 0,0 |
| 0x4203 | Massenstrom vom HFM | kg/h | - | unsigned integer | - | 0,03125 | 1 | 0,0 |
| 0x4204 | Umgebungstemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x4300 | Kühlwassertemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x4301 | Kühlerauslasstemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x4400 | Ölstand Mittelwert Langzeit | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x4401 | Füllstand Motoröl | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4402 | Öltemperatur | °C | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x4403 | Kraftstoff-Verbrauch seit letztem Service | - | - | unsigned long | - | 1,220703125E-4 | 1 | 0,0 |
| 0x4404 | km seit letztem Service | km | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| 0x4405 | Ölsensor Niveau Rohwert | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4406 | Ölsensor Qualität Rohwert | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4407 | Ölsensor Temperatur Rohwert | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4408 | Ölsensor Temperatur | °C | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x4409 | Ölsensor Niveau | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x440A | Ölsensor Qualität | - | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| 0x440B | Länderfaktor 1 codiert | - | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| 0x440C | Länderfaktor 2 codiert | - | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| 0x440D | Länderfaktor 1 | - | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| 0x440E | Länderfaktor 2 | - | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| 0x440F | Kurzmittelwert-Niveau für den Tester | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x4410 | Restweg aus Permittivität abgeleitet | km | - | signed integer | - | 10,0 | 1 | 0,0 |
| 0x4411 | Restweg aus Kraftstoffverbrauch abgeleitet | km | - | signed integer | - | 10,0 | 1 | 0,0 |
| 0x4412 | Öl-Alter in Monate | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4413 | aufbereitete Permittivität bei letztem Ölwechsel | - | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| 0x4414 | Permittivität für Bewertung aufbereitet (extrapoliert) | - | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| 0x4415 | Offset für Permittivitätskorrektur | - | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| 0x4416 | zugeteilte Bonuskraftstoffmenge | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4417 | zugeteilter Permittivitätsbonus | - | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| 0x4419 | Statusinformation vom Ölzustandssensor | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x441A | Statuswort mit Biteingangsgroessen OZ | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x441B | QLT-Kommunikation iO (Statuswort St_qlt_ok, Bit0) | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4505 | Sollwert Einlassspreizung | °CRK | - | unsigned char | - | 0,375 | 1 | 59,9999982118607 |
| 0x4506 | Nockenwellenposition Einlass | °CRK | - | unsigned integer | - | 0,375 | 1 | -95,9999971389771 |
| 0x4507 | Nockenwellenposition Auslass | °CRK | - | unsigned integer | - | 0,375 | 1 | -95,9999971389771 |
| 0x4508 | Istwert Einlassspreizung | °CRK | - | unsigned char | - | 0,375 | 1 | 59,9999982118607 |
| 0x4509 | Istwert Auslassspreizung | °CRK | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| 0x450A | Normspreizung Auslass | °CRK | - | signed integer | - | 0,0234375 | 1 | 0,0 |
| 0x450B | Normspreizung Einlass | °CRK | - | signed integer | - | 0,0234375 | 1 | 0,0 |
| 0x4600 | aktueller Drosselklappenwinkel | °TPS | - | unsigned integer | - | 0,00729414634406567 | 1 | 0,0 |
| 0x4601 | Drosselklappe Sollwert | °TPS | - | unsigned integer | - | 0,00729414634406567 | 1 | 0,0 |
| 0x4602 | Generator Sollspannung über BSD | V | - | unsigned long | - | 0,100000001490116 | 1 | 10,6 |
| 0x4603 | Chiptemperatur Generator 1 | °C | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x4604 | Generator Strom | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4605 | Chipversion Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4606 | Reglerversion Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4607 | Herstellercode Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4608 | Kennung Generatortyp Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4609 | Kl.87 Spannung / Versorgung DME | V | - | unsigned char | - | 0,101562492549419 | 1 | 0,0 |
| 0x460A | Batteriespannung aktuell | V | - | unsigned integer | - | 0,0149999996647239 | 1 | 0,0 |
| 0x460B | Batteriespannung von IBS gemessen | - | - | unsigned integer | - | 2,50000011874363E-4 | 1 | 6,0 |
| 0x460C | Batteriespannung vom AD-Wandler DME | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x460D | Korrekturwert Abschaltung | - | - | signed integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x460E | Abstand zur Startfähigkeitsgrenze | - | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x460F | Batterielast | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4611 | Sollwert E-Lüfter als PWM Wert | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4612 | Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x4613 | Kopierter Wert von zum Generator gesendeter Sollspannung Generator 1 | V | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x4614 | Auslastungsgrad Generator 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4615 | Kopie begrenzter Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x4616 | Kopie Generator 1 LR Vorgabe auf Bus gelegt | s | - | unsigned char | - | 0,100000001490116 | 1 | 0,0 |
| 0x4617 | gefiltertes Generatormoment absolut Ausgang | Nm | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x4618 | Kopie Drehzahlschwelle für LR-Funktion Generator 1 aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4700 | Status Lambdasonde betriebsbereit vor Katalysator Bank 1 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4701 | Status Lambdasonde betriebsbereit vor Katalysator Bank 2 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4702 | Spannung Lambdasonde vor Katalysator Bank 1 mit Offsetkorrektur | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x4703 | Spannung Lambdasonde vor Katalysator Bank 2 mit Offsetkorrektur | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x4704 | Lambda Sollwert Bank1 | - | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| 0x4705 | Lambda Sollwert Bank2 | - | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| 0x4800 | Kupplungsschalter Status | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4801 | Kupplungsschalter vorhanden | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4802 | Sporttaster aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4803 | Status Klima ein | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4804 | Sekundärluft Pumpe aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4805 | Startrelais über CAN aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4806 | Steuergeräte-Innentemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x4807 | Motor Drehzahl | rpm | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4808 | Leerlauf Solldrehzahl | rpm | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4809 | Status LL | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x480A | Kilometerstand Auflösung 1 km | km | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x480B | Pedalwert Fahrerwunsch in % | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5800 | Zeit nach Start | s | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x5801 | Umgebungsdruck | kPa | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5802 | Zustand Lambdaregelung Bank 1 | 0-n | - | 0xFF | _CNV_S_5_LACO_RANGE_694 | 1 | 1 | 0 |
| 0x5803 | Zustand Lambdaregelung Bank 2 | 0-n | - | 0xFF | _CNV_S_5_LACO_RANGE_694 | 1 | 1 | 0 |
| 0x5804 | Berechneter Lastwert | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5805 | Kühlmitteltemperatur OBD | °C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x5806 | Lambda Integrator Gruppe 1 | % | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| 0x5807 | Lambda Adaption Summe mul. und add. Gruppe 1 | % | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| 0x5808 | Lambda Integrator Gruppe 2 | % | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| 0x5809 | Lambda Adaption Summe mul. und add. Gruppe 2 | % | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| 0x580A | Kraftstoffdruck | kPa | - | unsigned char | - | 3,0 | 1 | 0,0 |
| 0x580C | Drehzahl | rpm | - | unsigned char | - | 64,0 | 1 | 0,0 |
| 0x580D | Geschwindigkeit | km/h | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x580E | Zündzeitpunkt Zylinder 1 | °CRK | - | unsigned char | - | 0,5 | 1 | -64,0 |
| 0x580F | Ansauglufttemperatur | °C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x5810 | Luftdurchsatz OBD | g/s | - | unsigned char | - | 2,5599999427795406 | 1 | 0,0 |
| 0x5811 | Motordrehzahl | rpm | - | unsigned char | - | 32,0 | 1 | 0,0 |
| 0x5812 | Luftmasse gemessen | kg/h | - | unsigned char | - | 8,0 | 1 | 0,0 |
| 0x5813 | Relative Last | % | - | signed char | - | 2,5599999427795406 | 1 | 0,0 |
| 0x5814 | Fahrpedalwert | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5815 | Batteriespannung | V | - | unsigned char | - | 0,2560000121593472 | 1 | 0,0 |
| 0x5816 | Lambda Setpoint | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x5817 | Umgebungstemperatur | °C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x5818 | Luftmasse gerechnet | mg/stk | - | unsigned char | - | 5,425863742828365 | 1 | 0,0 |
| 0x5819 | Drehzahl OBD Byte | rpm | - | unsigned char | - | 64,0 | 1 | 0,0 |
| 0x581A | Nockenwelle Einlass | °CRK | - | unsigned char | - | 0,400000005960464 | 1 | 50,0 |
| 0x581B | Nockenwelle Einlass Sollwert | °CRK | - | unsigned char | - | 0,400000005960464 | 1 | 50,0 |
| 0x581C | Nockenwelle Auslass | °CRK | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| 0x581D | Nockenwelle Auslass Sollwert | °CRK | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| 0x581E | Ansauglufttemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x581F | Motortemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5820 | Kühlmitteltemperatur Kühlerausgang | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5821 | Steuergeräte-Innentemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5822 | (Motor)-Öltemperatur | °C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x5823 | Zeit Motor steht | min | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x5824 | Umgebungstemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5825 | Abstellzeit | min | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x5826 | Drosselklappe Sensor 1 | °TPS | - | unsigned char | - | 1,8673014640808114 | 1 | 0,0 |
| 0x5827 | Lambdasondenheizung vor Katalysator Bank 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5828 | Lambdasondenheizung vor Katalysator Bank 2 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5829 | Lambdasondenheizung hinter Katalysator Bank 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x582A | Lambdasondenheizung hinter Katalysator Bank 2 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x582B | Drehmomenteingriff über CAN | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x582C | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x582D | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 2 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x582E | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 1 | - | - | unsigned char | - | 0,25 | 1 | 0,0 |
| 0x582F | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 2 | - | - | unsigned char | - | 0,25 | 1 | 0,0 |
| 0x5830 | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 1 | - | - | unsigned char | - | 0,25 | 1 | 0,0 |
| 0x5831 | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 2 | - | - | unsigned char | - | 0,25 | 1 | 0,0 |
| 0x5832 | Motor Status | 0-n | - | 0xFF | _CNV_S_6_RANGE_STAT_146 | 1 | 1 | 0 |
| 0x5833 | Umgebungstemperatur beim Start | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5834 | Umgebungsdruck | hPa | - | unsigned char | - | 21,226886749267585 | 1 | 0,0 |
| 0x5836 | Drehzahlgradient | rpm/s | - | signed char | - | 32,0 | 1 | 0,0 |
| 0x5837 | Status OBD-I Fehler vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_11_EGCP_RANGE_657 | 1 | 1 | 0 |
| 0x5838 | Status OBD-I Fehler vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_11_EGCP_RANGE_657 | 1 | 1 | 0 |
| 0x5839 | Status Drosselklappe Notlauf | 0-n | - | 0xFF | _CNV_S_6_RANGE_STAT_304 | 1 | 1 | 0 |
| 0x583A | Ansauglufttemperatur beim Start | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x583B | Kraftstofftank Füllstand | l | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x583C | Spannung Kl. 87 | V | - | unsigned char | - | 0,101562492549419 | 1 | 0,0 |
| 0x583D | Reset Quelle | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x583E | Motordrehzahl bei Reset | rpm | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x583F | Drosselklappe Sollwert | °TPS | - | unsigned char | - | 1,8673014640808114 | 1 | 0,0 |
| 0x5840 | CPU Last bei Reset | % | - | unsigned char | - | 25,0 | 1 | 0,0 |
| 0x5841 | SG-Innentemperatur Rohwert | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5843 | Versorgung FWG 1 | V | - | unsigned char | - | 0,0390625037252903 | 1 | 0,0 |
| 0x5845 | Spannung Lambdasonde vor Katalysator Bank 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5846 | Spannung Pedalwertgeber 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5847 | Spannung Pedalwertgeber 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5848 | Spannung Lambdasonde vor Katalysator Bank 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5849 | Spannung Lambdasonde hinter Katalysator Bank 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x584A | Spannung Kl. 15 Rohwert | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x584B | Spannung Lambdasonde hinter Katalysator Bank 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x584C | Spannung Drosselklappe Potentiometer 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x584D | korrigierter Sollwert Durchfluss Tankentlüftung | kg/h | - | unsigned char | - | 0,03125 | 1 | 0,0 |
| 0x584E | Spannung Drosselklappe Potentiometer 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x584F | Spannung Luftmasse | V | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| 0x5850 | Spannung Motortemperatur | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5851 | Spannung Ansauglufttemperatur | - | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| 0x5852 | Kühlmitteltemperatur Kühlerausgang Rohwert | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5853 | Spannung Kl.87 Rohwert | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5854 | Versorgung FWG 2 | V | - | unsigned char | - | 0,0390625037252903 | 1 | 0,0 |
| 0x5855 | Mittelwert Bank 1 | % | - | signed char | - | 0,390625 | 1 | 2,22044609888115E-14 |
| 0x5856 | Mittelwert Bank 2 | % | - | signed char | - | 0,390625 | 1 | 2,22044609888115E-14 |
| 0x5858 | Drosselklappe aktueller Wert | °TPS | - | unsigned char | - | 1,8673014640808114 | 1 | 0,0 |
| 0x5859 | DMTL Strom Referenzleck | mA | - | unsigned char | - | 0,195312470197678 | 1 | 0,0 |
| 0x585A | DMTL Strom Grobleck | mA | - | unsigned char | - | 0,195312470197678 | 1 | 0,0 |
| 0x585B | DMTL Strom Diagnoseende | mA | - | unsigned char | - | 0,195312470197678 | 1 | 0,0 |
| 0x585C | Widerstand Lambdasonde hinter Katalysator Bank 1 | ohm | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x585D | Widerstand Lambdasonde hinter Katalysator Bank 2 | ohm | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x585E | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 1 | ohm | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x585F | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 2 | ohm | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5860 | Widerstand Lambdasonde vor Katalysator Bank 1 | ohm | - | unsigned char | - | 64,0 | 1 | 0,0 |
| 0x5861 | Widerstand Lambdasonde vor Katalysator Bank 2 | ohm | - | unsigned char | - | 64,0 | 1 | 0,0 |
| 0x5863 | untere Byte Widerstand Lambdasonde vor Katalysator Bank 1 | ohm | - | unsigned char | - | 0,25 | 1 | 0,0 |
| 0x5864 | untere Byte Widerstand Lambdasonde vor Katalysator Bank 2 | ohm | - | unsigned char | - | 0,25 | 1 | 0,0 |
| 0x5865 | Ölstand Mittelwert Langzeit | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x5866 | Füllstand Motoröl | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5867 | Kilometerstand | km | - | unsigned char | - | 2560,0 | 1 | 0,0 |
| 0x5868 | Status Standverbraucher registriert Teil 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5869 | Status Standverbraucher registriert Teil 2 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x586A | Batteriespannung von IBS gemessen | - | - | unsigned char | - | 0,06400000303983693 | 1 | 6,0 |
| 0x586B | Zeit mit Ruhestrom 80 - 200 mA | min | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| 0x586C | Zeit mit Ruhestrom 200 - 1000 mA | min | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| 0x586D | Zähler Erkennung schlechte Strasse | - | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x586E | Zeit mit Ruhestrom größer 1000 mA | min | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| 0x5870 | Spannung DME Umgebungsdruck | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5871 | Lambda-Sollwert Gruppe 1 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x5873 | Lambda-Sollwert Gruppe 2 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x5874 | Spannung Strommessung DMTL | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5876 | Mittlere Diagnosewert minimale Luftmasse | kg/h | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5877 | Differenz zwischen Maximum und Minimum SAF | kg/h | - | unsigned char | - | 4,0 | 1 | 0,0 |
| 0x5878 | Lambdaverschiebung Rückführregler 1 | - | - | signed char | - | 9,765625E-4 | 1 | 0,0 |
| 0x5879 | Lambdaverschiebung Rückführregler 2 | - | - | signed char | - | 9,765625E-4 | 1 | 0,0 |
| 0x587A | Status FGR | 0-n | - | 0xFF | _CNV_S_6_RANGE_STAT_105 | 1 | 1 | 0 |
| 0x587C | Status Motorsteuerung | 0-n | - | 0xFF | _CNV_S_7_RANGE_ECU__142 | 1 | 1 | 0 |
| 0x587D | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_668 | 1 | 1 | 0 |
| 0x587E | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_668 | 1 | 1 | 0 |
| 0x587F | Tastverhältnis E-Lüfter | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5880 | Tastverhältnis Luftklappe | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5881 | berechneter Gang | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5882 | Motortemperatur beim Start | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5883 | Spannung Klopfwerte Zylinder 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5885 | Spannung Klopfwerte Zylinder 3 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5886 | Spannung Klopfwerte Zylinder 6 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5888 | Spannung Klopfwerte Zylinder 4 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5889 | Lambda-Istwert Gruppe 1 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x588A | Lambda-Istwert Gruppe 2 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x588B | Zeit seit Startende | s | - | unsigned char | - | 25,600000381469695 | 1 | 0,0 |
| 0x588C | Keramiktemperatur Lambdasonde vor Katalysator Bank 1 | °C | - | signed char | - | 16,0 | 1 | 0,0 |
| 0x588D | aktuelle Zeit DMTL Leckmessung | s | - | unsigned char | - | 25,600000381469695 | 1 | 0,0 |
| 0x588E | Pumpenstrom bei DMTL Pumpenprüfung | mA | - | unsigned char | - | 1,5625238418579097 | 1 | 0,0 |
| 0x588F | Keramiktemperatur Lambdasonde vor Katalysator Bank 2 | °C | - | signed char | - | 16,0 | 1 | 0,0 |
| 0x5891 | Momentanforderung an der Kupplung | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x5893 | Drehmomentabfall schnell bei Gangwechsel | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x5894 | Symptom Lambdasondenheizung vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_661 | 1 | 1 | 0 |
| 0x5895 | Symptom Lambdasondenheizung vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_661 | 1 | 1 | 0 |
| 0x5896 | Abgastemperatur hinter Katalysator Bank 1 | °C | - | unsigned char | - | 16,0 | 1 | 0,0 |
| 0x5897 | Abgastemperatur hinter Katalysator Bank 2 | °C | - | unsigned char | - | 16,0 | 1 | 0,0 |
| 0x5898 | Generator Sollspannung | V | - | unsigned char | - | 0,100000001490116 | 1 | 0,0 |
| 0x589B | Spannungsoffset Signalpfad CJ120 1 | V | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| 0x589C | Spannungsoffset Signalpfad CJ120 2 | V | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| 0x58A8 | Motorabstellzeit | min | - | unsigned char | - | 4,0 | 1 | 0,0 |
| 0x58A9 | Reset Zähler Überwachungsrechner | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58AA | Reset Zähler Hauptrechner | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58AB | Abweichung DK-Ersatzwert und DK-Potentiometer 1 | mg/stk | - | unsigned char | - | 5,425863742828365 | 1 | 0,0 |
| 0x58AC | Abweichung DK-Ersatzwert und DK-Potentiometer 2 | mg/stk | - | unsigned char | - | 5,425863742828365 | 1 | 0,0 |
| 0x58AD | Pedalwertgeber 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58AF | Kraftstoff Anforderung an Pumpe | l/h | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B0 | DK-Adaptionsschritt | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B1 | Funkenbrenndauer Zylinder 1 | ms | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| 0x58B2 | Funkenbrenndauer Zylinder 5 | ms | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| 0x58B3 | Funkenbrenndauer Zylinder 3 | ms | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| 0x58B4 | Funkenbrenndauer Zylinder 6 | ms | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| 0x58B5 | Funkenbrenndauer Zylinder 2 | ms | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| 0x58B6 | Funkenbrenndauer Zylinder 4 | ms | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| 0x58B7 | Bremsdruck | bar | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B8 | Drehzahl Überwachung | rpm | - | unsigned char | - | 32,0 | 1 | 0,0 |
| 0x58B9 | Pedalwert Überwachung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58BC | Luftmasse Überwachung | mg/stk | - | unsigned char | - | 5,44705867767334 | 1 | 0,0 |
| 0x58BD | Modellluftmasse Überwachung tiefpassgefiltert | mg/stk | - | unsigned char | - | 5,44705867767334 | 1 | 0,0 |
| 0x58BF | relative Momentenforderung von MSR über CAN | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58C0 | Motordrehzahl Ersatzwert Überwachung | rpm | - | unsigned char | - | 32,0 | 1 | 0,0 |
| 0x58C1 | Laufunruhe Segmentzeit | µs | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x58C7 | LL-Solldrehzahlabweichung Überwachung | rpm | - | unsigned char | - | 32,0 | 1 | -4096,0 |
| 0x58C8 | I-Anteil Momentdifferenz Überwachung und Modell | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58C9 | I-Anteil LL passive Rampe aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x58CA | PD-Anteil langsam Leerlaufregelung | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58CB | PD-Anteil schnell Leerlaufregelung | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58CC | Verlustmoment Überwachung | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58CD | Verlustmomentabweichung Überwachung | Nm | - | signed char | - | 2,0 | 1 | 0,0 |
| 0x58CE | Carrierbyte Schalterstati | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58CF | Motormoment Sollwert Überwachung | Nm | - | unsigned char | - | 2,0 | 1 | 0,0 |
| 0x58D0 | Motormoment Istwert Überwachung | Nm | - | unsigned char | - | 2,0 | 1 | 0,0 |
| 0x58D1 | Moment aktueller Wert | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58D4 | Abweichung maximales Moment an Kupplung Überwachung | Nm | - | signed char | - | 2,0 | 1 | 0,0 |
| 0x58D6 | Abweichung minimales Moment an Kupplung Überwachung | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58D9 | Fehler Hauptrechner | 0-n | - | 0xFF | _CNV_S_14_TMO3_ERR_C_364 | 1 | 1 | 0 |
| 0x58DA | Fehler Überwachungsrechner | 0-n | - | 0xFF | _CNV_S_21_TMO3_ERR_C_365 | 1 | 1 | 0 |
| 0x58DB | Fehler Bitfeld high Byte | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58DC | Fehler Bitfeld low Byte | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58DF | Spannung Sportschalter | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x58E0 | Abgleich Drosselklappenmodell (Faktor) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x58E1 | Abgleich Drosselklappenmodell (Offset) | kg/h | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58E2 | Abgleich Einlassventilmodell (Faktor) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x58E3 | Abgleich Einlassventilmodell (Offset) | kg/h | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58E4 | Betriebsart Istwert | 0-n | - | 0xFF | _CNV_S_7_Def_ba_400 | 1 | 1 | 0 |
| 0x58E5 | Maximale Drehzahl bei Zündaussetzern | rpm | - | unsigned char | - | 32,0 | 1 | 0,0 |
| 0x58E6 | Maximale relative Last bei Zündaussetzern | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58E7 | Minimale relative Last bei Zündaussetzern | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58E8 | Minimale Drehzahl bei Zündaussetzern | rpm | - | unsigned char | - | 32,0 | 1 | 0,0 |
| 0x58F1 | DME - Losnummer | 0-n | - | 0xFF | _CNV_S_7_RANGE_STAT_325 | 1 | 1 | 0 |
| 0x58F5 | Eingangssignal Rückführregler 1 | V | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| 0x58F6 | Eingangssignal Rückführregler 2 | V | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| 0x58F8 | Segmentadaption Laufunruhe Zyl. 5 | %. | - | signed char | - | 0,06103530898690227 | 1 | 1,92095835817427E-5 |
| 0x58F9 | Segmentadaption Laufunruhe Zyl. 3 | %. | - | signed char | - | 0,06103530898690227 | 1 | 1,92095835817427E-5 |
| 0x58FA | Beladungsgrad Aktivkohlefilter TEV- Funktionstest | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x58FB | Zähler Drehzahlerhöhungen TEV- Funktionstest | cyc | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5A00 | Versorgung FWG 1 | V | - | unsigned integer | - | 0,00976559147238731 | 1 | 0,0 |
| 0x5A01 | Versorgung FWG 2 | V | - | unsigned integer | - | 0,00976559147238731 | 1 | 0,0 |
| 0x5A04 | Spannung Pedalwertgeber 1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A05 | Spannung Pedalwertgeber 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A06 | Spannung Drosselklappe Potentiometer 1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A07 | Spannung Drosselklappe Potentiometer 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A08 | Spannung Ansauglufttemperatur | - | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| 0x5A09 | Spannung Motortemperatur | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A0A | Spannung Kühlmitteltemperatur Kühlerausgang | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A0B | Spannung DME Umgebungsdruck | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A0C | Spannung Luftmasse | V | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| 0x5A0E | Spannung SG-Innentemperatur | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A0F | Spannung Kl.15 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A10 | Spannung Kl15 | V | - | unsigned integer | - | 0,0280601158738136 | 1 | 0,0 |
| 0x5A11 | Spannung Lambdasonde vor Katalysator Bank 1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A12 | Spannung Lambdasonde vor Katalysator Bank 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A13 | Spannung Lambdasonde hinter Katalysator Bank 1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A14 | Spannung Lambdasonde hinter Katalysator Bank 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A17 | Spannung Strommessung DMTL | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A21 | Kühlmitteltemperatur Kühlerausgang | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5A22 | Steuergeräte-Innentemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5A24 | Drosselklappe Sollwert | °TPS | - | unsigned integer | - | 0,00729414634406567 | 1 | 0,0 |
| 0x5A26 | Umgebungsdruck | hPa | - | unsigned integer | - | 0,0829175263643265 | 1 | 0,0 |
| 0x5A27 | Pedalwertgeber Potentiometer 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A28 | Pedalwertgeber Potentiometer 2 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A29 | Fahrpedalwert | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A30 | Laufunruhe Zylinder 1 | µs | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A31 | Laufunruhe Zylinder 2 | µs | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A32 | Laufunruhe Zylinder 3 | µs | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A33 | Laufunruhe Zylinder 4 | µs | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A34 | Laufunruhe Zylinder 5 | µs | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A35 | Laufunruhe Zylinder 6 | µs | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A36 | Status Klopfen | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A37 | Spannung Klopfwerte Zylinder 1 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A38 | Spannung Klopfwerte Zylinder 2 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A39 | Spannung Klopfwerte Zylinder 3 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A3A | Spannung Klopfwerte Zylinder 4 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A3B | Spannung Klopfwerte Zylinder 5 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A3C | Spannung Klopfwerte Zylinder 6 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A3D | Klopfsignal Zylinder 1 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A3E | Klopfsignal Zylinder 1 relativ | - | - | unsigned integer | - | 1,52587890625E-5 | 1 | 0,0 |
| 0x5A3F | Klopfsignal Zylinder 6 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A40 | Klopfsignal Zylinder 6 relativ | - | - | unsigned integer | - | 1,52587890625E-5 | 1 | 0,0 |
| 0x5A42 | Einspritzzeit Zylinder 1 | ms | - | unsigned integer | - | 0,00400000018998981 | 1 | 0,0 |
| 0x5A43 | Einspritzzeit Zylinder 2 | ms | - | unsigned integer | - | 0,00400000018998981 | 1 | 0,0 |
| 0x5A44 | Einspritzzeit Zylinder 3 | ms | - | unsigned integer | - | 0,00400000018998981 | 1 | 0,0 |
| 0x5A45 | Einspritzzeit Zylinder 4 | ms | - | unsigned integer | - | 0,00400000018998981 | 1 | 0,0 |
| 0x5A46 | Einspritzzeit Zylinder 5 | ms | - | unsigned integer | - | 0,00400000018998981 | 1 | 0,0 |
| 0x5A47 | Einspritzzeit Zylinder 6 | ms | - | unsigned integer | - | 0,00400000018998981 | 1 | 0,0 |
| 0x5A49 | Zündwinkel Zylinder1 | °CRK | - | unsigned char | - | 0,375 | 1 | -35,6249989382923 |
| 0x5A4B | Berechneter Lastwert | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A4E | Klimakompressorrelais Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A50 | Lambdawert vor Katalysator Bank 1 | - | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| 0x5A51 | Lambdawert vor Katalysator Bank 2 | - | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| 0x5A52 | Status LS hinter Katalysator Bank 1 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A53 | Status LS hinter Katalysator Bank 2 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A54 | Status LS Heizung hinter Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_7_EGCP_RANGE_639 | 1 | 1 | 0 |
| 0x5A55 | Status LS Heizung hinter Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_7_EGCP_RANGE_639 | 1 | 1 | 0 |
| 0x5A56 | Status LS Heizung vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_7_EGCP_RANGE_639 | 1 | 1 | 0 |
| 0x5A57 | Status LS Heizung vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_7_EGCP_RANGE_639 | 1 | 1 | 0 |
| 0x5A58 | Lambdasondenheizung PWM vor Katalysator Bank 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A59 | Lambdasondenheizung PWM hinter Katalysator Bank 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A5A | Lambdasondenheizung PWM vor Katalysator Bank 2 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A5B | Lambdasondenheizung PWM hinter Katalysator Bank 2 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A60 | Bremslichtschalter Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A61 | Bremslichttestschalter Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A62 | Öldruckschalter Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A63 | E-Box-Lüfter Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A66 | DMTL Pumpe Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A67 | DMTL Ventil Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A68 | DMTL Heizung Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A69 | MIL Lampe Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A6A | Lampe FGR Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A6B | Lampe Check Engine Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A6D | Status Taste FGR | 0-n | - | 0xFF | _CNV_S_8_RANGE_STAT_18 | 1 | 1 | 0 |
| 0x5A74 | Beheizter Thermostat PWM | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A75 | Sekundärluft Ventil | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A76 | Adaption Öffnungspunkt Tankentlüftungsventil | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A77 | Tankentlüftungsventil TEV PWM | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A79 | E-Lüfter PWM | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A7A | VANOS PWM Wert Einlass früh | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A7B | VANOS PWM Wert Auslass früh | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A7C | VANOS PWM Wert Einlass spät | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A7D | VANOS PWM Wert Auslass spät | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A81 | Integrator Bank 1 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A82 | Integrator Bank 2 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A83 | Adaption Offset Lambda Bank 1 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5A84 | Adaption Offset Lambda Bank 2 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5A85 | Adaption Multiplikation Lambda Bank 1 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A86 | Adaption Multiplikation Lambda Bank 2 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A87 | Adaptionswert Trimregelung Bank 1 | - | - | signed integer | - | 6,103515625E-5 | 1 | 0,0 |
| 0x5A88 | Adaptionswert Trimregelung Bank 2 | - | - | signed integer | - | 6,103515625E-5 | 1 | 0,0 |
| 0x5A89 | multiplikative Gemischadaption hohe Last Bank 1 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A8A | multiplikative Gemischadaption hohe Last Bank 2 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A8B | multiplikative Gemischadaption niedrige Last Bank 1 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A8C | multiplikative Gemischadaption niedrige Last Bank 2 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A8D | additive Gemischadaption Leerlauf Bank 1 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5A8E | additive Gemischadaption Leerlauf Bank 2 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5A91 | Katalysatordiagnosewert Bank1 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x5A92 | Katalysatordiagnosewert Bank2 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x5A94 | Nockenwelle Auslass Sollwert | °CRK | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| 0x5A95 | Adaptionswert Nockenwelle Auslass | °CRK | - | unsigned char | - | 0,375 | 1 | -47,9999985694886 |
| 0x5A96 | Adaptionswert Nockenwelle Einlass | °CRK | - | unsigned char | - | 0,375 | 1 | -47,9999985694886 |
| 0x5A97 | Bedingung EVANOS im Anschlag beim letzten Abstellen | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A99 | Kurbelwellen Adaption beendet | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5AA1 | Status Diagnose TEV | 0-n | - | 0xFF | _CNV_S_10_STATE_EOL__351 | 1 | 1 | 0 |
| 0x5AA2 | Status Diagnose DMTL | 0-n | - | 0xFF | _CNV_S_10_STATE_EOL__351 | 1 | 1 | 0 |
| 0x5AA3 | Status Diagnose Lambdasonden | 0-n | - | 0xFF | _CNV_S_10_STATE_EOL__351 | 1 | 1 | 0 |
| 0x5AA4 | Status Diagnose Leerlaufdrehzahlverstellung | 0-n | - | 0xFF | _CNV_S_10_STATE_EOL__351 | 1 | 1 | 0 |
| 0x5AA5 | Status Diagnose Sekundärluft | 0-n | - | 0xFF | _CNV_S_10_STATE_EOL__351 | 1 | 1 | 0 |
| 0x5AB1 | Geschwindigkeit | km/h | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AB3 | Fahrstrecke mit MIL an | km | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5AB4 | Betriebsstundenzähler | h | - | unsigned long | - | 2,77777780866018E-5 | 1 | 0,0 |
| 0x5AB5 | Variante Sekundärluftpumpe | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5AB6 | Rohwert Ansauglufttemperatur 1 | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5AB7 | Rohwert Kühlwassertemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5AB9 | Spannung Sportschalter | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5ABA | PWM Kraftstoffpumpe | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5ABC | Luftmasse | kg/h | - | unsigned integer | - | 0,03125 | 1 | 0,0 |
| 0x5ABD | Starterrelais aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5AC0 | Reset Status Hardware-Register | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5AC1 | Reset Status Software-Register | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5AC2 | Reset Adresse | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5ACC | Istspreizung Einlassvanos | ° KW | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x5ACD | Sollspreizung Einlassvanos | ° KW | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x5ACE | Verstellzeit (Früh) Einlassvanos | ms | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5ACF | Verstellzeit (Spät) Einlassvanos | ms | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5AD0 | Status Vanos (Notlauf) | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AD1 | Istspreizung Auslassvanos | ° KW | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x5AD2 | Sollspreizung Auslassvanos | ° KW | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x5AD3 | Verstellzeit (Früh) Auslassvanos | ms | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5AD4 | Verstellzeit (Spät) Auslassvanos | ms | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5AE0 | Kühlmitteltemperatur &lt; 98°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AE1 | 98°C =&lt; Kühlmitteltemperatur =&lt; 112°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AE2 | 113°C =&lt; Kühlmitteltemperatur =&lt; 120°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AE3 | 121°C =&lt; Kühlmitteltemperatur =&lt; 125°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AE4 | Kühlmitteltemperatur &gt; 125°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AE5 | Motoröltemperatur &lt; 80°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AE6 | 80°C =&lt; Motoröltemperatur =&lt; 110°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AE7 | 110°C =&lt; Motoröltemperatur =&lt; 135°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AE8 | 135°C =&lt; Motoröltemperatur =&lt; 150°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AE9 | Motoröltemperatur &gt; 150°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEA | Getriebeöltemperatur &lt; 80°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEB | 80°C =&lt; Getriebeöltemperatur =&lt; 109°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEC | 110°C =&lt; Getriebeöltemperatur =&lt; 124°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AED | 125°C =&lt; Getriebeöltemperatur =&lt; 129°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEE | Getriebeöltemperatur &gt; 129°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEF | Umgebungstemperatur &lt; 3°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF0 | 3°C =&lt; Umgebungstemperatur =&lt; 19°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF1 | 20°C =&lt; Umgebungstemperatur =&lt; 29°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF2 | 30°C =&lt; Umgebungstemperatur =&lt; 39°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF3 | Umgebungstemperatur &gt; 39°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF4 | Status Auslass Dichtemessung  | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AF5 | Status Auslass Frühanschlag | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AF6 | Status Auslass Sollwert einregeln | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AF7 | Status Auslass Spätanschlag | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AF8 | Status Auslass Verstellzeitmessung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AF9 | Status Auslass Ventilansteuerung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AFA | Status Einlass Dichtemessung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AFB | Status Einlass Frühanschlag | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AFC | Status Einlass Sollwert einregeln | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AFD | Status Einlass Spätanschlag | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AFE | Status Einlass Verstellzeitmessung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AFF | Status Einlass Ventilansteuerung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58FF | Umweltbedingung unbekannt | - | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 247 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0000 | 0000 FehlerOrt nicht bedatet |
| 0x29CC | 29CC Verbrennungsaussetzer, mehrere Zylinder |
| 0x29CD | 29CD Verbrennungsaussetzer, Zylinder 1 |
| 0x29CE | 29CE Verbrennungsaussetzer, Zylinder 2 |
| 0x29CF | 29CF Verbrennungsaussetzer, Zylinder 3 |
| 0x29D0 | 29D0 Verbrennungsaussetzer, Zylinder 4 |
| 0x29D1 | 29D1 Verbrennungsaussetzer, Zylinder 5 |
| 0x29D2 | 29D2 Verbrennungsaussetzer, Zylinder 6 |
| 0x29D9 | 29D9 Verbrennungsaussetzer bei geringem Tankfüllstand |
| 0x29DA | 29DA Kurbelwellensensor, Segmentadaption |
| 0x29DB | 29DB Laufunruhe, Segmentzeitmessung |
| 0x29DC | 29DC Zylindereinspritzabschaltung |
| 0x29F4 | 29F4 Katalysatorkonvertierung |
| 0x29F5 | 29F5 Katalysatorkonvertierung 2 |
| 0x2A12 | 2A12 DMTL-Magnetventil, Ansteuerung |
| 0x2A13 | 2A13 DMTL-Leckdiagnosepumpe, Ansteuerung |
| 0x2A15 | 2A15 DMTL, Feinleck |
| 0x2A16 | 2A16 DMTL, Feinstleck |
| 0x2A17 | 2A17 DMTL, Systemfehler |
| 0x2A18 | 2A18 DMTL, Heizung: Ansteuerung |
| 0x2A19 | 2A19 Tankentlüftungsventil, Ansteuerung |
| 0x2A1A | 2A1A Tankentlüftungssystem, Funktion |
| 0x2A1B | 2A1B Tankdeckel |
| 0x2A1C | 2A1C Tankfüllstand, Plausibilität |
| 0x2A2E | 2A2E Gemischregelung |
| 0x2A2F | 2A2F Gemischregelung 2 |
| 0x2A80 | 2A80 Einlass-VANOS, Ansteuerung |
| 0x2A81 | 2A81 Einlass-VANOS, Ansteuerung 2 |
| 0x2A82 | 2A82 Einlass-VANOS |
| 0x2A85 | 2A85 Auslass-VANOS, Ansteuerung |
| 0x2A86 | 2A86 Auslass-VANOS, Ansteuerung 2 |
| 0x2A87 | 2A87 Auslass-VANOS, Mechanik |
| 0x2A92 | 2A92 Auslass-VANOS 1, Ansteuerung  |
| 0x2A93 | 2A93 Einlass-VANOS, Ansteuerung  |
| 0x2A94 | 2A94 Kurbelwellensensor, Signal |
| 0x2A95 | 2A95 Kurbelwellensensor, Synchronisation |
| 0x2A96 | 2A96 Kurbelwellensensor, Zahnfehler |
| 0x2A97 | 2A97 Kurbelwellensensor, Lückenfehler |
| 0x2A98 | 2A98 Kurbelwelle - Einlassnockenwelle, Korrelation |
| 0x2A99 | 2A99 Kurbelwelle - Auslassnockenwelle, Korrelation |
| 0x2A9A | 2A9A Nockenwellensensor Einlass, Signal |
| 0x2A9B | 2A9B Nockenwellensensor Auslass, Signal |
| 0x2A9C | 2A9C Kurbelwellensensor, elektrisch |
| 0x2A9E | 2A9E Nockenwellensensor Einlass, Synchonisation |
| 0x2A9F | 2A9F Nockenwellensensor Auslass, Synchronisation |
| 0x2AA0 | 2AA0 Nockenwellensensor Einlass, Signal |
| 0x2AA1 | 2AA1 Nockenwellensensor Auslass, Signal |
| 0x2AA2 | 2AA2 Nockenwellensensor Einlass, Lückenverlust |
| 0x2AA3 | 2AA3 Nockenwellengeber Auslass, Lückenverlust |
| 0x2AA4 | 2AA4 Nockenwellensensor Einlass, Zahnfehler |
| 0x2AA5 | 2AA5 Nockenwellensensor Auslass, Zahnfehler |
| 0x2AA6 | 2AA6 Nockenwellensensor 2 Einlass, Zahnfehler |
| 0x2AA7 | 2AA7 Nockenwellensensor 2 Auslass, Zahnfehler |
| 0x2AAD | 2AAD Kraftstoffpumpe, Notabschaltung |
| 0x2AAE | 2AAE Kraftstoffpumpe |
| 0x2AB2 | 2AB2 Steuergerät, interner Fehler: RAM |
| 0x2AB3 | 2AB3 Steuergerät, interner Fehler: Checksumme |
| 0x2AB4 | 2AB4 Steuergerät, interner Fehler: RAM-Checksumme |
| 0x2AB5 | 2AB5 Steuergerät, interner Fehler: Klopfsensorbaustein |
| 0x2AB6 | 2AB6 Steuergerät, interner Fehler: Mehrfachendstufenbaustein |
| 0x2AC6 | 2AC6 Taster Fahrdynamik-Control (SPORT-Taste), Signal |
| 0x2AC7 | 2AC7 Sportschalterbeleuchtung, elektrisch |
| 0x2ACB | 2ACB DME-Hauptrelais, Ansteuerung |
| 0x2ACC | 2ACC DME-Hauptrelais, Schaltverzögerung |
| 0x2AD0 | 2AD0 Getriebesteuerung |
| 0x2ADF | 2ADF Leerlaufregelung, Drehzahl |
| 0x2AE0 | 2AE0 Leerlaufregelung bei Kaltstart, Plausibilität |
| 0x2AE1 | 2AE1 Leistungsbedarf im Leerlauf zu hoch |
| 0x2AE5 | 2AE5 Leerlaufsteller Position AUF |
| 0x2AE6 | 2AE6 Leerlaufsteller Position ZU |
| 0x2AE7 | 2AE7 Leerlaufsteller, mechanisch |
| 0x2C24 | 2C24 Lambdasonden vor Katalysator, vertauscht |
| 0x2C27 | 2C27 Lambdasonde vor Katalysator, Systemcheck |
| 0x2C28 | 2C28 Lambdasonde vor Katalysator 2, Systemcheck |
| 0x2C2B | 2C2B Lambdasonde vor Katalysator, Systemcheck |
| 0x2C2C | 2C2C Lambdasonde vor Katalysator 2, Systemcheck |
| 0x2C2D | 2C2D Lambdasonde vor Katalysator, Schubprüfung |
| 0x2C2E | 2C2E Lambdasonde vor Katalysator 2, Schubprüfung |
| 0x2C31 | 2C31 Lambdasonde vor Katalysator, Trimmregelung |
| 0x2C32 | 2C32 Lambdasonde vor Katalysator 2, Trimmregelung |
| 0x2C39 | 2C39 Lambdasonde vor Katalysator, Dynamik |
| 0x2C3A | 2C3A Lambdasonde vor Katalysator 2, Dynamik |
| 0x2C3B | 2C3B Lambdasonde vor Katalysator, nicht angesteckt |
| 0x2C3C | 2C3C Lambdasonde vor Katalysator 2, nicht angesteckt |
| 0x2C3D | 2C3D Lambdasonde vor Katalysator, Leitungsfehler |
| 0x2C3E | 2C3E Lambdasonde vor Katalysator 2, Leitungsfehler |
| 0x2C3F | 2C3F Steuergerät, interner Fehler: Lambdasonde, Auswertebaustein |
| 0x2C40 | 2C40 Steuergerät, interner Fehler: Lambdasonde 2, Auswertebaustein |
| 0x2C41 | 2C41 Steuergerät, interner Fehler: Lambdasonde |
| 0x2C42 | 2C42 Steuergerät, interner Fehler: Lambdasonde 2 |
| 0x2C6A | 2C6A Lambdasonden nach Katalysator, vertauscht |
| 0x2C6B | 2C6B Lambdasonde nach Katalysator, Systemcheck |
| 0x2C6C | 2C6C Lambdasonde nach Katalysator 2, Systemcheck |
| 0x2C6D | 2C6D Lambdasonde nach Katalysator, Alterung |
| 0x2C6E | 2C6E Lambdasonde nach Katalysator 2, Alterung |
| 0x2C73 | 2C73 Lambdasonde nach Katalysator, Signal |
| 0x2C74 | 2C74 Lambdasonde nach Katalysator 2, Signal |
| 0x2C75 | 2C75 Lambdasonde nach Katalysator, Signal |
| 0x2C76 | 2C76 Lambdasonde nach Katalysator 2, Signal |
| 0x2C77 | 2C77 Lambdasonde nach Katalysator, Signal |
| 0x2C78 | 2C78 Lambdasonde nach Katalysator 2, Signal |
| 0x2C7B | 2C7B Lambdasonde nach Katalysator, Signal |
| 0x2C7C | 2C7C Lambdasonde nach Katalysator 2, Signal |
| 0x2C7E | 2C7E Lambdasonde nach Katalysator, Trimmregelung |
| 0x2C7F | 2C7F Lambdasonde nach Katalysator 2, Trimmregelung |
| 0x2C92 | 2C92 Abgastemperatursensor, elektrisch |
| 0x2C93 | 2C93 Abgastemperatursensor, Plausibilität |
| 0x2C9C | 2C9C Lambdasondenbeheizung vor Katalysator, Ansteuerung |
| 0x2C9D | 2C9D Lambdasondenbeheizung vor Katalysator 2, Ansteuerung |
| 0x2C9E | 2C9E Lambdasondenbeheizung nach Katalysator, Ansteuerung |
| 0x2C9F | 2C9F Lambdasondenbeheizung nach Katalysator 2, Ansteuerung |
| 0x2CA6 | 2CA6 Lambdasondenbeheizung vor Katalysator, Funktion |
| 0x2CA7 | 2CA7 Lambdasondenbeheizung vor Katalysator 2, Funktion |
| 0x2CA8 | 2CA8 Lambdasondenbeheizung nach Katalysator, Funktion |
| 0x2CA9 | 2CA9 Lambdasondenbeheizung nach Katalysator 2, Funktion |
| 0x2CEC | 2CEC Drosselklappensteller, klemmt kurzzeitig |
| 0x2CED | 2CED Drosselklappensteller, klemmt dauerhaft |
| 0x2CEE | 2CEE Drosselklappensteller, schwergängig |
| 0x2CEF | 2CEF Drosselklappensteller, Ansteuerung |
| 0x2CF6 | 2CF6 Drosselklappenpotenziometer 1, Plausibilität zu Luftmasse |
| 0x2CF7 | 2CF7 Drosselklappenpotenziometer 2, Plausibilität zu Luftmasse |
| 0x2CF9 | 2CF9 Drosselklappenpotenziometer 1 |
| 0x2CFA | 2CFA Drosselklappenpotenziometer 2 |
| 0x2CFB | 2CFB Drosselklappen-Adaptionswert |
| 0x2D06 | 2D06 Luftmassensystem |
| 0x2D07 | 2D07 Drosselklappe |
| 0x2D09 | 2D09 Drosselklappe |
| 0x2D0F | 2D0F Luftmassenmesser, Signal |
| 0x2D1B | 2D1B Fahrpedalmodul, Pedalwertgeber Signal 1 |
| 0x2D1C | 2D1C Fahrpedalmodul, Pedalwertgeber Signal 2 |
| 0x2D1D | 2D1D Fahrpedalmodul, Pedalwertgeber 1, Spannungsversorgung |
| 0x2D1E | 2D1E Fahrpedalmodul, Pedalwertgeber 2, Spannungsversorgung |
| 0x2D1F | 2D1F Fahrpedalmodul, Pedalwertgeber Potentiometer, Signal |
| 0x2D20 | 2D20 Fahrpedalmodul, Pedalwertgeber, Plausibilität zwischen Signal 1 und Signal 2 |
| 0x2D29 | 2D29 Differenzdrucksensor, Saugrohr: Plausibilität |
| 0x2D50 | 2D50 DME, interner Fehler:  Überwachung Fahrgeschwindigkeitsregelung |
| 0x2D51 | 2D51 Überwachung Luftpfad |
| 0x2D52 | 2D52 DME, interner Fehler: Überwachung Motordrehzahl |
| 0x2D53 | 2D53 DME, interner Fehler: Überwachung Drehzahlbegrenzung |
| 0x2D54 | 2D54 DME, interner Fehler: Überwachung  Drehzahlbegrenzung Reset |
| 0x2D55 | 2D55 DME, interner Fehler: Überwachung Fahrpedalmodul |
| 0x2D56 | 2D56 DME, interner Fehler: Überwachung Leerlaufregelung |
| 0x2D57 | 2D57 DME, interner Fehler: Überwachung externe Momentenanforderung |
| 0x2D58 | 2D58 DME, interner Fehler: Überwachung Sollmoment |
| 0x2D59 | 2D59 DME, interner Fehler: Überwachung Istmoment |
| 0x2D5A | 2D5A Überwachung Motordrehmoment-Begrenzung |
| 0x2D5C | 2D5C DME, interner Fehler: Überwachung Hardware |
| 0x2DB5 | 2DB5 Fahrgeschwindigkeitsregelung, Signal |
| 0x2DB6 | 2DB6 Fahrgeschwindigkeitsregelung,Schalter Multifunktionslenkrad |
| 0x2DB7 | 2DB7 Fahrgeschwindigkeitsregelung, Zeitlimit der Datenübertragung erreicht |
| 0x2DBE | 2DBE Aktive Geschwindigkeitsregelung, gesperrt für Fahrzyklus |
| 0x2DC0 | 2DC0 Längsdynamikmanagement |
| 0x2DC6 | 2DC6 Tankfüllstandswert, Plausibilität |
| 0x2DC8 | 2DC8 Botschaft vom EGS fehlt, EGS 1 |
| 0x2DC9 | 2DC9 Botschaft vom EGS fehlt, EGS 2 |
| 0x2DCC | 2DCC Botschaft vom ASC/DSC fehlt, ASC 1 |
| 0x2DCD | 2DCD Botschaft vom ASC/DSC fehlt, ASC 3 |
| 0x2DCE | 2DCE Botschaft vom ASC/DSC fehlt, ASC 4 |
| 0x2DD0 | 2DD0 Botschaft von der Instrumentenkombination fehlt, I-Kombi 2 |
| 0x2DD1 | 2DD1 Botschaft von der Instrumentenkombination fehlt, I-Kombi 3 |
| 0x2DD2 | 2DD2 Botschaft vom LWS-Steuergerät fehlt, LWS |
| 0x2DD3 | 2DD3 Botschaft vom SMG-Steuergerät fehlt,  SMG 1 |
| 0x2DE0 | 2DE0 Botschaft von der elektrischen Kraftstoffpumpe fehlt, EKP |
| 0x2E18 | 2E18 Zündung, Zylinder 1 |
| 0x2E19 | 2E19 Zündung, Zylinder 2 |
| 0x2E1A | 2E1A Zündung, Zylinder 3 |
| 0x2E1B | 2E1B Zündung, Zylinder 4 |
| 0x2E1C | 2E1C Zündung, Zylinder 5 |
| 0x2E1D | 2E1D Zündung, Zylinder 6 |
| 0x2E24 | 2E24 Zündspule Zylinder 1 |
| 0x2E25 | 2E25 Zündspule Zylinder 2 |
| 0x2E26 | 2E26 Zündspule Zylinder 3 |
| 0x2E27 | 2E27 Zündspule Zylinder 4 |
| 0x2E28 | 2E28 Zündspule Zylinder 5 |
| 0x2E29 | 2E29 Zündspule Zylinder 6 |
| 0x2E30 | 2E30 Einspritzventil Zylinder 1, Ansteuerung |
| 0x2E31 | 2E31 Einspritzventil Zylinder 2, Ansteuerung |
| 0x2E32 | 2E32 Einspritzventil Zylinder 3, Ansteuerung |
| 0x2E33 | 2E33 Einspritzventil Zylinder 4, Ansteuerung |
| 0x2E34 | 2E34 Einspritzventil Zylinder 5, Ansteuerung |
| 0x2E35 | 2E35 Einspritzventil Zylinder 6, Ansteuerung |
| 0x2E68 | 2E68 Klopfsensorsignal 1 |
| 0x2E69 | 2E69 Klopfsensorsignal 2 |
| 0x2E6A | 2E6A Klopfsensorsignal 3 |
| 0x2E77 | 2E77 Zündung, Spannungsversorgung |
| 0x2E7C | 2E7C Bitserielle Datenschnittstelle, Signal |
| 0x2E81 | 2E81 Elektrische Wasserpumpe, Drehzahlabweichung |
| 0x2E82 | 2E82 Elektrische Wasserpumpe, Abschaltung |
| 0x2E83 | 2E83 Elektrische Wasserpumpe, leistungsreduzierter Betrieb |
| 0x2E84 | 2E84 Elektrische Wasserpumpe, Kommunikation |
| 0x2E85 | 2E85 Elektrische Wasserpumpe, Kommunikation |
| 0x2E8B | 2E8B Intelligenter Batteriesensor, Signal |
| 0x2E8C | 2E8C Intelligenter Batteriesensor, Funktion |
| 0x2E8D | 2E8D Intelligenter Batteriesensor, Signalübertragung |
| 0x2E8E | 2E8E Intelligenter Batteriesensor, Kommunikation |
| 0x2E97 | 2E97 Generator |
| 0x2E98 | 2E98 Generator, Kommunikation |
| 0x2E9F | 2E9F Ölzustandssensor |
| 0x2EA1 | 2EA1 Ölzustandssensor, Kommunikation |
| 0x2EE0 | 2EE0 Kühlmitteltemperatursensor, Signal |
| 0x2EE1 | 2EE1 Kühlmitteltemperatursensor, Plausibilität |
| 0x2EE2 | 2EE2 Kühlmitteltemperatursensor, Plausibilität, Signal konstant |
| 0x2EE3 | 2EE3 Kühlmitteltemperatursensor, Plausibilität, Gradient |
| 0x2EEA | 2EEA Temperatursensor Kühleraustritt, Signal |
| 0x2EEB | 2EEB Temperatursensor Kühleraustritt, Plausibilität, Gradient |
| 0x2EEC | 2EEC Temperatursensor Kühleraustritt, Plausibilität |
| 0x2EF4 | 2EF4 Kennfeldthermostat, Mechanik |
| 0x2EF5 | 2EF5 Kennfeldthermostat, Ansteuerung |
| 0x2EFE | 2EFE Elektrolüfter, Ansteuerung |
| 0x2EFF | 2EFF Elektrolüfter, Eigendiagnose |
| 0x2F08 | 2F08 Ansauglufttemperatursensor, Signal |
| 0x2F09 | 2F09 Ansauglufttemperatursensor, Plausibilität |
| 0x2F0D | 2F0D Kühlerjalousie, Ansteuerung, (GLF) |
| 0x2F0F | 2F0F Kühlerjalousie, unten |
| 0x2F12 | 2F12 Klimakompressor, Ansteuerung |
| 0x2F44 | 2F44 EWS Manipulationsschutz |
| 0x2F45 | 2F45 Schnittstelle EWS-DME |
| 0x2F46 | 2F46 EWS Wechselcode-Abspeicherng |
| 0x2F47 | 2F47 EWS Irreversibler Steuergerätefehler |
| 0x2F4E | 2F4E Fahrzeuggeschwindigkeit, Signal |
| 0x2F4F | 2F4F Fahrzeuggeschwindigkeit, Plausibilität |
| 0x2F58 | 2F58 Startautomatik, Ansteuerung |
| 0x2F63 | 2F63 Bremslichtschalter, Plausibilität |
| 0x2F64 | 2F64 Bremslichttestschalter, Plausibilität |
| 0x2F65 | 2F65 Bremskraftverstärker, Systemcheck |
| 0x2F66 | 2F66 Bremskraftverstärker, elektrisch ATIC39 |
| 0x2F67 | 2F67 Kupplungsschalter, Signal |
| 0x2F71 | 2F71 E-Box-Lüfter, Ansteuerung |
| 0x2F76 | 2F76 Umgebungsdrucksensor, Signal |
| 0x2F77 | 2F77 Umgebungsdrucksensor, Plausibilität |
| 0x2F7B | 2F7B Öldruckschalter, Plausibilität |
| 0x2F80 | 2F80 Motorabstellzeit, Plausibilität |
| 0x2F85 | 2F85 DME, interner Fehler: Innentemperatursensor, Signal |
| 0x2F8F | 2F8F Fahrpedalmodul und Bremspedal, Plausibilität |
| 0x2F94 | 2F94 Kraftstoffpumpenrelais, Ansteuerung |
| 0x2F99 | 2F99 Umgebungstemperatursensor, Plausibilität |
| 0x2F9A | 2F9A Umgebungstemperatursensor, Kommunikation |
| 0x2F9E | 2F9E Thermischer Ölniveausensor |
| 0x2FA3 | 2FA3 Codierung fehlt |
| 0x2FA4 | 2FA4 Falscher Datensatz |
| 0x2FC6 | 2FC6 Energiesparmodus aktiv |
| 0x2FDA | 2FDA Kurbelgehäuseentlüftung, Systemcheck |
| 0x2FDB | 2FDB Kurbelgehäuseentlüftung, elektrisch ATIC39 |
| 0xCD87 | CD87 PT-CAN Kommunikationsfehler |
| 0xCD8B | CD8B Local-CAN Kommunikationsfehler |
| 0xCD8F | CD8F PT-CAN Kommunikationsfehler |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 243 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x29CC | 0x0007 | 0x0006 | 0x0005 | 0x0003 |
| 0x29CD | 0x0000 | 0x0006 | 0x0005 | 0x0003 |
| 0x29CE | 0x0000 | 0x0006 | 0x0005 | 0x0003 |
| 0x29CF | 0x0000 | 0x0006 | 0x0005 | 0x0003 |
| 0x29D0 | 0x0000 | 0x0006 | 0x0005 | 0x0003 |
| 0x29D1 | 0x0000 | 0x0006 | 0x0005 | 0x0003 |
| 0x29D2 | 0x0000 | 0x0006 | 0x0005 | 0x0003 |
| 0x29D9 | 0x0000 | 0x0000 | 0x0009 | 0x0000 |
| 0x29DA | 0x0000 | 0x0000 | 0x000A | 0x0000 |
| 0x29DB | 0x0000 | 0x0000 | 0x000B | 0x0000 |
| 0x29DC | 0x0009 | 0x0000 | 0x0000 | 0x0000 |
| 0x29F4 | 0x0000 | 0x0000 | 0x000C | 0x000C |
| 0x29F5 | 0x0000 | 0x0000 | 0x000C | 0x000C |
| 0x2A12 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2A13 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2A15 | 0x0000 | 0x0000 | 0x0000 | 0x001B |
| 0x2A16 | 0x0000 | 0x0000 | 0x001C | 0x0000 |
| 0x2A17 | 0x001F | 0x001E | 0x0020 | 0x001D |
| 0x2A18 | 0x0000 | 0x0016 | 0x0017 | 0x0021 |
| 0x2A19 | 0x0000 | 0x0016 | 0x0017 | 0x0021 |
| 0x2A1A | 0x0023 | 0x0022 | 0x0000 | 0x0000 |
| 0x2A1B | 0x0000 | 0x0000 | 0x0000 | 0x0024 |
| 0x2A1C | 0x0025 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A2E | 0x0000 | 0x0000 | 0x0027 | 0x0026 |
| 0x2A2F | 0x0000 | 0x0000 | 0x0027 | 0x0026 |
| 0x2A80 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2A81 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2A82 | 0x0028 | 0x00C8 | 0x0000 | 0x0000 |
| 0x2A85 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2A86 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2A87 | 0x0028 | 0x00C8 | 0x0000 | 0x0000 |
| 0x2A92 | 0x0000 | 0x00CB | 0x00CA | 0x00C9 |
| 0x2A93 | 0x0000 | 0x00CB | 0x00CA | 0x00C9 |
| 0x2A94 | 0x0000 | 0x0000 | 0x0019 | 0x0029 |
| 0x2A95 | 0x0000 | 0x0000 | 0x0000 | 0x002A |
| 0x2A96 | 0x0000 | 0x0000 | 0x0000 | 0x002B |
| 0x2A97 | 0x0000 | 0x0000 | 0x0000 | 0x002C |
| 0x2A98 | 0x0000 | 0x0000 | 0x002E | 0x002D |
| 0x2A99 | 0x0000 | 0x0000 | 0x002E | 0x002D |
| 0x2A9A | 0x0000 | 0x0000 | 0x0000 | 0x002F |
| 0x2A9B | 0x0000 | 0x0000 | 0x0000 | 0x002F |
| 0x2A9C | 0x0000 | 0x0000 | 0x0000 | 0x00CC |
| 0x2A9E | 0x0000 | 0x0000 | 0x0000 | 0x002A |
| 0x2A9F | 0x0000 | 0x0000 | 0x0000 | 0x002A |
| 0x2AA0 | 0x0000 | 0x0000 | 0x0000 | 0x0029 |
| 0x2AA1 | 0x0000 | 0x0000 | 0x0000 | 0x0029 |
| 0x2AA2 | 0x0000 | 0x0000 | 0x0000 | 0x0030 |
| 0x2AA3 | 0x0000 | 0x0000 | 0x0000 | 0x0030 |
| 0x2AA4 | 0x0000 | 0x0000 | 0x0000 | 0x00CD |
| 0x2AA5 | 0x0000 | 0x0000 | 0x0000 | 0x00CD |
| 0x2AA6 | 0x0000 | 0x0000 | 0x0000 | 0x00CD |
| 0x2AA7 | 0x0000 | 0x0000 | 0x0000 | 0x00CD |
| 0x2AAD | 0x0000 | 0x0031 | 0x0000 | 0x0000 |
| 0x2AAE | 0x0033 | 0x0035 | 0x0034 | 0x0032 |
| 0x2AB2 | 0x0000 | 0x0000 | 0x0037 | 0x0036 |
| 0x2AB3 | 0x0000 | 0x0039 | 0x003A | 0x0038 |
| 0x2AB4 | 0x0000 | 0x0000 | 0x0000 | 0x003B |
| 0x2AB5 | 0x0000 | 0x003C | 0x0000 | 0x0000 |
| 0x2AB6 | 0x0000 | 0x003C | 0x0000 | 0x0000 |
| 0x2AC6 | 0x0000 | 0x0000 | 0x0017 | 0x003D |
| 0x2ACB | 0x0000 | 0x0000 | 0x003F | 0x003E |
| 0x2ACC | 0x0000 | 0x0000 | 0x0000 | 0x0040 |
| 0x2AD0 | 0x0041 | 0x0000 | 0x0000 | 0x0000 |
| 0x2ADF | 0x0000 | 0x0000 | 0x0034 | 0x0032 |
| 0x2AE0 | 0x0000 | 0x0000 | 0x0034 | 0x0032 |
| 0x2AE1 | 0x0000 | 0x0000 | 0x0000 | 0x00CE |
| 0x2AE5 | 0x0000 | 0x00CB | 0x00CA | 0x00CF |
| 0x2AE6 | 0x0000 | 0x00CB | 0x00CA | 0x00C9 |
| 0x2C24 | 0x0042 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C27 | 0x0000 | 0x0000 | 0x0000 | 0x0026 |
| 0x2C28 | 0x0000 | 0x0000 | 0x0000 | 0x0026 |
| 0x2C2B | 0x0000 | 0x0000 | 0x0000 | 0x0027 |
| 0x2C2C | 0x0000 | 0x0000 | 0x0000 | 0x0027 |
| 0x2C2D | 0x0000 | 0x0000 | 0x0000 | 0x0043 |
| 0x2C2E | 0x0000 | 0x0000 | 0x0000 | 0x0043 |
| 0x2C31 | 0x0000 | 0x0000 | 0x0045 | 0x0044 |
| 0x2C32 | 0x0000 | 0x0000 | 0x0045 | 0x0044 |
| 0x2C39 | 0x0000 | 0x0000 | 0x0000 | 0x0047 |
| 0x2C3A | 0x0000 | 0x0000 | 0x0000 | 0x0047 |
| 0x2C3B | 0x0000 | 0x0000 | 0x0000 | 0x0048 |
| 0x2C3C | 0x0000 | 0x0000 | 0x0000 | 0x0048 |
| 0x2C3D | 0x004B | 0x004A | 0x0000 | 0x0049 |
| 0x2C3E | 0x004B | 0x004A | 0x0000 | 0x0049 |
| 0x2C3F | 0x0000 | 0x0000 | 0x0017 | 0x0015 |
| 0x2C40 | 0x0000 | 0x0000 | 0x0017 | 0x0015 |
| 0x2C41 | 0x0000 | 0x0000 | 0x004D | 0x004C |
| 0x2C42 | 0x0000 | 0x0000 | 0x004D | 0x004C |
| 0x2C6A | 0x004E | 0x0000 | 0x0000 | 0x0000 |
| 0x2C6B | 0x0000 | 0x0000 | 0x0050 | 0x004F |
| 0x2C6C | 0x0000 | 0x0000 | 0x0050 | 0x004F |
| 0x2C6D | 0x0051 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C6E | 0x0051 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C73 | 0x0000 | 0x0000 | 0x0000 | 0x0015 |
| 0x2C74 | 0x0000 | 0x0000 | 0x0000 | 0x0015 |
| 0x2C75 | 0x0000 | 0x0000 | 0x0017 | 0x0000 |
| 0x2C76 | 0x0000 | 0x0000 | 0x0017 | 0x0000 |
| 0x2C77 | 0x0000 | 0x0016 | 0x0000 | 0x0000 |
| 0x2C78 | 0x0000 | 0x0016 | 0x0000 | 0x0000 |
| 0x2C7B | 0x0054 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C7C | 0x0054 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C7E | 0x0000 | 0x0000 | 0x0045 | 0x0044 |
| 0x2C7F | 0x0000 | 0x0000 | 0x0045 | 0x0044 |
| 0x2C92 | 0x0000 | 0x0000 | 0x00CA | 0x00D0 |
| 0x2C93 | 0x0000 | 0x0000 | 0x00CA | 0x00D0 |
| 0x2C9C | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2C9D | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2C9E | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2C9F | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2CA6 | 0x0000 | 0x0057 | 0x0056 | 0x0055 |
| 0x2CA7 | 0x0000 | 0x0057 | 0x0056 | 0x0055 |
| 0x2CA8 | 0x0000 | 0x0000 | 0x0000 | 0x0058 |
| 0x2CA9 | 0x0000 | 0x0000 | 0x0000 | 0x0058 |
| 0x2CEC | 0x0000 | 0x0000 | 0x0000 | 0x0059 |
| 0x2CED | 0x0000 | 0x0000 | 0x0000 | 0x005A |
| 0x2CEE | 0x0000 | 0x0000 | 0x0000 | 0x005B |
| 0x2CEF | 0x0000 | 0x005C | 0x0000 | 0x0000 |
| 0x2CF6 | 0x005D | 0x0000 | 0x0000 | 0x0000 |
| 0x2CF7 | 0x005E | 0x0000 | 0x0000 | 0x0000 |
| 0x2CF9 | 0x0000 | 0x0000 | 0x0017 | 0x003D |
| 0x2CFA | 0x0000 | 0x0000 | 0x005F | 0x0015 |
| 0x2CFB | 0x0062 | 0x0061 | 0x0063 | 0x0060 |
| 0x2D06 | 0x0000 | 0x0000 | 0x0069 | 0x0068 |
| 0x2D07 | 0x006A | 0x0000 | 0x0000 | 0x0000 |
| 0x2D09 | 0x0000 | 0x006B | 0x0000 | 0x0000 |
| 0x2D0F | 0x0000 | 0x0000 | 0x005F | 0x0015 |
| 0x2D1B | 0x0000 | 0x0000 | 0x005F | 0x0015 |
| 0x2D1C | 0x0000 | 0x0000 | 0x005F | 0x0015 |
| 0x2D1D | 0x006C | 0x0000 | 0x0000 | 0x0000 |
| 0x2D1E | 0x006D | 0x0000 | 0x0000 | 0x0000 |
| 0x2D1F | 0x006E | 0x0000 | 0x0000 | 0x0000 |
| 0x2D20 | 0x006F | 0x0000 | 0x0000 | 0x0000 |
| 0x2D29 | 0x0000 | 0x0000 | 0x00D2 | 0x00D1 |
| 0x2D50 | 0x0000 | 0x0072 | 0x0071 | 0x0070 |
| 0x2D51 | 0x0000 | 0x0000 | 0x0073 | 0x0019 |
| 0x2D52 | 0x0074 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D53 | 0x0074 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D54 | 0x0019 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D55 | 0x0074 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D56 | 0x0000 | 0x0000 | 0x0076 | 0x0075 |
| 0x2D57 | 0x0078 | 0x0079 | 0x0000 | 0x0077 |
| 0x2D58 | 0x007B | 0x007D | 0x007C | 0x007A |
| 0x2D59 | 0x0019 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D5A | 0x0019 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D5C | 0x0074 | 0x0000 | 0x0000 | 0x0000 |
| 0x2DB5 | 0x0019 | 0x0000 | 0x0000 | 0x0000 |
| 0x2DB6 | 0x0082 | 0x0000 | 0x0000 | 0x0000 |
| 0x2DB7 | 0x0083 | 0x0000 | 0x0000 | 0x0000 |
| 0x2DBE | 0x0000 | 0x0000 | 0x0085 | 0x0084 |
| 0x2DC0 | 0x0072 | 0x0000 | 0x0000 | 0x0086 |
| 0x2DC6 | 0x0088 | 0x0000 | 0x0000 | 0x0000 |
| 0x2DC8 | 0x0000 | 0x0089 | 0x0000 | 0x0000 |
| 0x2DC9 | 0x008B | 0x0089 | 0x008A | 0x0000 |
| 0x2DCC | 0x0000 | 0x0089 | 0x0000 | 0x0000 |
| 0x2DCD | 0x0000 | 0x0089 | 0x0000 | 0x0000 |
| 0x2DCE | 0x0000 | 0x0089 | 0x0000 | 0x0000 |
| 0x2DD0 | 0x0000 | 0x0089 | 0x0000 | 0x0000 |
| 0x2DD1 | 0x0000 | 0x0089 | 0x0000 | 0x0000 |
| 0x2DD2 | 0x0000 | 0x0089 | 0x0000 | 0x0000 |
| 0x2DD3 | 0x008C | 0x0089 | 0x008A | 0x0000 |
| 0x2DE0 | 0x0000 | 0x008D | 0x0000 | 0x0000 |
| 0x2E18 | 0x0000 | 0x0000 | 0x0094 | 0x0000 |
| 0x2E19 | 0x0000 | 0x0000 | 0x0095 | 0x0000 |
| 0x2E1A | 0x0000 | 0x0000 | 0x0096 | 0x0000 |
| 0x2E1B | 0x0000 | 0x0000 | 0x0097 | 0x0000 |
| 0x2E1C | 0x0000 | 0x0000 | 0x0098 | 0x0000 |
| 0x2E1D | 0x0000 | 0x0000 | 0x0099 | 0x0000 |
| 0x2E24 | 0x0000 | 0x0000 | 0x0000 | 0x009A |
| 0x2E25 | 0x0000 | 0x0000 | 0x0000 | 0x009A |
| 0x2E26 | 0x0000 | 0x0000 | 0x0000 | 0x009A |
| 0x2E27 | 0x0000 | 0x0000 | 0x0000 | 0x009A |
| 0x2E28 | 0x0000 | 0x0000 | 0x0000 | 0x009A |
| 0x2E29 | 0x0000 | 0x0000 | 0x0000 | 0x009A |
| 0x2E30 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2E31 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2E32 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2E33 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2E34 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2E35 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2E68 | 0x0019 | 0x0000 | 0x009C | 0x009B |
| 0x2E69 | 0x0019 | 0x0000 | 0x009C | 0x009D |
| 0x2E6A | 0x0019 | 0x0000 | 0x009C | 0x009D |
| 0x2E77 | 0x0000 | 0x009E | 0x0000 | 0x0000 |
| 0x2E7C | 0x0000 | 0x004D | 0x0000 | 0x0000 |
| 0x2E81 | 0x0000 | 0x0000 | 0x0000 | 0x00D3 |
| 0x2E82 | 0x0000 | 0x00D5 | 0x008E | 0x00D4 |
| 0x2E83 | 0x00D8 | 0x00D7 | 0x0090 | 0x00D6 |
| 0x2E84 | 0x0000 | 0x004D | 0x0000 | 0x0000 |
| 0x2E85 | 0x00D9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E8B | 0x00DC | 0x00DB | 0x0000 | 0x00DA |
| 0x2E8C | 0x00DF | 0x00DE | 0x0000 | 0x00DD |
| 0x2E8D | 0x00E2 | 0x00E1 | 0x0000 | 0x00E0 |
| 0x2E8E | 0x0000 | 0x00A2 | 0x0000 | 0x0000 |
| 0x2E97 | 0x00A1 | 0x00A0 | 0x0000 | 0x0033 |
| 0x2E98 | 0x0000 | 0x00A2 | 0x0000 | 0x0000 |
| 0x2E9F | 0x00A4 | 0x004D | 0x00A5 | 0x00A3 |
| 0x2EA1 | 0x0000 | 0x00A2 | 0x0000 | 0x0000 |
| 0x2EE0 | 0x0000 | 0x0000 | 0x0017 | 0x003D |
| 0x2EE1 | 0x00A6 | 0x0000 | 0x0000 | 0x0000 |
| 0x2EE2 | 0x00A7 | 0x0000 | 0x0000 | 0x0000 |
| 0x2EE3 | 0x00A8 | 0x0000 | 0x0000 | 0x0000 |
| 0x2EEA | 0x0000 | 0x0000 | 0x0017 | 0x003D |
| 0x2EEB | 0x00A9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2EEC | 0x0019 | 0x0000 | 0x0000 | 0x00AA |
| 0x2EF4 | 0x001A | 0x0000 | 0x0000 | 0x0000 |
| 0x2EF5 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2EFE | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2EFF | 0x00AB | 0x0000 | 0x0000 | 0x0000 |
| 0x2F08 | 0x0000 | 0x0000 | 0x0017 | 0x003D |
| 0x2F09 | 0x0019 | 0x0000 | 0x00AC | 0x00AA |
| 0x2F0D | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2F0F | 0x00AB | 0x0000 | 0x0000 | 0x0000 |
| 0x2F12 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2F44 | 0x00AF | 0x00AE | 0x00B0 | 0x00AD |
| 0x2F45 | 0x00B3 | 0x00B2 | 0x00B1 | 0x0000 |
| 0x2F46 | 0x0000 | 0x00B5 | 0x00B6 | 0x00B4 |
| 0x2F47 | 0x0000 | 0x0000 | 0x00B7 | 0x00B7 |
| 0x2F4E | 0x0000 | 0x0029 | 0x0000 | 0x0000 |
| 0x2F4F | 0x0019 | 0x0000 | 0x0000 | 0x0000 |
| 0x2F58 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2F63 | 0x0019 | 0x0000 | 0x0000 | 0x0000 |
| 0x2F64 | 0x0019 | 0x0000 | 0x0000 | 0x0000 |
| 0x2F65 | 0x00E3 | 0x0000 | 0x0000 | 0x0000 |
| 0x2F66 | 0x0000 | 0x00CB | 0x00CA | 0x00C9 |
| 0x2F67 | 0x0000 | 0x0000 | 0x0017 | 0x003D |
| 0x2F71 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2F76 | 0x0000 | 0x0000 | 0x0017 | 0x003D |
| 0x2F77 | 0x0000 | 0x0000 | 0x00AC | 0x00AA |
| 0x2F7B | 0x0000 | 0x0016 | 0x0000 | 0x0000 |
| 0x2F80 | 0x0019 | 0x00B8 | 0x0000 | 0x0000 |
| 0x2F85 | 0x0000 | 0x0000 | 0x0017 | 0x003D |
| 0x2F8F | 0x00B9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2F94 | 0x0000 | 0x0016 | 0x0017 | 0x0015 |
| 0x2F99 | 0x0019 | 0x0000 | 0x0000 | 0x0000 |
| 0x2F9A | 0x0000 | 0x00BA | 0x0000 | 0x0000 |
| 0x2F9E | 0x0019 | 0x0029 | 0x00BB | 0x0000 |
| 0x2FA3 | 0x00BD | 0x00BC | 0x0000 | 0x0000 |
| 0x2FA4 | 0x00BF | 0x00BE | 0x0000 | 0x0000 |
| 0x2FC6 | 0x0000 | 0x00C1 | 0x00C2 | 0x00C0 |
| 0x2FDA | 0x00E4 | 0x0000 | 0x0000 | 0x0000 |
| 0x2FDB | 0x0000 | 0x00CB | 0x00CA | 0x00C9 |
| 0xCD87 | 0x00C4 | 0x00C3 | 0x0000 | 0x0000 |
| 0xCD8B | 0x0000 | 0x00C3 | 0x0000 | 0x0000 |
| 0xCD8F | 0x00C4 | 0x00C3 | 0x0000 | 0x0000 |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 230 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb Schwelle |
| 0x0002 | Signal oder Wert unterhalb Schwelle |
| 0x0003 | mit Kraftstoffabschaltung |
| 0x0004 | kein Signal oder Wert |
| 0x0005 | Abgasschädigend nach Startvorgang |
| 0x0006 | Abgasschädigend |
| 0x0007 | Verbrennungsaussetzer an mehreren Zylindern |
| 0x0008 | unplausibles Signal oder Wert |
| 0x0009 |  Tankfüllstand zu gering |
| 0x000A | Segmentadaption am  Anschlag |
| 0x000B | Zahnfehler Kurbelwellengeber |
| 0x000C | Wirkungsgrad unter Schwellwert |
| 0x000D | Sekundärluftventil oder -schlauch blockiert |
| 0x000E | Sekundärluftmasse zu gering |
| 0x000F | Grobe Undichtigkeit zwischen Sekundärluftpumpe und -Ventil |
| 0x0010 | Sekundärluftpumpe nicht aktiv |
| 0x0011 | Sekundärluftmenge zu gering Bank 1 |
| 0x0012 | Sekundärluftmenge zu gering Bank 2 |
| 0x0013 | Sekundärluftmenge zu gering Bank 1 und Bank 2 |
| 0x0014 | Klemmt offen |
| 0x0015 | Kurzschluss nach Plus |
| 0x0016 | Leitungsunterbrechung |
| 0x0017 | Kurzschluss nach Minus |
| 0x0018 | Leitungsunterbrechung  |
| 0x0019 | Signal unplausibel |
| 0x001A | klemmt offen |
| 0x001B | Leckage grösser 1,0 mm |
| 0x001C | Leckage grösser 0,5 mm |
| 0x001D | obere Schwelle Pumpenstrom bei Referenzmessung |
| 0x001E | Abbruch wegen Stromschwankungen bei Feinleckprüfung |
| 0x001F | Pumpenstromschwelle bei Ventilprüfung erreicht |
| 0x0020 | untere Schwelle Pumpenstrom bei Referenzmessung |
| 0x0021 | kurzschluss nach Plus |
| 0x0022 | Funktionstest Bandende |
| 0x0023 | Funktionstest |
| 0x0024 | nicht korrekt geschlossen |
| 0x0025 | Füllstandssignalwert zum Verbrauchswert unplausibel |
| 0x0026 | Gemisch zu mager |
| 0x0027 | Gemisch zu fett |
| 0x0028 | schwergängig, klemmt mechanisch |
| 0x0029 | Signal fehlt |
| 0x002A | Synchronisation |
| 0x002B | Zahnfehler |
| 0x002C | Zahnzeitfehler |
| 0x002D | Wert außerhalb Referenzbereich |
| 0x002E | Zahnsprung |
| 0x002F | Signal ungültig für Synchronisation |
| 0x0030 | Segmentzeit |
| 0x0031 | Notabschaltung |
| 0x0032 | Drehzahl zu hoch |
| 0x0033 | Übertemperatur |
| 0x0034 | Drehzahl zu niedrig |
| 0x0035 | Notlauf |
| 0x0036 | interner RAM-Baustein |
| 0x0037 | Sicherheitsrechner RAM |
| 0x0038 | Bootsoftware |
| 0x0039 | Datenbereich |
| 0x003A | Applikationssoftware |
| 0x003B | RAM-Überprüfung |
| 0x003C | Timeout SPI Bus |
| 0x003D | Kurzschluss nach Plus oder Leitungsunterbrechung |
| 0x003E | nicht abgefallen |
| 0x003F | nicht angezogen  |
| 0x0040 | schaltet zu spät |
| 0x0041 | Fehlerverwaltung Getriebe |
| 0x0042 | vertauschte Lambdasonden vor Katalysator |
| 0x0043 | Signal während Schubabschaltung unterhalb Schwelle |
| 0x0044 | Abgas nach Katalysator zu fett |
| 0x0045 | Abgas nach Katalysator zu mager |
| 0x0046 | Heiztakteinkopplung auf Signal |
| 0x0047 | Signalamplitude zu gering |
| 0x0048 | Sonde nicht angesteckt |
| 0x0049 | Unterbrechung Nernstleitung |
| 0x004A | Unterbrechung Pumpstrompfad oder virtuelle Masse |
| 0x004B | Unterbrechung Abgleichsleitung |
| 0x004C | Initialisierungsfehler |
| 0x004D | Kommunikationsfehler |
| 0x004E | vertauschte Lambdasonden nach Katalysator |
| 0x004F | Signal magerer als erwartet |
| 0x0050 | Signal fetter als erwartet |
| 0x0051 | Sondensignal zu träge |
| 0x0052 | Signal nicht plausibel |
| 0x0053 | Sondensignal zu träge nach Schubphase |
| 0x0054 | Signal während Schubabschaltung  oberhalb Schwelle |
| 0x0055 | Arbeitstemperatur Sonde nicht erreicht |
| 0x0056 | Betriebsbereitschaft Sonde zu spät erreicht |
| 0x0057 | Sondentemperatur  ungültig |
| 0x0058 | Innenwiderstand des Signalkreises zu hochohmig |
| 0x0059 | klemmt kurzzeitig |
| 0x005A | klemmt dauerhaft |
| 0x005B | schwergängig zu langsam |
| 0x005C | Ansteuerung fehlerhaft |
| 0x005D | Poti 1 unplausibel zu MAF |
| 0x005E | Poti 2 unplausibel zu MAF |
| 0x005F | Kurzschluss nach Minus oder Leitungsunterbrechung |
| 0x0060 | Randbedingungen verletzt |
| 0x0061 | Federtest und Notluftprüfung verfehlt  |
| 0x0062 | unteren Anschlag lernen während Urinitialisierung abgebrochen |
| 0x0063 | Notluftpunkt nicht adaptiert |
| 0x0064 | Federtest |
| 0x0065 | Notluftprüfung |
| 0x0066 | Neuadaption erforderlich |
| 0x0067 | unterer Anschlag nicht gelernt |
| 0x0068 | Messwert HFM zu hoch |
| 0x0069 | Messwert HFM zu niedrig |
| 0x006A | Plausibilitaet zwischen Poti 1 und 2 verletzt |
| 0x006B | Luftzufuhr nicht korrekt |
| 0x006C | Spannungsregler 1 |
| 0x006D | Spannungsregler 2 |
| 0x006E | Doppelfehler |
| 0x006F | Gleichlauffehler |
| 0x0070 | Momentenanforderung vom Tempomat trotz Bremssignal |
| 0x0071 | Momentenanforderung vom ACC/DCC unplausibel |
| 0x0072 | Momentenanforderung vom LDM unplausibel |
| 0x0073 | Drosselklappenstellung unplausibel |
| 0x0074 | defekt |
| 0x0075 | Anforderung I-Anteil unplausibel |
| 0x0076 | Anforderung PD-Anteil unplausibel |
| 0x0077 | Anforderung MSR unplausibel |
| 0x0078 | Anforderung EGS unplausibel |
| 0x0079 | Anforderung AMT unplausibel |
| 0x007A | maximales Kupplungsmoment unplausibel |
| 0x007B | Sporttastersignal unplausibel |
| 0x007C | minimales Kupplungsmoment unplausibel |
| 0x007D | Verlustmoment unplausibel |
| 0x007E | Software |
| 0x007F | SPI-Fehler |
| 0x0080 | Hardware |
| 0x0081 | Sicherheitsabschaltung |
| 0x0082 | Schalter defekt |
| 0x0083 | Toggle-Bit |
| 0x0084 | irreversibel aus |
| 0x0085 | reversibel aus |
| 0x0086 | Momentenanforderung vom LDM trotzt Bremssignal |
| 0x0087 | CAS-Fehler |
| 0x0088 | CAN Wert unplausibel |
| 0x0089 | kein Signal |
| 0x008A | ALIVE-Fehler |
| 0x008B | Prüfsumme |
| 0x008C | Checksumme |
| 0x008D | Timeout |
| 0x008E | Überspannung |
| 0x008F | batterieloser Betrieb |
| 0x0090 | Unterspannung |
| 0x0091 | Tiefentladung |
| 0x0092 | Powermanagement |
| 0x0093 | Ruhestromverletzung |
| 0x0094 | Zündzeit Zylinder 1 zu gering |
| 0x0095 | Zündzeit Zylinder 2 zu gering |
| 0x0096 | Zündzeit Zylinder 3 zu gering |
| 0x0097 | Zündzeit Zylinder 4 zu gering |
| 0x0098 | Zündzeit Zylinder 5 zu gering |
| 0x0099 | Zündzeit Zylinder 6 zu gering |
| 0x009A | Zündkreisüberwachung |
| 0x009B | Motor mechanisch zu laut  |
| 0x009C | Motor mechanisch zu leise |
| 0x009D | Motor mechanisch zu laut |
| 0x009E | Spannungsversorgung fehlt |
| 0x009F | Startphase |
| 0x00A0 | Elektrisch |
| 0x00A1 | Mechanisch |
| 0x00A2 | keine Kommunikation über BSD-Schnittstelle |
| 0x00A3 | Temperaturmessung |
| 0x00A4 | Permittivitätsmessung |
| 0x00A5 | Niveaumessung  |
| 0x00A6 | unplausibel bezüglich Lambdaregelung |
| 0x00A7 | Temperatursignal konstant |
| 0x00A8 | Temperaturgradient zu steil |
| 0x00A9 | Temperaturgradient zu hoch |
| 0x00AA | Signal oberhalb Schwelle |
| 0x00AB | Mechanischer- oder Hardwaredefekt |
| 0x00AC | Signal unterhalb Schwelle |
| 0x00AD | 1. Startwert im Flash zerstört. 2- aus 3-Auswahl fehlgeschlagen oder 2. Fehlerrückmeldung: Startwertprogrammierroutine |
| 0x00AE | Fehler beim Programmieren oder rücksetzen des Startwertes |
| 0x00AF | Falsche EWS-Telegramme empfangen. Die Fangbereichsrechnung ist für mindestens 5 Telegrammauswertungen fehlgeschlagen. |
| 0x00B0 | kein Startwert programmiert |
| 0x00B1 | Empfangsfehler des EWS-Telegramms (Start-, Stopbit- oder Framefehler) |
| 0x00B2 | Timeoutfehler: 10 Sekunden nach Kl.15 EIN noch kein EWS-Telegramm empfangen, evtl. Leitungsunterbrechung oder Kurzschluss nach Minus |
| 0x00B3 | Mehr als 3 Parity-Fehler erkannt |
| 0x00B4 | Lesefehler im EEPROM: Wechselcode Ablage |
| 0x00B5 | Schreibfehler im EEPROM: Wechselcode Ablage |
| 0x00B6 | Fehler Ablage |
| 0x00B7 | Steuergerät defekt |
| 0x00B8 | Timeout (Ungültigkeitswert vom Kombi) |
| 0x00B9 | Pedalwert zu Bremspedal |
| 0x00BA | Signalfehler |
| 0x00BB | Oelniveau zu niedrig |
| 0x00BC | Codierdaten im EEPROM fehlerhaft |
| 0x00BD | keine Codierung erfolgt (nach Programmierung) |
| 0x00BE | CAN Timeout |
| 0x00BF | Variantenüberwachung |
| 0x00C0 | Fertigungsmodus |
| 0x00C1 | Werkstattmodus |
| 0x00C2 | Transportmodus |
| 0x00C3 | CAN Bus off |
| 0x00C4 | CAN Baustein im Zustand passiv |
| 0x00C5 | Timeout  |
| 0x00C6 | Aktualisierungszähler inkrementiert nicht (Alive-Zähler) |
| 0x00C7 | Prüfsumme ungleich errechnetem Wert |
| 0x00C8 | kein Druck im Vanoshydrauliksystem |
| 0x00C9 | Kurzschluss nach Batterie Plus |
| 0x00CA | Kurzschluss nach Masse |
| 0x00CB | Unterbrechung |
| 0x00CC | Unterbrechung / Kurzschluss |
| 0x00CD | Nockenwellen- zur Kurbelwellenposition außerhalb Referenzbereich |
| 0x00CE | Integrierte Momentenreserve nicht erreicht |
| 0x00CF | Kurzschluss zu Batterie Plus |
| 0x00D0 | Kurzschluss nach Batterie Plus / Unterbrechung |
| 0x00D1 | IST Wert zu hoch |
| 0x00D2 | IST Wert zu niedrig |
| 0x00D3 | Drehzahl außerhalb der Toleranz |
| 0x00D4 | interne Temperatur zu hoch |
| 0x00D5 | Überstrom |
| 0x00D6 | Trockenlauf |
| 0x00D7 | Temperaturschwelle 1 überschritten |
| 0x00D8 | Temperaturschwelle 2 überschritten |
| 0x00D9 | keine Spannung am Notlauf-Eingang der Pumpe |
| 0x00DA | EBSD-Fehler |
| 0x00DB | BSD-Fehler |
| 0x00DC | Software-Fehler |
| 0x00DD | Temperatur |
| 0x00DE | Spannung |
| 0x00DF | Strom |
| 0x00E0 | Wakeupleitung Masseschluss |
| 0x00E1 | Systemfehler |
| 0x00E2 | Wakeupleitung Pegel unplausibel |
| 0x00E3 | Saugstrahlpumpe (Servo) defekt |
| 0x00E4 | Kurbelgehäuseentlüftung defekt |
| 0xFFFF | unbekannte Fehlerart |

<a id="table-messwertetab"></a>
### MESSWERTETAB

Dimensions: 444 rows × 12 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ITANS | 0x4200 | STAT_ANSAUGLUFTTEMPERATUR_WERT | Ansauglufttemperatur 1 | °C | TIA | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x4201 | STAT_0x4201_WERT | Umgebungsdruck | hPa | AMP_MES | - | unsigned integer | - | 0,0829175263643265 | 1 | 0,0 |
| ILMKG | 0x4203 | STAT_LUFTMASSE_WERT | Massenstrom vom HFM | kg/h | MAF_KGH_MES | - | unsigned integer | - | 0,03125 | 1 | 0,0 |
| ITUMG | 0x4204 | STAT_UMGEBUNGSTEMPERATUR_WERT | Umgebungstemperatur | °C | TAM | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| ITKUM | 0x4300 | STAT_KUEHLMITTELTEMPERATUR_WERT | Kühlwassertemperatur | °C | TCO | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x4301 | STAT_0x4301_WERT | Kühlerauslasstemperatur | °C | TCO_2 | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| IMLOE | 0x4400 | STAT_OELSTAND_LANGZEIT_MITTEL_WERT | Ölstand Mittelwert Langzeit | - | OZ_NIVLANGT | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| IFSOE | 0x4401 | STAT_FUELLSTAND_MOTOROEL_WERT | Füllstand Motoröl | - | OZ_LP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ITOEL | 0x4402 | STAT_OELTEMPERATUR_WERT | Öltemperatur | °C | TOEL | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| IKVLS | 0x4403 | STAT_KRAFTSTOFFVERBRAUCH_SEIT_SERVICE_WERT | Kraftstoff-Verbrauch seit letztem Service | - | OZ_KVBSM_UL | - | unsigned long | - | 1,220703125E-4 | 1 | 0,0 |
| IKMLS | 0x4404 | STAT_WEG_SEIT_SERVICE_WERT | km seit letztem Service | km | OZ_OELKM | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| RNIOE | 0x4405 | STAT_OELSENSOR_NIVEAU_ROH_WERT | Ölsensor Niveau Rohwert | - | OZ_NIVR | - | unsigned char | - | 1,0 | 1 | 0,0 |
| RQUOE | 0x4406 | STAT_OELSENSOR_QUALITAET_ROH_WERT | Ölsensor Qualität Rohwert | - | OZ_PERMR | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| RTOEL | 0x4407 | STAT_OELSENSOR_TEMPERATUR_ROH_WERT | Ölsensor Temperatur Rohwert | - | OZ_TEMPR | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ITSOE | 0x4408 | STAT_OELSENSOR_TEMPERATUR_WERT | Ölsensor Temperatur | °C | OZ_TEMPAKT | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| INIOE | 0x4409 | STAT_OELSENSOR_NIVEAU_WERT | Ölsensor Niveau | - | OZ_NIVAKT | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| IQOEL | 0x440A | STAT_OELSENSOR_QUALITAET_WERT | Ölsensor Qualität | - | OZ_PERMAKT | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| - | 0x440B | STAT_0x440B_WERT | Länderfaktor 1 codiert | - | OZ_LF1C | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| - | 0x440C | STAT_0x440C_WERT | Länderfaktor 2 codiert | - | OZ_LF2C | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| - | 0x440D | STAT_0x440D_WERT | Länderfaktor 1 | - | OZ_LF1T | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| - | 0x440E | STAT_0x440E_WERT | Länderfaktor 2 | - | OZ_LF2T | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| - | 0x440F | STAT_0x440F_WERT | Kurzmittelwert-Niveau für den Tester | - | OZ_NIVKRZT | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| - | 0x4410 | STAT_0x4410_WERT | Restweg aus Permittivität abgeleitet | km | OZ_RWPERM | - | signed integer | - | 10,0 | 1 | 0,0 |
| - | 0x4411 | STAT_0x4411_WERT | Restweg aus Kraftstoffverbrauch abgeleitet | km | OZ_RWKVB | - | signed integer | - | 10,0 | 1 | 0,0 |
| - | 0x4412 | STAT_0x4412_WERT | Öl-Alter in Monate | - | OZ_OELZEIT | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x4413 | STAT_0x4413_WERT | aufbereitete Permittivität bei letztem Ölwechsel | - | OZ_PERMLOW | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| - | 0x4414 | STAT_0x4414_WERT | Permittivität für Bewertung aufbereitet (extrapoliert) | - | OZ_PERMEX | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| - | 0x4415 | STAT_0x4415_WERT | Offset für Permittivitätskorrektur | - | OZ_PERMOFF | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| - | 0x4416 | STAT_0x4416_WERT | zugeteilte Bonuskraftstoffmenge | - | OZ_KVBOG | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x4417 | STAT_0x4417_WERT | zugeteilter Permittivitätsbonus | - | OZ_PERMBOG | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| - | 0x4419 | STAT_0x4419_WERT | Statusinformation vom Ölzustandssensor | - | OZ_STATUS | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x441A | STAT_0x441A_WERT | Statuswort mit Biteingangsgroessen OZ | - | OZ_STATUS | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x441B | STAT_0x441B_WERT | QLT-Kommunikation iO (Statuswort St_qlt_ok, Bit0) | 0/1 | B_QLT_OK | - | 0xFF | - | 1 | 1 | 0 |
| SSPEI | 0x4505 | STAT_VVT_EINLASSSPREIZUNG_SOLL_WERT | Sollwert Einlassspreizung | °CRK | CAM_SP_IVVT_IN | - | unsigned char | - | 0,375 | 1 | 59,9999982118607 |
| IPNWE | 0x4506 | STAT_POSITION_NOCKENWELLE_EINLASS_WERT | Nockenwellenposition Einlass | °CRK | PSN_CAM_IN_1 | - | unsigned integer | - | 0,375 | 1 | -95,9999971389771 |
| IPNWA | 0x4507 | STAT_POSITION_NOCKENWELLE_AUSLASS_WERT | Nockenwellenposition Auslass | °CRK | PSN_CAM_EX_1 | - | unsigned integer | - | 0,375 | 1 | -95,9999971389771 |
| ISNWE | 0x4508 | STAT_NW_EINLASSSPREIZUNG_WERT | Istwert Einlassspreizung | °CRK | CAM_IN[1] | - | unsigned char | - | 0,375 | 1 | 59,9999982118607 |
| ISNWA | 0x4509 | STAT_NW_AUSLASSSPREIZUNG_WERT | Istwert Auslassspreizung | °CRK | CAM_EX[1] | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| NSNWA | 0x450A | STAT_NW_NORMSPREIZUNG_AUSLASS_WERT | Normspreizung Auslass | °CRK | CAM_SP_REF_EX | - | signed integer | - | 0,0234375 | 1 | 0,0 |
| NSNWE | 0x450B | STAT_NW_NORMSPREIZUNG_EINLASS_WERT | Normspreizung Einlass | °CRK | CAM_SP_REF_IN | - | signed integer | - | 0,0234375 | 1 | 0,0 |
| IWDKL | 0x4600 | STAT_DROSSELKLAPPENWINKEL_WERT | aktueller Drosselklappenwinkel | °TPS | TPS_AV | - | unsigned integer | - | 0,00729414634406567 | 1 | 0,0 |
| SWDKL | 0x4601 | STAT_DROSSELKLAPPENWINKEL_SOLL_WERT | Drosselklappe Sollwert | °TPS | TPS_SP_MDL | - | unsigned integer | - | 0,00729414634406567 | 1 | 0,0 |
| SUGEB | 0x4602 | STAT_GENERATOR_SPANNUNG_BSD_SOLL_WERT | Generator Sollspannung über BSD | V | V_ALTER_SP | - | unsigned long | - | 0,100000001490116 | 1 | 10,6 |
| ITGEE | 0x4603 | STAT_GENERATOR_ELEKTRONIKTEMPERATUR_WERT | Chiptemperatur Generator 1 | °C | TCHIP | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| IIGEN | 0x4604 | STAT_GENERATOR_STROM_WERT | Generator Strom | - | I_GEN | - | unsigned char | - | 1,0 | 1 | 0,0 |
| VGENE | 0x4605 | STAT_GENERATOR_CHIPVERSION_WERT | Chipversion Generator 1 | - | BSDGENCV | - | unsigned char | - | 1,0 | 1 | 0,0 |
| VGENR | 0x4606 | STAT_GENERATOR_REGLERVERSION_WERT | Reglerversion Generator 1 | - | BSDGENREGV | - | unsigned char | - | 1,0 | 1 | 0,0 |
| VGENH | 0x4607 | STAT_GENERATOR_HERSTELLERCODE_WERT | Herstellercode Generator 1 | - | GEN_MANUFAK | - | unsigned char | - | 1,0 | 1 | 0,0 |
| VGTYP | 0x4608 | STAT_GENERATOR_TYP_WERT | Kennung Generatortyp Generator 1 | - | GEN_TYPKENN | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IUK87 | 0x4609 | STAT_KL87_SPANNUNG_WERT | Kl.87 Spannung / Versorgung DME | V | VB | - | unsigned char | - | 0,101562492549419 | 1 | 0,0 |
| IUBAT | 0x460A | STAT_UBATT_WERT | Batteriespannung aktuell | V | UBT | - | unsigned integer | - | 0,0149999996647239 | 1 | 0,0 |
| IUIBS | 0x460B | STAT_UBATT_IBS_WERT | Batteriespannung von IBS gemessen | - | U_BATT | - | unsigned integer | - | 2,50000011874363E-4 | 1 | 6,0 |
| IUADW | 0x460C | STAT_UBATT_AD_WANDLER_WERT | Batteriespannung vom AD-Wandler DME | V | VB_BAS | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| - | 0x460D | STAT_0x460D_WERT | Korrekturwert Abschaltung | - | ABSCH_KORR | - | signed integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x460E | STAT_0x460E_WERT | Abstand zur Startfähigkeitsgrenze | - | D_SOC | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| ILBAT | 0x460F | STAT_BATTERIELAST_WERT | Batterielast | % | LOAD_BAT | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STELU | 0x4611 | STAT_E_LUEFTER_PWM_SOLL_WERT | Sollwert E-Lüfter als PWM Wert | % | N_PERC_ECF | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x4612 | STAT_0x4612_WERT | Erregerstrom Generator 1 | A | IERR | - | unsigned char | - | 0,125 | 1 | 0,0 |
| - | 0x4613 | STAT_0x4613_WERT | Kopierter Wert von zum Generator gesendeter Sollspannung Generator 1 | V | U_FGEN | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| - | 0x4614 | STAT_0x4614_WERT | Auslastungsgrad Generator 1 | % | DFSIGGEN | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x4615 | STAT_0x4615_WERT | Kopie begrenzter Erregerstrom Generator 1 | A | IERRFGRENZ | - | unsigned char | - | 0,125 | 1 | 0,0 |
| - | 0x4616 | STAT_0x4616_WERT | Kopie Generator 1 LR Vorgabe auf Bus gelegt | s | TLRFGEN | - | unsigned char | - | 0,100000001490116 | 1 | 0,0 |
| - | 0x4617 | STAT_0x4617_WERT | gefiltertes Generatormoment absolut Ausgang | Nm | MD_GENNM | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| - | 0x4618 | STAT_0x4618_WERT | Kopie Drehzahlschwelle für LR-Funktion Generator 1 aktiv | 0/1 | B_LRFOFF | - | 0xFF | - | 1 | 1 | 0 |
| ISBV1 | 0x4700 | STAT_SONDENBEREITSCHAFT_VORKAT_BANK1 | Status Lambdasonde betriebsbereit vor Katalysator Bank 1 | 0/1 | LV_INH_LSCL[1] | - | 0xFF | - | 1 | 1 | 0 |
| ISBV2 | 0x4701 | STAT_SONDENBEREITSCHAFT_VORKAT_BANK2 | Status Lambdasonde betriebsbereit vor Katalysator Bank 2 | 0/1 | LV_INH_LSCL[2] | - | 0xFF | - | 1 | 1 | 0 |
| IUSO1 | 0x4702 | STAT_SONDENSPANNUNG_VORKAT_BANK1_MIT_OFFSET_WERT | Spannung Lambdasonde vor Katalysator Bank 1 mit Offsetkorrektur | V | VLS_COR_LSL[1] | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUSO2 | 0x4703 | STAT_SONDENSPANNUNG_VORKAT_BANK2_MIT_OFFSET_WERT | Spannung Lambdasonde vor Katalysator Bank 2 mit Offsetkorrektur | V | VLS_COR_LSL[2] | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| SINT1 | 0x4704 | STAT_LAMBDA_BANK1_SOLL_WERT | Lambda Sollwert Bank1 | - | LAMB_BAS[0] | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| SINT2 | 0x4705 | STAT_LAMBDA_BANK2_SOLL_WERT | Lambda Sollwert Bank2 | - | LAMB_BAS[1] | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| ISKUB | 0x4800 | STAT_KUPPLUNGSSCHALTER_BETAETIGT_WERT | Kupplungsschalter Status | 0/1 | LV_CS | - | 0xFF | - | 1 | 1 | 0 |
| ISKUV | 0x4801 | STAT_KUPPLUNGSSCHALTER_VORHANDEN_WERT | Kupplungsschalter vorhanden | 0/1 | LV_CS_CUS | - | 0xFF | - | 1 | 1 | 0 |
| ISSPO | 0x4802 | STAT_SPORTTASTER_BETAETIGT_WERT | Sporttaster aktiv | 0/1 | LV_SOF_SWI | - | 0xFF | - | 1 | 1 | 0 |
| ISKLI | 0x4803 | STAT_KLIMA_EIN | Status Klima ein | - | STATE_ACIN_CAN | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ISSLP | 0x4804 | STAT_SEKUNDAERLUFTPUMPE_WERT | Sekundärluft Pumpe aktiv | 0/1 | LV_SAP | - | 0xFF | - | 1 | 1 | 0 |
| ISSRC | 0x4805 | STAT_STARTRELAIS_UEBER_CAN_WERT | Startrelais über CAN aktiv | 0/1 | LV_RLY_ST_CAN | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x4806 | STAT_0x4806_WERT | Steuergeräte-Innentemperatur | °C | TECU | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| INMOT | 0x4807 | STAT_MOTORDREHZAHL_WERT | Motor Drehzahl | rpm | N | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| SNLLD | 0x4808 | STAT_LEERLAUFDREHZAHL_SOLL_WERT | Leerlauf Solldrehzahl | rpm | N_SP_IS | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| ISLLA | 0x4809 | STAT_LEERLAUF_AKTIV | Status LL | 0/1 | LV_IS | - | 0xFF | - | 1 | 1 | 0 |
| ISKME | 0x480A | STAT_KILOMETERSTAND_WERT | Kilometerstand Auflösung 1 km | km | CTR_KM_BN | - | unsigned long | - | 1,0 | 1 | 0,0 |
| IFPWG | 0x480B | STAT_FAHRERWUNSCH_PEDAL_WERT | Pedalwert Fahrerwunsch in % | % | PV_AV | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5800 | STAT_0x5800_WERT | Zeit nach Start | s | OBD_T_AST | - | unsigned char | - | 256,0 | 1 | 0,0 |
| - | 0x5801 | STAT_0x5801_WERT | Umgebungsdruck | kPa | OBD_AMP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ICLR1 | 0x5802 | STAT_LAMBDAREGELUNG_ZUSTAND_BANK1_WERT | Zustand Lambdaregelung Bank 1 | 0-n | STATE_LS[1] | - | 0xFF | _CNV_S_5_LACO_RANGE_694 | 1 | 1 | 0 |
| ICLR2 | 0x5803 | STAT_LAMBDAREGELUNG_ZUSTAND_BANK2_WERT | Zustand Lambdaregelung Bank 2 | 0-n | STATE_LS[2] | - | 0xFF | _CNV_S_5_LACO_RANGE_694 | 1 | 1 | 0 |
| SLAST | 0x5804 | STAT_LASTWERT_BERECHNET_WERT | Berechneter Lastwert | % | LOAD_CLC | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5805 | STAT_0x5805_WERT | Kühlmitteltemperatur OBD | °C | OBD_TCO | - | unsigned char | - | 1,0 | 1 | -40,0 |
| ILIN1 | 0x5806 | STAT_LAMBDA_INTEGRATOR_GRUPPE1_WERT | Lambda Integrator Gruppe 1 | % | OBD_LAM_COR[1] | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| ILAM1 | 0x5807 | STAT_LAMBDA_ADAPTION_MULTIPLIKATIV_GRUPPE1_WERT | Lambda Adaption Summe mul. und add. Gruppe 1 | % | OBD_LAM_AD[1] | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| ILIN2 | 0x5808 | STAT_LAMBDA_INTEGRATOR_GRUPPE2_WERT | Lambda Integrator Gruppe 2 | % | OBD_LAM_COR[2] | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| ILAM2 | 0x5809 | STAT_LAMBDA_ADAPTION_MULTIPLIKATIV_GRUPPE2_WERT | Lambda Adaption Summe mul. und add. Gruppe 2 | % | OBD_LAM_AD[2] | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| IPKRS | 0x580A | STAT_KRAFTSTOFFDRUCK_WERT | Kraftstoffdruck | kPa | OBD_FUP | - | unsigned char | - | 3,0 | 1 | 0,0 |
| INAUF | 0x580C | STAT_N_AUFLOESUNG_WERT | Drehzahl | rpm | OBD_N | - | unsigned char | - | 64,0 | 1 | 0,0 |
| IVKM2 | 0x580D | STAT_GESCHWINDIGKEIT_2_WERT | Geschwindigkeit | km/h | VS | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IZZY1 | 0x580E | STAT_ZUENDZEITPUNKT_ZYL1_WERT | Zündzeitpunkt Zylinder 1 | °CRK | OBD_IGA_IGC | - | unsigned char | - | 0,5 | 1 | -64,0 |
| ITANL | 0x580F | STAT_ANSAUGLUFTTEMPERATUR_LAW_WERT | Ansauglufttemperatur | °C | OBD_TIA | - | unsigned char | - | 1,0 | 1 | -40,0 |
| ILMGS | 0x5810 | STAT_LUFTMASSE_GRAMM_PRO_SEKUNDE_WERT | Luftdurchsatz OBD | g/s | OBD_MAF | - | unsigned char | - | 2,5599999427795406 | 1 | 0,0 |
| INM32 | 0x5811 | STAT_MOTORDREHZAHL_N32_WERT | Motordrehzahl | rpm | N_32 | - | unsigned char | - | 32,0 | 1 | 0,0 |
| - | 0x5812 | STAT_0x5812_WERT | Luftmasse gemessen | kg/h | MAF_KGH_MES_BAS | - | unsigned char | - | 8,0 | 1 | 0,0 |
| ILREL | 0x5813 | STAT_LASTWERT_RELATIV_WERT | Relative Last | % | RF | - | signed char | - | 2,5599999427795406 | 1 | 0,0 |
| - | 0x5814 | STAT_0x5814_WERT | Fahrpedalwert | % | PV_AV_RAW | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5815 | STAT_0x5815_WERT | Batteriespannung | V | OBD_VB | - | unsigned char | - | 0,2560000121593472 | 1 | 0,0 |
| - | 0x5816 | STAT_0x5816_WERT | Lambda Setpoint | - | OBD_LAMB_SP | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| - | 0x5817 | STAT_0x5817_WERT | Umgebungstemperatur | °C | OBD_TAM | - | unsigned char | - | 1,0 | 1 | -40,0 |
| ILMMG | 0x5818 | STAT_LUFTMASSE_PRO_HUB_WERT | Luftmasse gerechnet | mg/stk | MAF | - | unsigned char | - | 5,425863742828365 | 1 | 0,0 |
| - | 0x5819 | STAT_0x5819_WERT | Drehzahl OBD Byte | rpm | N_SAE_BYTE_KWP | - | unsigned char | - | 64,0 | 1 | 0,0 |
| - | 0x581A | STAT_0x581A_WERT | Nockenwelle Einlass | °CRK | CAM_IN_KWP | - | unsigned char | - | 0,400000005960464 | 1 | 50,0 |
| - | 0x581B | STAT_0x581B_WERT | Nockenwelle Einlass Sollwert | °CRK | CAM_SP_IVVT_IN_KWP | - | unsigned char | - | 0,400000005960464 | 1 | 50,0 |
| - | 0x581C | STAT_0x581C_WERT | Nockenwelle Auslass | °CRK | CAM_EX[1] | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| - | 0x581D | STAT_0x581D_WERT | Nockenwelle Auslass Sollwert | °CRK | CAM_SP_IVVT_EX | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| - | 0x581E | STAT_0x581E_WERT | Ansauglufttemperatur | °C | TIA_MES | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x581F | STAT_0x581F_WERT | Motortemperatur | °C | TCO_MES | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x5820 | STAT_0x5820_WERT | Kühlmitteltemperatur Kühlerausgang | °C | TCO_2_MES | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x5821 | STAT_0x5821_WERT | Steuergeräte-Innentemperatur | °C | TECU | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x5822 | STAT_0x5822_WERT | (Motor)-Öltemperatur | °C | TOIL_MES | - | unsigned char | - | 1,0 | 1 | -40,0 |
| IZMOS | 0x5823 | STAT_ZEIT_MOTOR_STEHT_WERT | Zeit Motor steht | min | T_ES | - | unsigned char | - | 256,0 | 1 | 0,0 |
| - | 0x5824 | STAT_0x5824_WERT | Umgebungstemperatur | °C | TAM | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x5825 | STAT_0x5825_WERT | Abstellzeit | min | T_ES_CUS | - | unsigned char | - | 256,0 | 1 | 0,0 |
| IDKS1 | 0x5826 | STAT_DROSSELKLAPPE_SENSOR1_WERT | Drosselklappe Sensor 1 | °TPS | TPS_AV_1 | - | unsigned char | - | 1,8673014640808114 | 1 | 0,0 |
| - | 0x5827 | STAT_0x5827_WERT | Lambdasondenheizung vor Katalysator Bank 1 | % | LSHPWM_UP[1] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5828 | STAT_0x5828_WERT | Lambdasondenheizung vor Katalysator Bank 2 | % | LSHPWM_UP[2] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5829 | STAT_0x5829_WERT | Lambdasondenheizung hinter Katalysator Bank 1 | % | LSHPWM_DOWN[1] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x582A | STAT_0x582A_WERT | Lambdasondenheizung hinter Katalysator Bank 2 | % | LSHPWM_DOWN[2] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IDRCA | 0x582B | STAT_DREHMOMENTEINGRIFF_CAN_WERT | Drehmomenteingriff über CAN | - | STATE_TQ_CAN_PLAUS | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x582C | STAT_0x582C_WERT | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 1 | - | CTR_ERR_LSL_IF_SPI_WR[1] | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x582D | STAT_0x582D_WERT | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 2 | - | CTR_ERR_LSL_IF_SPI_WR[2] | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x582E | STAT_0x582E_WERT | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 1 | - | FAC_DIAG_DYN_LSL_UP[1] | - | unsigned char | - | 0,25 | 1 | 0,0 |
| - | 0x582F | STAT_0x582F_WERT | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 2 | - | FAC_DIAG_DYN_LSL_UP[2] | - | unsigned char | - | 0,25 | 1 | 0,0 |
| - | 0x5830 | STAT_0x5830_WERT | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 1 | - | FAC_MV_DIAG_DYN_LSL_UP[1] | - | unsigned char | - | 0,25 | 1 | 0,0 |
| - | 0x5831 | STAT_0x5831_WERT | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 2 | - | FAC_MV_DIAG_DYN_LSL_UP[2] | - | unsigned char | - | 0,25 | 1 | 0,0 |
| IMOST | 0x5832 | STAT_MOTOR_STATUS_WERT | Motor Status | 0-n | STATE_ENG | - | 0xFF | _CNV_S_6_RANGE_STAT_146 | 1 | 1 | 0 |
| - | 0x5833 | STAT_0x5833_WERT | Umgebungstemperatur beim Start | °C | TAM_ST | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x5834 | STAT_0x5834_WERT | Umgebungsdruck | hPa | AMP_MES | - | unsigned char | - | 21,226886749267585 | 1 | 0,0 |
| INGRD | 0x5836 | STAT_DREHZAHLGRADIENT_WERT | Drehzahlgradient | rpm/s | N_GRD | - | signed char | - | 32,0 | 1 | 0,0 |
| - | 0x5837 | STAT_0x5837_WERT | Status OBD-I Fehler vor Katalysator Bank 1 | 0-n | STATE_ERR_EL_LSL_UP[1] | - | 0xFF | _CNV_S_11_EGCP_RANGE_657 | 1 | 1 | 0 |
| - | 0x5838 | STAT_0x5838_WERT | Status OBD-I Fehler vor Katalysator Bank 2 | 0-n | STATE_ERR_EL_LSL_UP[2] | - | 0xFF | _CNV_S_11_EGCP_RANGE_657 | 1 | 1 | 0 |
| ISDKN | 0x5839 | STAT_DROSSELKLAPPE_NOTLAUF_WERT | Status Drosselklappe Notlauf | 0-n | STATE_ETC_LIH | - | 0xFF | _CNV_S_6_RANGE_STAT_304 | 1 | 1 | 0 |
| - | 0x583A | STAT_0x583A_WERT | Ansauglufttemperatur beim Start | °C | TIA_ST | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| IKTFS | 0x583B | STAT_KRAFTSTOFFTANK_FUELLSTAND_WERT | Kraftstofftank Füllstand | l | FTL | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x583C | STAT_0x583C_WERT | Spannung Kl. 87 | V | VB | - | unsigned char | - | 0,101562492549419 | 1 | 0,0 |
| - | 0x583D | STAT_0x583D_WERT | Reset Quelle | - | RST_DET | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x583E | STAT_0x583E_WERT | Motordrehzahl bei Reset | rpm | N_RST_DET | - | unsigned char | - | 256,0 | 1 | 0,0 |
| - | 0x583F | STAT_0x583F_WERT | Drosselklappe Sollwert | °TPS | TPS_SP | - | unsigned char | - | 1,8673014640808114 | 1 | 0,0 |
| - | 0x5840 | STAT_0x5840_WERT | CPU Last bei Reset | % | CPU_LOAD_RST_DET | - | unsigned char | - | 25,0 | 1 | 0,0 |
| RTSGR | 0x5841 | STAT_STEUERGERAETE_INNENTEMPERATUR_ROH_WERT | SG-Innentemperatur Rohwert | V | V_TECU_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5843 | STAT_0x5843_WERT | Versorgung FWG 1 | V | VCC_PVS_1_KWP | - | unsigned char | - | 0,0390625037252903 | 1 | 0,0 |
| - | 0x5845 | STAT_0x5845_WERT | Spannung Lambdasonde vor Katalysator Bank 1 | V | VLS_UP_KWP[1] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5846 | STAT_0x5846_WERT | Spannung Pedalwertgeber 1 | V | V_PVS_1_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5847 | STAT_0x5847_WERT | Spannung Pedalwertgeber 2 | V | V_PVS_2_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5848 | STAT_0x5848_WERT | Spannung Lambdasonde vor Katalysator Bank 2 | V | VLS_UP_KWP[2] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5849 | STAT_0x5849_WERT | Spannung Lambdasonde hinter Katalysator Bank 1 | V | VLS_DOWN_KWP[1] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| RUK15 | 0x584A | STAT_KL15_SPANNUNG_ROH_WERT | Spannung Kl. 15 Rohwert | V | V_IGK_BAS_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x584B | STAT_0x584B_WERT | Spannung Lambdasonde hinter Katalysator Bank 2 | V | VLS_DOWN_KWP[2] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x584C | STAT_0x584C_WERT | Spannung Drosselklappe Potentiometer 2 | V | V_TPS_2_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| SQTEK | 0x584D | STAT_TANKENTLUEFTUNG_DURCHFLUSS_SOLL_WERT | korrigierter Sollwert Durchfluss Tankentlüftung | kg/h | FLOW_COR_CPS | - | unsigned char | - | 0,03125 | 1 | 0,0 |
| - | 0x584E | STAT_0x584E_WERT | Spannung Drosselklappe Potentiometer 1 | V | V_TPS_1_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x584F | STAT_0x584F_WERT | Spannung Luftmasse | V | V_MAF | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| - | 0x5850 | STAT_0x5850_WERT | Spannung Motortemperatur | V | V_TCO_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5851 | STAT_0x5851_WERT | Spannung Ansauglufttemperatur | - | V_TIA | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| - | 0x5852 | STAT_0x5852_WERT | Kühlmitteltemperatur Kühlerausgang Rohwert | V | V_TCO_2_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5853 | STAT_0x5853_WERT | Spannung Kl.87 Rohwert | V | VB_BAS_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5854 | STAT_0x5854_WERT | Versorgung FWG 2 | V | VCC_PVS_2_KWP | - | unsigned char | - | 0,0390625037252903 | 1 | 0,0 |
| - | 0x5855 | STAT_0x5855_WERT | Mittelwert Bank 1 | % | FAC_LAM_MV_MMV[1] | - | signed char | - | 0,390625 | 1 | 2,22044609888115E-14 |
| - | 0x5856 | STAT_0x5856_WERT | Mittelwert Bank 2 | % | FAC_LAM_MV_MMV[2] | - | signed char | - | 0,390625 | 1 | 2,22044609888115E-14 |
| - | 0x5858 | STAT_0x5858_WERT | Drosselklappe aktueller Wert | °TPS | TPS_AV | - | unsigned char | - | 1,8673014640808114 | 1 | 0,0 |
| - | 0x5859 | STAT_0x5859_WERT | DMTL Strom Referenzleck | mA | CUR_DMTL_REF_LEAK_KWP | - | unsigned char | - | 0,195312470197678 | 1 | 0,0 |
| - | 0x585A | STAT_0x585A_WERT | DMTL Strom Grobleck | mA | CUR_DMTL_ROUGH_LEAK_MIN_KWP | - | unsigned char | - | 0,195312470197678 | 1 | 0,0 |
| - | 0x585B | STAT_0x585B_WERT | DMTL Strom Diagnoseende | mA | CUR_DMTL_COR_FIL_KWP | - | unsigned char | - | 0,195312470197678 | 1 | 0,0 |
| - | 0x585C | STAT_0x585C_WERT | Widerstand Lambdasonde hinter Katalysator Bank 1 | ohm | R_IT_LS_DOWN_KWP_H[1] | - | unsigned char | - | 256,0 | 1 | 0,0 |
| IRLN2 | 0x585D | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT2_WERT | Widerstand Lambdasonde hinter Katalysator Bank 2 | ohm | R_IT_LS_DOWN_KWP_H[2] | - | unsigned char | - | 256,0 | 1 | 0,0 |
| IRUN1 | 0x585E | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT1_UNTERES_BYTE_WERT | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 1 | ohm | R_IT_LS_DOWN_KWP_L[1] | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IRUN2 | 0x585F | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT2_UNTERES_BYTE_WERT | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 2 | ohm | R_IT_LS_DOWN_KWP_L[2] | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IRLV1 | 0x5860 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT1_WERT | Widerstand Lambdasonde vor Katalysator Bank 1 | ohm | R_IT_LS_UP_KWP_H[1] | - | unsigned char | - | 64,0 | 1 | 0,0 |
| IRLV2 | 0x5861 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT2_WERT | Widerstand Lambdasonde vor Katalysator Bank 2 | ohm | R_IT_LS_UP_KWP_H[2] | - | unsigned char | - | 64,0 | 1 | 0,0 |
| IRUV1 | 0x5863 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT1_UNTERES_BYTE_WERT | untere Byte Widerstand Lambdasonde vor Katalysator Bank 1 | ohm | R_IT_LS_UP_KWP_L[1] | - | unsigned char | - | 0,25 | 1 | 0,0 |
| IRUV2 | 0x5864 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT2_UNTERES_BYTE_WERT | untere Byte Widerstand Lambdasonde vor Katalysator Bank 2 | ohm | R_IT_LS_UP_KWP_L[2] | - | unsigned char | - | 0,25 | 1 | 0,0 |
| - | 0x5865 | STAT_0x5865_WERT | Ölstand Mittelwert Langzeit | - | OZ_NIVLANGT | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| - | 0x5866 | STAT_0x5866_WERT | Füllstand Motoröl | - | OZ_LP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5867 | STAT_0x5867_WERT | Kilometerstand | km | CTR_KM_CAN | - | unsigned char | - | 2560,0 | 1 | 0,0 |
| ISSR1 | 0x5868 | STAT_STANDVERBRAUCHER_REGISTRIERT_TEIL1_WERT | Status Standverbraucher registriert Teil 1 | - | STAT_SV_REG1 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ISSR2 | 0x5869 | STAT_STANDVERBRAUCHER_REGISTRIERT_TEIL2_WERT | Status Standverbraucher registriert Teil 2 | - | STAT_SV_REG2 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x586A | STAT_0x586A_WERT | Batteriespannung von IBS gemessen | - | U_BATT | - | unsigned char | - | 0,06400000303983693 | 1 | 6,0 |
| IZR82 | 0x586B | STAT_ZEIT_MIT_RUHESTROM_80_200_WERT | Zeit mit Ruhestrom 80 - 200 mA | min | T2HISTSHORT | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| IZR21 | 0x586C | STAT_ZEIT_MIT_RUHESTROM_200_1000_WERT | Zeit mit Ruhestrom 200 - 1000 mA | min | T3HISTSHORT | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| IZSST | 0x586D | STAT_ZAEHLER_ERKENNUNG_SCHLECHTE_STRASSE_WERT | Zähler Erkennung schlechte Strasse | - | SUM_RR | - | unsigned char | - | 256,0 | 1 | 0,0 |
| IZRG1 | 0x586E | STAT_ZEIT_MIT_RUHESTROM_GROESER_1000_WERT | Zeit mit Ruhestrom größer 1000 mA | min | T4HISTSHORT | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| - | 0x5870 | STAT_0x5870_WERT | Spannung DME Umgebungsdruck | V | V_AMP_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| SLAG1 | 0x5871 | STAT_LAMBDA_SOLLWERT_GRUPPE1_WERT | Lambda-Sollwert Gruppe 1 | - | LAMB_SP_KWP[1] | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| SLAG2 | 0x5873 | STAT_LAMBDA_SOLLWERT_GRUPPE2_WERT | Lambda-Sollwert Gruppe 2 | - | LAMB_SP_KWP[2] | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| - | 0x5874 | STAT_0x5874_WERT | Spannung Strommessung DMTL | V | V_DMTL_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| ILMMM | 0x5876 | STAT_LUFTMASSE_MITTLERE_MINIMALE_WERT | Mittlere Diagnosewert minimale Luftmasse | kg/h | SAF_DIAG_MIN | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IDMMS | 0x5877 | STAT_DIFFERENZ_MAX_MIN_SAF_WERT | Differenz zwischen Maximum und Minimum SAF | kg/h | SAF_KGH_DIF | - | unsigned char | - | 4,0 | 1 | 0,0 |
| ILRR1 | 0x5878 | STAT_LAMBDAVERSCHIEBUNG_RUECKFUEHRREGLER1_WERT | Lambdaverschiebung Rückführregler 1 | - | LAMB_DELTA_I_LAM_ADJ_KWP[1] | - | signed char | - | 9,765625E-4 | 1 | 0,0 |
| ILRR2 | 0x5879 | STAT_LAMBDAVERSCHIEBUNG_RUECKFUEHRREGLER2_WERT | Lambdaverschiebung Rückführregler 2 | - | LAMB_DELTA_I_LAM_ADJ_KWP[2] | - | signed char | - | 9,765625E-4 | 1 | 0,0 |
| ISFGR | 0x587A | STAT_FGR_WERT | Status FGR | 0-n | STATE_CRU | - | 0xFF | _CNV_S_6_RANGE_STAT_105 | 1 | 1 | 0 |
| ISMST | 0x587C | STAT_MOTORSTEUERUNG_WERT | Status Motorsteuerung | 0-n | ECU_STATE | - | 0xFF | _CNV_S_7_RANGE_ECU__142 | 1 | 1 | 0 |
| - | 0x587D | STAT_0x587D_WERT | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 1 | 0-n | STATE_SYM_DIAG_PUC_LSL_UP[1] | - | 0xFF | _CNV_S_4_EGCP_RANGE_668 | 1 | 1 | 0 |
| - | 0x587E | STAT_0x587E_WERT | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 2 | 0-n | STATE_SYM_DIAG_PUC_LSL_UP[2] | - | 0xFF | _CNV_S_4_EGCP_RANGE_668 | 1 | 1 | 0 |
| IELTV | 0x587F | STAT_E_LUEFTER_TASTVERHAELTNIS_WERT | Tastverhältnis E-Lüfter | % | ECFPWM[0] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5880 | STAT_0x5880_WERT | Tastverhältnis Luftklappe | % | ECRASPWM | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| SBEGA | 0x5881 | STAT_BERECHNETER_GANG_WERT | berechneter Gang | - | GEAR | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ITMOS | 0x5882 | STAT_MOTORTEMPERATUR_BEIM_START_WERT | Motortemperatur beim Start | °C | TCO_ST | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x5883 | STAT_0x5883_WERT | Spannung Klopfwerte Zylinder 1 | V | NL[0] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5885 | STAT_0x5885_WERT | Spannung Klopfwerte Zylinder 3 | V | NL[2] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5886 | STAT_0x5886_WERT | Spannung Klopfwerte Zylinder 6 | V | NL[3] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5888 | STAT_0x5888_WERT | Spannung Klopfwerte Zylinder 4 | V | NL[5] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| ILAG1 | 0x5889 | STAT_LAMBDA_ISTWERT_GRUPPE1_WERT | Lambda-Istwert Gruppe 1 | - | LAMB_KWP[1] | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| ILAG2 | 0x588A | STAT_LAMBDA_ISTWERT_GRUPPE2_WERT | Lambda-Istwert Gruppe 2 | - | LAMB_KWP[2] | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| IZSSE | 0x588B | STAT_ZEIT_SEIT_STARTENDE_WERT | Zeit seit Startende | s | T_AST | - | unsigned char | - | 25,600000381469695 | 1 | 0,0 |
| ITKV1 | 0x588C | STAT_LAMBDASONDE_KERAMIKTEMPERATUR_VORKAT1_WERT | Keramiktemperatur Lambdasonde vor Katalysator Bank 1 | °C | TTIP_MES_LS_UP[1] | - | signed char | - | 16,0 | 1 | 0,0 |
| IZDML | 0x588D | STAT_ZEIT_DMTL_LECKMESSUNG_WERT | aktuelle Zeit DMTL Leckmessung | s | T_ACT_LEAK_MES | - | unsigned char | - | 25,600000381469695 | 1 | 0,0 |
| IIDMP | 0x588E | STAT_PUMPENSTROM_BEI_DMTL_PUMPENPRUEFUNG_WERT | Pumpenstrom bei DMTL Pumpenprüfung | mA | CUR_DMTL_DMTLS_TEST | - | unsigned char | - | 1,5625238418579097 | 1 | 0,0 |
| ITKV2 | 0x588F | STAT_LAMBDASONDE_KERAMIKTEMPERATUR_VORKAT2_WERT | Keramiktemperatur Lambdasonde vor Katalysator Bank 2 | °C | TTIP_MES_LS_UP[2] | - | signed char | - | 16,0 | 1 | 0,0 |
| IMOKU | 0x5891 | STAT_MOMENTANFORDERUNG_KUPPLUNG_WERT | Momentanforderung an der Kupplung | Nm | TQ_REQ_CLU | - | signed char | - | 8,0 | 1 | 0,0 |
| IDMGW | 0x5893 | STAT_DREHMOMENTABFALL_BEIM_GANGWECHSEL_WERT | Drehmomentabfall schnell bei Gangwechsel | Nm | TQI_GS_FAST_DEC | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x5894 | STAT_0x5894_WERT | Symptom Lambdasondenheizung vor Katalysator Bank 1 | 0-n | STATE_SYM_OBD_LSL_LSH_UP[1] | - | 0xFF | _CNV_S_4_EGCP_RANGE_661 | 1 | 1 | 0 |
| - | 0x5895 | STAT_0x5895_WERT | Symptom Lambdasondenheizung vor Katalysator Bank 2 | 0-n | STATE_SYM_OBD_LSL_LSH_UP[2] | - | 0xFF | _CNV_S_4_EGCP_RANGE_661 | 1 | 1 | 0 |
| - | 0x5896 | STAT_0x5896_WERT | Abgastemperatur hinter Katalysator Bank 1 | °C | TEG_CAT_DOWN_MDL[1] | - | unsigned char | - | 16,0 | 1 | 0,0 |
| - | 0x5897 | STAT_0x5897_WERT | Abgastemperatur hinter Katalysator Bank 2 | °C | TEG_CAT_DOWN_MDL[2] | - | unsigned char | - | 16,0 | 1 | 0,0 |
| SUGEN | 0x5898 | STAT_GENERATOR_SPANNUNG_SOLL_WERT | Generator Sollspannung | V | V_ALTER_SP_KWP | - | unsigned char | - | 0,100000001490116 | 1 | 0,0 |
| IUOS1 | 0x589B | STAT_SPANNUNGSOFFSET_SIGNALPFAD1_WERT | Spannungsoffset Signalpfad CJ120 1 | V | VLS_OFS_LSL_KWP[1] | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| IUOS2 | 0x589C | STAT_SPANNUNGSOFFSET_SIGNALPFAD2_WERT | Spannungsoffset Signalpfad CJ120 2 | V | VLS_OFS_LSL_KWP[2] | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| IZMAB | 0x58A8 | STAT_MOTORABSTELLZEIT_WERT | Motorabstellzeit | min | T_ES_KWP | - | unsigned char | - | 4,0 | 1 | 0,0 |
| - | 0x58A9 | STAT_0x58A9_WERT | Reset Zähler Überwachungsrechner | - | RST_CTR_MU_SAVE | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58AA | STAT_0x58AA_WERT | Reset Zähler Hauptrechner | - | RST_CTR_MC_SAVE | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IADK1 | 0x58AB | STAT_ABWEICHUNG_DK_POTI1_WERT | Abweichung DK-Ersatzwert und DK-Potentiometer 1 | mg/stk | TPS_MAF_DIF_INT_1 | - | unsigned char | - | 5,425863742828365 | 1 | 0,0 |
| IADK2 | 0x58AC | STAT_ABWEICHUNG_DK_POTI2_WERT | Abweichung DK-Ersatzwert und DK-Potentiometer 2 | mg/stk | TPS_MAF_DIF_INT_2 | - | unsigned char | - | 5,425863742828365 | 1 | 0,0 |
| IPWG1 | 0x58AD | STAT_PEDALWERTGEBER1_WERT | Pedalwertgeber 1 | % | PV_AV_1 | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IKRAN | 0x58AF | STAT_KRAFTSTOFF_ANFORDERUNG_AN_PUMPE_WERT | Kraftstoff Anforderung an Pumpe | l/h | VFF_EFP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IDKAD | 0x58B0 | STAT_DK_ADAPTIONSSCHRITT_WERT | DK-Adaptionsschritt | - | TPS_AD_STEP_KWP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IZFZ1 | 0x58B1 | STAT_FUNKENBRENNDAUER_ZYL1_WERT | Funkenbrenndauer Zylinder 1 | ms | V_DUR_IGC_0 | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| IZFZ5 | 0x58B2 | STAT_FUNKENBRENNDAUER_ZYL5_WERT | Funkenbrenndauer Zylinder 5 | ms | V_DUR_IGC_1 | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| IZFZ3 | 0x58B3 | STAT_FUNKENBRENNDAUER_ZYL3_WERT | Funkenbrenndauer Zylinder 3 | ms | V_DUR_IGC_2 | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| IZFZ6 | 0x58B4 | STAT_FUNKENBRENNDAUER_ZYL6_WERT | Funkenbrenndauer Zylinder 6 | ms | V_DUR_IGC_3 | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| IZFZ2 | 0x58B5 | STAT_FUNKENBRENNDAUER_ZYL2_WERT | Funkenbrenndauer Zylinder 2 | ms | V_DUR_IGC_4 | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| IZFZ4 | 0x58B6 | STAT_FUNKENBRENNDAUER_ZYL4_WERT | Funkenbrenndauer Zylinder 4 | ms | V_DUR_IGC_5 | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| IPBRE | 0x58B7 | STAT_BREMSDRUCK_WERT | Bremsdruck | bar | BRAKE_PRS | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58B8 | STAT_0x58B8_WERT | Drehzahl Überwachung | rpm | N_32_MON | - | unsigned char | - | 32,0 | 1 | 0,0 |
| - | 0x58B9 | STAT_0x58B9_WERT | Pedalwert Überwachung | % | PV_AV_MON | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x58BC | STAT_0x58BC_WERT | Luftmasse Überwachung | mg/stk | MAF_MON | - | unsigned char | - | 5,44705867767334 | 1 | 0,0 |
| - | 0x58BD | STAT_0x58BD_WERT | Modellluftmasse Überwachung tiefpassgefiltert | mg/stk | MAF_SUB_COR_MMV_MON | - | unsigned char | - | 5,44705867767334 | 1 | 0,0 |
| IMMSR | 0x58BF | STAT_MOMENTENANFORDERUNG_VON_MSR_RELATIV_WERT | relative Momentenforderung von MSR über CAN | % | TQI_MSR_CAN | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x58C0 | STAT_0x58C0_WERT | Motordrehzahl Ersatzwert Überwachung | rpm | N_32_SUB_MON | - | unsigned char | - | 32,0 | 1 | 0,0 |
| ITLSZ | 0x58C1 | STAT_LAUFUNRUHE_SEGMENTZEIT_WERT | Laufunruhe Segmentzeit | µs | SEG_T_MES | - | unsigned char | - | 256,0 | 1 | 0,0 |
| INSUE | 0x58C7 | STAT_LEERLAUF_SOLLDREHZAHLABWEICHUNG_WERT | LL-Solldrehzahlabweichung Überwachung | rpm | N_DIF_SP_IS_MON | - | unsigned char | - | 32,0 | 1 | -4096,0 |
| - | 0x58C8 | STAT_0x58C8_WERT | I-Anteil Momentdifferenz Überwachung und Modell | Nm | TQ_DIF_I_IS_MON | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58C9 | STAT_0x58C9_WERT | I-Anteil LL passive Rampe aktiv | 0/1 | LV_PAS_RAMP_ACT_I_IS | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x58CA | STAT_0x58CA_WERT | PD-Anteil langsam Leerlaufregelung | Nm | TQ_DIF_P_D_SLOW_IS | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58CB | STAT_0x58CB_WERT | PD-Anteil schnell Leerlaufregelung | Nm | TQ_DIF_P_D_FAST_IS | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58CC | STAT_0x58CC_WERT | Verlustmoment Überwachung | Nm | TQ_LOSS_MON | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58CD | STAT_0x58CD_WERT | Verlustmomentabweichung Überwachung | Nm | TQ_LOSS_DIF_MON | - | signed char | - | 2,0 | 1 | 0,0 |
| - | 0x58CE | STAT_0x58CE_WERT | Carrierbyte Schalterstati | - | STATE_BYTE_SWI_KWP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| SMOMO | 0x58CF | STAT_MOTORMOMENT_SOLL_WERT | Motormoment Sollwert Überwachung | Nm | TQI_SP_MON | - | unsigned char | - | 2,0 | 1 | 0,0 |
| IMOMO | 0x58D0 | STAT_MOTORMOMENT_IST_WERT | Motormoment Istwert Überwachung | Nm | TQI_AV_MON | - | unsigned char | - | 2,0 | 1 | 0,0 |
| IMOAK | 0x58D1 | STAT_MOTORMOMENT_AKTUELL_WERT | Moment aktueller Wert | Nm | TQI_AV | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58D4 | STAT_0x58D4_WERT | Abweichung maximales Moment an Kupplung Überwachung | Nm | TQ_MAX_CLU_DIF_MON | - | signed char | - | 2,0 | 1 | 0,0 |
| - | 0x58D6 | STAT_0x58D6_WERT | Abweichung minimales Moment an Kupplung Überwachung | Nm | TQ_MIN_CLU_DIF_MON | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58D9 | STAT_0x58D9_WERT | Fehler Hauptrechner | 0-n | ERR_COD_MC_SAVE | - | 0xFF | _CNV_S_14_TMO3_ERR_C_364 | 1 | 1 | 0 |
| - | 0x58DA | STAT_0x58DA_WERT | Fehler Überwachungsrechner | 0-n | ERR_COD_MU_SAVE | - | 0xFF | _CNV_S_21_TMO3_ERR_C_365 | 1 | 1 | 0 |
| - | 0x58DB | STAT_0x58DB_WERT | Fehler Bitfeld high Byte | - | STATE_N_MAX_MON_HIGH_KWP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58DC | STAT_0x58DC_WERT | Fehler Bitfeld low Byte | - | STATE_N_MAX_MON_LOW_KWP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IUSPS | 0x58DF | STAT_SPORTSCHALTER_SPANNUNG_WERT | Spannung Sportschalter | V | V_SOF_SWI_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x58E0 | STAT_0x58E0_WERT | Abgleich Drosselklappenmodell (Faktor) | - | EISYDK_KORFAK_B | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| - | 0x58E1 | STAT_0x58E1_WERT | Abgleich Drosselklappenmodell (Offset) | kg/h | EISYDK_KOROFF_B | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58E2 | STAT_0x58E2_WERT | Abgleich Einlassventilmodell (Faktor) | - | EISYEV_KORFAK_B | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| - | 0x58E3 | STAT_0x58E3_WERT | Abgleich Einlassventilmodell (Offset) | kg/h | EISYEV_KOROFF_B | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58E4 | STAT_0x58E4_WERT | Betriebsart Istwert | 0-n | BA_IST | - | 0xFF | _CNV_S_7_Def_ba_400 | 1 | 1 | 0 |
| INMAZ | 0x58E5 | STAT_DREHZAHL_MAXIMAL_BEI_ZUENDAUSSETZER_WERT | Maximale Drehzahl bei Zündaussetzern | rpm | N_MAX_SCDN_MIS_32_KWP | - | unsigned char | - | 32,0 | 1 | 0,0 |
| ILMAZ | 0x58E6 | STAT_LAST_MAXIMAL_BEI_ZUENDAUSSETZER_RELATIV_WERT | Maximale relative Last bei Zündaussetzern | % | LOAD_MAX_SCDN_MIS | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| ILMIZ | 0x58E7 | STAT_LAST_MINIMAL_BEI_ZUENDAUSSETZER_RELATIV_WERT | Minimale relative Last bei Zündaussetzern | % | LOAD_MIN_SCDN_MIS | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| INMIZ | 0x58E8 | STAT_DREHZAHL_MINIMAL_BEI_ZUENDAUSSETZER_WERT | Minimale Drehzahl bei Zündaussetzern | rpm | N_MIN_SCDN_MIS_32_KWP | - | unsigned char | - | 32,0 | 1 | 0,0 |
| IDMEL | 0x58F1 | STAT_DME_LOSNUMMER_WERT | DME - Losnummer | 0-n | STATE_LRN_ECU | - | 0xFF | _CNV_S_7_RANGE_STAT_325 | 1 | 1 | 0 |
| - | 0x58F5 | STAT_0x58F5_WERT | Eingangssignal Rückführregler 1 | V | VLS_DIF_LAM_ADJ_KWP[1] | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| - | 0x58F6 | STAT_0x58F6_WERT | Eingangssignal Rückführregler 2 | V | VLS_DIF_LAM_ADJ_KWP[2] | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| ILSA5 | 0x58F8 | STAT_LAUFUNRUHE_SEGMENTADAPTION_ZYL5_WERT | Segmentadaption Laufunruhe Zyl. 5 | %. | SEG_AD_MMV_ER[1] | - | signed char | - | 0,06103530898690227 | 1 | 1,92095835817427E-5 |
| ILSA3 | 0x58F9 | STAT_LAUFUNRUHE_SEGMENTADAPTION_ZYL3_WERT | Segmentadaption Laufunruhe Zyl. 3 | %. | SEG_AD_MMV_ER[2] | - | signed char | - | 0,06103530898690227 | 1 | 1,92095835817427E-5 |
| - | 0x58FA | STAT_0x58FA_WERT | Beladungsgrad Aktivkohlefilter TEV- Funktionstest | - | CL_MMV_SAE | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| - | 0x58FB | STAT_0x58FB_WERT | Zähler Drehzahlerhöhungen TEV- Funktionstest | cyc | SUM_DIAG_DIAGCPS_SAE | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IUPV1 | 0x5A00 | STAT_PWG1_VERSORGUNGSSPANNUNG_WERT | Versorgung FWG 1 | V | VCC_PVS_1 | - | unsigned integer | - | 0,00976559147238731 | 1 | 0,0 |
| IUPV2 | 0x5A01 | STAT_PWG2_VERSORGUNGSSPANNUNG_WERT | Versorgung FWG 2 | V | VCC_PVS_2 | - | unsigned integer | - | 0,00976559147238731 | 1 | 0,0 |
| IUPW1 | 0x5A04 | STAT_PWG1_SPANNUNG_WERT | Spannung Pedalwertgeber 1 | V | V_PVS_1 | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUPW2 | 0x5A05 | STAT_PWG2_SPANNUNG_WERT | Spannung Pedalwertgeber 2 | V | V_PVS_2 | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUDK1 | 0x5A06 | STAT_DK1_SPANNUNG_WERT | Spannung Drosselklappe Potentiometer 1 | V | V_TPS_1 | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUDK2 | 0x5A07 | STAT_DK2_SPANNUNG_WERT | Spannung Drosselklappe Potentiometer 2 | V | V_TPS_2 | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUANS | 0x5A08 | STAT_ANSAUGLUFTTEMPERATUR_SPANNUNG_WERT | Spannung Ansauglufttemperatur | - | V_TIA | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| IUKUM | 0x5A09 | STAT_KUEHLMITTELTEMPERATUR_SPANNUNG_WERT | Spannung Motortemperatur | V | V_TCO | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUKUA | 0x5A0A | STAT_KUEHLERAUSLASSTEMPERATUR_SPANNUNG_WERT | Spannung Kühlmitteltemperatur Kühlerausgang | V | V_TCO_2 | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUUMG | 0x5A0B | STAT_UMGEBUNGSDRUCK_SPANNUNG_WERT | Spannung DME Umgebungsdruck | V | V_AMP | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IULMM | 0x5A0C | STAT_LUFTMASSE_WERT | Spannung Luftmasse | V | V_MAF | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| IUSGI | 0x5A0E | STAT_STEUERGERAETE_INNENTEMPERATUR_SPANNUNG_WERT | Spannung SG-Innentemperatur | V | V_TECU | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| - | 0x5A0F | STAT_0x5A0F_WERT | Spannung Kl.15 | V | V_IGK_BAS | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUK15 | 0x5A10 | STAT_KL15_SPANNUNG_WERT | Spannung Kl15 | V | V_IGK_MES | - | unsigned integer | - | 0,0280601158738136 | 1 | 0,0 |
| IUSV1 | 0x5A11 | STAT_SONDENSPANNUNG_VORKAT_BANK1_WERT | Spannung Lambdasonde vor Katalysator Bank 1 | V | VLS_UP[1] | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUSV2 | 0x5A12 | STAT_SONDENSPANNUNG_VORKAT_BANK2_WERT | Spannung Lambdasonde vor Katalysator Bank 2 | V | VLS_UP[2] | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUSN1 | 0x5A13 | STAT_SONDENSPANNUNG_NACHKAT_BANK1_WERT | Spannung Lambdasonde hinter Katalysator Bank 1 | V | VLS_DOWN[1] | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUSN2 | 0x5A14 | STAT_SONDENSPANNUNG_NACHKAT_BANK2_WERT | Spannung Lambdasonde hinter Katalysator Bank 2 | V | VLS_DOWN[2] | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUDMT | 0x5A17 | STAT_DMTL_SPANNUNG_WERT | Spannung Strommessung DMTL | V | V_DMTL | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| ITKUA | 0x5A21 | STAT_KUEHLERAUSLASSTEMPERATUR_WERT | Kühlmitteltemperatur Kühlerausgang | °C | TCO_2_MES | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| ITSGI | 0x5A22 | STAT_STEUERGERAETE_INNENTEMPERATUR_WERT | Steuergeräte-Innentemperatur | °C | TECU | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| SWDKL | 0x5A24 | STAT_DK_WINKEL_SOLL_WERT | Drosselklappe Sollwert | °TPS | TPS_SP | - | unsigned integer | - | 0,00729414634406567 | 1 | 0,0 |
| IPUMG | 0x5A26 | STAT_UMGEBUNGSDRUCK_WERT | Umgebungsdruck | hPa | MAP | - | unsigned integer | - | 0,0829175263643265 | 1 | 0,0 |
| IPPW1 | 0x5A27 | STAT_PWG1_WERT | Pedalwertgeber Potentiometer 1 | % | PV_AV_1 | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IPPW2 | 0x5A28 | STAT_PWG2_WERT | Pedalwertgeber Potentiometer 2 | % | PV_AV_2 | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| RFPWG | 0x5A29 | STAT_FAHRERWUNSCH_PEDAL_ROH_WERT | Fahrpedalwert | % | PV_AV_RAW | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| ILUZ1 | 0x5A30 | STAT_LAUFUNRUHE_ZYL1_WERT | Laufunruhe Zylinder 1 | µs | ER_CYL[0] | - | signed integer | - | 1,0 | 1 | 0,0 |
| ILUZ2 | 0x5A31 | STAT_LAUFUNRUHE_ZYL2_WERT | Laufunruhe Zylinder 2 | µs | ER_CYL[4] | - | signed integer | - | 1,0 | 1 | 0,0 |
| ILUZ3 | 0x5A32 | STAT_LAUFUNRUHE_ZYL3_WERT | Laufunruhe Zylinder 3 | µs | ER_CYL[2] | - | signed integer | - | 1,0 | 1 | 0,0 |
| ILUZ4 | 0x5A33 | STAT_LAUFUNRUHE_ZYL4_WERT | Laufunruhe Zylinder 4 | µs | ER_CYL[5] | - | signed integer | - | 1,0 | 1 | 0,0 |
| ILUZ5 | 0x5A34 | STAT_LAUFUNRUHE_ZYL5_WERT | Laufunruhe Zylinder 5 | µs | ER_CYL[1] | - | signed integer | - | 1,0 | 1 | 0,0 |
| ILUZ6 | 0x5A35 | STAT_LAUFUNRUHE_ZYL6_WERT | Laufunruhe Zylinder 6 | µs | ER_CYL[3] | - | signed integer | - | 1,0 | 1 | 0,0 |
| ISKLO | 0x5A36 | STAT_STATUS_KLOPFEN_WERT | Status Klopfen | 0/1 | LV_KNK | - | 0xFF | - | 1 | 1 | 0 |
| IUKZ1 | 0x5A37 | STAT_KLOPFWERT_ZYL1_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 1 | V | NL[0] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IUKZ2 | 0x5A38 | STAT_KLOPFWERT_ZYL2_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 2 | V | NL[4] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IUKZ3 | 0x5A39 | STAT_KLOPFWERT_ZYL3_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 3 | V | NL[2] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IUKZ4 | 0x5A3A | STAT_KLOPFWERT_ZYL4_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 4 | V | NL[5] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IUKZ5 | 0x5A3B | STAT_KLOPFWERT_ZYL5_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 5 | V | NL[1] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IUKZ6 | 0x5A3C | STAT_KLOPFWERT_ZYL6_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 6 | V | NL[3] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IKSZ1 | 0x5A3D | STAT_KLOPFSIGNAL_ZYL1_WERT | Klopfsignal Zylinder 1 | V | KNKS[0] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IKRZ1 | 0x5A3E | STAT_KLOPFSIGNAL_ZYL1_RELATIV_WERT | Klopfsignal Zylinder 1 relativ | - | KNKS_REL_NL_0 | - | unsigned integer | - | 1,52587890625E-5 | 1 | 0,0 |
| IKSZ6 | 0x5A3F | STAT_KLOPFSIGNAL_ZYL6_WERT | Klopfsignal Zylinder 6 | V | KNKS[5] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IKRZ6 | 0x5A40 | STAT_KLOPFSIGNAL_ZYL6_RELATIV_WERT | Klopfsignal Zylinder 6 relativ | - | KNKS_REL_NL_5 | - | unsigned integer | - | 1,52587890625E-5 | 1 | 0,0 |
| IZEZ1 | 0x5A42 | STAT_EINSPRITZZEIT_ZYL1_WERT | Einspritzzeit Zylinder 1 | ms | ti_1_0 | - | unsigned integer | - | 0,00400000018998981 | 1 | 0,0 |
| IZEZ2 | 0x5A43 | STAT_EINSPRITZZEIT_ZYL2_WERT | Einspritzzeit Zylinder 2 | ms | ti_1_4 | - | unsigned integer | - | 0,00400000018998981 | 1 | 0,0 |
| IZEZ3 | 0x5A44 | STAT_EINSPRITZZEIT_ZYL3_WERT | Einspritzzeit Zylinder 3 | ms | ti_1_2 | - | unsigned integer | - | 0,00400000018998981 | 1 | 0,0 |
| IZEZ4 | 0x5A45 | STAT_EINSPRITZZEIT_ZYL4_WERT | Einspritzzeit Zylinder 4 | ms | ti_1_5 | - | unsigned integer | - | 0,00400000018998981 | 1 | 0,0 |
| IZEZ5 | 0x5A46 | STAT_EINSPRITZZEIT_ZYL5_WERT | Einspritzzeit Zylinder 5 | ms | ti_1_1 | - | unsigned integer | - | 0,00400000018998981 | 1 | 0,0 |
| IZEZ6 | 0x5A47 | STAT_EINSPRITZZEIT_ZYL6_WERT | Einspritzzeit Zylinder 6 | ms | ti_1_3 | - | unsigned integer | - | 0,00400000018998981 | 1 | 0,0 |
| IZWZ1 | 0x5A49 | STAT_ZUENDWINKEL_ZYL1_WERT | Zündwinkel Zylinder1 | °CRK | IGA_IGC[0] | - | unsigned char | - | 0,375 | 1 | -35,6249989382923 |
| ILASB | 0x5A4B | STAT_BERECHNETE_LAST_WERT | Berechneter Lastwert | % | LOAD_CLC | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| ISACR | 0x5A4E | STAT_KLIMAKOMPRESSORRELAIS_EIN | Klimakompressorrelais Ein | 0/1 | LV_ACCOUT_RLY | - | 0xFF | - | 1 | 1 | 0 |
| ILAB1 | 0x5A50 | STAT_LAMBDA_BANK1_WERT | Lambdawert vor Katalysator Bank 1 | - | LAMB_LS_UP[1] | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| ILAB2 | 0x5A51 | STAT_LAMBDA_BANK2_WERT | Lambdawert vor Katalysator Bank 2 | - | LAMB_LS_UP[2] | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| IRNK1 | 0x5A52 | STAT_READINESS_SONDE_NACHKAT_BANK1_WERT | Status LS hinter Katalysator Bank 1 | 0/1 | LV_LS_DOWN_READY[1] | - | 0xFF | - | 1 | 1 | 0 |
| IRNK2 | 0x5A53 | STAT_READINESS_SONDE_NACHKAT_BANK2_WERT | Status LS hinter Katalysator Bank 2 | 0/1 | LV_LS_DOWN_READY[2] | - | 0xFF | - | 1 | 1 | 0 |
| ISHN1 | 0x5A54 | STAT_SONDENHEIZUNG_NACHKAT_BANK1_WERT | Status LS Heizung hinter Katalysator Bank 1 | 0-n | STATE_LSH_DOWN[1] | - | 0xFF | _CNV_S_7_EGCP_RANGE_639 | 1 | 1 | 0 |
| ISHN2 | 0x5A55 | STAT_SONDENHEIZUNG_NACHKAT_BANK2_WERT | Status LS Heizung hinter Katalysator Bank 2 | 0-n | STATE_LSH_DOWN[2] | - | 0xFF | _CNV_S_7_EGCP_RANGE_639 | 1 | 1 | 0 |
| ISHV1 | 0x5A56 | STAT_SONDENHEIZUNG_VORKAT_BANK1_WERT | Status LS Heizung vor Katalysator Bank 1 | 0-n | STATE_LSH_UP[1] | - | 0xFF | _CNV_S_7_EGCP_RANGE_639 | 1 | 1 | 0 |
| ISHV2 | 0x5A57 | STAT_SONDENHEIZUNG_VORKAT_BANK2_WERT | Status LS Heizung vor Katalysator Bank 2 | 0-n | STATE_LSH_UP[2] | - | 0xFF | _CNV_S_7_EGCP_RANGE_639 | 1 | 1 | 0 |
| IAHV1 | 0x5A58 | STAT_SONDENHEIZUNG_PWM_VORKAT_BANK1_WERT | Lambdasondenheizung PWM vor Katalysator Bank 1 | % | LSHPWM_UP[1] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IAHN1 | 0x5A59 | STAT_SONDENHEIZUNG_PWM_NACHKAT_BANK1_WERT | Lambdasondenheizung PWM hinter Katalysator Bank 1 | % | LSHPWM_DOWN[1] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IAHV2 | 0x5A5A | STAT_SONDENHEIZUNG_PWM_VORKAT_BANK2_WERT | Lambdasondenheizung PWM vor Katalysator Bank 2 | % | LSHPWM_UP[2] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IAHN2 | 0x5A5B | STAT_SONDENHEIZUNG_PWM_NACHKAT_BANK2_WERT | Lambdasondenheizung PWM hinter Katalysator Bank 2 | % | LSHPWM_DOWN[2] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| ISBLS | 0x5A60 | STAT_BREMSLICHTSCHALTER_EIN_WERT | Bremslichtschalter Ein | 0/1 | LV_IM_BLS | - | 0xFF | - | 1 | 1 | 0 |
| ISBLT | 0x5A61 | STAT_BREMSLICHTTESTSCHALTER_EIN_WERT | Bremslichttestschalter Ein | 0/1 | LV_IM_BTS | - | 0xFF | - | 1 | 1 | 0 |
| ISOED | 0x5A62 | STAT_OELDRUCKSCHALTER_EIN_WERT | Öldruckschalter Ein | 0/1 | LV_POIL_SWI | - | 0xFF | - | 1 | 1 | 0 |
| ISEBO | 0x5A63 | STAT_E_BOXLUEFTER_EIN_WERT | E-Box-Lüfter Ein | 0/1 | LV_EBOX_CFA | - | 0xFF | - | 1 | 1 | 0 |
| ISDMP | 0x5A66 | STAT_DMTL_PUMPE_EIN_WERT | DMTL Pumpe Ein | 0/1 | LV_DMTL_PUMP | - | 0xFF | - | 1 | 1 | 0 |
| ISDMV | 0x5A67 | STAT_DMTL_VENTIL_EIN_WERT | DMTL Ventil Ein | 0/1 | LV_DMTLS | - | 0xFF | - | 1 | 1 | 0 |
| ISDMH | 0x5A68 | STAT_DMTL_HEIZUNG_EIN_WERT | DMTL Heizung Ein | 0/1 | LV_HDMTL_ON | - | 0xFF | - | 1 | 1 | 0 |
| ISMIL | 0x5A69 | STAT_MIL_EIN_WERT | MIL Lampe Ein | 0/1 | LV_MIL_CAN | - | 0xFF | - | 1 | 1 | 0 |
| ISFGR | 0x5A6A | STAT_LAMPE_FGR_EIN_WERT | Lampe FGR Ein | 0/1 | LV_CRU_MAIN_SWI | - | 0xFF | - | 1 | 1 | 0 |
| ISCEL | 0x5A6B | STAT_CHECK_ENGINE_LAMPE_EIN_WERT | Lampe Check Engine Ein | 0/1 | LV_WAL_1_CAN | - | 0xFF | - | 1 | 1 | 0 |
| ISTFG | 0x5A6D | STAT_TASTE_FGR_EIN_WERT | Status Taste FGR | 0-n | STATE_MSW_CAN | - | 0xFF | _CNV_S_8_RANGE_STAT_18 | 1 | 1 | 0 |
| IAKFT | 0x5A74 | STAT_BEHEIZTER_THERMOSTAT_PWM_WERT | Beheizter Thermostat PWM | % | ECTPWM | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IASEV | 0x5A75 | STAT_SEKUNDAERLUFT_VENTIL_PWM_WERT | Sekundärluft Ventil | 0/1 | LV_SAV | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5A76 | STAT_0x5A76_WERT | Adaption Öffnungspunkt Tankentlüftungsventil | % | CPPWM_ADD_AD_MEM | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IATEV | 0x5A77 | STAT_TEV_PWM_WERT | Tankentlüftungsventil TEV PWM | % | CPPWM_CPS | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IAELUE | 0x5A79 | STAT_E_LUEFTER_PWM_WERT | E-Lüfter PWM | % | ECFPWM[0] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IAVEP | 0x5A7A | STAT_VANOS_EINLASS_PWM_WERT | VANOS PWM Wert Einlass früh | % | IVVTPWM_IN_A | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IAVAP | 0x5A7B | STAT_VANOS_AUSLASS_PWM_WERT | VANOS PWM Wert Auslass früh | % | IVVTPWM_EX_A | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5A7C | STAT_0x5A7C_WERT | VANOS PWM Wert Einlass spät | % | IVVTPWM_IN_R | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5A7D | STAT_0x5A7D_WERT | VANOS PWM Wert Auslass spät | % | IVVTPWM_EX_R | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IINT1 | 0x5A81 | STAT_INTEGRATOR_BANK1_WERT | Integrator Bank 1 | % | FAC_LAM_LIM[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| IINT2 | 0x5A82 | STAT_INTEGRATOR_BANK2_WERT | Integrator Bank 2 | % | FAC_LAM_LIM[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| IADD1 | 0x5A83 | STAT_ADAPTION_ADDITIV_BANK1_WERT | Adaption Offset Lambda Bank 1 | mg/stk | MFF_ADD_LAM_AD_OUT[1] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| IADD2 | 0x5A84 | STAT_ADAPTION_ADDITIV_BANK2_WERT | Adaption Offset Lambda Bank 2 | mg/stk | MFF_ADD_LAM_AD_OUT[2] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| IMUL1 | 0x5A85 | STAT_ADAPTION_MULTIPLIKATIV_BANK1_WERT | Adaption Multiplikation Lambda Bank 1 | % | FAC_LAM_AD_OUT[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| IMUL2 | 0x5A86 | STAT_ADAPTION_MULTIPLIKATIV_BANK2_WERT | Adaption Multiplikation Lambda Bank 2 | % | FAC_LAM_AD_OUT[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5A87 | STAT_0x5A87_WERT | Adaptionswert Trimregelung Bank 1 | - | LAMB_DELTA_AD_LAM_ADJ[1] | - | signed integer | - | 6,103515625E-5 | 1 | 0,0 |
| - | 0x5A88 | STAT_0x5A88_WERT | Adaptionswert Trimregelung Bank 2 | - | LAMB_DELTA_AD_LAM_ADJ[2] | - | signed integer | - | 6,103515625E-5 | 1 | 0,0 |
| - | 0x5A89 | STAT_0x5A89_WERT | multiplikative Gemischadaption hohe Last Bank 1 | % | FAC_H_RNG_LAM_AD[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5A8A | STAT_0x5A8A_WERT | multiplikative Gemischadaption hohe Last Bank 2 | % | FAC_H_RNG_LAM_AD[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5A8B | STAT_0x5A8B_WERT | multiplikative Gemischadaption niedrige Last Bank 1 | % | FAC_L_RNG_LAM_AD[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5A8C | STAT_0x5A8C_WERT | multiplikative Gemischadaption niedrige Last Bank 2 | % | FAC_L_RNG_LAM_AD[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5A8D | STAT_0x5A8D_WERT | additive Gemischadaption Leerlauf Bank 1 | mg/stk | MFF_ADD_LAM_AD[1] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5A8E | STAT_0x5A8E_WERT | additive Gemischadaption Leerlauf Bank 2 | mg/stk | MFF_ADD_LAM_AD[2] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5A91 | STAT_0x5A91_WERT | Katalysatordiagnosewert Bank1 | - | EFF_CAT_DIAG[1] | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| - | 0x5A92 | STAT_0x5A92_WERT | Katalysatordiagnosewert Bank2 | - | EFF_CAT_DIAG[2] | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| SANWA | 0x5A94 | STAT_NW_AUSLASS_SOLL_WERT | Nockenwelle Auslass Sollwert | °CRK | CAM_SP_IVVT_EX | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| IANWA | 0x5A95 | STAT_NW_ADAPTION_AUSLASS_WERT | Adaptionswert Nockenwelle Auslass | °CRK | PSN_AD_CAM_EX_1 | - | unsigned char | - | 0,375 | 1 | -47,9999985694886 |
| IANWE | 0x5A96 | STAT_NW_ADAPTION_EINLASS_WERT | Adaptionswert Nockenwelle Einlass | °CRK | PSN_AD_CAM_IN_1 | - | unsigned char | - | 0,375 | 1 | -47,9999985694886 |
| - | 0x5A97 | STAT_0x5A97_WERT | Bedingung EVANOS im Anschlag beim letzten Abstellen | 0/1 | B_VSEAN_LOC | - | 0xFF | - | 1 | 1 | 0 |
| IAKWF | 0x5A99 | STAT_KURBELWELLEN_ADAPTION_BEENDET_WERT | Kurbelwellen Adaption beendet | 0/1 | LV_SEG_AD_AVL_ER | - | 0xFF | - | 1 | 1 | 0 |
| IDSLS | 0x5AA1 | STAT_SLS_DIAGNOSE_WERT | Status Diagnose TEV | 0-n | STATE_EOL_KWP_CPS | - | 0xFF | _CNV_S_10_STATE_EOL__351 | 1 | 1 | 0 |
| IDTEV | 0x5AA2 | STAT_TEV_DIAGNOSE_WERT | Status Diagnose DMTL | 0-n | STATE_EOL_KWP_DMTL | - | 0xFF | _CNV_S_10_STATE_EOL__351 | 1 | 1 | 0 |
| IDDMT | 0x5AA3 | STAT_DMTL_DIAGNOSE_WERT | Status Diagnose Lambdasonden | 0-n | STATE_EOL_KWP_VLS | - | 0xFF | _CNV_S_10_STATE_EOL__351 | 1 | 1 | 0 |
| IDLSS | 0x5AA4 | STAT_LS_DIAGNOSE_WERT | Status Diagnose Leerlaufdrehzahlverstellung | 0-n | STATE_EOL_KWP_N_SP_IS | - | 0xFF | _CNV_S_10_STATE_EOL__351 | 1 | 1 | 0 |
| - | 0x5AA5 | STAT_0x5AA5_WERT | Status Diagnose Sekundärluft | 0-n | STATE_EOL_KWP_SA | - | 0xFF | _CNV_S_10_STATE_EOL__351 | 1 | 1 | 0 |
| IVKMH | 0x5AB1 | STAT_GESCHWINDIGKEIT_WERT | Geschwindigkeit | km/h | VS | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IWMIL | 0x5AB3 | STAT_FAHRSTRECKE_MIL_AN_WERT | Fahrstrecke mit MIL an | km | DIST_ACT_MIL | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| IZBST | 0x5AB4 | STAT_BETRIEBSSTUNDENZAEHLER_WERT | Betriebsstundenzähler | h | TRT | - | unsigned long | - | 2,77777780866018E-5 | 1 | 0,0 |
| IVSLP | 0x5AB5 | STAT_VARIANTE_SEKUNDAERLUFTPUMPE_WERT | Variante Sekundärluftpumpe | 0/1 | LV_VAR_SAP | - | 0xFF | - | 1 | 1 | 0 |
| RTANS | 0x5AB6 | STAT_ANSAUGLUFTTEMPERATUR1_ROH_WERT | Rohwert Ansauglufttemperatur 1 | °C | TIA_MES | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| RTKWA | 0x5AB7 | STAT_KUEHLWASSERTEMPERATUR_ROH_WERT | Rohwert Kühlwassertemperatur | °C | TCO_MES | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| IUSST | 0x5AB9 | STAT_SPORTSCHALTER_SPANNUNG_WERT | Spannung Sportschalter | V | V_SOF_SWI | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IAKSP | 0x5ABA | STAT_KRAFTSTOFFPUMPE_PWM_WERT | PWM Kraftstoffpumpe | % | EFPPWM | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IMLUF | 0x5ABC | STAT_LUFTMASSE_WERT | Luftmasse | kg/h | MAF_KGH_MES_BAS | - | unsigned integer | - | 0,03125 | 1 | 0,0 |
| IASRE | 0x5ABD | STAT_STARTRELAIS_AKTIV_WERT | Starterrelais aktiv | 0/1 | LV_RLY_ST | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5AC0 | STAT_0x5AC0_WERT | Reset Status Hardware-Register | - | RST_HW_STATUS | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x5AC1 | STAT_0x5AC1_WERT | Reset Status Software-Register | - | RST_SW_STATUS | - | unsigned long | - | 1,0 | 1 | 0,0 |
| - | 0x5AC2 | STAT_0x5AC2_WERT | Reset Adresse | - | RST_LPRC_RESET_ADDRESS | - | unsigned long | - | 1,0 | 1 | 0,0 |
| - | 0x5ACC | STAT_0x5ACC_WERT | Istspreizung Einlassvanos | ° KW | VSE_SPRI | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| - | 0x5ACD | STAT_0x5ACD_WERT | Sollspreizung Einlassvanos | ° KW | VSE_SPRS | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| - | 0x5ACE | STAT_0x5ACE_WERT | Verstellzeit (Früh) Einlassvanos | ms | VSE_VERSTELLZT_FRUEH | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x5ACF | STAT_0x5ACF_WERT | Verstellzeit (Spät) Einlassvanos | ms | VSE_VERSTELLZT_SPAET | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x5AD0 | STAT_0x5AD0_WERT | Status Vanos (Notlauf) | - | ST_VNS_NOTL | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AD1 | STAT_0x5AD1_WERT | Istspreizung Auslassvanos | ° KW | VSA_SPRI | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| - | 0x5AD2 | STAT_0x5AD2_WERT | Sollspreizung Auslassvanos | ° KW | VSA_SPRS | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| - | 0x5AD3 | STAT_0x5AD3_WERT | Verstellzeit (Früh) Auslassvanos | ms | VSA_VERSTELLZT_FRUEH | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x5AD4 | STAT_0x5AD4_WERT | Verstellzeit (Spät) Auslassvanos | ms | VSA_VERSTELLZT_SPAET | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x5AE0 | STAT_0x5AE0_WERT | Kühlmitteltemperatur &lt; 98°C | % | TMOT_B1 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AE1 | STAT_0x5AE1_WERT | 98°C =&lt; Kühlmitteltemperatur =&lt; 112°C | % | TMOT_B2 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AE2 | STAT_0x5AE2_WERT | 113°C =&lt; Kühlmitteltemperatur =&lt; 120°C | % | TMOT_B3 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AE3 | STAT_0x5AE3_WERT | 121°C =&lt; Kühlmitteltemperatur =&lt; 125°C | % | TMOT_B4 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AE4 | STAT_0x5AE4_WERT | Kühlmitteltemperatur &gt; 125°C | % | TMOT_B5 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AE5 | STAT_0x5AE5_WERT | Motoröltemperatur &lt; 80°C | % | TOEL_B1 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AE6 | STAT_0x5AE6_WERT | 80°C =&lt; Motoröltemperatur =&lt; 110°C | % | TOEL_B2 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AE7 | STAT_0x5AE7_WERT | 110°C =&lt; Motoröltemperatur =&lt; 135°C | % | TOEL_B3 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AE8 | STAT_0x5AE8_WERT | 135°C =&lt; Motoröltemperatur =&lt; 150°C | % | TOEL_B4 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AE9 | STAT_0x5AE9_WERT | Motoröltemperatur &gt; 150°C | % | TOEL_B5 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AEA | STAT_0x5AEA_WERT | Getriebeöltemperatur &lt; 80°C | % | TGET_B1 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AEB | STAT_0x5AEB_WERT | 80°C =&lt; Getriebeöltemperatur =&lt; 109°C | % | TGET_B2 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AEC | STAT_0x5AEC_WERT | 110°C =&lt; Getriebeöltemperatur =&lt; 124°C | % | TGET_B3 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AED | STAT_0x5AED_WERT | 125°C =&lt; Getriebeöltemperatur =&lt; 129°C | % | TGET_B4 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AEE | STAT_0x5AEE_WERT | Getriebeöltemperatur &gt; 129°C | % | TGET_B5 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AEF | STAT_0x5AEF_WERT | Umgebungstemperatur &lt; 3°C | % | TUMG_B1 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF0 | STAT_0x5AF0_WERT | 3°C =&lt; Umgebungstemperatur =&lt; 19°C | % | TUMG_B2 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF1 | STAT_0x5AF1_WERT | 20°C =&lt; Umgebungstemperatur =&lt; 29°C | % | TUMG_B3 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF2 | STAT_0x5AF2_WERT | 30°C =&lt; Umgebungstemperatur =&lt; 39°C | % | TUMG_B4 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF3 | STAT_0x5AF3_WERT | Umgebungstemperatur &gt; 39°C | % | TUMG_B5 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF4 | STAT_0x5AF4_WERT | Status Auslass Dichtemessung  | - | ST_BT_VSA_DICHT | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AF5 | STAT_0x5AF5_WERT | Status Auslass Frühanschlag | - | ST_BT_VSA_FRUEHAN | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AF6 | STAT_0x5AF6_WERT | Status Auslass Sollwert einregeln | - | ST_BT_VSA_SOLL | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AF7 | STAT_0x5AF7_WERT | Status Auslass Spätanschlag | - | ST_BT_VSA_SPAETAN | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AF8 | STAT_0x5AF8_WERT | Status Auslass Verstellzeitmessung | - | ST_BT_VSA_VERST | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AF9 | STAT_0x5AF9_WERT | Status Auslass Ventilansteuerung | - | ST_BT_VSA_VENT | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AFA | STAT_0x5AFA_WERT | Status Einlass Dichtemessung | - | ST_BT_VSE_DICHT | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AFB | STAT_0x5AFB_WERT | Status Einlass Frühanschlag | - | ST_BT_VSE_FRUEHAN | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AFC | STAT_0x5AFC_WERT | Status Einlass Sollwert einregeln | - | ST_BT_VSE_SOLL | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AFD | STAT_0x5AFD_WERT | Status Einlass Spätanschlag | - | ST_BT_VSE_SPAETAN | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AFE | STAT_0x5AFE_WERT | Status Einlass Verstellzeitmessung | - | ST_BT_VSE_VERST | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AFF | STAT_0x5AFF_WERT | Status Einlass Ventilansteuerung | - | ST_BT_VSE_VENT | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58FF | - | Umweltbedingung unbekannt | - | - | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-cnv-s-10-state-eol-351"></a>
### _CNV_S_10_STATE_EOL__351

Dimensions: 11 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | ACT |
| 0x01 | ST_INH |
| 0x02 | PAR_NOT_PLAUS |
| 0x03 | WAIT_REL |
| 0x04 | UNDEF |
| 0x05 | NOT_START |
| 0x06 | END_WOUT_RESULT |
| 0x07 | ABORTED |
| 0x08 | END_WOUT_ERR |
| 0x09 | END_WITH_ERR |
| 0xFF | undefiniert |

<a id="table-cnv-s-11-egcp-range-657"></a>
### _CNV_S_11_EGCP_RANGE_657

Dimensions: 12 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | NO_FAULT |
| 0x01 | SCG_LINE_RCD |
| 0x02 | SCG_LINE_VIP |
| 0x03 | SCG_LINE_VG |
| 0x04 | SCG_LINE_VN |
| 0x05 | SCG |
| 0x06 | SCBAT_LINE_RCD |
| 0x07 | SCBAT_LINE_VIP |
| 0x08 | SCBAT_LINE_VG |
| 0x09 | SCBAT_LINE_VN |
| 0x0A | SCBAT |
| 0xFF | undefiniert |

<a id="table-cnv-s-14-tmo3-err-c-364"></a>
### _CNV_S_14_TMO3_ERR_C_364

Dimensions: 15 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | OK |
| 0x01 | COMM_CKS_ERR |
| 0x02 | COMM_HD_ERR |
| 0x03 | PRDR_CHK_ERR |
| 0x04 | SW_VERS_ERR |
| 0x05 | SW_VAR_ERR |
| 0x06 | ABC_MON2_MU_ERR |
| 0x07 | IDX_MON2_MU_ERR |
| 0x08 | SYN_PFM_MU_ERR |
| 0x09 | ROM_LVL2_ERR |
| 0x0A | RAM_LVL2_ERR |
| 0x0B | ROM_LVL1_ERR |
| 0x0C | RAM_LVL1_ERR |
| 0x0D | RST_LOOP_ERR |
| 0xFF | undefiniert |

<a id="table-cnv-s-21-tmo3-err-c-365"></a>
### _CNV_S_21_TMO3_ERR_C_365

Dimensions: 22 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | OK |
| 0x01 | COMM_HD_ERR |
| 0x02 | COMM_CKS_ERR |
| 0x03 | PIN_CONF_ERR |
| 0x04 | SW_VERS_ERR |
| 0x05 | COMM_TOUT_MAX_ERR |
| 0x06 | COMM_TOUT_MIN_ERR |
| 0x07 | RAM_CHK_MU_ERR |
| 0x08 | ROM_CHK_MU_ERR |
| 0x09 | RESP_MON2_MC_ERR |
| 0x0A | RED_SWI_OFF_PATH |
| 0x0B | PFM_1_MC_ERR |
| 0x0C | PFM_2_MC_ERR |
| 0x0D | PFM_3_MC_ERR |
| 0x0E | PFM_4_MC_ERR |
| 0x0F | PFM_5_MC_ERR |
| 0x10 | PFM_6_MC_ERR |
| 0x11 | PFM_7_MC_ERR |
| 0x12 | PFM_8_MC_ERR |
| 0x13 | WDG_MU_ERR |
| 0x14 | ENA_BYTE_ERR |
| 0xFF | undefiniert |

<a id="table-cnv-s-4-egcp-range-661"></a>
### _CNV_S_4_EGCP_RANGE_661

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | NO_SYM |
| 0x01 | TTIP_ERR |
| 0x02 | READY_ERR |
| 0x04 | TTIP_MES_ERR |
| 0xFF | undefiniert |

<a id="table-cnv-s-4-egcp-range-668"></a>
### _CNV_S_4_EGCP_RANGE_668

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | VLS_OK |
| 0x01 | VLS_L |
| 0x02 | VLS_H_OC |
| 0x03 | VLS_AFS_OC |
| 0xFF | undefiniert |

<a id="table-cnv-s-5-laco-range-694"></a>
### _CNV_S_5_LACO_RANGE_694

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | 1:OL_CDN |
| 0x02 | 2:CL |
| 0x04 | 4:OL_INTR |
| 0x08 | 8:OL_ERR |
| 0x10 | 10:CL_ERR |
| 0xFF | undefiniert |

<a id="table-cnv-s-6-range-stat-105"></a>
### _CNV_S_6_RANGE_STAT_105

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | PASSIVE |
| 0x01 | CONST_DRIVE |
| 0x03 | RESUME |
| 0x05 | SET_ACC |
| 0x07 | RETARD |
| 0x09 | TIP |
| 0xFF | undefiniert |

<a id="table-cnv-s-6-range-stat-146"></a>
### _CNV_S_6_RANGE_STAT_146

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | ES |
| 0x01 | ST |
| 0x02 | IS |
| 0x03 | PL |
| 0x04 | PU |
| 0x05 | PUC |
| 0xFF | undefiniert |

<a id="table-cnv-s-6-range-stat-304"></a>
### _CNV_S_6_RANGE_STAT_304

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | ETC_NO_LIH |
| 0x01 | ETC_LIH_1 |
| 0x02 | ETC_LIH_2_REV |
| 0x04 | ETC_LIH_2 |
| 0x08 | ETC_LIH_3 |
| 0x10 | ETC_LIH_4 |
| 0xFF | undefiniert |

<a id="table-cnv-s-7-def-ba-400"></a>
### _CNV_S_7_DEF_BA_400

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | KEINE |
| 0x01 | UGD |
| 0x02 | GD |
| 0x03 | GD_KLEINER_HUB |
| 0x06 | DKNOTL |
| 0x07 | VVTNOTL1 |
| 0x08 | VVTNOTL |
| 0xFF | undefiniert |

<a id="table-cnv-s-7-egcp-range-639"></a>
### _CNV_S_7_EGCP_RANGE_639

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | LSH_OFF |
| 0x01 | LSH_POW_RISE |
| 0x02 | LSH_POW_RED |
| 0x03 | LSH_POW_FALL |
| 0x04 | LSH_POW_CTL |
| 0x05 | LSH_VB_PROT |
| 0x06 | LSH_TEMP_PROT |
| 0xFF | undefiniert |

<a id="table-cnv-s-7-range-ecu-142"></a>
### _CNV_S_7_RANGE_ECU__142

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | ENG_STOP |
| 0x01 | RUN_ENG |
| 0x02 | SYN_ENG_IGK_ON |
| 0x03 | SYN_ENG_IGK_OFF |
| 0x04 | PWL |
| 0x05 | ENG_LOCK |
| 0x06 | WAKE_UP |
| 0xFF | undefiniert |

<a id="table-cnv-s-7-range-stat-325"></a>
### _CNV_S_7_RANGE_STAT_325

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | VAR_ECU_ROM_PLAUS |
| 0x5A5A | VAR_ECU_LOT1 |
| 0xA5A5 | VAR_ECU_LOT2 |
| 0xAEAE | VAR_ECU_LOT4 |
| 0xBCBC | VAR_ECU_SERIAL_ECU |
| 0xEAEA | VAR_ECU_LOT3 |
| 0xFFFF | VAR_ECU_NOT_LEARNED |
| 0xFFFF | undefiniert |

<a id="table-cnv-s-8-range-stat-18"></a>
### _CNV_S_8_RANGE_STAT_18

Dimensions: 9 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | None |
| 0x01 | Set-Acc-TipUp |
| 0x02 | Decelerate-TipDown |
| 0x03 | Resume |
| 0x04 | Off |
| 0x05 | - |
| 0x06 | - |
| 0x07 | Error |
| 0xFF | undefiniert |

<a id="table-stat-ruhestrom"></a>
### STAT_RUHESTROM

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | 0 keine Ruhestromverletzung, keine Standverbraucher aktiv |
| 0x01 | 1 Ruhestrom 80 bis 200mA aktiv, keine Standverbraucher aktiv |
| 0x02 | 2 Ruhestrom 200 bis 1000mA aktiv, keine Standverbraucher aktiv |
| 0x03 | 3 Ruhestrom über 1000mA aktiv, keine Standverbraucher aktiv |
| 0x04 | 4 keine Ruhestromverletzung, Standverbraucher Licht aktiv |
| 0x05 | 5 Ruhestrom 80 bis 200mA aktiv, Standverbraucher Licht aktiv |
| 0x06 | 6 Ruhestrom 200 bis 1000mA aktiv, Standverbraucher Licht aktiv |
| 0x07 | 7 Ruhestrom über 1000mA aktiv, Standverbraucher Licht aktiv |
| 0x08 | 8 keine Ruhestromverletzung, Standverbraucher Standheizung aktiv |
| 0x09 | 9 Ruhestrom 80 bis 200mA aktiv, Standverbraucher Standheizung aktiv |
| 0x0A | 10 Ruhestrom 200 bis 1000mA aktiv, Standverbraucher Standheizung aktiv |
| 0x0B | 11 Ruhestrom über 1000mA aktiv, Standverbraucher Standheizung aktiv |
| 0x0C | 12 keine Ruhestromverletzung, Standverbraucher Sonstige aktiv |
| 0x0D | 13 Ruhestrom 80 bis 200mA aktiv, Standverbraucher Sonstige aktiv |
| 0x0E | 14 Ruhestrom 200 bis 1000mA aktiv, Standverbraucher Sonstige aktiv |
| 0x0F | 15 Ruhestrom über 1000mA aktiv, Standverbraucher Sonstige aktiv |
| 0xFF | 255 Status unbekannt |
