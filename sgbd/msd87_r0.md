# msd87_r0.prg

- Jobs: [262](#jobs)
- Tables: [113](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Motorelektronik MSD 87 12 Zylinder N74 Master |
| ORIGIN | BMW EA-360 Markus_Lorch |
| REVISION | 11.000 |
| AUTHOR | P-+-Z-ENGINEERING-GMBH EA-362 Berger |
| COMMENT | SGBD für MSD87 C-Muster mit SW 9SP2C00S |
| PACKAGE | 1.987 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [IDENT](#job-ident) - Identdaten UDS  : $22   ReadDataByIdentifier UDS  : $F150 Sub-Parameter SGBD-Index Modus: Default
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $02 ReadDTCByStatusMask UDS  : $0C StatusMask (Bit2, Bit3) Modus: Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (einzelner Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $04 reportDTCSnapshotRecordByDTCNumber UDS  : $06 reportDTCExtendedDataRecordByDTCNumber UDS  : $09 reportSeverityInformationOfDTC Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen UDS  : $14 ClearDiagnosticInformation UDS  : $FF DTCHighByte UDS  : $FF DTCMiddleByte UDS  : $FF DTCLowByte Modus: Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels UDS  : $22   ReadDataByIdentifier UDS  : $1000 TestStamp Modus: Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. UDS  : $2E   WriteDataByIdentifier UDS  : $1000 TestStamp Modus: Default
- [SVK_LESEN](#job-svk-lesen) - Informationen zur Steuergeraete-Verbau-Kennung UDS  : $22   ReadDataByIdentifier UDS  : $F1xx Sub-Parameter fuer SVK UDS  : $F101 SVK_AKTUELL (Default) Modus: Default
- [STATUS_LESEN](#job-status-lesen) - Lesen eines oder mehrerer Stati UDS  : $22 ReadDataByIdentifier
- [STEUERN](#job-steuern) - Vorgeben eines Status UDS  : $2E WriteDataByIdentifier
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Seriennummer des Steuergeraets UDS  : $22   ReadDataByIdentifier UDS  : $F18C Sub-Parameter ECUSerialNumber Modus: Default
- [STEUERN_ROUTINE](#job-steuern-routine) - Vorgeben eines Status UDS  : $31 RoutineControl
- [IS_LESEN](#job-is-lesen) - Sekundaerer Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $22   ReadDataByIdentifierRequestServiceID UDS  : $2000 DataIdentifier sekundaerer Fehlerspeicher Modus: Default
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - sekundären Fehlerspeicher lesen (Info-Meldungen / Ort und Art) UDS  : $22 ReadDataByIdentifier UDS  : $20 dataIdentifier UDS  : $00 alle Info-Meldungen anschließend UDS  : $20 dataIdentifier UDS  : $nn Details zur Info-Meldung an der Position n Modus: Default
- [HERSTELLINFO_LESEN](#job-herstellinfo-lesen) - Lieferant und Herstelldatum lesen UDS  : $22   ReadDataByIdentifier UDS  : $F18A SystemSupplierIdentifier UDS  : $F18B ECUManufactoringData Modus: Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten UDS  : $3E TesterPresent UDS  : $?0 suppressPosRspMsgIndication Modus: Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen UDS  : $10 StartDiagnosticSession Modus: einstellbar mit diesem Job
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen UDS  : $11 ECUReset UDS  : $04 EnableRapidPowerShutDown Modus: Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $0F0C DataIdentifier ControlEnergySavingMode UDS   : $??   Mode Modus : Default
- [STATUS_ENERGIESPARMODE](#job-status-energiesparmode) - Energy-Saving-Mode auslesen UDS  : $22   ReadDataByIdentifier UDS  : $100A DataIdentifier EnergySavingMode Modus: Default
- [STATUS_BETRIEBSMODE](#job-status-betriebsmode) - Aktueller Betriebsmode SG muss sich im Energiersparmode befinden UDS  : $22   ReadDataByIdentifier UDS  : $100E Sub-Parameter Betriebsmode Modus: Default
- [STEUERN_BETRIEBSMODE](#job-steuern-betriebsmode) - Betriebsmode setzen SG muss sich im Energiersparmode befinden UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $1003 DataIdentifier Betriebsmode UDS  : $0?   Betriebsmode Modus: Default
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers Modus: Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers UDS  : $16xx SubbusMemberSerialNumber Modus: Default
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [CBS_INFO](#job-cbs-info) - Ausgabe der CBS-Version
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (fuer CBS-Version 5) UDS: $22 ReadDataByIdentifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS-Version 5) UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit 'Strich_Punkt' getrennt (nicht mit Komma!)
- [STEUERN_ROE_STOP](#job-steuern-roe-stop) - Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events [$02 eventWindowTime - infinite (nur 35up)] 35up: LH Diagnosemaster V11 oder höher pre35up: LH Diagnosemaster V6 - V9
- [STEUERN_ROE_START](#job-steuern-roe-start) - Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [CPS_LESEN](#job-cps-lesen) - Codierpruefstempel lesen UDS  : $22   ReadDataByIdentifier UDS  : $37FE DataIdentifier Codierpruefstempel Modus: Default
- [DIAG_SESSION_LESEN](#job-diag-session-lesen) - Aktive Diagnose-Session auslesen UDS  : $22   ReadDataByIdentifier UDS  : $F186 ActiveDiagnosticSession Modus: Default
- [FLASH_TP_LESEN](#job-flash-tp-lesen) - Flash Timing Parameter auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2504 FlashTimingParameter Modus: Default
- [PROG_ZAEHLER_LESEN](#job-prog-zaehler-lesen) - Programmierzaehler lesen UDS  : $22   ReadDataByIdentifier UDS  : $2502 ProgrammingCounter Modus: Default
- [PROG_MAX_LESEN](#job-prog-max-lesen) - Anzahl der maximal möglichen Programmiervorgänge auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2503 ProgrammingCounter Modus: Default
- [STATUS_EISYDR](#job-status-eisydr) - 0x3103F0E2 STATUS_EISYDR Auslesen Eisy-Adaptionswerte mit Druckregelung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_READINESS](#job-status-readiness) - 0x224105 STATUS_READINESS Monitorfunktionen und Readinessflags aus DME auslesen
- [STEUERN_ENDE_LSH1](#job-steuern-ende-lsh1) - 0x2F60D000 STEUERN_ENDE_LSH1 Lambdasondenheizung vor Kat Bank1 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_AEP_I12_ZYKLISCHES_NACHLADEN_HISTOGRAMM](#job-status-aep-i12-zyklisches-nachladen-histogramm) - Auslesen der Histogramme über die Standzeit bis zum Beginn des zyklischen Nachladens und der Ladedauern der zyklischen Nachladevorgänge AEP_I12_ZYKLISCHES_NACHLADEN_HISTOGRAMM (0x22 409E)
- [STEUERN_ENDE_LSH2](#job-steuern-ende-lsh2) - 0x2F60D100 STEUERN_ENDE_LSH2 Lambdasondenheizung hinter Kat Bank1 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_AGK](#job-steuern-agk) - 0x2F60C103 STEUERN_AGK Abgasklappe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [_STATUS_GENINFO](#job-status-geninfo) - 0x22401B _STATUS_GENINFO Infospeicher Generatordiagnose erweitert auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_VORKONFIG_OPF](#job-status-vorkonfig-opf) - 0x3103F082 STATUS_VORKONFIG_OPF Vorkonditionierung Otto Partikelfilter auslesen
- [STATUS_SYSTEMCHECK_L_REGELUNG_AUS](#job-status-systemcheck-l-regelung-aus) - 0x3103F0D9 STATUS_SYSTEMCHECK_L_REGELUNG_AUS Auslesen Lambdaregelung ausschalten Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ELUER](#job-steuern-eluer) - 0x2F608103 STEUERN_ELUER E-Luefter-Relais ansteuern NO_CON
- [STEUERN_RUHESTROMMESSUNG](#job-steuern-ruhestrommessung) - Ansteuern Ruhestrompruefung mit IBS UDS  : $31 RoutineControl UDS  : $01 startRoutine UDS  : $F02B Ruhestrompruefung
- [IDENT_IBS](#job-ident-ibs) - 0x224021 IDENT_IBS Identifikationsdaten fuer IBS-Sensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_EVAUSBL](#job-status-systemcheck-evausbl) - 0x3103F025 STATUS_SYSTEMCHECK_EVAUSBL Auslesen Diagnosefunktion EinspritzVentile EV-Ausblendung !ACHTUNG: hier wird die Zuendreihenfolge Bitcodiert verwendet! Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_IGRINFO_AEP](#job-status-igrinfo-aep) - 0x224016 STATUS_IGRINFO_AEP Infospeicher Intelligente Generator Regelung (IGR) auslesen
- [STATUS_RBMMS3](#job-status-rbmms3) - 0x224066 STATUS_RBMMS3 Rate Based Monitoring Motorsteuerung MS... Block 3 auslesen
- [STATUS_RBMMS2](#job-status-rbmms2) - 0x224028 STATUS_RBMMS2 Rate Based Monitoring Motorsteuerung MS (VDO) Block 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_RBMMS1](#job-status-rbmms1) - 0x224027 STATUS_RBMMS1 Rate Based Monitoring Motorsteuerung MS (VDO) Block 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [START_AEP_I12_ZYKNL_INFOSPEICHER_LOESCHEN](#job-start-aep-i12-zyknl-infospeicher-loeschen) - Löschen des Historienspeichers für die letzen 4 Ladevorgänge der 12V-Batterie aus der Hochvolt-Batterie AEP_I12_ZYKNL_INFOSPEICHER_LOESCHEN (0x31 01 AE02)
- [STEUERN_DMTL_P](#job-steuern-dmtl-p) - 0x2F60CC03 STEUERN_DMTL_P Diagnosemodul-Tank Leckage Pumpe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STATUS_SYSTEMCHECK_TEV](#job-status-systemcheck-tev) - 0x3103F022 STATUS_SYSTEMCHECK_TEV Auslesen Diagnosefunktion Tankentlueftungsventil Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_DMTL_V](#job-steuern-dmtl-v) - 0x2F60CD03 STEUERN_DMTL_V Diagnosemodul-Tank Leckage Ventil ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STATUS_EISYGD](#job-status-eisygd) - 0x3103F0E1 STATUS_EISYGD Auslesen Eisy-Adaptionswerte (gedrosselt) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_EML](#job-steuern-eml) - 0x2F60D603 STEUERN_EML EML (Engine Malfunction Lamp) ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [STEUERN_PM_HISTOGRAM_RESET](#job-steuern-pm-histogram-reset) - $2E 5F F5 04 Loeschen von pminfo1 index 23-30
- [START_SYSTEMCHECK_OPF](#job-start-systemcheck-opf) - 0x3101F07B START_SYSTEMCHECK_OPF OPF Systemtest   Für Master-Slave Projekte Kopplung der Start Routine über Master notwendig.
- [START_OBD_DEMO_GANGEINLEGEN](#job-start-obd-demo-gangeinlegen) - 0x3101F09D START_OBD_DEMO_GANGEINLEGEN OBD Demo Gangeinlegen
- [STATUS_RBMMODE9](#job-status-rbmmode9) - 0x224026 STATUS_RBMMODE9 Rate Based Monitoring Mode 9 auslesen (Ausgabe der Werte wie im Scantool Mode 9) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_TYPPRUEFNR](#job-status-typpruefnr) - 0x224047 STATUS_TYPPRUEFNR Typpruefnummer fuer BN2020-SGs lesen
- [STEUERN_EKP](#job-steuern-ekp) - 0x2F60D803 STEUERN_EKP Elektrische Kraftstoffpumpe 1 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STOP_OBD_DEMO_GANGEINLEGEN](#job-stop-obd-demo-gangeinlegen) - 0x3102F09D STOP_OBD_DEMO_GANGEINLEGEN OBD Demo Gangeinlegen  beenden
- [STEUERN_KVA](#job-steuern-kva) - 0x2E5FC1 STEUERN_KVA KraftstoffVerbrauchsAnzeige - Korrekturfaktor schreiben Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_VERBREDINFO](#job-status-verbredinfo) - 0x22401D STATUS_VERBREDINFO Verbraucherreduzierungsspeicher auslesen
- [_STATUS_AEP_I12_TEST_BATTERYGUARD](#job-status-aep-i12-test-batteryguard) - Anforderung Aufruf BatteryGuard Call auslesen Startvoraussetzungen: B_kl15 == TRUE. AEP_I12_TEST_BATTERYGUARD (0x31 03 F052)
- [STEUERN_OBD_TESTGROUP](#job-steuern-obd-testgroup) - 0x2EF813 Setzen der OBD_TESTGROUP
- [STEUERN_UGEN](#job-steuern-ugen) - 0x2F603203 STEUERN_UGEN Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1
- [STATUS_HIST_REGENERATIONSGRUND_OPF](#job-status-hist-regenerationsgrund-opf) - 0x22411D STATUS_HIST_REGENERATIONSGRUND_OPF Temperaturverteilung des OPF lesen
- [STEUERN_ENDE_ENWS](#job-steuern-ende-enws) - 0x2F60ED00 STEUERN_ENDE_ENWS Vanos Einlass Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_BATTERIETAUSCH_REGISTRIEREN](#job-steuern-batterietausch-registrieren) - UDS $31 01 F030 Batterietausch registrieren
- [STEUERN_RAM](#job-steuern-ram) - 0x3101F0F2 STEUERN_RAM Ansteuern RAM Backup zwangssichern
- [STOP_SYSTEMCHECK_SEK_LUFT](#job-stop-systemcheck-sek-luft) - 0x3102F020 STOP_SYSTEMCHECK_SEK_LUFT Diagnosefunktion Sekundaerluft beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_TEV](#job-steuern-tev) - 0x2F60CF03 STEUERN_TEV Tankentlueftungsventil ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [STATUS_BZETOMSA2](#job-status-bzetomsa2) - 0x224093 STATUS_BZETOMSA2 Analyse von MSA-Abschaltverhinderern durch BZE3 gegenüber AEPBZE SDG(A2l-NAME=bzetomsa)
- [STATUS_BZETOMSA](#job-status-bzetomsa) - 0x224155 STATUS_BZETOMSA Analyse von MSA-Abschaltverhinderern durch BZE3 gegenüber AEPBZE SDG(A2l-NAME=bzetomsa)
- [STEUERN_ENDE_LDS1](#job-steuern-ende-lds1) - 0x2F60B600 STEUERN_ENDE_LDS1 Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_TEV_REGELUNG_AUS](#job-status-tev-regelung-aus) - 0x3103F0CF STATUS_TEV_REGELUNG_AUS Deaktivierung TEV-Regelung auslesen
- [STEUERN_LLABG_PROG](#job-steuern-llabg-prog) - 0x2E5FF008 STEUERN_LLABG_PROG Abgleichwert LL (Leerlauf) programmieren Aktivierung: Klemme 15 = EIN UND Leerlaufabgleich ueber Testervorgabe = EIN Activation: LV_IGK = 1 UND LV_KWP_ENA = 1
- [STEUERN_IBS_STROMMESSUNG](#job-steuern-ibs-strommessung) - Ansteuern IBS Strommessung UDS: $31 RoutineControl
- [STATUS_OPF_TAUSCH_BANK1](#job-status-opf-tausch-bank1) - 0x224195 STATUS_OPF_TAUSCH_BANK1 Nutzung  des OPF lesen
- [STEUERN_DMTL_HEIZUNG](#job-steuern-dmtl-heizung) - 0x2F60CE03 STEUERN_DMTL_HEIZUNG Diagnosemodul-Tank Leckage Heizung ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [START_OPF_DRUCKSCHLAUCHABFALL](#job-start-opf-druckschlauchabfall) - 0x3101F09F START_OPF_DRUCKSCHLAUCHABFALL Diagnosefunktion OPF Druckschlauchabfall   (Für Master-Slave Projekte Kopplung der Start Routine über Master notwendig.)
- [STATUS_BZEDIAG2](#job-status-bzediag2) - Auslesen Infospeicher Batteriezustandserkennung 2 UDS*: $22 ReadDataByIdentifier
- [STOP_SYSTEMCHECK_L_REGELUNG_AUS](#job-stop-systemcheck-l-regelung-aus) - 0x3102F0D9 STOP_SYSTEMCHECK_L_REGELUNG_AUS Ende Lambdaregelung ausschalten Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_CBSMOTOROELHIST](#job-status-cbsmotoroelhist) - 0x22404F STATUS_CBSMOTOROELHIST CBS Motoroel Historien-Funktion lesen (FASTA)
- [STATUS_SERVICEREGENERATION_OPF](#job-status-serviceregeneration-opf) - 0x22419A STATUS_SERVICEREGENERATION_OPF Nutzung  des OPF lesen
- [STATUS_BZEDIAG](#job-status-bzediag) - 0x22403B STATUS_BZEDIAG BZE Infospeicher
- [STATUS_CALCVN](#job-status-calcvn) - Cal-ID (Calibration-ID) und CVN(Calibration Verification Number) auslesen. CALCVN (0x403C)
- [STEUERN_PM_RESTORE](#job-steuern-pm-restore) - 0x2E5F8B STEUERN_PM_RESTORE Schreiben PM-Restore Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_LL_ABGLEICH](#job-steuern-ll-abgleich) - 0x2E5FF007 STEUERN_LL_ABGLEICH Abgleichwert LL (Leerlauf) vorgeben Aktivierung: Klemme 15 = EIN UND Leerlaufabgleich ueber Testervorgabe = EIN Activation: LV_IGK = 1 UND LV_KWP_ENA = 1
- [STATUS_KRANN](#job-status-krann) - 0x3103F0E3 STATUS_KRANN Auslesen Krann-Adaptionswerte Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_TEV](#job-stop-systemcheck-tev) - 0x3102F022 STOP_SYSTEMCHECK_TEV Diagnosefunktion Tankentlueftungsventil beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_PM_BACKUP](#job-status-pm-backup) - 0x225F8B STATUS_PM_BACKUP Auslesen des PM-Backup Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_NUTZUNG_OPF](#job-status-nutzung-opf) - 0x224119 STATUS_NUTZUNG_OPF Nutzung  des OPF lesen
- [STEUERN_EISYDR](#job-steuern-eisydr) - 0x3101F0E2 STEUERN_EISYDR Ansteuern Eisy-Adaptionswerte mit Druckregelung (Anforderung aus CP5403)
- [START_VANOSSPUELEN](#job-start-vanosspuelen) - 0x3101F042 START_VANOSSPUELEN VANOS Spuelen fuer OBD und PVE. 
- [STEUERN_ENDE_EML](#job-steuern-ende-eml) - 0x2F60D600 STEUERN_ENDE_EML EML (Engine Malfunction Lamp) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [ADAP_SELEKTIV_LOESCHEN](#job-adap-selektiv-loeschen) - 0x3101F030 ADAP_SELEKTIV_LOESCHEN Ansteuern Adaptionen selektiv loeschen Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - 0x2F60DA03 STEUERN_E_LUEFTER E-Luefter ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Motortemperatur &lt; 95 Grad C UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND TCO &lt; C_TCO_MAX_KWP UND LV_IGK = 1
- [STATUS_OPF_DIAG](#job-status-opf-diag) - 0x2240EF STATUS_OPF_DIAG Otto Partikelfilter Verbaudiagnosestatus auslesen
- [STATUS_VERBRAUCHERSTROM_EFII](#job-status-verbraucherstrom-efii) - Auslesen Verbraucherstrommessung EFII UDS  : $31   RoutineControl UDS  : $03   routineControlType UDS  : $7002 routineIdentifier
- [STEUERN_ENDE_DK](#job-steuern-ende-dk) - 0x2F602A00 STEUERN_ENDE_DK Drosselklappe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_ATL](#job-stop-systemcheck-atl) - 0x3102F0D0 STOP_SYSTEMCHECK_ATL Diagnosefunktion Abgasturbolader beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MSAINFO2](#job-status-msainfo2) - Auslesen Infospeicher Batteriezustandserkennung 2 UDS*: 0x224092 ReadDataByIdentifier
- [STEUERN_MSVHDP5](#job-steuern-msvhdp5) - 0x2F60EF03 STEUERN_MSVHDP5 Mengensteuerventil HDP5 ansteuern NO_CON
- [STEUERN_ENDE_EKP](#job-steuern-ende-ekp) - 0x2F60D800 STEUERN_ENDE_EKP Elektrische Kraftstoffpumpe 1 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DFDSN](#job-status-dfdsn) - 0x224156 STATUS_DFDSN Diagnose der Generatorauslastung über FASTA
- [STATUS_BETRIEBSSTUNDENZAEHLER](#job-status-betriebsstundenzaehler) - 0x224AB4 STATUS_BETRIEBSSTUNDENZAEHLER Betriebsstundenzaehler auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_UGEN](#job-steuern-ende-ugen) - 0x2F603200 STEUERN_ENDE_UGEN Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_LEMINFO_AEP](#job-status-leminfo-aep) - 0x224017 STATUS_LEMINFO_AEP Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen
- [STATUS_IBS_STROMMESSUNG](#job-status-ibs-strommessung) - Auslesen IBS Strommessung UDS: $31 RoutineControl
- [ABGLEICHWERTE_SCHREIBEN](#job-abgleichwerte-schreiben) - 0x2E5F90 ABGLEICHWERTE_SCHREIBEN Abgleichwerte Injektoren programmieren für CASCADE mit Übernahme Daten aus COD-Datei Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STATUS_MOTORLAUFUNRUHE](#job-status-motorlaufunruhe) - 0x224003 STATUS_MOTORLAUFUNRUHE Motorlaufunruhewerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MESSWERTE](#job-status-messwerte) - 0x224000 STATUS_MESSWERTE Messwerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_IDENT_OPF](#job-status-ident-opf) - 0x224117 STATUS_IDENT_OPF Ladungsbilanz des OPF lesen
- [STEUERN_ENDE_AGK](#job-steuern-ende-agk) - 0x2F60C100 STEUERN_ENDE_AGK Abgasklappe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_OBD_DEMO_MOMENTENBEGRENZUNG](#job-status-obd-demo-momentenbegrenzung) - 0x3103F09E STATUS_OBD_DEMO_MOMENTENBEGRENZUNG OBD Demo Momentenbegrenzung
- [STEUERN_EISYGD](#job-steuern-eisygd) - 0x3101F0E1 STEUERN_EISYGD Ansteuern Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403)
- [START_SYSTEMCHECK_IGR_AUS](#job-start-systemcheck-igr-aus) - 0x3101F0F7 START_SYSTEMCHECK_IGR_AUS Ansteuerung Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EWS4_SK](#job-status-ews4-sk) - Lesen des SecretKey des Server sowie Client für EWS4 UDS   : $22   ReadDataByIdentifier UDS   : $C002 Sub-Parameter
- [START_AEP_I12_ZYKNL_HISTOGRAMM_LOESCHEN](#job-start-aep-i12-zyknl-histogramm-loeschen) - Löschen von Histogramm und Zähler aller Ladevorgänge der 12V-Batterie aus dem Hochvolt-System AEP_I12_ZYKNL_HISTOGRAMM_LOESCHEN (0x31 01 AE03)
- [STATUS_DIGITAL_0](#job-status-digital-0) - 0x224007 STATUS_DIGITAL_0 Status Schaltzustaende 0 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DIGITAL_1](#job-status-digital-1) - 0x224002 STATUS_DIGITAL_1 Status Schaltzustaende Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_IGR_AUS](#job-stop-systemcheck-igr-aus) - 0x3102F0F7 STOP_SYSTEMCHECK_IGR_AUS Ende Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_OBD_DEMO_GANGEINLEGEN](#job-status-obd-demo-gangeinlegen) - 0x3103F09D STATUS_OBD_DEMO_GANGEINLEGEN OBD Demo Gangeinlegen
- [STEUERN_PROGRAMM_IMAALLE](#job-steuern-programm-imaalle) - 0x2E5F90 STEUERN_PROGRAMM_IMAALLE Abgleichwerte Injektoren programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STATUS_SYSTEMCHECK_DMTL](#job-status-systemcheck-dmtl) - 0x3103F0DA STATUS_SYSTEMCHECK_DMTL Auslesen Diagnosefunktion DMTL Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_WAPUT](#job-steuern-ende-waput) - 0x2F608300 STEUERN_ENDE_WAPUT Wasserpumpe Turbolader auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_TEV_REGELUNG_AUS](#job-steuern-ende-tev-regelung-aus) - 0x3102F0CF STEUERN_ENDE_TEV_REGELUNG_AUS Deaktivierung TEV-Regelung beenden
- [STEUERN_ENDE_ELUER](#job-steuern-ende-eluer) - 0x2F608100 STEUERN_ENDE_ELUER E-Luefter-Relais Ansteuerung beenden NO_CON
- [START_SYSTEMCHECK_DMTL](#job-start-systemcheck-dmtl) - 0x3101F0DA START_SYSTEMCHECK_DMTL Ansteuern Diagnosefunktion DMTL Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_CODIERUNG_OEL](#job-status-codierung-oel) - 0x223320 STATUS_CODIERUNG_OEL Codierung fuer Oelwechselintervall auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_START_AEP_I12_TEST_BATTERYGUARD](#job-start-aep-i12-test-batteryguard) - Anforderung Aufruf BatteryGuard Call Setzen der Größe B_batteryguardcalldiag =1 Startvoraussetzungen: B_kl15 == TRUE. AEP_I12_TEST_BATTERYGUARD (0x31 01 F052)
- [START_SYSTEMCHECK_EVAUSBL](#job-start-systemcheck-evausbl) - 0x3101F025 START_SYSTEMCHECK_EVAUSBL Ansteuern Diagnosefunktion Einspritzventilausblendung!ACHTUNG: hier wird die Zuendreihenfolge Bitcodiert verwendet! Aktivierung: Klemme 15 = EIN UND Motorstatus = (Leerlauf ODER Teillast) UND Drehzahl &lt; 3000 1/min Activation: LV_IGK = 1 UND STATE_ENG = (IS ODER PL) UND N &lt; C_N_MAX_KWP
- [START_OBD_DEMO_MOMENTENBEGRENZUNG](#job-start-obd-demo-momentenbegrenzung) - 0x3101F09E START_OBD_DEMO_MOMENTENBEGRENZUNG OBD Demo Momentenbegrenzung
- [STATUS_BLOCK_LESEN](#job-status-block-lesen) - Lesen eines dynamisch definierten Datenblockes UDS  : $2C DynamicallyDefineDataIdentifier $03 ClearDynamicallyDefinedDataIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $2C DynamicallyDefineDataIdentifier $01 DefineByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $22 ReadDataByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  $2C$02 DefineByMemoryAddress wird nicht unterstützt 'Composite data blocks' werden nur komplett unterstützt
- [STATUS_EWS](#job-status-ews) - Zurücklesen verschiedener interner Stati für EWS UDS   : $22   ReadDataByIdentifier UDS   : $C000 Sub-Parameter
- [STATUS_LL_ABGLEICH](#job-status-ll-abgleich) - 0x225FF0 STATUS_LL_ABGLEICH Abgleichwert LL (Leerlauf) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_ATL](#job-status-systemcheck-atl) - 0x3103F0D0 STATUS_SYSTEMCHECK_ATL Diagnosefunktion Abgasturbolader auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_CTG](#job-status-ctg) - 0x22409B STATUS_CTG CtG-Conti: Bereitstellung der Statistiken von Diagnoseergebnissen von Close-the-Gap fuer das Feldmonitoring fuer MSD80/87 (N53-54 / N74) und MSV80 (N51-52KP). !!! Wegen Umrechnungsfehler in Include (Rest) definiert !!!
- [STATUS_DFDSPROFLE](#job-status-dfdsprofle) - Generatorauslastungsprofil auslesen DFDSPROFLE (0x22 4081)
- [STATUS_VANOSSPUELEN](#job-status-vanosspuelen) - 0x3103F042 STATUS_VANOSSPUELEN VANOS Spuelen fuer OBD und PVE.
- [STEUERN_TEV_REGELUNG_AUS](#job-steuern-tev-regelung-aus) - 0x3101F0CF STEUERN_TEV_REGELUNG_AUS Deaktivierung TEV-Regelung starten
- [STATUS_LADUNGSBILANZ_OPF](#job-status-ladungsbilanz-opf) - 0x224118 STATUS_LADUNGSBILANZ_OPF Ladungsbilanz des OPF lesen
- [START_VORKONFIG_OPF](#job-start-vorkonfig-opf) - 0x3101F082 START_VORKONFIG_OPF Vorkonditionierung Otto Partikelfilter starten Startvorraussetzungen: Freigabe über Applikationsschalter, Geschwindigkeit , GWS N oder P (AT), Neutral (MT), Gaspedal
- [STOP_SYSTEMCHECK_DMTL](#job-stop-systemcheck-dmtl) - 0x3102F0DA STOP_SYSTEMCHECK_DMTL Diagnosefunktion DMTL beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_ZGH](#job-steuern-ende-zgh) - 0x3102F034 STEUERN_ENDE_ZGH Ende Zylinder Gleichstellung Homogen
- [_SWE_LESEN](#job-swe-lesen) - 0x31010205 SWE_LESEN Informationen zu Softwareeinheiten auf dem Steuergerät unter Verwendung des Jobs SVK_LESEN UDS  : $31   RoutinControl by RequestSerice ID UDS  : $01xx Sub-Parameter fuer SVK UDS  : $0205 SWEDI (Default) Modus: Default
- [STATUS_ADAPTION_GEMISCH](#job-status-adaption-gemisch) - 0x22400A STATUS_ADAPTION_GEMISCH Gemischadaptionswerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_KFT](#job-steuern-ende-kft) - 0x2F60C900 STEUERN_ENDE_KFT Kennfeldthermostat Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_HIST_TEMPERATUR_OPF](#job-status-hist-temperatur-opf) - 0x22411E STATUS_HIST_TEMPERATUR_OPF Temperaturverteilung des OPF lesen
- [STEUERN_ULV](#job-steuern-ulv) - 0x2F60B503 STEUERN_ULV Umluftventil ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1
- [STATUS_IMAALLE](#job-status-imaalle) - 0x225F90 STATUS_IMAALLE Abgleichwerte Injektoren auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_ATLDIAG](#job-status-atldiag) - 0x224044 STATUS_ATLDIAG Turboladerstatus auslesen
- [START_SYSTEMCHECK_ATL](#job-start-systemcheck-atl) - 0x3101F0D0 START_SYSTEMCHECK_ATL Diagnosefunktion Abgasturbolader starten 
- [SPEICHER_LESEN_ASCII](#job-speicher-lesen-ascii) - 0x23 SPEICHER_LESEN_ASCII Auslesen des Steuergeraete-Speichers Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_RUHESTROMMESSUNG](#job-status-ruhestrommessung) - Auslesen Ruhestromprüfung mit IBS UDS  : $31 RoutineControl UDS  : $03 requestRoutineResults UDS  : $F02B Ruhestrompruefung
- [STEUERN_EWS4_SK](#job-steuern-ews4-sk) - 17 "EWS4-data" schreiben UDS   : $2E   WriteDataByIdentifier UDS   : $C001 Sub-Parameter
- [STEUERN_ENDE_UVLSS](#job-steuern-ende-uvlss) - 0x2F602000 STEUERN_ENDE_UVLSS Versorgung Einspritzung / Zuendung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STEUERN_AEP_I12_TEST_LADEENDEGRUND](#job-steuern-aep-i12-test-ladeendegrund) - Job zum Test für AEP Funktionen AEP_I12_GRUND_LADEENDE (0x2E 5FA0)
- [STATUS_AEP_I12_ZYKLISCHES_NACHLADEN_INFO](#job-status-aep-i12-zyklisches-nachladen-info) - Auslesen von wichtigen Kenngrößen der letzten 4 Vorgänge des zykllischen Nachladens plus dem letzten Parkvorgang AEP_I12_ZYKLISCHES_NACHLADEN_INFO (0x22 409D)
- [STEUERN_GVOBD](#job-steuern-gvobd) - 0x2E5F8007 STEUERN_GVOBD Gemischvertrimmung fuer OBD-Demo und PVE vorgeben. Der Korrekturfaktor soll bei Klemmenwechsel auf den Standardwert "1" zurueckgesetzt werden.
- [STATUS_OBD_TESTGROUP](#job-status-obd-testgroup) - 0x22F813  STATUS_OBD_TESTGROUP Abfragen der Antriebsstrang Identifier
- [STATUS_MFMA_DS](#job-status-mfma-ds) - 0x22403E STATUS_MFMA_DS Adaptionswerte MFMA_DS Lesen
- [STATUS_SYSTEMCHECK_SEK_LUFT](#job-status-systemcheck-sek-luft) - 0x3103F020 STATUS_SYSTEMCHECK_SEK_LUFT Auslesen Diagnosefunktion Sekundaerluft Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_AEPDFMONITOR](#job-status-aepdfmonitor) - 0x224015 STATUS_AEPDFMONITOR FASTA-Messwertblock 10 lesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_IGR_AUS](#job-status-systemcheck-igr-aus) - 0x3103F0F7 STATUS_SYSTEMCHECK_IGR_AUS Auslesen Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [SWE_KOMPLETT_LESEN](#job-swe-komplett-lesen) - 0x31010205 SWE_KOMPLETT_LESEN Informationen zu Softwareeinheiten auf dem Steuergerät unter Verwendung des Jobs SVK_LESEN UDS  : $31   RoutinControl by RequestSerice ID UDS  : $01xx Sub-Parameter fuer SVK UDS  : $0205 SWEDI (Default) Modus: Default
- [STATUS_MESSWERTE_LRP](#job-status-messwerte-lrp) - 0x22402D STATUS_MESSWERTE_LRP Messwerte Laufruhepruefung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_WAPUT](#job-steuern-waput) - 0x2F608303 STEUERN_WAPUT Wasserpumpe Turbolader ansteuern (Lagerstuhl) Aktivierung: Batteriespannung &gt; 10 V UND Motortemperatur &lt; 95 Grad C UND Drehzahl = 0 1/min  UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND TCO &lt; C_TCO_MAX_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STATUS_SYSTEMCHECK_LLERH](#job-status-systemcheck-llerh) - 0x3103F026 STATUS_SYSTEMCHECK_LLERH Auslesen Diagnosefunktion Leerlauf-Erhoehung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_KLANN](#job-steuern-klann) - 0x3101F0E4 STEUERN_KLANN Ansteuern Krann-Adaptionswerte (Anforderung aus CP10798)
- [_STOP_AEP_I12_TEST_BATTERYGUARD](#job-stop-aep-i12-test-batteryguard) - Anforderung Aufruf BatteryGuard Call beenden Setzen der Größe B_batteryguardcalldiag =0 Startvoraussetzungen: B_kl15 == TRUE. AEP_I12_TEST_BATTERYGUARD (0x31 02 F052)
- [STEUERN_ENDE_MSV](#job-steuern-ende-msv) - 0x2F60BD00 STEUERN_ENDE_MSV Mengensteuerventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_DMTL_HEIZUNG](#job-steuern-ende-dmtl-heizung) - 0x2F60CE00 STEUERN_ENDE_DMTL_HEIZUNG Diagnosemodul-Tank Leckage Heizung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [START_SYSTEMCHECK_LLERH](#job-start-systemcheck-llerh) - 0x3101F026 START_SYSTEMCHECK_LLERH Ansteuern Diagnosefunktion Leerlauf-Erhoehung
- [STEUERN_SLP](#job-steuern-slp) - 0x2F60CB03 STEUERN_SLP Sekundaerluftpumpe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STATUS_OPF_DRUCKSCHLAUCHABFALL](#job-status-opf-druckschlauchabfall) - 0x3103F09F STATUS_OPF_DRUCKSCHLAUCHABFALL Diagnosefunktion OPF Druckschlauchabfall
- [STEUERN_ANWS](#job-steuern-anws) - 0x2F60EE03 STEUERN_ANWS Vanos Auslass Ventil ansteuern Aktivierung: Drehzahl &gt; 1000 1/min Activation: N &gt; C_N_MIN_KWP
- [STEUERN_ENDE_TEV](#job-steuern-ende-tev) - 0x2F60CF00 STEUERN_ENDE_TEV Tankentlueftungsventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_RAM](#job-status-ram) - 0x3103F0F2 STATUS_RAM Auslesen RAM Backup zwangssichern
- [ADAP2_SELEKTIV_LOESCHEN](#job-adap2-selektiv-loeschen) - 0x3101F031 ADAP2_SELEKTIV_LOESCHEN Ansteuern Adaptionen 2 selektiv loeschen Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STATUS_MESSWERTE_IBS](#job-status-messwerte-ibs) - 0x22402B STATUS_MESSWERTE_IBS Messwerte IBS auslesen
- [STEUERN_HDPR](#job-steuern-hdpr) - 0x2F608203 STEUERN_HDPR Hochdruckpumpenrelais ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_ENDE_ULV](#job-steuern-ende-ulv) - 0x2F60B500 STEUERN_ENDE_ULV Umluftventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_PM_MESSEMODE](#job-status-systemcheck-pm-messemode) - 0x3103F0F6 STATUS_SYSTEMCHECK_PM_MESSEMODE Auslesen Messemode Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_KQE](#job-status-kqe) - 0x224035 STATUS_KQE Messwerte zur Kraftstoffqualitaet auslesen
- [STOP_VORKONFIG_OPF](#job-stop-vorkonfig-opf) - 0x3102F082 STOP_VORKONFIG_OPF Vorkonditionierung Otto Partikelfilter stoppen
- [STEUERN_ZGH](#job-steuern-zgh) - 0x3101F034 STEUERN_ZGH Ansteuern Zylinder Gleichstellung Homogen
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - 0x225F90 ABGLEICHWERTE_LESEN Abgleichwerte Injektoren auslesen für CASCADE für Vergleich mit Daten aus COD-Datei Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DFMONITOR](#job-status-dfmonitor) - 0x224001 STATUS_DFMONITOR Batterieladezustand auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_OPF](#job-stop-systemcheck-opf) - 0x3102F07B STOP_SYSTEMCHECK_OPF OPF Systemtest  beenden  Bei Master Slave Projekten Kopplung notwendig.
- [STOP_SYSTEMCHECK_PM_MESSEMODE](#job-stop-systemcheck-pm-messemode) - 0x3102F0F6 STOP_SYSTEMCHECK_PM_MESSEMODE Ende Messemode Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [MESSWERTBLOCK_LESEN](#job-messwertblock-lesen) - 0x2CF0 MESSWERTBLOCK_LESEN DDLI Messwerte auf Basis Übergabestring aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1 es können 40 Messwerte in einem Block zusammengefasst werden
- [STEUERN_EWAP](#job-steuern-ewap) - 0x2F60BF03 STEUERN_EWAP elektr. Wasserpumpe ueber LIN ansteuern nur bei Fahrzeuggeschwindigkeit v=0 und Motortemperatur TMOT kleiner 115gradCelsius und Batteriespannung UBAT groesser 10Volt CON_EWAP
- [STEUERN_ENDE_SLP](#job-steuern-ende-slp) - 0x2F60CB00 STEUERN_ENDE_SLP Sekundaerluftpumpe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_GEN](#job-stop-systemcheck-gen) - 0x3102F02A STOP_SYSTEMCHECK_GEN Diagnosefunktion Generatortest beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_KFT](#job-steuern-kft) - 0x2F60C903 STEUERN_KFT Kennfeldthermostat ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [STEUERN_PROGRAMM_GVOBD](#job-steuern-programm-gvobd) - 0x2E5F8008 STEUERN_PROGRAMM_GVOBD Gemischvertrimmung fuer OBD-Demo und PVE programmieren.
- [_STATUS_BZEINFO](#job-status-bzeinfo) - 0x22401A _STATUS_BZEINFO Infospeicher Batterie Zustands Erkennung (BZE) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_DK](#job-steuern-dk) - 0x2F602A03 STEUERN_DK Drosselklappe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [START_SYSTEMCHECK_SEK_LUFT](#job-start-systemcheck-sek-luft) - 0x3101F020 START_SYSTEMCHECK_SEK_LUFT Ansteuern Diagnosefunktion Sekundaerluft Aktivierung: Leerlauf UND Motortemperatur &gt; 75 Grad C UND Ueberspannung = AUS UND LV_TEMP_MAX_SAP_COIL = 0 UND Fehlerspeichereintrag Sekundaerluftmassenmesser = Aus UND Fehlerspeichereintrag Sekundaerluftsystem = AUS UND Fehlerspeichereintrag Luftmassenmesser = AUS UND Fehlerspeichereintrag Umgebungsdrucksensor = 0 UND Fehlerspeichereintrag Umgebungsdrucksensor Plausibilitaet = AUS UND Fehlerspeichereintrag Kuehlmitteltemperatursensor = AUS UND Fehlerspeichereintrag Kurbelwellensensor = AUS UND Fehlerspeichereintrag Tankfuellstand zu gering = AUS UND LV_MIS_STATE_A = 0 UND LV_MIS_STATE_B = 0 UND Fehlerspeichereintrag Sekundaerluftventil = AUS UND Fehlerspeichereintrag Sekundaerluftpumpe = AUS UND Fehlerspeichereintrag Umgebungsdrucksensor = 0 UND Fehlerspeichereintrag Drosselklappenstellung Plausibilitaet = 0 UND (Diagnosestatus Sekundaerluftmassenmesser = SAFM_DIAG_END ODER SAFM_DIAG_CNL) Activation: LV_IS = 1 UND TCO &gt; C_TCO_MIN_SA_EOL UND LV_VB_JUMP = 0 UND LV_TEMP_MAX_SAP_COIL = 0 UND LV_ERR_SA_SAFM = 0 UND LV_ERR_SA_SYS = 0 UND LV_ERR_SA_SAV = 0 UND LV_ERR_MAF = 0 UND LV_ERR_AMP = 0 UND LV_ERR_AMP_PLAUS = 0 UND LV_ERR_TCO = 0 UND LV_ERR_CRK = 0 UND LV_ERR_FTL_MIN = 0 UND LV_MIS_STATE_A = 0 UND LV_MIS_STATE_B = 0 UND LV_ERR_SAV = 0 UND LV_ERR_SAP = 0 UND LV_ERR_LOAD_TPS_PLAUS = 0 UND (STATE_DIAG_SA_SAFM = SAFM_DIAG_END ODER SAFM_DIAG_CNL)
- [STEUERN_MIL](#job-steuern-mil) - 0x2F60D403 STEUERN_MIL MIL (Malfunction Indicator Lamp) ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [STEUERN_LSH1](#job-steuern-lsh1) - 0x2F60D003 STEUERN_LSH1 Lambdasondenheizung vor Kat Bank1 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [ECU_CONFIG](#job-ecu-config) - 0x225FF2 ECU_CONFIG Variante auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_MSVHDP5](#job-steuern-ende-msvhdp5) - 0x2F60EF00 STEUERN_ENDE_MSVHDP5 Mengensteuerventil HDP5 Ansteuerung beenden NO_CON
- [STEUERN_DISCODBSR](#job-steuern-discodbsr) - 0x2E5F7E STEUERN_DISCODBSR Verriegelung des betriebsstundenrelevanten Kodierbereichs.
- [STEUERN_LSH2](#job-steuern-lsh2) - 0x2F60D103 STEUERN_LSH2 Lambdasondenheizung hinter Kat Bank1 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_PROGRAMM_IMA_ZYL_12](#job-steuern-programm-ima-zyl-12) - 0x2E5F98 STEUERN_PROGRAMM_IMA_ZYL_12 Abgleichwert Injektor 12 programmieren NO_CON
- [STEUERN_PROGRAMM_IMA_ZYL_10](#job-steuern-programm-ima-zyl-10) - 0x2E5F9C STEUERN_PROGRAMM_IMA_ZYL_10 Abgleichwert Injektor 10 programmieren NO_CON
- [STEUERN_PROGRAMM_IMA_ZYL_11](#job-steuern-programm-ima-zyl-11) - 0x2E5F94 STEUERN_PROGRAMM_IMA_ZYL_11 Abgleichwert Injektor 11 programmieren NO_CON
- [STEUERN_PROGRAMM_IMA_ZYL_5](#job-steuern-programm-ima-zyl-5) - 0x2E5F93 STEUERN_PROGRAMM_IMA_ZYL_5 Abgleichwert Injektor 05 programmieren NO_CON
- [STEUERN_PROGRAMM_IMA_ZYL_6](#job-steuern-programm-ima-zyl-6) - 0x2E5F97 STEUERN_PROGRAMM_IMA_ZYL_6 Abgleichwert Injektor 06 programmieren NO_CON
- [STEUERN_PROGRAMM_IMA_ZYL_3](#job-steuern-programm-ima-zyl-3) - 0x2E5F95 STEUERN_PROGRAMM_IMA_ZYL_3 Abgleichwert Injektor 03 programmieren NO_CON
- [STEUERN_PROGRAMM_IMA_ZYL_4](#job-steuern-programm-ima-zyl-4) - 0x2E5F9B STEUERN_PROGRAMM_IMA_ZYL_4 Abgleichwert Injektor 04 programmieren NO_CON
- [STEUERN_PROGRAMM_IMA_ZYL_9](#job-steuern-programm-ima-zyl-9) - 0x2E5F96 STEUERN_PROGRAMM_IMA_ZYL_9 Abgleichwert Injektor 09 programmieren NO_CON
- [STEUERN_PROGRAMM_IMA_ZYL_7](#job-steuern-programm-ima-zyl-7) - 0x2E5F92 STEUERN_PROGRAMM_IMA_ZYL_7 Abgleichwert Injektor 07 programmieren NO_CON
- [STEUERN_PROGRAMM_IMA_ZYL_8](#job-steuern-programm-ima-zyl-8) - 0x2E5F9A STEUERN_PROGRAMM_IMA_ZYL_8 Abgleichwert Injektor 08 programmieren NO_CON
- [STATUS_NOCKENWELLE_ADAPTION](#job-status-nockenwelle-adaption) - 0x224006 STATUS_NOCKENWELLE_ADAPTION Nockenwellenadationswerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_PROGRAMM_IMA_ZYL_1](#job-steuern-programm-ima-zyl-1) - 0x2E5F91 STEUERN_PROGRAMM_IMA_ZYL_1 Abgleichwert Injektor 01 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_PROGRAMM_IMA_ZYL_2](#job-steuern-programm-ima-zyl-2) - 0x2E5F99 STEUERN_PROGRAMM_IMA_ZYL_2 Abgleichwert Injektor 02 programmieren NO_CON
- [START_SYSTEMCHECK_L_REGELUNG_AUS](#job-start-systemcheck-l-regelung-aus) - 0x3101F0D9 START_SYSTEMCHECK_L_REGELUNG_AUS Ansteuerung Lambdaregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_VANOSSPUELEN](#job-stop-vanosspuelen) - 0x3102F042 STOP_VANOSSPUELEN VANOS Spuelen fuer OBD und PVE. Steuern-Ende
- [STOP_OPF_DRUCKSCHLAUCHABFALL](#job-stop-opf-druckschlauchabfall) - 0x3102F09F STOP_OPF_DRUCKSCHLAUCHABFALL Diagnosefunktion OPF Druckschlauchabfall  beenden  (Bei Master Slave Projekten Kopplung notwendig.)
- [STEUERN_VERBRAUCHERSTROM_EFII](#job-steuern-verbraucherstrom-efii) - Ansteuerung Verbraucherstrommessung EFII (IBS) UDS  : $31   RoutineControl UDS  : $01   routineControlType UDS  : $7002 routineIdentifier
- [IDENT_GEN](#job-ident-gen) - 0x2C01F3 IDENT_GEN Identifikationsdaten Generator Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_LLERH](#job-stop-systemcheck-llerh) - 0x3102F026 STOP_SYSTEMCHECK_LLERH Diagnosefunktion Leerlauf-Erhoehung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_ZGH](#job-status-zgh) - 0x3103F034 STATUS_ZGH Auslesen Zylinder Gleichstellung Homogen
- [STEUERN_KRANN](#job-steuern-krann) - 0x3101F0E3 STEUERN_KRANN Ansteuern Krann-Adaptionswerte (Anforderung aus CP5404)
- [START_SYSTEMCHECK_GEN](#job-start-systemcheck-gen) - 0x3101F02A START_SYSTEMCHECK_GEN Diagnosefunktion Generatortest 
- [STATUS_MSAINFO_AEP](#job-status-msainfo-aep) - 0x224018 _STATUS_MSAINFO_AEP Infospeicher Motor-Start/Stop Automatik (MSA) auslesen
- [STEUERN_ENDE_DMTL_P](#job-steuern-ende-dmtl-p) - 0x2F60CC00 STEUERN_ENDE_DMTL_P Diagnosemodul-Tank Leckage Pumpe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [ECU_CONFIG_RESET](#job-ecu-config-reset) - 0x2E5FF204 ECU_CONFIG_RESET Variante loeschen Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_ENDE_DMTL_V](#job-steuern-ende-dmtl-v) - 0x2F60CD00 STEUERN_ENDE_DMTL_V Diagnosemodul-Tank Leckage Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_UVLSS](#job-steuern-uvlss) - 0x2F602003 STEUERN_UVLSS Versorgung Einspritzung / Zuendung ansteuern Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_ENDE_VERBRAUCHERSTROM_EFII](#job-steuern-ende-verbraucherstrom-efii) - Ansteuerung Verbraucherstrommessung EFII (IBS) beenden UDS  : $31   RoutineControl UDS  : $02   routineControlType UDS  : $7002 routineIdentifier
- [STEUERN_ENWS](#job-steuern-enws) - 0x2F60ED03 STEUERN_ENWS Vanos Einlass Ventil ansteuern Aktivierung: Drehzahl &gt; 1000 1/min Activation: N &gt; C_N_MIN_KWP
- [STATUS_SYSTEMCHECK_GEN](#job-status-systemcheck-gen) - 0x3103F02A STATUS_SYSTEMCHECK_GEN Auslesen Diagnosefunktion Generatortest Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_E_LUEFTER](#job-steuern-ende-e-luefter) - 0x2F60DA00 STEUERN_ENDE_E_LUEFTER E-Luefter Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_ANWS](#job-steuern-ende-anws) - 0x2F60EE00 STEUERN_ENDE_ANWS Vanos Auslass Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_MSV](#job-steuern-msv) - 0x2F60BD03 STEUERN_MSV Mengensteuerventil ansteuern Aktivierung: 50000 hPa &lt; Raildruck &lt; 200000 hPa UND Leerlauf Activation: C_FUP_MIN_KWP &lt; FUP &lt; C_FUP_MAX_KWP UND LV_IS = 1
- [STATUS_DISCODBSR](#job-status-discodbsr) - 0x225F7E STATUS_DISCODBSR Verriegelung des betriebsstundenrelevanten Kodierbereichs (Auslesen vom Bit: DIS_COD_BSR)
- [START_SYSTEMCHECK_PM_MESSEMODE](#job-start-systemcheck-pm-messemode) - 0x3101F0F6 START_SYSTEMCHECK_PM_MESSEMODE Ansteuern Messemode Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_OBD_DEMO_MOMENTENBEGRENZUNG](#job-stop-obd-demo-momentenbegrenzung) - 0x3102F09E STOP_OBD_DEMO_MOMENTENBEGRENZUNG OBD Demo Momentenbegrenzung
- [STATUS_GVOBD](#job-status-gvobd) - 0x225F80 STATUS_GVOBD Gemischvertrimmung fuer OBD-Demo und PVE lesen. Bank 1
- [STEUERN_ENDE_HDPR](#job-steuern-ende-hdpr) - 0x2F608200 STEUERN_ENDE_HDPR Hochdruckpumpenrelais Ansteuerung beenden NO_CON
- [STATUS_KLANN](#job-status-klann) - 0x3103F0E4 STATUS_KLANN Auslesen Krann-Adaptionswerte Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_ADAPTION_OPF](#job-status-adaption-opf) - 0x22419B STATUS_ADAPTION_OPF Nutzung  des OPF lesen
- [STEUERN_ENDE_MIL](#job-steuern-ende-mil) - 0x2F60D400 STEUERN_ENDE_MIL MIL (Malfunction Indicator Lamp) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_EWAP](#job-steuern-ende-ewap) - 0x2F60BF00 STEUERN_ENDE_EWAP elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden NO_CON
- [STEUERN_LDS1](#job-steuern-lds1) - 0x2F60B603 STEUERN_LDS1 Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1
- [STATUS_SYSTEMCHECK_AEP_INFO_1](#job-status-systemcheck-aep-info-1) - 0x224022 STATUS_SYSTEMCHECK_AEP_INFO_1 Intelligenter Batteriesensor Bitfeld Pminfo1 lesen
- [STATUS_SYSTEMCHECK_AEP_INFO_2](#job-status-systemcheck-aep-info-2) - 0x224023 STATUS_SYSTEMCHECK_AEP_INFO_2 Intelligenter Batteriesensor Bitfeld Pminfo2 lesen
- [STATUS_SYSTEMCHECK_OPF](#job-status-systemcheck-opf) - 0x3103F07B STATUS_SYSTEMCHECK_OPF OPF Systemtest
- [START_SYSTEMCHECK_TEV](#job-start-systemcheck-tev) - 0x3101F022 START_SYSTEMCHECK_TEV Ansteuern Diagnosefunktion Tankentlueftungsventil Aktivierung: Klemme 15 = EIN UND Phase Motorstart beendet = EIN UND Funktionscheck TEV = EIN UND Geschwindigkeit = 0 km/h UND LV_MAF_SP_TQI_DYW_DIAGCPS = 1 UND (Betriebsart TEV = 1 ODER Betriebsart TEV = 2) UND Fehlerspeichereintrag TEV = AUS Activation: LV_IGK = 1 UND LV_ST_END = 1 UND LV_INH_DIAGCPS = 0 UND VS = 0 UND LV_MAF_SP_TQI_DYW_DIAGCPS = 1 UND (OPM_AV_DIAGCPS = 1 ODER OPM_AV_DIAGCPS = 2) UND LV_ERR_DIAGCPS = 0

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

<a id="job-ident"></a>
### IDENT

Identdaten UDS  : $22   ReadDataByIdentifier UDS  : $F150 Sub-Parameter SGBD-Index Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_SG_ADR | long | Steuergeraeteadresse |
| ID_SGBD_INDEX | long | Index zur Erkennung der SG-Variante |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $02 ReadDTCByStatusMask UDS  : $0C StatusMask (Bit2, Bit3) Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLER_KLASSE | string | 'IGNORIERE_EREIGNIS_DTC': Wenn EREIGNIS_DTC = '1', DTC-Fehlereinträge werden ignoriert sonst: FEHLERKLASSE wird ausgewertet |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers Fuer UDS immer 3 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC -1: wird nicht unterstuetzt table FOrtTexte EREIGNIS_DTC |
| F_FEHLERKLASSE | unsigned long | table FOrtTexte FEHLERKLASSE |
| F_STATUSBYTE | int | Wert des DTC-Statusbyte laut ISO 14229 (bitcodiert) Bedeutung der einzelnen Bits: Bit 7: warningIndicatorRequested Bit 6: testNotCompletedThisOperationCycle Bit 5: testFailedSinceLastClear Bit 4: testNotCompletedSinceLastClear Bit 3: ConfirmedDTC Bit 2: PendingDTC Bit 1: testFailedThisOperationCycle Bit 0: testFailed |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-detail"></a>
### FS_LESEN_DETAIL

Fehlerspeicher lesen (einzelner Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $04 reportDTCSnapshotRecordByDTCNumber UDS  : $06 reportDTCExtendedDataRecordByDTCNumber UDS  : $09 reportSeverityInformationOfDTC Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | long | gewaehlter Fehlercode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers Fuer UDS immer 3 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC table FOrtTexte EREIGNIS_DTC |
| F_STATUSBYTE | int | Wert des DTC-Statusbyte laut ISO 14229 (bitcodiert) Bedeutung der einzelnen Bits: Bit 7: warningIndicatorRequested Bit 6: testNotCompletedThisOperationCycle Bit 5: testFailedSinceLastClear Bit 4: testNotCompletedSinceLastClear Bit 3: ConfirmedDTC Bit 2: PendingDTC Bit 1: testFailedThisOperationCycle Bit 0: testFailed |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_HFK | int | Haeufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Heilungsszaehler |
| F_UEBERLAUF | int | 0: Kein Ueberlauf des Fehlerspeichers 1: Ueberlauf des Fehlerspeichers |
| F_FEHLERKLASSE_NR | int | 0: Keine Fehlerklasse verfuegbar 1: Ueberpruefung bei naechstem Werkstattbesuch 2: Ueberpruefung bei naechstem Halt 4: Ueberpruefung sofort erforderlich ! |
| F_FEHLERKLASSE_TEXT | string | Ausgabe der Fehlerklasse als Text table Fehlerklasse TEXT |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| F_UW_KM | long | Umweltbedingung Kilometerstand (3 Byte) Wertebereich: 0 - 16777215 km -1, wenn Kilometerstand nicht zur Verfuegung steht |
| F_UW_ZEIT | long | Umweltbedingung Absolute Zeit (4 Byte) Genauigkeit: in Sekunden -1, wenn Absolute Zeit nicht zur Verfuegung steht |
| F_UW_BN | int | Umweltbedingung Basisnetz (1 Byte) -1, wenn Daten bzgl. Basisnetz nicht zur Verfuegung stehen |
| F_UW_TN | long | Umweltbedingung Teilnetz (3 Byte) -1, wenn Daten bzgl. funktionalem Teilnetz nicht zur Verfuegung stehen |
| F_SAE_CODE | unsigned int | Wertebereich 0x000000 - 0xFFFFFF externe Tabelle T_SCOD |
| F_SAE_CODE_STRING | string | 5 stelliger Text in der Form 'Sxxxx' |
| F_SAE_CODE_TEXT | string | Text zu F_SAE_CODE |
| _RESPONSE_SNAPSHOT | binary | Hex-Antwort von SG |
| _RESPONSE_EXTENDED_DATA | binary | Hex-Antwort von SG |
| _RESPONSE_SEVERITY | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen UDS  : $14 ClearDiagnosticInformation UDS  : $FF DTCHighByte UDS  : $FF DTCMiddleByte UDS  : $FF DTCLowByte Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | long | 0x??????: Angabe eines einzelnen Fehlers Default: 0xFFFFFF: alle Fehler |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels UDS  : $22   ReadDataByIdentifier UDS  : $1000 TestStamp Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| BYTE1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. UDS  : $2E   WriteDataByIdentifier UDS  : $1000 TestStamp Modus: Default

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
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-svk-lesen"></a>
### SVK_LESEN

Informationen zur Steuergeraete-Verbau-Kennung UDS  : $22   ReadDataByIdentifier UDS  : $F1xx Sub-Parameter fuer SVK UDS  : $F101 SVK_AKTUELL (Default) Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SVK | string | table SVK_ID BEZEICHNUNG WERT default SVK_AKTUELL |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PROG_TEST | int | Programmierabhaengigkeiten (ProgrammingDependenciesChecked) 1: IO : Signaturpruefung und ProgrammingDependenciesCheck erfolgreich 2: NIO: mindestens eine SWE fehlerhaft oder ProgrammingDependenciesCheck nicht durchgefuehrt 3: NIO: mindestens eine SWE passt nicht mit einer HWE zusammen 4: NIO: mindestens eine SWE passt nicht mit einer anderen SWE zusammen sonst: reserviert |
| ANZAHL_EINHEITEN | int | Anzahl der xWEn |
| PROG_DATUM | string | Programmierdatum (DD.MM.YY) |
| PROG_KM | long | KM-Stand bei Programmierung (10 KM bis 655350 KM) Inkrement sind 10 KM -1: KM-Stand wird nicht unterstuetzt |
| PROZESSKLASSE_WERT | int | table Prozessklassen WERT dezimale Angabe der Prozessklasse |
| PROZESSKLASSE_TEXT | string | table Prozessklassen BEZEICHNUNG Text-Angabe der Prozessklasse |
| PROZESSKLASSE_KURZTEXT | string | table Prozessklassen PROZESSKLASSE Text-Angabe des Prozessklassenkurztextes |
| SGBM_IDENTIFIER | string | Angabe SGBM-ID der Prozessklasse |
| VERSION | string | Angabe der Version der Prozessklasse |
| SGBM_ID | string | Angabe von Prozessklasse, SGBM-Identifier, Version |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Lesen eines oder mehrerer Stati UDS  : $22 ReadDataByIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_SPALTE | string | 'ARG', 'ID', 'LABEL' |
| STATUS | string | Es muss mindestens ein Argument übergeben werden Es wird das zugehörige result erzeugt table SG_Funktionen ARG ID RESULTNAME RES_TABELLE ARG_TABELLE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Antwort von SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern"></a>
### STEUERN

Vorgeben eines Status UDS  : $2E WriteDataByIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_SPALTE | string | 'ARG', 'ID', 'LABEL' |
| STATUS | string | Siehe table SG_Funktionen ARG ID LABEL ARG_TABELLE |
| WERT | string | Es muss mindestens ein Argument übergeben werden Argumente siehe table SG_Funktionen ARG ID ARG_TABELLE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Antwort von SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-seriennummer-lesen"></a>
### SERIENNUMMER_LESEN

Seriennummer des Steuergeraets UDS  : $22   ReadDataByIdentifier UDS  : $F18C Sub-Parameter ECUSerialNumber Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SERIENNUMMER | string | Seriennummer des Steuergeraets |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-routine"></a>
### STEUERN_ROUTINE

Vorgeben eines Status UDS  : $31 RoutineControl

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_SPALTE | string | 'ARG', 'ID', 'LABEL' |
| STATUS | string | Siehe table SG_Funktionen ARG ID RES_TABELLE ARG_TABELLE |
| STEUERPARAMETER | string | 'STR'  = startRoutine 'STPR' = stopRoutine 'RRR'  = requestRoutineResults |
| WERT | string | Argumente siehe table SG_Funktionen ARG_TABELLE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Antwort von SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-is-lesen"></a>
### IS_LESEN

Sekundaerer Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $22   ReadDataByIdentifierRequestServiceID UDS  : $2000 DataIdentifier sekundaerer Fehlerspeicher Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers Fuer UDS immer 3 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC table FOrtTexte EREIGNIS_DTC |
| F_STATUSBYTE | int | Wert des DTC-Statusbyte laut ISO 14229 (bitcodiert) Bedeutung der einzelnen Bits: Bit 7: warningIndicatorRequested Bit 6: testNotCompletedThisOperationCycle Bit 5: testFailedSinceLastClear Bit 4: testNotCompletedSinceLastClear Bit 3: ConfirmedDTC Bit 2: PendingDTC Bit 1: testFailedThisOperationCycle Bit 0: testFailed |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-is-lesen-detail"></a>
### IS_LESEN_DETAIL

sekundären Fehlerspeicher lesen (Info-Meldungen / Ort und Art) UDS  : $22 ReadDataByIdentifier UDS  : $20 dataIdentifier UDS  : $00 alle Info-Meldungen anschließend UDS  : $20 dataIdentifier UDS  : $nn Details zur Info-Meldung an der Position n Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | long | gewaehlter Infocode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt. Es darf dann nicht argument F_POS angegeben werden |
| F_POS | int | gewaehlter Eintrag Wenn dieser Parameter angegeben wird, wird die Position benutzt. Wertebereich 1 - 255 Es darf dann nicht argument F_CODE angegeben werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers Fuer UDS immer 3 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC table FOrtTexte EREIGNIS_DTC |
| F_STATUSBYTE | int | Wert des DTC-Statusbyte laut ISO 14229 (bitcodiert) Bedeutung der einzelnen Bits: Bit 7: warningIndicatorRequested Bit 6: testNotCompletedThisOperationCycle Bit 5: testFailedSinceLastClear Bit 4: testNotCompletedSinceLastClear Bit 3: ConfirmedDTC Bit 2: PendingDTC Bit 1: testFailedThisOperationCycle Bit 0: testFailed |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_HFK | int | Haeufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Heilungsszaehler |
| F_UEBERLAUF | int | 0: Kein Ueberlauf des Fehlerspeichers 1: Ueberlauf des Fehlerspeichers |
| F_FEHLERKLASSE_NR | int | 0: Keine Fehlerklasse verfuegbar 1: Ueberpruefung bei naechstem Werkstattbesuch 2: Ueberpruefung bei naechstem Halt 4: Ueberpruefung sofort erforderlich ! |
| F_FEHLERKLASSE_TEXT | string | Ausgabe der Fehlerklasse als Text table Fehlerklasse TEXT |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| F_UW_KM | long | Umweltbedingung Kilometerstand (3 Byte) Wertebereich: 0 - 16777215 km -1, wenn Kilometerstand nicht zur Verfuegung steht |
| F_UW_ZEIT | long | Umweltbedingung Absolute Zeit (4 Byte) Genauigkeit: in Sekunden -1, wenn Absolute Zeit nicht zur Verfuegung steht |
| F_UW_BN | int | Umweltbedingung Basisnetz (1 Byte) -1, wenn Daten bzgl. Basisnetz nicht zur Verfuegung stehen |
| F_UW_TN | long | Umweltbedingung Teilnetz (3 Byte) -1, wenn Daten bzgl. funktionalem Teilnetz nicht zur Verfuegung stehen |
| F_SAE_CODE | unsigned int | Wertebereich 0x000000 - 0xFFFFFF externe Tabelle T_SCOD |
| F_SAE_CODE_STRING | string | 5 stelliger Text in der Form 'Sxxxx' |
| F_SAE_CODE_TEXT | string | Text zu F_SAE_CODE |
| _RESPONSE_2000 | binary | Hex-Antwort von SG |
| _RESPONSE_200X | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-herstellinfo-lesen"></a>
### HERSTELLINFO_LESEN

Lieferant und Herstelldatum lesen UDS  : $22   ReadDataByIdentifier UDS  : $F18A SystemSupplierIdentifier UDS  : $F18B ECUManufactoringData Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_LIEF_NR | long | Lieferantennummer 0xFFFFFF, falls nicht vorhanden |
| ID_LIEF_TEXT | string | Text zu ID_LIEF_NR table Lieferanten LIEF_TEXT unbekannter Hersteller, falls nicht vorhanden |
| ID_DATUM | string | Herstelldatum (DD.MM.YY) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

Diagnosemode des SG aufrecht erhalten UDS  : $3E TesterPresent UDS  : $?0 suppressPosRspMsgIndication Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ANTWORT | string | "ja"   -&gt; SG soll antworten "nein" -&gt; SG soll nicht antworten table DigitalArgument TEXT Default:  SG soll antworten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-diagnose-mode"></a>
### DIAGNOSE_MODE

SG in bestimmten Diagnosemode bringen UDS  : $10 StartDiagnosticSession Modus: einstellbar mit diesem Job

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-sleep-mode"></a>
### SLEEP_MODE

SG in Sleep-Mode versetzen UDS  : $11 ECUReset UDS  : $04 EnableRapidPowerShutDown Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-energiesparmode"></a>
### ENERGIESPARMODE

Einstellen des Energiesparmodes UDS   : $31   RoutineControlRequestServiceID UDS   : $01   startRoutine UDS   : $0F0C DataIdentifier ControlEnergySavingMode UDS   : $??   Mode Modus : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int | 0x00: Normalmode 0x01: Fertigungsmode 0x02: Transportmode 0x03: Flashmode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-energiesparmode"></a>
### STATUS_ENERGIESPARMODE

Energy-Saving-Mode auslesen UDS  : $22   ReadDataByIdentifier UDS  : $100A DataIdentifier EnergySavingMode Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENERGIESPARMODE_WERT | int | Ausgabe des Energiesparmodes 0: Kein Energiesparmode gesetzt 1: Produktionsmode gesetzt 2: Transportmode gesetzt 3: Flashmode gesetzt -1: Mode ungueltig |
| STAT_ENERGIESPARMODE_TEXT | string | Text zu STAT_ENERGIESPARMODE_WERT |
| STAT_PRODUKTIONSMODE_EIN | int | 0: Produktionsmode nicht aktiv 1: Produktionsmode aktiv |
| STAT_TRANSPORTMODE_EIN | int | 0: Transportmode nicht aktiv 1: Transportmode aktiv |
| STAT_FLASHMODE_EIN | int | 0: Flashmode nicht aktiv 1: Flashmode aktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-betriebsmode"></a>
### STATUS_BETRIEBSMODE

Aktueller Betriebsmode SG muss sich im Energiersparmode befinden UDS  : $22   ReadDataByIdentifier UDS  : $100E Sub-Parameter Betriebsmode Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BETRIEBSMODE_WERT | int | Aktueller Betriebsmode table Betriebsmode WERT 0     : Kein Betriebsmode gesetzt 1 - 16: Erweiterter Betriebsmode (Bedeutung siehe Tabelle) |
| STAT_BETRIEBSMODE_TEXT | string | Textausgabe STAT_BETRIEBSMODE_WERT table Betriebsmode TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-betriebsmode"></a>
### STEUERN_BETRIEBSMODE

Betriebsmode setzen SG muss sich im Energiersparmode befinden UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $1003 DataIdentifier Betriebsmode UDS  : $0?   Betriebsmode Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BETRIEBSMODE | int | Betriebsmode setzen table Betriebsmode WERT 0     : Kein Betriebsmode gesetzt 1 - 16: Erweiterter Betriebsmode (Bedeutung siehe Tabelle) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-sensoren-anzahl-lesen"></a>
### SENSOREN_ANZAHL_LESEN

Anzahl der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_ANZAHL | long | Anzahl der intelligenten Subbussensoren |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-sensoren-ident-lesen"></a>
### SENSOREN_IDENT_LESEN

Identifikation der intelligenten Subbussensoren lesen UDS  : $22   ReadDataByIdentifier UDS  : $1600 Identifier NumberofSubbusMembers UDS  : $16xx SubbusMemberSerialNumber Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SENSOR_NR | long | optionales Argument gewuenschter Sensor xx (0x01 - 0xFF) oder VERBAUORT eines bestimmten Sensors (table VerbauortTabelle ORT) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SENSOR_VERBAUORT | string | Verbauort des Sensors table VerbauortTabelle ORTTEXT |
| SENSOR_VERBAUORT_NR | long | Verbauort-Nummer des Sensors |
| SENSOR_BMW_NR | string | BMW-Teilenummer des Sensors |
| SENSOR_PART_NR | string | Teilenummer des Sensors optional wenn SENSOR_BMW_NR gueltig wenn Teilenummer vom Sensor nicht verfuegbar dann '--' |
| SENSOR_LIN_2_0_FORMAT | int | 1: Die optionalen Daten des Sensors (Hersteller, Seriennummer, ...) werden in LIN_2_Format geliefert 0: Optionale Daten nicht im LIN_2_Format (nur Defaultwerte werden ausgegeben) |
| SENSOR_HERSTELLER_NR | long | Lieferantennummer des Herstellers wenn Hersteller-Nummer nicht verfuegbar, dann 0 |
| SENSOR_HERSTELLER_TEXT | string | Textausgabe Lieferant wenn Softwarestand nicht verfuegbar, dann '--' |
| SENSOR_FUNKTIONS_NR | long | Funktionsnummer des Sensors wenn Funktions-Nummer nicht verfuegbar, dann 0 |
| SENSOR_VARIANTEN_NR | long | Variantennummer des Sensors wenn Varianten-Nummer nicht verfuegbar, dann 0 |
| SENSOR_PROD_DATUM | string | Produnktionsdatum (DD.MM.YY) des Sensors wenn Produktions-Datum nicht verfuegbar, dann '--' |
| SENSOR_SERIEN_NR | string | Seriennummer des Sensors wenn Serien-Nummer nicht verfuegbar, dann '--' |
| SENSOR_SW_RELEASE_NR | string | Softwarestand des Sensors wenn Softwarestand nicht verfuegbar, dann '--' |
| SENSOR_HW_RELEASE_NR | string | Hardwarestand des Sensors wenn Softwarestand nicht verfuegbar, dann '--' |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

<a id="job-steuergeraete-reset"></a>
### STEUERGERAETE_RESET

Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

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

CBS Daten auslesen (fuer CBS-Version 5) UDS: $22 ReadDataByIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Zahl |
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
| COUNT_CBS_WERT_OEL | int | Servicezaehler Motoroel, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BR_V | int | Verfuegbarkeit BR_V in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_BR_V | int | Servicezaehler Bremsbelag vorne, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BR_H | int | Verfuegbarkeit BR_H in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_BR_H | int | Servicezaehler Bremsbelag hinten, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_BRFL | int | Verfuegbarkeit BRFL in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_BRFL | int | Servicezaehler Bremsfluessigkeit, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_SIC | int | Verfuegbarkeit SIC in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_SIC | int | Servicezaehler Sichtpruefung, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_SIC_V | int | Verfuegbarkeit SIC_V in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_SIC_V | int | Servicezaehler Sichtpruefung/Fahrzeug-Check verknuepft, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_UEB | int | Verfuegbarkeit UEB in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_UEB | int | Servicezaehler Uebergabedurchsicht, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_NOX | int | Verfuegbarkeit NOX in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_NOX | int | Servicezaehler NOx-Additiv  , fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_EFK | int | Verfuegbarkeit Efk in %, fuer Pruefablauf Bandende |
| COUNT_CBS_WERT_EFK | int | Servicezaehler Einfahrkontrolle, fuer Pruefablauf Bandende |
| ZIEL_MM_WERT | int | Ziel-Monat |
| ZIEL_MM_EINH | string | Monat |
| ZIEL_YY_WERT | int | Ziel-Jahr |
| ZIEL_YY_EINH | string | Jahr |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall |
| FRC_INTM_WAY_CBS_EINH | string | Information zur Prognose Wegintervall |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall |
| STATUS_MESSUNG | int | Statusbyte |
| STATUS_MESSUNG_TEXT | string | Statusbyte im Klartext |
| RES_BYTE | int | Reserve Byte (noch unbenutzt) |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-cbs-reset"></a>
### CBS_RESET

CBS Daten Zuruecksetzen (fuer CBS-Version 5) UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit 'Strich_Punkt' getrennt (nicht mit Komma!)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CBS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, Sic, Sic_v, TUV, AU, Ueb, Efk Werte externe Umfaenge: Oel, NOx_a, Br_v, Br_h Defaultwert: 0x00 (ungueltig) |
| CBS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, keine Aenderung: 0xFFh (255 dez) Defaultwert: 100 (0x64h) Bremsflüssigkeit: 150 (0x96h) erlaubt |
| CBS_ANZAHL_SERVICE | int | Anzahl der durchgefuehrten Services: 0-30 Schalter, Erhoehung der Anzahl um +1: 31 Defaultwert: 31 |
| CBS_ZIEL_MONAT | int | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter, keine Aenderung: 0x0F (15 dez) Defaultwert: 0x0Fh (15 dez) |
| CBS_ZIEL_JAHR | int | Ziel-Jahr (HU/AU) 2000-2239: 0-239 Schalter, keine Aenderung: 0x3F (63 dez) Defaultwert: 0x3Fh (63 dez) |
| RMM_CBS_WERT | int | Restlaufleistung in km oder % (siehe Argument Einheit) Schalter, keine Aenderung: 8000h Defaultwert: 8000h |
| ST_UN_CBS_RSTG | int | Einheit Restlaufleistung 0hex -&gt; % 1hex -&gt; km*10 Fhex -&gt; d.c. Defaultwert: Fh |
| FRC_INTM_WAY_CBS_MESS | int | Prognose Wegintervall Umrechnung 1-254*1000km Schalter, setzt auf Defaultwert zurueck: 0h Schalter, keine Aenderung: FFh Defaultwert: FFh |
| FRC_INTM_T_CBS_MESS | int | Prognose Zeitintervall 0-254 Monate Schalter, keine Aenderung: FFh Defaultwert: FFh |
| RES_BYTE | int | Reserve Byte (noch unbenutzt) Defaultwert: 00h |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR_WERT | int | Steuergeraeteadresse als Zahl |
| ECU_ADR_HEX | string | Steuergeraeteadresse als Hex-String |
| ECU_ADR_TEXT | string | Steuergeraeteadresse im Klartext |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-stop"></a>
### STEUERN_ROE_STOP

Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-roe-report"></a>
### STATUS_ROE_REPORT

Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events [$02 eventWindowTime - infinite (nur 35up)] 35up: LH Diagnosemaster V11 oder höher pre35up: LH Diagnosemaster V6 - V9

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ROE_AKTIV | char | 0x00  = Aktive Fehlermeldung deaktiviert 0x01  = Aktive Fehlermeldung aktiviert 0xFF  = Status der aktiven Fehlermeldung nicht feststellbar |
| STAT_ROE_AKTIV_TEXT | string | Interpretation von STAT_ROE_AKTIV table UDS_TAB_ROE_AKTIV TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-start"></a>
### STEUERN_ROE_START

Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-persistent-stop"></a>
### STEUERN_ROE_PERSISTENT_STOP

Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-persistent-start"></a>
### STEUERN_ROE_PERSISTENT_START

Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-cps-lesen"></a>
### CPS_LESEN

Codierpruefstempel lesen UDS  : $22   ReadDataByIdentifier UDS  : $37FE DataIdentifier Codierpruefstempel Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CPS | string | Codierpruefstempel bis SP2021 bestehend aus VIN7        7 Zeichen (ASCII) Codierpruefstempel ab SP2021 bestehend aus Codierdatum 6 Zeichen (3 Byte Hex) bestehend aus TesterNr    6 Zeichen (3 Byte Hex) bestehend aus LizenzID   10 Zeichen (5 Byte Hex) bestehend aus VIN7        7 Zeichen (ASCII) |
| CPS_VIN7 | string | 7 Zeichen (ASCII) |
| CPS_DATUM | string | erst ab SP2021 Codierdatum 8 Zeichen TT.MM.JJJJ |
| CPS_TESTERNR | string | erst ab SP2021 Tester-Nummer 6 Zeichen hex |
| CPS_LIZENZID | string | erst ab SP2021 Tester-Lizenz-ID 10 Zeichen hex |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-diag-session-lesen"></a>
### DIAG_SESSION_LESEN

Aktive Diagnose-Session auslesen UDS  : $22   ReadDataByIdentifier UDS  : $F186 ActiveDiagnosticSession Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DIAG_SESSION_WERT | int | Diagnose-Session (1 Byte) |
| DIAG_SESSION_TEXT | string | Diagnose-Session als Text |
| DIAG_DETAIL_WERT | int | Details zur Diagnose-Session (1 Byte) |
| DIAG_DETAIL_TEXT | string | Details zur Diagnose-Session als Text |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-flash-tp-lesen"></a>
### FLASH_TP_LESEN

Flash Timing Parameter auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2504 FlashTimingParameter Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHEN | int | EraseMemoryTime (2 Byte) |
| FLASH_TEST | int | CheckMemoryTime (2 Byte) |
| FLASH_BOOT | int | BootloaderInstallationTime (2 Byte) |
| FLASH_AUTHENT | int | AuthenticationTime (2 Byte) |
| FLASH_RESET | int | ResetTime (2 Byte) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-prog-zaehler-lesen"></a>
### PROG_ZAEHLER_LESEN

Programmierzaehler lesen UDS  : $22   ReadDataByIdentifier UDS  : $2502 ProgrammingCounter Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PROG_ZAEHLER_STATUS_WERT | int | Status, wie oft das SG programmierbar ist |
| PROG_ZAEHLER_STATUS_TEXT | string | Status, wie oft das SG programmierbar ist |
| PROG_ZAEHLER | int | Programmierzaehler |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-prog-max-lesen"></a>
### PROG_MAX_LESEN

Anzahl der maximal möglichen Programmiervorgänge auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2503 ProgrammingCounter Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PROG_MAX | long | maximal mögliche Programmiervorgänge Sonderfall 0xFFFF: Anzahl der Programmiervorgänge unbegrenzt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-eisydr"></a>
### STATUS_EISYDR

0x3103F0E2 STATUS_EISYDR Auslesen Eisy-Adaptionswerte mit Druckregelung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_EISYDR_TEXT | string | Funktionsstatus Eisy-Adaptionswerte mit Druckregelung B_MAREGDK_AD   Min: 0 Max: 1 |
| STAT_FS_EISYDR_WERT | int | Funktionsstatus Eisy-Adaptionswerte mit Druckregelung B_MAREGDK_AD   Min: 0 Max: 1 |
| STAT_PRNN_TEST_WERT | real | Massenstromregler-Adaptionswert NN im AGR - Betrieb ueber Test gelesen MRNN_TEST_PR   Min: -2 Max: 1.9999 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-readiness"></a>
### STATUS_READINESS

0x224105 STATUS_READINESS Monitorfunktionen und Readinessflags aus DME auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_COMPREHENSIVE_TEXT | string | Ueberwachung der uebrigen Komponenten  Test abgeschlossen oder nicht anwendbar = 0  test nicht abgeschlossen = 1 STATE_READY_OBD_1[6] |
| STAT_COMPREHENSIVE_WERT | int | Ueberwachung der uebrigen Komponenten  Test abgeschlossen oder nicht anwendbar = 0  test nicht abgeschlossen = 1 STATE_READY_OBD_1[6] |
| STAT_FUELSYSTEM_TEXT | string | Ueberwachung Kraftstoffsystem  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_1[5] |
| STAT_FUELSYSTEM_WERT | int | Ueberwachung Kraftstoffsystem  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_1[5] |
| STAT_MISSFIRE_TEXT | string | Ueberwachung Verbrennungsaussetzer  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_1[4] |
| STAT_MISSFIRE_WERT | int | Ueberwachung Verbrennungsaussetzer  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_1[4] |
| STAT_COMPREHENSIVE_MONITOR_TEXT | string | Ueberwachung der uebrigen Komponenten  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 STATE_READY_OBD_1[2] |
| STAT_COMPREHENSIVE_MONITOR_WERT | int | Ueberwachung der uebrigen Komponenten  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 STATE_READY_OBD_1[2] |
| STAT_FUELSYSTEM_MONITOR_TEXT | string | Ueberwachung Kraftstoffsystem  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 STATE_READY_OBD_1[1] |
| STAT_FUELSYSTEM_MONITOR_WERT | int | Ueberwachung Kraftstoffsystem  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 STATE_READY_OBD_1[1] |
| STAT_MISSFIRE_MONITOR_TEXT | string | Ueberwachung Verbrennungsaussetzer  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 STATE_READY_OBD_1[0] |
| STAT_MISSFIRE_MONITOR_WERT | int | Ueberwachung Verbrennungsaussetzer  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 STATE_READY_OBD_1[0] |
| STAT_AGRRDY_EIN_TEXT | string | Ueberwachung Abgasrueckfuehrung  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[7] |
| STAT_AGRRDY_EIN_WERT | int | Ueberwachung Abgasrueckfuehrung  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[7] |
| STAT_HSRDY_EIN_TEXT | string | Ueberwachung Lambdasondenheizung  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[6] |
| STAT_HSRDY_EIN_WERT | int | Ueberwachung Lambdasondenheizung  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[6] |
| STAT_LSRDY_EIN_TEXT | string | Ueberwachung Lambdasonde  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[5] |
| STAT_LSRDY_EIN_WERT | int | Ueberwachung Lambdasonde  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[5] |
| STAT_KLIMARDY_EIN_TEXT | string | Ueberwachung Klimaanlage  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[4] |
| STAT_KLIMARDY_EIN_WERT | int | Ueberwachung Klimaanlage  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[4] |
| STAT_SLSRDY_EIN_TEXT | string | Ueberwachung Sekundaerluftsystem  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[3] |
| STAT_SLSRDY_EIN_WERT | int | Ueberwachung Sekundaerluftsystem  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[3] |
| STAT_TESRDY_EIN_TEXT | string | Ueberwachung Tankentlueftungssystem  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[2] |
| STAT_TESRDY_EIN_WERT | int | Ueberwachung Tankentlueftungssystem  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[2] |
| STAT_HKATRDY_EIN_TEXT | string | Ueberwachung Katalysatorheizung  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[1] |
| STAT_HKATRDY_EIN_WERT | int | Ueberwachung Katalysatorheizung  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[1] |
| STAT_KATRDY_EIN_TEXT | string | Ueberwachung Katalysator  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[0] |
| STAT_KATRDY_EIN_WERT | int | Ueberwachung Katalysator  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[0] |
| STAT_AGRMON_EIN_TEXT | string | Ueberwachung Abgasrueckfuehrung  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[7] |
| STAT_AGRMON_EIN_WERT | int | Ueberwachung Abgasrueckfuehrung  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[7] |
| STAT_HSMON_EIN_TEXT | string | Ueberwachung Lambdasondenheizung  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[6] |
| STAT_HSMON_EIN_WERT | int | Ueberwachung Lambdasondenheizung  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[6] |
| STAT_LSMON_EIN_TEXT | string | Ueberwachung Lambdasonde  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[5] |
| STAT_LSMON_EIN_WERT | int | Ueberwachung Lambdasonde  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[5] |
| STAT_KLIMAMON_EIN_TEXT | string | Ueberwachung Klimaanlage  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[4] |
| STAT_KLIMAMON_EIN_WERT | int | Ueberwachung Klimaanlage  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[4] |
| STAT_SLSMON_EIN_TEXT | string | Ueberwachung Sekundaerluftsystem  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[3] |
| STAT_SLSMON_EIN_WERT | int | Ueberwachung Sekundaerluftsystem  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[3] |
| STAT_TESMON_EIN_TEXT | string | Ueberwachung Tankentlueftungssystem  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[2] |
| STAT_TESMON_EIN_WERT | int | Ueberwachung Tankentlueftungssystem  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[2] |
| STAT_HKATMON_EIN_TEXT | string | Ueberwachung Katalysatorheizung  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[1] |
| STAT_HKATMON_EIN_WERT | int | Ueberwachung Katalysatorheizung  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[1] |
| STAT_KATMON_EIN_TEXT | string | Ueberwachung Katalysator  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[0] |
| STAT_KATMON_EIN_WERT | int | Ueberwachung Katalysator  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[0] |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh1"></a>
### STEUERN_ENDE_LSH1

0x2F60D000 STEUERN_ENDE_LSH1 Lambdasondenheizung vor Kat Bank1 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-aep-i12-zyklisches-nachladen-histogramm"></a>
### STATUS_AEP_I12_ZYKLISCHES_NACHLADEN_HISTOGRAMM

Auslesen der Histogramme über die Standzeit bis zum Beginn des zyklischen Nachladens und der Ladedauern der zyklischen Nachladevorgänge AEP_I12_ZYKLISCHES_NACHLADEN_HISTOGRAMM (0x22 409E)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_A | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich A. Bereich A &lt;= K_STDZEITLADEHISTGRZ1 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [0] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_B | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich A. Bereich A &lt;= K_STDZEITLADEHISTGRZ1 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [1] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_C | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich C. K_STDZEITLADEHISTGRZ2 (Tage) &lt; Bereich C &lt;= K_STDZEITLADEHISTGRZ3 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [2] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_D | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich D. K_STDZEITLADEHISTGRZ3 (Tage) &lt; Bereich D &lt;= K_STDZEITLADEHISTGRZ4 (Tage) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [3] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_E | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich E. K_STDZEITLADEHISTGRZ4 (Tage) &lt; Bereich E &lt;= K_STDZEITLADEHISTGRZ5 (Tage) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [4] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_F | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich F. K_STDZEITLADEHISTGRZ5 (Tage) &lt; Bereich F &lt;= K_STDZEITLADEHISTGRZ6 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [5] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_G | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich G. K_STDZEITLADEHISTGRZ6 (Tage) &lt; Bereich G &lt;= K_STDZEITLADEHISTGRZ7 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [6] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_H | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich H. K_STDZEITLADEHISTGRZ7 (Tage) &lt; Bereich H (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [7] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_A | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich A. Bereich A &lt;= K_NLDDAUERHISTGRZ1 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [8] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_B | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich B. K_NLDDAUERHISTGRZ1 (Minuten) &lt; Bereich B &lt;= K_NLDDAUERHISTGRZ2 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [9] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_C | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich C. K_NLDDAUERHISTGRZ2 (Minuten) &lt; Bereich C &lt;= K_NLDDAUERHISTGRZ3 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [10] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_D | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich D. K_NLDDAUERHISTGRZ3 (Minuten) &lt; Bereich D &lt;= K_NLDDAUERHISTGRZ4 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [11] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_E | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich E. K_NLDDAUERHISTGRZ4 (Minuten) &lt; Bereich E &lt;= K_NLDDAUERHISTGRZ5 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [12] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_F | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich F. K_NLDDAUERHISTGRZ5 (Minuten) &lt; Bereich F &lt;= K_NLDDAUERHISTGRZ6 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [13] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_G | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich G. K_NLDDAUERHISTGRZ6 (Minuten) &lt; Bereich F &lt;= K_NLDDAUERHISTGRZ7 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [14] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_H | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich G. K_NLDDAUERHISTGRZ6 (Minuten) &lt; Bereich F &lt;= K_NLDDAUERHISTGRZ7 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [15] Min: 0.0 Max: 255.0 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh2"></a>
### STEUERN_ENDE_LSH2

0x2F60D100 STEUERN_ENDE_LSH2 Lambdasondenheizung hinter Kat Bank1 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-agk"></a>
### STEUERN_AGK

0x2F60C103 STEUERN_AGK Abgasklappe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_AGK_WERT | unsigned long | Sollwert Abgasklappe LV_ACT_EF_EXT_ADJ[1]   Min: 0 Max: 1 |
| SW_TO_AGK_WERT | unsigned long | Timeout 0 bis 508s 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-geninfo"></a>
### _STATUS_GENINFO

0x22401B _STATUS_GENINFO Infospeicher Generatordiagnose erweitert auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DGENUB1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) ST_DGENUB1   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB1_EINH | string | V |
| STAT_DGENUB2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) ST_DGENUB2   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB2_EINH | string | V |
| STAT_DGENUBNZ_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) ST_DGENUBNZ   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUBNZ_EINH | string | V |
| STAT_DGENUBERR1 | unsigned long | Fehlerstatus zur Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) 1BIT IDENTICAL |
| STAT_DGENUBERR2 | unsigned long | Fehlerstatus zur Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) 1BIT IDENTICAL |
| STAT_DGENUBERRNZ | unsigned long | Fehlerstatus zur Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) 1BIT IDENTICAL |
| STAT_DGENUGEN1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) ST_DGENUGEN1   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN1_EINH | string | V |
| STAT_DGENUGEN2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) ST_DGENUGEN2   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN2_EINH | string | V |
| STAT_DGENUGENNZ_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) ST_DGENUGENNZ   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGENNZ_EINH | string | V |
| STAT_DGENUGENERR1 | unsigned long | Fehlerstatus zur Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) 1BIT IDENTICAL |
| STAT_DGENUGENERR2 | unsigned long | Fehlerstatus zur Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) 1BIT IDENTICAL |
| STAT_DGENUGENERRNZ | unsigned long | Fehlerstatus zur Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) 1BIT IDENTICAL |
| STAT_DGENGRENZ1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) ST_DGENGRENZ1   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ1_EINH | string | A |
| STAT_DGENGRENZ2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) ST_DGENGRENZ2   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ2_EINH | string | A |
| STAT_DGENGRENZNZ_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) ST_DGENGRENZNZ   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZNZ_EINH | string | A |
| STAT_DGENGRENZERR1 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) 1BIT IDENTICAL |
| STAT_DGENGRENZERR2 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) 1BIT IDENTICAL |
| STAT_DGENGRENZERRNZ | unsigned long | Fehlerstatus zur Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) 1BIT IDENTICAL |
| STAT_DGENUB1_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz ST_DGENUB1_MD1   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB1_MD1_EINH | string | V |
| STAT_DGENUB2_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz ST_DGENUB2_MD1   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB2_MD1_EINH | string | V |
| STAT_DGENUBNZ_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz ST_DGENUBNZ_MD1   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUBNZ_MD1_EINH | string | V |
| STAT_DGENUBERR1_MD1 | unsigned long | Fehlerstatus zur Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUBERR2_MD1 | unsigned long | Fehlerstatus zur Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUBERRNZ_MD1 | unsigned long | Fehlerstatus zur Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGEN1_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz ST_DGENUGEN1_MD1   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN1_MD1_EINH | string | V |
| STAT_DGENUGEN2_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz ST_DGENUGEN2_MD1   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN2_MD1_EINH | string | V |
| STAT_DGENUGENNZ_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz ST_DGENUGENNZ_MD1   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGENNZ_MD1_EINH | string | V |
| STAT_DGENUGENERR1_MD1 | unsigned long | Fehlerstatus zur Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGENERR2_MD1 | unsigned long | Fehlerstatus zur Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGENERRNZ_MD1 | unsigned long | Fehlerstatus zur Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZ1_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz ST_DGENGRENZ1_MD1   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ1_MD1_EINH | string | A |
| STAT_DGENGRENZ2_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz ST_DGENGRENZ2_MD1   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ2_MD1_EINH | string | A |
| STAT_DGENGRENZNZ_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz ST_DGENGRENZNZ_MD1   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZNZ_MD1_EINH | string | A |
| STAT_DGENGRENZERR1_MD1 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZERR2_MD1 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZERRNZ_MD1 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUB1_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz ST_DGENUB1_MD2   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB1_MD2_EINH | string | V |
| STAT_DGENUB2_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz ST_DGENUB2_MD2   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB2_MD2_EINH | string | V |
| STAT_DGENUBNZ_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz ST_DGENUBNZ_MD2   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUBNZ_MD2_EINH | string | V |
| STAT_DGENUBERR1_MD2 | unsigned long | Fehlerstatus zur Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUBERR2_MD2 | unsigned long | Fehlerstatus zur Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUBERRNZ_MD2 | unsigned long | Fehlerstatus zur Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGEN1_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz ST_DGENUGEN1_MD2   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN1_MD2_EINH | string | V |
| STAT_DGENUGEN2_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz ST_DGENUGEN2_MD2   Einheit: V   Min: 0 Max: 25.5 |
| STAT_DGENUGEN2_MD2_EINH | string | V |
| STAT_DGENUGENNZ_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz ST_DGENUGENNZ_MD2   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGENNZ_MD2_EINH | string | V |
| STAT_DGENUGENERR1_MD2 | unsigned long | Fehlerstatus zur Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGENERR2_MD2 | unsigned long | Fehlerstatus zur Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGENERRNZ_MD2 | unsigned long | Fehlerstatus zur Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZ1_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz ST_DGENGRENZ1_MD2   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ1_MD2_EINH | string | A |
| STAT_DGENGRENZ2_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz ST_DGENGRENZ2_MD2   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ2_MD2_EINH | string | A |
| STAT_DGENGRENZNZ_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz ST_DGENGRENZNZ_MD2   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZNZ_MD2_EINH | string | A |
| STAT_DGENGRENZERR1_MD2 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZERR2_MD2 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZERRNZ_MD2 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMRUHVERL_MD1 | unsigned long | PM Ruhestromverletzung zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMBATT_MD1 | unsigned long | Fehler PM Batterie zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMBN_MD1 | unsigned long | Fehler PM Bordnetz zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSDGLOB_MD1 | unsigned long | Fehler BSD global zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_4_MD1 | unsigned long | Kommunikation QLT zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_3_MD1 | unsigned long | Kommunikation EWAPU zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_0_MD1 | unsigned long | Kommunikation IBS zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENREGUPL_MD1 | unsigned long | Generatorfehler Reglertyp unplausibel zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENHTB_MD1 | unsigned long | Generatorfehler Hochtemperatur berechnet zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENELB_MD1 | unsigned long | Generatorfehler elektrisch berechnet zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENKOMM_MD1 | unsigned long | Kommunikation Generator zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENUPL_MD1 | unsigned long | Generatorfehler Typ unplausibel zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENHT_MD1 | unsigned long | Generatorfehler Hochtemperatur (Bitauswertung) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENMECH_MD1 | unsigned long | Generatorfehler mechanisch (Bitauswertung) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENEL_MD1 | unsigned long | Generatorfehler elektrisch (Bitauswertung) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMRUHVERL_MD2 | unsigned long | PM Ruhestromverletzung zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMBATT_MD2 | unsigned long | Fehler PM Batterie zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMBN_MD2 | unsigned long | Fehler PM Bordnetz zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSDGLOB_MD2 | unsigned long | Fehler BSD global zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_4_MD2 | unsigned long | Kommunikation QLT zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_3_MD2 | unsigned long | Kommunikation EWAPU zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_0_MD2 | unsigned long | Kommunikation IBS zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENREGUPL_MD2 | unsigned long | Generatorfehler Reglertyp unplausibel zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENHTB_MD2 | unsigned long | Generatorfehler Hochtemperatur berechnet zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENELB_MD2 | unsigned long | Generatorfehler elektrisch berechnet zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENKOMM_MD2 | unsigned long | Kommunikation Generator zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENUPL_MD2 | unsigned long | Generatorfehler Typ unplausibel zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENHT_MD2 | unsigned long | Generatorfehler Hochtemperatur (Bitauswertung) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENMECH_MD2 | unsigned long | Generatorfehler mechanisch (Bitauswertung) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENEL_MD2 | unsigned long | Generatorfehler elektrisch (Bitauswertung) zu 2. Messdatensatz 1BIT IDENTICAL |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-vorkonfig-opf"></a>
### STATUS_VORKONFIG_OPF

0x3103F082 STATUS_VORKONFIG_OPF Vorkonditionierung Otto Partikelfilter auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OPF_FS_TEXT | string | Funktionsstatus OPF 1BYTE FUNKTIONSSTATUS |
| STAT_OPF_FS_WERT | int | Funktionsstatus OPF 1BYTE FUNKTIONSSTATUS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-l-regelung-aus"></a>
### STATUS_SYSTEMCHECK_L_REGELUNG_AUS

0x3103F0D9 STATUS_SYSTEMCHECK_L_REGELUNG_AUS Auslesen Lambdaregelung ausschalten Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_REGELUNG_AUS | unsigned long | Status der Lambdasondenregelung LV_INH_LAM_KWP   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-eluer"></a>
### STEUERN_ELUER

0x2F608103 STEUERN_ELUER E-Luefter-Relais ansteuern NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ELUER_WERT | unsigned long | Sollwert E-Luefter-Relais LV_ACT_ECF_RLY_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_ELUER_WERT | unsigned long | Timeout E-Luefter-Relais 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ruhestrommessung"></a>
### STEUERN_RUHESTROMMESSUNG

Ansteuern Ruhestrompruefung mit IBS UDS  : $31 RoutineControl UDS  : $01 startRoutine UDS  : $F02B Ruhestrompruefung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_MAX_WERT | real | Max. Ruhestromschwelle (Eco_max_i) Eco_max_i   Einheit: A   Min: 0 Max: 1.275 |
| MSB_WERT | real | Ecos Messtartbedingung (Eco_msb) Eco_msb   Einheit: s   Min: 0 Max: 12.75 |
| MZ_WERT | real | Dauer Mittelwertmessung (Eco_mz) Eco_mz   Einheit: s   Min: 0 Max: 12.75 |
| TO_WERT | unsigned long | Ecos Messung Timeout (Eco_timo) Eco_timo   Einheit: min   Min: 1 Max: 254 Achtung, Wert 128 ist ungültig |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG (MEN48) |
| _RESPONSE | binary | Hex-Auftrag an SG (MEN48) |

<a id="job-ident-ibs"></a>
### IDENT_IBS

0x224021 IDENT_IBS Identifikationsdaten fuer IBS-Sensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_BMW_NR | string | BMW-Teilenummer 7 stellig vehicle Manufacturer ECU hardware Number Part2 |
| SERIENNUMMER | unsigned long | BMW-Seriennummer SNIBS   Min: 0 Max: 4294967295 |
| ZIF_PROGRAMMSTAND | unsigned long | Programm referenz IBSWBASE   Min: 0 Max: 255 |
| ZIF_STATUS | unsigned long | IBS Software Aenderungs Status (Programm Revision) IBSWCHANG   Min: 0 Max: 255 |
| HW_REF | unsigned long | IBS Hardware Version (Hardware Referenz) IBHWVERSI   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-evausbl"></a>
### STATUS_SYSTEMCHECK_EVAUSBL

0x3103F025 STATUS_SYSTEMCHECK_EVAUSBL Auslesen Diagnosefunktion EinspritzVentile EV-Ausblendung !ACHTUNG: hier wird die Zuendreihenfolge Bitcodiert verwendet! Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VENTIL_NR | unsigned long | Nummer des ausgeblendeten Einspritzventils INH_IV_KWP   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-igrinfo-aep"></a>
### STATUS_IGRINFO_AEP

0x224016 STATUS_IGRINFO_AEP Infospeicher Intelligente Generator Regelung (IGR) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_IGR_AEP0_BITS7 | unsigned long | Begrenzung 2 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS7_INFO | string | High Zyklisierungsgrenze erreicht/nicht erreicht (b_zykl_igrh) |
| STAT_IGR_AEP0_BITS6 | unsigned long | Begrenzung 1 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS6_INFO | string | Med Zyklisierungsgrenze erreicht/nicht erreicht (b_zykl_igrm) |
| STAT_IGR_AEP0_BITS5 | unsigned long | Regeneration 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS5_INFO | string | Regenerationsfunktion aktiv/nicht aktiv (B_battregen) |
| STAT_IGR_AEP0_BITS4 | unsigned long | IGR-Medium 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS4_INFO | string | IGR-Mediumphase angefordert/nicht angefordert (B_igrmed) |
| STAT_IGR_AEP0_BITS3 | unsigned long | IGR-High 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS3_INFO | string | IGR-Highphase angefordert/nicht angefordert (B_igrhigh) |
| STAT_IGR_AEP0_BITS2 | unsigned long | IGR-Low 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS2_INFO | string | IGR-Lowphase angefordert/nicht angefordert (B_igrlow) |
| STAT_IGR_AEP0_BITS1 | unsigned long | Diagnosejob gesetzt 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS1_INFO | string | IGR-Diagnose gesetzt/nicht gesetzt (B_diagigr) |
| STAT_IGR_AEP0_BITS0 | unsigned long | IGR codiert 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS0_INFO | string | IGR codiert/nicht codiert (B_cdigronw) |
| STAT_U_BN_SOLL_WERT | real | DREC_IGRINFO[2] 1BYTE in 0 bis 25,5Volt   Einheit: V   Min: 0 Max: 25.5 |
| STAT_U_BN_SOLL_EINH | string | V |
| STAT_IGR_AEP_PR1 | unsigned long | DREC_IGRINFO[3] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_AEP_PR2 | unsigned long | DREC_IGRINFO[4] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_AEP_QREKUP_WERT | real | DREC_IGRINFO[5] 1BYTE in 0 bis 25,5   Min: 0 Max: 25,5 |
| STAT_IGR_AEP_QREKUP_EINH | string | Ah |
| STAT_IGR_AEP_QLAD_WERT | real | Bilanz Low 2BYTE_in_0bis19088Ah   Einheit: Ah   Min: 0 Max: 19088.1 |
| STAT_IGR_AEP_QLAD_EINH | string | Ah |
| STAT_IGR_AEP_QLAD_M_WERT | long | Bilanz Medium IGRINFO_1BYTE_in_minus128bis127Ah   Einheit: Ah   Min: -128 Max: 127 |
| STAT_IGR_AEP_QLAD_M_EINH | string | Ah |
| STAT_IGR_AEP_QELAD_WERT | real | Bilanz High 2BYTE_in_0bis19088Ah   Einheit: Ah   Min: 0 Max: 19088.1 |
| STAT_IGR_AEP_QELAD_EINH | string | Ah |
| STAT_REG_AEP_ZR | unsigned long | Einfachzaehler 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_AEP_TCODE_WERT | unsigned long | Dauer iGR-Codiert 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_IGR_AEP_TCODE_EINH | string | Einfachzaehler 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_REG_AEP_SEIT_WERT | real | Zeit seit letzter R 1BYTE_in_0bis255h   Einheit: h   Min: 0 Max: 255 |
| STAT_REG_AEP_SEIT_EINH | string | h |
| STAT_REG_AEP_DAUER_WERT | real | Dauer letzte R 1BYTE_in_0bis255h   Einheit: h   Min: 0 Max: 255 |
| STAT_REG_AEP_DAUER_EINH | string | h |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hexfo-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-rbmms3"></a>
### STATUS_RBMMS3

0x224066 STATUS_RBMMS3 Rate Based Monitoring Motorsteuerung MS... Block 3 auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CTR_COMP_RBM_PUC_VLD_LS_UP_1 | unsigned long | (A2L-Name: rbm_stat_PUC_VLD_LS_UP_1.ctr_comp_rbm) CTR_COMP_RBM_PUC_VLD_LS_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_PUC_VLD_LS_UP_1 | unsigned long | (A2L-Name: rbm_stat_PUC_VLD_LS_UP_1.ctr_cdn_rbm) CTR_CDN_RBM_PUC_VLD_LS_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_PUC_VLD_LS_UP_2 | unsigned long | A2L-Name: rbm_stat_PUC_VLD_LS_UP_2.ctr_comp_rbm) CTR_COMP_RBM_PUC_VLD_LS_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_PUC_VLD_LS_UP_2 | unsigned long | (A2L-Name: rbm_stat_PUC_VLD_LS_UP_2.ctr_cdn_rbm) CTR_CDN_RBM_PUC_VLD_LS_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_OC_LS_DOWN_1 | unsigned long | (A2L-Name: rbm_stat_OC_LS_DOWN_1.ctr_comp_rbm) CTR_COMP_RBM_OC_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_OC_LS_DOWN_1 | unsigned long | (A2L-Name: rbm_stat_OC_LS_DOWN_1.ctr_cdn_rbm) CTR_CDN_RBM_OC_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_OC_LS_DOWN_2 | unsigned long | (A2L-Name: rbm_stat_OC_LS_DOWN_2.ctr_comp_rbm) CTR_COMP_RBM_OC_LS_DOWN_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_OC_LS_DOWN_2 | unsigned long | (A2L-Name: rbm_stat_OC_LS_DOWN_2.ctr_cdn_rbm) CTR_CDN_RBM_OC_LS_DOWN_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SCG_LS_DOWN_1 | unsigned long | (A2L-Name: rbm_stat_SCG_LS_DOWN_1.ctr_comp_rbm) CTR_COMP_RBM_SCG_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SCG_LS_DOWN_1 | unsigned long | A2L-Name: rbm_stat_SCG_LS_DOWN_1.ctr_cdn_rbm) CTR_CDN_RBM_SCG_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SCG_LS_DOWN_2 | unsigned long | (A2L-Name: rbm_stat_SCG_LS_DOWN_2.ctr_comp_rbm) CTR_COMP_RBM_SCG_LS_DOWN_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SCG_LS_DOWN_2 | unsigned long | (A2L-Name: rbm_stat_SCG_LS_DOWN_2.ctr_cdn_rbm) CTR_CDN_RBM_SCG_LS_DOWN_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_OC_LSL_UP_1 | unsigned long | (A2L-Name: rbm_stat_OC_LSL_UP_1.ctr_comp_rbm) CTR_COMP_RBM_OC_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_OC_LSL_UP_1 | unsigned long | (A2L-Name: rbm_stat_OC_LSL_UP_1.ctr_cdn_rbm) CTR_CDN_RBM_OC_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_OC_LSL_UP_2 | unsigned long | (A2L-Name: rbm_stat_OC_LSL_UP_2.ctr_comp_rbm) CTR_COMP_RBM_OC_LSL_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_OC_LSL_UP_2 | unsigned long | (A2L-Name: rbm_stat_OC_LSL_UP_2.ctr_cdn_rbm) CTR_CDN_RBM_OC_LSL_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_CSERS_INJ | unsigned long | (A2L-Name: rbm_stat_CSERS_INJ.ctr_comp_rbm) CTR_COMP_RBM_CSERS_INJ   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_CSERS_INJ | unsigned long | (A2L-Name: rbm_stat_CSERS_INJ.ctr_cdn_rbm) CTR_CDN_RBM_CSERS_INJ   Min: 0 Max: 65535 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-rbmms2"></a>
### STATUS_RBMMS2

0x224028 STATUS_RBMMS2 Rate Based Monitoring Motorsteuerung MS (VDO) Block 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CTR_COMP_RBM_DIAGCPS | unsigned long | Diagnose Tankentlueftungssystem (Numerator) CTR_COMP_RBM_DIAGCPS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_DIAGCPS | unsigned long | Diagnose Tankentlueftungssystem (Denominator) CTR_CDN_RBM_DIAGCPS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_ROUGH_LEAK | unsigned long | Diagnose Tankgrobleckpruefung (DMTL) (Numerator) CTR_COMP_RBM_ROUGH_LEAK   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_ROUGH_LEAK | unsigned long | Diagnose Tankgrobleckpruefung (DMTL) (Denominator) CTR_CDN_RBM_ROUGH_LEAK   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_DMTLM | unsigned long | Diagnosemodul Tankleckage (DMTL) (Numerator) CTR_COMP_RBM_DMTLM   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_DMTLM | unsigned long | Diagnosemodul Tankleckage (DMTL) (Denominator) CTR_CDN_RBM_DMTLM   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TH | unsigned long | Diagnose Thermostat (Numerator) CTR_COMP_RBM_TH   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TH | unsigned long | Diagnose Thermostat (Denominator) CTR_CDN_RBM_TH   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TCO_PLAUS | unsigned long | Diagnose Motortemperatur Plausibilitaet (Numerator) CTR_COMP_RBM_TCO_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TCO_PLAUS | unsigned long | Diagnose Motortemperatur Plausibilitaet (Denominator) CTR_CDN_RBM_TCO_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TCO_STUCK | unsigned long | Diagnose Motortemperatur haengendes Sensorsignal (Numerator) CTR_COMP_RBM_TCO_STUCK   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TCO_STUCK | unsigned long | Diagnose Motortemperatur haengendes Sensorsignal (Denominator) CTR_CDN_RBM_TCO_STUCK   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TCO_2_PLAUS | unsigned long | Diagnose Kuehlerauslasstemperatur Plausibilitaet (Numerator) CTR_COMP_RBM_TCO_2_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TCO_2_PLAUS | unsigned long | Diagnose Kuehlerauslasstemperatur Plausibilitaet (Denominator) CTR_CDN_RBM_TCO_2_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TAM_PLAUS | unsigned long | Diagnose Umgebungstemperatur Plausibilitaet (Numerator) CTR_COMP_RBM_TAM_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TAM_PLAUS | unsigned long | Diagnose Umgebungstemperatur Plausibilitaet (Denominator) CTR_CDN_RBM_TAM_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_VS_PLAUS | unsigned long | Diagnose Geschwindigkeit Plausibilitaet (Numerator) CTR_COMP_RBM_VS_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_VS_PLAUS | unsigned long | Diagnose Geschwindigkeit Plausibilitaet (Denominator) CTR_CDN_RBM_VS_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_FTL_OBD | unsigned long | Diagnose Tankfuellstand (Numerator) CTR_COMP_RBM_FTL_OBD   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_FTL_OBD | unsigned long | Diagnose Tankfuellstand (Denominator) CTR_CDN_RBM_FTL_OBD   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_OBD_LSH_DOWN_1 | unsigned long | Diagnose Lamdasondenheizung nach Katalysator Bank 1 (Numerator) CTR_COMP_RBM_OBD_LSH_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_OBD_LSH_DOWN_1 | unsigned long | Diagnose Lamdasondenheizung nach Katalysator Bank 1 (Denominator) CTR_CDN_RBM_OBD_LSH_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_OBD_VLD_LSH_UP_1 | unsigned long | Diagnose Alterung lineare Lamdasonde Bank 1 (Numerator) CTR_COMP_RBM_OBD_VLD_LSH_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_OBD_VLD_LSH_UP_1 | unsigned long | Diagnose Alterung lineare Lamdasonde Bank 1 (Denominator) CTR_CDN_RBM_OBD_VLD_LSH_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_CS | unsigned long | Diagnose Kupplungsschalter (Numerator) CTR_COMP_RBM_CS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_CS | unsigned long | Diagnose Kupplungsschalter (Denominator) CTR_CDN_RBM_CS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_ISC | unsigned long | Diagnose Leerlaufregler (Numerator) CTR_COMP_RBM_ISC   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_ISC | unsigned long | Diagnose Leerlaufregler (Denominator) CTR_CDN_RBM_ISC   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_MAF | unsigned long | Diagnose Luftmassenmesser (Numerator) CTR_COMP_RBM_MAF   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_MAF | unsigned long | Diagnose Luftmassenmesser (Denominator) CTR_CDN_RBM_MAF   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_AMP_PLAUS | unsigned long | Diagnose Umgebungsdruck Plausibilitaet (Numerator) CTR_COMP_RBM_AMP_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CND_RBM_AMP_PLAUS | unsigned long | Diagnose Umgebungsdruck Plausibilitaet (Denominator) CTR_CDN_RBM_AMP_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_LOAD_TPS_PLAUS | unsigned long | Diagnose Plausibilitaet Drosselklappeposition zu Signal Luftmassenmesser 6 Zylinder  (Numerator) CTR_COMP_RBM_LOAD_TPS_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_LOAD_TPS_PLAUS | unsigned long | Diagnose Plausibilitaet Drosselklappeposition zu Signal Luftmassenmesser 6 Zylinder  (Denominator) CTR_CDN_RBM_LOAD_TPS_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_PUT_PLAUS | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_PUT_PLAUS.ctr_comp_rbm) CTR_COMP_RBM_PUT_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_PUT_PLAUS | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_PUT_PLAUS.ctr_cdn_rbm) CTR_CDN_RBM_PUT_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_MAP_PLAUS | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_MAP_PLAUS.ctr_comp_rbm) CTR_COMP_RBM_MAP_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_MAP_PLAUS | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_MAP_PLAUS.ctr_cdn_rbm) CTR_CDN_RBM_MAP_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_MAP_TPS_PLAUS | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_MAP_TPS_PLAUS.ctr_comp_rbm) CTR_COMP_RBM_MAP_TPS_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_MAP_TPS_PLAUS | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_MAP_TPS_PLAUS.ctr_cdn_rbm) CTR_CDN_RBM_MAP_TPS_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_VLS_DOWN_DIF_1 | unsigned long | (A2L-Name: rbm_stat_VLS_DOWN_DIF_1.ctr_comp_rbm) CTR_COMP_RBM_VLS_DOWN_DIF_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_VLS_DOWN_DIF_1 | unsigned long | (A2L-Name: rbm_stat_VLS_DOWN_DIF_1.ctr_cdn_rbm) CTR_CDN_RBM_VLS_DOWN_DIF_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_T_ES | unsigned long | (A2L-Name: rbm_stat_T_ES.ctr_comp_rbm) CTR_COMP_RBM_T_ES   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_T_ES | unsigned long | (A2L-Name: rbm_stat_T_ES.ctr_cdn_rbm) CTR_CDN_RBM_T_ES   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TPS | unsigned long | (A2L-Name: rbm_stat_TPS.ctr_comp_rbm) CTR_COMP_RBM_TPS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TPS | unsigned long | (A2L-Name: rbm_stat_TPS.ctr_cdn_rbm) CTR_CDN_RBM_TPS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_ISC_CST | unsigned long | (A2L-Name: rbm_stat_ISC_CST.ctr_comp_rbm) CTR_COMP_RBM_ISC_CST   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_ISC_CST | unsigned long | (A2L-Name: rbm_stat_ISC_CST.ctr_cdn_rbm) CTR_CDN_RBM_ISC_CST   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TQ_CST | unsigned long | (A2L-Name: rbm_stat_TQ_CST.ctr_comp_rbm) CTR_COMP_RBM_TQ_CST   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TQ_CST | unsigned long | (A2L-Name: rbm_stat_TQ_CST.ctr_cdn_rbm) CTR_CDN_RBM_TQ_CST   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TCO_STUCK_RNG | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_TCO_STUCK_RNG.ctr_comp_rbm) CTR_COMP_RBM_TCO_STUCK_RNG   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TCO_STUCK_RNG | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_TCO_STUCK_RNG.ctr_cdn_rbm) CTR_CDN_RBM_TCO_STUCK_RNG   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TIA_IM_MES_PLAUS_0 | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_TIA_IM_MES_PLAUS_1.ctr_comp_rbm) CTR_COMP_RBM_TIA_IM_MES_PLAUS_0   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TIA_IM_MES_PLAUS_1 | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_TIA_IM_MES_PLAUS_1.ctr_cdn_rbm) CTR_CDN_RBM_TIA_IM_MES_PLAUS_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TIA_MES_PLAUS_0 | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_TIA_MES_PLAUS_0.ctr_comp_rbm) CTR_COMP_RBM_TIA_MES_PLAUS_0   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TIA_MES_PLAUS_0 | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_TIA_MES_PLAUS_0.ctr_cdn_rbm) CTR_CDN_RBM_TIA_MES_PLAUS_0   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TIA_THR_MES_PLAUS_0 | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_TIA_THR_MES_PLAUS_0.ctr_comp_rbm) CTR_COMP_RBM_TIA_THR_MES_PLAUS_0   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TIA_THR_MES_PLAUS_0 | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_TIA_THR_MES_PLAUS_0.ctr_cdn_rbm) CTR_CDN_RBM_TIA_THR_MES_PLAUS_0   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_T_ES_TCO_FAST | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_T_ES_TCO_FAST.ctr_comp_rbm) CTR_COMP_RBM_T_ES_TCO_FAST   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_T_ES_TCO_FAST | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_T_ES_TCO_FAST.ctr_cdn_rbm) CTR_CDN_RBM_T_ES_TCO_FAST   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_T_ES_TCO_SLOW | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_T_ES_TCO_SLOW.ctr_comp_rbm) CTR_COMP_RBM_T_ES_TCO_SLOW   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_T_ES_TCO_SLOW | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_T_ES_TCO_SLOW.ctr_cdn_rbm) CTR_CDN_RBM_T_ES_TCO_SLOW   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_FUP_CH | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_FUP_CH.ctr_comp_rbm) CTR_COMP_RBM_FUP_CH   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_FUP_CH | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_FUP_CH.ctr_cdn_rbm) CTR_CDN_RBM_FUP_CH   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_EFF_IGA_CST_IS | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_EFF_IGA_CST_IS.ctr_comp_rbm) CTR_COMP_RBM_EFF_IGA_CST_IS   Min: 0 Max: 65535 |
| STAT_CTR_CND_RBM_EFF_IGA_CST_IS | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_EFF_IGA_CST_IS.ctr_cdn_rbm) CTR_CDN_RBM_EFF_IGA_CST_IS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_EFF_IGA_CST_PL | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_EFF_IGA_CST_PL.ctr_comp_rbm) CTR_COMP_RBM_EFF_IGA_CST_PL   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_EFF_IGA_CST_PL | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_EFF_IGA_CST_PL.ctr_cdn_rbm) CTR_CDN_RBM_EFF_IGA_CST_PL   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_CAM_CST_IVVT_IN_1 | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_CAM_CST_IVVT_IN_1.ctr_comp_rbm) CTR_COMP_RBM_CAM_CST_IVVT_IN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_CAM_CST_IVVT_IN_1 | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_CAM_CST_IVVT_IN_1.ctr_cdn_rbm) CTR_CDN_RBM_CAM_CST_IVVT_IN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_CAM_CST_IVVT_EX_1 | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_CAM_CST_IVVT_EX_1.ctr_comp_rbm) CTR_COMP_RBM_CAM_CST_IVVT_EX_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_CAM_CST_IVVT_EX_1 | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_CAM_CST_IVVT_EX_1.ctr_cdn_rbm) CTR_CDN_RBM_CAM_CST_IVVT_EX_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_OPF_PFLT_CLD_CHK_T_SENS | unsigned long | Kaltstart Check Temperatursensor nach Partikelfilter Numerator 2BYTE_DUMMY |
| STAT_CTR_CND_OPF_PFLT_CLD_CHK_T_SENS | unsigned long | Kaltstart Check Temperatursensor nach Partikelfilter Denominator 2BYTE_DUMMY |
| STAT_CTR_COMP_OPF_PFLT_SIG_CHK_T_SENS | unsigned long | Haengendes Signal Check Temperatursensor nach Partikelfilter Numerator 2BYTE_DUMMY |
| STAT_CTR_CND_OPF_PFLT_SIG_CHK_T_SENS | unsigned long | Haengendes Signal Check Temperatursensor nach Partikelfilter Denominator 2BYTE_DUMMY |
| STAT_CTR_COMP_OPF_PFLT_CLD_CHK_T_SENS_2 | unsigned long | Kaltstart Check Temperatursensor vor Partikelfilter Numerator 2BYTE_DUMMY |
| STAT_CTR_CND_OPF_PFLT_CLD_CHK_T_SENS_2 | unsigned long | Kaltstart Check Temperatursensor vor Partikelfilter Denominator 2BYTE_DUMMY |
| STAT_CTR_COMP_OPF_PFLT_SIG_CHK_T_SENS_2 | unsigned long | Haengendes Signal Check Temperatursensor vor Partikelfilter Numerator 2BYTE_DUMMY |
| STAT_CTR_CND_OPF_PFLT_SIG_CHK_T_SENS_2 | unsigned long | Haengendes Signal Check Temperatursensor vor Partikelfilter Denominator 2BYTE_DUMMY |
| STAT_CTR_COMP_OPF_PFLT_ST_CHK_T_SENS | unsigned long | Stationaerer Zustand Check Temperatursensor nach Partikelfilter Numerator 2BYTE_DUMMY |
| STAT_CTR_CND_OPF_PFLT_ST_CHK_T_SENS | unsigned long | Stationaerer Zustand Check Temperatursensor nach Partikelfilter Denominator 2BYTE_DUMMY |
| STAT_CTR_COMP_OPF_PFLT_ST_CHK_T_SENS_2 | unsigned long | Stationaerer Zustand Check Temperatursensor vor Partikelfilter Numerator 2BYTE_DUMMY |
| STAT_CTR_CND_OPF_PFLT_ST_CHK_T_SENS_2 | unsigned long | Stationaerer Zustand Check Temperatursensor vor Partikelfilter Denominator 2BYTE_DUMMY |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-rbmms1"></a>
### STATUS_RBMMS1

0x224027 STATUS_RBMMS1 Rate Based Monitoring Motorsteuerung MS (VDO) Block 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CTR_COMP_RBM_CAT_DIAG_1 | unsigned long | Diagnose Katalysator Sauerstoffspeicherfaehigkeit Bank 1 (Numerator) CTR_COMP_RBM_CAT_DIAG_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_CAT_DIAG_1 | unsigned long | Diagnose Katalysator Sauerstoffspeicherfaehigkeit Bank 1 (Denominator) CTR_CDN_RBM_CAT_DIAG_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_DYN_VLD_LS_UP_1 | unsigned long | (A2L-Name: rbm_stat_DYN_VLD_LS_UP_1.ctr_comp_rbm) CTR_COMP_RBM_DYN_VLD_LS_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_DYN_VLD_LS_UP_1 | unsigned long | (A2L-Name: rbm_stat_DYN_VLD_LS_UP_1.ctr_cdn_rbm) CTR_CDN_RBM_DYN_VLD_LS_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SHIFT_AFL_LSL_UP_1 | unsigned long | (A2L-Name: rbm_stat_SHIFT_AFL_LSL_UP_1.ctr_comp_rbm) CTR_COMP_RBM_SHIFT_AFL_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SHIFT_AFL_LSL_UP_1 | unsigned long | (A2L-Name: rbm_stat_SHIFT_AFL_LSL_UP_1.ctr_cdn_rbm) CTR_CDN_RBM_SHIFT_AFL_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SHIFT_AFR_LSL_UP_1 | unsigned long | (A2L-Name: rbm_stat_SHIFT_AFR_LSL_UP_1.ctr_comp_rbm) CTR_COMP_RBM_SHIFT_AFR_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SHIFT_AFR_LSL_UP_1 | unsigned long | (A2L-Name: rbm_stat_SHIFT_AFR_LSL_UP_1.ctr_cdn_rbm) CTR_CDN_RBM_SHIFT_AFR_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_AIR_LSL_UP_1 | unsigned long | (A2L-Name: rbm_stat_AIR_LSL_UP_1.ctr_comp_rbm) CTR_COMP_RBM_AIR_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_AIR_LSL_UP_1 | unsigned long | (A2L-Name: rbm_stat_AIR_LSL_UP_1.ctr_cdn_rbm) CTR_CDN_RBM_AIR_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SMALL_LEAK | unsigned long | (A2L-Name: rbm_stat_SMALL_LEAK.ctr_comp_rbm) CTR_COMP_RBM_SMALL_LEAK   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SMALL_LEAK | unsigned long | (A2L-Name: rbm_stat_SMALL_LEAK.ctr_cdn_rbm) CTR_CDN_RBM_SMALL_LEAK   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_MEC_IVVT_IN | unsigned long | (A2L-Name: rbm_stat_MEC_IVVT_IN.ctr_comp_rbm) CTR_COMP_RBM_MEC_IVVT_IN   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_MEC_IVVT_IN | unsigned long | (A2L-Name: rbm_stat_MEC_IVVT_IN.ctr_cdn_rbm) CTR_CDN_RBM_MEC_IVVT_IN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_MEC_IVVT_EX | unsigned long | (A2L-Name: rbm_stat_MEC_IVVT_EX.ctr_comp_rbm) CTR_COMP_RBM_MEC_IVVT_EX   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_MEC_IVVT_EX | unsigned long | (A2L-Name: rbm_stat_MEC_IVVT_EX.ctr_cdn_rbm) CTR_CDN_RBM_MEC_IVVT_EX   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TOOTH_OFF_IN_1 | unsigned long | (A2L-Name: rbm_stat_TOOTH_OFF_IN_1.ctr_comp_rbm) CTR_COMP_RBM_TOOTH_OFF_IN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TOOTH_OFF_IN_1 | unsigned long | (A2L-Name: rbm_stat_TOOTH_OFF_IN_1.ctr_cdn_rbm) CTR_CDN_RBM_TOOTH_OFF_IN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TOOTH_OFF_EX_1 | unsigned long | (A2L-Name: rbm_stat_TOOTH_OFF_EX_1.ctr_comp_rbm) CTR_COMP_RBM_TOOTH_OFF_EX_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TOOTH_OFF_EX_1 | unsigned long | (A2L-Name: rbm_stat_TOOTH_OFF_EX_1.ctr_cdn_rbm) CTR_CDN_RBM_TOOTH_OFF_EX_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SA_SAP_TUBE | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_SA_SAP_TUBE.ctr_comp_rbm) CTR_COMP_RBM_SA_SAP   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SA_SAP_TUBE | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_SA_SAP_TUBE.ctr_cdn_rbm) CTR_CDN_RBM_SA_SAP_TUBE   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SA_SYS | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_SA_SYS.ctr_comp_rbm) CTR_COMP_RBM_SA_SYS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SA_SYS | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_SA_SYS.ctr_cdn_rbm) CTR_CDN_RBM_SA_SYS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SA_TUBE | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_SA_TUBE.ctr_comp_rbm) CTR_COMP_RBM_SA_TUBE   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SA_TUBE | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_SA_TUBE.ctr_cdn_rbm) CTR_CDN_RBM_SA_TUBE   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SAV_JAM_CLOSE | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_SAV_JAM_CLOSE.ctr_comp_rbm) CTR_COMP_RBM_SAV_JAM_CLOSE   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SAV_JAM_CLOSE | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_SAV_JAM_CLOSE.ctr_cdn_rbm) CTR_CDN_RBM_SAV_JAM_CLOSE   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SAV_JAM_OPEN | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_SAV_JAM_OPEN.ctr_comp_rbm) CTR_COMP_RBM_SAV_JAM_OPEN   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SAV_JAM_OPEN | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_SAV_JAM_OPEN.ctr_cdn_rbm) CTR_CDN_RBM_SAV_JAM_OPEN   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_PRS_SA_SIG_CHK | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_PRS_SA_SIG_CHK.ctr_comp_rbm) CTR_COMP_RBM_PRS_SA_SIG_CHK   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_PRS_SA_SIG_CHK | unsigned long | DREC_Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_PRS_SA_SIG_CHK.ctr_cdn_rbm) CTR_CDN_RBM_PRS_SA_SIG_CHK   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_CHK_LS_DOWN_1 | unsigned long | (A2L-Name: rbm_stat_CHK_LS_DOWN_1.ctr_comp_rbm) CTR_COMP_RBM_CHK_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_CHK_LS_DOWN_1 | unsigned long | (A2L-Name: rbm_stat_CHK_LS_DOWN_1.ctr_cdn_rbm) CTR_CDN_RBM_CHK_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SWT_LS_DOWN_1 | unsigned long | GRD- Diagnose fett zu mager Bank 1 (Numerator) (A2L-Name:rbm_stat_GRD_R2L_LS_DOWN_1.ctr_comp_rbm) CTR_COMP_RBM_SWT_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SWT_LS_DOWN_1 | unsigned long | GRD- Diagnose fett zu mager Bank 1 (Denominator)(A2L-Name: rbm_stat_GRD_R2L_LS_DOWN_1.ctr_cdn_rbm) CTR_CDN_RBM_SWT_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_PUC_LS_DOWN_1 | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_PUC_LS_DOWN_1.ctr_comp_rbm) CTR_COMP_RBM_PUC_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_PUC_LS_DOWN_1 | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_PUC_LS_DOWN_1.ctr_cdn_rbm) CTR_CDN_RBM_PUC_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_PUE_LS_DOWN_1 | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_PUE_LS_DOWN_1.ctr_comp_rbm) CTR_COMP_RBM_PUE_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_PUE_LS_DOWN_1 | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_PUE_LS_DOWN_1.ctr_cdn_rbm) CTR_CDN_RBM_PUE_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_DLY_L2R_LS_DOWN_1 | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_DLY_L2R_LS_DOWN_1.ctr_comp_rbm) CTR_COMP_RBM_DLY_L2R_LS_DOWN_1_(MST)   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_DLY_L2R_LS_DOWN_1 | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_DLY_L2R_LS_DOWN_1.ctr_cdn_rbm) CTR_CDN_RBM_DLY_L2R_LS_DOWN_1_(MST)   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_DLY_R2L_LS_DOWN_1 | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_DLY_R2L_LS_DOWN_1.ctr_comp_rbm) CTR_COMP_RBM_DLY_R2L_LS_DOWN_1_(MST)   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_DLY_R2L_LS_DOWN_1 | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_DLY_R2L_LS_DOWN_1.ctr_cdn_rbm) CTR_CDN_RBM_DLY_R2L_LS_DOWN_1_(MST)   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_PEAK_MAX_LS_DOWN_1 | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_PEAK_MAX_LS_DOWN_1.ctr_comp_rbm) CTR_COMP_RBM_PEAK_MAX_LS_DOWN_1_(MST)   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_PEAK_MAX_LS_DOWN_1 | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_PEAK_MAX_LS_DOWN_1.ctr_cdn_rbm) CTR_CDN_RBM_PEAK_MAX_LS_DOWN_1_(MST)   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_PEAK_MIN_LS_DOWN_1 | unsigned long | Monitor individual numerator: Number of DC with monitor done since first power up (A2L-Name: rbm_stat_PEAK_MIN_LS_DOWN_1.ctr_comp_rbm) CTR_COMP_RBM_PEAK_MIN_LS_DOWN_1_(MST)   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_PEAK_MIN_LS_DOWN_1 | unsigned long | Monitor individual denominator: Number of DC with convenient vehicle operation for monitor since first power up (A2L-Name: rbm_stat_PEAK_MIN_LS_DOWN_1.ctr_cdn_rbm) CTR_CDN_RBM_PEAK_MIN_LS_DOWN_1_(MST)   Min: 0 Max: 65535 |
| STAT_CTR_COMP_OPF_PFLT_T | unsigned long | Diagnose Temperatur-Basierte Partikelfilter Diagnose Numerator 2BYTE_DUMMY |
| STAT_CTR_CND_OPF_PFLT_T | unsigned long | Diagnose Temperatur-Basierte Partikelfilter Diagnose Denominator 2BYTE_DUMMY |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-aep-i12-zyknl-infospeicher-loeschen"></a>
### START_AEP_I12_ZYKNL_INFOSPEICHER_LOESCHEN

Löschen des Historienspeichers für die letzen 4 Ladevorgänge der 12V-Batterie aus der Hochvolt-Batterie AEP_I12_ZYKNL_INFOSPEICHER_LOESCHEN (0x31 01 AE02)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-p"></a>
### STEUERN_DMTL_P

0x2F60CC03 STEUERN_DMTL_P Diagnosemodul-Tank Leckage Pumpe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTL_P_WERT | unsigned long | Sollwert Diagnosemodul-Tank Leckage Pumpe LV_ACT_DMTL_PUMP_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_DMTL_P_WERT | unsigned long | Timeout Diagnosemodul-Tank Leckage Pumpe 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-tev"></a>
### STATUS_SYSTEMCHECK_TEV

0x3103F022 STATUS_SYSTEMCHECK_TEV Auslesen Diagnosefunktion Tankentlueftungsventil Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1_TEXT | string | Funktionsstatus Diagnosefunktion Tankentlueftungsventil STATE_EOL_KWP_CPS   Min: 0 Max: 9 |
| STAT_DIAGNOSE_1_WERT | int | Funktionsstatus Diagnosefunktion Tankentlueftungsventil STATE_EOL_KWP_CPS   Min: 0 Max: 9 |
| STAT_DIAGNOSE_2_TEXT | string | Status Diagnosefunktion Tankentlueftungsventil STATE_DIAGCPS   Min: 0 Max: 5 |
| STAT_DIAGNOSE_2_WERT | int | Status Diagnosefunktion Tankentlueftungsventil STATE_DIAGCPS   Min: 0 Max: 5 |
| STAT_SYSTEMCHECK_TEV_FUNC_1_WERT | unsigned long | Number of diagnoses if EOL-Test is active - Functional check CPS (A2L-Name: sum_diag_diagcps_eol) SUM_DIAG_DIAGCPS_EOL   Einheit: cyc   Min: 0 Max: 255 |
| STAT_SYSTEMCHECK_TEV_FUNC_1_EINH | string | cyc |
| STAT_SYSTEMCHECK_TEV_FUNC_2_WERT | unsigned long | Number of step 2 loops which have been passed if EOL-Test is active - fuctional check CPS (A2L-Name: sum_flow_sp_diagcps_eol) SUM_FLOW_SP_DIAGCPS_EOL   Einheit: cyc   Min: 0 Max: 255 |
| STAT_SYSTEMCHECK_TEV_FUNC_2_EINH | string | cyc |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-v"></a>
### STEUERN_DMTL_V

0x2F60CD03 STEUERN_DMTL_V Diagnosemodul-Tank Leckage Ventil ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTL_V_WERT | unsigned long | Sollwert Diagnosemodul-Tank Leckage Ventil LV_ACT_DMTLS_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_DMTL_V_WERT | unsigned long | Timeout Diagnosemodul-Tank Leckage Ventil 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-eisygd"></a>
### STATUS_EISYGD

0x3103F0E1 STATUS_EISYGD Auslesen Eisy-Adaptionswerte (gedrosselt) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_EISYGD_TEXT | string | FUNKTIONSSTATUS EISYGD B_MAREGDK_AD   Min: 0 Max: 1 |
| STAT_FS_EISYGD_WERT | int | FUNKTIONSSTATUS EISYGD B_MAREGDK_AD   Min: 0 Max: 1 |
| STAT_MRNN_TEST_DK_WERT | real | Massenstromregler-Adaptionswert NN im GD - Betrieb ueber Test gelesen MRNN_TEST_DK   Min: -1 Max: 0.999969482421875 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-eml"></a>
### STEUERN_EML

0x2F60D603 STEUERN_EML EML (Engine Malfunction Lamp) ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EML_WERT | unsigned long | Sollwert EML (Engine Malfunction Lamp) LV_ACT_WAL_1_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_EML_WERT | unsigned long | Timeout EML (Engine Malfunction Lamp) 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-pm-histogram-reset"></a>
### STEUERN_PM_HISTOGRAM_RESET

$2E 5F F5 04 Loeschen von pminfo1 index 23-30

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG (MEN48) |
| _RESPONSE | binary | Hex-Auftrag an SG (MEN48) |

<a id="job-start-systemcheck-opf"></a>
### START_SYSTEMCHECK_OPF

0x3101F07B START_SYSTEMCHECK_OPF OPF Systemtest   Für Master-Slave Projekte Kopplung der Start Routine über Master notwendig.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-obd-demo-gangeinlegen"></a>
### START_OBD_DEMO_GANGEINLEGEN

0x3101F09D START_OBD_DEMO_GANGEINLEGEN OBD Demo Gangeinlegen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-rbmmode9"></a>
### STATUS_RBMMODE9

0x224026 STATUS_RBMMODE9 Rate Based Monitoring Mode 9 auslesen (Ausgabe der Werte wie im Scantool Mode 9) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OBDCOND | unsigned long | OBD Monitoring Conditions Encountered Counts (general denominator) CTR_CDN_OBD_RBM   Min: 0 Max: 65535 |
| STAT_IGNCNTR | unsigned long | Ignition Counter CTR_IGK_CYC_RBM   Min: 0 Max: 65535 |
| STAT_CATCOMP1 | unsigned long | Catalyst Monitor Completion Counts Bank 1 (Numerator) CTR_COMP_RBM_CAT_DIAG_1   Min: 0 Max: 65535 |
| STAT_CATCOND1 | unsigned long | Catalyst Monitor Conditions Encountered Counts Bank 1 (Denominator) CTR_CDN_RBM_CAT_DIAG_1   Min: 0 Max: 65535 |
| STAT_CATCOMP2 | unsigned long | Catalyst Monitor Completion Counts Bank 2 (Numerator) CTR_COMP_RBM_CAT_DIAG_2   Min: 0 Max: 65535 |
| STAT_CATCOND2 | unsigned long | Catalyst Monitor Conditions Encountered Counts Bank 2 (Denominator) CTR_CDN_RBM_CAT_DIAG_2   Min: 0 Max: 65535 |
| STAT_O2SCOMP1 | unsigned long | O2 Sensor Monitor Completion Counts Bank 1 (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_O2SCOND1 | unsigned long | O2 Sensor Monitor Conditions Encountered Counts Bank 1 (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_O2SCOMP2 | unsigned long | O2 Sensor Monitor Completion Counts Bank 2 (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_O2SCOND2 | unsigned long | O2 Sensor Monitor Conditions Encountered Counts Bank 2 (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_EGRCOMP | unsigned long | EGR Monitor Completion Condition Counts (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_EGRCOND | unsigned long | EGR Monitor Conditions Encountered Counts (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_AIRCOMP | unsigned long | AIR Monitor Completion Condition Counts (Secondary Air) (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_AIRCOND | unsigned long | AIR Monitor Conditions Encountered (Secondary Air) (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_EVAPCOMP | unsigned long | EVAP Monitor Completion Condition Counts (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_EVAPCOND | unsigned long | EVAP Monitor Conditions Encountered Counts (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_O2SDCOMP | unsigned long | O2 Sensor Downstream Monitor Completion Counts Bank 1 (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_O2SDCOND | unsigned long | O2 Sensor Downstream Monitor Conditions Encountered Counts Bank 1 (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_O2SDCOMP2 | unsigned long | O2 Sensor Downstream Monitor Completion Counts Bank 2 (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_O2SDCOND2 | unsigned long | O2 Sensor Downstream Monitor Conditions Encountered Counts Bank 2 (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-typpruefnr"></a>
### STATUS_TYPPRUEFNR

0x224047 STATUS_TYPPRUEFNR Typpruefnummer fuer BN2020-SGs lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TYPPRUEFNUMMER | unsigned long | Typpruefnummer auslesen (a2l:c_typchecknr) 4BYTE in 0 bis 4294967294   Min: 0 Max: 4294967294 |
| STAT_TYPPRUEFNR_HEX_WERT | string | Typpruefnummer auslesen als Hex Wert Einheit: HEX Min: 0.0 Max: 4.294967295E9 |
| STAT_TYPPRUEFNR_HEX_EINH | string | "HEX" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

0x2F60D803 STEUERN_EKP Elektrische Kraftstoffpumpe 1 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EKP1_WERT | real | Tastverhaeltniss Elektrische Kraftstoffpumpe 1 EFPPWM_EXT_ADJ   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_EKP1_WERT | unsigned long | Timeout Elektrische Kraftstoffpumpe 1 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-obd-demo-gangeinlegen"></a>
### STOP_OBD_DEMO_GANGEINLEGEN

0x3102F09D STOP_OBD_DEMO_GANGEINLEGEN OBD Demo Gangeinlegen  beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-kva"></a>
### STEUERN_KVA

0x2E5FC1 STEUERN_KVA KraftstoffVerbrauchsAnzeige - Korrekturfaktor schreiben Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KVA_WERT | real | correction factor for consumption (A2L-Name: fac_fco_kwp) FAC_FCO_KWP   Min: -0.128 Max: 0.127 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-verbredinfo"></a>
### STATUS_VERBREDINFO

0x22401D STATUS_VERBREDINFO Verbraucherreduzierungsspeicher auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_E1_TAG | unsigned long | Ereignis 1 Tag (Verbredinfo[0]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_TAG_EINH | string | Tag |
| STAT_E1_MONAT | unsigned long | Ereignis 1 Monat (Verbredinfo[1]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_MONAT_EINH | string | Monat |
| STAT_E1_DAUER_WERT | unsigned long | Ereignis 1 Dauer der Verbraucherreduzierung (Verbredinfo[2]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E1_DAUER_EINH | string | Minute |
| STAT_E1_LRSA | unsigned long | Ereignis 1 Leistungsreduktionstufe A (Verbredinfo[3]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_LRSA_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse A |
| STAT_E1_LRSB | unsigned long | Ereignis 1 Leistungsreduktionstufe B (Verbredinfo[4]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_LRSB_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse B |
| STAT_E1_WCFA_B0 | unsigned long | Generatordrehzahl in Ordnung |
| STAT_E1_WCFA_B0_TEXT | string | Generatordrehzahl in Ordnung |
| STAT_E1_WCFA_B1 | unsigned long | Bordnetzstrom in Ordnung |
| STAT_E1_WCFA_B1_TEXT | string | Bordnetzstrom in Ordnung |
| STAT_E1_WCFA_B2 | unsigned long | Fahrzeit in Ordnung |
| STAT_E1_WCFA_B2_TEXT | string | Fahrzeit in Ordnung |
| STAT_E1_WCFA_B345 | unsigned long | Fahrzeit in Ordnung |
| STAT_E1_WCFA_B345_TEXT | string | Fahrzeit in Ordnung |
| STAT_E1_WCFB_B012 | unsigned long | Mittl. Stromverbrauch |
| STAT_E1_WCFB_B012_TEXT | string | Mittl. Stromverbrauch |
| STAT_E1_WCFB_B345 | unsigned long | Mittl. Fahrzeit |
| STAT_E1_WCFB_B345_TEXT | string | Mittl. Fahrzeit |
| STAT_E2_TAG | unsigned long | Ereignis 2 Tag (Verbredinfo[7]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_TAG_EINH | string | Tag |
| STAT_E2_MONAT | unsigned long | Ereignis 2 Monat (Verbredinfo[8]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_MONAT_EINH | string | Monat |
| STAT_E2_DAUER_WERT | unsigned long | Ereignis 2 Dauer der Verbraucherreduzierung (Verbredinfo[9]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E2_DAUER_EINH | string | Minute |
| STAT_E2_LRSA | unsigned long | Ereignis 2 Leistungsreduktionstufe A (Verbredinfo[10]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_LRSA_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse A |
| STAT_E2_LRSB | unsigned long | Ereignis 2 Leistungsreduktionstufe B (Verbredinfo[11]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_LRSB_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse B |
| STAT_E2_WCFA_B0 | unsigned long | Generatordrehzahl in Ordnung |
| STAT_E2_WCFA_B0_TEXT | string | Generatordrehzahl in Ordnung |
| STAT_E2_WCFA_B1 | unsigned long | Bordnetzstrom in Ordnung |
| STAT_E2_WCFA_B1_TEXT | string | Bordnetzstrom in Ordnung |
| STAT_E2_WCFA_B2 | unsigned long | Fahrzeit in Ordnung |
| STAT_E2_WCFA_B2_TEXT | string | Fahrzeit in Ordnung |
| STAT_E2_WCFA_B345 | unsigned long | Mittl. Generatordrehzahl |
| STAT_E2_WCFA_B345_TEXT | string | Mittl. Generatordrehzahl |
| STAT_E2_WCFB_B012 | unsigned long | Mittl. Stromverbrauch |
| STAT_E2_WCFB_B012_TEXT | string | Mittl. Stromverbrauch |
| STAT_E2_WCFB_B345 | unsigned long | Mittl. Fahrzeit |
| STAT_E2_WCFB_B345_TEXT | string | Mittl. Fahrzeit |
| STAT_E3_TAG | unsigned long | Ereignis 3 Tag (Verbredinfo[14]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_TAG_EINH | string | Tag |
| STAT_E3_MONAT | unsigned long | Ereignis 3 Monat (Verbredinfo[15]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_MONAT_EINH | string | Monat |
| STAT_E3_DAUER_WERT | unsigned long | Ereignis 3 Dauer der Verbraucherreduzierung (Verbredinfo[16]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E3_DAUER_EINH | string | Minute |
| STAT_E3_LRSA | unsigned long | Ereignis 3 Leistungsreduktionstufe A (Verbredinfo[17]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_LRSA_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse A |
| STAT_E3_LRSB | unsigned long | Ereignis 3 Leistungsreduktionstufe B (Verbredinfo[18]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_LRSB_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse B |
| STAT_E3_WCFA_B0 | unsigned long | Generatordrehzahl in Ordnung |
| STAT_E3_WCFA_B0_TEXT | string | Generatordrehzahl in Ordnung |
| STAT_E3_WCFA_B1 | unsigned long | Bordnetzstrom in Ordnung |
| STAT_E3_WCFA_B1_TEXT | string | Bordnetzstrom in Ordnung |
| STAT_E3_WCFA_B2 | unsigned long | Fahrzeit in Ordnung |
| STAT_E3_WCFA_B2_TEXT | string | Fahrzeit in Ordnung |
| STAT_E3_WCFA_B345 | unsigned long | Mittl. Generatordrehzahl |
| STAT_E3_WCFA_B345_TEXT | string | Mittl. Generatordrehzahl |
| STAT_E3_WCFB_B012 | unsigned long | Mittl. Stromverbrauch |
| STAT_E3_WCFB_B012_TEXT | string | Mittl. Stromverbrauch |
| STAT_E3_WCFB_B345 | unsigned long | Mittl. Fahrzeit |
| STAT_E3_WCFB_B345_TEXT | string | Mittl. Fahrzeit |
| STAT_E4_TAG | unsigned long | Ereignis 4 Tag (Verbredinfo[21]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_TAG_EINH | string | Tag |
| STAT_E4_MONAT | unsigned long | Ereignis 4 Monat (Verbredinfo[22]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_MONAT_EINH | string | Monat |
| STAT_E4_DAUER_WERT | unsigned long | Ereignis 4 Dauer der Verbraucherreduzierung (Verbredinfo[23]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E4_DAUER_EINH | string | Minute |
| STAT_E4_LRSA | unsigned long | Ereignis 4 Leistungsreduktionstufe A (Verbredinfo[24]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_LRSA_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse A |
| STAT_E4_LRSB | unsigned long | Ereignis 4 Leistungsreduktionstufe B (Verbredinfo[25]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_LRSB_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse B |
| STAT_E4_WCFA_B0 | unsigned long | Generatordrehzahl in Ordnung |
| STAT_E4_WCFA_B0_TEXT | string | Generatordrehzahl in Ordnung |
| STAT_E4_WCFA_B1 | unsigned long | Bordnetzstrom in Ordnung |
| STAT_E4_WCFA_B1_TEXT | string | Bordnetzstrom in Ordnung |
| STAT_E4_WCFA_B2 | unsigned long | Fahrzeit in Ordnung |
| STAT_E4_WCFA_B2_TEXT | string | Fahrzeit in Ordnung |
| STAT_E4_WCFA_B345 | unsigned long | Mittl. Generatordrehzahl |
| STAT_E4_WCFA_B345_TEXT | string | Mittl. Generatordrehzahl |
| STAT_E4_WCFB_B012 | unsigned long | Mittl. Stromverbrauch |
| STAT_E4_WCFB_B012_TEXT | string | Mittl. Stromverbrauch |
| STAT_E4_WCFB_B345 | unsigned long | Mittl. Fahrzeit |
| STAT_E4_WCFB_B345_TEXT | string | Mittl. Fahrzeit |
| STAT_ANZAHL_SCHLECHTE_LABI_GESAMT | unsigned long | Anzahl erkannter schlechter Ladebilanzen (Verbredinfo[28]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-aep-i12-test-batteryguard"></a>
### _STATUS_AEP_I12_TEST_BATTERYGUARD

Anforderung Aufruf BatteryGuard Call auslesen Startvoraussetzungen: B_kl15 == TRUE. AEP_I12_TEST_BATTERYGUARD (0x31 03 F052)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAG_AEP_BATTERYGUARD | unsigned char | Auslesen aktueller Status von B_batteryguardcalldiag Min: 0.0 Max: 1.0 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-obd-testgroup"></a>
### STEUERN_OBD_TESTGROUP

0x2EF813 Setzen der OBD_TESTGROUP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| OBD_TESTGROUP | string | Testnummer 12 Stellig wird geprüft,bei falscher Länge erfolg ein Abburch Beispielnummer HBMXV02.0B4X |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ugen"></a>
### STEUERN_UGEN

0x2F603203 STEUERN_UGEN Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PHY_UGEN_WERT | real | Spannung Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) V_ALTER_SP_EXT_ADJ   Einheit: V   Min: 0 Max: 6553.5 |
| SW_TO_UGEN_WERT | unsigned long | Timeout Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hist-regenerationsgrund-opf"></a>
### STATUS_HIST_REGENERATIONSGRUND_OPF

0x22411D STATUS_HIST_REGENERATIONSGRUND_OPF Temperaturverteilung des OPF lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HIST_REGGRUND_RUSSMOD_WERT | unsigned long | Regenerationen aus dem Russmodel über Lebenszeit 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_HIST_REGGRUND_FAHRDIST_WERT | unsigned long | Regenerationen aus Fahrdistanz über Lebenszeit 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_HIST_REGGRUND_MOTOR_AN_WERT | unsigned long | Regenerationen aus Motorlaufzeit über Lebenszeit 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_HIST_REGGRUND_KRAFTSTOFFVERBRAUCH_WERT | unsigned long | Regenerationen aus Kraftstoffverbrauch über Lebenszeit 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_HIST_REGGRUND_MOTORSTART_WERT | unsigned long | Regenerationen aus Motorstarts über Lebenszeit 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_HIST_REGGRUND_DRUCKFALL_WERT | unsigned long | Regenerationen aus Druckabfaellen über Lebenszeit 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_HIST_REGGRUND_FAHRPROFIL_WERT | unsigned long | Regenerationen aus dem Fahrprofil über Lebenszeit 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_HIST_REGGRUND_DRINGLKTSVERST_KALIB_WERT | unsigned long | Regeneration aus Dringlichkeitverstellung per Tester bzw. per Kalibrierung 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_HIST_REGGRUND_DRINGLKT_SCHIEFLAGE_WERT | unsigned long | Regeneration aus Dringlichkeitverstellung über erkannte Schieflage zwischen den Einzelbaenken der Partikelfilter 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-enws"></a>
### STEUERN_ENDE_ENWS

0x2F60ED00 STEUERN_ENDE_ENWS Vanos Einlass Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-batterietausch-registrieren"></a>
### STEUERN_BATTERIETAUSCH_REGISTRIEREN

UDS $31 01 F030 Batterietausch registrieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG (MEN48) |
| _RESPONSE | binary | Hex-Auftrag an SG (MEN48) |

<a id="job-steuern-ram"></a>
### STEUERN_RAM

0x3101F0F2 STEUERN_RAM Ansteuern RAM Backup zwangssichern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-sek-luft"></a>
### STOP_SYSTEMCHECK_SEK_LUFT

0x3102F020 STOP_SYSTEMCHECK_SEK_LUFT Diagnosefunktion Sekundaerluft beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

0x2F60CF03 STEUERN_TEV Tankentlueftungsventil ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_TEV_WERT | real | Tastverhaeltniss Tankentlueftungsventil CPPWM_EXT_ADJ   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_TEV_WERT | unsigned long | Timeout Tankentlueftungsventil 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bzetomsa2"></a>
### STATUS_BZETOMSA2

0x224093 STATUS_BZETOMSA2 Analyse von MSA-Abschaltverhinderern durch BZE3 gegenüber AEPBZE SDG(A2l-NAME=bzetomsa)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INFOSPEICHER_BZE3_MSA_0_2 | unsigned long | BZE3 AV=0, AEP-BZE AV=0 |
| STAT_INFOSPEICHER_BZE3_MSA_0_2_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_3_5 | unsigned long | BZE3 AV=0, AEP-BZE AV=1 |
| STAT_INFOSPEICHER_BZE3_MSA_3_5_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_6_8 | unsigned long | BZE3 AV=1, AEP-BZE AV=0 |
| STAT_INFOSPEICHER_BZE3_MSA_6_8_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_9_11 | unsigned long | BZE3 AV=1, AEP-BZE AV=1 |
| STAT_INFOSPEICHER_BZE3_MSA_9_11_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_12 | unsigned long | Zähler |
| STAT_INFOSPEICHER_BZE3_MSA_12_EINH | string | dimensionslos |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bzetomsa"></a>
### STATUS_BZETOMSA

0x224155 STATUS_BZETOMSA Analyse von MSA-Abschaltverhinderern durch BZE3 gegenüber AEPBZE SDG(A2l-NAME=bzetomsa)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INFOSPEICHER_BZE3_MSA_0_2 | unsigned long | BZE3 AV=0, AEP-BZE AV=0 |
| STAT_INFOSPEICHER_BZE3_MSA_0_2_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_3_5 | unsigned long | BZE3 AV=0, AEP-BZE AV=1 |
| STAT_INFOSPEICHER_BZE3_MSA_3_5_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_6_8 | unsigned long | BZE3 AV=1, AEP-BZE AV=0 |
| STAT_INFOSPEICHER_BZE3_MSA_6_8_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_9_11 | unsigned long | BZE3 AV=1, AEP-BZE AV=1 |
| STAT_INFOSPEICHER_BZE3_MSA_9_11_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_12 | unsigned long | Zähler |
| STAT_INFOSPEICHER_BZE3_MSA_12_EINH | string | dimensionslos |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lds1"></a>
### STEUERN_ENDE_LDS1

0x2F60B600 STEUERN_ENDE_LDS1 Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-tev-regelung-aus"></a>
### STATUS_TEV_REGELUNG_AUS

0x3103F0CF STATUS_TEV_REGELUNG_AUS Deaktivierung TEV-Regelung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LV_LAM_AD_ENA | unsigned long | Lambda Adaption möglich(A2L-Name: lv_lam_ad_ena) LV_LAM_AD_ENA   Min: 0 Max: 1 |
| STAT_LV_LAM_AD_END | unsigned long | LAmda Adaption temporaer beendet (A2L-Name: lv_lam_ad_end) LV_LAM_AD_END   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-llabg-prog"></a>
### STEUERN_LLABG_PROG

0x2E5FF008 STEUERN_LLABG_PROG Abgleichwert LL (Leerlauf) programmieren Aktivierung: Klemme 15 = EIN UND Leerlaufabgleich ueber Testervorgabe = EIN Activation: LV_IGK = 1 UND LV_KWP_ENA = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_OFS_ACC_DRI_IN_WERT | long | Abgleichswert LL mit Klima und Fahrbedingung N_KWP_OFS_ACC_DRI_KWP   Einheit: rpm   Min: -256 Max: 254 |
| SW_OFS_DRI_IN_WERT | long | Abgleichswert LL mit Fahrstufe N_KWP_OFS_DRI_KWP   Einheit: rpm   Min: -256 Max: 254 |
| SW_OFS_IN_WERT | long | Abgleichswert LL N_KWP_OFS_KWP   Einheit: rpm   Min: -256 Max: 254 |
| SW_OFS_ACC_IN_WERT | long | Abgleichswert LL mit Klimaanlage N_KWP_OFS_ACC_KWP   Einheit: rpm   Min: -256 Max: 254 |
| SW_OFS_VB_IN_WERT | long | Abgleichswert LL mit niedriger Batteriespannung N_KWP_OFS_VB_KWP   Einheit: rpm   Min: -256 Max: 254 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ibs-strommessung"></a>
### STEUERN_IBS_STROMMESSUNG

Ansteuern IBS Strommessung UDS: $31 RoutineControl

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHWELLE_WERT | real | Bereich: 0 - 1310.7 A (A2L_Name: Eco_i_schwelle) |
| HOLDOFF_WERT | real | Bereich: 0 - 2.55 s (A2L_Name: Eco_i_holdoff) |
| MESSZEIT_WERT | real | Bereich: 0 - 0.51 s (A2L_Name: Eco_i_messzeit) |
| TIMEOUT_WERT | real | Bereich: 0 - 25.5 s (A2L_Name: Eco_i_timeout) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-opf-tausch-bank1"></a>
### STATUS_OPF_TAUSCH_BANK1

0x224195 STATUS_OPF_TAUSCH_BANK1 Nutzung  des OPF lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZ_OPF_TAUSCH_WERT | unsigned long | Anzahl getauschter OPF 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM_ST_AKT_OPF_TAUSCH_WERT | unsigned long | Km Stand der letzten Tauschaktion 4BYTE in 0 bis 4294967294   Min: 0 Max: 4294967294 |
| STAT_ANZ_GEF_OPF_TAUSCH | unsigned long | Anzahl geforderter OPF-Tausch 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-heizung"></a>
### STEUERN_DMTL_HEIZUNG

0x2F60CE03 STEUERN_DMTL_HEIZUNG Diagnosemodul-Tank Leckage Heizung ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTLH_WERT | unsigned long | Sollwert Diagnosemodul-Tank Leckage Heizung LV_ACT_DMTLH_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_DMTLH_WERT | unsigned long | Timeout Diagnosemodul-Tank Leckage Heizung 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-opf-druckschlauchabfall"></a>
### START_OPF_DRUCKSCHLAUCHABFALL

0x3101F09F START_OPF_DRUCKSCHLAUCHABFALL Diagnosefunktion OPF Druckschlauchabfall   (Für Master-Slave Projekte Kopplung der Start Routine über Master notwendig.)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bzediag2"></a>
### STATUS_BZEDIAG2

Auslesen Infospeicher Batteriezustandserkennung 2 UDS*: $22 ReadDataByIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENTLADUNG_MSA_BEREICH1 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 1) |
| STAT_ENTLADUNG_MSA_BEREICH2 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 2) |
| STAT_ENTLADUNG_MSA_BEREICH3 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 3) |
| STAT_ENTLADUNG_MSA_BEREICH4 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 4) |
| STAT_ENTLADUNG_MSA_BEREICH5 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 5) |
| STAT_ENTLADUNG_MSA_BEREICH6 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 6) |
| STAT_ENTLADUNG_MSA_BEREICH7 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 7) |
| STAT_ENTLADUNG_MSA_BEREICH8 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 8) |
| STAT_TIEFENTLADUNG_AKTUELL | real | Index für Schädigungsgrad der aktuellen Tiefentladung |
| STAT_TIEFENTLADUNG_GESAMT | real | Index für den Schädigungsgrad aller Tiefentladungen |
| STAT_SOH_CIST | real | Alterungsindex auf Basis C_ist |
| STAT_SOH_WASSERVERLUST | real | Alterungsindex auf Basis Qv_h2o_zg |
| STAT_SOH_STANDZEIT | real | Alterungsindex auf Basis Bzd_sulfind |
| STAT_SOH_ZYKLEN | real | Alterungsindex auf Basis SoC-abhängiger Zyklenzähler |
| STAT_SOH_ENTLADUNG_STAND | real | Alterungsindex auf Basis Entladehistogramm im Stand |
| STAT_SOH_LADUNG_FAHRT | real | Alterungsindex auf Basis Ladehistogramm während der Fahrt |
| STAT_SOH_ENTLADUNG_MSA | real | Alterungsindex auf Basis Entladehistogramm im MSA-Stopp |
| STAT_SOH_TIEFENTLADUNG | real | Alterungsindex auf Basis Bzd_tiefentlabs |
| STAT_SOH_BATTERIE | real | Index für den aktuellen Alterungszustand der Batterie (SoH) |
| STAT_VOLLZYKLEN_GEWICHTET | real | Vollzyklenzähler der Batterie. Entladung wird je nach SoC gewichtet |
| STAT_ENTLADUNG_GEWICHTET_WERT | real | gewichteter Entladezähler abhängig vom SoC |
| STAT_ENTLADUNG_GEWICHTET_EINH | string | Einheit des gewichteten Entladezählers (Ah) |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-stop-systemcheck-l-regelung-aus"></a>
### STOP_SYSTEMCHECK_L_REGELUNG_AUS

0x3102F0D9 STOP_SYSTEMCHECK_L_REGELUNG_AUS Ende Lambdaregelung ausschalten Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cbsmotoroelhist"></a>
### STATUS_CBSMOTOROELHIST

0x22404F STATUS_CBSMOTOROELHIST CBS Motoroel Historien-Funktion lesen (FASTA)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OZ_KVBMW_WERT | real | Mittelwert Kraftstoffverbrauch (A2L-Name: Oz_kvbmw) OZ_KVBMW   Min: 0 Max: 100 |
| STAT_COZ_KMVERBR_WERT | unsigned long | Gefahrene Strecke fuer Coz_kvbverbrabs (A2L-Name: Coz_kmverbr) COZ_KMVERBR   Einheit: km   Min: 0 Max: 4294967295 |
| STAT_COZ_KMVERBR_EINH | string | km |
| STAT_COZ_KVBVERBRABS_WERT | real | Absolute verbrauchte Kraftstoffmenge (A2L-Name: Coz_kvbverbrabs) COZ_KVBVERBRABS   Einheit: l   Min: 0 Max: 42949672.95 |
| STAT_COZ_KVBVERBRABS_EINH | string | l |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-serviceregeneration-opf"></a>
### STATUS_SERVICEREGENERATION_OPF

0x22419A STATUS_SERVICEREGENERATION_OPF Nutzung  des OPF lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KM_STAND_BEG_REG | unsigned long | KM Stand bei Begin der Regeneration OPF 4BYTE in 0 bis 4294967294   Min: 0 Max: 4294967294 |
| STAT_BETRIEBSZEIT_BEG_REG_WERT | unsigned long | Betriebszeit bei Begin der Regeneration OPF 4BYTE in 0 bis 4294967294s   Einheit: s   Min: 0 Max: 4294967294 |
| STAT_BETRIEBSZEIT_BEG_REG_EINH | string | second |
| STAT_DAUER_REG_WERT | unsigned long | Dauer der Regeneration OPF 2BYTE_IN_0_BIS_6553_KOMMA_5_s   Einheit: s |
| STAT_DAUER_REG_EINH | string | second |
| STAT_MOD_RUSSBELADUNG_WERT | unsigned long | Modellwert Russbeladung bei Start der Regeneration 2BYTE_IN_0_BIS_65_KOMMA_535_g |
| STAT_MOD_ASCHEBELADUNG | unsigned long | Modellwert Aschebeladung bei Start der Regeneration 2BYTE_IN_0_BIS_65_KOMMA_535_g |
| STAT_REG_BEDARF_WERT | unsigned long | Dringlichkeit der Regeneration 1BYTE_in_0bis255prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_REG_BEDARF_WERT_EINH | string | percent |
| STAT_REG_GRUND | unsigned long | Grund der Regeneration 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_REG_FORTSCHRITT_WERT | unsigned long | Fortschritt der Regeneration 1BYTE_in_0bis255prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_REG_FORTSCHRITT_EINH | string | percent |
| STAT_MAX_TEMP_REG_WERT | long | Maximaltemperatur im OPF bei dieser Regeneration 2BYTE_IN_MINUS_3276_BIS_3276_GRAD_CELSIUS   Einheit: ° C |
| STAT_MAX_TEMP_REG_EINH | string | degree_C |
| STAT_GRUND_ABBRUCH | unsigned long | Grund für Regenerationsende 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bzediag"></a>
### STATUS_BZEDIAG

0x22403B STATUS_BZEDIAG BZE Infospeicher

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIEKAPAZITAET_AKTUEL_WERT | unsigned long | aktueller Wert C_ist (verfügbare Kapazität) - auf passende Quantisierung angepasst 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_AKTUEL_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_1_MONAT_WERT | unsigned long | C_ist vor 1 Zeiteinheit 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_1_MONAT_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_2_MONAT_WERT | unsigned long | C_ist vor 2 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_2_MONAT_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_3_MONAT_WERT | unsigned long | C_ist vor 3 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_3_MONAT_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_4_MONAT_WERT | unsigned long | C_ist vor 4 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_4_MONAT_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_5_MONAT_WERT | unsigned long | C_ist vor 5 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_5_MONAT_EINH | string | Ah |
| STAT_Q_BATTERIEKAPAZITAET_AKTUEL_WERT | real | Qualitaetsindex C_ist 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_Q_BATTERIEKAPAZITAET_AKTUEL_EINH | string | percent |
| STAT_LADEZUSTAND_AKTUELL_WERT | unsigned long | Aktueller Wert C_akt (Ladezustand)- auf passende Quantisierung angepasst 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_AKTUELL_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_1_TAG_WERT | unsigned long | C_akt vor 1 Zeiteinheit 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_1_TAG_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_2_TAG_WERT | unsigned long | C_akt vor 2 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_2_TAG_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_3_TAG_WERT | unsigned long | C_akt vor 3 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_3_TAG_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_4_TAG_WERT | unsigned long | C_akt vor 4 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_4_TAG_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_5_TAG_WERT | unsigned long | C_akt vor 5 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_5_TAG_EINH | string | Ah |
| STAT_Q_LADEZUSTAND_AKTUELL_WERT | real | Qualitaetsindex C_akt 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_Q_LADEZUSTAND_AKTUELL_EINH | string | percent |
| STAT_STROMAUFNAHME_AKTUELL_WERT | unsigned long | nominierte Stromaufnahme aktuell 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_AKTUELL_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_1_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 1 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_1_MONAT_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_2_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 2 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_2_MONAT_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_3_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 3 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_3_MONAT_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_4_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 4 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_4_MONAT_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_5_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 5 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_5_MONAT_EINH | string | A |
| STAT_Q_STROMAUFNAHME_AKTUELL_WERT | real | Qualitaetsindex normierte Stromaufnahme 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_Q_STROMAUFNAHME_AKTUELL_EINH | string | A |
| STAT_Q_BATTERIEZELLE_DEFEKT_WERT | real | Zelldefekt-Signal als Quali-Index 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_Q_BATTERIEZELLE_DEFEKT_EINH | string | percent |
| STAT_ANZ_BATTERIEWECHSEL | unsigned long | Anzahl der bisher getaetigten Batteriewechsel (0 = Originalbatterie) 4BIT_in_0bis15   Min: 0 Max: 15 |
| STAT_LETZTER_BATTERIEWECHSEL_TEXT | string | Anzeige, ob unzulaessiger Batteriewechsel durchgefuehrt wurde (C_nenn wird kleiner, oder AGM --) Nass) B_bzd_wrgbat |
| STAT_LETZTER_BATTERIEWECHSEL_WERT | int | Anzeige, ob unzulaessiger Batteriewechsel durchgefuehrt wurde (C_nenn wird kleiner, oder AGM --) Nass) |
| STAT_LETZTER_BATTERIEWECHSEL_EINH | string | - B_bzd_wrgbat |
| STAT_BATTERIEZUSTAND_TEXT | string | Zustand der Batterie / Tauschempfehlung Bzd_btzust |
| STAT_BATTERIEZUSTAND_WERT | int | Zustand der Batterie / Tauschempfehlung |
| STAT_BATTERIEZUSTAND_EINH | string | - Bzd_btzust |
| STAT_WASSERVERLUST_TEXT | string | Anzeige Wasserverlust ueberschreitet Grenzwert B_qvch2o |
| STAT_WASSERVERLUST_WERT | int | Anzeige Wasserverlust ueberschreitet Grenzwert |
| STAT_WASSERVERLUST_EINH | string | - B_qvch2o |
| STAT_TIEFENTLADUNG_TEXT | string | Anzeige Batterie wurde tiefentladen B_bzd_te |
| STAT_TIEFENTLADUNG_WERT | int | Anzeige Batterie wurde tiefentladen |
| STAT_TIEFENTLADUNG_EINH | string | - B_bzd_te |
| STAT_IBS_BZE_TEXT | string | Gibt an, ob eine IBS mit BZE3 erkannt wurde und die BZE-Daten somit relevant sind. B_bzdon |
| STAT_IBS_BZE_WERT | int | Gibt an, ob eine IBS mit BZE3 erkannt wurde und die BZE-Daten somit relevant sind. B_bzdon |
| STAT_IBS_BZE_EINH | string | - |
| STAT_PROGNOSE_KALTSTART_SOMMER_U_WERT | real | Praedizierter Klemmspannungswert Kaltstart Sommer Bze_pu   Einheit: V   Min: 0 Max: 25.5 |
| STAT_PROGNOSE_KALTSTART_SOMMER_U_EINH | string | V |
| STAT_PROGNOSE_KALTSTART_WINTER_U_WERT | real | Praedizierter Klemmspannungswert Kaltstart Winter Bze_pu   Einheit: V   Min: 0 Max: 25.5 |
| STAT_PROGNOSE_KALTSTART_WINTER_U_EINH | string | V |
| STAT_PROGNOSE_WARMSTART_U_WERT | real | Praedizierter Klemmspannungswert Warmstart Bze_pu   Einheit: V   Min: 0 Max: 25.5 |
| STAT_PROGNOSE_WARMSTART_U_EINH | string | V |
| STAT_PROGNOSE_WARMSTART_VORHALT_WERT | real | Vorhalt praedizierter Klemmspannungswert Warmstart Sommer/Winter Bze_pu   Einheit: V   Min: 0 Max: 25.5 |
| STAT_PROGNOSE_WARMSTART_VORHALT_EINH | string | V |
| STAT_R_BATTERIE_INITIAL_WERT | real | Initialer Innenwiderstand der Fzg.-Batterie nach Einbau / Tausch Bze_rbatt   Einheit: mOhm   Min: 0 Max: 25.5 |
| STAT_R_BATTERIE_INITIAL_EINH | string | mOhm |
| STAT_R_BATTERIE_AKTUELL_WERT | real | aktueller Innenwiderstand der Fzg.-Batterie Bze_rbatt   Einheit: mOhm   Min: 0 Max: 25.5 |
| STAT_R_BATTERIE_AKTUELL_EINH | string | mOhm |
| STAT_TREND_WARMSTART_U_WERT | real | Trendwert Klemmspannungsprognose Warmstart Bzd_wcstrend   Einheit: V   Min: -8 Max: 7.9375 |
| STAT_TREND_WARMSTART_U_EINH | string | V |
| STAT_TREND_WARMSTART_SOWI_U_WERT | real | Vorhalt Trendwert Klemmspannungsprognose Warmstart Sommer/Winter Bzd_wcwtrend   Einheit: V   Min: -8 Max: 7.9375 |
| STAT_TREND_WARMSTART_SOWI_U_EINH | string | V |
| STAT_BATTERIETEMPERATUR_MIN_AKTUELL_WERT | real | Klimaprofil: Wert vor 0 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_AKTUELL_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_1_MONAT_WERT | real | Klimaprofil: Wert vor 1 Monat Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_1_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_2_MONAT_WERT | real | Klimaprofil: Wert vor 2 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_2_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_3_MONAT_WERT | real | Klimaprofil: Wert vor 3 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_3_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_4_MONAT_WERT | real | Klimaprofil: Wert vor 4 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_4_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_5_MONAT_WERT | real | Klimaprofil: Wert vor 5 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_5_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_6_MONAT_WERT | real | Klimaprofil: Wert vor 6 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_6_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_7_MONAT_WERT | real | Klimaprofil: Wert vor 7 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_7_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_8_MONAT_WERT | real | Klimaprofil: Wert vor 8 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_8_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_9_MONAT_WERT | real | Klimaprofil: Wert vor 9 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_9_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_10_MONAT_WERT | real | Klimaprofil: Wert vor 10 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_10_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_11_MONAT_WERT | real | Klimaprofil: Wert vor 11 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_11_MONAT_EINH | string | degreeC |
| STAT_WASSERVERLUSTABS_WERT | real | Wasserverlust Qv_h2o_zg   Einheit: g/Ah   Min: 0 Max: 10 |
| STAT_WASSERVERLUSTABS_EINH | string | grammPerAmpereHour |
| STAT_STANDZEIT_LADEZUSTAND_NIEDRIG_AKTUELL | unsigned long | Vorhalt Sulfatierungsindex (Summe) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_STANDZEIT_LADEZUSTAND_NIEDRIG_GESAMT | unsigned long | Vorhalt Sulfatierungsrate 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIEKAPAZITAET_WERT | unsigned long | Absolutzeit juengster Historieneintrag C_ist 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIEKAPAZITAET_EINH | string | d |
| STAT_ZEIT_LETZTER_EINTRAG_LADEZUSTAND_WERT | unsigned long | Absolutzeit juengster Historieneintrag C_akt 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_LADEZUSTAND_EINH | string | d |
| STAT_ZEIT_LETZTER_EINTRAG_STROMAUFNAHME_WERT | unsigned long | Absolutzeit juengster Historieneintrag nominierte Stromaufnahme 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_STROMAUFNAHME_EINH | string | d |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIETEMPERATUR_WERT | unsigned long | Absolutzeit juengster Historieneintrag Klima 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIETEMPERATUR_EINH | string | d |
| STAT_ZEIT_LETZTE_TRENDWERTERMITTLUNG_WERT | unsigned long | Absolutzeit letzte Trendwertermittlung 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTE_TRENDWERTERMITTLUNG_EINH | string | d |
| STAT_ZEIT_SEIT_LETZTEM_BATTERIEWECHSEL_WERT | unsigned long | Zeit seit letztem Batterietausch 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_SEIT_LETZTEM_BATTERIEWECHSEL_EINH | string | d |
| STAT_ENTLADUNG_MOTOR_AUS_KLEINER_MINUS10AH_WERT | unsigned long | Entladung waehrend Motor aus &lt; -10Ah (Ladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_KLEINER_MINUS10AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_MINUS10AH_BIS_0AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen -10Ah und 0Ah (Ladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_MINUS10AH_BIS_0AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_0AH_BIS_5AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 0Ah und 5Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_0AH_BIS_5AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_5AH_BIS_10AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 5Ah und 10Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_5AH_BIS_10AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_10AH_BIS_15AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 10Ah und 15Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_10AH_BIS_15AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_15AH_BIS_25AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 15Ah und 25Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_15AH_BIS_25AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_25AH_BIS_50AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 25Ah und 50Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_25AH_BIS_50AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_GROESSER_50AH_WERT | unsigned long | Entladung waehrend Motor aus &gt; 50Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_GROESSER_50AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_KLEINER_MINUS20AH_WERT | unsigned long | Ladung waehrend Motor ein &lt; -20Ah (Entladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_KLEINER_MINUS20AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_MINUS20AH_BIS_MINUS10AH_WERT | unsigned long | Ladung waehrend Motor ein zwischen -20Ah und -10Ah (Entladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_MINUS20AH_BIS_MINUS10AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_MINUS10AH_BIS_0AH_WERT | unsigned long | Ladung waehrend Motor ein zwischen -10Ah und 0Ah (Entladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_MINUS10AH_BIS_0AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_0AH_BIS_10AH_WERT | unsigned long | Ladung waehrend Motor ein zwischen 0Ah und 10Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_0AH_BIS_10AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_10AH_BIS_20AH_WERT | unsigned long | Ladung waehrend Motor ein zwischen 10Ah und 20Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_10AH_BIS_20AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_GROESSER_20AH_WERT | unsigned long | Ladung waehrend Motor ein &gt; 20Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_GROESSER_20AH_EINH | string | Ah |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-calcvn"></a>
### STATUS_CALCVN

Cal-ID (Calibration-ID) und CVN(Calibration Verification Number) auslesen. CALCVN (0x403C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CALID_WERT | string | Cal-ID auslesen (hier muss die Cal-ID wie bei Mode $09 (PID $04) ausgegeben werden) |
| STAT_CVN_WERT | unsigned long | CVN auslesen (hier muss die CVN wie bei Mode $09 (PID $06) ausgegeben werden) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-pm-restore"></a>
### STEUERN_PM_RESTORE

0x2E5F8B STEUERN_PM_RESTORE Schreiben PM-Restore Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PMRESTORE_0_WERT | unsigned long | PM-Restore Byte 0 PMRESTORE[0]   Min: 0 Max: 255 |
| SW_PMRESTORE_1_WERT | unsigned long | PM-Restore Byte 1 PMRESTORE[1]   Min: 0 Max: 3 |
| SW_PMRESTORE_2_WERT | unsigned long | PM-Restore Byte 2 PMRESTORE[2]   Min: 0 Max: 255 |
| SW_PMRESTORE_3_WERT | unsigned long | PM-Restore Byte 3 PMRESTORE[3]   Min: 0 Max: 3 |
| SW_PMRESTORE_4_WERT | unsigned long | PM-Restore Byte 4 PMRESTORE[4]   Min: 0 Max: 255 |
| SW_PMRESTORE_5_WERT | unsigned long | PM-Restore Byte 5 PMRESTORE[5]   Min: 0 Max: 3 |
| SW_PMRESTORE_6_WERT | unsigned long | PM-Restore Byte 6 PMRESTORE[6]   Min: 0 Max: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ll-abgleich"></a>
### STEUERN_LL_ABGLEICH

0x2E5FF007 STEUERN_LL_ABGLEICH Abgleichwert LL (Leerlauf) vorgeben Aktivierung: Klemme 15 = EIN UND Leerlaufabgleich ueber Testervorgabe = EIN Activation: LV_IGK = 1 UND LV_KWP_ENA = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_OFS_ACC_DRI_IN_WERT | long | Abgleichswert LL mit Klima und Fahrbedingung N_KWP_OFS_ACC_DRI_KWP   Einheit: rpm   Min: -256 Max: 254 |
| SW_OFS_DRI_IN_WERT | long | Abgleichswert LL mit Fahrstufe N_KWP_OFS_DRI_KWP   Einheit: rpm   Min: -256 Max: 254 |
| SW_OFS_IN_WERT | long | Abgleichswert LL N_KWP_OFS_KWP   Einheit: rpm   Min: -256 Max: 254 |
| SW_OFS_ACC_IN_WERT | long | Abgleichswert LL mit Klimaanlage N_KWP_OFS_ACC_KWP   Einheit: rpm   Min: -256 Max: 254 |
| SW_OFS_VB_IN_WERT | long | Abgleichswert LL mit niedriger Batteriespannung N_KWP_OFS_VB_KWP   Einheit: rpm   Min: -256 Max: 254 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-krann"></a>
### STATUS_KRANN

0x3103F0E3 STATUS_KRANN Auslesen Krann-Adaptionswerte Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KRNN_TEST_WERT | real | Zuendwinkelaenderung aus Adaption Klopfregelung fuer Testerabfrage KRNN_TEST   Einheit: Grad   Min: -50 Max: 60 |
| STAT_KRNN_TEST_EINH | string | degree |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-tev"></a>
### STOP_SYSTEMCHECK_TEV

0x3102F022 STOP_SYSTEMCHECK_TEV Diagnosefunktion Tankentlueftungsventil beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-pm-backup"></a>
### STATUS_PM_BACKUP

0x225F8B STATUS_PM_BACKUP Auslesen des PM-Backup Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PMBACKUP_0 | unsigned long | PM-Backup Byte 0 PMBACKUP[0]   Min: 0 Max: 255 |
| STAT_PMBACKUP_1 | unsigned long | PM-Backup Byte 1 PMBACKUP[1]   Min: 0 Max: 3 |
| STAT_PMBACKUP_2 | unsigned long | PM-Backup Byte 2 PMBACKUP[2]   Min: 0 Max: 255 |
| STAT_PMBACKUP_3 | unsigned long | PM-Backup Byte 3 PMBACKUP[3]   Min: 0 Max: 3 |
| STAT_PMBACKUP_4 | unsigned long | PM-Backup Byte 4 PMBACKUP[4]   Min: 0 Max: 255 |
| STAT_PMBACKUP_5 | unsigned long | PM-Backup Byte 5 PMBACKUP[5]   Min: 0 Max: 3 |
| STAT_PMBACKUP_6 | unsigned long | PM-Backup Byte 6 PMBACKUP[6]   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-nutzung-opf"></a>
### STATUS_NUTZUNG_OPF

0x224119 STATUS_NUTZUNG_OPF Nutzung  des OPF lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZ_REG_SPONTAN_ALLE_WERT | unsigned long | Anzahl aller spontanen Regenerationen 4BYTE in 0 bis 4294967294   Min: 0 Max: 4294967294 |
| STAT_ANZ_REG_SPONTAN_VOLLST_WERT | unsigned long | Anzahl aller spontanen Regenerationen, welche vollstÃ¤ndig durchgelaufen sind 4BYTE in 0 bis 4294967294   Min: 0 Max: 4294967294 |
| STAT_ANZ_REG_AKTIV_ALLE_WERT | unsigned long | Anzahl aller aktiven Regenerationen 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ANZ_REG_AKTIV_VOLLST_WERT | unsigned long | Anzahl aller aktiven Regenerationen, welche vollstÃ¤ndig durchgelaufen sind 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ANZ_LEIST_BEG | unsigned long | Anzahl Leistungsbegrenzungen aufgrund Gegendruck 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZHL_REG_ANF_SERVICE_WERT | unsigned long | Anzahl aller Regenerationsanforderungen die durch Servicetester angefordert worden sind. 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_ZHL_REG_ANF_SERVICE_VOLLST_WERT | unsigned long | Anzahl aller Regenerationsanforderungen die durch Servicetester angefordert worden sind und vollstÃ¤ndig durchgelaufen sind. 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-eisydr"></a>
### STEUERN_EISYDR

0x3101F0E2 STEUERN_EISYDR Ansteuern Eisy-Adaptionswerte mit Druckregelung (Anforderung aus CP5403)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_WERT | long | Drehzahl NKW_SOLL   Einheit: Upm   Min: -32768 Max: 32767 |
| VSE_SPRI_WERT | real | Istwert Einlassspreizung variable NWS VSE_SPRI   Einheit: Grad KW   Min: 0 Max: 6553.5 |
| VSA_SPRI_WERT | real | Istwert Auslassspreizung variable NWS VSA_SPRI   Einheit: Grad KW   Min: 0 Max: 6553.5 |
| WDK_IST_WERT | real | Winkel Drosselklappe WDK_IST   Einheit: %   Min: -800 Max: 799.9755 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-vanosspuelen"></a>
### START_VANOSSPUELEN

0x3101F042 START_VANOSSPUELEN VANOS Spuelen fuer OBD und PVE. 

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VANOSSPL_M_MODUS_WERT | unsigned long | 1=gleichzeitiges Verstellen von Ein- und Auslass-Vanos. und 2=erst Verstellen Einlass, dann Verstellen Auslass. Default-Wert = 1. VANOSSPL_M_MODUS   Min: 1 Max: 2 |
| VANOSSPL_N_AZLVERSTL_WERT | unsigned long | 1 Verstellung bedeutet erst dvse1, dann dvse2 (von 1 bis 50).  Default-Wert = 10 Dez. VANOSSPL_N_AZLVERSTL   Min: 1 Max: 50 |
| VANOSSPL_T_HLTZVERSTL_WERT | real | Haltezeit Verstellung (0 bis 5 s). Default-Wert = 2.1 s.                        Gesamtzeit Vanosspuelen = N * 2 * T * m. T_HLD_CAM_OFS_EXT_ADJ   Einheit: s   Min: 0 Max: 25.5 |
| VANOSSPL_N1_UDZLGRNZ_WERT | unsigned long | Untere Drehzahlgrenze (500 bis 2000 U/min) ca 100 U/min unter LL-Solldrehzahl . Default-Wert = 1000. VANOSSPL_N1_UDZLGRNZ   Einheit: rpm   Min: 500 Max: 2000 |
| VANOSSPL_N2_ODZLGRNZ_WERT | unsigned long | Obere Drehzahlgrenze (500 bis 2000 U/min) ca 100 U/min ueber LL-Solldrehzahl . Default-Wert = 1200. VANOSSPL_N2_ODZLGRNZ   Einheit: rpm   Min: 500 Max: 2000 |
| VANOSSPL_V_MAX_WERT | unsigned long | Max. Fahrzeuggeschwindigkeit (0 bis 100 km/h). Default-Wert = 0 VANOSSPL_V_MAX   Einheit: km/h   Min: 0 Max: 100 |
| VANOSSPL_T2_ZUBRZ_WERT | real | Zulaessige Unterbrechungszeit (0 bis 25,5 s). Default-Wert = 5,1s. T_WAIT_MAX_CAM_OFS_EXT_ADJ   Einheit: s   Min: 0 Max: 25.5 |
| VANOSSPL_DVSE1_VO1EV_WERT | real | Verstelloffset 1 Einlass-Vanos (von -102,4 bis 101,6°KW). Default-Wert=5.6°Grad. VANOSSPL_DVSE1_VO1EV   Einheit: Grad   Min: -102.4 Max: 101.6 |
| VANOSSPL_DVSE2_VO2EV_WERT | real | Verstelloffset 2 Einlass-Vanos (von -102,4 bis 101,6°KW). Default-Wert=-5.6°Grad. VANOSSPL_DVSE2_VO2EV   Einheit: Grad   Min: -102.4 Max: 101.6 |
| VANOSSPL_DVSA1_VO1AV_WERT | real | Verstelloffset 1 Auslas-Vanos (von -102,4 bis 101,6°KW). Default-Wert=-5.6°Grad. VANOSSPL_DVSA1_VO1AV   Einheit: Grad   Min: -102.4 Max: 101.6 |
| VANOSSPL_DVSA2_VO1AV_WERT | real | Verstelloffset 2 Auslas-Vanos (von -102,4 bis 101,6°KW). Default-Wert=5.6°Grad. VANOSSPL_DVSA2_VO1AV   Einheit: Grad   Min: -102 Max: 102 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-eml"></a>
### STEUERN_ENDE_EML

0x2F60D600 STEUERN_ENDE_EML EML (Engine Malfunction Lamp) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-adap-selektiv-loeschen"></a>
### ADAP_SELEKTIV_LOESCHEN

0x3101F030 ADAP_SELEKTIV_LOESCHEN Ansteuern Adaptionen selektiv loeschen Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE_1 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_2 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_3 | int | Bit=1 löscht Bit=0 behält alten Wert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

0x2F60DA03 STEUERN_E_LUEFTER E-Luefter ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Motortemperatur &lt; 95 Grad C UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND TCO &lt; C_TCO_MAX_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ELUE_WERT | real | Tastverhaeltniss E-Luefter ECFPWM_ECF_EXT_ADJ   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_ELUE_WERT | unsigned long | Timeout E-Luefter 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-opf-diag"></a>
### STATUS_OPF_DIAG

0x2240EF STATUS_OPF_DIAG Otto Partikelfilter Verbaudiagnosestatus auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OPF_DIAG_BANK2 | unsigned long | Schlauchabfalldiagnose für Bank 2 ist durchgelaufen 1BYTE_IDENTICAL_BIT2 |
| STAT_OPF_DIAG_AKTIV | unsigned long | Schlauchabfalldiagnose ist aktiv 1BYTE_IDENTICAL_BIT0 |
| STAT_OPF_DIAG_BANK1 | unsigned long | Schlauchabfalldiagnose für Bank 1 ist durchgelaufen 1BYTE_IDENTICAL_BIT1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-verbraucherstrom-efii"></a>
### STATUS_VERBRAUCHERSTROM_EFII

Auslesen Verbraucherstrommessung EFII UDS  : $31   RoutineControl UDS  : $03   routineControlType UDS  : $7002 routineIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_WERT | unsigned int | Ecos2 Funktionsstati Wert |
| STAT_STATUS_EINH | string | Ecos2 Funktionsstati Einheit |
| STAT_STATUS_TEXT | string | Ecos2 Funktionsstati Text |
| STAT_BEWERTUNG | char | Ecos2 Resultat Bewertung |
| STAT_GRUNDWERT_WERT | real | Ecos2 Strom Grundwert in A |
| STAT_GRUNDWERT_EINH | string | Strom in A |
| STAT_DIFFERENZWERT_WERT | real | Ecos2 Strom Messwert in A |
| STAT_DIFFERENZWERT_EINH | string | Strom in A |
| STAT_TRANSIENT | binary | Transienten Array |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-ende-dk"></a>
### STEUERN_ENDE_DK

0x2F602A00 STEUERN_ENDE_DK Drosselklappe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-atl"></a>
### STOP_SYSTEMCHECK_ATL

0x3102F0D0 STOP_SYSTEMCHECK_ATL Diagnosefunktion Abgasturbolader beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-msainfo2"></a>
### STATUS_MSAINFO2

Auslesen Infospeicher Batteriezustandserkennung 2 UDS*: 0x224092 ReadDataByIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LADUNGSMENGE_GESAMT_WERT | real | Kumulierte, verbrauchte Ladungsmenge 2BYTE_in 0 bis 19087Ah   Einheit: Ah   Min: 0 Max: 190872 |
| STAT_LADUNGSMENGE_GESAMT_EINH | string | Ah |
| STAT_ANZAHL_MOTORSTART_GESAMT | real | Gesamtzahl Starts 2BYTE in 0 bis 327675   Min: 0 Max: 327675 |
| STAT_ANZAHL_MSASTART_GESAMT | real | Anzahl MSA Starts 2BYTE in 0 bis 327675   Min: 0 Max: 327675 |
| STAT_ANZAHL_FZGSTOP_GESAMT | real | Anzahl Fahrzeugstops 2BYTE in 0 bis 327675   Min: 0 Max: 327675 |
| STAT_ZEIT_IN_MSA_GESAMT_WERT | real | Zeit in MSA 2BYTE in 0 bis 3276750s   Einheit: s   Min: 0 Max: 3276750 |
| STAT_ZEIT_IN_MSA_GESAMT_EINH | string | Sekunde |
| STAT_ZEIT_IN_FZGSTOP_GESAMT_WERT | real | Zeit in Fahrzeugstop 2BYTE in 0 bis 3276750s   Einheit: s   Min: 0 Max: 3276750 |
| STAT_ZEIT_IN_FZGSTOP_GESAMT_EINH | string | Sekunde |
| STAT_BATTSPG_DSOC_INTERVALL1_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG1 und K_DSOCMSADG2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL1_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL2_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG2 und K_DSOCMSADG3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL2_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL3_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG3 und K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL3_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL4_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC groesser K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL4_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL1_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG1 und K_DSOCMSADG2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL1_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL2_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG2 und K_DSOCMSADG3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL2_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL3_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG3 und K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL3_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL4_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC groesser K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL4_UEBER_TGRENZ_EINH | string | V |
| STAT_ANZAHL_MSASTOPPS_INTERVALL_0_BIS_5_SEC | unsigned long | Anzahl der MSA-Stopps mit der Dauer: 0sec &lt;Dauer&lt; 5sec Bytes 20, 21 2BYTE in 0 bis 65535 |
| STAT_ANZAHL_MSASTOPPS_INTERVALL_5_BIS_20_SEC | unsigned long | Anzahl der MSA-Stopps mit der Dauer: &gt;5sec &lt;Dauer&lt; 20sec Bytes 22, 23 2BYTE in 0 bis 65535 |
| STAT_ANZAHL_MSASTOPPS_INTERVALL_20_BIS_45_SEC | unsigned long | Anzahl der MSA-Stopps mit der Dauer: &gt;20sec &lt;Dauer&lt; 45sec Bytes 24, 25 2BYTE in 0 bis 65535 |
| STAT_ANZAHL_MSASTOPPS_GROESSER_45_SEC | unsigned long | Anzahl der MSA-Stopps mit der Dauer: Dauer&gt; 45sec Bytes 26, 27 2BYTE in 0 bis 65535 |
| STAT_MSA_STOP_1_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 1 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_1_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_1_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 1 2BYTE in 0 bis 65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_1_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_1_TEMP_WERT | real | Temp MSA-Stop 1 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_1_TEMP_EINH | string | degreeC |
| STAT_MSA_STOP_2_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_2_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_2_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 2 2BYTE in 0 bis 65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_2_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_2_TEMP_WERT | real | Temp MSA-Stop 2 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_2_TEMP_EINH | string | degreeC |
| STAT_MSA_STOP_3_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_3_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_3_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 3 2BYTE in 0 bis 65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_3_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_3_TEMP_WERT | real | Temp MSA-Stop 3 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_3_TEMP_EINH | string | degreeC |
| STAT_MSA_EA_SOC_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer SOC 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_BATTERIESPANNUNG_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer BATTERIESPANNUNG 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_HOHER_ANLAUFSTROM_E_LUEFTER | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE2 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE3_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE3 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE4_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE4 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE5_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE5 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE6_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE6 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE7_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE7 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_SOC_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer SOC 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_STRTSPG_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Startspannung 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_DIAGNOSE_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Generator-Diagnose 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_TBATT_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Batterietemperatur 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_TRAMODE_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Tra-Mode 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_ZYKL_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Zyklisierung 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_BNSTROM_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer zu hoher Bordnetzstrom 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_NIEDRIGE_BATTTEMP | unsigned long | aktuell aktiver Abschaltverhinderer RESERVE2 1BIT   1: aktiv    0: nicht aktiv |
| STAT_ANZAHL_WIRKSAME_AV_NIEDRIGER_SOC | unsigned long | Anzahl der wirksamen AV: niedriger Ladezustand der Batterie. Gezählt wird nur ein AV während eines Kl15 Zyklus Byte 42 1BYTE in 0 bis 254, ohne Einheit |
| STAT_ANZAHL_WIRKSAME_AV_NIEDRIGE_STARTSPANNUNG | unsigned long | Anzahl der wirksamen AV: niedrige Startspannungslage. Gezählt wird nur ein AV während eines Kl15 Zyklus Byte 43 1BYTE in 0 bis 254, ohne Einheit |
| STAT_ANZAHL_WIRKSAME_AV_HOHE_BATTERIETEMPERATUR | unsigned long | Anzahl der wirksamen AV: hohe Batterietemperatur. Gezählt wird nur ein AV während eines Kl15 Zyklus Byte 44 1BYTE in 0 bis 254, ohne Einheit |
| STAT_ANZAHL_WIRKSAME_AV_HOHER_BORDNETZSTROM | unsigned long | Anzahl der wirksamen AV: hoher BN-Strom. Gezählt wird nur ein AV während eines Kl15 Zyklus Byte 45 1BYTE in 0 bis 254, ohne Einheit |
| STAT_ANZAHL_WIRKSAME_EA_NIEDRIGER_SOC | unsigned long | Anzahl der wirksamen Einschaltanforderer: niedriger Ladezustnd der Batterie. Gezählt wird nur ein EA während eines Kl15 Zyklus Byte 46 1BYTE in 0 bis 254, ohne Einheit |
| STAT_ANZAHL_WIRKSAME_EA_NIEDRIGE_SPANNUNG | unsigned long | Anzahl der wirksamen Einschaltanforderer: niedrige Spannungslage. Gezählt wird nur ein EA während eines Kl15 Zyklus Byte 47 1BYTE in 0 bis 254, ohne Einheit |
| STAT_KM_STAND_BEI_RESET_AV_EV_WERT | unsigned long | KM-Stand bei Reset der Abschaltverhinderer / Einschaltanforderer Zähler Bytes 48, 49 2BYTE in 0 bis 65535 |
| STAT_KM_STAND_BEI_RESET_AV_EV_EINH | string | km |
| STAT_ENTLADUNG_MSASTART_BIS_GENERATORVERSORGUNG_WERT | unsigned long | Entlademenge vom MSA Start bis zur Versorgung durch Generator Bytes 50, 51, 52 3BYTE in 0 bis 167772150, Einheit Amperesekunden |
| STAT_ENTLADUNG_MSASTART_BIS_GENERATORVERSORGUNG_EINH | string | As |
| STAT_ANZAHL_WIRKSAME_AV_NIEDRIGE_BATTTEMP | unsigned long | Label Num_msaav_lowtbatt neues Results ab AEP FR26,0 Ergebnis bei altem Programmstand: 255 Byte 53 1BYTE in 0 bis 254, ohne Einheit |
| STAT_ANZAHL_WIRKSAME_EA_HOHER_ANLAUFSTROM_ELUEFTER | unsigned long | Label Num_msaea_inlwm neues Results ab AEP FR26,0 Ergebnis bei altem Programmstand: 255 Byte 54 1BYTE in 0 bis 254, ohne Einheit |
| STAT_BALT_VERSCHIEBEKONSTANTE_WERT | unsigned long | Verschiebung Kennlinie KL_MSADSOC_AKT in Abhängigkeit von Batteriealterung neues Results ab AEP FR26,0 Ergebnis bei altem Programmstand: 255 Byte 55 1BYTE in 0 bis 254 |
| STAT_BALT_VERSCHIEBEKONSTANTE_EINH | string | % neues Results ab AEP FR26,0 |
| STAT_BALT_KMSTAND_BEI_AENDERUNG_VERSCHIEBEKONSTANTE_WERT | unsigned long | KM-Stand bei Reset der Abschaltverhinderer / Einschaltanforderer Zähler neues Results ab AEP FR26,0 Ergebnis bei altem Programmstand: 655350 Bytes 56, 57 (MSB: 56, LSB: 57) Auflösung 10km 2BYTE in 0 bis 655349 |
| STAT_BALT_KMSTAND_BEI_AENDERUNG_VERSCHIEBEKONSTANTE_EINH | string | km neues Results ab AEP FR26,0 |
| STAT_BALT_BZE3_ALTERUNGSERKENNUNG | long | KM-Stand bei Reset der Abschaltverhinderer / Einschaltanforderer Zähler neues Results ab AEP FR26,0 Ergebnis bei altem Programmstand: 255 Byte 58 Berechnung: Rohwert -100 1BYTE in 0 bis 254 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei neues Results ab AEP FR26,0 |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-msvhdp5"></a>
### STEUERN_MSVHDP5

0x2F60EF03 STEUERN_MSVHDP5 Mengensteuerventil HDP5 ansteuern NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_MSVHDP5_WERT | real | Tastverhaeltniss Mengensteuerventil HDP5 ARQTMSV_W_RB[0]   Einheit: CRK   Min: -3276.8 Max: 3276.7 |
| SW_TO_MSVHDP5_WERT | unsigned long | Timeout Mengensteuerventil HDP5 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ekp"></a>
### STEUERN_ENDE_EKP

0x2F60D800 STEUERN_ENDE_EKP Elektrische Kraftstoffpumpe 1 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dfdsn"></a>
### STATUS_DFDSN

0x224156 STATUS_DFDSN Diagnose der Generatorauslastung über FASTA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BEREICH_0_HOHEGENAUSLAST_STROMUNABH_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_0_HOHEGENAUSLAST_STROMUNABH_EINH | string | Prozent |
| STAT_BEREICH_1_ERHOEHTEGENAUSLAST_STROMUNABH_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_1_ERHOEHTEGENAUSLAST_STROMUNABH_EINH | string | Prozent |
| STAT_BEREICH_2_MITTLEREGENAUSLAST_STROMUNABH_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_2_MITTLEREGENAUSLAST_STROMUNABH_EINH | string | Prozent |
| STAT_BEREICH_3_NIEDRIGEGENAUSLAST_STROMUNABH_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_3_NIEDRIGEGENAUSLAST_STROMUNABH_EINH | string | Prozent |
| STAT_BEREICH_4_HOHEGENAUSLAST_HOHERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_4_HOHEGENAUSLAST_HOHERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_5_ERHOEHTEGENAUSLAST_HOHERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_5_ERHOEHTEGENAUSLAST_HOHERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_6_MITTLEREGENAUSLAST_HOHERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_6_MITTLEREGENAUSLAST_HOHERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_7_NIEDRIGEGENAUSLAST_HOHERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_7_NIEDRIGEGENAUSLAST_HOHERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_8_HOHEGENAUSLAST_GERINGERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_8_HOHEGENAUSLAST_GERINGERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_9_ERHOEHTEGENAUSLAST_GERINGERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_9_ERHOEHTEGENAUSLAST_GERINGERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_10_MITTLEREGENAUSLAST_GERINGERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_10_MITTLEREGENAUSLAST_GERINGERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_11_NIEDRIGEGENAUSLAST_GERINGERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_11_NIEDRIGEGENAUSLAST_GERINGERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_12_HOHEGENAUSLAST_KEINLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_12_HOHEGENAUSLAST_KEINLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_13_ERHOEHTEGENAUSLAST_KEINLADESTROM_WERT | real | gewichteter Mittelwert 6BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_13_ERHOEHTEGENAUSLAST_KEINLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_14_MITTLEREGENAUSLAST_KEINLADESTROM_WERT | real | gewichteter Mittelwert 6BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_14_MITTLEREGENAUSLAST_KEINLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_15_NIEDRIGEGENAUSLAST_KEINLADESTROM_WERT | real | gewichteter Mittelwert 6BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_15_NIEDRIGEGENAUSLAST_KEINLADESTROM_EINH | string | Prozent |
| STAT_SCHLECHTLADEBILANZ | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_SCHLECHTLADEBILANZ_EINH | string | Prozent |
| STAT_VERBRAUCHERREDUZIERUNG_BIT_6 | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_VERBRAUCHERREDUZIERUNG_BIT_6_EINH | string | Prozent |
| STAT_GENERATORSTATUS_BIT_5 | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_GENERATORSTATUS_BIT_5_EINH | string | Prozent |
| STAT_GENERATORSTATUS_BIT_6 | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_GENERATORSTATUS_BIT_6_EINH | string | Prozent |
| STAT_BSZ_DF | unsigned long | gewichteter Mittelwert 3BYTE   Einheit: Sekunden   Min: 0 Max: 16.777.215 |
| STAT_BSZ_DF_EINH | string | Sekunden |
| STAT_DFFGEN_TEMP_MXCNTR | unsigned long | gewichteter Mittelwert 2BYTE   Einheit: s   Min: 0 Max: 16.777.215 |
| STAT_DFFGEN_TEMP_MXCNTR_EINH | string | Sekunden |
| STAT_DFFGEN_TEMP_NCNTR | unsigned long | gewichteter Mittelwert 2BYTE   Einheit: s   Min: 0 Max: 16.777.215 |
| STAT_DFFGEN_TEMP_NCNTR_EINH | string | Sekunden |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-betriebsstundenzaehler"></a>
### STATUS_BETRIEBSSTUNDENZAEHLER

0x224AB4 STATUS_BETRIEBSSTUNDENZAEHLER Betriebsstundenzaehler auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TRT_WERT | real | Betriebsstundenzaehler(A2L-Name: trt) TRT   Einheit: h   Min: 0 Max: 119304.6471 |
| STAT_TRT_EINH | string | h |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ugen"></a>
### STEUERN_ENDE_UGEN

0x2F603200 STEUERN_ENDE_UGEN Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-leminfo-aep"></a>
### STATUS_LEMINFO_AEP

0x224017 STATUS_LEMINFO_AEP Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZR_USTAT_AEP_A_WERT | real | Haeufigkeitszaehler Zr_ustat_A 2BYTE in 0 bis 13107s   Einheit: s   Min: 0 Max: 13107 |
| STAT_ZR_USTAT_AEP_A_EINH | string | second |
| STAT_ZR_USTAT_AEP_A_INFO | string | Häufigkeit Spannungsbereich &gt;16 V |
| STAT_ZR_USTAT_AEP_B_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_B 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_B_EINH | string | second |
| STAT_ZR_USTAT_AEP_B_INFO | string | Häufigkeit Spannungsbereich zwischen K_LEMDIAGU1 und 16 V |
| STAT_ZR_USTAT_AEP_C_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_C 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_C_EINH | string | second |
| STAT_ZR_USTAT_AEP_C_INFO | string | Häufigkeit Spannungsbereich zwischen K_LEMDIAGU2 und  K_LEMDIAGU1 V |
| STAT_ZR_USTAT_AEP_D_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_D 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_D_EINH | string | second |
| STAT_ZR_USTAT_AEP_D_INFO | string | Häufigkeit Spannungsbereich zwischen K_LEMDIAGU3 und  K_LEMDIAGU2 V |
| STAT_ZR_USTAT_AEP_E_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_E 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_E_EINH | string | second |
| STAT_ZR_USTAT_AEP_E_INFO | string | Häufigkeit Spannungsbereich zwischen K_LEMDIAGU4 und  K_LEMDIAGU3 V |
| STAT_ZR_USTAT_AEP_F_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_F 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_F_EINH | string | second |
| STAT_ZR_USTAT_AEP_F_INFO | string | Häufigkeit Spannungsbereich zwischen 9 und  K_LEMDIAGU4 V |
| STAT_ZR_USTAT_AEP_G_WERT | real | Haeufigkeitszaehler Zr_ustat_G 2BYTE in 0 bis 13107s   Einheit: s   Min: 0 Max: 13107 |
| STAT_ZR_USTAT_AEP_G_EINH | string | second |
| STAT_ZR_USTAT_AEP_G_INFO | string | Häufigkeit Spannungsbereich &lt;9 V |
| STAT_ZR_PRIO_AEP_A_WERT | unsigned long | Haeufigkeit Priobereich A 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_A_EINH | string | second |
| STAT_ZR_PRIO_AEP_B_WERT | unsigned long | Haeufigkeit Priobereich B 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_B_EINH | string | second |
| STAT_ZR_PRIO_AEP_C_WERT | unsigned long | Haeufigkeit Priobereich C 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_C_EINH | string | second |
| STAT_ZR_PRIO_AEP_D_WERT | unsigned long | Haeufigkeit Priobereich D 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_D_EINH | string | second |
| STAT_ZR_PRIO_AEP_E_WERT | unsigned long | Haeufigkeit Priobereich E 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_E_EINH | string | second |
| STAT_ZR_PRIO_AEP_F_WERT | unsigned long | Haeufigkeit Priobereich F 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_F_EINH | string | second |
| STAT_ZR_PRIO_AEP_G_WERT | unsigned long | Haeufigkeit Priobereich G 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_G_EINH | string | second |
| STAT_ZR_PRIO_AEP_H_WERT | unsigned long | Haeufigkeit Priobereich H 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_H_EINH | string | second |
| STAT_ZR_PRIO_AEP_I_WERT | unsigned long | Haeufigkeit Priobereich I 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_I_EINH | string | second |
| STAT_ZR_PRIO_AEP_J_WERT | unsigned long | Haeufigkeit Priobereich J 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_J_EINH | string | second |
| STAT_ZR_PRIO_AEP_K_WERT | unsigned long | Haeufigkeit Priobereich K 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_K_EINH | string | second |
| STAT_ZR_PRIO_AEP_L_WERT | unsigned long | Haeufigkeit Priobereich L 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_L_EINH | string | second |
| STAT_ZR_PRIO_AEP_M_WERT | unsigned long | Haeufigkeit Priobereich M 2BYTE_in_0bis131070s   Einheit: s   Min: 0 Max: 131070 |
| STAT_ZR_PRIO_AEP_M_EINH | string | second |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ibs-strommessung"></a>
### STATUS_IBS_STROMMESSUNG

Auslesen IBS Strommessung UDS: $31 RoutineControl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FS_IBS_STROMMESSUNG | int | (A2L_Name: Eco_i_status) |
| STAT_STROMWERT_WERT | real | (A2L_Name: Eco_i_result) |
| STAT_STROMWERT_EINH | string | A |

<a id="job-abgleichwerte-schreiben"></a>
### ABGLEICHWERTE_SCHREIBEN

0x2E5F90 ABGLEICHWERTE_SCHREIBEN Abgleichwerte Injektoren programmieren für CASCADE mit Übernahme Daten aus COD-Datei Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_SCHREIBEN_DATEN | string | Abgleichdaten für alle Injektoren aus COD-Datei |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_SCHREIBEN_ABGLEICHDATEN | string | Abgleichdaten zum Steuergeraet |
| ABGLEICHWERTE_SCHREIBEN_PRUEFZEICHEN | string | das im Job berechnete Pruefzeichen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-motorlaufunruhe"></a>
### STATUS_MOTORLAUFUNRUHE

0x224003 STATUS_MOTORLAUFUNRUHE Motorlaufunruhewerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZYL1_WERT | real | gefilterte Laufunruhe Zylinder 1 ER_MMV_IS_DIAG[0]   Min: -8 Max: 7.99975586 |
| STAT_ZYL5_WERT | real | gefilterte Laufunruhe Zylinder 5 ER_MMV_IS_DIAG[1]   Min: -8 Max: 7.99975586 |
| STAT_ZYL3_WERT | real | gefilterte Laufunruhe Zylinder 3 ER_MMV_IS_DIAG[2]   Min: -8 Max: 7.99975586 |
| STAT_ZYL6_WERT | real | gefilterte Laufunruhe Zylinder 6 ER_MMV_IS_DIAG[3]   Min: -8 Max: 7.99975586 |
| STAT_ZYL2_WERT | real | gefilterte Laufunruhe Zylinder 2 ER_MMV_IS_DIAG[4]   Min: -8 Max: 7.99975586 |
| STAT_ZYL4_WERT | real | gefilterte Laufunruhe Zylinder 4 ER_MMV_IS_DIAG[5]   Min: -8 Max: 7.99975586 |
| STAT_GEBERRAD_ADAPTION | unsigned long | Kurbelwelle Segmentadaption beendet 0=nein / 1=ja LV_SEG_AD_AVL_ER   Min: 0 Max: 1 |
| STAT_VLS_UP_1_WERT | real | Spannung Lambdasonde vor Katalysator Bank 1 VLS_UP[1]   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_VLS_UP_1_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-messwerte"></a>
### STATUS_MESSWERTE

0x224000 STATUS_MESSWERTE Messwerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EV1_MW_WERT | real | Einspritzzeit EV 1 TI_1_HOM[0]   Einheit: ms   Min: 0 Max: 65.535 |
| STAT_EV1_MW_EINH | string | ms |
| STAT_LR1_MW_WERT | real | Lambdaregler 1 FAC_LAM_LIM[1]   Einheit: %   Min: -50 Max: 49.9984741210938 |
| STAT_LR1_MW_EINH | string | percent |
| STAT_LR2_MW_WERT | real | Lambdaregler 2 FAC_LAM_LIM[2]   Einheit: %   Min: -50 Max: 49.9984741210938 |
| STAT_LR2_MW_EINH | string | percent |
| STAT_VFZG_MW_WERT | unsigned long | Fahrzeuggeschwindigkeit VS   Einheit: km/h   Min: 0 Max: 255 |
| STAT_VFZG_MW_EINH | string | kmperh |
| STAT_NMOT_W_MW_WERT | unsigned long | Motordrehzahl hoch aufgeloest N   Einheit: rpm   Min: 0 Max: 8160 |
| STAT_NMOT_W_MW_EINH | string | rpm |
| STAT_NSOL_MW_WERT | unsigned long | Leerlauf-Solldrehzahl N_SP_IS   Einheit: rpm   Min: 0 Max: 8160 |
| STAT_NSOL_MW_EINH | string | rpm |
| STAT_CAM_IN_1_WERT | real | Istwert Einlassnockenwellensteller Bank 1 CAM_IN_H[1]   Einheit: CRK   Min: -3276.8 Max: 3276.7 |
| STAT_CAM_IN_1_EINH | string | degreeCRK |
| STAT_CAM_EX_1_WERT | real | Istwert Auslassnockenwellensteller Bank 1 CAM_EX[1]   Einheit: CRK   Min: -135.625 Max: -40 |
| STAT_CAM_EX_1_EINH | string | degreeCRK |
| STAT_TIA_WERT | real | Ansauglufttemperatur TIA   Einheit: C   Min: -48 Max: 142.5 |
| STAT_TIA_EINH | string | degreeC |
| STAT_TCO_MES_WERT | real | Kuehlmitteltemperatur Rohwert TCO_MES   Einheit: C   Min: -48 Max: 142.5 |
| STAT_TCO_MES_EINH | string | degreeC |
| STAT_IGA_IGC_WERT | real | Zuendwinkel Zylinder 1 IGA_IGC[0]   Einheit: CRK   Min: -35.625 Max: 60 |
| STAT_IGA_IGC_EINH | string | degreeCRK |
| STAT_TPS_AV_1_1_WERT | real | Drosselklappenwinkel Potentiometer 1 Bank 1 TPS_AV_1[1]   Einheit: TPS   Min: -119.507294146371 Max: 119.5 |
| STAT_TPS_AV_1_1_EINH | string | degreeTPS |
| STAT_MAF_KGH_MES_BAS_1_WERT | real | Gemessene Luftmasse Rohwert Bank 1 MAF_KGH_MES_BAS[1]   Einheit: kg/h   Min: 0 Max: 2047.96875 |
| STAT_MAF_KGH_MES_BAS_1_EINH | string | kgperh |
| STAT_TQI_AV_WERT | real | aktuelle Drehmomentanforderung TQI_AV   Einheit: Nm   Min: -1024 Max: 1023.96875 |
| STAT_TQI_AV_EINH | string | Nm |
| STAT_VB_WERT | real | Batteriespannung VB   Einheit: V   Min: 0 Max: 25.8984375 |
| STAT_VB_EINH | string | V |
| STAT_V_PVS_1_WERT | real | Pedalwertgeber 1 Rohwert V_PVS_1   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_V_PVS_1_EINH | string | V |
| STAT_TCO_2_MES_WERT | real | Kuehlmittelauslasstemperatur Rohwert TCO_2_MES   Einheit: C   Min: -48 Max: 142.5 |
| STAT_TCO_2_MES_EINH | string | degreeC |
| STAT_NL_0_WERT | real | Spannung Klopfwerte Zylinder 1 Bank 1 NL[0]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_NL_0_EINH | string | V |
| STAT_NL_1_WERT | real | Spannung Klopfwerte Zylinder 5 Bank 1 NL[1]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_NL_1_EINH | string | V |
| STAT_NL_2_WERT | real | Spannung Klopfwerte Zylinder 3 Bank 1 NL[2]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_NL_2_EINH | string | V |
| STAT_NL_3_WERT | real | Spannung Klopfwerte Zylinder 6 Bank 1 NL[3]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_NL_3_EINH | string | V |
| STAT_NL_4_WERT | real | Spannung Klopfwerte Zylinder 2 Bank 1 NL[4]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_NL_4_EINH | string | V |
| STAT_NL_5_WERT | real | Spannung Klopfwerte Zylinder 4 Bank 1 NL[5]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_NL_5_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ident-opf"></a>
### STATUS_IDENT_OPF

0x224117 STATUS_IDENT_OPF Ladungsbilanz des OPF lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOLLZUST_OPF_WERT | unsigned long | Sollzustand des OPF: Verbaut und Typ 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_SOLLZUST_OPF_DRUCKSENS_WERT | unsigned long | Sollzustand des OPF-Drucksensors: Verbaut und Typ 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_SOLLZUST_OPF_TEMPSENS_WERT | unsigned long | Sollzustand OPF Temperatursensoren (dezimal Kodiert) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-agk"></a>
### STEUERN_ENDE_AGK

0x2F60C100 STEUERN_ENDE_AGK Abgasklappe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-obd-demo-momentenbegrenzung"></a>
### STATUS_OBD_DEMO_MOMENTENBEGRENZUNG

0x3103F09E STATUS_OBD_DEMO_MOMENTENBEGRENZUNG OBD Demo Momentenbegrenzung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_MOTORMOMENTBEGRENZUNG_TEXT | string | Funktionsstatus der OBD DEMO Momentenbegrenzung 1BYTE FUNKTIONSSTATUS |
| STAT_FS_MOTORMOMENTBEGRENZUNG_WERT | int | Funktionsstatus der OBD DEMO Momentenbegrenzung 1BYTE FUNKTIONSSTATUS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-eisygd"></a>
### STEUERN_EISYGD

0x3101F0E1 STEUERN_EISYGD Ansteuern Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_WERT | long | Drehzahl NKW_SOLL   Einheit: Upm   Min: -32768 Max: 32767 |
| VSE_SPRI_WERT | real | Istwert Einlassspreizung variable NWS VSE_SPRI   Einheit: Grad KW   Min: 0 Max: 6553.5 |
| VSA_SPRI_WERT | real | Istwert Auslassspreizung variable NWS VSA_SPRI   Einheit: Grad KW   Min: 0 Max: 6553.5 |
| WDK_IST_WERT | real | Aktueller Drosselklappenwinkel WDK_IST   Einheit: %   Min: -800 Max: 799.9755 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-igr-aus"></a>
### START_SYSTEMCHECK_IGR_AUS

0x3101F0F7 START_SYSTEMCHECK_IGR_AUS Ansteuerung Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ews4-sk"></a>
### STATUS_EWS4_SK

Lesen des SecretKey des Server sowie Client für EWS4 UDS   : $22   ReadDataByIdentifier UDS   : $C002 Sub-Parameter

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAGSG | string | Diagnose Steuergerät zulässig DME, DME2, EGS ohne Eintrag wird Original-Diagnoseadresse verwendet |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS4_SERVER_SK | binary | SecretKey Server |
| STAT_EWS4_CLIENT_SK | binary | SecretKey Client |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-aep-i12-zyknl-histogramm-loeschen"></a>
### START_AEP_I12_ZYKNL_HISTOGRAMM_LOESCHEN

Löschen von Histogramm und Zähler aller Ladevorgänge der 12V-Batterie aus dem Hochvolt-System AEP_I12_ZYKNL_HISTOGRAMM_LOESCHEN (0x31 01 AE03)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-digital-0"></a>
### STATUS_DIGITAL_0

0x224007 STATUS_DIGITAL_0 Status Schaltzustaende 0 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LS1_REGELUNG_TEXT | string | Status Regelkreis Bank 1 LV_LAM_LSCL[1] |
| STAT_LS1_REGELUNG_WERT | int | Status Regelkreis Bank 1 LV_LAM_LSCL[1] |
| STAT_LS2_REGELUNG_TEXT | string | Status Regelkreis Bank 2 LV_LAM_LSCL[2] |
| STAT_LS2_REGELUNG_WERT | int | Status Regelkreis Bank 2 LV_LAM_LSCL[2] |
| STAT_LSVK1_TEXT | string | Status Lambdaregelung vor Katalysator Bank 1 LV_LS_UP_READY[1] |
| STAT_LSVK1_WERT | int | Status Lambdaregelung vor Katalysator Bank 1 LV_LS_UP_READY[1] |
| STAT_LSVK2_TEXT | string | Status Lambdaregelung vor Katalysator Bank 2 LV_LS_UP_READY[2] |
| STAT_LSVK2_WERT | int | Status Lambdaregelung vor Katalysator Bank 2 LV_LS_UP_READY[2] |
| STAT_LSHK2_TEXT | string | Status Lambdaregelung hinter Katalysator Bank 2 LV_LS_DOWN_READY[2] |
| STAT_LSHK2_WERT | int | Status Lambdaregelung hinter Katalysator Bank 2 LV_LS_DOWN_READY[2] |
| STAT_LSHK1_TEXT | string | Status Lambdaregelung hinter Katalysator Bank 1 LV_LS_DOWN_READY[1] |
| STAT_LSHK1_WERT | int | Status Lambdaregelung hinter Katalysator Bank 1 LV_LS_DOWN_READY[1] |
| STAT_VL_TEXT | string | Status Vollast LV_FL |
| STAT_VL_WERT | int | Status Vollast LV_FL |
| STAT_LL_TEXT | string | Status Leerlauf LV_IS |
| STAT_LL_WERT | int | Status Leerlauf LV_IS |
| STAT_DK_ABGLEICH_TEXT | string | Status Drosselklappen-Neuabgleich LV_TPS_AD_REQ |
| STAT_DK_ABGLEICH_WERT | int | Status Drosselklappen-Neuabgleich LV_TPS_AD_REQ |
| STAT_SCHUBAB_TEXT | string | Status Schubabschaltung LV_PUC |
| STAT_SCHUBAB_WERT | int | Status Schubabschaltung LV_PUC |
| STAT_FAHRSTUFE_TEXT | string | Status Fahrstufe LV_DRI |
| STAT_FAHRSTUFE_WERT | int | Status Fahrstufe LV_DRI |
| STAT_KICKDOWN_TEXT | string | Status Kickdownerkennung LV_KD |
| STAT_KICKDOWN_WERT | int | Status Kickdownerkennung LV_KD |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-digital-1"></a>
### STATUS_DIGITAL_1

0x224002 STATUS_DIGITAL_1 Status Schaltzustaende Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AC_EIN_TEXT | string | Status Klimabereitschaft LV_ACCOUT_RLY |
| STAT_AC_EIN_WERT | int | Status Klimabereitschaft LV_ACCOUT_RLY |
| STAT_BTS_EIN_TEXT | string | Status Bremslichtschalter-Kanal 2 LV_IM_BTS |
| STAT_BTS_EIN_WERT | int | Status Bremslichtschalter-Kanal 2 LV_IM_BTS |
| STAT_BLS_EIN_TEXT | string | Status Bremslichtschalter-Kanal 1 LV_IM_BLS |
| STAT_BLS_EIN_WERT | int | Status Bremslichtschalter-Kanal 1 LV_IM_BLS |
| STAT_KUPPL_EIN_TEXT | string | Status Kupplungsschalter LV_CS |
| STAT_KUPPL_EIN_WERT | int | Status Kupplungsschalter LV_CS |
| STAT_MOTOR_AUS_TEXT | string | Status Motorzustand LV_ES |
| STAT_MOTOR_AUS_WERT | int | Status Motorzustand LV_ES |
| STAT_KL15_EIN_TEXT | string | Status Klemme-15 LV_IGK |
| STAT_KL15_EIN_WERT | int | Status Klemme-15 LV_IGK |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-igr-aus"></a>
### STOP_SYSTEMCHECK_IGR_AUS

0x3102F0F7 STOP_SYSTEMCHECK_IGR_AUS Ende Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-obd-demo-gangeinlegen"></a>
### STATUS_OBD_DEMO_GANGEINLEGEN

0x3103F09D STATUS_OBD_DEMO_GANGEINLEGEN OBD Demo Gangeinlegen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_OBD_GANG_TEXT | string | Funktionsstatus von OBD DEMO verzoegertes Gangeinlegen 1BYTE FUNKTIONSSTATUS |
| STAT_FS_OBD_GANG_WERT | int | Funktionsstatus von OBD DEMO verzoegertes Gangeinlegen 1BYTE FUNKTIONSSTATUS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-imaalle"></a>
### STEUERN_PROGRAMM_IMAALLE

0x2E5F90 STEUERN_PROGRAMM_IMAALLE Abgleichwerte Injektoren programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_1_WERT | real | IMA Abgleichwert Injektor 01 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[0]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_1_WERT | real | IMA Abgleichwert Injektor 01 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[0]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_7_WERT | real | IMA Abgleichwert Injektor 07 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[1]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_7_WERT | real | IMA Abgleichwert Injektor 07 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[1]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_5_WERT | real | IMA Abgleichwert Injektor 05 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[2]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_5_WERT | real | IMA Abgleichwert Injektor 05 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[2]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_11_WERT | real | IMA Abgleichwert Injektor 11 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[3]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_11_WERT | real | IMA Abgleichwert Injektor 11 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[3]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_3_WERT | real | IMA Abgleichwert Injektor 03 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[4]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_3_WERT | real | IMA Abgleichwert Injektor 03 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[4]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_9_WERT | real | IMA Abgleichwert Injektor 09 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[5]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_9_WERT | real | IMA Abgleichwert Injektor 09 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[5]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_6_WERT | real | IMA Abgleichwert Injektor 06 Flow1 (Energie) (A2L-Name: egy_sp_iv_ext_adj[6]) EGY_SP_IV_EXT_ADJ[6]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_6_WERT | real | IMA Abgleichwert Injektor 06 Flow2 (Durchfluss) (A2L-Name: mff_absv_iv_ext_adj[6]) MFF_ABSV_IV_EXT_ADJ[6]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_12_WERT | real | IMA Abgleichwert Injektor 12 Flow1 (Energie)(A2L-Name: egy_sp_iv_ext_adj[7]) EGY_SP_IV_EXT_ADJ[7]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_12_WERT | real | IMA Abgleichwert Injektor 12 Flow2 (Durchfluss) (A2L-Name: mff_absv_iv_ext_adj[7]) MFF_ABSV_IV_EXT_ADJ[7]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_2_WERT | real | IMA Abgleichwert Injektor 02 Flow1 (Energie) (A2L-Name: egy_sp_iv_ext_adj[8]) EGY_SP_IV_EXT_ADJ[8]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_2_WERT | real | IMA Abgleichwert Injektor 02 Flow2 (Durchfluss) (A2L-Name: mff_absv_iv_ext_adj[8]) MFF_ABSV_IV_EXT_ADJ[8]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_8_WERT | real | IMA Abgleichwert Injektor 8 Flow1 (Energie) (A2L-Name: egy_sp_iv_ext_adj[9]) EGY_SP_IV_EXT_ADJ[9]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_8_WERT | real | IMA Abgleichwert Injektor 08 Flow2 (Durchfluss) (A2L-Name: mff_absv_iv_ext_adj[9]) MFF_ABSV_IV_EXT_ADJ[9]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_4_WERT | real | IMA Abgleichwert Injektor 04 Flow1 (Energie) (A2L-Name: egy_sp_iv_ext_adj[10]) EGY_SP_IV_EXT_ADJ[10]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_4_WERT | real | IMA Abgleichwert Injektor 04 Flow2 (Durchfluss) (A2L-Name: mff_absv_iv_ext_adj[10]) MFF_ABSV_IV_EXT_ADJ[10]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_10_WERT | real | IMA Abgleichwert Injektor 10 Flow1 (Energie) (A2L-Name: egy_sp_iv_ext_adj[11]) EGY_SP_IV_EXT_ADJ[11]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_10_WERT | real | IMA Abgleichwert Injektor 10  Flow2 (Durchfluss) (A2L-Name: mff_absv_iv_ext_adj[11]) MFF_ABSV_IV_EXT_ADJ[11]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-dmtl"></a>
### STATUS_SYSTEMCHECK_DMTL

0x3103F0DA STATUS_SYSTEMCHECK_DMTL Auslesen Diagnosefunktion DMTL Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1_TEXT | string | Funktionsstatus Diagnosefunktion DMTL STATE_EOL_KWP_DMTL   Min: 0 Max: 9 |
| STAT_DIAGNOSE_1_WERT | int | Funktionsstatus Diagnosefunktion DMTL STATE_EOL_KWP_DMTL   Min: 0 Max: 9 |
| STAT_DIAGNOSE_2_TEXT | string | Status Diagnosefunktion DMTL STATE_DMTL   Min: 0 Max: 12 |
| STAT_DIAGNOSE_2_WERT | int | Status Diagnosefunktion DMTL STATE_DMTL   Min: 0 Max: 12 |
| STAT_STROM_REF_WERT | real | Pumpenstrom Referenzleckmessung (A2L-Name: cur_dmtl_ref_leak) CUR_DMTL_REF_LEAK   Einheit: mA   Min: 0 Max: 400 |
| STAT_STROM_REF_EINH | string | milliAmper |
| STAT_STROM_GROB_WERT | real | Minimim Pumpenstromschwelle fuer EOL Test  (A2L-Name: cur_dmtl_rough_leak_min_eol) CUR_DMTL_ROUGH_LEAK_MIN_EOL   Einheit: mA   Min: 0 Max: 400 |
| STAT_STROM_GROB_EINH | string | milliAmper |
| STAT_STROM_WERT | real | Korregierter Pumpenstrom fuer EOL Test (A2L-Name: cur_dmtl_cor_fil_eol) CUR_DMTL_COR_FIL_EOL   Einheit: mA   Min: 0 Max: 400 |
| STAT_STROM_EINH | string | milliAmper |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-waput"></a>
### STEUERN_ENDE_WAPUT

0x2F608300 STEUERN_ENDE_WAPUT Wasserpumpe Turbolader auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-tev-regelung-aus"></a>
### STEUERN_ENDE_TEV_REGELUNG_AUS

0x3102F0CF STEUERN_ENDE_TEV_REGELUNG_AUS Deaktivierung TEV-Regelung beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-eluer"></a>
### STEUERN_ENDE_ELUER

0x2F608100 STEUERN_ENDE_ELUER E-Luefter-Relais Ansteuerung beenden NO_CON

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-dmtl"></a>
### START_SYSTEMCHECK_DMTL

0x3101F0DA START_SYSTEMCHECK_DMTL Ansteuern Diagnosefunktion DMTL Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-codierung-oel"></a>
### STATUS_CODIERUNG_OEL

0x223320 STATUS_CODIERUNG_OEL Codierung fuer Oelwechselintervall auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAENDERFAKTOR_1_WERT | real | Status fuer Codierung Laenderfaktor 1 Min: 0 Max: 2.55 |
| STAT_LAENDERFAKTOR_2_WERT | real | Status fuer Codierung Laenderfaktor 2 Min: 0 Max: 2.55 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-aep-i12-test-batteryguard"></a>
### _START_AEP_I12_TEST_BATTERYGUARD

Anforderung Aufruf BatteryGuard Call Setzen der Größe B_batteryguardcalldiag =1 Startvoraussetzungen: B_kl15 == TRUE. AEP_I12_TEST_BATTERYGUARD (0x31 01 F052)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-evausbl"></a>
### START_SYSTEMCHECK_EVAUSBL

0x3101F025 START_SYSTEMCHECK_EVAUSBL Ansteuern Diagnosefunktion Einspritzventilausblendung!ACHTUNG: hier wird die Zuendreihenfolge Bitcodiert verwendet! Aktivierung: Klemme 15 = EIN UND Motorstatus = (Leerlauf ODER Teillast) UND Drehzahl &lt; 3000 1/min Activation: LV_IGK = 1 UND STATE_ENG = (IS ODER PL) UND N &lt; C_N_MAX_KWP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VENTIL_NR_WERT | unsigned long | Shut off pattern for static cylinder shut off (fixed cylinder allocation) (A2L-Name: inh_iv) INH_IV_KWP   Min: 0 Max: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-obd-demo-momentenbegrenzung"></a>
### START_OBD_DEMO_MOMENTENBEGRENZUNG

0x3101F09E START_OBD_DEMO_MOMENTENBEGRENZUNG OBD Demo Momentenbegrenzung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_OBDDEMO_MOMENT_WERT | real | Momentendifferenz fuer Vertrimmung Mdi A2L-NAME=BMW_st_EngCtlEolCkTq BMWDGT_TQ_TQENGLIMDEMI   Einheit: Nm   Min: -3276.8 Max: 3276.7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-block-lesen"></a>
### STATUS_BLOCK_LESEN

Lesen eines dynamisch definierten Datenblockes UDS  : $2C DynamicallyDefineDataIdentifier $03 ClearDynamicallyDefinedDataIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $2C DynamicallyDefineDataIdentifier $01 DefineByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $22 ReadDataByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  $2C$02 DefineByMemoryAddress wird nicht unterstützt 'Composite data blocks' werden nur komplett unterstützt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_NR | long | Nummer des Blockes 0..255 |
| NEU_DEFINIEREN | string | Wenn 'JA' oder 'YES' wird der Block im SG gelöscht und neu ins SG geschrieben Wenn 'NEIN' oder 'NO' wird der Block im SG nicht gelöscht und nicht geschrieben Anschließend wird der Block gelesen |
| ARGUMENT_SPALTE | string | 'ARG', 'ID', 'LABEL' |
| STATUS | string | Es muss mindestens ein Argument übergeben werden Es wird das zugehörige Result table SG_Funktionen ARG ID RESULTNAME erzeugt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Antwort von SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Antwort von SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |
| _REQUEST_3 | binary | Hex-Antwort von SG |
| _RESPONSE_3 | binary | Hex-Antwort von SG |

<a id="job-status-ews"></a>
### STATUS_EWS

Zurücklesen verschiedener interner Stati für EWS UDS   : $22   ReadDataByIdentifier UDS   : $C000 Sub-Parameter

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIAGSG | string | Diagnose Steuergerät zulässig DME, DME2, EGS ohne Eintrag wird Original-Diagnoseadresse verwendet |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS3_CAPABLE | int | 0 Das SG beherrscht kein EWS3 1 Das SG beherrscht EWS3 |
| STAT_EWS4_CAPABLE | int | 0 Das SG beherrscht kein EWS4 1 Das SG beherrscht EWS4 |
| STAT_EWS3_ACTIVE | int | 0 EWS3 ist nicht (mehr) aktiv 1 EWS3 ist aktiv (oder lässt sich aktivieren) |
| STAT_EWS4_ACTIVE | int | 0 EWS4 ist nicht aktiv 1 EWS4 ist aktiv |
| STAT_EWS4_SERVER_SK_LOCKED | int | 0 SecretKey server lässt sich noch direkt schreiben 1 SecretKey server lässt sich nicht mehr schreiben/lesen |
| STAT_EWS4_CLIENT_SK_LOCKED | int | 0 SecretKey client lässt sich noch direkt schreiben 1 SecretKey client lässt sich nicht mehr schreiben/lesen |
| STAT_CLIENT_AUTHENTICATED | int | 0 Freigabe von Zuendung und Einspritzung (noch) nicht erteilt (noch nicht versucht oder Kommunikation gestört, Motorlauf gesperrt) 1 Freigabe von Zuendung und Einspritzung erteilt (Challenge-Response erfolgreich) 2 Freigabe von Zuendung und Einspritzung abgelehnt (Challenge-Response fehlgeschlagen, falsche Response, Kommunikation i.O.) 3 nicht definiert |
| STAT_CLIENT_AUTHENTICATED_TXT | string | Text zu Status Wert |
| STAT_FREE_SK0 | int | 0..0xFD Freie Flashablagen 0xFE    Freie Flashablage nicht begrenzt 0xFF    Fehlerkennzeichnung |
| _STAT_FREE_SK0_TXT | string | Freie Plaetze |
| STAT_FREE_SK1 | int | 0..0xFD Freie Flashablagen 0xFE    Freie Flashablage nicht begrenzt 0xFF    Fehlerkennzeichnung |
| _STAT_FREE_SK1_TXT | string | Freie Plaetze |
| STAT_VERSION | int | 0x01 Direktschreiben des SecretKey 0x02 Direktschreiben des SecretKey und DH-Abgleich |
| _STAT_VERSION_TXT | string | Version |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ll-abgleich"></a>
### STATUS_LL_ABGLEICH

0x225FF0 STATUS_LL_ABGLEICH Abgleichwert LL (Leerlauf) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFS_ACC_DRI_WERT | long | Abgleichswert LL mit Klima und Fahrbedingung N_KWP_OFS_ACC_DRI   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_ACC_DRI_EINH | string | rpm |
| STAT_OFS_DRI_WERT | long | Abgleichswert LL mit Fahrstufe N_KWP_OFS_DRI   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_DRI_EINH | string | rpm |
| STAT_OFS_WERT | long | Abgleichswert LL N_KWP_OFS   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_EINH | string | rpm |
| STAT_OFS_ACC_WERT | long | Abgleichswert LL mit Klimaanlage N_KWP_OFS_ACC   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_ACC_EINH | string | rpm |
| STAT_OFS_VB_WERT | long | Abgleichswert LL mit niedriger Batteriespannung N_KWP_OFS_VB   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_VB_EINH | string | rpm |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-atl"></a>
### STATUS_SYSTEMCHECK_ATL

0x3103F0D0 STATUS_SYSTEMCHECK_ATL Diagnosefunktion Abgasturbolader auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1_TEXT | string | Status waehrend der Diagnose der ATL (A2L-Name: St_atlsvc) St_atlsvc   Min: 0 Max: 9 |
| STAT_DIAGNOSE_1_WERT | int | Status waehrend der Diagnose der ATL (A2L-Name: St_atlsvc) St_atlsvc   Min: 0 Max: 9 |
| STAT_DIAGNOSE_2_TEXT | string | Ergebis der Diagnosefunktion der ATL (A2L-Name: St_atlsvc_pvdk) St_atlsvc_pvdk   Min: 0 Max: 5 |
| STAT_DIAGNOSE_2_WERT | int | Ergebis der Diagnosefunktion der ATL (A2L-Name: St_atlsvc_pvdk) St_atlsvc_pvdk   Min: 0 Max: 5 |
| STAT_AMP_WERT | real | Umgebungsdruck (measured or adapted) (A2L-Name: amp) AMP   Einheit: hPa   Min: 0 Max: 5434.25976563 |
| STAT_AMP_EINH | string | hPa |
| STAT_TAM_WERT | real | Umgebungstemperatur (A2L-Name: tam) TAM   Einheit: C   Min: -48 Max: 142.5 |
| STAT_TAM_EINH | string | degreeC |
| STAT_TIA_WERT | real | Ansauglufttemperatur (A2L-Name: tia) TIA   Einheit: C   Min: -48 Max: 142.5 |
| STAT_TIA_EINH | string | degreeC |
| STAT_ATLSVC_DPVDK1_WERT | real | Differenzdruck vor DK beider Turbolader (A2L-Name: Atlsvc_dpvdk1) ATLSVC_DPVDK1   Einheit: hPa   Min: -4096 Max: 4095.875 |
| STAT_ATLSVC_DPVDK1_EINH | string | hPa |
| STAT_ATLSVC_DPVDK2_WERT | real | Differenzdruck vor DK mit Turbolader 1 (A2L-Name: Atlsvc_dpvdk2) ATLSVC_DPVDK2   Einheit: hPa   Min: -4096 Max: 4095.875 |
| STAT_ATLSVC_DPVDK2_EINH | string | hPa |
| STAT_ATLSVC_DPVDK3_WERT | real | Differenzdruck vor DK mit Turbolader 2 (A2L-Name: Atlsvc_dpvdk3) ATLSVC_DPVDK3   Einheit: hPa   Min: -4096 Max: 4095.875 |
| STAT_ATLSVC_DPVDK3_EINH | string | hPa |
| STAT_PWG_IST_WERT | real | Pedalwert Fahrerwunsch in % (A2L-Name: Pwg_ist) Pwg_ist   Einheit: %   Min: -800 Max: 799.9755 |
| STAT_PWG_IST_EINH | string | percent |
| STAT_TN_ABSTELL | unsigned long | Abstellzeit (A2L-Name: Tn_abstell) Tn_abstell   Min: 0 Max: 65535 |
| STAT_B_KUPP_TEXT | string | Bedingung Kupplungsbetaetigung ueber Schalter oder Modell (A2L-Name: St_bgkuppl.B_kupp) B_KUPP   Min: 0 Max: 1 |
| STAT_B_KUPP_WERT | int | Bedingung Kupplungsbetaetigung ueber Schalter oder Modell (A2L-Name: St_bgkuppl.B_kupp) B_KUPP   Min: 0 Max: 1 |
| STAT_GANGI | unsigned long | Aktueller Gang intern (A2L-Name: Gangi) Gangi   Min: 0 Max: 255 |
| STAT_V_WERT | unsigned long | Fahrzeuggeschwindigkeit (A2L-Name: V) V   Einheit: km/h   Min: 0 Max: 360 |
| STAT_V_EINH | string | kmperh |
| STAT_TMOT_WERT | real | Kuehlwassertemperatur (A2L-Name: Tmot) TMOT   Einheit: C   Min: -327.68 Max: 327.67 |
| STAT_TMOT_EINH | string | degreeC |
| STAT_PU_WERT | real | Umgebungsdruck (A2L-Name: Pu) PU   Einheit: hPa   Min: 0 Max: 2559.9609 |
| STAT_PU_EINH | string | hPa |
| STAT_LV_ERR_PUT_EL | unsigned long | Elektrischer Fehler erkannt (A2L-Name: lv_err_put_el) LV_ERR_PUT_EL   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ctg"></a>
### STATUS_CTG

0x22409B STATUS_CTG CtG-Conti: Bereitstellung der Statistiken von Diagnoseergebnissen von Close-the-Gap fuer das Feldmonitoring fuer MSD80/87 (N53-54 / N74) und MSV80 (N51-52KP). !!! Wegen Umrechnungsfehler in Include (Rest) definiert !!!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VLS_DOWN_PUE_PUC_GRD_MES_L2R_MAX_0_WERT | long | Maxwert aller Diagnoseergebnisse, Gapping VLS_DOWN_PUE_PUC_GRD_MES_L2R_MAX_(MST)[0]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_PUE_PUC_GRD_MES_L2R_MAX_0_EINH | string | mVpers |
| STAT_VLS_DOWN_PUE_PUC_GRD_PUC_MAX_0_WERT | long | Maxwert aller Diagnoseergebnisse, Schub VLS_DOWN_PUE_PUC_GRD_PUC_MAX_(MST)[0]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_PUE_PUC_GRD_PUC_MAX_0_EINH | string | mVpers |
| STAT_VLS_DOWN_GRD_L2R_SAE_MIN_0_WERT | long | Minwert aller Diagnoseergebnisse, Schleppzeiger ueber alle DC. VLS_DOWN_GRD_L2R_SAE_MIN_(MST)[0]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_GRD_L2R_SAE_MIN_0_EINH | string | mVpers |
| STAT_VLS_DOWN_GRD_L2R_SAE_MMV_0_WERT | long | Mittelwert aller Diagnoseergebnisse, gebildet aus dem SAE Wert. VLS_DOWN_GRD_L2R_SAE_MMV_(MST)[0]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_GRD_L2R_SAE_MMV_0_EINH | string | mVpers |
| STAT_VLS_DOWN_GRD_L2R_SAE_STD_0_WERT | real | Standardabweichung aller Diagnoseergebnisse. VLS_DOWN_GRD_L2R_SAE_STD_(MST)[0]   Einheit: (V/s)   Min: 0 Max: 549755.81376 |
| STAT_VLS_DOWN_GRD_L2R_SAE_STD_0_EINH | string | lparenthesisVpersrparenthesisquadrat |
| STAT_VLS_DOWN_GRD_L2R_SAE_0_WERT | long | Endwert der Diagnose aktueller DC. VLS_DOWN_GRD_L2R_SAE_(MST)[1]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_GRD_L2R_SAE_0_EINH | string | mVpers |
| STAT_VLS_DOWN_PUE_PUC_GRD_MES_L2R_MAX_1_WERT | long | Maxwert aller Diagnoseergebnisse, Gapping. VLS_DOWN_PUE_PUC_GRD_MES_L2R_MAX_(MST)[1]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_PUE_PUC_GRD_MES_L2R_MAX_1_EINH | string | mVpers |
| STAT_VLS_DOWN_PUE_PUC_GRD_PUC_MAX_1_WERT | long | Maxwert aller Diagnoseergebnisse, Schub. VLS_DOWN_PUE_PUC_GRD_PUC_MAX_(MST)[1]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_PUE_PUC_GRD_PUC_MAX_1_EINH | string | mVpers |
| STAT_VLS_DOWN_GRD_L2R_SAE_MIN_1_WERT | long | Minwert aller Diagnoseergebnisse, Schleppzeiger ueber alle DC. VLS_DOWN_GRD_L2R_SAE_MIN_(MST)[1]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_GRD_L2R_SAE_MIN_1_EINH | string | mVpers |
| STAT_VLS_DOWN_GRD_L2R_SAE_MMV_1_WERT | long | Mittelwert aller Diagnoseergebnisse, gebildet aus dem SAE Wert. VLS_DOWN_GRD_L2R_SAE_MMV_(MST)[1]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_GRD_L2R_SAE_MMV_1_EINH | string | mVpers |
| STAT_VLS_DOWN_GRD_L2R_SAE_STD_1_WERT | real | Standardabweichung aller Diagnoseergebnisse. VLS_DOWN_GRD_L2R_SAE_STD_(MST)[1]   Einheit: (V/s)   Min: 0 Max: 549755.81376 |
| STAT_VLS_DOWN_GRD_L2R_SAE_STD_1_EINH | string | lparenthesisVpersrparenthesisquadrat |
| STAT_VLS_DOWN_GRD_L2R_SAE_1_WERT | long | Endwert der Diagnose aktueller DC. VLS_DOWN_GRD_L2R_SAE_(MST)[2]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_GRD_L2R_SAE_1_EINH | string | mVpers |
| STAT_VLS_DOWN_ACT_GRD_R2L_AFL_MAX_0_WERT | long | Maxwert aller Diagnoseergebnisse, Gapping (MAX-Wert ist der Kleinste, da Diagnoseergebnisse negativ sind). VLS_DOWN_ACT_GRD_R2L_AFL_MAX_(MST)[0]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_ACT_GRD_R2L_AFL_MAX_0_EINH | string | mVpers |
| STAT_VLS_DOWN_ACT_GRD_R2L_PUC_MAX_0_WERT | long | Maxwert aller Diagnoseergebnisse, Schub (MAX-Wert ist der Kleinste, da Diagnoseergebnisse negativ sind). VLS_DOWN_ACT_GRD_R2L_PUC_MAX_(MST)[0]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_ACT_GRD_R2L_PUC_MAX_0_EINH | string | mVpers |
| STAT_VLS_DOWN_GRD_R2L_SAE_MMV_0_WERT | long | Mittelwert aller Diagnoseergebnisse, gebildet aus dem SAE Wert. VLS_DOWN_GRD_R2L_SAE_MMV_(MST)[0]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_GRD_R2L_SAE_MMV_0_EINH | string | mVpers |
| STAT_VLS_DOWN_GRD_R2L_SAE_STD_0_WERT | real | Standardabweichung aller Diagnoseergebnisse. VLS_DOWN_GRD_R2L_SAE_STD_(MST)[0]   Einheit: (V/s)   Min: 0 Max: 549755.81376 |
| STAT_VLS_DOWN_GRD_R2L_SAE_STD_0_EINH | string | lparenthesisVpersrparenthesisquadrat |
| STAT_VLS_DOWN_GRD_R2L_SAE_0_WERT | long | Endwert der Diagnose aktueller DC. VLS_DOWN_GRD_R2L_SAE_(MST)[1]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_GRD_R2L_SAE_0_EINH | string | mVpers |
| STAT_VLS_DOWN_ACT_GRD_R2L_AFL_MAX_1_WERT | long | Maxwert aller Diagnoseergebnisse, Gapping (MAX-Wert ist der Kleinste, da Diagnoseergebnisse negativ sind). VLS_DOWN_ACT_GRD_R2L_AFL_MAX_(MST)[1]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_ACT_GRD_R2L_AFL_MAX_1_EINH | string | mVpers |
| STAT_VLS_DOWN_ACT_GRD_R2L_PUC_MAX_1_WERT | long | Maxwert aller Diagnoseergebnisse, Schub (MAX-Wert ist der Kleinste, da Diagnoseergebnisse negativ sind). VLS_DOWN_ACT_GRD_R2L_PUC_MAX_(MST)[1]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_ACT_GRD_R2L_PUC_MAX_1_EINH | string | mVpers |
| STAT_VLS_DOWN_GRD_R2L_SAE_MMV_1_WERT | long | Mittelwert aller Diagnoseergebnisse, gebildet aus dem SAE Wert. VLS_DOWN_GRD_R2L_SAE_MMV_(MST)[1]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_GRD_R2L_SAE_MMV_1_EINH | string | mVpers |
| STAT_VLS_DOWN_GRD_R2L_SAE_STD_1_WERT | real | Standardabweichung aller Diagnoseergebnisse. VLS_DOWN_GRD_R2L_SAE_STD_(MST)[1]   Einheit: (V/s)   Min: 0 Max: 549755.81376 |
| STAT_VLS_DOWN_GRD_R2L_SAE_STD_1_EINH | string | lparenthesisVpersrparenthesisquadrat |
| STAT_VLS_DOWN_GRD_R2L_SAE_1_WERT | long | Endwert der Diagnose aktueller DC. VLS_DOWN_GRD_R2L_SAE_(MST)[2]   Einheit: mV/s   Min: -65536 Max: 65534 |
| STAT_VLS_DOWN_GRD_R2L_SAE_1_EINH | string | mVpers |
| STAT_T_VLS_DOWN_DLY_DIAG_R2L_MAX_0_WERT | real | Maxwert aller Diagnoseergebnisse. T_VLS_DOWN_DLY_DIAG_R2L_MAX_(MST)[0]   Einheit: s   Min: 0 Max: 655.35 |
| STAT_T_VLS_DOWN_DLY_DIAG_R2L_MAX_0_EINH | string | s |
| STAT_T_VLS_DOWN_DLY_R2L_MMV_0_WERT | real | Mittelwert aller Diagnoseergebnisse, gebildet aus dem SAE Wert. T_VLS_DOWN_DLY_R2L_MMV_(MST)[0]   Einheit: s   Min: 0 Max: 655.35 |
| STAT_T_VLS_DOWN_DLY_R2L_MMV_0_EINH | string | s |
| STAT_T_VLS_DOWN_DLY_R2L_STD_0 | unsigned long | Standardabweichung aller Diagnoseergebnisse, gebildet aus dem SAE Wert (Umrechnung wird vom Zulieferer benoetigt). T_VLS_DOWN_DLY_R2L_STD_(MST)[0]   Min: 0 Max: 65535 |
| STAT_T_VLS_DOWN_DLY_R2L_SAE_0_WERT | real | Endwert der Diagnose aktueller DC. T_VLS_DOWN_DLY_R2L_SAE_(MST)[1]   Einheit: s   Min: 0 Max: 655.35 |
| STAT_T_VLS_DOWN_DLY_R2L_SAE_0_EINH | string | s |
| STAT_T_VLS_DOWN_DLY_DIAG_R2L_MAX_1_WERT | real | Maxwert aller Diagnoseergebnisse. T_VLS_DOWN_DLY_DIAG_R2L_MAX_(MST)[1]   Einheit: s   Min: 0 Max: 655.35 |
| STAT_T_VLS_DOWN_DLY_DIAG_R2L_MAX_1_EINH | string | s |
| STAT_T_VLS_DOWN_DLY_R2L_MMV_1_WERT | real | Mittelwert aller Diagnoseergebnisse, gebildet aus dem SAE Wert. T_VLS_DOWN_DLY_R2L_MMV_(MST)[1]   Einheit: s   Min: 0 Max: 655.35 |
| STAT_T_VLS_DOWN_DLY_R2L_MMV_1_EINH | string | s |
| STAT_T_VLS_DOWN_DLY_R2L_STD_1 | unsigned long | Endwert der Diagnose aktueller DC (Umrechnung wird vom Zulieferer benoetigt). T_VLS_DOWN_DLY_R2L_STD_(MST)[1]   Min: 0 Max: 65535 |
| STAT_T_VLS_DOWN_DLY_R2L_SAE_1_WERT | real | Endwert der Diagnose aktueller DC T_VLS_DOWN_DLY_R2L_SAE_(MST)[2]   Einheit: s   Min: 0 Max: 655.35 |
| STAT_T_VLS_DOWN_DLY_R2L_SAE_1_EINH | string | s |
| STAT_T_VLS_DOWN_DLY_DIAG_L2R_MAX_0_WERT | real | Maxwert aller Diagnoseergebnisse. T_VLS_DOWN_DLY_DIAG_L2R_MAX_(MST)[0]   Einheit: s   Min: 0 Max: 655.35 |
| STAT_T_VLS_DOWN_DLY_DIAG_L2R_MAX_0_EINH | string | s |
| STAT_T_VLS_DOWN_DLY_L2R_STD_0 | unsigned long | Mittelwert aller Diagnoseergebnisse, gebildet aus dem SAE Wert. T_VLS_DOWN_DLY_L2R_STD_(MST)[0]   Min: 0 Max: 65535 |
| STAT_T_VLS_DOWN_DLY_L2R_MMV_0_WERT | real | Standardabweichung aller Diagnoseergebnisse, gebildet aus dem SAE Wert (Umrechnung wird vom Zulieferer benoetigt). T_VLS_DOWN_DLY_L2R_MMV_(MST)[0]   Einheit: s   Min: 0 Max: 655.35 |
| STAT_T_VLS_DOWN_DLY_L2R_MMV_0_EINH | string | s |
| STAT_T_VLS_DOWN_DLY_L2R_SAE_0_WERT | real | Endwert der Diagnose aktueller DC T_VLS_DOWN_DLY_L2R_SAE_(MST)[1]   Einheit: s   Min: 0 Max: 655.35 |
| STAT_T_VLS_DOWN_DLY_L2R_SAE_0_EINH | string | s |
| STAT_T_VLS_DOWN_DLY_DIAG_L2R_MAX_1_WERT | real | Maxwert aller Diagnoseergebnisse T_VLS_DOWN_DLY_DIAG_L2R_MAX_(MST)[1]   Einheit: s   Min: 0 Max: 655.35 |
| STAT_T_VLS_DOWN_DLY_DIAG_L2R_MAX_1_EINH | string | s |
| STAT_T_VLS_DOWN_DLY_L2R_MMV_1_WERT | real | Mittelwert aller Diagnoseergebnisse, gebildet aus dem SAE Wert T_VLS_DOWN_DLY_L2R_MMV_(MST)[1]   Einheit: s   Min: 0 Max: 655.35 |
| STAT_T_VLS_DOWN_DLY_L2R_MMV_1_EINH | string | s |
| STAT_T_VLS_DOWN_DLY_L2R_STD_1 | unsigned long | Standardabweichung aller Diagnoseergebnisse, gebildet aus dem SAE Wert (Umrechnung wird vom Zulieferer benoetigt). T_VLS_DOWN_DLY_L2R_STD_(MST)[1]   Min: 0 Max: 65535 |
| STAT_T_VLS_DOWN_DLY_L2R_SAE_1_WERT | real | Endwert der Diagnose aktueller DC T_VLS_DOWN_DLY_L2R_SAE_(MST)[2]   Einheit: s   Min: 0 Max: 655.35 |
| STAT_T_VLS_DOWN_DLY_L2R_SAE_1_EINH | string | s |
| STAT_VLS_DOWN_PEAK_MIN_SAE_MIN_0_WERT | real | Minimalwert VLS_PEAK_MIN, Abspeichern am Ende des DC VLS_DOWN_PEAK_MIN_SAE_MIN_(MST)[0]   Einheit: V   Min: 0 Max: 9.999847410471 |
| STAT_VLS_DOWN_PEAK_MIN_SAE_MIN_0_EINH | string | V |
| STAT_VLS_DOWN_PEAK_MIN_SAE_MMV_0_WERT | real | Mittelwert aller Diagnoseergebnisse VLS_DOWN_PEAK_MIN_SAE_MMV_(MST)[0]   Einheit: V   Min: 0 Max: 9.999847410471 |
| STAT_VLS_DOWN_PEAK_MIN_SAE_MMV_0_EINH | string | V |
| STAT_VLS_DOWN_PEAK_MIN_SAE_MAX_0_WERT | real | Maximalwert von VLS_PEAK_MIN_SAVE VLS_DOWN_PEAK_MIN_SAE_MAX_(MST)[0]   Einheit: V   Min: 0 Max: 9.999847410471 |
| STAT_VLS_DOWN_PEAK_MIN_SAE_MAX_0_EINH | string | V |
| STAT_VLS_DOWN_PEAK_MIN_SAE_MIN_1_WERT | real | Minimalwert VLS_PEAK_MIN, Abspeichern am Ende des DC VLS_DOWN_PEAK_MIN_SAE_MIN_(MST)[1]   Einheit: V   Min: 0 Max: 9.999847410471 |
| STAT_VLS_DOWN_PEAK_MIN_SAE_MIN_1_EINH | string | V |
| STAT_VLS_DOWN_PEAK_MIN_SAE_MMV_1_WERT | real | Mittelwert aller Diagnoseergebnisse. VLS_DOWN_PEAK_MIN_SAE_MMV_(MST)[1]   Einheit: V   Min: 0 Max: 9.999847410471 |
| STAT_VLS_DOWN_PEAK_MIN_SAE_MMV_1_EINH | string | V |
| STAT_VLS_DOWN_PEAK_MIN_SAE_MAX_1_WERT | real | Maximalwert von VLS_PEAK_MIN_SAVE VLS_DOWN_PEAK_MIN_SAE_MAX_(MST)[1]   Einheit: V   Min: 0 Max: 9.999847410471 |
| STAT_VLS_DOWN_PEAK_MIN_SAE_MAX_1_EINH | string | V |
| STAT_VLS_DOWN_PEAK_MAX_SAE_MAX_0_WERT | real | Maximalwert VLS_PEAK_MAX, Abspeichern am Ende des DC VLS_DOWN_PEAK_MAX_SAE_MAX_(MST)[0]   Einheit: V   Min: 0 Max: 9.999847410471 |
| STAT_VLS_DOWN_PEAK_MAX_SAE_MAX_0_EINH | string | V |
| STAT_VLS_DOWN_PEAK_MAX_SAE_MMV_0_WERT | real | Mittelwert aller Diagnoseergebnisse VLS_DOWN_PEAK_MAX_SAE_MMV_(MST)[0]   Einheit: V   Min: 0 Max: 9.999847410471 |
| STAT_VLS_DOWN_PEAK_MAX_SAE_MMV_0_EINH | string | V |
| STAT_VLS_DOWN_PEAK_MAX_SAE_MIN_0_WERT | real | Minimalwert von VLS_PEAK_MAX_SAVE VLS_DOWN_PEAK_MAX_SAE_MIN_(MST)[0]   Einheit: V   Min: 0 Max: 9.999847410471 |
| STAT_VLS_DOWN_PEAK_MAX_SAE_MIN_0_EINH | string | V |
| STAT_VLS_DOWN_PEAK_MAX_SAE_MAX_1_WERT | real | Maximalwert VLS_PEAK_MAX, Abspeichern am Ende des DC VLS_DOWN_PEAK_MAX_SAE_MAX_(MST)[1]   Einheit: V   Min: 0 Max: 9.999847410471 |
| STAT_VLS_DOWN_PEAK_MAX_SAE_MAX_1_EINH | string | V |
| STAT_VLS_DOWN_PEAK_MAX_SAE_MMV_1_WERT | real | Mittelwert aller Diagnoseergebnisse VLS_DOWN_PEAK_MAX_SAE_MMV_(MST)[1]   Einheit: V   Min: 0 Max: 9.999847410471 |
| STAT_VLS_DOWN_PEAK_MAX_SAE_MMV_1_EINH | string | V |
| STAT_VLS_DOWN_PEAK_MAX_SAE_MIN_1_WERT | real | Minimalwert von VLS_PEAK_MAX_SAVE VLS_DOWN_PEAK_MAX_SAE_MIN_(MST)[1]   Einheit: V   Min: 0 Max: 9.999847410471 |
| STAT_VLS_DOWN_PEAK_MAX_SAE_MIN_1_EINH | string | V |
| STAT_RATIO_O2L_LIM_CAT_GAP_AFL_MIN_0_WERT | real | kleinster aus allen DC, Schleppzeiger RATIO_O2L_LIM_CAT_GAP_AFL_MIN_(MST)[0]   Min: 0 Max: 1023.99999976 |
| STAT_RATIO_O2L_LIM_CAT_GAP_AFL_MMV_0_WERT | real | Mittelwert aller Diagnoseergebnisse RATIO_O2L_LIM_CAT_GAP_AFL_MMV_(MST)[0]   Min: 0 Max: 1023.99999976 |
| STAT_EFF_CAT_DIAG_OBD_0_WERT | real | Endwert der Diagnose aktueller DC EFF_CAT_DIAG_OBD_(MST)[1]   Min: 0 Max: 1.9921875 |
| STAT_EFF_CAT_DIAG_OBD_MMV_0_WERT | real | Mittelwert aller Diagnoseergebnisse EFF_CAT_DIAG_OBD_MMV_(MST)[0]   Min: 0 Max: 1.9921875 |
| STAT_EFF_CAT_DIAG_OBD_STD_0 | unsigned long | Mittelwert aller Diagnoseergebnisse EFF_CAT_DIAG_OBD_STD_(MST)[0]   Min: 0 Max: 255 |
| STAT_RATIO_O2L_LIM_CAT_GAP_AFL_MIN_1_WERT | real | kleinster aus allen DC, Schleppzeiger RATIO_O2L_LIM_CAT_GAP_AFL_MIN_(MST)[1]   Min: 0 Max: 1023.99999976 |
| STAT_RATIO_O2L_LIM_CAT_GAP_AFL_MMV_1_WERT | real | Mittelwert aller Diagnoseergebnisse RATIO_O2L_LIM_CAT_GAP_AFL_MMV_(MST)[1]   Min: 0 Max: 1023.99999976 |
| STAT_EFF_CAT_DIAG_OBD_1_WERT | real | Endwert der Diagnose aktueller DC EFF_CAT_DIAG_OBD_(MST)[2]   Min: 0 Max: 1.9921875 |
| STAT_EFF_CAT_DIAG_OBD_MMV_1_WERT | real | Mittelwert aller Diagnoseergebnisse EFF_CAT_DIAG_OBD_MMV_(MST)[1]   Min: 0 Max: 1.9921875 |
| STAT_EFF_CAT_DIAG_OBD_STD_1 | unsigned long | Standardabweichung (Umrechnung wird vom Zulieferer benoetigt). EFF_CAT_DIAG_OBD_STD_(MST)[1]   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dfdsprofle"></a>
### STATUS_DFDSPROFLE

Generatorauslastungsprofil auslesen DFDSPROFLE (0x22 4081)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DFDSPROFLE_0 | unsigned char | Generatorauslastungsprofil 0 a2l-Name: dfdsprofle [0] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_1 | unsigned char | Generatorauslastungsprofil 1 a2l-Name: dfdsprofle [1] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_2 | unsigned char | Generatorauslastungsprofil 2 a2l-Name: dfdsprofle [2] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_3 | unsigned char | Generatorauslastungsprofil 3 a2l-Name: dfdsprofle [3] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_4 | unsigned char | Generatorauslastungsprofil 4 a2l-Name: dfdsprofle [4] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_5 | unsigned char | Generatorauslastungsprofil 5 a2l-Name: dfdsprofle [5] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_6 | unsigned char | Generatorauslastungsprofil 6 a2l-Name: dfdsprofle [6] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_7 | unsigned char | Generatorauslastungsprofil 7 a2l-Name: dfdsprofle [7] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_8 | unsigned char | Generatorauslastungsprofil 8 a2l-Name: dfdsprofle [8] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_9 | unsigned char | Generatorauslastungsprofil 9 a2l-Name: dfdsprofle [9] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_10 | unsigned char | Generatorauslastungsprofil 10 a2l-Name: dfdsprofle [10] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_11 | unsigned char | Generatorauslastungsprofil 11 a2l-Name: dfdsprofle [11] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_12 | unsigned char | Generatorauslastungsprofil 12 a2l-Name: dfdsprofle [12] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_13 | unsigned char | Generatorauslastungsprofil 13 a2l-Name: dfdsprofle [13] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_14 | unsigned char | Generatorauslastungsprofil 14 a2l-Name: dfdsprofle [14] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_15 | unsigned char | Generatorauslastungsprofil 15 a2l-Name: dfdsprofle [15] Min: 0.0 Max: 255.0 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei "ERROR", wenn nicht fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-vanosspuelen"></a>
### STATUS_VANOSSPUELEN

0x3103F042 STATUS_VANOSSPUELEN VANOS Spuelen fuer OBD und PVE.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_VANOSSPUELEN_TEXT | string | FUNKTIONSSTATUS VANOSSPUELEN 1BYTE FUNKTIONSSTATUS |
| STAT_FS_VANOSSPUELEN_WERT | int | FUNKTIONSSTATUS VANOSSPUELEN 1BYTE FUNKTIONSSTATUS |
| STAT_NMOT_W_WERT | real | Motordrehzahl soll zws. der unteren Drehzahlgrenze (ca. 100 rpm unter LL-Solldrehzahl. Default= 1000 rpm) und der oberen Drehzahlgrenze (ca. 100 rpm ueber LL-Solldrehzahl. Default = 1200 rpm) sein. nmot_w   Einheit: 1/min   Min: 0 Max: 10000 |
| STAT_NMOT_W_EINH | string | 1permin |
| STAT_V_WERT | unsigned long | Fahrzeuggeschwindigkeit soll zws. 0 und 100 Km/h liegen. Default = 0 V   Einheit: km/h   Min: 0 Max: 360 |
| STAT_V_EINH | string | kmperh |
| STAT_ST_LL | unsigned long | Status Leerlauf (A2L-Name: St_ll) St_ll   Min: 0 Max: 255 |
| STAT_CTR_CAM_OFS_EXT_ADJ | unsigned long | Anzahl der durchlaufenen Spuelzyklen im Funktionstest (A2L-Name: ctr_cam_ofs_ext_adj) CTR_CAM_OFS_EXT_ADJ   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-tev-regelung-aus"></a>
### STEUERN_TEV_REGELUNG_AUS

0x3101F0CF STEUERN_TEV_REGELUNG_AUS Deaktivierung TEV-Regelung starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ladungsbilanz-opf"></a>
### STATUS_LADUNGSBILANZ_OPF

0x224118 STATUS_LADUNGSBILANZ_OPF Ladungsbilanz des OPF lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_REG_BEDARF_WERT | real | Regenerationsdringlichkeit 2BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.9969482421875 |
| STAT_REG_BEDARF_EINH | string | percent |
| STAT_REG_VERURSACHER_WERT | unsigned long | Verursacher für die Regenerationsanforderung Bitcodiert 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-vorkonfig-opf"></a>
### START_VORKONFIG_OPF

0x3101F082 START_VORKONFIG_OPF Vorkonditionierung Otto Partikelfilter starten Startvorraussetzungen: Freigabe über Applikationsschalter, Geschwindigkeit , GWS N oder P (AT), Neutral (MT), Gaspedal

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-dmtl"></a>
### STOP_SYSTEMCHECK_DMTL

0x3102F0DA STOP_SYSTEMCHECK_DMTL Diagnosefunktion DMTL beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-zgh"></a>
### STEUERN_ENDE_ZGH

0x3102F034 STEUERN_ENDE_ZGH Ende Zylinder Gleichstellung Homogen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-swe-lesen"></a>
### _SWE_LESEN

0x31010205 SWE_LESEN Informationen zu Softwareeinheiten auf dem Steuergerät unter Verwendung des Jobs SVK_LESEN UDS  : $31   RoutinControl by RequestSerice ID UDS  : $01xx Sub-Parameter fuer SVK UDS  : $0205 SWEDI (Default) Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SWE_EINHEIT | string | auszulesender SWE Satz Eingabe von 0 bis 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| IST_REFERENZ | string | Referenz die zum Auslesen verwendet wird |
| REFERENZ_ANZ | int | Anzahl der Referenzen auf die sich die Softwareeinheit bezieht |
| REF_PROZESSKLASSE | string | Prozessklasse |
| REF_SGBM_ID | string | Steuergeräte Daten-Index |
| VERSION | string | Version der Hareware oder Softwareeinheit |
| INFO_FELD | string | gesamter string ab dem Bordnetzteilnehmer |
| REFERENZ_1 | string | Referenz 1 im Software-Development Infofeld |
| REFERENZ_2 | string | Referenz 2 im Software-Development Infofeld |
| REFERENZ_3 | string | Referenz 3 im Software-Development Infofeld |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-adaption-gemisch"></a>
### STATUS_ADAPTION_GEMISCH

0x22400A STATUS_ADAPTION_GEMISCH Gemischadaptionswerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADD_1_WERT | real | fuel mass set point offset, output from lambda adaptation MFF_ADD_LAM_AD_OUT[1]   Einheit: mg/stk   Min: -640 Max: 639.98046875 |
| STAT_ADD_1_EINH | string | mgperstk |
| STAT_ADD_2_WERT | real | fuel mass set point offset, output from lambda adaptation MFF_ADD_LAM_AD_OUT[2]   Einheit: mg/stk   Min: -640 Max: 639.98046875 |
| STAT_ADD_2_EINH | string | mgperstk |
| STAT_FAC_1_WERT | real | Lambda Adaption carried out by customer (multiplicative share) FAC_LAM_AD_CUS[1]   Einheit: %   Min: -50 Max: 49.9984741210938 |
| STAT_FAC_1_EINH | string | percent |
| STAT_FAC_2_WERT | real | Lambda Adaption carried out by customer (multiplicative share) FAC_LAM_AD_CUS[2]   Einheit: %   Min: -50 Max: 49.9984741210938 |
| STAT_FAC_2_EINH | string | percent |
| STAT_PWM_UP_1_WERT | real | Heater driver PWM duty cycle  acquired also by BSW LSHPWM_UP[1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_PWM_UP_1_EINH | string | percent |
| STAT_PWM_UP_2_WERT | real | Heater driver PWM duty cycle  acquired also by BSW LSHPWM_UP[2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_PWM_UP_2_EINH | string | percent |
| STAT_PWM_DOWN_1_WERT | real | Heater driver PWM duty cycle  acquired also by BSW LSHPWM_DOWN[1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_PWM_DOWN_1_EINH | string | percent |
| STAT_PWM_DOWN_2_WERT | real | Heater driver PWM duty cycle  acquired also by BSW LSHPWM_DOWN[2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_PWM_DOWN_2_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-kft"></a>
### STEUERN_ENDE_KFT

0x2F60C900 STEUERN_ENDE_KFT Kennfeldthermostat Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hist-temperatur-opf"></a>
### STATUS_HIST_TEMPERATUR_OPF

0x22411E STATUS_HIST_TEMPERATUR_OPF Temperaturverteilung des OPF lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OPF_TEMPKLASSE_1_WERT_WERT | unsigned long | OPF Verweildauer im Temperaturbetriebsbereich 1 4BYTE in 0 bis 4294967294s   Einheit: s   Min: 0 Max: 4294967294 |
| STAT_OPF_TEMPKLASSE_1_WERT_EINH | string | second |
| STAT_OPF_TEMPKLASSE_2_WERT_WERT | unsigned long | OPF Verweildauer im Temperaturbetriebsbereich 2 4BYTE in 0 bis 4294967294s   Einheit: s   Min: 0 Max: 4294967294 |
| STAT_OPF_TEMPKLASSE_2_WERT_EINH | string | second |
| STAT_OPF_TEMPKLASSE_3_WERT_WERT | unsigned long | OPF Verweildauer im Temperaturbetriebsbereich 3 4BYTE in 0 bis 4294967294s   Einheit: s   Min: 0 Max: 4294967294 |
| STAT_OPF_TEMPKLASSE_3_WERT_EINH | string | second |
| STAT_OPF_TEMPKLASSE_4_WERT_WERT | unsigned long | OPF Verweildauer im Temperaturbetriebsbereich 4 4BYTE in 0 bis 4294967294s   Einheit: s   Min: 0 Max: 4294967294 |
| STAT_OPF_TEMPKLASSE_4_WERT_EINH | string | second |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ulv"></a>
### STEUERN_ULV

0x2F60B503 STEUERN_ULV Umluftventil ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ULV_WERT | real | Tastverhaeltniss Umluftventil RFPPWM_EXT_ADJ[0]   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_ULV_WERT | unsigned long | Timeout Umluftventil 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-imaalle"></a>
### STATUS_IMAALLE

0x225F90 STATUS_IMAALLE Abgleichwerte Injektoren auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENERGIEABGLEICH_ZYL_1_WERT | real | IMA Abgleichwert Injektor 01 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[0]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_1_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_1_WERT | real | IMA Abgleichwert Injektor 01 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[0]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_1_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_7_WERT | real | IMA Abgleichwert Injektor 07 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[1]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_7_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_7_WERT | real | IMA Abgleichwert Injektor 07 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[1]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_7_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_5_WERT | real | IMA Abgleichwert Injektor 05 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[2]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_5_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_5_WERT | real | IMA Abgleichwert Injektor 05 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[2]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_5_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_11_WERT | real | IMA Abgleichwert Injektor 11 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[3]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_11_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_11_WERT | real | IMA Abgleichwert Injektor 11 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[3]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_11_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_3_WERT | real | IMA Abgleichwert Injektor 03 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[4]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_3_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_3_WERT | real | IMA Abgleichwert Injektor 03 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[4]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_3_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_9_WERT | real | IMA Abgleichwert Injektor 09 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[5]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_9_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_9_WERT | real | IMA Abgleichwert Injektor 09 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[5]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_9_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_6_WERT | real | IMA Abgleichswert Injektor 06 Flow 1 (Energie) EGY_SP_IV_EXT_ADJ[6]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_6_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_6_WERT | real | IMA Abgleichwert Injektor 06 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[6]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_6_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_12_WERT | real | IMA Abgleichwert Injektor 12 Flow1 (Energie) ) EGY_SP_IV_EXT_ADJ[7]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_12_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_12_WERT | real | IMA Abgleichwert Injektor 12 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[9]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_12_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_2_WERT | real | IMA Abgleichwert Injektor 02 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[8]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_2_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_2_WERT | real | IMA Abgleichwert Injektor 02 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[6]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_2_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_8_WERT | real | IMA Abgleichwert Injektor 08 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[9]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_8_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_8_WERT | real | IMA Abgleichwert Injektor 08 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[9]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_8_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_4_WERT | real | IMA Abgleichwert Injektor 04 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[10]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_4_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_4_WERT | real | IMA Abgleichwert Injektor 04 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[10]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_4_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_10_WERT | real | IMA Abgleichwert Injektor 10 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[11]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_10_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_10_WERT | real | IMA Abgleichwert Injektor 10 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[11]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_10_EINH | string | mgperstk |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-atldiag"></a>
### STATUS_ATLDIAG

0x224044 STATUS_ATLDIAG Turboladerstatus auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ATLDIAG_BANK2 | unsigned long | Ladedruckdiagnose fuer Bank 2 durchgelaufen 2 Byte |
| STAT_ATLDIAG_BANK1 | unsigned long | Ladedruckdiagnose fuer Bank 1 durchgelaufen 2 Byte |
| STAT_ATLDIAG_AKTIV | unsigned long | Ladedruckdiagnose aktiv 1BIT IDENTICAL |
| STAT_BANK1_HDR | unsigned long | Turboladerdiagnose Hochdruckbereich Bank 1 durchgelaufen (A2L-Name: LV_END_DIAG_TCHA_PRS_HIGH_1) LV_END_DIAG_TCHA_PRS_HIGH_1   Min: 0 Max: 1 |
| STAT_BANK1_NDR | unsigned long | Turboladerdiagnose Niederdruckbereich Bank 1 durchgelaufen (A2L-Name: LV_END_DIAG_TCHA_PRS_LOW_1) LV_END_DIAG_TCHA_PRS_LOW_1   Min: 0 Max: 1 |
| STAT_BANK2_HDR | unsigned long | Turboladerdiagnose Hochdruckbereich Bank 2 durchgelaufen (A2L-Name: LV_END_DIAG_TCHA_PRS_HIGH_2) LV_END_DIAG_TCHA_PRS_HIGH_2   Min: 0 Max: 1 |
| STAT_BANK2_NDR | unsigned long | Turboladerdiagnose Niederdruckbereich Bank 2 durchgelaufen (A2L-Name: LV_END_DIAG_TCHA_PRS_LOW_1) LV_END_DIAG_TCHA_PRS_LOW_2   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-atl"></a>
### START_SYSTEMCHECK_ATL

0x3101F0D0 START_SYSTEMCHECK_ATL Diagnosefunktion Abgasturbolader starten 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-speicher-lesen-ascii"></a>
### SPEICHER_LESEN_ASCII

0x23 SPEICHER_LESEN_ASCII Auslesen des Steuergeraete-Speichers Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADRESSE | long | Speicherzellenadresse 0x00000000 - 0xFFFFFFFF |
| ANZAHL | int | Anzahl auszulesende Bytes 1 - n (4095) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten Sortiert |
| DATEN_ROH | binary | ausgelesene Daten in unsortiertem Zustand |
| DATEN_ASCII | string | ausgelesene Daten als ASCII Format |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ruhestrommessung"></a>
### STATUS_RUHESTROMMESSUNG

Auslesen Ruhestromprüfung mit IBS UDS  : $31 RoutineControl UDS  : $03 requestRoutineResults UDS  : $F02B Ruhestrompruefung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_RUHESTROM_TEXT | string | Funktionsstatus RUHESTROM (Eco_jobstat1) 1BYTE FUNKTIONSSTATUS |
| STAT_FS_RUHESTROM_WERT | int | Status_Fehlerspeicher_Ruhestromwert |
| STAT_FS_RUHESTROM_EINH | string | - |
| STAT_STAT_RUHESTROM_WERT | real | Ruhestrom (Eco_result1) Eco_result1   Einheit: A   Min: 0 Max: 81.9187 |
| STAT_STAT_RUHESTROM_EINH | string | A |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG (MEN48) |
| _RESPONSE | binary | Hex-Auftrag an SG (MEN48) |

<a id="job-steuern-ews4-sk"></a>
### STEUERN_EWS4_SK

17 "EWS4-data" schreiben UDS   : $2E   WriteDataByIdentifier UDS   : $C001 Sub-Parameter

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | Byte0 LOCK_SERVER_SK LOCK_CLIENT_SK WRITE_SERVER_SK WRITE_CLIENT_SK UNLOCK_CLIENT_SK |
| DATEN | string | Byte1...16 16 Byte Daten (SecretKey), falls MODE = WRITE_SERVER_SK/WRITE_CLIENT_SK, "0x01,0x02,.." KEINE Daten nötig, falls MODE = LOCK_SERVER_SK/LOCK_CLIENT_SK |
| DIAGSG | string | Diagnose Steuergerät zulässig DME, DME2, EGS ohne Eintrag wird Original-Diagnoseadresse verwendet |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-uvlss"></a>
### STEUERN_ENDE_UVLSS

0x2F602000 STEUERN_ENDE_UVLSS Versorgung Einspritzung / Zuendung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-aep-i12-test-ladeendegrund"></a>
### _STEUERN_AEP_I12_TEST_LADEENDEGRUND

Job zum Test für AEP Funktionen AEP_I12_GRUND_LADEENDE (0x2E 5FA0)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DIAG_AEP_LADEENDEGRUND | unsigned char | Schreiben von Zyknlinfodiag Min: 0.0 Max: 255.0 a2l-Name: Zyknlinfodiag |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-aep-i12-zyklisches-nachladen-info"></a>
### STATUS_AEP_I12_ZYKLISCHES_NACHLADEN_INFO

Auslesen von wichtigen Kenngrößen der letzten 4 Vorgänge des zykllischen Nachladens plus dem letzten Parkvorgang AEP_I12_ZYKLISCHES_NACHLADEN_INFO (0x22 409D)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PARKEN_SYSTEMZEIT_WERT | unsigned long | Systemzeit beim Parken Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_PARKEN_SYSTEMZEIT_EINH | string | "s" |
| STAT_PARKEN_KILOMETERSTAND_WERT | unsigned long | Kilometerstand beim Parken |
| STAT_PARKEN_KILOMETERSTAND_EINH | string | "km" |
| STAT_PARKEN_NV_BATTERIE_SOC_WERT | real | Niedervolt SOC beim Parken Einheit: % Min: 0.0 Max: 127.5 |
| STAT_PARKEN_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E1_PARKEN_SYSTEMZEIT_WERT | unsigned long | 1. Ereignis (letzte): Systemzeit beim Parken Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E1_PARKEN_SYSTEMZEIT_EINH | string | "s" |
| STAT_E1_PARKEN_KILOMETERSTAND_WERT | unsigned long | 1. Ereignis (letzte): Kilometerstand beim Parken |
| STAT_E1_PARKEN_KILOMETERSTAND_EINH | string | "km" |
| STAT_E1_PARKEN_NV_BATTERIE_SOC_WERT | real | 1. Ereignis (letzte): Niedervolt SOC beim Parken Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E1_PARKEN_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E1_START_ZYKNL_SYSTEMZEIT_WERT | unsigned long | 1. Ereignis (letzte): Systemzeit beim Start des zyklischen Nachladens Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E1_START_ZYKNL_SYSTEMZEIT_EINH | string | "s" |
| STAT_E1_START_ZYKNL_NV_BATTERIE_SOC_WERT | real | 1. Ereignis (letzte): Niedervolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E1_START_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E1_START_ZYKNL_HV_BATTERIE_SOC_WERT | real | 1. Ereignis (letzte): Hochvolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E1_START_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E1_START_ZYKNL_NV_BATTERIE_TEMPERATUR_WERT | real | 1. Ereignis (letzte): Temperatur der Niedervolt Batterie beim Start des zyklischen Nachladens |
| STAT_E1_START_ZYKNL_NV_BATTERIE_TEMPERATUR_EINH | string | "°C" |
| STAT_E1_LADEDAUER_WERT | unsigned int | 1. Ereignis (letzte): Dauer des zyklischen Nachladens Einheit: s Min: 0.0 Max: 65535.0 |
| STAT_E1_LADEDAUER_EINH | string | "s" |
| STAT_E1_ENDE_ZYKNL_NV_BATTERIE_SOC_WERT | real | 1. Ereignis (letzte): Niedervolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E1_ENDE_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E1_ENDE_ZYKNL_HV_BATTERIE_SOC_WERT | real | 1. Ereignis (letzte): Hochvolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E1_ENDE_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E1_GRUND_LADEENDE | unsigned char | Sensorfehler eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 0 Min: 0.0 Max: 15.0 |
| STAT_E1_ZYKNL_PROGNOSE_EIN | unsigned char | Lagereglerabweichung eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 3 Min: 0.0 Max: 1.0 |
| STAT_E2_PARKEN_SYSTEMZEIT_WERT | unsigned long | 2. Ereignis: Systemzeit beim Parken Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E2_PARKEN_SYSTEMZEIT_EINH | string | "s" |
| STAT_E2_PARKEN_KILOMETERSTAND_WERT | unsigned long | 2. Ereignis: Kilometerstand beim Parken |
| STAT_E2_PARKEN_KILOMETERSTAND_EINH | string | "km" |
| STAT_E2_PARKEN_NV_BATTERIE_SOC_WERT | real | 2. Ereignis: Niedervolt SOC beim Parken Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E2_PARKEN_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E2_START_ZYKNL_SYSTEMZEIT_WERT | unsigned long | 2. Ereignis: Systemzeit beim Start des zyklischen Nachladens Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E2_START_ZYKNL_SYSTEMZEIT_EINH | string | "s" |
| STAT_E2_START_ZYKNL_NV_BATTERIE_SOC_WERT | real | 2. Ereignis: Niedervolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E2_START_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E2_START_ZYKNL_HV_BATTERIE_SOC_WERT | real | 2. Ereignis: Hochvolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E2_START_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E2_START_ZYKNL_NV_BATTERIE_TEMPERATUR_WERT | real | 2. Ereignis: Temperatur der Niedervolt Batterie beim Start des zyklischen Nachladens |
| STAT_E2_START_ZYKNL_NV_BATTERIE_TEMPERATUR_EINH | string | "°C" |
| STAT_E2_LADEDAUER_WERT | unsigned int | 2. Ereignis: Dauer des zyklischen Nachladens Einheit: s Min: 0.0 Max: 65535.0 |
| STAT_E2_LADEDAUER_EINH | string | "s" |
| STAT_E2_ENDE_ZYKNL_NV_BATTERIE_SOC_WERT | real | 2. Ereignis: Niedervolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E2_ENDE_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E2_ENDE_ZYKNL_HV_BATTERIE_SOC_WERT | real | 2. Ereignis: Hochvolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E2_ENDE_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E2_GRUND_LADEENDE | unsigned char | Sensorfehler eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 0 Min: 0.0 Max: 15.0 |
| STAT_E2_ZYKNL_PROGNOSE_EIN | unsigned char | Lagereglerabweichung eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 3 Min: 0.0 Max: 1.0 |
| STAT_E3_PARKEN_SYSTEMZEIT_WERT | unsigned long | 3. Ereignis: Systemzeit beim Parken Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E3_PARKEN_SYSTEMZEIT_EINH | string | "s" |
| STAT_E3_PARKEN_KILOMETERSTAND_WERT | unsigned long | 3. Ereignis: Kilometerstand beim Parken |
| STAT_E3_PARKEN_KILOMETERSTAND_EINH | string | "km" |
| STAT_E3_PARKEN_NV_BATTERIE_SOC_WERT | real | 3. Ereignis: Niedervolt SOC beim Parken Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E3_PARKEN_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E3_START_ZYKNL_SYSTEMZEIT_WERT | unsigned long | 3. Ereignis: Systemzeit beim Start des zyklischen Nachladens Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E3_START_ZYKNL_SYSTEMZEIT_EINH | string | "s" |
| STAT_E3_START_ZYKNL_NV_BATTERIE_SOC_WERT | real | 3. Ereignis: Niedervolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E3_START_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E3_START_ZYKNL_HV_BATTERIE_SOC_WERT | real | 3. Ereignis: Hochvolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E3_START_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E3_START_ZYKNL_NV_BATTERIE_TEMPERATUR_WERT | real | 3. Ereignis: Temperatur der Niedervolt Batterie beim Start des zyklischen Nachladens |
| STAT_E3_START_ZYKNL_NV_BATTERIE_TEMPERATUR_EINH | string | "°C" |
| STAT_E3_LADEDAUER_WERT | unsigned int | 3. Ereignis: Dauer des zyklischen Nachladens Einheit: s Min: 0.0 Max: 65535.0 |
| STAT_E3_LADEDAUER_EINH | string | "s" |
| STAT_E3_ENDE_ZYKNL_NV_BATTERIE_SOC_WERT | real | 3. Ereignis: Niedervolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E3_ENDE_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E3_ENDE_ZYKNL_HV_BATTERIE_SOC_WERT | real | 3. Ereignis: Hochvolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E3_ENDE_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E3_GRUND_LADEENDE | unsigned char | Sensorfehler eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 0 Min: 0.0 Max: 15.0 |
| STAT_E3_ZYKNL_PROGNOSE_EIN | unsigned char | Lagereglerabweichung eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 3 Min: 0.0 Max: 1.0 |
| STAT_E4_PARKEN_SYSTEMZEIT_WERT | unsigned long | 4. Ereignis: Systemzeit beim Parken Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E4_PARKEN_SYSTEMZEIT_EINH | string | "s" |
| STAT_E4_PARKEN_KILOMETERSTAND_WERT | unsigned long | 4. Ereignis: Kilometerstand beim Parken |
| STAT_E4_PARKEN_KILOMETERSTAND_EINH | string | "km" |
| STAT_E4_PARKEN_NV_BATTERIE_SOC_WERT | real | 4. Ereignis: Niedervolt SOC beim Parken Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E4_PARKEN_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E4_START_ZYKNL_SYSTEMZEIT_WERT | unsigned long | 4. Ereignis: Systemzeit beim Start des zyklischen Nachladens Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E4_START_ZYKNL_SYSTEMZEIT_EINH | string | "s" |
| STAT_E4_START_ZYKNL_NV_BATTERIE_SOC_WERT | real | 4. Ereignis: Niedervolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E4_START_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E4_START_ZYKNL_HV_BATTERIE_SOC_WERT | real | 4. Ereignis: Hochvolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E4_START_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E4_START_ZYKNL_NV_BATTERIE_TEMPERATUR_WERT | real | 4. Ereignis: Temperatur der Niedervolt Batterie beim Start des zyklischen Nachladens |
| STAT_E4_START_ZYKNL_NV_BATTERIE_TEMPERATUR_EINH | string | "°C" |
| STAT_E4_LADEDAUER_WERT | unsigned int | 4. Ereignis: Dauer des zyklischen Nachladens Einheit: s Min: 0.0 Max: 65535.0 |
| STAT_E4_LADEDAUER_EINH | string | "s" |
| STAT_E4_ENDE_ZYKNL_NV_BATTERIE_SOC_WERT | real | 4. Ereignis: Niedervolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E4_ENDE_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E4_ENDE_ZYKNL_HV_BATTERIE_SOC_WERT | real | 4. Ereignis: Hochvolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E4_ENDE_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E4_GRUND_LADEENDE | unsigned char | Sensorfehler eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 0 Min: 0.0 Max: 15.0 |
| STAT_E4_ZYKNL_PROGNOSE_EIN | unsigned char | Lagereglerabweichung eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 3 Min: 0.0 Max: 1.0 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-gvobd"></a>
### STEUERN_GVOBD

0x2E5F8007 STEUERN_GVOBD Gemischvertrimmung fuer OBD-Demo und PVE vorgeben. Der Korrekturfaktor soll bei Klemmenwechsel auf den Standardwert "1" zurueckgesetzt werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_F_MK_KORR_EXT_XZYL_1_WERT | real | Faktor auf Einspritzung Zylinder 1 F_mk_korr_ext_xzyl_[1]   Min: 0 Max: 1.99996948242188 |
| SW_F_MK_KORR_EXT_XZYL_5_WERT | real | Faktor auf Einspritzung Zylinder 5 F_mk_korr_ext_xzyl_[2]   Min: 0 Max: 1.99996948242188 |
| SW_F_MK_KORR_EXT_XZYL_3_WERT | real | Faktor auf Einspritzung Zylinder 3 F_mk_korr_ext_xzyl_[3]   Min: 0 Max: 1.99996948242188 |
| SW_F_MK_KORR_EXT_XZYL_6_WERT | real | Faktor auf Einspritzung Zylinder 6 F_mk_korr_ext_xzyl_[4]   Min: 0 Max: 1.99996948242188 |
| SW_F_MK_KORR_EXT_XZYL_2_WERT | real | Faktor auf Einspritzung Zylinder 2 F_mk_korr_ext_xzyl_[5]   Min: 0 Max: 1.99996948242188 |
| SW_F_MK_KORR_EXT_XZYL_4_WERT | real | Faktor auf Einspritzung Zylinder 4 F_mk_korr_ext_xzyl_[6]   Min: 0 Max: 1.99996948242188 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-obd-testgroup"></a>
### STATUS_OBD_TESTGROUP

0x22F813  STATUS_OBD_TESTGROUP Abfragen der Antriebsstrang Identifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTOR_GRUPPENNUMMER | string | Geprüfte Test Gruppe bzw Motor Gruppen Nummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-mfma-ds"></a>
### STATUS_MFMA_DS

0x22403E STATUS_MFMA_DS Adaptionswerte MFMA_DS Lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CTR_AD_TOT_CMB_AD_00 | unsigned long | Gesamtzahl der Verbrennungszyklen (A2L-Name: ctr_ad_tot_cmb_ad[0]) CTR_AD_TOT_CMB_AD[0]   Min: 0 Max: 65535 |
| STAT_DIST_INJ_AD_END_CMB_AD_00_WERT | real | Zeitraum zur letzten erfolgreichen Adaption (A2L-Name: dist_inj_ad_end_cmb_ad) DIST_INJ_AD_END_CMB_AD   Einheit: [km]   Min: 0 Max: 429496729.5 |
| STAT_DIST_INJ_AD_END_CMB_AD_00_EINH | string | lbracketkmrbracket |
| STAT_TI_OFS_CMB_AD_000_WERT | real | Offset der Einspritzzeit Zyl. 1 (relative to injection time map) (A2L-Name: ti_ofs_cmb_ad[0]) TI_OFS_CMB_AD[0]   Einheit: [ms]   Min: -13.1072 Max: 13.1064 |
| STAT_TI_OFS_CMB_AD_000_EINH | string | lbracketmsrbracket |
| STAT_TI_OFS_CMB_AD_016_WERT | real | Offset der Einspritzzeit Zyl. 5 (relative to injection time map) (A2L-Name: ti_ofs_cmb_ad[16]) TI_OFS_CMB_AD[16]   Einheit: [ms]   Min: -13.1072 Max: 13.1064 |
| STAT_TI_OFS_CMB_AD_016_EINH | string | lbracketmsrbracket |
| STAT_TI_OFS_CMB_AD_032_WERT | real | Offset der Einspritzzeit Zyl. 3 (relative to injection time map) (A2L-Name: ti_ofs_cmb_ad[32]) TI_OFS_CMB_AD[32]   Einheit: [ms]   Min: -13.1072 Max: 13.1064 |
| STAT_TI_OFS_CMB_AD_032_EINH | string | lbracketmsrbracket |
| STAT_TI_OFS_CMB_AD_048_WERT | real | Offset der Einspritzzeit Zyl. 6 (relative to injection time map) (A2L-Name: ti_ofs_cmb_ad[48]) TI_OFS_CMB_AD[48]   Einheit: [ms]   Min: -13.1072 Max: 13.1064 |
| STAT_TI_OFS_CMB_AD_048_EINH | string | lbracketmsrbracket |
| STAT_TI_OFS_CMB_AD_064_WERT | real | Offset der Einspritzzeit Zyl. 2 (relative to injection time map) (A2L-Name: ti_ofs_cmb_ad[64]) TI_OFS_CMB_AD[64]   Einheit: [ms]   Min: -13.1072 Max: 13.1064 |
| STAT_TI_OFS_CMB_AD_064_EINH | string | lbracketmsrbracket |
| STAT_TI_OFS_CMB_AD_080_WERT | real | Offset der Einspritzzeit Zyl. 4 (relative to injection time map) (A2L-Name: ti_ofs_cmb_ad[80]) TI_OFS_CMB_AD[80]   Einheit: [ms]   Min: -13.1072 Max: 13.1064 |
| STAT_TI_OFS_CMB_AD_080_EINH | string | lbracketmsrbracket |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-sek-luft"></a>
### STATUS_SYSTEMCHECK_SEK_LUFT

0x3103F020 STATUS_SYSTEMCHECK_SEK_LUFT Auslesen Diagnosefunktion Sekundaerluft Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATE_EOL_KWP_SA_TEXT | string | Status waehrend der Diagnose SekundÃ¤rluft (A2L-Name: state_eol_kwp_sa) STATE_EOL_KWP_SA   Min: 0 Max: 9 |
| STAT_STATE_EOL_KWP_SA_WERT | int | Status waehrend der Diagnose SekundÃ¤rluft (A2L-Name: state_eol_kwp_sa) STATE_EOL_KWP_SA   Min: 0 Max: 9 |
| STAT_STATE_DIAG_ERR_SA | unsigned long | Fehlerstatus fuer Systemcheck SekundÃ¤rluft (A2L-Name: state_diag_err_sa) STATE_DIAG_ERR_SA   Min: 0 Max: 65535 |
| STAT_STATE_DIAG_SA_INFO | unsigned long | Information about current step of the secondary air diagnosis inclunding interrupt reasons (A2L-Name: state_diag_sa_info) STATE_DIAG_SA_INFO   Min: 0 Max: 255 |
| STAT_STATE_DIAG_SA_INH_EOL | unsigned long | Bit-Vektor including the information about the reason(s) of an inhibition of an EOL-test (A2L-Name: state_diag_sa_inh_eol) STATE_DIAG_SA_INH_EOL   Min: 0 Max: 65535 |
| STAT_STATE_EOL_KWP_SA_PRG_WERT | real | Progress of secondary air system diagnosis (A2L-Name: state_eol_kwp_sa_prg) STATE_EOL_KWP_SA_PRG   Min: 0 Max: 99.9984741210938 |
| STAT_STATE_ERR_SYM_SA_EOL0 | unsigned long | Symptombit-Vector at one of the secondary air system errors for EOL-Test (A2L-Name: state_err_sym_sa_eol[0]) STATE_ERR_SYM_SA_EOL[0]   Min: 0 Max: 65535 |
| STAT_STATE_ERR_SYM_SA_EOL1 | unsigned long | Symptombit-Vector at one of the secondary air system errors for EOL-Test (A2L-Name: state_err_sym_sa_eol[1]) STATE_ERR_SYM_SA_EOL[1]   Min: 0 Max: 65535 |
| STAT_STATE_ERR_SYM_SA_EOL2 | unsigned long | Symptombit-Vector at one of the secondary air system errors for EOL-Test (A2L-Name: state_err_sym_sa_eol[2]) STATE_ERR_SYM_SA_EOL[2]   Min: 0 Max: 65535 |
| STAT_STATE_ERR_SYM_SA_EOL3 | unsigned long | Symptombit-Vector at one of the secondary air system errors for EOL-Test (A2L-Name: state_err_sym_sa_eol[3]) STATE_ERR_SYM_SA_EOL[3]   Min: 0 Max: 65535 |
| STAT_PRS_SA_DIAG_SA_ACT_1_EOL_WERT | real | Diagnosis value at activated secondary air system: secondary air pressure (bank 1) (EOL) (A2L-Name: prs_sa_diag_sa_act_1_eol) PRS_SA_DIAG_SA_ACT_1_EOL   Einheit: hPa   Min: -1280 Max: 1279.9609375 |
| STAT_PRS_SA_DIAG_SA_ACT_1_EOL_EINH | string | hPa |
| STAT_PRS_SA_DIAG_SA_ACT_2_EOL_WERT | real | Diagnosis value at activated secondary air system: secondary air pressure (bank 2) (EOL) (A2L-Name: prs_sa_diag_sa_act_2_eol) PRS_SA_DIAG_SA_ACT_2_EOL   Einheit: hPa   Min: -1280 Max: 1279.9609375 |
| STAT_PRS_SA_DIAG_SA_ACT_2_EOL_EINH | string | hPa |
| STAT_PRS_SA_DIAG_MAX_SA_ACT_1_EOL_WERT | real | Diagnosis value at activated secondary air system: secondary air pressure (bank 1) (EOL) (A2L-Name: prs_sa_diag_max_sa_act_1_eol) PRS_SA_DIAG_MAX_SA_ACT_1_EOL   Einheit: hPa   Min: -1280 Max: 1279.9609375 |
| STAT_PRS_SA_DIAG_MAX_SA_ACT_1_EOL_EINH | string | hPa |
| STAT_PRS_SA_DIAG_MAX_SA_ACT_2_EOL_WERT | real | Diagnosis value at activated secondary air system: secondary air pressure (bank 2) (EOL) (A2L-Name: prs_sa_diag_max_sa_act_2_eol) PRS_SA_DIAG_MAX_SA_ACT_2_EOL   Einheit: hPa   Min: -1280 Max: 1279.9609375 |
| STAT_PRS_SA_DIAG_MAX_SA_ACT_2_EOL_EINH | string | hPa |
| STAT_PRS_SA_DIAG_MIN_SA_ACT_1_EOL_WERT | real | Diagnosis value at activated secondary air system: secondary air pressure (bank 1) (EOL) (A2L-Name: prs_sa_diag_min_sa_act_1_eol) PRS_SA_DIAG_MIN_SA_ACT_1_EOL   Einheit: hPa   Min: -1280 Max: 1279.9609375 |
| STAT_PRS_SA_DIAG_MIN_SA_ACT_1_EOL_EINH | string | hPa |
| STAT_PRS_SA_DIAG_MIN_SA_ACT_2_EOL_WERT | real | Diagnosis value: secondary air pressure (bank 2) (EOL) (A2L-Name: prs_sa_diag_min_sa_act_2_eol) PRS_SA_DIAG_MIN_SA_ACT_2_EOL   Einheit: hPa   Min: -1280 Max: 1279.9609375 |
| STAT_PRS_SA_DIAG_MIN_SA_ACT_2_EOL_EINH | string | hPa |
| STAT_PRS_SA_DIAG_SA_DEAC_1_EOL_WERT | real | Diagnosis value at deactivated secondary air system: secondary air pressure (bank 1) (EOL) (A2L-Name: prs_sa_diag_sa_deac_1_eol) PRS_SA_DIAG_SA_DEAC_1_EOL   Einheit: hPa   Min: -1280 Max: 1279.9609375 |
| STAT_PRS_SA_DIAG_SA_DEAC_1_EOL_EINH | string | hPa |
| STAT_PRS_SA_DIAG_SA_DEAC_2_EOL_WERT | real | Diagnosis value at deactivated secondary air system: secondary air pressure (bank 2) (EOL) (A2L-Name: prs_sa_diag_sa_deac_2_eol) PRS_SA_DIAG_SA_DEAC_2_EOL   Einheit: hPa   Min: -1280 Max: 1279.9609375 |
| STAT_PRS_SA_DIAG_SA_DEAC_2_EOL_EINH | string | hPa |
| STAT_PRS_SA_DIAG_MIN_SA_DEAC_1_EOL_WERT | real | Diagnosis value at deactivated secondary air system: secondary air pressure (bank 1) (EOL) (A2L-Name: prs_sa_diag_min_sa_deac_1_eol) PRS_SA_DIAG_MIN_SA_DEAC_1_EOL   Einheit: hPa   Min: -1280 Max: 1279.9609375 |
| STAT_PRS_SA_DIAG_MIN_SA_DEAC_1_EOL_EINH | string | hPa |
| STAT_PRS_SA_DIAG_MIN_SA_DEAC_2_EOL_WERT | real | Diagnosis value at deactivated secondary air system: secondary air pressure (bank 2) (EOL) (A2L-Name: prs_sa_diag_min_sa_deac_2_eol) PRS_SA_DIAG_MIN_SA_DEAC_2_EOL   Einheit: hPa   Min: -1280 Max: 1279.9609375 |
| STAT_PRS_SA_DIAG_MIN_SA_DEAC_2_EOL_EINH | string | hPa |
| STAT_PRS_SA_DIAG_MAX_SA_DEAC_1_EOL_WERT | real | Diagnosis value at deactivated secondary air system: secondary air pressure (bank 1) (EOL) (A2L-Name: prs_sa_diag_max_sa_deac_1_eol) PRS_SA_DIAG_MAX_SA_DEAC_1_EOL   Einheit: hPa   Min: -1280 Max: 1279.9609375 |
| STAT_PRS_SA_DIAG_MAX_SA_DEAC_1_EOL_EINH | string | hPa |
| STAT_PRS_SA_DIAG_MAX_SA_DEAC_2_EOL_WERT | real | Diagnosis value at deactivated secondary air system: secondary air pressure (bank 2) (EOL) (A2L-Name: prs_sa_diag_max_sa_deac_2_eol) PRS_SA_DIAG_MAX_SA_DEAC_2_EOL   Einheit: hPa   Min: -1280 Max: 1279.9609375 |
| STAT_PRS_SA_DIAG_MAX_SA_DEAC_2_EOL_EINH | string | hPa |
| STAT_SAF_PRS_DIAG_SA_ACT_EOL_WERT | real | Diagnosis value at activated secondary air system: Pressure based secondary air flow (EOL) (A2L-Name: saf_prs_diag_sa_act_eol) SAF_PRS_DIAG_SA_ACT_EOL   Einheit: kg/h   Min: 0 Max: 1023.984375 |
| STAT_SAF_PRS_DIAG_SA_ACT_EOL_EINH | string | kgperh |
| STAT_SAF_PRS_DIAG_MAX_SA_ACT_EOL_WERT | real | Diagnosis value at activated secondary air system: Pressure based secondary air flow (EOL) (A2L-Name: saf_prs_diag_max_sa_act_eol) SAF_PRS_DIAG_MAX_SA_ACT_EOL   Einheit: kg/h   Min: 0 Max: 1023.984375 |
| STAT_SAF_PRS_DIAG_MAX_SA_ACT_EOL_EINH | string | kgperh |
| STAT_SAF_PRS_DIAG_MIN_SA_ACT_EOL_WERT | real | Diagnosis value at activated secondary air system: Pressure based secondary air flow (EOL) (A2L-Name: saf_prs_diag_min_sa_act_eol) SAF_PRS_DIAG_MIN_SA_ACT_EOL   Einheit: kg/h   Min: 0 Max: 1023.984375 |
| STAT_SAF_PRS_DIAG_MIN_SA_ACT_EOL_EINH | string | kgperh |
| STAT_SAF_LAMB_DIAG_SA_ACT_EOL_WERT | real | Diagnosis value at activated secondary air system: Lambda based secondary air flow (EOL) (A2L-Name: saf_lamb_diag_sa_act_eol) SAF_LAMB_DIAG_SA_ACT_EOL   Einheit: kg/h   Min: 0 Max: 1023.984375 |
| STAT_SAF_LAMB_DIAG_SA_ACT_EOL_EINH | string | kgperh |
| STAT_SAF_LAMB_DIAG_MAX_SA_ACT_EOL_WERT | real | Diagnosis value at activated secondary air system: Lambda based secondary air flow (EOL) (A2L-Name: saf_lamb_diag_max_sa_act_eol) SAF_LAMB_DIAG_MAX_SA_ACT_EOL   Einheit: kg/h   Min: 0 Max: 1023.984375 |
| STAT_SAF_LAMB_DIAG_MAX_SA_ACT_EOL_EINH | string | kgperh |
| STAT_SAF_LAMB_DIAG_MIN_SA_ACT_EOL_WERT | real | Diagnosis value at activated secondary air system: Lambda based secondary air flow (EOL) (A2L-Name: saf_lamb_diag_min_sa_act_eol) SAF_LAMB_DIAG_MIN_SA_ACT_EOL   Einheit: kg/h   Min: 0 Max: 1023.984375 |
| STAT_SAF_LAMB_DIAG_MIN_SA_ACT_EOL_EINH | string | kgperh |
| STAT_SAF_LAMB_DIAG_SA_DEAC_EOL_WERT | real | Diagnosis value at deactivated secondary air system: Lambda based secondary air flow (EOL) (A2L-Name: saf_lamb_diag_sa_deac_eol) SAF_LAMB_DIAG_SA_DEAC_EOL   Einheit: kg/h   Min: 0 Max: 1023.984375 |
| STAT_SAF_LAMB_DIAG_SA_DEAC_EOL_EINH | string | kgperh |
| STAT_SAF_LAMB_DIAG_MAX_SA_DEAC_EOL_WERT | real | Diagnosis value at deactivated secondary air system: Lambda based secondary air flow (EOL) (A2L-Name: saf_lamb_diag_max_sa_deac_eol) SAF_LAMB_DIAG_MAX_SA_DEAC_EOL   Einheit: kg/h   Min: 0 Max: 1023.984375 |
| STAT_SAF_LAMB_DIAG_MAX_SA_DEAC_EOL_EINH | string | kgperh |
| STAT_LAMB_SA_DIAG_SA_ACT_EOL_WERT | real | Diagnosis value at activated secondary air system: Secondary air Lambda (EOL) (A2L-Name: lamb_sa_diag_sa_act_eol) LAMB_SA_DIAG_SA_ACT_EOL   Min: 0 Max: 31.9990234375 |
| STAT_LAMB_SA_DIAG_MAX_SA_ACT_EOL_WERT | real | Diagnosis value at activated secondary air system: Secondary air Lambda (EOL) (A2L-Name: lamb_sa_diag_max_sa_act_eol) LAMB_SA_DIAG_MAX_SA_ACT_EOL   Min: 0 Max: 31.9990234375 |
| STAT_LAMB_SA_DIAG_MIN_SA_ACT_EOL_WERT | real | Diagnosis value at activated secondary air system: Secondary air Lambda (EOL) (A2L-Name: lamb_sa_diag_min_sa_act_eol) LAMB_SA_DIAG_MIN_SA_ACT_EOL   Min: 0 Max: 31.9990234375 |
| STAT_LAMB_SA_DIAG_SA_DEAC_EOL_WERT | real | Diagnosis value at deactivated secondary air system: Secondary air Lambda (EOL) (A2L-Name: lamb_sa_diag_sa_deac_eol) LAMB_SA_DIAG_SA_DEAC_EOL   Min: 0 Max: 31.9990234375 |
| STAT_LAMB_SA_DIAG_MAX_SA_DEAC_EOL_WERT | real | Diagnosis value at deactivated secondary air system: Secondary air Lambda (EOL) (A2L-Name: lamb_sa_diag_max_sa_deac_eol) LAMB_SA_DIAG_MAX_SA_DEAC_EOL   Min: 0 Max: 31.9990234375 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-aepdfmonitor"></a>
### STATUS_AEPDFMONITOR

0x224015 STATUS_AEPDFMONITOR FASTA-Messwertblock 10 lesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BSZSIFNP_WERT | unsigned long | Serviceintervall Betriebsstundenzaehler (bszsifnp_l) 4BYTE in 0 bis 4294967294s   Einheit: s   Min: 0 Max: 4294967294 |
| STAT_BSZSIFNP_EINH | string | second |
| STAT_NMDSFNP_00_WERT | real | Sekundaerkennfeldpunkt 00 STATE_TBL_DRIV[0][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_00_EINH | string | percent |
| STAT_NMDSFNP_10_WERT | real | Sekundaerkennfeldpunkt 10 STATE_TBL_DRIV[1][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_10_EINH | string | percent |
| STAT_NMDSFNP_20_WERT | real | Sekundaerkennfeldpunkt 20 STATE_TBL_DRIV[2][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_20_EINH | string | percent |
| STAT_NMDSFNP_30_WERT | real | Sekundaerkennfeldpunkt 30 STATE_TBL_DRIV[3][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_30_EINH | string | percent |
| STAT_NMDSFNP_40_WERT | real | Sekundaerkennfeldpunkt 40 STATE_TBL_DRIV[4][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_40_EINH | string | percent |
| STAT_NMDSFNP_50_WERT | real | Sekundaerkennfeldpunkt 50 STATE_TBL_DRIV[5][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_50_EINH | string | percent |
| STAT_NMDSFNP_60_WERT | real | Sekundaerkennfeldpunkt 60 STATE_TBL_DRIV[6][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_60_EINH | string | percent |
| STAT_NMDSFNP_70_WERT | real | Sekundaerkennfeldpunkt 70 STATE_TBL_DRIV[7][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_70_EINH | string | percent |
| STAT_NMDSFNP_01_WERT | real | Sekundaerkennfeldpunkt 01 STATE_TBL_DRIV[0][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_01_EINH | string | percent |
| STAT_NMDSFNP_11_WERT | real | Sekundaerkennfeldpunkt 11 STATE_TBL_DRIV[1][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_11_EINH | string | percent |
| STAT_NMDSFNP_21_WERT | real | Sekundaerkennfeldpunkt 21 STATE_TBL_DRIV[2][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_21_EINH | string | percent |
| STAT_NMDSFNP_31_WERT | real | Sekundaerkennfeldpunkt 31 STATE_TBL_DRIV[3][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_31_EINH | string | percent |
| STAT_NMDSFNP_41_WERT | real | Sekundaerkennfeldpunkt 41 STATE_TBL_DRIV[4][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_41_EINH | string | percent |
| STAT_NMDSFNP_51_WERT | real | Sekundaerkennfeldpunkt 51 STATE_TBL_DRIV[5][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_51_EINH | string | percent |
| STAT_NMDSFNP_61_WERT | real | Sekundaerkennfeldpunkt 61 STATE_TBL_DRIV[6][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_61_EINH | string | percent |
| STAT_NMDSFNP_71_WERT | real | Sekundaerkennfeldpunkt 71 STATE_TBL_DRIV[7][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_71_EINH | string | percent |
| STAT_NMDSFNP_02_WERT | real | Sekundaerkennfeldpunkt 02 STATE_TBL_DRIV[0][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_02_EINH | string | percent |
| STAT_NMDSFNP_12_WERT | real | Sekundaerkennfeldpunkt 12 STATE_TBL_DRIV[1][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_12_EINH | string | percent |
| STAT_NMDSFNP_22_WERT | real | Sekundaerkennfeldpunkt 22 STATE_TBL_DRIV[2][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_22_EINH | string | percent |
| STAT_NMDSFNP_32_WERT | real | Sekundaerkennfeldpunkt 32 STATE_TBL_DRIV[3][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_32_EINH | string | percent |
| STAT_NMDSFNP_42_WERT | real | Sekundaerkennfeldpunkt 42 STATE_TBL_DRIV[4][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_42_EINH | string | percent |
| STAT_NMDSFNP_52_WERT | real | Sekundaerkennfeldpunkt 52 STATE_TBL_DRIV[5][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_52_EINH | string | percent |
| STAT_NMDSFNP_62_WERT | real | Sekundaerkennfeldpunkt 62 STATE_TBL_DRIV[6][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_62_EINH | string | percent |
| STAT_NMDSFNP_72_WERT | real | Sekundaerkennfeldpunkt 72 STATE_TBL_DRIV[7][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_72_EINH | string | percent |
| STAT_NMDSFNP_03_WERT | real | Sekundaerkennfeldpunkt 03 STATE_TBL_DRIV[0][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_03_EINH | string | percent |
| STAT_NMDSFNP_13_WERT | real | Sekundaerkennfeldpunkt 13 STATE_TBL_DRIV[1][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_13_EINH | string | percent |
| STAT_NMDSFNP_23_WERT | real | Sekundaerkennfeldpunkt 23 STATE_TBL_DRIV[2][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_23_EINH | string | percent |
| STAT_NMDSFNP_33_WERT | real | Sekundaerkennfeldpunkt 33 STATE_TBL_DRIV[3][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_33_EINH | string | percent |
| STAT_NMDSFNP_43_WERT | real | Sekundaerkennfeldpunkt 43 STATE_TBL_DRIV[4][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_43_EINH | string | percent |
| STAT_NMDSFNP_53_WERT | real | Sekundaerkennfeldpunkt 53 STATE_TBL_DRIV[5][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_53_EINH | string | percent |
| STAT_NMDSFNP_63_WERT | real | Sekundaerkennfeldpunkt 63 STATE_TBL_DRIV[6][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_63_EINH | string | percent |
| STAT_NMDSFNP_73_WERT | real | Sekundaerkennfeldpunkt 73 STATE_TBL_DRIV[7][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_73_EINH | string | percent |
| STAT_NMDSFNP_04_WERT | real | Sekundaerkennfeldpunkt 04 STATE_TBL_DRIV[0][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_04_EINH | string | percent |
| STAT_NMDSFNP_14_WERT | real | Sekundaerkennfeldpunkt 14 STATE_TBL_DRIV[1][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_14_EINH | string | percent |
| STAT_NMDSFNP_24_WERT | real | Sekundaerkennfeldpunkt 24 STATE_TBL_DRIV[2][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_24_EINH | string | percent |
| STAT_NMDSFNP_34_WERT | real | Sekundaerkennfeldpunkt 34 STATE_TBL_DRIV[3][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_34_EINH | string | percent |
| STAT_NMDSFNP_44_WERT | real | Sekundaerkennfeldpunkt 44 STATE_TBL_DRIV[4][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_44_EINH | string | percent |
| STAT_NMDSFNP_54_WERT | real | Sekundaerkennfeldpunkt 54 STATE_TBL_DRIV[5][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_54_EINH | string | percent |
| STAT_NMDSFNP_64_WERT | real | Sekundaerkennfeldpunkt 64 STATE_TBL_DRIV[6][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_64_EINH | string | percent |
| STAT_NMDSFNP_74_WERT | real | Sekundaerkennfeldpunkt 74 STATE_TBL_DRIV[7][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_74_EINH | string | percent |
| STAT_NMDSFNP_05_WERT | real | Sekundaerkennfeldpunkt 05 STATE_TBL_DRIV[0][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_05_EINH | string | percent |
| STAT_NMDSFNP_15_WERT | real | Sekundaerkennfeldpunkt 15 STATE_TBL_DRIV[1][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_15_EINH | string | percent |
| STAT_NMDSFNP_25_WERT | real | Sekundaerkennfeldpunkt 25 STATE_TBL_DRIV[2][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_25_EINH | string | percent |
| STAT_NMDSFNP_35_WERT | real | Sekundaerkennfeldpunkt 35 STATE_TBL_DRIV[3][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_35_EINH | string | percent |
| STAT_NMDSFNP_45_WERT | real | Sekundaerkennfeldpunkt 45 STATE_TBL_DRIV[4][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_45_EINH | string | percent |
| STAT_NMDSFNP_55_WERT | real | Sekundaerkennfeldpunkt 55 STATE_TBL_DRIV[5][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_55_EINH | string | percent |
| STAT_NMDSFNP_65_WERT | real | Sekundaerkennfeldpunkt 65 STATE_TBL_DRIV[6][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_65_EINH | string | percent |
| STAT_NMDSFNP_75_WERT | real | Sekundaerkennfeldpunkt 75 STATE_TBL_DRIV[7][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_75_EINH | string | percent |
| STAT_DFDSFNP_00 | unsigned long | Kennfeldpunkt 00 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_01 | unsigned long | Kennfeldpunkt 01 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_02 | unsigned long | Kennfeldpunkt 02 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_03 | unsigned long | Kennfeldpunkt 03 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_10 | unsigned long | Kennfeldpunkt 10 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_11 | unsigned long | Kennfeldpunkt 11 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_12 | unsigned long | Kennfeldpunkt 12 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_13 | unsigned long | Kennfeldpunkt 13 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_20 | unsigned long | Kennfeldpunkt 20 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_21 | unsigned long | Kennfeldpunkt 21 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_22 | unsigned long | Kennfeldpunkt 22 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_23 | unsigned long | Kennfeldpunkt 23 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_30 | unsigned long | Kennfeldpunkt 30 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_31 | unsigned long | Kennfeldpunkt 31 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_32 | unsigned long | Kennfeldpunkt 32 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_33 | unsigned long | Kennfeldpunkt 33 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_IGENKFNP | unsigned long | Generatorstrom kumuliert IGENK   Min: -3e+038 Max: 3e+038 |
| STAT_TMOTB1 | unsigned long | Kuehlmitteltemperatur innerhalb Bereich 1 (tmot_b1) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TMOTB2 | unsigned long | Kuehlmitteltemperatur innerhalb Bereich 2 (tmot_b2) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TMOTB3 | unsigned long | Kuehlmitteltemperatur innerhalb Bereich 3 (tmot_b3) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TMOTB4 | unsigned long | Kuehlmitteltemperatur innerhalb Bereich 4 (tmot_b4) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TMOTB5 | unsigned long | Kuehlmitteltemperatur innerhalb Bereich 5 (tmot_b5) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TOELB1 | unsigned long | Motoroeltemperatur innerhalb Bereich 1 (toel_b1) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TOELB2 | unsigned long | Motoroeltemperatur innerhalb Bereich 2 (toel_b2) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TOELB3 | unsigned long | Motoroeltemperatur innerhalb Bereich 3 (toel_b3) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TOELB4 | unsigned long | Motoroeltemperatur innerhalb Bereich 4 (toel_b4) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TOELB5 | unsigned long | Motoroeltemperatur innerhalb Bereich 5 (toel_b5) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TGETB1 | unsigned long | Getriebeoeltemperatur innerhalb Bereich 1 (tget_b1) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TGETB2 | unsigned long | Getriebeoeltemperatur innerhalb Bereich 2 (tget_b2) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TGETB3 | unsigned long | Getriebeoeltemperatur innerhalb Bereich 3 (tget_b3) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TGETB4 | unsigned long | Getriebeoeltemperatur innerhalb Bereich 4 (tget_b4) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TGETB5 | unsigned long | Getriebeoeltemperatur innerhalb Bereich 5 (tget_b5) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TUMGB1 | unsigned long | Umgebungstemperatur innerhalb Bereich 1 (tumg_b1) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TUMGB2 | unsigned long | Umgebungstemperatur innerhalb Bereich 2 (tumg_b2) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TUMGB3 | unsigned long | Umgebungstemperatur innerhalb Bereich 3 (tumg_b3) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TUMGB4 | unsigned long | Umgebungstemperatur innerhalb Bereich 4 (tumg_b4) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TUMGB5 | unsigned long | Umgebungstemperatur innerhalb Bereich 5 (tumg_b5) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_CTR_STC_TECU_1 | unsigned long | statistic counter 1 for TECU monitoring (A2L-Name: ctr_stc_tecu_1) CTR_STC_TECU_1   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_2 | unsigned long | statistic counter 2 for TECU monitoring (A2L-Name: ctr_stc_tecu_2) CTR_STC_TECU_2   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_3 | unsigned long | statistic counter 3 for TECU monitoring (A2L-Name: ctr_stc_tecu_3) CTR_STC_TECU_3   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_4 | unsigned long | statistic counter 4 for TECU monitoring (A2L-Name: ctr_stc_tecu_4) CTR_STC_TECU_4   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_5 | unsigned long | statistic counter 5 for TECU monitoring (A2L-Name: ctr_stc_tecu_5) CTR_STC_TECU_5   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_6 | unsigned long | statistic counter 6 for TECU monitoring (A2L-Name: ctr_stc_tecu_6) CTR_STC_TECU_6   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_7 | unsigned long | statistic counter 7 for TECU monitoring (A2L-Name: ctr_stc_tecu_7) CTR_STC_TECU_7   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_8 | unsigned long | statistic counter 8 for TECU monitoring (A2L-Name: ctr_stc_tecu_8) CTR_STC_TECU_8   Min: 0 Max: 4294967295 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-igr-aus"></a>
### STATUS_SYSTEMCHECK_IGR_AUS

0x3103F0F7 STATUS_SYSTEMCHECK_IGR_AUS Auslesen Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_IGR_TEXT | string | Funktionsstatus Intelligente Generatorregelung B_DIAGIGR |
| STAT_SYSTEMCHECK_IGR_EINH | string | Funktionsstatus Intelligente Generatorregelung B_DIAGIGR |
| STAT_SYSTEMCHECK_IGR_WERT | int | Funktionsstatus Intelligente Generatorregelung B_DIAGIGR |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-swe-komplett-lesen"></a>
### SWE_KOMPLETT_LESEN

0x31010205 SWE_KOMPLETT_LESEN Informationen zu Softwareeinheiten auf dem Steuergerät unter Verwendung des Jobs SVK_LESEN UDS  : $31   RoutinControl by RequestSerice ID UDS  : $01xx Sub-Parameter fuer SVK UDS  : $0205 SWEDI (Default) Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| REFERENZ_ANZ | int | Anzahl der Referenzen auf die sich die Softwareeinheit bezieht |
| INFO_FELD_1 | string | gesamter string ab dem Bordnetzteilnehmer |
| STAT_BMW_SW_WERT | string | BMW Programmstands-Bezeichnung [1] a2l-Name: ecu_sw_bmw |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-messwerte-lrp"></a>
### STATUS_MESSWERTE_LRP

0x22402D STATUS_MESSWERTE_LRP Messwerte Laufruhepruefung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AMO_05_WERT | real | Gesamte DFT 0,5 Motorordnung (A2L-Name: Amo_05) AMO_05   Min: 0 Max: 15.9997 |
| STAT_AMO_10_WERT | real | Gesamte DFT 1,0 Motorordnung (A2L-Name: Amo_10) AMO_10   Min: 0 Max: 15.9997 |
| STAT_AMO_15_WERT | real | Gesamte DFT 1,5 Motorordnung (A2L-Name: Amo_15) AMO_15   Min: 0 Max: 15.9997 |
| STAT_AMO_20_WERT | real | Gesamte DFT 2,0 Motorordnung (A2L-Name: Amo_20) AMO_20   Min: 0 Max: 15.9997 |
| STAT_LURABS_F_0_WERT | real | gefilterte Laufunruhedeltas Zylinder 1 (A2L-Name: Lurabs_f) LURABS_F_[0]   Min: -3276.8 Max: 3276.7 |
| STAT_LURDIF_F_0_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes Zylinder 1 (A2L-Name: Lurdif_f) LURDIF_F_[0]   Min: -3276.8 Max: 3276.7 |
| STAT_ZW_OFFKORRVR_0_WERT | real | Zuendwinkeloffset fuer Verbrennungsregelung Zylinder 1 ZW_OFFKORRVR_[0]   Einheit: Grad   Min: -50 Max: 60 |
| STAT_ZW_OFFKORRVR_0_EINH | string | degree |
| STAT_LURABS_F_1_WERT | real | gefiltertes Laufunruhedeltas Zylinder 5 (A2L-Name: Lurabs_f) LURABS_F_[1]   Min: -3276.8 Max: 3276.7 |
| STAT_LURDIF_F_1_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[1]   Min: -3276.8 Max: 3276.7 |
| STAT_ZW_OFFKORRVR_1_WERT | real | Zuendwinkeloffset fuer Verbrennungsregelung Zylinder 5 ZW_OFFKORRVR_[1]   Einheit: Grad   Min: -50 Max: 60 |
| STAT_ZW_OFFKORRVR_1_EINH | string | degree |
| STAT_LURABS_F_2_WERT | real | gefiltertes Laufunruhedelta Zylinder 3  (A2L-Name: Lurabs_f) LURABS_F_[2]   Min: -3276.8 Max: 3276.7 |
| STAT_LURDIF_F_2_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[2]   Min: -3276.8 Max: 3276.7 |
| STAT_ZW_OFFKORRVR_2_WERT | real | Zuendwinkeloffset fuer Verbrennungsregelung Zylinder 3 ZW_OFFKORRVR_[2]   Einheit: Grad   Min: -50 Max: 60 |
| STAT_ZW_OFFKORRVR_2_EINH | string | degree |
| STAT_LURABS_F_3_WERT | real | gefiltertes Laufunruhedelta  Zylinder 6 (A2L-Name: Lurabs_f) LURABS_F_[3]   Min: -3276.8 Max: 3276.7 |
| STAT_LURDIF_F_3_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[3]   Min: -3276.8 Max: 3276.7 |
| STAT_ZW_OFFKORRVR_3_WERT | real | Zuendwinkeloffset fuer Verbrennungsregelung Zylinder 6 ZW_OFFKORRVR_[3]   Einheit: Grad   Min: -50 Max: 60 |
| STAT_ZW_OFFKORRVR_3_EINH | string | degree |
| STAT_LURABS_F_4_WERT | real | gefiltertes Laufunruhedelta Zylinder 2 (A2L-Name: Lurabs_f) LURABS_F_[4]   Min: -3276.8 Max: 3276.7 |
| STAT_LURDIF_F_4_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[4]   Min: -3276.8 Max: 3276.7 |
| STAT_ZW_OFFKORRVR_4_WERT | real | Zuendwinkeloffset fuer Verbrennungsregelung Zylinder 2 ZW_OFFKORRVR_[4]   Einheit: Grad   Min: -50 Max: 60 |
| STAT_ZW_OFFKORRVR_4_EINH | string | degree |
| STAT_LURABS_F_5_WERT | real | gefiltertes Laufunruhedelta Zylinders 4  (A2L-Name: Lurabs_f) LURABS_F_[5]   Min: -3276.8 Max: 3276.7 |
| STAT_LURDIF_F_5_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[5]   Min: -3276.8 Max: 3276.7 |
| STAT_ZW_OFFKORRVR_5_WERT | real | Zuendwinkeloffset fuer Verbrennungsregelung Zylinder 4 ZW_OFFKORRVR_[5]   Einheit: Grad   Min: -50 Max: 60 |
| STAT_ZW_OFFKORRVR_5_EINH | string | degree |
| STAT_AMO_30_WERT | real | Gesamte DFT 3,0 Motorordnung (A2L-Name: Amo_30) AMO_30   Min: 0 Max: 15.9997 |
| STAT_AMO_40_WERT | real | Gesamte DFT 4,0 Motorordnung (A2L-Name: Amo_40) AMO_40   Min: 0 Max: 15.9997 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-waput"></a>
### STEUERN_WAPUT

0x2F608303 STEUERN_WAPUT Wasserpumpe Turbolader ansteuern (Lagerstuhl) Aktivierung: Batteriespannung &gt; 10 V UND Motortemperatur &lt; 95 Grad C UND Drehzahl = 0 1/min  UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND TCO &lt; C_TCO_MAX_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_WAPUT_WERT | int | Sollwert Wasserpumpe Turbolader N_REL_CWP_SP_3_EXT_ADJ      Min: 0 Max: 1 |
| SW_TO_WAPUT_WERT | unsigned long | Timeout Wasserpumpe Turbolader 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-llerh"></a>
### STATUS_SYSTEMCHECK_LLERH

0x3103F026 STATUS_SYSTEMCHECK_LLERH Auslesen Diagnosefunktion Leerlauf-Erhoehung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_TEXT | string | Funktionsstatus Diagnosefunktion LL-Erhoehung STATE_EOL_KWP_N_SP_IS   Min: 0 Max: 9 |
| STAT_DIAGNOSE_WERT | int | Funktionsstatus Diagnosefunktion LL-Erhoehung STATE_EOL_KWP_N_SP_IS   Min: 0 Max: 9 |
| STAT_SYSTEMCHECK_LLERH_WERT | unsigned long | Istwert LL-Drehzahl N   Einheit: rpm   Min: 0 Max: 8160 |
| STAT_SYSTEMCHECK_LLERH_EINH | string | rpm |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-klann"></a>
### STEUERN_KLANN

0x3101F0E4 STEUERN_KLANN Ansteuern Krann-Adaptionswerte (Anforderung aus CP10798)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_LOC_WERT | long | Drehzahl NKW_LOC   Einheit: Upm   Min: -32768 Max: 32767 |
| RK_LOC_WERT | real | Relative Kraftstoffmasse RK_LOC   Min: 0 Max: 31.9995 |
| TMOT_LOC_WERT | real | Kuehlwassertemperatur TMOT_LOC   Einheit: C   Min: -327.68 Max: 327.67 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-aep-i12-test-batteryguard"></a>
### _STOP_AEP_I12_TEST_BATTERYGUARD

Anforderung Aufruf BatteryGuard Call beenden Setzen der Größe B_batteryguardcalldiag =0 Startvoraussetzungen: B_kl15 == TRUE. AEP_I12_TEST_BATTERYGUARD (0x31 02 F052)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-msv"></a>
### STEUERN_ENDE_MSV

0x2F60BD00 STEUERN_ENDE_MSV Mengensteuerventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-heizung"></a>
### STEUERN_ENDE_DMTL_HEIZUNG

0x2F60CE00 STEUERN_ENDE_DMTL_HEIZUNG Diagnosemodul-Tank Leckage Heizung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-llerh"></a>
### START_SYSTEMCHECK_LLERH

0x3101F026 START_SYSTEMCHECK_LLERH Ansteuern Diagnosefunktion Leerlauf-Erhoehung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LL_WERT | unsigned long | LL-Sollwert 0 bis 3000 1/min N_SP_IS_EXT_ADJ   Einheit: rpm   Min: 0 Max: 10000 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-slp"></a>
### STEUERN_SLP

0x2F60CB03 STEUERN_SLP Sekundaerluftpumpe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_SLP_WERT | unsigned long | Tastverhaeltniss Sekundaerluftpumpe LV_SAP_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_SLP_WERT | unsigned long | Timeout Sekundaerluftpumpe 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-opf-druckschlauchabfall"></a>
### STATUS_OPF_DRUCKSCHLAUCHABFALL

0x3103F09F STATUS_OPF_DRUCKSCHLAUCHABFALL Diagnosefunktion OPF Druckschlauchabfall

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_OPF_DRUCKSCHLAUCHABFALL_TEXT | string | Funktionsstatus der Diagnosefunktion OPF Druckschlauchabfall 1BYTE FUNKTIONSSTATUS |
| STAT_FS_OPF_DRUCKSCHLAUCHABFALL_WERT | int | Funktionsstatus der Diagnosefunktion OPF Druckschlauchabfall 1BYTE FUNKTIONSSTATUS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-anws"></a>
### STEUERN_ANWS

0x2F60EE03 STEUERN_ANWS Vanos Auslass Ventil ansteuern Aktivierung: Drehzahl &gt; 1000 1/min Activation: N &gt; C_N_MIN_KWP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ANWS_WERT | real | Tastverhaeltniss Ventil Auslassnockenwellensteller Bank 1 CAM_SP_EX_EXT_ADJ[1]   Einheit: CRK   Min: -128 Max: 52300 |
| SW_TO_ANWS_WERT | unsigned long | Timeout Ventil Auslassnockenwellensteller Bank 1 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-tev"></a>
### STEUERN_ENDE_TEV

0x2F60CF00 STEUERN_ENDE_TEV Tankentlueftungsventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ram"></a>
### STATUS_RAM

0x3103F0F2 STATUS_RAM Auslesen RAM Backup zwangssichern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_RAM_TEXT | string | FUNKTIONSSTATUS RAM 1BYTE FUNKTIONSSTATUS |
| STAT_FS_RAM_WERT | int | FUNKTIONSSTATUS RAM 1BYTE FUNKTIONSSTATUS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-adap2-selektiv-loeschen"></a>
### ADAP2_SELEKTIV_LOESCHEN

0x3101F031 ADAP2_SELEKTIV_LOESCHEN Ansteuern Adaptionen 2 selektiv loeschen Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE_1 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_2 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_3 | int | Bit=1 löscht Bit=0 behält alten Wert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-ibs"></a>
### STATUS_MESSWERTE_IBS

0x22402B STATUS_MESSWERTE_IBS Messwerte IBS auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_T_BATT_WERT | real | Batterietemperatur T_BATT   Einheit: C   Min: -3276.8 Max: 3276.7 |
| STAT_T_BATT_EINH | string | degreeC |
| STAT_U_BATT_WERT | real | Batteriespannung von IBS gemessen U_BATT   Einheit: V   Min: 6 Max: 22.3837 |
| STAT_U_BATT_EINH | string | V |
| STAT_I_BATT_WERT | real | Batteriestrom von IBS gemessen I_BATT   Einheit: A   Min: -200 Max: 5042.8 |
| STAT_I_BATT_EINH | string | A |
| STAT_IBSINFO_TEXT | string | gibt aus ob der IBS-Typ richtig ist |
| STAT_IBSINFO_01 | unsigned long | DREC_IBSINFO_01 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_02 | unsigned long | DREC_IBSINFO_02 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_03 | unsigned long | DREC_IBSINFO_03 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_04 | unsigned long | Ausgabe 1 Byte in hex, ohne Umrechnung 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_05 | unsigned long | DREC_IBSINFO_05 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_06 | unsigned long | DREC_IBSINFO_06 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_07 | unsigned long | DREC_IBSINFO_07 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_08 | unsigned long | DREC_IBSINFO_08 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_09 | unsigned long | DREC_IBSINFO_09 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_10 | unsigned long | DREC_IBSINFO_10 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_11 | unsigned long | DREC_IBSINFO_11 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_12 | unsigned long | DREC_IBSINFO_12 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_13 | unsigned long | DREC_IBSINFO_13 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_14 | unsigned long | DREC_IBSINFO_14 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_15 | unsigned long | DREC_IBSINFO_15 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_16 | unsigned long | DREC_IBSINFO_16 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_17 | unsigned long | DREC_IBSINFO_17 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_18 | unsigned long | DREC_IBSINFO_18 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_19 | unsigned long | DREC_IBSINFO_19 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_20 | unsigned long | DREC_IBSINFO_20 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_21 | unsigned long | DREC_IBSINFO_21 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_IBSINFO_22 | unsigned long | DREC_IBSINFO_22 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-hdpr"></a>
### STEUERN_HDPR

0x2F608203 STEUERN_HDPR Hochdruckpumpenrelais ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_HDPR_WERT | unsigned long | Sollwert Hochdruckpumpenrelais (A2L-Name: lv_rly_vcv_ext_adj) LV_RLY_VCV_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_HDPR_WERT | unsigned long | Timeout Hochdruckpumpenrelais 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ulv"></a>
### STEUERN_ENDE_ULV

0x2F60B500 STEUERN_ENDE_ULV Umluftventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-pm-messemode"></a>
### STATUS_SYSTEMCHECK_PM_MESSEMODE

0x3103F0F6 STATUS_SYSTEMCHECK_PM_MESSEMODE Auslesen Messemode Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_PM_MESSEMODE | unsigned long | Funktionsstatus Powermanagement Messemode LV_POW_MNG_MES_MOD   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-kqe"></a>
### STATUS_KQE

0x224035 STATUS_KQE Messwerte zur Kraftstoffqualitaet auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_QB1 | unsigned long | Qualitaetsbereich 1 (Niedrig) CTR_STC_RON_LOW   Min: 0 Max: 65535 |
| STAT_QB2 | unsigned long | Qualitaetsbereich 2 (Mittel) CTR_STC_RON_MEDIUM   Min: 0 Max: 65535 |
| STAT_QB3 | unsigned long | Qualitaetsbereich 3 (Hoch) CTR_STC_RON_HIGH   Min: 0 Max: 65535 |
| STAT_KM1_WERT | unsigned long | Kilometerstand 1 DIST_RON_STC[0]   Einheit: km   Min: 0 Max: 524280 |
| STAT_KM1_EINH | string | km |
| STAT_KM1QB | unsigned long | Qualitaetsbereich bei Kilometerstand 1 STATE_RON[0]   Min: 0 Max: 3 |
| STAT_KM2_WERT | unsigned long | Kilometerstand 2 DIST_RON_STC[1]   Einheit: km   Min: 0 Max: 524280 |
| STAT_KM2_EINH | string | km |
| STAT_KM2QB | unsigned long | Qualitaetsbereich bei Kilometerstand 2 STATE_RON[1]   Min: 0 Max: 3 |
| STAT_KM3_WERT | unsigned long | Kilometerstand 3 DIST_RON_STC[2]   Einheit: km   Min: 0 Max: 524280 |
| STAT_KM3_EINH | string | km |
| STAT_KM3QB | unsigned long | Qualitaetsbereich bei Kilometerstand 3 STATE_RON[2]   Min: 0 Max: 3 |
| STAT_KM4_WERT | unsigned long | Kilometerstand 4 DIST_RON_STC[3]   Einheit: km   Min: 0 Max: 524280 |
| STAT_KM4_EINH | string | km |
| STAT_KM4QB | unsigned long | Qualitaetsbereich bei Kilometerstand 4 STATE_RON[3]   Min: 0 Max: 3 |
| STAT_KM5_WERT | unsigned long | Kilometerstand 5 DIST_RON_STC[4]   Einheit: km   Min: 0 Max: 524280 |
| STAT_KM5_EINH | string | km |
| STAT_KM5QB | unsigned long | Qualitaetsbereich bei Kilometerstand 5 STATE_RON[4]   Min: 0 Max: 3 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-vorkonfig-opf"></a>
### STOP_VORKONFIG_OPF

0x3102F082 STOP_VORKONFIG_OPF Vorkonditionierung Otto Partikelfilter stoppen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-zgh"></a>
### STEUERN_ZGH

0x3101F034 STEUERN_ZGH Ansteuern Zylinder Gleichstellung Homogen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-abgleichwerte-lesen"></a>
### ABGLEICHWERTE_LESEN

0x225F90 ABGLEICHWERTE_LESEN Abgleichwerte Injektoren auslesen für CASCADE für Vergleich mit Daten aus COD-Datei Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_SCHREIBEN_DATEN | string | Abgleichdaten für alle Injektoren aus COD-Datei |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_LESEN_DATEN | string | Abgleichdaten für alle Injektoren aus COD-Datei nach Anwendung Umrechnungsmethoden |
| ABGLEICHWERTE_LESEN_ABGLEICHDATEN | string | Abgleichdaten für alle Injektoren aus Steuergeraet |
| ABGLEICHWERTE_LESEN_VERGLEICHSBIT_WERT | int | das im Job berechnete Vergleichsergebnis für Übereinstimmung zwischen COD- und DME-Werten |
| ABGLEICHWERTE_LESEN_VERGLEICHSBIT_TEXT | string | das im Job berechnete Vergleichsergebnis für Übereinstimmung zwischen COD- und DME-Werten als Text |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dfmonitor"></a>
### STATUS_DFMONITOR

0x224001 STATUS_DFMONITOR Batterieladezustand auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AUSGANG_WERT | real | Batterieladezustand DFMONITOR   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_AUSGANG_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-opf"></a>
### STOP_SYSTEMCHECK_OPF

0x3102F07B STOP_SYSTEMCHECK_OPF OPF Systemtest  beenden  Bei Master Slave Projekten Kopplung notwendig.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-pm-messemode"></a>
### STOP_SYSTEMCHECK_PM_MESSEMODE

0x3102F0F6 STOP_SYSTEMCHECK_PM_MESSEMODE Ende Messemode Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-messwertblock-lesen"></a>
### MESSWERTBLOCK_LESEN

0x2CF0 MESSWERTBLOCK_LESEN DDLI Messwerte auf Basis Übergabestring aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1 es können 40 Messwerte in einem Block zusammengefasst werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STRING_IN | string | Werte aus DDLI Liste Format 0x58XX,0x42YY,0x43ZZ,... |
| TRENNZEICHEN | string | Werte aus DDLI Liste Format 0x58XX,0x42YY,0x43ZZ,... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZAHL_WERTE | int | Anzahl Messwerte 0 bis n dezimal ansteigend |
| STAT_MESSWERT0_WERT | real | real Wert |
| STAT_MESSWERT0_STRING | string | String mit 10 signifikanten Stellen |
| STAT_MESSWERT0_TEXT | string | Text der Variablen aus INFO |
| STAT_MESSWERT0_EINH | string | Einheit der Variablen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an  SG Block löschen |
| _TEL_ANTWORT_L | binary | Hex-response von SG Block löschen |
| _TEL_AUFTRAG | binary | Hex-Auftrag an  SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-response von SG Block schreiben |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an  SG Block lesen |
| _TEL_ANTWORT | binary | Hex-response von SG Block lesen |

<a id="job-steuern-ewap"></a>
### STEUERN_EWAP

0x2F60BF03 STEUERN_EWAP elektr. Wasserpumpe ueber LIN ansteuern nur bei Fahrzeuggeschwindigkeit v=0 und Motortemperatur TMOT kleiner 115gradCelsius und Batteriespannung UBAT groesser 10Volt CON_EWAP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EWAP_WERT | real | Tastverhaeltniss elektr. Wasserpumpe ueber LIN N_REL_CWP_SP_2_EXT_ADJ   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_EWAP_WERT | unsigned long | Timeout elektr. Wasserpumpe 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-slp"></a>
### STEUERN_ENDE_SLP

0x2F60CB00 STEUERN_ENDE_SLP Sekundaerluftpumpe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-gen"></a>
### STOP_SYSTEMCHECK_GEN

0x3102F02A STOP_SYSTEMCHECK_GEN Diagnosefunktion Generatortest beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-kft"></a>
### STEUERN_KFT

0x2F60C903 STEUERN_KFT Kennfeldthermostat ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_KFT_WERT | real | Sollwert Kennfeldthermostat ECTPWM_EXT_ADJ   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_KFT_WERT | unsigned long | Timeout Kennfeldthermostat 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-gvobd"></a>
### STEUERN_PROGRAMM_GVOBD

0x2E5F8008 STEUERN_PROGRAMM_GVOBD Gemischvertrimmung fuer OBD-Demo und PVE programmieren.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_F_MK_KORR_EXT_XZYL_1_WERT | real | Faktor auf Einspritzung Zylinder 1 F_mk_korr_ext_xzyl_[1]   Min: 0 Max: 1.99996948242188 |
| SW_F_MK_KORR_EXT_XZYL_5_WERT | real | Faktor auf Einspritzung Zylinder 5 F_mk_korr_ext_xzyl_[2]   Min: 0 Max: 1.99996948242188 |
| SW_F_MK_KORR_EXT_XZYL_3_WERT | real | Faktor auf Einspritzung Zylinder 3 F_mk_korr_ext_xzyl_[3]   Min: 0 Max: 1.99996948242188 |
| SW_F_MK_KORR_EXT_XZYL_6_WERT | real | Faktor auf Einspritzung Zylinder 6 F_mk_korr_ext_xzyl_[4]   Min: 0 Max: 1.99996948242188 |
| SW_F_MK_KORR_EXT_XZYL_2_WERT | real | Faktor auf Einspritzung Zylinder 2 F_mk_korr_ext_xzyl_[5]   Min: 0 Max: 1.99996948242188 |
| SW_F_MK_KORR_EXT_XZYL_4_WERT | real | Faktor auf Einspritzung Zylinder 4 F_mk_korr_ext_xzyl_[6]   Min: 0 Max: 1.99996948242188 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bzeinfo"></a>
### _STATUS_BZEINFO

0x22401A _STATUS_BZEINFO Infospeicher Batterie Zustands Erkennung (BZE) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_QV_OUT_M_WERT | real | Gueltiger gemittelter Kapazitaetsverlust (A2L-Name: Qv_out_m) Qv_out_m   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_OUT_M_EINH | string | percent |
| STAT_QV_QUALI_M_WERT | real | Qualitaetsindex fuer gemittelten Qv-Wert (A2L-Name: Qv_quali_m) Qv_quali_m   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_M_EINH | string | percent |
| STAT_QV_STATUS | long | Prozessstatus / Trend fuer gemittelten Qv-Wert (A2L-Name: Qv_status) Qv_status   Min: -128 Max: 127 |
| STAT_QV_OUT_1_WERT | long | Kapazitaetsverlust letzter Start (A2L-Name: Qv_out_1) Qv_out_1   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_1_EINH | string | Ah |
| STAT_QV_OUT_2_WERT | long | Kapazitaetsverlust 2. letzter Start (A2L-Name: Qv_out_2) Qv_out_2   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_2_EINH | string | Ah |
| STAT_QV_OUT_3_WERT | long | Kapazitaetsverlust 3. letzter Start (A2L-Name: Qv_out_3) Qv_out_3   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_3_EINH | string | Ah |
| STAT_QV_OUT_4_WERT | long | Kapazitaetsverlust 4. letzter Start (A2L-Name: Qv_out_4) Qv_out_4   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_4_EINH | string | Ah |
| STAT_QV_OUT_5_WERT | long | Kapazitaetsverlust 5. letzter Start (A2L-Name: Qv_out_5) Qv_out_5   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_5_EINH | string | Ah |
| STAT_QV_QUALI_1_WERT | real | Qualitaetsindex letzter Qv-Wert (A2L-Name: Qv_quali_1) Qv_quali_1   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_1_EINH | string | percent |
| STAT_QV_QUALI_2_WERT | real | Qualitaetsindex 2. letzter Qv-Wert (A2L-Name: Qv_quali_2) Qv_quali_2   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_2_EINH | string | percent |
| STAT_QV_QUALI_3_WERT | real | Qualitaetsindex 3. letzter Qv-Wert (A2L-Name: Qv_quali_3) Qv_quali_3   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_3_EINH | string | percent |
| STAT_QV_QUALI_4_WERT | real | Qualitaetsindex 4. letzter Qv-Wert (A2L-Name: Qv_quali_4) Qv_quali_4   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_4_EINH | string | percent |
| STAT_QV_QUALI_5_WERT | real | Qualitaetsindex 5. letzter Qv-Wert (A2L-Name: Qv_quali_5) Qv_quali_5   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_5_EINH | string | percent |
| STAT_QV_TD1_WERT | unsigned long | Zeit seit Qv_out_1 Berechnung (A2L-Name: Qv_td1) Qv_td1   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD1_EINH | string | h |
| STAT_QV_TD2_WERT | unsigned long | Zeit zwischen Qv_out_1 und Qv_out_2 (A2L-Name: Qv_td2) Qv_td2   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD2_EINH | string | h |
| STAT_QV_TD3_WERT | unsigned long | Zeit zwischen Qv_out_2 und Qv_out_3 (A2L-Name: Qv_td3) Qv_td3   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD3_EINH | string | h |
| STAT_QV_TD4_WERT | unsigned long | Zeit zwischen Qv_out_3 und Qv_out_4 (A2L-Name: Qv_td4) Qv_td4   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD4_EINH | string | h |
| STAT_QV_TD5_WERT | unsigned long | Zeit zwischen Qv_out_4 und Qv_out_5 (A2L-Name: Qv_td5) Qv_td5   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD5_EINH | string | h |
| STAT_QVC_STATUS_1_WERT | real | Ausgang fuer Schluesselgroesse 1 (A2L-Name: Qvc_status_1) Qvc_status_1   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QVC_STATUS_1_EINH | string | percent |
| STAT_QVC_STATUS_2_WERT | real | Ausgang fuer Schluesselgroesse 2 (A2L-Name: Qvc_status_2) Qvc_status_2   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QVC_STATUS_2_EINH | string | percent |
| STAT_QVC_STATUS_3 | unsigned long | Ausgang fuer Schluesselgroesse 3 (A2L-Name: Qvc_status_3) Qvc_status_3   Min: 0 Max: 255 |
| STAT_QVC_STATUS_4 | long | Ausgang fuer Schluesselgroesse 4 (A2L-Name: Qvc_status_4) Qvc_status_4   Min: -128 Max: 127 |
| STAT_QV_NV_ZH | unsigned long | Anzahl der Hystereseauswertungen (A2L-Name: Qv_nv_zh) Qv_nv_zh   Min: 0 Max: 4294967295 |
| STAT_QV_NV_EZM_WERT | real | Mittlerer Fehler fuer gesamte Hystereseberechnung (A2L-Name: Qv_nv_ezm) Qv_nv_ezm   Min: 0 Max: 1 |
| STAT_QV_H2O_WERT | real | Bisheriger Wasserverlust Batterie (A2L-Name: Qv_h2o) Qv_h2o   Min: 0 Max: 63.999 |
| STAT_QV_H2OQUALI_WERT | real | Qualitaetswert fuer Wasserverlust Batterie (A2L-Name: Qv_h2oquali) Qv_h2oquali   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_H2OQUALI_EINH | string | percent |
| STAT_ST_QVC1 | unsigned long | Statuswort (A2L-Name: St_qvc1) Bedeutung: - 0: Wasserverlust O.K. - 1: Wasserverlust zu hoch St_qvc1   Min: 0 Max: 255 |
| STAT_QV_H2OSTATUS | unsigned long | Status fuer Entwicklung Wasserverlust (A2L-Name: Qv_h2ostatus) Qv_h2ostatus   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dk"></a>
### STEUERN_DK

0x2F602A03 STEUERN_DK Drosselklappe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DK_WERT | real | Tastverhaeltniss Drosselklappe TPS_SP_EXT_ADJ   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_DK_WERT | unsigned long | Timeout Drosselklappe 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-sek-luft"></a>
### START_SYSTEMCHECK_SEK_LUFT

0x3101F020 START_SYSTEMCHECK_SEK_LUFT Ansteuern Diagnosefunktion Sekundaerluft Aktivierung: Leerlauf UND Motortemperatur &gt; 75 Grad C UND Ueberspannung = AUS UND LV_TEMP_MAX_SAP_COIL = 0 UND Fehlerspeichereintrag Sekundaerluftmassenmesser = Aus UND Fehlerspeichereintrag Sekundaerluftsystem = AUS UND Fehlerspeichereintrag Luftmassenmesser = AUS UND Fehlerspeichereintrag Umgebungsdrucksensor = 0 UND Fehlerspeichereintrag Umgebungsdrucksensor Plausibilitaet = AUS UND Fehlerspeichereintrag Kuehlmitteltemperatursensor = AUS UND Fehlerspeichereintrag Kurbelwellensensor = AUS UND Fehlerspeichereintrag Tankfuellstand zu gering = AUS UND LV_MIS_STATE_A = 0 UND LV_MIS_STATE_B = 0 UND Fehlerspeichereintrag Sekundaerluftventil = AUS UND Fehlerspeichereintrag Sekundaerluftpumpe = AUS UND Fehlerspeichereintrag Umgebungsdrucksensor = 0 UND Fehlerspeichereintrag Drosselklappenstellung Plausibilitaet = 0 UND (Diagnosestatus Sekundaerluftmassenmesser = SAFM_DIAG_END ODER SAFM_DIAG_CNL) Activation: LV_IS = 1 UND TCO &gt; C_TCO_MIN_SA_EOL UND LV_VB_JUMP = 0 UND LV_TEMP_MAX_SAP_COIL = 0 UND LV_ERR_SA_SAFM = 0 UND LV_ERR_SA_SYS = 0 UND LV_ERR_SA_SAV = 0 UND LV_ERR_MAF = 0 UND LV_ERR_AMP = 0 UND LV_ERR_AMP_PLAUS = 0 UND LV_ERR_TCO = 0 UND LV_ERR_CRK = 0 UND LV_ERR_FTL_MIN = 0 UND LV_MIS_STATE_A = 0 UND LV_MIS_STATE_B = 0 UND LV_ERR_SAV = 0 UND LV_ERR_SAP = 0 UND LV_ERR_LOAD_TPS_PLAUS = 0 UND (STATE_DIAG_SA_SAFM = SAFM_DIAG_END ODER SAFM_DIAG_CNL)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-mil"></a>
### STEUERN_MIL

0x2F60D403 STEUERN_MIL MIL (Malfunction Indicator Lamp) ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_MIL_WERT | unsigned long | Sollwert MIL (Malfunction Indicator Lamp) LV_ACT_MIL_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_MIL_WERT | unsigned long | Timeout MIL (Malfunction Indicator Lamp) 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh1"></a>
### STEUERN_LSH1

0x2F60D003 STEUERN_LSH1 Lambdasondenheizung vor Kat Bank1 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH1_WERT | real | Tastverhaeltniss Lambdasondenheizung vor Kat Bank1 LSHPWM_UP_EXT_ADJ[1]   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_LSH1_WERT | unsigned long | Timeout Lambdasondenheizung vor Kat Bank1 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-ecu-config"></a>
### ECU_CONFIG

0x225FF2 ECU_CONFIG Variante auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AT | unsigned long | Automatik Getriebe  0=nicht vorhanden / 1=vorhanden LV_AT   Min: 0 Max: 1 |
| STAT_AC | unsigned long | Klimaanlage  0=nicht vorhanden / 1=vorhanden LV_VAR_ACIN   Min: 0 Max: 1 |
| STAT_AMT | unsigned long | SMG Sequentielles Manuelles Getriebe  0=nicht vorhanden / 1=vorhanden LV_VAR_AMT   Min: 0 Max: 1 |
| STAT_ARS | unsigned long | ARS Aktive Roll-Stabilisierung  0=nicht vorhanden / 1=vorhanden LV_VAR_ARS   Min: 0 Max: 1 |
| STAT_ASR | unsigned long | ASR Anti-Schlupf-Regelung  0=nicht vorhanden / 1=vorhanden LV_VAR_ASR   Min: 0 Max: 1 |
| STAT_BN | unsigned long | Bordnetz 2000  0=nicht vorhanden / 1=vorhanden LV_VAR_BN   Min: 0 Max: 1 |
| STAT_BN_MSW | unsigned long | Tempomat ueber CAN  0=nicht vorhanden / 1=vorhanden LV_VAR_BN_MSW   Min: 0 Max: 1 |
| STAT_DCC | unsigned long | Entfernungsueberwachung  0=nicht vorhanden / 1=vorhanden LV_VAR_DCC   Min: 0 Max: 1 |
| STAT_EBOX_CFA | unsigned long | E-Box-Luefter  0=nicht vorhanden / 1=vorhanden LV_VAR_EBOX_CFA   Min: 0 Max: 1 |
| STAT_ETCU | unsigned long | SMG/EGS Steuergeraet  0=nicht vorhanden / 1=vorhanden LV_VAR_ETCU   Min: 0 Max: 1 |
| STAT_ICL | unsigned long | Kombi ueber CAN  0=nicht vorhanden / 1=vorhanden LV_VAR_ICL   Min: 0 Max: 1 |
| STAT_MSW | unsigned long | Multifunktionslenkrad  0=nicht vorhanden / 1=vorhanden LV_VAR_MSW   Min: 0 Max: 1 |
| STAT_PSTE | unsigned long | Elektrische Lenkung  0=nicht vorhanden / 1=vorhanden LV_VAR_PSTE   Min: 0 Max: 1 |
| STAT_SOF | unsigned long | Soundklappe  0=nicht vorhanden / 1=vorhanden LV_VAR_SOF   Min: 0 Max: 1 |
| STAT_SOF_SWI | unsigned long | Sport-Taster  0=nicht vorhanden / 1=vorhanden CONF_SOF_SWI   Min: 0 Max: 2 |
| STAT_GEAR | unsigned long | Komfortstart  0=nicht vorhanden / 1=vorhanden LV_VAR_BN_GEAR_REV   Min: 0 Max: 1 |
| STAT_VEH | unsigned long | Fahrzeugvariante mit Power Modul (E60/E65) erkannt - nur BN 2000  0=nicht vorhanden / 1=vorhanden LV_VAR_VEH   Min: 0 Max: 1 |
| STAT_EF | unsigned long | Abgasklappe  0=nicht vorhanden / 1=vorhanden LV_VAR_EF   Min: 0 Max: 1 |
| STAT_ECRAS_UP | unsigned long | Lernvariante Aktive Kuehlerluftklappe (obere Klappe) LIN 1BIT IDENTICAL |
| STAT_DCDC | unsigned long | Lernvariante DCDC Wandler fuer Hybridfahrzeuge LIN 1BIT IDENTICAL |
| STAT_CWP_LIN | unsigned long | Lernvariante elektrische Wasserpumpe (50W) LIN 1BIT IDENTICAL |
| STAT_IBS | unsigned long | Lernvariante IBS-Sensor LIN 1BIT IDENTICAL |
| STAT_RLY_ST | unsigned long | Starterrelais  0=nicht vorhanden / 1=vorhanden LV_VAR_RLY_ST   Min: 0 Max: 1 |
| STAT_ASR3 | unsigned long | ASR3 Steuergeraet  0=nicht vorhanden / 1=vorhanden LV_VAR_ASR_3   Min: 0 Max: 1 |
| STAT_BN_LDM | unsigned long | Laengs-Dynamik-Management  0=nicht vorhanden / 1=vorhanden LV_VAR_BN_LDM   Min: 0 Max: 1 |
| STAT_BN_LTG_HDLP_L | unsigned long | Lampenzustand  0=nicht vorhanden / 1=vorhanden LV_VAR_BN_LTG_HDLP_L   Min: 0 Max: 1 |
| STAT_LSH_DOWN | unsigned long | Lambdasonde hinter Katalysator  0=nicht vorhanden / 1=vorhanden LV_VAR_LSH_DOWN   Min: 0 Max: 1 |
| STAT_LSH_UP | unsigned long | Lambdasonde vor Katalysator  0=nicht vorhanden / 1=vorhanden LV_VAR_LSH_UP   Min: 0 Max: 1 |
| STAT_ASR_4 | unsigned long | ASR4 Steuergeraet  0=nicht vorhanden / 1=vorhanden LV_VAR_ASR_4   Min: 0 Max: 1 |
| STAT_MAF | unsigned long | Luftmassenmesser  0=nicht vorhanden / 1=vorhanden LV_VAR_MAF & LV_VAR_MAF_LEARNT   Min: 0 Max: 1 |
| STAT_PSTE_2 | unsigned long | AFS Active-Front-Steering  0=nicht vorhanden / 1=vorhanden LV_VAR_PSTE_2   Min: 0 Max: 1 |
| STAT_BN_EFP | unsigned long | Elektrische Kraftstoffpumpe ueber CAN  0=nicht vorhanden / 1=vorhanden LV_VAR_BN_EFP   Min: 0 Max: 1 |
| STAT_BN_TRL | unsigned long | Anhaengermodul  0=nicht vorhanden / 1=vorhanden LV_VAR_BN_TRL   Min: 0 Max: 1 |
| STAT_ECRAS_DOWN | unsigned long | Kuehlerjalousie unten  0=nicht vorhanden / 1=vorhanden LV_VAR_ECRAS_DOWN   Min: 0 Max: 1 |
| STAT_TCT | unsigned long | Doppelkupplungsgetriebe A2L lv_var_tct LV_VAR_TCT   Min: 0 Max: 1 |
| STAT_AEB | unsigned long | Aktives Motorlager (A2L-Name: lv_var_aeb) LV_VAR_AEB   Min: 0 Max: 1 |
| STAT_TQ_PBR | unsigned long | Elektromechanische Parkbremse  (A2L-Name: lv_var_tq_pbr) LV_VAR_TQ_PBR   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-msvhdp5"></a>
### STEUERN_ENDE_MSVHDP5

0x2F60EF00 STEUERN_ENDE_MSVHDP5 Mengensteuerventil HDP5 Ansteuerung beenden NO_CON

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-discodbsr"></a>
### STEUERN_DISCODBSR

0x2E5F7E STEUERN_DISCODBSR Verriegelung des betriebsstundenrelevanten Kodierbereichs.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh2"></a>
### STEUERN_LSH2

0x2F60D103 STEUERN_LSH2 Lambdasondenheizung hinter Kat Bank1 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH2_WERT | real | Tastverhaeltniss Lambdasondenheizung hinter Kat Bank1 LSHPWM_DOWN_EXT_ADJ[1]   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_LSH2_WERT | unsigned long | Timeout Lambdasondenheizung hinter Kat Bank1 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-12"></a>
### STEUERN_PROGRAMM_IMA_ZYL_12

0x2E5F98 STEUERN_PROGRAMM_IMA_ZYL_12 Abgleichwert Injektor 12 programmieren NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_12_WERT | real | IMA Abgleichwert Injektor 12 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[7]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_12_WERT | real | IMA Abgleichwert Injektor 12 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[7]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-10"></a>
### STEUERN_PROGRAMM_IMA_ZYL_10

0x2E5F9C STEUERN_PROGRAMM_IMA_ZYL_10 Abgleichwert Injektor 10 programmieren NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_10_WERT | real | IMA Abgleichwert Injektor 10 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[11]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_10_WERT | real | IMA Abgleichwert Injektor 10 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[11]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-11"></a>
### STEUERN_PROGRAMM_IMA_ZYL_11

0x2E5F94 STEUERN_PROGRAMM_IMA_ZYL_11 Abgleichwert Injektor 11 programmieren NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_11_WERT | real | IMA Abgleichwert Injektor 11 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[3]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_11_WERT | real | IMA Abgleichwert Injektor 11 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[3]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-5"></a>
### STEUERN_PROGRAMM_IMA_ZYL_5

0x2E5F93 STEUERN_PROGRAMM_IMA_ZYL_5 Abgleichwert Injektor 05 programmieren NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_5_WERT | real | IMA Abgleichwert Injektor 05 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[2]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_5_WERT | real | IMA Abgleichwert Injektor 05 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[2]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-6"></a>
### STEUERN_PROGRAMM_IMA_ZYL_6

0x2E5F97 STEUERN_PROGRAMM_IMA_ZYL_6 Abgleichwert Injektor 06 programmieren NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_6_WERT | real | IMA Abgleichwert Injektor 06 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[6]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_6_WERT | real | IMA Abgleichwert Injektor 06 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[6]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-3"></a>
### STEUERN_PROGRAMM_IMA_ZYL_3

0x2E5F95 STEUERN_PROGRAMM_IMA_ZYL_3 Abgleichwert Injektor 03 programmieren NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_3_WERT | real | IMA Abgleichwert Injektor 03 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[4]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_3_WERT | real | IMA Abgleichwert Injektor 03 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[4]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-4"></a>
### STEUERN_PROGRAMM_IMA_ZYL_4

0x2E5F9B STEUERN_PROGRAMM_IMA_ZYL_4 Abgleichwert Injektor 04 programmieren NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_10_WERT | real | IMA Abgleichwert Injektor 11 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[10]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_10_WERT | real | IMA Abgleichwert Injektor 11 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[10]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-9"></a>
### STEUERN_PROGRAMM_IMA_ZYL_9

0x2E5F96 STEUERN_PROGRAMM_IMA_ZYL_9 Abgleichwert Injektor 09 programmieren NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_9_WERT | real | IMA Abgleichwert Injektor 09 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[5]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_9_WERT | real | IMA Abgleichwert Injektor 09 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[5]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-7"></a>
### STEUERN_PROGRAMM_IMA_ZYL_7

0x2E5F92 STEUERN_PROGRAMM_IMA_ZYL_7 Abgleichwert Injektor 07 programmieren NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_7_WERT | real | IMA Abgleichwert Injektor 07 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[1]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_7_WERT | real | IMA Abgleichwert Injektor 07 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[1]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-8"></a>
### STEUERN_PROGRAMM_IMA_ZYL_8

0x2E5F9A STEUERN_PROGRAMM_IMA_ZYL_8 Abgleichwert Injektor 08 programmieren NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_8_WERT | real | IMA Abgleichwert Injektor 08 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[9]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_8_WERT | real | IMA Abgleichwert Injektor 08 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[9]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-nockenwelle-adaption"></a>
### STATUS_NOCKENWELLE_ADAPTION

0x224006 STATUS_NOCKENWELLE_ADAPTION Nockenwellenadationswerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NC_PSN_EDGE_CAM_EX_1_WERT | real | Flanke Auslassnockenwellensteller Zylinder 1 NC_PSN_EDGE_CAM_EX_1   Einheit: Grad KW   Min: 0 Max: 719.9375 |
| STAT_NC_PSN_EDGE_CAM_EX_1_EINH | string | degree_KW |
| STAT_NC_PSN_EDGE_CAM_EX_6_WERT | real | Flanke  Auslassnockenwellensteller Zylinder 6 NC_PSN_EDGE_CAM_EX_6   Einheit: Grad KW   Min: 0 Max: 719.9375 |
| STAT_NC_PSN_EDGE_CAM_EX_6_EINH | string | degree_KW |
| STAT_NC_PSN_EDGE_CAM_IN_1_WERT | real | Flanke Einlassnockenwellensteller  Zylinder 1 NC_PSN_EDGE_CAM_IN_1   Einheit: Grad KW   Min: 0 Max: 719.9375 |
| STAT_NC_PSN_EDGE_CAM_IN_1_EINH | string | degree_KW |
| STAT_NC_PSN_EDGE_CAM_IN_6_WERT | real | Flanke Einlassnockenwellensteller Zylinder 6 NC_PSN_EDGE_CAM_IN_6   Einheit: Grad KW   Min: 0 Max: 719.9375 |
| STAT_NC_PSN_EDGE_CAM_IN_6_EINH | string | degree_KW |
| STAT_PSN_EDGE_AD_CAM_IN_1_WERT | real | Adaptierte Nockenwellenflanke Einlass 1 position PSN_EDGE_1_AD_CAM_IN_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_IN_1_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_IN_2_WERT | real | Adaptierte Nockenwellenflanke Einlass 2 position PSN_EDGE_2_AD_CAM_IN_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_IN_2_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_IN_3_WERT | real | Adaptierte Nockenwellenflanke Einlass 3 position PSN_EDGE_3_AD_CAM_IN_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_IN_3_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_IN_4_WERT | real | Adaptierte Nockenwellenflanke Einlass 4 position PSN_EDGE_4_AD_CAM_IN_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_IN_4_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_IN_5_WERT | real | Adaptierte Nockenwellenflanke Einlass 5 position PSN_EDGE_5_AD_CAM_IN_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_IN_5_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_IN_6_WERT | real | Adaptierte Nockenwellenflanke Einlass 5 position PSN_EDGE_6_AD_CAM_IN_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_IN_6_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_EX_1_WERT | real | Adaptierte Nockenwellenflanke Auslass 1 position PSN_EDGE_1_AD_CAM_EX_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_EX_1_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_EX_2_WERT | real | Adaptierte Nockenwellenflanke Auslass 1 position PSN_EDGE_2_AD_CAM_EX_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_EX_2_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_EX_3_WERT | real | Adaptierte Nockenwellenflanke Auslass 1 position PSN_EDGE_3_AD_CAM_EX_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_EX_3_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_EX_4_WERT | real | Adaptierte Nockenwellenflanke Auslass 1 position PSN_EDGE_4_AD_CAM_EX_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_EX_4_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_EX_5_WERT | real | Adaptierte Nockenwellenflanke Auslass 1 position PSN_EDGE_5_AD_CAM_EX_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_EX_5_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_EX_6_WERT | real | Adaptierte Nockenwellenflanke Auslass 1 position PSN_EDGE_6_AD_CAM_EX_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_EX_6_EINH | string | degreeCRK |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-1"></a>
### STEUERN_PROGRAMM_IMA_ZYL_1

0x2E5F91 STEUERN_PROGRAMM_IMA_ZYL_1 Abgleichwert Injektor 01 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_1_WERT | real | IMA Abgleichwert Injektor 01 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[0]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_1_WERT | real | IMA Abgleichwert Injektor 01 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[0]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-2"></a>
### STEUERN_PROGRAMM_IMA_ZYL_2

0x2E5F99 STEUERN_PROGRAMM_IMA_ZYL_2 Abgleichwert Injektor 02 programmieren NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_2_WERT | real | IMA Abgleichwert Injektor 02 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[8]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_2_WERT | real | IMA Abgleichwert Injektor 02 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[8]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-l-regelung-aus"></a>
### START_SYSTEMCHECK_L_REGELUNG_AUS

0x3101F0D9 START_SYSTEMCHECK_L_REGELUNG_AUS Ansteuerung Lambdaregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-vanosspuelen"></a>
### STOP_VANOSSPUELEN

0x3102F042 STOP_VANOSSPUELEN VANOS Spuelen fuer OBD und PVE. Steuern-Ende

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-opf-druckschlauchabfall"></a>
### STOP_OPF_DRUCKSCHLAUCHABFALL

0x3102F09F STOP_OPF_DRUCKSCHLAUCHABFALL Diagnosefunktion OPF Druckschlauchabfall  beenden  (Bei Master Slave Projekten Kopplung notwendig.)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-verbraucherstrom-efii"></a>
### STEUERN_VERBRAUCHERSTROM_EFII

Ansteuerung Verbraucherstrommessung EFII (IBS) UDS  : $31   RoutineControl UDS  : $01   routineControlType UDS  : $7002 routineIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STARTTRIGGERWERT | long | Ecos2 Start Trigger Wert [mA] |
| AUSSCHALTTRIGGER | long | Ecos2 Ende Trigger Wert [mA] |
| TOTZEIT | int | Ecos2 Strommessung holdoff Zeit [ms] |
| MESSZEIT | int | Ecos2 Messzeit [ms] |
| UNTERE_TOLERANZ | long | Ecos2 untere Stromschwelle [mA] |
| OBERE_TOLERANZ | long | Ecos2 obere Stromschwelle [mA] |
| MESSPUNKTE | int | Ecos2 Anzahl Messpunkte [-] |
| TRIGGERFILTER | int | Ecos2 Triggerfilter [ms] |
| MESSWERTFILTER | int | Ecos2 Messfilter [ms] |
| TIMEOUT | int | Ecos2 timeout Zeit [s] |
| POSTTRIGGER | int | Ecos2 Nachtrigger Aufzeichnung [ms] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-ident-gen"></a>
### IDENT_GEN

0x2C01F3 IDENT_GEN Identifikationsdaten Generator Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GEN_MANUFAK_WERT | unsigned long | Herstellercode Generator 1 GEN_MANUFAK   Min: 0 Max: 255 |
| STAT_GEN_MANUFAK_STRING | string | Herstellercode Generator 1  |
| STAT_GEN_MANUFAK_TEXT | string | Herstellercode Generator 1 als Text  |
| STAT_GEN_TYPKENN_WERT | unsigned long | Generatortyp Generator 1 GEN_TYPKENN   Min: 0 Max: 255 |
| STAT_GEN_TYPKENN_STRING | string | Generatortyp Generator 1  |
| STAT_GEN_TYPKENN_TEXT | string | Generatortyp Generator 1 als Text  |
| STAT_BSDGENREGV_WERT | unsigned long | Reglerversion Generator 1 BSDGENREGV   Min: 0 Max: 255 |
| STAT_BSDGENREGV_STRING | string | Reglerversion Generator 1  |
| STAT_BSDGENREGV_TEXT | string | Reglerversion Generator 1 als Text  |
| STAT_BSDGENCV_WERT | unsigned long | Chipversion Generator 1 BSDGENCV   Min: 0 Max: 255 |
| STAT_BSDGENCV_STRING | string | Chipversion Generator 1  |
| STAT_BSDGENCV_TEXT | string | Chipversion Generator 1 als Text  |
| STAT_B_BSDPROT2_WERT | unsigned long | BSD II Protokoll für Generator 1 B_BSDPROT2   Min: 0 Max: 255 |
| STAT_B_BSDPROT2_STRING | string | BSD II Protokoll für Generator 1  |
| STAT_B_BSDPROT2_TEXT | string | BSD II Protokoll für Generator 1 als Text  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an  SG Block löschen |
| _TEL_ANTWORT_L | binary | Hex-response von SG Block löschen |
| _TEL_AUFTRAG | binary | Hex-Auftrag an  SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-response von SG Block schreiben |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an  SG Block lesen |
| _TEL_ANTWORT | binary | Hex-response von SG Block lesen Hex-Antwort von SG |

<a id="job-stop-systemcheck-llerh"></a>
### STOP_SYSTEMCHECK_LLERH

0x3102F026 STOP_SYSTEMCHECK_LLERH Diagnosefunktion Leerlauf-Erhoehung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-zgh"></a>
### STATUS_ZGH

0x3103F034 STATUS_ZGH Auslesen Zylinder Gleichstellung Homogen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_ZGH_TEXT | string | FUNKTIONSSTATUS ZGH State of cylinder balancing homogenous (A2L-Name: state_er_bal_hom) STATE_ER_BAL_HOM   Min: 0 Max: 3 |
| STAT_FS_ZGH_WERT | int | FUNKTIONSSTATUS ZGH State of cylinder balancing homogenous (A2L-Name: state_er_bal_hom) STATE_ER_BAL_HOM   Min: 0 Max: 3 |
| STAT_STATE_BAL_RNG_TEXT | string | Aktueller Betriebsbereich(A2L-Name: state_er_bal_hom_rng) STATE_ER_BAL_HOM_RNG   Min: 0 Max: 3 |
| STAT_STATE_BAL_RNG_WERT | int | Aktueller Betriebsbereich(A2L-Name: state_er_bal_hom_rng) STATE_ER_BAL_HOM_RNG   Min: 0 Max: 3 |
| STAT_CYC_NR | unsigned long | gesamtanzahl von Durchlaufenen Adaptionen des Zylinderbalancings (A2L-Name: nr_cyc_ad_dc_bal_hom[RNG_IS]) NR_CYC_AD_DC_BAL_HOM[RNG_L]   Min: 0 Max: 255 |
| STAT_COND | unsigned long | Externe Anseuerung fuer Zylinderbalancing gesetzt(A2L-Name: lv_er_bal_hom_ena_ext) LV_ER_BAL_HOM_ENA_EXT   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-krann"></a>
### STEUERN_KRANN

0x3101F0E3 STEUERN_KRANN Ansteuern Krann-Adaptionswerte (Anforderung aus CP5404)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_WERT | long | Drehzahl NKW_SOLL   Einheit: Upm   Min: -32768 Max: 32767 |
| RK_SOLL_KR_WERT | real | Relative Krafstofffuellung RK_SOLL_KR   Einheit: %   Min: -1600 Max: 1599.9511 |
| TANS_WERT | real | Ansauglufttemperatur TANS   Einheit: C   Min: -3276.8 Max: 3276.7 |
| TMOT_WERT | real | Kuehlwassertemperatur TMOT   Einheit: C   Min: -327.68 Max: 327.67 |
| BA_IST_WERT | string | Istbetriebsart BA_IST   Min: 0 Max: 8 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-gen"></a>
### START_SYSTEMCHECK_GEN

0x3101F02A START_SYSTEMCHECK_GEN Diagnosefunktion Generatortest 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-msainfo-aep"></a>
### STATUS_MSAINFO_AEP

0x224018 _STATUS_MSAINFO_AEP Infospeicher Motor-Start/Stop Automatik (MSA) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LADUNGSMENGE_GESAMT_WERT | real | Kumulierte, verbrauchte Ladungsmenge 2BYTE_in 0 bis 19087Ah   Einheit: Ah   Min: 0 Max: 190872 |
| STAT_LADUNGSMENGE_GESAMT_EINH | string | Ah |
| STAT_ANZAHL_MOTORSTART_GESAMT | real | Gesamtzahl Starts 2BYTE in 0 bis 327675   Min: 0 Max: 327675 |
| STAT_ANZAHL_MSASTART_GESAMT | real | Anzahl MSA Starts 2BYTE in 0 bis 327675   Min: 0 Max: 327675 |
| STAT_ANZAHL_FZGSTOP_GESAMT | real | Anzahl Fahrzeugstops 2BYTE in 0 bis 327675   Min: 0 Max: 327675 |
| STAT_ZEIT_IN_MSA_GESAMT_WERT | real | Zeit in MSA 2BYTE in 0 bis 3276750s   Einheit: s   Min: 0 Max: 3276750 |
| STAT_ZEIT_IN_MSA_GESAMT_EINH | string | Sekunde |
| STAT_ZEIT_IN_FZGSTOP_GESAMT_WERT | real | Zeit in Fahrzeugstop 2BYTE in 0 bis 3276750s   Einheit: s   Min: 0 Max: 3276750 |
| STAT_ZEIT_IN_FZGSTOP_GESAMT_EINH | string | Sekunde |
| STAT_MSA_STOP_1_MIN_BZE_SPANNUNG_WERT | real | erste minimale Startspannungslage vom BZE3 gemessen bei MSA 1 Byte in 0 bis 255   Einheit: V   Min: 0 Max: 25,5 |
| STAT_MSA_STOP_1_MIN_BZE_SPANNUNG_EINH | string | Volt |
| STAT_MSA_STOP_3_MIN_BZE_SPANNUNG_WERT | real | zweite minimale Startspannungslage vom BZE3 gemessen bei MSA 1 Byte in 0 bis 255  Einheit: V  Min: 0 Max: 25,5 |
| STAT_MSA_STOP_3_MIN_BZE_SPANNUNG_EINH | string | Volt |
| STAT_BATTSPG_DSOC_INTERVALL1_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG1 und K_DSOCMSADG2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL1_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL2_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG2 und K_DSOCMSADG3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL2_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL3_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG3 und K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL3_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL4_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC groesser K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL4_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL1_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG1 und K_DSOCMSADG2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL1_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL2_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG2 und K_DSOCMSADG3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL2_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL3_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG3 und K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL3_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL4_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC groesser K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL4_UEBER_TGRENZ_EINH | string | V |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL1_WERT | unsigned long | Relative Haeufigkeit der MSA-Stops mit Dauer zwischen K_ZT0_MSASTP und K_ZT1_MSASTP 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.961 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL1_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL2_WERT | unsigned long | Relative Haeufigkeit der MSA-Stops mit Dauer zwischen K_ZT1_MSASTP und K_ZT2_MSASTP 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.961 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL2_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL3_WERT | unsigned long | Relative Haeufigkeit der MSA-Stops mit Dauer zwischen K_ZT2_MSASTP und K_ZT3_MSASTP 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.961 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL3_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL4_WERT | unsigned long | Relative Haeufigkeit der MSA-Stops mit Dauer groesser und K_ZT3_MSASTP 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.961 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL4_EINH | string | percent |
| STAT_MSA_STOP_1_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 1 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_1_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_1_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 1 2BYTE in 0 bis 65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_1_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_1_TEMP_WERT | real | Temp MSA-Stop 1 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_1_TEMP_EINH | string | degreeC |
| STAT_MSA_STOP_2_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_2_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_2_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 2 2BYTE in 0 bis 65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_2_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_2_TEMP_WERT | real | Temp MSA-Stop 2 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_2_TEMP_EINH | string | degreeC |
| STAT_MSA_STOP_3_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_3_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_3_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 3 2BYTE in 0 bis 65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_3_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_3_TEMP_WERT | real | Temp MSA-Stop 3 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_3_TEMP_EINH | string | degreeC |
| STAT_MSA_EA_SOC_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer SOC 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_BATTERIESPANNUNG_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer BATTERIESPANNUNG 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE2_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE2 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE3_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE3 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE4_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE4 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE5_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE5 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE6_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE6 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE7_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE7 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_SOC_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer SOC 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_STRTSPG_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Startspannung 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_DIAGNOSE_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Generator-Diagnose 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_TBATT_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Batterietemperatur 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_TRAMODE_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Tra-Mode 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_ZYKL_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Zyklisierung 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_BNSTROM_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer zu hoher Bordnetzstrom 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_RESERVE2_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer RESERVE2 1BIT   1: aktiv    0: nicht aktiv |
| STAT_REL_HAEUFIGKEIT_AV_SOC_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV SOC 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_SOC_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_STRTSPG_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV Startspannung 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_STRTSPG_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_DIAGNOSE_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV Diagnose 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_DIAGNOSE_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_TBATT_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV TBatt 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_TBATT_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_ZYKL_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV Zyklisierung 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_ZYKL_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_TRAMODE_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV Transportmode 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_TRAMODE_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_BNSTROM_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV Bordnetzstrom 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_BNSTROM_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_RESERVE2_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV RESERVE2 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_RESERVE2_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_EA_SOC_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund EA SOC 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_EA_SOC_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_EA_BATTERIESPANNUNG_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund EA BATTERIESPANNUNG 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_EA_BATTERIESPANNUNG_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-p"></a>
### STEUERN_ENDE_DMTL_P

0x2F60CC00 STEUERN_ENDE_DMTL_P Diagnosemodul-Tank Leckage Pumpe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-ecu-config-reset"></a>
### ECU_CONFIG_RESET

0x2E5FF204 ECU_CONFIG_RESET Variante loeschen Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_AT_WERT | unsigned long | Automatik Getriebe LV_AT   Min: 0 Max: 1 |
| SW_ARS_WERT | unsigned long | ARS Aktive Roll-Stabilisierung LV_VAR_ARS   Min: 0 Max: 1 |
| SW_EBOX_CFA_WERT | unsigned long | E-Box-Luefter LV_VAR_EBOX_CFA   Min: 0 Max: 1 |
| SW_MSW_WERT | unsigned long | Multifunktionslenkrad LV_VAR_MSW   Min: 0 Max: 1 |
| SW_SOF_WERT | unsigned long | Soundklappe LV_VAR_SOF   Min: 0 Max: 1 |
| SW_SOF_SWI_WERT | unsigned long | Sport-Taster CONF_SOF_SWI   Min: 0 Max: 1 |
| SW_GEAR_WERT | unsigned long | Komfortstart LV_VAR_BN_GEAR_REV   Min: 0 Max: 1 |
| SW_EF_WERT | unsigned long | Abgasklappe LV_VAR_EF   Min: 0 Max: 1 |
| SW_LIN_COMP_WERT | unsigned long | LIN Komponenten Kuehlerjalousie oben und unten, IBS, CWP, DCDC LIN Komponenten   Min: 0 Max: 1 |
| SW_RLY_ST_WERT | unsigned long | Starterrelais LV_VAR_RLY_ST   Min: 0 Max: 1 |
| SW_LSH_DOWN_WERT | unsigned long | Lambdasonde hinter Katalysator LV_VAR_LSH_DOWN   Min: 0 Max: 1 |
| SW_LSH_UP_WERT | unsigned long | Lambdasonde vor Katalysator LV_VAR_LSH_UP   Min: 0 Max: 1 |
| SW_BN_TRL_WERT | unsigned long | Anhaengermodul LV_VAR_BN_TRL   Min: 0 Max: 1 |
| SW_ETCU_SPT_WERT | unsigned long | Sportgetriebe  (A2L-Name: lv_var_etcu_spt) LV_VAR_ETCU_SPT   Min: 0 Max: 1 |
| SW_TCT_WERT | unsigned long | Doppelkuplungsgetriebe (A2L-Name: lv_var_tct) LV_VAR_TCT   Min: 0 Max: 1 |
| SW_AEB_WERT | unsigned long | Motorlager (A2L-Name: lv_var_aeb) LV_VAR_AEB   Min: 0 Max: 1 |
| SW_TQ_PBR_WERT | unsigned long | Elektromechanische Feststellbremse (A2L-Name: lv_var_tq_pbr) LV_VAR_TQ_PBR   Min: 0 Max: 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-v"></a>
### STEUERN_ENDE_DMTL_V

0x2F60CD00 STEUERN_ENDE_DMTL_V Diagnosemodul-Tank Leckage Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-uvlss"></a>
### STEUERN_UVLSS

0x2F602003 STEUERN_UVLSS Versorgung Einspritzung / Zuendung ansteuern Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PHY_UVLSS_WERT | unsigned long | Spannung Versorgung Einspritzung / Zuendung LV_RLY_HPDI_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_UVLSS_WERT | unsigned long | Timeout Versorgung Einspritzung / Zuendung 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-verbraucherstrom-efii"></a>
### STEUERN_ENDE_VERBRAUCHERSTROM_EFII

Ansteuerung Verbraucherstrommessung EFII (IBS) beenden UDS  : $31   RoutineControl UDS  : $02   routineControlType UDS  : $7002 routineIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-enws"></a>
### STEUERN_ENWS

0x2F60ED03 STEUERN_ENWS Vanos Einlass Ventil ansteuern Aktivierung: Drehzahl &gt; 1000 1/min Activation: N &gt; C_N_MIN_KWP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ENWS_WERT | real | Tastverhaeltniss Ventil Einlassnockenwellensteller Bank 1 CAM_SP_IN_EXT_ADJ[1]   Einheit: CRK   Min: -128 Max: 52300 |
| SW_TO_ENWS_WERT | unsigned long | Timeout Ventil Einlassnockenwellensteller Bank 1 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-gen"></a>
### STATUS_SYSTEMCHECK_GEN

0x3103F02A STATUS_SYSTEMCHECK_GEN Auslesen Diagnosefunktion Generatortest Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1_TEXT | string | Stati fuer Diagnosefunktion Generatortest ST_GENTEST |
| STAT_DIAGNOSE_1_WERT | int | Stati fuer Diagnosefunktion Generatortest ST_GENTEST |
| STAT_FI_GENEL_TEXT | string | Status elektrischer Fehler Generator GENIUTEST_ERR[0] |
| STAT_FI_GENEL_WERT | int | Status elektrischer Fehler Generator GENIUTEST_ERR[0] |
| STAT_FI_GENMECH_TEXT | string | Status mechanischer Fehler Generator GENIUTEST_ERR[1] |
| STAT_FI_GENMECH_WERT | int | Status mechanischer Fehler Generator GENIUTEST_ERR[1] |
| STAT_FI_GENHT_TEXT | string | Status Hochtemperaturfehler Generator GENIUTEST_ERR[2] |
| STAT_FI_GENHT_WERT | int | Status Hochtemperaturfehler Generator GENIUTEST_ERR[2] |
| STAT_FI_GENUPL_TEXT | string | Plausibilitaet Generatortyp GENIUTEST_ERR[3] |
| STAT_FI_GENUPL_WERT | int | Plausibilitaet Generatortyp GENIUTEST_ERR[3] |
| STAT_FI_GENKOMM_TEXT | string | Status Generatorkommunikation GENIUTEST_ERR[4] |
| STAT_FI_GENKOMM_WERT | int | Status Generatorkommunikation GENIUTEST_ERR[4] |
| STAT_FI_GENELB_TEXT | string | Plausibilitaet Generatorspannung aus Berechnung GENIUTEST_ERR[5] |
| STAT_FI_GENELB_WERT | int | Plausibilitaet Generatorspannung aus Berechnung GENIUTEST_ERR[5] |
| STAT_FI_GENHTB_TEXT | string | Hochtemperaturfehler Generator aus Berechnung GENIUTEST_ERR[6] |
| STAT_FI_GENHTB_WERT | int | Hochtemperaturfehler Generator aus Berechnung GENIUTEST_ERR[6] |
| STAT_FI_GENREGUPL_TEXT | string | Plausibilitaet Generatorregler GENIUTEST_ERR[7] |
| STAT_FI_GENREGUPL_WERT | int | Plausibilitaet Generatorregler GENIUTEST_ERR[7] |
| STAT_DF_HIGH_TEXT | string | Status Generatorauslastung GENIUTEST_AB[0] |
| STAT_DF_HIGH_WERT | int | Status Generatorauslastung GENIUTEST_AB[0] |
| STAT_GENITEST_TOL_WERT | real | Toleranzbereich fuer Abweichung vom Sollwert Strom (GENITEST_TOL) GENITEST_TOL   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_GENITEST_TOL_EINH | string | percent |
| STAT_GENUTEST_TOL_WERT | real | Toleranzbereich fuer Abweichung vom Sollwert Spannung  (GENUTEST_TOL) GENUTEST_TOL   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_GENUTEST_TOL_EINH | string | percent |
| STAT_I_GENTEST_WERT | unsigned long | Modellierter Generatorstrom I_GENTEST   Einheit: A   Min: 0 Max: 255 |
| STAT_I_GENTEST_EINH | string | A |
| STAT_U_GENTEST_WERT | real | Generatorsollspannung U_GENTEST   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_U_GENTEST_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-e-luefter"></a>
### STEUERN_ENDE_E_LUEFTER

0x2F60DA00 STEUERN_ENDE_E_LUEFTER E-Luefter Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-anws"></a>
### STEUERN_ENDE_ANWS

0x2F60EE00 STEUERN_ENDE_ANWS Vanos Auslass Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-msv"></a>
### STEUERN_MSV

0x2F60BD03 STEUERN_MSV Mengensteuerventil ansteuern Aktivierung: 50000 hPa &lt; Raildruck &lt; 200000 hPa UND Leerlauf Activation: C_FUP_MIN_KWP &lt; FUP &lt; C_FUP_MAX_KWP UND LV_IS = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_MSV_WERT | real | Tastverhaeltniss Mengensteuerventil FUP_SP_EXT_ADJ   Einheit: hPa   Min: 0 Max: 347776 |
| SW_TO_MSV_WERT | unsigned long | Timeout Mengensteuerventil 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-discodbsr"></a>
### STATUS_DISCODBSR

0x225F7E STATUS_DISCODBSR Verriegelung des betriebsstundenrelevanten Kodierbereichs (Auslesen vom Bit: DIS_COD_BSR)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIS_COD_BSR | unsigned long | Verriegelung des betriebsstundenrelevanten Kodierbereichs (Auslesen vom Bit: DIS_COD_BSR) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-pm-messemode"></a>
### START_SYSTEMCHECK_PM_MESSEMODE

0x3101F0F6 START_SYSTEMCHECK_PM_MESSEMODE Ansteuern Messemode Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-obd-demo-momentenbegrenzung"></a>
### STOP_OBD_DEMO_MOMENTENBEGRENZUNG

0x3102F09E STOP_OBD_DEMO_MOMENTENBEGRENZUNG OBD Demo Momentenbegrenzung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-gvobd"></a>
### STATUS_GVOBD

0x225F80 STATUS_GVOBD Gemischvertrimmung fuer OBD-Demo und PVE lesen. Bank 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_F_MK_KORR_EXT_XZYL_1_WERT | real | Faktor auf Einspritzung Zylinder 1 F_mk_korr_ext_xzyl_[1]   Min: 0 Max: 1.99996948242188 |
| STAT_F_MK_KORR_EXT_XZYL_5_WERT | real | Faktor auf Einspritzung Zylinder 5 F_mk_korr_ext_xzyl_[2]   Min: 0 Max: 1.99996948242188 |
| STAT_F_MK_KORR_EXT_XZYL_3_WERT | real | Faktor auf Einspritzung Zylinder 3 F_mk_korr_ext_xzyl_[3]   Min: 0 Max: 1.99996948242188 |
| STAT_F_MK_KORR_EXT_XZYL_6_WERT | real | Faktor auf Einspritzung Zylinder 6 F_mk_korr_ext_xzyl_[4]   Min: 0 Max: 1.99996948242188 |
| STAT_F_MK_KORR_EXT_XZYL_2_WERT | real | Faktor auf Einspritzung Zylinder 2 F_mk_korr_ext_xzyl_[5]   Min: 0 Max: 1.99996948242188 |
| STAT_F_MK_KORR_EXT_XZYL_4_WERT | real | Faktor auf Einspritzung Zylinder 4 F_mk_korr_ext_xzyl_[6]   Min: 0 Max: 1.99996948242188 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-hdpr"></a>
### STEUERN_ENDE_HDPR

0x2F608200 STEUERN_ENDE_HDPR Hochdruckpumpenrelais Ansteuerung beenden NO_CON

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-klann"></a>
### STATUS_KLANN

0x3103F0E4 STATUS_KLANN Auslesen Krann-Adaptionswerte Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLNN_TEST_WERT | real | Lambdaadaptionswert fuer Testerabfrage KLANN_TEST1   Min: -50 Max: 49.9984 |
| STAT_KLNN_TEST_2_WERT | real | Faktor aus Lambdaregelungsadaption fuer Bank 2, Testerabfrage (A2L-Name: Klann_test2) KLANN_TEST2   Min: -50 Max: 49.9984 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-adaption-opf"></a>
### STATUS_ADAPTION_OPF

0x22419B STATUS_ADAPTION_OPF Nutzung  des OPF lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZ_ADAPT_RUSSM | unsigned long | Anzahl der Adaptionen des Russmodels 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ANZ_ADAPT_ASCHEM | unsigned long | Anzahl Adaptionen Aschemodel 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ADAP_RUSS_KM_1_WERT | unsigned long | km-Stand Russmodel Adaption 1 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_RUSS_KM_1_EINH | string | kilometer |
| STAT_ADAP_RUSS_KM_2_WERT | unsigned long | km-Stand Russmodel Adaption 2 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_RUSS_KM_2_EINH | string | kilometer |
| STAT_ADAP_RUSS_KM_3_WERT | unsigned long | km-Stand Russmodel Adaption 3 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_RUSS_KM_3_EINH | string | kilometer |
| STAT_ADAP_RUSS_KM_4_WERT | unsigned long | km-Stand Russmodel Adaption 4 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_RUSS_KM_4_EINH | string | kilometer |
| STAT_ADAP_RUSS_KM_5_WERT | unsigned long | km-Stand Russmodel Adaption 5 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_RUSS_KM_5_EINH | string | kilometer |
| STAT_ADAP_RUSS_KM_6_WERT | unsigned long | km-Stand Russmodel Adaption 6 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_RUSS_KM_6_EINH | string | kilometer |
| STAT_ADAP_RUSS_KM_7_WERT | unsigned long | km-Stand Russmodel Adaption 7 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_RUSS_KM_7_EINH | string | kilometer |
| STAT_ADAP_RUSS_KM_8_WERT | unsigned long | km-Stand Russmodel Adaption 8 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_RUSS_KM_8_EINH | string | kilometer |
| STAT_ADAP_RUSS_KM_9_WERT | unsigned long | km-Stand Russmodel Adaption 9 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_RUSS_KM_9_EINH | string | kilometer |
| STAT_ADAP_RUSS_KM_10_WERT | unsigned long | km-Stand Russmodel Adaption 10 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_RUSS_KM_10_EINH | string | kilometer |
| STAT_ADAP_ASCHE_KM_1_WERT | unsigned long | km-Stand Aschemodel Adaption 1 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_ASCHE_KM_1_EINH | string | kilometer |
| STAT_ADAP_ASCHE_KM_2_WERT | unsigned long | km-Stand Aschemodel Adaption 2 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_ASCHE_KM_2_EINH | string | kilometer |
| STAT_ADAP_ASCHE_KM_3_WERT | unsigned long | km-Stand Aschemodel Adaption 3 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_ASCHE_KM_3_EINH | string | kilometer |
| STAT_ADAP_ASCHE_KM_4_WERT | unsigned long | km-Stand Aschemodel Adaption 4 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_ASCHE_KM_4_EINH | string | kilometer |
| STAT_ADAP_ASCHE_KM_5_WERT | unsigned long | km-Stand Aschemodel Adaption 5 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_ASCHE_KM_5_EINH | string | kilometer |
| STAT_ADAP_ASCHE_KM_6_WERT | unsigned long | km-Stand Aschemodel Adaption 6 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_ASCHE_KM_6_EINH | string | kilometer |
| STAT_ADAP_ASCHE_KM_7_WERT | unsigned long | km-Stand Aschemodel Adaption 7 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_ASCHE_KM_7_EINH | string | kilometer |
| STAT_ADAP_ASCHE_KM_8_WERT | unsigned long | km-Stand Aschemodel Adaption 8 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_ASCHE_KM_8_EINH | string | kilometer |
| STAT_ADAP_ASCHE_KM_9_WERT | unsigned long | km-Stand Aschemodel Adaption 9 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_ASCHE_KM_9_EINH | string | kilometer |
| STAT_ADAP_ASCHE_KM_10_WERT | unsigned long | km-Stand Aschemodel Adaption 10 4BYTE_IN_0_BIS_4294967295_KM   Einheit: km |
| STAT_ADAP_ASCHE_KM_10_EINH | string | kilometer |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-mil"></a>
### STEUERN_ENDE_MIL

0x2F60D400 STEUERN_ENDE_MIL MIL (Malfunction Indicator Lamp) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ewap"></a>
### STEUERN_ENDE_EWAP

0x2F60BF00 STEUERN_ENDE_EWAP elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden NO_CON

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-lds1"></a>
### STEUERN_LDS1

0x2F60B603 STEUERN_LDS1 Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LDS1_WERT | real | Tastverhaeltniss Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) WGPWM_EXT_ADJ[1]   Einheit: %   Min: 0 Max: 99.9984741210938 |
| SW_TO_LDS1_WERT | unsigned long | Timeout Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-aep-info-1"></a>
### STATUS_SYSTEMCHECK_AEP_INFO_1

0x224022 STATUS_SYSTEMCHECK_AEP_INFO_1 Intelligenter Batteriesensor Bitfeld Pminfo1 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIELADUNG_GESAMT_WERT | unsigned long | AEPINFO1_[0] 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIELADUNG_GESAMT_EINH | string | Ah |
| STAT_BATTERIELADUNG_BILANZ_WERT | unsigned long | Differenz LADUNG - ENTLADUNG in Ah 0 - 65535 |
| STAT_BATTERIELADUNG_BILANZ_EINH | string | Ah |
| STAT_BATTERIELADUNG_SALDO_WERT | long | Differenz LADUNG - ENTLADUNG in Ah |
| STAT_BATTERIELADUNG_SALDO_EINH | string | Ah |
| STAT_BATTERIELADUNG_SALDO_INFO | string | positives Ergebnis = Aufladung, negatives Ergebnis = Entladung |
| STAT_BATTERIEENTLADUNG_GESAMT_WERT | unsigned long | AEPINFO1_[1] 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIEENTLADUNG_GESAMT_EINH | string | Ah |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_WERT | unsigned long | AEPINFO1_[2] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_INFO | string | 0% &lt; Soc_rel = 40% |
| STAT_ZEIT_IM_LADUNGSBEREICH_A_B_WERT | unsigned long | AEPINFO1_[3] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_A_B_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH__A_B_INFO | string | 40% &lt; Soc_rel = 55% |
| STAT_ZEIT_IM_LADUNGSBEREICH_B_C_WERT | unsigned long | AEPINFO1_[4] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_B_C_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH__B_C_INFO | string | 55% &lt; Soc_rel = 70% |
| STAT_ZEIT_IM_LADUNGSBEREICH_C_D_WERT | unsigned long | AEPINFO1_[5] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_C_D_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH__C_D_INFO | string | 70% &lt; Soc_rel = 85% |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_WERT | unsigned long | AEPINFO1_[6] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_INFO | string | 85% &lt; Soc_rel |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_WERT | unsigned long | AEPINFO1_[7] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_INFO | string | T_batt = 0°C |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_WERT | unsigned long | AEPINFO1_[8] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_INFO | string | 0°C &lt; T_batt = 10°C |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_WERT | unsigned long | AEPINFO1_[9] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_INFO | string | 10°C &lt; T_batt = 30°C |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_WERT | unsigned long | AEPINFO1_[10] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_INFO | string | 30°C &lt; T_batt = 60°C |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_WERT | unsigned long | AEPINFO1_[11] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_INFO | string | 60°C &lt; T_batt |
| STAT_KM_STAND_AKTUELL_WERT | unsigned long | AEPINFO1_[12] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_AKTUELL_EINH | string | kilometer |
| STAT_KM_STAND_VOR_1_TAG_WERT | unsigned long | AEPINFO1_[13] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_1_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_2_TAG_WERT | unsigned long | AEPINFO1_[14] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_2_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_3_TAG_WERT | unsigned long | AEPINFO1_[15] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_3_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_4_TAG_WERT | unsigned long | AEPINFO1_[16] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_4_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_5_TAG_WERT | unsigned long | AEPINFO1_[17] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_5_TAG_EINH | string | kilometer |
| STAT_BATTERIETAUSCH_LETZTER_WERT | unsigned long | AEPINFO1_[18] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_BATTERIETAUSCH_LETZTER_EINH | string | kilometer |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_WERT | unsigned long | AEPINFO1_[19] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_EINH | string | kilometer |
| STAT_ANZAHL_LEERLAUFDREHZAHLANHEBUNG_EPS | unsigned long | AEPINFO1_[20] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ANZAHL_LEERLAUFDREHZAHLANHEBUNG_IBS | unsigned long | AEPINFO1_[20] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_BATTERIEENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_WERT | unsigned long | AEPINFO1_[22] 2BYTE_in_0bis65534h   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIEENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_EINH | string | Ah |
| STAT_RUHESTROM_VOR_3_ZYKLEN_TEXT | string | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_3_ZYKLEN_WERT | int | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_3_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_2_ZYKLEN_TEXT | string | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_2_ZYKLEN_WERT | int | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_2_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_1_ZYKLUS_TEXT | string | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_1_ZYKLUS_WERT | int | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_1_ZYKLUS_EINH | string | - |
| STAT_RUHESTROM_AKTUELL_TEXT | string | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_AKTUELL_WERT | int | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_AKTUELL_EINH | string | - |
| STAT_RUHESTROM_VOR_7_ZYKLEN_TEXT | string | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_7_ZYKLEN_WERT | int | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_7_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_6_ZYKLEN_TEXT | string | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_6_ZYKLEN_WERT | int | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_6_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_5_ZYKLEN_TEXT | string | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_5_ZYKLEN_WERT | int | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_5_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_4_ZYKLEN_TEXT | string | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_4_ZYKLEN_WERT | int | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_4_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_11_ZYKLEN_TEXT | string | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_11_ZYKLEN_WERT | int | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_11_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_10_ZYKLEN_TEXT | string | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_10_ZYKLEN_WERT | int | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_10_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_9_ZYKLEN_TEXT | string | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_9_ZYKLEN_WERT | int | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_9_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_8_ZYKLEN_TEXT | string | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_8_ZYKLEN_WERT | int | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_8_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_15_ZYKLEN_TEXT | string | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_15_ZYKLEN_WERT | int | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_15_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_14_ZYKLEN_TEXT | string | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_14_ZYKLEN_WERT | int | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_14_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_13_ZYKLEN_TEXT | string | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_13_ZYKLEN_WERT | int | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_13_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_12_ZYKLEN_TEXT | string | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_12_ZYKLEN_WERT | int | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_12_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_19_ZYKLEN_TEXT | string | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_19_ZYKLEN_WERT | int | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_19_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_18_ZYKLEN_TEXT | string | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_18_ZYKLEN_WERT | int | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_18_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_17_ZYKLEN_TEXT | string | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_17_ZYKLEN_WERT | int | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_17_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_16_ZYKLEN_TEXT | string | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_16_ZYKLEN_WERT | int | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_16_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_23_ZYKLEN_TEXT | string | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_23_ZYKLEN_WERT | int | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_23_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_22_ZYKLEN_TEXT | string | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_22_ZYKLEN_WERT | int | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_22_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_21_ZYKLEN_TEXT | string | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_21_ZYKLEN_WERT | int | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_21_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_20_ZYKLEN_TEXT | string | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_20_ZYKLEN_WERT | int | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_20_ZYKLEN_EINH | string | - |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_AUS_WERT | real | AEPINFO1_[29] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_EIN_WERT | real | AEPINFO1_[29] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_1_TAG_WERT_MOTOR_AUS_WERT | real | AEPINFO1_[30] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_1_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_1_TAG_MOTOR_EIN_WERT | real | AEPINFO1_[30] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_1_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_2_TAG_WERT_MOTOR_AUS_WERT | real | AEPINFO1_[31] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_2_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_2_TAG_MOTOR_EIN_WERT | real | AEPINFO1_[31] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_2_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_3_TAG_WERT_MOTOR_AUS_WERT | real | AEPINFO1_[32] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_3_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_3_TAG_MOTOR_EIN_WERT | real | AEPINFO1_[32] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_3_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_4_TAG_WERT_MOTOR_AUS_WERT | real | AEPINFO1_[33] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_4_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_4_TAG_MOTOR_EIN_WERT | real | AEPINFO1_[33] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_4_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_5_TAG_WERT_MOTOR_AUS_WERT | real | AEPINFO1_[34] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_5_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_5_TAG_MOTOR_EIN_WERT | real | AEPINFO1_[34] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_5_TAG_MOTOR_EIN_EINH | string | Ah |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-aep-info-2"></a>
### STATUS_SYSTEMCHECK_AEP_INFO_2

0x224023 STATUS_SYSTEMCHECK_AEP_INFO_2 Intelligenter Batteriesensor Bitfeld Pminfo2 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIE_KAPAZITAET_WERT | unsigned long | AEPINFO2_[0] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIE_KAPAZITAET_EINH | string | Ah |
| STAT_SOH_WERT | real | AEPINFO2_[1] 1BYTE_in_minus128bis127prozent   Einheit: % |
| STAT_SOH_EINH | string | percent |
| STAT_SOC_FIT_WERT | unsigned long | AEPINFO2_[2] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_SOC_FIT_EINH | string | percent |
| STAT_TEMP_SAISON_WERT | long | AEPINFO2_[3] 1BYTE_in_minus128bis127gradCelsius   Einheit: C |
| STAT_TEMP_SAISON_EINH | string | degreeC |
| STAT_ANZAHL_RUHESPANNUNGSAUSWERTUNGEN_OCV | unsigned long | AEPINFO2_[4] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_Q_SOC_AKTUELL_WERT | unsigned long | AEPINFO2_[5] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_AKTUELL_EINH | string | Ah |
| STAT_Q_SOC_VOR_1_TAG_WERT | unsigned long | AEPINFO2_[6] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_1_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_2_TAG_WERT | unsigned long | AEPINFO2_[7] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_2_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_3_TAG_WERT | unsigned long | AEPINFO2_[8] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_3_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_4_TAG_WERT | unsigned long | AEPINFO2_[9] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_4_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_5_TAG_WERT | unsigned long | AEPINFO2_[10] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_5_TAG_EINH | string | Ah |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_WERT | unsigned long | AEPINFO2_[11] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_WERT | unsigned long | AEPINFO2_[12] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_WERT | unsigned long | AEPINFO2_[13] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_WERT | unsigned long | AEPINFO2_[14] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_WERT | unsigned long | AEPINFO2_[15] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_WERT | unsigned long | AEPINFO2_[16] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_AKTUELL_WERT | unsigned long | AEPINFO2_[17] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_AKTUELL_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_WERT | unsigned long | AEPINFO2_[18] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_WERT | unsigned long | AEPINFO2_[19] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_WERT | unsigned long | AEPINFO2_[20] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_WERT | unsigned long | AEPINFO2_[21] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_WERT | unsigned long | AEPINFO2_[22] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_EINH | string | percent |
| STAT_BZE_DIAG_0 | unsigned long | AEPINFO2_[23] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_1 | unsigned long | AEPINFO2_[24] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_2 | unsigned long | AEPINFO2_[25] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_3 | unsigned long | AEPINFO2_[26] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_4 | unsigned long | AEPINFO2_[27] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-opf"></a>
### STATUS_SYSTEMCHECK_OPF

0x3103F07B STATUS_SYSTEMCHECK_OPF OPF Systemtest

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OPF_FS_TEXT | string | Funktionsstatus OPF 1BYTE FUNKTIONSSTATUS |
| STAT_OPF_FS_WERT | int | Funktionsstatus OPF 1BYTE FUNKTIONSSTATUS |
| STAT_OPF_FS_ERW | unsigned long | Funktionsstatus Erweitert Systemtest Otto Partikel Filter 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_OPF_ABLAUF | unsigned long | Ablaufstatus des Systemtest 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_OPF_REGENERATIONSABRUCH_1 | unsigned long | Regenerationsabbruch letzter Regeneration Teil 1 2BYTE_DUMMY |
| STAT_OPF_REGENERATIONSABRUCH_2 | unsigned long | Regenerationsabbruch letzter Regeneration Teil 2 2BYTE_DUMMY |
| STAT_OPF_REGENERATIONSVERHINDERER_1 | unsigned long | Regeneration kann aktuell nicht begonnen werden Teil 1 2BYTE_DUMMY |
| STAT_OPF_REGENERATIONSVERHINDERER_2 | unsigned long | Regeneration kann aktuell nicht begonnen werden Teil 2 2BYTE_DUMMY |
| STAT_OPF_VERBESSERUNGS_INDEX_WERT_WERT | real | Bewertungsinfo Regenerationserfolg in der Werkstattregeneration 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_OPF_VERBESSERUNGS_INDEX_WERT_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-tev"></a>
### START_SYSTEMCHECK_TEV

0x3101F022 START_SYSTEMCHECK_TEV Ansteuern Diagnosefunktion Tankentlueftungsventil Aktivierung: Klemme 15 = EIN UND Phase Motorstart beendet = EIN UND Funktionscheck TEV = EIN UND Geschwindigkeit = 0 km/h UND LV_MAF_SP_TQI_DYW_DIAGCPS = 1 UND (Betriebsart TEV = 1 ODER Betriebsart TEV = 2) UND Fehlerspeichereintrag TEV = AUS Activation: LV_IGK = 1 UND LV_ST_END = 1 UND LV_INH_DIAGCPS = 0 UND VS = 0 UND LV_MAF_SP_TQI_DYW_DIAGCPS = 1 UND (OPM_AV_DIAGCPS = 1 ODER OPM_AV_DIAGCPS = 2) UND LV_ERR_DIAGCPS = 0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (149 × 2)
- [FARTTEXTE](#table-farttexte) (35 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (7 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (365 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [LIEFERANTENLIN](#table-lieferantenlin) (225 × 2)
- [IARTTEXTE](#table-iarttexte) (35 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [CBSKENNUNG](#table-cbskennung) (12 × 3)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (1223 × 4)
- [FUMWELTTEXTE](#table-fumwelttexte) (241 × 9)
- [IBS_DEAK](#table-ibs-deak) (10 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (5 × 2)
- [IORTTEXTE](#table-iorttexte) (1223 × 4)
- [IUMWELTTEXTE](#table-iumwelttexte) (241 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (4 × 2)
- [MSD85UDS_CNV_S_2_DEF_BIT_UB_741_CM](#table-msd85uds-cnv-s-2-def-bit-ub-741-cm) (2 × 2)
- [RES_0X1061_R](#table-res-0x1061-r) (1 × 13)
- [SG_FUNKTIONEN](#table-sg-funktionen) (533 × 16)
- [STATUS_GENMANUFAK](#table-status-genmanufak) (8 × 2)
- [STATUS_GENTYPKENN](#table-status-gentypkenn) (27 × 2)
- [STATCLIENTAUTHTXT](#table-statclientauthtxt) (4 × 2)
- [STATEWSVERTXT](#table-statewsvertxt) (3 × 2)
- [STATFREESKTXT](#table-statfreesktxt) (3 × 2)
- [TABLE_STATUS_BATTERIEZUSTAND](#table-table-status-batteriezustand) (4 × 2)
- [TABLE_STATUS_ECO2_FUNKTIONSSTATI](#table-table-status-eco2-funktionsstati) (11 × 2)
- [TABLE_STATUS_IBS_BZE](#table-table-status-ibs-bze) (2 × 2)
- [TABLE_STATUS_LETZTER_BATTERIEWECHSEL](#table-table-status-letzter-batteriewechsel) (2 × 2)
- [TABLE_STATUS_TIEFENTLADUNG](#table-table-status-tiefentladung) (2 × 2)
- [TABLE_STATUS_WASSERVERLUST](#table-table-status-wasserverlust) (2 × 2)
- [_CNV_S_11_EGCP_RANGE_247](#table-cnv-s-11-egcp-range-247) (12 × 2)
- [_CNV_S_11_EGCP_RANGE_249](#table-cnv-s-11-egcp-range-249) (12 × 2)
- [_CNV_S_12__CNV_S_12__655](#table-cnv-s-12-cnv-s-12-655) (13 × 2)
- [_CNV_S_12__CNV_S_12__656](#table-cnv-s-12-cnv-s-12-656) (13 × 2)
- [_CNV_S_13_RANGE_STAT_839](#table-cnv-s-13-range-stat-839) (13 × 2)
- [_CNV_S_19_ECOP_RANGE_763](#table-cnv-s-19-ecop-range-763) (20 × 2)
- [_CNV_S_19_ECOP_RANGE_764](#table-cnv-s-19-ecop-range-764) (20 × 2)
- [_CNV_S_3_THRO_RANGE_890](#table-cnv-s-3-thro-range-890) (4 × 2)
- [_CNV_S_3_THRO_RANGE_891](#table-cnv-s-3-thro-range-891) (4 × 2)
- [_CNV_S_4_EGCP_RANGE_251](#table-cnv-s-4-egcp-range-251) (5 × 2)
- [_CNV_S_4_EGCP_RANGE_253](#table-cnv-s-4-egcp-range-253) (5 × 2)
- [_CNV_S_4_EGCP_RANGE_259](#table-cnv-s-4-egcp-range-259) (5 × 2)
- [_CNV_S_4_EGCP_RANGE_261](#table-cnv-s-4-egcp-range-261) (5 × 2)
- [_CNV_S_5_LACO_RANGE_298](#table-cnv-s-5-laco-range-298) (6 × 2)
- [_CNV_S_5_LACO_RANGE_300](#table-cnv-s-5-laco-range-300) (6 × 2)
- [_CNV_S_5__CNV_S_5_D_607](#table-cnv-s-5-cnv-s-5-d-607) (6 × 2)
- [_CNV_S_5__CNV_S_5_D_608](#table-cnv-s-5-cnv-s-5-d-608) (6 × 2)
- [_CNV_S_6_RANGE_STAT_56](#table-cnv-s-6-range-stat-56) (7 × 2)
- [_CNV_S_7_EGCP_RANGE_232](#table-cnv-s-7-egcp-range-232) (8 × 2)
- [_CNV_S_7_EGCP_RANGE_234](#table-cnv-s-7-egcp-range-234) (8 × 2)
- [_CNV_S_7_RANGE_ECU__54](#table-cnv-s-7-range-ecu-54) (8 × 2)
- [_CNV_S_8_RANGE_STAT_144](#table-cnv-s-8-range-stat-144) (9 × 2)
- [_CNV_S_8_RANGE_STAT_145](#table-cnv-s-8-range-stat-145) (9 × 2)
- [_MSD87_R0DEF_ST_ATLSVC_BMSNF](#table-msd87-r0def-st-atlsvc-bmsnf) (9 × 2)
- [_MSD87_R0DEF_ST_ATLSVC_PVDK_BMSNF](#table-msd87-r0def-st-atlsvc-pvdk-bmsnf) (6 × 2)
- [_MSD87_R0_CNV_S_10_STATE_EOL__449_CM_4DC3200S](#table-msd87-r0-cnv-s-10-state-eol-449-cm-4dc3200s) (10 × 2)
- [_MSD87_R0_CNV_S_10_STATE_EOL__449_CM_4DC3200S_](#table-msd87-r0-cnv-s-10-state-eol-449-cm-4dc3200s) (10 × 2)
- [_MSD87_R0_CNV_S_10_STATE_EOL__960_CM_9SP8300S](#table-msd87-r0-cnv-s-10-state-eol-960-cm-9sp8300s) (10 × 2)
- [_MSD87_R0_CNV_S_13_STATE_DMTL_140_CM](#table-msd87-r0-cnv-s-13-state-dmtl-140-cm) (21 × 2)
- [_MSD87_R0_CNV_S_2_DEF_BIT_UW_683_CM_4DC3500S](#table-msd87-r0-cnv-s-2-def-bit-uw-683-cm-4dc3500s) (2 × 2)
- [_MSD87_R0_CNV_S_2__CNV_S_2_D_435_CM_0X4_792E940S](#table-msd87-r0-cnv-s-2-cnv-s-2-d-435-cm-0x4-792e940s) (2 × 2)
- [_MSD87_R0_CNV_S_4_CYBL_RANGE_179_CM_792A900S](#table-msd87-r0-cnv-s-4-cybl-range-179-cm-792a900s) (4 × 2)
- [_MSD87_R0_CNV_S_4_CYBL_RANGE_180_CM_792A900S](#table-msd87-r0-cnv-s-4-cybl-range-180-cm-792a900s) (4 × 2)
- [_MSD87_R0_CNV_S_4_RANGE_STAT_455_CM_4DC3200S](#table-msd87-r0-cnv-s-4-range-stat-455-cm-4dc3200s) (4 × 2)
- [_MSD87_R0_CNV_S_4_STATE_CH_776_CM_762E940S](#table-msd87-r0-cnv-s-4-state-ch-776-cm-762e940s) (4 × 2)
- [_MSD87_R0_CNV_S_5_DEF_BA_GDI_588_CM](#table-msd87-r0-cnv-s-5-def-ba-gdi-588-cm) (5 × 2)
- [_MSD87_R0_CNV_S_6_STATE_DIAG_157_CM](#table-msd87-r0-cnv-s-6-state-diag-157-cm) (6 × 2)
- [_MSD87_R0_TABEL_STATUS_OBD_MONITOR](#table-msd87-r0-tabel-status-obd-monitor) (2 × 2)
- [_MSD87_R0_TABEL_STATUS_OBD_READINESS](#table-msd87-r0-tabel-status-obd-readiness) (2 × 2)
- [_MSD87_R0_TABLE_FS](#table-msd87-r0-table-fs) (11 × 2)
- [_MSD87_R0_TABLE_GENIUTEST_AB_BIT0](#table-msd87-r0-table-geniutest-ab-bit0) (2 × 2)
- [_MSD87_R0_TABLE_GENIUTEST_ERR_BIT0](#table-msd87-r0-table-geniutest-err-bit0) (2 × 2)
- [_MSD87_R0_TABLE_GENIUTEST_ERR_BIT1](#table-msd87-r0-table-geniutest-err-bit1) (2 × 2)
- [_MSD87_R0_TABLE_GENIUTEST_ERR_BIT2](#table-msd87-r0-table-geniutest-err-bit2) (2 × 2)
- [_MSD87_R0_TABLE_GENIUTEST_ERR_BIT3](#table-msd87-r0-table-geniutest-err-bit3) (2 × 2)
- [_MSD87_R0_TABLE_GENIUTEST_ERR_BIT4](#table-msd87-r0-table-geniutest-err-bit4) (2 × 2)
- [_MSD87_R0_TABLE_GENIUTEST_ERR_BIT5](#table-msd87-r0-table-geniutest-err-bit5) (2 × 2)
- [_MSD87_R0_TABLE_GENIUTEST_ERR_BIT6](#table-msd87-r0-table-geniutest-err-bit6) (2 × 2)
- [_MSD87_R0_TABLE_GENIUTEST_ERR_BIT7](#table-msd87-r0-table-geniutest-err-bit7) (2 × 2)
- [_MSD87_R0_TABLE_STATUS_BATTERIEZUSTAND](#table-msd87-r0-table-status-batteriezustand) (4 × 2)
- [_MSD87_R0_TABLE_STATUS_IBS_BZE](#table-msd87-r0-table-status-ibs-bze) (2 × 2)
- [_MSD87_R0_TABLE_STATUS_LETZTER_BATTERIEWECHSEL](#table-msd87-r0-table-status-letzter-batteriewechsel) (2 × 2)
- [_MSD87_R0_TABLE_STATUS_TIEFENTLADEN](#table-msd87-r0-table-status-tiefentladen) (2 × 2)
- [_MSD87_R0_TABLE_STATUS_WASSERVERLUST](#table-msd87-r0-table-status-wasserverlust) (2 × 2)
- [_MSD87_R0_TABLE_ST_GENTEST](#table-msd87-r0-table-st-gentest) (8 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_BIT0](#table-msd87-r0-table-switch-position-bit0) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_BIT1](#table-msd87-r0-table-switch-position-bit1) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_BIT2](#table-msd87-r0-table-switch-position-bit2) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_BIT3](#table-msd87-r0-table-switch-position-bit3) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_BIT4](#table-msd87-r0-table-switch-position-bit4) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_BIT7](#table-msd87-r0-table-switch-position-bit7) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT0](#table-msd87-r0-table-switch-position-high-byte-bit0) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT1](#table-msd87-r0-table-switch-position-high-byte-bit1) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT2](#table-msd87-r0-table-switch-position-high-byte-bit2) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT3](#table-msd87-r0-table-switch-position-high-byte-bit3) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT4](#table-msd87-r0-table-switch-position-high-byte-bit4) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT5](#table-msd87-r0-table-switch-position-high-byte-bit5) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT6](#table-msd87-r0-table-switch-position-high-byte-bit6) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT7](#table-msd87-r0-table-switch-position-high-byte-bit7) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_LOW_BYTE_BIT2](#table-msd87-r0-table-switch-position-low-byte-bit2) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_LOW_BYTE_BIT3](#table-msd87-r0-table-switch-position-low-byte-bit3) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_LOW_BYTE_BIT6](#table-msd87-r0-table-switch-position-low-byte-bit6) (2 × 2)
- [_MSD87_R0_TABLE_SWITCH_POSITION_LOW_BYTE_BIT7](#table-msd87-r0-table-switch-position-low-byte-bit7) (2 × 2)
- [MOTORUDSCODIERUNG_RUHESTROM](#table-motorudscodierung-ruhestrom) (16 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 76 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUB_FUNCTION_NOT_SUPPORTED |
| 0x13 | ERROR_ECU_INCORRECT_MESSAGE_LENGTH_OR_INVALID_FORMAT |
| 0x14 | ERROR_ECU_RESPONSE_TOO_LONG |
| 0x21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT |
| 0x24 | ERROR_ECU_REQUEST_SEQUENCE_ERROR |
| 0x25 | ERROR_ECU_NO_RESPONSE_FROM_SUBNET_COMPONENT |
| 0x26 | ERROR_ECU_FAILURE_PREVENTS_EXECUTION_OF_REQUESTED_ACTION |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x33 | ERROR_ECU_SECURITY_ACCESS_DENIED |
| 0x35 | ERROR_ECU_INVALID_KEY |
| 0x36 | ERROR_ECU_EXCEED_NUMBER_OF_ATTEMPTS |
| 0x37 | ERROR_ECU_REQUIRED_TIME_DELAY_NOT_EXPIRED |
| 0x70 | ERROR_ECU_UPLOAD_DOWNLOAD_NOT_ACCEPTED |
| 0x71 | ERROR_ECU_TRANSFER_DATA_SUSPENDED |
| 0x72 | ERROR_ECU_GENERAL_PROGRAMMING_FAILURE |
| 0x73 | ERROR_ECU_WRONG_BLOCK_SEQUENCE_COUNTER |
| 0x78 | ERROR_ECU_REQUEST_CORRECTLY_RECEIVED__RESPONSE_PENDING |
| 0x7E | ERROR_ECU_SUB_FUNCTION_NOT_SUPPORTED_IN_ACTIVE_SESSION |
| 0x7F | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_SESSION |
| 0x81 | ERROR_ECU_RPM_TOO_HIGH |
| 0x82 | ERROR_ECU_RPM_TOO_LOW |
| 0x83 | ERROR_ECU_ENGINE_IS_RUNNING |
| 0x84 | ERROR_ECU_ENGINE_IS_NOT_RUNNING |
| 0x85 | ERROR_ECU_ENGINE_RUN_TIME_TOO_LOW |
| 0x86 | ERROR_ECU_TEMPERATURE_TOO_HIGH |
| 0x87 | ERROR_ECU_TEMPERATURE_TOO_LOW |
| 0x88 | ERROR_ECU_VEHICLE_SPEED_TOO_HIGH |
| 0x89 | ERROR_ECU_VEHICLE_SPEED_TOO_LOW |
| 0x8A | ERROR_ECU_THROTTLE_PEDAL_TOO_HIGH |
| 0x8B | ERROR_ECU_THROTTLE_PEDAL_TOO_LOW |
| 0x8C | ERROR_ECU_TRANSMISSION_RANGE_NOT_IN_NEUTRAL |
| 0x8D | ERROR_ECU_TRANSMISSION_RANGE_NOT_IN_GEAR |
| 0x8F | ERROR_ECU_BRAKE_SWITCH_NOT_CLOSED |
| 0x90 | ERROR_ECU_SHIFTER_LEVER_NOT_IN_PARK |
| 0x91 | ERROR_ECU_TORQUE_CONVERTER_CLUTCH_LOCKED |
| 0x92 | ERROR_ECU_VOLTAGE_TOO_HIGH |
| 0x93 | ERROR_ECU_VOLTAGE_TOO_LOW |
| ?00? | OKAY |
| ?01? | ERROR_ECU_NO_RESPONSE |
| ?02? | ERROR_ECU_INCORRECT_LEN |
| ?03? | ERROR_ECU_INCORRECT_RESPONSE_ID |
| ?04? | ERROR_ECU_TA_RESPONSE_NOT_SA_REQUEST |
| ?05? | ERROR_ECU_SA_RESPONSE_NOT_TA_REQUEST |
| ?06? | ERROR_ECU_RESPONSE_INCORRECT_DATA_IDENTIFIER |
| ?07? | ERROR_ECU_RESPONSE_TOO_MUCH_DATA |
| ?08? | ERROR_ECU_RESPONSE_TOO_LESS_DATA |
| ?09? | ERROR_ECU_RESPONSE_VALUE_OUT_OF_RANGE |
| ?0A? | ERROR_TABLE |
| ?10? | ERROR_F_CODE |
| ?12? | ERROR_INTERPRETATION |
| ?13? | ERROR_F_POS |
| ?14? | ERROR_ECU_RESPONSE_INCORRECT_IO_CONTROL_PARAMETER |
| ?15? | ERROR_ECU_RESPONSE_INCORRECT_ROUTINE_CONTROL_TYPE |
| ?16? | ERROR_ECU_RESPONSE_INCORRECT_SUB_FUNCTION |
| ?17? | ERROR_ECU_RESPONSE_INCORRECT_DYNAMICALLY_DEFINED_DATA_IDENTIFIER |
| ?18? | ERROR_ECU_RESPONSE_NO_STRING_END_CHAR |
| ?19? | ERROR_ECU_RESPONSE_INCORRECT_ROUTINE_IDENTIFIER |
| ?1A? | ERROR_ECU_RESPONSE_INCORRECT_RESET_TYPE |
| ?1B? | ERROR_ECU_RESPONSE_INCORRECT_SERIAL_NUMBER_FORMAT |
| ?1C? | ERROR_ECU_RESPONSE_INCORRECT_DTC_BY_STATUS_MASK |
| ?1D? | ERROR_ECU_RESPONSE_INCORRECT_DTC_STATUS_AVAILABILITY_MASK |
| ?1E? | ERROR_ECU_RESPONSE_INCORRECT_ROUTINE_CONTROL_IDENTIFIER |
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?60? | ERROR_VERIFY |
| ?61? | ERROR_ECU_RESPONSE_ZGW |
| ?62? | ERROR_ECU_RESPONSE_BACKUP |
| ?70? | ERROR_CALID_CVN_INCORRECT_LEN |
| ?80? | ERROR_SVK_INCORRECT_LEN |
| ?81? | ERROR_SVK_INCORRECT_FINGERPRINT |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 149 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x000001 | Reinshagen / Delphi |
| 0x000002 | Leopold Kostal GmbH & Co. KG |
| 0x000003 | Hella Fahrzeugkomponenten GmbH |
| 0x000004 | Siemens |
| 0x000005 | Eaton |
| 0x000006 | UTA |
| 0x000007 | Helbako GmbH |
| 0x000008 | Robert Bosch GmbH |
| 0x000009 | Lear Corporation |
| 0x000010 | VDO |
| 0x000011 | Valeo GmbH |
| 0x000012 | MBB |
| 0x000013 | Kammerer |
| 0x000014 | SWF |
| 0x000015 | Blaupunkt |
| 0x000016 | Philips |
| 0x000017 | Alpine Electronics GmbH |
| 0x000018 | Continental Teves AG & Co. OHG |
| 0x000019 | Elektromatik Südafrika |
| 0x000020 | Harman Becker Automotive Systems |
| 0x000021 | Preh GmbH |
| 0x000022 | Alps Electric Co. Ltd. |
| 0x000023 | Motorola |
| 0x000024 | Temic |
| 0x000025 | Webasto SE |
| 0x000026 | MotoMeter |
| 0x000027 | Delphi Automotive PLC |
| 0x000028 | DODUCO (Beru) |
| 0x000029 | DENSO |
| 0x000030 | NEC |
| 0x000031 | DASA |
| 0x000032 | Pioneer Corporation |
| 0x000033 | Jatco |
| 0x000034 | FUBA Automotive GmbH & Co. KG |
| 0x000035 | UK-NSI |
| 0x000036 | AABG |
| 0x000037 | Dunlop |
| 0x000038 | Sachs |
| 0x000039 | ITT |
| 0x000040 | FTE (Fahrzeugtechnik Ebern) |
| 0x000041 | Megamos |
| 0x000042 | TRW Automotive GmbH |
| 0x000043 | WABCO Fahrzeugsysteme GmbH |
| 0x000044 | ISAD Electronic Systems |
| 0x000045 | HEC Hella Electronics Corporation |
| 0x000046 | Gemel |
| 0x000047 | ZF Friedrichshafen AG |
| 0x000048 | GMPT |
| 0x000049 | Harman Becker Automotive Systems GmbH |
| 0x000050 | Remes GmbH |
| 0x000051 | ZF Lenksysteme GmbH |
| 0x000052 | Magneti Marelli S.p.A. |
| 0x000053 | Johnson Controls Inc. |
| 0x000054 | GETRAG Getriebe- und Zahnradf. Hermann Hagenmeyer GmbH & Co. KG |
| 0x000055 | Behr-Hella Thermocontrol GmbH |
| 0x000056 | Siemens VDO Automotive |
| 0x000057 | Visteon Innovation & Technology GmbH |
| 0x000058 | Autoliv AB |
| 0x000059 | Haberl Electronic GmbH & Co. KG |
| 0x000060 | Magna International Inc. |
| 0x000061 | Marquardt GmbH |
| 0x000062 | AB Elektronik GmbH |
| 0x000063 | SDVO/BORG |
| 0x000064 | Hirschmann Car Communication GmbH |
| 0x000065 | hoerbiger-electronics |
| 0x000066 | Thyssen Krupp Automotive |
| 0x000067 | Gentex Corporation |
| 0x000068 | Atena GmbH |
| 0x000069 | Magna-Donelly |
| 0x000070 | Koyo Steeting Europe |
| 0x000071 | NSI Beheer B.V. |
| 0x000072 | Aisin AW Co. Ltd. |
| 0x000073 | Schorlock |
| 0x000074 | Schrader Electronics Ltd. |
| 0x000075 | Huf-Electronics Bretten GmbH |
| 0x000076 | CEL |
| 0x000077 | AUDIO MOBIL Elektronik GmbH |
| 0x000078 | rd electronic |
| 0x000079 | iSYS RTS GmbH |
| 0x000080 | Westfalia-Automotive GmbH |
| 0x000081 | Tyco Electronics |
| 0x000082 | Paragon AG |
| 0x000083 | IEE S.A. |
| 0x000084 | TEMIC AUTOMOTIVE of NA |
| 0x000085 | Sonceboz S.A. |
| 0x000086 | Meta System S.p.A. |
| 0x000087 | Huf Hülsbeck & Fürst GmbH & Co. KG |
| 0x000088 | MANN+HUMMEL GmbH |
| 0x000089 | Brose Fahrzeugteile GmbH & Co. |
| 0x000090 | Keihin |
| 0x000091 | Vimercati S.p.a |
| 0x000092 | CRH |
| 0x000093 | TPO Display Corp |
| 0x000094 | Küster Automotive GmbH |
| 0x000095 | Hitachi Automotive |
| 0x000096 | Continental AG |
| 0x000097 | TI-Automotive |
| 0x000098 | Hydro |
| 0x000099 | Johnson Controls Inc. |
| 0x00009A | Takata-Petri |
| 0x00009B | Mitsubishi Electric B.V. (Melco) |
| 0x00009C | Autokabel |
| 0x00009D | GKN Plc |
| 0x00009E | Zollner Elektronik AG |
| 0x00009F | peiker acustic GmbH & Co. KG |
| 0x0000A0 | Bosal-Oris |
| 0x0000A1 | Cobasys |
| 0x0000A2 | Automotive Lighting Reutlingen GmbH |
| 0x0000A3 | CONTI VDO |
| 0x0000A4 | A.D.C. Automotive Distance Control Systems GmbH |
| 0x0000A5 | Novero Dabendorf GmbH |
| 0x0000A6 | LAMES S.p.a. |
| 0x0000A7 | Magna/Closures |
| 0x0000A8 | Harbin Wan Yu Technology Co |
| 0x0000A9 | ThyssenKrupp Presta AG |
| 0x0000AA | ArvinMeritor |
| 0x0000AB | Kongsberg Automotive GmbH |
| 0x0000AC | SMR Automotive Mirrors Stuttgart GmbH |
| 0x0000AD | So.Ge.Mi. |
| 0x0000AE | MTA S.p.A. |
| 0x0000AF | Alfmeier Präzision AG |
| 0x0000B0 | Eltek Deutechland GmbH |
| 0x0000B1 | OMRON Automotive Electronics Europe GmbH |
| 0x0000B2 | ASK Industries GmbH |
| 0x0000B3 | CML Innovative Technologies GmbH & Co. KG |
| 0x0000B4 | APAG Elektronik AG |
| 0x0000B5 | Nexteer Automotive |
| 0x0000B6 | Hans Widmaier Fernmelde- und Feinwerktechnik |
| 0x0000B7 | Robert Bosch Battery Systems GmbH |
| 0x0000B8 | Kyocera Display Europe GmbH |
| 0x0000B9 | Magna Powertrain AG & Co. KG |
| 0x0000BA | BorgWarner Beru Systems GmbH |
| 0x0000BB | BMW AG |
| 0x0000BC | Benteler Duncan Plant |
| 0x0000BD | U-Shin Deutschland Zugangssysteme GmbH |
| 0x0000BE | Schaeffler Technologies AG & Co. KG |
| 0x0000BF | JTEKT Corporation |
| 0x0000C0 | VLF |
| 0x0000C1 | Flextronics |
| 0x0000C2 | LG Chem |
| 0x0000C3 | Panasonic |
| 0x0000C4 | Alpitronic GmbH |
| 0x0000C5 | Telemotive AG |
| 0x0000C6 | Garmin |
| 0x0000C7 | RSG Elotech Elektronische Baugruppen GmbH |
| 0x0000C8 | KEBODA TECHNOLOGY CORP |
| 0x0000C9 | Aptiv |
| 0x0000CA | SEG Automotive Germany GmbH |
| 0xFFFFFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 35 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler momentan vorhanden und bereits gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler momentan vorhanden und bereits gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler momentan vorhanden und bereits gespeichert |
| 0x20 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x21 | Fehler momentan vorhanden und bereits gespeichert |
| 0x24 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x25 | Fehler momentan vorhanden und bereits gespeichert |
| 0x28 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x29 | Fehler momentan vorhanden und bereits gespeichert |
| 0x2C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x2D | Fehler momentan vorhanden und bereits gespeichert |
| 0x40 | unbekannte Fehlerart |
| 0x44 | Fehler gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler gespeichert |
| 0x4D | Fehler gespeichert |
| 0x60 | Fehler gespeichert |
| 0x61 | Fehler gespeichert |
| 0x64 | Fehler gespeichert |
| 0x65 | Fehler gespeichert |
| 0x68 | Fehler gespeichert |
| 0x69 | Fehler gespeichert |
| 0x6C | Fehler gespeichert |
| 0x6D | Fehler gespeichert |
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x80 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x81 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
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

<a id="table-prozessklassen"></a>
### PROZESSKLASSEN

Dimensions: 26 rows × 3 columns

| WERT | PROZESSKLASSE | BEZEICHNUNG |
| --- | --- | --- |
| 0x00 | - | ungueltig |
| 0x01 | HWEL | Hardware (Elektronik) |
| 0x02 | HWAP | Hardwareauspraegung |
| 0x03 | HWFR | Hardwarefarbe |
| 0x05 | CAFD | Codierdaten |
| 0x06 | BTLD | Bootloader |
| 0x08 | SWFL | Software ECU Speicherimage |
| 0x09 | SWFF | Flash File Software |
| 0x0A | SWPF | Pruefsoftware |
| 0x0B | ONPS | Onboard Programmiersystem |
| 0x0F | FAFP | FA2FP |
| 0x1A | TLRT | Temporaere Loeschroutine |
| 0x1B | TPRG | Temporaere Programmierroutine |
| 0x07 | FLSL | Flashloader Slave |
| 0x0C | IBAD | Interaktive Betriebsanleitung Daten |
| 0x10 | FCFA | Freischaltcode Fahrzeug-Auftrag |
| 0x1C | BLUP | Bootloader-Update Applikation |
| 0x1D | FLUP | Flashloader-Update Applikation |
| 0xC0 | SWUP | Software-Update Package |
| 0xC1 | SWIP | Index Software-Update Package |
| 0xA0 | ENTD | Entertainment Daten |
| 0xA1 | NAVD | Navigation Daten |
| 0xA2 | FCFN | Freischaltcode Funktion |
| 0x04 | GWTB | Gateway-Tabelle |
| 0x0D | SWFK | BEGU: Detaillierung auf SWE-Ebene |
| 0xFF | - | ungueltig |

<a id="table-svk-id"></a>
### SVK_ID

Dimensions: 65 rows × 2 columns

| WERT | BEZEICHNUNG |
| --- | --- |
| 0x01 | SVK_AKTUELL |
| 0x02 | SVK_SUPPLIER |
| 0x03 | SVK_WERK |
| 0x04 | SVK_BACKUP_01 |
| 0x05 | SVK_BACKUP_02 |
| 0x06 | SVK_BACKUP_03 |
| 0x07 | SVK_BACKUP_04 |
| 0x08 | SVK_BACKUP_05 |
| 0x09 | SVK_BACKUP_06 |
| 0x0A | SVK_BACKUP_07 |
| 0x0B | SVK_BACKUP_08 |
| 0x0C | SVK_BACKUP_09 |
| 0x0D | SVK_BACKUP_10 |
| 0x0E | SVK_BACKUP_11 |
| 0x0F | SVK_BACKUP_12 |
| 0x10 | SVK_BACKUP_13 |
| 0x11 | SVK_BACKUP_14 |
| 0x12 | SVK_BACKUP_15 |
| 0x13 | SVK_BACKUP_16 |
| 0x14 | SVK_BACKUP_17 |
| 0x15 | SVK_BACKUP_18 |
| 0x16 | SVK_BACKUP_19 |
| 0x17 | SVK_BACKUP_20 |
| 0x18 | SVK_BACKUP_21 |
| 0x19 | SVK_BACKUP_22 |
| 0x1A | SVK_BACKUP_23 |
| 0x1B | SVK_BACKUP_24 |
| 0x1C | SVK_BACKUP_25 |
| 0x1D | SVK_BACKUP_26 |
| 0x1E | SVK_BACKUP_27 |
| 0x1F | SVK_BACKUP_28 |
| 0x20 | SVK_BACKUP_29 |
| 0x21 | SVK_BACKUP_30 |
| 0x22 | SVK_BACKUP_31 |
| 0x23 | SVK_BACKUP_32 |
| 0x24 | SVK_BACKUP_33 |
| 0x25 | SVK_BACKUP_34 |
| 0x26 | SVK_BACKUP_35 |
| 0x27 | SVK_BACKUP_36 |
| 0x28 | SVK_BACKUP_37 |
| 0x29 | SVK_BACKUP_38 |
| 0x2A | SVK_BACKUP_39 |
| 0x2B | SVK_BACKUP_40 |
| 0x2C | SVK_BACKUP_41 |
| 0x2D | SVK_BACKUP_42 |
| 0x2E | SVK_BACKUP_43 |
| 0x2F | SVK_BACKUP_44 |
| 0x30 | SVK_BACKUP_45 |
| 0x31 | SVK_BACKUP_46 |
| 0x32 | SVK_BACKUP_47 |
| 0x33 | SVK_BACKUP_48 |
| 0x34 | SVK_BACKUP_49 |
| 0x35 | SVK_BACKUP_50 |
| 0x36 | SVK_BACKUP_51 |
| 0x37 | SVK_BACKUP_52 |
| 0x38 | SVK_BACKUP_53 |
| 0x39 | SVK_BACKUP_54 |
| 0x3A | SVK_BACKUP_55 |
| 0x3B | SVK_BACKUP_56 |
| 0x3C | SVK_BACKUP_57 |
| 0x3D | SVK_BACKUP_58 |
| 0x3E | SVK_BACKUP_59 |
| 0x3F | SVK_BACKUP_60 |
| 0x40 | SVK_BACKUP_61 |
| 0xXY | ERROR_UNKNOWN |

<a id="table-dtcextendeddatarecordnumber"></a>
### DTCEXTENDEDDATARECORDNUMBER

Dimensions: 5 rows × 3 columns

| WERT | TEXT | ANZ_BYTE |
| --- | --- | --- |
| 0x00 | ISO_RESERVED | 0 |
| 0x01 | CONDITION_BYTE | 1 |
| 0x02 | HFK | 1 |
| 0x03 | HLZ | 1 |
| 0xFF | RECORD_UNKNOWN | 0 |

<a id="table-dtcsnapshotidentifier"></a>
### DTCSNAPSHOTIDENTIFIER

Dimensions: 7 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | KM_STAND | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1701 | ABS_ZEIT | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1702 | SAE_CODE | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1731 | Fehlerklasse_DTC | - | - | u char | - | 1 | 1 | 0.000000 |
| 0x1750 | PWF_Basinetz | 0-n | - | 0xFF | - | 1 | 1 | 0.000000 |
| 0x1751 | PWF_Teilnetz | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0xFFFF | IDENTIFIER_UNKNOWN | - | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |

<a id="table-fehlerklasse"></a>
### FEHLERKLASSE

Dimensions: 5 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x00 | Keine Fehlerklasse verfuegbar |
| 0x01 | Ueberpruefung bei naechstem Werkstattbesuch |
| 0x02 | Ueberpruefung bei naechstem Halt |
| 0x04 | Ueberpruefung sofort erforderlich ! |
| 0xFF | unbekannte Fehlerklasse |

<a id="table-diagmode"></a>
### DIAGMODE

Dimensions: 14 rows × 3 columns

| NR | MODE | MODE_TEXT |
| --- | --- | --- |
| 0x00 | UNGUELTIG | DefaultMode |
| 0x01 | DEFAULT | DefaultMode |
| 0x02 | ECUPM | ECUProgrammingMode |
| 0x03 | ECUEXTDIAG | ECUExtendedDiagnosticSession |
| 0x04 | ECUSSDS | ECUSafetySystemDiagnosticSession |
| 0x40 | ECUEOL | ECUEndOfLineSession |
| 0x41 | ECUCODE | ECUCodingSession |
| 0x42 | ECUSWT | ECUSwtSession |
| 0x43 | ECUHDD | ECUHDDDownloadSession |
| 0x44 | ECURSU | ECURsuSession |
| 0x4F | ECUDEVELOP | ECUDevelopmentSession |
| 0x5F | ECUGDM | ECUGarageDiagnoseMode |
| 0x61 | ECUSUPSPEC | ECUSupplierSpecificSession |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 365 rows × 3 columns

| ORT | ORTTEXT | LIN_2_FORMAT |
| --- | --- | --- |
| 0x0100 | Batteriesensor BSD | - |
| 0x0150 | Ölqualitätsensor BSD | - |
| 0x0200 | Elektrische Wasserpumpe BSD | - |
| 0x0250 | Elektrische Kraftstoffpumpe BSD | - |
| 0x0300 | Generator 1 | - |
| 0x0350 | Generator 2 | - |
| 0x03A0 | Druck- Temperatursensor Tank | 1 |
| 0x03C0 | EAC-Sensor | - |
| 0x0400 | Schaltzentrum Lenksäule | - |
| 0x0500 | DSC Sensor-Cluster | - |
| 0x0600 | Nahbereichsradarsensor links | - |
| 0x0700 | Nahbereichsradarsensor rechts | - |
| 0x0800 | Funkempfänger | - |
| 0x0900 | Elektrische Lenksäulenverriegelung | - |
| 0x0A00 | Regen- Lichtsensor | - |
| 0x290A00 | DSC Hydraulikblock | - |
| 0x0B00 | Nightvision Kamera | - |
| 0x0C00 | TLC Kamera | - |
| 0x0D00 | Spurwechselradarsensor hinten links | - |
| 0x0E00 | Heckklima Bedienteil rechts | 1 |
| 0x0F00 | Rearview Kamera hinten | 1 |
| 0x0F80 | Frontview Kamera vorne | 1 |
| 0x1000 | Topview Kamera Außenspiegel links | 1 |
| 0x1100 | Topview Kamera Außenspiegel rechts | 1 |
| 0x1200 | Sideview Kamera Stoßfänger vorne links | 1 |
| 0x1210 | Sideview Kamera Kotflügel vorne links | 1 |
| 0x1300 | Sideview Kamera Stoßfänger vorne rechts | 1 |
| 0x1310 | Sideview Kamera Kotflügel vorne rechts | 1 |
| 0x1400 | Wischermotor | 1 |
| 0x1500 | Regen- Lichtsensor | 1 |
| 0x1600 | Innenspiegel | 1 |
| 0x1700 | Garagentoröffner | 1 |
| 0x1800 | AUC-Sensor | 1 |
| 0x1900 | Druck- Temperatursensor | 1 |
| 0x1A20 | Schalterblock Sitzheizung hinten links | 1 |
| 0x1A40 | Schalterblock Sitzheizung hinten rechts | 1 |
| 0x1A60 | Sitzheizung Fahrer | 1 |
| 0x1A80 | Sitzheizung Beifahrer | 1 |
| 0x1AA0 | Sitzheizung Fahrer hinten | 1 |
| 0x1AC0 | Sitzheizung Beifahrer hinten | 1 |
| 0x1B00 | Schalterblock Sitzmemory/-massage Fahrer | 1 |
| 0x1C00 | Schalterblock Sitzmemory/-massage Beifahrer | 1 |
| 0x1C80 | Sitzverstellschalter Beifahrer über Fond | 1 |
| 0x1D00 | Sonnenrollo Seitenfenster Fahrer | 1 |
| 0x1E00 | Sonnenrollo Seitenfenster Beifahrer | 1 |
| 0x1E40 | Heckklappenemblem | 1 |
| 0x1F00 | KAFAS Kamera | 1 |
| 0x2000 | Automatische Anhängevorrichtung | 1 |
| 0x2100 | SINE | 1 |
| 0x2110 | DWA Mikrowellensensor vorne rechts | 1 |
| 0x2120 | DWA Mikrowellensensor hinten rechts | 1 |
| 0x2130 | DWA Mikrowellensensor hinten links | 1 |
| 0x2140 | DWA Mikrowellensensor vorne links | 1 |
| 0x2150 | DWA Mikrowellensensor hinten | 1 |
| 0x2180 | DWA Ultraschallsensor | 1 |
| 0x2200 | Aussenspiegel Fahrer | - |
| 0x2210 | Aussenspiegel Fahrer | 1 |
| 0x2300 | Aussenspiegel Beifahrer | - |
| 0x2310 | Aussenspiegel Beifahrer | 1 |
| 0x2400 | Schaltzentrum Tür | 1 |
| 0x2500 | Schalterblock Sitz Fahrer | 1 |
| 0x2600 | Schalterblock Sitz Beifahrer | 1 |
| 0x2700 | Gurtbringer Fahrer | 1 |
| 0x2800 | Gurtbringer Beifahrer | 1 |
| 0x2900 | Treibermodul Scheinwerfer links | 1 |
| 0x2A00 | Treibermodul Scheinwerfer rechts | 1 |
| 0x2B00 | Bedieneinheit Fahrerassistenzsysteme | 1 |
| 0x2C00 | Bedieneinheit Licht | 1 |
| 0x2D00 | Smart Opener | 1 |
| 0x2E00 | LED-Hauptlicht-Modul links | 1 |
| 0x2F00 | LED-Hauptlicht-Modul rechts | 1 |
| 0x0910 | Elektrische Lenksäulenverriegelung | 1 |
| 0x3200 | Funkempfänger | 1 |
| 0x3300 | Funkempfänger 2 | 1 |
| 0x3400 | Türgriffelektronik Fahrer | - |
| 0x3500 | Türgriffelektronik Beifahrer | - |
| 0x3600 | Türgriffelektronik Fahrer hinten | - |
| 0x3700 | Türgriffelektronik Beifahrer hinten | - |
| 0x3800 | Telestart-Handsender 1 | - |
| 0x3900 | Telestart-Handsender 2 | - |
| 0x3A00 | Fond-Fernbedienung | - |
| 0x3B00 | Elektrische Wasserpumpe | 1 |
| 0x3B10 | Elektrische Wasserpumpe 1 | 1 |
| 0x3B20 | Elektrische Wasserpumpe 2 | 1 |
| 0x3B30 | Elektrische Wasserpumpe 22 | 1 |
| 0x3B40 | Elektrische Wasserpumpe 23 | 1 |
| 0x3B80 | Elektrische Zusatzwasserpumpe | 1 |
| 0x3C00 | Batteriesensor LIN | - |
| 0x3D00 | Aktives Kühlklappensystem | 1 |
| 0x3D10 | Aktiver Kühlluftklappensteller oberer Kühllufteinlass | 1 |
| 0x3D20 | Aktiver Kühlluftklappensteller unterer Kühllufteinlass | 1 |
| 0x3D80 | Lüfter | 1 |
| 0x3D88 | Lüfter 2 | 1 |
| 0x3E00 | PCU(DCDC) | 1 |
| 0x3E80 | DCDC Versorgung Zustartbatterie | 1 |
| 0x3F00 | Startergenerator | 1 |
| 0x3F80 | Generator | 1 |
| 0x4000 | Sitzverstellschalter Fahrer | 1 |
| 0x4100 | Sitzverstellschalter Beifahrer | 1 |
| 0x4200 | Sitzverstellschalter Fahrer hinten | 1 |
| 0x4300 | Sitzverstellschalter Beifahrer hinten | 1 |
| 0x4400 | Gepäckraumschalter links | 1 |
| 0x4500 | Gepäckraumschalter rechts | 1 |
| 0x4600 | Nackenwärmer | 1 |
| 0x4610 | Nackenwärmer Fahrer | 1 |
| 0x4620 | Nackenwärmer Beifahrer | 1 |
| 0x4700 | Nackenwärmer Bedienschalter | 1 |
| 0x4A00 | Fond-Klimaanlage | 1 |
| 0x4B00 | Elektrischer Klimakompressor | 1 |
| 0x4C00 | Klimabedienteil | 1 |
| 0x4C80 | Klimabedienteil 3. Sitzreihe | 1 |
| 0x4D00 | Gebläseregler | 1 |
| 0x4E00 | Klappenmotor | 0 |
| 0x4F00 | Elektrischer Kältemittelverdichter eKMV | 1 |
| 0x4F80 | Elektrischer Zuheizer PTC | 1 |
| 0x4FC0 | Elektrischer Zuheizer 3. Sitzreihe | 1 |
| 0x6000 | Standheizung | 1 |
| 0x6100 | Wärmepumpe | 1 |
| 0x6180 | LIN-Zusatzwasserpumpe | 1 |
| 0x6200 | elektrischer Durchlaufheizer | 1 |
| 0x6300 | Ionisator | 1 |
| 0x6400 | Bedufter | 1 |
| 0x6500 | Sense-Touch-Modul links | 1 |
| 0x6600 | Sense-Touch-Modul rechts | 1 |
| 0x6700 | Hochdruck- Temperatursensor 1 | 1 |
| 0x6710 | Niederdruck- Temperatursensor 1 | 1 |
| 0x6720 | Elektrisches Expansionsventil | 1 |
| 0x5000 | PMA Sensor links | 1 |
| 0x5100 | PMA Sensor rechts | 1 |
| 0x5200 | CID-Klappe | - |
| 0x5300 | Schaltzentrum Lenksäule | 1 |
| 0x5400 | Multifunktionslenkrad | 1 |
| 0x5500 | Lenkradelektronik | 1 |
| 0x5600 | CID | - |
| 0x5700 | Satellit Upfront links | 0 |
| 0x5708 | Satellit Upfront rechts | 0 |
| 0x570C | Satellit Upfront mitte | 0 |
| 0x5710 | Satellit Tür links | 0 |
| 0x5718 | Satellit Tür rechts | 0 |
| 0x5720 | Satellit B-Säule links X | 0 |
| 0x5728 | Satellit B-Säule rechts X | 0 |
| 0x5730 | Satellit B-Säule links Y | 0 |
| 0x5738 | Satellit B-Säule rechts Y | 0 |
| 0x5740 | Satellit Zentralsensor X | 0 |
| 0x5748 | Satellit Zentralsensor Y | 0 |
| 0x5750 | Satellit Zentralsensor Low g Y | 0 |
| 0x5758 | Satellit Zentralsensor Low g Z | 0 |
| 0x5760 | Satellit Zentralsensor Roll Achse | 0 |
| 0x5768 | Fussgängerschutz Sensor vorne links | 0 |
| 0x5770 | Fussgängerschutz Sensor vorne rechts | 0 |
| 0x5778 | Fussgängerschutz Sensor vorne mitte | 0 |
| 0x5780 | Fussgängerschutzsensor statisch | 0 |
| 0x5782 | Fussgängerschutz Zusatzsensor Beschleunigung links | 0 |
| 0x5784 | Fussgängerschutz Zusatzsensor Beschleunigung rechts | 0 |
| 0x5788 | Satellit C-Säule links Y | 0 |
| 0x5790 | Satellit C-Säule rechts Y | 0 |
| 0x5798 | Satellit Zentrale Körperschall | 0 |
| 0x57A0 | Kapazitive Insassen- Sensorik CIS | 1 |
| 0x57A8 | Sitzbelegungserkennung Beifahrer SBR | 1 |
| 0x57B0 | Fussgängerschutzsensor dynamisch 1 | 0 |
| 0x57B8 | Fussgängerschutzsensor dynamisch 2 | 0 |
| 0x57C0 | Satellit Drucksensor Schlauch PTS 1 vorne links p | 0 |
| 0x57C4 | Satellit Drucksensor Schlauch PTS 1 vorne rechts p | 0 |
| 0x57C8 | Satellit Drucksensor Schlauch PTS 2 vorne links p | 0 |
| 0x57CC | Satellit Drucksensor Schlauch PTS 2 vorne rechts p | 0 |
| 0x57D0 | Beschleunigungssensor vorne links X | 0 |
| 0x57D4 | Beschleunigungssensor vorne mitte X | 0 |
| 0x57D8 | Beschleunigungssensor vorne rechts X | 0 |
| 0x57DC | Beschleunigungssensor hinten mitte X | 0 |
| 0x57E0 | Sitzbelegungserkennung Beifahrer CIS/Bladder | 1 |
| 0x57E4 | Sitzbelegungserkennung 2. Sitzreihe links CIS/Bladder | 1 |
| 0x57E8 | Sitzbelegungserkennung 2. Sitzreihe rechts CIS/Bladder | 1 |
| 0x5800 | HUD | 1 |
| 0x5900 | Audio-Bedienteil | 1 |
| 0x5A00 | Innenlichtelektronik | 1 |
| 0x5A01 | Innenbeleuchtung - Lichtschwert links | 1 |
| 0x5A02 | Innenbeleuchtung - Lichtschwert rechts | 1 |
| 0x5A03 | Innenbeleuchtung - Lautsprecher Hutablage rechts | 1 |
| 0x5A04 | Innenbeleuchtung - Lautsprecher Hutablage links | 1 |
| 0x5A05 | Innenbeleuchtung - Lautsprecher hinten links | 1 |
| 0x5A06 | Innenbeleuchtung - Lautsprecher Mitteltöner vorne links | 1 |
| 0x5A07 | Innenbeleuchtung - Lautsprecher Hochtöner vorne links | 1 |
| 0x5A08 | Innenbeleuchtung - Lautsprecher hinten rechts | 1 |
| 0x5A09 | Innenbeleuchtung - Lautsprecher Mitteltöner vorne rechts | 1 |
| 0x5A0A | Innenbeleuchtung - Lautsprecher Hochtöner vorne rechts | 1 |
| 0x5A0B | Innenbeleuchtung - Lautsprecher Centerspeaker | 1 |
| 0x5A0C | Innenbeleuchtung - Panoramadach LED Modul 1 (hinteres Glasfestelement) | 1 |
| 0x5A0D | Innenbeleuchtung - Panoramadach LED Modul 2 (hinteres Glasfestelement) | 1 |
| 0x5A0E | Innenbeleuchtung - Panoramadach LED Modul 3 (hinteres Glasfestelement) | 1 |
| 0x5A0F | Innenbeleuchtung - Panoramadach LED Modul 4 (hinteres Glasfestelement) | 1 |
| 0x5A10 | Innenbeleuchtung - Panoramadach LED Modul 5 (vorderes Glasschiebedach) | 1 |
| 0x5A11 | Innenbeleuchtung - Panoramadach LED Modul 6 (vorderes Glasschiebedach) | 1 |
| 0x5A12 | Innenbeleuchtung - Panoramadach LED Modul 7 (vorderes Glasschiebedach) | 1 |
| 0x5A13 | Innenbeleuchtung - Panoramadach LED Modul 8 (vorderes Glasschiebedach) | 1 |
| 0x5A14 | Touch Command Snap-In Adapter - Mittelkonsole Fond | 1 |
| 0x5A20 | Innenlichteinheit 2 | 1 |
| 0x5A30 | Innenlichteinheit 3 | 1 |
| 0x5A40 | Innenlichteinheit 4 | 1 |
| 0x5A50 | Innenlichteinheit 5 | 1 |
| 0x5AFF | unbekannter Verbauort | - |
| 0x5B00 | Zentralinstrument | 1 |
| 0x5B40 | CID | 1 |
| 0x5B80 | Fondmonitor links | 1 |
| 0x5BC0 | Fondmonitor rechts | 1 |
| 0x5B60 | Fondcontroller | 1 |
| 0x5B50 | AR (augmented reality) Kamera | 1 |
| 0x5C00 | Elektrische Lenksäulenverstellung ELSV | 1 |
| 0x5D00 | Hands-Off Detection HOD | 1 |
| 0x5E01 | Innenbeleuchtung Fußraum Fahrer vorne | 1 |
| 0x5E02 | Innenbeleuchtung Fußraum Fahrer hinten | 1 |
| 0x5E03 | Innenbeleuchtung Fußraum Beifahrer vorne | 1 |
| 0x5E04 | Innenbeleuchtung Fußraum Beifahrer hinten | 1 |
| 0x5E05 | Innenbeleuchtung Konturlinie Fahrertür vorne | 1 |
| 0x5E06 | Innenbeleuchtung Dekor indirekt Fahrertür vorne | 1 |
| 0x5E07 | Innenbeleuchtung Türöffner Fahrertür vorne | 1 |
| 0x5E08 | Innenbeleuchtung Fahrertür vorne Kartentasche | 1 |
| 0x5E09 | Innenbeleuchtung Konturlinie Fahrertür hinten | 1 |
| 0x5E0A | Innenbeleuchtung Dekor indirekt Fahrertür hinten | 1 |
| 0x5E0B | Innenbeleuchtung Fahrertür hinten Kartentasche | 1 |
| 0x5E0C | Innenbeleuchtung Konturlinie Beifahrertür vorne | 1 |
| 0x5E0D | Innenbeleuchtung Dekor indirekt Beifahrertür vorne | 1 |
| 0x5E0E | Innenbeleuchtung Türöffner Beifahrertür vorne | 1 |
| 0x5E0F | Innenbeleuchtung Beifahrertür vorne Kartentasche | 1 |
| 0x5E10 | Innenbeleuchtung Konturlinie Beifahrertür hinten | 1 |
| 0x5E11 | Innenbeleuchtung Dekor indirekt Beifahrertür hinten | 1 |
| 0x5E12 | Innenbeleuchtung Beifahrertür hinten Kartentasche | 1 |
| 0x5E13 | Innenbeleuchtung Konturlinie I-Tafel Fahrer | 1 |
| 0x5E14 | Innenbeleuchtung Dekor indirekt I-Tafel Fahrer | 1 |
| 0x5E15 | Innenbeleuchtung Konturlinie I-Tafel Mitte | 1 |
| 0x5E16 | Innenbeleuchtung Dekor indirekt I-Tafel Mitte | 1 |
| 0x5E17 | Innenbeleuchtung Konturlinie I-Tafel Beifahrer | 1 |
| 0x5E18 | Innenbeleuchtung Dekor indirekt I-Tafel Beifahrer | 1 |
| 0x5E19 | Innenbeleuchtung B-Säule Fahrer | 1 |
| 0x5E1A | Innenbeleuchtung B-Säule Beifahrer | 1 |
| 0x5E1B | Innenbeleuchtung Lehne Fahrersitz | 1 |
| 0x5E1C | Innenbeleuchtung Lehne Beifahrersitz | 1 |
| 0x5E1D | Innenbeleuchtung Centerstack Ablagefach | 1 |
| 0x5E1E | Innenbeleuchtung Mittelkonsole Ablagefach | 1 |
| 0x5E1F | Innenbeleuchtung Gangwahlschalter links | 1 |
| 0x5E20 | Innenbeleuchtung Gangwahlschalter rechts | 1 |
| 0x5E21 | Innenbeleuchtung Türöffner Fahrertür hinten | 1 |
| 0x5E22 | Innenbeleuchtung Türöffner Beifahrertür hinten | 1 |
| 0x5E23 | Innenbeleuchtung Fußraum Fahrer 3SR | 1 |
| 0x5E24 | Innenbeleuchtung Fußraum Beifahrer 3SR | 1 |
| 0x5E25 | Innenbeleuchtung Kartentasche Fahrertür 3SR | 1 |
| 0x5E26 | Innenbeleuchtung Kartentasche Beifahrertür 3SR | 1 |
| 0x5E27 | Innenbeleuchtung Konturlinie Fahrertür 3SR | 1 |
| 0x5E28 | Innenbeleuchtung Konturlinie Beifahrertür 3SR | 1 |
| 0x5E29 | Innenbeleuchtung Dekor indirekt Fahrertür 3SR | 1 |
| 0x5E2A | Innenbeleuchtung Dekor indirekt Beifahrertür 3SR | 1 |
| 0x5E2B | Innenbeleuchtung Konturlinie Mittelkonsole Fahrer vorne | 1 |
| 0x5E2C | Innenbeleuchtung Konturlinie Mittelkonsole Fahrer hinten | 1 |
| 0x5E2D | Innenbeleuchtung Konturlinie Mittelkonsole Beifahrer vorne | 1 |
| 0x5E2E | Innenbeleuchtung Konturlinie Mittelkonsole Beifahrer hinten | 1 |
| 0x5E2F | Innenbeleuchtung Dekor indirekt Mittelkonsole Fahrer vorne | 1 |
| 0x5E30 | Innenbeleuchtung Dekor indirekt Mittelkonsole Fahrer hinten | 1 |
| 0x5E31 | Innenbeleuchtung Dekor indirekt Mittelkonsole Beifahrer vorne | 1 |
| 0x5E32 | Innenbeleuchtung Dekor indirekt Mittelkonsole Beifahrer hinten | 1 |
| 0x5E33 | Innenbeleuchtung Backpanel Fahrersitz 2SR | 1 |
| 0x5E34 | Innenbeleuchtung Backpanel Beifahrersitz 2SR | 1 |
| 0x5E35 | Innenbeleuchtung Panoramadach Glasdeckel Front links vorne | 1 |
| 0x5E36 | Innenbeleuchtung Panoramadach Glasdeckel Front links hinten | 1 |
| 0x5E37 | Innenbeleuchtung Panoramadach Glasdeckel Front rechts vorne | 1 |
| 0x5E38 | Innenbeleuchtung Panoramadach Glasdeckel Front rechts hinten | 1 |
| 0x5E39 | Innenbeleuchtung Panoramadach Glasdeckel Fond links vorne | 1 |
| 0x5E3A | Innenbeleuchtung Panoramadach Glasdeckel Fond links hinten | 1 |
| 0x5E3B | Innenbeleuchtung Panoramadach Glasdeckel Fond rechts vorne | 1 |
| 0x5E3C | Innenbeleuchtung Panoramadach Glasdeckel Fond rechts hinten | 1 |
| 0x5E3D | Innenbeleuchtung Lichtschwert links | 1 |
| 0x5E3E | Innenbeleuchtung Lichtschwert rechts | 1 |
| 0x5E3F | Innenbeleuchtung Dekor hinterleuchtet Fahrertür vorne vorne | 1 |
| 0x5E40 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür vorne hinten | 1 |
| 0x5E41 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür hinten vorne | 1 |
| 0x5E42 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür hinten hinten | 1 |
| 0x5E43 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür vorne vorne | 1 |
| 0x5E44 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür vorne hinten | 1 |
| 0x5E45 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür hinten vorne | 1 |
| 0x5E46 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür hinten hinten | 1 |
| 0x5E47 | Innenbeleuchtung Dekor hinterleuchtet Mittelkonsole Fahrer vorne | 1 |
| 0x5E48 | Innenbeleuchtung Dekor hinterleuchtet Mittelkonsole Fahrer hinten | 1 |
| 0x5E49 | Innenbeleuchtung Dekor hinterleuchtet Mittelkonsole Beifahrer vorne | 1 |
| 0x5E4A | Innenbeleuchtung Dekor hinterleuchtet Mittelkonsole Beifahrer hinten | 1 |
| 0x5E4B | Innenbeleuchtung Cupholder vorne | 1 |
| 0x5E4C | Innenbeleuchtung Cupholder hinten | 1 |
| 0x5E4D | Innenbeleuchtung Kartentasche Fahrertür hinten 2 | 1 |
| 0x5E4E | Innenbeleuchtung Kartentasche Beifahrertür hinten 2 | 1 |
| 0x5E4F | Innenbeleuchtung Dekor hinterleuchtet I-Tafel Beifahrer oben | 1 |
| 0x5E50 | Innenbeleuchtung Dekor hinterleuchtet I-Tafel Beifahrer unten | 1 |
| 0x5E51 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür vorne oben | 1 |
| 0x5E52 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür vorne unten | 1 |
| 0x5E53 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür hinten oben | 1 |
| 0x5E54 | Innenbeleuchtung Dekor hinterleuchtet Fahrertür hinten unten | 1 |
| 0x5E55 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür vorne oben | 1 |
| 0x5E56 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür vorne unten | 1 |
| 0x5E57 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür hinten oben | 1 |
| 0x5E58 | Innenbeleuchtung Dekor hinterleuchtet Beifahrertür hinten unten | 1 |
| 0x5E59 | Innenbeleuchtung Hochtöner Fahrertür vorne | 1 |
| 0x5E5A | Innenbeleuchtung Hochtöner Beifahrertür vorne | 1 |
| 0x5E5B | Innenbeleuchtung Mitteltöner Fahrertür vorne | 1 |
| 0x5E5C | Innenbeleuchtung Mitteltöner Beifahrertür vorne | 1 |
| 0x5E5D | Innenbeleuchtung Mitteltöner Fahrertür hinten | 1 |
| 0x5E5E | Innenbeleuchtung Mitteltöner Beifahrertür hinten | 1 |
| 0x5E5F | Innenbeleuchtung Centerspeaker | 1 |
| 0x5E60 | Innenbeleuchtung Fireplace Mittelkonsole vorne | 1 |
| 0x5E61 | Innenbeleuchtung Fireplace Mittelkonsole hinten | 1 |
| 0x5E80 | Stromverteiler hinten | 1 |
| 0x5E90 | Stromverteiler vorne | 1 |
| 0x5EA0 | Wireless Charging Ablage | - |
| 0x5EC0 | Thermocupholder | 1 |
| 0x5F00 | Integrierte Fensterheber Elektronik Fahrer | 1 |
| 0x5F10 | Integrierte Fensterheber Elektronik Beifahrer | 1 |
| 0x5F20 | Integrierte Fensterheber Elektronik Fahrer hinten | 1 |
| 0x5F30 | Integrierte Fensterheber Elektronik Beifahrer hinten | 1 |
| 0x5F40 | Schalterblock Sitzmemory Fahrer | 1 |
| 0x5F50 | Schalterblock Sitzmemory Beifahrer | 1 |
| 0x5F60 | Schalterblock Sitzmemory Fahrer hinten | 1 |
| 0x5F70 | Schalterblock Sitzmemory Beifahrer hinten | 1 |
| 0x5F80 | Sonnenrollo Seitenfenster Fahrer | 1 |
| 0x5F90 | Sonnenrollo Seitenfenster Beifahrer | 1 |
| 0x5FA0 | Bedieneinheit Mittelkonsole | 1 |
| 0x5FB0 | WB und SARAH Schalter | 1 |
| 0x5FC0 | ABW-Türschloss Fahrer | 1 |
| 0x5FD0 | ABW-Türschloss Beifahrer | 1 |
| 0x7000 | Abschattungs-Elektronik-Dach | 1 |
| 0x7040 | Frontwischermotor | 1 |
| 0x7100 | NFC Leser Innenraum vorne | 1 |
| 0x7108 | NFC Leser Türgriff Fahrer | 1 |
| 0x7200 | Spurwechselradarsensor vorne rechts | 1 |
| 0x7208 | Spurwechselradarsensor vorne links | 1 |
| 0x7210 | Spurwechselradarsensor hinten rechts (Master) | 1 |
| 0x7218 | Spurwechselradarsensor hinten links | 1 |
| 0x7300 | Tanksensor links | 1 |
| 0x7310 | Tanksensor rechts | 1 |
| 0x7400 | Cargo Steuergeraet | 1 |
| 0x7500 | CID-Klappe | 1 |
| 0x7600 | Handschuhkasten | 1 |
| 0x7620 | Sternenhimmel Steuergerät | 1 |
| 0x7640 | Partition Wall Steuergerät | 1 |
| 0x7680 | Durchreiche Partition Wall | 1 |
| 0x76A0 | Bedienelement Dach | 1 |
| 0x7700 | Booster | 1 |
| 0x7800 | Dualspeicher | 1 |
| 0x7900 | Tablet | - |
| 0x7A00 | Beschleunigungssensor vorne links | 1 |
| 0x7A08 | Beschleunigungssensor vorne rechts | 1 |
| 0x7A10 | Beschleunigungssensor hinten links | 1 |
| 0x7A18 | Beschleunigungssensor hinten rechts | 1 |
| 0x7A20 | Abdeckrollo-Steuergerät | 1 |
| 0x7A28 | Schalterblock Gepäckraum | 1 |
| 0x7A30 | Unteres Heckklappenschloss links | 1 |
| 0x7A38 | Unteres Heckklappenschloss rechts | 1 |
| 0x7A40 | Elektrische Getriebeoelpumpe | 1 |
| 0x7B00 | ISC - Inertial Sensor Cluster | 1 |
| 0x7C00 | elektrischer Durchlaufheizer Hochvoltspeicher | 1 |
| 0xF000 | Motorrad Tachometer | 1 |
| 0xF010 | Motorrad Drehzahlmesser | 1 |
| 0xF020 | Motorrad Leistungsanzeige | 1 |
| 0xF030 | Motorrad Tankanzeige | 1 |
| 0xF040 | Motorrad 5Wege-Kombischalter links | 1 |
| 0xF050 | Motorrad Kombischalter rechts | 1 |
| 0xF060 | Motorrad Favoritentasterblock | 1 |
| 0xF070 | Motorrad Scheinwerfer | 1 |
| 0xF080 | Motorrad Radiobedienteil | 1 |
| 0xF090 | Motorrad Kombischalter links | 1 |
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-lieferantenlin"></a>
### LIEFERANTENLIN

Dimensions: 225 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x0001 | Audi |
| 0x0002 | BMW |
| 0x0003 | Daimler AG |
| 0x0004 | Motorola |
| 0x0005 | VCT/Mentor Graphics |
| 0x0006 | VW (VW-Group) |
| 0x0007 | Volvo Cars |
| 0x0008 | Ford Motor Company |
| 0x000B | Freescale Semiconductor |
| 0x0011 | NXP Semiconductors |
| 0x0012 | ST Microelectronics |
| 0x0013 | Melexis GmbH |
| 0x0014 | Microchip Technology Inc |
| 0x0015 | Centro Ricerche FIAT |
| 0x0016 | Renesas Technology Europe GmbH (formerly Mitsubishi) |
| 0x0017 | Atmel Germany GmbH |
| 0x0018 | Magneti Marelli S.p. A |
| 0x0019 | NEC Electronics GmbH |
| 0x001A | Fujitsu Microelectronics Europe GmbH |
| 0x001B | Adam Opel AG |
| 0x001C | Infineon Technologies AG |
| 0x001D | AMI Semiconductor Belguim BVBA |
| 0x001E | Vector Informatik GmbH |
| 0x001F | Brose Fahrzeugteile GmbH & Co |
| 0x0020 | Zentrum Mikroelektronik Dresden AG |
| 0x0021 | ihr GmbH |
| 0x0022 | Visteon Deutschland GmbH |
| 0x0023 | Elmos Semiconductor AG |
| 0x0024 | ON Semiconductor Germany GmbH |
| 0x0025 | Denso Corporation |
| 0x0026 | C&S Group GmbH |
| 0x0027 | Renault SA |
| 0x0028 | Renesas Technology Europe Ltd (formerly Hitachi) |
| 0x0029 | Yazaki Europe Ltd |
| 0x002A | Trinamic Microchips GmbH |
| 0x002B | Allegro Microsystems, Inc |
| 0x002C | Toyota Motor Engineering and Manufacturing Europe N.V / S.A |
| 0x002D | PSA Peugeot Citroen |
| 0x002E | Forschungs - und Transferzentrum e.V. der Westsächsische Hochschule Zwickau |
| 0x002F | Micron Electronic Devices AG |
| 0x0030 | Delphi Deutschland GmbH |
| 0x0031 | Texas Instruments Deutschland GmbH |
| 0x0032 | Maxim Integrated Products |
| 0x0033 | Bertrandt GmbH |
| 0x0034 | PKC Group Oyi |
| 0x0035 | BayTech IKs |
| 0x0036 | Hella KGaA & Co. |
| 0x0037 | Continental Automotive |
| 0x0038 | Johnson Controls GmbH |
| 0x0039 | Toshiba Electronics Europe GmbH |
| 0x003A | Analog Devices |
| 0x003B | TRW Automotive Electronics & Components GmbH & Co. KG |
| 0x003C | Advanced Data Controls, Corp. |
| 0x003D | GÖPEL electronic GmbH |
| 0x003E | Dr. Ing. h.c. F. Porsche AG |
| 0x003F | Marquardt GmbH |
| 0x0040 | ETAS GmbH - Robert Bosch |
| 0x0041 | Micronas GmbH |
| 0x0042 | Preh GmbH |
| 0x0043 | GENTEX CORPORATION |
| 0x0044 | ZF Lenksysteme GmbH |
| 0x0045 | Nagares S.A. |
| 0x0046 | MAN Nutzfahrzeuge AG |
| 0x0047 | BITRON SpA BU Grugliasco |
| 0x0048 | Pierburg GmbH |
| 0x0049 | Alps Electrics Co., Ltd |
| 0x004A | Beru Electronics GmbH |
| 0x004B | Paragon AG |
| 0x004C | Silicon Laboratories |
| 0x004D | Sensata Technologies Holland B.V. |
| 0x004E | Meta System S.p.A |
| 0x004F | DST Dräxlmaier Systemtechnik GmbH |
| 0x0050 | Grupo Antolin Ingenieria, S.A. |
| 0x0051 | MAGNA-Donnelly GmbH&Co.KG |
| 0x0052 | IEE S.A. |
| 0x0053 | austriamicrosystems AG |
| 0x0054 | Agilent Technologies, Inc. |
| 0x0055 | Lear Corporation  |
| 0x0056 | KOSTAL Ireland GmbH |
| 0x0057 | LIPOWSKY Industrie-Elektronik GmbH  |
| 0x0058 | Sanken Electric Co.,Ltd |
| 0x0059 | Elektrobit Automotive GmbH |
| 0x005A | VIMERCATI S.p.A. |
| 0x005B | VOLVO Group Trucks |
| 0x005C | SMSC Europe GmbH |
| 0x0060 | Sitronic GmbH & Co. KG |
| 0x0061 | Flextronics / Sidler Automotive GmbH & Co. KG |
| 0x0062 | EAO Automotive GmbH & Co. KG |
| 0x0063 | helag-electronic gmbh |
| 0x0064 | Magna Electronics |
| 0x0065 | INTEVA Products, LLC (formerly Arvinmeritor 2011-03-29) |
| 0x0066 | Valeo SA |
| 0x0067 | Defond Holding / BJAutomotive / DAC |
| 0x0068 | Industrie Saleri S. p. A. |
| 0x0069 | ROHM Semicon GmbH |
| 0x0070 | Alfmeier Präzision AG |
| 0x0071 | Sanden Corporation |
| 0x0072 | Huf Hülsbeck & Fürst GmbH & Co. KG |
| 0x0073 | ebm-papst St. Georgen GmbH & Co. KG |
| 0x0074 | CATEM |
| 0x0075 | OMRON Automotive Electronics Technology GmbH |
| 0x0076 | Johnson Electric International |
| 0x0077 | A123 Systems |
| 0x0078 | IPG Automotive GmbH, Karlsruhe |
| 0x0079 | Daesung Electric Co. Ltd. |
| 0x007A | Kromberg & Schubert GmbH & Co. KG |
| 0x007B | Bury GmbH & Co. KG |
| 0x007E | Measurement Specialties Inc (MEAS) |
| 0x007F | MRS Electronic GmbH |
| 0x0082 | Dale Electronics Inc |
| 0x0083 | Mirror Controls international |
| 0x0084 | Keboda Technology Co. Ltd. |
| 0x0085 | SPD Control Systems Corporation |
| 0x0087 | Röchling Automotive AG & Co. KG |
| 0x0088 | AEV s.r.o |
| 0x0089 | Kongsberg Automotive AB/Mullsjö Works |
| 0x008A | May & Scofield Ltd |
| 0x008C | C&S Technology Inc |
| 0x008D | RDC Semiconductor Co., Ltd |
| 0x008E | Webasto AG |
| 0x008F | Accel Elektronika UAB |
| 0x0090 | FICOSA International S.A. |
| 0x0091 | Mahle |
| 0x0093 | Phoenix International |
| 0x0094 | John Deere |
| 0x0095 | Grayhill Inc |
| 0x0096 | AppliedSensor GmbH |
| 0x0097 | UST Umweltsensortechnik GmbH |
| 0x0098 | Digades GmbH |
| 0x0099 | Thomson Linear Motion |
| 0x009A | TriMark Corporation |
| 0x009B | KB Auto Tech Co., Ltd. |
| 0x009C | Methode Electronics, Inc |
| 0x009D | Danlaw, Inc. |
| 0x009E | Federal-Mogul Corporation |
| 0x009F | Fujikoki Corporation |
| 0x00A0 | MENTOR Gmbh & Co. Praezisions-Bauteile KG |
| 0x00A1 | Toyota Industries Corporation |
| 0x00A2 | Strattec Security Corp. |
| 0x00A3 | TE Connectivity |
| 0x00A4 | Westfalia Automotive GmbH |
| 0x00A5 | Woco Industrietechnik GmbH |
| 0x00A6 | Minebea Co., Ltd |
| 0x00A7 | Magna |
| 0x00A8 | Dong IL Technology |
| 0x00A9 | Wilo SE |
| 0x00AA | Remy International, Inc. |
| 0x00AB | ACCUmotive |
| 0x00AC | Carling Technologies |
| 0x00B0 | Hanon Systems Korea |
| 0x00B1 | Eberspächer Controls Esslingen GmbH & Co. KG |
| 0x00B2 | WABCO Development GmbH |
| 0x00B3 | Sensirion AG |
| 0x00B4 | OSHINO Electronics Estonia OÜ |
| 0x00B5 | Fishman Thermo Technologies  LTD |
| 0x00B6 | Novalog Ltd |
| 0x00B7 | Hanon Systems USA |
| 0x00B8 | Leggett & Platt Automotive Group |
| 0x00B9 | Tremec |
| 0x00BA | Check Corporation |
| 0x00BB | Federal-Mogul Corporation |
| 0x00BC | fischer automotive systems |
| 0x00BD | Hi-Lex Europe GmbH |
| 0x00BE | SGX Sensortech |
| 0x00BF | AGM Automotive |
| 0x00C0 | Melecs |
| 0x00C1 | Robertshaw Controls Company |
| 0x00D0 | Dometic |
| 0x0100 | Isabellenhuette Heusler GmbH & Co. KG |
| 0x0101 | Huber Automotive AG |
| 0x0102 | Precision Motors Deutsche Minebea GmbH |
| 0x0103 | TK Holdings Inc., Electronics |
| 0x0104 | Cobra Automotive Technologies S.P.A. |
| 0x0105 | Embed Limited |
| 0x0106 | Kissling Elektrotechnik GmbH |
| 0x0107 | Autoliv B.V. & Co. KG |
| 0x0108 | PST Electronics |
| 0x0109 | BCA Leisure Ltd |
| 0x010A | APAG Elektronik AG |
| 0x010B | RAFI GmbH & Co. KG |
| 0x010C | Sonceboz AutomotiveSA |
| 0x010D | i2s Intelligente Sensorsysteme Dresden GmbH |
| 0x010E | AGM Automotive, Inc. |
| 0x010F | S&T Motiv |
| 0x0111 | UG Systems GmbH & Co. KG |
| 0x0113 | CHANGJIANG AUTOMOBILE ELECTRONIC SYSTEM CO.,LTD |
| 0x0114 | MES S.A. |
| 0x0115 | SL Corporation |
| 0x0116 | Dura Automotive Systems |
| 0x0118 | Delta Electronics, Inc. |
| 0x0119 | Penny and Giles Controls Ltd |
| 0x011A | Curtiss Wright Controls Industrial |
| 0x011B | HKR Seuffer Automotive GmbH & Co. KG |
| 0x011C | DMK U.S.A. Inc |
| 0x0120 | Littelfuse |
| 0x0121 | Hyundai MOBIS |
| 0x0122 | Alpine Electronics of America |
| 0x0123 | Ford Motor Company |
| 0x0124 | Hangzhou Sanhua Research Inst. Co, Ltd. |
| 0x0125 | Delvis |
| 0x0126 | Louko |
| 0x0127 | Etratech |
| 0x0128 | HiRain |
| 0x0129 | elobau GmbH & Co. KG |
| 0x012A | I.G.Bauerhin GmbH |
| 0x012B | HANS WIDMAIER  |
| 0x012C | Gentherm Inc |
| 0x012D | LINAK A/S |
| 0x012E | Casco Products Corporation |
| 0x012F | Bühler Motor GmbH |
| 0x0130 | SphereDesign GmbH |
| 0x0131 | Cooper Standard |
| 0x0132 | KÜSTER Automotive Control Systems GmbH |
| 0x0133 | SEWS-Components Europe B.V. |
| 0x0134 | OLHO tronic GmbH |
| 0x0135 | LG Electronics |
| 0x0136 | Eberspächer Controls GmbH & Co. KG |
| 0x0137 | AISIN Seiki Co., Ltd. |
| 0x0138 | Elektrosil Systeme der Elektronik GmbH |
| 0x0139 | Nidec Corporation |
| 0x013A | ISSI Integrated Silicon Solution Inc |
| 0x013B | Twin Disc, Incorporated |
| 0x013C | SPAL Automotive Srl |
| 0x013D | OTTO Engineering, Inc. |
| 0xFFFF | unbekannter Hersteller |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 35 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler momentan vorhanden und bereits gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler momentan vorhanden und bereits gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler momentan vorhanden und bereits gespeichert |
| 0x20 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x21 | Fehler momentan vorhanden und bereits gespeichert |
| 0x24 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x25 | Fehler momentan vorhanden und bereits gespeichert |
| 0x28 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x29 | Fehler momentan vorhanden und bereits gespeichert |
| 0x2C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x2D | Fehler momentan vorhanden und bereits gespeichert |
| 0x40 | unbekannte Fehlerart |
| 0x44 | Fehler gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler gespeichert |
| 0x4D | Fehler gespeichert |
| 0x60 | Fehler gespeichert |
| 0x61 | Fehler gespeichert |
| 0x64 | Fehler gespeichert |
| 0x65 | Fehler gespeichert |
| 0x68 | Fehler gespeichert |
| 0x69 | Fehler gespeichert |
| 0x6C | Fehler gespeichert |
| 0x6D | Fehler gespeichert |
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x80 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x81 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-uds-tab-roe-aktiv"></a>
### UDS_TAB_ROE_AKTIV

Dimensions: 3 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0x00 | Aktive Fehlermeldung deaktiviert |
| 0x01 | Aktive Fehlermeldung aktiviert |
| 0xFF | Status der aktiven Fehlermeldung nicht feststellbar |

<a id="table-cbskennung"></a>
### CBSKENNUNG

Dimensions: 12 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelag vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x05 | Bsi | Service Inclusive |
| 0x06 | Br_h | Bremsbelag hinten |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x15 | Efk | Einfahrkontrolle |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |
| 0x0D | NOx_a | NOx-Additiv |
| 0x64 | Sic_v | Sichtpruefung/Fahrzeug-Check verknuepft |

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 2 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | kein Betriebsmode gesetzt | kein Betriebsmode |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | ja |
| F_HLZ | ja |
| F_SEVERITY | nein |
| F_UWB_SATZ | 8 |
| F_HLZ_VIEW | ja |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 1223 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x021200 | Transportmodus: aktiv | 0 | - |
| 0x021300 | Transportmodus: aktiv | 0 | - |
| 0x100201 | Drosselklappe, schwergängig: zu langsam | 0 | - |
| 0x100301 | DME, interner Fehler, Ansteuerung Drosselklappe: Fehlfunktion | 0 | - |
| 0x100401 | Drosselklappe, schwergängig: zu langsam | 0 | - |
| 0x100501 | Drosselklappe 2, schwergängig: zu langsam | 0 | - |
| 0x100601 | Drosselklappe, Ansteuerung: Fehlfunktion | 0 | - |
| 0x100701 | DME, interner Fehler, Ansteuerung Drosselklappe 2: Fehlfunktion | 0 | - |
| 0x100801 | Drosselklappe, Funktion: klemmt | 0 | - |
| 0x100901 | Drosselklappe 2, Funktion: klemmt | 0 | - |
| 0x100A02 | Drosselklappe, Drosselklappenpotenziometer 1 und 2: Doppelfehler | 0 | - |
| 0x100B02 | Drosselklappe 2, Drosselklappenpotenziometer 1 und 2: Doppelfehler | 0 | - |
| 0x100C08 | Drosselklappe, Drosselklappenpotenziometer 1: Signal unplausibel zur Luftmasse | 0 | - |
| 0x100D08 | Drosselklappe 2, Drosselklappenpotenziometer 1: Signal unplausibel zur Luftmasse | 0 | - |
| 0x100E08 | Drosselklappe, Drosselklappenpotenziometer 2: Signal unplausibel zur Luftmasse | 0 | - |
| 0x100F08 | Drosselklappe 2, Drosselklappenpotenziometer 2: Signal unplausibel zur Luftmasse | 0 | - |
| 0x101001 | Drosselklappe, Drosselklappenpotenziometer 1: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x101002 | Drosselklappe: Drosselklappenpotenziometer 1, Kurzschluss nach Masse | 0 | - |
| 0x101101 | Drosselklappe 2, Drosselklappenpotenziometer 1: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x101102 | Drosselklappe 2: Drosselklappenpotenziometer 1, Kurzschluss nach Masse | 0 | - |
| 0x101201 | Drosselklappe: Drosselklappenpotenziometer 2, Kurzschluss nach Plus | 0 | - |
| 0x101202 | Drosselklappe, Drosselklappenpotenziometer 2: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x101301 | Drosselklappe 2: Drosselklappenpotenziometer 2, Kurzschluss nach Plus | 0 | - |
| 0x101302 | Drosselklappe 2, Drosselklappenpotenziometer 2: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x101401 | Drosselklappe, Adaption: Randbedingungen nicht erfüllt | 1 | - |
| 0x101402 | Drosselklappe: Notluftposition nicht adaptiert | 0 | - |
| 0x101408 | Drosselklappe: Erstadaption, unterer Anschlag nicht gelernt | 0 | - |
| 0x101501 | Drosselklappe 2, Adaption: Randbedingungen nicht erfüllt | 1 | - |
| 0x101502 | Drosselklappe 2: Notluftposition nicht adaptiert | 0 | - |
| 0x101508 | Drosselklappe 2: Erstadaption, unterer Anschlag nicht gelernt | 0 | - |
| 0x101601 | Drosselklappe: Federtest, unterer Anschlag nicht erreicht | 0 | - |
| 0x101602 | Drosselklappe: Federtest, Fehler untere Rückstellfeder | 0 | - |
| 0x101604 | Drosselklappe, Federtest: obere Sollposition nicht erreicht | 0 | - |
| 0x101608 | Drosselklappe, Federtest: Fehler obere Rückstellfeder | 0 | - |
| 0x101701 | Drosselklappe 2: Federtest, unterer Anschlag nicht erreicht | 0 | - |
| 0x101702 | Drosselklappe 2: Federtest, Fehler untere Rückstellfeder | 0 | - |
| 0x101704 | Drosselklappe 2, Federtest: obere Sollposition nicht erreicht | 0 | - |
| 0x101708 | Drosselklappe 2, Federtest: Fehler obere Rückstellfeder | 0 | - |
| 0x101801 | Drosselklappe 2, Startprüfung: Federtest | 0 | - |
| 0x101802 | Drosselklappe 2, Startprüfung: Prüfung Notluftposition | 0 | - |
| 0x101901 | Drosselklappe, Startprüfung: Federtest | 0 | - |
| 0x101902 | Drosselklappe, Startprüfung: Prüfung Notluftposition | 0 | - |
| 0x101C08 | Drosselklappe, Drosselklappenpotenziometer, Plausibilität: Gleichlauffehler zwischen Potentiometer 1 und 2 | 0 | - |
| 0x101D08 | Drosselklappe 2, Drosselklappenpotenziometer, Plausibilität: Gleichlauffehler zwischen Potentiometer 1 und 2 | 0 | - |
| 0x101F01 | Drosselklappenwinkel - Saugrohrdruck, Korrelation: Grenzwert überschritten | 0 | - |
| 0x101F02 | Drosselklappenwinkel - Absolutdruck Saugrohr, Vergleich: Druck zu niedrig | 0 | - |
| 0x102001 | Luftmasse, Plausibilität: Luftmasse zu hoch | 0 | - |
| 0x102002 | Luftmasse, Plausibilität: Luftmasse zu niedrig | 0 | - |
| 0x102301 | Luftmassenmesser, Arbeitsbereich: Periodendauer zu groß, Luftmasse zu niedrig | 0 | - |
| 0x102302 | Luftmassenmesser, Arbeitsbereich: Periodendauer zu niedrig, Luftmasse zu hoch | 0 | - |
| 0x102401 | Luftmassenmesser 2, Messbereich: Periodendauer zu groß, Luftmasse zu gering | 0 | - |
| 0x102402 | Luftmassenmesser 2, Arbeitsbereich: Periodendauer zu niedrig, Luftmasse zu hoch | 0 | - |
| 0x102501 | Luftmassenmesser: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x102502 | Luftmassenmesser: Kurzschluss nach Masse | 0 | - |
| 0x102601 | Luftmassenmesser 2: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x102602 | Luftmassenmesser 2: Kurzschluss nach Masse | 0 | - |
| 0x102901 | Luftmasse 2, Plausibilität: Luftmasse zu hoch | 0 | - |
| 0x102902 | Luftmasse 2, Plausibilität: Luftmasse zu niedrig | 0 | - |
| 0x102B01 | Luftmassenmesser, Korrektursignal: Kurzschluss nach Plus | 0 | - |
| 0x102B02 | Luftmassenmesser, Korrektursignal: Kurzschluss nach Masse | 0 | - |
| 0x102C01 | Luftmassenmesser 2, Korrektursignal: Kurzschluss nach Plus | 0 | - |
| 0x102C02 | Luftmassenmesser 2, Korrektursignal: Kurzschluss nach Masse | 0 | - |
| 0x102D01 | Luftmassenmesser, Korrektursignal, Arbeitsbereich: Periodendauer zu groß | 0 | - |
| 0x102D02 | Luftmassenmesser, Korrektursignal, Arbeitsbereich: Periodendauer zu niedrig | 0 | - |
| 0x102E01 | Luftmassenmesser 2, Korrektursignal, Arbeitsbereich: Periodendauer zu groß | 0 | - |
| 0x102E02 | Luftmassenmesser 2, Korrektursignal, Arbeitsbereich: Periodendauer zu niedrig | 0 | - |
| 0x103001 | Fahrpedalmodul, Pedalwertgeber 1: Kurzschluss nach Plus | 0 | - |
| 0x103002 | Fahrpedalmodul, Pedalwertgeber 1: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x103004 | Fahrpedalmodul, Pedalwertgeber 1: Arbeitsbereich, Spannung zu hoch | 0 | - |
| 0x103008 | Fahrpedalmodul, Pedalwertgeber 1: Arbeitsbereich, Spannung zu niedrig | 0 | - |
| 0x103101 | Fahrpedalmodul, Pedalwertgeber 2: Kurzschluss nach Plus | 0 | - |
| 0x103102 | Fahrpedalmodul, Pedalwertgeber 2: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x103104 | Fahrpedalmodul, Pedalwertgeber 2: Arbeitsbereich, Spannung zu hoch | 0 | - |
| 0x103108 | Fahrpedalmodul, Pedalwertgeber 2: Arbeitsbereich, Spannung zu niedrig | 0 | - |
| 0x103208 | Fahrpedalmodul, Pedalwertgeber: Doppelfehler | 0 | - |
| 0x103308 | Fahrpedalmodul, Pedalwertgeber, Plausibilität: Gleichlauffehler zwischen Pedalwertgeber 1 und Pedalwertgeber 2 | 0 | - |
| 0x104301 | Absolutdrucksensor, Saugrohr: Nachlauf, Druck zu hoch | 0 | - |
| 0x104302 | Absolutdrucksensor, Saugrohr: Nachlauf, Druck zu niedrig | 0 | - |
| 0x104401 | Absolutdrucksensor, Saugrohr: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x104402 | Absolutdrucksensor, Saugrohr: Kurzschluss nach Masse | 0 | - |
| 0x104501 | Absolutdrucksensor 2, Saugrohr: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x104502 | Absolutdrucksensor 2, Saugrohr: Kurzschluss nach Masse | 0 | - |
| 0x104601 | Absolutdrucksensor 2, Saugrohr: Nachlauf, Druck zu hoch | 0 | - |
| 0x104602 | Absolutdrucksensor 2, Saugrohr: Nachlauf, Druck zu niedrig | 0 | - |
| 0x105001 | Umgebungsdrucksensor: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x105002 | Umgebungsdrucksensor: Kurzschluss nach Masse | 0 | - |
| 0x105101 | Umgebungsdrucksensor, Plausibilität: Maximaldruck unplausibel | 0 | - |
| 0x105102 | Umgebungsdrucksensor, Plausibilität: Minimaldruck unplausibel | 0 | - |
| 0x105201 | Umgebungsdrucksensor, Nachlauf: Druck zu hoch | 0 | - |
| 0x105202 | Umgebungsdrucksensor, Nachlauf: Druck zu niedrig | 0 | - |
| 0x107001 | Drosselklappenwinkel - Saugrohrdruck 2, Korrelation: Grenzwert überschritten | 0 | - |
| 0x107002 | Drosselklappenwinkel 2 - Absolutdruck Saugrohr 2, Vergleich: Druck zu niedrig | 0 | - |
| 0x107508 | Luftmassenmesser, Eigendiagnose: Sensor defekt | 0 | - |
| 0x107608 | Luftmassenmesser 2, Eigendiagnose: Sensor defekt | 0 | - |
| 0x107C08 | Luftmassenmesser, Laststeuerung: Massenstrom zu hoch | 0 | - |
| 0x107D08 | Luftmassenmesser 2, Laststeuerung: Massenstrom zu hoch | 0 | - |
| 0x108201 | Ansauglufttemperatur: Plausibilität, Temperatur zu hoch | 0 | - |
| 0x108202 | Ansauglufttemperatur: Plausibilität, Temperatur zu niedrig | 0 | - |
| 0x108208 | Ansauglufttemperatur: Signal, festliegend | 0 | - |
| 0x108301 | Ansauglufttemperatur 2: Plausibilität, Temperatur zu hoch | 0 | - |
| 0x108302 | Ansauglufttemperatur 2: Plausibilität, Temperatur zu niedrig | 0 | - |
| 0x108308 | Ansauglufttemperatur 2: Signal, festliegend | 0 | - |
| 0x108401 | Ansauglufttemperatursensor vor Drosselklappe, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x108402 | Ansauglufttemperatursensor vor Drosselklappe, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x108501 | Ansauglufttemperatursensor vor Drosselklappe 2, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x108502 | Ansauglufttemperatursensor vor Drosselklappe 2, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x108601 | Ansauglufttemperatur vor Drosselklappe: Plausibilität, Temperatur zu hoch | 0 | - |
| 0x108602 | Ansauglufttemperatur vor Drosselklappe: Plausibilität, Temperatur zu niedrig | 0 | - |
| 0x108608 | Ansauglufttemperatur vor Drosselklappe: Signal, festliegend | 0 | - |
| 0x108701 | Ansauglufttemperatur vor Drosselklappe 2: Plausibilität, Temperatur zu hoch | 0 | - |
| 0x108702 | Ansauglufttemperatur vor Drosselklappe 2: Plausibilität, Temperatur zu niedrig | 0 | - |
| 0x108708 | Ansauglufttemperatur vor Drosselklappe 2: Signal, festliegend | 0 | - |
| 0x108801 | Ansauglufttemperatursensor vor Drosselklappe: Signaländerung, zu schnell | 0 | - |
| 0x108804 | Ansauglufttemperatursensor vor Drosselklappe: Plausibilität, Kaltstart, Temperatur zu hoch | 0 | - |
| 0x108808 | Ansauglufttemperatursensor vor Drosselklappe: Signaländerung, zu schnell | 0 | - |
| 0x108901 | Ansauglufttemperatursensor vor Drosselklappe 2: Signaländerung, zu schnell | 0 | - |
| 0x108904 | Ansauglufttemperatursensor vor Drosselklappe 2: Plausibilität, Kaltstart, Temperatur zu hoch | 0 | - |
| 0x108908 | Ansauglufttemperatursensor vor Drosselklappe 2: Signaländerung, zu schnell | 0 | - |
| 0x108A01 | Ladelufttemperatursensor, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x108A02 | Ladelufttemperatursensor, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x108B01 | Ladelufttemperatursensor 2, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x108B02 | Ladelufttemperatursensor 2, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x108C01 | Ladelufttemperatur: Plausibilität, Temperatur zu hoch | 0 | - |
| 0x108C02 | Ladelufttemperatur: Plausibilität, Temperatur zu niedrig | 0 | - |
| 0x108C08 | Ladelufttemperatur: Signal, festliegend | 0 | - |
| 0x108D01 | Ladelufttemperatur 2: Plausibilität, Temperatur zu hoch | 0 | - |
| 0x108D02 | Ladelufttemperatur 2: Plausibilität, Temperatur zu niedrig | 0 | - |
| 0x108D08 | Ladelufttemperatur 2: Signal, festliegend | 0 | - |
| 0x109001 | Kühlmitteltemperatursensor, elektrisch: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x109002 | Kühlmitteltemperatursensor, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x109208 | Kühlmitteltemperatursensor, Plausibilität: Signal hängt | 0 | - |
| 0x109308 | Kühlmitteltemperatursensor, Plausibilität: Signaländerung zu schnell | 0 | - |
| 0x109408 | Kühlmitteltemperatursensor, Plausibilität: Signal hängt im oberen Messbereich | 0 | - |
| 0x10A001 | Temperatursensor Kühleraustritt, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x10A002 | Temperatursensor Kühleraustritt, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x10A108 | Temperatursensor Kühleraustritt, Signaländerung: zu schnell | 0 | - |
| 0x10A201 | Temperatursensor Kühleraustritt: Plausibilität, Kaltstart, Temperatur zu hoch | 0 | - |
| 0x10A208 | Temperatursensor Kühleraustritt: Signal, festliegend | 0 | - |
| 0x10B008 | Außentemperatursensor, Plausibilität: Signal unplausibel | 0 | - |
| 0x10B101 | Außentemperatursensor, elektrisch: Kurzschluss nach Plus oder Leitungsunterbrechung | 1 | - |
| 0x10B102 | Außentemperatursensor, elektrisch: Kurzschluss nach Masse | 1 | - |
| 0x10B104 | Außentemperatursensor, elektrisch: Signalfehler | 1 | - |
| 0x10C000 | Ladelufttemperatursensor | 0 | - |
| 0x10C001 | Ladelufttemperatursensor: Signaländerung, zu schnell | 0 | - |
| 0x10C004 | Ladelufttemperatursensor: Plausibilität, Kaltstart, Temperatur zu hoch | 0 | - |
| 0x10C008 | Ladelufttemperatursensor: Signaländerung, zu schnell | 0 | - |
| 0x10C100 | Ladelufttemperatursensor 2 | 0 | - |
| 0x10C101 | Ladelufttemperatursensor 2: Signaländerung, zu schnell | 0 | - |
| 0x10C104 | Ladelufttemperatursensor 2: Plausibilität, Kaltstart, Temperatur zu hoch | 0 | - |
| 0x10C108 | Ladelufttemperatursensor 2: Signaländerung, zu schnell | 0 | - |
| 0x110001 | Zylindereinspritzabschaltung: Druck zu niedrig im Hochdrucksystem | 0 | - |
| 0x110002 | Zylindereinspritzabschaltung: Druck zu niedrig im Niederdrucksystem | 0 | - |
| 0x110008 | Zylindereinspritzabschaltung: Tankfüllstand zu gering | 0 | - |
| 0x110101 | Injektor Zylinder 1, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110102 | Injektor Zylinder 1, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110104 | Injektor Zylinder 1, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110108 | Injektor Zylinder 1, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110201 | Injektor Zylinder 2, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110202 | Injektor Zylinder 2, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110204 | Injektor Zylinder 2, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110208 | Injektor Zylinder 2, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110301 | Injektor Zylinder 3, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110302 | Injektor Zylinder 3, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110304 | Injektor Zylinder 3, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110308 | Injektor Zylinder 3, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110401 | Injektor Zylinder 4, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110402 | Injektor Zylinder 4, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110404 | Injektor Zylinder 4, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110408 | Injektor Zylinder 4, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110501 | Injektor Zylinder 5, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110502 | Injektor Zylinder 5, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110504 | Injektor Zylinder 5, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110508 | Injektor Zylinder 5, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110601 | Injektor Zylinder 6, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110602 | Injektor Zylinder 6, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110604 | Injektor Zylinder 6, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110608 | Injektor Zylinder 6, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110701 | Injektor Zylinder 7, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110702 | Injektor Zylinder 7, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110704 | Injektor Zylinder 7, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110708 | Injektor Zylinder 7, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110801 | Injektor Zylinder 8, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110802 | Injektor Zylinder 8, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110804 | Injektor Zylinder 8, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110808 | Injektor Zylinder 8, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110901 | Injektor Zylinder 9, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110902 | Injektor Zylinder 9, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110904 | Injektor Zylinder 9, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110908 | Injektor Zylinder 9, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110A01 | Injektor Zylinder 10, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110A02 | Injektor Zylinder 10, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110A04 | Injektor Zylinder 10, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110A08 | Injektor Zylinder 10, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110B01 | Injektor Zylinder 11, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110B02 | Injektor Zylinder 11, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110B04 | Injektor Zylinder 11, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110B08 | Injektor Zylinder 11, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110C01 | Injektor Zylinder 12, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110C02 | Injektor Zylinder 12, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110C04 | Injektor Zylinder 12, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110C08 | Injektor Zylinder 12, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x112101 | Injektor Zylinder 1, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112102 | Injektor Zylinder 1, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112104 | Injektor Zylinder 1, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112108 | Injektor Zylinder 1, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112201 | Injektor Zylinder 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112202 | Injektor Zylinder 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112204 | Injektor Zylinder 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112208 | Injektor Zylinder 2, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112301 | Injektor Zylinder 3, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112302 | Injektor Zylinder 3, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112304 | Injektor Zylinder 3, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112308 | Injektor Zylinder 3, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112401 | Injektor Zylinder 4, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112402 | Injektor Zylinder 4, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112404 | Injektor Zylinder 4, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112408 | Injektor Zylinder 4, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112501 | Injektor Zylinder 5, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112502 | Injektor Zylinder 5, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112504 | Injektor Zylinder 5, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112508 | Injektor Zylinder 5, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112601 | Injektor Zylinder 6, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112602 | Injektor Zylinder 6, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112604 | Injektor Zylinder 6, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112608 | Injektor Zylinder 6, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112701 | Injektor Zylinder 7, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112702 | Injektor Zylinder 7, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112704 | Injektor Zylinder 7, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112708 | Injektor Zylinder 7, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112801 | Injektor Zylinder 8, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112802 | Injektor Zylinder 8, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112804 | Injektor Zylinder 8, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112808 | Injektor Zylinder 8, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112901 | Injektor Zylinder 9, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112902 | Injektor Zylinder 9, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112904 | Injektor Zylinder 9, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112908 | Injektor Zylinder 9, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112A01 | Injektor Zylinder 10, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112A02 | Injektor Zylinder 10, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112A04 | Injektor Zylinder 10, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112A08 | Injektor Zylinder 10, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112B01 | Injektor Zylinder 11, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112B02 | Injektor Zylinder 11, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112B04 | Injektor Zylinder 11, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112B08 | Injektor Zylinder 11, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112C01 | Injektor Zylinder 12, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112C02 | Injektor Zylinder 12, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112C04 | Injektor Zylinder 12, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112C08 | Injektor Zylinder 12, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112E01 | Einspritzung 2, Plausibilität, Kaltstart: Anzahl Einspritzungen unplausibel | 0 | - |
| 0x112F01 | Einspritzung, Plausibilität, Kaltstart: Anzahl Einspritzungen unplausibel | 0 | - |
| 0x113101 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 1: Adaptionen nicht mehr möglich | 0 | - |
| 0x113201 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 2: Adaptionen nicht mehr möglich | 0 | - |
| 0x113301 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 3: Adaptionen nicht mehr möglich | 0 | - |
| 0x113401 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 4: Adaptionen nicht mehr möglich | 0 | - |
| 0x113501 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 5: Adaptionen nicht mehr möglich | 0 | - |
| 0x113601 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 6: Adaptionen nicht mehr möglich | 0 | - |
| 0x113701 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 7: Adaptionen nicht mehr möglich | 0 | - |
| 0x113801 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 8: Adaptionen nicht mehr möglich | 0 | - |
| 0x113901 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 9: Adaptionen nicht mehr möglich | 0 | - |
| 0x113A01 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 10: Adaptionen nicht mehr möglich | 0 | - |
| 0x113B01 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 11: Adaptionen nicht mehr möglich | 0 | - |
| 0x113C01 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 12: Adaptionen nicht mehr möglich | 0 | - |
| 0x115101 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 1: Adaption über gültigem Bereich | 0 | - |
| 0x115201 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 2: Adaption über gültigem Bereich | 0 | - |
| 0x115301 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 3: Adaption über gültigem Bereich | 0 | - |
| 0x115401 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 4: Adaption über gültigem Bereich | 0 | - |
| 0x115501 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 5: Adaption über gültigem Bereich | 0 | - |
| 0x115601 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 6: Adaption über gültigem Bereich | 0 | - |
| 0x115701 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 7: Adaption über gültigem Bereich | 0 | - |
| 0x115801 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 8: Adaption über gültigem Bereich | 0 | - |
| 0x115901 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 9: Adaption über gültigem Bereich | 0 | - |
| 0x115A01 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 10: Adaption über gültigem Bereich | 0 | - |
| 0x115B01 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 11: Adaption über gültigem Bereich | 0 | - |
| 0x115C01 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 12: Adaption über gültigem Bereich | 0 | - |
| 0x115D04 | Injektormengenabgleich, Plausibilität: Energie-Nominalwert | 0 | - |
| 0x115D08 | Injektormengenabgleich, Plausibilität: Kleinmengen-Nominalwert | 0 | - |
| 0x116100 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 1 | 0 | - |
| 0x116101 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 1: Adaption unter gültigem Bereich | 0 | - |
| 0x116200 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 2 | 0 | - |
| 0x116201 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 2: Adaption unter gültigem Bereich | 0 | - |
| 0x116301 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 3: Adaption unter gültigem Bereich | 0 | - |
| 0x116401 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 4: Adaption unter gültigem Bereich | 0 | - |
| 0x116501 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 5: Adaption unter gültigem Bereich | 0 | - |
| 0x116601 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 6: Adaption unter gültigem Bereich | 0 | - |
| 0x116701 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 7: Adaption unter gültigem Bereich | 0 | - |
| 0x116801 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 8: Adaption unter gültigem Bereich | 0 | - |
| 0x116901 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 9: Adaption unter gültigem Bereich | 0 | - |
| 0x116A01 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 10: Adaption unter gültigem Bereich | 0 | - |
| 0x116B01 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 11: Adaption unter gültigem Bereich | 0 | - |
| 0x116C01 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 12: Adaption unter gültigem Bereich | 0 | - |
| 0x118001 | Gemischregelung: Gemisch zu mager | 0 | - |
| 0x118002 | Gemischregelung: Gemisch zu fett | 0 | - |
| 0x118101 | Gemischregelung 2: Gemisch zu mager | 0 | - |
| 0x118102 | Gemischregelung 2: Gemisch zu fett | 0 | - |
| 0x118401 | Gemischregelung: Gemisch zu mager, große Abweichung | 0 | - |
| 0x118402 | Gemischregelung: Gemisch zu fett, große Abweichung | 0 | - |
| 0x118501 | Gemischregelung 2: Gemisch zu mager, große Abweichung | 0 | - |
| 0x118502 | Gemischregelung 2: Gemisch zu fett, große Abweichung | 0 | - |
| 0x118601 | Lambdasonde vor Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu fett | 0 | - |
| 0x118602 | Lambdasonde vor Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu mager | 0 | - |
| 0x118701 | Lambdasonde vor Katalysator 2, Gemischfeinregelung: Abgas nach Katalysator zu fett | 0 | - |
| 0x118702 | Lambdasonde vor Katalysator 2, Gemischfeinregelung: Abgas nach Katalysator zu mager | 0 | - |
| 0x118801 | Lambdasonde nach Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu fett | 0 | - |
| 0x118802 | Lambdasonde nach Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu mager | 0 | - |
| 0x118901 | Lambdasonde nach Katalysator 2, Gemischfeinregelung: Abgas nach Katalysator zu fett | 0 | - |
| 0x118902 | Lambdasonde nach Katalysator 2, Gemischfeinregelung: Abgas nach Katalysator zu mager | 0 | - |
| 0x119001 | Raildrucksensor, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x119002 | Raildrucksensor, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x119101 | Raildrucksensor 2, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x119102 | Raildrucksensor 2, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x119201 | Kraftstoffniederdrucksensor: elektrisch, Kurzschluss nach Plus | 0 | - |
| 0x119202 | Kraftstoffniederdrucksensor: elektrisch, Kurzschluss nach Masse | 0 | - |
| 0x119208 | Kraftstoffniederdrucksensor: Signal, festliegend | 0 | - |
| 0x119F01 | Kraftstoffhochdruck 2 bei Freigabe der Einspritzung: Druck zu niedrig | 0 | - |
| 0x11A001 | Kraftstoffhochdruck, Plausibilität: Druck zu hoch | 0 | - |
| 0x11A002 | Kraftstoffhochdruck, Plausibilität: Druck zu niedrig | 0 | - |
| 0x11A101 | Kraftstoffhochdruck 2, Plausibilität: Druck zu hoch | 0 | - |
| 0x11A102 | Kraftstoffhochdruck 2, Plausibilität: Druck zu niedrig | 0 | - |
| 0x11A201 | Kraftstoffniederdruck, Arbeitsbereich: Druck zu hoch | 0 | - |
| 0x11A202 | Kraftstoffniederdruck, Arbeitsbereich: Maximaldruck überschritten | 0 | - |
| 0x11A204 | Kraftstoffniederdruck, Arbeitsbereich: Druck zu niedrig | 0 | - |
| 0x11A401 | Kraftstoffhochdruck bei Freigabe der Einspritzung: Druck zu niedrig | 0 | - |
| 0x11A501 | Kraftstoffhochdruck, Arbeitsbereich: Druck zu hoch | 0 | - |
| 0x11A502 | Kraftstoffhochdruck, Arbeitsbereich: Druck zu hoch | 0 | - |
| 0x11A504 | Kraftstoffhochdruck, Arbeitsbereich: Druck zu niedrig | 0 | - |
| 0x11A601 | Kraftstoffhochdruck 2, Arbeitsbereich: Druck zu hoch | 0 | - |
| 0x11A602 | Kraftstoffhochdruck 2, Arbeitsbereich: Druck zu hoch | 0 | - |
| 0x11A604 | Kraftstoffhochdruck 2, Arbeitsbereich: Druck zu niedrig | 0 | - |
| 0x11A701 | Raildrucksensor, Plausibilität: Druck zu hoch | 0 | - |
| 0x11A702 | Raildrucksensor, Plausibilität: Druck zu niedrig | 0 | - |
| 0x11A801 | Raildrucksensor 2, Plausibilität: Druck zu hoch | 0 | - |
| 0x11A802 | Raildrucksensor 2, Plausibilität: Druck zu niedrig | 0 | - |
| 0x11AC01 | Kraftstoffhochdruck, Plausibilität, Kaltstart: Druck zu hoch | 0 | - |
| 0x11AC02 | Kraftstoffhochdruck, Plausibilität, Kaltstart: Druck zu niedrig | 0 | - |
| 0x11AD01 | Kraftstoffhochdruck 2, Plausibilität, Kaltstart: Druck zu hoch | 0 | - |
| 0x11AD02 | Kraftstoffhochdruck 2, Plausibilität, Kaltstart: Druck zu niedrig | 0 | - |
| 0x11B004 | Kraftstoffpumpe, Funktion: Notabschaltung | 1 | - |
| 0x11B101 | Elektrische Kraftstoffpumpe: Drehzahl zu hoch | 1 | - |
| 0x11B102 | Elektrische Kraftstoffpumpe: Drehzahl zu niedrig | 1 | - |
| 0x11B104 | Elektrische Kraftstoffpumpe: Notlauf | 1 | - |
| 0x11B108 | Kraftstoffpumpe: Übertemperatur | 1 | - |
| 0x11B201 | Kraftstoffniederdruckregelung, Plausibilität: Förderleistung außerhalb gültigem Bereich | 0 | - |
| 0x11B202 | Kraftstoffniederdruckregelung, Plausibilität: Förderleistung außerhalb Grenzwert wegen Alterung | 0 | - |
| 0x11B204 | Kraftstoffniederdruckregelung, Plausibilität: Förderleistung zu niedrig wegen Alterung | 0 | - |
| 0x11C201 | Mengensteuerventil, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x11C202 | Mengensteuerventil, Ansteuerung: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x11C301 | Mengensteuerventil 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x11C302 | Mengensteuerventil 2, Ansteuerung: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x11C401 | Mengensteuerventil, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x11C402 | Mengensteuerventil, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x120208 | Ladedruckregelung, Plausibilität: Druck zu hoch | 0 | - |
| 0x120308 | Ladedruckregelung, Plausibilität: Druck zu niedrig | 0 | - |
| 0x120408 | Ladedruckregelung, Abschaltung: Druckaufbau gesperrt | 0 | - |
| 0x120608 | Ladedruckregelung 2, Plausibilität: Druck zu hoch | 0 | - |
| 0x120708 | Ladedruckregelung 2, Plausibilität: Druck zu niedrig | 0 | - |
| 0x120908 | Ladedruckregelung 2, Abschaltung: Druckaufbau gesperrt | 0 | - |
| 0x121001 | Ladedrucksensor, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x121002 | Ladedrucksensor, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x121101 | Ladedrucksensor 2, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x121102 | Ladedrucksensor 2, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x121201 | Ladedrucksensor, Plausibilität, Nachlauf: Druck zu hoch | 0 | - |
| 0x121202 | Ladedrucksensor, Plausibilität, Nachlauf: Druck zu niedrig | 0 | - |
| 0x121301 | Ladedrucksensor 2, Plausibilität, Nachlauf: Druck zu hoch | 0 | - |
| 0x121302 | Ladedrucksensor 2, Plausibilität, Nachlauf: Druck zu niedrig | 0 | - |
| 0x122001 | Schubumluftventil, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x122002 | Schubumluftventil, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x122004 | Schubumluftventil, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x122101 | Schubumluftventil 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x122102 | Schubumluftventil 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x122104 | Schubumluftventil 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x123001 | Wastegate, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x123002 | Wastegate, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x123004 | Wastegate, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x123101 | Wastegate 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x123102 | Wastegate 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x123104 | Wastegate 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x128101 | Lambdasonde vor Katalysator, Systemprüfung: Signal konstant mager | 0 | - |
| 0x128201 | Lambdasonde vor Katalysator 2, Systemprüfung: Signal konstant mager | 0 | - |
| 0x128301 | Lambdasonde vor Katalysator, Systemprüfung: Signal konstant fett | 0 | - |
| 0x128401 | Lambdasonde vor Katalysator 2, Systemprüfung: Signal konstant fett | 0 | - |
| 0x128501 | Lambdasonde vor Katalysator, im Schub: Signal außerhalb Grenzwert | 0 | - |
| 0x128601 | Lambdasonde vor Katalysator 2, im Schub: Signal außerhalb Grenzwert | 0 | - |
| 0x128901 | Lambdasonde vor Katalysator, Dynamik: langsame Reaktion | 0 | - |
| 0x128902 | Lambdasonde vor Katalysator, Dynamik: langsame Reaktion | 0 | - |
| 0x128A01 | Lambdasonde vor Katalysator 2, Dynamik: langsame Reaktion | 0 | - |
| 0x128A02 | Lambdasonde vor Katalysator 2, Dynamik: langsame Reaktion | 0 | - |
| 0x128B01 | Lambdasonde vor Katalysator: Falschluft erkannt | 0 | - |
| 0x128C01 | Lambdasonde vor Katalysator 2: Falschluft erkannt | 0 | - |
| 0x128E01 | Lambdasonde vor Katalysator, Leitungsfehler: Unterbrechung Nernstleitung | 0 | - |
| 0x128E02 | Lambdasonde vor Katalysator, elektrisch: Unterbrechung virtuelle Masse oder Pumpstromleitung | 0 | - |
| 0x128E04 | Lambdasonde vor Katalysator, elektrisch: Unterbrechung virtuelle Masse oder Pumpstromleitung | 0 | - |
| 0x128F01 | Lambdasonde vor Katalysator 2, Leitungsfehler: Unterbrechung Nernstleitung | 0 | - |
| 0x128F02 | Lambdasonde vor Katalysator 2, elektrisch: Unterbrechung virtuelle Masse oder Pumpstromleitung | 0 | - |
| 0x128F04 | Lambdasonde vor Katalysator 2, elektrisch: Unterbrechung virtuelle Masse oder Pumpstromleitung | 0 | - |
| 0x129001 | Lambdasonde vor Katalysator, Signalleitungen: Kurzschluss nach Plus | 0 | - |
| 0x129002 | Lambdasonde vor Katalysator, Signalleitungen: Kurzschluss nach Masse | 0 | - |
| 0x129101 | Lambdasonde vor Katalysator 2, Signalleitungen: Kurzschluss nach Plus | 0 | - |
| 0x129102 | Lambdasonde vor Katalysator 2, Signalleitungen: Kurzschluss nach Masse | 0 | - |
| 0x129201 | DME, interner Fehler: Regler für Lambdasonde vor Katalysator defekt | 0 | - |
| 0x129202 | DME, interner Fehler: Regler für Lambdasonde vor Katalysator defekt | 0 | - |
| 0x129301 | DME, interner Fehler, Lambdasonde vor Katalysator 2: Initialisierungsfehler | 0 | - |
| 0x129302 | DME, interner Fehler, Lambdasonde vor Katalysator 2: Kommunikationsfehler | 0 | - |
| 0x12A101 | Lambdasonde nach Katalysator, Systemprüfung: Signal konstant fett | 0 | - |
| 0x12A102 | Lambdasonde nach Katalysator, Systemprüfung: Signal konstant Mager | 0 | - |
| 0x12A201 | Lambdasonde nach Katalysator 2, Systemprüfung: Signal konstant Fett | 0 | - |
| 0x12A202 | Lambdasonde nach Katalysator 2, Systemprüfung: Signal konstant Mager | 0 | - |
| 0x12A308 | Lambdasonde nach Katalysator, Dynamik, von Fett nach Mager: langsame Reaktion | 0 | - |
| 0x12A408 | Lambdasonde nach Katalysator 2, Dynamik, von Fett nach Mager: langsame Reaktion | 0 | - |
| 0x12A501 | Lambdasonde nach Katalysator 2: Signal festliegend auf Fett | 0 | - |
| 0x12A701 | Lambdasonde nach Katalysator, Signal: Kurzschluss nach Plus | 0 | - |
| 0x12A801 | Lambdasonde nach Katalysator 2, Signal: Kurzschluss nach Plus | 0 | - |
| 0x12A902 | Lambdasonde nach Katalysator, Signal: Kurzschluss nach Masse | 0 | - |
| 0x12AA02 | Lambdasonde nach Katalysator 2, Signal: Kurzschluss nach Masse | 0 | - |
| 0x12AB04 | Lambdasonde nach Katalysator, Signal: Leitungsunterbrechung | 0 | - |
| 0x12AC04 | Lambdasonde nach Katalysator 2, Signal: Leitungsunterbrechung | 0 | - |
| 0x12AD01 | Lambdasonde nach Katalysator: Signal festliegend auf Mager | 0 | - |
| 0x12AE01 | Lambdasonde nach Katalysator: Signal festliegend auf Fett | 0 | - |
| 0x12AF08 | Lambdasonde nach Katalysator, im Schub, von Fett nach Mager: verzögerte Reaktion | 0 | - |
| 0x12B001 | Lambdasonde nach Katalysator 2, von Fett nach Mager: verzögerte Reaktion | 0 | - |
| 0x12B008 | Lambdasonde nach Katalysator 2, im Schub, von Fett nach Mager: verzögerte Reaktion | 0 | - |
| 0x12B101 | Lambdasondenbeheizung vor Katalysator, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x12B102 | Lambdasondenbeheizung vor Katalysator, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x12B104 | Lambdasondenbeheizung vor Katalysator, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x12B201 | Lambdasondenbeheizung vor Katalysator 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x12B202 | Lambdasondenbeheizung vor Katalysator 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x12B204 | Lambdasondenbeheizung vor Katalysator 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x12B301 | Lambdasondenbeheizung nach Katalysator, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x12B302 | Lambdasondenbeheizung nach Katalysator, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x12B304 | Lambdasondenbeheizung nach Katalysator, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x12B401 | Lambdasondenbeheizung nach Katalysator 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x12B402 | Lambdasondenbeheizung nach Katalysator 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x12B404 | Lambdasondenbeheizung nach Katalysator 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x12B501 | Lambdasondentemperaturmessung vor Katalysator: Betriebstemperatur nicht erreicht | 0 | - |
| 0x12B502 | Lambdasondentemperaturmessung vor Katalysator: Betriebstemperatur im Warmlauf nicht erreicht | 0 | - |
| 0x12B504 | Lambdasondentemperaturmessung vor Katalysator: Messung im Steuergerät fehlgeschlagen | 0 | - |
| 0x12B601 | Lambdasondentemperaturmessung vor Katalysator 2: Betriebstemperatur nicht erreicht | 0 | - |
| 0x12B602 | Lambdasondentemperaturmessung vor Katalysator 2: Betriebstemperatur im Warmlauf nicht erreicht | 0 | - |
| 0x12B604 | Lambdasondentemperaturmessung vor Katalysator 2: Messung im Steuergerät fehlgeschlagen | 0 | - |
| 0x12B701 | Lambdasondenbeheizung nach Katalysator, Funktion: Innenwiderstand zu hoch | 0 | - |
| 0x12B801 | Lambdasondenbeheizung nach Katalysator 2, Funktion: Innenwiderstand zu hoch | 0 | - |
| 0x12B900 | Lambdasonde vor Katalysator, Temperatur | 0 | - |
| 0x12B901 | Lambdasondentemperaturmessung vor Katalysator: Betriebstemperatur nicht erreicht | 0 | - |
| 0x12B902 | Lambdasondentemperaturmessung vor Katalysator: Betriebstemperatur im Warmlauf nicht erreicht | 0 | - |
| 0x12B904 | Lambdasondentemperaturmessung vor Katalysator: Messung im Steuergerät fehlgeschlagen | 0 | - |
| 0x12BA01 | Lambdasondentemperaturmessung vor Katalysator 2: Betriebstemperatur nicht erreicht | 0 | - |
| 0x12BA02 | Lambdasondentemperaturmessung vor Katalysator 2: Betriebstemperatur im Warmlauf nicht erreicht | 0 | - |
| 0x12BA04 | Lambdasondentemperaturmessung vor Katalysator 2: Messung im Steuergerät fehlgeschlagen | 0 | - |
| 0x12BB01 | Lambdasonde nach Katalysator, von Mager nach Fett: verzögerte Reaktion | 0 | - |
| 0x12BC01 | Lambdasonde nach Katalysator 2, von Mager nach Fett: verzögerte Reaktion | 0 | - |
| 0x12BD01 | Lambdasonde nach Katalysator 2: Signal festliegend auf Mager | 0 | - |
| 0x12BE08 | Lambdasonde nach Katalysator, Dynamik, von Mager nach Fett: langsame Reaktion | 0 | - |
| 0x12BF08 | Lambdasonde nach Katalysator 2, Dynamik, von Mager nach Fett: langsame Reaktion | 0 | - |
| 0x130001 | VANOS-Magnetventil Einlass, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x130002 | VANOS-Magnetventil Einlass, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x130004 | VANOS-Magnetventil Einlass, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x130108 | VANOS, Einlass: Regelfehler, Position nicht erreicht | 0 | - |
| 0x130201 | VANOS-Magnetventil Auslass, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x130202 | VANOS-Magnetventil Auslass, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x130204 | VANOS-Magnetventil Auslass, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x130308 | VANOS, Auslass: Regelfehler, Position nicht erreicht | 0 | - |
| 0x130401 | VANOS-Magnetventil Einlass 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x130402 | VANOS-Magnetventil Einlass 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x130404 | VANOS-Magnetventil Einlass 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x130508 | VANOS, Einlass 2: Regelfehler, Position nicht erreicht | 0 | - |
| 0x130601 | VANOS-Magnetventil Auslass 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x130602 | VANOS-Magnetventil Auslass 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x130604 | VANOS-Magnetventil Auslass 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x130708 | VANOS, Auslass 2: Regelfehler, Position nicht erreicht | 0 | - |
| 0x130801 | Einlassnockenwelle, Positionsüberwachung: Zahnsprung | 0 | - |
| 0x130901 | Auslassnockenwelle, Positionsüberwachung: Zahnsprung | 0 | - |
| 0x130A01 | Einlassnockenwelle 2, Positionsüberwachung: Zahnsprung | 0 | - |
| 0x130B01 | Auslassnockenwelle 2, Positionsüberwachung: Zahnsprung | 0 | - |
| 0x130C01 | Kurbelwelle - Einlassnockenwelle, Referenz: Winkelunterschied außerhalb Grenzwert | 0 | - |
| 0x130D01 | Kurbelwelle - Auslassnockenwelle, Referenz: Winkelunterschied außerhalb Grenzwert | 0 | - |
| 0x130E01 | Kurbelwelle - Einlassnockenwelle, Synchronisation: Nockenwellensignal außerhalb Grenzwert | 0 | - |
| 0x130F01 | Kurbelwelle - Auslassnockenwelle, Synchronisation: Nockenwellensignal außerhalb Grenzwert | 0 | - |
| 0x131001 | Kurbelwelle - Einlassnockenwelle 2, Referenz: Winkelunterschied außerhalb Grenzwert | 0 | - |
| 0x131101 | Kurbelwelle - Auslassnockenwelle 2, Referenz: Winkelunterschied außerhalb Grenzwert | 0 | - |
| 0x131201 | Kurbelwelle - Einlassnockenwelle 2, Synchronisation: Nockenwellensignal außerhalb Grenzwert | 0 | - |
| 0x131301 | Kurbelwelle - Auslassnockenwelle 2, Synchronisation: Nockenwellensignal außerhalb Grenzwert | 0 | - |
| 0x131401 | VANOS, Auslass, Kaltstart: nicht regelbar | 0 | - |
| 0x131408 | VANOS, Auslass, Kaltstart: nicht regelbar | 0 | - |
| 0x131501 | VANOS, Einlass, Kaltstart: nicht regelbar | 0 | - |
| 0x131508 | VANOS, Einlass, Kaltstart: nicht regelbar | 0 | - |
| 0x131601 | VANOS, Auslass 2, Kaltstart: nicht regelbar | 0 | - |
| 0x131608 | VANOS, Auslass 2, Kaltstart: nicht regelbar | 0 | - |
| 0x131701 | VANOS, Einlass 2, Kaltstart: nicht regelbar | 0 | - |
| 0x131708 | VANOS, Einlass 2, Kaltstart: nicht regelbar | 0 | - |
| 0x131808 | VANOS, Auslass, Kaltstart: Position nicht erreicht | 0 | - |
| 0x131908 | VANOS, Einlass, Kaltstart: Position nicht erreicht | 0 | - |
| 0x132808 | VANOS, Auslass 2, Kaltstart: Position nicht erreicht | 0 | - |
| 0x132908 | VANOS, Einlass 2, Kaltstart: Position nicht erreicht | 0 | - |
| 0x138101 | Abgasklappe, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x138102 | Abgasklappe, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x138104 | Abgasklappe, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x138201 | Kühlerjalousie, oben, Versorgungsspannung, Eigendiagnose: Fehlfunktion | 0 | - |
| 0x138301 | Kühlerjalousie, oben, Eigendiagnose: Übertemperatur erkannt | 0 | - |
| 0x138401 | Kühlerjalousie, oben, Eigendiagnose: elektrischer Fehler | 0 | - |
| 0x138501 | Kühlerjalousie, oben: unterer Anschlag nicht erkannt | 0 | - |
| 0x138601 | Kühlerjalousie, oben: oberer Anschlag nicht erkannt | 0 | - |
| 0x138701 | Kühlerjalousie, oben: oberer Anschlag zu früh erkannt | 0 | - |
| 0x138901 | Kühlerjalousie, unten, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x138902 | Kühlerjalousie, unten, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x138904 | Kühlerjalousie, unten, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x138A01 | Abgasklappe 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x138A02 | Abgasklappe 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x138A04 | Abgasklappe 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x139001 | Lambdasonde nach Katalysator, von Fett nach Mager: verzögerte Reaktion | 0 | - |
| 0x140001 | Verbrennungsaussetzer, mehrere Zylinder: Einspritzung wird abgeschaltet | 0 | - |
| 0x140002 | Verbrennungsaussetzer, mehrere Zylinder: abgasschädigend nach Startvorgang | 0 | - |
| 0x140004 | Verbrennungsaussetzer, mehrere Zylinder: abgasschädigend | 0 | - |
| 0x140008 | Verbrennungsaussetzer, mehrere Zylinder: Summenfehler | 0 | - |
| 0x140101 | Verbrennungsaussetzer, Zylinder 1: Einspritzung wird abgeschaltet | 0 | - |
| 0x140102 | Verbrennungsaussetzer, Zylinder 1: abgasschädigend nach Startvorgang | 0 | - |
| 0x140104 | Verbrennungsaussetzer, Zylinder 1: abgasschädigend | 0 | - |
| 0x140201 | Verbrennungsaussetzer, Zylinder 2: Einspritzung wird abgeschaltet | 0 | - |
| 0x140202 | Verbrennungsaussetzer, Zylinder 2: abgasschädigend nach Startvorgang | 0 | - |
| 0x140204 | Verbrennungsaussetzer, Zylinder 2: abgasschädigend | 0 | - |
| 0x140301 | Verbrennungsaussetzer, Zylinder 3: Einspritzung wird abgeschaltet | 0 | - |
| 0x140302 | Verbrennungsaussetzer, Zylinder 3: abgasschädigend nach Startvorgang | 0 | - |
| 0x140304 | Verbrennungsaussetzer, Zylinder 3: abgasschädigend | 0 | - |
| 0x140401 | Verbrennungsaussetzer, Zylinder 4: Einspritzung wird abgeschaltet | 0 | - |
| 0x140402 | Verbrennungsaussetzer, Zylinder 4: abgasschädigend nach Startvorgang | 0 | - |
| 0x140404 | Verbrennungsaussetzer, Zylinder 4: abgasschädigend | 0 | - |
| 0x140500 | Verbrennungsaussetzer, Zylinder 5 | 0 | - |
| 0x140501 | Verbrennungsaussetzer, Zylinder 5: Einspritzung wird abgeschaltet | 0 | - |
| 0x140502 | Verbrennungsaussetzer, Zylinder 5: abgasschädigend nach Startvorgang | 0 | - |
| 0x140504 | Verbrennungsaussetzer, Zylinder 5: abgasschädigend | 0 | - |
| 0x140601 | Verbrennungsaussetzer, Zylinder 6: Einspritzung wird abgeschaltet | 0 | - |
| 0x140602 | Verbrennungsaussetzer, Zylinder 6: abgasschädigend nach Startvorgang | 0 | - |
| 0x140604 | Verbrennungsaussetzer, Zylinder 6: abgasschädigend | 0 | - |
| 0x140701 | Verbrennungsaussetzer, Zylinder 7: Einspritzung wird abgeschaltet | 0 | - |
| 0x140702 | Verbrennungsaussetzer, Zylinder 7: abgasschädigend nach Startvorgang | 0 | - |
| 0x140704 | Verbrennungsaussetzer, Zylinder 7: abgasschädigend | 0 | - |
| 0x140801 | Verbrennungsaussetzer, Zylinder 8: Einspritzung wird abgeschaltet | 0 | - |
| 0x140802 | Verbrennungsaussetzer, Zylinder 8: abgasschädigend nach Startvorgang | 0 | - |
| 0x140804 | Verbrennungsaussetzer, Zylinder 8: abgasschädigend | 0 | - |
| 0x140901 | Verbrennungsaussetzer, Zylinder 9: Einspritzung wird abgeschaltet | 0 | - |
| 0x140902 | Verbrennungsaussetzer, Zylinder 9: abgasschädigend nach Startvorgang | 0 | - |
| 0x140904 | Verbrennungsaussetzer, Zylinder 9: abgasschädigend | 0 | - |
| 0x140A01 | Verbrennungsaussetzer, Zylinder 10: Einspritzung wird abgeschaltet | 0 | - |
| 0x140A02 | Verbrennungsaussetzer, Zylinder 10: abgasschädigend nach Startvorgang | 0 | - |
| 0x140A04 | Verbrennungsaussetzer, Zylinder 10: abgasschädigend | 0 | - |
| 0x140B01 | Verbrennungsaussetzer, Zylinder 11: Einspritzung wird abgeschaltet | 0 | - |
| 0x140B02 | Verbrennungsaussetzer, Zylinder 11: abgasschädigend nach Startvorgang | 0 | - |
| 0x140B04 | Verbrennungsaussetzer, Zylinder 11: abgasschädigend | 0 | - |
| 0x140C01 | Verbrennungsaussetzer, Zylinder 12: Einspritzung wird abgeschaltet | 0 | - |
| 0x140C02 | Verbrennungsaussetzer, Zylinder 12: abgasschädigend nach Startvorgang | 0 | - |
| 0x140C04 | Verbrennungsaussetzer, Zylinder 12: abgasschädigend | 0 | - |
| 0x142002 | Verbrennungsaussetzer: Tankfüllstand zu gering | 0 | - |
| 0x143002 | Laufunruhemessung: Messfehler Kurbelwellensensor | 0 | - |
| 0x143108 | Otto Partikelfilter Temperatursensor vor OPF, Bank 1, Plausibilität, Kaltstart: Temperatur unplausibel | 0 | - |
| 0x143208 | Otto Partikelfilter Temperatursensor vor OPF, Bank 2, Plausibilität, Kaltstart: Temperatur unplausibel | 0 | - |
| 0x143308 | Otto Partikelfilter Temperatursensor nach OPF, Bank 2, Plausibilität, Kaltstart: Temperatur unplausibel | 0 | - |
| 0x143408 | Otto Partikelfilter Temperatursensor nach OPF, Bank 1, Plausibilität, Kaltstart: Temperatur unplausibel | 0 | - |
| 0x143501 | Otto Partikelfilter Temperatursensor vor OPF, Bank 1, elektrischer Fehler, Kurzschluss nach Plus oder offene Leitung | 0 | - |
| 0x143502 | Otto Partikelfilter Temperatursensor vor OPF, Bank 1, elektrischer Fehler, Kurzschluss nach Masse | 0 | - |
| 0x143601 | Otto Partikelfilter Temperatursensor vor OPF, Bank 2, elektrischer Fehler, Kurzschluss nach Plus oder offene Leitung | 0 | - |
| 0x143602 | Otto Partikelfilter Temperatursensor vor OPF, Bank 2, elektrischer Fehler, Kurzschluss nach Masse | 0 | - |
| 0x143901 | Otto Partikelfilter Temperatursensor nach OPF, Bank 2, elektrischer Fehler, Kurzschluss nach Plus oder offene Leitung | 0 | - |
| 0x143902 | Otto Partikelfilter Temperatursensor nach OPF, Bank 2, elektrischer Fehler, Kurzschluss nach Masse | 0 | - |
| 0x143B01 | Otto Partikelfilter Temperatursensor nach OPF, Bank 1, elektrischer Fehler, Kurzschluss nach Plus oder offene Leitung | 0 | - |
| 0x143B02 | Otto Partikelfilter Temperatursensor nach OPF, Bank 1, elektrischer Fehler, Kurzschluss nach Masse | 0 | - |
| 0x143D08 | Otto Partikelfilter Temperatursensor vor OPF, Bank 1, Plausibilität: Temperaturgradient zu hoch (Signal springt / Wackelkontakt) | 0 | - |
| 0x143E08 | Otto Partikelfilter Temperatursensor vor OPF, Bank 2, Plausibilität: Temperaturgradient zu hoch (Signal springt / Wackelkontakt) | 0 | - |
| 0x143F08 | Otto Partikelfilter Temperatursensor nach OPF, Bank 2, Plausibilität: Temperaturgradient zu hoch (Signal springt / Wackelkontakt) | 0 | - |
| 0x144008 | Otto Partikelfilter Temperatursensor nach OPF, Bank 1, Plausibilität: Temperaturgradient zu hoch (Signal springt / Wackelkontakt) | 0 | - |
| 0x144108 | Otto Partikelfilter Temperatursensor vor OPF, Bank 1, Plausibilität: Temperaturanstieg unplausibel | 0 | - |
| 0x144208 | Otto Partikelfilter Temperatursensor vor OPF, Bank 2, Plausibilität: Temperaturanstieg unplausibel | 0 | - |
| 0x144308 | Otto Partikelfilter Temperatursensor nach OPF, Bank 2, Plausibilität: Temperaturanstieg unplausibel | 0 | - |
| 0x144408 | Otto Partikelfilter Temperatursensor nach OPF, Bank 1, Plausibilität: Temperaturanstieg unplausibel | 0 | - |
| 0x144501 | Otto Partikelfilter Drucksensor, Bank 1, Drucksensoroffset: Adaptierte Offset unplausibel | 0 | - |
| 0x144601 | Otto Partikelfilter Drucksensor, Bank 2, Drucksensoroffset: Adaptierte Offset unplausibel | 0 | - |
| 0x144701 | Otto Partikelfilter Drucksensor, Bank 1, Drucksensorschlauch: Schlauchanschlüsse vertauscht, diagnostiziert während eines Fahrzyklus | 0 | - |
| 0x144801 | Otto Partikelfilter Drucksensor, Bank 2, Drucksensorschlauch: Schlauchanschlüsse vertauscht, diagnostiziert während eines Fahrzyklus | 0 | - |
| 0x144901 | Otto Partikelfilter Drucksensor, Bank 1, Plausibilität: Differenz des maximalen und minimalen Messwert unplausibel | 0 | - |
| 0x144A01 | Otto Partikelfilter Drucksensor, Bank 2, Plausibilität: Differenz des maximalen und minimalen Messwert unplausibel | 0 | - |
| 0x144B01 | Otto Partikelfilter Drucksensor, Bank 1, Plausibilität: Druck zu hoch im Nachlauf | 0 | - |
| 0x144C01 | Otto Partikelfilter Drucksensor, Bank 2, Plausibilität: Druck zu hoch im Nachlauf | 0 | - |
| 0x144D01 | Otto Partikelfilter Drucksensor, Bank 1, Plausibilität: Druckgradient zu hoch (Signal springt / Wackelkontakt) | 0 | - |
| 0x144E01 | Otto Partikelfilter Drucksensor, Bank 2, Plausibilität: Druckgradient zu hoch (Signal springt / Wackelkontakt) | 0 | - |
| 0x144F01 | Otto Partikelfilter Drucksensor, Bank 1, Versorgungsspannung: unplausibel (zu hoch) | 0 | - |
| 0x144F02 | Otto Partikelfilter Drucksensor, Bank 1, Versorgungsspannung: unplausibel (zu niedrig) | 0 | - |
| 0x145001 | Otto Partikelfilter Drucksensor, Bank 2, Versorgungsspannung: unplausibel (zu hoch) | 0 | - |
| 0x145002 | Otto Partikelfilter Drucksensor, Bank 2, Versorgungsspannung: unplausibel (zu niedrig) | 0 | - |
| 0x145301 | Otto Partikelfilter Drucksensor, Bank 1, Drucksensorschlauch: Schlauchanschlüsse vertauscht, diagnostiziert am Ende des Fahrzyklus | 0 | - |
| 0x145401 | Otto Partikelfilter Drucksensor, Bank 2, Drucksensorschlauch: Schlauchanschlüsse vertauscht, diagnostiziert am Ende des Fahrzyklus | 0 | - |
| 0x145501 | Otto Partikelfilter Drucksensor vor OPF, Bank 1, Drucksensorsschlauch: nicht angeschlossen/abgefallen | 0 | - |
| 0x145601 | Otto Partikelfilter Drucksensor vor OPF, Bank 2, Drucksensorsschlauch: nicht angeschlossen/abgefallen | 0 | - |
| 0x145708 | Otto Partikelfilter, Bank 1, leistungsreduzierter Betrieb: Warnung, wg. kritischer Differenzdruck zwischen OPF | 0 | - |
| 0x145808 | Otto Partikelfilter, Bank 2, leistungsreduzierter Betrieb: Warnung, wg. kritischer Differenzdruck zwischen OPF | 0 | - |
| 0x145908 | Otto Partikelfilter, Bank 1, leistungsreduzierter Betrieb: Fehler, wg. kritischer Differenzdruck zwischen OPF | 0 | - |
| 0x145A08 | Otto Partikelfilter, Bank 2, leistungsreduzierter Betrieb: Fehler, wg. kritischer Differenzdruck zwischen OPF | 0 | - |
| 0x145B08 | Otto Partikelfilter, Bank 1, leistungsreduzierter Betrieb: Warnung, wg. kritischer Rußbeladung im OPF | 0 | - |
| 0x145C08 | Otto Partikelfilter, Bank 2, leistungsreduzierter Betrieb: Warnung, wg. kritischer Rußbeladung im OPF | 0 | - |
| 0x145D08 | Otto Partikelfilter, Bank 1, leistungsreduzierter Betrieb: Fehler, wg. kritischer Rußbeladung im OPF | 0 | - |
| 0x145E08 | Otto Partikelfilter, Bank 2, leistungsreduzierter Betrieb: Fehler, wg. kritischer Rußbeladung im OPF | 0 | - |
| 0x145F08 | Otto Partikelfilter, Bank 1, kritsch überlastet von Ruß und Asche | 0 | - |
| 0x146008 | Otto Partikelfilter, Bank 2, kritsch überlastet von Ruß und Asche | 0 | - |
| 0x146108 | Otto Partikelfilter, Bank 1, überlastet von Ruß und Asche | 0 | - |
| 0x146208 | Otto Partikelfilter, Bank 2, überlastet von Ruß und Asche | 0 | - |
| 0x146308 | Otto Partikelfilter, Bank 1, kritisch überlastet von Ruß und Asche mit der Anforderung Partikelfilter muss getauscht werden | 0 | - |
| 0x146408 | Otto Partikelfilter, Bank 2, kritisch überlastet von Ruß und Asche mit der Anforderung Partikelfilter muss getauscht werden | 0 | - |
| 0x146508 | Otto Partikelfilter, Bank 1, kritisch überlastet von Asche innerhalb von nächsten Service mit der Anforderung, dass Partikelfilter muss präventiv getauscht werden | 0 | - |
| 0x146608 | Otto Partikelfilter, Bank 2, kritisch überlastet von Asche innerhalb von nächsten Service mit der Anforderung, dass Partikelfilter muss präventiv getauscht werden | 0 | - |
| 0x146708 | Otto Partikelfilter, Bank 1: Partikelfilter ausgebaut | 0 | - |
| 0x146808 | Otto Partikelfilter, Bank 2: Partikelfilter ausgebaut | 0 | - |
| 0x150102 | Zündung, Zylinder 1: Brenndauer zu kurz | 0 | - |
| 0x150202 | Zündung, Zylinder 2: Brenndauer zu kurz | 0 | - |
| 0x150302 | Zündung, Zylinder 3: Brenndauer zu kurz | 0 | - |
| 0x150402 | Zündung, Zylinder 4: Brenndauer zu kurz | 0 | - |
| 0x150502 | Zündung, Zylinder 5: Brenndauer zu kurz | 0 | - |
| 0x150602 | Zündung, Zylinder 6: Brenndauer zu kurz | 0 | - |
| 0x150702 | Zündung, Zylinder 7: Brenndauer zu kurz | 0 | - |
| 0x150802 | Zündung, Zylinder 8: Brenndauer zu kurz | 0 | - |
| 0x150902 | Zündung, Zylinder 9: Brenndauer zu kurz | 0 | - |
| 0x150A02 | Zündung, Zylinder 10: Brenndauer zu kurz | 0 | - |
| 0x150B02 | Zündung, Zylinder 11: Brenndauer zu kurz | 0 | - |
| 0x150C02 | Zündung, Zylinder 12: Brenndauer zu kurz | 0 | - |
| 0x151001 | Zündwinkelverstellung im Leerlauf, Kaltstart: Zündwinkel zu früh | 0 | - |
| 0x151100 | Zündwinkelverstellung in Teillast, Kaltstart | 0 | - |
| 0x151101 | Zündwinkelverstellung in Teillast, Kaltstart: Zündwinkel zu früh | 0 | - |
| 0x151200 | Zündwinkelverstellung 2 im Leerlauf, Kaltstart | 0 | - |
| 0x151201 | Zündwinkelverstellung 2 im Leerlauf, Kaltstart: Zündwinkel zu früh | 0 | - |
| 0x151300 | Zündwinkelverstellung 2 in Teillast, Kaltstart | 0 | - |
| 0x151301 | Zündwinkelverstellung 2 in Teillast, Kaltstart: Zündwinkel zu früh | 0 | - |
| 0x152008 | Zündkreis, Versorgungsspannung: Bankausfall oder Motorausfall | 0 | - |
| 0x152108 | Superklopfen, Zylinder 1: Einspritzungsabschaltung | 0 | - |
| 0x152208 | Superklopfen, Zylinder 2: Einspritzungsabschaltung | 0 | - |
| 0x152308 | Superklopfen, Zylinder 3: Einspritzungsabschaltung | 0 | - |
| 0x152408 | Superklopfen, Zylinder 4: Einspritzungsabschaltung | 0 | - |
| 0x152508 | Superklopfen, Zylinder 5: Einspritzungsabschaltung | 0 | - |
| 0x152608 | Superklopfen, Zylinder 6: Einspritzungsabschaltung | 0 | - |
| 0x152708 | Superklopfen, Zylinder 7: Einspritzungsabschaltung | 0 | - |
| 0x152808 | Superklopfen, Zylinder 8: Einspritzungsabschaltung | 0 | - |
| 0x152908 | Superklopfen, Zylinder 9: Einspritzungsabschaltung | 0 | - |
| 0x152A08 | Superklopfen, Zylinder 10: Einspritzungsabschaltung | 0 | - |
| 0x152B08 | Superklopfen, Zylinder 11: Einspritzungsabschaltung | 0 | - |
| 0x152C08 | Superklopfen, Zylinder 12: Einspritzungsabschaltung | 0 | - |
| 0x156101 | Zündspule Zylinder 1, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156201 | Zündspule Zylinder 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156301 | Zündspule Zylinder 3, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156401 | Zündspule Zylinder 4, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156501 | Zündspule Zylinder 5, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156601 | Zündspule Zylinder 6, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156701 | Zündspule Zylinder 7, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156801 | Zündspule Zylinder 8, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156901 | Zündspule Zylinder 9, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156A01 | Zündspule Zylinder 10, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156B01 | Zündspule Zylinder 11, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156C01 | Zündspule Zylinder 12, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x160001 | Kurbelwellensensor, Signal: fehlt | 0 | - |
| 0x160002 | Kurbelwellensensor, Signal: unplausibel | 0 | - |
| 0x160101 | Kurbelwellensensor, Synchronisation: Fehlfunktion | 0 | - |
| 0x160201 | Kurbelwellensensorsignal, Zahnfehler: Zähnezahl falsch | 0 | - |
| 0x160301 | Kurbelwellensensorsignal, Lückenfehler: Zahnzeit unplausibel | 0 | - |
| 0x160402 | Kurbelwellensensor, Segmentadaption: Grenzwert überschritten | 0 | - |
| 0x162001 | Einlassnockenwellensensor, Synchronisation: Fehlfunktion | 0 | - |
| 0x162101 | Einlassnockenwellensensor, elektrisch: Signal fehlt | 0 | - |
| 0x162201 | Einlassnockenwellensensor, Funktion: Segmentzeitfehler | 0 | - |
| 0x162301 | Einlassnockenwellensensor 2, Synchronisation: Fehlfunktion | 0 | - |
| 0x162401 | Einlassnockenwellensensor 2, elektrisch: Signal fehlt | 0 | - |
| 0x162501 | Einlassnockenwellensensor 2, Funktion: Segmentzeitfehler | 0 | - |
| 0x163101 | Auslassnockenwellensensor, Synchronisation: Fehlfunktion | 0 | - |
| 0x163201 | Auslassnockenwellensensor, elektrisch: Signal fehlt | 0 | - |
| 0x163301 | Auslassnockenwellensensor, Funktion: Segmentzeitfehler | 0 | - |
| 0x163401 | Auslassnockenwellensensor 2, Synchronisation: Fehlfunktion | 0 | - |
| 0x163501 | Auslassnockenwellensensor 2, elektrisch: Signal fehlt | 0 | - |
| 0x163601 | Auslassnockenwellensensor 2, Funktion: Segmentzeitfehler | 0 | - |
| 0x168001 | Klopfsensor 1, Signal: Motorgeräusch über Grenzwert | 0 | - |
| 0x168002 | Klopfsensor 1, Signal: Motorgeräusch unter Grenzwert | 0 | - |
| 0x168008 | Klopfsensor 1, Signal: unplausibel | 0 | - |
| 0x168101 | Klopfsensor 2, Signal: Motorgeräusch über Grenzwert | 0 | - |
| 0x168102 | Klopfsensor 2, Signal: Motorgeräusch unter Grenzwert | 0 | - |
| 0x168108 | Klopfsensor 2, Signal: unplausibel | 0 | - |
| 0x168201 | Klopfsensor 3, Signal: Motorgeräusch über Grenzwert | 0 | - |
| 0x168202 | Klopfsensor 3, Signal: Motorgeräusch unter Grenzwert oder Leitungsunterbrechung | 0 | - |
| 0x168208 | Klopfsensor 3, Signal: unplausibel | 0 | - |
| 0x168301 | Klopfsensor 4, Signal: Motorgeräusch über Grenzwert | 0 | - |
| 0x168302 | Klopfsensor 4, Signal: Motorgeräusch unter Grenzwert oder Leitungsunterbrechung | 0 | - |
| 0x168308 | Klopfsensor 4, Signal: unplausibel | 0 | - |
| 0x168401 | Klopfsensor 5, Signal: Motorgeräusch über Grenzwert | 0 | - |
| 0x168402 | Klopfsensor 5, Signal: Motorgeräusch unter Grenzwert | 0 | - |
| 0x168408 | Klopfsensor 5, Signal: unplausibel | 0 | - |
| 0x168501 | Klopfsensor 6, Signal: Motorgeräusch über Grenzwert | 0 | - |
| 0x168502 | Klopfsensor 6, Signal: Motorgeräusch unter Grenzwert | 0 | - |
| 0x168508 | Klopfsensor 6, Signal: unplausibel | 0 | - |
| 0x170301 | Sekundärluftpumpe, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x170302 | Sekundärluftpumpe, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x170304 | Sekundärluftpumpe, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x170401 | Differenzdrucksensor, Sekundärluft, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x170402 | Differenzdrucksensor, Sekundärluft, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x170404 | Differenzdrucksensor, Sekundärluft, elektrisch: Leitungsunterbrechung | 0 | - |
| 0x170501 | Differenzdrucksensor 2, Sekundärluft, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x170502 | Differenzdrucksensor 2, Sekundärluft, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x170504 | Differenzdrucksensor 2, Sekundärluft, elektrisch: Leitungsunterbrechung | 0 | - |
| 0x170604 | Differenzdrucksensor, Sekundärluft, Initialisierung: Druck außerhalb gültigem Bereich | 0 | - |
| 0x170608 | Differenzdrucksensor, Sekundärluft, Initialisierung: Druckdifferenz zwischen zwei Fahrzyklen unplausibel | 0 | - |
| 0x170704 | Differenzdrucksensor 2, Sekundärluft, Initialisierung: Druck außerhalb gültigem Bereich | 0 | - |
| 0x170708 | Differenzdrucksensor 2, Sekundärluft, Initialisierung: Druckdifferenz zwischen zwei Fahrzyklen unplausibel | 0 | - |
| 0x170808 | Sekundärluftleitung: Leistung Sekundärluftpumpe zu gering | 0 | - |
| 0x170908 | Sekundärluftleitung 2: Leistung Sekundärluftpumpe zu gering | 0 | - |
| 0x170A08 | Sekundärluftleitung: Luftmassenstrom zu gering | 0 | - |
| 0x170B08 | Sekundärluftleitung 2: Luftmassenstrom zu gering | 0 | - |
| 0x170C08 | Sekundärluftleitung: Undichtigkeit erkannt | 0 | - |
| 0x170D08 | Sekundärluftleitung 2: Undichtigkeit erkannt | 0 | - |
| 0x174208 | Sekundärluftventil: klemmt geschlossen | 0 | - |
| 0x174308 | Sekundärluftventil 2: klemmt geschlossen | 0 | - |
| 0x174408 | Sekundärluftventil: klemmt offen | 0 | - |
| 0x174508 | Sekundärluftventil 2: klemmt offen | 0 | - |
| 0x180001 | Katalysator: Wirkungsgrad unterhalb Grenzwert | 0 | - |
| 0x180002 | Katalysator: defekt | 0 | - |
| 0x180008 | Katalysator: Wirkungsgrad unterhalb Grenzwert (nicht validiert) | 0 | - |
| 0x180101 | Katalysator 2: Wirkungsgrad unterhalb Grenzwert | 0 | - |
| 0x180102 | Katalysator 2: defekt | 0 | - |
| 0x180108 | Katalysator 2: Wirkungsgrad unterhalb Grenzwert (nicht validiert) | 0 | - |
| 0x190001 | DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x190002 | DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x190004 | DMTL-Magnetventil, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x190201 | Tankentlüftungs- und Spülluftsystem, Feinleck: Leckage größer 1,0 mm | 0 | - |
| 0x190302 | Tankentlüftungs- und Spülluftsystem, Feinstleck: Leckage größer 0,5 mm | 0 | - |
| 0x190401 | DMTL, Systemfehler: Pumpenstrom zu groß bei Referenzmessung | 0 | - |
| 0x190402 | DMTL, Systemfehler: Pumpenstrom zu klein bei Referenzmessung | 0 | - |
| 0x190404 | DMTL, Systemfehler: Abbruch wegen Stromschwankungen bei Referenzmessung | 0 | - |
| 0x190408 | DMTL, Systemfehler: Pumpenstrom bei Ventilprüfung erreicht Grenzwert | 0 | - |
| 0x190501 | DMTL, Heizung, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x190502 | DMTL, Heizung, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x190504 | DMTL, Heizung, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x190601 | DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x190702 | DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x190704 | DMTL-Leckdiagnosepumpe, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x190802 | DMTL, Systemfehler: Pumpenstrom zu klein bei Referenzmessung | 0 | - |
| 0x190904 | DMTL, Systemfehler: Abbruch wegen Stromschwankungen bei Referenzmessung | 0 | - |
| 0x190A08 | DMTL, Systemfehler: Pumpenstrom bei Ventilprüfung erreicht Grenzwert | 0 | - |
| 0x190F04 | Tankentlüftungssystem: Fehlfunktion Bandende | 0 | - |
| 0x190F08 | Tankentlüftungssystem: Fehlfunktion | 0 | - |
| 0x191001 | Tankentlüftungsventil, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x191002 | Tankentlüftungsventil, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x191004 | Tankentlüftungsventil, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x191F00 | Entlüftung zwischen Tank und AKF | 0 | - |
| 0x191F02 | Entlüftung zwischen Tank und AKF: blockiert | 0 | - |
| 0x191F08 | Entlüftung zwischen Tank und AKF: blockiert | 0 | - |
| 0x193001 | Tankfüllstandssensor, links, Signal: Kurzschluss nach Plus oder Leitungsunterbrechung | 1 | - |
| 0x193002 | Tankfüllstandssensor, links, Signal: Kurzschluss nach Masse | 1 | - |
| 0x193008 | Tankfüllstandssensor, links, Signal: CAN Wert unplausibel | 1 | - |
| 0x193101 | Tankfüllstandssensor, rechts, Signal: Kurzschluss nach Plus oder Leitungsunterbrechung | 1 | - |
| 0x193102 | Tankfüllstandssensor, rechts, Signal: Kurzschluss nach Masse | 1 | - |
| 0x193108 | Tankfüllstandssensor, rechts, Signal: CAN Wert unplausibel | 1 | - |
| 0x193208 | Tankfüllstand, Plausibilität: unplausibel zu Verbrauchswert | 0 | - |
| 0x1A2001 | Elektrolüfter, Ansteuerungsleitung: Kurzschluss nach Plus | 0 | - |
| 0x1A2002 | Elektrolüfter, Ansteuerungsleitung: Kurzschluss nach Masse | 0 | - |
| 0x1A2004 | Elektrolüfter, Ansteuerungsleitung: Leitungsunterbrechung | 0 | - |
| 0x1A2108 | Elektrolüfter, Eigendiagnose Stufe 1: leichter Lüfterfehler | 0 | - |
| 0x1A2308 | Elektrolüfter, Eigendiagnose Stufe 2: Lüfterfehler mit potentieller Gefährdung für den Lüfter | 0 | - |
| 0x1A2408 | Elektrolüfter, Eigendiagnose Stufe 3: Lüfterfehler mit Motorfunktionseinschränkung | 0 | - |
| 0x1A2508 | Elektrolüfter, Eigendiagnose Stufe 4: schwerer Lüfterfehler | 0 | - |
| 0x1A2601 | Abschaltrelais Elektrolüfter, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x1A2602 | Abschaltrelais Elektrolüfter, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x1A2604 | Abschaltrelais Elektrolüfter, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x1B0004 | Fahrzeuggeschwindigkeit, Signal: fehlt | 0 | - |
| 0x1B0108 | Fahrzeuggeschwindigkeit, Plausibilität: Signal unplausibel | 0 | - |
| 0x1B0204 | Fahrzeuggeschwindigkeit, Plausibilität: Geschwindigkeit unplausibel oder CAN-Bus Kommunikation gestört | 1 | - |
| 0x1B0301 | Fahrzeuggeschwindigkeit, Plausibilität: Geschwindigkeit zu niedrig bei niedrigem Lastzustand | 1 | - |
| 0x1B0401 | Fahrzeuggeschwindigkeit, Signaländerung: unplausibel | 1 | - |
| 0x1B0501 | Fahrzeuggeschwindigkeit, Signal: festliegend auf Null | 1 | - |
| 0x1B0601 | Fahrzeuggeschwindigkeit, Signal: festliegend | 1 | - |
| 0x1B0701 | Fahrzeuggeschwindigkeit, Plausibilität: Geschwindigkeit zu hoch | 1 | - |
| 0x1B0808 | Fahrzeuggeschwindigkeit, Plausibilität: Geschwindigkeitssignal unplausibel | 0 | - |
| 0x1B0B01 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/links, Signaländerung: unplausibel | 1 | - |
| 0x1B0C01 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/rechts, Signaländerung: unplausibel | 1 | - |
| 0x1B0D01 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/links, Signaländerung: unplausibel | 1 | - |
| 0x1B0E01 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/rechts, Signaländerung: unplausibel | 1 | - |
| 0x1B2002 | EWS Manipulationsschutz: kein Startwert programmiert | 0 | - |
| 0x1B2008 | EWS Manipulationsschutz: Antwort unplausibel | 0 | - |
| 0x1B2101 | Schnittstelle EWS-DME: Hardwarefehler | 0 | - |
| 0x1B2102 | Schnittstelle EWS-DME: Framefehler | 0 | - |
| 0x1B2104 | Schnittstelle EWS-DME: Zeitüberschreitung | 0 | - |
| 0x1B2108 | Schnittstelle EWS-DME: Prüfsummenfehler | 0 | - |
| 0x1B2201 | DME, interner Fehler, EWS-Daten: keine verfügbare Speichermöglichkeit | 0 | - |
| 0x1B2202 | DME, interner Fehler, EWS-Daten: Fehlerfreischaltcodeablage | 0 | - |
| 0x1B2204 | DME, interner Fehler, EWS-Daten: Startwert zerstört/ 2- aus 3-Auswahl fehlgeschlagen | 0 | - |
| 0x1B2208 | DME, interner Fehler, EWS-Daten: Prüfsummenfehler | 0 | - |
| 0x1B2302 | FA-CAN, Botschaft (EWS Dienst DME1/DDE1, 0x5C0): Framefehler | 1 | - |
| 0x1B2304 | FA-CAN, Botschaft (EWS Dienst DME1/DDE1, 0x5C0): fehlt | 1 | - |
| 0x1B2401 | FlexRay, Botschaft (EWS Response Master, 251.0.8): Typfehler | 1 | - |
| 0x1B2501 | FlexRay, Botschaft (EWS Response Master, 251.0.8): fehlt | 1 | - |
| 0x1B2601 | FlexRay, Botschaft (EWS Challenge Slave, 251.4.8): Typfehler | 1 | - |
| 0x1B2701 | FlexRay, Botschaft (EWS Response Master, 251.0.8): Framefehler | 1 | - |
| 0x1B2A01 | DME-Sperrung, Slave: EWS nicht freigeschalten | 0 | - |
| 0x1B5001 | Überwachung Klemme 15: Wake-up-Leitung Kurzschluss nach Plus | 0 | - |
| 0x1B5002 | Überwachung Klemme 15: Wake-up-Leitung Kurzschluss nach Masse | 0 | - |
| 0x1B5004 | Überwachung Klemme 15: Botschaft vom CAS fehlt oder fehlerhaft | 0 | - |
| 0x1B5008 | Überwachung Klemme 15: Signal Wake-up-Leitung unplausibel zur Botschaft CAS Klemmenstatus | 0 | - |
| 0x1B5101 | Klemme 15_3, Leitung vom CAS, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x1B5102 | Klemme 15_3, Leitung vom CAS, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x1B9104 | Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi unplausibel im Motorlauf/Nachlauf | 0 | - |
| 0x1B9208 | Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi unplausibel im Wake-up | 0 | - |
| 0x1B9308 | Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi unplausibel im Motorlauf | 0 | - |
| 0x1B9408 | Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi unplausibel im Nachlauf | 0 | - |
| 0x1B9508 | Motorabstellzeit, Plausibilität: Zeit zu kurz in Korrelation zu Motorkühlmittel-Abkühlung | 0 | - |
| 0x1B9608 | Motorabstellzeit, Plausibilität: Zeit zu lang in Korrelation zu Motorkühlmittel-Abkühlung | 0 | - |
| 0x1BAF08 | Fahrpedalmodul - Bremspedal, Vergleich: Pedalwerte zueinander unplausibel | 0 | - |
| 0x1BD401 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/links, elektrisch: Kurzschluss nach Plus | 1 | - |
| 0x1BD402 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/links, elektrisch: Kurzschluss nach Masse | 1 | - |
| 0x1BD404 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/links, elektrisch: Leitungsunterbrechung | 1 | - |
| 0x1BD408 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/links, elektrisch: Fehlfunktion | 0 | - |
| 0x1BD501 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/links, elektrisch: Kurzschluss nach Plus | 1 | - |
| 0x1BD502 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/links, elektrisch: Kurzschluss nach Masse | 1 | - |
| 0x1BD504 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/links, elektrisch: Leitungsunterbrechung | 1 | - |
| 0x1BD508 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/links, elektrisch: Fehlfunktion | 0 | - |
| 0x1BD601 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/rechts, elektrisch: Kurzschluss nach Plus | 1 | - |
| 0x1BD602 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/rechts, elektrisch: Kurzschluss nach Masse | 1 | - |
| 0x1BD604 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/rechts, elektrisch: Leitungsunterbrechung | 1 | - |
| 0x1BD608 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/rechts, elektrisch: Fehlfunktion | 0 | - |
| 0x1BD701 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/rechts, elektrisch: Kurzschluss nach Plus | 1 | - |
| 0x1BD702 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/rechts, elektrisch: Kurzschluss nach Masse | 1 | - |
| 0x1BD704 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/rechts, elektrisch: Leitungsunterbrechung | 1 | - |
| 0x1BD708 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/rechts, elektrisch: Fehlfunktion | 0 | - |
| 0x1C3204 | Motoröldruckschalter: Leitungsunterbrechung oder Schalter klemmt | 0 | - |
| 0x1C4002 | Thermischer Ölniveausensor: Niveau zu niedrig | 0 | - |
| 0x1C4102 | Motorölniveau: zu niedrig | 0 | - |
| 0x1C5001 | Ölzustandssensor: Temperaturmessung | 0 | - |
| 0x1C5002 | Ölzustandssensor: Niveaumessung | 0 | - |
| 0x1C5004 | Ölzustandssensor: Kommunikationsfehler | 0 | - |
| 0x1C5008 | Ölzustandssensor: Permittivitätsfehler | 0 | - |
| 0x1C5104 | Ölzustandssensor, Kommunikation: keine Kommunikation | 0 | - |
| 0x1D2008 | Kennfeldthermostat: klemmt offen | 0 | - |
| 0x1D2204 | Kennfeldthermostat, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x1D2301 | Kennfeldthermostat, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x1D2401 | Kennfeldthermostat, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x1D2402 | Kennfeldthermostat, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x1D2404 | Kennfeldthermostat, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x1D3701 | Schaltzeitpunkt: Anpassung | 1 | - |
| 0x1D3901 | EGS, Signalüberwachung (Turbinendrehzahl): ungültiger Signalinhalt | 1 | - |
| 0x1D3A01 | EGS, Signalüberwachung (Drehzahl Abtrieb): ungültiger Signalinhalt | 1 | - |
| 0x1D3B01 | EGS, Signalüberwachung (Ganginformation): ungültiger Signalinhalt | 1 | - |
| 0x1D3C01 | EGS, Signalüberwachung (Status Schaltvorgang): ungültiger Signalinhalt | 1 | - |
| 0x1E0001 | Leerlaufregelung: Drehzahl zu hoch | 0 | - |
| 0x1E0002 | Leerlaufregelung: Drehzahl zu niedrig | 0 | - |
| 0x1E0101 | Leerlaufregelung, Kaltstart: Drehzahl zu hoch | 0 | - |
| 0x1E0102 | Leerlaufregelung, Kaltstart: Drehzahl zu niedrig | 0 | - |
| 0x1E0308 | Leerlaufregelung, Plausibilität, Kaltstart: Drehzahl unplausibel | 0 | - |
| 0x1E5008 | Drehmomentüberwachung: Plausibilität | 0 | - |
| 0x1E5108 | Motordrehmoment, Anforderung über CAN: nicht erfüllbar | 0 | - |
| 0x1E5201 | Drehzahlbegrenzung bei stehendem Fahrzeug: Leerlaufdrehzahl zu lange zu hoch | 0 | - |
| 0x1F0001 | DME, interner Fehler, RAM: RAM-Baustein | 0 | - |
| 0x1F0002 | DME, interner Fehler, RAM: Sicherheitsrechner RAM | 0 | - |
| 0x1F0101 | DME, interner Fehler, Prüfsumme: Bootsoftware | 0 | - |
| 0x1F0102 | DME, interner Fehler, Prüfsumme: Applikationssoftware | 0 | - |
| 0x1F0104 | DME, interner Fehler, Prüfsumme: Datenbereich | 0 | - |
| 0x1F0201 | DME, interner Fehler, NVMY-Prüfsumme: NVMY-Überprüfung | 0 | - |
| 0x1F0304 | DME, interner Fehler, Klopfsensorbaustein: SPI-Kommunikation gestört | 0 | - |
| 0x1F0404 | DME, interner Fehler, Mehrfachendstufenbaustein: SPI-Kommunikation gestört | 0 | - |
| 0x1F0502 | Klemme 15N vom CAS, Signal: nicht geschaltet | 0 | - |
| 0x1F0601 | Klemme 15N vom CAS, Schaltverzögerung: schaltet zu spät | 0 | - |
| 0x1F0801 | Warm Reset Diagnose: Geplanter Software Reset | 0 | - |
| 0x1F0802 | Warm Reset Diagnose: unerwünschter Software Reset | 0 | - |
| 0x1F0804 | Warm Reset Diagnose: Power On Reset | 0 | - |
| 0x1F0808 | Warm Reset Diagnose: Hardware Reset | 0 | - |
| 0x1F1004 | Master/Slave Kohärenz: Programmstände ungleich | 0 | - |
| 0x1F1008 | Master/Slave Kohärenz: Datenstände ungleich | 0 | - |
| 0x1F1108 | Master/Slave Umschaltung: maximale Anzahl Umschaltungen überschritten | 0 | - |
| 0x1F1208 | Master/Slave Erkennung: Erkennung nicht möglich | 0 | - |
| 0x1F1308 | Master/Slave NVMY Status: Speichern oder Auslesen des Status nicht möglich | 0 | - |
| 0x1F1508 | Master/Slave Erkennung: Erkennung nicht möglich | 0 | - |
| 0x1F1601 | DME, Nachlauf: unvollständiges Herunterfahren erkannt | 0 | - |
| 0x1F2004 | Kodierung fehlt: Kodierdaten im EEPROM fehlerhaft | 0 | - |
| 0x1F2008 | Kodierung fehlt: keine Kodierung nach Programmierung | 0 | - |
| 0x1F2104 | Falscher Datensatz: CAN Timeout | 0 | - |
| 0x1F2108 | Falscher Datensatz: Variantenüberwachung | 0 | - |
| 0x1F2201 | Injektoren Gruppe 1 oder DME, interner Fehler: Initialisierungsfehler | 0 | - |
| 0x1F2202 | Injektoren Gruppe 1 oder DME, interner Fehler: Leitungsunterbrechung | 0 | - |
| 0x1F2204 | Injektoren Gruppe 1 oder DME, interner Fehler: Entladungsfehler | 0 | - |
| 0x1F2301 | Injektoren Gruppe 2 oder DME, interner Fehler: Initialisierungsfehler | 0 | - |
| 0x1F2302 | Injektoren Gruppe 2 oder DME, interner Fehler: Leitungsunterbrechung | 0 | - |
| 0x1F2304 | Injektoren Gruppe 2 oder DME, interner Fehler: Entladungsfehler | 0 | - |
| 0x1F2401 | Injektoren Gruppe 3 oder DME, interner Fehler: Initialisierungsfehler | 0 | - |
| 0x1F2402 | Injektoren Gruppe 3 oder DME, interner Fehler: Leitungsunterbrechung | 0 | - |
| 0x1F2404 | Injektoren Gruppe 3 oder DME, interner Fehler: Entladungsfehler | 0 | - |
| 0x1F2501 | Injektoren Gruppe 4 oder DME, interner Fehler: Initialisierungsfehler | 0 | - |
| 0x1F2502 | Injektoren Gruppe 4 oder DME, interner Fehler: Leitungsunterbrechung | 0 | - |
| 0x1F2504 | Injektoren Gruppe 4 oder DME, interner Fehler: Entladungsfehler | 0 | - |
| 0x1F2601 | Kodierung: falsche Variante kodiert | 0 | - |
| 0x1F2602 | Kodierung: Variante fehlt | 0 | - |
| 0x1F2701 | Kodierung: Fehler beim Schreiben der Variante | 0 | - |
| 0x1F2702 | Kodierung: Variantenprüfung fehlerhaft | 0 | - |
| 0x1F2704 | Kodierung: Unplausible Variante | 0 | - |
| 0x1F2801 | DME, Software: Programm ungültig | 0 | - |
| 0x1F2802 | DME, Software: Daten ungültig | 0 | - |
| 0x1F2804 | DME, Software: Programm und Daten ungültig | 0 | - |
| 0x1F2901 | DME Slave, Software: Programm ungültig | 0 | - |
| 0x1F2902 | DME Slave, Software: Daten ungültig | 0 | - |
| 0x1F2904 | DME Slave, Software: Programm und Daten ungültig | 0 | - |
| 0x1F3008 | DME, interner Fehler, Fahrpedalmodul: Spannungsversorgung Pedalwertgeber 1 | 0 | - |
| 0x1F3108 | DME, interner Fehler, Fahrpedalmodul: Spannungsversorgung Pedalwertgeber 2 | 0 | - |
| 0x1F4001 | Startautomatik, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x1F4002 | Startautomatik, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x1F4004 | Startautomatik, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x1F4A04 | Entlastungsrelais für Zündung und Einspritzung: nicht abgefallen | 0 | - |
| 0x1F4A08 | Entlastungsrelais für Zündung und Einspritzung: nicht angezogen | 0 | - |
| 0x1F4B08 | Entlastungsrelais für Zündung und Einspritzung, Schaltverzögerung: schaltet zu spät | 0 | - |
| 0x1F4C01 | Relais Mengensteuerventil: Kurzschluss nach Plus | 0 | - |
| 0x1F4C02 | Relais Mengensteuerventil: Kurzschluss nach Masse | 0 | - |
| 0x1F4C04 | Relais Mengensteuerventil: Leitungsunterbrechung | 0 | - |
| 0x1F4E04 | Relais 2 Zündung und Injektoren: nicht abgefallen | 0 | - |
| 0x1F4E08 | Relais 2 Zündung und Injektoren: nicht angezogen | 0 | - |
| 0x1F4F08 | Relais 2 Zündung und Injektoren, Schaltverzögerung: schaltet zu spät | 0 | - |
| 0x1F5001 | DME, interner Fehler, Innentemperatursensor, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x1F5002 | DME, interner Fehler, Innentemperatursensor, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x200004 | DME, interner Fehler, Überwachung Fahrgeschwindigkeitsregelung: LDM Überwachung | 0 | - |
| 0x200108 | DME, interner Fehler, Überwachung Motordrehzahl: Fehlfunktion | 0 | - |
| 0x200208 | DME, interner Fehler, Überwachung Drehzahlbegrenzung: Fehlfunktion | 0 | - |
| 0x200308 | DME, interner Fehler, Überwachung Fahrpedalmodul: Fehlfunktion | 0 | - |
| 0x200404 | DME, interner Fehler, Überwachung Leerlaufregelung: Anforderung I-Anteil unplausibel | 0 | - |
| 0x200408 | DME, interner Fehler, Überwachung Leerlaufregelung: Anforderung PD-Anteil unplausibel | 0 | - |
| 0x200500 | DME, interner Fehler, Überwachung externe Momentenanforderung: Sendesignale unplausibel | 0 | - |
| 0x200501 | DME, interner Fehler, Überwachung externe Momentenanforderung: Anforderung MSR unplausibel | 0 | - |
| 0x200502 | DME, interner Fehler, Überwachung externe Momentenanforderung: Anforderung ICM unplausibel | 0 | - |
| 0x200504 | DME, interner Fehler, Überwachung externe Momentenanforderung: Sendesignale unplausibel | 0 | - |
| 0x200508 | DME, interner Fehler, Überwachung externe Momentenanforderung: Anforderung EGS unplausibel | 0 | - |
| 0x200601 | DME, interner Fehler, Überwachung Sollmoment: maximales Kupplungsmoment unplausibel | 0 | - |
| 0x200602 | DME, interner Fehler, Überwachung Sollmoment: minimales Kupplungsmoment unplausibel | 0 | - |
| 0x200604 | DME, interner Fehler, Überwachung Sollmoment: Verlustmoment unplausibel | 0 | - |
| 0x200708 | DME, interner Fehler, Überwachung Istmoment: Signal unplausibel | 0 | - |
| 0x200808 | DME, interner Fehler, Überwachung Hardware: Fehlfunktion | 0 | - |
| 0x200908 | DME, interner Fehler, Überwachung Kraftstoffmasse: Luftmasse zu Kraftstoffmasse unplausibel | 0 | - |
| 0x200A08 | DME, interner Fehler, Überwachung Luftpfad: Drosselklappenwinkel unplausibel | 0 | - |
| 0x200C01 | DME, interner Fehler: ROM-Fehler | 0 | - |
| 0x200C02 | DME, interner Fehler: RAM-Fehler | 0 | - |
| 0x200C04 | DME, interner Fehler: Prozessor-Fehler | 0 | - |
| 0x200C08 | DME, interner Fehler: Hauptprozessor-Fehler | 0 | - |
| 0x200D01 | DME, interner Fehler, Überwachung Sendesignale: Radmomente unplausibel | 0 | - |
| 0x200D02 | DME, interner Fehler, Überwachung Sendesignale: Fahrerwunsch unplausibel | 0 | - |
| 0x200D04 | DME, interner Fehler, Überwachung Sendesignale: Fahrpedalwert unplausibel | 0 | - |
| 0x200D08 | DME, interner Fehler, Überwachung Sendesignale: CAN-Fehler | 0 | - |
| 0x20A001 | Kühlmittelpumpe für Ladeluftkühler, Drehzahlabweichung: außerhalb der Toleranz | 0 | - |
| 0x20A101 | Kühlmittelpumpe für Ladeluftkühler, Abschaltung: interne Temperatur zu hoch | 0 | - |
| 0x20A102 | Kühlmittelpumpe für Ladeluftkühler, Abschaltung: Überspannung | 0 | - |
| 0x20A104 | Kühlmittelpumpe für Ladeluftkühler, Abschaltung: Überstrom | 0 | - |
| 0x20A201 | Kühlmittelpumpe für Ladeluftkühler, leistungsreduzierter Betrieb: Trockenlauf | 0 | - |
| 0x20A202 | Kühlmittelpumpe für Ladeluftkühler, leistungsreduzierter Betrieb: Unterspannung | 0 | - |
| 0x20A204 | Kühlmittelpumpe für Ladeluftkühler, leistungsreduzierter Betrieb: Temperaturgrenze 1 überschritten | 0 | - |
| 0x20A208 | Kühlmittelpumpe für Ladeluftkühler, leistungsreduzierter Betrieb: Temperaturgrenze 2 überschritten | 0 | - |
| 0x20A408 | Kühlmittelpumpe für Ladeluftkühler, Plausibilität Kommunikation: keine Spannung am Notlauf-Eingang der Pumpe | 0 | - |
| 0x20A501 | Turbolader-Kühlmittelpumpe, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x20A502 | Turbolader-Kühlmittelpumpe, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x20A504 | Turbolader-Kühlmittelpumpe, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x20A608 | Turbolader-Kühlmittelpumpe, Ansteuerung: Pumpe blockiert | 0 | - |
| 0x20E102 | Kurbelgehäuseentlüftung, Entlüftungsschlauch: nicht angeschlossen/defekt | 0 | - |
| 0x20E202 | Kurbelgehäuseentlüftung 2, Entlüftungsschlauch: nicht angeschlossen/defekt | 0 | - |
| 0x210201 | Generator, elektrisch: Fehlfunktion | 0 | - |
| 0x210301 | Generator, Plausibilität, elektrisch: berechnet | 0 | - |
| 0x210401 | Generator, Temperatur: Übertemperatur | 1 | - |
| 0x210501 | Generator, Plausibilität, Temperatur: Übertemperatur berechnet | 1 | - |
| 0x210601 | Generator, mechanisch: Fehlfunktion | 0 | - |
| 0x210701 | Generator, Regler: Typ falsch | 0 | - |
| 0x210801 | Generator: Typ falsch | 0 | - |
| 0x210901 | Generator, Kommunikation: keine Kommunikation | 0 | - |
| 0x213301 | Powermanagement, Überspannung: Überspannung erkannt | 1 | - |
| 0x213401 | Powermanagement, Unterspannung: Unterspannung erkannt | 1 | - |
| 0x213501 | Powermanagement, Batterieüberwachung: Tiefentladung | 1 | - |
| 0x213601 | Powermanagement, Ruhestromüberwachung: Ruhestromverletzung | 0 | - |
| 0x213701 | Powermanagement: Batterieloser Betrieb | 0 | - |
| 0x213801 | Batterie, Transport: Batterie auf Transport geschädigt | 0 | - |
| 0x213901 | Verbraucherreduzierung: aktiv | 1 | - |
| 0x213A01 | Batterie, Transport, Überwachung: Batterie auf Transport entladen | 0 | - |
| 0x213B01 | Powermanagement, Batteriezustandserkennung: Batteriedefekt | 0 | - |
| 0x213C01 | Powermanagement, Batteriezustandserkennung: Tiefentladung | 0 | - |
| 0x213E01 | Bordnetzspannung: Arbeitsbereich, Spannung zu hoch | 0 | - |
| 0x213F01 | Bordnetzspannung: Arbeitsbereich, Spannung zu niedrig | 0 | - |
| 0x215401 | Intelligenter Batteriesensor, Plausibilität: Spannung unplausibel | 0 | - |
| 0x215501 | Intelligenter Batteriesensor, Plausibilität: Strom unplausibel | 0 | - |
| 0x215601 | Intelligenter Batteriesensor, Plausibilität: Temperatur unplausibel | 0 | - |
| 0x215701 | Intelligenter Batteriesensor: Eigendiagnose, Systemfehler | 0 | - |
| 0x215801 | Intelligenter Batteriesensor: Wake-up-Leitung, elektrisch, Kurzschluss nach Plus oder Masse | 0 | - |
| 0x215901 | Intelligenter Batteriesensor: Kompabilität, Version nicht plausibel | 0 | - |
| 0x215A01 | Intelligenter Batteriesensor: Wake-up-Leitung, elektrisch, Leitungsunterbrechung | 0 | - |
| 0x215B01 | LIN, Kommunikation (Intelligenter Batteriesensor): Zusatzstatus Framefehler | 0 | - |
| 0x230004 | Kommunikation Einschlafkoordinator: Zeitüberschreitung | 0 | - |
| 0x230008 | Kommunikation Einschlafkoordinator: Nachricht unplausibel | 0 | - |
| 0x230102 | Botschaft (Kopplung 1 Slave Antrieb): Aliveprüfung | 1 | - |
| 0x230104 | Botschaft (Kopplung 1 Slave Antrieb): fehlt | 1 | - |
| 0x230108 | Botschaft (Kopplung 1 Slave Antrieb): Prüfsumme falsch | 1 | - |
| 0x230202 | Botschaft (Kopplung 2 Slave Antrieb): Aliveprüfung | 1 | - |
| 0x230204 | Botschaft (Kopplung 2 Slave Antrieb): fehlt | 1 | - |
| 0x230208 | Botschaft (Kopplung 2 Slave Antrieb): Prüfsumme falsch | 1 | - |
| 0x230302 | Botschaft (Kopplung 3 Slave Antrieb): Aliveprüfung | 1 | - |
| 0x230304 | Botschaft (Kopplung 3 Slave Antrieb): fehlt | 1 | - |
| 0x230308 | Botschaft (Kopplung 3 Slave Antrieb): Prüfsumme falsch | 1 | - |
| 0x230402 | Botschaft (Kopplung 4 Slave Antrieb): Aliveprüfung | 1 | - |
| 0x230404 | Botschaft (Kopplung 4 Slave Antrieb): fehlt | 1 | - |
| 0x230408 | Botschaft (Kopplung 4 Slave Antrieb): Prüfsumme falsch | 1 | - |
| 0x231101 | Fehlerspeichereintrag: nur zum Test | 0 | - |
| 0x231201 | Fehlerspeichereintrag: nur zum Test | 0 | - |
| 0x231301 | Netzwerkfehler: nur zum Test | 0 | - |
| 0x231401 | Netzwerkfehler: nur zum Test | 0 | - |
| 0x231501 | Fehlerspeichereintrag: Sendepuffer voll | 0 | - |
| 0x231502 | Fehlerspeichereintrag: Senden fehlgeschlagen | 0 | - |
| 0x231701 | CAN-Kommunikation bei Unterspannung: Kommunikationsfehler zur EGS | 1 | - |
| 0x231801 | CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an FA-CAN | 1 | - |
| 0x231802 | CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an A-CAN | 1 | - |
| 0x231804 | CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an FA-CAN und A-CAN | 1 | - |
| 0x231901 | CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an FA-CAN | 1 | - |
| 0x231902 | CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an A-CAN | 1 | - |
| 0x231904 | CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an FA-CAN und A-CAN | 1 | - |
| 0x231F04 | A- / FA-CAN, Botschaften (Getriebe): fehlen | 0 | - |
| 0x232004 | A- / FA-CAN, Botschaften (Getriebe): fehlen | 0 | - |
| 0x233004 | FA-CAN, Botschaft (OBD Sensor Diagnosestatus, 0x5E0): fehlt, Sender Kombi | 1 | - |
| 0x233804 | FA-CAN, Botschaft (OBD Sensor Diagnosestatus, 0x5E0): fehlt | 1 | - |
| 0x238102 | Botschaft (Kopplung 1 Master Antrieb): Aliveprüfung | 1 | - |
| 0x238104 | Botschaft (Kopplung 1 Master Antrieb): fehlt | 1 | - |
| 0x238108 | Botschaft (Kopplung 1 Master Antrieb): Prüfsumme falsch | 1 | - |
| 0x238202 | Botschaft (Kopplung 2 Master Antrieb): Aliveprüfung | 1 | - |
| 0x238204 | Botschaft (Kopplung 2 Master Antrieb): fehlt | 1 | - |
| 0x238208 | Botschaft (Kopplung 2 Master Antrieb): Prüfsumme falsch | 1 | - |
| 0x238302 | Botschaft (Kopplung 3 Master Antrieb): Aliveprüfung | 1 | - |
| 0x238304 | Botschaft (Kopplung 3 Master Antrieb): fehlt | 1 | - |
| 0x238308 | Botschaft (Kopplung 3 Master Antrieb): Prüfsumme falsch | 1 | - |
| 0x238402 | Botschaft (Kopplung 4 Master Antrieb): Aliveprüfung | 1 | - |
| 0x238404 | Botschaft (Kopplung 4 Master Antrieb): fehlt | 1 | - |
| 0x238408 | Botschaft (Kopplung 4 Master Antrieb): Prüfsumme falsch | 1 | - |
| 0xCD8408 | FlexRay Bus: Controller-Reset durchgeführt | 0 | - |
| 0xCD840A | FA-CAN Bus: Kommunikationsfehler | 0 | - |
| 0xCD8420 | FlexRay Bus: Kommunikationsfehler | 0 | - |
| 0xCD8486 | A-CAN Bus: Kommunikationsfehler | 1 | - |
| 0xCD8487 | FlexRay Controller, Startup: Fehlfunktion | 1 | - |
| 0xCD8508 | FlexRay Bus: Hardware defekt | 1 | - |
| 0xCD8601 | FlexRay Controller, Startup: Synchronisationsfehler | 1 | - |
| 0xCD8801 | FlexRay Controller, Startup: maximale Startupzeit überschritten | 1 | - |
| 0xCD8B02 | FlexRay, Botschaft (Diagnose OBD 1, 263.3.4): Aliveprüfung | 0 | - |
| 0xCD8B04 | FlexRay, Botschaft (Diagnose OBD 1, 263.3.4): fehlt | 1 | - |
| 0xCD8E01 | LIN  Bus, Kommunikationsfehler: Kurzschluss | 0 | - |
| 0xCD8E02 | LIN  Bus, Kommunikationsfehler: Leitungsunterbrechung | 0 | - |
| 0xCD8F01 | LIN, Kommunikation (intelligenter Batteriesensor): fehlt | 0 | - |
| 0xCD9001 | LIN, Kommunikation (Ladeluft-Kühlmittelpumpe): fehlt | 0 | - |
| 0xCD9002 | LIN, Kommunikation (Ladeluft-Kühlmittelpumpe): fehlerhaft | 0 | - |
| 0xCD9101 | Batterieladeeinheit, LIN Kommunikation: Zeitüberschreitung | 0 | - |
| 0xCD9102 | Batterieladeeinheit, LIN Kommunikation: ungültige Botschaft | 0 | - |
| 0xCD9201 | LIN, Kommunikation (Kühlerjalousie): fehlt | 0 | - |
| 0xCD9202 | LIN, Kommunikation (Kühlerjalousie): ungültiger Botschaftsinhalt | 0 | - |
| 0xCD9304 | Bitserielle Datenschnittstelle, Signal: Kommunikationsfehler | 0 | - |
| 0xCD9402 | FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): Aliveprüfung | 1 | - |
| 0xCD9404 | FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): fehlt | 1 | - |
| 0xCD9408 | FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): Prüfsumme falsch | 1 | - |
| 0xCD9430 | CAN-Kommunikation bei Unterspannung: Kommunikationsfehler zur EGS | 1 | - |
| 0xCD9431 | CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an FA-CAN | 1 | - |
| 0xCD9432 | CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an A-CAN | 1 | - |
| 0xCD9433 | CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an FA-CAN und A-CAN | 1 | - |
| 0xCD9434 | CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an FA-CAN | 1 | - |
| 0xCD9435 | CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an A-CAN | 1 | - |
| 0xCD9436 | CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an FA-CAN und A-CAN | 1 | - |
| 0xCD9502 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung / Soll Verteilung Längsmoment Vorderachse Hinterachse, 43.1.4): Aliveprüfung | 1 | - |
| 0xCD9504 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung / Soll Verteilung Längsmoment Vorderachse Hinterachse, 43.1.4): fehlt | 1 | - |
| 0xCD9508 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung / Soll Verteilung Längsmoment Vorderachse Hinterachse, 43.1.4): Prüfsumme falsch | 1 | - |
| 0xCD9602 | FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): Aliveprüfung | 1 | - |
| 0xCD9604 | FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): fehlt | 1 | - |
| 0xCD9608 | FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): Prüfsumme falsch | 1 | - |
| 0xCD9702 | FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): Aliveprüfung | 1 | - |
| 0xCD9704 | FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): fehlt | 1 | - |
| 0xCD9708 | FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): Prüfsumme falsch | 1 | - |
| 0xCD9804 | FlexRay, Botschaft (Einheiten BN2020, 252.0.4 ): fehlt | 1 | - |
| 0xCD9902 | FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): Aliveprüfung | 1 | - |
| 0xCD9904 | FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): fehlt | 1 | - |
| 0xCD9908 | FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): Prüfsumme falsch | 1 | - |
| 0xCD9A02 | FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): Aliveprüfung | 1 | - |
| 0xCD9A04 | FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): fehlt | 1 | - |
| 0xCD9A08 | FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): Prüfsumme falsch | 1 | - |
| 0xCD9B02 | FlexRay, Botschaft (Ist Drehzahl Rad, 46.1.2): Aliveprüfung | 1 | - |
| 0xCD9B04 | FlexRay, Botschaft (Ist Drehzahl Rad, 46.1.2): fehlt | 1 | - |
| 0xCD9B08 | FlexRay, Botschaft (Ist Drehzahl Rad, 46.1.2): Prüfsumme falsch | 1 | - |
| 0xCD9C02 | FlexRay, Botschaft (Ist Lenkwinkel Fahrer, 59.0.2): Aliveprüfung | 1 | - |
| 0xCD9C04 | FlexRay, Botschaft (Ist Lenkwinkel Fahrer, 59.0.2): fehlt | 1 | - |
| 0xCD9C08 | FlexRay, Botschaft (Ist Lenkwinkel Fahrer, 59.0.2): Prüfsumme falsch | 1 | - |
| 0xCD9D02 | FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): Aliveprüfung | 1 | - |
| 0xCD9D04 | FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): fehlt | 1 | - |
| 0xCD9D08 | FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): Prüfsumme falsch | 1 | - |
| 0xCD9E02 | FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): Aliveprüfung | 1 | - |
| 0xCD9E04 | FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): fehlt | 1 | - |
| 0xCD9E08 | FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): Prüfsumme falsch | 1 | - |
| 0xCD9F02 | FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): Aliveprüfung | 1 | - |
| 0xCD9F04 | FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): fehlt | 1 | - |
| 0xCD9F08 | FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): Prüfsumme falsch | 1 | - |
| 0xCDA002 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): Aliveprüfung | 1 | - |
| 0xCDA004 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): fehlt | 1 | - |
| 0xCDA008 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): Prüfsumme falsch | 1 | - |
| 0xCDA104 | FlexRay, Botschaft (Neigung Fahrbahn, 56.1.2): fehlt | 1 | - |
| 0xCDA204 | FlexRay, Botschaft (Anforderung Leistung Elektrisch EPS, 234.0.2): fehlt | 1 | - |
| 0xCDA302 | FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): Aliveprüfung | 1 | - |
| 0xCDA304 | FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): fehlt | 1 | - |
| 0xCDA308 | FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): Prüfsumme falsch | 1 | - |
| 0xCDA524 | FA-CAN, Botschaft (Status Elektrische Kraftstoffpumpe, 0x335): fehlt | 1 | - |
| 0xCDA602 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Aliveprüfung | 1 | - |
| 0xCDA604 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): fehlt | 1 | - |
| 0xCDA608 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Prüfsumme falsch | 1 | - |
| 0xCDA702 | FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): Aliveprüfung | 1 | - |
| 0xCDA704 | FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): fehlt | 1 | - |
| 0xCDA708 | FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): Prüfsumme falsch | 1 | - |
| 0xCDA804 | FA-CAN, Botschaft (Relativzeit, 0x328): fehlt | 1 | - |
| 0xCDA904 | FA-CAN, Botschaft (Status Anhänger, 0x2E4): fehlt | 1 | - |
| 0xCDAC04 | FA-CAN, Botschaft (Status Getriebesteuergerät, 0x39A): fehlt | 1 | - |
| 0xCDAD04 | FA-CAN, Botschaft (Steuerung Crashabschaltung elektrische Kraftstoffpumpe, 0x135): fehlt | 1 | - |
| 0xCDAE04 | FA-CAN, Botschaft (Uhrzeit/Datum, 0x2F8): fehlt | 1 | - |
| 0xCDAF04 | FA-CAN, Botschaft (ZV und Klappenzustand, 0x2FC): fehlt | 1 | - |
| 0xCDB002 | FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Aliveprüfung | 1 | - |
| 0xCDB004 | FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): fehlt | 1 | - |
| 0xCDB008 | FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Prüfsumme falsch | 1 | - |
| 0xCDB102 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): Aliveprüfung | 1 | - |
| 0xCDB104 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): fehlt | 1 | - |
| 0xCDB108 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): Prüfsumme falsch | 1 | - |
| 0xCDB204 | FA-CAN, Botschaft (Außentemperatur, 0x2CA): fehlt | 1 | - |
| 0xCDB404 | FA-CAN, Botschaft (Fahrzeugzustand, 0x3A0): fehlt | 1 | - |
| 0xCDB504 | FA-CAN, Botschaft (Kilometerstand/Reichweite, 0x330): fehlt | 1 | - |
| 0xCDB602 | FA-CAN, Botschaft (Klemmen, 0x12F): Aliveprüfung | 1 | - |
| 0xCDB604 | FA-CAN, Botschaft (Klemmen, 0x12F): fehlt | 1 | - |
| 0xCDB608 | FA-CAN, Botschaft (Klemmen, 0x12F): Prüfsumme falsch | 1 | - |
| 0xCDB704 | FA-CAN, Botschaft (Nachlaufzeit Stromversorgung, 0x3BE): fehlt | 1 | - |
| 0xCDB804 | FA-CAN, Botschaft (Anforderung Klimaanlage, 0x2F9): fehlt | 1 | - |
| 0xCDB904 | FA-CAN, Botschaft (Diagnose OBD Getriebe, 0x396): fehlt | 1 | - |
| 0xCDBB02 | A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Aliveprüfung | 1 | - |
| 0xCDBB04 | A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): fehlt | 1 | - |
| 0xCDBB08 | A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Prüfsumme falsch | 1 | - |
| 0xCDBC04 | A-CAN, Botschaft (Anforderung Leistung Elektrisch PCU, 0x33F): fehlt | 1 | - |
| 0xCDBD04 | A-CAN, Botschaft (Status Energieerzeugung BN2, 0x2AF): fehlt | 1 | - |
| 0xCDBE02 | A-CAN, Botschaft (Anzeige Drehzahl Motor Dynamisierung, 0xF8): Aliveprüfung | 1 | - |
| 0xCDBE04 | A-CAN, Botschaft (Anzeige Drehzahl Motor Dynamisierung, 0xF8): fehlt | 1 | - |
| 0xCDBF04 | A-CAN, Botschaft (Status Getriebesteuergerät, 0x39A): fehlt | 1 | - |
| 0xCDC004 | A-CAN, Botschaft (Diagnose OBD Getriebe, 0x396): fehlt | 1 | - |
| 0xCDC102 | A-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Aliveprüfung | 1 | - |
| 0xCDC104 | A-CAN, Botschaft (Daten Getriebestrang, 0x1AF): fehlt | 1 | - |
| 0xCDC108 | A-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Prüfsumme falsch | 1 | - |
| 0xCDC202 | A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): Aliveprüfung | 1 | - |
| 0xCDC204 | A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): fehlt | 1 | - |
| 0xCDC208 | A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): Prüfsumme falsch | 1 | - |
| 0xCDC304 | A-CAN, Botschaft (Status Elektrische Kraftstoffpumpe, 0x335): fehlt | 1 | - |
| 0xCDC408 | FlexRay Bus: Controller-Reset durchgeführt | 0 | - |
| 0xCDC40A | FA-CAN Bus: Kommunikationsfehler | 0 | - |
| 0xCDC420 | FlexRay Bus: Kommunikationsfehler | 0 | - |
| 0xCDC487 | FlexRay Controller, Startup: Fehlfunktion | 0 | - |
| 0xCDC508 | FlexRay Bus: Hardware defekt | 1 | - |
| 0xCDC601 | FlexRay Controller, Startup: Synchronisationsfehler | 0 | - |
| 0xCDC801 | FlexRay Controller, Startup: maximale Startupzeit überschritten | 0 | - |
| 0xCDD402 | FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): Aliveprüfung | 1 | - |
| 0xCDD404 | FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): fehlt | 1 | - |
| 0xCDD408 | FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): Prüfsumme falsch | 1 | - |
| 0xCDD502 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung / Soll Verteilung Längsmoment Vorderachse Hinterachse, 43.1.4): Aliveprüfung | 1 | - |
| 0xCDD504 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung / Soll Verteilung Längsmoment Vorderachse Hinterachse, 43.1.4): fehlt | 1 | - |
| 0xCDD508 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung / Soll Verteilung Längsmoment Vorderachse Hinterachse, 43.1.4): Prüfsumme falsch | 1 | - |
| 0xCDD512 | FlexRay, Botschaft (Daten Antriebsstrang 2, 230.0.2): Aliveprüfung | 1 | - |
| 0xCDD513 | FlexRay, Botschaft (Daten Antriebsstrang 2, 230.0.2): fehlt | 1 | - |
| 0xCDD514 | FlexRay, Botschaft (Daten Antriebsstrang 2, 230.0.2): Prüfsumme falsch | 1 | - |
| 0xCDD602 | FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): Aliveprüfung | 1 | - |
| 0xCDD604 | FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): fehlt | 1 | - |
| 0xCDD608 | FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): Prüfsumme falsch | 1 | - |
| 0xCDD612 | FlexRay, Botschaft (Radmoment Antrieb 1, 41.3.4): Aliveprüfung | 1 | - |
| 0xCDD613 | FlexRay, Botschaft (Radmoment Antrieb 1, 41.3.4): fehlt | 1 | - |
| 0xCDD614 | FlexRay, Botschaft (Radmoment Antrieb 1, 41.3.4): Prüfsumme falsch | 1 | - |
| 0xCDD702 | FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): Aliveprüfung | 1 | - |
| 0xCDD704 | FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): fehlt | 1 | - |
| 0xCDD708 | FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): Prüfsumme falsch | 1 | - |
| 0xCDD712 | FlexRay, Botschaft (Radmoment Antrieb 4, 40.3.4): Aliveprüfung | 1 | - |
| 0xCDD713 | FlexRay, Botschaft (Radmoment Antrieb 4, 40.3.4): fehlt | 1 | - |
| 0xCDD714 | FlexRay, Botschaft (Radmoment Antrieb 4, 40.3.4): Prüfsumme falsch | 1 | - |
| 0xCDD902 | FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): Aliveprüfung | 1 | - |
| 0xCDD904 | FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): fehlt | 1 | - |
| 0xCDD908 | FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): Prüfsumme falsch | 1 | - |
| 0xCDDA02 | FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): Aliveprüfung | 1 | - |
| 0xCDDA04 | FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): fehlt | 1 | - |
| 0xCDDA08 | FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): Prüfsumme falsch | 1 | - |
| 0xCDDB02 | FlexRay, Botschaft (Ist Drehzahl Rad, 46.1.2): Aliveprüfung | 1 | - |
| 0xCDDB04 | FlexRay, Botschaft (Ist Drehzahl Rad, 46.1.2): fehlt | 1 | - |
| 0xCDDB08 | FlexRay, Botschaft (Ist Drehzahl Rad, 46.1.2): Prüfsumme falsch | 1 | - |
| 0xCDDC02 | FlexRay, Botschaft (Ist Lenkwinkel Fahrer, 59.0.2): Aliveprüfung | 1 | - |
| 0xCDDC04 | FlexRay, Botschaft (Ist Lenkwinkel Fahrer, 59.0.2): fehlt | 1 | - |
| 0xCDDC08 | FlexRay, Botschaft (Ist Lenkwinkel Fahrer, 59.0.2): Prüfsumme falsch | 1 | - |
| 0xCDDD02 | FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): Aliveprüfung | 1 | - |
| 0xCDDD04 | FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): fehlt | 1 | - |
| 0xCDDD08 | FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): Prüfsumme falsch | 1 | - |
| 0xCDDE02 | FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): Aliveprüfung | 1 | - |
| 0xCDDE04 | FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): fehlt | 1 | - |
| 0xCDDE08 | FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): Prüfsumme falsch | 1 | - |
| 0xCDDF02 | FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): Aliveprüfung | 1 | - |
| 0xCDDF04 | FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): fehlt | 1 | - |
| 0xCDDF08 | FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): Prüfsumme falsch | 1 | - |
| 0xCDE002 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): Aliveprüfung | 1 | - |
| 0xCDE004 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): fehlt | 1 | - |
| 0xCDE008 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): Prüfsumme falsch | 1 | - |
| 0xCDE104 | FlexRay, Botschaft (Neigung Fahrbahn, 56.1.2): fehlt | 1 | - |
| 0xCDE204 | FlexRay, Botschaft (Anforderung Leistung Elektrisch EPS, 234.0.2): fehlt | 1 | - |
| 0xCDE302 | FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): Aliveprüfung | 1 | - |
| 0xCDE304 | FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): fehlt | 1 | - |
| 0xCDE308 | FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): Prüfsumme falsch | 1 | - |
| 0xCDE602 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Aliveprüfung | 1 | - |
| 0xCDE604 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): fehlt | 1 | - |
| 0xCDE608 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Prüfsumme falsch | 1 | - |
| 0xCDE702 | FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): Aliveprüfung | 1 | - |
| 0xCDE704 | FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): fehlt | 1 | - |
| 0xCDE708 | FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): Prüfsumme falsch | 1 | - |
| 0xCDE804 | FA-CAN, Botschaft (Relativzeit, 0x328): fehlt | 1 | - |
| 0xCDE904 | FA-CAN, Botschaft (Status Anhänger, 0x2E4): fehlt | 1 | - |
| 0xCDEC04 | FA-CAN, Botschaft (Status Getriebesteuergerät, 0x39A): fehlt | 1 | - |
| 0xCDED04 | FA-CAN, Botschaft (Steuerung Crashabschaltung elektrische Kraftstoffpumpe, 0x135): fehlt | 1 | - |
| 0xCDEE04 | FA-CAN, Botschaft (Uhrzeit/Datum, 0x2F8): fehlt | 1 | - |
| 0xCDEF04 | FA-CAN, Botschaft (ZV und Klappenzustand, 0x2FC): fehlt | 1 | - |
| 0xCDF002 | FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Aliveprüfung | 1 | - |
| 0xCDF004 | FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): fehlt | 1 | - |
| 0xCDF008 | FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Prüfsumme falsch | 1 | - |
| 0xCDF102 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): Aliveprüfung | 1 | - |
| 0xCDF104 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): fehlt | 1 | - |
| 0xCDF108 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): Prüfsumme falsch | 1 | - |
| 0xCDF204 | FA-CAN, Botschaft (Außentemperatur, 0x2CA): fehlt | 1 | - |
| 0xCDF302 | FA-CAN, Botschaft (Daten Anzeige Getriebestrang, 0x3FD): Aliveprüfung | 1 | - |
| 0xCDF304 | FA-CAN, Botschaft (Daten Anzeige Getriebestrang, 0x3FD): fehlt | 1 | - |
| 0xCDF308 | FA-CAN, Botschaft (Daten Anzeige Getriebestrang, 0x3FD): Prüfsumme falsch | 1 | - |
| 0xCDF404 | FA-CAN, Botschaft (Fahrzeugzustand, 0x3A0): fehlt | 1 | - |
| 0xCDF504 | FA-CAN, Botschaft (Kilometerstand/Reichweite, 0x330): fehlt | 1 | - |
| 0xCDF602 | FA-CAN, Botschaft (Klemmen, 0x12F): Aliveprüfung | 1 | - |
| 0xCDF604 | FA-CAN, Botschaft (Klemmen, 0x12F): fehlt | 1 | - |
| 0xCDF608 | FA-CAN, Botschaft (Klemmen, 0x12F): Prüfsumme falsch | 1 | - |
| 0xCDF704 | FA-CAN, Botschaft (Nachlaufzeit Stromversorgung, 0x3BE): fehlt | 1 | - |
| 0xCDF804 | FA-CAN, Botschaft (Anforderung Klimaanlage, 0x2F9): fehlt | 1 | - |
| 0xCDF904 | FA-CAN, Botschaft (Diagnose OBD Getriebe, 0x396): fehlt | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 241 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x5800 | Zeit nach Start | s | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5801 | Umgebungsdruck | kPa | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5802 | Zustand Lambdaregelung Bank 1 | 0-n | - | 0xFF | _CNV_S_5_LACO_RANGE_300 | - | - | - |
| 0x5803 | Zustand Lambdaregelung Bank 2 | 0-n | - | 0xFF | _CNV_S_5_LACO_RANGE_300 | - | - | - |
| 0x5804 | Berechneter Lastwert | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5805 | Kühlmitteltemperatur OBD | °C | - | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0x5806 | Lambda Integrator Gruppe 1 | % | - | unsigned char | - | 0.78125 | 1.0 | -100.00000224 |
| 0x5807 | Lambda Adaption Summe mul. und add. Gruppe 1 | % | - | unsigned char | - | 0.78125 | 1.0 | -100.00000224 |
| 0x5808 | Lambda Integrator Gruppe 2 | % | - | unsigned char | - | 0.78125 | 1.0 | -100.00000224 |
| 0x5809 | Lambda Adaption Summe mul. und add. Gruppe 2 | % | - | unsigned char | - | 0.78125 | 1.0 | -100.00000224 |
| 0x580B | Saugrohrdruck | kPa | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x580C | Drehzahl | 1/min | - | unsigned char | - | 64.0 | 1.0 | 0.0 |
| 0x580D | Geschwindigkeit | km/h | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x580E | Zündzeitpunkt Zylinder 1 | ° KW | - | unsigned char | - | 0.5 | 1.0 | -64.0 |
| 0x580F | Ansauglufttemperatur | °C | - | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0x5810 | Luftdurchsatz OBD | g/s | - | unsigned char | - | 2.55999994 | 1.0 | 0.0 |
| 0x5811 | Motordrehzahl | 1/min | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x5812 | Luftmasse gemessen | kg/h | - | unsigned char | - | 8.0 | 1.0 | 0.0 |
| 0x5813 | Relative Last | % | - | signed char | - | 2.55999994 | 1.0 | 0.0 |
| 0x5814 | Fahrpedalwert | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5815 | Batteriespannung | V | - | unsigned char | - | 0.25600001 | 1.0 | 0.0 |
| 0x5816 | Lambda Setpoint | - | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 |
| 0x5817 | Umgebungstemperatur | °C | - | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0x5818 | Luftmasse gerechnet | mg/stroke | - | unsigned char | - | 5.44705868 | 1.0 | 0.0 |
| 0x5819 | Drehzahl OBD Byte | 1/min | - | unsigned char | - | 64.0 | 1.0 | 0.0 |
| 0x581A | Periodendauer Sensor Ansauglufttemperatur | µs | - | unsigned char | - | 256.0 | 1.0 | 0.0 |
| 0x581B | Spannung Drucksensor | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x581C | Rohwert Lufttemperatur | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x581D | Spannung Lufttemperatur | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x581E | Lufttemperatur Drosselklappe | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x581F | Motortemperatur | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x5820 | Kühlmitteltemperatur Kühlerausgang | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x5821 | Steuergeräte-Innentemperatur | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x5822 | (Motor)-Öltemperatur | °C | - | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0x5823 | Zeit Motor steht | min | - | unsigned char | - | 256.0 | 1.0 | 0.0 |
| 0x5824 | Umgebungstemperatur | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x5825 | Abstellzeit | min | - | unsigned char | - | 4.0 | 1.0 | 0.0 |
| 0x5826 | Drosselklappentemperatur | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x5827 | Lambdasondenheizung vor Katalysator Bank 1 | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5828 | Lambdasondenheizung vor Katalysator Bank 2 | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5829 | Lambdasondenheizung hinter Katalysator Bank 1 | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x582A | Lambdasondenheizung hinter Katalysator Bank 2 | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x582B | Drehmomenteingriff über CAN | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x582C | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 1 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x582D | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 2 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x582E | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 1 | - | - | unsigned char | - | 0.00390625 | 1.0 | 0.0 |
| 0x582F | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 2 | - | - | unsigned char | - | 0.00390625 | 1.0 | 0.0 |
| 0x5830 | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 1 | - | - | unsigned char | - | 0.004 | 1.0 | 0.0 |
| 0x5831 | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 2 | - | - | unsigned char | - | 0.004 | 1.0 | 0.0 |
| 0x5832 | Motor Status | 0-n | - | 0xFF | _CNV_S_6_RANGE_STAT_56 | - | - | - |
| 0x5833 | Umgebungstemperatur beim Start | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x5834 | Umgebungsdruck | hPa | - | unsigned char | - | 5.30664063 | 1.0 | 0.0 |
| 0x5835 | Herstellercode Generator 1 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5836 | Drehzahlgradient | 1/s | - | signed char | - | 32.0 | 1.0 | 0.0 |
| 0x5837 | Status OBD-I Fehler vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_11_EGCP_RANGE_249 | - | - | - |
| 0x5838 | Status OBD-I Fehler vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_11_EGCP_RANGE_249 | - | - | - |
| 0x5839 | Status Drosselklappe Notlauf | 0-n | - | 0xFF | _CNV_S_3_THRO_RANGE_891 | - | - | - |
| 0x583A | Ansauglufttemperatur beim Start | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x583B | Kraftstofftank Füllstand | l | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x583C | Spannung Kl. 87 | V | - | unsigned char | - | 0.10156249 | 1.0 | 0.0 |
| 0x583D | Resettyp | 0-n | - | 0xFF | _CNV_S_19_ECOP_RANGE_764 | - | - | - |
| 0x583E | Motordrehzahl bei Reset | 1/min | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x583F | Drosselklappe Sollwert | ° DK | - | unsigned char | - | 0.46682537 | 1.0 | 0.0 |
| 0x5840 | CPU Last bei Reset | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5841 | SG-Innentemperatur Rohwert | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5842 | Kennung Generatortyp Generator 1 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5843 | Versorgung FWG 1 | V | - | unsigned char | - | 0.0390625 | 1.0 | 0.0 |
| 0x5844 | Chiptemperatur Generator 1 | °C | - | unsigned char | - | 1.0 | 1.0 | -48.0 |
| 0x5845 | Spannung Lambdasonde vor Katalysator Bank 1 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5846 | Spannung Pedalwertgeber 1 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5847 | Spannung Pedalwertgeber 2 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5848 | Spannung Lambdasonde vor Katalysator Bank 2 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5849 | Spannung Lambdasonde hinter Katalysator Bank 1 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x584A | Spannung Kl. 15 Rohwert | V | - | unsigned char | - | 0.11294118 | 1.0 | 0.0 |
| 0x584B | Spannung Lambdasonde hinter Katalysator Bank 2 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x584D | korrigierter Sollwert Durchfluss Tankentlüftung | kg/h | - | unsigned char | - | 0.03125 | 1.0 | 0.0 |
| 0x584F | Höhe Gegendruck OPF  | hPa | - | unsigned char | - | 21.47483647 | 1.0 | 0.0 |
| 0x5850 | Spannung Motortemperatur | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5851 | Spannung Ansauglufttemperatur, Sensor | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5852 | Kühlmitteltemperatur Kühlerausgang Rohwert | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5853 | Spannung Kl.87 Rohwert | V | - | unsigned char | - | 0.11294118 | 1.0 | 0.0 |
| 0x5854 | Versorgung FWG 2 | V | - | unsigned char | - | 0.0390625 | 1.0 | 0.0 |
| 0x5855 | Mittelwert Bank 1 | % | - | signed char | - | 0.390625 | 1.0 | 0.0 |
| 0x5856 | Mittelwert Bank 2 | % | - | signed char | - | 0.390625 | 1.0 | 0.0 |
| 0x5857 | Erregerstrom Generator 1 | A | - | unsigned char | - | 0.125 | 1.0 | 0.0 |
| 0x5858 | Drosselklappe aktueller Wert | ° DK | - | unsigned char | - | 0.46682537 | 1.0 | 0.0 |
| 0x5859 | DMTL Strom Referenzleck | mA | - | unsigned char | - | 0.19531247 | 1.0 | 0.0 |
| 0x585A | DMTL Strom Grobleck | mA | - | unsigned char | - | 0.19531247 | 1.0 | 0.0 |
| 0x585B | DMTL Strom Diagnoseende | mA | - | unsigned char | - | 0.19531247 | 1.0 | 0.0 |
| 0x585C | Widerstand Lambdasonde hinter Katalysator Bank 1 | Ohm | - | unsigned char | - | 256.0 | 1.0 | 0.0 |
| 0x585D | Widerstand Lambdasonde hinter Katalysator Bank 2 | Ohm | - | unsigned char | - | 256.0 | 1.0 | 0.0 |
| 0x585E | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 1 | Ohm | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x585F | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 2 | Ohm | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5860 | Widerstand Lambdasonde vor Katalysator Bank 1 | Ohm | - | unsigned char | - | 64.0 | 1.0 | 0.0 |
| 0x5861 | Widerstand Lambdasonde vor Katalysator Bank 2 | Ohm | - | unsigned char | - | 64.0 | 1.0 | 0.0 |
| 0x5862 | Rußbeladung bei Leistungsbegrenzung OPF  | g | - | unsigned char | - | 1.0 | 64.00008031 | 0.0 |
| 0x5863 | untere Byte Widerstand Lambdasonde vor Katalysator Bank 1 | Ohm | - | unsigned char | - | 0.25 | 1.0 | 0.0 |
| 0x5864 | untere Byte Widerstand Lambdasonde vor Katalysator Bank 2 | Ohm | - | unsigned char | - | 0.25 | 1.0 | 0.0 |
| 0x5865 | Ölstand Mittelwert Langzeit | mm | - | unsigned char | - | 0.29296875 | 1.0 | 0.0 |
| 0x5866 | Füllstand Motoröl | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5867 | Kilometerstand | km | - | unsigned char | - | 2560.0 | 1.0 | 0.0 |
| 0x5869 | Status Standverbraucher registriert Teil 2 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x586A | Batteriespannung von IBS gemessen | V | - | unsigned char | - | 0.064 | 1.0 | 6.016 |
| 0x586B | Zeit mit Ruhestrom 80 - 200 mA | min | - | unsigned char | - | 14.9333334 | 1.0 | 0.0 |
| 0x586C | Zeit mit Ruhestrom 200 - 1000 mA | min | - | unsigned char | - | 14.9333334 | 1.0 | 0.0 |
| 0x586D | Zähler Erkennung schlechte Strasse | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x586E | Zeit mit Ruhestrom größer 1000 mA | min | - | unsigned char | - | 14.9333334 | 1.0 | 0.0 |
| 0x5870 | Spannung DME Umgebungsdruck | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5871 | Lambda-Sollwert Gruppe 1 | - | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 |
| 0x5872 | Reglerversion Generator 1 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5873 | Lambda-Sollwert Gruppe 2 | - | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 |
| 0x5874 | Spannung Strommessung DMTL | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5875 | Sollwert Motormoment | Nm | - | unsigned char | - | 4.0 | 1.0 | 0.0 |
| 0x5876 | Raildruck OBD (High-Byte von FUP für OBD) | kPa | - | unsigned char | - | 2560.0 | 1.0 | 0.0 |
| 0x5877 | Raildruck OBD (Low-Byte von FUP für OBD) | kPa | - | unsigned char | - | 10.0 | 1.0 | 0.0 |
| 0x5878 | Lambdaverschiebung Rückführregler 1 | - | - | signed char | - | 0.00097656 | 1.0 | 0.0 |
| 0x5879 | Lambdaverschiebung Rückführregler 2 | - | - | signed char | - | 0.00097656 | 1.0 | 0.0 |
| 0x587A | Status FGR | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x587B | Gemessene Spannung vom DCDC Wandler gegen Masse | V | - | unsigned char | - | 0.25 | 1.0 | 0.0 |
| 0x587C | Status Motorsteuerung | 0-n | - | 0xFF | _CNV_S_7_RANGE_ECU__54 | - | - | - |
| 0x587D | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_261 | - | - | - |
| 0x587E | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_261 | - | - | - |
| 0x587F | Tastverhältnis E-Lüfter | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5880 | Ansteuerung untere Luftklappe | 0/1 | - | 0x01 | - | - | - | - |
| 0x5881 | berechneter Gang | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5882 | Motortemperatur beim Start | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x5883 | Spannung Klopfwerte Zylinder 1 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5884 | Rückgelesener Erregergrenzstrom Generator 1 | A | - | unsigned char | - | 0.125 | 1.0 | 0.0 |
| 0x5885 | Spannung Klopfwerte Zylinder 3 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5886 | Spannung Klopfwerte Zylinder 6 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5887 | Auslastungsgrad Generator 1 | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5888 | Spannung Klopfwerte Zylinder 4 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5889 | Lambda-Istwert Gruppe 1 | - | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 |
| 0x588A | Lambda-Istwert Gruppe 2 | - | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 |
| 0x588B | Zeit seit Startende | s | - | unsigned char | - | 256.0 | 1.0 | 0.0 |
| 0x588C | Keramiktemperatur Lambdasonde vor Katalysator Bank 1 | °C | - | signed char | - | 16.0 | 1.0 | 0.0 |
| 0x588D | aktuelle Zeit DMTL Leckmessung | s | - | unsigned char | - | 25.60000038 | 1.0 | 0.0 |
| 0x588E | Pumpenstrom bei DMTL Pumpenprüfung | mA | - | unsigned char | - | 0.19531247 | 1.0 | 0.0 |
| 0x588F | Keramiktemperatur Lambdasonde vor Katalysator Bank 2 | °C | - | signed char | - | 16.0 | 1.0 | 0.0 |
| 0x5890 | OPF Drucksensor Druck Master /Slave  | hPa | - | unsigned char | - | 21.47483647 | 1.0 | 0.0 |
| 0x5891 | Momentanforderung an der Kupplung | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x5892 | OPF Temperatursensor Temperaturistwert 1Master / 2Slave | °C | - | unsigned char | - | 16.0 | 1.0 | -273.15 |
| 0x5893 | Drehmomentabfall schnell bei Gangwechsel | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x5894 | Symptom Lambdasondenheizung vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_253 | - | - | - |
| 0x5895 | Symptom Lambdasondenheizung vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_253 | - | - | - |
| 0x5896 | Abgastemperatur hinter Katalysator Bank 1 | °C | - | signed char | - | 16.0 | 1.0 | 0.0 |
| 0x5897 | Abgastemperatur hinter Katalysator Bank 2 | °C | - | signed char | - | 16.0 | 1.0 | 0.0 |
| 0x5898 | Generator Sollspannung | V | - | unsigned char | - | 0.1 | 1.0 | 0.0 |
| 0x589B | Spannungsoffset Signalpfad CJ120 1 | V | - | signed char | - | 0.00488278 | 1.0 | -0.00000361 |
| 0x589C | Spannungsoffset Signalpfad CJ120 2 | V | - | signed char | - | 0.00488278 | 1.0 | -0.00000361 |
| 0x589D | Abweichung Lambdasonde zu Lambdamodellwert Überwachung | mg/stroke | - | unsigned char | - | 2.71050191 | 1.0 | 0.0 |
| 0x589F | Motordrehzahl | 1/min | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x58A0 | Batterietemperatur | °C | - | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x58A1 | Entladung während Ruhestromverletzung | Ah | - | unsigned char | - | 0.49803922 | 1.0 | 0.0 |
| 0x58A2 | Wasserpumpe Stromaufnahme | A | - | unsigned char | - | 0.2 | 1.0 | 0.0 |
| 0x58A3 | relative Wasserpumpenspannung | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58A4 | Status Generator | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58A5 | Generatorauslastung | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58A6 | Generatorspannung | V | - | unsigned char | - | 0.1 | 1.0 | 0.0 |
| 0x58A7 | Abstellzeit in min | min | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58A8 | Motorabstellzeit | min | - | unsigned char | - | 4.0 | 1.0 | 0.0 |
| 0x58A9 | Resetzähler Rechnerüberwachung: alter Wert | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58AA | Fehlercode Rechnerüberwachung: alter Wert | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58AB | Abweichung DK-Potentiometer 1 und Modellwert | ° DK | - | unsigned char | - | 0.46682537 | 1.0 | 0.0 |
| 0x58AC | Abweichung DK-Potentiometer 2 und Modellwert | ° DK | - | unsigned char | - | 0.46682537 | 1.0 | 0.0 |
| 0x58AD | Pedalwertgeber 1 | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58AE | Periodendauer Luftmasse | µs | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x58AF | Kraftstoff Anforderung an Pumpe | l/h | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58B0 | DK-Adaptionsschritt | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58B1 | Funkenbrenndauer Zylinder 1 (Slave 7) | ms | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 |
| 0x58B2 | Funkenbrenndauer Zylinder 5 (Slave 11) | ms | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 |
| 0x58B3 | Funkenbrenndauer Zylinder 3 (Slave 9) | ms | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 |
| 0x58B4 | Funkenbrenndauer Zylinder 6 (Slave 12) | ms | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 |
| 0x58B5 | Funkenbrenndauer Zylinder 2 (Slave 8) | ms | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 |
| 0x58B6 | Funkenbrenndauer Zylinder 4 (Slave 10) | ms | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 |
| 0x58B7 | Bremsdruck | bar | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58B8 | Drehzahl Überwachung | 1/min | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x58B9 | Pedalwert Überwachung | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58BA | eingespritze Kraftstoffmasse | l/h | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58BB | PWM Kraftstoffpumpe | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58BC | Luftmasse Überwachung | mg/stroke | - | unsigned char | - | 2.71050191 | 1.0 | 0.0 |
| 0x58BD | Statusbyte externe Momentenanforderung 3 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58BE | Aschebeladung bei Leistungsbegrenzung OPF  | g | - | unsigned char | - | 1.0 | 64.00008031 | 0.0 |
| 0x58BF | Statusbyte vom Error Memory Management | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58C0 | Motordrehzahl Ersatzwert Überwachung | 1/min | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x58C1 | Laufunruhe Segmentzeit | µs | - | unsigned char | - | 7812.21826172 | 1.0 | 0.0 |
| 0x58C2 | Statusbyte MFF-Monitoring | mg/stroke | - | unsigned char | - | 2.71050191 | 1.0 | 0.0 |
| 0x58C3 | Statusbyte ISC-Monitoring | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58C4 | Statusbyte CRU-Monitoring | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58C5 | Drehzahl Überwachung (resetsicher) | 1/min | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x58C6 | Status Einspritzventile (resetsicher) | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58C7 | LL-Solldrehzahlabweichung Überwachung | 1/min | - | signed char | - | 32.0 | 1.0 | 0.0 |
| 0x58C8 | I-Anteil Momentdifferenz Überwachung und Modell | Nm | - | signed char | - | 2.0 | 1.0 | 0.0 |
| 0x58C9 | I-Anteil LL passive Rampe aktiv | 0/1 | - | 0x01 | - | - | - | - |
| 0x58CA | PD-Anteil langsam Leerlaufregelung | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x58CB | PD-Anteil schnell Leerlaufregelung | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x58CC | Verlustmoment Überwachung | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x58CD | Grund für Leistungsbegrenzung von OPF  | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58CE | Carrierbyte Schalterstati | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58CF | Motormoment Sollwert Überwachung | Nm | - | unsigned char | - | 4.0 | 1.0 | 0.0 |
| 0x58D0 | Motormoment Istwert Überwachung | Nm | - | unsigned char | - | 4.0 | 1.0 | 0.0 |
| 0x58D1 | Moment aktueller Wert | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x58D2 | Sollposition obere Luftklappe in Grad | ° | - | unsigned char | - | 256.0 | 1.0 | -95.0 |
| 0x58D3 | Istposition obere Luftklappe in Grad | ° | - | unsigned char | - | 256.0 | 1.0 | -95.0 |
| 0x58D4 | Abweichung maximales Moment an Kupplung Überwachung | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x58D6 | Abweichung minimales Moment an Kupplung Überwachung | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x58D7 | Spannung des Ansauglufttemperatursensors im Laderstrang | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x58D9 | Fehlercode Rechnerüberwachung: aktueller Wert | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58DA | Resetzähler Rechnerüberwachung: aktueller Wert | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58DB | Inhalt Statusbyte 1 Drehzahlüberwachung (resetsicher) | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58DC | Inhalt Statusbyte 2 Drehzahlüberwachung (resetsicher) | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58DD | ATL upstream | kPa | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58DE | Spannung für Drucksensor vor Drosselklappe | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x58E4 | Betriebsart Istwert | 0-n | - | 0xFF | _CNV_S_5__CNV_S_5_D_608 | - | - | - |
| 0x58E5 | Lastwert für Aussetzererkennung | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58E6 | Nulllastwert für Aussetzererkennung | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58E7 | Spannung Pedalwertgeber 1 Überwachung | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x58E8 | Spannung Pedalwertgeber 2 Überwachung | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x58E9 | Wasserpumpe Spannung | V | - | unsigned char | - | 0.1 | 1.0 | 0.0 |
| 0x58EA | Wasserpumpe Drehzahl | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58EB | Wasserpumpe Drehzahl Soll-Ist-Differenz | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58EC | Wasserpumpe Temperatur Elektronik | °C | - | unsigned char | - | 1.0 | 1.0 | -50.0 |
| 0x58ED | gemittelter Raildruck Bank 1 | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x58EF | Raildruck Bank 1 | hPa | - | unsigned char | - | 1358.5177002 | 1.0 | 0.0 |
| 0x58F0 | Dummy für Fehlerspecherfehlbedatung | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58F1 | DME - Losnummer | 0-n | - | 0xFF | _CNV_S_13_RANGE_STAT_839 | - | - | - |
| 0x58F2 | PWM-Signal des Mengensteuerventils | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58F3 | Kraftstoffdruck vor Mengensteuerventil | hPa | - | unsigned char | - | 42.45375824 | 1.0 | 0.0 |
| 0x58F4 | Spannung für Kraftstoffdrucksensor vor Mengensteuerventil | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x58F5 | Eingangssignal Rückführregler 1 | V | - | signed char | - | 0.00488278 | 1.0 | -0.00000361 |
| 0x58F6 | Eingangssignal Rückführregler 2 | V | - | signed char | - | 0.00488278 | 1.0 | -0.00000361 |
| 0x58F7 | Laufunruhe Segmentzeit | µs | - | unsigned char | - | 30.51647758 | 1.0 | 0.0 |
| 0x58F8 | Segmentadaption Laufunruhe Zyl. 5 (Slave 11) | % | - | signed char | - | 0.06103515 | 1.0 | 0.00000008 |
| 0x58F9 | Segmentadaption Laufunruhe Zyl. 3 (Slave 9) | % | - | signed char | - | 0.06103515 | 1.0 | 0.00000008 |
| 0x58FA | Beladungsgrad Aktivkohlefilter TEV- Funktionstest | - | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 |
| 0x58FB | Zähler Drehzahlerhöhungen TEV- Funktionstest | cyc | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58FC | Katheizen aktiv | 0/1 | - | 0x01 | - | - | - | - |
| 0x58FD | Statusbit STATE_LV_ERR_COM_MON_1_2 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58FE | Statusbyte externe Momentenanforderung | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58FF | Umweltbedingung unbekannt | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-ibs-deak"></a>
### IBS_DEAK

Dimensions: 10 rows × 2 columns

| NR | TEXT |
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

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 5 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
| F_UWB_SATZ | 3 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1223 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERKLASSE |
| --- | --- | --- | --- |
| 0x021200 | Transportmodus: aktiv | 0 | - |
| 0x021300 | Transportmodus: aktiv | 0 | - |
| 0x100201 | Drosselklappe, schwergängig: zu langsam | 0 | - |
| 0x100301 | DME, interner Fehler, Ansteuerung Drosselklappe: Fehlfunktion | 0 | - |
| 0x100401 | Drosselklappe, schwergängig: zu langsam | 0 | - |
| 0x100501 | Drosselklappe 2, schwergängig: zu langsam | 0 | - |
| 0x100601 | Drosselklappe, Ansteuerung: Fehlfunktion | 0 | - |
| 0x100701 | DME, interner Fehler, Ansteuerung Drosselklappe 2: Fehlfunktion | 0 | - |
| 0x100801 | Drosselklappe, Funktion: klemmt | 0 | - |
| 0x100901 | Drosselklappe 2, Funktion: klemmt | 0 | - |
| 0x100A02 | Drosselklappe, Drosselklappenpotenziometer 1 und 2: Doppelfehler | 0 | - |
| 0x100B02 | Drosselklappe 2, Drosselklappenpotenziometer 1 und 2: Doppelfehler | 0 | - |
| 0x100C08 | Drosselklappe, Drosselklappenpotenziometer 1: Signal unplausibel zur Luftmasse | 0 | - |
| 0x100D08 | Drosselklappe 2, Drosselklappenpotenziometer 1: Signal unplausibel zur Luftmasse | 0 | - |
| 0x100E08 | Drosselklappe, Drosselklappenpotenziometer 2: Signal unplausibel zur Luftmasse | 0 | - |
| 0x100F08 | Drosselklappe 2, Drosselklappenpotenziometer 2: Signal unplausibel zur Luftmasse | 0 | - |
| 0x101001 | Drosselklappe, Drosselklappenpotenziometer 1: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x101002 | Drosselklappe: Drosselklappenpotenziometer 1, Kurzschluss nach Masse | 0 | - |
| 0x101101 | Drosselklappe 2, Drosselklappenpotenziometer 1: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x101102 | Drosselklappe 2: Drosselklappenpotenziometer 1, Kurzschluss nach Masse | 0 | - |
| 0x101201 | Drosselklappe: Drosselklappenpotenziometer 2, Kurzschluss nach Plus | 0 | - |
| 0x101202 | Drosselklappe, Drosselklappenpotenziometer 2: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x101301 | Drosselklappe 2: Drosselklappenpotenziometer 2, Kurzschluss nach Plus | 0 | - |
| 0x101302 | Drosselklappe 2, Drosselklappenpotenziometer 2: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x101401 | Drosselklappe, Adaption: Randbedingungen nicht erfüllt | 1 | - |
| 0x101402 | Drosselklappe: Notluftposition nicht adaptiert | 0 | - |
| 0x101408 | Drosselklappe: Erstadaption, unterer Anschlag nicht gelernt | 0 | - |
| 0x101501 | Drosselklappe 2, Adaption: Randbedingungen nicht erfüllt | 1 | - |
| 0x101502 | Drosselklappe 2: Notluftposition nicht adaptiert | 0 | - |
| 0x101508 | Drosselklappe 2: Erstadaption, unterer Anschlag nicht gelernt | 0 | - |
| 0x101601 | Drosselklappe: Federtest, unterer Anschlag nicht erreicht | 0 | - |
| 0x101602 | Drosselklappe: Federtest, Fehler untere Rückstellfeder | 0 | - |
| 0x101604 | Drosselklappe, Federtest: obere Sollposition nicht erreicht | 0 | - |
| 0x101608 | Drosselklappe, Federtest: Fehler obere Rückstellfeder | 0 | - |
| 0x101701 | Drosselklappe 2: Federtest, unterer Anschlag nicht erreicht | 0 | - |
| 0x101702 | Drosselklappe 2: Federtest, Fehler untere Rückstellfeder | 0 | - |
| 0x101704 | Drosselklappe 2, Federtest: obere Sollposition nicht erreicht | 0 | - |
| 0x101708 | Drosselklappe 2, Federtest: Fehler obere Rückstellfeder | 0 | - |
| 0x101801 | Drosselklappe 2, Startprüfung: Federtest | 0 | - |
| 0x101802 | Drosselklappe 2, Startprüfung: Prüfung Notluftposition | 0 | - |
| 0x101901 | Drosselklappe, Startprüfung: Federtest | 0 | - |
| 0x101902 | Drosselklappe, Startprüfung: Prüfung Notluftposition | 0 | - |
| 0x101C08 | Drosselklappe, Drosselklappenpotenziometer, Plausibilität: Gleichlauffehler zwischen Potentiometer 1 und 2 | 0 | - |
| 0x101D08 | Drosselklappe 2, Drosselklappenpotenziometer, Plausibilität: Gleichlauffehler zwischen Potentiometer 1 und 2 | 0 | - |
| 0x101F01 | Drosselklappenwinkel - Saugrohrdruck, Korrelation: Grenzwert überschritten | 0 | - |
| 0x101F02 | Drosselklappenwinkel - Absolutdruck Saugrohr, Vergleich: Druck zu niedrig | 0 | - |
| 0x102001 | Luftmasse, Plausibilität: Luftmasse zu hoch | 0 | - |
| 0x102002 | Luftmasse, Plausibilität: Luftmasse zu niedrig | 0 | - |
| 0x102301 | Luftmassenmesser, Arbeitsbereich: Periodendauer zu groß, Luftmasse zu niedrig | 0 | - |
| 0x102302 | Luftmassenmesser, Arbeitsbereich: Periodendauer zu niedrig, Luftmasse zu hoch | 0 | - |
| 0x102401 | Luftmassenmesser 2, Messbereich: Periodendauer zu groß, Luftmasse zu gering | 0 | - |
| 0x102402 | Luftmassenmesser 2, Arbeitsbereich: Periodendauer zu niedrig, Luftmasse zu hoch | 0 | - |
| 0x102501 | Luftmassenmesser: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x102502 | Luftmassenmesser: Kurzschluss nach Masse | 0 | - |
| 0x102601 | Luftmassenmesser 2: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x102602 | Luftmassenmesser 2: Kurzschluss nach Masse | 0 | - |
| 0x102901 | Luftmasse 2, Plausibilität: Luftmasse zu hoch | 0 | - |
| 0x102902 | Luftmasse 2, Plausibilität: Luftmasse zu niedrig | 0 | - |
| 0x102B01 | Luftmassenmesser, Korrektursignal: Kurzschluss nach Plus | 0 | - |
| 0x102B02 | Luftmassenmesser, Korrektursignal: Kurzschluss nach Masse | 0 | - |
| 0x102C01 | Luftmassenmesser 2, Korrektursignal: Kurzschluss nach Plus | 0 | - |
| 0x102C02 | Luftmassenmesser 2, Korrektursignal: Kurzschluss nach Masse | 0 | - |
| 0x102D01 | Luftmassenmesser, Korrektursignal, Arbeitsbereich: Periodendauer zu groß | 0 | - |
| 0x102D02 | Luftmassenmesser, Korrektursignal, Arbeitsbereich: Periodendauer zu niedrig | 0 | - |
| 0x102E01 | Luftmassenmesser 2, Korrektursignal, Arbeitsbereich: Periodendauer zu groß | 0 | - |
| 0x102E02 | Luftmassenmesser 2, Korrektursignal, Arbeitsbereich: Periodendauer zu niedrig | 0 | - |
| 0x103001 | Fahrpedalmodul, Pedalwertgeber 1: Kurzschluss nach Plus | 0 | - |
| 0x103002 | Fahrpedalmodul, Pedalwertgeber 1: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x103004 | Fahrpedalmodul, Pedalwertgeber 1: Arbeitsbereich, Spannung zu hoch | 0 | - |
| 0x103008 | Fahrpedalmodul, Pedalwertgeber 1: Arbeitsbereich, Spannung zu niedrig | 0 | - |
| 0x103101 | Fahrpedalmodul, Pedalwertgeber 2: Kurzschluss nach Plus | 0 | - |
| 0x103102 | Fahrpedalmodul, Pedalwertgeber 2: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x103104 | Fahrpedalmodul, Pedalwertgeber 2: Arbeitsbereich, Spannung zu hoch | 0 | - |
| 0x103108 | Fahrpedalmodul, Pedalwertgeber 2: Arbeitsbereich, Spannung zu niedrig | 0 | - |
| 0x103208 | Fahrpedalmodul, Pedalwertgeber: Doppelfehler | 0 | - |
| 0x103308 | Fahrpedalmodul, Pedalwertgeber, Plausibilität: Gleichlauffehler zwischen Pedalwertgeber 1 und Pedalwertgeber 2 | 0 | - |
| 0x104301 | Absolutdrucksensor, Saugrohr: Nachlauf, Druck zu hoch | 0 | - |
| 0x104302 | Absolutdrucksensor, Saugrohr: Nachlauf, Druck zu niedrig | 0 | - |
| 0x104401 | Absolutdrucksensor, Saugrohr: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x104402 | Absolutdrucksensor, Saugrohr: Kurzschluss nach Masse | 0 | - |
| 0x104501 | Absolutdrucksensor 2, Saugrohr: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x104502 | Absolutdrucksensor 2, Saugrohr: Kurzschluss nach Masse | 0 | - |
| 0x104601 | Absolutdrucksensor 2, Saugrohr: Nachlauf, Druck zu hoch | 0 | - |
| 0x104602 | Absolutdrucksensor 2, Saugrohr: Nachlauf, Druck zu niedrig | 0 | - |
| 0x105001 | Umgebungsdrucksensor: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x105002 | Umgebungsdrucksensor: Kurzschluss nach Masse | 0 | - |
| 0x105101 | Umgebungsdrucksensor, Plausibilität: Maximaldruck unplausibel | 0 | - |
| 0x105102 | Umgebungsdrucksensor, Plausibilität: Minimaldruck unplausibel | 0 | - |
| 0x105201 | Umgebungsdrucksensor, Nachlauf: Druck zu hoch | 0 | - |
| 0x105202 | Umgebungsdrucksensor, Nachlauf: Druck zu niedrig | 0 | - |
| 0x107001 | Drosselklappenwinkel - Saugrohrdruck 2, Korrelation: Grenzwert überschritten | 0 | - |
| 0x107002 | Drosselklappenwinkel 2 - Absolutdruck Saugrohr 2, Vergleich: Druck zu niedrig | 0 | - |
| 0x107508 | Luftmassenmesser, Eigendiagnose: Sensor defekt | 0 | - |
| 0x107608 | Luftmassenmesser 2, Eigendiagnose: Sensor defekt | 0 | - |
| 0x107C08 | Luftmassenmesser, Laststeuerung: Massenstrom zu hoch | 0 | - |
| 0x107D08 | Luftmassenmesser 2, Laststeuerung: Massenstrom zu hoch | 0 | - |
| 0x108201 | Ansauglufttemperatur: Plausibilität, Temperatur zu hoch | 0 | - |
| 0x108202 | Ansauglufttemperatur: Plausibilität, Temperatur zu niedrig | 0 | - |
| 0x108208 | Ansauglufttemperatur: Signal, festliegend | 0 | - |
| 0x108301 | Ansauglufttemperatur 2: Plausibilität, Temperatur zu hoch | 0 | - |
| 0x108302 | Ansauglufttemperatur 2: Plausibilität, Temperatur zu niedrig | 0 | - |
| 0x108308 | Ansauglufttemperatur 2: Signal, festliegend | 0 | - |
| 0x108401 | Ansauglufttemperatursensor vor Drosselklappe, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x108402 | Ansauglufttemperatursensor vor Drosselklappe, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x108501 | Ansauglufttemperatursensor vor Drosselklappe 2, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x108502 | Ansauglufttemperatursensor vor Drosselklappe 2, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x108601 | Ansauglufttemperatur vor Drosselklappe: Plausibilität, Temperatur zu hoch | 0 | - |
| 0x108602 | Ansauglufttemperatur vor Drosselklappe: Plausibilität, Temperatur zu niedrig | 0 | - |
| 0x108608 | Ansauglufttemperatur vor Drosselklappe: Signal, festliegend | 0 | - |
| 0x108701 | Ansauglufttemperatur vor Drosselklappe 2: Plausibilität, Temperatur zu hoch | 0 | - |
| 0x108702 | Ansauglufttemperatur vor Drosselklappe 2: Plausibilität, Temperatur zu niedrig | 0 | - |
| 0x108708 | Ansauglufttemperatur vor Drosselklappe 2: Signal, festliegend | 0 | - |
| 0x108801 | Ansauglufttemperatursensor vor Drosselklappe: Signaländerung, zu schnell | 0 | - |
| 0x108804 | Ansauglufttemperatursensor vor Drosselklappe: Plausibilität, Kaltstart, Temperatur zu hoch | 0 | - |
| 0x108808 | Ansauglufttemperatursensor vor Drosselklappe: Signaländerung, zu schnell | 0 | - |
| 0x108901 | Ansauglufttemperatursensor vor Drosselklappe 2: Signaländerung, zu schnell | 0 | - |
| 0x108904 | Ansauglufttemperatursensor vor Drosselklappe 2: Plausibilität, Kaltstart, Temperatur zu hoch | 0 | - |
| 0x108908 | Ansauglufttemperatursensor vor Drosselklappe 2: Signaländerung, zu schnell | 0 | - |
| 0x108A01 | Ladelufttemperatursensor, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x108A02 | Ladelufttemperatursensor, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x108B01 | Ladelufttemperatursensor 2, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x108B02 | Ladelufttemperatursensor 2, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x108C01 | Ladelufttemperatur: Plausibilität, Temperatur zu hoch | 0 | - |
| 0x108C02 | Ladelufttemperatur: Plausibilität, Temperatur zu niedrig | 0 | - |
| 0x108C08 | Ladelufttemperatur: Signal, festliegend | 0 | - |
| 0x108D01 | Ladelufttemperatur 2: Plausibilität, Temperatur zu hoch | 0 | - |
| 0x108D02 | Ladelufttemperatur 2: Plausibilität, Temperatur zu niedrig | 0 | - |
| 0x108D08 | Ladelufttemperatur 2: Signal, festliegend | 0 | - |
| 0x109001 | Kühlmitteltemperatursensor, elektrisch: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 | - |
| 0x109002 | Kühlmitteltemperatursensor, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x109208 | Kühlmitteltemperatursensor, Plausibilität: Signal hängt | 0 | - |
| 0x109308 | Kühlmitteltemperatursensor, Plausibilität: Signaländerung zu schnell | 0 | - |
| 0x109408 | Kühlmitteltemperatursensor, Plausibilität: Signal hängt im oberen Messbereich | 0 | - |
| 0x10A001 | Temperatursensor Kühleraustritt, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x10A002 | Temperatursensor Kühleraustritt, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x10A108 | Temperatursensor Kühleraustritt, Signaländerung: zu schnell | 0 | - |
| 0x10A201 | Temperatursensor Kühleraustritt: Plausibilität, Kaltstart, Temperatur zu hoch | 0 | - |
| 0x10A208 | Temperatursensor Kühleraustritt: Signal, festliegend | 0 | - |
| 0x10B008 | Außentemperatursensor, Plausibilität: Signal unplausibel | 0 | - |
| 0x10B101 | Außentemperatursensor, elektrisch: Kurzschluss nach Plus oder Leitungsunterbrechung | 1 | - |
| 0x10B102 | Außentemperatursensor, elektrisch: Kurzschluss nach Masse | 1 | - |
| 0x10B104 | Außentemperatursensor, elektrisch: Signalfehler | 1 | - |
| 0x10C000 | Ladelufttemperatursensor | 0 | - |
| 0x10C001 | Ladelufttemperatursensor: Signaländerung, zu schnell | 0 | - |
| 0x10C004 | Ladelufttemperatursensor: Plausibilität, Kaltstart, Temperatur zu hoch | 0 | - |
| 0x10C008 | Ladelufttemperatursensor: Signaländerung, zu schnell | 0 | - |
| 0x10C100 | Ladelufttemperatursensor 2 | 0 | - |
| 0x10C101 | Ladelufttemperatursensor 2: Signaländerung, zu schnell | 0 | - |
| 0x10C104 | Ladelufttemperatursensor 2: Plausibilität, Kaltstart, Temperatur zu hoch | 0 | - |
| 0x10C108 | Ladelufttemperatursensor 2: Signaländerung, zu schnell | 0 | - |
| 0x110001 | Zylindereinspritzabschaltung: Druck zu niedrig im Hochdrucksystem | 0 | - |
| 0x110002 | Zylindereinspritzabschaltung: Druck zu niedrig im Niederdrucksystem | 0 | - |
| 0x110008 | Zylindereinspritzabschaltung: Tankfüllstand zu gering | 0 | - |
| 0x110101 | Injektor Zylinder 1, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110102 | Injektor Zylinder 1, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110104 | Injektor Zylinder 1, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110108 | Injektor Zylinder 1, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110201 | Injektor Zylinder 2, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110202 | Injektor Zylinder 2, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110204 | Injektor Zylinder 2, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110208 | Injektor Zylinder 2, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110301 | Injektor Zylinder 3, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110302 | Injektor Zylinder 3, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110304 | Injektor Zylinder 3, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110308 | Injektor Zylinder 3, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110401 | Injektor Zylinder 4, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110402 | Injektor Zylinder 4, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110404 | Injektor Zylinder 4, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110408 | Injektor Zylinder 4, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110501 | Injektor Zylinder 5, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110502 | Injektor Zylinder 5, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110504 | Injektor Zylinder 5, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110508 | Injektor Zylinder 5, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110601 | Injektor Zylinder 6, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110602 | Injektor Zylinder 6, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110604 | Injektor Zylinder 6, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110608 | Injektor Zylinder 6, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110701 | Injektor Zylinder 7, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110702 | Injektor Zylinder 7, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110704 | Injektor Zylinder 7, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110708 | Injektor Zylinder 7, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110801 | Injektor Zylinder 8, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110802 | Injektor Zylinder 8, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110804 | Injektor Zylinder 8, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110808 | Injektor Zylinder 8, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110901 | Injektor Zylinder 9, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110902 | Injektor Zylinder 9, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110904 | Injektor Zylinder 9, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110908 | Injektor Zylinder 9, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110A01 | Injektor Zylinder 10, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110A02 | Injektor Zylinder 10, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110A04 | Injektor Zylinder 10, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110A08 | Injektor Zylinder 10, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110B01 | Injektor Zylinder 11, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110B02 | Injektor Zylinder 11, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110B04 | Injektor Zylinder 11, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110B08 | Injektor Zylinder 11, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110C01 | Injektor Zylinder 12, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x110C02 | Injektor Zylinder 12, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110C04 | Injektor Zylinder 12, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 | - |
| 0x110C08 | Injektor Zylinder 12, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 | - |
| 0x112101 | Injektor Zylinder 1, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112102 | Injektor Zylinder 1, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112104 | Injektor Zylinder 1, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112108 | Injektor Zylinder 1, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112201 | Injektor Zylinder 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112202 | Injektor Zylinder 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112204 | Injektor Zylinder 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112208 | Injektor Zylinder 2, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112301 | Injektor Zylinder 3, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112302 | Injektor Zylinder 3, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112304 | Injektor Zylinder 3, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112308 | Injektor Zylinder 3, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112401 | Injektor Zylinder 4, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112402 | Injektor Zylinder 4, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112404 | Injektor Zylinder 4, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112408 | Injektor Zylinder 4, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112501 | Injektor Zylinder 5, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112502 | Injektor Zylinder 5, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112504 | Injektor Zylinder 5, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112508 | Injektor Zylinder 5, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112601 | Injektor Zylinder 6, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112602 | Injektor Zylinder 6, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112604 | Injektor Zylinder 6, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112608 | Injektor Zylinder 6, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112701 | Injektor Zylinder 7, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112702 | Injektor Zylinder 7, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112704 | Injektor Zylinder 7, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112708 | Injektor Zylinder 7, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112801 | Injektor Zylinder 8, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112802 | Injektor Zylinder 8, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112804 | Injektor Zylinder 8, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112808 | Injektor Zylinder 8, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112901 | Injektor Zylinder 9, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112902 | Injektor Zylinder 9, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112904 | Injektor Zylinder 9, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112908 | Injektor Zylinder 9, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112A01 | Injektor Zylinder 10, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112A02 | Injektor Zylinder 10, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112A04 | Injektor Zylinder 10, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112A08 | Injektor Zylinder 10, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112B01 | Injektor Zylinder 11, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112B02 | Injektor Zylinder 11, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112B04 | Injektor Zylinder 11, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112B08 | Injektor Zylinder 11, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112C01 | Injektor Zylinder 12, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x112C02 | Injektor Zylinder 12, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x112C04 | Injektor Zylinder 12, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x112C08 | Injektor Zylinder 12, Ansteuerung: Leitungsunterbrechung bei aufgeladenem Injektor | 0 | - |
| 0x112E01 | Einspritzung 2, Plausibilität, Kaltstart: Anzahl Einspritzungen unplausibel | 0 | - |
| 0x112F01 | Einspritzung, Plausibilität, Kaltstart: Anzahl Einspritzungen unplausibel | 0 | - |
| 0x113101 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 1: Adaptionen nicht mehr möglich | 0 | - |
| 0x113201 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 2: Adaptionen nicht mehr möglich | 0 | - |
| 0x113301 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 3: Adaptionen nicht mehr möglich | 0 | - |
| 0x113401 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 4: Adaptionen nicht mehr möglich | 0 | - |
| 0x113501 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 5: Adaptionen nicht mehr möglich | 0 | - |
| 0x113601 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 6: Adaptionen nicht mehr möglich | 0 | - |
| 0x113701 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 7: Adaptionen nicht mehr möglich | 0 | - |
| 0x113801 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 8: Adaptionen nicht mehr möglich | 0 | - |
| 0x113901 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 9: Adaptionen nicht mehr möglich | 0 | - |
| 0x113A01 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 10: Adaptionen nicht mehr möglich | 0 | - |
| 0x113B01 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 11: Adaptionen nicht mehr möglich | 0 | - |
| 0x113C01 | Zylinderindividuelle Gemischüberwachung, Eigendiagnose, Zylinder 12: Adaptionen nicht mehr möglich | 0 | - |
| 0x115101 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 1: Adaption über gültigem Bereich | 0 | - |
| 0x115201 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 2: Adaption über gültigem Bereich | 0 | - |
| 0x115301 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 3: Adaption über gültigem Bereich | 0 | - |
| 0x115401 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 4: Adaption über gültigem Bereich | 0 | - |
| 0x115501 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 5: Adaption über gültigem Bereich | 0 | - |
| 0x115601 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 6: Adaption über gültigem Bereich | 0 | - |
| 0x115701 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 7: Adaption über gültigem Bereich | 0 | - |
| 0x115801 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 8: Adaption über gültigem Bereich | 0 | - |
| 0x115901 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 9: Adaption über gültigem Bereich | 0 | - |
| 0x115A01 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 10: Adaption über gültigem Bereich | 0 | - |
| 0x115B01 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 11: Adaption über gültigem Bereich | 0 | - |
| 0x115C01 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 12: Adaption über gültigem Bereich | 0 | - |
| 0x115D04 | Injektormengenabgleich, Plausibilität: Energie-Nominalwert | 0 | - |
| 0x115D08 | Injektormengenabgleich, Plausibilität: Kleinmengen-Nominalwert | 0 | - |
| 0x116100 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 1 | 0 | - |
| 0x116101 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 1: Adaption unter gültigem Bereich | 0 | - |
| 0x116200 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 2 | 0 | - |
| 0x116201 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 2: Adaption unter gültigem Bereich | 0 | - |
| 0x116301 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 3: Adaption unter gültigem Bereich | 0 | - |
| 0x116401 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 4: Adaption unter gültigem Bereich | 0 | - |
| 0x116501 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 5: Adaption unter gültigem Bereich | 0 | - |
| 0x116601 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 6: Adaption unter gültigem Bereich | 0 | - |
| 0x116701 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 7: Adaption unter gültigem Bereich | 0 | - |
| 0x116801 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 8: Adaption unter gültigem Bereich | 0 | - |
| 0x116901 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 9: Adaption unter gültigem Bereich | 0 | - |
| 0x116A01 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 10: Adaption unter gültigem Bereich | 0 | - |
| 0x116B01 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 11: Adaption unter gültigem Bereich | 0 | - |
| 0x116C01 | Zylinderindividuelle Gemischüberwachung, Adaption, Zylinder 12: Adaption unter gültigem Bereich | 0 | - |
| 0x118001 | Gemischregelung: Gemisch zu mager | 0 | - |
| 0x118002 | Gemischregelung: Gemisch zu fett | 0 | - |
| 0x118101 | Gemischregelung 2: Gemisch zu mager | 0 | - |
| 0x118102 | Gemischregelung 2: Gemisch zu fett | 0 | - |
| 0x118401 | Gemischregelung: Gemisch zu mager, große Abweichung | 0 | - |
| 0x118402 | Gemischregelung: Gemisch zu fett, große Abweichung | 0 | - |
| 0x118501 | Gemischregelung 2: Gemisch zu mager, große Abweichung | 0 | - |
| 0x118502 | Gemischregelung 2: Gemisch zu fett, große Abweichung | 0 | - |
| 0x118601 | Lambdasonde vor Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu fett | 0 | - |
| 0x118602 | Lambdasonde vor Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu mager | 0 | - |
| 0x118701 | Lambdasonde vor Katalysator 2, Gemischfeinregelung: Abgas nach Katalysator zu fett | 0 | - |
| 0x118702 | Lambdasonde vor Katalysator 2, Gemischfeinregelung: Abgas nach Katalysator zu mager | 0 | - |
| 0x118801 | Lambdasonde nach Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu fett | 0 | - |
| 0x118802 | Lambdasonde nach Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu mager | 0 | - |
| 0x118901 | Lambdasonde nach Katalysator 2, Gemischfeinregelung: Abgas nach Katalysator zu fett | 0 | - |
| 0x118902 | Lambdasonde nach Katalysator 2, Gemischfeinregelung: Abgas nach Katalysator zu mager | 0 | - |
| 0x119001 | Raildrucksensor, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x119002 | Raildrucksensor, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x119101 | Raildrucksensor 2, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x119102 | Raildrucksensor 2, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x119201 | Kraftstoffniederdrucksensor: elektrisch, Kurzschluss nach Plus | 0 | - |
| 0x119202 | Kraftstoffniederdrucksensor: elektrisch, Kurzschluss nach Masse | 0 | - |
| 0x119208 | Kraftstoffniederdrucksensor: Signal, festliegend | 0 | - |
| 0x119F01 | Kraftstoffhochdruck 2 bei Freigabe der Einspritzung: Druck zu niedrig | 0 | - |
| 0x11A001 | Kraftstoffhochdruck, Plausibilität: Druck zu hoch | 0 | - |
| 0x11A002 | Kraftstoffhochdruck, Plausibilität: Druck zu niedrig | 0 | - |
| 0x11A101 | Kraftstoffhochdruck 2, Plausibilität: Druck zu hoch | 0 | - |
| 0x11A102 | Kraftstoffhochdruck 2, Plausibilität: Druck zu niedrig | 0 | - |
| 0x11A201 | Kraftstoffniederdruck, Arbeitsbereich: Druck zu hoch | 0 | - |
| 0x11A202 | Kraftstoffniederdruck, Arbeitsbereich: Maximaldruck überschritten | 0 | - |
| 0x11A204 | Kraftstoffniederdruck, Arbeitsbereich: Druck zu niedrig | 0 | - |
| 0x11A401 | Kraftstoffhochdruck bei Freigabe der Einspritzung: Druck zu niedrig | 0 | - |
| 0x11A501 | Kraftstoffhochdruck, Arbeitsbereich: Druck zu hoch | 0 | - |
| 0x11A502 | Kraftstoffhochdruck, Arbeitsbereich: Druck zu hoch | 0 | - |
| 0x11A504 | Kraftstoffhochdruck, Arbeitsbereich: Druck zu niedrig | 0 | - |
| 0x11A601 | Kraftstoffhochdruck 2, Arbeitsbereich: Druck zu hoch | 0 | - |
| 0x11A602 | Kraftstoffhochdruck 2, Arbeitsbereich: Druck zu hoch | 0 | - |
| 0x11A604 | Kraftstoffhochdruck 2, Arbeitsbereich: Druck zu niedrig | 0 | - |
| 0x11A701 | Raildrucksensor, Plausibilität: Druck zu hoch | 0 | - |
| 0x11A702 | Raildrucksensor, Plausibilität: Druck zu niedrig | 0 | - |
| 0x11A801 | Raildrucksensor 2, Plausibilität: Druck zu hoch | 0 | - |
| 0x11A802 | Raildrucksensor 2, Plausibilität: Druck zu niedrig | 0 | - |
| 0x11AC01 | Kraftstoffhochdruck, Plausibilität, Kaltstart: Druck zu hoch | 0 | - |
| 0x11AC02 | Kraftstoffhochdruck, Plausibilität, Kaltstart: Druck zu niedrig | 0 | - |
| 0x11AD01 | Kraftstoffhochdruck 2, Plausibilität, Kaltstart: Druck zu hoch | 0 | - |
| 0x11AD02 | Kraftstoffhochdruck 2, Plausibilität, Kaltstart: Druck zu niedrig | 0 | - |
| 0x11B004 | Kraftstoffpumpe, Funktion: Notabschaltung | 1 | - |
| 0x11B101 | Elektrische Kraftstoffpumpe: Drehzahl zu hoch | 1 | - |
| 0x11B102 | Elektrische Kraftstoffpumpe: Drehzahl zu niedrig | 1 | - |
| 0x11B104 | Elektrische Kraftstoffpumpe: Notlauf | 1 | - |
| 0x11B108 | Kraftstoffpumpe: Übertemperatur | 1 | - |
| 0x11B201 | Kraftstoffniederdruckregelung, Plausibilität: Förderleistung außerhalb gültigem Bereich | 0 | - |
| 0x11B202 | Kraftstoffniederdruckregelung, Plausibilität: Förderleistung außerhalb Grenzwert wegen Alterung | 0 | - |
| 0x11B204 | Kraftstoffniederdruckregelung, Plausibilität: Förderleistung zu niedrig wegen Alterung | 0 | - |
| 0x11C201 | Mengensteuerventil, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x11C202 | Mengensteuerventil, Ansteuerung: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x11C301 | Mengensteuerventil 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x11C302 | Mengensteuerventil 2, Ansteuerung: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 | - |
| 0x11C401 | Mengensteuerventil, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x11C402 | Mengensteuerventil, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x120208 | Ladedruckregelung, Plausibilität: Druck zu hoch | 0 | - |
| 0x120308 | Ladedruckregelung, Plausibilität: Druck zu niedrig | 0 | - |
| 0x120408 | Ladedruckregelung, Abschaltung: Druckaufbau gesperrt | 0 | - |
| 0x120608 | Ladedruckregelung 2, Plausibilität: Druck zu hoch | 0 | - |
| 0x120708 | Ladedruckregelung 2, Plausibilität: Druck zu niedrig | 0 | - |
| 0x120908 | Ladedruckregelung 2, Abschaltung: Druckaufbau gesperrt | 0 | - |
| 0x121001 | Ladedrucksensor, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x121002 | Ladedrucksensor, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x121101 | Ladedrucksensor 2, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x121102 | Ladedrucksensor 2, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x121201 | Ladedrucksensor, Plausibilität, Nachlauf: Druck zu hoch | 0 | - |
| 0x121202 | Ladedrucksensor, Plausibilität, Nachlauf: Druck zu niedrig | 0 | - |
| 0x121301 | Ladedrucksensor 2, Plausibilität, Nachlauf: Druck zu hoch | 0 | - |
| 0x121302 | Ladedrucksensor 2, Plausibilität, Nachlauf: Druck zu niedrig | 0 | - |
| 0x122001 | Schubumluftventil, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x122002 | Schubumluftventil, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x122004 | Schubumluftventil, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x122101 | Schubumluftventil 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x122102 | Schubumluftventil 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x122104 | Schubumluftventil 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x123001 | Wastegate, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x123002 | Wastegate, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x123004 | Wastegate, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x123101 | Wastegate 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x123102 | Wastegate 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x123104 | Wastegate 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x128101 | Lambdasonde vor Katalysator, Systemprüfung: Signal konstant mager | 0 | - |
| 0x128201 | Lambdasonde vor Katalysator 2, Systemprüfung: Signal konstant mager | 0 | - |
| 0x128301 | Lambdasonde vor Katalysator, Systemprüfung: Signal konstant fett | 0 | - |
| 0x128401 | Lambdasonde vor Katalysator 2, Systemprüfung: Signal konstant fett | 0 | - |
| 0x128501 | Lambdasonde vor Katalysator, im Schub: Signal außerhalb Grenzwert | 0 | - |
| 0x128601 | Lambdasonde vor Katalysator 2, im Schub: Signal außerhalb Grenzwert | 0 | - |
| 0x128901 | Lambdasonde vor Katalysator, Dynamik: langsame Reaktion | 0 | - |
| 0x128902 | Lambdasonde vor Katalysator, Dynamik: langsame Reaktion | 0 | - |
| 0x128A01 | Lambdasonde vor Katalysator 2, Dynamik: langsame Reaktion | 0 | - |
| 0x128A02 | Lambdasonde vor Katalysator 2, Dynamik: langsame Reaktion | 0 | - |
| 0x128B01 | Lambdasonde vor Katalysator: Falschluft erkannt | 0 | - |
| 0x128C01 | Lambdasonde vor Katalysator 2: Falschluft erkannt | 0 | - |
| 0x128E01 | Lambdasonde vor Katalysator, Leitungsfehler: Unterbrechung Nernstleitung | 0 | - |
| 0x128E02 | Lambdasonde vor Katalysator, elektrisch: Unterbrechung virtuelle Masse oder Pumpstromleitung | 0 | - |
| 0x128E04 | Lambdasonde vor Katalysator, elektrisch: Unterbrechung virtuelle Masse oder Pumpstromleitung | 0 | - |
| 0x128F01 | Lambdasonde vor Katalysator 2, Leitungsfehler: Unterbrechung Nernstleitung | 0 | - |
| 0x128F02 | Lambdasonde vor Katalysator 2, elektrisch: Unterbrechung virtuelle Masse oder Pumpstromleitung | 0 | - |
| 0x128F04 | Lambdasonde vor Katalysator 2, elektrisch: Unterbrechung virtuelle Masse oder Pumpstromleitung | 0 | - |
| 0x129001 | Lambdasonde vor Katalysator, Signalleitungen: Kurzschluss nach Plus | 0 | - |
| 0x129002 | Lambdasonde vor Katalysator, Signalleitungen: Kurzschluss nach Masse | 0 | - |
| 0x129101 | Lambdasonde vor Katalysator 2, Signalleitungen: Kurzschluss nach Plus | 0 | - |
| 0x129102 | Lambdasonde vor Katalysator 2, Signalleitungen: Kurzschluss nach Masse | 0 | - |
| 0x129201 | DME, interner Fehler: Regler für Lambdasonde vor Katalysator defekt | 0 | - |
| 0x129202 | DME, interner Fehler: Regler für Lambdasonde vor Katalysator defekt | 0 | - |
| 0x129301 | DME, interner Fehler, Lambdasonde vor Katalysator 2: Initialisierungsfehler | 0 | - |
| 0x129302 | DME, interner Fehler, Lambdasonde vor Katalysator 2: Kommunikationsfehler | 0 | - |
| 0x12A101 | Lambdasonde nach Katalysator, Systemprüfung: Signal konstant fett | 0 | - |
| 0x12A102 | Lambdasonde nach Katalysator, Systemprüfung: Signal konstant Mager | 0 | - |
| 0x12A201 | Lambdasonde nach Katalysator 2, Systemprüfung: Signal konstant Fett | 0 | - |
| 0x12A202 | Lambdasonde nach Katalysator 2, Systemprüfung: Signal konstant Mager | 0 | - |
| 0x12A308 | Lambdasonde nach Katalysator, Dynamik, von Fett nach Mager: langsame Reaktion | 0 | - |
| 0x12A408 | Lambdasonde nach Katalysator 2, Dynamik, von Fett nach Mager: langsame Reaktion | 0 | - |
| 0x12A501 | Lambdasonde nach Katalysator 2: Signal festliegend auf Fett | 0 | - |
| 0x12A701 | Lambdasonde nach Katalysator, Signal: Kurzschluss nach Plus | 0 | - |
| 0x12A801 | Lambdasonde nach Katalysator 2, Signal: Kurzschluss nach Plus | 0 | - |
| 0x12A902 | Lambdasonde nach Katalysator, Signal: Kurzschluss nach Masse | 0 | - |
| 0x12AA02 | Lambdasonde nach Katalysator 2, Signal: Kurzschluss nach Masse | 0 | - |
| 0x12AB04 | Lambdasonde nach Katalysator, Signal: Leitungsunterbrechung | 0 | - |
| 0x12AC04 | Lambdasonde nach Katalysator 2, Signal: Leitungsunterbrechung | 0 | - |
| 0x12AD01 | Lambdasonde nach Katalysator: Signal festliegend auf Mager | 0 | - |
| 0x12AE01 | Lambdasonde nach Katalysator: Signal festliegend auf Fett | 0 | - |
| 0x12AF08 | Lambdasonde nach Katalysator, im Schub, von Fett nach Mager: verzögerte Reaktion | 0 | - |
| 0x12B001 | Lambdasonde nach Katalysator 2, von Fett nach Mager: verzögerte Reaktion | 0 | - |
| 0x12B008 | Lambdasonde nach Katalysator 2, im Schub, von Fett nach Mager: verzögerte Reaktion | 0 | - |
| 0x12B101 | Lambdasondenbeheizung vor Katalysator, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x12B102 | Lambdasondenbeheizung vor Katalysator, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x12B104 | Lambdasondenbeheizung vor Katalysator, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x12B201 | Lambdasondenbeheizung vor Katalysator 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x12B202 | Lambdasondenbeheizung vor Katalysator 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x12B204 | Lambdasondenbeheizung vor Katalysator 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x12B301 | Lambdasondenbeheizung nach Katalysator, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x12B302 | Lambdasondenbeheizung nach Katalysator, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x12B304 | Lambdasondenbeheizung nach Katalysator, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x12B401 | Lambdasondenbeheizung nach Katalysator 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x12B402 | Lambdasondenbeheizung nach Katalysator 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x12B404 | Lambdasondenbeheizung nach Katalysator 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x12B501 | Lambdasondentemperaturmessung vor Katalysator: Betriebstemperatur nicht erreicht | 0 | - |
| 0x12B502 | Lambdasondentemperaturmessung vor Katalysator: Betriebstemperatur im Warmlauf nicht erreicht | 0 | - |
| 0x12B504 | Lambdasondentemperaturmessung vor Katalysator: Messung im Steuergerät fehlgeschlagen | 0 | - |
| 0x12B601 | Lambdasondentemperaturmessung vor Katalysator 2: Betriebstemperatur nicht erreicht | 0 | - |
| 0x12B602 | Lambdasondentemperaturmessung vor Katalysator 2: Betriebstemperatur im Warmlauf nicht erreicht | 0 | - |
| 0x12B604 | Lambdasondentemperaturmessung vor Katalysator 2: Messung im Steuergerät fehlgeschlagen | 0 | - |
| 0x12B701 | Lambdasondenbeheizung nach Katalysator, Funktion: Innenwiderstand zu hoch | 0 | - |
| 0x12B801 | Lambdasondenbeheizung nach Katalysator 2, Funktion: Innenwiderstand zu hoch | 0 | - |
| 0x12B900 | Lambdasonde vor Katalysator, Temperatur | 0 | - |
| 0x12B901 | Lambdasondentemperaturmessung vor Katalysator: Betriebstemperatur nicht erreicht | 0 | - |
| 0x12B902 | Lambdasondentemperaturmessung vor Katalysator: Betriebstemperatur im Warmlauf nicht erreicht | 0 | - |
| 0x12B904 | Lambdasondentemperaturmessung vor Katalysator: Messung im Steuergerät fehlgeschlagen | 0 | - |
| 0x12BA01 | Lambdasondentemperaturmessung vor Katalysator 2: Betriebstemperatur nicht erreicht | 0 | - |
| 0x12BA02 | Lambdasondentemperaturmessung vor Katalysator 2: Betriebstemperatur im Warmlauf nicht erreicht | 0 | - |
| 0x12BA04 | Lambdasondentemperaturmessung vor Katalysator 2: Messung im Steuergerät fehlgeschlagen | 0 | - |
| 0x12BB01 | Lambdasonde nach Katalysator, von Mager nach Fett: verzögerte Reaktion | 0 | - |
| 0x12BC01 | Lambdasonde nach Katalysator 2, von Mager nach Fett: verzögerte Reaktion | 0 | - |
| 0x12BD01 | Lambdasonde nach Katalysator 2: Signal festliegend auf Mager | 0 | - |
| 0x12BE08 | Lambdasonde nach Katalysator, Dynamik, von Mager nach Fett: langsame Reaktion | 0 | - |
| 0x12BF08 | Lambdasonde nach Katalysator 2, Dynamik, von Mager nach Fett: langsame Reaktion | 0 | - |
| 0x130001 | VANOS-Magnetventil Einlass, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x130002 | VANOS-Magnetventil Einlass, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x130004 | VANOS-Magnetventil Einlass, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x130108 | VANOS, Einlass: Regelfehler, Position nicht erreicht | 0 | - |
| 0x130201 | VANOS-Magnetventil Auslass, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x130202 | VANOS-Magnetventil Auslass, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x130204 | VANOS-Magnetventil Auslass, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x130308 | VANOS, Auslass: Regelfehler, Position nicht erreicht | 0 | - |
| 0x130401 | VANOS-Magnetventil Einlass 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x130402 | VANOS-Magnetventil Einlass 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x130404 | VANOS-Magnetventil Einlass 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x130508 | VANOS, Einlass 2: Regelfehler, Position nicht erreicht | 0 | - |
| 0x130601 | VANOS-Magnetventil Auslass 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x130602 | VANOS-Magnetventil Auslass 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x130604 | VANOS-Magnetventil Auslass 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x130708 | VANOS, Auslass 2: Regelfehler, Position nicht erreicht | 0 | - |
| 0x130801 | Einlassnockenwelle, Positionsüberwachung: Zahnsprung | 0 | - |
| 0x130901 | Auslassnockenwelle, Positionsüberwachung: Zahnsprung | 0 | - |
| 0x130A01 | Einlassnockenwelle 2, Positionsüberwachung: Zahnsprung | 0 | - |
| 0x130B01 | Auslassnockenwelle 2, Positionsüberwachung: Zahnsprung | 0 | - |
| 0x130C01 | Kurbelwelle - Einlassnockenwelle, Referenz: Winkelunterschied außerhalb Grenzwert | 0 | - |
| 0x130D01 | Kurbelwelle - Auslassnockenwelle, Referenz: Winkelunterschied außerhalb Grenzwert | 0 | - |
| 0x130E01 | Kurbelwelle - Einlassnockenwelle, Synchronisation: Nockenwellensignal außerhalb Grenzwert | 0 | - |
| 0x130F01 | Kurbelwelle - Auslassnockenwelle, Synchronisation: Nockenwellensignal außerhalb Grenzwert | 0 | - |
| 0x131001 | Kurbelwelle - Einlassnockenwelle 2, Referenz: Winkelunterschied außerhalb Grenzwert | 0 | - |
| 0x131101 | Kurbelwelle - Auslassnockenwelle 2, Referenz: Winkelunterschied außerhalb Grenzwert | 0 | - |
| 0x131201 | Kurbelwelle - Einlassnockenwelle 2, Synchronisation: Nockenwellensignal außerhalb Grenzwert | 0 | - |
| 0x131301 | Kurbelwelle - Auslassnockenwelle 2, Synchronisation: Nockenwellensignal außerhalb Grenzwert | 0 | - |
| 0x131401 | VANOS, Auslass, Kaltstart: nicht regelbar | 0 | - |
| 0x131408 | VANOS, Auslass, Kaltstart: nicht regelbar | 0 | - |
| 0x131501 | VANOS, Einlass, Kaltstart: nicht regelbar | 0 | - |
| 0x131508 | VANOS, Einlass, Kaltstart: nicht regelbar | 0 | - |
| 0x131601 | VANOS, Auslass 2, Kaltstart: nicht regelbar | 0 | - |
| 0x131608 | VANOS, Auslass 2, Kaltstart: nicht regelbar | 0 | - |
| 0x131701 | VANOS, Einlass 2, Kaltstart: nicht regelbar | 0 | - |
| 0x131708 | VANOS, Einlass 2, Kaltstart: nicht regelbar | 0 | - |
| 0x131808 | VANOS, Auslass, Kaltstart: Position nicht erreicht | 0 | - |
| 0x131908 | VANOS, Einlass, Kaltstart: Position nicht erreicht | 0 | - |
| 0x132808 | VANOS, Auslass 2, Kaltstart: Position nicht erreicht | 0 | - |
| 0x132908 | VANOS, Einlass 2, Kaltstart: Position nicht erreicht | 0 | - |
| 0x138101 | Abgasklappe, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x138102 | Abgasklappe, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x138104 | Abgasklappe, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x138201 | Kühlerjalousie, oben, Versorgungsspannung, Eigendiagnose: Fehlfunktion | 0 | - |
| 0x138301 | Kühlerjalousie, oben, Eigendiagnose: Übertemperatur erkannt | 0 | - |
| 0x138401 | Kühlerjalousie, oben, Eigendiagnose: elektrischer Fehler | 0 | - |
| 0x138501 | Kühlerjalousie, oben: unterer Anschlag nicht erkannt | 0 | - |
| 0x138601 | Kühlerjalousie, oben: oberer Anschlag nicht erkannt | 0 | - |
| 0x138701 | Kühlerjalousie, oben: oberer Anschlag zu früh erkannt | 0 | - |
| 0x138901 | Kühlerjalousie, unten, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x138902 | Kühlerjalousie, unten, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x138904 | Kühlerjalousie, unten, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x138A01 | Abgasklappe 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x138A02 | Abgasklappe 2, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x138A04 | Abgasklappe 2, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x139001 | Lambdasonde nach Katalysator, von Fett nach Mager: verzögerte Reaktion | 0 | - |
| 0x140001 | Verbrennungsaussetzer, mehrere Zylinder: Einspritzung wird abgeschaltet | 0 | - |
| 0x140002 | Verbrennungsaussetzer, mehrere Zylinder: abgasschädigend nach Startvorgang | 0 | - |
| 0x140004 | Verbrennungsaussetzer, mehrere Zylinder: abgasschädigend | 0 | - |
| 0x140008 | Verbrennungsaussetzer, mehrere Zylinder: Summenfehler | 0 | - |
| 0x140101 | Verbrennungsaussetzer, Zylinder 1: Einspritzung wird abgeschaltet | 0 | - |
| 0x140102 | Verbrennungsaussetzer, Zylinder 1: abgasschädigend nach Startvorgang | 0 | - |
| 0x140104 | Verbrennungsaussetzer, Zylinder 1: abgasschädigend | 0 | - |
| 0x140201 | Verbrennungsaussetzer, Zylinder 2: Einspritzung wird abgeschaltet | 0 | - |
| 0x140202 | Verbrennungsaussetzer, Zylinder 2: abgasschädigend nach Startvorgang | 0 | - |
| 0x140204 | Verbrennungsaussetzer, Zylinder 2: abgasschädigend | 0 | - |
| 0x140301 | Verbrennungsaussetzer, Zylinder 3: Einspritzung wird abgeschaltet | 0 | - |
| 0x140302 | Verbrennungsaussetzer, Zylinder 3: abgasschädigend nach Startvorgang | 0 | - |
| 0x140304 | Verbrennungsaussetzer, Zylinder 3: abgasschädigend | 0 | - |
| 0x140401 | Verbrennungsaussetzer, Zylinder 4: Einspritzung wird abgeschaltet | 0 | - |
| 0x140402 | Verbrennungsaussetzer, Zylinder 4: abgasschädigend nach Startvorgang | 0 | - |
| 0x140404 | Verbrennungsaussetzer, Zylinder 4: abgasschädigend | 0 | - |
| 0x140500 | Verbrennungsaussetzer, Zylinder 5 | 0 | - |
| 0x140501 | Verbrennungsaussetzer, Zylinder 5: Einspritzung wird abgeschaltet | 0 | - |
| 0x140502 | Verbrennungsaussetzer, Zylinder 5: abgasschädigend nach Startvorgang | 0 | - |
| 0x140504 | Verbrennungsaussetzer, Zylinder 5: abgasschädigend | 0 | - |
| 0x140601 | Verbrennungsaussetzer, Zylinder 6: Einspritzung wird abgeschaltet | 0 | - |
| 0x140602 | Verbrennungsaussetzer, Zylinder 6: abgasschädigend nach Startvorgang | 0 | - |
| 0x140604 | Verbrennungsaussetzer, Zylinder 6: abgasschädigend | 0 | - |
| 0x140701 | Verbrennungsaussetzer, Zylinder 7: Einspritzung wird abgeschaltet | 0 | - |
| 0x140702 | Verbrennungsaussetzer, Zylinder 7: abgasschädigend nach Startvorgang | 0 | - |
| 0x140704 | Verbrennungsaussetzer, Zylinder 7: abgasschädigend | 0 | - |
| 0x140801 | Verbrennungsaussetzer, Zylinder 8: Einspritzung wird abgeschaltet | 0 | - |
| 0x140802 | Verbrennungsaussetzer, Zylinder 8: abgasschädigend nach Startvorgang | 0 | - |
| 0x140804 | Verbrennungsaussetzer, Zylinder 8: abgasschädigend | 0 | - |
| 0x140901 | Verbrennungsaussetzer, Zylinder 9: Einspritzung wird abgeschaltet | 0 | - |
| 0x140902 | Verbrennungsaussetzer, Zylinder 9: abgasschädigend nach Startvorgang | 0 | - |
| 0x140904 | Verbrennungsaussetzer, Zylinder 9: abgasschädigend | 0 | - |
| 0x140A01 | Verbrennungsaussetzer, Zylinder 10: Einspritzung wird abgeschaltet | 0 | - |
| 0x140A02 | Verbrennungsaussetzer, Zylinder 10: abgasschädigend nach Startvorgang | 0 | - |
| 0x140A04 | Verbrennungsaussetzer, Zylinder 10: abgasschädigend | 0 | - |
| 0x140B01 | Verbrennungsaussetzer, Zylinder 11: Einspritzung wird abgeschaltet | 0 | - |
| 0x140B02 | Verbrennungsaussetzer, Zylinder 11: abgasschädigend nach Startvorgang | 0 | - |
| 0x140B04 | Verbrennungsaussetzer, Zylinder 11: abgasschädigend | 0 | - |
| 0x140C01 | Verbrennungsaussetzer, Zylinder 12: Einspritzung wird abgeschaltet | 0 | - |
| 0x140C02 | Verbrennungsaussetzer, Zylinder 12: abgasschädigend nach Startvorgang | 0 | - |
| 0x140C04 | Verbrennungsaussetzer, Zylinder 12: abgasschädigend | 0 | - |
| 0x142002 | Verbrennungsaussetzer: Tankfüllstand zu gering | 0 | - |
| 0x143002 | Laufunruhemessung: Messfehler Kurbelwellensensor | 0 | - |
| 0x143108 | Otto Partikelfilter Temperatursensor vor OPF, Bank 1, Plausibilität, Kaltstart: Temperatur unplausibel | 0 | - |
| 0x143208 | Otto Partikelfilter Temperatursensor vor OPF, Bank 2, Plausibilität, Kaltstart: Temperatur unplausibel | 0 | - |
| 0x143308 | Otto Partikelfilter Temperatursensor nach OPF, Bank 2, Plausibilität, Kaltstart: Temperatur unplausibel | 0 | - |
| 0x143408 | Otto Partikelfilter Temperatursensor nach OPF, Bank 1, Plausibilität, Kaltstart: Temperatur unplausibel | 0 | - |
| 0x143501 | Otto Partikelfilter Temperatursensor vor OPF, Bank 1, elektrischer Fehler, Kurzschluss nach Plus oder offene Leitung | 0 | - |
| 0x143502 | Otto Partikelfilter Temperatursensor vor OPF, Bank 1, elektrischer Fehler, Kurzschluss nach Masse | 0 | - |
| 0x143601 | Otto Partikelfilter Temperatursensor vor OPF, Bank 2, elektrischer Fehler, Kurzschluss nach Plus oder offene Leitung | 0 | - |
| 0x143602 | Otto Partikelfilter Temperatursensor vor OPF, Bank 2, elektrischer Fehler, Kurzschluss nach Masse | 0 | - |
| 0x143901 | Otto Partikelfilter Temperatursensor nach OPF, Bank 2, elektrischer Fehler, Kurzschluss nach Plus oder offene Leitung | 0 | - |
| 0x143902 | Otto Partikelfilter Temperatursensor nach OPF, Bank 2, elektrischer Fehler, Kurzschluss nach Masse | 0 | - |
| 0x143B01 | Otto Partikelfilter Temperatursensor nach OPF, Bank 1, elektrischer Fehler, Kurzschluss nach Plus oder offene Leitung | 0 | - |
| 0x143B02 | Otto Partikelfilter Temperatursensor nach OPF, Bank 1, elektrischer Fehler, Kurzschluss nach Masse | 0 | - |
| 0x143D08 | Otto Partikelfilter Temperatursensor vor OPF, Bank 1, Plausibilität: Temperaturgradient zu hoch (Signal springt / Wackelkontakt) | 0 | - |
| 0x143E08 | Otto Partikelfilter Temperatursensor vor OPF, Bank 2, Plausibilität: Temperaturgradient zu hoch (Signal springt / Wackelkontakt) | 0 | - |
| 0x143F08 | Otto Partikelfilter Temperatursensor nach OPF, Bank 2, Plausibilität: Temperaturgradient zu hoch (Signal springt / Wackelkontakt) | 0 | - |
| 0x144008 | Otto Partikelfilter Temperatursensor nach OPF, Bank 1, Plausibilität: Temperaturgradient zu hoch (Signal springt / Wackelkontakt) | 0 | - |
| 0x144108 | Otto Partikelfilter Temperatursensor vor OPF, Bank 1, Plausibilität: Temperaturanstieg unplausibel | 0 | - |
| 0x144208 | Otto Partikelfilter Temperatursensor vor OPF, Bank 2, Plausibilität: Temperaturanstieg unplausibel | 0 | - |
| 0x144308 | Otto Partikelfilter Temperatursensor nach OPF, Bank 2, Plausibilität: Temperaturanstieg unplausibel | 0 | - |
| 0x144408 | Otto Partikelfilter Temperatursensor nach OPF, Bank 1, Plausibilität: Temperaturanstieg unplausibel | 0 | - |
| 0x144501 | Otto Partikelfilter Drucksensor, Bank 1, Drucksensoroffset: Adaptierte Offset unplausibel | 0 | - |
| 0x144601 | Otto Partikelfilter Drucksensor, Bank 2, Drucksensoroffset: Adaptierte Offset unplausibel | 0 | - |
| 0x144701 | Otto Partikelfilter Drucksensor, Bank 1, Drucksensorschlauch: Schlauchanschlüsse vertauscht, diagnostiziert während eines Fahrzyklus | 0 | - |
| 0x144801 | Otto Partikelfilter Drucksensor, Bank 2, Drucksensorschlauch: Schlauchanschlüsse vertauscht, diagnostiziert während eines Fahrzyklus | 0 | - |
| 0x144901 | Otto Partikelfilter Drucksensor, Bank 1, Plausibilität: Differenz des maximalen und minimalen Messwert unplausibel | 0 | - |
| 0x144A01 | Otto Partikelfilter Drucksensor, Bank 2, Plausibilität: Differenz des maximalen und minimalen Messwert unplausibel | 0 | - |
| 0x144B01 | Otto Partikelfilter Drucksensor, Bank 1, Plausibilität: Druck zu hoch im Nachlauf | 0 | - |
| 0x144C01 | Otto Partikelfilter Drucksensor, Bank 2, Plausibilität: Druck zu hoch im Nachlauf | 0 | - |
| 0x144D01 | Otto Partikelfilter Drucksensor, Bank 1, Plausibilität: Druckgradient zu hoch (Signal springt / Wackelkontakt) | 0 | - |
| 0x144E01 | Otto Partikelfilter Drucksensor, Bank 2, Plausibilität: Druckgradient zu hoch (Signal springt / Wackelkontakt) | 0 | - |
| 0x144F01 | Otto Partikelfilter Drucksensor, Bank 1, Versorgungsspannung: unplausibel (zu hoch) | 0 | - |
| 0x144F02 | Otto Partikelfilter Drucksensor, Bank 1, Versorgungsspannung: unplausibel (zu niedrig) | 0 | - |
| 0x145001 | Otto Partikelfilter Drucksensor, Bank 2, Versorgungsspannung: unplausibel (zu hoch) | 0 | - |
| 0x145002 | Otto Partikelfilter Drucksensor, Bank 2, Versorgungsspannung: unplausibel (zu niedrig) | 0 | - |
| 0x145301 | Otto Partikelfilter Drucksensor, Bank 1, Drucksensorschlauch: Schlauchanschlüsse vertauscht, diagnostiziert am Ende des Fahrzyklus | 0 | - |
| 0x145401 | Otto Partikelfilter Drucksensor, Bank 2, Drucksensorschlauch: Schlauchanschlüsse vertauscht, diagnostiziert am Ende des Fahrzyklus | 0 | - |
| 0x145501 | Otto Partikelfilter Drucksensor vor OPF, Bank 1, Drucksensorsschlauch: nicht angeschlossen/abgefallen | 0 | - |
| 0x145601 | Otto Partikelfilter Drucksensor vor OPF, Bank 2, Drucksensorsschlauch: nicht angeschlossen/abgefallen | 0 | - |
| 0x145708 | Otto Partikelfilter, Bank 1, leistungsreduzierter Betrieb: Warnung, wg. kritischer Differenzdruck zwischen OPF | 0 | - |
| 0x145808 | Otto Partikelfilter, Bank 2, leistungsreduzierter Betrieb: Warnung, wg. kritischer Differenzdruck zwischen OPF | 0 | - |
| 0x145908 | Otto Partikelfilter, Bank 1, leistungsreduzierter Betrieb: Fehler, wg. kritischer Differenzdruck zwischen OPF | 0 | - |
| 0x145A08 | Otto Partikelfilter, Bank 2, leistungsreduzierter Betrieb: Fehler, wg. kritischer Differenzdruck zwischen OPF | 0 | - |
| 0x145B08 | Otto Partikelfilter, Bank 1, leistungsreduzierter Betrieb: Warnung, wg. kritischer Rußbeladung im OPF | 0 | - |
| 0x145C08 | Otto Partikelfilter, Bank 2, leistungsreduzierter Betrieb: Warnung, wg. kritischer Rußbeladung im OPF | 0 | - |
| 0x145D08 | Otto Partikelfilter, Bank 1, leistungsreduzierter Betrieb: Fehler, wg. kritischer Rußbeladung im OPF | 0 | - |
| 0x145E08 | Otto Partikelfilter, Bank 2, leistungsreduzierter Betrieb: Fehler, wg. kritischer Rußbeladung im OPF | 0 | - |
| 0x145F08 | Otto Partikelfilter, Bank 1, kritsch überlastet von Ruß und Asche | 0 | - |
| 0x146008 | Otto Partikelfilter, Bank 2, kritsch überlastet von Ruß und Asche | 0 | - |
| 0x146108 | Otto Partikelfilter, Bank 1, überlastet von Ruß und Asche | 0 | - |
| 0x146208 | Otto Partikelfilter, Bank 2, überlastet von Ruß und Asche | 0 | - |
| 0x146308 | Otto Partikelfilter, Bank 1, kritisch überlastet von Ruß und Asche mit der Anforderung Partikelfilter muss getauscht werden | 0 | - |
| 0x146408 | Otto Partikelfilter, Bank 2, kritisch überlastet von Ruß und Asche mit der Anforderung Partikelfilter muss getauscht werden | 0 | - |
| 0x146508 | Otto Partikelfilter, Bank 1, kritisch überlastet von Asche innerhalb von nächsten Service mit der Anforderung, dass Partikelfilter muss präventiv getauscht werden | 0 | - |
| 0x146608 | Otto Partikelfilter, Bank 2, kritisch überlastet von Asche innerhalb von nächsten Service mit der Anforderung, dass Partikelfilter muss präventiv getauscht werden | 0 | - |
| 0x146708 | Otto Partikelfilter, Bank 1: Partikelfilter ausgebaut | 0 | - |
| 0x146808 | Otto Partikelfilter, Bank 2: Partikelfilter ausgebaut | 0 | - |
| 0x150102 | Zündung, Zylinder 1: Brenndauer zu kurz | 0 | - |
| 0x150202 | Zündung, Zylinder 2: Brenndauer zu kurz | 0 | - |
| 0x150302 | Zündung, Zylinder 3: Brenndauer zu kurz | 0 | - |
| 0x150402 | Zündung, Zylinder 4: Brenndauer zu kurz | 0 | - |
| 0x150502 | Zündung, Zylinder 5: Brenndauer zu kurz | 0 | - |
| 0x150602 | Zündung, Zylinder 6: Brenndauer zu kurz | 0 | - |
| 0x150702 | Zündung, Zylinder 7: Brenndauer zu kurz | 0 | - |
| 0x150802 | Zündung, Zylinder 8: Brenndauer zu kurz | 0 | - |
| 0x150902 | Zündung, Zylinder 9: Brenndauer zu kurz | 0 | - |
| 0x150A02 | Zündung, Zylinder 10: Brenndauer zu kurz | 0 | - |
| 0x150B02 | Zündung, Zylinder 11: Brenndauer zu kurz | 0 | - |
| 0x150C02 | Zündung, Zylinder 12: Brenndauer zu kurz | 0 | - |
| 0x151001 | Zündwinkelverstellung im Leerlauf, Kaltstart: Zündwinkel zu früh | 0 | - |
| 0x151100 | Zündwinkelverstellung in Teillast, Kaltstart | 0 | - |
| 0x151101 | Zündwinkelverstellung in Teillast, Kaltstart: Zündwinkel zu früh | 0 | - |
| 0x151200 | Zündwinkelverstellung 2 im Leerlauf, Kaltstart | 0 | - |
| 0x151201 | Zündwinkelverstellung 2 im Leerlauf, Kaltstart: Zündwinkel zu früh | 0 | - |
| 0x151300 | Zündwinkelverstellung 2 in Teillast, Kaltstart | 0 | - |
| 0x151301 | Zündwinkelverstellung 2 in Teillast, Kaltstart: Zündwinkel zu früh | 0 | - |
| 0x152008 | Zündkreis, Versorgungsspannung: Bankausfall oder Motorausfall | 0 | - |
| 0x152108 | Superklopfen, Zylinder 1: Einspritzungsabschaltung | 0 | - |
| 0x152208 | Superklopfen, Zylinder 2: Einspritzungsabschaltung | 0 | - |
| 0x152308 | Superklopfen, Zylinder 3: Einspritzungsabschaltung | 0 | - |
| 0x152408 | Superklopfen, Zylinder 4: Einspritzungsabschaltung | 0 | - |
| 0x152508 | Superklopfen, Zylinder 5: Einspritzungsabschaltung | 0 | - |
| 0x152608 | Superklopfen, Zylinder 6: Einspritzungsabschaltung | 0 | - |
| 0x152708 | Superklopfen, Zylinder 7: Einspritzungsabschaltung | 0 | - |
| 0x152808 | Superklopfen, Zylinder 8: Einspritzungsabschaltung | 0 | - |
| 0x152908 | Superklopfen, Zylinder 9: Einspritzungsabschaltung | 0 | - |
| 0x152A08 | Superklopfen, Zylinder 10: Einspritzungsabschaltung | 0 | - |
| 0x152B08 | Superklopfen, Zylinder 11: Einspritzungsabschaltung | 0 | - |
| 0x152C08 | Superklopfen, Zylinder 12: Einspritzungsabschaltung | 0 | - |
| 0x156101 | Zündspule Zylinder 1, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156201 | Zündspule Zylinder 2, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156301 | Zündspule Zylinder 3, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156401 | Zündspule Zylinder 4, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156501 | Zündspule Zylinder 5, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156601 | Zündspule Zylinder 6, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156701 | Zündspule Zylinder 7, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156801 | Zündspule Zylinder 8, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156901 | Zündspule Zylinder 9, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156A01 | Zündspule Zylinder 10, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156B01 | Zündspule Zylinder 11, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x156C01 | Zündspule Zylinder 12, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x160001 | Kurbelwellensensor, Signal: fehlt | 0 | - |
| 0x160002 | Kurbelwellensensor, Signal: unplausibel | 0 | - |
| 0x160101 | Kurbelwellensensor, Synchronisation: Fehlfunktion | 0 | - |
| 0x160201 | Kurbelwellensensorsignal, Zahnfehler: Zähnezahl falsch | 0 | - |
| 0x160301 | Kurbelwellensensorsignal, Lückenfehler: Zahnzeit unplausibel | 0 | - |
| 0x160402 | Kurbelwellensensor, Segmentadaption: Grenzwert überschritten | 0 | - |
| 0x162001 | Einlassnockenwellensensor, Synchronisation: Fehlfunktion | 0 | - |
| 0x162101 | Einlassnockenwellensensor, elektrisch: Signal fehlt | 0 | - |
| 0x162201 | Einlassnockenwellensensor, Funktion: Segmentzeitfehler | 0 | - |
| 0x162301 | Einlassnockenwellensensor 2, Synchronisation: Fehlfunktion | 0 | - |
| 0x162401 | Einlassnockenwellensensor 2, elektrisch: Signal fehlt | 0 | - |
| 0x162501 | Einlassnockenwellensensor 2, Funktion: Segmentzeitfehler | 0 | - |
| 0x163101 | Auslassnockenwellensensor, Synchronisation: Fehlfunktion | 0 | - |
| 0x163201 | Auslassnockenwellensensor, elektrisch: Signal fehlt | 0 | - |
| 0x163301 | Auslassnockenwellensensor, Funktion: Segmentzeitfehler | 0 | - |
| 0x163401 | Auslassnockenwellensensor 2, Synchronisation: Fehlfunktion | 0 | - |
| 0x163501 | Auslassnockenwellensensor 2, elektrisch: Signal fehlt | 0 | - |
| 0x163601 | Auslassnockenwellensensor 2, Funktion: Segmentzeitfehler | 0 | - |
| 0x168001 | Klopfsensor 1, Signal: Motorgeräusch über Grenzwert | 0 | - |
| 0x168002 | Klopfsensor 1, Signal: Motorgeräusch unter Grenzwert | 0 | - |
| 0x168008 | Klopfsensor 1, Signal: unplausibel | 0 | - |
| 0x168101 | Klopfsensor 2, Signal: Motorgeräusch über Grenzwert | 0 | - |
| 0x168102 | Klopfsensor 2, Signal: Motorgeräusch unter Grenzwert | 0 | - |
| 0x168108 | Klopfsensor 2, Signal: unplausibel | 0 | - |
| 0x168201 | Klopfsensor 3, Signal: Motorgeräusch über Grenzwert | 0 | - |
| 0x168202 | Klopfsensor 3, Signal: Motorgeräusch unter Grenzwert oder Leitungsunterbrechung | 0 | - |
| 0x168208 | Klopfsensor 3, Signal: unplausibel | 0 | - |
| 0x168301 | Klopfsensor 4, Signal: Motorgeräusch über Grenzwert | 0 | - |
| 0x168302 | Klopfsensor 4, Signal: Motorgeräusch unter Grenzwert oder Leitungsunterbrechung | 0 | - |
| 0x168308 | Klopfsensor 4, Signal: unplausibel | 0 | - |
| 0x168401 | Klopfsensor 5, Signal: Motorgeräusch über Grenzwert | 0 | - |
| 0x168402 | Klopfsensor 5, Signal: Motorgeräusch unter Grenzwert | 0 | - |
| 0x168408 | Klopfsensor 5, Signal: unplausibel | 0 | - |
| 0x168501 | Klopfsensor 6, Signal: Motorgeräusch über Grenzwert | 0 | - |
| 0x168502 | Klopfsensor 6, Signal: Motorgeräusch unter Grenzwert | 0 | - |
| 0x168508 | Klopfsensor 6, Signal: unplausibel | 0 | - |
| 0x170301 | Sekundärluftpumpe, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x170302 | Sekundärluftpumpe, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x170304 | Sekundärluftpumpe, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x170401 | Differenzdrucksensor, Sekundärluft, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x170402 | Differenzdrucksensor, Sekundärluft, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x170404 | Differenzdrucksensor, Sekundärluft, elektrisch: Leitungsunterbrechung | 0 | - |
| 0x170501 | Differenzdrucksensor 2, Sekundärluft, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x170502 | Differenzdrucksensor 2, Sekundärluft, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x170504 | Differenzdrucksensor 2, Sekundärluft, elektrisch: Leitungsunterbrechung | 0 | - |
| 0x170604 | Differenzdrucksensor, Sekundärluft, Initialisierung: Druck außerhalb gültigem Bereich | 0 | - |
| 0x170608 | Differenzdrucksensor, Sekundärluft, Initialisierung: Druckdifferenz zwischen zwei Fahrzyklen unplausibel | 0 | - |
| 0x170704 | Differenzdrucksensor 2, Sekundärluft, Initialisierung: Druck außerhalb gültigem Bereich | 0 | - |
| 0x170708 | Differenzdrucksensor 2, Sekundärluft, Initialisierung: Druckdifferenz zwischen zwei Fahrzyklen unplausibel | 0 | - |
| 0x170808 | Sekundärluftleitung: Leistung Sekundärluftpumpe zu gering | 0 | - |
| 0x170908 | Sekundärluftleitung 2: Leistung Sekundärluftpumpe zu gering | 0 | - |
| 0x170A08 | Sekundärluftleitung: Luftmassenstrom zu gering | 0 | - |
| 0x170B08 | Sekundärluftleitung 2: Luftmassenstrom zu gering | 0 | - |
| 0x170C08 | Sekundärluftleitung: Undichtigkeit erkannt | 0 | - |
| 0x170D08 | Sekundärluftleitung 2: Undichtigkeit erkannt | 0 | - |
| 0x174208 | Sekundärluftventil: klemmt geschlossen | 0 | - |
| 0x174308 | Sekundärluftventil 2: klemmt geschlossen | 0 | - |
| 0x174408 | Sekundärluftventil: klemmt offen | 0 | - |
| 0x174508 | Sekundärluftventil 2: klemmt offen | 0 | - |
| 0x180001 | Katalysator: Wirkungsgrad unterhalb Grenzwert | 0 | - |
| 0x180002 | Katalysator: defekt | 0 | - |
| 0x180008 | Katalysator: Wirkungsgrad unterhalb Grenzwert (nicht validiert) | 0 | - |
| 0x180101 | Katalysator 2: Wirkungsgrad unterhalb Grenzwert | 0 | - |
| 0x180102 | Katalysator 2: defekt | 0 | - |
| 0x180108 | Katalysator 2: Wirkungsgrad unterhalb Grenzwert (nicht validiert) | 0 | - |
| 0x190001 | DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x190002 | DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x190004 | DMTL-Magnetventil, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x190201 | Tankentlüftungs- und Spülluftsystem, Feinleck: Leckage größer 1,0 mm | 0 | - |
| 0x190302 | Tankentlüftungs- und Spülluftsystem, Feinstleck: Leckage größer 0,5 mm | 0 | - |
| 0x190401 | DMTL, Systemfehler: Pumpenstrom zu groß bei Referenzmessung | 0 | - |
| 0x190402 | DMTL, Systemfehler: Pumpenstrom zu klein bei Referenzmessung | 0 | - |
| 0x190404 | DMTL, Systemfehler: Abbruch wegen Stromschwankungen bei Referenzmessung | 0 | - |
| 0x190408 | DMTL, Systemfehler: Pumpenstrom bei Ventilprüfung erreicht Grenzwert | 0 | - |
| 0x190501 | DMTL, Heizung, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x190502 | DMTL, Heizung, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x190504 | DMTL, Heizung, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x190601 | DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x190702 | DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x190704 | DMTL-Leckdiagnosepumpe, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x190802 | DMTL, Systemfehler: Pumpenstrom zu klein bei Referenzmessung | 0 | - |
| 0x190904 | DMTL, Systemfehler: Abbruch wegen Stromschwankungen bei Referenzmessung | 0 | - |
| 0x190A08 | DMTL, Systemfehler: Pumpenstrom bei Ventilprüfung erreicht Grenzwert | 0 | - |
| 0x190F04 | Tankentlüftungssystem: Fehlfunktion Bandende | 0 | - |
| 0x190F08 | Tankentlüftungssystem: Fehlfunktion | 0 | - |
| 0x191001 | Tankentlüftungsventil, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x191002 | Tankentlüftungsventil, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x191004 | Tankentlüftungsventil, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x191F00 | Entlüftung zwischen Tank und AKF | 0 | - |
| 0x191F02 | Entlüftung zwischen Tank und AKF: blockiert | 0 | - |
| 0x191F08 | Entlüftung zwischen Tank und AKF: blockiert | 0 | - |
| 0x193001 | Tankfüllstandssensor, links, Signal: Kurzschluss nach Plus oder Leitungsunterbrechung | 1 | - |
| 0x193002 | Tankfüllstandssensor, links, Signal: Kurzschluss nach Masse | 1 | - |
| 0x193008 | Tankfüllstandssensor, links, Signal: CAN Wert unplausibel | 1 | - |
| 0x193101 | Tankfüllstandssensor, rechts, Signal: Kurzschluss nach Plus oder Leitungsunterbrechung | 1 | - |
| 0x193102 | Tankfüllstandssensor, rechts, Signal: Kurzschluss nach Masse | 1 | - |
| 0x193108 | Tankfüllstandssensor, rechts, Signal: CAN Wert unplausibel | 1 | - |
| 0x193208 | Tankfüllstand, Plausibilität: unplausibel zu Verbrauchswert | 0 | - |
| 0x1A2001 | Elektrolüfter, Ansteuerungsleitung: Kurzschluss nach Plus | 0 | - |
| 0x1A2002 | Elektrolüfter, Ansteuerungsleitung: Kurzschluss nach Masse | 0 | - |
| 0x1A2004 | Elektrolüfter, Ansteuerungsleitung: Leitungsunterbrechung | 0 | - |
| 0x1A2108 | Elektrolüfter, Eigendiagnose Stufe 1: leichter Lüfterfehler | 0 | - |
| 0x1A2308 | Elektrolüfter, Eigendiagnose Stufe 2: Lüfterfehler mit potentieller Gefährdung für den Lüfter | 0 | - |
| 0x1A2408 | Elektrolüfter, Eigendiagnose Stufe 3: Lüfterfehler mit Motorfunktionseinschränkung | 0 | - |
| 0x1A2508 | Elektrolüfter, Eigendiagnose Stufe 4: schwerer Lüfterfehler | 0 | - |
| 0x1A2601 | Abschaltrelais Elektrolüfter, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x1A2602 | Abschaltrelais Elektrolüfter, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x1A2604 | Abschaltrelais Elektrolüfter, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x1B0004 | Fahrzeuggeschwindigkeit, Signal: fehlt | 0 | - |
| 0x1B0108 | Fahrzeuggeschwindigkeit, Plausibilität: Signal unplausibel | 0 | - |
| 0x1B0204 | Fahrzeuggeschwindigkeit, Plausibilität: Geschwindigkeit unplausibel oder CAN-Bus Kommunikation gestört | 1 | - |
| 0x1B0301 | Fahrzeuggeschwindigkeit, Plausibilität: Geschwindigkeit zu niedrig bei niedrigem Lastzustand | 1 | - |
| 0x1B0401 | Fahrzeuggeschwindigkeit, Signaländerung: unplausibel | 1 | - |
| 0x1B0501 | Fahrzeuggeschwindigkeit, Signal: festliegend auf Null | 1 | - |
| 0x1B0601 | Fahrzeuggeschwindigkeit, Signal: festliegend | 1 | - |
| 0x1B0701 | Fahrzeuggeschwindigkeit, Plausibilität: Geschwindigkeit zu hoch | 1 | - |
| 0x1B0808 | Fahrzeuggeschwindigkeit, Plausibilität: Geschwindigkeitssignal unplausibel | 0 | - |
| 0x1B0B01 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/links, Signaländerung: unplausibel | 1 | - |
| 0x1B0C01 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/rechts, Signaländerung: unplausibel | 1 | - |
| 0x1B0D01 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/links, Signaländerung: unplausibel | 1 | - |
| 0x1B0E01 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/rechts, Signaländerung: unplausibel | 1 | - |
| 0x1B2002 | EWS Manipulationsschutz: kein Startwert programmiert | 0 | - |
| 0x1B2008 | EWS Manipulationsschutz: Antwort unplausibel | 0 | - |
| 0x1B2101 | Schnittstelle EWS-DME: Hardwarefehler | 0 | - |
| 0x1B2102 | Schnittstelle EWS-DME: Framefehler | 0 | - |
| 0x1B2104 | Schnittstelle EWS-DME: Zeitüberschreitung | 0 | - |
| 0x1B2108 | Schnittstelle EWS-DME: Prüfsummenfehler | 0 | - |
| 0x1B2201 | DME, interner Fehler, EWS-Daten: keine verfügbare Speichermöglichkeit | 0 | - |
| 0x1B2202 | DME, interner Fehler, EWS-Daten: Fehlerfreischaltcodeablage | 0 | - |
| 0x1B2204 | DME, interner Fehler, EWS-Daten: Startwert zerstört/ 2- aus 3-Auswahl fehlgeschlagen | 0 | - |
| 0x1B2208 | DME, interner Fehler, EWS-Daten: Prüfsummenfehler | 0 | - |
| 0x1B2302 | FA-CAN, Botschaft (EWS Dienst DME1/DDE1, 0x5C0): Framefehler | 1 | - |
| 0x1B2304 | FA-CAN, Botschaft (EWS Dienst DME1/DDE1, 0x5C0): fehlt | 1 | - |
| 0x1B2401 | FlexRay, Botschaft (EWS Response Master, 251.0.8): Typfehler | 1 | - |
| 0x1B2501 | FlexRay, Botschaft (EWS Response Master, 251.0.8): fehlt | 1 | - |
| 0x1B2601 | FlexRay, Botschaft (EWS Challenge Slave, 251.4.8): Typfehler | 1 | - |
| 0x1B2701 | FlexRay, Botschaft (EWS Response Master, 251.0.8): Framefehler | 1 | - |
| 0x1B2A01 | DME-Sperrung, Slave: EWS nicht freigeschalten | 0 | - |
| 0x1B5001 | Überwachung Klemme 15: Wake-up-Leitung Kurzschluss nach Plus | 0 | - |
| 0x1B5002 | Überwachung Klemme 15: Wake-up-Leitung Kurzschluss nach Masse | 0 | - |
| 0x1B5004 | Überwachung Klemme 15: Botschaft vom CAS fehlt oder fehlerhaft | 0 | - |
| 0x1B5008 | Überwachung Klemme 15: Signal Wake-up-Leitung unplausibel zur Botschaft CAS Klemmenstatus | 0 | - |
| 0x1B5101 | Klemme 15_3, Leitung vom CAS, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x1B5102 | Klemme 15_3, Leitung vom CAS, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x1B9104 | Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi unplausibel im Motorlauf/Nachlauf | 0 | - |
| 0x1B9208 | Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi unplausibel im Wake-up | 0 | - |
| 0x1B9308 | Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi unplausibel im Motorlauf | 0 | - |
| 0x1B9408 | Motorabstellzeit, Zeitzähler Kombi - Zeitzähler DME, Vergleich: Wert Zeitzähler Kombi unplausibel im Nachlauf | 0 | - |
| 0x1B9508 | Motorabstellzeit, Plausibilität: Zeit zu kurz in Korrelation zu Motorkühlmittel-Abkühlung | 0 | - |
| 0x1B9608 | Motorabstellzeit, Plausibilität: Zeit zu lang in Korrelation zu Motorkühlmittel-Abkühlung | 0 | - |
| 0x1BAF08 | Fahrpedalmodul - Bremspedal, Vergleich: Pedalwerte zueinander unplausibel | 0 | - |
| 0x1BD401 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/links, elektrisch: Kurzschluss nach Plus | 1 | - |
| 0x1BD402 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/links, elektrisch: Kurzschluss nach Masse | 1 | - |
| 0x1BD404 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/links, elektrisch: Leitungsunterbrechung | 1 | - |
| 0x1BD408 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/links, elektrisch: Fehlfunktion | 0 | - |
| 0x1BD501 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/links, elektrisch: Kurzschluss nach Plus | 1 | - |
| 0x1BD502 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/links, elektrisch: Kurzschluss nach Masse | 1 | - |
| 0x1BD504 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/links, elektrisch: Leitungsunterbrechung | 1 | - |
| 0x1BD508 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/links, elektrisch: Fehlfunktion | 0 | - |
| 0x1BD601 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/rechts, elektrisch: Kurzschluss nach Plus | 1 | - |
| 0x1BD602 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/rechts, elektrisch: Kurzschluss nach Masse | 1 | - |
| 0x1BD604 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/rechts, elektrisch: Leitungsunterbrechung | 1 | - |
| 0x1BD608 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor hinten/rechts, elektrisch: Fehlfunktion | 0 | - |
| 0x1BD701 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/rechts, elektrisch: Kurzschluss nach Plus | 1 | - |
| 0x1BD702 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/rechts, elektrisch: Kurzschluss nach Masse | 1 | - |
| 0x1BD704 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/rechts, elektrisch: Leitungsunterbrechung | 1 | - |
| 0x1BD708 | Fahrzeuggeschwindigkeit, Raddrehzahlsensor vorn/rechts, elektrisch: Fehlfunktion | 0 | - |
| 0x1C3204 | Motoröldruckschalter: Leitungsunterbrechung oder Schalter klemmt | 0 | - |
| 0x1C4002 | Thermischer Ölniveausensor: Niveau zu niedrig | 0 | - |
| 0x1C4102 | Motorölniveau: zu niedrig | 0 | - |
| 0x1C5001 | Ölzustandssensor: Temperaturmessung | 0 | - |
| 0x1C5002 | Ölzustandssensor: Niveaumessung | 0 | - |
| 0x1C5004 | Ölzustandssensor: Kommunikationsfehler | 0 | - |
| 0x1C5008 | Ölzustandssensor: Permittivitätsfehler | 0 | - |
| 0x1C5104 | Ölzustandssensor, Kommunikation: keine Kommunikation | 0 | - |
| 0x1D2008 | Kennfeldthermostat: klemmt offen | 0 | - |
| 0x1D2204 | Kennfeldthermostat, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x1D2301 | Kennfeldthermostat, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x1D2401 | Kennfeldthermostat, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x1D2402 | Kennfeldthermostat, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x1D2404 | Kennfeldthermostat, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x1D3701 | Schaltzeitpunkt: Anpassung | 1 | - |
| 0x1D3901 | EGS, Signalüberwachung (Turbinendrehzahl): ungültiger Signalinhalt | 1 | - |
| 0x1D3A01 | EGS, Signalüberwachung (Drehzahl Abtrieb): ungültiger Signalinhalt | 1 | - |
| 0x1D3B01 | EGS, Signalüberwachung (Ganginformation): ungültiger Signalinhalt | 1 | - |
| 0x1D3C01 | EGS, Signalüberwachung (Status Schaltvorgang): ungültiger Signalinhalt | 1 | - |
| 0x1E0001 | Leerlaufregelung: Drehzahl zu hoch | 0 | - |
| 0x1E0002 | Leerlaufregelung: Drehzahl zu niedrig | 0 | - |
| 0x1E0101 | Leerlaufregelung, Kaltstart: Drehzahl zu hoch | 0 | - |
| 0x1E0102 | Leerlaufregelung, Kaltstart: Drehzahl zu niedrig | 0 | - |
| 0x1E0308 | Leerlaufregelung, Plausibilität, Kaltstart: Drehzahl unplausibel | 0 | - |
| 0x1E5008 | Drehmomentüberwachung: Plausibilität | 0 | - |
| 0x1E5108 | Motordrehmoment, Anforderung über CAN: nicht erfüllbar | 0 | - |
| 0x1E5201 | Drehzahlbegrenzung bei stehendem Fahrzeug: Leerlaufdrehzahl zu lange zu hoch | 0 | - |
| 0x1F0001 | DME, interner Fehler, RAM: RAM-Baustein | 0 | - |
| 0x1F0002 | DME, interner Fehler, RAM: Sicherheitsrechner RAM | 0 | - |
| 0x1F0101 | DME, interner Fehler, Prüfsumme: Bootsoftware | 0 | - |
| 0x1F0102 | DME, interner Fehler, Prüfsumme: Applikationssoftware | 0 | - |
| 0x1F0104 | DME, interner Fehler, Prüfsumme: Datenbereich | 0 | - |
| 0x1F0201 | DME, interner Fehler, NVMY-Prüfsumme: NVMY-Überprüfung | 0 | - |
| 0x1F0304 | DME, interner Fehler, Klopfsensorbaustein: SPI-Kommunikation gestört | 0 | - |
| 0x1F0404 | DME, interner Fehler, Mehrfachendstufenbaustein: SPI-Kommunikation gestört | 0 | - |
| 0x1F0502 | Klemme 15N vom CAS, Signal: nicht geschaltet | 0 | - |
| 0x1F0601 | Klemme 15N vom CAS, Schaltverzögerung: schaltet zu spät | 0 | - |
| 0x1F0801 | Warm Reset Diagnose: Geplanter Software Reset | 0 | - |
| 0x1F0802 | Warm Reset Diagnose: unerwünschter Software Reset | 0 | - |
| 0x1F0804 | Warm Reset Diagnose: Power On Reset | 0 | - |
| 0x1F0808 | Warm Reset Diagnose: Hardware Reset | 0 | - |
| 0x1F1004 | Master/Slave Kohärenz: Programmstände ungleich | 0 | - |
| 0x1F1008 | Master/Slave Kohärenz: Datenstände ungleich | 0 | - |
| 0x1F1108 | Master/Slave Umschaltung: maximale Anzahl Umschaltungen überschritten | 0 | - |
| 0x1F1208 | Master/Slave Erkennung: Erkennung nicht möglich | 0 | - |
| 0x1F1308 | Master/Slave NVMY Status: Speichern oder Auslesen des Status nicht möglich | 0 | - |
| 0x1F1508 | Master/Slave Erkennung: Erkennung nicht möglich | 0 | - |
| 0x1F1601 | DME, Nachlauf: unvollständiges Herunterfahren erkannt | 0 | - |
| 0x1F2004 | Kodierung fehlt: Kodierdaten im EEPROM fehlerhaft | 0 | - |
| 0x1F2008 | Kodierung fehlt: keine Kodierung nach Programmierung | 0 | - |
| 0x1F2104 | Falscher Datensatz: CAN Timeout | 0 | - |
| 0x1F2108 | Falscher Datensatz: Variantenüberwachung | 0 | - |
| 0x1F2201 | Injektoren Gruppe 1 oder DME, interner Fehler: Initialisierungsfehler | 0 | - |
| 0x1F2202 | Injektoren Gruppe 1 oder DME, interner Fehler: Leitungsunterbrechung | 0 | - |
| 0x1F2204 | Injektoren Gruppe 1 oder DME, interner Fehler: Entladungsfehler | 0 | - |
| 0x1F2301 | Injektoren Gruppe 2 oder DME, interner Fehler: Initialisierungsfehler | 0 | - |
| 0x1F2302 | Injektoren Gruppe 2 oder DME, interner Fehler: Leitungsunterbrechung | 0 | - |
| 0x1F2304 | Injektoren Gruppe 2 oder DME, interner Fehler: Entladungsfehler | 0 | - |
| 0x1F2401 | Injektoren Gruppe 3 oder DME, interner Fehler: Initialisierungsfehler | 0 | - |
| 0x1F2402 | Injektoren Gruppe 3 oder DME, interner Fehler: Leitungsunterbrechung | 0 | - |
| 0x1F2404 | Injektoren Gruppe 3 oder DME, interner Fehler: Entladungsfehler | 0 | - |
| 0x1F2501 | Injektoren Gruppe 4 oder DME, interner Fehler: Initialisierungsfehler | 0 | - |
| 0x1F2502 | Injektoren Gruppe 4 oder DME, interner Fehler: Leitungsunterbrechung | 0 | - |
| 0x1F2504 | Injektoren Gruppe 4 oder DME, interner Fehler: Entladungsfehler | 0 | - |
| 0x1F2601 | Kodierung: falsche Variante kodiert | 0 | - |
| 0x1F2602 | Kodierung: Variante fehlt | 0 | - |
| 0x1F2701 | Kodierung: Fehler beim Schreiben der Variante | 0 | - |
| 0x1F2702 | Kodierung: Variantenprüfung fehlerhaft | 0 | - |
| 0x1F2704 | Kodierung: Unplausible Variante | 0 | - |
| 0x1F2801 | DME, Software: Programm ungültig | 0 | - |
| 0x1F2802 | DME, Software: Daten ungültig | 0 | - |
| 0x1F2804 | DME, Software: Programm und Daten ungültig | 0 | - |
| 0x1F2901 | DME Slave, Software: Programm ungültig | 0 | - |
| 0x1F2902 | DME Slave, Software: Daten ungültig | 0 | - |
| 0x1F2904 | DME Slave, Software: Programm und Daten ungültig | 0 | - |
| 0x1F3008 | DME, interner Fehler, Fahrpedalmodul: Spannungsversorgung Pedalwertgeber 1 | 0 | - |
| 0x1F3108 | DME, interner Fehler, Fahrpedalmodul: Spannungsversorgung Pedalwertgeber 2 | 0 | - |
| 0x1F4001 | Startautomatik, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x1F4002 | Startautomatik, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x1F4004 | Startautomatik, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x1F4A04 | Entlastungsrelais für Zündung und Einspritzung: nicht abgefallen | 0 | - |
| 0x1F4A08 | Entlastungsrelais für Zündung und Einspritzung: nicht angezogen | 0 | - |
| 0x1F4B08 | Entlastungsrelais für Zündung und Einspritzung, Schaltverzögerung: schaltet zu spät | 0 | - |
| 0x1F4C01 | Relais Mengensteuerventil: Kurzschluss nach Plus | 0 | - |
| 0x1F4C02 | Relais Mengensteuerventil: Kurzschluss nach Masse | 0 | - |
| 0x1F4C04 | Relais Mengensteuerventil: Leitungsunterbrechung | 0 | - |
| 0x1F4E04 | Relais 2 Zündung und Injektoren: nicht abgefallen | 0 | - |
| 0x1F4E08 | Relais 2 Zündung und Injektoren: nicht angezogen | 0 | - |
| 0x1F4F08 | Relais 2 Zündung und Injektoren, Schaltverzögerung: schaltet zu spät | 0 | - |
| 0x1F5001 | DME, interner Fehler, Innentemperatursensor, elektrisch: Kurzschluss nach Plus | 0 | - |
| 0x1F5002 | DME, interner Fehler, Innentemperatursensor, elektrisch: Kurzschluss nach Masse | 0 | - |
| 0x200004 | DME, interner Fehler, Überwachung Fahrgeschwindigkeitsregelung: LDM Überwachung | 0 | - |
| 0x200108 | DME, interner Fehler, Überwachung Motordrehzahl: Fehlfunktion | 0 | - |
| 0x200208 | DME, interner Fehler, Überwachung Drehzahlbegrenzung: Fehlfunktion | 0 | - |
| 0x200308 | DME, interner Fehler, Überwachung Fahrpedalmodul: Fehlfunktion | 0 | - |
| 0x200404 | DME, interner Fehler, Überwachung Leerlaufregelung: Anforderung I-Anteil unplausibel | 0 | - |
| 0x200408 | DME, interner Fehler, Überwachung Leerlaufregelung: Anforderung PD-Anteil unplausibel | 0 | - |
| 0x200500 | DME, interner Fehler, Überwachung externe Momentenanforderung: Sendesignale unplausibel | 0 | - |
| 0x200501 | DME, interner Fehler, Überwachung externe Momentenanforderung: Anforderung MSR unplausibel | 0 | - |
| 0x200502 | DME, interner Fehler, Überwachung externe Momentenanforderung: Anforderung ICM unplausibel | 0 | - |
| 0x200504 | DME, interner Fehler, Überwachung externe Momentenanforderung: Sendesignale unplausibel | 0 | - |
| 0x200508 | DME, interner Fehler, Überwachung externe Momentenanforderung: Anforderung EGS unplausibel | 0 | - |
| 0x200601 | DME, interner Fehler, Überwachung Sollmoment: maximales Kupplungsmoment unplausibel | 0 | - |
| 0x200602 | DME, interner Fehler, Überwachung Sollmoment: minimales Kupplungsmoment unplausibel | 0 | - |
| 0x200604 | DME, interner Fehler, Überwachung Sollmoment: Verlustmoment unplausibel | 0 | - |
| 0x200708 | DME, interner Fehler, Überwachung Istmoment: Signal unplausibel | 0 | - |
| 0x200808 | DME, interner Fehler, Überwachung Hardware: Fehlfunktion | 0 | - |
| 0x200908 | DME, interner Fehler, Überwachung Kraftstoffmasse: Luftmasse zu Kraftstoffmasse unplausibel | 0 | - |
| 0x200A08 | DME, interner Fehler, Überwachung Luftpfad: Drosselklappenwinkel unplausibel | 0 | - |
| 0x200C01 | DME, interner Fehler: ROM-Fehler | 0 | - |
| 0x200C02 | DME, interner Fehler: RAM-Fehler | 0 | - |
| 0x200C04 | DME, interner Fehler: Prozessor-Fehler | 0 | - |
| 0x200C08 | DME, interner Fehler: Hauptprozessor-Fehler | 0 | - |
| 0x200D01 | DME, interner Fehler, Überwachung Sendesignale: Radmomente unplausibel | 0 | - |
| 0x200D02 | DME, interner Fehler, Überwachung Sendesignale: Fahrerwunsch unplausibel | 0 | - |
| 0x200D04 | DME, interner Fehler, Überwachung Sendesignale: Fahrpedalwert unplausibel | 0 | - |
| 0x200D08 | DME, interner Fehler, Überwachung Sendesignale: CAN-Fehler | 0 | - |
| 0x20A001 | Kühlmittelpumpe für Ladeluftkühler, Drehzahlabweichung: außerhalb der Toleranz | 0 | - |
| 0x20A101 | Kühlmittelpumpe für Ladeluftkühler, Abschaltung: interne Temperatur zu hoch | 0 | - |
| 0x20A102 | Kühlmittelpumpe für Ladeluftkühler, Abschaltung: Überspannung | 0 | - |
| 0x20A104 | Kühlmittelpumpe für Ladeluftkühler, Abschaltung: Überstrom | 0 | - |
| 0x20A201 | Kühlmittelpumpe für Ladeluftkühler, leistungsreduzierter Betrieb: Trockenlauf | 0 | - |
| 0x20A202 | Kühlmittelpumpe für Ladeluftkühler, leistungsreduzierter Betrieb: Unterspannung | 0 | - |
| 0x20A204 | Kühlmittelpumpe für Ladeluftkühler, leistungsreduzierter Betrieb: Temperaturgrenze 1 überschritten | 0 | - |
| 0x20A208 | Kühlmittelpumpe für Ladeluftkühler, leistungsreduzierter Betrieb: Temperaturgrenze 2 überschritten | 0 | - |
| 0x20A408 | Kühlmittelpumpe für Ladeluftkühler, Plausibilität Kommunikation: keine Spannung am Notlauf-Eingang der Pumpe | 0 | - |
| 0x20A501 | Turbolader-Kühlmittelpumpe, Ansteuerung: Kurzschluss nach Plus | 0 | - |
| 0x20A502 | Turbolader-Kühlmittelpumpe, Ansteuerung: Kurzschluss nach Masse | 0 | - |
| 0x20A504 | Turbolader-Kühlmittelpumpe, Ansteuerung: Leitungsunterbrechung | 0 | - |
| 0x20A608 | Turbolader-Kühlmittelpumpe, Ansteuerung: Pumpe blockiert | 0 | - |
| 0x20E102 | Kurbelgehäuseentlüftung, Entlüftungsschlauch: nicht angeschlossen/defekt | 0 | - |
| 0x20E202 | Kurbelgehäuseentlüftung 2, Entlüftungsschlauch: nicht angeschlossen/defekt | 0 | - |
| 0x210201 | Generator, elektrisch: Fehlfunktion | 0 | - |
| 0x210301 | Generator, Plausibilität, elektrisch: berechnet | 0 | - |
| 0x210401 | Generator, Temperatur: Übertemperatur | 1 | - |
| 0x210501 | Generator, Plausibilität, Temperatur: Übertemperatur berechnet | 1 | - |
| 0x210601 | Generator, mechanisch: Fehlfunktion | 0 | - |
| 0x210701 | Generator, Regler: Typ falsch | 0 | - |
| 0x210801 | Generator: Typ falsch | 0 | - |
| 0x210901 | Generator, Kommunikation: keine Kommunikation | 0 | - |
| 0x213301 | Powermanagement, Überspannung: Überspannung erkannt | 1 | - |
| 0x213401 | Powermanagement, Unterspannung: Unterspannung erkannt | 1 | - |
| 0x213501 | Powermanagement, Batterieüberwachung: Tiefentladung | 1 | - |
| 0x213601 | Powermanagement, Ruhestromüberwachung: Ruhestromverletzung | 0 | - |
| 0x213701 | Powermanagement: Batterieloser Betrieb | 0 | - |
| 0x213801 | Batterie, Transport: Batterie auf Transport geschädigt | 0 | - |
| 0x213901 | Verbraucherreduzierung: aktiv | 1 | - |
| 0x213A01 | Batterie, Transport, Überwachung: Batterie auf Transport entladen | 0 | - |
| 0x213B01 | Powermanagement, Batteriezustandserkennung: Batteriedefekt | 0 | - |
| 0x213C01 | Powermanagement, Batteriezustandserkennung: Tiefentladung | 0 | - |
| 0x213E01 | Bordnetzspannung: Arbeitsbereich, Spannung zu hoch | 0 | - |
| 0x213F01 | Bordnetzspannung: Arbeitsbereich, Spannung zu niedrig | 0 | - |
| 0x215401 | Intelligenter Batteriesensor, Plausibilität: Spannung unplausibel | 0 | - |
| 0x215501 | Intelligenter Batteriesensor, Plausibilität: Strom unplausibel | 0 | - |
| 0x215601 | Intelligenter Batteriesensor, Plausibilität: Temperatur unplausibel | 0 | - |
| 0x215701 | Intelligenter Batteriesensor: Eigendiagnose, Systemfehler | 0 | - |
| 0x215801 | Intelligenter Batteriesensor: Wake-up-Leitung, elektrisch, Kurzschluss nach Plus oder Masse | 0 | - |
| 0x215901 | Intelligenter Batteriesensor: Kompabilität, Version nicht plausibel | 0 | - |
| 0x215A01 | Intelligenter Batteriesensor: Wake-up-Leitung, elektrisch, Leitungsunterbrechung | 0 | - |
| 0x215B01 | LIN, Kommunikation (Intelligenter Batteriesensor): Zusatzstatus Framefehler | 0 | - |
| 0x230004 | Kommunikation Einschlafkoordinator: Zeitüberschreitung | 0 | - |
| 0x230008 | Kommunikation Einschlafkoordinator: Nachricht unplausibel | 0 | - |
| 0x230102 | Botschaft (Kopplung 1 Slave Antrieb): Aliveprüfung | 1 | - |
| 0x230104 | Botschaft (Kopplung 1 Slave Antrieb): fehlt | 1 | - |
| 0x230108 | Botschaft (Kopplung 1 Slave Antrieb): Prüfsumme falsch | 1 | - |
| 0x230202 | Botschaft (Kopplung 2 Slave Antrieb): Aliveprüfung | 1 | - |
| 0x230204 | Botschaft (Kopplung 2 Slave Antrieb): fehlt | 1 | - |
| 0x230208 | Botschaft (Kopplung 2 Slave Antrieb): Prüfsumme falsch | 1 | - |
| 0x230302 | Botschaft (Kopplung 3 Slave Antrieb): Aliveprüfung | 1 | - |
| 0x230304 | Botschaft (Kopplung 3 Slave Antrieb): fehlt | 1 | - |
| 0x230308 | Botschaft (Kopplung 3 Slave Antrieb): Prüfsumme falsch | 1 | - |
| 0x230402 | Botschaft (Kopplung 4 Slave Antrieb): Aliveprüfung | 1 | - |
| 0x230404 | Botschaft (Kopplung 4 Slave Antrieb): fehlt | 1 | - |
| 0x230408 | Botschaft (Kopplung 4 Slave Antrieb): Prüfsumme falsch | 1 | - |
| 0x231101 | Fehlerspeichereintrag: nur zum Test | 0 | - |
| 0x231201 | Fehlerspeichereintrag: nur zum Test | 0 | - |
| 0x231301 | Netzwerkfehler: nur zum Test | 0 | - |
| 0x231401 | Netzwerkfehler: nur zum Test | 0 | - |
| 0x231501 | Fehlerspeichereintrag: Sendepuffer voll | 0 | - |
| 0x231502 | Fehlerspeichereintrag: Senden fehlgeschlagen | 0 | - |
| 0x231701 | CAN-Kommunikation bei Unterspannung: Kommunikationsfehler zur EGS | 1 | - |
| 0x231801 | CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an FA-CAN | 1 | - |
| 0x231802 | CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an A-CAN | 1 | - |
| 0x231804 | CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an FA-CAN und A-CAN | 1 | - |
| 0x231901 | CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an FA-CAN | 1 | - |
| 0x231902 | CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an A-CAN | 1 | - |
| 0x231904 | CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an FA-CAN und A-CAN | 1 | - |
| 0x231F04 | A- / FA-CAN, Botschaften (Getriebe): fehlen | 0 | - |
| 0x232004 | A- / FA-CAN, Botschaften (Getriebe): fehlen | 0 | - |
| 0x233004 | FA-CAN, Botschaft (OBD Sensor Diagnosestatus, 0x5E0): fehlt, Sender Kombi | 1 | - |
| 0x233804 | FA-CAN, Botschaft (OBD Sensor Diagnosestatus, 0x5E0): fehlt | 1 | - |
| 0x238102 | Botschaft (Kopplung 1 Master Antrieb): Aliveprüfung | 1 | - |
| 0x238104 | Botschaft (Kopplung 1 Master Antrieb): fehlt | 1 | - |
| 0x238108 | Botschaft (Kopplung 1 Master Antrieb): Prüfsumme falsch | 1 | - |
| 0x238202 | Botschaft (Kopplung 2 Master Antrieb): Aliveprüfung | 1 | - |
| 0x238204 | Botschaft (Kopplung 2 Master Antrieb): fehlt | 1 | - |
| 0x238208 | Botschaft (Kopplung 2 Master Antrieb): Prüfsumme falsch | 1 | - |
| 0x238302 | Botschaft (Kopplung 3 Master Antrieb): Aliveprüfung | 1 | - |
| 0x238304 | Botschaft (Kopplung 3 Master Antrieb): fehlt | 1 | - |
| 0x238308 | Botschaft (Kopplung 3 Master Antrieb): Prüfsumme falsch | 1 | - |
| 0x238402 | Botschaft (Kopplung 4 Master Antrieb): Aliveprüfung | 1 | - |
| 0x238404 | Botschaft (Kopplung 4 Master Antrieb): fehlt | 1 | - |
| 0x238408 | Botschaft (Kopplung 4 Master Antrieb): Prüfsumme falsch | 1 | - |
| 0xCD8408 | FlexRay Bus: Controller-Reset durchgeführt | 0 | - |
| 0xCD840A | FA-CAN Bus: Kommunikationsfehler | 0 | - |
| 0xCD8420 | FlexRay Bus: Kommunikationsfehler | 0 | - |
| 0xCD8486 | A-CAN Bus: Kommunikationsfehler | 1 | - |
| 0xCD8487 | FlexRay Controller, Startup: Fehlfunktion | 1 | - |
| 0xCD8508 | FlexRay Bus: Hardware defekt | 1 | - |
| 0xCD8601 | FlexRay Controller, Startup: Synchronisationsfehler | 1 | - |
| 0xCD8801 | FlexRay Controller, Startup: maximale Startupzeit überschritten | 1 | - |
| 0xCD8B02 | FlexRay, Botschaft (Diagnose OBD 1, 263.3.4): Aliveprüfung | 0 | - |
| 0xCD8B04 | FlexRay, Botschaft (Diagnose OBD 1, 263.3.4): fehlt | 0 | - |
| 0xCD8E01 | LIN  Bus, Kommunikationsfehler: Kurzschluss | 0 | - |
| 0xCD8E02 | LIN  Bus, Kommunikationsfehler: Leitungsunterbrechung | 0 | - |
| 0xCD8F01 | LIN, Kommunikation (intelligenter Batteriesensor): fehlt | 0 | - |
| 0xCD9001 | LIN, Kommunikation (Ladeluft-Kühlmittelpumpe): fehlt | 0 | - |
| 0xCD9002 | LIN, Kommunikation (Ladeluft-Kühlmittelpumpe): fehlerhaft | 0 | - |
| 0xCD9101 | Batterieladeeinheit, LIN Kommunikation: Zeitüberschreitung | 0 | - |
| 0xCD9102 | Batterieladeeinheit, LIN Kommunikation: ungültige Botschaft | 0 | - |
| 0xCD9201 | LIN, Kommunikation (Kühlerjalousie): fehlt | 0 | - |
| 0xCD9202 | LIN, Kommunikation (Kühlerjalousie): ungültiger Botschaftsinhalt | 0 | - |
| 0xCD9304 | Bitserielle Datenschnittstelle, Signal: Kommunikationsfehler | 0 | - |
| 0xCD9402 | FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): Aliveprüfung | 1 | - |
| 0xCD9404 | FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): fehlt | 1 | - |
| 0xCD9408 | FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): Prüfsumme falsch | 1 | - |
| 0xCD9430 | CAN-Kommunikation bei Unterspannung: Kommunikationsfehler zur EGS | 1 | - |
| 0xCD9431 | CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an FA-CAN | 1 | - |
| 0xCD9432 | CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an A-CAN | 1 | - |
| 0xCD9433 | CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an FA-CAN und A-CAN | 1 | - |
| 0xCD9434 | CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an FA-CAN | 1 | - |
| 0xCD9435 | CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an A-CAN | 1 | - |
| 0xCD9436 | CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an FA-CAN und A-CAN | 1 | - |
| 0xCD9502 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung / Soll Verteilung Längsmoment Vorderachse Hinterachse, 43.1.4): Aliveprüfung | 1 | - |
| 0xCD9504 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung / Soll Verteilung Längsmoment Vorderachse Hinterachse, 43.1.4): fehlt | 1 | - |
| 0xCD9508 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung / Soll Verteilung Längsmoment Vorderachse Hinterachse, 43.1.4): Prüfsumme falsch | 1 | - |
| 0xCD9602 | FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): Aliveprüfung | 1 | - |
| 0xCD9604 | FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): fehlt | 1 | - |
| 0xCD9608 | FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): Prüfsumme falsch | 1 | - |
| 0xCD9702 | FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): Aliveprüfung | 1 | - |
| 0xCD9704 | FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): fehlt | 1 | - |
| 0xCD9708 | FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): Prüfsumme falsch | 1 | - |
| 0xCD9804 | FlexRay, Botschaft (Einheiten BN2020, 252.0.4 ): fehlt | 1 | - |
| 0xCD9902 | FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): Aliveprüfung | 1 | - |
| 0xCD9904 | FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): fehlt | 1 | - |
| 0xCD9908 | FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): Prüfsumme falsch | 1 | - |
| 0xCD9A02 | FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): Aliveprüfung | 1 | - |
| 0xCD9A04 | FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): fehlt | 1 | - |
| 0xCD9A08 | FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): Prüfsumme falsch | 1 | - |
| 0xCD9B02 | FlexRay, Botschaft (Ist Drehzahl Rad, 46.1.2): Aliveprüfung | 1 | - |
| 0xCD9B04 | FlexRay, Botschaft (Ist Drehzahl Rad, 46.1.2): fehlt | 1 | - |
| 0xCD9B08 | FlexRay, Botschaft (Ist Drehzahl Rad, 46.1.2): Prüfsumme falsch | 1 | - |
| 0xCD9C02 | FlexRay, Botschaft (Ist Lenkwinkel Fahrer, 59.0.2): Aliveprüfung | 1 | - |
| 0xCD9C04 | FlexRay, Botschaft (Ist Lenkwinkel Fahrer, 59.0.2): fehlt | 1 | - |
| 0xCD9C08 | FlexRay, Botschaft (Ist Lenkwinkel Fahrer, 59.0.2): Prüfsumme falsch | 1 | - |
| 0xCD9D02 | FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): Aliveprüfung | 1 | - |
| 0xCD9D04 | FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): fehlt | 1 | - |
| 0xCD9D08 | FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): Prüfsumme falsch | 1 | - |
| 0xCD9E02 | FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): Aliveprüfung | 1 | - |
| 0xCD9E04 | FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): fehlt | 1 | - |
| 0xCD9E08 | FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): Prüfsumme falsch | 1 | - |
| 0xCD9F02 | FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): Aliveprüfung | 1 | - |
| 0xCD9F04 | FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): fehlt | 1 | - |
| 0xCD9F08 | FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): Prüfsumme falsch | 1 | - |
| 0xCDA002 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): Aliveprüfung | 1 | - |
| 0xCDA004 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): fehlt | 1 | - |
| 0xCDA008 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): Prüfsumme falsch | 1 | - |
| 0xCDA104 | FlexRay, Botschaft (Neigung Fahrbahn, 56.1.2): fehlt | 1 | - |
| 0xCDA204 | FlexRay, Botschaft (Anforderung Leistung Elektrisch EPS, 234.0.2): fehlt | 1 | - |
| 0xCDA302 | FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): Aliveprüfung | 1 | - |
| 0xCDA304 | FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): fehlt | 1 | - |
| 0xCDA308 | FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): Prüfsumme falsch | 1 | - |
| 0xCDA524 | FA-CAN, Botschaft (Status Elektrische Kraftstoffpumpe, 0x335): fehlt | 1 | - |
| 0xCDA602 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Aliveprüfung | 1 | - |
| 0xCDA604 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): fehlt | 1 | - |
| 0xCDA608 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Prüfsumme falsch | 1 | - |
| 0xCDA702 | FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): Aliveprüfung | 1 | - |
| 0xCDA704 | FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): fehlt | 1 | - |
| 0xCDA708 | FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): Prüfsumme falsch | 1 | - |
| 0xCDA804 | FA-CAN, Botschaft (Relativzeit, 0x328): fehlt | 1 | - |
| 0xCDA904 | FA-CAN, Botschaft (Status Anhänger, 0x2E4): fehlt | 1 | - |
| 0xCDAC04 | FA-CAN, Botschaft (Status Getriebesteuergerät, 0x39A): fehlt | 1 | - |
| 0xCDAD04 | FA-CAN, Botschaft (Steuerung Crashabschaltung elektrische Kraftstoffpumpe, 0x135): fehlt | 1 | - |
| 0xCDAE04 | FA-CAN, Botschaft (Uhrzeit/Datum, 0x2F8): fehlt | 1 | - |
| 0xCDAF04 | FA-CAN, Botschaft (ZV und Klappenzustand, 0x2FC): fehlt | 1 | - |
| 0xCDB002 | FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Aliveprüfung | 1 | - |
| 0xCDB004 | FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): fehlt | 1 | - |
| 0xCDB008 | FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Prüfsumme falsch | 1 | - |
| 0xCDB102 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): Aliveprüfung | 1 | - |
| 0xCDB104 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): fehlt | 1 | - |
| 0xCDB108 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): Prüfsumme falsch | 1 | - |
| 0xCDB204 | FA-CAN, Botschaft (Außentemperatur, 0x2CA): fehlt | 1 | - |
| 0xCDB404 | FA-CAN, Botschaft (Fahrzeugzustand, 0x3A0): fehlt | 1 | - |
| 0xCDB504 | FA-CAN, Botschaft (Kilometerstand/Reichweite, 0x330): fehlt | 1 | - |
| 0xCDB602 | FA-CAN, Botschaft (Klemmen, 0x12F): Aliveprüfung | 1 | - |
| 0xCDB604 | FA-CAN, Botschaft (Klemmen, 0x12F): fehlt | 1 | - |
| 0xCDB608 | FA-CAN, Botschaft (Klemmen, 0x12F): Prüfsumme falsch | 1 | - |
| 0xCDB704 | FA-CAN, Botschaft (Nachlaufzeit Stromversorgung, 0x3BE): fehlt | 1 | - |
| 0xCDB804 | FA-CAN, Botschaft (Anforderung Klimaanlage, 0x2F9): fehlt | 1 | - |
| 0xCDB904 | FA-CAN, Botschaft (Diagnose OBD Getriebe, 0x396): fehlt | 1 | - |
| 0xCDBB02 | A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Aliveprüfung | 1 | - |
| 0xCDBB04 | A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): fehlt | 1 | - |
| 0xCDBB08 | A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Prüfsumme falsch | 1 | - |
| 0xCDBC04 | A-CAN, Botschaft (Anforderung Leistung Elektrisch PCU, 0x33F): fehlt | 1 | - |
| 0xCDBD04 | A-CAN, Botschaft (Status Energieerzeugung BN2, 0x2AF): fehlt | 1 | - |
| 0xCDBE02 | A-CAN, Botschaft (Anzeige Drehzahl Motor Dynamisierung, 0xF8): Aliveprüfung | 1 | - |
| 0xCDBE04 | A-CAN, Botschaft (Anzeige Drehzahl Motor Dynamisierung, 0xF8): fehlt | 1 | - |
| 0xCDBF04 | A-CAN, Botschaft (Status Getriebesteuergerät, 0x39A): fehlt | 1 | - |
| 0xCDC004 | A-CAN, Botschaft (Diagnose OBD Getriebe, 0x396): fehlt | 1 | - |
| 0xCDC102 | A-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Aliveprüfung | 1 | - |
| 0xCDC104 | A-CAN, Botschaft (Daten Getriebestrang, 0x1AF): fehlt | 1 | - |
| 0xCDC108 | A-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Prüfsumme falsch | 1 | - |
| 0xCDC202 | A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): Aliveprüfung | 1 | - |
| 0xCDC204 | A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): fehlt | 1 | - |
| 0xCDC208 | A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): Prüfsumme falsch | 1 | - |
| 0xCDC304 | A-CAN, Botschaft (Status Elektrische Kraftstoffpumpe, 0x335): fehlt | 1 | - |
| 0xCDC408 | FlexRay Bus: Controller-Reset durchgeführt | 0 | - |
| 0xCDC40A | FA-CAN Bus: Kommunikationsfehler | 0 | - |
| 0xCDC420 | FlexRay Bus: Kommunikationsfehler | 0 | - |
| 0xCDC487 | FlexRay Controller, Startup: Fehlfunktion | 0 | - |
| 0xCDC508 | FlexRay Bus: Hardware defekt | 1 | - |
| 0xCDC601 | FlexRay Controller, Startup: Synchronisationsfehler | 0 | - |
| 0xCDC801 | FlexRay Controller, Startup: maximale Startupzeit überschritten | 0 | - |
| 0xCDD402 | FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): Aliveprüfung | 1 | - |
| 0xCDD404 | FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): fehlt | 1 | - |
| 0xCDD408 | FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): Prüfsumme falsch | 1 | - |
| 0xCDD502 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung / Soll Verteilung Längsmoment Vorderachse Hinterachse, 43.1.4): Aliveprüfung | 1 | - |
| 0xCDD504 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung / Soll Verteilung Längsmoment Vorderachse Hinterachse, 43.1.4): fehlt | 1 | - |
| 0xCDD508 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung / Soll Verteilung Längsmoment Vorderachse Hinterachse, 43.1.4): Prüfsumme falsch | 1 | - |
| 0xCDD512 | FlexRay, Botschaft (Daten Antriebsstrang 2, 230.0.2): Aliveprüfung | 1 | - |
| 0xCDD513 | FlexRay, Botschaft (Daten Antriebsstrang 2, 230.0.2): fehlt | 1 | - |
| 0xCDD514 | FlexRay, Botschaft (Daten Antriebsstrang 2, 230.0.2): Prüfsumme falsch | 1 | - |
| 0xCDD602 | FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): Aliveprüfung | 1 | - |
| 0xCDD604 | FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): fehlt | 1 | - |
| 0xCDD608 | FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): Prüfsumme falsch | 1 | - |
| 0xCDD612 | FlexRay, Botschaft (Radmoment Antrieb 1, 41.3.4): Aliveprüfung | 1 | - |
| 0xCDD613 | FlexRay, Botschaft (Radmoment Antrieb 1, 41.3.4): fehlt | 1 | - |
| 0xCDD614 | FlexRay, Botschaft (Radmoment Antrieb 1, 41.3.4): Prüfsumme falsch | 1 | - |
| 0xCDD702 | FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): Aliveprüfung | 1 | - |
| 0xCDD704 | FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): fehlt | 1 | - |
| 0xCDD708 | FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): Prüfsumme falsch | 1 | - |
| 0xCDD712 | FlexRay, Botschaft (Radmoment Antrieb 4, 40.3.4): Aliveprüfung | 1 | - |
| 0xCDD713 | FlexRay, Botschaft (Radmoment Antrieb 4, 40.3.4): fehlt | 1 | - |
| 0xCDD714 | FlexRay, Botschaft (Radmoment Antrieb 4, 40.3.4): Prüfsumme falsch | 1 | - |
| 0xCDD902 | FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): Aliveprüfung | 1 | - |
| 0xCDD904 | FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): fehlt | 1 | - |
| 0xCDD908 | FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): Prüfsumme falsch | 1 | - |
| 0xCDDA02 | FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): Aliveprüfung | 1 | - |
| 0xCDDA04 | FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): fehlt | 1 | - |
| 0xCDDA08 | FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): Prüfsumme falsch | 1 | - |
| 0xCDDB02 | FlexRay, Botschaft (Ist Drehzahl Rad, 46.1.2): Aliveprüfung | 1 | - |
| 0xCDDB04 | FlexRay, Botschaft (Ist Drehzahl Rad, 46.1.2): fehlt | 1 | - |
| 0xCDDB08 | FlexRay, Botschaft (Ist Drehzahl Rad, 46.1.2): Prüfsumme falsch | 1 | - |
| 0xCDDC02 | FlexRay, Botschaft (Ist Lenkwinkel Fahrer, 59.0.2): Aliveprüfung | 1 | - |
| 0xCDDC04 | FlexRay, Botschaft (Ist Lenkwinkel Fahrer, 59.0.2): fehlt | 1 | - |
| 0xCDDC08 | FlexRay, Botschaft (Ist Lenkwinkel Fahrer, 59.0.2): Prüfsumme falsch | 1 | - |
| 0xCDDD02 | FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): Aliveprüfung | 1 | - |
| 0xCDDD04 | FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): fehlt | 1 | - |
| 0xCDDD08 | FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): Prüfsumme falsch | 1 | - |
| 0xCDDE02 | FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): Aliveprüfung | 1 | - |
| 0xCDDE04 | FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): fehlt | 1 | - |
| 0xCDDE08 | FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): Prüfsumme falsch | 1 | - |
| 0xCDDF02 | FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): Aliveprüfung | 1 | - |
| 0xCDDF04 | FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): fehlt | 1 | - |
| 0xCDDF08 | FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): Prüfsumme falsch | 1 | - |
| 0xCDE002 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): Aliveprüfung | 1 | - |
| 0xCDE004 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): fehlt | 1 | - |
| 0xCDE008 | FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): Prüfsumme falsch | 1 | - |
| 0xCDE104 | FlexRay, Botschaft (Neigung Fahrbahn, 56.1.2): fehlt | 1 | - |
| 0xCDE204 | FlexRay, Botschaft (Anforderung Leistung Elektrisch EPS, 234.0.2): fehlt | 1 | - |
| 0xCDE302 | FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): Aliveprüfung | 1 | - |
| 0xCDE304 | FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): fehlt | 1 | - |
| 0xCDE308 | FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): Prüfsumme falsch | 1 | - |
| 0xCDE602 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Aliveprüfung | 1 | - |
| 0xCDE604 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): fehlt | 1 | - |
| 0xCDE608 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Prüfsumme falsch | 1 | - |
| 0xCDE702 | FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): Aliveprüfung | 1 | - |
| 0xCDE704 | FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): fehlt | 1 | - |
| 0xCDE708 | FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): Prüfsumme falsch | 1 | - |
| 0xCDE804 | FA-CAN, Botschaft (Relativzeit, 0x328): fehlt | 1 | - |
| 0xCDE904 | FA-CAN, Botschaft (Status Anhänger, 0x2E4): fehlt | 1 | - |
| 0xCDEC04 | FA-CAN, Botschaft (Status Getriebesteuergerät, 0x39A): fehlt | 1 | - |
| 0xCDED04 | FA-CAN, Botschaft (Steuerung Crashabschaltung elektrische Kraftstoffpumpe, 0x135): fehlt | 1 | - |
| 0xCDEE04 | FA-CAN, Botschaft (Uhrzeit/Datum, 0x2F8): fehlt | 1 | - |
| 0xCDEF04 | FA-CAN, Botschaft (ZV und Klappenzustand, 0x2FC): fehlt | 1 | - |
| 0xCDF002 | FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Aliveprüfung | 1 | - |
| 0xCDF004 | FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): fehlt | 1 | - |
| 0xCDF008 | FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Prüfsumme falsch | 1 | - |
| 0xCDF102 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): Aliveprüfung | 1 | - |
| 0xCDF104 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): fehlt | 1 | - |
| 0xCDF108 | FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe, 0xB0): Prüfsumme falsch | 1 | - |
| 0xCDF204 | FA-CAN, Botschaft (Außentemperatur, 0x2CA): fehlt | 1 | - |
| 0xCDF302 | FA-CAN, Botschaft (Daten Anzeige Getriebestrang, 0x3FD): Aliveprüfung | 1 | - |
| 0xCDF304 | FA-CAN, Botschaft (Daten Anzeige Getriebestrang, 0x3FD): fehlt | 1 | - |
| 0xCDF308 | FA-CAN, Botschaft (Daten Anzeige Getriebestrang, 0x3FD): Prüfsumme falsch | 1 | - |
| 0xCDF404 | FA-CAN, Botschaft (Fahrzeugzustand, 0x3A0): fehlt | 1 | - |
| 0xCDF504 | FA-CAN, Botschaft (Kilometerstand/Reichweite, 0x330): fehlt | 1 | - |
| 0xCDF602 | FA-CAN, Botschaft (Klemmen, 0x12F): Aliveprüfung | 1 | - |
| 0xCDF604 | FA-CAN, Botschaft (Klemmen, 0x12F): fehlt | 1 | - |
| 0xCDF608 | FA-CAN, Botschaft (Klemmen, 0x12F): Prüfsumme falsch | 1 | - |
| 0xCDF704 | FA-CAN, Botschaft (Nachlaufzeit Stromversorgung, 0x3BE): fehlt | 1 | - |
| 0xCDF804 | FA-CAN, Botschaft (Anforderung Klimaanlage, 0x2F9): fehlt | 1 | - |
| 0xCDF904 | FA-CAN, Botschaft (Diagnose OBD Getriebe, 0x396): fehlt | 1 | - |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 241 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x5800 | Zeit nach Start | s | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5801 | Umgebungsdruck | kPa | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5802 | Zustand Lambdaregelung Bank 1 | 0-n | - | 0xFF | _CNV_S_5_LACO_RANGE_300 | - | - | - |
| 0x5803 | Zustand Lambdaregelung Bank 2 | 0-n | - | 0xFF | _CNV_S_5_LACO_RANGE_300 | - | - | - |
| 0x5804 | Berechneter Lastwert | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5805 | Kühlmitteltemperatur OBD | °C | - | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0x5806 | Lambda Integrator Gruppe 1 | % | - | unsigned char | - | 0.78125 | 1.0 | -100.00000224 |
| 0x5807 | Lambda Adaption Summe mul. und add. Gruppe 1 | % | - | unsigned char | - | 0.78125 | 1.0 | -100.00000224 |
| 0x5808 | Lambda Integrator Gruppe 2 | % | - | unsigned char | - | 0.78125 | 1.0 | -100.00000224 |
| 0x5809 | Lambda Adaption Summe mul. und add. Gruppe 2 | % | - | unsigned char | - | 0.78125 | 1.0 | -100.00000224 |
| 0x580B | Saugrohrdruck | kPa | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x580C | Drehzahl | 1/min | - | unsigned char | - | 64.0 | 1.0 | 0.0 |
| 0x580D | Geschwindigkeit | km/h | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x580E | Zündzeitpunkt Zylinder 1 | ° KW | - | unsigned char | - | 0.5 | 1.0 | -64.0 |
| 0x580F | Ansauglufttemperatur | °C | - | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0x5810 | Luftdurchsatz OBD | g/s | - | unsigned char | - | 2.55999994 | 1.0 | 0.0 |
| 0x5811 | Motordrehzahl | 1/min | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x5812 | Luftmasse gemessen | kg/h | - | unsigned char | - | 8.0 | 1.0 | 0.0 |
| 0x5813 | Relative Last | % | - | signed char | - | 2.55999994 | 1.0 | 0.0 |
| 0x5814 | Fahrpedalwert | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5815 | Batteriespannung | V | - | unsigned char | - | 0.25600001 | 1.0 | 0.0 |
| 0x5816 | Lambda Setpoint | - | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 |
| 0x5817 | Umgebungstemperatur | °C | - | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0x5818 | Luftmasse gerechnet | mg/stroke | - | unsigned char | - | 5.44705868 | 1.0 | 0.0 |
| 0x5819 | Drehzahl OBD Byte | 1/min | - | unsigned char | - | 64.0 | 1.0 | 0.0 |
| 0x581A | Periodendauer Sensor Ansauglufttemperatur | µs | - | unsigned char | - | 256.0 | 1.0 | 0.0 |
| 0x581B | Spannung Drucksensor | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x581C | Rohwert Lufttemperatur | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x581D | Spannung Lufttemperatur | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x581E | Lufttemperatur Drosselklappe | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x581F | Motortemperatur | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x5820 | Kühlmitteltemperatur Kühlerausgang | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x5821 | Steuergeräte-Innentemperatur | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x5822 | (Motor)-Öltemperatur | °C | - | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0x5823 | Zeit Motor steht | min | - | unsigned char | - | 256.0 | 1.0 | 0.0 |
| 0x5824 | Umgebungstemperatur | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x5825 | Abstellzeit | min | - | unsigned char | - | 4.0 | 1.0 | 0.0 |
| 0x5826 | Drosselklappentemperatur | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x5827 | Lambdasondenheizung vor Katalysator Bank 1 | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5828 | Lambdasondenheizung vor Katalysator Bank 2 | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5829 | Lambdasondenheizung hinter Katalysator Bank 1 | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x582A | Lambdasondenheizung hinter Katalysator Bank 2 | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x582B | Drehmomenteingriff über CAN | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x582C | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 1 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x582D | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 2 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x582E | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 1 | - | - | unsigned char | - | 0.00390625 | 1.0 | 0.0 |
| 0x582F | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 2 | - | - | unsigned char | - | 0.00390625 | 1.0 | 0.0 |
| 0x5830 | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 1 | - | - | unsigned char | - | 0.004 | 1.0 | 0.0 |
| 0x5831 | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 2 | - | - | unsigned char | - | 0.004 | 1.0 | 0.0 |
| 0x5832 | Motor Status | 0-n | - | 0xFF | _CNV_S_6_RANGE_STAT_56 | - | - | - |
| 0x5833 | Umgebungstemperatur beim Start | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x5834 | Umgebungsdruck | hPa | - | unsigned char | - | 5.30664063 | 1.0 | 0.0 |
| 0x5835 | Herstellercode Generator 1 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5836 | Drehzahlgradient | 1/s | - | signed char | - | 32.0 | 1.0 | 0.0 |
| 0x5837 | Status OBD-I Fehler vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_11_EGCP_RANGE_249 | - | - | - |
| 0x5838 | Status OBD-I Fehler vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_11_EGCP_RANGE_249 | - | - | - |
| 0x5839 | Status Drosselklappe Notlauf | 0-n | - | 0xFF | _CNV_S_3_THRO_RANGE_891 | - | - | - |
| 0x583A | Ansauglufttemperatur beim Start | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x583B | Kraftstofftank Füllstand | l | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x583C | Spannung Kl. 87 | V | - | unsigned char | - | 0.10156249 | 1.0 | 0.0 |
| 0x583D | Resettyp | 0-n | - | 0xFF | _CNV_S_19_ECOP_RANGE_764 | - | - | - |
| 0x583E | Motordrehzahl bei Reset | 1/min | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x583F | Drosselklappe Sollwert | ° DK | - | unsigned char | - | 0.46682537 | 1.0 | 0.0 |
| 0x5840 | CPU Last bei Reset | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5841 | SG-Innentemperatur Rohwert | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5842 | Kennung Generatortyp Generator 1 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5843 | Versorgung FWG 1 | V | - | unsigned char | - | 0.0390625 | 1.0 | 0.0 |
| 0x5844 | Chiptemperatur Generator 1 | °C | - | unsigned char | - | 1.0 | 1.0 | -48.0 |
| 0x5845 | Spannung Lambdasonde vor Katalysator Bank 1 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5846 | Spannung Pedalwertgeber 1 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5847 | Spannung Pedalwertgeber 2 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5848 | Spannung Lambdasonde vor Katalysator Bank 2 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5849 | Spannung Lambdasonde hinter Katalysator Bank 1 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x584A | Spannung Kl. 15 Rohwert | V | - | unsigned char | - | 0.11294118 | 1.0 | 0.0 |
| 0x584B | Spannung Lambdasonde hinter Katalysator Bank 2 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x584D | korrigierter Sollwert Durchfluss Tankentlüftung | kg/h | - | unsigned char | - | 0.03125 | 1.0 | 0.0 |
| 0x584F | Höhe Gegendruck OPF  | hPa | - | unsigned char | - | 21.47483647 | 1.0 | 0.0 |
| 0x5850 | Spannung Motortemperatur | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5851 | Spannung Ansauglufttemperatur, Sensor | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5852 | Kühlmitteltemperatur Kühlerausgang Rohwert | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5853 | Spannung Kl.87 Rohwert | V | - | unsigned char | - | 0.11294118 | 1.0 | 0.0 |
| 0x5854 | Versorgung FWG 2 | V | - | unsigned char | - | 0.0390625 | 1.0 | 0.0 |
| 0x5855 | Mittelwert Bank 1 | % | - | signed char | - | 0.390625 | 1.0 | 0.0 |
| 0x5856 | Mittelwert Bank 2 | % | - | signed char | - | 0.390625 | 1.0 | 0.0 |
| 0x5857 | Erregerstrom Generator 1 | A | - | unsigned char | - | 0.125 | 1.0 | 0.0 |
| 0x5858 | Drosselklappe aktueller Wert | ° DK | - | unsigned char | - | 0.46682537 | 1.0 | 0.0 |
| 0x5859 | DMTL Strom Referenzleck | mA | - | unsigned char | - | 0.19531247 | 1.0 | 0.0 |
| 0x585A | DMTL Strom Grobleck | mA | - | unsigned char | - | 0.19531247 | 1.0 | 0.0 |
| 0x585B | DMTL Strom Diagnoseende | mA | - | unsigned char | - | 0.19531247 | 1.0 | 0.0 |
| 0x585C | Widerstand Lambdasonde hinter Katalysator Bank 1 | Ohm | - | unsigned char | - | 256.0 | 1.0 | 0.0 |
| 0x585D | Widerstand Lambdasonde hinter Katalysator Bank 2 | Ohm | - | unsigned char | - | 256.0 | 1.0 | 0.0 |
| 0x585E | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 1 | Ohm | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x585F | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 2 | Ohm | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5860 | Widerstand Lambdasonde vor Katalysator Bank 1 | Ohm | - | unsigned char | - | 64.0 | 1.0 | 0.0 |
| 0x5861 | Widerstand Lambdasonde vor Katalysator Bank 2 | Ohm | - | unsigned char | - | 64.0 | 1.0 | 0.0 |
| 0x5862 | Rußbeladung bei Leistungsbegrenzung OPF  | g | - | unsigned char | - | 1.0 | 64.00008031 | 0.0 |
| 0x5863 | untere Byte Widerstand Lambdasonde vor Katalysator Bank 1 | Ohm | - | unsigned char | - | 0.25 | 1.0 | 0.0 |
| 0x5864 | untere Byte Widerstand Lambdasonde vor Katalysator Bank 2 | Ohm | - | unsigned char | - | 0.25 | 1.0 | 0.0 |
| 0x5865 | Ölstand Mittelwert Langzeit | mm | - | unsigned char | - | 0.29296875 | 1.0 | 0.0 |
| 0x5866 | Füllstand Motoröl | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5867 | Kilometerstand | km | - | unsigned char | - | 2560.0 | 1.0 | 0.0 |
| 0x5869 | Status Standverbraucher registriert Teil 2 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x586A | Batteriespannung von IBS gemessen | V | - | unsigned char | - | 0.064 | 1.0 | 6.016 |
| 0x586B | Zeit mit Ruhestrom 80 - 200 mA | min | - | unsigned char | - | 14.9333334 | 1.0 | 0.0 |
| 0x586C | Zeit mit Ruhestrom 200 - 1000 mA | min | - | unsigned char | - | 14.9333334 | 1.0 | 0.0 |
| 0x586D | Zähler Erkennung schlechte Strasse | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x586E | Zeit mit Ruhestrom größer 1000 mA | min | - | unsigned char | - | 14.9333334 | 1.0 | 0.0 |
| 0x5870 | Spannung DME Umgebungsdruck | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5871 | Lambda-Sollwert Gruppe 1 | - | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 |
| 0x5872 | Reglerversion Generator 1 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5873 | Lambda-Sollwert Gruppe 2 | - | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 |
| 0x5874 | Spannung Strommessung DMTL | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5875 | Sollwert Motormoment | Nm | - | unsigned char | - | 4.0 | 1.0 | 0.0 |
| 0x5876 | Raildruck OBD (High-Byte von FUP für OBD) | kPa | - | unsigned char | - | 2560.0 | 1.0 | 0.0 |
| 0x5877 | Raildruck OBD (Low-Byte von FUP für OBD) | kPa | - | unsigned char | - | 10.0 | 1.0 | 0.0 |
| 0x5878 | Lambdaverschiebung Rückführregler 1 | - | - | signed char | - | 0.00097656 | 1.0 | 0.0 |
| 0x5879 | Lambdaverschiebung Rückführregler 2 | - | - | signed char | - | 0.00097656 | 1.0 | 0.0 |
| 0x587A | Status FGR | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x587B | Gemessene Spannung vom DCDC Wandler gegen Masse | V | - | unsigned char | - | 0.25 | 1.0 | 0.0 |
| 0x587C | Status Motorsteuerung | 0-n | - | 0xFF | _CNV_S_7_RANGE_ECU__54 | - | - | - |
| 0x587D | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_261 | - | - | - |
| 0x587E | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_261 | - | - | - |
| 0x587F | Tastverhältnis E-Lüfter | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5880 | Ansteuerung untere Luftklappe | 0/1 | - | 0x01 | - | - | - | - |
| 0x5881 | berechneter Gang | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x5882 | Motortemperatur beim Start | °C | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 |
| 0x5883 | Spannung Klopfwerte Zylinder 1 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5884 | Rückgelesener Erregergrenzstrom Generator 1 | A | - | unsigned char | - | 0.125 | 1.0 | 0.0 |
| 0x5885 | Spannung Klopfwerte Zylinder 3 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5886 | Spannung Klopfwerte Zylinder 6 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5887 | Auslastungsgrad Generator 1 | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x5888 | Spannung Klopfwerte Zylinder 4 | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x5889 | Lambda-Istwert Gruppe 1 | - | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 |
| 0x588A | Lambda-Istwert Gruppe 2 | - | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 |
| 0x588B | Zeit seit Startende | s | - | unsigned char | - | 256.0 | 1.0 | 0.0 |
| 0x588C | Keramiktemperatur Lambdasonde vor Katalysator Bank 1 | °C | - | signed char | - | 16.0 | 1.0 | 0.0 |
| 0x588D | aktuelle Zeit DMTL Leckmessung | s | - | unsigned char | - | 25.60000038 | 1.0 | 0.0 |
| 0x588E | Pumpenstrom bei DMTL Pumpenprüfung | mA | - | unsigned char | - | 0.19531247 | 1.0 | 0.0 |
| 0x588F | Keramiktemperatur Lambdasonde vor Katalysator Bank 2 | °C | - | signed char | - | 16.0 | 1.0 | 0.0 |
| 0x5890 | OPF Drucksensor Druck Master /Slave  | hPa | - | unsigned char | - | 21.47483647 | 1.0 | 0.0 |
| 0x5891 | Momentanforderung an der Kupplung | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x5892 | OPF Temperatursensor Temperaturistwert 1Master / 2Slave | °C | - | unsigned char | - | 16.0 | 1.0 | -273.15 |
| 0x5893 | Drehmomentabfall schnell bei Gangwechsel | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x5894 | Symptom Lambdasondenheizung vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_253 | - | - | - |
| 0x5895 | Symptom Lambdasondenheizung vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_253 | - | - | - |
| 0x5896 | Abgastemperatur hinter Katalysator Bank 1 | °C | - | signed char | - | 16.0 | 1.0 | 0.0 |
| 0x5897 | Abgastemperatur hinter Katalysator Bank 2 | °C | - | signed char | - | 16.0 | 1.0 | 0.0 |
| 0x5898 | Generator Sollspannung | V | - | unsigned char | - | 0.1 | 1.0 | 0.0 |
| 0x589B | Spannungsoffset Signalpfad CJ120 1 | V | - | signed char | - | 0.00488278 | 1.0 | -0.00000361 |
| 0x589C | Spannungsoffset Signalpfad CJ120 2 | V | - | signed char | - | 0.00488278 | 1.0 | -0.00000361 |
| 0x589D | Abweichung Lambdasonde zu Lambdamodellwert Überwachung | mg/stroke | - | unsigned char | - | 2.71050191 | 1.0 | 0.0 |
| 0x589F | Motordrehzahl | 1/min | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x58A0 | Batterietemperatur | °C | - | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x58A1 | Entladung während Ruhestromverletzung | Ah | - | unsigned char | - | 0.49803922 | 1.0 | 0.0 |
| 0x58A2 | Wasserpumpe Stromaufnahme | A | - | unsigned char | - | 0.2 | 1.0 | 0.0 |
| 0x58A3 | relative Wasserpumpenspannung | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58A4 | Status Generator | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58A5 | Generatorauslastung | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58A6 | Generatorspannung | V | - | unsigned char | - | 0.1 | 1.0 | 0.0 |
| 0x58A7 | Abstellzeit in min | min | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58A8 | Motorabstellzeit | min | - | unsigned char | - | 4.0 | 1.0 | 0.0 |
| 0x58A9 | Resetzähler Rechnerüberwachung: alter Wert | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58AA | Fehlercode Rechnerüberwachung: alter Wert | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58AB | Abweichung DK-Potentiometer 1 und Modellwert | ° DK | - | unsigned char | - | 0.46682537 | 1.0 | 0.0 |
| 0x58AC | Abweichung DK-Potentiometer 2 und Modellwert | ° DK | - | unsigned char | - | 0.46682537 | 1.0 | 0.0 |
| 0x58AD | Pedalwertgeber 1 | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58AE | Periodendauer Luftmasse | µs | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x58AF | Kraftstoff Anforderung an Pumpe | l/h | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58B0 | DK-Adaptionsschritt | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58B1 | Funkenbrenndauer Zylinder 1 (Slave 7) | ms | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 |
| 0x58B2 | Funkenbrenndauer Zylinder 5 (Slave 11) | ms | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 |
| 0x58B3 | Funkenbrenndauer Zylinder 3 (Slave 9) | ms | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 |
| 0x58B4 | Funkenbrenndauer Zylinder 6 (Slave 12) | ms | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 |
| 0x58B5 | Funkenbrenndauer Zylinder 2 (Slave 8) | ms | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 |
| 0x58B6 | Funkenbrenndauer Zylinder 4 (Slave 10) | ms | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 |
| 0x58B7 | Bremsdruck | bar | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58B8 | Drehzahl Überwachung | 1/min | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x58B9 | Pedalwert Überwachung | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58BA | eingespritze Kraftstoffmasse | l/h | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58BB | PWM Kraftstoffpumpe | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58BC | Luftmasse Überwachung | mg/stroke | - | unsigned char | - | 2.71050191 | 1.0 | 0.0 |
| 0x58BD | Statusbyte externe Momentenanforderung 3 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58BE | Aschebeladung bei Leistungsbegrenzung OPF  | g | - | unsigned char | - | 1.0 | 64.00008031 | 0.0 |
| 0x58BF | Statusbyte vom Error Memory Management | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58C0 | Motordrehzahl Ersatzwert Überwachung | 1/min | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x58C1 | Laufunruhe Segmentzeit | µs | - | unsigned char | - | 7812.21826172 | 1.0 | 0.0 |
| 0x58C2 | Statusbyte MFF-Monitoring | mg/stroke | - | unsigned char | - | 2.71050191 | 1.0 | 0.0 |
| 0x58C3 | Statusbyte ISC-Monitoring | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58C4 | Statusbyte CRU-Monitoring | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58C5 | Drehzahl Überwachung (resetsicher) | 1/min | - | unsigned char | - | 32.0 | 1.0 | 0.0 |
| 0x58C6 | Status Einspritzventile (resetsicher) | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58C7 | LL-Solldrehzahlabweichung Überwachung | 1/min | - | signed char | - | 32.0 | 1.0 | 0.0 |
| 0x58C8 | I-Anteil Momentdifferenz Überwachung und Modell | Nm | - | signed char | - | 2.0 | 1.0 | 0.0 |
| 0x58C9 | I-Anteil LL passive Rampe aktiv | 0/1 | - | 0x01 | - | - | - | - |
| 0x58CA | PD-Anteil langsam Leerlaufregelung | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x58CB | PD-Anteil schnell Leerlaufregelung | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x58CC | Verlustmoment Überwachung | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x58CD | Grund für Leistungsbegrenzung von OPF  | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58CE | Carrierbyte Schalterstati | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58CF | Motormoment Sollwert Überwachung | Nm | - | unsigned char | - | 4.0 | 1.0 | 0.0 |
| 0x58D0 | Motormoment Istwert Überwachung | Nm | - | unsigned char | - | 4.0 | 1.0 | 0.0 |
| 0x58D1 | Moment aktueller Wert | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x58D2 | Sollposition obere Luftklappe in Grad | ° | - | unsigned char | - | 256.0 | 1.0 | -95.0 |
| 0x58D3 | Istposition obere Luftklappe in Grad | ° | - | unsigned char | - | 256.0 | 1.0 | -95.0 |
| 0x58D4 | Abweichung maximales Moment an Kupplung Überwachung | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x58D6 | Abweichung minimales Moment an Kupplung Überwachung | Nm | - | signed char | - | 8.0 | 1.0 | 0.0 |
| 0x58D7 | Spannung des Ansauglufttemperatursensors im Laderstrang | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x58D9 | Fehlercode Rechnerüberwachung: aktueller Wert | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58DA | Resetzähler Rechnerüberwachung: aktueller Wert | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58DB | Inhalt Statusbyte 1 Drehzahlüberwachung (resetsicher) | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58DC | Inhalt Statusbyte 2 Drehzahlüberwachung (resetsicher) | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58DD | ATL upstream | kPa | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58DE | Spannung für Drucksensor vor Drosselklappe | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x58E4 | Betriebsart Istwert | 0-n | - | 0xFF | _CNV_S_5__CNV_S_5_D_608 | - | - | - |
| 0x58E5 | Lastwert für Aussetzererkennung | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58E6 | Nulllastwert für Aussetzererkennung | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58E7 | Spannung Pedalwertgeber 1 Überwachung | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x58E8 | Spannung Pedalwertgeber 2 Überwachung | V | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 |
| 0x58E9 | Wasserpumpe Spannung | V | - | unsigned char | - | 0.1 | 1.0 | 0.0 |
| 0x58EA | Wasserpumpe Drehzahl | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58EB | Wasserpumpe Drehzahl Soll-Ist-Differenz | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58EC | Wasserpumpe Temperatur Elektronik | °C | - | unsigned char | - | 1.0 | 1.0 | -50.0 |
| 0x58ED | gemittelter Raildruck Bank 1 | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x58EF | Raildruck Bank 1 | hPa | - | unsigned char | - | 1358.5177002 | 1.0 | 0.0 |
| 0x58F0 | Dummy für Fehlerspecherfehlbedatung | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58F1 | DME - Losnummer | 0-n | - | 0xFF | _CNV_S_13_RANGE_STAT_839 | - | - | - |
| 0x58F2 | PWM-Signal des Mengensteuerventils | % | - | unsigned char | - | 0.390625 | 1.0 | 0.0 |
| 0x58F3 | Kraftstoffdruck vor Mengensteuerventil | hPa | - | unsigned char | - | 42.45375824 | 1.0 | 0.0 |
| 0x58F4 | Spannung für Kraftstoffdrucksensor vor Mengensteuerventil | V | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 |
| 0x58F5 | Eingangssignal Rückführregler 1 | V | - | signed char | - | 0.00488278 | 1.0 | -0.00000361 |
| 0x58F6 | Eingangssignal Rückführregler 2 | V | - | signed char | - | 0.00488278 | 1.0 | -0.00000361 |
| 0x58F7 | Laufunruhe Segmentzeit | µs | - | unsigned char | - | 30.51647758 | 1.0 | 0.0 |
| 0x58F8 | Segmentadaption Laufunruhe Zyl. 5 (Slave 11) | % | - | signed char | - | 0.06103515 | 1.0 | 0.00000008 |
| 0x58F9 | Segmentadaption Laufunruhe Zyl. 3 (Slave 9) | % | - | signed char | - | 0.06103515 | 1.0 | 0.00000008 |
| 0x58FA | Beladungsgrad Aktivkohlefilter TEV- Funktionstest | - | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 |
| 0x58FB | Zähler Drehzahlerhöhungen TEV- Funktionstest | cyc | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58FC | Katheizen aktiv | 0/1 | - | 0x01 | - | - | - | - |
| 0x58FD | Statusbit STATE_LV_ERR_COM_MON_1_2 | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58FE | Statusbyte externe Momentenanforderung | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x58FF | Umweltbedingung unbekannt | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 4 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0X01 | ERROR |
| 0X02 | ARGUMENT FEHLERHAFT |
| 0x03 | ERROR_DIAGSG |
| 0xXY | ERROR_UNKNOWN |

<a id="table-msd85uds-cnv-s-2-def-bit-ub-741-cm"></a>
### MSD85UDS_CNV_S_2_DEF_BIT_UB_741_CM

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | -- |
| 1 | -- |

<a id="table-res-0x1061-r"></a>
### RES_0X1061_R

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_FS_ENDE_WABL | - | - | + | 0/1 | high | unsigned char | - | - | - | - | - | 0: Verriegelt (loeschen von Einzelfehlern und PDTCs wird unterbunden) 1: Entriegelt (loeschen von Einzelfehlern und PDTCs wird nicht unterbunden) |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 533 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| FS_LOESCHEN_PERMANENT | 0x1060 | - | Job zum Löschen der Permanent-DTCs | - | - | - | - | - | - | - | - | - | 31 | - | - |
| FEHLERSPEICHER_ENDE_WERKSABLAUF | 0x1061 | - | Löschen von Einzelfehlern und Permanent-DTCs unterbindet | - | - | - | - | - | - | - | - | - | 31 | - | RES_0x1061_R |
| ITANS | 0x4200 | STAT_ANSAUGLUFTTEMPERATUR_WERT | Ansauglufttemperatur 1 | °C | TIA | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| IPUMG | 0x4201 | STAT_UMGEBUNGSDRUCK_WERT | Umgebungsdruck | hPa | AMP_MES | - | unsigned int | - | 0.08291753 | 1.0 | 0.0 | - | 22;2C | - | - |
| IPSAU | 0x4202 | STAT_SAUGROHRDRUCK_WERT | Saugrohrdruck | hPa | MAP_MES | - | unsigned int | - | 0.08291753 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILMKG | 0x4203 | STAT_LUFTMASSE_WERT | Massenstrom vom HFM | kg/h | MAF_KGH_MES[1] | - | unsigned int | - | 0.03125 | 1.0 | 0.0 | - | 22;2C | - | - |
| ITUMG | 0x4204 | STAT_UMGEBUNGSTEMPERATUR_WERT | Umgebungstemperatur | °C | TAM | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| IPLAD | 0x4205 | STAT_LADEDRUCK_WERT | Saugrohrdruck 1 / Ladedruck 1 | hPa | MAP_DIP_MES_BAS[1] | - | unsigned int | - | 0.08291753 | 1.0 | 0.0 | - | 22;2C | - | - |
| ITKUM | 0x4300 | STAT_KUEHLMITTELTEMPERATUR_WERT | Kühlwassertemperatur | °C | TCO | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| ITKKA | 0x4301 | STAT_0X4301_WERT | Kühlerauslasstemperatur | °C | TCO_2 | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| IPWAB | 0x4302 | STAT_WASSERPUMPENLEISTUNG_BSD_WERT | Wasserpumpe Leistung über BSD | % | REL_CWP_PWR | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| ITWAE | 0x4303 | STAT_WASSERPUMPE_ELEKTRONIK_TEMPERATUR_WERT | Wasserpumpe Elektronik Temperatur | °C | TEMP_EL_CWP_SEC | - | unsigned char | - | 1.0 | 1.0 | -50.0 | - | 22;2C | - | - |
| IIWAP | 0x4304 | STAT_WASSERPUMPE_STROM_WERT | Wasserpumpe Strom | A | CUR_CNS_CWP_SEC | - | unsigned char | - | 0.2 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4307_WERT | 0x4307 | STAT_0X4307_WERT | Wasserpumpe Betriebsart | 0-n | BA_WM_IST | - | unsigned char | _CNV_S_12__CNV_S_12__656 | - | - | - | - | 22;2C | - | - |
| IMLOE | 0x4400 | STAT_OELSTAND_LANGZEIT_MITTEL_WERT | Ölstand Mittelwert Langzeit | mm | OZ_NIVLANGT | - | unsigned char | - | 0.29296875 | 1.0 | 0.0 | - | 22;2C | - | - |
| IFSOE | 0x4401 | STAT_FUELLSTAND_MOTOROEL_WERT | Füllstand Motoröl | - | OZ_LP | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| ITOEL | 0x4402 | STAT_OELTEMPERATUR_WERT | Öltemperatur | °C | TOEL | - | signed int | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| IKVLS | 0x4403 | STAT_KRAFTSTOFFVERBRAUCH_SEIT_SERVICE_WERT | Kraftstoff-Verbrauch seit letztem Service | - | OZ_KVBSM_UL | - | unsigned long | - | 0.00012207 | 1.0 | 0.0 | - | 22;2C | - | - |
| IKMLS | 0x4404 | STAT_WEG_SEIT_SERVICE_WERT | km seit letztem Service | km | OZ_OELKM | - | unsigned int | - | 10.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| RNIOE | 0x4405 | STAT_OELSENSOR_NIVEAU_ROH_WERT | Ölsensor Niveau Rohwert | - | OZ_NIVR | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| RQUOE | 0x4406 | STAT_OELSENSOR_QUALITAET_ROH_WERT | Ölsensor Qualität Rohwert | - | OZ_PERMR | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| RTOEL | 0x4407 | STAT_OELSENSOR_TEMPERATUR_ROH_WERT | Ölsensor Temperatur Rohwert | - | OZ_TEMPR | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| ITSOE | 0x4408 | STAT_OELSENSOR_TEMPERATUR_WERT | Ölsensor Temperatur | °C | OZ_TEMPAKT | - | signed int | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| INIOE | 0x4409 | STAT_OELSENSOR_NIVEAU_WERT | Ölsensor Niveau | mm | OZ_NIVAKT | - | unsigned char | - | 0.29296875 | 1.0 | 0.0 | - | 22;2C | - | - |
| IQOEL | 0x440A | STAT_OELSENSOR_QUALITAET_WERT | Ölsensor Qualität | - | OZ_PERMAKT | - | unsigned int | - | 0.00009155 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x440B_WERT | 0x440B | STAT_0X440B_WERT | Länderfaktor 1 codiert | - | OZ_LF1C | - | unsigned char | - | 0.01 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x440C_WERT | 0x440C | STAT_0X440C_WERT | Länderfaktor 2 codiert | - | OZ_LF2C | - | unsigned char | - | 0.01 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x440D_WERT | 0x440D | STAT_0X440D_WERT | Länderfaktor 1 | - | OZ_LF1T | - | unsigned char | - | 0.01 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x440E_WERT | 0x440E | STAT_0X440E_WERT | Länderfaktor 2 | - | OZ_LF2T | - | unsigned char | - | 0.01 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x440F_WERT | 0x440F | STAT_0X440F_WERT | Kurzmittelwert-Niveau für den Tester | mm | OZ_NIVKRZT | - | unsigned char | - | 0.29296875 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4411_WERT | 0x4411 | STAT_0X4411_WERT | Restweg aus Kraftstoffverbrauch abgeleitet | km | OZ_RWKVB | - | signed int | - | 10.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4412_WERT | 0x4412 | STAT_0X4412_WERT | Öl-Alter in Monate | - | OZ_OELZEIT | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4418_WERT | 0x4418 | STAT_0X4418_WERT | Status Peilstabanzeige | - | OZ_LV | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4419_WERT | 0x4419 | STAT_0X4419_WERT | Kilometerstand letzter Ölwechsel | km | OZ_KMLOW | - | signed long | - | 10.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x441E_WERT | 0x441E | STAT_0X441E_WERT | Kurzzeitmittelwert | mm | OZ_KRZOR | - | unsigned char | - | 0.29296875 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x441F_WERT | 0x441F | STAT_0X441F_WERT | Vormittelwert | mm | OZ_VORMW | - | unsigned char | - | 0.29296875 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4421_WERT | 0x4421 | STAT_0X4421_WERT | Orientierungswert Counter | - | OZ_ORICNT | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4422_WERT | 0x4422 | STAT_0X4422_WERT | Vormittelwert Counter | - | OZ_VORMWCNT | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4423_WERT | 0x4423 | STAT_0X4423_WERT | Kurzzeitmittelwert Counter | - | OZ_KRZCNT | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4424_WERT | 0x4424 | STAT_0X4424_WERT | Langzeitmittelwert Counter | - | OZ_LGMWCNT | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| SSPEI | 0x4505 | STAT_NW_EINLASSSPREIZUNG_SOLL_WERT | Sollwert Einlassspreizung | ° KW | CAM_SP_IVVT_IN | - | signed int | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| IPNWE | 0x4506 | STAT_POSITION_NOCKENWELLE_EINLASS_WERT | Nockenwellenposition Einlass | ° KW | PSN_CAM_IN_1 | - | unsigned int | - | 0.375 | 1.0 | -95.99999714 | - | 22;2C | - | - |
| IPNWA | 0x4507 | STAT_POSITION_NOCKENWELLE_AUSLASS_WERT | Nockenwellenposition Auslass | ° KW | PSN_CAM_EX_1 | - | unsigned int | - | 0.375 | 1.0 | -95.99999714 | - | 22;2C | - | - |
| ISNWA | 0x4509 | STAT_NW_AUSLASSSPREIZUNG_WERT | Istwert Auslassspreizung Bank 1 | ° KW | CAM_EX[1] | - | unsigned char | - | -0.375 | 1.0 | -39.99999785 | - | 22;2C | - | - |
| NSNWA | 0x450A | STAT_NW_NORMSPREIZUNG_AUSLASS_WERT | Normspreizung Auslass | ° KW | CAM_SP_REF_EX | - | signed int | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| NSNWE | 0x450B | STAT_NW_NORMSPREIZUNG_EINLASS_WERT | Normspreizung Einlass | ° KW | CAM_SP_REF_IN | - | signed int | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| ISNWE | 0x4510 | STAT_0X4510_WERT | Istwert Einlassspreizung Bank 1 | ° KW | CAM_IN_H[1] | - | signed int | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| SUGEN | 0x4602 | STAT_SOLLWERT_GENERATORSPANNUNG_WERT | Generator Sollspannung über BSD | V | V_ALTER_SP | - | unsigned char | - | 0.1 | 1.0 | 10.6 | - | 22;2C | - | - |
| ITGEE | 0x4603 | STAT_GENERATOR_ELEKTRONIKTEMPERATUR_WERT | Chiptemperatur Generator 1 | °C | TCHIP | - | signed int | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| IIGEN | 0x4604 | STAT_GENERATOR_STROM_WERT | Generator Strom | - | I_GEN | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| VGENE | 0x4605 | STAT_GENERATOR_CHIPVERSION_WERT | Chipversion Generator 1 | - | BSDGENCV | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| VGENR | 0x4606 | STAT_GENERATOR_REGLERVERSION_WERT | Reglerversion Generator 1 | - | BSDGENREGV | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| VGENH | 0x4607 | STAT_GENERATOR_HERSTELLERCODE_WERT | Herstellercode Generator 1 | - | GEN_MANUFAK | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| VGTYP | 0x4608 | STAT_GENERATOR_TYP_WERT | Kennung Generatortyp Generator 1 | - | GEN_TYPKENN | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUK87 | 0x4609 | STAT_KL87_SPANNUNG_WERT | Kl.87 Spannung / Versorgung DME | V | VB | - | unsigned char | - | 0.10156249 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUIBS | 0x460B | STAT_UBATT_IBS_WERT | Batteriespannung von IBS gemessen | - | U_BATT | - | unsigned int | - | 0.00025 | 1.0 | 6.0 | - | 22;2C | - | - |
| IUADW | 0x460C | STAT_UBATT_AD_WANDLER_WERT | Batteriespannung vom AD-Wandler DME | V | VB_BAS | - | unsigned int | - | 0.02806012 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x460D_WERT | 0x460D | STAT_0X460D_WERT | Korrekturwert Abschaltung | - | ABSCH_KORR | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| TDSTF | 0x460E | STAT_ABSTAND_ZUR_STARTFAEHIGKEITSGRENZE_WERT | Abstand zur Startfähigkeitsgrenze | - | D_SOC | - | signed int | - | 0.00305176 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILBAT | 0x460F | STAT_BATTERIELAST_WERT | Batterielast | % | LOAD_BAT | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STELU | 0x4611 | STAT_E_LUEFTER_PWM_SOLL_WERT | Sollwert E-Lüfter als PWM Wert | % | N_PERC_ECF | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| IIEGE | 0x4612 | STAT_GENERATOR_ERREGERSTROM_WERT | Erregerstrom Generator 1 | A | IERR | - | unsigned char | - | 0.125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4613_WERT | 0x4613 | STAT_0X4613_WERT | Kopierter Wert von zum Generator gesendeter Sollspannung Generator 1 | V | U_FGEN | - | unsigned int | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| IGENA | 0x4614 | STAT_AUSLASTUNGSGRAD_GENERATOR_WERT | Auslastungsgrad Generator 1 | % | DFSIGGEN | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4615_WERT | 0x4615 | STAT_0X4615_WERT | Kopie begrenzter Erregerstrom Generator 1 | A | IERRFGRENZ | - | unsigned char | - | 0.125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4616_WERT | 0x4616 | STAT_0X4616_WERT | Kopie Generator 1 LR Vorgabe auf Bus gelegt | s | TLRFGEN | - | unsigned char | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| MGENG | 0x4617 | STAT_GEFILTERTES_GENERATORMOMENT_ABSOLUT_AUSGANG_WERT | gefiltertes Generatormoment absolut Ausgang | Nm | MD_GENNM_NA | - | signed int | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4618_WERT | 0x4618 | STAT_0X4618_WERT | Kopie Drehzahlschwelle für LR-Funktion Generator 1 aktiv | 0/1 | B_LRFOFF | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x4619_WERT | 0x4619 | STAT_0X4619_WERT | Bedingung BSD II Protokoll | 0/1 | B_BSDPROT2 | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| IUNGE | 0x461A | STAT_NOMINALE_GENERATORSPANNUNG_WERT | Nominale Generatorspannung | V | UREGNOM | - | unsigned int | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x461B_WERT | 0x461B | STAT_0X461B_WERT | angeschlossenes Batterieladegerät erkannt  | 0/1 | B_ULADE | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x461C_WERT | 0x461C | STAT_0X461C_WERT | bisheriger Wasserverlust | g/Ah | QV_H2O_ZG | High | unsigned long | - | 1.0 | 360000000.0 | 0.0 | - | 22;2C | - | - |
| ANTEIL_RUSS_OPF | 0x4620 | STAT_ANTEIL_RUSS_OPF_WERT | Rußbeladung OPF  | g | M_SOOT_PF_ACT | - | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22;2C | - | - |
| ANTEIL_ASCHE_OPF | 0x4621 | STAT_ANTEIL_ASCHE_OPF_WERT | Aschebeladung OPF  | g | M_ASH_LOAD_PF | - | unsigned int | - | 1.0 | 1000.0 | 0.0 | - | 22;2C | - | - |
| REGBEDARF_OPF | 0x4622 | STAT_REGBEDARF_OPF_WERT | Regenerationsdringlichkeit OPF  | % | LOAD_SOOT_PERC_PF | - | unsigned int | - | 1.0 | 100.0 | 0.0 | - | 22;2C | - | - |
| REGGRUND_OPF | 0x4623 | STAT_REGGRUND_OPF_WERT | Grund für Regeneration OPF  | - | LF_LOAD_SOOT_PERC_PF_MAX | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| BERTIEB_H_VREG_OPF | 0x4624 | STAT_BERTIEB_H_VREG_OPF_WERT | Betriebstundenzähler seit letzter vollständiger Regeneration OPF | h | TRT_LST_RGN_PF_HIS | - | unsigned long | - | 1.0 | 36000.0 | 0.0 | - | 22;2C | - | - |
| FAHRSTR_H_VREG_OPF | 0x4625 | STAT_FAHRSTR_H_VREG_OPF_WERT | Gefahrene Wegstrecke seit letzter vollständiger Regeneration OPF | m | DIST_LST_RGN_PF_HIS | - | unsigned long | - | 100.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| TEMP_OPF | 0x4626 | STAT_TEMP_OPF_WERT | Partikelfiltertemperatur OPF  | °C | TEG_PF[0] | - | unsigned int | - | 1.0 | 16.0 | -273.15 | - | 22;2C | - | - |
| FAHRSTR_TAUSCH_OPF | 0x4627 | STAT_FAHRSTR_TAUSCH_OPF_WERT | Wegstrecke bis OPF Tausch wegen Asche benötigt  | km | CTR_KM_PF_CHG_ASH | - | unsigned int | - | 10.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| ISBV1 | 0x4700 | STAT_SONDENBEREITSCHAFT_VORKAT_BANK1 | Status Lambdasonde betriebsbereit vor Katalysator Bank 1 | 0/1 | LV_IPLSL_VLD[1] | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| IUSO1 | 0x4702 | STAT_SONDENSPANNUNG_VORKAT_BANK1_MIT_OFFSET_WERT | Spannung Lambdasonde vor Katalysator Bank 1 mit Offsetkorrektur | V | VLS_UP_COR[1] | - | unsigned int | - | 0.00488281 | 1.0 | 0.0 | - | 22;2C | - | - |
| SINT1 | 0x4704 | STAT_LAMBDA_BANK1_SOLL_WERT | Lambda Sollwert Bank1 | - | LAMB_BAS[1] | - | unsigned int | - | 0.00097656 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4706_WERT | 0x4706 | STAT_0X4706_WERT | STATUSBIT MSV-Relais | 0/1 | LV_RLY_VCV | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x4707_WERT | 0x4707 | STAT_0X4707_WERT | PWM-Signal Umluftventil 1 | % | RFPPWM[1] | - | unsigned int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4709_WERT | 0x4709 | STAT_0X4709_WERT | Lernvariante Hochdruckpumpenrelais | 0/1 | LV_RLY_HPDI | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x470A_WERT | 0x470A | STAT_0X470A_WERT | Versorgungsspannung Einspritzung /Zündung (HDPI-Relais) | V | VB_RLY_HPDI | - | unsigned int | - | 0.02806012 | 1.0 | 0.0 | - | 22;2C | - | - |
| ISKUB | 0x4800 | STAT_KUPPLUNGSSCHALTER_BETAETIGT_WERT | Kupplungsschalter Status | 0/1 | LV_CS | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISKUV | 0x4801 | STAT_KUPPLUNGSSCHALTER_VORHANDEN_WERT | Kupplungsschalter vorhanden | 0/1 | LV_CS_CUS | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISSPO | 0x4802 | STAT_SPORTTASTER_BETAETIGT_WERT | Sporttaster aktiv | 0/1 | LV_SOF_SWI | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISKLI | 0x4803 | STAT_KLIMA_EIN | Status Klima ein | - | STATE_ACIN_CAN | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| ISSLP | 0x4804 | STAT_SEKUNDAERLUFTPUMPE_WERT | Sekundärluft Pumpe aktiv | 0/1 | LV_SAP | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISSRC | 0x4805 | STAT_STARTRELAIS_UEBER_CAN_WERT | Startrelais über CAN aktiv | 0/1 | LV_RLY_ST_CAN | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x4806_WERT | 0x4806 | STAT_0X4806_WERT | Steuergeräte-Innentemperatur | °C | TECU | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| INMOT | 0x4807 | STAT_MOTORDREHZAHL_WERT | Motor Drehzahl | 1/min | N | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| SNLLD | 0x4808 | STAT_LEERLAUFDREHZAHL_SOLL_WERT | Leerlauf Solldrehzahl | 1/min | N_SP_IS | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| ISLLA | 0x4809 | STAT_LEERLAUF_AKTIV | Status LL | 0/1 | LV_IS | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISKME | 0x480A | STAT_KILOMETERSTAND_WERT | Kilometerstand Auflösung 1 km | km | CTR_KM_BN | - | unsigned long | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IFPWG | 0x480B | STAT_FAHRERWUNSCH_PEDAL_WERT | Pedalwert Fahrerwunsch in % | % | PV_AV | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x482E_WERT | 0x482E | STAT_0X482E_WERT | Status Wasserpumpe Lagerstuhl | 0/1 | LV_PWL_CWP | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x4830_WERT | 0x4830 | STAT_0X4830_WERT | Zähler Gradientenüberwachungsdiagnose beendet, Bank 1 | - | CTR_NR_DIAG_PUE_LS_DOWN[1] | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4831_WERT | 0x4831 | STAT_0X4831_WERT | Zähler Gradientenüberwachungsdiagnose beendet, Bank 2 | - | CTR_NR_DIAG_PUE_LS_DOWN[2] | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4832_WERT | 0x4832 | STAT_0X4832_WERT | Veränderlicher Durchschnittswert der Gradientenüberwachung, Bank 1 | mV/s | VLS_DOWN_PUE_MMV[1] | - | signed int | - | 2.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4833_WERT | 0x4833 | STAT_0X4833_WERT | Veränderlicher Durchschnittswert der Gradientenüberwachung, Bank 2 | mV/s | VLS_DOWN_PUE_MMV[2] | - | signed int | - | 2.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4834_WERT | 0x4834 | STAT_0X4834_WERT | Gepeicherter Maximalgradient, O2-Sensor downstream über alle Fahrzyklen, Bank 1 | mV/s | VLS_DOWN_PUE_SAVE_MAX[1] | - | signed int | - | 2.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4835_WERT | 0x4835 | STAT_0X4835_WERT | Gepeicherter Maximalgradient, O2-Sensor downstream über alle Fahrzyklen, Bank 2 | mV/s | VLS_DOWN_PUE_SAVE_MAX[2] | - | signed int | - | 2.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4836_WERT | 0x4836 | STAT_0X4836_WERT | Gespeicherter Minimalgradient, O2-Sensor downstream über alle Fahrzyklen, Bank 1 | mV/s | VLS_DOWN_PUE_SAVE_MIN[1] | - | signed int | - | 2.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4837_WERT | 0x4837 | STAT_0X4837_WERT | Gespeicherter Minimalgradient, O2-Sensor downstream über alle Fahrzyklen, Bank 2 | mV/s | VLS_DOWN_PUE_SAVE_MIN[2] | - | signed int | - | 2.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4838_WERT | 0x4838 | STAT_0X4838_WERT | Quadrierte Standardabweichung der Gradientenüberwachung, Bank 1 | (V/s)² | VLS_DOWN_PUE_STD[1] | - | unsigned long | - | 0.000128 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4839_WERT | 0x4839 | STAT_0X4839_WERT | Quadrierte Standardabweichung der Gradientenüberwachung, Bank 2 | (V/s)² | VLS_DOWN_PUE_STD[2] | - | unsigned long | - | 0.000128 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4840_WERT | 0x4840 | STAT_0X4840_WERT | berechneter Hochdrucksollwert, Bank 1  | hPa | FUP_SP_MPL[0] | - | unsigned int | - | 5.30672169 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4842_WERT | 0x4842 | STAT_0X4842_WERT | Drehzahl Kraftstoffpumpe | 1/min | N_EFP_AV | - | unsigned char | - | 50.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4843_WERT | 0x4843 | STAT_0X4843_WERT | Hochdruckreglerwert Ausgang  | MPa | PRDR_W_RB[0] | - | signed int | - | 0.0005 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4850_WERT | 0x4850 | STAT_0X4850_WERT | Zähler Verbrennungsaussetzer Zylinder 1 (Slave 7) | - | CTR_MIS_DET_CYL[1] | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4851_WERT | 0x4851 | STAT_0X4851_WERT | Zähler Verbrennungsaussetzer Zylinder 5 (Slave 11 )  | - | CTR_MIS_DET_CYL[2] | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4852_WERT | 0x4852 | STAT_0X4852_WERT | Zähler Verbrennungsaussetzer Zylinder 3(Slave 9)  | - | CTR_MIS_DET_CYL[3] | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4853_WERT | 0x4853 | STAT_0X4853_WERT | Zähler Verbrennungsaussetzer Zylinder 6 (Slave 12)  | - | CTR_MIS_DET_CYL[4] | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4854_WERT | 0x4854 | STAT_0X4854_WERT | Zähler Verbrennungsaussetzer Zylinder 2(Slave 8)  | - | CTR_MIS_DET_CYL[5] | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4855_WERT | 0x4855 | STAT_0X4855_WERT | Zähler Verbrennungsaussetzer Zylinder 4 (Slave 10) | - | CTR_MIS_DET_CYL[6] | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| P_DRUCKSENS_OPF | 0x4882 | STAT_P_DRUCKSENS_OPF_WERT | OPF Druck Istwert | hPa | dip_pf | - | unsigned int | - | 1.0 | 12.06017667 | 0.0 | - | 22;2C | - | - |
| T_TEMPSENS_OPF | 0x4883 | STAT_T_TEMPSENS_OPF_WERT | OPF Tempperatur 1 Master /2 Slave Istwert | °C | TEG_MES[1] | - | unsigned int | - | 1.0 | 16.0 | -273.15 | - | 22;2C | - | - |
| V_DRUCKSENS_OPF | 0x4886 | STAT_V_DRUCKSENS_OPF_WERT | OPF Rohwert Drucksensorsignal Master1 / Slave2 | V | V_DIP_PF[0] | - | unsigned int | - | 1.0 | 204.8 | 0.0 | - | 22;2C | - | - |
| V_TEMPSENS_OPF | 0x4887 | STAT_V_TEMPSENS_OPF_WERT | OPF Rohwert Temperatursignal Master1 / Slave2 | V | VP_TEG_MES[1] | - | unsigned int | - | 1.0 | 6553.60054018 | 0.0 | - | 22;2C | - | - |
| IUPV1 | 0x4A00 | STAT_PWG1_VERSORGUNGSSPANNUNG_WERT | Versorgung FWG 1 | V | VCC_PVS_1 | - | unsigned int | - | 0.00976559 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUPV2 | 0x4A01 | STAT_PWG2_VERSORGUNGSSPANNUNG_WERT | Versorgung FWG 2 | V | VCC_PVS_2 | - | unsigned int | - | 0.00976559 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUPW1 | 0x4A04 | STAT_PWG1_SPANNUNG_WERT | Spannung Pedalwertgeber 1 | V | V_PVS_1 | - | unsigned int | - | 0.00488281 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUPW2 | 0x4A05 | STAT_PWG2_SPANNUNG_WERT | Spannung Pedalwertgeber 2 | V | V_PVS_2 | - | unsigned int | - | 0.00488281 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUKUM | 0x4A09 | STAT_KUEHLMITTELTEMPERATUR_SPANNUNG_WERT | Spannung Motortemperatur | V | VP_TCO[1] | - | unsigned int | - | 0.00015259 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUKUA | 0x4A0A | STAT_KUEHLERAUSLASSTEMPERATUR_SPANNUNG_WERT | Spannung Kühlmitteltemperatur Kühlerausgang | V | VP_TCO[2] | - | unsigned int | - | 0.00015259 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUUMG | 0x4A0B | STAT_UMGEBUNGSDRUCK_SPANNUNG_WERT | Spannung DME Umgebungsdruck | V | V_AMP | - | unsigned int | - | 0.00488281 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUSGI | 0x4A0E | STAT_STEUERGERAETE_INNENTEMPERATUR_SPANNUNG_WERT | Spannung SG-Innentemperatur | V | VP_TECU | - | unsigned int | - | 0.00015259 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A0F_WERT | 0x4A0F | STAT_0X4A0F_WERT | Spannung Kl.15 | V | V_IGK_BAS | - | unsigned int | - | 0.02806012 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUK15 | 0x4A10 | STAT_KL15_SPANNUNG_WERT | Spannung Kl15 | V | V_IGK_MES | - | unsigned int | - | 0.02806012 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUSV1 | 0x4A11 | STAT_SONDENSPANNUNG_VORKAT_BANK1_WERT | Spannung Lambdasonde vor Katalysator Bank 1 | V | VLS_UP[1] | - | unsigned int | - | 0.00488281 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUSN1 | 0x4A13 | STAT_SONDENSPANNUNG_NACHKAT_BANK1_WERT | Spannung Lambdasonde hinter Katalysator Bank 1 | V | VLS_DOWN[1] | - | unsigned int | - | 0.00488281 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A15_WERT | 0x4A15 | STAT_0X4A15_WERT |  Turboladerdiagnose im Niederdruckbereich abgelaufen | 0/1 | LV_END_DIAG_TCHA_PRS_LOW | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x4A16_WERT | 0x4A16 | STAT_0X4A16_WERT |  Turboladerdiagnose im Hochdruckbereich abgelaufen | 0/1 | LV_END_DIAG_TCHA_PRS_HIGH | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| IUDMT | 0x4A17 | STAT_DMTL_SPANNUNG_WERT | Spannung Strommessung DMTL | V | V_DMTL | - | unsigned int | - | 0.00488281 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A1A_WERT | 0x4A1A | STAT_0X4A1A_WERT | Test-Bedingung Turboladerdiagnose Unterladefehler erfüllt | 0/1 | LV_CDN_DIAG_TCHA_PRS_LOW | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x4A1C_WERT | 0x4A1C | STAT_0X4A1C_WERT | Test-Bedingung Turboladerdiagnose Überladefehler erfüllt | 0/1 | LV_CDN_DIAG_TCHA_PRS_HIGH | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ITKUA | 0x4A21 | STAT_KUEHLERAUSLASSTEMPERATUR_WERT | Kühlmitteltemperatur Kühlerausgang | °C | TCO_2_MES | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| ITSGI | 0x4A22 | STAT_STEUERGERAETE_INNENTEMPERATUR_WERT | Steuergeräte-Innentemperatur | °C | TECU | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| SWDKL | 0x4A24 | STAT_DK_WINKEL_SOLL_WERT | Drosselklappe Sollwert | ° DK | TPS_SP | - | unsigned int | - | 0.00729415 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A26_WERT | 0x4A26 | STAT_0X4A26_WERT | Saugrohdruck Absolut | hPa | map | - | unsigned int | - | 0.08291753 | 1.0 | 0.0 | - | 22;2C | - | - |
| IPPW1 | 0x4A27 | STAT_PWG1_WERT | Pedalwertgeber Potentiometer 1 | % | PV_AV_1 | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| IPPW2 | 0x4A28 | STAT_PWG2_WERT | Pedalwertgeber Potentiometer 2 | % | PV_AV_2 | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| RFPWG | 0x4A29 | STAT_FAHRERWUNSCH_PEDAL_ROH_WERT | Fahrpedalwert | % | PV_AV_RAW | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A2A_WERT | 0x4A2A | STAT_0X4A2A_WERT | Sollwert elektrische Kraftstoffpumpe | hPa | FUP_EFP_SP | - | unsigned int | - | 2.65336084 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A2B_WERT | 0x4A2B | STAT_0X4A2B_WERT | Temperatur vor Drosselklappe | °C | TANS | - | signed int | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A2C_WERT | 0x4A2C | STAT_0X4A2C_WERT | Druck vor Drosselklappe | hPa | PVDKDS | - | unsigned int | - | 0.125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A2D_WERT | 0x4A2D | STAT_0X4A2D_WERT | Druck nach Drosselklappe | hPa | PS_IST | - | unsigned int | - | 0.125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A2E_WERT | 0x4A2E | STAT_0X4A2E_WERT | Kraftstoffniederdrucksensor | hPa | FUP_EFP | - | unsigned int | - | 2.65336084 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A2F_WERT | 0x4A2F | STAT_0X4A2F_WERT | Raildruck | hPa | FUP_MES[0] | - | unsigned int | - | 5.30672169 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILUZ1 | 0x4A30 | STAT_LAUFUNRUHE_ZYL1_WERT | Laufunruhe Zylinder 1 (Slave 7) | µs | ER_CYL[0] | - | signed long | - | 0.23841858 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILUZ2 | 0x4A31 | STAT_LAUFUNRUHE_ZYL2_WERT | Laufunruhe Zylinder 2 (Slave 8) | µs | ER_CYL[4] | - | signed long | - | 0.23841858 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILUZ3 | 0x4A32 | STAT_LAUFUNRUHE_ZYL3_WERT | Laufunruhe Zylinder 3 (Slave 9) | µs | ER_CYL[2] | - | signed long | - | 0.23841858 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILUZ4 | 0x4A33 | STAT_LAUFUNRUHE_ZYL4_WERT | Laufunruhe Zylinder 4 (Slave 10) | µs | ER_CYL[5] | - | signed long | - | 0.23841858 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILUZ5 | 0x4A34 | STAT_LAUFUNRUHE_ZYL5_WERT | Laufunruhe Zylinder 5 (Slave 11) | µs | ER_CYL[1] | - | signed long | - | 0.23841858 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILUZ6 | 0x4A35 | STAT_LAUFUNRUHE_ZYL6_WERT | Laufunruhe Zylinder 6 (Slave 12) | µs | ER_CYL[3] | - | signed long | - | 0.23841858 | 1.0 | 0.0 | - | 22;2C | - | - |
| ISKLO | 0x4A36 | STAT_STATUS_KLOPFEN_WERT | Status Klopfen | 0/1 | LV_KNK | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| IUKZ1 | 0x4A37 | STAT_KLOPFWERT_ZYL1_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 1 (Slave 7) | V | NL[0] | - | unsigned int | - | 0.00007629 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUKZ2 | 0x4A38 | STAT_KLOPFWERT_ZYL2_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 2 (Slave 8) | V | NL[4] | - | unsigned int | - | 0.00007629 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUKZ3 | 0x4A39 | STAT_KLOPFWERT_ZYL3_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 3 (Slave 9) | V | NL[2] | - | unsigned int | - | 0.00007629 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUKZ4 | 0x4A3A | STAT_KLOPFWERT_ZYL4_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 4 (Slave 10) | V | NL[5] | - | unsigned int | - | 0.00007629 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUKZ5 | 0x4A3B | STAT_KLOPFWERT_ZYL5_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 5 (Slave 11) | V | NL[1] | - | unsigned int | - | 0.00007629 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUKZ6 | 0x4A3C | STAT_KLOPFWERT_ZYL6_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 6 (Slave 12) | V | NL[3] | - | unsigned int | - | 0.00007629 | 1.0 | 0.0 | - | 22;2C | - | - |
| IKSZ1 | 0x4A3D | STAT_KLOPFSIGNAL_ZYL1_WERT | Klopfsignal Zylinder 1 (Slave 7) | V | KNKS[0] | - | unsigned int | - | 0.00007629 | 1.0 | 0.0 | - | 22;2C | - | - |
| IKSZ5 | 0x4A3E | STAT_KLOPFSIGNAL_ZYL5_WERT | Klopfsignal Zylinder 5 (Slave 11) | V | KNKS[1] | - | unsigned int | - | 0.00007629 | 1.0 | 0.0 | - | 22;2C | - | - |
| IKSZ4 | 0x4A3F | STAT_KLOPFSIGNAL_ZYL4_WERT | Klopfsignal Zylinder 4 (Slave 10) | V | KNKS[5] | - | unsigned int | - | 0.00007629 | 1.0 | 0.0 | - | 22;2C | - | - |
| IKSZ3 | 0x4A40 | STAT_KLOPFSIGNAL_ZYL3_WERT | Klopfsignal Zylinder 3 (Slave 9) | V | KNKS[2] | - | unsigned int | - | 0.00007629 | 1.0 | 0.0 | - | 22;2C | - | - |
| IKSZ6 | 0x4A41 | STAT_KLOPFSIGNAL_ZYL6_WERT | Klopfsignal Zylinder 6 (Slave 12) | V | KNKS[3] | - | unsigned int | - | 0.00007629 | 1.0 | 0.0 | - | 22;2C | - | - |
| IKSZ2 | 0x4A42 | STAT_KLOPFSIGNAL_ZYL2_WERT | Klopfsignal Zylinder 2 (Slave 8) | V | KNKS[4] | - | unsigned int | - | 0.00007629 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZWZ1 | 0x4A49 | STAT_ZUENDWINKEL_ZYL1_WERT | Zündwinkel Zylinder 1 | ° KW | IGA_IGC[0] | - | unsigned char | - | 0.375 | 1.0 | -35.62499894 | - | 22;2C | - | - |
| ILASB | 0x4A4B | STAT_BERECHNETE_LAST_WERT | Berechneter Lastwert | % | LOAD_CLC | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| ISACR | 0x4A4E | STAT_KLIMAKOMPRESSORRELAIS_EIN | Klimakompressorrelais Ein | 0/1 | LV_ACCOUT_RLY | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ILAB1 | 0x4A50 | STAT_LAMBDA_BANK1_WERT | Lambdawert vor Katalysator Bank 1 | - | LAMB_LS_UP[1] | - | unsigned int | - | 0.00097656 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILAB2 | 0x4A51 | STAT_LAMBDA_BANK2_WERT | Lambdawert vor Katalysator Bank 2 | - | LAMB_LS_UP[2] | - | unsigned int | - | 0.00097656 | 1.0 | 0.0 | - | 22;2C | - | - |
| IRNK1 | 0x4A52 | STAT_READINESS_SONDE_NACHKAT_BANK1_WERT | Status LS hinter Katalysator Bank 1 | 0/1 | LV_LS_DOWN_READY[1] | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISHN1 | 0x4A54 | STAT_SONDENHEIZUNG_NACHKAT_BANK1_WERT | Status LS Heizung hinter Katalysator Bank 1 | 0-n | STATE_LSH_DOWN[1] | - | unsigned char | _CNV_S_7_EGCP_RANGE_234 | - | - | - | - | 22;2C | - | - |
| ISHV1 | 0x4A56 | STAT_SONDENHEIZUNG_VORKAT_BANK1_WERT | Status LS Heizung vor Katalysator Bank 1 | 0-n | STATE_LSH_UP[1] | - | unsigned char | _CNV_S_7_EGCP_RANGE_234 | - | - | - | - | 22;2C | - | - |
| IAHV1 | 0x4A58 | STAT_SONDENHEIZUNG_PWM_VORKAT_BANK1_WERT | Lambdasondenheizung PWM vor Katalysator Bank 1 | % | LSHPWM_UP[1] | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| IAHN1 | 0x4A59 | STAT_SONDENHEIZUNG_PWM_NACHKAT_BANK1_WERT | Lambdasondenheizung PWM hinter Katalysator Bank 1 | % | LSHPWM_DOWN[1] | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| ISBLS | 0x4A60 | STAT_BREMSLICHTSCHALTER_EIN_WERT | Bremslichtschalter Ein | 0/1 | LV_IM_BLS | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISBLT | 0x4A61 | STAT_BREMSLICHTTESTSCHALTER_EIN_WERT | Bremslichttestschalter Ein | 0/1 | LV_IM_BTS | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISOED | 0x4A62 | STAT_OELDRUCKSCHALTER_EIN_WERT | Öldruckschalter Ein | 0/1 | LV_POIL_SWI | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISAGK | 0x4A65 | STAT_ABGASKLAPPE_EIN_WERT | Abgasklappe Ein | 0/1 | LV_EF | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISDMP | 0x4A66 | STAT_DMTL_PUMPE_EIN_WERT | DMTL Pumpe Ein | 0/1 | LV_DMTL_PUMP | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISDMV | 0x4A67 | STAT_DMTL_VENTIL_EIN_WERT | DMTL Ventil Ein | 0/1 | LV_DMTLS | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISDMH | 0x4A68 | STAT_DMTL_HEIZUNG_EIN_WERT | DMTL Heizung Ein | 0/1 | LV_HDMTL_ON | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISMIL | 0x4A69 | STAT_MIL_EIN_WERT | MIL Lampe Ein | 0/1 | LV_MIL_CAN | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| ISCEL | 0x4A6B | STAT_CHECK_ENGINE_LAMPE_EIN_WERT | Lampe Check Engine Ein | 0/1 | LV_WAL_1_CAN | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x4A6C_WERT | 0x4A6C | STAT_0X4A6C_WERT | Verbrauchskorrekturfaktor | - | FAC_FCO_KWP | - | signed char | - | 0.001 | 1.0 | 0.0 | - | 22;2C | - | - |
| ISTFG | 0x4A6D | STAT_TASTE_FGR_EIN_WERT | Status Taste FGR | 0-n | STATE_MSW_CAN | - | unsigned char | _CNV_S_8_RANGE_STAT_145 | - | - | - | - | 22;2C | - | - |
| IAKFT | 0x4A74 | STAT_BEHEIZTER_THERMOSTAT_PWM_WERT | Beheizter Thermostat PWM | % | ECTPWM | - | unsigned int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| IATEV | 0x4A77 | STAT_TEV_PWM_WERT | Tankentlüftungsventil TEV PWM | % | CPPWM_CPS | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| IAELUE | 0x4A79 | STAT_E_LUEFTER_PWM_WERT | E-Lüfter PWM | % | ECFPWM[0] | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| IAVEP | 0x4A7A | STAT_VANOS_EINLASS_PWM_WERT | VANOS PWM Wert Einlass | % | IVVTPWM_IN[0] | - | unsigned int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| IAVAP | 0x4A7B | STAT_VANOS_AUSLASS_PWM_WERT | VANOS PWM Wert Auslass | % | IVVTPWM_EX[0] | - | unsigned int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A7C_WERT | 0x4A7C | STAT_0X4A7C_WERT | Lüfterfehler mit Funktionseinschränkungen | 0/1 | lv_err_ecfpwm_fb_3 | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x4A7D_WERT | 0x4A7D | STAT_0X4A7D_WERT | Schwerwiegender Lüfterfehler | 0/1 | lv_err_ecfpwm_fb_4 | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| IINT1 | 0x4A81 | STAT_INTEGRATOR_BANK1_WERT | Integrator Bank 1 | % | FAC_LAM_LIM[1] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| IINT2 | 0x4A82 | STAT_INTEGRATOR_BANK2_WERT | Integrator Bank 2 | % | FAC_LAM_LIM[2] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| IMUL1 | 0x4A85 | STAT_ADAPTION_MULTIPLIKATIV_BANK1_WERT | Adaption Multiplikation Lambda Bank 1 | % | FAC_LAM_AD_CUS[1] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| IMUL2 | 0x4A86 | STAT_ADAPTION_MULTIPLIKATIV_BANK2_WERT | Adaption Multiplikation Lambda Bank 2 | % | FAC_LAM_AD_CUS[2] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A87_WERT | 0x4A87 | STAT_0X4A87_WERT | Adaptionswert Trimregelung Bank 1 | - | LAMB_DELTA_AD_LAM_ADJ[1] | - | signed int | - | 0.00006104 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A88_WERT | 0x4A88 | STAT_0X4A88_WERT | Adaptionswert Trimregelung Bank 2 | - | LAMB_DELTA_AD_LAM_ADJ[2] | - | signed int | - | 0.00006104 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A89_WERT | 0x4A89 | STAT_0X4A89_WERT | multiplikative Gemischadaption hohe Last Bank 1 | % | FAC_H_RNG_LAM_AD[1] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A8A_WERT | 0x4A8A | STAT_0X4A8A_WERT | multiplikative Gemischadaption hohe Last Bank 2 | % | FAC_H_RNG_LAM_AD[2] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A8B_WERT | 0x4A8B | STAT_0X4A8B_WERT | multiplikative Gemischadaption niedrige Last Bank 1 | % | FAC_L_RNG_LAM_AD[1] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A8C_WERT | 0x4A8C | STAT_0X4A8C_WERT | multiplikative Gemischadaption niedrige Last Bank 2 | % | FAC_L_RNG_LAM_AD[2] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A8D_WERT | 0x4A8D | STAT_0X4A8D_WERT | additive Gemischadaption Leerlauf Bank 1 | mg/stroke | MFF_ADD_LAM_AD[1] | - | signed int | - | 0.02119478 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A8E_WERT | 0x4A8E | STAT_0X4A8E_WERT | additive Gemischadaption Leerlauf Bank 2 | mg/stroke | MFF_ADD_LAM_AD[2] | - | signed int | - | 0.02119478 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A8F_WERT | 0x4A8F | STAT_0X4A8F_WERT | Adaption Schubabgleich Bank 1 | - | FAC_LSL_GAIN_AD[1] | - | unsigned int | - | 0.00003052 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A90_WERT | 0x4A90 | STAT_0X4A90_WERT | Adaption Schubabgleich Bank 2 | - | FAC_LSL_GAIN_AD[2] | - | unsigned int | - | 0.00003052 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A91_WERT | 0x4A91 | STAT_0X4A91_WERT | Katalysatordiagnosewert Bank1 | - | EFF_CAT_DIAG_OBD[1] | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4A92_WERT | 0x4A92 | STAT_0X4A92_WERT | Katalysatordiagnosewert Bank2 | - | EFF_CAT_DIAG_OBD[2] | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 | - | 22;2C | - | - |
| SANWA | 0x4A94 | STAT_NW_AUSLASS_SOLL_WERT | Nockenwelle Auslass Sollwert | ° KW | CAM_SP_IVVT_EX | - | signed int | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| IANWA | 0x4A95 | STAT_NW_ADAPTION_AUSLASS_WERT | Adaptionswert Nockenwelle Auslass Bank 1 | ° KW | PSN_AD_CAM_EX_1 | - | unsigned char | - | 0.375 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| IANWE | 0x4A96 | STAT_NW_ADAPTION_EINLASS_WERT | Adaptionswert Nockenwelle Einlass Bank 1 | ° KW | PSN_AD_CAM_IN_1 | - | unsigned char | - | 0.375 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| STAT_0x4A97_WERT | 0x4A97 | STAT_0X4A97_WERT | Bedingung EVANOS im Anschlag beim letzten Abstellen | 0/1 | B_VSEAN_LOC | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| IAKWF | 0x4A99 | STAT_KURBELWELLEN_ADAPTION_BEENDET_WERT | Kurbelwellen Adaption beendet | 0/1 | LV_SEG_AD_AVL_ER | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x4AA1_WERT | 0x4AA1 | STAT_0X4AA1_WERT | Angefordertes PWM-Signal, E-Lüfter | % | ECFPWM_REQ | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AA2_WERT | 0x4AA2 | STAT_0X4AA2_WERT | ECF Relais aktivieren | 0/1 | LV_ECF_RLY_ACT | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x4AA7_WERT | 0x4AA7 | STAT_0X4AA7_WERT | Leckluftadaption Istwert | kg/h | MSNLGOFS_TMP | - | signed int | - | 0.03125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AAB_WERT | 0x4AAB | STAT_0X4AAB_WERT | Wastegate 1 PWM | % | WGPWM[1] | - | unsigned int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AAD_WERT | 0x4AAD | STAT_0X4AAD_WERT | Vorsteuerung Ladedruckregelung | % | ATLVST | - | unsigned int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AAE_WERT | 0x4AAE | STAT_0X4AAE_WERT | Reglerausgang und Vorsteuerung | % | ATLR | - | unsigned int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AAF_WERT | 0x4AAF | STAT_0X4AAF_WERT | Adaptionswert von der Ladedruckregelung | - | F_ATLAD | - | unsigned int | - | 0.00003052 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AB0_WERT | 0x4AB0 | STAT_0X4AB0_WERT | Solladedruck | hPa | PLDR_SOLL | - | unsigned int | - | 0.125 | 1.0 | 0.0 | - | 22;2C | - | - |
| IVKMH | 0x4AB1 | STAT_GESCHWINDIGKEIT_WERT | Geschwindigkeit | km/h | VS | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AB3_WERT | 0x4AB3 | STAT_FAHRSTRECKE_MIL_AN_WERT | Fahrstrecke mit MIL an | km | DIST_ACT_MIL | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZBST | 0x4AB4 | STAT_BETRIEBSSTUNDENZAEHLER_WERT | Betriebsstundenzähler | h | TRT | - | unsigned long | - | 0.00002778 | 1.0 | 0.0 | - | 22;2C | - | - |
| RTANS | 0x4AB6 | STAT_ANSAUGLUFTTEMPERATUR1_ROH_WERT | Rohwert Ansauglufttemperatur | °C | TIA_MES[1] | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| RTKWA | 0x4AB7 | STAT_KUEHLWASSERTEMPERATUR_ROH_WERT | Rohwert Kühlwassertemperatur | °C | TCO_MES | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| IUSAU | 0x4AB8 | STAT_SAUGROHRDRUCK_SPANNUNG_WERT | Spannung Saugrohrdruck | V | V_MAP[1] | - | unsigned int | - | 0.00488281 | 1.0 | 0.0 | - | 22;2C | - | - |
| IAKSP | 0x4ABA | STAT_KRAFTSTOFFPUMPE_PWM_WERT | PWM Kraftstoffpumpe | % | EFPPWM | - | unsigned int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| IMLUF | 0x4ABC | STAT_LUFTMASSE_WERT | Luftmasse | kg/h | MAF_KGH_MES_BAS[1] | - | unsigned int | - | 0.03125 | 1.0 | 0.0 | - | 22;2C | - | - |
| IASRE | 0x4ABD | STAT_STARTRELAIS_AKTIV_WERT | Starterrelais aktiv | 0/1 | LV_RLY_ST | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x4ABE_WERT | 0x4ABE | STAT_0X4ABE_WERT | I-Anteil Kraftstoffpumpe, PWM | % | EFPPWM_I | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AC2_WERT | 0x4AC2 | STAT_0X4AC2_WERT | Reset Adresse | - | STACK_ADR_RST[0][0] | - | unsigned long | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AC4_WERT | 0x4AC4 | STAT_0X4AC4_WERT | Minimale Pumpengeschwindigkeit der elektrischen Kraftsoffpumpe | % | EFPPWM_MIN_AD | - | unsigned int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AC5_WERT | 0x4AC5 | STAT_0X4AC5_WERT | Aditiver I-Anteil des EKP-Controllers | % | EFPPWM_I_AD | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4ACC_WERT | 0x4ACC | STAT_0X4ACC_WERT | Sollposition obere Luftklappe in Verstellschritten | - | CTR_ECRAS_UP_SP | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4ACD_WERT | 0x4ACD | STAT_0X4ACD_WERT | Istposition obere Luftklappe in Verstellschritten | - | CTR_ECRAS_UP_LST | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AD0_WERT | 0x4AD0 | STAT_0X4AD0_WERT | Fehlerstatus obere Luftklappe | - | STATE_ECRAS_UP_ERR | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AD1_WERT | 0x4AD1 | STAT_0X4AD1_WERT | Diagnosestatus obere Luftklappe | - | STATE_ECRAS_UP_DIAG_END | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AD2_WERT | 0x4AD2 | STAT_0X4AD2_WERT | Status obere Luftklappe | - | STATE_ECRAS_DOWN | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AE2_WERT | 0x4AE2 | STAT_0X4AE2_WERT | Resetart des letzten Resets | 0-n | STATE_RST_TYP_ACT | - | unsigned char | _CNV_S_19_ECOP_RANGE_764 | - | - | - | - | 22;2C | - | - |
| STAT_0x4AE3_WERT | 0x4AE3 | STAT_0X4AE3_WERT | Hintegrundinformationen zum letzten gültigen Reset | 0/1 | LV_DBG_INFO_VLD[0] | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x4AE4_WERT | 0x4AE4 | STAT_0X4AE4_WERT | Zusätzliche Resetinformationen zur Resetursache | - | STATE_RST_INFO_ADD[0] | - | unsigned long | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4AEA_WERT | 0x4AEA | STAT_0X4AEA_WERT | Anzahl von atypischen Warm-Resets seit letzter Power-Up-Phase (BSW) | - | CTR_WRST | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B00_WERT | 0x4B00 | STAT_0X4B00_WERT | Einspritzzeit Zylinder 1(Slave 7) von der Endstufe rückgemessen | ms | TI_1_MES[0] | - | unsigned int | - | 0.001 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B01_WERT | 0x4B01 | STAT_0X4B01_WERT | Einspritzzeit Zylinder 2 (Slave 8) von der Endstufe rückgemessen | ms | TI_1_MES[4] | - | unsigned int | - | 0.001 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B02_WERT | 0x4B02 | STAT_0X4B02_WERT | Einspritzzeit Zylinder 3 (Slave 9) von der Endstufe rückgemessen | ms | TI_1_MES[2] | - | unsigned int | - | 0.001 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B03_WERT | 0x4B03 | STAT_0X4B03_WERT | Einspritzzeit Zylinder 4 (Slave 10) von der Endstufe rückgemessen | ms | TI_1_MES[5] | - | unsigned int | - | 0.001 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B04_WERT | 0x4B04 | STAT_0X4B04_WERT | Einspritzzeit Zylinder 5 (Slave 11) von der Endstufe rückgemessen | ms | TI_1_MES[1] | - | unsigned int | - | 0.001 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B05_WERT | 0x4B05 | STAT_0X4B05_WERT | Einspritzzeit Zylinder 6 (Slave 12) von der Endstufe rückgemessen | ms | TI_1_MES[3] | - | unsigned int | - | 0.001 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B10_WERT | 0x4B10 | STAT_0X4B10_WERT | Tastverhältnis Injektor 1 (Slave 7) an Endstufe | % | EGY_STEP_INJ_CHA_GRD[0] | - | unsigned int | - | 0.00610352 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B11_WERT | 0x4B11 | STAT_0X4B11_WERT | Tastverhältnis Injektor 2 (Slave 8) an Endstufe | % | EGY_STEP_INJ_CHA_GRD[4] | - | unsigned int | - | 0.00610352 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B12_WERT | 0x4B12 | STAT_0X4B12_WERT | Tastverhältnis Injektor 3 (Slave9) an Endstufe | % | EGY_STEP_INJ_CHA_GRD[2] | - | unsigned int | - | 0.00610352 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B13_WERT | 0x4B13 | STAT_0X4B13_WERT | Tastverhältnis Injektor 4 (Slave 10) an Endstufe | % | EGY_STEP_INJ_CHA_GRD[5] | - | unsigned int | - | 0.00610352 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B14_WERT | 0x4B14 | STAT_0X4B14_WERT | Tastverhältnis Injektor 5 (Slave 11) an Endstufe | % | EGY_STEP_INJ_CHA_GRD[1] | - | unsigned int | - | 0.00610352 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B15_WERT | 0x4B15 | STAT_0X4B15_WERT | Tastverhältnis Injektor 6 (Slave 12) an Endstufe | % | EGY_STEP_INJ_CHA_GRD[3] | - | unsigned int | - | 0.00610352 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B20_WERT | 0x4B20 | STAT_0X4B20_WERT | Elektrische Ladung Injektor 1 (Slave 7) | µAs | CHA_IV_1_MES[0] | - | unsigned int | - | 2.22160006 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B21_WERT | 0x4B21 | STAT_0X4B21_WERT | Elektrische Ladung Injektor 2 (Slave 8) | µAs | CHA_IV_1_MES[4] | - | unsigned int | - | 2.22160006 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B22_WERT | 0x4B22 | STAT_0X4B22_WERT | Elektrische Ladung Injektor 3 (Slave 9) | µAs | CHA_IV_1_MES[2] | - | unsigned int | - | 2.22160006 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B23_WERT | 0x4B23 | STAT_0X4B23_WERT | Elektrische Ladung Injektor 4 (Slave 10) | µAs | CHA_IV_1_MES[5] | - | unsigned int | - | 2.22160006 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B24_WERT | 0x4B24 | STAT_0X4B24_WERT | Elektrische Ladung Injektor 5 (Slave 11) | µAs | CHA_IV_1_MES[1] | - | unsigned int | - | 2.22160006 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B25_WERT | 0x4B25 | STAT_0X4B25_WERT | Elektrische Ladung Injektor 6 (Slave 12) | µAs | CHA_IV_1_MES[3] | - | unsigned int | - | 2.22160006 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B30_WERT | 0x4B30 | STAT_0X4B30_WERT | Spannung Injektor 1 (Slave 7) | V | V_IV_1_MES[0] | - | unsigned int | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B31_WERT | 0x4B31 | STAT_0X4B31_WERT | Spannung Injektor 2 (Slave 8) | V | V_IV_1_MES[4] | - | unsigned int | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B32_WERT | 0x4B32 | STAT_0X4B32_WERT | Spannung Injektor 3 (Slave 9) | V | V_IV_1_MES[2] | - | unsigned int | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B33_WERT | 0x4B33 | STAT_0X4B33_WERT | Spannung Injektor 4 (Slave 10) | V | V_IV_1_MES[5] | - | unsigned int | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B34_WERT | 0x4B34 | STAT_0X4B34_WERT | Spannung Injektor 5 (Slave 11) | V | V_IV_1_MES[1] | - | unsigned int | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B35_WERT | 0x4B35 | STAT_0X4B35_WERT | Spannung Injektor 6 (Slave 12) | V | V_IV_1_MES[3] | - | unsigned int | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B40_WERT | 0x4B40 | STAT_0X4B40_WERT | Adaptionswert der Enstufe Injektor 1 (Slave 7) | %/mJ | FAC_EGY_PWM_AD[0] | - | unsigned int | - | 0.00003052 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B41_WERT | 0x4B41 | STAT_0X4B41_WERT | Adaptionswert der Enstufe Injektor 2 (Slave 8) | %/mJ | FAC_EGY_PWM_AD[4] | - | unsigned int | - | 0.00003052 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B42_WERT | 0x4B42 | STAT_0X4B42_WERT | Adaptionswert der Enstufe Injektor 3 (Slave 9) | %/mJ | FAC_EGY_PWM_AD[2] | - | unsigned int | - | 0.00003052 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B43_WERT | 0x4B43 | STAT_0X4B43_WERT | Adaptionswert der Enstufe Injektor 4 (Slave 10) | %/mJ | FAC_EGY_PWM_AD[5] | - | unsigned int | - | 0.00003052 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B44_WERT | 0x4B44 | STAT_0X4B44_WERT | Adaptionswert der Enstufe Injektor 5 (Slave 11) | %/mJ | FAC_EGY_PWM_AD[1] | - | unsigned int | - | 0.00003052 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4B45_WERT | 0x4B45 | STAT_0X4B45_WERT | Adaptionswert der Enstufe Injektor 6 (Slave 12) | %/mJ | FAC_EGY_PWM_AD[3] | - | unsigned int | - | 0.00003052 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4BBE_WERT | 0x4BBE | STAT_0X4BBE_WERT | Plausibilität Injektorcodierung Energieabgleich | - | LF_ERR_PLAUS_IV_EGY_CAL | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4BBF_WERT | 0x4BBF | STAT_0X4BBF_WERT | Plausibilität Injektorcodierung Durchflussabgleich | - | LF_ERR_PLAUS_IV_MFF_CAL | - | unsigned int | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4BCA_WERT | 0x4BCA | STAT_0X4BCA_WERT | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt A | % | FAC_LAM_TCO_A[1] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4BCB_WERT | 0x4BCB | STAT_0X4BCB_WERT | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt A | % | FAC_LAM_TCO_A[2] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4BCC_WERT | 0x4BCC | STAT_0X4BCC_WERT | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt B | % | FAC_LAM_TCO_B[1] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4BCD_WERT | 0x4BCD | STAT_0X4BCD_WERT | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt B | % | FAC_LAM_TCO_B[2] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4BCE_WERT | 0x4BCE | STAT_0X4BCE_WERT | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt C | % | FAC_LAM_TCO_C[1] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4BCF_WERT | 0x4BCF | STAT_0X4BCF_WERT | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt C | % | FAC_LAM_TCO_C[2] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4BD0_WERT | 0x4BD0 | STAT_0X4BD0_WERT | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt D | % | FAC_LAM_TCO_D[1] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4BD1_WERT | 0x4BD1 | STAT_0X4BD1_WERT | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt D | % | FAC_LAM_TCO_D[2] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4BD2_WERT | 0x4BD2 | STAT_0X4BD2_WERT | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt E | % | FAC_LAM_TCO_E[1] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x4BD3_WERT | 0x4BD3 | STAT_0X4BD3_WERT | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt E | % | FAC_LAM_TCO_E[2] | - | signed int | - | 0.00152588 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5800_WERT | 0x5800 | STAT_0X5800_WERT | Zeit nach Start | s | T_AST_SAE_KWP | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5801_WERT | 0x5801 | STAT_0X5801_WERT | Umgebungsdruck | kPa | OBD_AMP | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| ICLR1 | 0x5802 | STAT_LAMBDAREGELUNG_ZUSTAND_BANK1_WERT | Zustand Lambdaregelung Bank 1 | 0-n | STATE_LS[1] | - | unsigned char | _CNV_S_5_LACO_RANGE_300 | - | - | - | - | 22;2C | - | - |
| ICLR2 | 0x5803 | STAT_LAMBDAREGELUNG_ZUSTAND_BANK2_WERT | Zustand Lambdaregelung Bank 2 | 0-n | STATE_LS[2] | - | unsigned char | _CNV_S_5_LACO_RANGE_300 | - | - | - | - | 22;2C | - | - |
| SLAST | 0x5804 | STAT_LASTWERT_BERECHNET_WERT | Berechneter Lastwert | % | LOAD_CLC | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5805_WERT | 0x5805 | STAT_0X5805_WERT | Kühlmitteltemperatur OBD | °C | OBD_TCO | - | unsigned char | - | 1.0 | 1.0 | -40.0 | - | 22;2C | - | - |
| ILIN1 | 0x5806 | STAT_LAMBDA_INTEGRATOR_GRUPPE1_WERT | Lambda Integrator Gruppe 1 | % | OBD_LAM_COR[1] | - | unsigned char | - | 0.78125 | 1.0 | -100.00000224 | - | 22;2C | - | - |
| ILAM1 | 0x5807 | STAT_LAMBDA_ADAPTION_MULTIPLIKATIV_GRUPPE1_WERT | Lambda Adaption Summe mul. und add. Gruppe 1 | % | OBD_LAM_AD[1] | - | unsigned char | - | 0.78125 | 1.0 | -100.00000224 | - | 22;2C | - | - |
| ILIN2 | 0x5808 | STAT_LAMBDA_INTEGRATOR_GRUPPE2_WERT | Lambda Integrator Gruppe 2 | % | OBD_LAM_COR[2] | - | unsigned char | - | 0.78125 | 1.0 | -100.00000224 | - | 22;2C | - | - |
| ILAM2 | 0x5809 | STAT_LAMBDA_ADAPTION_MULTIPLIKATIV_GRUPPE2_WERT | Lambda Adaption Summe mul. und add. Gruppe 2 | % | OBD_LAM_AD[2] | - | unsigned char | - | 0.78125 | 1.0 | -100.00000224 | - | 22;2C | - | - |
| IPSA2 | 0x580B | STAT_SAUGROHRDRUCK_2_WERT | Saugrohrdruck | kPa | MAP_SAE | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| INAUF | 0x580C | STAT_N_AUFLOESUNG_WERT | Drehzahl | 1/min | OBD_N_H | - | unsigned char | - | 64.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IVKM2 | 0x580D | STAT_GESCHWINDIGKEIT_2_WERT | Geschwindigkeit | km/h | VS | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZZY1 | 0x580E | STAT_ZUENDZEITPUNKT_ZYL1_WERT | Zündzeitpunkt Zylinder 1 | ° KW | OBD_IGA_IGC | - | unsigned char | - | 0.5 | 1.0 | -64.0 | - | 22;2C | - | - |
| ITANL | 0x580F | STAT_ANSAUGLUFTTEMPERATUR_LOW_WERT | Ansauglufttemperatur | °C | OBD_TIA | - | unsigned char | - | 1.0 | 1.0 | -40.0 | - | 22;2C | - | - |
| ILMGS | 0x5810 | STAT_LUFTMASSE_GRAMM_PRO_SEKUNDE_WERT | Luftdurchsatz OBD | g/s | OBD_MAF_H | - | unsigned char | - | 2.55999994 | 1.0 | 0.0 | - | 22;2C | - | - |
| INM32 | 0x5811 | STAT_MOTORDREHZAHL_N32_WERT | Motordrehzahl | 1/min | N_32 | - | unsigned char | - | 32.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5812_WERT | 0x5812 | STAT_0X5812_WERT | Luftmasse gemessen | kg/h | MAF_KGH_MES_BAS_KWP[1] | - | unsigned char | - | 8.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILREL | 0x5813 | STAT_LASTWERT_RELATIV_WERT | Relative Last | % | RF_KWP | - | signed char | - | 2.55999994 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5814_WERT | 0x5814 | STAT_0X5814_WERT | Fahrpedalwert | % | PV_AV_RAW | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5815_WERT | 0x5815 | STAT_0X5815_WERT | Batteriespannung | V | OBD_VB_H | - | unsigned char | - | 0.25600001 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5816_WERT | 0x5816 | STAT_0X5816_WERT | Lambda Setpoint | - | OBD_LAMB_SP_H | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5817_WERT | 0x5817 | STAT_0X5817_WERT | Umgebungstemperatur | °C | OBD_TAM | - | unsigned char | - | 1.0 | 1.0 | -40.0 | - | 22;2C | - | - |
| ILMMG | 0x5818 | STAT_LUFTMASSE_PRO_HUB_WERT | Luftmasse gerechnet | mg/stroke | MAF_KWP | - | unsigned char | - | 5.44705868 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5819_WERT | 0x5819 | STAT_0X5819_WERT | Drehzahl OBD Byte | 1/min | N_SAE_BYTE_KWP | - | unsigned char | - | 64.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x581A_WERT | 0x581A | STAT_0X581A_WERT | Periodendauer Sensor Ansauglufttemperatur | µs | T_PER_TIA_PWM_BAS_KWP[0] | - | unsigned char | - | 256.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x581B_WERT | 0x581B | STAT_0X581B_WERT | Spannung Drucksensor | V | V_MAP_KWP[0] | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x581C_WERT | 0x581C | STAT_0X581C_WERT | Rohwert Lufttemperatur | °C | TIA_IM_MES[1] | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| STAT_0x581D_WERT | 0x581D | STAT_0X581D_WERT | Spannung Lufttemperatur | V | VP_TIA_IM_KWP[0] | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x581E_WERT | 0x581E | STAT_0X581E_WERT | Lufttemperatur Drosselklappe | °C | TIA_THR_MES[1] | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| STAT_0x581F_WERT | 0x581F | STAT_0X581F_WERT | Motortemperatur | °C | TCO_MES | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| STAT_0x5820_WERT | 0x5820 | STAT_0X5820_WERT | Kühlmitteltemperatur Kühlerausgang | °C | TCO_2_MES | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| STAT_0x5821_WERT | 0x5821 | STAT_0X5821_WERT | Steuergeräte-Innentemperatur | °C | TECU | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| STAT_0x5822_WERT | 0x5822 | STAT_0X5822_WERT | (Motor)-Öltemperatur | °C | TOIL_MES | - | unsigned char | - | 1.0 | 1.0 | -40.0 | - | 22;2C | - | - |
| IZMOS | 0x5823 | STAT_ZEIT_MOTOR_STEHT_WERT | Zeit Motor steht | min | T_ES_H | - | unsigned char | - | 256.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5824_WERT | 0x5824 | STAT_0X5824_WERT | Umgebungstemperatur | °C | TAM | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| STAT_0x5825_WERT | 0x5825 | STAT_0X5825_WERT | Abstellzeit | min | T_ES_CUS_KWP | - | unsigned char | - | 4.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5826_WERT | 0x5826 | STAT_0X5826_WERT | Drosselklappentemperatur | V | VP_TIA_THR_KWP[0] | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5827_WERT | 0x5827 | STAT_0X5827_WERT | Lambdasondenheizung vor Katalysator Bank 1 | % | LSHPWM_UP[1] | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5828_WERT | 0x5828 | STAT_0X5828_WERT | Lambdasondenheizung vor Katalysator Bank 2 | % | LSHPWM_UP[2] | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5829_WERT | 0x5829 | STAT_0X5829_WERT | Lambdasondenheizung hinter Katalysator Bank 1 | % | LSHPWM_DOWN[1] | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x582A_WERT | 0x582A | STAT_0X582A_WERT | Lambdasondenheizung hinter Katalysator Bank 2 | % | LSHPWM_DOWN[2] | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| IDRCA | 0x582B | STAT_DREHMOMENTEINGRIFF_CAN_WERT | Drehmomenteingriff über CAN | - | STATE_TQ_CAN_PLAUS | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x582C_WERT | 0x582C | STAT_0X582C_WERT | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 1 | - | CTR_ERR_LSL_IF_SPI_WR[1] | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x582D_WERT | 0x582D | STAT_0X582D_WERT | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 2 | - | CTR_ERR_LSL_IF_SPI_WR[2] | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x582E_WERT | 0x582E | STAT_0X582E_WERT | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 1 | - | FAC_DIAG_DYN_LSL_UP_KWP[1] | - | unsigned char | - | 0.00390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x582F_WERT | 0x582F | STAT_0X582F_WERT | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 2 | - | FAC_DIAG_DYN_LSL_UP_KWP[2] | - | unsigned char | - | 0.00390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5830_WERT | 0x5830 | STAT_0X5830_WERT | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 1 | - | FAC_MV_DIAG_DYN_LSL_UP_KWP[1] | - | unsigned char | - | 0.004 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5831_WERT | 0x5831 | STAT_0X5831_WERT | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 2 | - | FAC_MV_DIAG_DYN_LSL_UP_KWP[2] | - | unsigned char | - | 0.004 | 1.0 | 0.0 | - | 22;2C | - | - |
| IMOST | 0x5832 | STAT_MOTOR_STATUS_WERT | Motor Status | 0-n | STATE_ENG | - | unsigned char | _CNV_S_6_RANGE_STAT_56 | - | - | - | - | 22;2C | - | - |
| STAT_0x5833_WERT | 0x5833 | STAT_0X5833_WERT | Umgebungstemperatur beim Start | °C | TAM_ST | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| STAT_0x5834_WERT | 0x5834 | STAT_0X5834_WERT | Umgebungsdruck | hPa | AMP_MES_KWP | - | unsigned char | - | 5.30664063 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5835_WERT | 0x5835 | STAT_0X5835_WERT | Herstellercode Generator 1 | - | GEN_MANUFAK | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| INGRD | 0x5836 | STAT_DREHZAHLGRADIENT_WERT | Drehzahlgradient | 1/s | N_GRD | - | signed char | - | 32.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5837_WERT | 0x5837 | STAT_0X5837_WERT | Status OBD-I Fehler vor Katalysator Bank 1 | 0-n | STATE_ERR_EL_LSL_UP[1] | - | unsigned char | _CNV_S_11_EGCP_RANGE_249 | - | - | - | - | 22;2C | - | - |
| STAT_0x5838_WERT | 0x5838 | STAT_0X5838_WERT | Status OBD-I Fehler vor Katalysator Bank 2 | 0-n | STATE_ERR_EL_LSL_UP[2] | - | unsigned char | _CNV_S_11_EGCP_RANGE_249 | - | - | - | - | 22;2C | - | - |
| ISDKN | 0x5839 | STAT_DROSSELKLAPPE_NOTLAUF_WERT | Status Drosselklappe Notlauf | 0-n | STATE_N_LIM_ETC_REQ | - | unsigned char | _CNV_S_3_THRO_RANGE_891 | - | - | - | - | 22;2C | - | - |
| STAT_0x583A_WERT | 0x583A | STAT_0X583A_WERT | Ansauglufttemperatur beim Start | °C | TIA_ST | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| IKTFS | 0x583B | STAT_KRAFTSTOFFTANK_FUELLSTAND_WERT | Kraftstofftank Füllstand | l | FTL | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x583C_WERT | 0x583C | STAT_0X583C_WERT | Spannung Kl. 87 | V | VB | - | unsigned char | - | 0.10156249 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x583D_WERT | 0x583D | STAT_0X583D_WERT | Resettyp | 0-n | STATE_RST_TYP[0] | - | unsigned char | _CNV_S_19_ECOP_RANGE_764 | - | - | - | - | 22;2C | - | - |
| STAT_0x583E_WERT | 0x583E | STAT_0X583E_WERT | Motordrehzahl bei Reset | 1/min | N_RST_DET_KWP | - | unsigned char | - | 32.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x583F_WERT | 0x583F | STAT_0X583F_WERT | Drosselklappe Sollwert | ° DK | TPS_SP_KWP | - | unsigned char | - | 0.46682537 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5840_WERT | 0x5840 | STAT_0X5840_WERT | CPU Last bei Reset | % | CPU_LOAD_RST_DET_KWP | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| RTSGR | 0x5841 | STAT_STEUERGERAETE_INNENTEMPERATUR_ROH_WERT | SG-Innentemperatur Rohwert | V | VP_TECU_KWP | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5842_WERT | 0x5842 | STAT_0X5842_WERT | Kennung Generatortyp Generator 1 | - | GEN_TYPKENN | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5843_WERT | 0x5843 | STAT_0X5843_WERT | Versorgung FWG 1 | V | VCC_PVS_1_KWP | - | unsigned char | - | 0.0390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5844_WERT | 0x5844 | STAT_0X5844_WERT | Chiptemperatur Generator 1 | °C | TCHIP_KWP | - | unsigned char | - | 1.0 | 1.0 | -48.0 | - | 22;2C | - | - |
| STAT_0x5845_WERT | 0x5845 | STAT_0X5845_WERT | Spannung Lambdasonde vor Katalysator Bank 1 | V | VLS_UP_KWP[1] | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5846_WERT | 0x5846 | STAT_0X5846_WERT | Spannung Pedalwertgeber 1 | V | V_PVS_1_KWP | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5847_WERT | 0x5847 | STAT_0X5847_WERT | Spannung Pedalwertgeber 2 | V | V_PVS_2_KWP | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5848_WERT | 0x5848 | STAT_0X5848_WERT | Spannung Lambdasonde vor Katalysator Bank 2 | V | VLS_UP_KWP[2] | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5849_WERT | 0x5849 | STAT_0X5849_WERT | Spannung Lambdasonde hinter Katalysator Bank 1 | V | VLS_DOWN_KWP[1] | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| RUK15 | 0x584A | STAT_KL15_SPANNUNG_ROH_WERT | Spannung Kl. 15 Rohwert | V | V_IGK_BAS_KWP | - | unsigned char | - | 0.11294118 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x584B_WERT | 0x584B | STAT_0X584B_WERT | Spannung Lambdasonde hinter Katalysator Bank 2 | V | VLS_DOWN_KWP[2] | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| SQTEK | 0x584D | STAT_TANKENTLUEFTUNG_DURCHFLUSS_SOLL_WERT | korrigierter Sollwert Durchfluss Tankentlüftung | kg/h | FLOW_COR_CPS_KWP | - | unsigned char | - | 0.03125 | 1.0 | 0.0 | - | 22;2C | - | - |
| FS_P_GGDRUCK_OPF | 0x584F | STAT_P_GGDRUCK_FS_OPF_WERT | Höhe Gegendruck OPF  | hPa | DIP_PF_KWP_1 | - | unsigned char | - | 21.47483647 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5850_WERT | 0x5850 | STAT_0X5850_WERT | Spannung Motortemperatur | V | VP_TCO_KWP[1] | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5851_WERT | 0x5851 | STAT_0X5851_WERT | Spannung Ansauglufttemperatur, Sensor | V | VP_TIA_KWP | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5852_WERT | 0x5852 | STAT_0X5852_WERT | Kühlmitteltemperatur Kühlerausgang Rohwert | V | V_TCO_2_KWP | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5853_WERT | 0x5853 | STAT_0X5853_WERT | Spannung Kl.87 Rohwert | V | VB_BAS_KWP | - | unsigned char | - | 0.11294118 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5854_WERT | 0x5854 | STAT_0X5854_WERT | Versorgung FWG 2 | V | VCC_PVS_2_KWP | - | unsigned char | - | 0.0390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5855_WERT | 0x5855 | STAT_0X5855_WERT | Mittelwert Bank 1 | % | FAC_LAM_MV_MMV_KWP[1] | - | signed char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5856_WERT | 0x5856 | STAT_0X5856_WERT | Mittelwert Bank 2 | % | FAC_LAM_MV_MMV_KWP[2] | - | signed char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5857_WERT | 0x5857 | STAT_0X5857_WERT | Erregerstrom Generator 1 | A | IERR | - | unsigned char | - | 0.125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5858_WERT | 0x5858 | STAT_0X5858_WERT | Drosselklappe aktueller Wert | ° DK | TPS_AV_KWP | - | unsigned char | - | 0.46682537 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5859_WERT | 0x5859 | STAT_0X5859_WERT | DMTL Strom Referenzleck | mA | CUR_DMTL_REF_LEAK_KWP | - | unsigned char | - | 0.19531247 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x585A_WERT | 0x585A | STAT_0X585A_WERT | DMTL Strom Grobleck | mA | CUR_DMTL_ROUGH_LEAK_MIN_KWP | - | unsigned char | - | 0.19531247 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x585B_WERT | 0x585B | STAT_0X585B_WERT | DMTL Strom Diagnoseende | mA | CUR_DMTL_COR_FIL_KWP | - | unsigned char | - | 0.19531247 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x585C_WERT | 0x585C | STAT_0X585C_WERT | Widerstand Lambdasonde hinter Katalysator Bank 1 | Ohm | R_IT_LS_DOWN_KWP_H[1] | - | unsigned char | - | 256.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IRLN2 | 0x585D | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT2_WERT | Widerstand Lambdasonde hinter Katalysator Bank 2 | Ohm | R_IT_LS_DOWN_KWP_H[2] | - | unsigned char | - | 256.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IRUN1 | 0x585E | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT1_UNTERES_BYTE_WERT | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 1 | Ohm | R_IT_LS_DOWN_KWP_L[1] | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IRUN2 | 0x585F | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT2_UNTERES_BYTE_WERT | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 2 | Ohm | R_IT_LS_DOWN_KWP_L[2] | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IRLV1 | 0x5860 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT1_WERT | Widerstand Lambdasonde vor Katalysator Bank 1 | Ohm | R_IT_LS_UP_KWP_H[1] | - | unsigned char | - | 64.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IRLV2 | 0x5861 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT2_WERT | Widerstand Lambdasonde vor Katalysator Bank 2 | Ohm | R_IT_LS_UP_KWP_H[2] | - | unsigned char | - | 64.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| FS_ANTEIL_RUSS_OPF | 0x5862 | STAT_ANTEIL_RUSS_FS_OPF_WERT | Rußbeladung bei Leistungsbegrenzung OPF  | g | M_SOOT_PF_ACT_KWP | - | unsigned char | - | 1.0 | 64.00008031 | 0.0 | - | 22;2C | - | - |
| IRUV1 | 0x5863 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT1_UNTERES_BYTE_WERT | untere Byte Widerstand Lambdasonde vor Katalysator Bank 1 | Ohm | R_IT_LS_UP_KWP_L[1] | - | unsigned char | - | 0.25 | 1.0 | 0.0 | - | 22;2C | - | - |
| IRUV2 | 0x5864 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT2_UNTERES_BYTE_WERT | untere Byte Widerstand Lambdasonde vor Katalysator Bank 2 | Ohm | R_IT_LS_UP_KWP_L[2] | - | unsigned char | - | 0.25 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5865_WERT | 0x5865 | STAT_0X5865_WERT | Ölstand Mittelwert Langzeit | mm | OZ_NIVLANGT | - | unsigned char | - | 0.29296875 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5866_WERT | 0x5866 | STAT_0X5866_WERT | Füllstand Motoröl | - | OZ_LP | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5867_WERT | 0x5867 | STAT_0X5867_WERT | Kilometerstand | km | CTR_KM_CAN_KWP | - | unsigned char | - | 2560.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| ISSR2 | 0x5869 | STAT_STANDVERBRAUCHER_REGISTRIERT_TEIL2_WERT | Status Standverbraucher registriert Teil 2 | - | STAT_SV_REG2 | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x586A_WERT | 0x586A | STAT_0X586A_WERT | Batteriespannung von IBS gemessen | V | U_BATT_KWP | - | unsigned char | - | 0.064 | 1.0 | 6.016 | - | 22;2C | - | - |
| IZR82 | 0x586B | STAT_ZEIT_MIT_RUHESTROM_80_200_WERT | Zeit mit Ruhestrom 80 - 200 mA | min | T2HISTSHORT | - | unsigned char | - | 14.9333334 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZR21 | 0x586C | STAT_ZEIT_MIT_RUHESTROM_200_1000_WERT | Zeit mit Ruhestrom 200 - 1000 mA | min | T3HISTSHORT | - | unsigned char | - | 14.9333334 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZSST | 0x586D | STAT_ZAEHLER_ERKENNUNG_SCHLECHTE_STRASSE_WERT | Zähler Erkennung schlechte Strasse | - | SUM_RR | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZRG1 | 0x586E | STAT_ZEIT_MIT_RUHESTROM_GROESER_1000_WERT | Zeit mit Ruhestrom größer 1000 mA | min | T4HISTSHORT | - | unsigned char | - | 14.9333334 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5870_WERT | 0x5870 | STAT_0X5870_WERT | Spannung DME Umgebungsdruck | V | V_AMP_KWP | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| SLAG1 | 0x5871 | STAT_LAMBDA_SOLLWERT_GRUPPE1_WERT | Lambda-Sollwert Gruppe 1 | - | LAMB_SP_KWP[1] | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5872_WERT | 0x5872 | STAT_0X5872_WERT | Reglerversion Generator 1 | - | BSDGENREGV | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| SLAG2 | 0x5873 | STAT_LAMBDA_SOLLWERT_GRUPPE2_WERT | Lambda-Sollwert Gruppe 2 | - | LAMB_SP_KWP[2] | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5874_WERT | 0x5874 | STAT_0X5874_WERT | Spannung Strommessung DMTL | V | V_DMTL_KWP | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5875_WERT | 0x5875 | STAT_0X5875_WERT | Sollwert Motormoment | Nm | TQI_SP_KWP | - | unsigned char | - | 4.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5876_WERT | 0x5876 | STAT_0X5876_WERT | Raildruck OBD (High-Byte von FUP für OBD) | kPa | OBD_FUP_RNG_H_H | - | unsigned char | - | 2560.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5877_WERT | 0x5877 | STAT_0X5877_WERT | Raildruck OBD (Low-Byte von FUP für OBD) | kPa | OBD_FUP_RNG_H_L | - | unsigned char | - | 10.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILRR1 | 0x5878 | STAT_LAMBDAVERSCHIEBUNG_RUECKFUEHRREGLER1_WERT | Lambdaverschiebung Rückführregler 1 | - | LAMB_DELTA_I_LAM_ADJ_KWP[1] | - | signed char | - | 0.00097656 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILRR2 | 0x5879 | STAT_LAMBDAVERSCHIEBUNG_RUECKFUEHRREGLER2_WERT | Lambdaverschiebung Rückführregler 2 | - | LAMB_DELTA_I_LAM_ADJ_KWP[2] | - | signed char | - | 0.00097656 | 1.0 | 0.0 | - | 22;2C | - | - |
| ISFGR | 0x587A | STAT_FGR_WERT | Status FGR | - | STATE_CRU_BN | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x587B_WERT | 0x587B | STAT_0X587B_WERT | Gemessene Spannung vom DCDC Wandler gegen Masse | V | V_DCDC_LIN_LOW_KWP | - | unsigned char | - | 0.25 | 1.0 | 0.0 | - | 22;2C | - | - |
| ISMST | 0x587C | STAT_MOTORSTEUERUNG_WERT | Status Motorsteuerung | 0-n | ECU_STATE | - | unsigned char | _CNV_S_7_RANGE_ECU__54 | - | - | - | - | 22;2C | - | - |
| STAT_0x587D_WERT | 0x587D | STAT_0X587D_WERT | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 1 | 0-n | STATE_SYM_DIAG_PUC_LSL_UP[1] | - | unsigned char | _CNV_S_4_EGCP_RANGE_261 | - | - | - | - | 22;2C | - | - |
| STAT_0x587E_WERT | 0x587E | STAT_0X587E_WERT | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 2 | 0-n | STATE_SYM_DIAG_PUC_LSL_UP[2] | - | unsigned char | _CNV_S_4_EGCP_RANGE_261 | - | - | - | - | 22;2C | - | - |
| IELTV | 0x587F | STAT_E_LUEFTER_TASTVERHAELTNIS_WERT | Tastverhältnis E-Lüfter | % | ECFPWM[0] | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5880_WERT | 0x5880 | STAT_0X5880_WERT | Ansteuerung untere Luftklappe | 0/1 | LV_ECRAS_DOWN_1 | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| SBEGA | 0x5881 | STAT_BERECHNETER_GANG_WERT | berechneter Gang | - | GEAR | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| ITMOS | 0x5882 | STAT_MOTORTEMPERATUR_BEIM_START_WERT | Motortemperatur beim Start | °C | TCO_ST | - | unsigned char | - | 0.75 | 1.0 | -47.99999857 | - | 22;2C | - | - |
| STAT_0x5883_WERT | 0x5883 | STAT_0X5883_WERT | Spannung Klopfwerte Zylinder 1 | V | NL_KWP[0] | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5884_WERT | 0x5884 | STAT_0X5884_WERT | Rückgelesener Erregergrenzstrom Generator 1 | A | IERRFGRENZ | - | unsigned char | - | 0.125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5885_WERT | 0x5885 | STAT_0X5885_WERT | Spannung Klopfwerte Zylinder 3 | V | NL_KWP[2] | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5886_WERT | 0x5886 | STAT_0X5886_WERT | Spannung Klopfwerte Zylinder 6 | V | NL_KWP[3] | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5887_WERT | 0x5887 | STAT_0X5887_WERT | Auslastungsgrad Generator 1 | % | DFSIGGEN | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5888_WERT | 0x5888 | STAT_0X5888_WERT | Spannung Klopfwerte Zylinder 4 | V | NL_KWP[5] | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILAG1 | 0x5889 | STAT_LAMBDA_ISTWERT_GRUPPE1_WERT | Lambda-Istwert Gruppe 1 | - | LAMB_KWP[1] | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILAG2 | 0x588A | STAT_LAMBDA_ISTWERT_GRUPPE2_WERT | Lambda-Istwert Gruppe 2 | - | LAMB_KWP[2] | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZSSE | 0x588B | STAT_ZEIT_SEIT_STARTENDE_WERT | Zeit seit Startende | s | T_AST_SAE_H_KWP | - | unsigned char | - | 256.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| ITKV1 | 0x588C | STAT_LAMBDASONDE_KERAMIKTEMPERATUR_VORKAT1_WERT | Keramiktemperatur Lambdasonde vor Katalysator Bank 1 | °C | TTIP_MES_LS_UP_KWP[1] | - | signed char | - | 16.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZDML | 0x588D | STAT_ZEIT_DMTL_LECKMESSUNG_WERT | aktuelle Zeit DMTL Leckmessung | s | T_ACT_LEAK_MES_KWP | - | unsigned char | - | 25.60000038 | 1.0 | 0.0 | - | 22;2C | - | - |
| IIDMP | 0x588E | STAT_PUMPENSTROM_BEI_DMTL_PUMPENPRUEFUNG_WERT | Pumpenstrom bei DMTL Pumpenprüfung | mA | CUR_DMTL_DMTLS_TEST_KWP | - | unsigned char | - | 0.19531247 | 1.0 | 0.0 | - | 22;2C | - | - |
| ITKV2 | 0x588F | STAT_LAMBDASONDE_KERAMIKTEMPERATUR_VORKAT2_WERT | Keramiktemperatur Lambdasonde vor Katalysator Bank 2 | °C | TTIP_MES_LS_UP_KWP[2] | - | signed char | - | 16.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| FS_P_DRUCKSENS_OPF | 0x5890 | STAT_P_DRUCKSENS_FS_OPF_WERT | OPF Drucksensor Druck Master /Slave  | hPa | DIP_PF_KWP | - | unsigned char | - | 21.47483647 | 1.0 | 0.0 | - | 22;2C | - | - |
| IMOKU | 0x5891 | STAT_MOMENTANFORDERUNG_KUPPLUNG_WERT | Momentanforderung an der Kupplung | Nm | TQ_REQ_CLU_KWP | - | signed char | - | 8.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| FS_T_TEMPSENS_OPF | 0x5892 | STAT_TEMPSENS_FS_OPF__WERT | OPF Temperatursensor Temperaturistwert 1Master / 2Slave | °C | TEG_MES_KWP[0] | - | unsigned char | - | 16.0 | 1.0 | -273.15 | - | 22;2C | - | - |
| IDMGW | 0x5893 | STAT_DREHMOMENTABFALL_BEIM_GANGWECHSEL_WERT | Drehmomentabfall schnell bei Gangwechsel | Nm | TQI_GS_FAST_DEC_KWP | - | signed char | - | 8.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5894_WERT | 0x5894 | STAT_0X5894_WERT | Symptom Lambdasondenheizung vor Katalysator Bank 1 | 0-n | STATE_SYM_OBD_LSL_LSH_UP[1] | - | unsigned char | _CNV_S_4_EGCP_RANGE_253 | - | - | - | - | 22;2C | - | - |
| STAT_0x5895_WERT | 0x5895 | STAT_0X5895_WERT | Symptom Lambdasondenheizung vor Katalysator Bank 2 | 0-n | STATE_SYM_OBD_LSL_LSH_UP[2] | - | unsigned char | _CNV_S_4_EGCP_RANGE_253 | - | - | - | - | 22;2C | - | - |
| STAT_0x5896_WERT | 0x5896 | STAT_0X5896_WERT | Abgastemperatur hinter Katalysator Bank 1 | °C | TEG_CAT_DOWN_MDL_KWP[1] | - | signed char | - | 16.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5897_WERT | 0x5897 | STAT_0X5897_WERT | Abgastemperatur hinter Katalysator Bank 2 | °C | TEG_CAT_DOWN_MDL_KWP[2] | - | signed char | - | 16.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x5898_WERT | 0x5898 | STAT_GENERATOR_SPANNUNG_SOLL_WERT | Generator Sollspannung | V | V_ALTER_SP_KWP | - | unsigned char | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUOS1 | 0x589B | STAT_SPANNUNGSOFFSET_SIGNALPFAD1_WERT | Spannungsoffset Signalpfad CJ120 1 | V | VLS_OFS_LSL_KWP[1] | - | signed char | - | 0.00488278 | 1.0 | -0.00000361 | - | 22;2C | - | - |
| IUOS2 | 0x589C | STAT_SPANNUNGSOFFSET_SIGNALPFAD2_WERT | Spannungsoffset Signalpfad CJ120 2 | V | VLS_OFS_LSL_KWP[2] | - | signed char | - | 0.00488278 | 1.0 | -0.00000361 | - | 22;2C | - | - |
| STAT_0x589D_WERT | 0x589D | STAT_0X589D_WERT | Abweichung Lambdasonde zu Lambdamodellwert Überwachung | mg/stroke | MFF_TI_MON_KWP | - | unsigned char | - | 2.71050191 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x589F_WERT | 0x589F | STAT_0X589F_WERT | Motordrehzahl | 1/min | N_32 | - | unsigned char | - | 32.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58A0_WERT | 0x58A0 | STAT_0X58A0_WERT | Batterietemperatur | °C | T_BATT_KWP | - | signed char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58A1_WERT | 0x58A1 | STAT_0X58A1_WERT | Entladung während Ruhestromverletzung | Ah | Q_IRUHE2_KWP | - | unsigned char | - | 0.49803922 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58A2_WERT | 0x58A2 | STAT_0X58A2_WERT | Wasserpumpe Stromaufnahme | A | CUR_CNS_CWP_SEC | - | unsigned char | - | 0.2 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58A3_WERT | 0x58A3 | STAT_0X58A3_WERT | relative Wasserpumpenspannung | % | REL_CWP_PWR | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58A4_WERT | 0x58A4 | STAT_0X58A4_WERT | Status Generator | - | ST_GEN | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58A5_WERT | 0x58A5 | STAT_0X58A5_WERT | Generatorauslastung | % | DFFGEN | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58A6_WERT | 0x58A6 | STAT_0X58A6_WERT | Generatorspannung | V | U_GEN_KWP | - | unsigned char | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58A7_WERT | 0x58A7 | STAT_0X58A7_WERT | Abstellzeit in min | min | TN_ABSTELLM_KWP | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZMAB | 0x58A8 | STAT_MOTORABSTELLZEIT_WERT | Motorabstellzeit | min | T_ES_KWP | - | unsigned char | - | 4.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58A9_WERT | 0x58A9 | STAT_0X58A9_WERT | Resetzähler Rechnerüberwachung: alter Wert | - | ENVD_3_MON_3 | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58AA_WERT | 0x58AA | STAT_0X58AA_WERT | Fehlercode Rechnerüberwachung: alter Wert | - | ENVD_2_MON_3 | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58AB_WERT | 0x58AB | STAT_0X58AB_WERT | Abweichung DK-Potentiometer 1 und Modellwert | ° DK | TPS_DIF_DIAG_COR_1_KWP | - | unsigned char | - | 0.46682537 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58AC_WERT | 0x58AC | STAT_0X58AC_WERT | Abweichung DK-Potentiometer 2 und Modellwert | ° DK | TPS_DIF_DIAG_COR_2_KWP | - | unsigned char | - | 0.46682537 | 1.0 | 0.0 | - | 22;2C | - | - |
| IPWG1 | 0x58AD | STAT_PEDALWERTGEBER1_WERT | Pedalwertgeber 1 | % | PV_AV_1 | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58AE_WERT | 0x58AE | STAT_0X58AE_WERT | Periodendauer Luftmasse | µs | T_PER_MAF_FRQ_KWP | - | unsigned char | - | 32.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IKRAN | 0x58AF | STAT_KRAFTSTOFF_ANFORDERUNG_AN_PUMPE_WERT | Kraftstoff Anforderung an Pumpe | l/h | VFF_EFP | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IDKAD | 0x58B0 | STAT_DK_ADAPTIONSSCHRITT_WERT | DK-Adaptionsschritt | - | TPS_AD_STEP_KWP | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZFZ1 | 0x58B1 | STAT_FUNKENBRENNDAUER_ZYL1_WERT | Funkenbrenndauer Zylinder 1 (Slave 7) | ms | V_DUR_IGC_KWP[0] | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZFZ5 | 0x58B2 | STAT_FUNKENBRENNDAUER_ZYL5_WERT | Funkenbrenndauer Zylinder 5 (Slave 11) | ms | V_DUR_IGC_KWP[1] | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZFZ3 | 0x58B3 | STAT_FUNKENBRENNDAUER_ZYL3_WERT | Funkenbrenndauer Zylinder 3 (Slave 9) | ms | V_DUR_IGC_KWP[2] | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZFZ6 | 0x58B4 | STAT_FUNKENBRENNDAUER_ZYL6_WERT | Funkenbrenndauer Zylinder 6 (Slave 12) | ms | V_DUR_IGC_KWP[3] | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZFZ2 | 0x58B5 | STAT_FUNKENBRENNDAUER_ZYL2_WERT | Funkenbrenndauer Zylinder 2 (Slave 8) | ms | V_DUR_IGC_KWP[4] | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 | - | 22;2C | - | - |
| IZFZ4 | 0x58B6 | STAT_FUNKENBRENNDAUER_ZYL4_WERT | Funkenbrenndauer Zylinder 4 (Slave 10) | ms | V_DUR_IGC_KWP[5] | - | unsigned char | - | 1.02400005 | 1.0 | 0.0 | - | 22;2C | - | - |
| IPBRE | 0x58B7 | STAT_BREMSDRUCK_WERT | Bremsdruck | bar | BRAKE_PRS | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58B8_WERT | 0x58B8 | STAT_0X58B8_WERT | Drehzahl Überwachung | 1/min | N_32_MON | - | unsigned char | - | 32.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58B9_WERT | 0x58B9 | STAT_0X58B9_WERT | Pedalwert Überwachung | % | PV_AV_MON | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58BA_WERT | 0x58BA | STAT_0X58BA_WERT | eingespritze Kraftstoffmasse | l/h | VFF_MFF_SP_FUP_CTL_KWP | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58BB_WERT | 0x58BB | STAT_0X58BB_WERT | PWM Kraftstoffpumpe | % | EFPPWM_KWP | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58BC_WERT | 0x58BC | STAT_0X58BC_WERT | Luftmasse Überwachung | mg/stroke | MFF_MAF_MON_KWP | - | unsigned char | - | 2.71050191 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58BD_WERT | 0x58BD | STAT_0X58BD_WERT | Statusbyte externe Momentenanforderung 3 | - | STATE_LV_ERR_COM_MON_1_3 | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| FS_ANTEIL_ASCHE_OPF | 0x58BE | STAT_ANTEIL_ASCHE_FS_OPF_WERT | Aschebeladung bei Leistungsbegrenzung OPF  | g | M_ASH_LOAD_PF_KWP | - | unsigned char | - | 1.0 | 64.00008031 | 0.0 | - | 22;2C | - | - |
| STAT_0x58BF_WERT | 0x58BF | STAT_0X58BF_WERT | Statusbyte vom Error Memory Management | - | STATE_LV_ERR_COM_MON_1 | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58C0_WERT | 0x58C0 | STAT_0X58C0_WERT | Motordrehzahl Ersatzwert Überwachung | 1/min | N_32_SUB_MON | - | unsigned char | - | 32.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| ITLSZ | 0x58C1 | STAT_LAUFUNRUHE_SEGMENTZEIT_WERT | Laufunruhe Segmentzeit | µs | SEG_T_MES_KWP_H | - | unsigned char | - | 7812.21826172 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58C2_WERT | 0x58C2 | STAT_0X58C2_WERT | Statusbyte MFF-Monitoring | mg/stroke | MFF_SP_MV_KWP | - | unsigned char | - | 2.71050191 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58C3_WERT | 0x58C3 | STAT_0X58C3_WERT | Statusbyte ISC-Monitoring | - | STATE_LV_ERR_TQ_DIF_ISC_MON_1 | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58C4_WERT | 0x58C4 | STAT_0X58C4_WERT | Statusbyte CRU-Monitoring | - | STATE_LV_ERR_CRU_INH_MON_1 | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58C5_WERT | 0x58C5 | STAT_0X58C5_WERT | Drehzahl Überwachung (resetsicher) | 1/min | N_32_MON_SAVE | - | unsigned char | - | 32.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58C6_WERT | 0x58C6 | STAT_0X58C6_WERT | Status Einspritzventile (resetsicher) | - | PREV_STATE_IV_SAVE | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| INSUE | 0x58C7 | STAT_LEERLAUF_SOLLDREHZAHLABWEICHUNG_WERT | LL-Solldrehzahlabweichung Überwachung | 1/min | N_DIF_SP_IS_MON | - | signed char | - | 32.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58C8_WERT | 0x58C8 | STAT_0X58C8_WERT | I-Anteil Momentdifferenz Überwachung und Modell | Nm | TQ_DIF_I_IS_MON_KWP | - | signed char | - | 2.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58C9_WERT | 0x58C9 | STAT_0X58C9_WERT | I-Anteil LL passive Rampe aktiv | 0/1 | LV_PAS_RAMP_ACT_I_IS | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x58CA_WERT | 0x58CA | STAT_0X58CA_WERT | PD-Anteil langsam Leerlaufregelung | Nm | TQ_DIF_P_D_SLOW_IS_KWP | - | signed char | - | 8.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58CB_WERT | 0x58CB | STAT_0X58CB_WERT | PD-Anteil schnell Leerlaufregelung | Nm | TQ_DIF_P_D_FAST_IS_KWP | - | signed char | - | 8.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58CC_WERT | 0x58CC | STAT_0X58CC_WERT | Verlustmoment Überwachung | Nm | TQ_LOSS_MON_KWP | - | signed char | - | 8.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| FS_LEIST_BEG_OPF | 0x58CD | STAT_LEIST_BEG_FS_OPF_WERT | Grund für Leistungsbegrenzung von OPF  | - | LF_POW_LIM_PF_KWP | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58CE_WERT | 0x58CE | STAT_0X58CE_WERT | Carrierbyte Schalterstati | - | STATE_BYTE_SWI_KWP | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| SMOMO | 0x58CF | STAT_MOTORMOMENT_SOLL_WERT | Motormoment Sollwert Überwachung | Nm | TQI_SP_H_RNG_MON_KWP | - | unsigned char | - | 4.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IMOMO | 0x58D0 | STAT_MOTORMOMENT_IST_WERT | Motormoment Istwert Überwachung | Nm | TQI_AV_H_RNG_MON_KWP | - | unsigned char | - | 4.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IMOAK | 0x58D1 | STAT_MOTORMOMENT_AKTUELL_WERT | Moment aktueller Wert | Nm | TQI_AV_KWP | - | signed char | - | 8.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58D2_WERT | 0x58D2 | STAT_0X58D2_WERT | Sollposition obere Luftklappe in Grad | ° | ANG_ECRAS_UP_SP | - | unsigned char | - | 256.0 | 1.0 | -95.0 | - | 22;2C | - | - |
| STAT_0x58D3_WERT | 0x58D3 | STAT_0X58D3_WERT | Istposition obere Luftklappe in Grad | ° | ANG_ECRAS_UP | - | unsigned char | - | 256.0 | 1.0 | -95.0 | - | 22;2C | - | - |
| STAT_0x58D4_WERT | 0x58D4 | STAT_0X58D4_WERT | Abweichung maximales Moment an Kupplung Überwachung | Nm | TQ_MAX_CLU_DIF_MON_KWP | - | signed char | - | 8.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58D6_WERT | 0x58D6 | STAT_0X58D6_WERT | Abweichung minimales Moment an Kupplung Überwachung | Nm | TQ_MIN_CLU_DIF_MON_KWP | - | signed char | - | 8.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58D7_WERT | 0x58D7 | STAT_0X58D7_WERT | Spannung des Ansauglufttemperatursensors im Laderstrang | V | VP_TIA_TCHA_KWP | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58D9_WERT | 0x58D9 | STAT_0X58D9_WERT | Fehlercode Rechnerüberwachung: aktueller Wert | - | ENVD_0_MON_3 | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58DA_WERT | 0x58DA | STAT_0X58DA_WERT | Resetzähler Rechnerüberwachung: aktueller Wert | - | ENVD_1_MON_3 | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58DB_WERT | 0x58DB | STAT_0X58DB_WERT | Inhalt Statusbyte 1 Drehzahlüberwachung (resetsicher) | - | STATE_TQI_N_MAX_MON_1_1_SAVE | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58DC_WERT | 0x58DC | STAT_0X58DC_WERT | Inhalt Statusbyte 2 Drehzahlüberwachung (resetsicher) | - | STATE_TQI_N_MAX_MON_1_2_SAVE | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58DD_WERT | 0x58DD | STAT_0X58DD_WERT | ATL upstream | kPa | PUT_KWP[1] | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58DE_WERT | 0x58DE | STAT_0X58DE_WERT | Spannung für Drucksensor vor Drosselklappe | V | V_PUT_KWP[1] | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58E4_WERT | 0x58E4 | STAT_0X58E4_WERT | Betriebsart Istwert | 0-n | BA_IST | - | unsigned char | _CNV_S_5__CNV_S_5_D_608 | - | - | - | - | 22;2C | - | - |
| STAT_0x58E5_WERT | 0x58E5 | STAT_0X58E5_WERT | Lastwert für Aussetzererkennung | % | LOAD_MIS_KWP | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58E6_WERT | 0x58E6 | STAT_0X58E6_WERT | Nulllastwert für Aussetzererkennung | % | LOAD_MIN_MIS_KWP | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58E7_WERT | 0x58E7 | STAT_0X58E7_WERT | Spannung Pedalwertgeber 1 Überwachung | V | V_PVS_1_MON_KWP | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58E8_WERT | 0x58E8 | STAT_0X58E8_WERT | Spannung Pedalwertgeber 2 Überwachung | V | V_PVS_2_MON_KWP | - | unsigned char | - | 0.01953125 | 1.0 | 0.0 | - | 22;2C | - | - |
| IUWAP | 0x58E9 | STAT_WASSERPUMPE_SPANNUNG_WERT | Wasserpumpe Spannung | V | V_CWP_SEC | - | unsigned char | - | 0.1 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58EA_WERT | 0x58EA | STAT_0X58EA_WERT | Wasserpumpe Drehzahl | - | N_REL_CWP | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| INWSI | 0x58EB | STAT_WASSERPUMPE_DREHZAHL_SOLL_IST_DIFFERENZ_WERT | Wasserpumpe Drehzahl Soll-Ist-Differenz | - | N_REL_CWP_DIF | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58EC_WERT | 0x58EC | STAT_0X58EC_WERT | Wasserpumpe Temperatur Elektronik | °C | TEMP_EL_CWP_SEC | - | unsigned char | - | 1.0 | 1.0 | -50.0 | - | 22;2C | - | - |
| STAT_0x58ED_WERT | 0x58ED | STAT_0X58ED_WERT | gemittelter Raildruck Bank 1 | V | V_FUP_MV_0_KWP | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58EF_WERT | 0x58EF | STAT_0X58EF_WERT | Raildruck Bank 1 | hPa | FUP_KWP[1] | - | unsigned char | - | 1358.5177002 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58F0_WERT | 0x58F0 | STAT_0X58F0_WERT | Dummy für Fehlerspecherfehlbedatung | - | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| IDMEL | 0x58F1 | STAT_DME_LOSNUMMER_WERT | DME - Losnummer | 0-n | STATE_LRN_ECU_KWP | - | unsigned char | _CNV_S_13_RANGE_STAT_839 | - | - | - | - | 22;2C | - | - |
| STAT_0x58F2_WERT | 0x58F2 | STAT_0X58F2_WERT | PWM-Signal des Mengensteuerventils | % | PWM_VCV_KWP | - | unsigned char | - | 0.390625 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58F3_WERT | 0x58F3 | STAT_0X58F3_WERT | Kraftstoffdruck vor Mengensteuerventil | hPa | FUP_EFP_KWP | - | unsigned char | - | 42.45375824 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58F4_WERT | 0x58F4 | STAT_0X58F4_WERT | Spannung für Kraftstoffdrucksensor vor Mengensteuerventil | V | V_FUP_EFP_MV_KWP | - | unsigned char | - | 0.01953122 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58F5_WERT | 0x58F5 | STAT_0X58F5_WERT | Eingangssignal Rückführregler 1 | V | VLS_DIF_LAM_ADJ_KWP[1] | - | signed char | - | 0.00488278 | 1.0 | -0.00000361 | - | 22;2C | - | - |
| STAT_0x58F6_WERT | 0x58F6 | STAT_0X58F6_WERT | Eingangssignal Rückführregler 2 | V | VLS_DIF_LAM_ADJ_KWP[2] | - | signed char | - | 0.00488278 | 1.0 | -0.00000361 | - | 22;2C | - | - |
| STAT_0x58F7_WERT | 0x58F7 | STAT_0X58F7_WERT | Laufunruhe Segmentzeit | µs | SEG_T_MES_KWP_L | - | unsigned char | - | 30.51647758 | 1.0 | 0.0 | - | 22;2C | - | - |
| ILSA5 | 0x58F8 | STAT_LAUFUNRUHE_SEGMENTADAPTION_ZYL5_WERT | Segmentadaption Laufunruhe Zyl. 5 (Slave 11) | % | SEG_AD_MMV_ER_KWP[1] | - | signed char | - | 0.06103515 | 1.0 | 0.00000008 | - | 22;2C | - | - |
| ILSA3 | 0x58F9 | STAT_LAUFUNRUHE_SEGMENTADAPTION_ZYL3_WERT | Segmentadaption Laufunruhe Zyl. 3 (Slave 9) | % | SEG_AD_MMV_ER_KWP[2] | - | signed char | - | 0.06103515 | 1.0 | 0.00000008 | - | 22;2C | - | - |
| STAT_0x58FA_WERT | 0x58FA | STAT_0X58FA_WERT | Beladungsgrad Aktivkohlefilter TEV- Funktionstest | - | CL_MMV_SAE_KWP | - | unsigned char | - | 0.0078125 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58FB_WERT | 0x58FB | STAT_0X58FB_WERT | Zähler Drehzahlerhöhungen TEV- Funktionstest | cyc | SUM_DIAG_DIAGCPS_SAE | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58FC_WERT | 0x58FC | STAT_0X58FC_WERT | Katheizen aktiv | 0/1 | LV_WUP | - | unsigned char | - | - | - | - | - | 22;2C | - | - |
| STAT_0x58FD_WERT | 0x58FD | STAT_0X58FD_WERT | Statusbit STATE_LV_ERR_COM_MON_1_2 | - | STATE_LV_ERR_COM_MON_1_2 | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58FE_WERT | 0x58FE | STAT_0X58FE_WERT | Statusbyte externe Momentenanforderung | - | STATE_LV_ERR_TQ_EXT_MON_1 | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |
| STAT_0x58FF_WERT | 0x58FF | STAT_0X58FF_WERT | Umweltbedingung unbekannt | - | - | - | unsigned char | - | 1.0 | 1.0 | 0.0 | - | 22;2C | - | - |

<a id="table-status-genmanufak"></a>
### STATUS_GENMANUFAK

Dimensions: 8 rows × 2 columns

| NR | HERSTELLER |
| --- | --- |
| 0x00 | Hersteller: Bosch |
| 0x01 | Hersteller: Valeo |
| 0x02 | Hersteller: Denso/Delphi |
| 0x03 | Hersteller: Hitachi |
| 0x04 | Hersteller: Denso |
| 0x05 | Hersteller: Melco |
| 0x06 | Hersteller: Visteon |
| 0xFF | Hersteller: unbekannt |

<a id="table-status-gentypkenn"></a>
### STATUS_GENTYPKENN

Dimensions: 27 rows × 2 columns

| NR | TYP |
| --- | --- |
| 0x00 | Generatortyp: - |
| 0x01 | Generatortyp: C2.1 / SC1 |
| 0x02 | Generatortyp: C2.4 / SC2 |
| 0x03 | Generatortyp: TG23 / H3.1 / SC3 |
| 0x04 | Generatortyp: SG9 / LIF150 / SC4 |
| 0x05 | Generatortyp: SC5 |
| 0x06 | Generatortyp: M2.5 / SC6 |
| 0x07 | Generatortyp: CL8+ / EL7-150 |
| 0x08 | Generatortyp: SG12 / TG12 /LIF180 / EL7-150 HED |
| 0x09 | Generatortyp: C1.9 / EL7-175 |
| 0x0A | Generatortyp: M2.3 / EL7-175 HED |
| 0x0B | Generatortyp: H3.8 / EL8-180 |
| 0x0C | Generatortyp: E4 / SG11 / EL8-180 HED |
| 0x0D | Generatortyp: M3.0 / EL8-210 |
| 0x0E | Generatortyp: EL8-210 HED |
| 0x10 | Generatortyp: TG17 |
| 0x11 | Generatortyp: TG17 (mit Bosch) |
| 0x13 | Generatortyp: CL 12+ Prince |
| 0x14 | Generatortyp: E8 / SG14 / FG18D |
| 0x15 | Generatortyp: FG18 |
| 0x16 | Generatortyp: FG18D |
| 0x18 | Generatortyp: TG15 |
| 0x19 | Generatortyp: FG23 |
| 0x1A | Generatortyp: CG25 |
| 0x1C | Generatortyp: E8+ (mit BSD I) |
| 0x1F | Generatortyp: E8+ (mit BSD II) |
| 0xFF | Generatortyp: unbekannt |

<a id="table-statclientauthtxt"></a>
### STATCLIENTAUTHTXT

Dimensions: 4 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0x00 | Freigabe von Zuendung und Einspritzung (noch) nicht erteilt (noch nicht versucht oder Kommunikation gestört, Motorlauf gesperrt) |
| 0x01 | Freigabe von Zuendung und Einspritzung erteilt (Challenge-Response erfolgreich) |
| 0x02 | Freigabe von Zuendung und Einspritzung abgelehnt (Challenge-Response fehlgeschlagen, falsche Response, Kommunikation i.O.) |
| 0x03 | nicht definiert |

<a id="table-statewsvertxt"></a>
### STATEWSVERTXT

Dimensions: 3 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0x01 | Direktschreiben des SecretKey |
| 0x02 | Direktschreiben des SecretKey und DH-Abgleich |
| 0xXY | unbekannt |

<a id="table-statfreesktxt"></a>
### STATFREESKTXT

Dimensions: 3 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0xFE | Ablage unbegrenzt |
| 0xFF | ungültig |
| 0xXY | freie Ablagen |

<a id="table-table-status-batteriezustand"></a>
### TABLE_STATUS_BATTERIEZUSTAND

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Batterie i.O. |
| 1 | Batterie pruefen |
| 2 | Batterie nicht i.O. |
| 3 | ungueltig |

<a id="table-table-status-eco2-funktionsstati"></a>
### TABLE_STATUS_ECO2_FUNKTIONSSTATI

Dimensions: 11 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Funktion nicht gestartet |
| 2 | Stop-Routine erfolgreich abgearbeitet |
| 3 | Funktion wartet auf Freigabe |
| 4 | Parameter unplausibel |
| 5 | Warten auf Trigger |
| 6 | Trigger erkannt |
| 7 | Funktion abgebrochen, Motor läuft oder keine Rückmeldung vom IBS |
| 8 | Messung beendet |
| 9 | Funktion abgebrochen, Time Out erreicht |
| 10 | Messung beendet, Time Out erreicht |
| 255 | Ungültiger Wert |

<a id="table-table-status-ibs-bze"></a>
### TABLE_STATUS_IBS_BZE

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | BZE nicht aktiv |
| 1 | BZE aktiv |

<a id="table-table-status-letzter-batteriewechsel"></a>
### TABLE_STATUS_LETZTER_BATTERIEWECHSEL

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Wechsel zulässig |
| 1 | Wechsel unzulässig |

<a id="table-table-status-tiefentladung"></a>
### TABLE_STATUS_TIEFENTLADUNG

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Batterie i.O. |
| 1 | Batterie durch Tiefentladung geschädigt |

<a id="table-table-status-wasserverlust"></a>
### TABLE_STATUS_WASSERVERLUST

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Wasserverlust i.O. |
| 1 | Wasserverlust nicht i.O. |

<a id="table-cnv-s-11-egcp-range-247"></a>
### _CNV_S_11_EGCP_RANGE_247

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
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

<a id="table-cnv-s-11-egcp-range-249"></a>
### _CNV_S_11_EGCP_RANGE_249

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
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

<a id="table-cnv-s-12-cnv-s-12-655"></a>
### _CNV_S_12__CNV_S_12__655

Dimensions: 13 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine |
| 0x01 | WARMLAUF |
| 0x02 | ECO |
| 0x03 | NORMAL |
| 0x04 | HIGH |
| 0x05 | HIGH+KFT |
| 0x06 | BAUTEILSCHUTZ |
| 0x07 | HEIZLEISTUNG |
| 0x08 | NOTLAUF |
| 0x09 | APPLIKATION |
| 0x0A | Befuellen/Entlueften |
| 0x0B | Verbrennungsmotor steht |
| 0xFF | undefiniert |

<a id="table-cnv-s-12-cnv-s-12-656"></a>
### _CNV_S_12__CNV_S_12__656

Dimensions: 13 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Keine |
| 0x01 | WARMLAUF |
| 0x02 | ECO |
| 0x03 | NORMAL |
| 0x04 | HIGH |
| 0x05 | HIGH+KFT |
| 0x06 | BAUTEILSCHUTZ |
| 0x07 | HEIZLEISTUNG |
| 0x08 | NOTLAUF |
| 0x09 | APPLIKATION |
| 0x0A | Befuellen/Entlueften |
| 0x0B | Verbrennungsmotor steht |
| 0xFF | undefiniert |

<a id="table-cnv-s-13-range-stat-839"></a>
### _CNV_S_13_RANGE_STAT_839

Dimensions: 13 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ROM_NOT_PLAUS |
| 0x11 | LEARNING_FAILED |
| 0x3D | LOT8 |
| 0x5A | LOT1 |
| 0x79 | LOT5 |
| 0x97 | LOT9 |
| 0xA5 | LOT2 |
| 0xAE | LOT4 |
| 0xBC | SERIAL_ECU |
| 0xCB | LOT6 |
| 0xD3 | LOT7 |
| 0xEA | LOT3 |
| 0xFF | NOT LEARNED |

<a id="table-cnv-s-19-ecop-range-763"></a>
### _CNV_S_19_ECOP_RANGE_763

Dimensions: 20 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NO |
| 0x01 | DET_ERROR |
| 0x02 | DISABLED |
| 0x10 | PORST_UNINTENDED |
| 0x11 | PORST_CPL_FAIL |
| 0x12 | PORST_INTENDED |
| 0x13 | PORST_VDD_ERROR |
| 0x20 | EXTRST_UNINTENDED |
| 0x30 | WDTRST_UNINTENDED |
| 0x40 | LLRST_UNINTENDED |
| 0x50 | LCRST_UNINTENDED |
| 0x60 | CSRST_UNINTENDED |
| 0xA0 | SWRST_UNINTENDED |
| 0xA1 | SWRST_CPL_FAIL |
| 0xA2 | SWRST_INTENDED |
| 0xA3 | SWRST_VDD_ERROR |
| 0xA4 | SWRST_EXCEPTION |
| 0xA5 | SWRST_NMI |
| 0xA6 | SWRST_ERROR |
| 0xFF | undefiniert |

<a id="table-cnv-s-19-ecop-range-764"></a>
### _CNV_S_19_ECOP_RANGE_764

Dimensions: 20 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NO |
| 0x01 | DET_ERROR |
| 0x02 | DISABLED |
| 0x10 | PORST_UNINTENDED |
| 0x11 | PORST_CPL_FAIL |
| 0x12 | PORST_INTENDED |
| 0x13 | PORST_VDD_ERROR |
| 0x20 | EXTRST_UNINTENDED |
| 0x30 | WDTRST_UNINTENDED |
| 0x40 | LLRST_UNINTENDED |
| 0x50 | LCRST_UNINTENDED |
| 0x60 | CSRST_UNINTENDED |
| 0xA0 | SWRST_UNINTENDED |
| 0xA1 | SWRST_CPL_FAIL |
| 0xA2 | SWRST_INTENDED |
| 0xA3 | SWRST_VDD_ERROR |
| 0xA4 | SWRST_EXCEPTION |
| 0xA5 | SWRST_NMI |
| 0xA6 | SWRST_ERROR |
| 0xFF | undefiniert |

<a id="table-cnv-s-3-thro-range-890"></a>
### _CNV_S_3_THRO_RANGE_890

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | N_NOT_LIM |
| 0x01 | N_LIM_CON |
| 0x02 | N_LIM_PVS |
| 0xFF | undefiniert |

<a id="table-cnv-s-3-thro-range-891"></a>
### _CNV_S_3_THRO_RANGE_891

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | N_NOT_LIM |
| 0x01 | N_LIM_CON |
| 0x02 | N_LIM_PVS |
| 0xFF | undefiniert |

<a id="table-cnv-s-4-egcp-range-251"></a>
### _CNV_S_4_EGCP_RANGE_251

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NO_SYM |
| 0x01 | TTIP_ERR |
| 0x02 | READY_ERR |
| 0x04 | TTIP_MES_ERR |
| 0xFF | undefiniert |

<a id="table-cnv-s-4-egcp-range-253"></a>
### _CNV_S_4_EGCP_RANGE_253

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | NO_SYM |
| 0x01 | TTIP_ERR |
| 0x02 | READY_ERR |
| 0x04 | TTIP_MES_ERR |
| 0xFF | undefiniert |

<a id="table-cnv-s-4-egcp-range-259"></a>
### _CNV_S_4_EGCP_RANGE_259

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | VLS_OK |
| 0x01 | VLS_L |
| 0x02 | VLS_H_OC |
| 0x04 | VLS_AFS_OC |
| 0xFF | undefiniert |

<a id="table-cnv-s-4-egcp-range-261"></a>
### _CNV_S_4_EGCP_RANGE_261

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | VLS_OK |
| 0x01 | VLS_L |
| 0x02 | VLS_H_OC |
| 0x04 | VLS_AFS_OC |
| 0xFF | undefiniert |

<a id="table-cnv-s-5-laco-range-298"></a>
### _CNV_S_5_LACO_RANGE_298

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | 1:OL_CDN |
| 0x02 | 2:CL |
| 0x04 | 4:OL_INTR |
| 0x08 | 8:OL_ERR |
| 0x10 | 10:CL_ERR |
| 0xFF | undefiniert |

<a id="table-cnv-s-5-laco-range-300"></a>
### _CNV_S_5_LACO_RANGE_300

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | 1:OL_CDN |
| 0x02 | 2:CL |
| 0x04 | 4:OL_INTR |
| 0x08 | 8:OL_ERR |
| 0x10 | 10:CL_ERR |
| 0xFF | undefiniert |

<a id="table-cnv-s-5-cnv-s-5-d-607"></a>
### _CNV_S_5__CNV_S_5_D_607

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE |
| 0x01 | Schicht |
| 0x02 | Homogen |
| 0x03 | Homogen_Schicht |
| 0x08 | NOTLAUF |
| 0xFF | undefiniert |

<a id="table-cnv-s-5-cnv-s-5-d-608"></a>
### _CNV_S_5__CNV_S_5_D_608

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | KEINE |
| 0x01 | Schicht |
| 0x02 | Homogen |
| 0x03 | Homogen_Schicht |
| 0x08 | NOTLAUF |
| 0xFF | undefiniert |

<a id="table-cnv-s-6-range-stat-56"></a>
### _CNV_S_6_RANGE_STAT_56

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ES |
| 0x01 | ST |
| 0x02 | IS |
| 0x03 | PL |
| 0x04 | PU |
| 0x05 | PUC |
| 0xFF | undefiniert |

<a id="table-cnv-s-7-egcp-range-232"></a>
### _CNV_S_7_EGCP_RANGE_232

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | LSH_OFF |
| 0x01 | LSH_POW_RISE |
| 0x02 | LSH_POW_RED |
| 0x03 | LSH_POW_FALL |
| 0x04 | LSH_POW_CTL |
| 0x05 | LSH_VB_PROT |
| 0x06 | LSH_TEMP_PROT |
| 0xFF | undefiniert |

<a id="table-cnv-s-7-egcp-range-234"></a>
### _CNV_S_7_EGCP_RANGE_234

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | LSH_OFF |
| 0x01 | LSH_POW_RISE |
| 0x02 | LSH_POW_RED |
| 0x03 | LSH_POW_FALL |
| 0x04 | LSH_POW_CTL |
| 0x05 | LSH_VB_PROT |
| 0x06 | LSH_TEMP_PROT |
| 0xFF | undefiniert |

<a id="table-cnv-s-7-range-ecu-54"></a>
### _CNV_S_7_RANGE_ECU__54

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ENG_STOP |
| 0x01 | RUN_ENG |
| 0x02 | SYN_ENG_IGK_ON |
| 0x03 | SYN_ENG_IGK_OFF |
| 0x04 | PWL |
| 0x05 | ENG_LOCK |
| 0x06 | WAKE_UP |
| 0xFF | undefiniert |

<a id="table-cnv-s-8-range-stat-144"></a>
### _CNV_S_8_RANGE_STAT_144

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
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

<a id="table-cnv-s-8-range-stat-145"></a>
### _CNV_S_8_RANGE_STAT_145

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
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

<a id="table-msd87-r0def-st-atlsvc-bmsnf"></a>
### _MSD87_R0DEF_ST_ATLSVC_BMSNF

Dimensions: 9 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Startbedingung nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 5 | Funktionstest laeuft |
| 6 | Funktion beendet |
| 7 | Funktion abgebrochen |
| 8 | Funktion vollstaendig durchlaufen und kein Fehler erkannt |
| 9 | Funktion vollstaendig durchlaufen und Fehler erkannt |

<a id="table-msd87-r0def-st-atlsvc-pvdk-bmsnf"></a>
### _MSD87_R0DEF_ST_ATLSVC_PVDK_BMSNF

Dimensions: 6 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Ladedruckdiagnose ohne Ergebnis |
| 1 | Ladedruck fehlerfrei |
| 2 | Gesamtladedruck zu niedrig |
| 3 | Turbolader 1 mit Ladedruckfehler |
| 4 | Turbolader 2 mit Ladedruckfehler |
| 5 | Gesamtladedruck zu niedrig, Bank nicht identifiziert |

<a id="table-msd87-r0-cnv-s-10-state-eol-449-cm-4dc3200s"></a>
### _MSD87_R0_CNV_S_10_STATE_EOL__449_CM_4DC3200S

Dimensions: 10 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Startbedingungen nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | Undefinierter Zustand |
| 5 | Funktionstest laeuft |
| 6 | Funktion ergebnislos beendet |
| 7 | Funktion abgebrochen |
| 8 | Funktion durchlaufen und kein Fehler erkannt |
| 9 | Funktion durchlaufen und Fehler erkannt |

<a id="table-msd87-r0-cnv-s-10-state-eol-449-cm-4dc3200s"></a>
### _MSD87_R0_CNV_S_10_STATE_EOL__449_CM_4DC3200S_

Dimensions: 10 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Startbedingungen nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | Undefinierter Zustand |
| 5 | Funktionstest laeuft |
| 6 | Funktion ergebnislos beendet |
| 7 | Funktion abgebrochen |
| 8 | Funktion durchlaufen und kein Fehler erkannt |
| 9 | Funktion durchlaufen und Fehler erkannt |

<a id="table-msd87-r0-cnv-s-10-state-eol-960-cm-9sp8300s"></a>
### _MSD87_R0_CNV_S_10_STATE_EOL__960_CM_9SP8300S

Dimensions: 10 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Startbedingung nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | nicht Definiert |
| 5 | Funktionstest laeuft |
| 6 | Funktion beendet ohne Ergebniss |
| 7 | Funktion abgebrochen |
| 8 | Funktion vollstaendig durchlaufen und kein Fehler erkannt |
| 9 | Funktion vollstaendig durchlaufen und Fehler erkannt |

<a id="table-msd87-r0-cnv-s-13-state-dmtl-140-cm"></a>
### _MSD87_R0_CNV_S_13_STATE_DMTL_140_CM

Dimensions: 21 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Start |
| 1 | Erste Referenzleck Messung |
| 2 | Grobleck Messung Start |
| 3 | Grobleck Messung erweitert |
| 4 | Grobleck Messung beendet |
| 5 | Feinleck Messung Start |
| 6 | Feinleck Messung erweitert |
| 7 | Zweite Referenzleck Messung |
| 8 | Tank geprueft |
| 9 | Feinleck |
| 10 | Grobleck |
| 11 | Modulfehler |
| 12 | Ende |
| 17 | Batteriespannung aus gueltigem Bereich |
| 18 | elektrischer Fehler |
| 33 | Tank nachfuellen festgestellt |
| 34 | Tankverschluss offen |
| 35 | Batteriespannung Fluktuation zu hoch |
| 36 | Diagnose maximale Zeit erreicht |
| 37 | Fluktuation Referenzsrtom zu hoch |
| 38 | Pumpenstrom abgefallen waehrend der Messung |

<a id="table-msd87-r0-cnv-s-2-def-bit-uw-683-cm-4dc3500s"></a>
### _MSD87_R0_CNV_S_2_DEF_BIT_UW_683_CM_4DC3500S

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Falsch |
| 1 | Wahr |

<a id="table-msd87-r0-cnv-s-2-cnv-s-2-d-435-cm-0x4-792e940s"></a>
### _MSD87_R0_CNV_S_2__CNV_S_2_D_435_CM_0X4_792E940S

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | FALSE |
| 4 | TRUE |

<a id="table-msd87-r0-cnv-s-4-cybl-range-179-cm-792a900s"></a>
### _MSD87_R0_CNV_S_4_CYBL_RANGE_179_CM_792A900S

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | NO |
| 1 | LOW |
| 2 | HIGH |
| 3 | IS |

<a id="table-msd87-r0-cnv-s-4-cybl-range-180-cm-792a900s"></a>
### _MSD87_R0_CNV_S_4_CYBL_RANGE_180_CM_792A900S

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | INITIALIZATION |
| 1 | LOCK |
| 2 | WAIT |
| 3 | CYLINDER_BALANCING |

<a id="table-msd87-r0-cnv-s-4-range-stat-455-cm-4dc3200s"></a>
### _MSD87_R0_CNV_S_4_RANGE_STAT_455_CM_4DC3200S

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Deaktiviert |
| 1 | Fertigungsmodus |
| 2 | Transportmodus |
| 3 | Flashmodus |

<a id="table-msd87-r0-cnv-s-4-state-ch-776-cm-762e940s"></a>
### _MSD87_R0_CNV_S_4_STATE_CH_776_CM_762E940S

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | CH_OFF |
| 1 | CH_AST |
| 2 | CH_LOW_LOAD |
| 3 | CH_SO2P |

<a id="table-msd87-r0-cnv-s-5-def-ba-gdi-588-cm"></a>
### _MSD87_R0_CNV_S_5_DEF_BA_GDI_588_CM

Dimensions: 5 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Keine |
| 1 | Schicht |
| 2 | Homogen |
| 3 | Homogen_Schicht |
| 8 | Notlauf |

<a id="table-msd87-r0-cnv-s-6-state-diag-157-cm"></a>
### _MSD87_R0_CNV_S_6_STATE_DIAG_157_CM

Dimensions: 6 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Initialisierung |
| 1 | Schritt 1 |
| 2 | Schritt 2 |
| 3 | Schritt 3 |
| 4 | Rampe |
| 5 | Ende LOCK_STEP |

<a id="table-msd87-r0-tabel-status-obd-monitor"></a>
### _MSD87_R0_TABEL_STATUS_OBD_MONITOR

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-msd87-r0-tabel-status-obd-readiness"></a>
### _MSD87_R0_TABEL_STATUS_OBD_READINESS

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-msd87-r0-table-fs"></a>
### _MSD87_R0_TABLE_FS

Dimensions: 11 rows × 2 columns

| NR | TEXT |
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

<a id="table-msd87-r0-table-geniutest-ab-bit0"></a>
### _MSD87_R0_TABLE_GENIUTEST_AB_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorauslastung nicht zu hoch |
| 1 | Generatortest, Generatorauslastung zu hoch |

<a id="table-msd87-r0-table-geniutest-err-bit0"></a>
### _MSD87_R0_TABLE_GENIUTEST_ERR_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, elektrischer Fehler Generator nicht vorhanden |
| 1 | Generatortest, elektrischer Fehler Generator vorhanden |

<a id="table-msd87-r0-table-geniutest-err-bit1"></a>
### _MSD87_R0_TABLE_GENIUTEST_ERR_BIT1

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, mechanischer Fehler Generator nicht vorhanden |
| 1 | Generatortest, mechanischer Fehler Generator vorhanden |

<a id="table-msd87-r0-table-geniutest-err-bit2"></a>
### _MSD87_R0_TABLE_GENIUTEST_ERR_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Hochtemperaturfehler Generator nicht vorhanden |
| 1 | Generatortest, Hochtemperaturfehler Generator vorhanden |

<a id="table-msd87-r0-table-geniutest-err-bit3"></a>
### _MSD87_R0_TABLE_GENIUTEST_ERR_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatortyp plausibel |
| 1 | Generatortest, Generatortyp unplausibel |

<a id="table-msd87-r0-table-geniutest-err-bit4"></a>
### _MSD87_R0_TABLE_GENIUTEST_ERR_BIT4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorkommunikation vorhanden |
| 1 | Generatortest, keine Generatorkommunikation vorhanden |

<a id="table-msd87-r0-table-geniutest-err-bit5"></a>
### _MSD87_R0_TABLE_GENIUTEST_ERR_BIT5

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorspannung aus Berechnung plausibel |
| 1 | Generatortest, Generatorspannung aus Berechnung unplausibel |

<a id="table-msd87-r0-table-geniutest-err-bit6"></a>
### _MSD87_R0_TABLE_GENIUTEST_ERR_BIT6

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Hochtemperaturfehler Generator aus Berechnung nicht vorhanden |
| 1 | Generatortest, Hochtemperaturfehler Generator aus Berechnung vorhanden |

<a id="table-msd87-r0-table-geniutest-err-bit7"></a>
### _MSD87_R0_TABLE_GENIUTEST_ERR_BIT7

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorregler plausibel |
| 1 | Generatortest, Generatorregler unplausibel |

<a id="table-msd87-r0-table-status-batteriezustand"></a>
### _MSD87_R0_TABLE_STATUS_BATTERIEZUSTAND

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Batterie i.O. |
| 1 | Batterie pruefen |
| 2 | Batterie nicht i.O. |
| 3 | ungueltig |

<a id="table-msd87-r0-table-status-ibs-bze"></a>
### _MSD87_R0_TABLE_STATUS_IBS_BZE

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | keine BZE3 |
| 1 | BZE3 |

<a id="table-msd87-r0-table-status-letzter-batteriewechsel"></a>
### _MSD87_R0_TABLE_STATUS_LETZTER_BATTERIEWECHSEL

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Wechsel zulaessig |
| 1 | Wechsel unzulaessig |

<a id="table-msd87-r0-table-status-tiefentladen"></a>
### _MSD87_R0_TABLE_STATUS_TIEFENTLADEN

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Batterie i.O. |
| 1 | Batterie tiefentladen |

<a id="table-msd87-r0-table-status-wasserverlust"></a>
### _MSD87_R0_TABLE_STATUS_WASSERVERLUST

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Wasserverbrauch i.O. |
| 1 | Wasserverbrauch nicht i.O. |

<a id="table-msd87-r0-table-st-gentest"></a>
### _MSD87_R0_TABLE_ST_GENTEST

Dimensions: 8 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Start-/Ansteuerbedingung nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | -- |
| 5 | Funktion laeuft |
| 6 | Funktion beendet |
| 7 | Funktion abgebrochen |

<a id="table-msd87-r0-table-switch-position-bit0"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Klemme-15 aus |
| 1 | Klemme-15 ein |

<a id="table-msd87-r0-table-switch-position-bit1"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_BIT1

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Motor laeuft |
| 1 | Motor steht |

<a id="table-msd87-r0-table-switch-position-bit2"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Kupplung aus |
| 1 | Kupplung ein |

<a id="table-msd87-r0-table-switch-position-bit3"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Bremslichtschalter-Kanal 1 aus |
| 1 | Bremslichtschalter-Kanal 1 ein |

<a id="table-msd87-r0-table-switch-position-bit4"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_BIT4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Bremslichtschalter-Kanal 2 aus |
| 1 | Bremslichtschalter-Kanal 2 ein |

<a id="table-msd87-r0-table-switch-position-bit7"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_BIT7

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Anforderung Klimabereitschaft aus |
| 1 | Anforderung Klimabereitschaft ein |

<a id="table-msd87-r0-table-switch-position-high-byte-bit0"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein Leerlauf |
| 1 | Leerlauf |

<a id="table-msd87-r0-table-switch-position-high-byte-bit1"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT1

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | keine Vollast |
| 1 | Vollast |

<a id="table-msd87-r0-table-switch-position-high-byte-bit2"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Lambdaregelung hinter Katalysator Bank 1 nicht aktiv |
| 1 | Lambdaregelung hinter Katalysator Bank 1 aktiv |

<a id="table-msd87-r0-table-switch-position-high-byte-bit3"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Lambdaregelung hinter Katalysator Bank 2 nicht aktiv |
| 1 | Lambdaregelung hinter Katalysator Bank 2 aktiv |

<a id="table-msd87-r0-table-switch-position-high-byte-bit4"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Lambdaregelung vor Katalysator Bank 2 nicht aktiv |
| 1 | Lambdaregelung vor Katalysator Bank 2 aktiv |

<a id="table-msd87-r0-table-switch-position-high-byte-bit5"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT5

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Lambdaregelung vor Katalysator Bank 1 nicht aktiv |
| 1 | Lambdaregelung vor Katalysator Bank 1 aktiv |

<a id="table-msd87-r0-table-switch-position-high-byte-bit6"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT6

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Regelkreis Bank 2 nicht geschlossen |
| 1 | Regelkreis Bank 2 geschlossen |

<a id="table-msd87-r0-table-switch-position-high-byte-bit7"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT7

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Regelkreis Bank 1 nicht geschlossen |
| 1 | Regelkreis Bank 1 geschlossen |

<a id="table-msd87-r0-table-switch-position-low-byte-bit2"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_LOW_BYTE_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein Kickdown erkannt |
| 1 | Kickdown erkannt |

<a id="table-msd87-r0-table-switch-position-low-byte-bit3"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_LOW_BYTE_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Gang nicht eingelegt, Park- oder Neutralstellung |
| 1 | Gang eingelegt, nicht Park- oder Neutralstellung |

<a id="table-msd87-r0-table-switch-position-low-byte-bit6"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_LOW_BYTE_BIT6

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | keine Schubabschaltung aktiv |
| 1 | Schubabschaltung aktiv |

<a id="table-msd87-r0-table-switch-position-low-byte-bit7"></a>
### _MSD87_R0_TABLE_SWITCH_POSITION_LOW_BYTE_BIT7

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Drosselklappen-Neuabgleich nicht erforderlich |
| 1 | Drosselklappen-Neuabgleich erforderlich |

<a id="table-motorudscodierung-ruhestrom"></a>
### MOTORUDSCODIERUNG_RUHESTROM

Dimensions: 16 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Ruhestrom kleiner 80mA, keine Aktion des IBS |
| 1 | Ruhestrom = 80...200mA, keine Aktion da Entladung kleiner Schwellwert |
| 2 | Ruhestrom = 200...1000mA, keine Aktion da Entladung kleiner Schwellwert |
| 3 | Ruhestrom groesser 1000mA, keine Aktion da Entladung kleiner Schwellwert |
| 4 | Ruhestrom kleiner 80mA, Anforderung Reset Kl.30f (B_ierr1 = 1) |
| 5 | Ruhestrom = 80...200mA, Anforderung Reset Kl.30f (B_ierr1 = 1) |
| 6 | Ruhestrom = 200...1000mA, Anforderung Reset Kl.30f (B_ierr1 = 1) |
| 7 | Ruhestrom groesser 1000mA, Anforderung Reset Kl.30f (B_ierr1 = 1) |
| 8 | Ruhestrom kleiner 80mA, Anforderung Abschaltung Kl.30f (B_ierr2 = 1) |
| 9 | Ruhestrom = 80...200mA, Anforderung Abschaltung Kl.30f (B_ierr2 = 1) |
| 10 | Ruhestrom = 200...1000mA, Anforderung Abschaltung Kl.30f (B_ierr2 = 1) |
| 11 | Ruhestrom groesser 1000mA, Anforderung Abschaltung Kl.30f (B_ierr2 = 1) |
| 12 | Ruhestrom kleiner 80mA, erneuter Fehler bei Kl.30f aus (B_ierr3 = 1) |
| 13 | Ruhestrom = 80...200mA, erneuter Fehler bei Kl.30f aus (B_ierr3 = 1) |
| 14 | Ruhestrom = 200...1000mA, erneuter Fehler bei Kl.30f aus (B_ierr3 = 1) |
| 15 | Ruhestrom groesser 1000mA, erneuter Fehler bei Kl.30f aus (B_ierr3 = 1) |
