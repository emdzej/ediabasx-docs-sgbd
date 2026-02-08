# lmv_01.prg

- Jobs: [77](#jobs)
- Tables: [66](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Längsmomentverteilung |
| ORIGIN | BMW EA-515 Joerg_Fischer |
| REVISION | 7.003 |
| AUTHOR | Magna_Steyr EEC H._Sauer, Magna_Steyr HES G._Suppan, Magna_Stey |
| COMMENT | - |
| PACKAGE | 1.40 |
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
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [CBS_INFO](#job-cbs-info) - Ausgabe der CBS-Version
- [CBS_DATEN_LESEN](#job-cbs-daten-lesen) - CBS Daten auslesen (fuer CBS-Version 5) UDS: $22 ReadDataByIdentifier Modus  : Default
- [CBS_RESET](#job-cbs-reset) - CBS Daten Zuruecksetzen (fuer CBS-Version 5) UDS: $2E WriteDataByIdentifier Modus  : Default Musterparametersatz fuer Bremsbelagverschleiss Vorder/Hinterachse br_v,100,1,0,0,0,1,0,0 br_h,100,1,0,0,0,1,0,0 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma!)
- [STEUERN_ROE_STOP](#job-steuern-roe-stop) - Temporaeres Deaktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $00 Stop $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)
- [STATUS_ROE_REPORT](#job-status-roe-report) - Abfrage Status der Aktivierung der aktiven Fehlermeldung UDS: $86 ResponseOnEvent $04 report activated events [$02 eventWindowTime - infinite (nur 35up)] 35up: LH Diagnosemaster V11 oder höher pre35up: LH Diagnosemaster V6 - V9
- [STEUERN_ROE_START](#job-steuern-roe-start) - Temporaeres Aktivieren der aktiven Fehlermeldung UDS   : $86 ResponseOnEvent $05 Start $02 (EventWindowTime) gültig für LH Diagnosemaster V9 oder früher. (pre 35up)
- [STEUERN_ROE_PERSISTENT_STOP](#job-steuern-roe-persistent-stop) - Persistentes Deaktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $40 Stop persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [STEUERN_ROE_PERSISTENT_START](#job-steuern-roe-persistent-start) - Persistentes Aktivieren der aktiven Fehlermeldung an den Diagnosemaster ueber TAS UDS   : $86 ResponseOnEvent $45 Start persistent $02 (EventWindowTime) gültig für LH Diagnosemaster V6 - V12 (Stand 2013)
- [CALID_CVN_LESEN](#job-calid-cvn-lesen) - OBD Calibration ID, CVN Calibration verification number UDS  : $22   ReadDataByIdentifier UDS  : $2541 CAL-ID Calibration ID and CVN Calibration verification number
- [CPS_LESEN](#job-cps-lesen) - Codierpruefstempel lesen UDS  : $22   ReadDataByIdentifier UDS  : $37FE DataIdentifier Codierpruefstempel Modus: Default
- [DIAG_SESSION_LESEN](#job-diag-session-lesen) - Aktive Diagnose-Session auslesen UDS  : $22   ReadDataByIdentifier UDS  : $F186 ActiveDiagnosticSession Modus: Default
- [FLASH_TP_LESEN](#job-flash-tp-lesen) - Flash Timing Parameter auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2504 FlashTimingParameter Modus: Default
- [PROG_ZAEHLER_LESEN](#job-prog-zaehler-lesen) - Programmierzaehler lesen UDS  : $22   ReadDataByIdentifier UDS  : $2502 ProgrammingCounter Modus: Default
- [PROG_MAX_LESEN](#job-prog-max-lesen) - Anzahl der maximal möglichen Programmiervorgänge auslesen UDS  : $22   ReadDataByIdentifier UDS  : $2503 ProgrammingCounter Modus: Default
- [STATUS_AKTUATOR_MOTORREGLER](#job-status-aktuator-motorregler) - Ein- Ausgangsgrößen Aktuator Motorregler
- [STATUS_ATIC](#job-status-atic) - Fehlerspeicherregister und Initialisierungsregister des ATIC106
- [STATUS_AUTOCODIERUNG](#job-status-autocodierung) - Codierstatus / daten
- [STATUS_CALCVN](#job-status-calcvn) - Auslesen von Cal-ID und CVN
- [STATUS_FAHRZEUGZUSTAND](#job-status-fahrzeugzustand) - Eingangsdaten aus dem Fahrzeugzustandsmanagement
- [STATUS_GETRIEBEKLASSE](#job-status-getriebeklasse) - Getriebeklasse, Offset- und Steigungsklassierung Verteilergetriebe Dieser Job kann erst ab 09/2011 bzw. ab einer Software-Version ab 000.020.000 verwendet werden.
- [STATUS_INTEGRATOREN](#job-status-integratoren) - HO Getriebe und Lamellen Schädigungs Integratoren
- [STATUS_ISTMOMENT](#job-status-istmoment) - Momenten Istwert und Qualifier vom LMV
- [STATUS_KALIBRIERUNG](#job-status-kalibrierung) - Kalibrierstatus / daten
- [STATUS_KLASSIERUNG](#job-status-klassierung) - Offset / Steigungsklassierung Verteilergetriebe
- [STATUS_KLEMMENSPANNUNG](#job-status-klemmenspannung) - Spannungen an den LMV Eingangsklemmen
- [STATUS_KUPPLUNGSSTATUS](#job-status-kupplungsstatus) - Service - Qualifier des LMV
- [STATUS_LT_INTEGRATOREN](#job-status-lt-integratoren) - Lifetime Getriebe und Lamellen Schädigungs Integratoren
- [STATUS_PRUEFSTAND](#job-status-pruefstand) - Pruefstandsmodus Status / Daten
- [STATUS_SOLLMOMENT](#job-status-sollmoment) - Momenten Sollwert und Qualifier
- [STATUS_SYSINFO_LESEN](#job-status-sysinfo-lesen) - Liest die Information der in Getriebe befindlichen Softwarekomponenten aus Achtung: STAT_ATIC_ID_* nur direkt nach einem Power-up gültig!
- [STATUS_TEMPERATURHISTOGRAMM](#job-status-temperaturhistogramm) - Temperaturverteilung LMV SG / Betriebszeit
- [STATUS_VERTEILERGETRIEBE](#job-status-verteilergetriebe) - Verteilergetriebedaten für FASTA Auswertung
- [STATUS_VTG_SN_LESEN](#job-status-vtg-sn-lesen) - Liest die VTG-SN aus (wird am Getriebe EOL geschrieben)
- [STEUERN_AUTOCODIERUNG_DEFAULT](#job-steuern-autocodierung-default) - Aktivierung eines uncodierten SG mit Default Werten Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein Achtung: Dieser Job kann nur innerhalb von 20 Sekunden nach Kl15ein aktiviert werden!
- [STEUERN_CODIERDATEN_RUECKSETZEN](#job-steuern-codierdaten-ruecksetzen) - Codierdaten im EEPROM loeschen Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein
- [STEUERN_DISABLE_CHECK_CRC_ALIVE](#job-steuern-disable-check-crc-alive) - Schaltet die Botschaftsabsicherung mittels CRC und Alive Counter bis zum nächsten SG Neustart aus Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein
- [STEUERN_FUNKTIONSPRUEFUNG](#job-steuern-funktionspruefung) - Funktionsprüfung der Kupplung mit vorherigem löschen des Kalibrierwinkels Bedingungen: Wenn (vFzg &lt; 3 km/h && VKMaus && KL15ein && gültige Klassierung) oder (vFzg &lt; 3 km/h && VKMein && MKsoll &lt; 10 Nm && gültige Klassierung)
- [STEUERN_GETRIEBEKLASSE_RUECKSETZEN](#job-steuern-getriebeklasse-ruecksetzen) - Setzt die Klassierinformation im EEPROM auf den Initialwert (unklassiert) zurück Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein Dieser Job kann erst ab 09/2011 bzw. ab einer Software-Version ab 000.020.000 verwendet werden.
- [STEUERN_GETRIEBEKLASSE_SETZEN](#job-steuern-getriebeklasse-setzen) - Setzt die Klassierinformation im EEPROM auf die Werte des Arguments Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein Dieser Job kann erst ab 09/2011 bzw. ab einer Software-Version ab 000.020.000 verwendet werden.
- [STEUERN_INTEGRATOREN_LOESCHEN](#job-steuern-integratoren-loeschen) - HO Getriebe und Lamellenintegratoren zurücksetzen Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein
- [STEUERN_KALIBRIERUNG_LOESCHEN](#job-steuern-kalibrierung-loeschen) - Kalibrierwinkel im EEPROM loeschen Bedingungen: Wenn (vFzg &lt; 3 km/h && VKMaus && KL15ein) oder (vFzg &lt; 3 km/h && VKMein && MKsoll &lt; 10 Nm)
- [STEUERN_KLASSIERSPEICHER_RUECKSETZEN](#job-steuern-klassierspeicher-ruecksetzen) - Setzt die Klassierinformation im EEPROM auf den Initialwert (unklassiert) zurück Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein
- [STEUERN_KLASSIERSPEICHER_SETZEN](#job-steuern-klassierspeicher-setzen) - Setzt die Klassierinformation im EEPROM auf die Werte des Arguments Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein
- [STEUERN_KUPPLUNG_FUNKTIONSPRUEFUNG](#job-steuern-kupplung-funktionspruefung) - Funktionsprüfung der Kupplung Bedingungen: Wenn (vFzg &lt; 3 km/h && VKMaus && KL15ein && gültige Klassierung) oder (vFzg &lt; 3 km/h && VKMein && MKsoll &lt; 10 Nm && gültige Klassierung)
- [STEUERN_LT_INTEGRATOREN_LOESCHEN](#job-steuern-lt-integratoren-loeschen) - Lifetime Getriebe und Lamellenintegratoren zurücksetzen Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein
- [STEUERN_PRUEFSTAND](#job-steuern-pruefstand) - Setzt SG intern eine Sollmomentenvorgabe ohne Restbussimulation
- [WRITE_GETRIEBE_INTEGRATOREN](#job-write-getriebe-integratoren) - Schreibt die HO Getriebe Integratoren und den Intervall km Stand ins EEPROM Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein
- [WRITE_LAMELLEN_INTEGRATOREN](#job-write-lamellen-integratoren) - Schreibt die HO Lamellen Integratoren ins EEPROM Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein
- [WRITE_LT_GETRIEBE_INTEGRATOREN](#job-write-lt-getriebe-integratoren) - Schreibt die LT Getriebe Integratoren ins EEPROM Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein
- [WRITE_LT_LAMELLEN_INTEGRATOREN](#job-write-lt-lamellen-integratoren) - Schreibt die LT Lamellen Integratoren ins EEPROM Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein
- [WRITE_SOLLMOMENT](#job-write-sollmoment) - Setzt SG intern eine Sollmomentenvorgabe und den Sollwertqualifier auf 'Sollwert umsetzen' Bedingungen: v_fzg &lt; 20 km/h && VKMein && Kl15 ein
- [WRITE_VTG_SN](#job-write-vtg-sn) - Schreibt eine 20 stellige Getriebe SN ins EEPROM Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein

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
| F_HFK | int | Haeufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Heilungsszaehler |
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
| F_HFK | int | Haeufigkeitszaehler als Zahl Wertebereich 0 - 255 Bei mehr als 255 bleibt Zaehler stehen. Kein Ueberlauf |
| F_HLZ | int | Heilungsszaehler als Zahl Wertebereich 0 - 255 -1: ohne Heilungsszaehler |
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
| CBS_VERFUEGBARKEIT | int | gewuenschte Verfuegbarkeit in Prozent: 0-100 Schalter, keine Aenderung: 0xFFh (255 dez) Defaultwert: 100 (0x64h) Bremflüssigkeit: 150 (0x96h) erlaubt |
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

<a id="job-calid-cvn-lesen"></a>
### CALID_CVN_LESEN

OBD Calibration ID, CVN Calibration verification number UDS  : $22   ReadDataByIdentifier UDS  : $2541 CAL-ID Calibration ID and CVN Calibration verification number

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ANZAHL_CALID_CVN | int | Anzahl der CAL-ID CVN Paare |
| CALID | string | Calibration ID |
| CVN | string | Calibration verification number |
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

<a id="job-status-aktuator-motorregler"></a>
### STATUS_AKTUATOR_MOTORREGLER

Ein- Ausgangsgrößen Aktuator Motorregler

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_UKL30_WERT | real | LMV Klemmenspannung Kl30 |
| STAT_UKL30_EINH | string | physikalische Einheit der Klemmenspannung |
| STAT_USM_WERT | real | Spannungsvorgabe Stellmotor |
| STAT_USM_EINH | string | Aktuator_Spannung_Einheit |
| STAT_PWM_WERT | real | PWM Vorgabe Stellmotor (ohne Totzeitkorrektur) |
| STAT_PWM_EINH | string | Einheit der PWM Vorgabe |
| STAT_ISM_WERT | real | LMV Stellmotorstrom iSM |
| STAT_ISM_EINH | string | physikalische Einheit des Stellmotorstroms |
| STAT_IKL30_WERT | real | LMV Kl30 Eingangsstrom |
| STAT_IKL30_EINH | string | physikalische Einheit des Eingangsstroms Kl30 |
| STAT_TICSM_WERT | int | AMS-RPS-Winkel |
| STAT_TICSM_EINH | string | Einheit des AMS-RPS-Winkels |
| STAT_PHISM_WERT | real | Sperrenwinkel an der Kugelrampe |
| STAT_PHISM_EINH | string | Einheit des Sperrenwinkels |
| STAT_FSM_WERT | real | AMS-RPS-Frequenz |
| STAT_FSM_EINH | string | Einheit der AMS-RPS-Frequenz |
| STAT_NSM_WERT | real | Stellmotordrehzahl (Drehzahl an der Kugelrampe) |
| STAT_NSM_EINH | string | Einheit der Stellmotordrehzahl |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-atic"></a>
### STATUS_ATIC

Fehlerspeicherregister und Initialisierungsregister des ATIC106

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SM_ERROR_WERT | unsigned int | Antwort des ATIC106 auf das Kommandowort B1 |
| STAT_SM_ERROR_TEXT | string | Antwort des ATIC106 auf das Kommandowort B1 |
| STAT_SM_ERROR_EINH | string | Einheit der Antwort des ATIC106 |
| STAT_STATUS_ATIC_WERT | unsigned int | Antwort des ATIC106 auf das Kommandowort B2 |
| STAT_STATUS_ATIC_TEXT | string | Antwort des ATIC106 auf das Kommandowort B2 |
| STAT_STATUS_ATIC_EINH | string | Einheit der Antwort des ATIC106 |
| STAT_ATIC_D1_REGISTER_WERT | unsigned int | Zuletzt gelesener Inhalt des D1 Registers des ATIC106 nach Kommandowort D1 |
| STAT_ATIC_D1_REGISTER_TEXT | string | Zuletzt gelesener Inhalt des D1 Registers des ATIC106 nach Kommandowort D1 |
| STAT_ATIC_D1_REGISTER_EINH | string | Einheit des zuletzt gelesenen Inhalts des D1 Registers |
| STAT_ATIC_D2_REGISTER_WERT | unsigned int | Zuletzt gelesener Inhalt des D2 Registers des ATIC106 nach Kommandowort D2 |
| STAT_ATIC_D2_REGISTER_TEXT | string | Zuletzt gelesener Inhalt des D2 Registers |
| STAT_ATIC_D2_REGISTER_EINH | string | Einheit des zuletzt gelesener Inhalts des D2 Registers |
| STAT_ATIC_E_REGISTER_WERT | unsigned int | Zuletzt gelesener Inhalt des E Registers des ATIC106 nach Kommandowort E |
| STAT_ATIC_E_REGISTER_TEXT | string | Zuletzt gelesener Inhalt des E Registers des ATIC106 nach Kommandowort E |
| STAT_ATIC_E_REGISTER_EINH | string | Einheit des zuuletzt gelesener Inhalts des E Registers |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-autocodierung"></a>
### STATUS_AUTOCODIERUNG

Codierstatus / daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CODIERUNG_TEXT | string | Status Codierung Tabelle TAB_LMV_CODIERSTATUS |
| STAT_CODIERUNG_WERT | int | Status Codierung |
| STAT_CODIERUNG_EINH | string | Einheit des Status Codierung |
| STAT_ERST_CODIERUNG_TEXT | string | Status Erst Codierung Tabelle TAB_LMV_EEPROM_CODIERUNG |
| STAT_ERST_CODIERUNG_WERT | int | Status Erst Codierung |
| STAT_ERST_CODIERUNG_EINH | string | Einheit des Status Erst Codierung |
| STAT_TYP_VEHICLE_TEXT | string | Fahrzeugtyp - Baureihe Tabelle TAB_LMV_BAUREIHE |
| STAT_TYP_VEHICLE_WERT | int | Fahrzeugtyp - Baureihe |
| STAT_TYP_VEHICLE_EINH | string | Einheit der Fahrzeugtyp - Baureihe |
| STAT_AC_DIFF_RATIO_WERT | real | Variable AC_DiffRatio |
| STAT_AC_DIFF_RATIO_EINH | string | Einheit der Variable AC_DiffRatio |
| STAT_QUAN_CYL_WERT | int | Variable QUAN_CYL |
| STAT_QUAN_CYL_EINH | string | Einheit der Variable QUAN_CYL |
| STAT_QUAN_GR_WERT | int | Variable QUAN_GR |
| STAT_QUAN_GR_EINH | string | Einheit der Variable QUAN_GR |
| STAT_TYP_GRB_WERT | int | Variable TYP_GRB |
| STAT_TYP_GRB_EINH | string | Einheit der Variable TYP_GRB |
| STAT_TYP_ENG_WERT | int | Variable TYP_ENG |
| STAT_TYP_ENG_EINH | string | Einheit der Variable TYP_ENG |
| STAT_CLAS_PWR_WERT | int | Variable CLAS_PWR |
| STAT_CLAS_PWR_EINH | string | Einheit der Variable CLAS_PWR |
| STAT_TYP_CAPA_WERT | int | Variable TYP_CAPA |
| STAT_TYP_CAPA_EINH | string | Einheit der Variable TYP_CAPA |
| STAT_DATAINDEX | int | Variable DATAINDEX |
| STAT_DATAINDEX_EINH | string | Einheit der Variable DATAINDEX |
| STAT_TYP_VEHICLE_WERT_BUS | int | Variable VEHICLE_WERT_BUS |
| STAT_TYP_VEHICLE_STATUS | string | Variable STAT_TYP_VEHICLE_STATUS |
| STAT_TYP_VEHICLE_BUS_EINH | string | Einheit der Variable VEHICLE_WERT_BUS |
| STAT_QUAN_CYL_WERT_BUS | int | Variable QUAN_CYL_WERT_BUS |
| STAT_QUAN_CYL_STATUS | string | Variable STAT_QUAN_CYL_STATUS |
| STAT_QUAN_CYL_BUS_EINH | string | Einheit der Variable VEHICLE_WERT_BUS |
| STAT_QUAN_GR_WERT_BUS | int | Variable QUAN_GR_WERT_BUS |
| STAT_QUAN_GR_STATUS | string | Variable STAT_QUAN_GR_WERT_BUS |
| STAT_QUAN_GR_BUS_EINH | string | Einheit der Variable QUAN_GR_WERT_BUS |
| STAT_TYP_GRB_WERT_BUS | int | Variable TYP_GRB_WERT_BUS |
| STAT_TYP_GRB_STATUS | string | Variable STAT_TYP_GRB_STATUS |
| STAT_TYP_GRB_BUS_EINH | string | Einheit der Variable TYP_GRB_BUS_EINH |
| STAT_TYP_ENG_WERT_BUS | int | Variable TYP_ENG_WERT_BUS |
| STAT_TYP_ENG_STATUS | string | Variable STAT_TYP_ENG_STATUS |
| STAT_TYP_ENG_BUS_EINH | string | Einheit der Variable TYP_ENG_WERT_BUS |
| STAT_CLAS_PWR_WERT_BUS | int | Variable CLAS_PWR_WERT_BUS |
| STAT_CLAS_PWR_STATUS | string | Variable STAT_CLAS_PWR_STATUS |
| STAT_CLAS_PWR_BUS_EINH | string | Einheit der Variable CLAS_PWR_WERT_BUS |
| STAT_TYP_CAPA_WERT_BUS | int | Variable TYP_CAPA_WERT_BUS |
| STAT_TYP_CAPA_STATUS | string | Variable TYP_CAPA_STATUS |
| STAT_TYP_CAPA_BUS_EINH | string | Einheit der Variable TYP_CAPA_WERT_BUS |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-calcvn"></a>
### STATUS_CALCVN

Auslesen von Cal-ID und CVN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| STAT_CALID_TEXT | string | Cal-ID text |
| STAT_CVN_WERT | string | CVN Einheit wert |
| STAT_CVN_EINH | string | Einheit des CVN |
| STAT_CVN_INFO | string | Info CVN |
| STAT_CALID_EINH | string | Einheit Cal-ID |
| STAT_CALID_INFO | string | Info Cal-ID |

<a id="job-status-fahrzeugzustand"></a>
### STATUS_FAHRZEUGZUSTAND

Eingangsdaten aus dem Fahrzeugzustandsmanagement

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VSM_ST_STATE_WERT | int | Operationsstatus aus dem Statusmonitor Client (0 - 15) |
| STAT_VSM_ST_STATE_TEXT | string | Operationsstatus aus dem Statusmonitor Client Tabelle TAB_FZG_OP_STATE |
| STAT_VSM_ST_STATE_EINH | string | Einheit Operationsstatus aus dem Statusmonitor Client |
| STAT_VSM_STM_CEL_WERT | int | Status Kommunikations - Fehlerspeichersperre (0 - 3) |
| STAT_VSM_STM_CEL_TEXT | string | Status Kommunikations - Fehlerspeichersperre Tabelle TAB_FZG_COM_STATE |
| STAT_VSM_STM_CEL_EINH | string | Einheit Status Kommunikations - Fehlerspeichersperre |
| STAT_VSM_STM_EN_WERT | int | Energiestatus aus dem Statusmonitor Client (0, 1, 2, 3, 15) |
| STAT_VSM_STM_EN_TEXT | string | Einheit Energiestatus aus dem Statusmonitor Client Tabelle TAB_FZG_ENERGY_STATE |
| STAT_VSM_STM_EN_EINH | string | Einheit Energiestatus aus dem Statusmonitor Client |
| STAT_VSM_ST_MODE_WERT | int | Klemmenstatus (0 - 15) |
| STAT_VSM_ST_MODE_TEXT | string | Klemmenstatus Tabelle TAB_FZG_KL_STATE |
| STAT_VSM_ST_MODE_EINH | string | Einheit Klemmenstatus |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-getriebeklasse"></a>
### STATUS_GETRIEBEKLASSE

Getriebeklasse, Offset- und Steigungsklassierung Verteilergetriebe Dieser Job kann erst ab 09/2011 bzw. ab einer Software-Version ab 000.020.000 verwendet werden.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CLASS_INFO_GEARBOX_TEXT | string | Klassierinformation Getriebeklasse Verteilergetriebe table TAB_GETRIEBEKLASSE_GEARBOX |
| STAT_CLASS_INFO_GEARBOX_WERT | int | Getriebeklasse Verteilergetriebe |
| STAT_CLASS_INFO_GEARBOX_EINH | string | Einheit der Getriebeklasse Verteilergetriebe |
| STAT_CLASS_INFO_OFFSET_TEXT | string | Klassierinformation Offset Klasse Verteilergetriebe table TAB_GETRIEBEKLASSE_OFFSET |
| STAT_CLASS_INFO_OFFSET_WERT | int | Offset Klasse Verteilergetriebe |
| STAT_CLASS_INFO_OFFSET_EINH | string | Einheit der Offset Klasse Verteilergetriebe |
| STAT_CLASS_INFO_GAIN_TEXT | string | Klassierinformation Steigungs Klasse Verteilergetriebe table TAB_GETRIEBEKLASSE_GAIN |
| STAT_CLASS_INFO_GAIN_WERT | int | Steigungs Klasse Verteilergetriebe |
| STAT_CLASS_INFO_GAIN_EINH | string | Einheit der Steigungs Klasse Verteilergetriebe |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-integratoren"></a>
### STATUS_INTEGRATOREN

HO Getriebe und Lamellen Schädigungs Integratoren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HO_GETRIEBE_1_WERT | real | Getriebe Verschleißintegrator 1 |
| STAT_HO_GETRIEBE_1_EINH | string | Einheit des Getriebe Verschleißintegrator 1 |
| STAT_HO_GETRIEBE_2_WERT | real | Getriebe Verschleißintegrator 2 |
| STAT_HO_GETRIEBE_2_EINH | string | Einheit des Getriebe Verschleißintegrator 2 |
| STAT_HO_GETRIEBE_3_WERT | real | Öl-Verschleißintegrator |
| STAT_HO_GETRIEBE_3_EINH | string | Einheit des Öl-Verschleißintegrator |
| STAT_HO_LAMELLE_1_WERT | real | Lamellen Verschleißintegrator 1 |
| STAT_HO_LAMELLE_1_EINH | string | Einheit des Lamellenverschleißintegrator 1 |
| STAT_HO_LAMELLE_2_WERT | real | Lamellen Verschleißintegrator 2 |
| STAT_HO_LAMELLE_2_EINH | string | Einheit des Lamellenverschleißintegrator 2 |
| STAT_HO_LAMELLE_3_WERT | real | Lamellen Verschleißintegrator 3 |
| STAT_HO_LAMELLE_3_EINH | string | Einheit des Lamellenverschleißintegrator 3 |
| STAT_HO_INTEGRATOR_KM_WERT | unsigned long | Gefahrene Kilometer seit letztem Wechsel des Getriebeöls |
| STAT_HO_INTEGRATOR_KM_EINH | string | Einheit des Intervallkilometerzählers |
| STAT_RUN_IN_COMP_1_WERT | unsigned long | Momentenübergleitungszähler 1 |
| STAT_RUN_IN_COMP_1_EINH | string | Einheit Momentenübergleitungszähler 1 |
| STAT_RUN_IN_COMP_2_WERT | unsigned long | Momentenübergleitungszähler 2 |
| STAT_RUN_IN_COMP_2_EINH | string | Einheit Momentenübergleitungszähler 2 |
| STAT_RUN_IN_COMP_3_WERT | unsigned long | Momentenübergleitungszähler 3 |
| STAT_RUN_IN_COMP_3_EINH | string | Einheit Momentenübergleitungszähler 3 |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-istmoment"></a>
### STATUS_ISTMOMENT

Momenten Istwert und Qualifier vom LMV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_AVL_REPAT_XTRQ_FTAX_BAX_WERT | long | Istwert des Moments zur Vorderachse - LMV |
| STAT_AVL_REPAT_XTRQ_FTAX_BAX_EINH | string | Einheit des Istmoment |
| STAT_QU_AVL_REPAT_XTRQ_FTAX_BAX_WERT | int | Signalqualifier zum Istmoment |
| STAT_QU_AVL_REPAT_XTRQ_FTAX_BAX_TEXT | string | Signalqualifier zum Istmoment Tabelle TAB_LMV_ISTMOMENTQUALIFIER |
| STAT_QU_AVL_REPAT_XTRQ_FTAX_BAX_EINH | string | Einheit des Signalqualifier |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-kalibrierung"></a>
### STATUS_KALIBRIERUNG

Kalibrierstatus / daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_KALIB_INFO_TEXT | string | Status Kalibrierung Tabelle TAB_KALIBRIERUNG_INFO |
| STAT_PHISPERREKAL_WERT | real | aktueller Kalibrierwinkel |
| STAT_PHISPERREKAL_EINH | string | aktueller Kalibrierwinkel Einheit |
| STAT_DELTAPHI_WERT | real | Differenz zum Erst-Kalibrierwinkel |
| STAT_DELTAPHI_EINH | string | deltaPhi Einheit |
| STAT_COUNT_KAL_WERT | unsigned long | Anzahl der durchgeführten Nachlaufkalibrierungen |
| STAT_COUNT_KAL_EINH | string | Einheit Anzahl der durchgeführten Nachlaufkalibrierungen |
| STAT_COUNT_FORCE_WERT | unsigned long | Anzahl der Zwangskalibrierungen |
| STAT_COUNT_FORCE_EINH | string | Einheit Anzahl der Zwangskalibrierungen |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-klassierung"></a>
### STATUS_KLASSIERUNG

Offset / Steigungsklassierung Verteilergetriebe

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CLASS_INFO_OFFSET_TEXT | string | Klassierinformation Offset Klasse Verteilergetriebe table TAB_KLASSIERUNG_OFFSET |
| STAT_CLASS_INFO_OFFSET_WERT | int | Offset Klasse Verteilergetriebe |
| STAT_CLASS_INFO_OFFSET_EINH | string | Einheit der Offset Klasse Verteilergetriebe |
| STAT_CLASS_INFO_GAIN_TEXT | string | Klassierinformation Steigung Klasse Verteilergetriebe table TAB_KLASSIERUNG_GAIN |
| STAT_CLASS_INFO_GAIN_WERT | int | Steigungs Klasse Verteilergetriebe |
| STAT_CLASS_INFO_GAIN_EINH | string | Einheit der Steigung Klasse Verteilergetriebe |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-klemmenspannung"></a>
### STATUS_KLEMMENSPANNUNG

Spannungen an den LMV Eingangsklemmen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_UKL30_WERT | real | LMV Klemmenspannung Kl30 |
| STAT_UKL30_EINH | string | physikalische Einheit der Klemmenspannung |
| STAT_UKL30B_WERT | real | LMV Klemmenspannung Kl30b |
| STAT_UKL30B_EINH | string | physikalische Einheit der Klemmenspannung |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-kupplungsstatus"></a>
### STATUS_KUPPLUNGSSTATUS

Service - Qualifier des LMV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_QU_SER_BASIS_WERT | int | Service Basis - Qualifier des LMV |
| STAT_QU_SER_BASIS_TEXT | string | Service Basis - Qualifier des LMV Tabelle TAB_4004_1 |
| STAT_QU_SER_BASIS_EINH | string | Einheit des Service Basis - Qualifier |
| STAT_QU_SER_NOTLAUF_WERT | int | Notlaufregler |
| STAT_QU_SER_NOTLAUF_TEXT | string | Notlaufregler Tabelle TAB_4004_2 |
| STAT_QU_SER_NOTLAUF_EINH | string | Einheit Notlaufregler |
| STAT_QU_SER_POSITION_WERT | int | Position LMV Stellglied |
| STAT_QU_SER_POSITION_TEXT | string | Position LMV Stellglied |
| STAT_QU_SER_POSITION_EINH | string | Einheit Position LMV Stellglied |
| STAT_QU_SER_SCHUTZ_WERT | int | LMV Schutzfunktion |
| STAT_QU_SER_SCHUTZ_TEXT | string | LMV Schutzfunktion |
| STAT_QU_SER_SCHUTZ_EINH | string | Einheit LMV Schutzfunktion |
| STAT_QU_SER_VV_KUPPLUNG_WERT | int | Verfügbarkeit Kupplung |
| STAT_QU_SER_VV_KUPPLUNG_TEXT | string | Verfügbarkeit Kupplung Tabelle TAB_LMV_VV_KUPPLUNG |
| STAT_QU_SER_VV_KUPPLUNG_EINH | string | Einheit Verfügbarkeit Kupplung |
| STAT_QU_SER_VV_STELLGLIED_WERT | int | Verfügbarkeit Stellglied |
| STAT_QU_SER_VV_STELLGLIED_TEXT | string | Verfügbarkeit Stellglied |
| STAT_QU_SER_VV_STELLGLIED_EINH | string | Einheit Verfügbarkeit Stellglied |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-lt-integratoren"></a>
### STATUS_LT_INTEGRATOREN

Lifetime Getriebe und Lamellen Schädigungs Integratoren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LT_GETRIEBE_1_WERT | real | Getriebe Verschleißintegrator 1 |
| STAT_LT_GETRIEBE_1_EINH | string | Einheit des Getriebe Verschleißintegrator 1 |
| STAT_LT_GETRIEBE_2_WERT | real | Getriebe Verschleißintegrator 2 |
| STAT_LT_GETRIEBE_2_EINH | string | Einheit des Getriebe Verschleißintegrator 2 |
| STAT_LT_LAMELLE_1_WERT | real | Lamellen Verschleißintegrator 1 |
| STAT_LT_LAMELLE_1_EINH | string | Einheit des Lamellenverschleißintegrator 1 |
| STAT_LT_LAMELLE_2_WERT | real | Lamellen Verschleißintegrator 2 |
| STAT_LT_LAMELLE_2_EINH | string | Einheit des Lamellenverschleißintegrator 2 |
| STAT_LT_LAMELLE_3_WERT | real | Lamellen Verschleißintegrator 3 |
| STAT_LT_LAMELLE_3_EINH | string | Einheit des Lamellenverschleißintegrator 3 |
| STAT_LT_OEL_WERT | real | Öl-Verschleißintegrator |
| STAT_LT_OEL_EINH | string | Einheit des Öl-Verschleißintegrators |
| STAT_LT_INTEGRATOR_KM_WERT | unsigned long | Mile Km vom Bus |
| STAT_LT_INTEGRATOR_KM_EINH | string | Einheit des Mile-km Wertes |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-pruefstand"></a>
### STATUS_PRUEFSTAND

Pruefstandsmodus Status / Daten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PRUEFSTANDSMODE_WERT | int | Aktueller Pruefstandsmodus 0	: Pruefstandsmodus nicht aktiviert 1	: Pruefstandsmodus aktiviert |
| STAT_PRUEFSTANDSMODE_TEXT | string | Tabelle  TAB_PRUEFSTAND_INFO |
| STAT_PRUEFSTANDSMODE_EINH | string | Einheit der Variable PRUEFSTANDSMODE |
| STAT_DATAINDEX | int | Autocodierungsindex laut Vorgabe im Job STEUERN_PRUEFSTAND |
| STAT_DATAINDEX_TEXT | string | Tabelle TAB_PRUEFSTAND_AUTOCODIERUNG |
| STAT_DATAINDEX_EINH | string | Einheit der Variable DATAINDEX |
| STAT_VKM_PRUEFSTAND_WERT | int | VKM Status laut Vorgabe im Job STEUERN_PRUEFSTAND |
| STAT_VKM_PRUEFSTAND_TEXT | string | Tabelle TAB_PRUEFSTAND_VKM |
| STAT_VKM_PRUEFSTAND_EINH | string | Einheit der Variable VKM_PRUEFSTAND |
| STAT_SOLLMOMENT_PRUEFSTAND_WERT | long | Sollmoment laut Vorgabe im Job STEUERN_PRUEFSTAND |
| STAT_SOLLMOMENT_PRUEFSTAND_EINH | string | Einheit des Sollmoment |
| STAT_AVL_REPAT_XTRQ_FTAX_BAX_WERT | int | Istwert des Moments zur Vorderachse - VGSG |
| STAT_AVL_REPAT_XTRQ_FTAX_BAX_EINH | string | Einheit des Istmoment |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-sollmoment"></a>
### STATUS_SOLLMOMENT

Momenten Sollwert und Qualifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TAR_REPAT_XTRQ_FTAX_BAX_ACT_WERT | long | Sollmoment - Vorgabe zur Vorderache |
| STAT_TAR_REPAT_XTRQ_FTAX_BAX_ACT_EINH | string | Einheit des Sollmoment |
| STAT_QU_TAR_REPAT_XTRQ_FTAX_BAX_ACT_WERT | int | Sollwertqualifier zur Sollmomentvorgabe |
| STAT_QU_TAR_REPAT_XTRQ_FTAX_BAX_ACT_TEXT | string | Sollwertqualifier zur Sollmomentvorgabe Tabelle TAB_LMV_SOLLWERTQUALIFIER |
| STAT_QU_TAR_REPAT_XTRQ_FTAX_BAX_ACT_EINH | string | Einheit des Sollmomentqualifiers |
| STAT_ST_ECU_TAR_REPAT_XTRQ_FTAX_BAX_WERT | int | ECU Qualifier vom Fahrdynamik SG |
| STAT_ST_ECU_TAR_REPAT_XTRQ_FTAX_BAX_TEXT | string | ECU Qualifier vom Fahrdynamik SG Tabelle TAB_LMV_ECU_QUALIFIER |
| STAT_ST_ECU_TAR_REPAT_XTRQ_FTAX_BAX_EINH | string | Einheit des ECU Qualifiers |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-sysinfo-lesen"></a>
### STATUS_SYSINFO_LESEN

Liest die Information der in Getriebe befindlichen Softwarekomponenten aus Achtung: STAT_ATIC_ID_* nur direkt nach einem Power-up gültig!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_HWE_SGBMID | string | HWE Information |
| STAT_HWE_INFO | string | HWE Information |
| STAT_HWE_REAL_WERT | unsigned char | HWE Information |
| STAT_HWE_REAL_TEXT | string | HWE Information Tabelle TAB_HWE_ID |
| STAT_HWE_REAL_EINH | string | Einheit HWE Information |
| STAT_BLTD_SGBMID | string | BLTD Information |
| STAT_BLTD_INFO | string | BLTD Information |
| STAT_SWE1_SGBMID | string | SWE1/BSW Information |
| STAT_SWE1_INFO | string | SWE1/BSW Information |
| STAT_SWE2_SGBMID | string | SWE2 Information |
| STAT_SWE2_INFO | string | SWE2 Information |
| STAT_SWE3_SGBMID | string | SWE3 Information |
| STAT_SWE3_INFO | string | SWE3 Information |
| STAT_SWE4_SGBMID | string | SWE4 Information |
| STAT_SWE4_INFO | string | SWE4 Information |
| STAT_ATIC_ID_WERT | unsigned int | ATIC ID Information |
| STAT_ATIC_ID_TEXT | string | ATIC ID Information Tabelle TAB_ATIC_ID |
| STAT_ATIC_ID_EINH | string | Einheit ATIC ID Information |
| STAT_MCU_ID_WERT | unsigned char | MCU ID Information |
| STAT_MCU_ID_TEXT | string | MCU ID Information ('Family Identifier') Tabelle TAB_MCU_FAMILY |
| STAT_MCU_ID_EINH | string | Einheit MCU ID Information |
| STAT_MCU_MASK_WERT | unsigned char | MCU MASK Information |
| STAT_MCU_MASK_TEXT | string | MCU MASK Information ('Mask Set Number') Tabelle TAB_MCU_MASK |
| STAT_MCU_MASK_EINH | string | Einheit MCU MASK Information |
| STAT_MCU_VERSION_ID_WERT | unsigned int | MCU Version ID Information |
| STAT_MCU_VERSION_ID_EINH | string | Einheit MCU Version ID Information |
| STAT_BSW_LIB_INFO | string | BSW Library Information |
| STAT_BSW_DATA_INFO | string | BSW Data Information |
| STAT_NLR_LIB_INFO | string | NLR Library Information |
| STAT_NLR_DATA_INFO | string | NLR Data Information |
| STAT_FSW_LIB_INFO | string | FSW Library Information |
| STAT_FSW_DATA_INFO | string | FSW Data Information |
| STAT_ANZAHL_EINHEITEN | int | Anzahl der xWEn |
| STAT_PROZESSKLASSE_WERT_0 | int | table Prozessklassen WERT dezimale Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_TEXT_0 | string | table Prozessklassen BEZEICHNUNG Text-Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_KURZTEXT_0 | string | table Prozessklassen PROZESSKLASSE Text-Angabe des Prozessklassenkurztextes |
| STAT_SGBM_IDENTIFIER_0 | string | Angabe SGBM-ID der Prozessklasse |
| STAT_VERSION_0 | string | Angabe der Version der Prozessklasse |
| STAT_SGBM_ID_0 | string | Angabe von Prozessklasse, SGBM-Identifier, Version |
| STAT_PROZESSKLASSE_WERT_1 | int | table Prozessklassen WERT dezimale Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_TEXT_1 | string | table Prozessklassen BEZEICHNUNG Text-Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_KURZTEXT_1 | string | table Prozessklassen PROZESSKLASSE Text-Angabe des Prozessklassenkurztextes |
| STAT_SGBM_IDENTIFIER_1 | string | Angabe SGBM-ID der Prozessklasse |
| STAT_VERSION_1 | string | Angabe der Version der Prozessklasse |
| STAT_SGBM_ID_1 | string | Angabe von Prozessklasse, SGBM-Identifier, Version |
| STAT_PROZESSKLASSE_WERT_2 | int | table Prozessklassen WERT dezimale Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_TEXT_2 | string | table Prozessklassen BEZEICHNUNG Text-Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_KURZTEXT_2 | string | table Prozessklassen PROZESSKLASSE Text-Angabe des Prozessklassenkurztextes |
| STAT_SGBM_IDENTIFIER_2 | string | Angabe SGBM-ID der Prozessklasse |
| STAT_VERSION_2 | string | Angabe der Version der Prozessklasse |
| STAT_SGBM_ID_2 | string | Angabe von Prozessklasse, SGBM-Identifier, Version |
| STAT_PROZESSKLASSE_WERT_3 | int | table Prozessklassen WERT dezimale Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_TEXT_3 | string | table Prozessklassen BEZEICHNUNG Text-Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_KURZTEXT_3 | string | table Prozessklassen PROZESSKLASSE Text-Angabe des Prozessklassenkurztextes |
| STAT_SGBM_IDENTIFIER_3 | string | Angabe SGBM-ID der Prozessklasse |
| STAT_VERSION_3 | string | Angabe der Version der Prozessklasse |
| STAT_SGBM_ID_3 | string | Angabe von Prozessklasse, SGBM-Identifier, Version |
| STAT_PROZESSKLASSE_WERT_4 | int | table Prozessklassen WERT dezimale Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_TEXT_4 | string | table Prozessklassen BEZEICHNUNG Text-Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_KURZTEXT_4 | string | table Prozessklassen PROZESSKLASSE Text-Angabe des Prozessklassenkurztextes |
| STAT_SGBM_IDENTIFIER_4 | string | Angabe SGBM-ID der Prozessklasse |
| STAT_VERSION_4 | string | Angabe der Version der Prozessklasse |
| STAT_SGBM_ID_4 | string | Angabe von Prozessklasse, SGBM-Identifier, Version |
| STAT_PROZESSKLASSE_WERT_5 | int | table Prozessklassen WERT dezimale Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_TEXT_5 | string | table Prozessklassen BEZEICHNUNG Text-Angabe der Prozessklasse |
| STAT_PROZESSKLASSE_KURZTEXT_5 | string | table Prozessklassen PROZESSKLASSE Text-Angabe des Prozessklassenkurztextes |
| STAT_SGBM_IDENTIFIER_5 | string | Angabe SGBM-ID der Prozessklasse |
| STAT_VERSION_5 | string | Angabe der Version der Prozessklasse |
| STAT_SGBM_ID_5 | string | Angabe von Prozessklasse, SGBM-Identifier, Version |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-temperaturhistogramm"></a>
### STATUS_TEMPERATURHISTOGRAMM

Temperaturverteilung LMV SG / Betriebszeit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TMP_HISTO_12_WERT | unsigned int | Intervallzähler Temperaturbereich 12, Basis 5min |
| STAT_TMP_HISTO_12_EINH | string | Einheit Intervallzähler Temperaturbereich 12, Basis 5min |
| STAT_TMP_HISTO_11_WERT | unsigned int | Intervallzähler Temperaturbereich 11, Basis 5min |
| STAT_TMP_HISTO_11_EINH | string | Einheit Intervallzähler Temperaturbereich 11, Basis 5min |
| STAT_TMP_HISTO_10_WERT | unsigned int | Intervallzähler Temperaturbereich 10, Basis 5min |
| STAT_TMP_HISTO_10_EINH | string | Einheit Intervallzähler Temperaturbereich 10, Basis 5min |
| STAT_TMP_HISTO_09_WERT | unsigned int | Intervallzähler Temperaturbereich 9, Basis 5min |
| STAT_TMP_HISTO_09_EINH | string | Einheit Intervallzähler Temperaturbereich 9, Basis 5min |
| STAT_TMP_HISTO_08_WERT | unsigned int | Intervallzähler Temperaturbereich 8, Basis 5min |
| STAT_TMP_HISTO_08_EINH | string | Einheit Intervallzähler Temperaturbereich 8, Basis 5min |
| STAT_TMP_HISTO_07_WERT | unsigned int | Intervallzähler Temperaturbereich 7, Basis 5min |
| STAT_TMP_HISTO_07_EINH | string | Einheit Intervallzähler Temperaturbereich 7, Basis 5min |
| STAT_TMP_HISTO_06_WERT | unsigned int | Intervallzähler Temperaturbereich 6, Basis 5min |
| STAT_TMP_HISTO_06_EINH | string | Einheit Intervallzähler Temperaturbereich 6, Basis 5min |
| STAT_TMP_HISTO_05_WERT | unsigned int | Intervallzähler Temperaturbereich 5, Basis 5min |
| STAT_TMP_HISTO_05_EINH | string | Einheit Intervallzähler Temperaturbereich 5, Basis 5min |
| STAT_TMP_HISTO_04_WERT | unsigned int | Intervallzähler Temperaturbereich 4, Basis 5min |
| STAT_TMP_HISTO_04_EINH | string | Einheit Intervallzähler Temperaturbereich 4, Basis 5min |
| STAT_TMP_HISTO_03_WERT | unsigned int | Intervallzähler Temperaturbereich 3, Basis 5min |
| STAT_TMP_HISTO_03_EINH | string | Einheit Intervallzähler Temperaturbereich 3, Basis 5min |
| STAT_TMP_HISTO_02_WERT | unsigned int | Intervallzähler Temperaturbereich 2, Basis 5min |
| STAT_TMP_HISTO_02_EINH | string | Einheit Intervallzähler Temperaturbereich 2, Basis 5min |
| STAT_TMP_HISTO_01_WERT | unsigned int | Intervallzähler Temperaturbereich 1, Basis 5min |
| STAT_TMP_HISTO_01_EINH | string | Einheit Intervallzähler Temperaturbereich 1, Basis 5min |
| STAT_OPERATION_TIME_WERT | real | Betriebsdauer VGSG |
| STAT_OPERATION_TIME_EINH | string | Einheit der Betriebsdauer |
| STAT_TIME_REL_WERT | real | Relativzeit aus Botschaft in Stunden |
| STAT_TIME_REL_EINH | string | Einheit der Relativzeit |
| STAT_MILE_KM_WERT | unsigned long | Wegstrecke - Kilometerstand aus Busbotschaft |
| STAT_MILE_KM_EINH | string | Einheit der Wegstrecke |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-verteilergetriebe"></a>
### STATUS_VERTEILERGETRIEBE

Verteilergetriebedaten für FASTA Auswertung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VTG_INFO_TEXT | string | Status Verteilergetriebe Tabelle TAB_KALIBRIERUNG_INFO |
| STAT_PHISPERREKAL_WERT | real | aktueller Kalibrierwinkel |
| STAT_PHISPERREKAL_EINH | string | aktueller Kalibrierwinkel Einheit |
| STAT_DELTAPHI_WERT | real | Differenz zum Erst-Kalibrierwinkel |
| STAT_DELTAPHI_EINH | string | deltaPhi Einheit |
| STAT_COUNT_KAL_WERT | unsigned long | Anzahl der durchgeführten Nachlaufkalibrierungen |
| STAT_COUNT_KAL_EINH | string | Einheit Anzahl der durchgeführten Nachlaufkalibrierungen |
| STAT_COUNT_FORCE_WERT | unsigned long | Anzahl der Zwangskalibrierungen |
| STAT_COUNT_FORCE_EINH | string | Einheit Anzahl der Zwangskalibrierungen |
| STAT_DELTAPHI_RAW_WERT | real | Ungefilteter Kalibrierwinkel |
| STAT_DELTAPHI_RAW_EINH | string | Ungefilteter Kalibrierwinkel Einheit |
| STAT_CLASS_INFO_GEARBOX_TEXT | string | Klassierinformation Getriebeklasse Verteilergetriebe table TAB_GETRIEBEKLASSE_GEARBOX |
| STAT_CLASS_INFO_GEARBOX_WERT | int | Getriebeklasse Verteilergetriebe |
| STAT_CLASS_INFO_GEARBOX_EINH | string | Einheit der Getriebeklasse Verteilergetriebe |
| STAT_WORKOIL4DIAG_WERT | real | Ölverschleiß |
| STAT_WORKOIL4DIAG_EINH | string | Einheit Ölverschleiß |
| STAT_HO_GETRIEBE_1_WERT | real | Getriebe Verschleißintegrator 1 |
| STAT_HO_GETRIEBE_1_EINH | string | Einheit des Getriebe Verschleißintegrator 1 |
| STAT_HO_GETRIEBE_2_WERT | real | Getriebe Verschleißintegrator 2 |
| STAT_HO_GETRIEBE_2_EINH | string | Einheit des Getriebe Verschleißintegrator 2 |
| STAT_HO_GETRIEBE_3_WERT | real | Öl-Verschleißintegrator |
| STAT_HO_GETRIEBE_3_EINH | string | Einheit des Öl-Verschleißintegrator |
| STAT_HO_LAMELLE_1_WERT | real | Lamellen Verschleißintegrator 1 |
| STAT_HO_LAMELLE_1_EINH | string | Einheit des Lamellenverschleißintegrator 1 |
| STAT_HO_LAMELLE_2_WERT | real | Lamellen Verschleißintegrator 2 |
| STAT_HO_LAMELLE_2_EINH | string | Einheit des Lamellenverschleißintegrator 2 |
| STAT_HO_LAMELLE_3_WERT | real | Lamellen Verschleißintegrator 3 |
| STAT_HO_LAMELLE_3_EINH | string | Einheit des Lamellenverschleißintegrator 3 |
| STAT_HO_INTEGRATOR_KM_WERT | unsigned long | Gefahrene Kilometer seit letztem Wechsel des Getriebeöls |
| STAT_HO_INTEGRATOR_KM_EINH | string | Einheit des Intervallkilometerzählers |
| STAT_RUN_IN_COMP_1_WERT | unsigned long | Momentenübergleitungszähler 1 |
| STAT_RUN_IN_COMP_1_EINH | string | Einheit Momentenübergleitungszähler 1 |
| STAT_RUN_IN_COMP_2_WERT | unsigned long | Momentenübergleitungszähler 2 |
| STAT_RUN_IN_COMP_2_EINH | string | Einheit Momentenübergleitungszähler 2 |
| STAT_RUN_IN_COMP_3_WERT | unsigned long | Momentenübergleitungszähler 3 |
| STAT_RUN_IN_COMP_3_EINH | string | Einheit Momentenübergleitungszähler 3 |
| STAT_CNT_START_TRQ_INCREASE_WERT | unsigned long | Anzahl der Anfahrten mit Momentenerhöhung |
| STAT_CNT_START_TRQ_INCREASE_EINH | string | Einheit Anzahl der Anfahrten mit Momentenerhöhung |
| STAT_CNT_START_TRQ_DECREASE_WERT | unsigned long | Anzahl der Anfahrten mit Momentenabsenkung |
| STAT_CNT_START_TRQ_DECREASE_EINH | string | Einheit Anzahl der Anfahrten mit Momentenabsenkungöhung |
| STAT_CNT_ANSU_WERT | unsigned long | Anzahl der Anschlagsuchen |
| STAT_CNT_ANSU_EINH | string | Einheit Anzahl der Anschlagsuchen |
| STAT_ITA_TRQ_CCW_WERT | real | Momentkonstante ITA CCW |
| STAT_ITA_TRQ_CCW_EINH | string | Einheit Momentkonstante ITA CCW |
| STAT_ITA_TRQ_CW_WERT | real | Momentkonstante ITA CW |
| STAT_ITA_TRQ_CW_EINH | string | Einheit Momentkonstante ITA CW |
| STAT_TMP_HISTO_12_WERT | unsigned int | Intervallzähler Temperaturbereich 12, Basis 5min |
| STAT_TMP_HISTO_12_EINH | string | Einheit Intervallzähler Temperaturbereich 12, Basis 5min |
| STAT_TMP_HISTO_11_WERT | unsigned int | Intervallzähler Temperaturbereich 11, Basis 5min |
| STAT_TMP_HISTO_11_EINH | string | Einheit Intervallzähler Temperaturbereich 11, Basis 5min |
| STAT_TMP_HISTO_10_WERT | unsigned int | Intervallzähler Temperaturbereich 10, Basis 5min |
| STAT_TMP_HISTO_10_EINH | string | Einheit Intervallzähler Temperaturbereich 10, Basis 5min |
| STAT_TMP_HISTO_09_WERT | unsigned int | Intervallzähler Temperaturbereich 9, Basis 5min |
| STAT_TMP_HISTO_09_EINH | string | Einheit Intervallzähler Temperaturbereich 9, Basis 5min |
| STAT_TMP_HISTO_08_WERT | unsigned int | Intervallzähler Temperaturbereich 8, Basis 5min |
| STAT_TMP_HISTO_08_EINH | string | Einheit Intervallzähler Temperaturbereich 8, Basis 5min |
| STAT_TMP_HISTO_07_WERT | unsigned int | Intervallzähler Temperaturbereich 7, Basis 5min |
| STAT_TMP_HISTO_07_EINH | string | Einheit Intervallzähler Temperaturbereich 7, Basis 5min |
| STAT_TMP_HISTO_06_WERT | unsigned int | Intervallzähler Temperaturbereich 6, Basis 5min |
| STAT_TMP_HISTO_06_EINH | string | Einheit Intervallzähler Temperaturbereich 6, Basis 5min |
| STAT_TMP_HISTO_05_WERT | unsigned int | Intervallzähler Temperaturbereich 5, Basis 5min |
| STAT_TMP_HISTO_05_EINH | string | Einheit Intervallzähler Temperaturbereich 5, Basis 5min |
| STAT_TMP_HISTO_04_WERT | unsigned int | Intervallzähler Temperaturbereich 4, Basis 5min |
| STAT_TMP_HISTO_04_EINH | string | Einheit Intervallzähler Temperaturbereich 4, Basis 5min |
| STAT_TMP_HISTO_03_WERT | unsigned int | Intervallzähler Temperaturbereich 3, Basis 5min |
| STAT_TMP_HISTO_03_EINH | string | Einheit Intervallzähler Temperaturbereich 3, Basis 5min |
| STAT_TMP_HISTO_02_WERT | unsigned int | Intervallzähler Temperaturbereich 2, Basis 5min |
| STAT_TMP_HISTO_02_EINH | string | Einheit Intervallzähler Temperaturbereich 2, Basis 5min |
| STAT_TMP_HISTO_01_WERT | unsigned int | Intervallzähler Temperaturbereich 1, Basis 5min |
| STAT_TMP_HISTO_01_EINH | string | Einheit Intervallzähler Temperaturbereich 1, Basis 5min |
| STAT_OPERATION_TIME_WERT | real | Betriebsdauer VGSG |
| STAT_OPERATION_TIME_EINH | string | Einheit der Betriebsdauer |
| STAT_TIME_REL_WERT | real | Relativzeit aus Botschaft in Stunden |
| STAT_TIME_REL_EINH | string | Einheit der Relativzeit |
| STAT_MILE_KM_WERT | unsigned long | Wegstrecke - Kilometerstand aus Busbotschaft |
| STAT_MILE_KM_EINH | string | Einheit der Wegstrecke |
| STAT_EEPROM_INFO_TEXT | string | Status EEPROM |
| STAT_EEPROM_HIGH_WERT | unsigned char | FCCOB-Register High-Byte (Dead Sector Count/Part Count) |
| STAT_EEPROM_HIGH_EINH | string | Einheit der Wegstrecke |
| STAT_EEPROM_LOW_WERT | unsigned char | FCCOB-Register Low-Byte (Ready Sector Count/Part Count) |
| STAT_EEPROM_LOW_EINH | string | Einheit der Wegstrecke |
| STAT_ZEIT_ROLLENERKENNUNG_EINACHSROLLE_WERT | unsigned int | Zähler Zeit Rollenerkennung aktiv - Einachsrolle |
| STAT_ZEIT_ROLLENERKENNUNG_EINACHSROLLE_EINH | string | Einheit der Zeit Rollenerkennung aktiv - Einachsrolle |
| STAT_ZEIT_ROLLENERKENNUNG_BREMSPRUEFSTAND_WERT | unsigned int | Zähler: Zeit Rollenerkennung aktiv - Bremsenprüfstand |
| STAT_ZEIT_ROLLENERKENNUNG_BREMSPRUEFSTAND_EINH | string | Einheit der Zeit Rollenerkennung aktiv - Bremsenprüfstand |
| STAT_ANZAHL_FALSCHE_KLASSIERUNG_WERT | int | Zähler für Diagnose falsche Klassierung |
| STAT_ANZAHL_FALSCHE_KLASSIERUNG_EINH | string | Einheit für Diagnose falsche Klassierung |
| STAT_ANZAHL_NACHLAUFKALIBRIERUNG_FEHLGESCHLAGEN_WERT | int | Zähler: Nachlaufkalibrierung- aufgrund RPS-Sensor Fehler innerhalb 30s (Parameter) nicht erfolgreich |
| STAT_ANZAHL_NACHLAUFKALIBRIERUNG_FEHLGESCHLAGEN_EINH | string | Einheit der Nachlaufkalibrierung- aufgrund RPS-Sensor Fehler innerhalb 30s (Parameter) nicht erfolgreich |
| STAT_ANZAHL_SOLLPOSITION_NICHT_ERREICHT_WERT | unsigned int | Zähler: Im Momentauf- bzw. Abbau Sollposition (+/-0,25°) nicht erreicht |
| STAT_ANZAHL_SOLLPOSITION_NICHT_ERREICHT_EINH | string | Einheit der im Momentauf- bzw. Abbau Sollposition (+/-0,25°) nicht erreicht |
| STAT_ANZAHL_KL15_ZYKLEN_OHNE_VIN_WERT | unsigned int | Zähler: Klemme15 Zyklen ohne empfangener VIN |
| STAT_ANZAHL_KL15_ZYKLEN_OHNE_VIN_EINH | string | Einheit der Klemme15 Zyklen ohne empfangener VIN |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-vtg-sn-lesen"></a>
### STATUS_VTG_SN_LESEN

Liest die VTG-SN aus (wird am Getriebe EOL geschrieben)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_VTG_SN | string | Seriennummer des LMV-SG |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-autocodierung-default"></a>
### STEUERN_AUTOCODIERUNG_DEFAULT

Aktivierung eines uncodierten SG mit Default Werten Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein Achtung: Dieser Job kann nur innerhalb von 20 Sekunden nach Kl15ein aktiviert werden!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-codierdaten-ruecksetzen"></a>
### STEUERN_CODIERDATEN_RUECKSETZEN

Codierdaten im EEPROM loeschen Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-disable-check-crc-alive"></a>
### STEUERN_DISABLE_CHECK_CRC_ALIVE

Schaltet die Botschaftsabsicherung mittels CRC und Alive Counter bis zum nächsten SG Neustart aus Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-funktionspruefung"></a>
### STEUERN_FUNKTIONSPRUEFUNG

Funktionsprüfung der Kupplung mit vorherigem löschen des Kalibrierwinkels Bedingungen: Wenn (vFzg &lt; 3 km/h && VKMaus && KL15ein && gültige Klassierung) oder (vFzg &lt; 3 km/h && VKMein && MKsoll &lt; 10 Nm && gültige Klassierung)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int | Kein Argument : Funktionsprüfung der Kupplung mit vorherigem löschen des Kalibrierwinkels und SG-Reset Argument = 1  : Funktionsprüfung der Kupplung ohne vorherigem löschen des Kalibrierwinkels und ohne SG-Reset |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei NO_VALID_CLASS, wenn die Klassierung fehlt ERROR_SYSTEM_BUSY, wenn die FSW nicht bereit ist, den Job auszuführen ERROR_TIMEOUT_JOB_START, wenn die FSW auf Jobstart nicht reagiert ERROR_REJECT_JOB_START, wenn die FSW mit Fehlermeldung auf Jobstart reagiert ERROR_TIMEOUT_JOB_PENDING, wenn die FSW den Status 'Warten auf Ausführung' nicht verlaesst ERROR_REJECT_JOB_PENDING, wenn die FSW vom Status 'Warten auf Ausführung' nicht in den Status 'Job wird ausgeführt' wechselt ERROR_TIMEOUT_JOB, wenn die FSW den Job nicht beendet ERROR_REJECT_JOB, wenn die FSW den Job mit Fehler beendet ERROR_ARGUMENT, wenn der Parameter ungültig ist (ungleich 1) tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |
| _REQUEST_3 | binary | Hex-Auftrag an SG |
| _RESPONSE_3 | binary | Hex-Antwort von SG |
| _REQUEST_4 | binary | Hex-Auftrag an SG |
| _RESPONSE_4 | binary | Hex-Antwort von SG |
| _REQUEST_5 | binary | Hex-Auftrag an SG |
| _RESPONSE_5 | binary | Hex-Antwort von SG |

<a id="job-steuern-getriebeklasse-ruecksetzen"></a>
### STEUERN_GETRIEBEKLASSE_RUECKSETZEN

Setzt die Klassierinformation im EEPROM auf den Initialwert (unklassiert) zurück Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein Dieser Job kann erst ab 09/2011 bzw. ab einer Software-Version ab 000.020.000 verwendet werden.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

<a id="job-steuern-getriebeklasse-setzen"></a>
### STEUERN_GETRIEBEKLASSE_SETZEN

Setzt die Klassierinformation im EEPROM auf die Werte des Arguments Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein Dieser Job kann erst ab 09/2011 bzw. ab einer Software-Version ab 000.020.000 verwendet werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_CLASSGRB | int | EEClassGrb = Argument_1 (1 - 239, 3013 - 7411) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |
| _REQUEST_3 | binary | Hex-Auftrag an SG |
| _RESPONSE_3 | binary | Hex-Antwort von SG |
| _REQUEST_4 | binary | Hex-Auftrag an SG |
| _RESPONSE_4 | binary | Hex-Antwort von SG |

<a id="job-steuern-integratoren-loeschen"></a>
### STEUERN_INTEGRATOREN_LOESCHEN

HO Getriebe und Lamellenintegratoren zurücksetzen Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

<a id="job-steuern-kalibrierung-loeschen"></a>
### STEUERN_KALIBRIERUNG_LOESCHEN

Kalibrierwinkel im EEPROM loeschen Bedingungen: Wenn (vFzg &lt; 3 km/h && VKMaus && KL15ein) oder (vFzg &lt; 3 km/h && VKMein && MKsoll &lt; 10 Nm)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

<a id="job-steuern-klassierspeicher-ruecksetzen"></a>
### STEUERN_KLASSIERSPEICHER_RUECKSETZEN

Setzt die Klassierinformation im EEPROM auf den Initialwert (unklassiert) zurück Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

<a id="job-steuern-klassierspeicher-setzen"></a>
### STEUERN_KLASSIERSPEICHER_SETZEN

Setzt die Klassierinformation im EEPROM auf die Werte des Arguments Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_OFFSET | int | EE_idxOffsetClass = Argument_1 (1 - 15) |
| ARG_GAIN | int | EE_idxGainClass = Argument_2 (1 - 15) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

<a id="job-steuern-kupplung-funktionspruefung"></a>
### STEUERN_KUPPLUNG_FUNKTIONSPRUEFUNG

Funktionsprüfung der Kupplung Bedingungen: Wenn (vFzg &lt; 3 km/h && VKMaus && KL15ein && gültige Klassierung) oder (vFzg &lt; 3 km/h && VKMein && MKsoll &lt; 10 Nm && gültige Klassierung)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei NO_VALID_CLASS, wenn die Klassierung fehlt ERROR_SYSTEM_BUSY, wenn die FSW nicht bereit ist, den Job auszuführen ERROR_TIMEOUT_JOB_START, wenn die FSW auf Jobstart nicht reagiert ERROR_REJECT_JOB_START, wenn die FSW mit Fehlermeldung auf Jobstart reagiert ERROR_TIMEOUT_JOB_PENDING, wenn die FSW den Status 'Warten auf Ausführung' nicht verlaesst ERROR_REJECT_JOB_PENDING, wenn die FSW vom Status 'Warten auf Ausführung' nicht in den Satus 'Job wird ausgeführt' wechselt ERROR_TIMEOUT_JOB, wenn die FSW den Job nicht beendet ERROR_REJECT_JOB, wenn die FSW den Job mit Fehler beendet tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |
| _REQUEST_3 | binary | Hex-Auftrag an SG |
| _RESPONSE_3 | binary | Hex-Antwort von SG |

<a id="job-steuern-lt-integratoren-loeschen"></a>
### STEUERN_LT_INTEGRATOREN_LOESCHEN

Lifetime Getriebe und Lamellenintegratoren zurücksetzen Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

<a id="job-steuern-pruefstand"></a>
### STEUERN_PRUEFSTAND

Setzt SG intern eine Sollmomentenvorgabe ohne Restbussimulation

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_PRUEFSTANDMODE | int | P_Input_enIgnMan = Argument_1 (0, 1) 0     ... Pruefstandmode AUS 1     ... Pruefstandmode EIN |
| ARG_AUTOCODIERUNG | int | 0     ... Default Codierung 255   ... Fahrzeugtypbotschaft wird verwendet 1-254 ... Autocodierungstabelle |
| ARG_NKAL | int | P_stCombEngMan = Argument_3 (0, 1) 0     ... VKM AUS 1     ... VKM EIN |
| ARG_SOLLMOMENT | int | P_S_trqCltReqMan = Argument_4 (-2, 0...1400 Nm) -2    ... Kupplung lüften |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_SYSTEM_BUSY, wenn Job bereits läuft ERROR_PARAMETER_OUT_OF_RANGE, wenn die Parameter ungültig sind ERROR_TIMEOUT_JOB_START, wenn der Job vom NLR nicht gestartet wird tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |

<a id="job-write-getriebe-integratoren"></a>
### WRITE_GETRIEBE_INTEGRATOREN

Schreibt die HO Getriebe Integratoren und den Intervall km Stand ins EEPROM Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_HO_GETRIEBE_1 | real | EE_workChain = Argument_1 (0 - 4772,185883 [kWh]) |
| ARG_HO_GETRIEBE_2 | real | EE_workClutch = Argument_2 (0 - 4772,185883 [kWh]) |
| ARG_HO_INTEGRATOR_KM | unsigned long | EE_kmVehServOil = Argument_3 (0 - 4294967295 [km]) |
| ARG_MOM_UEBERGLZ_1 | unsigned long | EE_rngRunInComp1 = Argument_4 (0 - 60000) |
| ARG_MOM_UEBERGLZ_2 | unsigned long | EE_rngRunInComp2 = Argument_5 (0 - 6000000) |
| ARG_MOM_UEBERGLZ_3 | unsigned long | EE_rngRunInComp3 = Argument_6 (0 - 60000) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

<a id="job-write-lamellen-integratoren"></a>
### WRITE_LAMELLEN_INTEGRATOREN

Schreibt die HO Lamellen Integratoren ins EEPROM Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_HO_LAMELLE_1 | real | EE_workBld1 = Argument_1 (0 - 1193,04647083 [kWh]) |
| ARG_HO_LAMELLE_2 | real | EE_workBld2  = Argument_2 (0 - 1193,04647083 [kWh]) |
| ARG_HO_LAMELLE_3 | real | EE_workBld3 = Argument_3 (0 - 1193,04647083 [kWh]) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

<a id="job-write-lt-getriebe-integratoren"></a>
### WRITE_LT_GETRIEBE_INTEGRATOREN

Schreibt die LT Getriebe Integratoren ins EEPROM Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LT_GETRIEBE_1 | real | EE_workChain_LT   = Argument_1 (0 - 4772,185883 [kWh]) |
| ARG_LT_GETRIEBE_2 | real | EE_workClutch_LT  = Argument_2 (0 - 4772,185883 [kWh]) |
| ARG_LT_OEL | real | EE_workOil_LT     = Argument_3 (0 - 2047 [kWh]) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

<a id="job-write-lt-lamellen-integratoren"></a>
### WRITE_LT_LAMELLEN_INTEGRATOREN

Schreibt die LT Lamellen Integratoren ins EEPROM Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_LT_LAMELLE_1 | real | EE_workBld1_LT = Argument_1 (0 - 1193 [kWh]) |
| ARG_LT_LAMELLE_2 | real | EE_workBld2_LT = Argument_2 (0 - 1193 [kWh]) |
| ARG_LT_LAMELLE_3 | real | EE_workBld3_LT = Argument_3 (0 - 1193 [kWh]) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

<a id="job-write-sollmoment"></a>
### WRITE_SOLLMOMENT

Setzt SG intern eine Sollmomentenvorgabe und den Sollwertqualifier auf 'Sollwert umsetzen' Bedingungen: v_fzg &lt; 20 km/h && VKMein && Kl15 ein

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_SOLLMOMENT | int | S_trqCltReq = Argument_1 (-2, 0...1400 Nm) -2... Kupplung lüften |
| ARG_TIMETICKS | int | S_stTrqCltReq = Argument_2 (0...300 s) 0... Laufenden Job abbrechen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_SYSTEM_BUSY, wenn Job bereits läuft ERROR_PARAMETER_OUT_OF_RANGE, wenn die Parameter ungültig sind ERROR_TIMEOUT_JOB_START, wenn der Job vom NLR nicht gestartet wird tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-write-vtg-sn"></a>
### WRITE_VTG_SN

Schreibt eine 20 stellige Getriebe SN ins EEPROM Bedingungen: v_fzg &lt; 3 km/h und VKMaus und Kl15ein

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_VTG_SN | string | Seriennummer des LMV-SG Beispiel: 35AA0000000 01-01-01 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei tables JobResult/JobResultExtended STATUS_TEXT |
| _REQUEST_1 | binary | Hex-Auftrag an SG |
| _RESPONSE_1 | binary | Hex-Antwort von SG |
| _REQUEST_2 | binary | Hex-Auftrag an SG |
| _RESPONSE_2 | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (134 × 2)
- [FARTTEXTE](#table-farttexte) (35 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (12 × 3)
- [IARTTEXTE](#table-iarttexte) (18 × 2)
- [UDS_TAB_ROE_AKTIV](#table-uds-tab-roe-aktiv) (3 × 2)
- [CBSKENNUNG](#table-cbskennung) (11 × 3)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (70 × 3)
- [FUMWELTTEXTE](#table-fumwelttexte) (41 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IORTTEXTE](#table-iorttexte) (61 × 3)
- [IUMWELTTEXTE](#table-iumwelttexte) (35 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (15 × 2)
- [RES_0X2541](#table-res-0x2541) (2 × 10)
- [RES_0X4012](#table-res-0x4012) (2 × 10)
- [SG_FUNKTIONEN](#table-sg-funktionen) (3 × 16)
- [TAB_4004_1](#table-tab-4004-1) (6 × 2)
- [TAB_4004_2](#table-tab-4004-2) (3 × 2)
- [TAB_4004_3](#table-tab-4004-3) (3 × 2)
- [TAB_4004_4](#table-tab-4004-4) (3 × 2)
- [TAB_ATIC_ID](#table-tab-atic-id) (3 × 2)
- [TAB_FZG_COM_STATE](#table-tab-fzg-com-state) (5 × 2)
- [TAB_FZG_ENERGY_STATE](#table-tab-fzg-energy-state) (6 × 2)
- [TAB_FZG_KL_STATE](#table-tab-fzg-kl-state) (17 × 2)
- [TAB_FZG_OP_STATE](#table-tab-fzg-op-state) (17 × 2)
- [TAB_GETRIEBEKLASSE_GAIN](#table-tab-getriebeklasse-gain) (4 × 2)
- [TAB_GETRIEBEKLASSE_GEARBOX](#table-tab-getriebeklasse-gearbox) (4 × 2)
- [TAB_GETRIEBEKLASSE_OFFSET](#table-tab-getriebeklasse-offset) (4 × 2)
- [TAB_HWE_ID](#table-tab-hwe-id) (16 × 2)
- [TAB_KALIBRIERUNG_INFO](#table-tab-kalibrierung-info) (3 × 2)
- [TAB_KLASSIERUNG_GAIN](#table-tab-klassierung-gain) (3 × 2)
- [TAB_KLASSIERUNG_OFFSET](#table-tab-klassierung-offset) (3 × 2)
- [TAB_LMV_BAUREIHE](#table-tab-lmv-baureihe) (21 × 2)
- [TAB_LMV_CODIERSTATUS](#table-tab-lmv-codierstatus) (3 × 2)
- [TAB_LMV_ECU_QUALIFIER](#table-tab-lmv-ecu-qualifier) (17 × 2)
- [TAB_LMV_EEPROM_CODIERUNG](#table-tab-lmv-eeprom-codierung) (3 × 2)
- [TAB_LMV_ISTMOMENTQUALIFIER](#table-tab-lmv-istmomentqualifier) (14 × 2)
- [TAB_LMV_SOLLWERTQUALIFIER](#table-tab-lmv-sollwertqualifier) (9 × 2)
- [TAB_LMV_VEHDATA_STAT](#table-tab-lmv-vehdata-stat) (9 × 2)
- [TAB_LMV_VV_KUPPLUNG](#table-tab-lmv-vv-kupplung) (4 × 2)
- [TAB_LMV_VV_STELLGLIED](#table-tab-lmv-vv-stellglied) (5 × 2)
- [TAB_MCU_FAMILY](#table-tab-mcu-family) (2 × 2)
- [TAB_MCU_MASK](#table-tab-mcu-mask) (6 × 2)
- [TAB_PRUEFSTAND_AUTOCODIERUNG](#table-tab-pruefstand-autocodierung) (3 × 2)
- [TAB_PRUEFSTAND_INFO](#table-tab-pruefstand-info) (3 × 2)
- [TAB_PRUEFSTAND_VKM](#table-tab-pruefstand-vkm) (3 × 2)
- [TAB_STAT_EEPROM](#table-tab-stat-eeprom) (6 × 2)
- [TAB_SUB_NLR_STATUS_10A](#table-tab-sub-nlr-status-10a) (5 × 2)
- [TAB_SUB_SM_PWM_19B](#table-tab-sub-sm-pwm-19b) (1 × 2)
- [TAB_SUB_STATUS_BRIDGE_ENABLE](#table-tab-sub-status-bridge-enable) (9 × 2)
- [TAB_SUB_STATUS_BSW_N1B](#table-tab-sub-status-bsw-n1b) (7 × 2)
- [TAB_SUB_STATUS_FSW_N3A](#table-tab-sub-status-fsw-n3a) (16 × 2)
- [TAB_SUB_STATUS_SYSTEMUPTIME_N3B](#table-tab-sub-status-systemuptime-n3b) (5 × 2)
- [TAB_SUB_ST_VEH_CON_N1A](#table-tab-sub-st-veh-con-n1a) (17 × 2)
- [TAB_SUB_S_ISM_10B](#table-tab-sub-s-ism-10b) (1 × 2)
- [TAB_SUB_TASK_ID_7B](#table-tab-sub-task-id-7b) (1 × 2)
- [TAB_SUB_WD_DISABLED_7A](#table-tab-sub-wd-disabled-7a) (5 × 2)
- [TAB_WRITE_SOLLMOMENT](#table-tab-write-sollmoment) (240 × 2)

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

Dimensions: 134 rows × 2 columns

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
| SAE_CODE | nein |
| F_HLZ | ja |
| F_SEVERITY | nein |
| F_UWB_SATZ | 21 |
| F_HLZ_VIEW | ja |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 70 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x021900 | Energiesparmode_aktiv | 0 |
| 0x021908 | Codierung: Steuergerät ist nicht codiert | 0 |
| 0x021909 | Codierung: Fehler bei Codierdatentransaktion aufgetreten | 0 |
| 0x02190A | Codierung: Signatur der Codierdaten ungültig | 0 |
| 0x02190B | Codierung: Codierdaten passen nicht zum Fahrzeug | 0 |
| 0x02190C | Codierung: Unplausible Daten während Codierdatentransaktion | 0 |
| 0x02190D | Codierung: Codierdaten nicht qualifiziert | 0 |
| 0x02FF19 | DM_TEST_APPL | 0 |
| 0x440000 | E-Maschine aktiv im Nicht Hybrid Fahrzeug | 1 |
| 0x440001 | Temperatursensor, Elektronischer Fehler | 1 |
| 0x440002 | Temperatursensor, Temperatur außerhalb Wertebereich | 1 |
| 0x440003 | Temperatursensor, Temperatur unplausibel verschieden | 1 |
| 0x44003C | Klemme 30: Unterspannung | 1 |
| 0x44003D | Klemme 30: Überspannung | 1 |
| 0x44003E | Klemme 30: Leitungsunterbrechung | 0 |
| 0x44003F | Klemme 30b: Unterspannung | 1 |
| 0x440040 | Klemme 30b: Leitungsunterbrechung | 0 |
| 0x44007C | Motorlagesensor | 0 |
| 0x44007D | Stellmotor: Fehler Lastkreis | 0 |
| 0x44007E | Elektrischer Lastkreis: fehlerhaft | 0 |
| 0x44007F | Steuergerät: interner Fehler (Watchdog) | 0 |
| 0x440080 | Steuergerät: Übertemperatur | 0 |
| 0x440081 | Dummy DTC wird nicht eingetragen | 0 |
| 0x440083 | Steuergerät: EEPROM Schreib-Lese-Fehler | 0 |
| 0x440084 | Steuergerät: EEPROM End of Life | 0 |
| 0x4400FA | Steuergerät: nicht kodiert | 0 |
| 0x4400FB | Kodierdaten: unplausibel | 0 |
| 0x4400FC | Steuergerät: unerlaubter Kreuztausch | 0 |
| 0x4400FD | Gestelltes Moment ausserhalb Momentenlinie | 0 |
| 0x4400FE | Anschlagsuche: unplausibel | 0 |
| 0x4400FF | Ankerkreiswiderstand: unplausibel | 0 |
| 0x440100 | Steuergerät: Fehler Gesamtsystem | 0 |
| 0x440101 | Ende Lebensdauer Getriebe erreicht | 0 |
| 0x440102 | Ölverschleiss | 0 |
| 0x440103 | Klassierung: fehlt | 0 |
| 0x440104 | Erstkalibrierung: fehlt | 0 |
| 0x440105 | Kalibrierung: fehlerhaft | 0 |
| 0x440107 | Steuergerät: interner Fehler | 0 |
| 0x440108 | Steuergerät: interner Fehler (Watchdog, unerwarteter Reset) | 0 |
| 0x440109 | Steuergerät: interner Fehler (Watchdog, deaktiviert) | 0 |
| 0x44010F | Steuergerät: interner Fehler | 0 |
| 0x440110 | Offset-Kompensation fehlerhaft | 0 |
| 0x440113 | Falschverbau - Allradverteilergetriebe passt nicht zur Fahrzeugvariante | 0 |
| 0x440114 | Falschverbau - Allradverteilergetriebe ATCx5L passt nicht zur Fahrzeugvariante | 0 |
| 0x440115 | VTG: Kalibrierwinkelabweichung ausserhalb Toleranz | 0 |
| 0x440116 | VTG: Klassierungsplausibilisierung fehlgeschlagen oder nicht durchführbar | 0 |
| 0x440117 | Allradverteilergetriebe temporär stillgelegt | 0 |
| 0x440118 | Allradverteilergetriebe temporär stillgelegt - Aktuatuorschutz | 0 |
| 0x440119 | Unerwartete Deaktivierung PWM | 0 |
| 0x44011A | Motorlagesensor: fehlerhaft | 0 |
| 0x44011B | Gestelltes Moment ausserhalb Momentenkennlinie | 0 |
| 0x44011C | Schutzfunktion Antriebsstrang deaktiviert | 0 |
| 0xCF441F | LMV, FlexRay: Leitungsfehler | 0 |
| 0xCF4420 | LMV, FlexRay: Logischer Busfehler | 1 |
| 0xCF4BFF | DM_TEST_COM | 0 |
| 0xCF5401 | Botschaft (Sollmoment, 43.1.4) fehlt, Empfänger LMV (A-FlexRay), Sender DSC (A-FlexRay) | 1 |
| 0xCF5402 | Botschaft (Daten_Antriebsstrang_2, 230.0.2) fehlt, Empfänger LMV (A-FlexRay), Sender DME1 (A-FlexRay) | 1 |
| 0xCF5408 | Botschaft (Kilometerstand, 276.4.8) fehlt, Empfänger LMV (A-FlexRay), Sender Kombi (FA-CAN) | 1 |
| 0xCF5409 | Botschaft (Klemmen, 116.0.2) fehlt, Empfänger LMV (A-FlexRay), Sender CAS (Body-CAN) | 1 |
| 0xCF5412 | Botschaft (Geschwindigkeit_Fahrgzeug, 55.3.4) fehlt, Empfänger LMV (A-FlexRay), Sender ICM_QL (A-FlexRay) | 1 |
| 0xCF5440 | Botschaft (Sollmoment, 43.1.4) fehlerhaft, Empfänger LMV (A-FlexRay), Sender DSC (A-FlexRay) | 1 |
| 0xCF5441 | Botschaft (Daten_Antriebsstrang_2, 230.0.2) fehlerhaft, Empfänger LMV (A-FlexRay), Sender DME1 (A-FlexRay) | 1 |
| 0xCF5449 | Botschaft (Klemmen, 116.0.2) fehlerhaft, Empfänger LMV (A-FlexRay), Sender CAS (Body-CAN) | 1 |
| 0xCF5453 | Botschaft (Geschwindigkeit_Fahrzeug, 55.3.4) fehlerhaft, Empfänger LMV (A-FlexRay), Sender ICM_QL (A-FlexRay) | 1 |
| 0xCF5480 | Schnittstelle DSC (Sollwertvorgabe Drehmoment, 43.1.4): Signal ungültig | 1 |
| 0xCF5481 | Schnittstelle DME1 (Status Gang Getriebe, 230.0.2): Signal ungültig | 1 |
| 0xCF5488 | Schnittstelle Kombi (Kilometerstand, 276.4.8): Signal ungültig | 1 |
| 0xCF5489 | Schnittstelle CAS (Klemmen, 116.0.2): Signal ungültig | 1 |
| 0xCF5493 | Schnittstelle ICM_QL(Geschwindigkeit_Fahrzeug, 55.3.4) Signal ungültig | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 41 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4000 | Status Fahrzeug Zustand | Text | High | 1 | - | 1.0 | 1.0 | 0.0 |
| 0x4003 | LMV Service Qualifier | Text | High | 2 | - | 1.0 | 1.0 | 0.0 |
| 0x4005 | Bordnetzspannung LMV Klemme 30 | V | High | unsigned char | - | 1.0 | 8.0 | 0.0 |
| 0x4006 | Bordnetzspannung LMV Klemme 30b | V | High | unsigned char | - | 1.0 | 8.0 | 0.0 |
| 0x4007 | ATIC Status Register B1 | HEX | High | unsigned int | - | - | - | - |
| 0x4008 | ATIC Status Register B2 | HEX | High | unsigned int | - | - | - | - |
| 0x4009 | ST_VEH_CON / Status BSW | 0/1 | High | 0xff | - | - | - | - |
| 0x400A | ST_VEH_CON | 0-n | High | 0xf0 | TAB_SUB_ST_VEH_CON_N1A | - | - | - |
| 0x400B | Status BSW | 0-n | High | 0x0f | TAB_SUB_STATUS_BSW_N1B | - | - | - |
| 0x400C | Status FSW / Status System Up Time | 0/1 | High | 0xff | - | - | - | - |
| 0x400D | Status System Up Time | 0-n | High | 0xc0 | TAB_SUB_STATUS_SYSTEMUPTIME_N3B | - | - | - |
| 0x400E | Status FSW | 0-n | High | 0x3F | TAB_SUB_STATUS_FSW_N3A | - | - | - |
| 0x400F | Local Condition FSW | HEX | High | unsigned int | - | - | - | - |
| 0x4013 | System Up Time | ms | High | unsigned int | - | 10.0 | 1.0 | 0.0 |
| 0x4014 | UKl30_Min_Anfilterung | V | High | unsigned char | - | 1.0 | 8.0 | 0.0 |
| 0x4017 | S12 Reset Register | HEX | High | unsigned char | - | - | - | - |
| 0x4018 | Status Watchdog Disabled / Task ID | 0/1 | High | 0xff | - | - | - | - |
| 0x4019 | STATUS_PIN_WATCHDOG_DISABLED | 0-n | High | 0xc0 | TAB_SUB_WD_DISABLED_7A | - | - | - |
| 0x401A | Task_ID | 0-n | High | 0x3f | TAB_SUB_TASK_ID_7B | - | - | - |
| 0x401B | Status_Bridge_Enable / SM_PWM | 0/1 | High | 0xff | - | - | - | - |
| 0x401C | Status_Bridge_Enable | 0-n | High | 0xE0 | TAB_SUB_STATUS_BRIDGE_ENABLE | - | - | - |
| 0x401D | SM_PWM | 0-n | High | 0x1f | TAB_SUB_SM_PWM_19B | - | - | - |
| 0x4021 | NLR Status / S_iSM | 0/1 | High | 0xffff | - | - | - | - |
| 0x4022 | NLR Status | 0-n | High | 0xc000 | TAB_SUB_NLR_STATUS_10A | - | - | - |
| 0x4023 | S_iSM | 0-n | High | 0x3FFF | TAB_SUB_S_ISM_10B | - | - | - |
| 0x4028 | Local Condition BSW | HEX | High | unsigned char | - | - | - | - |
| 0x4029 | V_VEH | km/h | High | signed char | - | 1.0 | 2.0 | 0.0 |
| 0x402A | S_rpsDltTicSMmax | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x402B | Brückentemperatur | °C | High | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0x402C | Winkel auf Niveau Aktuatorwelle | ° | High | signed int | - | 1.0 | 64.0 | 0.0 |
| 0x402D | S_nSM | 1/min | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x402E | phiCal | ° | High | unsigned char | - | 1.0 | 2.0 | -16.0 |
| 0x402F | phiCal_raw | ° | High | unsigned char | - | 1.0 | 2.0 | -16.0 |
| 0x4032 | Reserved / Status FSW | 0/1 | High | 0xff | - | - | - | - |
| 0x4033 | ATIC_Response_Command_E | HEX | High | unsigned int | - | - | - | - |
| 0x4034 | ATIC_Response_Command_D1 | HEX | High | unsigned int | - | - | - | - |
| 0x4035 | ATIC_Response_Command_D2 | HEX | High | unsigned int | - | - | - | - |
| 0x4036 | Local Condition Endstufendiagnose | HEX | High | unsigned char | - | - | - | - |
| 0x4045 | ELMOS_Error_State | HEX | High | unsigned int | - | - | - | - |
| 0x4046 | Minor Version Software | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0xXYXY | UWB_UNKNOWN | - | - | - | - | - | - | - |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | ja |
| F_SEVERITY | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 61 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x43FFFE | DM_QUEUE_EMPTY | 0 |
| 0x43FFFF | DM_QUEUE_FULL | 0 |
| 0x440004 | NVM_E_CONTROL_FAILED | 0 |
| 0x440005 | NVM_E_ERASE_FAILED | 0 |
| 0x440006 | NVM_E_READ_ALL_FAILED | 0 |
| 0x440007 | NVM_E_READ_FAILED | 0 |
| 0x440008 | NVM_E_WRITE_ALL_FAILED | 0 |
| 0x440009 | NVM_E_WRITE_FAILED | 0 |
| 0x44000A | NVM_E_WRONG_CONFIG_ID | 0 |
| 0x44000B | Steuergerät: interner Fehler (XGATE) | 0 |
| 0x44000C | DM_EVENT_ZEITBOTSCHAFTTIMEOUT | 0 |
| 0x44000D | Temperatursensor, Temperatur unplausibel verschieden | 1 |
| 0x440010 | DM_QUEUE_DELETED | 0 |
| 0x440011 | VSM_EVENT_VEHICLESTATE | 0 |
| 0x440082 | Steuergerät: interner Fehler (HW-Register) | 0 |
| 0x440106 | Notlaufregler: Abbruch | 0 |
| 0x44010E | Steuergerät: interner Fehler (VTG Software: Systemüberlastung) | 0 |
| 0x44011C | Schutzfunktion Antriebsstrang deaktiviert | 0 |
| 0xCF5403 | Botschaft (Daten_Antriebsstrang_3, 251.1.4) fehlt, Empfänger LMV (A-FlexRay), Sender DME1 (A-FlexRay) | 1 |
| 0xCF5404 | Botschaft (Kurbelwelle_Fahrpedal, 40.1.4) fehlt, Empfänger LMV (A-FlexRay), Sender DME1 (A-FlexRay) | 1 |
| 0xCF5405 | Botschaft (Bremsmoment, 43.3.4) fehlt, Empfänger LMV (A-FlexRay), Sender DSC (A-FlexRay) | 1 |
| 0xCF5406 | Botschaft (Drehzahl_Rad, 46.0.1) fehlt, Empfänger LMV (A-FlexRay), Sender DSC (A-FlexRay) | 1 |
| 0xCF5407 | Botschaft (Querbeschleunigung, 55.0.2) fehlt, Empfänger LMV (A-FlexRay), Sender ICM_QL (A-FlexRay) | 1 |
| 0xCF540A | Botschaft (Relativzeit, 276.2.8) fehlt, Empfänger LMV (A-FlexRay), Sender Kombi (FA-CAN) | 1 |
| 0xCF540B | Botschaft (Status_Stabilisierung, 47.1.2) fehlt, Empfänger LMV (A-FlexRay), Sender DSC (A-FlexRay) | 1 |
| 0xCF540C | Botschaft (Lenkwinkel, 56.1.2) fehlt, Empfänger LMV (A-FlexRay), Sender ICM_QL (A-FlexRay) | 1 |
| 0xCF540D | Botschaft (Giergeschwindigkeit, 56.0.2) fehlt, Empfänger LMV (A-FlexRay), Sender ICM_QL (A-FlexRay) | 1 |
| 0xCF540F | Botschaft (Radmoment_Antrieb_5, 40.3.4) fehlt, Empfänger LMV (A-FlexRay), Sender DME1 (A-FlexRay) | 1 |
| 0xCF5414 | Botschaft (Kurbelwelle_Fahrpedal, 40.1.4) fehlt, Empfänger LMV (A-FlexRay), Sender DME1 (A-FlexRay) | 1 |
| 0xCF5415 | Botschaft (Bremsmoment, 43.3.4) fehlt, Empfänger LMV (A-FlexRay), Sender DSC (A-FlexRay) | 1 |
| 0xCF5416 | Botschaft (Radmoment_Antrieb_4, 40.3.4) fehlt, Empfänger LMV (A-FlexRay), SenderDME1 (A-FlexRay) | 1 |
| 0xCF5442 | Botschaft (Daten_Antriebsstrang_3, 251.1.4) fehlerhaft, Empfänger LMV (A-FlexRay), Sender DME1 (A-FlexRay) | 1 |
| 0xCF5443 | Botschaft (Kurbelwelle, 40.1.4) fehlerhaft, Empfänger LMV (A-FlexRay), Sender DME1 (A-FlexRay) | 1 |
| 0xCF5444 | Botschaft (Fahrpedal, 40.1.4) fehlerhaft, Empfänger LMV (A-FlexRay), Sender DME1 (A-FlexRay) | 1 |
| 0xCF5445 | Botschaft (Bremsmoment, 43.3.4) fehlerhaft, Empfänger LMV (A-FlexRay), Sender DSC (A-FlexRay) | 1 |
| 0xCF5446 | Botschaft (Drehzahl_Rad, 46.0.1) fehlerhaft, Empfänger LMV (A-FlexRay), Sender DSC (A-FlexRay) | 1 |
| 0xCF5447 | Botschaft (Querbeschleunigung, 55.0.2) fehlerhaft, Empfänger LMV (A-FlexRay), Sender ICM_QL (A-FlexRay) | 1 |
| 0xCF544B | Botschaft (Status_Stabilisierung, 47.1.2) fehlerhaft, Empfänger LMV (A-FlexRay), Sender DSC (A-FlexRay) | 1 |
| 0xCF544C | Botschaft (Lenkwinkel, 56.1.2) fehlerhaft, Empfänger LMV (A-FlexRay), Sender ICM_QL (A-FlexRay) | 1 |
| 0xCF544D | Botschaft (Giergeschwindigkeit, 56.0.2) fehlerhaft, Empfänger LMV (A-FlexRay), Sender ICM_QL (A-FlexRay) | 1 |
| 0xCF544F | Botschaft (Radmoment_Antrieb_4, 40.3.4) fehlerhaft, Empfänger LMV (A-FlexRay), Sender DME1 (A-FlexRay) | 1 |
| 0xCF5450 | Botschaft (Radmoment_Antrieb_5, 40.3.4) fehlerhaft, Empfänger LMV (A-FlexRay), Sender DME1 (A-FlexRay) | 1 |
| 0xCF5454 | Botschaft (Kurbelwelle, 40.1.4) fehlerhaft, Empfänger LMV (A-FlexRay), Sender DME1 (A-FlexRay) | 1 |
| 0xCF5455 | Botschaft (Bremsmoment, 43.3.4) fehlerhaft, Empfänger LMV (A-FlexRay), Sender DSC (A-FlexRay) | 1 |
| 0xCF5456 | Botschaft (Radmoment_Antrieb_4, 40.3.4) fehlerhaft, Empfänger LMV (A-FlexRay), Sender DME1 (A-FlexRay) | 1 |
| 0xCF5482 | Schnittstelle DME1 (Übersetzung Hinterachse, 251.1.4): Signal ungültig | 1 |
| 0xCF5483 | Schnittstelle DME1 (Motordrehzahl, 40.1.4): Signal ungültig | 1 |
| 0xCF5484 | Schnittstelle DME1 (Istwinkel Fahrpedal, 40.1.4): Signal ungültig | 1 |
| 0xCF5485 | Schnittstelle DSC (Bremsmoment, 43.3.4): Signal ungültig | 1 |
| 0xCF5486 | Schnittstelle DSC (Raddrehzahl, 46.0.1): Signal ungültig | 1 |
| 0xCF5487 | Schnittstelle ICM_QL (Querbeschleunigung, 55.0.2): Signal ungültig | 1 |
| 0xCF548A | Schnittstelle Kombi (Relativzeit, 276.2.8): Signal ungültig | 1 |
| 0xCF548B | Schnittstelle DSC (Status Bremseingriff, 47.1.2): Signal ungültig | 1 |
| 0xCF548C | Schnittstelle ICM_QL (Lenkwinkel, 56.1.2): Signal ungültig | 1 |
| 0xCF548D | Schnittstelle ICM_QL (Giergeschwindigkeit, 56.0.2): Signal ungültig | 1 |
| 0xCF548F | Schnittstelle DME1 (Status Kraftschluss, 40.3.4): Signal ungültig | 1 |
| 0xCF5490 | Schnittstelle DME1 (Radmoment koordiniert, 40.3.4): Signal ungültig | 1 |
| 0xCF5494 | Schnittstelle DME1 (Kurbelwelle, 40.1.4): Signal ungültig | 1 |
| 0xCF5495 | Schnittstelle DSC (Bremsmoment, 43.3.4): Signal ungültig | 1 |
| 0xCF5496 | Schnittstelle DME1 (Status Kraftschluss, 40.3.4): Signal ungültig | 1 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 35 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4000 | Status Fahrzeug Zustand | Text | High | 1 | - | 1.0 | 1.0 | 0.0 |
| 0x4003 | LMV Service Qualifier | Text | High | 2 | - | 1.0 | 1.0 | 0.0 |
| 0x4005 | Bordnetzspannung LMV Klemme 30 | V | High | unsigned char | - | 1.0 | 8.0 | 0.0 |
| 0x4006 | Bordnetzspannung LMV Klemme 30b | V | High | unsigned char | - | 1.0 | 8.0 | 0.0 |
| 0x4007 | ATIC Status Register B1 | HEX | High | unsigned int | - | - | - | - |
| 0x4008 | ATIC Status Register B2 | HEX | High | unsigned int | - | - | - | - |
| 0x4009 | ST_VEH_CON / Status BSW | 0/1 | High | 0xff | - | - | - | - |
| 0x400A | ST_VEH_CON | 0-n | High | 0xf0 | TAB_SUB_ST_VEH_CON_N1A | - | - | - |
| 0x400B | Status BSW | 0-n | High | 0x0f | TAB_SUB_STATUS_BSW_N1B | - | - | - |
| 0x400C | Status FSW / Status System Up Time | 0/1 | High | 0xff | - | - | - | - |
| 0x400D | Status System Up Time | 0-n | High | 0xc0 | TAB_SUB_STATUS_SYSTEMUPTIME_N3B | - | - | - |
| 0x400E | Status FSW | 0-n | High | 0x3F | TAB_SUB_STATUS_FSW_N3A | - | - | - |
| 0x400F | Local Condition FSW | HEX | High | unsigned int | - | - | - | - |
| 0x4013 | System Up Time | ms | High | unsigned int | - | 10.0 | 1.0 | 0.0 |
| 0x4017 | S12 Reset Register | HEX | High | unsigned char | - | - | - | - |
| 0x4018 | Status Watchdog Disabled / Task ID | 0/1 | High | 0xff | - | - | - | - |
| 0x4019 | STATUS_PIN_WATCHDOG_DISABLED | 0-n | High | 0xc0 | TAB_SUB_WD_DISABLED_7A | - | - | - |
| 0x401A | Task_ID | 0-n | High | 0x3f | TAB_SUB_TASK_ID_7B | - | - | - |
| 0x401B | Status_Bridge_Enable / SM_PWM | 0/1 | High | 0xff | - | - | - | - |
| 0x401C | Status_Bridge_Enable | 0-n | High | 0xE0 | TAB_SUB_STATUS_BRIDGE_ENABLE | - | - | - |
| 0x401D | SM_PWM | 0-n | High | 0x1f | TAB_SUB_SM_PWM_19B | - | - | - |
| 0x4021 | NLR Status / S_iSM | 0/1 | High | 0xffff | - | - | - | - |
| 0x4022 | NLR Status | 0-n | High | 0xc000 | TAB_SUB_NLR_STATUS_10A | - | - | - |
| 0x4023 | S_iSM | 0-n | High | 0x3FFF | TAB_SUB_S_ISM_10B | - | - | - |
| 0x4028 | Local Condition BSW | HEX | High | unsigned char | - | - | - | - |
| 0x4029 | V_VEH | km/h | High | signed char | - | 1.0 | 2.0 | 0.0 |
| 0x402A | S_rpsDltTicSMmax | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0x402B | Brückentemperatur | °C | High | unsigned char | - | 1.0 | 1.0 | -40.0 |
| 0x402C | Winkel auf Niveau Aktuatorwelle | ° | High | signed int | - | 1.0 | 64.0 | 0.0 |
| 0x402D | S_nSM | 1/min | High | signed char | - | 1.0 | 1.0 | 0.0 |
| 0x402E | phiCal | ° | High | unsigned char | - | 1.0 | 2.0 | -16.0 |
| 0x402F | phiCal_raw | ° | High | unsigned char | - | 1.0 | 2.0 | -16.0 |
| 0x4045 | ELMOS_Error_State | HEX | High | unsigned int | - | - | - | - |
| 0x4046 | Minor Version Software | - | High | unsigned char | - | 1.0 | 1.0 | 0.0 |
| 0xXYXY | UWB_UNKNOWN | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 15 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x7F | Negative Response |
| 0xE0 | ERROR_SYSTEM_BUSY |
| 0xE1 | ERROR_TIMEOUT_JOB_START |
| 0xE2 | ERROR_REJECT_JOB_START |
| 0xE3 | ERROR_TIMEOUT_JOB_PENDING |
| 0xE4 | ERROR_REJECT_JOB_PENDING |
| 0xE5 | ERROR_TIMEOUT_JOB |
| 0xE6 | ERROR_REJECT_JOB |
| 0xE9 | ERROR_PARAMETER_OUT_OF_RANGE |
| 0xF0 | ERROR_JOB_ABORTED |
| 0xF1 | ERROR_STATE_ERROR |
| 0xF2 | ERROR_FSM_NOT_IDLE |
| 0xF8 | ERROR_EEPROM_ERROR_1 |
| 0xF9 | ERROR_EEPROM_ERROR_2 |
| 0xXY | ERROR_UNKNOWN |

<a id="table-res-0x2541"></a>
### RES_0X2541

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_CALID_TEXT | TEXT | high | string[16] | - | - | 1.0 | 1.0 | 0.0 | Cal-ID auslesen (hier muss die Cal-ID wie bei Mode $09 (PID $04) ausgegeben werden). |
| STAT_CVN_WERT | HEX | high | unsigned long | - | - | - | - | - | CVN auslesen (hier muss die CVN wie bei Mode $09 (PID $06) ausgegeben werden) |

<a id="table-res-0x4012"></a>
### RES_0X4012

Dimensions: 2 rows × 10 columns

| RESULTNAME | EINHEIT | L/H | DATENTYP | MASKE | NAME | MUL | DIV | ADD | INFO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STAT_PRUEFSTANDSMODE_WERT | - | high | int | - | - | 1.0 | 1.0 | 0.0 | Aktueller Pruefstandsmodus 0 : Pruefstandsmodus nicht aktiviert 1 : Pruefstandsmodus aktiviert |
| STAT_PRUEFSTANDSMODE_TEXT | TEXT | high | string | - | - | 1.0 | 1.0 | 0.0 | Tabelle  TAB_PRUEFSTAND_INFO |

<a id="table-sg-funktionen"></a>
### SG_FUNKTIONEN

Dimensions: 3 rows × 16 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD | SG_ADR | SERVICE | ARG_TABELLE | RES_TABELLE |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| STATUS_CALCVN | 0x2541 | - | Cal-ID (Calibration-ID) und CVN(Calibration Verification Number) auslesen. (OBD-Umfänge)   Byte-Layout: 20 Byte lang 00-15 = STAT_CALID_WERT 16-19 = STAT_CVN_EINH als Hex  unit32 im Intel Format | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x2541 |
| STATUS_PRUEFSTAND | 0x4012 | - | Liste der Signale, die den Wertebereich überschritten haben | - | - | - | - | - | - | - | - | - | 22 | - | RES_0x4012 |
| STEUERN_PRUEFSTAND | 0xF016 | - | Setzt SG intern eine Sollmomentenvorgabe ohne Restbussimulation | - | - | - | - | - | - | - | - | - | 31 | - | - |

<a id="table-tab-4004-1"></a>
### TAB_4004_1

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0800 | Initialisierung |
| 0x0200 | Service verfügbar |
| 0x0B00 | Service temporär eingeschrankt verfügbar - Akutschutz aktiv |
| 0x0300 | Service permanent eingeschrankt verfügbar - Langzeitschutz aktiv |
| 0x0600 | Service nicht verfügbar - Fehler |
| 0x0E00 | Service nicht verfügbar - Standby |

<a id="table-tab-4004-2"></a>
### TAB_4004_2

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Notlaufregler nicht aktiv |
| 0x0080 | Notlaufregler aktiv |
| 0xFFFF | unplausibel |

<a id="table-tab-4004-3"></a>
### TAB_4004_3

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | Position LMV Stellglied bekannt |
| 0x0040 | Position LMV Stellglied nicht bekannt |
| 0xFFFF | unplausibel |

<a id="table-tab-4004-4"></a>
### TAB_4004_4

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | LMV Schutzfunktion nicht aktiv |
| 0x0020 | LMV Schutzfunktion aktiv |
| 0xFFFF | unplausibel |

<a id="table-tab-atic-id"></a>
### TAB_ATIC_ID

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0340 | silicon A1 or A2 |
| 0x0341 | silicon B1 |
| 0xFFFF | unbekannt |

<a id="table-tab-fzg-com-state"></a>
### TAB_FZG_COM_STATE

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Fehlerspeicherfreigabe |
| 1 | Fehlerspeichersperre |
| 2 | Reserve |
| 3 | Signal ungültig |
| 0xXY | unplausibel |

<a id="table-tab-fzg-energy-state"></a>
### TAB_FZG_ENERGY_STATE

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ENSTATE_GOOD |
| 1 | ENSTATE_OK |
| 2 | ENSTATE_SHORTAGE |
| 3 | ENSTATE_SEVERE_SHORTAGE |
| 15 | Signal ungültig |
| 0xXY | unplausibel |

<a id="table-tab-fzg-kl-state"></a>
### TAB_FZG_KL_STATE

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Initialisierung |
| 1 | Reserve |
| 2 | KL30 |
| 3 | KL30F-Änderung |
| 4 | KL30F-Ein |
| 5 | KL30B-Änderung |
| 6 | KL30B-Ein |
| 7 | KLR-Änderung |
| 8 | KLR-Ein |
| 9 | KL15-Änderung |
| 10 | KL15-Ein |
| 11 | KL50-Verzögerung |
| 12 | KL50-Änderung |
| 13 | KL50-Ein |
| 14 | Fehler |
| 15 | Signal ungültig |
| 0xXY | unplausibel |

<a id="table-tab-fzg-op-state"></a>
### TAB_FZG_OP_STATE

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Initialisierung |
| 1 | Standby, Fahrer abwesend |
| 2 | Basisbetrieb, Fahrer anwesend |
| 3 | Basisbetrieb, Fahrzeug rollt |
| 4 | Motornachlauf |
| 5 | Zündung ein |
| 6 | Zündung ein, Fahrzeug rollt |
| 7 | Motor an, Fahrzeug steht |
| 8 | Fahrt |
| 9 | Bevorstehender Motorstart |
| 10 | Bevorstehender Motorstart, Fahrzeug rollt |
| 11 | Motorstart |
| 12 | Motorstart, Fahrzeug rollt |
| 13 | Waschstrassenbetrieb |
| 14 | Fehler |
| 15 | Signal ungültig |
| 0xXY | unplausibel |

<a id="table-tab-getriebeklasse-gain"></a>
### TAB_GETRIEBEKLASSE_GAIN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Steigung unklassiert |
| 1 | Steigung klassiert ATC x50 |
| 2 | Steigung klassiert ATClight |
| 0xXY | nicht definiert |

<a id="table-tab-getriebeklasse-gearbox"></a>
### TAB_GETRIEBEKLASSE_GEARBOX

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Getriebe unklassiert |
| 1 | Getriebeklasse ATC x50 |
| 2 | Getriebeklasse ATClight |
| 0xXY | nicht definiert |

<a id="table-tab-getriebeklasse-offset"></a>
### TAB_GETRIEBEKLASSE_OFFSET

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Offset unklassiert |
| 1 | Offset klassiert ATC x50 |
| 2 | Offset klassiert ATClight |
| 0xXY | nicht definiert |

<a id="table-tab-hwe-id"></a>
### TAB_HWE_ID

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 159 | B4 |
| 149 | B5 |
| 139 | B6 |
| 129 | B7 |
| 99 | C0 |
| 89 | C1 |
| 79 | C2 |
| 69 | C3 |
| 29 | D0 |
| 19 | D1 |
| 09 | D2 |
| 00 | D3 |
| 250 | Defaultwert (entspricht B4) |
| 254 | Initialwert (Signal ungültig) |
| 255 | Fehlerwert (Signal ungültig) |
| 0xXY | unbekannt |

<a id="table-tab-kalibrierung-info"></a>
### TAB_KALIBRIERUNG_INFO

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht kalibriert |
| 1 | kalibriert |
| 0xXY | unplausibel |

<a id="table-tab-klassierung-gain"></a>
### TAB_KLASSIERUNG_GAIN

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Steigung unklassiert, Ersatzwert neutrale Klasse |
| 1 | Steigung klassiert |
| 0xXY | nicht definiert |

<a id="table-tab-klassierung-offset"></a>
### TAB_KLASSIERUNG_OFFSET

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Offset unklassiert, Ersatzwert neutrale Offset Klasse |
| 1 | Offset klassiert |
| 0xXY | nicht definiert |

<a id="table-tab-lmv-baureihe"></a>
### TAB_LMV_BAUREIHE

Dimensions: 21 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 24 | F01, 7er |
| 25 | F02, 7er lang |
| 27 | F07, 5er GT |
| 28 | F10, 5er |
| 29 | F11, 5er Touring |
| 30 | F12, 6er |
| 31 | F13, 6er C |
| 33 | F31 |
| 34 | F32 |
| 35 | F33 |
| 36 | F20 |
| 37 | F30 |
| 38 | F22 |
| 39 | F23 |
| 41 | F25 |
| 44 | F21 |
| 45 | F15 |
| 46 | F16 |
| 50 | F06 |
| 51 | F34 |
| 0xFF | unbekannt |

<a id="table-tab-lmv-codierstatus"></a>
### TAB_LMV_CODIERSTATUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Codierung passt nicht zu Fahrzeugdaten, aktuell ungültig codiert |
| 0x01 | Codierung passt zu Fahrzeugdaten, gültig codiert |
| 0xFF | nicht definiert |

<a id="table-tab-lmv-ecu-qualifier"></a>
### TAB_LMV_ECU_QUALIFIER

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Zustand Initialisierung |
| 0x01 | Zustand Normalbetrieb |
| 0x02 | Zustand Normalbetrieb / Überspannung sensiert |
| 0x03 | Zustand Normalbetrieb / Unterspannung sensiert |
| 0x04 | Zustand Diagnose |
| 0x05 | Zustand Diagnose / Überspannung sensiert |
| 0x06 | Zustand Diagnose / Unterspannung sensiert |
| 0x07 | Zustand Powerdown |
| 0x08 | Zustand PowerSave |
| 0x09 | Zustand Nicht verfügbar |
| 0x0A | Zustand Reset |
| 0x0B | Zustand Reserviert11 |
| 0x0C | Zustand Reserviert12 |
| 0x0D | Zustand Reserviert13 |
| 0x0E | Zustand Reserviert14 |
| 0x0F | Signal ungültig |
| 0xXY | unplausibel |

<a id="table-tab-lmv-eeprom-codierung"></a>
### TAB_LMV_EEPROM_CODIERUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | keine gültige Erstcodierung vorhanden |
| 0x01 | gültige Erstcodierung vorhanden |
| 0xFF | nicht definiert |

<a id="table-tab-lmv-istmomentqualifier"></a>
### TAB_LMV_ISTMOMENTQUALIFIER

Dimensions: 14 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 8 | Initialisierung |
| 1 | Signalwert ist gültig und abgesichert und plausibilisiert, Zustand/Status permanent |
| 9 | Signalwert ist gültig und abgesichert, Zustand/Status temporär |
| 2 | Signalwert ist gültig, Zustand/Status permanent |
| 10 | Signalwert ist gültig, Zustand/Status temporär |
| 3 | Signalqualität bzw. Überwachung eingeschränkt, Zustand/Status permanent |
| 11 | Signalqualität bzw. Überwachung eingeschränkt, Zustand/Status temporär |
| 4 | Ersatzwert ist im Nutzsignal gesetzt, Zustand/Status permanent |
| 12 | Abgleichwert ist im Nutzsignal gesetzt, Zustand/Status temporär |
| 6 | Signalwert ist ungültig, Zustand/Status permanent |
| 14 | Signalwert ist ungültig, Zustand/Status temporär |
| 7 | Sensor nicht vorhanden |
| 15 | Signal ungültig |
| 0xFF | nicht definiert |

<a id="table-tab-lmv-sollwertqualifier"></a>
### TAB_LMV_SOLLWERTQUALIFIER

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x20 | Sollwert umsetzen |
| 0x28 | Kupplung schnell öffnen |
| 0x60 | Sollwert nicht umsetzen, Notlaufregler |
| 0x61 | Sollwert nicht umsetzen, Notlaufregler, RTA Abgleich |
| 0x62 | Sollwert nicht umsetzen, Notlaufregler, Kupplung schnell öffnen |
| 0x70 | Sollwert nicht vorhanden, Heckantrieb |
| 0x80 | Initialisierung |
| 0xE0 | Sollwert nicht vorhanden, Standby |
| 0xFF | Sollwert ungültig |

<a id="table-tab-lmv-vehdata-stat"></a>
### TAB_LMV_VEHDATA_STAT

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | 000 - Signal nicht empfangen (TO oder Busfehler usw.) |
| 0x01 | 001 - Signal empfangen/ In Codierung akzeptiert (alles i.O.) |
| 0x02 | 010 - Signal empfangen/ nicht akzeptiert (Wert nicht in der Autocodierungstabelle gefunden)  |
| 0x03 | 011 - Signal empfangen/ nicht geprüft (alle weiteren Werte, die zwar empfangen aber nicht mehr in der Autocodierungstabelle geprüft wurden)  |
| 0x04 | 100 - Defaultwert |
| 0x05 | 101 - Klemmenwechsel erforderlich |
| 0x06 | 110 - EEPROM-Daten corrupt, Klemmenwechsel erforderlich |
| 0x07 | 111 - Timeout beim Schreiben bzw. Konsistenz-Check von NVM-Daten |
| 0xFF | nicht definiert |

<a id="table-tab-lmv-vv-kupplung"></a>
### TAB_LMV_VV_KUPPLUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | volle Verfügbarkeit Kupplung Stufe 0, THR_STRS_CLT = 0-50% |
| 0x0001 | eingeschränkte Verfügbarkeit Kupplung Stufe 1, THR_STRS_CLT = 51-80% |
| 0x0002 | eingeschränkte Verfügbarkeit Kupplung Stufe 2, THR_STRS_CLT = 81-100% |
| 0xFFFF | unplausibel |

<a id="table-tab-lmv-vv-stellglied"></a>
### TAB_LMV_VV_STELLGLIED

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | volle Verfügbarkeit Stellglied Stufe 0, THR_STRS_MOT = 0-30% |
| 0x0004 | eingeschränkte Verfügbarkeit Stellglied Stufe 1, THR_STRS_MOT = 31-50% |
| 0x0008 | eingeschränkte Verfügbarkeit Stellglied Stufe 2, THR_STRS_MOT = 51-80% |
| 0x000C | eingeschränkte Verfügbarkeit Stellglied Stufe 3, THR_STRS_MOT = 81-100% |
| 0xFFFF | unplausibel |

<a id="table-tab-mcu-family"></a>
### TAB_MCU_FAMILY

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xD4 | MC9S12XF512 (or family derivate) |
| 0xXY | unbekannt |

<a id="table-tab-mcu-mask"></a>
### TAB_MCU_MASK

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x80 | 0M64J (nicht-eindeutige Detektionsmethode) |
| 0x81 | 1M64J or 2M64J (nicht-eindeutige Detektionsmethode) |
| 0xD4800001 | 0M64J |
| 0xD4810001 | 1M64J |
| 0xD4810006 | 2M64J |
| 0xXY | unbekannt |

<a id="table-tab-pruefstand-autocodierung"></a>
### TAB_PRUEFSTAND_AUTOCODIERUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Default Codierung |
| 0xFF | Fahrzeugtypbotschaft wird verwendet |
| 0xXY | unplausibel |

<a id="table-tab-pruefstand-info"></a>
### TAB_PRUEFSTAND_INFO

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Pruefstandsmodus nicht aktiviert |
| 0x01 | Pruefstandsmodus aktiviert |
| 0xXY | unplausibel |

<a id="table-tab-pruefstand-vkm"></a>
### TAB_PRUEFSTAND_VKM

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | VKM Aus |
| 0x01 | VKM Ein |
| 0xXY | unplausibel |

<a id="table-tab-stat-eeprom"></a>
### TAB_STAT_EEPROM

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | EEPROM ok,  STAT_EEPROM_xy_WERT=Dead/Rdy Sektoren |
| 0x01 | EEPROM Test nicht ok - Abfrage fehlgeschlagen, STAT_EEPROM_xy_WERT ungültig |
| 0x20 | Falsche Partionierung des EEPROM,  STAT_EEPROM_xy_WERT=ERPART |
| 0x40 | Falsche Partionierung des EEPROM,  STAT_EEPROM_xy_WERT=DFPART |
| 0x80 | EEPROM defekt,  STAT_EEPROM_xy_WERT=Dead/Rdy Sektoren |
| 0xXY | unbekannt |

<a id="table-tab-sub-nlr-status-10a"></a>
### TAB_SUB_NLR_STATUS_10A

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x0000 | NLR nicht aktiv |
| 0x4000 | NLR aktiv |
| 0x8000 | NLR Abbruch |
| 0xC000 | Einachsrollen-Prüfstandmodus |
| 0xffff | nicht definiert |

<a id="table-tab-sub-sm-pwm-19b"></a>
### TAB_SUB_SM_PWM_19B

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xffff | 0xXY |

<a id="table-tab-sub-status-bridge-enable"></a>
### TAB_SUB_STATUS_BRIDGE_ENABLE

Dimensions: 9 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | ATIC=0,BSW=0,FSW=0 |
| 0x20 | ATIC=0,BSW=0,FSW=1 |
| 0x40 | ATIC=0,BSW=1,FSW=0 |
| 0x60 | ATIC=0,BSW=1,FSW=1 |
| 0x80 | ATIC=1,BSW=0,FSW=0 |
| 0xA0 | ATIC=1,BSW=0,FSW=1 |
| 0xC0 | ATIC=1,BSW=1,FSW=0 |
| 0xE0 | ATIC=1,BSW=1,FSW=1 |
| 0xffff | nicht definiert |

<a id="table-tab-sub-status-bsw-n1b"></a>
### TAB_SUB_STATUS_BSW_N1B

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | APPL_STATE_STARTUP |
| 0x01 | APPL_STATE_NORMAL_OPERATION |
| 0x02 | APPL_STATE_RESTART |
| 0x03 | APPL_STATE_RESET |
| 0x04 | APPL_STATE_SHUTDOWN |
| 0x05 | APPL_STATE_CANCEL_SHUTDOWN |
| 0xffff | nicht definiert |

<a id="table-tab-sub-status-fsw-n3a"></a>
### TAB_SUB_STATUS_FSW_N3A

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Defaultwert |
| 1 | Kalibrierung läuft |
| 2 | Momentenstellen |
| 3 | erhöhte Toleranz Aktuatorschutzmodell (inaktiv) |
| 4 | Maximalmoment begrenzt Aktuatorschutzmodell |
| 5 | Kupplung ist geöffnet |
| 6 | Anschlagsuche |
| 7 | Kupplung wird geöffnet |
| 8 | Erstkalibrierung läuft |
| 9 | Ersatzprogramm wird ausgeführt |
| 10 | keine Kupplungsansteuerung möglich |
| 11 | Ersatzprogramm beenden |
| 21 | Position unbekannt (Anschlagsuche fehlgeschlagen) |
| 0x3e | Initialwert |
| 0x3f | Fehlerwert |
| 0xffff | unplausibel |

<a id="table-tab-sub-status-systemuptime-n3b"></a>
### TAB_SUB_STATUS_SYSTEMUPTIME_N3B

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | 0-Power_On |
| 0x40 | 1-KL15_an |
| 0x80 | 2-VKM_ein |
| 0xC0 | 3-Nachlauf |
| 0xffff | nicht definiert |

<a id="table-tab-sub-st-veh-con-n1a"></a>
### TAB_SUB_ST_VEH_CON_N1A

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | VSM_STM_STATE_INIT |
| 0x10 | VSM_STM_STATE_STANDBY |
| 0x20 | VSM_STM_STATE_BASICOP |
| 0x30 | VSM_STM_STATE_BASICOP_ROLL |
| 0x40 | VSM_STM_STATE_15OFF_DRIVE |
| 0x50 | VSM_STM_STATE_IGNITION |
| 0x60 | VSM_STM_STATE_IGNITION_ROLL |
| 0x70 | VSM_STM_STATE_ENG_IDLE |
| 0x80 | VSM_STM_STATE_DRIVE |
| 0x90 | VSM_STM_STATE_ENG_START_PRE |
| 0xA0 | VSM_STM_STATE_ENG_START_PRE_ROLL |
| 0xB0 | VSM_STM_STATE_ENG_START |
| 0xC0 | VSM_STM_STATE_ENG_START_ROLL |
| 0xD0 | VSM_STM_STATE_WASH |
| 0xE0 | VSM_STM_STATE_ERROR |
| 0xF0 | VSM_STM_STATE_INVALID |
| 0xffff | nicht definiert |

<a id="table-tab-sub-s-ism-10b"></a>
### TAB_SUB_S_ISM_10B

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xffff | 0xXY |

<a id="table-tab-sub-task-id-7b"></a>
### TAB_SUB_TASK_ID_7B

Dimensions: 1 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0xffff | 0xXY |

<a id="table-tab-sub-wd-disabled-7a"></a>
### TAB_SUB_WD_DISABLED_7A

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Port PJ1=Low -- Port PJ2=Low |
| 0x40 | Port PJ1=Low -- Port PJ2=High |
| 0x80 | Port PJ1=High -- Port PJ2=Low |
| 0xC0 | Port PJ1=High -- Port PJ2=High |
| 0xffff | nicht definiert |

<a id="table-tab-write-sollmoment"></a>
### TAB_WRITE_SOLLMOMENT

Dimensions: 240 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 61 | 0x3D |
| 62 | 0x3E |
| 63 | 0x3F |
| 64 | 0x3F |
| 65 | 0x40 |
| 66 | 0x41 |
| 67 | 0x41 |
| 68 | 0x42 |
| 69 | 0x43 |
| 70 | 0x43 |
| 71 | 0x44 |
| 72 | 0x45 |
| 73 | 0x45 |
| 74 | 0x46 |
| 75 | 0x47 |
| 76 | 0x47 |
| 77 | 0x48 |
| 78 | 0x48 |
| 79 | 0x49 |
| 80 | 0x4A |
| 81 | 0x4A |
| 82 | 0x4B |
| 83 | 0x4B |
| 84 | 0x4C |
| 85 | 0x4D |
| 86 | 0x4D |
| 87 | 0x4E |
| 88 | 0x4E |
| 89 | 0x4F |
| 90 | 0x4F |
| 91 | 0x50 |
| 92 | 0x51 |
| 93 | 0x51 |
| 94 | 0x52 |
| 95 | 0x52 |
| 96 | 0x53 |
| 97 | 0x53 |
| 98 | 0x54 |
| 99 | 0x55 |
| 100 | 0x55 |
| 101 | 0x56 |
| 102 | 0x56 |
| 103 | 0x57 |
| 104 | 0x57 |
| 105 | 0x58 |
| 106 | 0x58 |
| 107 | 0x59 |
| 108 | 0x59 |
| 109 | 0x5A |
| 110 | 0x5A |
| 111 | 0x5B |
| 112 | 0x5B |
| 113 | 0x5C |
| 114 | 0x5C |
| 115 | 0x5D |
| 116 | 0x5D |
| 117 | 0x5E |
| 118 | 0x5E |
| 119 | 0x5F |
| 120 | 0x5F |
| 121 | 0x60 |
| 122 | 0x60 |
| 123 | 0x61 |
| 124 | 0x61 |
| 125 | 0x62 |
| 126 | 0x62 |
| 127 | 0x63 |
| 128 | 0x63 |
| 129 | 0x64 |
| 130 | 0x64 |
| 131 | 0x65 |
| 132 | 0x65 |
| 133 | 0x66 |
| 134 | 0x66 |
| 135 | 0x67 |
| 136 | 0x67 |
| 137 | 0x68 |
| 138 | 0x68 |
| 139 | 0x69 |
| 140 | 0x69 |
| 141 | 0x6A |
| 142 | 0x6A |
| 143 | 0x6B |
| 144 | 0x6B |
| 145 | 0x6B |
| 146 | 0x6C |
| 147 | 0x6C |
| 148 | 0x6D |
| 149 | 0x6D |
| 150 | 0x6E |
| 151 | 0x6E |
| 152 | 0x6F |
| 153 | 0x6F |
| 154 | 0x6F |
| 155 | 0x70 |
| 156 | 0x70 |
| 157 | 0x71 |
| 158 | 0x71 |
| 159 | 0x72 |
| 160 | 0x72 |
| 161 | 0x73 |
| 162 | 0x73 |
| 163 | 0x73 |
| 164 | 0x74 |
| 165 | 0x74 |
| 166 | 0x75 |
| 167 | 0x75 |
| 168 | 0x76 |
| 169 | 0x76 |
| 170 | 0x76 |
| 171 | 0x77 |
| 172 | 0x77 |
| 173 | 0x78 |
| 174 | 0x78 |
| 175 | 0x79 |
| 176 | 0x79 |
| 177 | 0x79 |
| 178 | 0x7A |
| 179 | 0x7A |
| 180 | 0x7B |
| 181 | 0x7B |
| 182 | 0x7B |
| 183 | 0x7C |
| 184 | 0x7C |
| 185 | 0x7D |
| 186 | 0x7D |
| 187 | 0x7D |
| 188 | 0x7E |
| 189 | 0x7E |
| 190 | 0x7F |
| 191 | 0x7F |
| 192 | 0x7F |
| 193 | 0x80 |
| 194 | 0x80 |
| 195 | 0x81 |
| 196 | 0x81 |
| 197 | 0x81 |
| 198 | 0x82 |
| 199 | 0x82 |
| 200 | 0x83 |
| 201 | 0x83 |
| 202 | 0x83 |
| 203 | 0x84 |
| 204 | 0x84 |
| 205 | 0x85 |
| 206 | 0x85 |
| 207 | 0x85 |
| 208 | 0x86 |
| 209 | 0x86 |
| 210 | 0x87 |
| 211 | 0x87 |
| 212 | 0x87 |
| 213 | 0x88 |
| 214 | 0x88 |
| 215 | 0x88 |
| 216 | 0x89 |
| 217 | 0x89 |
| 218 | 0x8A |
| 219 | 0x8A |
| 220 | 0x8A |
| 221 | 0x8B |
| 222 | 0x8B |
| 223 | 0x8B |
| 224 | 0x8C |
| 225 | 0x8C |
| 226 | 0x8D |
| 227 | 0x8D |
| 228 | 0x8D |
| 229 | 0x8E |
| 230 | 0x8E |
| 231 | 0x8E |
| 232 | 0x8F |
| 233 | 0x8F |
| 234 | 0x8F |
| 235 | 0x90 |
| 236 | 0x90 |
| 237 | 0x91 |
| 238 | 0x91 |
| 239 | 0x91 |
| 240 | 0x92 |
| 241 | 0x92 |
| 242 | 0x92 |
| 243 | 0x93 |
| 244 | 0x93 |
| 245 | 0x93 |
| 246 | 0x94 |
| 247 | 0x94 |
| 248 | 0x95 |
| 249 | 0x95 |
| 250 | 0x95 |
| 251 | 0x96 |
| 252 | 0x96 |
| 253 | 0x96 |
| 254 | 0x97 |
| 255 | 0x97 |
| 256 | 0x97 |
| 257 | 0x98 |
| 258 | 0x98 |
| 259 | 0x98 |
| 260 | 0x99 |
| 261 | 0x99 |
| 262 | 0x99 |
| 263 | 0x9A |
| 264 | 0x9A |
| 265 | 0x9A |
| 266 | 0x9B |
| 267 | 0x9B |
| 268 | 0x9B |
| 269 | 0x9C |
| 270 | 0x9C |
| 271 | 0x9C |
| 272 | 0x9D |
| 273 | 0x9D |
| 274 | 0x9D |
| 275 | 0x9E |
| 276 | 0x9E |
| 277 | 0x9E |
| 278 | 0x9F |
| 279 | 0x9F |
| 280 | 0x9F |
| 281 | 0xA0 |
| 282 | 0xA0 |
| 283 | 0xA0 |
| 284 | 0xA1 |
| 285 | 0xA1 |
| 286 | 0xA1 |
| 287 | 0xA2 |
| 288 | 0xA2 |
| 289 | 0xA2 |
| 290 | 0xA3 |
| 291 | 0xA3 |
| 292 | 0xA3 |
| 293 | 0xA4 |
| 294 | 0xA4 |
| 295 | 0xA4 |
| 296 | 0xA5 |
| 297 | 0xA5 |
| 298 | 0xA5 |
| 299 | 0xA6 |
| 300 | 0xA6 |
