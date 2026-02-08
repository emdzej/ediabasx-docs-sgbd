# MEV9N46L.prg

- Jobs: [236](#jobs)
- Tables: [43](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MEV9 fuer N46-Motoren  |
| ORIGIN | BMW EA-53 Rigl |
| REVISION | 3.001 |
| AUTHOR | EA-53 EA-53 S.Rigl |
| COMMENT | SGBD fuer N46-Layer  |
| PACKAGE | 1.26 |
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
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers Modus  : Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers $16xx SubbusMemberSerialNumber Modus  : Default
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
- [DATA_ID_LESEN](#job-data-id-lesen) - Data-ID des SG auslesen
- [STEUERN_VVT_ANSCHLAG](#job-steuern-vvt-anschlag) - Lernen der VVT-Anschlaege
- [STATUS_VVT_ANSCHLAG](#job-status-vvt-anschlag) - Status Lernen VVT-Anschlaege
- [STOP_VVT_ANSCHLAG](#job-stop-vvt-anschlag) - Ende von Lernen der VVT-Anschlaege
- [FS_HEX_LESEN](#job-fs-hex-lesen) - Fehlerspeicher auslesen als Hex Dump
- [STEUERN_EV_1](#job-steuern-ev-1) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_2](#job-steuern-ev-2) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_3](#job-steuern-ev-3) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_4](#job-steuern-ev-4) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_5](#job-steuern-ev-5) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_6](#job-steuern-ev-6) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_7](#job-steuern-ev-7) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_8](#job-steuern-ev-8) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_1_AUS](#job-steuern-ev-1-aus) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_2_AUS](#job-steuern-ev-2-aus) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_3_AUS](#job-steuern-ev-3-aus) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_4_AUS](#job-steuern-ev-4-aus) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_5_AUS](#job-steuern-ev-5-aus) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_6_AUS](#job-steuern-ev-6-aus) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_7_AUS](#job-steuern-ev-7-aus) - Stellgliedansteuerung Einspritzventile
- [STEUERN_EV_8_AUS](#job-steuern-ev-8-aus) - Stellgliedansteuerung Einspritzventile
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - Stellgliedansteuerung E-Luefter
- [STEUERN_E_LUEFTER_AUS](#job-steuern-e-luefter-aus) - Stellgliedansteuerung E-Luefter
- [STEUERN_SLP](#job-steuern-slp) - Stellgliedansteuerung SLP
- [STEUERN_SLP_AUS](#job-steuern-slp-aus) - Stellgliedansteuerung SLP
- [START_SYSTEMCHECK_TEV_FUNC](#job-start-systemcheck-tev-func) - Systemtest von TEV
- [STATUS_SYSTEMCHECK_TEV_FUNC](#job-status-systemcheck-tev-func) - Status Systemtest TEV
- [STOP_SYSTEMCHECK_TEV_FUNC](#job-stop-systemcheck-tev-func) - Beenden von TEV-Systemtest
- [STEUERN_TEV_AUS](#job-steuern-tev-aus) - Stellgliedansteuerung TEV vom Tester an DME freigeben
- [STEUERN_TEV](#job-steuern-tev) - Stellgliedansteuerung TEV
- [STEUERN_KFK](#job-steuern-kfk) - Stellgliedansteuerung KFK
- [STEUERN_KFK_AUS](#job-steuern-kfk-aus) - Stellgliedansteuerung KFK
- [STEUERN_SLV](#job-steuern-slv) - Stellgliedansteuerung SLV
- [STEUERN_SLV_AUS](#job-steuern-slv-aus) - Stellgliedansteuerung SLV
- [STEUERN_EKP](#job-steuern-ekp) - Stellgliedansteuerung EKP
- [STEUERN_EKP_AUS](#job-steuern-ekp-aus) - Stellgliedansteuerung EKP
- [STEUERN_HLS1](#job-steuern-hls1) - Stellgliedansteuerung Lambdasondenheizung1
- [STEUERN_HLS1_AUS](#job-steuern-hls1-aus) - Stellgliedansteuerung Lambdasondeheizung 1 aus
- [STEUERN_HLS2](#job-steuern-hls2) - Stellgliedansteuerung Lambdasondenheizung 2
- [STEUERN_HLS2_AUS](#job-steuern-hls2-aus) - Stellgliedansteuerung Lambdasondeheizung 2 aus
- [STEUERN_HLS3](#job-steuern-hls3) - Stellgliedansteuerung Lambdasondenheizung3
- [STEUERN_HLS3_AUS](#job-steuern-hls3-aus) - Stellgliedansteuerung Lambdasondeheizung 3 aus
- [STEUERN_HLS4](#job-steuern-hls4) - Stellgliedansteuerung Lambdasondenheizung 4
- [STEUERN_HLS4_AUS](#job-steuern-hls4-aus) - Stellgliedansteuerung Lambdasondeheizung 4 aus
- [STEUERN_STA](#job-steuern-sta) - Stellgliedansteuerung Startrelais
- [STEUERN_STA_AUS](#job-steuern-sta-aus) - Stellgliedansteuerung Startrelais aus
- [STEUERN_KOE](#job-steuern-koe) - Stellgliedansteuerung KOREL
- [STEUERN_KOE_AUS](#job-steuern-koe-aus) - Stellgliedansteuerung KOREL aus
- [STEUERN_EBL](#job-steuern-ebl) - Stellgliedansteuerung E-Box-Luefter
- [STEUERN_EBL_AUS](#job-steuern-ebl-aus) - Stellgliedansteuerung E-Box-Luefter aus
- [STEUERN_AGK](#job-steuern-agk) - Stellgliedansteuerung Abgasklappe
- [STEUERN_AGK_AUS](#job-steuern-agk-aus) - Stellgliedansteuerung Abgasklappe aus
- [STEUERN_DMTLP](#job-steuern-dmtlp) - Stellgliedansteuerung DM-TL Pumpe
- [STEUERN_DMTLP_AUS](#job-steuern-dmtlp-aus) - Stellgliedansteuerung DM-TL Pumpe aus
- [STEUERN_DMTLV](#job-steuern-dmtlv) - Stellgliedansteuerung DM-TL Ventil
- [STEUERN_DMTLV_AUS](#job-steuern-dmtlv-aus) - Stellgliedansteuerung DM-TL Ventil aus
- [RAM_LESEN](#job-ram-lesen) - Beliebige RAM - Zellen auslesen
- [RAM_BACKUP](#job-ram-backup) - Loeschen der RAM-Backup-Werte
- [START_SYSTEMCHECK_LLERH](#job-start-systemcheck-llerh) - Diagnosefunktion LL-Erhoehung
- [STATUS_SYSTEMCHECK_LLERH](#job-status-systemcheck-llerh) - Diagnosefunktion LL-Erhoehung Status lesen
- [STOP_SYSTEMCHECK_LLERH](#job-stop-systemcheck-llerh) - Diagnosefunktion LL-Erhoehung Status lesen
- [START_SYSTEMCHECK_DMTL](#job-start-systemcheck-dmtl) - Start Systemtest DMTL
- [STATUS_SYSTEMCHECK_DMTL](#job-status-systemcheck-dmtl) - Status Systemtest DMTL
- [STOP_SYSTEMCHECK_DMTL](#job-stop-systemcheck-dmtl) - Ende Systemtest DM-TL
- [STEUERN_VANOS_EINLASS](#job-steuern-vanos-einlass) - Stellgliedansteuerung Einlass-VANOS
- [STEUERN_VANOS_EINLASS_AUS](#job-steuern-vanos-einlass-aus) - Stellgliedansteuerung Einlass-VANOS freigeben
- [STEUERN_VANOS_AUSLASS](#job-steuern-vanos-auslass) - Stellgliedansteuerung Auslass-VANOS
- [STEUERN_VANOS_AUSLASS_AUS](#job-steuern-vanos-auslass-aus) - Stellgliedansteuerung Auslass-VANOS freigeben
- [STEUERN_DISA](#job-steuern-disa) - Stellgliedansteuerung DISA
- [STEUERN_DISA_AUS](#job-steuern-disa-aus) - Stellgliedansteuerung DISA freigeben
- [STEUERN_EVAUSBL](#job-steuern-evausbl) - Systemdiagnose Einspritzventile ausblenden
- [STEUERN_EVAUSBL_AUS](#job-steuern-evausbl-aus) - Ende Systemtest DM-TL
- [STATUS_MESSWERTE](#job-status-messwerte) - Auslesen von Messwerten
- [STATUS_BATTERIEINTEGRATOR](#job-status-batterieintegrator) - Auslesen von Messwertenund Statusflags
- [STATUS_SCHALTERSTATI](#job-status-schalterstati) - Auslesen von SchalterStatusflags
- [STATUS_FUNKTIONSSTATI](#job-status-funktionsstati) - Auslesen von SchalterStatusflags
- [STATUS_LAUFUNRUHE](#job-status-laufunruhe) - Auslesen von Laufunruhewerten
- [STATUS_DKHFM](#job-status-dkhfm) - Auslesen von DK/HFM-Abgleichswerten
- [STATUS_SAUGROHR](#job-status-saugrohr) - Auslesen von EISY-Größen
- [FS_LESEN_LANG](#job-fs-lesen-lang) - Fehlerspeicher auslesen
- [STEUERN_VVT](#job-steuern-vvt) - Stellgliedansteuerung VVT
- [STEUERN_VVT_AUS](#job-steuern-vvt-aus) - beenden Stellgliedansteuerung VVT
- [STATUS_CO_ABGLEICH](#job-status-co-abgleich) - Auslesen des LL-CO-Wertes
- [STEUERN_CO_ABGLEICH_VERSTELLEN](#job-steuern-co-abgleich-verstellen) - LL-CO-Wert vorgeben
- [STEUERN_CO_ABGLEICH_PROGRAMMIEREN](#job-steuern-co-abgleich-programmieren) - LL-CO-WERT programmieren
- [STATUS_GEMISCH](#job-status-gemisch) - Auslesen von Gemischwerten
- [STATUS_AUSGAENGE](#job-status-ausgaenge) - Auslesen von Ausgaengen
- [STATUS_NWGADAPTION](#job-status-nwgadaption) - Auslesen der NWG-Adaptionen
- [STATUS_VARIANTE](#job-status-variante) - Auslesen der Variante
- [ECU_CONFIG](#job-ecu-config) - Auslesen der Variante
- [STEUERN_VARIANTE](#job-steuern-variante) - Loeschen der Varianten
- [STATUS_KVA](#job-status-kva) - Auslesen Faktor KVA
- [STEUERN_KVA](#job-steuern-kva) - Faktor KVA Korrektur vorgeben
- [STATUS_READINESS](#job-status-readiness) - Auslesen des Readinessbyte
- [STATUS_FGR](#job-status-fgr) - Auslesen des FGR-Statuses
- [STEUERN_LLABG](#job-steuern-llabg) - LL-Abgleichswerte werden vorgegeben
- [STEUERN_LLABG_PROG](#job-steuern-llabg-prog) - LL-Abgleichswerte werden programmiert
- [STATUS_LLABG](#job-status-llabg) - LL-Abgleichswerte werden gelesen
- [IDENT_AIF](#job-ident-aif) - Identdaten mit KWP2000: $1A ReadECUIdentification Modus  : Default Auslesen des Anwender Informations Feldes mit KWP 2000: $23 ReadMemoryByAddress Standard Flashjob Modus   : Default
- [STATUS_VVT](#job-status-vvt) - Auslesen VVT-Messwerte
- [STATUS_DIFFERENZDRUCKSENSOR](#job-status-differenzdrucksensor) - Werte des Differenzdrucksensors im Ansaugluftsystem
- [STATUS_FASTA1](#job-status-fasta1) - Auslesen FASTA-Messwertblock 1
- [STATUS_FASTA2](#job-status-fasta2) - Auslesen FASTA-Messwertblock 2
- [STATUS_FASTA3](#job-status-fasta3) - Auslesen FASTA-Messwertblock 3
- [STATUS_FASTA4](#job-status-fasta4) - Auslesen FASTA-Messwertblock 4
- [STATUS_FASTA5](#job-status-fasta5) - Auslesen FASTA-Messwertblock 5
- [STATUS_FASTA6](#job-status-fasta6) - Auslesen FASTA-Messwertblock 6
- [STATUS_FASTA7](#job-status-fasta7) - Auslesen FASTA-Messwertblock 7
- [STATUS_ADC](#job-status-adc) - Auslesen ADC-Werte
- [STEUERN_LL_ERH](#job-steuern-ll-erh) - Diagnosefunktion LL-Erhoehung
- [START_SYSTEMCHECK_LSU](#job-start-systemcheck-lsu) - Systemdiagnose LSU starten
- [STATUS_SYSTEMCHECK_LSU](#job-status-systemcheck-lsu) - Status Systemdiagnose LSU
- [STOP_SYSTEMCHECK_LSU](#job-stop-systemcheck-lsu) - Ende Systemdiagnose LSU
- [START_SYSTEMCHECK_KAT](#job-start-systemcheck-kat) - Systemdiagnose KAT
- [STOP_SYSTEMCHECK_KAT](#job-stop-systemcheck-kat) - Ende Systemdiagnose KAT
- [START_SYSTEMCHECK_LSH](#job-start-systemcheck-lsh) - Start der Systemdiagnose LSH
- [STATUS_SYSTEMCHECK_LSH](#job-status-systemcheck-lsh) - Status LSH-Diagnose auslesen
- [STOP_SYSTEMCHECK_LSH](#job-stop-systemcheck-lsh) - Ende der Systemdiagnose LSH
- [START_SYSTEMCHECK_GRUNDADAPT](#job-start-systemcheck-grundadapt) - Systemdiagnose Grundadaptionenen
- [STATUS_SYSTEMCHECK_GRUNDADAPT](#job-status-systemcheck-grundadapt) - Status Systemdiagnose Grundadaptionen starten
- [STOP_SYSTEMCHECK_GRUNDADAPT](#job-stop-systemcheck-grundadapt) - Ende Systemdiagnose Grundadaptionen starten
- [START_SYSTEMCHECK_GEMISCHADAPT_SPERR](#job-start-systemcheck-gemischadapt-sperr) - Systemdiagnose Gemischadaptionen sperren
- [STOP_SYSTEMCHECK_GEMISCHADAPT_SPERR](#job-stop-systemcheck-gemischadapt-sperr) - Ende Systemdiagnose Gemischadaptionen sperren
- [START_SYSTEMCHECK_LAMBDA_AUS](#job-start-systemcheck-lambda-aus) - Systemdiagnose Labdaregelung aus
- [STATUS_SYSTEMCHECK_LAMBDA_AUS](#job-status-systemcheck-lambda-aus) - Status Systemdiagnose Lambdaregelung aus
- [STOP_SYSTEMCHECK_LAMBDA_AUS](#job-stop-systemcheck-lambda-aus) - Ende Systemdiagnose Lambdaregelung aus
- [START_SYSTEMCHECK_KOMPRESSION](#job-start-systemcheck-kompression) - Systemdiagnose Kompressionstest
- [STOP_SYSTEMCHECK_KOMPRESSION](#job-stop-systemcheck-kompression) - Ende Systemdiagnose Kompressiostest
- [STEUERN_ZWANG_RAMBACKUP](#job-steuern-zwang-rambackup) - Zwangssichern der RAM-Backup-Werte
- [STEUERN_POWER_DOWN](#job-steuern-power-down) - Anforderung Power Down Mode
- [STEUERN_DISA_ANSCHLAG](#job-steuern-disa-anschlag) - lernen der DISA-Anschlaege
- [STATUS_DISA_ANSCHLAG](#job-status-disa-anschlag) - Status Lernen der DISA-Anschlaege
- [STOP_DISA_ANSCHLAG](#job-stop-disa-anschlag) - Ende des Lernes DISA-Anschlaege
- [START_SYSTEMCHECK_SEK_LUFT](#job-start-systemcheck-sek-luft) - Systemdiagnose SLS
- [STATUS_SYSTEMCHECK_SEK_LUFT](#job-status-systemcheck-sek-luft) - Status Systemdiagnose SLS
- [STOP_SYSTEMCHECK_SEK_LUFT](#job-stop-systemcheck-sek-luft) - Ende Systemdiagnose SLS
- [STEUERN_ADAPTIONEN_LOESCHEN](#job-steuern-adaptionen-loeschen) - Loeschen der Adaptionswerte
- [STEUERN_ADAPTIONEN_LOESCHEN_NEU](#job-steuern-adaptionen-loeschen-neu) - Loeschen der Adaptionswerte
- [STATUS_MINHUB](#job-status-minhub) - Auslesen des VVT-Minhubes
- [STEUERN_MINHUB](#job-steuern-minhub) - Vorgeben des VVT-Minhubes
- [STEUERN_MINHUB_PROGRAMM](#job-steuern-minhub-programm) - Programmieren des VVT-Minhubes
- [STATUS_BANKABGLEICH](#job-status-bankabgleich) - Auslesen des VVT-Bankabgleiches
- [STEUERN_BANKABGLEICH_PROGRAMM](#job-steuern-bankabgleich-programm) - Programmieren des VVT-Minhubes
- [STATUS_BETRIEBSSTUNDENZAEHLER](#job-status-betriebsstundenzaehler) - Status Betriebsstundenzaehler auslesen
- [STATUS_SYSTEMCHECK_KAT](#job-status-systemcheck-kat) - Status Systemtest KAT
- [EWS_STARTWERT](#job-ews-startwert) - EWS-Startwertinitialisierung
- [EWS_EMPFANG](#job-ews-empfang) - EWS-Empfangsstatus auslesen
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - Auslesen der Motortemperatur
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Auslesen der Motordrehzahl
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - Auslesen der Lufttemperatur
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - Auslesen der Luftmasse
- [STATUS_L_SONDE](#job-status-l-sonde) - Auslesen der Lambdasondenspannung vorne Bank 1
- [STATUS_L_SONDE_2](#job-status-l-sonde-2) - Auslesen der Lambdasondenspannung vorne Bank 2
- [STATUS_L_SONDE_H](#job-status-l-sonde-h) - Auslesen der Lambdasondenspannung hinten Bank 1
- [STATUS_L_SONDE_2_H](#job-status-l-sonde-2-h) - Auslesen der Lambdasondenspannung hinten Bank 2
- [STATUS_INT](#job-status-int) - Auslesen der Lambdaregelung
- [STATUS_INT_2](#job-status-int-2) - Auslesen der Lambdaregelung Bank2
- [STATUS_ADD](#job-status-add) - Auslesen der additiven Lambdaregelung
- [STATUS_ADD_2](#job-status-add-2) - Auslesen der additiven Lambdaregelung Bank2
- [STATUS_MUL](#job-status-mul) - Auslesen der multipikativen Lambdaregelung
- [STATUS_MUL_2](#job-status-mul-2) - Auslesen der multipikativen Lambdaregelung Bank 2
- [STATUS_MOTORLAUFUNRUHE](#job-status-motorlaufunruhe) - Auslesen der Laufunruhewerte
- [STATUS_UBATT](#job-status-ubatt) - Auslesen der Batteriespannung
- [STATUS_GEBERRAD_ADAPTION](#job-status-geberrad-adaption) - Auslesen der NWG-Adaptionen
- [STATUS_DIGITAL](#job-status-digital) - Auslesen von SchalterStatusflags
- [STATUS_PWG_POTI_SPANNUNG](#job-status-pwg-poti-spannung) - Auslesen des Pedalwertgebers
- [WECHSELCODE_SYNC_DME](#job-wechselcode-sync-dme) - EWS zuruecksetzen
- [TESTER](#job-tester) - Ausfuehren eines Telegramms mit Uebergabe nur der Daten 
- [STATUS_OELSENSOR](#job-status-oelsensor) - Temperatur, Niveau, Permitivitaet
- [IDENT_GENERATOR](#job-ident-generator)
- [START_SYSTEMCHECK_LSHV](#job-start-systemcheck-lshv)
- [STOP_SYSTEMCHECK_LSHV](#job-stop-systemcheck-lshv)
- [STATUS_SYSTEMCHECK_LSHV](#job-status-systemcheck-lshv)
- [STEUERN_EKP_SPERREN](#job-steuern-ekp-sperren)
- [STEUERN_EKP_SPERREN_AUS](#job-steuern-ekp-sperren-aus)
- [IDENT_IBS](#job-ident-ibs) - $22 40 21 BMW Nr, Seriennummer, SW/HW Index
- [STATUS_SYSTEMCHECK_PM_INFO_1](#job-status-systemcheck-pm-info-1) - $22 40 22 Bytefeld 1 Batterie Powermanagement lesen
- [STATUS_SYSTEMCHECK_PM_INFO_2](#job-status-systemcheck-pm-info-2) - $22 40 23 Bytefeld 2 Batterie Powermanagement lesen
- [STEUERN_PM_HISTOGRAM_RESET](#job-steuern-pm-histogram-reset) - $30 F5 04 Loeschen von pminfo1 index 23-30
- [ADAP_SELEKTIV_LOESCHEN](#job-adap-selektiv-loeschen) - Löschen von Adaptionen und gelernte Varianten KWP 2000 $31 30 xx xx xx Loeschen der Adaptionswerte
- [STEUERN_BATTERIETAUSCH_REGISTRIEREN](#job-steuern-batterietausch-registrieren) - KWP 2000 $31 30 00 10 00 Bit setzen Batterietausch registrieren
- [START_SYSTEMCHECK_PM_MESSEMODE](#job-start-systemcheck-pm-messemode) - $31 F6 Systemdiagnose BatterieSensor reset
- [STOP_SYSTEMCHECK_PM_MESSEMODE](#job-stop-systemcheck-pm-messemode) - $32 F6 Systemdiagnose BatterieSensor reset beenden

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

_No arguments._

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

<a id="job-sensoren-anzahl-lesen"></a>
### SENSOREN_ANZAHL_LESEN

Anzahl der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SENSOR_ANZAHL | long | Anzahl der intelligenten Subbussensoren |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sensoren-ident-lesen"></a>
### SENSOREN_IDENT_LESEN

Identifikation der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers $16xx SubbusMemberSerialNumber Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_NR | long | optionales Argument gewuenschter Sensor xx (0x01 - 0xFF) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SENSOR_VERBAUORT | string | Verbauort des Sensors table VerbauortTabelle ORTTEXT |
| SENSOR_BMW_NR | string | BMW-Teilenummer des Sensors |
| SENSOR_PART_NR | string | Teilenummer des Sensors optional wenn SENSOR_BMW_NR gueltig wenn vom Teilenummer vom Sensor nicht verfuegbar dann '--' |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

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

<a id="job-data-id-lesen"></a>
### DATA_ID_LESEN

Data-ID des SG auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| DATA_ID | string | ASCII-String fuer Data-ID |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt-anschlag"></a>
### STEUERN_VVT_ANSCHLAG

Lernen der VVT-Anschlaege

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vvt-anschlag"></a>
### STATUS_VVT_ANSCHLAG

Status Lernen VVT-Anschlaege

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VVT_ANSCHL1 | int | Status des Lernens Bank1 |
| STAT_VVT_ANSCHL1_TEXT | string | Status des Lernens Bank1 |
| STAT_VVT_ANSCHL2 | int | Status des Lernens Bank2 |
| STAT_VVT_ANSCHL2_TEXT | string | Status des Lernens Bank2 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-vvt-anschlag"></a>
### STOP_VVT_ANSCHLAG

Ende von Lernen der VVT-Anschlaege

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-hex-lesen"></a>
### FS_HEX_LESEN

Fehlerspeicher auslesen als Hex Dump

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLERNR | int | wird die Nummer des zu lesenden Fehlers im Fehlerspeicher uebergeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| F_ANZ_INT | int | Anzahl der eingetragenen Fehler |
| FEHLER_NR_TEXT | string | Fehlernummer im Speicher |
| FS_ZEILE1 | string | 10 Byte des Fehlerspeichers als Dump |
| FS_ZEILE2 | string | naechsten 10 Byte aus FS |
| FS_ZEILE3 | string | naechsten 10 Byte aus FS |
| FS_ZEILE4 | string | naechsten 10 Byte aus FS |
| FS_ZEILE5 | string | naechsten 10 Byte aus FS |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-1"></a>
### STEUERN_EV_1

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-2"></a>
### STEUERN_EV_2

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-3"></a>
### STEUERN_EV_3

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-4"></a>
### STEUERN_EV_4

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-5"></a>
### STEUERN_EV_5

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-6"></a>
### STEUERN_EV_6

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-7"></a>
### STEUERN_EV_7

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-8"></a>
### STEUERN_EV_8

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | sHex-Antwort von SG |

<a id="job-steuern-ev-1-aus"></a>
### STEUERN_EV_1_AUS

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-2-aus"></a>
### STEUERN_EV_2_AUS

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-3-aus"></a>
### STEUERN_EV_3_AUS

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-4-aus"></a>
### STEUERN_EV_4_AUS

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-5-aus"></a>
### STEUERN_EV_5_AUS

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-6-aus"></a>
### STEUERN_EV_6_AUS

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-7-aus"></a>
### STEUERN_EV_7_AUS

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ev-8-aus"></a>
### STEUERN_EV_8_AUS

Stellgliedansteuerung Einspritzventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

Stellgliedansteuerung E-Luefter

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTRATE | int | zwischen 10 und 95 % Ansteuerverhaeltins |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-e-luefter-aus"></a>
### STEUERN_E_LUEFTER_AUS

Stellgliedansteuerung E-Luefter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-slp"></a>
### STEUERN_SLP

Stellgliedansteuerung SLP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-slp-aus"></a>
### STEUERN_SLP_AUS

Stellgliedansteuerung SLP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-tev-func"></a>
### START_SYSTEMCHECK_TEV_FUNC

Systemtest von TEV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-tev-func"></a>
### STATUS_SYSTEMCHECK_TEV_FUNC

Status Systemtest TEV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_TEV_FUNC_WERT | int | Status der TEV-Diagnose |
| STAT_SYSTEMCHECK_TEV_FUNC_TEXT | string | Status der TEV-Diagnose |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-tev-func"></a>
### STOP_SYSTEMCHECK_TEV_FUNC

Beenden von TEV-Systemtest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tev-aus"></a>
### STEUERN_TEV_AUS

Stellgliedansteuerung TEV vom Tester an DME freigeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

Stellgliedansteuerung TEV

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANSTEUERRATE | int | Sollwert 0 - 100% |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kfk"></a>
### STEUERN_KFK

Stellgliedansteuerung KFK

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kfk-aus"></a>
### STEUERN_KFK_AUS

Stellgliedansteuerung KFK

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-slv"></a>
### STEUERN_SLV

Stellgliedansteuerung SLV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-slv-aus"></a>
### STEUERN_SLV_AUS

Stellgliedansteuerung SLV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

Stellgliedansteuerung EKP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ekp-aus"></a>
### STEUERN_EKP_AUS

Stellgliedansteuerung EKP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls1"></a>
### STEUERN_HLS1

Stellgliedansteuerung Lambdasondenheizung1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls1-aus"></a>
### STEUERN_HLS1_AUS

Stellgliedansteuerung Lambdasondeheizung 1 aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls2"></a>
### STEUERN_HLS2

Stellgliedansteuerung Lambdasondenheizung 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls2-aus"></a>
### STEUERN_HLS2_AUS

Stellgliedansteuerung Lambdasondeheizung 2 aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls3"></a>
### STEUERN_HLS3

Stellgliedansteuerung Lambdasondenheizung3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls3-aus"></a>
### STEUERN_HLS3_AUS

Stellgliedansteuerung Lambdasondeheizung 3 aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls4"></a>
### STEUERN_HLS4

Stellgliedansteuerung Lambdasondenheizung 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls4-aus"></a>
### STEUERN_HLS4_AUS

Stellgliedansteuerung Lambdasondeheizung 4 aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sta"></a>
### STEUERN_STA

Stellgliedansteuerung Startrelais

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sta-aus"></a>
### STEUERN_STA_AUS

Stellgliedansteuerung Startrelais aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-koe"></a>
### STEUERN_KOE

Stellgliedansteuerung KOREL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-koe-aus"></a>
### STEUERN_KOE_AUS

Stellgliedansteuerung KOREL aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ebl"></a>
### STEUERN_EBL

Stellgliedansteuerung E-Box-Luefter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ebl-aus"></a>
### STEUERN_EBL_AUS

Stellgliedansteuerung E-Box-Luefter aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-agk"></a>
### STEUERN_AGK

Stellgliedansteuerung Abgasklappe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-agk-aus"></a>
### STEUERN_AGK_AUS

Stellgliedansteuerung Abgasklappe aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlp"></a>
### STEUERN_DMTLP

Stellgliedansteuerung DM-TL Pumpe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlp-aus"></a>
### STEUERN_DMTLP_AUS

Stellgliedansteuerung DM-TL Pumpe aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlv"></a>
### STEUERN_DMTLV

Stellgliedansteuerung DM-TL Ventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlv-aus"></a>
### STEUERN_DMTLV_AUS

Stellgliedansteuerung DM-TL Ventil aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ram-lesen"></a>
### RAM_LESEN

Beliebige RAM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |
| RAM_LESEN_ANZAHL_BYTE | long | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| RAM_LESEN_WERT | binary | nichts |
| RAM_LESEN_EINH | string | Einheit HEX |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ram-backup"></a>
### RAM_BACKUP

Loeschen der RAM-Backup-Werte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-llerh"></a>
### START_SYSTEMCHECK_LLERH

Diagnosefunktion LL-Erhoehung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LL_WERT | int | gesetzter LL-Sollwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-llerh"></a>
### STATUS_SYSTEMCHECK_LLERH

Diagnosefunktion LL-Erhoehung Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LL_TEXT | string | Status der Diagnose |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-llerh"></a>
### STOP_SYSTEMCHECK_LLERH

Diagnosefunktion LL-Erhoehung Status lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-dmtl"></a>
### START_SYSTEMCHECK_DMTL

Start Systemtest DMTL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-dmtl"></a>
### STATUS_SYSTEMCHECK_DMTL

Status Systemtest DMTL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_POINTER_VALUE | int | Wert des Zustandspointer der DMTL-Diagnose |
| STAT_POINTER | string | Zustandspointer der DMTL-Diagnose |
| STAT_POINTER_FREEZE | string | Zustandspointer der DMTL-Diagnose |
| STAT_POINTER_FREEZE_VALUE | int | Zustandspointer der DMTL-Diagnose |
| STAT_DMTLDIAG_TEXT | string | Status der DMTL-Diagnose |
| STAT_IPTESKF_TEXT | string | Pumpenstrom DM-TL gefiltert |
| STAT_IPGLMN_TEXT | string | minimaler Pumpenstrom Grobleckmessung |
| STAT_IPTREF_TEXT | string | Pumpenstrom Referenzleck |
| STAT_IPTESKF_WERT | real | Pumpenstrom DM-TL gefiltert |
| STAT_IPGLMN_WERT | real | minimaler Pumpenstrom Grobleckmessung |
| STAT_IPTREF_WERT | real | Pumpenstrom Referenzleck |
| STAT_IPT_EINH | string | Einheit der Stroeme |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-dmtl"></a>
### STOP_SYSTEMCHECK_DMTL

Ende Systemtest DM-TL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vanos-einlass"></a>
### STEUERN_VANOS_EINLASS

Stellgliedansteuerung Einlass-VANOS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WINKEL | int | gibt den Verstellwinkel an (-102..102) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vanos-einlass-aus"></a>
### STEUERN_VANOS_EINLASS_AUS

Stellgliedansteuerung Einlass-VANOS freigeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vanos-auslass"></a>
### STEUERN_VANOS_AUSLASS

Stellgliedansteuerung Auslass-VANOS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WINKEL | int | gibt den Verstellwinkel an (-102..102) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vanos-auslass-aus"></a>
### STEUERN_VANOS_AUSLASS_AUS

Stellgliedansteuerung Auslass-VANOS freigeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-disa"></a>
### STEUERN_DISA

Stellgliedansteuerung DISA

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WINKEL | int | gibt den Verstellwinkel an (0..100) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-disa-aus"></a>
### STEUERN_DISA_AUS

Stellgliedansteuerung DISA freigeben

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-evausbl"></a>
### STEUERN_EVAUSBL

Systemdiagnose Einspritzventile ausblenden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VENTIL_NR | int | gibt die Ventile (binaer, jedes Bit ein EV) an, die ausgeblendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-evausbl-aus"></a>
### STEUERN_EVAUSBL_AUS

Ende Systemtest DM-TL

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VENTIL_NR | int | gibt die Ventile (binaer, jedes Bit ein EV) an, die ausgeblendet werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte"></a>
### STATUS_MESSWERTE

Auslesen von Messwerten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_TE_WERT | real | Wert von TE_W |
| STAT_TE_EINH | string | Einheit von TE_W |
| STAT_FR_WERT | real | Wert von FR_W |
| STAT_FR_EINH | string | Einheit von FR_W |
| STAT_FR2_WERT | real | Wert von FR_W |
| STAT_FR2_EINH | string | Einheit von FR_W |
| STAT_VFZG_WERT | real | Wert von VFZG |
| STAT_VFZG_EINH | string | Einheit von VFZG |
| STAT_NMOT_WERT | real | Wert von NMOT_W |
| STAT_NMOT_EINH | string | Einheit von NMOT_W |
| STAT_NSOL_WERT | real | Wert von NSOL |
| STAT_NSOL_EINH | string | Einheit von NSOL |
| STAT_WNWKWE_WERT | real | Wert von WNWKWE_W |
| STAT_WNWKWE_EINH | string | Einheit von WNWKWE_W |
| STAT_WNWKWA_WERT | real | Wert von WNWKWA_W |
| STAT_WNWKWA_EINH | string | Einheit von WNWKWA_W |
| STAT_TANS_WERT | real | Wert von TANS |
| STAT_TANS_EINH | string | Einheit von TANS |
| STAT_TMOT_WERT | real | Wert von TMOT |
| STAT_TMOT_EINH | string | Einheit von TMOT |
| STAT_ZWOUT_WERT | real | Wert von ZWOUT |
| STAT_ZWOUT_EINH | string | Einheit von ZWOUT |
| STAT_WDKBA_WERT | real | Wert von WDKBA |
| STAT_WDKBA_EINH | string | Einheit von WDKBA |
| STAT_MSHFM_WERT | real | Wert von MSHFM_W |
| STAT_MSHFM_EINH | string | Einheit von MSHFM_W |
| STAT_MIIST_WERT | real | Wert von MIIST_W |
| STAT_MIIST_EINH | string | Einheit von MIIST_W |
| STAT_UB_WERT | real | Wert von UB |
| STAT_UB_EINH | string | Einheit von UB |
| STAT_UPWG_WERT | real | Wert von UPWG_W |
| STAT_UPWG_EINH | string | Einheit von UPWG_W |
| STAT_TKA_WERT | real | Wert von TKA |
| STAT_TKA_EINH | string | Einheit von TKA |
| STAT_RKRN0_WERT | real | Wert von RKRN_W_0 |
| STAT_RKRN0_EINH | string | Einheit von RKRN_W_0 |
| STAT_RKRN1_WERT | real | Wert von RKRN_W_1 |
| STAT_RKRN1_EINH | string | Einheit von RKRN_W_1 |
| STAT_RKRN2_WERT | real | Wert von RKRN_W_2 |
| STAT_RKRN2_EINH | string | Einheit von RKRN_W_2 |
| STAT_RKRN3_WERT | real | Wert von RKRN_W_3 |
| STAT_RKRN3_EINH | string | Einheit von RKRN_W_3 |
| STAT_RKRN4_WERT | real | Wert von RKRN_W_4 |
| STAT_RKRN4_EINH | string | Einheit von RKRN_W_4 |
| STAT_RKRN5_WERT | real | Wert von RKRN_W_5 |
| STAT_RKRN5_EINH | string | Einheit von RKRN_W_5 |
| STAT_RKRN6_WERT | real | Wert von RKRN_W_6 |
| STAT_RKRN6_EINH | string | Einheit von RKRN_W_6 |
| STAT_RKRN7_WERT | real | Wert von RKRN_W_7 |
| STAT_RKRN7_EINH | string | Einheit von RKRN_W_7 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-batterieintegrator"></a>
### STATUS_BATTERIEINTEGRATOR

Auslesen von Messwertenund Statusflags

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_DFMONITOR_WERT | real | Wert von dfmonitor |
| STAT_DFMONITOR_EINH | string | Einheit von dfmonitor |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schalterstati"></a>
### STATUS_SCHALTERSTATI

Auslesen von SchalterStatusflags

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_KL15_EIN | int | Bedingung KL15 ein |
| STAT_ESTART_EIN | int | Bedingung Startrelais |
| STAT_KUPPL_EIN | int | Bedingung Kupplung betaetigt |
| STAT_BL_EIN | int | Bedingung Bremsschalter ein |
| STAT_BR_EIN | int | Bedingung Bremslichttestschalter ein |
| STAT_KO_EIN | int | Bedingung Klimakompressor ein |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-funktionsstati"></a>
### STATUS_FUNKTIONSSTATI

Auslesen von SchalterStatusflags

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_LL_EIN | int | Bedingung Leerlauf |
| STAT_VL_EIN | int | Bedingung Vollast |
| STAT_SBBHK2_EIN | int | Bedingung Lambdasondenbereitschaft hinter Kat Bank2 |
| STAT_SBBHK_EIN | int | Bedingung Lambdasondenbereitschaft hinter Kat |
| STAT_SBBVK2_EIN | int | Bedingung Lambdasondenbereitschaft vor Kat Bank2 |
| STAT_SBBVK_EIN | int | Bedingung Lambdasondenbereitschaft vor Kat |
| STAT_LR2_EIN | int | Bedingung Lambdaregelung Bank2 ein |
| STAT_LR_EIN | int | Bedingung Lambdaregelung ein |
| STAT_KD_EIN | int | Bedingung KickDown ein |
| STAT_PN_EIN | int | Bedingung Park-Neutral ein |
| STAT_ECULOCK_EIN | int | Bedingung EWS_OK ein |
| STAT_TEHB_EIN | int | Bedingung ein |
| STAT_SA_EIN | int | Bedingung Schubabschneiden ein |
| STAT_LRNRDY_EIN | int | Bedingung UMA Lernerfolg |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-laufunruhe"></a>
### STATUS_LAUFUNRUHE

Auslesen von Laufunruhewerten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_LUTSFI1_WERT | real | Wert von LUTSFI1 |
| STAT_LUTSFI1_EINH | string | Einheit von LUTSFI1 |
| STAT_LUTSFI2_WERT | real | Wert von LUTSFI2 |
| STAT_LUTSFI2_EINH | string | Einheit von LUTSFI2 |
| STAT_LUTSFI3_WERT | real | Wert von LUTSFI3 |
| STAT_LUTSFI3_EINH | string | Einheit von LUTSFI3 |
| STAT_LUTSFI4_WERT | real | Wert von LUTSFI4 |
| STAT_LUTSFI4_EINH | string | Einheit von LUTSFI4 |
| STAT_LUTSFI5_WERT | real | Wert von LUTSFI5 |
| STAT_LUTSFI5_EINH | string | Einheit von LUTSFI5 |
| STAT_LUTSFI6_WERT | real | Wert von LUTSFI6 |
| STAT_LUTSFI6_EINH | string | Einheit von LUTSFI6 |
| STAT_LUTSFI7_WERT | real | Wert von LUTSFI7 |
| STAT_LUTSFI7_EINH | string | Einheit von LUTSFI7 |
| STAT_LUTSFI8_WERT | real | Wert von LUTSFI8 |
| STAT_LUTSFI8_EINH | string | Einheit von LUTSFI8 |
| STAT_FOFR1_EIN | int | Wert von B_FOFR1 |
| STAT_UULSUV_WERT | real | Wert von UULSUV_W |
| STAT_UULSUV_EINH | string | Einheit von UULSUV_W |
| STAT_UULSUV2_WERT | real | Wert von UULSUV2_W |
| STAT_UULSUV2_EINH | string | Einheit von UULSUV2_W |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dkhfm"></a>
### STATUS_DKHFM

Auslesen von DK/HFM-Abgleichswerten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_MSNDKO_WERT | real | Wert von MSNDKO |
| STAT_MSNDKO_EINH | string | Einheit von MSNDKO |
| STAT_FKMSDKA_WERT | real | Wert von FKMSDKA |
| STAT_FKMSDKA_EINH | string | Einheit von FKMSDKA |
| STAT_FKMSDK_WERT | real | Wert von FKMSDK |
| STAT_FKMSDK_EINH | string | Einheit von FKMSDK |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-saugrohr"></a>
### STATUS_SAUGROHR

Auslesen von EISY-Größen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_EISYDKFKAF_WERT | real | Wert von EISYDKFKAF |
| STAT_EISYDKKOFF_WERT | real | Wert von EISYDKKOFF |
| STAT_EISYEVFKAF_WERT | real | Wert von EISYEVFKAF |
| STAT_EISYEVKOFF_WERT | real | Wert von EISYEVKOFF |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-lang"></a>
### FS_LESEN_LANG

Fehlerspeicher auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLERNR | int | wird die Nummer des zu lesenden Fehlers uebergeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| F_ANZ_INT | int | Anzahl der eingetragenen Fehler |
| F_ORT_NR | long | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_SYMPTOM_NR | int | Gibt die Nummer der Fehlerart aus |
| F_SYMPTOM_TEXT | string | Interpretiert die Fehlerart |
| F_READY_NR | int | Gibt an, ob Readiness gesetzt |
| F_READY_TEXT | string | gibt einen Text zur Readiness aus |
| F_VORHANDEN_NR | int | Gibt die Nummer des Eintragstatuses aus |
| F_VORHANDEN_TEXT | string | gibt die Eintragsentprellung des Fehlers an |
| F_WARNUNG_NR | int | Gibt die Nummer fuer MIL EIN aus |
| F_WARNUNG_TEXT | string | gibt an, ob die MIL angesteuert wird |
| F_ART_ERW_WERT | int | gibt das FehlerarterweiterungsByte als integer zurueck |
| F_ZYKLUS_FLAG | string | gibt an, ob Zyklus-Flag gesetzt wurden ist |
| F_AKTIV_FLAG | string | gibt an, ob Diagnose laeuft |
| F_STOP_FLAG | string | gibt an, ob Stopbedingungen vorliegen |
| F_ERROR_FLAG | string | zeigt Error-Flag an |
| F_MIL_FLAG | string | zeigt den MIL-Status an |
| F_ENTPRELL_FLAG | string | gibt den MIL-Entprellstatus an |
| F_CLA | int | Klasse |
| F_FLC | int | Wert Entprellvorgaenge FLC |
| F_HLC | int | Wert Entprellvorgaenge HLC |
| F_LZ | int | Wert Loeschvorgaenge DLC |
| F_TSF | real | Wert Schwerezaehler TSF |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_KM_FIRST | string | Km-Stand bei Erstauftreten |
| F_KM_NEXT | string | Km-Stand bei Erstauftreten |
| F_KM_LAST | string | Km-Stand bei Erstauftreten |
| F_KM_FIRST_WERT | real | Km-Stand bei Erstauftreten |
| F_KM_NEXT_WERT | real | Km-Stand bei Erstauftreten |
| F_KM_LAST_WERT | real | Km-Stand bei Erstauftreten |
| F_UW1_APP_NR | int | Applikationswert der 1. Umweltbedingung |
| F_UW2_APP_NR | int | Applikationswert der 2. Umweltbedingung |
| F_UW3_APP_NR | int | Applikationswert der 3. Umweltbedingung |
| F_UW4_APP_NR | int | Applikationswert der 4. Umweltbedingung |
| F_UW1_NR | int | 1.Satz Umweltbedingung 1 Index (Ersterkennung) |
| F_UW1_TEXT | string | 1.Satz UW1 Text zur Umweltbedingung |
| F_UW1_WERT | real | 1.Satz UW1 Wert der Umweltbedingung |
| F_UW1_EINH | string | 1.Satz UW1 Einheit |
| F_UW2_NR | int | 1.Satz Umweltbedingung 2 Index (Ersterkennung) |
| F_UW2_TEXT | string | 1.Satz UW2 Text zur Umweltbedingung |
| F_UW2_WERT | real | 1.Satz UW2 Wert der Umweltbedingung |
| F_UW2_EINH | string | 1.Satz UW2 Einheit |
| F_UW3_NR | int | 1.Satz Umweltbedingung 3 Index (Ersterkennung) |
| F_UW3_TEXT | string | 1.Satz UW3 Text zur Umweltbedingung |
| F_UW3_WERT | real | 1.Satz UW3 Wert der Umweltbedingung |
| F_UW3_EINH | string | 1.Satz UW3 Einheit |
| F_UW4_NR | int | 1.Satz Umweltbedingung 4 Index (Ersterkennung) |
| F_UW4_TEXT | string | 1.Satz UW4 Text zur Umweltbedingung |
| F_UW4_WERT | real | 1.Satz UW4 Wert der Umweltbedingung |
| F_UW4_EINH | string | 1.Satz UW4 Einheit |
| F_UW5_NR | int | 2.Satz Umweltbedingung 1 Index (zweite Erkennung) |
| F_UW5_TEXT | string | 2.Satz UW1 Text zur Umweltbedingung |
| F_UW5_WERT | real | 2.Satz UW1 Wert der Umweltbedingung |
| F_UW5_EINH | string | 2.Satz UW1 Einheit |
| F_UW6_NR | int | 2.Satz Umweltbedingung 2 Index (zweite Erkennung) |
| F_UW6_TEXT | string | 2.Satz UW2 Text zur Umweltbedingung |
| F_UW6_WERT | real | 2.Satz UW2 Wert der Umweltbedingung |
| F_UW6_EINH | string | 2.Satz UW2 Einheit |
| F_UW7_NR | int | 2.Satz Umweltbedingung 3 Index (zweite Erkennung) |
| F_UW7_TEXT | string | 2.Satz UW3 Text zur Umweltbedingung |
| F_UW7_WERT | real | 2.Satz UW3 Wert der Umweltbedingung |
| F_UW7_EINH | string | 2.Satz UW3 Einheit |
| F_UW8_NR | int | 2.Satz Umweltbedingung 4 Index (zweite Erkennung) |
| F_UW8_TEXT | string | 2.Satz UW4 Text zur Umweltbedingung |
| F_UW8_WERT | real | 2.Satz UW4 Wert der Umweltbedingung |
| F_UW8_EINH | string | 2.Satz UW4 Einheit |
| F_UW9_NR | int | 3.Satz Umweltbedingung 1 Index (aktuelle Erkennung) |
| F_UW9_TEXT | string | 3.Satz UW1 Text zur Umweltbedingung |
| F_UW9_WERT | real | 3.Satz UW1 Wert der Umweltbedingung |
| F_UW9_EINH | string | 3.Satz UW1 Einheit |
| F_UW10_NR | int | 3.Satz Umweltbedingung 2 Index (aktuelle Erkennung) |
| F_UW10_TEXT | string | 3.Satz UW2 Text zur Umweltbedingung |
| F_UW10_WERT | real | 3.Satz UW2 Wert der Umweltbedingung |
| F_UW10_EINH | string | 3.Satz UW2 Einheit |
| F_UW11_NR | int | 3.Satz Umweltbedingung 3 Index (aktuelle Erkennung) |
| F_UW11_TEXT | string | 3.Satz UW3 Text zur Umweltbedingung |
| F_UW11_WERT | real | 3.Satz UW3 Wert der Umweltbedingung |
| F_UW11_EINH | string | 3.Satz UW3 Einheit |
| F_UW12_NR | int | 3.Satz Umweltbedingung 4 Index (aktuelle Erkennung) |
| F_UW12_TEXT | string | 3.Satz UW4 Text zur Umweltbedingung |
| F_UW12_WERT | real | 3.Satz UW4 Wert der Umweltbedingung |
| F_UW12_EINH | string | 3.Satz UW4 Einheit |
| F_FF1_WERT | int | Freeze Frame Umweltbedingung 1 Wert |
| F_FF1_TEXT | string | Freeze Frame Umweltbedingung 1 |
| F_FF1_BESCH | string | Freeze Frame Umweltbedingung 1 Beschreibung |
| F_FF2_WERT | int | Freeze Frame Umweltbedingung 2 Wert |
| F_FF2_TEXT | string | Freeze Frame Umweltbedingung 2 Text |
| F_FF2_BESCH | string | Freeze Frame Umweltbedingung 2 Beschreibung |
| F_FF3_TEXT | string | Freeze Frame Umweltbedingung 3 Text |
| F_FF3_EINH | string | Freeze Frame Umweltbedingung 3 Einheit |
| F_FF3_WERT | real | Freeze Frame Umweltbedingung 3 Wert |
| F_FF4_TEXT | string | Freeze Frame Umweltbedingung 4 Text |
| F_FF4_EINH | string | Freeze Frame Umweltbedingung 4 EINH |
| F_FF4_WERT | real | Freeze Frame Umweltbedingung 4  Wert |
| F_FF5_TEXT | string | Freeze Frame Umweltbedingung 5 Text |
| F_FF5_EINH | string | Freeze Frame Umweltbedingung 5 EINH |
| F_FF5_WERT | real | Freeze Frame Umweltbedingung 5  Wert |
| F_FF6_TEXT | string | Freeze Frame Umweltbedingung 6 Text |
| F_FF6_EINH | string | Freeze Frame Umweltbedingung 6 EINH |
| F_FF6_WERT | real | Freeze Frame Umweltbedingung 6  Wert |
| F_FF7_TEXT | string | Freeze Frame Umweltbedingung 7 Text |
| F_FF7_EINH | string | Freeze Frame Umweltbedingung 7 EINH |
| F_FF7_WERT | real | Freeze Frame Umweltbedingung 7  Wert |
| F_FF8_TEXT | string | Freeze Frame Umweltbedingung 8 Text |
| F_FF8_EINH | string | Freeze Frame Umweltbedingung 8 EINH |
| F_FF8_WERT | real | Freeze Frame Umweltbedingung 8  Wert |
| F_FF9_TEXT | string | Freeze Frame Umweltbedingung 9 Text |
| F_FF9_EINH | string | Freeze Frame Umweltbedingung 9 EINH |
| F_FF9_WERT | real | Freeze Frame Umweltbedingung 9  Wert |
| F_FF10_TEXT | string | Freeze Frame Umweltbedingung 10 Text |
| F_FF10_EINH | string | Freeze Frame Umweltbedingung 10 EINH |
| F_FF10_WERT | real | Freeze Frame Umweltbedingung 10  Wert |
| F_FF11_TEXT | string | Freeze Frame Umweltbedingung 11 Text |
| F_FF11_EINH | string | Freeze Frame Umweltbedingung 11 EINH |
| F_FF11_WERT | real | Freeze Frame Umweltbedingung 11  Wert |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_P_CODE | string | P-Code des eingetragenen Fehlers |
| F_HEX_CODE | binary | Hexdump des Fehlers |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt"></a>
### STEUERN_VVT

Stellgliedansteuerung VVT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WINKEL | int | gibt einen absoluten Verstellwinkel an (0..180 Grd) |
| RAMPE | int | eine definierte Rampe wird automatisch abgefahren (VS-21 Funktion) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt-aus"></a>
### STEUERN_VVT_AUS

beenden Stellgliedansteuerung VVT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-co-abgleich"></a>
### STATUS_CO_ABGLEICH

Auslesen des LL-CO-Wertes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_CO_ABGLEICH_WERT | real | LL CO-Abgleichswert |
| STAT_CO_ABGLEICH_EINH | string | Einheit des LL CO-Abgleichswertes |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-co-abgleich-verstellen"></a>
### STEUERN_CO_ABGLEICH_VERSTELLEN

LL-CO-Wert vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CO_WERT | int | LL CO-Abgleichswert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-co-abgleich-programmieren"></a>
### STEUERN_CO_ABGLEICH_PROGRAMMIEREN

LL-CO-WERT programmieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CO_FEST | int | LL CO-Abgleichswert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gemisch"></a>
### STATUS_GEMISCH

Auslesen von Gemischwerten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_RKAT_WERT | real | Wert von rkat_w |
| STAT_RKAT_EINH | string | Einheit von rkat_w |
| STAT_RKAT2_WERT | real | Wert von rkat2_w |
| STAT_RKAT2_EINH | string | Einheit von rkat2_w |
| STAT_FRA_WERT | real | Wert von fra_w |
| STAT_FRA_EINH | string | Einheit von fra_w |
| STAT_FRA2_WERT | real | Wert von fra2_w |
| STAT_FRA2_EINH | string | Einheit von fra2_w |
| STAT_TEDUB_WERT | real | Wert von tedub |
| STAT_TEDUB_EINH | string | Einheit von tedub |
| STAT_TEDUB2_WERT | real | Wert von tedub2 |
| STAT_TEDUB2_EINH | string | Einheit von tedub2 |
| STAT_DYNLSU_WERT | real | Wert von dynlsu_w |
| STAT_DYNLSU_EINH | string | Einheit von dynlsu_w |
| STAT_DYNLSU2_WERT | real | Wert von dynlsu2_w |
| STAT_DYNLSU2_EINH | string | Einheit von dynlsu2_w |
| STAT_LAMSONI_WERT | real | Wert von lamsoni_w |
| STAT_LAMSONI_EINH | string | Einheit von lamsoni_w |
| STAT_LAMSONI2_WERT | real | Wert von lamsoni2_w |
| STAT_LAMSONI2_EINH | string | Einheit von lamsoni2_W |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ausgaenge"></a>
### STATUS_AUSGAENGE

Auslesen von Ausgaengen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_TATEIST_WERT | real | Wert von tateist |
| STAT_TATEIST_EINH | string | Einheit von tateist |
| STAT_VSASPRI_WERT | real | Wert von vsa_spri |
| STAT_VSASPRI_EINH | string | Einheit von vsa_spri |
| STAT_VSASPRI2_WERT | real | Wert von vsa2spri |
| STAT_VSASPRI2_EINH | string | Einheit von vsa2spri |
| STAT_VSESPRI_WERT | real | Wert von vse_spri |
| STAT_VSESPRI_EINH | string | Einheit von vse_spri |
| STAT_VSESPRI2_WERT | real | Wert von vse2spri |
| STAT_VSESPRI2_EINH | string | Einheit von vse2spri |
| STAT_VSATV_WERT | real | Wert von vsa_tv |
| STAT_VSATV_EINH | string | Einheit von vsa_tv |
| STAT_VSATV2_WERT | real | Wert von vsa2tv |
| STAT_VSATV2_EINH | string | Einheit von vsa2tv |
| STAT_VSETV_WERT | real | Wert von vse_tv |
| STAT_VSETV_EINH | string | Einheit von vse_tv |
| STAT_VSETV2_WERT | real | Wert von vse2tv |
| STAT_VSETV2_EINH | string | Einheit von vse2tv |
| STAT_TAML_WERT | real | Wert von taml |
| STAT_TAML_EINH | string | Einheit von taml |
| STAT_SLV_EIN | int | Bedingung SLV ein (nur Vorhalt) |
| STAT_SLP_EIN | int | Bedingung SLP ein |
| STAT_KOE_EIN | int | Bedingung KOE ein (nur Vorhalt) |
| STAT_HSVE_EIN | int | Bedingung Heizung LS v Kat ein |
| STAT_HSVE2_EIN | int | Bedingung Heizung LS v Kat Bank2 ein |
| STAT_HSHE_EIN | int | Bedingung Heizung LS h Kat ein |
| STAT_HSHE2_EIN | int | Bedingung Heizung LS h Kat Bank2 ein |
| STAT_AKR_EIN | int | Bedingung Abgasklappe ein |
| STAT_EBL_EIN | int | Bedingung E-Box Luefter ein |
| STAT_EKP_EIN | int | Bedingung EKP ein |
| STAT_ETR_EIN | int | Bedingung Kennfeldthermostat ein |
| STAT_STA_EIN | int | Bedingung Startrelais ein |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-nwgadaption"></a>
### STATUS_NWGADAPTION

Auslesen der NWG-Adaptionen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_VSAADP_WERT | real | Wert von vsa_adp |
| STAT_VSAADP_EINH | string | Einheit von vsa_adp |
| STAT_VSAADP2_WERT | real | Wert von vsa2_adp |
| STAT_VSAADP2_EINH | string | Einheit von vsa2_adp |
| STAT_VSEADP_WERT | real | Wert von vse_adp |
| STAT_VSEADP_EINH | string | Einheit von vse_adp |
| STAT_VSEADP2_WERT | real | Wert von vse2_adp |
| STAT_VSEADP2_EINH | string | Einheit von vse2_adp |
| STAT_VSAADPFL0_WERT | real | Wert von vsa_adp_fl0 |
| STAT_VSAADPFL0_EINH | string | Einheit von vsa_adp_fl0 |
| STAT_VSAADPFL1_WERT | real | Wert von vsa_adp_fl1 |
| STAT_VSAADPFL1_EINH | string | Einheit von vsa_adp_fl1 |
| STAT_VSAADPFL2_WERT | real | Wert von vsa_adp_fl2 |
| STAT_VSAADPFL2_EINH | string | Einheit von vsa_adp_fl2 |
| STAT_VSAADPFL3_WERT | real | Wert von vsa_adp_fl3 |
| STAT_VSAADPFL3_EINH | string | Einheit von vsa_adp_fl3 |
| STAT_VSAADP2FL0_WERT | real | Wert von vsa2_adp_fl0 |
| STAT_VSAADP2FL0_EINH | string | Einheit von vsa2_adp_fl0 |
| STAT_VSAADP2FL1_WERT | real | Wert von vsa2_adp_fl1 |
| STAT_VSAADP2FL1_EINH | string | Einheit von vsa2_adp_fl1 |
| STAT_VSAADP2FL2_WERT | real | Wert von vsa2_adp_fl2 |
| STAT_VSAADP2FL2_EINH | string | Einheit von vsa2_adp_fl2 |
| STAT_VSAADP2FL3_WERT | real | Wert von vsa2_adp_fl3 |
| STAT_VSAADP2FL3_EINH | string | Einheit von vsa2_adp_fl3 |
| STAT_VSEADPFL0_WERT | real | Wert von vse_adp_fl0 |
| STAT_VSEADPFL0_EINH | string | Einheit von vse_adp_fl0 |
| STAT_VSEADPFL1_WERT | real | Wert von vse_adp_fl1 |
| STAT_VSEADPFL1_EINH | string | Einheit von vse_adp_fl1 |
| STAT_VSEADPFL2_WERT | real | Wert von vse_adp_fl2 |
| STAT_VSEADPFL2_EINH | string | Einheit von vse_adp_fl2 |
| STAT_VSEADPFL3_WERT | real | Wert von vse_adp_fl3 |
| STAT_VSEADPFL3_EINH | string | Einheit von vse_adp_fl3 |
| STAT_VSEADP2FL0_WERT | real | Wert von vse2_adp_fl0 |
| STAT_VSEADP2FL0_EINH | string | Einheit von vse2_adp_fl0 |
| STAT_VSEADP2FL1_WERT | real | Wert von vse2_adp_fl1 |
| STAT_VSEADP2FL1_EINH | string | Einheit von vse2_adp_fl1 |
| STAT_VSEADP2FL2_WERT | real | Wert von vse2_adp_fl2 |
| STAT_VSEADP2FL2_EINH | string | Einheit von vse2_adp_fl2 |
| STAT_VSEADP2FL3_WERT | real | Wert von vse2_adp_fl3 |
| STAT_VSEADP2FL3_EINH | string | Einheit von vse2_adp_fl3 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-variante"></a>
### STATUS_VARIANTE

Auslesen der Variante

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_NOKATFZ_EIN | int | Bedingung NoKatFahrzeug ein |
| STAT_AUTGET_EIN | int | Bedingung Automatikgetriebe vorhanden |
| STAT_ACC_EIN | int | Bedingung ACC Fahrzeug |
| STAT_ASCPKW_EIN | int | Bedingung DSC Fahrzeug ein |
| STAT_ARSVAR_EIN | int | Bedingung ARS Fahrzeug ein |
| STAT_TXUGET_EIN | int | Bedingung Verteilergetriebe vorhanden |
| STAT_KOGER_EIN | int | Bedingung KOGER (4zyl.) vorhanden |
| STAT_AGR_EIN | int | Bedingung Abgasrueckfuehrung vorhanden |
| STAT_MFL_EIN | int | Bedingung Multifunktionslenkrad vorhanden |
| STAT_AKRFZ_EIN | int | Bedingung AKR erkannt |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecu-config"></a>
### ECU_CONFIG

Auslesen der Variante

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_DISA_GESCH_EIN | int | DISA geschaltet gelernt |
| STAT_DISA_GEREG_EIN | int | DISA 2-stufig gelernt |
| STAT_ANSKL_EIN | int | Ansaugklappe gelernt |
| STAT_AGR_EIN | int | Abgasrueckfuehrung gelernt |
| STAT_ABGK_MONO_EIN | int | Abgaskonzept Mono gelernt |
| STAT_ABGK_Y_EIN | int | Abgaskonzept Y gelernt |
| STAT_ABGK_STER_EIN | int | Abgaskonzept Stereo gelernt |
| STAT_NOKATFZ_EIN | int | Abgaskonzept ohne KAT gelernt |
| STAT_LIN_LSVK_EIN | int | Lineare Lambdasonden vor KAT gelernt |
| STAT_ZWP_LSVK_EIN | int | Zweipunkt Lambdasonden vor KAT gelernt |
| STAT_SLPVAR_EIN | int | Sekundaerluftpumpe gelernt |
| STAT_SLVVAR_EIN | int | Sekundaerluftventil gelernt |
| STAT_AKRFZ_EIN | int | Abgasklappe gelernt |
| STAT_SOUNDKL_EIN | int | Soundklappe gelernt |
| STAT_GLFVAR_EIN | int | Kuehler Jalousie gelernt |
| STAT_ELUE400_EIN | int | E-Luefter mit 400W gelernt |
| STAT_ELUE600_EIN | int | E-Luefter mit 600W gelernt |
| STAT_EBLVAR_EIN | int | E-Boxluefter gelernt |
| STAT_MFL_EIN | int | Multifunktionslenkrad gelernt |
| STAT_SPTVAR_EIN | int | Sporttaster gelernt |
| STAT_STRVAR_EIN | int | Starter Realais gelernt |
| STAT_TOENSVAR_EIN | int | Thermischer Oelnivausensor gelernt |
| STAT_HS_EIN | int | Handschalter gelernt |
| STAT_SSG_EIN | int | SSG gelernt |
| STAT_EGS_EIN | int | EGS gelernt |
| STAT_TXUGET_EIN | int | TUX Allrad gelernt |
| STAT_ASCPKW_EIN | int | Automatic Stability Control gelernt |
| STAT_ACC_EIN | int | Automatic Curise Control gelernt |
| STAT_ARSVAR_EIN | int | Dynamic Curise Control |
| STAT_AFSVAR_EIN | int | Active Front Steering gelernt |
| STAT_KOVAR_EIN | int | Relais Klimakompressor gelernt |
| STAT_IBSDETEC_EIN | int | Intelligenter Batteriesensor gelernt |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-variante"></a>
### STEUERN_VARIANTE

Loeschen der Varianten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VARIANTE_LOESCHEN | string | gibt bei OKAY an, ob loeschen erfolgreich war |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kva"></a>
### STATUS_KVA

Auslesen Faktor KVA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_KVA_WERT | real | Wert von vsa_adp |
| STAT_KVA_EINH | string | Einheit von vsa_adp |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kva"></a>
### STEUERN_KVA

Faktor KVA Korrektur vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KVA_WERT | int | Faktor KVA |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-readiness"></a>
### STATUS_READINESS

Auslesen des Readinessbyte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_KATFZ_EIN | int | Bedingung KatFahrzeug ein |
| STAT_CDTES_EIN | int | Bedingung Diagnosefreigabe Tankentlueftungssystem |
| STAT_CDSLS_EIN | int | Bedingung Diagnosefreigabe Sekundaerluftsystem |
| STAT_CDLSV_EIN | int | Bedingung Diagnosefreigabe Lambdasonde vor Kat |
| STAT_CDHSV_EIN | int | Bedingung Diagnosefreigabe Lambdasondenheizung vor Kat |
| STAT_CDAGR_EIN | int | Bedingung Diagnosefreigabe Abgasrueckfuehrung (nur BDE!) |
| STAT_KATRDY_EIN | int | Bedingung Katdiagnose ready |
| STAT_TESRDY_EIN | int | Bedingung Tankentlueftungssystem ready |
| STAT_SLSRDY_EIN | int | Bedingung Sekundaerluftsystem ready |
| STAT_LSRDY_EIN | int | Bedingung Lambdasonden ready |
| STAT_HSRDY_EIN | int | Bedingung Heizung Lambdasonden ready |
| STAT_AGRRDY_EIN | int | Bedingung Abgasrueckfuehrung ready |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fgr"></a>
### STATUS_FGR

Auslesen des FGR-Statuses

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_FGRAT_EIN | int | Bedingung FGR Austaste ein |
| STAT_FGRHSA_EIN | int | Bedingung FGR Hauptschalter |
| STAT_FGRTBE_EIN | int | Bedingung Taste Beschleunigung |
| STAT_FGRTSE_EIN | int | Bedingung Taste Setzen |
| STAT_FGRTVE_EIN | int | Bedingung Taste Verzoegern |
| STAT_FGRTWA_EIN | int | Bedingung Taste Wiederaufnahme |
| STAT_LFGR_EIN | int | Bedingung FGR-Lampe |
| STAT_ACC_EIN | int | Bedingung ACC |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-llabg"></a>
### STEUERN_LLABG

LL-Abgleichswerte werden vorgegeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DNLLMV | int | Abgleichswert LL ohne FS |
| DNSACMV | int | Abgleichswert LL mit Klimaanlage ohne FS |
| DNSLBV | int | Abgleichswert LL aus %LLRUB, niedriger UBatt |
| DNFSACMV | int | Abgleichswert LL mit Klimaanlage mit FS |
| DNFSMV | int | Abgleichswert LL mit FS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-llabg-prog"></a>
### STEUERN_LLABG_PROG

LL-Abgleichswerte werden programmiert

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DNLLMV | int | Abgleichswert LL ohne FS |
| DNSACMV | int | Abgleichswert LL mit Klimaanlage ohne FS |
| DNSLBV | int | Abgleichswert LL aus %LLRUB, niedriger UBatt |
| DNFSACMV | int | Abgleichswert LL mit Klimaanlage mit FS |
| DNFSMV | int | Abgleichswert LL mit FS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-llabg"></a>
### STATUS_LLABG

LL-Abgleichswerte werden gelesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_DNLLMV_WERT | real | Abgleichswert LL ohne FS |
| STAT_DNLLMV_EINH | string | Einheit von dnllmv |
| STAT_DNSACMV_WERT | real | Abgleichswert LL mit Klimaanlage ohne FS |
| STAT_DNSACMV_EINH | string | Einheit von dnsacmv |
| STAT_DNSLBV_WERT | real | Abgleichswert LL aus %LLRUB, niedriger UBatt |
| STAT_DNSLBV_EINH | string | Einheit von dnslbv |
| STAT_DNFSACMV_WERT | real | Abgleichswert LL mit Klimaanlage mit FS |
| STAT_DNFSACMV_EINH | string | Einheit von dnfsacmv |
| STAT_DNFSMV_WERT | real | Abgleichswert LL mit FS |
| STAT_DNFSMV_EINH | string | Einheit von dnfsmv |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-aif"></a>
### IDENT_AIF

Identdaten mit KWP2000: $1A ReadECUIdentification Modus  : Default Auslesen des Anwender Informations Feldes mit KWP 2000: $23 ReadMemoryByAddress Standard Flashjob Modus   : Default

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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vvt"></a>
### STATUS_VVT

Auslesen VVT-Messwerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_VVTSW_WERT | real | Wert von vvt_sw |
| STAT_VVTSW_EINH | string | Einheit von vvt_sw |
| STAT_VVTIW_WERT | real | Wert von vvt_iw |
| STAT_VVTIW_EINH | string | Einheit von vvt_iw |
| STAT_VVTTV_WERT | real | Wert von vvt_tv |
| STAT_VVTTV_EINH | string | Einheit von vvt_tv |
| STAT_VVTES_WERT | real | Wert von vvt_es |
| STAT_VVTES_EINH | string | Einheit von vvt_es |
| STAT_VVTSW2_WERT | real | Wert von vvt_sw2 |
| STAT_VVTSW2_EINH | string | Einheit von vvt_sw2 |
| STAT_VVTIW2_WERT | real | Wert von vvt_iw2 |
| STAT_VVTIW2_EINH | string | Einheit von vvt_iw2 |
| STAT_VVTTV2_WERT | real | Wert von vvt_tv2 |
| STAT_VVTTV2_EINH | string | Einheit von vvt_tv2 |
| STAT_VVTES2_WERT | real | Wert von vvt_es2 |
| STAT_VVTES2_EINH | string | Einheit von vvt_es2 |
| STAT_MINHUBVSI_WERT | real | Wert von minhubvsi_W |
| STAT_MINHUBVSI_EINH | string | Einheit von minhubvsi_W |
| STAT_DELTAGVFI_WERT | real | Wert von deltagvfi_W |
| STAT_DELTAGVFI_EINH | string | Einheit von deltagvfi_W |
| STAT_FLUB1_WERT | real | Wert von flub1_W |
| STAT_FLUB1_EINH | string | Einheit von flub1_W |
| STAT_FLUB2_WERT | real | Wert von flub2_W |
| STAT_FLUB2_EINH | string | Einheit von flub2_W |
| STAT_MINHUBROH_WERT | real | Wert von minhub_roh |
| STAT_MINHUBROH_EINH | string | Einheit von minhub_roh |
| STAT_NMOT_EIN | int | Wert von B_nmot |
| STAT_MINHUBVS_EIN | int | Wert von B_minhubvs |
| STAT_FBGL_EIN | int | Wert von B_fbgl |
| STAT_BGL_EIN | int | Wert von B_bgl |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-differenzdrucksensor"></a>
### STATUS_DIFFERENZDRUCKSENSOR

Werte des Differenzdrucksensors im Ansaugluftsystem

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_DPS_WERT | real | Wert von dps_w |
| STAT_DPS_EINH | string | Einheit von dps_w |
| STAT_DPSSOL_WERT | real | Wert von dpssol_w |
| STAT_DPSSOL_EINH | string | Einheit von dpssol_w |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta1"></a>
### STATUS_FASTA1

Auslesen FASTA-Messwertblock 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_TSG_WERT | real | Wert von tsg |
| STAT_TSG_EINH | string | Einheit von tsg |
| STAT_KRDWS_EIN | int | Wert von B_krdws |
| STAT_DMVAD_WERT | real | Wert von dmvad_w |
| STAT_DMVAD_EINH | string | Einheit von dmvad_w |
| STAT_DPS_WERT | real | Wert von dps_w |
| STAT_DPS_EINH | string | Einheit von dps_w |
| STAT_DPSRAUS_WERT | real | Wert von dpsraus_i |
| STAT_DPSRAUS_EINH | string | Einheit von dpsraus_i |
| STAT_FKMSVVT_WERT | real | Wert von fkmsvvt_w |
| STAT_FKMSVVT_EINH | string | Einheit von fkmsvvt_w |
| STAT_FPRSTEP_WERT | real | Wert von fprstep_c |
| STAT_FPRSTEP_EINH | string | Einheit von fprstep_c |
| STAT_LRNSTEP_WERT | real | Wert von lrnstep_c |
| STAT_LRNSTEP_EINH | string | Einheit von lrnstep_c |
| STAT_MSNVVTO_WERT | real | Wert von msnvvto_w |
| STAT_MSNVVTO_EINH | string | Einheit von msnvvto_w |
| STAT_NNW10_WERT | real | Wert von nn_w1_0 |
| STAT_NNW10_EINH | string | Einheit von nn_w1_0 |
| STAT_NNW11_WERT | real | Wert von nn_w1_1 |
| STAT_NNW11_EINH | string | Einheit von nn_w1_1 |
| STAT_NNW12_WERT | real | Wert von nn_w1_2 |
| STAT_NNW12_EINH | string | Einheit von nn_w1_2 |
| STAT_NNW20_WERT | real | Wert von nn_w2_0 |
| STAT_NNW20_EINH | string | Einheit von nn_w2_0 |
| STAT_NNW21_WERT | real | Wert von nn_w2_1 |
| STAT_NNW21_EINH | string | Einheit von nn_w2_1 |
| STAT_NNW22_WERT | real | Wert von nn_w2_2 |
| STAT_NNW22_EINH | string | Einheit von nn_w2_2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta2"></a>
### STATUS_FASTA2

Auslesen FASTA-Messwertblock 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_NSOLFASTA_WERT | real | Wert von nsol_w |
| STAT_NSOLFASTA_EINH | string | Einheit von nsol_w |
| STAT_RL_WERT | real | Wert von rl_w |
| STAT_RL_EINH | string | Einheit von rl_w |
| STAT_RLSOL_WERT | real | Wert von rlsol_w |
| STAT_RLSOL_EINH | string | Einheit von rlsol_w |
| STAT_TE_WERT | real | Wert von te_w |
| STAT_TE_EINH | string | Einheit von te_w |
| STAT_TE2_WERT | real | Wert von te2_w |
| STAT_TE2_EINH | string | Einheit von te2_w |
| STAT_VVTSTATUS_WERT | real | Wert von vvtstatus |
| STAT_VVTSTATUS_EINH | string | Einheit von vvtstatus |
| STAT_WDKBAFASTA_WERT | real | Wert von wdkba_w |
| STAT_WDKBAFASTA_EINH | string | Einheit von wdkba_w |
| STAT_WDKS_WERT | real | Wert von wdks_w |
| STAT_WDKS_EINH | string | Einheit von wdks_w |
| STAT_WPED_WERT | real | Wert von wped_w |
| STAT_WPED_EINH | string | Einheit von wped_w |
| STAT_ZWIST_WERT | real | Wert von zwist |
| STAT_ZWIST_EINH | string | Einheit von zwist |
| STAT_MIL_EIN | int | Wert von B_mil |
| STAT_DMLLRI_WERT | real | Wert von dmllri_w |
| STAT_DMLLRI_EINH | string | Einheit von dmllri_w |
| STAT_MIMIN_WERT | real | Wert von mimin_w |
| STAT_MIMIN_EINH | string | Einheit von mimin_w |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta3"></a>
### STATUS_FASTA3

Auslesen FASTA-Messwertblock 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_MDGEN_WERT | real | Wert von mdgen |
| STAT_MDGEN_EINH | string | Einheit von mdgen |
| STAT_MDKO_WERT | real | Wert von mdko |
| STAT_MDKO_EINH | string | Einheit von mdko |
| STAT_DMRLLR_WERT | real | Wert von dmrllr_w |
| STAT_DMRLLR_EINH | string | Einheit von dmrllr_w |
| STAT_FS_EIN | int | Wert von B_fs |
| STAT_MDWAN_WERT | real | Wert von mdwan ist eigentlich eine Word-Groesse |
| STAT_MDWAN_EINH | string | Einheit von mdwan |
| STAT_DWKR_WERT | real | Wert von dwkr |
| STAT_DWKR_EINH | string | Einheit von dwkr |
| STAT_DZWS_WERT | real | Wert von dzws |
| STAT_DZWS_EINH | string | Einheit von dzws |
| STAT_DFFGEN_WERT | real | Wert von dffgen |
| STAT_DFFGEN_EINH | string | Einheit von dffgen |
| STAT_TUMG_WERT | real | Wert von tumg |
| STAT_TUMG_EINH | string | Einheit von tumg |
| STAT_DMVADFS_WERT | real | Wert von dmvadfs |
| STAT_DMVADFS_EINH | string | Einheit von dmvadfs |
| STAT_DMVADKO_WERT | real | Wert von dmvadko |
| STAT_DMVADKO_EINH | string | Einheit von dmvadko |
| STAT_DLAHI_WERT | real | Wert von dlahi_w |
| STAT_DLAHI_EINH | string | Einheit von dlahi_w |
| STAT_DLAHI2_WERT | real | Wert von dlahi2_w |
| STAT_DLAHI2_EINH | string | Einheit von dlahi2_w |
| STAT_RINH_WERT | real | Wert von rinh_w |
| STAT_RINH_EINH | string | Einheit von rinh_w |
| STAT_RINH2_WERT | real | Wert von rinh2_w |
| STAT_RINH2_EINH | string | Einheit von rinh2_w |
| STAT_RKATS_WERT | real | Wert von rkats_w |
| STAT_RKATS_EINH | string | Einheit von rkats_w |
| STAT_DPSSOL_WERT | real | Wert von dpssol_w |
| STAT_DPSSOL_EINH | string | Einheit von dpssol_w |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta4"></a>
### STATUS_FASTA4

Auslesen FASTA-Messwertblock 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_ECULOCK_EIN | int | Wert von B_eculock |
| STAT_LRNRDY_EIN | int | Wert von B_lrnrdy |
| STAT_LLTD_EIN | int | Wert von B_lltd |
| STAT_LLK_EIN | int | Wert von B_llk |
| STAT_TEAKT_EIN | int | Wert von B_teakt |
| STAT_VVTNOTL_EIN | int | Wert von B_vvtnotl |
| STAT_NVRBUPOK_EIN | int | Wert von B_nvrbupok --&gt; Rambackup ok |
| STAT_COPOT_WERT | real | Wert von co_pot_w |
| STAT_COPOT_EINH | string | Einheit von co_pot_w |
| STAT_UPWG_WERT | real | Wert von upwg_w |
| STAT_UPWG_EINH | string | Einheit von upwg_w |
| STAT_MINHUB_WERT | real | Wert von minhub_w |
| STAT_MINHUB_EINH | string | Einheit von minhub_w |
| STAT_GVIST_WERT | real | Wert von gvist |
| STAT_GVIST_EINH | string | Einheit von gvist |
| STAT_FTBR_WERT | real | Wert von ftbr_w |
| STAT_FTBR_EINH | string | Einheit von ftbr_w |
| STAT_FHO_WERT | real | Wert von fho_w |
| STAT_FHO_EINH | string | Einheit von fho_w |
| STAT_FTVDK_WERT | real | Wert von ftvdk |
| STAT_FTVDK_EINH | string | Einheit von ftvdk |
| STAT_MSNVVTOLL_WERT | real | Wert von msnvvtoll_w |
| STAT_MSNVVTOLL_EINH | string | Einheit von msnvvtoll_w |
| STAT_VSESPRS_WERT | real | Wert von vse_sprs |
| STAT_VSESPRS_EINH | string | Einheit von vse_sprs |
| STAT_VSE2SPRS_WERT | real | Wert von vse2sprs |
| STAT_VSE2SPRS_EINH | string | Einheit von vse2sprs |
| STAT_VSASPRS_WERT | real | Wert von vsa_sprs |
| STAT_VSASPRS_EINH | string | Einheit von vsa_sprs |
| STAT_VSA2SPRS_WERT | real | Wert von vsa2sprs |
| STAT_VSA2SPRS_EINH | string | Einheit von vsa2sprs |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta5"></a>
### STATUS_FASTA5

Auslesen FASTA-Messwertblock 5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_ATMTPA_EIN | int | Wert von B_atmtpa |
| STAT_ATMTPK_EIN | int | Wert von B_atmtpk |
| STAT_EVHUBI_WERT | real | Wert von evhubi_w |
| STAT_EVHUBI_EINH | string | Einheit von evhubi_w |
| STAT_EVHUBI2_WERT | real | Wert von evhubi2_w |
| STAT_EVHUBI2_EINH | string | Einheit von evhubi2_w |
| STAT_EVHUBS_WERT | real | Wert von evhubs_w |
| STAT_EVHUBS_EINH | string | Einheit von evhubs_w |
| STAT_OFWNKADBG_WERT | real | Wert von ofwnkadbg |
| STAT_OFWNKADBG_EINH | string | Einheit von ofwnkadbg |
| STAT_KH_EIN | int | Wert von B_kh |
| STAT_NSUB_EIN | int | Wert von B_nsub |
| STAT_TE_EIN | int | Wert von B_te |
| STAT_DFSERESZ_WERT | real | Wert von dfseresz_w |
| STAT_DFSERESZ_EINH | string | Einheit von dfseresz_w |
| STAT_DMVADFK_WERT | real | Wert von dmvadfk_w |
| STAT_DMVADFK_EINH | string | Einheit von dmvadfk_w |
| STAT_DMVADLL_WERT | real | Wert von dmvadll_w |
| STAT_DMVADLL_EINH | string | Einheit von dmvadll_w |
| STAT_EXWINKI_WERT | real | Wert von exwinki_w |
| STAT_EXWINKI_EINH | string | Einheit von exwinki_w |
| STAT_EXWINKI2_WERT | real | Wert von exwinki2_w |
| STAT_EXWINKI2_EINH | string | Einheit von exwinki2_w |
| STAT_EXWINKS_WERT | real | Wert von exwinks_w |
| STAT_EXWINKS_EINH | string | Einheit von exwinks_w |
| STAT_FE_WERT | int | Wert von B_fe (ist kein Flag!) |
| STAT_FE_EINH | string | Einheit von B_fe |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta6"></a>
### STATUS_FASTA6

Auslesen FASTA-Messwertblock 6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_FKMSVVTA_WERT | real | Wert von fkmsvvta_w |
| STAT_FKMSVVTA_EINH | string | Einheit von fkmsvvta_w |
| STAT_FOFRESZ_WERT | real | Wert von fofresz |
| STAT_FOFRESZ_EINH | string | Einheit von fofresz |
| STAT_MSDIF_WERT | real | Wert von msdif_w |
| STAT_MSDIF_EINH | string | Einheit von msdif_w |
| STAT_TABGM_WERT | real | Wert von tabgm |
| STAT_TABGM_EINH | string | Einheit von tabgm |
| STAT_TNSE_WERT | real | Wert von tnse_w |
| STAT_TNSE_EINH | string | Einheit von tnse_w |
| STAT_OZRWPERM_WERT | real | Wert von ozrwperm |
| STAT_OZRWPERM_EINH | string | Einheit von ozrwperm |
| STAT_OZRWKVB_WERT | real | Wert von ozrwkvb |
| STAT_OZRWKVB_EINH | string | Einheit von ozrwkvb |
| STAT_OZOELZEIT_WERT | real | Wert von ozoelzeit |
| STAT_OZOELZEIT_EINH | string | Einheit von ozoelzeit |
| STAT_OZKVBSM_WERT | real | Wert von ozkvbsm_ul |
| STAT_OZKVBSM_EINH | string | Einheit von ozkvbsm_ul |
| STAT_OZPERMLOW_WERT | real | Wert von ozpermlow |
| STAT_OZPERMLOW_EINH | string | Einheit von ozpermlow |
| STAT_OZPERMEX_WERT | real | Wert von ozpermex |
| STAT_OZPERMEX_EINH | string | Einheit von ozpermex |
| STAT_OZPERMOFF_WERT | real | Wert von ozpermoff |
| STAT_OZPERMOFF_EINH | string | Einheit von ozpermoff |
| STAT_OZKVBOG_WERT | real | Wert von ozkvbog |
| STAT_OZKVBOG_EINH | string | Einheit von ozkvbog |
| STAT_OZPERMBOG_WERT | real | Wert von ozpermbog |
| STAT_OZPERMBOG_EINH | string | Einheit von ozpermbog |
| STAT_OZOELKM_WERT | real | Wert von ozoelkm |
| STAT_OZOELKM_EINH | string | Einheit von ozoelkm |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta7"></a>
### STATUS_FASTA7

Auslesen FASTA-Messwertblock 7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_NADMTLL_WERT | real | Wert von nadmtll_w |
| STAT_NADMTLL_EINH | string | Einheit von nadmtll_w |
| STAT_NTGLM_WERT | real | Wert von ntglm_w |
| STAT_NTGLM_EINH | string | Einheit von ntglm_w |
| STAT_NTKLM_WERT | real | Wert von ntklm_w |
| STAT_NTKLM_EINH | string | Einheit von ntklm_w |
| STAT_NDIPFRO_WERT | real | Wert von ndipfro_w |
| STAT_NDIPFRO_EINH | string | Einheit von ndipfro_w |
| STAT_NKFL_WERT | real | Wert von nkfl |
| STAT_NKFL_EINH | string | Einheit von nkfl |
| STAT_SSLLCNT_WERT | real | Wert von ssllcnt |
| STAT_SSLLCNT_EINH | string | Einheit von ssllcnt |
| STAT_MINHUBFAK_WERT | real | Wert von minhubfak |
| STAT_MINHUBFAK_EINH | string | Einheit von minhubfak |
| STAT_MINADRDY_WERT | real | Wert von minadrdy |
| STAT_MINADRDY_EINH | string | Einheit von minadrdy |
| STAT_BGLFLAGS1_NR | int | Wert von bgl_flags1 |
| STAT_BGLFLAGS2_NR | int | Wert von bgl_flags2 |
| STAT_BGLFLAGS3_NR | int | Wert von bgl_flags3 |
| STAT_BGLFLAGS4_NR | int | Wert von bgl_flags4 |
| STAT_SSLL_EIN | int | Wert von B_ssll |
| STAT_TDAON_EIN | int | Wert von B_tdaon |
| STAT_BGLRDY_EIN | int | Wert von B_bglrdy |
| STAT_FDLUBBGL_WERT | real | Wert von fdlubbgl_w |
| STAT_FDLUBBGL_EINH | string | Einheit von fdlubbgl_w |
| STAT_OFWNKBG1_WERT | real | Wert von ofwnkbg1 |
| STAT_OFWNKBG1_EINH | string | Einheit von ofwnkbg1 |
| STAT_OFWNKBG2_WERT | real | Wert von ofwnkbg2 |
| STAT_OFWNKBG2_EINH | string | Einheit von ofwnkbg2 |
| STAT_OFWNKMX_WERT | real | Wert von ofwnkmx |
| STAT_OFWNKMX_EINH | string | Einheit von ofwnkmx |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-adc"></a>
### STATUS_ADC

Auslesen ADC-Werte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_WTSG_WERT | real | Wert von wtsg |
| STAT_WTSG_EINH | string | Einheit von WTSG |
| STAT_USHK2_WERT | real | Wert von ushk_2 |
| STAT_USHK2_EINH | string | Einheit von ushk_2 |
| STAT_UPWG1_WERT | real | Wert von upwg1_w |
| STAT_UPWG1_EINH | string | Einheit von upwg1_w |
| STAT_UPWG2_WERT | real | Wert von upwg2_w |
| STAT_UPWG2_EINH | string | Einheit von upwg2_w |
| STAT_USHK_WERT | real | Wert von ushk_w |
| STAT_USHK_EINH | string | Einheit von ushk_w |
| STAT_WUB_WERT | real | Wert von wub |
| STAT_WUB_EINH | string | Einheit von wub |
| STAT_UDKP2_WERT | real | Wert von udkp1_w |
| STAT_UDKP2_EINH | string | Einheit von udkp1_w |
| STAT_UDKP1V_WERT | real | Wert von udkp1v_w |
| STAT_UDKP1V_EINH | string | Einheit von udkp1v_w |
| STAT_UDKP1_WERT | real | Wert von udkp1_w |
| STAT_UDKP1_EINH | string | Einheit von udkp1_w |
| STAT_UHFM_WERT | real | Wert von uhfm_w |
| STAT_UHFM_EINH | string | Einheit von uhfm_w |
| STAT_WTMOT_WERT | real | Wert von wtmot |
| STAT_WTMOT_EINH | string | Einheit von wtmot |
| STAT_WTANS_WERT | real | Wert von wtans |
| STAT_WTANS_EINH | string | Einheit von wtans |
| STAT_WTKA_WERT | real | Wert von wtka |
| STAT_WTKA_EINH | string | Einheit von wtka |
| STAT_UHSV_WERT | real | Wert von uhsv |
| STAT_UHSV_EINH | string | Einheit von uhsv |
| STAT_UHSV2_WERT | real | Wert von uhsv2 |
| STAT_UHSV2_EINH | string | Einheit von uhsv2 |
| STAT_UHSH_WERT | real | Wert von uhsh |
| STAT_UHSH_EINH | string | Einheit von uhsh |
| STAT_UHSH2_WERT | real | Wert von uhsh2 |
| STAT_UHSH2_EINH | string | Einheit von uhsh2 |
| STAT_DISA_WERT | real | Wert von disa_spg |
| STAT_DISA_EINH | string | Einheit von disa_spg |
| STAT_UDDSS_WERT | real | Wert von uddss_w |
| STAT_UDDSS_EINH | string | Einheit von uddss_w |
| STAT_UDSU_WERT | real | Wert von udsu_w |
| STAT_UDSU_EINH | string | Einheit von udsu_w |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ll-erh"></a>
### STEUERN_LL_ERH

Diagnosefunktion LL-Erhoehung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LL_WERT | int | gesetzter LL-Sollwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-lsu"></a>
### START_SYSTEMCHECK_LSU

Systemdiagnose LSU starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-lsu"></a>
### STATUS_SYSTEMCHECK_LSU

Status Systemdiagnose LSU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LSU_WERT | int | Status der LSU-Diagnose Bank1 |
| STAT_LSU2_WERT | int | Status der LSU-Diagnose Bank2 |
| STAT_LSUBANK1_TEXT | string | Status der LSU-Diagnose Bank1 |
| STAT_LSUBANK2_TEXT | string | Status der LSU-Diagnose Bank2 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-lsu"></a>
### STOP_SYSTEMCHECK_LSU

Ende Systemdiagnose LSU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-kat"></a>
### START_SYSTEMCHECK_KAT

Systemdiagnose KAT

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BANK | int | selektiert die Bank aus (1--&gt; Bank1, 2--&gt; Bank2, 3--&gt; Bank1 und 2) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-kat"></a>
### STOP_SYSTEMCHECK_KAT

Ende Systemdiagnose KAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-lsh"></a>
### START_SYSTEMCHECK_LSH

Start der Systemdiagnose LSH

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BANK | int | selektiert die Bank aus (1--&gt; Bank1, 2--&gt; Bank2, 3--&gt; Bank1 und 2) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-lsh"></a>
### STATUS_SYSTEMCHECK_LSH

Status LSH-Diagnose auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZLSH_EIN | int | Status Zyklus-Flag LSH Bank1 lesen |
| STAT_ZLSH2_EIN | int | Status Zyklus-Flag LSH Bank2 lesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-lsh"></a>
### STOP_SYSTEMCHECK_LSH

Ende der Systemdiagnose LSH

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-grundadapt"></a>
### START_SYSTEMCHECK_GRUNDADAPT

Systemdiagnose Grundadaptionenen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-grundadapt"></a>
### STATUS_SYSTEMCHECK_GRUNDADAPT

Status Systemdiagnose Grundadaptionen starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GAD_EIN | int | Status Grundadaption ein (B_gad) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-grundadapt"></a>
### STOP_SYSTEMCHECK_GRUNDADAPT

Ende Systemdiagnose Grundadaptionen starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-gemischadapt-sperr"></a>
### START_SYSTEMCHECK_GEMISCHADAPT_SPERR

Systemdiagnose Gemischadaptionen sperren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-gemischadapt-sperr"></a>
### STOP_SYSTEMCHECK_GEMISCHADAPT_SPERR

Ende Systemdiagnose Gemischadaptionen sperren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-lambda-aus"></a>
### START_SYSTEMCHECK_LAMBDA_AUS

Systemdiagnose Labdaregelung aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-lambda-aus"></a>
### STATUS_SYSTEMCHECK_LAMBDA_AUS

Status Systemdiagnose Lambdaregelung aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAMBREGBANK1_TEXT | string | Status der Lambdaregelung Bank1 (flglrs) |
| STAT_LAMBREGBANK2_TEXT | string | Status der Lambdaregelung Bank2 (flglrs2) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-lambda-aus"></a>
### STOP_SYSTEMCHECK_LAMBDA_AUS

Ende Systemdiagnose Lambdaregelung aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-kompression"></a>
### START_SYSTEMCHECK_KOMPRESSION

Systemdiagnose Kompressionstest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-kompression"></a>
### STOP_SYSTEMCHECK_KOMPRESSION

Ende Systemdiagnose Kompressiostest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zwang-rambackup"></a>
### STEUERN_ZWANG_RAMBACKUP

Zwangssichern der RAM-Backup-Werte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-power-down"></a>
### STEUERN_POWER_DOWN

Anforderung Power Down Mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-disa-anschlag"></a>
### STEUERN_DISA_ANSCHLAG

lernen der DISA-Anschlaege

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-disa-anschlag"></a>
### STATUS_DISA_ANSCHLAG

Status Lernen der DISA-Anschlaege

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DISA_ANSCHL | int | Status des Lernens Disa |
| STAT_DISA_ANSCHL_TEXT | string | Status des Lernens Disa |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-disa-anschlag"></a>
### STOP_DISA_ANSCHLAG

Ende des Lernes DISA-Anschlaege

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-sek-luft"></a>
### START_SYSTEMCHECK_SEK_LUFT

Systemdiagnose SLS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-sek-luft"></a>
### STATUS_SYSTEMCHECK_SEK_LUFT

Status Systemdiagnose SLS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_SEK_LUFT_TEXT | string | Status der SLS-Diagnose |
| STAT_SYSTEMCHECK_SEK_LUFT_STATUS | int | Status der SLS-Diagnose |
| STAT_SYSTEMCHECK_SEK_LUFT_WERT | int | Status der SLS-Diagnose |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-sek-luft"></a>
### STOP_SYSTEMCHECK_SEK_LUFT

Ende Systemdiagnose SLS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-adaptionen-loeschen"></a>
### STEUERN_ADAPTIONEN_LOESCHEN

Loeschen der Adaptionswerte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE_1 | int | siehe LH 1 430 227, setzt REYO_01 bitweise |
| AUSWAHLBYTE_2 | int | siehe LH 1 430 227, setzt REYO_02 bitweise |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-adaptionen-loeschen-neu"></a>
### STEUERN_ADAPTIONEN_LOESCHEN_NEU

Loeschen der Adaptionswerte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE_1 | int | siehe LH 1 430 227, setzt REYO_01 bitweise |
| AUSWAHLBYTE_2 | int | siehe LH 1 430 227, setzt REYO_02 bitweise |
| AUSWAHLBYTE_3 | int | setzt REYO_03 bitweise |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-minhub"></a>
### STATUS_MINHUB

Auslesen des VVT-Minhubes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MINHUB_WERT | real | Wert von minhub_w |
| STAT_MINHUB_EINH | string | Einheit von minhub_w |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-minhub"></a>
### STEUERN_MINHUB

Vorgeben des VVT-Minhubes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MINHUB | int | Vorsteuerwert minhubvs_w in tausendstel Milimeter |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-minhub-programm"></a>
### STEUERN_MINHUB_PROGRAMM

Programmieren des VVT-Minhubes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MINHUB | int | zu programmierender Wert minhubvs_w in tausendstel Milimeter |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bankabgleich"></a>
### STATUS_BANKABGLEICH

Auslesen des VVT-Bankabgleiches

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFWTSTBER_WERT | real | Wert von ofwtstber |
| STAT_OFWTSTBER_EINH | string | Einheit von ofwtstber |
| STAT_OFWNKTEST_WERT | real | Wert von ofwnktest |
| STAT_OFWNKTEST_EINH | string | Einheit von ofwnktest |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bankabgleich-programm"></a>
### STEUERN_BANKABGLEICH_PROGRAMM

Programmieren des VVT-Minhubes

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| OFWTSTBER | int | Offsetbereich, momentan nur ein Dummy |
| OFWNKTEST | int | Verstellung Bankabgleich (folg. Werte zulaessig: -50,...,50 in 10-er Schritten) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betriebsstundenzaehler"></a>
### STATUS_BETRIEBSSTUNDENZAEHLER

Status Betriebsstundenzaehler auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BSZ | string | Status Betriebsstundenzaehler lesen |
| STAT_BSZ_WERT | int | Status Betriebsstundenzaehler (int) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-kat"></a>
### STATUS_SYSTEMCHECK_KAT

Status Systemtest KAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_KAT_WERT | int | Status der KAT-Diagnose |
| STAT_SYSTEMCHECK_KAT_TEXT | string | Status der KAT-Diagnose |
| STAT_SYSTEMCHECK_KAT2_WERT | int | Status der KAT-Diagnose |
| STAT_SYSTEMCHECK_KAT2_TEXT | string | Status der KAT-Diagnose |
| STAT_OSCDKTF_WERT | real | Wert von oscdktf_w (gefilt. Speichervermögen des KAT) |
| STAT_OSCDKTF_EINH | string | Einheit von oscdktf_w |
| STAT_OSCDKTF2_WERT | real | Wert von oscdktf2_w (gefilt. Speichervermögen des KAT) |
| STAT_OSCDKTF2_EINH | string | Einheit von oscdktf2_w |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ews-startwert"></a>
### EWS_STARTWERT

EWS-Startwertinitialisierung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PARAMETER | int | Parameter zur Initialisierung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| EWS_STATUS | string | Rueckgabestatus bei der Startwertinitialisierung |
| STAT_EWS_WERT | int | Rueckgabewert bei der Startwertinitialisierung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ews-empfang"></a>
### EWS_EMPFANG

EWS-Empfangsstatus auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| EWS_EMPFANGSSTATUS | string | Rueckgabestatus bei der Startwertinitialisierung |
| EWS_STATUS_VALUE | int | Rueckgabestatus bei der Startwertinitialisierung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

Auslesen der Motortemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_MOTORTEMPERATUR_WERT | real | Wert von TI_W |
| STAT_MOTORTEMPERATUR_EINH | string | Einheit von TI_W |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Auslesen der Motordrehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORDREHZAHL_WERT | real | Wert von Motordrehzahl |
| STAT_MOTORDREHZAHL_EINH | string | Einheit von Motordrehzahl |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

Auslesen der Lufttemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_AN_LUFTTEMPERATUR_WERT | real | Wert von Lufttemperatur |
| STAT_AN_LUFTTEMPERATUR_EINH | string | Einheit von Lufttemperatur |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

Auslesen der Luftmasse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_LMM_MASSE_WERT | real | Wert von Luftmasse |
| STAT_LMM_MASSE_EINH | string | Einheit von Luftmasse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde"></a>
### STATUS_L_SONDE

Auslesen der Lambdasondenspannung vorne Bank 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_L_SONDE_WERT | real | Wert der Lambdasonden Spannung |
| STAT_L_SONDE_EINH | string | Einheit der Lambdasonden Spannung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde-2"></a>
### STATUS_L_SONDE_2

Auslesen der Lambdasondenspannung vorne Bank 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_L_SONDE_2_WERT | real | Wert der Lambdasonden Spg. |
| STAT_L_SONDE_2_EINH | string | Einheit der Lambdasonden Spg. |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde-h"></a>
### STATUS_L_SONDE_H

Auslesen der Lambdasondenspannung hinten Bank 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_L_SONDE_H_WERT | real | Wert der hinteren Lambdasonden Spg. |
| STAT_L_SONDE_H_EINH | string | Einheit der hinteren Lambdasonden Spg. |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde-2-h"></a>
### STATUS_L_SONDE_2_H

Auslesen der Lambdasondenspannung hinten Bank 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_L_SONDE_2_H_WERT | real | Wert der hinteren Lambdasonden Spg. Bank2 |
| STAT_L_SONDE_2_H_EINH | string | Einheit der hinteren Lambdasonden Spg. Bank2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-int"></a>
### STATUS_INT

Auslesen der Lambdaregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_INT_WERT | real | Wert der Lambdasondenregelung |
| STAT_INT_EINH | string | Einheit der Lambdasondenregelung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-int-2"></a>
### STATUS_INT_2

Auslesen der Lambdaregelung Bank2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_INT_2_WERT | real | Wert der Lambdasondenregelung Bank2 |
| STAT_INT_2_EINH | string | Einheit der Lambdasondenregelung Bank2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-add"></a>
### STATUS_ADD

Auslesen der additiven Lambdaregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_ADD_WERT | real | Wert des additiven Lambdaregelung |
| STAT_ADD_EINH | string | Einheit des additiven Lambdaregelung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-add-2"></a>
### STATUS_ADD_2

Auslesen der additiven Lambdaregelung Bank2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_ADD_2_WERT | real | Wert des additiven Lambdaregelung Bank2 |
| STAT_ADD_2_EINH | string | Einheit des additiven Lambdaregelung Bank2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mul"></a>
### STATUS_MUL

Auslesen der multipikativen Lambdaregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_MUL_WERT | real | Wert des multiplikativen Lambdaregelung |
| STAT_MUL_EINH | string | Einheit des multiplikativen Lambdaregelung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mul-2"></a>
### STATUS_MUL_2

Auslesen der multipikativen Lambdaregelung Bank 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_MUL_2_WERT | real | Wert des multiplikativen Lambdaregelung Bank2 |
| STAT_MUL_2_EINH | string | Einheit des multiplikativen Lambdaregelung Bank2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motorlaufunruhe"></a>
### STATUS_MOTORLAUFUNRUHE

Auslesen der Laufunruhewerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_ZYL1_WERT | real | Wert von LUTSFI1 |
| STAT_ZYL2_WERT | real | Wert von LUTSFI2 |
| STAT_ZYL3_WERT | real | Wert von LUTSFI3 |
| STAT_ZYL4_WERT | real | Wert von LUTSFI4 |
| STAT_ZYL5_WERT | real | Wert von LUTSFI5 |
| STAT_ZYL6_WERT | real | Wert von LUTSFI6 |
| STAT_ZYL7_WERT | real | Wert von LUTSFI7 |
| STAT_ZYL8_WERT | real | Wert von LUTSFI8 |
| STAT_LAUFUNRUHE_EINH | string | Einheit in sec-1 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

Auslesen der Batteriespannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_UBATT_WERT | real | Wert der Batterie-Spg. |
| STAT_UBATT_EINH | string | Einheit der Batterie-Spg. |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-geberrad-adaption"></a>
### STATUS_GEBERRAD_ADAPTION

Auslesen der NWG-Adaptionen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_GEBERRAD_ADAPTION_VSA_WERT | real | Wert von vsa_adp |
| STAT_GEBERRAD_ADAPTION_VSA_EINH | string | Wert von vsa_adp Einheit in Grd KW |
| STAT_GEBERRAD_ADAPTION_VSA_2_WERT | real | Wert von vsa2_adp |
| STAT_GEBERRAD_ADAPTION_VSA_2_EINH | string | Wert von vsa2_adp Einheit in Grd KW |
| STAT_GEBERRAD_ADAPTION_VSE_WERT | real | Wert von vse_adp |
| STAT_GEBERRAD_ADAPTION_VSE_EINH | string | Wert von vse_adp Einheit in Grd KW |
| STAT_GEBERRAD_ADAPTION_VSE_2_WERT | real | Wert von vse2_adp |
| STAT_GEBERRAD_ADAPTION_VSE_2_EINH | string | Wert von vse2_adp Einheit in Grd KW |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Auslesen von SchalterStatusflags

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_KL15_EIN | int | Bedingung KL15 ein |
| STAT_ESTART_EIN | int | Bedingung Startrelais |
| STAT_KUP_EIN | int | Bedingung Kupplung betaetigt |
| STAT_BLS_EIN | int | Bedingung Bremsschalter ein |
| STAT_BLTS_EIN | int | Bedingung Bremslichttestschalter ein |
| STAT_KO_EIN | int | Bedingung Klimakompressor ein |
| STAT_AC_EIN | int | Dummy fuer Klimaanforderung (entspricht Klimakompressor ein) |
| STAT_LL_EIN | int | Zustand Leerlauf erreicht |
| STAT_VL_EIN | int | Zustand Vollast erreicht |
| STAT_SBBHK2_EIN | int | Lambdasondenbereitschaft hinter Kat Bank2 |
| STAT_SBBHK_EIN | int | Lambdasondenbereitschaft hinter Kat Bank1 |
| STAT_SBBVK2_EIN | int | Lambdasondenbereitschaft vor Kat Bank2 |
| STAT_SBBVK_EIN | int | Lambdasondenbereitschaft vor Kat Bank1 |
| STAT_LR2_EIN | int | Zustand Lambdaregelung Bank2 ein |
| STAT_LR_EIN | int | Zustand Lambdaregelung Bank1 ein |
| STAT_KD_EIN | int | Zustand KickDown ein |
| STAT_PN_EIN | int | Zustand Park-Neutral ein |
| STAT_ECULOCK_EIN | int | Zustand EWS_OK ein |
| STAT_TEHB_EIN | int | Zustand TEHB ein |
| STAT_SA_EIN | int | Zustand Schubabschneiden ein |
| STAT_LRNRDY_EIN | int | Zustand UMA Lernerfolg |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pwg-poti-spannung"></a>
### STATUS_PWG_POTI_SPANNUNG

Auslesen des Pedalwertgebers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_PWG_POTI_SPANNUNG_1_WERT | real | Wert von upwg1_w |
| STAT_PWG_POTI_SPANNUNG_2_WERT | real | Wert von upwg2_w |
| STAT_PWG_POTI_SPANNUNG_EINH | string | Einheit in V |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-wechselcode-sync-dme"></a>
### WECHSELCODE_SYNC_DME

EWS zuruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "ACKNOWLEDGE", wenn fehlerfrei |

<a id="job-tester"></a>
### TESTER

Ausfuehren eines Telegramms mit Uebergabe nur der Daten 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| REQUEST | binary | Daten ohne Header  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| RESPONSE | binary | Daten ohne Header |

<a id="job-status-oelsensor"></a>
### STATUS_OELSENSOR

Temperatur, Niveau, Permitivitaet

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_OELNIVEAU_WERT | real | Wert von oznivakt |
| STAT_OELTEMPERATUR_WERT | real | Wert von oztmpakt |
| STAT_OELPERMITIVITAET_WERT | real | Wert von ozprmakt |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-generator"></a>
### IDENT_GENERATOR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| LIEFERANT | string |  |
| ID_BMW_NR | string | wird noch nicht unterstützt |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-lshv"></a>
### START_SYSTEMCHECK_LSHV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_SONDEN | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-lshv"></a>
### STOP_SYSTEMCHECK_LSHV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_SONDEN | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-lshv"></a>
### STATUS_SYSTEMCHECK_LSHV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_LAMSONI_VOR_ANFETTEN_WERT | real | Wert von lamsoni_w |
| STAT_LAMSONI_VOR_ANFETTEN_EINH | string | Einheit von lamsoni_w |
| STAT_LAMSONI2_VOR_ANFETTEN_WERT | real | Wert von lamsoni2_w |
| STAT_LAMSONI2_VOR_ANFETTEN_EINH | string | Einheit von lamsoni2_W |
| STAT_USHK_NACH_ANFETTEN_WERT | real | Wert von ushk_2 |
| STAT_USHK_NACH_ANFETTEN_EINH | string | Einheit von ushk_2 |
| STAT_USHK2_NACH_ANFETTEN_WERT | real | Wert von ushk_2 |
| STAT_USHK2_NACH_ANFETTEN_EINH | string | Einheit von ushk_2 |
| STAT_LAMSONI_VOR_ABMAGERN_WERT | real | Wert von lamsoni_w |
| STAT_LAMSONI_VOR_ABMAGERN_EINH | string | Einheit von lamsoni_w |
| STAT_LAMSONI2_VOR_ABMAGERN_WERT | real | Wert von lamsoni2_w |
| STAT_LAMSONI2_VOR_ABMAGERN_EINH | string | Einheit von lamsoni2_W |
| STAT_USHK_NACH_ABMAGERN_WERT | real | Wert von ushk_2 |
| STAT_USHK_NACH_ABMAGERN_EINH | string | Einheit von ushk_2 |
| STAT_USHK2_NACH_ABMAGERN_WERT | real | Wert von ushk_2 |
| STAT_USHK2_NACH_ABMAGERN_EINH | string | Einheit von ushk_2 |
| STAT_TKTSTOER_WERT | real |  |
| STAT_SONDEN | string |  |
| STAT_SONDEN_ERW | string |  |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ekp-sperren"></a>
### STEUERN_EKP_SPERREN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ekp-sperren-aus"></a>
### STEUERN_EKP_SPERREN_AUS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (4 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (72 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (9 × 2)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [CBSKENNUNG](#table-cbskennung) (14 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (212 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (12 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (212 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (223 × 9)
- [FARTTYP](#table-farttyp) (207 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (236 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [BETRIEBSWTAB](#table-betriebswtab) (222 × 13)
- [BITS](#table-bits) (121 × 4)
- [VVTSTATUSBG2_2](#table-vvtstatusbg2-2) (11 × 2)
- [SONDENSTATUS](#table-sondenstatus) (11 × 2)
- [SONDENSTATUS_ERW](#table-sondenstatus-erw) (13 × 2)
- [GENHERSTELLER](#table-genhersteller) (4 × 2)
- [EWSSTART](#table-ewsstart) (5 × 2)
- [EWSEMPFANGSSTATUS](#table-ewsempfangsstatus) (15 × 2)
- [REGEL](#table-regel) (7 × 2)
- [SLSSTATUS](#table-slsstatus) (29 × 2)
- [TEVSTATUS](#table-tevstatus) (9 × 2)
- [STAGEDMTL](#table-stagedmtl) (19 × 2)
- [STAGEDMTLFREEZE](#table-stagedmtlfreeze) (23 × 2)
- [LSUSTATUS](#table-lsustatus) (4 × 2)
- [DISASTATUS](#table-disastatus) (9 × 2)
- [LAMBDASTATUS](#table-lambdastatus) (6 × 2)
- [BETRIEBSSTUNDENSTATUS](#table-betriebsstundenstatus) (4 × 2)
- [KATSTATUS](#table-katstatus) (7 × 2)
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

Dimensions: 72 rows × 2 columns

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
| 0x10 | Testbedingungen erfuellt |
| 0x11 | Testbedingungen noch nicht erfuellt |
| 0x20 | Fehler bisher nicht aufgetreten |
| 0x21 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x22 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase) |
| 0x23 | Fehler momentan vorhanden und bereits gespeichert |
| 0x30 | Fehler wuerde kein Aufleuchten einer Warnlampe verursachen |
| 0x31 | Fehler wuerde das Aufleuchten einer Warnlampe verursachen |
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
| 0x03 | Speicher geloescht |
| 0x04 | nicht benutzt |
| 0x05 | Signaturpruefung PAF nicht durchgefuehrt |
| 0x06 | Signaturpruefung DAF nicht durchgefuehrt |
| 0x07 | Programmprogrammiersitzung aktiv |
| 0x08 | Datenprogrammiersitzung aktiv |
| 0x09 | Hardwarereferenzeintrag fehlerhaft |
| 0x0A | Programmreferenzeintrag fehlerhaft |
| 0x0B | Referenzierungsfehler Hardware -&gt; Programm |
| 0x0C | Programm nicht vorhanden oder nicht vollstaendig |
| 0x0D | Datenreferenzeintrag fehlerhaft |
| 0x0E | Referenzierungsfehler Programm -&gt; Daten |
| 0x0F | Daten nicht vorhanden oder nicht vollstaendig |
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

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 9 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0100 | Batteriesensor |
| 0x0200 | Elektrische Wasserpumpe |
| 0x0300 | Generator 1 |
| 0x0350 | Generator 2 |
| 0x0400 | Schaltzentrum Lenksäule |
| 0x0500 | DSC Sensor-Cluster |
| 0x0600 | Nahbereichsradarsensor links |
| 0x0700 | Nahbereichsradarsensor rechts |
| 0xFFFF | unbekannter Verbauort |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-cbskennung"></a>
### CBSKENNUNG

Dimensions: 14 rows × 3 columns

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
| 0x14 | Ueb | Uebergabedurchsicht |
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

Dimensions: 4 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| 1 | BMW-FAST |
| 2 | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 212 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x29CC | CDKMD - Aussetzererkennung Summenfehler |
| 0x29CD | CDKMD00 - Aussetzererkennung Zylinder 1 in 1.Zuendreihenfolge |
| 0x29CE | CDKMD03 - Aussetzererkennung Zylinder 2 in 4.Zuendreihenfolge |
| 0x29CF | CDKMD01 - Aussetzererkennung Zylinder 3 in 2.Zuendreihenfolge |
| 0x29D0 | CDKMD02 - Aussetzererkennung Zylinder 4 in 3.Zuendreihenfolge |
| 0x29D9 | CDKCPFLL - Verbrennungsaussetzer bei geringem Tankfüllstand |
| 0x29DD | CDKSWE - Schlechtwegstreckenerkennung |
| 0x29E5 | CDKFRAO - LR-Adaption multiplikativ Bereich2 (Bank1) |
| 0x29E6 | CDKFRAO2 - LR-Adaption multiplikativ Bereich2 (Bank2) |
| 0x29E7 | CDKRKAT - LR-Adaption additiv pro Zeit (Bank1) |
| 0x29E8 | CDKRKAT2 - LR-Adaption additiv pro Zeit (Bank2) |
| 0x29E9 | CDKRKAZ - LR-Adaption additiv pro Zuendung |
| 0x29EA | CDKRKAZ2 - LR-Adaption additiv pro Zuendung Bank2 |
| 0x29EB | CDKFRST - LR-Abweichung |
| 0x29EC | CDKFRST2 - LR-Abweichung Bank2 |
| 0x29ED | CDKFRAU - LR-Adaption multiplikativ Bereich1 (Bank1) |
| 0x29EE | CDKFRAU2 - LR-Adaption multiplikativ Bereich1 (Bank2) |
| 0x29F4 | CDKKAT - Katalysator-Konvertierung |
| 0x29F5 | CDKKAT2 - Katalysator-Konvertierung (Bank2) |
| 0x29F8 | CDKKATSP - Katalysator-Konvertierung LSU |
| 0x29F9 | CDKKATSP2 - Katalysator-Konvertierung LSU Bank2 |
| 0x29FE | CDKSLS - Sekundaerluftsystem |
| 0x29FF | CDKSLS2 - Sekundaerluftsystem (Bank2) |
| 0x2A01 | CDKSLV - Sekundaerluftventil |
| 0x2A02 | CDKSLVE - Ansteuerung Sekundaerluftventil |
| 0x2A03 | CDKSLPE - Sekundaerluftpumperelais |
| 0x2A05 | CDKSLV2 - Sekundaerluftventil Bank2 |
| 0x2A0E | CDKAGRF - AGR Ventil |
| 0x2A14 | CDKDMTK - DM-TL Feinleck |
| 0x2A17 | CDKDMTL - DM-TL Modul |
| 0x2A19 | CDKTEVE - Tankentlueftungsventil |
| 0x2A1A | CDKTES - Tankentlueftung functional check |
| 0x2A1D | CDKTESK - Tankleckueberwachung |
| 0x2A1E | CDKLDP - Leckdiagnosepumpe |
| 0x2A58 | CDKVVTE - VVT-Enable Ansteuerung |
| 0x2A59 | CDKDVFFS - VVT-Fuehrungssensor |
| 0x2A5B | CDKDVFRS - VVT-Referenzsensor |
| 0x2A5D | CDKDVPLA - VVT-Sensorplausibilisierung |
| 0x2A5F | CDKDVUSE - VVT-Versorgungsspannung Sensor |
| 0x2A61 | CDKDVLRN - VVT-Lernfunktion Anschlag |
| 0x2A63 | CDKDVSTE - VVT-Stellgliedueberwachung |
| 0x2A67 | CDKDVEST - VVT-Ansteuerung |
| 0x2A69 | CDKDVULV - VVT-Leistungsversorgung |
| 0x2A6B | CDKDVPMN - Leistungsbegrenzung VVT-Notlauf |
| 0x2A6C | CDKDVALRN - VVT-Anschlaege lernen notwendig |
| 0x2A6D | CDKDVOVL - VVT-Systemueberlast |
| 0x2A6F | CDKMINHUB - Minhubadaption Anschlag mehrfach |
| 0x2A70 | CDKDIVVT - Fehler Stromplausibilisierung |
| 0x2A71 | CDKVVTRE - Endstufendiagnose Entlastungsrelais VVT |
| 0x2A72 | CDKVVTLRU - Stellgliedüberwachung VVT Hubverstellung |
| 0x2A80 | CDKENWSE - Einlass-VANOS |
| 0x2A83 | CDKENWS - Nockenwellensteuerung- Einlass |
| 0x2A85 | CDKANWSE - Auslass-VANOS |
| 0x2A88 | CDKANWS - Nockenwellensteuerung Auslass |
| 0x2B5C | CDKN - Kurbelwellengeber |
| 0x2B5D | CDKBM - Bezugsmarkengeber |
| 0x2B61 | CDKNWKW - Zuordnung Nockenwelle zur Kurbelwelle |
| 0x2B62 | CDKPH - Nockenwellengeber Einlass |
| 0x2B63 | CDKPH2 - Nockenwellengeber Auslass |
| 0x2B66 | CDKPHM - Master Nockenwellengeber |
| 0x2B70 | CDKSUE - DISA |
| 0x2B80 | CDKLLR - Leerlaufregelung |
| 0x2B8A | CDKKRNT - Klopfregelung Nulltest |
| 0x2B8B | CDKKROF - Klopfregelung Offset |
| 0x2B8C | CDKKRTP - Klopfregelung Testimpuls |
| 0x2B98 | CDKNVRMON - Plausibilitaetsueberwachung RAM-Backup |
| 0x2B99 | CDKNVRBUP - RAM Backup |
| 0x2B9A | CDKURRAM - SG Selbsttest RAM |
| 0x2B9B | CDKURROM - SG Selbsttest ROM |
| 0x2B9C | CDKURRST - SG Selbsttest RESET |
| 0x2B9D | CDKWDA - Ueberspanungserkennung auf VCC |
| 0x2BA7 | CDKMDB - Momentenbegrenzung Ebene 1 |
| 0x2BB6 | CDKUBR - Überwachung Hauptrelais |
| 0x2B9E | CDKFETRWE - Energiesparmode aktiv |
| 0x2C24 | CDKLSVV - Vertauschte Lambdasonden |
| 0x2C45 | CDKLSV - Lambda-Sonde vor Kat |
| 0x2C46 | CDKLSV2 - Lambda-Sonde vor Kat(Bank2) |
| 0x2C55 | CDKLATP - Lambda-Sondenalterung Periodendauer |
| 0x2C56 | CDKLATV - Lambda-Sondenalterung TV |
| 0x2C6A | CDKLSHV - Vertauschte Lambdasonden hinter Kat |
| 0x2C6D | CDKLASH - Lambda-Sondenalterung hinter Kat (BAnk1) |
| 0x2C6E | CDKLASH2 - Lambda-Sondenalterung hinter Kat (Bank2) |
| 0x2C6F | CDKLAVH - Lambdasondenalterung hinter Kat (VL- Prüfung) |
| 0x2C70 | CDKLAVH2 - Lambdasondenalterung hinter Kat Bank2 |
| 0x2C71 | CDKLSH - Lambda-Sonde hinter Kat |
| 0x2C72 | CDKLSH2 - Lambda-Sonde hinter Kat (Bank2) |
| 0x2C9C | CDKHSVE - Endstufe Heizung Sonde vor Katalysator |
| 0x2C9D | CDKHSVE2 - Endstufe Heizung Sonde vor Katalysator Bank2 |
| 0x2C9E | CDKHSHE - Ansteuerung Heizung Sonde hinter Kat |
| 0x2C9F | CDKHSHE2 - Ansteuerung Heizung Sonde hinter Kat (Bank2) |
| 0x2CA0 | CDKHSV - Lambdasonden-Heizung vor Kat |
| 0x2CA1 | CDKHSV2 - Lambdasonden-Heizung vor Kat (Bank2) |
| 0x2CA2 | CDKHSVSA - Heizung Lambdasonde vor Kat (Schubspannung) |
| 0x2CA3 | CDKHSVSA2 - Heizung Lambdasonde vor Kat (Schubspannung) Bank2 |
| 0x2CA8 | CDKHSH - Lambdasonden-Heizung hinter Kat |
| 0x2CA9 | CDKHSH2 - Lambdasonden-Heizung hinter Kat (Bank2) |
| 0x2CEF | CDKDVEE - DK-Steller |
| 0x2CF0 | CDKDVER - DK-Steller Regelbereich |
| 0x2CF1 | CDKDVEL - DK Positionsueberwachung |
| 0x2CF8 | CDKDK - DK-Potentiometer |
| 0x2CF9 | CDKDK1P - Drosselklappenpoti 1 |
| 0x2CFA | CDKDK2P - Drosselklappenpoti 2 |
| 0x2CFF | CDKDVEV - DK-Steller Fehler bei Verstaerkerabgleich |
| 0x2D00 | CDKDVEF - Federpruefung DK-Steller schliessende Feder |
| 0x2D01 | CDKDVEFO - Federpruefung DK-Steller oeffnende Feder |
| 0x2D02 | CDKDVEN - Pruefung Notluftpunkt |
| 0x2D03 | CDKDVEUB - Abbruch DV-Adaption wegen Umweltbedingungen |
| 0x2D04 | CDKDVEU - Drosselklappen- Adaption |
| 0x2D05 | CDKDVEUW - Abbruch bei UMA-Wiederlernen |
| 0x2D08 | CDKDVET - Tauscherkennung ohne Adaption |
| 0x2D10 | CDKHFMPL - Plausibilisierung HFM |
| 0x2D11 | CDKMSLAM - Plausibilisierung, Massenstrom Lambdasonde |
| 0x2D12 | CDKMSLAM2 - Plausibilisierung, Massenstrom Lambdasonde Bank2 |
| 0x2D0F | CDKLM - Heissfilmluftmassenmesser |
| 0x2D19 | CDKBWF  - PWG-Bewegung |
| 0x2D1A | CDKFPP - Pedalwertgeber |
| 0x2D1B | CDKFP1P - Pedalwertgeber Poti1 |
| 0x2D1C | CDKFP2P - Pedalwertgeber Poti2 |
| 0x2D28 | CDKDDSS - Differenzdrucksensor Saugrohr |
| 0x2D29 | CDKPDDSS - Plausibilitaet Differenzdrucksensor |
| 0x2D32 | CDKDPSRPL - Plausibilitaet Drucksensor Saugrohr |
| 0x2D6E | CDKUFMV - Momentenueberwachung Ebene 2 |
| 0x2D6F | CDKUFRLIP - Lastsensorueberwachung |
| 0x2D70 | CDKUFSGA - Steuergeraeteueberwachung Gruppe A |
| 0x2D71 | CDKUFSGB - Steuergeraeteueberwachung Gruppe B |
| 0x2D72 | CDKUFSGC - Steuergeraeteueberwachung Gruppe C |
| 0x2D73 | CDKUFPR - Kraftstoffdrucksensor |
| 0x2D74 | CDKUFRKC - Funktionsüberwachung: Lambda-Plausibilisierung |
| 0x2D75 | CDKUFNC - Motordrehzahlueberwachung |
| 0x2D76 | CDKUFSPSC - Pedalwertgeberueberwachung (Ebene2) |
| 0x2D78 | CDKUFMSAC - Ueberwachung Luftmassenstromabgleich |
| 0x2DB4 | CDKMFL - Schnittstelle MFL |
| 0x2DBF | CDKCACC  - CAN ACC Signalfehler |
| 0x2DCA | CDKCEGS - CAN Timeout Getriebesteuergeraet |
| 0x2DCB | CDKCSSG - CAN SSG Signalfehler |
| 0x2DCF | CDKCINS  - CAN- Timeout Instrumentenkombination |
| 0x2DD7 | CDKCDSC - CAN Timeout DSG SG |
| 0x2DD8 | CDKCAFS - Active Front Steering Moment |
| 0x2DD9 | CDKCARS  - CAN ARS Signalfehler |
| 0x2DDA | CDKCCAS  - CAN CAS Signalfehler |
| 0x2DDB | CDKCIHKA  - CAN IHKA Signalfehler |
| 0x2DDC | CDKCSZL  - CAN  SZL Signalfehler |
| 0x2DDD | CDKCVVT - CAN-Timeout VVT-Steuergeraet |
| 0x2DEB | CDKPMBN - Powermanagement Bordnetz |
| 0x2DEC | CDKPMBAT - Powermanagement Batterie |
| 0x2DED | CDKPMRUHV - Powermanagement Ruhestromverletzung |
| 0x2E24 | CDKDZKU0 - Zuendspule Zylinder 1 in 1.Zuendreihenfolge |
| 0x2E25 | CDKDZKU3 - Zuendspule Zylinder 2 in 4.Zuendreihenfolge |
| 0x2E26 | CDKDZKU1 - Zuendspule Zylinder 3 in 2.Zuendreihenfolge |
| 0x2E27 | CDKDZKU2 - Zuendspule Zylinder 4 in 3.Zuendreihenfolge |
| 0x2E30 | CDKEV1 - Einspritzventil Zylinder 1 in 1. Zylinderreihenfolge |
| 0x2E31 | CDKEV4 - Einspritzventil Zylinder 2 in 4. Zylinderreihenfolge |
| 0x2E32 | CDKEV2 - Einspritzventil Zylinder 3 in 2. Zylinderreihenfolge |
| 0x2E33 | CDKEV3 - Einspritzventil Zylinder 4 in 3. Zylinderreihenfolge |
| 0x2E68 | CDKKS1 - Klopfsensor1 |
| 0x2E69 | CDKKS2 - Klopfsensor2 (Bank1) |
| 0x2E6A | CDKKS3 - Klopfsensor3 |
| 0x2E6B | CDKKS4 - Klopfsensor4 |
| 0x2E7C | CDKBSD - BSD-Leitungsfehler |
| 0x2E86 | CDKEWAPU - Elektrische Wasserpumpe |
| 0x2E8B | CDKIBSK - IBS Kommunikation |
| 0x2E8C | CDKIBSP - IBS Eigendiagnose 1 |
| 0x2E8D | CDKIBSA - IBS Eigendiagnose 2 |
| 0x2E95 | CDKDGENBS - Generatorkommunikation |
| 0x2E97 | CDKDGEN/CDKGEN - BSD Generator |
| 0x2E9F | CDKOEZS - Fehler Oelqualitaetssensor |
| 0x2EA0 | CDKQLT - Oelzustandssensor |
| 0x2EB8 | CDKBSDD0 - BSD-Botschaft vom IBS fehlt |
| 0x2EBC | CDKBSDD4 - BSD-Botschaft vom Ölzustandssensor fehlt |
| 0x2EBD | CDKBSDD5 - BSD-Botschaft vom Generator fehlt |
| 0x2EBE | CDKBSDD6-BSD-Botschaft vom Generator fehlt |
| 0x2EE0 | CDKTM - Temperaturfuehler Motorkuehlmittel |
| 0x2EEA | CDKTKA - Temperaturfuehler Kuehleraustritt |
| 0x2EF4 | CDKTHS - Thermostat Kennfeldkühlung, mechanisch |
| 0x2EF5 | CDKETS - Thermostat Kennfeldkühlung, Ansteuerung |
| 0x2EF6 | CDKKFT - Kennfeldthermostat |
| 0x2EFE | CDKMLE - Motorluefter |
| 0x2F08 | CDKTA - Ansauglufttemperatur |
| 0x2F12 | CDKKOSE - Klimakompressorsteuerung |
| 0x2F17 | CDKMTOEL - Zwangsschaltung EGS |
| 0x2F21 | CDKWMKD - Motorsteuerung, Leistungsreduktion |
| 0x2F44 | CDKWFS - EWS3.3 Manipulationsschutz |
| 0x2F45 | CDKDWA - EWS3.3 Schnittstelle DME-EWS |
| 0x2F46 | CDKWCA - EWS3.3 Wechselcode-Abspeicherung |
| 0x2F4E | CDKVFZ - Fahrzeuggeschwindigkeit |
| 0x2F50 | CDKVAT - Geschwindigkeitsanzeige im Kombi Fehlerhaft  |
| 0x2F58 | CDKSTAE - Startautomatik Ansteuerung |
| 0x2F59 | CDKSTS - Startautomatik Eingang |
| 0x2F5A | CDKSTA - Startautomatik |
| 0x2F62 | CDKBREMS - Schalter Bremse |
| 0x2F67 | CDKKUPPL - Schalter Kupplung |
| 0x2F6C | CDKAKRE - Ansteuerung Abgasklappe |
| 0x2F71 | CDKELS - E-Box Luefter |
| 0x2F76 | CDKDSU - Drucksensor Umgebung |
| 0x2F7B | CDKPOELS - Oeldruckschalter |
| 0x2F80 | CDKCUHR - Fehler CAN / relativer Zeitgeber |
| 0x2F85 | CDKTSG - DME- Temperatur |
| 0x2F8A | CDKUB - Batteriespannung |
| 0x2F94 | CDKKPE - Kraftstoffpumpen-Relais |
| 0x2F99 | CDKTUM - Umgebungstemperatur |
| 0x2F9E | CDKTOENS - Thermischer Oelniveausensor |
| 0x2FA3 | CDKCOD - HO-Prozessfehler, Codierung fehlt |
| 0xCD87 | CDKCANA - PT - CAN Bus Off |
| 0xCD8B | CDKCANB - Local CAN Bus Off |
| 0xCD9B | CDKX315 - Status Fahrzeugmodus |
| 0xCDA1 | CDKXC4 - Lenkradwinkel |
| 0xCDA2 | CDKX3B4 - Powermanagement Batteriespannung |
| 0xCDA3 | CDKX334 - Powermanagement Ladespannung |
| 0xCDA7 | CDKX3B0 - Status Gang Rückwärts |
| 0xCDAA | CDKX135 - Steuerung Crashabschaltung EKP |
| 0xCDAC | CDKX3B5 - Status Wasserventil |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | 00654321 |
| F_PCODE | ja |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 12 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxxx0 | 10 | -- |
| xxxxxxx1 | 11 | Diagnose aktiv  |
| xxxxxx0x | 20 | -- |
| xxxxxx1x | 21 | Diagnose gestoppt |
| xxxxx0xx | 30 | -- |
| xxxxx1xx | 31 | Zyklus-Flag gesetzt |
| xxxx0xxx | 40 | -- |
| xxxx1xxx | 41 | Error-Flag gesetzt |
| xxx0xxxx | 50 | -- |
| xxx1xxxx | 51 | MIL ein |
| xx0xxxxx | 60 | -- |
| xx1xxxxx | 61 | Fehler in Entprellphase |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 212 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x29CC | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x29CD | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x29CE | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x29CF | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x29D0 | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x29D9 | 0x0A | 0x12 | 0x3C | 0x1A |
| 0x29DD | 0x0A | 0x1A | 0x0B | 0x8C |
| 0x29E5 | 0x0A | 0x1A | 0x13 | 0x3C |
| 0x29E6 | 0x0A | 0x1A | 0x13 | 0x3C |
| 0x29E7 | 0x0A | 0x1A | 0x3C | 0x05 |
| 0x29E8 | 0x0A | 0x1A | 0x3C | 0x07 |
| 0x29E9 | 0x0A | 0x1A | 0x3C | 0x05 |
| 0x29EA | 0x0A | 0x1A | 0x3C | 0x07 |
| 0x29EB | 0x0A | 0x14 | 0x12 | 0x8C |
| 0x29EC | 0x0A | 0x14 | 0x12 | 0x8C |
| 0x29ED | 0x0A | 0x1A | 0x13 | 0x3C |
| 0x29EE | 0x0A | 0x1A | 0x13 | 0x3C |
| 0x29F4 | 0xA3 | 0x1A | 0xBF | 0xB2 |
| 0x29F5 | 0xA4 | 0x1A | 0xC0 | 0xB3 |
| 0x29F8 | 0xA3 | 0x1A | 0xBF | 0xB2 |
| 0x29F9 | 0xA4 | 0x1A | 0xC0 | 0xB3 |
| 0x29FE | 0xCC | 0xCD | 0xCE | 0xCF |
| 0x29FF | 0xD0 | 0xD1 | 0xD2 | 0xD3 |
| 0x2A01 | 0x0A | 0x11 | 0x14 | 0x05 |
| 0x2A02 | 0x0A | 0x12 | 0x13 | 0x14 |
| 0x2A03 | 0x0A | 0x12 | 0x13 | 0x14 |
| 0x2A05 | 0x0A | 0x11 | 0x14 | 0x07 |
| 0x2A0E | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x2A14 | 0x3C | 0x35 | 0x24 | 0x14 |
| 0x2A17 | 0x3C | 0x35 | 0x24 | 0x14 |
| 0x2A19 | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x2A1A | 0x0A | 0x1A | 0x24 | 0x35 |
| 0x2A1D | 0x0A | 0x24 | 0x14 | 0x12 |
| 0x2A1E | 0x0A | 0x35 | 0x24 | 0x14 |
| 0x2A58 | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x2A59 | 0x14 | 0xEF | 0xE8 | 0xE9 |
| 0x2A5B | 0x14 | 0xEF | 0xE8 | 0xE9 |
| 0x2A5D | 0xEA | 0xEE | 0xE8 | 0xE9 |
| 0x2A5F | 0x14 | 0xEF | 0xE8 | 0xE9 |
| 0x2A61 | 0xF0 | 0xF1 | 0xE8 | 0xE6 |
| 0x2A63 | 0x14 | 0xE4 | 0xEB | 0xEC |
| 0x2A67 | 0x14 | 0xF7 | 0xF6 | 0xEE |
| 0x2A69 | 0x14 | 0xF5 | 0xF7 | 0xA5 |
| 0x2A6B | 0x11 | 0xF6 | 0xE8 | 0xE9 |
| 0x2A6C | 0xF0 | 0xF1 | 0xE8 | 0xE6 |
| 0x2A6D | 0x0A | 0xF6 | 0xF2 | 0xF3 |
| 0x2A6F | 0x0A | 0x12 | 0x13 | 0xF8 |
| 0x2A70 | 0xF7 | 0xE4 | 0xE2 | 0xE3 |
| 0x2A71 | 0x14 | 0xF7 | 0xF5 | 0x8C |
| 0x2A72 | 0x14 | 0xEB | 0xEC | 0xF3 |
| 0x2A80 | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x2A83 | 0x0A | 0x12 | 0x1A | 0x6C |
| 0x2A85 | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x2A88 | 0x0A | 0x12 | 0x1A | 0x14 |
| 0x2B5C | 0x0A | 0x12 | 0x24 | 0x14 |
| 0x2B5D | 0x0A | 0x12 | 0x24 | 0x14 |
| 0x2B61 | 0x0A | 0x12 | 0x1A | 0xFF |
| 0x2B62 | 0x0A | 0x12 | 0x24 | 0x14 |
| 0x2B63 | 0x0A | 0x12 | 0x24 | 0x14 |
| 0x2B66 | 0x0A | 0x12 | 0x24 | 0x14 |
| 0x2B70 | 0x0A | 0x12 | 0x13 | 0x23 |
| 0x2B80 | 0x0A | 0x1A | 0x14 | 0x15 |
| 0x2B8A | 0x0A | 0x1A | 0x14 | 0x80 |
| 0x2B8B | 0x0A | 0x1A | 0x14 | 0x81 |
| 0x2B8C | 0x0A | 0x1A | 0x77 | 0x81 |
| 0x2B98 | 0x14 | 0xBE | 0x12 | 0x24 |
| 0x2B99 | 0x0A | 0x14 | 0x12 | 0xFF |
| 0x2B9A | 0x0A | 0x1A | 0x1F | 0x22 |
| 0x2B9B | 0x0A | 0x1A | 0x1F | 0x22 |
| 0x2B9C | 0x0A | 0x1A | 0x1F | 0x22 |
| 0x2B9D | 0x0A | 0x1A | 0x14 | 0x8C |
| 0x2BA7 | 0x0A | 0x23 | 0x1A | 0x12 |
| 0x2BB6 | 0x0A | 0x14 | 0x24 | 0x12 |
| 0x2B9E | 0x0A | 0x14 | 0x24 | 0x12 |
| 0x2C24 | 0x12 | 0x8C | 0x06 | 0x08 |
| 0x2C45 | 0xA1 | 0xA8 | 0x29 | 0x17 |
| 0x2C46 | 0xA2 | 0xA9 | 0x2A | 0x19 |
| 0x2C55 | 0x0A | 0x29 | 0x31 | 0x36 |
| 0x2C56 | 0x0A | 0x29 | 0x31 | 0x36 |
| 0x2C6A | 0xB2 | 0xB3 | 0x17 | 0x19 |
| 0x2C6D | 0x0A | 0x2B | 0x33 | 0x17 |
| 0x2C6E | 0x0A | 0x2C | 0x34 | 0x19 |
| 0x2C6F | 0x82 | 0xB2 | 0x2B | 0x17 |
| 0x2C70 | 0x83 | 0xB3 | 0x2C | 0x19 |
| 0x2C71 | 0x2B | 0x8C | 0x33 | 0x17 |
| 0x2C72 | 0x2C | 0x8C | 0x34 | 0x19 |
| 0x2C9C | 0x14 | 0x2D | 0x29 | 0xA8 |
| 0x2C9D | 0x14 | 0x2E | 0x2A | 0xA9 |
| 0x2C9E | 0x0A | 0x12 | 0x13 | 0x14 |
| 0x2C9F | 0x0A | 0x12 | 0x13 | 0x14 |
| 0x2CA0 | 0x2D | 0x8C | 0x14 | 0x0B |
| 0x2CA1 | 0x2E | 0x8C | 0x14 | 0x0B |
| 0x2CA2 | 0x2D | 0xA8 | 0x29 | 0x0B |
| 0x2CA3 | 0x2E | 0xA9 | 0x2A | 0x0B |
| 0x2CA8 | 0x78 | 0x2F | 0x2B | 0x33 |
| 0x2CA9 | 0x79 | 0x30 | 0x2C | 0x34 |
| 0x2CEF | 0x14 | 0x12 | 0x15 | 0x28 |
| 0x2CF0 | 0x14 | 0x13 | 0x15 | 0x28 |
| 0x2CF1 | 0x14 | 0x13 | 0x15 | 0x28 |
| 0x2CF8 | 0x0A | 0x15 | 0x26 | 0x27 |
| 0x2CF9 | 0x0A | 0x28 | 0x24 | 0x27 |
| 0x2CFA | 0x0A | 0x28 | 0x24 | 0x26 |
| 0x2CFF | 0x14 | 0x13 | 0x26 | 0x65 |
| 0x2D00 | 0x14 | 0x13 | 0x15 | 0x64 |
| 0x2D01 | 0x14 | 0x13 | 0x15 | 0x64 |
| 0x2D02 | 0x14 | 0x13 | 0x64 | 0x76 |
| 0x2D03 | 0x0A | 0x14 | 0x13 | 0x23 |
| 0x2D04 | 0x14 | 0x13 | 0x26 | 0x65 |
| 0x2D05 | 0x0A | 0x14 | 0x13 | 0x23 |
| 0x2D08 | 0x14 | 0x26 | 0x64 | 0x76 |
| 0x2D0F | 0x0A | 0x13 | 0x15 | 0x71 |
| 0x2D10 | 0x14 | 0x11 | 0x15 | 0xEB |
| 0x2D11 | 0x0A | 0x1A | 0x44 | 0x12 |
| 0x2D12 | 0x0A | 0x1A | 0x44 | 0x12 |
| 0x2D19 | 0x0A | 0x23 | 0x1B | 0x1D |
| 0x2D1A | 0x0A | 0x23 | 0x1B | 0x1D |
| 0x2D1B | 0x0A | 0x23 | 0x1B | 0x1D |
| 0x2D1C | 0x0A | 0x23 | 0x1B | 0x1D |
| 0x2D28 | 0x0A | 0x12 | 0x13 | 0x14 |
| 0x2D29 | 0x14 | 0x0A | 0x12 | 0x35 |
| 0x2D32 | 0x0A | 0x1A | 0x46 | 0x09 |
| 0x2D6E | 0x0A | 0x1A | 0x20 | 0x21 |
| 0x2D6F | 0x0A | 0x1A | 0x43 | 0x40 |
| 0x2D70 | 0x14 | 0x13 | 0x0A | 0x12 |
| 0x2D71 | 0x14 | 0x13 | 0x0A | 0x12 |
| 0x2D72 | 0x14 | 0x13 | 0x0A | 0x12 |
| 0x2D73 | 0x0A | 0x1F | 0xFF | 0xFF |
| 0x2D74 | 0x0A | 0x1A | 0xB2 | 0xB3 |
| 0x2D75 | 0x0A | 0x15 | 0x1F | 0x23 |
| 0x2D76 | 0x1B | 0x1C | 0x23 | 0x1F |
| 0x2D78 | 0x46 | 0x47 | 0x44 | 0x45 |
| 0x2DB4 | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x2DBF | 0x0A | 0x1A | 0x14 | 0x8C |
| 0x2DCA | 0x0A | 0x1A | 0x14 | 0x8C |
| 0x2DCB | 0x0B | 0x23 | 0x0A | 0xC9 |
| 0x2DCF | 0x0A | 0x1A | 0x14 | 0x8C |
| 0x2DD7 | 0x0A | 0x1A | 0x14 | 0x8C |
| 0x2DD8 | 0x0A | 0x1A | 0x14 | 0x8C |
| 0x2DD9 | 0x0A | 0x1A | 0x14 | 0x8C |
| 0x2DDA | 0x0A | 0x1A | 0x14 | 0x8C |
| 0x2DDB | 0x0A | 0x1A | 0x14 | 0x8C |
| 0x2DDC | 0x0A | 0x1A | 0x14 | 0x8C |
| 0x2DDD | 0x0A | 0x1A | 0x14 | 0x8C |
| 0x2DEB | 0x0A | 0x14 | 0xDF | 0xBA |
| 0x2DEC | 0xA5 | 0x14 | 0x48 | 0x49 |
| 0x2DED | 0xA5 | 0x4A | 0x4B | 0x4C |
| 0x2E24 | 0x0A | 0x12 | 0x03 | 0x14 |
| 0x2E25 | 0x0A | 0x12 | 0x03 | 0x14 |
| 0x2E26 | 0x0A | 0x12 | 0x03 | 0x14 |
| 0x2E27 | 0x0A | 0x12 | 0x03 | 0x14 |
| 0x2E30 | 0x0A | 0x12 | 0x14 | 0x05 |
| 0x2E31 | 0x0A | 0x12 | 0x14 | 0x07 |
| 0x2E32 | 0x0A | 0x12 | 0x14 | 0x07 |
| 0x2E33 | 0x0A | 0x12 | 0x14 | 0x05 |
| 0x2E68 | 0x0A | 0x1A | 0x8D | 0x90 |
| 0x2E69 | 0x0A | 0x1A | 0x8E | 0x8F |
| 0x2E6A | 0x0A | 0x1A | 0x8D | 0x90 |
| 0x2E6B | 0x0A | 0x1A | 0x8E | 0x8F |
| 0x2E7C | 0x4D | 0x4E | 0x14 | 0x0A |
| 0x2E86 | 0x0A | 0x12 | 0x14 | 0x13 |
| 0x2E8B | 0x0A | 0x14 | 0xD4 | 0xD5 |
| 0x2E8C | 0x0A | 0x14 | 0xD4 | 0xD5 |
| 0x2E8D | 0x0A | 0x14 | 0xD4 | 0xD5 |
| 0x2E95 | 0x0A | 0x14 | 0x13 | 0xBB |
| 0x2E97 | 0xF8 | 0x4E | 0x14 | 0x0A |
| 0x2E9F | 0x0A | 0x14 | 0x12 | 0x3C |
| 0x2EA0 | 0xFF | 0x11 | 0xFF | 0xFF |
| 0x2EB8 | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x2EBC | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x2EBD | 0x14 | 0xBA | 0x0A | 0xBB |
| 0x2EBE | 0x14 | 0xBA | 0x0A | 0xBB |
| 0x2EE0 | 0x25 | 0x13 | 0x0A | 0x72 |
| 0x2EEA | 0x0A | 0x12 | 0x24 | 0x74 |
| 0x2EF4 | 0x0A | 0x12 | 0x13 | 0x74 |
| 0x2EF5 | 0x0A | 0x12 | 0x13 | 0x14 |
| 0x2EF6 | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x2EFE | 0x0A | 0x12 | 0x14 | 0x6B |
| 0x2F08 | 0x0A | 0x12 | 0x24 | 0x73 |
| 0x2F12 | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x2F17 | 0x0A | 0x12 | 0x13 | 0x14 |
| 0x2F21 | 0x0A | 0x1A | 0x14 | 0x8C |
| 0x2F44 | 0x0A | 0x12 | 0x14 | 0xBE |
| 0x2F45 | 0x0A | 0x12 | 0x14 | 0xBE |
| 0x2F46 | 0x0A | 0x12 | 0x14 | 0xBE |
| 0x2F4E | 0x0A | 0x1A | 0xCB | 0x14 |
| 0x2F50 | 0x0A | 0x1A | 0x70 | 0x14 |
| 0x2F58 | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x2F59 | 0x0A | 0x03 | 0xFF | 0xFF |
| 0x2F5A | 0xFF | 0x1A | 0xFF | 0xFF |
| 0x2F62 | 0x0A | 0x12 | 0x0B | 0x14 |
| 0x2F67 | 0x0A | 0x12 | 0x0B | 0x14 |
| 0x2F6C | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x2F71 | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x2F76 | 0x0A | 0x0B | 0x24 | 0x75 |
| 0x2F7B | 0x12 | 0x84 | 0x8C | 0xBE |
| 0x2F80 | 0x0A | 0x1A | 0x14 | 0x8C |
| 0x2F85 | 0x14 | 0x8C | 0x12 | 0x24 |
| 0x2F8A | 0x0A | 0x14 | 0x24 | 0x12 |
| 0x2F94 | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x2F99 | 0x12 | 0x13 | 0x24 | 0x14 |
| 0x2F9E | 0x0A | 0x12 | 0x0B | 0x14 |
| 0x2FA3 | 0x14 | 0x0A | 0x8C | 0xFF |
| 0xCD87 | 0x0A | 0x1A | 0x14 | 0x8C |
| 0xCD8B | 0x0A | 0x1A | 0x14 | 0x8C |
| 0xCD9B | 0x0A | 0x1A | 0x14 | 0x8C |
| 0xCDA1 | 0x0A | 0x1A | 0x14 | 0x8C |
| 0xCDA2 | 0x0A | 0x1A | 0x14 | 0x8C |
| 0xCDA3 | 0x0A | 0x1A | 0x14 | 0x8C |
| 0xCDA7 | 0x0A | 0x1A | 0x14 | 0x8C |
| 0xCDAA | 0x0A | 0x1A | 0x14 | 0x8C |
| 0xCDAC | 0x0A | 0x1A | 0x14 | 0x8C |
| default | - | - | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 223 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x00 | --- | 1 | - | unsigned char | - | 1 | 1 | 0 |
| 0x01 | Regelstatus Bank1 (flglrs) | 1 | 0-n | unsigned char | - | 1 | 1 | 0 |
| 0x02 | Regelstatus Bank2 (flglrs2) | 1 | 0-n | unsigned char | - | 1 | 1 | 0 |
| 0x03 | Berechnete Last (rml) | % | - | unsigned char | - | 0.3906 | 1 | 0 |
| 0x04 | Motortemperatur  (tmot) | Grad C | - | unsigned char | - | 1 | 1 | -40 |
| 0x05 | Regelfaktor Bank1 (fr_u) | - | - | unsigned char | - | 0.0078 | 1 | 0 |
| 0x06 | Adaptionsfaktor Bank1 (fra_u) | - | - | unsigned char | - | 0.0078 | 1 | 0 |
| 0x07 | Regelfaktor Bank2 (fr2_u) | - | - | unsigned char | - | 0.0078 | 1 | 0 |
| 0x08 | Adaptionsfaktor Bank2 (fra_u2) | - | - | unsigned char | - | 0.0078 | 1 | 0 |
| 0x09 | Saugrohrdruck (psdss_u) | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x0A | Motordrehzahl (nmot) | /min | - | unsigned char | - | 40 | 1 | 0 |
| 0x0B | Fahrzeuggeschwindigkeit (vfzg_u) | km/h | - | unsigned char | - | 1 | 1 | 0 |
| 0x0C | --- | 1 | - | unsigned char | - | 0 | 1 | 0 |
| 0x0D | --- | 1 | - | unsigned char | - | 0 | 1 | 0 |
| 0x0E | --- | 1 | - | unsigned char | - | 0 | 1 | 0 |
| 0x0F | --- | 1 | - | unsigned char | - | 0 | 1 | 0 |
| 0x10 | --- | 1 | - | unsigned char | - | 0 | 1 | 0 |
| 0x11 | Luftmassenfluss (ml) | kg/h | - | unsigned char | - | 4 | 1 | 0 |
| 0x12 | Motortemperatur (tmot) | Grad C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0x13 | Ansauglufttemperatur (tans) | Grad C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0x14 | Versorgungsspannung (ub) | V | - | unsigned char | - | 0.0942 | 1 | 0 |
| 0x15 | Winkel DK bez. auf DK-Anschl. (wdkba) | % DK | - | unsigned char | - | 0.3922 | 1 | 0 |
| 0x16 | Sondenspannung v. Kat Bank1  (usvk) | V | - | unsigned char | - | 0.00522 | 1 | -0.2 |
| 0x17 | Sondenspannung h. Kat Bank1  (ushk) | V | - | unsigned char | - | 0.00522 | 1 | -0.2 |
| 0x18 | Sondenspannung v. Kat Bank2  (usvk2) | V | - | unsigned char | - | 0.00522 | 1 | -0.2 |
| 0x19 | Sondenspannung h. Kat Bank2  (ushk2) | V | - | unsigned char | - | 0.00522 | 1 | -0.2 |
| 0x1A | relative Luftfuellung (rl) | % | - | unsigned char | - | 0.75 | 1 | 0 |
| 0x1B | Spannung PWG Poti1 (upwg1_u) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x1C | Spannung PWG Poti2 (upwg2_u) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x1D | verdoppelte Spannung PWG Poti2 (upwg2d_u) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x1E | skapfad | bin | - | unsigned char | - | 1 | 1 | 0 |
| 0x1F | eagspfad | bin | - | unsigned char | - | 1 | 1 | 0 |
| 0x20 | mpfad | bin | - | unsigned char | - | 1 | 1 | 0 |
| 0x21 | Istmoment bei M.-vergleich (mi_duf) | % | - | unsigned char | - | 0.3906 | 1 | 0 |
| 0x22 | rstpfad | bin | - | unsigned char | - | 1 | 1 | 0 |
| 0x23 | normierter Fahrpedalwinkel (wped) | % | - | unsigned char | - | 0.3922 | 1 | 0 |
| 0x24 | Umgebungstemperatur (tumg) | Grd C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0x25 | Motortemp.-Ersatzwert aus Modell (tmew) | Grd C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0x26 | Spannung DK-Poti1 (udkp1_u) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x27 | Spannung DK-Poti2 (udkp2_u) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x28 | Sollwert DK bez. auf unteren Anschl.(wdks) | % | - | unsigned char | - | 0.3906 | 1 | 0 |
| 0x29 | Abgastemp. v. Kat aus Modell (tabgm) | Grd C | - | unsigned char | - | 5 | 1 | -50 |
| 0x2A | Abgastemp. v. Kat aus Modell Bank2(tabgm2) | Grd C | - | unsigned char | - | 5 | 1 | -50 |
| 0x2B | Kat-Temperatur aus Modell (tkatm) | Grd C | - | unsigned char | - | 5 | 1 | -50 |
| 0x2C | Kat-Temperatur aus Modell Bank2(tkatm2) | Grd C | - | unsigned char | - | 5 | 1 | -50 |
| 0x2D | Spannung LS-Heizung v. Kat (uhsv) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x2E | Spannung LS-Heizung v. Kat Bank2 (uhsv2) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x2F | Spannung LS-Heizung h. Kat (uhsh) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x30 | Spannung LS-Heizung h. Kat Bank2 (uhsh2) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x31 | Innenwiderstand LS v. Kat (rinv) | Ohm | - | unsigned char | - | 64 | 1 | 0 |
| 0x32 | Innenwiderstand LS v. Kat Bank2 (rinv2) | Ohm | - | unsigned char | - | 64 | 1 | 0 |
| 0x33 | Innenwiderstand LS h. Kat (rinh) | Ohm | - | unsigned char | - | 64 | 1 | 0 |
| 0x34 | Innenwiderstand LS h. Kat Bank2 (rinh2) | Ohm | - | unsigned char | - | 64 | 1 | 0 |
| 0x35 | Umgebungdruck (pu) | hPa | - | unsigned char | - | 5 | 1 | 0 |
| 0x36 | gef Periodendauer LS v. Kat (tpsvkmf) | s | - | unsigned char | - | 0.04 | 1 | 0 |
| 0x37 | gef Periodendauer LS v. Kat B2 (tpsvkmf2) | s | - | unsigned char | - | 0.04 | 1 | 0 |
| 0x38 | fr | - | - | unsigned char | - | 0.0078 | 1 | 0 |
| 0x39 | fra | - | - | unsigned char | - | 0.0078 | 1 | 0 |
| 0x3A | fr2 | - | - | unsigned char | - | 0.0078 | 1 | 0 |
| 0x3B | fra2 | - | - | unsigned char | - | 0.0078 | 1 | 0 |
| 0x3C | Tankfuellstand (tfst) | l | - | unsigned char | - | 1 | 1 | 0 |
| 0x3D | rl | % | - | unsigned char | - | 0.75 | 1 | 0 |
| 0x3E | Motortemperatur linear. (tmotlin) | Grad C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0x3F | Motortemp. Referenz aus Modell (tmrm) | Grad C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0x40 | Ist-Moment der Fkt-ueberwachung (mi-um) | % | - | unsigned char | - | 0.3906 | 1 | 0 |
| 0x41 | Ist-Gang (gangi) | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x42 | zul. ind. Moment vor Filter (mizuvfil) | % | - | unsigned char | - | 0.3906 | 1 | 0 |
| 0x43 | ind. Sollmoment vor Begrenzung (mizsolv) | % | - | unsigned char | - | 0.3906 | 1 | 0 |
| 0x44 | eisyevfkaf (Massenstromregler-Faktor) | % | - | unsigned char | - | 0.0078125 | 1 | 0 |
| 0x45 | eisyevkoff (Massenstromregler-Offset) | % | - | unsigned char | - | 8 | 1 | 0 |
| 0x46 | eisydkfkaf (Druckregler-Faktor) | % | - | unsigned char | - | 0.0078125 | 1 | 0 |
| 0x47 | eisydkkoff (Druckregler-Offset) | % | - | unsigned char | - | 8 | 1 | 0 |
| 0x48 | statsvreg1 | % | - | unsigned char | - | 1 | 1 | 0 |
| 0x49 | statsvreg2 | % | - | unsigned char | - | 1 | 1 | 0 |
| 0x4A | t2hstshort | min | - | unsigned char | - | 14.9333333 | 1 | 0 |
| 0x4B | t3hstshort | min | - | unsigned char | - | 14.9333333 | 1 | 0 |
| 0x4C | t4hstshort | min | - | unsigned char | - | 14.9333333 | 1 | 0 |
| 0x4D | dfsiggen | % | - | unsigned char | - | 0.390625 | 1 | 0 |
| 0x4E | ufgen | % | - | unsigned char | - | 0.1 | 1 | 10.6 |
| 0x64 | Winkel DK in Notluftpunkt (wdknlp) | % | - | unsigned char | - | 0.3922 | 1 | 0 |
| 0x65 | Spannung Dk-Poti1 unt. Anschlag (udkp1a_u) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x66 | Integratorgradient Offset KR (igokr_u) | V/s | - | signed char | - | 23.844 | 1 | 0 |
| 0x67 | ADC-Spannung LS v. Kat (uusvk_u) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x68 | ADC-Spannung LS v. Kat Bank2 (uusvk2_u) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x69 | ADC-Spannung LS h. Kat (uushk_u) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x6A | ADC-Spannung LS h. Kat Bank2 (uushk2_u) | V | - | unsigned char | - | 0.0195 | 1 | 0 |
| 0x6B | Tastverhaelnis E-Luefter (taml) | % | - | unsigned char | - | 0.3922 | 1 | 0 |
| 0x6C | Istwinkel für Nockenwelle 1(wnwi1_u) | Grad KW | - | signed char | - | 1 | 1 | 0 |
| 0x6D | Istwinkel für Nockenwelle 2 (wnwi2_u) | Grad KW | - | signed char | - | 1 | 1 | 0 |
| 0x6E | adapt. Haltetastung NW (tanwrhf_0) | % TV | - | unsigned char | - | 0.3922 | 1 | 0 |
| 0x6F | adapt. Haltetastung NW Bank2 (tanwrhf_1) | % TV | - | unsigned char | - | 0.3922 | 1 | 0 |
| 0x70 | vfzg2 | km/h | - | unsigned char | - | 1.25 | 1 | 0 |
| 0x71 | ADC HFM (adhfm) | V | - | unsigned char | - | 0.0196 | 1 | 0 |
| 0x72 | ADC TM  (adtm) | V | - | unsigned char | - | 0.0196 | 1 | 0 |
| 0x73 | ADC TA  (adta) | V | - | unsigned char | - | 0.0196 | 1 | 0 |
| 0x74 | ADC TKA (adtka) | V | - | unsigned char | - | 0.0196 | 1 | 0 |
| 0x75 | ADC DSU (addsu) | V | - | unsigned char | - | 0.0196 | 1 | 0 |
| 0x76 | Sollwert DK in NLP-Stellung (wdknlpr) | % DK | - | unsigned char | - | 0.3921 | 1 | 0 |
| 0x77 | Integratorw. KR Testimpuls (ikrmet) | V | - | unsigned char | - | 0.0196 | 1 | 0 |
| 0x78 | gef. Kat-Temperatur aus Modell (tkatmf) | Grad C | - | unsigned char | - | 5 | 1 | -50 |
| 0x79 | gef. Kat-Temperatur aus Modell B2(tkatmf2) | Grad C | - | unsigned char | - | 5 | 1 | -50 |
| 0x7A | gef. Abgastemperatur aus Modell (tabgmf) | Grad C | - | unsigned char | - | 5 | 1 | -50 |
| 0x7B | gef Abgastemperatur aus Modell B2(tabgmf2) | Grad C | - | unsigned char | - | 5 | 1 | -50 |
| 0x7C | phlsnv | - | - | unsigned char | - | 0.01 | 1 | 0 |
| 0x7D | phlsnv2 | - | - | unsigned char | - | 0.01 | 1 | 0 |
| 0x7E | norm. Heizleistung LS h. Kat (phlsnh) | - | - | unsigned char | - | 0.01 | 1 | 0 |
| 0x7F | norm. Heizleistung LS h. Kat B2 (phlsnh2) | - | - | unsigned char | - | 0.01 | 1 | 0 |
| 0x80 | Integratorgradient Nulltest KR (igod) | V/s | - | signed char | - | 23.844 | 1 | 0 |
| 0x81 | Integratorwert KR Messanfang (ikrma) | V | - | unsigned char | - | 0.0196 | 1 | 0 |
| 0x82 | Lambda-Sollwert (lamsons) | - | - | unsigned char | - | 0.0625 | 1 | 0 |
| 0x83 | Lambda-Sollwert Bank2 (lamsons2) | - | - | unsigned char | - | 0.0625 | 1 | 0 |
| 0x84 | Motorstarttemperatur (tmst) | Grd C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0x85 | Mittelwert Lambdaregelfaktor (frm) | - | - | unsigned char | - | 0.0078 | 1 | 0 |
| 0x86 | Mittelwert Lambdaregelfaktor Bank2 (frm2) | - | - | unsigned char | - | 0.0078 | 1 | 0 |
| 0x87 | Mittelwert Sonde h. Kat (ahkat) | - | - | unsigned char | - | 0.0039 | 1 | 0 |
| 0x88 | Mittelwert Sonde h. Kat Bank2(ahkat2) | - | - | unsigned char | - | 0.0039 | 1 | 0 |
| 0x89 | I-Anteil verz. Reglerumsch.(tvlrhi) | s | - | unsigned char | - | 0.01 | 1 | 0 |
| 0x8A | I-Anteil verz. Reglerumsch.(tvlrhi2) | s | - | unsigned char | - | 0.01 | 1 | 0 |
| 0x8B | Fakt. Luftdichte TANS Hoehe (frhol_u) | - | - | unsigned char | - | 0.0078 | 1 | 0 |
| 0x8C | Zeit nach Start (tnse_u) | s | - | unsigned char | - | 25.6 | 1 | 0 |
| 0x8D | norm. Referenzpegel KR SW-Zyl0 (rkrn_u_0) | V | - | unsigned char | - | 0.625 | 1 | 0 |
| 0x8E | norm. Referenzpegel KR SW-Zyl1 (rkrn_u_1) | V | - | unsigned char | - | 0.625 | 1 | 0 |
| 0x8F | norm. Referenzpegel KR SW-Zyl2 (rkrn_u_2) | V | - | unsigned char | - | 0.625 | 1 | 0 |
| 0x90 | norm. Referenzpegel KR SW-Zyl3 (rkrn_u_3) | V | - | unsigned char | - | 0.625 | 1 | 0 |
| 0x91 | norm. Referenzpegel KR SW-Zyl4 (rkrn_u_4) | V | - | unsigned char | - | 0.625 | 1 | 0 |
| 0x92 | norm. Referenzpegel KR SW-Zyl5 (rkrn_u_5) | V | - | unsigned char | - | 0.625 | 1 | 0 |
| 0x93 | norm. Referenzpegel KR SW-Zyl6 (rkrn_u_6) | V | - | unsigned char | - | 0.625 | 1 | 0 |
| 0x94 | norm. Referenzpegel KR SW-Zyl7 (rkrn_u_7) | V | - | unsigned char | - | 0.625 | 1 | 0 |
| 0x95 | Statusflag ti-Abschaltung (flgtiab) | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x96 | Fuellstand Kraftstofftank (fstt) | l | - | unsigned char | - | 1 | 1 | 0 |
| 0x97 | Pumpenstrom Referenzleck (iptref) | mA | - | unsigned char | - | 0.1953 | 1 | 0 |
| 0x98 | aktuelle Zeit Leckmessung (tdmlka) | s | - | unsigned char | - | 1.6 | 1 | 0 |
| 0x99 | Pumpenstrom DM-TL Ventilpruefung (iptumv) | mA | - | unsigned char | - | 0.1953 | 1 | 0 |
| 0x9A | Differenz Pumpenstrom (iptgh) | mA | - | unsigned char | - | 0.1953 | 1 | 0 |
| 0x9D | I-Anteil der stetigen LRHK (dlahi_u) | - | - | signed char | - | 0.000488 | 1 | 0 |
| 0x9E | I-Anteil der stetigen LRHK Bank2(dlahi2_u) | - | - | signed char | - | 0.000488 | 1 | 0 |
| 0x9F | Korrekturfak. LSU-Spannung (kusvk_u) | V | - | signed char | - | 0.004883 | 1 | 0 |
| 0xA0 | Korrekturfak. LSU-Spannung Bank2(kusvk2_u) | V | - | signed char | - | 0.004883 | 1 | 0 |
| 0xA1 | StatusByte LSU unplausibel (lsunpstat) | bin | - | unsigned char | - | 1 | 1 | 0 |
| 0xA2 | StatusByte LSU unplausibel B2(lsunpstat2) | bin | - | unsigned char | - | 1 | 1 | 0 |
| 0xA3 | Abgasmassenfluss gefiltert (msabg) | kg/h | - | unsigned char | - | 4 | 1 | 0 |
| 0xA4 | Abgasmassenfluss gefiltert Bank2(msabg2) | kg/h | - | unsigned char | - | 4 | 1 | 0 |
| 0xA5 | Abstellzeit (tabst_u) | s | - | unsigned char | - | 256 | 1 | 0 |
| 0xA6 | LSU-Spannung vKat korr. (usvkk_u) | V | - | unsigned char | - | 0.01953 | 1 | 0 |
| 0xA7 | LSU-Spannung vKat korr. Bank2(usvkk2_u) | V | - | unsigned char | - | 0.01953 | 1 | 0 |
| 0xA8 | LSU-Spannung vKat (ADC) (uulsuv_u) | V | - | unsigned char | - | 0.01953 | 1 | 0 |
| 0xA9 | LSU-Spannung vKat Bank2 (ADC)(uulsuv2_u) | V | - | unsigned char | - | 0.01953 | 1 | 0 |
| 0xAA | Dynamikwert LSU-Sonde (dynlsu_u) | - | - | unsigned char | - | 0.015625 | 1 | 0 |
| 0xAB | Dynamikwert LSU-Sonde Bank2(dynlsu2_u) | - | - | unsigned char | - | 0.015625 | 1 | 0 |
| 0xAC | mult. Gemischadapt.fakt. unt.Ber.(frau_u) | - | - | unsigned char | - | 0.0078125 | 1 | 0 |
| 0xAD | mult. Gemischadapt.fakt. u.Ber. B2(frau2_u) | - | - | unsigned char | - | 0.0078125 | 1 | 0 |
| 0xAE | Regelabweichung Lambda (ladiff_u) | - | - | signed char | - | 0.00195 | 1 | 0 |
| 0xAF | Regelabweichung Lambda Bank2(ladiff2_u) | - | - | signed char | - | 0.00195 | 1 | 0 |
| 0xB0 | Lambdaamplitude nach Filterung (lamsam_u) | - | - | signed char | - | 0.00195 | 1 | 0 |
| 0xB1 | Lambdaamplitude n. Filter. Bank2(lamsam2_u) | - | - | signed char | - | 0.00195 | 1 | 0 |
| 0xB2 | Lambda-Istwert vKat (lamsoni_u) | - | - | unsigned char | - | 0.0625 | 1 | 0 |
| 0xB3 | Lambda-Istwert vKat Bank2(lamsoni2_u) | - | - | unsigned char | - | 0.0625 | 1 | 0 |
| 0xB4 | Absolutdruck Abgassystem (palsu_u) | hPa | - | unsigned char | - | 10 | 1 | 0 |
| 0xB5 | Absolutdruck Abgassystem Bank2(palsu2_u) | hPa | - | unsigned char | - | 10 | 1 | 0 |
| 0xB6 | gefilt. Abgastemperatur aus Modell (talsuf) | Grd C | - | unsigned char | - | 5 | 1 | -50 |
| 0xB7 | gef. Abgastemperatur aus Modell B2(talsuf2) | Grd C | - | unsigned char | - | 5 | 1 | -50 |
| 0xB8 | gef. LSU-Spannung vKat (uulsuf_u) | V | - | unsigned char | - | 0.01953 | 1 | 0 |
| 0xB9 | gef. LSU-Spannung vKat Bank2 (uulsuf2_u) | V | - | unsigned char | - | 0.01953 | 1 | 0 |
| 0xBA | Generatorspannung (ugen) | V | - | unsigned char | - | 0.1 | 1 | 10.6 |
| 0xBB | vom Generator empf. Lastsignal (dffgen) | % | - | unsigned char | - | 0.39215 | 1 | 0 |
| 0xBC | Generatortemperatur (gentemp) | Grd C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0xBD | Beladung des Aktivkohlefilters (ftead_u) | - | - | signed char | - | 0.5 | 1 | 0 |
| 0xBE | Betriebsstundenzaehler (top_u) | - | - | unsigned char | - | 1536 | 1 | 0 |
| 0xBF | Abgastemperatur Kat. aus Modell (tikatm) | Grd C | - | unsigned char | - | 5 | 1 | -50 |
| 0xC0 | Abgastemperatur Kat. aus Modell B2(tikatm2) | Grd C | - | unsigned char | - | 5 | 1 | -50 |
| 0xC1 | Lambdasondenistwert korr.(lamzak) | - | - | unsigned char | - | 0.0625 | 1 | 0 |
| 0xC2 | Lambdasondenistwert korr. Bank2(lamzak2) | - | - | unsigned char | - | 0.0625 | 1 | 0 |
| 0xC3 | VVT-Sollwert (vvt_sw) | % | - | unsigned char | - | 0.390625 | 1 | 0 |
| 0xC4 | VVT-Sollwert Bank2(vvt_sw2) | % | - | unsigned char | - | 0.390625 | 1 | 0 |
| 0xC5 | VVT-Istwert (vvt_iw) | % | - | unsigned char | - | 0.390625 | 1 | 0 |
| 0xC6 | VVT-Istwert Bank2(vvt_iw2) | % | - | unsigned char | - | 0.390625 | 1 | 0 |
| 0xC7 | Betriebsartenbyte VVT(B_fe) | bin | - | unsigned char | - | 1.0 | 1 | 0 |
| 0xC8 | Zähler v. Deltas RAM-Backup(dnvrbupctr) | - | - | unsigned char | - | 1.0 | 1 | 0 |
| 0xC9 | Fehlerstatus SSG-Diagnose (stssgerr) | - | - | unsigned char | - | 1.0 | 1 | 0 |
| 0xCA | Korrekturfaktor Höhe (fho_u) | - | - | unsigned char | - | 0.015625 | 1 | 0 |
| 0xCB | Fahrzeuggeschwindigkeit v1 CAN (vfzgv1_u) | - | - | unsigned char | - | 1.0 | 1 | 0 |
| 0xCC | Mittelwert Lambdaregelfaktor gefreezt (frm) | - | - | unsigned char | - | 0.0078 | 1 | 0 |
| 0xCD | Lambda-Sollwert gefreezt (lamsons) | - | - | unsigned char | - | 0.0625 | 1 | 0 |
| 0xCE | Korrekturfaktor Höhe gefreezt (fho_u) | - | - | unsigned char | - | 0.015625 | 1 | 0 |
| 0xCF | Motorstarttemperatur gefreezt (tmst) | Grd C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0xD0 | Mittelwert Lambdaregelfaktor gefreezt B2(frm2) | - | - | unsigned char | - | 0.0078 | 1 | 0 |
| 0xD1 | Lambda-Sollwert gefreezt Bank2 (lamsons2) | - | - | unsigned char | - | 0.0625 | 1 | 0 |
| 0xD2 | Korrekturfaktor Höhe gefreezt B2(fho_u) | - | - | unsigned char | - | 0.015625 | 1 | 0 |
| 0xD3 | Motorstarttemperatur gefreezt (tmst) | Grd C | - | unsigned char | - | 0.75 | 1 | -48 |
| 0xD4 | intelligenter Batteriesensor Fehler 1 (ibsderrs1) |   | - | unsigned char | - | 1 | 1 | 0 |
| 0xD5 | intelligenter Batteriesensor Fehler 2 (ibsders2_u) |   | - | unsigned char | - | 1 | 1 | 0 |
| 0xD6 | Referenzmoment fuer Aussetzererkennung | % | - | unsigned char | - | 0.390625 | 1 | 0 |
| 0xD9 | relative Kraftstoffmasse | % | - | unsigned char | - | 3 | 1 | 0 |
| 0xDD | Abstand zur Startfaehigeitsgrenze(d_soc_u) | % | - | unsigned char | - | 1.0240020752 | 1 | -100 |
| 0xDE | Korrekturwert Abschaltung(abschkor_u) | % | - | unsigned char | - | 1.0240020752 | 1 | -100 |
| 0xDF | aktuelle Batteriespannung (ubatt_u) | V | - | unsigned char | - | 0.064 | 1 | 6 |
| 0xE0 | aktuelles Oelniveau korrigiert |   | - | unsigned char | - | 0.5 | 1 | 0 |
| 0xE1 | relativer Fuellstand des Motoroels |   | - | unsigned char | - | 1 | 1 | 0 |
| 0xE2 | Bordnetzstromentnahme VVT (ivvtbn_u) | A | - | signed char | - | 1.5625 | 1 | 0 |
| 0xE3 | Motorstrom VVT (ivvtm_u) | A | - | signed char | - | 1.5625 | 1 | 0 |
| 0xE4 | Tastverhaeltnis VVT- Motoransteuerung (tvvvtm_u) | % | - | signed char | - | 0.78125 | 1 | 0 |
| 0xE5 | Abstellposition VVT- Führungssensor | ° | - | unsigned char | - | 0.703125 | 1 | 0 |
| 0xE6 | Feststellbereich Fuehrungssensor (exwnkfvb_u) | ° | - | unsigned char | - | 0.703125 | 1 | 0 |
| 0xE7 | Feststellbereich Referenzsensor | ° | - | unsigned char | - | 0.703125 | 1 | 0 |
| 0xE8 | VVT- Fuehrungssensor Rohwert (exwnkfsr_u) | ° | - | unsigned char | - | 0.703125 | 1 | 0 |
| 0xE9 | VVT- Referenzsensor Rohwert (exwnkrsr_u) | ° | - | unsigned char | - | 0.703125 | 1 | 0 |
| 0xEA | Differenz Führungs- zu Referenzsensor (dwvvtfrs_u) | ° | - | unsigned char | - | 0.703125 | 1 | 0 |
| 0xEB | Istwert Exzenterwinkel VVT (exwnki_u) | Grad | - | unsigned char | - | 0.8 | 1 | 0 |
| 0xEC | Sollwert Exzenterwinkel VVT(exwinks_u) | Grad | - | unsigned char | - | 0.8 | 1 | 0 |
| 0xED | Statusbit VVT- Lageregler |   | - | unsigned char | - | 1 | 1 | 0 |
| 0xEE | Spannung Diagnose-Port VVT- Ansteuerung (uvvtdia) | V | - | unsigned char | - | 0.01953125 | 1 | 0 |
| 0xEF | ADC- Wert VVT- Sensorversorgungsspannung (wvvtusen) | V | - | unsigned char | - | 0.01953125 | 1 | 0 |
| 0xF0 | Status VVT- Anschlaglernen (intern)(vvtlrnst) |   | - | unsigned char | - | 1 | 1 | 0 |
| 0xF1 | Anforderung VVT- Anschlaglernen (intern)(vvtlrnaf) |   | - | unsigned char | - | 1 | 1 | 0 |
| 0xF2 | Temperatur VVT- Endstufe (tvvtes_u) | Grad C | - | unsigned char | - | 1 | 1 | 0 |
| 0xF3 | Temperatur VVT- Stellmotor (tvvtm_u) | Grad C | - | unsigned char | - | 1 | 1 | 0 |
| 0xF4 | Statusbit VVT- Lagereglerueberwachung |   | - | unsigned char | - | 1 | 1 | 0 |
| 0xF5 | Spannung VVT- Relais (uvvtr_u) | V | - | unsigned char | - | 0.078125 | 1 | 0 |
| 0xF6 | Status Fehler Ueberlast VVT1 (stdvovrld) |   | - | unsigned char | - | 1 | 1 | 0 |
| 0xF7 | Byteorientierte Ablage fuer B_vvt im FF- Array (bitcnv_vvt) |   | - | unsigned char | - | 1 | 1 | 0 |
| 0xF8 | Erregerstrom Generator (ierr) | A | - | unsigned char | - | 0.125 | 1 | 0 |
| 0xFF | --- | - | - | unsigned char | - | 1 | 1 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 207 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x29CC | 0x8B | 0xFF | 0x8C | 0x8A |
| 0x29CD | 0x8B | 0xFF | 0x8C | 0x8A |
| 0x29CE | 0x8B | 0xFF | 0x8C | 0x8A |
| 0x29CF | 0x8B | 0xFF | 0x8C | 0x8A |
| 0x29D0 | 0x8B | 0xFF | 0x8C | 0x8A |
| 0x29D9 | 0xFF | 0xFF | 0xFC | 0xFF |
| 0x29DD | 0xFF | 0xF4 | 0xFF | 0xF3 |
| 0x29E5 | 0xFF | 0xFF | 0x96 | 0x97 |
| 0x29E6 | 0xFF | 0xFF | 0x96 | 0x97 |
| 0x29E7 | 0xFF | 0xFF | 0x96 | 0x97 |
| 0x29E8 | 0xFF | 0xFF | 0x96 | 0x97 |
| 0x29E9 | 0xFF | 0xFF | 0x96 | 0x97 |
| 0x29EA | 0xFF | 0xFF | 0x96 | 0x97 |
| 0x29EB | 0x04 | 0xFF | 0x97 | 0x96 |
| 0x29EC | 0x04 | 0xFF | 0x97 | 0x96 |
| 0x29ED | 0xFF | 0xFF | 0x96 | 0x97 |
| 0x29EE | 0xFF | 0xFF | 0x96 | 0x97 |
| 0x29F4 | 0xFF | 0xFF | 0x7D | 0xFF |
| 0x29F5 | 0xFF | 0xFF | 0x7D | 0xFF |
| 0x29F8 | 0xFF | 0xFF | 0x7D | 0xFF |
| 0x29F9 | 0xFF | 0xFF | 0x7D | 0xFF |
| 0x29FE | 0xFF | 0xFF | 0x98 | 0xFF |
| 0x29FF | 0xFF | 0xFF | 0x98 | 0xFF |
| 0x2A02 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2A03 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2A0E | 0x04 | 0x22 | 0x07 | 0x08 |
| 0x2A14 | 0x04 | 0x03 | 0x29 | 0x28 |
| 0x2A17 | 0x3E | 0x3D | 0x3C | 0x3B |
| 0x2A19 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2A1A | 0xFF | 0xFF | 0xA1 | 0xFF |
| 0x2A1D | 0x04 | 0x22 | 0x07 | 0x08 |
| 0x2A1E | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x2A58 | 0x04 | 0x22 | 0x07 | 0x08 |
| 0x2A59 | 0x43 | 0x42 | 0x41 | 0x40 |
| 0x2A5B | 0x43 | 0x42 | 0x41 | 0x40 |
| 0x2A5D | 0x44 | 0xFF | 0xFF | 0xFF |
| 0x2A5F | 0xFF | 0xFF | 0x46 | 0x47 |
| 0x2A61 | 0x53 | 0xF8 | 0x54 | 0x55 |
| 0x2A63 | 0x56 | 0x57 | 0xFF | 0xFF |
| 0x2A67 | 0x4F | 0x4E | 0x07 | 0x08 |
| 0x2A69 | 0x52 | 0xFF | 0x51 | 0x50 |
| 0x2A6B | 0xFF | 0x3C | 0x6A | 0xFF |
| 0x2A6C | 0xFF | 0xFF | 0xFF | 0x59 |
| 0x2A6D | 0xFF | 0xFF | 0xBE | 0xBD |
| 0x2A6F | 0xFF | 0xFF | 0xFF | 0x3A |
| 0x2A70 | 0xEA | 0xFF | 0xFF | 0xFF |
| 0x2A71 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2A72 | 0x57 | 0xFF | 0xFF | 0xFF |
| 0x2A80 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2A83 | 0x71 | 0xFF | 0x72 | 0xFF |
| 0x2A85 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2A88 | 0x71 | 0xFF | 0x72 | 0xFF |
| 0x2B5C | 0x69 | 0x6B | 0xFF | 0xFF |
| 0x2B5D | 0x2D | 0x29 | 0xFF | 0x28 |
| 0x2B62 | 0x92 | 0x93 | 0x07 | 0x08 |
| 0x2B63 | 0x92 | 0x93 | 0x07 | 0x08 |
| 0x2B66 | 0xFF | 0x94 | 0xFF | 0xFF |
| 0x2B70 | 0x9B | 0xFF | 0xFF | 0xFF |
| 0x2B80 | 0xFF | 0xFF | 0x87 | 0x86 |
| 0x2B8A | 0x7E | 0xFF | 0xFF | 0xFF |
| 0x2B8B | 0x7E | 0xFF | 0xFF | 0xFF |
| 0x2B8C | 0x7E | 0xFF | 0xFF | 0xFF |
| 0x2B98 | 0xC1 | 0xFF | 0xFF | 0xFF |
| 0x2B99 | 0xFF | 0xFF | 0x8E | 0x8F |
| 0x2B9A | 0xB1 | 0xFF | 0xFF | 0xFF |
| 0x2B9B | 0xB2 | 0xFF | 0xFF | 0xFF |
| 0x2B9C | 0xB3 | 0xBA | 0xAF | 0xFF |
| 0x2B9D | 0xFF | 0xED | 0xEC | 0xEB |
| 0x2BA7 | 0xFF | 0xFF | 0xFF | 0x8D |
| 0x2BB6 | 0x52 | 0xFF | 0x51 | 0x50 |
| 0x2B9E | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x2C24 | 0x89 | 0xFF | 0xFF | 0xFF |
| 0x2C45 | 0x88 | 0x3B | 0x82 | 0x0B |
| 0x2C46 | 0x88 | 0x3B | 0x82 | 0x0B |
| 0x2C55 | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x2C56 | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x2C6A | 0x89 | 0xFF | 0xFF | 0xFF |
| 0x2C6D | 0x82 | 0x83 | 0x84 | 0x85 |
| 0x2C6E | 0x82 | 0x83 | 0x84 | 0x85 |
| 0x2C6F | 0xFF | 0xFF | 0xFF | 0xC2 |
| 0x2C70 | 0xFF | 0xFF | 0xFF | 0xC2 |
| 0x2C71 | 0x09 | 0x22 | 0x07 | 0x08 |
| 0x2C72 | 0x09 | 0x22 | 0x07 | 0x08 |
| 0x2C9C | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2C9D | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2C9E | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2C9F | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2CA0 | 0x7B | 0xFF | 0xFF | 0xFF |
| 0x2CA1 | 0x7B | 0xFF | 0xFF | 0xFF |
| 0x2CA2 | 0x7C | 0xFF | 0xFF | 0xFF |
| 0x2CA3 | 0x7C | 0xFF | 0xFF | 0xFF |
| 0x2CA8 | 0x7B | 0x22 | 0x07 | 0x08 |
| 0x2CA9 | 0x7B | 0x22 | 0x07 | 0x08 |
| 0x2CEF | 0xF7 | 0x22 | 0x07 | 0x08 |
| 0x2CF0 | 0xFF | 0xFF | 0x61 | 0x62 |
| 0x2CF1 | 0x5F | 0xFF | 0xFF | 0xFF |
| 0x2CF8 | 0x23 | 0xFF | 0xFF | 0xFF |
| 0x2CF9 | 0x26 | 0xFF | 0x25 | 0x24 |
| 0x2CFA | 0x27 | 0xFF | 0x25 | 0x24 |
| 0x2CFF | 0x68 | 0xFF | 0xFF | 0xFF |
| 0x2D00 | 0xFF | 0xFF | 0x5A | 0x5B |
| 0x2D01 | 0xFF | 0xFF | 0x5D | 0x5E |
| 0x2D02 | 0x60 | 0xFF | 0xFF | 0xFF |
| 0x2D03 | 0xFF | 0xFF | 0x65 | 0x66 |
| 0x2D04 | 0x64 | 0xFF | 0xFF | 0xFF |
| 0x2D05 | 0x67 | 0xFF | 0xFF | 0xFF |
| 0x2D08 | 0x63 | 0xFF | 0xFF | 0xFF |
| 0x2D10 | 0xFF | 0xFF | 0x02 | 0x01 |
| 0x2D11 | 0xFF | 0xFF | 0x02 | 0x01 |
| 0x2D12 | 0xFF | 0xFF | 0x02 | 0x01 |
| 0x2D0F | 0xFF | 0xFF | 0x39 | 0x38 |
| 0x2D19 | 0x15 | 0xFF | 0xFF | 0xFF |
| 0x2D1A | 0x74 | 0xFF | 0xFF | 0xFF |
| 0x2D1B | 0x73 | 0xFF | 0x51 | 0x50 |
| 0x2D1C | 0xFF | 0xFF | 0x51 | 0x50 |
| 0x2D28 | 0xFF | 0xFF | 0x39 | 0x38 |
| 0x2D29 | 0xFF | 0xFF | 0x90 | 0x91 |
| 0x2D32 | 0xFF | 0xFF | 0x02 | 0x01 |
| 0x2D6E | 0xA4 | 0xFF | 0xFF | 0xFF |
| 0x2D6F | 0xA6 | 0xA7 | 0xA8 | 0x01 |
| 0x2D70 | 0xFF | 0xAA | 0xAB | 0xAC |
| 0x2D71 | 0xFF | 0xAE | 0xAD | 0xC7 |
| 0x2D72 | 0xE5 | 0xFF | 0xF0 | 0xEF |
| 0x2D73 | 0xE8 | 0xFF | 0xFF | 0xFF |
| 0x2D74 | 0xE9 | 0xFF | 0xFF | 0xFF |
| 0x2D75 | 0xA5 | 0xFF | 0xFF | 0xFF |
| 0x2D76 | 0xB0 | 0xFF | 0xFF | 0xFF |
| 0x2D78 | 0xBB | 0xFF | 0xFF | 0xFF |
| 0x2DB4 | 0x15 | 0xF7 | 0xF6 | 0xF5 |
| 0x2DBF | 0xC9 | 0xC6 | 0xC5 | 0xFF |
| 0x2DCA | 0xC9 | 0xC6 | 0xC5 | 0xFF |
| 0x2DCF | 0xC9 | 0xC6 | 0xC5 | 0xFF |
| 0x2DD7 | 0xC9 | 0xC6 | 0xC5 | 0xFF |
| 0x2DD8 | 0x31 | 0xC6 | 0x32 | 0xFF |
| 0x2DD9 | 0x31 | 0xC6 | 0xC5 | 0xFF |
| 0x2DDA | 0x32 | 0xC6 | 0xFF | 0xFF |
| 0x2DDB | 0xFF | 0xC6 | 0xFF | 0xFF |
| 0x2DDC | 0xC9 | 0xC6 | 0xC5 | 0xFF |
| 0x2DEB | 0xFF | 0xE3 | 0xE1 | 0xE2 |
| 0x2DEC | 0xC8 | 0xFF | 0xCA | 0xFF |
| 0x2DED | 0xE4 | 0xFF | 0xFF | 0xFF |
| 0x2E24 | 0x31 | 0xFF | 0xFF | 0xFF |
| 0x2E25 | 0x31 | 0xFF | 0xFF | 0xFF |
| 0x2E26 | 0x31 | 0xFF | 0xFF | 0xFF |
| 0x2E27 | 0x31 | 0xFF | 0xFF | 0xFF |
| 0x2E30 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2E31 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2E32 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2E33 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2E68 | 0xFF | 0xFF | 0x80 | 0x7F |
| 0x2E69 | 0xFF | 0xFF | 0x80 | 0x7F |
| 0x2E6A | 0x04 | 0x03 | 0x80 | 0x7F |
| 0x2E6B | 0x04 | 0x03 | 0x80 | 0x7F |
| 0x2E7C | 0x0F | 0x10 | 0xFF | 0xFF |
| 0x2E86 | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x2E8B | 0xC3 | 0x12 | 0xFF | 0xC4 |
| 0x2E8C | 0xCF | 0xCE | 0xFF | 0xCC |
| 0x2E8D | 0xF9 | 0xE0 | 0xFF | 0xFA |
| 0x2E95 | 0x0F | 0x10 | 0x02 | 0x01 |
| 0x2E97 | 0x0C | 0x0D | 0x0F | 0x0E |
| 0x2E9F | 0x11 | 0x12 | 0x13 | 0x14 |
| 0x2EA0 | 0xFB | 0x10 | 0x13 | 0x14 |
| 0x2EB8 | 0xFF | 0xC6 | 0xFF | 0xFF |
| 0x2EBC | 0xFF | 0xC6 | 0xFF | 0xFF |
| 0x2EBD | 0xFF | 0xC6 | 0xFF | 0xFF |
| 0x2EBE | 0xFF | 0xC6 | 0xFF | 0xFF |
| 0x2EE0 | 0x9E | 0x9F | 0x9C | 0x07 |
| 0x2EEA | 0xFF | 0xFF | 0x9C | 0x07 |
| 0x2EF4 | 0xFF | 0xFF | 0xA0 | 0xFF |
| 0x2EF5 | 0x15 | 0x22 | 0x07 | 0x08 |
| 0x2EF6 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2EFE | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2F08 | 0xFF | 0xFF | 0x08 | 0x07 |
| 0x2F12 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2F17 | 0xFF | 0xFF | 0xFF | 0x45 |
| 0x2F21 | 0xFF | 0xFF | 0xFF | 0xFF |
| 0x2F44 | 0x1B | 0x1C | 0x1D | 0x1E |
| 0x2F45 | 0x18 | 0x19 | 0x1A | 0xFF |
| 0x2F46 | 0xFF | 0x1F | 0x20 | 0x21 |
| 0x2F4E | 0xFF | 0xB6 | 0xFF | 0xFF |
| 0x2F50 | 0xB4 | 0xFF | 0xFF | 0xB5 |
| 0x2F58 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2F59 | 0xFF | 0x9A | 0xFF | 0xFF |
| 0x2F5A | 0xFF | 0x99 | 0xFF | 0xFF |
| 0x2F62 | 0x2E | 0xFF | 0xFF | 0xFF |
| 0x2F67 | 0xFF | 0x81 | 0xFF | 0xFF |
| 0x2F6C | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2F71 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2F76 | 0x3F | 0xFF | 0x46 | 0x47 |
| 0x2F7B | 0x95 | 0xFF | 0xFF | 0xFF |
| 0x2F80 | 0xE7 | 0xFF | 0xFF | 0xFF |
| 0x2F85 | 0xFF | 0xFF | 0xE6 | 0xBF |
| 0x2F8A | 0x52 | 0xFF | 0x51 | 0x50 |
| 0x2F94 | 0xFF | 0x22 | 0x07 | 0x08 |
| 0x2F99 | 0x77 | 0xA2 | 0xFF | 0xFF |
| 0x2F9E | 0x15 | 0x16 | 0x17 | 0xFF |
| 0x2FA3 | 0x36 | 0xFF | 0xFF | 0xFF |
| 0xCD87 | 0xFF | 0x35 | 0x34 | 0x33 |
| 0xCD8B | 0x35 | 0x22 | 0x34 | 0x33 |
| 0xCD9B | 0x37 | 0x37 | 0xFF | 0xFF |
| 0xCDA1 | 0xFF | 0x37 | 0xFF | 0xFF |
| 0xCDA2 | 0xFF | 0x37 | 0xFF | 0xFF |
| 0xCDA3 | 0xFF | 0x37 | 0xFF | 0xFF |
| 0xCDA7 | 0xFF | 0x37 | 0xFF | 0xFF |
| 0xCDAA | 0xFF | 0x37 | 0xFF | 0xFF |
| 0xCDAC | 0xFF | 0x37 | 0xFF | 0xFF |
| 0xFFFF | 0xFF | 0xFF | 0xFF | 0xFF |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 236 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Signal oder Wert oberhalb Schwelle |
| 0x02 | Signal oder Wert unterhalb Schwelle |
| 0x03 | kein Signal oder Wert |
| 0x04 | unplausibles Signal oder Wert |
| 0x05 | mangelnde Signalbereitschaft |
| 0x06 | Lastabfall |
| 0x07 | Kurzschluss nach Minus |
| 0x08 | Kurzschluss nach Plus |
| 0x09 | Heizereinkopplung Signalpfad |
| 0x0A | geringe Signaldynamik |
| 0x0B | Signal-Offset |
| 0x0C | Fehler mechanisch |
| 0x0D | Fehler elektrisch |
| 0x0E | Uebertemperatur |
| 0x0F | Generatortyp unplausibel |
| 0x10 | Kommunikationsverlust |
| 0x11 | Messfehler Oelzustand |
| 0x12 | BSD Kommunikation |
| 0x13 | Messfehler Oelniveau |
| 0x14 | Messfehler Oeltemperatur |
| 0x15 | Signal unplausibel |
| 0x16 | Signal abgefallen |
| 0x17 | Warnschwelle Oelverlust ausgeloest |
| 0x18 | Empfangsfehler serielle Schnittstelle (Paritybit &gt; 3x) |
| 0x19 | Timeout EWS-Telegramm (kein Telegramm innerhalb 2s nach Kl.15 ein) |
| 0x1A | Empfangsfehler serielle Schnittstelle (Frame- oder Stopbit &gt; 3x) |
| 0x1B | WC passt nicht zum erwarteten WC (Fangbereichsueberschreitung) |
| 0x1C | Fehler beim Programmieren oder Rücksetzen des Startwerts |
| 0x1D | noch kein Startwert programmiert |
| 0x1E | Startwert nicht eindeutig erkennbar (Fehler in 2-aus-3-Auswahl) |
| 0x1F | Schreibfehler EEPROM (3 Fehlversuche beim Schreiben ins EEPROM) |
| 0x20 | WC-Ablage fehlerhaft im EXRAM (z.B. nach Powerfail) |
| 0x21 | Lesefehler EEPROM (3 Fehlversuche beim Lesen aus EEPROM) |
| 0x22 | Leitungsunterbrechung |
| 0x23 | Fehler DK-Poti 1 oder DK-Poti 2 |
| 0x24 | Bereichsverletzung Poti nach oben |
| 0x25 | Bereichsverletzung Poti nach unten |
| 0x26 | Drosselklappenpotentiometer 1 unplausibel zur Luftmasse |
| 0x27 | Drosselklappenpotentiometer 2 unplausibel zur Luftmasse |
| 0x28 | Fehlereintrag durch Lueckenkorrektur |
| 0x29 | keine Bezugsmarke gefunden |
| 0x2A | VANOS hat Spaetposition nicht erreicht |
| 0x2B | VANOS hat Fruehposition nicht erreicht |
| 0x2C | VANOS hat unplausible Position |
| 0x2D | Kurbelwellen-Zahnfehler oder Lueckenverlust |
| 0x2E | Pruefresultat unplausibel |
| 0x2F | Timeout abgelaufen |
| 0x30 | Alive-Fehler |
| 0x31 | Plausibilitaetfehler |
| 0x32 | Checksumme oder Alivefehler |
| 0x33 | Baustein im Zustand Passiv |
| 0x34 | DPRAM von CAN Baustein defekt |
| 0x35 | CAN Baustein Bus off oder Bus defekt |
| 0x36 | DME noch nicht codiert |
| 0x37 | fehlerhafte Botschaft |
| 0x38 | Signal oberhalb Schwelle oder Kurzschluss nach Plus |
| 0x39 | Signal unterhalb Schwelle oder Kurzschluss nach Minus |
| 0x3A | max.Anzahl der MINHUB-Anschläge überschritten |
| 0x3B | Sondendefekt |
| 0x3C | Plausibilisierung Luftmasse zu gering |
| 0x3D | Abbruch wegen Stromschwankungen bei Feinleckpruefung |
| 0x3E | Pumpenstromschwelle bei Ventilpruefung erreicht |
| 0x3F | Sensorwert unplausibel |
| 0x40 | Magnet loss |
| 0x41 | Resetfehler |
| 0x42 | Parityfehler |
| 0x43 | Gradientenfehler |
| 0x44 | Sensoren unplausibel |
| 0x45 | Zwangshochschaltung Getriebe |
| 0x46 | Sensorspannung zu gering |
| 0x47 | Sensorspannung zu hoch |
| 0x48 | Sollwertsbotschaften nicht empfangen |
| 0x49 | VVT-Boschaften nicht empfangen |
| 0x4A | ROM-Test Fehler |
| 0x4B | Stack-Test Fehler |
| 0x4C | RAM-Test Fehler |
| 0x4D | EEPROM-Test Fehler |
| 0x4E | Kurzschluss der Motorleitung |
| 0x4F | Ansteuerungsfehler allgemein |
| 0x50 | Spannung oberhalb Schwelle |
| 0x51 | Spannung unterhalb Schwelle |
| 0x52 | Relaisfehler |
| 0x53 | keine Anschlaege gelernt |
| 0x54 | Fehler unteres Lernfenster |
| 0x55 | Verstellbereich fehlerhaft |
| 0x56 | Drehrichtungserkennung |
| 0x57 | Lagereglerueberwachung |
| 0x58 | Uebertemperatur |
| 0x59 | Vergleich Abstell- zur Startposition fehlerhaft |
| 0x5A | Klappe laesst sich vom UMA nicht oeffnen |
| 0x5B | Feder schliesst nicht |
| 0x5C | DKS Ansteuerungsfehler, Endstufe abgeschaltet |
| 0x5D | Klappe laesst sich vom UMA nicht schliessen |
| 0x5E | Feder oeffnet nicht |
| 0x5F | DKS Lageabweichung |
| 0x60 | Fehler bei NLP-Pruefung und Lernen |
| 0x61 | DKS klemmt kurzzeitig |
| 0x62 | DKS klemmt anhaltend |
| 0x63 | DKS-Tauscherkennung ohne Adaption Notluftpunkt |
| 0x64 | Fehler in Urinitialisierung des unteren mech. Anschlags (UMA) |
| 0x65 | Lernverbot unterer mech. Anschlag (UMA) wegen Unterspannung |
| 0x66 | Lernverbot unterer mech. Anschlag (UMA) wegen Umweltbedinungen |
| 0x67 | Fehler bei Wiederhollernen unterer mech. Anschlag (UMA) |
| 0x68 | Fehler bei Verstaerkerabgleich  |
| 0x69 | gestörtes Drehzahlsignal (länger als 50ms) |
| 0x6A | Ventil öffnet nicht (Winkeldetektion), Vollhub wird nicht erreicht |
| 0x6B | kein Drehzahlsignal gefunden |
| 0x6C | Uebertemperaturabschaltung |
| 0x6D | Kurzschluss nach Minus |
| 0x6E | Kurzschluss nach Plus oder niedere Impedanz  |
| 0x6F | Massenstromadaption zu klein |
| 0x70 | Massenstromadaption zu gross |
| 0x71 | Regelanschlag zu lange zu gross |
| 0x72 | Anschlagadaption ausserhalb gueltigen Bereich |
| 0x73 | Gleichlauffehler zwischen Poti1 und Poti2 |
| 0x74 | Poti1 oder Poti2 fehlerhaft oder ausserhalb der Toleranzen |
| 0x75 | untere Plausibilitaetsschwelle unterschritten |
| 0x76 | obere Plausibilitaetsschwelle ueberschritten |
| 0x77 | Umgebungstemperatur unplausibel |
| 0x78 | CAN-Fehler Tankfuellstand |
| 0x79 | Tankfuellstandssignal Tank2 fehlerhaft |
| 0x7A | Tankfuellstandssignal Tank1 fehlerhaft |
| 0x7B | Sondenheizung defekt (Innenwiderstand) |
| 0x7C | zu geringe Schubsignalspannung |
| 0x7D | Katalysatorwirkungsgrad unter Schwellwert |
| 0x7E | Klopfbaustein defekt |
| 0x7F | Motor mechanisch zu laut oder Klopfsensor ausserhalb Toleranz |
| 0x80 | elektrischer Fehler Klopfsensor (Wackelkontakt o. Klopfsensor locker) |
| 0x81 | Signal inaktiv |
| 0x82 | Sonde dynamisch zu langsam |
| 0x83 | Sondenspannung im Schub Schwelle nicht unterschritten |
| 0x84 | Sondenspannung unterschreitet Schwellwert nicht |
| 0x85 | Sondenspannung ueberschreitet Schwellwert nicht |
| 0x86 | LL-Steller Oeffnung zu gross oder Leckluft |
| 0x87 | LL-Steller Oeffnung zu gering |
| 0x88 | Adernschluss oder vergiftete Referenzluft (CSD) |
| 0x89 | vertauschte Lambdasonden |
| 0x8A | Verbrennungsaussetzer mit Zylinderabschaltung |
| 0x8B | Verbrennungsaussetzer im Warmlauf, emissionsverschlechternd |
| 0x8C | Verbrennungsaussetzer betriebswarm, emissionsverschlechternd |
| 0x8D | Drehmomentbegrenzung, Sollmoment liegt über zulässigem Moment |
| 0x8E | Schreibfehler |
| 0x8F | Lesefehler |
| 0x90 | Differenzdruck zu klein |
| 0x91 | Differenzdruck zu gross |
| 0x92 | unplausible Phasenflankenanzahl |
| 0x93 | Lage der Phasenflanken oder Einbaulage ausserhalb Toleranz |
| 0x94 | keine Masternockenwelle vorhanden |
| 0x95 | Schalter unplausibel |
| 0x96 | Gemisch zu fett |
| 0x97 | Gemisch zu mager |
| 0x98 | Sekundaerluftdurchsatz zu gering |
| 0x99 | Drehzahlimpulse innerhalb des Messfensters erkannt |
| 0x9A | Start in laufendem Motor |
| 0x9B | Fehler Ansteuerung DISA (Kurzschluesse nach Plus oder Minus) |
| 0x9C | Kurzschluss nach Plus oder Leitungsunterbrechung |
| 0x9D | Kurzschluss nach Minus |
| 0x9E | Kuehlwassertemperatur unplausibel gegenueber Modell |
| 0x9F | Kuehlwassertemperatur fuer Lambdaregelungsfreigabe nicht erreicht |
| 0xA0 | Thermostat klemmt |
| 0xA1 | Funktionstest Tankentlueftung fehlerhaft |
| 0xA2 | Umgebungstemperatur vom Kombi fehlerhaft |
| 0xA3 | ADC Fehler |
| 0xA4 | Funktionsueberwachung Momentenvergleich |
| 0xA5 | Kurbelwellengeber-, Zuleitungs- oder Steuergeraetefehler |
| 0xA6 | Lastsensor-, Zuleitungs- oder Steuergeraetefehler |
| 0xA7 | VVT-Ventilplausibilisierung |
| 0xA8 | Drucksensorplausibilisierung |
| 0xA9 | Reaktionsueberwachung |
| 0xAA | ADC-Ueberwachung |
| 0xAB | Zuendwinkelueberwachung |
| 0xAC | RL-Ueberwachung |
| 0xAD | Plausibilisierung rk-ti |
| 0xAE | Variantencodierungsueberwachung |
| 0xAF | Reset TPU-RAM |
| 0xB0 | Pedalwertgeber-, Zuleitungs- oder Steuergeraetefehler |
| 0xB1 | RAM-Fehler |
| 0xB2 | ROM-Fehler |
| 0xB3 | Reset-Fehler |
| 0xB4 | Geschwindigkeitssignal vom Kombi und DSC nicht kompatibel |
| 0xB5 | Geschwindigkeitssignal vom Kombi fehlerhaft |
| 0xB6 | fehlendes Geschwindigkeitssignal (Hardwaresignal) |
| 0xB7 | Hochimpedanz |
| 0xB8 | Lagerreglerabweichung zu gross |
| 0xB9 | Uebertemperatur DISA-Stellmotor |
| 0xBA | Reset TPU-CPU |
| 0xBB | Ueberwachung Luftmassenstromabgleich |
| 0xBC | zu starke Erwaermung des Steller |
| 0xBD | Temperatur VVT-Endstufe zu hoch |
| 0xBE | Temperatur E-Motor zu hoch |
| 0xBF | Steuergeraeteinnentemperatur zu hoch |
| 0xC0 | Ueberlastschutz VVT-System |
| 0xC1 | Aktualitaetszaehler zwischen EEPROM und RAM-Backup unterschiedlich |
| 0xC2 | Signal bei Vollast unterhalb Fettschwelle |
| 0xC3 | Version unplausibel |
| 0xC4 | Erweiterte BSD Kommunikation |
| 0xC5 | Alivefehler |
| 0xC6 | Timeout |
| 0xC7 | Überwachung Kraftstoffkorektur |
| 0xC8 | Powermanagement defekt |
| 0xC9 | Checksumme |
| 0xCA | Tiefenentladung |
| 0xCB | Strom Temperatur |
| 0xCC | Temperatur |
| 0xCE | Spannung |
| 0xCF | Strom |
| 0xE0 | System |
| 0xE1 | Unterspannung |
| 0xE2 | Ueberspannung |
| 0xE3 | batterieloser Betrieb |
| 0xE4 | Ruhestrom |
| 0xE5 | Lambdatest |
| 0xE6 | Steuergeraeteinnentemperatur zu niedrig |
| 0xE7 | CAN rel. Zeitgeber unplausibel |
| 0xE8 | Kraftstoffdrucktest |
| 0xE9 | Lambda-Plausibilisierung |
| 0xEA | gemessener Strom VVT unplausibel |
| 0xEB | Ueberspannung auf VCC |
| 0xEC | WDA-Abschaltung erkannt (unbekannte Fehlerursache) |
| 0xED | fehlerhafte/fehlende F/A- Kommunikation |
| 0xEF | ADC-Queue Überwachung |
| 0xF0 | ADC-Testspannung außerhalb zulässigem Bereich |
| 0xF1 | Sondensignal zu traege |
| 0xF2 | Schaltzeiten Fett- Mager zu langsam |
| 0xF3 | Radgeschwindigkeit zu hoch |
| 0xF4 | kein Raddrehzahlsignal erhalten |
| 0xF5 | Toggle-Bit Fehler |
| 0xF6 | Frequenzfehler |
| 0xF7 | Signalfehler |
| 0xF8 | Speicherung Lernwerte in EEPROM nicht möglich |
| 0xF9 | KL15- Wakeupleitung unplausibel |
| 0xFA | KL15- Wakeupleitung Masseschluss |
| 0xFB | Permitivitätsmessung fehlerhaft |
| 0xFC | Tankfüllstand zu gering |
| 0xFF | unbekannte Fehlerart |

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

<a id="table-betriebswtab"></a>
### BETRIEBSWTAB

Dimensions: 222 rows × 13 columns

| NAME | TELEGRAM | POS_ADR | LEN_ADR | ADR | BYTE | DATA_TYPE | COMPU_TYPE | FACT_A | FACT_B | MASK | VALUE | MEAS |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TE_W | 8312F1224000 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.008 | 0 | 0 | 0 | ms |
| FR_W | 8312F1224000 | 0 | 0 | 0x00 | 5 | 5 | -- | 0.0000305 | 0 | 0 | 0 |   |
| FR2_W | 8312F1224000 | 0 | 0 | 0x00 | 7 | 5 | -- | 0.0000305 | 0 | 0 | 0 |   |
| VFZG | 8312F1224000 | 0 | 0 | 0x00 | 9 | 2 | -- | 1.25 | 0 | 0 | 0 | km/h |
| NMOT_W | 8312F1224000 | 0 | 0 | 0x00 | 10 | 5 | -- | 0.25 | 0 | 0 | 0 | min-1 |
| NSOL | 8312F1224000 | 0 | 0 | 0x00 | 12 | 2 | -- | 10 | 0 | 0 | 0 | min-1 |
| WNWKWE_W | 8312F1224000 | 0 | 0 | 0x00 | 13 | 5 | -- | 0.1 | 0 | 0 | 0 | GradKW |
| WNWKWA_W | 8312F1224000 | 0 | 0 | 0x00 | 15 | 5 | -- | 0.1 | 0 | 0 | 0 | GradKW |
| TANS | 8312F1224000 | 0 | 0 | 0x00 | 17 | 2 | -- | 0.75 | -48 | 0 | 0 | Grad C |
| TMOT | 8312F1224000 | 0 | 0 | 0x00 | 18 | 2 | -- | 0.75 | -48 | 0 | 0 | Grad C |
| ZWOUT | 8312F1224000 | 0 | 0 | 0x00 | 19 | 3 | -- | 0.75 | 0 | 0 | 0 | Grad |
| WDKBA | 8312F1224000 | 0 | 0 | 0x00 | 20 | 2 | -- | 0.39216 | 0 | 0 | 0 | % DK |
| MSHFM_W | 8312F1224000 | 0 | 0 | 0x00 | 21 | 5 | -- | 0.1 | 0 | 0 | 0 | kg/h |
| MIIST_W | 8312F1224000 | 0 | 0 | 0x00 | 23 | 5 | -- | 0.0015259 | 0 | 0 | 0 | % |
| UB | 8312F1224000 | 0 | 0 | 0x00 | 25 | 2 | -- | 0.0942 | 0 | 0 | 0 | V |
| UPWG_W | 8312F1224000 | 0 | 0 | 0x00 | 26 | 5 | -- | 0.0048828 | 0 | 0 | 0 | V |
| TKA | 8312F1224000 | 0 | 0 | 0x00 | 28 | 2 | -- | 0.75 | -48 | 0 | 0 | Grad C |
| RKRN_W_0 | 8312F1224000 | 0 | 0 | 0x00 | 29 | 5 | -- | 0.019531 | 0 | 0 | 0 | V |
| RKRN_W_1 | 8312F1224000 | 0 | 0 | 0x00 | 31 | 5 | -- | 0.019531 | 0 | 0 | 0 | V |
| RKRN_W_2 | 8312F1224000 | 0 | 0 | 0x00 | 33 | 5 | -- | 0.019531 | 0 | 0 | 0 | V |
| RKRN_W_3 | 8312F1224000 | 0 | 0 | 0x00 | 35 | 5 | -- | 0.019531 | 0 | 0 | 0 | V |
| RKRN_W_4 | 8312F1224000 | 0 | 0 | 0x00 | 37 | 5 | -- | 0.019531 | 0 | 0 | 0 | V |
| RKRN_W_5 | 8312F1224000 | 0 | 0 | 0x00 | 39 | 5 | -- | 0.019531 | 0 | 0 | 0 | V |
| RKRN_W_6 | 8312F1224000 | 0 | 0 | 0x00 | 41 | 5 | -- | 0.019531 | 0 | 0 | 0 | V |
| RKRN_W_7 | 8312F1224000 | 0 | 0 | 0x00 | 43 | 5 | -- | 0.019531 | 0 | 0 | 0 | V |
| DFMONITOR | 8312F1224001 | 0 | 0 | 0x00 | 3 | 2 | -- | 0,390588 | 0 | 0 | 0 | % |
| LUTSFI1 | 8312F1224003 | 0 | 0 | 0x00 | 3 | 7 | -- | 0.0027756 | 0 | 0 | 0 | sec-1 |
| LUTSFI2 | 8312F1224003 | 0 | 0 | 0x00 | 5 | 7 | -- | 0.0027756 | 0 | 0 | 0 | sec-1 |
| LUTSFI3 | 8312F1224003 | 0 | 0 | 0x00 | 7 | 7 | -- | 0.0027756 | 0 | 0 | 0 | sec-1 |
| LUTSFI4 | 8312F1224003 | 0 | 0 | 0x00 | 9 | 7 | -- | 0.0027756 | 0 | 0 | 0 | sec-1 |
| LUTSFI5 | 8312F1224003 | 0 | 0 | 0x00 | 11 | 7 | -- | 0.0027756 | 0 | 0 | 0 | sec-1 |
| LUTSFI6 | 8312F1224003 | 0 | 0 | 0x00 | 13 | 7 | -- | 0.0027756 | 0 | 0 | 0 | sec-1 |
| LUTSFI7 | 8312F1224003 | 0 | 0 | 0x00 | 15 | 7 | -- | 0.0027756 | 0 | 0 | 0 | sec-1 |
| LUTSFI8 | 8312F1224003 | 0 | 0 | 0x00 | 17 | 7 | -- | 0.0027756 | 0 | 0 | 0 | sec-1 |
| UULSUV | 8312F1224003 | 0 | 0 | 0x00 | 20 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| UULSUV2 | 8312F1224003 | 0 | 0 | 0x00 | 22 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| USVK | 8312F1224003 | 0 | 0 | 0x00 | 20 | 5 | -- | 0.00488 | -1 | 0 | 0 | V |
| USVK2 | 8312F1224003 | 0 | 0 | 0x00 | 22 | 5 | -- | 0.00488 | -1 | 0 | 0 | V |
| MSNDKO | 8312F1224008 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.1 | 0 | 0 | 0 | kg/h |
| FKMSDKA | 8312F1224008 | 0 | 0 | 0x00 | 5 | 5 | -- | 0.00006103 | 0 | 0 | 0 |   |
| FKMSDK | 8312F1224008 | 0 | 0 | 0x00 | 7 | 5 | -- | 0.00006103 | 0 | 0 | 0 |   |
| EISYDKFKAF | 8312F1224008 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.0078125 | 0 | 0 | 0 |   |
| EISYDKKOFF | 8312F1224008 | 0 | 0 | 0x00 | 4 | 5 | -- | 8 | 0 | 0 | 0 |   |
| EISYEVFKAF | 8312F1224008 | 0 | 0 | 0x00 | 5 | 5 | -- | 0.0078125 | 0 | 0 | 0 |   |
| EISYEVKOFF | 8312F1224008 | 0 | 0 | 0x00 | 6 | 5 | -- | 8 | 0 | 0 | 0 |   |
| RKAT | 8312F1224004 | 0 | 0 | 0x00 | 3 | 7 | -- | 0.0468 | 0 | 0 | 0 | % |
| RKAT2 | 8312F1224004 | 0 | 0 | 0x00 | 5 | 7 | -- | 0.0468 | 0 | 0 | 0 | % |
| FRA | 8312F1224004 | 0 | 0 | 0x00 | 7 | 5 | -- | 0.00003052 | 0 | 0 | 0 |   |
| FRA2 | 8312F1224004 | 0 | 0 | 0x00 | 9 | 5 | -- | 0.00003052 | 0 | 0 | 0 |   |
| TEDUB | 8312F1224004 | 0 | 0 | 0x00 | 11 | 2 | -- | 0.01 | 0 | 0 | 0 | s |
| TEDUB2 | 8312F1224004 | 0 | 0 | 0x00 | 12 | 2 | -- | 0.01 | 0 | 0 | 0 | s |
| DYNLSU | 8312F1224004 | 0 | 0 | 0x00 | 13 | 5 | -- | 0.00024 | 0 | 0 | 0 |   |
| DYNLSU2 | 8312F1224004 | 0 | 0 | 0x00 | 15 | 5 | -- | 0.00024 | 0 | 0 | 0 |   |
| LAMSONI | 8312F1224004 | 0 | 0 | 0x00 | 17 | 5 | -- | 0.00024 | 0 | 0 | 0 | V |
| LAMSONI2 | 8312F1224004 | 0 | 0 | 0x00 | 19 | 5 | -- | 0.00024 | 0 | 0 | 0 | V |
| TATEIST | 8312F1224005 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.390625 | 0 | 0 | 0 | % |
| VSASPRI | 8312F1224005 | 0 | 0 | 0x00 | 4 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSASPRI2 | 8312F1224005 | 0 | 0 | 0x00 | 6 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSESPRI | 8312F1224005 | 0 | 0 | 0x00 | 8 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSESPRI2 | 8312F1224005 | 0 | 0 | 0x00 | 10 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSATV | 8312F1224005 | 0 | 0 | 0x00 | 12 | 5 | -- | 0.01 | 0 | 0 | 0 | % |
| VSATV2 | 8312F1224005 | 0 | 0 | 0x00 | 14 | 5 | -- | 0.01 | 0 | 0 | 0 | % |
| VSETV | 8312F1224005 | 0 | 0 | 0x00 | 16 | 5 | -- | 0.01 | 0 | 0 | 0 | % |
| VSETV2 | 8312F1224005 | 0 | 0 | 0x00 | 18 | 5 | -- | 0.01 | 0 | 0 | 0 | % |
| TAML | 8312F1224005 | 0 | 0 | 0x00 | 20 | 2 | -- | 0.39215686 | 0 | 0 | 0 | % |
| VSAADP | 8312F1224006 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSAADP2 | 8312F1224006 | 0 | 0 | 0x00 | 5 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSEADP | 8312F1224006 | 0 | 0 | 0x00 | 7 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSEADP2 | 8312F1224006 | 0 | 0 | 0x00 | 9 | 5 | -- | 0.1 | 0 | 0 | 0 | Grd KW |
| VSAADPFL0 | 8312F1224006 | 0 | 0 | 0x00 | 11 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADPFL1 | 8312F1224006 | 0 | 0 | 0x00 | 12 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADPFL2 | 8312F1224006 | 0 | 0 | 0x00 | 13 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADPFL3 | 8312F1224006 | 0 | 0 | 0x00 | 14 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADP2FL0 | 8312F1224006 | 0 | 0 | 0x00 | 15 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADP2FL1 | 8312F1224006 | 0 | 0 | 0x00 | 16 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADP2FL2 | 8312F1224006 | 0 | 0 | 0x00 | 17 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSAADP2FL3 | 8312F1224006 | 0 | 0 | 0x00 | 18 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADPFL0 | 8312F1224006 | 0 | 0 | 0x00 | 19 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADPFL1 | 8312F1224006 | 0 | 0 | 0x00 | 20 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADPFL2 | 8312F1224006 | 0 | 0 | 0x00 | 21 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADPFL3 | 8312F1224006 | 0 | 0 | 0x00 | 22 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADP2FL0 | 8312F1224006 | 0 | 0 | 0x00 | 23 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADP2FL1 | 8312F1224006 | 0 | 0 | 0x00 | 24 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADP2FL2 | 8312F1224006 | 0 | 0 | 0x00 | 25 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| VSEADP2FL3 | 8312F1224006 | 0 | 0 | 0x00 | 26 | 3 | -- | 0.05 | 0 | 0 | 0 | Grd KW |
| KVA_KORR | 8212F121C1 | 0 | 0 | 0x00 | 2 | 3 | -- | 0.001 | 0 | 0 | 0 | % |
| DNLLMV | 8312F130A101 | 0 | 0 | 0x00 | 6 | 3 | -- | 10 | 0 | 0 | 0 | min-1 |
| DNSACMV | 8312F130A101 | 0 | 0 | 0x00 | 7 | 3 | -- | 10 | 0 | 0 | 0 | min-1 |
| DNSLBV | 8312F130A101 | 0 | 0 | 0x00 | 8 | 3 | -- | 10 | 0 | 0 | 0 | min-1 |
| DNFSACMV | 8312F130A101 | 0 | 0 | 0x00 | 9 | 3 | -- | 10 | 0 | 0 | 0 | min-1 |
| DNFSMV | 8312F130A101 | 0 | 0 | 0x00 | 10 | 3 | -- | 10 | 0 | 0 | 0 | min-1 |
| VVTSW | 8312F122400B | 0 | 0 | 0x00 | 3 | 5 | -- | 0.0015259 | 0 | 0 | 0 | % |
| VVTIW | 8312F122400B | 0 | 0 | 0x00 | 5 | 5 | -- | 0.0015259 | 0 | 0 | 0 | % |
| VVTTV | 8312F122400B | 0 | 0 | 0x00 | 7 | 2 | -- | 0.392157 | 0 | 0 | 0 | % |
| VVTES | 8312F122400B | 0 | 0 | 0x00 | 8 | 2 | -- | 0.5 | -63.5 | 0 | 0 |   |
| VVTSW2 | 8312F122400B | 0 | 0 | 0x00 | 9 | 5 | -- | 0.0015259 | 0 | 0 | 0 | % |
| VVTIW2 | 8312F122400B | 0 | 0 | 0x00 | 11 | 5 | -- | 0.0015259 | 0 | 0 | 0 | % |
| VVTTV2 | 8312F122400B | 0 | 0 | 0x00 | 13 | 2 | -- | 0.392157 | 0 | 0 | 0 | % |
| VVTES2 | 8312F122400B | 0 | 0 | 0x00 | 14 | 2 | -- | 0.5 | -63.5 | 0 | 0 |   |
| MINHUBVSI | 8312F122400B | 0 | 0 | 0x00 | 17 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| DELTAGVFI | 8312F122400B | 0 | 0 | 0x00 | 19 | 7 | -- | 0.0019532 | 0 | 0 | 0 |   |
| FLUB1 | 8312F122400B | 0 | 0 | 0x00 | 21 | 7 | -- | 0.0002441 | 0 | 0 | 0 |   |
| FLUB2 | 8312F122400B | 0 | 0 | 0x00 | 23 | 7 | -- | 0.0002441 | 0 | 0 | 0 |   |
| MINHUBROH | 8312F122400B | 0 | 0 | 0x00 | 27 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| TSG | 8312F122400C | 0 | 0 | 0x00 | 3 | 2 | -- | 0.75 | -48 | 0 | 0 | Grad C |
| DMVAD | 8312F122400C | 0 | 0 | 0x00 | 5 | 7 | -- | 0.00305185 | 0 | 0 | 0 | % |
| DPS | 8312F122400C | 0 | 0 | 0x00 | 7 | 7 | -- | 0.03906247 | 0 | 0 | 0 | hPa |
| DPSRAUS | 8312F122400C | 0 | 0 | 0x00 | 9 | 5 | -- | 5.01945 | 0 | 0 | 0 | hPa |
| FKMSVVT | 8312F122400C | 0 | 0 | 0x00 | 11 | 5 | -- | 0.00006104 | 0 | 0 | 0 |   |
| FPRSTEP | 8312F122400C | 0 | 0 | 0x00 | 13 | 2 | -- | 1 | 0 | 0 | 0 |   |
| LRNSTEP | 8312F122400C | 0 | 0 | 0x00 | 14 | 2 | -- | 1 | 0 | 0 | 0 |   |
| MSNVVTO | 8312F122400C | 0 | 0 | 0x00 | 15 | 7 | -- | 0.1 | 0 | 0 | 0 | kg/h |
| NNW10 | 8312F122400C | 0 | 0 | 0x00 | 17 | 7 | -- | 1 | 0 | 0 | 0 |   |
| NNW11 | 8312F122400C | 0 | 0 | 0x00 | 19 | 7 | -- | 1 | 0 | 0 | 0 |   |
| NNW12 | 8312F122400C | 0 | 0 | 0x00 | 21 | 7 | -- | 1 | 0 | 0 | 0 |   |
| NNW20 | 8312F122400C | 0 | 0 | 0x00 | 23 | 7 | -- | 1 | 0 | 0 | 0 |   |
| NNW21 | 8312F122400C | 0 | 0 | 0x00 | 25 | 7 | -- | 1 | 0 | 0 | 0 |   |
| NNW22 | 8312F122400C | 0 | 0 | 0x00 | 27 | 7 | -- | 1 | 0 | 0 | 0 |   |
| NSOLFASTA | 8312F122400D | 0 | 0 | 0x00 | 3 | 5 | -- | 0.25 | 0 | 0 | 0 | min-1 |
| RL | 8312F122400D | 0 | 0 | 0x00 | 5 | 5 | -- | 0.0234375 | 0 | 0 | 0 | % |
| RLSOL | 8312F122400D | 0 | 0 | 0x00 | 7 | 5 | -- | 0.0234375 | 0 | 0 | 0 | % |
| TE | 8312F122400D | 0 | 0 | 0x00 | 9 | 5 | -- | 0.008 | 0 | 0 | 0 | ms |
| TE2 | 8312F122400D | 0 | 0 | 0x00 | 11 | 5 | -- | 0.008 | 0 | 0 | 0 | ms |
| VVTSTATUS | 8312F122400D | 0 | 0 | 0x00 | 13 | 5 | -- | 1 | 0 | 0 | 0 |   |
| WDKBAFASTA | 8312F122400D | 0 | 0 | 0x00 | 15 | 5 | -- | 0.02441406 | 0 | 0 | 0 | %DK |
| WDKS | 8312F122400D | 0 | 0 | 0x00 | 17 | 5 | -- | 0.00152588 | 0 | 0 | 0 | % |
| WPED | 8312F122400D | 0 | 0 | 0x00 | 19 | 5 | -- | 0.0015259 | 0 | 0 | 0 | %PED |
| ZWIST | 8312F122400D | 0 | 0 | 0x00 | 21 | 3 | -- | 0.75 | 0 | 0 | 0 | Grad KW |
| DMLLRI | 8312F122400D | 0 | 0 | 0x00 | 23 | 7 | -- | 0.0030518 | 0 | 0 | 0 | % |
| MIMIN | 8312F122400D | 0 | 0 | 0x00 | 25 | 5 | -- | 0.00152588 | 0 | 0 | 0 | % |
| MDGEN | 8312F122400E | 0 | 0 | 0x00 | 3 | 2 | -- | 0.390625 | 0 | 0 | 0 | % |
| MDKO | 8312F122400E | 0 | 0 | 0x00 | 4 | 2 | -- | 0.390625 | 0 | 0 | 0 | % |
| DMRLLR | 8312F122400E | 0 | 0 | 0x00 | 5 | 5 | -- | 0.097647 | 0 | 0 | 0 | % |
| MDWAN | 8312F122400E | 0 | 0 | 0x00 | 8 | 5 | -- | 0.0030518 | 0 | 0 | 0 | % |
| DWKR | 8312F122400E | 0 | 0 | 0x00 | 10 | 3 | -- | 0.75 | 0 | 0 | 0 | Grad KW |
| DZWS | 8312F122400E | 0 | 0 | 0x00 | 11 | 3 | -- | 0.75 | 0 | 0 | 0 | Grad KW |
| DFFGEN | 8312F122400E | 0 | 0 | 0x00 | 12 | 2 | -- | 0.3921568 | 0 | 0 | 0 | % |
| TUMG | 8312F122400E | 0 | 0 | 0x00 | 13 | 2 | -- | 0.75 | -48 | 0 | 0 | Grad C |
| DMVADFS | 8312F122400E | 0 | 0 | 0x00 | 14 | 7 | -- | 0.0030518 | 0 | 0 | 0 | % |
| DMVADKO | 8312F122400E | 0 | 0 | 0x00 | 16 | 7 | -- | 0.0030518 | 0 | 0 | 0 | % |
| DLAHI | 8312F122400E | 0 | 0 | 0x00 | 18 | 7 | -- | 0.000030518 | 0 | 0 | 0 |   |
| DLAHI2 | 8312F122400E | 0 | 0 | 0x00 | 20 | 7 | -- | 0.000030518 | 0 | 0 | 0 |   |
| RINH | 8312F122400E | 0 | 0 | 0x00 | 22 | 5 | -- | 2 | 0 | 0 | 0 | Ohm |
| RINH2 | 8312F122400E | 0 | 0 | 0x00 | 24 | 5 | -- | 2 | 0 | 0 | 0 | Ohm |
| RKATS | 8312F122400E | 0 | 0 | 0x00 | 26 | 7 | -- | 0.0468749 | 0 | 0 | 0 | % |
| DPSSOL | 8312F122400E | 0 | 0 | 0x00 | 28 | 7 | -- | 0.03906247 | 0 | 0 | 0 | hPa |
| CO_POT | 8312F122400F | 0 | 0 | 0x00 | 5 | 7 | -- | 1 | 0 | 0 | 0 |   |
| UPWG | 8312F122400F | 0 | 0 | 0x00 | 7 | 5 | -- | 0.0048828 | 0 | 0 | 0 | V |
| MINHUB | 8312F122400F | 0 | 0 | 0x00 | 9 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| GVIST | 8312F122400F | 0 | 0 | 0x00 | 12 | 7 | -- | 0.00195314 | 0 | 0 | 0 |   |
| FTBR | 8312F122400F | 0 | 0 | 0x00 | 14 | 5 | -- | 0.00003052 | 0 | 0 | 0 |   |
| FHO | 8312F122400F | 0 | 0 | 0x00 | 16 | 5 | -- | 0.00006104 | 0 | 0 | 0 |   |
| FTVDK | 8312F122400F | 0 | 0 | 0x00 | 18 | 2 | -- | 0.0078125 | 0 | 0 | 0 |   |
| MSNVVTOLL | 8312F122400F | 0 | 0 | 0x00 | 20 | 7 | -- | 0.1 | 0 | 0 | 0 | kg/h |
| VSESPRS | 8312F122400F | 0 | 0 | 0x00 | 24 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad KW |
| VSE2SPRS | 8312F122400F | 0 | 0 | 0x00 | 26 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad KW |
| VSASPRS | 8312F122400F | 0 | 0 | 0x00 | 29 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad KW |
| VSA2SPRS | 8312F122400F | 0 | 0 | 0x00 | 30 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad KW |
| EVHUBI | 8312F1224010 | 0 | 0 | 0x00 | 5 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| EVHUBI2 | 8312F1224010 | 0 | 0 | 0x00 | 7 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| EVHUBS | 8312F1224010 | 0 | 0 | 0x00 | 9 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| OFWNKADBG | 8312F1224010 | 0 | 0 | 0x00 | 11 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| DFSERESZ | 8312F1224010 | 0 | 0 | 0x00 | 16 | 5 | -- | 1 | 0 | 0 | 0 |   |
| DMVADFK | 8312F1224010 | 0 | 0 | 0x00 | 18 | 7 | -- | 0.0030517 | 0 | 0 | 0 | % |
| DMVADLL | 8312F1224010 | 0 | 0 | 0x00 | 20 | 7 | -- | 0.0030517 | 0 | 0 | 0 | % |
| EXWINKI | 8312F1224010 | 0 | 0 | 0x00 | 22 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| EXWINKI2 | 8312F1224010 | 0 | 0 | 0x00 | 24 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| EXWINKS | 8312F1224010 | 0 | 0 | 0x00 | 26 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| FKMSVVTA | 8312F1224011 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00006104 | 0 | 0 | 0 |   |
| FOFRESZ | 8312F1224011 | 0 | 0 | 0x00 | 5 | 5 | -- | 1 | 0 | 0 | 0 |   |
| MSDIF | 8312F1224011 | 0 | 0 | 0x00 | 7 | 7 | -- | 0.1 | 0 | 0 | 0 | kg/h |
| TABGM | 8312F1224011 | 0 | 0 | 0x00 | 9 | 2 | -- | 5 | -50 | 0 | 0 | Grad C |
| TNSE | 8312F1224011 | 0 | 0 | 0x00 | 10 | 5 | -- | 0.1 | 0 | 0 | 0 | s |
| OZRWPERM | 8312F1224011 | 0 | 0 | 0x00 | 12 | 7 | -- | 10 | 0 | 0 | 0 |   |
| OZRWKVB | 8312F1224011 | 0 | 0 | 0x00 | 14 | 7 | -- | 10 | 0 | 0 | 0 |   |
| OZPERMLOW | 8312F1224011 | 0 | 0 | 0x00 | 24 | 5 | -- | 0.00009155 | 0 | 0 | 0 |   |
| OZPERMEX | 8312F1224011 | 0 | 0 | 0x00 | 26 | 5 | -- | 0.00009155 | 0 | 0 | 0 |   |
| OZPERMOFF | 8312F1224011 | 0 | 0 | 0x00 | 28 | 7 | -- | 0.00018311 | 0 | 0 | 0 |   |
| OZKVBOG | 8312F1224011 | 0 | 0 | 0x00 | 30 | 7 | -- | 0.01831082 | 0 | 0 | 0 |   |
| OZPERMBOG | 8312F1224011 | 0 | 0 | 0x00 | 32 | 7 | -- | 0.000030517585 | 0 | 0 | 0 |   |
| OZOELKM | 8312F1224011 | 0 | 0 | 0x00 | 34 | 7 | -- | 10 | 0 | 0 | 0 | km |
| NADMTLL | 8312F1224012 | 0 | 0 | 0x00 | 3 | 5 | -- | 1 | 0 | 0 | 0 |   |
| NTGLM | 8312F1224012 | 0 | 0 | 0x00 | 5 | 5 | -- | 1 | 0 | 0 | 0 |   |
| NTKLM | 8312F1224012 | 0 | 0 | 0x00 | 7 | 5 | -- | 1 | 0 | 0 | 0 |   |
| NDIPFRO | 8312F1224012 | 0 | 0 | 0x00 | 9 | 5 | -- | 1 | 0 | 0 | 0 |   |
| NKFL | 8312F1224012 | 0 | 0 | 0x00 | 11 | 2 | -- | 1 | 0 | 0 | 0 |   |
| SSLLCNT | 8312F1224012 | 0 | 0 | 0x00 | 12 | 2 | -- | 1 | 0 | 0 | 0 |   |
| MINHUBFAK | 8312F1224012 | 0 | 0 | 0x00 | 15 | 2 | -- | 0.00784314 | 0 | 0 | 0 |   |
| MINADRDY | 8312F1224012 | 0 | 0 | 0x00 | 16 | 2 | -- | 1 | 0 | 0 | 0 |   |
| FDLUBBGL | 8312F1224012 | 0 | 0 | 0x00 | 21 | 5 | -- | 0.00024414 | 0 | 0 | 0 |   |
| OFWNKBG1 | 8312F1224012 | 0 | 0 | 0x00 | 24 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| OFWNKBG2 | 8312F1224012 | 0 | 0 | 0x00 | 26 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| OFWNKMX | 8312F1224012 | 0 | 0 | 0x00 | 28 | 5 | -- | 0.1 | 0 | 0 | 0 | Grad |
| WTSG | 8312F1304101 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| USHK2 | 8312F1304501 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| USHK2_W | 8312F1304501 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | -1 | 0 | 0 | V |
| UPWG1 | 8312F1304601 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| UPWG2 | 8312F1304701 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| USHK | 8312F1304801 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| USHK_W | 8312F1304801 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | -1 | 0 | 0 | V |
| WUB | 8312F1304A01 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.0942 | 0 | 0 | 0 | V |
| UDKP2 | 8312F1304C01 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.001222 | 0 | 0 | 0 | V |
| UDKP1V | 8312F1304D01 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| UDKP1 | 8312F1304E01 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.001222 | 0 | 0 | 0 | V |
| UHFM | 8312F1304F01 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00977 | 0 | 0 | 0 | V |
| WTMOT | 8312F1305001 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| WTANS | 8312F1305101 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| WTKA | 8312F1305201 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| UHSV | 8312F1305C01 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| UHSV2 | 8312F1305D01 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| UHSH | 8312F1305E01 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| UHSH2 | 8312F1305F01 | 0 | 0 | 0x00 | 3 | 2 | -- | 0.019531 | 0 | 0 | 0 | V |
| DISA | 8312F1306D01 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| UDDSS | 8312F1306F01 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| UDSU | 8312F1307001 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| UUPTES | 8312F1307401 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.00488 | 0 | 0 | 0 | V |
| MINHUB_W | 8312F130A301 | 0 | 0 | 0x00 | 3 | 5 | -- | 0.001 | 0 | 0 | 0 | mm |
| OFWTSTBER | 8312F130A401 | 0 | 0 | 0x00 | 3 | 2 | -- | 1 | 0 | 0 | 0 |   |
| OFWNKTEST | 8312F130A401 | 0 | 0 | 0x00 | 4 | 7 | -- | 0.1 | 0 | 0 | 0 | Grad |
| OSCDKTF | 8212F1211C | 0 | 0 | 0x00 | 4 | 5 | -- | 0.00024414 | 0 | 0 | 0 |   |
| OSCDKTF2 | 8212F1211C | 0 | 0 | 0x00 | 6 | 5 | -- | 0.00024414 | 0 | 0 | 0 |   |
| ENDE |  |  |  |  | 1 | 1 | -- | 1 | 0 | 0 | 0 |   |

<a id="table-bits"></a>
### BITS

Dimensions: 121 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| B_FOFR1 | 19 | 0x01 | 0x01 |
| B_KRDWS | 4 | 0x01 | 0x01 |
| B_MIL | 22 | 0x01 | 0x01 |
| B_FS | 7 | 0x01 | 0x01 |
| B_ECULOCKF | 3 | 0x01 | 0x01 |
| B_LRNRDYFAST | 4 | 0x01 | 0x01 |
| B_LLTD | 11 | 0x01 | 0x01 |
| B_LLK | 19 | 0x01 | 0x01 |
| B_TEAKT | 22 | 0x01 | 0x01 |
| B_VVTNOTL | 23 | 0x01 | 0x01 |
| B_NVRBUPOK | 32 | 0x01 | 0x01 |
| B_ATMTPA | 3 | 0x01 | 0x01 |
| B_ATMTPK | 4 | 0x01 | 0x01 |
| B_KH | 13 | 0x01 | 0x01 |
| B_NSUB | 14 | 0x01 | 0x01 |
| B_TE | 15 | 0x01 | 0x01 |
| B_FE | 28 | 0x01 | 0x01 |
| B_SSLL | 13 | 0x01 | 0x01 |
| B_TDAON | 14 | 0x01 | 0x01 |
| B_BGLRDY | 23 | 0x01 | 0x01 |
| B_KL15 | 3 | 0x01 | 0x01 |
| B_ESTART | 3 | 0x02 | 0x02 |
| B_KUPPL | 3 | 0x04 | 0x04 |
| B_BL | 3 | 0x08 | 0x08 |
| B_BR | 3 | 0x10 | 0x10 |
| B_KO | 3 | 0x80 | 0x80 |
| B_LL | 3 | 0x01 | 0x01 |
| B_VL | 3 | 0x02 | 0x02 |
| B_SBBHK2 | 3 | 0x04 | 0x04 |
| B_SBBHK | 3 | 0x08 | 0x08 |
| B_SBBVK2 | 3 | 0x10 | 0x10 |
| B_SBBVK | 3 | 0x20 | 0x20 |
| B_LR2 | 3 | 0x40 | 0x40 |
| B_LR | 3 | 0x80 | 0x80 |
| B_KD | 4 | 0x04 | 0x04 |
| B_PN | 4 | 0x08 | 0x08 |
| B_ECULOCK | 4 | 0x10 | 0x10 |
| B_TEHB | 4 | 0x20 | 0x20 |
| B_SA | 4 | 0x40 | 0x40 |
| B_LRNRDY | 4 | 0x80 | 0x80 |
| B_SLV | 21 | 0x02 | 0x02 |
| B_SLP | 21 | 0x04 | 0x04 |
| B_KOE | 21 | 0x08 | 0x08 |
| B_HSVE2 | 21 | 0x10 | 0x10 |
| B_HSVE | 21 | 0x20 | 0x20 |
| B_HSHE2 | 21 | 0x40 | 0x40 |
| B_HSHE | 21 | 0x80 | 0x80 |
| B_AKR | 22 | 0x08 | 0x08 |
| B_EBL | 22 | 0x10 | 0x10 |
| B_EKP | 22 | 0x20 | 0x20 |
| B_ETR | 22 | 0x40 | 0x40 |
| B_STA | 22 | 0x80 | 0x80 |
| B_NOKATFZ | 3 | 0x01 | 0x01 |
| B_AUTGET | 3 | 0x02 | 0x02 |
| B_ACC | 3 | 0x04 | 0x04 |
| B_ASCPKW | 3 | 0x08 | 0x08 |
| B_ARSVAR | 3 | 0x10 | 0x10 |
| B_TXUGET | 3 | 0x20 | 0x20 |
| B_KOGER | 3 | 0x40 | 0x40 |
| B_AGR | 3 | 0x80 | 0x80 |
| B_MFL | 4 | 0x01 | 0x01 |
| B_AKRFZ | 4 | 0x02 | 0x02 |
| B_DISA_GESCH_GL_VAR_NEU | 3 | 0x01 | 0x01 |
| B_DISA_GEREG_LAGEM_VAR_NEU | 3 | 0x04 | 0x04 |
| B_ANSKL_GL_VAR_NEU | 3 | 0x08 | 0x08 |
| B_AGR_VAR_NEU | 3 | 0x80 | 0x80 |
| B_ABGK_MONO_GL_VAR_NEU | 4 | 0x01 | 0x01 |
| B_ABGK_Y_GL_VAR_NEU | 4 | 0x02 | 0x02 |
| B_ABGK_STER_GL_VAR_NEU | 4 | 0x04 | 0x04 |
| B_NOKATFZ_VAR_NEU | 4 | 0x08 | 0x08 |
| B_LIN_LSVK_GL_VAR_NEU | 4 | 0x10 | 0x10 |
| B_ZWP_LSVK_GL_VAR_NEU | 4 | 0x20 | 0x20 |
| B_SLPVAR_VAR_NEU | 4 | 0x40 | 0x40 |
| B_SLVVAR_VAR_NEU | 4 | 0x80 | 0x80 |
| B_AKRFZ_VAR_NEU | 5 | 0x01 | 0x01 |
| B_SOUNDKL_VAR_NEU | 5 | 0x02 | 0x02 |
| B_GLFVAR_VAR_NEU | 5 | 0x04 | 0x04 |
| B_ELUE400_GL_VAR_NEU | 5 | 0x08 | 0x08 |
| B_ELUE600_GL_VAR_NEU | 5 | 0x10 | 0x10 |
| B_EBLVAR_VAR_NEU | 5 | 0x20 | 0x20 |
| B_MFL_VAR_NEU | 5 | 0x40 | 0x40 |
| B_SPTVAR_VAR_NEU | 5 | 0x80 | 0x80 |
| B_STRVAR_VAR_NEU | 6 | 0x01 | 0x01 |
| B_TOENSVAR_VAR_NEU | 6 | 0x02 | 0x02 |
| B_HS_GL_VAR_NEU | 6 | 0x10 | 0x10 |
| B_SSG_GL_VAR_NEU | 6 | 0x20 | 0x20 |
| B_EGS_GL_VAR_NEU | 6 | 0x40 | 0x40 |
| B_TXUGET_VAR_NEU | 6 | 0x80 | 0x80 |
| B_ASCPKW_VAR_NEU | 7 | 0x01 | 0x01 |
| B_ACC_VAR_NEU | 7 | 0x02 | 0x02 |
| B_ARSVAR_VAR_NEU | 7 | 0x08 | 0x08 |
| B_AFSVAR_VAR_NEU | 7 | 0x40 | 0x40 |
| B_KOVAR_VAR_NEU | 7 | 0x80 | 0x80 |
| B_IBSDETEC_VAR_NEU | 8 | 0x80 | 0x80 |
| B_KATFZ | 2 | 0x01 | 0x01 |
| B_CDTES | 2 | 0x04 | 0x04 |
| B_CDSLS | 2 | 0x08 | 0x08 |
| B_CDLSV | 2 | 0x20 | 0x20 |
| B_CDHSV | 2 | 0x40 | 0x40 |
| B_CDAGR | 2 | 0x80 | 0x80 |
| B_KATRDY | 3 | 0x01 | 0x01 |
| B_TESRDY | 3 | 0x04 | 0x04 |
| B_SLSRDY | 3 | 0x08 | 0x08 |
| B_LSRDY | 3 | 0x20 | 0x20 |
| B_HSRDY | 3 | 0x40 | 0x40 |
| B_AGRRDY | 3 | 0x80 | 0x80 |
| B_FGRAT | 2 | 0x01 | 0x01 |
| B_FGRHSA | 2 | 0x02 | 0x02 |
| B_FGRTBE | 2 | 0x04 | 0x04 |
| B_FGRTSE | 2 | 0x08 | 0x08 |
| B_FGRTVE | 2 | 0x10 | 0x10 |
| B_FGRTWA | 2 | 0x20 | 0x20 |
| L_FGR | 2 | 0x40 | 0x40 |
| B_ACC_FGR | 2 | 0x80 | 0x80 |
| B_GAD | 2 | 0x01 | 0x01 |
| Z_LSH | 2 | 0x02 | 0x02 |
| Z_LSH2 | 2 | 0x02 | 0x02 |
| B_NMOT | 15 | 0x01 | 0x01 |
| B_MINHUBVS | 16 | 0x01 | 0x01 |
| B_FBGL | 25 | 0x01 | 0x01 |
| B_BGL | 26 | 0x01 | 0x01 |

<a id="table-vvtstatusbg2-2"></a>
### VVTSTATUSBG2_2

Dimensions: 11 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | keine Testeranforderung vorhanden |
| 0x01 | Startbedingung nicht erfüllt (Motorlauf) |
| 0x02 | nicht belegt |
| 0x03 | nicht belegt |
| 0x04 | nicht belegt |
| 0x05 | Lernvorgang aktiv |
| 0x06 | nicht belegt |
| 0x07 | Abbruch durch Motorlauf, Fehler im VVT-System, Rücknahme Lernanforderung |
| 0x08 | Lernanforderung ohne Fehler beendet |
| 0x09 | Lernvorgang mit aufgetretenem Fehler beendet |
| 0xXY | Fehlerhafter Status |

<a id="table-sondenstatus"></a>
### SONDENSTATUS

Dimensions: 11 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Funktion noch nicht gestartet |
| 0x01 | Start-/Ansteuerbedingung nicht erfüllt |
| 0x02 | Uebergabeparameter nicht plausibel |
| 0x03 | Funktion wartet auf Freigabe |
| 0x04 | nicht belegt |
| 0x05 | Funktion läuft |
| 0x06 | Funktion beendet ohne Ergebnis |
| 0x07 | Funktion abgebrochen (kein Zyklusflag/Readiness gesetzt) |
| 0x08 | Funktion vollständig durchlaufen (Zyklusflag/Readiness gesetzt)und kein Fehler erkannt |
| 0x09 | Funktion vollständig durchlaufen (Zyklusflag/Readiness gesetzt)und Fehler erkannt |
| 0xXY | Fehlerhafter Status |

<a id="table-sondenstatus-erw"></a>
### SONDENSTATUS_ERW

Dimensions: 13 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Diagnose inaktiv |
| 0x01 | Diagnose Step 1 |
| 0x02 | Diagnose Step 2 |
| 0x10 | Diagnose beendet Sensor OK |
| 0x11 | Diagnose beendet, Lambdasonde vor Kat vertauscht |
| 0x12 | Diagnose beendet, Lambdasonde hinter Kat vertauscht |
| 0x13 | Diagnose beendet, Lambdasonde vor und nach Kat vertauscht |
| 0x14 | Diagnose beendet, Lambdasonde vor Kat Bank 1 unplausibel |
| 0x15 | Diagnose beendet, Lambdasonde vor Kat Bank 2 unplausibel |
| 0x16 | Diagnose beendet, Lambdasonde nach Kat Bank 1 unplausibel |
| 0x17 | Diagnose beendet, Lambdasonde nach Kat Bank 2 unplausibel |
| 0x18 | Diagnose beendet, kein interpretierbares Ergebnis |
| 0xXY | Fehlerhafter Status |

<a id="table-genhersteller"></a>
### GENHERSTELLER

Dimensions: 4 rows × 2 columns

| NR | HERSTELLER_TEXT |
| --- | --- |
| 0x08 | BOSCH |
| 0x0B | VALEO |
| 0x1D | DENSO |
| 0xXY | unbekannter Hersteller |

<a id="table-ewsstart"></a>
### EWSSTART

Dimensions: 5 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | ME9.2 bereit, Startwert zu empfangen |
| 0x01 | kein freier Startwert mit Freigabe vorhanden |
| 0x02 | noch kein Startwert gespeichert |
| 0x03 | Startwert nicht plausibel (wie im DS2-LH definiert) |
| 0xXY | Fehlerhafter Status |

<a id="table-ewsempfangsstatus"></a>
### EWSEMPFANGSSTATUS

Dimensions: 15 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Startwertprogrammierung bzw. -ruecksetzen war erfolgreich |
| 0x01 | falscher Startwert beim Ruecksetzen (EWS u. DME passen ni. zusammen)  |
| 0x02 | Telegramminhalt war kein Startwert (event. Wechselcode) |
| 0x03 | Schnittstellenfehler DWA: Frame o. Parity oder kein Signal (Timeout) |
| 0x04 | Prozess laeuft |
| 0x05 | Programmierung bzw. Ruecksetzen im Fahrzyklus noch nicht ausgefuehrt |
| 0x06 | gleiche Zufallszahl wie bei vorherigem Ruecksetzen trotz Weiterschaltung |
| 0x07 | noch kein Startwert programmiert |
| 0x10 | Startwert nicht korrekt in Flash programmiert |
| 0x11 | Wechselcode nicht korrekt in EEPROM-Spiegel programmiert |
| 0x12 | Zufallszahl nicht korrekt in EEPROM-Spiegel programmiert |
| 0x20 | Fehler bei Startwertprogrammierroutine |
| 0x21 | 2-aus-3-Startwertablage im Flash nicht in Ordnung |
| 0x22 | Ablage im EEPROM-Spiegel nicht in Ordnung |
| 0xXY | Fehlerhafter Status |

<a id="table-regel"></a>
### REGEL

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Regelung AUS, Einschaltbedingung noch nicht erfuellt |
| 0x02 | Regelung EIN |
| 0x04 | Regelung AUS wegen Fahrbedingung |
| 0x08 | Regelung AUS wegen erkanntem Fehler |
| 0x10 | Regelung EIN mit Einschraenkung |
| 0xXY | ?? |

<a id="table-slsstatus"></a>
### SLSSTATUS

Dimensions: 29 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Sekundaerluftdiagnose laeuft aufgrund einer Testanforderung gerade ab |
| 0x01 | Systemtest kann nicht gestartet werden |
| 0x02 | Funktionsanforderung vorhanden |
| 0x05 | keine Funktionsanforderung an die Sekundaerluftdiagnose |
| 0x06 | Systemtest SLS ist beendet |
| 0x10 | Sekundaerluftmindermasse erkannt (bei 2 Bank Systemen gilt dies nur für Bank1) |
| 0x11 | Sekundaerluftmindermasse auf Bank2 erkannt (nur bei 2 Bank Systemen, keine Bewertung von Bank1) |
| 0x12 | Sekundaerluftmindermasse auf Bank1 und Bank2 erkannt (nur bei 2 Bank Systemen) |
| 0x13 | Sekundaerluftdiagnoseergebnis n.i.o. (bei 2 Bank Systemen gilt Aussage nur für Bank1) |
| 0x14 | Sekundaerluftdiagnoseergebnis 2 n.i.o. (nur bei 2 Bank Systemen) |
| 0x15 | Sekundaerluftdiagnoseergebnis Bank 1 + 2 n.i.o. (nur bei 2 Bank Systemen) |
| 0x16 | Sekundaerluftdiagnoseergebnis i.o. |
| 0x20 | Sekundaerluftwicklungstemperatur zu groß |
| 0x21 | SLP-Abbruch z.B. aufgrund: Sek Druckdifferenz, Batteriesp., Motorluftmasse außerhalb der Schwellen |
| 0x22 | Messphase abgebrochen wurde |
| 0x23 | Offsetphase abgebrochen wurde |
| 0x24 | Vorsteuerung auf Bank1 und Bank2 außerhalb der Schwellen lag (nur bei 2-Bank Systemen) |
| 0x25 | Vorsteuerung auf Bank1 außerhalb der Schwellen lag |
| 0x26 | Vorsteuerung auf Bank2 außerhalb der Schwellen lag |
| 0x30 | Motortemperatur noch zu gering ist |
| 0x31 | Wicklungstemperatur noch zu hoch ist |
| 0x32 | Fehler einer das Ergebnis beeinflussenden Komponente vorliegt |
| 0x33 | Motortemp., Ansauglufttemp. oder Kattemp. außerhalb der Grenzen, B_zslsp(2) noch nicht geloescht |
| 0x34 | Motorluftmasse außerhalb der Grenzen liegt |
| 0x35 | LSU(2) nicht Betriebsbereit, VVT umschaltet, r1 nicht im Diagnosefenster |
| 0x36 | Tankentlueftung aktiv ist |
| 0xFE | nicht genau spezifizierter Grund |
| 0xFF | Ungueltigkeitswert (wird zur Zeit nicht benutzt) |
| 0xXY | Status Systemtest SLS kann nicht ausgegeben werden |

<a id="table-tevstatus"></a>
### TEVSTATUS

Dimensions: 9 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Systemtest TEV laeuft |
| 0x01 | Systemtest kann nicht gestartet werden |
| 0x05 | Systemtest ist nicht gestartet |
| 0x06 | Systemtest TEV ist beendet |
| 0x08 | TEV noch nicht geschlossen für Drehzahlpruefung |
| 0x09 | Beladungspruefung laeuft |
| 0x0A | Systemtest TEV beendet ohne Fehler |
| 0x0B | Systemtest TEV beendet mit Fehler |
| 0xXY | Status Systemtest TEV kann nicht ausgegeben werden |

<a id="table-stagedmtl"></a>
### STAGEDMTL

Dimensions: 19 rows × 2 columns

| STAGE | TEXT |
| --- | --- |
| 0x00 | Funktion laeuft |
| 0x01 | Referenzleckmessung laeuft |
| 0x02 | Grobleckpruefung/verlaengerte Grobleckpruefung laeuft |
| 0x03 | Feinstleckpruefung laeuft |
| 0x04 | Referenzleckmessung 2 laeuft |
| 0x05 | Funktion nicht aktiv |
| 0x06 | Funktion beendet |
| 0x0A | Funktion kann nicht gestartet werden |
| 0x0B | Funktion nicht startbar  --&gt; Ubatt ausserhalb Bereich |
| 0x0C | Funktion nicht startbar  --&gt; Schwankung Referenzstrom zu gross |
| 0x0D | Funktion nicht startbar  --&gt; Elektrische Fehler liegen vor |
| 0x0E | Funktion nicht startbar  --&gt; max. Diagnosedauer erreicht |
| 0x0F | Funktion nicht startbar  --&gt; keine Grobleckfreigabe |
| 0x14 | Funktion wurde abgebrochen |
| 0x15 | Abbruch  --&gt;  Betankung erkannt |
| 0x16 | Abbruch  --&gt;  Tankdeckel geoeffnet |
| 0x17 | Abbruch  --&gt;  Ubatt-Schwankung zu gross |
| 0x18 | Abbruch  --&gt;  Bedingung Kl.15 AUS/EIN erkannt |
| 0xXY | Stagepointer unbekannt |

<a id="table-stagedmtlfreeze"></a>
### STAGEDMTLFREEZE

Dimensions: 23 rows × 2 columns

| STAGE | TEXT |
| --- | --- |
| 0x00 | Funktion laeuft |
| 0x01 | Referenzleckmessung |
| 0x02 | Grobleckpruefung/verlaengerte Grobleckpruefung |
| 0x03 | Feinstleckpruefung |
| 0x04 | Referenzleckmessung 2 |
| 0x0A | Funktion kann nicht gestartet werden |
| 0x0B | Funktion war nicht startbar  --&gt; Ubatt ausserhalb Bereich |
| 0x0C | Funktion war nicht startbar  --&gt; Schwankung Referenzstrom zu gross |
| 0x0D | Funktion war nicht startbar  --&gt; Elektrische Fehler liegen vor |
| 0x0E | Funktion war nicht startbar  --&gt; max. Diagnosedauer erreicht |
| 0x0F | Funktion war nicht startbar  --&gt; keine Grobleckfreigabe |
| 0x14 | Funktion wurde abgebrochen |
| 0x15 | Abbruch  --&gt;  Betankung erkannt |
| 0x16 | Abbruch  --&gt;  Tankdeckel geoeffnet |
| 0x17 | Abbruch  --&gt;  Ubatt-Schwankung zu gross |
| 0x18 | Abbruch  --&gt;  Bedingung Kl.15 AUS/EIN erkannt |
| 0x1E | Funktion beendet, Dicht erkannt |
| 0x1F | Funktion beendet, Feinleck erkannt |
| 0x20 | Funktion beendet, Grobleck erkannt |
| 0x21 | Funktion beendet, Modulfehler erkannt |
| 0x22 | Funktion beendet, kein Grobleck erkannt |
| 0xFF | DM-TL Diagnose noch nie durchlaufen |
| 0xXY | Stagepointer unbekannt |

<a id="table-lsustatus"></a>
### LSUSTATUS

Dimensions: 4 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x01 | LSU Dynamikprüfung aktiv |
| 0x02 | LSU Prüfung abgeschlossen |
| 0x03 | LSU Prüfung abgeschlossen und noch aktiv |
| 0xXY | Status LSU-Diagnose kann nicht ausgegeben werden |

<a id="table-disastatus"></a>
### DISASTATUS

Dimensions: 9 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | nicht gelernt |
| 0x01 | Lernschritt 1 (Naehe Unterer mech. Anschlag) |
| 0x02 | Lernschritt 2 (Langsames Fahren gegen unteren mech. Anschlag) |
| 0x03 | Lernen erfolgreich beendet |
| 0x04 | Poti MIN- oder MAX-Fehler (Verlassen des Diagnosebereichs) |
| 0x05 | Lagereglerfehler |
| 0x06 | Temperaturwarnung |
| 0x07 | Uebertemperatur Antriebseinheit |
| 0xXY | Status DISA-Diagnose kann nicht ausgegeben werden |

<a id="table-lambdastatus"></a>
### LAMBDASTATUS

Dimensions: 6 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Steuerbetrieb, Startbedingungen noch nicht erfuellt |
| 0x01 | Regelbetrieb mit zwei Sonden |
| 0x02 | Steuerbetrieb durch Betriebsbedingungen |
| 0x04 | Steuerbetrieb nach Systemfehler |
| 0x08 | Regelung mit nur einer Sonde (vor Kat) |
| 0xXY | Status LSU-Diagnose kann nicht ausgegeben werden |

<a id="table-betriebsstundenstatus"></a>
### BETRIEBSSTUNDENSTATUS

Dimensions: 4 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Betriebsstundenzaehler verstanden und akzeptiert (top_w &lt; 10h) |
| 0x01 | Betriebsstundenzaehler verstanden aber nicht akzeptiert (top_w &gt; 10h) |
| 0x02 | Betriebsstundenzaehler nicht verstanden und nicht akzeptiert |
| 0xXY | Betriebsstundenzaehler kann nicht ausgegeben werden |

<a id="table-katstatus"></a>
### KATSTATUS

Dimensions: 7 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Systemtest KAT laeuft |
| 0x01 | Startbedingungen nicht erfüllt |
| 0x05 | Systemtest ist noch nicht gestartet |
| 0x07 | Funktion abgebrochen wegen anderer Fehlereinträge |
| 0x08 | Funktion vollständig durchlaufen, kein Fehler |
| 0x09 | Funktion vollständig durchlaufen, Fehler erkannt |
| 0xXY | Status Systemtest KAT kann nicht ausgegeben werden |

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
