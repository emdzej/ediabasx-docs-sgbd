# mevd172_alt.prg

- Jobs: [234](#jobs)
- Tables: [107](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MEVD172 für N55 mit UDS-Protokoll |
| ORIGIN | BMW EA-413 Ortner |
| REVISION | 3.003 |
| AUTHOR | P&Z EA-413 Berger, P&Z EA-413 Lorch, P&Z EA-413 Hadersdorfer |
| COMMENT | SGBD für MEVD172 C-Muster zur SW 7572650B |
| PACKAGE | 1.12 |
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
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Seriennummer des Steuergeraets UDS  : $22   ReadDataByIdentifier UDS  : $F18C Sub-Parameter ECUSerialNumber Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $0F06 ClearSecondaryDTCMemory Modus: Default
- [STATUS_BLOCK_LESEN](#job-status-block-lesen) - Lesen eines dynamisch definierten Datenblockes UDS  : $2C DynamicallyDefineDataIdentifier $03 ClearDynamicallyDefinedDataIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $2C DynamicallyDefineDataIdentifier $01 DefineByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  UDS  : $22 ReadDataByIdentifier $F300-$F3FF DynamicallyDefinedDataIdentifier  $2C$02 DefineByMemoryAddress wird nicht unterstützt 'Composite data blocks' werden nur komplett unterstützt
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
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS-Version 5) UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)
- [STEUERN_ROE_STOP](#job-steuern-roe-stop) - Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime)
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $04 report activated events
- [STEUERN_ROE_START](#job-steuern-roe-start) - Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime)
- [CPS_LESEN](#job-cps-lesen) - Codierpruefstempel lesen UDS  : $22   ReadDataByIdentifier UDS  : $37FE DataIdentifier Codierpruefstempel Modus: Default
- [DIAG_SESSION_LESEN](#job-diag-session-lesen) - Aktive Diagnose-Session auslesen UDS  : $22   ReadDataByIdentifier UDS  : $F186 ActiveDiagnosticSession Modus: Default
- [FLASH_TP_LESEN](#job-flash-tp-lesen) - Flash Timing Parameter auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2504 FlashTimingParameter Modus: Default
- [PROG_ZAEHLER_LESEN](#job-prog-zaehler-lesen) - Programmierzaehler lesen UDS  : $22   ReadDataByIdentifier UDS  : $2502 ProgrammingCounter Modus: Default
- [PROG_MAX_LESEN](#job-prog-max-lesen) - Anzahl der maximal möglichen Programmiervorgänge auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2503 ProgrammingCounter Modus: Default
- [IS_LESEN](#job-is-lesen) - Sekundaerer Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $22   ReadDataByIdentifierRequestServiceID UDS  : $2000 DataIdentifier sekundaerer Fehlerspeicher Modus: Default
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - sekundären Fehlerspeicher lesen (Info-Meldungen / Ort und Art) UDS  : $22 ReadDataByIdentifier UDS  : $20 dataIdentifier UDS  : $00 alle Info-Meldungen anschließend UDS  : $20 dataIdentifier UDS  : $nn Details zur Info-Meldung an der Position n Modus: Default
- [STEUERN_EWS4_SK](#job-steuern-ews4-sk) - 17 "EWS4-data" schreiben UDS   : $2E   WriteDataByIdentifier UDS   : $C001 Sub-Parameter
- [STATUS_EWS](#job-status-ews) - Zurücklesen verschiedener interner Stati für EWS UDS   : $22   ReadDataByIdentifier UDS   : $C000 Sub-Parameter
- [STATUS_EWS4_SK](#job-status-ews4-sk) - Lesen des SecretKey des Server sowie Client für EWS4 UDS   : $22   ReadDataByIdentifier UDS   : $C002 Sub-Parameter
- [FS_LESEN_PERMANENT](#job-fs-lesen-permanent) - permanente Fehler aus Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $15 ReportDTCWithPermanentStatus Modus: Default
- [SPEICHER_LESEN_ASCII](#job-speicher-lesen-ascii) - 0x23 SPEICHER_LESEN_ASCII Auslesen des Steuergeraete-Speichers Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_SWE_LESEN](#job-swe-lesen) - 0x31010205 SWE_LESEN Informationen zu Softwareeinheiten auf dem Steuergerät unter Verwendung des Jobs SVK_LESEN UDS  : $31   RoutinControl by RequestSerice ID UDS  : $01xx Sub-Parameter fuer SVK UDS  : $0205 SWEDI (Default) Modus: Default
- [MESSWERTBLOCK_LESEN](#job-messwertblock-lesen) - 0x2CF0 MESSWERTBLOCK_LESEN DDLI Messwerte auf Basis Übergabestring aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [ABGLEICHWERTE_SCHREIBEN](#job-abgleichwerte-schreiben) - 0x2E5F90 ABGLEICHWERTE_SCHREIBEN Abgleichwerte Injektoren programmieren für CASCADE mit Übernahme Daten aus COD-Datei Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - 0x225F90 ABGLEICHWERTE_LESEN Abgleichwerte Injektoren auslesen für CASCADE für Vergleich mit Daten aus COD-Datei Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [START_SYSTEMCHECK_LLERH](#job-start-systemcheck-llerh) - Ansteuern Diagnosefunktion Leerlauf-Erhoehung SYSTEMCHECK_LLERH (0xF026)
- [STATUS_SYSTEMCHECK_LLERH](#job-status-systemcheck-llerh) - Auslesen Diagnosefunktion Leerlauf-Erhoehung SYSTEMCHECK_LLERH (0xF026)
- [STOP_SYSTEMCHECK_LLERH](#job-stop-systemcheck-llerh) - Diagnosefunktion Leerlauf-Erhoehung beenden SYSTEMCHECK_LLERH (0xF026)
- [STATUS_BZEDIAG](#job-status-bzediag) - BZE Infospeicher BZEDIAG (0x403B)
- [STATUS_MESSWERTE](#job-status-messwerte) - Messwerte auslesen MESSWERTE (0x4000)
- [STATUS_DFMONITOR](#job-status-dfmonitor) - Batterieladezustand auslesen DFMONITOR (0x4001)
- [STATUS_DIGITAL_1](#job-status-digital-1) - Status Schaltzustaende 1 DIGITAL_1 (0x4002)
- [STATUS_NOCKENWELLE_ADAPTION](#job-status-nockenwelle-adaption) - Nockenwellenadationswerte auslesen NOCKENWELLE_ADAPTION (0x4006)
- [STATUS_DIGITAL_0](#job-status-digital-0) - Status Schaltzustaende 0 DIGITAL_0 (0x4007)
- [STATUS_ADAPTION_DK](#job-status-adaption-dk) - Drosselklappenadaptionswerte auslesen ADAPTION_DK (0x4008)
- [STATUS_ADAPTION_GEMISCH](#job-status-adaption-gemisch) - Gemischadaptionswerte auslesen ADAPTION_GEMISCH (0x400A)
- [STATUS_MESSWERTE_VVT](#job-status-messwerte-vvt) - VVT Messwerte auslesen MESSWERTE_VVT (0x400B)
- [FASTA10](#job-fasta10) - FASTA-Messwertblock 10 lesen FASTA10 (0x4015)
- [STATUS_GENINFO](#job-status-geninfo) - Infospeicher Generatordiagnose erweitert auslesen GENINFO (0x401B)
- [IDENT_IBS](#job-ident-ibs) - Identifikationsdaten fuer IBS-Sensor auslesen IDENT_IBS (0x4021)
- [STATUS_MESSWERTE_EWAP](#job-status-messwerte-ewap) - elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) Messwerte auslesen MESSWERTE_EWAP (0x4024)
- [STATUS_MESSWERTE_VAD](#job-status-messwerte-vad) - Variantenadaptionen auslesen MESSWERTE_VAD (0x4025)
- [STATUS_RBMMODE9](#job-status-rbmmode9) - Rate Based Monitoring Mode 9 auslesen (Ausgabe der Werte wie im Scantool Mode 9) RBMMODE9 (0x4026)
- [STATUS_RBMME1](#job-status-rbmme1) - Rate Based Monitoring Motorsteuerung ME... Block 1 auslesen (Vorhalt) RBMME1 (0x4029)
- [STATUS_RBMME2](#job-status-rbmme2) - Rate Based Monitoring Motorsteuerung ME... Block 2 auslesen (Vorhalt) RBMME2 (0x402A)
- [STATUS_MESSWERTE_LRP](#job-status-messwerte-lrp) - Messwerte Laufruhepruefung auslesen MESSWERTE_LRP (0x402D)
- [STATUS_CALCVN](#job-status-calcvn) - Cal-ID (Calibration-ID) und CVN(Calibration Verification Number) auslesen. CALCVN (0x403C)
- [STATUS_INJAD](#job-status-injad) - Injektor Adaptionswerte lesen INJAD (Kleinstmengen-Adaption RB-Umfaenge) INJAD (0x403F)
- [STATUS_ATLDIAG](#job-status-atldiag) - Turboladerstatus auslesen ATLDIAG (0x4044)
- [STATUS_KLANNADAP](#job-status-klannadap) - KLANN Adaptionen auslesen KLANNADAP (0x4046)
- [STATUS_TYPPRUEFNR](#job-status-typpruefnr) - Typpruefnummer fuer BN2020 SGs auslesen TYPPRUEFNR (0x4047)
- [STATUS_READINESS](#job-status-readiness) - Monitorfunktionen und Readinessflags aus DME auslesen READINESS (0x4105)
- [STATUS_GVOBD](#job-status-gvobd) - Gemischvertrimmung fuer OBD-Demo und PVE auslesen. GVOBD (0x5F80)
- [STEUERN_GVOBD](#job-steuern-gvobd) - Gemischvertrimmung fuer OBD-Demo und PVE vorgeben. Der Korrekturfaktor soll bei Klemmenwechsel auf den Standardwert 1 zurueckgesetzt werden. STEUERN_GVOBD (0x5F80)
- [STEUERN_PROGRAMM_GVOBD](#job-steuern-programm-gvobd) - Gemischvertrimmung fuer OBD-Demo und PVE programmieren. STEUERN_PROGRAMM_GVOBD (0x5F80)
- [STATUS_PM_BACKUP](#job-status-pm-backup) - Auslesen des PM-Backup PM_BACKUP (0x5F8B)
- [STEUERN_PM_RESTORE](#job-steuern-pm-restore) - Schreiben PM-Restore PM_RESTORE (0x5F8B)
- [STATUS_HUBKORR](#job-status-hubkorr) - Hubkorrektur auslesen HUBKORR (0x5F8C)
- [STEUERN_HUBKORR_PROGRAMMIEREN](#job-steuern-hubkorr-programmieren) - Hubkorrektur programmieren STEUERN_HUBKORR_PROGRAMMIEREN (0x5F8C)
- [STEUERN_HUBKORR_RESET](#job-steuern-hubkorr-reset) - Hubkorrektur loeschen STEUERN_HUBKORR_RESET (0x5F8C)
- [STEUERN_HUBKORR_VERSTELLEN](#job-steuern-hubkorr-verstellen) - Hubkorrektur vorgeben STEUERN_HUBKORR_VERSTELLEN (0x5F8C)
- [STATUS_IMAALLE](#job-status-imaalle) - Abgleichwerte Injektoren auslesen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. IMAALLE (0x5F90)
- [STEUERN_IMAALLE](#job-steuern-imaalle) - Abgleichwerte Injektoren programmieren IMAALLE (0x5F90)
- [STEUERN_IMA_ZYL_1](#job-steuern-ima-zyl-1) - Abgleichwert Injektor 01 (phys) programmieren IMA_ZYL_1 (0x5F91)
- [STEUERN_IMA_ZYL_2](#job-steuern-ima-zyl-2) - Abgleichwert Injektor 02 (phys) programmieren IMA_ZYL_2 (0x5F92)
- [STEUERN_IMA_ZYL_3](#job-steuern-ima-zyl-3) - Abgleichwert Injektor 03 (phys) programmieren IMA_ZYL_3 (0x5F93)
- [STEUERN_IMA_ZYL_4](#job-steuern-ima-zyl-4) - Abgleichwert Injektor 04 (phys) programmieren IMA_ZYL_4 (0x5F94)
- [STEUERN_IMA_ZYL_5](#job-steuern-ima-zyl-5) - Abgleichwert Injektor 05 (phys) programmieren IMA_ZYL_5 (0x5F95)
- [STEUERN_IMA_ZYL_6](#job-steuern-ima-zyl-6) - Abgleichwert Injektor 06 (phys) programmieren IMA_ZYL_6 (0x5F96)
- [STEUERN_KVA](#job-steuern-kva) - KraftstoffVerbrauchsAnzeige - Korrekturfaktor schreiben KVA (0x5FC1)
- [STATUS_VVTMINH](#job-status-vvtminh) - VVT-Minhub auslesen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. VVTMINH (0x5FDE)
- [STATUS_LL_ABGLEICH](#job-status-ll-abgleich) - Abgleichwert LL (Leerlauf) auslesen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. LL_ABGLEICH (0x5FF0)
- [STEUERN_ENDE_ABLL](#job-steuern-ende-abll) - Abgleichwert LL (Leerlauf) Vorgeben beenden STEUERN_ENDE_ABLL (0x5FF0)
- [STEUERN_LLABG_PROG](#job-steuern-llabg-prog) - Abgleichwert LL (Leerlauf) programmieren STEUERN_LLABG_PROG (0x5FF0)
- [STEUERN_LL_ABGLEICH](#job-steuern-ll-abgleich) - Abgleichwert LL (Leerlauf) vorgeben STEUERN_LL_ABGLEICH (0x5FF0)
- [ECU_CONFIG](#job-ecu-config) - Variante auslesen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. ECU_CONFIG (0x5FF2)
- [ECU_CONFIG_RESET](#job-ecu-config-reset) - Variante loeschen ECU_CONFIG_RESET (0x5FF2)
- [STEUERN_PM_HISTOGRAM_RESET](#job-steuern-pm-histogram-reset) - Powermanagement Histogramm loeschen STEUERN_PM_HISTOGRAM_RESET (0x5FF5)
- [STEUERN_DK](#job-steuern-dk) - Drosselklappe ansteuern DK (0x602A)
- [STEUERN_ENDE_DK](#job-steuern-ende-dk) - Drosselklappe Ansteuerung beenden DK (0x602A)
- [STEUERN_ENDE_UGEN](#job-steuern-ende-ugen) - Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden UGEN (0x6032)
- [STEUERN_UGEN](#job-steuern-ugen) - Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) ansteuern UGEN (0x6032)
- [STEUERN_ELUER](#job-steuern-eluer) - E-Luefter-Relais ansteuern ELUER (0x6081)
- [STEUERN_ENDE_ELUER](#job-steuern-ende-eluer) - E-Luefter-Relais Ansteuerung beenden ELUER (0x6081)
- [STEUERN_ENDE_GLF2](#job-steuern-ende-glf2) - Gesteuerte Luftfuehrung Klappe 2 Ansteuerung beenden GLF2 (0x60A4)
- [STEUERN_GLF2](#job-steuern-glf2) - Gesteuerte Luftfuehrung Klappe 2 ansteuern GLF2 (0x60A4)
- [STEUERN_ENDE_ODR](#job-steuern-ende-odr) - Oel Druck Regelung (Geregeltes Oeldrucksystem) Ansteuerung beenden ODR (0x60AB)
- [STEUERN_ODR](#job-steuern-odr) - Oel Druck Regelung (Geregeltes Oeldrucksystem) ansteuern ODR (0x60AB)
- [STEUERN_ENDE_ODV](#job-steuern-ende-odv) - Oeldruckventil (Geregeltes Oeldrucksystem) Ansteuerung beenden ODV (0x60AC)
- [STEUERN_ODV](#job-steuern-odv) - Oeldruckventil (Geregeltes Oeldrucksystem) ansteuern ODV (0x60AC)
- [STEUERN_ENDE_MLS](#job-steuern-ende-mls) - Motorlagersteuerung Ansteuerung beenden MLS (0x60B2)
- [STEUERN_MLS](#job-steuern-mls) - Motorlagersteuerung ansteuern MLS (0x60B2)
- [STEUERN_ENDE_ULV](#job-steuern-ende-ulv) - Umluftventil Ansteuerung beenden ULV (0x60B5)
- [STEUERN_ULV](#job-steuern-ulv) - Umluftventil ansteuern ULV (0x60B5)
- [STEUERN_ENDE_LDS1](#job-steuern-ende-lds1) - Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) Ansteuerung beenden LDS1 (0x60B6)
- [STEUERN_LDS1](#job-steuern-lds1) - Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) ansteuern LDS1 (0x60B6)
- [STEUERN_ENDE_MSV](#job-steuern-ende-msv) - Mengensteuerventil Ansteuerung beenden MSV (0x60BD)
- [STEUERN_MSV](#job-steuern-msv) - Mengensteuerventil ansteuern MSV (0x60BD)
- [STEUERN_ENDE_EWAP](#job-steuern-ende-ewap) - elektr. Wasserpumpe Ansteuerung beenden EWAP (0x60BF)
- [STEUERN_EWAP](#job-steuern-ewap) - elektr. Wasserpumpe (Bit Serielle Datenschnittstelle) ansteuern EWAP (0x60BF)
- [STEUERN_AGK](#job-steuern-agk) - Abgasklappe ansteuern AGK (0x60C1)
- [STEUERN_ENDE_AGK](#job-steuern-ende-agk) - Abgasklappe Ansteuerung beenden AGK (0x60C1)
- [STEUERN_ENDE_GLF](#job-steuern-ende-glf) - Gesteuerte Luftfuehrung (Klappe 1) Ansteuerung beenden GLF (0x60C3)
- [STEUERN_GLF](#job-steuern-glf) - Gesteuerte Luftfuehrung (Klappe 1) ansteuern GLF (0x60C3)
- [STEUERN_ENDE_KFT](#job-steuern-ende-kft) - Kennfeldthermostat Ansteuerung beenden KFT (0x60C9)
- [STEUERN_KFT](#job-steuern-kft) - Kennfeldthermostat ansteuern KFT (0x60C9)
- [STEUERN_DMTL_P](#job-steuern-dmtl-p) - Diagnosemodul-Tank Leckage Pumpe ansteuern DMTL_P (0x60CC)
- [STEUERN_ENDE_DMTL_P](#job-steuern-ende-dmtl-p) - Diagnosemodul-Tank Leckage Pumpe Ansteuerung beenden DMTL_P (0x60CC)
- [STEUERN_DMTL_V](#job-steuern-dmtl-v) - Diagnosemodul-Tank Leckage Ventil ansteuern DMTL_V (0x60CD)
- [STEUERN_ENDE_DMTL_V](#job-steuern-ende-dmtl-v) - Diagnosemodul-Tank Leckage Ventil Ansteuerung beenden DMTL_V (0x60CD)
- [STEUERN_DMTL_HEIZUNG](#job-steuern-dmtl-heizung) - Diagnosemodul-Tank Leckage Heizung ansteuern DMTL_HEIZUNG (0x60CE)
- [STEUERN_ENDE_DMTL_HEIZUNG](#job-steuern-ende-dmtl-heizung) - Diagnosemodul-Tank Leckage Heizung Ansteuerung beenden DMTL_HEIZUNG (0x60CE)
- [STEUERN_ENDE_TEV](#job-steuern-ende-tev) - Tankentlueftungsventil Ansteuerung beenden TEV (0x60CF)
- [STEUERN_TEV](#job-steuern-tev) - Tankentlueftungsventil ansteuern TEV (0x60CF)
- [STEUERN_ENDE_LSH1](#job-steuern-ende-lsh1) - Lambdasondenheizung vor Kat Bank1 Ansteuerung beenden LSH1 (0x60D0)
- [STEUERN_LSH1](#job-steuern-lsh1) - Lambdasondenheizung vor Kat Bank1 ansteuern LSH1 (0x60D0)
- [STEUERN_ENDE_LSH2](#job-steuern-ende-lsh2) - Lambdasondenheizung hinter Kat Bank1 Ansteuerung beenden LSH2 (0x60D1)
- [STEUERN_LSH2](#job-steuern-lsh2) - Lambdasondenheizung hinter Kat Bank1 ansteuern LSH2 (0x60D1)
- [STEUERN_ENDE_MIL](#job-steuern-ende-mil) - MIL (Malfunction Indicator Lamp) Ansteuerung beenden MIL (0x60D4)
- [STEUERN_MIL](#job-steuern-mil) - MIL (Malfunction Indicator Lamp) ansteuern MIL (0x60D4)
- [STEUERN_EML](#job-steuern-eml) - EML (Engine Malfunction Lamp) ansteuern EML (0x60D6)
- [STEUERN_ENDE_EML](#job-steuern-ende-eml) - EML (Engine Malfunction Lamp) Ansteuerung beenden EML (0x60D6)
- [STEUERN_EKP](#job-steuern-ekp) - Elektrische Kraftstoffpumpe 1 ansteuern Elektrische Kraftstoffpumpe 1 Deaktivierung aufheben EKP (0x60D8)
- [STEUERN_ENDE_EKP](#job-steuern-ende-ekp) - Elektrische Kraftstoffpumpe 1 Ansteuerung beenden Elektrische Kraftstoffpumpe 1 Deaktivierung aufheben EKP (0x60D8)
- [STEUERN_ENDE_E_LUEFTER](#job-steuern-ende-e-luefter) - E-Luefter Ansteuerung beenden E_LUEFTER (0x60DA)
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - E-Luefter ansteuern E_LUEFTER (0x60DA)
- [STEUERN_ENDE_VVT](#job-steuern-ende-vvt) - VVT Ansteuerung beenden VVT (0x60DD)
- [STEUERN_VVT](#job-steuern-vvt) - VVT ansteuern VVT (0x60DD)
- [STEUERN_ENDE_EV1](#job-steuern-ende-ev1) - Einspritzventil 1 (physikalisch) Ansteuerung beenden EV1 (0x60E1)
- [STEUERN_EV1](#job-steuern-ev1) - Einspritzventil 1 (physikalisch) ansteuern EV1 (0x60E1)
- [STEUERN_ENDE_EV2](#job-steuern-ende-ev2) - Einspritzventil 2 (physikalisch) Ansteuerung beenden EV2 (0x60E2)
- [STEUERN_EV2](#job-steuern-ev2) - Einspritzventil 2 (physikalisch) ansteuern EV2 (0x60E2)
- [STEUERN_ENDE_EV3](#job-steuern-ende-ev3) - Einspritzventil 3 (physikalisch) Ansteuerung beenden EV3 (0x60E3)
- [STEUERN_EV3](#job-steuern-ev3) - Einspritzventil 3 (physikalisch) ansteuern EV3 (0x60E3)
- [STEUERN_ENDE_EV4](#job-steuern-ende-ev4) - Einspritzventil 4 (physikalisch) Ansteuerung beenden EV4 (0x60E4)
- [STEUERN_EV4](#job-steuern-ev4) - Einspritzventil 4 (physikalisch) ansteuern EV4 (0x60E4)
- [STEUERN_ENDE_EV5](#job-steuern-ende-ev5) - Einspritzventil 5 (physikalisch) Ansteuerung beenden EV5 (0x60E5)
- [STEUERN_EV5](#job-steuern-ev5) - Einspritzventil 5 (physikalisch) ansteuern EV5 (0x60E5)
- [STEUERN_ENDE_EV6](#job-steuern-ende-ev6) - Einspritzventil 6 (physikalisch) Ansteuerung beenden EV6 (0x60E6)
- [STEUERN_EV6](#job-steuern-ev6) - Einspritzventil 6 (physikalisch) ansteuern EV6 (0x60E6)
- [STEUERN_ENDE_ENWS](#job-steuern-ende-enws) - Vanos Einlass Ventil Ansteuerung beenden ENWS (0x60ED)
- [STEUERN_ENWS](#job-steuern-enws) - Vanos Einlass Ventil ansteuern ENWS (0x60ED)
- [STEUERN_ANWS](#job-steuern-anws) - Vanos Auslass Ventil ansteuern ANWS (0x60EE)
- [STEUERN_ENDE_ANWS](#job-steuern-ende-anws) - Vanos Auslass Ventil Ansteuerung beenden ANWS (0x60EE)
- [STEUERN_ENDE_TEAV](#job-steuern-ende-teav) - Absperrventil Tankentlueftung Ansteuerung beenden TEAV (0x60FC)
- [STEUERN_TEAV](#job-steuern-teav) - Absperrventil Tankentlueftung Ansteuerung TEAV (0x60FC)
- [START_SYSTEMCHECK_TEV](#job-start-systemcheck-tev) - Ansteuern Diagnosefunktion Tankentlueftungsventil SYSTEMCHECK_TEV (0xF022)
- [STATUS_SYSTEMCHECK_TEV](#job-status-systemcheck-tev) - Auslesen Diagnosefunktion Tankentlueftungsventil SYSTEMCHECK_TEV (0xF022)
- [STOP_SYSTEMCHECK_TEV](#job-stop-systemcheck-tev) - Diagnosefunktion Tankentlueftungsventil beenden SYSTEMCHECK_TEV (0xF022)
- [START_SYSTEMCHECK_EVAUSBL](#job-start-systemcheck-evausbl) - Ansteuern Diagnosefunktion Einspritzventilausblendung SYSTEMCHECK_EVAUSBL (0xF025)
- [STATUS_SYSTEMCHECK_EVAUSBL](#job-status-systemcheck-evausbl) - Auslesen Diagnosefunktion EinspritzVentile EV-Ausblendung SYSTEMCHECK_EVAUSBL (0xF025)
- [STOP_SYSTEMCHECK_EVAUSBL](#job-stop-systemcheck-evausbl) - Ende Diagnosefunktion EinspritzVentile EV-Ausblendung SYSTEMCHECK_EVAUSBL (0xF025)
- [START_SYSTEMCHECK_VVT_ANSCHLAG](#job-start-systemcheck-vvt-anschlag) - Ansteuern Diagnosefunktion VVT-Anschlag lernen SYSTEMCHECK_VVT_ANSCHLAG (0xF027)
- [STATUS_SYSTEMCHECK_VVT_ANSCHLAG](#job-status-systemcheck-vvt-anschlag) - Auslesen VVT Anschlag lernen SYSTEMCHECK_VVT_ANSCHLAG (0xF027)
- [STOP_SYSTEMCHECK_VVT_ANSCHLAG](#job-stop-systemcheck-vvt-anschlag) - Diagnosefunktion VVT Anschlag lernen beenden SYSTEMCHECK_VVT_ANSCHLAG (0xF027)
- [START_SYSTEMCHECK_GEN](#job-start-systemcheck-gen) - Diagnosefunktion Generatortest SYSTEMCHECK_GEN (0xF02A)
- [STATUS_SYSTEMCHECK_GEN](#job-status-systemcheck-gen) - Auslesen Diagnosefunktion Generatortest SYSTEMCHECK_GEN (0xF02A)
- [STOP_SYSTEMCHECK_GEN](#job-stop-systemcheck-gen) - Diagnosefunktion Generatortest beenden SYSTEMCHECK_GEN (0xF02A)
- [START_SYSTEMCHECK_ODR](#job-start-systemcheck-odr) - Diagnosefunktion Oeldruckregelung SYSTEMCHECK_ODR (0xF02C)
- [STATUS_SYSTEMCHECK_ODR](#job-status-systemcheck-odr) - Auslesen Diagnosefunktion Oeldruckregelung SYSTEMCHECK_ODR (0xF02C)
- [STOP_SYSTEMCHECK_ODR](#job-stop-systemcheck-odr) - Diagnosefunktion Oeldruckregelung beenden SYSTEMCHECK_ODR (0xF02C)
- [ADAP_SELEKTIV_LOESCHEN](#job-adap-selektiv-loeschen) - Ansteuern Adaptionen selektiv loeschen - Batterietausch ausgeblendet. ADAP_SELEKTIV_LOESCHEN (0xF030)
- [ADAP2_SELEKTIV_LOESCHEN](#job-adap2-selektiv-loeschen) - Ansteuern Adaptionen 2 selektiv loeschen ADAP2_SELEKTIV_LOESCHEN (0xF031)
- [START_SYSTEMCHECK_ZSZ](#job-start-systemcheck-zsz) - Ansteuern Zuendkerze freibrennen (Kalttestspezifisch) SYSTEMCHECK_ZSZ (0xF036)
- [STATUS_SYSTEMCHECK_ZSZ](#job-status-systemcheck-zsz) - Auslesen Zuendkerze freibrennen (Kalttestspezifisch) SYSTEMCHECK_ZSZ (0xF036)
- [STOP_SYSTEMCHECK_ZSZ](#job-stop-systemcheck-zsz) - Ende Zuendkerze freibrennen (Kalttestspezifisch) SYSTEMCHECK_ZSZ (0xF036)
- [START_SYSTEMCHECK_ZSZW](#job-start-systemcheck-zszw) - Ansteuern betriebspunktunabhaengiger (Winkelsynchroner) Zuenspulentest (Kalttestspezifisch) SYSTEMCHECK_ZSZW (0xF037)
- [STATUS_SYSTEMCHECK_ZSZW](#job-status-systemcheck-zszw) - Auslesen betriebspunktunabhaengiger (Winkelsynchroner) Zuenspulentest (Kalttestspezifisch) SYSTEMCHECK_ZSZW (0xF037)
- [STOP_SYSTEMCHECK_ZSZW](#job-stop-systemcheck-zszw) - Ende betriebspunktunabhaengiger (Winkelsynchroner) Zuenspulentest (Kalttestspezifisch) SYSTEMCHECK_ZSZW (0xF037)
- [START_SYSTEMCHECK_EVZ](#job-start-systemcheck-evz) - Ansteuern Sequentieller EV-Zylinderabfolgetest (Kalttestspezifisch) SYSTEMCHECK_EVZ (0xF038)
- [STATUS_SYSTEMCHECK_EVZ](#job-status-systemcheck-evz) - Auslesen Sequentieller EV-Zylinderabfolgetest (Kalttestspezifisch) SYSTEMCHECK_EVZ (0xF038)
- [STOP_SYSTEMCHECK_EVZ](#job-stop-systemcheck-evz) - Ende Sequentieller EV-Zylinderabfolgetest (Kalttestspezifisch) SYSTEMCHECK_EVZ (0xF038)
- [START_SYSTEMCHECK_ZSZZ](#job-start-systemcheck-zszz) - Ansteuern Zeitbasierte Zuendsequenz (Kalttestspezifisch) SYSTEMCHECK_ZSZZ (0xF039)
- [STATUS_SYSTEMCHECK_ZSZZ](#job-status-systemcheck-zszz) - Auslesen Zeitbasierte Zuendsequenz (Kalttestspezifisch) SYSTEMCHECK_ZSZZ (0xF039)
- [STOP_SYSTEMCHECK_ZSZZ](#job-stop-systemcheck-zszz) - Ende Zeitbasierte Zuendsequenz (Kalttestspezifisch) SYSTEMCHECK_ZSZZ (0xF039)
- [START_ZWDIAG](#job-start-zwdiag) - CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Start-Routine ZWDIAG (0xF03A)
- [STATUS_ZWDIAG](#job-status-zwdiag) - CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Status-Routine ZWDIAG (0xF03A)
- [STOP_ZWDIAG](#job-stop-zwdiag) - CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Stop-Routine ZWDIAG (0xF03A)
- [START_VANOSSPUELEN](#job-start-vanosspuelen) - VANOS Spuelen fuer OBD und PVE. VANOSSPUELEN (0xF042)
- [STATUS_VANOSSPUELEN](#job-status-vanosspuelen) - VANOS Spuelen fuer OBD und PVE. VANOSSPUELEN (0xF042)
- [STOP_VANOSSPUELEN](#job-stop-vanosspuelen) - VANOS Spuelen fuer OBD und PVE. VANOSSPUELEN (0xF042)
- [START_SYSTEMCHECK_ATL](#job-start-systemcheck-atl) - Diagnosefunktion Abgasturbolader starten SYSTEMCHECK_ATL (0xF0D0)
- [STATUS_SYSTEMCHECK_ATL](#job-status-systemcheck-atl) - Diagnosefunktion Abgasturbolader auslesen SYSTEMCHECK_ATL (0xF0D0)
- [STOP_SYSTEMCHECK_ATL](#job-stop-systemcheck-atl) - Diagnosefunktion Abgasturbolader beenden SYSTEMCHECK_ATL (0xF0D0)
- [START_SYSTEMCHECK_GLF](#job-start-systemcheck-glf) - Ansteuern Gesteuerte Luftfuehrung Systemcheck SYSTEMCHECK_GLF (0xF0D5)
- [STATUS_SYSTEMCHECK_GLF](#job-status-systemcheck-glf) - Auslesen Gesteuerte Luftfuehrung Systemcheck SYSTEMCHECK_GLF (0xF0D5)
- [STOP_SYSTEMCHECK_GLF](#job-stop-systemcheck-glf) - Ende Gesteuerte Luftfuehrung Systemcheck SYSTEMCHECK_GLF (0xF0D5)
- [START_SYSTEMCHECK_L_REGELUNG_AUS](#job-start-systemcheck-l-regelung-aus) - Ansteuerung Lambdaregelung deaktivieren SYSTEMCHECK_L_REGELUNG_AUS (0xF0D9)
- [STATUS_SYSTEMCHECK_L_REGELUNG_AUS](#job-status-systemcheck-l-regelung-aus) - Auslesen Lambdaregelung ausschalten SYSTEMCHECK_L_REGELUNG_AUS (0xF0D9)
- [STOP_SYSTEMCHECK_L_REGELUNG_AUS](#job-stop-systemcheck-l-regelung-aus) - Ende Lambdaregelung ausschalten SYSTEMCHECK_L_REGELUNG_AUS (0xF0D9)
- [START_SYSTEMCHECK_DMTL](#job-start-systemcheck-dmtl) - Ansteuern Diagnosefunktion DMTL SYSTEMCHECK_DMTL (0xF0DA)
- [STATUS_SYSTEMCHECK_DMTL](#job-status-systemcheck-dmtl) - Auslesen Diagnosefunktion DMTL SYSTEMCHECK_DMTL (0xF0DA)
- [STOP_SYSTEMCHECK_DMTL](#job-stop-systemcheck-dmtl) - Diagnosefunktion DMTL beenden SYSTEMCHECK_DMTL (0xF0DA)
- [START_EISYUGD](#job-start-eisyugd) - Ansteuern Eisy-Adaptionswerte (ungedrosselt) (Anforderung aus CP5403) EISYUGD (0xF0E0)
- [STATUS_EISYUGD](#job-status-eisyugd) - Auslesen Eisy-Adaptionswerte (ungedrosselt) (Anforderung aus CP5403) EISYUGD (0xF0E0)
- [START_EISYGD](#job-start-eisygd) - Ansteuern Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403) EISYGD (0xF0E1)
- [STATUS_EISYGD](#job-status-eisygd) - Auslesen Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403) EISYGD (0xF0E1)
- [START_KLANN](#job-start-klann) - Ansteuern Klann-Adaptionswerte (Anforderung aus CP10798) KLANN (0xF0E4)
- [STATUS_KLANN](#job-status-klann) - Auslesen Klann-Adaptionswerte (Anforderung aus CP10798) KLANN (0xF0E4)
- [START_DDLSHK](#job-start-ddlshk) - Ansteuern Dynamik Diagnose Lamdasonden hinter Hauptkat DDLSHK (0xF0E7)
- [STATUS_DDLSHK](#job-status-ddlshk) - Auslesen Dynamik Diagnose Lamdasonden hinter Hauptkat DDLSHK (0xF0E7)
- [STOP_DDLSHK](#job-stop-ddlshk) - Ende Dynamik Diagnose Lamdasonden hinter Hauptkat DDLSHK (0xF0E7)
- [START_CRAM](#job-start-cram) - Ansteuern RAM-Backup-Werte loeschen CRAM (0xF0E9)
- [STATUS_CRAM](#job-status-cram) - Auslesen RAM-Backup-Werte loeschen CRAM (0xF0E9)
- [START_SYSTEMCHECK_DKAT](#job-start-systemcheck-dkat) - Ansteuern Kurztest Kat SYSTEMCHECK_DKAT (0xF0EB)
- [STATUS_SYSTEMCHECK_DKAT](#job-status-systemcheck-dkat) - Auslesen Kurztest Kat SYSTEMCHECK_DKAT (0xF0EB)
- [STOP_SYSTEMCHECK_DKAT](#job-stop-systemcheck-dkat) - Ende Kurztest Kat SYSTEMCHECK_DKAT (0xF0EB)
- [START_RAM](#job-start-ram) - Ansteuern RAM Backup zwangssichern RAM (0xF0F2)
- [STATUS_RAM](#job-status-ram) - Auslesen RAM Backup zwangssichern RAM (0xF0F2)
- [START_SYSTEMCHECK_PM_MESSEMODE](#job-start-systemcheck-pm-messemode) - Ansteuern Messemode SYSTEMCHECK_PM_MESSEMODE (0xF0F6)
- [STATUS_SYSTEMCHECK_PM_MESSEMODE](#job-status-systemcheck-pm-messemode) - Auslesen Messemode SYSTEMCHECK_PM_MESSEMODE (0xF0F6)
- [STOP_SYSTEMCHECK_PM_MESSEMODE](#job-stop-systemcheck-pm-messemode) - Ende Messemode SYSTEMCHECK_PM_MESSEMODE (0xF0F6)

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

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers Fuer UDS immer 3 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC table FOrtTexte EREIGNIS_DTC |
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
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_UEBERLAUF | int | 0: Kein Ueberlauf des Fehlerspeichers 1: Ueberlauf des Fehlerspeichers |
| F_FEHLERKLASSE_NR | int | 0: Keine Fehlerklasse verfuegbar 1: Ueberpruefung bei naechstem Werkstattbesuch 2: Ueberpruefung bei naechstem Halt 4: Ueberpruefung sofort erforderlich ! |
| F_FEHLERKLASSE_TEXT | string | Ausgabe der Fehlerklasse als Text table Fehlerklasse TEXT |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| F_UW_KM | long | Umweltbedingung Kilometerstand (3 Byte) Wertebereich: 0 - 16777215 km -1, wenn Kilometerstand nicht zur Verfuegung steht |
| F_UW_ZEIT | long | Umweltbedingung Absolute Zeit (4 Byte) Genauigkeit: in Sekunden -1, wenn Absolute Zeit nicht zur Verfuegung steht |
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

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Infospeicher loeschen UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $0F06 ClearSecondaryDTCMemory Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
| SENSOR_HERSTELLER_TEXT | string | Textausgabe Lieferant wenn Softwarestand nicht verfuegbar, dann 'Information nicht verfuegbar' |
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

CBS Daten Zuruecksetzen (fuer CBS-Version 5) UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CBS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, Sic, Sic_v, TUV, AU, Ueb, Efk Werte externe Umfaenge: Oel, NOx_a, Br_v, Br_h Defaultwert: 0x00 (ungueltig) |
| CBS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, keine Aenderung: 255 Defaultwert: 100 |
| CBS_ANZAHL_SERVICE | int | Anzahl der durchgefuehrten Services: 0-30 Schalter, Erhoehung der Anzahl um +1: 31 Defaultwert: 31 |
| CBS_ZIEL_MONAT | int | Ziel-Monat (HU/AU) Januar-Dezember: 1-12 Schalter, keine Aenderung: 255 Defaultwert: 255 |
| CBS_ZIEL_JAHR | int | Ziel-Jahr (HU/AU) 2000-2239: 0-239 Schalter, keine Aenderung: 255 Defaultwert: 255 |
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

Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-roe-report"></a>
### STATUS_ROE_REPORT

Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $04 report activated events

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ROE_AKTIV | char | 0x00  = Aktive Fehlermeldung deaktiviert 0x01  = Aktive Fehlermeldung aktiviert 0xFF = Status der aktiven Fehlermeldung nicht feststellbar |
| STAT_ROE_AKTIV_TEXT | string | Interpretation von STAT_ROE_AKTIV table UDS_TAB_ROE_AKTIV TEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-start"></a>
### STEUERN_ROE_START

Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-persistent-stop"></a>
### STEUERN_ROE_PERSISTENT_STOP

Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-roe-persistent-start"></a>
### STEUERN_ROE_PERSISTENT_START

Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime)

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
| CPS | string | Codierpruefstempel 7-stellig |
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
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_UEBERLAUF | int | 0: Kein Ueberlauf des Fehlerspeichers 1: Ueberlauf des Fehlerspeichers |
| F_FEHLERKLASSE_NR | int | 0: Keine Fehlerklasse verfuegbar 1: Ueberpruefung bei naechstem Werkstattbesuch 2: Ueberpruefung bei naechstem Halt 4: Ueberpruefung sofort erforderlich ! |
| F_FEHLERKLASSE_TEXT | string | Ausgabe der Fehlerklasse als Text table Fehlerklasse TEXT |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...) existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| F_UW_KM | long | Umweltbedingung Kilometerstand (3 Byte) Wertebereich: 0 - 16777215 km -1, wenn Kilometerstand nicht zur Verfuegung steht |
| F_UW_ZEIT | long | Umweltbedingung Absolute Zeit (4 Byte) Genauigkeit: in Sekunden -1, wenn Absolute Zeit nicht zur Verfuegung steht |
| F_SAE_CODE | unsigned int | Wertebereich 0x000000 - 0xFFFFFF externe Tabelle T_SCOD |
| F_SAE_CODE_STRING | string | 5 stelliger Text in der Form 'Sxxxx' |
| F_SAE_CODE_TEXT | string | Text zu F_SAE_CODE |
| _RESPONSE_2000 | binary | Hex-Antwort von SG |
| _RESPONSE_200X | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

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

<a id="job-fs-lesen-permanent"></a>
### FS_LESEN_PERMANENT

permanente Fehler aus Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $15 ReportDTCWithPermanentStatus Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers fuer UDS immer 3 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| F_EREIGNIS_DTC | int | 0: DTC kein Ereignis DTC 1: DTC ist Ereignis DTC table FOrtTexte EREIGNIS_DTC |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table FArtTexte ARTTEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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

<a id="job-messwertblock-lesen"></a>
### MESSWERTBLOCK_LESEN

0x2CF0 MESSWERTBLOCK_LESEN DDLI Messwerte auf Basis Übergabestring aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

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
| STAT_MESSWERT0_STRING | string | String mit 9 signifikanten Stellen |
| STAT_MESSWERT0_TEXT | string | Text der Variablen aus INFO |
| STAT_MESSWERT0_EINH | string | Einheit der Variablen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an  SG Block löschen |
| _TEL_ANTWORT_L | binary | Hex-response von SG Block löschen |
| _TEL_AUFTRAG | binary | Hex-Auftrag an  SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-response von SG Block schreiben |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an  SG Block lesen |
| _TEL_ANTWORT | binary | Hex-response von SG Block lesen |

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

<a id="job-start-systemcheck-llerh"></a>
### START_SYSTEMCHECK_LLERH

Ansteuern Diagnosefunktion Leerlauf-Erhoehung SYSTEMCHECK_LLERH (0xF026)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LL | unsigned long | Drehzahlerhoeung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-llerh"></a>
### STATUS_SYSTEMCHECK_LLERH

Auslesen Diagnosefunktion Leerlauf-Erhoehung SYSTEMCHECK_LLERH (0xF026)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE | unsigned char | Funktionsstatus Diagnosefunktion LL-Erhoehung |
| STAT_DIAGNOSE_TEXT | string | Funktionsstatus Diagnosefunktion LL-Erhoehung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-llerh"></a>
### STOP_SYSTEMCHECK_LLERH

Diagnosefunktion Leerlauf-Erhoehung beenden SYSTEMCHECK_LLERH (0xF026)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bzediag"></a>
### STATUS_BZEDIAG

BZE Infospeicher BZEDIAG (0x403B)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIEKAPAZITAET_AKTUEL_WERT | unsigned char | aktueller Wert C_ist (verfügbare Kapazität) - auf passende Quantisierung angepasst |
| STAT_BATTERIEKAPAZITAET_AKTUEL_EINH | string | "Ah" |
| STAT_BATTERIEKAPAZITAET_VOR_1_MONAT_WERT | unsigned char | C_ist vor 1 Zeiteinheit |
| STAT_BATTERIEKAPAZITAET_VOR_1_MONAT_EINH | string | "Ah" |
| STAT_BATTERIEKAPAZITAET_VOR_2_MONAT_WERT | unsigned char | C_ist vor 2 Zeiteinheiten |
| STAT_BATTERIEKAPAZITAET_VOR_2_MONAT_EINH | string | "Ah" |
| STAT_BATTERIEKAPAZITAET_VOR_3_MONAT_WERT | unsigned char | C_ist vor 3 Zeiteinheiten |
| STAT_BATTERIEKAPAZITAET_VOR_3_MONAT_EINH | string | "Ah" |
| STAT_BATTERIEKAPAZITAET_VOR_4_MONAT_WERT | unsigned char | C_ist vor 4 Zeiteinheiten |
| STAT_BATTERIEKAPAZITAET_VOR_4_MONAT_EINH | string | "Ah" |
| STAT_BATTERIEKAPAZITAET_VOR_5_MONAT_WERT | unsigned char | C_ist vor 5 Zeiteinheiten |
| STAT_BATTERIEKAPAZITAET_VOR_5_MONAT_EINH | string | "Ah" |
| STAT_Q_BATTERIEKAPAZITAET_AKTUEL_WERT | unsigned char | Qualitaetsindex C_ist |
| STAT_Q_BATTERIEKAPAZITAET_AKTUEL_EINH | string | "%" |
| STAT_LADEZUSTAND_AKTUELL_WERT | unsigned char | Aktueller Wert C_akt (Ladezustand)- auf passende Quantisierung angepasst |
| STAT_LADEZUSTAND_AKTUELL_EINH | string | "Ah" |
| STAT_LADEZUSTAND_VOR_1_TAG_WERT | unsigned char | C_akt vor 1 Zeiteinheit |
| STAT_LADEZUSTAND_VOR_1_TAG_EINH | string | "Ah" |
| STAT_LADEZUSTAND_VOR_2_TAG_WERT | unsigned char | C_akt vor 2 Zeiteinheiten |
| STAT_LADEZUSTAND_VOR_2_TAG_EINH | string | "Ah" |
| STAT_LADEZUSTAND_VOR_3_TAG_WERT | unsigned char | C_akt vor 3 Zeiteinheiten |
| STAT_LADEZUSTAND_VOR_3_TAG_EINH | string | "Ah" |
| STAT_LADEZUSTAND_VOR_4_TAG_WERT | unsigned char | C_akt vor 4 Zeiteinheiten |
| STAT_LADEZUSTAND_VOR_4_TAG_EINH | string | "Ah" |
| STAT_LADEZUSTAND_VOR_5_TAG_WERT | unsigned char | C_akt vor 5 Zeiteinheiten |
| STAT_LADEZUSTAND_VOR_5_TAG_EINH | string | "Ah" |
| STAT_Q_SOC_AKTUELL_WERT | unsigned char | Qualitaetsindex C_akt |
| STAT_Q_SOC_AKTUELL_EINH | string | "%" |
| STAT_STROMAUFNAHME_AKTUELL_WERT | unsigned char | normierte Stromaufnahme aktuell |
| STAT_STROMAUFNAHME_AKTUELL_EINH | string | "A" |
| STAT_STROMAUFNAHME_VOR_1_MONAT_WERT | unsigned char | normierte Stromaufnahme vor 1 Zeiteinheiten |
| STAT_STROMAUFNAHME_VOR_1_MONAT_EINH | string | "A" |
| STAT_STROMAUFNAHME_VOR_2_MONAT_WERT | unsigned char | normierte Stromaufnahme vor 2 Zeiteinheiten |
| STAT_STROMAUFNAHME_VOR_2_MONAT_EINH | string | "A" |
| STAT_STROMAUFNAHME_VOR_3_MONAT_WERT | unsigned char | normierte Stromaufnahme vor 3 Zeiteinheiten |
| STAT_STROMAUFNAHME_VOR_3_MONAT_EINH | string | "A" |
| STAT_STROMAUFNAHME_VOR_4_MONAT_WERT | unsigned char | normierte Stromaufnahme vor 4 Zeiteinheiten |
| STAT_STROMAUFNAHME_VOR_4_MONAT_EINH | string | "A" |
| STAT_STROMAUFNAHME_VOR_5_MONAT_WERT | unsigned char | normierte Stromaufnahme vor 5 Zeiteinheiten |
| STAT_STROMAUFNAHME_VOR_5_MONAT_EINH | string | "A" |
| STAT_Q_STROMAUFNAHME_AKTUELL_WERT | unsigned char | Qualitaetsindex normierte Stromaufnahme |
| STAT_Q_STROMAUFNAHME_AKTUELL_EINH | string | "%" |
| STAT_Q_BATTERIEZELLE_DEFEKT_WERT | unsigned char | Zelldefekt-Signal als Quali-Index |
| STAT_Q_BATTERIEZELLE_DEFEKT_EINH | string | "%" |
| STAT_ANZ_BATTERIEWECHSEL_WERT | unsigned char | Anzahl der bisher getaetigten Batteriewechsel (0 = Originalbatterie) |
| STAT_LETZTER_BATTERIEWECHSEL | unsigned char | Anzeige, ob unzulaessiger Batteriewechsel durchgefuehrt wurde (C_nenn wird kleiner, oder AGM --&gt; Nass) |
| STAT_LETZTER_BATTERIEWECHSEL_TEXT | string | Anzeige, ob unzulaessiger Batteriewechsel durchgefuehrt wurde (C_nenn wird kleiner, oder AGM --&gt; Nass) |
| STAT_BATTERIEZUSTAND | unsigned char | Zustand der Batterie / Tauschempfehlung |
| STAT_BATTERIEZUSTAND_TEXT | string | Zustand der Batterie / Tauschempfehlung |
| STAT_WASSERVERLUST | unsigned char | Anzeige Wasserverlust ueberschreitet Grenzwert |
| STAT_WASSERVERLUST_TEXT | string | Anzeige Wasserverlust ueberschreitet Grenzwert |
| STAT_TIEFENTLADEN | unsigned char | Anzeige Batterie wurde tiefentladen |
| STAT_TIEFENTLADEN_TEXT | string | Anzeige Batterie wurde tiefentladen |
| STAT_IBS_BZE | unsigned char | Gibt an, ob eine IBS mit BZE3 erkannt wurde und die BZE-Daten somit relevant sind. |
| STAT_IBS_BZE_TEXT | string | Gibt an, ob eine IBS mit BZE3 erkannt wurde und die BZE-Daten somit relevant sind. |
| STAT_PROGNOSE_KALTSTART_SOMMER_U_WERT | real | Praedizierter Klemmspannungswert Kaltstart Sommer |
| STAT_PROGNOSE_KALTSTART_SOMMER_U_EINH | string | "V" |
| STAT_PROGNOSE_KALTSTART_WINTER_U_WERT | real | Praedizierter Klemmspannungswert Kaltstart Winter |
| STAT_PROGNOSE_KALTSTART_WINTER_U_EINH | string | "V" |
| STAT_PROGNOSE_WARMSTART_U_WERT | real | Praedizierter Klemmspannungswert Warmstart |
| STAT_PROGNOSE_WARMSTART_U_EINH | string | "V" |
| STAT_PROGNOSE_WARMSTART_SOWI_U_WERT | real | Vorhalt praedizierter Klemmspannungswert Warmstart Sommer/Winter |
| STAT_PROGNOSE_WARMSTART_SOWI_U_EINH | string | "V" |
| STAT_TREND_KALTSTART_SOMMER_U_WERT | real | Trendwert Klemmspannungsprognose Kaltstart Sommer |
| STAT_TREND_KALTSTART_SOMMER_U_EINH | string | "V" |
| STAT_TREND_KALTSTART_WINTER_U_WERT | real | Trendwert Klemmspannungsprognose Kaltstart Winter |
| STAT_TREND_KALTSTART_WINTER_U_EINH | string | "V" |
| STAT_TREND_WARMSTART_U_WERT | real | Trendwert Klemmspannungsprognose Warmstart |
| STAT_TREND_WARMSTART_U_EINH | string | "V" |
| STAT_TREND_WARMSTART_SOWI_U_WERT | real | Vorhalt Trendwert Klemmspannungsprognose Warmstart Sommer/Winter |
| STAT_TREND_WARMSTART_SOWI_U_EINH | string | "V" |
| STAT_BATTERIETEMPERATUR_MIN_AKTUELL_WERT | real | Klimaprofil: Wert vor 0 Monaten |
| STAT_BATTERIETEMPERATUR_MIN_AKTUELL_EINH | string | "C" |
| STAT_BATTERIETEMPERATUR_MIN_VOR_1_MONAT_WERT | real | Klimaprofil: Wert vor 1 Monat |
| STAT_BATTERIETEMPERATUR_MIN_VOR_1_MONAT_EINH | string | "C" |
| STAT_BATTERIETEMPERATUR_MIN_VOR_2_MONAT_WERT | real | Klimaprofil: Wert vor 2 Monaten |
| STAT_BATTERIETEMPERATUR_MIN_VOR_2_MONAT_EINH | string | "C" |
| STAT_BATTERIETEMPERATUR_MIN_VOR_3_MONAT_WERT | real | Klimaprofil: Wert vor 3 Monaten |
| STAT_BATTERIETEMPERATUR_MIN_VOR_3_MONAT_EINH | string | "C" |
| STAT_BATTERIETEMPERATUR_MIN_VOR_4_MONAT_WERT | real | Klimaprofil: Wert vor 4 Monaten |
| STAT_BATTERIETEMPERATUR_MIN_VOR_4_MONAT_EINH | string | "C" |
| STAT_BATTERIETEMPERATUR_MIN_VOR_5_MONAT_WERT | real | Klimaprofil: Wert vor 5 Monaten |
| STAT_BATTERIETEMPERATUR_MIN_VOR_5_MONAT_EINH | string | "C" |
| STAT_BATTERIETEMPERATUR_MIN_VOR_6_MONAT_WERT | real | Klimaprofil: Wert vor 6 Monaten |
| STAT_BATTERIETEMPERATUR_MIN_VOR_6_MONAT_EINH | string | "C" |
| STAT_BATTERIETEMPERATUR_MIN_VOR_7_MONAT_WERT | real | Klimaprofil: Wert vor 7 Monaten |
| STAT_BATTERIETEMPERATUR_MIN_VOR_7_MONAT_EINH | string | "C" |
| STAT_BATTERIETEMPERATUR_MIN_VOR_8_MONAT_WERT | real | Klimaprofil: Wert vor 8 Monaten |
| STAT_BATTERIETEMPERATUR_MIN_VOR_8_MONAT_EINH | string | "C" |
| STAT_BATTERIETEMPERATUR_MIN_VOR_9_MONAT_WERT | real | Klimaprofil: Wert vor 9 Monaten |
| STAT_BATTERIETEMPERATUR_MIN_VOR_9_MONAT_EINH | string | "C" |
| STAT_BATTERIETEMPERATUR_MIN_VOR_10_MONAT_WERT | real | Klimaprofil: Wert vor 10 Monaten |
| STAT_BATTERIETEMPERATUR_MIN_VOR_10_MONAT_EINH | string | "C" |
| STAT_BATTERIETEMPERATUR_MIN_VOR_11_MONAT_WERT | real | Klimaprofil: Wert vor 11 Monaten |
| STAT_BATTERIETEMPERATUR_MIN_VOR_11_MONAT_EINH | string | "C" |
| STAT_WASSERVERLUSTABS_WERT | real | Wasserverlust |
| STAT_STANDZEIT_LADEZUSTAND_NIEDRIG_AKTUELL_WERT | unsigned int | Vorhalt Sulfatierungsrate (Standzeit bei niedrigem Ladezustand) seit letztem fahrt |
| STAT_STANDZEIT_LADEZUSTAND_NIEDRIG_GESAMT_WERT | unsigned int | Vorhalt Sulfatierungsindex (Standzeit in niedrigem Ladezustand) fahrzeugslebendauer |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIEKAPAZITAET_WERT | unsigned int | Absolutzeit juengster Historieneintrag C_ist |
| STAT_ZEIT_LETZTER_EINTRAG_LADEZUSTAND_WERT | unsigned int | Absolutzeit juengster Historieneintrag C_akt |
| STAT_ZEIT_LETZTER_EINTRAG_STROMAUFNAHME_WERT | unsigned int | Absolutzeit juengster Historieneintrag normierte Stromaufnahme |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIETEMPERATUR_WERT | unsigned int | Absolutzeit juengster Historieneintrag Klima |
| STAT_ZEIT_LETZTE_TRENDWERTERMITTLUNG_WERT | unsigned int | Absolutzeit letzte Trendwertermittlung |
| STAT_ZEIT_SEIT_LETZTEM_BATTERIEWECHSEL_WERT | unsigned int | Zeit seit letztem Batterietausch |
| STAT_ENTLADUNG_MOTOR_AUS_KLEINER_MINUS10AH_WERT | unsigned int | Entladung waehrend Motor aus &lt; -10Ah (Ladung) |
| STAT_ENTLADUNG_MOTOR_AUS_KLEINER_MINUS10AH_EINH | string | "Ah" |
| STAT_ENTLADUNG_MOTOR_AUS_MINUS10AH_BIS_0AH_WERT | unsigned int | Entladung waehrend Motor aus zwischen -10Ah und 0Ah (Ladung) |
| STAT_ENTLADUNG_MOTOR_AUS_MINUS10AH_BIS_0AH_EINH | string | "Ah" |
| STAT_ENTLADUNG_MOTOR_AUS_0AH_BIS_5AH_WERT | unsigned int | Entladung waehrend Motor aus zwischen 0Ah und 5Ah |
| STAT_ENTLADUNG_MOTOR_AUS_0AH_BIS_5AH_EINH | string | "Ah" |
| STAT_ENTLADUNG_MOTOR_AUS_5AH_BIS_10AH_WERT | unsigned int | Entladung waehrend Motor aus zwischen 5Ah und 10Ah |
| STAT_ENTLADUNG_MOTOR_AUS_5AH_BIS_10AH_EINH | string | "Ah" |
| STAT_ENTLADUNG_MOTOR_AUS_10AH_BIS_15AH_WERT | unsigned int | Entladung waehrend Motor aus zwischen 10Ah und 15Ah |
| STAT_ENTLADUNG_MOTOR_AUS_10AH_BIS_15AH_EINH | string | "Ah" |
| STAT_ENTLADUNG_MOTOR_AUS_15AH_BIS_25AH_WERT | unsigned int | Entladung waehrend Motor aus zwischen 15Ah und 25Ah |
| STAT_ENTLADUNG_MOTOR_AUS_15AH_BIS_25AH_EINH | string | "Ah" |
| STAT_ENTLADUNG_MOTOR_AUS_25AH_BIS_50AH_WERT | unsigned int | Entladung waehrend Motor aus zwischen 25Ah und 50Ah |
| STAT_ENTLADUNG_MOTOR_AUS_25AH_BIS_50AH_EINH | string | "Ah" |
| STAT_ENTLADUNG_MOTOR_AUS_GROESSER_50AH_WERT | unsigned int | Entladung waehrend Motor aus &gt; 50Ah |
| STAT_ENTLADUNG_MOTOR_AUS_GROESSER_50AH_EINH | string | "Ah" |
| STAT_LADUNG_MOTOR_EIN_KLEINER_MINUS20AH_WERT | unsigned int | Ladung waehrend Motor ein &lt; -20Ah (Entladung) |
| STAT_LADUNG_MOTOR_EIN_KLEINER_MINUS20AH_EINH | string | "Ah" |
| STAT_LADUNG_MOTOR_EIN_MINUS20AH_BIS_MINUS10AH_WERT | unsigned int | Ladung waehrend Motor ein zwischen -20Ah und -10Ah (Entladung) |
| STAT_LADUNG_MOTOR_EIN_MINUS20AH_BIS_MINUS10AH_EINH | string | "Ah" |
| STAT_LADUNG_MOTOR_EIN_MINUS10AH_BIS_0AH_WERT | unsigned int | Ladung waehrend Motor ein zwischen -10Ah und 0Ah (Entladung) |
| STAT_LADUNG_MOTOR_EIN_MINUS10AH_BIS_0AH_EINH | string | "Ah" |
| STAT_LADUNG_MOTOR_EIN_0AH_BIS_10AH_WERT | unsigned int | Ladung waehrend Motor ein zwischen 0Ah und 10Ah |
| STAT_LADUNG_MOTOR_EIN_0AH_BIS_10AH_EINH | string | "Ah" |
| STAT_LADUNG_MOTOR_EIN_10AH_BIS_20AH_WERT | unsigned int | Ladung waehrend Motor ein zwischen 10Ah und 20Ah |
| STAT_LADUNG_MOTOR_EIN_10AH_BIS_20AH_EINH | string | "Ah" |
| STAT_LADUNG_MOTOR_EIN_GROESSER_20AH_WERT | unsigned int | Ladung waehrend Motor ein &gt; 20Ah |
| STAT_LADUNG_MOTOR_EIN_GROESSER_20AH_EINH | string | "Ah" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-messwerte"></a>
### STATUS_MESSWERTE

Messwerte auslesen MESSWERTE (0x4000)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LR1_MW_WERT | real | Lambdaregler 1 |
| STAT_LR2_MW_WERT | real | Lambdaregler 2 (für den Biturbo vorgesehen) |
| STAT_VFZG_MW_WERT | real | Fahrzeuggeschwindigkeit |
| STAT_VFZG_MW_EINH | string | "km/h" |
| STAT_NMOT_W_MW_WERT | real | Motordrehzahl hoch aufgeloest |
| STAT_NMOT_W_MW_EINH | string | "1/min" |
| STAT_NSOL_MW_WERT | real | Leerlauf-Solldrehzahl |
| STAT_NSOL_MW_EINH | string | "1/min" |
| STAT_CAM_IN_WERT | real | Istwert Einlassnockenwellensteller |
| STAT_CAM_IN_EINH | string | "Grad KW" |
| STAT_CAM_EX_WERT | real | Istwert Auslassnockenwellensteller |
| STAT_CAM_EX_EINH | string | "Grad KW" |
| STAT_TIA_WERT | real | Ansauglufttemperatur |
| STAT_TIA_EINH | string | "Grad C" |
| STAT_TCO_MES_WERT | real | Kuehlmitteltemperatur Rohwert |
| STAT_TCO_MES_EINH | string | "Grad C" |
| STAT_IGA_IGC_WERT | real | Zuendwinkel Zylinder 1 |
| STAT_IGA_IGC_EINH | string | "Grad KW" |
| STAT_TPS_AV_1_WERT | real | Drosselklappenwinkel Potentiometer 1 |
| STAT_TPS_AV_1_EINH | string | "%DK" |
| STAT_MAF_KGH_MES_BAS_WERT | real | Gemessene Luftmasse Rohwert |
| STAT_MAF_KGH_MES_BAS_EINH | string | "kg/h" |
| STAT_TQI_AV_WERT | real | aktuelle Drehmomentanforderung |
| STAT_TQI_AV_EINH | string | "Nm" |
| STAT_VB_WERT | real | Batteriespannung |
| STAT_VB_EINH | string | "V" |
| STAT_V_PVS_1_WERT | real | Pedalwertgeber 1 Rohwert |
| STAT_V_PVS_1_EINH | string | "V" |
| STAT_TCO_2_MES_WERT | real | Kuehlmittelauslasstemperatur Rohwert |
| STAT_TCO_2_MES_EINH | string | "Grad C" |
| STAT_NL_0_WERT | real | Spannung Klopfwerte Zylinder 1 (phys) |
| STAT_NL_0_EINH | string | "V" |
| STAT_NL_1_WERT | real | Spannung Klopfwerte Zylinder 5 (phys) |
| STAT_NL_1_EINH | string | "V" |
| STAT_NL_2_WERT | real | Spannung Klopfwerte Zylinder 3 (phys) |
| STAT_NL_2_EINH | string | "V" |
| STAT_NL_3_WERT | real | Spannung Klopfwerte Zylinder 6 (phys) |
| STAT_NL_3_EINH | string | "V" |
| STAT_NL_4_WERT | real | Spannung Klopfwerte Zylinder 2 (phys) |
| STAT_NL_4_EINH | string | "V" |
| STAT_NL_5_WERT | real | Spannung Klopfwerte Zylinder 4 (phys) |
| STAT_NL_5_EINH | string | "V" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dfmonitor"></a>
### STATUS_DFMONITOR

Batterieladezustand auslesen DFMONITOR (0x4001)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AUSGANG_WERT | real | Batterieladezustand |
| STAT_AUSGANG_EINH | string | "%" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-digital-1"></a>
### STATUS_DIGITAL_1

Status Schaltzustaende 1 DIGITAL_1 (0x4002)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AC_EIN | unsigned char | Status Klimabereitschaft |
| STAT_AC_EIN_TEXT | string | Status Klimabereitschaft |
| STAT_BTS_EIN | unsigned char | Status Bremslichtschalter-Kanal 2 |
| STAT_BTS_EIN_TEXT | string | Status Bremslichtschalter-Kanal 2 |
| STAT_BLS_EIN | unsigned char | Status Bremslichtschalter-Kanal 1 |
| STAT_BLS_EIN_TEXT | string | Status Bremslichtschalter-Kanal 1 |
| STAT_KUPPL_EIN | unsigned char | Status Kupplungsschalter |
| STAT_KUPPL_EIN_TEXT | string | Status Kupplungsschalter |
| STAT_MOTOR_AUS | unsigned char | Status Motorzustand |
| STAT_MOTOR_AUS_TEXT | string | Status Motorzustand |
| STAT_KL15_EIN | unsigned char | Status Klemme-15 |
| STAT_KL15_EIN_TEXT | string | Status Klemme-15 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-nockenwelle-adaption"></a>
### STATUS_NOCKENWELLE_ADAPTION

Nockenwellenadationswerte auslesen NOCKENWELLE_ADAPTION (0x4006)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WINKELVERSATZ_ZYL_1_WERT | real | Nullpunktverschiebung fuer die Winkelversatz Diagnose |
| STAT_WINKELVERSATZ_ZYL_1_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_IN_0_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_IN_0_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_IN_1_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_IN_1_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_IN_2_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_IN_2_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_IN_3_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_IN_3_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_IN_4_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_IN_4_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_IN_5_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Einlassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_IN_5_EINH | string | "deg CrS" |
| STAT_WINKELVERSATZ_ZYL_5_WERT | real | Nullpunktverschiebung fuer die Winkelversatz Diagnose |
| STAT_WINKELVERSATZ_ZYL_5_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_EX_0_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Auslassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_EX_0_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_EX_1_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Auslassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_EX_1_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_EX_2_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Auslassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_EX_2_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_EX_3_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Auslassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_EX_3_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_EX_4_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Auslassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_EX_4_EINH | string | "deg CrS" |
| STAT_PSN_EDGE_AD_CAM_EX_5_WERT | real | Adaptierte Referenzposition einer NW-Flanke der Auslassnockenwelle |
| STAT_PSN_EDGE_AD_CAM_EX_5_EINH | string | "deg CrS" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-digital-0"></a>
### STATUS_DIGITAL_0

Status Schaltzustaende 0 DIGITAL_0 (0x4007)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LS1_REGELUNG | unsigned char | Status Regelkreis Bank 1 |
| STAT_LS1_REGELUNG_TEXT | string | Status Regelkreis Bank 1 |
| STAT_LS2_REGELUNG | unsigned char | Status Regelkreis Bank 2 |
| STAT_LS2_REGELUNG_TEXT | string | Status Regelkreis Bank 2 |
| STAT_LSVK1 | unsigned char | Status Lambdaregelung vor Katalysator Bank 1 |
| STAT_LSVK1_TEXT | string | Status Lambdaregelung vor Katalysator Bank 1 |
| STAT_LSVK2 | unsigned char | Status Lambdaregelung vor Katalysator Bank 2 |
| STAT_LSVK2_TEXT | string | Status Lambdaregelung vor Katalysator Bank 2 |
| STAT_LSHK1 | unsigned char | Status Lambdaregelung hinter Katalysator Bank 1 |
| STAT_LSHK1_TEXT | string | Status Lambdaregelung hinter Katalysator Bank 1 |
| STAT_LSHK2 | unsigned char | Status Lambdaregelung hinter Katalysator Bank 2 |
| STAT_LSHK2_TEXT | string | Status Lambdaregelung hinter Katalysator Bank 2 |
| STAT_VL | unsigned char | Status Vollast |
| STAT_VL_TEXT | string | Status Vollast |
| STAT_LL | unsigned char | Status Leerlauf |
| STAT_LL_TEXT | string | Status Leerlauf |
| STAT_DK_ABGLEICH | unsigned char | Status Drosselklappen-Neuabgleich |
| STAT_DK_ABGLEICH_TEXT | string | Status Drosselklappen-Neuabgleich |
| STAT_SCHUBAB | unsigned char | Status Schubabschaltung |
| STAT_SCHUBAB_TEXT | string | Status Schubabschaltung |
| STAT_FAHRSTUFE | unsigned char | Status Fahrstufe |
| STAT_FAHRSTUFE_TEXT | string | Status Fahrstufe |
| STAT_KICKDOWN | unsigned char | Status Kickdownerkennung |
| STAT_KICKDOWN_TEXT | string | Status Kickdownerkennung |
| STAT_SPORT | unsigned char | Sportschalter (a2l: B_pedsport) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-adaption-dk"></a>
### STATUS_ADAPTION_DK

Drosselklappenadaptionswerte auslesen ADAPTION_DK (0x4008)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EV_ADD_WERT | long | Adaption Einstritzventil Offset |
| STAT_EV_ADD_EINH | string | "kg/h" |
| STAT_EV_FAC_WERT | real | Adaption Einspritzventil Faktor |
| STAT_DK_ADD_WERT | long | Adaption Drosselkappe Offset |
| STAT_DK_ADD_EINH | string | "kg/h" |
| STAT_DK_FAC_WERT | real | Adaption Drosselklappe Faktor |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-adaption-gemisch"></a>
### STATUS_ADAPTION_GEMISCH

Gemischadaptionswerte auslesen ADAPTION_GEMISCH (0x400A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FAC_1_WERT | real | Lambda Adaption carried out by customer (multiplicative share) |
| STAT_PWM_UP_1_WERT | real | Heater driver PWM duty cycle acquired also by BSW |
| STAT_PWM_UP_1_EINH | string | "%" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-vvt"></a>
### STATUS_MESSWERTE_VVT

VVT Messwerte auslesen MESSWERTE_VVT (0x400B)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOLLW_VVT_WERT | real | VVT Exzenterwinkel Sollwert |
| STAT_SOLLW_VVT_EINH | string | "Grad" |
| STAT_ISTW_VVT_WERT | real | VVT Exzenterwinkel Istwert |
| STAT_ISTW_VVT_EINH | string | "Grad" |
| STAT_I_VVT_WERT | real | VVT-Stellmotorstrom, Vorzeichen kennzeichnet Bewegungsrichtung |
| STAT_I_VVT_EINH | string | "A" |
| STAT_U_VVT_WERT | real | VVT-Spannung Leitungsversorgung |
| STAT_U_VVT_EINH | string | "V" |
| STAT_SRF_VVT_WERT | real | VVT-SensorRohwert Fuehrungssensor |
| STAT_SRF_VVT_EINH | string | "°" |
| STAT_NOTL_VVT | unsigned char | VVT-Notlaufzustand |
| STAT_NOTL_VVT_TEXT | string | VVT-Notlaufzustand |
| STAT_SUEL_VVT_WERT | unsigned char | VVT-Systemueberlast |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-fasta10"></a>
### FASTA10

FASTA-Messwertblock 10 lesen FASTA10 (0x4015)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BSZSIFNP_WERT | unsigned long | Serviceintervall Betriebsstundenzaehler (bszsifnp_l) |
| STAT_BSZSIFNP_EINH | string | "s" |
| STAT_NMDSFNP_0_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 1 |
| STAT_NMDSFNP_1_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 2 |
| STAT_NMDSFNP_2_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 3 |
| STAT_NMDSFNP_3_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 4 |
| STAT_NMDSFNP_4_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 5 |
| STAT_NMDSFNP_5_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 6 |
| STAT_NMDSFNP_6_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 7 |
| STAT_NMDSFNP_7_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 8 |
| STAT_NMDSFNP_8_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 9 |
| STAT_NMDSFNP_9_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 10 |
| STAT_NMDSFNP_10_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 11 |
| STAT_NMDSFNP_11_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 12 |
| STAT_NMDSFNP_12_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 13 |
| STAT_NMDSFNP_13_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 14 |
| STAT_NMDSFNP_14_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 15 |
| STAT_NMDSFNP_15_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 16 |
| STAT_NMDSFNP_16_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 17 |
| STAT_NMDSFNP_17_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 18 |
| STAT_NMDSFNP_18_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 19 |
| STAT_NMDSFNP_19_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 20 |
| STAT_NMDSFNP_20_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 21 |
| STAT_NMDSFNP_21_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 22 |
| STAT_NMDSFNP_22_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 23 |
| STAT_NMDSFNP_23_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 24 |
| STAT_NMDSFNP_24_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 25 |
| STAT_NMDSFNP_25_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 26 |
| STAT_NMDSFNP_26_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 27 |
| STAT_NMDSFNP_27_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 28 |
| STAT_NMDSFNP_28_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 29 |
| STAT_NMDSFNP_29_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 30 |
| STAT_NMDSFNP_30_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 31 |
| STAT_NMDSFNP_31_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 32 |
| STAT_NMDSFNP_32_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 33 |
| STAT_NMDSFNP_33_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 34 |
| STAT_NMDSFNP_34_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 35 |
| STAT_NMDSFNP_35_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 36 |
| STAT_NMDSFNP_36_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 37 |
| STAT_NMDSFNP_37_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 38 |
| STAT_NMDSFNP_38_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 39 |
| STAT_NMDSFNP_39_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 40 |
| STAT_NMDSFNP_40_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 41 |
| STAT_NMDSFNP_41_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 42 |
| STAT_NMDSFNP_42_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 43 |
| STAT_NMDSFNP_43_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 44 |
| STAT_NMDSFNP_44_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 45 |
| STAT_NMDSFNP_45_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 46 |
| STAT_NMDSFNP_46_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 47 |
| STAT_NMDSFNP_47_WERT | unsigned char | Sekundaeres n/Md-Kennfeld zur Erfassung von Fahrzeugnutzungsprofilen 48 |
| STAT_DFDSPROFLE_0_WERT | unsigned char | Generatorauslastungsprofil 1 |
| STAT_DFDSPROFLE_1_WERT | unsigned char | Generatorauslastungsprofil 2 |
| STAT_DFDSPROFLE_2_WERT | unsigned char | Generatorauslastungsprofil 3 |
| STAT_DFDSPROFLE_3_WERT | unsigned char | Generatorauslastungsprofil 4 |
| STAT_DFDSPROFLE_4_WERT | unsigned char | Generatorauslastungsprofil 5 |
| STAT_DFDSPROFLE_5_WERT | unsigned char | Generatorauslastungsprofil 6 |
| STAT_DFDSPROFLE_6_WERT | unsigned char | Generatorauslastungsprofil 7 |
| STAT_DFDSPROFLE_7_WERT | unsigned char | Generatorauslastungsprofil 8 |
| STAT_DFDSPROFLE_8_WERT | unsigned char | Generatorauslastungsprofil 9 |
| STAT_DFDSPROFLE_9_WERT | unsigned char | Generatorauslastungsprofil 10 |
| STAT_DFDSPROFLE_10_WERT | unsigned char | Generatorauslastungsprofil 11 |
| STAT_DFDSPROFLE_11_WERT | unsigned char | Generatorauslastungsprofil 12 |
| STAT_DFDSPROFLE_12_WERT | unsigned char | Generatorauslastungsprofil 13 |
| STAT_DFDSPROFLE_13_WERT | unsigned char | Generatorauslastungsprofil 14 |
| STAT_DFDSPROFLE_14_WERT | unsigned char | Generatorauslastungsprofil 15 |
| STAT_DFDSPROFLE_15_WERT | unsigned char | Generatorauslastungsprofil 16 |
| STAT_IGENKFNP_WERT | real | Generatorstrom kumuliert |
| STAT_TMOTB1_WERT | real | Kühlmitteltemperatur innerhalb Bereich 1 |
| STAT_TMOTB1_EINH | string | "%" |
| STAT_TMOTB2_WERT | real | Kühlmitteltemperatur innerhalb Bereich 2 |
| STAT_TMOTB2_EINH | string | "%" |
| STAT_TMOTB3_WERT | real | Kühlmitteltemperatur innerhalb Bereich 3 |
| STAT_TMOTB3_EINH | string | "%" |
| STAT_TMOTB4_WERT | real | Kühlmitteltemperatur innerhalb Bereich 4 |
| STAT_TMOTB4_EINH | string | "%" |
| STAT_TMOTB5_WERT | real | Kühlmitteltemperatur innerhalb Bereich 5 |
| STAT_TMOTB5_EINH | string | "%" |
| STAT_TOELB1_WERT | real | Motoröltemperatur innerhalb Bereich 1 |
| STAT_TOELB1_EINH | string | "%" |
| STAT_TOELB2_WERT | real | Motoröltemperatur innerhalb Bereich 2 |
| STAT_TOELB2_EINH | string | "%" |
| STAT_TOELB3_WERT | real | Motoröltemperatur innerhalb Bereich 3 |
| STAT_TOELB3_EINH | string | "%" |
| STAT_TOELB4_WERT | real | Motoröltemperatur innerhalb Bereich 4 |
| STAT_TOELB4_EINH | string | "%" |
| STAT_TOELB5_WERT | real | Motoröltemperatur innerhalb Bereich 5 |
| STAT_TOELB5_EINH | string | "%" |
| STAT_TGETB1_WERT | real | Getriebeöltemperatur innerhalb Bereich 1 |
| STAT_TGETB1_EINH | string | "%" |
| STAT_TGETB2_WERT | real | Getriebeöltemperatur innerhalb Bereich 2 |
| STAT_TGETB2_EINH | string | "%" |
| STAT_TGETB3_WERT | real | Getriebeöltemperatur innerhalb Bereich 3 |
| STAT_TGETB3_EINH | string | "%" |
| STAT_TGETB4_WERT | real | Getriebeöltemperatur innerhalb Bereich 4 |
| STAT_TGETB4_EINH | string | "%" |
| STAT_TGETB5_WERT | real | Getriebeöltemperatur innerhalb Bereich 5 |
| STAT_TGETB5_EINH | string | "%" |
| STAT_TUMGB1_WERT | real | Umgebungstemperatur innerhalb Bereich 1 |
| STAT_TUMGB1_EINH | string | "%" |
| STAT_TUMGB2_WERT | real | Umgebungstemperatur innerhalb Bereich 2 |
| STAT_TUMGB2_EINH | string | "%" |
| STAT_TUMGB3_WERT | real | Umgebungstemperatur innerhalb Bereich 3 |
| STAT_TUMGB3_EINH | string | "%" |
| STAT_TUMGB4_WERT | real | Umgebungstemperatur innerhalb Bereich 4 |
| STAT_TUMGB4_EINH | string | "%" |
| STAT_TUMGB5_WERT | real | Umgebungstemperatur innerhalb Bereich 5 |
| STAT_TUMGB5_EINH | string | "%" |
| STAT_N_STET_WERT | unsigned long | Zähler Anzahl Statistikeinträge |
| STAT_TECU_1_1_WERT | string | Statistikkennfeld Wert 1.1 |
| STAT_TECU_1_1_EINH | string | "HEX" |
| STAT_TECU_1_2_WERT | string | Statistikkennfeld Wert 1.2 |
| STAT_TECU_1_2_EINH | string | "HEX" |
| STAT_TECU_1_3_WERT | string | Statistikkennfeld Wert 1.3 |
| STAT_TECU_1_3_EINH | string | "HEX" |
| STAT_TECU_1_4_WERT | string | Statistikkennfeld Wert 1.4 |
| STAT_TECU_1_4_EINH | string | "HEX" |
| STAT_TECU_1_5_WERT | string | Statistikkennfeld Wert 1.5 |
| STAT_TECU_1_5_EINH | string | "HEX" |
| STAT_TECU_2_1_WERT | string | Statistikkennfeld Wert 2.1 |
| STAT_TECU_2_1_EINH | string | "HEX" |
| STAT_TECU_2_2_WERT | string | Statistikkennfeld Wert 2.2 |
| STAT_TECU_2_2_EINH | string | "HEX" |
| STAT_TECU_2_3_WERT | string | Statistikkennfeld Wert 2.3 |
| STAT_TECU_2_3_EINH | string | "HEX" |
| STAT_TECU_2_4_WERT | string | Statistikkennfeld Wert 2.4 |
| STAT_TECU_2_4_EINH | string | "HEX" |
| STAT_TECU_2_5_WERT | string | Statistikkennfeld Wert 2.5 |
| STAT_TECU_2_5_EINH | string | "HEX" |
| STAT_TECU_3_1_WERT | string | Statistikkennfeld Wert 3.1 |
| STAT_TECU_3_1_EINH | string | "HEX" |
| STAT_TECU_3_2_WERT | string | Statistikkennfeld Wert 3.2 |
| STAT_TECU_3_2_EINH | string | "HEX" |
| STAT_TECU_3_3_WERT | string | Statistikkennfeld Wert 3.3 |
| STAT_TECU_3_3_EINH | string | "HEX" |
| STAT_TECU_3_4_WERT | string | Statistikkennfeld Wert 3.4 |
| STAT_TECU_3_4_EINH | string | "HEX" |
| STAT_TECU_3_5_WERT | string | Statistikkennfeld Wert 3.5 |
| STAT_TECU_3_5_EINH | string | "HEX" |
| STAT_TECU_4_1_WERT | string | Statistikkennfeld Wert 4.1 |
| STAT_TECU_4_1_EINH | string | "HEX" |
| STAT_TECU_4_2_WERT | string | Statistikkennfeld Wert 4.2 |
| STAT_TECU_4_2_EINH | string | "HEX" |
| STAT_TECU_4_3_WERT | string | Statistikkennfeld Wert 4.3 |
| STAT_TECU_4_3_EINH | string | "HEX" |
| STAT_TECU_4_4_WERT | string | Statistikkennfeld Wert 4.4 |
| STAT_TECU_4_4_EINH | string | "HEX" |
| STAT_TECU_4_5_WERT | string | Statistikkennfeld Wert 4.5 |
| STAT_TECU_4_5_EINH | string | "HEX" |
| STAT_TECU_5_1_WERT | string | Statistikkennfeld Wert 5.1 |
| STAT_TECU_5_1_EINH | string | "HEX" |
| STAT_TECU_5_2_WERT | string | Statistikkennfeld Wert 5.2 |
| STAT_TECU_5_2_EINH | string | "HEX" |
| STAT_TECU_5_3_WERT | string | Statistikkennfeld Wert 5.3 |
| STAT_TECU_5_3_EINH | string | "HEX" |
| STAT_TECU_5_4_WERT | string | Statistikkennfeld Wert 5.4 |
| STAT_TECU_5_4_EINH | string | "HEX" |
| STAT_TECU_5_5_WERT | string | Statistikkennfeld Wert 5.5 |
| STAT_TECU_5_5_EINH | string | "HEX" |
| STAT_SSV_NMOT_1_WERT | string | Stützstellenverteilung nmot-1 SG-Temperaturhistogramm (Kennwert STNSG1) |
| STAT_SSV_NMOT_1_EINH | string | "HEX" |
| STAT_SSV_NMOT_2_WERT | string | Stützstellenverteilung nmot-2 SG-Temperaturhistogramm (Kennwert STNSG2) |
| STAT_SSV_NMOT_2_EINH | string | "HEX" |
| STAT_SSV_NMOT_3_WERT | string | Stützstellenverteilung nmot-3 SG-Temperaturhistogramm (Kennwert STNSG3) |
| STAT_SSV_NMOT_3_EINH | string | "HEX" |
| STAT_SSV_NMOT_4_WERT | string | Stützstellenverteilung nmot-4 SG-Temperaturhistogramm (Kennwert STNSG4) |
| STAT_SSV_NMOT_4_EINH | string | "HEX" |
| STAT_SSV_NMOT_5_WERT | string | Stützstellenverteilung nmot-5 SG-Temperaturhistogramm (Kennwert STNSG5) |
| STAT_SSV_NMOT_5_EINH | string | "HEX" |
| STAT_SSV_TSG_1_WERT | string | 1Byte Stützstellenverteilung nmot-1 SG-Temperatur |
| STAT_SSV_TSG_1_EINH | string | "HEX" |
| STAT_SSV_TSG_2_WERT | string | 1Byte Stützstellenverteilung nmot-2 SG-Temperatur |
| STAT_SSV_TSG_2_EINH | string | "HEX" |
| STAT_SSV_TSG_3_WERT | string | 1Byte Stützstellenverteilung nmot-3 SG-Temperatur |
| STAT_SSV_TSG_3_EINH | string | "HEX" |
| STAT_SSV_TSG_4_WERT | string | 1Byte Stützstellenverteilung nmot-4 SG-Temperatur |
| STAT_SSV_TSG_4_EINH | string | "HEX" |
| STAT_SSV_TSG_5_WERT | string | 1Byte Stützstellenverteilung nmot-5 SG-Temperatur |
| STAT_SSV_TSG_5_EINH | string | "HEX" |
| STAT_TINT_SGTH_WERT | unsigned char | 1Byte Zeitintervall für Erfassung SG-Temperatur-Histogramm |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-geninfo"></a>
### STATUS_GENINFO

Infospeicher Generatordiagnose erweitert auslesen GENINFO (0x401B)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DGENUB1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) |
| STAT_DGENUB1_EINH | string | "V" |
| STAT_DGENUB2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) |
| STAT_DGENUB2_EINH | string | "V" |
| STAT_DGENUBNZ_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) |
| STAT_DGENUBNZ_EINH | string | "V" |
| STAT_DGENUBERR_WERT | unsigned char | Fehlerstati zur Batteriespannung |
| STAT_DGENUGEN1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) |
| STAT_DGENUGEN1_EINH | string | "V" |
| STAT_DGENUGEN2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) |
| STAT_DGENUGEN2_EINH | string | "V" |
| STAT_DGENUGENNZ_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) |
| STAT_DGENUGENNZ_EINH | string | "V" |
| STAT_DGENUGENERR_WERT | unsigned char | Fehlerstati zur Generatorsollspannung |
| STAT_DGENGRENZ1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) |
| STAT_DGENGRENZ1_EINH | string | "A" |
| STAT_DGENGRENZ2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) |
| STAT_DGENGRENZ2_EINH | string | "A" |
| STAT_DGENGRENZNZ_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) |
| STAT_DGENGRENZNZ_EINH | string | "A" |
| STAT_DGENGRENZERR_WERT | unsigned char | Fehlerstati zur Erregerstrombegrenzung |
| STAT_DGENUB1_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz |
| STAT_DGENUB1_MD1_EINH | string | "V" |
| STAT_DGENUB2_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz |
| STAT_DGENUB2_MD1_EINH | string | "V" |
| STAT_DGENUBNZ_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz |
| STAT_DGENUBNZ_MD1_EINH | string | "V" |
| STAT_DGENUBERR_MD1_WERT | unsigned char | Fehlerstati zur Batteriespannung zu 1. Messdatensatz |
| STAT_DGENUGEN1_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz |
| STAT_DGENUGEN1_MD1_EINH | string | "V" |
| STAT_DGENUGEN2_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz |
| STAT_DGENUGEN2_MD1_EINH | string | "V" |
| STAT_DGENUGENNZ_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz |
| STAT_DGENUGENNZ_MD1_EINH | string | "V" |
| STAT_DGENUGENERR_MD1_WERT | unsigned char | Fehlerstati zur Generatorsollspannung zu 1. Messdatensatz |
| STAT_DGENGRENZ1_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz |
| STAT_DGENGRENZ1_MD1_EINH | string | "A" |
| STAT_DGENGRENZ2_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz |
| STAT_DGENGRENZ2_MD1_EINH | string | "A" |
| STAT_DGENGRENZNZ_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz |
| STAT_DGENGRENZNZ_MD1_EINH | string | "A" |
| STAT_DGENGRENZERR_MD1_WERT | unsigned char | Fehlerstati zur Erregerstrombegrenzung zu 1. Messdatensatz |
| STAT_DGENUB1_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz |
| STAT_DGENUB1_MD2_EINH | string | "V" |
| STAT_DGENUB2_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz |
| STAT_DGENUB2_MD2_EINH | string | "V" |
| STAT_DGENUBNZ_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz |
| STAT_DGENUBNZ_MD2_EINH | string | "V" |
| STAT_DGENUBERR_MD2_WERT | unsigned char | Fehlerstati zur Batteriespannung zu 2. Messdatensatz |
| STAT_DGENUGEN1_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz |
| STAT_DGENUGEN1_MD2_EINH | string | "V" |
| STAT_DGENUGEN2_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz |
| STAT_DGENUGEN2_MD2_EINH | string | "V" |
| STAT_DGENUGENNZ_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz |
| STAT_DGENUGENNZ_MD2_EINH | string | "V" |
| STAT_DGENUGENERR_MD2_WERT | unsigned char | Fehlerstati zur Generatorsollspannung zu 2. Messdatensatz |
| STAT_DGENGRENZ1_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz |
| STAT_DGENGRENZ1_MD2_EINH | string | "A" |
| STAT_DGENGRENZ2_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz |
| STAT_DGENGRENZ2_MD2_EINH | string | "A" |
| STAT_DGENGRENZNZ_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz |
| STAT_DGENGRENZNZ_MD2_EINH | string | "A" |
| STAT_DGENGRENZERR_MD2_WERT | unsigned char | Fehlerstati zur Erregerstrombegrenzung zu 2. Messdatensatz |
| STAT_DGENERRST_MD1_WERT | unsigned int | Trigger zur Statuswortablage zu 1. Messdatensatz |
| STAT_DGENERRST_MD2_WERT | unsigned int | Trigger zur Statuswortablage zu 2. Messdatensatz |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-ident-ibs"></a>
### IDENT_IBS

Identifikationsdaten fuer IBS-Sensor auslesen IDENT_IBS (0x4021)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ID_BMW_NR | unsigned long | BMW-Teilenummer Intelligenter Batteriesensor |
| SERIENNUMMER | unsigned long | Seriennummer Intelligenter Batteriesensor DEZ Long 4-1 |
| ZIF_PROGRAMMSTAND | unsigned char | Software Baseline Intelligenter Batteriesensor DEZ Byte |
| ZIF_STATUS | unsigned char | Software Index Intelligenter Batteriesensor DEZ Byte |
| HW_REF | unsigned char | Hardware Index Intelligenter Batteriesensor DEZ Byte |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-ewap"></a>
### STATUS_MESSWERTE_EWAP

elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) Messwerte auslesen MESSWERTE_EWAP (0x4024)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_U_EWAP_WERT | real | Pumpenspannung elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) |
| STAT_U_EWAP_EINH | string | "V" |
| STAT_T_EWAP_WERT | real | Pumpentemperatur elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) |
| STAT_I_EWAP_WERT | real | Pumpenstrom elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) |
| STAT_I_EWAP_EINH | string | "%" |
| STAT_ERR_BIT0_EWAP | unsigned char | Error Status Sperrung-Sollwert |
| STAT_ERR_BIT1_EWAP | unsigned char | Error Status Keine Drehzahlueberwachung |
| STAT_ERR_BIT2_EWAP | unsigned char | Error Status Sperrung-Deblockierung |
| STAT_ERR_BIT3_EWAP | unsigned char | Error Status Uebertemperatur |
| STAT_ERR_BIT4_EWAP | unsigned char | Error Status Ueberstrom |
| STAT_ERR_BIT5_EWAP | unsigned char | Error Status Trockenlauf |
| STAT_ERR_BIT6_EWAP | unsigned char | Error Status falsche Versorgungsspannung |
| STAT_ERR_BIT7_EWAP | unsigned char | Error Status Deblockierung aktiv |
| STAT_TMOT_WERT | real | Motortemperatur |
| STAT_TMOT_EINH | string | "Grad C" |
| STAT_UBAT_WERT | real | Batteriespannung |
| STAT_UBAT_EINH | string | "V" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-vad"></a>
### STATUS_MESSWERTE_VAD

Variantenadaptionen auslesen MESSWERTE_VAD (0x4025)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_I_HA_WERT | real | Hinterachsuebersetzung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-rbmmode9"></a>
### STATUS_RBMMODE9

Rate Based Monitoring Mode 9 auslesen (Ausgabe der Werte wie im Scantool Mode 9) RBMMODE9 (0x4026)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OBDCOND_WERT | unsigned int | OBD Monitoring Conditions Encountered Counts (general denominator) |
| STAT_IGNCNTR_WERT | unsigned int | Ignition Counter |
| STAT_CATCOMP1_WERT | unsigned int | Catalyst Monitor Completion Counts Bank 1 (Numerator) |
| STAT_CATCOND1_WERT | unsigned int | Catalyst Monitor Conditions Encountered Counts Bank 1 (Denominator) |
| STAT_CATCOMP2_WERT | unsigned int | Catalyst Monitor Completion Counts Bank 2 (Numerator) |
| STAT_CATCOND2_WERT | unsigned int | Catalyst Monitor Conditions Encountered Counts Bank 2 (Denominator) |
| STAT_O2SCOMP1_WERT | unsigned int | O2 Sensor Monitor Completion Counts Bank 1 (Numerator) |
| STAT_O2SCOND1_WERT | unsigned int | O2 Sensor Monitor Conditions Encountered Counts Bank 1 (Denominator) |
| STAT_O2SCOMP2_WERT | unsigned int | O2 Sensor Monitor Completion Counts Bank 2 (Numerator) |
| STAT_O2SCOND2_WERT | unsigned int | O2 Sensor Monitor Conditions Encountered Counts Bank 2 (Denominator) |
| STAT_EGRCOMP_WERT | unsigned int | EGR Monitor Completion Condition Counts (Numerator) |
| STAT_EGRCOND_WERT | unsigned int | EGR Monitor Conditions Encountered Counts (Denominator) |
| STAT_AIRCOMP1_WERT | unsigned int | AIR Monitor Completion Condition Counts Bank 1 (Secondary Air) (Numerator) |
| STAT_AIRCOND1_WERT | unsigned int | AIR Monitor Conditions Encountered Counts Bank 1 (Secondary Air) (Denominator) |
| STAT_EVAPCOMP_WERT | unsigned int | EVAP Monitor Completion Condition Counts (Numerator) |
| STAT_EVAPCOND_WERT | unsigned int | EVAP Monitor Conditions Encountered Counts (Denominator) |
| STAT_VVTCOMP1_WERT | unsigned int | SO2 Sensor Monitor Completion Condition Counts Bank 1 (Numerator) |
| STAT_VVTCOND1_WERT | unsigned int | SO2 Sensor Monitor Conditions Encountered Counts Bank 1 (Denominator) |
| STAT_VVTCOMP2_WERT | unsigned int | SO2 Sensor Monitor Completion Condition Counts Bank 2 (Numerator) |
| STAT_VVTCOND2_WERT | unsigned int | SO2 Sensor Monitor Conditions Encountered Counts Bank 2 (Denominator) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-rbmme1"></a>
### STATUS_RBMME1

Rate Based Monitoring Motorsteuerung ME... Block 1 auslesen (Vorhalt) RBMME1 (0x4029)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NUM_FID_BHKT_WERT | unsigned int | Katalysator Bank1-Numerator |
| STAT_DEN_FID_BHKT_WERT | unsigned int | Katalysator Bank1-Denumerator |
| STAT_NUM_FID_CDLSU_WERT | unsigned int | LSU dynamisch zu langsam Bank1 Numerator |
| STAT_DEN_FID_CDLSU_WERT | unsigned int | LSU dynamisch zu langsam Bank1-Denumerator |
| STAT_NUM_FID_CULSU_WERT | unsigned int | Spannungsüberwachung LSU Bank1-Numerator |
| STAT_DEN_FID_CULSU_WERT | unsigned int | Spannungsüberwachung LSU Bank1-Denumerator |
| STAT_NUM_FID_CPLSU_WERT | unsigned int | Plausibilität der LSU Bank1-Numerator |
| STAT_DEN_FID_CPLSU_WERT | unsigned int | Plausibilität der LSU Bank1-Denumerator |
| STAT_NUM_FID_ATEVTLD_WERT | unsigned int | TEV-Check mit Tankleckagediagnose aktiv Numerator |
| STAT_DEN_FID_ATEVTLD_WERT | unsigned int | TEV-Check mit Tankleckage aktiv Denumerator |
| STAT_NUM_FID_CTESG_WERT | unsigned int | Tankdiagnose, Grobleck-Numerator |
| STAT_DEN_FID_CTESG_WERT | unsigned int | Tankdiagnose, Grobleck-Denumerator |
| STAT_NUM_FID_CDMTK_WERT | unsigned int | Tankdiagnose, Feinstleck-Numerator |
| STAT_DEN_FID_CDMTK_WERT | unsigned int | Tankdiagnose, Feinstleck-Denumerator |
| STAT_NUM_FID_CDMTL_WERT | unsigned int | Tankdiagnose, Modulfehler-Numerator |
| STAT_DEN_FID_CDMTL_WERT | unsigned int | Tankdiagnose, Modulfehler-Denumerator |
| STAT_NUM_FID_CENWS_WERT | unsigned int | Nockenwellensteuerung Einlass Bank 1-Numerator |
| STAT_DEN_FID_CENWS_WERT | unsigned int | Nockenwellensteuerung Einlass Bank1-Denumerator |
| STAT_NUM_FID_CANWS_WERT | unsigned int | Nockenwellensteuerung Auslass Bank1-Numerator |
| STAT_DEN_FID_CANWS_WERT | unsigned int | Nockenwellensteuerung Auslass Bank 1-Denumerator |
| STAT_NUM_FID_CNWVE_WERT | unsigned int | Nockenwellenverriegelungsdiagnose Einlass Bank1-Numerator |
| STAT_DEN_FID_CNWVE_WERT | unsigned int | Nockenwellenverriegelungsdiagnose Einlass Bank1-Denumerator |
| STAT_NUM_FID_CNWVA_WERT | unsigned int | Nockenwellenverriegelungsdiagnose Auslass Bank1-Numerator |
| STAT_DEN_FID_CNWVA_WERT | unsigned int | Nockenwellenverriegelungsdiagnose Ausass Bank1-Denumerator |
| STAT_NUM_FID_EPMCASOFSERRCASI1_WERT | unsigned int | Zuordnung Einlassnockenwelle zu Kurbelwelle-Numerator |
| STAT_DEN_FID_EPMCASOFSERRCASI1_WERT | unsigned int | Zuordnung Einlassnockenwelle zu Kurbelwelle-Denumerator |
| STAT_NUM_FID_EPMCASOFSERRCASO1_WERT | unsigned int | Zuordnung Auslassnockenwelle zu Kurbelwelle-Numerator |
| STAT_DEN_FID_EPMCASOFSERRCASO1_WERT | unsigned int | Zuordnung Auslassnockenwelle zu Kurbelwelle Numerator |
| STAT_NUM_FID_BLASH_WERT | unsigned int | Lambdasondenalterung hinter KAT-Numerator |
| STAT_DEN_FID_BLASH_WERT | unsigned int | Lambdasondenalterung hinter KAT-Denumerator |
| STAT_NUM_FID_CDYSH_WERT | unsigned int | Diagnose Delay time für O2 Sensor nach Hauptkatalysator-Numerator |
| STAT_DEN_FID_CDYSH_WERT | unsigned int | Diagnose Delay time für O2 Sensor nach Hauptkatalysator-Denumerator |
| STAT_NUM_FID_ADSLS_WERT | unsigned int | Sekundärluftsystem-Numerator |
| STAT_DEN_FID_ADSLS_WERT | unsigned int | Sekundärluftsystem-Denumerator |
| STAT_NUM_FID_CSLSU_WERT | unsigned int | Überwachung des Schubadaptionsfaktors LSU-Numerator |
| STAT_DEN_FID_CSLSU_WERT | unsigned int | Überwachung des Schubadaptionsfaktors LSU-Denumerator |
| STAT_NUM_FID_CTRSH_WERT | unsigned int | Diagnose Transition Time für O2Sensor nach Hauptkat-Numerator |
| STAT_DEN_FID_CTRSH_WERT | unsigned int | Diagnose Transition Time für O2Sensor nach Hauptkat-Denumerator |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-rbmme2"></a>
### STATUS_RBMME2

Rate Based Monitoring Motorsteuerung ME... Block 2 auslesen (Vorhalt) RBMME2 (0x402A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NUM_FID_CCUHR_WERT | unsigned int | CAN relativer Zeitgeber-Numerator |
| STAT_DEN_FID_CCUHR_WERT | unsigned int | CAN relativer Zeitgeber-Denumerator |
| STAT_NUM_FID_CHSHK_WERT | unsigned int | Heizung Lambdasonde hinter KAT-Numerator |
| STAT_DEN_FID_CHSHK_WERT | unsigned int | Heizung Lambdasonde hinter KAT-Denumerator |
| STAT_NUM_FID_CHSV_WERT | unsigned int | Heizung Lamdbasonde vor KAT-Numerator |
| STAT_DEN_FID_CHSV_WERT | unsigned int | Heizung Lambdasonde vor KAT-Denumerator |
| STAT_NUM_FID_BLLRH_WERT | unsigned int | Leerlaufregelung-Numerator |
| STAT_DEN_FID_BLLRH_WERT | unsigned int | Leerlaufregelung-Denumerator |
| STAT_NUM_FID_BLLRKH_WERT | unsigned int | Leerlaufregelung während KAT-Heizen-Numerator |
| STAT_DEN_FID_BLLRKH_WERT | unsigned int | Leerlaufregelung während KAT-Heizen-Denumerator |
| STAT_NUM_FID_CPUR_WERT | unsigned int | Umgebungsdrucksensor Range Check-Numerator |
| STAT_DEN_FID_CPUR_WERT | unsigned int | Umgebungsdrucksensor Range Check-Denumerator |
| STAT_NUM_FID_CTAVDC_WERT | unsigned int | Kaltstartdiagnose Ansauglufttemperatursensor vor DK-Numerator |
| STAT_DEN_FID_CTAVDC_WERT | unsigned int | Kaltstartdiagnose Ansauglufttemperatursensor vor DK-Denumerator |
| STAT_NUM_FID_CTAVDR_WERT | unsigned int | Diagnose Ansauglufttemperatursensor VDK-Denumerator |
| STAT_DEN_FID_CTAVDR_WERT | unsigned int | Diagnose Ansauglufttemperatursensor VDK-Denumerator |
| STAT_NUM_FID_CTANLC_WERT | unsigned int | Kaltstartdiagnose Ansauglufttemperatursensor nach Luftfilter-Numerator |
| STAT_DEN_FID_CTANLC_WERT | unsigned int | Kaltstartdiagnose Ansauglufttemperatursensor nach Luftfilter-Denumerator |
| STAT_NUM_FID_CTANLR_WERT | unsigned int | Diagnsoe Ansauglufttemperatursensor nach Luftfilter-Numerator |
| STAT_DEN_FID_CTANLR_WERT | unsigned int | Diagnose Ansauglufttemperatursensor nach Luftfilter-Denumerator |
| STAT_NUM_FID_CTM_WERT | unsigned int | Motortemperatur TMOT-Numerator |
| STAT_DEN_FID_CTM_WERT | unsigned int | Motortemperatur TMOT-Denumerator |
| STAT_NUM_FID_CTMCS_WERT | unsigned int | Motortemperatur TMOT-Sensor bei Kaltstart-Numerator |
| STAT_DEN_FID_CTMCS_WERT | unsigned int | Motortemperatur TMOT-Sensor bei Kaltstart-Denumerator |
| STAT_NUM_FID_CTUM_WERT | unsigned int | Umgebungstemperatur TUM-Numerator |
| STAT_DEN_FID_CTUM_WERT | unsigned int | Umgebungstemperatur TUM-Denumerator |
| STAT_NUM_FID_CVFZ_WERT | unsigned int | Geschwindigkeitssignal-Numerator |
| STAT_DEN_FID_CVFZ_WERT | unsigned int | Geschwindigkeitssignal-Denumerator |
| STAT_NUM_FID_CDVEF_WERT | unsigned int | DV-E Fehler bei Federprüfung-Numerator |
| STAT_DEN_FID_CDVEF_WERT | unsigned int | V-E Fehler bei Federprüfung-Denumerator |
| STAT_NUM_FID_CDVEL_WERT | unsigned int | DV-E Lageabweichung-Numerator |
| STAT_DEN_FID_CDVEL_WERT | unsigned int | DV-E Lageabweichung-Denumerator |
| STAT_NUM_FID_CDVER_WERT | unsigned int | DV-E Regelbereich-Numerator |
| STAT_DEN_FID_CDVER_WERT | unsigned int | DV-E Regelbereich-Denumerator |
| STAT_NUM_FID_BMW_HFMPL_WERT | unsigned int | Plausibilisierung Luftmassenmesser-Numerator |
| STAT_DEN_FID_BMW_HFMPL_WERT | unsigned int | Plausibilisierung Luftmassenmesser-Denumerator |
| STAT_NUM_FID_BMW_DKPSRPL_WERT | unsigned int | Plausibilisierung Drucksensor Saugrohr-Numerator |
| STAT_DEN_FID_BMW_DKPSRPL_WERT | unsigned int | Plausiblisierung Drucksensor Saugrohr-Denumerator |
| STAT_NUM_FID_CDK_WERT | unsigned int | DK-Potentiometer-Numerator |
| STAT_DEN_FID_CDK_WERT | unsigned int | DK-Potentiometer-Denumerator |
| STAT_NUM_FID_CDK1P_WERT | unsigned int | Drosselklappenpotentiometer 1-Numerator |
| STAT_DEN_FID_CDK1P_WERT | unsigned int | Drosselklappenpotentiometer 1-Denumerator |
| STAT_NUM_FID_CDK2P_WERT | unsigned int | Drosselklappenpotentiometer 2-Numerator |
| STAT_DEN_FID_CDK2P_WERT | unsigned int | Drosselklappenpotentiometer 2-Denumerator |
| STAT_NUM_FID_CKUP_WERT | unsigned int | Pedalwertgeber Kupplung-Numerator |
| STAT_DEN_FID_CKUP_WERT | unsigned int | Pedalwertgeber Kupplung-Denumerator |
| STAT_NUM_FID_CPVDR_WERT | unsigned int | Drucksensor vor Drosselklappe Plausibel Diagnose-Numerator |
| STAT_DEN_FID_CPVDR_WERT | unsigned int | Drucksensor vor Drosselklappe Plausibel Diagnose-Denumerator |
| STAT_NUM_FID_CDSKVR_WERT | unsigned int | Diagnose Hochdrucksensor plausibel-Numerator |
| STAT_DEN_FID_CDSKVR_WERT | unsigned int | Diagnose Hochdrucksensor plausibel-Denumerator |
| STAT_NUM_FID_BMW_DMDKH_WERT | unsigned int | Md-Überwachung bei Katheizen-Numerator |
| STAT_DEN_FID_BMW_DMDKH_WERT | unsigned int | Md-Überwachung bei Katheizen-Denumerator |
| STAT_NUM_FID_CENCS_WERT | unsigned int | Funktion NW Stellerdiagnose-Einlass CERS-Numerator |
| STAT_DEN_FID_CENCS_WERT | unsigned int | Funktion NW Stellerdiagnose-Einlass CERS-Denumerator |
| STAT_NUM_FID_CANCS_WERT | unsigned int | Funktion NW Stellerdiagnose-Auslass CERS-Numerator |
| STAT_DEN_FID_CANCS_WERT | unsigned int | Funktion NW Stellerdiagnose-Auslass CERS-Denumerator |
| STAT_NUM_FID_CHDRKH_WERT | unsigned int | Raildruckregelung während KAT-Heizen CERS-Numerator |
| STAT_DEN_FID_CHDRKH_WERT | unsigned int | Raildruckregelung während KAT-Heizen CERS Denumerator |
| STAT_NUM_FID_CETKHL_WERT | unsigned int | Zündwinkelwirkungsgraddiagnose bei Katheizen(im Leerlauf) CERS-Numerator |
| STAT_DEN_FID_CETKHL_WERT | unsigned int | Zündwinkelwirkungsgraddiagnose bei Katheizen (im Leerlauf) CERS-Denumerator |
| STAT_NUM_FID_CTEOEH_WERT | unsigned int | Diagnose CAN-Uhr ist zu schnell-Numerator |
| STAT_DEN_FID_CTEOEH_WERT | unsigned int | Diagnose CAN-Uhr ist zu schnell-Denumerator |
| STAT_NUM_FID_CTEOEL_WERT | unsigned int | Diagnose CAN-Uhr ist zu langsam-Numerator |
| STAT_DEN_FID_CTEOEL_WERT | unsigned int | Diagnose CAN-Uhr ist zu langsam-Denumerator |
| STAT_NUM_FID_CTEOES_WERT | unsigned int | Diagnose Einseitiger Fehler der CAN-Uhr-Numerator |
| STAT_DEN_FID_CTEOES_WERT | unsigned int | Diagnose Einseitiger Fehler der CAN-Uhr-Denumerator |
| STAT_NUM_FID_CTEOET_WERT | unsigned int | Diagnose Fehler der CAN-Uhr (beidseitiger Check)-Numerator |
| STAT_DEN_FID_CTEOET_WERT | unsigned int | Diagnose Fehler der CAN-Uhr (beidseitiger Check)-Denumerator |
| STAT_NUM_FID_CETKHT_WERT | unsigned int | Zündwinkelwirkungsgraddiagnose bei Katheizen (im Teillastbereich) CERS-Numerator |
| STAT_DEN_FID_CETKHT_WERT | unsigned int | Zündwinkelwirkungsgraddiagnose bei Katheizen (im Teillastbereich) CERS-Denumerator |
| STAT_NUM_FID_BMW_ATLDIAG_WERT | unsigned int | Diagnose Ladedruck-Numerator |
| STAT_DEN_FID_BMW_ATLDIAG_WERT | unsigned int | Diagnose Ladedruck-Denumerator |
| STAT_NUM_FID_HFM_WERT | unsigned int | HFM Diagnose Numerator |
| STAT_DEN_FID_HFM_WERT | unsigned int | HFM Diagnose Denominator |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-lrp"></a>
### STATUS_MESSWERTE_LRP

Messwerte Laufruhepruefung auslesen MESSWERTE_LRP (0x402D)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STVBRVSO_WERT | unsigned int | Statuswort Verbrennungsregelung fuer Service |
| STAT_STVBRVSIN_WERT | unsigned char | Statuswort Verbrennungsregelung vom Tester |
| STAT_STVBRVSNNV_WERT | unsigned char | Statuswort Verbrennungsregelung vom Tester nichtfluechtig |
| STAT_AMO_05_WERT | real | Gesamte DFT 0,5 Motorordnung |
| STAT_AMO_10_WERT | real | Gesamte DFT 1,0 Motorordnung |
| STAT_AMO_15_WERT | real | Gesamte DFT 1,5 Motorordnung |
| STAT_AMO_20_WERT | real | Gesamte DFT 2,0 Motorordnung |
| STAT_EXWKOR_0_WERT | real | Korrekturwinkel Excenterwelle zur Hubkorrektur |
| STAT_EXWKOR_0_EINH | string | "°" |
| STAT_ZYLHUBKOR_0_WERT | unsigned char | Fuer Hubkorrektur ausgewaehlter Zylinder |
| STAT_MINHUB_WERT | real | Tatsaechlich wirksamer Minhub (nach Ein-/Ausblenddungsfaktoren) |
| STAT_MINHUB_EINH | string | "mm" |
| STAT_MINHUBFAK_WERT | real | Faktor Ein-/Ausblendung Minhub ueber Tmot und Nkw |
| STAT_MINHUB_ROH_WERT | real | Minhubrohwert aus Adaption |
| STAT_MINHUB_ROH_EINH | string | "mm" |
| STAT_MINHUBVS_WERT | real | Vorgabe Minhub ueber Tester |
| STAT_MINHUBVS_EINH | string | "mm" |
| STAT_MINHUBVSI_WERT | real | Tatsaechlich wirksamer Minhub aus Verstelleingriff (vor Ein-/Ausblendungsfaktoren) |
| STAT_MINHUBVSI_EINH | string | "mm" |
| STAT_MINHUBVSNV_WERT | real | dauerhaft fest programmierter Minhub |
| STAT_MINHUBVSNV_EINH | string | "mm" |
| STAT_S_VSMNHB | unsigned char | Schalter fuer Testereingriff |
| STAT_S_VSMNHB_TEXT | string | Schalter fuer Testereingriff |
| STAT_S_VSMNHBNV_WERT | unsigned char | Schalter fuer Testereingriff |
| STAT_LURABS_F_0_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (physikalischer Zylinder 1) |
| STAT_LURDIF_F_0_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (physikalischer Zylinder 1) |
| STAT_LURABS_F_1_WERT | real | gefilterte Laufruhedeltas eines Zylinders (physikalischer Zylinder 5) |
| STAT_LURDIF_F_1_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (physikalischer Zylinder 5) |
| STAT_LURABS_F_2_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (physikalischer Zylinder 3) |
| STAT_LURDIF_F_2_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (physikalischer Zylinder 3) |
| STAT_LURABS_F_3_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (physikalischer Zylinder 6) |
| STAT_LURDIF_F_3_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (physikalischer Zylinder 6) |
| STAT_LURABS_F_4_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (physikalischer Zylinder 2) |
| STAT_LURDIF_F_4_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (physikalischer Zylinder 2) |
| STAT_LURABS_F_5_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (physikalischer Zylinder 4) |
| STAT_LURDIF_F_5_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (physikalischer Zylinder 4) |
| STAT_AMO_30_WERT | real | Gesamte DFT 3,0 Motorordnung |
| STAT_EXWKOR_1_WERT | real | Korrekturwinkel Exzenterwelle zur Hubkorrektur. |
| STAT_EXWKOR_1_EINH | string | "°" |
| STAT_ZYLHUBKOR_1_WERT | unsigned char | Für Hubkorrektur ausgewählter Zylinder. |
| STAT_HUBKOR_0_WERT | unsigned char | Hubkorrektur Status. |
| STAT_HUBKOR_1_WERT | unsigned char | Hubkorrektur Status. |
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
| STAT_CVN_WERT | string | CVN auslesen (hier muss die CVN wie bei Mode $09 (PID $06) ausgegeben werden) |
| STAT_CVN_EINH | string | "HEX" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-injad"></a>
### STATUS_INJAD

Injektor Adaptionswerte lesen INJAD (Kleinstmengen-Adaption RB-Umfaenge) INJAD (0x403F)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_F_INJAD_XZYL_YMOD_00_WERT | real | Korrekturfaktor pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: fakkorteadp_w[0]) |
| STAT_F_INJAD_XYZL_YMOD_01_WERT | real | Korrekturfaktor pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: fakkorteadp_w[1]) |
| STAT_F_INJAD_XZYL_YMOD_02_WERT | real | Korrekturfaktor pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: fakkorteadp_w[2]) |
| STAT_F_INJAD_XZYL_YMOD_03_WERT | real | Korrekturfaktor pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: fakkorteadp_w[3]) |
| STAT_F_INJAD_XZYL_YMOD_04_WERT | real | Korrekturfaktor pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: fakkorteadp_w[4]) |
| STAT_F_INJAD_XZYL_YMOD_05_WERT | real | Korrekturfaktor pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: fakkorteadp_w[5]) |
| STAT_F_INJAD_XZYL_YMOD_06_WERT | real | Korrekturfaktor pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: fakkorteadp_w[6]) |
| STAT_F_INJAD_XZYL_YMOD_07_WERT | real | Korrekturfaktor pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: fakkorteadp_w[7]) |
| STAT_F_INJAD_XZYL_YMOD_08_WERT | real | Korrekturfaktor pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: fakkorteadp_w[8]) |
| STAT_F_INJAD_XZYL_YMOD_09_WERT | real | Korrekturfaktor pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: fakkorteadp_w[9]) |
| STAT_F_INJAD_XZYL_YMOD_10_WERT | real | Korrekturfaktor pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: fakkorteadp_w[10]) |
| STAT_F_INJAD_XZYL_YMOD_11_WERT | real | Korrekturfaktor pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: fakkorteadp_w[11]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_00_WERT | real | Korrekturoffset pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: tiofsinjad_w[0]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_00_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_01_WERT | real | Korrekturoffset pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: tiofsinjad_w[1]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_01_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_02_WERT | real | Korrekturoffset pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: tiofsinjad_w[2]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_02_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_03_WERT | real | Korrekturoffset pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: tiofsinjad_w[3]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_03_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_04_WERT | real | Korrekturoffset pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: tiofsinjad_w[4]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_04_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_05_WERT | real | Korrekturoffset pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: tiofsinjad_w[5]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_05_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_06_WERT | real | Korrekturoffset pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: tiofsinjad_w[6]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_06_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_07_WERT | real | Korrekturoffset pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: tiofsinjad_w[7]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_07_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_08_WERT | real | Korrekturoffset pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: tiofsinjad_w[8]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_08_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_09_WERT | real | Korrekturoffset pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: tiofsinjad_w[9]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_09_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_10_WERT | real | Korrekturoffset pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: tiofsinjad_w[10]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_10_EINH | string | "ms" |
| STAT_TI_OFS_INJAD_XZYL_YMOD_11_WERT | real | Korrekturoffset pro Zylinder und Korrekturpunkt für die Injektorkennlinie (A2L-Name: tiofsinjad_w[11]) |
| STAT_TI_OFS_INJAD_XZYL_YMOD_11_EINH | string | "ms" |
| STAT_KM_ST_LAST_INJAD_WERT | real | Kilometerstand der letzten vollständigen Injektoradaption (A2L-Name: kmstlastinjad_w) |
| STAT_KM_ST_LAST_INJAD_EINH | string | "km" |
| STAT_INJAD_XAB_YSEQ_0_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) (A2L-Name: statinjadyseq[0]) |
| STAT_INJAD_XAB_YSEQ_1_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) (A2L-Name: statinjadyseq[1]) |
| STAT_INJAD_XAB_YSEQ_2_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) (A2L-Name: statinjadyseq[2]) |
| STAT_INJAD_XAB_YSEQ_3_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) (A2L-Name: statinjadyseq[3]) |
| STAT_INJAD_XAB_YSEQ_4_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) (A2L-Name: statinjadyseq[4]) |
| STAT_INJAD_XAB_YSEQ_5_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) (A2L-Name: statinjadyseq[5]) |
| STAT_INJAD_XAB_YSEQ_6_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) (A2L-Name: statinjadyseq[6]) |
| STAT_INJAD_XAB_YSEQ_7_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) (A2L-Name: statinjadyseq[7]) |
| STAT_INJAD_XAB_YSEQ_8_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) (A2L-Name: statinjadyseq[8]) |
| STAT_INJAD_XAB_YSEQ_9_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) (A2L-Name: statinjadyseq[9]) |
| STAT_INJAD_XAB_YSEQ_10_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) (A2L-Name: statinjadyseq[10]) |
| STAT_INJAD_XAB_YSEQ_11_WERT | unsigned char | Status Injektoradaption (bankweise / Ablaufsequenz) (A2L-Name: statinjadyseq[11]) |
| STAT_ZR_INJAD_AUSS_XAB_YSEQ_0_WERT | unsigned int | Zaehler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) (A2L-Name: zrinjadaussxy_w[0]) |
| STAT_ZR_INJAD_AUSS_XAB_YSEQ_1_WERT | unsigned int | Zaehler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) (A2L-Name: zrinjadaussxy_w[1]) |
| STAT_ZR_INJAD_AUSS_XAB_YSEQ_2_WERT | unsigned int | Zaehler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) (A2L-Name: zrinjadaussxy_w[2]) |
| STAT_ZR_INJAD_AUSS_XAB_YSEQ_3_WERT | unsigned int | Zaehler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) (A2L-Name: zrinjadaussxy_w[3]) |
| STAT_ZR_INJAD_AUSS_XAB_YSEQ_4_WERT | unsigned int | Zaehler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) (A2L-Name: zrinjadaussxy_w[4]) |
| STAT_ZR_INJAD_AUSS_XAB_YSEQ_5_WERT | unsigned int | Zaehler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) (A2L-Name: zrinjadaussxy_w[5]) |
| STAT_ZR_INJAD_AUSS_XAB_YSEQ_6_WERT | unsigned int | Zaehler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) (A2L-Name: zrinjadaussxy_w[6]) |
| STAT_ZR_INJAD_AUSS_XAB_YSEQ_7_WERT | unsigned int | Zaehler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) (A2L-Name: zrinjadaussxy_w[7]) |
| STAT_ZR_INJAD_AUSS_XAB_YSEQ_8_WERT | unsigned int | Zaehler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) (A2L-Name: zrinjadaussxy_w[8]) |
| STAT_ZR_INJAD_AUSS_XAB_YSEQ_9_WERT | unsigned int | Zaehler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) (A2L-Name: zrinjadaussxy_w[9]) |
| STAT_ZR_INJAD_AUSS_XAB_YSEQ_10_WERT | unsigned int | Zaehler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) (A2L-Name: zrinjadaussxy_w[10]) |
| STAT_ZR_INJAD_AUSS_XAB_YSEQ_11_WERT | unsigned int | Zaehler Aussetzer waehrend Injad (bankweise / Ablaufsequenz) (A2L-Name: zrinjadaussxy_w[11]) |
| STAT_ZR_INJAD_TI_BOUND_XAB_YSEQ_0_WERT | unsigned char | Zaehler Verletzung zulaessiger Ti-Bereich (bankweise / Ablaufsequenz) (A2L-Name: zrinjadtiboundxy_w[0]) |
| STAT_ZR_INJAD_TI_BOUND_XAB_YSEQ_1_WERT | unsigned char | Zaehler Verletzung zulaessiger Ti-Bereich (bankweise / Ablaufsequenz) (A2L-Name: zrinjadtiboundxy_w[1]) |
| STAT_ZR_INJAD_TI_BOUND_XAB_YSEQ_2_WERT | unsigned char | Zaehler Verletzung zulaessiger Ti-Bereich (bankweise / Ablaufsequenz) (A2L-Name: zrinjadtiboundxy_w[2]) |
| STAT_ZR_INJAD_TI_BOUND_XAB_YSEQ_3_WERT | unsigned char | Zaehler Verletzung zulaessiger Ti-Bereich (bankweise / Ablaufsequenz)(A2L-Name: zrinjadtiboundxy_w[3]) |
| STAT_ZR_INJAD_TI_BOUND_XAB_YSEQ_4_WERT | unsigned char | Zaehler Verletzung zulaessiger Ti-Bereich (bankweise / Ablaufsequenz) (A2L-Name: zrinjadtiboundxy_w[4]) |
| STAT_ZR_INJAD_TI_BOUND_XAB_YSEQ_5_WERT | unsigned char | Zaehler Verletzung zulaessiger Ti-Bereich (bankweise / Ablaufsequenz) (A2L-Name: zrinjadtiboundxy_w[5]) |
| STAT_ZR_INJAD_TI_BOUND_XAB_YSEQ_6_WERT | unsigned char | Zaehler Verletzung zulaessiger Ti-Bereich (bankweise / Ablaufsequenz)(A2L-Name: zrinjadtiboundxy_w[6]) |
| STAT_ZR_INJAD_TI_BOUND_XAB_YSEQ_7_WERT | unsigned char | Zaehler Verletzung zulaessiger Ti-Bereich (bankweise / Ablaufsequenz) (A2L-Name: zrinjadtiboundxy_w[7]) |
| STAT_ZR_INJAD_TI_BOUND_XAB_YSEQ_8_WERT | unsigned char | Zaehler Verletzung zulaessiger Ti-Bereich (bankweise / Ablaufsequenz) (A2L-Name: zrinjadtiboundxy_w[8]) |
| STAT_ZR_INJAD_TI_BOUND_XAB_YSEQ_9_WERT | unsigned char | Zaehler Verletzung zulaessiger Ti-Bereich (bankweise / Ablaufsequenz) (A2L-Name: zrinjadtiboundxy_w[9]) |
| STAT_ZR_INJAD_TI_BOUND_XAB_YSEQ_10_WERT | unsigned char | Zaehler Verletzung zulaessiger Ti-Bereich (bankweise / Ablaufsequenz) (A2L-Name: zrinjadtiboundxy_w[10]) |
| STAT_ZR_INJAD_TI_BOUND_XAB_YSEQ_11_WERT | unsigned char | Zaehler Verletzung zulaessiger Ti-Bereich (bankweise / Ablaufsequenz) (A2L-Name: zrinjadtiboundxy_w[11]) |
| STAT_ZR_INJAD_COMPL_WERT | unsigned char | Anzahl abgeschlossener Adaptionen (A2L-Name: zrinjadcompl) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-atldiag"></a>
### STATUS_ATLDIAG

Turboladerstatus auslesen ATLDIAG (0x4044)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ATLDIAG_AKTIV | unsigned char | Ladedruckdiagnose aktiv (a2l-Name: B_atl_denom) |
| STAT_ATLDIAG_BANK1 | unsigned char | Ladedruckdiagnose fuer Bank 1 durchgelaufen (a2l-Name: B_atl_nom_b1) |
| STAT_ATLDIAG_BANK2 | unsigned char | Ladedruckdiagnose fuer Bank 2 durchgelaufen (a2l-Name: B_atl_nom_b2) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-klannadap"></a>
### STATUS_KLANNADAP

KLANN Adaptionen auslesen KLANNADAP (0x4046)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_F_LRADAP1_WERT | real | Faktor aus Lambdaregelungsadaption fuer Bank 1 (A2L-Name: frann_w) |
| STAT_DLATRMO_WERT | real | Delta Sondenoffset Fuehrungsregelung (A2L-Name: dlatrmo_w) |
| STAT_FLRADAP1C_W_0_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 1 |
| STAT_FLRADAP1C_W_1_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 2 |
| STAT_FLRADAP1C_W_2_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 3 |
| STAT_FLRADAP1C_W_3_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 4 |
| STAT_FLRADAP1C_W_4_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 5 |
| STAT_FLRADAP1C_W_5_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 6 |
| STAT_FLRADAP1C_W_6_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 7 |
| STAT_FLRADAP1C_W_7_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 8 |
| STAT_FLRADAP1C_W_8_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 9 |
| STAT_FLRADAP1C_W_9_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 10 |
| STAT_FLRADAP1C_W_10_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 11 |
| STAT_FLRADAP1C_W_11_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 12 |
| STAT_FLRADAP1C_W_12_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 13 |
| STAT_FLRADAP1C_W_13_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 14 |
| STAT_FLRADAP1C_W_14_WERT | real | Faktoren aus KLANN-Befragung an applizierten Zentren Bank1 15 |
| STAT_F_LRLZA1_WERT | real | Langzeitadaptions-Faktor aus KLANN Bank1 (NV-Ram) (A2L-Name: frannlza_w) |
| STAT_FLRADAPSTXAB_W_0_WERT | real | Faktor aus KLANN für Start/Nachstartkorrektur Bank1/2 (NV-Ram) 1 |
| STAT_FLRADAPSTXAB_W_1_WERT | real | Faktor aus KLANN für Start/Nachstartkorrektur Bank1/2 (NV-Ram) 2 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-typpruefnr"></a>
### STATUS_TYPPRUEFNR

Typpruefnummer fuer BN2020 SGs auslesen TYPPRUEFNR (0x4047)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TYPPRUEFNR_WERT | unsigned long | Typpruefnummer auslesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-readiness"></a>
### STATUS_READINESS

Monitorfunktionen und Readinessflags aus DME auslesen READINESS (0x4105)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_COMPREHENSIVE | unsigned char | Ueberwachung der uebrigen Komponenten Test abgeschlossen oder nicht anwendbar = 0 test nicht abgeschlossen = 1 |
| STAT_COMPREHENSIVE_TEXT | string | Ueberwachung der uebrigen Komponenten Test abgeschlossen oder nicht anwendbar = 0 test nicht abgeschlossen = 1 |
| STAT_FUELSYSTEM | unsigned char | Ueberwachung Kraftstoffsystem Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_FUELSYSTEM_TEXT | string | Ueberwachung Kraftstoffsystem Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_MISSFIRE | unsigned char | Ueberwachung Verbrennungsaussetzer Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_MISSFIRE_TEXT | string | Ueberwachung Verbrennungsaussetzer Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_COMPREHENSIVE_MONITOR | unsigned char | Ueberwachung der uebrigen Komponenten Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_COMPREHENSIVE_MONITOR_TEXT | string | Ueberwachung der uebrigen Komponenten Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_FUELSYSTEM_MONITOR | unsigned char | Ueberwachung Kraftstoffsystem Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_FUELSYSTEM_MONITOR_TEXT | string | Ueberwachung Kraftstoffsystem Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_MISSFIRE_MONITOR | unsigned char | Ueberwachung Verbrennungsaussetzer Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_MISSFIRE_MONITOR_TEXT | string | Ueberwachung Verbrennungsaussetzer Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_AGRRDY_EIN | unsigned char | Ueberwachung Abgasrueckfuehrung Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_AGRRDY_EIN_TEXT | string | Ueberwachung Abgasrueckfuehrung Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_HSRDY_EIN | unsigned char | Ueberwachung Lambdasondenheizung Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_HSRDY_EIN_TEXT | string | Ueberwachung Lambdasondenheizung Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_LSRDY_EIN | unsigned char | Ueberwachung Lambdasonde Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_LSRDY_EIN_TEXT | string | Ueberwachung Lambdasonde Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_KLIMARDY_EIN | unsigned char | Ueberwachung Klimaanlage Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_KLIMARDY_EIN_TEXT | string | Ueberwachung Klimaanlage Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_SLSRDY_EIN | unsigned char | Ueberwachung Sekundaerluftsystem Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_SLSRDY_EIN_TEXT | string | Ueberwachung Sekundaerluftsystem Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_TESRDY_EIN | unsigned char | Ueberwachung Tankentlueftungssystem Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_TESRDY_EIN_TEXT | string | Ueberwachung Tankentlueftungssystem Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_HKATRDY_EIN | unsigned char | Ueberwachung Katalysatorheizung Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_HKATRDY_EIN_TEXT | string | Ueberwachung Katalysatorheizung Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_KATRDY_EIN | unsigned char | Ueberwachung Katalysator Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_KATRDY_EIN_TEXT | string | Ueberwachung Katalysator Test abgeschlossen oder nicht anwendbar = 0 Test nicht abgeschlossen = 1 |
| STAT_AGRMON_EIN | unsigned char | Ueberwachung Abgasrueckfuehrung Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_AGRMON_EIN_TEXT | string | Ueberwachung Abgasrueckfuehrung Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_HSMON_EIN | unsigned char | Ueberwachung Lambdasondenheizung Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_HSMON_EIN_TEXT | string | Ueberwachung Lambdasondenheizung Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_LSMON_EIN | unsigned char | Ueberwachung Lambdasonde Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_LSMON_EIN_TEXT | string | Ueberwachung Lambdasonde Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_KLIMAMON_EIN | unsigned char | Ueberwachung Klimaanlage Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_KLIMAMON_EIN_TEXT | string | Ueberwachung Klimaanlage Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_SLSMON_EIN | unsigned char | Ueberwachung Sekundaerluftsystem Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_SLSMON_EIN_TEXT | string | Ueberwachung Sekundaerluftsystem Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_TESMON_EIN | unsigned char | Ueberwachung Tankentlueftungssystem Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_TESMON_EIN_TEXT | string | Ueberwachung Tankentlueftungssystem Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_HKATMON_EIN | unsigned char | Ueberwachung Katalysatorheizung Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_HKATMON_EIN_TEXT | string | Ueberwachung Katalysatorheizung Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_KATMON_EIN | unsigned char | Ueberwachung Katalysator Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| STAT_KATMON_EIN_TEXT | string | Ueberwachung Katalysator Test wird durch dieses Modul nicht unterstuetzt = 0 Test wird durch dieses Modul unterstuetzt = 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-gvobd"></a>
### STATUS_GVOBD

Gemischvertrimmung fuer OBD-Demo und PVE auslesen. GVOBD (0x5F80)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SW_F_MK_KORR_EXT_XZYL_1_WERT | real | Faktor auf Einspritzung Zylinder 1 (Physikalische Reihenfolge) |
| STAT_SW_F_MK_KORR_EXT_XZYL_5_WERT | real | Faktor auf Einspritzung Zylinder 5 (Physikalische Reihenfolge) |
| STAT_SW_F_MK_KORR_EXT_XZYL_3_WERT | real | Faktor auf Einspritzung Zylinder 3 (Physikalische Reihenfolge) |
| STAT_SW_F_MK_KORR_EXT_XZYL_6_WERT | real | Faktor auf Einspritzung Zylinder 6 (Physikalische Reihenfolge) |
| STAT_SW_F_MK_KORR_EXT_XZYL_2_WERT | real | Faktor auf Einspritzung Zylinder 2 (Physikalische Reihenfolge) |
| STAT_SW_F_MK_KORR_EXT_XZYL_4_WERT | real | Faktor auf Einspritzung Zylinder 4 (Physikalische Reihenfolge) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-gvobd"></a>
### STEUERN_GVOBD

Gemischvertrimmung fuer OBD-Demo und PVE vorgeben. Der Korrekturfaktor soll bei Klemmenwechsel auf den Standardwert 1 zurueckgesetzt werden. STEUERN_GVOBD (0x5F80)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_F_MK_KORR_EXT_XZYL_1 | real | Faktor auf Einspritzung Zylinder 1 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_5 | real | Faktor auf Einspritzung Zylinder 5 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_3 | real | Faktor auf Einspritzung Zylinder 3 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_6 | real | Faktor auf Einspritzung Zylinder 6 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_2 | real | Faktor auf Einspritzung Zylinder 2 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_4 | real | Faktor auf Einspritzung Zylinder 4 (Physikalische Reihenfolge) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-gvobd"></a>
### STEUERN_PROGRAMM_GVOBD

Gemischvertrimmung fuer OBD-Demo und PVE programmieren. STEUERN_PROGRAMM_GVOBD (0x5F80)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_F_MK_KORR_EXT_XZYL_1 | real | Faktor auf Einspritzung Zylinder 1 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_5 | real | Faktor auf Einspritzung Zylinder 5 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_3 | real | Faktor auf Einspritzung Zylinder 3 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_6 | real | Faktor auf Einspritzung Zylinder 6 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_4 | real | Faktor auf Einspritzung Zylinder 4 (Physikalische Reihenfolge) |
| SW_F_MK_KORR_EXT_XZYL_2 | real | Faktor auf Einspritzung Zylinder 2 (Physikalische Reihenfolge) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-pm-backup"></a>
### STATUS_PM_BACKUP

Auslesen des PM-Backup PM_BACKUP (0x5F8B)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PMBACKUP_0_WERT | unsigned char | Powermanagement Backup [0] |
| STAT_PMBACKUP_1_WERT | unsigned char | Powermanagement Backup [1] |
| STAT_PMBACKUP_2_WERT | unsigned char | Powermanagement Backup [2] |
| STAT_PMBACKUP_3_WERT | unsigned char | Powermanagement Backup [3] |
| STAT_PMBACKUP_4_WERT | unsigned char | Powermanagement Backup [4] |
| STAT_PMBACKUP_5_WERT | unsigned char | Powermanagement Backup [5] |
| STAT_PMBACKUP_6_WERT | unsigned char | Powermanagement Backup [6] |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-pm-restore"></a>
### STEUERN_PM_RESTORE

Schreiben PM-Restore PM_RESTORE (0x5F8B)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PMRESTORE_0 | unsigned char | Codierdaten Powermanagement Backup |
| SW_PMRESTORE_1 | unsigned char | Codierdaten Powermanagement Backup |
| SW_PMRESTORE_2 | unsigned char | Codierdaten Powermanagement Backup |
| SW_PMRESTORE_3 | unsigned char | Codierdaten Powermanagement Backup |
| SW_PMRESTORE_4 | unsigned char | Codierdaten Powermanagement Backup |
| SW_PMRESTORE_5 | unsigned char | Codierdaten Powermanagement Backup |
| SW_PMRESTORE_6 | unsigned char | Codierdaten Powermanagement Backup |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hubkorr"></a>
### STATUS_HUBKORR

Hubkorrektur auslesen HUBKORR (0x5F8C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STVBRVSIN_WERT | unsigned char | Statuswort Verbrennungsregelung vom Tester nichtflüchtig. |
| STAT_STVBRVSNNV_WERT | unsigned char | Statuswort Verbrennungsregelung vom Tester. |
| STAT_STVBRVSO_WERT | unsigned int | Statuswort Verbrennungsregelung für Service. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-hubkorr-programmieren"></a>
### STEUERN_HUBKORR_PROGRAMMIEREN

Hubkorrektur programmieren STEUERN_HUBKORR_PROGRAMMIEREN (0x5F8C)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_STVBRVSNNV | unsigned char | Codierdaten Hub Korrektur |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-hubkorr-reset"></a>
### STEUERN_HUBKORR_RESET

Hubkorrektur loeschen STEUERN_HUBKORR_RESET (0x5F8C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-hubkorr-verstellen"></a>
### STEUERN_HUBKORR_VERSTELLEN

Hubkorrektur vorgeben STEUERN_HUBKORR_VERSTELLEN (0x5F8C)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_STVBRVSIN | unsigned char | Codierdaten Hub Korrektur |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-imaalle"></a>
### STATUS_IMAALLE

Abgleichwerte Injektoren auslesen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. IMAALLE (0x5F90)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DURCHFLUSSABGLEICH_ZYL_1_WERT | real | IMA Abgleichwert Injektor 01 Flow2 (Durchfluss) |
| STAT_DURCHFLUSSABGLEICH_ZYL_1_EINH | string | "mg/Hub" |
| STAT_DURCHFLUSSABGLEICH_ZYL_2_WERT | real | IMA Abgleichwert Injektor 02 Flow2 (Durchfluss) |
| STAT_DURCHFLUSSABGLEICH_ZYL_2_EINH | string | "mg/Hub" |
| STAT_DURCHFLUSSABGLEICH_ZYL_3_WERT | real | IMA Abgleichwert Injektor 03 Flow2 (Durchfluss) |
| STAT_DURCHFLUSSABGLEICH_ZYL_3_EINH | string | "mg/Hub" |
| STAT_DURCHFLUSSABGLEICH_ZYL_4_WERT | real | IMA Abgleichwert Injektor 04 Flow2 (Durchfluss) |
| STAT_DURCHFLUSSABGLEICH_ZYL_4_EINH | string | "mg/Hub" |
| STAT_DURCHFLUSSABGLEICH_ZYL_5_WERT | real | IMA Abgleichwert Injektor 05 Flow2 (Durchfluss) |
| STAT_DURCHFLUSSABGLEICH_ZYL_5_EINH | string | "mg/Hub" |
| STAT_DURCHFLUSSABGLEICH_ZYL_6_WERT | real | IMA Abgleichwert Injektor 06 Flow2 (Durchfluss) |
| STAT_DURCHFLUSSABGLEICH_ZYL_6_EINH | string | "mg/Hub" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-imaalle"></a>
### STEUERN_IMAALLE

Abgleichwerte Injektoren programmieren IMAALLE (0x5F90)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_1 | real | IMA Abgleichwert Injektor 01 Flow2 (Durchfluss) |
| SW_DURCHFLUSSABGLEICH_ZYL_2 | real | IMA Abgleichwert Injektor 02 Flow2 (Durchfluss) |
| SW_DURCHFLUSSABGLEICH_ZYL_3 | real | IMA Abgleichwert Injektor 03 Flow2 (Durchfluss) |
| SW_DURCHFLUSSABGLEICH_ZYL_4 | real | IMA Abgleichwert Injektor 04 Flow2 (Durchfluss) |
| SW_DURCHFLUSSABGLEICH_ZYL_5 | real | IMA Abgleichwert Injektor 05 Flow2 (Durchfluss) |
| SW_DURCHFLUSSABGLEICH_ZYL_6 | real | IMA Abgleichwert Injektor 06 Flow2 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ima-zyl-1"></a>
### STEUERN_IMA_ZYL_1

Abgleichwert Injektor 01 (phys) programmieren IMA_ZYL_1 (0x5F91)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_1 | real | IMA Abgleichwert Injektor 01 Flow2 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ima-zyl-2"></a>
### STEUERN_IMA_ZYL_2

Abgleichwert Injektor 02 (phys) programmieren IMA_ZYL_2 (0x5F92)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_2 | real | IMA Abgleichwert Injektor 02 Flow2 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ima-zyl-3"></a>
### STEUERN_IMA_ZYL_3

Abgleichwert Injektor 03 (phys) programmieren IMA_ZYL_3 (0x5F93)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_3 | real | IMA Abgleichwert Injektor 03 Flow2 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ima-zyl-4"></a>
### STEUERN_IMA_ZYL_4

Abgleichwert Injektor 04 (phys) programmieren IMA_ZYL_4 (0x5F94)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_4 | real | IMA Abgleichwert Injektor 04 Flow2 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ima-zyl-5"></a>
### STEUERN_IMA_ZYL_5

Abgleichwert Injektor 05 (phys) programmieren IMA_ZYL_5 (0x5F95)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_5 | real | IMA Abgleichwert Injektor 05 Flow2 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ima-zyl-6"></a>
### STEUERN_IMA_ZYL_6

Abgleichwert Injektor 06 (phys) programmieren IMA_ZYL_6 (0x5F96)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DURCHFLUSSABGLEICH_ZYL_6 | real | IMA Abgleichwert Injektor 06 Flow2 (Durchfluss) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-kva"></a>
### STEUERN_KVA

KraftstoffVerbrauchsAnzeige - Korrekturfaktor schreiben KVA (0x5FC1)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KVA | real | Codierung Verbrauchsanzeigekorrektur Umrechnung: 0x80 bis 0x7F in -0.128 bis 0.127 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-vvtminh"></a>
### STATUS_VVTMINH

VVT-Minhub auslesen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. VVTMINH (0x5FDE)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_VVTMINH_WERT | real | Hub VVT-Minhub |
| STAT_PHY_VVTMINH_EINH | string | "mm" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ll-abgleich"></a>
### STATUS_LL_ABGLEICH

Abgleichwert LL (Leerlauf) auslesen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. LL_ABGLEICH (0x5FF0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFS_WERT | long | Drehzahlanhebung im Leerlauf |
| STAT_OFS_EINH | string | "1/min" |
| STAT_OFS_ACC_DRI_WERT | long | Drehzahlanhebung im Leerlauf mit Klimaanlage ein |
| STAT_OFS_ACC_DRI_EINH | string | "1/min" |
| STAT_OFS_DRI_WERT | long | Drehzahlanhebung im Leerlauf mit Fahrstufe |
| STAT_OFS_DRI_EINH | string | "1/min" |
| STAT_OFS_ACC_WERT | long | Drehzahlanhebung im Leerlauf mit Fahrstufe und Klimaanlage ein |
| STAT_OFS_ACC_EINH | string | "1/min" |
| STAT_OFS_VB_WERT | long | Drehzahlanhebung im Leerlauf zum Batterie laden |
| STAT_OFS_VB_EINH | string | "1/min" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-abll"></a>
### STEUERN_ENDE_ABLL

Abgleichwert LL (Leerlauf) Vorgeben beenden STEUERN_ENDE_ABLL (0x5FF0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-llabg-prog"></a>
### STEUERN_LLABG_PROG

Abgleichwert LL (Leerlauf) programmieren STEUERN_LLABG_PROG (0x5FF0)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ABLL1 | long | Drehzahlanhebung im Leerlauf |
| SW_ABLL2 | long | Drehzahlanhebung im Leerlauf mit Klimaanlage ein |
| SW_ABLL3 | long | Drehzahlanhebung im Leerlauf mit Fahrstufe |
| SW_ABLL4 | long | Drehzahlanhebung im Leerlauf mit Fahrstufe und Klimaanlage ein |
| SW_ABLL5 | long | Drehzahlanhebung im Leerlauf zum Batterie laden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ll-abgleich"></a>
### STEUERN_LL_ABGLEICH

Abgleichwert LL (Leerlauf) vorgeben STEUERN_LL_ABGLEICH (0x5FF0)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ABLL1 | long | Drehzahlanhebung im Leerlauf |
| SW_ABLL2 | long | Drehzahlanhebung im Leerlauf mit Klimaanlage ein |
| SW_ABLL3 | long | Drehzahlanhebung im Leerlauf mit Fahrstufe |
| SW_ABLL4 | long | Drehzahlanhebung im Leerlauf mit Fahrstufe und Klimaanlage ein |
| SW_ABLL5 | long | Drehzahlanhebung im Leerlauf zum Batterie laden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-ecu-config"></a>
### ECU_CONFIG

Variante auslesen ACHTUNG: Dieser Diagnosedienst darf nur in Ausnahmefaellen als Ersatz fuer den entsprechenden Diagnosedienst 0x30xx-xx verwendet werden. ECU_CONFIG (0x5FF2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DISA_WERT | unsigned char | DISA geschaltet vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_DISA_LM_WERT | unsigned char | DISA geregelt mit Lagerueckmeldung. 0=nicht vorhanden / 1=vorhanden |
| STAT_ANSK_WERT | unsigned char | Ansaugluftklappe vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_TURBO_WERT | unsigned char | Turbo mit Wastegate vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_TURBO_VTG_WERT | unsigned char | Turbo mit variabler Turbinengeometrie vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AGR_WERT | unsigned char | Abgasrueckfuehrung vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AGK_MONO_WERT | unsigned char | Abgaskonzept Mono vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AGK_Y_WERT | unsigned char | Abgaskonzept Y vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AGK_STEREO_WERT | unsigned char | Abgaskonzept Stereo vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AGK_KAT_WERT | unsigned char | Abgaskonzept ohne KAT vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_LLSVK_WERT | unsigned char | Lineare Lambdasonden vor KAT vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_BLSVK_WERT | unsigned char | Binaere Lambdasonden vor KAT vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_SLP_WERT | unsigned char | Sekundaerluftpumpe vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_SLV_WERT | unsigned char | Sekundaerluftventil vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AGK_WERT | unsigned char | Abgasklappe vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_SOK_WERT | unsigned char | Soundklappe vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_KLJ_WERT | unsigned char | Kuehler Jalousie vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_ELUE_400_WERT | unsigned char | E-Luefter 400W vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_ELUE_600_WERT | unsigned char | E-Luefter 600W vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_EBL_WERT | unsigned char | E-Box-Luefter. 0=nicht vorhanden / 1=vorhanden |
| STAT_MFL_WERT | unsigned char | Multifunktionslenkrad. 0=nicht vorhanden / 1=vorhanden |
| STAT_SPT_WERT | unsigned char | Sport-Taster. 0=nicht vorhanden / 1=vorhanden |
| STAT_TOZNIV_WERT | unsigned char | Thermischer Oelniveausensor vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AKKS_BN2000_WERT | unsigned char | Aktive Kuehlluftklappe (oben). 0=nicht vorhanden / 1=vorhanden |
| STAT_PKKS_BN2000_WERT | unsigned char | Passive Kuehlluftklappe (unten). 0=nicht vorhanden / 1=vorhanden |
| STAT_HS_WERT | unsigned char | Handschalter vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_EGS_WERT | unsigned char | EGS vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_DKG_WERT | unsigned char | DKG vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_ASC_WERT | unsigned char | Automatic Stability Control vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_ARS_WERT | unsigned char | Anti Roll Stabilisierung vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_AFS_WERT | unsigned char | Active Front Steering vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_RKK_WERT | unsigned char | Relais Klimakompressor vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_MSA_WERT | unsigned char | Start-Stop-Automatik. 0=nicht vorhanden / 1=vorhanden |
| STAT_AOEL_WERT | unsigned char | Oelabscheiderheizung vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_EMF_WERT | unsigned char | Elektromechanische Feststellbremse vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_SAT_WERT | unsigned char | Sportautomat. 0=nicht vorhanden / 1=vorhanden |
| STAT_ELUE_850_WERT | unsigned char | E-Luefter 850W vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_IBS_WERT | unsigned char | Vorhalt (bisher: intelligenter Batteriesensor an BSD vorhanden) 0=nicht vorhanden / 1=vorhanden |
| STAT_ELUE_1000_WERT | unsigned char | E-Luefter 1000W vorhanden. 0=nicht vorhanden / 1=vorhanden |
| STAT_KLIMA_WERT | unsigned char | Klimaanlage verbaut. 0=nicht vorhanden / 1=vorhanden |
| STAT_BN2000_WERT | unsigned char | Bordnetz 2000. 0=nicht vorhanden / 1=vorhanden |
| STAT_TEMP_CAN_WERT | unsigned char | Tempomat ueber CAN. 0=nicht vorhanden / 1=vorhanden |
| STAT_KOMBI_WERT | unsigned char | Kombi ueber CAN. 0=nicht vorhanden / 1=vorhanden |
| STAT_LDM_WERT | unsigned char | Laengsdynamik-Management. 0=nicht vorhanden / 1=vorhanden |
| STAT_LMM_WERT | unsigned char | Luftmassenmesser. 0=nicht vorhanden / 1=vorhanden |
| STAT_PST_AFS_WERT | unsigned char | Powersteering: AFS1-Botschaft Variante. 0=nicht vorhanden / 1=vorhanden |
| STAT_PST_STE_WERT | unsigned char | Powersteering: STE1-Botschaft Variante. 0=nicht vorhanden / 1=vorhanden |
| STAT_FSTCAN_WERT | unsigned char | Fuellstandsinformation ueber CAN. 0=nicht vorhanden / 1=vorhanden |
| STAT_ICM_WERT | unsigned char | Bedingung ICM verbaut. 0=nicht vorhanden / 1=vorhanden |
| STAT_IBS_BSD_WERT | unsigned char | Batteriesensor am BSD erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_ZWP_BSD_WERT | unsigned char | El. Zusatzwasserpumpe fuer Elektronik am BSD erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_EWAP_BSD_WERT | unsigned char | El. Wasserpumpe am BSD erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_OZS_BSD_WERT | unsigned char | Oelzustandssensor am BSD erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_GEN_2_BSD_WERT | unsigned char | Generator 2 am BSD erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_GEN_1_BSD_WERT | unsigned char | Generator 1 am BSD erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_AFS_BN2020_WERT | unsigned char | Elektrische Lenkung L6 erkannt. 0=nicht vorhanden / 1=vorhanden |
| STAT_IBS_LIN_WERT | unsigned char | Batteriesensor an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_AKKS_LIN_WERT | unsigned char | Aktive Kuehlklappensteuerung an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_BCU_LIN_WERT | unsigned char | Broadcastunit an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_SGR_LIN_WERT | unsigned char | Startergenerator an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_OELSENS_WERT | unsigned char | Variante Oelsensor. 0=nicht vorhanden / 1=vorhanden |
| STAT_WAP_LIN_WERT | unsigned char | Wasserpumpe an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_GEN_LIN_WERT | unsigned char | Generator an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_ZWAP_LIN_WERT | unsigned char | Zusatzwasserpumpe an LIN. 0=nicht vorhanden / 1=vorhanden |
| STAT_KSNDS_WERT | unsigned char | Kraftstoff-Niederdrucksensor. 0=nicht vorhanden / 1=vorhanden |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-ecu-config-reset"></a>
### ECU_CONFIG_RESET

Variante loeschen ECU_CONFIG_RESET (0x5FF2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-pm-histogram-reset"></a>
### STEUERN_PM_HISTOGRAM_RESET

Powermanagement Histogramm loeschen STEUERN_PM_HISTOGRAM_RESET (0x5FF5)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dk"></a>
### STEUERN_DK

Drosselklappe ansteuern DK (0x602A)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DK | real | Tastverhaeltniss Drosselklappe |
| SW_TO_DK | unsigned long | Timeout Drosselklappe |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dk"></a>
### STEUERN_ENDE_DK

Drosselklappe Ansteuerung beenden DK (0x602A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ugen"></a>
### STEUERN_ENDE_UGEN

Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden UGEN (0x6032)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ugen"></a>
### STEUERN_UGEN

Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) ansteuern UGEN (0x6032)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_UGEN | real | Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) |
| SW_TO_UGEN | unsigned long | Timeout Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-eluer"></a>
### STEUERN_ELUER

E-Luefter-Relais ansteuern ELUER (0x6081)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ELUER | unsigned char | Tastverhaeltniss E-Luefter-Relais |
| SW_TO_ELUER | unsigned long | Timeout E-Luefter-Relais |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-eluer"></a>
### STEUERN_ENDE_ELUER

E-Luefter-Relais Ansteuerung beenden ELUER (0x6081)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-glf2"></a>
### STEUERN_ENDE_GLF2

Gesteuerte Luftfuehrung Klappe 2 Ansteuerung beenden GLF2 (0x60A4)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-glf2"></a>
### STEUERN_GLF2

Gesteuerte Luftfuehrung Klappe 2 ansteuern GLF2 (0x60A4)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_GLF2 | unsigned char | Tastverhaeltniss Gesteuerte Luftfuehrung Klappe 2 |
| SW_TO_GLF2 | unsigned long | Timeout Gesteuerte Luftfuehrung Klappe 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-odr"></a>
### STEUERN_ENDE_ODR

Oel Druck Regelung (Geregeltes Oeldrucksystem) Ansteuerung beenden ODR (0x60AB)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-odr"></a>
### STEUERN_ODR

Oel Druck Regelung (Geregeltes Oeldrucksystem) ansteuern ODR (0x60AB)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_P_OELSOL_TST | unsigned long | Oeldruck Sollwert |
| SW_TO_ODR | unsigned long | Timeout Oeldruck Sollwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-odv"></a>
### STEUERN_ENDE_ODV

Oeldruckventil (Geregeltes Oeldrucksystem) Ansteuerung beenden ODV (0x60AC)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-odv"></a>
### STEUERN_ODV

Oeldruckventil (Geregeltes Oeldrucksystem) ansteuern ODV (0x60AC)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ODV | real | Tastverhaeltniss Oeldruckventil Sollwert |
| SW_TO_ODV | unsigned long | Timeout Oeldruckventil Sollwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-mls"></a>
### STEUERN_ENDE_MLS

Motorlagersteuerung Ansteuerung beenden MLS (0x60B2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-mls"></a>
### STEUERN_MLS

Motorlagersteuerung ansteuern MLS (0x60B2)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_MLS | unsigned char | Sollwert Motorlagersteuerung |
| SW_TO_MLS | unsigned long | Timeout Motorlagersteuerung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ulv"></a>
### STEUERN_ENDE_ULV

Umluftventil Ansteuerung beenden ULV (0x60B5)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ulv"></a>
### STEUERN_ULV

Umluftventil ansteuern ULV (0x60B5)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ULV | real | Tastverhaeltniss Umluftventil |
| SW_TO_ULV | unsigned long | Timeout Umluftventil |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lds1"></a>
### STEUERN_ENDE_LDS1

Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) Ansteuerung beenden LDS1 (0x60B6)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-lds1"></a>
### STEUERN_LDS1

Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) ansteuern LDS1 (0x60B6)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LDS1 | real | Tastverhaeltniss Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) |
| SW_TO_LDS1 | unsigned long | Timeout Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-msv"></a>
### STEUERN_ENDE_MSV

Mengensteuerventil Ansteuerung beenden MSV (0x60BD)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-msv"></a>
### STEUERN_MSV

Mengensteuerventil ansteuern MSV (0x60BD)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_MSV | real | Tastverhaeltniss Mengensteuerventil |
| SW_TO_MSV | unsigned long | Timeout Mengensteuerventil |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ewap"></a>
### STEUERN_ENDE_EWAP

elektr. Wasserpumpe Ansteuerung beenden EWAP (0x60BF)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ewap"></a>
### STEUERN_EWAP

elektr. Wasserpumpe (Bit Serielle Datenschnittstelle) ansteuern EWAP (0x60BF)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EWAP | unsigned char | Tastverhaeltniss elektr. Wasserpumpe |
| SW_TO_EWAP | unsigned char | Timeout elektr. Wasserpumpe |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-agk"></a>
### STEUERN_AGK

Abgasklappe ansteuern AGK (0x60C1)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_AGK | unsigned char | Tastverhaeltniss Abgasklappe 0 bis 100 Prozent |
| SW_TO_AGK | unsigned long | Timeout Abgasklappe 0 bis 510s |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-agk"></a>
### STEUERN_ENDE_AGK

Abgasklappe Ansteuerung beenden AGK (0x60C1)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-glf"></a>
### STEUERN_ENDE_GLF

Gesteuerte Luftfuehrung (Klappe 1) Ansteuerung beenden GLF (0x60C3)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-glf"></a>
### STEUERN_GLF

Gesteuerte Luftfuehrung (Klappe 1) ansteuern GLF (0x60C3)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_GLF | unsigned char | Tastverhaeltnis Gesteuerte Luftfuehrung Klappe 1 |
| SW_TO_GLF | unsigned long | Timeout Gesteuerte Luftfuehrung Klappe 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-kft"></a>
### STEUERN_ENDE_KFT

Kennfeldthermostat Ansteuerung beenden KFT (0x60C9)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-kft"></a>
### STEUERN_KFT

Kennfeldthermostat ansteuern KFT (0x60C9)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_KFT | unsigned char | Komponentenansteuerung: Kennfeldthermostat 1 = Kennfeldthermostat ansteuern 0 = Ansteuerung beenden |
| SW_TO_KFT | unsigned long | Timeout Kennfeldthermostat |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-p"></a>
### STEUERN_DMTL_P

Diagnosemodul-Tank Leckage Pumpe ansteuern DMTL_P (0x60CC)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTL_P | unsigned char | Komponentenansteuerung: Diagnosemodul-Tank Leckage Pumpe 1 = Diagnosemodul-Tank Leckage Pumpe ansteuern 0 = Ansteuerung beenden |
| SW_TO_DMTL_P | unsigned long | Timeout Diagnosemodul-Tank Leckage Pumpe |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-p"></a>
### STEUERN_ENDE_DMTL_P

Diagnosemodul-Tank Leckage Pumpe Ansteuerung beenden DMTL_P (0x60CC)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-v"></a>
### STEUERN_DMTL_V

Diagnosemodul-Tank Leckage Ventil ansteuern DMTL_V (0x60CD)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTL_V | unsigned char | Komponentenansteuerung: Diagnosemodul-Tank Leckage Ventil 1 = Diagnosemodul-Tank Leckage Ventil ansteuern 0 = Ansteuerung beenden |
| SW_TO_DMTL_V | unsigned long | Timeout Diagnosemodul-Tank Leckage Ventil |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-v"></a>
### STEUERN_ENDE_DMTL_V

Diagnosemodul-Tank Leckage Ventil Ansteuerung beenden DMTL_V (0x60CD)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-heizung"></a>
### STEUERN_DMTL_HEIZUNG

Diagnosemodul-Tank Leckage Heizung ansteuern DMTL_HEIZUNG (0x60CE)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTLH | unsigned char | Komponentenansteuerung: Diagnosemodul-Tank Leckage Heizung 1 = Diagnosemodul-Tank Leckage Heizung ansteuern 0 = Ansteuerung beenden |
| SW_TO_DMTLH | unsigned long | Timeout Diagnosemodul-Tank Leckage Heizung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-heizung"></a>
### STEUERN_ENDE_DMTL_HEIZUNG

Diagnosemodul-Tank Leckage Heizung Ansteuerung beenden DMTL_HEIZUNG (0x60CE)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-tev"></a>
### STEUERN_ENDE_TEV

Tankentlueftungsventil Ansteuerung beenden TEV (0x60CF)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

Tankentlueftungsventil ansteuern TEV (0x60CF)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_TEV | real | Tastverhaeltniss Tankentlueftungsventil |
| SW_TO_TEV | unsigned long | Timeout Tankentlueftungsventil |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh1"></a>
### STEUERN_ENDE_LSH1

Lambdasondenheizung vor Kat Bank1 Ansteuerung beenden LSH1 (0x60D0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh1"></a>
### STEUERN_LSH1

Lambdasondenheizung vor Kat Bank1 ansteuern LSH1 (0x60D0)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH1 | unsigned char | Tastverhaeltniss Lambdasondenheizung vor Kat 1 |
| SW_TO_LSH1 | unsigned long | Timeout Lambdasondenheizung vor Kat 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh2"></a>
### STEUERN_ENDE_LSH2

Lambdasondenheizung hinter Kat Bank1 Ansteuerung beenden LSH2 (0x60D1)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh2"></a>
### STEUERN_LSH2

Lambdasondenheizung hinter Kat Bank1 ansteuern LSH2 (0x60D1)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH2 | unsigned char | Tastverhaeltniss Lambdasondenheizung hinter Kat 1 |
| SW_TO_LSH2 | unsigned long | Timeout Lambdasondenheizung hinter Kat 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-mil"></a>
### STEUERN_ENDE_MIL

MIL (Malfunction Indicator Lamp) Ansteuerung beenden MIL (0x60D4)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-mil"></a>
### STEUERN_MIL

MIL (Malfunction Indicator Lamp) ansteuern MIL (0x60D4)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_MIL | unsigned long | Tastverhaeltniss MIL (Malfunction Indicator Lamp) |
| SW_TO_MIL | unsigned long | Timeout MIL (Malfunction Indicator Lamp) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-eml"></a>
### STEUERN_EML

EML (Engine Malfunction Lamp) ansteuern EML (0x60D6)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EML | unsigned long | Tastverhaeltniss EML (Engine Malfunction Lamp) |
| SW_TO_EML | unsigned long | Timeout EML (Engine Malfunction Lamp) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-eml"></a>
### STEUERN_ENDE_EML

EML (Engine Malfunction Lamp) Ansteuerung beenden EML (0x60D6)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

Elektrische Kraftstoffpumpe 1 ansteuern Elektrische Kraftstoffpumpe 1 Deaktivierung aufheben EKP (0x60D8)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EKP1 | unsigned char | Komponentenansteuerung: Elektrische Kraftstoffpumpe 1 1 = Elektrische Kraftstoffpumpe 1 ansteuern 0 = Ansteuerung beenden |
| SW_TO_EKP1 | unsigned long | Timeout Elektrische Kraftstoffpumpe 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ekp"></a>
### STEUERN_ENDE_EKP

Elektrische Kraftstoffpumpe 1 Ansteuerung beenden Elektrische Kraftstoffpumpe 1 Deaktivierung aufheben EKP (0x60D8)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-e-luefter"></a>
### STEUERN_ENDE_E_LUEFTER

E-Luefter Ansteuerung beenden E_LUEFTER (0x60DA)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

E-Luefter ansteuern E_LUEFTER (0x60DA)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ELUE | real | Tastverhaeltniss E-Luefter |
| SW_TO_ELUE | unsigned long | Timeout E-Luefter |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-vvt"></a>
### STEUERN_ENDE_VVT

VVT Ansteuerung beenden VVT (0x60DD)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-vvt"></a>
### STEUERN_VVT

VVT ansteuern VVT (0x60DD)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_VVT | real | Tastverhaeltnis VVT |
| SW_TO_VVT | unsigned long | Timeout VVT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev1"></a>
### STEUERN_ENDE_EV1

Einspritzventil 1 (physikalisch) Ansteuerung beenden EV1 (0x60E1)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ev1"></a>
### STEUERN_EV1

Einspritzventil 1 (physikalisch) ansteuern EV1 (0x60E1)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV1 | unsigned long | Periodendauer Einspritzventil 1 |
| SW_TV_EV1 | real | Tastverhaeltniss Einspritzventil 1 |
| SW_TO_EV1 | unsigned long | Timeout Einspritzventil 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev2"></a>
### STEUERN_ENDE_EV2

Einspritzventil 2 (physikalisch) Ansteuerung beenden EV2 (0x60E2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ev2"></a>
### STEUERN_EV2

Einspritzventil 2 (physikalisch) ansteuern EV2 (0x60E2)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV2 | unsigned long | Periodendauer Einspritzventil 2 |
| SW_TV_EV2 | real | Tastverhaeltniss Einspritzventil 2 |
| SW_TO_EV2 | unsigned long | Timeout Einspritzventil 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev3"></a>
### STEUERN_ENDE_EV3

Einspritzventil 3 (physikalisch) Ansteuerung beenden EV3 (0x60E3)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ev3"></a>
### STEUERN_EV3

Einspritzventil 3 (physikalisch) ansteuern EV3 (0x60E3)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV3 | unsigned long | Periodendauer Einspritzventil 3 |
| SW_TV_EV3 | real | Tastverhaeltniss Einspritzventil 3 |
| SW_TO_EV3 | unsigned long | Timeout Einspritzventil 3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev4"></a>
### STEUERN_ENDE_EV4

Einspritzventil 4 (physikalisch) Ansteuerung beenden EV4 (0x60E4)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ev4"></a>
### STEUERN_EV4

Einspritzventil 4 (physikalisch) ansteuern EV4 (0x60E4)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV4 | unsigned long | Periodendauer Einspritzventil 4 |
| SW_TV_EV4 | real | Tastverhaeltniss Einspritzventil 4 |
| SW_TO_EV4 | unsigned long | Timeout Einspritzventil 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev5"></a>
### STEUERN_ENDE_EV5

Einspritzventil 5 (physikalisch) Ansteuerung beenden EV5 (0x60E5)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ev5"></a>
### STEUERN_EV5

Einspritzventil 5 (physikalisch) ansteuern EV5 (0x60E5)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV5 | unsigned long | Periodendauer Einspritzventil 5 |
| SW_TV_EV5 | real | Tastverhaeltniss Einspritzventil 5 |
| SW_TO_EV5 | unsigned long | Timeout Einspritzventil 5 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ev6"></a>
### STEUERN_ENDE_EV6

Einspritzventil 6 (physikalisch) Ansteuerung beenden EV6 (0x60E6)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ev6"></a>
### STEUERN_EV6

Einspritzventil 6 (physikalisch) ansteuern EV6 (0x60E6)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PD_EV6 | unsigned long | Periodendauer Einspritzventil 6 |
| SW_TV_EV6 | real | Tastverhaeltniss Einspritzventil 6 |
| SW_TO_EV6 | unsigned long | Timeout Einspritzventil 6 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-enws"></a>
### STEUERN_ENDE_ENWS

Vanos Einlass Ventil Ansteuerung beenden ENWS (0x60ED)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-enws"></a>
### STEUERN_ENWS

Vanos Einlass Ventil ansteuern ENWS (0x60ED)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ENWS | real | Tastverhaeltniss Vanos Einlassventil |
| SW_TO_ENWS | unsigned long | Timeout Vanos Einlassventil |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-anws"></a>
### STEUERN_ANWS

Vanos Auslass Ventil ansteuern ANWS (0x60EE)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ANWS | real | Tastverhaeltniss Vanos Auslassventil |
| SW_TO_ANWS | unsigned long | Timeout Vanos Auslassventil |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-anws"></a>
### STEUERN_ENDE_ANWS

Vanos Auslass Ventil Ansteuerung beenden ANWS (0x60EE)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-teav"></a>
### STEUERN_ENDE_TEAV

Absperrventil Tankentlueftung Ansteuerung beenden TEAV (0x60FC)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-teav"></a>
### STEUERN_TEAV

Absperrventil Tankentlueftung Ansteuerung TEAV (0x60FC)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_TEAV | unsigned char | Komponentenansteuerung: Absperrventil Tankentlueftung 1 = Absperrventil Tankentlueftung ansteuern 0 = Ansteuerung beenden |
| SW_TO_TEAV | unsigned long | Timeout Absperrventil Tankentlueftung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-tev"></a>
### START_SYSTEMCHECK_TEV

Ansteuern Diagnosefunktion Tankentlueftungsventil SYSTEMCHECK_TEV (0xF022)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-tev"></a>
### STATUS_SYSTEMCHECK_TEV

Auslesen Diagnosefunktion Tankentlueftungsventil SYSTEMCHECK_TEV (0xF022)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFTE | unsigned char | FUNKTIONSSTATUS DFTE |
| STAT_FS_DFTE_TEXT | string | FUNKTIONSSTATUS DFTE |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-tev"></a>
### STOP_SYSTEMCHECK_TEV

Diagnosefunktion Tankentlueftungsventil beenden SYSTEMCHECK_TEV (0xF022)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-evausbl"></a>
### START_SYSTEMCHECK_EVAUSBL

Ansteuern Diagnosefunktion Einspritzventilausblendung SYSTEMCHECK_EVAUSBL (0xF025)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DEVOFF | unsigned char | Ausblendmaske |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-evausbl"></a>
### STATUS_SYSTEMCHECK_EVAUSBL

Auslesen Diagnosefunktion EinspritzVentile EV-Ausblendung SYSTEMCHECK_EVAUSBL (0xF025)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFEV | unsigned char | FUNKTIONSSTATUS DFEV |
| STAT_FS_DFEV_TEXT | string | FUNKTIONSSTATUS DFEV |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-evausbl"></a>
### STOP_SYSTEMCHECK_EVAUSBL

Ende Diagnosefunktion EinspritzVentile EV-Ausblendung SYSTEMCHECK_EVAUSBL (0xF025)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-vvt-anschlag"></a>
### START_SYSTEMCHECK_VVT_ANSCHLAG

Ansteuern Diagnosefunktion VVT-Anschlag lernen SYSTEMCHECK_VVT_ANSCHLAG (0xF027)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-vvt-anschlag"></a>
### STATUS_SYSTEMCHECK_VVT_ANSCHLAG

Auslesen VVT Anschlag lernen SYSTEMCHECK_VVT_ANSCHLAG (0xF027)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_VVTL | unsigned char | FUNKTIONSSTATUS VVTL |
| STAT_FS_VVTL_TEXT | string | FUNKTIONSSTATUS VVTL |
| STAT_VVTL_BIT0 | unsigned char | Auswertung Bit 0 Fehler unterer Anschlag nicht gefunden |
| STAT_VVTL_BIT0_TEXT | string | Auswertung Bit 0 Fehler unterer Anschlag nicht gefunden |
| STAT_VVTL_BIT1 | unsigned char | Auswertung Bit 1 Fehler oberer Anschlag nicht gefunden |
| STAT_VVTL_BIT1_TEXT | string | Auswertung Bit 1 Fehler oberer Anschlag nicht gefunden |
| STAT_VVTL_BIT2 | unsigned char | Auswertung Bit 2 Fehler Verstellbereich Fuehrungssensor unplausibel |
| STAT_VVTL_BIT2_TEXT | string | Auswertung Bit 2 Fehler Verstellbereich Fuehrungssensor unplausibel |
| STAT_VVTL_BIT3 | unsigned char | Auswertung Bit 3 Fehler Verstellbereich Referenzsensor unplausibel |
| STAT_VVTL_BIT3_TEXT | string | Auswertung Bit 3 Fehler Verstellbereich Referenzsensor unplausibel |
| STAT_VVTL_BIT4 | unsigned char | Auswertung Bit 4 Fehler zulaessige Hoechstzeit Anschlaglernvorgang ueberschritten |
| STAT_VVTL_BIT4_TEXT | string | Auswertung Bit 4 Fehler zulaessige Hoechstzeit Anschlaglernvorgang ueberschritten |
| STAT_VVTL_BIT5 | unsigned char | Auswertung Bit 5 Fehler Spannungsversorgung |
| STAT_VVTL_BIT5_TEXT | string | Auswertung Bit 5 Fehler Spannungsversorgung |
| STAT_VVTL_BIT6 | unsigned char | Auswertung Bit 6 Fehler VVT-Sensor, Leistungsversorgung oder Stellglied |
| STAT_VVTL_BIT6_TEXT | string | Auswertung Bit 6 Fehler VVT-Sensor, Leistungsversorgung oder Stellglied |
| STAT_VVTL_BIT7 | unsigned char | Auswertung Bit 7 Ruecknahme Lernanforderung |
| STAT_VVTL_BIT7_TEXT | string | Auswertung Bit 7 Ruecknahme Lernanforderung |
| STAT_ROTW_VVT_WERT | unsigned int | VVT Rotorwinkel |
| STAT_ROTW_VVT_EINH | string | "°" |
| STAT_EXW_VVT_WERT | real | Rel. Exenterwinkel |
| STAT_EXW_VVT_EINH | string | "Grad" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-vvt-anschlag"></a>
### STOP_SYSTEMCHECK_VVT_ANSCHLAG

Diagnosefunktion VVT Anschlag lernen beenden SYSTEMCHECK_VVT_ANSCHLAG (0xF027)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-gen"></a>
### START_SYSTEMCHECK_GEN

Diagnosefunktion Generatortest SYSTEMCHECK_GEN (0xF02A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-gen"></a>
### STATUS_SYSTEMCHECK_GEN

Auslesen Diagnosefunktion Generatortest SYSTEMCHECK_GEN (0xF02A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1 | unsigned char | Stati fuer Diagnosefunktion Generatortest |
| STAT_DIAGNOSE_1_TEXT | string | Stati fuer Diagnosefunktion Generatortest |
| STAT_FI_GENEL | unsigned char | Status elektrischer Fehler Generator |
| STAT_FI_GENEL_TEXT | string | Status elektrischer Fehler Generator |
| STAT_FI_GENMECH | unsigned char | Status mechanischer Fehler Generator |
| STAT_FI_GENMECH_TEXT | string | Status mechanischer Fehler Generator |
| STAT_FI_GENHT | unsigned char | Status Hochtemperaturfehler Generator |
| STAT_FI_GENHT_TEXT | string | Status Hochtemperaturfehler Generator |
| STAT_FI_GENUPL | unsigned char | Plausibilitaet Generatortyp |
| STAT_FI_GENUPL_TEXT | string | Plausibilitaet Generatortyp |
| STAT_FI_GENKOMM | unsigned char | Status Generatorkommunikation |
| STAT_FI_GENKOMM_TEXT | string | Status Generatorkommunikation |
| STAT_FI_GENELB | unsigned char | Plausibilitaet Generatorspannung aus Berechnung |
| STAT_FI_GENELB_TEXT | string | Plausibilitaet Generatorspannung aus Berechnung |
| STAT_FI_GENHTB | unsigned char | Hochtemperaturfehler Generator aus Berechnung |
| STAT_FI_GENHTB_TEXT | string | Hochtemperaturfehler Generator aus Berechnung |
| STAT_FI_GENREGUPL | unsigned char | Plausibilitaet Generatorregler |
| STAT_FI_GENREGUPL_TEXT | string | Plausibilitaet Generatorregler |
| STAT_DF_HIGH | unsigned char | Status Generatorauslastung |
| STAT_DF_HIGH_TEXT | string | Status Generatorauslastung |
| STAT_GENITEST_TOL_WERT | real | Toleranzbereich fuer Abweichung vom Sollwert Strom |
| STAT_GENITEST_TOL_EINH | string | "%" |
| STAT_GENUTEST_TOL_WERT | real | Toleranzbereich fuer Abweichung vom Sollwert Spannung |
| STAT_GENUTEST_TOL_EINH | string | "%" |
| STAT_I_GENTEST_WERT | unsigned char | Modellierter Generatorstrom |
| STAT_I_GENTEST_EINH | string | "A" |
| STAT_U_GENTEST_WERT | real | Generatorsollspannung |
| STAT_U_GENTEST_EINH | string | "V" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-gen"></a>
### STOP_SYSTEMCHECK_GEN

Diagnosefunktion Generatortest beenden SYSTEMCHECK_GEN (0xF02A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-odr"></a>
### START_SYSTEMCHECK_ODR

Diagnosefunktion Oeldruckregelung SYSTEMCHECK_ODR (0xF02C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-odr"></a>
### STATUS_SYSTEMCHECK_ODR

Auslesen Diagnosefunktion Oeldruckregelung SYSTEMCHECK_ODR (0xF02C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1 | unsigned char | Stati fuer Diagnosefunktion Oeldruckregelung |
| STAT_DIAGNOSE_1_TEXT | string | Stati fuer Diagnosefunktion Oeldruckregelung |
| STAT_DIAGNOSE_2 | unsigned char | Erweiterte Stati fuer Diagnosefunktion Oeldruckregelung |
| STAT_DIAGNOSE_2_TEXT | string | Erweiterte Stati fuer Diagnosefunktion Oeldruckregelung |
| STAT_TOEL_WERT | real | Ausgabewert Motoroeltemperatur fuer LoCAN (A2L-Name: Toel) |
| STAT_TOEL_EINH | string | "°C" |
| STAT_P_OEL_SOLL_WERT | real | Sollwert Oeldruck |
| STAT_P_OEL_SOLL_EINH | string | "kPa" |
| STAT_P_OEL_IST_WERT | int | Istwert Oeldruck |
| STAT_P_OEL_IST_EINH | string | "hPa" |
| STAT_NKW_SOLL_WERT | int | Sollwertanforderung Drehzahl aus Funktion Oeldruckregelung |
| STAT_NKW_SOLL_EINH | string | "1/min" |
| STAT_NKW_WERT | real | Istwert Drehzahl Kurbelwelle |
| STAT_NKW_EINH | string | "rpm" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-odr"></a>
### STOP_SYSTEMCHECK_ODR

Diagnosefunktion Oeldruckregelung beenden SYSTEMCHECK_ODR (0xF02C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-adap-selektiv-loeschen"></a>
### ADAP_SELEKTIV_LOESCHEN

Ansteuern Adaptionen selektiv loeschen - Batterietausch ausgeblendet. ADAP_SELEKTIV_LOESCHEN (0xF030)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE_1 | unsigned char | AUSWAHLBYTE_1_BIT_7 -- &gt; Adaption Abgasrueckfuehrungsventil (NOT USED) AUSWAHLBYTE_1_BIT_6 --&gt; Adaption Lambdaregelung AUSWAHLBYTE_1_BIT_5 --&gt; Adaption Drosselklappe AUSWAHLBYTE_1_BIT_4 --&gt; Adaption Saugrohrmodell AUSWAHLBYTE_1_BIT_3 --&gt; Adaption Tankentlueftung AUSWAHLBYTE_1_BIT_2 --&gt; Adaption Lambdasonden AUSWAHLBYTE_1_BIT_1 --&gt; Adaption Klopfregelung AUSWAHLBYTE_1_BIT_0 --&gt; Adaption Leerlaufabgleich |
| AUSWAHLBYTE_2 | unsigned char | AUSWAHLBYTE_2_BIT_7 --&gt; Adaption Variabler Ventiltrieb (VVT) AUSWAHLBYTE_2_BIT_6 --&gt; Adaption gelernte Varainten AUSWAHLBYTE_2_BIT_5 --&gt; Adaption Oktanzahl AUSWAHLBYTE_2_BIT_4 --&gt; Registrierung Batterietausch AUSWAHLBYTE_2_BIT_3 --&gt; Adaption Hochdruckpumpe AUSWAHLBYTE_2_BIT_2 --&gt; Adaption Sekundaerluftsystem (NOT USED) AUSWAHLBYTE_2_BIT_1 --&gt; Adaption NOx-Sensor (NOT USED) AUSWAHLBYTE_2_BIT_0 --&gt; Adaption Lastregelung |
| AUSWAHLBYTE_3 | unsigned char | AUSWAHLBYTE_3_BIT_7 --&gt; Energieadaption Injektoren (NOT USED) AUSWAHLBYTE_3_BIT_6 --&gt; NOT USED AUSWAHLBYTE_3_BIT_5 --&gt; NOT USED AUSWAHLBYTE_3_BIT_4 --&gt; Adaption Laufunruhe (Faktor und Offset) und zylinderindividuelle Lambdaregelung(NOT USED) AUSWAHLBYTE_3_BIT_3 --&gt; Adaption Zylindergleichstellung fuer Bandende und Fahrzyklus AUSWAHLBYTE_3_BIT_2 --&gt; Adaption Verbrennungsregelung AUSWAHLBYTE_3_BIT_1 --&gt; Adaption Segmentzeit AUSWAHLBYTE_3_BIT_0 --&gt; Adaption VANOS |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-adap2-selektiv-loeschen"></a>
### ADAP2_SELEKTIV_LOESCHEN

Ansteuern Adaptionen 2 selektiv loeschen ADAP2_SELEKTIV_LOESCHEN (0xF031)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADAV2_AUSWAHLBYTE_1 | unsigned char | ADAV2_AUSWAHLBYTE_1_BIT_7 -- &gt; Kleinstmengenadaption ADAV2_AUSWAHLBYTE_1_BIT_6 --&gt; NOT USED ADAV2_AUSWAHLBYTE_1_BIT_5 --&gt; NOT USED ADAV2_AUSWAHLBYTE_1_BIT_4 --&gt; NOT USED ADAV2_AUSWAHLBYTE_1_BIT_3 --&gt; Adaption elektrische Kraftstoffpumpe ADAV2_AUSWAHLBYTE_1_BIT_2 --&gt; Adaption Langzeit fuer Injektoralterung Bank 2(NOT USED) ADAV2_AUSWAHLBYTE_1_BIT_1 --&gt; Adaption Langzeit fuer Injektoralterung Bank 1(NOT USED) ADAV2_AUSWAHLBYTE_1_BIT_0 --&gt; Adaption Nullgangsensor (Achtung: Mit diesem Bit darf die Adaption des Nullgangsensors nicht mehr geloescht werden! Bei Austausch des Nullgangsensors soll die Adaption mit dem dafuer vorgesehenen Dienst durch |
| ADAV2_AUSWAHLBYTE_2 | unsigned char | ADAV2_AUSWAHLBYTE_2_BIT_7 --&gt; NOT USED ADAV2_AUSWAHLBYTE_2_BIT_6 --&gt; Verlustmomentadaption Reset ADAV2_AUSWAHLBYTE_2_BIT_5 --&gt; Adaption NOx-Katalysator (NOT USED) ADAV2_AUSWAHLBYTE_2_BIT_4 --&gt; Bereichserkennung Benzin im Oel (B_clradbo) ADAV2_AUSWAHLBYTE_2_BIT_3 --&gt; NOT USED ADAV2_AUSWAHLBYTE_2_BIT_2 --&gt; NOT USED ADAV2_AUSWAHLBYTE_2_BIT_1 --&gt; NOT USED ADAV2_AUSWAHLBYTE_2_BIT_0 --&gt; NOT USED |
| ADAV2_AUSWAHLBYTE_3 | unsigned char | ADAV2_AUSWAHLBYTE_3_BIT_7 --&gt; NOT USED ADAV2_AUSWAHLBYTE_3_BIT_6 --&gt; NOT USED ADAV2_AUSWAHLBYTE_3_BIT_5 --&gt; NOT USED ADAV2_AUSWAHLBYTE_3_BIT_4 --&gt; NOT USED ADAV2_AUSWAHLBYTE_3_BIT_3 --&gt; NOT USED ADAV2_AUSWAHLBYTE_3_BIT_2 --&gt; NOT USED ADAV2_AUSWAHLBYTE_3_BIT_1 --&gt; NOT USED ADAV2_AUSWAHLBYTE_3_BIT_0 --&gt; NOT USED |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-zsz"></a>
### START_SYSTEMCHECK_ZSZ

Ansteuern Zuendkerze freibrennen (Kalttestspezifisch) SYSTEMCHECK_ZSZ (0xF036)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZUENDFREQUENZ | unsigned char | Zuendfrequenz zum Freibrennen der Zuendkerzen |
| FREIBRENNDAUER | real | Freibrenndauer |
| LADEDAUER | real | Ladedauer fuer alle Kalttest-Zuendungstests (Freibrennen, zeitgesteuerte Ablauf- sequenz, winkelsynchroner Test) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-zsz"></a>
### STATUS_SYSTEMCHECK_ZSZ

Auslesen Zuendkerze freibrennen (Kalttestspezifisch) SYSTEMCHECK_ZSZ (0xF036)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_ZSZ | unsigned char | FUNKTIONSSTATUS ZSZ |
| STAT_FS_ZSZ_TEXT | string | FUNKTIONSSTATUS ZSZ |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-zsz"></a>
### STOP_SYSTEMCHECK_ZSZ

Ende Zuendkerze freibrennen (Kalttestspezifisch) SYSTEMCHECK_ZSZ (0xF036)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-zszw"></a>
### START_SYSTEMCHECK_ZSZW

Ansteuern betriebspunktunabhaengiger (Winkelsynchroner) Zuenspulentest (Kalttestspezifisch) SYSTEMCHECK_ZSZW (0xF037)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LADEDAUER | real | Ladedauer fuer alle Kalttest-Zuendungstests (Freibrennen, zeitgesteuerte Ablauf- sequenz, winkelsynchroner Test) |
| ZUENDWINKEL | real | Zuendwinkel fuer winkelsynchronen Zuendungstest (Es wird nur ein Wert übertragen, welcher für alle Zylinder gleichermassen gilt). |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-zszw"></a>
### STATUS_SYSTEMCHECK_ZSZW

Auslesen betriebspunktunabhaengiger (Winkelsynchroner) Zuenspulentest (Kalttestspezifisch) SYSTEMCHECK_ZSZW (0xF037)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_ZSZW | unsigned char | FUNKTIONSSTATUS ZSZW |
| STAT_FS_ZSZW_TEXT | string | FUNKTIONSSTATUS ZSZW |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-zszw"></a>
### STOP_SYSTEMCHECK_ZSZW

Ende betriebspunktunabhaengiger (Winkelsynchroner) Zuenspulentest (Kalttestspezifisch) SYSTEMCHECK_ZSZW (0xF037)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-evz"></a>
### START_SYSTEMCHECK_EVZ

Ansteuern Sequentieller EV-Zylinderabfolgetest (Kalttestspezifisch) SYSTEMCHECK_EVZ (0xF038)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ANSTEUERDAUER | real | Ansteuerdauer pro Einspritzimpuls vom Testermodul |
| PERIONDENDAUER | real | Periodendauer fuer Einspritzimpuls vom Testermodul |
| PAUSENDAUER | real | Pausendauer zwischen der Ansteuerung der Injektoren bei Ansteuersequenz vom Testermodul |
| ANZAHL_DER_TESTIMPULSE | unsigned char | Anzahl der Testimpulse pro Injektor vom Testermodul |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-evz"></a>
### STATUS_SYSTEMCHECK_EVZ

Auslesen Sequentieller EV-Zylinderabfolgetest (Kalttestspezifisch) SYSTEMCHECK_EVZ (0xF038)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_EVZ | unsigned char | FUNKTIONSSTATUS EVZ |
| STAT_FS_EVZ_TEXT | string | FUNKTIONSSTATUS EVZ |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-evz"></a>
### STOP_SYSTEMCHECK_EVZ

Ende Sequentieller EV-Zylinderabfolgetest (Kalttestspezifisch) SYSTEMCHECK_EVZ (0xF038)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-zszz"></a>
### START_SYSTEMCHECK_ZSZZ

Ansteuern Zeitbasierte Zuendsequenz (Kalttestspezifisch) SYSTEMCHECK_ZSZZ (0xF039)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PAUSENDAUER | real | Pausendauer zwischen der Ansteuerung der Zuendkerzen bei Ansteuersequenz vom Testermodul |
| LADEDAUER | real | Ladedauer fuer alle Kalttest-Zuendungstests (Freibrennen, zeitgesteuerte Ablauf- sequenz, winkelsynchroner Test |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-zszz"></a>
### STATUS_SYSTEMCHECK_ZSZZ

Auslesen Zeitbasierte Zuendsequenz (Kalttestspezifisch) SYSTEMCHECK_ZSZZ (0xF039)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_ZSZZ | unsigned char | FUNKTIONSSTATUS ZSZZ |
| STAT_FS_ZSZZ_TEXT | string | FUNKTIONSSTATUS ZSZZ |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-zszz"></a>
### STOP_SYSTEMCHECK_ZSZZ

Ende Zeitbasierte Zuendsequenz (Kalttestspezifisch) SYSTEMCHECK_ZSZZ (0xF039)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-zwdiag"></a>
### START_ZWDIAG

CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Start-Routine ZWDIAG (0xF03A)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAC_CH_DIAG_EXT_ADJ_IS | real | Manipulation factor of CH torque reserve for ignition angle efficiency monitoring - demo-mode IS |
| FAC_CH_DIAG_EXT_ADJ_PL | real | Manipulation factor of CH torque reserve for ignition angle efficiency monitoring - demo-mode PL |
| LV_CH_DIAG_EXT_REQ | unsigned char | External request for ignition angle efficiency monitoring - demo- mode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-zwdiag"></a>
### STATUS_ZWDIAG

CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Status-Routine ZWDIAG (0xF03A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_ZWDIAG | unsigned char | FUNKTIONSSTATUS ZWDIAG |
| STAT_FS_ZWDIAG_TEXT | string | FUNKTIONSSTATUS ZWDIAG |
| STAT_LV_DIAG_CST_ACT | unsigned char | Condition for cold start diagnosis active |
| STAT_LV_DIAG_CST_ACT_TEXT | string | Condition for cold start diagnosis active |
| STAT_LV_INH_DIAG_EFF_IGA_CST | unsigned char | Flag for inhibitation of the Ignition angle efficiency Diagnosis |
| STAT_LV_INH_DIAG_EFF_IGA_CST_TEXT | string | Flag for inhibitation of the Ignition angle efficiency Diagnosis |
| STAT_STATE_CH | unsigned char | state of catalyst heating (A2L-Name: state_ch) |
| STAT_STATE_CH_TEXT | string | state of catalyst heating (A2L-Name: state_ch) |
| STAT_T_AST_WERT | real | Time after start (A2L-Name: t_ast) |
| STAT_T_AST_EINH | string | "s" |
| STAT_TCO_ST_WERT | real | coolant temperature at start (A2L-Name: tco_st) |
| STAT_TCO_ST_EINH | string | "Grad C" |
| STAT_LV_CDN_DIAG_EFF_IGA_CST_IS | unsigned char | Diagnosis conditions fulfilled Ignition angle efficiency at coldstart - idle speed |
| STAT_LV_CDN_DIAG_EFF_IGA_CST_IS_TEXT | string | Diagnosis conditions fulfilled Ignition angle efficiency at coldstart - idle speed |
| STAT_LV_CDN_DIAG_EFF_IGA_CST_PL | unsigned char | Diagnosis conditions fulfilled Ignition angle efficiency at coldstart - part load |
| STAT_LV_CDN_DIAG_EFF_IGA_CST_PL_TEXT | string | Diagnosis conditions fulfilled Ignition angle efficiency at coldstart - part load |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-zwdiag"></a>
### STOP_ZWDIAG

CSERS Diagnose zur Fehlerdemo (Zuendwinkeldiagnose) Stop-Routine ZWDIAG (0xF03A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-vanosspuelen"></a>
### START_VANOSSPUELEN

VANOS Spuelen fuer OBD und PVE. VANOSSPUELEN (0xF042)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VANOSSPL_M_MODUS | unsigned char | 1=gleichzeitiges Verstellen von Ein- und Auslass-Vanos. und 2=erst Verstellen Einlass, dann Verstellen Auslass. Default-Wert = 1. (A2L-Name: modenwstcl) |
| VANOSSPL_N_AZLVERSTL | unsigned char | Anzahl Verstellungen (von 1 bis 50). Default-Wert = 10 Dez. (A2L-Name: anztvtcl) |
| VANOSSPL_T_HLTZVERSTL | real | Haltezeit Verstellung (0 bis 5 s). Default-Wert = 2.0 s. Gesamtzeit Vanosspuelen = N * 2 * T * m. (A2L-Name: takttcl) |
| VANOSSPL_N1_UDZLGRNZ | unsigned long | Untere Drehzahlgrenze (500 bis 2000 U/min) ca 100 U/min unter LL-Solldrehzahl . Default-Wert = 1000. (A2L-Name: nmotmintcl) |
| VANOSSPL_N2_ODZLGRNZ | unsigned long | Obere Drehzahlgrenze (500 bis 2000 U/min) ca 100 U/min ueber LL-Solldrehzahl . Default-Wert = 1200. (A2L-Name: nmotmaxtcl) |
| VANOSSPL_V_MAX | unsigned char | Max. Fahrzeuggeschwindigkeit (0 bis 100 km/h). Default-Wert = 0 (A2L-Name: vfzgmxtcl) |
| VANOSSPL_T2_ZUBRZ | real | Zulaessige Unterbrechungszeit (0 bis 20 s). Default-Wert = 5s. (A2L-Name: taktumxtcl) |
| VANOSSPL_DVSE1_VO1EV | real | Verstelloffset 1 Einlass-Vanos (von -102,4 bis 101,6°KW). Default-Wert=5.6°Grad. (A2L-Name: ofstclnwe1) |
| VANOSSPL_DVSE2_VO2EV | real | Verstelloffset 2 Einlass-Vanos (von -102,4 bis 101,6°KW). Default-Wert=-5.6°Grad. (A2L-Name: ofstclnwe2) |
| VANOSSPL_DVSA1_VO1AV | real | Verstelloffset 1 Auslas-Vanos (von -102,4 bis 101,6°KW). Default-Wert=-5.6°Grad. (A2L-Name: ofstclnwa1) |
| VANOSSPL_DVSA2_VO1AV | real | Verstelloffset 2 Auslas-Vanos (von -102,4 bis 101,6°KW). Default-Wert=5.6°Grad. (A2L-Name: ofstclnwa2) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-vanosspuelen"></a>
### STATUS_VANOSSPUELEN

VANOS Spuelen fuer OBD und PVE. VANOSSPUELEN (0xF042)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_VANOSSPUELEN | unsigned char | FUNKTIONSSTATUS VANOSSPUELEN |
| STAT_FS_VANOSSPUELEN_TEXT | string | FUNKTIONSSTATUS VANOSSPUELEN |
| STAT_NMOT_W_WERT | real | Motordrehzahl soll zws. der unteren Drehzahlgrenze (ca. 100 rpm unter LL-Solldrehzahl. Default= 1000 rpm) und der oberen Drehzahlgrenze (ca. 100 rpm ueber LL-Solldrehzahl. Default = 1200 rpm) sein. |
| STAT_NMOT_W_EINH | string | "1/min" |
| STAT_V_WERT | unsigned int | Fahrzeuggeschwindigkeit soll zws. 0 und 100 Km/h liegen. Default = 0 |
| STAT_V_EINH | string | "km/h" |
| STAT_ST_LL_WERT | unsigned char | Status Leerlauf (A2L-Name: St_ll) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-vanosspuelen"></a>
### STOP_VANOSSPUELEN

VANOS Spuelen fuer OBD und PVE. VANOSSPUELEN (0xF042)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-atl"></a>
### START_SYSTEMCHECK_ATL

Diagnosefunktion Abgasturbolader starten SYSTEMCHECK_ATL (0xF0D0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-atl"></a>
### STATUS_SYSTEMCHECK_ATL

Diagnosefunktion Abgasturbolader auslesen SYSTEMCHECK_ATL (0xF0D0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1 | unsigned char | Status waehrend der Diagnose der ATL (A2L-Name: St_atlsvc) |
| STAT_DIAGNOSE_1_TEXT | string | Status waehrend der Diagnose der ATL (A2L-Name: St_atlsvc) |
| STAT_DIAGNOSE_2 | unsigned char | Ergebis der Diagnosefunktion der ATL (A2L-Name: St_atlsvc_pvdk) |
| STAT_DIAGNOSE_2_TEXT | string | Ergebis der Diagnosefunktion der ATL (A2L-Name: St_atlsvc_pvdk) |
| STAT_AMP_WERT | real | Ambient pressure (measured or adapted) (A2L-Name: amp) |
| STAT_AMP_EINH | string | "hPa" |
| STAT_TAM_WERT | real | Ambient temperature (A2L-Name: tam) |
| STAT_TAM_EINH | string | "Grad C" |
| STAT_TIA_WERT | real | Intake air temperature (A2L-Name: tia) |
| STAT_TIA_EINH | string | "Grad C" |
| STAT_ATLSVC_DPVDK1_WERT | real | Differenzdruck vor DK beider Turbolader (A2L-Name: Atlsvc_dpvdk1) |
| STAT_ATLSVC_DPVDK2_WERT | real | Differenzdruck vor DK mit Turbolader 1 (A2L-Name: Atlsvc_dpvdk2) |
| STAT_ATLSVC_DPVDK3_WERT | real | Differenzdruck vor DK mit Turbolader 2 (A2L-Name: Atlsvc_dpvdk3) |
| STAT_PWG_IST_WERT | real | Pedalwert Fahrerwunsch in % (A2L-Name: Pwg_ist) |
| STAT_TN_ABSTELL_WERT | unsigned int | Abstellzeit (A2L-Name: Tn_abstell) |
| STAT_B_KUPP | unsigned char | Bedingung Kupplungsbetätigung über Schalter oder Modell (A2L-Name: St_bgkuppl.B_kupp) |
| STAT_B_KUPP_TEXT | string | Bedingung Kupplungsbetätigung über Schalter oder Modell (A2L-Name: St_bgkuppl.B_kupp) |
| STAT_GANGI_WERT | unsigned char | Aktueller Gang intern (A2L-Name: Gangi) |
| STAT_V_WERT | real | Fahrzeuggeschwindigkeit (A2L-Name: V) |
| STAT_V_EINH | string | "km/h" |
| STAT_TMOT_WERT | real | Kuehlwassertemperatur (A2L-Name: Tmot) |
| STAT_TMOT_EINH | string | "Grad C" |
| STAT_PU_WERT | real | Umgebungsdruck (A2L-Name: Pu) |
| STAT_PU_EINH | string | "hPa" |
| STAT_LV_ERR_PUT_EL_WERT | unsigned long | electrical PUT sensor error detected (A2L-Name: lv_err_put_el) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-atl"></a>
### STOP_SYSTEMCHECK_ATL

Diagnosefunktion Abgasturbolader beenden SYSTEMCHECK_ATL (0xF0D0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-glf"></a>
### START_SYSTEMCHECK_GLF

Ansteuern Gesteuerte Luftfuehrung Systemcheck SYSTEMCHECK_GLF (0xF0D5)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-glf"></a>
### STATUS_SYSTEMCHECK_GLF

Auslesen Gesteuerte Luftfuehrung Systemcheck SYSTEMCHECK_GLF (0xF0D5)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CTR_ECRAS_UP_SP_WERT | unsigned int | Sollposition in Schritten fuer Luftklappe (a2l: RadSht_StpEng) |
| STAT_CTR_ECRAS_UP_WERT | unsigned int | Istposition in Schritten fuer Luftklappe (a2l: ShtrECU_StpEngPos) |
| STAT_ANG_ECRAS_UP_SP_WERT | real | Sollposition in Grad obere Luftklappe (a2l: RadSht_phiPos) |
| STAT_ANG_ECRAS_UP_WERT | real | Istposition in Grad obere Luftklappe (a2l: RadSht_phiPos) |
| STAT_ECRAS_UP_ERR7 | unsigned char | nicht belegt |
| STAT_ECRAS_UP_ERR6 | unsigned char | nicht belegt |
| STAT_ECRAS_UP_ERR5 | unsigned char | nicht belegt |
| STAT_ECRAS_UP_ERR4 | unsigned char | nicht belegt |
| STAT_ECRAS_UP_ERR3 | unsigned char | nicht belegt |
| STAT_ECRAS_UP_ERR2 | unsigned char | nicht belegt |
| STAT_ECRAS_UP_ERR1 | unsigned char | nicht belegt |
| STAT_ECRAS_UP_ERR0 | unsigned char | Fehler im Luftklappengesamtsystem (0=nicht vorhanden 1= vorhanden) |
| STAT_ECRAS_UP_DIAG_END7 | unsigned char | Anschlagtest Auf (Blockiererkennung) bei der AKKS-LIN (0=noch nicht durchgeführt 1= beendet) |
| STAT_ECRAS_UP_DIAG_END6 | unsigned char | Anschlagtest AUF (Anschlag nicht gefunden) bei der AKKS-LIN (0=noch nicht durchgeführt 1= beendet) |
| STAT_ECRAS_UP_DIAG_END5 | unsigned char | Anschlagtest ZU bei der AKKS-LIN (0=noch nicht durchgeführt 1= beendet) |
| STAT_ECRAS_UP_DIAG_END4 | unsigned char | Status Elektrodiagnose im AKKS-LIN Steller (0=noch nicht durchgeführt 1= beendet) |
| STAT_ECRAS_UP_DIAG_END3 | unsigned char | Status Temperaturdiagnose im AKKS-LIN Steller (0=noch nicht durchgeführt 1= beendet) |
| STAT_ECRAS_UP_DIAG_END2 | unsigned char | Status Spannungsdiagnose im AKKS-LIN Steller (0=noch nicht durchgeführt 1= beendet) |
| STAT_ECRAS_UP_DIAG_END1 | unsigned char | Status Kommunikationsdiagnose auf Framefehler (0= noch nicht durchgeführt, 1= beendet) |
| STAT_ECRAS_UP_DIAG_END0 | unsigned char | Status Kommunikationsdiagnose auf LIN Botschaften (0= noch nicht durchgeführt, 1= beendet) |
| STAT_ECRAS_UP7 | unsigned char | externe Ansteuerung AKKS-LIN (0= nicht aktiv 1= aktiv) |
| STAT_ECRAS_UP6 | unsigned char | Systemtest (0= nicht aktiv 1= aktiv) |
| STAT_ECRAS_UP5 | unsigned char | Anschlagtest Aus (0= nicht aktiv 1= aktiv) |
| STAT_ECRAS_UP4 | unsigned char | Anschlagtest Zu (0= nicht aktiv 1= aktiv) |
| STAT_ECRAS_UP3 | unsigned char | Spannungsstatus für AKKS-LIN Steller (0= UB n.i.O. 1= UB i.O.) |
| STAT_ECRAS_UP2 | unsigned char | AKKS-LIN offen (0= nicht offen 1= offen) |
| STAT_ECRAS_UP1 | unsigned char | AKKS-LIN geschlossen (0= nicht geschlossen 1= geschlossen) |
| STAT_ECRAS_UP0 | unsigned char | Variante AKKS-LIN (0=nicht vorhanden 1= vorhanden) |
| STAT_ECRAS_DOWN7 | unsigned char | Ansteuerung PKKS (0= Zu, 1= Auf) |
| STAT_ECRAS_DOWN6 | unsigned char | externe Ansteuerung PKKS (0= nicht aktiv 1= aktiv) |
| STAT_ECRAS_DOWN5 | unsigned char | nicht belegt |
| STAT_ECRAS_DOWN4 | unsigned char | nicht belegt |
| STAT_ECRAS_DOWN3 | unsigned char | nicht belegt |
| STAT_ECRAS_DOWN2 | unsigned char | nicht belegt |
| STAT_ECRAS_DOWN1 | unsigned char | elektrischer Fehler PKKS (0=nicht vorhanden 1= vorhanden) |
| STAT_ECRAS_DOWN0 | unsigned char | Variante PKKS (0=nicht vorhanden 1= vorhanden) |
| STAT_STATE_ECRAS_UP_VAR_WERT | unsigned char | Varianteninfo vom AKKS-LIN Steller (highbyte= Hardwareversion 0-F lowbyte= Softwareversion 0-F) (a2l: shtrecu_stinit) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-glf"></a>
### STOP_SYSTEMCHECK_GLF

Ende Gesteuerte Luftfuehrung Systemcheck SYSTEMCHECK_GLF (0xF0D5)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-l-regelung-aus"></a>
### START_SYSTEMCHECK_L_REGELUNG_AUS

Ansteuerung Lambdaregelung deaktivieren SYSTEMCHECK_L_REGELUNG_AUS (0xF0D9)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-l-regelung-aus"></a>
### STATUS_SYSTEMCHECK_L_REGELUNG_AUS

Auslesen Lambdaregelung ausschalten SYSTEMCHECK_L_REGELUNG_AUS (0xF0D9)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DFL0 | unsigned char | FUNKTIONSSTATUS DFLO |
| STAT_FS_DFL0_TEXT | string | FUNKTIONSSTATUS DFLO |
| STAT_FLGRS | unsigned char | CARB FREEZE FRAME Byte, Bank 1, für LR. |
| STAT_FLGRS_TEXT | string | CARB FREEZE FRAME Byte, Bank 1, für LR. |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-l-regelung-aus"></a>
### STOP_SYSTEMCHECK_L_REGELUNG_AUS

Ende Lambdaregelung ausschalten SYSTEMCHECK_L_REGELUNG_AUS (0xF0D9)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-dmtl"></a>
### START_SYSTEMCHECK_DMTL

Ansteuern Diagnosefunktion DMTL SYSTEMCHECK_DMTL (0xF0DA)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-dmtl"></a>
### STATUS_SYSTEMCHECK_DMTL

Auslesen Diagnosefunktion DMTL SYSTEMCHECK_DMTL (0xF0DA)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1 | unsigned char | Funktionsstatus Diagnosefunktion DMTL |
| STAT_DIAGNOSE_1_TEXT | string | Funktionsstatus Diagnosefunktion DMTL |
| STAT_DIAGNOSE_2 | unsigned char | Status Diagnosefunktion DMTL |
| STAT_DIAGNOSE_2_TEXT | string | Status Diagnosefunktion DMTL |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-dmtl"></a>
### STOP_SYSTEMCHECK_DMTL

Diagnosefunktion DMTL beenden SYSTEMCHECK_DMTL (0xF0DA)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-eisyugd"></a>
### START_EISYUGD

Ansteuern Eisy-Adaptionswerte (ungedrosselt) (Anforderung aus CP5403) EISYUGD (0xF0E0)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW | int | Drehzahl |
| VSE_SPRI | real | Istwert Einlassspreizung variable NWS |
| VSA_SPRI | real | Istwert Auslassspreizung variable NWS |
| HUBEV_IST | real | Istwert Einlassventilhub |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-eisyugd"></a>
### STATUS_EISYUGD

Auslesen Eisy-Adaptionswerte (ungedrosselt) (Anforderung aus CP5403) EISYUGD (0xF0E0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_EISYUGD | unsigned char | FUNKTIONSSTATUS EISYUGD |
| STAT_FS_EISYUGD_TEXT | string | FUNKTIONSSTATUS EISYUGD |
| STAT_MRNN_TEST_VVT_WERT | real | Massenstromregler-Adaptionswert NN im VVT Betrieb ueber Test gelesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-eisygd"></a>
### START_EISYGD

Ansteuern Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403) EISYGD (0xF0E1)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW | int | Drehzahl |
| VSE_SPRI | real | Istwert Einlassspreizung variable NWS |
| VSA_SPRI | real | Istwert Auslassspreizung variable NWS |
| WDK_IST | real | Aktueller Drosselklappenwinkel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-eisygd"></a>
### STATUS_EISYGD

Auslesen Eisy-Adaptionswerte (gedrosselt) (Anforderung aus CP5403) EISYGD (0xF0E1)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_EISYGD | unsigned char | Massestromregler auf DK erstmalig erfolgt |
| STAT_FS_EISYGD_TEXT | string | Massestromregler auf DK erstmalig erfolgt |
| STAT_MRNN_TEST_DK_WERT | real | Massenstromregler-Adaptionswert NN im GD - Betrieb ueber Test gelesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-klann"></a>
### START_KLANN

Ansteuern Klann-Adaptionswerte (Anforderung aus CP10798) KLANN (0xF0E4)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_LOC | int | Drehzahl |
| RK_LOC | real | Relative Kraftstoffmasse |
| TMOT_LOC | real | Kuehlwassertemperatur |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-klann"></a>
### STATUS_KLANN

Auslesen Klann-Adaptionswerte (Anforderung aus CP10798) KLANN (0xF0E4)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLNN_TEST_WERT | real | Lambdaadaptionswert fuer Testerabfrage |
| STAT_KLNN_TEST_EINH | string | "%" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-ddlshk"></a>
### START_DDLSHK

Ansteuern Dynamik Diagnose Lamdasonden hinter Hauptkat DDLSHK (0xF0E7)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ddlshk"></a>
### STATUS_DDLSHK

Auslesen Dynamik Diagnose Lamdasonden hinter Hauptkat DDLSHK (0xF0E7)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DDLSHK | unsigned char | Bedingung dynamikmessung Lambdasonde Hinterkat freigegeben |
| STAT_FS_DDLSHK_TEXT | string | Bedingung dynamikmessung Lambdasonde Hinterkat freigegeben |
| STAT_TAHSO_WERT | real | Abgastemperatur an Sonde hinter Kat |
| STAT_TAHSO_EINH | string | "Grad C" |
| STAT_TRLRS2_WERT | real | Ereignisfilterwert für Transient Zeit Sonde hinter KAT LR |
| STAT_TRLRS2_EINH | string | "s" |
| STAT_TRRLS2_WERT | real | Ereignisfilterwert für Transient Zeit Sonde hinter KAT Bank 2 |
| STAT_TRRLS2_EINH | string | "s" |
| STAT_DTLRFS2_WERT | real | Ereignisfilterwert für Response Zeit Sonde hinter KAT LR |
| STAT_DTLRFS2_EINH | string | "s" |
| STAT_DTRLFS2_WERT | real | Ereignisfilterwert für Response Zeit Sonde hinter KAT RL |
| STAT_DTRLFS2_EINH | string | "s" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-ddlshk"></a>
### STOP_DDLSHK

Ende Dynamik Diagnose Lamdasonden hinter Hauptkat DDLSHK (0xF0E7)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-cram"></a>
### START_CRAM

Ansteuern RAM-Backup-Werte loeschen CRAM (0xF0E9)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cram"></a>
### STATUS_CRAM

Auslesen RAM-Backup-Werte loeschen CRAM (0xF0E9)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_CRAM | unsigned char | FUNKTIONSSTATUS CRAM |
| STAT_FS_CRAM_TEXT | string | FUNKTIONSSTATUS CRAM |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-dkat"></a>
### START_SYSTEMCHECK_DKAT

Ansteuern Kurztest Kat SYSTEMCHECK_DKAT (0xF0EB)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-dkat"></a>
### STATUS_SYSTEMCHECK_DKAT

Auslesen Kurztest Kat SYSTEMCHECK_DKAT (0xF0EB)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_DKAT | unsigned char | FUNKTIONSSTATUS DKAT |
| STAT_FS_DKAT_TEXT | string | FUNKTIONSSTATUS DKAT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-dkat"></a>
### STOP_SYSTEMCHECK_DKAT

Ende Kurztest Kat SYSTEMCHECK_DKAT (0xF0EB)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-ram"></a>
### START_RAM

Ansteuern RAM Backup zwangssichern RAM (0xF0F2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ram"></a>
### STATUS_RAM

Auslesen RAM Backup zwangssichern RAM (0xF0F2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_RAM | unsigned char | FUNKTIONSSTATUS RAM |
| STAT_FS_RAM_TEXT | string | FUNKTIONSSTATUS RAM |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-pm-messemode"></a>
### START_SYSTEMCHECK_PM_MESSEMODE

Ansteuern Messemode SYSTEMCHECK_PM_MESSEMODE (0xF0F6)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-pm-messemode"></a>
### STATUS_SYSTEMCHECK_PM_MESSEMODE

Auslesen Messemode SYSTEMCHECK_PM_MESSEMODE (0xF0F6)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_PM_MESSEMODE | unsigned char | Funktionsstatus Powermanagement Messemode |
| STAT_SYSTEMCHECK_PM_MESSEMODE_TEXT | string | Funktionsstatus Powermanagement Messemode |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-pm-messemode"></a>
### STOP_SYSTEMCHECK_PM_MESSEMODE

Ende Messemode SYSTEMCHECK_PM_MESSEMODE (0xF0F6)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (66 × 2)
- [LIEFERANTEN](#table-lieferanten) (116 × 2)
- [FARTTEXTE](#table-farttexte) (19 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (24 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (11 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (120 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [LIEFERANTENLIN](#table-lieferantenlin) (92 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [CBSKENNUNG](#table-cbskennung) (11 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (8 × 3)
- [FORTTEXTE](#table-forttexte) (849 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (525 × 9)
- [IORTTEXTE](#table-iorttexte) (1 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [MESSWERTETAB](#table-messwertetab) (388 × 12)
- [RESET_GRPID](#table-reset-grpid) (33 × 2)
- [RESET_ID](#table-reset-id) (146 × 2)
- [BA_VCV_STATE_TEXT](#table-ba-vcv-state-text) (8 × 2)
- [SG_FUNKTIONEN](#table-sg-funktionen) (388 × 16)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [STATCLIENTAUTHTXT](#table-statclientauthtxt) (4 × 2)
- [STATFREESKTXT](#table-statfreesktxt) (3 × 2)
- [STATEWSVERTXT](#table-statewsvertxt) (3 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT4_DOP](#table-t-1bit-switch-position-high-byte-bit4-dop) (2 × 2)
- [T_ST_ATLSVC_PVDK_DOP](#table-t-st-atlsvc-pvdk-dop) (6 × 2)
- [T_B_BZDON_DOP](#table-t-b-bzdon-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT2_DOP](#table-t-1bit-switch-position-low-byte-bit2-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT2_DOP](#table-t-1bit-state-ready-obd-2-bit2-dop) (2 × 2)
- [T_1BIT_GENIUTEST_ERR_BIT2_DOP](#table-t-1bit-geniutest-err-bit2-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_1_BIT6_DOP](#table-t-1bit-state-ready-obd-1-bit6-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_BIT2_DOP](#table-t-1bit-switch-position-bit2-dop) (2 × 2)
- [T_1BIT_GENIUTEST_ERR_BIT7_DOP](#table-t-1bit-geniutest-err-bit7-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_1_BIT0_DOP](#table-t-1bit-state-ready-obd-1-bit0-dop) (2 × 2)
- [T_1BIT_GENIUTEST_ERR_BIT3_DOP](#table-t-1bit-geniutest-err-bit3-dop) (2 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT2_DOP](#table-t-1bit-c-state-ready-obd-2-bit2-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT4_DOP](#table-t-1bit-fs-erw-vvtl-bit4-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT5_DOP](#table-t-1bit-fs-erw-vvtl-bit5-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_1_BIT4_DOP](#table-t-1bit-state-ready-obd-1-bit4-dop) (2 × 2)
- [T_B_BZD_WRGBAT_DOP](#table-t-b-bzd-wrgbat-dop) (2 × 2)
- [T_BZD_BTZUST_DOP](#table-t-bzd-btzust-dop) (4 × 2)
- [T_STATE_DMTL_DOP](#table-t-state-dmtl-dop) (21 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT4_DOP](#table-t-1bit-c-state-ready-obd-2-bit4-dop) (2 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT6_DOP](#table-t-1bit-c-state-ready-obd-2-bit6-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT7_DOP](#table-t-1bit-state-ready-obd-2-bit7-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_BIT0_DOP](#table-t-1bit-switch-position-bit0-dop) (2 × 2)
- [T_ST_ATLSVC_DOP](#table-t-st-atlsvc-dop) (9 × 2)
- [T_1BIT_SWITCH_POSITION_BIT3_DOP](#table-t-1bit-switch-position-bit3-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT6_DOP](#table-t-1bit-switch-position-high-byte-bit6-dop) (2 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT7_DOP](#table-t-1bit-c-state-ready-obd-2-bit7-dop) (2 × 2)
- [T_B_VVTNOTL_DOP](#table-t-b-vvtnotl-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT7_DOP](#table-t-1bit-switch-position-high-byte-bit7-dop) (2 × 2)
- [T_1BYTE_FS_DDLHK_DOP](#table-t-1byte-fs-ddlhk-dop) (6 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT0_DOP](#table-t-1bit-switch-position-high-byte-bit0-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT7_DOP](#table-t-1bit-fs-erw-vvtl-bit7-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT7_DOP](#table-t-1bit-switch-position-low-byte-bit7-dop) (2 × 2)
- [T_1BIT_GENIUTEST_ERR_BIT1_DOP](#table-t-1bit-geniutest-err-bit1-dop) (2 × 2)
- [T_1BIT_GENIUTEST_ERR_BIT4_DOP](#table-t-1bit-geniutest-err-bit4-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT3_DOP](#table-t-1bit-fs-erw-vvtl-bit3-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT4_DOP](#table-t-1bit-state-ready-obd-2-bit4-dop) (2 × 2)
- [T_1BIT_GENIUTEST_ERR_BIT6_DOP](#table-t-1bit-geniutest-err-bit6-dop) (2 × 2)
- [T_1BIT_GENIUTEST_ERR_BIT5_DOP](#table-t-1bit-geniutest-err-bit5-dop) (2 × 2)
- [T_EOL_RAM_1__DOP](#table-t-eol-ram-1-dop) (10 × 2)
- [T_1BIT_SWITCH_POSITION_BIT4_DOP](#table-t-1bit-switch-position-bit4-dop) (2 × 2)
- [T_ST_TESTPOELSYS2_DOP](#table-t-st-testpoelsys2-dop) (7 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT1_DOP](#table-t-1bit-fs-erw-vvtl-bit1-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT6_DOP](#table-t-1bit-fs-erw-vvtl-bit6-dop) (2 × 2)
- [T_B_QVCH2O_DOP](#table-t-b-qvch2o-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT3_DOP](#table-t-1bit-state-ready-obd-2-bit3-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT1_DOP](#table-t-1bit-state-ready-obd-2-bit1-dop) (2 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT1_DOP](#table-t-1bit-c-state-ready-obd-2-bit1-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_1_BIT2_DOP](#table-t-1bit-state-ready-obd-1-bit2-dop) (2 × 2)
- [T_B_BZD_TE_DOP](#table-t-b-bzd-te-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_BIT1_DOP](#table-t-1bit-switch-position-bit1-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT5_DOP](#table-t-1bit-state-ready-obd-2-bit5-dop) (2 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT3_DOP](#table-t-1bit-c-state-ready-obd-2-bit3-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT6_DOP](#table-t-1bit-state-ready-obd-2-bit6-dop) (2 × 2)
- [T_ST_GENTEST_DOP](#table-t-st-gentest-dop) (8 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT5_DOP](#table-t-1bit-c-state-ready-obd-2-bit5-dop) (2 × 2)
- [T_B_STANDARD_1BYTE_LESEN_0_1](#table-t-b-standard-1byte-lesen-0-1) (3 × 2)
- [T_1BIT_C_STATE_READY_OBD_2_BIT0_DOP](#table-t-1bit-c-state-ready-obd-2-bit0-dop) (2 × 2)
- [T_1BYTE_FS_DOP](#table-t-1byte-fs-dop) (11 × 2)
- [T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT3_DOP](#table-t-1bit-switch-position-low-byte-bit3-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_1_BIT1_DOP](#table-t-1bit-state-ready-obd-1-bit1-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_1_BIT5_DOP](#table-t-1bit-state-ready-obd-1-bit5-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT0_DOP](#table-t-1bit-fs-erw-vvtl-bit0-dop) (2 × 2)
- [T_1BIT_GENIUTEST_AB_BIT0_DOP](#table-t-1bit-geniutest-ab-bit0-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT3_DOP](#table-t-1bit-switch-position-high-byte-bit3-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_BIT7_DOP](#table-t-1bit-switch-position-bit7-dop) (2 × 2)
- [T_S_VSMNHB_DOP](#table-t-s-vsmnhb-dop) (2 × 2)
- [T_1BIT_FS_ERW_VVTL_BIT2_DOP](#table-t-1bit-fs-erw-vvtl-bit2-dop) (2 × 2)
- [T_1BIT_GENIUTEST_ERR_BIT0_DOP](#table-t-1bit-geniutest-err-bit0-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT6_DOP](#table-t-1bit-switch-position-low-byte-bit6-dop) (2 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT1_DOP](#table-t-1bit-switch-position-high-byte-bit1-dop) (2 × 2)
- [T_ST_TESTPOELSYS_DOP](#table-t-st-testpoelsys-dop) (8 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT5_DOP](#table-t-1bit-switch-position-high-byte-bit5-dop) (2 × 2)
- [T_1BIT_STATE_READY_OBD_2_BIT0_DOP](#table-t-1bit-state-ready-obd-2-bit0-dop) (2 × 2)
- [T_BA_IST_DOP](#table-t-ba-ist-dop) (5 × 2)
- [T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT2_DOP](#table-t-1bit-switch-position-high-byte-bit2-dop) (2 × 2)
- [RES_0XF04](#table-res-0xf04) (1 × 13)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 66 rows × 2 columns

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
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?80? | ERROR_SVK_INCORRECT_LEN |
| ?81? | ERROR_SVK_INCORRECT_FINGERPRINT |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 116 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x000001 | Reinshagen =&gt; Delphi |
| 0x000002 | Kostal |
| 0x000003 | Hella |
| 0x000004 | Siemens |
| 0x000005 | Eaton |
| 0x000006 | UTA |
| 0x000007 | Helbako |
| 0x000008 | Bosch |
| 0x000009 | Loewe =&gt; Lear |
| 0x000010 | VDO |
| 0x000011 | Valeo |
| 0x000012 | MBB |
| 0x000013 | Kammerer |
| 0x000014 | SWF |
| 0x000015 | Blaupunkt |
| 0x000016 | Philips |
| 0x000017 | Alpine |
| 0x000018 | Continental Teves |
| 0x000019 | Elektromatik Suedafrika |
| 0x000020 | Becker |
| 0x000021 | Preh |
| 0x000022 | Alps |
| 0x000023 | Motorola |
| 0x000024 | Temic |
| 0x000025 | Webasto |
| 0x000026 | MotoMeter |
| 0x000027 | Delphi PHI |
| 0x000028 | DODUCO =&gt; BERU |
| 0x000029 | DENSO |
| 0x000030 | NEC |
| 0x000031 | DASA |
| 0x000032 | Pioneer |
| 0x000033 | Jatco |
| 0x000034 | Fuba |
| 0x000035 | UK-NSI |
| 0x000036 | AABG |
| 0x000037 | Dunlop |
| 0x000038 | Sachs |
| 0x000039 | ITT |
| 0x000040 | FTE |
| 0x000041 | Megamos |
| 0x000042 | TRW |
| 0x000043 | Wabco |
| 0x000044 | ISAD Electronic Systems |
| 0x000045 | HEC (Hella Electronics Corporation) |
| 0x000046 | Gemel |
| 0x000047 | ZF |
| 0x000048 | GMPT |
| 0x000049 | Harman Kardon |
| 0x000050 | Remes |
| 0x000051 | ZF Lenksysteme |
| 0x000052 | Magneti Marelli |
| 0x000053 | Borg Instruments |
| 0x000054 | GETRAG |
| 0x000055 | BHTC (Behr Hella Thermocontrol) |
| 0x000056 | Siemens VDO Automotive |
| 0x000057 | Visteon |
| 0x000058 | Autoliv |
| 0x000059 | Haberl |
| 0x000060 | Magna Steyr |
| 0x000061 | Marquardt |
| 0x000062 | AB-Elektronik |
| 0x000063 | Siemens VDO Borg |
| 0x000064 | Hirschmann Electronics |
| 0x000065 | Hoerbiger Electronics |
| 0x000066 | Thyssen Krupp Automotive Mechatronics |
| 0x000067 | Gentex GmbH |
| 0x000068 | Atena GmbH |
| 0x000069 | Magna-Donelly |
| 0x000070 | Koyo Steering Europe |
| 0x000071 | NSI B.V |
| 0x000072 | AISIN AW CO.LTD |
| 0x000073 | Shorlock |
| 0x000074 | Schrader |
| 0x000075 | BERU Electronics GmbH |
| 0x000076 | CEL |
| 0x000077 | Audio Mobil |
| 0x000078 | rd electronic |
| 0x000079 | iSYS RTS GmbH |
| 0x000080 | Westfalia Automotive GmbH |
| 0x000081 | Tyco Electronics |
| 0x000082 | Paragon AG |
| 0x000083 | IEE S.A |
| 0x000084 | TEMIC AUTOMOTIVE of NA |
| 0x000085 | AKsys GmbH |
| 0x000086 | META System |
| 0x000087 | Hülsbeck & Fürst GmbH & Co KG |
| 0x000088 | Mann & Hummel Automotive GmbH |
| 0x000089 | Brose Fahrzeugteile GmbH & Co |
| 0x000090 | Keihin |
| 0x000091 | Vimercati S.p.A. |
| 0x000092 | CRH |
| 0x000093 | TPO Display Corp. |
| 0x000094 | KÜSTER Automotive Control |
| 0x000095 | Hitachi Automotive |
| 0x000096 | Continental Automotive |
| 0x000097 | TI-Automotive |
| 0x000098 | Hydro |
| 0x000099 | Johnson Controls |
| 0x00009A | Takata- Petri |
| 0x00009B | Mitsubishi Electric B.V. (Melco) |
| 0x00009C | Autokabel |
| 0x00009D | GKN-Driveline |
| 0x00009E | Zollner Elektronik AG |
| 0x00009F | PEIKER acustics GmbH |
| 0x0000A0 | Bosal-Oris |
| 0x0000A1 | Cobasys |
| 0x0000A2 | Lighting Reutlingen GmbH |
| 0x0000A3 | CONTI VDO |
| 0x0000A4 | ADC Automotive Distance Control Systems GmbH |
| 0x0000A5 | Funkwerk Dabendorf GmbH |
| 0x0000A6 | Lame |
| 0x0000A7 | Magna/Closures |
| 0x0000A8 | Wanyu |
| 0x0000A9 | Thyssen Krupp Presta |
| 0xFFFFFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 19 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler momentan vorhanden und bereits gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler momentan vorhanden und bereits gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler momentan vorhanden und bereits gespeichert |
| 0x40 | unbekannte Fehlerart |
| 0x44 | Fehler gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler gespeichert |
| 0x4D | Fehler gespeichert |
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

Dimensions: 24 rows × 3 columns

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
| 0xA0 | ENTD | Entertainment Daten |
| 0xA1 | NAVD | Navigation Daten |
| 0xA2 | FCFN | Freischaltcode Funktion |
| 0xC0 | SWUP | Software-Update Package |
| 0xC1 | SWIP | Index Software-Update Package |
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

Dimensions: 5 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | KM_STAND | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1701 | ABS_ZEIT | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1702 | SAE_CODE | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1731 | Fehlerklasse_DTC | - | - | u char | - | 1 | 1 | 0.000000 |
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

Dimensions: 11 rows × 3 columns

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
| 0x4F | ECUDEVELOP | ECUDevelopmentSession |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 120 rows × 3 columns

| ORT | ORTTEXT | LIN_2_FORMAT |
| --- | --- | --- |
| 0x0100 | Batteriesensor BSD | - |
| 0x0150 | Ölqualitätsensor BSD | - |
| 0x0200 | Elektrische Wasserpumpe BSD | - |
| 0x0250 | Elektrische Kraftstoffpumpe BSD | - |
| 0x0300 | Generator 1 | - |
| 0x0350 | Generator 2 | - |
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
| 0x1000 | Topview Kamera Außenspiegel links | 1 |
| 0x1100 | Topview Kamera Außenspiegel rechts | 1 |
| 0x1200 | Sideview Kamera Stoßfänger vorne links | 1 |
| 0x1300 | Sideview Kamera Stoßfänger vorne rechts | 1 |
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
| 0x2300 | Aussenspiegel Beifahrer | - |
| 0x2400 | Schaltzentrum Tür | 1 |
| 0x2500 | Schalterblock Sitz Fahrer | 1 |
| 0x2600 | Schalterblock Sitz Beifahrer | 1 |
| 0x2700 | Gurtbringer Fahrer | 1 |
| 0x2800 | Gurtbringer Beifahrer | 1 |
| 0x2900 | Treibermodul Scheinwerfer links | 1 |
| 0x2A00 | Treibermodul Scheinwerfer rechts | 1 |
| 0x2B00 | Bedieneinheit Fahrerassistenzsysteme | 1 |
| 0x2C00 | Bedieneinheit Licht | 1 |
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
| 0x3B80 | Elektrische Zusatzwasserpumpe | 1 |
| 0x3C00 | Batteriesensor LIN | - |
| 0x3D00 | Aktives Kühlklappensystem | 1 |
| 0x3E00 | PCU(DCDC) | 1 |
| 0x3F00 | Startergenerator | 1 |
| 0x3F80 | Generator | 1 |
| 0x4000 | Sitzverstellschalter Fahrer | 1 |
| 0x4100 | Sitzverstellschalter Beifahrer | 1 |
| 0x4200 | Sitzverstellschalter Fahrer hinten | 1 |
| 0x4300 | Sitzverstellschalter Beifahrer hinten | 1 |
| 0x4400 | Gepäckraumschalter links | 1 |
| 0x4500 | Gepäckraumschalter rechts | 1 |
| 0x4A00 | Fond-Klimaanlage | 1 |
| 0x4B00 | Elektrischer Klimakompressor | 1 |
| 0x5000 | PMA Sensor links | 1 |
| 0x5100 | PMA Sensor rechts | 1 |
| 0x5200 | CID-Klappe | - |
| 0x5300 | Schaltzentrum Lenksäule | 1 |
| 0x5400 | Multifunktionslenkrad | 1 |
| 0x5500 | Lenkradelektronik | 1 |
| 0x5600 | CID | - |
| 0x5700 | Satellit Upfront links | 0 |
| 0x5708 | Satellit Upfront rechts | 0 |
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
| 0x5768 | Fussgängerschutz Sensor links | 0 |
| 0x5770 | Fussgängerschutz Sensor rechts | 0 |
| 0x5778 | Fussgängerschutz Sensor mitte | 0 |
| 0x5780 | Fussgängerschutz Sensorband | 0 |
| 0x5788 | Satellit C-Säule links Y | 0 |
| 0x5790 | Satellit C-Säule rechts Y | 0 |
| 0x5798 | Satellit Zentrale Körperschall | 0 |
| 0x57A0 | Kapazitive Insassen- Sensorik CIS | 1 |
| 0x57A8 | Sitzbelegungserkennung Beifahrer SBR | 1 |
| 0x5800 | HUD | 1 |
| 0x5900 | Audio-Bedienteil | 1 |
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-lieferantenlin"></a>
### LIEFERANTENLIN

Dimensions: 92 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x0001 | Audi |
| 0x0002 | BMW |
| 0x0003 | DaimlerChrysler |
| 0x0004 | Motorola |
| 0x0005 | VCT/Mentor Graphics |
| 0x0006 | VW (VW-Group) |
| 0x0007 | Volvo Cars (Ford Group) |
| 0x000B | Freescale Semiconductor |
| 0x0011 | NXP Semiconductors |
| 0x0012 | ST Microelectronics |
| 0x0013 | Melexis |
| 0x0014 | Microchip |
| 0x0015 | CRF |
| 0x0016 | Renesas Technology Europe GmbH |
| 0x0017 | Atmel |
| 0x0018 | Magnet Marelli |
| 0x0019 | NEC |
| 0x001A | Fujitsu |
| 0x001B | Opel |
| 0x001C | Infineon |
| 0x001D | AMI Semiconductor |
| 0x001E | Vector Informatik |
| 0x001F | Brose |
| 0x0020 | ZMD |
| 0x0021 | ihr |
| 0x0022 | Visteon |
| 0x0023 | ELMOS |
| 0x0024 | ON Semi |
| 0x0025 | Denso |
| 0x0026 | c&s |
| 0x0027 | Renault |
| 0x0028 | Renesas Technology Europe Limited |
| 0x0029 | Yazaki |
| 0x002A | Trinamic Microchips |
| 0x002B | Allegro Microsystems |
| 0x002C | Toyota |
| 0x002D | PSA Peugeot Citroën |
| 0x002E | Westsächsische Hochschule Zwickau |
| 0x002F | Micron AG |
| 0x0030 | Delphi Deutschland GmbH |
| 0x0031 | Texas Instruments Deutschland GmbH |
| 0x0032 | Maxim Integrated Products |
| 0x0033 | Bertrandt Ingenierbüro GmbH |
| 0x0034 | PKC Group Oyi |
| 0x0035 | BayTech IKs |
| 0x0036 | Hella KGaA Hueck & Co. |
| 0x0037 | Continental Temic microelectronic GmbH |
| 0x0038 | Johnson Controls GmbH |
| 0x0039 | Toshiba Electronics Europe GmbH |
| 0x003A | Analog Devices |
| 0x003B | TRW Automotive Electronics & Components GmbH & Co. KG |
| 0x003C | Advanced Data Controls, Corp. |
| 0x003D | GÖPEL electronic GmbH |
| 0x003E | Dr. Ing. h.c. F. Porsche AG |
| 0x003F | Marquardt GmbH |
| 0x0040 | ETAS GmbH |
| 0x0041 | Micronas GmbH |
| 0x0042 | Preh GmbH |
| 0x0043 | GENTEX CORPORATION |
| 0x0044 | ZF Lenksysteme GmbH |
| 0x0045 | Nagares S.A. |
| 0x0046 | MAN Nutzfahrzeuge AG |
| 0x0047 | BITRON SpA BU Grugliasco |
| 0x0048 | Pierburg GmbH |
| 0x0049 | Alps Electric Co., Ltd |
| 0x004A | Beru Electronics GmbH |
| 0x004B | Paragon AG |
| 0x004C | Silicon Laboratories |
| 0x004D | Sensata Technologies Holland B.V. |
| 0x004E | Meta System S.p.A |
| 0x004F | Dräxlmaier Systemtechnik GmbH |
| 0x0050 | Grupo Antolin Ingenieria, S.A. |
| 0x0051 | MAGNA-Donnelly GmbH&Co.KG |
| 0x0052 | IEE S.A. |
| 0x0053 | austriamicrosystems AG |
| 0x0054 | Agilent Technologies |
| 0x0055 | Lear Corporation  |
| 0x0056 | KOSTAL Ireland GmbH |
| 0x0057 | LIPOWSKY Industrie-Elektronik GmbH  |
| 0x0058 | Sanken Electric Co.,Ltd |
| 0x0059 | Elektrobit Automotive GmbH |
| 0x005A | VIMERCATI S.p.A. |
| 0x005B | AB Volvo |
| 0x005C | SMSC Europe GmbH |
| 0x0060 | Sitronic |
| 0x0061 | Flextronics / Sidler Automotive |
| 0x0062 | EAO Automotive |
| 0x0063 | helag-electronic |
| 0x0064 | Magna International |
| 0x0065 | ARVINMERITOR |
| 0x0067 | Defond Holding / BJAutomotive |
| 0xFFFF | unbekannter Hersteller |

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

Dimensions: 11 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelag vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x06 | Br_h | Bremsbelag hinten |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x15 | Efk | Einfahrkontrolle |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |
| 0x0D | NOx_a | NOx-Additiv |
| 0x64 | Sic_v | Sichtpruefung/Fahrzeug-Check verknuepft |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 8 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | Allgemeiner Fertigungs- und Energiesparmode  | Allgemeiner Fertigungs- und Energiesparmode  |
| 0x01 | Spezieller Energiesparmode | Spezieller Energiesparmode |
| 0x02 | ECOS-Mode | ECOS-Mode |
| 0x03 | MOST-Mode | MOST-Mode |
| 0x04 | Betriebsmode 4 | Betriebsmode 4 |
| 0x05 | Betriebsmode 5 | Betriebsmode 5 |
| 0x06 | Rollenmode | Rollenmode |
| 0xFF | ungültiger Betriebsmodus | ungültig |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 849 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x000000 | 000000 FehlerOrt nicht bedatet | 0 |
| 0x021200 | 0x021200 Energiesparmode: aktiv | 0 |
| 0x02FF12 | 0x02FF12 Dummy Application DTC: application DTC | 0 |
| 0x100001 | 0x100001 Drosselklappe, Funktion: klemmt kurzzeitig | 0 |
| 0x100101 | 0x100101 Drosselklappe, Funktion: klemmt dauerhaft | 0 |
| 0x100201 | 0x100201 Drosselklappe, Funktion: schwergängig, zu langsam | 0 |
| 0x100210 | 0x100210 Drosselklappensteller, Positionsüberwachung: Lageabweichung | 0 |
| 0x100A02 | 0x100A02 Drosselklappe, Drosselklappenpotenziometer 1 und 2: Doppelfehler | 0 |
| 0x100A10 | 0x100A10 Drosselklappe, Drosselklappenpotenziometer 1 und 2: Sammelfehler | 0 |
| 0x100C08 | 0x100C08 Drosselklappe, Drosselklappenpotenziometer 1: Signal unplausibel zur Luftmasse | 0 |
| 0x100E08 | 0x100E08 Drosselklappe, Drosselklappenpotenziometer 2: Signal unplausibel zur Luftmasse | 0 |
| 0x101001 | 0x101001 Drosselklappe, Drosselklappenpotenziometer 1, elektrisch: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x101002 | 0x101002 Drosselklappe, Drosselklappenpotenziometer 1, elektrisch: Kurzschluss nach Masse | 0 |
| 0x101201 | 0x101201 Drosselklappe, Drosselklappenpotenziometer 2, elektrisch: Kurzschluss nach Plus | 0 |
| 0x101202 | 0x101202 Drosselklappe, Drosselklappenpotenziometer 2, elektrisch: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 |
| 0x101401 | 0x101401 Drosselklappe, Adaption: Randbedingungen nicht erfüllt | 1 |
| 0x101402 | 0x101402 Drosselklappe, Adaption: Notluftposition nicht adaptiert | 0 |
| 0x101408 | 0x101408 Drosselklappe, Adaption: Erstadaption, unterer Anschlag nicht gelernt | 0 |
| 0x101410 | 0x101410 Drosselklappe, Adaption: Randbedingungen nicht erfüllt, Batteriespannung zu niedrig | 1 |
| 0x101C08 | 0x101C08 Drosselklappe, Drosselklappenpotenziometer, Plausibilität: Gleichlauffehler zwischen Poti 1 und Poti 2 | 0 |
| 0x101F01 | 0x101F01 Drosselklappenwinkel - Saugrohrdruck, Korrelation: Grenzwert überschritten | 0 |
| 0x101F02 | 0x101F02 Drosselklappenwinkel - Saugrohrdruck, Korrelation: Grenzwert unterschritten | 0 |
| 0x102010 | 0x102010 Luftmassenmesser, Plausibilität: Luftmasse gegenüber Modell zu hoch | 0 |
| 0x102011 | 0x102011 Luftmassenmesser, Plausibilität: Luftmasse gegenüber Modell zu niedrig | 0 |
| 0x102610 | 0x102610 Luftmassenmesser, Signal: Unplausible Periodendauer, Wackelkontakt mit niedriger Frequenz | 0 |
| 0x102611 | 0x102611 Luftmassenmesser, Signal: Unplausible Periodendauer, Wackelkontakt mit hoher Frequenz | 0 |
| 0x102612 | 0x102612 Luftmassenmesser, Signal: Kurzschluss oder Leitungsunterbrechung | 0 |
| 0x103001 | 0x103001 Fahrpedalmodul, Pedalwertgeber 1, elektrisch: Kurzschluss nach Plus | 0 |
| 0x103002 | 0x103002 Fahrpedalmodul, Pedalwertgeber 1, elektrisch: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 |
| 0x103101 | 0x103101 Fahrpedalmodul, Pedalwertgeber 2, elektrisch: Kurzschluss nach Plus | 0 |
| 0x103102 | 0x103102 Fahrpedalmodul, Pedalwertgeber 2, elektrisch: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 |
| 0x103308 | 0x103308 Fahrpedalmodul, Pedalwertgeber, Plausibilität: Gleichlauffehler zwischen Signal 1 und Signal 2 | 0 |
| 0x10351C | 0x10351C Fahrpedalmodul, Pedalwertgeber: Sammelfehler | 0 |
| 0x104402 | 0x104402 Absolutdrucksensor, Saugrohr, elektrisch: Kurzschluss nach Masse | 0 |
| 0x104610 | 0x104610 Absolutdrucksensor, Saugrohr, Plausibilität: Saugrohrdruck zu hoch | 0 |
| 0x104611 | 0x104611 Absolutdrucksensor, Saugrohr, Plausibilität: Saugrohrdruck zu niedrig | 0 |
| 0x104A40 | 0x104A40 Absolutdrucksensor, Saugrohr, elektrisch: Kurzschluss nach Plus | 0 |
| 0x104B01 | 0x104B01 Absolutdrucksensor, Saugrohr, Sammelfehler: elektrisch und Plausibilität | 0 |
| 0x105001 | 0x105001 Umgebungsdrucksensor, elektrisch: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x105002 | 0x105002 Umgebungsdrucksensor, elektrisch: Kurzschluss nach Masse | 0 |
| 0x105201 | 0x105201 Umgebungsdrucksensor, Nachlauf: Druck zu hoch | 0 |
| 0x105202 | 0x105202 Umgebungsdrucksensor, Nachlauf: Druck zu niedrig | 0 |
| 0x105A30 | 0x105A30 Umgebungsdrucksensor, Sammelfehler: elektrisch und Plausibilität | 0 |
| 0x105A40 | 0x105A40 Umgebungsdrucksensor, Plausibilität: Druck zu hoch | 0 |
| 0x105A41 | 0x105A41 Umgebungsdrucksensor, Plausibilität: Druck zu niedrig | 0 |
| 0x105A42 | 0x105A42 Umgebungsdrucksensor, Plausibilität: Druck unplausibel | 0 |
| 0x105A43 | 0x105A43 Umgebungsdrucksensor, Plausibilität: Druck unplausibel | 0 |
| 0x107A22 | 0x107A22 Drosselklappe, Drosselklappenpotenziometer 1: Signal unplausibel zu Ersatzwert aus Füllung | 0 |
| 0x107A30 | 0x107A30 Drosselklappe, Drosselklappenpotenziometer 2, elektrisch: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x107A31 | 0x107A31 Drosselklappe, Drosselklappenpotenziometer 2, elektrisch: Kurzschluss nach Masse | 0 |
| 0x107A32 | 0x107A32 Drosselklappe, Drosselklappenpotenziometer 2: Signal unplausibel zu Ersatzwert aus Füllung | 0 |
| 0x107A40 | 0x107A40 Drosselklappenpotenziometer: Drosselklappenpotenziometer 1 oder 2, Funktion | 0 |
| 0x107A50 | 0x107A50 Drosselklappe: Notlauf aktiv | 0 |
| 0x107A70 | 0x107A70 DME, interner Fehler, Ansteuerung Drosselklappe: Kurzschluss | 0 |
| 0x107A71 | 0x107A71 DME, interner Fehler, Ansteuerung Drosselklappe: Übertemperatur oder Strom zu hoch | 0 |
| 0x107A72 | 0x107A72 DME, interner Fehler, Ansteuerung Drosselklappe: Interner Kommunikationsfehler | 0 |
| 0x107A73 | 0x107A73 DME, interner Fehler, Ansteuerung Drosselklappe: Leitungsunterbrechung | 0 |
| 0x107A80 | 0x107A80 Drosselklappensteller, schliessende Federprüfung: Abbruch Prüfung, Feder schliesst nicht | 0 |
| 0x107A81 | 0x107A81 Drosselklappensteller, schliessende Federprüfung: Fehler bei Federprüfung | 0 |
| 0x107A90 | 0x107A90 Drosselklappensteller, öffnende Federprüfung: Abbruch Prüfung, Feder öffnet nicht | 0 |
| 0x107A91 | 0x107A91 Drosselklappensteller, öffnende Federprüfung: Fehler bei Federprüfung | 0 |
| 0x107AE0 | 0x107AE0 Drosselklappe, Adaption: Wiederlernen, unterer Anschlag nicht gelernt | 0 |
| 0x107AF0 | 0x107AF0 Drosselklappensteller, Verstärkerabgleich: Fehlfunktion | 0 |
| 0x107C10 | 0x107C10 Laststeuerung, Plausibilität: Massenstrom zu hoch | 0 |
| 0x108001 | 0x108001 Ansauglufttemperatursensor, elektrisch: Kurzschluss nach Plus | 0 |
| 0x108002 | 0x108002 Ansauglufttemperatursensor, elektrisch: Kurzschluss nach Masse | 0 |
| 0x108010 | 0x108010 Ansauglufttemperatursensor, elektrisch: Signal nicht plausibel | 0 |
| 0x108920 | 0x108920 Ladelufttemperatursensor, Kaltstart, Sammelfehler: elektrisch und Plausibilität | 0 |
| 0x108930 | 0x108930 Ladelufttemperatursensor, Kaltstart, Sammelfehler: elektrisch und Plausibilität | 0 |
| 0x108932 | 0x108932 Ansauglufttemperatursensor, Kaltstart, Sammelfehler: elektrisch und Plausibilität | 0 |
| 0x108A01 | 0x108A01 Ladelufttemperatursensor, elektrisch: Kurzschluss nach Plus | 0 |
| 0x108A02 | 0x108A02 Ladelufttemperatursensor, elektrisch: Kurzschluss nach Masse | 0 |
| 0x108A10 | 0x108A10 Ladelufttemperatursensor, elektrisch: Signal nicht plausibel  | 0 |
| 0x108C08 | 0x108C08 Ladelufttemperatursensor, Plausibilität: Signal hängt | 0 |
| 0x108F01 | 0x108F01 Ansaugluftsystem: Verdacht auf Undichtigkeit zwischen Turbolader und Einlassventilen | 0 |
| 0x109001 | 0x109001 Kühlmitteltemperatursensor, elektrisch: Kurzschluss nach Plus oder Leitungsunterbrechung | 0 |
| 0x109002 | 0x109002 Kühlmitteltemperatursensor, elektrisch: Kurzschluss nach Masse | 0 |
| 0x109308 | 0x109308 Kühlmitteltemperatursensor, Plausibilität: Signaländerung zu schnell | 0 |
| 0x10AA20 | 0x10AA20 Kühlmitteltemperatursensor, Kaltstart: Kühlmitteltemperatur zu hoch | 0 |
| 0x10AA21 | 0x10AA21 Kühlmitteltemperatursensor, Kaltstart: Kühlmitteltemperatur zu niedrig | 0 |
| 0x10AA30 | 0x10AA30 Kühlmitteltemperatursensor, Sammelfehler: elektrisch und Signal | 0 |
| 0x10AA40 | 0x10AA40 Kühlmitteltemperatursensor, elektrisch: Signal fehlt | 0 |
| 0x10AA50 | 0x10AA50 Kühlmitteltemperatursensor, Plausibilität: Motortemperatur gegenüber Modell unplausibel zu hoch | 0 |
| 0x10AA51 | 0x10AA51 Kühlmitteltemperatursensor, Plausibilität: Motortemperatur gegenüber Modell unplausibel zu niedrig | 0 |
| 0x10AA52 | 0x10AA52 Kühlmitteltemperatursensor, Plausibilität: Motortemperatur unplausibel | 0 |
| 0x10BA20 | 0x10BA20 Außentemperatursensor, Signal: Oberen Schwellwert überschritten | 0 |
| 0x10BA21 | 0x10BA21 Außentemperatursensor, Signal: Unteren Schwellwert unterschritten | 0 |
| 0x10BA22 | 0x10BA22 Außentemperatursensor, Signal: CAN-Botschaft fehlerhaft | 0 |
| 0x10BA30 | 0x10BA30 Außentemperatursensor, Sammelfehler: elektrisch und Plausibilität | 0 |
| 0x10BA40 | 0x10BA40 Außentemperatursensor, Plausibilität: Umgebungstemperatur größer als Modelltemperatur | 0 |
| 0x10BA41 | 0x10BA41 Außentemperatursensor, Plausibilität: Umgebungstemperatur kleiner als Modelltemperatur | 0 |
| 0x10BA42 | 0x10BA42 Ansauglufttemperatursensor, Kaltstart: Ansauglufttemperatur zu hoch | 0 |
| 0x10BA43 | 0x10BA43 Ansauglufttemperatursensor, Kaltstart: Ansauglufttemperatur zu niedrig | 0 |
| 0x10BA48 | 0x10BA48 Ansauglufttemperatursensor, Plausibilität: Ansauglufttemperatur zu hoch | 0 |
| 0x10BA49 | 0x10BA49 Ansauglufttemperatursensor, Plausibilität: Ansauglufttemperatur zu niedrig | 0 |
| 0x10BA4A | 0x10BA4A Ladelufttemperatursensor, Kaltstart: Ladelufttemperatur zu hoch | 0 |
| 0x10BA4B | 0x10BA4B Ladelufttemperatursensor, Kaltstart: Ladelufttemperatur zu niedrig | 0 |
| 0x10BA4F | 0x10BA4F Ladelufttemperatursensor, Plausibilität: Ladelufttemperatur zu hoch | 0 |
| 0x10BA51 | 0x10BA51 Ladelufttemperatursensor, Kaltstart: Sammelfehler | 0 |
| 0x10BA52 | 0x10BA52 Ladelufttemperatursensor, Sammelfehler: Plausibilität | 0 |
| 0x10C005 | 0x10C005 Ladelufttemperatursensor, Gradient: Anstieg zu hoch | 0 |
| 0x110101 | 0x110101 Injektor Zylinder 1, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 |
| 0x110102 | 0x110102 Injektor Zylinder 1, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 |
| 0x110104 | 0x110104 Injektor Zylinder 1, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 |
| 0x110108 | 0x110108 Injektor Zylinder 1, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 |
| 0x110201 | 0x110201 Injektor Zylinder 2, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 |
| 0x110202 | 0x110202 Injektor Zylinder 2, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 |
| 0x110204 | 0x110204 Injektor Zylinder 2, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 |
| 0x110208 | 0x110208 Injektor Zylinder 2, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 |
| 0x110301 | 0x110301 Injektor Zylinder 3, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 |
| 0x110302 | 0x110302 Injektor Zylinder 3, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 |
| 0x110304 | 0x110304 Injektor Zylinder 3, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 |
| 0x110308 | 0x110308 Injektor Zylinder 3, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 |
| 0x110401 | 0x110401 Injektor Zylinder 4, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 |
| 0x110402 | 0x110402 Injektor Zylinder 4, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 |
| 0x110404 | 0x110404 Injektor Zylinder 4, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 |
| 0x110408 | 0x110408 Injektor Zylinder 4, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 |
| 0x110501 | 0x110501 Injektor Zylinder 5, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 |
| 0x110502 | 0x110502 Injektor Zylinder 5, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 |
| 0x110504 | 0x110504 Injektor Zylinder 5, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 |
| 0x110508 | 0x110508 Injektor Zylinder 5, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 |
| 0x110601 | 0x110601 Injektor Zylinder 6, Ansteuerung: Hochspannungsseite; Kurzschluss nach Masse | 0 |
| 0x110602 | 0x110602 Injektor Zylinder 6, Ansteuerung: Niederspannungsseite; Kurzschluss nach Plus | 0 |
| 0x110604 | 0x110604 Injektor Zylinder 6, Ansteuerung: Hochspannungsseite; Kurzschluss nach Plus | 0 |
| 0x110608 | 0x110608 Injektor Zylinder 6, Ansteuerung: Niederspannungsseite; Kurzschluss nach Masse | 0 |
| 0x111020 | 0x111020 Injektor Zylinder 1 Hochspannungsseite, Ansteuerung: Windungsschluss | 0 |
| 0x111021 | 0x111021 Injektor Zylinder 2 Hochspannungsseite, Ansteuerung: Windungsschluss | 0 |
| 0x111022 | 0x111022 Injektor Zylinder 3 Hochspannungsseite, Ansteuerung: Windungsschluss | 0 |
| 0x111023 | 0x111023 Injektor Zylinder 4 Hochspannungsseite, Ansteuerung: Windungsschluss | 0 |
| 0x111024 | 0x111024 Injektor Zylinder 5 Hochspannungsseite, Ansteuerung: Windungsschluss | 0 |
| 0x111025 | 0x111025 Injektor Zylinder 6 Hochspannungsseite, Ansteuerung: Windungsschluss | 0 |
| 0x111030 | 0x111030 Injektor Zylinder 1 Niederspannungsseite, Ansteuerung: Boosterzeitfenster | 0 |
| 0x111031 | 0x111031 Injektor Zylinder 2 Niederspannungsseite, Ansteuerung: Boosterzeitfenster | 0 |
| 0x111032 | 0x111032 Injektor Zylinder 3 Niederspannungsseite, Ansteuerung: Boosterzeitfenster | 0 |
| 0x111033 | 0x111033 Injektor Zylinder 4 Niederspannungsseite, Ansteuerung: Boosterzeitfenster | 0 |
| 0x111034 | 0x111034 Injektor Zylinder 5 Niederspannungsseite, Ansteuerung: Boosterzeitfenster | 0 |
| 0x111035 | 0x111035 Injektor Zylinder 6 Niederspannungsseite, Ansteuerung: Boosterzeitfenster | 0 |
| 0x111040 | 0x111040 Injektor Zylinder 1 Niederspannungsseite, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x111041 | 0x111041 Injektor Zylinder 2 Niederspannungsseite, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x111042 | 0x111042 Injektor Zylinder 3 Niederspannungsseite, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x111043 | 0x111043 Injektor Zylinder 4 Niederspannungsseite, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x111044 | 0x111044 Injektor Zylinder 5 Niederspannungsseite, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x111045 | 0x111045 Injektor Zylinder 6 Niederspannungsseite, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x111050 | 0x111050 Injektor Zylinder 1, mechanisch: Ventil klemmt offen | 0 |
| 0x111051 | 0x111051 Injektor Zylinder 2, mechanisch: Ventil klemmt offen | 0 |
| 0x111052 | 0x111052 Injektor Zylinder 3, mechanisch: Ventil klemmt offen | 0 |
| 0x111053 | 0x111053 Injektor Zylinder 4, mechanisch: Ventil klemmt offen | 0 |
| 0x111054 | 0x111054 Injektor Zylinder 5, mechanisch: Ventil klemmt offen | 0 |
| 0x111055 | 0x111055 Injektor Zylinder 6, mechanisch: Ventil klemmt offen | 0 |
| 0x111060 | 0x111060 Injektor Zylinder 1 und 2, elektrisch: Einspritzventil 1 oder 2 klemmt offen | 0 |
| 0x111061 | 0x111061 Injektor Zylinder 3 und 4, elektrisch: Einspritzventil 3 oder 4 klemmt offen | 0 |
| 0x111110 | 0x111110 DME, interner Fehler, HDEV-Endstufen-Baustein 1: SPI-Kommunikation fehlerhaft | 0 |
| 0x111111 | 0x111111 DME, interner Fehler, HDEV-Endstufen-Baustein 2: SPI-Kommunikation fehlerhaft | 0 |
| 0x111112 | 0x111112 DME, interner Fehler, HDEV-Endstufen-Baustein 1: SPI-Kommunikation unplausibel | 0 |
| 0x111113 | 0x111113 DME, interner Fehler, HDEV-Endstufen-Baustein 2: SPI-Kommunikation unplausibel | 0 |
| 0x111114 | 0x111114 DME, interner Fehler, HDEV-Endstufen-Baustein 1: SPI-Kommunikation, Signalfehler | 0 |
| 0x111115 | 0x111115 DME, interner Fehler, HDEV-Endstufen-Baustein 2: SPI-Kommunikation, Signalfehler | 0 |
| 0x111116 | 0x111116 Injektor Zylinder 5 und 6, elektrisch: Einspritzventil 5 oder 6 klemmt offen | 0 |
| 0x111117 | 0x111117 Injektor Zylinder 7 und 8, elektrisch: Einspritzventil 7 oder 8 klemmt offen | 0 |
| 0x113025 | 0x113025 Injektoren, Spannungsversorgung: Kurzschluss nach Plus | 0 |
| 0x113026 | 0x113026 Injektoren, Spannungsversorgung: Kurzschluss nach Masse | 0 |
| 0x113027 | 0x113027 Injektoren, Spannungsversorgung: Leitungsunterbrechung | 0 |
| 0x118601 | 0x118601 Lambdasonde vor Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu fett | 0 |
| 0x118602 | 0x118602 Lambdasonde vor Katalysator, Gemischfeinregelung: Abgas nach Katalysator zu mager | 0 |
| 0x118C02 | 0x118C02 Gemischadaption, Injektor-Alterung: Zylinderseite 1: langfristige Adaption zu hoch | 0 |
| 0x118E01 | 0x118E01 Gemischadaption, Leerlauf: Gemisch zu mager | 0 |
| 0x118E02 | 0x118E02 Gemischadaption, Leerlauf: Gemisch zu fett | 0 |
| 0x118F20 | 0x118F20 Gemischadaption, unterer Drehzahlbereich: Gemisch in Teillast zu mager | 0 |
| 0x118F21 | 0x118F21 Gemischadaption, unterer Drehzahlbereich: Gemisch in Teillast zu fett | 0 |
| 0x119001 | 0x119001 Raildrucksensor, elektrisch: Kurzschluss nach Plus | 0 |
| 0x119002 | 0x119002 Raildrucksensor, elektrisch: Kurzschluss nach Masse | 0 |
| 0x119201 | 0x119201 Kraftstoffniederdrucksensor, elektrisch: Kurzschluss nach Plus | 0 |
| 0x119202 | 0x119202 Kraftstoffniederdrucksensor, elektrisch: Kurzschluss nach Masse | 0 |
| 0x119301 | 0x119301 Raildrucksensor, Spannungsprüfung: obere Schwelle überschritten | 0 |
| 0x119302 | 0x119302 Raildrucksensor, Spannungsprüfung: untere Schwelle unterschritten | 0 |
| 0x119304 | 0x119304 Raildrucksensor, Plausibilität: Maximaldruck überschritten | 0 |
| 0x119308 | 0x119308 Raildrucksensor, Plausibilität: Minimaldruck unterschritten | 0 |
| 0x119404 | 0x119404 Raildrucksensor, Plausibilität: Signal hängt | 0 |
| 0x11A001 | 0x11A001 Kraftstoffhochdrucksystem, Kraftstoffdruck: Maximaldruck überschritten | 0 |
| 0x11A002 | 0x11A002 Kraftstoffhochdrucksystem, Kraftstoffdruck: Minimaldruck unterschritten | 0 |
| 0x11A210 | 0x11A210 Kraftstoffniederdrucksystem: Leistung elektrische Kraftstoffpumpe für Istdruck zu hoch | 0 |
| 0x11A211 | 0x11A211 Kraftstoffniederdrucksystem: Leistung elektrische Kraftstoffpumpe für Istdruck zu niedrig | 0 |
| 0x11A301 | 0x11A301 Kraftstoffhochdruck nach Motorstopp: Druck zu hoch | 0 |
| 0x11A401 | 0x11A401 Kraftstoffhochdruck bei Freigabe der Einspritzung: Druck zu niedrig | 0 |
| 0x11AA01 | 0x11AA01 Kraftstoffversorgungssystem: Druck zu hoch, Notlauf mit Niederdruck | 0 |
| 0x11AA02 | 0x11AA02 Kraftstoffversorgungssystem: Druck zu hoch, Notlauf mit Einspritzabschaltung | 0 |
| 0x11AA04 | 0x11AA04 Kraftstoffversorgungssystem: Druck kurzzeitig zu hoch, Drehzahl- und Lastbegrenzung | 0 |
| 0x11AB01 | 0x11AB01 Kraftstoffhochdrucksystem, Plausibilität: Regelabweichung des Mengensteuerventils zu groß | 0 |
| 0x11AB02 | 0x11AB02 Kraftstoffhochdrucksystem, Plausibilität: Regelabweichung des Mengensteuerventils zu klein | 0 |
| 0x11AC01 | 0x11AC01 Kraftstoffhochdrucksystem, Kaltstart: Druck zu hoch | 0 |
| 0x11AC02 | 0x11AC02 Kraftstoffhochdrucksystem, Kaltstart: Druck zu niedrig | 0 |
| 0x11AD10 | 0x11AD10 Kraftstoffdruck: Minimaldruck unterschritten, Einspritzabschaltung zum Katschutz | 0 |
| 0x11AE01 | 0x11AE01 Kraftstoffversorgungssytem, Lambdaregelung: obere Grenze überschritten | 0 |
| 0x11AE02 | 0x11AE02 Kraftstoffversorgungssytem, Lambdaregelung: untere Grenze unterschritten | 0 |
| 0x11B209 | 0x11B209 Kraftstoffniederdrucksystem: allgemeiner Fehler | 0 |
| 0x11B210 | 0x11B210 Kraftstoffniederdrucksystem, Signal: Spannung elektrische Kraftstoffpumpe unplausibel | 0 |
| 0x11B211 | 0x11B211 Kraftstoffniederdrucksystem, Regelung: Istdruck zu niedrig | 0 |
| 0x11B212 | 0x11B212 Kraftstoffniederdrucksystem, Regelung: Istdruck zu hoch | 0 |
| 0x11C401 | 0x11C401 Mengensteuerventil, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x11C402 | 0x11C402 Mengensteuerventil, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x11C404 | 0x11C404 Mengensteuerventil, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x11CF30 | 0x11CF30 Kraftstoffversorgungssystem, Sammelfehler: Gemischadaption im Leerlauf und unteren Drehzahlbereich | 0 |
| 0x120208 | 0x120208 Ladedruckregelung, oberer Wert: Ladedruck zu hoch | 0 |
| 0x120308 | 0x120308 Ladedruckregelung, unterer Wert: Ladedruck zu niedrig | 0 |
| 0x120408 | 0x120408 Ladedruckregelung, Abschaltung: Ladedruckaufbau gesperrt | 0 |
| 0x121001 | 0x121001 Ladedrucksensor, elektrisch: Kurzschluss nach Plus | 0 |
| 0x121002 | 0x121002 Ladedrucksensor, elektrisch: Kurzschluss nach Masse | 0 |
| 0x121521 | 0x121521 Ladedrucksensor, Sammelfehler: elektrisch und Plausibilität | 0 |
| 0x121530 | 0x121530 Ladedrucksensor, Plausibilität: Druck vor Drosselklappe zu hoch | 0 |
| 0x121531 | 0x121531 Ladedrucksensor, Plausibilität: Druck vor Drosselklappe zu niedrig | 0 |
| 0x121532 | 0x121532 Ladedrucksensor, Plausibilität: Druck vor Drosselklappe bei Motorstillstand zu hoch | 0 |
| 0x121533 | 0x121533 Ladedrucksensor, Plausibilität: Druck vor Drosselklappe bei Motorstillstand zu niedrig | 0 |
| 0x121601 | 0x121601 Ladedrucksensor: Druck zu hoch | 0 |
| 0x121602 | 0x121602 Ladedrucksensor: Druck zu niedrig | 0 |
| 0x122001 | 0x122001 Schubumluftventil, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x122002 | 0x122002 Schubumluftventil, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x122004 | 0x122004 Schubumluftventil, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x122108 | 0x122108 Schubumluftventil, Mechanik: klemmt geschlossen | 0 |
| 0x122201 | 0x122201 Schubumluftventil, Mechanik: Verdacht auf offen klemmendes Schubumluftventil | 0 |
| 0x123001 | 0x123001 Wastegate, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x123002 | 0x123002 Wastegate, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x123004 | 0x123004 Wastegate, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x123201 | 0x123201 Wastegate, Ansteuerung: Verdacht auf Fehler in der Wastegateansteuerung | 0 |
| 0x128101 | 0x128101 Lambdasonde vor Katalysator, Systemprüfung: Signal festliegend auf Mager | 0 |
| 0x128301 | 0x128301 Lambdasonde vor Katalysator, Systemprüfung: Signal festliegend auf Fett | 0 |
| 0x128501 | 0x128501 Lambdasonde vor Katalysator, im Schub: Signal außerhalb Grenzwert | 0 |
| 0x128901 | 0x128901 Lambdasonde vor Katalysator, Dynamik: langsame Reaktion | 0 |
| 0x128B01 | 0x128B01 Lambdasonde vor Katalysator, Verbau: Sonde nicht angesteckt | 0 |
| 0x128E01 | 0x128E01 Lambdasonde vor Katalysator, Leitungsfehler: Unterbrechung Nernstleitung | 0 |
| 0x128E08 | 0x128E08 Lambdasonde vor Katalysator, Leitungsfehler: Unterbrechung Abgleichleitung | 0 |
| 0x129001 | 0x129001 Lambdasonde vor Katalysator, Signalleitungen: Kurzschluss nach Plus | 0 |
| 0x129002 | 0x129002 Lambdasonde vor Katalysator, Signalleitungen: Kurzschluss nach Masse | 0 |
| 0x129201 | 0x129201 DME, interner Fehler, Lambdasonde vor Katalysator: Initialisierungsfehler | 0 |
| 0x129202 | 0x129202 DME, interner Fehler, Lambdasonde vor Katalysator: Kommunikationsfehler | 0 |
| 0x129801 | 0x129801 Lambdasonde nach Katalysator, Dynamik: langsame Reaktion | 0 |
| 0x129A20 | 0x129A20 DME, interner Fehler, Lambdasonde vor Katalysator: Lambdasondenbaustein, Signalkreisadaptionswerte zu hoch | 0 |
| 0x129A21 | 0x129A21 DME, interner Fehler, Lambdasonde vor Katalysator: Lambdasondenbaustein, Unterspannung | 0 |
| 0x12A101 | 0x12A101 Lambdasonde nach Katalysator, Systemprüfung: Signal festliegend auf Fett | 0 |
| 0x12A102 | 0x12A102 Lambdasonde nach Katalysator, Systemprüfung: Signal festliegend auf Mager | 0 |
| 0x12A308 | 0x12A308 Lambdasonde nach Katalysator, Dynamik, von Fett nach Mager: langsame Reaktion | 0 |
| 0x12A701 | 0x12A701 Lambdasonde nach Katalysator, elektrisch: Kurzschluss nach Plus | 0 |
| 0x12A902 | 0x12A902 Lambdasonde nach Katalysator, elektrisch: Kurzschluss nach Masse | 0 |
| 0x12AB04 | 0x12AB04 Lambdasonde nach Katalysator, elektrisch: Leitungsunterbrechung | 0 |
| 0x12AF08 | 0x12AF08 Lambdasonde nach Katalysator, im Schub, von Fett nach Mager: verzögerte Reaktion | 0 |
| 0x12B101 | 0x12B101 Lambdasondenbeheizung vor Katalysator, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x12B102 | 0x12B102 Lambdasondenbeheizung vor Katalysator, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x12B104 | 0x12B104 Lambdasondenbeheizung vor Katalysator, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x12B301 | 0x12B301 Lambdasondenbeheizung nach Katalysator, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x12B302 | 0x12B302 Lambdasondenbeheizung nach Katalysator, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x12B304 | 0x12B304 Lambdasondenbeheizung nach Katalysator, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x12B505 | 0x12B505 Lambdasondenbeheizung vor Katalysator, Funktion: Heizerfehler | 0 |
| 0x12B701 | 0x12B701 Lambdasondenbeheizung nach Katalysator, Funktion: Innenwiderstand zu hoch | 0 |
| 0x12BD20 | 0x12BD20 Lambdasondenbeheizung vor Katalysator, Funktion: Betriebstemperatur nicht erreicht | 0 |
| 0x12BD21 | 0x12BD21 Lambdasondenbeheizung vor Katalysator, Funktion: Mangelnde Signalbereitschaft | 0 |
| 0x12BD22 | 0x12BD22 Lambdasondenbeheizung vor Katalysator, Funktion: Innenwiderstand des Signalkreises zu hochohmig | 0 |
| 0x12BD33 | 0x12BD33 Lambdasonde nach Katalysator, Alterung: Schubspannungsschwelle nicht erreicht | 0 |
| 0x12BD40 | 0x12BD40 Lambdasonde nach Katalysator, elektrisch: Kurzschluss nach Plus | 0 |
| 0x12BD41 | 0x12BD41 Lambdasonde nach Katalysator, elektrisch: Adernschluss oder Lambdasonde vergiftet | 0 |
| 0x12BD43 | 0x12BD43 Lambdasonde nach Katalysator, elektrisch: Leitungsunterbrechung | 0 |
| 0x12BD50 | 0x12BD50 Lambdasonde vor Katalysator, Pumpstromleitung: Lambdaregelwert oberhalb Schwelle infolge offener Pumpstromleitung | 0 |
| 0x12BD51 | 0x12BD51 Lambdasonde vor Katalysator, Pumpstromleitung: Signalspannung im Schub zu klein infolge offener Pumpstromleitung | 0 |
| 0x12BD52 | 0x12BD52 Lambdasonde vor Katalysator, Leitungsfehler: Unterbrechung Pumpstromleitung | 0 |
| 0x12BD60 | 0x12BD60 Lambdasonde vor Katalysator, Leitungsfehler: Unterbrechung virtuelle Masse | 0 |
| 0x12BD70 | 0x12BD70 Lambdasonde vor Katalysator, elektrisch: Nernstzellenwiderstand oder Keramiktemperatur unplausibel, Leitungs- oder Heizungsfehler | 0 |
| 0x12BD80 | 0x12BD80 Lambdasonde vor Katalysator: Sammelfehler | 0 |
| 0x12BD90 | 0x12BD90 Lambdasonde vor Katalysator, Plausibilität: Gemisch nach Katalysator zu fett | 0 |
| 0x12BD91 | 0x12BD91 Lambdasonde vor Katalysator, Plausibilität: Gemisch nach Katalysator zu mager | 0 |
| 0x12BD92 | 0x12BD92 Lambdasonde vor Katalysator, Plausibilität: festliegend auf mager | 0 |
| 0x12BD93 | 0x12BD93 Lambdasonde vor Katalysator, Plausibilität: festliegend auf fett | 0 |
| 0x130001 | 0x130001 VANOS-Magnetventil Einlass, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x130002 | 0x130002 VANOS-Magnetventil Einlass, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x130004 | 0x130004 VANOS-Magnetventil Einlass, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x130104 | 0x130104 VANOS, Einlass: Regelfehler, Nockenwelle klemmt | 0 |
| 0x130108 | 0x130108 VANOS, Einlass: Regelfehler, Position nicht erreicht | 0 |
| 0x130201 | 0x130201 VANOS-Magnetventil Auslass, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x130202 | 0x130202 VANOS-Magnetventil Auslass, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x130204 | 0x130204 VANOS-Magnetventil Auslass, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x130304 | 0x130304 VANOS, Auslass: Regelfehler, Nockenwelle klemmt | 0 |
| 0x130308 | 0x130308 VANOS, Auslass: Regelfehler, Position nicht erreicht | 0 |
| 0x130E11 | 0x130E11 Einlassnockenwellensensor: Signal unplausibel | 0 |
| 0x130E20 | 0x130E20 Einlassnockenwelle: Winkelversatz zur Kurbelwelle außerhalb Toleranz | 0 |
| 0x130F11 | 0x130F11 Auslassnockenwellensensor: Signal unplausibel | 0 |
| 0x130F20 | 0x130F20 Auslassnockenwelle: Winkelversatz zur Kurbelwelle außerhalb Toleranz | 0 |
| 0x131401 | 0x131401 VANOS, Auslass, Kaltstart: nicht regelbar | 0 |
| 0x131501 | 0x131501 VANOS, Einlass, Kaltstart: nicht regelbar | 0 |
| 0x132101 | 0x132101 VANOS, Auslass, Sammelfehler: elektrisch oder mechanisch | 0 |
| 0x132201 | 0x132201 VANOS, Einlass, Sammelfehler: elektrisch oder mechanisch | 0 |
| 0x132301 | 0x132301 VANOS, Sammelfehler: elektrisch oder mechanisch | 0 |
| 0x132408 | 0x132408 VANOS, Auslass: Nockenwelle beim Start nicht in Verriegelungsposition | 0 |
| 0x132508 | 0x132508 VANOS, Einlass: Nockenwelle beim Start nicht in Verriegelungsposition | 0 |
| 0x133101 | 0x133101 Valvetronic Relais, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x133102 | 0x133102 Valvetronic Relais, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x133104 | 0x133104 Valvetronic Relais, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x133201 | 0x133201 Valvetronic-Stellmotor, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x133202 | 0x133202 Valvetronic-Stellmotor, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x133206 | 0x133206 Valvetronic-Stellmotor, Ansteuerung: Abschaltung im Fahrbetrieb | 0 |
| 0x133208 | 0x133208 Valvetronic-Stellmotor, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x133710 | 0x133710 Valvetronic, Exzenterwellenadaption: unterer Anschlag erreicht | 0 |
| 0x134F01 | 0x134F01 Valvetronic, Verstellbereich: Urlernen ausserhalb Toleranzen | 0 |
| 0x134F02 | 0x134F02 Valvetronic, Verstellbereich: Anschlag nicht gelernt | 0 |
| 0x134F04 | 0x134F04 Valvetronic, Verstellbereich: Fehler Bereichsüberprüfung | 0 |
| 0x134F08 | 0x134F08 Valvetronic, Verstellbereich: Bereichsüberprüfung Abweichung zu Urlernen | 0 |
| 0x134F10 | 0x134F10 Valvetronic, Verstellbereich: Anschlag nicht gelernt wegen Umweltbedingungen | 1 |
| 0x135301 | 0x135301 Valvetronic, Bauteileschutz Endstufe: Abschaltung System | 0 |
| 0x135302 | 0x135302 Valvetronic, Bauteileschutz Stellmotor: Abschaltung System | 0 |
| 0x135401 | 0x135401 Valvetronic, Überlastschutz: Endstufe überlastet | 0 |
| 0x135402 | 0x135402 Valvetronic, Überlastschutz: Stellmotor überlastet | 0 |
| 0x135501 | 0x135501 Valvetronic, Überlastschutz: Warnschwelle Endstufe überschritten | 0 |
| 0x135502 | 0x135502 Valvetronic, Überlastschutz: Warnschwelle Stellmotor überschritten | 0 |
| 0x135604 | 0x135604 Valvetronic System: Regelabweichung zu gross | 0 |
| 0x135608 | 0x135608 Valvetronic System: keine Bewegung erkannt | 0 |
| 0x135704 | 0x135704 Valvetronic System: Warnschwelle Regelabweichung überschritten | 0 |
| 0x135808 | 0x135808 Valvetronic-Stellmotor, Positionssensoren: Kurzschluss oder Leitungsunterbrechung | 0 |
| 0x135908 | 0x135908 Valvetronic-Stellmotor, Positionssensoren: Versorgungsspannung fehlerhaft | 0 |
| 0x135A08 | 0x135A08 Valvetronic-Stellmotor, Positionssensoren: Signal unplausibel | 0 |
| 0x135A10 | 0x135A10 Valvetronic-Stellmotor, Positionssensoren: Exzenterwinkel falsch | 0 |
| 0x135B10 | 0x135B10 Valvetronic-Stellmotor, Ansteuerung Phase U: Leitungsunterbrechung | 0 |
| 0x135B11 | 0x135B11 Valvetronic-Stellmotor, Ansteuerung Phase V: Leitungsunterbrechung | 0 |
| 0x135B12 | 0x135B12 Valvetronic-Stellmotor, Ansteuerung Phase W: Leitungsunterbrechung | 0 |
| 0x135C10 | 0x135C10 Valvetronic-Stellmotor, Positionssensoren: Fehler erkannt | 0 |
| 0x135C11 | 0x135C11 Valvetronic-Stellmotor, Positionssensoren: Signale unplausibel | 0 |
| 0x138101 | 0x138101 Abgasklappe, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x138102 | 0x138102 Abgasklappe, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x138104 | 0x138104 Abgasklappe, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x138201 | 0x138201 Kühlerjalousie, oben, Versorgungsspannung Steller: Spannungsfehler | 0 |
| 0x138301 | 0x138301 Kühlerjalousie, oben, Übertemperatur Steller: Grenzwert überschritten | 0 |
| 0x138401 | 0x138401 Kühlerjalousie, oben, Steller intern: elektrischer Fehler | 0 |
| 0x138501 | 0x138501 Kühlerjalousie, oben, unterer Anschlag: wird nicht erkannt | 0 |
| 0x138601 | 0x138601 Kühlerjalousie, oben, oberer Anschlag: wird nicht erkannt | 0 |
| 0x138701 | 0x138701 Kühlerjalousie, oben, oberer Anschlag: zu früh erkannt | 0 |
| 0x138901 | 0x138901 Kühlerjalousie, unten, elektrisch: Kurzschluss nach Plus | 0 |
| 0x138902 | 0x138902 Kühlerjalousie, unten, elektrisch: Kurzschluss nach Masse | 0 |
| 0x138904 | 0x138904 Kühlerjalousie, unten, elektrisch: Leitungsunterbrechung | 0 |
| 0x140001 | 0x140001 Verbrennungsaussetzer, mehrere Zylinder: Einspritzung wird abgeschaltet | 0 |
| 0x140002 | 0x140002 Verbrennungsaussetzer, mehrere Zylinder: abgasschädigend nach Startvorgang | 0 |
| 0x140004 | 0x140004 Verbrennungsaussetzer, mehrere Zylinder: abgasschädigend | 0 |
| 0x140101 | 0x140101 Verbrennungsaussetzer, Zylinder 1: Einspritzung wird abgeschaltet | 0 |
| 0x140102 | 0x140102 Verbrennungsaussetzer, Zylinder 1: abgasschädigend nach Startvorgang | 0 |
| 0x140104 | 0x140104 Verbrennungsaussetzer, Zylinder 1: abgasschädigend | 0 |
| 0x140201 | 0x140201 Verbrennungsaussetzer, Zylinder 2: Einspritzung wird abgeschaltet | 0 |
| 0x140202 | 0x140202 Verbrennungsaussetzer, Zylinder 2: abgasschädigend nach Startvorgang | 0 |
| 0x140204 | 0x140204 Verbrennungsaussetzer, Zylinder 2: abgasschädigend | 0 |
| 0x140301 | 0x140301 Verbrennungsaussetzer, Zylinder 3: Einspritzung wird abgeschaltet | 0 |
| 0x140302 | 0x140302 Verbrennungsaussetzer, Zylinder 3: abgasschädigend nach Startvorgang | 0 |
| 0x140304 | 0x140304 Verbrennungsaussetzer, Zylinder 3: abgasschädigend | 0 |
| 0x140401 | 0x140401 Verbrennungsaussetzer, Zylinder 4: Einspritzung wird abgeschaltet | 0 |
| 0x140402 | 0x140402 Verbrennungsaussetzer, Zylinder 4: abgasschädigend nach Startvorgang | 0 |
| 0x140404 | 0x140404 Verbrennungsaussetzer, Zylinder 4: abgasschädigend | 0 |
| 0x140501 | 0x140501 Verbrennungsaussetzer, Zylinder 5: Einspritzung wird abgeschaltet | 0 |
| 0x140502 | 0x140502 Verbrennungsaussetzer, Zylinder 5: abgasschädigend nach Startvorgang | 0 |
| 0x140504 | 0x140504 Verbrennungsaussetzer, Zylinder 5: abgasschädigend | 0 |
| 0x140601 | 0x140601 Verbrennungsaussetzer, Zylinder 6: Einspritzung wird abgeschaltet | 0 |
| 0x140602 | 0x140602 Verbrennungsaussetzer, Zylinder 6: abgasschädigend nach Startvorgang | 0 |
| 0x140604 | 0x140604 Verbrennungsaussetzer, Zylinder 6: abgasschädigend | 0 |
| 0x143201 | 0x143201 Laufunruhe, Füllung Einzelzylinder: Momentenbeitrag zu niedrig | 0 |
| 0x150102 | 0x150102 Zündung, Zylinder 1: Brenndauer zu kurz | 0 |
| 0x150202 | 0x150202 Zündung, Zylinder 2: Brenndauer zu kurz | 0 |
| 0x150302 | 0x150302 Zündung, Zylinder 3: Brenndauer zu kurz | 0 |
| 0x150402 | 0x150402 Zündung, Zylinder 4: Brenndauer zu kurz | 0 |
| 0x150502 | 0x150502 Zündung, Zylinder 5: Brenndauer zu kurz | 0 |
| 0x150602 | 0x150602 Zündung, Zylinder 6: Brenndauer zu kurz | 0 |
| 0x151001 | 0x151001 Zündwinkelverstellung im Leerlauf, Kaltstart: Zündwinkel zu früh | 0 |
| 0x151101 | 0x151101 Zündwinkelverstellung in Teillast, Kaltstart: Zündwinkel zu früh | 0 |
| 0x152001 | 0x152001 Zündung, Spannungsversorgung: Kurzschluss nach Plus | 0 |
| 0x152007 | 0x152007 Zündung, Spannungsversorgung: Leitungsunterbrechung oder Kurzschluss nach Masse | 0 |
| 0x152009 | 0x152009 Zündkreis, Versorgungsspannung: Bank- oder Motorausfall | 0 |
| 0x152108 | 0x152108 Superklopfen Zylinder 1: Einspritzungsabschaltung | 0 |
| 0x152208 | 0x152208 Superklopfen Zylinder 2: Einspritzungsabschaltung | 0 |
| 0x152308 | 0x152308 Superklopfen Zylinder 3: Einspritzungsabschaltung | 0 |
| 0x152408 | 0x152408 Superklopfen Zylinder 4: Einspritzungsabschaltung | 0 |
| 0x152508 | 0x152508 Superklopfen Zylinder 5: Einspritzungsabschaltung | 0 |
| 0x152608 | 0x152608 Superklopfen Zylinder 6: Einspritzungsabschaltung | 0 |
| 0x152D08 | 0x152D08 Superklopfen: Einspritzungsabschaltung | 0 |
| 0x160001 | 0x160001 Kurbelwellensensor, Signal: fehlt | 0 |
| 0x160020 | 0x160020 Kurbelwellensensor: Gestörtes Kurbelwellensignal | 0 |
| 0x160510 | 0x160510 Kurbelwellensensor, Abstellposition: unplausibel | 0 |
| 0x164020 | 0x164020 Einlassnockenwellensensor: Signal hoch | 0 |
| 0x164021 | 0x164021 Einlassnockenwellensensor: Signal niedrig | 0 |
| 0x164030 | 0x164030 Auslassnockenwellensensor: Signal hoch | 0 |
| 0x164031 | 0x164031 Auslassnockenwellensensor: Signal niedrig | 0 |
| 0x164040 | 0x164040 Einlassnockenwelle, Mechanik: Montage fehlerhaft | 0 |
| 0x164041 | 0x164041 Auslassnockenwelle, Mechanik: Montage fehlerhaft | 0 |
| 0x168A20 | 0x168A20 Klopfregelung, Fehlerprüfung: Fehlfunktion, Systemfehler | 0 |
| 0x168A30 | 0x168A30 Klopfsensor, elektrisch: Signal-Eingang A, Kurzschluss nach Plus | 0 |
| 0x168A31 | 0x168A31 Klopfsensor, elektrisch: Signal-Eingang A, Kurzschluss nach Masse | 0 |
| 0x168A40 | 0x168A40 Klopfsensor, elektrisch: Signal-Eingang B, Kurzschluss nach Plus | 0 |
| 0x168A41 | 0x168A41 Klopfsensor, elektrisch: Signal-Eingang B, Kurzschluss nach Masse | 0 |
| 0x168A50 | 0x168A50 Klopfsensor 2, elektrisch: Signal-Eingang A, Kurzschluss nach Plus | 0 |
| 0x168A51 | 0x168A51 Klopfsensor 2, elektrisch: Signal-Eingang A, Kurzschluss nach Masse | 0 |
| 0x168A60 | 0x168A60 Klopfsensor 2, elektrisch: Signal-Eingang B, Kurzschluss nach Plus | 0 |
| 0x168A61 | 0x168A61 Klopfsensor 2, elektrisch: Signal-Eingang B, Kurzschluss nach Masse | 0 |
| 0x168A70 | 0x168A70 Klopfsensor, Signal: Motor mechanisch zu laut oder KS außerhalb Toleranz (Empfindlichkeit) | 0 |
| 0x168A71 | 0x168A71 Klopfsensor, Signal: Elektrischer Fehler KS (Wackelkontakt) oder KS locker | 0 |
| 0x168A80 | 0x168A80 Klopfsensor 2, Signal: Motor mechanisch zu laut oder KS außerhalb Toleranz (Empfindlichkeit) | 0 |
| 0x168A81 | 0x168A81 Klopfsensor 2, Signal: Elektrischer Fehler KS (Wackelkontakt) oder KS locker | 0 |
| 0x180001 | 0x180001 Katalysator: Wirkungsgrad unterhalb Grenzwert | 0 |
| 0x190001 | 0x190001 DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x190002 | 0x190002 DMTL-Magnetventil, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x190004 | 0x190004 DMTL-Magnetventil, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x190201 | 0x190201 Tankentlüftungs- und Spülluftsystem, Feinleck: Leckage größer 1, 0 mm | 0 |
| 0x190302 | 0x190302 Tankentlüftungs- und Spülluftsystem, Feinstleck: Leckage größer 0, 5 mm | 0 |
| 0x190401 | 0x190401 DMTL, Systemfehler: Pumpenstrom zu groß bei Referenzmessung | 0 |
| 0x190402 | 0x190402 DMTL, Systemfehler: Pumpenstrom zu klein bei Referenzmessung | 0 |
| 0x190404 | 0x190404 DMTL, Systemfehler: Abbruch wegen Stromschwankungen bei Referenzmessung | 0 |
| 0x190408 | 0x190408 DMTL, Systemfehler: Pumpenstrom bei Ventilprüfung erreicht Grenzwert | 0 |
| 0x190501 | 0x190501 DMTL, Heizung, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x190502 | 0x190502 DMTL, Heizung, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x190504 | 0x190504 DMTL, Heizung, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x190601 | 0x190601 DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x190702 | 0x190702 DMTL-Leckdiagnosepumpe, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x190704 | 0x190704 DMTL-Leckdiagnosepumpe, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x191001 | 0x191001 Tankentlüftungsventil, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x191002 | 0x191002 Tankentlüftungsventil, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x191004 | 0x191004 Tankentlüftungsventil, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x191A20 | 0x191A20 Tankentlüftungsventil: klemmt geschlossen | 0 |
| 0x191A21 | 0x191A21 Tankentlüftungsventil: klemmt offen | 0 |
| 0x191B01 | 0x191B01 Tankentlüftungssystem Absperrventil, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x191B02 | 0x191B02 Tankentlüftungssystem Absperrventil, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x191B04 | 0x191B04 Tankentlüftungssystem Absperrventil, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x191C01 | 0x191C01 Tankentlüftungssystem Absperrventil: klemmt offen | 0 |
| 0x191C02 | 0x191C02 Tankentlüftungssystem: Fehlfunktion | 0 |
| 0x191C03 | 0x191C03 Tankentlüftungssystem, Nachlauf: Fehlfunktion | 0 |
| 0x191D01 | 0x191D01 Tankentlüftungssystem: Fehlfunktion | 0 |
| 0x192001 | 0x192001 Tankdeckel: nicht korrekt geschlossen | 0 |
| 0x192002 | 0x192002 Tankdeckel: offen im Nachlauf | 0 |
| 0x193002 | 0x193002 Tankfüllstandssensor, links, Signal: Kurzschluss nach Masse | 0 |
| 0x193008 | 0x193008 Tankfüllstandssensor, links, Signal: CAN Wert unplausibel | 0 |
| 0x193011 | 0x193011 Tankfüllstandssensor, rechts, Signal: Kurzschluss nach Plus | 0 |
| 0x193102 | 0x193102 Tankfüllstandssensor, rechts, Signal: Kurzschluss nach Masse | 0 |
| 0x193108 | 0x193108 Tankfüllstandssensor, rechts, Signal: CAN Wert unplausibel | 0 |
| 0x193111 | 0x193111 Tankfüllstandssensor, links, Signal: Kurzschluss nach Plus | 0 |
| 0x193120 | 0x193120 Tankfüllstandssensor, links, Signal: Tankfüllstandsignal unplausibel zu hoch | 0 |
| 0x193218 | 0x193218 Tankfüllstandssensor: Signal unplausibel wegen festhängendem Tankfüllstandsgeber | 0 |
| 0x193220 | 0x193220 Tankfüllstandssensor: Tankfüllstand größer als Tankvolumen | 0 |
| 0x193221 | 0x193221 Tankfüllstandssensor: Abweichung zwischen Verbrauch und Füllstandsänderung | 0 |
| 0x193A20 | 0x193A20 Tankfüllstand, Sammelfehler: Signal und elektrisch | 0 |
| 0x1A2001 | 0x1A2001 Elektrolüfter, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x1A2002 | 0x1A2002 Elektrolüfter, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x1A2004 | 0x1A2004 Elektrolüfter, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x1A2108 | 0x1A2108 Elektrolüfter, Eigendiagnose Stufe 1: leichter Lüfterfehler | 0 |
| 0x1A2308 | 0x1A2308 Elektrolüfter, Eigendiagnose Stufe 2: Lüfterfehler mit potentieller Gefährdung für den Lüfter | 0 |
| 0x1A2408 | 0x1A2408 Elektrolüfter, Eigendiagnose Stufe 3: Lüfterfehler mit Motorfunktionseinschränkung | 0 |
| 0x1A2508 | 0x1A2508 Elektrolüfter, Eigendiagnose Stufe 4: schwerer Lüfterfehler | 0 |
| 0x1A2601 | 0x1A2601 Sicherungsrelais Elektrolüfter, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x1A2602 | 0x1A2602 Sicherungsrelais Elektrolüfter, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x1A2604 | 0x1A2604 Sicherungsrelais Elektrolüfter, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x1A2804 | 0x1A2804 Elektrolüfter, Betriebsbereitschaft: eingeschränkt | 0 |
| 0x1A2904 | 0x1A2904 Elektrolüfter, Betriebsbereitschaft: nicht gegeben | 0 |
| 0x1B0A20 | 0x1B0A20 Schlechtwegstreckenerkennung: Radgeschwindigkeit zu hoch | 0 |
| 0x1B0A21 | 0x1B0A21 Schlechtwegstreckenerkennung: Kein Raddrehzahlsignal erhalten | 0 |
| 0x1B0A40 | 0x1B0A40 Fahrzeuggeschwindigkeit: Signal zu hoch | 0 |
| 0x1B0A50 | 0x1B0A50 Fahrzeuggeschwindigkeit, Sammelfehler: Signal und Plausibilität | 0 |
| 0x1B0A60 | 0x1B0A60 Fahrzeuggeschwindigkeit, Plausibilität: Mindestgeschwindigkeit unter Last nicht erreicht | 0 |
| 0x1B0A61 | 0x1B0A61 Fahrzeuggeschwindigkeit, Plausibilität: Mindestgeschwindigkeit im Schub nicht erreicht | 0 |
| 0x1B0A62 | 0x1B0A62 Fahrzeuggeschwindigkeit, Plausibilität: Unplausibles Geschwindigkeitssignal | 0 |
| 0x1B0A64 | 0x1B0A64 Fahrzeuggeschwindigkeit, Radsensor hinten/links, Plausibilität: Signal unplausibel | 0 |
| 0x1B0A65 | 0x1B0A65 Fahrzeuggeschwindigkeit, Radsensor vorn/links, Plausibilität: Signal unplausibel | 0 |
| 0x1B0A66 | 0x1B0A66 Fahrzeuggeschwindigkeit, Radsensor hinten/rechts, Plausibilität: Signal unplausibel | 0 |
| 0x1B0A67 | 0x1B0A67 Fahrzeuggeschwindigkeit, Radsensor vorn/rechts, Plausibilität: Signal unplausibel | 0 |
| 0x1B2002 | 0x1B2002 EWS Manipulationsschutz: kein Startwert programmiert | 0 |
| 0x1B2008 | 0x1B2008 EWS Manipulationsschutz: erwartete Antwort unplausibel | 0 |
| 0x1B2101 | 0x1B2101 Schnittstelle EWS-DME: Hardwarefehler | 0 |
| 0x1B2102 | 0x1B2102 Schnittstelle EWS-DME: Framefehler | 0 |
| 0x1B2104 | 0x1B2104 Schnittstelle EWS-DME: Zeitüberschreitung | 0 |
| 0x1B2109 | 0x1B2109 Schnittstelle EWS-DME: Empfangsfehler CAS Schnittstelle | 0 |
| 0x1B2201 | 0x1B2201 DME, interner Fehler, EWS-Daten: keine verfügbare Speichermöglichkeit | 0 |
| 0x1B2202 | 0x1B2202 DME, interner Fehler, EWS-Daten: Fehlerfreischaltcodeablage | 0 |
| 0x1B2208 | 0x1B2208 DME, interner Fehler, EWS-Daten: Prüfsummenfehler | 0 |
| 0x1B2209 | 0x1B2209 DME, interner Fehler, EWS-Daten: Schreibfehler Secret Key | 0 |
| 0x1B2302 | 0x1B2302 Botschaft EWS-DME fehlerhaft: Framefehler | 0 |
| 0x1B2304 | 0x1B2304 Botschaft EWS-DME fehlerhaft: Zeitüberschreitung | 0 |
| 0x1B5101 | 0x1B5101 Klemme 15_3, Leitung vom CAS, elektrisch: Kurzschluss nach Plus | 0 |
| 0x1B5102 | 0x1B5102 Klemme 15_3, Leitung vom CAS, elektrisch: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 |
| 0x1B5202 | 0x1B5202 Klemme 15N_1, Versorgung geschaltet durch CAS, elektrisch: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 |
| 0x1B5302 | 0x1B5302 Klemme 15N_2, Versorgung geschaltet durch CAS, elektrisch: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 |
| 0x1B5402 | 0x1B5402 Klemme 15N_3, Versorgung geschaltet durch CAS, elektrisch: Kurzschluss nach Masse oder Leitungsunterbrechung | 0 |
| 0x1B6008 | 0x1B6008 Bremslichtschalter, Plausibilität: Signal unplausibel | 0 |
| 0x1B9004 | 0x1B9004 Motorabstellzeit: Zeitüberschreitung oder Ungültigkeitswert | 0 |
| 0x1B9008 | 0x1B9008 Motorabstellzeit: Signal unplausibel | 0 |
| 0x1B9508 | 0x1B9508 Motorabstellzeit, Plausibilität: Zeit zu kurz in Korrelation zu Motorkühlmittel-Abkühlung | 0 |
| 0x1B9608 | 0x1B9608 Motorabstellzeit, Plausibilität: Zeit zu lang in Korrelation zu Motorkühlmittel-Abkühlung | 0 |
| 0x1B9701 | 0x1B9701 Motorabstellzeit: zu schnell im Motorlauf | 0 |
| 0x1B9702 | 0x1B9702 Motorabstellzeit: zu langsam im Motorlauf | 0 |
| 0x1B9804 | 0x1B9804 Motorabstellzeit, Signal: fehlt | 0 |
| 0x1B9A01 | 0x1B9A01 Motorabstellzeit: zu schnell im Nachlauf | 0 |
| 0x1B9A02 | 0x1B9A02 Motorabstellzeit: zu langsam im Nachlauf | 0 |
| 0x1BC004 | 0x1BC004 Nullgangsensor, Adaption: nicht gelernt (MSA deaktiviert) | 0 |
| 0x1C0001 | 0x1C0001 Motoröldruckregelung, dynamisch: Druckschwankungen | 0 |
| 0x1C0101 | 0x1C0101 Motoröldruckregelung, statisch: Motoröldruck zu hoch, Notlauf | 0 |
| 0x1C0102 | 0x1C0102 Motoröldruckregelung, statisch: Motoröldruck zu niedrig, Notlauf | 0 |
| 0x1C0201 | 0x1C0201 Öldruckregelventil, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x1C0202 | 0x1C0202 Öldruckregelventil, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x1C0204 | 0x1C0204 Öldruckregelventil, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x1C0301 | 0x1C0301 Öldruckregelventil, mechanisch: hängt in voll bestromter Stellung (minimaler Öldruck) | 0 |
| 0x1C0302 | 0x1C0302 Öldruckregelventil, mechanisch: hängt in unbestromter Stellung (maximaler Öldruck) | 0 |
| 0x1C0401 | 0x1C0401 Motoröldrucksystem: Regelung instabil | 0 |
| 0x1C2001 | 0x1C2001 Ölpumpe, mechanisch: Öldruck zu hoch | 0 |
| 0x1C2002 | 0x1C2002 Ölpumpe, mechanisch: Öldruck zu niedrig | 0 |
| 0x1C3001 | 0x1C3001 Motoröldrucksensor, elektrisch: Kurzschluss nach Plus | 0 |
| 0x1C3002 | 0x1C3002 Motoröldrucksensor, elektrisch: Kurzschluss nach Masse | 0 |
| 0x1C3101 | 0x1C3101 Motoröldrucksensor, Plausibilität: Druck zu hoch vor Start | 0 |
| 0x1C3102 | 0x1C3102 Motoröldrucksensor, Plausibilität: Druck zu niedrig vor Start | 0 |
| 0x1C3108 | 0x1C3108 Motoröldrucksensor, Plausibilität: Signal hängt | 0 |
| 0x1C4002 | 0x1C4002 Motorölniveau: zu niedrig | 0 |
| 0x1C4110 | 0x1C4110 Ölzustandssensor, elektrisch: Fehlfunktion | 0 |
| 0x1C4111 | 0x1C4111 Ölzustandssensor, Plausibilität: Niveau unplausibel | 0 |
| 0x1C4112 | 0x1C4112 Ölzustandssensor, Plausibilität: Temperatur unplausibel | 0 |
| 0x1C4113 | 0x1C4113 Ölzustandssensor, Plausibilität: Niveau unplausibel | 0 |
| 0x1C4114 | 0x1C4114 Ölzustandssensor, Plausibilität: Permittivität unplausibel | 0 |
| 0x1C4115 | 0x1C4115 Ölzustandssensor, Plausibilität: Temperatur unplausibel | 0 |
| 0x1C4116 | 0x1C4116 Ölzustandssensor, elektrisch: Niveau Fehlfunktion | 0 |
| 0x1C4117 | 0x1C4117 Ölzustandssensor, elektrisch: Permittivität Fehlfunktion | 0 |
| 0x1C4118 | 0x1C4118 Ölzustandssensor, elektrisch: Temperatur Fehlfunktion | 0 |
| 0x1C4119 | 0x1C4119 Motoröltemperatursensor, elektrisch: Fehlfunktion | 0 |
| 0x1C4120 | 0x1C4120 Motoröltemperatursensor, Plausibilität: Temperatur unplausibel | 0 |
| 0x1C5A20 | 0x1C5A20 BSD-Botschaft vom Ölzustandssensor: fehlt | 0 |
| 0x1D2008 | 0x1D2008 Kennfeldthermostat, mechanisch: klemmt offen | 0 |
| 0x1D2401 | 0x1D2401 Kennfeldthermostat, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x1D2402 | 0x1D2402 Kennfeldthermostat, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x1D2404 | 0x1D2404 Kennfeldthermostat, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x1D3701 | 0x1D3701 Schaltzeitpunkt: Anpassung | 0 |
| 0x1D3901 | 0x1D3901 EGS, Signalüberwachung (Turbinendrehzahl): ungültiger Signalinhalt | 1 |
| 0x1D3A01 | 0x1D3A01 EGS, Signalüberwachung (Drehzahl Abtrieb): ungültiger Signalinhalt | 1 |
| 0x1D3B01 | 0x1D3B01 EGS, Signalüberwachung (Ganginformation): ungültiger Signalinhalt | 1 |
| 0x1D3C01 | 0x1D3C01 EGS, Signalüberwachung (Status Schaltvorgang): ungültiger Signalinhalt | 1 |
| 0x1E0001 | 0x1E0001 Leerlaufregelung: Drehzahl zu hoch | 0 |
| 0x1E0002 | 0x1E0002 Leerlaufregelung: Drehzahl zu niedrig | 0 |
| 0x1E0101 | 0x1E0101 Leerlaufregelung, Kaltstart: Drehzahl zu hoch | 0 |
| 0x1E0102 | 0x1E0102 Leerlaufregelung, Kaltstart: Drehzahl zu niedrig | 0 |
| 0x1E5201 | 0x1E5201 Drehzahlbegrenzung bei stehendem Fahrzeug: Leerlaufdrehzahl zu lange zu hoch | 0 |
| 0x1E5A20 | 0x1E5A20 Überwachung Motordrehmoment-Begrenzung: Maximal zulässiges Sollmoment wird dauerhaft überschritten | 0 |
| 0x1F0514 | 0x1F0514 Valvetronic-Relais, Versorgungsspannung: Kurzschluss nach Masse | 0 |
| 0x1F0515 | 0x1F0515 Valvetronic-Relais, Versorgungsspannung: Leitungsunterbrechung | 0 |
| 0x1F0516 | 0x1F0516 DME, interner Fehler, Überwachung elektrisches Fahrpedal: AD-Wandler Leerlauftestimpulsprüfung | 0 |
| 0x1F0517 | 0x1F0517 DME, interner Fehler, Überwachung elektrisches Fahrpedal: AD-Wandler Testspannungsprüfung | 0 |
| 0x1F0518 | 0x1F0518 DME, interner Fehler, Überwachung elektrisches Fahrpedal: Luftmengenabgleich | 0 |
| 0x1F0519 | 0x1F0519 DME, interner Fehler: Überwachung Signalplausibilisierung Fahrpedalmodul oder Pedalwertgeber | 0 |
| 0x1F0520 | 0x1F0520 DME, interner Fehler, Überwachung elektrisches Fahrpedal: Drehzahlgeber | 0 |
| 0x1F0521 | 0x1F0521 DME, interner Fehler: Überwachung Plausibilisierung der Gemischkorrekturfaktoren | 0 |
| 0x1F0522 | 0x1F0522 DME, interner Fehler: Überwachung Einspritzmengenbegrenzung Ebene 1 | 0 |
| 0x1F0523 | 0x1F0523 DME, interner Fehler: Überwachung Einspritzmengenbegrenzung Ebene 2 | 0 |
| 0x1F0524 | 0x1F0524 DME, interner Fehler: Überwachung des Lambda-Sollwertes | 0 |
| 0x1F0525 | 0x1F0525 DME, interner Fehler: Überwachung Plausibilisierung der relativen Kraftstoffmasse | 0 |
| 0x1F0526 | 0x1F0526 DME, interner Fehler: Überwachung Momentenvergleich | 0 |
| 0x1F0527 | 0x1F0527 DME, interner Fehler, Überwachung elektrisches Fahrpedal: Antriebstrangübersetzungsverhältnis unplausibel | 0 |
| 0x1F0528 | 0x1F0528 DME, interner Fehler: Überwachung Variantencodierung | 0 |
| 0x1F0529 | 0x1F0529 DME, interner Fehler, Überwachung elektrisches Fahrpedal: Zündwinkelüberwachung | 0 |
| 0x1F0530 | 0x1F0530 DME, interner Fehler: Abschaltpfad-Test durch Überwachungsmodul | 0 |
| 0x1F0531 | 0x1F0531 DME, interner Fehler: Überwachung Plausiblisierung Kraftstoffmasse | 0 |
| 0x1F0532 | 0x1F0532 DME, interner Fehler, Überwachung MSC-Kommunikation: Fehlfunktion an Baustein R2S2/1 | 0 |
| 0x1F0533 | 0x1F0533 DME, interner Fehler, Überwachung MSC-Kommunikation: Fehlfunktion an Baustein R2S2/2 | 0 |
| 0x1F0904 | 0x1F0904 DME, interner Fehler, Ansteuerung Valvetronic: Fehlfunktion | 0 |
| 0x1F1A40 | 0x1F1A40 DME, interner Fehler: Überwachung SPI-Kommunikation | 0 |
| 0x1F1A50 | 0x1F1A50 DME, interner Fehler: Löschen EEPROM fehlerhaft | 0 |
| 0x1F1A51 | 0x1F1A51 DME, interner Fehler: Lesen EEPROM fehlerhaft | 0 |
| 0x1F1A52 | 0x1F1A52 DME, interner Fehler: Schreiben EEPROM fehlerhaft | 0 |
| 0x1F1A60 | 0x1F1A60 DME, interner Fehler: Überwachungsmodulfehler | 0 |
| 0x1F1A70 | 0x1F1A70 DME, interner Fehler, Überwachung 5V-Versorgung: Überspannung erkannt | 0 |
| 0x1F1A71 | 0x1F1A71 DME, interner Fehler, Überwachung 5V-Versorgung: Unterspannung erkannt | 0 |
| 0x1F1A72 | 0x1F1A72 DME, interner Fehler, Überwachung 5V-Versorgung 2: Überspannung erkannt | 0 |
| 0x1F1A73 | 0x1F1A73 DME, interner Fehler, Überwachung 5V-Versorgung 2: Unterspannung erkannt | 0 |
| 0x1F1A80 | 0x1F1A80 DME, interner Fehler, Watchdog-Ausgang: Fehlfunktion | 0 |
| 0x1F1A81 | 0x1F1A81 DME, interner Fehler, Watchdog-Ausgang: fehlerhafte Frage-/Antwort-Kommunikation | 0 |
| 0x1F1A82 | 0x1F1A82 DME, interner Fehler, Watchdog-Ausgang: Überspannungserkennung | 0 |
| 0x1F1A90 | 0x1F1A90 DME, interner Fehler, Überwachung 5V Sensor-Versorgung: Spannung außerhalb gültigem Bereich | 0 |
| 0x1F1A91 | 0x1F1A91 DME, interner Fehler, Überwachung 5V Sensor-Versorgung 2: Spannung außerhalb gültigem Bereich | 0 |
| 0x1F1A92 | 0x1F1A92 DME, interner Fehler, Überwachung 5V Sensor-Versorgung 3: Spannung außerhalb gültigem Bereich | 0 |
| 0x1F1AA0 | 0x1F1AA0 DME, interner Fehler: Software-Reset | 0 |
| 0x1F1AA1 | 0x1F1AA1 DME, interner Fehler: Software-Reset | 0 |
| 0x1F1AA2 | 0x1F1AA2 DME, interner Fehler: Software-Reset | 0 |
| 0x1F1B40 | 0x1F1B40 Starter, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x1F1B41 | 0x1F1B41 Starter, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x1F1B42 | 0x1F1B42 Starter, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x1F1B50 | 0x1F1B50 Bordnetzspannung, DME-Hauptrelais: Spannung zu hoch | 0 |
| 0x1F2104 | 0x1F2104 Falscher Datensatz: CAN Timeout | 0 |
| 0x1F2108 | 0x1F2108 Falscher Datensatz: Variantenüberwachung | 0 |
| 0x1F2601 | 0x1F2601 Codierung: falsche Variante codiert | 0 |
| 0x1F2604 | 0x1F2604 Codierung: Fahrgestellnummer nicht kodiert | 0 |
| 0x1F2701 | 0x1F2701 Codierung: Fehler beim Schreiben der Variante | 0 |
| 0x1F2702 | 0x1F2702 Codierung: Variantenprüfung fehlerhaft | 0 |
| 0x1F2704 | 0x1F2704 Codierung: Unplausible Variante | 0 |
| 0x1F4A01 | 0x1F4A01 Relais Zündung und Injektoren, Ansteuerung: Kurzschluss nach Plus | 0 |
| 0x1F4A02 | 0x1F4A02 Relais Zündung und Injektoren, Ansteuerung: Kurzschluss nach Masse | 0 |
| 0x1F4A10 | 0x1F4A10 Relais Zündung und Injektoren, Ansteuerung: Leitungsunterbrechung | 0 |
| 0x1F5020 | 0x1F5020 DME, interner Fehler, Innentemperatursensor: Wert zu hoch | 0 |
| 0x1F5021 | 0x1F5021 DME, interner Fehler, Innentemperatursensor: Wert zu niedrig | 0 |
| 0x1F5101 | 0x1F5101 DME Temperatur: Übertemperatur | 0 |
| 0x200502 | 0x200502 DME, interner Fehler, Überwachung externe Momentenanforderung: Anforderung ICM unplausibel | 0 |
| 0x200503 | 0x200503 DME, interner Fehler, Überwachung externe Momentenanforderung: Anforderung ICM unplausibel | 0 |
| 0x200D04 | 0x200D04 DME, interner Fehler, Überwachung Sendesignale: Fahrpedal unplausibel | 0 |
| 0x200F11 | 0x200F11 DME, interner Fehler, Überwachung Sendesignale: Ist-Radmoment unplausibel | 0 |
| 0x200F12 | 0x200F12 DME, interner Fehler, Überwachung Sendesignale: koordiniertes Radmoment unplausibel | 0 |
| 0x200F13 | 0x200F13 DME, interner Fehler, Überwachung Sendesignale: Verlustmoment unplausibel | 0 |
| 0x200F14 | 0x200F14 DME, interner Fehler, Überwachung Sendesignale: Verstärkung Antriebsstrang unplausibel | 0 |
| 0x200F15 | 0x200F15 DME, interner Fehler, Überwachung Sendesignale: Status Schnittstelle Fahrerassistenzsystem unplausibel | 0 |
| 0x200F16 | 0x200F16 DME, interner Fehler, Überwachung Sendesignale: Statuswort Radmomentenschnittstelle unplausibel | 0 |
| 0x200F17 | 0x200F17 DME, interner Fehler, Überwachung Sendesignale: Schleppmoment unplausibel | 0 |
| 0x200F18 | 0x200F18 DME, interner Fehler, erweiterte Überwachung Sendesignale: Fahrpedal unplausibel | 0 |
| 0x200F19 | 0x200F19 DME, interner Fehler, erweiterte Überwachung Sendesignale: Ist-Radmoment unplausibel | 0 |
| 0x200F20 | 0x200F20 DME, interner Fehler, erweiterte Überwachung Sendesignale: koordiniertes Radmoment unplausibel | 0 |
| 0x200F21 | 0x200F21 DME, interner Fehler, erweiterte Überwachung Sendesignale: Verlustmoment unplausibel | 0 |
| 0x200F22 | 0x200F22 DME, interner Fehler, erweiterte Überwachung Sendesignale: Verstärkung Antriebsstrang unplausibel | 0 |
| 0x200F23 | 0x200F23 DME, interner Fehler, erweiterte Überwachung Sendesignale: Status Schnittstelle Fahrerassistenzsystem unplausibel | 0 |
| 0x200F24 | 0x200F24 DME, interner Fehler, erweiterte Überwachung Sendesignale: Qualifier Radmomentenschnittstelle unplausibel | 0 |
| 0x200F25 | 0x200F25 DME, interner Fehler, erweiterte Überwachung Sendesignale: Schleppmoment unplausibel | 0 |
| 0x200F26 | 0x200F26 DME, interner Fehler, erweiterte Überwachung Sendesignale: Status Motorlauf unplausibel | 0 |
| 0x200F27 | 0x200F27 DME, interner Fehler, Überwachung Sendesignale: Drehzahl Hinterachse unplausibel | 0 |
| 0x200F28 | 0x200F28 DME, interner Fehler, Überwachung Sendesignale: Fahrtrichtungswunsch unplausibel | 0 |
| 0x200F29 | 0x200F29 DME, interner Fehler, Überwachung Sendesignale: Motorstatus unplausibel | 0 |
| 0x200F2A | 0x200F2A DME, interner Fehler, Überwachung Sendesignale: Status Kraftschluss Antriebsstrang unplausibel | 0 |
| 0x200F2B | 0x200F2B DME, interner Fehler, erweiterte Überwachung Sendesignale: Drehzahl Hinterachse unplausibel | 0 |
| 0x200F2C | 0x200F2C DME, interner Fehler, erweiterte Überwachung Sendesignale: Fahrtrichtungswunsch unplausibel | 0 |
| 0x200F2D | 0x200F2D DME, interner Fehler, erweiterte Überwachung Sendesignale: Motorstatus unplausibel | 0 |
| 0x200F2E | 0x200F2E DME, interner Fehler, erweiterte Überwachung Sendesignale: Status Kraftschluss Antriebsstrang unplausibel | 0 |
| 0x201004 | 0x201004 CBS-Client: Ausgabe von Ersatzwert | 0 |
| 0x201008 | 0x201008 CBS-Client: Verfügbarkeitssprung | 0 |
| 0x201010 | 0x201010 CAN Hardware: defekt | 0 |
| 0x201020 | 0x201020 FlexRay Hardware: defekt | 0 |
| 0x201030 | 0x201030 Testfunktion Layer: Fehlergruppe 1 | 0 |
| 0x201040 | 0x201040 Testfunktion Layer: Fehlergruppe 2 | 0 |
| 0x201101 | 0x201101 DME, Manipulationsschutz: Programm oder Datenmanipulation erkannt | 0 |
| 0x20A701 | 0x20A701 Kühlmittelpumpe, Drehzahlabweichung: außerhalb der Toleranz | 0 |
| 0x20A801 | 0x20A801 Kühlmittelpumpe, Abschaltung: interne Temperatur zu hoch | 0 |
| 0x20A802 | 0x20A802 Kühlmittelpumpe, Abschaltung: Überspannung erkannt | 0 |
| 0x20A804 | 0x20A804 Kühlmittelpumpe, Abschaltung: Pumpe blockiert | 0 |
| 0x20A901 | 0x20A901 Kühlmittelpumpe, leistungsreduzierter Betrieb: Trockenlauf erkannt | 0 |
| 0x20A902 | 0x20A902 Kühlmittelpumpe, leistungsreduzierter Betrieb: Unterspannung erkannt | 0 |
| 0x20A904 | 0x20A904 Kühlmittelpumpe, leistungsreduzierter Betrieb: Temperaturgrenze 1 überschritten | 0 |
| 0x20A908 | 0x20A908 Kühlmittelpumpe, leistungsreduzierter Betrieb: Temperaturgrenze 2 überschritten | 0 |
| 0x20A909 | 0x20A909 BSD-Botschaft von der elektrischen Kühlmittelpumpe: fehlt | 0 |
| 0x20AA04 | 0x20AA04 Kühlmittelpumpe, Kommunikation: Fehlfunktion | 0 |
| 0x20AB08 | 0x20AB08 Kühlmittelpumpe, Notlauf-Eingang: keine Spannung | 0 |
| 0x20AC08 | 0x20AC08 Kühlmittelpumpe, Hardwareeingang: Status Notlauf-Eingang unplausibel | 0 |
| 0x20AD08 | 0x20AD08 Kühlmittelpumpe: Drehzahl unplausibel | 0 |
| 0x20BA20 | 0x20BA20 Kupplungsschalter, Signal: Signal fehlt | 0 |
| 0x210201 | 0x210201 Generator, elektrisch: Fehlfunktion | 0 |
| 0x210301 | 0x210301 Generator, Plausibilität, elektrisch: berechnet | 0 |
| 0x210401 | 0x210401 Generator, Temperatur: Übertemperatur | 1 |
| 0x210501 | 0x210501 Generator, Plausibilität, Temperatur: Übertemperatur berechnet | 1 |
| 0x210601 | 0x210601 Generator, mechanisch: Fehlfunktion | 0 |
| 0x210701 | 0x210701 Generator, Regler: Typ falsch | 0 |
| 0x210801 | 0x210801 Generator: Typ falsch | 0 |
| 0x210901 | 0x210901 Generator, Kommunikation: keine Kommunikation | 0 |
| 0x210C01 | 0x210C01 Generator, Kommunikation: Bus-Fehler | 0 |
| 0x211A21 | 0x211A21 BSD-Bus: Kommunikationsfehler | 0 |
| 0x211F01 | 0x211F01 Generator/Startergenerator: Codierung fehlt | 0 |
| 0x212001 | 0x212001 Startergenerator, Kommunikation: Bus-Fehler | 0 |
| 0x212101 | 0x212101 Startergenerator, Plausibilität, elektrisch: berechnet | 0 |
| 0x212201 | 0x212201 Startergenerator, elektrisch: Fehlfunktion | 0 |
| 0x212301 | 0x212301 Startergenerator: Übertemperatur | 1 |
| 0x212401 | 0x212401 Startergenerator, mechanisch: Fehlfunktion | 0 |
| 0x212501 | 0x212501 Startergenerator, MSA Hardwareleitung: Signal unplausibel | 0 |
| 0x212601 | 0x212601 Startergenerator: MSA dauerhaft deaktiviert | 1 |
| 0x212701 | 0x212701 Startergenerator: MSA zeitweise deaktiviert | 1 |
| 0x212801 | 0x212801 Startergenerator: Sensorfehler | 0 |
| 0x212A01 | 0x212A01 Startergenerator: Typ falsch | 0 |
| 0x213301 | 0x213301 Powermanagement, Überspannung: Überspannung erkannt | 1 |
| 0x213401 | 0x213401 Powermanagement, Unterspannung: Unterspannung erkannt | 1 |
| 0x213501 | 0x213501 Powermanagement, Batterieüberwachung: Tiefentladung | 1 |
| 0x213604 | 0x213604 Powermanagement, Ruhestromüberwachung: Ruhestromverletzung | 1 |
| 0x213701 | 0x213701 Powermanagement: Batterieloser Betrieb | 1 |
| 0x213801 | 0x213801 Batterie, Transport: Batterie auf Transport geschädigt | 1 |
| 0x213901 | 0x213901 Verbraucherreduzierung: aktiv | 1 |
| 0x213A01 | 0x213A01 Batterie, Transport, Überwachung: Batterie auf Transport entladen | 1 |
| 0x213A20 | 0x213A20 Bordnetzspannung: Spannung zu hoch | 0 |
| 0x213A21 | 0x213A21 Bordnetzspannung: Spannung zu niedrig | 0 |
| 0x213A22 | 0x213A22 Bordnetzspannung: Analog-Digital-Wandler defekt | 0 |
| 0x213B08 | 0x213B08 Powermanagement, Batteriezustandserkennung: Batteriedefekt | 0 |
| 0x213C08 | 0x213C08 Powermanagement, Batteriezustandserkennung: Tiefentladung | 0 |
| 0x213D01 | 0x213D01 Powermanagement, Bauteilerkennung: Batterieladeeinheit und Power Control Unit erkannt | 0 |
| 0x215001 | 0x215001 Intelligenter Batteriesensor, Signal: Bus-Fehler | 0 |
| 0x215101 | 0x215101 Intelligenter Batteriesensor, Funktion: Temperaturfehler | 0 |
| 0x215104 | 0x215104 Intelligenter Batteriesensor, Funktion: Spannungsfehler | 0 |
| 0x215108 | 0x215108 Intelligenter Batteriesensor, Funktion: Stromfehler | 0 |
| 0x215801 | 0x215801 Intelligenter Batteriesensor, Wake-up-Leitung: Kurzschluss nach Plus oder Masse | 0 |
| 0x215901 | 0x215901 Intelligenter Batteriesensor, Kompatibilität: Version nicht plausibel | 0 |
| 0x215A01 | 0x215A01 Intelligenter Batteriesensor, Wake-up-Leitung: Leitungsunterbrechung | 0 |
| 0x215B01 | 0x215B01 Intelligenter Batteriesensor, Kommunikation: keine Kommunikation | 0 |
| 0x215C01 | 0x215C01 Intelligenter Batteriesensor, Eigendiagnose: interner Fehler | 0 |
| 0x218001 | 0x218001 Batterieladeeinheit: Interner Fehler | 0 |
| 0x218101 | 0x218101 Batterieladeeinheit: Leitungsüberwachung fehlerhaft | 0 |
| 0x218201 | 0x218201 Batterieladeeinheit: Zusatzbatterie defekt | 0 |
| 0x218301 | 0x218301 Batterieladeeinheit: Fehler im Trennrelais oder Kabelbaum oder Zusatzbatterie tiefentladen | 0 |
| 0x219001 | 0x219001 Aktives Motorlager, elektrisch: Kurzschluss nach Plus | 0 |
| 0x219002 | 0x219002 Aktives Motorlager, elektrisch: Kurzschluss nach Masse | 0 |
| 0x219004 | 0x219004 Aktives Motorlager, elektrisch: Leitungsunterbrechung | 0 |
| 0x231501 | 0x231501 Aktive DTC-reporting: DTC-Puffer voll | 0 |
| 0x231502 | 0x231502 Aktive DTC-reporting: DTC-Senden fehlerhaft | 0 |
| 0x231802 | 0x231802 CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an A-CAN | 1 |
| 0x231902 | 0x231902 CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an A-CAN | 1 |
| 0x231F04 | 0x231F04 EGS über A- und FA-CAN: Kommunikationsfehler | 0 |
| 0x233004 | 0x233004 Dienst (0x5E0, OBD Sensor Diagnosestatus): fehlt | 1 |
| 0xCD840A | 0xCD840A FA-CAN Bus: Kommunikationsfehler | 0 |
| 0xCD8420 | 0xCD8420 FlexRay Bus: Kommunikationsfehler | 0 |
| 0xCD8486 | 0xCD8486 A-CAN Bus: Kommunikationsfehler | 0 |
| 0xCD8801 | 0xCD8801 FlexRay controller, Startupzeit: maximale Startupzeit überschritten | 0 |
| 0xCD8BFF | 0xCD8BFF Dummy Network DTC: network DTC | 0 |
| 0xCD8D10 | 0xCD8D10 LIN, Botschaft (Kühlerjalousie, 0x33): Kommunikationsfehler vom Kühlerjalousieantrieb | 0 |
| 0xCD8D15 | 0xCD8D15 LIN, Botschaft (Batterieladeeinheit, Zusatzbatterie): Elektrischer Fehler | 0 |
| 0xCD8D16 | 0xCD8D16 LIN, Botschaft (Batterieladeeinheit, H-Brücke): Kein Ladebetrieb möglich | 0 |
| 0xCD8D17 | 0xCD8D17 LIN, Botschaft (Batterieladeeinheit, Status Energieerzeugung Bordnetz 2, 0x5): fehlt | 0 |
| 0xCD8D18 | 0xCD8D18 LIN, Botschaft (Batterieladeeinheit, Trennrelais oder Leitung): Elektrischer Fehler | 0 |
| 0xCD8D19 | 0xCD8D19 LIN, Botschaft (Batterieladeeinheit, zweite Spannungsebene): Fehlfunktion | 0 |
| 0xCD8E10 | 0xCD8E10 LIN Bus, Kommunikation: Signal fehlt | 1 |
| 0xCD8F01 | 0xCD8F01 Intelligenter Batteriesensor, LIN Kommunikation: Zeitüberschreitung | 0 |
| 0xCD9002 | 0xCD9002 Kühlmittelpumpe, Kommunikation: Ungültige Botschaft | 1 |
| 0xCD9011 | 0xCD9011 Kühlmittelpumpe, Kommunikation: ungültige Botschaft | 1 |
| 0xCD9201 | 0xCD9201 Kühlerjalousie, LIN Kommunikation: Zeitüberschreitung | 0 |
| 0xCD9203 | 0xCD9203 Kühlerjalousie, LIN Kommunikation: Signal fehlerhaft | 0 |
| 0xCD9402 | 0xCD9402 FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): Aliveprüfung | 1 |
| 0xCD9404 | 0xCD9404 FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): fehlt | 1 |
| 0xCD9408 | 0xCD9408 FlexRay, Botschaft (Anforderung Drehmoment Kurbelwelle Fahrdynamik, 58.1.4): Prüfsumme falsch | 1 |
| 0xCD9432 | 0xCD9432 CAN, Botschaft (Status Getriebesteuergerät, 0x39A) bei Unterspannung: Kommunikationsfehler an A-CAN | 1 |
| 0xCD9435 | 0xCD9435 CAN, Botschaft (Daten Getriebestrang, 0x1AF) bei Unterspannung: Kommunikationsfehler an A-CAN | 1 |
| 0xCD9437 | 0xCD9437 FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung, 43.1.4) bei Unterspannung: Kommunikationsfehler | 1 |
| 0xCD9502 | 0xCD9502 FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung, 43.1.4): Aliveprüfung | 1 |
| 0xCD9504 | 0xCD9504 FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung, 43.1.4): fehlt | 1 |
| 0xCD9508 | 0xCD9508 FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe Stabilisierung, 43.1.4): Prüfsumme falsch | 1 |
| 0xCD9602 | 0xCD9602 FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): Aliveprüfung | 1 |
| 0xCD9604 | 0xCD9604 FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): fehlt | 1 |
| 0xCD9608 | 0xCD9608 FlexRay, Botschaft (Anforderung Radmoment Antriebsstrang Summe Rekuperation, 47.0.2): Prüfsumme falsch | 1 |
| 0xCD9702 | 0xCD9702 FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): Aliveprüfung | 1 |
| 0xCD9704 | 0xCD9704 FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): fehlt | 1 |
| 0xCD9708 | 0xCD9708 FlexRay, Botschaft (Konfiguration Schalter Fahrdynamik, 272.4.8): Prüfsumme falsch | 1 |
| 0xCD9902 | 0xCD9902 FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): Aliveprüfung | 1 |
| 0xCD9904 | 0xCD9904 FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): fehlt | 1 |
| 0xCD9908 | 0xCD9908 FlexRay, Botschaft (Geschwindigkeit Fahrzeug, 55.3.4): Prüfsumme falsch | 1 |
| 0xCD9932 | 0xCD9932 Flexray, Botschaft (Giergeschwindigkeit Fahrzeug, 38.0.2): Aliveprüfung | 1 |
| 0xCD9933 | 0xCD9933 Flexray, Botschaft (Giergeschwindigkeit Fahrzeug, 38.0.2): fehlt | 1 |
| 0xCD9934 | 0xCD9934 Flexray, Botschaft (Giergeschwindigkeit Fahrzeug, 38.0.2): Prüfsumme falsch | 1 |
| 0xCD9935 | 0xCD9935 Flexray, Botschaft (Daten Fahrdynamiksensor Erweitert, 38.0.2): fehlt | 1 |
| 0xCD9A02 | 0xCD9A02 FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): Aliveprüfung | 1 |
| 0xCD9A04 | 0xCD9A04 FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): fehlt | 1 |
| 0xCD9A08 | 0xCD9A08 FlexRay, Botschaft (Ist Bremsmoment Summe, 43.3.4): Prüfsumme falsch | 1 |
| 0xCD9B02 | 0xCD9B02 FlexRay, Botschaft (Ist Drehzahl Rad, 46.0.1): Aliveprüfung | 1 |
| 0xCD9B04 | 0xCD9B04 FlexRay, Botschaft (Ist Drehzahl Rad, 46.0.1): fehlt | 1 |
| 0xCD9B08 | 0xCD9B08 FlexRay, Botschaft (Ist Drehzahl Rad, 46.0.1): Prüfsumme falsch | 1 |
| 0xCD9D02 | 0xCD9D02 FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): Aliveprüfung | 1 |
| 0xCD9D04 | 0xCD9D04 FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): fehlt | 1 |
| 0xCD9D08 | 0xCD9D08 FlexRay, Botschaft (Längsbeschleunigung Schwerpunkt, 55.0.2): Prüfsumme falsch | 1 |
| 0xCD9E02 | 0xCD9E02 FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): Aliveprüfung | 1 |
| 0xCD9E04 | 0xCD9E04 FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): fehlt | 1 |
| 0xCD9E08 | 0xCD9E08 FlexRay, Botschaft (Querbeschleunigung Schwerpunkt, 55.0.2): Prüfsumme falsch | 1 |
| 0xCD9F02 | 0xCD9F02 FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): Aliveprüfung | 1 |
| 0xCD9F04 | 0xCD9F04 FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): fehlt | 1 |
| 0xCD9F08 | 0xCD9F08 FlexRay, Botschaft (Status Stabilisierung DSC, 47.1.2): Prüfsumme falsch | 1 |
| 0xCDA002 | 0xCDA002 FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): Aliveprüfung | 1 |
| 0xCDA004 | 0xCDA004 FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): fehlt | 1 |
| 0xCDA008 | 0xCDA008 FlexRay, Botschaft (Anforderung Radmoment Antriebstrang Summe FAS, 33.1.4): Prüfsumme falsch | 1 |
| 0xCDA102 | 0xCDA102 FlexRay, Botschaft (Neigung Fahrbahn, 56.1.2): Aliveprüfung | 1 |
| 0xCDA104 | 0xCDA104 FlexRay, Botschaft (Neigung Fahrbahn, 56.1.2): fehlt | 1 |
| 0xCDA108 | 0xCDA108 FlexRay, Botschaft (Neigung Fahrbahn, 56.1.2): Prüfsumme falsch | 1 |
| 0xCDA204 | 0xCDA204 FlexRay, Botschaft (Anforderung Leistung Elektrisch EPS, 234.0.2): fehlt | 1 |
| 0xCDA302 | 0xCDA302 FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): Aliveprüfung | 1 |
| 0xCDA304 | 0xCDA304 FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): fehlt | 1 |
| 0xCDA308 | 0xCDA308 FlexRay, Botschaft (Status Fahrzeugstillstand, 263.1.4): Prüfsumme falsch | 1 |
| 0xCDA402 | 0xCDA402 FlexRay, Botschaft (Ist Lenkwinkel Vorderachse, 57.1.2): Aliveprüfung | 1 |
| 0xCDA404 | 0xCDA404 FlexRay, Botschaft (Ist Lenkwinkel Vorderachse, 57.1.2): fehlt | 1 |
| 0xCDA408 | 0xCDA408 FlexRay, Botschaft (Ist Lenkwinkel Vorderachse, 57.1.2): Prüfsumme falsch | 1 |
| 0xCDA410 | 0xCDA410 FlexRay, Botschaft (Anzeige LDM 1, 135.0.2): fehlt | 1 |
| 0xCDA421 | 0xCDA421 FlexRay, Botschaft (Status Türsensoren Abgesichert, 256.3.4): Aliveprüfung | 0 |
| 0xCDA422 | 0xCDA422 FlexRay, Botschaft (Status Türsensoren Abgesichert, 256.3.4): fehlt | 0 |
| 0xCDA423 | 0xCDA423 FlexRay, Botschaft (Status Türsensoren Abgesichert, 256.3.4): Prüfsumme falsch | 0 |
| 0xCDA425 | 0xCDA425 FlexRay, Botschaft (Status Parkassistent, 231.1.2): fehlt | 1 |
| 0xCDA426 | 0xCDA426 FlexRay, Botschaft (Status Verteilung Längsmoment Vorderachse Hinterachse, 19.3.4): fehlt | 1 |
| 0xCDA430 | 0xCDA430 FlexRay, Botschaft (Betriebsart Drehzahl Drehmoment Hybrid, 74.0.2): Aliveprüfung | 1 |
| 0xCDA431 | 0xCDA431 FlexRay, Botschaft (Betriebsart Drehzahl Drehmoment Hybrid, 74.0.2): Prüfsumme falsch | 1 |
| 0xCDA432 | 0xCDA432 FlexRay, Botschaft (Betriebsart Drehzahl Drehmoment Hybrid, 74.0.2): fehlt | 1 |
| 0xCDA435 | 0xCDA435 FlexRay, Botschaft (Masse/Gewicht Fahrzeug, 108.1.2): fehlt | 1 |
| 0xCDA440 | 0xCDA440 FlexRay, Botschaft (Steuerung Koordination Drehmoment Hybrid, 73.0.2): Aliveprüfung | 1 |
| 0xCDA441 | 0xCDA441 FlexRay, Botschaft (Steuerung Koordination Drehmoment Hybrid, 73.0.2): Prüfsumme falsch | 1 |
| 0xCDA442 | 0xCDA442 FlexRay, Botschaft (Steuerung Koordination Drehmoment Hybrid, 73.0.2): fehlt | 1 |
| 0xCDA512 | 0xCDA512 FA-CAN, Botschaft (Status Gurt Kontakt Sitzbelegung, 0x297): Aliveprüfung | 1 |
| 0xCDA514 | 0xCDA514 FA-CAN, Botschaft (Status Gurt Kontakt Sitzbelegung, 0x297): fehlt | 1 |
| 0xCDA518 | 0xCDA518 FA-CAN, Botschaft (Status Gurt Kontakt Sitzbelegung, 0x297): Prüfsumme falsch | 1 |
| 0xCDA602 | 0xCDA602 FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Aliveprüfung | 1 |
| 0xCDA608 | 0xCDA608 FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Prüfsumme falsch | 1 |
| 0xCDA702 | 0xCDA702 FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): Aliveprüfung | 1 |
| 0xCDA704 | 0xCDA704 FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): fehlt | 1 |
| 0xCDA708 | 0xCDA708 FA-CAN, Botschaft (Status Fahrzeugstillstand Parkbremse, 0x2DC): Prüfsumme falsch | 1 |
| 0xCDA804 | 0xCDA804 FA-CAN, Botschaft (Relativzeit, 0x328): fehlt | 1 |
| 0xCDA904 | 0xCDA904 FA-CAN, Botschaft (Status Anhänger, 0x2E4): fehlt | 1 |
| 0xCDAB04 | 0xCDAB04 FA-CAN, Botschaft (Status Gang Rückwärts, 0x3B0): fehlt | 1 |
| 0xCDAC04 | 0xCDAC04 FA-CAN, Botschaft (Status Getriebesteuergerät, 0x39A): fehlt | 1 |
| 0xCDAD04 | 0xCDAD04 FA-CAN, Botschaft (Steuerung Crashabschaltung EKP, 0x135): fehlt | 1 |
| 0xCDAE04 | 0xCDAE04 FA-CAN, Botschaft (Uhrzeit/Datum, 0x2F8): fehlt | 1 |
| 0xCDAF04 | 0xCDAF04 FA-CAN, Botschaft (ZV und Klappenzustand, 0x2FC): fehlt | 1 |
| 0xCDB002 | 0xCDB002 FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Aliveprüfung | 1 |
| 0xCDB008 | 0xCDB008 FA-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Prüfsumme falsch | 1 |
| 0xCDB102 | 0xCDB102 FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle EGS, 0xB0): Aliveprüfung | 1 |
| 0xCDB108 | 0xCDB108 FA-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle EGS, 0xB0): Prüfsumme falsch | 1 |
| 0xCDB204 | 0xCDB204 FA-CAN, Botschaft (Außentemperatur, 0x2CA): fehlt | 1 |
| 0xCDB304 | 0xCDB304 FA-CAN, Botschaft (Daten Anzeige Getriebestrang, 0x3FD): fehlt | 1 |
| 0xCDB404 | 0xCDB404 FA-CAN, Botschaft (Fahrzeugzustand, 0x3A0): fehlt | 1 |
| 0xCDB504 | 0xCDB504 FA-CAN, Botschaft (Kilometerstand/Reichweite, 0x330): fehlt | 1 |
| 0xCDB602 | 0xCDB602 FA-CAN, Botschaft (Klemmen, 0x12F): Aliveprüfung | 1 |
| 0xCDB604 | 0xCDB604 FA-CAN, Botschaft (Klemmen, 0x12F): fehlt | 1 |
| 0xCDB608 | 0xCDB608 FA-CAN, Botschaft (Klemmen, 0x12F): Prüfsumme falsch | 1 |
| 0xCDB804 | 0xCDB804 FA-CAN, Botschaft (Anforderung Klimaanlage, 0x2F9): fehlt | 1 |
| 0xCDB904 | 0xCDB904 FA-CAN, Botschaft (Diagnose OBD Getriebe, 0x396): fehlt | 1 |
| 0xCDBA04 | 0xCDBA04 FA-CAN, Botschaft (Schlafbereitschaft Global FZM, 0x3A5): fehlt | 1 |
| 0xCDBA10 | 0xCDBA10 FA-CAN, Botschaft (Drehmoment Getriebe Hybrid, 0x8D): Aliveprüfung | 1 |
| 0xCDBA11 | 0xCDBA11 FA-CAN, Botschaft (Drehmoment Getriebe Hybrid, 0x8D): Prüfsumme falsch | 1 |
| 0xCDBA12 | 0xCDBA12 FA-CAN, Botschaft (Drehmoment Getriebe Hybrid, 0x8D): fehlt | 1 |
| 0xCDBA13 | 0xCDBA13 FA-CAN, Botschaft (Soll Daten Getriebe E-Motor 1, 0x91): Aliveprüfung | 1 |
| 0xCDBA14 | 0xCDBA14 FA-CAN, Botschaft (Soll Daten Getriebe E-Motor 1, 0x91): Prüfsumme falsch | 1 |
| 0xCDBA15 | 0xCDBA15 FA-CAN, Botschaft (Soll Daten Getriebe E-Motor 1, 0x91): fehlt | 1 |
| 0xCDBA17 | 0xCDBA17 FA-CAN, Botschaft (Freigabe Kühlung Hochvoltspeicher, 0x37B): fehlt | 1 |
| 0xCDBA20 | 0xCDBA20 FA-CAN, Botschaft (Ist Daten E-Motor 1, 0x90): Aliveprüfung | 1 |
| 0xCDBA21 | 0xCDBA21 FA-CAN, Botschaft (Ist Daten E-Motor 1, 0x90): Prüfsumme falsch | 1 |
| 0xCDBA22 | 0xCDBA22 FA-CAN, Botschaft (Ist Daten E-Motor 1, 0x90): fehlt | 1 |
| 0xCDBA25 | 0xCDBA25 FA-CAN, Botschaft (Diagnose OBD Motorsteuerung Elektrisch, 0x3E8): fehlt | 1 |
| 0xCDBA30 | 0xCDBA30 FA-CAN, Botschaft (Ist Daten E-Motor 1 Langzeit, 0x25B): Aliveprüfung | 1 |
| 0xCDBA31 | 0xCDBA31 FA-CAN, Botschaft (Ist Daten E-Motor 1 Langzeit, 0x25B): Prüfsumme falsch | 1 |
| 0xCDBA32 | 0xCDBA32 FA-CAN, Botschaft (Ist Daten E-Motor 1 Langzeit, 0x25B): fehlt | 1 |
| 0xCDBB02 | 0xCDBB02 A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Aliveprüfung | 1 |
| 0xCDBB04 | 0xCDBB04 A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): fehlt | 1 |
| 0xCDBB08 | 0xCDBB08 A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle Getriebe 2, 0xA0): Prüfsumme falsch | 1 |
| 0xCDBB10 | 0xCDBB10 A-CAN, Botschaft (Status Getriebe Hybrid, 0x409): Aliveprüfung | 1 |
| 0xCDBB11 | 0xCDBB11 A-CAN, Botschaft (Status Getriebe Hybrid, 0x409): Prüfsumme falsch | 1 |
| 0xCDBB12 | 0xCDBB12 A-CAN, Botschaft (Status Getriebe Hybrid, 0x409): fehlt | 1 |
| 0xCDBB20 | 0xCDBB20 A-CAN, Botschaft (Status Leckdiagnose Drucktank, 0x2E7): Aliveprüfung | 1 |
| 0xCDBB21 | 0xCDBB21 A-CAN, Botschaft (Status Leckdiagnose Drucktank, 0x2E7): Prüfsumme falsch | 1 |
| 0xCDBB22 | 0xCDBB22 A-CAN, Botschaft (Status Leckdiagnose Drucktank, 0x2E7): fehlt | 1 |
| 0xCDBC04 | 0xCDBC04 A-CAN, Botschaft (Anforderung Leistung Elektrisch PCU, 0x33F): fehlt | 1 |
| 0xCDBC10 | 0xCDBC10 A-CAN, Botschaft (Daten Antrieb Elektrisch, 0x32F): fehlt | 1 |
| 0xCDBC20 | 0xCDBC20 A-CAN, Botschaft (Status Antrieb Hybrid, 0x3A4): Aliveprüfung | 1 |
| 0xCDBC21 | 0xCDBC21 A-CAN, Botschaft (Status Antrieb Hybrid, 0x3A4): Prüfsumme falsch | 1 |
| 0xCDBC22 | 0xCDBC22 A-CAN, Botschaft (Status Antrieb Hybrid, 0x3A4): fehlt | 1 |
| 0xCDBC23 | 0xCDBC23 A-CAN, Botschaft (Diagnose OBD Motorsteuerung Elektrisch, 0x3E8): fehlt | 1 |
| 0xCDBD04 | 0xCDBD04 A-CAN, Botschaft (Status Energieerzeugung BN2, 0x2AF): fehlt | 1 |
| 0xCDBE02 | 0xCDBE02 A-CAN, Botschaft (Anzeige Drehzahl Motor Dynamisierung, 0xF8): Aliveprüfung | 1 |
| 0xCDBE04 | 0xCDBE04 A-CAN, Botschaft (Anzeige Drehzahl Motor Dynamisierung, 0xF8): fehlt | 1 |
| 0xCDBE20 | 0xCDBE20 A-CAN, Botschaft (Möglichkeit Motorstart Motorstop. 0x3EC): Aliveprüfung | 1 |
| 0xCDBE21 | 0xCDBE21 A-CAN, Botschaft (Möglichkeit Motorstart Motorstop. 0x3EC): Prüfsumme falsch | 1 |
| 0xCDBE22 | 0xCDBE22 A-CAN, Botschaft (Möglichkeit Motorstart Motorstop. 0x3EC): fehlt | 1 |
| 0xCDBF04 | 0xCDBF04 A-CAN, Botschaft (Status Getriebesteuergerät, 0x39A): fehlt | 1 |
| 0xCDBF20 | 0xCDBF20 A-CAN, Botschaft (Daten Verbrennungsmotor E-Motor 1, 0x407): Aliveprüfung | 1 |
| 0xCDBF21 | 0xCDBF21 A-CAN, Botschaft (Daten Verbrennungsmotor E-Motor 1, 0x407): Prüfsumme falsch | 1 |
| 0xCDBF22 | 0xCDBF22 A-CAN, Botschaft (Daten Verbrennungsmotor E-Motor 1, 0x407): fehlt | 1 |
| 0xCDC004 | 0xCDC004 A-CAN, Botschaft (Diagnose OBD Getriebe, 0x396): fehlt | 1 |
| 0xCDC102 | 0xCDC102 A-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Aliveprüfung | 1 |
| 0xCDC104 | 0xCDC104 A-CAN, Botschaft (Daten Getriebestrang, 0x1AF): fehlt | 1 |
| 0xCDC108 | 0xCDC108 A-CAN, Botschaft (Daten Getriebestrang, 0x1AF): Prüfsumme falsch | 1 |
| 0xCDC202 | 0xCDC202 A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle EGS, 0xB0): Aliveprüfung | 1 |
| 0xCDC204 | 0xCDC204 A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle EGS, 0xB0): fehlt | 1 |
| 0xCDC208 | 0xCDC208 A-CAN, Botschaft (Anforderung Drehmoment Kurbelwelle EGS, 0xB0): Prüfsumme falsch | 1 |
| 0xCDC304 | 0xCDC304 A-CAN, Botschaft (Status Elektrische Kraftstoffpumpe, 0x335): fehlt | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

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
| F_HLZ_VIEW | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 525 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4201 | Umgebungsdruck | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x4205 | Druck vor Drosselklappe | hPa | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| 0x4300 | Motor-Temperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x4306 | Quittung  Solldrehzahl von BSS-Wasserpumpe | 1/min | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4307 | empf. Status von BSS-Wasserpumpe | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4402 | Oeltemperatur nach Filter | Grad C | - | unsigned integer | - | 0,75 | 1 | -48,0 |
| 0x4403 | Kraftstoffverbrauch seit letztem Ölwechsel | - | - | unsigned long | - | 1,220703125E-4 | 1 | 0,0 |
| 0x4404 | Ölkilometer | km | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| 0x4405 | Sensorrohwert Ölniveau | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4406 | Sensorrohwert Permittivität | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4407 | Sensorrohwert Öltemperatur | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4408 | Öltemperatur ungefiltert | Grad C | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4409 | Ölniveau ungefiltert in [mm] | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x440A | Permitivität für den Tester | - | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| 0x440B | CodingDataSet-ÖL-Länderfaktor1- EEPROM | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x440C | CodingDataSet-ÖL-Länderfaktor2- EEPROM | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x440D | Länderfaktor 1 | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x440E | Länderfaktor 2 | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x440F | Kurzzeit-Ölniveau-Mittelwert für den DIS-Tester | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x4411 | Restweg aus Kraftstoffverbrauch abgeleitet | - | - | signed integer | - | 10,0 | 1 | 0,0 |
| 0x4412 | Öllaufzeit | month | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4418 | Status Ölzustandssensor | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4505 | Sollwinkel vom BMW Layer (Einlass-VANOS) | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x4506 | Einlassnockenwellenposition | Grad KW | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4507 | Auslassnockenwellenposition | Grad KW | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x450C | Kurbelwellenadaption Einlass erfolgt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x450D | Kurbelwellenadaption Auslass erfolgt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x450E | Kurbelwellennullpunktverschiebung in Grad für Winkelversatzdiagnose | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x4510 | VVT-Lageregler, bleibende Abweichung erkannt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4511 | VVT-Lageregelung, Schwingung erkannt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4512 | VVT überlastet | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4513 | VVT-Überlastung, klemmender Steller | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4514 | VVT-Adaption möglich | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4515 | Anforderung, VVT-Anschlaglernen | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4516 | Status VVT-Anschlaglernen | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4517 | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 0 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x4518 | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 1 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x4519 | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 2 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x451A | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 3 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x451B | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 4 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x451C | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 5 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x451D | Gesamtzeit VVT-Performancetest | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x451E | Stromsumme VVT-Performancetest | A | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4600 | Drosselklappenwinkel bezogen auf unteren Anschlag | %DK | - | signed integer | - | 0,0244140625 | 1 | 0,0 |
| 0x4601 | Sollwert Drosselklappenwinkel, bezogen auf (unteren) Anschlag | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4604 | Generatorstrom | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4605 | Chipversion Generator 2 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4607 | Kennung Generator Hersteller | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4608 | Kennung Generatortyp | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x460A | momentane Batteriespannung | V | - | unsigned integer | - | 0,014999999664723873 | 1 | 0,0 |
| 0x460C | Batteriespannung; vom AD-Wandler erfaßter Wert  | V | - | unsigned integer | - | 0,02355000004172325 | 1 | 0,0 |
| 0x460D | Korrekturwert Abschaltung | % | - | unsigned integer | - | 0,004000000189989805 | 1 | -100,0 |
| 0x460E | Abstand zur Startfähigkeit | % | - | unsigned integer | - | 0,004000000189989805 | 1 | -100,0 |
| 0x460F | DF-Monitor für Batterie-Ladezustand in % | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4612 | Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x4613 | vom Generator empfangene Generatorsollspannung (Kopie gesendeter Wert) | V | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| 0x4615 | Kopie begrenzter Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x4616 | vom Generator empfangene Load response Zeit (Kopie gesendeter Wert) | s | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4617 | gefiltertes Generatormoment absolut | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4618 | Drehzahlschwelle für LR-Funktion Generator 1 aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4619 | Bedingung BSD Protokollinhalt für BSD2 Regler | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x461A | Nominalspannung Regler Generator 1 | V | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| 0x4680 | Leerlaufdrehzahl gelernt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4681 | Bereitschaft Getriebe Neutralposition anlernen | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4700 | Bedingung Sonde betriebsbereit vor Kat | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4701 | Bedingung Sonde betriebsbereit vor Kat, Bank 2 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4702 | Offset korrigierte Sondenspannung vor Kat einer Breitbandlambdasonde | V | - | unsigned integer | - | 4,8828125E-4 | 1 | 0,0 |
| 0x4703 | Offset korrigierte Sondenspannung vor Kat einer Breitbandlambdasonde Bank 2 | V | - | unsigned integer | - | 4,8828125E-4 | 1 | 0,0 |
| 0x4704 | Lambdasoll Begrenzung (word) | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x4705 | Lambdasoll Begrenzung (word) Bank2 | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x4800 | Bedingung Kupplungspedal betätigt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4801 | Schalter Kupplung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4802 | Bedingung umschalten auf KFPEDS | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4803 | Bedingung für Kompressoreinschalten | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4805 | Schalter Klemme 50 von CAN | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4807 | Motordrehzahl | 1/min | - | unsigned integer | - | 0,25 | 1 | 0,0 |
| 0x4808 | Leerlaufsolldrehzahl | 1/min | - | unsigned integer | - | 0,25 | 1 | 0,0 |
| 0x4809 | Bedingung Leerlaufregelung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x480B | normierter Fahrpedalwinkel | %PED | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| 0x4880 | Max. Quotient Zündwinkelwirkungsgrad-Fehlerintegral im Leerlauf bez. auf Schwellwert | % | - | unsigned char | - | 0,78125 | 1 | 0,0 |
| 0x4881 | Max. Quotient Zündwinkelwirkungsgrad-Fehlerintegral im Teillast bez. auf Schwellwert | % | - | unsigned char | - | 0,78125 | 1 | 0,0 |
| 0x4A02 | ATL-Leckagediagnose läuft | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A14 | Spannung Lambdasonde (4.88mV/LSB) hinter Katalysator 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 |
| 0x4A17 | Spannung Pumpenstrom Tankdiagnose | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x4A1B | Elektrische Kraftstoffpumpe | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A1D | Spannung Bremsenunterdruck | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x4A21 | Kühlmitteltemperatur (Sensorwert) nach Tiefpassfilterung | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x4A2B | physikalischer Temperaturwert, der sich bei Wandlung der tiefpassgefilterten Sensorspannung wtfa1f_w | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x4A2D | Saugrohr-Absolutdruck gemessen | hPa | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| 0x4A30 | Laufunruhe Zylinder 1 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x4A31 | Laufunruhe Zylinder 2 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x4A32 | Laufunruhe Zylinder 3 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x4A33 | Laufunruhe Zylinder 4 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x4A34 | Laufunruhe Zylinder 5 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x4A35 | Laufunruhe Zylinder 6 | (Umdr./sec)^2 | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| 0x4A36 | Bedingung für erkannte Klopfer | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A37 | normierter Referenzpegel Klopfregelung Zylinder 1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x4A38 | normierter Referenzpegel Klopfregelung Zylinder 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x4A39 | normierter Referenzpegel Klopfregelung Zylinder 3 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x4A3A | normierter Referenzpegel Klopfregelung Zylinder 4 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x4A3B | normierter Referenzpegel Klopfregelung Zylinder 5 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x4A3C | normierter Referenzpegel Klopfregelung Zylinder 6 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x4A49 | Ausgegebener Zündwinkel | Grad KW | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4A50 | Lambda-Istwert | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x4A51 | Lambda-Istwert Bank2 | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x4A52 | Bedingung Sonde betriebsbereit hinter Kat | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A53 | Bedingung Sonde betriebsbereit hinter Kat Bank2 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A54 | Bedingung Sonde hinter Kat ausreichend beheizt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A55 | Bedingung Sonde 2 hinter Kat ausreichend beheizt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A56 | Bedingung: Heizerstatus A liegt vor, Sonde ist ausreichend aufgeheizt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A57 | Bedingung: Heizerstatus A liegt vor, Sonde ist ausreichend aufgeheizt, Bank2 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A60 | Bedingung Bremslichtschalter betätigt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A61 | Bedingung Bremstestschalter betätigt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A65 | Bedingung Abgasklappe mit Resonator | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A66 | Bedingung DMTL-Pumpenmotor an | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A67 | Bedingung DMTL-Magnetventil an | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A68 | Bedingung Heizung DM-TL Portansteuerung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A69 | MIL-Ansteuerung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A6A | Lampe FGR ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A6B | Bedingung für Ansteuerung EGAS-Fehlerlampe | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A6C | Korrekturfaktor für die Kraftstoffmenge | % | - | signed char | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x4A74 | Tastverhältnis Kennfeldthermostat | - | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4A77 | ausgegebenes Tastverhältnis für Tankentlüftungsventil (16 Bit) | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4A7A | Tastverhältnis Einlaßnockenwellenregelung Ansteuerung Endstufe(word) | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4A7B | Tastverhältnis Auslaßnockenwellenregelung Ansteuerung Endstufe(word) | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4A85 | multiplikative Gemischkorrektur der Gemischadaption (Word) | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x4A91 | Amplitudenverhältnis laafh/laafv gefiltert | - | - | unsigned char | - | 0,00390625 | 1 | 0,0 |
| 0x4A92 | Amplitudenverhältnis laafh/laafv gefiltert Bank2 | - | - | unsigned char | - | 0,00390625 | 1 | 0,0 |
| 0x4A93 | Fehlerzähler für Lernen Nullgang | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4A94 | gespeicherter Nockenwellensollwinkel Auslaß | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x4A95 | Adaptionswert Nockenwelle Auslass Bank 1 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x4A96 | Adaptionswert Nockenwelle Einlass Bank 1 | deg CrS | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| 0x4A97 | Bedi. Vanos Einlass im Anschlag | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4A99 | Status der fuel-off Adaption im aktuellen Betriebsbereich | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4A9D | multiplikative Gemischkorrektur der Gemischadaption | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x4AA1 | Zyklusflag: Tankentlüftungsventil Endstufe | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4AA2 | Funktionsstatus-Zähler DM-TL für Testerausgabe aus letztem Fahrzyklus | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4AA4 | Funktionsstatus LLRNS bei Anforderung Systemcheck | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4AAA | Tastverhältnis PWM Ansteuerung Öldruck | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4AAB | Tastverhältnis an Endstufe des Ladedruckstellers | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4AAC | Tastverhältnis an Endstufe des Ladedruckstellers, Bank 2 | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4AB0 | Ladedruck- Sollwert | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x4AB1 | Fahrzeuggeschwindigkeit | km/h | - | unsigned integer | - | 0,0078125 | 1 | 0,0 |
| 0x4AB3 | Zähler für gefahrene Kilometer mit MIL EIN | km | - | unsigned long | - | 0,009999999776482582 | 1 | 0,0 |
| 0x4AB4 | sekundengenauer Betribsstundenzähler als 32 Bitwert | s | - | unsigned long | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4AB8 | Spannung Drucksensor Saugrohrdruck (word) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x4ABC | Luftmassenfluss gefiltert (Word) | kg/h | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x4ABD | Bedingung automatischer Start | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4ABE | I-Regler Mengenregelung Kraftstoffsystem | mg | - | signed integer | - | 0,0211944580078125 | 1 | 0,0 |
| 0x4ABF | Verbrauch ohne Regler | l/h | - | unsigned integer | - | 0,0038910505827516317 | 1 | 0,0 |
| 0x4AC0 | Verbrauch mit Regler | l/h | - | unsigned integer | - | 0,0038910505827516317 | 1 | 0,0 |
| 0x4AC2 | Reset Information  | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x4AC4 | Raildruck Kraftstoffsystem Sollwert | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x4AC6 | Modus Kraftstoffsystem (Druck-, Mengen-, oder Maximumregelung) | 0-n | - | 0xFF | ba_vcv_state_text | 1 | 1 | 0 |
| 0x4ACC | Luftklappe - Sollposition in Schritten | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4ACD | Luftklappe - Istposition in Schritten | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4AD0 | Luftklappe - Diagnosestatus allgemein | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4AD1 | Luftklappe - Diagnosestatus obere Luftklappe | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4AD2 | Luftklappe - Status obere Luftklappe | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4AD3 | Luftklappe - Status untere Luftklappe | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4AD4 | Luftklappe - Varianteninfo vom Steller | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4AD5 | Kraftstofftemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x4AD6 | Bedingung Schubabschalten | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4AE2 | Reset Information - Reset-group-ID of the last reset reason | 0-n | - | 0xFF | Reset_GrpID | 1 | 1 | 0 |
| 0x4AE3 | Reset Information - Reset-ID of the last reset | 0-n | - | 0xFFFF | Reset_ID | 1 | 1 | 0 |
| 0x4AE4 | Reset Information - User defined value of the last reset reason | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x4AEB | Kühlmitteltemperatur &lt; 98°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4AEC | 98°C =&lt; Kühlmitteltemperatur =&lt; 112°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4AED | 113°C =&lt; Kühlmitteltemperatur =&lt; 120°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4AEE | 121°C =&lt; Kühlmitteltemperatur =&lt; 125°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4AEF | Kühlmitteltemperatur &gt; 125°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x4AF0 | Motoröltemperatur &lt; 80°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5800 | Zeitzähler ab Startende (16bit) | s | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5801 | Umgebungsdruck | hPa | - | unsigned char | - | 5,0 | 1 | 0,0 |
| 0x5802 | CARB FREEZE FRAME Byte, Bank 1, für LR | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5803 | CARB FREEZE FRAME Byte, Bank 2, für LR | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5804 | relative Luftmasse (calc. load value) nach SAE J1979 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5805 | Motortemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5806 | Lambda-Regler-Ausgang (Word) | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5807 | Faktor aus Lambdaregelungsadaption für Bank 1 | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5809 | Faktor aus Lambdaregelungsadaption, Bank 2 | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x580B | Saugrohr-Absolutdruck | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x580C | Motordrehzahl | 1/min | - | unsigned char | - | 40,0 | 1 | 0,0 |
| 0x580D | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 1,25 | 1 | 0,0 |
| 0x580E | Zündwinkel Zylinder 1 | Grad KW | - | signed char | - | 0,75 | 1 | 0,0 |
| 0x580F | Ansaugluft-Temperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5812 | Massenstrom HFM | kg/h | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5813 | relative Luftfüllung | % | - | unsigned char | - | 0,75 | 1 | 0,0 |
| 0x5814 | Normierter Fahrpedalwinkel | %PED | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| 0x5815 | Batteriespannung | V | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 |
| 0x5816 | Lambda-Sollwert bezogen auf Einbauort Lambda-Sensor | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x5817 | Umgebungstemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5818 | Luftmassenfluß | kg/h | - | unsigned char | - | 4,0 | 1 | 0,0 |
| 0x5819 | Motordrehzahl [1/min] | rpm | - | signed integer | - | 0,5 | 1 | 0,0 |
| 0x581A | Winkel Einlassventil oeffnet bezogen auf LWOT | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x581B | Sollwinkel Nockenwelle Einlass öffnet | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x581C | Winkel Auslassventil schließt bezogen auf LWOT | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x581D | Sollwinkel Nockenwelle Auslass schließt | Grad KW | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| 0x581E | Ansauglufttemperatur, linearisiert und umgerechnet | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5820 | Bedingung Klemme 15 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5821 | Steuergerätetemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5822 | Öltemperatur | Grad C | - | unsigned char | - | 1,0 | 1 | -60,0 |
| 0x5823 | Abstellzeit | s | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5825 | Spannung von BCU gemessen (U_BCU_LIN) | V | - | signed integer | - | 0,009999999776482582 | 1 | 0,0 |
| 0x5826 | Drosselklappenwinkel aus Poti 1 | %DK | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| 0x5827 | Tastverhältnis für Lambdasondenheizung | % | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x5828 | Tastverhältnis für Lambdasondenheizung, Bank 2 | % | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x5829 | normierte Heizleistung der Lambdasonde hinter Kat | - | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| 0x582B | Drehmomentaufnahme des Wandlers über CAN | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x582C | Lambdasonden-Istwert | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x582D | Korrekturwert der LSU-Spannung vor KAT | V | - | signed integer | - | 4,8828125E-4 | 1 | 0,0 |
| 0x582F | Abgastemperatur nach KAT aus Modell | Grad C | - | unsigned char | - | 5,0 | 1 | -50,0 |
| 0x5830 | Dynamikwert der LSU | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x5831 | Dynamikwert der LSU, Bank 2 | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x5832 | Zustand Motor-Koordinator | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5834 | Umgebungsdruck von Sensor | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x5835 | Kennung Generator Hersteller | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5836 | gefilterter Drehzahlgradient | 1/min/s | - | signed char | - | 100,0 | 1 | 0,0 |
| 0x5837 | Solldruck Hochdrucksystem | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x5838 | Relatives Moment für Aussetzererkennung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5839 | Bedingung Sicherheitskraftstoffabschaltung (SKA) | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x583A | Ansaugluft-Temperatur bei Start | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x583B | Fuellstand Kraftstofftank | L | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x583C | Batteriespannung; vom AD-Wandler erfasster Wert | V | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 |
| 0x583D | Betriebsstundenzähler | min | - | unsigned integer | - | 6,0 | 1 | 0,0 |
| 0x583E | Sollwert Drosselklappenwinkel, bez. auf unteren Anschlag | %DK | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| 0x583F | Sollwert DK-Winkel, bezogen auf unteren Anschlag | %DK | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| 0x5840 | DK-Winkel der Notluftposition | %DK | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| 0x5841 | Wert Temperatur Steuergerät | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5842 | Kennung Generatortyp | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5843 | Bedingung Startanforderung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5844 | Chiptemperatur Generator 1 | Grad C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x5845 | Sondenspannung vor Kat einer Breitbandlambdasonde (ADC-Wert) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5846 | Spannung PWG-Poti 1 (Word) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5847 | Spannung PWG-Poti 2 (Word) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5849 | ADC-Spannung Lambdasonde hinter Katalysator (Word) | V | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 |
| 0x584B | ADC-Spannung Lambdasonde hinter Katalysator Bank2 (Word) | V | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 |
| 0x584C | Spannung DK-Poti 2 | V | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| 0x584D | Massenstrom Tankentlüftung in das Saugrohr | kg/h | - | unsigned integer | - | 3,906250058207661E-4 | 1 | 0,0 |
| 0x584E | Spannung DK-Poti 1 | V | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| 0x584F | Erkennung Bordnetzinstabilität | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5850 | Signalspannung des Kühlmitteltemperatursensor | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5851 | Spannungswert des Ansauglufttemperatursensors tfa2 (SY_TFAKON &gt; 0) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5852 | Batteriestrom vom IBS | A | - | unsigned integer | - | 0,019999999552965164 | 1 | -200,0 |
| 0x5853 | Batteriespannung von IBS | V | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x5854 | Batterietemperatur vom IBS | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5855 | schneller Mittelwert des Lambdaregelfaktors (Word) | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5856 | schneller Mittelwert des Lambdaregelfaktors Bank 2(Word) | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5857 | Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x5858 | Drosselklappenwinkel bezogen auf unteren Anschlag | %DK | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| 0x5859 | Pumpenstrom Referenzleck | mA | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x585A | min. Pumpenstrom bei Grobleckmessung | mA | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x585B | Pumpenstrom am Ende der Feinstleckmessung | mA | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x585C | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT | Ohm | - | unsigned char | - | 512,0 | 1 | 0,0 |
| 0x585D | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT Bank2 | Ohm | - | unsigned char | - | 512,0 | 1 | 0,0 |
| 0x585E | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT | Ohm | - | unsigned char | - | 2,0 | 1 | 0,0 |
| 0x585F | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT Bank2 | Ohm | - | unsigned char | - | 2,0 | 1 | 0,0 |
| 0x5860 | Innenwiderstand der Nernstzelle der LSU | Ohm | - | unsigned char | - | 10,0 | 1 | 0,0 |
| 0x5861 | Innenwiderstand der Nernstzelle der LSU, Bank 2 | Ohm | - | unsigned char | - | 10,0 | 1 | 0,0 |
| 0x5862 | Sollwert Öldruck | kPa | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x5863 | Innenwiderstand der Nernstzelle der LSU | Ohm | - | unsigned char | - | 0,0390625 | 1 | 0,0 |
| 0x5864 | Innenwiderstand der Nernstzelle der LSU, Bank 2 | Ohm | - | unsigned char | - | 0,0390625 | 1 | 0,0 |
| 0x5865 | Langzeit-Ölniveau-Mittelwert für den DIS-Tester | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x5866 | Relativer Füllstand des Motoröls | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5867 | Fahrstrecke des Fahrzeugs als Information über CAN | km | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| 0x5868 | Status Standverbraucher registriert Teil 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5869 | Status Standverbraucher registriert Teil 2 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x586A | aktuelle Batteriespannung | V | - | unsigned integer | - | 2,500000118743628E-4 | 1 | 6,0 |
| 0x586B | Zeit, indem der Ruhestrom bei 80..200mA liegt | min | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| 0x586C | Zeit, indem der Ruhestrom bei 200..1000mA liegt | min | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| 0x586E | Zeit, indem der Ruhestrom größer als 1000mA liegt | min | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| 0x586F | Öldruck | hPa | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5870 | Spannung Umgebungsdrucksensor (word 10-Bit von ADC) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5871 | Zähler Prüfzustand für DVESTANZNMOT | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5872 | Reglerversion on Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5873 | Lambda-Sollwert bezogen auf Einbauort Lambda-Sensor Bank2 | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x5874 | ADC-Spannung Pumpenstrom Tankdiagnose | V | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| 0x5875 | Soll-Motormoment MSR für schnellen Eingriff | Nm | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5876 | Schnittstelle für Scan Tool Mode $01/$02 Raildruck Rohwert | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x5878 | I-Anteil der stetigen LRSHK Variante kontinuierlich | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x587C | Periodendauer des Nullgangsensorsignals | ms | - | unsigned integer | - | 9,999999747378752E-5 | 1 | 0,0 |
| 0x587D | Status Nullgangsensor | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x587F | Tastverhältnis E-Lüfter | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5881 | Ist-Gang | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5882 | Motorstarttemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x5883 | Referenzpegel Klopfregelung, 16 bit | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5884 | Kopie begrenzter Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x5885 | Referenzpegel Klopfregelung, 16bit | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5886 | Referenzpegel Klopfregelung, 16bit | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5887 | Auslastungsgrad Generator 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5888 | Referenzpegel Klopfregelung, 16bit | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5889 | Lambda-Istwert | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x588A | Lambda-Istwert Bank2 | - | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| 0x588B | Zeit nach Startende | s | - | unsigned integer | - | 0,009999999776482582 | 1 | 0,0 |
| 0x588C | Keramiktemperatur der LSU | Grad C | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 |
| 0x588D | aktuelle Zeit Leckmessung | s | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x588E | Pumpenstrom Tankdiagnose | mA | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x588F | Keramiktemperatur der LSU, Bank 2 | Grad C | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 |
| 0x5891 | Kupplungsmotormoment Istwert | Nm | - | signed integer | - | 0,5 | 1 | 0,0 |
| 0x5892 | Differenz zwischen Umgebungsdruck und  Bremskraftverstärker-Druck von Drucksensor (Rohwert) | hPa | - | signed integer | - | 0,0390625 | 1 | 0,0 |
| 0x5893 | Indiziertes Soll-Motormoment GS für schnellen Eingriff | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5894 | Spannung Klopfwerte Zylinder 2 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5895 | Spannung Klopfwerte Zylinder 5 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5896 | Abgastemperatur hinter Hauptkat aus Modell | Grad C | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 |
| 0x5898 | phys. Wert Generatorsollspannung (Volt) für Komponententreiber Generator | V | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| 0x5899 | Bedingung Anforderung Motorrelais einschalten | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x589A | Tastverhältnis Nullgangsensor | % | - | unsigned integer | - | 0,009999999776482582 | 1 | 0,0 |
| 0x589B | Bedingung unzulössig hoher Motorstrom bei Kurzschluss erkannt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x589C | Bedingung Freigabe VVT-Endstufe | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x589E | Sollwert Exzenterwinkel VVT | Grad | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x589F | Batterietemperatur | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x58A0 | Entladung während Ruhestromverletzung | Ah | - | unsigned integer | - | 0,018204445019364357 | 1 | 0,0 |
| 0x58A1 | Wegstrecke_km auf 1km genau | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x58A2 | Istwert Exzenterwinkel VVT | Grad | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58A3 | rel. Exzenterwinkel am oberen mech. Anschlag | Grad | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58A4 | Generatorstatus | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58A5 | Vom Generator empfangenes Lastsignal | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58A6 | Rel. Exzenterwinkel | Grad | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58A7 | Abstellzeit aus relativem Minutenzähler bis Motorstart | min | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58A8 | Rel. Exzenterwinkel am unteren mech. Anschlag | Grad | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58A9 | VVT Verstellbereich aus Urlernvorgang | Grad | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58AA | Verstellbereich des Exzenterwinkels | Grad | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58AB | DLR für DV-E: Summe der PID-Anteile | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x58AD | Sauerstoffspeichervermögen KAT | mg | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58AE | Peridendauer für Massenstrom aus HFM | us | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58AF | EKP-Sollvolumenstrom | l | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B0 | Zähler für Lerndauer eines Lernsteps | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B1 | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 1 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B2 | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 5 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B3 | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 3 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B4 | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 6 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B5 | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 2 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B6 | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 4 | ms | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| 0x58B7 | aktueller Bremsdruck | hPa | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B8 | Motordrehzahl in der Funktionsüberwachung | 1/min | - | unsigned char | - | 40,0 | 1 | 0,0 |
| 0x58B9 | Pedalsollwert (8 Bit) in der Funktionsüberwachung | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x58BA | Bank mittel eingespritzte effektive relative Krafftstoffmasse (inkl. Reduzierstufe) | % | - | unsigned integer | - | 0,046875 | 1 | 0,0 |
| 0x58BB | Strom für VVT-Motor | A | - | signed integer | - | 0,006103515625 | 1 | 0,0 |
| 0x58BC | relative Luftfüllung in der Funktionsüberwachung | % | - | unsigned char | - | 0,75 | 1 | 0,0 |
| 0x58BD | Status Fehler Überlast VVT1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58BE | DV-E-Adaption: Status Prüfbedingungen | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58C0 | VVT-Endstufentemperatur aus Modell | Grad C | - | unsigned integer | - | 0,75 | 1 | -48,0 |
| 0x58C1 | Korrigierte Segmentdauer | us | - | unsigned long | - | 0,05000000074505806 | 1 | 0,0 |
| 0x58C2 | Status STG Anforderung Radmoment Antriebsstrang Summe FAS | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58C3 | Status STG Anforderung Drehmoment Kurbelwelle Fahrdynamik | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58C4 | Status STG Anforderung Radmoment Antriebsstrang Summe Stabilisierung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58C5 | Status STG ist Bremsmoment Summe | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58C6 | Status STG ist Lenkwinkel Vorderachse | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58C7 | Status STG Status Stabilisierung DSC | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58C8 | geforderte Drehmomentänderung von der LLR (I-Anteil) | % | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x58C9 | vvtmode | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58CA | geforderte MD-Änderung von der LLR (PD-Zündungsanteil) | % | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x58CB | PD-Anteil schnell Leerlaufregelung | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58CC | Verlustmoment Überwachung | % | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x58CD | Verlustmomentabweichung Überwachung | V | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58CE | Carrierbyte Schalterstati | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58CF | Soll- Motormoment aus Getriebeüberwachung in der Funktionsüberwachung | Nm | - | signed integer | - | 0,0625 | 1 | 0,0 |
| 0x58D0 | Berechnetes Ist-Moment in der Funktionsüberwachung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58D1 | Massenstrom Abgas ohne Kraftstoffanteil vor Hauptkatalysator | kg/h | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58D2 | Luftklappe - Sollposition in Grad | - | - | unsigned char | - | 0,501960813999176 | 1 | 0,0 |
| 0x58D3 | Luftklappe - Istposition in Grad | - | - | unsigned char | - | 0,501960813999176 | 1 | 0,0 |
| 0x58D4 | Startbedingung Kraftschluss erfüllt | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x58D5 | physikalischer Temperaturwert, der sich bei Wandlung der elektrischen Sensorspannung wtfa1_w ergibt | Grad C | - | unsigned char | - | 0,75 | 1 | -48,0 |
| 0x58D7 | Spannungswert des Ansauglufttemperatursensors tfa1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x58D8 | Differenz-DK-Winkel Sollwert - Istwert | %DK | - | signed integer | - | 0,0244140625 | 1 | 0,0 |
| 0x58D9 | Schrittzähler DK-Rückstellfeder-Prüfung | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58DA | koordiniertes Moment für Füllung | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x58DB | Fehlerzähler abgasrelevante Aussetzer über alle Zylinder | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58DC | Intervallzähler für abgasrelevante Aussetzer | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x58DD | Druck vor Drosselklappe Rohwert | hPa | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| 0x58DE | Spannung Drucksensor vor Drosselklappe | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x58E0 | Abgleich DK-Modell (Faktor) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x58E1 | Abgleich DK-Modell (Offset) | kg/h | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58E2 | Abgleich EV-Modell (Faktor) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x58E3 | Abgleich EV-Modell (Offset) | kg/h | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58E4 | Ist-Betriebsart | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58E9 | empf. Spannung von BSS-Wasserpumpe | V | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58EA | empf. Istdrehzahl von BSS-Wasserpumpe | 1/min | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58EC | empf. Temperatur von BSS-Wasserpumpe | Grad C | - | unsigned char | - | 1,0 | 1 | -50,0 |
| 0x58ED | empf. Strom von BSS-Wasserpumpe | % | - | unsigned char | - | 0,5 | 1 | 0,0 |
| 0x58EF | Gefilterter Raildruck-Istwert (Absolutdruck) | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x58F0 | ungefilterter Raildruck Istwert (abs.) | MPa | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| 0x58F2 | Tastverhältnis Mengensteuerventil | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x58F3 | Ungefilterter Niederdruck Rohwert | kPa | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| 0x58F4 | Spannung Kraftstoffniederdrucksensor im 1 ms Raster | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x58F5 | Spannung Diagnose-Port VVT-Ansteuerung (3V ADC) | V | - | unsigned char | - | 0,012890624813735485 | 1 | 0,0 |
| 0x58F6 | Sollspannung des VVT Lagereglers | V | - | signed integer | - | 7,812500116415322E-4 | 1 | 0,0 |
| 0x58F7 | VVT-Strom | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58FA | gefilterter Faktor Tankentlüftungs-Adaption | - | - | signed char | - | 0,5 | 1 | 0,0 |
| 0x58FC | Fertigungs-Werkstatt-,Transportmodus | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58FD | Untermodi des Fe Tra Fla Mode | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0xF400 | PID 00 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF401 | PID 01 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF402 | PID 02 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF403 | PID 03 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF404 | PID 04 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF405 | PID 05 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF406 | PID 06 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF407 | PID 07 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF40B | PID 0B | text | - | 1 | - | 1 | 1 | 0 |
| 0xF40C | PID 0C | text | - | 2 | - | 1 | 1 | 0 |
| 0xF40D | PID 0D | text | - | 1 | - | 1 | 1 | 0 |
| 0xF40E | PID 0E | text | - | 1 | - | 1 | 1 | 0 |
| 0xF40F | PID 0F | text | - | 1 | - | 1 | 1 | 0 |
| 0xF410 | PID 10 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF411 | PID 11 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF412 | PID 12 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF413 | PID 13 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF414 | PID 14 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF415 | PID 15 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF416 | PID 16 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF417 | PID 17 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF418 | PID 18 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF419 | PID 19 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF41A | PID 1A | text | - | 2 | - | 1 | 1 | 0 |
| 0xF41B | PID 1B | text | - | 2 | - | 1 | 1 | 0 |
| 0xF41C | PID 1C | text | - | 1 | - | 1 | 1 | 0 |
| 0xF41D | PID 1D | text | - | 1 | - | 1 | 1 | 0 |
| 0xF41E | PID 1E | text | - | 1 | - | 1 | 1 | 0 |
| 0xF41F | PID 1F | text | - | 2 | - | 1 | 1 | 0 |
| 0xF420 | PID 20 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF421 | PID 21 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF422 | PID 22 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF423 | PID 23 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF424 | PID 24 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF425 | PID 25 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF426 | PID 26 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF427 | PID 27 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF428 | PID 28 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF429 | PID 29 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF42A | PID 2A | text | - | 4 | - | 1 | 1 | 0 |
| 0xF42B | PID 2B | text | - | 4 | - | 1 | 1 | 0 |
| 0xF42C | PID 2C | text | - | 1 | - | 1 | 1 | 0 |
| 0xF42D | PID 2D | text | - | 1 | - | 1 | 1 | 0 |
| 0xF42E | PID 2E | text | - | 1 | - | 1 | 1 | 0 |
| 0xF42F | PID 2F | text | - | 1 | - | 1 | 1 | 0 |
| 0xF430 | PID 30 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF431 | PID 31 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF432 | PID 32 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF433 | PID 33 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF434 | PID 34 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF435 | PID 35 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF436 | PID 36 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF437 | PID 37 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF438 | PID 38 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF439 | PID 39 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF43A | PID 3A | text | - | 4 | - | 1 | 1 | 0 |
| 0xF43B | PID 3B | text | - | 4 | - | 1 | 1 | 0 |
| 0xF43C | PID 3C | text | - | 2 | - | 1 | 1 | 0 |
| 0xF43D | PID 3D | text | - | 2 | - | 1 | 1 | 0 |
| 0xF43E | PID 3E | text | - | 2 | - | 1 | 1 | 0 |
| 0xF43F | PID 3F | text | - | 2 | - | 1 | 1 | 0 |
| 0xF440 | PID 40 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF441 | PID 41 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF442 | PID 42 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF443 | PID 43 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF444 | PID 44 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF445 | PID 45 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF446 | PID 46 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF447 | PID 47 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF448 | PID 48 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF449 | PID 49 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF44A | PID 4A | text | - | 1 | - | 1 | 1 | 0 |
| 0xF44B | PID 4B | text | - | 1 | - | 1 | 1 | 0 |
| 0xF44C | PID 4C | text | - | 1 | - | 1 | 1 | 0 |
| 0xF44D | PID 4D | text | - | 2 | - | 1 | 1 | 0 |
| 0xF44E | PID 4E | text | - | 2 | - | 1 | 1 | 0 |
| 0xF44F | PID 4F | text | - | 4 | - | 1 | 1 | 0 |
| 0xF450 | PID 50 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF451 | PID 51 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF452 | PID 52 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF453 | PID 53 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF454 | PID 54 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF455 | PID 55 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF456 | PID 56 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF457 | PID 57 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF458 | PID 58 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF459 | PID 59 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF45A | PID 5A | text | - | 1 | - | 1 | 1 | 0 |
| 0xF45B | PID 5B | text | - | 1 | - | 1 | 1 | 0 |
| 0xF45C | PID 5C | text | - | 1 | - | 1 | 1 | 0 |
| 0xF45D | PID 5D | text | - | 2 | - | 1 | 1 | 0 |
| 0xF45E | PID 5E | text | - | 2 | - | 1 | 1 | 0 |
| 0xF45F | PID 5F | text | - | 1 | - | 1 | 1 | 0 |
| 0xF460 | PID 60 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF461 | PID 61 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF462 | PID 62 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF463 | PID 63 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF464 | PID 64 | text | - | 5 | - | 1 | 1 | 0 |
| 0xF465 | PID 65 | text | - | 2 | - | 1 | 1 | 0 |
| 0xF466 | PID 66 | text | - | 5 | - | 1 | 1 | 0 |
| 0xF467 | PID 67 | text | - | 3 | - | 1 | 1 | 0 |
| 0xF468 | PID 68 | text | - | 7 | - | 1 | 1 | 0 |
| 0xF469 | PID 69 | text | - | 7 | - | 1 | 1 | 0 |
| 0xF46A | PID 6A | text | - | 5 | - | 1 | 1 | 0 |
| 0xF46B | PID 6B | text | - | 5 | - | 1 | 1 | 0 |
| 0xF46C | PID 6C | text | - | 5 | - | 1 | 1 | 0 |
| 0xF46D | PID 6D | text | - | 11 | - | 1 | 1 | 0 |
| 0xF46E | PID 6E | text | - | 9 | - | 1 | 1 | 0 |
| 0xF46F | PID 6F | text | - | 3 | - | 1 | 1 | 0 |
| 0xF470 | PID 70 | text | - | 10 | - | 1 | 1 | 0 |
| 0xF471 | PID 71 | text | - | 6 | - | 1 | 1 | 0 |
| 0xF472 | PID 72 | text | - | 5 | - | 1 | 1 | 0 |
| 0xF473 | PID 73 | text | - | 5 | - | 1 | 1 | 0 |
| 0xF474 | PID 74 | text | - | 5 | - | 1 | 1 | 0 |
| 0xF475 | PID 75 | text | - | 7 | - | 1 | 1 | 0 |
| 0xF476 | PID 76 | text | - | 7 | - | 1 | 1 | 0 |
| 0xF477 | PID 77 | text | - | 5 | - | 1 | 1 | 0 |
| 0xF478 | PID 78 | text | - | 9 | - | 1 | 1 | 0 |
| 0xF479 | PID 79 | text | - | 9 | - | 1 | 1 | 0 |
| 0xF47A | PID 7A | text | - | 7 | - | 1 | 1 | 0 |
| 0xF47B | PID 7B | text | - | 7 | - | 1 | 1 | 0 |
| 0xF47C | PID 7C | text | - | 9 | - | 1 | 1 | 0 |
| 0xF47D | PID 7D | text | - | 1 | - | 1 | 1 | 0 |
| 0xF47E | PID 7E | text | - | 1 | - | 1 | 1 | 0 |
| 0xF47F | PID 7F | text | - | 13 | - | 1 | 1 | 0 |
| 0xF480 | PID 80 | text | - | 4 | - | 1 | 1 | 0 |
| 0xF481 | PID 81 | text | - | 21 | - | 1 | 1 | 0 |
| 0xF482 | PID 82 | text | - | 21 | - | 1 | 1 | 0 |
| 0xF483 | PID 83 | text | - | 5 | - | 1 | 1 | 0 |
| 0xF484 | PID 84 | text | - | 1 | - | 1 | 1 | 0 |
| 0xF485 | PID 85 | text | - | 10 | - | 1 | 1 | 0 |
| 0xF486 | PID 86 | text | - | 5 | - | 1 | 1 | 0 |
| 0xF487 | PID 87 | text | - | 5 | - | 1 | 1 | 0 |
| 0x58FF | Umweltbedingung unbekannt | - | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |

<a id="table-messwertetab"></a>
### MESSWERTETAB

Dimensions: 388 rows × 12 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| IPUMG | 0x4201 | STAT_UMGEBUNGSDRUCK_WERT | Umgebungsdruck | hPa | pu_w | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| IPLAD | 0x4205 | STAT_LADEDRUCK_WERT | Druck vor Drosselklappe | hPa | pvd_w | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| ITKUM | 0x4300 | STAT_KUEHLMITTELTEMPERATUR_WERT | Motor-Temperatur | Grad C | tmot | - | unsigned char | - | 0,75 | 1 | -48,0 |
| SNWAP | 0x4306 | STAT_WASSERPUMPE_DREHZAHL_SOLL_WERT | Quittung  Solldrehzahl von BSS-Wasserpumpe | 1/min | wmpdzst | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x4307_WERT | 0x4307 | STAT_0x4307_WERT | empf. Status von BSS-Wasserpumpe | - | wmstat | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ITOEL | 0x4402 | STAT_OELTEMPERATUR_WERT | Oeltemperatur nach Filter | Grad C | toel_w | - | unsigned integer | - | 0,75 | 1 | -48,0 |
| IKVLS | 0x4403 | STAT_KRAFTSTOFFVERBRAUCH_SEIT_SERVICE_WERT | Kraftstoffverbrauch seit letztem Ölwechsel | - | ozkvbsm_ul | - | unsigned long | - | 1,220703125E-4 | 1 | 0,0 |
| IKMLS | 0x4404 | STAT_WEG_SEIT_SERVICE_WERT | Ölkilometer | km | ozoelkm | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| RNIOE | 0x4405 | STAT_OELSENSOR_NIVEAU_ROH_WERT | Sensorrohwert Ölniveau | - | oznivr | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| RQUOE | 0x4406 | STAT_OELSENSOR_QUALITAET_ROH_WERT | Sensorrohwert Permittivität | - | ozpermr_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| RTOEL | 0x4407 | STAT_OELSENSOR_TEMPERATUR_ROH_WERT | Sensorrohwert Öltemperatur | - | oztempr | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| ITSOE | 0x4408 | STAT_OELSENSOR_TEMPERATUR_WERT | Öltemperatur ungefiltert | Grad C | oztemp_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| INIOE | 0x4409 | STAT_OELSENSOR_NIVEAU_WERT | Ölniveau ungefiltert in [mm] | - | ozniv | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| IQOEL | 0x440A | STAT_OELSENSOR_QUALITAET_WERT | Permitivität für den Tester | - | ozpermakt | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| STAT_0x440B_WERT | 0x440B | STAT_0x440B_WERT | CodingDataSet-ÖL-Länderfaktor1- EEPROM | - | ozlf1c_eep | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| STAT_0x440C_WERT | 0x440C | STAT_0x440C_WERT | CodingDataSet-ÖL-Länderfaktor2- EEPROM | - | ozlf2c_eep | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| STAT_0x440D_WERT | 0x440D | STAT_0x440D_WERT | Länderfaktor 1 | - | ozlf1t | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| STAT_0x440E_WERT | 0x440E | STAT_0x440E_WERT | Länderfaktor 2 | - | ozlf2t | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| STAT_0x440F_WERT | 0x440F | STAT_0x440F_WERT | Kurzzeit-Ölniveau-Mittelwert für den DIS-Tester | - | oznivkrzt | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| STAT_0x4411_WERT | 0x4411 | STAT_0x4411_WERT | Restweg aus Kraftstoffverbrauch abgeleitet | - | ozrwkvb | - | signed integer | - | 10,0 | 1 | 0,0 |
| STAT_0x4412_WERT | 0x4412 | STAT_0x4412_WERT | Öllaufzeit | month | ozoelzeit | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x4418_WERT | 0x4418 | STAT_0x4418_WERT | Status Ölzustandssensor | - | ozstatus | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| SSPEI | 0x4505 | STAT_NW_EINLASSSPREIZUNG_SOLL_WERT | Sollwinkel vom BMW Layer (Einlass-VANOS) | Grad KW | wnwsaeb_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| IPNWE | 0x4506 | STAT_POSITION_NOCKENWELLE_EINLASS_WERT | Einlassnockenwellenposition | Grad KW | wnwkwe_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| IPNWA | 0x4507 | STAT_POSITION_NOCKENWELLE_AUSLASS_WERT | Auslassnockenwellenposition | Grad KW | wnwkwa_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x450C_WERT | 0x450C | STAT_0x450C_WERT | Kurbelwellenadaption Einlass erfolgt | 0/1 | B_phade | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x450D_WERT | 0x450D | STAT_0x450D_WERT | Kurbelwellenadaption Auslass erfolgt | 0/1 | B_phada | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x450E_WERT | 0x450E | STAT_0x450E_WERT | Kurbelwellennullpunktverschiebung in Grad für Winkelversatzdiagnose | deg CrS | EpmCaS_phiDiffAvrgLim | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x4510_WERT | 0x4510 | STAT_0x4510_WERT | VVT-Lageregler, bleibende Abweichung erkannt | 0/1 | B_dvvtregelabweichung | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4511_WERT | 0x4511 | STAT_0x4511_WERT | VVT-Lageregelung, Schwingung erkannt | 0/1 | B_dvvtschwingung | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4512_WERT | 0x4512 | STAT_0x4512_WERT | VVT überlastet | 0/1 | B_vvttempovl_wrn | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4513_WERT | 0x4513 | STAT_0x4513_WERT | VVT-Überlastung, klemmender Steller | 0/1 | B_vvttempovl | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4514_WERT | 0x4514 | STAT_0x4514_WERT | VVT-Adaption möglich | 0/1 | B_enadpvvt | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4515_WERT | 0x4515 | STAT_0x4515_WERT | Anforderung, VVT-Anschlaglernen | - | vvtlrnaf | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x4516_WERT | 0x4516 | STAT_0x4516_WERT | Status VVT-Anschlaglernen | - | vvtlrnst | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x4517_WERT | 0x4517 | STAT_0x4517_WERT | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 0 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x4518_WERT | 0x4518 | STAT_0x4518_WERT | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 1 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x4519_WERT | 0x4519 | STAT_0x4519_WERT | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 2 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x451A_WERT | 0x451A | STAT_0x451A_WERT | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 3 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x451B_WERT | 0x451B | STAT_0x451B_WERT | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 4 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x451C_WERT | 0x451C | STAT_0x451C_WERT | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 5 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x451D_WERT | 0x451D | STAT_0x451D_WERT | Gesamtzeit VVT-Performancetest | - | vvtdtperf_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x451E_WERT | 0x451E | STAT_0x451E_WERT | Stromsumme VVT-Performancetest | A | ivvtsumperf_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| IWDKL | 0x4600 | STAT_DROSSELKLAPPENWINKEL_WERT | Drosselklappenwinkel bezogen auf unteren Anschlag | %DK | wdkba_w | - | signed integer | - | 0,0244140625 | 1 | 0,0 |
| SWDKL | 0x4601 | STAT_DROSSELKLAPPENWINKEL_SOLL_WERT | Sollwert Drosselklappenwinkel, bezogen auf (unteren) Anschlag | % | wdks_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IIGEN | 0x4604 | STAT_GENERATOR_STROM_WERT | Generatorstrom | - | st_i_gen | - | unsigned char | - | 1,0 | 1 | 0,0 |
| VGENE | 0x4605 | STAT_GENERATOR_CHIPVERSION_WERT | Chipversion Generator 2 | - | bsdgencv | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IUBAT | 0x460A | STAT_UBATT_WERT | momentane Batteriespannung | V | ubt | - | unsigned integer | - | 0,014999999664723873 | 1 | 0,0 |
| IUADW | 0x460C | STAT_UBATT_AD_WANDLER_WERT | Batteriespannung; vom AD-Wandler erfaßter Wert  | V | wub_w | - | unsigned integer | - | 0,02355000004172325 | 1 | 0,0 |
| STAT_0x460D_WERT | 0x460D | STAT_0x460D_WERT | Korrekturwert Abschaltung | % | abschkor_w | - | unsigned integer | - | 0,004000000189989805 | 1 | -100,0 |
| TDSTF | 0x460E | STAT_0x460E_WERT | Abstand zur Startfähigkeit | % | dsoc_w | - | unsigned integer | - | 0,004000000189989805 | 1 | -100,0 |
| ILBAT | 0x460F | STAT_BATTERIELAST_WERT | DF-Monitor für Batterie-Ladezustand in % | % | dfmonitor | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STAT_0x4613_WERT | 0x4613 | STAT_0x4613_WERT | vom Generator empfangene Generatorsollspannung (Kopie gesendeter Wert) | V | ufgen | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| STAT_0x4615_WERT | 0x4615 | STAT_0x4615_WERT | Kopie begrenzter Erregerstrom Generator 1 | A | ierrfgrenz | - | unsigned char | - | 0,125 | 1 | 0,0 |
| STAT_0x4616_WERT | 0x4616 | STAT_0x4616_WERT | vom Generator empfangene Load response Zeit (Kopie gesendeter Wert) | s | tlrfgen | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x4617_WERT | 0x4617 | STAT_0x4617_WERT | gefiltertes Generatormoment absolut | % | mdgenvf_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x4618_WERT | 0x4618 | STAT_0x4618_WERT | Drehzahlschwelle für LR-Funktion Generator 1 aktiv | 0/1 | B_lrfoff | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4619_WERT | 0x4619 | STAT_0x4619_WERT | Bedingung BSD Protokollinhalt für BSD2 Regler | 0/1 | B_bsdprot2 | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x461A_WERT | 0x461A | STAT_0x461A_WERT | Nominalspannung Regler Generator 1 | V | uregnom | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| STAT_0x4680_WERT | 0x4680 | STAT_0x4680_WERT | Leerlaufdrehzahl gelernt | 0/1 | B_nggelernt | - | 0xFF | - | 1 | 1 | 0 |
| STAT_0x4681_WERT | 0x4681 | STAT_0x4681_WERT | Bereitschaft Getriebe Neutralposition anlernen | 0/1 | B_ngimlf | - | 0xFF | - | 1 | 1 | 0 |
| ISBV1 | 0x4700 | STAT_SONDENBEREITSCHAFT_VORKAT_BANK1 | Bedingung Sonde betriebsbereit vor Kat | 0/1 | B_sbbvk | - | unsigned char | - | 1 | 1 | 0 |
| ISBV2 | 0x4701 | STAT_SONDENBEREITSCHAFT_VORKAT_BANK2 | Bedingung Sonde betriebsbereit vor Kat, Bank 2 | 0/1 | B_sbbvk2 | - | unsigned char | - | 1 | 1 | 0 |
| IUSO1 | 0x4702 | STAT_SONDENSPANNUNG_VORKAT_BANK1_MIT_OFFSET_WERT | Offset korrigierte Sondenspannung vor Kat einer Breitbandlambdasonde | V | ua10mo_w | - | unsigned integer | - | 4,8828125E-4 | 1 | 0,0 |
| IUSO2 | 0x4703 | STAT_SONDENSPANNUNG_VORKAT_BANK2_MIT_OFFSET_WERT | Offset korrigierte Sondenspannung vor Kat einer Breitbandlambdasonde Bank 2 | V | ua10mo2_w | - | unsigned integer | - | 4,8828125E-4 | 1 | 0,0 |
| SINT1 | 0x4704 | STAT_LAMBDA_BANK1_SOLL_WERT | Lambdasoll Begrenzung (word) | - | lamsbg_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| SINT2 | 0x4705 | STAT_LAMBDA_BANK2_SOLL_WERT | Lambdasoll Begrenzung (word) Bank2 | - | lamsbg2_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| ISKUB | 0x4800 | STAT_KUPPLUNGSSCHALTER_BETAETIGT_WERT | Bedingung Kupplungspedal betätigt | 0/1 | B_kuppl | - | unsigned char | - | 1 | 1 | 0 |
| ISKUV | 0x4801 | STAT_KUPPLUNGSSCHALTER_VORHANDEN_WERT | Schalter Kupplung | 0/1 | S_kupp | - | unsigned char | - | 1 | 1 | 0 |
| ISSPO | 0x4802 | STAT_SPORTTASTER_BETAETIGT_WERT | Bedingung umschalten auf KFPEDS | 0/1 | B_pedsport | - | unsigned char | - | 1 | 1 | 0 |
| ISKLI | 0x4803 | STAT_KLIMA_EIN | Bedingung für Kompressoreinschalten | 0/1 | B_koe | - | unsigned char | - | 1 | 1 | 0 |
| ISSRC | 0x4805 | STAT_STARTRELAIS_UEBER_CAN_WERT | Schalter Klemme 50 von CAN | 0/1 | S_ckl50 | - | unsigned char | - | 1 | 1 | 0 |
| INMOT | 0x4807 | STAT_MOTORDREHZAHL_WERT | Motordrehzahl | 1/min | nmot_w | - | unsigned integer | - | 0,25 | 1 | 0,0 |
| SNLLD | 0x4808 | STAT_LEERLAUFDREHZAHL_SOLL_WERT | Leerlaufsolldrehzahl | 1/min | nsol_w | - | unsigned integer | - | 0,25 | 1 | 0,0 |
| ISLLA | 0x4809 | STAT_LEERLAUF_AKTIV | Bedingung Leerlaufregelung | 0/1 | B_llr | - | unsigned char | - | 1 | 1 | 0 |
| IFPWG | 0x480B | STAT_FAHRERWUNSCH_PEDAL_WERT | normierter Fahrpedalwinkel | %PED | wped_w | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| STAT_0x4880_WERT | 0x4880 | STAT_0x4880_WERT | Max. Quotient Zündwinkelwirkungsgrad-Fehlerintegral im Leerlauf bez. auf Schwellwert | % | etkhlmx | - | unsigned char | - | 0,78125 | 1 | 0,0 |
| STAT_0x4881_WERT | 0x4881 | STAT_0x4881_WERT | Max. Quotient Zündwinkelwirkungsgrad-Fehlerintegral im Teillast bez. auf Schwellwert | % | etkhtmx | - | unsigned char | - | 0,78125 | 1 | 0,0 |
| STAT_0x4A02_WERT | 0x4A02 | STAT_0x4A02_WERT | ATL-Leckagediagnose läuft | 0/1 | B_atlberlek | - | unsigned char | - | 1 | 1 | 0 |
| IUDMT | 0x4A17 | STAT_DMTL_SPANNUNG_WERT | Spannung Pumpenstrom Tankdiagnose | V | uptes_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x4A1B_WERT | 0x4A1B | STAT_0x4A1B_WERT | Elektrische Kraftstoffpumpe | 0/1 | B_ekp | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4A1D_WERT | 0x4A1D | STAT_0x4A1D_WERT | Spannung Bremsenunterdruck | V | udsbkv_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| ITKUA | 0x4A21 | STAT_KUEHLERAUSLASSTEMPERATUR_WERT | Kühlmitteltemperatur (Sensorwert) nach Tiefpassfilterung | Grad C | tmotlinf | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x4A2B_WERT | 0x4A2B | STAT_0x4A2B_WERT | physikalischer Temperaturwert, der sich bei Wandlung der tiefpassgefilterten Sensorspannung wtfa1f_w | Grad C | tfa1linf | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x4A2D_WERT | 0x4A2D | STAT_0x4A2D_WERT | Saugrohr-Absolutdruck gemessen | hPa | psrg_w | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| ILUZ1 | 0x4A30 | STAT_LAUFUNRUHE_ZYL1_WERT | Laufunruhe Zylinder 1 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| ILUZ2 | 0x4A31 | STAT_LAUFUNRUHE_ZYL2_WERT | Laufunruhe Zylinder 2 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| ILUZ3 | 0x4A32 | STAT_LAUFUNRUHE_ZYL3_WERT | Laufunruhe Zylinder 3 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| ILUZ4 | 0x4A33 | STAT_LAUFUNRUHE_ZYL4_WERT | Laufunruhe Zylinder 4 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| ILUZ5 | 0x4A34 | STAT_LAUFUNRUHE_ZYL5_WERT | Laufunruhe Zylinder 5 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| ILUZ6 | 0x4A35 | STAT_LAUFUNRUHE_ZYL6_WERT | Laufunruhe Zylinder 6 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 |
| ISKLO | 0x4A36 | STAT_STATUS_KLOPFEN_WERT | Bedingung für erkannte Klopfer | 0/1 | B_kl | - | unsigned char | - | 1 | 1 | 0 |
| IUKZ1 | 0x4A37 | STAT_KLOPFWERT_ZYL1_SPANNUNG_WERT | normierter Referenzpegel Klopfregelung Zylinder 1 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUKZ2 | 0x4A38 | STAT_KLOPFWERT_ZYL2_SPANNUNG_WERT | normierter Referenzpegel Klopfregelung Zylinder 2 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUKZ3 | 0x4A39 | STAT_KLOPFWERT_ZYL3_SPANNUNG_WERT | normierter Referenzpegel Klopfregelung Zylinder 3 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUKZ4 | 0x4A3A | STAT_KLOPFWERT_ZYL4_SPANNUNG_WERT | normierter Referenzpegel Klopfregelung Zylinder 4 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUKZ5 | 0x4A3B | STAT_KLOPFWERT_ZYL5_SPANNUNG_WERT | normierter Referenzpegel Klopfregelung Zylinder 5 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUKZ6 | 0x4A3C | STAT_KLOPFWERT_ZYL6_SPANNUNG_WERT | normierter Referenzpegel Klopfregelung Zylinder 6 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IZWZ1 | 0x4A49 | STAT_ZUENDWINKEL_ZYL1_WERT | Ausgegebener Zündwinkel | Grad KW | zwoutzyl_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| ILAB1 | 0x4A50 | STAT_LAMBDA_BANK1_WERT | Lambda-Istwert | - | lamsoni_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| ILAB2 | 0x4A51 | STAT_LAMBDA_BANK2_WERT | Lambda-Istwert Bank2 | - | lamsoni2_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| IRNK1 | 0x4A52 | STAT_READINESS_SONDE_NACHKAT_BANK1_WERT | Bedingung Sonde betriebsbereit hinter Kat | 0/1 | B_sbbhk | - | unsigned char | - | 1 | 1 | 0 |
| IRNK2 | 0x4A53 | STAT_READINESS_SONDE_NACHKAT_BANK2_WERT | Bedingung Sonde betriebsbereit hinter Kat Bank2 | 0/1 | B_sbbhk2 | - | unsigned char | - | 1 | 1 | 0 |
| ISHN1 | 0x4A54 | STAT_SONDENHEIZUNG_NACHKAT_BANK1_WERT | Bedingung Sonde hinter Kat ausreichend beheizt | 0/1 | B_hsha | - | unsigned char | - | 1 | 1 | 0 |
| ISHN2 | 0x4A55 | STAT_SONDENHEIZUNG_NACHKAT_BANK2_WERT | Bedingung Sonde 2 hinter Kat ausreichend beheizt | 0/1 | B_hsha2 | - | unsigned char | - | 1 | 1 | 0 |
| ISHV1 | 0x4A56 | STAT_SONDENHEIZUNG_VORKAT_BANK1_WERT | Bedingung: Heizerstatus A liegt vor, Sonde ist ausreichend aufgeheizt | 0/1 | B_hstlsua | - | unsigned char | - | 1 | 1 | 0 |
| ISHV2 | 0x4A57 | STAT_SONDENHEIZUNG_VORKAT_BANK2_WERT | Bedingung: Heizerstatus A liegt vor, Sonde ist ausreichend aufgeheizt, Bank2 | 0/1 | B_hstlsua2 | - | unsigned char | - | 1 | 1 | 0 |
| ISBLS | 0x4A60 | STAT_BREMSLICHTSCHALTER_EIN_WERT | Bedingung Bremslichtschalter betätigt | 0/1 | B_bl | - | unsigned char | - | 1 | 1 | 0 |
| ISBLT | 0x4A61 | STAT_BREMSLICHTTESTSCHALTER_EIN_WERT | Bedingung Bremstestschalter betätigt | 0/1 | B_br | - | unsigned char | - | 1 | 1 | 0 |
| ISAGK | 0x4A65 | STAT_ABGASKLAPPE_EIN_WERT | Bedingung Abgasklappe mit Resonator | 0/1 | B_akr | - | unsigned char | - | 1 | 1 | 0 |
| ISDMP | 0x4A66 | STAT_DMTL_PUMPE_EIN_WERT | Bedingung DMTL-Pumpenmotor an | 0/1 | B_admtpm | - | unsigned char | - | 1 | 1 | 0 |
| ISDMV | 0x4A67 | STAT_DMTL_VENTIL_EIN_WERT | Bedingung DMTL-Magnetventil an | 0/1 | B_admtmv | - | unsigned char | - | 1 | 1 | 0 |
| ISDMH | 0x4A68 | STAT_DMTL_HEIZUNG_EIN_WERT | Bedingung Heizung DM-TL Portansteuerung | 0/1 | B_hdmtlp | - | unsigned char | - | 1 | 1 | 0 |
| ISMIL | 0x4A69 | STAT_MIL_EIN_WERT | MIL-Ansteuerung | 0/1 | B_mil | - | unsigned char | - | 1 | 1 | 0 |
| ISFGR | 0x4A6A | STAT_LAMPE_FGR_EIN_WERT | Lampe FGR ein | 0/1 | B_fgr | - | unsigned char | - | 1 | 1 | 0 |
| ISCEL | 0x4A6B | STAT_CHECK_ENGINE_LAMPE_EIN_WERT | Bedingung für Ansteuerung EGAS-Fehlerlampe | 0/1 | B_epcl | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4A6C_WERT | 0x4A6C | STAT_0x4A6C_WERT | Korrekturfaktor für die Kraftstoffmenge | % | kva_korr | - | signed char | - | 0,0010000000474974513 | 1 | 0,0 |
| IAKFT | 0x4A74 | STAT_BEHEIZTER_THERMOSTAT_PWM_WERT | Tastverhältnis Kennfeldthermostat | - | tkwpwm | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| IATEV | 0x4A77 | STAT_TEV_PWM_WERT | ausgegebenes Tastverhältnis für Tankentlüftungsventil (16 Bit) | % | tateout_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IAVEP | 0x4A7A | STAT_VANOS_EINLASS_PWM_WERT | Tastverhältnis Einlaßnockenwellenregelung Ansteuerung Endstufe(word) | % | tanwree_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IAVAP | 0x4A7B | STAT_VANOS_AUSLASS_PWM_WERT | Tastverhältnis Auslaßnockenwellenregelung Ansteuerung Endstufe(word) | % | tanwraa_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IMUL1 | 0x4A85 | STAT_ADAPTION_MULTIPLIKATIV_BANK1_WERT | multiplikative Gemischkorrektur der Gemischadaption (Word) | - | fra_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| STAT_0x4A91_WERT | 0x4A91 | STAT_0x4A91_WERT | Amplitudenverhältnis laafh/laafv gefiltert | - | avkatf | - | unsigned char | - | 0,00390625 | 1 | 0,0 |
| STAT_0x4A92_WERT | 0x4A92 | STAT_0x4A92_WERT | Amplitudenverhältnis laafh/laafv gefiltert Bank2 | - | avkatf2 | - | unsigned char | - | 0,00390625 | 1 | 0,0 |
| STAT_0x4A93_WERT | 0x4A93 | STAT_0x4A93_WERT | Fehlerzähler für Lernen Nullgang | - | GbxNPos_ctDefPlausDia | - | unsigned char | - | 1,0 | 1 | 0,0 |
| SANWA | 0x4A94 | STAT_NW_AUSLASS_SOLL_WERT | gespeicherter Nockenwellensollwinkel Auslaß | Grad KW | wnwsswa_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| IANWA | 0x4A95 | STAT_NW_ADAPTION_AUSLASS_WERT | Adaptionswert Nockenwelle Auslass Bank 1 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| IANWE | 0x4A96 | STAT_NW_ADAPTION_EINLASS_WERT | Adaptionswert Nockenwelle Einlass Bank 1 | deg CrS | EpmCaS_phiAdapRefPosI1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 |
| STAT_0x4A97_WERT | 0x4A97 | STAT_0x4A97_WERT | Bedi. Vanos Einlass im Anschlag | 0/1 | B_vseansch | - | unsigned char | - | 1 | 1 | 0 |
| IAKWF | 0x4A99 | STAT_KURBELWELLEN_ADAPTION_BEENDET_WERT | Status der fuel-off Adaption im aktuellen Betriebsbereich | - | fofstat | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x4A9D_WERT | 0x4A9D | STAT_0x4A9D_WERT | multiplikative Gemischkorrektur der Gemischadaption | - | frai_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| IDSLS | 0x4AA1 | STAT_SLS_DIAGNOSE_WERT | Zyklusflag: Tankentlüftungsventil Endstufe | - | Z_teve_byte | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IDTEV | 0x4AA2 | STAT_TEV_DIAGNOSE_WERT | Funktionsstatus-Zähler DM-TL für Testerausgabe aus letztem Fahrzyklus | - | stpdmtla | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IDLSS | 0x4AA4 | STAT_LS_DIAGNOSE_WERT | Funktionsstatus LLRNS bei Anforderung Systemcheck | - | llsstat | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x4AAA_WERT | 0x4AAA | STAT_0x4AAA_WERT | Tastverhältnis PWM Ansteuerung Öldruck | % | tvpoel_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x4AAB_WERT | 0x4AAB | STAT_0x4AAB_WERT | Tastverhältnis an Endstufe des Ladedruckstellers | % | tvldste_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5AAC_WERT | 0x4AAC | STAT_0x5AAC_WERT | Tastverhältnis an Endstufe des Ladedruckstellers, Bank 2 | % | tvldste2_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x4AB0_WERT | 0x4AB0 | STAT_0x4AB0_WERT | Ladedruck- Sollwert | hPa | psolldr_w | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| IVKMH | 0x4AB1 | STAT_GESCHWINDIGKEIT_WERT | Fahrzeuggeschwindigkeit | km/h | vfzg_w | - | unsigned integer | - | 0,0078125 | 1 | 0,0 |
| STAT_0x5AB3_WERT | 0x4AB3 | STAT_FAHRSTRECKE_MIL_AN_WERT | Zähler für gefahrene Kilometer mit MIL EIN | km | DSMDur_ctPID21h | - | unsigned long | - | 0,009999999776482582 | 1 | 0,0 |
| IZBST | 0x4AB4 | STAT_BETRIEBSSTUNDENZAEHLER_WERT | sekundengenauer Betribsstundenzähler als 32 Bitwert | s | top_l | - | unsigned long | - | 0,10000000149011612 | 1 | 0,0 |
| IUSAU | 0x4AB8 | STAT_SAUGROHRDRUCK_SPANNUNG_WERT | Spannung Drucksensor Saugrohrdruck (word) | V | udss_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IMLUF | 0x4ABC | STAT_LUFTMASSE_WERT | Luftmassenfluss gefiltert (Word) | kg/h | ml_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| IASRE | 0x4ABD | STAT_STARTRELAIS_AKTIV_WERT | Bedingung automatischer Start | 0/1 | B_sta | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4ABE_WERT | 0x4ABE | STAT_0x4ABE_WERT | I-Regler Mengenregelung Kraftstoffsystem | mg | FUEL_MASS_REQ_I_CTL_H_RES | - | signed integer | - | 0,0211944580078125 | 1 | 0,0 |
| STAT_0x4ABF_WERT | 0x4ABF | STAT_0x4ABF_WERT | Verbrauch ohne Regler | l/h | VFF_MFF_SP_FUP_CTL | - | unsigned integer | - | 0,0038910505827516317 | 1 | 0,0 |
| STAT_0x4AC0_WERT | 0x4AC0 | STAT_0x4AC0_WERT | Verbrauch mit Regler | l/h | VFF_VCV | - | unsigned integer | - | 0,0038910505827516317 | 1 | 0,0 |
| STAT_0x4AC2_WERT | 0x4AC2 | STAT_0x4AC2_WERT | Reset Information  | - | Reset_Env.adLoc | - | unsigned long | - | 1,0 | 1 | 0,0 |
| STAT_0x4AC4_WERT | 0x4AC4 | STAT_0x4AC4_WERT | Raildruck Kraftstoffsystem Sollwert | MPa | prsoll_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| STAT_0x4AC6_WERT | 0x4AC6 | STAT_0x4AC6_WERT | Modus Kraftstoffsystem (Druck-, Mengen-, oder Maximumregelung) | 0-n | STATE_PWM_VCV | - | unsigned char | ba_vcv_state_text | 1 | 1 | 0 |
| STAT_0x4ACC_WERT | 0x4ACC | STAT_0x4ACC_WERT | Luftklappe - Sollposition in Schritten | - | RadSht_StpEng | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x4ACD_WERT | 0x4ACD | STAT_0x4ACD_WERT | Luftklappe - Istposition in Schritten | - | ShtrEcu_StpEngPos | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x4AD0_WERT | 0x4AD0 | STAT_0x4AD0_WERT | Luftklappe - Diagnosestatus allgemein | - | RadSht_stDiagGen | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x4AD1_WERT | 0x4AD1 | STAT_0x4AD1_WERT | Luftklappe - Diagnosestatus obere Luftklappe | - | RadSht_stDiagAKKS | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x4AD2_WERT | 0x4AD2 | STAT_0x4AD2_WERT | Luftklappe - Status obere Luftklappe | - | RadSht_stDiagAbvAirVlv | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x4AD3_WERT | 0x4AD3 | STAT_0x4AD3_WERT | Luftklappe - Status untere Luftklappe | - | RadSht_stDiagBntAirVlv | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x4AD4_WERT | 0x4AD4 | STAT_0x4AD4_WERT | Luftklappe - Varianteninfo vom Steller | - | ShtrEcu_stVrs | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x4AD5_WERT | 0x4AD5 | STAT_0x4AD5_WERT | Kraftstofftemperatur | Grad C | tkrst | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x4AD6_WERT | 0x4AD6 | STAT_0x4AD6_WERT | Bedingung Schubabschalten | 0/1 | B_sa | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x4AE2_WERT | 0x4AE2 | STAT_0x4AE2_WERT | Reset Information - Reset-group-ID of the last reset reason | 0-n | Reset_Env.xGrp | - | unsigned char | Reset_GrpID | 1 | 1 | 0 |
| STAT_0x4AE3_WERT | 0x4AE3 | STAT_0x4AE3_WERT | Reset Information - Reset-ID of the last reset | 0-n | Reset_Env.xId | - | unsigned integer | Reset_ID | 1 | 1 | 0 |
| STAT_0x4AE4_WERT | 0x4AE4 | STAT_0x4AE4_WERT | Reset Information - User defined value of the last reset reason | - | Reset_Env.xUserValue | - | unsigned long | - | 1,0 | 1 | 0,0 |
| STAT_0x4AEB_WERT | 0x4AEB | STAT_0x4AEB_WERT | Kühlmitteltemperatur &lt; 98°C | % | tmotb1_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x4AEC_WERT | 0x4AEC | STAT_0x4AEC_WERT | 98°C =&lt; Kühlmitteltemperatur =&lt; 112°C | % | tmotb2_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x4AED_WERT | 0x4AED | STAT_0x4AED_WERT | 113°C =&lt; Kühlmitteltemperatur =&lt; 120°C | % | tmotb3_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x4AEE_WERT | 0x4AEE | STAT_0x4AEE_WERT | 121°C =&lt; Kühlmitteltemperatur =&lt; 125°C | % | tmotb4_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x4AEF_WERT | 0x4AEF | STAT_0x4AEF_WERT | Kühlmitteltemperatur &gt; 125°C | % | tmotb5_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x4AF0_WERT | 0x4AF0 | STAT_0x4AF0_WERT | Motoröltemperatur &lt; 80°C | % | toelb1_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5800_WERT | 0x5800 | STAT_0x5800_WERT | Zeitzähler ab Startende (16bit) | s | tnse_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x5801_WERT | 0x5801 | STAT_0x5801_WERT | Umgebungsdruck | hPa | pu | - | unsigned char | - | 5,0 | 1 | 0,0 |
| ICLR1 | 0x5802 | STAT_LAMBDAREGELUNG_ZUSTAND_BANK1_WERT | CARB FREEZE FRAME Byte, Bank 1, für LR | - | flglrs | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5803_WERT | 0x5803 | STAT_0x5803_WERT | CARB FREEZE FRAME Byte, Bank 2, für LR | - | flglrs2 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ILMAR | 0x5804 | STAT_LUFTMASSE_RELATIV_WERT | relative Luftmasse (calc. load value) nach SAE J1979 | % | rml | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| ITMOT | 0x5805 | STAT_MOTORTEMPERATUR_LINEAR_WERT | Motortemperatur, linearisiert und umgerechnet | Grad C | tmotlin | - | unsigned char | - | 0,75 | 1 | -48,0 |
| IINT1 | 0x5806 | STAT_INTEGRATOR_BANK1_WERT | Lambda-Regler-Ausgang (Word) | - | fr_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| ILAM1 | 0x5807 | STAT_LAMBDA_ADAPTION_MULTIPLIKATIV_GRUPPE1_WERT | Faktor aus Lambdaregelungsadaption für Bank 1 | - | frann_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| ILAM2 | 0x5809 | STAT_LAMBDA_ADAPTION_MULTIPLIKATIV_GRUPPE2_WERT | Faktor aus Lambdaregelungsadaption, Bank 2 | - | frann2_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| IPSAU | 0x580B | STAT_SAUGROHRDRUCK_WERT | Saugrohr-Absolutdruck | hPa | ps_w | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| INAUF | 0x580C | STAT_N_AUFLOESUNG_WERT | Motordrehzahl | 1/min | nmot | - | unsigned char | - | 40,0 | 1 | 0,0 |
| IVKM2 | 0x580D | STAT_GESCHWINDIGKEIT_2_WERT | Fahrzeuggeschwindigkeit | km/h | vfzg | - | unsigned char | - | 1,25 | 1 | 0,0 |
| IZZY1 | 0x580E | STAT_ZUENDZEITPUNKT_ZYL1_WERT | Zündwinkel Zylinder 1 | Grad KW | zwzyl1 | - | signed char | - | 0,75 | 1 | 0,0 |
| ITANS | 0x580F | STAT_ANSAUGLUFTTEMPERATUR_WERT | Ansaugluft-Temperatur | Grad C | tans | - | unsigned char | - | 0,75 | 1 | -48,0 |
| ILMKG | 0x5812 | STAT_LUFTMASSE_WERT | Massenstrom HFM | kg/h | mshfm_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| ILREL | 0x5813 | STAT_LASTWERT_RELATIV_WERT | relative Luftfüllung | % | rl | - | unsigned char | - | 0,75 | 1 | 0,0 |
| STAT_0x5814_WERT | 0x5814 | STAT_0x5814_WERT | Normierter Fahrpedalwinkel | %PED | wped | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| IUK87 | 0x5815 | STAT_KL87_SPANNUNG_WERT | Batteriespannung | V | ub | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 |
| STAT_0x5816_WERT | 0x5816 | STAT_0x5816_WERT | Lambda-Sollwert bezogen auf Einbauort Lambda-Sensor | - | lamsons_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| ITUMG | 0x5817 | STAT_UMGEBUNGSTEMPERATUR_WERT | Umgebungstemperatur | Grad C | tumg | - | unsigned char | - | 0,75 | 1 | -48,0 |
| ILMMG | 0x5818 | STAT_LUFTMASSE_PRO_HUB_WERT | Luftmassenfluß | kg/h | ml | - | unsigned char | - | 4,0 | 1 | 0,0 |
| STAT_0x5819_WERT | 0x5819 | STAT_0x5819_WERT | Motordrehzahl [1/min] | rpm | Epm_nEng | - | signed integer | - | 0,5 | 1 | 0,0 |
| ISNWE | 0x581A | STAT_NW_EINLASSSPREIZUNG_WERT | Winkel Einlassventil oeffnet bezogen auf LWOT | Grad KW | wnwe_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| STAT_0x581B_WERT | 0x581B | STAT_0x581B_WERT | Sollwinkel Nockenwelle Einlass öffnet | Grad KW | wnwse_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| ISNWA | 0x581C | STAT_NW_AUSLASSSPREIZUNG_WERT | Winkel Auslassventil schließt bezogen auf LWOT | Grad KW | wnwa_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| STAT_0x581D_WERT | 0x581D | STAT_0x581D_WERT | Sollwinkel Nockenwelle Auslass schließt | Grad KW | wnwsa_w | - | signed integer | - | 0,0078125 | 1 | 0,0 |
| RTANS | 0x581E | STAT_ANSAUGLUFTTEMPERATUR1_ROH_WERT | Ansauglufttemperatur, linearisiert und umgerechnet | Grad C | tanslin | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x5820_WERT | 0x5820 | STAT_0x5820_WERT | Bedingung Klemme 15 | 0/1 | B_kl15 | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x5821_WERT | 0x5821 | STAT_0x5821_WERT | Steuergerätetemperatur | Grad C | tsg | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x5822_WERT | 0x5822 | STAT_0x5822_WERT | Öltemperatur | Grad C | toel | - | unsigned char | - | 1,0 | 1 | -60,0 |
| IZMOS | 0x5823 | STAT_ZEIT_MOTOR_STEHT_WERT | Abstellzeit | s | tabst_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5825_WERT | 0x5825 | STAT_0x5825_WERT | Spannung von BCU gemessen (U_BCU_LIN) | V | BcuEcu_u | - | signed integer | - | 0,009999999776482582 | 1 | 0,0 |
| IDKS1 | 0x5826 | STAT_DROSSELKLAPPE_SENSOR1_WERT | Drosselklappenwinkel aus Poti 1 | %DK | wdk1 | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| IAHV1 | 0x5827 | STAT_SONDENHEIZUNG_PWM_VORKAT_BANK1_WERT | Tastverhältnis für Lambdasondenheizung | % | tahrlsu_w | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 |
| IAHV2 | 0x5828 | STAT_SONDENHEIZUNG_PWM_VORKAT_BANK2_WERT | Tastverhältnis für Lambdasondenheizung, Bank 2 | % | tahrlsu2_w | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 |
| IAHN1 | 0x5829 | STAT_SONDENHEIZUNG_PWM_NACHKAT_BANK1_WERT | normierte Heizleistung der Lambdasonde hinter Kat | - | phlsnh | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 |
| IDRCA | 0x582B | STAT_DREHMOMENTEINGRIFF_CAN_WERT | Drehmomentaufnahme des Wandlers über CAN | % | mdwancan_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x582C_WERT | 0x582C | STAT_0x582C_WERT | Lambdasonden-Istwert | - | lamzak_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| STAT_0x582D_WERT | 0x582D | STAT_0x582D_WERT | Korrekturwert der LSU-Spannung vor KAT | V | kusvk_w | - | signed integer | - | 4,8828125E-4 | 1 | 0,0 |
| STAT_0x582F_WERT | 0x582F | STAT_0x582F_WERT | Abgastemperatur nach KAT aus Modell | Grad C | tkatm | - | unsigned char | - | 5,0 | 1 | -50,0 |
| STAT_0x5830_WERT | 0x5830 | STAT_0x5830_WERT | Dynamikwert der LSU | - | dynlsu_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| STAT_0x5831_WERT | 0x5831 | STAT_0x5831_WERT | Dynamikwert der LSU, Bank 2 | - | dynlsu2_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| IMOST | 0x5832 | STAT_MOTOR_STATUS_WERT | Zustand Motor-Koordinator | - | CoEng_st | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5834_WERT | 0x5834 | STAT_0x5834_WERT | Umgebungsdruck von Sensor | hPa | pur_w | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| VGENH | 0x5835 | STAT_GENERATOR_HERSTELLERCODE_WERT | Kennung Generator Hersteller | - | genmanufak | - | unsigned char | - | 1,0 | 1 | 0,0 |
| INGRD | 0x5836 | STAT_DREHZAHLGRADIENT_WERT | gefilterter Drehzahlgradient | 1/min/s | ngfil | - | signed char | - | 100,0 | 1 | 0,0 |
| STAT_0x5837_WERT | 0x5837 | STAT_0x5837_WERT | Solldruck Hochdrucksystem | MPa | prsoll_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| STAT_0x5838_WERT | 0x5838 | STAT_0x5838_WERT | Relatives Moment für Aussetzererkennung | % | midmd | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| ISDKN | 0x5839 | STAT_DROSSELKLAPPE_NOTLAUF_WERT | Bedingung Sicherheitskraftstoffabschaltung (SKA) | 0/1 | B_dkpu | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x583A_WERT | 0x583A | STAT_0x583A_WERT | Ansaugluft-Temperatur bei Start | Grad C | tansst | - | unsigned char | - | 0,75 | 1 | -48,0 |
| IKTFS | 0x583B | STAT_KRAFTSTOFFTANK_FUELLSTAND_WERT | Fuellstand Kraftstofftank | L | fstt | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x583C_WERT | 0x583C | STAT_0x583C_WERT | Batteriespannung; vom AD-Wandler erfasster Wert | V | wub | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 |
| STAT_0x583D_WERT | 0x583D | STAT_0x583D_WERT | Betriebsstundenzähler | min | top_w | - | unsigned integer | - | 6,0 | 1 | 0,0 |
| STAT_0x583E_WERT | 0x583E | STAT_0x583E_WERT | Sollwert Drosselklappenwinkel, bez. auf unteren Anschlag | %DK | wdknlpr_w | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| STAT_0x583F_WERT | 0x583F | STAT_0x583F_WERT | Sollwert DK-Winkel, bezogen auf unteren Anschlag | %DK | wdks | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| STAT_0x5840_WERT | 0x5840 | STAT_0x5840_WERT | DK-Winkel der Notluftposition | %DK | wdknlp_w | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 |
| IUSGI | 0x5841 | STAT_STEUERGERAETE_INNENTEMPERATUR_SPANNUNG_WERT | Wert Temperatur Steuergerät | V | wtsg | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| VGTYP | 0x5842 | STAT_GENERATOR_TYP_WERT | Kennung Generatortyp | - | gentypkenn | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5843_WERT | 0x5843 | STAT_0x5843_WERT | Bedingung Startanforderung | 0/1 | B_staanf | - | unsigned char | - | 1 | 1 | 0 |
| ITGEE | 0x5844 | STAT_GENERATOR_ELEKTRONIKTEMPERATUR | Chiptemperatur Generator 1 | Grad C | tchip | - | unsigned char | - | 1,0 | 1 | -40,0 |
| IUSV1 | 0x5845 | STAT_SONDENSPANNUNG_VORKAT_WERT | Sondenspannung vor Kat einer Breitbandlambdasonde (ADC-Wert) | V | uulsuv_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUPW1 | 0x5846 | STAT_PWG1_SPANNUNG_WERT | Spannung PWG-Poti 1 (Word) | V | upwg1_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUPW2 | 0x5847 | STAT_PWG2_SPANNUNG_WERT | Spannung PWG-Poti 2 (Word) | V | upwg2_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUSN1 | 0x5849 | STAT_SONDENSPANNUNG_NACHKAT_WERT | ADC-Spannung Lambdasonde hinter Katalysator (Word) | V | ushk_w | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 |
| IUSN2 | 0x584B | STAT_SONDENSPANNUNG_NACHKAT_BANK2_WERT | ADC-Spannung Lambdasonde hinter Katalysator Bank2 (Word) | V | ushk2_w | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 |
| IUDK2 | 0x584C | STAT_DK2_SPANNUNG_WERT | Spannung DK-Poti 2 | V | udkp2_w | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| SQTEK | 0x584D | STAT_TANKENTLUEFTUNG_DURCHFLUSS_SOLL_WERT | Massenstrom Tankentlüftung in das Saugrohr | kg/h | mste_w | - | unsigned integer | - | 3,906250058207661E-4 | 1 | 0,0 |
| IUDK1 | 0x584E | STAT_DK1_SPANNUNG_WERT | Spannung DK-Poti 1 | V | udkp1_w | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| STAT_0x584F_WERT | 0x584F | STAT_0x584F_WERT | Erkennung Bordnetzinstabilität | - | statbnserr | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IUKUM | 0x5850 | STAT_KUEHLMITTELTEMPERATUR_SPANNUNG_WERT | Signalspannung des Kühlmitteltemperatursensor | V | utcw_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IULMM | 0x5851 | STAT_LUFTMASSE_WERT | Spannungswert des Ansauglufttemperatursensors tfa2 (SY_TFAKON &gt; 0) | V | wtfa2_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x5852_WERT | 0x5852 | STAT_0x5852_WERT | Batteriestrom vom IBS | A | iibsl_w | - | unsigned integer | - | 0,019999999552965164 | 1 | -200,0 |
| STAT_0x5853_WERT | 0x5853 | STAT_0x5853_WERT | Batteriespannung von IBS | V | uibsl_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| STAT_0x5854_WERT | 0x5854 | STAT_0x5854_WERT | Batterietemperatur vom IBS | Grad C | tibsl | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x5855_WERT | 0x5855 | STAT_0x5855_WERT | schneller Mittelwert des Lambdaregelfaktors (Word) | - | frm_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| STAT_0x5856_WERT | 0x5856 | STAT_0x5856_WERT | schneller Mittelwert des Lambdaregelfaktors Bank 2(Word) | - | frm2_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| IIEGE | 0x5857 | STAT_0x5857_WERT | Erregerstrom Generator 1 | A | ierr | - | unsigned char | - | 0,125 | 1 | 0,0 |
| STAT_0x5858_WERT | 0x5858 | STAT_0x5858_WERT | Drosselklappenwinkel bezogen auf unteren Anschlag | %DK | wdkba | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 |
| STAT_0x5859_WERT | 0x5859 | STAT_0x5859_WERT | Pumpenstrom Referenzleck | mA | iptrefr_w | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| STAT_0x585A_WERT | 0x585A | STAT_0x585A_WERT | min. Pumpenstrom bei Grobleckmessung | mA | iptglmn_w | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| STAT_0x585B_WERT | 0x585B | STAT_0x585B_WERT | Pumpenstrom am Ende der Feinstleckmessung | mA | iptkl_w | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| IRLN1 | 0x585C | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT1_OBERES_BYTE_WERT | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT | Ohm | rinh_w | - | unsigned char | - | 512,0 | 1 | 0,0 |
| IRLN2 | 0x585D | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT2_OBERES_BYTE_WERT | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT Bank2 | Ohm | rinh2_w | - | unsigned char | - | 512,0 | 1 | 0,0 |
| IRUN1 | 0x585E | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT1_UNTERES_BYTE_WERT | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT | Ohm | rinh_w | - | unsigned char | - | 2,0 | 1 | 0,0 |
| IRUN2 | 0x585F | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT2_UNTERES_BYTE_WERT | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT Bank2 | Ohm | rinh2_w | - | unsigned char | - | 2,0 | 1 | 0,0 |
| IRLV1 | 0x5860 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT1_WERT | Innenwiderstand der Nernstzelle der LSU | Ohm | rinlsu_w | - | unsigned char | - | 10,0 | 1 | 0,0 |
| IRLV2 | 0x5861 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT2_WERT | Innenwiderstand der Nernstzelle der LSU, Bank 2 | Ohm | rinlsu2_w | - | unsigned char | - | 10,0 | 1 | 0,0 |
| STAT_0x5862_WERT | 0x5862 | STAT_0x5862_WERT | Sollwert Öldruck | kPa | poels_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| IRUV1 | 0x5863 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT1_UNTERES_BYTE_WERT | Innenwiderstand der Nernstzelle der LSU | Ohm | rinlsu_w | - | unsigned char | - | 0,0390625 | 1 | 0,0 |
| IRUV2 | 0x5864 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT2_UNTERES_BYTE_WERT | Innenwiderstand der Nernstzelle der LSU, Bank 2 | Ohm | rinlsu2_w | - | unsigned char | - | 0,0390625 | 1 | 0,0 |
| IMLOE | 0x5865 | STAT_OELSTAND_LANGZEIT_MITTEL_WERT | Langzeit-Ölniveau-Mittelwert für den DIS-Tester | - | oznivlangt | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| IFSOE | 0x5866 | STAT_FUELLSTAND_MOTOROEL_WERT | Relativer Füllstand des Motoröls | - | oelstandr | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x5867_WERT | 0x5867 | STAT_0x5867_WERT | Fahrstrecke des Fahrzeugs als Information über CAN | km | kmstand | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| ISSR1 | 0x5868 | STAT_STANDVERBRAUCHER_REGISTRIERT_TEIL1_WERT | Status Standverbraucher registriert Teil 1 | - | statsvreg1 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ISSR2 | 0x5869 | STAT_STANDVERBRAUCHER_REGISTRIERT_TEIL2_WERT | Status Standverbraucher registriert Teil 2 | - | statsvreg2 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IUIBS | 0x586A | STAT_UBATT_IBS_WERT | aktuelle Batteriespannung | V | ubatt_w | - | unsigned integer | - | 2,500000118743628E-4 | 1 | 6,0 |
| IZR82 | 0x586B | STAT_ZEIT_MIT_RUHESTROM_80_200_WERT | Zeit, indem der Ruhestrom bei 80..200mA liegt | min | t2hstshort | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| IZR21 | 0x586C | STAT_ZEIT_MIT_RUHESTROM_200_1000_WERT | Zeit, indem der Ruhestrom bei 200..1000mA liegt | min | t3hstshort | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| IZRG1 | 0x586E | STAT_ZEIT_MIT_RUHESTROM_GROESER_1000_WERT | Zeit, indem der Ruhestrom größer als 1000mA liegt | min | t4hstshort | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 |
| STAT_0x586F_WERT | 0x586F | STAT_0x586F_WERT | Öldruck | hPa | poel_w | - | signed integer | - | 1,0 | 1 | 0,0 |
| IUUMG | 0x5870 | STAT_UMGEBUNGSDRUCK_SPANNUNG_WERT | Spannung Umgebungsdrucksensor (word 10-Bit von ADC) | V | udsu_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x5871_WERT | 0x5871 | STAT_0x5871_WERT | Zähler Prüfzustand für DVESTANZNMOT | - | dvestanznmotctr | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| VGENR | 0x5872 | STAT_GENERATOR_REGLERVERSION_WERT | Reglerversion on Generator 1 | - | bsdgenregv | - | unsigned char | - | 1,0 | 1 | 0,0 |
| SLAG2 | 0x5873 | STAT_LAMBDA_SOLLWERT_GRUPPE2_WERT | Lambda-Sollwert bezogen auf Einbauort Lambda-Sensor Bank2 | - | lamsons2_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| STAT_0x5874_WERT | 0x5874 | STAT_0x5874_WERT | ADC-Spannung Pumpenstrom Tankdiagnose | V | urptes_w | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 |
| STAT_0x5875_WERT | 0x5875 | STAT_0x5875_WERT | Soll-Motormoment MSR für schnellen Eingriff | Nm | mdradmsrs_w | - | signed integer | - | 1,0 | 1 | 0,0 |
| STAT_0x5876_WERT | 0x5876 | STAT_0x5876_WERT | Schnittstelle für Scan Tool Mode $01/$02 Raildruck Rohwert | MPa | prrohr_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| ILRR1 | 0x5878 | STAT_LAMBDAVERSCHIEBUNG_RUECKFUEHRREGLER1_WERT | I-Anteil der stetigen LRSHK Variante kontinuierlich | - | dlahi_w | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| STAT_0x587C_WERT | 0x587C | STAT_0x587C_WERT | Periodendauer des Nullgangsensorsignals | ms | GbxNPos_tiPwmPer | - | unsigned integer | - | 9,999999747378752E-5 | 1 | 0,0 |
| STAT_0x587D_WERT | 0x587D | STAT_0x587D_WERT | Status Nullgangsensor | - | stngang | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IELTV | 0x587F | STAT_E_LUEFTER_TASTVERHAELTNIS_WERT | Tastverhältnis E-Lüfter | % | taml | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| SBEGA | 0x5881 | STAT_BERECHNETER_GANG_WERT | Ist-Gang | - | gangi | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ITMOS | 0x5882 | STAT_MOTORTEMPERATUR_BEIM_START_WERT | Motorstarttemperatur | Grad C | tmst | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x5883_WERT | 0x5883 | STAT_0x5883_WERT | Referenzpegel Klopfregelung, 16 bit | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| STAT_0x5884_WERT | 0x5884 | STAT_0x5884_WERT | Kopie begrenzter Erregerstrom Generator 1 | A | ierrfgrenz | - | unsigned char | - | 0,125 | 1 | 0,0 |
| STAT_0x5885_WERT | 0x5885 | STAT_0x5885_WERT | Referenzpegel Klopfregelung, 16bit | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| STAT_0x5886_WERT | 0x5886 | STAT_0x5886_WERT | Referenzpegel Klopfregelung, 16bit | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IGENA | 0x5887 | STAT_0x5887_WERT | Auslastungsgrad Generator 1 | % | dfsiggen | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STAT_0x5888_WERT | 0x5888 | STAT_0x5888_WERT | Referenzpegel Klopfregelung, 16bit | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| ILAG1 | 0x5889 | STAT_LAMBDA_ISTWERT_GRUPPE1_WERT | Lambda-Istwert | - | lamsoni_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| ILAG2 | 0x588A | STAT_LAMBDA_ISTWERT_GRUPPE2_WERT | Lambda-Istwert Bank2 | - | lamsoni2_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 |
| IZSSE | 0x588B | STAT_ZEIT_SEIT_STARTENDE_WERT | Zeit nach Startende | s | tnst_w | - | unsigned integer | - | 0,009999999776482582 | 1 | 0,0 |
| ITKV1 | 0x588C | STAT_LAMBDASONDE_KERAMIKTEMPERATUR_VORKAT1_WERT | Keramiktemperatur der LSU | Grad C | tkerlsu_w | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 |
| IZDML | 0x588D | STAT_ZEIT_DMTL_LECKMESSUNG_WERT | aktuelle Zeit Leckmessung | s | tdmlka_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| IIDMP | 0x588E | STAT_PUMPENSTROM_BEI_DMTL_PUMPENPRUEFUNG_WERT | Pumpenstrom Tankdiagnose | mA | iptes_w | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| ITKV2 | 0x588F | STAT_LAMBDASONDE_KERAMIKTEMPERATUR_VORKAT2_WERT | Keramiktemperatur der LSU, Bank 2 | Grad C | tkerlsu2_w | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 |
| IMOKU | 0x5891 | STAT_MOMENTANFORDERUNG_KUPPLUNG_WERT | Kupplungsmotormoment Istwert | Nm | mkist_w | - | signed integer | - | 0,5 | 1 | 0,0 |
| STAT_0x5892_WERT | 0x5892 | STAT_0x5892_WERT | Differenz zwischen Umgebungsdruck und  Bremskraftverstärker-Druck von Drucksensor (Rohwert) | hPa | dpbkvur_w | - | signed integer | - | 0,0390625 | 1 | 0,0 |
| IDMGW | 0x5893 | STAT_DREHMOMENTABFALL_BEIM_GANGWECHSEL_WERT | Indiziertes Soll-Motormoment GS für schnellen Eingriff | % | migs_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x5894_WERT | 0x5894 | STAT_0x5894_WERT | Spannung Klopfwerte Zylinder 2 | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| STAT_0x5895_WERT | 0x5895 | STAT_0x5895_WERT | Spannung Klopfwerte Zylinder 5 | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| STAT_0x5896_WERT | 0x5896 | STAT_0x5896_WERT | Abgastemperatur hinter Hauptkat aus Modell | Grad C | tanhkm_w | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 |
| SUGEN | 0x5898 | STAT_GENERATOR_SPANNUNG_SOLL_WERT | phys. Wert Generatorsollspannung (Volt) für Komponententreiber Generator | V | ugen | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 |
| STAT_0x5899_WERT | 0x5899 | STAT_0x5899_WERT | Bedingung Anforderung Motorrelais einschalten | 0/1 | B_amtr | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x589A_WERT | 0x589A | STAT_0x589A_WERT | Tastverhältnis Nullgangsensor | % | tngang_w | - | unsigned integer | - | 0,009999999776482582 | 1 | 0,0 |
| STAT_0x589B_WERT | 0x589B | STAT_0x589B_WERT | Bedingung unzulössig hoher Motorstrom bei Kurzschluss erkannt | 0/1 | B_ivvtkse | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x589C_WERT | 0x589C | STAT_0x589C_WERT | Bedingung Freigabe VVT-Endstufe | 0/1 | B_vvten | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x589E_WERT | 0x589E | STAT_0x589E_WERT | Sollwert Exzenterwinkel VVT | Grad | exwinks_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x589F_WERT | 0x589F | STAT_0x589F_WERT | Batterietemperatur | Grad C | tbatt | - | unsigned char | - | 0,75 | 1 | -48,0 |
| STAT_0x58A0_WERT | 0x58A0 | STAT_0x58A0_WERT | Entladung während Ruhestromverletzung | Ah | qiruhe2_w | - | unsigned integer | - | 0,018204445019364357 | 1 | 0,0 |
| ISKME | 0x58A1 | STAT_KILOMETERSTAND_WERT | Wegstrecke_km auf 1km genau | - | kmstand_l | - | unsigned long | - | 1,0 | 1 | 0,0 |
| STAT_0x58A2_WERT | 0x58A2 | STAT_0x58A2_WERT | Istwert Exzenterwinkel VVT | Grad | exwnki_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58A3_WERT | 0x58A3 | STAT_0x58A3_WERT | rel. Exzenterwinkel am oberen mech. Anschlag | Grad | exwnkoar_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58A4_WERT | 0x58A4 | STAT_0x58A4_WERT | Generatorstatus | - | st_gen | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58A5_WERT | 0x58A5 | STAT_0x58A5_WERT | Vom Generator empfangenes Lastsignal | % | dffgen | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STAT_0x58A6_WERT | 0x58A6 | STAT_0x58A6_WERT | Rel. Exzenterwinkel | Grad | exwnkr_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58A7_WERT | 0x58A7 | STAT_0x58A7_WERT | Abstellzeit aus relativem Minutenzähler bis Motorstart | min | tabsmn_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| IZMAB | 0x58A8 | STAT_MOTORABSTELLZEIT_WERT | Rel. Exzenterwinkel am unteren mech. Anschlag | Grad | exwnkuar_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58A9_WERT | 0x58A9 | STAT_0x58A9_WERT | VVT Verstellbereich aus Urlernvorgang | Grad | exwnkvb_ur_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58AA_WERT | 0x58AA | STAT_0x58AA_WERT | Verstellbereich des Exzenterwinkels | Grad | exwnkvb_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58AB_WERT | 0x58AB | STAT_0x58AB_WERT | DLR für DV-E: Summe der PID-Anteile | % | dlrspid_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IPWG1 | 0x58AD | STAT_PEDALWERTGEBER1_WERT | Sauerstoffspeichervermögen KAT | mg | oscdktt_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58AE_WERT | 0x58AE | STAT_0x58AE_WERT | Peridendauer für Massenstrom aus HFM | us | tpmshfm_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| IKRAN | 0x58AF | STAT_KRAFTSTOFF_ANFORDERUNG_AN_PUMPE_WERT | EKP-Sollvolumenstrom | l | vssekp | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IDKAD | 0x58B0 | STAT_DK_ADAPTIONSSCHRITT_WERT | Zähler für Lerndauer eines Lernsteps | - | lrnstep_c | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IZFZ1 | 0x58B1 | STAT_FUNKENBRENNDAUER_ZYL1_WERT | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 1 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| IZFZ5 | 0x58B2 | STAT_FUNKENBRENNDAUER_ZYL5_WERT | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 5 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| IZFZ3 | 0x58B3 | STAT_FUNKENBRENNDAUER_ZYL3_WERT | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 3 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| IZFZ6 | 0x58B4 | STAT_FUNKENBRENNDAUER_ZYL6_WERT | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 6 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| IZFZ2 | 0x58B5 | STAT_FUNKENBRENNDAUER_ZYL2_WERT | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 2 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| IZFZ4 | 0x58B6 | STAT_FUNKENBRENNDAUER_ZYL4_WERT | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 4 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 |
| IPBRE | 0x58B7 | STAT_BREMSDRUCK_WERT | aktueller Bremsdruck | hPa | pbrems | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58B8_WERT | 0x58B8 | STAT_0x58B8_WERT | Motordrehzahl in der Funktionsüberwachung | 1/min | MoF_nEng | - | unsigned char | - | 40,0 | 1 | 0,0 |
| STAT_0x58B9_WERT | 0x58B9 | STAT_0x58B9_WERT | Pedalsollwert (8 Bit) in der Funktionsüberwachung | V | MoF_uAPP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| STAT_0x58BA_WERT | 0x58BA | STAT_0x58BA_WERT | Bank mittel eingespritzte effektive relative Krafftstoffmasse (inkl. Reduzierstufe) | % | rkmeeff_w | - | unsigned integer | - | 0,046875 | 1 | 0,0 |
| STAT_0x58BB_WERT | 0x58BB | STAT_0x58BB_WERT | Strom für VVT-Motor | A | ivvtm_w | - | signed integer | - | 0,006103515625 | 1 | 0,0 |
| STAT_0x58BC_WERT | 0x58BC | STAT_0x58BC_WERT | relative Luftfüllung in der Funktionsüberwachung | % | rl_um | - | unsigned char | - | 0,75 | 1 | 0,0 |
| STAT_0x58BD_WERT | 0x58BD | STAT_0x58BD_WERT | Status Fehler Überlast VVT1 | - | stdvovrld | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58BE_WERT | 0x58BE | STAT_0x58BE_WERT | DV-E-Adaption: Status Prüfbedingungen | - | dveadchst | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58C0_WERT | 0x58C0 | STAT_0x58C0_WERT | VVT-Endstufentemperatur aus Modell | Grad C | tvvtes_w | - | unsigned integer | - | 0,75 | 1 | -48,0 |
| ITLSZ | 0x58C1 | STAT_LAUFUNRUHE_SEGMENTZEIT_WERT | Korrigierte Segmentdauer | us | tsk_l | - | unsigned long | - | 0,05000000074505806 | 1 | 0,0 |
| STAT_0x58C2_WERT | 0x58C2 | STAT_0x58C2_WERT | Status STG Anforderung Radmoment Antriebsstrang Summe FAS | - | Com_stTrqWhlDemFASQl_FX | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58C3_WERT | 0x58C3 | STAT_0x58C3_WERT | Status STG Anforderung Drehmoment Kurbelwelle Fahrdynamik | - | Com_stDrvDyn_FX | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58C4_WERT | 0x58C4 | STAT_0x58C4_WERT | Status STG Anforderung Radmoment Antriebsstrang Summe Stabilisierung | - | Com_stEcuRqTrqSumStab_FX | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58C5_WERT | 0x58C5 | STAT_0x58C5_WERT | Status STG ist Bremsmoment Summe | - | Com_stEcuBrkTrqSum_FX | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58C6_WERT | 0x58C6 | STAT_0x58C6_WERT | Status STG ist Lenkwinkel Vorderachse | - | Com_stEcuAvlSteaFtax_FX | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58C7_WERT | 0x58C7 | STAT_0x58C7_WERT | Status STG Status Stabilisierung DSC | - | Com_stECUStStabDSC_FX | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58C8_WERT | 0x58C8 | STAT_0x58C8_WERT | geforderte Drehmomentänderung von der LLR (I-Anteil) | % | dmllri_w | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| STAT_0x58C9_WERT | 0x58C9 | STAT_0x58C9_WERT | vvtmode | - | vvtmode | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58CA_WERT | 0x58CA | STAT_0x58CA_WERT | geforderte MD-Änderung von der LLR (PD-Zündungsanteil) | % | dmllrz_w | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| STAT_0x58CB_WERT | 0x58CB | STAT_0x58CB_WERT | PD-Anteil schnell Leerlaufregelung | - | dvvttempovl | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x58CC_WERT | 0x58CC | STAT_0x58CC_WERT | Verlustmoment Überwachung | % | tvvvtm_w | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| STAT_0x58CD_WERT | 0x58CD | STAT_0x58CD_WERT | Verlustmomentabweichung Überwachung | V | umtr | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58CE_WERT | 0x58CE | STAT_0x58CE_WERT | Carrierbyte Schalterstati | - | funst_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| SMOMO | 0x58CF | STAT_MOTORMOMENT_SOLL_WERT | Soll- Motormoment aus Getriebeüberwachung in der Funktionsüberwachung | Nm | MoF_trqClthTra16 | - | signed integer | - | 0,0625 | 1 | 0,0 |
| IMOMO | 0x58D0 | STAT_MOTORMOMENT_IST_WERT | Berechnetes Ist-Moment in der Funktionsüberwachung | % | MoF_rTrqInrAct | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| STAT_0x58D0_WERT | 0x58D1 | STAT_0x58D0_WERT | Massenstrom Abgas ohne Kraftstoffanteil vor Hauptkatalysator | kg/h | msaovhk_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58D2_WERT | 0x58D2 | STAT_0x58D2_WERT | Luftklappe - Sollposition in Grad | - | RadSht_phiPosDes | - | unsigned char | - | 0,501960813999176 | 1 | 0,0 |
| STAT_0x58D3_WERT | 0x58D3 | STAT_0x58D3_WERT | Luftklappe - Istposition in Grad | - | RadSht_phiPos | - | unsigned char | - | 0,501960813999176 | 1 | 0,0 |
| STAT_0x58D4_WERT | 0x58D4 | STAT_0x58D4_WERT | Startbedingung Kraftschluss erfüllt | 0/1 | B_kupp1 | - | unsigned char | - | 1 | 1 | 0 |
| STAT_0x58D5_WERT | 0x58D5 | STAT_0x58D5_WERT | physikalischer Temperaturwert, der sich bei Wandlung der elektrischen Sensorspannung wtfa1_w ergibt | Grad C | tfa1lin | - | unsigned char | - | 0,75 | 1 | -48,0 |
| IUANS | 0x58D7 | STAT_ANSAUGLUFTTEMPERATUR_SPANNUNG_WERT | Spannungswert des Ansauglufttemperatursensors tfa1 | V | wtfa1_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x58D8_WERT | 0x58D8 | STAT_0x58D8_WERT | Differenz-DK-Winkel Sollwert - Istwert | %DK | dwdkdlr_w | - | signed integer | - | 0,0244140625 | 1 | 0,0 |
| STAT_0x58D9_WERT | 0x58D9 | STAT_0x58D9_WERT | Schrittzähler DK-Rückstellfeder-Prüfung | - | fprstep_c | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58DA_WERT | 0x58DA | STAT_0x58DA_WERT | koordiniertes Moment für Füllung | % | milsol_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x58DB_WERT | 0x58DB | STAT_0x58DB_WERT | Fehlerzähler abgasrelevante Aussetzer über alle Zylinder | - | fzabgs_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x58DC_WERT | 0x58DC | STAT_0x58DC_WERT | Intervallzähler für abgasrelevante Aussetzer | - | ivzabg_w | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| STAT_0x58DD_WERT | 0x58DD | STAT_0x58DD_WERT | Druck vor Drosselklappe Rohwert | hPa | pvdr_w | - | unsigned integer | - | 0,078125 | 1 | 0,0 |
| STAT_0x58DE_WERT | 0x58DE | STAT_0x58DE_WERT | Spannung Drucksensor vor Drosselklappe | V | udsvd_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x58E0_WERT | 0x58E0 | STAT_0x58E0_WERT | Abgleich DK-Modell (Faktor) | - | eisydkfkaf | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| STAT_0x58E1_WERT | 0x58E1 | STAT_0x58E1_WERT | Abgleich DK-Modell (Offset) | kg/h | eisydkkoff | - | signed char | - | 8,0 | 1 | 0,0 |
| STAT_0x58E2_WERT | 0x58E2 | STAT_0x58E2_WERT | Abgleich EV-Modell (Faktor) | - | eisyevfkaf | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| STAT_0x58E3_WERT | 0x58E3 | STAT_0x58E3_WERT | Abgleich EV-Modell (Offset) | kg/h | eisyevkoff | - | signed char | - | 8,0 | 1 | 0,0 |
| STAT_0x58E4_WERT | 0x58E4 | STAT_0x58E4_WERT | Ist-Betriebsart | - | opmodi | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IUWAP | 0x58E9 | STAT_WASSERPUMPE_SPANNUNG_WERT | empf. Spannung von BSS-Wasserpumpe | V | wmu | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 |
| INWAP | 0x58EA | STAT_WASSERPUMPE_DREHZAHL_WERT | empf. Istdrehzahl von BSS-Wasserpumpe | 1/min | wmpdzi | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ITWAE | 0x58EC | STAT_WASSERPUMPE_ELEKTRONIK_TEMPERATUR_WERT | empf. Temperatur von BSS-Wasserpumpe | Grad C | wmt | - | unsigned char | - | 1,0 | 1 | -50,0 |
| IIWAP | 0x58ED | STAT_WASSERPUMPE_STROM_WERT | empf. Strom von BSS-Wasserpumpe | % | wmi | - | unsigned char | - | 0,5 | 1 | 0,0 |
| STAT_0x58EF_WERT | 0x58EF | STAT_0x58EF_WERT | Gefilterter Raildruck-Istwert (Absolutdruck) | MPa | prist_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| STAT_0x58F0_WERT | 0x58F0 | STAT_0x58F0_WERT | ungefilterter Raildruck Istwert (abs.) | MPa | prroh_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 |
| STAT_0x58F2_WERT | 0x58F2 | STAT_0x58F2_WERT | Tastverhältnis Mengensteuerventil | % | PWM_VCV | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| STAT_0x58F3_WERT | 0x58F3 | STAT_0x58F3_WERT | Ungefilterter Niederdruck Rohwert | kPa | pistndr_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 |
| STAT_0x58F4_WERT | 0x58F4 | STAT_0x58F4_WERT | Spannung Kraftstoffniederdrucksensor im 1 ms Raster | V | upnd1ms_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| STAT_0x58F5_WERT | 0x58F5 | STAT_0x58F5_WERT | Spannung Diagnose-Port VVT-Ansteuerung (3V ADC) | V | uvvtdia3V | - | unsigned char | - | 0,012890624813735485 | 1 | 0,0 |
| STAT_0x58F6_WERT | 0x58F6 | STAT_0x58F6_WERT | Sollspannung des VVT Lagereglers | V | uvvtlrs_w | - | signed integer | - | 7,812500116415322E-4 | 1 | 0,0 |
| STAT_0x58F7_WERT | 0x58F7 | STAT_0x58F7_WERT | VVT-Strom | - | vvtipl | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58FA_WERT | 0x58FA | STAT_0x58FA_WERT | gefilterter Faktor Tankentlüftungs-Adaption | - | fteadf | - | signed char | - | 0,5 | 1 | 0,0 |
| STAT_0x58FC_WERT | 0x58FC | STAT_0x58FC_WERT | Fertigungs-Werkstatt-,Transportmodus | - | fetrawemod | - | unsigned char | - | 1,0 | 1 | 0,0 |
| STAT_0x58FD_WERT | 0x58FD | STAT_0x58FD_WERT | Untermodi des Fe Tra Fla Mode | - | fetraflamod | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x58FF | - | Umweltbedingung unbekannt | - | - | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-reset-grpid"></a>
### RESET_GRPID

Dimensions: 33 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | SWRESET_GRP_POWERON_E |
| 0x01 | SWRESET_GRP_HWRESET_E |
| 0x02 | SWRESET_GRP_WDT_E |
| 0x03 | SWRESET_GRP_WAKEUP_E |
| 0x04 | SWRESET_GRP_TRAP_E |
| 0x05 | SWRESET_GRP_SB_E |
| 0x06 | SWRESET_GRP_CB_E |
| 0x07 | SWRESET_SOFTRESETGRP_E |
| 0x08 | SWRESET_GRP_DUMMY_01 |
| 0x09 | SWRESET_GRP_DUMMY_02 |
| 0x0A | SWRESET_GRP_DUMMY_03 |
| 0x0B | RESET_EEP_GRP_E |
| 0x0C | RESET_SWRESET_EPM_E |
| 0x0D | RESET_SWRESET_ESC_E |
| 0x0E | RESET_EXECON_GRP_E |
| 0x0F | RESET_SWRESET_ASW_01 |
| 0x10 | SWRESET_GRP_MO_PREICO |
| 0x11 | RESET_SWRESET_MOC |
| 0x12 | RESET_SWRESET_SOP |
| 0x13 | RESET_SWRESET_MOFICO |
| 0x14 | SWRESET_OCWDA |
| 0x15 | RESET_SWRESET_OS_01 |
| 0x16 | SWRESET_PCP_GRP_E |
| 0x17 | RESET_HWEMONGRP_E |
| 0x18 | RESET_ERRINTRGRP_E |
| 0x19 | SWRESET_SYCGRP_E |
| 0x1A | RESET_SWRESET_TPROT |
| 0x1B | SWRESET_UNSUPPORTED_CPU_E |
| 0x1C | RESET_ADCI_E |
| 0x1D | SWRESET_R2S2_INI_GRP_E |
| 0x1E | RESET_DMA_E |
| 0x1F | RESET_FLASH_E |
| 0xFF | undefiniert |

<a id="table-reset-id"></a>
### RESET_ID

Dimensions: 146 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | SWRESET_POWERON_E |
| 0x0001 | SWRESET_POWERON_WDT_E |
| 0x0002 | SWRESET_POWERON_KL15_E |
| 0x0003 | SWRESET_HW_E |
| 0x0004 | SWRESET_WDT_E |
| 0x1000 | TRAP_MMU_VAF_E |
| 0x1001 | TRAP_MMU_VAP_E |
| 0x1002 | TRAP_INTPROT_PRIV_E |
| 0x1003 | TRAP_INTPROT_MPR_E |
| 0x1004 | TRAP_INTPROT_MPW_E |
| 0x1005 | TRAP_INTPROT_MPX_E |
| 0x1006 | TRAP_INTPROT_MPP_E |
| 0x1007 | TRAP_INTPROT_MPN_E |
| 0x1008 | TRAP_INTPROT_GRWP_E |
| 0x1009 | TRAP_INSTRERR_IOPC_E |
| 0x100A | TRAP_INSTRERR_UOPC_E |
| 0x100B | TRAP_INSTRERR_OPD_E |
| 0x100C | TRAP_INSTRERR_ALN_E |
| 0x100D | TRAP_INSTRERR_MEM_E |
| 0x100E | TRAP_CONTMANA_FCD_E |
| 0x100F | TRAP_CONTMANA_CDO_E |
| 0x1010 | TRAP_CONTMANA_CDU_E |
| 0x1011 | TRAP_CONTMANA_FCU_E |
| 0x1012 | TRAP_CONTMANA_CSU_E |
| 0x1013 | TRAP_CONTMANA_CTYP_E |
| 0x1014 | TRAP_CONTMANA_NEST_E |
| 0x1015 | TRAP_SYSBUSERR_PSE_E |
| 0x1016 | TRAP_SYSBUSERR_DSE_E |
| 0x1017 | TRAP_SYSBUSERR_DAE_E |
| 0x1018 | TRAP_SYSBUSERR_CAE_E |
| 0x1019 | TRAP_SYSBUSERR_PIE_E |
| 0x101A | TRAP_SYSBUSERR_DIE_E |
| 0x101B | TRAP_ASSTRAP_OVF_E |
| 0x101C | TRAP_ASSTRAP_SOVF_E |
| 0x101D | TRAP_SYSCALL_SYS_E |
| 0x101E | TRAP_NMI_ESR0_E |
| 0x101F | TRAP_NMI_ESR1_E |
| 0x1020 | TRAP_NMI_RES0_E |
| 0x1021 | TRAP_NMI_WDT_E |
| 0x1022 | TRAP_NMI_PE_E |
| 0x1023 | TRAP_NMI_OSCLWD_E |
| 0x1024 | TRAP_NMI_OSCHWD_E |
| 0x1025 | TRAP_NMI_OSCSPWD_E |
| 0x1026 | TRAP_NMI_SYSVCOLCK_E |
| 0x1027 | TRAP_NMI_ERAYVCOLCKT |
| 0x1028 | TRAP_NMI_FLOT_E |
| 0x2000 | SWRESET_POWERON_SIMU_E |
| 0x2001 | SWRESET_HRESET_SIMU_E |
| 0x2002 | SWRESET_RB_PROG_E |
| 0x2003 | SWRESET_SOFTRESET_5VUNDERVOLTAGE_E |
| 0x2004 | SWRESET_SOFTRESET_POSTDRV2PREDRV_E |
| 0x2005 | SWRESET_CBPROG_E |
| 0x2006 | SWRESET_CBCPU_E |
| 0x2007 | SWRESET_SBDUMMY_1_E |
| 0x2008 | SWRESET_SBDUMMY_2_E |
| 0x2009 | SWRESET_SBDUMMY_3_E |
| 0x200A | SWRESET_SBDUMMY_4_E |
| 0x200B | SWRESET_SBDUMMY_5_E |
| 0x200C | SWRESET_SBDUMMY_6_E |
| 0x200D | SWRESET_SBDUMMY_7_E |
| 0x200E | SWRESET_SBDUMMY_8_E |
| 0x3000 | SWRST_EEPBANDGAP_E |
| 0x3001 | SWRST_EEPNODEBUGGER_E |
| 0x3002 | SWRST_EEPDELENVRAM_E |
| 0x3003 | SWRST_WRITE_ERRORS_SECTORCHANGE_E |
| 0x3004 | SWRST_EEPACTFIRSTINIT_E |
| 0x3005 | RESET_SWRESET_EPMHCRS_WAIT_PCP_RESET_E |
| 0x3006 | RESET_SWRESET_ESC_SCHED_RESET_E |
| 0x3007 | SWRST_EXECON_FAULTYSTATE_E |
| 0x3008 | RESET_SWRESET_ILLEGAL_OPCODE |
| 0x3009 | RESET_SWRESET_ILLEGAL_RETURN_TO_MAIN |
| 0x300A | SWRESET_MOCADCNTP_PREICO |
| 0x300B | SWRESET_MOCADCTST_PREICO |
| 0x300C | RESET_SWRESET_ILLEGAL_SW_PATH |
| 0x300D | RESET_SWRESET_MOCCOM_SPI_ERROR |
| 0x300E | RESET_SWRESET_MOCCOM_CTSOPTST |
| 0x300F | RESET_SWRESET_MOCCOM_SOPTST |
| 0x3010 | RESET_SWRESET_MOCCOM_CPLCHK_FAILED |
| 0x3011 | RESET_SWRESET_MOCCOM_OS_TIMEOUT_ERROR |
| 0x3012 | RESET_SWRESET_MOCGPTA |
| 0x3013 | RESET_SWRESET_MOCMEM_CPL |
| 0x3014 | RESET_SWRESET_MOCMEM_RAM |
| 0x3015 | RESET_SWRESET_MOCMEM_ROM |
| 0x3016 | RESET_SWRESET_MOCPCP |
| 0x3017 | RESET_SWRESET_MOCRAM_WRI |
| 0x3018 | RESET_SWRESET_MOCRAM_CPL |
| 0x3019 | RESET_SWRESET_MOCRAM_RAMTAB |
| 0x301A | RESET_SWRESET_MOCRAM_RSTPTRRAM |
| 0x301B | RESET_SWRESET_MOCRAM_STACKRAM |
| 0x301C | RESET_SWRESET_MOCRAM_CSARAM |
| 0x301D | RESET_SWRESET_MOCRAM_XRAM |
| 0x301E | RESET_SWRESET_MOCRAM_IRAM |
| 0x301F | RESET_SWRESET_MOCRAM_EXRAM |
| 0x3020 | RESET_SWRESET_MOCRAM_PROTRAM |
| 0x3021 | RESET_SWRESET_MOCRAM_EEPCPL |
| 0x3022 | RESET_SWRESET_MOCRAM_REPEXOK |
| 0x3023 | RESET_SWRESET_MOCROM |
| 0x3024 | RESET_SWRESET_MOCROM_CPL |
| 0x3025 | RESET_SWRESET_MOCROM_INDEX |
| 0x3026 | RESET_SWRESET_MOCROM_WD |
| 0x3027 | RESET_SWRESET_SOPTEST_FAILED |
| 0x3028 | RESET_SWRESET_CPLCHK_FAILED |
| 0x3029 | RESET_SWRESET_MOCSOP_MSC_ERROR |
| 0x302A | RESET_SWRESET_MOCSOP_SPI_ERROR |
| 0x302B | RESET_SWRESET_MOCSOP_OS_TIMEOUT_ERROR |
| 0x302C | RESET_SWRESET_MOCSOP_TIRESPTIME_ERROR |
| 0x302D | SWRESET_MOFAIR_ADJ_PREICO |
| 0x302E | SWRESET_MOFAPP_PREICO |
| 0x302F | SWRESET_MOFESPD_PREICO |
| 0x3030 | SWRESET_MOFGKC_PREICO |
| 0x3031 | SWRESET_MOFRLC_PREICO |
| 0x3032 | RESET_SWRESET_MOFICO_CHK_SYEGAS_FAILED |
| 0x3033 | SWRESET_MOFMODC_PREICO |
| 0x3034 | SWRESET_MOFRKTI_PREICO |
| 0x3035 | SWRESET_MOFTRQCMP_PREICO |
| 0x3036 | SWRESET_MOFTRQRAT_PREICO |
| 0x3037 | SWRESET_MOFTX_PREICO |
| 0x3038 | SWRESET_MOFVAR_PREICO |
| 0x3039 | SWRESET_MOFZWC_PREICO |
| 0x303A | SWRESET_OCWDA_WDA_ACTV |
| 0x303B | SWRESET_OCWDA_WDA_MONITOR |
| 0x303C | SWRESET_OCWDA_LOW_VLTG |
| 0x303D | SWRESET_OCWDA_OVR_VLTG |
| 0x303E | RESET_SWRESET_INTERRUPTLOCK_EXPECTED |
| 0x303F | RESET_USERSTACKOVERFLOW_DETECTED |
| 0x3040 | SWRESET_PCP_ERROR_E |
| 0x3041 | SWRST_HWEMONDEFAULT_E |
| 0x3042 | RESET_ERRINTR_E |
| 0x3043 | SWRESET_CALWAKEUP_E |
| 0x3044 | SWRESET_DEADLINE1MS_E |
| 0x3045 | SWRESET_DEADLINE10MS_E |
| 0x3046 | SWRESET_DEADLINEBG_E |
| 0x3047 | SWRESET_NMIDISABLED_E |
| 0x3048 | SWRESET_POSTDRIVE_E |
| 0x3049 | SWRESET_SOFTRESET_WAKEUP_E |
| 0x304A | SWRESET_SOFTRESET_SHUTDOWN_E |
| 0x304B | SWRESET_T15RSTSHUTDOWN_E |
| 0x304C | SWRESET_UNDERVOLTAGE_E |
| 0x304D | SWRESET_T15_PRE_E |
| 0x304E | RESET_SWRESET_SWOVER_DONE |
| 0x304F | SWRESET_CORE_ENV_E |
| 0x3050 | SWRST_ADCI_ERROR_E |
| 0x3051 | SWRST_R2S2_INI_ERROR_E |
| 0x3052 | RESET_DMA_ERROR_E |
| 0x3053 | SWRST_FLASHCONFIG_E |
| 0xFFFF | undefiniert |

<a id="table-ba-vcv-state-text"></a>
### BA_VCV_STATE_TEXT

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | VCV_TEST |
| 0x01 | START |
| 0x02 | MFP_CTL |
| 0x03 | VCV_CLOSE |
| 0x04 | VCV_CRASH |
| 0x05 | MFP_MAX |
| 0x06 | VCV_LIH |
| 0xFF | undefiniert |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 388 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| IPUMG | 0x4201 | STAT_UMGEBUNGSDRUCK_WERT | Umgebungsdruck | hPa | pu_w | - | unsigned integer | - | 0,0390625 | 1 | 0,0 | - | 22;2C | - | - |
| IPLAD | 0x4205 | STAT_LADEDRUCK_WERT | Druck vor Drosselklappe | hPa | pvd_w | - | unsigned integer | - | 0,078125 | 1 | 0,0 | - | 22;2C | - | - |
| ITKUM | 0x4300 | STAT_KUEHLMITTELTEMPERATUR_WERT | Motor-Temperatur | Grad C | tmot | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| SNWAP | 0x4306 | STAT_WASSERPUMPE_DREHZAHL_SOLL_WERT | Quittung  Solldrehzahl von BSS-Wasserpumpe | 1/min | wmpdzst | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4307_WERT | 0x4307 | STAT_0x4307_WERT | empf. Status von BSS-Wasserpumpe | - | wmstat | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| ITOEL | 0x4402 | STAT_OELTEMPERATUR_WERT | Oeltemperatur nach Filter | Grad C | toel_w | - | unsigned integer | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| IKVLS | 0x4403 | STAT_KRAFTSTOFFVERBRAUCH_SEIT_SERVICE_WERT | Kraftstoffverbrauch seit letztem Ölwechsel | - | ozkvbsm_ul | - | unsigned long | - | 1,220703125E-4 | 1 | 0,0 | - | 22;2C | - | - |
| IKMLS | 0x4404 | STAT_WEG_SEIT_SERVICE_WERT | Ölkilometer | km | ozoelkm | - | unsigned integer | - | 10,0 | 1 | 0,0 | - | 22;2C | - | - |
| RNIOE | 0x4405 | STAT_OELSENSOR_NIVEAU_ROH_WERT | Sensorrohwert Ölniveau | - | oznivr | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| RQUOE | 0x4406 | STAT_OELSENSOR_QUALITAET_ROH_WERT | Sensorrohwert Permittivität | - | ozpermr_w | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| RTOEL | 0x4407 | STAT_OELSENSOR_TEMPERATUR_ROH_WERT | Sensorrohwert Öltemperatur | - | oztempr | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| ITSOE | 0x4408 | STAT_OELSENSOR_TEMPERATUR_WERT | Öltemperatur ungefiltert | Grad C | oztemp_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| INIOE | 0x4409 | STAT_OELSENSOR_NIVEAU_WERT | Ölniveau ungefiltert in [mm] | - | ozniv | - | unsigned char | - | 0,29296875 | 1 | 0,0 | - | 22;2C | - | - |
| IQOEL | 0x440A | STAT_OELSENSOR_QUALITAET_WERT | Permitivität für den Tester | - | ozpermakt | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x440B_WERT | 0x440B | STAT_0x440B_WERT | CodingDataSet-ÖL-Länderfaktor1- EEPROM | - | ozlf1c_eep | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x440C_WERT | 0x440C | STAT_0x440C_WERT | CodingDataSet-ÖL-Länderfaktor2- EEPROM | - | ozlf2c_eep | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x440D_WERT | 0x440D | STAT_0x440D_WERT | Länderfaktor 1 | - | ozlf1t | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x440E_WERT | 0x440E | STAT_0x440E_WERT | Länderfaktor 2 | - | ozlf2t | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x440F_WERT | 0x440F | STAT_0x440F_WERT | Kurzzeit-Ölniveau-Mittelwert für den DIS-Tester | - | oznivkrzt | - | unsigned char | - | 0,29296875 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4411_WERT | 0x4411 | STAT_0x4411_WERT | Restweg aus Kraftstoffverbrauch abgeleitet | - | ozrwkvb | - | signed integer | - | 10,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4412_WERT | 0x4412 | STAT_0x4412_WERT | Öllaufzeit | month | ozoelzeit | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4418_WERT | 0x4418 | STAT_0x4418_WERT | Status Ölzustandssensor | - | ozstatus | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| SSPEI | 0x4505 | STAT_NW_EINLASSSPREIZUNG_SOLL_WERT | Sollwinkel vom BMW Layer (Einlass-VANOS) | Grad KW | wnwsaeb_w | - | signed integer | - | 0,0078125 | 1 | 0,0 | - | 22;2C | - | - |
| IPNWE | 0x4506 | STAT_POSITION_NOCKENWELLE_EINLASS_WERT | Einlassnockenwellenposition | Grad KW | wnwkwe_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| IPNWA | 0x4507 | STAT_POSITION_NOCKENWELLE_AUSLASS_WERT | Auslassnockenwellenposition | Grad KW | wnwkwa_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x450C_WERT | 0x450C | STAT_0x450C_WERT | Kurbelwellenadaption Einlass erfolgt | 0/1 | B_phade | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x450D_WERT | 0x450D | STAT_0x450D_WERT | Kurbelwellenadaption Auslass erfolgt | 0/1 | B_phada | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x450E_WERT | 0x450E | STAT_0x450E_WERT | Kurbelwellennullpunktverschiebung in Grad für Winkelversatzdiagnose | deg CrS | EpmCaS_phiDiffAvrgLim | - | signed integer | - | 0,02197265625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4510_WERT | 0x4510 | STAT_0x4510_WERT | VVT-Lageregler, bleibende Abweichung erkannt | 0/1 | B_dvvtregelabweichung | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x4511_WERT | 0x4511 | STAT_0x4511_WERT | VVT-Lageregelung, Schwingung erkannt | 0/1 | B_dvvtschwingung | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x4512_WERT | 0x4512 | STAT_0x4512_WERT | VVT überlastet | 0/1 | B_vvttempovl_wrn | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x4513_WERT | 0x4513 | STAT_0x4513_WERT | VVT-Überlastung, klemmender Steller | 0/1 | B_vvttempovl | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x4514_WERT | 0x4514 | STAT_0x4514_WERT | VVT-Adaption möglich | 0/1 | B_enadpvvt | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x4515_WERT | 0x4515 | STAT_0x4515_WERT | Anforderung, VVT-Anschlaglernen | - | vvtlrnaf | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4516_WERT | 0x4516 | STAT_0x4516_WERT | Status VVT-Anschlaglernen | - | vvtlrnst | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4517_WERT | 0x4517 | STAT_0x4517_WERT | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 0 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4518_WERT | 0x4518 | STAT_0x4518_WERT | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 1 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4519_WERT | 0x4519 | STAT_0x4519_WERT | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 2 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x451A_WERT | 0x451A | STAT_0x451A_WERT | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 3 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x451B_WERT | 0x451B | STAT_0x451B_WERT | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 4 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x451C_WERT | 0x451C | STAT_0x451C_WERT | Adaptierte Referenzposition einer Auslassnockenwellenflanke, Wert 5 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x451D_WERT | 0x451D | STAT_0x451D_WERT | Gesamtzeit VVT-Performancetest | - | vvtdtperf_w | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x451E_WERT | 0x451E | STAT_0x451E_WERT | Stromsumme VVT-Performancetest | A | ivvtsumperf_w | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| IWDKL | 0x4600 | STAT_DROSSELKLAPPENWINKEL_WERT | Drosselklappenwinkel bezogen auf unteren Anschlag | %DK | wdkba_w | - | signed integer | - | 0,0244140625 | 1 | 0,0 | - | 22;2C | - | - |
| SWDKL | 0x4601 | STAT_DROSSELKLAPPENWINKEL_SOLL_WERT | Sollwert Drosselklappenwinkel, bezogen auf (unteren) Anschlag | % | wdks_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| IIGEN | 0x4604 | STAT_GENERATOR_STROM_WERT | Generatorstrom | - | st_i_gen | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| VGENE | 0x4605 | STAT_GENERATOR_CHIPVERSION_WERT | Chipversion Generator 2 | - | bsdgencv | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| IUBAT | 0x460A | STAT_UBATT_WERT | momentane Batteriespannung | V | ubt | - | unsigned integer | - | 0,014999999664723873 | 1 | 0,0 | - | 22;2C | - | - |
| IUADW | 0x460C | STAT_UBATT_AD_WANDLER_WERT | Batteriespannung; vom AD-Wandler erfaßter Wert  | V | wub_w | - | unsigned integer | - | 0,02355000004172325 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x460D_WERT | 0x460D | STAT_0x460D_WERT | Korrekturwert Abschaltung | % | abschkor_w | - | unsigned integer | - | 0,004000000189989805 | 1 | -100,0 | - | 22;2C | - | - |
| TDSTF | 0x460E | STAT_0x460E_WERT | Abstand zur Startfähigkeit | % | dsoc_w | - | unsigned integer | - | 0,004000000189989805 | 1 | -100,0 | - | 22;2C | - | - |
| ILBAT | 0x460F | STAT_BATTERIELAST_WERT | DF-Monitor für Batterie-Ladezustand in % | % | dfmonitor | - | unsigned char | - | 0,390625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4613_WERT | 0x4613 | STAT_0x4613_WERT | vom Generator empfangene Generatorsollspannung (Kopie gesendeter Wert) | V | ufgen | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 | - | 22;2C | - | - |
| STAT_0x4615_WERT | 0x4615 | STAT_0x4615_WERT | Kopie begrenzter Erregerstrom Generator 1 | A | ierrfgrenz | - | unsigned char | - | 0,125 | 1 | 0,0 | - | - | - | - |
| STAT_0x4616_WERT | 0x4616 | STAT_0x4616_WERT | vom Generator empfangene Load response Zeit (Kopie gesendeter Wert) | s | tlrfgen | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4617_WERT | 0x4617 | STAT_0x4617_WERT | gefiltertes Generatormoment absolut | % | mdgenvf_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4618_WERT | 0x4618 | STAT_0x4618_WERT | Drehzahlschwelle für LR-Funktion Generator 1 aktiv | 0/1 | B_lrfoff | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x4619_WERT | 0x4619 | STAT_0x4619_WERT | Bedingung BSD Protokollinhalt für BSD2 Regler | 0/1 | B_bsdprot2 | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x461A_WERT | 0x461A | STAT_0x461A_WERT | Nominalspannung Regler Generator 1 | V | uregnom | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 | - | 22;2C | - | - |
| STAT_0x4680_WERT | 0x4680 | STAT_0x4680_WERT | Leerlaufdrehzahl gelernt | 0/1 | B_nggelernt | - | 0xFF | - | 1 | 1 | 0 | - | - | - | - |
| STAT_0x4681_WERT | 0x4681 | STAT_0x4681_WERT | Bereitschaft Getriebe Neutralposition anlernen | 0/1 | B_ngimlf | - | 0xFF | - | 1 | 1 | 0 | - | - | - | - |
| ISBV1 | 0x4700 | STAT_SONDENBEREITSCHAFT_VORKAT_BANK1 | Bedingung Sonde betriebsbereit vor Kat | 0/1 | B_sbbvk | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISBV2 | 0x4701 | STAT_SONDENBEREITSCHAFT_VORKAT_BANK2 | Bedingung Sonde betriebsbereit vor Kat, Bank 2 | 0/1 | B_sbbvk2 | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| IUSO1 | 0x4702 | STAT_SONDENSPANNUNG_VORKAT_BANK1_MIT_OFFSET_WERT | Offset korrigierte Sondenspannung vor Kat einer Breitbandlambdasonde | V | ua10mo_w | - | unsigned integer | - | 4,8828125E-4 | 1 | 0,0 | - | 22;2C | - | - |
| IUSO2 | 0x4703 | STAT_SONDENSPANNUNG_VORKAT_BANK2_MIT_OFFSET_WERT | Offset korrigierte Sondenspannung vor Kat einer Breitbandlambdasonde Bank 2 | V | ua10mo2_w | - | unsigned integer | - | 4,8828125E-4 | 1 | 0,0 | - | 22;2C | - | - |
| SINT1 | 0x4704 | STAT_LAMBDA_BANK1_SOLL_WERT | Lambdasoll Begrenzung (word) | - | lamsbg_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 | - | 22;2C | - | - |
| SINT2 | 0x4705 | STAT_LAMBDA_BANK2_SOLL_WERT | Lambdasoll Begrenzung (word) Bank2 | - | lamsbg2_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 | - | 22;2C | - | - |
| ISKUB | 0x4800 | STAT_KUPPLUNGSSCHALTER_BETAETIGT_WERT | Bedingung Kupplungspedal betätigt | 0/1 | B_kuppl | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISKUV | 0x4801 | STAT_KUPPLUNGSSCHALTER_VORHANDEN_WERT | Schalter Kupplung | 0/1 | S_kupp | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISSPO | 0x4802 | STAT_SPORTTASTER_BETAETIGT_WERT | Bedingung umschalten auf KFPEDS | 0/1 | B_pedsport | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISKLI | 0x4803 | STAT_KLIMA_EIN | Bedingung für Kompressoreinschalten | 0/1 | B_koe | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISSRC | 0x4805 | STAT_STARTRELAIS_UEBER_CAN_WERT | Schalter Klemme 50 von CAN | 0/1 | S_ckl50 | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| INMOT | 0x4807 | STAT_MOTORDREHZAHL_WERT | Motordrehzahl | 1/min | nmot_w | - | unsigned integer | - | 0,25 | 1 | 0,0 | - | 22;2C | - | - |
| SNLLD | 0x4808 | STAT_LEERLAUFDREHZAHL_SOLL_WERT | Leerlaufsolldrehzahl | 1/min | nsol_w | - | unsigned integer | - | 0,25 | 1 | 0,0 | - | 22;2C | - | - |
| ISLLA | 0x4809 | STAT_LEERLAUF_AKTIV | Bedingung Leerlaufregelung | 0/1 | B_llr | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| IFPWG | 0x480B | STAT_FAHRERWUNSCH_PEDAL_WERT | normierter Fahrpedalwinkel | %PED | wped_w | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4880_WERT | 0x4880 | STAT_0x4880_WERT | Max. Quotient Zündwinkelwirkungsgrad-Fehlerintegral im Leerlauf bez. auf Schwellwert | % | etkhlmx | - | unsigned char | - | 0,78125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4881_WERT | 0x4881 | STAT_0x4881_WERT | Max. Quotient Zündwinkelwirkungsgrad-Fehlerintegral im Teillast bez. auf Schwellwert | % | etkhtmx | - | unsigned char | - | 0,78125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4A02_WERT | 0x4A02 | STAT_0x4A02_WERT | ATL-Leckagediagnose läuft | 0/1 | B_atlberlek | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| IUDMT | 0x4A17 | STAT_DMTL_SPANNUNG_WERT | Spannung Pumpenstrom Tankdiagnose | V | uptes_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4A1B_WERT | 0x4A1B | STAT_0x4A1B_WERT | Elektrische Kraftstoffpumpe | 0/1 | B_ekp | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x4A1D_WERT | 0x4A1D | STAT_0x4A1D_WERT | Spannung Bremsenunterdruck | V | udsbkv_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | - | - | - |
| ITKUA | 0x4A21 | STAT_KUEHLERAUSLASSTEMPERATUR_WERT | Kühlmitteltemperatur (Sensorwert) nach Tiefpassfilterung | Grad C | tmotlinf | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| STAT_0x4A2B_WERT | 0x4A2B | STAT_0x4A2B_WERT | physikalischer Temperaturwert, der sich bei Wandlung der tiefpassgefilterten Sensorspannung wtfa1f_w | Grad C | tfa1linf | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| STAT_0x4A2D_WERT | 0x4A2D | STAT_0x4A2D_WERT | Saugrohr-Absolutdruck gemessen | hPa | psrg_w | - | unsigned integer | - | 0,078125 | 1 | 0,0 | - | 22;2C | - | - |
| ILUZ1 | 0x4A30 | STAT_LAUFUNRUHE_ZYL1_WERT | Laufunruhe Zylinder 1 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 | - | 22;2C | - | - |
| ILUZ2 | 0x4A31 | STAT_LAUFUNRUHE_ZYL2_WERT | Laufunruhe Zylinder 2 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 | - | 22;2C | - | - |
| ILUZ3 | 0x4A32 | STAT_LAUFUNRUHE_ZYL3_WERT | Laufunruhe Zylinder 3 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 | - | 22;2C | - | - |
| ILUZ4 | 0x4A33 | STAT_LAUFUNRUHE_ZYL4_WERT | Laufunruhe Zylinder 4 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 | - | 22;2C | - | - |
| ILUZ5 | 0x4A34 | STAT_LAUFUNRUHE_ZYL5_WERT | Laufunruhe Zylinder 5 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 | - | 22;2C | - | - |
| ILUZ6 | 0x4A35 | STAT_LAUFUNRUHE_ZYL6_WERT | Laufunruhe Zylinder 6 | (Umdr./sec)^2 | lutskzyl_w | - | signed integer | - | 0,0063159349374473095 | 1 | 0,0 | - | 22;2C | - | - |
| ISKLO | 0x4A36 | STAT_STATUS_KLOPFEN_WERT | Bedingung für erkannte Klopfer | 0/1 | B_kl | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| IUKZ1 | 0x4A37 | STAT_KLOPFWERT_ZYL1_SPANNUNG_WERT | normierter Referenzpegel Klopfregelung Zylinder 1 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| IUKZ2 | 0x4A38 | STAT_KLOPFWERT_ZYL2_SPANNUNG_WERT | normierter Referenzpegel Klopfregelung Zylinder 2 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| IUKZ3 | 0x4A39 | STAT_KLOPFWERT_ZYL3_SPANNUNG_WERT | normierter Referenzpegel Klopfregelung Zylinder 3 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| IUKZ4 | 0x4A3A | STAT_KLOPFWERT_ZYL4_SPANNUNG_WERT | normierter Referenzpegel Klopfregelung Zylinder 4 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| IUKZ5 | 0x4A3B | STAT_KLOPFWERT_ZYL5_SPANNUNG_WERT | normierter Referenzpegel Klopfregelung Zylinder 5 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| IUKZ6 | 0x4A3C | STAT_KLOPFWERT_ZYL6_SPANNUNG_WERT | normierter Referenzpegel Klopfregelung Zylinder 6 | V | rkrnv6_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| IZWZ1 | 0x4A49 | STAT_ZUENDWINKEL_ZYL1_WERT | Ausgegebener Zündwinkel | Grad KW | zwoutzyl_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| ILAB1 | 0x4A50 | STAT_LAMBDA_BANK1_WERT | Lambda-Istwert | - | lamsoni_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 | - | - | - | - |
| ILAB2 | 0x4A51 | STAT_LAMBDA_BANK2_WERT | Lambda-Istwert Bank2 | - | lamsoni2_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 | - | - | - | - |
| IRNK1 | 0x4A52 | STAT_READINESS_SONDE_NACHKAT_BANK1_WERT | Bedingung Sonde betriebsbereit hinter Kat | 0/1 | B_sbbhk | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| IRNK2 | 0x4A53 | STAT_READINESS_SONDE_NACHKAT_BANK2_WERT | Bedingung Sonde betriebsbereit hinter Kat Bank2 | 0/1 | B_sbbhk2 | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISHN1 | 0x4A54 | STAT_SONDENHEIZUNG_NACHKAT_BANK1_WERT | Bedingung Sonde hinter Kat ausreichend beheizt | 0/1 | B_hsha | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISHN2 | 0x4A55 | STAT_SONDENHEIZUNG_NACHKAT_BANK2_WERT | Bedingung Sonde 2 hinter Kat ausreichend beheizt | 0/1 | B_hsha2 | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISHV1 | 0x4A56 | STAT_SONDENHEIZUNG_VORKAT_BANK1_WERT | Bedingung: Heizerstatus A liegt vor, Sonde ist ausreichend aufgeheizt | 0/1 | B_hstlsua | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISHV2 | 0x4A57 | STAT_SONDENHEIZUNG_VORKAT_BANK2_WERT | Bedingung: Heizerstatus A liegt vor, Sonde ist ausreichend aufgeheizt, Bank2 | 0/1 | B_hstlsua2 | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISBLS | 0x4A60 | STAT_BREMSLICHTSCHALTER_EIN_WERT | Bedingung Bremslichtschalter betätigt | 0/1 | B_bl | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISBLT | 0x4A61 | STAT_BREMSLICHTTESTSCHALTER_EIN_WERT | Bedingung Bremstestschalter betätigt | 0/1 | B_br | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISAGK | 0x4A65 | STAT_ABGASKLAPPE_EIN_WERT | Bedingung Abgasklappe mit Resonator | 0/1 | B_akr | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISDMP | 0x4A66 | STAT_DMTL_PUMPE_EIN_WERT | Bedingung DMTL-Pumpenmotor an | 0/1 | B_admtpm | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISDMV | 0x4A67 | STAT_DMTL_VENTIL_EIN_WERT | Bedingung DMTL-Magnetventil an | 0/1 | B_admtmv | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISDMH | 0x4A68 | STAT_DMTL_HEIZUNG_EIN_WERT | Bedingung Heizung DM-TL Portansteuerung | 0/1 | B_hdmtlp | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISMIL | 0x4A69 | STAT_MIL_EIN_WERT | MIL-Ansteuerung | 0/1 | B_mil | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISFGR | 0x4A6A | STAT_LAMPE_FGR_EIN_WERT | Lampe FGR ein | 0/1 | B_fgr | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ISCEL | 0x4A6B | STAT_CHECK_ENGINE_LAMPE_EIN_WERT | Bedingung für Ansteuerung EGAS-Fehlerlampe | 0/1 | B_epcl | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x4A6C_WERT | 0x4A6C | STAT_0x4A6C_WERT | Korrekturfaktor für die Kraftstoffmenge | % | kva_korr | - | signed char | - | 0,0010000000474974513 | 1 | 0,0 | - | 22;2C | - | - |
| IAKFT | 0x4A74 | STAT_BEHEIZTER_THERMOSTAT_PWM_WERT | Tastverhältnis Kennfeldthermostat | - | tkwpwm | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| IATEV | 0x4A77 | STAT_TEV_PWM_WERT | ausgegebenes Tastverhältnis für Tankentlüftungsventil (16 Bit) | % | tateout_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| IAVEP | 0x4A7A | STAT_VANOS_EINLASS_PWM_WERT | Tastverhältnis Einlaßnockenwellenregelung Ansteuerung Endstufe(word) | % | tanwree_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| IAVAP | 0x4A7B | STAT_VANOS_AUSLASS_PWM_WERT | Tastverhältnis Auslaßnockenwellenregelung Ansteuerung Endstufe(word) | % | tanwraa_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| IMUL1 | 0x4A85 | STAT_ADAPTION_MULTIPLIKATIV_BANK1_WERT | multiplikative Gemischkorrektur der Gemischadaption (Word) | - | fra_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4A91_WERT | 0x4A91 | STAT_0x4A91_WERT | Amplitudenverhältnis laafh/laafv gefiltert | - | avkatf | - | unsigned char | - | 0,00390625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4A92_WERT | 0x4A92 | STAT_0x4A92_WERT | Amplitudenverhältnis laafh/laafv gefiltert Bank2 | - | avkatf2 | - | unsigned char | - | 0,00390625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4A93_WERT | 0x4A93 | STAT_0x4A93_WERT | Fehlerzähler für Lernen Nullgang | - | GbxNPos_ctDefPlausDia | - | unsigned char | - | 1,0 | 1 | 0,0 | - | - | - | - |
| SANWA | 0x4A94 | STAT_NW_AUSLASS_SOLL_WERT | gespeicherter Nockenwellensollwinkel Auslaß | Grad KW | wnwsswa_w | - | signed integer | - | 0,0078125 | 1 | 0,0 | - | 22;2C | - | - |
| IANWA | 0x4A95 | STAT_NW_ADAPTION_AUSLASS_WERT | Adaptionswert Nockenwelle Auslass Bank 1 | deg CrS | EpmCaS_phiAdapRefPosO1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 | - | 22;2C | - | - |
| IANWE | 0x4A96 | STAT_NW_ADAPTION_EINLASS_WERT | Adaptionswert Nockenwelle Einlass Bank 1 | deg CrS | EpmCaS_phiAdapRefPosI1_mp | - | signed integer | - | 0,02197265625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4A97_WERT | 0x4A97 | STAT_0x4A97_WERT | Bedi. Vanos Einlass im Anschlag | 0/1 | B_vseansch | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| IAKWF | 0x4A99 | STAT_KURBELWELLEN_ADAPTION_BEENDET_WERT | Status der fuel-off Adaption im aktuellen Betriebsbereich | - | fofstat | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4A9D_WERT | 0x4A9D | STAT_0x4A9D_WERT | multiplikative Gemischkorrektur der Gemischadaption | - | frai_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| IDSLS | 0x4AA1 | STAT_SLS_DIAGNOSE_WERT | Zyklusflag: Tankentlüftungsventil Endstufe | - | Z_teve_byte | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| IDTEV | 0x4AA2 | STAT_TEV_DIAGNOSE_WERT | Funktionsstatus-Zähler DM-TL für Testerausgabe aus letztem Fahrzyklus | - | stpdmtla | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| IDLSS | 0x4AA4 | STAT_LS_DIAGNOSE_WERT | Funktionsstatus LLRNS bei Anforderung Systemcheck | - | llsstat | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AAA_WERT | 0x4AAA | STAT_0x4AAA_WERT | Tastverhältnis PWM Ansteuerung Öldruck | % | tvpoel_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AAB_WERT | 0x4AAB | STAT_0x4AAB_WERT | Tastverhältnis an Endstufe des Ladedruckstellers | % | tvldste_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5AAC_WERT | 0x4AAC | STAT_0x5AAC_WERT | Tastverhältnis an Endstufe des Ladedruckstellers, Bank 2 | % | tvldste2_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AB0_WERT | 0x4AB0 | STAT_0x4AB0_WERT | Ladedruck- Sollwert | hPa | psolldr_w | - | unsigned integer | - | 0,0390625 | 1 | 0,0 | - | 22;2C | - | - |
| IVKMH | 0x4AB1 | STAT_GESCHWINDIGKEIT_WERT | Fahrzeuggeschwindigkeit | km/h | vfzg_w | - | unsigned integer | - | 0,0078125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5AB3_WERT | 0x4AB3 | STAT_FAHRSTRECKE_MIL_AN_WERT | Zähler für gefahrene Kilometer mit MIL EIN | km | DSMDur_ctPID21h | - | unsigned long | - | 0,009999999776482582 | 1 | 0,0 | - | 22;2C | - | - |
| IZBST | 0x4AB4 | STAT_BETRIEBSSTUNDENZAEHLER_WERT | sekundengenauer Betribsstundenzähler als 32 Bitwert | s | top_l | - | unsigned long | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| IUSAU | 0x4AB8 | STAT_SAUGROHRDRUCK_SPANNUNG_WERT | Spannung Drucksensor Saugrohrdruck (word) | V | udss_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| IMLUF | 0x4ABC | STAT_LUFTMASSE_WERT | Luftmassenfluss gefiltert (Word) | kg/h | ml_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| IASRE | 0x4ABD | STAT_STARTRELAIS_AKTIV_WERT | Bedingung automatischer Start | 0/1 | B_sta | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x4ABE_WERT | 0x4ABE | STAT_0x4ABE_WERT | I-Regler Mengenregelung Kraftstoffsystem | mg | FUEL_MASS_REQ_I_CTL_H_RES | - | signed integer | - | 0,0211944580078125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4ABF_WERT | 0x4ABF | STAT_0x4ABF_WERT | Verbrauch ohne Regler | l/h | VFF_MFF_SP_FUP_CTL | - | unsigned integer | - | 0,0038910505827516317 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AC0_WERT | 0x4AC0 | STAT_0x4AC0_WERT | Verbrauch mit Regler | l/h | VFF_VCV | - | unsigned integer | - | 0,0038910505827516317 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AC2_WERT | 0x4AC2 | STAT_0x4AC2_WERT | Reset Information  | - | Reset_Env.adLoc | - | unsigned long | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AC4_WERT | 0x4AC4 | STAT_0x4AC4_WERT | Raildruck Kraftstoffsystem Sollwert | MPa | prsoll_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AC6_WERT | 0x4AC6 | STAT_0x4AC6_WERT | Modus Kraftstoffsystem (Druck-, Mengen-, oder Maximumregelung) | 0-n | STATE_PWM_VCV | - | unsigned char | ba_vcv_state_text | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x4ACC_WERT | 0x4ACC | STAT_0x4ACC_WERT | Luftklappe - Sollposition in Schritten | - | RadSht_StpEng | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4ACD_WERT | 0x4ACD | STAT_0x4ACD_WERT | Luftklappe - Istposition in Schritten | - | ShtrEcu_StpEngPos | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AD0_WERT | 0x4AD0 | STAT_0x4AD0_WERT | Luftklappe - Diagnosestatus allgemein | - | RadSht_stDiagGen | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AD1_WERT | 0x4AD1 | STAT_0x4AD1_WERT | Luftklappe - Diagnosestatus obere Luftklappe | - | RadSht_stDiagAKKS | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AD2_WERT | 0x4AD2 | STAT_0x4AD2_WERT | Luftklappe - Status obere Luftklappe | - | RadSht_stDiagAbvAirVlv | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AD3_WERT | 0x4AD3 | STAT_0x4AD3_WERT | Luftklappe - Status untere Luftklappe | - | RadSht_stDiagBntAirVlv | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AD4_WERT | 0x4AD4 | STAT_0x4AD4_WERT | Luftklappe - Varianteninfo vom Steller | - | ShtrEcu_stVrs | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AD5_WERT | 0x4AD5 | STAT_0x4AD5_WERT | Kraftstofftemperatur | Grad C | tkrst | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| STAT_0x4AD6_WERT | 0x4AD6 | STAT_0x4AD6_WERT | Bedingung Schubabschalten | 0/1 | B_sa | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x4AE2_WERT | 0x4AE2 | STAT_0x4AE2_WERT | Reset Information - Reset-group-ID of the last reset reason | 0-n | Reset_Env.xGrp | - | unsigned char | Reset_GrpID | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x4AE3_WERT | 0x4AE3 | STAT_0x4AE3_WERT | Reset Information - Reset-ID of the last reset | 0-n | Reset_Env.xId | - | unsigned integer | Reset_ID | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x4AE4_WERT | 0x4AE4 | STAT_0x4AE4_WERT | Reset Information - User defined value of the last reset reason | - | Reset_Env.xUserValue | - | unsigned long | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AEB_WERT | 0x4AEB | STAT_0x4AEB_WERT | Kühlmitteltemperatur &lt; 98°C | % | tmotb1_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AEC_WERT | 0x4AEC | STAT_0x4AEC_WERT | 98°C =&lt; Kühlmitteltemperatur =&lt; 112°C | % | tmotb2_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AED_WERT | 0x4AED | STAT_0x4AED_WERT | 113°C =&lt; Kühlmitteltemperatur =&lt; 120°C | % | tmotb3_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AEE_WERT | 0x4AEE | STAT_0x4AEE_WERT | 121°C =&lt; Kühlmitteltemperatur =&lt; 125°C | % | tmotb4_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AEF_WERT | 0x4AEF | STAT_0x4AEF_WERT | Kühlmitteltemperatur &gt; 125°C | % | tmotb5_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x4AF0_WERT | 0x4AF0 | STAT_0x4AF0_WERT | Motoröltemperatur &lt; 80°C | % | toelb1_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5800_WERT | 0x5800 | STAT_0x5800_WERT | Zeitzähler ab Startende (16bit) | s | tnse_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5801_WERT | 0x5801 | STAT_0x5801_WERT | Umgebungsdruck | hPa | pu | - | unsigned char | - | 5,0 | 1 | 0,0 | - | 22;2C | - | - |
| ICLR1 | 0x5802 | STAT_LAMBDAREGELUNG_ZUSTAND_BANK1_WERT | CARB FREEZE FRAME Byte, Bank 1, für LR | - | flglrs | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5803_WERT | 0x5803 | STAT_0x5803_WERT | CARB FREEZE FRAME Byte, Bank 2, für LR | - | flglrs2 | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| ILMAR | 0x5804 | STAT_LUFTMASSE_RELATIV_WERT | relative Luftmasse (calc. load value) nach SAE J1979 | % | rml | - | unsigned char | - | 0,390625 | 1 | 0,0 | - | 22;2C | - | - |
| ITMOT | 0x5805 | STAT_MOTORTEMPERATUR_LINEAR_WERT | Motortemperatur, linearisiert und umgerechnet | Grad C | tmotlin | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| IINT1 | 0x5806 | STAT_INTEGRATOR_BANK1_WERT | Lambda-Regler-Ausgang (Word) | - | fr_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| ILAM1 | 0x5807 | STAT_LAMBDA_ADAPTION_MULTIPLIKATIV_GRUPPE1_WERT | Faktor aus Lambdaregelungsadaption für Bank 1 | - | frann_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| ILAM2 | 0x5809 | STAT_LAMBDA_ADAPTION_MULTIPLIKATIV_GRUPPE2_WERT | Faktor aus Lambdaregelungsadaption, Bank 2 | - | frann2_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| IPSAU | 0x580B | STAT_SAUGROHRDRUCK_WERT | Saugrohr-Absolutdruck | hPa | ps_w | - | unsigned integer | - | 0,0390625 | 1 | 0,0 | - | 22;2C | - | - |
| INAUF | 0x580C | STAT_N_AUFLOESUNG_WERT | Motordrehzahl | 1/min | nmot | - | unsigned char | - | 40,0 | 1 | 0,0 | - | 22;2C | - | - |
| IVKM2 | 0x580D | STAT_GESCHWINDIGKEIT_2_WERT | Fahrzeuggeschwindigkeit | km/h | vfzg | - | unsigned char | - | 1,25 | 1 | 0,0 | - | 22;2C | - | - |
| IZZY1 | 0x580E | STAT_ZUENDZEITPUNKT_ZYL1_WERT | Zündwinkel Zylinder 1 | Grad KW | zwzyl1 | - | signed char | - | 0,75 | 1 | 0,0 | - | 22;2C | - | - |
| ITANS | 0x580F | STAT_ANSAUGLUFTTEMPERATUR_WERT | Ansaugluft-Temperatur | Grad C | tans | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| ILMKG | 0x5812 | STAT_LUFTMASSE_WERT | Massenstrom HFM | kg/h | mshfm_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| ILREL | 0x5813 | STAT_LASTWERT_RELATIV_WERT | relative Luftfüllung | % | rl | - | unsigned char | - | 0,75 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5814_WERT | 0x5814 | STAT_0x5814_WERT | Normierter Fahrpedalwinkel | %PED | wped | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 | - | 22;2C | - | - |
| IUK87 | 0x5815 | STAT_KL87_SPANNUNG_WERT | Batteriespannung | V | ub | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5816_WERT | 0x5816 | STAT_0x5816_WERT | Lambda-Sollwert bezogen auf Einbauort Lambda-Sensor | - | lamsons_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 | - | 22;2C | - | - |
| ITUMG | 0x5817 | STAT_UMGEBUNGSTEMPERATUR_WERT | Umgebungstemperatur | Grad C | tumg | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| ILMMG | 0x5818 | STAT_LUFTMASSE_PRO_HUB_WERT | Luftmassenfluß | kg/h | ml | - | unsigned char | - | 4,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5819_WERT | 0x5819 | STAT_0x5819_WERT | Motordrehzahl [1/min] | rpm | Epm_nEng | - | signed integer | - | 0,5 | 1 | 0,0 | - | 22;2C | - | - |
| ISNWE | 0x581A | STAT_NW_EINLASSSPREIZUNG_WERT | Winkel Einlassventil oeffnet bezogen auf LWOT | Grad KW | wnwe_w | - | signed integer | - | 0,0078125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x581B_WERT | 0x581B | STAT_0x581B_WERT | Sollwinkel Nockenwelle Einlass öffnet | Grad KW | wnwse_w | - | signed integer | - | 0,0078125 | 1 | 0,0 | - | 22;2C | - | - |
| ISNWA | 0x581C | STAT_NW_AUSLASSSPREIZUNG_WERT | Winkel Auslassventil schließt bezogen auf LWOT | Grad KW | wnwa_w | - | signed integer | - | 0,0078125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x581D_WERT | 0x581D | STAT_0x581D_WERT | Sollwinkel Nockenwelle Auslass schließt | Grad KW | wnwsa_w | - | signed integer | - | 0,0078125 | 1 | 0,0 | - | 22;2C | - | - |
| RTANS | 0x581E | STAT_ANSAUGLUFTTEMPERATUR1_ROH_WERT | Ansauglufttemperatur, linearisiert und umgerechnet | Grad C | tanslin | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| STAT_0x5820_WERT | 0x5820 | STAT_0x5820_WERT | Bedingung Klemme 15 | 0/1 | B_kl15 | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x5821_WERT | 0x5821 | STAT_0x5821_WERT | Steuergerätetemperatur | Grad C | tsg | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| STAT_0x5822_WERT | 0x5822 | STAT_0x5822_WERT | Öltemperatur | Grad C | toel | - | unsigned char | - | 1,0 | 1 | -60,0 | - | 22;2C | - | - |
| IZMOS | 0x5823 | STAT_ZEIT_MOTOR_STEHT_WERT | Abstellzeit | s | tabst_w | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5825_WERT | 0x5825 | STAT_0x5825_WERT | Spannung von BCU gemessen (U_BCU_LIN) | V | BcuEcu_u | - | signed integer | - | 0,009999999776482582 | 1 | 0,0 | - | 22;2C | - | - |
| IDKS1 | 0x5826 | STAT_DROSSELKLAPPE_SENSOR1_WERT | Drosselklappenwinkel aus Poti 1 | %DK | wdk1 | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 | - | 22;2C | - | - |
| IAHV1 | 0x5827 | STAT_SONDENHEIZUNG_PWM_VORKAT_BANK1_WERT | Tastverhältnis für Lambdasondenheizung | % | tahrlsu_w | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 | - | 22;2C | - | - |
| IAHV2 | 0x5828 | STAT_SONDENHEIZUNG_PWM_VORKAT_BANK2_WERT | Tastverhältnis für Lambdasondenheizung, Bank 2 | % | tahrlsu2_w | - | unsigned integer | - | 0,0030517578125 | 1 | 0,0 | - | 22;2C | - | - |
| IAHN1 | 0x5829 | STAT_SONDENHEIZUNG_PWM_NACHKAT_BANK1_WERT | normierte Heizleistung der Lambdasonde hinter Kat | - | phlsnh | - | unsigned char | - | 0,009999999776482582 | 1 | 0,0 | - | 22;2C | - | - |
| IDRCA | 0x582B | STAT_DREHMOMENTEINGRIFF_CAN_WERT | Drehmomentaufnahme des Wandlers über CAN | % | mdwancan_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x582C_WERT | 0x582C | STAT_0x582C_WERT | Lambdasonden-Istwert | - | lamzak_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x582D_WERT | 0x582D | STAT_0x582D_WERT | Korrekturwert der LSU-Spannung vor KAT | V | kusvk_w | - | signed integer | - | 4,8828125E-4 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x582F_WERT | 0x582F | STAT_0x582F_WERT | Abgastemperatur nach KAT aus Modell | Grad C | tkatm | - | unsigned char | - | 5,0 | 1 | -50,0 | - | 22;2C | - | - |
| STAT_0x5830_WERT | 0x5830 | STAT_0x5830_WERT | Dynamikwert der LSU | - | dynlsu_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5831_WERT | 0x5831 | STAT_0x5831_WERT | Dynamikwert der LSU, Bank 2 | - | dynlsu2_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 | - | 22;2C | - | - |
| IMOST | 0x5832 | STAT_MOTOR_STATUS_WERT | Zustand Motor-Koordinator | - | CoEng_st | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5834_WERT | 0x5834 | STAT_0x5834_WERT | Umgebungsdruck von Sensor | hPa | pur_w | - | unsigned integer | - | 0,0390625 | 1 | 0,0 | - | 22;2C | - | - |
| VGENH | 0x5835 | STAT_GENERATOR_HERSTELLERCODE_WERT | Kennung Generator Hersteller | - | genmanufak | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| INGRD | 0x5836 | STAT_DREHZAHLGRADIENT_WERT | gefilterter Drehzahlgradient | 1/min/s | ngfil | - | signed char | - | 100,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5837_WERT | 0x5837 | STAT_0x5837_WERT | Solldruck Hochdrucksystem | MPa | prsoll_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5838_WERT | 0x5838 | STAT_0x5838_WERT | Relatives Moment für Aussetzererkennung | % | midmd | - | unsigned char | - | 0,390625 | 1 | 0,0 | - | 22;2C | - | - |
| ISDKN | 0x5839 | STAT_DROSSELKLAPPE_NOTLAUF_WERT | Bedingung Sicherheitskraftstoffabschaltung (SKA) | 0/1 | B_dkpu | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x583A_WERT | 0x583A | STAT_0x583A_WERT | Ansaugluft-Temperatur bei Start | Grad C | tansst | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| IKTFS | 0x583B | STAT_KRAFTSTOFFTANK_FUELLSTAND_WERT | Fuellstand Kraftstofftank | L | fstt | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x583C_WERT | 0x583C | STAT_0x583C_WERT | Batteriespannung; vom AD-Wandler erfasster Wert | V | wub | - | unsigned char | - | 0,094200000166893 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x583D_WERT | 0x583D | STAT_0x583D_WERT | Betriebsstundenzähler | min | top_w | - | unsigned integer | - | 6,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x583E_WERT | 0x583E | STAT_0x583E_WERT | Sollwert Drosselklappenwinkel, bez. auf unteren Anschlag | %DK | wdknlpr_w | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x583F_WERT | 0x583F | STAT_0x583F_WERT | Sollwert DK-Winkel, bezogen auf unteren Anschlag | %DK | wdks | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5840_WERT | 0x5840 | STAT_0x5840_WERT | DK-Winkel der Notluftposition | %DK | wdknlp_w | - | unsigned integer | - | 0,0015259021893143654 | 1 | 0,0 | - | 22;2C | - | - |
| IUSGI | 0x5841 | STAT_STEUERGERAETE_INNENTEMPERATUR_SPANNUNG_WERT | Wert Temperatur Steuergerät | V | wtsg | - | unsigned char | - | 0,01953125 | 1 | 0,0 | - | 22;2C | - | - |
| VGTYP | 0x5842 | STAT_GENERATOR_TYP_WERT | Kennung Generatortyp | - | gentypkenn | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5843_WERT | 0x5843 | STAT_0x5843_WERT | Bedingung Startanforderung | 0/1 | B_staanf | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| ITGEE | 0x5844 | STAT_GENERATOR_ELEKTRONIKTEMPERATUR | Chiptemperatur Generator 1 | Grad C | tchip | - | unsigned char | - | 1,0 | 1 | -40,0 | - | 22;2C | - | - |
| IUSV1 | 0x5845 | STAT_SONDENSPANNUNG_VORKAT_WERT | Sondenspannung vor Kat einer Breitbandlambdasonde (ADC-Wert) | V | uulsuv_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| IUPW1 | 0x5846 | STAT_PWG1_SPANNUNG_WERT | Spannung PWG-Poti 1 (Word) | V | upwg1_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| IUPW2 | 0x5847 | STAT_PWG2_SPANNUNG_WERT | Spannung PWG-Poti 2 (Word) | V | upwg2_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| IUSN1 | 0x5849 | STAT_SONDENSPANNUNG_NACHKAT_WERT | ADC-Spannung Lambdasonde hinter Katalysator (Word) | V | ushk_w | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 | - | 22;2C | - | - |
| IUSN2 | 0x584B | STAT_SONDENSPANNUNG_NACHKAT_BANK2_WERT | ADC-Spannung Lambdasonde hinter Katalysator Bank2 (Word) | V | ushk2_w | - | unsigned integer | - | 0,0048828125 | 1 | -1,0 | - | 22;2C | - | - |
| IUDK2 | 0x584C | STAT_DK2_SPANNUNG_WERT | Spannung DK-Poti 2 | V | udkp2_w | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 | - | 22;2C | - | - |
| SQTEK | 0x584D | STAT_TANKENTLUEFTUNG_DURCHFLUSS_SOLL_WERT | Massenstrom Tankentlüftung in das Saugrohr | kg/h | mste_w | - | unsigned integer | - | 3,906250058207661E-4 | 1 | 0,0 | - | 22;2C | - | - |
| IUDK1 | 0x584E | STAT_DK1_SPANNUNG_WERT | Spannung DK-Poti 1 | V | udkp1_w | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x584F_WERT | 0x584F | STAT_0x584F_WERT | Erkennung Bordnetzinstabilität | - | statbnserr | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| IUKUM | 0x5850 | STAT_KUEHLMITTELTEMPERATUR_SPANNUNG_WERT | Signalspannung des Kühlmitteltemperatursensor | V | utcw_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| IULMM | 0x5851 | STAT_LUFTMASSE_WERT | Spannungswert des Ansauglufttemperatursensors tfa2 (SY_TFAKON &gt; 0) | V | wtfa2_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5852_WERT | 0x5852 | STAT_0x5852_WERT | Batteriestrom vom IBS | A | iibsl_w | - | unsigned integer | - | 0,019999999552965164 | 1 | -200,0 | - | 22;2C | - | - |
| STAT_0x5853_WERT | 0x5853 | STAT_0x5853_WERT | Batteriespannung von IBS | V | uibsl_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5854_WERT | 0x5854 | STAT_0x5854_WERT | Batterietemperatur vom IBS | Grad C | tibsl | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| STAT_0x5855_WERT | 0x5855 | STAT_0x5855_WERT | schneller Mittelwert des Lambdaregelfaktors (Word) | - | frm_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5856_WERT | 0x5856 | STAT_0x5856_WERT | schneller Mittelwert des Lambdaregelfaktors Bank 2(Word) | - | frm2_w | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| IIEGE | 0x5857 | STAT_0x5857_WERT | Erregerstrom Generator 1 | A | ierr | - | unsigned char | - | 0,125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5858_WERT | 0x5858 | STAT_0x5858_WERT | Drosselklappenwinkel bezogen auf unteren Anschlag | %DK | wdkba | - | unsigned char | - | 0,3921568691730499 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5859_WERT | 0x5859 | STAT_0x5859_WERT | Pumpenstrom Referenzleck | mA | iptrefr_w | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x585A_WERT | 0x585A | STAT_0x585A_WERT | min. Pumpenstrom bei Grobleckmessung | mA | iptglmn_w | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x585B_WERT | 0x585B | STAT_0x585B_WERT | Pumpenstrom am Ende der Feinstleckmessung | mA | iptkl_w | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 | - | 22;2C | - | - |
| IRLN1 | 0x585C | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT1_OBERES_BYTE_WERT | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT | Ohm | rinh_w | - | unsigned char | - | 512,0 | 1 | 0,0 | - | 22;2C | - | - |
| IRLN2 | 0x585D | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT2_OBERES_BYTE_WERT | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT Bank2 | Ohm | rinh2_w | - | unsigned char | - | 512,0 | 1 | 0,0 | - | 22;2C | - | - |
| IRUN1 | 0x585E | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT1_UNTERES_BYTE_WERT | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT | Ohm | rinh_w | - | unsigned char | - | 2,0 | 1 | 0,0 | - | 22;2C | - | - |
| IRUN2 | 0x585F | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT2_UNTERES_BYTE_WERT | Istwert (word) Innenwiderstand Ri-Nernstzelle der Lambdasonde hinter KAT Bank2 | Ohm | rinh2_w | - | unsigned char | - | 2,0 | 1 | 0,0 | - | 22;2C | - | - |
| IRLV1 | 0x5860 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT1_WERT | Innenwiderstand der Nernstzelle der LSU | Ohm | rinlsu_w | - | unsigned char | - | 10,0 | 1 | 0,0 | - | 22;2C | - | - |
| IRLV2 | 0x5861 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT2_WERT | Innenwiderstand der Nernstzelle der LSU, Bank 2 | Ohm | rinlsu2_w | - | unsigned char | - | 10,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5862_WERT | 0x5862 | STAT_0x5862_WERT | Sollwert Öldruck | kPa | poels_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| IRUV1 | 0x5863 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT1_UNTERES_BYTE_WERT | Innenwiderstand der Nernstzelle der LSU | Ohm | rinlsu_w | - | unsigned char | - | 0,0390625 | 1 | 0,0 | - | 22;2C | - | - |
| IRUV2 | 0x5864 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT2_UNTERES_BYTE_WERT | Innenwiderstand der Nernstzelle der LSU, Bank 2 | Ohm | rinlsu2_w | - | unsigned char | - | 0,0390625 | 1 | 0,0 | - | 22;2C | - | - |
| IMLOE | 0x5865 | STAT_OELSTAND_LANGZEIT_MITTEL_WERT | Langzeit-Ölniveau-Mittelwert für den DIS-Tester | - | oznivlangt | - | unsigned char | - | 0,29296875 | 1 | 0,0 | - | 22;2C | - | - |
| IFSOE | 0x5866 | STAT_FUELLSTAND_MOTOROEL_WERT | Relativer Füllstand des Motoröls | - | oelstandr | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5867_WERT | 0x5867 | STAT_0x5867_WERT | Fahrstrecke des Fahrzeugs als Information über CAN | km | kmstand | - | unsigned integer | - | 10,0 | 1 | 0,0 | - | 22;2C | - | - |
| ISSR1 | 0x5868 | STAT_STANDVERBRAUCHER_REGISTRIERT_TEIL1_WERT | Status Standverbraucher registriert Teil 1 | - | statsvreg1 | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| ISSR2 | 0x5869 | STAT_STANDVERBRAUCHER_REGISTRIERT_TEIL2_WERT | Status Standverbraucher registriert Teil 2 | - | statsvreg2 | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| IUIBS | 0x586A | STAT_UBATT_IBS_WERT | aktuelle Batteriespannung | V | ubatt_w | - | unsigned integer | - | 2,500000118743628E-4 | 1 | 6,0 | - | 22;2C | - | - |
| IZR82 | 0x586B | STAT_ZEIT_MIT_RUHESTROM_80_200_WERT | Zeit, indem der Ruhestrom bei 80..200mA liegt | min | t2hstshort | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 | - | 22;2C | - | - |
| IZR21 | 0x586C | STAT_ZEIT_MIT_RUHESTROM_200_1000_WERT | Zeit, indem der Ruhestrom bei 200..1000mA liegt | min | t3hstshort | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 | - | 22;2C | - | - |
| IZRG1 | 0x586E | STAT_ZEIT_MIT_RUHESTROM_GROESER_1000_WERT | Zeit, indem der Ruhestrom größer als 1000mA liegt | min | t4hstshort | - | unsigned char | - | 14,933333396911621 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x586F_WERT | 0x586F | STAT_0x586F_WERT | Öldruck | hPa | poel_w | - | signed integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| IUUMG | 0x5870 | STAT_UMGEBUNGSDRUCK_SPANNUNG_WERT | Spannung Umgebungsdrucksensor (word 10-Bit von ADC) | V | udsu_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5871_WERT | 0x5871 | STAT_0x5871_WERT | Zähler Prüfzustand für DVESTANZNMOT | - | dvestanznmotctr | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| VGENR | 0x5872 | STAT_GENERATOR_REGLERVERSION_WERT | Reglerversion on Generator 1 | - | bsdgenregv | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| SLAG2 | 0x5873 | STAT_LAMBDA_SOLLWERT_GRUPPE2_WERT | Lambda-Sollwert bezogen auf Einbauort Lambda-Sensor Bank2 | - | lamsons2_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5874_WERT | 0x5874 | STAT_0x5874_WERT | ADC-Spannung Pumpenstrom Tankdiagnose | V | urptes_w | - | unsigned integer | - | 0,001220703125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5875_WERT | 0x5875 | STAT_0x5875_WERT | Soll-Motormoment MSR für schnellen Eingriff | Nm | mdradmsrs_w | - | signed integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5876_WERT | 0x5876 | STAT_0x5876_WERT | Schnittstelle für Scan Tool Mode $01/$02 Raildruck Rohwert | MPa | prrohr_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 | - | 22;2C | - | - |
| ILRR1 | 0x5878 | STAT_LAMBDAVERSCHIEBUNG_RUECKFUEHRREGLER1_WERT | I-Anteil der stetigen LRSHK Variante kontinuierlich | - | dlahi_w | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x587C_WERT | 0x587C | STAT_0x587C_WERT | Periodendauer des Nullgangsensorsignals | ms | GbxNPos_tiPwmPer | - | unsigned integer | - | 9,999999747378752E-5 | 1 | 0,0 | - | - | - | - |
| STAT_0x587D_WERT | 0x587D | STAT_0x587D_WERT | Status Nullgangsensor | - | stngang | - | unsigned char | - | 1,0 | 1 | 0,0 | - | - | - | - |
| IELTV | 0x587F | STAT_E_LUEFTER_TASTVERHAELTNIS_WERT | Tastverhältnis E-Lüfter | % | taml | - | unsigned char | - | 0,390625 | 1 | 0,0 | - | 22;2C | - | - |
| SBEGA | 0x5881 | STAT_BERECHNETER_GANG_WERT | Ist-Gang | - | gangi | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| ITMOS | 0x5882 | STAT_MOTORTEMPERATUR_BEIM_START_WERT | Motorstarttemperatur | Grad C | tmst | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| STAT_0x5883_WERT | 0x5883 | STAT_0x5883_WERT | Referenzpegel Klopfregelung, 16 bit | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5884_WERT | 0x5884 | STAT_0x5884_WERT | Kopie begrenzter Erregerstrom Generator 1 | A | ierrfgrenz | - | unsigned char | - | 0,125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5885_WERT | 0x5885 | STAT_0x5885_WERT | Referenzpegel Klopfregelung, 16bit | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5886_WERT | 0x5886 | STAT_0x5886_WERT | Referenzpegel Klopfregelung, 16bit | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| IGENA | 0x5887 | STAT_0x5887_WERT | Auslastungsgrad Generator 1 | % | dfsiggen | - | unsigned char | - | 0,390625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5888_WERT | 0x5888 | STAT_0x5888_WERT | Referenzpegel Klopfregelung, 16bit | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| ILAG1 | 0x5889 | STAT_LAMBDA_ISTWERT_GRUPPE1_WERT | Lambda-Istwert | - | lamsoni_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 | - | 22;2C | - | - |
| ILAG2 | 0x588A | STAT_LAMBDA_ISTWERT_GRUPPE2_WERT | Lambda-Istwert Bank2 | - | lamsoni2_w | - | unsigned integer | - | 2,44140625E-4 | 1 | 0,0 | - | 22;2C | - | - |
| IZSSE | 0x588B | STAT_ZEIT_SEIT_STARTENDE_WERT | Zeit nach Startende | s | tnst_w | - | unsigned integer | - | 0,009999999776482582 | 1 | 0,0 | - | 22;2C | - | - |
| ITKV1 | 0x588C | STAT_LAMBDASONDE_KERAMIKTEMPERATUR_VORKAT1_WERT | Keramiktemperatur der LSU | Grad C | tkerlsu_w | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 | - | 22;2C | - | - |
| IZDML | 0x588D | STAT_ZEIT_DMTL_LECKMESSUNG_WERT | aktuelle Zeit Leckmessung | s | tdmlka_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| IIDMP | 0x588E | STAT_PUMPENSTROM_BEI_DMTL_PUMPENPRUEFUNG_WERT | Pumpenstrom Tankdiagnose | mA | iptes_w | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 | - | 22;2C | - | - |
| ITKV2 | 0x588F | STAT_LAMBDASONDE_KERAMIKTEMPERATUR_VORKAT2_WERT | Keramiktemperatur der LSU, Bank 2 | Grad C | tkerlsu2_w | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 | - | 22;2C | - | - |
| IMOKU | 0x5891 | STAT_MOMENTANFORDERUNG_KUPPLUNG_WERT | Kupplungsmotormoment Istwert | Nm | mkist_w | - | signed integer | - | 0,5 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5892_WERT | 0x5892 | STAT_0x5892_WERT | Differenz zwischen Umgebungsdruck und  Bremskraftverstärker-Druck von Drucksensor (Rohwert) | hPa | dpbkvur_w | - | signed integer | - | 0,0390625 | 1 | 0,0 | - | 22;2C | - | - |
| IDMGW | 0x5893 | STAT_DREHMOMENTABFALL_BEIM_GANGWECHSEL_WERT | Indiziertes Soll-Motormoment GS für schnellen Eingriff | % | migs_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5894_WERT | 0x5894 | STAT_0x5894_WERT | Spannung Klopfwerte Zylinder 2 | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5895_WERT | 0x5895 | STAT_0x5895_WERT | Spannung Klopfwerte Zylinder 5 | V | rkr_w | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x5896_WERT | 0x5896 | STAT_0x5896_WERT | Abgastemperatur hinter Hauptkat aus Modell | Grad C | tanhkm_w | - | unsigned integer | - | 0,0234375 | 1 | -273,1499938964844 | - | 22;2C | - | - |
| SUGEN | 0x5898 | STAT_GENERATOR_SPANNUNG_SOLL_WERT | phys. Wert Generatorsollspannung (Volt) für Komponententreiber Generator | V | ugen | - | unsigned char | - | 0,10000000149011612 | 1 | 10,6 | - | 22;2C | - | - |
| STAT_0x5899_WERT | 0x5899 | STAT_0x5899_WERT | Bedingung Anforderung Motorrelais einschalten | 0/1 | B_amtr | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x589A_WERT | 0x589A | STAT_0x589A_WERT | Tastverhältnis Nullgangsensor | % | tngang_w | - | unsigned integer | - | 0,009999999776482582 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x589B_WERT | 0x589B | STAT_0x589B_WERT | Bedingung unzulössig hoher Motorstrom bei Kurzschluss erkannt | 0/1 | B_ivvtkse | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x589C_WERT | 0x589C | STAT_0x589C_WERT | Bedingung Freigabe VVT-Endstufe | 0/1 | B_vvten | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x589E_WERT | 0x589E | STAT_0x589E_WERT | Sollwert Exzenterwinkel VVT | Grad | exwinks_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x589F_WERT | 0x589F | STAT_0x589F_WERT | Batterietemperatur | Grad C | tbatt | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| STAT_0x58A0_WERT | 0x58A0 | STAT_0x58A0_WERT | Entladung während Ruhestromverletzung | Ah | qiruhe2_w | - | unsigned integer | - | 0,018204445019364357 | 1 | 0,0 | - | 22;2C | - | - |
| ISKME | 0x58A1 | STAT_KILOMETERSTAND_WERT | Wegstrecke_km auf 1km genau | - | kmstand_l | - | unsigned long | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58A2_WERT | 0x58A2 | STAT_0x58A2_WERT | Istwert Exzenterwinkel VVT | Grad | exwnki_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58A3_WERT | 0x58A3 | STAT_0x58A3_WERT | rel. Exzenterwinkel am oberen mech. Anschlag | Grad | exwnkoar_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58A4_WERT | 0x58A4 | STAT_0x58A4_WERT | Generatorstatus | - | st_gen | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58A5_WERT | 0x58A5 | STAT_0x58A5_WERT | Vom Generator empfangenes Lastsignal | % | dffgen | - | unsigned char | - | 0,390625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58A6_WERT | 0x58A6 | STAT_0x58A6_WERT | Rel. Exzenterwinkel | Grad | exwnkr_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58A7_WERT | 0x58A7 | STAT_0x58A7_WERT | Abstellzeit aus relativem Minutenzähler bis Motorstart | min | tabsmn_w | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| IZMAB | 0x58A8 | STAT_MOTORABSTELLZEIT_WERT | Rel. Exzenterwinkel am unteren mech. Anschlag | Grad | exwnkuar_w | - | signed integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58A9_WERT | 0x58A9 | STAT_0x58A9_WERT | VVT Verstellbereich aus Urlernvorgang | Grad | exwnkvb_ur_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58AA_WERT | 0x58AA | STAT_0x58AA_WERT | Verstellbereich des Exzenterwinkels | Grad | exwnkvb_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58AB_WERT | 0x58AB | STAT_0x58AB_WERT | DLR für DV-E: Summe der PID-Anteile | % | dlrspid_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| IPWG1 | 0x58AD | STAT_PEDALWERTGEBER1_WERT | Sauerstoffspeichervermögen KAT | mg | oscdktt_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58AE_WERT | 0x58AE | STAT_0x58AE_WERT | Peridendauer für Massenstrom aus HFM | us | tpmshfm_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| IKRAN | 0x58AF | STAT_KRAFTSTOFF_ANFORDERUNG_AN_PUMPE_WERT | EKP-Sollvolumenstrom | l | vssekp | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| IDKAD | 0x58B0 | STAT_DK_ADAPTIONSSCHRITT_WERT | Zähler für Lerndauer eines Lernsteps | - | lrnstep_c | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| IZFZ1 | 0x58B1 | STAT_FUNKENBRENNDAUER_ZYL1_WERT | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 1 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 | - | 22;2C | - | - |
| IZFZ5 | 0x58B2 | STAT_FUNKENBRENNDAUER_ZYL5_WERT | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 5 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 | - | 22;2C | - | - |
| IZFZ3 | 0x58B3 | STAT_FUNKENBRENNDAUER_ZYL3_WERT | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 3 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 | - | 22;2C | - | - |
| IZFZ6 | 0x58B4 | STAT_FUNKENBRENNDAUER_ZYL6_WERT | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 6 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 | - | 22;2C | - | - |
| IZFZ2 | 0x58B5 | STAT_FUNKENBRENNDAUER_ZYL2_WERT | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 2 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 | - | 22;2C | - | - |
| IZFZ4 | 0x58B6 | STAT_FUNKENBRENNDAUER_ZYL4_WERT | Diagnose Zuendung: Brenndauer des Zuendfunkens aus dem HW-nahen SW-RAM, Zylinder 4 | ms | dztbd_w | - | unsigned integer | - | 0,0010000000474974513 | 1 | 0,0 | - | 22;2C | - | - |
| IPBRE | 0x58B7 | STAT_BREMSDRUCK_WERT | aktueller Bremsdruck | hPa | pbrems | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58B8_WERT | 0x58B8 | STAT_0x58B8_WERT | Motordrehzahl in der Funktionsüberwachung | 1/min | MoF_nEng | - | unsigned char | - | 40,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58B9_WERT | 0x58B9 | STAT_0x58B9_WERT | Pedalsollwert (8 Bit) in der Funktionsüberwachung | V | MoF_uAPP | - | unsigned char | - | 0,01953125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58BA_WERT | 0x58BA | STAT_0x58BA_WERT | Bank mittel eingespritzte effektive relative Krafftstoffmasse (inkl. Reduzierstufe) | % | rkmeeff_w | - | unsigned integer | - | 0,046875 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58BB_WERT | 0x58BB | STAT_0x58BB_WERT | Strom für VVT-Motor | A | ivvtm_w | - | signed integer | - | 0,006103515625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58BC_WERT | 0x58BC | STAT_0x58BC_WERT | relative Luftfüllung in der Funktionsüberwachung | % | rl_um | - | unsigned char | - | 0,75 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58BD_WERT | 0x58BD | STAT_0x58BD_WERT | Status Fehler Überlast VVT1 | - | stdvovrld | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58BE_WERT | 0x58BE | STAT_0x58BE_WERT | DV-E-Adaption: Status Prüfbedingungen | - | dveadchst | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58C0_WERT | 0x58C0 | STAT_0x58C0_WERT | VVT-Endstufentemperatur aus Modell | Grad C | tvvtes_w | - | unsigned integer | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| ITLSZ | 0x58C1 | STAT_LAUFUNRUHE_SEGMENTZEIT_WERT | Korrigierte Segmentdauer | us | tsk_l | - | unsigned long | - | 0,05000000074505806 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58C2_WERT | 0x58C2 | STAT_0x58C2_WERT | Status STG Anforderung Radmoment Antriebsstrang Summe FAS | - | Com_stTrqWhlDemFASQl_FX | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58C3_WERT | 0x58C3 | STAT_0x58C3_WERT | Status STG Anforderung Drehmoment Kurbelwelle Fahrdynamik | - | Com_stDrvDyn_FX | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58C4_WERT | 0x58C4 | STAT_0x58C4_WERT | Status STG Anforderung Radmoment Antriebsstrang Summe Stabilisierung | - | Com_stEcuRqTrqSumStab_FX | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58C5_WERT | 0x58C5 | STAT_0x58C5_WERT | Status STG ist Bremsmoment Summe | - | Com_stEcuBrkTrqSum_FX | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58C6_WERT | 0x58C6 | STAT_0x58C6_WERT | Status STG ist Lenkwinkel Vorderachse | - | Com_stEcuAvlSteaFtax_FX | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58C7_WERT | 0x58C7 | STAT_0x58C7_WERT | Status STG Status Stabilisierung DSC | - | Com_stECUStStabDSC_FX | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58C8_WERT | 0x58C8 | STAT_0x58C8_WERT | geforderte Drehmomentänderung von der LLR (I-Anteil) | % | dmllri_w | - | signed integer | - | 0,0030517578125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58C9_WERT | 0x58C9 | STAT_0x58C9_WERT | vvtmode | - | vvtmode | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58CA_WERT | 0x58CA | STAT_0x58CA_WERT | geforderte MD-Änderung von der LLR (PD-Zündungsanteil) | % | dmllrz_w | - | signed integer | - | 0,0030517578125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58CB_WERT | 0x58CB | STAT_0x58CB_WERT | PD-Anteil schnell Leerlaufregelung | - | dvvttempovl | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58CC_WERT | 0x58CC | STAT_0x58CC_WERT | Verlustmoment Überwachung | % | tvvvtm_w | - | signed integer | - | 0,0030517578125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58CD_WERT | 0x58CD | STAT_0x58CD_WERT | Verlustmomentabweichung Überwachung | V | umtr | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58CE_WERT | 0x58CE | STAT_0x58CE_WERT | Carrierbyte Schalterstati | - | funst_w | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| SMOMO | 0x58CF | STAT_MOTORMOMENT_SOLL_WERT | Soll- Motormoment aus Getriebeüberwachung in der Funktionsüberwachung | Nm | MoF_trqClthTra16 | - | signed integer | - | 0,0625 | 1 | 0,0 | - | 22;2C | - | - |
| IMOMO | 0x58D0 | STAT_MOTORMOMENT_IST_WERT | Berechnetes Ist-Moment in der Funktionsüberwachung | % | MoF_rTrqInrAct | - | unsigned char | - | 0,390625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58D0_WERT | 0x58D1 | STAT_0x58D0_WERT | Massenstrom Abgas ohne Kraftstoffanteil vor Hauptkatalysator | kg/h | msaovhk_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58D2_WERT | 0x58D2 | STAT_0x58D2_WERT | Luftklappe - Sollposition in Grad | - | RadSht_phiPosDes | - | unsigned char | - | 0,501960813999176 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58D3_WERT | 0x58D3 | STAT_0x58D3_WERT | Luftklappe - Istposition in Grad | - | RadSht_phiPos | - | unsigned char | - | 0,501960813999176 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58D4_WERT | 0x58D4 | STAT_0x58D4_WERT | Startbedingung Kraftschluss erfüllt | 0/1 | B_kupp1 | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |
| STAT_0x58D5_WERT | 0x58D5 | STAT_0x58D5_WERT | physikalischer Temperaturwert, der sich bei Wandlung der elektrischen Sensorspannung wtfa1_w ergibt | Grad C | tfa1lin | - | unsigned char | - | 0,75 | 1 | -48,0 | - | 22;2C | - | - |
| IUANS | 0x58D7 | STAT_ANSAUGLUFTTEMPERATUR_SPANNUNG_WERT | Spannungswert des Ansauglufttemperatursensors tfa1 | V | wtfa1_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58D8_WERT | 0x58D8 | STAT_0x58D8_WERT | Differenz-DK-Winkel Sollwert - Istwert | %DK | dwdkdlr_w | - | signed integer | - | 0,0244140625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58D9_WERT | 0x58D9 | STAT_0x58D9_WERT | Schrittzähler DK-Rückstellfeder-Prüfung | - | fprstep_c | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58DA_WERT | 0x58DA | STAT_0x58DA_WERT | koordiniertes Moment für Füllung | % | milsol_w | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58DB_WERT | 0x58DB | STAT_0x58DB_WERT | Fehlerzähler abgasrelevante Aussetzer über alle Zylinder | - | fzabgs_w | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58DC_WERT | 0x58DC | STAT_0x58DC_WERT | Intervallzähler für abgasrelevante Aussetzer | - | ivzabg_w | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58DD_WERT | 0x58DD | STAT_0x58DD_WERT | Druck vor Drosselklappe Rohwert | hPa | pvdr_w | - | unsigned integer | - | 0,078125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58DE_WERT | 0x58DE | STAT_0x58DE_WERT | Spannung Drucksensor vor Drosselklappe | V | udsvd_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58E0_WERT | 0x58E0 | STAT_0x58E0_WERT | Abgleich DK-Modell (Faktor) | - | eisydkfkaf | - | unsigned char | - | 0,0078125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58E1_WERT | 0x58E1 | STAT_0x58E1_WERT | Abgleich DK-Modell (Offset) | kg/h | eisydkkoff | - | signed char | - | 8,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58E2_WERT | 0x58E2 | STAT_0x58E2_WERT | Abgleich EV-Modell (Faktor) | - | eisyevfkaf | - | unsigned char | - | 0,0078125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58E3_WERT | 0x58E3 | STAT_0x58E3_WERT | Abgleich EV-Modell (Offset) | kg/h | eisyevkoff | - | signed char | - | 8,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58E4_WERT | 0x58E4 | STAT_0x58E4_WERT | Ist-Betriebsart | - | opmodi | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| IUWAP | 0x58E9 | STAT_WASSERPUMPE_SPANNUNG_WERT | empf. Spannung von BSS-Wasserpumpe | V | wmu | - | unsigned char | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| INWAP | 0x58EA | STAT_WASSERPUMPE_DREHZAHL_WERT | empf. Istdrehzahl von BSS-Wasserpumpe | 1/min | wmpdzi | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| ITWAE | 0x58EC | STAT_WASSERPUMPE_ELEKTRONIK_TEMPERATUR_WERT | empf. Temperatur von BSS-Wasserpumpe | Grad C | wmt | - | unsigned char | - | 1,0 | 1 | -50,0 | - | 22;2C | - | - |
| IIWAP | 0x58ED | STAT_WASSERPUMPE_STROM_WERT | empf. Strom von BSS-Wasserpumpe | % | wmi | - | unsigned char | - | 0,5 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58EF_WERT | 0x58EF | STAT_0x58EF_WERT | Gefilterter Raildruck-Istwert (Absolutdruck) | MPa | prist_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58F0_WERT | 0x58F0 | STAT_0x58F0_WERT | ungefilterter Raildruck Istwert (abs.) | MPa | prroh_w | - | unsigned integer | - | 5,000000237487257E-4 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58F2_WERT | 0x58F2 | STAT_0x58F2_WERT | Tastverhältnis Mengensteuerventil | % | PWM_VCV | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58F3_WERT | 0x58F3 | STAT_0x58F3_WERT | Ungefilterter Niederdruck Rohwert | kPa | pistndr_w | - | unsigned integer | - | 0,10000000149011612 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58F4_WERT | 0x58F4 | STAT_0x58F4_WERT | Spannung Kraftstoffniederdrucksensor im 1 ms Raster | V | upnd1ms_w | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58F5_WERT | 0x58F5 | STAT_0x58F5_WERT | Spannung Diagnose-Port VVT-Ansteuerung (3V ADC) | V | uvvtdia3V | - | unsigned char | - | 0,012890624813735485 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58F6_WERT | 0x58F6 | STAT_0x58F6_WERT | Sollspannung des VVT Lagereglers | V | uvvtlrs_w | - | signed integer | - | 7,812500116415322E-4 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58F7_WERT | 0x58F7 | STAT_0x58F7_WERT | VVT-Strom | - | vvtipl | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58FA_WERT | 0x58FA | STAT_0x58FA_WERT | gefilterter Faktor Tankentlüftungs-Adaption | - | fteadf | - | signed char | - | 0,5 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58FC_WERT | 0x58FC | STAT_0x58FC_WERT | Fertigungs-Werkstatt-,Transportmodus | - | fetrawemod | - | unsigned char | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| STAT_0x58FD_WERT | 0x58FD | STAT_0x58FD_WERT | Untermodi des Fe Tra Fla Mode | - | fetraflamod | - | unsigned integer | - | 1,0 | 1 | 0,0 | - | 22;2C | - | - |
| - | 0x58FF | - | Umweltbedingung unbekannt | - | - | - | unsigned char | - | 1 | 1 | 0 | - | 22;2C | - | - |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 18 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler momentan vorhanden und bereits gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler momentan vorhanden und bereits gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler momentan vorhanden und bereits gespeichert |
| 0x44 | Fehler gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler gespeichert |
| 0x4D | Fehler gespeichert |
| 0x10 | Testbedingungen erfüllt |
| 0x11 | Testbedingungen noch nicht erfüllt |
| 0x80 | Fehler würde kein Aufleuchten einer Warnlampe verursachen |
| 0x81 | Fehler würde das Aufleuchten einer Warnlampe verursachen |
| 0xFF | unbekannte Fehlerart |

<a id="table-statclientauthtxt"></a>
### STATCLIENTAUTHTXT

Dimensions: 4 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0x00 | Freigabe von Zuendung und Einspritzung (noch) nicht erteilt (noch nicht versucht oder Kommunikation gestört, Motorlauf gesperrt) |
| 0x01 | Freigabe von Zuendung und Einspritzung erteilt (Challenge-Response erfolgreich) |
| 0x02 | Freigabe von Zuendung und Einspritzung abgelehnt (Challenge-Response fehlgeschlagen, falsche Response, Kommunikation i.O.) |
| 0x03 | nicht definiert |

<a id="table-statfreesktxt"></a>
### STATFREESKTXT

Dimensions: 3 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0xFE | Ablage unbegrenzt |
| 0xFF | ungültig |
| 0xXY | freie Ablagen |

<a id="table-statewsvertxt"></a>
### STATEWSVERTXT

Dimensions: 3 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0x01 | Direktschreiben des SecretKey |
| 0x02 | Direktschreiben des SecretKey und DH-Abgleich |
| 0xXY | unbekannt |

<a id="table-t-1bit-switch-position-high-byte-bit4-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Lambdaregelung vor Katalysator Bank 2 nicht aktiv |
| 1 | Lambdaregelung vor Katalysator Bank 2 aktiv |

<a id="table-t-st-atlsvc-pvdk-dop"></a>
### T_ST_ATLSVC_PVDK_DOP

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Ladedruckdiagnose ohne Ergebnis |
| 1 | Ladedruck fehlerfrei |
| 2 | Gesamtladedruck zu niedrig |
| 3 | Turbolader 1 mit Ladedruckfehler |
| 4 | Turbolader 2 mit Ladedruckfehler |
| 5 | Gesamtladedruck zu niedrig, Bank nicht identifiziert |

<a id="table-t-b-bzdon-dop"></a>
### T_B_BZDON_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine BZE3 |
| 1 | BZE3 |

<a id="table-t-1bit-switch-position-low-byte-bit2-dop"></a>
### T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Kickdown erkannt |
| 1 | Kickdown erkannt |

<a id="table-t-1bit-state-ready-obd-2-bit2-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-geniutest-err-bit2-dop"></a>
### T_1BIT_GENIUTEST_ERR_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Generatortest, Hochtemperaturfehler Generator nicht vorhanden |
| 1 | Generatortest, Hochtemperaturfehler Generator vorhanden |

<a id="table-t-1bit-state-ready-obd-1-bit6-dop"></a>
### T_1BIT_STATE_READY_OBD_1_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-switch-position-bit2-dop"></a>
### T_1BIT_SWITCH_POSITION_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kupplung aus |
| 1 | Kupplung ein |

<a id="table-t-1bit-geniutest-err-bit7-dop"></a>
### T_1BIT_GENIUTEST_ERR_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorregler plausibel |
| 1 | Generatortest, Generatorregler unplausibel |

<a id="table-t-1bit-state-ready-obd-1-bit0-dop"></a>
### T_1BIT_STATE_READY_OBD_1_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-geniutest-err-bit3-dop"></a>
### T_1BIT_GENIUTEST_ERR_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Generatortest, Generatortyp plausibel |
| 1 | Generatortest, Generatortyp unplausibel |

<a id="table-t-1bit-c-state-ready-obd-2-bit2-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-fs-erw-vvtl-bit4-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 4 - Fehler zulaessige Hoechstzeit Anschlaglernvorgang ueberschritten |
| 1 | Bit 4 - Fehler zulaessige Hoechstzeit Anschlaglernvorgang ueberschritten |

<a id="table-t-1bit-fs-erw-vvtl-bit5-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT5_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 5 - Fehler Spannungsversorgung |
| 1 | Bit 5 - Fehler Spannungsversorgung |

<a id="table-t-1bit-state-ready-obd-1-bit4-dop"></a>
### T_1BIT_STATE_READY_OBD_1_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-b-bzd-wrgbat-dop"></a>
### T_B_BZD_WRGBAT_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Wechsel zulaessig |
| 1 | Wechsel unzulaessig |

<a id="table-t-bzd-btzust-dop"></a>
### T_BZD_BTZUST_DOP

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Batterie i.O. |
| 1 | Batterie pruefen |
| 2 | Batterie nicht i.O. |
| 3 | ungueltig |

<a id="table-t-state-dmtl-dop"></a>
### T_STATE_DMTL_DOP

Dimensions: 21 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | START |
| 1 | Referenzleck Messung |
| 2 | Grobleck Messung |
| 3 | Feinleck Messung |
| 4 | Zweite Referenzleck Messung |
| 6 | Diagnose beendet |
| 10 | Funktion nicht Startbar |
| 11 | Batteriespannung ausserhalb Bereich |
| 12 | Schwankung von Referenzstrom zu groß |
| 13 | Elektrischer Fehler vorhanden |
| 14 | Max. Diagnosezeit erreicht/ueberschritten |
| 15 | Kein Freigabe TEV Aktiv |
| 20 | Funktion wurde Abgebrochen |
| 23 | Spannungsschwankung zu groß |
| 24 | Zündung an |
| 30 | Funktion beendet: Tank Dicht |
| 31 | Funktion beendet: Feinleck erkannt |
| 32 | Funktion beendet: Grobleck erkannt |
| 33 | Funktion beendet: Modulfehler |
| 34 | Funktion beendet: Kein Grobleck erkannt |
| 255 | Funktion noch nicht gestartet |

<a id="table-t-1bit-c-state-ready-obd-2-bit4-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-c-state-ready-obd-2-bit6-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-state-ready-obd-2-bit7-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-switch-position-bit0-dop"></a>
### T_1BIT_SWITCH_POSITION_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Klemme-15 aus |
| 1 | Klemme-15 ein |

<a id="table-t-st-atlsvc-dop"></a>
### T_ST_ATLSVC_DOP

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
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

<a id="table-t-1bit-switch-position-bit3-dop"></a>
### T_1BIT_SWITCH_POSITION_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bremslichtschalter-Kanal 1 aus |
| 1 | Bremslichtschalter-Kanal 1 ein |

<a id="table-t-1bit-switch-position-high-byte-bit6-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Regelkreis Bank 2 nicht geschlossen |
| 1 | Regelkreis Bank 2 geschlossen |

<a id="table-t-1bit-c-state-ready-obd-2-bit7-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-b-vvtnotl-dop"></a>
### T_B_VVTNOTL_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | 0 |
| 1 | 1 |

<a id="table-t-1bit-switch-position-high-byte-bit7-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Regelkreis Bank 1 nicht geschlossen |
| 1 | Regelkreis Bank 1 geschlossen |

<a id="table-t-1byte-fs-ddlhk-dop"></a>
### T_1BYTE_FS_DDLHK_DOP

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Open Loop - Start-/Ansteuerbedingung für Regelung nicht erfüllt |
| 1 | Closed Loop - Lambdaregelung-Diagnose |
| 2 | Open Loop - Keine Regelung durch Fahrzustand. Gemisch zu fett/mager |
| 3 | Open Loop - Fehler erkannt |
| 4 | Closed Loop - Min. eine Lambdasonde fehlerhaft. U.u. in Einzelbetrieb. |
| 5 | Ungültiger Wert |

<a id="table-t-1bit-switch-position-high-byte-bit0-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Leerlauf |
| 1 | Leerlauf |

<a id="table-t-1bit-fs-erw-vvtl-bit7-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 7 - Ruecknahme Lernanforderung |
| 1 | Bit 7 - Ruecknahme Lernanforderung |

<a id="table-t-1bit-switch-position-low-byte-bit7-dop"></a>
### T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Drosselklappen-Neuabgleich erforderlich |
| 1 | Drosselklappen-Neuabgleich nicht erforderlich |

<a id="table-t-1bit-geniutest-err-bit1-dop"></a>
### T_1BIT_GENIUTEST_ERR_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Generatortest, mechanischer Fehler Generator nicht vorhanden |
| 1 | Generatortest, mechanischer Fehler Generator vorhanden |

<a id="table-t-1bit-geniutest-err-bit4-dop"></a>
### T_1BIT_GENIUTEST_ERR_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorkommunikation vorhanden |
| 1 | Generatortest, keine Generatorkommunikation vorhanden |

<a id="table-t-1bit-fs-erw-vvtl-bit3-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 3 - Fehler Verstellbereich Referenzsensor unplausibel |
| 1 | Bit 3 - Fehler Verstellbereich Referenzsensor unplausibel |

<a id="table-t-1bit-state-ready-obd-2-bit4-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-geniutest-err-bit6-dop"></a>
### T_1BIT_GENIUTEST_ERR_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Generatortest, Hochtemperaturfehler Generator aus Berechnung nicht vorhanden |
| 1 | Generatortest, Hochtemperaturfehler Generator aus Berechnung vorhanden |

<a id="table-t-1bit-geniutest-err-bit5-dop"></a>
### T_1BIT_GENIUTEST_ERR_BIT5_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorspannung aus Berechnung plausibel |
| 1 | Generatortest, Generatorspannung aus Berechnung unplausibel |

<a id="table-t-eol-ram-1-dop"></a>
### T_EOL_RAM_1__DOP

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
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

<a id="table-t-1bit-switch-position-bit4-dop"></a>
### T_1BIT_SWITCH_POSITION_BIT4_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bremslichtschalter-Kanal 2 aus |
| 1 | Bremslichtschalter-Kanal 2 ein |

<a id="table-t-st-testpoelsys2-dop"></a>
### T_ST_TESTPOELSYS2_DOP

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | -- |
| 1 | Abbruch durch Tester |
| 2 | Warmlauf (Oeltemperatur zu niedrig) |
| 3 | Abbruch aufgrund zu hoher Oeltemperatur |
| 4 | Abbruch der Diagnosefunktion nach Schritt 1 (Fehlerspeicher auslesen) |
| 5 | Abbruch der Diagnosefunktion nach Schritt 2 (Fehlerspeicher auslesen) |
| 6 | Abbruch der Diagnosefunktion nach Schritt 3 (Fehlerspeicher auslesen) |

<a id="table-t-1bit-fs-erw-vvtl-bit1-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 1 - Fehler oberer Anschlag nicht gefunden |
| 1 | Bit 1 - Fehler oberer Anschlag nicht gefunden |

<a id="table-t-1bit-fs-erw-vvtl-bit6-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 6 - Fehler VVT-Sensor, Leistungsversorgung oder Stellglied |
| 1 | Bit 6 - Fehler VVT-Sensor, Leistungsversorgung oder Stellglied |

<a id="table-t-b-qvch2o-dop"></a>
### T_B_QVCH2O_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Wasserverbrauch i.O. |
| 1 | Wasserverbrauch nicht i.O. |

<a id="table-t-1bit-state-ready-obd-2-bit3-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-state-ready-obd-2-bit1-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-c-state-ready-obd-2-bit1-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-state-ready-obd-1-bit2-dop"></a>
### T_1BIT_STATE_READY_OBD_1_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-b-bzd-te-dop"></a>
### T_B_BZD_TE_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Batterie i.O. |
| 1 | Batterie tiefentladen |

<a id="table-t-1bit-switch-position-bit1-dop"></a>
### T_1BIT_SWITCH_POSITION_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Motor laeuft |
| 1 | Motor steht |

<a id="table-t-1bit-state-ready-obd-2-bit5-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT5_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-c-state-ready-obd-2-bit3-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-state-ready-obd-2-bit6-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-st-gentest-dop"></a>
### T_ST_GENTEST_DOP

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Start-/Ansteuerbedingung nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | -- |
| 5 | Funktion laeuft |
| 6 | Funktion beendet |
| 7 | Funktion abgebrochen |

<a id="table-t-1bit-c-state-ready-obd-2-bit5-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT5_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-b-standard-1byte-lesen-0-1"></a>
### T_B_STANDARD_1BYTE_LESEN_0_1

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | 0 |
| 1 | 1 |
| 2 | Groesser 1 |

<a id="table-t-1bit-c-state-ready-obd-2-bit0-dop"></a>
### T_1BIT_C_STATE_READY_OBD_2_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

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

<a id="table-t-1bit-switch-position-low-byte-bit3-dop"></a>
### T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Gang nicht eingelegt, Park- oder Neutralstellung |
| 1 | Gang eingelegt, nicht Park- oder Neutralstellung |

<a id="table-t-1bit-state-ready-obd-1-bit1-dop"></a>
### T_1BIT_STATE_READY_OBD_1_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-t-1bit-state-ready-obd-1-bit5-dop"></a>
### T_1BIT_STATE_READY_OBD_1_BIT5_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-1bit-fs-erw-vvtl-bit0-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 0 - Fehler unterer Anschlag nicht gefunden |
| 1 | Bit 0 - Fehler unterer Anschlag nicht gefunden |

<a id="table-t-1bit-geniutest-ab-bit0-dop"></a>
### T_1BIT_GENIUTEST_AB_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorauslastung nicht zu hoch |
| 1 | Generatortest, Generatorauslastung zu hoch |

<a id="table-t-1bit-switch-position-high-byte-bit3-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT3_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Lambdaregelung hinter Katalysator Bank 2 nicht aktiv |
| 1 | Lambdaregelung hinter Katalysator Bank 2 aktiv |

<a id="table-t-1bit-switch-position-bit7-dop"></a>
### T_1BIT_SWITCH_POSITION_BIT7_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Anforderung Klimabereitschaft aus |
| 1 | Anforderung Klimabereitschaft ein |

<a id="table-t-s-vsmnhb-dop"></a>
### T_S_VSMNHB_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | 0 |
| 128 | 1 |

<a id="table-t-1bit-fs-erw-vvtl-bit2-dop"></a>
### T_1BIT_FS_ERW_VVTL_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Bit 2 - Fehler Verstellbereich Fuehrungssensor unplausibel |
| 1 | Bit 2 - Fehler Verstellbereich Fuehrungssensor unplausibel |

<a id="table-t-1bit-geniutest-err-bit0-dop"></a>
### T_1BIT_GENIUTEST_ERR_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Generatortest, elektrischer Fehler Generator nicht vorhanden |
| 1 | Generatortest, elektrischer Fehler Generator vorhanden |

<a id="table-t-1bit-switch-position-low-byte-bit6-dop"></a>
### T_1BIT_SWITCH_POSITION_LOW_BYTE_BIT6_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Schubabschaltung aktiv |
| 1 | Schubabschaltung aktiv |

<a id="table-t-1bit-switch-position-high-byte-bit1-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT1_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Vollast |
| 1 | Vollast |

<a id="table-t-st-testpoelsys-dop"></a>
### T_ST_TESTPOELSYS_DOP

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 3 | Funktion wartet auf Freigabe |
| 4 | -- |
| 5 | Funktionstest laeuft |
| 6 | Funktion beendet |
| 7 | Funktion abgebrochen |
| 8 | Funktion vollstaendig durchlaufen und kein Fehler erkannt |
| 9 | Funktion vollstaendig durchlaufen und Fehler erkannt |

<a id="table-t-1bit-switch-position-high-byte-bit5-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT5_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Lambdaregelung vor Katalysator Bank 1 nicht aktiv |
| 1 | Lambdaregelung vor Katalysator Bank 1 aktiv |

<a id="table-t-1bit-state-ready-obd-2-bit0-dop"></a>
### T_1BIT_STATE_READY_OBD_2_BIT0_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-t-ba-ist-dop"></a>
### T_BA_IST_DOP

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Keine |
| 1 | Schicht |
| 2 | Homogen |
| 3 | Homogen_Schicht |
| 8 | Notlauf |

<a id="table-t-1bit-switch-position-high-byte-bit2-dop"></a>
### T_1BIT_SWITCH_POSITION_HIGH_BYTE_BIT2_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Lambdaregelung hinter Katalysator Bank 1 nicht aktiv |
| 1 | Lambdaregelung hinter Katalysator Bank 1 aktiv |

<a id="table-res-0xf04"></a>
### RES_0XF04

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_RESULT_WERT | - | - | + | - | high | data[255] | - | - | - | - | - | Ergebnis Selbsttest |
