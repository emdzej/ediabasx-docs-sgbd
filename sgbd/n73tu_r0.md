# n73tu_r0.prg

- Jobs: [193](#jobs)
- Tables: [38](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MED9.2.2 fuer NG-Motoren  |
| ORIGIN | BMWAG EA-740 Markus_Lorch |
| REVISION | 1.015 |
| AUTHOR | BMW EA-41 Roth, ValleyForge-T.I.S. EA-41 Wieser, P+Z EA-740 Ber |
| COMMENT | SGBD fuer Master-SG MED9.2.2 (PST 744AJ0AX) |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
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
- [DATA_ID_LESEN](#job-data-id-lesen) - Auslesen der Data-ID (PST+DS) des SG
- [IDENT_AIF](#job-ident-aif) - (1) Auslesen der Identdaten mit KWP2000: $1A ReadECUIdentification (2) Auslesen des Anwender Informations Feldes mit KWP2000: $23 ReadMemoryByAddress (3) =Standard Flashjob
- [FS_LESEN_LANG](#job-fs-lesen-lang) - Fehlerspeicher auslesen
- [FS_HEX_LESEN](#job-fs-hex-lesen) - Fehlerspeicher auslesen als Hex Dump
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - Stellgliedansteuerung E-Luefter
- [STEUERN_E_LUEFTER_AUS](#job-steuern-e-luefter-aus) - Stop Stellgliedansteuerung E-Luefter
- [STEUERN_KFK](#job-steuern-kfk) - Stellgliedansteuerung Kennfeldkühlung
- [STEUERN_KFK_AUS](#job-steuern-kfk-aus) - Stop Stellgliedansteuerung Kennfeldkühlung
- [STEUERN_EKP](#job-steuern-ekp) - Stellgliedansteuerung EKP
- [STEUERN_EKP_AUS](#job-steuern-ekp-aus) - Stellgliedansteuerung EKP stoppen
- [STEUERN_DMTLP](#job-steuern-dmtlp) - Stellgliedansteuerung DMTL-Pumpe
- [STEUERN_DMTLP_AUS](#job-steuern-dmtlp-aus) - Stop Stellgliedansteuerung DMTL-Pumpe
- [STEUERN_DMTLV](#job-steuern-dmtlv) - Stellgliedansteuerung DMTL-Ventil
- [STEUERN_DMTLV_AUS](#job-steuern-dmtlv-aus) - Stop Stellgliedansteuerung DMTL-Ventil
- [STEUERN_DMTLH](#job-steuern-dmtlh) - Stellgliedansteuerung DMTL-Heizung
- [STEUERN_DMTLH_AUS](#job-steuern-dmtlh-aus) - Stop Stellgliedansteuerung DMTL-Heizung
- [STEUERN_HLS1](#job-steuern-hls1) - Stellgliedansteuerung Lambdasondenheizung 1 (LS vor Kat)
- [STEUERN_HLS1_AUS](#job-steuern-hls1-aus) - Stop Stellgliedansteuerung Lambdasondenheizung 1 (LS vor Kat)
- [STEUERN_HLS2](#job-steuern-hls2) - Stellgliedansteuerung Lambdasondenheizung 1 (LS hinter Kat)
- [STEUERN_HLS2_AUS](#job-steuern-hls2-aus) - Stop Stellgliedansteuerung Lambdasondenheizung 2 (LS hinter Kat)
- [STEUERN_RBVE](#job-steuern-rbve) - Stellgliedansteuerung Rücklaufbelüftungsventil
- [STEUERN_RBVE_AUS](#job-steuern-rbve-aus) - Stellgliedansteuerung Rücklaufbelüftungsventil
- [STEUERN_EBL](#job-steuern-ebl) - Stellgliedansteuerung E-Box-Lüfter
- [STEUERN_EBL_AUS](#job-steuern-ebl-aus) - Stop Stellgliedansteuerung E-Box-Lüfter
- [STEUERN_AGK](#job-steuern-agk) - Stellgliedansteuerung Abgasklappe
- [STEUERN_AGK_AUS](#job-steuern-agk-aus) - Stop Stellgliedansteuerung Abgasklappe
- [STEUERN_AGK_INV](#job-steuern-agk-inv) - Stellgliedansteuerung Abgasklappe invertiert
- [STEUERN_AGK_INV_AUS](#job-steuern-agk-inv-aus) - Stop invertierte Stellgliedansteuerung Abgasklappe
- [STEUERN_ANSKL](#job-steuern-anskl) - Stellgliedansteuerung Ansaugklappe
- [STEUERN_ANSKL_AUS](#job-steuern-anskl-aus) - Stop Stellgliedansteuerung Abgasklappe
- [STEUERN_RAVE](#job-steuern-rave) - Stellgliedansteuerung Rücklaufabsperrventil
- [STEUERN_RAVE_AUS](#job-steuern-rave-aus) - Stop Stellgliedansteuerung Rücklaufabsperrventil
- [STEUERN_TEV](#job-steuern-tev) - Stellgliedansteuerung Tankentlüftungsventil
- [STEUERN_TEV_AUS](#job-steuern-tev-aus) - Stop Stellgliedansteuerung Tankentlüftungsventil
- [STEUERN_VVT](#job-steuern-vvt) - Stellgliedansteuerung VVT Für die VVT-Ansteuerung gibt es 2 Möglichkeiten: (1) Anst. durch Verstellung der Excenterwelle auf einen vorgegebenen Winkel (2) Anst. durch Fahren einer Rampe von Position f. LL -&gt; Maxhub -&gt; LL
- [STEUERN_VVT_AUS](#job-steuern-vvt-aus) - Stop Stellgliedansteuerung VVT
- [STEUERN_VVT_ENABLE](#job-steuern-vvt-enable) - Generierung eines Testsignals auf der VVT-Enable-Leitung
- [STEUERN_VVT_ENABLE_AUS](#job-steuern-vvt-enable-aus) - Testsignal von VVT-Enable-Leitung zurücknehmen
- [STEUERN_VANOS_EINLASS](#job-steuern-vanos-einlass) - Stellgliedansteuerung Einlass-VANOS
- [STEUERN_VANOS_EINLASS_AUS](#job-steuern-vanos-einlass-aus) - Stop Stellgliedansteuerung Einlass-VANOS
- [STEUERN_VANOS_AUSLASS](#job-steuern-vanos-auslass) - Stellgliedansteuerung Auslass-VANOS
- [STEUERN_VANOS_AUSLASS_AUS](#job-steuern-vanos-auslass-aus) - Stop Stellgliedansteuerung Auslass-VANOS
- [STEUERN_MIL](#job-steuern-mil) - Stellgliedansteuerung MIL (Lampe Motorfehler)
- [STEUERN_MIL_AUS](#job-steuern-mil-aus) - Stop Stellgliedansteuerung MIL (Lampe Motorfehler)
- [STEUERN_EML](#job-steuern-eml) - Stellgliedansteuerung EML (Lampe Fehler Gesamtfahrzeug)
- [STEUERN_EML_AUS](#job-steuern-eml-aus) - Stop Stellgliedansteuerung EML (Lampe Fehler Gesamtfahrzeug)
- [STATUS_VARIANTE](#job-status-variante) - Auslesen der Varianten
- [STEUERN_VARIANTE](#job-steuern-variante) - Löschen der Varianten
- [STEUERN_ADAPTIONEN_LOESCHEN](#job-steuern-adaptionen-loeschen) - Selektives Löschen der Adaptionswerte
- [STATUS_KVA](#job-status-kva) - Auslesen Faktor kva_korr
- [STEUERN_KVA](#job-steuern-kva) - Programmieren Korrekturfaktor Kraftstoffverbrauch kva_korr
- [STATUS_CO_ABGLEICH](#job-status-co-abgleich) - Abgleichwert Korrektur CO-Einstellung lesen
- [STEUERN_CO_ABGLEICH_VERSTELLEN](#job-steuern-co-abgleich-verstellen) - Abgleichwert Korrektur CO-Einstellung verstellen
- [STEUERN_CO_ABGLEICH_PROGRAMMIEREN](#job-steuern-co-abgleich-programmieren) - Abgleichwert Korrektur CO-Einstellung programmieren
- [STATUS_LLABG](#job-status-llabg) - Auslesen LL-Abgleichswerte
- [STEUERN_LLABG](#job-steuern-llabg) - LL-Abgleichswerte vorgeben
- [STEUERN_LLABG_PROG](#job-steuern-llabg-prog) - LL-Abgleichswerte programmieren
- [STEUERN_EVAUSBL](#job-steuern-evausbl) - Ausblenden von EVs
- [STEUERN_EVAUSBL_AUS](#job-steuern-evausbl-aus) - Ausblenden von EVs beenden
- [START_SYSTEMCHECK_TEV_FUNC](#job-start-systemcheck-tev-func) - Anstoßen Systemtest TEV
- [STATUS_SYSTEMCHECK_TEV_FUNC](#job-status-systemcheck-tev-func) - Auslesen Status Systemtest TEV
- [STOP_SYSTEMCHECK_TEV_FUNC](#job-stop-systemcheck-tev-func) - Stop Systemtest TEV
- [START_SYSTEMCHECK_LLERH](#job-start-systemcheck-llerh) - Anstoßen Systemtest LL-Erhöhung
- [STATUS_SYSTEMCHECK_LLERH](#job-status-systemcheck-llerh) - Auslesen Status Systemtest LL-Erhöhung
- [STOP_SYSTEMCHECK_LLERH](#job-stop-systemcheck-llerh) - Systemtest LL-Erhöhung beenden
- [STEUERN_VVT_ANSCHLAG](#job-steuern-vvt-anschlag) - Anstoßen Diagnose 'VVT-Anschläge lernen'
- [STATUS_VVT_ANSCHLAG](#job-status-vvt-anschlag) - Auslesen Status Diagnose 'VVT-Anschläge lernen'
- [STOP_VVT_ANSCHLAG](#job-stop-vvt-anschlag) - Diagnose 'VVT-Anschläge lernen' beenden
- [START_SYSTEMCHECK_DMTL](#job-start-systemcheck-dmtl) - Anstoßen Tankdiagnose DMTL
- [STATUS_SYSTEMCHECK_DMTL](#job-status-systemcheck-dmtl) - Status Tankdiagnose DMTL
- [STOP_SYSTEMCHECK_DMTL](#job-stop-systemcheck-dmtl) - Tankdiagnose DMTL beenden
- [START_SYSTEMCHECK_LSU](#job-start-systemcheck-lsu) - Anstoßen LSU-Systemdiagnose
- [STATUS_SYSTEMCHECK_LSU](#job-status-systemcheck-lsu) - Status Systemdiagnose LSU
- [STOP_SYSTEMCHECK_LSU](#job-stop-systemcheck-lsu) - LSU-Systemdiagnose beenden
- [STATUS_DIAGNOSE_LSV](#job-status-diagnose-lsv) - Auslesen Zyklusflags Z_LSV
- [START_SYSTEMCHECK_KAT](#job-start-systemcheck-kat) - Anstoßen Kurztest KAT
- [STATUS_SYSTEMCHECK_KAT](#job-status-systemcheck-kat) - Status Kurztest KAT
- [STOP_SYSTEMCHECK_KAT](#job-stop-systemcheck-kat) - Kurztest KAT beenden
- [START_SYSTEMCHECK_LSH](#job-start-systemcheck-lsh) - Anstoßen Systemttest LS hinter KAT
- [STATUS_SYSTEMCHECK_LSH](#job-status-systemcheck-lsh) - Status Systemttest LS hinter KAT
- [STOP_SYSTEMCHECK_LSH](#job-stop-systemcheck-lsh) - Systemttest LS hinter KAT beenden
- [START_SYSTEMCHECK_GEMISCHADAPT_SPERR](#job-start-systemcheck-gemischadapt-sperr) - Anstoßen Systemttest 'Gemischadaption sperren'
- [STOP_SYSTEMCHECK_GEMISCHADAPT_SPERR](#job-stop-systemcheck-gemischadapt-sperr) - Systemttest 'Gemischadaption sperren' beenden
- [START_SYSTEMCHECK_GRUNDADAPT](#job-start-systemcheck-grundadapt) - Anstoßen Systemttest 'Grundadaption starten'
- [STATUS_SYSTEMCHECK_GRUNDADAPT](#job-status-systemcheck-grundadapt) - Status Systemttest 'Grundadaption starten'
- [STOP_SYSTEMCHECK_GRUNDADAPT](#job-stop-systemcheck-grundadapt) - Systemttest 'Grundadaption starten' beenden
- [START_SYSTEMCHECK_LAMBDA_AUS](#job-start-systemcheck-lambda-aus) - Systemttest 'Lambdaregelung aus' anstoßen
- [STATUS_SYSTEMCHECK_LAMBDA_AUS](#job-status-systemcheck-lambda-aus) - Status Systemttest 'Lambdaregelung aus'
- [STOP_SYSTEMCHECK_LAMBDA_AUS](#job-stop-systemcheck-lambda-aus) - Systemttest 'Lambdaregelung aus' beenden
- [START_SYSTEMCHECK_KOMPRESSION](#job-start-systemcheck-kompression) - Kompressionstest anstoßen
- [STOP_SYSTEMCHECK_KOMPRESSION](#job-stop-systemcheck-kompression) - Kompressionstest beenden
- [STEUERN_POWER_DOWN](#job-steuern-power-down) - Anforderung Power Down Mode
- [STEUERN_ZWANG_RAMBACKUP](#job-steuern-zwang-rambackup) - Zwangssichern der RAM-Backup-Werte
- [RAM_BACKUP](#job-ram-backup) - Loeschen der RAM-Backup-Werte
- [RAM_LESEN](#job-ram-lesen) - Auslesen von beliebigen RAM-Zellen
- [STATUS_RBM_MODE9](#job-status-rbm-mode9) - Lesen der RBM-Werte Mode9
- [STATUS_RBM_BLOCK1](#job-status-rbm-block1) - Lesen der RBM-Werte Block1
- [STATUS_RBM_BLOCK2](#job-status-rbm-block2) - Lesen der RBM-Werte Block2
- [STATUS_MESSWERTE](#job-status-messwerte) - Auslesen des allgemeinen Messwerteblocks
- [STATUS_MESSWERTE_DI](#job-status-messwerte-di) - Auslesen der DI-Messwerte
- [STATUS_BATTERIEINTEGRATOR](#job-status-batterieintegrator) - Auslesen des Batterie-Ladezustands
- [STATUS_SCHALTERSTATI](#job-status-schalterstati) - Auslesen der Schalterstati
- [STATUS_FUNKTIONSSTATI](#job-status-funktionsstati) - Auslesen der Funktionsstati
- [STATUS_DIGITAL](#job-status-digital) - Auslesen der Funktions- und Schalterstati
- [STATUS_LAUFUNRUHE](#job-status-laufunruhe) - Auslesen der Laufunruhewerte
- [STATUS_DKHFM](#job-status-dkhfm) - Auslesen der DK/HFM-Abgleichswerte
- [STATUS_GEMISCH](#job-status-gemisch) - Auslesen der Gemischwerte
- [STATUS_AUSGAENGE](#job-status-ausgaenge) - Auslesen der Ausgänge
- [STATUS_NWGADAPTION](#job-status-nwgadaption) - Auslesen der NWG-Adaptionen
- [STATUS_READINESS](#job-status-readiness) - Auslesen der NWG-Adaptionen
- [STATUS_FGR](#job-status-fgr) - Auslesen des FGR-Status
- [STATUS_VVT](#job-status-vvt) - Auslesen der VVT-Messwerte
- [STATUS_MINHUB](#job-status-minhub) - Auslesen des Minhub-Wertes
- [STATUS_BETRIEBSSTUNDENZAEHLER](#job-status-betriebsstundenzaehler) - Auslesen des Betriebsstundenzähler-Status
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - Auslesen der Motortemperatur
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Auslesen der Motordrehzahl
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - Auslesen der Ansauglufttemperatur
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - Auslesen des Luftmassenstroms
- [STATUS_L_SONDE](#job-status-l-sonde) - Auslesen der Lambdasondenspannung 1
- [STATUS_L_SONDE_H](#job-status-l-sonde-h) - Auslesen der Lambdasondenspannung 1
- [STATUS_INT](#job-status-int) - Auslesen des Lambdaregler-Ausgangs
- [STATUS_ADD](#job-status-add) - Auslesen der additiven Lambdaregelung
- [STATUS_MUL](#job-status-mul) - Auslesen der multipikativen Lambdaregelung
- [STATUS_UBATT](#job-status-ubatt) - Auslesen der Batteriespannung
- [STATUS_GEBERRAD_ADAPTION](#job-status-geberrad-adaption) - Auslesen der NWG-Adaption
- [STATUS_PWG_POTI_SPANNUNG](#job-status-pwg-poti-spannung) - Auslesen des Pedalwertgeber-Status
- [STATUS_ADC](#job-status-adc) - Auslesen der ADC-Werte
- [STATUS_FASTA1](#job-status-fasta1) - Auslesen FASTA-Messwertblock 1
- [STATUS_FASTA2](#job-status-fasta2) - Auslesen FASTA-Messwertblock 2
- [STATUS_FASTA3](#job-status-fasta3) - Auslesen FASTA-Messwertblock 3
- [STATUS_FASTA4](#job-status-fasta4) - Auslesen FASTA-Messwertblock 4
- [STATUS_FASTA5](#job-status-fasta5) - Auslesen FASTA-Messwertblock 5
- [STATUS_FASTA6](#job-status-fasta6) - Auslesen FASTA-Messwertblock 6
- [STATUS_FASTA7](#job-status-fasta7) - Auslesen FASTA-Messwertblock 7
- [EWS_STARTWERT](#job-ews-startwert) - EWS-Startwertinitialisierung
- [EWS_EMPFANG](#job-ews-empfang) - EWS-Empfangsstatus auslesen
- [WECHSELCODE_SYNC_DME](#job-wechselcode-sync-dme) - EWS zuruecksetzen
- [START_ZWDIAG](#job-start-zwdiag) - CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Start-Routine ZWDIAG (0x31 3A)
- [STATUS_ZWDIAG](#job-status-zwdiag) - CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Status-Routine ZWDIAG (0x33 3A)
- [STOP_ZWDIAG](#job-stop-zwdiag) - CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Stop-Routine ZWDIAG (0x32 3A)
- [STATUS_ENERGIESPARMODE](#job-status-energiesparmode) - 0x22100A STATUS_ENERGIESPARMODE Status Energiesparmode Aktivierung: Klemme 15 = EIN
- [STATUS_CODIERUNG_OEL](#job-status-codierung-oel) - 0x223200 STATUS_CODIERUNG_OEL Codierung fuer Oelwechselintervall auslesen Aktivierung: Klemme 15 = EIN
- [STATUS_ETKH](#job-status-etkh) - 0x2CF099 und 0x2CF19A STATUS_ETKH Auslesen der Quotient Zündwinkelwirkungsgrad-Fehlerintegral Aktivierung: Klemme 15 = EIN

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
| AVAI_BOS_WERT_H2 | int | Verfuegbarkeit H2 in %, für Prüfablauf Bandende |
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

<a id="job-data-id-lesen"></a>
### DATA_ID_LESEN

Auslesen der Data-ID (PST+DS) des SG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| DATA_ID | string | ASCII-String fuer Data-ID |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-aif"></a>
### IDENT_AIF

(1) Auslesen der Identdaten mit KWP2000: $1A ReadECUIdentification (2) Auslesen des Anwender Informations Feldes mit KWP2000: $23 ReadMemoryByAddress (3) =Standard Flashjob

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
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
| ID_LIEF_TEXT | string | Lieferanten-Text |
| ID_SW_NR_MCV | string | Softwarenummer (message catalogue version) |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| ID_SW_NR_OSV | string | Softwarenummer (operating system version) |
| ID_SW_NR_RES | string | Softwarenummer (reserved - currently unused) |
| _TEL_AUFTRAG_IDENT | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_IDENT | binary | Hex-Antwort von SG |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ANZ_DATEN | int | Groesse des AIF-Eintrags |
| AIF_ADRESSE_HIGH | int | AIF Adresse des AIF, High-Word |
| AIF_ADRESSE_LOW | int | AIF Adresse des AIF, Low-Word |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | long | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |
| AIF_GROESSE | int | Groesse des AIF |
| _TEL_AUFTRAG_AIF | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_AIF | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-lang"></a>
### FS_LESEN_LANG

Fehlerspeicher auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLERNR | int | Eingabe Fehlerortnummer des auszulesenden Fehlers Eingabe in hex- oder dez-Format |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| F_ANZ_INT | int | Anzahl der eingetragenen Fehler im Fehlerspeicher |
| F_ORT_NR | long | Fehlerort in Dezimaldarstellung |
| F_ORT_TEXT | string | Text zum Fehlerort |
| F_SYMPTOM_NR | int | ID für die Grundfehlerart (1=max, 2=min, 4=sig, 8=plaus) |
| F_SYMPTOM_TEXT | string | Interpretation der Fehlerart |
| F_READY_NR | int | Gibt an, ob Readiness gesetzt |
| F_READY_TEXT | string | Text zur Readiness |
| F_VORHANDEN_NR | int | ID zum Eintragstatus des Fehlers |
| F_VORHANDEN_TEXT | string | Text zum Eintragsstatus (bzgl. Entprellung) des Fehlers |
| F_WARNUNG_NR | int | Nummer fuer MIL EIN |
| F_WARNUNG_TEXT | string | gibt an, ob die MIL angesteuert wird |
| F_ART_ERW_WERT | int | FehlerarterweiterungsByte als integer |
| F_ZYKLUS_FLAG | string | gibt an, ob Zyklus-Flag gesetzt worden ist |
| F_AKTIV_FLAG | string | gibt an, ob Diagnose läuft |
| F_STOP_FLAG | string | gibt an, ob Stopbedingungen vorliegen |
| F_ERROR_FLAG | string | zeigt Error-Flag an |
| F_MIL_FLAG | string | zeigt den MIL-Status an |
| F_ENTPRELL_FLAG | string | gibt den MIL-Entprellstatus an |
| F_CLA | int | Fehlerklasse |
| F_FLC | int | Wert Entprellvorgaenge FLC |
| F_HLC | int | Wert Entprellvorgaenge HLC |
| F_LZ | int | Wert Löschvorgänge DLC |
| F_TSF | real | Wert Schwerezähler TSF |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_KM_FIRST | string | Km-Stand bei Erstauftreten des Fehlers (Wert+Einheit) |
| F_KM_NEXT | string | Km-Stand beim zweiten Auftreten des Fehlers (Wert+Einheit) |
| F_KM_LAST | string | Km-Stand beim letzten Auftreten des Fehlers (Wert+Einheit) |
| F_KM_FIRST_WERT | real | Km-Stand bei Erstauftreten des Fehlers (nur Wert) |
| F_KM_NEXT_WERT | real | Km-Stand beim zweiten Auftreten des Fehlers (nur Wert) |
| F_KM_LAST_WERT | real | Km-Stand beim letzten Auftreten des Fehlers (nur Wert) |
| F_UW1_APP_NR | int | Applikationswert der 1. Umweltbedingung (UW1) |
| F_UW2_APP_NR | int | Applikationswert der 2. Umweltbedingung (UW2) |
| F_UW3_APP_NR | int | Applikationswert der 3. Umweltbedingung (UW3) |
| F_UW4_APP_NR | int | Applikationswert der 4. Umweltbedingung (UW4) |
| F_UW1_NR | int | Index UW1 bei Ersterkennung des Fehlers |
| F_UW1_TEXT | string | Text zur UW1 bei Ersterkennung des Fehlers |
| F_UW1_WERT | real | Physikalische Wert der UW1 bei Ersterkennung des Fehlers |
| F_UW1_EINH | string | Physikalische Einheit der UW1 bei Ersterkennung des Fehlers |
| F_UW2_NR | int | Index UW2 bei Ersterkennung des Fehlers |
| F_UW2_TEXT | string | Text zur UW2 bei Ersterkennung des Fehlers |
| F_UW2_WERT | real | Physikalische Wert der UW2 bei Ersterkennung des Fehlers |
| F_UW2_EINH | string | Physikalische Einheit der UW2 bei Ersterkennung des Fehlers |
| F_UW3_NR | int | Index UW3 bei Ersterkennung des Fehlers |
| F_UW3_TEXT | string | Text zur UW3 bei Ersterkennung des Fehlers |
| F_UW3_WERT | real | Physikalische Wert der UW3 bei Ersterkennung des Fehlers |
| F_UW3_EINH | string | Physikalische Einheit der UW3 bei Ersterkennung des Fehlers |
| F_UW4_NR | int | Index UW4 bei Ersterkennung des Fehlers |
| F_UW4_TEXT | string | Text zur UW4 bei Ersterkennung des Fehlers |
| F_UW4_WERT | real | Physikalische Wert der UW4 bei Ersterkennung des Fehlers |
| F_UW4_EINH | string | Physikalische Einheit der UW4 bei Ersterkennung des Fehlers |
| F_UW5_NR | int | Index UW1 bei zweiter Erkennung des Fehlers |
| F_UW5_TEXT | string | Text zur UW1 bei zweiter Erkennung des Fehlers |
| F_UW5_WERT | real | Physikalische Wert der UW1 bei zweiter Erkennung des Fehlers |
| F_UW5_EINH | string | Physikalische Einheit der UW1 bei zweiter Erkennung des Fehlers |
| F_UW6_NR | int | Index UW2 bei zweiter Erkennung des Fehlers |
| F_UW6_TEXT | string | Text zur UW2 bei zweiter Erkennung des Fehlers |
| F_UW6_WERT | real | Physikalische Wert der UW2 bei zweiter Erkennung des Fehlers |
| F_UW6_EINH | string | Physikalische Einheit der UW2 bei zweiter Erkennung des Fehlers |
| F_UW7_NR | int | Index UW3 bei zweiter Erkennung des Fehlers |
| F_UW7_TEXT | string | Text zur UW3 bei zweiter Erkennung des Fehlers |
| F_UW7_WERT | real | Physikalische Wert der UW3 bei zweiter Erkennung des Fehlers |
| F_UW7_EINH | string | Physikalische Einheit der UW3 bei zweiter Erkennung des Fehlers |
| F_UW8_NR | int | Index UW4 bei zweiter Erkennung des Fehlers |
| F_UW8_TEXT | string | Text zur UW4 bei zweiter Erkennung des Fehlers |
| F_UW8_WERT | real | Physikalische Wert der UW4 bei zweiter Erkennung des Fehlers |
| F_UW8_EINH | string | Physikalische Einheit der UW4 bei zweiter Erkennung des Fehlers |
| F_UW9_NR | int | Index UW1 bei letzter Erkennung des Fehlers |
| F_UW9_TEXT | string | Text zur UW1 bei letzter Erkennung des Fehlers |
| F_UW9_WERT | real | Physikalische Wert der UW1 bei letzter Erkennung des Fehlers |
| F_UW9_EINH | string | Physikalische Einheit der UW1 bei letzter Erkennung des Fehlers |
| F_UW10_NR | int | Index UW2 bei letzter Erkennung des Fehlers |
| F_UW10_TEXT | string | Text zur UW2 bei letzter Erkennung des Fehlers |
| F_UW10_WERT | real | Physikalische Wert der UW2 bei letzter Erkennung des Fehlers |
| F_UW10_EINH | string | Physikalische Einheit der UW2 bei letzter Erkennung des Fehlers |
| F_UW11_NR | int | Index UW3 bei letzter Erkennung des Fehlers |
| F_UW11_TEXT | string | Text zur UW3 bei letzter Erkennung des Fehlers |
| F_UW11_WERT | real | Physikalische Wert der UW3 bei letzter Erkennung des Fehlers |
| F_UW11_EINH | string | Physikalische Einheit der UW3 bei letzter Erkennung des Fehlers |
| F_UW12_NR | int | Index UW4 bei letzter Erkennung des Fehlers |
| F_UW12_TEXT | string | Text zur UW4 bei letzter Erkennung des Fehlers |
| F_UW12_WERT | real | Physikalische Wert der UW4 bei letzter Erkennung des Fehlers |
| F_UW12_EINH | string | Physikalische Einheit der UW4 bei letzter Erkennung des Fehlers |
| F_FF1_WERT | int | Wert der UW1 des Freeze-Frame |
| F_FF1_TEXT | string | Text zur UW1 des Freeze-Frame |
| F_FF1_BESCH | string | Beschreibung UW1 des Freeze-Frame |
| F_FF3_WERT | real | Physikalischer Wert der UW3 des Freeze-Frame |
| F_FF3_EINH | string | Physikalische Einheit der UW3 des Freeze-Frame |
| F_FF3_TEXT | string | Text zur UW3 des Freeze-Frame |
| F_FF4_WERT | real | Physikalischer Wert der UW4 des Freeze-Frame |
| F_FF4_EINH | string | Physikalische Einheit der UW4 des Freeze-Frame |
| F_FF4_TEXT | string | Text zur UW4 des Freeze-Frame |
| F_FF5_WERT | real | Physikalischer Wert der UW5 des Freeze-Frame |
| F_FF5_EINH | string | Physikalische Einheit der UW5 des Freeze-Frame |
| F_FF5_TEXT | string | Text zur UW5 des Freeze-Frame |
| F_FF6_WERT | real | Physikalischer Wert der UW6 des Freeze-Frame |
| F_FF6_EINH | string | Physikalische Einheit der UW6 des Freeze-Frame |
| F_FF6_TEXT | string | Text zur UW6 des Freeze-Frame |
| F_FF10_WERT | real | Physikalischer Wert der UW10 des Freeze-Frame |
| F_FF10_EINH | string | Physikalische Einheit der UW10 des Freeze-Frame |
| F_FF10_TEXT | string | Text zur UW10 des Freeze-Frame |
| F_FF11_WERT | real | Physikalischer Wert der UW11 des Freeze-Frame |
| F_FF11_EINH | string | Physikalische Einheit der UW11 des Freeze-Frame |
| F_FF11_TEXT | string | Text zur UW11 des Freeze-Frame |
| F_HFK | int | Fehlerhäufigkeit |
| F_P_CODE | string | P-Code des eingetragenen Fehlers |
| F_HEX_CODE | binary | Hexdump des Fehlers |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-hex-lesen"></a>
### FS_HEX_LESEN

Fehlerspeicher auslesen als Hex Dump

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLERNR | int | Eingabe Fehlerortnummer des auszulesenden Fehlers Eingabe in hex- oder dez-Format |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| F_ANZ_INT | int | Anzahl der eingetragenen Fehler im Fehlerspeicher |
| FEHLER_NR_TEXT | string | Fehlernummer im Speicher |
| FS_ZEILE1 | string | ersten 10 Byte des Fehlerspeichers als Dump |
| FS_ZEILE2 | string | nächsten 10 Byte des Fehlerspeichers als Dump |
| FS_ZEILE3 | string | nächsten 10 Byte des Fehlerspeichers als Dump |
| FS_ZEILE4 | string | nächsten 10 Byte des Fehlerspeichers als Dump |
| FS_ZEILE5 | string | nächsten 10 Byte des Fehlerspeichers als Dump |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

Stellgliedansteuerung E-Luefter

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTRATE | int | Eingabe Ansteuerverhältnis (0%...100%) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-e-luefter-aus"></a>
### STEUERN_E_LUEFTER_AUS

Stop Stellgliedansteuerung E-Luefter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kfk"></a>
### STEUERN_KFK

Stellgliedansteuerung Kennfeldkühlung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kfk-aus"></a>
### STEUERN_KFK_AUS

Stop Stellgliedansteuerung Kennfeldkühlung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

Stellgliedansteuerung EKP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ekp-aus"></a>
### STEUERN_EKP_AUS

Stellgliedansteuerung EKP stoppen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlp"></a>
### STEUERN_DMTLP

Stellgliedansteuerung DMTL-Pumpe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlp-aus"></a>
### STEUERN_DMTLP_AUS

Stop Stellgliedansteuerung DMTL-Pumpe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlv"></a>
### STEUERN_DMTLV

Stellgliedansteuerung DMTL-Ventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlv-aus"></a>
### STEUERN_DMTLV_AUS

Stop Stellgliedansteuerung DMTL-Ventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlh"></a>
### STEUERN_DMTLH

Stellgliedansteuerung DMTL-Heizung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtlh-aus"></a>
### STEUERN_DMTLH_AUS

Stop Stellgliedansteuerung DMTL-Heizung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls1"></a>
### STEUERN_HLS1

Stellgliedansteuerung Lambdasondenheizung 1 (LS vor Kat)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls1-aus"></a>
### STEUERN_HLS1_AUS

Stop Stellgliedansteuerung Lambdasondenheizung 1 (LS vor Kat)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls2"></a>
### STEUERN_HLS2

Stellgliedansteuerung Lambdasondenheizung 1 (LS hinter Kat)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hls2-aus"></a>
### STEUERN_HLS2_AUS

Stop Stellgliedansteuerung Lambdasondenheizung 2 (LS hinter Kat)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-rbve"></a>
### STEUERN_RBVE

Stellgliedansteuerung Rücklaufbelüftungsventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-rbve-aus"></a>
### STEUERN_RBVE_AUS

Stellgliedansteuerung Rücklaufbelüftungsventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ebl"></a>
### STEUERN_EBL

Stellgliedansteuerung E-Box-Lüfter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ebl-aus"></a>
### STEUERN_EBL_AUS

Stop Stellgliedansteuerung E-Box-Lüfter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-agk"></a>
### STEUERN_AGK

Stellgliedansteuerung Abgasklappe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-agk-aus"></a>
### STEUERN_AGK_AUS

Stop Stellgliedansteuerung Abgasklappe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-agk-inv"></a>
### STEUERN_AGK_INV

Stellgliedansteuerung Abgasklappe invertiert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-agk-inv-aus"></a>
### STEUERN_AGK_INV_AUS

Stop invertierte Stellgliedansteuerung Abgasklappe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-anskl"></a>
### STEUERN_ANSKL

Stellgliedansteuerung Ansaugklappe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-anskl-aus"></a>
### STEUERN_ANSKL_AUS

Stop Stellgliedansteuerung Abgasklappe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-rave"></a>
### STEUERN_RAVE

Stellgliedansteuerung Rücklaufabsperrventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-rave-aus"></a>
### STEUERN_RAVE_AUS

Stop Stellgliedansteuerung Rücklaufabsperrventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

Stellgliedansteuerung Tankentlüftungsventil

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANSTEUERRATE | int | Tastverhältnis (0%...100%) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tev-aus"></a>
### STEUERN_TEV_AUS

Stop Stellgliedansteuerung Tankentlüftungsventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt"></a>
### STEUERN_VVT

Stellgliedansteuerung VVT Für die VVT-Ansteuerung gibt es 2 Möglichkeiten: (1) Anst. durch Verstellung der Excenterwelle auf einen vorgegebenen Winkel (2) Anst. durch Fahren einer Rampe von Position f. LL -&gt; Maxhub -&gt; LL

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WINKEL | int | -&gt; Bei Verstellung über Winkel =&gt; WINKEL = Vorgabewert (0..180) / RAMPE = 0 -&gt; Bei Verstellung über Rampe =&gt; WINKEL = beliebig wählbar (wird eh nicht ausgewertet) RAMPE = beliebig außer '0' wählbar, da eine fest definierte Rampe gefahren wird |
| RAMPE | int | -&gt; Bei Verstellung über Winkel =&gt; WINKEL = Vorgabewert (0..180) / RAMPE = 0 -&gt; Bei Verstellung über Rampe =&gt; WINKEL = beliebig wählbar (wird eh nicht ausgewertet) RAMPE = beliebig außer '0' wählbar, da eine fest definierte Rampe gefahren wird |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt-aus"></a>
### STEUERN_VVT_AUS

Stop Stellgliedansteuerung VVT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt-enable"></a>
### STEUERN_VVT_ENABLE

Generierung eines Testsignals auf der VVT-Enable-Leitung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt-enable-aus"></a>
### STEUERN_VVT_ENABLE_AUS

Testsignal von VVT-Enable-Leitung zurücknehmen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vanos-einlass"></a>
### STEUERN_VANOS_EINLASS

Stellgliedansteuerung Einlass-VANOS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WINKEL | int | Verstellwinkel Vanos (-102....+102) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vanos-einlass-aus"></a>
### STEUERN_VANOS_EINLASS_AUS

Stop Stellgliedansteuerung Einlass-VANOS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vanos-auslass"></a>
### STEUERN_VANOS_AUSLASS

Stellgliedansteuerung Auslass-VANOS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| WINKEL | int | Verstellwinkel Vanos (-102....+102) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vanos-auslass-aus"></a>
### STEUERN_VANOS_AUSLASS_AUS

Stop Stellgliedansteuerung Auslass-VANOS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mil"></a>
### STEUERN_MIL

Stellgliedansteuerung MIL (Lampe Motorfehler)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mil-aus"></a>
### STEUERN_MIL_AUS

Stop Stellgliedansteuerung MIL (Lampe Motorfehler)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eml"></a>
### STEUERN_EML

Stellgliedansteuerung EML (Lampe Fehler Gesamtfahrzeug)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eml-aus"></a>
### STEUERN_EML_AUS

Stop Stellgliedansteuerung EML (Lampe Fehler Gesamtfahrzeug)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-variante"></a>
### STATUS_VARIANTE

Auslesen der Varianten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
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

<a id="job-steuern-variante"></a>
### STEUERN_VARIANTE

Löschen der Varianten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_VARIANTE_LOESCHEN | string | "OK", wenn Löschen erfolgreich war / andernfalls "nicht OK" |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-adaptionen-loeschen"></a>
### STEUERN_ADAPTIONEN_LOESCHEN

Selektives Löschen der Adaptionswerte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE_1 | int | siehe LH 1 430 227, setzt REYO_01 bitweise |
| AUSWAHLBYTE_2 | int | siehe LH 1 430 227, setzt REYO_02 bitweise |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kva"></a>
### STATUS_KVA

Auslesen Faktor kva_korr

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_KVA_WERT | real | Wert von kva_korr (-0.128 ... 0.127) |
| STAT_KVA_EINH | string | Einheit von kva_korr: [%] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kva"></a>
### STEUERN_KVA

Programmieren Korrekturfaktor Kraftstoffverbrauch kva_korr

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KVA_WERT | int | Wertebereich für Eingabeparameter: -128 ... 127 kva_korr = KVA_WERT \ 1000 zB: KVA_WERT = -55   =&gt; kva_korr = -0.055% |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-co-abgleich"></a>
### STATUS_CO_ABGLEICH

Abgleichwert Korrektur CO-Einstellung lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_CO_ABGLEICH_WERT | real | Wert von co_pot |
| STAT_CO_ABGLEICH_EINH | string | Einheit von co_pot [-] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-co-abgleich-verstellen"></a>
### STEUERN_CO_ABGLEICH_VERSTELLEN

Abgleichwert Korrektur CO-Einstellung verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CO_WERT | int | LL-CO-Abgleichswert co_pot |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-co-abgleich-programmieren"></a>
### STEUERN_CO_ABGLEICH_PROGRAMMIEREN

Abgleichwert Korrektur CO-Einstellung programmieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CO_FEST | int | LL-CO-Abgleichswert co_pot |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-llabg"></a>
### STATUS_LLABG

Auslesen LL-Abgleichswerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_DNLLMV_WERT | real | Abgleichswert LL ohne Fahrstufe (dnllmv) |
| STAT_DNLLMV_EINH | string | Einheit von dnllmv: [Upmin] |
| STAT_DNSACMV_WERT | real | Abgleichswert LL mit Klimaanlage ohne Fahrstufe (dnsacmv) |
| STAT_DNSACMV_EINH | string | Einheit von dnsacmv: [Upmin] |
| STAT_DNSLBV_WERT | real | Abgleichswert LL bei niedriger UBatt (dnslbv) |
| STAT_DNSLBV_EINH | string | Einheit von dnslbv: [Upmin] |
| STAT_DNFSACMV_WERT | real | Abgleichswert LL mit Klimaanlage mit Fahrstufe (dnfsacmv) |
| STAT_DNFSACMV_EINH | string | Einheit von dnfsacmv: [Upmin] |
| STAT_DNFSMV_WERT | real | Abgleichswert LL mit Fahrstufe (dnfsmv) |
| STAT_DNFSMV_EINH | string | Einheit von dnfsmv: [Upmin] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-llabg"></a>
### STEUERN_LLABG

LL-Abgleichswerte vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DNLLMV | int | Abgleichswert LL ohne Fahrstufe (dnllmv) |
| DNSACMV | int | Abgleichswert LL mit Klimaanlage ohne Fahrstufe (dnsacmv) |
| DNSLBV | int | Abgleichswert LL bei niedriger UBatt (dnslbv) |
| DNFSACMV | int | Abgleichswert LL mit Klimaanlage mit Fahrstufe (dnfsacmv) |
| DNFSMV | int | Abgleichswert LL mit Fahrstufe (dnfsmv) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-llabg-prog"></a>
### STEUERN_LLABG_PROG

LL-Abgleichswerte programmieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DNLLMV | int | Abgleichswert LL ohne Fahrstufe (dnllmv) |
| DNSACMV | int | Abgleichswert LL mit Klimaanlage ohne Fahrstufe (dnsacmv) |
| DNSLBV | int | Abgleichswert LL bei niedriger UBatt (dnslbv) |
| DNFSACMV | int | Abgleichswert LL mit Klimaanlage mit Fahrstufe (dnfsacmv) |
| DNFSMV | int | Abgleichswert LL mit Fahrstufe (dnfsmv) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-evausbl"></a>
### STEUERN_EVAUSBL

Ausblenden von EVs

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VENTIL_NR | int | gibt Ventile an, die ausgeblendet werden (binaer, jedes Bit ein EV) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-evausbl-aus"></a>
### STEUERN_EVAUSBL_AUS

Ausblenden von EVs beenden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VENTIL_NR | int | gibt Ventile an, die ausgeblendet werden (binaer, jedes Bit ein EV) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-tev-func"></a>
### START_SYSTEMCHECK_TEV_FUNC

Anstoßen Systemtest TEV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-tev-func"></a>
### STATUS_SYSTEMCHECK_TEV_FUNC

Auslesen Status Systemtest TEV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_SYSTEMCHECK_TEV_FUNC_WERT | int | Status-Wert der TEV-Diagnose |
| STAT_SYSTEMCHECK_TEV_FUNC_TEXT | string | Status-Text der TEV-Diagnose |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-tev-func"></a>
### STOP_SYSTEMCHECK_TEV_FUNC

Stop Systemtest TEV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-llerh"></a>
### START_SYSTEMCHECK_LLERH

Anstoßen Systemtest LL-Erhöhung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LL_WERT | int | Eingabewert = 0....2550 wg. Begr. i. PST sind nur Werte zw. 400 u. 1200 sinnvoll |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-llerh"></a>
### STATUS_SYSTEMCHECK_LLERH

Auslesen Status Systemtest LL-Erhöhung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_LLERH_TEXT | string | Status der Diagnose |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-llerh"></a>
### STOP_SYSTEMCHECK_LLERH

Systemtest LL-Erhöhung beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt-anschlag"></a>
### STEUERN_VVT_ANSCHLAG

Anstoßen Diagnose 'VVT-Anschläge lernen'

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vvt-anschlag"></a>
### STATUS_VVT_ANSCHLAG

Auslesen Status Diagnose 'VVT-Anschläge lernen'

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_VVT_ANSCHL_WERT | int | Status-Wert der Diagnose |
| STAT_VVT_ANSCHL_TEXT | string | Status-Text der Diagnose |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-vvt-anschlag"></a>
### STOP_VVT_ANSCHLAG

Diagnose 'VVT-Anschläge lernen' beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-dmtl"></a>
### START_SYSTEMCHECK_DMTL

Anstoßen Tankdiagnose DMTL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-dmtl"></a>
### STATUS_SYSTEMCHECK_DMTL

Status Tankdiagnose DMTL

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
| STAT_IPGLMN_TEXT | string | Minimaler Pumpenstrom Grobleckmessung |
| STAT_IPTREF_TEXT | string | Pumpenstrom Referenzleck |
| STAT_IPTESKF_WERT | real | Pumpenstrom DM-TL gefiltert |
| STAT_IPGLMN_WERT | real | Minimaler Pumpenstrom Grobleckmessung |
| STAT_IPTREF_WERT | real | Pumpenstrom Referenzleck |
| STAT_IPT_EINH | string | Einheit der Stroeme |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-dmtl"></a>
### STOP_SYSTEMCHECK_DMTL

Tankdiagnose DMTL beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-lsu"></a>
### START_SYSTEMCHECK_LSU

Anstoßen LSU-Systemdiagnose

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-lsu"></a>
### STATUS_SYSTEMCHECK_LSU

Status Systemdiagnose LSU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LSU_WERT | int | Status_Wert der LSU-Diagnose (lsunpstat) |
| STAT_LSU_TEXT | string | Status_Text der LSU-Diagnose (lsunpstat) |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-lsu"></a>
### STOP_SYSTEMCHECK_LSU

LSU-Systemdiagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-diagnose-lsv"></a>
### STATUS_DIAGNOSE_LSV

Auslesen Zyklusflags Z_LSV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZLSV_WERT | int | Status Zyklusflag LSV |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-kat"></a>
### START_SYSTEMCHECK_KAT

Anstoßen Kurztest KAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-kat"></a>
### STATUS_SYSTEMCHECK_KAT

Status Kurztest KAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_KAT_WERT | int | Status_Wert der KAT-Diagnose |
| STAT_SYSTEMCHECK_KAT_TEXT | string | Status_Text der KAT-Diagnose |
| STAT_OSCDKTF_WERT | real | gefilt. Speichervermögen des KAT (oscdktf_w) |
| STAT_OSCDKTF_EINH | string | Einheit von oscdktf_w [-] |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-kat"></a>
### STOP_SYSTEMCHECK_KAT

Kurztest KAT beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-lsh"></a>
### START_SYSTEMCHECK_LSH

Anstoßen Systemttest LS hinter KAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-lsh"></a>
### STATUS_SYSTEMCHECK_LSH

Status Systemttest LS hinter KAT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_ZLSH_EIN | int | Status Zyklus-Flag LSH lesen |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-lsh"></a>
### STOP_SYSTEMCHECK_LSH

Systemttest LS hinter KAT beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-gemischadapt-sperr"></a>
### START_SYSTEMCHECK_GEMISCHADAPT_SPERR

Anstoßen Systemttest 'Gemischadaption sperren'

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-gemischadapt-sperr"></a>
### STOP_SYSTEMCHECK_GEMISCHADAPT_SPERR

Systemttest 'Gemischadaption sperren' beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-grundadapt"></a>
### START_SYSTEMCHECK_GRUNDADAPT

Anstoßen Systemttest 'Grundadaption starten'

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-grundadapt"></a>
### STATUS_SYSTEMCHECK_GRUNDADAPT

Status Systemttest 'Grundadaption starten'

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GAD_EIN | int | Status Grundadaption ein (B_gad) |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-grundadapt"></a>
### STOP_SYSTEMCHECK_GRUNDADAPT

Systemttest 'Grundadaption starten' beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-lambda-aus"></a>
### START_SYSTEMCHECK_LAMBDA_AUS

Systemttest 'Lambdaregelung aus' anstoßen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-lambda-aus"></a>
### STATUS_SYSTEMCHECK_LAMBDA_AUS

Status Systemttest 'Lambdaregelung aus'

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAMBREG_TEXT | string | Status der Lambdaregelung (flglrs) |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-lambda-aus"></a>
### STOP_SYSTEMCHECK_LAMBDA_AUS

Systemttest 'Lambdaregelung aus' beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-kompression"></a>
### START_SYSTEMCHECK_KOMPRESSION

Kompressionstest anstoßen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-kompression"></a>
### STOP_SYSTEMCHECK_KOMPRESSION

Kompressionstest beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-power-down"></a>
### STEUERN_POWER_DOWN

Anforderung Power Down Mode

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zwang-rambackup"></a>
### STEUERN_ZWANG_RAMBACKUP

Zwangssichern der RAM-Backup-Werte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ram-backup"></a>
### RAM_BACKUP

Loeschen der RAM-Backup-Werte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ram-lesen"></a>
### RAM_LESEN

Auslesen von beliebigen RAM-Zellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |
| RAM_LESEN_ANZAHL_BYTE | long | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| RAM_LESEN_WERT | binary | Ausgelesener Wert |
| RAM_LESEN_EINH | string | Einheit ausgelesener Wert [HEX] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbm-mode9"></a>
### STATUS_RBM_MODE9

Lesen der RBM-Werte Mode9

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_M9GENDEN_WERT | unsigned long | General Denominator (m9genden_w) |
| STAT_M9IGNCYC_WERT | unsigned long | Anzahl Zündungen (m9igncyc_w) |
| STAT_M9NMCAT1_WERT | unsigned long | Wert von m9nmcat1_w |
| STAT_M9DNCAT1_WERT | unsigned long | Wert von m9dncat1_w |
| STAT_M9NMCAT2_WERT | unsigned long | Wert von m9nmcat2_w |
| STAT_M9DNCAT2_WERT | unsigned long | Wert von m9dncat2_w |
| STAT_M9NMOXS1_WERT | unsigned long | Wert von m9nmoxs1_w |
| STAT_M9DNOXS1_WERT | unsigned long | Wert von m9dnoxs1_w |
| STAT_M9NMOXS2_WERT | unsigned long | Wert von m9nmoxs2_w |
| STAT_M9DNOXS2_WERT | unsigned long | Wert von m9dnoxs2_w |
| STAT_M9NMEGR_WERT | unsigned long | Wert von m9nmegr_w |
| STAT_M9DNEGR_WERT | unsigned long | Wert von m9dnegr_w |
| STAT_M9NMSAIR_WERT | unsigned long | Wert von m9nmsair_w |
| STAT_M9DNSAIR_WERT | unsigned long | Wert von m9dnsair_w |
| STAT_M9NMEVAP_WERT | unsigned long | Wert von m9nmevap_w |
| STAT_M9DNEVAP_WERT | unsigned long | Wert von m9dnevap_w |
| STAT_M9NMSOS1_WERT | unsigned long | Nummerator Lamdasonde hinter Kat Bank1 |
| STAT_M9DNSOS1_WERT | unsigned long | Denominator Lamdasonde hinter Kat Bank1 |
| STAT_M9NMSOS2_WERT | unsigned long | Nummerator Lamdasonde hinter Kat Bank2 |
| STAT_M9DNSOS2_WERT | unsigned long | Denominator Lamdasonde hinter Kat Bank2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbm-block1"></a>
### STATUS_RBM_BLOCK1

Lesen der RBM-Werte Block1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_NOMINATOR_KAT | unsigned long | Nominator Katalysator |
| STAT_DENOMINATOR_KAT | unsigned long | Denominator Katalysator |
| STAT_NOMINATOR_KAT_2 | unsigned long | Nominator Katalysator Bank 2 |
| STAT_DENOMINATOR_KAT_2 | unsigned long | Denominator Katalysator Bank 2 |
| STAT_NOMINATOR_DYLSU | unsigned long | Nominator LSU dynamisch zu langsam |
| STAT_DENOMINATOR_DYLSU | unsigned long | Denominator LSU dynamisch zu langsam |
| STAT_NOMINATOR_DYLSU_2 | unsigned long | Nominator LSU dynamisch zu langsam Bank 2 |
| STAT_DENOMINATOR_DYLSU_2 | unsigned long | Denominator LSU dynamisch zu langsam Bank 2 |
| STAT_NOMINATOR_ULSU | unsigned long | Nominator Spannungsüberwachung LSU |
| STAT_DENOMINATOR_ULSU | unsigned long | Denominator Spannungsüberwachung LSU |
| STAT_NOMINATOR_ULSU_2 | unsigned long | Nominator Spannungsüberwachung LSU Bank 2 |
| STAT_DENOMINATOR_ULSU_2 | unsigned long | Denominator Spannungsüberwachung LSU Bank 2 |
| STAT_NOMINATOR_PLLSU | unsigned long | Nominator Plausibilität LSU |
| STAT_DENOMINATOR_PLLSU | unsigned long | Denominator Plausibilität LSU |
| STAT_NOMINATOR_PLLSU_2 | unsigned long | Nominator Plausibilität LSU Bank 2 |
| STAT_DENOMINATOR_PLLSU_2 | unsigned long | Denominator Plausibilität LSU Bank 2 |
| STAT_NOMINATOR_TES | unsigned long | Nominator Tankentlüftungssystem |
| STAT_DENOMINATOR_TES | unsigned long | Denominator Tankentlüftungssystem |
| STAT_NOMINATOR_TESG | unsigned long | Nominator Tankdiagnose Grobleck |
| STAT_DENOMINATOR_TESG | unsigned long | Denominator Tankdiagnose Grobleck |
| STAT_NOMINATOR_DMTK | unsigned long | Nominator Tankdiagnose Feinstleck |
| STAT_DENOMINATOR_DMTK | unsigned long | Denominator Tankdiagnose Feinstleck |
| STAT_NOMINATOR_DMTL | unsigned long | Nominator Tankdiagnose Modulfehler |
| STAT_DENOMINATOR_DMTL | unsigned long | Denominator Tankdiagnose Modulfehler |
| STAT_NOMINATOR_ENWS | unsigned long | Nominator Nockenwellensteuerung Einlass Nockenwelle |
| STAT_DENOMINATOR_ENWS | unsigned long | Denominator Nockenwellensteuerung Einlass Nockenwelle |
| STAT_NOMINATOR_ANWS | unsigned long | Nominator Nockenwellensteuerung Auslass Nockenwelle |
| STAT_DENOMINATOR_ANWS | unsigned long | Denominator Nockenwellensteuerung Auslass Nockenwelle |
| STAT_NOMINATOR_ENWS_2 | unsigned long | Nominator Nockenwellensteuerung Einlass Nockenwelle Bank 2 |
| STAT_DENOMINATOR_ENWS_2 | unsigned long | Denominator Nockenwellensteuerung Einlass Nockenwelle Bank 2 |
| STAT_NOMINATOR_ANWS_2 | unsigned long | Nominator Nockenwellensteuerung Auslass Nockenwelle Bank 2 |
| STAT_DENOMINATOR_ANWS_2 | unsigned long | Denominator Nockenwellensteuerung Auslass Nockenwelle Bank 2 |
| STAT_NOMINATOR_ENWSAD | unsigned long | Nominator Einlassnockenwellensteuerung Anschlagsadaption |
| STAT_DENOMINATOR_ENWSAD | unsigned long | Denominator Einlassnockenwellensteuerung Anschlagsadaption |
| STAT_NOMINATOR_ENWSAD_2 | unsigned long | Nominator Einlassnockenwellensteuerung Anschlagsadaption Bank 2 |
| STAT_DENOMINATOR_ENWSAD_2 | unsigned long | Denominator Einlassnockenwellensteuerung Anschlagsadaption Bank 2 |
| STAT_NOMINATOR_ANWSAD | unsigned long | Nominator Auslassnockenwellensteuerung Anschlagsadaption |
| STAT_DENOMINATOR_ANWSAD | unsigned long | Denominator Auslassnockenwellensteuerung Anschlagsadaption |
| STAT_NOMINATOR_ANWSAD_2 | unsigned long | Nominator Auslassnockenwellensteuerung Anschlagsadaption Bank 2 |
| STAT_DENOMINATOR_ANWSAD_2 | unsigned long | Denominator Auslassnockenwellensteuerung Anschlagsadaption Bank 2 |
| STAT_NOMINATOR_NWEKW | unsigned long | Nominator Zuordnung Einlassnockenwelle zu Kurbelwelle |
| STAT_DENOMINATOR_NWEKW | unsigned long | Denominator Zuordnung Einlassnockenwelle zu Kurbelwelle |
| STAT_NOMINATOR_NWEKW_2 | unsigned long | Nominator Zuordnung Einlassnockenwelle zu Kurbelwelle Bank 2 |
| STAT_DENOMINATOR_NWEKW_2 | unsigned long | Denominator Zuordnung Einlassnockenwelle zu Kurbelwelle Bank 2 |
| STAT_NOMINATOR_NWAKW | unsigned long | Nominator Zuordnung Auslassnockenwelle zu Kurbelwelle |
| STAT_DENOMINATOR_NWAKW | unsigned long | Denominator Zuordnung Auslassnockenwelle zu Kurbelwelle |
| STAT_NOMINATOR_NWAKW_2 | unsigned long | Nominator Zuordnung Auslassnockenwelle zu Kurbelwelle Bank 2 |
| STAT_DENOMINATOR_NWAKW_2 | unsigned long | Denominator Zuordnung Auslassnockenwelle zu Kurbelwelle Bank 2 |
| STAT_NOMINATOR_DPSPL | unsigned long | Nominator Plausibilität Drucksensor Saugrohr |
| STAT_DENOMINATOR_DPSPL | unsigned long | Denominator Plausibilität Drucksensor Saugrohr |
| STAT_NUMERATOR_DYSHN | unsigned long | Numerator Plausibilisierung Dynamikmessung Sonde hinter Kat |
| STAT_DENOMINATOR_DYSHN | unsigned long | Denominator Plausibilisierung Dynamikmessung Sonde hinter Kat |
| STAT_NUMERATOR_DYSH2N | unsigned long | Numerator Plausibilisierung Dynamikmessung Sonde hinter Kat Bank2 |
| STAT_DENOMINATOR_DYSH2N | unsigned long | Denominator Plausibilisierung Dynamikmessung Sonde hinter Kat Bank2 |
| STAT_NUMERATOR_LASH | unsigned long | Numerator Plausibilisierung Lamdasondenalterung |
| STAT_DENOMINATOR_LASH | unsigned long | Denominator Plausibilisierung Lamdasondenalterung |
| STAT_NUMERATOR_LASH2 | unsigned long | Numerator Plausibilisierung Lamdasondenalterung Bank2 |
| STAT_DENOMINATOR_LASH2 | unsigned long | Denominator Plausibilisierung Lamdasondenalterung |
| STAT_NUMERATOR_CTRSH | unsigned long | Numerator Dynamikmessung LS Hinter-KAT Transienttime |
| STAT_DENOMINATOR_CTRSH | unsigned long | Denominator Dynamikmessung LS Hinter-KAT Transienttime |
| STAT_NUMERATOR_CTRSH2 | unsigned long | Numerator Dynamikmessung LS Hinter-KAT Transienttime Bank2 |
| STAT_DENOMINATOR_CTRSH2 | unsigned long | Denominator Dynamikmessung LS Hinter-KAT Transienttime Bank2 |
| STAT_NUMERATOR_BHDYRE | unsigned long | Numerator Dynamikmessung LS Hinter-KAT Responsetime |
| STAT_DENOMINATOR_BHDYRE | unsigned long | Denominator Dynamikmessung LS Hinter-KAT Responsetime |
| STAT_NUMERATOR_BHDYRE2 | unsigned long | Numerator Dynamikmessung LS Hinter-KAT Responsetime Bank2 |
| STAT_DENOMINATOR_BHDYRE2 | unsigned long | Denominator Dynamikmessung LS Hinter-KAT Responsetime Bank2 |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort an SG |

<a id="job-status-rbm-block2"></a>
### STATUS_RBM_BLOCK2

Lesen der RBM-Werte Block2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STAT_NOMINATOR_CUHR | unsigned long | Nominator CAN rel. Zeitgeber |
| STAT_DENOMINATOR_CUHR | unsigned long | Denominator CAN rel. Zeitgeber |
| STAT_NOMINATOR_HSH | unsigned long | Nominator Heizung Lambdasonde hinter KAT |
| STAT_DENOMINATOR_HSH | unsigned long | Denominator Heizung Lambdasonde hinter KAT |
| STAT_NOMINATOR_HSH_2 | unsigned long | Nominator Heizung Lambdasonde hinter KAT Bank 2 |
| STAT_DENOMINATOR_HSH_2 | unsigned long | Denominator Heizung Lambdasonde hinter KAT Bank 2 |
| STAT_NOMINATOR_HSV | unsigned long | Nominator Heizung Lambdasonde vor KAT |
| STAT_DENOMINATOR_HSV | unsigned long | Denominator Heizung Lambdasonde vor KAT |
| STAT_NOMINATOR_HSV_2 | unsigned long | Nominator Heizung Lambdasonde vor KAT Bank 2 |
| STAT_DENOMINATOR_HSV_2 | unsigned long | Denominator Heizung Lambdasonde vor KAT Bank 2 |
| STAT_NOMINATOR_LASH | unsigned long | Nominator Lambdasondenalterung hinter KAT |
| STAT_DENOMINATOR_LASH | unsigned long | Denominator Lambdasondenalterung hinter KAT |
| STAT_NOMINATOR_LLRCS | unsigned long | Leerlaufdrehzahlabweichung mit CSERS Strategie Numerator |
| STAT_DENOMINATOR_LLRCS | unsigned long | Leerlaufdrehzahlabweichung mit CSERS Strategie Denominator |
| STAT_NOMINATOR_LLR | unsigned long | Nominator Leerlaufregelung |
| STAT_DENOMINATOR_LLR | unsigned long | Denominator Leerlaufregelung |
| STAT_NOMINATOR_PUR | unsigned long | Nominator Umgebungsdrucksensor Range Check |
| STAT_DENOMINATOR_PUR | unsigned long | Denominator Umgebungsdrucksensor Range Check |
| STAT_NOMINATOR_TA | unsigned long | Nominator Ansauglufttemperatur TANS |
| STAT_DENOMINATOR_TA | unsigned long | Denominator Ansauglufttemperatur TANS |
| STAT_NOMINATOR_TM | unsigned long | Nominator Motortemperatur TMOT |
| STAT_DENOMINATOR_TM | unsigned long | Denominator Motortemperatur TMOT |
| STAT_NOMINATOR_TUM | unsigned long | Nominator Umgebungstemperatur |
| STAT_DENOMINATOR_TUM | unsigned long | Denominator Umgebungstemperatur |
| STAT_NOMINATOR_VFZ | unsigned long | Nominator Geschwindigkeitssignal |
| STAT_DENOMINATOR_VFZ | unsigned long | Denominator Geschwindigkeitssignal |
| STAT_NOMINATOR_DVEF | unsigned long | Nominator DV-E Fehler bei Federprüfung |
| STAT_DENOMINATOR_DVEF | unsigned long | Denominator DV-E Fehler bei Federprüfung |
| STAT_NOMINATOR_DVEL | unsigned long | Nominator DV-E Lageabweichung |
| STAT_DENOMINATOR_DVEL | unsigned long | Denominator DV-E Lageabweichung |
| STAT_NOMINATOR_DVER | unsigned long | Nominator DV-E Regelbereich |
| STAT_DENOMINATOR_DVER | unsigned long | Denominator DV-E Regelbereich |
| STAT_NOMINATOR_FST | unsigned long | Nominator Tankfuellstandssensor |
| STAT_DENOMINATOR_FST | unsigned long | Denominator Tankfuellstandssensor |
| STAT_NOMINATOR_HFM | unsigned long | Nominator Hauptfüllungssignal |
| STAT_DENOMINATOR_HFM | unsigned long | Denominator Hauptfüllungssignal |
| STAT_NOMINATOR_DK | unsigned long | Nominator DK-Potentiometer |
| STAT_DENOMINATOR_DK | unsigned long | Denominator DK-Potentiometer |
| STAT_NOMINATOR_DK1P | unsigned long | Nominator Drosselklappenpotentiometer 1 |
| STAT_DENOMINATOR_DK1P | unsigned long | Denominator Drosselklappenpotentiometer 1 |
| STAT_NOMINATOR_DK2P | unsigned long | Nominator Drosselklappenpotentiometer 2 |
| STAT_DENOMINATOR_DK2P | unsigned long | Denominator Drosselklappenpotentiometer 2 |
| STAT_NOMINATOR_LLRKH | unsigned long | Nominator Leerlaufregelung während KAT-Heizen |
| STAT_DENOMINATOR_LLRKH | unsigned long | Denominator Leerlaufregelung während KAT-Heizen |
| STAT_NOMINATOR_TACS | unsigned long | Nominator Ansauglufttemperatur TANS-Sensor bei Kaltstart |
| STAT_DENOMINATOR_TACS | unsigned long | Denominator Ansauglufttemperatur TANS-Sensor bei Kaltstart |
| STAT_NOMINATOR_TMCS | unsigned long | Nominator Motortemperatur TMOT-Sensor bei Kaltstart |
| STAT_DENOMINATOR_TMCS | unsigned long | Denominator Motortemperatur TMOT-Sensor bei Kaltstart |
| STAT_NOMINATOR_DYSH | unsigned long | Nominator Dynamikmessung Lambdasonde hinter KAT Bank 1 |
| STAT_DENOMINATOR_DYSH | unsigned long | Denominator Dynamikmessung Lambdasonde hinter KAT Bank 1 |
| STAT_NOMINATOR_DYSH_2 | unsigned long | Nominator Dynamikmessung Lambdasonde hinter KAT Bank 2 |
| STAT_DENOMINATOR_DYSH_2 | unsigned long | Denominator Dynamikmessung Lambdasonde hinter KAT Bank 2 |
| STAT_NUMERATOR_TEOEH | unsigned long | Numerator Diagnose der CAN-Uhr (High-Check) |
| STAT_DENOMINATOR_TEOEH | unsigned long | Denominator Diagnose der CAN-Uhr (High-Check) |
| STAT_NUMERATOR_TEOEL | unsigned long | Numerator Diagnose der CAN-Uhr (Low-Check) |
| STAT_DENOMINATOR_TEOEL | unsigned long | Denominator Diagnose der CAN-Uhr (Low-Check) |
| STAT_NUMERATOR_TEOES | unsigned long | Numerator Einseitiger Fehler der CAN-Uhr |
| STAT_DENOMINATOR_TEOES | unsigned long | Denominator Einseitiger Fehler der CAN-Uhr |
| STAT_NUMERATOR_TEOET | unsigned long | Numerator Fehler der CAN-Uhr (beidseitiger Check) |
| STAT_DENOMINATOR_TEOET | unsigned long | Denominator Fehler der CAN-Uhr (beidseitiger Check) |
| STAT_NUMERATOR_CANCS | unsigned long | Numerator Lageregler Überwachung Auslass-VANOS während Katheizen |
| STAT_DENOMINATOR_CANCS | unsigned long | Denominator Lageregler Überwachung Auslass-VANOS während Katheizen |
| STAT_NUMERATOR_CANCX | unsigned long | Numerator Lageregler Überwachung Auslass-VANOS für korrekte Sollwerteinstellung während Katheizen |
| STAT_DENOMINATOR_CANCX | unsigned long | Denominator Lageregler Überwachung Auslass-VANOS für korrekte Sollwerteinstellung während Katheizen |
| STAT_NUMERATOR_CENCS | unsigned long | Numerator Lageregler Überwachung Einlass-VANOS während Katheizen |
| STAT_DENOMINATOR_CENCS | unsigned long | Denominator Lageregler Überwachung Einlass-VANOS während Katheizen |
| STAT_NUMERATOR_CENCX | unsigned long | Numerator Lageregler Überwachung Einlass-VANOS für korrekte Sollwerteinstellung während Katheizen |
| STAT_DENOMINATOR_CENCX | unsigned long | Denominator Lageregler Überwachung Einlass-VANOS für korrekte Sollwerteinstellung während Katheizen |
| STAT_NUMERATOR_CETKHL | unsigned long | Numerator Überwachung Zündwinkelverstellung während Katheizen in Leerlauf |
| STAT_DENOMINATOR_CETKHL | unsigned long | Denominator Überwachung Zündwinkelverstellung während Katheizen in Leerlauf |
| STAT_NUMERATOR_CETKHT | unsigned long | Numerator Überwachung Zündwinkelverstellung während Katheizen in Teillast |
| STAT_DENOMINATOR_CETKHT | unsigned long | Denominator Überwachung Zündwinkelverstellung während Katheizen in Teillast |
| STAT_NUMERATOR_CHDRKH | unsigned long | Numerator Überwachung Regler Kraftstoffhochdruck während Katheizen im Leerlauf |
| STAT_DENOMINATOR_CHDRKH | unsigned long | Denominator Überwachung Regler Kraftstoffhochdruck während Katheizen im Leerlauf |
| STAT_NUMERATOR_CIA | unsigned long | Numerator Lambdasonde Abgleichleitung open load |
| STAT_DENOMINATOR_CIA | unsigned long | Denominator Lambdasonde Abgleichleitung open load |
| STAT_NUMERATOR_CIP | unsigned long | Numerator Lambdasonde Pump-Leitung open load |
| STAT_DENOMINATOR_CIP | unsigned long | Denominator Lambdasonde Pump-Leitung open load |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort an SG |

<a id="job-status-messwerte"></a>
### STATUS_MESSWERTE

Auslesen des allgemeinen Messwerteblocks

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_TE_WERT | real | Effektive Einspritzzeit (te_w) |
| STAT_TE_EINH | string | Einheit von te_w [ms] |
| STAT_FR_WERT | real | Lambdaregler-Ausgang (fr_w) |
| STAT_FR_EINH | string | Einheit von fr_w  [-] |
| STAT_VFZG_WERT | real | Fahrzeuggeschwindigkeit (vfzg) |
| STAT_VFZG_EINH | string | Einheit von vfzg [km/h] |
| STAT_NMOT_WERT | real | Motordrehzahl nmot_w |
| STAT_NMOT_EINH | string | Einheit von nmot_w [min-1] |
| STAT_NSOL_WERT | real | Leerlauf-Solldrehzahl (nsol) |
| STAT_NSOL_EINH | string | Einheit von nsol  [min-1] |
| STAT_WNWKWE_WERT | real | Winkel Einlass-NW-Flanke rel. zur KW (wnwkwe_w) |
| STAT_WNWKWE_EINH | string | Einheit von wnwkwe_w [Grad KW] |
| STAT_WNWKWA_WERT | real | Winkel Auslass-NW-Flanke rel. zur KW (wnwkwa_w) |
| STAT_WNWKWA_EINH | string | Einheit von wnwkwa_w [Grad KW] |
| STAT_TANS_WERT | real | Ansauglufttemperatur (tans) |
| STAT_TANS_EINH | string | Einheit von tans  [Grad C] |
| STAT_TMOT_WERT | real | Motortemperatur (tmot) |
| STAT_TMOT_EINH | string | Einheit von tmot [Grad C] |
| STAT_ZWOUT_WERT | real | Zündwinkelausgabe (zwout) |
| STAT_ZWOUT_EINH | string | Einheit von zwout [Grad] |
| STAT_WDKBA_WERT | real | DK Winkel rel. zum unteren Anschlag (wdkba) |
| STAT_WDKBA_EINH | string | Einheit von wdkba [% DK] |
| STAT_MSHFM_WERT | real | Massenstrom (mshfm_w) |
| STAT_MSHFM_EINH | string | Einheit von mshfm_w [kg/h] |
| STAT_MIIST_WERT | real | Indiziertes Motormoment (miist_w) |
| STAT_MIIST_EINH | string | Einheit von miist_w [%] |
| STAT_UB_WERT | real | Batteriespannung (ub) |
| STAT_UB_EINH | string | Einheit von ub [V] |
| STAT_UPWG_WERT | real | Spannung PWG-Poti 1 (upwg1_w) |
| STAT_UPWG_EINH | string | Einheit von upwg1_w [V] |
| STAT_TKA_WERT | real | Temperatur Kühlerausgang (tkalin) |
| STAT_TKA_EINH | string | Einheit von tklin [Grad C] |
| STAT_RKRN0_WERT | real | Normierter Referenzpegel Klopfsensor 1 (rkrn_w[0]) |
| STAT_RKRN0_EINH | string | Einheit von rkrn_w[0] [V] |
| STAT_RKRN1_WERT | real | Normierter Referenzpegel Klopfsensor 2 (rkrn_w[1]) |
| STAT_RKRN1_EINH | string | Einheit von rkrn_w[1] [V] |
| STAT_RKRN2_WERT | real | Normierter Referenzpegel Klopfsensor 3 (rkrn_w[2]) |
| STAT_RKRN2_EINH | string | Einheit von rkrn_w[2] [V] |
| STAT_RKRN3_WERT | real | Normierter Referenzpegel Klopfsensor 4 (rkrn_w[3]) |
| STAT_RKRN3_EINH | string | Einheit von rkrn_w[3] [V] |
| STAT_RKRN4_WERT | real | Normierter Referenzpegel Klopfsensor 5 (rkrn_w[4]) |
| STAT_RKRN4_EINH | string | Einheit von rkrn_w[4] [V] |
| STAT_RKRN5_WERT | real | Normierter Referenzpegel Klopfsensor 6 (rkrn_w[5]) |
| STAT_RKRN5_EINH | string | Einheit von rkrn_w[5] [V] |
| STAT_OZKRZMWKOR_WERT | real | Kurzzeitmittelwert Ölniveau (ozkrzmwkor) |
| STAT_OZKRZMWKOR_EINH | string | Einheit von ozkrzmwkor [-] |
| STAT_OZLANGMW_WERT | real | Langzeitmittelwert Ölniveau (ozlangmw) |
| STAT_OZLANGMW_EINH | string | Einheit von ozlangmw [-] |
| STAT_OELSTANDR_WERT | real | Füllstand Motoröl (oelstandr) |
| STAT_OELSTANDR_EINH | string | Einheit von oelstandr [-] |
| STAT_STOELNFM_WERT | real | Status Peilstabanzeige (stoelnfm) |
| STAT_STOELNFM_EINH | string | Einheit von stoelnfm [-] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-di"></a>
### STATUS_MESSWERTE_DI

Auslesen der DI-Messwerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_PRIST_WERT | real | Gefilterter Raildruck-Istwert (prist_w) |
| STAT_PRIST_EINH | string | Einheit von prist_w [MPa] |
| STAT_PRROH_WERT | real | Ungefilterter Raildruck-Istwert (prroh_w) |
| STAT_PRROH_EINH | string | Einheit von prroh_w [MPa] |
| STAT_PRSOLL_WERT | real | Sollwert Raildruckregelung (prsoll_w) |
| STAT_PRSOLL_EINH | string | Einheit von prsoll_w  [MPa] |
| STAT_VSSEKP_WERT | real | EKP-Sollvolumenstrom (vssekp) |
| STAT_VSSEKP_EINH | string | Einheit von vssekp [l] |
| STAT_DWMSVO_WERT | real | Deltawinkel öffnen MSV (dwmsvo_w) |
| STAT_DWMSVO_EINH | string | Einheit von dwmsvo_w [Grad KW] |
| STAT_B_MILFB_EIN | int | MIL-Ansteuerung fremdbestimmt B_milfb |
| STAT_B_MILSL_EIN | int | MIL-Ansteuerung durch Slave-SG B_milsl |
| STAT_DFRMOFF_WERT | real | frm-Offset zur Kontrolle v. Problemen der Vorsteuerung (dfrmoff_w) |
| STAT_DFRMOFF_EINH | string | Einheit von dfrmoff_w [-] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-batterieintegrator"></a>
### STATUS_BATTERIEINTEGRATOR

Auslesen des Batterie-Ladezustands

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_DFMONITOR_WERT | real | Batterie-Ladezustand (dfmonitor) |
| STAT_DFMONITOR_EINH | string | Einheit von dfmonitor [%] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schalterstati"></a>
### STATUS_SCHALTERSTATI

Auslesen der Schalterstati

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_KL15_EIN | int | Bedingung KL15 ein (B_kl15) |
| STAT_ESTART_EIN | int | Bedingung Startrelais (B_estart) |
| STAT_KUPPL_EIN | int | Bedingung Kupplung betaetigt (B_kuppl) |
| STAT_BL_EIN | int | Bedingung Bremsschalter ein (B_br) |
| STAT_BR_EIN | int | Bedingung Bremslichttestschalter ein (B_bl) |
| STAT_KO_EIN | int | Bedingung Klimakompressor ein (B_ko) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-funktionsstati"></a>
### STATUS_FUNKTIONSSTATI

Auslesen der Funktionsstati

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_LL_EIN | int | Bedingung Leerlauf (B_ll) |
| STAT_VL_EIN | int | Bedingung Vollast (B_vl) |
| STAT_SBBHK_EIN | int | Bedingung Lambdasondenbereitschaft hinter Kat (B_sbbhk) |
| STAT_SBBVK_EIN | int | Bedingung Lambdasondenbereitschaft vor Kat (B_sbbvk) |
| STAT_LR_EIN | int | Bedingung Lambdaregelung ein (B_lr) |
| STAT_KD_EIN | int | Bedingung KickDown ein (B_kd) |
| STAT_PN_EIN | int | Bedingung Park-Neutral ein (B_pn) |
| STAT_ECULOCK_EIN | int | Bedingung EWS=OK ein (B_eculock) |
| STAT_TEHB_EIN | int | Bedingung Tankentlüftung m. hoher Beladung ein (B_tehb) |
| STAT_SA_EIN | int | Bedingung Schubabschneiden ein (B_sa) |
| STAT_LRNRDY_EIN | int | Bedingung UMA Lernerfolg (B_lrnrdy) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Auslesen der Funktions- und Schalterstati

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_KL15_EIN | int | Bedingung KL15 ein (B_kl15) |
| STAT_ESTART_EIN | int | Bedingung Startrelais (B_estart) |
| STAT_KUP_EIN | int | Bedingung Kupplung betaetigt (B_kuppl) |
| STAT_BLS_EIN | int | Bedingung Bremsschalter ein (B_br) |
| STAT_BLTS_EIN | int | Bedingung Bremslichttestschalter ein (B_bl) |
| STAT_KO_EIN | int | Bedingung Klimakompressor ein (B_ko) |
| STAT_LL_EIN | int | Zustand Leerlauf erreicht (B_ll) |
| STAT_VL_EIN | int | Zustand Vollast erreicht (B_vl) |
| STAT_SBBHK_EIN | int | Lambdasondenbereitschaft hinter Kat Bank1 (B_sbbhk) |
| STAT_SBBVK_EIN | int | Lambdasondenbereitschaft vor Kat Bank1 (B_sbbvk) |
| STAT_LR_EIN | int | Zustand Lambdaregelung Bank1 ein (B_lr) |
| STAT_KD_EIN | int | Zustand KickDown ein (B_kd) |
| STAT_PN_EIN | int | Zustand Park-Neutral ein (B_pn) |
| STAT_ECULOCK_EIN | int | Zustand EWS_OK ein (B_eculock) |
| STAT_TEHB_EIN | int | Zustand TEHB ein (B_tehb) |
| STAT_SA_EIN | int | Zustand Schubabschneiden ein (B_sa) |
| STAT_LRNRDY_EIN | int | Zustand UMA Lernerfolg (B_lrnrdy) |
| _TEL_AUFTRAG_SCHALT | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_SCHALT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_FUNK | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_FUNK | binary | Hex-Antwort von SG |

<a id="job-status-laufunruhe"></a>
### STATUS_LAUFUNRUHE

Auslesen der Laufunruhewerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_LUTSFI1_WERT | real | Laufunruhewert Zylinder 1 (lutsfi1_w) |
| STAT_LUTSFI1_EINH | string | Einheit von lutsfi1_w [sec-1] |
| STAT_LUTSFI2_WERT | real | Laufunruhewert Zylinder 2 (lutsfi2_w) |
| STAT_LUTSFI2_EINH | string | Einheit von lutsfi2_w [sec-1] |
| STAT_LUTSFI3_WERT | real | Laufunruhewert Zylinder 3 (lutsfi13_w) |
| STAT_LUTSFI3_EINH | string | Einheit von lutsfi3_w [sec-1] |
| STAT_LUTSFI4_WERT | real | Laufunruhewert Zylinder 4 (lutsfi4_w) |
| STAT_LUTSFI4_EINH | string | Einheit von lutsfi4_w [sec-1] |
| STAT_LUTSFI5_WERT | real | Laufunruhewert Zylinder 5 (lutsfi5_w) |
| STAT_LUTSFI5_EINH | string | Einheit von lutsfi5_w [sec-1] |
| STAT_LUTSFI6_WERT | real | Laufunruhewert Zylinder 6 (lutsfi6_w) |
| STAT_LUTSFI6_EINH | string | Einheit von lutsfi6_w [sec-1] |
| STAT_LUTSFI7_WERT | real | Laufunruhewert Zylinder 7 (lutsfi7_w) |
| STAT_LUTSFI7_EINH | string | Einheit von lutsfi7_w [sec-1] |
| STAT_LUTSFI8_WERT | real | Laufunruhewert Zylinder 8 (lutsfi8_w) |
| STAT_LUTSFI8_EINH | string | Einheit von lutsfi8_w [sec-1] |
| STAT_LUTSFI9_WERT | real | Laufunruhewert Zylinder 9 (lutsfi9_w) |
| STAT_LUTSFI9_EINH | string | Einheit von lutsfi9_w [sec-1] |
| STAT_LUTSFI10_WERT | real | Laufunruhewert Zylinder 10 (lutsfi10_w) |
| STAT_LUTSFI10_EINH | string | Einheit von lutsfi10_w [sec-1] |
| STAT_LUTSFI11_WERT | real | Laufunruhewert Zylinder 11 (lutsfi11_w) |
| STAT_LUTSFI11_EINH | string | Einheit von lutsfi11_w [sec-1] |
| STAT_LUTSFI12_WERT | real | Laufunruhewert Zylinder 12 (lutsfi12_w) |
| STAT_LUTSFI12_EINH | string | Einheit von lutsfi12_w [sec-1] |
| STAT_FOFR1_EIN | int | LL-Adaption abgeschlossen (B_fofr1) |
| STAT_UULSUV_WERT | real | Lambdasondenspannung 1 (uulsuv_w) |
| STAT_UULSUV_EINH | string | Einheit von uulsuv_w [V] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dkhfm"></a>
### STATUS_DKHFM

Auslesen der DK/HFM-Abgleichswerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_MSNDKO_WERT | real | Leckluftmassenstrom (msndko_w) |
| STAT_MSNDKO_EINH | string | Einheit von msndko_w  [kg/h] |
| STAT_FKMSDKA_WERT | real | Korr.fakt. schn. Massenstromabgleich (fkmsdka_w) |
| STAT_FKMSDKA_EINH | string | Einheit von fkmsdka_w [-] |
| STAT_FKMSDK_WERT | real | Korr.fakt. Massenstr. Neb.fü.sig. (fkmsdk_w) |
| STAT_FKMSDK_EINH | string | Einheit von fkmsdk_w [-] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gemisch"></a>
### STATUS_GEMISCH

Auslesen der Gemischwerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_RKAT_WERT | real | Gemischadaption additiv (rkat_w) |
| STAT_RKAT_EINH | string | Einheit von rkat_w [%] |
| STAT_FRA_WERT | real | Gemischadaption multiplikativ (fra_w) |
| STAT_FRA_EINH | string | Einheit von fra_w [-] |
| STAT_TEDUB_WERT | real | Einschaltdauer Heizerendstufe (tedub) |
| STAT_TEDUB_EINH | string | Einheit von tedub [s] |
| STAT_DYNLSU_WERT | real | Normierter Dynamikwert (dynlsu_w) |
| STAT_DYNLSU_EINH | string | Einheit von dynlsu_w [-] |
| STAT_LAMSONI_WERT | real | Lambda Istwert (lamsoni_w) |
| STAT_LAMSONI_EINH | string | Einheit von lamsoni_w [-] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ausgaenge"></a>
### STATUS_AUSGAENGE

Auslesen der Ausgänge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_TATEIST_WERT | real | Tastverhältnis (tateist) |
| STAT_TATEIST_EINH | string | Einheit von tateist [%] |
| STAT_VSASPRI_WERT | real | Istwert Auslasspreizung (Vsa_spri) |
| STAT_VSASPRI_EINH | string | Einheit von Vsa_spri [Grad KW] |
| STAT_VSESPRI_WERT | real | Istwert Einlasspreizung (Vse_spri) |
| STAT_VSESPRI_EINH | string | Einheit von Vse_spri [Grad KW] |
| STAT_VSATV_WERT | real | Tastverhältnis Auslasspreizung (Vsa_tv) |
| STAT_VSATV_EINH | string | Einheit von Vsa_tv [%] |
| STAT_VSETV_WERT | real | Tastverhältnis Einlasspreizung (Vse_tv) |
| STAT_VSETV_EINH | string | Einheit von Vse_tv [%] |
| STAT_TAML_WERT | real | Tastverhältnis E-Lüfter (taml) |
| STAT_TAML_EINH | string | Einheit von taml [%] |
| STAT_KOE_EIN | int | Bedingung Klimakompressor ein (B_koe) |
| STAT_HSVE_EIN | int | Bedingung Heizung LS vor KAT ein (B_hsve) |
| STAT_HSHE_EIN | int | Bedingung Heizung LS h Kat ein (B_hshe) |
| STAT_AKR_EIN | int | Bedingung Abgasklappe ein (B_akr) |
| STAT_EBL_EIN | int | Bedingung E-Box Luefter ein (B_ebl) |
| STAT_EKP_EIN | int | Bedingung EKP ein (B_ekp) |
| STAT_ETR_EIN | int | Bedingung Kennfeldthermostat ein (B_etr) |
| STAT_STA_EIN | int | Bedingung Startrelais ein (B_sta) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-nwgadaption"></a>
### STATUS_NWGADAPTION

Auslesen der NWG-Adaptionen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_VSAADP_WERT | real | Adaptionswert Anschlag Auslasspreizung variable NWS (Vsa_adp) |
| STAT_VSAADP_EINH | string | Einheit von Vsa_adp [Grad KW] |
| STAT_VSEADP_WERT | real | Adaptionswert Anschlag Einlasspreizung variable NWS (Vse_adp) |
| STAT_VSEADP_EINH | string | Einheit von Vse_adp [Grad KW] |
| STAT_VSAADPFL0_WERT | real | Flankenindivid. Adaption Auslasspreizung var. NWS (Vsa_adp_fl0) |
| STAT_VSAADPFL0_EINH | string | Einheit von Vsa_adp_fl0 [Grad KW] |
| STAT_VSAADPFL1_WERT | real | Flankenindivid. Adaption Auslasspreizung var. NWS (Vsa_adp_fl1) |
| STAT_VSAADPFL1_EINH | string | Einheit von Vsa_adp_fl1 [Grad KW] |
| STAT_VSAADPFL2_WERT | real | Flankenindivid. Adaption Auslasspreizung var. NWS (Vsa_adp_fl2) |
| STAT_VSAADPFL2_EINH | string | Einheit von Vsa_adp_fl2 [Grad KW] |
| STAT_VSAADPFL3_WERT | real | Flankenindivid. Adaption Auslasspreizung var. NWS (Vsa_adp_fl3) |
| STAT_VSAADPFL3_EINH | string | Einheit von Vsa_adp_fl3 [Grad KW] |
| STAT_VSEADPFL0_WERT | real | Flankenindivid. Adaption Einlasspreizung var. NWS (Vse_adp_fl0) |
| STAT_VSEADPFL0_EINH | string | Einheit von vse_adp_fl0 [Grad KW] |
| STAT_VSEADPFL1_WERT | real | Flankenindivid. Adaption Einlasspreizung var. NWS (Vse_adp_fl1) |
| STAT_VSEADPFL1_EINH | string | Einheit von vse_adp_fl1 [Grad KW] |
| STAT_VSEADPFL2_WERT | real | Flankenindivid. Adaption Einlasspreizung var. NWS (Vse_adp_fl2) |
| STAT_VSEADPFL2_EINH | string | Einheit von vse_adp_fl2 [Grad KW] |
| STAT_VSEADPFL3_WERT | real | Flankenindivid. Adaption Einlasspreizung var. NWS (Vse_adp_fl3) |
| STAT_VSEADPFL3_EINH | string | Einheit von vse_adp_fl3 [Grad KW] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-readiness"></a>
### STATUS_READINESS

Auslesen der NWG-Adaptionen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_KATFZ_EIN | int | Bedingung KatFahrzeug (B_katfz) |
| STAT_CDTES_EIN | int | Bedingung Diagnosefreigabe Tankentlueftungssystem (B_cdtes) |
| STAT_CDSLS_EIN | int | Bedingung Diagnosefreigabe Sekundaerluftsystem (B_cdsls) |
| STAT_CDLSV_EIN | int | Bedingung Diagnosefreigabe Lambdasonde vor KAT (B_cdlsv) |
| STAT_CDHSV_EIN | int | Bedingung Diagnosefreigabe Lambdasondenheizung vor KAT (B_cdhsv) |
| STAT_CDAGR_EIN | int | Bedingung Diagnosefreigabe Abgasrueckfuehrung (B_cdagr) |
| STAT_KATRDY_EIN | int | Bedingung Katdiagnose ready (B_katrdy) |
| STAT_TESRDY_EIN | int | Bedingung Tankentlueftungssystem ready (B_tesrdy) |
| STAT_SLSRDY_EIN | int | Bedingung Sekundaerluftsystem ready (B_slsrdy) |
| STAT_LSRDY_EIN | int | Bedingung Lambdasonden ready (B_lsrdy) |
| STAT_HSRDY_EIN | int | Bedingung Heizung Lambdasonden ready (B_hsrdy) |
| STAT_AGRRDY_EIN | int | Bedingung Abgasrueckfuehrung ready (B_agrrdy) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fgr"></a>
### STATUS_FGR

Auslesen des FGR-Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_FGRAT_EIN | int | Bedingung FGR Austaste ein (B_FGRAT) |
| STAT_FGRHSA_EIN | int | Bedingung FGR Hauptschalter ein (B_FGRHSA) |
| STAT_FGRTBE_EIN | int | Bedingung Taste Beschleunigung ein (B_FGRTBE) |
| STAT_FGRTSE_EIN | int | Bedingung Taste Setzen ein (B_FGRTSE) |
| STAT_FGRTVE_EIN | int | Bedingung Taste Verzoegern ein (B_FGRTVE) |
| STAT_FGRTWA_EIN | int | Bedingung Taste Wiederaufnahme ein (B_FGRTWA) |
| STAT_LFGR_EIN | int | Bedingung FGR-Lampe ein (L_FGR) |
| STAT_ACC_EIN | int | Bedingung ACC ein (B_ACC) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-vvt"></a>
### STATUS_VVT

Auslesen der VVT-Messwerte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_VVTSW_WERT | real | VVT-Sollwert (vvt_sw) |
| STAT_VVTSW_EINH | string | Einheit von vvt_sw [%] |
| STAT_VVTIW_WERT | real | VVT-Istwert (vvt_iw) |
| STAT_VVTIW_EINH | string | Einheit von vvt_iw [%] |
| STAT_VVTTV_WERT | real | VVT-Tastverhältnis (vvt_tv) |
| STAT_VVTTV_EINH | string | Einheit von vvt_tv [%] |
| STAT_VVTES_WERT | real | VVT-Strombedarf (vvt_es) |
| STAT_VVTES_EINH | string | Einheit von vvt_es [-] |
| STAT_MINHUBVSI_WERT | real | Bedingung Adaptionswert gelöscht (minhubvsi) |
| STAT_MINHUBVSI_EINH | string | Einheit von minhubvsi_w [mm] |
| STAT_DELTAGVFI_WERT | real | deltagv nach PT1-Filter (deltagvfi) |
| STAT_DELTAGVFI_EINH | string | Einheit von deltagvfi [] |
| STAT_FLUB1_WERT | real | Mittelwert Laufunruhe gefiltert (flub1_w) |
| STAT_FLUB1_EINH | string | Einheit von flub1_w [] |
| STAT_MINHUBROH_WERT | real | Minhub vom Tester oder aus Adaption (minhub_roh) |
| STAT_MINHUBROH_EINH | string | Einheit von minhub_roh [mm] |
| STAT_MINHUBVS_EIN | int | Über Tester vorgegebener Minhub (B_minhubvs) |
| STAT_NMOT_EIN | int | Bedingung Motordrehzahl: n&gt;NMIN (B_nmot) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-minhub"></a>
### STATUS_MINHUB

Auslesen des Minhub-Wertes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_MINHUB_WERT | real | Wert von minhub_w |
| STAT_MINHUB_EINH | string | Einheit von minhub_w |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betriebsstundenzaehler"></a>
### STATUS_BETRIEBSSTUNDENZAEHLER

Auslesen des Betriebsstundenzähler-Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_BSZ | string | Status Betriebsstundenzaehler (Text) |
| STAT_BSZ_WERT | int | Status Betriebsstundenzaehler (Wert top_w) |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

Auslesen der Motortemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_MOTORTEMPERATUR_WERT | real | Motortemperatur (tmot) |
| STAT_MOTORTEMPERATUR_EINH | string | Einheit von tmot [Grad C] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Auslesen der Motordrehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_MOTORDREHZAHL_WERT | real | Motordrehzahl (nmot) |
| STAT_MOTORDREHZAHL_EINH | string | Einheit von nmot [Grad C] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

Auslesen der Ansauglufttemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_AN_LUFTTEMPERATUR_WERT | real | Ansauglufttemperatur (tans) |
| STAT_AN_LUFTTEMPERATUR_EINH | string | Einheit von tans [Grad C] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

Auslesen des Luftmassenstroms

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_LMM_MASSE_WERT | real | Massenstrom (mshfm_w) |
| STAT_LMM_MASSE_EINH | string | Einheit von mshfm_w [kg/h] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde"></a>
### STATUS_L_SONDE

Auslesen der Lambdasondenspannung 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_L_SONDE_WERT | real | Lambdasondenspannung 1 (uulsuv_w) |
| STAT_L_SONDE_EINH | string | Einheit von uulsuv_w [V] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde-h"></a>
### STATUS_L_SONDE_H

Auslesen der Lambdasondenspannung 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_L_SONDE_H_WERT | real | Lambdasondenspannung 1 (uushk_w) |
| STAT_L_SONDE_H_EINH | string | Einheit von uushk_w [V] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-int"></a>
### STATUS_INT

Auslesen des Lambdaregler-Ausgangs

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_INT_WERT | real | Lambdaregler-Ausgang (fr_w) |
| STAT_INT_EINH | string | Einheit von fr_w [-] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-add"></a>
### STATUS_ADD

Auslesen der additiven Lambdaregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_ADD_WERT | real | Additive Lambdaregelung (rkat_w) |
| STAT_ADD_EINH | string | Einheit von rkat_w [%] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mul"></a>
### STATUS_MUL

Auslesen der multipikativen Lambdaregelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_MUL_WERT | real | Multipikative Lambdaregelung (fra_w) |
| STAT_MUL_EINH | string | Einheit von fra_w [-] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

Auslesen der Batteriespannung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_UBATT_WERT | real | Batteriespannung (ub) |
| STAT_UBATT_EINH | string | Einheit von ub [V] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-geberrad-adaption"></a>
### STATUS_GEBERRAD_ADAPTION

Auslesen der NWG-Adaption

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_GEBERRAD_ADAPTION_VSA_WERT | real | Ad.wert Anschlag Auslasspreizung var. NWS Bank 1 (Vsa_adp) |
| STAT_GEBERRAD_ADAPTION_VSE_WERT | real | Ad.wert Anschlag Einlasspreizung var. NWS Bank 1 (Vse_adp) |
| STAT_GEBERRAD_ADAPTION_VSA_ADP_FL_0_WERT | real | Ad.wert Flanke Auslasspreizung var. NWS (Vsa_adp_fl_0) |
| STAT_GEBERRAD_ADAPTION_VSA_ADP_FL_1_WERT | real | Ad.wert Flanke Auslasspreizung var. NWS (Vsa_adp_fl_1) |
| STAT_GEBERRAD_ADAPTION_VSA_ADP_FL_2_WERT | real | Ad.wert Flanke Auslasspreizung var. NWS (Vsa_adp_fl_2) |
| STAT_GEBERRAD_ADAPTION_VSA_ADP_FL_3_WERT | real | Ad.wert Flanke Auslasspreizung var. NWS (Vsa_adp_fl_3) |
| STAT_GEBERRAD_ADAPTION_VSE_ADP_FL_0_WERT | real | Ad.wert Flanke Einlasspreizung var. NWS (Vse_adp_fl_0) |
| STAT_GEBERRAD_ADAPTION_VSE_ADP_FL_1_WERT | real | Ad.wert Flanke Einlasspreizung var. NWS (Vse_adp_fl_1) |
| STAT_GEBERRAD_ADAPTION_VSE_ADP_FL_2_WERT | real | Ad.wert Flanke Einlasspreizung var. NWS (Vse_adp_fl_2) |
| STAT_GEBERRAD_ADAPTION_VSE_ADP_FL_3_WERT | real | Ad.wert Flanke Einlasspreizung var. NWS (Vse_adp_fl_3) |
| STAT_GEBERRAD_ADAPTION_EINH | string | Einheit von Vsa_adp und Vse_adp [Grad KW] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pwg-poti-spannung"></a>
### STATUS_PWG_POTI_SPANNUNG

Auslesen des Pedalwertgeber-Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_PWG_POTI_SPANNUNG_1_WERT | real | Spannung PWG-Poti 1 (upwg1_w) |
| STAT_PWG_POTI_SPANNUNG_EINH | string | Einheit von upwg1_w [V] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-adc"></a>
### STATUS_ADC

Auslesen der ADC-Werte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_WTSG_WERT | real | A/D-Wert SG-Innentemperatur (wtsg) |
| STAT_WTSG_EINH | string | Einheit von wtsg [V] |
| STAT_UPWG1_WERT | real | A/D-Wert Pedalwertgeber 1 (upwg1_w) |
| STAT_UPWG1_EINH | string | Einheit von upwg1_w [V] |
| STAT_UPWG2_WERT | real | A/D-Wert Pedalwertgeber 2 (upwg2_w) |
| STAT_UPWG2_EINH | string | Einheit von upwg2_w [V] |
| STAT_USHK_WERT | real | A/D-Wert Lambdasondenspannung (uushk_w) |
| STAT_USHK_EINH | string | Einheit von uushk_w [V] |
| STAT_ULSUV_WERT | real | A/D-Wert Lambdasondenspannung (uulsuv_w) |
| STAT_ULSUV_EINH | string | Einheit von uulsuv_w [V] |
| STAT_WUB_WERT | real | A/D-Wert Batteriespannung (wub) |
| STAT_WUB_EINH | string | Einheit von wub [V] |
| STAT_UDKP1V_WERT | real | A/D-Wert DK-Poti verstärkt (udkp1v_w) |
| STAT_UDKP1V_EINH | string | Einheit von udkp1v_w [V] |
| STAT_UDKP1_WERT | real | A/D-Wert DK-Poti 1 (udkp1_w) |
| STAT_UDKP1_EINH | string | Einheit von udkp1_w [V] |
| STAT_UDKP2_WERT | real | A/D-Wert DK-Poti 2 (udkp2_w) |
| STAT_UDKP2_EINH | string | Einheit von udkp2_w [V] |
| STAT_UHFM_WERT | real | A/D-Wert Heissluftmassenmesser (uhfm_w) |
| STAT_UHFM_EINH | string | Einheit von uhfm_w [V] |
| STAT_WTMOT_WERT | real | A/D-Wert Motortemperatur (wtmot) |
| STAT_WTMOT_EINH | string | Einheit von wtmot [V] |
| STAT_WTANS_WERT | real | A/D-Wert Ansauglufttemperatur (wtans) |
| STAT_WTANS_EINH | string | Einheit von wtans [V] |
| STAT_WTKA_WERT | real | A/D-Wert Kühlmitteltemperatur Kühlerausgang (wtka) |
| STAT_WTKA_EINH | string | Einheit von wtka [V] |
| STAT_UHSV_WERT | real | A/D-Wert Lambdasondenheizung vor KAT (uhsv) |
| STAT_UHSV_EINH | string | Einheit von uhsv [V] |
| STAT_UHSH_WERT | real | A/D-Wert Lambdasondenheizung hinter KAT (uhsh) |
| STAT_UHSH_EINH | string | Einheit von uhsh [V] |
| STAT_URINLSU_WERT | real | A/D-Wert LS-Innenwiderstand (LSU4.9) (urinlsu_w) |
| STAT_URINLSU_EINH | string | Einheit von urinlsu_w [V] |
| STAT_UPR1MS_WERT | real | A/D-Wert Raildruckfühler (upr1ms_w) |
| STAT_UPR1MS_EINH | string | Einheit von upr1ms_w [V] |
| STAT_UDDSS_WERT | real | A/D-Wert Saugrohrdruckfühler (uddss_w) |
| STAT_UDDSS_EINH | string | Einheit von uddss_w [V] |
| STAT_UDSU_WERT | real | A/D-Wert Umgebungsdruckfühler (udsu_w) |
| STAT_UDSU_EINH | string | Einheit von udsu_w [V] |
| STAT_UPTES_WERT | real | A/D-Wert Ausgangsstrom DMTL (uuptes_w) |
| STAT_UPTES_EINH | string | Einheit von uuptes_w [V] |
| _TEL_AUFTRAG_WTSG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_WTSG | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UPWG1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UPWG1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UPWG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UPWG2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_USHK | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_USHK | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_ULSUV | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_ULSUV | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_WUB | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_WUB | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UDKP1V | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UDKP1V | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UDKP1 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UDKP1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UDKP2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UDKP2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UHFM | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UHFM | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_WTMOT | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_WTMOT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_WTANS | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_WTANS | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_WTKA | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_WTKA | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UHSV | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UHSV | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UHSH | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UHSH | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_URINLSU | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_URINLSU | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UPR1MS | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UPR1MS | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UDDSS | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UDDSS | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UDSU | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UDSU | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_UPTES | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_UPTES | binary | Hex-Antwort von SG |

<a id="job-status-fasta1"></a>
### STATUS_FASTA1

Auslesen FASTA-Messwertblock 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_TSG_WERT | real | SG Innentemperatur (tsg) |
| STAT_TSG_EINH | string | Einheit von tsg [Grad C] |
| STAT_KRDWS_EIN | int | Bedingung KR-Notlauf (B_krdws) |
| STAT_DMVAD_WERT | real | LL-Verlustadaption (dmvad_w) |
| STAT_DMVAD_EINH | string | Einheit von dmvad_w [%] |
| STAT_DPS_WERT | real | Differenzdruck Sauganl./ Umg. (dps_w) |
| STAT_DPS_EINH | string | Einheit von dps_w [hPa] |
| STAT_DPSRAUS_WERT | real | Differenzdruckregler (dpsraus_i) |
| STAT_DPSRAUS_EINH | string | Einheit von dpsraus_i [hPa] |
| STAT_FKMSVVT_WERT | real | Multipl. Massenstromabgleich (fkmsvvt_w) |
| STAT_FKMSVVT_EINH | string | Einheit von fkmsvvt_w [-] |
| STAT_FPRSTEP_WERT | real | DK-Lernstatus Federprüfung (fprstep_c) |
| STAT_FPRSTEP_EINH | string | Einheit von fprstep_c [-] |
| STAT_LRNSTEP_WERT | real | DK-Lernstatus Anschlag (lrnstep_c) |
| STAT_LRNSTEP_EINH | string | Einheit von lrnstep_c [-] |
| STAT_MSNVVTO_WERT | real | Addiit. Massenstromabgleich (msnvvto_w) |
| STAT_MSNVVTO_EINH | string | Einheit von msnvvto_w [kg/h] |
| STAT_NNW10_WERT | real | Koeff. NN für Massenstromabgleich (nn_w1_0) |
| STAT_NNW10_EINH | string | Einheit von nn_w1_0 [-] |
| STAT_NNW11_WERT | real | Koeff. NN für Massenstromabgleich (nn_w1_1) |
| STAT_NNW11_EINH | string | Einheit von nn_w1_1 [-] |
| STAT_NNW12_WERT | real | Koeff. NN für Massenstromabgleich (nn_w1_2) |
| STAT_NNW12_EINH | string | Einheit von nn_w1_2 [-] |
| STAT_NNW20_WERT | real | Koeff. NN für Massenstromabgleich (nn_w2_0) |
| STAT_NNW20_EINH | string | Einheit von nn_w2_0 [-] |
| STAT_NNW21_WERT | real | Koeff. NN für Massenstromabgleich (nn_w2_1) |
| STAT_NNW21_EINH | string | Einheit von nn_w2_1 [-] |
| STAT_NNW22_WERT | real | Koeff. NN für Massenstromabgleich (nn_w2_2) |
| STAT_NNW22_EINH | string | Einheit von nn_w2_2 [-] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta2"></a>
### STATUS_FASTA2

Auslesen FASTA-Messwertblock 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_NSOLFASTA_WERT | real | Motorsolldrehzahl (nsol_w) |
| STAT_NSOLFASTA_EINH | string | Einheit von nsol_w [min-1] |
| STAT_RL_WERT | real | Relative Luftmasse (rl_w) |
| STAT_RL_EINH | string | Einheit von rl_w [%] |
| STAT_RLSOL_WERT | real | Soll-Luftmasse (rlsol_w) |
| STAT_RLSOL_EINH | string | Einheit von rlsol_w [%] |
| STAT_TE_WERT | real | Einspritzzeit (te_w) |
| STAT_TE_EINH | string | Einheit von te_w [ms] |
| STAT_VVTSTATUS_WERT | real | Status VVT-System (vvtstatus) |
| STAT_VVTSTATUS_EINH | string | Einheit von vvtstatus [-] |
| STAT_WDKBAFASTA_WERT | real | DK-Istwert (wdkba_w) |
| STAT_WDKBAFASTA_EINH | string | Einheit von wdkba_w [%DK] |
| STAT_WDKS_WERT | real | DK-Sollwert (wdks_w) |
| STAT_WDKS_EINH | string | Einheit von wdks_w [%] |
| STAT_WPED_WERT | real | Pedalwertgeber (wped_w) |
| STAT_WPED_EINH | string | Einheit von wped_w [%PED] |
| STAT_ZWIST_WERT | real | Zündwinkel (zwist) |
| STAT_ZWIST_EINH | string | Einheit von zwist [Grad KW] |
| STAT_MIL_EIN | int | EOBD-Lampe (B_mil) |
| STAT_DMLLRI_WERT | real | LL-I-Regler (dmllri_w) |
| STAT_DMLLRI_EINH | string | Einheit von dmllri_w [%] |
| STAT_MIMIN_WERT | real | Minimales Motormoment (mimin_w) |
| STAT_MIMIN_EINH | string | Einheit von mimin_w [%] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta3"></a>
### STATUS_FASTA3

Auslesen FASTA-Messwertblock 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_MDGEN_WERT | real | Generatormoment (mdgen) |
| STAT_MDGEN_EINH | string | Einheit von mdgen [%] |
| STAT_MDKO_WERT | real | Klimamoment (mdko) |
| STAT_MDKO_EINH | string | Einheit von mdko [%] |
| STAT_DMRLLR_WERT | real | Reservemoment (dmrllr_w) |
| STAT_DMRLLR_EINH | string | Einheit von dmrllr_w [%] |
| STAT_FS_EIN | int | Bedingung Fahrstufe (B_fs) |
| STAT_MDWAN_WERT | real | Wandlermoment (mdwan) |
| STAT_MDWAN_EINH | string | Einheit von mdwan [%] |
| STAT_DWKR_WERT | real | KR-Spätzündung (dwkr) |
| STAT_DWKR_EINH | string | Einheit von dwkr [Grad KW] |
| STAT_DZWS_WERT | real | Delta ZW aus Momentenstruktur (dzws) |
| STAT_DZWS_EINH | string | Einheit von dzws [Grad KW] |
| STAT_DFFGEN_WERT | real | Generatorerregung (dffgen) |
| STAT_DFFGEN_EINH | string | Einheit von dffgen [%] |
| STAT_TUMG_WERT | real | Umgebungstemperatur (tumg) |
| STAT_TUMG_EINH | string | Einheit von tumg [Grad C] |
| STAT_DMVADFS_WERT | real | LL-Verlustmomentenadaption mit FS (dmvadfs_w) |
| STAT_DMVADFS_EINH | string | Einheit von dmvadfs [%] |
| STAT_DMVADKO_WERT | real | LL-Verlustmomentenadaption mit AC (dmvadko_w) |
| STAT_DMVADKO_EINH | string | Einheit von dmvadko [%] |
| STAT_DLAHI_WERT | real | I-Anteil der stetigen LRHK (dlahi_w) |
| STAT_DLAHI_EINH | string | Einheit von dlahi_w [-] |
| STAT_RINH_WERT | real | Innenwiderstand LSH25 (rinh_w) |
| STAT_RINH_EINH | string | Einheit von rinh_w [Ohm] |
| STAT_DPSSOL_WERT | real | Soll-Differenzdruck (dpssol_w) |
| STAT_DPSSOL_EINH | string | Einheit von dpssol_w [hPa] |
| STAT_SONDENOFFSET_WERT | real | Delta Sondenoffset Führungsregelung (dlatrmo_w) |
| STAT_SONDENOFFSET_EINH | string | Delta Sondenoffset  Führungsregelung [-] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta4"></a>
### STATUS_FASTA4

Auslesen FASTA-Messwertblock 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_ECULOCK_EIN | int | Verriegelungsanforderung Wegfahrsperre (B_eculock) |
| STAT_LRNRDY_EIN | int | DK Lernen beendet (B_lrnrdy) |
| STAT_LLTD_EIN | int | Bedingung Teildrosselung aktiv (B_lltd) |
| STAT_LLK_EIN | int | Bedingung LL-Kennlinie (B_llk) |
| STAT_TEAKT_EIN | int | Bedingung Tankentlüftung aktiv (B_teakt) |
| STAT_VVTNOTL_EIN | int | Bedingung VVT-Notlauf (B_vvtnotl) |
| STAT_NVRBUPOK_EIN | int | Erfolgreiches RAM Backup im Flash (B_nvrbupok) |
| STAT_COPOT_WERT | real | CO-Abgleichswert (co_pot_w) |
| STAT_COPOT_EINH | string | Einheit von co_pot_w [-] |
| STAT_UPWG_WERT | real | PWG-Spannung nach Plaus.Prüf. (upwg_w) |
| STAT_UPWG_EINH | string | Einheit von upwg_w [V] |
| STAT_MINHUB_WERT | real | Minhub bei Teildrosselung (minhub_w) |
| STAT_MINHUB_EINH | string | Einheit von minhub_w [mm] |
| STAT_GVIST_WERT | real | Istwert Gleichvert. Teildrosselung (gvist) |
| STAT_GVIST_EINH | string | Einheit von gvist [-] |
| STAT_FTBR_WERT | real | Faktor Temp.korr. i. Brennraum (ftbr_w) |
| STAT_FTBR_EINH | string | Einheit von ftbr_w [-] |
| STAT_FHO_WERT | real | Höhenkorrekturfaktor (fho_w) |
| STAT_FHO_EINH | string | Einheit von fho_w [-] |
| STAT_FTVDK_WERT | real | Korrekturfaktor Temp. vor DK (ftvdk) |
| STAT_FTVDK_EINH | string | Einheit von ftvdk [-] |
| STAT_MSNVVTOLL_WERT | real | Massestrom v. KIMSALL-Integr.\| MSLG (msnvvtoll_w) |
| STAT_MSNVVTOLL_EINH | string | Einheit von msnvvtoll_w [kg/h] |
| STAT_VSESPRS_WERT | real | Sollwert Einlasspreizung variable NWS (Vse_sprs) |
| STAT_VSESPRS_EINH | string | Einheit von Vse_sprs [Grad KW] |
| STAT_VSASPRS_WERT | real | Sollwert Einlasspreizung variable NWS (Vsa_sprs) |
| STAT_VSASPRS_EINH | string | Einheit von Vsa_sprs [Grad KW] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta5"></a>
### STATUS_FASTA5

Auslesen FASTA-Messwertblock 5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_EVHUBI_WERT | real | Istwert Hubverstellung (evhubi_w) |
| STAT_EVHUBI_EINH | string | Einheit von evhubi_w  [mm] |
| STAT_EVHUBS_WERT | real | Sollwert Huibverstellung (evhubs_w) |
| STAT_EVHUBS_EINH | string | Einheit von evhubs_w [mm] |
| STAT_OFWNKADBG_WERT | real | Adaption Excenterwinkel (ofwnkadbg) |
| STAT_OFWNKADBG_EINH | string | Einheit von ofwnkadbg [] |
| STAT_KH_EIN | int | Bedingung Kat-Heizung (B_kh) |
| STAT_NSUB_EIN | int | Bedingung LL-Anhebung wegen UB (B_nsub) |
| STAT_ATMTPA_EIN | int | Bedingung Taupunkt vor KAT (B_atmtpa) |
| STAT_ATMTPK_EIN | int | Bedingung Taupunkt hinter KAT (B_atmtpk) |
| STAT_TE_EIN | int | Bedingung Tankentlüftung (B_te) |
| STAT_DFSERESZ_WERT | real | Resetzähler Plausibilitätspr. (dfseresz_w) |
| STAT_DFSERESZ_EINH | string | Einheit von dfseresz_w [] |
| STAT_DMVADFK_WERT | real | Delta Motormoment aus Verlust (dmvadfk_w) |
| STAT_DMVADFK_EINH | string | Einheit von dmvadfk_w [] |
| STAT_DMVADLL_WERT | real | Delta Motormoment aus Verlust (dmvadll_w) |
| STAT_DMVADLL_EINH | string | Einheit von dmvadll_w [] |
| STAT_EXWINKI_WERT | real | Istwert Excenterwinkel (exwinki_w) |
| STAT_EXWINKI_EINH | string | Einheit von exwinki_w [] |
| STAT_EXWINKS_WERT | real | Sollwert Excenterwinkel (exwinks_w) |
| STAT_EXWINKS_EINH | string | Einheit von exwinks_w |
| STAT_FE_WERT | int | Betriebsartenbyte (B_fe/ !! ist kein Flag) |
| STAT_FE_EINH | string | Einheit von B_fe [] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta6"></a>
### STATUS_FASTA6

Auslesen FASTA-Messwertblock 6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_FKMSVVTA_WERT | real | Faktor Massenstromabgl. langsam VVT (fkmsvvta_w) |
| STAT_FKMSVVTA_EINH | string | Einheit von fkmsvvta_w [-] |
| STAT_FOFRESZ_WERT | real | Resetzähler Lernfilter (fofresz) |
| STAT_FOFRESZ_EINH | string | Einheit von fofresz [-] |
| STAT_MSDIF_WERT | real | Massenstromdifferenz (msdif_w) |
| STAT_MSDIF_EINH | string | Einheit von msdif_w [kg/h] |
| STAT_TABGM_WERT | real | Abgastemp. vor KAT Modell (tabgm) |
| STAT_TABGM_EINH | string | Einheit von tabgm [Grad C] |
| STAT_TNSE_WERT | real | Zeitzähler ab Startende (tnse_w) |
| STAT_TNSE_EINH | string | Einheit von tnse_w [s] |
| STAT_OZRWPERM_WERT | real | Restweg aus Epsilon (ozrwperm) |
| STAT_OZRWPERM_EINH | string | Einheit von ozrwperm [-] |
| STAT_OZRWKVB_WERT | real | Restweg aus Kraftstoffverbrauch (ozrwkvb) |
| STAT_OZRWKVB_EINH | string | Einheit von ozrwkvb [km] |
| STAT_OZOELZEIT_WERT | real | Zeit seit Ölwechsel in Tage (ozoelzeit) |
| STAT_OZOELZEIT_EINH | string | Einheit von ozoelzeit [] |
| STAT_OZKVBSM_WERT | real | Verbrauchte Kraftstoffsumme (ozkvbsm_ul) |
| STAT_OZKVBSM_EINH | string | Einheit von ozkvbsm_ul [] |
| STAT_OZPERMLOW_WERT | real | Epsilon R(0) (ozpermlow) |
| STAT_OZPERMLOW_EINH | string | Einheit von ozpermlow [-] |
| STAT_OZPERMEX_WERT | real | Epsilon R(ext) (ozpermex) |
| STAT_OZPERMEX_EINH | string | Einheit von ozpermex [-] |
| STAT_OZPERMOFF_WERT | real | Epsilon R (offset) ozpermoff |
| STAT_OZPERMOFF_EINH | string | Einheit von ozpermoff [-] |
| STAT_OZKVBOG_WERT | real | Gesamter Kraftstoffbonus (ozkvbog) |
| STAT_OZKVBOG_EINH | string | Einheit von ozkvbog [-] |
| STAT_OZPERMBOG_WERT | real | Gesamter Epsilon R Bonus (ozpermbog) |
| STAT_OZPERMBOG_EINH | string | Einheit von ozpermbog [-] |
| STAT_OZOELKM_WERT | real | Gefahrene km seit letztem SI (ozoelkm) |
| STAT_OZOELKM_EINH | string | Einheit von ozoelkm [km] |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta7"></a>
### STATUS_FASTA7

Auslesen FASTA-Messwertblock 7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| STAT_NADMTLL_WERT | real | Anzahl begonnener Leckmessungen (nadmtll_w) |
| STAT_NADMTLL_EINH | string | Einheit von nadmtll_w [-] |
| STAT_NTGLM_WERT | real | Gesamtzahl durchgef. Grobleckmessungen (ntglm_w) |
| STAT_NTGLM_EINH | string | Einheit von ntglm_w [-] |
| STAT_NTKLM_WERT | real | Gesamtzahl durchgef. Kleinstleckmess. (ntklm_w) |
| STAT_NTKLM_EINH | string | Einheit von ntklm_w [-] |
| STAT_NDIPFRO_WERT | real | Anzahl abgebrochener Mess. wg. Strom (ndipfro_w) |
| STAT_NDIPFRO_EINH | string | Einheit von ndipfro_w [-] |
| STAT_NKFL_WERT | real | Anzahl abgebr. Feinleckmess. wg. Strom (nkfl) |
| STAT_NKFL_EINH | string | Einheit von nkfl [-] |
| STAT_SSLLCNT_WERT | real | Zähler für die Resets der Minhubadaption (ssllcnt) |
| STAT_SSLLCNT_EINH | string | Einheit von ssllcnt [-] |
| STAT_MINHUBFAK_WERT | real | Faktor zur Gewichtung von minhubad_w (minhubfak) |
| STAT_MINHUBFAK_EINH | string | Einheit von minhubfak [-] |
| STAT_MINADRDY_WERT | real | Minhubadaption läuft oder abgeschlossen (minadrdy) |
| STAT_MINADRDY_EINH | string | Einheit von minadrdy [-] |
| STAT_SSLL_EIN | int | Bed. f. minhub_w für TMINHUBMX am o. Anschlag (B_ssll) |
| STAT_TDAON_EIN | int | Minhubadaption aktiv (B_tdaon) |
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
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| EWS_STATUS | string | Rückgabestatus bei der Startwertinitialisierung |
| STAT_EWS_WERT | int | Rückgabewert bei der Startwertinitialisierung |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ews-empfang"></a>
### EWS_EMPFANG

EWS-Empfangsstatus auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status Jobausführung (="OKAY" wenn fehlerfrei) |
| EWS_EMPFANGSSTATUS | string | Rückgabestatus EWS-Empfang |
| EWS_STATUS_VALUE | int | Rückgabewert EWS-Empfang |
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

<a id="job-start-zwdiag"></a>
### START_ZWDIAG

CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Start-Routine ZWDIAG (0x31 3A)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAC_CH_DIAG_EXT_ADJ_IS | real | Faktor zur Korrektur des Soll-Wirkungsgrades bei Katheizen im Leerlauf Min: 0.0 Max: 1.9921875 a2l-Name: f_mrkhll_t |
| FAC_CH_DIAG_EXT_ADJ_PL | real | Faktor zur Korrektur des Soll-Wirkungsgrades bei Katheizen in der Teillast Min: 0.0 Max: 1.9921875 a2l-Name: f_mrkhtl_t |
| LV_CH_DIAG_EXT_REQ | unsigned char | Anforderung an Anpassung der geforderten Momentenreserve durch Katheizen über Tester (Leerlauf/Teillastbetrieb) Min: 0.0 Max: 3.0 a2l-Name:  B_mrkhll_t, B_mrkhtl_t |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-zwdiag"></a>
### STATUS_ZWDIAG

CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Status-Routine ZWDIAG (0x33 3A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_ZWDIAG | unsigned char | FUNKTIONSSTATUS ZWDIAG |
| STAT_FS_ZWDIAG_TEXT | string | FUNKTIONSSTATUS ZWDIAG |
| STAT_LV_DIAG_CST_ACT | unsigned char | Freigabe Diagnose zur Überwachung der Kaltstartstrategie a2l-Name: B_endcsst |
| STAT_LV_DIAG_CST_ACT_TEXT | string | Freigabe Diagnose zur Überwachung der Kaltstartstrategie |
| STAT_LV_INH_DIAG_EFF_IGA_CST | unsigned char | Flag für Sperrung der Zündwinkeldiagnose a2l-Name: B_endcsst BitMapping[0=1,1=0] |
| STAT_LV_INH_DIAG_EFF_IGA_CST_TEXT | string | Flag für Sperrung der Zündwinkeldiagnose |
| STAT_STATE_CH | unsigned char | Anforderung Katheizen bei kaltem Motor a2l-Name: B_khakt |
| STAT_STATE_CH_TEXT | string | Anforderung Katheizen bei kaltem Motor |
| STAT_T_AST_WERT | real | Zeitzähler ab Startende (16bit) a2l-Name: tnse_w Einheit: s Min: 0.0 Max: 6553.5 |
| STAT_T_AST_EINH | string | "s" |
| STAT_TCO_ST_WERT | real | Motorstarttemperatur a2l-Name: tmst Einheit: Grad C Min: -48.0 Max: 143.25 |
| STAT_TCO_ST_EINH | string | "Grad C" |
| STAT_LV_CDN_DIAG_EFF_IGA_CST_IS | unsigned char | Freigabe Berechnung der Wirkungsgradabweichung für Zündwinkeldiagnose im Leerlauf a2l-Name: B_enetkhll |
| STAT_LV_CDN_DIAG_EFF_IGA_CST_IS_TEXT | string | Freigabe Berechnung der Wirkungsgradabweichung für Zündwinkeldiagnose im Leerlauf |
| STAT_LV_CDN_DIAG_EFF_IGA_CST_PL | unsigned char | Freigabe Berechnung der Wirkungsgradabweichung für Zündwinkeldiagnose im Teillastbereich a2l-Name: B_enetkhtl |
| STAT_LV_CDN_DIAG_EFF_IGA_CST_PL_TEXT | string | Freigabe Berechnung der Wirkungsgradabweichung für Zündwinkeldiagnose im Teillastbereich |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-zwdiag"></a>
### STOP_ZWDIAG

CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Stop-Routine ZWDIAG (0x32 3A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-energiesparmode"></a>
### STATUS_ENERGIESPARMODE

0x22100A STATUS_ENERGIESPARMODE Status Energiesparmode Aktivierung: Klemme 15 = EIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENERGIESPARMODE_TEXT | string | Status Energiesparmode  00 = Passiv, 01 = Fertigung, 02 = Transport, 03 = Werkstatt EEPROM_MIRROR_stnmaxmd   Min: 0 Max: 3 |
| STAT_ENERGIESPARMODE_WERT | int | Status Energiesparmode  00 = Passiv, 01 = Fertigung, 02 = Transport, 03 = Werkstatt EEPROM_MIRROR_stnmaxmd   Min: 0 Max: 3 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-oel"></a>
### STATUS_CODIERUNG_OEL

0x223200 STATUS_CODIERUNG_OEL Codierung fuer Oelwechselintervall auslesen Aktivierung: Klemme 15 = EIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAENDERFAKTOR_1_WERT | real | Status fuer Codierung Laenderfaktor 1 OZLF1C   Min: 0 Max: 2.55 |
| STAT_LAENDERFAKTOR_2_WERT | real | Status fuer Codierung Laenderfaktor 2 OZLF2C   Min: 0 Max: 2.55 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-etkh"></a>
### STATUS_ETKH

0x2CF099 und 0x2CF19A STATUS_ETKH Auslesen der Quotient Zündwinkelwirkungsgrad-Fehlerintegral Aktivierung: Klemme 15 = EIN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ETKHLMX_WERT | real | Integrator Bank 1 etkhlmx |
| STAT_ETKHLMX_EINH | string | percent |
| STAT_ETKHTMX_WERT | real | Integrator Bank 1 etkhtmx |
| STAT_ETKHTMX_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [CBSKENNUNG](#table-cbskennung) (20 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (256 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (12 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (255 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (119 × 9)
- [FARTTYP](#table-farttyp) (253 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (285 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [VVTSTATUSBG2_2](#table-vvtstatusbg2-2) (8 × 2)
- [EWSSTART](#table-ewsstart) (5 × 2)
- [EWSEMPFANGSSTATUS](#table-ewsempfangsstatus) (15 × 2)
- [REGEL](#table-regel) (7 × 2)
- [SLSSTATUS](#table-slsstatus) (29 × 2)
- [TEVSTATUS](#table-tevstatus) (9 × 2)
- [STAGEDMTL](#table-stagedmtl) (19 × 2)
- [STAGEDMTLFREEZE](#table-stagedmtlfreeze) (23 × 2)
- [LSUSTATUS](#table-lsustatus) (5 × 2)
- [LAMBDASTATUS](#table-lambdastatus) (6 × 2)
- [KATSTATUS](#table-katstatus) (7 × 2)
- [BETRIEBSSTUNDENSTATUS](#table-betriebsstundenstatus) (4 × 2)
- [BITS](#table-bits) (102 × 4)
- [T_1BYTE_FS_DOP](#table-t-1byte-fs-dop) (11 × 2)
- [T_B_STANDARD_1BYTE_LESEN_0_1](#table-t-b-standard-1byte-lesen-0-1) (3 × 2)
- [T_ENERGIESPARMODUS_LESEN](#table-t-energiesparmodus-lesen) (4 × 2)

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

Dimensions: 20 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelag vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x04 | Filt | Mikrofilter |
| 0x06 | Br_h | Bremsbelag hinten |
| 0x07 | CSF | Dieselpartikelfilter |
| 0x08 | Batt | Batterie |
| 0x09 | QMV | QMV-H-Oel |
| 0x10 | ZKrz | Zuendkerzen |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x12 | Kfl | Kuehlfluessigkeit |
| 0x13 | H2 | H2-Check |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x15 | Efk | Einfahrkontrolle |
| 0x16 | DAD | Additiv fuer Partikelfilter |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |
| 0x23 | DKG | DK-Getriebeoel |
| 0x0A | ZKrz_a | Zuendkerzen adaptiv |
| 0x0D | NOx_a | NOx-Additiv |

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

Dimensions: 256 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xCDB7 | CDKX5E0 0xCDB7 - Botschaft (OBD-Sensor Diagnosestatus, 5E0) |
| 0x2F44 | CDKWFS 0x2F44 - EWS Manipulationsschutz |
| 0x2F46 | CDKWCA 0x2F46 - EWS Wechselcode-Abspeicherng |
| 0x2A58 | CDKVVTE 0x2A58 - Valvetronic,  Spannungsversorgung |
| 0x2F4F | CDKVFZNP 0x2F4F - Fahrzeuggeschwindigkeit, Plausibilität |
| 0x2F4E | CDKVFZE 0x2F4E - Fahrzeuggeschwindigkeit, Signal |
| 0x2F50 | CDKVAT 0x2F50 - Fahrzeuggeschwindigkeit, Plausibilität |
| 0x2B9C | CDKURRST 0x2B9C - Steuergerät, interner Fehler: Reset |
| 0x2B9B | CDKURROM 0x2B9B - Steuergerät, interner Fehler: ROM |
| 0x2B9A | CDKURRAM 0x2B9A - Steuergerät, interner Fehler: RAM |
| 0x2C3B | CDKULSU 0x2C3B - Lambdasonde vor Katalysator, nicht angesteckt |
| 0x2D76 | CDKUFSPSC 0x2D76 - DME, interner Fehler: Überwachung Fahrpedalmodul |
| 0x2D72 | CDKUFSGC 0x2D72 - DME, interner Fehler: Überwachung Hardware |
| 0x2D71 | CDKUFSGB 0x2D71 - DME, interner Fehler: Überwachung Eingangsgrößen |
| 0x2D70 | CDKUFSGA 0x2D70 - DME, interner Fehler: Überwachung Motorfunktionen |
| 0x2D6F | CDKUFRLIP 0x2D6F - DME, interner Fehler: Überwachung Luftpfad |
| 0x2D74 | CDKUFRKC 0x2D74 - DME, interner Fehler: Überwachung Kraftstoffdrucksensor |
| 0x2D75 | CDKUFNC 0x2D75 - DME, interner Fehler: Überwachung Motordrehzahl |
| 0x2D6E | CDKUFMV 0x2D6E - DME, interner Fehler: Überwachung Istmoment |
| 0x2D6D | CDKUF2SG 0x2D6D - DME, interner Fehler: Überwachung DME/DME2 |
| 0x2F8A | CDKUB 0x2F8A - Batteriespannung |
| 0x2BC0 | CDKTUMP 0x2BC0 - Umgebungstemperatursensor, Plausibilität |
| 0x2BC1 | CDKTUME 0x2BC1 - Umgebungstemperatursensor, Signal |
| 0x2EE1 | CDKTMP 0x2EE1 - Kühlmitteltemperatursensor, Plausibilität |
| 0x2EE0 | CDKTME 0x2EE0 - Kühlmitteltemperatursensor, Signal |
| 0x2EE4 | CDKTMCS 0x2EE4 - Kühlmitteltemperatursensor, Messbereich |
| 0x2EEA | CDKTKA 0x2EEA - Temperatursensor Kühleraustritt, Signal |
| 0x2EF4 | CDKTHM 0x2EF4 - Kennfeldthermostat, Mechanik |
| 0x2A19 | CDKTEVE 0x2A19 - Tankentlüftungsventil, Ansteuerung |
| 0x2A15 | CDKTESG 0x2A15 - Tankentlüftungs- und Spülluftsystem, Feinleck |
| 0x2A1A | CDKTES 0x2A1A - Tankentlüftungssystem, Funktion |
| 0x2F09 | CDKTAR 0x2F09 - Ansauglufttemperatursensor, Plausibilität |
| 0x2F08 | CDKTAE 0x2F08 - Ansauglufttemperatursensor, Signal |
| 0x2F0B | CDKTACS 0x2F0B - Ansauglufttemperatursensor, Plausibilität, Kaltstart |
| 0x29DD | CDKSWE 0x29DD - Schlechtwegstreckenerkennung |
| 0x2F59 | CDKSTS 0x2F59 - Startautomatik, Startsignal |
| 0x2F5A | CDKSTA 0x2F5A - Startautomatik |
| 0x2BAC | CDKSGAPL 0x2BAC - DME, DME2: Programmstandsunterschied |
| 0x2BAD | CDKSGA 0x2BAD - DME,DME2: Hardware, Plausibilität |
| 0x30E8 | CDKRLMAX 0x30E8 - Füllungsbegrenzung |
| 0x29E7 | CDKRKAT 0x29E7 - Gemischadaption im Leerlauf pro Zeit |
| 0x2A2A | CDKRBVE 0x2A2A - Rücklaufbelüftungsventil, Ansteuerung |
| 0x2F77 | CDKPUR 0x2F77 - Umgebungsdrucksensor, Plausibilität |
| 0x2F78 | CDKPUE 0x2F78 - DME, interner Fehler: Umgebungsdrucksensor |
| 0x2F7B | CDKPOELS 0x2F7B - Öldruckschalter, Plausibilität |
| 0x2C49 | CDKPLLSU 0x2C49 - Lambdasonde vor Katalysator, Plausibilität |
| 0x2B66 | CDKPHM 0x2B66 - Nockenwellensensor, Master |
| 0x2B63 | CDKPH2 0x2B63 - Nockenwellensensor, Auslass |
| 0x2B62 | CDKPH 0x2B62 - Nockenwellensensor, Einlass |
| 0x2D29 | CDKPDDSS 0x2D29 - Differenzdrucksensor, Saugrohr: Plausibilität |
| 0x2E9F | CDKOEZS 0x2E9F - Ölzustandssensor |
| 0x2A8E | CDKNWEKW 0x2A8E - Einlassnockenwelle, Zahnversatz zur Kurbelwelle |
| 0x2A90 | CDKNWAKW 0x2A90 - Auslassnockenwelle, Zahnversatz zur Kurbelwelle |
| 0x2B98 | CDKNVRMON 0x2B98 - Steuergerät, interner Fehler: RAM Backup, Plausibilität |
| 0x2B99 | CDKNVRBUP 0x2B99 - Steuergerät, interner Fehler: RAM Backup |
| 0x2B5C | CDKN 0x2B5C - Kurbelwellensensor, Signal |
| 0x2F17 | CDKMTOEL 0x2F17 - Motoröltemperatur, zeitweise zu hoch, EGS-Zwangsschaltung |
| 0x29E4 | CDKMSVE 0x29E4 - Mengensteuerventil, Ansteuerung |
| 0x2EFE | CDKMLE 0x2EFE - Elektrolüfter, Ansteuerung |
| 0x2EFC | CDKMLE 0x2EFC - Elektrolüfter 2, Ansteuerung |
| 0x2A6F | CDKMINHUB 0x2A6F - Valvetronic, Minimalhub |
| 0x2BA7 | CDKMDB 0x2BA7 - DME, interner Fehler: Überwachung Momentenbegrenzung Ebene 1 |
| 0x29D6 | CDKMD11 0x29D6 - Verbrennungsaussetzer, Zylinder 10 |
| 0x29D0 | CDKMD10 0x29D0 - Verbrennungsaussetzer, Zylinder 4 |
| 0x29D4 | CDKMD09 0x29D4 - Verbrennungsaussetzer, Zylinder 8 |
| 0x29CE | CDKMD08 0x29CE - Verbrennungsaussetzer, Zylinder 2 |
| 0x29D8 | CDKMD07 0x29D8 - Verbrennungsaussetzer, Zylinder 12 |
| 0x29D2 | CDKMD06 0x29D2 - Verbrennungsaussetzer, Zylinder 6 |
| 0x29D5 | CDKMD05 0x29D5 - Verbrennungsaussetzer, Zylinder 9 |
| 0x29CF | CDKMD04 0x29CF - Verbrennungsaussetzer, Zylinder 3 |
| 0x29D7 | CDKMD03 0x29D7 - Verbrennungsaussetzer, Zylinder 11 |
| 0x29D1 | CDKMD02 0x29D1 - Verbrennungsaussetzer, Zylinder 5 |
| 0x29D3 | CDKMD01 0x29D3 - Verbrennungsaussetzer, Zylinder 7 |
| 0x29CD | CDKMD00 0x29CD - Verbrennungsaussetzer, Zylinder 1 |
| 0x29CC | CDKMD 0x29CC - Verbrennungsaussetzer, mehrere Zylinder |
| 0x2D77 | CDKMBV 0x2D77 - DME, DME2: Momentenvergleich |
| 0x2C24 | CDKLSVV 0x2C24 - Lambdasonden vor Katalysator, vertauscht |
| 0x2C61 | CDKLSVE 0x2C61 - Lamdasonde vor Katalysator, elektrischer Fehler |
| 0x2C53 | CDKLSUVM 0x2C53 - Lambdasonde vor Katalysator, virtuelle Masse |
| 0x2C51 | CDKLSUUN 0x2C51 - Lambdasonde vor Katalysator, Nernstleitung |
| 0x2C47 | CDKLSUKS 0x2C47 - Lambdasonde vor Katalysator, Sondenleitungen |
| 0x2C4D | CDKLSUIP 0x2C4D - Lambdasonde vor Katalysator, Pumpstromleitung |
| 0x2C4F | CDKLSUIA 0x2C4F - Lambdasonde vor Katalysator, Abgleichleitung |
| 0x2C71 | CDKLSH 0x2C71 - Lambdasonde nach Katalysator |
| 0x2B82 | CDKLLRKH 0x2B82 - Leerlaufregelung bei Katalysatorbeheizung |
| 0x2B81 | CDKLLRH 0x2B81 - Leerlaufregelung bei homogenem Betrieb |
| 0x2AE2 | CDKLLRCS 0x2AE2 - Leerlaufregelung, Plausibilität, Kaltstart |
| 0x2C6D | CDKLASH 0x2C6D - Lambdasonde nach Katalysator, Alterung |
| 0x2E6A | CDKKS3 0x2E6A - Klopfsensorsignal 3 |
| 0x2E69 | CDKKS2 0x2E69 - Klopfsensorsignal 2 |
| 0x2E68 | CDKKS1 0x2E68 - Klopfsensorsignal 1 |
| 0x2E73 | CDKKRSPI 0x2E73 - Steuergerät, interner Fehler: Klopfsensorbaustein |
| 0x2E72 | CDKKRIC 0x2E72 - Steuergerät, interner Fehler: Klopfsensorbaustein |
| 0x29F4 | CDKKAT 0x29F4 - Katalysatorkonvertierung |
| 0x2C4B | CDKICLSU 0x2C4B - Steuergerät, interner Fehler: Lambdasondenbaustein |
| 0x2C9C | CDKHSVE 0x2C9C - Lambdasondenbeheizung vor Katalysator, Ansteuerung |
| 0x2CA0 | CDKHSV 0x2CA0 - Lambdasondenbeheizung vor Katalysator |
| 0x2C9E | CDKHSHE 0x2C9E - Lambdasondenbeheizung nach Katalysator, Ansteuerung |
| 0x2CA8 | CDKHSH 0x2CA8 - Lambdasondenbeheizung nach Katalysator, Funktion |
| 0x2D13 | CDKHFMR 0x2D13 - Luftmassenmesser, Rationalität |
| 0x2D0F | CDKHFME 0x2D0F - Luftmassenmesser, Signal |
| 0x2C37 | CDKHELSU 0x2C37 - Lambdasonde vor Katalysator, Heizereinkopplung |
| 0x29F1 | CDKHDRPL 0x29F1 - Kraftstoffdruck, Plausibilität |
| 0x2B2C | CDKHDRKH 0x2B2C - Kraftstoffhochdruck, Plausibilität, Kaltstart |
| 0x29E3 | CDKHDR 0x29E3 - Kraftstoffdruckregelung, Plausibilität |
| 0x2E60 | CDKHDEVK 0x2E60 - HDEV-Steuergerät, interner Fehler: Kommunikation |
| 0x30B5 | CDKHDEV6 0x30B5 - Einspritzventil Zylinder 10, Ansteuerung |
| 0x30AF | CDKHDEV6 0x30AF - Einspritzventil Zylinder 4, Ansteuerung |
| 0x30B3 | CDKHDEV5 0x30B3 - Einspritzventil Zylinder 8, Ansteuerung |
| 0x30AD | CDKHDEV5 0x30AD - Einspritzventil Zylinder 2, Ansteuerung |
| 0x30B7 | CDKHDEV4 0x30B7 - Einspritzventil Zylinder 12, Ansteuerung |
| 0x30B1 | CDKHDEV4 0x30B1 - Einspritzventil Zylinder 6, Ansteuerung |
| 0x30B4 | CDKHDEV3 0x30B4 - Einspritzventil Zylinder 9, Ansteuerung |
| 0x30AE | CDKHDEV3 0x30AE - Einspritzventil Zylinder 3, Ansteuerung |
| 0x30B6 | CDKHDEV2 0x30B6 - Einspritzventil Zylinder 11, Ansteuerung |
| 0x30B0 | CDKHDEV2 0x30B0 - Einspritzventil Zylinder 5, Ansteuerung |
| 0x30B2 | CDKHDEV1 0x30B2 - Einspritzventil Zylinder 7, Ansteuerung |
| 0x30AC | CDKHDEV1 0x30AC - Einspritzventil Zylinder 1, Ansteuerung |
| 0x2E53 | CDKHBOOST6 0x2E53 - Booster Hochdruckeinspritzventil  10 |
| 0x2E4D | CDKHBOOST6 0x2E4D - Booster Hochdruckeinspritzventil  4 |
| 0x2E52 | CDKHBOOST5 0x2E52 - Booster Hochdruckeinspritzventil  8 |
| 0x2E4C | CDKHBOOST5 0x2E4C - Booster Hochdruckeinspritzventil  2 |
| 0x2E51 | CDKHBOOST4 0x2E51 - Booster Hochdruckeinspritzventil  12 |
| 0x2E4B | CDKHBOOST4 0x2E4B - Booster Hochdruckeinspritzventil  6 |
| 0x2E50 | CDKHBOOST3 0x2E50 - Booster Hochdruckeinspritzventil  9 |
| 0x2E4A | CDKHBOOST3 0x2E4A - Booster Hochdruckeinspritzventil  3 |
| 0x2E4F | CDKHBOOST2 0x2E4F - Booster Hochdruckeinspritzventil  11 |
| 0x2E49 | CDKHBOOST2 0x2E49 - Booster Hochdruckeinspritzventil  5 |
| 0x2E4E | CDKHBOOST1 0x2E4E - Booster Hochdruckeinspritzventil  7 |
| 0x2E48 | CDKHBOOST1 0x2E48 - Booster Hochdruckeinspritzventil  1 |
| 0x2C31 | CDKFTDLA 0x2C31 - Lambdasonde vor Katalysator, Trimmregelung |
| 0x2A1E | CDKFSTSI 0x2A1E - Tankfüllstand, Signal |
| 0x2A21 | CDKFSTS2 0x2A21 - Tankfüllstand 2, Signal |
| 0x2A22 | CDKFSTP 0x2A22 - Tankfüllstand, Korrelation |
| 0x2A1D | CDKFSTP 0x2A1D - Tankfüllstand, Plausibilität |
| 0x29ED | CDKFRAU 0x29ED - Gemischadaption, unterer Drehzahlbereich |
| 0x29E5 | CDKFRAO 0x29E5 - Gemischadaption, oberer Drehzahlbereich |
| 0x2D1A | CDKFPP 0x2D1A - Fahrpedalmodul, Pedalwertgeber |
| 0x2D37 | CDKFP2PRG 0x2D37 - Fahrpedalmodul, Pedalwertgeber 2, Arbeitsbereich |
| 0x2D1C | CDKFP2P 0x2D1C - Fahrpedalmodul, Pedalwertgeber Signal 2 |
| 0x2D36 | CDKFP1PRG 0x2D36 - Fahrpedalmodul, Pedalwertgeber 1, Arbeitsbereich |
| 0x2D1B | CDKFP1P 0x2D1B - Fahrpedalmodul, Pedalwertgeber Signal 1 |
| 0x29F0 | CDKFMAS 0x29F0 - Gemischadaption 2, Summenfehler |
| 0x29EF | CDKFMAS 0x29EF - Gemischadaption, Summenfehler |
| 0x2E45 | CDKEVLE6 0x2E45 - HDEV-Steuergerät Leitung 4, Ansteuerung |
| 0x2E3F | CDKEVLE6 0x2E3F - HDEV-Steuergerät Leitung 10, Ansteuerung |
| 0x2E44 | CDKEVLE5 0x2E44 - HDEV-Steuergerät Leitung 2, Ansteuerung |
| 0x2E3E | CDKEVLE5 0x2E3E - HDEV-Steuergerät Leitung 8, Ansteuerung |
| 0x2E43 | CDKEVLE4 0x2E43 - HDEV-Steuergerät Leitung 6, Ansteuerung |
| 0x2E3D | CDKEVLE4 0x2E3D - HDEV-Steuergerät Leitung 12, Ansteuerung |
| 0x2E42 | CDKEVLE3 0x2E42 - HDEV-Steuergerät Leitung 3, Ansteuerung |
| 0x2E3C | CDKEVLE3 0x2E3C - HDEV-Steuergerät Leitung 9, Ansteuerung |
| 0x2E47 | CDKEVLE2 0x2E47 - HDEV-Steuergerät Leitung 11, Ansteuerung |
| 0x2E41 | CDKEVLE2 0x2E41 - HDEV-Steuergerät Leitung 5, Ansteuerung |
| 0x2E46 | CDKEVLE1 0x2E46 - HDEV-Steuergerät Leitung 7, Ansteuerung |
| 0x2E40 | CDKEVLE1 0x2E40 - HDEV-Steuergerät Leitung 1, Ansteuerung |
| 0x2EF5 | CDKETS 0x2EF5 - Kennfeldthermostat, Ansteuerung |
| 0x2E7B | CDKETAKHT 0x2E7B - Zündwinkelverstellung in Teillast, Kaltstart |
| 0x2E7A | CDKETAKHL 0x2E7A - Zündwinkelverstellung im Leerlauf, Kaltstart |
| 0x2A80 | CDKENWSE 0x2A80 - Einlass-VANOS, Ansteuerung |
| 0x2A8A | CDKENWSAD 0x2A8A - Einlass-VANOS, Adaption Anschlag |
| 0x2A83 | CDKENWS 0x2A83 - Einlass-VANOS |
| 0x2A79 | CDKENWCX 0x2A79 - VANOS, Einlass, Kaltstart |
| 0x2A7C | CDKENWCS 0x2A7C - VANOS, Einlass, Kaltstart |
| 0x2F71 | CDKELS 0x2F71 - E-Box-Lüfter, Ansteuerung |
| 0x2B7F | CDKEGFE 0x2B7F - Abgleich Drosselklappe-Luftmassenmesser |
| 0x2E6F | CDKDZKUB1 0x2E6F - Zündung 2, Überwachung: Brenndauer |
| 0x2E6E | CDKDZKUB1 0x2E6E - Zündung, Überwachung: Brenndauer |
| 0x2E2D | CDKDZKU5 0x2E2D - Zündspule Zylinder 10 |
| 0x2E27 | CDKDZKU5 0x2E27 - Zündspule Zylinder 4 |
| 0x2E2B | CDKDZKU4 0x2E2B - Zündspule Zylinder 8 |
| 0x2E25 | CDKDZKU4 0x2E25 - Zündspule Zylinder 2 |
| 0x2E2F | CDKDZKU3 0x2E2F - Zündspule Zylinder 12 |
| 0x2E29 | CDKDZKU3 0x2E29 - Zündspule Zylinder 6 |
| 0x2E2C | CDKDZKU2 0x2E2C - Zündspule Zylinder 9 |
| 0x2E26 | CDKDZKU2 0x2E26 - Zündspule Zylinder 3 |
| 0x2E2E | CDKDZKU1 0x2E2E - Zündspule Zylinder 11 |
| 0x2E28 | CDKDZKU1 0x2E28 - Zündspule Zylinder 5 |
| 0x2E2A | CDKDZKU0 0x2E2A - Zündspule Zylinder 7 |
| 0x2E24 | CDKDZKU0 0x2E24 - Zündspule Zylinder 1 |
| 0x2C39 | CDKDYLSU 0x2C39 - Lambdasonde vor Katalysator, Dynamik |
| 0x2C84 | CDKDYLSH 0x2C84 - Lambdasonde nach Katalysator, Dynamik |
| 0x2F45 | CDKDWA 0x2F45 - Schnittstelle EWS-DME |
| 0x2A5F | CDKDVUSE 0x2A5F - Valvetronic, Exzenterwellensensor: Spannungsversorgung |
| 0x2A69 | CDKDVULV 0x2A69 - Valvetronic, Stellmotor: Spannungsversorgung |
| 0x2A63 | CDKDVSTE 0x2A63 - Valvetronic, Stellmotor: Überwachung Schwergängigkeit, Drehrichtung |
| 0x2A6B | CDKDVPMN 0x2A6B - Valvetronic, Leistungsbegrenzung |
| 0x2A5D | CDKDVPLA 0x2A5D - Valvetronic, Exzenterwellensensor: Plausibilität |
| 0x2A6D | CDKDVOVL 0x2A6D - Valvetronic, elektrischer Überlastschutz |
| 0x2A61 | CDKDVLRN 0x2A61 - Valvetronic, Verstellbereich |
| 0x2A65 | CDKDVFSG 0x2A65 - Valvetronic,  interner Fehler |
| 0x2A5B | CDKDVFRS 0x2A5B - Valvetronic, Exzenterwellensensor: Referenz |
| 0x2A59 | CDKDVFFS 0x2A59 - Valvetronic, Exzenterwellensensor: Führung |
| 0x2CFF | CDKDVEV 0x2CFF - Drosselklappensteller, Verstärkerabgleich |
| 0x2D05 | CDKDVEUW 0x2D05 - Drosselklappensteller, Abbruch bei UMA-Wiederlernen |
| 0x2D03 | CDKDVEUB 0x2D03 - Drosselklappensteller, Abbruch Adaption wegen Umweltbedingungen |
| 0x2D04 | CDKDVEU 0x2D04 - Drosselklappensteller, Prüfung unterer Anschlag |
| 0x2A67 | CDKDVEST 0x2A67 - Valvetronic, Stellmotor: Ansteuerung |
| 0x2CF0 | CDKDVER 0x2CF0 - Drosselklappensteller, Regelbereich |
| 0x2D02 | CDKDVEN 0x2D02 - Drosselklappensteller, Notluftpunkt |
| 0x2CF1 | CDKDVEL 0x2CF1 - Drosselklappensteller, Positionsüberwachung |
| 0x2D01 | CDKDVEFO 0x2D01 - Drosselklappensteller, Federprüfung öffnende Feder |
| 0x2D00 | CDKDVEF 0x2D00 - Drosselklappensteller, Federprüfung schliessende Feder |
| 0x2CEF | CDKDVEE 0x2CEF - Drosselklappensteller, Ansteuerung |
| 0x2DDE | CDKDVCAN 0x2DDE - Local-CAN Kommunikation |
| 0x2A6C | CDKDVAN 0x2A6C - Valvetronic, Position bei Neustart: Plausibilität |
| 0x29E2 | CDKDSKV 0x29E2 - Kraftstoffeinspritzleiste, Drucksensorsignal |
| 0x2A17 | CDKDMTL 0x2A17 - DMTL, Systemfehler |
| 0x2A16 | CDKDMTKNM 0x2A16 - Tankentlüftungs- und Spülluftsystem, Feinstleck |
| 0x2A14 | CDKDMTK 0x2A14 - Tankentlüftungs- und Spülluftsystem, Feinstleck |
| 0x2A13 | CDKDMPME 0x2A13 - DMTL-Leckdiagnosepumpe, Ansteuerung |
| 0x2A12 | CDKDMMVE 0x2A12 - DMTL-Magnetventil, Ansteuerung |
| 0x2CFA | CDKDK2P 0x2CFA - Drosselklappenpotenziometer 2 |
| 0x2CF9 | CDKDK1P 0x2CF9 - Drosselklappenpotenziometer 1 |
| 0x2CF8 | CDKDK 0x2CF8 - Drosselklappenpotenziometer |
| 0x2A18 | CDKDHDMTE 0x2A18 - DMTL, Heizung: Ansteuerung |
| 0x2E98 | CDKDGENBS 0x2E98 - Generator, Kommunikation |
| 0x2E9A | CDKDGENB2 0x2E9A - Generator 2, Kommunikation |
| 0x2E99 | CDKDGEN2 0x2E99 - Generator 2 |
| 0x2E97 | CDKDGEN 0x2E97 - Generator |
| 0x2D28 | CDKDDSS 0x2D28 - Differenzdrucksensor, Saugrohr: Signal |
| 0x2DDD | CDKCVVT 0x2DDD - Botschaft vom Valvetronic-Steuergerät fehlt |
| 0x2F80 | CDKCUHR 0x2F80 - Motorabstellzeit, Plausibilität |
| 0x2DDC | CDKCSZL 0x2DDC - Botschaft vom SZL fehlt |
| 0x2DC1 | CDKCPWML 0x2DC1 - Botschaft vom Powermodul fehlt |
| 0x2FA3 | CDKCOD 0x2FA3 - Codierung fehlt |
| 0x2F87 | CDKCNCLKT 0x2F87 - Motorabstellzeit |
| 0x2F7E | CDKCNCLKL 0x2F7E - Motorabstellzeit, Plausibilität |
| 0x2F7F | CDKCNCLKH 0x2F7F - Motorabstellzeit, Plausibilität |
| 0x2F88 | CDKCNCLKD 0x2F88 - Motorabstellzeit |
| 0x2DCF | CDKCINS 0x2DCF - CAN, Instrumentenkombination: Signalfehler |
| 0x2DDB | CDKCIHKA 0x2DDB - CAN, IHKA: Signalfehler |
| 0x30D4 | CDKCHDEV 0x30D4 - Botschaft vom HDEV fehlt |
| 0xCDDD | CDKCGE 0xCDDD - Botschaft (Getriebedaten, BA) |
| 0x2DE6 | CDKCDM 0x2DE6 - Local-CAN, DME/DME2: Kommunikation |
| 0x2DDA | CDKCCAS 0x2DDA - CAN, CAS: Signalfehler |
| 0xCDE0 | CDKCAS 0xCDE0 - Botschaft (Klemmenstatus, 130) |
| 0x2DD7 | CDKCAS 0x2DD7 - Botschaft vom DSC fehlt, Timeout |
| 0x2DD9 | CDKCARS 0x2DD9 - CAN, ARS: Signalfehler |
| 0xCDCB | CDKCANB 0xCDCB - Local-CAN Kommunikationsfehler |
| 0xCD8B | CDKCANB 0xCD8B - Local-CAN Kommunikationsfehler |
| 0xCDC7 | CDKCANA 0xCDC7 - PT-CAN Kommunikationsfehler |
| 0xCD87 | CDKCANA 0xCD87 - PT-CAN Kommunikationsfehler |
| 0x2DBF | CDKCACC 0x2DBF - CAN, ACC: Signalfehler |
| 0x2F62 | CDKBREMS 0x2F62 - Bremslichtschalter |
| 0x2B5D | CDKBM 0x2B5D - Kurbelwellensensor, Plausibilität |
| 0x2B7A | CDKASVE 0x2B7A - Rücklaufabsperrventil, Ansteuerung |
| 0x2A85 | CDKANWSE 0x2A85 - Auslass-VANOS, Ansteuerung |
| 0x2A8C | CDKANWSAD 0x2A8C - Auslass-VANOS, Adaption Anschlag |
| 0x2A88 | CDKANWS 0x2A88 - Auslass-VANOS |
| 0x2A78 | CDKANWCX 0x2A78 - VANOS, Auslass, Kaltstart |
| 0x2A7A | CDKANWCS 0x2A7A - VANOS, Auslass, Kaltstart |
| 0x2B84 | CDKANSKE 0x2B84 - Zusatzluftklappe, Ansteuerung |
| 0x2F6C | CDKAKRE 0x2F6C - Abgasklappe, Ansteuerung |
| 0x0000 | 0000 FehlerOrt nicht bedatet |
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
| xx1xxxxx | 61 | MIL Entprellung war bereits erreicht, HLC=0 |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 255 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x0000 | 0x00FF | 0x00FF | 0x00FF | 0x00FF |
| 0x29CC | 0x000A | 0x00D6 | 0x0012 | 0x003C |
| 0x29CD | 0x000A | 0x00D6 | 0x0012 | 0x003C |
| 0x29CE | 0x000A | 0x00D6 | 0x0012 | 0x003C |
| 0x29CF | 0x000A | 0x00D6 | 0x0012 | 0x003C |
| 0x29D0 | 0x000A | 0x00D6 | 0x0012 | 0x003C |
| 0x29D1 | 0x000A | 0x00D6 | 0x0012 | 0x003C |
| 0x29D2 | 0x000A | 0x00D6 | 0x0012 | 0x003C |
| 0x29D3 | 0x000A | 0x00D6 | 0x0012 | 0x003C |
| 0x29D4 | 0x000A | 0x00D6 | 0x0012 | 0x003C |
| 0x29D5 | 0x000A | 0x00D6 | 0x0012 | 0x003C |
| 0x29D6 | 0x000A | 0x00D6 | 0x0012 | 0x003C |
| 0x29D7 | 0x000A | 0x00D6 | 0x0012 | 0x003C |
| 0x29D8 | 0x000A | 0x00D6 | 0x0012 | 0x003C |
| 0x29DD | 0x000A | 0x001A | 0x000B | 0x008C |
| 0x29E2 | 0x000A | 0x0012 | 0x0014 | 0x003C |
| 0x29E3 | 0x000A | 0x001A | 0x003C | 0x0035 |
| 0x29E4 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x29E5 | 0x000B | 0x001A | 0x0006 | 0x0005 |
| 0x29E7 | 0x000A | 0x0013 | 0x003C | 0x0005 |
| 0x29ED | 0x000A | 0x001A | 0x00AC | 0x0006 |
| 0x29EF | 0x0005 | 0x0006 | 0x001A | 0x000A |
| 0x29F0 | 0x0005 | 0x0006 | 0x001A | 0x000A |
| 0x29F4 | 0x00A3 | 0x001A | 0x00BF | 0x00C1 |
| 0x2A12 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A13 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A14 | 0x003C | 0x0035 | 0x0024 | 0x0014 |
| 0x2A15 | 0x003C | 0x0035 | 0x0024 | 0x0014 |
| 0x2A16 | 0x003C | 0x0035 | 0x0024 | 0x0014 |
| 0x2A17 | 0x003C | 0x0035 | 0x0024 | 0x0014 |
| 0x2A18 | 0x000A | 0x0014 | 0x0024 | 0x000B |
| 0x2A19 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A1A | 0x0012 | 0x0013 | 0x0041 | 0x00BD |
| 0x2A1D | 0x000A | 0x003C | 0x0014 | 0x000B |
| 0x2A1E | 0x000A | 0x003C | 0x0014 | 0x000B |
| 0x2A21 | 0x000A | 0x003C | 0x0014 | 0x000B |
| 0x2A22 | 0x000A | 0x003C | 0x0014 | 0x000B |
| 0x2A2A | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A58 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A59 | 0x000A | 0x0014 | 0x0012 | 0x00C5 |
| 0x2A5B | 0x000A | 0x0014 | 0x0012 | 0x00C5 |
| 0x2A5D | 0x000A | 0x0014 | 0x0012 | 0x00C3 |
| 0x2A5F | 0x000A | 0x0014 | 0x0012 | 0x0024 |
| 0x2A61 | 0x000A | 0x0014 | 0x0012 | 0x0024 |
| 0x2A63 | 0x000A | 0x0014 | 0x0012 | 0x00C5 |
| 0x2A65 | 0x000A | 0x0014 | 0x0012 | 0x0024 |
| 0x2A67 | 0x000A | 0x0014 | 0x0012 | 0x00C5 |
| 0x2A69 | 0x000A | 0x0014 | 0x0012 | 0x0024 |
| 0x2A6B | 0x000A | 0x0014 | 0x0012 | 0x00C5 |
| 0x2A6C | 0x000A | 0x0014 | 0x0012 | 0x00BE |
| 0x2A6D | 0x000A | 0x008C | 0x0012 | 0x00C5 |
| 0x2A6F | 0x0012 | 0x00BE | 0x000A | 0x001A |
| 0x2A78 | 0x000A | 0x001A | 0x00FF | 0x00FF |
| 0x2A79 | 0x000A | 0x001A | 0x00FF | 0x00FF |
| 0x2A7A | 0x000A | 0x001A | 0x00FF | 0x00FF |
| 0x2A7C | 0x000A | 0x001A | 0x00FF | 0x00FF |
| 0x2A80 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A83 | 0x000A | 0x001A | 0x0012 | 0x0014 |
| 0x2A85 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2A88 | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A8A | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A8C | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A8E | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2A90 | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2AE2 | 0x000A | 0x003E | 0x0024 | 0x0014 |
| 0x2B2C | 0x000A | 0x00FF | 0x00FF | 0x003E |
| 0x2B5C | 0x000A | 0x0012 | 0x0024 | 0x0014 |
| 0x2B5D | 0x000A | 0x0012 | 0x0024 | 0x0014 |
| 0x2B62 | 0x000A | 0x0012 | 0x0024 | 0x0014 |
| 0x2B63 | 0x000A | 0x0012 | 0x0024 | 0x0014 |
| 0x2B66 | 0x000A | 0x0012 | 0x0024 | 0x0014 |
| 0x2B7A | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2B7F | 0x0011 | 0x0015 | 0x0013 | 0x0035 |
| 0x2B81 | 0x000A | 0x001A | 0x0014 | 0x0015 |
| 0x2B82 | 0x000A | 0x001A | 0x0014 | 0x0015 |
| 0x2B84 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2B98 | 0x0014 | 0x00BE | 0x0012 | 0x0024 |
| 0x2B99 | 0x000A | 0x0014 | 0x0012 | 0x00BE |
| 0x2B9A | 0x000A | 0x001A | 0x001F | 0x0022 |
| 0x2B9B | 0x000A | 0x001A | 0x001F | 0x0022 |
| 0x2B9C | 0x000A | 0x001A | 0x001F | 0x0022 |
| 0x2BA7 | 0x000A | 0x0023 | 0x001A | 0x0012 |
| 0x2BAC | 0x000A | 0x001A | 0x0014 | 0x000B |
| 0x2BAD | 0x0014 | 0x0013 | 0x000A | 0x0012 |
| 0x2BC0 | 0x0012 | 0x0013 | 0x0024 | 0x0014 |
| 0x2BC1 | 0x0012 | 0x0013 | 0x0024 | 0x0014 |
| 0x2C24 | 0x0012 | 0x008C | 0x00A6 | 0x00A8 |
| 0x2C31 | 0x009D | 0x00A8 | 0x0017 | 0x0085 |
| 0x2C37 | 0x0082 | 0x00A8 | 0x0029 | 0x003C |
| 0x2C39 | 0x00AA | 0x00B0 | 0x00A8 | 0x0085 |
| 0x2C3B | 0x008C | 0x00A8 | 0x0017 | 0x0044 |
| 0x2C47 | 0x0014 | 0x000B | 0x00A8 | 0x009F |
| 0x2C49 | 0x009D | 0x00A8 | 0x0017 | 0x0085 |
| 0x2C4B | 0x009F | 0x008C | 0x0014 | 0x00A8 |
| 0x2C4D | 0x00A8 | 0x0082 | 0x0044 | 0x009F |
| 0x2C4F | 0x00A8 | 0x0082 | 0x0044 | 0x008C |
| 0x2C51 | 0x00A8 | 0x0082 | 0x0044 | 0x009F |
| 0x2C53 | 0x0014 | 0x00A8 | 0x0082 | 0x009F |
| 0x2C61 | 0x0029 | 0x0044 | 0x00A8 | 0x000B |
| 0x2C6D | 0x000A | 0x002B | 0x0033 | 0x0017 |
| 0x2C71 | 0x002B | 0x008C | 0x0033 | 0x0017 |
| 0x2C84 | 0x002B | 0x008C | 0x0033 | 0x0017 |
| 0x2C9C | 0x000B | 0x008C | 0x0014 | 0x0044 |
| 0x2C9E | 0x007E | 0x002F | 0x002B | 0x0033 |
| 0x2CA0 | 0x000B | 0x008C | 0x0029 | 0x0044 |
| 0x2CA8 | 0x007E | 0x0017 | 0x002B | 0x0033 |
| 0x2CEF | 0x0014 | 0x0012 | 0x0015 | 0x0028 |
| 0x2CF0 | 0x0014 | 0x0013 | 0x0015 | 0x0028 |
| 0x2CF1 | 0x0014 | 0x0013 | 0x0015 | 0x0028 |
| 0x2CF8 | 0x000A | 0x0015 | 0x0026 | 0x0027 |
| 0x2CF9 | 0x000A | 0x0028 | 0x0024 | 0x0027 |
| 0x2CFA | 0x000A | 0x0028 | 0x0024 | 0x0026 |
| 0x2CFF | 0x0014 | 0x0013 | 0x0026 | 0x0065 |
| 0x2D00 | 0x0014 | 0x0013 | 0x0015 | 0x0064 |
| 0x2D01 | 0x0014 | 0x0013 | 0x0015 | 0x0064 |
| 0x2D02 | 0x0014 | 0x0013 | 0x0064 | 0x0076 |
| 0x2D03 | 0x000A | 0x0014 | 0x0013 | 0x0023 |
| 0x2D04 | 0x0014 | 0x0013 | 0x0026 | 0x0065 |
| 0x2D05 | 0x000A | 0x0014 | 0x0013 | 0x0023 |
| 0x2D0F | 0x000A | 0x0013 | 0x0015 | 0x0071 |
| 0x2D13 | 0x000A | 0x0013 | 0x0015 | 0x0071 |
| 0x2D1A | 0x000A | 0x0023 | 0x001B | 0x001D |
| 0x2D1B | 0x000A | 0x0023 | 0x001B | 0x001D |
| 0x2D1C | 0x000A | 0x0023 | 0x001B | 0x001D |
| 0x2D28 | 0x000A | 0x001A | 0x0012 | 0x0014 |
| 0x2D29 | 0x000A | 0x001A | 0x0012 | 0x00C7 |
| 0x2D36 | 0x000A | 0x001B | 0x001C | 0x0014 |
| 0x2D37 | 0x000A | 0x001B | 0x001C | 0x0014 |
| 0x2D6D | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2D6E | 0x000A | 0x001A | 0x0020 | 0x0021 |
| 0x2D6F | 0x000A | 0x001A | 0x0043 | 0x0040 |
| 0x2D70 | 0x0014 | 0x0013 | 0x000A | 0x0012 |
| 0x2D71 | 0x0014 | 0x0013 | 0x000A | 0x0012 |
| 0x2D72 | 0x0014 | 0x0013 | 0x000A | 0x0012 |
| 0x2D74 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2D75 | 0x000A | 0x0015 | 0x001F | 0x0023 |
| 0x2D76 | 0x001B | 0x001C | 0x0023 | 0x001F |
| 0x2D77 | 0x000A | 0x001A | 0x0021 | 0x000B |
| 0x2DBF | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DC1 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DCF | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DD7 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DD9 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DDA | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DDB | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DDC | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DDD | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2DDE | 0x000A | 0x0014 | 0x0012 | 0x008C |
| 0x2DE6 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x2E24 | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E25 | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E26 | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E27 | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E28 | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E29 | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E2A | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E2B | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E2C | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E2D | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E2E | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E2F | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E3C | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E3D | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E3E | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E3F | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E40 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E41 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E42 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E43 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E44 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E45 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E46 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E47 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E48 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E49 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E4A | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E4B | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E4C | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E4D | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E4E | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E4F | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E50 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E51 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E52 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E53 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E60 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2E68 | 0x000A | 0x001A | 0x008D | 0x0094 |
| 0x2E69 | 0x000A | 0x001A | 0x0092 | 0x008F |
| 0x2E6A | 0x000A | 0x001A | 0x008E | 0x0091 |
| 0x2E6E | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E6F | 0x000A | 0x0012 | 0x0003 | 0x0014 |
| 0x2E72 | 0x000A | 0x001A | 0x0080 | 0x0081 |
| 0x2E73 | 0x000A | 0x001A | 0x0080 | 0x0081 |
| 0x2E7A | 0x000A | 0x001A | 0x00FF | 0x00FF |
| 0x2E7B | 0x000A | 0x001A | 0x00FF | 0x00FF |
| 0x2E97 | 0x0014 | 0x00BA | 0x000A | 0x00BB |
| 0x2E98 | 0x000A | 0x0014 | 0x0013 | 0x00BB |
| 0x2E99 | 0x0014 | 0x00BA | 0x000A | 0x00BB |
| 0x2E9A | 0x000A | 0x0014 | 0x0013 | 0x00BB |
| 0x2E9F | 0x000A | 0x0014 | 0x0012 | 0x003C |
| 0x2EE0 | 0x0025 | 0x0013 | 0x000A | 0x0072 |
| 0x2EE1 | 0x0025 | 0x0013 | 0x000A | 0x0072 |
| 0x2EE4 | 0x00A5 | 0x0013 | 0x003E | 0x0024 |
| 0x2EEA | 0x000A | 0x0012 | 0x0024 | 0x0074 |
| 0x2EF4 | 0x000A | 0x0012 | 0x0024 | 0x0074 |
| 0x2EF5 | 0x000A | 0x0012 | 0x0013 | 0x0014 |
| 0x2EFC | 0x000A | 0x0012 | 0x0014 | 0x006B |
| 0x2EFE | 0x000A | 0x0012 | 0x0014 | 0x006B |
| 0x2F08 | 0x000A | 0x0012 | 0x0024 | 0x0073 |
| 0x2F09 | 0x000A | 0x0012 | 0x0024 | 0x0073 |
| 0x2F0B | 0x000A | 0x0012 | 0x0024 | 0x0073 |
| 0x2F17 | 0x000A | 0x0012 | 0x0013 | 0x0014 |
| 0x2F44 | 0x000A | 0x0012 | 0x0014 | 0x008C |
| 0x2F45 | 0x000A | 0x0012 | 0x0014 | 0x00BE |
| 0x2F46 | 0x000A | 0x0012 | 0x0014 | 0x008C |
| 0x2F4E | 0x000A | 0x001A | 0x00CB | 0x0014 |
| 0x2F4F | 0x000A | 0x001A | 0x00CB | 0x0014 |
| 0x2F50 | 0x000A | 0x001A | 0x0014 | 0x00CB |
| 0x2F59 | 0x000A | 0x0014 | 0x0012 | 0x008C |
| 0x2F5A | 0x000A | 0x001A | 0x0014 | 0x000B |
| 0x2F62 | 0x000A | 0x0012 | 0x000B | 0x0014 |
| 0x2F6C | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2F71 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x2F77 | 0x000A | 0x000B | 0x0024 | 0x0075 |
| 0x2F78 | 0x000A | 0x000B | 0x0024 | 0x0075 |
| 0x2F7B | 0x000A | 0x0012 | 0x001A | 0x008C |
| 0x2F7E | 0x000A | 0x0024 | 0x0012 | 0x00A5 |
| 0x2F7F | 0x000A | 0x0024 | 0x0012 | 0x00A5 |
| 0x2F80 | 0x0014 | 0x0024 | 0x00A5 | 0x008C |
| 0x2F87 | 0x000A | 0x0024 | 0x0012 | 0x00A5 |
| 0x2F88 | 0x000A | 0x0024 | 0x0012 | 0x00A5 |
| 0x2F8A | 0x000A | 0x0014 | 0x0024 | 0x0012 |
| 0x2FA3 | 0x0014 | 0x000A | 0x008C | 0x00BE |
| 0x30AC | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x30AD | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x30AE | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x30AF | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x30B0 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x30B1 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x30B2 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x30B3 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x30B4 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x30B5 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x30B6 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x30B7 | 0x000A | 0x0012 | 0x0014 | 0x000B |
| 0x30D4 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0x30E8 | 0x000A | 0x001A | 0x0011 | 0x0023 |
| 0xCD87 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCD8B | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDB7 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDC7 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDCB | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDDD | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xCDE0 | 0x000A | 0x001A | 0x0014 | 0x008C |
| 0xFFFF | 0x00FF | 0x00FF | 0x00FF | 0x00FF |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 119 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | Regelstatus Bank 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0003 | Relative Luftmasse | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x0004 | Motortemperatur | Grad C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x0005 | Regelfaktor Bank 1 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x0006 | Adaptionsfaktor Bank 1 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x000A | Motordrehzahl | 1/min | - | unsigned char | - | 40,0 | 1 | 0,0 |
| 0x000B | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0011 | Luftmassenfluß | kg/h | - | unsigned char | - | 4,0 | 1 | 0,0 |
| 0x0012 | Motortemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x0013 | Ansauglufttemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x0014 | Batteriespannung | V | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 |
| 0x0015 | Drosselklappenwinkel bez. auf unteren Anschlag | %DK | - | unsigned char | - | 0,39215686917305 | 1 | 0,0 |
| 0x0016 | Sondenspannung vor Katalysator Bank 1 | V | - | unsigned char | - | 0,00521568628028035 | 1 | -0,2 |
| 0x0017 | Sondenspannung hinter Katalysator Bank 1 | V | - | unsigned char | - | 0,00521568628028035 | 1 | -0,2 |
| 0x001A | relative Luftfüllung | % | - | unsigned char | - | 0,75 | 1 | 0,0 |
| 0x001B | Spannung Pedalwertgeber Poti 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x001C | Spannung Pedalwertgeber Poti 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x001D | Verdoppelte Spannung Pedalwertgeber Poti 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x001E | Pfadidentifier SKA-Überwachung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x001F | Pfadidentifier EGAS-Überwachung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0020 | Pfadidentifier Momenten-Überwachung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0021 | Istmoment beim Momentenvergleich | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x0022 | Pfadidentifier Reset-Überwachung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0023 | normierter Fahrpedalwinkel | %PED | - | unsigned char | - | 0,39215686917305 | 1 | 0,0 |
| 0x0024 | Umgebungstemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x0025 |  Motortemperatur Ersatzwert aus Modell | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x0026 | Spannung Drosselklappenpotenziometer 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0027 | Spannung Drosselklappenpotenziometer 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0028 | Sollwert DK-Winkel bez. auf unteren Anschlag | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x0029 | Abgastemperatur vor Katalysator aus Modell | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x002B | Katalysatortemperatur aus Modell | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x002F | Spannung an der Heizerendstufe hinter Kat | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0033 | Innenwiderstand Lambdasonde hinter Kat. | Ohm | - | unsigned char | - | 64,0 | 1 | 0,0 |
| 0x0035 | Umgebungsdruck | hPa | - | unsigned char | - | 5,0 | 1 | 0,0 |
| 0x003C | Tankfüllstand 1L / Ink. | l | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x003E | Motortemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x003F | Motortemperatur-Referenzwert aus Modell | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x0040 | Berechnetes Ist-Moment in der Funktionsüberwachung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x0041 | Ist Gang | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0042 | Zulässiges indiziertes Moment vor Filter | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x0043 | Indiziertes Sollmoment für ZW-Eingriff vor Momentenbegrenzung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x0044 | Innenwiderstand LSU | Ohm | - | unsigned char | - | 10,0 | 1 | 0,0 |
| 0x0064 | DK-Winkel der Notluftposition | % | - | unsigned char | - | 0,390630960464478 | 1 | 0,0 |
| 0x0065 | Spannung Drosselklappen-Poti 1 am unteren Anschlag | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0066 | Integratorgradient für Offsetkorrektur Klopfregelung | V/s | - | signed char | - | 23,841869354248 | 1 | 0,0 |
| 0x0069 | Spannung Lambdasonde hinter Katalysator | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x006B | Tastverhältnis Elektrolüfter | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x0071 | ADC- Spannung Luftmasse | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0072 | ADC- Spannung Motortemperatur | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0073 | ADC- Spannung Ansauglufttemperatur | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0074 | ADC- Spannung Temperaturkuehleraustritt | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0075 | ADC- Spannung Umgebungsdrucksensor | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0076 | Dauer-RAM: Sollwert DK-Winkel in Notluftposition, bez. auf UMA | % | - | unsigned char | - | 0,390630960464478 | 1 | 0,0 |
| 0x0077 | Integratorwert Klopfregelung Meßfensterende Testimpuls | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0078 | gefilterte Katalysatortemperatur aus Modell | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x007E | normierte Heizleistung der Lambdasonde hinter Kat | - | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| 0x0080 | Integratorgradient für Nulltest-Diagnose Klopfregelung | V/s | - | signed char | - | 23,841869354248 | 1 | 0,0 |
| 0x0081 | Integratorwert Klopfregelung Meßfensteranfang | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x0082 | Lambda-Sollwert bez. auf Einbauort Lambdasonde | - | - | unsigned char | - | 0,0625 | 1 | 0,0 |
| 0x0084 | Motorstarttemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x0085 | schneller Mittelwert des Lambdaregelfaktors | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x0087 | Mittelwert der Amplitude Sondensignal hinter Kat. korrigiert mit KB | - | - | unsigned char | - | 0,00390625 | 1 | 0,0 |
| 0x008B | Faktor Luftdichte f(Ansauglufttemp., Höhe) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x008C | Zeitzähler ab Startende | s | - | unsigned char | - | 25,6000003814697 | 1 | 0,0 |
| 0x008D | normierter Referenzpegel KR SW- Zylinder 0 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x008E | normierter Referenzpegel KR SW- Zylinder 1 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x008F | normierter Referenzpegel KR SW- Zylinder 2 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x0090 | normierter Referenzpegel KR SW- Zylinder 3 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x0091 | normierter Referenzpegel KR SW- Zylinder 4 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x0092 | normierter Referenzpegel KR SW- Zylinder 5 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x0093 | normierter Referenzpegel KR SW- Zylinder 6 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x0094 | normierter Referenzpegel KR SW- Zylinder 7 | V | - | unsigned char | - | 0,078125 | 1 | 0,0 |
| 0x0095 | Statusflag ti- Abschaltung bei kat. schädigenden Aussetzerraten | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0096 | Tankfüllstand | l | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x0097 | DMTL Pumpenstrom Referenzleck | mA | - | unsigned char | - | 0,1953125 | 1 | 0,0 |
| 0x0098 | aktuelle Zeit DMTL Leckmessung | s | - | unsigned char | - | 1,60000002384186 | 1 | 0,0 |
| 0x009A | Differenz Pumpstrom zwischen Referenz und min. bei Grobleckmessung | mA | - | unsigned char | - | 0,1953125 | 1 | 0,0 |
| 0x009D | I-Anteil der stetigen LRHK (Byte) | - | - | signed char | - | 4,8828125E-4 | 1 | 0,0 |
| 0x009F | Korrekturwert der LSU-Spannung vor Kat (Byte) | V | - | signed char | - | 0,001953125 | 1 | 0,0 |
| 0x00A1 | Statusbyte: Teilprüfungserkennung für Plausibilitätsfehler | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00A3 | Abgasmassenfluß gefiltert, Bank 1 | kg/h | - | unsigned char | - | 4,0 | 1 | 0,0 |
| 0x00A5 | Abstellzeit (Byte) | s | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x00A6 | LSU-Spannung vor Kat, korrigiert (Byte) | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x00A8 | Sondenspannung vor Kat einer Breitbandlambdasonde (ADC-Wert) (Byte) | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x00AA | Dynamikwert der LSU (Byte) | - | - | unsigned char | - | 0,015625 | 1 | 0,0 |
| 0x00AC | multiplikativer Gemischadaptionsfaktor unterer mult. Bereich (Byte) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x00AE | Regelabweichung Lambda (Byte) | - | - | signed char | - | 0,0078125 | 1 | 0,0 |
| 0x00B0 | Lambdaamplitude nach Filterung (Byte) | - | - | signed char | - | 0,0625 | 1 | 0,0 |
| 0x00B2 | Lambda-Istwert (Byte) | - | - | unsigned char | - | 0,0625 | 1 | 0,0 |
| 0x00B4 | Absolutdruck Abgassystem (Byte) | hPa | - | unsigned char | - | 10,0 | 1 | 0,0 |
| 0x00B6 | gefilterte Abgastemperatur aus Modell | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x00B8 | gefilterte Sondenspannung vor Kat einer Breitbandlambdasonde (Byte) | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x00BA | Generatorspannung | V | - | unsigned char | - | 0,100000001490116 | 1 | 10,6 |
| 0x00BB | vom Generator empfangenes Lastsignal | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x00BC | Generatortemperatur | Grad C | - | unsigned char | - | 192,0 | 1 | -48,0 |
| 0x00BD | Beladung des Aktivkohlefilters | - | - | signed char | - | 0,5 | 1 | 0,0 |
| 0x00BE | Betriebszeit | min | - | unsigned char | - | 1536,0 | 1 | 0,0 |
| 0x00BF | Abgastemperatur im Katalysator aus Modell | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x00C1 | Istwert Lambdasonde, korrigiert um Zusatzamplitude | - | - | unsigned char | - | 0,0625 | 1 | 0,0 |
| 0x00C3 | VVT-Sollwert in Prozent bzgl Verstellbereich Bank1 | % | - | unsigned char | - | 0,390625089406967 | 1 | 0,0 |
| 0x00C5 | VVT-Istwert in Prozent bzgl. Verstellbereich Bank1 | % | - | unsigned char | - | 0,390625089406967 | 1 | 0,0 |
| 0x00C7 | Betriebsartenbyte | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00C8 | Delta Counter NVRAM-Backup | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00C9 | Status SMG-Diagnose | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00CA | Korrekturfaktor Höhe (byte) | - | - | unsigned char | - | 0,015625 | 1 | 0,0 |
| 0x00CB | Fahrzeuggeschwindigkeit, CAN-Signal | km/h | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00D4 | intelligenter Batteriesensor Fehler 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00D5 | intelligenter Batteriesensor Fehler 2 | - | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x00D6 | Referenzmoment für Aussetzererkennung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x00D9 | relative Kraftstoffmasse | % | - | unsigned char | - | 3,0 | 1 | 0,0 |
| 0x00DA | O2- Überschuss bzw. O2-Mangel der LSU im Abgas | % O2 | - | signed char | - | 0,25 | 1 | 0,0 |
| 0x00DB | Korrekturwert für den Innenwiderstand der Nernstzelle der LSU (Byte) | Ohm | - | signed char | - | 10,0 | 1 | 0,0 |
| 0x00DC | Korrekturfaktor für Funktionspumstrom LSU aus Schubabgleich | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x00DD | Abstand zur Startfähigkeitsgrenze | % | - | unsigned char | - | 1,02400004863739 | 1 | -100,0 |
| 0x00DF | aktuelle Batteriespannung | V | - | unsigned char | - | 0,0640000030398369 | 1 | 6,0 |
| 0x00E0 | aktuelles Oelniveau korrigiert | - | - | unsigned char | - | 0,5 | 1 | 0,0 |
| 0x00E1 | relativer Fuellstand des Motoroels | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x00F9 | vom Generator empfangene Generatorsollspannung | V | - | unsigned char | - | 0,100000001490116 | 1 | 10,6 |
| 0x00FF | Umweltbedingung unbekannt | - | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 253 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x29CC | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29CD | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29CE | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29CF | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D0 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D1 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D2 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D3 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D4 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D5 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D6 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D7 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29D8 | 0x1113 | 0x0000 | 0x1114 | 0x1115 |
| 0x29DD | 0x0000 | 0x1116 | 0x0000 | 0x1117 |
| 0x29E2 | 0x1644 | 0x1645 | 0x11F8 | 0x1014 |
| 0x29E3 | 0x1118 | 0x1119 | 0x111B | 0x111A |
| 0x29E4 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x29E5 | 0x0000 | 0x0000 | 0x1009 | 0x1008 |
| 0x29E7 | 0x0000 | 0x0000 | 0x111C | 0x111D |
| 0x29ED | 0x0000 | 0x0000 | 0x1009 | 0x1008 |
| 0x29EF | 0x111E | 0x111F | 0x1009 | 0x1008 |
| 0x29F0 | 0x111E | 0x111F | 0x1009 | 0x1008 |
| 0x29F4 | 0x0000 | 0x0000 | 0x100A | 0x0000 |
| 0x2A12 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A13 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A14 | 0x0000 | 0x0000 | 0x0000 | 0x15F4 |
| 0x2A15 | 0x0000 | 0x0000 | 0x0000 | 0x1121 |
| 0x2A16 | 0x0000 | 0x0000 | 0x15F4 | 0x0000 |
| 0x2A17 | 0x101D | 0x15F5 | 0x101F | 0x101C |
| 0x2A18 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A19 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A1A | 0x0000 | 0x0000 | 0x1123 | 0x0000 |
| 0x2A1D | 0x1124 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A1E | 0x0000 | 0x13C5 | 0x1015 | 0x1060 |
| 0x2A21 | 0x0000 | 0x13C5 | 0x1015 | 0x1060 |
| 0x2A22 | 0x1024 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A2A | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A58 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A59 | 0x108E | 0x1025 | 0x1127 | 0x1126 |
| 0x2A5B | 0x1128 | 0x112A | 0x1127 | 0x1129 |
| 0x2A5D | 0x1028 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A5F | 0x0000 | 0x0000 | 0x112B | 0x112C |
| 0x2A61 | 0x0000 | 0x102A | 0x112D | 0x112E |
| 0x2A63 | 0x112F | 0x1029 | 0x0000 | 0x0000 |
| 0x2A65 | 0x1130 | 0x1132 | 0x1133 | 0x1131 |
| 0x2A67 | 0x1134 | 0x102F | 0x1015 | 0x1014 |
| 0x2A69 | 0x102E | 0x0000 | 0x1135 | 0x1136 |
| 0x2A6B | 0x0000 | 0x1137 | 0x1039 | 0x1138 |
| 0x2A6C | 0x0000 | 0x0000 | 0x0000 | 0x1139 |
| 0x2A6D | 0x113A | 0x113D | 0x113C | 0x113B |
| 0x2A6F | 0x0000 | 0x0000 | 0x0000 | 0x113E |
| 0x2A78 | 0x16F9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A79 | 0x16F9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A7A | 0x15D0 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A7C | 0x15D0 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A80 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A83 | 0x113F | 0x0000 | 0x1140 | 0x0000 |
| 0x2A85 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2A88 | 0x113F | 0x0000 | 0x1140 | 0x0000 |
| 0x2A8A | 0x0000 | 0x0000 | 0x1141 | 0x0000 |
| 0x2A8C | 0x0000 | 0x0000 | 0x1142 | 0x0000 |
| 0x2A8E | 0x0000 | 0x0000 | 0x1143 | 0x0000 |
| 0x2A90 | 0x0000 | 0x0000 | 0x1143 | 0x0000 |
| 0x2AE2 | 0x0000 | 0x16FD | 0x0000 | 0x0000 |
| 0x2B2C | 0x0000 | 0x0000 | 0x129B | 0x129A |
| 0x2B5C | 0x0000 | 0x1144 | 0x0000 | 0x0000 |
| 0x2B5D | 0x1145 | 0x1146 | 0x0000 | 0x1147 |
| 0x2B62 | 0x1148 | 0x1149 | 0x1015 | 0x1014 |
| 0x2B63 | 0x1148 | 0x1149 | 0x1015 | 0x1014 |
| 0x2B66 | 0x0000 | 0x114A | 0x0000 | 0x0000 |
| 0x2B7A | 0x0000 | 0x1016 | 0x1015 | 0x1020 |
| 0x2B7F | 0x0000 | 0x0000 | 0x114B | 0x114C |
| 0x2B81 | 0x0000 | 0x0000 | 0x114D | 0x114E |
| 0x2B82 | 0x0000 | 0x0000 | 0x114F | 0x1150 |
| 0x2B84 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2B98 | 0x1151 | 0x0000 | 0x0000 | 0x0000 |
| 0x2B99 | 0x0000 | 0x0000 | 0x1152 | 0x1153 |
| 0x2B9A | 0x1154 | 0x0000 | 0x0000 | 0x0000 |
| 0x2B9B | 0x1155 | 0x0000 | 0x0000 | 0x0000 |
| 0x2B9C | 0x1156 | 0x1157 | 0x1158 | 0x0000 |
| 0x2BA7 | 0x0000 | 0x0000 | 0x0000 | 0x1159 |
| 0x2BAC | 0x115A | 0x0000 | 0x0000 | 0x0000 |
| 0x2BAD | 0x115B | 0x115C | 0x0000 | 0x0000 |
| 0x2BC0 | 0x10EE | 0x1090 | 0x0000 | 0x0000 |
| 0x2BC1 | 0x0000 | 0x13C5 | 0x13C7 | 0x13C6 |
| 0x2C24 | 0x1160 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C31 | 0x0000 | 0x0000 | 0x1161 | 0x1162 |
| 0x2C37 | 0x0000 | 0x1163 | 0x0000 | 0x0000 |
| 0x2C39 | 0x0000 | 0x0000 | 0x1076 | 0x0000 |
| 0x2C3B | 0x1164 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C47 | 0x0000 | 0x0000 | 0x1015 | 0x1014 |
| 0x2C49 | 0x1165 | 0x1166 | 0x1309 | 0x130A |
| 0x2C4B | 0x1072 | 0x1169 | 0x1167 | 0x1168 |
| 0x2C4D | 0x116A | 0x116B | 0x0000 | 0x116C |
| 0x2C4F | 0x0000 | 0x1016 | 0x0000 | 0x0000 |
| 0x2C51 | 0x0000 | 0x1016 | 0x0000 | 0x0000 |
| 0x2C53 | 0x0000 | 0x1016 | 0x0000 | 0x0000 |
| 0x2C61 | 0x0000 | 0x0000 | 0x0000 | 0x116D |
| 0x2C6D | 0x116E | 0x1171 | 0x1170 | 0x116F |
| 0x2C71 | 0x1172 | 0x1016 | 0x1173 | 0x1014 |
| 0x2C84 | 0x0000 | 0x15F3 | 0x0000 | 0x1490 |
| 0x2C9C | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2C9E | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2CA0 | 0x1174 | 0x1177 | 0x1175 | 0x1176 |
| 0x2CA8 | 0x1178 | 0x0000 | 0x0000 | 0x0000 |
| 0x2CEF | 0x1179 | 0x117B | 0x117C | 0x117A |
| 0x2CF0 | 0x0000 | 0x0000 | 0x117D | 0x117E |
| 0x2CF1 | 0x117F | 0x0000 | 0x0000 | 0x0000 |
| 0x2CF8 | 0x1180 | 0x0000 | 0x0000 | 0x0000 |
| 0x2CF9 | 0x1181 | 0x0000 | 0x1015 | 0x1014 |
| 0x2CFA | 0x1181 | 0x0000 | 0x1015 | 0x1014 |
| 0x2CFF | 0x1182 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D00 | 0x0000 | 0x0000 | 0x1183 | 0x1184 |
| 0x2D01 | 0x0000 | 0x0000 | 0x1185 | 0x1186 |
| 0x2D02 | 0x1187 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D03 | 0x0000 | 0x0000 | 0x1188 | 0x1189 |
| 0x2D04 | 0x118A | 0x0000 | 0x0000 | 0x0000 |
| 0x2D05 | 0x118B | 0x0000 | 0x0000 | 0x0000 |
| 0x2D0F | 0x0000 | 0x0000 | 0x1015 | 0x1014 |
| 0x2D13 | 0x0000 | 0x0000 | 0x118C | 0x118D |
| 0x2D1A | 0x118E | 0x0000 | 0x0000 | 0x0000 |
| 0x2D1B | 0x1632 | 0x0000 | 0x11F8 | 0x1014 |
| 0x2D1C | 0x0000 | 0x0000 | 0x11F8 | 0x1014 |
| 0x2D28 | 0x0000 | 0x0000 | 0x1192 | 0x1193 |
| 0x2D29 | 0x1194 | 0x0000 | 0x1196 | 0x1195 |
| 0x2D36 | 0x0000 | 0x0000 | 0x1355 | 0x1136 |
| 0x2D37 | 0x0000 | 0x0000 | 0x1355 | 0x1136 |
| 0x2D6D | 0x115A | 0x0000 | 0x0000 | 0x0000 |
| 0x2D6E | 0x1197 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D6F | 0x1198 | 0x1199 | 0x119A | 0x0000 |
| 0x2D70 | 0x119B | 0x119E | 0x119C | 0x119D |
| 0x2D71 | 0x119F | 0x11A1 | 0x11A2 | 0x11A0 |
| 0x2D72 | 0x0000 | 0x0000 | 0x0000 | 0x11A3 |
| 0x2D74 | 0x11A4 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D75 | 0x11A5 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D76 | 0x11A6 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D77 | 0x0000 | 0x0000 | 0x0000 | 0x11A7 |
| 0x2DBF | 0x11A8 | 0x10B9 | 0x11AA | 0x11A9 |
| 0x2DC1 | 0x0000 | 0x10B9 | 0x0000 | 0x0000 |
| 0x2DCF | 0x11AB | 0x10B9 | 0x11AA | 0x0000 |
| 0x2DD7 | 0x1418 | 0x10B9 | 0x1417 | 0x0000 |
| 0x2DD9 | 0x11AC | 0x10B9 | 0x11AA | 0x0000 |
| 0x2DDA | 0x11AD | 0x10B9 | 0x0000 | 0x0000 |
| 0x2DDB | 0x0000 | 0x10B9 | 0x0000 | 0x0000 |
| 0x2DDC | 0x11A8 | 0x10B9 | 0x11AA | 0x0000 |
| 0x2DDD | 0x11AE | 0x10B9 | 0x0000 | 0x0000 |
| 0x2DDE | 0x10B9 | 0x11AF | 0x0000 | 0x11AA |
| 0x2DE6 | 0x11B0 | 0x1102 | 0x0000 | 0x0000 |
| 0x2E24 | 0x11B1 | 0x11B2 | 0x11B4 | 0x11B3 |
| 0x2E25 | 0x11B1 | 0x11B2 | 0x11B4 | 0x11B3 |
| 0x2E26 | 0x11B1 | 0x11B2 | 0x11B4 | 0x11B3 |
| 0x2E27 | 0x11B1 | 0x11B2 | 0x11B4 | 0x11B3 |
| 0x2E28 | 0x11B1 | 0x11B2 | 0x11B4 | 0x11B3 |
| 0x2E29 | 0x11B1 | 0x11B2 | 0x11B4 | 0x11B3 |
| 0x2E2A | 0x11B1 | 0x11B2 | 0x11B4 | 0x11B3 |
| 0x2E2B | 0x11B1 | 0x11B2 | 0x11B4 | 0x11B3 |
| 0x2E2C | 0x11B1 | 0x11B2 | 0x11B4 | 0x11B3 |
| 0x2E2D | 0x11B1 | 0x11B2 | 0x11B4 | 0x11B3 |
| 0x2E2E | 0x11B1 | 0x11B2 | 0x11B4 | 0x11B3 |
| 0x2E2F | 0x11B1 | 0x11B2 | 0x11B4 | 0x11B3 |
| 0x2E3C | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E3D | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E3E | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E3F | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E40 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E41 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E42 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E43 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E44 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E45 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E46 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E47 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2E48 | 0x10B9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E49 | 0x10B9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E4A | 0x10B9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E4B | 0x10B9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E4C | 0x10B9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E4D | 0x10B9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E4E | 0x10B9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E4F | 0x10B9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E50 | 0x10B9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E51 | 0x10B9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E52 | 0x10B9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E53 | 0x10B9 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E60 | 0x1071 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E68 | 0x11B5 | 0x0000 | 0x11B7 | 0x11B6 |
| 0x2E69 | 0x11B5 | 0x0000 | 0x11B7 | 0x11B6 |
| 0x2E6A | 0x11B5 | 0x0000 | 0x11B7 | 0x11B6 |
| 0x2E6E | 0x12ED | 0x0000 | 0x0000 | 0x0000 |
| 0x2E6F | 0x12ED | 0x0000 | 0x0000 | 0x0000 |
| 0x2E72 | 0x1025 | 0x0000 | 0x11B9 | 0x11B8 |
| 0x2E73 | 0x11BA | 0x0000 | 0x0000 | 0x0000 |
| 0x2E7A | 0x0000 | 0x0000 | 0x0000 | 0x15D4 |
| 0x2E7B | 0x0000 | 0x0000 | 0x0000 | 0x15D4 |
| 0x2E97 | 0x11BB | 0x11BC | 0x0000 | 0x1055 |
| 0x2E98 | 0x10E7 | 0x11BD | 0x0000 | 0x0000 |
| 0x2E99 | 0x11BB | 0x11BC | 0x0000 | 0x1055 |
| 0x2E9A | 0x10E7 | 0x11BD | 0x0000 | 0x0000 |
| 0x2E9F | 0x11BE | 0x11BF | 0x11C1 | 0x11C0 |
| 0x2EE0 | 0x0000 | 0x0000 | 0x11F8 | 0x1014 |
| 0x2EE1 | 0x13BD | 0x11C4 | 0x13BE | 0x13BC |
| 0x2EE4 | 0x0000 | 0x0000 | 0x0000 | 0x1646 |
| 0x2EEA | 0x1194 | 0x0000 | 0x1060 | 0x1015 |
| 0x2EF4 | 0x11C7 | 0x0000 | 0x0000 | 0x0000 |
| 0x2EF5 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2EFC | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2EFE | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2F08 | 0x0000 | 0x0000 | 0x11F8 | 0x1014 |
| 0x2F09 | 0x1636 | 0x0000 | 0x118C | 0x1646 |
| 0x2F0B | 0x0000 | 0x0000 | 0x12E1 | 0x1646 |
| 0x2F17 | 0x0000 | 0x0000 | 0x0000 | 0x11C8 |
| 0x2F44 | 0x11C9 | 0x11CC | 0x11CA | 0x11CB |
| 0x2F45 | 0x11CD | 0x11CE | 0x11CF | 0x0000 |
| 0x2F46 | 0x0000 | 0x11D0 | 0x11D1 | 0x11D2 |
| 0x2F4E | 0x11D3 | 0x115F | 0x118C | 0x118D |
| 0x2F4F | 0x11D4 | 0x0000 | 0x11D5 | 0x11D6 |
| 0x2F50 | 0x11D7 | 0x0000 | 0x0000 | 0x11D8 |
| 0x2F59 | 0x0000 | 0x11D9 | 0x0000 | 0x0000 |
| 0x2F5A | 0x0000 | 0x11DA | 0x0000 | 0x0000 |
| 0x2F62 | 0x11DB | 0x0000 | 0x0000 | 0x0000 |
| 0x2F6C | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2F71 | 0x0000 | 0x1016 | 0x1015 | 0x1014 |
| 0x2F77 | 0x11DC | 0x11DF | 0x11DE | 0x11DD |
| 0x2F78 | 0x0000 | 0x0000 | 0x1015 | 0x1014 |
| 0x2F7B | 0x108D | 0x0000 | 0x0000 | 0x0000 |
| 0x2F7E | 0x15CB | 0x0000 | 0x0000 | 0x0000 |
| 0x2F7F | 0x15CC | 0x0000 | 0x0000 | 0x0000 |
| 0x2F80 | 0x1194 | 0x10B9 | 0x0000 | 0x0000 |
| 0x2F87 | 0x0000 | 0x0000 | 0x15D8 | 0x15D7 |
| 0x2F88 | 0x0000 | 0x0000 | 0x15D6 | 0x15D5 |
| 0x2F8A | 0x11E0 | 0x11E1 | 0x1191 | 0x1190 |
| 0x2FA3 | 0x11E2 | 0x0000 | 0x0000 | 0x0000 |
| 0x30AC | 0x0000 | 0x11E3 | 0x11E5 | 0x11E4 |
| 0x30AD | 0x0000 | 0x11E3 | 0x11E5 | 0x11E4 |
| 0x30AE | 0x0000 | 0x11E3 | 0x11E5 | 0x11E4 |
| 0x30AF | 0x0000 | 0x11E3 | 0x11E5 | 0x11E4 |
| 0x30B0 | 0x0000 | 0x11E3 | 0x11E5 | 0x11E4 |
| 0x30B1 | 0x0000 | 0x11E3 | 0x11E5 | 0x11E4 |
| 0x30B2 | 0x0000 | 0x11E3 | 0x11E5 | 0x11E4 |
| 0x30B3 | 0x0000 | 0x11E3 | 0x11E5 | 0x11E4 |
| 0x30B4 | 0x0000 | 0x11E3 | 0x11E5 | 0x11E4 |
| 0x30B5 | 0x0000 | 0x11E3 | 0x11E5 | 0x11E4 |
| 0x30B6 | 0x0000 | 0x11E3 | 0x11E5 | 0x11E4 |
| 0x30B7 | 0x0000 | 0x11E3 | 0x11E5 | 0x11E4 |
| 0x30D4 | 0x0000 | 0x10B9 | 0x0000 | 0x0000 |
| 0x30E8 | 0x115A | 0x0000 | 0x11E6 | 0x11E7 |
| 0xCD87 | 0x0000 | 0x11E8 | 0x11EA | 0x11E9 |
| 0xCD8B | 0x0000 | 0x11E8 | 0x11EA | 0x11E9 |
| 0xCDB7 | 0x0000 | 0x10B9 | 0x0000 | 0x0000 |
| 0xCDC7 | 0x0000 | 0x11E8 | 0x11EA | 0x11E9 |
| 0xCDCB | 0x0000 | 0x11E8 | 0x11EA | 0x11E9 |
| 0xCDDD | 0x11A8 | 0x10B9 | 0x11AA | 0x0000 |
| 0xCDE0 | 0x115A | 0x10B9 | 0x11AA | 0x0000 |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 285 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x1008 | Gemisch zu mager |
| 0x1009 | Gemisch zu fett |
| 0x100A | Wirkungsgrad unter Schwellwert |
| 0x1014 | Kurzschluss nach Plus |
| 0x1015 | Kurzschluss nach Minus |
| 0x1016 | Leitungsunterbrechung |
| 0x101C | obere Schwelle Pumpenstrom bei Referenzmessung |
| 0x101D | Pumpenstromschwelle bei Ventilprüfung erreicht |
| 0x101E | Abbruch wegen Stromschwankungen bei Feinleckprüfung |
| 0x101F | untere Schwelle Pumpenstrom bei Referenzmessung |
| 0x1020 | kurzschluss nach Plus |
| 0x1023 | nicht korrekt geschlossen |
| 0x1024 | Füllstandssignalwert zum Verbrauchswert unplausibel |
| 0x1025 | Parity-Fehler |
| 0x1028 | Sensorsignale zueinander unplausibel |
| 0x1029 | Lagereglerüberwachung |
| 0x102A | keine Anschläge gelernt |
| 0x102E | Relais-Fehler |
| 0x102F | Kurzschluss der Motorleitungen |
| 0x1039 | Exzenterwinkel fährt nicht auf Vollhubposition |
| 0x1055 | Übertemperatur |
| 0x1060 | Kurzschluss nach Plus oder Leitungsunterbrechung |
| 0x1071 | Kommunikationsfehler |
| 0x1072 | Initialisierungsfehler |
| 0x1076 | Sondensignal zu träge |
| 0x108D | elektrischer Fehler |
| 0x108E | Gradientenfehler |
| 0x1090 | Signal oberhalb Schwelle |
| 0x10B9 | Timeout |
| 0x10E7 | Generatortyp nicht plausibel |
| 0x10EE | Signal unterhalb Schwelle |
| 0x1102 | CAN Timeout |
| 0x1113 | Verbrennungsaussetzer im Warmlauf, emissionsverschlechternd |
| 0x1114 | Verbrennungsaussetzer betriebswarm, emissionsverschlechternd |
| 0x1115 | Verbrennungsaussetzer mit Zylinderabschaltung |
| 0x1116 | kein Raddrehzahlsignal erhalten |
| 0x1117 | Radgeschwindigkeit zu hoch |
| 0x1118 | Fehlfunktion |
| 0x1119 | Druckschwingungen |
| 0x111A | Raildruck zu hoch |
| 0x111B | Raildruck zu niedrig |
| 0x111C | System zu fett additiv pro Zeit zu groß |
| 0x111D | System zu mager additiv pro Zeit zu groß |
| 0x111E | System zu fett additiv pro Zeit zu gross |
| 0x111F | System zu mager additiv pro Zeit zu gross |
| 0x1120 | Feinleck erkannt |
| 0x1121 | Leckage größer 1,0mm |
| 0x1122 | sehr kleines Leck detektiert |
| 0x1123 | Tankentlüftungssystem |
| 0x1124 | Tankfüllstandssignal unplausibel |
| 0x1125 | CAN, Ungültigkeitswert empfangen |
| 0x1126 | Magnetloss-Fehler |
| 0x1127 | Reset-Fehler |
| 0x1128 | Gradientenüberschreitung |
| 0x1129 | Magnetloss |
| 0x112A | Parity-Fehler oder kein Signal |
| 0x112B | Sensorversorgungsspannung zu klein |
| 0x112C | Sensorversorgungsspannung zu hoch |
| 0x112D | Fehler unteres Lernfenster |
| 0x112E | Verstellbereich fehlerhaft |
| 0x112F | Drehrichtungserkennung |
| 0x1130 | ROM-Test-Fehler |
| 0x1131 | EEPROM-Test-Fehler |
| 0x1132 | Watchdog oder Temperatursensorfehler |
| 0x1133 | RAM-Test-Fehler |
| 0x1134 | Ansteuerungsfehler allgemein |
| 0x1135 | Spannung zu klein |
| 0x1136 | Spannung zu hoch |
| 0x1137 | Plausibilitätsfehler Luftmasse |
| 0x1138 | Drehzahlfüllungsbegrenzung |
| 0x1139 | Anschläge lernen notwendig |
| 0x113A | Überlastschutz Valvetronic-System |
| 0x113B | Strom E-Motor zu hoch |
| 0x113C | Temperatur E-Motor zu hoch |
| 0x113D | Steuergerätetemperatur zu hoch |
| 0x113E | maximale Anzahl der Minhubanschläge überschritten |
| 0x113F | Regelanschlag zu lange zu groß |
| 0x1140 | Anschlagadaption außerhalb gültigem Bereich |
| 0x1141 | Anschlagadaptionen außerhalb gültigem Bereich |
| 0x1142 | llenverstellung hat Spätposition nicht erreicht |
| 0x1143 | Korrelationsfehler, ein Zahn Versatz |
| 0x1144 | Leitungsunterbrechung, Drehzahlsignal |
| 0x1145 | Kurbelwellen Zahnfehler oder Lückenverlust |
| 0x1146 | Zahnkorrektur bei einem Zahn zuwenig |
| 0x1147 | Zahnkorrektur bei einem Zahn zuviel |
| 0x1148 | unplausible Phasenflankenanzahl |
| 0x1149 | Lage der Phasenflanken oder Einbaulage außerhalb Toleranzen |
| 0x114A | keine Master-Nockenwelle vorhanden |
| 0x114B | Massenstromadaption zu klein |
| 0x114C | Massenstromadaption zu groß |
| 0x114D | Unterdrehzahlfehler (LL-Steller Öffnung zu gering) |
| 0x114E | Überdrehzahlfehler (LL-Steller oder Leckluft) |
| 0x114F | Unterdrehzahlfehler (Leerlauf-Steller Öffnung zu gering) |
| 0x1150 | Überdrehzahlfehler (Leerlauf-Steller oder Leckluft) |
| 0x1151 | Aktualitätszähler EEPROM und RAMBACKUP unterschiedlich |
| 0x1152 | Schreibfehler, RAM Backup fehlerhaft |
| 0x1153 | Lesefehler, RAM Backup fehlerhaft |
| 0x1154 | Rechnerüberwachung: RAM |
| 0x1155 | Rechnerüberwachung: ROM |
| 0x1156 | Rechnerüberwachung: RESET |
| 0x1157 | Reset aus der TPU-Überwachung |
| 0x1158 | Reset aus dem TPU-RAM-Test |
| 0x1159 | maximal zulässiges Sollmoment wird dauerhaft überschritten |
| 0x115A | Plausibilitätsfehler |
| 0x115B | Master/Slave-DME - Plausibilitätsfehler |
| 0x115C | Master/Slave-DME - Identifizierung fehlerhaft |
| 0x115D | Umgebungstemperatur grösser als Modelltemperatur |
| 0x115E | Umgebungstemperatur kleiner als Modelltemperatur |
| 0x115F | CAN Botschaft fehlerhaft |
| 0x1160 | vertauschte Lambdasonden |
| 0x1161 | Offsetprüfung, System zu mager |
| 0x1162 | Offsetprüfung, System zu fett |
| 0x1163 | Heizereinkopplung auf Signalpfad |
| 0x1164 | Sonde an Luft |
| 0x1165 | Signal zu mager |
| 0x1166 | Signal zu fett |
| 0x1167 | Betriebsspannung am IC zu niedrig |
| 0x1168 | Signalkreisaptionswert zu hoch |
| 0x1169 | SPI Kommunikation gestört |
| 0x116A | Signalspannung im Schub zu klein infolge offener Pumpstromleitung |
| 0x116B | Unterbrechung Pumpstrompfad |
| 0x116C | Lambdaregelwert oberhalb Schwelle infolge offener Pumpstromleitung |
| 0x116D | Nernstzellenwiderstand oder Keramiktemperatur unplausibel, Leitungs- oder Heizerfehler |
| 0x116E | Sonde dynamisch zu langsam |
| 0x116F | Signal überschreitet Schwellwert nicht |
| 0x1170 | Signal unterschreitet Schwellwert nicht |
| 0x1171 | Schubspannungsschwelle nicht erreicht |
| 0x1172 | Heiztakteinkopplung auf Signal |
| 0x1173 | Adernschluss oder CSD (Referenzluft vergiftet) |
| 0x1174 | Innenwiderstand der Nernstzelle unplausibel oder zu späte Betriebsbereitschaft |
| 0x1175 | RI-Regler dauerhaft am unteren Anschlag |
| 0x1176 | RI-Regler dauerhaft am oberen Anschlag |
| 0x1177 | Kalibrierwiderstand in DME fehlerhaft |
| 0x1178 | Sondenheizung defekt (Innenwiderstand) |
| 0x1179 | interner SPI Kommunikationfehler |
| 0x117A | Kurzschluss |
| 0x117B | Lastabfall |
| 0x117C | Überlastung |
| 0x117D | Lageregelung klemmt kurzzeitig |
| 0x117E | Lageregelung klemmt anhaltend |
| 0x117F | Lageabweichung |
| 0x1180 | Poti 1 oder Poti 2 fehlerhaft , oder beide unplausibel zum Ersatzwert |
| 0x1181 | unplausibel zu Ersatzwert aus Füllung |
| 0x1182 | DVE-Fehler bei Verstärkerabgleich |
| 0x1183 | Fehler bei Prüfung der öffnenden Feder |
| 0x1184 | Fehler bei Prüfung der Rückstellfeder |
| 0x1185 | Fehler bei Federprüfung Öffnen |
| 0x1186 | Fehler bei Federprüfung Öffnen, Abbruch Feder öffnet nicht |
| 0x1187 | DVE-Fehler bei Prüfung Notluftposition |
| 0x1188 | Lernverbot, Batteriespannung zu niedrig |
| 0x1189 | Lernfreigabe, aber Umweltbedingungen unplausibel |
| 0x118A | UMA-Lernen während Urinitialisierung abgebrochen |
| 0x118B | wiederholtes UMA-Lernen fehlerhaft |
| 0x118C | untere Schwelle unterschritten |
| 0x118D | obere Schwelle überschritten |
| 0x118E | Geber 1 oder Geber 2 fehlerhaft oder außerhalb der Toleranz |
| 0x118F | Gleichlauffehler zwischen PWG1 und PWG2 |
| 0x1190 | Spannungsschwellwert überschritten |
| 0x1191 | Spannungsschwellwert unterschritten |
| 0x1192 | Signal unterhalb Schwelle, Kurzschluss nach Minus |
| 0x1193 | Signal oberhalb Schwelle, Kurzschluss nach Plus |
| 0x1194 | Unplausibel |
| 0x1195 | Drucksensor hat obere Schwelle überschritten |
| 0x1196 | Drucksensor hat untere Schwelle unterschritten |
| 0x1197 | Funktionsüberwachung Momentenvergleich |
| 0x1198 | Lastsensor-, Zuleitung- oder DME-Fehler |
| 0x1199 | Valvetronic, Ventil Plausibilisierung |
| 0x119A | Drucksensor Plausibilisierung |
| 0x119B | Reaktionsüberwachung |
| 0x119C | Zündwinkelüberwachung |
| 0x119D | RL-Überwachung |
| 0x119E | ADC-Überwachung |
| 0x119F | Drosselklappen-Anschlagüberwachung (UMA) Ebene 2 |
| 0x11A0 | Rkti - Plausibilisierung |
| 0x11A1 | Varianten Codierungsüberwachung |
| 0x11A2 | GKC Kraftstoffkorrektur |
| 0x11A3 | TPU-Überwachung |
| 0x11A4 | Funktionsüberwachung  Lambdaplausibilisierung |
| 0x11A5 | Funktionsüberwachung Drehzahlgeber-, Zuleitung- oder DME-Fehler |
| 0x11A6 | Pedalwertgeber-, Zuleitung- oder DME-Fehler |
| 0x11A7 | Bankabweichung zu gross |
| 0x11A8 | Checksumme fehlerhaft |
| 0x11A9 | Bremsüberwachung, keine ACC Reaktion |
| 0x11AA | Alive-Fehler |
| 0x11AB | MIL-Check |
| 0x11AC | Delta-Ist- oder Delta-Soll-Moment unplausibel |
| 0x11AD | Checksumme fehlerhaft oder Alive-Fehler |
| 0x11AE | Checksumme oder Alive-Fehler |
| 0x11AF | Valvetronic, Sollwert-Botschaft nicht empfangen |
| 0x11B0 | interner Prüfsummenfehler |
| 0x11B1 | Signal nicht plausibel, Zündkreisüberwachung |
| 0x11B2 | Übertemperaturabschaltung oder Signalabfall |
| 0x11B3 | Kurzschluss nach Plus, Nichtimpedanz |
| 0x11B4 | Übergangswiderstand, Hochimpedanz |
| 0x11B5 | mehrere Leitungsfehler detektiert |
| 0x11B6 | Motor mechanisch zu laut oder Sensor außerhalb Toleranz (Empfindlichkeit) |
| 0x11B7 | elektrischer Fehler (Wackelkontakt oder Sensor locker) |
| 0x11B8 | Testimpulsfehler |
| 0x11B9 | Nulltestfehler |
| 0x11BA | SPI Kommunikation unplausibel |
| 0x11BB | Mechanisch |
| 0x11BC | Elektrisch |
| 0x11BD | Keine Kommunikation über BSD-Schnittstelle |
| 0x11BE | Permittivitätsmessung fehlerhaft |
| 0x11BF | Kommunikationsfehler Ölsensor |
| 0x11C0 | Temperaturmessung fehlerhaft |
| 0x11C1 | Niveaumessung fehlerhaft |
| 0x11C2 | unplausibel |
| 0x11C3 | Signalfehler aus High-Side-Check erkannt |
| 0x11C4 | Motortemperaturschwelle für Lambdaregelungsfreigabe nicht erreicht |
| 0x11C5 | Motortemperatursignal im unteren Bereich nicht plausibel |
| 0x11C6 | Kaltstart, Nebenschluss erkannt |
| 0x11C7 | Thermostat fehlerhaft |
| 0x11C8 | Maximalwert Öltemperatur überschritten |
| 0x11C9 | EWS-Telegramme fehlerhaft. Fangbereichsrechnung fehlgeschlagen |
| 0x11CA | Startwert nicht programmiert |
| 0x11CB | Startwert im Flash zerstört oder 2- aus 3-Auswahl fehlgeschlagen oder Startwertprogrammierroutine fehlerhaft |
| 0x11CC | Fehler beim Programmieren oder Rücksetzen des Startwertes |
| 0x11CD | Mehr als 3 Parity-Fehler erkannt |
| 0x11CE | Timeoutfehler: 10 Sekunden nach Kl. 15 EIN noch kein EWS-Telegramm empfangen, evtl. Leitungsunterbre |
| 0x11CF | Empfangsfehler des EWS-Telegramms (Start-, Stopbit- oder Framefehler) |
| 0x11D0 | Schreibfehler, Wechselcodeablage im EEPROM-Spiegel |
| 0x11D1 | Fehler Wechselcode-Ablage (z.B. Powerfail) |
| 0x11D2 | Lesefehler, Wechselcodeablage im EEPROM-Spiegel |
| 0x11D3 | keine Signaländerungen |
| 0x11D4 | Geschwindigkeit unplausibel |
| 0x11D5 | Mindestgeschwindigkeit im Schub nicht erreicht |
| 0x11D6 | Mindestgeschwindigkeit unter Last nicht erreicht |
| 0x11D7 | Geschwindigkeitssignal vom Kombi und ASC nicht kompatibel |
| 0x11D8 | Kombi hat ungültiges Signal gesendet |
| 0x11D9 | Start in laufenden Motor |
| 0x11DA | Signalfehler Startautomatik |
| 0x11DB | Prüfresultat unplausibel |
| 0x11DC | Differenz Umgebungsdruck zwischen Master- und Slave-DME zu gross |
| 0x11DD | Signal oder Wert oberhalb Schwelle |
| 0x11DE | Signal oder Wert unterhalb Schwelle |
| 0x11DF | Stetigkeitsfehler |
| 0x11E0 | ADC-defekt, Hardwarefehler |
| 0x11E1 | Stromversorgung instabil |
| 0x11E2 | DME nicht codiert |
| 0x11E3 | Lastabfall Lowside oder Highside |
| 0x11E4 | Windungsschluss oder Kurzschluss nach Plus Lowside |
| 0x11E5 | Kurzschluss nach Minus Lowside oder Highside oder Kurzschluss nach Plus Highside |
| 0x11E6 | Lambda zu fett |
| 0x11E7 | Überlast Hochdruckpumpe |
| 0x11E8 | CAN Baustein Bus Off oder CAN-Bus defekt |
| 0x11E9 | CAN Baustein im Zustand Passiv |
| 0x11EA | CAN Baustein DPRAM defekt |
| 0x11F8 | Kurzschluss nach Masse |
| 0x129A | Druck zu hoch |
| 0x129B | Druck zu niedrig |
| 0x12E1 | Temperatur zu niedrig |
| 0x12ED | Bankabschaltung |
| 0x1309 | System zu mager |
| 0x130A | System zu fett |
| 0x1355 | Spannung zu niedrig |
| 0x13BC | High-Side Check unplausibel |
| 0x13BD | Stuck-Check unplausibel |
| 0x13BE | Low-Side Check unplausibel |
| 0x13C5 | CAN Botschaft Ungültig |
| 0x13C6 | Wert oberhalb Schwelle |
| 0x13C7 | Wert unterhalb Schwelle |
| 0x1417 | Alivefehler |
| 0x1418 | Checksummenfehler |
| 0x1490 | langsame Reaktion von Fett nach Mager (Transient Time) |
| 0x15CB | Zeit zu kurz in Korrelation zu Motorkühlmittel-Abkühlung |
| 0x15CC | Zeit zu lang in Korrelation zu Motorkühlmittel-Abkühlung |
| 0x15D0 | nicht regelbar |
| 0x15D4 | Zündwinkel zu früh |
| 0x15D5 | zu schnell im Motorlauf |
| 0x15D6 | zu langsam im Motorlauf |
| 0x15D7 | zu schnell im Nachlauf |
| 0x15D8 | zu langsam im Nachlauf |
| 0x15F3 | verzögerte Reaktion von Fett nach Mager (Response Time) |
| 0x15F4 | Leckage größer 0,5mm |
| 0x15F5 | Abbruch wegen Stromschwankungen bei Referenzleckmessung |
| 0x1632 | Gleichlauffehler zwischen Pedalwertgeber 1 und Pedalwertgeber 2 |
| 0x1636 | Signal, festliegend |
| 0x1644 | Arbeitsbereich, Druck zu niedrig |
| 0x1645 | Arbeitsbereich, Druck zu hoch |
| 0x1646 | Temperatur zu hoch |
| 0x16F9 | Position nicht erreicht |
| 0x16FD | Drehzahl unplausibel |
| 0xFFFF | unbekannte Fehlerart |

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

<a id="table-vvtstatusbg2-2"></a>
### VVTSTATUSBG2_2

Dimensions: 8 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Anschlaege werden gerade gelernt |
| 0x01 | Lernanforderung durch VVT-SG zurueckgewiesen |
| 0x02 | Lernen durch DME abgebrochen |
| 0x03 | Lernen durch VVT abgebrochen |
| 0x05 | Keine Anforderung zum Anschlaglernen |
| 0x06 | Lernvorgang beendet |
| 0x07 | Signal ungueltig |
| 0xXY | Fehlerhafter Status |

<a id="table-ewsstart"></a>
### EWSSTART

Dimensions: 5 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | MED9.2.2 bereit, Startwert zu empfangen |
| 0x01 | Kein freier Startwert mit Freigabe vorhanden |
| 0x02 | Noch kein Startwert gespeichert |
| 0x03 | Startwert nicht plausibel (wie im DS2-LH definiert) |
| 0xXY | Fehlerhafter Status |

<a id="table-ewsempfangsstatus"></a>
### EWSEMPFANGSSTATUS

Dimensions: 15 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Startwertprogrammierung bzw. Wechselcoderuecksetzung war erfolgreich |
| 0x01 | Falscher Startwert b. Ruecksetzen (EWS u. DME haben nicht den gl. Startwert) |
| 0x02 | Telegramminhalt war kein Startwert (event. Wechselcode) |
| 0x03 | Schnittstellenfehler DWA: Frame o. Parity oder kein Signal (Timeout) |
| 0x04 | Prozess laeuft |
| 0x05 | Programmierung bzw. Ruecksetzen im Fahrzyklus noch nicht ausgefuehrt |
| 0x06 | Gleiche Zufallszahl wie bei vorherigem Ruecksetzen trotz Weiterschaltung |
| 0x07 | Noch kein Startwert programmiert |
| 0x10 | Startwert nicht korrekt in Flash programmiert |
| 0x11 | Wechselcode nicht korrekt in EEPROM-Spiegel programmiert |
| 0x12 | Zufallszahl nicht korrekt in EEPROM-Spiegel programmiert |
| 0x20 | Fehler bei Startwert-Programmierroutine |
| 0x21 | 2-aus-3-Startwertablage im Flash nicht in Ordnung |
| 0x22 | Ablage im EEPROM-Spiegel nicht in Ordnung |
| 0xXY | Fehlerhafter Status |

<a id="table-regel"></a>
### REGEL

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | --                                                                    |
| 0x01 | Regelung AUS, Einschaltbedingung noch nicht erfuellt |
| 0x02 | Regelung EIN |
| 0x04 | Regelung AUS wegen Fahrbedingung |
| 0x08 | Regelung AUS wegen erkanntem Fehler |
| 0x10 | Regelung EIN mit Einschraenkung |
| 0xXY | ??                          |

<a id="table-slsstatus"></a>
### SLSSTATUS

Dimensions: 29 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Sekundaerluftdiagnose laeuft gerade ab |
| 0x01 | Systemtest kann nicht gestartet werden |
| 0x02 | Funktionsanforderung vorhanden |
| 0x05 | keine Funktionsanforderung an die Sekundaerluftdiagnose |
| 0x06 | Systemtest SLS ist beendet |
| 0x10 | Sekundaerluftmindermasse erkannt |
| 0x11 | Sekundaerluftmindermasse erkannt |
| 0x12 | Sekundaerluftmindermasse erkannt  |
| 0x13 | Sekundaerluftdiagnoseergebnis n.i.o. |
| 0x14 | Sekundaerluftdiagnoseergebnis n.i.o |
| 0x15 | Sekundaerluftdiagnoseergebnis n.i.o. |
| 0x16 | Sekundaerluftdiagnoseergebnis i.o. |
| 0x20 | Sekundaerluftwicklungstemperatur zu groß |
| 0x21 | SLP-Abbruch (wg. Sek Druckdifferenz, Batteriesp., Motorluftmasse ...) |
| 0x22 | Messphase abgebrochen |
| 0x23 | Offsetphase abgebrochen |
| 0x24 | Vorsteuerung auf außerhalb der Schwellen |
| 0x25 | Vorsteuerung auf außerhalb der Schwellen |
| 0x26 | Vorsteuerung auf außerhalb der Schwellen |
| 0x30 | Motortemperatur noch zu gering ist |
| 0x31 | Wicklungstemperatur noch zu hoch ist |
| 0x32 | Fehler einer das Ergebnis beeinflussenden Komonente |
| 0x33 | Motor-,Ansaugluft- o. Kattemperaturen außerh. Grenzen, B_zslsp nicht geloescht |
| 0x34 | Motorluftmasse außerhalb der Grenzen |
| 0x35 | LSU nicht betriebsbereit, VVT umgeschaltet, r1 nicht im Fenster |
| 0x36 | Tankentlueftung ist aktiv |
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

Dimensions: 5 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | LSU-Dynamikprüfung noch nicht aktiv |
| 0x01 | Dynamikprüfung aktiv |
| 0x02 | LSU-Prüfung abgeschlossen |
| 0x03 | LSU-Prüfung abgeschlossen (Dynamikprüfung noch aktiv) |
| 0xXY | Status LSU-Diagnose kann nicht ausgegeben werden |

<a id="table-lambdastatus"></a>
### LAMBDASTATUS

Dimensions: 6 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x01 | Steuerbetrieb, Startbedingungen noch nicht erfuellt |
| 0x02 | Regelbetrieb mit zwei Sonden |
| 0x04 | Steuerbetrieb durch Betriebsbedingungen |
| 0x08 | Steuerbetrieb nach Systemfehler |
| 0x10 | Regelung mit nur einer Sonde (vor Kat) |
| 0xXY | Status LSU-Diagnose kann nicht ausgegeben werden |

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

<a id="table-betriebsstundenstatus"></a>
### BETRIEBSSTUNDENSTATUS

Dimensions: 4 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Betriebsstundenzaehler verstanden und akzeptiert (top_w &lt; 10h) |
| 0x01 | Betriebsstundenzaehler verstanden aber nicht akzeptiert (top_w &gt; 10h) |
| 0x02 | Betriebsstundenzaehler nicht verstanden und nicht akzeptiert |
| 0xXY | Betriebsstundenzaehler kann nicht ausgegeben werden |

<a id="table-bits"></a>
### BITS

Dimensions: 102 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| B_MILFB | 12 | 0x01 | 0x01 |
| B_MILSL | 13 | 0x01 | 0x01 |
| B_FOFR1 | 19 | 0x01 | 0x01 |
| B_KL15 | 3 | 0x01 | 0x01 |
| B_ESTART | 3 | 0x02 | 0x02 |
| B_KUPPL | 3 | 0x04 | 0x04 |
| B_BL | 3 | 0x08 | 0x08 |
| B_BR | 3 | 0x10 | 0x10 |
| B_KO | 3 | 0x80 | 0x80 |
| B_LL | 3 | 0x01 | 0x01 |
| B_VL | 3 | 0x02 | 0x02 |
| B_SBBHK | 3 | 0x08 | 0x08 |
| B_SBBVK | 3 | 0x20 | 0x20 |
| B_LR | 3 | 0x80 | 0x80 |
| B_KD | 4 | 0x04 | 0x04 |
| B_PN | 4 | 0x08 | 0x08 |
| B_ECULOCK | 4 | 0x10 | 0x10 |
| B_TEHB | 4 | 0x20 | 0x20 |
| B_SA | 4 | 0x40 | 0x40 |
| B_LRNRDY | 4 | 0x80 | 0x80 |
| B_KOE | 21 | 0x08 | 0x08 |
| B_HSVE | 21 | 0x20 | 0x20 |
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
| B_NMOT | 15 | 0x01 | 0x01 |
| B_MINHUBVS | 16 | 0x01 | 0x01 |
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
| B_SSLL | 13 | 0x01 | 0x01 |
| B_TDAON | 14 | 0x01 | 0x01 |
| B_GAD | 2 | 0x01 | 0x01 |
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
| Z_LSH | 2 | 0x02 | 0x02 |
| ENDE | 0 | 0x01 | 0x01 |

<a id="table-t-1byte-fs-dop"></a>
### T_1BYTE_FS_DOP

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Start-/Ansteuerbedingung nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | -- |
| 5 | Funktion laeuft |
| 6 | Funktion beendet (ohne Ergebnis) |
| 7 | Funktion abgebrochen (kein Zyklusflag/Readiness gesetzt) |
| 8 | Funktion vollstaendig durchlaufen (Zyklusflag/Readiness gesetzt) und kein Fehler erkannt |
| 9 | Funktion vollstaendig durchlaufen (Zyklusflag/Readiness gesetzt) und Fehler erkannt |
| 255 | ungueltiger Wert |

<a id="table-t-b-standard-1byte-lesen-0-1"></a>
### T_B_STANDARD_1BYTE_LESEN_0_1

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | 0 |
| 1 | 1 |
| 255 | Groesser 1 |

<a id="table-t-energiesparmodus-lesen"></a>
### T_ENERGIESPARMODUS_LESEN

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Deaktiviert |
| 1 | Fertigungsmodus |
| 2 | Transportmodus |
| 3 | Werkstattmodus |
