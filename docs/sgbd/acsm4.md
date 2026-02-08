# acsm4.prg

- Jobs: [86](#jobs)
- Tables: [39](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Airbag (ACSM4-B, ACSM4-C) |
| ORIGIN | BMW EI-510 Erich.Daucher |
| REVISION | 4.003 |
| AUTHOR | BMW EI-622 Erich.Daucher |
| COMMENT | N/A |
| PACKAGE | 1.57 |
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
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers UDS  : $85 ControlDTCSetting UDS  : $?? Sperren ($02) / Freigabe ($01) Modus: Default
- [IS_LESEN](#job-is-lesen) - Sekundaerer Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $22   ReadDataByIdentifierRequestServiceID UDS  : $2000 DataIdentifier sekundaerer Fehlerspeicher Modus: Default
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - sekundären Fehlerspeicher lesen (Info-Meldungen / Ort und Art) UDS  : $22 ReadDataByIdentifier UDS  : $20 dataIdentifier UDS  : $00 alle Info-Meldungen anschließend UDS  : $20 dataIdentifier UDS  : $nn Details zur Info-Meldung an der Position n Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen UDS  : $31   RoutineControl UDS  : $01   startRoutine UDS  : $0F06 ClearSecondaryDTCMemory Modus: Default
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
- [DIAGNOSEPROTOKOLL_LESEN](#job-diagnoseprotokoll-lesen) - Gibt die möglichen Diagnoseprotokolle für eine Auswahl an den Aufrufer zurück
- [CAF_LOGISTIKDATEN_LESEN](#job-caf-logistikdaten-lesen) - CAF Logistikdaten lesen (CAF1 ? CAF3) UDS : $22 ReadDataByIdentifier UDS : $3003 CAF_LOGISTIKDATEN_LESEN (CAF1) UDS : $30FB CAF_LOGISTIKDATEN_LESEN (CAF2) UDS : $311B CAF_LOGISTIKDATEN_LESEN (CAF3) Modus: Default
- [CODIERDATEN_LESEN](#job-codierdaten-lesen) - Codierdaten blockweise lesen (CAF1 ? CAF3) UDS : $22 ReadDataByIdentifier UDS : $3000 ? $311D RDBI_CD Modus: Default
- [STATUS_DEBUG_INFO_LESEN](#job-status-debug-info-lesen) - DTC Debug Info lesen UDS : $22 ReadDataByIdentifier UDS : $4061 DEBUG_INFO_LESEN1 UDS : $4062 DEBUG_INFO_LESEN2 UDS : $4063 DEBUG_INFO_LESEN3 Modus: Default
- [STATUS_EDR_PUBLIC_DATA_LESEN](#job-status-edr-public-data-lesen) - EDR-PUBLIC-DATA lesen UDS : $22 ReadDataByIdentifier UDS : $FA13 EDR-PUBLIC-DATA_LESEN1 UDS : $FA14 EDR-PUBLIC-DATA_LESEN2 UDS : $FA15 EDR-PUBLIC-DATA_LESEN3 UDS : $FA16 EDR-PUBLIC-DATA_LESEN4 UDS : $FA17 EDR-PUBLIC-DATA_LESEN5 Modus: Development
- [STEUERN_DIAGNOSEART_AENDERN](#job-steuern-diagnoseart-aendern) - Diagnoseart aendern UDS : $3101 RoutineControl UDS : $F200 DIAGNOSEART_AENDERN_BMW_DIAG UDS : $F201 DIAGNOSEART_AENDERN_SUPPL_DIAG Modus: Development
- [STEUERN_DTC_DEBUG_INFO_LOESCHEN](#job-steuern-dtc-debug-info-loeschen) - DTC Debug Info loeschen UDS : $3101 RoutineControl UDS : $F011 DEBUG_INFO_LOESCHEN1 UDS : $F012 DEBUG_INFO_LOESCHEN2 UDS : $F013 DEBUG_INFO_LOESCHEN3 Modus: Default
- [_STATUS_NEAR_CRASH_DATEN_LESEN](#job-status-near-crash-daten-lesen) - NEAR_CRASH-Daten lesen UDS : $22 ReadDataByIdentifier UDS : $4023 NEAR_CRASH_DATEN_LESEN1 UDS : $4024 NEAR_CRASH_DATEN_LESEN2 Modus: Development Dies ist kein NHTSA-EDR, sondern ein Near-Crash-Recoder
- [STATUS_BATTERIESPANNUNG_AM_SG](#job-status-batteriespannung-am-sg) - Batteriespannung am Steuergeraet lesen UDS : $22 ReadDataByIdentifier UDS : $4006 BATTERIESPANNUNG_AM_SG Modus: Default (0x4006)
- [STATUS_FEHLERZAEHLER_PRIMAER](#job-status-fehlerzaehler-primaer) - Anzahl Eintraege Primaerer Fehlerspeicher lesen UDS : $22 ReadDataByIdentifier UDS : $4015 FEHLERZAEHLER_PRIMAER Modus: Default (0x4015)
- [STATUS_FEHLERZAEHLER_SEKUNDAER](#job-status-fehlerzaehler-sekundaer) - Anzahl Eintraege Sekundaerer Fehlerspeicher lesen UDS : $22 ReadDataByIdentifier UDS : $4016 FEHLERZAEHLER_SEKUNDAER Modus: Default (0x4016)
- [STATUS_VERRIEGELUNG_LESEN](#job-status-verriegelung-lesen) - Status Verriegelung lesen UDS : $22 ReadDataByIdentifier UDS : $4080 VERRIEGELUNG_LESEN Modus: Default (0x4080)
- [STEUERN_VERRIEGELUNG_SCHREIBEN](#job-steuern-verriegelung-schreiben) - Verriegelung schreiben UDS : $2E WriteDataByIdentifier UDS : $4080 VERRIEGELUNG_SCHREIBEN Modus: Default (0x4080)
- [SBE_DATEN](#job-sbe-daten) - Daten Sitzmatten lesen UDS : $22 ReadDataByIdentifier UDS : $4085 SBE_DATEN Modus: Default (0x4085)
- [STATUS_AUSSTATTUNG](#job-status-ausstattung) - Ausstattung lesen (CAF1) UDS : $22 ReadDataByIdentifier UDS : $4070 AUSSTATTUNG Modus: Default (0xD470)
- [STATUS_LESEN_AIRBAG](#job-status-lesen-airbag) - IO Bytes des Steuergeraets UDS : $22 ReadDataByIdentifier UDS : $D471 LESEN_AIRBAG Modus: Default (0xD471)
- [STATUS_FREIGABE_ZUENDKREISE](#job-status-freigabe-zuendkreise) - Freigabeinfo Zuendkreise UDS : $22 ReadDataByIdentifier UDS : $D472 FREIGABE_ZUENDKREIS Modus: Default (0xD472)
- [STATUS_WIDERSTAND_ZUENDKREIS](#job-status-widerstand-zuendkreis) - Widerstandswert Zuendkreise auslesen UDS : $22 ReadDataByIdentifier UDS : $D473 WIDERSTAND_ZUENDKREIS Modus: Default (0xD473)
- [STATUS_GURTKONTAKTE](#job-status-gurtkontakte) - Stromwerte Gurtkontakte, POS und SPS auslesen UDS : $22 ReadDataByIdentifier UDS : $D474 GURTKONTAKTE Modus: Default (0xD474)
- [STATUS_FEHLERZAEHLER_SAT_LESEN](#job-status-fehlerzaehler-sat-lesen) - Fehlerzaehler Schnittstelle Crashsensoren lesen UDS : $22 ReadDataByIdentifier UDS : $D475 FEHLERZAEHLER_SAT_LESEN Modus: Default (0xD475)
- [STATUS_SEATBELTMIND](#job-status-seatbeltmind) - Status Seatbeltreminder lesen UDS : $22 ReadDataByIdentifier UDS : $D477 SEATBELTMIND Modus: Default (0xD477)
- [STATUS_SG_TEMP](#job-status-sg-temp) - Innentemperatur Steuergerät lesen UDS : $22 ReadDataByIdentifier UDS : $D478 SG_TEMP Modus: Default (0xD478)
- [STEUERN_POL](#job-steuern-pol) - PassengerAirbag Off- Leuchte POL steuern/ dimmen UDS : $2E WriteDataByIdentifier UDS : $D479 POL Modus: Default (0xD479)
- [STATUS_LENKSEITE](#job-status-lenkseite) - Eincodierte Lenkseite auslesen UDS : $22 ReadDataByIdentifier UDS : $D47A LENKSEITE Modus: Default (0xD47A)
- [STEUERN_TEST_RO_MAGN](#job-steuern-test-ro-magn) - Testausloesung magnetische Rolloveraktuatoren UDS : $2E WriteDataByIdentifier UDS : $D47B STEUERN_RO_MAGN Ausloesung magnetischer Rolloverbuegel (0xD47B)
- [STATUS_BAUREIHE](#job-status-baureihe) - Baureihe auslesen UDS : $22 ReadDataByIdentifier UDS : $D47E BAUREIHE Modus: Default (0xD47E)
- [STATUS_LAENDERVARIANTE](#job-status-laendervariante) - Laendervariante lesen UDS : $22 ReadDataByIdentifier UDS : $D47F LAENDERVARIANTE Modus: Default (0xD47F)
- [STATUS_AACN](#job-status-aacn) - AACN lesen UDS : $22 ReadDataByIdentifier UDS : $D480 AACN Modus: Default (0xD480)
- [STEUERN_NEAR_CRASH_DATEN_LOESCHEN](#job-steuern-near-crash-daten-loeschen) - NEAR_CRASH_DATEN Speicher loeschen UDS : $2E WriteDataByIdentifier UDS : $F020 NEAR_CRASH-DATEN_LOESCHEN Modus: Development Löscht alle Infospeichereinträge (0xF020)
- [STATUS_FAHRGESTELLNUMMER](#job-status-fahrgestellnummer) - Fahrgestellnummer lesen UDS : $22 ReadDataByIdentifier UDS $F190 FAHRGESTELLNUMMER Modus: Default (0xF190)
- [STATUS_NUMBER_OF_EDR_DEVICES_LESEN](#job-status-number-of-edr-devices-lesen) - Anzahl Crash-Recorder-Eintraege lesen UDS : $22 ReadDataByIdentifier UDS : $FA10 NUMBER_OF_EDR_DEVICES Modus: Default (0xFA10)
- [STATUS_EDR_IDENTIFICATION_LESEN](#job-status-edr-identification-lesen) - Anzahl Crash-Recorder-Eintraege lesen UDS : $22 ReadDataByIdentifier UDS : $FA11 EDR_IDENTIFICATION Modus: Default (0xFA11)
- [STATUS_EDR_ADDRESS_INFORMATION_VERSION_LESEN](#job-status-edr-address-information-version-lesen) - Anzahl Crash-Recorder-Eintraege lesen UDS : $22 ReadDataByIdentifier UDS : $FA12 EDR_ADDRESS_INFORMATION Modus: Default (0xFA12)
- [STATUS_BETRIEBSSTUNDENZAEHLER_AKTUELL](#job-status-betriebsstundenzaehler-aktuell) - Betriebsstundenzaehler aktuell lesen UDS : $22 ReadDataByIdentifier UDS : $FD21 BETRIEBSSTUNDENZAEHLER Modus: Default Steuergerätebezogene Betriebszeit (0xFD21)
- [STATUS_POWER_ON_ZAEHLER](#job-status-power-on-zaehler) - Power on Zaehler lesen UDS : $22 ReadDataByIdentifier UDS : $FD22 POWER_ON_ZAEHLER Modus: Default (0xFD22)
- [STATUS_KENNUNG_ZE_PARAMETER](#job-status-kennung-ze-parameter) - Kennung der Algorithmus-Parameter lesen UDS : $22 ReadDataByIdentifier UDS : $FD23 KENNUNG_ZE_PARAMETER Modus: Default (0xFD23)
- [STATUS_SYSTEMZEIT_LETZTES_FS_LOESCHEN](#job-status-systemzeit-letztes-fs-loeschen) - Betriebsstundenzaehler letztes FS-Loeschen lesen UDS : $22 ReadDataByIdentifier UDS : $FD24 SYSTEMZEIT_LETZTES_FS_LOESCHEN Modus: Default Steuergerätebezogene Betriebszeit (0xFD24)
- [STATUS_SYSTEMZEIT_POWER_ON](#job-status-systemzeit-power-on) - Betriebsstundenzaehler Beginn aktueller Power- on- Zyklus lesen UDS : $22 ReadDataByIdentifier UDS : $FD25 SYSTEMZEIT_POWER_ON Modus: Default Steuergerätebezogene Betriebszeit (0xFD25)
- [STATUS_SYSTEMZEIT_ZEITMASTER_POWER_ON](#job-status-systemzeit-zeitmaster-power-on) - Systemzeit Zeitmaster aktueller Power on Zyklus lesen UDS : $22 ReadDataByIdentifier UDS : $FD26 SYSTEMZEIT_ZEITMASTER_POWER_ON Modus: Default Fahrzeugbezogene Betriebszeit (0xFD26)
- [STATUS_SYSTEMZEIT_ZEITMASTER_AKTUELL](#job-status-systemzeit-zeitmaster-aktuell) - Systemzeit Zeitmaster aktuell lesen UDS : $22 ReadDataByIdentifier UDS : $FD30 SYSTEMZEIT_ZEITMASTER_AKTUELL Modus: Default Fahrzeugbezogene Betriebszeit (0xFD30)
- [STATUS_SYSTEMZEIT_ZEITMASTER_LETZTES_FS_LOESCHEN](#job-status-systemzeit-zeitmaster-letztes-fs-loeschen) - Systemzeit Zeitmaster beim letzen FS-Loeschen UDS : $22 ReadDataByIdentifier UDS : $FD31 SYSTEMZEIT_ZEITMASTER_LETZTES_FS_LOESCHEN Modus: Default Fahrzeugbezogene Betriebszeit (0xFD31)
- [STATUS_ZEITSTEMPEL_POWER_ON](#job-status-zeitstempel-power-on) - Zeitstempel zum Zeitpunkt des aktuellen Power-On auslesen (Tag/ Monat/ Jahr) UDS : $22 ReadDataByIdentifier UDS : $FD32 ZEITSTEMPEL_POWER_ON Modus: Default (0xFD32)
- [STATUS_ZEITSTEMPEL_AKTUELL](#job-status-zeitstempel-aktuell) - Zeitstempel aktuell lesen (Tag/ Monat/ Jahr) UDS : $22 ReadDataByIdentifier UDS : $FD33 ZEITSTEMPEL_AKTUELL Modus: Default (0xFD33)
- [STATUS_ZEITSTEMPEL_LETZTES_FS_LOESCHEN](#job-status-zeitstempel-letztes-fs-loeschen) - Zeitstempel zum Zeitpunkt des letzten Fehlerspeicher-Loeschens auslesen (Tag/ Monat/ Jahr) UDS : $22 ReadDataByIdentifier UDS : $FD34 ZEITSTEMPEL_LETZTES_FS_LOESCHEN Modus: Default (0xFD34)
- [STATUS_LETZTE_SYSTEMZEIT_AKTIV](#job-status-letzte-systemzeit-aktiv) - Systemzeit Zeitmaster, Ende letzter Klemmenzyklus, lesen UDS : $22 ReadDataByIdentifier UDS : $FD35 LETZTE_SYSTEMZEIT_AKTIV Modus: Default (0xFD35)
- [STATUS_BMW_SACHNUMMER](#job-status-bmw-sachnummer) - Lesen BMW Sachnummer UDS : $22 ReadDataByIdentifier UDS : $FD50 BMW_SACHNUMMER Modus: Default (0xFD50)
- [TESTAUSL_ROLL_MAGN](#job-testausl-roll-magn) - UDS   : $2E   RoutineControl UDS   : $40   Testauslösung vorbereiten UDS   : $81   Testauslösung vorbereiten UDS   : $2E   RoutineControl UDS   : $D4   Testauslösung durchführen UDS   : $7B   Testauslösung durchführen
- [_STEUERN_NOTRUF](#job-steuern-notruf) - Steuern Notruf Steuern Notruf UDS : $2E WriteDataByIdentifier UDS : $D47C Steuern_Notruf Wird verwendet zur Telefonabsicherung bei EI-4.

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
| IGNORIERE_EREIGNIS_DTC | string | 'IGNORIERE_EREIGNIS_DTC': Alle Ereignis DTC-Fehlereinträge werden ignoriert sonst: alle Fehlereinträge werden ausgegeben |

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

<a id="job-caf-logistikdaten-lesen"></a>
### CAF_LOGISTIKDATEN_LESEN

CAF Logistikdaten lesen (CAF1 ? CAF3) UDS : $22 ReadDataByIdentifier UDS : $3003 CAF_LOGISTIKDATEN_LESEN (CAF1) UDS : $30FB CAF_LOGISTIKDATEN_LESEN (CAF2) UDS : $311B CAF_LOGISTIKDATEN_LESEN (CAF3) Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CAF_NR | string | CAF_NR Werttabelle 12291 = CAF1 12539 = CAF2 12571 = CAF3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| H_NR | string | Haendlernummer |
| H_NR_EINH | string | "HEX" |
| C_DATUM | unsigned long | Codierdatum |
| BR | string | Baureihe |
| BR_EINH | string | "HEX" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

Codierdaten blockweise lesen (CAF1 ? CAF3) UDS : $22 ReadDataByIdentifier UDS : $3000 ? $311D RDBI_CD Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DID | string | DataIdentifier Werttabelle Zugelassene Werte siehe Tabelle T_CD_DOP |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RDBI_DREC | binary | dataRecord |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-debug-info-lesen"></a>
### STATUS_DEBUG_INFO_LESEN

DTC Debug Info lesen UDS : $22 ReadDataByIdentifier UDS : $4061 DEBUG_INFO_LESEN1 UDS : $4062 DEBUG_INFO_LESEN2 UDS : $4063 DEBUG_INFO_LESEN3 Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ID_DTC_DEBUG_INFO_LESEN | string | ID DTC_DEBUG_INFO_LESEN Werttabelle 16481 = 1 16482 = 2 16483 = 3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AKTUELLER_QUALIFIKATIONSZAEHLER_WERT | unsigned char | Aktueller Qualifikationszaehler |
| STAT_MAXIMALER_QUALIFIKATIONSZAEHLER_WERT | unsigned char | Maximaler Qualifikationszaehler |
| STAT_ANZAHL_TESTS_MIT_FEHLER_WERT | unsigned char | Anzahl Tests mit Fehler |
| STAT_ADRESSINHALT1_WERT | string | Adressinhalt1 |
| STAT_ADRESSINHALT1_EINH | string | "HEX" |
| STAT_ADRESSINHALT2_WERT | string | Adressinhalt2 |
| STAT_ADRESSINHALT2_EINH | string | "HEX" |
| STAT_UNGUELTIGKEIT1_WERT | unsigned char | Gueltigkeitsprüfung Adressinhalt1 |
| STAT_UNGUELTIGKEIT2_WERT | unsigned char | Gueltigkeitsprüfung Adressinhalt2 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-edr-public-data-lesen"></a>
### STATUS_EDR_PUBLIC_DATA_LESEN

EDR-PUBLIC-DATA lesen UDS : $22 ReadDataByIdentifier UDS : $FA13 EDR-PUBLIC-DATA_LESEN1 UDS : $FA14 EDR-PUBLIC-DATA_LESEN2 UDS : $FA15 EDR-PUBLIC-DATA_LESEN3 UDS : $FA16 EDR-PUBLIC-DATA_LESEN4 UDS : $FA17 EDR-PUBLIC-DATA_LESEN5 Modus: Development

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ID_EDR_PUBLIC_DATA_LESEN | string | ID_EDR_PUBLIC_DATA_LESEN Werttabelle 64019 = 1 64020 = 2 64021 = 3 64022 = 4 64023 = 5 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_UINT8_HEX_WERT | string | 1 Byte |
| STAT_UINT8_HEX_EINH | string | "HEX" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-diagnoseart-aendern"></a>
### STEUERN_DIAGNOSEART_AENDERN

Diagnoseart aendern UDS : $3101 RoutineControl UDS : $F200 DIAGNOSEART_AENDERN_BMW_DIAG UDS : $F201 DIAGNOSEART_AENDERN_SUPPL_DIAG Modus: Development

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SPRMIB | unsigned char | SuppressPositiveResponseMessageIndicationBit Werttabelle 0 = false 1 = true |
| RID | string | RID Werttabelle 61952 = BMW_DIAG 61953 = SUPPL_DIAG |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-dtc-debug-info-loeschen"></a>
### STEUERN_DTC_DEBUG_INFO_LOESCHEN

DTC Debug Info loeschen UDS : $3101 RoutineControl UDS : $F011 DEBUG_INFO_LOESCHEN1 UDS : $F012 DEBUG_INFO_LOESCHEN2 UDS : $F013 DEBUG_INFO_LOESCHEN3 Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SPRMIB | unsigned char | SuppressPositiveResponseMessageIndicationBit Werttabelle 0 = false 1 = true |
| RID | string | RID Werttabelle 61457 = 1 61458 = 2 61459 = 3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-near-crash-daten-lesen"></a>
### _STATUS_NEAR_CRASH_DATEN_LESEN

NEAR_CRASH-Daten lesen UDS : $22 ReadDataByIdentifier UDS : $4023 NEAR_CRASH_DATEN_LESEN1 UDS : $4024 NEAR_CRASH_DATEN_LESEN2 Modus: Development Dies ist kein NHTSA-EDR, sondern ein Near-Crash-Recoder

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ID_NEAR_CRASH_DATEN_LESEN | string | ID NEAR_CRASH_DATEN_LESEN Werttabelle 16419 = 1 16420 = 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_UINT8_HEX_WERT | string | 1 Byte |
| STAT_UINT8_HEX_EINH | string | "HEX" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-batteriespannung-am-sg"></a>
### STATUS_BATTERIESPANNUNG_AM_SG

Batteriespannung am Steuergeraet lesen UDS : $22 ReadDataByIdentifier UDS : $4006 BATTERIESPANNUNG_AM_SG Modus: Default (0x4006)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIESPANNUNG_AM_SG | unsigned char | BATTERIESPANNUNG_AM_SG_LESEN |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-fehlerzaehler-primaer"></a>
### STATUS_FEHLERZAEHLER_PRIMAER

Anzahl Eintraege Primaerer Fehlerspeicher lesen UDS : $22 ReadDataByIdentifier UDS : $4015 FEHLERZAEHLER_PRIMAER Modus: Default (0x4015)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PRIMAER_FEHLERZAEHLER | unsigned char | PRIMAER_FEHLERZAEHLER auslesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-fehlerzaehler-sekundaer"></a>
### STATUS_FEHLERZAEHLER_SEKUNDAER

Anzahl Eintraege Sekundaerer Fehlerspeicher lesen UDS : $22 ReadDataByIdentifier UDS : $4016 FEHLERZAEHLER_SEKUNDAER Modus: Default (0x4016)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SEKUNDAER_FEHLERZAEHLER | unsigned char | SEKUNDAER_FEHLERZAEHLER auslesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-verriegelung-lesen"></a>
### STATUS_VERRIEGELUNG_LESEN

Status Verriegelung lesen UDS : $22 ReadDataByIdentifier UDS : $4080 VERRIEGELUNG_LESEN Modus: Default (0x4080)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VERRIEGELUNG_LESEN_01_WERT | unsigned char | Alle drei Results: 0: verriegelt, sonst nicht verriegelt |
| STAT_VERRIEGELUNG_LESEN_02_WERT | unsigned char | Alle drei Results: 0: verriegelt, sonst nicht verriegelt |
| STAT_VERRIEGELUNG_LESEN_03_WERT | unsigned char | Alle drei Results: 0: verriegelt, sonst nicht verriegelt |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-verriegelung-schreiben"></a>
### STEUERN_VERRIEGELUNG_SCHREIBEN

Verriegelung schreiben UDS : $2E WriteDataByIdentifier UDS : $4080 VERRIEGELUNG_SCHREIBEN Modus: Default (0x4080)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| UEBERGABEPARAMETER | unsigned long | 00 00 00 = verriegeln |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-sbe-daten"></a>
### SBE_DATEN

Daten Sitzmatten lesen UDS : $22 ReadDataByIdentifier UDS : $4085 SBE_DATEN Modus: Default (0x4085)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BMW_TEILENUMMER_MATTE_FA | string | BMW-Teilenummer Matte Fahrer |
| STAT_BMW_TEILENUMMER_MATTE_FA_EINH | string | "HEX" |
| STAT_BMW_TEILENUMMER_MATTE_BF | string | BMW-Teilenummer Matte Beifahrer |
| STAT_BMW_TEILENUMMER_MATTE_BF_EINH | string | "HEX" |
| STAT_BMW_TEILENUMMER_MATTE_HL | string | BMW-Teilenummer Matte hinten links |
| STAT_BMW_TEILENUMMER_MATTE_HL_EINH | string | "HEX" |
| STAT_BMW_TEILENUMMER_MATTE_HR | string | BMW-Teilenummer Matte hinten rechts |
| STAT_BMW_TEILENUMMER_MATTE_HR_EINH | string | "HEX" |
| STAT_BMW_SERIENNUMMER_MATTE_FA | string | BMW-Seriennummer Matte Fahrer |
| STAT_BMW_SERIENNUMMER_MATTE_FA_EINH | string | "HEX" |
| STAT_BMW_SERIENNUMMER_MATTE_BF | string | BMW-Seriennummer Matte Beifahrer |
| STAT_BMW_SERIENNUMMER_MATTE_BF_EINH | string | "HEX" |
| STAT_BMW_SERIENNUMMER_MATTE_HL | string | BMW-Seriennummer Matte hinten links |
| STAT_BMW_SERIENNUMMER_MATTE_HL_EINH | string | "HEX" |
| STAT_BMW_SERIENNUMMER_MATTE_HR | string | BMW-Seriennummer Matte hinten rechts |
| STAT_BMW_SERIENNUMMER_MATTE_HR_EINH | string | "HEX" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-ausstattung"></a>
### STATUS_AUSSTATTUNG

Ausstattung lesen (CAF1) UDS : $22 ReadDataByIdentifier UDS : $4070 AUSSTATTUNG Modus: Default (0xD470)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AB1_FA_KODIERT | unsigned char | FIX_ZK: Airbag Fahrer Stufe 1 Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_AB2_FA_KODIERT | unsigned char | VAR_ZK: Airbag Fahrer Stufe 2 Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_AB_FA_VENTIL_KODIERT | unsigned char | VAR_ZK: Adaptiver Airbag Fahrer Ventil Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_AB1_BF_KODIERT | unsigned char | FIX_ZK: Airbag Beifahrer Stufe 1 Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_AB2_BF_KODIERT | unsigned char | VAR_ZK: Airbag Beifahrer Stufe 2 Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_AB_BF_VENTIL_KODIERT | unsigned char | VAR_ZK: Adaptiver Airbag Beifahrer Ventil Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_GS_FA_KODIERT | unsigned char | FIX_ZK: Gurtstrammer Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_EBS_FA_KODIERT | unsigned char | VAR_ZK: Endbeschlagstrammer Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_GKB_FA_KODIERT | unsigned char | VAR_ ZK: Adaptiver Gurt-Kraftbegrenzer Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_GS_BF_KODIERT | unsigned char | FIX_ZK: Gurtstrammer Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_EBS_BF_KODIERT | unsigned char | VAR_ZK: Endbeschlagstrammer Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_GKB_BF_KODIERT | unsigned char | VAR_ZK: Adaptiver Gurt-Kraftbegrenzer Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_KNIE_AB_FA_KODIERT | unsigned char | VAR_ZK: Knieairbag Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_KNIE_AB_BF_KODIERT | unsigned char | VAR_ZK: Knieairbag Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_KOS_FA_KODIERT | unsigned char | VAR_ZK: Aktive Kopfstuetze Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_KOS_BF_KODIERT | unsigned char | VAR_ZK: Aktive Kopfstuetze Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_GS_HLI_KODIERT | unsigned char | VAR_ZK: Gurtstrammer hinten links Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_GS_HRE_KODIERT | unsigned char | VAR_ZK: Gurtstrammer hinten rechts Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_ARS_FA_KODIERT | unsigned char | VAR_ZK: Aufrollstrammer Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_ARS_BF_KODIERT | unsigned char | VAR_ZK: Aufrollstrammer Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SEITEN_AB_FA_KODIERT | unsigned char | FIX_ZK: Sitzairbag Thorax Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SEITEN_AB_BF_KODIERT | unsigned char | FIX_ZK: Sitzairbag Thorax Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SEITEN_AB_FA_VENTIL_KODIERT | unsigned char | VAR_ZK: Adaptives Sitzairbagventil Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SEITEN_AB_BF_VENTIL_KODIERT | unsigned char | VAR_ZK: Adaptives Sitzairbagventil Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_KOPF_AB_LI_KODIERT | unsigned char | VAR_ZK: Kopfairbag (Curtain) links Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_KOPF_AB_RE_KODIERT | unsigned char | VAR_ZK: Kopfairbag (Curtain) rechts Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SBK1_KODIERT | unsigned char | FIX_ZK: Sicherheitsbatterieklemme 1 Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SBK2_KODIERT | unsigned char | VAR_ZK: Sicherheitsbatterieklemme 2 Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_RO_SCHUTZ_LI_KODIERT | unsigned char | VAR_ZK: Rollover- Schutz links Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_RO_SCHUTZ_RE_KODIERT | unsigned char | VAR_ZK: Rollover- Schutz rechts Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_RO_SCHUTZ_MAGN_LI_KODIERT | unsigned char | VAR_ZK: Rollover- Schutz magnetisch links Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_RO_SCHUTZ_MAGN_RE_KODIERT | unsigned char | VAR_ZK: Rollover- Schutz magnetisch rechts Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_FGS_VLI_KODIERT | unsigned char | VAR_ZK: Fussgaengerschutzsystem vorn links Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_FGS_VRE_KODIERT | unsigned char | VAR_ZK: Fussgaengerschutzsystem vorn rechts Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_FGS_HLI_KODIERT | unsigned char | VAR_ZK: Fussgaengerschutzsystem hinten links Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_FGS_HRE_KODIERT | unsigned char | VAR_ZK: Fussgaengerschutzsystem hinten rechts Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SBK3_KODIERT | unsigned char | VAR_ZK: Sicherheitsbatterieklemme 3 Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_PPA_KODIERT | unsigned char | VAR_ZK: PPA Windowbag Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_FGS_PPA_RHM_KODIERT | unsigned char | VAR_ZK: FGS_PPA_RHM Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE6_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE7_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE8_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE9_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE10_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE11_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE12_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE13_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE14_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE15_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE16_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE17_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE18_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE19_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE20_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE21_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE22_ZK_KODIERT | unsigned char | VAR_ZK: Reserve Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SENSOR_UPFRONT_KODIERT | unsigned char | UpFront Sensoren links und rechts Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE1_SENSOR_KODIERT | unsigned char | Reserve1_Sensor Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE1A_SENSOR_KODIERT | unsigned char | Reserve1A_Sensor Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SENSOR_TUER_KODIERT | unsigned char | Tuer Satelliten links und rechts Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SENSOR_CSAEULE_KODIERT | unsigned char | C-Saeulen Satelliten links und rechts Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SENSOR_FGS_PTS_KODIERT | unsigned char | Fussgängerschutzsensor Pressure Tube System Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SENSOR_FGS_ARMING_KODIERT | unsigned char | Fussgaengerschutz-Sensor Arming Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SENSOR_FGS_SB_KODIERT | unsigned char | Fussgaengerschutz-Sensor Sensorband Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SENSOR_ZENTRAL_KODIERT | unsigned char | Zentralsensor Airbag/ ICM Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SENSOR_ROSE_KODIERT | unsigned char | Sensor mit Rollover Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SENSOR_ZENTRAL_2SLOTS_KODIERT | unsigned char | Zentralsensor Datentransfer mit 2 PSI5- Slots Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE4_SENSOR_KODIERT | unsigned char | Reserve4_Sensor Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE3A_SENSOR_KODIERT | unsigned char | Reserve3a_Sensor Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE4A_SENSOR_KODIERT | unsigned char | Reserve4a_Sensor Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE5_SENSOR_KODIERT | unsigned char | Reserve5_Sensor Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SENSOR_ZENTRAL_SCHALL_KODIERT | unsigned char | Zentralsensor mit Körperschallsensorik Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_GK_FA_KODIERT | unsigned char | Gurtkontakt Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_GK_BF_KODIERT | unsigned char | Gurtkontakt Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_GK_HLI_KODIERT | unsigned char | Gurtkontakt hinten links Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_GK_HRE_KODIERT | unsigned char | Gurtkontakt hinten rechts Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_GK_HMI_KODIERT | unsigned char | Gurtkontakt hinten Mitte Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SITZ_POS_FA_KODIERT | unsigned char | Sitzpositionssensor Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SITZ_POS_MEM_FA_KODIERT | unsigned char | Sitzpositionserkennung Sitzmemory Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE6_SENSOR_KODIERT | unsigned char | Reserve6_Sensor Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE7_SENSOR_KODIERT | unsigned char | Reserve7_Sensor Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SITZ_POS_BF_KODIERT | unsigned char | Sitzpositionssensor Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SITZ_POS_MEM_BF_KODIERT | unsigned char | Sitzpositionserkennung Sitzmemory Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SBR_MATTE_BF_KODIERT | unsigned char | Seatbelt-Reminder Sensor Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SBR_MATTE_BF_R_KODIERT | unsigned char | Seatbelt-Reminder Sensor Beifahrer widerstandscodiert Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE8_SENSOR_KODIERT | unsigned char | Reserve8_Sensor Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_CIS_MATTE_BF_KODIERT | unsigned char | Capacity Interior Sensing Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE9_SENSOR_KODIERT | unsigned char | Reserve9_Sensor Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE10_SENSOR_KODIERT | unsigned char | Reserve10_Sensor Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE11_SENSOR_KODIERT | unsigned char | Reserve11_Sensor Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE12_SENSOR_KODIERT | unsigned char | Reserve12_Sensor Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE1_FUNKTION_KODIERT | unsigned char | Reserve1_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE2_FUNKTION_KODIERT | unsigned char | Reserve2_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE3_FUNKTION_KODIERT | unsigned char | Reserve3_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE4_FUNKTION_KODIERT | unsigned char | Reserve4_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE5_FUNKTION_KODIERT | unsigned char | Reserve5_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE6_FUNKTION_KODIERT | unsigned char | Reserve6_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_PASSENGER_AIRBAG_OFF_LIGHT_HW_KODIERT | unsigned char | Passenger Airbag Off Light Hardware Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_PASSENGER_AIRBAG_OFF_LIGHT_LOGIK_KODIERT | unsigned char | Passenger Airbag Off Light Logik Alt/Neu Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE7_FUNKTION_KODIERT | unsigned char | Reserve7_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE8_FUNKTION_KODIERT | unsigned char | Reserve8_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE9_FUNKTION_KODIERT | unsigned char | Reserve9_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE10_FUNKTION_KODIERT | unsigned char | Reserve10_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE11_FUNKTION_KODIERT | unsigned char | Reserve11_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SLV_FA_KODIERT | unsigned char | Sitzlehnenverriegelung Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SLV_BF_KODIERT | unsigned char | Sitzlehnenverriegelung Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE12_FUNKTION_KODIERT | unsigned char | Reserve12_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SICHERHEITSFZG_KODIERT | unsigned char | Sicherheitsfahrzeug Ueberfallfunktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE13_FUNKTION_KODIERT | unsigned char | Reserve13_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_EDR_NHTSA_KODIERT | unsigned char | EDR NHTSA Event-Data-Recorder fuer NHTSA-Standard Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_TROMMEL_OFF_KODIERT | unsigned char | Trommelspeicher schreiben deaktivieren 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE15_FUNKTION_KODIERT | unsigned char | Reserve15_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE16_FUNKTION_KODIERT | unsigned char | Reserve16_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE17_FUNKTION_KODIERT | unsigned char | Reserve17_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE18_FUNKTION_KODIERT | unsigned char | Reserve18_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE19_FUNKTION_KODIERT | unsigned char | Reserve19_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE20_FUNKTION_KODIERT | unsigned char | Reserve20_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE21_FUNKTION_KODIERT | unsigned char | Reserve21_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE22_FUNKTION_KODIERT | unsigned char | Reserve22_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE23_FUNKTION_KODIERT | unsigned char | Reserve23_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_INITIAL_GURTWARNUNG_FA_KODIERT | unsigned char | Initial Gurtwarnung fuer Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SBR_FA_FUNKTION_KODIERT | unsigned char | Seatbelt-Reminder Funktion Fahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SBR_BF_FUNKTION_KODIERT | unsigned char | Seatbelt-Reminder Funktion Beifahrer Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE20A_FUNKTION_KODIERT | unsigned char | Reserve20a_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE21A_FUNKTION_KODIERT | unsigned char | Reserve21a_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE22A_FUNKTION_KODIERT | unsigned char | Reserve22a_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE23A_FUNKTION_KODIERT | unsigned char | Reserve23a_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE23B_FUNKTION_KODIERT | unsigned char | Reserve23b_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SBR_PREWARNING_FA_KODIERT | unsigned char | SBR PreWarning (SPW) Fahrer, Wird sich während der Fahrt abgegurtet, ertönt einmal ein Gong, falls es kodiert ist. Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_SBR_PREWARNING_BF_KODIERT | unsigned char | SBR PreWarning (SPW) Beifahrer, Wird sich während der Fahrt abgegurtet, ertönt einmal ein Gong, falls es kodiert ist. Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE24_FUNKTION_KODIERT | unsigned char | Reserve24_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE25_FUNKTION_KODIERT | unsigned char | Reserve25_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE26_FUNKTION_KODIERT | unsigned char | Reserve26_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE27_FUNKTION_KODIERT | unsigned char | Reserve27_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE28_FUNKTION_KODIERT | unsigned char | Reserve28_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE29_FUNKTION_KODIERT | unsigned char | Reserve29_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_PASSENGER_AIRBAG_OFF_SWITCH_KODIERT | unsigned char | Passenger Airbag Off Schalter Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_INFO_MOTORSTART_KODIERT | unsigned char | Ergaenzungsinformation beim Motorstart Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE30_FUNKTION_KODIERT | unsigned char | Reserve30_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE31_FUNKTION_KODIERT | unsigned char | Reserve31_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_PWM_LEITUNG_FPC_ABSCHALTUNG_KODIERT | unsigned char | Aktivierung der PWM-Leitung für die Crashabschaltung der FPC (Fuel Pump Controller) Eincodiert 0 = nicht kodiert 1 = kodiert |
| STAT_ABSCHALTEN_FEHLERLQUALI_DTC_PLAUSI_CHECK_DYN_DATEN_KODIERT | unsigned char | Fehlerqualifikation für FGS-Plausibilitätsprüfung dynamische Daten (DTC) Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE34_FUNKTION_KODIERT | unsigned char | Reserve34_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| _STAT_RESERVE35_FUNKTION_KODIERT | unsigned char | Reserve35_Funktion Eincodiert 0 = nicht kodiert 1 = kodiert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-lesen-airbag"></a>
### STATUS_LESEN_AIRBAG

IO Bytes des Steuergeraets UDS : $22 ReadDataByIdentifier UDS : $D471 LESEN_AIRBAG Modus: Default (0xD471)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AB1_FA_OKAY | unsigned char | FIX_ZK: Airbag Fahrer Stufe 1 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_AB2_FA_OKAY | unsigned char | VAR_ZK: Airbag Fahrer Stufe 2 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_AB_FA_VENTIL_OKAY | unsigned char | VAR_ZK: Adaptiver Airbag Fahrer Ventil 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_AB1_BF_OKAY | unsigned char | FIX_ZK: Airbag Beifahrer Stufe 1 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_AB2_BF_OKAY | unsigned char | VAR_ZK: Airbag Beifahrer Stufe 2 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_AB_BF_VENTIL_OKAY | unsigned char | VAR_ZK: Adaptiver Airbag Beifahrer Ventil 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_GS_FA_OKAY | unsigned char | FIX_ZK: Gurtstrammer Fahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_EBS_FA_OKAY | unsigned char | VAR_ZK: Endbeschlagstrammer Fahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_GKB_FA_OKAY | unsigned char | VAR_ ZK: Adaptiver Gurt-Kraftbegrenzer Fahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_GS_BF_OKAY | unsigned char | FIX_ZK: Gurtstrammer Beifahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_EBS_BF_OKAY | unsigned char | VAR_ZK: Endbeschlagstrammer Beifahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_GKB_BF_OKAY | unsigned char | VAR_ZK: Adaptiver Gurt-Kraftbegrenzer Beifahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_KNIE_AB_FA_OKAY | unsigned char | VAR_ZK: Knieairbag Fahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_KNIE_AB_BF_OKAY | unsigned char | VAR_ZK: Knieairbag Beifahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_KOS_FA_OKAY | unsigned char | VAR_ZK: Aktive Kopfstuetze Fahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_KOS_BF_OKAY | unsigned char | VAR_ZK: Aktive Kopfstuetze Beifahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_GS_HLI_OKAY | unsigned char | VAR_ZK: Gurtstrammer hinten links 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_GS_HRE_OKAY | unsigned char | VAR_ZK: Gurtstrammer hinten rechts 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ARS_FA_OKAY | unsigned char | VAR_ZK: Aufrollstrammer Fahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_ARS_BF_OKAY | unsigned char | VAR_ZK: Aufrollstrammer Beifahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_SEITEN_AB_FA_OKAY | unsigned char | FIX_ZK: Sitzairbag Thorax Fahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_SEITEN_AB_BF_OKAY | unsigned char | FIX_ZK: Sitzairbag Thorax Beifahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_SEITEN_AB_FA_VENTIL_OKAY | unsigned char | VAR_ZK: Adaptives Sitzairbagventil Fahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_SEITEN_AB_BF_VENTIL_OKAY | unsigned char | VAR_ZK: Adaptives Sitzairbagventil Beifahrer 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_KOPF_AB_LI_OKAY | unsigned char | VAR_ZK: Kopfairbag (Curtain) links 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_KOPF_AB_RE_OKAY | unsigned char | VAR_ZK: Kopfairbag (Curtain) rechts 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_SBK1_OKAY | unsigned char | FIX_ZK: Sicherheitsbatterieklemme 1 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_SBK2_OKAY | unsigned char | VAR_ZK: Sicherheitsbatterieklemme 2 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_RO_SCHUTZ_LI_OKAY | unsigned char | VAR_ZK: Rollover-Schutz links 0 = n.i.O. (externer Fehler), 1 = i.O. ACSM4-B: Rollover-Schutz magnetisch oder pyrotechnisch ACSM4-C: nur pyrotechnisch |
| STAT_RO_SCHUTZ_RE_OKAY | unsigned char | VAR_ZK: Rollover-Schutz rechts 0 = n.i.O. (externer Fehler), 1 = i.O. ACSM4-B: Rollover-Schutz magnetisch oder pyrotechnisch ACSM4-C: nur pyrotechnisch |
| STAT_RO_SCHUTZ_LI_MAGN_OKAY | unsigned char | VAR_ZK: Rollover-Schutz rechts magnetisch (nur ACSM4-C) 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_RO_SCHUTZ_RE_MAGN_OKAY | unsigned char | VAR_ZK: Rollover-Schutz rechts magnetisch (nur ACSM4-C) 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_FGS_VLI_OKAY | unsigned char | VAR_ZK: Fussgaengerschutzsystem vorn links 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_FGS_VRE_OKAY | unsigned char | VAR_ZK: Fussgaengerschutzsystem vorn rechts 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_FGS_HLI_OKAY | unsigned char | VAR_ZK: Fussgaengerschutzsystem hinten links 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_FGS_HRE_OKAY | unsigned char | VAR_ZK: Fussgaengerschutzsystem hinten rechts 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_SBK3_OKAY | unsigned char | VAR_ZK: Sicherheitsbatterieklemme 3 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_PPA_OKAY | unsigned char | VAR_ZK: PPA Windowbag 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_FGS_PPA_RHM_OKAY | unsigned char | VAR_ZK: FGS_PPA_RHM 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE6_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE7_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE8_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE9_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE10_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE11_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE12_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE13_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE14_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE15_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE16_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE17_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE18_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE19_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE20_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE21_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| _STAT_RESERVE22_ZK_OKAY | unsigned char | VAR_ZK: Reserve 0 = n.i.O. (externer Fehler), 1 = i.O. |
| STAT_GK_FA_ZUSTAND | unsigned char | Gurtkontakt Fahrer 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GK_FA_FEHLER | unsigned char | Gurtkontakt Fahrer 0 = kein Fehler, 1 = Fehler |
| STAT_GK_FA_PLAUSIBILITAET | unsigned char | Gurtkontakt Fahrer 0 = i.O., 1 = n.i.O. (Plausibilitätsfehler) |
| STAT_GK_BF_ZUSTAND | unsigned char | Gurtkontakt Beifahrer 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GK_BF_FEHLER | unsigned char | Gurtkontakt Beifahrer 0 = kein Fehler, 1 = Fehler |
| STAT_GK_BF_PLAUSIBILITAET | unsigned char | Gurtkontakt Beifahrer 0 = i.O., 1 = n. i.O. (Plausibilitätsfehler) |
| _STAT_RESERVE1_SENSOR_OKAY | unsigned char | Reserve1_Sensor |
| _STAT_RESERVE2_SENSOR_OKAY | unsigned char | Reserve2_Sensor |
| STAT_GK_HLI_ZUSTAND | unsigned char | Gurtkontakt hinten links 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GK_HLI_FEHLER | unsigned char | Gurtkontakt hinten links 0 = kein Fehler, 1 = Fehler |
| STAT_GK_HLI_PLAUSIBILITAET | unsigned char | Gurtkontakt hinten links 0 = i.O. , 1 = n. i.O. (Plausibilitätsfehler) |
| STAT_GK_HRE_ZUSTAND | unsigned char | Gurtkontakt hinten rechts 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GK_HRE_FEHLER | unsigned char | Gurtkontakt hinten rechts 0 = kein Fehler, 1 = Fehler |
| STAT_GK_HRE_PLAUSIBILITAET | unsigned char | Gurtkontakt hinten rechts 0 = i.O., 1 = n. i.O. (Plausibilitätsfehler) |
| _STAT_RESERVE3_SENSOR_OKAY | unsigned char | Reserve3_Sensor |
| _STAT_RESERVE4_SENSOR_OKAY | unsigned char | Reserve4_Sensor |
| STAT_GK_HMI_ZUSTAND | unsigned char | Gurtkontakt hinten mitte 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GK_HMI_FEHLER | unsigned char | Gurtkontakt hinten mitte 0 = kein Fehler, 1 = Fehler |
| STAT_GK_HMI_PLAUSIBILITAET | unsigned char | Gurtkontakt hinten mitte 0 = i.O., 1 = n. i.O. (Plausibilitätsfehler) |
| _STAT_RESERVE5_SENSOR_OKAY | unsigned char | Reserve5_Sensor |
| _STAT_RESERVE6_SENSOR_OKAY | unsigned char | Reserve6_Sensor |
| _STAT_RESERVE7_SENSOR_OKAY | unsigned char | Reserve7_Sensor |
| _STAT_RESERVE8_SENSOR_OKAY | unsigned char | Reserve8_Sensor |
| _STAT_RESERVE9_SENSOR_OKAY | unsigned char | Reserve9_Sensor |
| STAT_PASSENGER_AIRBAG_OFF_SWITCH_ZUSTAND | unsigned char | Zustand Passenger Airbag Off Schalter , 1 = nicht geschaltet = Steuergerät sendet 1 = Airbag ein = Aufdruck Schalter On (= Schalterstellung 0) 0 = geschaltet = Steuergerät sendet 0 = Airbag aus = Aufdruck Schalter Off (= Schalterstellung 1) |
| STAT_PASSENGER_AIRBAG_OFF_SWITCH_FEHLER | unsigned char | Status Fehler Passenger Airbag Off Schalter 0 = kein Fehler, 1 = Fehler |
| STAT_PASSENGER_AIRBAG_OFF_SWITCH_PLAUSIBILITAET | unsigned char | Passenger Airbag Off Schalter 0 = i.O., 1 = n. i.O. (Plausibilitätsfehler) |
| _STAT_RESERVE10_SENSOR_OKAY | unsigned char | Reserve10_Sensor |
| STAT_SITZ_POS_FA_ZUSTAND | unsigned char | Sitzpositionssensor Fahrer 0 = Sitzposition 50%-Mann, 1 = Sitzposition 5%-Frau |
| STAT_SITZ_POS_FA_FEHLER | unsigned char | Sitzpositionssensor Fahrer 0 = kein Fehler, 1 = Fehler |
| STAT_SITZ_POS_FA_PLAUSIBILITAET | unsigned char | Sitzpositionssensor Fahrer 0 = i.O., 1 = n. i.O. (Plausibilitätsfehler) |
| STAT_SITZ_POS_FA_NORMIERUNG_OKAY | unsigned char | Sitzpositionserkennung Sitzmemory Fahrer 0 = Normierungslauf notwendig, 1 = kein Normierungslauf notwendig |
| _STAT_RESERVE11_SENSOR_OKAY | unsigned char | Reserve11_Sensor |
| _STAT_RESERVE12_SENSOR_OKAY | unsigned char | Reserve12_Sensor |
| _STAT_RESERVE13_SENSOR_OKAY | unsigned char | Reserve13_Sensor |
| _STAT_RESERVE14_SENSOR_OKAY | unsigned char | Reserve14_Sensor |
| STAT_SITZ_POS_BF_ZUSTAND | unsigned char | Status Zustand Sitzpositionssensor Beifahrer 0 = Sitzposition 50%-Mann, 1 = Sitzposition 5%-Frau |
| STAT_SITZ_POS_BF_FEHLER | unsigned char | Status Fehler Sitzpositionssensor Beifahrer 0 = kein Fehler, 1 = Fehler, |
| STAT_SITZ_POS_BF_PLAUSIBILITAET | unsigned char | Status Plausibilität Sitzpositionssensor Beifahrer 0 = i.O., 1 = n. i.O. (Plausibilitätsfehler) |
| STAT_SITZ_POS_BF_NORMIERUNG_OKAY | unsigned char | Normierung Sitzpositionssensor Beifahrer 0 = Normierungslauf notwendig, 1 = kein Normierungslauf notwendig |
| STAT_SBR_MATTE_BF_VERBAUT | unsigned char | SBR-Matte Beifahrer Sitzbelegung 0 = System nicht verbaut, 1 = System verbaut |
| STAT_SBR_MATTE_BF_PLAUSIBILITAET | unsigned char | SBR-Matte Beifahrer Sitzbelegung angeschlossen, aber nicht Eincodiert (Plausifehler) 0 = i.O., 1 = n. i.O. (Plausibilitätsfehler) |
| STAT_SBR_MATTE_BF_R_VERBAUT | unsigned char | SBR-Matte Beifahrer widerstandscodiert Sitzbelegung 0 = System nicht verbaut, 1 = System verbaut |
| STAT_SBR_MATTE_BF_R_PLAUSIBILITAET | unsigned char | SBR-Matte Beifahrer widerstandscodiert Sitzbelegung angeschlossen, aber nicht Eincodiert (Plausifehler) 0 = i.O. , 1 = n. i.O.(Plausibilitätsfehler) |
| STAT_CIS_MATTE_BF_VERBAUT | unsigned char | CIS-Matte Beifahrer Sitzbelegung 0 = System nicht verbaut, 1 = System verbaut |
| STAT_CIS_MATTE_BF_PLAUSIBILITAET | unsigned char | CIS-Matte Beifahrer Sitzbelegung angeschlossen, aber nicht Eincodiert (Plausifehler) 0 = i.O. , 1 = n. i.O. (Plausibilitätsfehler) |
| _STAT_RESERVE15_SENSOR_OKAY | unsigned char | Reserve15_Sensor |
| _STAT_RESERVE16_SENSOR_OKAY | unsigned char | Reserve16_Sensor |
| STAT_SITZBELEGUNG_BF | unsigned char | Sitzbelegung Beifahrer (SBR-Sensor widerstandscodiert oder LIN ODER CIS) 0 = SBR Off (wird ausgegeben, wenn keine Person erkannt wurde), 1 = SBR On (wird ausgegeben, wenn Sitz mit einer Person belegt ist!) |
| STAT_SITZBELEGUNG_BF_UNGUELTIG | unsigned char | Sitzbelegung Beifahrer CIS 0= gueltig, 1 = ungueltig |
| STAT_SITZBELEGUNG_BF_FEHLER | unsigned char | Sitzbelegung Beifahrer (SBR-Sensor widerstandscodiert ODER CIS) 0 = kein Fehler, 1 = Fehler |
| _STAT_RESERVE17_SENSOR_OKAY | unsigned char | Reserve17_Sensor |
| STAT_GEWICHTSKLASSE_BF_UNGUELTIG | unsigned char | Gewichtsklasse Beifahrer OC3/CIS 0= gueltig, 1 = ungueltig (Fehler) |
| STAT_GEWICHTSKLASSE_BF_FEHLER | unsigned char | Gewichtsklasse Beifahrer OC3/CIS 0= i.O., 1= Fehler/ nicht verbaut |
| STAT_GEWICHTSKLASSE_BF_ZUSTAND | unsigned char | Gewichtsklasse Beifahrer OC3/CIS 0= keine Person erkannt, 1= Person erkannt |
| _STAT_RESERVE18_SENSOR_OKAY | unsigned char | Reserve18_Sensor |
| _STAT_RESERVE19_SENSOR_OKAY | unsigned char | Reserve19_Sensor |
| _STAT_RESERVE20_SENSOR_OKAY | unsigned char | Reserve20_Sensor |
| _STAT_RESERVE21_SENSOR_OKAY | unsigned char | Reserve21_Sensor |
| STAT_SENSOR_FGS_PTS_LINKS_FEHLER | unsigned char | 0 = kein Fehler, 1 = sendet Fehler |
| STAT_SENSOR_FGS_PTS_LINKS_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_FGS_PTS_LINKS_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_FGS_PTS_LINKS_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_FGS_PTS_LINKS_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| STAT_SENSOR_ZENTRAL_XY_FEHLER | unsigned char | 0 = kein Fehler, 1 = sendet Fehler |
| STAT_SENSOR_ZENTRAL_XY_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_ZENTRAL_XY_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_ZENTRAL_XY_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_ZENTRAL_XY_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| _STAT_RESERVE27_SENSOR_OKAY | unsigned char | Reserve27_Sensor |
| _STAT_RESERVE28_SENSOR_OKAY | unsigned char | Reserve28_Sensor |
| _STAT_RESERVE29_SENSOR_OKAY | unsigned char | Reserve29_Sensor |
| STAT_SENSOR_ZENTRAL_RO_FEHLER | unsigned char | 0 = kein Fehler, 1 = sendet Fehler |
| STAT_SENSOR_ZENTRAL_RO_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_ZENTRAL_RO_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_ZENTRAL_RO_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_ZENTRAL_RO_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| _STAT_RESERVE30_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE31_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE32_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_SENSOR_UPFRONT_LI_FEHLER | unsigned char | 0 = kein Fehler, 1 = sendet Fehler |
| STAT_SENSOR_UPFRONT_LI_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_UPFRONT_LI_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_UPFRONT_LI_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_UPFRONT_LI_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| _STAT_RESERVE33_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE34_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE35_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_SENSOR_UPFRONT_RE_FEHLER | unsigned char | 0 = kein Fehler, 1 = sendet Fehler |
| STAT_SENSOR_UPFRONT_RE_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_UPFRONT_RE_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_UPFRONT_RE_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_UPFRONT_RE_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| _STAT_RESERVE36_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE37_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE38_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_SENSOR_TUER_LI_FEHLER | unsigned char | 0 = kein Fehler, 1 = sendet Fehler |
| STAT_SENSOR_TUER_LI_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_TUER_LI_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_TUER_LI_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_TUER_LI_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| _STAT_RESERVE39_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE40_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE41_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_SENSOR_TUER_RE_FEHLER | unsigned char | 0 = kein Fehler, 1 = sendet Fehler |
| STAT_SENSOR_TUER_RE_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_TUER_RE_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_TUER_RE_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_TUER_RE_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| _STAT_RESERVE42_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE43_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE44_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_SENSOR_BSAEULE_LI_FEHLER | unsigned char | 0 = kein Fehler, 1 = sendet Fehler |
| STAT_SENSOR_BSAEULE_LI_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_BSAEULE_LI_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_BSAEULE_LI_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_BSAEULE_LI_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| _STAT_RESERVE45_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE46_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE47_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_SENSOR_BSAEULE_RE_FEHLER | unsigned char | 0 = kein Fehler, 1 = sendet Fehler |
| STAT_SENSOR_BSAEULE_RE_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_BSAEULE_RE_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_BSAEULE_RE_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_BSAEULE_RE_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| _STAT_RESERVE48_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE49_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE50_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_SENSOR_CSAEULE_LI_FEHLER | unsigned char | 0 = sendet Fehler, 1 = kein Fehler |
| STAT_SENSOR_CSAEULE_LI_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_CSAEULE_LI_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_CSAEULE_LI_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_CSAEULE_LI_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| _STAT_RESERVE51_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE52_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE53_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_SENSOR_CSAEULE_RE_FEHLER | unsigned char | 0 = sendet Fehler, 1 = kein Fehler |
| STAT_SENSOR_CSAEULE_RE_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_CSAEULE_RE_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_CSAEULE_RE_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_CSAEULE_RE_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| _STAT_RESERVE54_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE55_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE56_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_SENSOR_FGS_SB_FEHLER | unsigned char | 0 = sendet Fehler, 1 = kein Fehler |
| STAT_SENSOR_FGS_SB_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_FGS_SB_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_FGS_SB_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_FGS_SB_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| _STAT_RESERVE57_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE58_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE59_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_SLV_FA_VERRIEGELT | unsigned char | Sitzlehnenverriegelung Fahrer nur wenn Gurtautomat in Sitzlehne 0 = nicht verriegelt, 1 = verriegelt |
| STAT_SLV_FA_DEFEKT | unsigned char | Sitzlehnenverriegelung Fahrer nur wenn Gurtautomat in Sitzlehne 0 = nicht defekt, 1 = Meldet defekt |
| STAT_SLV_FA_UNGUELTIG | unsigned char | Sitzlehnenverriegelung Fahrer nur wenn Gurtautomat in Sitzlehne 0 = Signal OKAY, 1 = Signal ungueltig |
| _STAT_RESERVE60_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_SLV_BF_VERRIEGELT | unsigned char | Sitzlehnenverriegelung Beifahrer nur wenn Gurtautomat in Sitzlehne 0 = nicht verriegelt, 1 = verriegelt |
| STAT_SLV_BF_DEFEKT | unsigned char | Sitzlehnenverriegelung Beifahrer nur wenn Gurtautomat in Sitzlehne 0 = nicht defekt, 1 = Meldet defekt |
| STAT_SLV_BF_UNGUELTIG | unsigned char | Sitzlehnenverriegelung Beifahrer nur wenn Gurtautomat in Sitzlehne 0 = Signal OKAY, 1 = Signal ungueltig |
| _STAT_RESERVE61_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_KLEMMENZUSTAND_KL30 | unsigned char | Status Klemmenzustand via CAN 0 = nicht erkannt, 1 = Kl. 30 erkannt |
| STAT_KLEMMENZUSTAND_KLR | unsigned char | Status Klemmenzustand via CAN 0 = nicht erkannt, 1 = Kl. R erkannt |
| STAT_KLEMMENZUSTAND_KL15 | unsigned char | Status Klemmenzustand via CAN 0 = nicht erkannt, 1 = Kl.15 erkannt |
| STAT_MOTORZUSTAND | unsigned char | Status Motor via CAN 0 = Motor steht, 1 = Motor liefert Drehmoment |
| _STAT_RESERVE62_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE63_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE64_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE65_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_ENERGIEZUSTAND_NORMAL | unsigned char | Status der Energieversorgung des ACSM4 0 = Autarkie, 1 = Normalspannung |
| STAT_ENERGIEZUSTAND_UNTER_UEBER | unsigned char | Status der Energieversorgung des ACSM4 0 = Normalspannung, 1 = Unterspannung |
| STAT_ENERGIEZUSTAND_UEBERSPANNUNG | unsigned char | Status der Energieversorgung des ACSM4 0 = Normalspannung, 1 = Überspannung |
| STAT_ENERGIESPARMODE | unsigned char | Status Energiesparmode: 0 = AUS, 1 = EIN |
| STAT_PREDRIVE_CHECK | unsigned char | Status PreDriveCeck: 0 = AUS, 1 = EIN |
| _STAT_RESERVE67_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE68_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_ACL_AKTIV | unsigned char | ACL- Freischaltung für Recycling 0 = keine Freischaltung, 1 = Freischaltung aktiv |
| STAT_SENSOR_FGS_ARMING_FEHLER | unsigned char | 0 = kein Fehler, 1 = sendet Fehler |
| STAT_SENSOR_FGS_ARMING_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_FGS_ARMING_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_FGS_ARMING_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_FGS_ARMING_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| _STAT_RESERVE74_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE75_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE76_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_GK_FA_OUT_ZUSTAND | unsigned char | CAN-Info: Gurtkontakt Fahrer 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GK_FA_OUT_UNGUELTIG | unsigned char | CAN-Info: Gurtkontakt Fahrer 0 = Signal gueltig , 1 = Signal ungueltig |
| _STAT_RESERVE76A_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_GK_BF_OUT_ZUSTAND | unsigned char | CAN-Info: Gurtkontakt Beifahrer 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GK_BF_OUT_UNGUELTIG | unsigned char | CAN-Info: Gurtkontakt Beifahrer 0 = Signal gueltig , 1 = Signal ungueltig |
| _STAT_RESERVE76B_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE77_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE78_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_SITZBELEGUNG_BF_OUT_ZUSTAND | unsigned char | CAN-Info: Sitzbelegung Beifahrer (SBR-Sensor widerstandscodiert oder LIN ODER CIS) 0 = SBR Off (wird ausgegeben, wenn keine Person erkannt wurde), 1 = SBR On (wird ausgegeben, wenn Sitz mit einer Person belegt ist!) |
| STAT_SITZBELEGUNG_BF_OUT_UNGUELTIG | unsigned char | CAN-Info: Sitzbelegung Beifahrer 0= gueltig, 1 = ungueltig |
| STAT_SITZBELEGUNG_BF_OUT_INIT | unsigned char | CAN-Info: Sitzbelegung Beifahrer Initialisierung 0= INI nicht aktiv, 1 = INI aktiv |
| STAT_SENSOR_FGS_PTS_RECHTS_FEHLER | unsigned char | 0 = kein Fehler, 1 = sendet Fehler |
| STAT_SENSOR_FGS_PTS_RECHTS_KOMMUNIKATION_FEHLER | unsigned char | 0 = kein Fehler, 1 = Kommunikationsfehler |
| STAT_SENSOR_FGS_PTS_RECHTS_LEITUNG_FEHLER | unsigned char | 0 = kein Fehler, 1 = Leitungsfehler |
| STAT_SENSOR_FGS_PTS_RECHTS_TYP_FEHLER | unsigned char | 0 = Typ OKAY, 1 = falscher Typ |
| STAT_SENSOR_FGS_PTS_RECHTS_PLAUSIBILITAET | unsigned char | 0 = Plausibilität OKAY, 1 = Plausibilitätsfehler |
| STAT_GK_HL_OUT_ZUSTAND | unsigned char | CAN-Info: Gurtkontakt hinten links 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GK_HL_OUT_UNGUELTIG | unsigned char | CAN-Info: Gurtkontakt hinten links 0 =  Signal gueltig , 1 = Signal ungueltig |
| _STAT_RESERVE82A_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_GK_HR_OUT_ZUSTAND | unsigned char | CAN-Info: Gurtkontakt hinten rechts 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GK_HR_OUT_UNGUELTIG | unsigned char | CAN-Info: Gurtkontakt hinten rechts 0 = Signal gueltig , 1 = Signal ungueltig |
| _STAT_RESERVE82B_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE83_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE84_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| STAT_GK_HM_OUT_ZUSTAND | unsigned char | CAN-Info: Gurtkontakt hinten mitte 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GK_HM_OUT_UNGUELTIG | unsigned char | CAN-Info: Gurtkontakt hinten mitte 0 = Signal gueltig, 1 = Signal ungueltig |
| _STAT_RESERVE84A_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE85_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE86_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE87_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE88_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| _STAT_RESERVE89_SENSOR_OKAY | unsigned char | Reserve_Sensor |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-freigabe-zuendkreise"></a>
### STATUS_FREIGABE_ZUENDKREISE

Freigabeinfo Zuendkreise UDS : $22 ReadDataByIdentifier UDS : $D472 FREIGABE_ZUENDKREIS Modus: Default (0xD472)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AB1_FA_FREIGABE | unsigned char | FIX_ZK: Airbag Fahrer Stufe 1 0 = gesperrt, 1 = freigegeben |
| STAT_AB2_FA_FREIGABE | unsigned char | VAR_ZK: Airbag Fahrer Stufe 2 0 = gesperrt, 1 = freigegeben |
| STAT_AB_FA_VENTIL_FREIGABE | unsigned char | VAR_ZK: Adaptiver Airbag Fahrer Ventil 0 = gesperrt, 1 = freigegeben |
| STAT_AB1_BF_FREIGABE | unsigned char | FIX_ZK: Airbag Beifahrer Stufe 1 0 = gesperrt, 1 = freigegeben |
| STAT_AB2_BF_FREIGABE | unsigned char | VAR_ZK: Airbag Beifahrer Stufe 2 0 = gesperrt, 1 = freigegeben |
| STAT_AB_BF_VENTIL_FREIGABE | unsigned char | VAR_ZK: Adaptiver Airbag Beifahrer Ventil 0 = gesperrt, 1 = freigegeben |
| STAT_GS_FA_FREIGABE | unsigned char | FIX_ZK: Gurtstrammer Fahrer 0 = gesperrt, 1 = freigegeben |
| STAT_EBS_FA_FREIGABE | unsigned char | VAR_ZK: Endbeschlagstrammer Fahrer 0 = gesperrt, 1 = freigegeben |
| STAT_GKB_FA_FREIGABE | unsigned char | VAR_ ZK: Adaptiver Gurt-Kraftbegrenzer Fahrer 0 = gesperrt, 1 = freigegeben |
| STAT_GS_BF_FREIGABE | unsigned char | FIX_ZK: Gurtstrammer Beifahrer 0 = gesperrt, 1 = freigegeben |
| STAT_EBS_BF_FREIGABE | unsigned char | VAR_ZK: Endbeschlagstrammer Beifahrer 0 = gesperrt, 1 = freigegeben |
| STAT_GKB_BF_FREIGABE | unsigned char | VAR_ZK: Adaptiver Gurt-Kraftbegrenzer Beifahrer 0 = gesperrt, 1 = freigegeben |
| STAT_KNIE_AB_FA_FREIGABE | unsigned char | VAR_ZK: Knieairbag Fahrer 0 = gesperrt, 1 = freigegeben |
| STAT_KNIE_AB_BF_FREIGABE | unsigned char | VAR_ZK: Knieairbag Beifahrer 0 = gesperrt, 1 = freigegeben |
| STAT_KOS_FA_FREIGABE | unsigned char | VAR_ZK: Aktive Kopfstuetze Fahrer 0 = gesperrt, 1 = freigegeben |
| STAT_KOS_BF_FREIGABE | unsigned char | VAR_ZK: Aktive Kopfstuetze Beifahrer 0 = gesperrt, 1 = freigegeben |
| STAT_GS_HLI_FREIGABE | unsigned char | VAR_ZK: Gurtstrammer hinten links 0 = gesperrt, 1 = freigegeben |
| STAT_GS_HRE_FREIGABE | unsigned char | VAR_ZK: Gurtstrammer hinten rechts 0 = gesperrt, 1 = freigegeben |
| STAT_ARS_FA_FREIGABE | unsigned char | VAR_ZK: Aufrollstrammer Fahrer 0 = gesperrt, 1 = freigegeben |
| STAT_ARS_BF_FREIGABE | unsigned char | VAR_ZK: Aufrollstrammer Beifahrer 0 = gesperrt, 1 = freigegeben |
| STAT_SEITEN_AB_FA_FREIGABE | unsigned char | FIX_ZK: Sitzairbag Thorax Fahrer 0 = gesperrt, 1 = freigegeben |
| STAT_SEITEN_AB_BF_FREIGABE | unsigned char | FIX_ZK: Sitzairbag Thorax Beifahrer 0 = gesperrt, 1 = freigegeben |
| STAT_SEITEN_AB_FA_VENTIL_FREIGABE | unsigned char | VAR_ZK: Adaptives Sitzairbagventil Fahrer 0 = gesperrt, 1 = freigegeben |
| STAT_SEITEN_AB_BF_VENTIL_FREIGABE | unsigned char | VAR_ZK: Adaptives Sitzairbagventil Beifahrer 0 = gesperrt, 1 = freigegeben |
| STAT_KOPF_AB_LI_FREIGABE | unsigned char | VAR_ZK: Kopfairbag (Curtain) links 0 = gesperrt, 1 = freigegeben |
| STAT_KOPF_AB_RE_FREIGABE | unsigned char | VAR_ZK: Kopfairbag (Curtain) rechts 0 = gesperrt, 1 = freigegeben |
| STAT_SBK1_FREIGABE | unsigned char | FIX_ZK: Sicherheitsbatterieklemme 1 0 = gesperrt, 1 = freigegeben |
| STAT_SBK2_FREIGABE | unsigned char | VAR_ZK: Sicherheitsbatterieklemme 2 0 = gesperrt, 1 = freigegeben |
| STAT_RO_SCHUTZ_LINKS_FREIGABE | unsigned char | VAR_ZK: Rollover- Schutz links 0 = gesperrt, 1 = freigegeben ACSM4-B: Rollover-Schutz magnetisch oder pyrotechnisch ACSM4-C: nur pyrotechnisch |
| STAT_RO_SCHUTZ_RECHTS_FREIGABE | unsigned char | VAR_ZK: Rollover- Schutz rechts 0 = gesperrt, 1 = freigegeben ACSM4-B: Rollover-Schutz magnetisch oder pyrotechnisch ACSM4-C: nur pyrotechnisch |
| STAT_RO_SCHUTZ_LI_MAGN_FREIGABE | unsigned char | VAR_ZK: Rollover-Schutz magnetisch links (nur ACSM4-C) 0 = gesperrt, 1 = freigegeben |
| STAT_RO_SCHUTZ_RE_MAGN_FREIGABE | unsigned char | VAR_ZK: Rollover-Schutz magnetisch rechts (nur ACSM4-C) 0 = gesperrt, 1 = freigegeben |
| STAT_FGS_VLI_FREIGABE | unsigned char | VAR_ZK: Fussgaengerschutzsystem vorn links 0 = gesperrt, 1 = freigegeben |
| STAT_FGS_VRE_FREIGABE | unsigned char | VAR_ZK: Fussgaengerschutzsystem vorn rechts 0 = gesperrt, 1 = freigegeben |
| STAT_FGS_HLI_FREIGABE | unsigned char | VAR_ZK: Fussgaengerschutzsystem hinten links 0 = gesperrt, 1 = freigegeben |
| STAT_FGS_HRE_FREIGABE | unsigned char | VAR_ZK: Fussgaengerschutzsystem hinten rechts 0 = gesperrt, 1 = freigegeben |
| STAT_SBK3_FREIGABE | unsigned char | VAR_ZK: Sicherheitsbatterieklemme 3 0 = gesperrt, 1 = freigegeben |
| STAT_PPA_FREIGABE | unsigned char | VAR_ZK: PPA Windowbag 0 = gesperrt, 1 = freigegeben |
| STAT_FGS_PPA_RHM_FREIGABE | unsigned char | VAR_ZK: FGS_PPA_RHM 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE6_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE7_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE8_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE9_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE10_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE11_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE12_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE13_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE14_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE15_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE16_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE17_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE18_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE19_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE20_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE21_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| _STAT_RESERVE22_ZK_FREIGABE | unsigned char | VAR_ZK: Reserve 0 = gesperrt, 1 = freigegeben |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-widerstand-zuendkreis"></a>
### STATUS_WIDERSTAND_ZUENDKREIS

Widerstandswert Zuendkreise auslesen UDS : $22 ReadDataByIdentifier UDS : $D473 WIDERSTAND_ZUENDKREIS Modus: Default (0xD473)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AB1_FA_WERT | real | FIX_ZK: Airbag Fahrer Stufe 1 Zündkreiswiderstand in Ohm |
| STAT_AB1_FA_EINH | string | "Ohm" |
| STAT_AB2_FA_WERT | real | VAR_ZK: Airbag Fahrer Stufe 2 Zündkreiswiderstand in Ohm |
| STAT_AB2_FA_EINH | string | "Ohm" |
| STAT_AB_FA_VENTIL_WERT | real | VAR_ZK: Adaptiver Airbag Fahrer Ventil Zündkreiswiderstand in Ohm |
| STAT_AB_FA_VENTIL_EINH | string | "Ohm" |
| STAT_AB1_BF_WERT | real | FIX_ZK: Airbag Beifahrer Stufe 1 Zündkreiswiderstand in Ohm |
| STAT_AB1_BF_EINH | string | "Ohm" |
| STAT_AB2_BF_WERT | real | VAR_ZK: Airbag Beifahrer Stufe 2 Zündkreiswiderstand in Ohm |
| STAT_AB2_BF_EINH | string | "Ohm" |
| STAT_AB_BF_VENTIL_WERT | real | VAR_ZK: Adaptiver Airbag Beifahrer Ventil Zündkreiswiderstand in Ohm |
| STAT_AB_BF_VENTIL_EINH | string | "Ohm" |
| STAT_GS_FA_WERT | real | FIX_ZK: Gurtstrammer Fahrer Zündkreiswiderstand in Ohm |
| STAT_GS_FA_EINH | string | "Ohm" |
| STAT_EBS_FA_WERT | real | VAR_ZK: Endbeschlagstrammer Fahrer Zündkreiswiderstand in Ohm |
| STAT_EBS_FA_EINH | string | "Ohm" |
| STAT_GKB_FA_WERT | real | VAR_ ZK: Adaptiver Gurt-Kraftbegrenzer Fahrer Zündkreiswiderstand in Ohm |
| STAT_GKB_FA_EINH | string | "Ohm" |
| STAT_GS_BF_WERT | real | FIX_ZK: Gurtstrammer Beifahrer Zündkreiswiderstand in Ohm |
| STAT_GS_BF_EINH | string | "Ohm" |
| STAT_EBS_BF_WERT | real | VAR_ZK: Endbeschlagstrammer Beifahrer Zündkreiswiderstand in Ohm |
| STAT_EBS_BF_EINH | string | "Ohm" |
| STAT_GKB_BF_WERT | real | VAR_ZK: Adaptiver Gurt-Kraftbegrenzer Beifahrer Zündkreiswiderstand in Ohm |
| STAT_GKB_BF_EINH | string | "Ohm" |
| STAT_KNIE_AB_FA_WERT | real | VAR_ZK: Knieairbag Fahrer Zündkreiswiderstand in Ohm |
| STAT_KNIE_AB_FA_EINH | string | "Ohm" |
| STAT_KNIE_AB_BF_WERT | real | VAR_ZK: Knieairbag Beifahrer Zündkreiswiderstand in Ohm |
| STAT_KNIE_AB_BF_EINH | string | "Ohm" |
| STAT_KOS_FA_WERT | real | VAR_ZK: Aktive Kopfstuetze Fahrer Zündkreiswiderstand in Ohm |
| STAT_KOS_FA_EINH | string | "Ohm" |
| STAT_KOS_BF_WERT | real | VAR_ZK: Aktive Kopfstuetze Beifahrer Zündkreiswiderstand in Ohm |
| STAT_KOS_BF_EINH | string | "Ohm" |
| STAT_GS_HLI_WERT | real | VAR_ZK: Gurtstrammer hinten links Zündkreiswiderstand in Ohm |
| STAT_GS_HLI_EINH | string | "Ohm" |
| STAT_GS_HRE_WERT | real | VAR_ZK: Gurtstrammer hinten rechts Zündkreiswiderstand in Ohm |
| STAT_GS_HRE_EINH | string | "Ohm" |
| STAT_ARS_FA_WERT | real | VAR_ZK: Aufrollstrammer Fahrer Zündkreiswiderstand in Ohm |
| STAT_ARS_FA_EINH | string | "Ohm" |
| STAT_ARS_BF_WERT | real | VAR_ZK: Aufrollstrammer Beifahrer Zündkreiswiderstand in Ohm |
| STAT_ARS_BF_EINH | string | "Ohm" |
| STAT_SEITEN_AB_FA_WERT | real | FIX_ZK: Sitzairbag Thorax Fahrer Zündkreiswiderstand in Ohm |
| STAT_SEITEN_AB_FA_EINH | string | "Ohm" |
| STAT_SEITEN_AB_BF_WERT | real | FIX_ZK: Sitzairbag Thorax Beifahrer Zündkreiswiderstand in Ohm |
| STAT_SEITEN_AB_BF_EINH | string | "Ohm" |
| STAT_SEITEN_AB_FA_VENTIL_WERT | real | VAR_ZK: Adaptiver Sitzairbagventil Fahrer Zündkreiswiderstand in Ohm |
| STAT_SEITEN_AB_FA_VENTIL_EINH | string | "Ohm" |
| STAT_SEITEN_AB_BF_VENTIL_WERT | real | VAR_ZK: Adaptiver Sitzairbagventil Beifahrer Zündkreiswiderstand in Ohm |
| STAT_SEITEN_AB_BF_VENTIL_EINH | string | "Ohm" |
| STAT_KOPF_AB_LI_WERT | real | VAR_ZK: Kopfairbag (Curtain) links Zündkreiswiderstand in Ohm |
| STAT_KOPF_AB_LI_EINH | string | "Ohm" |
| STAT_KOPF_AB_RE_WERT | real | VAR_ZK: Kopfairbag (Curtain) rechts Zündkreiswiderstand in Ohm |
| STAT_KOPF_AB_RE_EINH | string | "Ohm" |
| STAT_SBK1_WERT | real | FIX_ZK: Sicherheitsbatterieklemme 1 Zündkreiswiderstand in Ohm |
| STAT_SBK1_EINH | string | "Ohm" |
| STAT_SBK2_WERT | real | VAR_ZK: Sicherheitsbatterieklemme 2 Zündkreiswiderstand in Ohm |
| STAT_SBK2_EINH | string | "Ohm" |
| STAT_RO_SCHUTZ_LI_WERT | real | VAR_ZK: Rollover- Schutz links Zündkreiswiderstand in Ohm ACSM4-B: Rollover-Schutz magnetisch oder pyrotechnisch ACSM4-C: nur pyrotechnisch |
| STAT_RO_SCHUTZ_LI_EINH | string | "Ohm" |
| STAT_RO_SCHUTZ_RE_WERT | real | VAR_ZK: Rollover- Schutz rechts Zündkreiswiderstand in Ohm ACSM4-B: Rollover-Schutz magnetisch oder pyrotechnisch ACSM4-C: nur pyrotechnisch |
| STAT_RO_SCHUTZ_RE_EINH | string | "Ohm" |
| STAT_RO_SCHUTZ_LI_MAGN_WERT | real | VAR_ZK: Rollover-Schutz magnetisch links (nur ACSM4-C) Zündkreiswiderstand in Ohm |
| STAT_RO_SCHUTZ_LI_MAGN_EINH | string | "Ohm" |
| STAT_RO_SCHUTZ_RE_MAGN_WERT | real | VAR_ZK: Rollover-Schutz magnetisch rechts (nur ACSM4-C) Zündkreiswiderstand in Ohm |
| STAT_RO_SCHUTZ_RE_MAGN_EINH | string | "Ohm" |
| STAT_FGS_VLI_WERT | real | VAR_ZK: Fussgaengerschutzsystem vorn links Zündkreiswiderstand in Ohm |
| STAT_FGS_VLI_EINH | string | "Ohm" |
| STAT_FGS_VRE_WERT | real | VAR_ZK: Fussgaengerschutzsystem vorn rechts Zündkreiswiderstand in Ohm |
| STAT_FGS_VRE_EINH | string | "Ohm" |
| STAT_FGS_HLI_WERT | real | VAR_ZK: Fussgaengerschutzsystem hinten links Zündkreiswiderstand in Ohm |
| STAT_FGS_HLI_EINH | string | "Ohm" |
| STAT_FGS_HRE_WERT | real | VAR_ZK: Fussgaengerschutzsystem hinten rechts Zündkreiswiderstand in Ohm |
| STAT_FGS_HRE_EINH | string | "Ohm" |
| STAT_SBK3_WERT | real | VAR_ZK: Sicherheitsbatterieklemme 3 Zündkreiswiderstand in Ohm |
| STAT_SBK3_EINH | string | "Ohm" |
| STAT_PPA_WERT | real | VAR_ZK: PPA Windowbag Zündkreiswiderstand in Ohm |
| STAT_PPA_EINH | string | "Ohm" |
| STAT_FGS_PPA_RHM_WERT | real | VAR_ZK: FGS PPA RHM Zündkreiswiderstand in Ohm |
| STAT_FGS_PPA_RHM_EINH | string | "Ohm" |
| _STAT_RESERVE6_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE6_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE7_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE7_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE8_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE8_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE9_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE9_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE10_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE10_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE11_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE11_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE12_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE12_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE13_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE13_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE14_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE14_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE15_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE15_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE16_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE16_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE17_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE17_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE18_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE18_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE19_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE19_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE20_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE20_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE21_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE21_ZK_EINH | string | "Ohm" |
| _STAT_RESERVE22_ZK_WERT | real | VAR_ZK: Reserve Zündkreiswiderstand in Ohm |
| _STAT_RESERVE22_ZK_EINH | string | "Ohm" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-gurtkontakte"></a>
### STATUS_GURTKONTAKTE

Stromwerte Gurtkontakte, POS und SPS auslesen UDS : $22 ReadDataByIdentifier UDS : $D474 GURTKONTAKTE Modus: Default (0xD474)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GK_FA_WERT | real | Stromwert Gurtkontakt Fahrer |
| STAT_GK_FA_EINH | string | "mA" |
| STAT_GK_BF_WERT | real | Stromwert Gurtkontakt Beifahrer |
| STAT_GK_BF_EINH | string | "mA" |
| STAT_GK_HLI_WERT | real | Stromwert Gurtkontakt hinten links |
| STAT_GK_HLI_EINH | string | "mA" |
| STAT_GK_HRE_WERT | real | Stromwert Gurtkontakt hinten rechts |
| STAT_GK_HRE_EINH | string | "mA" |
| STAT_GK_HMI_WERT | real | Stromwert Gurtkontakt hinten mitte |
| STAT_GK_HMI_EINH | string | "mA" |
| STAT_POS_WERT | real | Stromwert Passenger Airbag Off Schalter |
| STAT_POS_EINH | string | "mA" |
| STAT_SPSF_WERT | real | Stromwert Sitzpositionssensor Fahrer |
| STAT_SPSF_EINH | string | "mA" |
| STAT_SPSBF_WERT | real | Stromwert Sitzpositionssensor Beifahrer |
| STAT_SPSBF_EINH | string | "mA" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-fehlerzaehler-sat-lesen"></a>
### STATUS_FEHLERZAEHLER_SAT_LESEN

Fehlerzaehler Schnittstelle Crashsensoren lesen UDS : $22 ReadDataByIdentifier UDS : $D475 FEHLERZAEHLER_SAT_LESEN Modus: Default (0xD475)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ERROR_UFL_WERT | unsigned long | Fehlerzaehler UpFront links |
| STAT_ERROR_UFR_WERT | unsigned long | Fehlerzaehler UpFront rechts |
| STAT_ERROR_SSTL_WERT | unsigned long | Fehlerzaehler Satellit Tür links |
| STAT_ERROR_SSTR_WERT | unsigned long | Fehlerzaehler Satellit Tür rechts |
| STAT_ERROR_SSBLX_WERT | unsigned long | Fehlerzaehler Satellit B-Saeule links X |
| STAT_ERROR_SSBLY_WERT | unsigned long | Fehlerzaehler Satellit B-Saeule links Y |
| STAT_ERROR_SSBRX_WERT | unsigned long | Fehlerzaehler Satellit B-Saeule rechts X |
| STAT_ERROR_SSBRY_WERT | unsigned long | Fehlerzaehler Satellit B-Saeule rechts Y |
| STAT_ERROR_SZX_WERT | unsigned long | Fehlerzaehler Satellit Zentralsensor X |
| STAT_ERROR_SZY_WERT | unsigned long | Fehlerzaehler Satellit Zentralsensor Y |
| STAT_ERROR_ZS_LGY_WERT | unsigned long | Fehlerzaehler Satellit Zentralsensor Low g Y |
| STAT_ERROR_ZS_LGZ_WERT | unsigned long | Fehlerzaehler Satellit Zentralsensor Low g Z |
| STAT_ERROR_ZS_ROLL_WERT | unsigned long | Fehlerzaehler Satellit Zentralsensor Roll Achse |
| STAT_ERROR_FGS_SB_WERT | unsigned long | Fehlerzaehler Fussgaengerschutz Sensorband |
| STAT_ERROR_SSCLY_WERT | unsigned long | Fehlerzaehler Satellit C-Saeule links Y oder Fehlerzaehler PTS links |
| STAT_ERROR_SSCRY_WERT | unsigned long | Fehlerzaehler Satellit C-Saeule rechts Y oder Fehlerzaehler PTS rechts |
| STAT_ERROR_ZS_SCHALL_WERT | unsigned long | Fehlerzaehler Satellit Zentralsensor Koerperschall |
| STAT_ERROR_FGS_M_WERT | unsigned long | Fehlerzaehler Fussgängerschutz Safing-Sensor |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-seatbeltmind"></a>
### STATUS_SEATBELTMIND

Status Seatbeltreminder lesen UDS : $22 ReadDataByIdentifier UDS : $D477 SEATBELTMIND Modus: Default (0xD477)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHASE_SBR_FA_WERT | unsigned char | Phase der SBR- Berechnung Fahrer |
| STAT_PHASE_SBR_BF_WERT | unsigned char | Phase der SBR- Berechnung Beifahrer |
| STAT_WEGSTRECKE_WERT | unsigned int | zurückgelegte Wegstrecke |
| STAT_WEGSTRECKE_EINH | string | "m" |
| STAT_GESCHWINDIGKEIT_WERT | unsigned int | momentane Fahrzeuggeschwindigkeit |
| STAT_GESCHWINDIGKEIT_EINH | string | "km/h" |
| STAT_RICHTUNG_FAHRT | unsigned char | Erkannte Fahrtrichtung |
| STAT_RICHTUNG_FAHRT_TEXT | string | Erkannte Fahrtrichtung |
| STAT_MONITOR_SBR_FA_WERT | unsigned int | Zeit seit abgegurtet Fahrer |
| STAT_MONITOR_SBR_FA_EINH | string | "s" |
| STAT_MONITOR_SBR_BF_WERT | unsigned int | Zeit seit abgegurtet Beifahrer |
| STAT_MONITOR_SBR_BF_EINH | string | "s" |
| STAT_WARN_FA | unsigned char | Status Fahrerwarnung 0 = aus 1 = ein |
| STAT_WARN_BF | unsigned char | Status Beifahrerwarnung 0 = aus 1 = ein |
| STAT_GK_FA_ZUSTAND | unsigned char | Status Zustand Gurtkontakt Fahrer 0 = nicht gesteckt, 1 = gesteckt |
| STAT_GK_BF_ZUSTAND | unsigned char | Status Zustand Gurtkontakt Beifahrer 0 = nicht gesteckt, 1 = gesteckt |
| STAT_SITZBELEGUNG_BF | unsigned char | Sitzbelegung Beifahrer (SBR-Sensor widerstandscodiert oder LIN ODER CIS) 0 = SBR Off (wird ausgegeben, wenn keine Person erkannt wurde), 1 = SBR On (wird ausgegeben, wenn Sitz mit einer Person belegt ist!) |
| STAT_SITZBELEGUNG_BF_FEHLER | unsigned char | Sitzbelegung Beifahrer (SBR-Sensor widerstandscodiert ODER CIS) 0 = kein Fehler, 1 = Fehler |
| STAT_SITZBELEGUNG_BF_INTERN | unsigned char | Entprellter Wert der Sitzbelegung Beifahrer (SBR-Sensor widerstandscodiert oder LIN ODER CIS) 0 = SBR Off (wird ausgegeben, wenn keine Person erkannt wurde), 1 = SBR On (wird ausgegeben, wenn Sitz mit einer Person belegt ist!) |
| STAT_STATE_MACH_FA_WERT | unsigned long | Status State Machine Fahrer |
| STAT_STATE_MACH_BF_WERT | unsigned long | Status State Machine Beifahrer |
| STAT_KLEMMENZUSTAND_KL15 | unsigned char | Status Klemmenzustand via CAN 0 = Kl.15 nicht erkannt, 1 = Kl.15 erkannt |
| STAT_PASSENGER_AIRBAG_OFF_SWITCH_ZUSTAND | unsigned char | Zustand Passenger Airbag Off Schalter , 1 = nicht geschaltet = Steuergerät sendet 1 = Airbag ein = Aufdruck Schalter On (= Schalterstellung 0) 0 = geschaltet = Steuergerät sendet 0 = Airbag aus = Aufdruck Schalter Off (= Schalterstellung 1) |
| STAT_PASSENGER_AIRBAG_OFF_SWITCH_FEHLER | unsigned char | Status Fehler Passenger Airbag Off Schalter 0 = kein Fehler, 1 = Fehler |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-sg-temp"></a>
### STATUS_SG_TEMP

Innentemperatur Steuergerät lesen UDS : $22 ReadDataByIdentifier UDS : $D478 SG_TEMP Modus: Default (0xD478)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SG_TEMP_WERT | real | Steuergeräteinnentemperatur in °C |
| STAT_SG_TEMP_EINH | string | "°C" |
| STAT_SG_TEMP_ZUSTAND | unsigned char | 0..200 = in Ordnung 201..254 = unbekannt 255 = ungueltig |
| STAT_SG_TEMP_ZUSTAND_TEXT | string | 0..200 = in Ordnung 201..254 = unbekannt 255 = ungueltig |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-pol"></a>
### STEUERN_POL

PassengerAirbag Off- Leuchte POL steuern/ dimmen UDS : $2E WriteDataByIdentifier UDS : $D479 POL Modus: Default (0xD479)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_ID_STEUERN_POL | unsigned long | 0 = Aus, 255 = 100% Ein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-lenkseite"></a>
### STATUS_LENKSEITE

Eincodierte Lenkseite auslesen UDS : $22 ReadDataByIdentifier UDS : $D47A LENKSEITE Modus: Default (0xD47A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LENKSEITE | unsigned char | 0 =Linkslenker 1= Rechtslenker |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-test-ro-magn"></a>
### STEUERN_TEST_RO_MAGN

Testausloesung magnetische Rolloveraktuatoren UDS : $2E WriteDataByIdentifier UDS : $D47B STEUERN_RO_MAGN Ausloesung magnetischer Rolloverbuegel (0xD47B)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STEUERN_RO_MAGN | unsigned char | Argument schützt vor unbeabsichtigter Ausführung. Zu übergebender Parameter: 0x5A |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-baureihe"></a>
### STATUS_BAUREIHE

Baureihe auslesen UDS : $22 ReadDataByIdentifier UDS : $D47E BAUREIHE Modus: Default (0xD47E)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BAUREIHE | unsigned char | Baureihenkennung siehe Tabelle TAB_BAUREIHENKENNUNG |
| STAT_BAUREIHE_TEXT | string | Baureihenkennung siehe Tabelle TAB_BAUREIHENKENNUNG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-laendervariante"></a>
### STATUS_LAENDERVARIANTE

Laendervariante lesen UDS : $22 ReadDataByIdentifier UDS : $D47F LAENDERVARIANTE Modus: Default (0xD47F)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAENDERVAR | unsigned char | Ländervariante des Fahrzeugs 0 = ECE 1 = US |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-aacn"></a>
### STATUS_AACN

AACN lesen UDS : $22 ReadDataByIdentifier UDS : $D480 AACN Modus: Default (0xD480)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AACN | unsigned char | Status Datenübertragung TCU via AACN |
| STAT_AACN_TEXT | string | Status Datenübertragung TCU via AACN |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-near-crash-daten-loeschen"></a>
### STEUERN_NEAR_CRASH_DATEN_LOESCHEN

NEAR_CRASH_DATEN Speicher loeschen UDS : $2E WriteDataByIdentifier UDS : $F020 NEAR_CRASH-DATEN_LOESCHEN Modus: Development Löscht alle Infospeichereinträge (0xF020)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SPRMIB | unsigned char | SuppressPositiveResponseMessageIndicationBit Werttabelle 0 = false 1 = true |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-fahrgestellnummer"></a>
### STATUS_FAHRGESTELLNUMMER

Fahrgestellnummer lesen UDS : $22 ReadDataByIdentifier UDS $F190 FAHRGESTELLNUMMER Modus: Default (0xF190)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FAHRGESTELLNUMMER | string | BMW-Fahrgestellnummer (VIN) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-number-of-edr-devices-lesen"></a>
### STATUS_NUMBER_OF_EDR_DEVICES_LESEN

Anzahl Crash-Recorder-Eintraege lesen UDS : $22 ReadDataByIdentifier UDS : $FA10 NUMBER_OF_EDR_DEVICES Modus: Default (0xFA10)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NUMBER_OF_EDR_DEVICES | string | NUMBER_OF_EDR_DEVICES_LESEN |
| STAT_NUMBER_OF_EDR_DEVICES_EINH | string | "HEX" |
| STAT_RESERVED | unsigned char | RESERVED |
| STAT_STORAGE_TYPE | unsigned char | STAT_STORAGE_TYPE |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-edr-identification-lesen"></a>
### STATUS_EDR_IDENTIFICATION_LESEN

Anzahl Crash-Recorder-Eintraege lesen UDS : $22 ReadDataByIdentifier UDS : $FA11 EDR_IDENTIFICATION Modus: Default (0xFA11)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OEM_IDENTIFICATION | string | STAT_OEM_IDENTIFICATION |
| STAT_OEM_IDENTIFICATION_EINH | string | "HEX" |
| STAT_EDR_VERSION | unsigned int | STAT_EDR_VERSION |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-edr-address-information-version-lesen"></a>
### STATUS_EDR_ADDRESS_INFORMATION_VERSION_LESEN

Anzahl Crash-Recorder-Eintraege lesen UDS : $22 ReadDataByIdentifier UDS : $FA12 EDR_ADDRESS_INFORMATION Modus: Default (0xFA12)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADDRESS_FORMAT | string | 1 - 11bit normal addressing 2 - 11bit extended addressing 3 - 11bit mixed addressing 4 - 29bit normal fixed addressing 5 - 29bit mixed adressing 6 - 29bit unique adddressing 07..FF - reserved |
| STAT_ADDRESS_FORMAT_EINH | string | "HEX" |
| STAT_REQUEST_ADDRESS_EDR_STORAGE | unsigned long | 11bit or 29bit CAN-Identifier |
| STAT_RESPONSE_ADDRESS_EDR_STORAGE | unsigned long | 11bit or 29bit CAN-Identifier |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-betriebsstundenzaehler-aktuell"></a>
### STATUS_BETRIEBSSTUNDENZAEHLER_AKTUELL

Betriebsstundenzaehler aktuell lesen UDS : $22 ReadDataByIdentifier UDS : $FD21 BETRIEBSSTUNDENZAEHLER Modus: Default Steuergerätebezogene Betriebszeit (0xFD21)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BETRIEBSSTUNDENZAEHLER_AKTUELL_WERT | binary | BETRIEBSSTUNDENZAEHLER_AKTUELL (Zeit in ms) lesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-power-on-zaehler"></a>
### STATUS_POWER_ON_ZAEHLER

Power on Zaehler lesen UDS : $22 ReadDataByIdentifier UDS : $FD22 POWER_ON_ZAEHLER Modus: Default (0xFD22)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_POWER_ON_ZAEHLER | unsigned long | Power-On-Zaehler lesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-kennung-ze-parameter"></a>
### STATUS_KENNUNG_ZE_PARAMETER

Kennung der Algorithmus-Parameter lesen UDS : $22 ReadDataByIdentifier UDS : $FD23 KENNUNG_ZE_PARAMETER Modus: Default (0xFD23)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KENNUNG_CRASH_ALGO | string | Kennung ZE Parameterdaten (Crash-Algo) lesen |
| STAT_KENNUNG_FGS_ALGO | string | Kennung ZE Parameterdaten (FGS-Algo) lesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemzeit-letztes-fs-loeschen"></a>
### STATUS_SYSTEMZEIT_LETZTES_FS_LOESCHEN

Betriebsstundenzaehler letztes FS-Loeschen lesen UDS : $22 ReadDataByIdentifier UDS : $FD24 SYSTEMZEIT_LETZTES_FS_LOESCHEN Modus: Default Steuergerätebezogene Betriebszeit (0xFD24)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BETRIEBSSTUNDENZAEHLER_DER_LETZTEN_FEHLERLOESCHUNG | binary | Betriebsstundenzaehler der letzten Fehlerloeschung (in ms) lesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemzeit-power-on"></a>
### STATUS_SYSTEMZEIT_POWER_ON

Betriebsstundenzaehler Beginn aktueller Power- on- Zyklus lesen UDS : $22 ReadDataByIdentifier UDS : $FD25 SYSTEMZEIT_POWER_ON Modus: Default Steuergerätebezogene Betriebszeit (0xFD25)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BETRIEBSSTUNDENZAEHLER_LETZTER_POWER_ON | binary | BETRIEBSSTUNDENZAEHLER letzter Power on (in ms) lesen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemzeit-zeitmaster-power-on"></a>
### STATUS_SYSTEMZEIT_ZEITMASTER_POWER_ON

Systemzeit Zeitmaster aktueller Power on Zyklus lesen UDS : $22 ReadDataByIdentifier UDS : $FD26 SYSTEMZEIT_ZEITMASTER_POWER_ON Modus: Default Fahrzeugbezogene Betriebszeit (0xFD26)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMZEIT_ZEITMASTER_POWER_ON | unsigned long | SYSTEMZEIT_ZEITMASTER_POWER_ON |
| STAT_SYSTEMZEIT_ZEITMASTER_POWER_ON_EINH | string | "s" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemzeit-zeitmaster-aktuell"></a>
### STATUS_SYSTEMZEIT_ZEITMASTER_AKTUELL

Systemzeit Zeitmaster aktuell lesen UDS : $22 ReadDataByIdentifier UDS : $FD30 SYSTEMZEIT_ZEITMASTER_AKTUELL Modus: Default Fahrzeugbezogene Betriebszeit (0xFD30)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMZEIT_ZEITMASTER_AKTUELL | unsigned long | Systemzeit Zeitmaster lesen |
| STAT_SYSTEMZEIT_ZEITMASTER_AKTUELL_EINH | string | "s" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemzeit-zeitmaster-letztes-fs-loeschen"></a>
### STATUS_SYSTEMZEIT_ZEITMASTER_LETZTES_FS_LOESCHEN

Systemzeit Zeitmaster beim letzen FS-Loeschen UDS : $22 ReadDataByIdentifier UDS : $FD31 SYSTEMZEIT_ZEITMASTER_LETZTES_FS_LOESCHEN Modus: Default Fahrzeugbezogene Betriebszeit (0xFD31)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMZEIT_ZEITMASTER_LETZTES_FS_LOESCHEN | unsigned long | SYSTEMZEIT_ZEITMASTER_LETZTES_FS_LOESCHEN lesen |
| STAT_SYSTEMZEIT_ZEITMASTER_LETZTES_FS_LOESCHEN_EINH | string | "s" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-zeitstempel-power-on"></a>
### STATUS_ZEITSTEMPEL_POWER_ON

Zeitstempel zum Zeitpunkt des aktuellen Power-On auslesen (Tag/ Monat/ Jahr) UDS : $22 ReadDataByIdentifier UDS : $FD32 ZEITSTEMPEL_POWER_ON Modus: Default (0xFD32)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DISP_HR | unsigned char | DISP_HR |
| STAT_DISP_MN | unsigned char | DISP_MN |
| STAT_DISP_SEC | unsigned char | DISP_SEC |
| STAT_DISP_DATE_DAY | unsigned char | DISP_DATE_DAY |
| STAT_DISP_DATE_WDAY | unsigned char | DISP_DATE_WDAY |
| STAT_DISP_DATE_WDAY_TEXT | string | DISP_DATE_WDAY |
| STAT_DISP_DATE_MON | unsigned char | DISP_DATE_MON |
| STAT_DISP_DATE_YR | unsigned int | DISP_DATE_YR |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-zeitstempel-aktuell"></a>
### STATUS_ZEITSTEMPEL_AKTUELL

Zeitstempel aktuell lesen (Tag/ Monat/ Jahr) UDS : $22 ReadDataByIdentifier UDS : $FD33 ZEITSTEMPEL_AKTUELL Modus: Default (0xFD33)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DISP_HR | unsigned char | DISP_HR |
| STAT_DISP_MN | unsigned char | DISP_MN |
| STAT_DISP_SEC | unsigned char | DISP_SEC |
| STAT_DISP_DATE_DAY | unsigned char | DISP_DATE_DAY |
| STAT_DISP_DATE_WDAY | unsigned char | DISP_DATE_WDAY |
| STAT_DISP_DATE_WDAY_TEXT | string | DISP_DATE_WDAY |
| STAT_DISP_DATE_MON | unsigned char | DISP_DATE_MON |
| STAT_DISP_DATE_YR | unsigned int | DISP_DATE_YR |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-zeitstempel-letztes-fs-loeschen"></a>
### STATUS_ZEITSTEMPEL_LETZTES_FS_LOESCHEN

Zeitstempel zum Zeitpunkt des letzten Fehlerspeicher-Loeschens auslesen (Tag/ Monat/ Jahr) UDS : $22 ReadDataByIdentifier UDS : $FD34 ZEITSTEMPEL_LETZTES_FS_LOESCHEN Modus: Default (0xFD34)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DISP_HR | unsigned char | DISP_HR |
| STAT_DISP_MN | unsigned char | DISP_MN |
| STAT_DISP_SEC | unsigned char | DISP_SEC |
| STAT_DISP_DATE_DAY | unsigned char | DISP_DATE_DAY |
| STAT_DISP_DATE_WDAY | unsigned char | DISP_DATE_WDAY |
| STAT_DISP_DATE_WDAY_TEXT | string | DISP_DATE_WDAY |
| STAT_DISP_DATE_MON | unsigned char | DISP_DATE_MON |
| STAT_DISP_DATE_YR | unsigned int | DISP_DATE_YR |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-letzte-systemzeit-aktiv"></a>
### STATUS_LETZTE_SYSTEMZEIT_AKTIV

Systemzeit Zeitmaster, Ende letzter Klemmenzyklus, lesen UDS : $22 ReadDataByIdentifier UDS : $FD35 LETZTE_SYSTEMZEIT_AKTIV Modus: Default (0xFD35)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LETZTE_SYSTEMZEIT_AKTIV | unsigned long | ZEITSTEMPEL_POWER_ON |
| STAT_LETZTE_SYSTEMZEIT_AKTIV_EINH | string | "s" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bmw-sachnummer"></a>
### STATUS_BMW_SACHNUMMER

Lesen BMW Sachnummer UDS : $22 ReadDataByIdentifier UDS : $FD50 BMW_SACHNUMMER Modus: Default (0xFD50)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BMW_SACHNUMMER | string | BMW-Sachnummer |
| STAT_BMW_SACHNUMMER_EINH | string | "HEX" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-testausl-roll-magn"></a>
### TESTAUSL_ROLL_MAGN

UDS   : $2E   RoutineControl UDS   : $40   Testauslösung vorbereiten UDS   : $81   Testauslösung vorbereiten UDS   : $2E   RoutineControl UDS   : $D4   Testauslösung durchführen UDS   : $7B   Testauslösung durchführen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| P1 | int | 0x0FF0 	: Freigabe Testauslösung vorbereiten |
| P2 | int | 0x5A 	: Freigabe Testauslösung durchführen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST2 | binary | Hex-Auftrag an SG |
| _RESPONSE2 | binary | Hex-Antwort von SG |
| _REQUEST3 | binary | Hex-Auftrag an SG |
| _RESPONSE3 | binary | Hex-Antwort von SG |

<a id="job-steuern-notruf"></a>
### _STEUERN_NOTRUF

Steuern Notruf Steuern Notruf UDS : $2E WriteDataByIdentifier UDS : $D47C Steuern_Notruf Wird verwendet zur Telefonabsicherung bei EI-4.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CONTEXT_COUNTER | unsigned char | ContextCounter 7-Bit Zähler von 0-127 |
| E_CALL_TYPE | unsigned char | ECallType |
| NO_OF_CRASH_EVENTS | unsigned char | Anzahl Crash-Events Anzahl Crasheinträge -&gt; Beeinflußt nicht die Anzahl der anzugebenden Parameter |
| VERSION_NUMBER | unsigned char | Versionsnummer Versionsnummer der "SendEmergencyCall"-Nachricht. (von 0.0 bis 25.5 -&gt; hier $1F=31=V3.1) |
| OCCUPANT_STATE | unsigned int | Insassen-Status |
| DEPLOYED_AIRBAGS | unsigned long | Ausgelöste Airbags |
| ROLL_OVER | unsigned char | RollOver 00: not detected (default) 01: detected 10: not equipped 11: unknown |
| CRASH_EVENT_1_RICHTUNG | char | CrashEvent 1 Richtung +0/Bit1..0	FrontCrash			00: not detected (default) +0/Bit3..2	DriverSideCrash		01: detected +0/Bit5..4	NonDriverSideCrash	10: reserved +0/Bit7..6	RearCrash			11: reserved |
| CRASH_EVENT_1_DELTAVX | char | CrashEvent 1 DeltaVx  0x00: 	kein delta-v detektiert (default) 0x81: 	kleiner als -126km/h 0x82-0x7E:	-126km/h bis +126km/h 0x7F: 	größer als +126km/h 0x80: 	unknown (codiert als signed integer)  DeltaVx: Zentralsensor (x-Richtung) DeltaVyl: B-Säule links (y-Richtung) DeltaVyr: B-Säule rechts (y-Richtung) DeltaVyc: Zentralsensor (y-Richtung) |
| CRASH_EVENT_1_DELTAVYL | char | CrashEvent 1 DeltaVyl (Beschreibung siehe DeltaVx) |
| CRASH_EVENT_1_DELTAVYR | char | CrashEvent 1 DeltaVyr (Beschreibung siehe DeltaVx) |
| CRASH_EVENT_1_DELTAVYC | char | CrashEvent 1 DeltaVyc (Beschreibung siehe DeltaVx) |
| CRASH_EVENT_1_CLIPPING | char | CrashEvent 1 Clipping IntegrationTime (+5/Bit1..0) Integrationszeit für die Ermittlung der DeltaV-Werte 0x00: &lt;=100ms 0x01: &lt;=150ms 0x02: &lt;=200ms 0x03: &gt; 200ms  ClippingTime_left (+5/Bit4..2) Clipping-Zeit während der DeltaVyl-Berechnung 0x00: &lt;=2ms 0x01: &gt;2ms und &lt;=4ms ... 0x06: &gt;10ms und &lt;=12ms 0x07: &gt;12ms  ClippingTime_right (+5/Bit7..5) Clipping-Zeit während der DeltaVyr-Berechnung 0x00: &lt;=2ms 0x01: &gt;2ms und &lt;=4ms ... 0x06: &gt;10ms und &lt;=12ms 0x07: &gt;12ms |
| CRASH_EVENT_2_RICHTUNG | char | CrashEvent 2 Richtung (Beschreibung siehe Crashevent 1) |
| CRASH_EVENT_2_DELTAVX | char | CrashEvent 2 DeltaVx (Beschreibung siehe Crashevent 1) |
| CRASH_EVENT_2_DELTAVYL | char | CrashEvent 2 DeltaVyl (Beschreibung siehe Crashevent 1) |
| CRASH_EVENT_2_DELTAVYR | char | CrashEvent 2 DeltaVyr (Beschreibung siehe Crashevent 1) |
| CRASH_EVENT_2_DELTAVYC | char | CrashEvent 2 DeltaVyc (Beschreibung siehe Crashevent 1) |
| CRASH_EVENT_2_CLIPPING | char | CrashEvent 2 Clipping (Beschreibung siehe Crashevent 1) |
| CRASH_EVENT_3_RICHTUNG | char | CrashEvent 3 Richtung (Beschreibung siehe Crashevent 1) |
| CRASH_EVENT_3_DELTAVX | char | CrashEvent 3 DeltaVx (Beschreibung siehe Crashevent 1) |
| CRASH_EVENT_3_DELTAVYL | char | CrashEvent 3 DeltaVyl (Beschreibung siehe Crashevent 1) |
| CRASH_EVENT_3_DELTAVYR | char | CrashEvent 3 DeltaVyr (Beschreibung siehe Crashevent 1) |
| CRASH_EVENT_3_DELTAVYC | char | CrashEvent 3 DeltaVyc (Beschreibung siehe Crashevent 1) |
| CRASH_EVENT_3_CLIPPING | char | CrashEvent 3 Clipping (Beschreibung siehe Crashevent 1) |
| CHECKSUM | char | Checksumme Checksumme 0x00 bedeutet, dass die Checksumme vom SG befuellt wird. Bei allen anderen Werten wird der jeweils eingegebene Wert uebernommen. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (137 × 2)
- [FARTTEXTE](#table-farttexte) (35 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (7 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (12 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (237 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [LIEFERANTENLIN](#table-lieferantenlin) (198 × 2)
- [IARTTEXTE](#table-iarttexte) (35 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [FORTTEXTE](#table-forttexte) (685 × 4)
- [IORTTEXTE](#table-iorttexte) (411 × 4)
- [IUMWELTTEXTE](#table-iumwelttexte) (8 × 9)
- [SG_FUNKTIONEN](#table-sg-funktionen) (2 × 16)
- [FUMWELTTEXTE](#table-fumwelttexte) (8 × 9)
- [T_TAB_DTC_DEBUG_INFO_LOESCHEN_DOP](#table-t-tab-dtc-debug-info-loeschen-dop) (3 × 2)
- [T_TAB_DTC_DEBUG_INFO_LESEN_DOP](#table-t-tab-dtc-debug-info-lesen-dop) (3 × 2)
- [T_TAB_DIAGNOSEART_AENDERN_DOP](#table-t-tab-diagnoseart-aendern-dop) (2 × 2)
- [T_CD_DOP](#table-t-cd-dop) (24 × 2)
- [RES_0X1720](#table-res-0x1720) (4 × 10)
- [T_TAB_FAHRTRICHTUNG](#table-t-tab-fahrtrichtung) (7 × 2)
- [T_TAB_AACN](#table-t-tab-aacn) (4 × 2)
- [T_TAB_INNENTEMPERATUR_SG_DOP_UW](#table-t-tab-innentemperatur-sg-dop-uw) (203 × 2)
- [T_TAB_CAF_NR_DOP](#table-t-tab-caf-nr-dop) (3 × 2)
- [T_TAB_BAUREIHENKENNUNG](#table-t-tab-baureihenkennung) (31 × 2)
- [T_TAB_EDR_PUBLIC_DATA_LESEN_DOP](#table-t-tab-edr-public-data-lesen-dop) (5 × 2)
- [T_TAB_WOCHENTAG_STRUCTURE_DOP](#table-t-tab-wochentag-structure-dop) (8 × 2)
- [T_TAB_SG_TEMP_ZUSTAND](#table-t-tab-sg-temp-zustand) (3 × 2)
- [T_TAB_NEAR_CRASH_DATEN_LESEN_DOP](#table-t-tab-near-crash-daten-lesen-dop) (2 × 2)

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

Dimensions: 137 rows × 2 columns

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
| 0x0000AA | ArvinMeritor |
| 0x0000AB | Kongsberg Automotive GmbH |
| 0x0000AC | SMR Automotive Mirrors |
| 0x0000AD | So.Ge.Mi. |
| 0x0000AE | MTA |
| 0x0000AF | Alfmeier |
| 0x0000B0 | ELTEK VALERE DEUTSCHLAND GMBH |
| 0x0000B1 | Omron Automotive Electronics Europe Group |
| 0x0000B2 | ASK |
| 0x0000B3 | CML Innovative Technologies GmbH & Co. KG |
| 0x0000B4 | APAG Elektronik AG |
| 0x0000B5 | Nexteer Automotive World Headquarters |
| 0x0000B6 | Hans Widmaier |
| 0x0000B7 | Robert Bosch Battery Systems GmbH |
| 0x0000B8 | KYOCERA Display Corporation |
| 0x0000B9 | MAGNA Powertrain AG & Co KG |
| 0x0000BA | BorgWarner |
| 0x0000BB | BMW - Fahrzeugsimulator |
| 0x0000BC | Benteler Duncan Plant |
| 0x0000BD | U-Shin |
| 0x0000BE | Schaeffler Technologies |
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

Dimensions: 12 rows × 3 columns

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
| 0x5F | ECUGDM | ECUGarageDiagnoseMode |
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 237 rows × 3 columns

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
| 0x3B80 | Elektrische Zusatzwasserpumpe | 1 |
| 0x3C00 | Batteriesensor LIN | - |
| 0x3D00 | Aktives Kühlklappensystem | 1 |
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
| 0x4700 | Nackenwärmer Bedienschalter | 1 |
| 0x4A00 | Fond-Klimaanlage | 1 |
| 0x4B00 | Elektrischer Klimakompressor | 1 |
| 0x4C00 | Klimabedienteil | 1 |
| 0x4D00 | Gebläseregler | 1 |
| 0x4E00 | Klappenmotor | 0 |
| 0x4F00 | Elektrischer Kältemittelverdichter eKMV | 1 |
| 0x4F80 | Elektrischer Zuheizer PTC | 1 |
| 0x4FC0 | Elektrischer Zuheizer 3. Sitzreihe | 1 |
| 0x6000 | Standheizung | 1 |
| 0x6100 | Wärmepumpe | 1 |
| 0x6200 | elektrischer Durchlaufheizer | 1 |
| 0x6300 | Ionisator | 1 |
| 0x6400 | Bedufter | 1 |
| 0x6500 | Sense-Touch-Modul links | 1 |
| 0x6600 | Sense-Touch-Modul rechts | 1 |
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
| 0x5780 | Fussgängerschutzsensor statisch | 0 |
| 0x5788 | Satellit C-Säule links Y | 0 |
| 0x5790 | Satellit C-Säule rechts Y | 0 |
| 0x5798 | Satellit Zentrale Körperschall | 0 |
| 0x57A0 | Kapazitive Insassen- Sensorik CIS | 1 |
| 0x57A8 | Sitzbelegungserkennung Beifahrer SBR | 1 |
| 0x57B0 | Fussgängerschutzsensor dynamisch 1 | 0 |
| 0x57B8 | Fussgängerschutzsensor dynamisch 2 | 0 |
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
| 0x5B00 | Zentralinstrument | 1 |
| 0x5B40 | CID | 1 |
| 0x5B80 | Fondmonitor links | 1 |
| 0x5BC0 | Fondmonitor rechts | 1 |
| 0x5C00 | Elektrische Lenksäulenverstellung ELSV | 1 |
| 0x5D00 | Hands-Off Detection HOD | 1 |
| 0x5E01 | Innenbeleuchtung Fußraum Fahrer vorne | 1 |
| 0x5E02 | Innenbeleuchtung Fußraum Fahrer hinten | 1 |
| 0x5E03 | Innenbeleuchtung Fußraum Beifahrer vorne | 1 |
| 0x5E04 | Innenbeleuchtung Fußraum Beifahrer hinten | 1 |
| 0x5E05 | Innenbeleuchtung Fahrertür vorne oben | 1 |
| 0x5E06 | Innenbeleuchtung Fahrertür vorne Mitte | 1 |
| 0x5E07 | Innenbeleuchtung Fahrertür vorne unten | 1 |
| 0x5E08 | Innenbeleuchtung Fahrertür vorne Kartentasche | 1 |
| 0x5E09 | Innenbeleuchtung Fahrertür hinten oben | 1 |
| 0x5E0A | Innenbeleuchtung Fahrertür hinten unten | 1 |
| 0x5E0B | Innenbeleuchtung Fahrertür hinten Kartentasche | 1 |
| 0x5E0C | Innenbeleuchtung Beifahrertür vorne oben | 1 |
| 0x5E0D | Innenbeleuchtung Beifahrertür vorne Mitte | 1 |
| 0x5E0E | Innenbeleuchtung Beifahrertür vorne unten | 1 |
| 0x5E0F | Innenbeleuchtung Beifahrertür vorne Kartentasche | 1 |
| 0x5E10 | Innenbeleuchtung Beifahrertür hinten oben | 1 |
| 0x5E11 | Innenbeleuchtung Beifahrertür hinten unten | 1 |
| 0x5E12 | Innenbeleuchtung Beifahrertür hinten Kartentasche | 1 |
| 0x5E13 | Innenbeleuchtung I-Tafel Fahrer oben | 1 |
| 0x5E14 | Innenbeleuchtung I-Tafel Fahrer unten | 1 |
| 0x5E15 | Innenbeleuchtung I-Tafel oben Mitte | 1 |
| 0x5E16 | Innenbeleuchtung I-Tafel unten Mitte | 1 |
| 0x5E17 | Innenbeleuchtung I-Tafel oben Beifahrer | 1 |
| 0x5E18 | Innenbeleuchtung I-Tafel unten Beifahrer | 1 |
| 0x5E19 | Innenbeleuchtung B-Säule Fahrer | 1 |
| 0x5E1A | Innenbeleuchtung B-Säule Beifahrer | 1 |
| 0x5E1B | Innenbeleuchtung Lehne Fahrersitz | 1 |
| 0x5E1C | Innenbeleuchtung Lehne Beifahrersitz | 1 |
| 0x5E1D | Innenbeleuchtung Centerstack | 1 |
| 0x5E1E | Innenbeleuchtung Mittelkonsole Ablagefach | 1 |
| 0x5E1F | Innenbeleuchtung Gangwahlschalter links | 1 |
| 0x5E20 | Innenbeleuchtung Gangwahlschalter rechts | 1 |
| 0x5E80 | Stromverteiler hinten | 1 |
| 0x5EA0 | Wireless Charging Ablage | - |
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
| 0x7700 | Booster | - |
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-lieferantenlin"></a>
### LIEFERANTENLIN

Dimensions: 198 rows × 2 columns

| LIEF_NR | LIEF_TEXT |
| --- | --- |
| 0x0001 | Audi |
| 0x0002 | BMW |
| 0x0003 | Daimler AG |
| 0x0004 | Motorola |
| 0x0005 | VCT/Mentor Graphics |
| 0x0006 | VW (VW-Group) |
| 0x0007 | Volvo Cars (Ford Group) |
| 0x000B | Freescale Semiconductor |
| 0x0011 | NXP Semiconductors |
| 0x0012 | ST Microelectronics |
| 0x0013 | Melexis GmbH |
| 0x0014 | Microchip Technology Inc |
| 0x0015 | Centro Ricerche FIAT |
| 0x0016 | Renesas Technology Europe GmbH - Mitsubishi |
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
| 0x0028 | Renesas Technology Europe Ltd  - Hitachi |
| 0x0029 | Yazaki Europe Ltd |
| 0x002A | Trinamic Microchips GmbH |
| 0x002B | Allegro Microsystems, Inc |
| 0x002C | Toyota Motor Engineering and Manufacturing Europe N.V / S.A |
| 0x002D | PSA Peugeot Citroën |
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
| 0x005B | VOLVO Technology Schweden |
| 0x005C | SMSC Europe GmbH |
| 0x0060 | Sitronic GmbH & Co. KG |
| 0x0061 | Flextronics / Sidler Automotive GmbH & Co. KG |
| 0x0062 | EAO Automotive GmbH & Co. KG |
| 0x0063 | helag-electronic gmbh |
| 0x0064 | Magna Electronics |
| 0x0065 | INTEVA Products, LLC |
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
| 0x007B | Bury GmbH & Co. KG |
| 0x007A | Kromberg & Schubert GmbH & Co. KG |
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
| 0x013A | ISSI – Integrated Silicon Solution Inc |
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

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 6 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | Allgemeiner Fertigungs- und Energiesparmode | Hier deaktivierte Funktionen gemäß FeTra-Liste festhalten |
| 0x01 | Spezieller Energiesparmode | - |
| 0x02 | ECOS-Mode | - |
| 0x03 | MOST-Mode | - |
| 0x04 | Rollenmode | - |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | ja |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |
| F_HLZ_VIEW | ja |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | ja |
| F_SEVERITY | nein |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 685 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERSETZBEDINGUNGEN |
| --- | --- | --- | --- |
| 0x020100 | Energiesparmode aktiv | 0 | ZP |
| 0xC94401 | FA-CAN Physikalischer Busfehler | 0 | ZP |
| 0xC94402 | FA-CAN Kommunikationsfehler | 0 | ZP |
| 0xC94403 | FA-CAN high - Unterbrechung | 0 | ZP |
| 0xC94404 | FA-CAN high - Kurzschluss nach Minus | 0 | ZP |
| 0xC94405 | FA-CAN high - Kurzschluss nach Plus | 0 | ZP |
| 0xC94406 | FA-CAN low - Unterbrechung | 0 | ZP |
| 0xC94407 | FA-CAN low - Kurzschluss nach Minus | 0 | ZP |
| 0xC94408 | FA-CAN low - Kurzschluss nach Plus | 0 | ZP |
| 0xC94409 | FA-CAN low - Kurzschluss beider CAN-Leitungen | 0 | ZP |
| 0xC9440A | FA-CAN - Control Module Bus OFF | 0 | ZP |
| 0xC94BFF | Dummy-Fehlerspeichereintrag im Netzwerkfehlerbereich nur fuer Testzwecke | 1 | - |
| 0xC94D1E | LIN-Bus Sitzbelegungserkennung Fahrerseite: Kommunikationsfehler | 0 | ZP |
| 0xC94D1F | LIN-Bus Sitzbelegungserkennung Beifahrerseite: Kommunikationsfehler | 0 | ZP |
| 0xC94D20 | LIN-Bus Sitzbelegungserkennung hinten links: Kommunikationsfehler | 0 | ZP |
| 0xC94D21 | LIN-Bus Sitzbelegungserkennung hinten rechts: Kommunikationsfehler | 0 | ZP |
| 0xC94D22 | LIN-Bus Timeout verursacht durch einen Hardwarefehler | 0 | ZP |
| 0xC94D23 | LIN_S: Bus Error Slave6 | 0 | ZP |
| 0xC94D24 | LIN_S: Bus Error Slave 7 | 0 | ZP |
| 0xC94D25 | LIN_S: Bus Error Slave 8 | 0 | ZP |
| 0xC94D26 | LIN_S: Bus Error Slave 9 | 0 | ZP |
| 0xC94D27 | LIN_S: Bus Error Slave 10 | 0 | ZP |
| 0xC94D28 | LIN_S: Bus Error Slave 11 | 0 | ZP |
| 0xC94D29 | LIN_S: Bus Error Slave 12 | 0 | ZP |
| 0xC94D2A | LIN_S: Bus Error Slave 13 | 0 | ZP |
| 0xC94D2B | LIN_S: Bus Error Slave 14 | 0 | ZP |
| 0xC94D2C | LIN_S: Bus Error Slave 15 | 0 | ZP |
| 0xC94D2D | LIN_S: Bus Error Slave 16 | 0 | ZP |
| 0xC94D2E | LIN_S: Bus Error Slave 17 | 0 | ZP |
| 0xC94D2F | LIN_S: Bus Error Slave 18 | 0 | ZP |
| 0xC94D30 | LIN_S: Bus Error Slave 19 | 0 | ZP |
| 0xC94D31 | LIN_S: Bus Error Slave 20 | 0 | ZP |
| 0xC94D32 | LIN_S: Bus Error Slave 21 | 0 | ZP |
| 0xC94D33 | LIN_S: Bus Error Slave 22 | 0 | ZP |
| 0xC94D34 | LIN_S: Bus Error Slave 23 | 0 | ZP |
| 0xC94D35 | LIN_S: Bus Error Slave 24 | 0 | ZP |
| 0xC94D36 | LIN_S: Bus Error Slave 25 | 0 | ZP |
| 0xC94D37 | LIN_S: Bus Error Slave 26 | 0 | ZP |
| 0xC94D38 | LIN_S: Bus Error Slave 27 | 0 | ZP |
| 0xC94D39 | LIN_S: Bus Error Slave 28 | 0 | ZP |
| 0xC94D3A | LIN_S: Bus Error Slave 29 | 0 | ZP |
| 0xC94D3B | LIN_S: Bus Error Slave 30 | 0 | ZP |
| 0xC94D3C | LIN_S: Bus Error Slave 31 | 0 | ZP |
| 0xC94D3D | LIN_S: Bus Error Slave 32 | 0 | ZP |
| 0xC95400 | Ueberfallschalter: Modul sendet nicht | 1 | ZP |
| 0xC95401 | Ueberfallschalter: Kommunikationsstoerung | 1 | ZP |
| 0xC95403 | LCD Leuchtdichte: Modul sendet nicht | 1 | ZP |
| 0xC95404 | LCD Leuchtdichte: Alive-Signal-Fehler | 1 | ZP |
| 0xC95405 | Geschwindigkeit: Modul sendet nicht | 1 | ZP |
| 0xC95406 | Geschwindigkeit: Kommunikationsstoerung | 1 | ZP |
| 0xC95407 | Geschwindigkeit: Pruefsummenfehler | 1 | ZP |
| 0xC95409 | Sitzmodul Fahrer (Sitzmemory): Modul sendet nicht | 1 | ZP |
| 0xC9540A | Sitzmodul Fahrer (Sitzmemory): Kommunikationsstoerung | 1 | ZP |
| 0xC9540B | Sitzmodul Beifahrer (Sitzmemory): Modul sendet nicht | 1 | ZP |
| 0xC9540C | Sitzmodul Beifahrer (Sitzmemory): Kommunikationsstoerung | 1 | ZP |
| 0xC95417 | (Fahrzeugzustand, 0x3A0) fehlt, Empfaenger ACSM (FA-CAN), Sender JBE (K-CAN2) | 1 | ZP |
| 0xC95418 | DME: Modul sendet nicht | 1 | ZP |
| 0xC95419 | DME: Modul Kommunikationsstörung | 1 | ZP |
| 0xC95420 | DME: Signal Gangwahl Antrieb oder Signal Antrieb Fahrzeug ungueltig | 1 | ZP |
| 0xC95421 | ICM: Lenkwinkel Vorderachse effektiv - Modul sendet nicht | 1 | ZP |
| 0xC95422 | ICM: Modul Kommunikationsstörung - Nachricht Lenkwinkel Vorderachse effektiv | 1 | ZP |
| 0xC95423 | ICM: Lenkwinkel Vorderachse effektiv - Signal ungültig | 1 | ZP |
| 0xC95424 | ICM: Fahrzeug Dynamik Daten geschaetzt - Modul sendet nicht | 1 | ST |
| 0xC95425 | ICM: Modul Kommunikationsstörung - Nachricht Fahrzeug Dynamik Daten geschätzt | 1 | ZP |
| 0xC95426 | ICM: Schwimmwinkel - Signal ungueltig | 1 | ZP |
| 0xC95428 | Geschwindigkeit : Modul fuer Geschwindigkeit - sendet nicht | 1 | ZP |
| 0xC95429 | Geschwindigkeit Fahrzeug - Kommunikationsstoerung / Alive-Fehler | 1 | ZP |
| 0xC9542A | Geschwindigkeit Fahrzeug - Pruefsummenfehler | 1 | ZP |
| 0xC9542C | Geschwindigkeit Fahrzeug - Signal ungueltig | 1 | ZP |
| 0xC9542D | Geschwindigkeit Fahrzeug - Signal ungueltig | 1 | ZP |
| 0xC9542E | LCD-Helligkeit-Regelung - Signal ungueltig | 1 | ZP |
| 0xC9542F | Status Ueberfallfunktion - Signal ungueltig | 1 | ZP |
| 0xC95430 | Sitzmodul Fahrer (Sitzmemory), (Sitzlehnenverriegelung), Nachricht Status Sitzlehnenverriegelung: Signal ungueltig | 1 | ZP |
| 0xC95431 | Sitzmodul Beifahrer (Sitzmemory), (Sitzlehnenverriegelung), Nachricht Status Sitzlehnenverriegelung: Signal ungueltig | 1 | ZP |
| 0xC95432 | Sitzmodul Fahrer (Sitzmemory), (Sitzlehnenverriegelung), Nachricht Status Sitzlehnenverriegelung: Fehler Normierung | 1 | ZP |
| 0xC95433 | Sitzmodul Beifahrer (Sitzmemory), (Sitzlehnenverriegelung), Nachricht Status Sitzlehnenverriegelung: Fehler Normierung | 1 | ZP |
| 0x02FF01 | Dummy-Fehlerspeichereintrag im Komponentenfehlerbereich nur für Testzwecke | 1 | Debug |
| 0x930900 | Airbag Fahrer 1. Stufe: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930901 | Airbag Fahrer 1. Stufe: Kurzschluss nach Minus | 0 | ZP |
| 0x930902 | Airbag Fahrer 1. Stufe: Kurzschluss nach Plus | 0 | ZP |
| 0x930903 | Airbag Fahrer 1. Stufe: Widerstand zu klein | 0 | ZP |
| 0x930904 | Airbag Fahrer 1. Stufe: Widerstand zu groß | 0 | ZP |
| 0x930905 | Airbag Fahrer 1. Stufe: Leitung verkoppelt | 0 | ST |
| 0x930906 | Airbag Fahrer 2. Stufe: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930907 | Airbag Fahrer 2. Stufe: Kurzschluss nach Minus | 0 | ZP |
| 0x930908 | Airbag Fahrer 2. Stufe: Kurzschluss nach Plus | 0 | ZP |
| 0x930909 | Airbag Fahrer 2. Stufe: Widerstand zu klein | 0 | ZP |
| 0x93090A | Airbag Fahrer 2. Stufe: Widerstand zu groß | 0 | ZP |
| 0x93090B | Airbag Fahrer 2. Stufe: Leitung verkoppelt | 0 | ST |
| 0x93090C | Airbag Fahrer Ventil: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x93090D | Airbag Fahrer Ventil: Kurzschluss nach Minus | 0 | ZP |
| 0x93090E | Airbag Fahrer Ventil: Kurzschluss nach Plus | 0 | ZP |
| 0x93090F | Airbag Fahrer Ventil: Widerstand zu klein | 0 | ZP |
| 0x930910 | Airbag Fahrer Ventil: Widerstand zu groß | 0 | ZP |
| 0x930911 | Airbag Fahrer Ventil: Leitung verkoppelt | 0 | ST |
| 0x930912 | Airbag Beifahrer 1. Stufe: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930913 | Airbag Beifahrer 1. Stufe: Kurzschluss nach Minus | 0 | ZP |
| 0x930914 | Airbag Beifahrer 1. Stufe: Kurzschluss nach Plus | 0 | ZP |
| 0x930915 | Airbag Beifahrer 1. Stufe: Widerstand zu klein | 0 | ZP |
| 0x930916 | Airbag Beifahrer 1. Stufe: Widerstand zu groß | 0 | ZP |
| 0x930917 | Airbag Beifahrer 1. Stufe: Leitung verkoppelt | 0 | ST |
| 0x930918 | Airbag Beifahrer 2. Stufe: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930919 | Airbag Beifahrer 2. Stufe: Kurzschluss nach Minus | 0 | ZP |
| 0x93091A | Airbag Beifahrer 2. Stufe: Kurzschluss nach Plus | 0 | ZP |
| 0x93091B | Airbag Beifahrer 2. Stufe: Widerstand zu klein | 0 | ZP |
| 0x93091C | Airbag Beifahrer 2. Stufe: Widerstand zu groß | 0 | ZP |
| 0x93091D | Airbag Beifahrer 2. Stufe: Leitung verkoppelt | 0 | ST |
| 0x93091E | Airbag Beifahrer Ventil: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x93091F | Airbag Beifahrer Ventil: Kurzschluss nach Minus | 0 | ZP |
| 0x930920 | Airbag Beifahrer Ventil: Kurzschluss nach Plus | 0 | ZP |
| 0x930921 | Airbag Beifahrer Ventil: Widerstand zu klein | 0 | ZP |
| 0x930922 | Airbag Beifahrer Ventil: Widerstand zu groß | 0 | ZP |
| 0x930923 | Airbag Beifahrer Ventil: Leitung verkoppelt | 0 | ST |
| 0x930924 | Gurtstrammer Fahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930925 | Gurtstrammer Fahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x930926 | Gurtstrammer Fahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x930927 | Gurtstrammer Fahrer: Widerstand zu klein | 0 | ZP |
| 0x930928 | Gurtstrammer Fahrer: Widerstand zu groß | 0 | ZP |
| 0x930929 | Gurtstrammer Fahrer: Leitung verkoppelt | 0 | ST |
| 0x93092A | Endbeschlagstrammer Fahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x93092B | Endbeschlagstrammer Fahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x93092C | Endbeschlagstrammer Fahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x93092D | Endbeschlagstrammer Fahrer: Widerstand zu klein | 0 | ZP |
| 0x93092E | Endbeschlagstrammer Fahrer: Widerstand zu groß | 0 | ZP |
| 0x93092F | Endbeschlagstrammer Fahrer: Leitung verkoppelt | 0 | ST |
| 0x930930 | Gurtkraftbegrenzer Fahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930931 | Gurtkraftbegrenzer Fahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x930932 | Gurtkraftbegrenzer Fahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x930933 | Gurtkraftbegrenzer Fahrer: Widerstand zu klein | 0 | ZP |
| 0x930934 | Gurtkraftbegrenzer Fahrer: Widerstand zu groß | 0 | ZP |
| 0x930935 | Gurtkraftbegrenzer Fahrer: Leitung verkoppelt | 0 | ST |
| 0x930936 | Gurtstrammer Beifahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930937 | Gurtstrammer Beifahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x930938 | Gurtstrammer Beifahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x930939 | Gurtstrammer Beifahrer: Widerstand zu klein | 0 | ZP |
| 0x93093A | Gurtstrammer Beifahrer: Widerstand zu groß | 0 | ZP |
| 0x93093B | Gurtstrammer Beifahrer: Leitung verkoppelt | 0 | ST |
| 0x93093C | Endbeschlagstrammer Beifahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x93093D | Endbeschlagstrammer Beifahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x93093E | Endbeschlagstrammer Beifahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x93093F | Endbeschlagstrammer Beifahrer: Widerstand zu klein | 0 | ZP |
| 0x930940 | Endbeschlagstrammer Beifahrer: Widerstand zu groß | 0 | ZP |
| 0x930941 | Endbeschlagstrammer Beifahrer: Leitung verkoppelt | 0 | ST |
| 0x930942 | Gurtkraftbegrenzer Beifahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930943 | Gurtkraftbegrenzer Beifahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x930944 | Gurtkraftbegrenzer Beifahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x930945 | Gurtkraftbegrenzer Beifahrer: Widerstand zu klein | 0 | ZP |
| 0x930946 | Gurtkraftbegrenzer Beifahrer: Widerstand zu groß | 0 | ZP |
| 0x930947 | Gurtkraftbegrenzer Beifahrer: Leitung verkoppelt | 0 | ST |
| 0x930948 | Knieairbag Fahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930949 | Knieairbag Fahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x93094A | Knieairbag Fahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x93094B | Knieairbag Fahrer: Widerstand zu klein | 0 | ZP |
| 0x93094C | Knieairbag Fahrer: Widerstand zu groß | 0 | ZP |
| 0x93094D | Knieairbag Fahrer: Leitung verkoppelt | 0 | ST |
| 0x93094E | Knieairbag Beifahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x93094F | Knieairbag Beifahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x930950 | Knieairbag Beifahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x930951 | Knieairbag Beifahrer: Widerstand zu klein | 0 | ZP |
| 0x930952 | Knieairbag Beifahrer: Widerstand zu groß | 0 | ZP |
| 0x930953 | Knieairbag Beifahrer: Leitung verkoppelt | 0 | ST |
| 0x930954 | Aktive Kopfstuetze Fahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930955 | Aktive Kopfstuetze Fahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x930956 | Aktive Kopfstuetze Fahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x930957 | Aktive Kopfstuetze Fahrer: Widerstand zu klein | 0 | ZP |
| 0x930958 | Aktive Kopfstuetze Fahrer: Widerstand zu groß | 0 | ZP |
| 0x930959 | Aktive Kopfstuetze Fahrer: Leitung verkoppelt | 0 | ST |
| 0x93095A | Aktive Kopfstuetze Beifahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x93095B | Aktive Kopfstuetze Beifahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x93095C | Aktive Kopfstuetze Beifahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x93095D | Aktive Kopfstuetze Beifahrer: Widerstand zu klein | 0 | ZP |
| 0x93095E | Aktive Kopfstuetze Beifahrer: Widerstand zu groß | 0 | ZP |
| 0x93095F | Aktive Kopfstuetze Beifahrer: Leitung verkoppelt | 0 | ST |
| 0x930960 | Gurtstrammer hinten links: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930961 | Gurtstrammer hinten links: Kurzschluss nach Minus | 0 | ZP |
| 0x930962 | Gurtstrammer hinten links: Kurzschluss nach Plus | 0 | ZP |
| 0x930963 | Gurtstrammer hinten links: Widerstand zu klein | 0 | ZP |
| 0x930964 | Gurtstrammer hinten links: Widerstand zu groß | 0 | ZP |
| 0x930965 | Gurtstrammer hinten links: Leitung verkoppelt | 0 | ST |
| 0x930966 | Gurtstrammer hinten rechts: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930967 | Gurtstrammer hinten rechts: Kurzschluss nach Minus | 0 | ZP |
| 0x930968 | Gurtstrammer hinten rechts: Kurzschluss nach Plus | 0 | ZP |
| 0x930969 | Gurtstrammer hinten rechts: Widerstand zu klein | 0 | ZP |
| 0x93096A | Gurtstrammer hinten rechts: Widerstand zu groß | 0 | ZP |
| 0x93096B | Gurtstrammer hinten rechts: Leitung verkoppelt | 0 | ST |
| 0x93096C | Seitenairbag Fahrer Ventil: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x93096D | Seitenairbag Fahrer Ventil: Kurzschluss nach Minus | 0 | ZP |
| 0x93096E | Seitenairbag Fahrer Ventil: Kurzschluss nach Plus | 0 | ZP |
| 0x93096F | Seitenairbag Fahrer Ventil: Widerstand zu klein | 0 | ZP |
| 0x930970 | Seitenairbag Fahrer Ventil: Widerstand zu groß | 0 | ZP |
| 0x930971 | Seitenairbag Fahrer Ventil: Leitung verkoppelt | 0 | ST |
| 0x930972 | Seitenairbag Beifahrer Ventil: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930973 | Seitenairbag Beifahrer Ventil: Kurzschluss nach Minus | 0 | ZP |
| 0x930974 | Seitenairbag Beifahrer Ventil: Kurzschluss nach Plus | 0 | ZP |
| 0x930975 | Seitenairbag Beifahrer Ventil: Widerstand zu klein | 0 | ZP |
| 0x930976 | Seitenairbag Beifahrer Ventil: Widerstand zu groß | 0 | ZP |
| 0x930977 | Seitenairbag Beifahrer Ventil: Leitung verkoppelt | 0 | ST |
| 0x930978 | Seitenairbag Fahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930979 | Seitenairbag Fahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x93097A | Seitenairbag Fahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x93097B | Seitenairbag Fahrer: Widerstand zu klein | 0 | ZP |
| 0x93097C | Seitenairbag Fahrer: Widerstand zu groß | 0 | ZP |
| 0x93097D | Seitenairbag Fahrer: Leitung verkoppelt | 0 | ST |
| 0x93097E | Seitenairbag Beifahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x93097F | Seitenairbag Beifahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x930980 | Seitenairbag Beifahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x930981 | Seitenairbag Beifahrer: Widerstand zu klein | 0 | ZP |
| 0x930982 | Seitenairbag Beifahrer: Widerstand zu groß | 0 | ZP |
| 0x930983 | Seitenairbag Beifahrer: Leitung verkoppelt | 0 | ST |
| 0x930984 | Kopfairbag links: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930985 | Kopfairbag links: Kurzschluss nach Minus | 0 | ZP |
| 0x930986 | Kopfairbag links: Kurzschluss nach Plus | 0 | ZP |
| 0x930987 | Kopfairbag links: Widerstand zu klein | 0 | ZP |
| 0x930988 | Kopfairbag links: Widerstand zu groß | 0 | ZP |
| 0x930989 | Kopfairbag links: Leitung verkoppelt | 0 | ST |
| 0x93098A | Kopfairbag rechts: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x93098B | Kopfairbag rechts: Kurzschluss nach Minus | 0 | ZP |
| 0x93098C | Kopfairbag rechts: Kurzschluss nach Plus | 0 | ZP |
| 0x93098D | Kopfairbag rechts: Widerstand zu klein | 0 | ZP |
| 0x93098E | Kopfairbag rechts: Widerstand zu groß | 0 | ZP |
| 0x93098F | Kopfairbag rechts: Leitung verkoppelt | 0 | ST |
| 0x930990 | Sicherheitsbatterieklemme: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930991 | Sicherheitsbatterieklemme: Kurzschluss nach Minus | 0 | ZP |
| 0x930992 | Sicherheitsbatterieklemme: Kurzschluss nach Plus | 0 | ZP |
| 0x930993 | Sicherheitsbatterieklemme: Widerstand zu klein | 0 | ZP |
| 0x930994 | Sicherheitsbatterieklemme: Widerstand zu groß | 0 | ZP |
| 0x930995 | Sicherheitsbatterieklemme: Leitung verkoppelt | 0 | ST |
| 0x930996 | Sicherheitsbatterieklemme 2: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930997 | Sicherheitsbatterieklemme 2: Kurzschluss nach Minus | 0 | ZP |
| 0x930998 | Sicherheitsbatterieklemme 2: Kurzschluss nach Plus | 0 | ZP |
| 0x930999 | Sicherheitsbatterieklemme 2: Widerstand zu klein | 0 | ZP |
| 0x93099A | Sicherheitsbatterieklemme 2: Widerstand zu groß | 0 | ZP |
| 0x93099B | Sicherheitsbatterieklemme 2: Leitung verkoppelt | 0 | ST |
| 0x93099C | Sicherheitsbatterieklemme 3: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x93099D | Sicherheitsbatterieklemme 3: Kurzschluss nach Minus | 0 | ZP |
| 0x93099E | Sicherheitsbatterieklemme 3: Kurzschluss nach Plus | 0 | ZP |
| 0x93099F | Sicherheitsbatterieklemme 3: Widerstand zu klein | 0 | ZP |
| 0x9309A0 | Sicherheitsbatterieklemme 3: Widerstand zu groß | 0 | ZP |
| 0x9309A1 | Sicherheitsbatterieklemme 3: Leitung verkoppelt | 0 | ST |
| 0x9309A8 | Fussgaengerschutzsystem vorn links: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x9309A9 | Fussgaengerschutzsystem vorn links: Kurzschluss nach Minus | 0 | ZP |
| 0x9309AA | Fussgaengerschutzsystem vorn links: Kurzschluss nach Plus | 0 | ZP |
| 0x9309AB | Fussgaengerschutzsystem vorn links: Widerstand zu klein | 0 | ZP |
| 0x9309AC | Fussgaengerschutzsystem vorn links: Widerstand zu groß | 0 | ZP |
| 0x9309AD | Fussgaengerschutzsystem vorn links: Leitung verkoppelt | 0 | ST |
| 0x9309AE | Fussgaengerschutzsystem vorn rechts: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x9309AF | Fussgaengerschutzsystem vorn rechts: Kurzschluss nach Minus | 0 | ZP |
| 0x9309B0 | Fussgaengerschutzsystem vorn rechts: Kurzschluss nach Plus | 0 | ZP |
| 0x9309B1 | Fussgaengerschutzsystem vorn rechts: Widerstand zu klein | 0 | ZP |
| 0x9309B2 | Fussgaengerschutzsystem vorn rechts: Widerstand zu groß | 0 | ZP |
| 0x9309B3 | Fussgaengerschutzsystem vorn rechts: Leitung verkoppelt | 0 | ST |
| 0x9309B4 | Fussgaengerschutzsystem hinten links: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x9309B5 | Fussgaengerschutzsystem hinten links: Kurzschluss nach Minus | 0 | ZP |
| 0x9309B6 | Fussgaengerschutzsystem hinten links: Kurzschluss nach Plus | 0 | ZP |
| 0x9309B7 | Fussgaengerschutzsystem hinten links: Widerstand zu klein | 0 | ZP |
| 0x9309B8 | Fussgaengerschutzsystem hinten links: Widerstand zu groß | 0 | ZP |
| 0x9309B9 | Fussgaengerschutzsystem hinten links: Leitung verkoppelt | 0 | ST |
| 0x9309BA | Fussgaengerschutzsystem hinten rechts: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x9309BB | Fussgaengerschutzsystem hinten rechts: Kurzschluss nach Minus | 0 | ZP |
| 0x9309BC | Fussgaengerschutzsystem hinten rechts: Kurzschluss nach Plus | 0 | ZP |
| 0x9309BD | Fussgaengerschutzsystem hinten rechts: Widerstand zu klein | 0 | ZP |
| 0x9309BE | Fussgaengerschutzsystem hinten rechts: Widerstand zu groß | 0 | ZP |
| 0x9309BF | Fussgaengerschutzsystem hinten rechts: Leitung verkoppelt | 0 | ST |
| 0x9309C0 | Gurtschlosskontakt Fahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x9309C1 | Gurtschlosskontakt Fahrer: Messwert außerhalb des gültigen Bereiches | 0 | ZP |
| 0x9309C2 | Gurtschlosskontakt Fahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x9309C3 | Gurtschlosskontakt Fahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x9309C4 | Gurtschlosskontakt Fahrer: Unterbrechung | 0 | ZP |
| 0x9309C5 | Gurtschlosskontakt Fahrer: Leitung verkoppelt | 0 | ST |
| 0x9309C6 | Gurtschlosskontakt Beifahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x9309C7 | Gurtschlosskontakt Beifahrer: Messwert außerhalb des gültigen Bereiches | 0 | ZP |
| 0x9309C8 | Gurtschlosskontakt Beifahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x9309C9 | Gurtschlosskontakt Beifahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x9309CA | Gurtschlosskontakt Beifahrer: Unterbrechung | 0 | ZP |
| 0x9309CB | Gurtschlosskontakt Beifahrer: Leitung verkoppelt | 0 | ST |
| 0x9309CC | Gurtschlosskontakt hinten links: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x9309CD | Gurtschlosskontakt hinten links: Messwert außerhalb des gültigen Bereiches | 0 | ZP |
| 0x9309CE | Gurtschlosskontakt hinten links: Kurzschluss nach Minus | 0 | ZP |
| 0x9309CF | Gurtschlosskontakt hinten links: Kurzschluss nach Plus | 0 | ZP |
| 0x9309D0 | Gurtschlosskontakt hinten links: Unterbrechung | 0 | ZP |
| 0x9309D1 | Gurtschlosskontakt hinten links: Leitung verkoppelt | 0 | ST |
| 0x9309D2 | Gurtschlosskontakt hinten rechts: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x9309D3 | Gurtschlosskontakt hinten rechts: Messwert außerhalb des gültigen Bereiches | 0 | ZP |
| 0x9309D4 | Gurtschlosskontakt hinten rechts: Kurzschluss nach Minus | 0 | ZP |
| 0x9309D5 | Gurtschlosskontakt hinten rechts: Kurzschluss nach Plus | 0 | ZP |
| 0x9309D6 | Gurtschlosskontakt hinten rechts: Unterbrechung | 0 | ZP |
| 0x9309D7 | Gurtschlosskontakt hinten rechts: Leitung verkoppelt | 0 | ST |
| 0x9309D8 | Gurtschlosskontakt hinten mitte: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x9309D9 | Gurtschlosskontakt hinten mitte: Messwert außerhalb des gültigen Bereiches | 0 | ZP |
| 0x9309DA | Gurtschlosskontakt hinten mitte: Kurzschluss nach Minus | 0 | ZP |
| 0x9309DB | Gurtschlosskontakt hinten mitte: Kurzschluss nach Plus | 0 | ZP |
| 0x9309DC | Gurtschlosskontakt hinten mitte: Unterbrechung | 0 | ZP |
| 0x9309DD | Gurtschlosskontakt hinten mitte: Leitung verkoppelt | 0 | ST |
| 0x9309DE | POS: Schalter fuer Beifahrerairbag-Abschaltung: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x9309DF | POS: Schalter fuer Beifahrerairbag-Abschaltung: Messwert außerhalb des gültigen Bereiches | 0 | ZP |
| 0x9309E0 | POS: Schalter fuer Beifahrerairbag-Abschaltung: Kurzschluss nach Minus | 0 | ZP |
| 0x9309E1 | POS: Schalter fuer Beifahrerairbag-Abschaltung: Kurzschluss nach Plus | 0 | ZP |
| 0x9309E2 | POS: Schalter fuer Beifahrerairbag-Abschaltung: Unterbrechung | 0 | ZP |
| 0x9309E3 | POS: Schalter fuer Beifahrerairbag-Abschaltung :Leitung verkoppelt | 0 | ST |
| 0x9309E4 | Sitzpositionssensor Fahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x9309E5 | Sitzpositionssensor Fahrer: Messwert außerhalb des gültigen Bereiches | 0 | ZP |
| 0x9309E6 | Sitzpositionssensor Fahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x9309E7 | Sitzpositionssensor Fahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x9309E8 | Sitzpositionssensor Fahrer: Unterbrechung | 0 | ZP |
| 0x9309E9 | Sitzpositionssensor Fahrer: Leitung verkoppelt | 0 | ST |
| 0x9309ED | ODS-System: Sitzbelegungsmatte Beifahrer: noch nicht freigegeben | 0 | ZP |
| 0x9309F1 | SBR-Sensor: Sitzbelegungsmatte Beifahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x9309F2 | SBR-Sensor: Sitzbelegungsmatte Beifahrer: Kommunikationsstoerung | 0 | ZP |
| 0x9309F3 | SBR-Sensor: Sitzbelegungsmatte Beifahrer: sendet internen Fehler | 0 | ZP |
| 0x9309F4 | ODS-System: Sitzbelegungsmatte Beifahrer: konnte nicht freigegeben werden | 0 | ZP |
| 0x9309F5 | SBR-Sensor: Sitzbelegungsmatte Beifahrer: sendet Matte Unterbrechung | 0 | ZP |
| 0x9309F6 | SBR-Sensor: Sitzbelegungsmatte Beifahrer: sendet Matte Kurzschluss | 0 | ZP |
| 0x9309F7 | SBR-Sensor: Sitzbelegungsmatte Beifahrer: sendet nicht | 0 | ZP |
| 0x9309FB | Airbagfrontsensor links - Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930A02 | Airbagfrontsensor rechts - Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930A06 | ODS-System: Sitzbelegungsmatte Beifahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930A07 | ODS-System: Sitzbelegungsmatte Beifahrer: Signal ungueltig | 0 | ZP |
| 0x930A08 | ODS-System: Sitzbelegungsmatte Beifahrer: sendet Fehler Sensor Kurzschluss | 0 | ZP |
| 0x930A0A | Airbagsensor B-Saeule rechts (x-y-Richtung): Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930A0B | Airbagsensor Tür vorn links - Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930A0C | Airbagsensor Tür vorn rechts - Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930A0D | Zentralsensor (Gierrate) - Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930A0E | Zentralsensor  (x-y-Richtung) - Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930A0F | Zentralsensor (Gierrate) - Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930A10 | Fussgängerschutzsensor vorn links - Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930A11 | Fussgängerschutzsensor vorn Mitte - Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930A12 | ODS-System: Sitzbelegungsmatte Beifahrer: Modul sendet nicht | 0 | ST |
| 0x930A13 | ODS-System: Sitzbelegungsmatte Beifahrer: Datenspeicher voll | 0 | ZP |
| 0x930A14 | ODS-System: Sitzbelegungsmatte Beifahrer: Kommunikationsstoerung | 0 | ZP |
| 0x930A15 | Fussgängerschutzsensor vorn rechts - Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930A18 | SBR-Sensor: Sitzbelegungsmatte Beifahrer: Signal ungueltig | 0 | ZP |
| 0x930A1B | ODS-System: Sitzbelegungsmatte Beifahrer: sendet Fehler Sensor Unterbrechung | 0 | ZP |
| 0x930A1C | ODS-System: Sitzbelegungsmatte Beifahrer: sendet Sensorfehler wegen Feuchtigkeit | 0 | ZP |
| 0x930A1D | ODS-System: Sitzbelegungsmatte Beifahrer: sendet unplausible Messwerte | 0 | ZP |
| 0x930A1E | Airbagsensor B-Saeule links (x-y-Richtung) - Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930A21 | ODS-System: Sitzbelegungsmatte Beifahrer: sendet Fehler Masse Sitzpfanne | 0 | ZP |
| 0x930A22 | ODS-System: Sitzbelegungsmatte Beifahrer: sendet unplausible Messwerte Heizdraht | 0 | ZP |
| 0x930A23 | ODS-System: Sitzbelegungsmatte Beifahrer: sendet Fehler Freigabe fehlgeschlagen | 0 | ZP |
| 0x930A24 | UpFront: Airbagfrontsensor links: Sensortyp falsch | 0 | ST |
| 0x930A26 | UpFront: Airbagfrontsensor links: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930A27 | UpFront: Airbagfrontsensor links: sendet Fehler | 0 | ZP |
| 0x930A28 | UpFront: Airbagfrontsensor links: Kommunikationsstoerung | 0 | ZP |
| 0x930A2A | UpFront: Airbagfrontsensor links: Kurzschluss nach Minus | 0 | ZP |
| 0x930A2B | UpFront: Airbagfrontsensor links: Kurzschluss nach Plus | 0 | ZP |
| 0x930A2C | UpFront: Airbagfrontsensor links: Unterbrechung | 0 | ZP |
| 0x930A2E | UpFront: Airbagfrontsensor rechts: Sensortyp falsch | 0 | ST |
| 0x930A30 | UpFront: Airbagfrontsensor rechts: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930A31 | UpFront: Airbagfrontsensor rechts: sendet Fehler | 0 | ZP |
| 0x930A32 | UpFront: Airbagfrontsensor rechts: Kommunikationsstoerung | 0 | ZP |
| 0x930A34 | UpFront: Airbagfrontsensor rechts: Kurzschluss nach Minus | 0 | ZP |
| 0x930A35 | UpFront: Airbagfrontsensor rechts: Kurzschluss nach Plus | 0 | ZP |
| 0x930A36 | UpFront: Airbagfrontsensor rechts: Unterbrechung | 0 | ZP |
| 0x930A38 | Airbagsensor B-Saeule links (x-y-Richtung): Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930A39 | Airbagsensor B-Saeule links (x-y-Richtung): Kommunikationsstoerung | 0 | ZP |
| 0x930A3B | Airbagsensor B-Saeule links (x-y-Richtung): Kurzschluss nach Minus | 0 | ZP |
| 0x930A3C | Airbagsensor B-Saeule links (x-y-Richtung): Kurzschluss nach Plus | 0 | ZP |
| 0x930A3D | Airbagsensor B-Saeule links (x-y-Richtung): Unterbrechung | 0 | ZP |
| 0x930A3F | Airbagsensor B-Saeule links (x-Richtung): Sensortyp falsch | 0 | ST |
| 0x930A41 | Airbagsensor B-Saeule links (x-Richtung): sendet Fehler | 0 | ZP |
| 0x930A42 | Airbagsensor B-Saeule links (y-Richtung): Sensortyp falsch | 0 | ST |
| 0x930A44 | Airbagsensor B-Saeule links (y-Richtung): sendet Fehler | 0 | ZP |
| 0x930A45 | Airbagsensor B-Saeule rechts (x-y-Richtung): Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930A46 | Airbagsensor B-Saeule rechts (x-y-Richtung): Kommunikationsstoerung | 0 | ZP |
| 0x930A48 | Airbagsensor B-Saeule rechts (x-y-Richtung): Kurzschluss nach Minus | 0 | ZP |
| 0x930A49 | Airbagsensor B-Saeule rechts (x-y-Richtung): Kurzschluss nach Plus | 0 | ZP |
| 0x930A4A | Airbagsensor B-Saeule rechts (x-y-Richtung): Unterbrechung | 0 | ZP |
| 0x930A4C | Airbagsensor B-Saeule rechts (x-Richtung): Sensortyp falsch | 0 | ST |
| 0x930A4E | Airbagsensor B-Saeule rechts (x-Richtung): sendet Fehler | 0 | ZP |
| 0x930A4F | Airbagsensor B-Saeule rechts (y-Richtung): Sensortyp falsch | 0 | ST |
| 0x930A51 | Airbagsensor B-Saeule rechts (y-Richtung): sendet Fehler | 0 | ZP |
| 0x930A52 | Airbagsensor Tür vorn links: Sensortyp falsch | 0 | ST |
| 0x930A53 | Airbagsensor Tür vorn links: Druckwert ueber Grenzwert | 0 | ZP |
| 0x930A54 | Airbagsensor Tür vorn links: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930A55 | Airbagsensor Tür vorn links: sendet Fehler | 0 | ZP |
| 0x930A56 | Airbagsensor Tür vorn links: Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930A57 | Airbagsensor Tür vorn links: Kommunikationsstoerung | 0 | ZP |
| 0x930A59 | Airbagsensor Tür vorn links: Kurzschluss nach Minus | 0 | ZP |
| 0x930A5A | Airbagsensor Tür vorn links: Kurzschluss nach Plus | 0 | ZP |
| 0x930A5B | Airbagsensor Tür vorn links: Unterbrechung | 0 | ZP |
| 0x930A5C | Airbagsensor Tür vorn rechts: Sensortyp falsch | 0 | ST |
| 0x930A5D | Airbagsensor Tür vorn rechts: Druckwert ueber Grenzwert | 0 | ZP |
| 0x930A5E | Airbagsensor Tür vorn rechts: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930A5F | Airbagsensor Tür vorn rechts: sendet Fehler | 0 | ZP |
| 0x930A60 | ODS-System: Sitzbelegungsmatte Beifahrer: sendet Fehler Sitz nass | 0 | ZP |
| 0x930A61 | Airbagsensor Tür vorn rechts: Kommunikationsstoerung | 0 | ZP |
| 0x930A63 | Airbagsensor Tür vorn rechts: Kurzschluss nach Minus | 0 | ZP |
| 0x930A64 | Airbagsensor Tür vorn rechts: Kurzschluss nach Plus | 0 | ZP |
| 0x930A65 | Airbagsensor Tür vorn rechts: Unterbrechung | 0 | ZP |
| 0x930A66 | Airbagsensor-Cluster (high g x-y-Richtung): Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930A67 | Airbagsensor-Cluster (high g x-y-Richtung): Kommunikationsstoerung | 0 | ZP |
| 0x930A69 | Airbagsensor-Cluster (high g x-y-Richtung): Kurzschluss nach Minus | 0 | ZP |
| 0x930A6A | Airbagsensor-Cluster (high g x-y-Richtung): Kurzschluss nach Plus | 0 | ZP |
| 0x930A6B | Airbagsensor-Cluster (high g x-y-Richtung): Unterbrechung | 0 | ZP |
| 0x930A6D | Airbagsensor-Cluster (high g x-Richtung): Sensortyp falsch | 0 | ST |
| 0x930A6F | Airbagsensor-Cluster (high g x-Richtung): sendet Fehler | 0 | ZP |
| 0x930A70 | Airbagsensor-Cluster (high g y-Richtung): Sensortyp falsch | 0 | ST |
| 0x930A72 | Airbagsensor-Cluster (y-Richtung high g): sendet Fehler | 0 | ZP |
| 0x930A73 | Airbagsensor-Cluster (low g Drehrate): Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930A74 | Airbagsensor-Cluster (low g Drehrate): Kommunikationsstoerung | 0 | ZP |
| 0x930A76 | Airbagsensor-Cluster (low g Drehrate): Kurzschluss nach Minus | 0 | ZP |
| 0x930A77 | Airbagsensor-Cluster (low g Drehrate): Kurzschluss nach Plus | 0 | ZP |
| 0x930A78 | Airbagsensor-Cluster (low g Drehrate): Unterbrechung | 0 | ZP |
| 0x930A7A | Airbagsensor-Cluster (low g y-Richtung): Sensortyp falsch | 0 | ST |
| 0x930A7C | Airbagsensor-Cluster (low g y-Richtung): sendet Fehler | 0 | ZP |
| 0x930A7D | Airbagsensor-Cluster (low g z-Richtung): Sensortyp falsch | 0 | ST |
| 0x930A7F | Airbagsensor-Cluster (low g z-Richtung): sendet Fehler | 0 | ZP |
| 0x930A80 | Airbagsensor-Cluster (Drehsensor): Sensortyp falsch | 0 | ST |
| 0x930A82 | Airbagsensor-Cluster (Drehsensor): sendet Fehler | 0 | ZP |
| 0x930A84 | Fussgängerschutzsensor vorn links: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930A85 | Fussgängerschutzsensor vorn links: sendet Fehler | 0 | ZP |
| 0x930A86 | Fussgängerschutzsensor vorn links: Sensortyp falsch | 0 | ST |
| 0x930A87 | Fussgängerschutzsensor vorn links: Kommunikationsstoerung | 0 | ZP |
| 0x930A89 | Fussgängerschutzsensor vorn links: Kurzschluss nach Minus | 0 | ZP |
| 0x930A8A | Fussgängerschutzsensor vorn links: Kurzschluss nach Plus | 0 | ZP |
| 0x930A8B | Fussgängerschutzsensor vorn links: Unterbrechung | 0 | ZP |
| 0x930A8E | Fussgängerschutzsensor vorn Mitte: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930A8F | Fussgängerschutzsensor vorn Mitte: sendet Fehler | 0 | ZP |
| 0x930A90 | Fussgängerschutzsensor vorn Mitte: Sensortyp falsch | 0 | ST |
| 0x930A91 | Fussgängerschutzsensor vorn Mitte: Kommunikationsstoerung | 0 | ZP |
| 0x930A93 | Fussgängerschutzsensor vorn Mitte: Kurzschluss nach Minus | 0 | ZP |
| 0x930A94 | Fussgängerschutzsensor vorn Mitte: Kurzschluss nach Plus | 0 | ZP |
| 0x930A95 | Fussgängerschutzsensor vorn Mitte: Unterbrechung | 0 | ZP |
| 0x930A98 | Fussgängerschutzsensor vorn rechts: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930A99 | Fussgängerschutzsensor vorn rechts: sendet Fehler | 0 | ZP |
| 0x930A9A | Fussgängerschutzsensor vorn rechts: Sensortyp falsch | 0 | ST |
| 0x930A9B | Fussgängerschutzsensor vorn rechts: Kommunikationsstoerung | 0 | ZP |
| 0x930A9D | Fussgängerschutzsensor vorn rechts: Kurzschluss nach Minus | 0 | ZP |
| 0x930A9E | Fussgängerschutzsensor vorn rechts: Kurzschluss nach Plus | 0 | ZP |
| 0x930A9F | Fussgängerschutzsensor vorn rechts: Unterbrechung | 0 | ZP |
| 0x930AA1 | Versorgungsspannung: Unterspannung | 1 | ZP |
| 0x930AA2 | Versorgungsspannung: Ueberspannung | 1 | ZP |
| 0x930AA3 | Versorgungsspannung: Unterspannung im Selbstest erkannt (PDC) | 1 | ST |
| 0x930AA4 | Versorgungsspannung: Ueberspannung im Selbstest erkannt (PDC) | 1 | ST |
| 0x930AA5 | ODS-System: Sitzbelegungsmatte Beifahrer: sendet CIS-interner Elektronikfehler (EEPROM) | 0 | ZP |
| 0x930AA6 | Versorgungsspannung Sitzmatte Beifahrer: Stromaufnahme zu klein | 0 | ZP |
| 0x930AA7 | Versorgungsspannung Sitzmatte Beifahrer: Stromaufnahme zu groß | 0 | ZP |
| 0x930AA8 | ODS-System: Sitzbelegungsmatte Beifahrer: sendet CIS-interner Elektronikfehler (COMP) | 0 | ZP |
| 0x930AAE | ODS-System: Sitzbelegungsmatte Beifahrer: sendet CIS-Speicherfehler Elektronik | 0 | ZP |
| 0x930AAF | Versorgungsspannung Reserve: Stromaufnahme zu klein | 0 | ZP |
| 0x930AB0 | Versorgungsspannung Reserve: Stromaufnahme zu gross | 0 | ZP |
| 0x930AB1 | POL: Kontrollleuchte fuer Beifahrerairbag-Abschaltung: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930AB2 | POL: Kontrollleuchte fuer Beifahrerairbag-Abschaltung: Kurzschluss nach Minus oder Unterbrechung | 0 | ZP |
| 0x930AB3 | POL: Kontrollleuchte fuer Beifahrerairbag-Abschaltung: Kurzschluss nach Plus | 0 | ZP |
| 0x930AB4 | Codierdatenfehler: (CBD-Block: CRC Fehler durch Schreiben der Codierdaten) | 0 | ST |
| 0x930AB5 | Codierpruefstempel stimmt nicht mit Fahrgestellnummer ueberein | 0 | ZP |
| 0x930AB6 | Crash-Botschaft gespeichert | 0 | ZP |
| 0x930AB7 | Drei Crash-Botschaften gespeichert | 0 | ZP |
| 0x930AB9 | Recycling-Zuendung wurde ausgefuehrt | 0 | ZP |
| 0x930ABC | Steuergeraet nicht verriegelt | 0 | ST, ZP |
| 0x930ABD | Interner Steuergeraetefehler | 0 | ZP |
| 0x930ABF | ODS-System: Sitzbelegungsmatte Beifahrer: sendet Fehler CIS-Codierdaten | 0 | ZP |
| 0x930AC0 | ODS-System: Sitzbelegungsmatte Beifahrer: sendet Algorithmusfehler | 0 | ZP |
| 0x930AC4 | Ueberfallschalter: Deaktivierung der Zuendkreise durch Ueberfallfunktion | 1 | ZP |
| 0x930AC9 | ODS-System: Sitzbelegungsmatte Beifahrer: sendet CIS-interner Elektronikfehler (externer Komparator) | 0 | ZP |
| 0x930ACA | ODS-System: Sitzbelegungsmatte Beifahrer: sendet CIS-interner Elektronikfehler (Kapazitaetsfehler) | 0 | ZP |
| 0x930ACB | Fussgaengerschutzsystem: Crash-Botschaft gespeichert | 0 | ZP |
| 0x930ACC | UpFront: Airbagfrontsensor links: Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930ACD | UpFront: Airbagfrontsensor rechts: Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930ACE | Airbagsensor B-Saeule links (x-y-Richtung): Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930ACF | Airbagsensor B-Saeule rechts (x-y-Richtung): Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930AD0 | Airbagsensor Tür vorn links: Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930AD1 | Airbagsensor Tür vorn rechts: Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930AD2 | Airbagsensor-Cluster (high g x-y-Richtung): Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930AD3 | Airbagsensor-Cluster (low g Drehrate): Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930AD4 | Fussgängerschutzsensor vorn links: Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930AD5 | Fussgängerschutzsensor vorn Mitte: Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930AD6 | Fussgängerschutzsensor vorn rechts: Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930AD7 | ODS-System: Sitzbelegungsmatte Beifahrer: sendet Fehler CIS Spannungsversorgung | 0 | ZP |
| 0x930AD8 | Rollover- Schutz links pyrotechnisch: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930AD9 | Rollover- Schutz links pyrotechnisch: Kurzschluss nach Minus | 0 | ZP |
| 0x930ADA | Rollover- Schutz links pyrotechnisch: Kurzschluss nach Plus | 0 | ZP |
| 0x930ADB | Rollover- Schutz links pyrotechnisch: Widerstand zu klein | 0 | ZP |
| 0x930ADC | Rollover- Schutz links pyrotechnisch: Widerstand zu gross | 0 | ZP |
| 0x930ADD | Rollover- Schutz links pyrotechnisch: Leitung verkoppelt | 0 | ST |
| 0x930ADE | Rollover- Schutz rechts pyrotechnisch: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930ADF | Rollover- Schutz rechts pyrotechnisch: Kurzschluss nach Minus | 0 | ZP |
| 0x930AE0 | Rollover- Schutz rechts pyrotechnisch: Kurzschluss nach Plus | 0 | ZP |
| 0x930AE1 | Rollover- Schutz rechts pyrotechnisch: Widerstand zu klein | 0 | ZP |
| 0x930AE2 | Rollover- Schutz rechts pyrotechnisch: Widerstand zu gross | 0 | ZP |
| 0x930AE3 | Rollover- Schutz rechts pyrotechnisch: Leitung verkoppelt | 0 | ST |
| 0x930AE4 | Curtain hinten links: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930AE5 | Curtain hinten links: Kurzschluss nach Minus | 0 | ZP |
| 0x930AE6 | Curtain hinten links: Kurzschluss nach Plus | 0 | ZP |
| 0x930AE7 | Curtain hinten links: Widerstand zu klein | 0 | ZP |
| 0x930AE8 | Curtain hinten links: Widerstand zu groß | 0 | ZP |
| 0x930AE9 | Curtain hinten links: Leitung verkoppelt | 0 | ST |
| 0x930AEA | Curtain hinten rechts: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930AEB | Curtain hinten rechts: Kurzschluss nach Minus | 0 | ZP |
| 0x930AEC | Curtain hinten rechts: Kurzschluss nach Plus | 0 | ZP |
| 0x930AED | Curtain hinten rechts: Widerstand zu klein | 0 | ZP |
| 0x930AEE | Curtain hinten rechts: Widerstand zu groß | 0 | ZP |
| 0x930AEF | Curtain hinten rechts: Leitung verkoppelt | 0 | ST |
| 0x930AF0 | Variable Zuendkreistabelle nicht eindeutig kodiert | 0 | ST |
| 0x930AF1 | Fussgaengerschutzfunktion nicht aktiv | 0 | ST |
| 0x930AF2 | Fehler in der Crashalgorithmuskennung | 0 | ST |
| 0x930AF3 | Zentralsensor (Gierratensensor): unplausible Werte | 0 | ZP |
| 0x930AF5 | UpFront: Airbagfrontsensor links: Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930AF6 | UpFront: Airbagfrontsensor rechts: Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930AF7 | Airbagsensor B-Saeule links (x-Richtung): Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930AF8 | Airbagsensor B-Saeule links (y-Richtung): Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930AF9 | Airbagsensor B-Saeule rechts (x-Richtung): Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930AFA | Airbagsensor B-Saeule rechts (y-Richtung): Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930AFB | Airbagsensor Tür vorn rechts: Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930AFC | Zentralsensor (x-Richtung): Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930AFD | Zentralsensor (y-Richtung): Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930AFE | Zentralsensor (y-Richtung): Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930AFF | Zentralsensor (z-Richtung): Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930B01 | Fussgängerschutzsensor vorn links - Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930B02 | Fussgängerschutzsensor vorn Mitte - Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930B03 | Fussgängerschutzsensor vorn rechts - Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930B04 | Automatenstrammer Fahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B05 | Automatenstrammer Fahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x930B06 | Automatenstrammer Fahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x930B07 | Automatenstrammer Fahrer: Widerstand zu klein | 0 | ZP |
| 0x930B08 | Automatenstrammer Fahrer: Widerstand zu groß | 0 | ZP |
| 0x930B09 | Automatenstrammer Fahrer: Leitung verkoppelt | 0 | ST |
| 0x930B0A | Automatenstrammer Beifahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B0B | Automatenstrammer Beifahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x930B0C | Automatenstrammer Beifahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x930B0D | Automatenstrammer Beifahrer: Widerstand zu klein | 0 | ZP |
| 0x930B0E | Automatenstrammer Beifahrer: Widerstand zu groß | 0 | ZP |
| 0x930B0F | Automatenstrammer Beifahrer: Leitung verkoppelt | 0 | ST |
| 0x930B11 | FGS_SB Fussgängerschutzsensor: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B12 | FGS_SB Fussgängerschutzsensor: sendet Fehler | 0 | ZP |
| 0x930B13 | FGS_SB Fussgängerschutzsensor: Sensortyp falsch | 0 | ZP |
| 0x930B14 | FGS_SB Fussgängerschutzsensor: Kommunikationsstoerung | 0 | ZP |
| 0x930B15 | FGS_SB Fussgängerschutzsensor: Kurzschluss nach Minus | 0 | ZP |
| 0x930B16 | FGS_SB Fussgängerschutzsensor: Kurzschluss nach Plus | 0 | ZP |
| 0x930B17 | FGS_SB Fussgängerschutzsensor: Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930B18 | FGS_SB Fussgängerschutzsensor: Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930B19 | FGS_SB Fussgängerschutzsensor: Unterbrechung | 0 | ZP |
| 0x930B1A | FGS_SB Fussgängerschutzsensor: Sensor defekt | 0 | ZP |
| 0x930B1B | Sitzpositionssensor Beifahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B1C | Sitzpositionssensor Beifahrer: Messwert außerhalb des gültigen Bereiches | 0 | ZP |
| 0x930B1D | Sitzpositionssensor Beifahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x930B1E | Sitzpositionssensor Beifahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x930B1F | Sitzpositionssensor Beifahrer: Unterbrechung | 0 | ZP |
| 0x930B20 | Sitzpositionssensor Beifahrer: Leitung verkoppelt | 0 | ST |
| 0x930B21 | Airbagsensor C-Saeule links (y-Richtung) - Sensortyp falsch | 0 | ZP |
| 0x930B22 | Airbagsensor C-Saeule links (y-Richtung) - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B23 | Airbagsensor C-Saeule links (y-Richtung) - sendet Fehler | 0 | ZP |
| 0x930B24 | Airbagsensor C-Saeule links (y-Richtung) - Kommunikationsstoerung | 0 | ZP |
| 0x930B25 | Airbagsensor C-Saeule links (y-Richtung) - Kurzschluss nach Minus | 0 | ZP |
| 0x930B26 | Airbagsensor C-Saeule links (y-Richtung) - Kurzschluss nach Plus | 0 | ZP |
| 0x930B27 | Airbagsensor C-Saeule links (y-Richtung) - Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930B28 | Airbagsensor C-Saeule links (y-Richtung) - Unterbrechung | 0 | ZP |
| 0x930B29 | Airbagsensor C-Saeule links (y-Richtung) - Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930B2A | Airbagsensor C-Saeule links (y-Richtung) - Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930B2B | Airbagsensor C-Saeule rechts (y-Richtung) - Sensortyp falsch | 0 | ZP |
| 0x930B2C | Airbagsensor C-Saeule rechts (y-Richtung) - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B2D | Airbagsensor C-Saeule rechts (y-Richtung) - sendet Fehler | 0 | ZP |
| 0x930B2E | Airbagsensor C-Saeule rechts (y-Richtung) - Kommunikationsstoerung | 0 | ZP |
| 0x930B2F | Airbagsensor C-Saeule rechts (y-Richtung) - Kurzschluss nach Minus | 0 | ZP |
| 0x930B30 | Airbagsensor C-Saeule rechts (y-Richtung) - Kurzschluss nach Plus | 0 | ZP |
| 0x930B31 | Airbagsensor C-Saeule rechts (y-Richtung) - Kurzschluss nach Plus oder Unterbrechung | 0 | ZP |
| 0x930B32 | Airbagsensor C-Saeule rechts (y-Richtung) - Unterbrechung | 0 | ZP |
| 0x930B33 | Airbagsensor C-Saeule rechts (y-Richtung) - Kurzschluss nach Minus oder Plus | 0 | ZP |
| 0x930B34 | Airbagsensor C-Saeule rechts (y-Richtung) - Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930B4F | Rollover- Schutz links magnetisch: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B50 | Rollover- Schutz links magnetisch: Kurzschluss nach Minus | 0 | ZP |
| 0x930B51 | Rollover- Schutz links magnetisch: Kurzschluss nach Plus | 0 | ZP |
| 0x930B52 | Rollover- Schutz links magnetisch: Widerstand zu klein | 0 | ZP |
| 0x930B53 | Rollover- Schutz links magnetisch: Widerstand zu gross | 0 | ZP |
| 0x930B54 | Rollover- Schutz links magnetisch: Leitung verkoppelt | 0 | ST |
| 0x930B55 | Rollover- Schutz rechts magnetisch: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B56 | Rollover- Schutz rechts magnetisch: Kurzschluss nach Minus | 0 | ZP |
| 0x930B57 | Rollover- Schutz rechts magnetisch: Kurzschluss nach Plus | 0 | ZP |
| 0x930B58 | Rollover- Schutz rechts magnetisch: Widerstand zu klein | 0 | ZP |
| 0x930B59 | Rollover- Schutz rechts magnetisch: Widerstand zu gross | 0 | ZP |
| 0x930B5A | Rollover- Schutz rechts magnetisch: Leitung verkoppelt | 0 | ST |
| 0x930B64 | Plausibilitaetsfehler Zuendkreis Pin A06 - A07 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B65 | Plausibilitaetsfehler Zuendkreis Pin A08 - A09 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B66 | Plausibilitaetsfehler Zuendkreis Pin A11 - A12 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B67 | Plausibilitaetsfehler Zuendkreis Pin A13 - A14 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B68 | Plausibilitaetsfehler Zuendkreis Pin A16 - A17 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B69 | Plausibilitaetsfehler Zuendkreis Pin A18 - A19 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B6A | Plausibilitaetsfehler Zuendkreis Pin B40 - B41 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B6B | Plausibilitaetsfehler Zuendkreis Pin B42 - B43 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B6C | Plausibilitaetsfehler Zuendkreis Pin B59 - B60 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B6D | Plausibilitaetsfehler Zuendkreis Pin B61 - B62 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B6E | Plausibilitaetsfehler Zuendkreis Pin B63 - B64 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B6F | Plausibilitaetsfehler Zuendkreis Pin B66 - B67 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B70 | Plausibilitaetsfehler Zuendkreis Pin B68 - B69 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B71 | Plausibilitaetsfehler Zuendkreis Pin B70 - B71 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B72 | Plausibilitaetsfehler Zuendkreis Pin B72 - B73 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B73 | Plausibilitaetsfehler Zuendkreis Pin B74 - B75 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B74 | Plausibilitaetsfehler Zuendkreis Pin B76 - B77 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B75 | Plausibilitaetsfehler Zuendkreis Pin B79 - B80 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B76 | Plausibilitaetsfehler Zuendkreis Pin B81 - B82  - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B77 | Plausibilitaetsfehler Zuendkreis Pin B83 - B84 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B78 | Plausibilitaetsfehler Zuendkreis Pin B85 - B86 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B79 | Plausibilitaetsfehler Zuendkreis Pin B87 - B88 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B7A | Plausibilitaetsfehler Zuendkreis Pin B89 - B90 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B7B | Plausibilitaetsfehler Zuendkreis Pin B92 - B93 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B7C | Plausibilitaetsfehler Zuendkreis Pin B94 - B95 - Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B7D | Plausibilitaetsfehler Zuendkreis Pin B96 - B97 - Kodierdaten stimmen nicht Ausstattung ueberein | 0 | ST |
| 0x930B7E | Plausibilitaetsfehler Zuendkreis Pin B98 - B99 - Kodierdaten stimmen nicht Ausstattung ueberein | 0 | ST |
| 0x930B7F | Plausibilitaetsfehler Zuendkreis Pin B100 - B101 - Kodierdaten stimmen nicht Ausstattung ueberein | 0 | ST |
| 0x930B80 | Plausibilitaetsfehler Zuendkreis Pin B102 - B103 - Kodierdaten stimmen nicht Ausstattung ueberein | 0 | ST |
| 0x930B8A | Schalter fuer Beifahrerairbag-Abschaltung - Kurzschluss | 0 | ZP |
| 0x930B8B | SBR-Sensor: Sitzbelegungsmatte Beifahrer: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930B8C | SBR-Sensor: Sitzbelegungsmatte Beifahrer: Messwert außerhalb des gültigen Bereiches | 0 | ZP |
| 0x930B8D | SBR-Sensor: Sitzbelegungsmatte Beifahrer: Kurzschluss nach Minus | 0 | ZP |
| 0x930B8E | SBR-Sensor: Sitzbelegungsmatte Beifahrer: Kurzschluss nach Plus | 0 | ZP |
| 0x930B8F | SBR-Sensor Beifahrer - Unterbrechung | 0 | ZP |
| 0x930B91 | Gurtschlosskontakt Fahrer - Messwert außerhalb des gültigen Bereiches | 0 | ZP |
| 0x930B92 | Gurtschlosskontakt Fahrer - Kurzschluss nach Masse | 0 | ZP |
| 0x930B93 | Gurtschlosskontakt Fahrer - Kurzschluss nach Plus | 0 | ZP |
| 0x930B94 | Gurtschlosskontakt Fahrer - Unterbrechung | 0 | ZP |
| 0x930B95 | Gurtschlosskontakt Fahrer - Leitung verkoppelt | 0 | ST |
| 0x930B96 | Gurtschlosskontakt Beifahrer - Messwert außerhalb des gültigen Bereiches | 0 | ZP |
| 0x930B97 | Gurtschlosskontakt Beifahrer - Kurzschluss nach Masse | 0 | ZP |
| 0x930B98 | Gurtschlosskontakt Beifahrer - Kurzschluss nach Plus | 0 | ZP |
| 0x930B99 | Gurtschlosskontakt Beifahrer - Unterbrechung | 0 | ZP |
| 0x930B9A | Gurtschlosskontakt Beifahrer - Leitung verkoppelt | 0 | ST |
| 0x930B9B | High Side Power Switch Sitzmatte: Kurzschluss nach Minus | 0 | ZP |
| 0x930B9C | High Side Power Switch Sitzmatte: Kurzschluss nach Plus | 0 | ZP |
| 0x930B9D | High Side Power Switch Reserve - Kurzschluss nach Minus | 0 | ZP |
| 0x930B9E | High Side Power Switch Reserve - Kurzschluss nach Plus | 0 | ZP |
| 0x930B9F | Codierung : Codierung passt nicht zum Fahrzeug | 0 | - |
| 0x930BA0 | Codierung: Steuergeraet ist nicht codiert | 0 | - |
| 0x930BA1 | Codierung : Fehler bei Codierung aufgetreten | 0 | - |
| 0x930BA2 | Codierung: Signatur für Daten ungültig | 0 | - |
| 0x930BA3 | Codierung : Unplausible Daten während Transaktion | 0 | - |
| 0x930BA4 | Interner Steuergeraetefehler | 0 | ZP |
| 0x930BA5 | Fehler in der Crashalgorithmuskennung | 0 | ST |
| 0x930BA6 | Airbagsensor B-Saeule links (x-y-Richtung): Leitung verkoppelt | 0 | ST |
| 0x930BA7 | Airbagsensor B-Saeule rechts (x-y-Richtung) - Leitung verkoppelt | 0 | ST |
| 0x930BA8 | Airbagsensor Tür vorn links: Leitung verkoppelt | 0 | ST |
| 0x930BA9 | Airbagsensor Tür vorn rechts: Leitung verkoppelt | 0 | ST |
| 0x930BAA | Airbagsensor-Cluster (high g x-y-Richtung): Leitung verkoppelt | 0 | ST |
| 0x930BAB | Airbagsensor-Cluster (low g Drehrate): Leitung verkoppelt | 0 | ST |
| 0x930BAC | Fussgängerschutzsensor vorn links - Leitung verkoppelt | 0 | ST |
| 0x930BAD | Fussgängerschutzsensor vorn Mitte - Leitung verkoppelt | 0 | ST |
| 0x930BAE | Fussgängerschutzsensor vorn rechts - Leitung verkoppelt | 0 | ST |
| 0x930BAF | UpFront: Airbagfrontsensor links: Leitung verkoppelt | 0 | ST |
| 0x930BB1 | UpFront: Airbagfrontsensor rechts: Leitung verkoppelt | 0 | ST |
| 0x930BB2 | Fussgängerschutz Sensorband: Leitung verkoppelt | 0 | ST |
| 0x930BB3 | Airbagsensor C-Saeule links (y-Richtung) - Leitung verkoppelt | 0 | ST |
| 0x930BB4 | Airbagsensor C-Saeule rechts  (y-Richtung) - Leitung verkoppelt | 0 | ST |
| 0x930BB5 | Datenkonsistenzfehler - Programmcode (Datenfehler) | 0 | ST |
| 0x930BB6 | Datenkonsistenzfehler: Codierdaten (Datenfehler) | 0 | ST |
| 0x930BB7 | Datenkonsistenzfehler - Programmcode (Datenfehler) | 0 | ST |
| 0x930BB8 | Datenkonsistenzfehler: Codierdaten (Datenfehler) | 0 | ST |
| 0x930BB9 | Fehlerspeicher gesperrt | 0 | ZP |
| 0x930BBA | Die Sequenz zum Ausloesen der Rollover-Buegel ist aktiv | 1 | ZP |
| 0x930BBB | Rollover-Sensorkanal: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ZP |
| 0x930BBC | SBR-Sensor: Sitzbelegungsmatte Beifahrer: Leitung verkoppelt | 0 | ST |
| 0x930BBD | Airbagsensor-Cluster (Koerperschall): Sensortyp falsch | 0 | ST |
| 0x930BBE | Airbagsensor-Cluster (Koerperschall): sendet Fehler | 0 | ZP |
| 0x930BBF | Airbagsensor-Cluster (Koerperschall): Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930BC0 | Airbagsensoren Tueren vorn: Werte Initialmessung unterschiedlich | 0 | ST |
| 0x930BC6 | FGS_Drucksystem - Funktion nicht verfügbar oder fehlerhaft | 0 | ZP |
| 0x930BC7 | Fussgängerschutzsensor PTS links: Sensortyp falsch | 0 | ST |
| 0x930BC8 | Fussgängerschutzsensor PTS links: Druckwert ueber Grenzwert | 0 | ZP |
| 0x930BC9 | Fussgängerschutzsensor PTS links: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930BCA | Fussgängerschutzsensor PTS links: sendet Fehler | 0 | ZP |
| 0x930BCB | Fussgängerschutzsensor PTS links: Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930BCC | Fussgängerschutzsensor PTS links: Kommunikationsstoerung | 0 | ZP |
| 0x930BCD | Fussgängerschutzsensor PTS links: Kurzschluss nach Minus | 0 | ZP |
| 0x930BCE | Fussgängerschutzsensor PTS links: Kurzschluss nach Plus | 0 | ZP |
| 0x930BCF | Fussgängerschutzsensor PTS links: Unterbrechung | 0 | ZP |
| 0x930BD0 | Fussgängerschutzsensor PTS rechts: Sensortyp falsch | 0 | ST |
| 0x930BD1 | Fussgängerschutzsensor PTS rechts: Druckwert ueber Grenzwert | 0 | ZP |
| 0x930BD2 | Fussgängerschutzsensor PTS rechts: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930BD3 | Fussgängerschutzsensor PTS rechts: sendet Fehler | 0 | ZP |
| 0x930BD4 | Fussgängerschutzsensor PTS rechts: Sensorwerte liegen dauerhaft ueber Offset-Wert | 0 | ZP |
| 0x930BD5 | Fussgängerschutzsensor PTS rechts: Kommunikationsstoerung | 0 | ZP |
| 0x930BD6 | Fussgängerschutzsensor PTS rechts: Kurzschluss nach Minus | 0 | ZP |
| 0x930BD7 | Fussgängerschutzsensor PTS rechts: Kurzschluss nach Plus | 0 | ZP |
| 0x930BD8 | Fussgängerschutzsensor PTS rechts : Unterbrechung | 0 | ZP |
| 0x930BD9 | Drei Event- Eintraege belegt | 0 | ZP |
| 0x930C30 | Windowbag : Kurzschluss nach Minus | 0 | ZP |
| 0x930C31 | Windowbag: Kurzschluss nach Plus | 0 | ZP |
| 0x930C32 | Windowbag: Widerstand zu klein | 0 | ZP |
| 0x930C33 | Windowbag: Widerstand zu gross | 0 | ZP |
| 0x930C34 | Windowbag: Leitung verkoppelt | 0 | ST |
| 0x930C35 | Windowbag Rueckholung: Kurzschluss nach Minus | 0 | ZP |
| 0x930C36 | Windowbag Rueckholung: Kurzschluss nach Plus | 0 | ZP |
| 0x930C37 | Windowbag Rueckholung: Widerstand zu klein | 0 | ZP |
| 0x930C38 | Windowbag Rueckholung: Widerstand zu groß | 0 | ZP |
| 0x930C39 | Windowbag Rueckholung: Leitung verkoppelt | 0 | ST |
| 0x930C44 | Windowbag : Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0x930C45 | Windowbag Rueckholung: Kodierdaten stimmen nicht mit Ausstattung ueberein | 0 | ST |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 411 rows × 4 columns

| ORT | ORTTEXT | EREIGNIS_DTC | FEHLERSETZBEDINGUNGEN |
| --- | --- | --- | --- |
| 0x019000 | COMM_E_STOP_Tx_TIMEOUT_C0 | 0 | - |
| 0x019001 | COMM_E_START_Tx_TIMEOUT_C0 | 0 | - |
| 0x019002 | CAN_E_TIMEOUT | 0 | - |
| 0x019003 | Fehler konnte nach maximaler Anzahl von Versuchen nicht gesendet werden | 1 | - |
| 0x019004 | Puffer für ausgehende Fehlermeldungen ist voll | 1 | - |
| 0x019006 | Botschaft (Fahrzeugzustand, 0x3A0) fehlt | 1 | - |
| 0x019007 | CANIF_E_INVALID_TXPDUID | 0 | - |
| 0x019008 | CANIF_E_INVALID_RXPDUID | 0 | - |
| 0x019009 | NVM_E_REQ_FAILED | 0 | - |
| 0x01900A | ECUM_E_ALL_RUN_REQUESTS_KILLED | 0 | - |
| 0x01900B | COMM_E_NET_START_IND_CHANNEL_0 | 0 | - |
| 0x019010 | VSM_EVENT_OPMODE | 0 | - |
| 0x019011 | WDGM_E_ALIVE_SUPERVISION | 0 | - |
| 0x019012 | PIA_E_IO_ERROR | 0 | - |
| 0x019013 | FR_E_ACCESS | 0 | - |
| 0x019014 | FRIF_E_JLE_SYNC | 0 | - |
| 0x019015 | FRTRCV_10_TJA1080_E_FR_NO_TRCV_C | 0 | - |
| 0x019017 | CNM_E_NETWORK_TIMEOUT | 0 | - |
| 0x019018 | FLS_E_ERASE_FAILED | 0 | - |
| 0x019019 | FLS_E_WRITE_FAILED | 0 | - |
| 0x01901A | FLS_E_READ_FAILED | 0 | - |
| 0x01901B | FLS_E_COMPARE_FAILED | 0 | - |
| 0x01901C | IPDUM_E_TRANSMIT_FAILED | 0 | - |
| 0x01901D | COMM_E_START_Tx_TIMEOUT_C1 | 0 | - |
| 0x01901E | COMM_E_STOP_Tx_TIMEOUT_C1 | 0 | - |
| 0x01901F | COMM_E_NET_START_IND_CHANNEL_1 | 0 | - |
| 0x019020 | LINIF_E_RESPONSE | 0 | - |
| 0x019021 | LINIF_E_NC_NO_RESPONSE | 0 | - |
| 0x019022 | CSM_E_ERROR_EVENT | 0 | - |
| 0x019023 | NVM_E_INTEGRITY_FAILED | 0 | - |
| 0x019024 | CANIF_E_FULL_TX_BUFFER | 0 | - |
| 0x019025 | CANIF_E_STOPPED | 0 | - |
| 0x019026 | CANNM_E_INIT_FAILED | 0 | - |
| 0x019027 | CANNM_E_CANIF_TRANSMIT_ERROR | 0 | - |
| 0x019028 | CANTP_E_COMM | 0 | - |
| 0x019029 | CNM_E_TX_PATH_FAILED | 0 | - |
| 0x01902B | FEE_E_WRITE_FAILED | 0 | - |
| 0x01902C | WDGM_E_SET_MODE | 0 | - |
| 0x01902D | WDG_E_MODE_SWITCH_FAILED | 0 | - |
| 0x01902E | WDG_E_DISABLE_REJECTED | 0 | - |
| 0x01902F | MCU_E_LOCK_FAILURE | 0 | - |
| 0x019031 | Signal (Zeit_Sekunde_Zaehler_Relativ, 0x328): ungültig | 1 | - |
| 0x019032 | MCU_E_CLOCK_FAILURE | 0 | - |
| 0x019033 | MCU_E_CLOCK_FAILURE | 0 | - |
| 0x019034 | MCU_E_CLOCK_FAILURE | 0 | - |
| 0x019035 | MCU_E_CLOCK_FAILURE | 0 | - |
| 0x010000 | Systemzeit Diagnose Master - Empfang unplausibel / keine Systemzeit erhalten | 1 | ZP |
| 0x010002 | Geschwindigkeit - Signal fehlerhaft | 1 | ZP |
| 0x010020 | FGS_SB Fussgaengerschutz-Sensor - Timeout Fahrzeuggeschwindigkeit bei Alert | 0 | ZP |
| 0x010021 | FGS_SB Fussgaengerschutz-Sensor - Timeout dynamische Daten Normal | 0 | ZP |
| 0x010022 | FGS_SB Fussgaengerschutz-Sensor - Timeout dynamische Daten Alert | 0 | ZP |
| 0x010023 | FGS_SB Fussgängerschutzsensor - Timeout statische Daten | 0 | ZP |
| 0x010024 | FGS_SB Fussgaengerschutz-Sensor - Timeout Temperatur | 0 | ZP |
| 0x010025 | FGS_SB Fussgaengerschutz-Sensor - Offset Drift | 0 | ZP |
| 0x010026 | FGS_SB Fussgaengerschutz-Sensor - Plausibilitaet dynamische Daten | 0 | ZP |
| 0x010027 | FGS_SB Fussgaengerschutz-Sensor - Initialisierung fehlerhaft | 0 | ZP |
| 0x010028 | FGS_SB Fussgaengerschutz-Sensor - Offset Abgleich fehlerhaft | 0 | ZP |
| 0x010029 | FGS_SB Fussgaengerschutz-Sensor - Safing Path gesperrt | 0 | ZP |
| 0x01002A | Info Alert-Schwelle | 0 | ZP |
| 0x01002B | FGS_SB Fussgängerschutzsensor - Arming fehlt | 0 | ZP |
| 0x01002C | Datenrecorder Datenspeicherung nicht möglich | 0 | ZP |
| 0x01002D | FGS_Drucksystem - Integritaetsfehler Sensor links | 0 | ZP |
| 0x01002E | FGS_Drucksystem - Integritaetsfehler Sensor rechts | 0 | ZP |
| 0x01002F | FGS_Drucksystem - FGS-Algo :  Fahrzeuggeschwindigkeit Timeout | 0 | ZP |
| 0x010030 | FGS_Drucksystem - Safing-Path gesperrt | 0 | ZP |
| 0x010031 | FGS_Drucksystem - Safing-Sensor Arming fehlt | 0 | ZP |
| 0x010032 | FGS Near Deploy low | 0 | TODO |
| 0x010033 | FGS Near Deploy high | 0 | TODO |
| 0x010036 | Info NoAlive MVBAT(KL30B) | 0 | TODO |
| 0x010037 | Info NoAlive VBDIAG(GKEY) | 0 | TODO |
| 0x010038 | Trigger Rollover eCall - gesendet | 0 | ZP |
| 0x013000 | FltAB1FDHighSidePowerstage | 0 | ST |
| 0x013001 | FltAB1FDLowSidePowerstage | 0 | ST |
| 0x013002 | FltAB2FDHighSidePowerstage | 0 | ST |
| 0x013003 | FltAB2FDLowSidePowerstage | 0 | ST |
| 0x013004 | FltAAV1FDHighSidePowerstage | 0 | ST |
| 0x013005 | FltAAV1FDLowSidePowerstage | 0 | ST |
| 0x013006 | FltAB1FPHighSidePowerstage | 0 | ST |
| 0x013007 | FltAB1FPLowSidePowerstage | 0 | ST |
| 0x013008 | FltAB2FPHighSidePowerstage | 0 | ST |
| 0x013009 | FltAB2FPLowSidePowerstage | 0 | ST |
| 0x01300A | FltAAV1FPHighSidePowerstage | 0 | ST |
| 0x01300B | FltAAV1FPLowSidePowerstage | 0 | ST |
| 0x01300C | FltBT1FDHighSidePowerstage | 0 | ST |
| 0x01300D | FltBT1FDLowSidePowerstage | 0 | ST |
| 0x01300E | FltCT1FDHighSidePowerstage | 0 | ST |
| 0x01300F | FltCT1FDLowSidePowerstage | 0 | ST |
| 0x013010 | FltBL1FDHighSidePowerstage | 0 | ST |
| 0x013011 | FltBL1FDLowSidePowerstage | 0 | ST |
| 0x013012 | FltBT1FPHighSidePowerstage | 0 | ST |
| 0x013013 | FltBT1FPLowSidePowerstage | 0 | ST |
| 0x013014 | FltCT1FPHighSidePowerstage | 0 | ST |
| 0x013015 | FltCT1FPLowSidePowerstage | 0 | ST |
| 0x013016 | FltBL1FPHighSidePowerstage | 0 | ST |
| 0x013017 | FltBL1FPLowSidePowerstage | 0 | ST |
| 0x013018 | FltKB1FDHighSidePowerstage | 0 | ST |
| 0x013019 | FltKB1FDLowSidePowerstage | 0 | ST |
| 0x01301A | FltKB1FPHighSidePowerstage | 0 | ST |
| 0x01301B | FltKB1FPLowSidePowerstage | 0 | ST |
| 0x013028 | FltSA1FDHighSidePowerstage | 0 | ST |
| 0x013029 | FltSA1FDLowSidePowerstage | 0 | ST |
| 0x01302A | FltSA1FPHighSidePowerstage | 0 | ST |
| 0x01302B | FltSA1FPLowSidePowerstage | 0 | ST |
| 0x01302C | FltCA1LHighSidePowerstage | 0 | ST |
| 0x01302D | FltCA1LLowSidePowerstage | 0 | ST |
| 0x01302E | FltCA1RHighSidePowerstage | 0 | ST |
| 0x01302F | FltCA1RLowSidePowerstage | 0 | ST |
| 0x013030 | FltBATD1HighSidePowerstage | 0 | ST |
| 0x013031 | FltBATD1LowSidePowerstage | 0 | ST |
| 0x013032 | FltBATD2HighSidePowerstage | 0 | ST |
| 0x013033 | FltBATD2LowSidePowerstage | 0 | ST |
| 0x013038 | FltPPAFLHighSidePowerstage | 0 | ST |
| 0x013039 | FltPPAFLLowSidePowerstage | 0 | ST |
| 0x01303A | FltPPAFRHighSidePowerstage | 0 | ST |
| 0x01303B | FltPPAFRLowSidePowerstage | 0 | ST |
| 0x01303C | FltPPARLHighSidePowerstage | 0 | ST |
| 0x01303D | FltPPARLLowSidePowerstage | 0 | ST |
| 0x01303E | FltPPARRHighSidePowerstage | 0 | ST |
| 0x01303F | FltPPARRLowSidePowerstage | 0 | ST |
| 0x013040 | FltRUTFDHighSidePowerstage | 0 | ST |
| 0x013041 | FltRUTFDLowSidePowerstage | 0 | ST |
| 0x013042 | FltRUTFPHighSidePowerstage | 0 | ST |
| 0x013043 | FltRUTFPLowSidePowerstage | 0 | ST |
| 0x013044 | FltCAHRDHighSidePowerstage | 0 | ST |
| 0x013045 | FltCAHRDLowSidePowerstage | 0 | ST |
| 0x013046 | FltBT1RLHighSidePowerstage | 0 | ST |
| 0x013047 | FltBT1RLLowSidePowerstage | 0 | ST |
| 0x013048 | FltBT1RRHighSidePowerstage | 0 | ST |
| 0x013049 | FltBT1RRLowSidePowerstage | 0 | ST |
| 0x01304E | FltHVD3HighSidePowerstage | 0 | ST |
| 0x01304F | FltHVD3LowSidePowerstage | 0 | ST |
| 0x013050 | FltROLLBARLHighSidePowerstage | 0 | ST |
| 0x013051 | FltROLLBARLLowSidePowerstage | 0 | ST |
| 0x013052 | FltROLLBARRHighSidePowerstage | 0 | ST |
| 0x013053 | FltROLLBARRHighSidePowerstage | 0 | ST |
| 0x013054 | FltROLLMAGLHighSidePowerstage | 0 | ST |
| 0x013055 | FltROLLMAGLLowSidePowerstage | 0 | ST |
| 0x013056 | FltROLLMAGRHighSidePowerstage | 0 | ST |
| 0x013057 | FltROLLMAGRLowSidePowerstage | 0 | ST |
| 0x013058 | FltCAHRPHighSidePowerstage | 0 | ST |
| 0x013059 | FltCAHRPLowSidePowerstage | 0 | ST |
| 0x013080 | FltUFSLInternalCommunication | 0 | ZP |
| 0x013081 | FltUFSRInternalCommunication | 0 | ZP |
| 0x013082 | FltPBLXInternalCommunication | 0 | ZP |
| 0x013083 | FltPBLYInternalCommunication | 0 | ZP |
| 0x013084 | FltPBRXInternalCommunication | 0 | ZP |
| 0x013085 | FltPBRYInternalCommunication | 0 | ZP |
| 0x013086 | FltPPSLInternalCommunication | 0 | ZP |
| 0x013087 | FltPPSRInternalCommunication | 0 | ZP |
| 0x013089 | FltCRCErrorExternal | 0 | ST |
| 0x01308A | FltSwitchInvalidConfig | 0 | ZP |
| 0x01308B | FltSEMConfiguration | 0 | ST |
| 0x01308C | FltAsicPsiInterface | 0 | ST |
| 0x013100 | FltDCUXInternalCommunication | 0 | ZP |
| 0x013101 | FltDCUYInternalCommunication | 0 | ZP |
| 0x013102 | FltSMI510ZInternalCommunication | 0 | ZP |
| 0x013103 | FltSMI510YInternalCommunication | 0 | ZP |
| 0x013104 | FltSMI510RRInternalCommunication | 0 | ZP |
| 0x013105 | FltMCSICH1InternalCommunication | 0 | ZP |
| 0x013106 | FltMCSICH2InternalCommunication | 0 | ZP |
| 0x013107 | FltMCSICH3InternalCommunication | 0 | ZP |
| 0x01310B | FltSBSHFInternalCommunication | 0 | ZP |
| 0x014000 | IdleMode | 0 | ST |
| 0x014001 | FltE2promNoCommunication | 0 | ST |
| 0x014002 | FltE2promWriteTimeout | 0 | ZP |
| 0x014003 | FltE2promWriteVerifyFault | 0 | ZP |
| 0x014004 | FltERMissing | 0 | ST |
| 0x014005 | FltERCapacity | 0 | ST |
| 0x014006 | FltERAutarkyCurrent | 0 | ST |
| 0x014007 | FltERUpConverter | 0 | ST |
| 0x014008 | FltERESR | 0 | ST |
| 0x014009 | FltERPPTest | 0 | ST |
| 0x01400A | FltFLICAoutENFLShort | 0 | ST |
| 0x01400B | FltSystemAsic1ENFLPowerstage | 0 | ST |
| 0x01400C | FltSystemAsic1SplDisablePowerstage | 0 | ST |
| 0x01400D | FltSystemAsic1SquibRefResistance | 0 | ZP |
| 0x01400E | FltSystemAsic1SquibERVoltage | 0 | ZP |
| 0x01400F | FltSystemAsic1VASVoltage | 0 | ZP |
| 0x014011 | FltAB9FlicRRefResistance | 0 | ZP |
| 0x014012 | FltAB9FLICSplDisablePowerstage | 0 | ST |
| 0x014013 | FltAB9FlicERVoltage | 0 | ZP |
| 0x014014 | FltAB9FlicRMVoltage | 0 | ZP |
| 0x014015 | FltAB9FLICAoutDisAHPShort | 0 | ST |
| 0x014016 | FltRAMSquibFiringStatus | 0 | ZP |
| 0x014017 | FltSquibConfigPlausibility | 0 | ST |
| 0x014018 | FltSystemAsicOverTemperature | 0 | ZP |
| 0x014019 | FltCompanionAsicOverTemperature | 0 | ZP |
| 0x01401A | FltDisableLines | 0 | ST |
| 0x01401B | FltSCONPlausibilityPath | 0 | ST |
| 0x01401C | FltCOMPDisLinesconnection | 0 | ST |
| 0x01401D | FltWD1 | 0 | ST |
| 0x01401E | FltWD2 | 0 | ST |
| 0x01401F | FltWD3 | 0 | ST |
| 0x014020 | FltWDSeq | 0 | ZP |
| 0x014021 | FltWDTemp | 0 | ZP |
| 0x014022 | FltWDDis | 0 | ZP |
| 0x014023 | FltSVRFailure | 0 | ST |
| 0x014024 | FltSystemAsic1AMUBusy | 0 | ZP |
| 0x014025 | FltSystemAsic1AMUTiming1 | 0 | ST |
| 0x014026 | FltSystemAsic1AMUTiming2 | 0 | ST |
| 0x014027 | FltSystemAsic1AMUTiming3 | 0 | ST |
| 0x014028 | FltSystemAsic1AMUTiming4 | 0 | ST |
| 0x014029 | FltSystemAsic1AMUAdc | 0 | ZP |
| 0x01402A | FltSystemAsic1AMUMuxTest1 | 0 | ZP |
| 0x01402B | FltSystemAsic1AMUMuxTest2 | 0 | ZP |
| 0x01402C | FltSystemAsic1AMUMuxTest3 | 0 | ZP |
| 0x01402E | FltPreMuxTest | 0 | ST |
| 0x01402F | FltADC | 0 | ST |
| 0x014030 | FltBISTFailure | 0 | ZP |
| 0x014031 | FltNSYSRESShortToVST33 | 0 | ST |
| 0x014033 | FltIllegalEvent | 0 | ZP |
| 0x014035 | FltSpiTFF | 0 | ZP |
| 0x014036 | FltCCTFailed | 0 | ST |
| 0x014037 | FltIniTestTimeOut | 0 | ST |
| 0x014039 | FltCRCClassFault | 0 | ST |
| 0x01403A | FltCRCDataSetInvalid | 0 | ST |
| 0x01403B | FltCRCDataSetNotEqual | 0 | ST |
| 0x01403C | FltCRCRamFault | 0 | ZP |
| 0x01403D | FltCRCPrimary | 0 | ST |
| 0x01403E | FltSystemAsic1RegProg | 0 | ST |
| 0x01403F | FltSystemAsic1Eop | 0 | ST |
| 0x014040 | FltSystemAsic1RegMon | 0 | ZP |
| 0x014041 | FltSystemAsic1EopMon | 0 | ZP |
| 0x014042 | FltParameterLayoutIDInvalid | 0 | ST |
| 0x014043 | FltCoreVtgFailure | 0 | ZP |
| 0x014044 | FltStackOverFlow | 0 | ZP |
| 0x014045 | FltROMTestFailed | 0 | ZP |
| 0x014046 | FltRAMFailure | 0 | ZP |
| 0x014047 | FltSystemAsic1IPPProgramming | 0 | ST |
| 0x014052 | FltCF190PasLine1RegProg | 0 | ST |
| 0x014053 | FltCF190PasLine2RegProg | 0 | ST |
| 0x014055 | FltKline1NoComm | 0 | ZP |
| 0x014057 | FltERVDN | 0 | ST |
| 0x014058 | FltVerHigh | 0 | ZP |
| 0x014059 | FltVerLow | 0 | ZP |
| 0x01405A | FltSdlHwSwMismatch | 0 | ZP |
| 0x01405B | FltSystemAsic1CfgMismatch | 0 | ZP |
| 0x01405D | FltCG9859CfgMismatch | 0 | ZP |
| 0x01405E | FltCsAsicXYCfgMismatch | 0 | ZP |
| 0x014070 | SAPHIR-Line 1: KS_to_Gnd | 0 | ZP |
| 0x014071 | SAPHIR-Line 1: KS_to_Ubat | 0 | ZP |
| 0x014072 | SAPHIR-Line 1: CrossCouple | 0 | ST |
| 0x014073 | SAPHIR-Line 2: KS_to_Gnd | 0 | ZP |
| 0x014074 | SAPHIR-Line 2: KS_to_Ubat | 0 | ZP |
| 0x014075 | SAPHIR-Line 2: CrossCouple | 0 | ST |
| 0x014076 | SAPHIR-Line 3: KS_to_Gnd | 0 | ZP |
| 0x014077 | SAPHIR-Line 3: KS_to_Ubat | 0 | ZP |
| 0x014078 | SAPHIR-Line 3: CrossCouple | 0 | ST |
| 0x014079 | SAPHIR-Line 4: KS_to_Gnd | 0 | ZP |
| 0x01407A | SAPHIR-Line 4: KS_to_Ubat | 0 | ZP |
| 0x01407B | SAPHIR-Line 4: CrossCouple | 0 | ST |
| 0x01407C | RAMSES-Line 1: KS_to_Gnd | 0 | ZP |
| 0x01407D | RAMSES-Line 1: KS_to_Ubat | 0 | ZP |
| 0x01407E | RAMSES-Line 1: CrossCouple | 0 | ST |
| 0x01407F | RAMSES-Line 2: KS_to_Gnd | 0 | ZP |
| 0x014080 | RAMSES-Line 2: KS_to_Ubat | 0 | ZP |
| 0x014081 | RAMSES-Line 2: CrossCouple | 0 | ST |
| 0x014082 | CF190: EClkMonTest | 0 | ST |
| 0x014083 | CF190: EClkInterruption | 0 | ST |
| 0x015000 | Airbagsensor B-Saeule rechts (x-Richtung) - Plausibilitaetsfehler | 0 | ST |
| 0x015001 | Airbagsensor B-Saeule rechts (x-Richtung) - Kommunikationsstoerung | 0 | ZP |
| 0x015002 | Airbagsensor B-Saeule rechts (y-Richtung) - Plausibilitaetsfehler | 0 | ST |
| 0x015003 | Airbagsensor B-Saeule rechts (y-Richtung) - Kommunikationsstoerung | 0 | ZP |
| 0x015004 | Airbagsensor B-Saeule links (x-Richtung) - Plausibilitaetsfehler | 0 | ST |
| 0x015005 | Airbagsensor B-Saeule links (x-Richtung) - Kommunikationsstoerung | 0 | ZP |
| 0x015006 | Airbagsensor B-Saeule links (y-Richtung) - Plausibilitaetsfehler | 0 | ST |
| 0x015007 | Airbagsensor B-Saeule links (y-Richtung) - Kommunikationsstoerung | 0 | ZP |
| 0x015008 | Airbagsensor-Cluster (high g x-Richtung) - Plausibilitaetsfehler | 0 | ST |
| 0x015009 | Airbagsensor-Cluster (high g x-Richtung) - Kommunikationsstoerung | 0 | ZP |
| 0x01500A | Airbagsensor-Cluster (high g y-Richtung) - Plausibilitaetsfehler | 0 | ST |
| 0x01500B | Airbagsensor-Cluster (high g y-Richtung) - Kommunikationsstoerung | 0 | ZP |
| 0x01500D | Airbagsensor-Cluster (SBS-Sensor) - Kommunikationsstoerung | 0 | ZP |
| 0x01500E | Airbagsensor-Cluster (low g y-Richtung) - Plausibilitaetsfehler | 0 | ST |
| 0x01500F | Airbagsensor-Cluster (low g y-Richtung) - Kommunikationsstoerung | 0 | ZP |
| 0x015010 | Airbagsensor-Cluster (low g z-Richtung) - Plausibilitaetsfehler | 0 | ST |
| 0x015011 | Airbagsensor-Cluster (low g z-Richtung) - Kommunikationsstoerung | 0 | ZP |
| 0x015012 | Airbagsensor-Cluster (Drehrate) - Plausibilitaetsfehler | 0 | ST |
| 0x015013 | Airbagsensor-Cluster (Drehrate) - Kommunikationsstoerung | 0 | ZP |
| 0x015014 | FGS_SB Fussgängerschutzsensor Kanal 1 - Plausibilitaetsfehler | 0 | ST |
| 0x015015 | FGS_SB Fussgängerschutzsensor Kanal 1- sendet Fehler | 0 | ZP |
| 0x015016 | FGS_SB Fussgängerschutzsensor Kanal 1 - Sensortyp falsch | 0 | ZP |
| 0x015017 | FGS_SB Fussgängerschutzsensor Kanal 1 - Kommunikationsstoerung | 0 | ZP |
| 0x015018 | FGS_SB Fussgängerschutzsensor Kanal 1 - Signalplausibilitaetsfehler | 0 | ZP |
| 0x015019 | FGS_SB Fussgängerschutzsensor Kanal 2- Plausibilitaetsfehler | 0 | ST |
| 0x01501A | FGS_SB Fussgängerschutzsensor Kanal 2- sendet Fehler | 0 | ZP |
| 0x01501B | FGS_SB Fussgängerschutzsensor Kanal 2 - Sensortyp falsch | 0 | ZP |
| 0x01501C | FGS_SB Fussgängerschutzsensor Kanal 2 - Kommunikationsstoerung | 0 | ZP |
| 0x01501D | FGS_SB Fussgängerschutzsensor Kanal 2 - Signalplausibilitaetsfehler | 0 | ZP |
| 0x01501E | FGS_SB Fussgängerschutzsensor Kanal 3- Plausibilitaetsfehler | 0 | ST |
| 0x01501F | FGS_SB Fussgängerschutzsensor Kanal 3- sendet Fehler | 0 | ZP |
| 0x015020 | FGS_SB Fussgängerschutzsensor Kanal 3 - Sensortyp falsch | 0 | ZP |
| 0x015021 | FGS_SB Fussgängerschutzsensor Kanal 3 - Kommunikationsstoerung | 0 | ZP |
| 0x015022 | FGS_SB Fussgängerschutzsensor Kanal 3 - Signalplausibilitaetsfehler | 0 | ZP |
| 0x015023 | FltSWVersion | 0 | ZP |
| 0x015024 | EEPROM Layout Mismatch | 0 | ZP |
| 0x016000 | Referenzzündpille ATIC 129 1 | 0 | TODO |
| 0x016001 | Referenzzündpille ATIC 129 2 | 0 | TODO |
| 0x016002 | Referenzzündpille ATIC 129 3 | 0 | TODO |
| 0x016003 | Referenzzündpille ATIC 99 | 0 | TODO |
| 0x016010 | Interne Spannung ATIC 129 1 | 0 | TODO |
| 0x016011 | Interne Spannung ATIC 129 2 | 0 | TODO |
| 0x016012 | Interne Spannung ATIC 129 3 | 0 | TODO |
| 0x016013 | Interne Sapannung ATIC 99 | 0 | TODO |
| 0x016020 | Zündspannung ATIC 129 1 | 0 | TODO |
| 0x016021 | Zündspannung ATIC 129 2 | 0 | TODO |
| 0x016022 | Zündspannung ATIC 129 3 | 0 | TODO |
| 0x016023 | Zündspannung ATIC 99 | 0 | TODO |
| 0x016030 | ROM CRC fehlgeschlagen | 0 | TODO |
| 0x016031 | RAM Start-up Test fehlgeschlagen | 0 | TODO |
| 0x016032 | RAM CRC fehlgeschlagen | 0 | TODO |
| 0x016035 | Safing Transistor Test fehlgeschlagen | 0 | TODO |
| 0x016040 | Parameter-CRC-Fehler Algorithmus, Seite | 0 | TODO |
| 0x016041 | Parameter-CRC-Fehler Algorithmus, Front | 0 | TODO |
| 0x016042 | Parameter-CRC-Fehler Algorithmus, Heck | 0 | TODO |
| 0x016043 | Parameter-CRC-Fehler Algorithmus, Rollover | 0 | TODO |
| 0x016045 | Parameter-CRC-Fehler Zündpillengrenzen | 0 | TODO |
| 0x016046 | Parameter-CRC-Fehler Hall-Sensoren-Limits | 0 | TODO |
| 0x016047 | Parameter-CRC-Fehler IASG | 0 | TODO |
| 0x01604A | Parameter-CRC-Fehler Satelliten, Sensierungsrichtung | 0 | TODO |
| 0x016050 | Low Side Schalter Zündendstufe defekt ATIC 99 | 0 | TODO |
| 0x016051 | Low Side Schalter Zündendstufe defekt ATIC 129 1 | 0 | TODO |
| 0x016052 | Low Side Schalter Zündendstufe defekt ATIC 129 2 | 0 | TODO |
| 0x016053 | Low Side Schalter Zündendstufe defekt ATIC 129 3 | 0 | TODO |
| 0x016054 | Low Side Schalter Zündendstufe defekt Rollover 1 | 0 | TODO |
| 0x016055 | Low Side Schalter Zündendstufe defekt Rollover 2 | 0 | TODO |
| 0x016060 | High Side Schalter Zündendstufe defekt ATIC 99 | 0 | TODO |
| 0x016061 | High Side Schalter Zündendstufe defekt ATIC 129 1 | 0 | TODO |
| 0x016062 | High Side Schalter Zündendstufe defekt ATIC 129 2 | 0 | TODO |
| 0x016063 | High Side Schalter Zündendstufe defekt ATIC 129 3 | 0 | TODO |
| 0x016064 | High Side Schalter Zündendstufe defekt Rollover 1 | 0 | TODO |
| 0x016065 | High Side Schalter Zündendstufe defekt Rollover 2 | 0 | TODO |
| 0x016070 | Zündstrom, Zündzeit Konfiguration fehlgeschlagen ATIC 99 | 0 | TODO |
| 0x016071 | Zündstrom, Zündzeit Konfiguration fehlgeschlagen ATIC 129 1 | 0 | TODO |
| 0x016072 | Zündstrom, Zündzeit Konfiguration fehlgeschlagen ATIC 129 2 | 0 | TODO |
| 0x016073 | Zündstrom, Zündzeit Konfiguration fehlgeschlagen ATIC 129 3 | 0 | TODO |
| 0x016090 | Zündfreigabeleitungen: ARMQ Satellit Fehler | 0 | TODO |
| 0x016091 | Zündfreigabeleitungen: ARMQ OMNI Fehler | 0 | TODO |
| 0x016092 | Zündfreigabeleitungen: ARMQ HSX Fehler | 0 | TODO |
| 0x016093 | Zündfreigabeleitungen: TestMQ Fehler | 0 | TODO |
| 0x016094 | Zündfreigabeleitungen: Fehler in Freigabeleitung | 0 | TODO |
| 0x016095 | Zündfreigabeleitungen: ARMI SCRAP Fehler | 0 | TODO |
| 0x016096 | LSEN2Q Fehler | 0 | TODO |
| 0x016097 | HS RES LEAK TO GROUND Fehler | 0 | TODO |
| 0x016098 | LD 1 OPEN Fehler | 0 | TODO |
| 0x016099 | LD 2 OPEN Fehler | 0 | TODO |
| 0x01609A | HS RES LEAK TO UBATT Fehler | 0 | TODO |
| 0x01609B | VZ FA Fehler | 0 | TODO |
| 0x01609C | VSGC Fault | 0 | TODO |
| 0x01609D | Rollover CAPA Measurement | 0 | TODO |
| 0x0160A0 | Energiereserve-Kondensator: Kapazität zu klein oder nicht vorhanden | 0 | TODO |
| 0x0160B0 | Autarkiezeit zu klein | 0 | TODO |
| 0x0160C0 | Microcontroller Ports verkoppelte/offene uC-Pins | 0 | TODO |
| 0x0160E2 | CANNM_E_NETWORK_TIMEOUT | 0 | TODO |
| 0x0160F0 | CANTP_E_COM | 0 | TODO |
| 0x0160F1 | CANTP_E_OPER_NOT_SUPPORTED | 0 | TODO |
| 0x016110 | EEP_E_WORN_OUT | 0 | TODO |
| 0x016111 | EEP_E_READY_SECTORS | 0 | TODO |
| 0x016140 | Fehlerspeicher gesperrt wegen Crasheintrag | 0 | TODO |
| 0x016141 | Fehlerspeicher gesperrt wegen Crasheintrag | 0 | TODO |
| 0x016170 | ECUM_E_RAM_CHECK_FAILED | 0 | TODO |
| 0x016171 | ECUM_E_RAM_CHECKED_FAILED | 0 | TODO |
| 0x016181 | VSM_EVENT_OPMODE_OLD | 0 | TODO |
| 0x016200 | DARH_EVENT_ID_DELETE_ERROR_ | 0 | TODO |
| 0x016201 | Information Code Phase 2A | 0 | TODO |
| 0x016202 | Information Code Phase 2B | 0 | TODO |
| 0x016203 | Information Code Phase 3A | 0 | TODO |
| 0x016204 | Information Code Phase 3B | 0 | TODO |
| 0x016205 | Information Code Phase 3C | 0 | TODO |
| 0x016206 | &gt;Information Code Phase 3D | 0 | TODO |
| 0x016207 | Information Code Phase 3E | 0 | TODO |
| 0x016208 | Information Code Phase COMPLETED | 0 | TODO |
| 0x016209 | VRCM Fehler ATIC 99 | 0 | TODO |
| 0x01620A | Internal Fault ATIC 99 | 0 | TODO |
| 0x01620B | Hal Undervoltage Fault | 0 | TODO |
| 0x01620C | Hal Overvoltage Fault | 0 | TODO |
| 0x01620D | Hal Internal Undervoltage Fault ACE4 | 0 | TODO |
| 0x01620E | Hal Internal Overvoltage Fault ACE4 | 0 | TODO |
| 0x01620F | Hal Internal Undervoltage Fault AFS1 | 0 | TODO |
| 0x016210 | Hal Internal Overvoltage Fault AFS1 | 0 | TODO |
| 0x016211 | Hal Internal Undervoltage Fault AFS2 | 0 | TODO |
| 0x016212 | Hal Internal Overvoltage Fault AFS2 | 0 | TODO |
| 0x016214 | Hal Internal Undervoltage Fault AFS3 | 0 | TODO |
| 0x016215 | Hal Internal Overvoltage Fault AFS3 | 0 | TODO |
| 0x016218 | Spi Asic | 0 | TODO |
| 0x016219 | SQRef AFS1 | 0 | TODO |
| 0x01621A | SQRef AFS2 | 0 | TODO |
| 0x01621D | FLEN | 0 | TODO |
| 0x01621E | Capacity Missing | 0 | TODO |
| 0x01621F | Capa Meas | 0 | TODO |
| 0x016220 | Reset | 0 | TODO |
| 0x016221 | Exception | 0 | TODO |
| 0x016222 | Watchdog Fail | 0 | TODO |
| 0x016223 | Autarchy Time | 0 | TODO |
| 0x016224 | ROM CRC Fail | 0 | TODO |
| 0x016225 | RAM CRC Fail | 0 | TODO |
| 0x016226 | Stack Cyclic Fail | 0 | TODO |
| 0x016227 | EEPROM CRC Fail | 0 | TODO |
| 0x016228 | Vref | 0 | TODO |
| 0x01622B | IC Side Algo Started | 0 | TODO |
| 0x01622C | IC Side Algo Reset | 0 | TODO |
| 0x01622D | IC Conn KL15 | 0 | TODO |
| 0x01622E | IC Capa Meas NOK | 0 | TODO |
| 0x01622F | IC Capa Meas Skipped | 0 | TODO |
| 0x016230 | IC_ATIC95 1 SPIERR | 0 | TODO |
| 0x016231 | IC_ATIC95 2 SPIERR | 0 | TODO |
| 0x016232 | IASG Multiplex-Treiber defekt  | 0 | TODO |
| 0x016233 | ATIC 99 diskrete Hardware Verkopplungsnetzwerk defekt | 0 | TODO |
| 0x016300 | Fehlerspeicher gesperrt wegen Diagnosebefehl | 0 | TODO |
| 0x016301 | Fehlerspeicher gesperrt wegen Crasheintrag | 0 | TODO |
| 0xC95423 | ICM: Lenkwinkel Vorderachse effektiv - Signal ungültig | 1 | ZP |
| 0xFFFFFF | unbekannter Fehlerort | 0 | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 8 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4000 | STAT_BETRIEBSSTUNDENZAEHLER_BEGINN | s | high | unsigned long | - | - | - | - |
| 0x4001 | STAT_BETRIEBSSTUNDENZAEHLER_ENDE | s | high | unsigned long | - | - | - | - |
| 0x4002 | STAT_SG_TEMP_WERT | 0-n | - | 0xFF | T_TAB_INNENTEMPERATUR_SG_DOP_UW | - | - | - |
| 0x4003 | STAT_SYSTEMZUSTAND | text | high | 5 | - | - | - | - |
| 0x4004 | STAT_ZEIT_NACH_POR | s | high | unsigned int | - | - | - | - |
| 0x4005 | STAT_POWER_ON_ZAEHLER | - | high | unsigned long | - | - | - | - |
| 0x4006 | STAT_BATTERIESPANNUNG_AM_SG | - | - | unsigned char | - | - | - | - |
| 0x400A | STAT_AUSSENTEMPERATUR | °C | - | unsigned char | - | 0,5 | - | -40,0 |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 2 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SC_VERSION | 0x1720 | - | Standard Core Version | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x1720 |
| VIN | 0xF190 | STAT_VIN_WERT | Fahrgestellnummer | - | - | high | string[17] | - | - | - | - | - | 22 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 8 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4000 | STAT_BETRIEBSSTUNDENZAEHLER_BEGINN | s | high | unsigned long | - | - | - | - |
| 0x4001 | STAT_BETRIEBSSTUNDENZAEHLER_ENDE | s | high | unsigned long | - | - | - | - |
| 0x4002 | STAT_SG_TEMP_WERT | 0-n | - | 0xFF | T_TAB_INNENTEMPERATUR_SG_DOP_UW | - | - | - |
| 0x4003 | STAT_SYSTEMZUSTAND | text | high | 5 | - | - | - | - |
| 0x4004 | STAT_ZEIT_NACH_POR | s | high | unsigned int | - | - | - | - |
| 0x4005 | STAT_POWER_ON_ZAEHLER | - | high | unsigned long | - | - | - | - |
| 0x4006 | STAT_BATTERIESPANNUNG_AM_SG | - | - | unsigned char | - | - | - | - |
| 0x400A | STAT_AUSSENTEMPERATUR | °C | - | unsigned char | - | 0,5 | - | -40,0 |

<a id="table-t-tab-dtc-debug-info-loeschen-dop"></a>
### T_TAB_DTC_DEBUG_INFO_LOESCHEN_DOP

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 61457 | 1 |
| 61458 | 2 |
| 61459 | 3 |

<a id="table-t-tab-dtc-debug-info-lesen-dop"></a>
### T_TAB_DTC_DEBUG_INFO_LESEN_DOP

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 16481 | 1 |
| 16482 | 2 |
| 16483 | 3 |

<a id="table-t-tab-diagnoseart-aendern-dop"></a>
### T_TAB_DIAGNOSEART_AENDERN_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 61952 | BMW_DIAG |
| 61953 | SUPPL_DIAG |

<a id="table-t-cd-dop"></a>
### T_CD_DOP

Dimensions: 24 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 12288 | CAF 1 AUSSTATTUNGSFLAGS |
| 12289 | CAF 1 SEAT_BELT_REMINDER |
| 12290 | CAF 1 BMW_WERKNUMMER |
| 12291 | CAF 1 HAENDLER_NUMMER_CODIERDATUM_BAUREIHE |
| 12292 | CAF 1 ABGLEICHPARAMETER |
| 12293 | CAF 1 CIS-PARAMETER |
| 12304 | CAF 1 CRS-FLAGS |
| 12312 | CAF 1 CAFID_1 |
| 12313 | CAF 1 SIGNATUR |
| 12320 | CAF 2 ZUENDMITTELZUORDUNGSTABELLE |
| 12336 | CAF 2 CRS-TIME-DELAY_0-75 |
| 12337 | CAF 2 CRS-TIME-DELAY_CHECKSUMME |
| 12352 | CAF 2 ALGO_KENNUNG_BYTE_0-19 |
| 12353 | CAF 2 PARAMETER_UND_PARAMETERSATZ_CHECKSUMME |
| 12538 | CAF 2 BMW_WERKNUMMER |
| 12539 | CAF 2 HAENDLER_NUMMER_CODIERDATUM_BAUREIHE |
| 12540 | CAF 2 CAFID_2 |
| 12541 | CAF 2 SIGNATUR |
| 12544 | CAF 3 ALGO_KENNUNG_BYTE_0-19 |
| 12545 | CAF 3 PARAMETER_UND_PARAMETERSATZ_CHECKSUMME |
| 12570 | CAF 3 BMW_WERKSNUMMER |
| 12571 | CAF 3 HAENDLER_NUMMER_CODIERDATEN_BAUREIHE |
| 12572 | CAF 3 CAFID_3 |
| 12573 | CAF 3 SIGNATUR |

<a id="table-res-0x1720"></a>
### RES_0X1720

Dimensions: 4 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_GENERATION_WERT | HEX | - | unsigned char | - | - | - | - | - | Generation |
| STAT_FEATURESET_WERT | HEX | - | unsigned char | - | - | - | - | - | Featureset |
| STAT_BUGFIX_WERT | HEX | - | unsigned char | - | - | - | - | - | Bugfix |
| STAT_RESERVIERT_WERT | HEX | - | unsigned char | - | - | - | - | - | reserviert |

<a id="table-t-tab-fahrtrichtung"></a>
### T_TAB_FAHRTRICHTUNG

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Fahrzeug steht |
| 1 | Fahrzeug faehrt vorwaerts |
| 2 | Fahrzeug faehrt rueckwaerts |
| 3 | Fahrzeug faehrt |
| 4 | Fahrzeug steht, Hinterachse auf Rollenpruefstand erkannt |
| 5 | Fahrzeug steht, Zweiachs-Rollenbetrieb gesetzt |
| 255 | Signal ungueltig |

<a id="table-t-tab-aacn"></a>
### T_TAB_AACN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | AACN Sendet nicht |
| 1 | AACN Sendet kein Notruf |
| 2 | AACN Sendet Notruf |
| 255 | nicht definiert |

<a id="table-t-tab-innentemperatur-sg-dop-uw"></a>
### T_TAB_INNENTEMPERATUR_SG_DOP_UW

Dimensions: 203 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 1 | -49 °C |
| 2 | -48 °C |
| 3 | -47 °C |
| 4 | -46 °C |
| 5 | -45 °C |
| 6 | -44 °C |
| 7 | -43 °C |
| 8 | -42 °C |
| 9 | -41 °C |
| 10 | -40 °C |
| 11 | -39 °C |
| 12 | -38 °C |
| 13 | -37 °C |
| 14 | -36 °C |
| 15 | -35 °C |
| 16 | -34 °C |
| 17 | -33 °C |
| 18 | -32 °C |
| 19 | -31 °C |
| 20 | -30 °C |
| 21 | -29 °C |
| 22 | -28 °C |
| 23 | -27 °C |
| 24 | -26 °C |
| 25 | -25 °C |
| 26 | -24 °C |
| 27 | -23 °C |
| 28 | -22 °C |
| 29 | -21 °C |
| 30 | -20 °C |
| 31 | -19 °C |
| 32 | -18 °C |
| 33 | -17 °C |
| 34 | -16 °C |
| 35 | -15 °C |
| 36 | -14 °C |
| 37 | -13 °C |
| 38 | -12 °C |
| 39 | -11 °C |
| 40 | -10 °C |
| 41 | -9 °C |
| 42 | -8 °C |
| 43 | -7 °C |
| 44 | -6 °C |
| 45 | -5 °C |
| 48 | -2 °C |
| 49 | -1 °C |
| 50 | 0 °C |
| 51 | 1 °C |
| 52 | 2 °C |
| 53 | 3 °C |
| 54 | 4 °C |
| 55 | 5 °C |
| 56 | 6 °C |
| 57 | 7 °C |
| 58 | 8 °C |
| 59 | 9 °C |
| 60 | 10 °C |
| 61 | 11 °C |
| 62 | 12 °C |
| 63 | 13 °C |
| 64 | 14 °C |
| 65 | 15 °C |
| 66 | 16 °C |
| 67 | 17 °C |
| 68 | 18 °C |
| 69 | 19 °C |
| 70 | 20 °C |
| 71 | 21 °C |
| 72 | 22 °C |
| 73 | 23 °C |
| 74 | 24 °C |
| 75 | 25 °C |
| 76 | 26 °C |
| 77 | 27 °C |
| 78 | 28 °C |
| 79 | 29 °C |
| 80 | 30 °C |
| 81 | 31 °C |
| 82 | 32 °C |
| 83 | 33 °C |
| 84 | 34 °C |
| 85 | 35 °C |
| 86 | 36 °C |
| 87 | 37 °C |
| 88 | 38 °C |
| 89 | 39 °C |
| 90 | 40 °C |
| 91 | 41 °C |
| 92 | 42 °C |
| 93 | 43 °C |
| 94 | 44 °C |
| 95 | 45 °C |
| 96 | 46 °C |
| 97 | 47 °C |
| 98 | 48 °C |
| 99 | 49 °C |
| 100 | 50 °C |
| 101 | 51 °C |
| 102 | 52 °C |
| 103 | 53 °C |
| 104 | 54 °C |
| 105 | 55 °C |
| 106 | 56 °C |
| 107 | 57 °C |
| 108 | 58 °C |
| 109 | 59 °C |
| 110 | 60 °C |
| 111 | 61 °C |
| 112 | 62 °C |
| 113 | 63 °C |
| 114 | 64 °C |
| 115 | 65 °C |
| 116 | 66 °C |
| 117 | 67 °C |
| 118 | 68 °C |
| 119 | 69 °C |
| 120 | 70 °C |
| 121 | 71 °C |
| 122 | 72 °C |
| 123 | 73 °C |
| 124 | 74 °C |
| 125 | 75 °C |
| 126 | 76 °C |
| 127 | 77 °C |
| 128 | 78 °C |
| 129 | 79 °C |
| 130 | 80 °C |
| 132 | 82 °C |
| 133 | 83 °C |
| 134 | 84 °C |
| 135 | 85 °C |
| 137 | 87 °C |
| 138 | 88 °C |
| 140 | 90 °C |
| 141 | 91 °C |
| 143 | 93 °C |
| 144 | 94 °C |
| 146 | 96 °C |
| 148 | 98 °C |
| 150 | 100 °C |
| 151 | 101 °C |
| 153 | 103 °C |
| 156 | 106 °C |
| 158 | 108 °C |
| 160 | 110 °C |
| 163 | 113 °C |
| 166 | 116 °C |
| 168 | 118 °C |
| 172 | 122 °C |
| 171 | 121 °C |
| 170 | 120 °C |
| 169 | 119 °C |
| 167 | 117 °C |
| 165 | 115 °C |
| 164 | 114 °C |
| 162 | 112 °C |
| 161 | 111 °C |
| 159 | 109 °C |
| 157 | 107 °C |
| 155 | 105 °C |
| 154 | 104 °C |
| 152 | 102 °C |
| 0 | -50 °C |
| 46 | -4 °C |
| 47 | -3 °C |
| 131 | 81 °C |
| 136 | 86 °C |
| 139 | 89 °C |
| 142 | 92 °C |
| 145 | 95 °C |
| 147 | 97 °C |
| 149 | 99 °C |
| 173 | 123 °C |
| 174 | 124 °C |
| 175 | 125 °C |
| 176 | 126 °C |
| 177 | 127 °C |
| 178 | 128 °C |
| 179 | 129 °C |
| 180 | 130 °C |
| 181 | 131 °C |
| 182 | 132 °C |
| 183 | 133 °C |
| 184 | 134 °C |
| 185 | 135 °C |
| 186 | 136 °C |
| 187 | 137 °C |
| 188 | 138 °C |
| 189 | 139 °C |
| 190 | 140 °C |
| 191 | 141 °C |
| 192 | 142 °C |
| 193 | 143 °C |
| 194 | 144 °C |
| 195 | 145 °C |
| 196 | 146 °C |
| 197 | 147 °C |
| 198 | 148 °C |
| 199 | 149 °C |
| 200 | 150 °C |
| 201 | unbekannt |
| 255 | Fehler |

<a id="table-t-tab-caf-nr-dop"></a>
### T_TAB_CAF_NR_DOP

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 12291 | CAF1 |
| 12539 | CAF2 |
| 12571 | CAF3 |

<a id="table-t-tab-baureihenkennung"></a>
### T_TAB_BAUREIHENKENNUNG

Dimensions: 31 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 64 | F01 |
| 65 | F02 |
| 66 | F03 |
| 67 | F04 |
| 68 | F07 |
| 80 | F10 |
| 81 | F11 |
| 82 | F12 |
| 83 | F13 |
| 84 | F18 |
| 85 | F06 |
| 96 | RR4 |
| 97 | RR05 |
| 112 | F25 |
| 117 | F15 |
| 118 | F16 |
| 128 | F20 |
| 129 | F22 |
| 130 | F23 |
| 131 | F30 |
| 132 | F31 |
| 133 | F32 |
| 134 | F33 |
| 135 | F21 |
| 136 | F34 |
| 137 | F35 |
| 160 | F80 |
| 161 | F82 |
| 162 | F83 |
| 163 | F36 |
| 255 | unbekannte Baureihe |

<a id="table-t-tab-edr-public-data-lesen-dop"></a>
### T_TAB_EDR_PUBLIC_DATA_LESEN_DOP

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 64019 | 1 |
| 64020 | 2 |
| 64021 | 3 |
| 64022 | 4 |
| 64023 | 5 |

<a id="table-t-tab-wochentag-structure-dop"></a>
### T_TAB_WOCHENTAG_STRUCTURE_DOP

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | MONTAG |
| 2 | DIENSTAG |
| 3 | MITTWOCH |
| 4 | DONNERSTAG |
| 5 | FREITAG |
| 6 | SAMSTAG |
| 7 | SONNTAG |
| 8 | SIGNAL UNGUELTIG |

<a id="table-t-tab-sg-temp-zustand"></a>
### T_TAB_SG_TEMP_ZUSTAND

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | in Ordnung |
| 201 | unbekannt |
| 255 | ungueltig |

<a id="table-t-tab-near-crash-daten-lesen-dop"></a>
### T_TAB_NEAR_CRASH_DATEN_LESEN_DOP

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 16419 | 1 |
| 16420 | 2 |
