# cas4.prg

- Jobs: [160](#jobs)
- Tables: [77](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | CAS4 |
| ORIGIN | BMW EI-73 Andreas Wojcik |
| REVISION | 0.906 |
| AUTHOR | mPT Kögel GmbH Automotive Alfred Kögel, Conti Temic GmbH L/B2/EFB Dieter Karg |
| COMMENT | N/A |
| PACKAGE | 0.27 |
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
- [STEUERN_IO](#job-steuern-io) - Vorgeben eines Status UDS  : $2F InputOutputControlByIdentifier
- [STEUERN_ROUTINE](#job-steuern-routine) - Vorgeben eines Status UDS  : $31 RoutineControl
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers UDS  : $85 ControlDTCSetting UDS  : $?? Sperren ($02) / Freigabe ($01) Modus: Default
- [IS_LESEN](#job-is-lesen) - Sekundaerer Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $22   ReadDataByIdentifierRequestServiceID UDS  : $2000 DataIdentifier sekundaerer Fehlerspeicher Modus: Default
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - sekundären Fehlerspeicher lesen (Info-Meldungen / Ort und Art) UDS  : $22 ReadDataByIdentifier UDS  : $20 dataIdentifier UDS  : $00 alle Info-Meldungen anschließend UDS  : $20 dataIdentifier UDS  : $nn Details zur Info-Meldung an der Position n Modus: Default
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
- [_STATUS_CAS_INIT_KENNUNG](#job-status-cas-init-kennung) - Jobbeschreibung:	Der Job dient zum Auslesen des CAS Zustands (Verriegelt/Entriegelt) bezüglich des Schlüsselanlernens Vorbedingungen:		keine Diagnose-Service:	UDS $22 DID $4001 Gültigkeit:			Ab F001-08-09-300 Kommentare:			JobHeaderFormat.Nicht in der Diagnose-Datenbank erfasst!
- [STATUS_ANALOG](#job-status-analog) - Job zum Auslesen Analoger Spannungs-Werte am Steuergerät. JobHeaderFormat Aus Kompatibilitaetsgruenden nur fuer I300 Softwarestand verwenden! 0xF3A0 _STATUS_U_KL15N30B (KL15N, KL30B_1, KL30B_2, KL15WUP) 0xF3A1 _STATUS_U_KL15_KL50 (KL15_1, KL15_2, KL15_3, KL15_50, KL50, KL50MSA) 0xF3A2 _STATUS_U_POWERSUPPLY (TEMP, LF_DIAG, LF_STROM) 0xF3A3 _STATUS_U_ELV (KL30_ELV, KL31_ELV) 0xF3A4 _STATUS_U_HALL_TAGE (HALL_VERS13, HALL_VERS24)
- [STATUS_PM_HISTORIE](#job-status-pm-historie) - Der Job dient zum Auslesen des Powermanagement Historienspeicher des CAS. Der Historienspeicher gibt die Weckquelle, das zeitliche Auftreten (relativer Abstand zwischen 2 Weckereignissen) und die Häufigkeit von Weckereignissen wieder. JobHeaderFormat STATUS_PM_HISTORIE Diagnose-Service:	UDS $22 DID $4103
- [STATUS_PM_SCHLAFBEREITSCHAFT](#job-status-pm-schlafbereitschaft) - Der Job dient zum Auslesen der Schlafbereitschaft des CAS und gibt den Status aller möglichen Einschlafverhinderer, d.h. Weckquellen (CAS-intern/extern) aus. JobHeaderFormat STATUS_PM_SCHLAFBEREITSCHAFT Diagnose-Service:	UDS $22 DID $4104
- [_STATUS_STARTCYC_CNT](#job-status-startcyc-cnt) - Jobbeschreibung:	Der Job dient zum Auslesen des Startzykluszählers. Hinweis: Der Startzykluszähler zählt die Anzahl der erfolgreichen Motorstarts. Vorbedingungen:		keine Diagnose-Service:	UDS Diagnose-Service:	UDS $22 DID $4205 Gültigkeit:			Ab F001-08-09-300 Kommentare:			JobHeaderFormat.Nicht in der Diagnose-Datenbank erfasst!
- [_STEUERN_CAS_INIT_KENNUNG](#job-steuern-cas-init-kennung) - Jobbeschreibung:	Der Job dient zum Verriegeln bzw. Entriegeln des CAS für das Schlüsselanlernen Vorbedingungen:		keine Diagnose-Service:	UDS $2E DID $4001 Gültigkeit:			Ab F001-08-09-300 Kommentare:			JobHeaderFormat.Nicht in der Diagnose-Datenbank erfasst!
- [_STEUERN_STARTCYC_CNT](#job-steuern-startcyc-cnt) - Jobbeschreibung:	Der Job dient zum Schreiben des Startzykluszählers. Hinweis: Der Startzykluszähler zählt die Anzahl der erfolgreichen Motorstarts. Vorbedingungen:		keine Diagnose-Service:	UDS Diagnose-Service:	UDS $2E DID $4205 Gültigkeit:			Ab F001-08-09-300 Kommentare:			JobHeaderFormat.Nicht in der Diagnose-Datenbank erfasst!
- [STATUS_CAS_ANLIEFERZUSTAND](#job-status-cas-anlieferzustand) - Dieser Job liefert den aktuellen Fortschritt des Rücksetzen nach STEUERN_CAS_ANLIEFERZUSTAND. JobHeaderFormat STATUS_CAS_ANLIEFERZUSTAND Diagnose-Service:	UDS $22 DID $4003
- [STATUS_CAS_FREQ_TYPE](#job-status-cas-freq-type) - Konfiguration des CAS bzgl. Schlüssel-Initialisierung auslesen. JobHeaderFormat STATUS_CAS_FREQ_TYPE Diagnose-Service:	UDS $22 DID $4202
- [STATUS_CAS_INIT_LOC_DATE](#job-status-cas-init-loc-date) - Konfiguration des CAS bzgl. Schlüssel-Initialisierung auslesen. JobHeaderFormat STATUS_CAS_INIT_LOC_DATE Diagnose-Service:	UDS $22 DID $4203
- [STATUS_CAS_WUP](#job-status-cas-wup) - 4-Byte FBD-Wakeup-Pattern lesen. JobHeaderFormat STATUS_CAS_WUP Diagnose-Service:	UDS $22 DID $4204
- [STATUS_DIGITAL](#job-status-digital) - Job zum Auslesen digitaler Stati JobHeaderFormat 0xF3A5 _STATUS_DIG_INPUT_START_STOP (A_S_START, BLS_MSA) 0xF3A6 _STATUS_DIG_INPUT_HALL (HALL_SSTA, HALL_SSTB) 0xF3A8 _STATUS_DIG_INPUT_SCHALTER (CLT, MHK, HOTEL, MSA, TOEHKL) 0xF3A9 _STATUS_DIG_INPUT_BREMSE_KUPPL (BLTS, PN_KUPPL)
- [STATUS_EGS_ISN](#job-status-egs-isn) - Verriegelungs-Status für EGS-ISN im CAS lesen (wird für Getriebe-EWS genutzt) JobHeaderFormat STATUS_EGS_ISN Diagnose-Service:	UDS $22 DID $4300
- [STATUS_EWS](#job-status-ews) - Liefert den aktuellen Status der EWS-SecretKeys ISNs und den Status bzgl. KeyID KeyPIN JobHeaderFormat STATUS_EWS_CAS Diagnose-Service:	UDS $22 DID $C000
- [STATUS_EWS4_SK](#job-status-ews4-sk) - Dieser Job dient zum (Gegen-)Lesen der Secretkeys / ISNs (vor einem anschließenden Verriegeln Kommando) JobHeaderFormat STATUS_EWS4_SK_CAS Diagnose-Service:	UDS $22 DID $C002
- [STATUS_FAHRGESTELLNUMMER](#job-status-fahrgestellnummer) - Lesen der Fahrgestellnummer JobHeaderFormat STATUS_FAHRGESTELLNUMMER Diagnose-Service:	UDS $22 DID $F190
- [STATUS_SCHLUESSEL_TRSP](#job-status-schluessel-trsp) - Liefert den Status des momentan in der Ringspule befindlichen Schlüssels. Der Job liefert den Status des zuletzt gefundenen Transponders in der Ringspule. Die Daten sind max. 300 ms alt und entprellt (bei dauerhaft vorhandenem Transponder, keine flackernden Results). Ist der Schlüssel unbekannt und bereits gelocked, so werden nur die immer lesbaren Informationen ausgegeben. JobHeaderFormat STATUS_SCHLUESSEL_TRSP Diagnose-Service:	UDS $22 DID $4200
- [STATUS_SCHLUESSELDATEN](#job-status-schluesseldaten) - Jobbeschreibung:	Dieser Job dient dazu den Status eines Schlüssel laut Transpondertabelle auszulesen. Anmerkung: Die Informationen sind unabhängig von einem evtl. gerade vorhandenen Transponder in der Ringspule bzw. einem erkannten ID-Geber. Vorbedingungen:		keine Diagnose-Service:	UDS Diagnose-Service:	UDS $22 DID $4210 Gültigkeit:			Ab F001-08-09-300 Kommentare:			Im JobHeaderFormat in der Diagnose-Datenbank angelegt
- [STATUS_CAS_HW_GESCHWINDIGKEIT](#job-status-cas-hw-geschwindigkeit) - Auslesen der vom CAS (über separate HW-Leitung vom DSC) erkannte Geschwindigkeit. JobHeaderFormat CAS_HW_GESCHWINDIGKEIT Diagnose-Service:	UDS $22 DID $DC51
- [STATUS_CAS_HW_VARIANTE](#job-status-cas-hw-variante) - Hardware-Variante des CAS lesen. JobHeaderFormat CAS_HW_VARIANTE Diagnose-Service:	UDS $22 DID $DAB7
- [STATUS_ISTUFE](#job-status-istufe) - Liefert die im EEPROM abgelegte I-Stufe jeweils für Werk, HO und HO-Backup. JobHeaderFormat STATUS_ISTUFE Diagnose-Service:	UDS $22 DID $100B
- [STATUS_KILOMETERSTAND](#job-status-kilometerstand) - Aufruf liefert den angezeigeten Gesamtwegstreckenzähler. Beim CAS den im EEPROM hinterlegten Wert. JobHeaderFormat STATUS_KILOMETERSTAND Diagnose-Service:	UDS $22 DID $1700
- [STEUERN_CAS_ANLIEFERZUSTAND](#job-steuern-cas-anlieferzustand) - Versetzt das CAS in den Anlieferzustand (Montage-Modi, Codierung, VIN, Tansponder-Tabelle, EWS4_CLIENT_SK, ...) Falls Rücksetzen unzulässig: ERROR_ECU_CONDITIONS_NOT_CORRECT. Anmerkung: Nach dem Rücksetzen müssen alle im verriegelten Zustand geschützten W JobHeaderFormat STEUERN_CAS_ANLIEFERZUSTAND Diagnose-Service:	UDS $3101 DID $AC50($4003)
- [STEUERN_CAS_FREQ_TYPE](#job-steuern-cas-freq-type) - Konfigurationd des CAS setzen. Die Konfiguration ist nach dem Verriegeln des EWS4_SK bzw. EWS4_TRSP_SK nicht mehr änderbar (ERROR_ECU_CONDITIONS_NOT_CORRECT). Werden unzulässige Daten übergeben, so erfolgt ein ERROR_DATA. JobHeaderFormat STEUERN_CAS_FREQ_TYPE Diagnose-Service:	UDS $2E DID $4202
- [STEUERN_CAS_INIT_LOC_DATE](#job-steuern-cas-init-loc-date) - Konfigurationd des CAS setzen. Die Konfiguration ist nach dem Verriegeln des EWS4_SK bzw. EWS4_TRSP_SK nicht mehr änderbar (ERROR_ECU_CONDITIONS_NOT_CORRECT). Werden unzulässige Daten übergeben, so erfolgt ein ERROR_DATA. JobHeaderFormat STEUERN_CAS_INIT_LOC_DATE Diagnose-Service:	UDS $2E DID $4203
- [STEUERN_CAS_WUP](#job-steuern-cas-wup) - 4-Byte FBD-Wakeup-Pattern schreiben. JobHeaderFormat STEUERN_CAS_WUP Diagnose-Service:	UDS $2E DID $4204
- [STEUERN_EGS_ISN](#job-steuern-egs-isn) - EGS-ISN im CAS setzen (wird für Getriebe-EWS genutzt) JobHeaderFormat STEUERN_EGS_ISN Diagnose-Service:	UDS $2E DID $4300
- [STEUERN_EWS4](#job-steuern-ews4) - Dieser Job dient zum Setzen der Secretkeys und zum anschließenden Verriegeln. JobHeaderFormat STEUERN_EWS4_CAS Diagnose-Service:	UDS $2E DID $C001
- [STEUERN_FAHRGESTELLNUMMER](#job-steuern-fahrgestellnummer) - Schreiben der Fahrgestellnummer JobHeaderFormat STEUERN_FAHRGESTELLNUMMER Diagnose-Service:	UDS $2E DID $F190
- [STEUERN_SCHLUESSEL_INIT](#job-steuern-schluessel-init) - Job zum Anstoßen der Schlüssel-Initialisierung. Nur zulässig, solange EWS4_TRSP_SK noch nicht verriegelt. JobHeaderFormat STEUERN_SCHLUESSEL_INIT Diagnose-Service:	UDS $3101 RID $AC52($4005)
- [STEUERN_SCHLUESSELDATEN](#job-steuern-schluesseldaten) - Schlüssel-Daten in CAS schreiben (z.B. für Ersatz-Steuergerät oder Nacharbeit). Nur zulässig solange EWS4_TRSP_SK nicht verriegelt. JobHeaderFormat STEUERN_SCHLUESSELDATEN Diagnose-Service:	UDS $2E DID $4210
- [STEUERN_PIA_NR](#job-steuern-pia-nr) - PIA-Nummer eines Schlüssels umdefinieren. JobHeaderFormat STEUERN_PIA_NR Diagnose-Service:	UDS $22 DID $DC5B
- [STEUERN_SERVICE_SCHLUESSELDATEN_UPDATE](#job-steuern-service-schluesseldaten-update) - Dieser Job ermöglicht es einem folgende Aktionen anzustossen: Ermitteln der aktuellen Daten aus dem Fahrzeug, Übertragen der Daten in alle aktuell erkannten Schlüssel (inkrementell oder komplett). JobHeaderFormat STEUERN_SERVICE_SCHLUESSELDATEN_UPDATE Diagnose-Service:	UDS $3101 DID $4005
- [STATUS_SERVICE_SCHLUESSELDATEN_LESEN](#job-status-service-schluesseldaten-lesen) - Dieser Job erlaubt es die Service-Schlüsseldaten blockweise aus dem CAS auszulesen. JobHeaderFormat STATUS_SERVICE_SCHLUESSELDATEN Diagnose-Service:	UDS $3101 DID $1006
- [_DIAGNOSE_MODE](#job-diagnose-mode) - UDS  : $10   DiagnosticSessionControl Mode einstellbar ueber das Argument
- [_STATUS_IDENT_ISTUFE](#job-status-ident-istufe) - Lesen Identifikation I-Stufe UDS  : $22   ReadDataByIdentifier $100B Modus: Default
- [_STATUS_KILOMETERSTAND](#job-status-kilometerstand) - Lesen aktueller Kilometerstand UDS  : $22   ReadDataByIdentifier $1700 Modus: Default
- [_STATUS_ABS_TIME](#job-status-abs-time) - Lesen aktuelle absolute Zeit UDS  : $22   ReadDataByIdentifier $1701 Modus: Default
- [_STATUS_DARH_DTC](#job-status-darh-dtc) - Lesen Anzahl der abgelegten Fehler UDS  : $22   ReadDataByIdentifier $1704 Modus: Default
- [_STATUS_SC_VERSION](#job-status-sc-version) - Lesen Standard Core Version UDS  : $22   ReadDataByIdentifier $1720 Modus: Default
- [_STATUS_SC_PACKAGE_ID](#job-status-sc-package-id) - Lesen Standard Core Package Id UDS  : $22   ReadDataByIdentifier $1726 Modus: Default
- [_STATUS_MEM_SEG_TABLE](#job-status-mem-seg-table) - Lesen Memory segmentation table UDS  : $22   ReadDataByIdentifier $2501 Modus: Default
- [_STATUS_PROG_COUNTER](#job-status-prog-counter) - Lesen Programming counter Status UDS  : $22   ReadDataByIdentifier $2502 Modus: Default
- [_STATUS_PROG_COUNTER_MAX](#job-status-prog-counter-max) - Lesen Maximalwert des Programming Counters UDS  : $22   ReadDataByIdentifier $2503 Modus: Default
- [_STATUS_FLASH_TIM_PARA](#job-status-flash-tim-para) - Lesen Flash Timing Parameter UDS  : $22   ReadDataByIdentifier $2504 Modus: Default
- [_STATUS_MAX_BLOCK_LENGTH](#job-status-max-block-length) - Lesen maximale Blocklaenge UDS  : $22   ReadDataByIdentifier $2505 Modus: Default
- [_STATUS_FAHRZEUGAUFTRAG_TEIL_1](#job-status-fahrzeugauftrag-teil-1) - aktuelle 160 Byte Fahrzeugauftrag Teil1 UDS  : $22   ReadDataByIdentifier $3F1C Modus: Default
- [_STATUS_FAHRZEUGAUFTRAG_TEIL_2](#job-status-fahrzeugauftrag-teil-2) - aktuelle 160 Byte Fahrzeugauftrag Teil2 UDS  : $22   ReadDataByIdentifier $3F1C Modus: Default
- [_STATUS_CAS_VAR_KONFIG](#job-status-cas-var-konfig) - aktueller Status "CAS, Varianten Konfiguration" UDS  : $22   ReadDataByIdentifier $4000 Modus: Default
- [_STATUS_TRSP_MECH_CODE](#job-status-trsp-mech-code) - aktueller Status "Transponder MechCode" UDS  : $22   ReadDataByIdentifier $4201 Modus: Default
- [_STATUS_TRSP_FAHRZYKLUS](#job-status-trsp-fahrzyklus) - aktueller Status "Transponder Programmierdaten" UDS  : $22   ReadDataByIdentifier $4205 Modus: Default
- [_STATUS_FBD_EMPFANGSDATEN](#job-status-fbd-empfangsdaten) - aktuelle 18 Byte des FBD Empfangs UDS  : $22   ReadDataByIdentifier $4600 Modus: Default
- [_STATUS_ACT_DIAG_SESSION](#job-status-act-diag-session) - Lesen active diagnose session UDS  : $22   ReadDataByIdentifier $F186 Modus: Default
- [_STATUS_SUPPLIER_NUMBER](#job-status-supplier-number) - Lesen ECU serial number UDS  : $22   ReadDataByIdentifier $F18A Modus: Default
- [_STATUS_ECU_MANUFACTURING_DATA](#job-status-ecu-manufacturing-data) - Lesen ECU serial number UDS  : $22   ReadDataByIdentifier $F18B Modus: Default
- [_STATUS_ECU_SERIAL_NUMBER](#job-status-ecu-serial-number) - Lesen ECU serial number UDS  : $22   ReadDataByIdentifier $F18C Modus: Default
- [_STATUS_CAS4_AUSLIEFERUNGSSTAND](#job-status-cas4-auslieferungsstand) - CAS4 Auslieferungsstand UDS  : $22   ReadDataByIdentifier $F300 Modus: Default Fuer CT Qualitaetssicherung benoetigt hierueber erfolgt die Identifikation des SW Stand der ECU
- [_STATUS_COMPILATION_DATE_TIME](#job-status-compilation-date-time) - aktuelle 21 Byte Ascii UDS  : $22   ReadDataByIdentifier $F317 Modus: Default Datum ist in ASCII hinterlegt, das Format ist von der Systemdatum und -zeit Variablen eines Windows PC abhaengig
- [_STATUS_ANT_LINKS_AUSSEN_HANDLE](#job-status-ant-links-aussen-handle) - aktueller Status "Antenne Links aussen Handle" UDS  : $22   ReadDataByIdentifier $F320 Modus: Default
- [_STATUS_ANT_RECHTS_AUSSEN_HANDLE](#job-status-ant-rechts-aussen-handle) - aktueller Status "Antenne Rechts aussen Handle" UDS  : $22   ReadDataByIdentifier $F321 Modus: Default
- [_STATUS_ANT_KOFFERR_AUSSEN_HANDLE](#job-status-ant-kofferr-aussen-handle) - aktueller Status "Antenne Kofferraum aussen Handle" UDS  : $22   ReadDataByIdentifier $F322 Modus: Default
- [_STATUS_ANT_VORNE_INNEN_HANDLE](#job-status-ant-vorne-innen-handle) - aktueller Status "Antenne vorne innen Handle" UDS  : $22   ReadDataByIdentifier $F323 Modus: Default
- [_STATUS_ANT_MITTE_INNEN_HANDLE](#job-status-ant-mitte-innen-handle) - aktueller Status "Antenne vorne innen Handle" UDS  : $22   ReadDataByIdentifier $F324 Modus: Default
- [_STATUS_ANT_HUTABLAGE_HANDLE](#job-status-ant-hutablage-handle) - aktueller Status "Antenne Hutablage Handle" UDS  : $22   ReadDataByIdentifier $F325 Modus: Default
- [_STATUS_ANT_KOFFERR_INNEN_LINKS_HANDLE](#job-status-ant-kofferr-innen-links-handle) - aktueller Status "Antenne Kofferraum innen links Handle" UDS  : $22   ReadDataByIdentifier $F326 Modus: Default
- [_STATUS_ANT_KOFFERR_INNEN_RECHTS_HANDLE](#job-status-ant-kofferr-innen-rechts-handle) - aktueller Status "Antenne Kofferraum innen rechts Handle" UDS  : $22   ReadDataByIdentifier $F327 Modus: Default
- [_STATUS_COMFORT_GO_ANT_KONFIG](#job-status-comfort-go-ant-konfig) - aktueller Status "Comfort Go Antennen Konfiguration" UDS  : $22   ReadDataByIdentifier $F330 Modus: Default 
- [_STATUS_TAGE_ID](#job-status-tage-id) - aktueller Status "Status TAGE Identifier" UDS  : $22   ReadDataByIdentifier $F331 Modus: Default BMW Teilenummer (6Byte String) fuer jede Tuer
- [_STATUS_ANTENNEN](#job-status-antennen) - aktueller Status "Status Antennen" UDS  : $22   ReadDataByIdentifier $F340 Modus: Default Liefert die Stati der bis zu 8 Antennen und einen globalen Status
- [_STATUS_TAGE](#job-status-tage) - aktueller Status "Status Tueraussengriffelektronik" UDS  : $22   ReadDataByIdentifier $F341 Modus: Default
- [_STATUS_CA_TELEGRAMM](#job-status-ca-telegramm) - aktueller Status "Status CA Telegramm" UDS  : $22   ReadDataByIdentifier $F342 Modus: Default
- [_STATUS_ANT_STROEME](#job-status-ant-stroeme) - aktueller Status "Status Antennenstroeme" UDS  : $22   ReadDataByIdentifier $F343 Modus: Default Bei der zuletzt ausgefuehrten CA Aktion gemessener Antennenstrom fuer alle Antennen
- [_STATUS_SCHLUESSEL_INFO](#job-status-schluessel-info) - aktueller Status "Status Schluesselinfo" UDS  : $22   ReadDataByIdentifier $F344 Modus: Default
- [_STATUS_CA_HANDLER](#job-status-ca-handler) - aktueller Status "Status CA Handler" UDS  : $22   ReadDataByIdentifier $F345 Modus: Default Interner CAH-Statusspeicher, nur zu Entwicklungszwecken
- [_STATUS_RES_FREQ](#job-status-res-freq) - aktueller Status "Status Resonanz Frequenz" UDS  : $22   ReadDataByIdentifier $F346 Modus: Default Lesen der geschaetzten Resonanzfrequenzen
- [_STATUS_ANT_GUETE](#job-status-ant-guete) - aktueller Status "Status Guete Antenne" UDS  : $22   ReadDataByIdentifier $F347 Modus: Default Lesen der geschaetzten Gueten
- [_STATUS_LF_TREIBER](#job-status-lf-treiber) - aktueller Status "Status LF Treiber" UDS  : $22   ReadDataByIdentifier $F348 Modus: Default Verhalten des LF-Treibers und des CAH
- [_STATUS_U_KL15N30B](#job-status-u-kl15n30b) - aktueller Status analoge Spannungswerte Funktionsgruppe 15N30B UDS  : $22   ReadDataByIdentifier $F3A0 Modus: Default
- [_STATUS_U_KL15_KL50](#job-status-u-kl15-kl50) - aktueller Status analoge Spannungswerte Funktionsgruppe KL15 UDS  : $22   ReadDataByIdentifier $F3A1 Modus: Default
- [_STATUS_U_POWERSUPPLY](#job-status-u-powersupply) - aktueller Status analoge Spannungswerte Funktionsgruppe Powersupply UDS  : $22   ReadDataByIdentifier $F3A2 Modus: Default
- [_STATUS_U_ELV](#job-status-u-elv) - aktueller Status analoge Spannungswerte ELV Funktionsgruppe Powersupply UDS  : $22   ReadDataByIdentifier $F3A3 Modus: Default
- [_STATUS_U_HALL_TAGE](#job-status-u-hall-tage) - aktueller Status analoge Spannungswerte Hallsensoren und Tueraussengriffe Funktionsgruppe Powersupply UDS  : $22   ReadDataByIdentifier $F3A4 Modus: Default
- [_STATUS_DIG_INPUT_START_STOP](#job-status-dig-input-start-stop) - aktueller Status digitale Eingaenge Funktionsgruppen 15N30B und 15WUP UDS  : $22   ReadDataByIdentifier $F3A5 Modus: Default
- [_STATUS_DIG_INPUT_HALL](#job-status-dig-input-hall) - aktueller Status digitale Eingaenge Funktionsgruppen HALL UDS  : $22   ReadDataByIdentifier $F3A6 Modus: Default
- [_STATUS_DIG_INPUT_SCHALTER](#job-status-dig-input-schalter) - aktueller Status digitale Eingaenge Funktionsgruppen Schalter UDS  : $22   ReadDataByIdentifier $F3A8 Modus: Default
- [_STATUS_DIG_INPUT_BREMSE_KUPPL](#job-status-dig-input-bremse-kuppl) - aktueller Status digitale Eingaenge Funktionsgruppen Bremse und Kupplung UDS  : $22   ReadDataByIdentifier $F3A9 Modus: Default
- [_STATUS_DIG_INPUT_KLEMMEN](#job-status-dig-input-klemmen) - aktueller Status digitale Eingaenge Funktionsgruppen 15N30B und 15WUP UDS  : $22   ReadDataByIdentifier $F3AB Modus: Default
- [_SA_REQUEST_SEED](#job-sa-request-seed) - Anfordern des SEED Codes von der ECU Es muessen immer alle 5 Argumente im angegebenen Wertebereich uebergeben werden. UDS  : $27   SecurityAccess SID $01   Sub Identifier "Request Seed" User-ID Byte[0] User-ID Byte[1] User-ID Byte[2] User-ID Byte[3] Modus: Default
- [_SA_SEND_KEY](#job-sa-send-key) - Senden des Key Wertes an die ECU Es muessen immer alle Argumente im jeweils gueltigen Wertebereich uebergeben werden. UDS  : $27   SecurityAccess SID $02   Sub Identifier "Request Seed" $03   FixCode[68 Byte Array] Modus: Default
- [_STEUERN_IDENT_ISTUFE](#job-steuern-ident-istufe) - Beschreiben der I-Stufe Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $100B Modus: Default
- [_STEUERN_FAHRZEUGAUFTRAG_TEIL_1](#job-steuern-fahrzeugauftrag-teil-1) - Beschreiben der Fahrzeugauftrag Teil1 Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $3F1C Modus: Default
- [_STEUERN_FAHRZEUGAUFTRAG_TEIL_2](#job-steuern-fahrzeugauftrag-teil-2) - Beschreiben der Fahrzeugauftrag Teil2 Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $3F1D Modus: Default
- [_STEUERN_CAS_VAR_KONFIG](#job-steuern-cas-var-konfig) - Beschreiben der CAS Varianten Konfiguration Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $4000 CAS_VAR_KONFIG Modus: Default
- [_STEUERN_TRSP_MECH_CODE](#job-steuern-trsp-mech-code) - Beschreiben des Transponder MechCode Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $4201 Modus: Default
- [_STEUERN_TRSP_FAHRZYKLUS](#job-steuern-trsp-fahrzyklus) - Beschreiben des Transponder Fahrzykluszaehler Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $4205 Modus: Default
- [_STEUERN_EWS4_SECKEY](#job-steuern-ews4-seckey) - Schreiben des EWS4 Secret Key 17 Byte Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $C001 Modus: Default
- [_STEUERN_SVK_SUPPLIER](#job-steuern-svk-supplier) - Schreiben der BMW Logistik Daten Zulieferer Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F102 Modus: Default
- [_STEUERN_SVK_WERK](#job-steuern-svk-werk) - Schreiben der BMW Logistik Daten Werk Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F103 Modus: Default
- [_STEUERN_ANT_LINKS_AUSSEN_HANDLE](#job-steuern-ant-links-aussen-handle) - Beschreiben des Antenne links Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F320 Data Modus: Default
- [_STEUERN_ANT_RECHTS_AUSSEN_HANDLE](#job-steuern-ant-rechts-aussen-handle) - Beschreiben des Antenne rechts aussen Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F321 Data Modus: Default
- [_STEUERN_ANT_KOFFERR_AUSSEN_HANDLE](#job-steuern-ant-kofferr-aussen-handle) - Beschreiben des Antenne Kofferraum aussen Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F322 Data Modus: Default
- [_STEUERN_ANT_VORNE_INNEN_HANDLE](#job-steuern-ant-vorne-innen-handle) - Beschreiben des Antenne vorne innen Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F323 Data Modus: Default
- [_STEUERN_ANT_MITTE_INNEN_HANDLE](#job-steuern-ant-mitte-innen-handle) - Beschreiben des Antenne mitte innen Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F324 Data Modus: Default
- [_STEUERN_ANT_HUTABLAGE_HANDLE](#job-steuern-ant-hutablage-handle) - Beschreiben des Antenne Hutablage Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F325 Data Modus: Default
- [_STEUERN_ANT_KOFFERR_INNEN_LINKS_HANDLE](#job-steuern-ant-kofferr-innen-links-handle) - Beschreiben des Antenne Kofferraum innen links Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F326 Data Modus: Default
- [_STEUERN_ANT_KOFFERR_INNEN_RECHTS_HANDLE](#job-steuern-ant-kofferr-innen-rechts-handle) - Beschreiben des Antenne Kofferraum innen rechts Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F327 Data Modus: Default
- [_STEUERN_COMFORT_GO_ANT_KONFIG](#job-steuern-comfort-go-ant-konfig) - Beschreiben der Comfort go Antennen Konfig Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F330 Data Modus: Default
- [_STEUERN_TAGE_ID](#job-steuern-tage-id) - Beschreiben der Tueraussengriffelektronik Id Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F331 Data Modus: Default
- [_STEUERN_TREIBERSTUFE_KL15_30](#job-steuern-treiberstufe-kl15-30) - Ansteuerung der Klemme 15/30 Ausgangspins UDS  : $2F     I/O Control By Local Id $0201   Data Id
- [_STEUERN_TREIBERSTUFE_KL15_50](#job-steuern-treiberstufe-kl15-50) - Ansteuerung der Klemme 15/50 Ausgangspins UDS  : $2F     I/O Control By Local Id $0202   Data Id
- [_STEUERN_BIMAG](#job-steuern-bimag) - Ansteuerung der BiMAG UDS  : $2F     I/O Control By Local Id $0203   Data Id
- [_STEUERN_ELV](#job-steuern-elv) - Ansteuerung ELV UDS  : $2F     I/O Control By Local Id $0204   Data Id
- [_STEUERN_HALL](#job-steuern-hall) - Ansteuerung HALL Sensoren UDS  : $2F     I/O Control By Local Id $0205   Data Id
- [_STEUERN_LED_LF](#job-steuern-led-lf) - Ansteuerung LED und LF UDS  : $2F     I/O Control By Local Id $0206   Data Id
- [_STEUERN_ANT_STATUS_RESET](#job-steuern-ant-status-reset) - Antennenstatus ruecksetzen UDS  : $31       Routine Control $xxF801   Routine Id $F801 Modus: Default
- [_STEUERN_SCHLUESSEL_SUCHE](#job-steuern-schluessel-suche) - Schluesselsuche, CA Handler versendet LF Telegramm UDS  : $31       Routine Control $xxF802   Routine Id $F802 Modus: Default
- [_STEUERN_LF_HW_TEST](#job-steuern-lf-hw-test) - LF Hardware Selbsttest UDS  : $31       Routine Control $xxF803   Routine Id $F803 Modus: Default
- [_STEUERN_LF_TEST_TELEGRAMM](#job-steuern-lf-test-telegramm) - Versendet LF Telegramm mit der im Parameter angegebenen Anzahl Bytes UDS  : $31       Routine Control $xxF804   Routine Id $F804 Modus: Default
- [_STEUERN_RESET_DET](#job-steuern-reset-det) - Ruecksetzen der Eintraege im Debugmodul "Development Error Tracer (DET)" UDS  : $31       Routine Control $xxF806   Routine Id $F806 Modus: Default
- [_DEVELOPMENT_JOB](#job-development-job) - Frei programmierbare Diagnosebotschaft, die ohne Vorfilterung auf dem CAN gesendet wird. Wird benoetigt fuer Diagnose Tests. Auch &gt; 64 Byte Daten Adressierung unterstuetzt. Modus: Default

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
| PROZESSKLASSE_WERT | int | table Prozessklasse WERT dezimale Angabe der Prozessklasse |
| PROZESSKLASSE_TEXT | string | table Prozessklasse BEZEICHNUNG Text-Angabe der Prozessklasse |
| SGBM_IDENTIFIER | string | Angabe SGBM-ID der Prozessklasse |
| VERSION | string | Angabe der Version der Prozessklasse |
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

<a id="job-steuern-io"></a>
### STEUERN_IO

Vorgeben eines Status UDS  : $2F InputOutputControlByIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARGUMENT_SPALTE | string | 'ARG', 'ID', 'LABEL' |
| STATUS | string | Siehe table SG_Funktionen ARG ID RES_TABELLE ARG_TABELLE |
| STEUERPARAMETER | string | 'RCTECU' = returnControlToECU 'RTD'    = resetToDefault 'FCS'    = freezeCurrentState 'STA'    = shortTermAdjustment optionales Argument Wenn nicht angegeben, dann kein InputOutputControlParameter im Request |
| WERT | string | Argumente siehe table SG_Funktionen ARG_TABELLE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Antwort von SG |
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

<a id="job-fs-sperren"></a>
### FS_SPERREN

Sperren bzw. Freigeben des Fehlerspeichers UDS  : $85 ControlDTCSetting UDS  : $?? Sperren ($02) / Freigabe ($01) Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPERREN | string | "ja"   -&gt; Fehlerspeicher sperren "nein" -&gt; Fehlerspeicher freigeben table DigitalArgument TEXT Default: "ja" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
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
| SENSOR_NR | long | optionales Argument gewuenschter Sensor xx (0x01 - 0xFF) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SENSOR_VERBAUORT | string | Verbauort des Sensors table VerbauortTabelle ORTTEXT |
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
| PROG_MAX | int | maximal mögliche Programmiervorgänge Sonderfall 0xFFFF: Anzahl der Programmiervorgänge unbegrenzt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cas-init-kennung"></a>
### _STATUS_CAS_INIT_KENNUNG

Jobbeschreibung:	Der Job dient zum Auslesen des CAS Zustands (Verriegelt/Entriegelt) bezüglich des Schlüsselanlernens Vorbedingungen:		keine Diagnose-Service:	UDS $22 DID $4001 Gültigkeit:			Ab F001-08-09-300 Kommentare:			JobHeaderFormat.Nicht in der Diagnose-Datenbank erfasst!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CAS_INIT | binary | Beschreibung:		Das Ergebnis enthält den Verriegelungsstatus des CAS hinsichtlich des Anlernens von Schlüsseln Datenlänge: 		3 Byte Gültige Werte: 		0xAAAAAA = CAS für Schlüssel anlernen gesperrt Alle anderen Werte = CAS für Schlüssel anlernen frei Einheit:			hex |
| JOB_STATUS | string | Beschreibung: 		Status der Jobverarbeitung Gültige Werte: 		OKAY = Fehlerfrei table JobResult 	STATUS_TEXT |
| _REQUEST | binary | Beschreibung:		Hex-Auftrag an SG |
| _RESPONSE | binary | Beschreibung:		Hex-Antwort von SG |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Job zum Auslesen Analoger Spannungs-Werte am Steuergerät. JobHeaderFormat Aus Kompatibilitaetsgruenden nur fuer I300 Softwarestand verwenden! 0xF3A0 _STATUS_U_KL15N30B (KL15N, KL30B_1, KL30B_2, KL15WUP) 0xF3A1 _STATUS_U_KL15_KL50 (KL15_1, KL15_2, KL15_3, KL15_50, KL50, KL50MSA) 0xF3A2 _STATUS_U_POWERSUPPLY (TEMP, LF_DIAG, LF_STROM) 0xF3A3 _STATUS_U_ELV (KL30_ELV, KL31_ELV) 0xF3A4 _STATUS_U_HALL_TAGE (HALL_VERS13, HALL_VERS24)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_KLEMME_15N_WERT | string | Spannungswert am Steuergerät an Klemme 15N Bei Alt-Baureihen entspricht dies KL30G Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15N_EINH | string | Spannungswert am Steuergerät an Klemme 15N Bei Alt-Baureihen entspricht dies KL30G Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_30B_1_WERT | string | Spannungswert am Steuergerät an Klemme 30B_1 Bei Alt-Baureihen entspricht dies Klemme R Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_30B_1_EINH | string | Spannungswert am Steuergerät an Klemme 30B_1 Bei Alt-Baureihen entspricht dies Klemme R Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_30B_2_WERT | string | Spannungswert am Steuergerät an Klemme 30B_2 Bei Alt-Baureihen entspricht dies Klemme R Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_30B_2_EINH | string | Spannungswert am Steuergerät an Klemme 30B_2 Bei Alt-Baureihen entspricht dies Klemme R Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15WUP_WERT | string | Spannungswert am Steuergerät an Klemme 15_WUP Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15WUP_EINH | string | Spannungswert am Steuergerät an Klemme 15_WUP Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15_1_WERT | string | Spannungswert am Steuergerät an Klemme 15_1 Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15_1_EINH | string | Spannungswert am Steuergerät an Klemme 15_1 Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15_2_WERT | string | Spannungswert am Steuergerät an Klemme 15_2 Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15_2_EINH | string | Spannungswert am Steuergerät an Klemme 15_2 Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15_3_WERT | string | Spannungswert am Steuergerät an Klemme 15_3 Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15_3_EINH | string | Spannungswert am Steuergerät an Klemme 15_3 Bei CAS Ausgang |
| STAT_STROM_KLEMME_15_50_WERT | string | Stromwert am Steuergerät an Klemme 15 und 50 Bei CAS Ausgang |
| STAT_STROM_KLEMME_15_50_EINH | string | Stromwert am Steuergerät an Klemme 15 und 50 Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_50_WERT | string | Spannungswert am Steuergerät an Klemme 50 Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_50_EINH | string | Spannungswert am Steuergerät an Klemme 50 Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_50MSA_WERT | string | Spannungswert am Steuergerät an Klemme 50MSA Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_50MSA_EINH | string | Spannungswert am Steuergerät an Klemme 50MSA Bei CAS Ausgang |
| STAT_STROM_LF_WERT | string | Stromwert am Steuergerät an LF (CA-Antennen) Bei CAS Ausgang |
| STAT_STROM_LF_EINH | string | Stromwert am Steuergerät an LF (CA-Antennen) Bei CAS Ausgang |
| STAT_DIAG_LF_WERT | string | Spannung am Steuergerät an LF (CA-Antennen) Bei CAS Ausgang |
| STAT_DIAG_LF_EINH | string | Spannung am Steuergerät an LF (CA-Antennen) Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_31ELV_WERT | string | Spannungswert am CAS-Steuergerät an Klemme 30_ELV Ausgang am CAS |
| STAT_SPANNUNG_KLEMME_31ELV_EINH | string | Spannungswert am CAS-Steuergerät an Klemme 30_ELV Ausgang am CAS |
| STAT_SPANNUNG_KLEMME_30ELV_WERT | string | Spannungswert am CAS-Steuergerät an Klemme 30_ELV Ausgang am CAS |
| STAT_SPANNUNG_KLEMME_30ELV_EINH | string | Spannungswert am CAS-Steuergerät an Klemme 30_ELV Ausgang am CAS |
| STAT_SPANNUNG_INNENTEMPERATUR_WERT | string | Spannung am PTC/NTC im Steuergerät zur Ermittlung der Innentemperatur |
| STAT_SPANNUNG_INNENTEMPERATUR_EINH | string | Spannung am PTC/NTC im Steuergerät zur Ermittlung der Innentemperatur |
| STAT_SPANNUNG_HALL_VERS13_WERT | string | Spannung Hall-Sensor-Versorgung (Peak) Sensoren 1 und 3 |
| STAT_SPANNUNG_HALL_VERS13_EINH | string | Spannung Hall-Sensor-Versorgung (Peak) Sensoren 1 und 3 |
| STAT_SPANNUNG_HALL_VERS24_WERT | string | Spannung Hall-Sensor-Versorgung (Peak) Sensoren 2 und 4 |
| STAT_SPANNUNG_HALL_VERS24_EINH | string | Spannung Hall-Sensor-Versorgung (Peak) Sensoren 2 und 4 |
| STAT_SPANNUNG_KLEMME_30B_3_WERT | string | Spannungswert am Steuergerät an Klemme 30B_3 Bei Alt-Baureihen entspricht dies Klemme R Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_30B_3_EINH | string | Spannungswert am Steuergerät an Klemme 30B_3 Bei Alt-Baureihen entspricht dies Klemme R Bei CAS Ausgang |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-pm-historie"></a>
### STATUS_PM_HISTORIE

Der Job dient zum Auslesen des Powermanagement Historienspeicher des CAS. Der Historienspeicher gibt die Weckquelle, das zeitliche Auftreten (relativer Abstand zwischen 2 Weckereignissen) und die Häufigkeit von Weckereignissen wieder. JobHeaderFormat STATUS_PM_HISTORIE Diagnose-Service:	UDS $22 DID $4103

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PMHISTORIE_ANZAHL_ERGEBNISSAETZE_WERT | unsigned char | Anzahl der Einträge im Historienspeicher. Abhängig von dieser Anzahl n (n = 1, 2, ...) existieren n mal folgende Results in je einem eigenen EDIABAS-Ergebnissatz (analog FS_LESEN): STAT_PMHISTORIE_ID_WECKQUELLE, STAT_PMHISTORIE_HAEUFIGKEITSZAEHLER_WERT, STAT_PMHISTORIE_BETRIEBSSEKUNDENZAEHLER_WERT, STAT_PM_HISTORIE_ERGEBNISSATZ_NUMMER_WERT Wertebereich: 0: Keine Historienspeicher vorhanden 1 - 255: Anzahl der Historienspeichereinträge |
| STAT_PMHISTORIE_ANZAHL_ERGEBNISSAETZE_EINH | string | Anzahl der Einträge im Historienspeicher. Abhängig von dieser Anzahl n (n = 1, 2, ...) existieren n mal folgende Results in je einem eigenen EDIABAS-Ergebnissatz (analog FS_LESEN): STAT_PMHISTORIE_ID_WECKQUELLE, STAT_PMHISTORIE_HAEUFIGKEITSZAEHLER_WERT, STAT_PMHISTORIE_BETRIEBSSEKUNDENZAEHLER_WERT, STAT_PM_HISTORIE_ERGEBNISSATZ_NUMMER_WERT Wertebereich: 0: Keine Historienspeicher vorhanden 1 - 255: Anzahl der Historienspeichereinträge |
| STAT_PMHISTORIE_ERGEBNISSATZ_NUMMER_WERT | unsigned char | Aktuelle Satz-Nummer 1 bis n |
| STAT_PMHISTORIE_ERGEBNISSATZ_NUMMER_EINH | string | Aktuelle Satz-Nummer 1 bis n |
| STAT_PMHISTORIE_ID_WECKQUELLE | unsigned char | Das Ergebnis enthält die PM-ID der entsprechenden Aufweckquelle. Hinweise:  Die PM-ID für eine Wakeupquelle unterscheidet sich von der FZM-ID dadurch, das bei dir PM-ID auch interne CAS-Weckquellen unterschieden werden. |
| STAT_PMHISTORIE_ID_WECKQUELLE_TEXT | string | Das Ergebnis enthält die PM-ID der entsprechenden Aufweckquelle. Hinweise:  Die PM-ID für eine Wakeupquelle unterscheidet sich von der FZM-ID dadurch, das bei dir PM-ID auch interne CAS-Weckquellen unterschieden werden. |
| STAT_PMHISTORIE_HAEUFIGKEITSZAEHLER_WERT | unsigned char | Das Ergebnis enthält den Wert des Haeufigkeitszählers für die entsprechende Weckquelle, d.h. wie oft wurde das CAS durch die entsprechende Weckquelle geweckt. Wertebereich: 0: Ungültiger Wert/Häufigkeitszähler nicht ermittelbar 1-255: Anzahl der Weckvorgänge durch die Weckquelle. Der Häufigkeitszähler einer Weckquelle umfasst nur 1 Byte und kann daher überlaufen, d.h. Überschreitet derWert den Wert 255, so beginnt der Zähler wieder von vorne. |
| STAT_PMHISTORIE_HAEUFIGKEITSZAEHLER_EINH | string | Das Ergebnis enthält den Wert des Haeufigkeitszählers für die entsprechende Weckquelle, d.h. wie oft wurde das CAS durch die entsprechende Weckquelle geweckt. Wertebereich: 0: Ungültiger Wert/Häufigkeitszähler nicht ermittelbar 1-255: Anzahl der Weckvorgänge durch die Weckquelle. Der Häufigkeitszähler einer Weckquelle umfasst nur 1 Byte und kann daher überlaufen, d.h. Überschreitet derWert den Wert 255, so beginnt der Zähler wieder von vorne. |
| STAT_PMHISTORIE_BETRIEBSSEKUNDENZAEHLER_WERT | unsigned long | Das Ergebnis enthält den Wert des Betriebssekundenzählers bei dem das Weckereignis auftrat. |
| STAT_PMHISTORIE_BETRIEBSSEKUNDENZAEHLER_EINH | string | Das Ergebnis enthält den Wert des Betriebssekundenzählers bei dem das Weckereignis auftrat. |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-pm-schlafbereitschaft"></a>
### STATUS_PM_SCHLAFBEREITSCHAFT

Der Job dient zum Auslesen der Schlafbereitschaft des CAS und gibt den Status aller möglichen Einschlafverhinderer, d.h. Weckquellen (CAS-intern/extern) aus. JobHeaderFormat STATUS_PM_SCHLAFBEREITSCHAFT Diagnose-Service:	UDS $22 DID $4104

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PM_SCHLAFBEREITSCHAFT | unsigned char | Das Ergebnis gibt an, ob das CAS einschlafbereit ist oder nicht. Dabei wird Wachbleiben aufgrund von gerade laufender Tester-Diagnose nicht berücksichtigt. 0 = Einschlafbereit 1 = Nicht Einschlafbereit, mindestens ein WUP-Quelle hält das CAS aktuell wach. |
| STAT_PM_ANZAHL_ERGEBNISSAETZE_WERT | unsigned char | Anzahl der Weckquellen, die das CAS prinzipiell wachhalten können. Je nach dieser Anzahl n (n = 1, 2, ...) existieren n mal folgende Results in einem eigenen EDIABAS-Ergebnis-Satz erstellt. STAT_PM_ID_WECKQUELLE STAT_PM_RESTZEIT_SCHLAFBEREITSCHAFT_WERT STAT_PM_HAEUFIGKEITSZAEHLER |
| STAT_PM_ANZAHL_ERGEBNISSAETZE_EINH | string | Anzahl der Weckquellen, die das CAS prinzipiell wachhalten können. Je nach dieser Anzahl n (n = 1, 2, ...) existieren n mal folgende Results in einem eigenen EDIABAS-Ergebnis-Satz erstellt. STAT_PM_ID_WECKQUELLE STAT_PM_RESTZEIT_SCHLAFBEREITSCHAFT_WERT STAT_PM_HAEUFIGKEITSZAEHLER |
| STAT_PM_ID_WECKQUELLE | unsigned char | Das Ergebnis enthält die PM-ID der entsprechenden Aufweckquelle. Hinweise:  Die PM-ID für eine Wakeupquelle unterscheidet sich von der FZM-ID dadurch, da bei derr PM-ID auch interne CAS-Weckquellen unterschieden werden. |
| STAT_PM_ID_WECKQUELLE_TEXT | string | Das Ergebnis enthält die PM-ID der entsprechenden Aufweckquelle. Hinweise:  Die PM-ID für eine Wakeupquelle unterscheidet sich von der FZM-ID dadurch, das bei dir PM-ID auch interne CAS-Weckquellen unterschieden werden. |
| STAT_PM_ID_FLAGS | unsigned char | Das Ergebnis enthält die FLAGS der entsprechenden Aufweckquelle. |
| STAT_PM_RESTZEIT_SCHLAFBEREITSCHAFT_WERT | unsigned int | Das Ergebnis enthält die Restzeit, die die entsprechende Weckquelle das CAS noch wachhält. Hinweise: Ist der Wert &gt; 0, so verhindert diese Weckquelle das Einschlafen noch mindestens für die angegebene Anzahl Millisekunden. |
| STAT_PM_RESTZEIT_SCHLAFBEREITSCHAFT_EINH | string | Das Ergebnis enthält die Restzeit, die die entsprechende Weckquelle das CAS noch wachhält. Hinweise: Ist der Wert &gt; 0, so verhindert diese Weckquelle das Einschlafen noch mindestens für die angegebene Anzahl Millisekunden. |
| STAT_PM_HAEUFIGKEITSZAEHLER_WERT | unsigned char | Das Ergebnis enthält den Wert des Haeufigkeitszählers für die entsprechende Weckquelle, d.h. wie oft wurde das CAS durch die entsprechende Weckquelle bereits geweckt. Hinweise: Der Häufigkeitszähler einer Weckquelle umfasst 1 Byte und kann überlaufen. D.h. Überschreitet derWert den Wert 255, so beginnt der Zähler wieder von vorne. |
| STAT_PM_HAEUFIGKEITSZAEHLER_EINH | string | Das Ergebnis enthält den Wert des Haeufigkeitszählers für die entsprechende Weckquelle, d.h. wie oft wurde das CAS durch die entsprechende Weckquelle bereits geweckt. Hinweise: Der Häufigkeitszähler einer Weckquelle umfasst 1 Byte und kann überlaufen. D.h. Überschreitet derWert den Wert 255, so beginnt der Zähler wieder von vorne. |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-startcyc-cnt"></a>
### _STATUS_STARTCYC_CNT

Jobbeschreibung:	Der Job dient zum Auslesen des Startzykluszählers. Hinweis: Der Startzykluszähler zählt die Anzahl der erfolgreichen Motorstarts. Vorbedingungen:		keine Diagnose-Service:	UDS Diagnose-Service:	UDS $22 DID $4205 Gültigkeit:			Ab F001-08-09-300 Kommentare:			JobHeaderFormat.Nicht in der Diagnose-Datenbank erfasst!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STARTCYC_CNT_WERT | binary | Beschreibung:	Das Ergebnis enthält den Wert des Startzykluszählers. Datenlänge: 	4 Byte Gültige Werte: 	0x00000000 - 0xFFFFFFFF = Hexadezimaler Wert des counters Einheit:		hex |
| STAT_STARTCYC_CNT_EINH | string | Beschreibung:	Einheit der Result STAT_STARTCYC_CNT_WERT Datenlänge: 	3 Byte Gültige Werte: 	"hex" |
| JOB_STATUS | string | Beschreibung: 	Status der Jobverarbeitung Gültige Werte: 	OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Beschreibung:	Hex-Auftrag an SG |
| _RESPONSE | binary | Beschreibung:	Hex-Antwort von SG |

<a id="job-steuern-cas-init-kennung"></a>
### _STEUERN_CAS_INIT_KENNUNG

Jobbeschreibung:	Der Job dient zum Verriegeln bzw. Entriegeln des CAS für das Schlüsselanlernen Vorbedingungen:		keine Diagnose-Service:	UDS $2E DID $4001 Gültigkeit:			Ab F001-08-09-300 Kommentare:			JobHeaderFormat.Nicht in der Diagnose-Datenbank erfasst!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAS_INIT | string | Beschreibung:		Das Argument dient zum Verriegeln des CAS hinsichtlich des Anlernens von Schlüsseln. Datenlänge: 		3 Byte Gültige Werte: 		0xAAAAAA = CAS für Schlüssel anlernen sperren Alle anderen Werte = CAS für Schlüssel anlernen freischalten Einheit:			hex |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Beschreibung: 		Status der Jobverarbeitung Gültige Werte: 		OKAY 					= Fehlerfrei ERROR_FORMAT_ARGUMENT 	= Fehler, da Argument nicht in einem der folgenden unterstützten Formate "0x01,0x02,0x03" oder"01,02,03" oder "0x01 0x02 0x03" oder "01 02 03" ERROR_LEN_ARGUMENT 		= Fehler, da noch Daten übrig oder fehlen (Argument insgesamt zu lang oder zu kurz) ERROR_ARGUMENT			= Fehler, da dem Job kein Argument übergeben wurde table JobResult 	STATUS_TEXT |
| _REQUEST | binary | Beschreibung: 		Hex-Auftrag an SG |
| _RESPONSE | binary | Beschreibung:		Hex-Antwort von SG |

<a id="job-steuern-startcyc-cnt"></a>
### _STEUERN_STARTCYC_CNT

Jobbeschreibung:	Der Job dient zum Schreiben des Startzykluszählers. Hinweis: Der Startzykluszähler zählt die Anzahl der erfolgreichen Motorstarts. Vorbedingungen:		keine Diagnose-Service:	UDS Diagnose-Service:	UDS $2E DID $4205 Gültigkeit:			Ab F001-08-09-300 Kommentare:			JobHeaderFormat.Nicht in der Diagnose-Datenbank erfasst!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STARTCYC_CNT | string | Beschreibung:		Das Argument enthält den zu setzten Wert für den Startzykluszählers. Datenlänge: 		4 Byte Gültige Werte: 		0x00000000 - 0xFFFFFFFF = Hexadezimaler Wert des Startzykluszählers Einheit:			hex |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Beschreibung: 		Status der Jobverarbeitung Gültige Werte: 		OKAY 					= Fehlerfrei ERROR_FORMAT_ARGUMENT 	= Fehler, da Argument nicht in einem der folgenden unterstützten Formate "0x01,0x02,0x03,0x04" oder"01,02,03,04" oder "0x01 0x02 0x03 0x04" oder "01 02 03 04" ERROR_LEN_ARGUMENT 		= Fehler, da noch Daten übrig oder fehlen (Argument insgesamt zu lang oder zu kurz) ERROR_ARGUMENT			= Fehler, da dem Job kein Argument übergeben wurde table JobResult 	STATUS_TEXT |
| _REQUEST | binary | Beschreibung:		Hex-Auftrag an SG |
| _RESPONSE | binary | Beschreibung:		Hex-Antwort von SG |

<a id="job-status-cas-anlieferzustand"></a>
### STATUS_CAS_ANLIEFERZUSTAND

Dieser Job liefert den aktuellen Fortschritt des Rücksetzen nach STEUERN_CAS_ANLIEFERZUSTAND. JobHeaderFormat STATUS_CAS_ANLIEFERZUSTAND Diagnose-Service:	UDS $22 DID $4003

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EEBLOCKS_TODO | int | Liefert die Anzahl der noch zu löschenden Blöcke im CAS. Bei 0 ist löschen fertig. Bei -1 wurde kein löschen in diesem Alive-Zyklus durchgeführt. Bei &gt;0: Anzahl noch zu löschender Blöcke |
| STAT_EEBLOCKS_TODO_TEXT | string | Liefert die Anzahl der noch zu löschenden Blöcke im CAS. Bei 0 ist löschen fertig. Bei -1 wurde kein löschen in diesem Alive-Zyklus durchgeführt. Bei &gt;0: Anzahl noch zu löschender Blöcke |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cas-freq-type"></a>
### STATUS_CAS_FREQ_TYPE

Konfiguration des CAS bzgl. Schlüssel-Initialisierung auslesen. JobHeaderFormat STATUS_CAS_FREQ_TYPE Diagnose-Service:	UDS $22 DID $4202

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INIT_FREQ | unsigned char | Kennzahl Schlüssel-Frequenz (1 Byte) 0: Unbekannte oder keine Schlüssel-Frequenz 1 - n: Werte für Frequenzen: 6 -&gt; 868MHz, 5 -&gt; 433MHz, 4 -&gt; 315MHz, 3 -&gt; 315MHz LowPower (Japan/Korea). Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| STAT_INIT_FREQ_TEXT | string | Kennzahl Schlüssel-Frequenz (1 Byte) 0: Unbekannte oder keine Schlüssel-Frequenz 1 - n: Werte für Frequenzen: 6 -&gt; 868MHz, 5 -&gt; 433MHz, 4 -&gt; 315MHz, 3 -&gt; 315MHz LowPower (Japan/Korea). Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| STAT_TRSP_TYPE | unsigned char | Art der verwendeten Transponder 1 = 'HT2' alt L2, 2 = 'HT3' neu L6 (default) |
| STAT_TRSP_TYPE_TEXT | string | Art der verwendeten Transponder 1 = 'HT2' alt L2, 2 = 'HT3' neu L6 (default) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cas-init-loc-date"></a>
### STATUS_CAS_INIT_LOC_DATE

Konfiguration des CAS bzgl. Schlüssel-Initialisierung auslesen. JobHeaderFormat STATUS_CAS_INIT_LOC_DATE Diagnose-Service:	UDS $22 DID $4203

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INIT_DAY_WERT | unsigned int | Tag der CAS-/Schlüssel-Initialisierung 1 - 31 Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| STAT_INIT_DAY_EINH | string | Tag der CAS-/Schlüssel-Initialisierung 1 - 31 Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| STAT_INIT_MONTH_WERT | unsigned int | Monat der CAS-/Schlüssel-Initialisierung 1 - 12 Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| STAT_INIT_MONTH_EINH | string | Monat der CAS-/Schlüssel-Initialisierung 1 - 12 Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| STAT_INIT_YEAR_WERT | unsigned int | Jahr der CAS-/Schlüssel-Initialisierung 2000 - 2999 Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| STAT_INIT_YEAR_EINH | string | Jahr der CAS-/Schlüssel-Initialisierung 2000 - 2999 Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| STAT_INIT_LOCATION_WERT | string | Ort der Schlüssel-Initialisierung (4 Zeichen ASCII) 0240 = Werk 2.4, 0220 =Werk 2.2, 0100 =Werk München, ... Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| STAT_INIT_LOCATION_EINH | string | Ort der Schlüssel-Initialisierung (4 Zeichen ASCII) 0240 = Werk 2.4, 0220 =Werk 2.2, 0100 =Werk München, ... Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| STAT_INIT_STATION_WERT | string | BMW-Spezifisch (4 Zeichen ASCII, z.B. Anlagennummer, Kennung für Nacharbeit, ...). Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| STAT_INIT_STATION_EINH | string | BMW-Spezifisch (4 Zeichen ASCII, z.B. Anlagennummer, Kennung für Nacharbeit, ...). Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cas-wup"></a>
### STATUS_CAS_WUP

4-Byte FBD-Wakeup-Pattern lesen. JobHeaderFormat STATUS_CAS_WUP Diagnose-Service:	UDS $22 DID $4204

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FBD_WAKEUP_WERT | binary | FBD-Wakeup-Pattern (4 Byte) Z.B. "01234567" Im Anlieferzustand "FFFFFFFF" |
| STAT_FBD_WAKEUP_EINH | string | FBD-Wakeup-Pattern (4 Byte) Z.B. "01234567" Im Anlieferzustand "FFFFFFFF" |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Job zum Auslesen digitaler Stati JobHeaderFormat 0xF3A5 _STATUS_DIG_INPUT_START_STOP (A_S_START, BLS_MSA) 0xF3A6 _STATUS_DIG_INPUT_HALL (HALL_SSTA, HALL_SSTB) 0xF3A8 _STATUS_DIG_INPUT_SCHALTER (CLT, MHK, HOTEL, MSA, TOEHKL) 0xF3A9 _STATUS_DIG_INPUT_BREMSE_KUPPL (BLTS, PN_KUPPL)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EIN_HALL_SSTA_AKTIV | unsigned char | Status des SST Hall-Sensors A (entprellt), 0 nicht aktiv, 1 aktiv |
| STAT_EIN_HALL_SSTB_AKTIV | unsigned char | Status des SST Hall-Sensors B (entprellt), 0 nicht aktiv, 1 aktiv |
| STAT_EIN_SCHALTER_KUPPL_PN_AKTIV | unsigned char | HW Taster Kupplungsschalter, 1 Taster gerückt / PN eingelegt, 0 Taster nicht gedrückt, 3 Signal ungültig / unplausibel |
| STAT_EIN_SCHALTER_KUPPL_PN_AKTIV_TEXT | string | HW Taster Kupplungsschalter, 1 Taster gerückt / PN eingelegt, 0 Taster nicht gedrückt, 3 Signal ungültig / unplausibel |
| STAT_EIN_SCHALTER_BREMSL_HIGH_AKTIV | unsigned char | HW Taster Bremslichtschalter, 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Taster nicht vorhanden (kein Automatik-Getriebe), 3 Signal ungültig / unplausibel |
| STAT_EIN_SCHALTER_BREMSL_HIGH_AKTIV_TEXT | string | HW Taster Bremslichtschalter, 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Taster nicht vorhanden (kein Automatik-Getriebe), 3 Signal ungültig / unplausibel |
| STAT_EIN_TASTER_CENTERLOCK_AKTIV | unsigned char | HW Taster Centerlock, 1 Taster gerückt, 0 Taster nicht gedrückt, 3 Signal ungültig / unplausibel |
| STAT_EIN_TASTER_CENTERLOCK_AKTIV_TEXT | string | HW Taster Centerlock, 1 Taster gerückt, 0 Taster nicht gedrückt, 3 Signal ungültig / unplausibel |
| STAT_EIN_SCHALTER_MOTORHAUBE_AKTIV | unsigned char | Motorhauben-Kontakt, 1 aktiv (offen), 0 nicht aktiv (geschlossen), 2 Fahrzeug besitzt keinen Motorhaubenkontakt, 3 Signal ungültig / unplausibel |
| STAT_EIN_SCHALTER_HOTEL_AKTIV | unsigned char | Hotelschalter, 1 Hotelfunktion aktiv, 0 Hotelfunktion nicht aktiv, 2 Fahrzeug besitzt keinen Hotelschalter, 3 Signal ungültig / unplausibel |
| STAT_EIN_SCHALTER_HOTEL_AKTIV_TEXT | string | Hotelschalter, 1 Hotelfunktion aktiv, 0 Hotelfunktion nicht aktiv, 2 Fahrzeug besitzt keinen Hotelschalter, 3 Signal ungültig / unplausibel |
| STAT_EIN_TASTER_MSA_AKTIV | unsigned char | Taster MSA, 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Fahrzeug besitzt keinen Taster, 3 Signal ungültig / unplausibel |
| STAT_EIN_TASTER_MSA_AKTIV_TEXT | string | Taster MSA, 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Fahrzeug besitzt keinen Taster, 3 Signal ungültig / unplausibel |
| STAT_EIN_TASTER_SICHERN_HECKKL_AKTIV | unsigned char | HW TasterSichern an der HKL 1 Taster gedrückt, 0 Taster nicht gedrückt, 3 Signal ungültig / unplausibel |
| STAT_EIN_TASTER_SICHERN_HECKKL_AKTIV_TEXT | string | HW TasterSichern an der HKL 1 Taster gedrückt, 0 Taster nicht gedrückt, 3 Signal ungültig / unplausibel |
| STAT_EIN_TASTER_HECKKL_INNEN_AKTIV | unsigned char | Heckklappentaster innen, 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Fahrzeug besitzt keinen Taster, 3 Signal ungültig / unplausibel |
| STAT_EIN_TASTER_HECKKL_INNEN_AKTIV_TEXT | string | Heckklappentaster innen, 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Fahrzeug besitzt keinen Taster, 3 Signal ungültig / unplausibel |
| STAT_EIN_MOST_WUP_AKTIV | unsigned char | MOST_WUP von TCU, 1 Spannung liegt an, 0 Ausgang abgeschaltet |
| STAT_EIN_A_S_START_AKTIV | unsigned char | DME_START_ENDE, 1 Spannung liegt an, 0 Ausgang abgeschaltet |
| STAT_EIN_SCHALTER_BREMSL_LOW_AKTIV | unsigned char | HW Taster Bremslichtschalter (Test-Schalter), 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Taster nicht vorhanden (kein Automatik-Getriebe), 3 Signal ungültig / unplausibel |
| STAT_EIN_SCHALTER_BREMSL_LOW_AKTIV_TEXT | string | HW Taster Bremslichtschalter (Test-Schalter), 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Taster nicht vorhanden (kein Automatik-Getriebe), 3 Signal ungültig / unplausibel |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-egs-isn"></a>
### STATUS_EGS_ISN

Verriegelungs-Status für EGS-ISN im CAS lesen (wird für Getriebe-EWS genutzt) JobHeaderFormat STATUS_EGS_ISN Diagnose-Service:	UDS $22 DID $4300

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EGS_ISN_WERT | binary | Aktueller EGS-ISN (4 Byte) zur Anbindung vom EGS Falls kein Schlüssel vorhanden oder nicht implementiert "FFFFFFFF". Falls Schlüssel bereits verriegelt ist "00000000". |
| STAT_EGS_ISN_EINH | string | Aktueller EGS-ISN (4 Byte) zur Anbindung vom EGS Falls kein Schlüssel vorhanden oder nicht implementiert "FFFFFFFF". Falls Schlüssel bereits verriegelt ist "00000000". |
| STAT_EGS_ISN_LOCKED | unsigned char | Aktueller Verriegelungs-Status für EGS-ISN: 0 = unlocked, 1 = locked |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ews"></a>
### STATUS_EWS

Liefert den aktuellen Status der EWS-SecretKeys ISNs und den Status bzgl. KeyID KeyPIN JobHeaderFormat STATUS_EWS_CAS Diagnose-Service:	UDS $22 DID $C000

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS_EGS_ACTIVE | unsigned char | 0: Das CAS ist nicht auf EWS_EGS konfiguriert, 1: Das CAS ist auf EWS_EGS konfiguriert (EGS-ISN wird nach verlassen des KL50-Montagemodus und verriegeln des TRSP_SK gesendet). Anmerkung: Gibt das über Codierung gesetzte Flag aus. |
| STAT_TRSP_SK_LOCKED | unsigned char | 0: TRSP-SecretKey lässt sich noch direkt schreiben/lesen, 1: TRSP-SecretKey lässt sich nicht mehr schreiben/lesen (EWS4-TRSP-SecretKey bereits verriegelt) Hinweis: Hierdurch wird auch der Schreibzugriff auf die Transponder-Tabelle (TRSP-IDs) und Fahrgestellnummer gesperrt! |
| STAT_DMEDDE_SK_LOCKED | unsigned char | 0: EWS4_DMEDDE-SecretKey und EGS-ISN lässt sich noch direkt schreiben/lesen, 1: EWS4_DMEDDE-SecretKey und/oder EWS3-ISN lässt sich nicht mehr schreiben/lesen (DMEDDE-Anbindung ist bereits verriegelt) Hinweis: Dieser SecretKey lässt sich erst nach dem TRSP-SK verriegeln! |
| STAT_VERSION | int | Version der EWS4-Schnittstelle, 0x01: Direktschreiben des SecretKey (alter Ablauf L1,L2,L3,L4 heute), 0x02: Direktschreiben des SecretKey ohne keyPIN (bisheriger Planstand F01) 0x03 Direktschreiben des SecretKey mit keyPIN (Ziel F01) |
| _STAT_DMEDDE_SK | int | Beschreibung:		Liefert den internen CAS-Status zum SecretKey DME/DDE (EWS-Server) Datenlänge: 		1 Byte Gültige Werte: 		0xFF = KEY_STATE_CLEARED 0xEE = START_RND 0xDD = INIT_RND1 0xCC = INIT_RND2 0xBB = WAIT_WR_RND 0xAA = CALC_FACTOR 0x9E = WAIT_FSC_UNLOCKED 0x9D = WAIT_FSC 0x9B = WAIT_FSC_KEYREADY 0x8E = CHECK_FSC_UNLOCKED 0x8D = CHECK_FSC 0x8B = CHECK_FSC_KEYREADY 0x77 = CALC_KEY 0x66 = COMPRESS_KEY 0x5E = RND_KEY 0x5D = SEND_RPLY_KEY 0x00 = KEY_READY Einheit:			- |
| _STAT_TRSP_SK | int | Beschreibung:		Liefert den internen CAS-Status zum SecretKey Transponder (EWS-Client) Datenlänge: 		1 Byte Gültige Werte: 		0xFF = KEY_STATE_CLEARED 0xEE = START_RND 0xDD = INIT_RND1 0xCC = INIT_RND2 0xBB = WAIT_WR_RND 0xAA = CALC_FACTOR 0x9E = WAIT_FSC_UNLOCKED 0x9D = WAIT_FSC 0x9B = WAIT_FSC_KEYREADY 0x8E = CHECK_FSC_UNLOCKED 0x8D = CHECK_FSC 0x8B = CHECK_FSC_KEYREADY 0x77 = CALC_KEY 0x66 = COMPRESS_KEY 0x5E = RND_KEY 0x5D = SEND_RPLY_KEY 0x00 = KEY_READY Einheit:			- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ews4-sk"></a>
### STATUS_EWS4_SK

Dieser Job dient zum (Gegen-)Lesen der Secretkeys / ISNs (vor einem anschließenden Verriegeln Kommando) JobHeaderFormat STATUS_EWS4_SK_CAS Diagnose-Service:	UDS $22 DID $C002

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS4_TRSP_SK | binary | Aktueller SecretKey (jeweils 16 Byte) des EWS4-Clients zur Anbindung der Transponder-Schlüssel (dient zur Erzeugung der SessionKeys) Falls kein Schlüssel vorhanden oder nicht implementiert "FFFF....FFFF". Falls Schlüssel bereits verriegelt ist "0000....0000" |
| STAT_EWS4_TRSP_SK_EINH | string | Aktueller SecretKey (jeweils 16 Byte) des EWS4-Clients zur Anbindung der Transponder-Schlüssel (dient zur Erzeugung der SessionKeys) Falls kein Schlüssel vorhanden oder nicht implementiert "FFFF....FFFF". Falls Schlüssel bereits verriegelt ist "0000....0000" |
| STAT_EWS4_DMEDDE_SK | binary | "Aktueller SecretKey (jeweils 16 Byte) des EWS4-Servers zur Anbindung einer EWS4-DME/DDE Falls kein Schlüssel vorhanden oder nicht implementiert ""FFFF....FFFF"". Falls Schlüssel bereits verriegelt ist ""0000....0000"". |
| STAT_EWS4_DMEDDE_SK_EINH | string | "Aktueller SecretKey (jeweils 16 Byte) des EWS4-Servers zur Anbindung einer EWS4-DME/DDE Falls kein Schlüssel vorhanden oder nicht implementiert ""FFFF....FFFF"". Falls Schlüssel bereits verriegelt ist ""0000....0000"". |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-fahrgestellnummer"></a>
### STATUS_FAHRGESTELLNUMMER

Lesen der Fahrgestellnummer JobHeaderFormat STATUS_FAHRGESTELLNUMMER Diagnose-Service:	UDS $22 DID $F190

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FGNR17_WERT | string | 17-Stellige Fahrgestellnummer '00000000000000000' bei keine Fahrgestellnummer vorhanden (jungfräuliches Steuergerät). |
| STAT_FGNR17_EINH | string | 17-Stellige Fahrgestellnummer '00000000000000000' bei keine Fahrgestellnummer vorhanden (jungfräuliches Steuergerät). |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-schluessel-trsp"></a>
### STATUS_SCHLUESSEL_TRSP

Liefert den Status des momentan in der Ringspule befindlichen Schlüssels. Der Job liefert den Status des zuletzt gefundenen Transponders in der Ringspule. Die Daten sind max. 300 ms alt und entprellt (bei dauerhaft vorhandenem Transponder, keine flackernden Results). Ist der Schlüssel unbekannt und bereits gelocked, so werden nur die immer lesbaren Informationen ausgegeben. JobHeaderFormat STATUS_SCHLUESSEL_TRSP Diagnose-Service:	UDS $22 DID $4200

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TAB_INDEX | int | 255 Aktuelle Schlüssel-ID konnte keiner Position im CAS zugeordnet werden. 0 - 9 Erkannte Schlüssel-Position in der Schlüssel-Tabelle, 255 unbekannt |
| STAT_TAB_INDEX_TEXT | string | 255 Aktuelle Schlüssel-ID konnte keiner Position im CAS zugeordnet werden. 0 - 9 Erkannte Schlüssel-Position in der Schlüssel-Tabelle, 255 unbekannt |
| STAT_KEY_DISABLED | int | Status ob aktueller Schlüssel im CAS gesperrt (disabled) ist. 0: Aktueller Schlüssel nicht gesperrt oder unbekannt 1: Aktueller Schlüssel gesperrt 2: Aktueller Schlüssel temporär gesperrt (CA-Funktion) |
| STAT_KEY_DISABLED_TEXT | string | Status ob aktueller Schlüssel im CAS gesperrt (disabled) ist. 0: Aktueller Schlüssel nicht gesperrt oder unbekannt 1: Aktueller Schlüssel gesperrt 2: Aktueller Schlüssel temporär gesperrt (CA-Funktion) |
| STAT_KEY_VALID | int | 0: Aktueller Schlüssel ungültig, unbekannt oder gesperrt 1: Aktueller Schlüssel gültig (authentisiert) |
| STAT_KEY_CAM_NR | int | 0 ... 7: ID-Geber Nummer (Codierbar: 0 ... 1, 0 ... 3, 0 ... 7) 255: bei kein ID-Geber |
| STAT_KEY_CAM_NR_TEXT | string | 0 ... 7: ID-Geber Nummer (Codierbar: 0 ... 1, 0 ... 3, 0 ... 7) 255: bei kein ID-Geber |
| STAT_TRSP_ERROR | int | Kommunikations-Fehler und Anlernfehler 0 kein Fehler 1 Keine Ringspule 2 Lesefehler Page 0 (nach retries) 3 Lesefahler TRSP_TYP ... Weitere Werte siehe Liste Jan Vastl |
| STAT_TRSP_ERROR_TEXT | string | Kommunikations-Fehler und Anlernfehler 0 kein Fehler 1 Keine Ringspule 2 Lesefehler Page 0 (nach retries) 3 Lesefahler TRSP_TYP ... Weitere Werte siehe Liste Jan Vastl |
| STAT_KEY_PIA_NR | int | 15 Keine personalisierung zugewiesen oder Schlüssel unbekannt 0 - 2 Erkannte Schlüssel-Personalisierung in der Schlüssel-Tabelle 3 keine/default Personalisierung |
| STAT_KEY_PIA_NR_TEXT | string | 15 Keine personalisierung zugewiesen oder Schlüssel unbekannt 0 - 2 Erkannte Schlüssel-Personalisierung in der Schlüssel-Tabelle 3 keine/default Personalisierung |
| STAT_KEY_PARTNUMBER_WERT | string | 7-stellige Sachnummer des Schlüssels bzw. der Gleichschliessung. (6-Byte BCD dekodiert, ggf. führende Nullen) |
| STAT_KEY_PARTNUMBER_EINH | string | 7-stellige Sachnummer des Schlüssels bzw. der Gleichschliessung. (6-Byte BCD dekodiert, ggf. führende Nullen) |
| STAT_KEY_VIN17_WERT | string | 17-Stellige Fahrgestellnummer aus dem Schlüssel '00000000000000000' bei keine Fahrgestellnummer vorhanden (jungfräulicher Schlüssel). 'FFFFFFFFFFFFFFFF' bei Fahrgestellnummer nicht lesbar (falls notwendig). |
| STAT_KEY_VIN17_EINH | string | 17-Stellige Fahrgestellnummer aus dem Schlüssel '00000000000000000' bei keine Fahrgestellnummer vorhanden (jungfräulicher Schlüssel). 'FFFFFFFFFFFFFFFF' bei Fahrgestellnummer nicht lesbar (falls notwendig). |
| STAT_KEY_FREQ | int | Kennzahl Schlüssel-Frequenz (1 Byte) 0: Unbekannte oder keine Schlüssel-Frequenz (Drivers-Key, Wallet-Key) 1 - n: Werte für Frequenzen 6 -&gt; 868MHz 5 -&gt; 433MHz 4 -&gt; 315MHz 3 -&gt; 315MHz LowPower (Japan/Korea) |
| STAT_KEY_FREQ_TEXT | string | Kennzahl Schlüssel-Frequenz (1 Byte) 0: Unbekannte oder keine Schlüssel-Frequenz (Drivers-Key, Wallet-Key) 1 - n: Werte für Frequenzen 6 -&gt; 868MHz 5 -&gt; 433MHz 4 -&gt; 315MHz 3 -&gt; 315MHz LowPower (Japan/Korea) |
| STAT_KEY_ID_WERT | binary | ID des aktuellen Schlüssels (z.B. '12 34 AB EF'). |
| STAT_KEY_ID_EINH | string | ID des aktuellen Schlüssels (z.B. '12 34 AB EF'). |
| STAT_KEY_ID_KNOWN | int | 1: Aktueller Schlüssel ist dem CAS bekannt 0: Aktueller Schlüssel ist dem CAS unbekannt |
| STAT_KEY_SUPPLIER_YEAR_WERT | int | Jahr des Herstelldatums (im Schlüssel nicht mehr änderbar) 2000 - 2999 |
| STAT_KEY_SUPPLIER_YEAR_EINH | string | Jahr des Herstelldatums (im Schlüssel nicht mehr änderbar) 2000 - 2999 |
| STAT_KEY_SUPPLIER_ID_WERT | unsigned char | Herstellungsort (im Schlüssel nicht mehr änderbar, 1Byte) Z.B. Lieferanten-Kennung |
| STAT_KEY_SUPPLIER_ID_WERT_TEXT | string | Herstellungsort (im Schlüssel nicht mehr änderbar, 1Byte) Z.B. Lieferanten-Kennung |
| STAT_KEY_SUPPLIER_MONTH_WERT | int | Monat des Herstelldatums (im Schlüssel nicht mehr änderbar) 1 - 12 |
| STAT_KEY_SUPPLIER_MONTH_EINH | string | Monat des Herstelldatums (im Schlüssel nicht mehr änderbar) 1 - 12 |
| STAT_KEY_SUPPLIER_STATION_WERT | int | Zulieferer-Spezifisch (z.B. Anlagennummer, Scharschennummer, ....) (im Schlüssel nicht mehr änderbar, 2 Byte) |
| STAT_KEY_SUPPLIER_STATION_EINH | string | Zulieferer-Spezifisch (z.B. Anlagennummer, Scharschennummer, ....) (im Schlüssel nicht mehr änderbar, 2 Byte) |
| STAT_KEY_SUPPLIER_DAY_WERT | int | Tag des Herstelldatums (im Schlüssel nicht mehr änderbar) 1 - 31 |
| STAT_KEY_SUPPLIER_DAY_EINH | string | Tag des Herstelldatums (im Schlüssel nicht mehr änderbar) 1 - 31 |
| STAT_KEY_MECHCODE_WERT | string | 5 Stellen des Mechanischen Schliesscodes (letzte Stelle ist CS) '00000' bei kein Schliesscode vorhanden (FBD-/PA-Schlüssel) Dieser Mechcode wird beim Zulieferer geschrieben. Der Schliesscode wird im CAS nicht gespeichert. |
| STAT_KEY_MECHCODE_EINH | string | 5 Stellen des Mechanischen Schliesscodes (letzte Stelle ist CS) '00000' bei kein Schliesscode vorhanden (FBD-/PA-Schlüssel) Dieser Mechcode wird beim Zulieferer geschrieben. Der Schliesscode wird im CAS nicht gespeichert. |
| STAT_KEY_MECHCODE_VALID | int | 1: Schliesscode plausibel 0: Schliesscode ungültig (CS falsch, unzulässige Werte, ...). Der Schliesscode wird im CAS nicht gespeichert. |
| STAT_KEY_INIT_YEAR_WERT | int | Jahr der Schlüssel-Initialisierung (im Schlüssel nicht mehr änderbar) 2000 - 2999 |
| STAT_KEY_INIT_YEAR_EINH | string | Jahr der Schlüssel-Initialisierung (im Schlüssel nicht mehr änderbar) 2000 - 2999 |
| STAT_KEY_INIT_LOCATION_WERT | string | Ort der Schlüssel-Initialisierung (im Schlüssel nicht mehr änderbar, 4 Byte) (definition Helmut Wagatha) 24: Werk 2.4 22: Werk 2.2 1: Werk München Bei Anlernen über FSC evtl. Händler-Nummer |
| STAT_KEY_INIT_LOCATION_EINH | string | Ort der Schlüssel-Initialisierung (im Schlüssel nicht mehr änderbar, 4 Byte) (definition Helmut Wagatha) 24: Werk 2.4 22: Werk 2.2 1: Werk München Bei Anlernen über FSC evtl. Händler-Nummer |
| STAT_KEY_INIT_MONTH_WERT | int | Monat der Schlüssel-Initialisierung (im Schlüssel nicht mehr änderbar):  1 = Januar, usw - 12 |
| STAT_KEY_INIT_MONTH_EINH | string | Monat der Schlüssel-Initialisierung (im Schlüssel nicht mehr änderbar):  1 = Januar, usw - 12 |
| STAT_KEY_INIT_STATION_WERT | string | BMW-Spezifisch (z.B. Anlagennummer , Händlernummer)  (im Schlüssel nicht mehr änderbar, 4-Byte) |
| STAT_KEY_INIT_STATION_EINH | string | BMW-Spezifisch (z.B. Anlagennummer , Händlernummer)  (im Schlüssel nicht mehr änderbar, 4-Byte) |
| STAT_KEY_INIT_DAY_WERT | int | Tag der Schlüssel-Initialisierung (im Schlüssel nicht mehr änderbar) 1 - 31 |
| STAT_KEY_INIT_DAY_EINH | string | Tag der Schlüssel-Initialisierung (im Schlüssel nicht mehr änderbar) 1 - 31 |
| STAT_KEY_TYPE | int | Schlüssel-Typ (4 Bit) 0: Dummy-Schlüssel bzw. Umlaufschlüssel 2: Geldbörsen-Schlüssel 3: Drivers-Key 4: Funk-Schlüssel 5: ID-Geber 15: Unbekannter Schlüssel-Typ |
| STAT_KEY_TYPE_TEXT | string | Schlüssel-Typ (4 Bit) 0: Dummy-Schlüssel bzw. Umlaufschlüssel 2: Geldbörsen-Schlüssel 3: Drivers-Key 4: Funk-Schlüssel 5: ID-Geber 15: Unbekannter Schlüssel-Typ |
| STAT_FBD_BATTERIE_ZUSTAND | unsigned char | Quantisierte Batterie-Spannung des Schlüssels. 0 sehr schlecht, 6 sehr gut, 10 Status Battrie Schwach (bei Kommunikation ohne Authentisierung), 11 Status Battrie Gut (bei Kommunikation ohne Authentisierung), 255 nicht ermittelbar bzw. nicht relevant |
| STAT_FBD_BATTERIE_ZUSTAND_TEXT | string | Quantisierte Batterie-Spannung des Schlüssels. 0 sehr schlecht, 6 sehr gut, 10 Status Battrie Schwach (bei Kommunikation ohne Authentisierung), 11 Status Battrie Gut (bei Kommunikation ohne Authentisierung), 255 nicht ermittelbar bzw. nicht relevant |
| STAT_KEY_VARIANT | int | Variante des Schlüssels. Zur späteren unterscheidung von Änderungen. (4-Bit) Am Anfang z.B. 1 |
| STAT_KEY_VARIANT_TEXT | string | Variante des Schlüssels. Zur späteren unterscheidung von Änderungen. (4-Bit) Am Anfang z.B. 1 |
| STAT_KEY_LOCKED | int | Verriegelungs-Status des AES-Transponders: 0: Schlüssel noch nicht verriegelt, d.h. er lässt sich (nochmal) anlernen. 1: Schlüssel komplett verriegelt (Wegfahrsperre-Daten sind verriegelt), 2: Schlüssel ist teilweise bzgl. Wegfahrsperre verriegelt (Zwischenzustand), 3: fehlerhafte Konfiguration, Initialisierung nicht möglich, 4: Kein normaler Anlieferzustand, Schlüssel komplett offen (Anlieferzustand Philips) |
| STAT_KEY_LOCKED_TEXT | string | Verriegelungs-Status des AES-Transponders: 0: Schlüssel noch nicht verriegelt, d.h. er lässt sich (nochmal) anlernen. 1: Schlüssel komplett verriegelt (Wegfahrsperre-Daten sind verriegelt), 2: Schlüssel ist teilweise bzgl. Wegfahrsperre verriegelt (Zwischenzustand), 3: fehlerhafte Konfiguration, Initialisierung nicht möglich, 4: Kein normaler Anlieferzustand, Schlüssel komplett offen (Anlieferzustand Philips) |
| STAT_INIT_DONE | int | 1: Schlüssel vollständig angelernt 254: Schlüssel (noch) nicht angelernt (d.h. SecretKey, FBD-Konfig, VIN17, ... Noch nicht In Schlüssel übertragen und Schlüssel nicht verriegelt). 255 Unbekannter Schlüssel. |
| STAT_INIT_DONE_TEXT | string | 1: Schlüssel vollständig angelernt 254: Schlüssel (noch) nicht angelernt (d.h. SecretKey, FBD-Konfig, VIN17, ... Noch nicht In Schlüssel übertragen und Schlüssel nicht verriegelt). 255 Unbekannter Schlüssel. |
| STAT_KEY_TRSP_TYPE | int | 1 = HT2 2 = HT3/AES |
| STAT_KEY_TRSP_TYPE_TEXT | string | 1 = HT2 2 = HT3/AES |
| STAT_KEY_CAM_NR_AKTUALISIERT | unsigned char | Das Ergebnis gibt an, ob die CAM-Nr auch im Schlüssel aktualisiert wurde und nicht nur im CAS. Beim ersten Verwenden eines Ersatzschlüssels oder beim Freigeben eines Schlüssels wird die CAM-Nr (ComfortAcessMaster-Nr.) vom CAS neu berechnet. Diese muss dann auch noch im Schlüssel aktualisiert werden. 0 = CAM-Nr wurde noch nicht im Schlüssel aktualisiert 1 = CAM-Nr wurde im Schlüssel aktualisiert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-schluesseldaten"></a>
### STATUS_SCHLUESSELDATEN

Jobbeschreibung:	Dieser Job dient dazu den Status eines Schlüssel laut Transpondertabelle auszulesen. Anmerkung: Die Informationen sind unabhängig von einem evtl. gerade vorhandenen Transponder in der Ringspule bzw. einem erkannten ID-Geber. Vorbedingungen:		keine Diagnose-Service:	UDS Diagnose-Service:	UDS $22 DID $4210 Gültigkeit:			Ab F001-08-09-300 Kommentare:			Im JobHeaderFormat in der Diagnose-Datenbank angelegt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TAB_INDEX | int | Beschreibung:		Das Argument zur Auswahl der Schlüssel-Position in der Transponder-Tabelle 0 - 9 Datenlänge: 		1 Byte Gültige Werte: 		0-9 = Transponder-Tabelle Einheit:			keine |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KEY_TYPE | int | Beschreibung:		Das Result enthält den zu Typ des Schlüssels als ID Datenlänge: 		1 Byte Gültige Werte: 		0  = Umlauf-Schlüssel 2  = Geldbörsen-Schlüssel 3  = Drivers-Key 4  = Funk-Schlüssel 5  = ID-Geber Einheit:			keine |
| STAT_KEY_TYPE_TEXT | string | Beschreibung:		Das Result enthält den Typ des Schlüssels als Text Datenlänge: 		- Gültige Werte: 		"Unbekannter Schluesseltyp" = Unbekannter Schluesseltyp "Umlaufschluessel"  = Umlauf-Schlüssel "GB-Schluessel"  	= Geldbörsen-Schlüssel "Drivers Key"  		= Drivers-Key "FBD-Schluessel"  	= Funk-Schlüssel "ID-Geber"  		= ID-Geber Einheit:			keine |
| _STAT_KEY_SQCNT_UPD | int | Sequence counter update Beschreibung:		Das Result gibt an, ob der Sequence Counter, der zur Absicherung der Kommunikation Schlüssel &lt;-&gt; CAS hochgezählt wird, bei der nächsten bidirektionalen Kommunikation neu initialisiert (mit einerZufallszahl) wird. Datenlänge: 		1 Byte Gültige Werte: 		0 = Keine Initialisierung des Sequence Counter bei nächster bidirektionalen Kommunikation 1 = Neuinitialisierung des Sequence Counter bei nächster bidirektionalen Kommunikation Einheit:			keine |
| STAT_DISABLED | int | Schl. gesperrt Beschreibung:		Das Result enthält den Status, ob der Schlüssel gesperrt (disabled) ist Datenlänge: 		1 Byte Gültige Werte: 		0: Schlüssel nicht gesperrt oder unbekannt 1: Schlüssel gesperrt 2: Schlüssel temporär gesperrt (CA-Funktion) Einheit:			keine |
| STAT_CAM_NR | int | Beschreibung:		Das Result enthält die CA ID-Geber Nummer. Anmerkung: Die CA ID-Geber Nummer wird vom CAS selbständig vergeben. Datenlänge: 		1 Byte Gültige Werte: 		0-7 = CAM Nummer 255 = kein ID-Geber Einheit:			keine |
| STAT_CAM_NR_TEXT | string | Beschreibung:		Das Result enthält die CA ID-Geber Nummer als Textstring. Datenlänge: 		- Gültige Werte: 		"ID-Geber-Nummer" + CAM Nummer Einheit:			keine |
| _STAT_CAM_NR_ACT | int | Beschreibung:		Das Ergebnis gibt an, ob die CAM-Nr auch im Schlüssel aktualisiert wurde und nicht nur im CAS. Datenlänge: 		1 Byte Gültige Werte:		0 = CAM-Nr wurde noch nicht im Schlüssel aktualisiert 1 = CAM-Nr wurde im Schlüssel aktualisiert Einheit:			keine |
| STAT_INIT_DONE | int | Beschreibung:		Das Result enthält den Status des Anlernen des Schlüssels. Datenlänge: 		1 Byte Gültige Werte:		1		= Schlüssel vollständig angelernt 2-254	= Schlüssel (noch) nicht angelernt (d.h. SecretKey, FBD-Konfig, VIN17, ... Noch nicht In Schlüssel übertragen und Schlüssel nicht verriegelt). 255		= Für Ersatz-Schlüssel reserviert. Einheit:			keine |
| STAT_INIT_DONE_TEXT | string | Beschreibung:		Das Result enthält den Status des Anlernen des Schlüssels als Textstring. Datenlänge: 		- Gültige Werte:		"Angelernt"							= 1: Schlüssel vollständig angelernt "Anlernen noch nicht abgeschlossen"	= 2-254: Schlüssel (noch) nicht angelernt (d.h. SecretKey, FBD-Konfig, VIN17, ... Noch nicht In Schlüssel übertragen und Schlüssel nicht verriegelt). "Default Wert						= 255: Für Ersatz-Schlüssel reserviert. "Ungültiger Wert" 					= 0: Ungültiger Wert Einheit:			keine |
| STAT_KEY_ID_WERT | binary | Beschreibung:		Das Result enthält die zu ID des Schlüssels Datenlänge: 		4 Byte Gültige Werte: 		Alle Werte ausser FF FF FF FF = Gültige Schluessel-ID FF FF FF FF = unbekannt Einheit:			hex |
| STAT_KEY_ID_EINH | string | Beschreibung:		Enthält die Einheit des Result STAT_KEY_ID_WERT als Textstring Datenlänge: 		- Gültige Werte: 		"hex" Einheit:			keine |
| STAT_PIA_NR | int | Beschreibung:		Das Result enthält die PIA-Nr Datenlänge: 		1 Byte Gültige Werte: 		15		= Keine PIA-Nr zugewiesen oder Schlüssel unbekannt 0 - 2	= Zugewiesene PIA-Nr in der Schlüssel-Tabelle Einheit:			keine |
| STAT_PIA_NR_TEXT | string | Beschreibung:		Das Result enthält die PIA-Nr als Textstring Datenlänge: 		- Gültige Werte: 		"keine Personalisierung" 	= 15: Keine PIA-Nr zugewiesen oder Schlüssel unbekannt "Personalisierung" + Nr 	= 0-2: Zugewiesene PIA-Nr in der Schlüssel-Tabelle Einheit:			keine |
| _STAT_ROHDATEN | binary | ALLE 8 Byte ausgelesene Daten Beschreibung:		Das Result enthält den kompletten EEPROM-Datenblock des Schlüssels als 8 Byte hexadezimale Rohdaten Datenlänge: 		8 Byte Gültige Werte: 		8 Byte Hex-Wert Einheit:			hex |
| JOB_STATUS | string | Beschreibung: 		Status der Jobverarbeitung Gültige Werte: 		OKAY = Fehlerfrei table JobResult 	STATUS_TEXT |
| _REQUEST | binary | Beschreibung:		Hex-Auftrag an SG |
| _RESPONSE | binary | Beschreibung:		Hex-Antwort von SG |

<a id="job-status-cas-hw-geschwindigkeit"></a>
### STATUS_CAS_HW_GESCHWINDIGKEIT

Auslesen der vom CAS (über separate HW-Leitung vom DSC) erkannte Geschwindigkeit. JobHeaderFormat CAS_HW_GESCHWINDIGKEIT Diagnose-Service:	UDS $22 DID $DC51

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HW_SPEED_STATUS | unsigned char | HW-Geschwindigkeitssignal, 0 Unplausibel bzgl. Frequenz, 1 Unplausibel, DSC kann keinen gültigen Status senden, 2 Fahrzeug steht, 3 Rollt, 4 Fahrt V1, 5 Fahrt V2, 6 Fahrt V3 |
| STAT_HW_SPEED_STATUS_TEXT | string | HW-Geschwindigkeitssignal, 0 Unplausibel bzgl. Frequenz, 1 Unplausibel, DSC kann keinen gültigen Status senden, 2 Fahrzeug steht, 3 Rollt, 4 Fahrt V1, 5 Fahrt V2, 6 Fahrt V3 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cas-hw-variante"></a>
### STATUS_CAS_HW_VARIANTE

Hardware-Variante des CAS lesen. JobHeaderFormat CAS_HW_VARIANTE Diagnose-Service:	UDS $22 DID $DAB7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CAS_HW_VARIANTE_CG_VORHANDEN | long | CG-Funktion vorhanden ja/nein: 0 CAS4 ohne CG-Ansteuerung, 1 CAS4 mit CG-Ansteuerung |
| STAT_CAS_HW_VARIANTE_CE_VORHANDEN | long | CE-Funktion vorhanden ja/nein: 0 CAS4 ohne CE-Ansteuerung, 1 CAS4 mit CE-Ansteuerung |
| STAT_CAS_HW_VARIANTE_ELV_VORHANDEN | long | ELV vorhanden ja/nein: 0 CAS4 ohne ELV-Ansteuerung, 1 CAS4 mit ELV-Ansteuerung |
| STAT_CAS_HW_VARIANTE_KEYLOCK_VORHANDEN | long | Schlüsselverrastung (KeyLock) vorhanden ja/nein: 0 CAS4 ohne KeyLock-Ansteuerung, 1 CAS4 mit KeyKlock-Ansteuerung |
| STAT_CAS_HW_VARIANTE_BN2000 | long | BN2000 Software vorhanden ja/nein: 0 CAS4 UDS neu, 1 CAS4 BN2000-Kompatibel |
| STAT_CAS_HW_VARIANTE_FA_CAN_VORHANDEN | long | Zweiter CAN-Bus (FA-CAN) bestückt: 0 CAS4 kein FA-CAN, 1 CAS4 mit FA-CAN |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-istufe"></a>
### STATUS_ISTUFE

Liefert die im EEPROM abgelegte I-Stufe jeweils für Werk, HO und HO-Backup. JobHeaderFormat STATUS_ISTUFE Diagnose-Service:	UDS $22 DID $100B

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ISTUFE_WERK_WERT | string | Liefert die im EEPROM abgelegte Werks-I-Stufe. |
| STAT_ISTUFE_HO_WERT | string | Liefert die im EEPROM abgelegte HO-I-Stufe. |
| STAT_ISTUFE_HO_BACKUP_WERT | string | Liefert die im EEPROM abgelegte HO-Backup-I-Stufe. |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-kilometerstand"></a>
### STATUS_KILOMETERSTAND

Aufruf liefert den angezeigeten Gesamtwegstreckenzähler. Beim CAS den im EEPROM hinterlegten Wert. JobHeaderFormat STATUS_KILOMETERSTAND Diagnose-Service:	UDS $22 DID $1700

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KILOMETERSTAND_WERT | long | Liefert den absoluten Gesamtwegstreckenzähler aus dem EEPROM. |
| STAT_KILOMETERSTAND_EINH | string | Liefert den absoluten Gesamtwegstreckenzähler aus dem EEPROM. |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-cas-anlieferzustand"></a>
### STEUERN_CAS_ANLIEFERZUSTAND

Versetzt das CAS in den Anlieferzustand (Montage-Modi, Codierung, VIN, Tansponder-Tabelle, EWS4_CLIENT_SK, ...) Falls Rücksetzen unzulässig: ERROR_ECU_CONDITIONS_NOT_CORRECT. Anmerkung: Nach dem Rücksetzen müssen alle im verriegelten Zustand geschützten W JobHeaderFormat STEUERN_CAS_ANLIEFERZUSTAND Diagnose-Service:	UDS $3101 DID $AC50($4003)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EWS4_TRSP_SK | string | Falls SG verriegelt muss der geheime EWS4_TRSP_SK als Argument angegeben werden (optional). Der Job liefert immer Status 'OKAY' und dauert immer gleich lange (&lt; 5 Sekunden). Der Erfolg des Rückstzens ist anschließend nur über die anderen Status-Jobs erkennbar. (Es müssen zuallererst die Secret-Keys gelöscht werden.) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-cas-freq-type"></a>
### STEUERN_CAS_FREQ_TYPE

Konfigurationd des CAS setzen. Die Konfiguration ist nach dem Verriegeln des EWS4_SK bzw. EWS4_TRSP_SK nicht mehr änderbar (ERROR_ECU_CONDITIONS_NOT_CORRECT). Werden unzulässige Daten übergeben, so erfolgt ein ERROR_DATA. JobHeaderFormat STEUERN_CAS_FREQ_TYPE Diagnose-Service:	UDS $2E DID $4202

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INIT_FREQ | unsigned char | Kennzahl Schlüssel-Frequenz (1 Byte) 0: Unbekannte oder keine Schlüssel-Frequenz 1 - n: Werte für Frequenzen: 6 -&gt; 868MHz, 5 -&gt; 433MHz, 4 -&gt; 315MHz, 3 -&gt; 315MHz LowPower (Japan/Korea). Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| TRSP_TYPE | unsigned char | Optional: Art der verwendeten Transponder 1 = 'HT2' alt L2, 2 = 'HT3' neu L6 (default). |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-cas-init-loc-date"></a>
### STEUERN_CAS_INIT_LOC_DATE

Konfigurationd des CAS setzen. Die Konfiguration ist nach dem Verriegeln des EWS4_SK bzw. EWS4_TRSP_SK nicht mehr änderbar (ERROR_ECU_CONDITIONS_NOT_CORRECT). Werden unzulässige Daten übergeben, so erfolgt ein ERROR_DATA. JobHeaderFormat STEUERN_CAS_INIT_LOC_DATE Diagnose-Service:	UDS $2E DID $4203

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| INIT_DAY | unsigned int | Tag der CAS-/Schlüssel-Initialisierung 1 - 31 Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| INIT_MONTH | unsigned int | Monat der CAS-/Schlüssel-Initialisierung 1 - 12 Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| INIT_YEAR | unsigned int | Jahr der CAS-/Schlüssel-Initialisierung 2000 - 2999 Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| INIT_LOCATION | string | Ort der Schlüssel-Initialisierung (4 Zeichen ASCII) 0240 = Werk 2.4, 0220 =Werk 2.2, 0100 =Werk München, ... Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |
| INIT_STATION | string | BMW-Spezifisch (4 Zeichen ASCII, z.B. Anlagennummer, Kennung für Nacharbeit, ...). Dieser Wert ist nach dem Verriegeln des EWS4_TRSP_SK nicht mehr änderbar. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-cas-wup"></a>
### STEUERN_CAS_WUP

4-Byte FBD-Wakeup-Pattern schreiben. JobHeaderFormat STEUERN_CAS_WUP Diagnose-Service:	UDS $2E DID $4204

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FBD_WAKEUP | string | FBD-Wakeup-Pattern (4 Byte) Folgende Übergabe-Formate müssen unterstützt werden: "01 23 45 67" und "0x01,0x23,0x45,0x67" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-egs-isn"></a>
### STEUERN_EGS_ISN

EGS-ISN im CAS setzen (wird für Getriebe-EWS genutzt) JobHeaderFormat STEUERN_EGS_ISN Diagnose-Service:	UDS $2E DID $4300

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EGS_ISN | string | EGS-ISN (4 Byte) Folgende Übergabe-Formate müssen unterstützt werden: "01 23 45 67" und "0x01,0x23,0x45,0x67" |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ews4"></a>
### STEUERN_EWS4

Dieser Job dient zum Setzen der Secretkeys und zum anschließenden Verriegeln. JobHeaderFormat STEUERN_EWS4_CAS Diagnose-Service:	UDS $2E DID $C001

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | "WRITE_DMEDDE_SK" SecretKey des EWS4-Servers zur Anbindung einer EWS4-DME/DDE soll geschrieben werden. Argument ist der DMEDDE-SecretKey. "LOCK_DMEDDE_SK" EGS_ISN und EWS4_DMEDDE_SK soll verriegelt werden. Kein Argument. "WRITE_TRSP_SK" SecretKey des EWS4-Clients zur Anbindung der Transponder-Schlüssel soll geschrieben werden. Argument ist der TRSP-SecretKey. "LOCK_TRSP_SK" SecretKey des EWS4-Clients zur Anbindung der Transponder-Schlüssel soll verriegelt werden. Kein Argument. "LOCK_EWS4": SecretKeys der EWS4-Clients zur Anbindung der Transponder-Schlüssel und SecretKey des EWS4-Servers zur Anbindung einer EWS4-DME/DDE sollen beide verriegelt werden. Argument DATA enthält 0x00. "UNLOCK_DMEDDE_SK": NUR ENTWICKLUNG! Argument DATA muss EWS4_DMEDDE_SK enthalten, der bereits im CAS gespeichert ist! "UNLOCK_TRSP_SK": NUR ENTWICKLUNG! Argument DATA muss TRSP_SK  enthalten, der bereits im CAS gespeichert ist! |
| DATA | string | SecretKey, der geschrieben werden soll (16 Byte, Argument nur bei WRITE_xxx, kein Argument falls Mode LOCK_xxx) Folgende Formate müssen unterstützt werden: "01 23 45 67 89 AB CD EF 01 23 45 67 89 AB CD EF" und "0x01,0x23,0x45,0x67,0x89,0xAB,0xCD,0xEF,0x01,0x23,0x45,0x67,0x89,0xAB,0xCD,0xEF". (Implementierung analog CAS-&gt;STEUERN_SCHLUESSELDATEN: Argument IDENTIFIER) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST2 | binary | Beschreibung:	2. Hex-Auftrag an SG |
| _RESPONSE2 | binary | Beschreibung:	2. Hex-Antwort von SG |

<a id="job-steuern-fahrgestellnummer"></a>
### STEUERN_FAHRGESTELLNUMMER

Schreiben der Fahrgestellnummer JobHeaderFormat STEUERN_FAHRGESTELLNUMMER Diagnose-Service:	UDS $2E DID $F190

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FGNR17 | string | 17-Stellige Fahrgestellnummer. Zum Zurücksetzen im Steuergerät wird das Argument '00000000000000000' verwendet. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-schluessel-init"></a>
### STEUERN_SCHLUESSEL_INIT

Job zum Anstoßen der Schlüssel-Initialisierung. Nur zulässig, solange EWS4_TRSP_SK noch nicht verriegelt. JobHeaderFormat STEUERN_SCHLUESSEL_INIT Diagnose-Service:	UDS $3101 RID $AC52($4005)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TAB_INDEX | unsigned char | Schlüssel-Position in der Transponder-Tabelle 0 - 9, 100 THS1, 101 THS2. Folgende Sonderfunktionen sind noch möglich (ohne einen Anlernvorgang anzustossen): 255 stößt eine neue Schlüsselsuche über die Ringspule an. 254 verhindert nur das Einschlafen des CAS für die nächsten 10 Sekunden. |
| KEY_ID | string | ID des Schlüssels |
| KEY_TYPE | unsigned char | 0: Umlauf-Schlüssel 2: Geldbörsen-Schlüssel 3: Drivers-Key 4: Funk-Schlüssel 5: ID-Geber |
| INIT_MODE | unsigned char | Modus festlegen (optional). 1: Normal anlernen und Schlüssel verriegeln(default), 0: Schlüssel wird nicht verriegelt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-schluesseldaten"></a>
### STEUERN_SCHLUESSELDATEN

Schlüssel-Daten in CAS schreiben (z.B. für Ersatz-Steuergerät oder Nacharbeit). Nur zulässig solange EWS4_TRSP_SK nicht verriegelt. JobHeaderFormat STEUERN_SCHLUESSELDATEN Diagnose-Service:	UDS $2E DID $4210

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TAB_INDEX | unsigned char | Schlüssel-Position in der Transponder-Tabelle 0 - 9, 100 THS1, 101 THS2, 200 RSE-Fernbedienung. |
| KEY_ID | string | ID des Schlüssels (Gleichzeitig wird KEY_INIT_DONE auf 1 gesetzt) 'FF FF FF FF' bei unbekannt. (Gleichzeitig wird KEY_INIT_DONE auf 0 gesetzt) Falls ID 'FF FF FF FF' und gleichzeitig KEY_TYPE nicht 15: ERROR_DATA |
| KEY_TYPE | unsigned char | 0: Umlauf-Schlüssel 2: Geldbörsen-Schlüssel 3: Drivers-Key 4: Funk-Schlüssel 5: ID-Geber 15: künftiger Ersatzschlüssel |
| KEY_DISABLED | unsigned char | 0: Schlüssel nicht gesperrt 1: Schlüssel gesperrt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-pia-nr"></a>
### STEUERN_PIA_NR

PIA-Nummer eines Schlüssels umdefinieren. JobHeaderFormat STEUERN_PIA_NR Diagnose-Service:	UDS $22 DID $DC5B

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TAB_INDEX | unsigned char | Schlüssel-Position in der Transponder-Tabelle 0 - 9 |
| PIA_NR | unsigned char | 15 Keine personalisierung zugewiesen oder Schlüssel unbekannt 0 - 3: Schlüssel-Personalisierung in der Schlüssel-Tabelle Anmerkung: Die PIA-Nummer wird beim Anlernen automatisch vergeben, kann aber über Diagnose geändert werden. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-service-schluesseldaten-update"></a>
### STEUERN_SERVICE_SCHLUESSELDATEN_UPDATE

Dieser Job ermöglicht es einem folgende Aktionen anzustossen: Ermitteln der aktuellen Daten aus dem Fahrzeug, Übertragen der Daten in alle aktuell erkannten Schlüssel (inkrementell oder komplett). JobHeaderFormat STEUERN_SERVICE_SCHLUESSELDATEN_UPDATE Diagnose-Service:	UDS $3101 DID $4005

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| UPDATE_MODUS | unsigned char | Legt den Update-Modus fest (welche Daten werden vom CAS aus dem Fahrzeug aktualisiert und wie werden sie übertragen). Folgende Modi sind möglich: 0-&gt;Vollständiges Update CAS-Speicher+Vollständiges Update Schlüssel, 1-&gt;Vollständiges Update CAS-Speicher+Inkrementelles Update Schlüssel, 2-&gt;Kein Update CAS-Speicher+Vollständiges Update Schlüssel, 3-&gt;Kein Update CAS-Speicher+Inkrementelles Update Schlüssel, 15-&gt;Vollständiges Update CAS-Speicher+Kein Update Schlüssel |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-service-schluesseldaten-lesen"></a>
### STATUS_SERVICE_SCHLUESSELDATEN_LESEN

Dieser Job erlaubt es die Service-Schlüsseldaten blockweise aus dem CAS auszulesen. JobHeaderFormat STATUS_SERVICE_SCHLUESSELDATEN Diagnose-Service:	UDS $3101 DID $1006

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BLOCK_NR | unsigned int | Nummer des zu lesenden Service-Schlüsseldaten-Blocks. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DATEN_BLOCK_WERT | string | 32 Byte Rohdaten des Service-Schlüsseldaten-Blocks. |
| STAT_DATEN_BLOCK_EINH | string | 32 Byte Rohdaten des Service-Schlüsseldaten-Blocks. |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-diagnose-mode"></a>
### _DIAGNOSE_MODE

UDS  : $10   DiagnosticSessionControl Mode einstellbar ueber das Argument

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SESSION | int | 0x01 = defaultSession 0x03 = extendedDiagnosticSession |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anfrage vom Tester |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ident-istufe"></a>
### _STATUS_IDENT_ISTUFE

Lesen Identifikation I-Stufe UDS  : $22   ReadDataByIdentifier $100B Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_IDENT_ISTUFE_WERT | binary | 24 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kilometerstand"></a>
### _STATUS_KILOMETERSTAND

Lesen aktueller Kilometerstand UDS  : $22   ReadDataByIdentifier $1700 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KILOMETERSTAND_WERT | binary | 3 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-abs-time"></a>
### _STATUS_ABS_TIME

Lesen aktuelle absolute Zeit UDS  : $22   ReadDataByIdentifier $1701 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ABS_TIME_WERT | binary | 4 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-darh-dtc"></a>
### _STATUS_DARH_DTC

Lesen Anzahl der abgelegten Fehler UDS  : $22   ReadDataByIdentifier $1704 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DARH_DTC_WERT | binary | 7 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sc-version"></a>
### _STATUS_SC_VERSION

Lesen Standard Core Version UDS  : $22   ReadDataByIdentifier $1720 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SC_VERSION_WERT | binary | 4 Byte Byte 1: Major Version Byte 2: Minor Version Byte 3: Patch version Byte 4: reserviert |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sc-package-id"></a>
### _STATUS_SC_PACKAGE_ID

Lesen Standard Core Package Id UDS  : $22   ReadDataByIdentifier $1726 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SC_PACK_ID_WERT | binary | 136 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mem-seg-table"></a>
### _STATUS_MEM_SEG_TABLE

Lesen Memory segmentation table UDS  : $22   ReadDataByIdentifier $2501 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_MEM_SEG_TABLE_WERT | binary | 13 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-prog-counter"></a>
### _STATUS_PROG_COUNTER

Lesen Programming counter Status UDS  : $22   ReadDataByIdentifier $2502 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PROG_CTR_WERT | binary | 4 Byte Byte 1: reserviert Byte 2: ECU Programming State Byte 3: Programming Counter HiByte Byte 4: Programming Counter LoByte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-prog-counter-max"></a>
### _STATUS_PROG_COUNTER_MAX

Lesen Maximalwert des Programming Counters UDS  : $22   ReadDataByIdentifier $2503 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PROG_CTR_MAX_WERT | binary | 2 Byte Byte 1: MaxValue HiByte des Programming Counters Byte 2: MaxValue LoByte des Programming Counters |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-flash-tim-para"></a>
### _STATUS_FLASH_TIM_PARA

Lesen Flash Timing Parameter UDS  : $22   ReadDataByIdentifier $2504 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FLASH_TIM_PARA_WERT | binary | 15 Byte Byte 0-1:  Erase Memory Time Byte 2-3:  Check Memory Time Byte 4-5:  Bootloader Install Time Byte 6-7:  Authentification Time Byte 8-9:  Reset Time Byte 10:   Neues Datenobjekt 1 Byte 11:   Neues Datenobjekt 2 Byte 12:   Neues Datenobjekt 3 Byte 13:   Neues Datenobjekt 4 Byte 14:   Neues Datenobjekt 5 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-max-block-length"></a>
### _STATUS_MAX_BLOCK_LENGTH

Lesen maximale Blocklaenge UDS  : $22   ReadDataByIdentifier $2505 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FLASH_BLOCK_LENGTH_WERT | binary | 3 Byte Byte 1:  Adress Format Id (0x20) Byte 2-3:  Flash Block Length |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrzeugauftrag-teil-1"></a>
### _STATUS_FAHRZEUGAUFTRAG_TEIL_1

aktuelle 160 Byte Fahrzeugauftrag Teil1 UDS  : $22   ReadDataByIdentifier $3F1C Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 160 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fahrzeugauftrag-teil-2"></a>
### _STATUS_FAHRZEUGAUFTRAG_TEIL_2

aktuelle 160 Byte Fahrzeugauftrag Teil2 UDS  : $22   ReadDataByIdentifier $3F1C Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 160 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cas-var-konfig"></a>
### _STATUS_CAS_VAR_KONFIG

aktueller Status "CAS, Varianten Konfiguration" UDS  : $22   ReadDataByIdentifier $4000 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 8 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-trsp-mech-code"></a>
### _STATUS_TRSP_MECH_CODE

aktueller Status "Transponder MechCode" UDS  : $22   ReadDataByIdentifier $4201 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 5 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-trsp-fahrzyklus"></a>
### _STATUS_TRSP_FAHRZYKLUS

aktueller Status "Transponder Programmierdaten" UDS  : $22   ReadDataByIdentifier $4205 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 4 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fbd-empfangsdaten"></a>
### _STATUS_FBD_EMPFANGSDATEN

aktuelle 18 Byte des FBD Empfangs UDS  : $22   ReadDataByIdentifier $4600 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FBD_EMPFANG_WERT | binary | 18 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-act-diag-session"></a>
### _STATUS_ACT_DIAG_SESSION

Lesen active diagnose session UDS  : $22   ReadDataByIdentifier $F186 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ACT_DIA_SESS_WERT | binary | 2 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-supplier-number"></a>
### _STATUS_SUPPLIER_NUMBER

Lesen ECU serial number UDS  : $22   ReadDataByIdentifier $F18A Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 3 Byte ECU Supplier Byte 0 ECU Supplier Byte 1 ECU Supplier Byte 2 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ecu-manufacturing-data"></a>
### _STATUS_ECU_MANUFACTURING_DATA

Lesen ECU serial number UDS  : $22   ReadDataByIdentifier $F18B Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 3 Byte ECU Herstelldatum Tag 1..31 ECU Herstelldatum Monat 1..12 ECU Herstelldatum Jahr Offset zum Jahr 2000 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ecu-serial-number"></a>
### _STATUS_ECU_SERIAL_NUMBER

Lesen ECU serial number UDS  : $22   ReadDataByIdentifier $F18C Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 9 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cas4-auslieferungsstand"></a>
### _STATUS_CAS4_AUSLIEFERUNGSSTAND

CAS4 Auslieferungsstand UDS  : $22   ReadDataByIdentifier $F300 Modus: Default Fuer CT Qualitaetssicherung benoetigt hierueber erfolgt die Identifikation des SW Stand der ECU

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 3 Byte Jahr KW Index Index wird verwendet fuer mehrere Auslieferungen innerhalb einer KW |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-compilation-date-time"></a>
### _STATUS_COMPILATION_DATE_TIME

aktuelle 21 Byte Ascii UDS  : $22   ReadDataByIdentifier $F317 Modus: Default Datum ist in ASCII hinterlegt, das Format ist von der Systemdatum und -zeit Variablen eines Windows PC abhaengig

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_COMP_TIMESTAMP | binary | 21 Byte Hinter "Datum" und "Zeit" wird jeweils ein 0x00 gesetzt z. B.: May 05 2006[0x00]13:45:00[0x00] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-links-aussen-handle"></a>
### _STATUS_ANT_LINKS_AUSSEN_HANDLE

aktueller Status "Antenne Links aussen Handle" UDS  : $22   ReadDataByIdentifier $F320 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 33 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-rechts-aussen-handle"></a>
### _STATUS_ANT_RECHTS_AUSSEN_HANDLE

aktueller Status "Antenne Rechts aussen Handle" UDS  : $22   ReadDataByIdentifier $F321 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 33 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-kofferr-aussen-handle"></a>
### _STATUS_ANT_KOFFERR_AUSSEN_HANDLE

aktueller Status "Antenne Kofferraum aussen Handle" UDS  : $22   ReadDataByIdentifier $F322 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 33 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-vorne-innen-handle"></a>
### _STATUS_ANT_VORNE_INNEN_HANDLE

aktueller Status "Antenne vorne innen Handle" UDS  : $22   ReadDataByIdentifier $F323 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 33 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-mitte-innen-handle"></a>
### _STATUS_ANT_MITTE_INNEN_HANDLE

aktueller Status "Antenne vorne innen Handle" UDS  : $22   ReadDataByIdentifier $F324 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 33 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-hutablage-handle"></a>
### _STATUS_ANT_HUTABLAGE_HANDLE

aktueller Status "Antenne Hutablage Handle" UDS  : $22   ReadDataByIdentifier $F325 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 33 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-kofferr-innen-links-handle"></a>
### _STATUS_ANT_KOFFERR_INNEN_LINKS_HANDLE

aktueller Status "Antenne Kofferraum innen links Handle" UDS  : $22   ReadDataByIdentifier $F326 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 33 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-kofferr-innen-rechts-handle"></a>
### _STATUS_ANT_KOFFERR_INNEN_RECHTS_HANDLE

aktueller Status "Antenne Kofferraum innen rechts Handle" UDS  : $22   ReadDataByIdentifier $F327 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 33 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-comfort-go-ant-konfig"></a>
### _STATUS_COMFORT_GO_ANT_KONFIG

aktueller Status "Comfort Go Antennen Konfiguration" UDS  : $22   ReadDataByIdentifier $F330 Modus: Default 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 3 Byte Byte 0: Comfort Go Configbyte Auswahl der Antennen (bitcodiert, Antenne 0 = Bit0), die verwendet werden sollen Byte 1: Communication Retries Maximale Anzahl der Kommunikationsversuche Byte 2: Reserved |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tage-id"></a>
### _STATUS_TAGE_ID

aktueller Status "Status TAGE Identifier" UDS  : $22   ReadDataByIdentifier $F331 Modus: Default BMW Teilenummer (6Byte String) fuer jede Tuer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 24 Byte Byte  0 -  5 TAGE ID Fahrertuer Byte  6 - 11 TAGE ID Beifahrertuer Byte 12 - 17 TAGE ID Fahrertuer hinten Byte 18 - 23 TAGE ID Beifahrertuer hinten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-antennen"></a>
### _STATUS_ANTENNEN

aktueller Status "Status Antennen" UDS  : $22   ReadDataByIdentifier $F340 Modus: Default Liefert die Stati der bis zu 8 Antennen und einen globalen Status

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 18 Byte Byte  0 -  1:	Status Antenne 0 Byte  2 -  3:	Status Antenne 1 Byte  4 -  5:	Status Antenne 2 Byte  6 -  7:	Status Antenne 3 Byte  8 -  9:	Status Antenne 4 Byte 10 - 11:	Status Antenne 5 Byte 12 - 13:	Status Antenne 6 Byte 14 - 15:	Status Antenne 7 Byte 16 - 17: Status global Status 0x0000 -&gt; No Error 0x0001 -&gt; Antenna Short to Battey 0x0002 -&gt; Antenna Short to Ground 0x0004 -&gt; Antenna Open Load 0x0008 -&gt; reserved 0x0010 -&gt; F0 Out of Range 0x0020 -&gt; Q Out of Range 0x0040 -&gt; Supply Voltage LF Driver Low 0x0080 -&gt; Supply Voltage LF Driver High 0x0100 -&gt; ISR Overrun Flag 0x0200 -&gt; reserved 0x0400 -&gt; Selected Current Out of Range 0x0800 -&gt; reserved 0x1000 -&gt; reserved 0x2000 -&gt; reserved 0x4000 -&gt; reserved 0x8000 -&gt; reserved |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tage"></a>
### _STATUS_TAGE

aktueller Status "Status Tueraussengriffelektronik" UDS  : $22   ReadDataByIdentifier $F341 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 4 Byte Byte 0		Status TAGE Fahrertuer Byte 1		Status TAGE Beifahrertuer Byte 2		Status TAGE Fahrertuer hinten Byte 3		Status TAGE Beifahrertuer hinten Status TAGE fuer jede Tuer: 0 Kein Status (keine Betätigung) 1 Zugsensor Betätigt 2 Sichern Sensor Betätigt 3 Entriegeln Sensor Betätigt (Status wird 5 s gehalten oder bis anderer Befehl kommt) |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ca-telegramm"></a>
### _STATUS_CA_TELEGRAMM

aktueller Status "Status CA Telegramm" UDS  : $22   ReadDataByIdentifier $F342 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 14 Byte Byte 0 Schluesselnummer 0...9 Schlüssel-Index in Schlüssel-Tabelle "15" = ungültiger / unbekannter Schlüssel  Byte 1..4 Schluessel ID  Byte 5 Personalisierungsnummer 0...3 Pers-Nr "15" = ungültiger / unbekannter Schlüssel  Byte 6 FBD Feldstaerke Empfangsstärke Signal Schlüssel an FBD-Empfänger 0...255 Empfangsstärke  Byte 7 FBD Feldstaerke Schluessel Empfangsstärke Signal FBD-Empfänger an Schlüssel 0...255 Empfangsstärke  Byte 8 LF Feldstaerke Schluessel Empfangsstärke LF-Signal 125 kHz Fahrzeug an Schlüssel 0...255 Empfangsstärke  Byte 9 CA Aktion Aktion bzw. Ursache 1 Entriegeln 2 Verriegeln 3 Kofferraum öffnen 4 Motor starten / Innenraum-Suche Byte 10 Suchort Empfangsort / Suchort 1 IRV (Innenraum vorn) 2 IRH (Innenraum hinten) 3 FT (Fahrertür/-seite) 4 BFT (Beifahrertür/-seite) 5 HA (Hut-Ablage) 6 KRLI (Kofferraum links) 7 KRRE (Kofferraum rechts) 8 SF (Stoßfänger)  Byte 11 Gueltigkeit Gütigkeitsstatus 0 ungültig 1 gültig  Byte 12..13 Batterie-Spannung des sendenden Schluessels |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-stroeme"></a>
### _STATUS_ANT_STROEME

aktueller Status "Status Antennenstroeme" UDS  : $22   ReadDataByIdentifier $F343 Modus: Default Bei der zuletzt ausgefuehrten CA Aktion gemessener Antennenstrom fuer alle Antennen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 16 Byte Byte 0..1	Antennenstrom (mA) Antenne0 Byte 2..3	Antennenstrom (mA) Antenne1 Byte 4..5	Antennenstrom (mA) Antenne2 Byte 6..7	Antennenstrom (mA) Antenne3 Byte 8..9	Antennenstrom (mA) Antenne4 Byte 10..11	Antennenstrom (mA) Antenne5 Byte 12..13	Antennenstrom (mA) Antenne6 Byte 14..15	Antennenstrom (mA) Antenne7 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-schluessel-info"></a>
### _STATUS_SCHLUESSEL_INFO

aktueller Status "Status Schluesselinfo" UDS  : $22   ReadDataByIdentifier $F344 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 9 Byte |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ca-handler"></a>
### _STATUS_CA_HANDLER

aktueller Status "Status CA Handler" UDS  : $22   ReadDataByIdentifier $F345 Modus: Default Interner CAH-Statusspeicher, nur zu Entwicklungszwecken

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 12 Byte Byte 0..3	Number of Keysearch Calls Byte 4..7 Authentication Time Byte 8..9 Max Tasktime Byte 10   CA Handler Statusbyte 1 Byte 11   CA Handler Statusbyte 2 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-res-freq"></a>
### _STATUS_RES_FREQ

aktueller Status "Status Resonanz Frequenz" UDS  : $22   ReadDataByIdentifier $F346 Modus: Default Lesen der geschaetzten Resonanzfrequenzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 8 Byte Byte 0	aussen links Byte 1	aussen rechts Byte 2	aussen Kofferraum Byte 3	innen vorne Byte 4	innen mitte Byte 5	innen hinten Byte 6	innen Kofferraum links Byte 7	innen Kofferraum rechts |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ant-guete"></a>
### _STATUS_ANT_GUETE

aktueller Status "Status Guete Antenne" UDS  : $22   ReadDataByIdentifier $F347 Modus: Default Lesen der geschaetzten Gueten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 8 Byte Byte 0	aussen links Byte 1	aussen rechts Byte 2	aussen Kofferraum Byte 3	innen vorne Byte 4	innen mitte Byte 5	innen hinten Byte 6	innen Kofferraum links Byte 7	innen Kofferraum rechts |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lf-treiber"></a>
### _STATUS_LF_TREIBER

aktueller Status "Status LF Treiber" UDS  : $22   ReadDataByIdentifier $F348 Modus: Default Verhalten des LF-Treibers und des CAH

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 4 Byte Byte 0    Anzahl der max. Kommunikationsversuche Byte 1..2 LF-Sendestrom fuer Diagnosefunktionen Byte 3    CA Handler Statusflags Byte 2 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-u-kl15n30b"></a>
### _STATUS_U_KL15N30B

aktueller Status analoge Spannungswerte Funktionsgruppe 15N30B UDS  : $22   ReadDataByIdentifier $F3A0 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | Byte 0-1 AI_15N Byte 2-3 AI_30B_1 Byte 4-5 AI_30B_2 Byte 6-7 AI_15WUP |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-u-kl15-kl50"></a>
### _STATUS_U_KL15_KL50

aktueller Status analoge Spannungswerte Funktionsgruppe KL15 UDS  : $22   ReadDataByIdentifier $F3A1 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | Byte 0-1 AI_15_1 Byte 2-3 AI_15_2 Byte 4-5 AI_15_3 Byte 6-7 AI_15_50 Byte 8-9 AI_50L Byte 10-11 AI_50L_RS |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-u-powersupply"></a>
### _STATUS_U_POWERSUPPLY

aktueller Status analoge Spannungswerte Funktionsgruppe Powersupply UDS  : $22   ReadDataByIdentifier $F3A2 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | Byte 0-1 AI_30E Byte 2-3 AI_30L Byte 4-5 AI_TEMP Byte 6-7 AI_LF_DIAG Byte 8-9 AI_LF_STROM |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-u-elv"></a>
### _STATUS_U_ELV

aktueller Status analoge Spannungswerte ELV Funktionsgruppe Powersupply UDS  : $22   ReadDataByIdentifier $F3A3 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | Byte 0-1 AI_30 ELV Byte 2-3 AI_31 ELV |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-u-hall-tage"></a>
### _STATUS_U_HALL_TAGE

aktueller Status analoge Spannungswerte Hallsensoren und Tueraussengriffe Funktionsgruppe Powersupply UDS  : $22   ReadDataByIdentifier $F3A4 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | Byte 0 AI_TAGE_ER_BFT Byte 1 AI_TAGE_ER_BFTH Byte 2 AI_TAGE_ER_FT Byte 3 AI_TAGE_ER_FTH Byte 4-5 AI_VCC_HALL13 Byte 6-7 AI_VCC_HALL24 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dig-input-start-stop"></a>
### _STATUS_DIG_INPUT_START_STOP

aktueller Status digitale Eingaenge Funktionsgruppen 15N30B und 15WUP UDS  : $22   ReadDataByIdentifier $F3A5 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 3 Byte Byte 0: Bit0 DI_A_S_START Bit1 DI_BLS_MSA Bit2 Reserve Bit3 Reserve Bit4 DI_A_S_START Co Bit1 DI_BLS_MSA Co Bit2 Reserve Bit3 Reserve Byte 1: Bit0..Bit3 DI_DFASIM Bit4..Bit7 Reserve Byte 2: Bit0..Bit3 DI_DFASIM Co Bit4..Bit7 Reserve |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dig-input-hall"></a>
### _STATUS_DIG_INPUT_HALL

aktueller Status digitale Eingaenge Funktionsgruppen HALL UDS  : $22   ReadDataByIdentifier $F3A6 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 1 Byte Bit0 DI_HALL1_SSTA Bit1 DI_HALL2_SSTB |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dig-input-schalter"></a>
### _STATUS_DIG_INPUT_SCHALTER

aktueller Status digitale Eingaenge Funktionsgruppen Schalter UDS  : $22   ReadDataByIdentifier $F3A8 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 1 Byte Bit0 DI_WU_CLT Bit1 DI_WU_HOTEL Bit2 DI_WU_MHK Bit3 DI_WU_MOST_WUP Bit4 DI_WU_MSA Bit5 DI_WU_TOEHKI Bit6 Reserve Bit7 Reserve |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dig-input-bremse-kuppl"></a>
### _STATUS_DIG_INPUT_BREMSE_KUPPL

aktueller Status digitale Eingaenge Funktionsgruppen Bremse und Kupplung UDS  : $22   ReadDataByIdentifier $F3A9 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 1 Byte Bit0 DI_BLTS Bit1 DI_PN_KUPPL Bit2 Reserve Bit3 Reserve Bit4 DI_BLTS_Co Bit5 DI_PN_KUPPL_Co Bit6 Reserve Bit7 Reserve |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dig-input-klemmen"></a>
### _STATUS_DIG_INPUT_KLEMMEN

aktueller Status digitale Eingaenge Funktionsgruppen 15N30B und 15WUP UDS  : $22   ReadDataByIdentifier $F3AB Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DATA | binary | 1 Byte Bit0 DI_15N_30B_1_STAT Bit1 DI_30B_2_STAT Bit2 DI_WU_15WUP_RS |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sa-request-seed"></a>
### _SA_REQUEST_SEED

Anfordern des SEED Codes von der ECU Es muessen immer alle 5 Argumente im angegebenen Wertebereich uebergeben werden. UDS  : $27   SecurityAccess SID $01   Sub Identifier "Request Seed" User-ID Byte[0] User-ID Byte[1] User-ID Byte[2] User-ID Byte[3] Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SUB_ID_RS | int | Bereich: 1-1 bzw. 0x01-0x01 |
| USER_ID0 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| USER_ID1 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| USER_ID2 | int | Bereich: 0-255 bzw. 0x00-0xFF |
| USER_ID3 | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sa-send-key"></a>
### _SA_SEND_KEY

Senden des Key Wertes an die ECU Es muessen immer alle Argumente im jeweils gueltigen Wertebereich uebergeben werden. UDS  : $27   SecurityAccess SID $02   Sub Identifier "Request Seed" $03   FixCode[68 Byte Array] Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KEYVALUE | binary | Sub-ID "Send Key" und aus Seedwert berechneter Key 1Byte (Default 0x02) + 68 Bytes, Defaultwert 0x03 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ident-istufe"></a>
### _STEUERN_IDENT_ISTUFE

Beschreiben der I-Stufe Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $100B Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,22, .. ,AA" ======&gt; Byte 0 - 23 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fahrzeugauftrag-teil-1"></a>
### _STEUERN_FAHRZEUGAUFTRAG_TEIL_1

Beschreiben der Fahrzeugauftrag Teil1 Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $3F1C Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,2A,..,33,44" ======&gt; Byte 0 - 159 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-fahrzeugauftrag-teil-2"></a>
### _STEUERN_FAHRZEUGAUFTRAG_TEIL_2

Beschreiben der Fahrzeugauftrag Teil2 Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $3F1D Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,2A,..,33,44" ======&gt; Byte 0 - 159 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-cas-var-konfig"></a>
### _STEUERN_CAS_VAR_KONFIG

Beschreiben der CAS Varianten Konfiguration Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $4000 CAS_VAR_KONFIG Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11, .. ,AA" ======&gt; Byte 0 - 7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-trsp-mech-code"></a>
### _STEUERN_TRSP_MECH_CODE

Beschreiben des Transponder MechCode Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $4201 Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "00,11,..,AA" ======&gt; Byte 0 - 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-trsp-fahrzyklus"></a>
### _STEUERN_TRSP_FAHRZYKLUS

Beschreiben des Transponder Fahrzykluszaehler Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $4205 Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZYKLUS | string | "FAHRZYKLUS": z.B. "00,00,11,00" ======&gt; Byte 0 - 3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ews4-seckey"></a>
### _STEUERN_EWS4_SECKEY

Schreiben des EWS4 Secret Key 17 Byte Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $C001 Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,22, .. ,AA" ======&gt; Byte 0 - 16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-svk-supplier"></a>
### _STEUERN_SVK_SUPPLIER

Schreiben der BMW Logistik Daten Zulieferer Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F102 Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,2A, .. ,AA"  Achtung, variable Datenlaenge ! Im Byte 3 wird die Anzahl der vorhandenen HW und SW Einheiten festgelegt Die danach eingegebenen Daten muessen exakt dieser Angabe entsprechen Byte 0 SVK Version Byte 1 Programming Dependencies Status Byte 2 Number of SVK Entries MSB Byte 3 Number of SVK Entries LSB  Byte  4-16 13 Byte Fingerprint Byte 17-24  8 Byte Daten HWE 0 Byte 25-32  8 Byte Daten SWE 0 Byte 33-40  8 Byte Daten SWE 1 (falls vorhanden) Byte 41-48  8 Byte Daten SWE 2 (falls vorhanden) Byte 49-56  8 Byte Daten SWE 3 (falls vorhanden) Byte 57-64  8 Byte Daten SWE 4 (falls vorhanden) Byte 65-72  8 Byte Daten SWE 5 (falls vorhanden) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-svk-werk"></a>
### _STEUERN_SVK_WERK

Schreiben der BMW Logistik Daten Werk Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F103 Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,2A, .. ,AA"  Achtung, variable Datenlaenge ! Im Byte 3 wird die Anzahl der vorhandenen HW und SW Einheiten festgelegt Die danach eingegebenen Daten muessen exakt dieser Angabe entsprechen Byte 0 SVK Version Byte 1 Programming Dependencies Status Byte 2 Number of SVK Entries MSB Byte 3 Number of SVK Entries LSB  Byte  4-16 13 Byte Fingerprint Byte 17-24  8 Byte Daten HWE 0 Byte 25-32  8 Byte Daten SWE 0 Byte 33-40  8 Byte Daten SWE 1 (falls vorhanden) Byte 41-48  8 Byte Daten SWE 2 (falls vorhanden) Byte 49-56  8 Byte Daten SWE 3 (falls vorhanden) Byte 57-64  8 Byte Daten SWE 4 (falls vorhanden) Byte 65-72  8 Byte Daten SWE 5 (falls vorhanden) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ant-links-aussen-handle"></a>
### _STEUERN_ANT_LINKS_AUSSEN_HANDLE

Beschreiben des Antenne links Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F320 Data Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,22, .. ,AA" ======&gt; Byte 0 - 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ant-rechts-aussen-handle"></a>
### _STEUERN_ANT_RECHTS_AUSSEN_HANDLE

Beschreiben des Antenne rechts aussen Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F321 Data Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,22, .. ,AA" ======&gt; Byte 0 - 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ant-kofferr-aussen-handle"></a>
### _STEUERN_ANT_KOFFERR_AUSSEN_HANDLE

Beschreiben des Antenne Kofferraum aussen Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F322 Data Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,22, .. ,AA" ======&gt; Byte 0 - 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ant-vorne-innen-handle"></a>
### _STEUERN_ANT_VORNE_INNEN_HANDLE

Beschreiben des Antenne vorne innen Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F323 Data Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,22, .. ,AA" ======&gt; Byte 0 - 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ant-mitte-innen-handle"></a>
### _STEUERN_ANT_MITTE_INNEN_HANDLE

Beschreiben des Antenne mitte innen Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F324 Data Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,22, .. ,AA" ======&gt; Byte 0 - 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ant-hutablage-handle"></a>
### _STEUERN_ANT_HUTABLAGE_HANDLE

Beschreiben des Antenne Hutablage Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F325 Data Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,22, .. ,AA" ======&gt; Byte 0 - 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ant-kofferr-innen-links-handle"></a>
### _STEUERN_ANT_KOFFERR_INNEN_LINKS_HANDLE

Beschreiben des Antenne Kofferraum innen links Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F326 Data Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,22, .. ,AA" ======&gt; Byte 0 - 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ant-kofferr-innen-rechts-handle"></a>
### _STEUERN_ANT_KOFFERR_INNEN_RECHTS_HANDLE

Beschreiben des Antenne Kofferraum innen rechts Handle Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F327 Data Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,22, .. ,AA" ======&gt; Byte 0 - 32 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-comfort-go-ant-konfig"></a>
### _STEUERN_COMFORT_GO_ANT_KONFIG

Beschreiben der Comfort go Antennen Konfig Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F330 Data Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,22,33" ======&gt; Byte 0 - 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tage-id"></a>
### _STEUERN_TAGE_ID

Beschreiben der Tueraussengriffelektronik Id Eingabe der Daten als Hexwert von 00..FF UDS  : $2E   WriteDataByIdentifier $F331 Data Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | string | "Daten": z.B. "11,22..FF" ======&gt; Byte 0 - 23 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-treiberstufe-kl15-30"></a>
### _STEUERN_TREIBERSTUFE_KL15_30

Ansteuerung der Klemme 15/30 Ausgangspins UDS  : $2F     I/O Control By Local Id $0201   Data Id

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_OPTION | int | 0 return Control to ECU 1 Reset 3 Set |
| DATEN | string | "Control States": z.B. "11,22" ======&gt; Byte 0 - 1 ACHTUNG nur bei Control Option 3 (Set) eingeben! Byte0 Pinmaske (siehe Diagnosebeschreibung) Byte1 Zustandsmaske (siehe Diagnosebeschreibung) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anfrage vom Tester |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-treiberstufe-kl15-50"></a>
### _STEUERN_TREIBERSTUFE_KL15_50

Ansteuerung der Klemme 15/50 Ausgangspins UDS  : $2F     I/O Control By Local Id $0202   Data Id

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_OPTION | int | 0 return Control to ECU 1 Reset 3 Set |
| DATEN | string | "Control States": z.B. "11,22" ======&gt; Byte 0 - 1 ACHTUNG nur bei Control Option 3 (Set) eingeben! Byte0 Pinmaske (siehe Diagnosebeschreibung) Byte1 Zustandsmaske (siehe Diagnosebeschreibung) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anfrage vom Tester |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-bimag"></a>
### _STEUERN_BIMAG

Ansteuerung der BiMAG UDS  : $2F     I/O Control By Local Id $0203   Data Id

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_OPTION | int | 0 return Control to ECU 1 Reset 3 Set |
| DATEN | string | "Control States": z.B. "11,22" ======&gt; Byte 0 - 1 ACHTUNG nur bei Control Option 3 (Set) eingeben! Byte0 Pinmaske (siehe Diagnosebeschreibung) Byte1 Zustandsmaske (siehe Diagnosebeschreibung) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anfrage vom Tester |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-elv"></a>
### _STEUERN_ELV

Ansteuerung ELV UDS  : $2F     I/O Control By Local Id $0204   Data Id

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_OPTION | int | 0 return Control to ECU 1 Reset 3 Set |
| DATEN | string | "Control States": z.B. "11,22" ======&gt; Byte 0 - 1 ACHTUNG nur bei Control Option 3 (Set) eingeben! Byte0 Pinmaske (siehe Diagnosebeschreibung) Byte1 Zustandsmaske (siehe Diagnosebeschreibung) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anfrage vom Tester |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hall"></a>
### _STEUERN_HALL

Ansteuerung HALL Sensoren UDS  : $2F     I/O Control By Local Id $0205   Data Id

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_OPTION | int | 0 return Control to ECU 1 Reset 3 Set |
| DATEN | string | "Control States": z.B. "11,22" ======&gt; Byte 0 - 1 ACHTUNG nur bei Control Option 3 (Set) eingeben! Byte0 Pinmaske (siehe Diagnosebeschreibung) Byte1 Zustandsmaske (siehe Diagnosebeschreibung) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anfrage vom Tester |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-led-lf"></a>
### _STEUERN_LED_LF

Ansteuerung LED und LF UDS  : $2F     I/O Control By Local Id $0206   Data Id

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTROL_OPTION | int | 0 return Control to ECU 1 Reset 3 Set |
| DATEN | string | "Control States": z.B. "11,22" ======&gt; Byte 0 - 1 ACHTUNG nur bei Control Option 3 (Set) eingeben! Byte0 Pinmaske (siehe Diagnosebeschreibung) Byte1 Zustandsmaske (siehe Diagnosebeschreibung) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anfrage vom Tester |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ant-status-reset"></a>
### _STEUERN_ANT_STATUS_RESET

Antennenstatus ruecksetzen UDS  : $31       Routine Control $xxF801   Routine Id $F801 Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERVICE_REQ | int | 1 Start routine 2 Stop routine 3 Request routine results |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anfrage vom Tester |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-schluessel-suche"></a>
### _STEUERN_SCHLUESSEL_SUCHE

Schluesselsuche, CA Handler versendet LF Telegramm UDS  : $31       Routine Control $xxF802   Routine Id $F802 Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERVICE_REQ | int | 1 Start routine 2 Stop routine 3 Request routine results |
| ID_GEBER_NR | int | 0-7, die zu bevorzugende Schluesselnummer |
| GESPERRTE_SCHL_BYTE0 | int | Keine Schluesselsuche fuer ..., bitcodiert Bit0: Schluessel 8, Bit1: Schluessel 9 ... |
| GESPERRTE_SCHL_BYTE1 | int | Keine Schluesselsuche fuer ..., bitcodiert Bit0: Schluessel 0, Bit1: Schluessel 1 ... |
| SUCH_MODUS | int | 0-19, Suchmodus lt. Diagnosebeschreibung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anfrage vom Tester |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lf-hw-test"></a>
### _STEUERN_LF_HW_TEST

LF Hardware Selbsttest UDS  : $31       Routine Control $xxF803   Routine Id $F803 Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERVICE_REQ | int | 1 Start routine |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anfrage vom Tester |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lf-test-telegramm"></a>
### _STEUERN_LF_TEST_TELEGRAMM

Versendet LF Telegramm mit der im Parameter angegebenen Anzahl Bytes UDS  : $31       Routine Control $xxF804   Routine Id $F804 Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERVICE_REQ | int | 1 Start routine |
| ANZ_BYTES | int | Testdatenanzahl |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anfrage vom Tester |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-reset-det"></a>
### _STEUERN_RESET_DET

Ruecksetzen der Eintraege im Debugmodul "Development Error Tracer (DET)" UDS  : $31       Routine Control $xxF806   Routine Id $F806 Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anfrage vom Tester |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-development-job"></a>
### _DEVELOPMENT_JOB

Frei programmierbare Diagnosebotschaft, die ohne Vorfilterung auf dem CAN gesendet wird. Wird benoetigt fuer Diagnose Tests. Auch &gt; 64 Byte Daten Adressierung unterstuetzt. Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DEVJOB_DATALEN | int | Anzahl der Nutzdaten |
| DEVJOB_DATA | binary | Frei programmierbarer Datenarray Alle fuer den Service benoetigten Bytes muessen programmiert werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anfrage vom Tester |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (64 × 2)
- [LIEFERANTEN](#table-lieferanten) (97 × 2)
- [FARTTEXTE](#table-farttexte) (18 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (20 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (4 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (9 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (45 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [LIEFERANTENLIN](#table-lieferantenlin) (73 × 2)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FORTTEXTE](#table-forttexte) (56 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (5 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (1 × 9)
- [IORTTEXTE](#table-iorttexte) (8 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (3 × 2)
- [SG_FUNKTIONEN](#table-sg-funktionen) (33 × 16)
- [TAB_STEUERN_EWS4_MODE](#table-tab-steuern-ews4-mode) (8 × 4)
- [RES_0XDAB6](#table-res-0xdab6) (1 × 13)
- [TAB_WECKQUELLE](#table-tab-weckquelle) (30 × 2)
- [RES_0XDC54](#table-res-0xdc54) (1 × 10)
- [ARG_0XDC54](#table-arg-0xdc54) (7 × 12)
- [RES_0XDAC1](#table-res-0xdac1) (6 × 10)
- [TAB_CAS_ZV_STATUS](#table-tab-cas-zv-status) (7 × 2)
- [RES_0XDAB9](#table-res-0xdab9) (1 × 10)
- [ARG_0XDAB9](#table-arg-0xdab9) (1 × 12)
- [TAB_CAS_MONTAGEMODUS](#table-tab-cas-montagemodus) (4 × 2)
- [RES_0XDC68](#table-res-0xdc68) (2 × 10)
- [ARG_0XDC68](#table-arg-0xdc68) (1 × 12)
- [RES_0XDC63](#table-res-0xdc63) (2 × 10)
- [ARG_0XDC63](#table-arg-0xdc63) (1 × 12)
- [RES_0XDC65](#table-res-0xdc65) (2 × 10)
- [ARG_0XDC65](#table-arg-0xdc65) (1 × 12)
- [RES_0XDC62](#table-res-0xdc62) (2 × 10)
- [ARG_0XDC62](#table-arg-0xdc62) (1 × 12)
- [RES_0XDABC](#table-res-0xdabc) (6 × 10)
- [TAB_CAS_GANG](#table-tab-cas-gang) (12 × 2)
- [TAB_CAS_MOTOR_STATUS](#table-tab-cas-motor-status) (4 × 2)
- [TAB_CAS_MOTORSTART_FREIGABE](#table-tab-cas-motorstart-freigabe) (4 × 2)
- [TAB_CAS_MOTOR_ANLASSERSPERRE](#table-tab-cas-motor-anlassersperre) (4 × 2)
- [ARG_0XAC51](#table-arg-0xac51) (1 × 12)
- [RES_0XDAB5](#table-res-0xdab5) (4 × 10)
- [RES_0XDC67](#table-res-0xdc67) (2 × 10)
- [ARG_0XDC67](#table-arg-0xdc67) (1 × 12)
- [RES_0XDABB](#table-res-0xdabb) (7 × 10)
- [TAB_CAS_KLEMMENSTATUS](#table-tab-cas-klemmenstatus) (16 × 2)
- [RES_0XDC64](#table-res-0xdc64) (2 × 10)
- [ARG_0XDC64](#table-arg-0xdc64) (1 × 12)
- [TAB_CAS_PIA_NUMMER](#table-tab-cas-pia-nummer) (5 × 2)
- [RES_0XDC60](#table-res-0xdc60) (4 × 10)
- [ARG_0XDC60](#table-arg-0xdc60) (2 × 12)
- [RES_0XDABF](#table-res-0xdabf) (4 × 10)
- [TAB_CAS_FH_STATUS](#table-tab-cas-fh-status) (4 × 2)
- [RES_0XDABD](#table-res-0xdabd) (3 × 10)
- [TAB_CAS_GESCHW_STATUS](#table-tab-cas-geschw-status) (6 × 2)
- [RES_0XDACA](#table-res-0xdaca) (4 × 10)
- [RES_0XDAB0](#table-res-0xdab0) (2 × 10)
- [RES_0XDC69](#table-res-0xdc69) (2 × 10)
- [ARG_0XDC69](#table-arg-0xdc69) (1 × 12)
- [RES_0XDC61](#table-res-0xdc61) (4 × 10)
- [ARG_0XDC61](#table-arg-0xdc61) (2 × 12)
- [RES_0XAC57](#table-res-0xac57) (1 × 13)
- [ARG_0XAC57](#table-arg-0xac57) (1 × 12)
- [TAB_ZV_AKTION](#table-tab-zv-aktion) (8 × 2)
- [TAB_ZV_ZUSTAND](#table-tab-zv-zustand) (9 × 2)
- [RES_0XDAB3](#table-res-0xdab3) (16 × 10)
- [RES_0XDC66](#table-res-0xdc66) (2 × 10)
- [ARG_0XDC66](#table-arg-0xdc66) (1 × 12)
- [RES_0XDC6A](#table-res-0xdc6a) (2 × 10)
- [ARG_0XDC6A](#table-arg-0xdc6a) (1 × 12)
- [TAB_CAS_DIGITAL_EINGANG](#table-tab-cas-digital-eingang) (4 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 64 rows × 2 columns

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

Dimensions: 97 rows × 2 columns

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
| 0xFFFFFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 18 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler gespeichert |
| 0x44 | Fehler momentan vorhanden und bereits gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler momentan vorhanden und bereits gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler momentan vorhanden und bereits gespeichert |
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

Dimensions: 20 rows × 3 columns

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
| 0xA0 | ENTD | Entertainment Daten |
| 0xA1 | NAVD | Navigation Daten |
| 0xA2 | FCFN | Freischaltcode Funktion |
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

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x1700 | KM_STAND | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1701 | ABS_ZEIT | 0-n | - | 0xFFFFFFFF | - | 1 | 1 | 0.000000 |
| 0x1702 | SAE_CODE | 0-n | - | 0xFFFFFF | - | 1 | 1 | 0.000000 |
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

Dimensions: 9 rows × 3 columns

| NR | MODE | MODE_TEXT |
| --- | --- | --- |
| 0x00 | UNGUELTIG | DefaultMode |
| 0x01 | DEFAULT | DefaultMode |
| 0x02 | ECUPM | ECUProgrammingMode |
| 0x03 | ECUEXTDIAG | ECUExtendedDiagnosticSession |
| 0x40 | ECUEOL | ECUEndOfLineSession |
| 0x41 | ECUCODE | ECUCodingSession |
| 0x42 | ECUSWT | ECUSwtSession |
| 0x4F | ECUDEVELOP | ECUDevelopmentSession |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 45 rows × 3 columns

| ORT | ORTTEXT | LIN_2_FORMAT |
| --- | --- | --- |
| 0x0100 | Batteriesensor | - |
| 0x0200 | Elektrische Wasserpumpe | - |
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
| 0x0F00 | Rearview Kamera hinten | - |
| 0x1000 | Topview Kamera Außenspiegel links | - |
| 0x1100 | Topview Kamera Außenspiegel rechts | - |
| 0x1200 | Sideview Kamera Stoßfänger vorne links | - |
| 0x1300 | Sideview Kamera Stoßfänger vorne rechts | - |
| 0x1400 | Wischermotor | 1 |
| 0x1500 | Regen- Lichtsensor | 1 |
| 0x1600 | Innenspiegel | 1 |
| 0x1700 | Garagentoröffner | 1 |
| 0x1800 | AUC-Sensor | 1 |
| 0x1900 | Druck- Temperatursensor | 1 |
| 0x1A00 | Schalterblock Sitzheizung hinten | 1 |
| 0x1B00 | Schalterblock Sitzmemory/-massage Fahrer | 1 |
| 0x1C00 | Schalterblock Sitzmemory/-massage Beifahrer | 1 |
| 0x1D00 | Sonnenrollo Seitenfenster Fahrer | 1 |
| 0x1E00 | Sonnenrollo Seitenfenster Beifahrer | 1 |
| 0x1F00 | KAFAS Kamera | 1 |
| 0x2000 | Automatische Anhängevorrichtung | 1 |
| 0x2100 | SINE | 1 |
| 0x2200 | Funkempfänger | 1 |
| 0x2300 | Funkempfänger 2 | 1 |
| 0x2400 | Türgriffelektronik Fahrer | - |
| 0x2500 | Türgriffelektronik Beifahrer | - |
| 0x2600 | Türgriffelektronik Fahrer hinten | - |
| 0x2700 | Türgriffelektronik Beifahrer hinten | - |
| 0x2800 | Telestart-Handsender 1 | - |
| 0x2900 | Telestart-Handsender 2 | - |
| 0x2A00 | RSE-Fernbedienung | - |
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-lieferantenlin"></a>
### LIEFERANTENLIN

Dimensions: 73 rows × 2 columns

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
| 0xFFFF | unbekannter Hersteller |

<a id="table-iarttexte"></a>
### IARTTEXTE

Dimensions: 18 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler gespeichert |
| 0x44 | Fehler momentan vorhanden und bereits gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler momentan vorhanden und bereits gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler momentan vorhanden und bereits gespeichert |
| 0x4D | Fehler gespeichert |
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

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 2 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | kein Betriebsmode gesetzt | kein Betriebsmode |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 56 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x002711 | Coding Event: not coded | 0 |
| 0x002712 | Coding Event: transaction failed | 0 |
| 0x002713 | Coding Event: signature error | 0 |
| 0x002714 | Coding Event: wrong vehicle | 0 |
| 0x002715 | Coding Event: invalid data | 0 |
| 0x024000 | Energiesparmode aktiv | 0 |
| 0x02FF40 | DM test appl | 0 |
| 0x240000 | VSM Event Opmode | 0 |
| 0x400401 | DM queue full | 0 |
| 0x400402 | DM queue deleted | 0 |
| 0x4003A0 | Ausfall CAN-ID 3A0 | 0 |
| 0x401001 | DM Event Zeitbotschaft Timeout | 0 |
| 0x402847 | PIA E Io Error | 0 |
| 0xD9045F | Body-CAN Bus | 0 |
| 0xD90468 | Body-CAN Control Module Bus OFF | 0 |
| 0xD90BFF | DM_TEST_COM Standardcore Diagnosemodul Testfehlerspeichereintrag | 0 |
| 0x93080C | Unterspannung | 0 |
| 0x93080D | Überspannung KL30L/KL30E | 0 |
| 0x930820 | CAS4-Versorgung KL30L / KL30E: Unterspannung | 0 |
| 0x930821 | Bremssignale BLSH: Kurzschluss Masse | 0 |
| 0x930822 | P-Signal PN_KUPPL: Kurzschluss Masse | 0 |
| 0x930823 | Kupplungssignal PN_KUPPL | 0 |
| 0x930824 | Bedientaster MSA | 0 |
| 0x930825 | Komfortstartleitung A_S_START: Kurzschluss Masse | 0 |
| 0x930826 | Fehler Motorstart bei Anlasserbetrieb: Kurzschluss Masse | 0 |
| 0x930827 | Geschwindigkeitssignal DFA_EMF | 0 |
| 0x930828 | Hallsensor SSTA | 0 |
| 0x930829 | Hallsensor SSTB | 0 |
| 0x93082A | Treiber 15WUP | 0 |
| 0x93082B | KL15WUP_RS | 0 |
| 0x93082C | Treiber KL30B1: Kurzschluss Masse | 0 |
| 0x93082D | Treiber KL30B2 | 0 |
| 0x93082E | Treiber KL30B3 | 0 |
| 0x93082F | Treiber KL15-1: Kurzschluss Masse | 0 |
| 0x930830 | Treiber KL15-2 | 0 |
| 0x930831 | Treiber KL15-3 | 0 |
| 0x930832 | Treiber KL15N: Kurzschluss Masse | 0 |
| 0x930833 | Treiber KL50L | 0 |
| 0x930834 | Treiber KL5MSA / KL50L_RS | 0 |
| 0x930835 | Treiber LED_SST | 0 |
| 0x930836 | Treiber LED_MSA | 0 |
| 0x930837 | Treiber VCC_HALL1 | 0 |
| 0x930838 | Treiber VC_HALL2 | 0 |
| 0x930839 | Fehler Freigabe CoProzessor | 0 |
| 0x93083A | Ungleiche CRC-Summe CoProzessor | 0 |
| 0x930841 | Bremssignale BLSH: Kurzschluss Batteriespannung | 0 |
| 0x930842 | Bremssgnale BLSL: Kurzschluss Batteriespannung | 0 |
| 0x930843 | Bremssignale BLSL: Kurzschluss Masse | 0 |
| 0x930846 | P-Signal PN_KUPPL: Kurzschluss Batteriespannung | 0 |
| 0x93084A | Komfortstartleitung A_S_START: Kurzschluss Masse | 0 |
| 0x930851 | Fehler Motorstart bei Anlasserbetrieb: Relaiskleber | 0 |
| 0x930852 | Fehler Motorstart bei Anlasserbetrieb: Motor dreht nicht | 0 |
| 0x930856 | Treiber KL30B1: Kurzschluss Batteriespannung | 0 |
| 0x930861 | Treiber KL15-1: Kurzschluss Batteriespannung | 0 |
| 0x930871 | Treiber KL15N: Kurzschluss Batteriespannung | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 5 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | ja |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 1 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x40FF | Fehlerart | HEX | - | unsigned char | - | - | - | - |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 8 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x402001 | NVM E write failed | 0 |
| 0x402002 | NVM E read failed | 0 |
| 0x402003 | NVM E control failed | 0 |
| 0x402004 | NVM E erase failed | 0 |
| 0x402006 | NVM E write all failed | 0 |
| 0x402007 | NVM E read all failed | 0 |
| 0x402010 | NVM E wrong config id | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 3 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 33 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TASTER_SST | 0xDAB6 | STAT_TASTER_SST_AKTIV | Das Result enthält den aktuellen Zustand des Start-Stopp-Tasters | 0/1 | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| HO_INFO | 0xDC54 | - | Job zum Schreiben/Lesen der HändlerInformationen für die Handelsorganisation. Wird vom Werk mit Händlernummer 0 und dem Datum der Schlüssel-Initialisierung gesetzt. Diese Informationen sind Teil der CBS-Daten und werden auch in den Schlüssel übertragen. | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xDC54 | RES_0xDC54 |
| BUS_IN_ZV | 0xDAC1 | - | Vom Bus empfangener Status aller ZV-Antriebe. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDAC1 |
| CAS_MONTAGEMODUS | 0xDAB9 | - | Statusabfrage des Montagemodus für ELV-Sperre und KL50-Sperre.  Im Anlieferzustand sind immer Alle Sperren Aktiv.  Die ELV-Sperre wird mit gültigem Geschwindigkeitssignal automatisch deaktiviert. Die KL50-Sperre muss explizit per Diagnose aufgehoben werden. Ist die ELV-Sperre aktiv, so ist auch zwingend die KL50-Sperre aktiv. | - | - | - | - | - | - | - | - | - | 2E;22 | ARG_0xDAB9 | RES_0xDAB9 |
| TASTER_SICHERN_HECKKL | 0xDC68 | - | Taster Sichern an der HKL, Eingang am CAS. | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xDC68 | RES_0xDC68 |
| SCHALTER_KUPPL_PN | 0xDC63 | - | Kupplungsschalter oder PN-Signal vom EGS, 1 Taster gerückt, 0 Taster nicht gedrückt, 255 Signal ungültig / unplausibel | - | - | - | - | - | - | - | - | - | 2F;22 | ARG_0xDC63 | RES_0xDC63 |
| SCHALTER_MOTORHAUBE | 0xDC65 | - | Motorhauben-Kontakt am CAS. | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xDC65 | RES_0xDC65 |
| A_S_START_LEITUNG | 0xDC62 | - | Eingang Start-Ende-Leitung von DME/DDE an CAS. 1 Spannung liegt an, 0 Spannung liegt nicht an, 2 nicht vorhanden, 255 ungültig/Fehler. | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xDC62 | RES_0xDC62 |
| BUS_IN_DME1 | 0xDABC | - | Auslesen der vom BUS empfangenen Stati. Wird eine Botschaft innerhalb der erwarteten Zeit nicht empfangen (timeout), so wird der Status ungültig/kein Signal zurückgegeben. CAN-Signal von DME1. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDABC |
| STEUERN_KL15_ABSCHALTUNG | 0xAC51 | - | Setzen der Geschwindigkeit, bei der die Funktion KL15-Abschaltung wieder aktiviert (default) werden soll: 0 -&gt; KL15-Abschaltung wieder aktivieren xx -&gt; KL15-Abschaltung unterdrücken bis nächstes Mal über xx Kmh (xx = min. 1 Km/h bis max 50 Km/h) Mit Argument = 0 soll die KL-15-Abschaltung sofort wieder aktiviert werden können. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAC51 | - |
| SPANNUNG_KLEMME_30E_WERT | 0xDADA | STAT_SPANNUNG_KLEMME_30E_WERT | Job zum Auslesen der Klemmensteuerung am Steuergerät. | Volt | - | - | int | - | - | 10 | - | - | 22 | - | - |
| CA_TAGE_ER_LEITUNG | 0xDAB5 | - | CAS: Job zum Auslesen der analogen Spannungswerte der Entriegeln-Leitung zur TAGE | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDAB5 |
| TASTER_MSA | 0xDC67 | - | MSA-Taster am CAS. | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xDC67 | RES_0xDC67 |
| BUS_IN_DATUM_ZEIT | 0xDABB | - | CAS: Aktuelles vom Kombi empfangenes Datum/Zeit | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDABB |
| STATUS_KLEMMEN | 0xDC56 | STAT_KLEMMENSTATUS | Vom CAS aktuell gesendeter Klemmenstatus. In I-300 Job-Header, Später STATUS_LESEN. | 0-n | - | - | unsigned char | TAB_CAS_KLEMMENSTATUS | - | - | - | - | 22 | - | - |
| NACHLAUFZEIT_KLEMME_15N | 0xDB2D | STAT_NACHLAUFZEIT_KLEMME_15N_WERT | Nachlaufzeit der Klemme 15N über BUS-Nachrich in Sekunden: Interpretation siehe BN-DB | s | - | - | int | - | - | - | - | - | 22 | - | - |
| TASTER_CENTERLOCK | 0xDC64 | - | Taster Centerlock (ZV-Taster), 1 Taster gedrückt, 0 Taster nicht gedrückt, 255 Signal ungültig / unplausibel | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xDC64 | RES_0xDC64 |
| PIA_NR_AKTUELL | 0x0F27 | STAT_PIA_NR_AKTUELL | Aktuell vom CAS gesendete FBD-Personalisierungs-Nummer | 0-n | - | - | unsigned char | TAB_CAS_PIA_NUMMER | - | - | - | - | 22 | - | - |
| CAS_HW_GESCHWINDIGKEIT | 0xDC51 | STAT_HW_SPEED_STATUS | Auslesen der vom CAS (über separate HW-Leitung vom DSC) erkannte Geschwindigkeit. In I-300 Job-Header, Später STATUS_LESEN. | 0-n | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| HALL_START_STOP_TASTER | 0xDC60 | - | Hallsensor A und B des Start-Stop-Tasters am CAS. | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xDC60 | RES_0xDC60 |
| BUS_IN_FH | 0xDABF | - | Auslesen der vom BUS empfangenen Stati. Wird eine Botschaft innerhalb der erwarteten Zeit nicht empfangen (timeout), so wird der Status ungültig/kein Signal zurückgegeben. CAN-Signal Status Fensterheber (je Tür FT,BFT,FTH,BFTH). | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDABF |
| BUS_IN_DSC | 0xDABD | - | Auslesen der vom BUS empfangenen Stati. Wird eine Botschaft innerhalb der erwarteten Zeit nicht empfangen (timeout), so wird der Status ungültig/kein Signal zurückgegeben. CAN-Signal vom DSC. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDABD |
| KEY_VALID_NR_AKTUELL | 0xDAB4 | STAT_KEY_VAILD_NR_AKTUELL | Nummer des aktuell gültigen Schlüssels. | 0-n | - | - | unsigned char | - | - | - | - | - | 22 | - | - |
| NACHLAUFZEIT_KLEMME_30B | 0xDB2E | STAT_NACHLAUFZEIT_KLEMME_30B_WERT | Nachlaufzeit der Klemme 30B über BUS-Nachrich in Sekunden: Interpretation siehe BN-DB | s | - | - | int | - | - | - | - | - | 22 | - | - |
| CA_TAGE_STATUS | 0xDACA | - | Lesen der TAGE Sensorstati für jede Tür BFT, BFTH, FT, FTH. Das CAS gibt den zuletzt von der TAGE empfangenen Status für 5 Sekunden aus. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDACA |
| SPANNUNG_KLEMME_30L_WERT | 0xDADD | STAT_SPANNUNG_KLEMME_30L_WERT | Job zum Auslesen der Klemmensteuerung am Steuergerät. | Volt | - | - | int | - | - | 10 | - | - | 22 | - | - |
| SPANNUNG_HALL_VERS | 0xDAB0 | - | Spannung Hall-Sensor-Versorgung (Peak) Sensoren 1 und 3, 2 und 4 In I-300 Job-Header, Später STATUS_LESEN | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDAB0 |
| TASTER_HECKKL_INNEN | 0xDC69 | - | Heckklappentaster innen, Eingang am CAS. 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Fahrzeug besitzt keinen Taster, 255 Signal ungültig / unplausibel | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xDC69 | RES_0xDC69 |
| SCHALTER_BREMSLICHT | 0xDC61 | - | Status Bremslichtschalter High- und Low-schaltend am CAS. | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xDC61 | RES_0xDC61 |
| STEUERN_ZV_MASTER | 0xAC57 | - | Dieser Job dient dazu per Diagnose die Zentralverriegelung anzusteuern. Hinweis: Aufruf des Jobs erfolgt über Standardjob STEUERN_ROUTINE mit Argument STEUERN_ZV_MASTER. | - | - | - | - | - | - | - | - | - | 31 | ARG_0xAC57 | RES_0xAC57 |
| SPANNUNG_KLEMMEN | 0xDAB3 | - | CAS: Job zum Auslesen Analoger Klemmen-Spannungs- und Stromwerte am Steuergerät. Für I-300 über Job-Header, Später über einzel-IDs pro Wert. | - | - | - | - | - | - | - | - | - | 22 | - | RES_0xDAB3 |
| SCHALTER_HOTEL | 0xDC66 | - | Hotelschalter am CAS. | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xDC66 | RES_0xDC66 |
| EINGANG_MOST_WUP | 0xDC6A | - | Status Leitung MOST_WUP von TCU an CAS. 1 Spannung liegt an, 0 Ausgang abgeschaltet, 255 Signal ungültig / Fehler. | - | - | - | - | - | - | - | - | - | 22;2F | ARG_0xDC6A | RES_0xDC6A |

<a id="table-tab-steuern-ews4-mode"></a>
### TAB_STEUERN_EWS4_MODE

Dimensions: 8 rows × 4 columns

| WERT | NAME | TEXT | DATA_LENGTH |
| --- | --- | --- | --- |
| 0x01 | LOCK_EWS4 | LOCK DMEDDE-Sk & Trsp-Sk | 16 |
| 0x02 | WRITE_DMEDDE_SK | Write DME/DDE-Sk | 16 |
| 0x03 | WRITE_TRSP_SK | Write Trsp-Sk | 16 |
| 0x04 | LOCK_DMEDDE_SK | Lock DME/DDE-Sk | 16 |
| 0x05 | LOCK_TRSP_SK | Lock Trsp-Sk | 16 |
| 0x06 | UNLOCK_DMEDDE_SK | UnLock DME/DDE-Sk | 16 |
| 0x07 | UNLOCK_TRSP_SK | UnLock Trsp-Sk | 16 |
| 0xFF | UNKNOWN_MODE | UNKNOWN_MODE | 0 |

<a id="table-res-0xdab6"></a>
### RES_0XDAB6

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | BESCHREIBUNG |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TASTER_SST_AKTIV |  |  |  |  |  | unsigned char | 0x01 |  |  |  |  | Das Result enthält den aktuellen Zustand des Start-Stopp-Tasters |

<a id="table-tab-weckquelle"></a>
### TAB_WECKQUELLE

Dimensions: 30 rows × 2 columns

| WERT | NAME |
| --- | --- |
| 0 | Entwicklungsfunktion, reserviert |
| 1 | System wachhalten wegen Zündung an |
| 2 | Buswecken über K-CAN(L1..L4)/Body-CAN(L6) |
| 3 | Buswecken über LO-CAN(optional) |
| 4 | Buswecken über CAS-BUS(TAGE:L1..L4) |
| 5 | Taster Heckklappe öffnen innen (TOEHKI) |
| 6 | Motorhaubenkontakt (MHK) |
| 7 | Start Stopp Taster A (SSTA) |
| 8 | Start Stopp Taster B (SSTB) |
| 9 | Funkschlüssel-Einschub(EJECT) |
| 10 | Center Lock Taster (CLT) |
| 11 | Parkstellung Automatik Verriegelt (PLOCK) |
| 12 | FBD-Empfänger (L1..L4) |
| 13 | Wakeup-Signal von TCU (MOST_WUP) |
| 14 | Hotelschalter (HOTEL) |
| 15 | Bidirektionaler Funkempfänger (L6) |
| 16 | Kupplung (PN_KUPPL)(nur bei KL30B aktiv) |
| 17 | Bremse (BLTS)(nur bei KL30B aktiv) |
| 18 | Weckleitung (15WUP) |
| 19 | Reserviert |
| 20 | Taster Fahrertür (TAGE-FT-ER) |
| 21 | Taster Beifahrertür (TAGE-BFT-ER) |
| 22 | Taster Fahrertür hinten (TAGE-FTH-ER) |
| 23 | Taster Beifahrertür hinten (TAGE-BTH-ER) |
| 24 | Authentisierung Fahrertür (TAGE-FT-AUTH) |
| 25 | Authentisierung Beifahrertür (TAGE-BFT-AUTH) |
| 26 | Authentisierung Fahrer hinten (TAGE-FTH-AUTH) |
| 27 | Authentisierung Beifahrer hinten (TAGE-FTH-AUTH) |
| 28 | Kurzschluss KL30B (bei Busruhe) |
| 29 | Unterspannung (Zeitstempel sichern, kein WakeUp) |

<a id="table-res-0xdc54"></a>
### RES_0XDC54

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HAENDLER_NUMMER_WERT | - | - | string[5] | - | - | - | - | - | Händlernummer (5-stellige Nummer). Im Werk wird dieser Wert auf 00000 |

<a id="table-arg-0xdc54"></a>
### ARG_0XDC54

Dimensions: 7 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| HAENDLER_NUMMER | - | - | string[5] | - | - | - | - | - | - | - | Händlernummer (5-stellige Nummer). Im Werk wird dieser Wert auf 00000 |
| ERSTZULASSUNGSDATUM_TAG | - | - | unsigned char | - | - | - | - | - | - | - | Tag des Erstzulassungsdatums. Im werk wird dieser Wert auf den Tag der Schlüssel-Initialisierung gesetzt. |
| ERSTZULASSUNGSDATUM_MONAT | - | - | unsigned char | - | - | - | - | - | - | - | Monat des Erstzulassungsdatums.  Im werk wird dieser Wert auf den Monat der Schlüssel-Initialisierung gesetzt. |
| ERSTZULASSUNGSDATUM_JAHR | - | - | unsigned int | - | - | - | - | - | - | - | Jahr des Erstzulassungsdatums. .  Im werk wird dieser Wert auf den Jahr der Schlüssel-Initialisierung gesetzt. |
| STAT_ERSTZULASSUNGSDATUM_TAG_WERT | - | - | unsigned char | - | - | - | - | - | - | - | Tag des Erstzulassungsdatums. Im werk wird dieser Wert auf den Tag der Schlüssel-Initialisierung gesetzt. |
| STAT_ERSTZULASSUNGSDATUM_MONAT_WERT | - | - | unsigned char | - | - | - | - | - | - | - | Monat des Erstzulassungsdatums.  Im werk wird dieser Wert auf den Monat der Schlüssel-Initialisierung gesetzt. |
| STAT_ERSTZULASSUNGSDATUM_JAHR_WERT | - | - | unsigned int | - | - | - | - | - | - | - | Jahr des Erstzulassungsdatums. .  Im werk wird dieser Wert auf den Jahr der Schlüssel-Initialisierung gesetzt. |

<a id="table-res-0xdac1"></a>
### RES_0XDAC1

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STATUS_ZV_FT | 0-n | - | unsigned char | - | TAB_CAS_ZV_STATUS | - | - | - | Status Zentralverriegelung Fahrertür. |
| STATUS_ZV_BFT | 0-n | - | unsigned char | - | TAB_CAS_ZV_STATUS | - | - | - | Status Zentralverriegelung Beifahrertür. |
| STATUS_ZV_FTH | 0-n | - | unsigned char | - | TAB_CAS_ZV_STATUS | - | - | - | Status Zentralverriegelung Fahrertür-Hinten. |
| STATUS_ZV_BFTH | 0-n | - | unsigned char | - | TAB_CAS_ZV_STATUS | - | - | - | Status Zentralverriegelung Beifahrertür-Hinten. |
| STATUS_ZV_HECKKLAPPE | 0-n | - | unsigned char | - | TAB_CAS_ZV_STATUS | - | - | - | Status Zentralverriegelung Heckklappe. |
| STATUS_ZV_HECKSCHEIBE | 0-n | - | unsigned char | - | TAB_CAS_ZV_STATUS | - | - | - | Status Zentralverriegelung Heckscheibe. |

<a id="table-tab-cas-zv-status"></a>
### TAB_CAS_ZV_STATUS

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Entriegelt |
| 1 | Verriegelt |
| 2 | Gesichert |
| 128 | Klappe/Scheibe geschlossen |
| 129 | Klappe/Scheibe geöffnet |
| 130 | Klappe in Vorrast |
| 255 | ungültig |

<a id="table-res-0xdab9"></a>
### RES_0XDAB9

Dimensions: 1 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CAS_MONTAGEMODUS | 0-n | - | unsigned char | - | TAB_CAS_MONTAGEMODUS | - | - | - | Die ELV-Sperre (ELV-Montagemodus) verhindert die Ansteuerung (Verriegeln/Entriegeln) der ELV während des Montage-Prozesses. Die ELV-Diagnosen (z.B. Status-Abfragen, ELV-Ident) sind zulässig. Die KL50-Sperre verhindert das Ansteuern des Anlassers während des Montage-Prozesses. Definierte Montagemodi: 0 Alle Montagemodi sind deaktiviert (ELV- und KL50-Ansteuerung wird durchgeführ), 1 Nur KL50-Montagemodus aktiv (kein Anlasser), 2 ELV- und KL50 Montage-Modus sind aktiv (keine ELV-Ansteuerung, kein Anlasser) |

<a id="table-arg-0xdab9"></a>
### ARG_0XDAB9

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CAS_MONTAGEMODUS | 0-n | - | unsigned char | - | TAB_CAS_MONTAGEMODUS | - | - | - | - | - | Die ELV-Sperre (ELV-Montagemodus) verhindert die Ansteuerung (Verriegeln/Entriegeln) der ELV während des Montage-Prozesses. Die ELV-Diagnosen (z.B. Status-Abfragen, ELV-Ident) sind zulässig. Die KL50-Sperre verhindert das Ansteuern des Anlassers während des Montage-Prozesses. Definierte Montagemodi: 0 Alle Montagemodi sind deaktiviert (ELV- und KL50-Ansteuerung wird durchgeführ), 1 Nur KL50-Montagemodus aktiv (kein Anlasser), 2 ELV- und KL50 Montage-Modus sind aktiv (keine ELV-Ansteuerung, kein Anlasser) |

<a id="table-tab-cas-montagemodus"></a>
### TAB_CAS_MONTAGEMODUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Normalbetrieb - Alle Montagemodi deaktiviert |
| 1 | KL50-Montagemodus - Anlassersperre aktiv |
| 2 | ELV_KL50-Montagemodus - Anlassersperre und keine Ansteuerung ELV |
| 255 | unbekannter Zustand |

<a id="table-res-0xdc68"></a>
### RES_0XDC68

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TASTER_SICHERN_HECKKL_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Taster Sichern an der HKL, Eingang am CAS. 1 Taster gedrückt, 0 Taster nicht gedrückt, 255 Signal ungültig / unplausibel |
| STAT_TASTER_SICHERN_HECKKL_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Taster Sichern an der HKL, Eingang am CAS. 1 Taster gedrückt, 0 Taster nicht gedrückt, 255 Signal ungültig / unplausibel |

<a id="table-arg-0xdc68"></a>
### ARG_0XDC68

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TASTER_SICHERN_HECKKL | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | - | - | Taster Sichern an der HKL, Eingang am CAS. 1 Taster gedrückt, 0 Taster nicht gedrückt. |

<a id="table-res-0xdc63"></a>
### RES_0XDC63

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHALTER_KUPPL_PN_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Kupplungsschalter oder PN-Signal vom EGS, 1 Taster gerückt, 0 Taster nicht gedrückt, 255 Signal ungültig / unplausibel |
| STAT_SCHALTER_KUPPL_PN_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Kupplungsschalter oder PN-Signal vom EGS, 1 Taster gerückt, 0 Taster nicht gedrückt, 255 Signal ungültig / unplausibel |

<a id="table-arg-0xdc63"></a>
### ARG_0XDC63

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SCHALTER_KUPPL_PN | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | - | - | Kupplungsschalter oder PN-Signal vom EGS, 1 Taster gerückt, 0 Taster nicht gedrückt. |

<a id="table-res-0xdc65"></a>
### RES_0XDC65

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHALTER_MOTORHAUBE_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Motorhauben-Kontakt, 1 aktiv (offen), 0 nicht aktiv (geschlossen), 2 Fahrzeug besitzt keinen Motorhaubenkontakt, 255 Signal ungültig / unplausibel |
| STAT_SCHALTER_MOTORHAUBE_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Motorhauben-Kontakt, 1 aktiv (offen), 0 nicht aktiv (geschlossen), 2 Fahrzeug besitzt keinen Motorhaubenkontakt, 255 Signal ungültig / unplausibel |

<a id="table-arg-0xdc65"></a>
### ARG_0XDC65

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SCHALTER_MOTORHAUBE | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | - | - | Status Motorhauben-Kontakt vorgrbrn, 1 aktiv (offen), 0 nicht aktiv (geschlossen). |

<a id="table-res-0xdc62"></a>
### RES_0XDC62

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_EINGANG_A_S_START_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Eingang Start-Ende-Leitung von DME/DDE, 1 Spannung liegt an, 0 Spannung liegt nicht an, 2 nicht vorhanden, 255 ungültig/Fehler. |
| STAT_EINGANG_A_S_START_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Eingang Start-Ende-Leitung von DME/DDE, 1 Spannung liegt an, 0 Spannung liegt nicht an, 2 nicht vorhanden, 255 ungültig/Fehler. |

<a id="table-arg-0xdc62"></a>
### ARG_0XDC62

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| EINGANG_A_S_START | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | - | - | Eingang Start-Ende-Leitung von DME/DDE, 1 Spannung liegt an, 0 Spannung liegt nicht an. |

<a id="table-res-0xdabc"></a>
### RES_0XDABC

Dimensions: 6 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BUS_IN_GANG | 0-n | - | unsigned char | - | TAB_CAS_GANG | - | - | - | Auslesen der vom BUS empfangenen Stati. Wird eine Botschaft innerhalb der erwarteten Zeit nicht empfangen (timeout), so wird der Status ungültig/kein Signal zurückgegeben. CAN-Signal Gang von DME1. 1 N neutral; 2 R rückwärts; 3 P Park; 5 Gang 1; 6 Gang 2; 7 Gang 3; 8 Gang 4; 9 Gang 5; 10 Gang 6; 11 Gang 7; 12 Gang 8; 255 ungültig / kein Signal |
| STAT_BUS_IN_MOTOR_LAEUFT | 0-n | - | unsigned char | - | TAB_CAS_MOTOR_STATUS | - | - | - | Auslesen der vom BUS empfangenen Stati. Wird eine Botschaft innerhalb der erwarteten Zeit nicht empfangen (timeout), so wird der Status ungültig/kein Signal zurückgegeben. CAN-Signal Motor läuft von DME1. 0 Motor aus; 1 Motor startet; 2 Motor läuft: 255 ungültig / kein Signal |
| STAT_BUS_IN_MOTOR_FREIGABE | 0-n | - | unsigned char | - | TAB_CAS_MOTORSTART_FREIGABE | - | - | - | Auslesen der vom BUS empfangenen Stati. Wird eine Botschaft innerhalb der erwarteten Zeit nicht empfangen (timeout), so wird der Status ungültig/kein Signal zurückgegeben. CAN-Signal Motor Freigabe von DME1. 0 Kein Motorstart; 1 Motorstart verzögert; 2 Motorstart zugelassen; 255 ungültig / kein Signal |
| STAT_BUS_IN_ANLASSER_SPERRE | 0-n | - | unsigned char | - | TAB_CAS_MOTOR_ANLASSERSPERRE | - | - | - | Auslesen der vom BUS empfangenen Stati. Wird eine Botschaft innerhalb der erwarteten Zeit nicht empfangen (timeout), so wird der Status ungültig/kein Signal zurückgegeben. CAN-Signal Anlasser Sperre von DME1. 0 Kein Motorstart, Getriebe D / R; 1 Motorstart zulassen, Getriebe N; 2 Motorstart und -stop zulassen Getriebe in P; 255 ungültig / kein Signal |
| STAT_BUS_IN_KUPPLUNG | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Auslesen der vom BUS empfangenen Stati. Wird eine Botschaft innerhalb der erwarteten Zeit nicht empfangen (timeout), so wird der Status ungültig/kein Signal zurückgegeben. CAN-Signal Kupplung von DME1. 0 Kupplung nicht betätigt; 1 Kupplung betätigt; 255 ungültig / kein Signal / nicht verbaut |
| STAT_BUS_IN_DREHZAHL_WERT | U/min | - | unsigned int | - | - | - | 4 | - | Auslesen der vom BUS empfangenen Stati. Wird eine Botschaft innerhalb der erwarteten Zeit nicht empfangen (timeout), so wird der Status ungültig/kein Signal zurückgegeben. CAN-Signal Drehzahl von DME1. Aktuelle Drehzahl; -1 ungültige Drehzahl |

<a id="table-tab-cas-gang"></a>
### TAB_CAS_GANG

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | N - Kein Kraftschluss |
| 2 | R - Rückwärtsgang |
| 3 | P - Parkposition |
| 5 | 1. Gang |
| 6 | 2. Gang |
| 7 | 3. Gang |
| 8 | 4. Gang |
| 9 | 5. Gang |
| 10 | 6. Gang |
| 11 | 7. Gang |
| 12 | 8. Gang |
| 255 | ungültig |

<a id="table-tab-cas-motor-status"></a>
### TAB_CAS_MOTOR_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Motor aus |
| 1 | Motor startet |
| 2 | Motor läuft |
| 255 | ungültig/unbekannt |

<a id="table-tab-cas-motorstart-freigabe"></a>
### TAB_CAS_MOTORSTART_FREIGABE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein Motorstart |
| 1 | Motorstart/-stop verzögert |
| 2 | Motorstart zulassen |
| 255 | ungültig/unbekannt |

<a id="table-tab-cas-motor-anlassersperre"></a>
### TAB_CAS_MOTOR_ANLASSERSPERRE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Motorstart zulassen - Getriebe in N |
| 0 | Kein Motorstart, Pos. D/R |
| 2 | Motorstart zulassen, Motorstop zulassen - Getriebe in P |
| 255 | ungültig/unbekannt |

<a id="table-arg-0xac51"></a>
### ARG_0XAC51

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DEAKTIVIERUNGSGESCHWINDIGKEIT | km/h | - | unsigned char | - | - | - | - | - | - | - | Gibt an bei welcher Geschindigkeit die Funktion KL15-Abschaltung wieder aktiviert (default) werden soll: 0 -&gt; KL15-Abschaltung wieder aktivieren xx -&gt; KL15-Abschaltung unterdrücken bis nächstes Mal über xx Kmh (xx = min. 1 Km/h bis max 50 Km/h) Mit Argument = 0 soll die KL-15-Abschaltung sofort wieder aktiviert werden können. |

<a id="table-res-0xdab5"></a>
### RES_0XDAB5

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_STROM_TAGE_ER_FT_WERT | A | - | unsigned int | - | - | - | 1000 | - | Strom der Entriegeln-Leitung zur TAGE Fahrertüre. Mittelwert über je 100 ms. |
| STAT_STROM_TAGE_ER_BFT_WERT | A | - | unsigned int | - | - | - | 1000 | - | Strom der Entriegeln-Leitung zur TAGE Beiahrertüre. Mittelwert über je 100 ms. |
| STAT_STROM_TAGE_ER_FTH_WERT | A | - | unsigned int | - | - | - | 1000 | - | Strom der Entriegeln-Leitung zur TAGE Fahrertüre hinten. Mittelwert über je 100 ms. |
| STAT_STROM_TAGE_ER_BFTH_WERT | A | - | unsigned int | - | - | - | 1000 | - | Strom der Entriegeln-Leitung zur TAGE Beiahrertüre hinten. Mittelwert über je 100 ms. |

<a id="table-res-0xdc67"></a>
### RES_0XDC67

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TASTER_MSA_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Status MSA-Taster am CAS. 1 Taster gedrückt, 0 Taster nicht gedrückt, 2 Fahrzeug besitzt keinen Taster, 255 Signal ungültig / unplausibel |
| STAT_TASTER_MSA_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Status MSA-Taster am CAS. 1 Taster gedrückt, 0 Taster nicht gedrückt, 2 Fahrzeug besitzt keinen Taster, 255 Signal ungültig / unplausibel |

<a id="table-arg-0xdc67"></a>
### ARG_0XDC67

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TASTER_MSA | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | - | - | Status MSA-Taster am CAS. 1 Taster gedrückt, 0 Taster nicht gedrückt. |

<a id="table-res-0xdabb"></a>
### RES_0XDABB

Dimensions: 7 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BUS_IN_ZEIT_STUNDEN | 0-n | - | unsigned char | - | - | - | - | - | Stunden: 0 - 23; 253 entspricht  -- ; 254 Keine Angabe: 255 Signal ungültig |
| STAT_BUS_IN_ZEIT_MINUTEN | 0-n | - | unsigned char | - | - | - | - | - | Minuten: 0 - 59; 253 entspricht  -- ; 254 Keine Angabe; 255 Signal ungültig |
| STAT_BUS_IN_DATUM_TAG | 0-n | - | unsigned char | - | - | - | - | - | Tag: 1 - 31 |
| STAT_BUS_IN_DATUM_MONAT | 0-n | - | unsigned char | - | - | - | - | - | Monat: 1 - 12 |
| STAT_BUS_IN_DATUM_JAHR | 0-n | - | unsigned int | - | - | - | - | - | Jahr: 1 - 65534 |
| STAT_BUS_IN_ZEIT_RELATIV_WERT | - | - | unsigned long | - | - | - | - | - | Aktuelles Relative Zeit in Sekunden seit 01.01.2000, Sekuden: 0 - 4,2 Millarden |
| STAT_BUS_IN_ZEIT_TAGE_RELATIV_WERT | - | - | unsigned int | - | - | - | - | - | Aktuelles Relative gesehene Tage seit 01.01.2000; Tage: 1 entspricht 01.01.2000 |

<a id="table-tab-cas-klemmenstatus"></a>
### TAB_CAS_KLEMMENSTATUS

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | INIT |
| 1 | Reserve |
| 2 | KL30 alle Klemmen aus |
| 3 | KL30F-Änderung |
| 4 | KL30F |
| 5 | KL30B-Änderung |
| 6 | KL30B |
| 7 | KLR-Änderung |
| 8 | KLR |
| 9 | KL15-Änderung |
| 10 | KL15 |
| 11 | KL50-Verzögerung |
| 12 | KL50-Änderung |
| 13 | KL50 |
| 14 | Fehler |
| 15 | Ungültig |

<a id="table-res-0xdc64"></a>
### RES_0XDC64

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TASTER_CENTERLOCK_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | HW Taster Centerlock, 1 Taster gerückt, 0 Taster nicht gedrückt, 255 Signal ungültig / unplausibel |
| STAT_TASTER_CENTERLOCK_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | HW Taster Centerlock, 1 Taster gerückt, 0 Taster nicht gedrückt, 255 Signal ungültig / unplausibel |

<a id="table-arg-0xdc64"></a>
### ARG_0XDC64

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TASTER_CENTERLOCK | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | - | - | Status Taster Centerlock vorgeben, 1 Taster gedrückt, 0 Taster nicht gedrückt. |

<a id="table-tab-cas-pia-nummer"></a>
### TAB_CAS_PIA_NUMMER

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Personalisierungskonfiguration 0 |
| 1 | Personalisierungskonfiguration 1 |
| 2 | Personalisierungskonfiguration 2 |
| 10 | Gast |
| 15 | ungültig |

<a id="table-res-0xdc60"></a>
### RES_0XDC60

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_HALL_SSTA_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Status des SST Hall-Sensors A (entprellt), 0 nicht aktiv, 1 aktiv |
| STAT_HALL_SSTB_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Status des SST Hall-Sensors B (entprellt), 0 nicht aktiv, 1 aktiv |
| STAT_HALL_SSTA_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Status des SST Hall-Sensors A (entprellt), 0 nicht aktiv, 1 aktiv |
| STAT_HALL_SSTB_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Status des SST Hall-Sensors B (entprellt), 0 nicht aktiv, 1 aktiv |

<a id="table-arg-0xdc60"></a>
### ARG_0XDC60

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| HALL_SSTA | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | - | - | Vorgeben des Status von Hallsensor A. 0 nicht aktiv, 1 aktiv. |
| HALL_SSTB | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | - | - | Vorgeben des Status von Hallsensor B. 0 nicht aktiv, 1 aktiv. |

<a id="table-res-0xdabf"></a>
### RES_0XDABF

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BUS_IN_FH_FT | 0-n | - | unsigned char | - | TAB_CAS_FH_STATUS | - | - | - | CAN-Signal Status Fensterheber Fahrertür, 0 Geschlossen; 1 Zwischenstellung; 2 Offen; 255 Signal ungültig / unplausibel |
| STAT_BUS_IN_FH_BFT | 0-n | - | unsigned char | - | TAB_CAS_FH_STATUS | - | - | - | CAN-Signal Status Fensterheber Beifahrertür, 0 Geschlossen; 1 Zwischenstellung; 2 Offen; 255 Signal ungültig / unplausibel |
| STAT_BUS_IN_FH_FTH | 0-n | - | unsigned char | - | TAB_CAS_FH_STATUS | - | - | - | CAN-Signal Status Fensterheber fahrertür hinten, 0 Geschlossen; 1 Zwischenstellung; 2 Offen; 255 Signal ungültig / unplausibel |
| STAT_BUS_IN_FH_BFTH | 0-n | - | unsigned char | - | TAB_CAS_FH_STATUS | - | - | - | CAN-Signal Status Fensterheber Beifahrertür hinten, 0 Geschlossen; 1 Zwischenstellung; 2 Offen; 255 Signal ungültig / unplausibel |

<a id="table-tab-cas-fh-status"></a>
### TAB_CAS_FH_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Geschlossen |
| 1 | Zwischenstellung |
| 2 | Offen |
| 255 | ungültig/unbekannt |

<a id="table-res-0xdabd"></a>
### RES_0XDABD

Dimensions: 3 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_BUS_IN_GESCHW_WERT | km/h | - | unsigned int | - | - | - | 64 | - | Auslesen der vom BUS empfangenen Stati. Wird eine Botschaft innerhalb der erwarteten Zeit nicht empfangen (timeout), so wird der Status ungültig/kein Signal zurückgegeben. CAN-Signal Geschwindigkeit vom DSC. CAN-Signal Geschwindigkeit vom DSC |
| STAT_BUS_IN_GESCHW_STATUS | 0-n | - | unsigned char | - | TAB_CAS_GESCHW_STATUS | - | - | - | Auslesen der vom BUS empfangenen Stati. Wird eine Botschaft innerhalb der erwarteten Zeit nicht empfangen (timeout), so wird der Status ungültig/kein Signal zurückgegeben. CAN-Signal Geschwindigkeit-Status vom DSC. 0 Fahrzeug steht; 1 Fahrzeug fährt vorwärts; 2 Fahrzeug fährt rückwärts; 3 Fahrzeug fährt; 4 Fahrzeug steht Hinterachse auf Rollenprüfstand; 7 ungültig / kein Signal |
| STAT_BUS_IN_BREMSPEDAL | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Auslesen der vom BUS empfangenen Stati. Wird eine Botschaft innerhalb der erwarteten Zeit nicht empfangen (timeout), so wird der Status ungültig/kein Signal zurückgegeben. CAN-Signal Status Bremspedal vom DSC. 0 Nicht betätigt; 1 Betätigt; 255 Signal ungültig / unplausibel (Hinweis: CAN-Signal Status_Bremsung_Fahrer, Auswertung der Bit-Kodierung Betätigung_Bremssystem_Fahrer + Gesamtsignal ungültig muss im CAS erfolgen). |

<a id="table-tab-cas-geschw-status"></a>
### TAB_CAS_GESCHW_STATUS

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Fahrzeug steht |
| 1 | Fahrzeug fährt vorwärts |
| 2 | Fahrzeug fährt rückwärts |
| 3 | Fahrzeug fährt |
| 4 | Fahrzeug steht, Hinterachse auf Rollenprüfstand erkannt |
| 7 | Signal ungültig |

<a id="table-res-0xdaca"></a>
### RES_0XDACA

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TAGE_FT | 0-n | - | unsigned char | - | - | - | - | - | Status TAGE Fahrertüre, 0 Kein Status (keine Betätigung), 1 Zugsensor Betätigt (Hall); 2 Sichern Sensor Betätigt (Piezo UND VR-Kap-Sensor); 3 Entriegeln Sensor Betätigt (ER-Kap-Sensor) |
| STAT_TAGE_BFT | 0-n | - | unsigned char | - | - | - | - | - | Status TAGE Beifahrertüre, 0 Kein Status (keine Betätigung), 1 Zugsensor Betätigt (Hall); 2 Sichern Sensor Betätigt (Piezo UND VR-Kap-Sensor); 3 Entriegeln Sensor Betätigt (ER-Kap-Sensor) |
| STAT_TAGE_FTH | 0-n | - | unsigned char | - | - | - | - | - | Status TAGE Fahrertüre hinten, 0 Kein Status (keine Betätigung), 1 Zugsensor Betätigt (Hall); 2 Sichern Sensor Betätigt (Piezo UND VR-Kap-Sensor); 3 Entriegeln Sensor Betätigt (ER-Kap-Sensor) |
| STAT_TAGE_BFTH | 0-n | - | unsigned char | - | - | - | - | - | Status TAGE Beifahrertüre hinten, 0 Kein Status (keine Betätigung), 1 Zugsensor Betätigt (Hall); 2 Sichern Sensor Betätigt (Piezo UND VR-Kap-Sensor); 3 Entriegeln Sensor Betätigt (ER-Kap-Sensor) |

<a id="table-res-0xdab0"></a>
### RES_0XDAB0

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_HALL_VERS13_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannung Hall-Sensor-Versorgung (Peak) Sensoren 1 und 3 |
| STAT_SPANNUNG_HALL_VERS24_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannung Hall-Sensor-Versorgung (Peak) Sensoren 2 und 4 |

<a id="table-res-0xdc69"></a>
### RES_0XDC69

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_TASTER_HECKKL_INNEN_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Heckklappentaster innen, Eingang am CAS. 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Fahrzeug besitzt keinen Taster, 255 Signal ungültig / unplausibel. |
| STAT_TASTER_HECKKL_INNEN_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Heckklappentaster innen, Eingang am CAS. 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Fahrzeug besitzt keinen Taster, 255 Signal ungültig / unplausibel. |

<a id="table-arg-0xdc69"></a>
### ARG_0XDC69

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TASTER_HECKKL_INNEN | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | - | - | Heckklappentaster innen, Eingang am CAS. 1 Taster gerückt, 0 Taster nicht gedrückt. |

<a id="table-res-0xdc61"></a>
### RES_0XDC61

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHALTER_BREMSL_HIGH_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | HW Taster Bremslichtschalter, 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Taster nicht vorhanden (kein Automatik-Getriebe), 255 Signal ungültig / unplausibel |
| STAT_SCHALTER_BREMSL_LOW_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | HW Taster Bremslichtschalter (Test-Schalter), 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Taster nicht vorhanden (kein Automatik-Getriebe), 255 Signal ungültig / unplausibel |
| STAT_SCHALTER_BREMSL_HIGH_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | HW Taster Bremslichtschalter, 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Taster nicht vorhanden (kein Automatik-Getriebe), 255 Signal ungültig / unplausibel |
| STAT_SCHALTER_BREMSL_LOW_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | HW Taster Bremslichtschalter (Test-Schalter), 1 Taster gerückt, 0 Taster nicht gedrückt, 2 Taster nicht vorhanden (kein Automatik-Getriebe), 255 Signal ungültig / unplausibel |

<a id="table-arg-0xdc61"></a>
### ARG_0XDC61

Dimensions: 2 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SCHALTER_BREMSL_HIGH | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | - | - | Status des High-schaltenden Bremslichtschalters vorgeben. 1 Taster gerückt, 0 Taster nicht gedrückt. |
| SCHALTER_BREMSL_LOW | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | - | - | Status des Low-schaltenden Bremslichtschalters vorgeben. 1 Taster gerückt, 0 Taster nicht gedrückt. |

<a id="table-res-0xac57"></a>
### RES_0XAC57

Dimensions: 1 rows × 13 columns

| RESULTNAME | STR | STPR | RRR | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_ZV_STATUS | + | + | + | 0-n | - | unsigned char | - | TAB_ZV_ZUSTAND | - | - | - | Aktuell gesendeter ZV-Status: 0 Unbekannter Status, 1 mindestens eine Tür entriegelt, 2 mindestens eine Tür verriegelt, 4 interner Status ist gesichert, 15 ungültig (Kombinationen siehe Tabelle TAB_ZV_ZUSTAND). |

<a id="table-arg-0xac57"></a>
### ARG_0XAC57

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ZV_AKTION | 0-n | - | unsigned char | - | TAB_ZV_AKTION | - | - | - | - | - | Das Argument enthält die auszuführende ZV-Aktion. Mögliche Argumente sind: 0=keine Aktion, 1=Entriegeln, 2=Verriegeln, 3=Sichern, 4=Selektiv entriegeln, 5=logisch entriegeln. |

<a id="table-tab-zv-aktion"></a>
### TAB_ZV_AKTION

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Aktion |
| 1 | Entriegeln |
| 2 | Verriegeln |
| 3 | Sichern |
| 4 | Selektiv Entriegeln |
| 5 | logisch Entriegeln |
| 100 | Elektrisch öffnen ist aktiv |
| 255 | ungültig |

<a id="table-tab-zv-zustand"></a>
### TAB_ZV_ZUSTAND

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Status noch unbekannt |
| 1 | mindestens eine Tür entriegelt - keine Tür verriegelt oder gesichert |
| 2 | mindestens eine Tür verriegelt - keine Tür entriegelt |
| 3 | mindestens eine Tür entriegelt - mindestens eine Tür verriegelt |
| 4 | alle Türen gesichert |
| 5 | gesichert - mindestens eine Tür entriegelt |
| 6 | teilweise gesichert - Zwischenzustand oder Fehlerzustand |
| 7 | teilweise gesichert - Zwischenzustand oder Fehlerzustand |
| 15 | ungültig |

<a id="table-res-0xdab3"></a>
### RES_0XDAB3

Dimensions: 16 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SPANNUNG_KLEMME_30B_1_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannungswert am Steuergerät an Klemme 30B_1 Bei Alt-Baureihen entspricht dies Klemme R Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_30B_2_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannungswert am Steuergerät an Klemme 30B_2 Bei Alt-Baureihen entspricht dies Klemme R Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_30B_3_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannungswert am Steuergerät an Klemme 30B_3 Bei Alt-Baureihen entspricht dies Klemme R Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15WUP_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannungswert am Steuergerät an Klemme 15_WUP Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15N_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannungswert am Steuergerät an Klemme 15N Bei Alt-Baureihen entspricht dies KL30G Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15_1_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannungswert am Steuergerät an Klemme 15_1 Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15_2_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannungswert am Steuergerät an Klemme 15_2 Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_15_3_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannungswert am Steuergerät an Klemme 15_3 Bei CAS Ausgang |
| STAT_STROM_KLEMME_15_50_WERT | V | - | unsigned int | - | - | - | 1000 | - | Stromwert am Steuergerät an Klemme 15 und 50 Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_50_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannungswert am Steuergerät an Klemme 50 Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_50MSA_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannungswert am Steuergerät an Klemme 50MSA Bei CAS Ausgang |
| STAT_STROM_LF_WERT | A | - | unsigned int | - | - | - | 1000 | - | Stromwert am Steuergerät an LF (CA-Antennen) Bei CAS Ausgang |
| STAT_DIAG_LF_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannung am Steuergerät an LF (CA-Antennen) Bei CAS Ausgang |
| STAT_SPANNUNG_KLEMME_31ELV_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannungswert am CAS-Steuergerät an Klemme 30_ELV Ausgang am CAS |
| STAT_SPANNUNG_KLEMME_30ELV_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannungswert am CAS-Steuergerät an Klemme 30_ELV Ausgang am CAS |
| STAT_SPANNUNG_INNENTEMPERATUR_WERT | V | - | unsigned int | - | - | - | 1000 | - | Spannung am PTC/NTC im Steuergerät zur Ermittlung der Innentemperatur |

<a id="table-res-0xdc66"></a>
### RES_0XDC66

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_SCHALTER_HOTEL_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Hotelschalter, 1 Hotelfunktion aktiv, 0 Hotelfunktion nicht aktiv, 2 Fahrzeug besitzt keinen Hotelschalter, 255 Signal ungültig / unplausibel |
| STAT_SCHALTER_HOTEL_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Hotelschalter, 1 Hotelfunktion aktiv, 0 Hotelfunktion nicht aktiv, 2 Fahrzeug besitzt keinen Hotelschalter, 255 Signal ungültig / unplausibel |

<a id="table-arg-0xdc66"></a>
### ARG_0XDC66

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SCHALTER_HOTEL | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | - | - | Hotelschalter, 1 Hotelfunktion aktiv, 0 Hotelfunktion nicht aktiv. |

<a id="table-res-0xdc6a"></a>
### RES_0XDC6A

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_EINGANG_MOST_WUP_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Status Leitung MOST_WUP von TCU an CAS. 1 Spannung liegt an, 0 Ausgang abgeschaltet, 255 Signal ungültig / Fehler. |
| STAT_EINGANG_MOST_WUP_AKTIV | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | Status Leitung MOST_WUP von TCU an CAS. 1 Spannung liegt an, 0 Ausgang abgeschaltet, 255 Signal ungültig / Fehler. |

<a id="table-arg-0xdc6a"></a>
### ARG_0XDC6A

Dimensions: 1 rows × 12 columns

| ARG | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | MIN | MAX | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| EINGANG_MOST_WUP | 0-n | - | unsigned char | - | TAB_CAS_DIGITAL_EINGANG | - | - | - | - | - | Status Leitung MOST_WUP von TCU an CAS. 1 Spannung liegt an, 0 Ausgang abgeschaltet. |

<a id="table-tab-cas-digital-eingang"></a>
### TAB_CAS_DIGITAL_EINGANG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht aktiv / nicht betätigt |
| 1 | aktiv / betätigt |
| 2 | nicht verbaut / Status nicht verfügbar |
| 255 | ungültig / Fehler erkannt |
