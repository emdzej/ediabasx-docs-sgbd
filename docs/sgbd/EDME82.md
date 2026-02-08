# EDME82.prg

- Jobs: [93](#jobs)
- Tables: [58](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | eDME10 |
| ORIGIN | DELPHI DEG Cyril Ravenet |
| REVISION | 1.008 |
| AUTHOR | DELPHI DEG Cyril_Ravenet, DELPHI DEG Julien_Monnard |
| COMMENT | N/A |
| PACKAGE | 1.57 |
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
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus $04 requestIdentifiedShadowMemoryDTCAndStatus
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
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
- [_SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [STATUS_EWS](#job-status-ews) - KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC000 Zurücklesen verschiedener interner Stati für EWS
- [STATUS_EWS4_SK](#job-status-ews4-sk) - KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC002 Lesen des SecretKey des Server sowie Client für EWS4
- [STEUERN_EWS4_SK](#job-steuern-ews4-sk) - 17 "EWS4-data" schreiben KWP 2000: $2E WriteDataByCommonIdentifier CommonIdentifier=0xC001
- [_FREISCHALTCODE_SCHREIBEN_ALL](#job-freischaltcode-schreiben-all) - Mehrere Aktionen, FSC Laenge schreiben, FSC schreiben KWP 2000: $31 $1F $F2 / SetFSCLen KWP 2000: $31 $1F $F1 / FSCwrite KWP 2000: $31 $1F $EE / FSCcheck
- [STATUS_MONTAGEMODUS](#job-status-montagemodus) - 0x3343 STATUS_MONTAGEMODUS Auslesen Montage-Modus
- [STEUERN_ENDE_MONTAGEMODUS](#job-steuern-ende-montagemodus) - 0x3243 STEUERN_ENDE_MONTAGEMODUS Ende Montage-Modus
- [STEUERN_MONTAGEMODUS](#job-steuern-montagemodus) - 0x3143 STEUERN_MONTAGEMODUS Ansteuern Montage-Modus
- [STATUS_HVPM_DCDC_ALS](#job-status-hvpm-dcdc-als) - HVPM DCDC ALS EME_HVPM_DCDC_ALS (0xDE1C)
- [STATUS_HVPM_DCDC_ANSTEUERUNG](#job-status-hvpm-dcdc-ansteuerung) - DCDC Ansteuerung EME_HVPM_DCDC_ANSTEUERUNG (0xDE00)
- [STATUS_HVPM_ENERGIEBORDNETZ_2](#job-status-hvpm-energiebordnetz-2) - Anzahl Herstellung Fahrbereitschaft im SOC Bereich EME_HVPM_ENERGIEBORDNETZ_2 (0xDE04)
- [STATUS_HVPM_ENERGIEBORDNETZ](#job-status-hvpm-energiebordnetz) - HV Energie / Zellspannungen EME_HVPM_ENERGIEBORDNETZ (0xDE03)
- [STATUS_HVPM_PKOR](#job-status-hvpm-pkor) - HVPM Leistungskoordinator EME_HVPM_PKOR (0xDE06)
- [STATUS_KLE](#job-status-kle) - Infos zu Ladekabel und Phasenströme STATUS_KLE (0xDE97)
- [IDENT_IBS](#job-ident-ibs) - 0x224021 IDENT_IBS Identifikationsdaten fuer IBS-Sensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_BATTERIETAUSCH_REGISTRIEREN](#job-steuern-batterietausch-registrieren) - UDS $31 F8 Batterietausch registrieren
- [STATUS_LEMINFO_AEP](#job-status-leminfo-aep) - 0x224017 STATUS_LEMINFO_AEP Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen
- [STATUS_MESSWERTE_IBS](#job-status-messwerte-ibs) - 0x22402B STATUS_MESSWERTE_IBS Messwerte IBS auslesen
- [STATUS_VERBREDINFO](#job-status-verbredinfo) - 0x22401D STATUS_VERBREDINFO Verbraucherreduzierungsspeicher auslesen
- [STEUERN_DCDC_WANDLER_RESULT](#job-steuern-dcdc-wandler-result) - RIDI_DCDC - Steuern der HV-Spannung des DC/DC-Wandlers EME_DCDC_WANDLER (0xF1)
- [STEUERN_DCDC_WANDLER_START](#job-steuern-dcdc-wandler-start) - RIDI_DCDC - Steuern der HV-Spannung des DC/DC-Wandlers EME_DCDC_WANDLER (0xF1)
- [STEUERN_HVPM_INFOSPEICHER_PKOR_LOESCHEN](#job-steuern-hvpm-infospeicher-pkor-loeschen) - RIDI_HVPM_PKOR_CLR - Alle Infospeicher aus Job STATUS_HVPM_EKMV Null setzen EME_HVPM_INFOSPEICHER_PKOR_LOESCHEN (0xDE08)
- [STEUERN_HVPM_INFOSPEICHER_SPMON_LOESCHEN](#job-steuern-hvpm-infospeicher-spmon-loeschen) - RIDI_HVPM_SPMON_CLR - Löschen Infospeicher HVPM (SPMON) EME_HVPM_INFOSPEICHER_SPMON_LOESCHEN (0xDE0A)
- [STEUERN_HVPM_INFOSPEICHER_STRZLR_LOESCHEN](#job-steuern-hvpm-infospeicher-strzlr-loeschen) - RIDI_HVPM_STRZLR_CLR - Löschen Infospeicher HSPM (STRZL) EME_HVPM_INFOSPEICHER_STRZLR_LOESCHEN (0xDE09)
- [STEUERN_PM_HISTOGRAM_RESET](#job-steuern-pm-histogram-reset) - UDS $40 2B AEP Histogram Reset
- [STATUS_PEDALWERTGEBER](#job-status-pedalwertgeber) - Werte vom Pedalwertgeber PEDALWERTGEBER (0xDE9C)
- [STATUS_HVSTART_FEHLER](#job-status-hvstart-fehler) - Angabe des Fehlers beim Hochfahren des HV-Systems EME_HVSTART_FEHLER (0xDE26)
- [STEUERN_ELUE_RESULT](#job-steuern-elue-result) - Ansteuerung E-Lüfter ELUE (0xF7)
- [STEUERN_ELUE_START](#job-steuern-elue-start) - Ansteuerung E-Lüfter ELUE (0xF7)
- [STEUERN_ELUE_STOP](#job-steuern-elue-stop) - Ansteuerung E-Lüfter ELUE (0xF7)
- [STATUS_CONNECTED_DRIVE](#job-status-connected-drive) - Informationen über Connected Drive STATUS_CONNECTED_DRIVE (0xE0)
- [STATUS_HVPM_HV_SYSTEM_ON_OFF](#job-status-hvpm-hv-system-on-off) - Hochvoltsystem An / Aus EME_HVPM_HV_SYSTEM_ON_OFF (0xDE02)
- [STEUERN_EME_EWAP_RESULT](#job-steuern-eme-ewap-result) - Ansteuerung der LIN Wasserpumpe EME mit Vorgabe Drehzahl und Ansteuerzeit EME_EWAP (0xF6)
- [STEUERN_EME_EWAP_START](#job-steuern-eme-ewap-start) - Ansteuerung der LIN Wasserpumpe EME mit Vorgabe Drehzahl und Ansteuerzeit EME_EWAP (0xF6)
- [STEUERN_EME_EWAP_STOP](#job-steuern-eme-ewap-stop) - Ansteuerung der LIN Wasserpumpe EME mit Vorgabe Drehzahl und Ansteuerzeit EME_EWAP (0xF6)
- [STATUS_AE](#job-status-ae) - Info über AE: DCDC, ELUP, Temperaturen STATUS_AE (0xDE99)
- [STATUS_SME](#job-status-sme) - Temperatur, Spannungen,Strom, SOC der HV-Batterie STATUS_SME (0xDE98)
- [STEUERN_LADELEISTUNG_START](#job-steuern-ladeleistung-start) - STEUERN_LADELEISTUNG (0xC2)
- [STATUS_ELUP](#job-status-elup) - aktueller Zustand ELUP EME_ELUP (0xDE19)
- [STATUS_EME_ANSTEUERUNG_ELUP](#job-status-eme-ansteuerung-elup) - Aktueller Schaltzustand ELUP (0 = Aus, 1 = Ein) EME_ANSTEUERUNG_ELUP (0xDE0E)
- [STATUS_TSR_LADEN](#job-status-tsr-laden) - Alle Rückgabewerte bezüglich TSR Laden STATUS_TSR_LADEN (0xE4)
- [STATUS_SYSTEMCHECK_PM_INFO_1](#job-status-systemcheck-pm-info-1) - 0x224022 STATUS_SYSTEMCHECK_PM_INFO_1 Intelligenter Batteriesensor Bitfeld Pminfo1 lesen
- [STATUS_SYSTEMCHECK_PM_INFO_2](#job-status-systemcheck-pm-info-2) - 0x224023 STATUS_SYSTEMCHECK_PM_INFO_2 Intelligenter Batteriesensor Bitfeld Pminfo2 lesen
- [STATUS_TSR_PKOR](#job-status-tsr-pkor) - Status TSR Leistungskoordinator STATUS_TSR_PKOR (0xDEAC)
- [STATUS_ECOPRO](#job-status-ecopro) - STATUS_ECOPRO (0xDEB8)
- [STATUS_TSR_3_LESEN](#job-status-tsr-3-lesen) - Teleservice Daten 3 auslesen STATUS_TSR_3_LESEN (0xE3)
- [STATUS_BPAS_LESEN](#job-status-bpas-lesen) - Teleservice Daten bzgl. BPAS auslesen STATUS_TSR_3_LESEN (0xE6)
- [STATUS_SYSTEMCHECK_AEP_INFO_1](#job-status-systemcheck-aep-info-1) - 0x22DEBA STATUS_SYSTEMCHECK_AEP_INFO_1 Intelligenter Batteriesensor Bitfeld Pminfo1 lesen
- [STATUS_SYSTEMCHECK_AEP_INFO_2](#job-status-systemcheck-aep-info-2) - 0x22DEBB STATUS_SYSTEMCHECK_AEP_INFO_2 Intelligenter Batteriesensor Bitfeld Pminfo2 lesen
- [STEUERN_FLASHMODE_ACAN_RESULT](#job-steuern-flashmode-acan-result) - Flashmode ACAN (0xF5)
- [STEUERN_FLASHMODE_ACAN_START](#job-steuern-flashmode-acan-start) - Flashmode ACAN (0xF5)
- [STEUERN_FLASHMODE_ACAN_STOP](#job-steuern-flashmode-acan-stop) - Flashmode ACAN (0xF5)
- [STATUS_TSR_1_LESEN](#job-status-tsr-1-lesen) - Tele Service Daten auslesen STATUS_TSR_1_LESEN (0xE1)
- [STEUERN_START_LADEN_START](#job-steuern-start-laden-start) - Ladestart anfordern STEUERN_START_LADEN (0xC0)
- [STEUERN_STOP_LADEN_STOP](#job-steuern-stop-laden-stop) - Ladestop anfordern STEUERN_STOP_LADEN (0xC100)
- [STATUS_TSR_2_LESEN](#job-status-tsr-2-lesen) - Tele Service Daten auslesen STATUS_TSR_2_LESEN (0xE2)
- [STATUS_DEGRAD_DISP_LESEN](#job-status-degrad-disp-lesen) - Angezeigte Degradationen der letzten 10 Fahrzyklen DEGRAD_DISP_LESEN (0xDEC1)

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

<a id="job-is-lesen"></a>
### IS_LESEN

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus $04 requestIdentifiedShadowMemoryDTCAndStatus

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

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default

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

<a id="job-seriennummer-lesen"></a>
### _SERIENNUMMER_LESEN

Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SERIENNUMMER | string | Seriennummer des Steuergeraets |
| SERIENNUMMER_FSC | string | Seriennummer des Steuergeraets für Freischaltcodeeingabe in Hex-Form |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-status-ews"></a>
### STATUS_EWS

KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC000 Zurücklesen verschiedener interner Stati für EWS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS3_CAPABLE | int | 0 Das SG beherrscht kein EWS3 1 Das SG beherrscht EWS3 |
| STAT_EWS4_CAPABLE | int | 0 Das SG beherrscht kein EWS4 1 Das SG beherrscht EWS4 |
| STAT_EWS3_ACTIVE | int | 0 EWS3 ist nicht (mehr) aktiv 1 EWS3 ist aktiv (oder lässt sich aktivieren) |
| STAT_EWS4_ACTIVE | int | 0 EWS4 ist nicht aktiv 1 EWS4 ist aktiv |
| STAT_EWS4_SERVER_SK_LOCKED | int | 0 SecretKey server lässt sich noch schreiben 1 SecretKey server lässt sich nicht mehr schreiben/lesen |
| STAT_EWS4_CLIENT_SK_LOCKED | int | 0 SecretKey client lässt sich noch schreiben 1 SecretKey client lässt sich nicht mehr schreiben/lesen |
| STAT_CLIENT_AUTHENTICATED | int | 0 Freigabe (noch) nicht erteilt (noch nicht versucht oder Kommunikation gestört) 1 Freigabe erteilt (Challenge-Response erfolgreich) 2 Freigabe abgelehnt (Challenge-Response fehlgeschlagen, falsche Response, Kommunikation i.O.) 3 nicht definiert |
| STAT_CLIENT_AUTHENTICATED_TXT | string | Text zu Status Wert |
| STAT_DH_ACTIVE | int | 0 Diffie-Hellman-Abgleich nicht aktiv 1 Diffie-Hellman-Abgleich aktiv |
| STAT_E_LABEL_ACTIVE | int | 0 E-Label ist nicht aktiv 1 E-Label ist aktiv |
| STAT_FREE_SK0 | int | 0..0xFD Freie Flashablagen 0xFE    Freie Flashablage nicht begrenzt 0xFF    Fehlerkennzeichnung |
| _STAT_FREE_SK0_TXT | string | Freie Plaetze |
| STAT_FREE_SK1 | int | 0..0xFD Freie Flashablagen 0xFE    Freie Flashablage nicht begrenzt 0xFF    Fehlerkennzeichnung |
| _STAT_FREE_SK1_TXT | string | Freie Plaetze |
| STAT_VERSION | int | 0x01 Direktschreiben des SecretKey 0x02 Direktschreiben des SecretKey und DH-Abgleich |
| _STAT_VERSION_TXT | string | Version |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ews4-sk"></a>
### STATUS_EWS4_SK

KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC002 Lesen des SecretKey des Server sowie Client für EWS4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EWS4_SERVER_SK | binary | SecretKey Server |
| STAT_EWS4_CLIENT_SK | binary | SecretKey Client |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ews4-sk"></a>
### STEUERN_EWS4_SK

17 "EWS4-data" schreiben KWP 2000: $2E WriteDataByCommonIdentifier CommonIdentifier=0xC001

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | Byte0 LOCK_SERVER_SK LOCK_CLIENT_SK WRITE_SERVER_SK WRITE_CLIENT_SK UNLOCK_CLIENT_SK |
| DATA | string | Byte1...16 16 Byte Daten (SecretKey), falls MODE = WRITE_SERVER_SK/WRITE_CLIENT_SK, "0x01,0x02,.." KEINE Daten nötig, falls MODE = LOCK_SERVER_SK/LOCK_CLIENT_SK |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-freischaltcode-schreiben-all"></a>
### _FREISCHALTCODE_SCHREIBEN_ALL

Mehrere Aktionen, FSC Laenge schreiben, FSC schreiben KWP 2000: $31 $1F $F2 / SetFSCLen KWP 2000: $31 $1F $F1 / FSCwrite KWP 2000: $31 $1F $EE / FSCcheck

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATA | string | Daten werden in Hex-Form ohne vorangestelltes 0x, ohne Zwischenraum uebertragen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| JOB_STAT_CODE | string | 1 Byte Hex Format Eingangspunkt im table SwtFehler |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-montagemodus"></a>
### STATUS_MONTAGEMODUS

0x3343 STATUS_MONTAGEMODUS Auslesen Montage-Modus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_MONTAGEMODUS_TEXT | string | FUNKTIONSSTATUS MONTAGEMODUS 1BYTE FUNKTIONSSTATUS |
| STAT_FS_MONTAGEMODUS_WERT | int | FUNKTIONSSTATUS MONTAGEMODUS 1BYTE FUNKTIONSSTATUS |
| STAT_FS_MONTAGEMODUS_EINH | string | EINHEIT |
| STAT_ST_MONTAGE_MODUS_TEXT | string | Status Montage-Modus aktiv/inaktiv 1BYTE STATUS MONTAGE_MODUS |
| STAT_ST_MONTAGE_MODUS_WERT | int | Status Montage-Modus aktiv/inaktiv 1BYTE STATUS MONTAGE_MODUS |
| STAT_ST_MONTAGE_MODUS_EINH | string | EINHEIT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-montagemodus"></a>
### STEUERN_ENDE_MONTAGEMODUS

0x3243 STEUERN_ENDE_MONTAGEMODUS Ende Montage-Modus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-montagemodus"></a>
### STEUERN_MONTAGEMODUS

0x3143 STEUERN_MONTAGEMODUS Ansteuern Montage-Modus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hvpm-dcdc-als"></a>
### STATUS_HVPM_DCDC_ALS

HVPM DCDC ALS EME_HVPM_DCDC_ALS (0xDE1C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NV_DCDC_ALS_HIST_BEREICH_NULL_WERT | real | Zeit durchschnittlicher DCDC Strom im Buckmode LV-seitig in Bereich 0 |
| STAT_NV_DCDC_ALS_HIST_BEREICH_NULL_EINH | string | "s" |
| STAT_NV_DCDC_ALS_HIST_BEREICH_1_WERT | real | Zeit durchschnittlicher DCDC Strom im Buckmode LV-seitig in Bereich 1 |
| STAT_NV_DCDC_ALS_HIST_BEREICH_1_EINH | string | "s" |
| STAT_NV_DCDC_ALS_HIST_BEREICH_2_WERT | real | Zeit durchschnittlicher DCDC Strom im Buckmode LV-seitig in Bereich 2 |
| STAT_NV_DCDC_ALS_HIST_BEREICH_2_EINH | string | "s" |
| STAT_NV_DCDC_ALS_HIST_BEREICH_3_WERT | real | Zeit durchschnittlicher DCDC Strom im Buckmode LV-seitig in Bereich 3 |
| STAT_NV_DCDC_ALS_HIST_BEREICH_3_EINH | string | "s" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hvpm-dcdc-ansteuerung"></a>
### STATUS_HVPM_DCDC_ANSTEUERUNG

DCDC Ansteuerung EME_HVPM_DCDC_ANSTEUERUNG (0xDE00)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOC_HVB_WERT | real | Ladezustand HV Batterie |
| STAT_SOC_HVB_EINH | string | "%" |
| STAT_SOC_HVB_MIN_WERT | real | Startfähigkeitsgrenze Ladezustand HV Batterie |
| STAT_SOC_HVB_MIN_EINH | string | "%" |
| STAT_LADEGERAET | unsigned char | Ladegerät erkannt 1 / 0 |
| STAT_FREMDLADUNG | unsigned char | Fremdladung 1 / 0 |
| STAT_FAHRB | unsigned char | Fahrbereitschaft 1 / 0 |
| STAT_BA_DCDC_KOMM_WERT | unsigned char | Kommandierte Betriebsart: 0 = Anforderung Standby 1 = Anforderung Buck |
| STAT_BA_DCDC_KOMM_EINH | string | "" |
| STAT_I_DCDC_HV_OUT_WERT | real | Stromgrenze HV-Seite |
| STAT_I_DCDC_HV_OUT_EINH | string | "A" |
| STAT_U_DCDC_HV_OUT_WERT | real | Spannungsgrenze HV-Seite |
| STAT_U_DCDC_HV_OUT_EINH | string | "V" |
| STAT_I_DCDC_LV_OUT_WERT | real | Stromgrenze NV-Seite |
| STAT_I_DCDC_LV_OUT_EINH | string | "A" |
| STAT_U_DCDC_LV_OUT_WERT | real | Spannungsgrenze NV-Seite |
| STAT_U_DCDC_LV_OUT_EINH | string | "V" |
| STAT_BA_DCDC_IST_WERT | unsigned char | IST-Betriebsart DCDC-Wandler: 0 = Standby 1 = Buck |
| STAT_BA_DCDC_IST_EINH | string | "" |
| STAT_ALS_DCDC_WERT | real | Auslastung DC/DC-Wandler |
| STAT_ALS_DCDC_EINH | string | "%" |
| STAT_I_DCDC_HV_WERT | real | Strom HV-Seite |
| STAT_I_DCDC_HV_EINH | string | "A" |
| STAT_U_DCDC_HV_WERT | real | Spannung HV-Seite |
| STAT_U_DCDC_HV_EINH | string | "V" |
| STAT_I_DCDC_LV_WERT | real | Strom NV-Seite |
| STAT_I_DCDC_LV_EINH | string | "A" |
| STAT_U_DCDC_LV_WERT | real | Spannung NV-Seite |
| STAT_U_DCDC_LV_EINH | string | "V" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hvpm-energiebordnetz-2"></a>
### STATUS_HVPM_ENERGIEBORDNETZ_2

Anzahl Herstellung Fahrbereitschaft im SOC Bereich EME_HVPM_ENERGIEBORDNETZ_2 (0xDE04)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NV_HVB_SOC_FAHRB_0_20_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_0_20_EINH | string | "-" |
| STAT_NV_HVB_SOC_FAHRB_20_25_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_20_25_EINH | string | "-" |
| STAT_NV_HVB_SOC_FAHRB_25_30_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_25_30_EINH | string | "-" |
| STAT_NV_HVB_SOC_FAHRB_30_33_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_30_33_EINH | string | "-" |
| STAT_NV_HVB_SOC_FAHRB_33_36_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_33_36_EINH | string | "-" |
| STAT_NV_HVB_SOC_FAHRB_36_39_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_36_39_EINH | string | "-" |
| STAT_NV_HVB_SOC_FAHRB_39_42_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_39_42_EINH | string | "-" |
| STAT_NV_HVB_SOC_FAHRB_42_45_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_42_45_EINH | string | "-" |
| STAT_NV_HVB_SOC_FAHRB_45_48_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_45_48_EINH | string | "-" |
| STAT_NV_HVB_SOC_FAHRB_48_51_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_48_51_EINH | string | "-" |
| STAT_NV_HVB_SOC_FAHRB_51_56_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_51_56_EINH | string | "-" |
| STAT_NV_HVB_SOC_FAHRB_56_65_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_56_65_EINH | string | "-" |
| STAT_NV_HVB_SOC_FAHRB_65_80_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_65_80_EINH | string | "-" |
| STAT_NV_HVB_SOC_FAHRB_80_100_WERT | unsigned char | "" |
| STAT_NV_HVB_SOC_FAHRB_80_100_EINH | string | "-" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hvpm-energiebordnetz"></a>
### STATUS_HVPM_ENERGIEBORDNETZ

HV Energie / Zellspannungen EME_HVPM_ENERGIEBORDNETZ (0xDE03)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NV_MSA_DCDC_WERT | unsigned int | Zähler Ladungsmenge DC/DC MSA |
| STAT_NV_MSA_DCDC_EINH | string | "Ah" |
| STAT_NV_MSA_EKK_WERT | real | Zähler Ladungsmenge EKK MSA |
| STAT_NV_MSA_EKK_EINH | string | "Ah" |
| STAT_NV_ENTL_EKK_STD_WERT | real | Zähler Ladungsmenge EKK Standkühlung |
| STAT_NV_ENTL_EKK_STD_EINH | string | "Ah" |
| STAT_NV_ENTL_EKK15_WERT | real | Zähler Ladungsmenge EKK Kl15 |
| STAT_NV_ENTL_EKK15_EINH | string | "Ah" |
| STAT_NV_ENTL_DCDC15_WERT | real | Zähler Ladungsmenge DC/DC Kl15 |
| STAT_NV_ENTL_DCDC15_EINH | string | "Ah" |
| STAT_NV_ENTL_EM1_WERT | real | Zähler Ladungsmenge EM1 |
| STAT_NV_ENTL_EM1_EINH | string | "Ah" |
| STAT_NV_ENTL_EKK_WERT | real | Zähler Ladungsmenge EKK |
| STAT_NV_ENTL_EKK_EINH | string | "Ah" |
| STAT_NV_ENTL_DCDC_WERT | real | Zähler Ladungsmenge DC/DC |
| STAT_NV_ENTL_DCDC_EINH | string | "Ah" |
| STAT_NV_MSA_EM1_WERT | real | Zähler Ladungsmenge EM1 MSA |
| STAT_NV_MSA_EM1_EINH | string | "Ah" |
| STAT_NV_UHVB_SB_NULL_WERT | real | Zeit durchschnittliche Zellenspannung in SB0 |
| STAT_NV_UHVB_SB_NULL_EINH | string | "s" |
| STAT_NV_UHVB_SB_1_WERT | real | Zeit durchschnittliche Zellenspannung in SB1 |
| STAT_NV_UHVB_SB_1_EINH | string | "s" |
| STAT_NV_UHVB_SB_2_WERT | real | Zeit durchschnittliche Zellenspannung in SB2 |
| STAT_NV_UHVB_SB_2_EINH | string | "s" |
| STAT_NV_UHVB_SB_3_WERT | real | Zeit durchschnittliche Zellenspannung in SB3 |
| STAT_NV_UHVB_SB_3_EINH | string | "s" |
| STAT_NV_UHVB_SB_4_WERT | real | Zeit durchschnittliche Zellenspannung in SB4 |
| STAT_NV_UHVB_SB_4_EINH | string | "s" |
| STAT_NV_UHVB_SB_5_WERT | real | Zeit durchschnittliche Zellenspannung in SB5 |
| STAT_NV_UHVB_SB_5_EINH | string | "s" |
| STAT_NV_UHVB_SB_6_WERT | real | Zeit durchschnittliche Zellenspannung in SB6 |
| STAT_NV_UHVB_SB_6_EINH | string | "s" |
| STAT_NV_UHVB_SB_7_WERT | real | Zeit durchschnittliche Zellenspannung in SB7 |
| STAT_NV_UHVB_SB_7_EINH | string | "s" |
| STAT_NV_UHVB_SB_8_WERT | real | Zeit durchschnittliche Zellenspannung in SB8 |
| STAT_NV_UHVB_SB_8_EINH | string | "s" |
| STAT_NV_UHVB_SB_9_WERT | real | Zeit durchschnittliche Zellenspannung in SB9 |
| STAT_NV_UHVB_SB_9_EINH | string | "s" |
| STAT_NV_UHVB_SB_10_WERT | real | Zeit durchschnittliche Zellenspannung in SB10 |
| STAT_NV_UHVB_SB_10_EINH | string | "s" |
| STAT_NV_UHVB_SB_11_WERT | real | Zeit durchschnittliche Zellenspannung in SB11 |
| STAT_NV_UHVB_SB_11_EINH | string | "s" |
| STAT_NV_UHVB_SB_12_WERT | real | Zeit durchschnittliche Zellenspannung in SB12 |
| STAT_NV_UHVB_SB_12_EINH | string | "s" |
| STAT_NV_UHVB_SB_13_WERT | real | Zeit durchschnittliche Zellenspannung in SB13 |
| STAT_NV_UHVB_SB_13_EINH | string | "s" |
| STAT_NV_UHVB_SB_14_WERT | real | Zeit durchschnittliche Zellenspannung in SB14 |
| STAT_NV_UHVB_SB_14_EINH | string | "s" |
| STAT_NV_UHVB_SB_15_WERT | real | Zeit durchschnittliche Zellenspannung in SB15 |
| STAT_NV_UHVB_SB_15_EINH | string | "s" |
| STAT_NV_UHVB_SB_16_WERT | real | Zeit durchschnittliche Zellenspannung in SB16 |
| STAT_NV_UHVB_SB_16_EINH | string | "s" |
| STAT_NV_UHVB_SB_17_WERT | real | Zeit durchschnittliche Zellenspannung in SB17 |
| STAT_NV_UHVB_SB_17_EINH | string | "s" |
| STAT_NV_UHVB_SB_18_WERT | real | Zeit durchschnittliche Zellenspannung in SB18 |
| STAT_NV_UHVB_SB_18_EINH | string | "s" |
| STAT_NV_UHVB_SB_19_WERT | real | Zeit durchschnittliche Zellenspannung in SB19 |
| STAT_NV_UHVB_SB_19_EINH | string | "s" |
| STAT_NV_UHVB_SB_20_WERT | real | Zeit durchschnittliche Zellenspannung in SB20 |
| STAT_NV_UHVB_SB_20_EINH | string | "s" |
| STAT_NV_UHVB_SB_21_WERT | real | Zeit durchschnittliche Zellenspannung in SB21 |
| STAT_NV_UHVB_SB_21_EINH | string | "s" |
| STAT_NV_UHVB_SB_22_WERT | real | Zeit durchschnittliche Zellenspannung in SB22 |
| STAT_NV_UHVB_SB_22_EINH | string | "s" |
| STAT_NV_UHVB_SB_23_WERT | real | Zeit durchschnittliche Zellenspannung in SB23 |
| STAT_NV_UHVB_SB_23_EINH | string | "s" |
| STAT_NV_UHVB_SB_24_WERT | real | Zeit durchschnittliche Zellenspannung in SB24 |
| STAT_NV_UHVB_SB_24_EINH | string | "s" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hvpm-pkor"></a>
### STATUS_HVPM_PKOR

HVPM Leistungskoordinator EME_HVPM_PKOR (0xDE06)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NV_KM_DEG_EKMV_VM_AN_A_WERT | unsigned long | Kilometerstand bei Beginn der Reduzierung EKMV bei VM an. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_KM_DEG_EKMV_VM_AN_A_EINH | string | "km" |
| STAT_NV_T_DEG_EKMV_VM_AN_A_WERT | unsigned char | Gesamtdauer der Reduzierungen EKMV bei VM an. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_T_DEG_EKMV_VM_AN_A_EINH | string | "min" |
| STAT_NV_KM_DEG_BUCK_VM_AN_A_WERT | unsigned long | Kilometerstand bei beginn der Reduzierung Buckmode bei VM an. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_KM_DEG_BUCK_VM_AN_A_EINH | string | "km" |
| STAT_NV_T_DEG_BUCK_VM_AN_A_WERT | unsigned char | Gesamtdauer der Reduzierungen Buckmode bei VM an. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_T_DEG_BUCK_VM_AN_A_EINH | string | "min" |
| STAT_NV_KM_DEG_EKMV_VM_AUS_A_WERT | unsigned long | Kilometerstand bei beginn der Reduzierung EKMV bei VM aus. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_KM_DEG_EKMV_VM_AUS_A_EINH | string | "km" |
| STAT_NV_T_DEG_EKMV_VM_AUS_A_WERT | unsigned char | Gesamtdauer der Reduzierungen EKMV bei VM aus. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_T_DEG_EKMV_VM_AUS_A_EINH | string | "min" |
| STAT_NV_KM_DEG_BUCK_VM_AUS_A_WERT | unsigned long | Kilometerstand bei beginn der Reduzierung Buckmode bei VM aus. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_KM_DEG_BUCK_VM_AUS_A_EINH | string | "km" |
| STAT_NV_T_DEG_BUCK_VM_AUS_A_WERT | unsigned char | Gesamtdauer der Reduzierungen Buckmode bei VM aus. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_T_DEG_BUCK_VM_AUS_A_EINH | string | "min" |
| STAT_NV_KM_DEG_EKMV_VM_AN_B_WERT | unsigned long | Kilometerstand bei beginn der Reduzierung EKMV bei VM an. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_KM_DEG_EKMV_VM_AN_B_EINH | string | "km" |
| STAT_NV_T_DEG_EKMV_VM_AN_B_WERT | unsigned char | Gesamtdauer der Reduzierungen EKMV bei VM an. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_T_DEG_EKMV_VM_AN_B_EINH | string | "min" |
| STAT_NV_KM_DEG_BUCK_VM_AN_B_WERT | unsigned long | Kilometerstand bei beginn der Reduzierung Buckmode bei VM an. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_KM_DEG_BUCK_VM_AN_B_EINH | string | "km" |
| STAT_NV_T_DEG_BUCK_VM_AN_B_WERT | unsigned char | Gesamtdauer der Reduzierungen Buckmode bei VM an. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_T_DEG_BUCK_VM_AN_B_EINH | string | "min" |
| STAT_NV_KM_DEG_EKMV_VM_AUS_B_WERT | unsigned long | Kilometerstand bei beginn der Reduzierung EKMV bei VM aus. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_KM_DEG_EKMV_VM_AUS_B_EINH | string | "km" |
| STAT_NV_T_DEG_EKMV_VM_AUS_B_WERT | unsigned char | Gesamtdauer der Reduzierungen EKMV bei VM aus. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_T_DEG_EKMV_VM_AUS_B_EINH | string | "min" |
| STAT_NV_KM_DEG_BUCK_VM_AUS_B_WERT | unsigned long | Kilometerstand bei beginn der Reduzierung Buckmode bei VM aus. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_KM_DEG_BUCK_VM_AUS_B_EINH | string | "km" |
| STAT_NV_T_DEG_BUCK_VM_AUS_B_WERT | unsigned char | Gesamtdauer der Reduzierungen Buckmode bei VM aus. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_T_DEG_BUCK_VM_AUS_B_EINH | string | "min" |
| STAT_NV_KM_DEG_EM1_LL_A_WERT | unsigned long | Kilometerstand bei beginn der Reduzierung EM im Leerlauf. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_KM_DEG_EM1_LL_A_EINH | string | "km" |
| STAT_NV_T_DEG_EM1_LL_A_WERT | unsigned char | Gesamtdauer der Reduzierungen EM im Leerlauf Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_T_DEG_EM1_LL_A_EINH | string | "min" |
| STAT_NV_KM_DEG_EM1_LL_B_WERT | unsigned long | Kilometerstand bei beginn der Reduzierung EM im Leerlauf. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_KM_DEG_EM1_LL_B_EINH | string | "km" |
| STAT_NV_T_DEG_EM1_LL_B_WERT | unsigned char | Gesamtdauer der Reduzierungen EM nicht im Leerlauf. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_T_DEG_EM1_LL_B_EINH | string | "min" |
| STAT_NV_KM_DEG_EM1_NOTLL_A_WERT | unsigned long | Kilometerstand bei beginn der Reduzierung EM nicht im Leerlauf. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_KM_DEG_EM1_NOTLL_A_EINH | string | "km" |
| STAT_NV_T_DEG_EM1_NOTLL_A_WERT | unsigned char | Gesamtdauer der Reduzierungen EM nicht im Leerlauf. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_T_DEG_EM1_NOTLL_A_EINH | string | "min" |
| STAT_NV_KM_DEG_EM1_NOTLL_B_WERT | unsigned long | Kilometerstand bei beginn der Reduzierung EM nicht im Leerlauf. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_KM_DEG_EM1_NOTLL_B_EINH | string | "km" |
| STAT_NV_T_DEG_EM1_NOTLL_B_WERT | unsigned char | Gesamtdauer der Reduzierungen EM nicht im Leerlauf. Änderung nur bei Reduzierungen &gt; 1min. |
| STAT_NV_T_DEG_EM1_NOTLL_B_EINH | string | "min" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kle"></a>
### STATUS_KLE

Infos zu Ladekabel und Phasenströme STATUS_KLE (0xDE97)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LADEKABEL_ERKANNT | unsigned char | aktueller Zustand Ladekabel |
| STAT_LADEKABEL_ERKANNT_TEXT | string | aktueller Zustand Ladekabel |
| STAT_AC_LINE_VOLTAGE_1_WERT | unsigned char | Geglätteter und gefilterter AC-Spannungseffektiv-Istwert zwischen Leiter 1 und Nullleiter |
| STAT_AC_LINE_VOLTAGE_1_EINH | string | "V" |
| STAT_AC_LINE_VOLTAGE_2_WERT | unsigned char | Geglätteter und gefilterter AC-Spannungseffektiv-Istwert zwischen Leiter 2 und Nullleiter |
| STAT_AC_LINE_VOLTAGE_2_EINH | string | "V" |
| STAT_AC_LINE_VOLTAGE_3_WERT | unsigned char | Geglätteter und gefilterter AC-Spannungseffektiv-Istwert zwischen Leiter 3 und Nullleiter |
| STAT_AC_LINE_VOLTAGE_3_EINH | string | "V" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-batterietausch-registrieren"></a>
### STEUERN_BATTERIETAUSCH_REGISTRIEREN

UDS $31 F8 Batterietausch registrieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-leminfo-aep"></a>
### STATUS_LEMINFO_AEP

0x224017 STATUS_LEMINFO_AEP Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZR_USTAT_AEP_A_WERT | real | Haeufigkeitszaehler Zr_ustat_A 2BYTE in 0 bis 13107s   Einheit: s   Min: 0 Max: 13107 |
| STAT_ZR_USTAT_AEP_A_EINH | string | second |
| STAT_ZR_USTAT_AEP_B_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_B 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_B_EINH | string | second |
| STAT_ZR_USTAT_AEP_C_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_C 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_C_EINH | string | second |
| STAT_ZR_USTAT_AEP_D_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_D 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_D_EINH | string | second |
| STAT_ZR_USTAT_AEP_E_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_E 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_E_EINH | string | second |
| STAT_ZR_USTAT_AEP_F_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_F 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_F_EINH | string | second |
| STAT_ZR_USTAT_AEP_G_WERT | real | Haeufigkeitszaehler Zr_ustat_G 2BYTE in 0 bis 13107s   Einheit: s   Min: 0 Max: 13107 |
| STAT_ZR_USTAT_AEP_G_EINH | string | second |
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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-verbredinfo"></a>
### STATUS_VERBREDINFO

0x22401D STATUS_VERBREDINFO Verbraucherreduzierungsspeicher auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_E1_TAG | unsigned long | Ereignis 1 Tag (Verbredinfo[0]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_MONAT | unsigned long | Ereignis 1 Monat (Verbredinfo[1]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_DAUER_WERT | unsigned long | Ereignis 1 Dauer der Verbraucherreduzierung (Verbredinfo[2]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E1_DAUER_EINH | string | Minute |
| STAT_E1_LRSA | unsigned long | Ereignis 1 Leistungsreduktionstufe A (Verbredinfo[3]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_LRSB | unsigned long | Ereignis 1 Leistungsreduktionstufe B (Verbredinfo[4]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_WCFA | unsigned long | Ereignis 1 Worst Case Fahrerprofil A (Verbredinfo[5]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E1_WCFB | unsigned long | Ereignis 1 Worst Case Fahrerprofil B (Verbredinfo[6]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E2_TAG | unsigned long | Ereignis 2 Tag (Verbredinfo[7]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_MONAT | unsigned long | Ereignis 2 Monat (Verbredinfo[8]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_DAUER_WERT | unsigned long | Ereignis 2 Dauer der Verbraucherreduzierung (Verbredinfo[9]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E2_DAUER_EINH | string | Minute |
| STAT_E2_LRSA | unsigned long | Ereignis 2 Leistungsreduktionstufe A (Verbredinfo[10]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_LRSB | unsigned long | Ereignis 2 Leistungsreduktionstufe B (Verbredinfo[11]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_WCFA | unsigned long | Ereignis 2 Worst Case Fahrerprofil A (Verbredinfo[12]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E2_WCFB | unsigned long | Ereignis 2 Worst Case Fahrerprofil B (Verbredinfo[13]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E3_TAG | unsigned long | Ereignis 3 Tag (Verbredinfo[14]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_MONAT | unsigned long | Ereignis 3 Monat (Verbredinfo[15]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_DAUER_WERT | unsigned long | Ereignis 3 Dauer der Verbraucherreduzierung (Verbredinfo[16]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E3_DAUER_EINH | string | Minute |
| STAT_E3_LRSA | unsigned long | Ereignis 3 Leistungsreduktionstufe A (Verbredinfo[17]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_LRSB | unsigned long | Ereignis 3 Leistungsreduktionstufe B (Verbredinfo[18]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_WCFA | unsigned long | Ereignis 3 Worst Case Fahrerprofil A (Verbredinfo[19]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E3_WCFB | unsigned long | Ereignis 3 Worst Case Fahrerprofil B (Verbredinfo[20]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E4_TAG | unsigned long | Ereignis 4 Tag (Verbredinfo[21]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_MONAT | unsigned long | Ereignis 4 Monat (Verbredinfo[22]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_DAUER_WERT | unsigned long | Ereignis 4 Dauer der Verbraucherreduzierung (Verbredinfo[23]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E4_DAUER_EINH | string | Minute |
| STAT_E4_LRSA | unsigned long | Ereignis 4 Leistungsreduktionstufe A (Verbredinfo[24]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_LRSB | unsigned long | Ereignis 4 Leistungsreduktionstufe B (Verbredinfo[25]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_WCFA | unsigned long | Ereignis 4 Worst Case Fahrerprofil A (Verbredinfo[26]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_E4_WCFB | unsigned long | Ereignis 4 Worst Case Fahrerprofil B (Verbredinfo[27]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_ANZAHL_SCHLECHTE_LABI_GESAMT | unsigned long | Anzahl erkannter schlechter Ladebilanzen (Verbredinfo[28]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dcdc-wandler-result"></a>
### STEUERN_DCDC_WANDLER_RESULT

RIDI_DCDC - Steuern der HV-Spannung des DC/DC-Wandlers EME_DCDC_WANDLER (0xF1)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ST_DIAG_DCDC_MODUS | unsigned char | Rückmeldung Betriebsart DCDC |
| STAT_ST_DIAG_DCDC_MODUS_TEXT | string | Rückmeldung Betriebsart DCDC |
| STAT_ST_DIAG_DCDC_GRENZEN | unsigned char | Rückmeldung Grenzen |
| STAT_ST_DIAG_DCDC_GRENZEN_TEXT | string | Rückmeldung Grenzen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dcdc-wandler-start"></a>
### STEUERN_DCDC_WANDLER_START

RIDI_DCDC - Steuern der HV-Spannung des DC/DC-Wandlers EME_DCDC_WANDLER (0xF1)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ST_DIAG_DCDC_ANF | unsigned char | Anforderung Betriebsart DCDC |
| ST_B_DIAG_DCDC | unsigned char | Auswahl der Systemgrenze |
| SOC_DIAG_LAD_LMT | unsigned int | SOC HV Batterie Ladegrenze |
| I_DIAG_DCDC_LV_OUT | int | LV Stromgrenze Systemgrenze |
| I_DIAG_DCDC_HV_OUT | int | HV Stromgrenze Systemgrenze |
| U_DIAG_DCDC_LV_OUT | unsigned int | LV Spannung Systemgrenze |
| U_DIAG_DCDC_HV_OUT | unsigned int | HV Spannung Systemgrenze |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hvpm-infospeicher-pkor-loeschen"></a>
### STEUERN_HVPM_INFOSPEICHER_PKOR_LOESCHEN

RIDI_HVPM_PKOR_CLR - Alle Infospeicher aus Job STATUS_HVPM_EKMV Null setzen EME_HVPM_INFOSPEICHER_PKOR_LOESCHEN (0xDE08)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hvpm-infospeicher-spmon-loeschen"></a>
### STEUERN_HVPM_INFOSPEICHER_SPMON_LOESCHEN

RIDI_HVPM_SPMON_CLR - Löschen Infospeicher HVPM (SPMON) EME_HVPM_INFOSPEICHER_SPMON_LOESCHEN (0xDE0A)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hvpm-infospeicher-strzlr-loeschen"></a>
### STEUERN_HVPM_INFOSPEICHER_STRZLR_LOESCHEN

RIDI_HVPM_STRZLR_CLR - Löschen Infospeicher HSPM (STRZL) EME_HVPM_INFOSPEICHER_STRZLR_LOESCHEN (0xDE09)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pm-histogram-reset"></a>
### STEUERN_PM_HISTOGRAM_RESET

UDS $40 2B AEP Histogram Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pedalwertgeber"></a>
### STATUS_PEDALWERTGEBER

Werte vom Pedalwertgeber PEDALWERTGEBER (0xDE9C)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_PEDALWERT1_WERT | real | Spannung gemessen am Pedalwertgeber 1 |
| STAT_SPANNUNG_PEDALWERT1_EINH | string | "V" |
| STAT_SPANNUNG_PEDALWERT2_WERT | real | Spannung gemessen am Pedalwertgeber 2 |
| STAT_SPANNUNG_PEDALWERT2_EINH | string | "V" |
| STAT_PEDALWERT_WERT | real | aus Pedalwertgeber 1 und 2 ermittelter Pedalwert |
| STAT_PEDALWERT_EINH | string | "%" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hvstart-fehler"></a>
### STATUS_HVSTART_FEHLER

Angabe des Fehlers beim Hochfahren des HV-Systems EME_HVSTART_FEHLER (0xDE26)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BIT_0 | unsigned char | HV aus durch Diagnose Steuern-Job angefordert, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_1 | unsigned char | Flash-Modus, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_2 | unsigned char | Interlockfehler, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_3 | unsigned char | Kategorie 6 Batteriefehler, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_4 | unsigned char | HV aus durch Entladeschutzfunktion HEV angefordert, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_5 | unsigned char | Notaus, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_6 | unsigned char | schwerer Crash, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_7 | unsigned char | Crash, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_8 | unsigned char | Kategorie 7 Batteriefehler, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_9 | unsigned char | einfacher Schützkleber, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_10 | unsigned char | doppelter Schützkleber, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_11 | unsigned char | Schützkleber verhindert HV-batterielosen Betrieb, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_12 | unsigned char | Signale von SME ungültig oder ausgefallen, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_13 | unsigned char | Signale von LE ungültig oder ausgefallen, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_14 | unsigned char | HV aus durch Power Down, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_15 | unsigned char | HV aus Nachlaufzeit Klemme 30b abgelaufen, 1 = aktiv, 0 = inaktiv |
| STAT_BIT_16 | unsigned char | HV aus durch Entladeschutzfunktion BEV angefordert, 1 = aktiv, 0 = inaktiv |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-elue-result"></a>
### STEUERN_ELUE_RESULT

Ansteuerung E-Lüfter ELUE (0xF7)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ELUESOLL_AKTIV | unsigned char | aktueller Zustand des E-Lüfter ( 0 = aus, 1 = ein ) |
| STAT_ELUESOLL_WERT | real | aktuelle Drehzahl des E-Lüfters (in %) |
| STAT_ELUESOLL_EINH | string | "%" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-elue-start"></a>
### STEUERN_ELUE_START

Ansteuerung E-Lüfter ELUE (0xF7)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ELUESOLL_WERT | real | Vorgabe der Lüfterdrehzahl (0 - 99.6 %) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-elue-stop"></a>
### STEUERN_ELUE_STOP

Ansteuerung E-Lüfter ELUE (0xF7)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-connected-drive"></a>
### STATUS_CONNECTED_DRIVE

Informationen über Connected Drive STATUS_CONNECTED_DRIVE (0xE0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LADEN_NR | unsigned char | Bit0: kein Laden Bit1: Ladestecker gesteckt + kein Laden Bit2: Laden aktiv Bit3: Laden beendet Bit4: Ladestörung Bit5: Ladefehler |
| STAT_LADEN_NR_TEXT | string | Bit0: kein Laden Bit1: Ladestecker gesteckt + kein Laden Bit2: Laden aktiv Bit3: Laden beendet Bit4: Ladestörung Bit5: Ladefehler |
| STAT_REMOTE_LADEN_NR | unsigned char | Bit0: RemoteLaden nicht aktiv Bit1: RemoteLaden on Hold Bit2: RemoteLaden aktiv |
| STAT_REMOTE_LADEN_NR_TEXT | string | Bit0: RemoteLaden nicht aktiv Bit1: RemoteLaden on Hold Bit2: RemoteLaden aktiv |
| STAT_TIMER_LADEN_NR | unsigned char | Bit0: TimerLaden nicht aktiv Bit1: TimerLaden on Hold Bit2: TimerLaden aktiv |
| STAT_TIMER_LADEN_NR_TEXT | string | Bit0: TimerLaden nicht aktiv Bit1: TimerLaden on Hold Bit2: TimerLaden aktiv |
| STAT_HV_SOC_WERT | real | Anzeige Ladezustand HV-Batterie |
| STAT_HV_SOC_EINH | string | "%" |
| STAT_ZEIT_LADEENDE_WERT | unsigned int | Ladedauer |
| STAT_ZEIT_LADEENDE_EINH | string | "min" |
| STAT_MAX_LADESTROM_LADEGERAET_WERT | unsigned char | Maximaler AC-Ladestrom Ladegerät |
| STAT_MAX_LADESTROM_LADEGERAET_EINH | string | "A" |
| STAT_IST_AC_SPANNUNG_LADEGERAET_WERT | unsigned char | Ist-AC-Spannung Ladegerät |
| STAT_IST_AC_SPANNUNG_LADEGERAET_EINH | string | "V" |
| STAT_REICHWEITE_WERT | unsigned int | Reichweite |
| STAT_REICHWEITE_EINH | string | "km" |
| STAT_HVB_TEMP_WERT | real | Temperatur der HV-Batterie |
| STAT_HVB_TEMP_EINH | string | "°" |
| STAT_TRIGGER_SEGMENTSPEICHER_WERT | unsigned char | Auslösebedingung für das Lesen des Segmentspeichers |
| STAT_TRIGGER_SEGMENTSPEICHER_EINH | string | "" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-hvpm-hv-system-on-off"></a>
### STATUS_HVPM_HV_SYSTEM_ON_OFF

Hochvoltsystem An / Aus EME_HVPM_HV_SYSTEM_ON_OFF (0xDE02)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_U_DC_HV_LE_WERT | real | HV-Zwischenkreisspannung |
| STAT_U_DC_HV_LE_EINH | string | "V" |
| STAT_HV_READY | unsigned char | Freigabe HV |
| STAT_HDCAC_EREQ | unsigned char | Anforderung Schließen Schütze HV-Batterie |
| STAT_I0ANF_HVB | unsigned char | Status Nullstromanforderung |
| STAT_I0ANF_HVB_TEXT | string | Status Nullstromanforderung |
| STAT_ANF_ENTL_DCDC | unsigned char | Anforderung Entladung HV-Zwischenkreis durch DCDC-Wandler |
| STAT_HVSTART_KOMM | unsigned char | Ausgabe des Stateflow-Status des HVPM Startsystems |
| STAT_HVSTART_KOMM_TEXT | string | Ausgabe des Stateflow-Status des HVPM Startsystems |
| STAT_ANF_ENTL_EME | unsigned char | Anforderung Notentladung ZK: 0 = nicht aktiv 1 = aktiv |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eme-ewap-result"></a>
### STEUERN_EME_EWAP_RESULT

Ansteuerung der LIN Wasserpumpe EME mit Vorgabe Drehzahl und Ansteuerzeit EME_EWAP (0xF6)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANSTEUERUNG_ERFOLGREICH_EIN | unsigned char | Ansteuerung der LIN Wasserpumpe EME (0 - Job inaktiv 1 - Job aktiv) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eme-ewap-start"></a>
### STEUERN_EME_EWAP_START

Ansteuerung der LIN Wasserpumpe EME mit Vorgabe Drehzahl und Ansteuerzeit EME_EWAP (0xF6)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DREHZAHL_WERT | unsigned char | geforderte Drehzahl (0-100%) nur möglich, falls Temperatur des Jobs job STATUS_TEMP_EMASCHINE zwischen 15 und 45 °C |
| ZEIT_ANSTEUERUNG_WERT | unsigned int | geforderte Ansteuerzeit (0-500s) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eme-ewap-stop"></a>
### STEUERN_EME_EWAP_STOP

Ansteuerung der LIN Wasserpumpe EME mit Vorgabe Drehzahl und Ansteuerzeit EME_EWAP (0xF6)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ae"></a>
### STATUS_AE

Info über AE: DCDC, ELUP, Temperaturen STATUS_AE (0xDE99)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BETRIEBSART_DCDC_IST | unsigned char | Aktuelle Betriebsart des DC/DC-Wandlers |
| STAT_BETRIEBSART_DCDC_IST_TEXT | string | Aktuelle Betriebsart des DC/DC-Wandlers |
| STAT_DREHZAHL_WERT | real | Ist-Drehzahl Traktions-EM |
| STAT_DREHZAHL_EINH | string | "1/min" |
| STAT_SPANNUNG_ELUP_WERT | real | Aktuelle Spannung, die an der ELUP anliegt |
| STAT_SPANNUNG_ELUP_EINH | string | "V" |
| STAT_STROM_SYSTEM_LEG_WERT | real | Aktueller HV-DC Strom der Leistungselektronik derTraktions- EM |
| STAT_STROM_SYSTEM_LEG_EINH | string | "A" |
| STAT_AC_LINE_POWER_WERT | unsigned int | Von der SLE aus dem EVU-Netz entnommene AC-Wirkleistung |
| STAT_AC_LINE_POWER_EINH | string | "W" |
| STAT_TEMPERATUR_DCDC_WANDLER_WERT | long | Bauteiltemperatur des Gleichspannnungswandlers |
| STAT_TEMPERATUR_DCDC_WANDLER_EINH | string | "°C" |
| STAT_TEMPERATUR_EMOTOR_WERT | long | Bauteiltemperatur der ersten E-Maschine |
| STAT_TEMPERATUR_EMOTOR_EINH | string | "°C" |
| STAT_TEMPERATUR_LADEELEKTRONIK_WERT | long | Aktuelle Temperatur der Ladeelektronik |
| STAT_TEMPERATUR_LADEELEKTRONIK_EINH | string | "°C" |
| STAT_TEMPERATUR_LEISTUNGSENDSTUFE_WERT | long | Bauteiltemperatur des Leistungsteils der Elektromotorelektronik |
| STAT_TEMPERATUR_LEISTUNGSENDSTUFE_EINH | string | "°C" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sme"></a>
### STATUS_SME

Temperatur, Spannungen,Strom, SOC der HV-Batterie STATUS_SME (0xDE98)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIETEMP_MIN_WERT | long | Niedrigste Temperatur in der HV-Batterie |
| STAT_BATTERIETEMP_MIN_EINH | string | "°C" |
| STAT_BATTERIETEMP_MAX_WERT | long | Höchste Temperatur in der HV-Batterie |
| STAT_BATTERIETEMP_MAX_EINH | string | "°C" |
| STAT_BATTERIETEMP_WERT | long | Höchste Temperatur in der HV-Batterie |
| STAT_BATTERIETEMP_EINH | string | "°C" |
| STAT_SPANNUNG_HV_BATTERIE_WERT | real | Aktuell gemessene HV-Batterie-Spannung |
| STAT_SPANNUNG_HV_BATTERIE_EINH | string | "V" |
| STAT_STROM_HV_BATTERIE_WERT | real | Aktuell gemessener Strom. Der Ladestrom ist generell mit positivem Vorzeichen definiert. |
| STAT_STROM_HV_BATTERIE_EINH | string | "A" |
| STAT_BATTERIESPANNUNG_MIN_WERT | real | Spannungsgrenze bei Entladung. Die minimal erlaubte Entladespannung |
| STAT_BATTERIESPANNUNG_MIN_EINH | string | "V" |
| STAT_BATTERIESPANNUNG_MAX_WERT | real | Spannungsgrenze bei Ladung, die maximal erlaubte Ladespannung |
| STAT_BATTERIESPANNUNG_MAX_EINH | string | "V" |
| STAT_SOC_GESPEICHERT_WERT | real | Letzer gültig empfangener Ladezustand des HV Speichers bezogen auf die Ist-Kapazität |
| STAT_SOC_GESPEICHERT_EINH | string | "%" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ladeleistung-start"></a>
### STEUERN_LADELEISTUNG_START

STEUERN_LADELEISTUNG (0xC2)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MAX_LADELEISTUNG | unsigned long | Vorgabe maximaler Ladeleistung an eDME |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-elup"></a>
### STATUS_ELUP

aktueller Zustand ELUP EME_ELUP (0xDE19)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZAHL_BREMSBTG_WERT | unsigned long | Anzahl Bremsbetätigungen |
| STAT_ANZAHL_BREMSBTG_EINH | string | "-" |
| STAT_LAUFZEIT_ELUP_S_WERT | unsigned long | Laufzeit Elup |
| STAT_LAUFZEIT_ELUP_S_EINH | string | "s" |
| STAT_ANLAUFE_ELUP_WERT | unsigned long | Anzahl Anläufe Elup |
| STAT_ANLAUFE_ELUP_EINH | string | "-" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eme-ansteuerung-elup"></a>
### STATUS_EME_ANSTEUERUNG_ELUP

Aktueller Schaltzustand ELUP (0 = Aus, 1 = Ein) EME_ANSTEUERUNG_ELUP (0xDE0E)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANST_ELUP_ON | unsigned char | Aktueller Schaltzustand ELUP (0 - Aus 1 - Ein) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tsr-laden"></a>
### STATUS_TSR_LADEN

Alle Rückgabewerte bezüglich TSR Laden STATUS_TSR_LADEN (0xE4)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZ_LADEVORGAENGE_GESAMT_WERT | unsigned char | Anzahl Ladevorgänge seit letztem TSR |
| STAT_ANZ_LADEVORGAENGE_GESAMT_EINH | string | "-" |
| STAT_ANZ_LADEVORGAENGE_REG_WERT | unsigned char | Anzahl Ladevorgänge seit letztem TSR größer eine Minute |
| STAT_ANZ_LADEVORGAENGE_REG_EINH | string | "-" |
| STAT_TIME_LADEBEGINN_HR_WERT | unsigned char | Uhrzeit bei Ladebeginn (Kombi) Stunde |
| STAT_TIME_LADEBEGINN_HR_EINH | string | "h" |
| STAT_TIME_LADEBEGINN_MIN_WERT | unsigned char | Uhrzeit bei Ladebeginn (Kombi) Minute |
| STAT_TIME_LADEBEGINN_MIN_EINH | string | "min" |
| STAT_KM_STAND_LADEBEGINN_WERT | unsigned long | km-Stand bei Ladebeginn |
| STAT_KM_STAND_LADEBEGINN_EINH | string | "km" |
| STAT_DELTA_RANGE_WERT | unsigned char | Differenz Reichweitenprognose zu letztem Ladeende und aktuellem Ladebeginn |
| STAT_DELTA_RANGE_EINH | string | "km" |
| STAT_DELTA_KM_STAND_WERT | unsigned char | Differenz km-Stand seit letztem Ladeende und aktuellem Ladebeginn |
| STAT_DELTA_KM_STAND_EINH | string | "km" |
| STAT_DELTA_SOC_WERT | real | SoC-Hub zwischen letztem Ladevorgang und aktuellem Ladebeginn |
| STAT_DELTA_SOC_EINH | string | "%" |
| STAT_SOC_LADEBEGINN_WERT | real | HV-SoC bei Ladebeginn |
| STAT_SOC_LADEBEGINN_EINH | string | "%" |
| STAT_SOC_LADEENDE_WERT | real | HV-SoC bei Ladeende |
| STAT_SOC_LADEENDE_EINH | string | "%" |
| STAT_ABBRUCHBED_LADEN | unsigned char | Start- und Abbruchbedingung Laden |
| STAT_ART_LADEANF_BIT_0 | unsigned char | 1 = Ladeanforderung HVB, 0 = keine Ladeanforderung HVB |
| STAT_ART_LADEANF_BIT_0_TEXT | string | 1 = Ladeanforderung HVB, 0 = keine Ladeanforderung HVB |
| STAT_ART_LADEANF_BIT_1 | unsigned char | 1 = Vorkonditionierung, 0 = keine Vorkonditionierung |
| STAT_ART_LADEANF_BIT_1_TEXT | string | 1 = Vorkonditionierung, 0 = keine Vorkonditionierung |
| STAT_ART_LADEANF_BIT_2 | unsigned char | 1 = Nachladeanforderung NVB, 0 = keine Nachladeanforderung NVB |
| STAT_ART_LADEANF_BIT_2_TEXT | string | 1 = Nachladeanforderung NVB, 0 = keine Nachladeanforderung NVB |
| STAT_BEDINGUNG_LADESTART | unsigned char | Startbedingung des aktuellen Ladevorganges |
| STAT_BEDINGUNG_LADESTART_TEXT | string | Startbedingung des aktuellen Ladevorganges |
| STAT_ABBRUCHBEDINGUNG | unsigned char | Zustand, der zum Ende des Ladevorgangs führte |
| STAT_ABBRUCHBEDINGUNG_TEXT | string | Zustand, der zum Ende des Ladevorgangs führte |
| STAT_LADEDAUER_GESAMT_WERT | unsigned int | Dauer Ladevorgang gesamt |
| STAT_LADEDAUER_GESAMT_EINH | string | "s" |
| STAT_LADEDAUER_EFFEKTIV_WERT | unsigned int | Dauer Ladevorgang ohne Ladeunterbrechungen |
| STAT_LADEDAUER_EFFEKTIV_EINH | string | "s" |
| STAT_ANZ_LADEUNTERBR_WERT | unsigned char | Anzahl Ladeunterbrechungen |
| STAT_ANZ_LADEUNTERBR_EINH | string | "-" |
| STAT_REAS_LDUNTERBR | unsigned int | Ursache für die letzten 4 Ladeunterbrechungen |
| STAT_REAS_LDUNTERBR__0 | unsigned int | Ursache für die letzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR__0_TEXT | string | Ursache für die letzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR__1 | unsigned int | Ursache für die zweitletzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR__1_TEXT | string | Ursache für die zweitletzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR__2 | unsigned int | Ursache für die drittletzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR__2_TEXT | string | Ursache für die drittletzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR__3 | unsigned int | Ursache für die viertletzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR__3_TEXT | string | Ursache für die viertletzte Ladeunterbrechung |
| STAT_PROGNOSE_LADEDAUER_WERT | real | Prognostizierte Ladedauer zu Ladebeginn |
| STAT_PROGNOSE_LADEDAUER_EINH | string | "min" |
| STAT_DAUER_DER_WERT | unsigned int | Dauer des Deratings |
| STAT_DAUER_DER_EINH | string | "s" |
| STAT_MIN_VALUE_DER_WERT | unsigned int | Minimal auftretender Wert während Derating |
| STAT_MIN_VALUE_DER_EINH | string | "W" |
| STAT_DERATING_PROZENTUAL_WERT | unsigned char | Mittlerer Wert des Deratings |
| STAT_DERATING_PROZENTUAL_EINH | string | "%" |
| STAT_I_LIM_GRID_WERT | unsigned char | Netzseitige Stromgrenze |
| STAT_I_LIM_GRID_EINH | string | "%" |
| STAT_T_AMB_LADEBEGINN_WERT | real | Umgebungstemperatur Ladebeginn |
| STAT_T_AMB_LADEBEGINN_EINH | string | "°C" |
| STAT_T_AMB_LADEENDE_WERT | real | Umgebungstemperatur Ladeende |
| STAT_T_AMB_LADEENDE_EINH | string | "°C" |
| STAT_T_HVB_LADEBEGINN_WERT | real | Temperatur HV-Batterie |
| STAT_T_HVB_LADEBEGINN_EINH | string | "°C" |
| STAT_T_HVB_LADEENDE_WERT | real | Temperatur HV-Batterie Ladeende |
| STAT_T_HVB_LADEENDE_EINH | string | "°C" |
| STAT_U_GRID_MIN_WERT | unsigned char | Minimale Netzspannung |
| STAT_U_GRID_MIN_EINH | string | "V" |
| STAT_U_GRID_MAX_WERT | unsigned char | Maximale Netzspannung |
| STAT_U_GRID_MAX_EINH | string | "V" |
| STAT_HIST_P_KLE_0_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall 0-1 kW |
| STAT_HIST_P_KLE_0_EINH | string | "s" |
| STAT_HIST_P_KLE_1_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall 1-2 kW |
| STAT_HIST_P_KLE_1_EINH | string | "s" |
| STAT_HIST_P_KLE_2_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall 2-3 kW |
| STAT_HIST_P_KLE_2_EINH | string | "s" |
| STAT_HIST_P_KLE_3_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall 3-4 kW |
| STAT_HIST_P_KLE_3_EINH | string | "s" |
| STAT_HIST_P_KLE_4_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall 4-5 kW |
| STAT_HIST_P_KLE_4_EINH | string | "s" |
| STAT_HIST_P_KLE_5_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall 5-6 kW |
| STAT_HIST_P_KLE_5_EINH | string | "s" |
| STAT_HIST_P_KLE_6_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall &gt; 6 kW |
| STAT_HIST_P_KLE_6_EINH | string | "s" |
| STAT_ENERGIE_KLE_WERT | unsigned long | Energieverbrauch KLE |
| STAT_ENERGIE_KLE_EINH | string | "Wh" |
| STAT_HIST_P_EKMV_EDH_0_WERT | unsigned int | Dauer des Leistungsbedarfs von EKMV und EDH im Intervall 0-1 kW |
| STAT_HIST_P_EKMV_EDH_0_EINH | string | "s" |
| STAT_HIST_P_EKMV_EDH_1_WERT | unsigned int | Dauer des Leistungsbedarfs von EKMV und EDH im Intervall 1-2 kW |
| STAT_HIST_P_EKMV_EDH_1_EINH | string | "s" |
| STAT_HIST_P_EKMV_EDH_2_WERT | unsigned int | Dauer des Leistungsbedarfs von EKMV und EDH im Intervall 2-3 kW |
| STAT_HIST_P_EKMV_EDH_2_EINH | string | "s" |
| STAT_HIST_P_EKMV_EDH_3_WERT | unsigned int | Dauer des Leistungsbedarfs von EKMV und EDH im Intervall 3-4 kW |
| STAT_HIST_P_EKMV_EDH_3_EINH | string | "s" |
| STAT_HIST_P_EKMV_EDH_4_WERT | unsigned int | Dauer des Leistungsbedarfs von EKMV und EDH im Intervall 4-5 kW |
| STAT_HIST_P_EKMV_EDH_4_EINH | string | "s" |
| STAT_HIST_P_EKMV_EDH_5_WERT | unsigned int | Dauer des Leistungsbedarfs von EKMV und EDH im Intervall &gt; 5 kW |
| STAT_HIST_P_EKMV_EDH_5_EINH | string | "s" |
| STAT_ENERGIE_EDH_EKMV_WERT | unsigned long | Energieverbrauch EDH und EKMV |
| STAT_ENERGIE_EDH_EKMV_EINH | string | "Wh" |
| STAT_ANF_ART_VOKO | unsigned char | Bit0: Voko Innenraum Bit1: Voko Innenraum forced Bit2: Voko Batt Bit3: Voko Batt forced |
| STAT_ANF_ART_VOKO_BIT_0 | unsigned char | 1 = Voko Innenraum, 0 = keine Voko Innenraum |
| STAT_ANF_ART_VOKO_BIT_0_TEXT | string | 1 = Voko Innenraum, 0 = keine Voko Innenraum |
| STAT_ANF_ART_VOKO_BIT_1 | unsigned char | 1 = Voko Innenraum forced, 0 = keine Voko Innenraum forced |
| STAT_ANF_ART_VOKO_BIT_1_TEXT | string | 1 = Voko Innenraum forced, 0 = keine Voko Innenraum forced |
| STAT_ANF_ART_VOKO_BIT_2 | unsigned char | 1 = Voko Batt, 0 = keine Voko Batt |
| STAT_ANF_ART_VOKO_BIT_2_TEXT | string | 1 = Voko Batt, 0 = keine Voko Batt |
| STAT_ANF_ART_VOKO_BIT_3 | unsigned char | 1 = Voko Batt forced, 0 = keine Voko Batt forced |
| STAT_ANF_ART_VOKO_BIT_3_TEXT | string | 1 = Voko Batt forced, 0 = keine Voko Batt forced |
| STAT_HIST_P_HVB_0_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB &lt; -4 kW |
| STAT_HIST_P_HVB_0_EINH | string | "s" |
| STAT_HIST_P_HVB_1_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB -4 kW bis -3 kW |
| STAT_HIST_P_HVB_1_EINH | string | "s" |
| STAT_HIST_P_HVB_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB -3 kW bis -2 kW |
| STAT_HIST_P_HVB_2_EINH | string | "s" |
| STAT_HIST_P_HVB_3_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB -2 kW bis -1 kW |
| STAT_HIST_P_HVB_3_EINH | string | "s" |
| STAT_HIST_P_HVB_4_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB -1 kW bis 0 kW |
| STAT_HIST_P_HVB_4_EINH | string | "s" |
| STAT_HIST_P_HVB_5_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 0 kW bis 1 kW |
| STAT_HIST_P_HVB_5_EINH | string | "s" |
| STAT_HIST_P_HVB_6_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 1 kW bis 2 kW |
| STAT_HIST_P_HVB_6_EINH | string | "s" |
| STAT_HIST_P_HVB_7_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 2 kW bis 3 kW |
| STAT_HIST_P_HVB_7_EINH | string | "s" |
| STAT_HIST_P_HVB_8_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 3 kW bis 4 kW |
| STAT_HIST_P_HVB_8_EINH | string | "s" |
| STAT_HIST_P_HVB_9_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 4 kW bis 5 kW |
| STAT_HIST_P_HVB_9_EINH | string | "s" |
| STAT_HIST_P_HVB_10_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 5 kW bis 6 kW |
| STAT_HIST_P_HVB_10_EINH | string | "s" |
| STAT_HIST_P_HVB_11_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 6 kW bis 7 kW |
| STAT_HIST_P_HVB_11_EINH | string | "s" |
| STAT_HIST_P_HVB_12_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB &gt; 7 kW |
| STAT_HIST_P_HVB_12_EINH | string | "s" |
| STAT_ENERGIE_HVB_WERT | unsigned long | Energieverbrauch HVB |
| STAT_ENERGIE_HVB_EINH | string | "Wh" |
| STAT_P_AVG_DCDC_HV_WERT | unsigned int | Durchschnittliche Leistung DCDC-Wandler HV-seitig |
| STAT_P_AVG_DCDC_HV_EINH | string | "W" |
| STAT_DAUER_SPANNUNGSGRENZE_WERT | unsigned int | Dauer in Spannungsbegrenzung während Ladevorgang |
| STAT_DAUER_SPANNUNGSGRENZE_EINH | string | "s" |
| STAT_SOC_SPANNUNGSGRENZE_WERT | real | SoC bei der Spannungsgrenze erreicht wird |
| STAT_SOC_SPANNUNGSGRENZE_EINH | string | "%" |
| STAT_TIME_LADEBEGINN_HR_2_WERT | unsigned char | Uhrzeit bei Ladebeginn (Kombi) Stunde 2 |
| STAT_TIME_LADEBEGINN_HR_2_EINH | string | "h" |
| STAT_TIME_LADEBEGINN_MIN_2_WERT | unsigned char | Uhrzeit bei Ladebeginn (Kombi) Minute 2 |
| STAT_TIME_LADEBEGINN_MIN_2_EINH | string | "min" |
| STAT_KM_STAND_LADEBEGINN_2_WERT | unsigned long | km-Stand bei Ladebeginn 2 |
| STAT_KM_STAND_LADEBEGINN_2_EINH | string | "km" |
| STAT_DELTA_RANGE_2_WERT | unsigned char | Differenz Reichweitenprognose zu letztem Ladeende und aktuellem Ladebeginn 2 |
| STAT_DELTA_RANGE_2_EINH | string | "km" |
| STAT_DELTA_KM_STAND_2_WERT | unsigned char | Differenz km-Stand seit letztem Ladeende und aktuellem Ladebeginn 2 |
| STAT_DELTA_KM_STAND_2_EINH | string | "km" |
| STAT_DELTA_SOC_2_WERT | real | SoC-Hub zwischen letztem Ladevorgang und aktuellem Ladebeginn 2 |
| STAT_DELTA_SOC_2_EINH | string | "%" |
| STAT_SOC_LADEBEGINN_2_WERT | real | HV-SoC bei Ladebeginn 2 |
| STAT_SOC_LADEBEGINN_2_EINH | string | "%" |
| STAT_SOC_LADEENDE_2_WERT | real | HV-SoC bei Ladeende 2 |
| STAT_SOC_LADEENDE_2_EINH | string | "%" |
| STAT_ABBRUCHBED_LADEN_2 | unsigned char | Start- und Abbruchbedingung Laden 2 |
| STAT_ART_LADEANF_2_BIT_0 | unsigned char | 1 = Ladeanforderung HVB, 0 = keine Ladeanforderung HVB |
| STAT_ART_LADEANF_2_BIT_0_TEXT | string | 1 = Ladeanforderung HVB, 0 = keine Ladeanforderung HVB |
| STAT_ART_LADEANF_2_BIT_1 | unsigned char | 1 = Vorkonditionierung, 0 = keine Vorkonditionierung |
| STAT_ART_LADEANF_2_BIT_1_TEXT | string | 1 = Vorkonditionierung, 0 = keine Vorkonditionierung |
| STAT_ART_LADEANF_2_BIT_2 | unsigned char | 1 = Nachladeanforderung NVB, 0 = keine Nachladeanforderung NVB |
| STAT_ART_LADEANF_2_BIT_2_TEXT | string | 1 = Nachladeanforderung NVB, 0 = keine Nachladeanforderung NVB |
| STAT_BEDINGUNG_LADESTART_2 | unsigned char | Startbedingung des aktuellen Ladevorganges |
| STAT_BEDINGUNG_LADESTART_2_TEXT | string | Startbedingung des aktuellen Ladevorganges |
| STAT_ABBRUCHBEDINGUNG_2 | unsigned char | Zustand, der zum Ende des Ladevorgangs führte |
| STAT_ABBRUCHBEDINGUNG_2_TEXT | string | Zustand, der zum Ende des Ladevorgangs führte |
| STAT_LADEDAUER_GESAMT_2_WERT | unsigned int | Dauer Ladevorgang gesamt 2 |
| STAT_LADEDAUER_GESAMT_2_EINH | string | "s" |
| STAT_LADEDAUER_EFFEKTIV_2_WERT | unsigned int | Dauer Ladevorgang ohne Ladeunterbrechungen 2 |
| STAT_LADEDAUER_EFFEKTIV_2_EINH | string | "s" |
| STAT_ANZ_LADEUNTERBR_2_WERT | unsigned char | Anzahl Ladeunterbrechungen 2 |
| STAT_ANZ_LADEUNTERBR_2_EINH | string | "-" |
| STAT_REAS_LDUNTERBR_2 | unsigned int | Ursache für die letzten 4 Ladeunterbrechungen 2 |
| STAT_REAS_LDUNTERBR_2__0 | unsigned int | Ursache für die letzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR_2__0_TEXT | string | Ursache für die letzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR_2__1 | unsigned int | Ursache für die zweitletzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR_2__1_TEXT | string | Ursache für die zweitletzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR_2__2 | unsigned int | Ursache für die drittletzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR_2__2_TEXT | string | Ursache für die drittletzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR_2__3 | unsigned int | Ursache für die viertletzte Ladeunterbrechung |
| STAT_REAS_LDUNTERBR_2__3_TEXT | string | Ursache für die viertletzte Ladeunterbrechung |
| STAT_PROGNOSE_LADEDAUER_2_WERT | real | Prognostizierte Ladedauer zu Ladebeginn 2 |
| STAT_PROGNOSE_LADEDAUER_2_EINH | string | "min" |
| STAT_DAUER_DER_2_WERT | unsigned int | Dauer des Deratings 2 |
| STAT_DAUER_DER_2_EINH | string | "s" |
| STAT_MIN_VALUE_DER_2_WERT | unsigned int | Minimal auftretender Wert während Derating 2 |
| STAT_MIN_VALUE_DER_2_EINH | string | "W" |
| STAT_DERATING_PROZENTUAL_2_WERT | unsigned char | Mittlerer Wert des Deratings 2 |
| STAT_DERATING_PROZENTUAL_2_EINH | string | "%" |
| STAT_I_LIM_GRID_2_WERT | unsigned char | Netzseitige Stromgrenze 2 |
| STAT_I_LIM_GRID_2_EINH | string | "%" |
| STAT_T_AMB_LADEBEGINN_2_WERT | real | Umgebungstemperatur Ladebeginn 2 |
| STAT_T_AMB_LADEBEGINN_2_EINH | string | "°C" |
| STAT_T_AMB_LADEENDE_2_WERT | real | Umgebungstemperatur Ladeende 2 |
| STAT_T_AMB_LADEENDE_2_EINH | string | "°C" |
| STAT_T_HVB_LADEBEGINN_2_WERT | real | Temperatur HV-Batterie 2 |
| STAT_T_HVB_LADEBEGINN_2_EINH | string | "°C" |
| STAT_T_HVB_LADEENDE_2_WERT | real | Temperatur HV-Batterie Ladeende 2 |
| STAT_T_HVB_LADEENDE_2_EINH | string | "°C" |
| STAT_U_GRID_MIN_2_WERT | unsigned char | Minimale Netzspannung 2 |
| STAT_U_GRID_MIN_2_EINH | string | "V" |
| STAT_U_GRID_MAX_2_WERT | unsigned char | Maximale Netzspannung 2 |
| STAT_U_GRID_MAX_2_EINH | string | "V" |
| STAT_HIST_P_KLE_0_2_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall 0-1 kW 2 |
| STAT_HIST_P_KLE_0_2_EINH | string | "s" |
| STAT_HIST_P_KLE_1_2_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall 1-2 kW 2 |
| STAT_HIST_P_KLE_1_2_EINH | string | "s" |
| STAT_HIST_P_KLE_2_2_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall 2-3 kW 2 |
| STAT_HIST_P_KLE_2_2_EINH | string | "s" |
| STAT_HIST_P_KLE_3_2_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall 3-4 kW 2 |
| STAT_HIST_P_KLE_3_2_EINH | string | "s" |
| STAT_HIST_P_KLE_4_2_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall 4-5 kW 2 |
| STAT_HIST_P_KLE_4_2_EINH | string | "s" |
| STAT_HIST_P_KLE_5_2_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall 5-6 kW 2 |
| STAT_HIST_P_KLE_5_2_EINH | string | "s" |
| STAT_HIST_P_KLE_6_2_WERT | unsigned int | Dauer des Leistungsbedarfs KLE im Intervall &gt; 6 kW 2 |
| STAT_HIST_P_KLE_6_2_EINH | string | "s" |
| STAT_ENERGIE_KLE_2_WERT | unsigned long | Energieverbrauch KLE 2 |
| STAT_ENERGIE_KLE_2_EINH | string | "Wh" |
| STAT_HIST_P_EKMV_EDH_0_2_WERT | unsigned int | Dauer des Leistungsbedarfs von EKMV und EDH im Intervall 0-1 kW 2 |
| STAT_HIST_P_EKMV_EDH_0_2_EINH | string | "s" |
| STAT_HIST_P_EKMV_EDH_1_2_WERT | unsigned int | Dauer des Leistungsbedarfs von EKMV und EDH im Intervall 1-2 kW 2 |
| STAT_HIST_P_EKMV_EDH_1_2_EINH | string | "s" |
| STAT_HIST_P_EKMV_EDH_2_2_WERT | unsigned int | Dauer des Leistungsbedarfs von EKMV und EDH im Intervall 2-3 kW 2 |
| STAT_HIST_P_EKMV_EDH_2_2_EINH | string | "s" |
| STAT_HIST_P_EKMV_EDH_3_2_WERT | unsigned int | Dauer des Leistungsbedarfs von EKMV und EDH im Intervall 3-4 kW 2 |
| STAT_HIST_P_EKMV_EDH_3_2_EINH | string | "s" |
| STAT_HIST_P_EKMV_EDH_4_2_WERT | unsigned int | Dauer des Leistungsbedarfs von EKMV und EDH im Intervall 4-5 kW 2 |
| STAT_HIST_P_EKMV_EDH_4_2_EINH | string | "s" |
| STAT_HIST_P_EKMV_EDH_5_2_WERT | unsigned int | Dauer des Leistungsbedarfs von EKMV und EDH im Intervall &gt; 5 kW 2 |
| STAT_HIST_P_EKMV_EDH_5_2_EINH | string | "s" |
| STAT_ENERGIE_EDH_EKMV_2_WERT | unsigned long | Energieverbrauch EDH und EKMV 2 |
| STAT_ENERGIE_EDH_EKMV_2_EINH | string | "Wh" |
| STAT_ANF_ART_VOKO_2 | unsigned char | Art der Vorkonditionierung 2 |
| STAT_ANF_ART_VOKO_2_BIT_0 | unsigned char | 1 = Voko Innenraum, 0 = keine Voko Innenraum |
| STAT_ANF_ART_VOKO_2_BIT_0_TEXT | string | 1 = Voko Innenraum, 0 = keine Voko Innenraum |
| STAT_ANF_ART_VOKO_2_BIT_1 | unsigned char | 1 = Voko Innenraum forced, 0 = keine Voko Innenraum forced |
| STAT_ANF_ART_VOKO_2_BIT_1_TEXT | string | 1 = Voko Innenraum forced, 0 = keine Voko Innenraum forced |
| STAT_ANF_ART_VOKO_2_BIT_2 | unsigned char | 1 = Voko Batt, 0 = keine Voko Batt |
| STAT_ANF_ART_VOKO_2_BIT_2_TEXT | string | 1 = Voko Batt, 0 = keine Voko Batt |
| STAT_ANF_ART_VOKO_2_BIT_3 | unsigned char | 1 = Voko Batt forced, 0 = keine Voko Batt forced |
| STAT_ANF_ART_VOKO_2_BIT_3_TEXT | string | 1 = Voko Batt forced, 0 = keine Voko Batt forced |
| STAT_HIST_P_HVB_0_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB &lt; -4 kW 2 |
| STAT_HIST_P_HVB_0_2_EINH | string | "s" |
| STAT_HIST_P_HVB_1_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB -4 kW bis -3 kW 2 |
| STAT_HIST_P_HVB_1_2_EINH | string | "s" |
| STAT_HIST_P_HVB_2_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB -3 kW bis -2 kW 2 |
| STAT_HIST_P_HVB_2_2_EINH | string | "s" |
| STAT_HIST_P_HVB_3_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB -2 kW bis -1 kW 2 |
| STAT_HIST_P_HVB_3_2_EINH | string | "s" |
| STAT_HIST_P_HVB_4_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB -1 kW bis 0 kW 2 |
| STAT_HIST_P_HVB_4_2_EINH | string | "s" |
| STAT_HIST_P_HVB_5_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 0 kW bis 1 kW 2 |
| STAT_HIST_P_HVB_5_2_EINH | string | "s" |
| STAT_HIST_P_HVB_6_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 1 kW bis 2 kW 2 |
| STAT_HIST_P_HVB_6_2_EINH | string | "s" |
| STAT_HIST_P_HVB_7_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 2 kW bis 3 kW 2 |
| STAT_HIST_P_HVB_7_2_EINH | string | "s" |
| STAT_HIST_P_HVB_8_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 3 kW bis 4 kW 2 |
| STAT_HIST_P_HVB_8_2_EINH | string | "s" |
| STAT_HIST_P_HVB_9_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 4 kW bis 5 kW 2 |
| STAT_HIST_P_HVB_9_2_EINH | string | "s" |
| STAT_HIST_P_HVB_10_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 5 kW bis 6 kW 2 |
| STAT_HIST_P_HVB_10_2_EINH | string | "s" |
| STAT_HIST_P_HVB_11_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB 6 kW bis 7 kW 2 |
| STAT_HIST_P_HVB_11_2_EINH | string | "s" |
| STAT_HIST_P_HVB_12_2_WERT | unsigned int | Dauer des Leistungsbedarfes der HVB &gt; 7 kW 2 |
| STAT_HIST_P_HVB_12_2_EINH | string | "s" |
| STAT_ENERGIE_HVB_2_WERT | unsigned long | Energieverbrauch HVB 2 |
| STAT_ENERGIE_HVB_2_EINH | string | "Wh" |
| STAT_P_AVG_DCDC_HV_2_WERT | unsigned int | Durchschnittliche Leistung DCDC-Wandler HV-seitig 2 |
| STAT_P_AVG_DCDC_HV_2_EINH | string | "W" |
| STAT_DAUER_SPANNUNGSGRENZE_2_WERT | unsigned int | Dauer in Spannungsbegrenzung während Ladevorgang 2 |
| STAT_DAUER_SPANNUNGSGRENZE_2_EINH | string | "s" |
| STAT_SOC_SPANNUNGSGRENZE_2_WERT | real | SoC bei der Spannungsgrenze erreicht wird 2 |
| STAT_SOC_SPANNUNGSGRENZE_2_EINH | string | "%" |
| STAT_ANZ_NACHLADEANF_WERT | unsigned char | Anzahl Nachladeanforderungen seit letztem TSR |
| STAT_ANZ_NACHLADEANF_EINH | string | "-" |
| STAT_DAUER_NACHLADEANF_WERT | unsigned int | Dauer der letzen Nachladeanforderung |
| STAT_DAUER_NACHLADEANF_EINH | string | "s" |
| STAT_P_LADE_AVG_NVB_WERT | unsigned int | Durchschnittliche Ladeleistung NVB während Nachladeanforderung |
| STAT_P_LADE_AVG_NVB_EINH | string | "W" |
| STAT_P_LADE_AVG_DCDC_HV_WERT | unsigned int | Durchschnittliche Leistung DCDC-Wandler HV-seitig während Nachladeanforderung |
| STAT_P_LADE_AVG_DCDC_HV_EINH | string | "W" |
| STAT_ZUSATZINFO_NACHLADEANF | unsigned char | Bit0: Nachladeanforderung nach Wecken durch IBS Bit1: Ladevorgang bei Fahrzeug wach Bit2: Vorbehalt Bit3: Vorbehalt Bit4: HVB-SoC min. unterschritten Bit5: Min. Nachladestrom NVB unterschritten Bit6: Abbruch durch St_kl_15 Bit7: Schlechte Ladebilanz |
| STAT_ZUSATZINFO_NACHLADEANFORDERUNG | unsigned char | Nachladeanforderung |
| STAT_ZUSATZINFO_NACHLADEANFORDERUNG_TEXT | string | Nachladeanforderung |
| STAT_ZUSATZINFO_ABBRUCHBEDINGUNG | unsigned char | Abbruchbedingung |
| STAT_ZUSATZINFO_ABBRUCHBEDINGUNG_TEXT | string | Abbruchbedingung |
| STAT_GESAMTDAUER_NACHLAUF_WERT | unsigned int | Aufsummierte Nachlaufdauer seit letzten TSR |
| STAT_GESAMTDAUER_NACHLAUF_EINH | string | "s" |
| STAT_P_AVG_DCDC_INSGESAMT_WERT | unsigned int | Durchschnittliche Leistung DCDC-Wandler während Nachlauf |
| STAT_P_AVG_DCDC_INSGESAMT_EINH | string | "W" |
| STAT_P_AVG_BATT_INSGESAMT_WERT | unsigned int | Durchschnittliche Ladeleistung NVB während Nachlauf |
| STAT_P_AVG_BATT_INSGESAMT_EINH | string | "W" |
| STAT_DELTA_SOC_STANDZEIT_1_WERT | real | Änderung SoC über Standzeit_1 |
| STAT_DELTA_SOC_STANDZEIT_1_EINH | string | "%" |
| STAT_DAUER_STANDZEIT_1_WERT | unsigned int | Dauer Standzeit_1 |
| STAT_DAUER_STANDZEIT_1_EINH | string | "min" |
| STAT_DELTA_SOC_STANDZEIT_2_WERT | real | Änderung SoC über Standzeit_2 |
| STAT_DELTA_SOC_STANDZEIT_2_EINH | string | "%" |
| STAT_DAUER_STANDZEIT_2_WERT | unsigned int | Dauer Standzeit_2 |
| STAT_DAUER_STANDZEIT_2_EINH | string | "min" |
| STAT_REAS_DERATING | unsigned char | Ursache(n) des Deratings Bit0: Übertemperatur Bit1: Netzfrequenz zu niedrig Bit2: Ausfall eines Lademoduls Bit3: DC-Strombegrenzung Bit4: Netzseitig verfügbare Leistung kleiner Nennleistung |
| STAT_REAS_DERATING_BIT_0 | unsigned char | 1 = Übertemperatur, 0 = keine Übertemperatur |
| STAT_REAS_DERATING_BIT_0_TEXT | string | 1 = Übertemperatur, 0 = keine Übertemperatur |
| STAT_REAS_DERATING_BIT_1 | unsigned char | 1 = Netzfrequenz zu niedrig, 0 = Netzfrequenz nicht zu niedrig |
| STAT_REAS_DERATING_BIT_1_TEXT | string | 1 = Netzfrequenz zu niedrig, 0 = Netzfrequenz nicht zu niedrig |
| STAT_REAS_DERATING_BIT_2 | unsigned char | 1 = Ausfall eines Lademoduls, 0 = kein Ausfall eines Lademoduls |
| STAT_REAS_DERATING_BIT_2_TEXT | string | 1 = Ausfall eines Lademoduls, 0 = kein Ausfall eines Lademoduls |
| STAT_REAS_DERATING_BIT_3 | unsigned char | 1 = DC-Strombegrenzung, 0 = keine DC-Strombegrenzung |
| STAT_REAS_DERATING_BIT_3_TEXT | string | 1 = DC-Strombegrenzung, 0 = keine DC-Strombegrenzung |
| STAT_REAS_DERATING_BIT_4 | unsigned char | 1 = Netzseitig verfügbare Leistung kleiner Nennleistung, 0 = Netzseitig verfügbare Leistung nicht kleiner Nennleistung |
| STAT_REAS_DERATING_BIT_4_TEXT | string | 1 = Netzseitig verfügbare Leistung kleiner Nennleistung, 0 = Netzseitig verfügbare Leistung nicht kleiner Nennleistung |
| STAT_REAS_DERATING_2 | unsigned char | Ursache(n) des Deratings_2 Bit0: Übertemperatur_2 Bit1: Netzfrequenz zu niedrig_2 Bit2: Ausfall eines Lademoduls_2 Bit3: DC-Strombegrenzung_2 Bit4: Netzseitig verfügbare Leistung kleiner Nennleistung_2 |
| STAT_REAS_DERATING_2_BIT_0 | unsigned char | 1 = Übertemperatur, 0 = keine Übertemperatur |
| STAT_REAS_DERATING_2_BIT_0_TEXT | string | 1 = Übertemperatur, 0 = keine Übertemperatur |
| STAT_REAS_DERATING_2_BIT_1 | unsigned char | 1 = Netzfrequenz zu niedrig, 0 = Netzfrequenz nicht zu niedrig |
| STAT_REAS_DERATING_2_BIT_1_TEXT | string | 1 = Netzfrequenz zu niedrig, 0 = Netzfrequenz nicht zu niedrig |
| STAT_REAS_DERATING_2_BIT_2 | unsigned char | 1 = Ausfall eines Lademoduls, 0 = kein Ausfall eines Lademoduls |
| STAT_REAS_DERATING_2_BIT_2_TEXT | string | 1 = Ausfall eines Lademoduls, 0 = kein Ausfall eines Lademoduls |
| STAT_REAS_DERATING_2_BIT_3 | unsigned char | 1 = DC-Strombegrenzung, 0 = keine DC-Strombegrenzung |
| STAT_REAS_DERATING_2_BIT_3_TEXT | string | 1 = DC-Strombegrenzung, 0 = keine DC-Strombegrenzung |
| STAT_REAS_DERATING_2_BIT_4 | unsigned char | 1 = Netzseitig verfügbare Leistung kleiner Nennleistung, 0 = Netzseitig verfügbare Leistung nicht kleiner Nennleistung |
| STAT_REAS_DERATING_2_BIT_4_TEXT | string | 1 = Netzseitig verfügbare Leistung kleiner Nennleistung, 0 = Netzseitig verfügbare Leistung nicht kleiner Nennleistung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-pm-info-1"></a>
### STATUS_SYSTEMCHECK_PM_INFO_1

0x224022 STATUS_SYSTEMCHECK_PM_INFO_1 Intelligenter Batteriesensor Bitfeld Pminfo1 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIELADUNG_GESAMT_WERT | unsigned long | PMINFO1[0] 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIELADUNG_BILANZ_WERT | unsigned long | Differenz LADUNG - ENTLADUNG in Ah 0 - 65535 |
| STAT_BATTERIELADUNG_BILANZ_EINH | string | Ah |
| STAT_BATTERIELADUNG_GESAMT_EINH | string | Ah |
| STAT_BATTERIEENTLADUNG_GESAMT_WERT | unsigned long | PMINFO1[1] 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIEENTLADUNG_GESAMT_EINH | string | Ah |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_WERT | unsigned long | PMINFO1[2] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_A_B_WERT | unsigned long | PMINFO1[3] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_A_B_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_B_C_WERT | unsigned long | PMINFO1[4] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_B_C_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_C_D_WERT | unsigned long | PMINFO1[5] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_C_D_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_WERT | unsigned long | PMINFO1[6] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_EINH | string | h |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_WERT | unsigned long | PMINFO1[7] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_WERT | unsigned long | PMINFO1[8] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_WERT | unsigned long | PMINFO1[9] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_WERT | unsigned long | PMINFO1[10] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_WERT | unsigned long | PMINFO1[11] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_EINH | string | Minute |
| STAT_KM_STAND_AKTUELL_WERT | unsigned long | PMINFO1[12] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_AKTUELL_EINH | string | kilometer |
| STAT_KM_STAND_VOR_1_TAG_WERT | unsigned long | PMINFO1[13] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_1_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_2_TAG_WERT | unsigned long | PMINFO1[14] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_2_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_3_TAG_WERT | unsigned long | PMINFO1[15] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_3_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_4_TAG_WERT | unsigned long | PMINFO1[16] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_4_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_5_TAG_WERT | unsigned long | PMINFO1[17] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_5_TAG_EINH | string | kilometer |
| STAT_BATTERIETAUSCH_LETZTER_WERT | unsigned long | PMINFO1[18] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_BATTERIETAUSCH_LETZTER_EINH | string | kilometer |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_WERT | unsigned long | PMINFO1[19] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_EINH | string | kilometer |
| STAT_ANZAHL_LEERLAUFDREHZAHLANHEBUNG_EPS | unsigned long | PMINFO1[20] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ANZAHL_LEERLAUFDREHZAHLANHEBUNG_IBS | unsigned long | PMINFO1[20] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_BATTERIEENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_WERT | unsigned long | PMINFO1[22] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_BATTERIEENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_EINH | string | h |
| STAT_RUHESTROM_VOR_3_ZYKLEN_TEXT | string | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_3_ZYKLEN_WERT | int | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_2_ZYKLEN_TEXT | string | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_2_ZYKLEN_WERT | int | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_1_ZYKLUS_TEXT | string | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_1_ZYKLUS_WERT | int | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_AKTUELL_TEXT | string | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_AKTUELL_WERT | int | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_7_ZYKLEN_TEXT | string | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_7_ZYKLEN_WERT | int | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_6_ZYKLEN_TEXT | string | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_6_ZYKLEN_WERT | int | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_5_ZYKLEN_TEXT | string | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_5_ZYKLEN_WERT | int | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_4_ZYKLEN_TEXT | string | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_4_ZYKLEN_WERT | int | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_11_ZYKLEN_TEXT | string | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_11_ZYKLEN_WERT | int | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_10_ZYKLEN_TEXT | string | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_10_ZYKLEN_WERT | int | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_9_ZYKLEN_TEXT | string | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_9_ZYKLEN_WERT | int | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_8_ZYKLEN_TEXT | string | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_8_ZYKLEN_WERT | int | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_15_ZYKLEN_TEXT | string | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_15_ZYKLEN_WERT | int | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_14_ZYKLEN_TEXT | string | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_14_ZYKLEN_WERT | int | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_13_ZYKLEN_TEXT | string | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_13_ZYKLEN_WERT | int | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_12_ZYKLEN_TEXT | string | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_12_ZYKLEN_WERT | int | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_19_ZYKLEN_TEXT | string | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_19_ZYKLEN_WERT | int | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_18_ZYKLEN_TEXT | string | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_18_ZYKLEN_WERT | int | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_17_ZYKLEN_TEXT | string | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_17_ZYKLEN_WERT | int | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_16_ZYKLEN_TEXT | string | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_16_ZYKLEN_WERT | int | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_23_ZYKLEN_TEXT | string | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_23_ZYKLEN_WERT | int | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_22_ZYKLEN_TEXT | string | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_22_ZYKLEN_WERT | int | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_21_ZYKLEN_TEXT | string | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_21_ZYKLEN_WERT | int | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_20_ZYKLEN_TEXT | string | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_20_ZYKLEN_WERT | int | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[29] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_EIN_WERT | unsigned long | PMINFO1[29] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_1_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[30] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_1_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_1_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[30] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_1_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_2_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[31] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_2_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_2_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[31] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_2_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_3_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[32] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_3_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_3_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[32] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_3_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_4_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[33] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_4_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_4_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[33] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_4_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_5_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[34] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_5_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_5_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[34] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_5_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_RUHESTROM_AKTUELL_EINH | string | - |
| STAT_RUHESTROM_VOR_1_ZYKLUS_EINH | string | - |
| STAT_RUHESTROM_VOR_2_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_3_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_4_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_5_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_6_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_7_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_8_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_9_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_10_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_11_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_12_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_13_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_14_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_15_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_16_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_17_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_18_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_19_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_20_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_21_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_22_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_23_ZYKLEN_EINH | string | - |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-pm-info-2"></a>
### STATUS_SYSTEMCHECK_PM_INFO_2

0x224023 STATUS_SYSTEMCHECK_PM_INFO_2 Intelligenter Batteriesensor Bitfeld Pminfo2 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIE_KAPAZITAET_WERT | unsigned long | PMINFO2[0] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIE_KAPAZITAET_EINH | string | Ah |
| STAT_SOH_WERT | real | PMINFO2[1] 1BYTE_in_minus128bis127prozent   Einheit: % |
| STAT_SOH_EINH | string | percent |
| STAT_SOC_FIT_WERT | unsigned long | PMINFO2[2] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_SOC_FIT_EINH | string | percent |
| STAT_TEMP_SAISON_WERT | long | PMINFO2[3] 1BYTE_in_minus128bis127gradCelsius   Einheit: C |
| STAT_TEMP_SAISON_EINH | string | degreeC |
| STAT_ANZAHL_RUHESPANNUNGSAUSWERTUNGEN_OCV | unsigned long | PMINFO2[4] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_Q_SOC_AKTUELL_WERT | unsigned long | PMINFO2[5] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_AKTUELL_EINH | string | Ah |
| STAT_Q_SOC_VOR_1_TAG_WERT | unsigned long | PMINFO2[6] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_1_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_2_TAG_WERT | unsigned long | PMINFO2[7] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_2_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_3_TAG_WERT | unsigned long | PMINFO2[8] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_3_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_4_TAG_WERT | unsigned long | PMINFO2[9] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_4_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_5_TAG_WERT | unsigned long | PMINFO2[10] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_5_TAG_EINH | string | Ah |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_WERT | unsigned long | PMINFO2[11] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_WERT | unsigned long | PMINFO2[12] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_WERT | unsigned long | PMINFO2[13] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_WERT | unsigned long | PMINFO2[14] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_WERT | unsigned long | PMINFO2[15] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_WERT | unsigned long | PMINFO2[16] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_AKTUELL_WERT | unsigned long | PMINFO2[17] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_AKTUELL_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_WERT | unsigned long | PMINFO2[18] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_WERT | unsigned long | PMINFO2[19] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_WERT | unsigned long | PMINFO2[20] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_WERT | unsigned long | PMINFO2[21] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_WERT | unsigned long | PMINFO2[22] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_EINH | string | percent |
| STAT_BZE_DIAG_0 | unsigned long | PMINFO2[23] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_1 | unsigned long | PMINFO2[24] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_2 | unsigned long | PMINFO2[25] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_3 | unsigned long | PMINFO2[26] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_4 | unsigned long | PMINFO2[27] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tsr-pkor"></a>
### STATUS_TSR_PKOR

Status TSR Leistungskoordinator STATUS_TSR_PKOR (0xDEAC)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_T_P_WUNSCH_ID_0_WERT | unsigned int | Heat Up - Zeit, während der Funktion angefordert war. |
| STAT_T_P_WUNSCH_ID_0_EINH | string | "s" |
| STAT_T_P_WUNSCH_ID_1_WERT | unsigned int | E-Heizen - Zeit, während der Funktion angefordert war. |
| STAT_T_P_WUNSCH_ID_1_EINH | string | "s" |
| STAT_T_P_WUNSCH_ID_2_WERT | unsigned int | Cool-Down - Zeit, während der Funktion angefordert war. |
| STAT_T_P_WUNSCH_ID_2_EINH | string | "s" |
| STAT_T_P_WUNSCH_ID_3_WERT | unsigned int | E-Kühlen - Zeit, während der Funktion angefordert war. |
| STAT_T_P_WUNSCH_ID_3_EINH | string | "s" |
| STAT_T_P_WUNSCH_ID_4_WERT | unsigned int | Beschlag - Zeit, während der Funktion angefordert war. |
| STAT_T_P_WUNSCH_ID_4_EINH | string | "s" |
| STAT_T_P_WUNSCH_ID_5_WERT | unsigned int | Defrost - Zeit, während der Funktion angefordert war. |
| STAT_T_P_WUNSCH_ID_5_EINH | string | "s" |
| STAT_T_P_WUNSCH_ID_6_WERT | unsigned int | Batterie Kühlung - Zeit, während der Funktion angefordert war. |
| STAT_T_P_WUNSCH_ID_6_EINH | string | "s" |
| STAT_T_P_WUNSCH_ID_7_WERT | unsigned int | Batterie Kühlung dringend - Zeit, während der Funktion angefordert war. |
| STAT_T_P_WUNSCH_ID_7_EINH | string | "s" |
| STAT_T_P_WUNSCH_ID_8_WERT | unsigned int | Batterieheizung - Zeit, während der Funktion angefordert war. |
| STAT_T_P_WUNSCH_ID_8_EINH | string | "s" |
| STAT_T_P_WUNSCH_ID_9_WERT | unsigned int | DC/DC-Wandler - Zeit, während der Funktion angefordert war. |
| STAT_T_P_WUNSCH_ID_9_EINH | string | "s" |
| STAT_T_P_WUNSCH_ID_10_WERT | unsigned int | Antrieb 1 - Zeit, während der Funktion angefordert war. |
| STAT_T_P_WUNSCH_ID_10_EINH | string | "s" |
| STAT_T_P_WUNSCH_ID_11_WERT | unsigned int | Antrieb 2 - Zeit, während der Funktion angefordert war. |
| STAT_T_P_WUNSCH_ID_11_EINH | string | "s" |
| STAT_T_P_WUNSCH_ID_12_WERT | unsigned int | Antrieb 3 - Zeit, während der Funktion angefordert war. |
| STAT_T_P_WUNSCH_ID_12_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_0_WERT | unsigned int | Heat Up - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 1. |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_0_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_1_WERT | unsigned int | E-Heizen - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 1. |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_1_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_2_WERT | unsigned int | Cool-Down - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 1. |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_2_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_3_WERT | unsigned int | E-Kühlen - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 1. |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_3_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_4_WERT | unsigned int | Beschlag - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 1. |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_4_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_5_WERT | unsigned int | Defrost - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 1. |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_5_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_6_WERT | unsigned int | Batterie Kühlung - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 1. |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_6_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_7_WERT | unsigned int | Batterie Kühlung dringend - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 1. |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_7_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_8_WERT | unsigned int | Batterieheizung - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 1. |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_8_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_9_WERT | unsigned int | DC/DC-Wandler - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 1. |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_9_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_10_WERT | unsigned int | Antrieb 1 - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 1. |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_10_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_11_WERT | unsigned int | Antrieb 2 - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 1. |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_11_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_12_WERT | unsigned int | Antrieb 3 - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 1. |
| STAT_T_P_SOLL_WUNSCH_RANGE1_ID_12_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_0_WERT | unsigned int | Heat Up - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 2. |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_0_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_1_WERT | unsigned int | E-Heizen - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 2. |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_1_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_2_WERT | unsigned int | Cool-Down - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 2. |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_2_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_3_WERT | unsigned int | E-Kühlen - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 2. |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_3_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_4_WERT | unsigned int | Beschlag - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 2. |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_4_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_5_WERT | unsigned int | Defrost - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 2. |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_5_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_6_WERT | unsigned int | Batterie Kühlung - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 2. |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_6_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_7_WERT | unsigned int | Batterie Kühlung dringend - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 2. |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_7_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_8_WERT | unsigned int | Batterieheizung - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 2. |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_8_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_9_WERT | unsigned int | DC/DC-Wandler - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 2. |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_9_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_10_WERT | unsigned int | Antrieb 1 - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 2. |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_10_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_11_WERT | unsigned int | Antrieb 2 - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 2. |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_11_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_12_WERT | unsigned int | Antrieb 3 - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 2. |
| STAT_T_P_SOLL_WUNSCH_RANGE2_ID_12_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_0_WERT | unsigned int | Heat Up - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 3. |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_0_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_1_WERT | unsigned int | E-Heizen - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 3. |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_1_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_2_WERT | unsigned int | Cool-Down - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 3. |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_2_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_3_WERT | unsigned int | E-Kühlen - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 3. |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_3_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_4_WERT | unsigned int | Beschlag - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 3. |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_4_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_5_WERT | unsigned int | Defrost - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 3. |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_5_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_6_WERT | unsigned int | Batterie Kühlung - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 3. |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_6_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_7_WERT | unsigned int | Batterie Kühlung dringend - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 3. |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_7_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_8_WERT | unsigned int | Batterieheizung - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 3. |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_8_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_9_WERT | unsigned int | DC/DC-Wandler - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 3. |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_9_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_10_WERT | unsigned int | Antrieb 1 - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 3. |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_10_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_11_WERT | unsigned int | Antrieb 2 - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 3. |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_11_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_12_WERT | unsigned int | Antrieb 3 - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 3. |
| STAT_T_P_SOLL_WUNSCH_RANGE3_ID_12_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_0_WERT | unsigned int | Heat Up - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 4. |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_0_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_1_WERT | unsigned int | E-Heizen - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 4. |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_1_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_2_WERT | unsigned int | Cool-Down - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 4. |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_2_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_3_WERT | unsigned int | E-Kühlen - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 4. |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_3_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_4_WERT | unsigned int | Beschlag - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 4. |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_4_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_5_WERT | unsigned int | Defrost - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 4. |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_5_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_6_WERT | unsigned int | Batterie Kühlung - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 4. |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_6_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_7_WERT | unsigned int | Batterie Kühlung dringend - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 4. |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_7_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_8_WERT | unsigned int | Batterieheizung - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 4. |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_8_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_9_WERT | unsigned int | DC/DC-Wandler - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 4. |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_9_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_10_WERT | unsigned int | Antrieb 1 - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 4. |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_10_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_11_WERT | unsigned int | Antrieb 2 - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 4. |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_11_EINH | string | "s" |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_12_WERT | unsigned int | Antrieb 3 - Zeit, während der Funktion nicht vollständig freigegeben war, SOC-Bereich 4. |
| STAT_T_P_SOLL_WUNSCH_RANGE4_ID_12_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_0_WERT | unsigned int | Mittlere DCDC-Leistung über die 1. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_0_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_1_WERT | unsigned int | Mittlere DCDC-Leistung über die 2. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_1_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_2_WERT | unsigned int | Mittlere DCDC-Leistung über die 3. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_2_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_3_WERT | unsigned int | Mittlere DCDC-Leistung über die 4. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_3_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_4_WERT | unsigned int | Mittlere DCDC-Leistung über die 5. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_4_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_5_WERT | unsigned int | Mittlere DCDC-Leistung über die 6. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_5_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_6_WERT | unsigned int | Mittlere DCDC-Leistung über die 7. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_6_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_7_WERT | unsigned int | Mittlere DCDC-Leistung über die 1. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_7_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_8_WERT | unsigned int | Mittlere DCDC-Leistung über die 9. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_8_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_9_WERT | unsigned int | Mittlere DCDC-Leistung über die 10. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_9_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_10_WERT | unsigned int | Mittlere DCDC-Leistung über die 11. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_10_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_11_WERT | unsigned int | Mittlere DCDC-Leistung über die 12. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_11_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_12_WERT | unsigned int | Mittlere DCDC-Leistung über die 13. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_12_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_13_WERT | unsigned int | Mittlere DCDC-Leistung über die 14. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_13_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_14_WERT | unsigned int | Mittlere DCDC-Leistung über die 15. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_14_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_15_WERT | unsigned int | Mittlere DCDC-Leistung über die 16. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_15_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_16_WERT | unsigned int | Mittlere DCDC-Leistung über die 17. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_16_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_17_WERT | unsigned int | Mittlere DCDC-Leistung über die 18. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_17_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_18_WERT | unsigned int | Mittlere DCDC-Leistung über die 19. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_18_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_19_WERT | unsigned int | Mittlere DCDC-Leistung über die 20. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_19_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_20_WERT | unsigned int | Mittlere DCDC-Leistung über die 21. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_20_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_21_WERT | unsigned int | Mittlere DCDC-Leistung über die 22. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_21_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_22_WERT | unsigned int | Mittlere DCDC-Leistung über die 23. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_22_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_23_WERT | unsigned int | Mittlere DCDC-Leistung über die 24. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_23_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_24_WERT | unsigned int | Mittlere DCDC-Leistung über die 25. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_24_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_25_WERT | unsigned int | Mittlere DCDC-Leistung über die 26. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_25_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_26_WERT | unsigned int | Mittlere DCDC-Leistung über die 27. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_26_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_27_WERT | unsigned int | Mittlere DCDC-Leistung über die 28. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_27_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_28_WERT | unsigned int | Mittlere DCDC-Leistung über die 29. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_28_EINH | string | "s" |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_29_WERT | unsigned int | Mittlere DCDC-Leistung über die 30. Minute |
| STAT_P_HVPM_DCDC_MITTEL_30MIN_29_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_0_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 1. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_0_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_1_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 2. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_1_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_2_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 3. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_2_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_3_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 4. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_3_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_4_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 5. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_4_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_5_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 6. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_5_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_6_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 7. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_6_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_7_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 8. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_7_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_8_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 9. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_8_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_9_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 10. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_9_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_10_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 11. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_10_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_11_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 12. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_11_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_12_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 13. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_12_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_13_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 14. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_13_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_14_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 15. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_14_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_15_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 16. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_15_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_16_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 17. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_16_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_17_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 18. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_17_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_18_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 19. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_18_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_19_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 20. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_19_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_20_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 21. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_20_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_21_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 22. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_21_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_22_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 23. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_22_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_23_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 24. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_23_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_24_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 25. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_24_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_25_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 26. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_25_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_26_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 27. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_26_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_27_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 28. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_27_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_28_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 29. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_28_EINH | string | "s" |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_29_WERT | unsigned int | Mittlere Leistung Komfortverbraucher über die 30. Minute |
| STAT_P_HVPM_KOMFORT_MITTEL_30MIN_29_EINH | string | "s" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ecopro"></a>
### STATUS_ECOPRO

STATUS_ECOPRO (0xDEB8)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ECOPRO_NR | unsigned char | Zustand Fahrerlebnisschalter ECOPro |
| STAT_ECOPRO_NR_TEXT | string | Zustand Fahrerlebnisschalter ECOPro |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tsr-3-lesen"></a>
### STATUS_TSR_3_LESEN

Teleservice Daten 3 auslesen STATUS_TSR_3_LESEN (0xE3)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BSZFAHRB_WERT | unsigned long | Betriebsstundenzähler fahrbereit |
| STAT_BSZFAHRB_EINH | string | "%" |
| STAT_AS_BER001_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 1, M-Bereich 1) |
| STAT_AS_BER001_EINH | string | "%" |
| STAT_AS_BER002_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 1, M-Bereich 2) |
| STAT_AS_BER002_EINH | string | "%" |
| STAT_AS_BER003_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 1, M-Bereich 3) |
| STAT_AS_BER003_EINH | string | "%" |
| STAT_AS_BER004_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 1, M-Bereich 4) |
| STAT_AS_BER004_EINH | string | "%" |
| STAT_AS_BER005_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 1, M-Bereich 5) |
| STAT_AS_BER005_EINH | string | "%" |
| STAT_AS_BER006_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 1, M-Bereich 6) |
| STAT_AS_BER006_EINH | string | "%" |
| STAT_AS_BER007_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 1, M-Bereich 7) |
| STAT_AS_BER007_EINH | string | "%" |
| STAT_AS_BER008_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 1, M-Bereich 8) |
| STAT_AS_BER008_EINH | string | "%" |
| STAT_AS_BER009_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 1, M-Bereich 9) |
| STAT_AS_BER009_EINH | string | "%" |
| STAT_AS_BER010_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 1, M-Bereich 10) |
| STAT_AS_BER010_EINH | string | "%" |
| STAT_AS_BER011_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 1, M-Bereich 11) |
| STAT_AS_BER011_EINH | string | "%" |
| STAT_AS_BER012_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 1, M-Bereich 12) |
| STAT_AS_BER012_EINH | string | "%" |
| STAT_AS_BER101_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 2, M-Bereich 1) |
| STAT_AS_BER101_EINH | string | "%" |
| STAT_AS_BER102_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 2, M-Bereich 2) |
| STAT_AS_BER102_EINH | string | "%" |
| STAT_AS_BER103_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 2, M-Bereich 3) |
| STAT_AS_BER103_EINH | string | "%" |
| STAT_AS_BER104_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 2, M-Bereich 4) |
| STAT_AS_BER104_EINH | string | "%" |
| STAT_AS_BER105_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 2, M-Bereich 5) |
| STAT_AS_BER105_EINH | string | "%" |
| STAT_AS_BER106_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 2, M-Bereich 6) |
| STAT_AS_BER106_EINH | string | "%" |
| STAT_AS_BER107_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 2, M-Bereich 7) |
| STAT_AS_BER107_EINH | string | "%" |
| STAT_AS_BER108_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 2, M-Bereich 8) |
| STAT_AS_BER108_EINH | string | "%" |
| STAT_AS_BER109_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 2, M-Bereich 9) |
| STAT_AS_BER109_EINH | string | "%" |
| STAT_AS_BER110_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 2, M-Bereich 10) |
| STAT_AS_BER110_EINH | string | "%" |
| STAT_AS_BER111_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 2, M-Bereich 11) |
| STAT_AS_BER111_EINH | string | "%" |
| STAT_AS_BER112_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 2, M-Bereich 12) |
| STAT_AS_BER112_EINH | string | "%" |
| STAT_AS_BER201_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 3, M-Bereich 1) |
| STAT_AS_BER201_EINH | string | "%" |
| STAT_AS_BER202_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 3, M-Bereich 2) |
| STAT_AS_BER202_EINH | string | "%" |
| STAT_AS_BER203_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 3, M-Bereich 3) |
| STAT_AS_BER203_EINH | string | "%" |
| STAT_AS_BER204_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 3, M-Bereich 4) |
| STAT_AS_BER204_EINH | string | "%" |
| STAT_AS_BER205_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 3, M-Bereich 5) |
| STAT_AS_BER205_EINH | string | "%" |
| STAT_AS_BER206_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 3, M-Bereich 6) |
| STAT_AS_BER206_EINH | string | "%" |
| STAT_AS_BER207_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 3, M-Bereich 7) |
| STAT_AS_BER207_EINH | string | "%" |
| STAT_AS_BER208_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 3, M-Bereich 8) |
| STAT_AS_BER208_EINH | string | "%" |
| STAT_AS_BER209_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 3, M-Bereich 9) |
| STAT_AS_BER209_EINH | string | "%" |
| STAT_AS_BER210_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 3, M-Bereich 10) |
| STAT_AS_BER210_EINH | string | "%" |
| STAT_AS_BER211_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 3, M-Bereich 11) |
| STAT_AS_BER211_EINH | string | "%" |
| STAT_AS_BER212_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 3, M-Bereich 12) |
| STAT_AS_BER212_EINH | string | "%" |
| STAT_AS_BER301_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 4, M-Bereich 1) |
| STAT_AS_BER301_EINH | string | "%" |
| STAT_AS_BER302_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 4, M-Bereich 2) |
| STAT_AS_BER302_EINH | string | "%" |
| STAT_AS_BER303_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 4, M-Bereich 3) |
| STAT_AS_BER303_EINH | string | "%" |
| STAT_AS_BER304_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 4, M-Bereich 4) |
| STAT_AS_BER304_EINH | string | "%" |
| STAT_AS_BER305_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 4, M-Bereich 5) |
| STAT_AS_BER305_EINH | string | "%" |
| STAT_AS_BER306_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 4, M-Bereich 6) |
| STAT_AS_BER306_EINH | string | "%" |
| STAT_AS_BER307_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 4, M-Bereich 7) |
| STAT_AS_BER307_EINH | string | "%" |
| STAT_AS_BER308_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 4, M-Bereich 8) |
| STAT_AS_BER308_EINH | string | "%" |
| STAT_AS_BER309_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 4, M-Bereich 9) |
| STAT_AS_BER309_EINH | string | "%" |
| STAT_AS_BER310_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 4, M-Bereich 10) |
| STAT_AS_BER310_EINH | string | "%" |
| STAT_AS_BER311_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 4, M-Bereich 11) |
| STAT_AS_BER311_EINH | string | "%" |
| STAT_AS_BER312_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 4, M-Bereich 12) |
| STAT_AS_BER312_EINH | string | "%" |
| STAT_AS_BER401_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 5, M-Bereich 1) |
| STAT_AS_BER401_EINH | string | "%" |
| STAT_AS_BER402_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 5, M-Bereich 2) |
| STAT_AS_BER402_EINH | string | "%" |
| STAT_AS_BER403_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 5, M-Bereich 3) |
| STAT_AS_BER403_EINH | string | "%" |
| STAT_AS_BER404_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 5, M-Bereich 4) |
| STAT_AS_BER404_EINH | string | "%" |
| STAT_AS_BER405_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 5, M-Bereich 5) |
| STAT_AS_BER405_EINH | string | "%" |
| STAT_AS_BER406_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 5, M-Bereich 6) |
| STAT_AS_BER406_EINH | string | "%" |
| STAT_AS_BER407_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 5, M-Bereich 7) |
| STAT_AS_BER407_EINH | string | "%" |
| STAT_AS_BER408_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 5, M-Bereich 8) |
| STAT_AS_BER408_EINH | string | "%" |
| STAT_AS_BER409_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 5, M-Bereich 9) |
| STAT_AS_BER409_EINH | string | "%" |
| STAT_AS_BER410_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 5, M-Bereich 10) |
| STAT_AS_BER410_EINH | string | "%" |
| STAT_AS_BER411_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 5, M-Bereich 11) |
| STAT_AS_BER411_EINH | string | "%" |
| STAT_AS_BER412_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 5, M-Bereich 12) |
| STAT_AS_BER412_EINH | string | "%" |
| STAT_AS_BER501_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 6, M-Bereich 1) |
| STAT_AS_BER501_EINH | string | "%" |
| STAT_AS_BER502_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 6, M-Bereich 2) |
| STAT_AS_BER502_EINH | string | "%" |
| STAT_AS_BER503_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 6, M-Bereich 3) |
| STAT_AS_BER503_EINH | string | "%" |
| STAT_AS_BER504_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 6, M-Bereich 4) |
| STAT_AS_BER504_EINH | string | "%" |
| STAT_AS_BER505_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 6, M-Bereich 5) |
| STAT_AS_BER505_EINH | string | "%" |
| STAT_AS_BER506_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 6, M-Bereich 6) |
| STAT_AS_BER506_EINH | string | "%" |
| STAT_AS_BER507_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 6, M-Bereich 7) |
| STAT_AS_BER507_EINH | string | "%" |
| STAT_AS_BER508_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 6, M-Bereich 8) |
| STAT_AS_BER508_EINH | string | "%" |
| STAT_AS_BER509_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 6, M-Bereich 9) |
| STAT_AS_BER509_EINH | string | "%" |
| STAT_AS_BER510_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 6, M-Bereich 10) |
| STAT_AS_BER510_EINH | string | "%" |
| STAT_AS_BER511_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 6, M-Bereich 11) |
| STAT_AS_BER511_EINH | string | "%" |
| STAT_AS_BER512_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 6, M-Bereich 12) |
| STAT_AS_BER512_EINH | string | "%" |
| STAT_AS_BER601_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 7, M-Bereich 1) |
| STAT_AS_BER601_EINH | string | "%" |
| STAT_AS_BER602_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 7, M-Bereich 2) |
| STAT_AS_BER602_EINH | string | "%" |
| STAT_AS_BER603_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 7, M-Bereich 3) |
| STAT_AS_BER603_EINH | string | "%" |
| STAT_AS_BER604_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 7, M-Bereich 4) |
| STAT_AS_BER604_EINH | string | "%" |
| STAT_AS_BER605_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 7, M-Bereich 5) |
| STAT_AS_BER605_EINH | string | "%" |
| STAT_AS_BER606_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 7, M-Bereich 6) |
| STAT_AS_BER606_EINH | string | "%" |
| STAT_AS_BER607_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 7, M-Bereich 7) |
| STAT_AS_BER607_EINH | string | "%" |
| STAT_AS_BER608_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 7, M-Bereich 8) |
| STAT_AS_BER608_EINH | string | "%" |
| STAT_AS_BER609_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 7, M-Bereich 9) |
| STAT_AS_BER609_EINH | string | "%" |
| STAT_AS_BER610_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 7, M-Bereich 10) |
| STAT_AS_BER610_EINH | string | "%" |
| STAT_AS_BER611_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 7, M-Bereich 11) |
| STAT_AS_BER611_EINH | string | "%" |
| STAT_AS_BER612_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 7, M-Bereich 12) |
| STAT_AS_BER612_EINH | string | "%" |
| STAT_AS_BER701_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 8, M-Bereich 1) |
| STAT_AS_BER701_EINH | string | "%" |
| STAT_AS_BER702_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 8, M-Bereich 2) |
| STAT_AS_BER702_EINH | string | "%" |
| STAT_AS_BER703_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 8, M-Bereich 3) |
| STAT_AS_BER703_EINH | string | "%" |
| STAT_AS_BER704_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 8, M-Bereich 4) |
| STAT_AS_BER704_EINH | string | "%" |
| STAT_AS_BER705_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 8, M-Bereich 5) |
| STAT_AS_BER705_EINH | string | "%" |
| STAT_AS_BER706_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 8, M-Bereich 6) |
| STAT_AS_BER706_EINH | string | "%" |
| STAT_AS_BER707_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 8, M-Bereich 7) |
| STAT_AS_BER707_EINH | string | "%" |
| STAT_AS_BER708_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 8, M-Bereich 8) |
| STAT_AS_BER708_EINH | string | "%" |
| STAT_AS_BER709_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 8, M-Bereich 9) |
| STAT_AS_BER709_EINH | string | "%" |
| STAT_AS_BER710_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 8, M-Bereich 10) |
| STAT_AS_BER710_EINH | string | "%" |
| STAT_AS_BER711_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 8, M-Bereich 11) |
| STAT_AS_BER711_EINH | string | "%" |
| STAT_AS_BER712_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 8, M-Bereich 12) |
| STAT_AS_BER712_EINH | string | "%" |
| STAT_AS_BER801_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 9, M-Bereich 1) |
| STAT_AS_BER801_EINH | string | "%" |
| STAT_AS_BER802_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 9, M-Bereich 2) |
| STAT_AS_BER802_EINH | string | "%" |
| STAT_AS_BER803_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 9, M-Bereich 3) |
| STAT_AS_BER803_EINH | string | "%" |
| STAT_AS_BER804_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 9, M-Bereich 4) |
| STAT_AS_BER804_EINH | string | "%" |
| STAT_AS_BER805_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 9, M-Bereich 5) |
| STAT_AS_BER805_EINH | string | "%" |
| STAT_AS_BER806_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 9, M-Bereich 6) |
| STAT_AS_BER806_EINH | string | "%" |
| STAT_AS_BER807_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 9, M-Bereich 7) |
| STAT_AS_BER807_EINH | string | "%" |
| STAT_AS_BER808_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 9, M-Bereich 8) |
| STAT_AS_BER808_EINH | string | "%" |
| STAT_AS_BER809_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 9, M-Bereich 9) |
| STAT_AS_BER809_EINH | string | "%" |
| STAT_AS_BER810_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 9, M-Bereich 10) |
| STAT_AS_BER810_EINH | string | "%" |
| STAT_AS_BER811_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 9, M-Bereich 11) |
| STAT_AS_BER811_EINH | string | "%" |
| STAT_AS_BER812_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 9, M-Bereich 12) |
| STAT_AS_BER812_EINH | string | "%" |
| STAT_AS_BER901_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 10, M-Bereich 1) |
| STAT_AS_BER901_EINH | string | "%" |
| STAT_AS_BER902_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 10, M-Bereich 2) |
| STAT_AS_BER902_EINH | string | "%" |
| STAT_AS_BER903_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 10, M-Bereich 3) |
| STAT_AS_BER903_EINH | string | "%" |
| STAT_AS_BER904_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 10, M-Bereich 4) |
| STAT_AS_BER904_EINH | string | "%" |
| STAT_AS_BER905_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 10, M-Bereich 5) |
| STAT_AS_BER905_EINH | string | "%" |
| STAT_AS_BER906_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 10, M-Bereich 6) |
| STAT_AS_BER906_EINH | string | "%" |
| STAT_AS_BER907_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 10, M-Bereich 7) |
| STAT_AS_BER907_EINH | string | "%" |
| STAT_AS_BER908_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 10, M-Bereich 8) |
| STAT_AS_BER908_EINH | string | "%" |
| STAT_AS_BER909_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 10, M-Bereich 9) |
| STAT_AS_BER909_EINH | string | "%" |
| STAT_AS_BER910_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 10, M-Bereich 10) |
| STAT_AS_BER910_EINH | string | "%" |
| STAT_AS_BER911_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 10, M-Bereich 11) |
| STAT_AS_BER911_EINH | string | "%" |
| STAT_AS_BER912_WERT | real | Betriebspunkt Antriebssystem (v-Bereich 10, M-Bereich 12) |
| STAT_AS_BER912_EINH | string | "%" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bpas-lesen"></a>
### STATUS_BPAS_LESEN

Teleservice Daten bzgl. BPAS auslesen STATUS_TSR_3_LESEN (0xE6)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BSZ_WERT | unsigned long | Betriebsstundenzähler gesamt |
| STAT_BSZFAHRB_WERT | real | Betriebsstundenzähler fahrbereit |
| STAT_BPAS110_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 1, M-Bereich 1) |
| STAT_BPAS111_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 1, M-Bereich 2) |
| STAT_BPAS112_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 1, M-Bereich 3) |
| STAT_BPAS113_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 1, M-Bereich 4) |
| STAT_BPAS114_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 1, M-Bereich 5) |
| STAT_BPAS115_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 1, M-Bereich 6) |
| STAT_BPAS116_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 1, M-Bereich 7) |
| STAT_BPAS117_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 1, M-Bereich 8) |
| STAT_BPAS118_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 1, M-Bereich 9) |
| STAT_BPAS119_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 1, M-Bereich 10) |
| STAT_BPAS120_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 2, M-Bereich 1) |
| STAT_BPAS121_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 2, M-Bereich 2) |
| STAT_BPAS122_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 2, M-Bereich 3) |
| STAT_BPAS123_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 2, M-Bereich 4) |
| STAT_BPAS124_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 2, M-Bereich 5) |
| STAT_BPAS125_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 2, M-Bereich 6) |
| STAT_BPAS126_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 2, M-Bereich 7) |
| STAT_BPAS127_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 2, M-Bereich 8) |
| STAT_BPAS128_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 2, M-Bereich 9) |
| STAT_BPAS129_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 2, M-Bereich 10) |
| STAT_BPAS130_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 3, M-Bereich 1) |
| STAT_BPAS131_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 3, M-Bereich 2) |
| STAT_BPAS132_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 3, M-Bereich 3) |
| STAT_BPAS133_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 3, M-Bereich 4) |
| STAT_BPAS134_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 3, M-Bereich 5) |
| STAT_BPAS135_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 3, M-Bereich 6) |
| STAT_BPAS136_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 3, M-Bereich 7) |
| STAT_BPAS137_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 3, M-Bereich 8) |
| STAT_BPAS138_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 3, M-Bereich 9) |
| STAT_BPAS139_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 3, M-Bereich 10) |
| STAT_BPAS140_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 4, M-Bereich 1) |
| STAT_BPAS141_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 4, M-Bereich 2) |
| STAT_BPAS142_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 4, M-Bereich 3) |
| STAT_BPAS143_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 4, M-Bereich 4) |
| STAT_BPAS144_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 4, M-Bereich 5) |
| STAT_BPAS145_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 4, M-Bereich 6) |
| STAT_BPAS146_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 4, M-Bereich 7) |
| STAT_BPAS147_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 4, M-Bereich 8) |
| STAT_BPAS148_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 4, M-Bereich 9) |
| STAT_BPAS149_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 4, M-Bereich 10) |
| STAT_BPAS150_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 5, M-Bereich 1) |
| STAT_BPAS151_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 5, M-Bereich 2) |
| STAT_BPAS152_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 5, M-Bereich 3) |
| STAT_BPAS153_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 5, M-Bereich 4) |
| STAT_BPAS154_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 5, M-Bereich 5) |
| STAT_BPAS155_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 5, M-Bereich 6) |
| STAT_BPAS156_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 5, M-Bereich 7) |
| STAT_BPAS157_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 5, M-Bereich 8) |
| STAT_BPAS158_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 5, M-Bereich 9) |
| STAT_BPAS159_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 5, M-Bereich 10) |
| STAT_BPAS160_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 6, M-Bereich 1) |
| STAT_BPAS161_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 6, M-Bereich 2) |
| STAT_BPAS162_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 6, M-Bereich 3) |
| STAT_BPAS163_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 6, M-Bereich 4) |
| STAT_BPAS164_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 6, M-Bereich 5) |
| STAT_BPAS165_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 6, M-Bereich 6) |
| STAT_BPAS166_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 6, M-Bereich 7) |
| STAT_BPAS167_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 6, M-Bereich 8) |
| STAT_BPAS168_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 6, M-Bereich 9) |
| STAT_BPAS169_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 6, M-Bereich 10) |
| STAT_BPAS170_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 7, M-Bereich 1) |
| STAT_BPAS171_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 7, M-Bereich 2) |
| STAT_BPAS172_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 7, M-Bereich 3) |
| STAT_BPAS173_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 7, M-Bereich 4) |
| STAT_BPAS174_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 7, M-Bereich 5) |
| STAT_BPAS175_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 7, M-Bereich 6) |
| STAT_BPAS176_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 7, M-Bereich 7) |
| STAT_BPAS177_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 7, M-Bereich 8) |
| STAT_BPAS178_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 7, M-Bereich 9) |
| STAT_BPAS179_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 7, M-Bereich 10) |
| STAT_BPAS180_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 8, M-Bereich 1) |
| STAT_BPAS181_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 8, M-Bereich 2) |
| STAT_BPAS182_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 8, M-Bereich 3) |
| STAT_BPAS183_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 8, M-Bereich 4) |
| STAT_BPAS184_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 8, M-Bereich 5) |
| STAT_BPAS185_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 8, M-Bereich 6) |
| STAT_BPAS186_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 8, M-Bereich 7) |
| STAT_BPAS187_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 8, M-Bereich 8) |
| STAT_BPAS188_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 8, M-Bereich 9) |
| STAT_BPAS189_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 1, v-Bereich 8, M-Bereich 10) |
| STAT_BPAS210_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 1, M-Bereich 1) |
| STAT_BPAS211_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 1, M-Bereich 2) |
| STAT_BPAS212_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 1, M-Bereich 3) |
| STAT_BPAS213_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 1, M-Bereich 4) |
| STAT_BPAS214_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 1, M-Bereich 5) |
| STAT_BPAS215_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 1, M-Bereich 6) |
| STAT_BPAS216_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 1, M-Bereich 7) |
| STAT_BPAS217_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 1, M-Bereich 8) |
| STAT_BPAS218_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 1, M-Bereich 9) |
| STAT_BPAS219_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 1, M-Bereich 10) |
| STAT_BPAS220_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 2, M-Bereich 1) |
| STAT_BPAS221_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 2, M-Bereich 2) |
| STAT_BPAS222_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 2, M-Bereich 3) |
| STAT_BPAS223_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 2, M-Bereich 4) |
| STAT_BPAS224_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 2, M-Bereich 5) |
| STAT_BPAS225_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 2, M-Bereich 6) |
| STAT_BPAS226_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 2, M-Bereich 7) |
| STAT_BPAS227_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 2, M-Bereich 8) |
| STAT_BPAS228_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 2, M-Bereich 9) |
| STAT_BPAS229_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 2, M-Bereich 10) |
| STAT_BPAS230_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 3, M-Bereich 1) |
| STAT_BPAS231_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 3, M-Bereich 2) |
| STAT_BPAS232_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 3, M-Bereich 3) |
| STAT_BPAS233_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 3, M-Bereich 4) |
| STAT_BPAS234_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 3, M-Bereich 5) |
| STAT_BPAS235_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 3, M-Bereich 6) |
| STAT_BPAS236_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 3, M-Bereich 7) |
| STAT_BPAS237_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 3, M-Bereich 8) |
| STAT_BPAS238_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 3, M-Bereich 9) |
| STAT_BPAS239_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 3, M-Bereich 10) |
| STAT_BPAS240_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 4, M-Bereich 1) |
| STAT_BPAS241_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 4, M-Bereich 2) |
| STAT_BPAS242_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 4, M-Bereich 3) |
| STAT_BPAS243_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 4, M-Bereich 4) |
| STAT_BPAS244_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 4, M-Bereich 5) |
| STAT_BPAS245_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 4, M-Bereich 6) |
| STAT_BPAS246_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 4, M-Bereich 7) |
| STAT_BPAS247_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 4, M-Bereich 8) |
| STAT_BPAS248_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 4, M-Bereich 9) |
| STAT_BPAS249_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 4, M-Bereich 10) |
| STAT_BPAS250_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 5, M-Bereich 1) |
| STAT_BPAS251_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 5, M-Bereich 2) |
| STAT_BPAS252_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 5, M-Bereich 3) |
| STAT_BPAS253_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 5, M-Bereich 4) |
| STAT_BPAS254_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 5, M-Bereich 5) |
| STAT_BPAS255_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 5, M-Bereich 6) |
| STAT_BPAS256_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 5, M-Bereich 7) |
| STAT_BPAS257_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 5, M-Bereich 8) |
| STAT_BPAS258_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 5, M-Bereich 9) |
| STAT_BPAS259_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 5, M-Bereich 10) |
| STAT_BPAS260_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 6, M-Bereich 1) |
| STAT_BPAS261_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 6, M-Bereich 2) |
| STAT_BPAS262_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 6, M-Bereich 3) |
| STAT_BPAS263_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 6, M-Bereich 4) |
| STAT_BPAS264_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 6, M-Bereich 5) |
| STAT_BPAS265_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 6, M-Bereich 6) |
| STAT_BPAS266_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 6, M-Bereich 7) |
| STAT_BPAS267_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 6, M-Bereich 8) |
| STAT_BPAS268_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 6, M-Bereich 9) |
| STAT_BPAS269_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 6, M-Bereich 10) |
| STAT_BPAS270_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 7, M-Bereich 1) |
| STAT_BPAS271_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 7, M-Bereich 2) |
| STAT_BPAS272_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 7, M-Bereich 3) |
| STAT_BPAS273_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 7, M-Bereich 4) |
| STAT_BPAS274_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 7, M-Bereich 5) |
| STAT_BPAS275_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 7, M-Bereich 6) |
| STAT_BPAS276_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 7, M-Bereich 7) |
| STAT_BPAS277_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 7, M-Bereich 8) |
| STAT_BPAS278_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 7, M-Bereich 9) |
| STAT_BPAS279_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 7, M-Bereich 10) |
| STAT_BPAS280_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 8, M-Bereich 1) |
| STAT_BPAS281_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 8, M-Bereich 2) |
| STAT_BPAS282_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 8, M-Bereich 3) |
| STAT_BPAS283_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 8, M-Bereich 4) |
| STAT_BPAS284_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 8, M-Bereich 5) |
| STAT_BPAS285_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 8, M-Bereich 6) |
| STAT_BPAS286_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 8, M-Bereich 7) |
| STAT_BPAS287_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 8, M-Bereich 8) |
| STAT_BPAS288_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 8, M-Bereich 9) |
| STAT_BPAS289_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 2, v-Bereich 8, M-Bereich 10) |
| STAT_BPAS310_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 1, M-Bereich 1) |
| STAT_BPAS311_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 1, M-Bereich 2) |
| STAT_BPAS312_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 1, M-Bereich 3) |
| STAT_BPAS313_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 1, M-Bereich 4) |
| STAT_BPAS314_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 1, M-Bereich 5) |
| STAT_BPAS315_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 1, M-Bereich 6) |
| STAT_BPAS316_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 1, M-Bereich 7) |
| STAT_BPAS317_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 1, M-Bereich 8) |
| STAT_BPAS318_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 1, M-Bereich 9) |
| STAT_BPAS319_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 1, M-Bereich 10) |
| STAT_BPAS320_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 2, M-Bereich 1) |
| STAT_BPAS321_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 2, M-Bereich 2) |
| STAT_BPAS322_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 2, M-Bereich 3) |
| STAT_BPAS323_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 2, M-Bereich 4) |
| STAT_BPAS324_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 2, M-Bereich 5) |
| STAT_BPAS325_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 2, M-Bereich 6) |
| STAT_BPAS326_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 2, M-Bereich 7) |
| STAT_BPAS327_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 2, M-Bereich 8) |
| STAT_BPAS328_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 2, M-Bereich 9) |
| STAT_BPAS329_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 2, M-Bereich 10) |
| STAT_BPAS330_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 3, M-Bereich 1) |
| STAT_BPAS331_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 3, M-Bereich 2) |
| STAT_BPAS332_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 3, M-Bereich 3) |
| STAT_BPAS333_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 3, M-Bereich 4) |
| STAT_BPAS334_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 3, M-Bereich 5) |
| STAT_BPAS335_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 3, M-Bereich 6) |
| STAT_BPAS336_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 3, M-Bereich 7) |
| STAT_BPAS337_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 3, M-Bereich 8) |
| STAT_BPAS338_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 3, M-Bereich 9) |
| STAT_BPAS339_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 3, M-Bereich 10) |
| STAT_BPAS340_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 4, M-Bereich 1) |
| STAT_BPAS341_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 4, M-Bereich 2) |
| STAT_BPAS342_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 4, M-Bereich 3) |
| STAT_BPAS343_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 4, M-Bereich 4) |
| STAT_BPAS344_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 4, M-Bereich 5) |
| STAT_BPAS345_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 4, M-Bereich 6) |
| STAT_BPAS346_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 4, M-Bereich 7) |
| STAT_BPAS347_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 4, M-Bereich 8) |
| STAT_BPAS348_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 4, M-Bereich 9) |
| STAT_BPAS349_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 4, M-Bereich 10) |
| STAT_BPAS350_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 5, M-Bereich 1) |
| STAT_BPAS351_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 5, M-Bereich 2) |
| STAT_BPAS352_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 5, M-Bereich 3) |
| STAT_BPAS353_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 5, M-Bereich 4) |
| STAT_BPAS354_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 5, M-Bereich 5) |
| STAT_BPAS355_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 5, M-Bereich 6) |
| STAT_BPAS356_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 5, M-Bereich 7) |
| STAT_BPAS357_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 5, M-Bereich 8) |
| STAT_BPAS358_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 5, M-Bereich 9) |
| STAT_BPAS359_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 5, M-Bereich 10) |
| STAT_BPAS360_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 6, M-Bereich 1) |
| STAT_BPAS361_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 6, M-Bereich 2) |
| STAT_BPAS362_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 6, M-Bereich 3) |
| STAT_BPAS363_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 6, M-Bereich 4) |
| STAT_BPAS364_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 6, M-Bereich 5) |
| STAT_BPAS365_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 6, M-Bereich 6) |
| STAT_BPAS366_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 6, M-Bereich 7) |
| STAT_BPAS367_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 6, M-Bereich 8) |
| STAT_BPAS368_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 6, M-Bereich 9) |
| STAT_BPAS369_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 6, M-Bereich 10) |
| STAT_BPAS370_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 7, M-Bereich 1) |
| STAT_BPAS371_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 7, M-Bereich 2) |
| STAT_BPAS372_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 7, M-Bereich 3) |
| STAT_BPAS373_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 7, M-Bereich 4) |
| STAT_BPAS374_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 7, M-Bereich 5) |
| STAT_BPAS375_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 7, M-Bereich 6) |
| STAT_BPAS376_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 7, M-Bereich 7) |
| STAT_BPAS377_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 7, M-Bereich 8) |
| STAT_BPAS378_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 7, M-Bereich 9) |
| STAT_BPAS379_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 7, M-Bereich 10) |
| STAT_BPAS380_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 8, M-Bereich 1) |
| STAT_BPAS381_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 8, M-Bereich 2) |
| STAT_BPAS382_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 8, M-Bereich 3) |
| STAT_BPAS383_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 8, M-Bereich 4) |
| STAT_BPAS384_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 8, M-Bereich 5) |
| STAT_BPAS385_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 8, M-Bereich 6) |
| STAT_BPAS386_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 8, M-Bereich 7) |
| STAT_BPAS387_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 8, M-Bereich 8) |
| STAT_BPAS388_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 8, M-Bereich 9) |
| STAT_BPAS389_WERT | real | Betriebspunkt Antriebssystem (U_HV-Bereich 3, v-Bereich 8, M-Bereich 10) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-aep-info-1"></a>
### STATUS_SYSTEMCHECK_AEP_INFO_1

0x22DEBA STATUS_SYSTEMCHECK_AEP_INFO_1 Intelligenter Batteriesensor Bitfeld Pminfo1 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIELADUNG_GESAMT_WERT | unsigned long | PMINFO1[0] 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIELADUNG_BILANZ_WERT | unsigned long | Differenz LADUNG - ENTLADUNG in Ah 0 - 65535 |
| STAT_BATTERIELADUNG_BILANZ_EINH | string | Ah |
| STAT_BATTERIELADUNG_GESAMT_EINH | string | Ah |
| STAT_BATTERIEENTLADUNG_GESAMT_WERT | unsigned long | PMINFO1[1] 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIEENTLADUNG_GESAMT_EINH | string | Ah |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_WERT | unsigned long | PMINFO1[2] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_A_B_WERT | unsigned long | PMINFO1[3] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_A_B_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_B_C_WERT | unsigned long | PMINFO1[4] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_B_C_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_C_D_WERT | unsigned long | PMINFO1[5] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_C_D_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_WERT | unsigned long | PMINFO1[6] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_EINH | string | h |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_WERT | unsigned long | PMINFO1[7] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_WERT | unsigned long | PMINFO1[8] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_WERT | unsigned long | PMINFO1[9] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_WERT | unsigned long | PMINFO1[10] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_WERT | unsigned long | PMINFO1[11] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_EINH | string | Minute |
| STAT_KM_STAND_AKTUELL_WERT | unsigned long | PMINFO1[12] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_AKTUELL_EINH | string | kilometer |
| STAT_KM_STAND_VOR_1_TAG_WERT | unsigned long | PMINFO1[13] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_1_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_2_TAG_WERT | unsigned long | PMINFO1[14] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_2_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_3_TAG_WERT | unsigned long | PMINFO1[15] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_3_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_4_TAG_WERT | unsigned long | PMINFO1[16] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_4_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_5_TAG_WERT | unsigned long | PMINFO1[17] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_5_TAG_EINH | string | kilometer |
| STAT_BATTERIETAUSCH_LETZTER_WERT | unsigned long | PMINFO1[18] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_BATTERIETAUSCH_LETZTER_EINH | string | kilometer |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_WERT | unsigned long | PMINFO1[19] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_EINH | string | kilometer |
| STAT_ANZAHL_LEERLAUFDREHZAHLANHEBUNG_EPS | unsigned long | PMINFO1[20] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ANZAHL_LEERLAUFDREHZAHLANHEBUNG_IBS | unsigned long | PMINFO1[20] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_BATTERIEENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_WERT | unsigned long | PMINFO1[22] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_BATTERIEENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_EINH | string | h |
| STAT_RUHESTROM_VOR_3_ZYKLEN_TEXT | string | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_3_ZYKLEN_WERT | int | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_2_ZYKLEN_TEXT | string | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_2_ZYKLEN_WERT | int | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_1_ZYKLUS_TEXT | string | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_1_ZYKLUS_WERT | int | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_AKTUELL_TEXT | string | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_AKTUELL_WERT | int | PMINFO1[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_7_ZYKLEN_TEXT | string | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_7_ZYKLEN_WERT | int | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_6_ZYKLEN_TEXT | string | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_6_ZYKLEN_WERT | int | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_5_ZYKLEN_TEXT | string | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_5_ZYKLEN_WERT | int | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_4_ZYKLEN_TEXT | string | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_4_ZYKLEN_WERT | int | PMINFO1[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_11_ZYKLEN_TEXT | string | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_11_ZYKLEN_WERT | int | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_10_ZYKLEN_TEXT | string | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_10_ZYKLEN_WERT | int | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_9_ZYKLEN_TEXT | string | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_9_ZYKLEN_WERT | int | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_8_ZYKLEN_TEXT | string | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_8_ZYKLEN_WERT | int | PMINFO1[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_15_ZYKLEN_TEXT | string | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_15_ZYKLEN_WERT | int | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_14_ZYKLEN_TEXT | string | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_14_ZYKLEN_WERT | int | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_13_ZYKLEN_TEXT | string | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_13_ZYKLEN_WERT | int | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_12_ZYKLEN_TEXT | string | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_12_ZYKLEN_WERT | int | PMINFO1[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_19_ZYKLEN_TEXT | string | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_19_ZYKLEN_WERT | int | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_18_ZYKLEN_TEXT | string | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_18_ZYKLEN_WERT | int | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_17_ZYKLEN_TEXT | string | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_17_ZYKLEN_WERT | int | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_16_ZYKLEN_TEXT | string | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_16_ZYKLEN_WERT | int | PMINFO1[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_23_ZYKLEN_TEXT | string | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_23_ZYKLEN_WERT | int | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_22_ZYKLEN_TEXT | string | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_22_ZYKLEN_WERT | int | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_21_ZYKLEN_TEXT | string | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_21_ZYKLEN_WERT | int | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_20_ZYKLEN_TEXT | string | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_20_ZYKLEN_WERT | int | PMINFO1[28] 4BIT_RUHESTROM |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[29] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_EIN_WERT | unsigned long | PMINFO1[29] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_1_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[30] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_1_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_1_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[30] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_1_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_2_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[31] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_2_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_2_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[31] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_2_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_3_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[32] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_3_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_3_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[32] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_3_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_4_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[33] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_4_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_4_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[33] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_4_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_5_TAG_WERT_MOTOR_AUS_WERT | unsigned long | PMINFO1[34] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_5_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_5_TAG_MOTOR_EIN_WERT | unsigned long | PMINFO1[34] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_5_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_RUHESTROM_AKTUELL_EINH | string | - |
| STAT_RUHESTROM_VOR_1_ZYKLUS_EINH | string | - |
| STAT_RUHESTROM_VOR_2_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_3_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_4_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_5_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_6_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_7_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_8_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_9_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_10_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_11_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_12_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_13_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_14_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_15_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_16_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_17_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_18_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_19_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_20_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_21_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_22_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_23_ZYKLEN_EINH | string | - |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-aep-info-2"></a>
### STATUS_SYSTEMCHECK_AEP_INFO_2

0x22DEBB STATUS_SYSTEMCHECK_AEP_INFO_2 Intelligenter Batteriesensor Bitfeld Pminfo2 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIE_KAPAZITAET_WERT | unsigned long | PMINFO2[0] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIE_KAPAZITAET_EINH | string | Ah |
| STAT_SOH_WERT | real | PMINFO2[1] 1BYTE_in_minus128bis127prozent   Einheit: % |
| STAT_SOH_EINH | string | percent |
| STAT_SOC_FIT_WERT | unsigned long | PMINFO2[2] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_SOC_FIT_EINH | string | percent |
| STAT_TEMP_SAISON_WERT | long | PMINFO2[3] 1BYTE_in_minus128bis127gradCelsius   Einheit: C |
| STAT_TEMP_SAISON_EINH | string | degreeC |
| STAT_ANZAHL_RUHESPANNUNGSAUSWERTUNGEN_OCV | unsigned long | PMINFO2[4] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_Q_SOC_AKTUELL_WERT | unsigned long | PMINFO2[5] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_AKTUELL_EINH | string | Ah |
| STAT_Q_SOC_VOR_1_TAG_WERT | unsigned long | PMINFO2[6] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_1_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_2_TAG_WERT | unsigned long | PMINFO2[7] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_2_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_3_TAG_WERT | unsigned long | PMINFO2[8] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_3_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_4_TAG_WERT | unsigned long | PMINFO2[9] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_4_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_5_TAG_WERT | unsigned long | PMINFO2[10] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_5_TAG_EINH | string | Ah |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_WERT | unsigned long | PMINFO2[11] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_WERT | unsigned long | PMINFO2[12] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_WERT | unsigned long | PMINFO2[13] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_WERT | unsigned long | PMINFO2[14] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_WERT | unsigned long | PMINFO2[15] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_WERT | unsigned long | PMINFO2[16] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_AKTUELL_WERT | unsigned long | PMINFO2[17] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_AKTUELL_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_WERT | unsigned long | PMINFO2[18] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_WERT | unsigned long | PMINFO2[19] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_WERT | unsigned long | PMINFO2[20] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_WERT | unsigned long | PMINFO2[21] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_WERT | unsigned long | PMINFO2[22] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_EINH | string | percent |
| STAT_BZE_DIAG_0 | unsigned long | PMINFO2[23] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_1 | unsigned long | PMINFO2[24] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_2 | unsigned long | PMINFO2[25] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_3 | unsigned long | PMINFO2[26] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_4 | unsigned long | PMINFO2[27] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-flashmode-acan-result"></a>
### STEUERN_FLASHMODE_ACAN_RESULT

Flashmode ACAN (0xF5)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FLASHMODE_ACAN | unsigned char | Flashmode ACAN ( 0 = aus, 1 = ein ) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-flashmode-acan-start"></a>
### STEUERN_FLASHMODE_ACAN_START

Flashmode ACAN (0xF5)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-flashmode-acan-stop"></a>
### STEUERN_FLASHMODE_ACAN_STOP

Flashmode ACAN (0xF5)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tsr-1-lesen"></a>
### STATUS_TSR_1_LESEN

Tele Service Daten auslesen STATUS_TSR_1_LESEN (0xE1)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LADUNG_AMP_STUNDEN_WERT | real | Wertebereich: 0 - 65535 Ah Die kumulierte Ladung für Ladevorgänge in Ah |
| STAT_LADUNG_AMP_STUNDEN_EINH | string | "Ah" |
| STAT_ENTLADUNG_AMP_STUNDEN_WERT | real | Wertebereich: 0 - 65535 Ah Die kumulierte Ladung für Entladevorgänge in Ah |
| STAT_ENTLADUNG_AMP_STUNDEN_EINH | string | "Ah" |
| STAT_ISOWIDERSTAND_EXT_AC_WERT | real | Wertebereich: 0 - 16383,75 kOhm Wert des externen AC Isolationswiderstands in kOhm |
| STAT_ISOWIDERSTAND_EXT_AC_EINH | string | "kOhm" |
| STAT_ISOWIDERSTAND_EXT_AC_WERT_QUAL | unsigned int | Qualifier-Norm Plausibilität des Isolationswiderstands |
| STAT_FEHLERBIT_SPANNUNG_OBEN | unsigned int | 0 = kein Fehler, 1 = Fehler Fehlerbit ob obere Spannungsgrenze überschritten wurde |
| STAT_FEHLERBIT_SPANNUNG_UNTEN | unsigned int | 0 = kein Fehler, 1 = Fehler Fehlerbit ob untere Spannungsgrenze überschritten wurde |
| STAT_ISOWIDERSTAND_EXT_DC_WERT | real | Wertebereich: 0 - 16383,75 kOhm Wert des externen DC Isolationswiderstands in kOhm |
| STAT_ISOWIDERSTAND_EXT_DC_EINH | string | "kOhm" |
| STAT_ISOWIDERSTAND_INT_DC_WERT | real | Wertebereich: 0 - 16383,75 kOhm Wert des internen DC Isolationswiderstands in kOhm |
| STAT_ISOWIDERSTAND_INT_DC_EINH | string | "kOhm" |
| STAT_ISOWIDERSTAND1_INT_DC_WERT | real | Wertebereich: 0 - 16383,75 kOhm Wert des internen DC Isolationswiderstands in kOhm |
| STAT_ISOWIDERSTAND1_INT_DC_EINH | string | "kOhm" |
| STAT_ISOWIDERSTAND_EXT_DC_WERT_QUAL | unsigned int | Qualifier-Norm Plausibilität des Isolationswiderstands |
| STAT_ISOWIDERSTAND_INT_DC_WERT_QUAL | unsigned int | Qualifier-Norm Plausibilität des Isolationswiderstands |
| STAT_ISOWIDERSTAND1_INT_DC_WERT_QUAL | unsigned int | Qualifier-Norm Plausibilität des Isolationswiderstands |
| STAT_ISOWIDERSTAND2_INT_DC_WERT | real | Wertebereich: 0 - 16383,75 kOhm Wert des internen DC Isolationswiderstands in kOhm |
| STAT_ISOWIDERSTAND2_INT_DC_EINH | string | "kOhm" |
| STAT_ALTERUNG_INNENWIDERSTAND_WERT | real | Wertebereich: 0 - 100 % Innenwiderstandsansteige in % bezogen auf den Neuwert |
| STAT_ALTERUNG_INNENWIDERSTAND_EINH | string | "%" |
| STAT_ALTERUNG_KAPAZITAET_WERT | real | Wertebereich: 0 - 100 % Kapazitaetsverliust in % bezogen auf die Nennkapazitaet |
| STAT_ALTERUNG_KAPAZITAET_EINH | string | "%" |
| STAT_MAXIMALE_TEMPERATUR_WERT | real | Wertebereich: -50 - 204 °C Minimale jemals gemessene Temperatur |
| STAT_MAXIMALE_TEMPERATUR_EINH | string | "°C" |
| STAT_MINIMALE_TEMPERATUR_WERT | real | Wertebereich: -50 - 204 °C Maximale jemals gemessene Temperatur |
| STAT_MINIMALE_TEMPERATUR_EINH | string | "°C" |
| STAT_ISOWIDERSTAND2_INT_DC_WERT_QUAL | unsigned int | Qualifier-Norm Plausibilität des Isolationswiderstands |
| STAT_FEHLERBIT_T_OBEN | unsigned int | 0 = kein Fehler, 1 = Fehler Fehlerbit ob obere Temperaturgrenze überschritten wurde |
| STAT_FEHLERBIT_T_OBEN_BETRIEB | unsigned int | 0 = kein Fehler, 1 = Fehler Fehlerbit ob obere Temperaturgrenze im HV on überschritten wurde |
| STAT_FAKTOR_RP_ENTLADE_WERT | real | Wertebereich: 0 - 0,1 Ohm paralleler Entladewiderstan |
| STAT_FAKTOR_RP_ENTLADE_EINH | string | "Ohm" |
| STAT_FAKTOR_RP_LADE_WERT | real | Wertebereich: 0 - 0,1 Ohm paralleler Ladewiderstan |
| STAT_FAKTOR_RP_LADE_EINH | string | "Ohm" |
| STAT_FAKTOR_CP_ENTLADE_WERT | real | Wertebereich: 0 - 25500 F parallele Entladekapazität |
| STAT_FAKTOR_CP_ENTLADE_EINH | string | "F" |
| STAT_FAKTOR_CP_LADE_WERT | real | Wertebereich: 0 - 25500 F parallele Ladekapazität |
| STAT_FAKTOR_CP_LADE_EINH | string | "F" |
| STAT_FEHLERBIT_T_UNTEN | unsigned int | 0 = kein Fehler, 1 = Fehler Fehlerbit ob untere Temperaturgrenze überschritten wurde |
| STAT_FEHLERBIT_T_UNTEN_BETRIEB | unsigned int | 0 = kein Fehler, 1 = Fehler Fehlerbit ob untere Temperaturgrenze im HV on überschritten wurde |
| STAT_FAKTOR_RS_ENTLADE_WERT | real | Wertebereich: 0 - 0,1 Ohm serieller Entladewiderstand |
| STAT_FAKTOR_RS_ENTLADE_EINH | string | "Ohm" |
| STAT_FAKTOR_RS_LADE_WERT | real | Wertebereich: 0 - 0,1 Ohm serieller Ladewiderstand |
| STAT_FAKTOR_RS_LADE_EINH | string | "Ohm" |
| STAT_KAPAZITAET_WERT | real | Wertebereich: 0 - 65535 Wh Ist-Kapazität |
| STAT_KAPAZITAET_EINH | string | "Wh" |
| STAT_ZEIT_POWER_DCHG_1_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Leistungsklasse 1 für Entladevorgänge (0 - 100 W/cell) |
| STAT_ZEIT_POWER_DCHG_1_EINH | string | "min" |
| STAT_ZEIT_POWER_DCHG_2_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Leistungsklasse 2 für Entladevorgänge (100 - 200 W/cell) |
| STAT_ZEIT_POWER_DCHG_2_EINH | string | "min" |
| STAT_ZEIT_POWER_DCHG_3_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Leistungsklasse 3 für Entladevorgänge (200 - 300 W/cell) |
| STAT_ZEIT_POWER_DCHG_3_EINH | string | "min" |
| STAT_ZEIT_POWER_DCHG_4_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Leistungsklasse 4 für Entladevorgänge (300 - 400 W/cell) |
| STAT_ZEIT_POWER_DCHG_4_EINH | string | "min" |
| STAT_ZEIT_POWER_DCHG_5_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Leistungsklasse 5)für Entladevorgänge (400 - 500 W/cell) |
| STAT_ZEIT_POWER_DCHG_5_EINH | string | "min" |
| STAT_ZEIT_POWER_DCHG_6_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Leistungsklasse 6 für Entladevorgänge (500 - 600 W/cell) |
| STAT_ZEIT_POWER_DCHG_6_EINH | string | "min" |
| STAT_ZEIT_POWER_CHG_1_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Leistungsklasse 1 für Ladevorgänge (0 - 100 W/cell) |
| STAT_ZEIT_POWER_CHG_1_EINH | string | "min" |
| STAT_ZEIT_POWER_CHG_2_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Leistungsklasse 2 für Ladevorgänge (100 - 200 W/cell) |
| STAT_ZEIT_POWER_CHG_2_EINH | string | "min" |
| STAT_ZEIT_POWER_CHG_3_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Leistungsklasse 3 für Ladevorgänge (200 - 300 W/cell) |
| STAT_ZEIT_POWER_CHG_3_EINH | string | "min" |
| STAT_ZEIT_POWER_CHG_4_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Leistungsklasse 4 für Ladevorgänge (300 - 400 W/cell) |
| STAT_ZEIT_POWER_CHG_4_EINH | string | "min" |
| STAT_ZEIT_POWER_CHG_5_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Leistungsklasse 5 für Ladevorgänge (400 - 500 W/cell) |
| STAT_ZEIT_POWER_CHG_5_EINH | string | "min" |
| STAT_ZEIT_POWER_CHG_6_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Leistungsklasse 6 für Ladevorgänge (500 - 600 W/cell) |
| STAT_ZEIT_POWER_CHG_6_EINH | string | "min" |
| STAT_ZEIT_SOC_1_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in SOC-Klasse 1 (0 %- 30%) |
| STAT_ZEIT_SOC_1_EINH | string | "min" |
| STAT_ZEIT_SOC_2_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in SOC-Klasse 2 (30% - 40 %) |
| STAT_ZEIT_SOC_2_EINH | string | "min" |
| STAT_ZEIT_SOC_3_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in SOC-Klasse 3 (40% - 50%) |
| STAT_ZEIT_SOC_3_EINH | string | "min" |
| STAT_ZEIT_SOC_4_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in SOC-Klasse 4 (50 % - 55%) |
| STAT_ZEIT_SOC_4_EINH | string | "min" |
| STAT_ZEIT_SOC_5_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in SOC-Klasse 5 (55%-50%) |
| STAT_ZEIT_SOC_5_EINH | string | "min" |
| STAT_ZEIT_SOC_6_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in SOC-Klasse 6 (60 % -65%) |
| STAT_ZEIT_SOC_6_EINH | string | "min" |
| STAT_ZEIT_SOC_7_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in SOC-Klasse 7 (65 % -70%) |
| STAT_ZEIT_SOC_7_EINH | string | "min" |
| STAT_ZEIT_SOC_8_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in SOC-Klasse 8 (70 % -75%) |
| STAT_ZEIT_SOC_8_EINH | string | "min" |
| STAT_ZEIT_SOC_9_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in SOC-Klasse 9 (75 % -90%) |
| STAT_ZEIT_SOC_9_EINH | string | "min" |
| STAT_ZEIT_SOC_10_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in SOC-Klasse 10 (90 % -100%) |
| STAT_ZEIT_SOC_10_EINH | string | "min" |
| STAT_ZEIT_TEMP_HSOFFEN_1_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 1 ( &lt; 10°C) bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_1_EINH | string | "min" |
| STAT_ZEIT_TEMP_HSOFFEN_2_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 2 (10°C - 20°C) bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_2_EINH | string | "min" |
| STAT_ZEIT_TEMP_HSOFFEN_3_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 3 (20°C - 30°C) bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_3_EINH | string | "min" |
| STAT_ZEIT_TEMP_HSOFFEN_4_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 4 (30°C - 35°C) bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_4_EINH | string | "min" |
| STAT_ZEIT_TEMP_HSOFFEN_5_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 5 (35°C - 40°C) bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_5_EINH | string | "min" |
| STAT_ZEIT_TEMP_HSOFFEN_6_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 6 (40°C - 45°C) bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_6_EINH | string | "min" |
| STAT_ZEIT_TEMP_HSOFFEN_7_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 7 (45°C - 50°C) bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_7_EINH | string | "min" |
| STAT_ZEIT_TEMP_HSOFFEN_8_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 8 (50°C - 55°C) bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_8_EINH | string | "min" |
| STAT_ZEIT_TEMP_HSOFFEN_9_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 9 (55°C - 60°C) bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_9_EINH | string | "min" |
| STAT_ZEIT_TEMP_HSOFFEN_10_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 10 (&gt;  60°C) bei geöffneten Hauptschaltern |
| STAT_ZEIT_TEMP_HSOFFEN_10_EINH | string | "min" |
| STAT_ZEIT_TEMP_TOTAL_1_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 1 ( &lt; 10°C) bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_1_EINH | string | "min" |
| STAT_ZEIT_TEMP_TOTAL_2_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 2 (10°C - 20°C) bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_2_EINH | string | "min" |
| STAT_ZEIT_TEMP_TOTAL_3_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 3 (20°C - 30°C) bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_3_EINH | string | "min" |
| STAT_ZEIT_TEMP_TOTAL_4_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 4 (30°C - 35°C) bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_4_EINH | string | "min" |
| STAT_ZEIT_TEMP_TOTAL_5_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 5 (35°C - 40°C) bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_5_EINH | string | "min" |
| STAT_ZEIT_TEMP_TOTAL_6_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 6 (40°C - 45°C) bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_6_EINH | string | "min" |
| STAT_ZEIT_TEMP_TOTAL_7_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 7 (45°C - 50°C) bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_7_EINH | string | "min" |
| STAT_ZEIT_TEMP_TOTAL_8_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 8 (50°C - 55°C) bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_8_EINH | string | "min" |
| STAT_ZEIT_TEMP_TOTAL_9_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 9 (55°C - 60°C) bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_9_EINH | string | "min" |
| STAT_ZEIT_TEMP_TOTAL_10_WERT | real | Wertebereich: 0 - 655350 min Zeit in Minuten in Temperaturklasse 10 (&gt;  60°C) bei geöffneten und geschlossenen Hauptschaltern |
| STAT_ZEIT_TEMP_TOTAL_10_EINH | string | "min" |
| STAT_SUM_OF_SOC_CHARGE_5_10_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Ladehüben im Bereich 5 - 10 % |
| STAT_SUM_OF_SOC_CHARGE_5_10_EINH | string | "-" |
| STAT_SUM_OF_SOC_CHARGE_10_15_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Ladehüben im Bereich 10 - 15 % |
| STAT_SUM_OF_SOC_CHARGE_10_15_EINH | string | "-" |
| STAT_SUM_OF_SOC_CHARGE_15_20_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Ladehüben im Bereich 15 - 20 % |
| STAT_SUM_OF_SOC_CHARGE_15_20_EINH | string | "-" |
| STAT_SUM_OF_SOC_CHARGE_20_25_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Ladehüben im Bereich 20 - 25 % |
| STAT_SUM_OF_SOC_CHARGE_20_25_EINH | string | "-" |
| STAT_SUM_OF_SOC_CHARGE_25_30_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Ladehüben im Bereich 25 - 30 % |
| STAT_SUM_OF_SOC_CHARGE_25_30_EINH | string | "-" |
| STAT_SUM_OF_SOC_CHARGE_30_35_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Ladehüben im Bereich 30 - 35 % |
| STAT_SUM_OF_SOC_CHARGE_30_35_EINH | string | "-" |
| STAT_SUM_OF_SOC_CHARGE_35_40_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Ladehüben im Bereich 35 - 40 % |
| STAT_SUM_OF_SOC_CHARGE_35_40_EINH | string | "-" |
| STAT_SUM_OF_SOC_CHARGE_40_45_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Ladehüben im Bereich 40 - 45 % |
| STAT_SUM_OF_SOC_CHARGE_40_45_EINH | string | "-" |
| STAT_SUM_OF_SOC_CHARGE_45_50_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Ladehüben im Bereich 45 - 50 % |
| STAT_SUM_OF_SOC_CHARGE_45_50_EINH | string | "-" |
| STAT_SUM_OF_SOC_CHARGE_50_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Ladehüben im Bereich &gt; 50 % |
| STAT_SUM_OF_SOC_CHARGE_50_EINH | string | "-" |
| STAT_SUM_OF_SOC_DISCHARGE_5_10_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Entladehüben im Bereich 5 - 10 % |
| STAT_SUM_OF_SOC_DISCHARGE_5_10_EINH | string | "-" |
| STAT_SUM_OF_SOC_DISCHARGE_10_15_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Entladehüben im Bereich 10 - 15 % |
| STAT_SUM_OF_SOC_DISCHARGE_10_15_EINH | string | "-" |
| STAT_SUM_OF_SOC_DISCHARGE_15_20_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Entladehüben im Bereich 15 - 20 % |
| STAT_SUM_OF_SOC_DISCHARGE_15_20_EINH | string | "-" |
| STAT_SUM_OF_SOC_DISCHARGE_20_25_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Entladehüben im Bereich 20 - 25 % |
| STAT_SUM_OF_SOC_DISCHARGE_20_25_EINH | string | "-" |
| STAT_SUM_OF_SOC_DISCHARGE_25_30_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Entladehüben im Bereich 25 - 30 % |
| STAT_SUM_OF_SOC_DISCHARGE_25_30_EINH | string | "-" |
| STAT_SUM_OF_SOC_DISCHARGE_30_35_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Entladehüben im Bereich 30 - 35 % |
| STAT_SUM_OF_SOC_DISCHARGE_30_35_EINH | string | "-" |
| STAT_SUM_OF_SOC_DISCHARGE_35_40_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Entladehüben im Bereich 35 - 40 % |
| STAT_SUM_OF_SOC_DISCHARGE_35_40_EINH | string | "-" |
| STAT_SUM_OF_SOC_DISCHARGE_40_45_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Entladehüben im Bereich 40 - 45 % |
| STAT_SUM_OF_SOC_DISCHARGE_40_45_EINH | string | "-" |
| STAT_SUM_OF_SOC_DISCHARGE_45_50_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Entladehüben im Bereich 45 - 50 % |
| STAT_SUM_OF_SOC_DISCHARGE_45_50_EINH | string | "-" |
| STAT_SUM_OF_SOC_DISCHARGE_50_WERT | real | Wertebereich: 0 - 2550 - Anzahl an Entladehüben im Bereich &gt; 50 % |
| STAT_SUM_OF_SOC_DISCHARGE_50_EINH | string | "-" |
| STAT_I_HISTO_KLASSE8_WERT | real | Wertebereich: 0 - 655350 min Zeit in s für die i &lt;= -160 A |
| STAT_I_HISTO_KLASSE8_EINH | string | "min" |
| STAT_I_HISTO_KLASSE7_WERT | real | Wertebereich: 0 - 655350 min Zeit in s für die -160 A &lt; i &lt;= -80 A |
| STAT_I_HISTO_KLASSE7_EINH | string | "min" |
| STAT_I_HISTO_KLASSE6_WERT | real | Wertebereich: 0 - 655350 min Zeit in s für die -80 A &lt; i &lt;= -5 A |
| STAT_I_HISTO_KLASSE6_EINH | string | "min" |
| STAT_I_HISTO_KLASSE5_WERT | real | Wertebereich: 0 - 655350 min Zeit in s für die -5 A &lt; i &lt;= 0 A |
| STAT_I_HISTO_KLASSE5_EINH | string | "min" |
| STAT_I_HISTO_KLASSE4_WERT | real | Wertebereich: 0 - 655350 min Zeit in s für die 0 A &lt; i &lt;= 5 A |
| STAT_I_HISTO_KLASSE4_EINH | string | "min" |
| STAT_I_HISTO_KLASSE3_WERT | real | Wertebereich: 0 - 655350 min Zeit in s für die 5 A &lt; i &lt;= 80 A |
| STAT_I_HISTO_KLASSE3_EINH | string | "min" |
| STAT_I_HISTO_KLASSE2_WERT | real | Wertebereich: 0 - 655350 min Zeit in s für die 80 A &lt; i &lt;= 160 A |
| STAT_I_HISTO_KLASSE2_EINH | string | "min" |
| STAT_I_HISTO_KLASSE1_WERT | real | Wertebereich: 0 - 655350 min Zeit in s für die 160 A &lt; i |
| STAT_I_HISTO_KLASSE1_EINH | string | "min" |
| STAT_DELTA_SOC_MAX_WERT | real | Wertebereich: 0 - 25,5 % Maximaler jemals gemessnener delta SOC zwischen den Zellen |
| STAT_DELTA_SOC_MAX_EINH | string | "%" |
| STAT_SYM_DELTASOC_1_WERT | real | Wertebereich: 0 - 25,5 % Maximaler delta SOC zwischen den Zellen während des letzten Fahrzyklus |
| STAT_SYM_DELTASOC_1_EINH | string | "%" |
| STAT_SYM_DELTASOC_2_WERT | real | Wertebereich: 0 - 25,5 % Maximaler delta SOC zwischen den Zellen während des voletzten Fahrzyklus |
| STAT_SYM_DELTASOC_2_EINH | string | "%" |
| STAT_SYM_DELTASOC_3_WERT | real | Wertebereich: 0 - 25,5 % Maximaler delta SOC zwischen den Zellen während des vorvoletzten Fahrzyklus |
| STAT_SYM_DELTASOC_3_EINH | string | "%" |
| STAT_SYM_DELTASOC_4_WERT | real | Wertebereich: 0 - 25,5 % Maximaler delta SOC zwischen den Zellen während des vorvorvoletzten Fahrzyklus |
| STAT_SYM_DELTASOC_4_EINH | string | "%" |
| STAT_SYM_DELTASOC_5_WERT | real | Wertebereich: 0 - 25,5 % Maximaler delta SOC zwischen den Zellen während des vorvorvorvoletzten Fahrzyklus |
| STAT_SYM_DELTASOC_5_EINH | string | "%" |
| STAT_SYM_DELTASOC_6_WERT | real | Wertebereich: 0 - 25,5 % Maximaler delta SOC zwischen den Zellen während des vorvorvorvorvoletzten Fahrzyklus |
| STAT_SYM_DELTASOC_6_EINH | string | "%" |
| STAT_SYMMETRIERHAEUFIGKEIT_WERT | real | Wertebereich: 0 - 2550 - Prozentualer Anteil des Balancing an der HV OFF time |
| STAT_SYMMETRIERHAEUFIGKEIT_EINH | string | "-" |
| STAT_KUMULIERTE_HEIZUNGSDAUER_WERT | real | Wertebereich: 0 - 655350 min Zeit in der eine Heizanforderung vorliegt |
| STAT_KUMULIERTE_HEIZUNGSDAUER_EINH | string | "min" |
| STAT_KUMULIERTE_KUEHLUNGSDAUER_WERT | real | Wertebereich: 0 - 655350 min Zeit in der eine Kühlanforderung vorliegt |
| STAT_KUMULIERTE_KUEHLUNGSDAUER_EINH | string | "min" |
| STAT_KUMULIERTE_ZEIT_SCHUETZE_OFFEN_WERT | real | Wertebereich: 0 - 655350 min Zeitdauer in der die Schütze offen sind (Schlafphasen der SME werden mit einberechnet) |
| STAT_KUMULIERTE_ZEIT_SCHUETZE_OFFEN_EINH | string | "min" |
| STAT_KUMULIERTE_LAUFZEIT_WASSERPUMPE_HEIZUNG_WERT | real | Wertebereich: 0 - 655350 min Zeit in der eine Heizanforderung vorliegt |
| STAT_KUMULIERTE_LAUFZEIT_WASSERPUMPE_HEIZUNG_EINH | string | "min" |
| STAT_KUMULIERTE_LAUFZEIT_WASSERPUMPE_KUEHLUNG_WERT | real | Wertebereich: 0 - 655350 min Zeit in der die Pumpe läuft und in der nicht geheizt wird |
| STAT_KUMULIERTE_LAUFZEIT_WASSERPUMPE_KUEHLUNG_EINH | string | "min" |
| STAT_KUMULIERTE_ZEIT_SCHUETZE_GESCHLOSSEN_WERT | real | Wertebereich: 0 - 655350 min Zeitdauer in der die Schütze geschlossen sind |
| STAT_KUMULIERTE_ZEIT_SCHUETZE_GESCHLOSSEN_EINH | string | "min" |
| STAT_MITTLERE_ANSTEUERUNG_WASSERPUMPE_WERT | real | Wertebereich: 0 - 100 % Mittlere Pumpengeschwindigkeit in Betrieb |
| STAT_MITTLERE_ANSTEUERUNG_WASSERPUMPE_EINH | string | "%" |
| STAT_HAEUFIGKEIT_NUTZUNG_VORKONDITIONIERUNG_WERT | unsigned int | Wertebereich: 0 - 4095 - Zähler wie oft eine Vorkonditionierung gewünscht wird |
| STAT_HAEUFIGKEIT_NUTZUNG_VORKONDITIONIERUNG_EINH | string | "-" |
| STAT_STARTTEMPERATUR_VORKONDITIONIERUNG_1_WERT | real | Wertebereich: -50 - 204 °C Speichertemperatur zu beginn der letzten Vorkonditionierung |
| STAT_STARTTEMPERATUR_VORKONDITIONIERUNG_1_EINH | string | "°C" |
| STAT_STARTTEMPERATUR_VORKONDITIONIERUNG_2_WERT | real | Wertebereich: -50 - 204 °C Speichertemperatur zu beginn der vorletzten Vorkonditionierung |
| STAT_STARTTEMPERATUR_VORKONDITIONIERUNG_2_EINH | string | "°C" |
| STAT_STARTTEMPERATUR_VORKONDITIONIERUNG_3_WERT | real | Wertebereich: -50 - 204 °C Speichertemperatur zu beginn der vorvorletzten Vorkonditionierung |
| STAT_STARTTEMPERATUR_VORKONDITIONIERUNG_3_EINH | string | "°C" |
| STAT_STARTTEMPERATUR_VORKONDITIONIERUNG_4_WERT | real | Wertebereich: -50 - 204 °C Speichertemperatur zu beginn der vorvorvorletzten Vorkonditionierung |
| STAT_STARTTEMPERATUR_VORKONDITIONIERUNG_4_EINH | string | "°C" |
| STAT_STARTTEMPERATUR_VORKONDITIONIERUNG_5_WERT | real | Wertebereich: -50 - 204 °C Speichertemperatur zu beginn der vorvorvorvorletzten Vorkonditionierung |
| STAT_STARTTEMPERATUR_VORKONDITIONIERUNG_5_EINH | string | "°C" |
| STAT_STARTTEMPERATUR_VORKONDITIONIERUNG_6_WERT | real | Wertebereich: -50 - 204 °C Speichertemperatur zu beginn der vorvorvorvorvorletzten Vorkonditionierung |
| STAT_STARTTEMPERATUR_VORKONDITIONIERUNG_6_EINH | string | "°C" |
| STAT_SPEICHERTEMPERATUR_VOR_ABFAHRT_1_WERT | real | Wertebereich: -50 - 204 °C Speichertemperatur vor dem letzten HV on |
| STAT_SPEICHERTEMPERATUR_VOR_ABFAHRT_1_EINH | string | "°C" |
| STAT_SPEICHERTEMPERATUR_VOR_ABFAHRT_2_WERT | real | Wertebereich: -50 - 204 °C Speichertemperatur vor dem vorletzten HV on |
| STAT_SPEICHERTEMPERATUR_VOR_ABFAHRT_2_EINH | string | "°C" |
| STAT_SPEICHERTEMPERATUR_VOR_ABFAHRT_3_WERT | real | Wertebereich: -50 - 204 °C Speichertemperatur vor dem vorvorletzten HV on |
| STAT_SPEICHERTEMPERATUR_VOR_ABFAHRT_3_EINH | string | "°C" |
| STAT_SPEICHERTEMPERATUR_VOR_ABFAHRT_4_WERT | real | Wertebereich: -50 - 204 °C Speichertemperatur vor dem vorvorvorletzten HV on |
| STAT_SPEICHERTEMPERATUR_VOR_ABFAHRT_4_EINH | string | "°C" |
| STAT_SPEICHERTEMPERATUR_VOR_ABFAHRT_5_WERT | real | Wertebereich: -50 - 204 °C Speichertemperatur vor dem vorvorvorvorletzten HV on |
| STAT_SPEICHERTEMPERATUR_VOR_ABFAHRT_5_EINH | string | "°C" |
| STAT_SPEICHERTEMPERATUR_VOR_ABFAHRT_6_WERT | real | Wertebereich: -50 - 204 °C Speichertemperatur vor dem vorvorvorvorvorletzten HV on |
| STAT_SPEICHERTEMPERATUR_VOR_ABFAHRT_6_EINH | string | "°C" |
| STAT_LADEZEIT_1_WERT | real | Wertebereich: 0 - 655350 min Dauer des letzten Ladevorgangs |
| STAT_LADEZEIT_1_EINH | string | "min" |
| STAT_LADEZEIT_2_WERT | real | Wertebereich: 0 - 655350 min Dauer des vorletzten Ladevorgangs |
| STAT_LADEZEIT_2_EINH | string | "min" |
| STAT_LADEZEIT_3_WERT | real | Wertebereich: 0 - 655350 min Dauer des vorvorletzten Ladevorgangs |
| STAT_LADEZEIT_3_EINH | string | "min" |
| STAT_LADEZEIT_4_WERT | real | Wertebereich: 0 - 655350 min Dauer des vorvorvorletzten Ladevorgangs |
| STAT_LADEZEIT_4_EINH | string | "min" |
| STAT_LADEZEIT_5_WERT | real | Wertebereich: 0 - 655350 min Dauer des vorvorvorvorletzten Ladevorgangs |
| STAT_LADEZEIT_5_EINH | string | "min" |
| STAT_LADEZEIT_6_WERT | real | Wertebereich: 0 - 655350 min Dauer des vorvorvorvorvorletzten Ladevorgangs |
| STAT_LADEZEIT_6_EINH | string | "min" |
| STAT_LADE_END_SOC_AVG_WERT | real | Wertebereich: 0 - 100 % Durchschnittlicher SOC beim Ladeende |
| STAT_LADE_END_SOC_AVG_EINH | string | "%" |
| STAT_LADE_END_SOC_MAX_WERT | real | Wertebereich: 0 - 100 % Maximaler SOC über Lebenszeit beim Ladeende |
| STAT_LADE_END_SOC_MAX_EINH | string | "%" |
| STAT_LADE_END_SOC_MIN_WERT | real | Wertebereich: 0 - 100 % Minimaler SOC über Lebenszeit beim Ladeende |
| STAT_LADE_END_SOC_MIN_EINH | string | "%" |
| STAT_ENERGIEPROGNOSE_1_WERT | real | Wertebereich: 0 - 51000 Wh Prognostizierte Energie beim HV_ON - prognostizierte Energie beim HV_OFF |
| STAT_ENERGIEPROGNOSE_1_EINH | string | "Wh" |
| STAT_ENERGIEPROGNOSE_2_WERT | real | Wertebereich: 0 - 51000 Wh Tatsächlich entnommene Energie zwischen HV_ON und HV_OFF |
| STAT_ENERGIEPROGNOSE_2_EINH | string | "Wh" |
| STAT_LADEDAUER_VS_LADEZEITPROGNOSE_AVG_WERT | real | Wertebereich: 0 - 100 % Durschnitt der Zeitdifferenz von prognostizierter und tatsächlicher Ladezeit |
| STAT_LADEDAUER_VS_LADEZEITPROGNOSE_AVG_EINH | string | "%" |
| STAT_LADEDAUER_VS_LADEZEITPROGNOSE_MAX_WERT | real | Wertebereich: 0 - 100 % Maximale Differenz der tatsächlichen Ladezeit und der Prognose |
| STAT_LADEDAUER_VS_LADEZEITPROGNOSE_MAX_EINH | string | "%" |
| STAT_LADEDAUER_VS_LADEZEITPROGNOSE_MIN_WERT | real | Wertebereich: 0 - 100 % Minimale Differenz der tatsächlichen Ladezeit und der Prognose |
| STAT_LADEDAUER_VS_LADEZEITPROGNOSE_MIN_EINH | string | "%" |
| STAT_STREUUNG_INNENWIDERSTAND_AVG_WERT | real | Wertebereich: 0 - 10 - Durchschnitt der Streuung des Innenwiderstandes |
| STAT_STREUUNG_INNENWIDERSTAND_AVG_EINH | string | "-" |
| STAT_STREUUNG_INNENWIDERSTAND_MAX_WERT | real | Wertebereich: 0 - 10 - Maximum der Streuung des Innenwiderstandes |
| STAT_STREUUNG_INNENWIDERSTAND_MAX_EINH | string | "-" |
| STAT_STREUUNG_INNENWIDERSTAND_MIN_WERT | real | Wertebereich: 0 - 10 - Minimum der Streuung des Innenwiderstandes |
| STAT_STREUUNG_INNENWIDERSTAND_MIN_EINH | string | "-" |
| STAT_FEHLERBIT_1 | unsigned int | 0 = kein Fehler, 1 = Fehler 01 ACAN_Comm |
| STAT_FEHLERBIT_2 | unsigned int | 0 = kein Fehler, 1 = Fehler 02 MainSw_Driver_Err |
| STAT_FEHLERBIT_3 | unsigned int | 0 = kein Fehler, 1 = Fehler 03 HW_Monitoring_CSC |
| STAT_FEHLERBIT_4 | unsigned int | 0 = kein Fehler, 1 = Fehler 04 ServiceDisconnect |
| STAT_FEHLERBIT_5 | unsigned int | 0 = kein Fehler, 1 = Fehler 05 Crash_Handling |
| STAT_FEHLERBIT_6 | unsigned int | 0 = kein Fehler, 1 = Fehler 06 Terminal_Monitoring |
| STAT_FEHLERBIT_7 | unsigned int | 0 = kein Fehler, 1 = Fehler 07 Temp_Management |
| STAT_FEHLERBIT_8 | unsigned int | 0 = kein Fehler, 1 = Fehler 08 Current_Monitoring |
| STAT_FEHLERBIT_9 | unsigned int | 0 = kein Fehler, 1 = Fehler 09 HV_Voltage_Monitoring |
| STAT_FEHLERBIT_10 | unsigned int | 0 = kein Fehler, 1 = Fehler 10 HVIL_Monitoring |
| STAT_FEHLERBIT_11 | unsigned int | 0 = kein Fehler, 1 = Fehler 11 Temperature_Monitoring |
| STAT_FEHLERBIT_12 | unsigned int | 0 = kein Fehler, 1 = Fehler 12 PreCharge_Monitoring |
| STAT_FEHLERBIT_13 | unsigned int | 0 = kein Fehler, 1 = Fehler 13 Signal_Plausibility |
| STAT_FEHLERBIT_14 | unsigned int | 0 = kein Fehler, 1 = Fehler 14 Modul_Temp |
| STAT_FEHLERBIT_15 | unsigned int | 0 = kein Fehler, 1 = Fehler 15 State_Monitoring |
| STAT_FEHLERBIT_16 | unsigned int | 0 = kein Fehler, 1 = Fehler 16 Error_Management |
| STAT_FEHLERBIT_17 | unsigned int | 0 = kein Fehler, 1 = Fehler 17 Safety_Concept |
| STAT_FEHLERBIT_18 | unsigned int | 0 = kein Fehler, 1 = Fehler 18 Isolation_Monitoring_mst |
| STAT_FEHLERBIT_19 | unsigned int | 0 = kein Fehler, 1 = Fehler 19 Isolation_Monitoring_sl1 |
| STAT_FEHLERBIT_20 | unsigned int | 0 = kein Fehler, 1 = Fehler 20 Isolation_Monitoring_sl2 |
| STAT_FEHLERBIT_21 | unsigned int | 0 = kein Fehler, 1 = Fehler 21 Contactor_Monitoring_mst |
| STAT_FEHLERBIT_22 | unsigned int | 0 = kein Fehler, 1 = Fehler 22 Contactor_Monitoring_sl1 |
| STAT_FEHLERBIT_23 | unsigned int | 0 = kein Fehler, 1 = Fehler 23 Contactor_Monitoring_sl2 |
| STAT_FEHLERBIT_24 | unsigned int | 0 = kein Fehler, 1 = Fehler 24 HW_Reisleine |
| STAT_FEHLERBIT_25 | unsigned int | 0 = kein Fehler, 1 = Fehler 25 MainSw_El_Diag |
| STAT_FEHLERBIT_26 | unsigned int | 0 = kein Fehler, 1 = Fehler 26 Init_Err_Slave |
| STAT_FEHLERBIT_27 | unsigned int | 0 = kein Fehler, 1 = Fehler 27 Supply_Errs |
| STAT_FEHLERBIT_28 | unsigned int | 0 = kein Fehler, 1 = Fehler 28 RTC_Errs |
| STAT_FEHLERBIT_29 | unsigned int | 0 = kein Fehler, 1 = Fehler 29 Cooling_El_Diag |
| STAT_FEHLERBIT_30 | unsigned int | 0 = kein Fehler, 1 = Fehler 30 RAM_ROM_EEPROM |
| STAT_FEHLERBIT_31 | unsigned int | 0 = kein Fehler, 1 = Fehler 31 Isens_Diag |
| STAT_FEHLERBIT_32 | unsigned int | 0 = kein Fehler, 1 = Fehler 32 IsoMeas_Err |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-start-laden-start"></a>
### STEUERN_START_LADEN_START

Ladestart anfordern STEUERN_START_LADEN (0xC0)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-stop-laden-stop"></a>
### STEUERN_STOP_LADEN_STOP

Ladestop anfordern STEUERN_STOP_LADEN (0xC100)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tsr-2-lesen"></a>
### STATUS_TSR_2_LESEN

Tele Service Daten auslesen STATUS_TSR_2_LESEN (0xE2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BSZ_WERT | unsigned long | Betriebsstundenzähler gesamt |
| STAT_BSZ_EINH | string | "s" |
| STAT_BSZFAHRB_WERT | unsigned long | Betriebsstundenzähler fahrbereit |
| STAT_BSZFAHRB_EINH | string | "%" |
| STAT_BSZKL15_WERT | real | Betriebsstundenzähler Kl15Ein |
| STAT_BSZKL15_EINH | string | "%" |
| STAT_BAREKU_WERT | real | Zeitanteil im Reku-Betrieb |
| STAT_BAREKU_EINH | string | "%" |
| STAT_BASEG_WERT | real | Zeitanteil im Segel-Betrieb |
| STAT_BASEG_EINH | string | "%" |
| STAT_BAANTR_WERT | real | Zeitanteil im Antriebs-Betrieb |
| STAT_BAANTR_EINH | string | "%" |
| STAT_BAREKU_ENGY_BATT_WERT | real | Energie im Reku-Betrieb Batterie |
| STAT_BAREKU_ENGY_BATT_EINH | string | "kWh" |
| STAT_BAANTR_ENGY_BATT_WERT | real | Energie im Antriebs-Betrieb Batterie |
| STAT_BAANTR_ENGY_BATT_EINH | string | "kWh" |
| STAT_BAREKU_ENGY_EM_WERT | real | Energie im Reku-Betrieb EM |
| STAT_BAREKU_ENGY_EM_EINH | string | "kWh" |
| STAT_BAANTR_ENGY_EM_WERT | real | Energie im Antriebs-Betrieb EM |
| STAT_BAANTR_ENGY_EM_EINH | string | "kWh" |
| STAT_SPORT_WERT | real | Zeitanteil für Sport-Betrieb |
| STAT_SPORT_EINH | string | "%" |
| STAT_NORM_WERT | real | Zeitanteil für Normal-Betrieb |
| STAT_NORM_EINH | string | "%" |
| STAT_ECO_WERT | real | Zeitanteil für ECO-Betrieb |
| STAT_ECO_EINH | string | "%" |
| STAT_ECOP_WERT | real | Zeitanteil für ECO+ -Betrieb |
| STAT_ECOP_EINH | string | "%" |
| STAT_TRIGG90_WERT | unsigned int | Zähler Trigger Begrenzung 90kW |
| STAT_TRIGG90_EINH | string | "-" |
| STAT_DEG90_WERT | real | Zähler Begrenzung 90kW bezogen Trigger |
| STAT_DEG90_EINH | string | "%" |
| STAT_DEG0_WERT | real | Anteil AE Derating wegen Übertemperatur IGBT/Diode |
| STAT_DEG0_EINH | string | "%" |
| STAT_DEG1_WERT | real | Anteil AE Derating wegen Temperaturspreizung NTC zu IGBT/Diode |
| STAT_DEG1_EINH | string | "%" |
| STAT_DEG2_WERT | real | Anteil AE Derating wegen Übertemperatur NTC |
| STAT_DEG2_EINH | string | "%" |
| STAT_DEG3_WERT | real | Anteil AE Derating wegen Übertemperatur Kühlmittel |
| STAT_DEG3_EINH | string | "%" |
| STAT_DEG4_WERT | real | Anteil AE Derating wegen Schaltüberspannung wg. U_DC Niveau |
| STAT_DEG4_EINH | string | "%" |
| STAT_DEG5_WERT | real | Anteil AE Derating wegen Drehzahlbereich |
| STAT_DEG5_EINH | string | "%" |
| STAT_DEG6_WERT | real | Anteil EM Derating Moment bedingt durch HV-DC Spannung (Motorischer Betrieb) |
| STAT_DEG6_EINH | string | "%" |
| STAT_DEG7_WERT | real | Anteil EM Derating Moment bedingt durch HV-DC Spannung (Generatorischer Betrieb) |
| STAT_DEG7_EINH | string | "%" |
| STAT_DEG8_WERT | real | Anteil EM Derating Moment bedingt durch Drehzahl (Motorischer Betrieb) |
| STAT_DEG8_EINH | string | "%" |
| STAT_DEG9_WERT | real | Anteil EM Derating Moment bedingt durch Drehzahl (Generatorischer Betrieb) |
| STAT_DEG9_EINH | string | "%" |
| STAT_DEG10_WERT | real | Anteil EM derating Moment wegen HV-DC Strom (Motorischer Betrieb) |
| STAT_DEG10_EINH | string | "%" |
| STAT_DEG11_WERT | real | Anteil EM derating Moment wegen HV-DC Strom (Generatorischer Betrieb) |
| STAT_DEG11_EINH | string | "%" |
| STAT_DEG12_WERT | real | Anteil AE Derating Moment durch Temperatur EM |
| STAT_DEG12_EINH | string | "%" |
| STAT_DEG13_WERT | real | Dauer Reku eingeschränkt CCM793 |
| STAT_DEG13_EINH | string | "%" |
| STAT_DEG14_WERT | real | Dauer Reku eingeschränkt Stufe 1 CCM800 |
| STAT_DEG14_EINH | string | "%" |
| STAT_DEG15_WERT | real | Dauer Reku eingeschränkt Stufe 2 CCM796 |
| STAT_DEG15_EINH | string | "%" |
| STAT_DEG16_WERT | real | Dauer N-MAX Überschreitung CCM795 |
| STAT_DEG16_EINH | string | "%" |
| STAT_NLM_WERT | unsigned int | Dauer Begrenzung Notlaufmanager |
| STAT_NLM_EINH | string | "min" |
| STAT_NLM_ANZ_WERT | unsigned int | Anzahl Begrenzung Notlaufmanager |
| STAT_NLM_ANZ_EINH | string | "-" |
| STAT_FAHRD_WERT | real | Anteil Fahrstufe D |
| STAT_FAHRD_EINH | string | "%" |
| STAT_FAHRP_WERT | real | Anteil Fahrstufe P |
| STAT_FAHRP_EINH | string | "%" |
| STAT_FAHRN_WERT | real | Anteil Fahrstufe N |
| STAT_FAHRN_EINH | string | "%" |
| STAT_FAHRR_WERT | real | Anteil Fahrstufe R |
| STAT_FAHRR_EINH | string | "%" |
| STAT_ACC1_WERT | real | Beschleunigungsprofil Punkt 1 |
| STAT_ACC1_EINH | string | "%" |
| STAT_ACC2_WERT | real | Beschleunigungsprofil Punkt 2 |
| STAT_ACC2_EINH | string | "%" |
| STAT_ACC3_WERT | real | Beschleunigungsprofil Punkt 3 |
| STAT_ACC3_EINH | string | "%" |
| STAT_ACC4_WERT | real | Beschleunigungsprofil Punkt 4 |
| STAT_ACC4_EINH | string | "%" |
| STAT_ACC5_WERT | real | Beschleunigungsprofil Punkt 5 |
| STAT_ACC5_EINH | string | "%" |
| STAT_ELUP_ZEIT_WERT | unsigned long | Laufzeit ELUP |
| STAT_ELUP_ZEIT_EINH | string | "%" |
| STAT_ELUP_AN_WERT | unsigned long | Anläufe ELUP |
| STAT_ELUP_AN_EINH | string | "%" |
| STAT_BREMS_ANZ_WERT | unsigned long | Anzahl Bremsbetätigungen |
| STAT_BREMS_ANZ_EINH | string | "%" |
| STAT_PWUNSCH2_WERT | real | Beschleunigungsprofil Punkt 4 |
| STAT_PWUNSCH2_EINH | string | "%" |
| STAT_PWUNSCH3_WERT | real | Beschleunigungsprofil Punkt 5 |
| STAT_PWUNSCH3_EINH | string | "%" |
| STAT_WEGSTRK_WERT | real | Wegstrecke |
| STAT_WEGSTRK_EINH | string | "km" |
| STAT_NELUEFTB1_WERT | real | E-Lüfter-Profil Bereich 1 |
| STAT_NELUEFTB1_EINH | string | "%" |
| STAT_NELUEFTB2_WERT | real | E-Lüfter-Profil Bereich 2 |
| STAT_NELUEFTB2_EINH | string | "%" |
| STAT_NELUEFTB3_WERT | real | E-Lüfter-Profil Bereich 3 |
| STAT_NELUEFTB3_EINH | string | "%" |
| STAT_NELUEFTB4_WERT | real | E-Lüfter-Profil Bereich 4 |
| STAT_NELUEFTB4_EINH | string | "%" |
| STAT_NELUEFTB5_WERT | real | E-Lüfter-Profil Bereich 5 |
| STAT_NELUEFTB5_EINH | string | "%" |
| STAT_NEWP6SOLLB1_WERT | real | Pumpensolldrehzahl-Profil Bereich 1 |
| STAT_NEWP6SOLLB1_EINH | string | "%" |
| STAT_NEWP6SOLLB2_WERT | real | Pumpensolldrehzahl-Profil Bereich 2 |
| STAT_NEWP6SOLLB2_EINH | string | "%" |
| STAT_NEWP6SOLLB3_WERT | real | Pumpensolldrehzahl-Profil Bereich 3 |
| STAT_NEWP6SOLLB3_EINH | string | "%" |
| STAT_NEWP6SOLLB4_WERT | real | Pumpensolldrehzahl-Profil Bereich 4 |
| STAT_NEWP6SOLLB4_EINH | string | "%" |
| STAT_NEWP6SOLLB5_WERT | real | Pumpensolldrehzahl-Profil Bereich 5 |
| STAT_NEWP6SOLLB5_EINH | string | "%" |
| STAT_TN_TSRVOKO_WERT | unsigned int | Betriebsstundenzähler Vorkonditionierung |
| STAT_TN_TSRVOKO_EINH | string | "h" |
| STAT_TN_TSRLADEN_WERT | unsigned int | Betriebsstundenzähler Laden |
| STAT_TN_TSRLADEN_EINH | string | "h" |
| STAT_TN_TSRNK_WERT | unsigned int | Betriebsstundenzähler BA Notfallkühlsystem |
| STAT_TN_TSRNK_EINH | string | "s" |
| STAT_TN_TSRBS_WERT | unsigned int | Betriebsstundenzähler BA Bauteilschutz |
| STAT_TN_TSRBS_EINH | string | "s" |
| STAT_Z_BSTDCDC_WERT | unsigned char | Ursache BA Notfall / BS: DCDC-Übertemperatur |
| STAT_Z_BSTDCDC_EINH | string | "-" |
| STAT_Z_BSTEM_WERT | unsigned char | Ursache BA Notfall / BS: EM-Übertemperatur |
| STAT_Z_BSTEM_EINH | string | "-" |
| STAT_Z_BSTLE_WERT | unsigned char | Ursache BA Notfall / BS: LE-Übertemperatur |
| STAT_Z_BSTLE_EINH | string | "-" |
| STAT_Z_BSTELE_WERT | unsigned char | Ursache BA Notfall / BS: ELE-Übertemperatur |
| STAT_Z_BSTELE_EINH | string | "-" |
| STAT_Z_EL_FEHLER_WERT | unsigned char | Ursache BA Notfall / BS: ELÜFTER- Fehler |
| STAT_Z_EL_FEHLER_EINH | string | "-" |
| STAT_Z_EWP6_FEHLER_WERT | unsigned char | Ursache BA Notfall / BS: EWP6-Fehler |
| STAT_Z_EWP6_FEHLER_EINH | string | "-" |
| STAT_TEMB1_WERT | real | Profil E-Maschinen-Temperatur Bereich 1 |
| STAT_TEMB1_EINH | string | "%" |
| STAT_TEMB2_WERT | real | Profil E-Maschinen-Temperatur Bereich 2 |
| STAT_TEMB2_EINH | string | "%" |
| STAT_TEMB3_WERT | real | Profil E-Maschinen-Temperatur Bereich 3 |
| STAT_TEMB3_EINH | string | "%" |
| STAT_TEMB4_WERT | real | Profil E-Maschinen-Temperatur Bereich 4 |
| STAT_TEMB4_EINH | string | "%" |
| STAT_TEMB5_WERT | real | Profil E-Maschinen-Temperatur Bereich 5 |
| STAT_TEMB5_EINH | string | "%" |
| STAT_TEMMAX_WERT | int | Maximalwert E-Maschinen-Temperatur |
| STAT_TEMMAX_EINH | string | "°C" |
| STAT_TDCDCB1_WERT | real | Profil DCDC-Wandler-Temperatur Bereich 1 |
| STAT_TDCDCB1_EINH | string | "%" |
| STAT_TDCDCB2_WERT | real | Profil DCDC-Wandler-Temperatur Bereich 2 |
| STAT_TDCDCB2_EINH | string | "%" |
| STAT_TDCDCB3_WERT | real | Profil DCDC-Wandler-Temperatur Bereich 3 |
| STAT_TDCDCB3_EINH | string | "%" |
| STAT_TDCDCB4_WERT | real | Profil DCDC-Wandler-Temperatur Bereich 4 |
| STAT_TDCDCB4_EINH | string | "%" |
| STAT_TDCDCB5_WERT | real | Profil DCDC-Wandler-Temperatur Bereich 5 |
| STAT_TDCDCB5_EINH | string | "%" |
| STAT_TDCDCMAX_WERT | int | Maximalwert DCDC-Wandler-Temperatur |
| STAT_TDCDCMAX_EINH | string | "°C" |
| STAT_TELEB1_WERT | real | Profil ELE-Temperatur Bereich 1 |
| STAT_TELEB1_EINH | string | "%" |
| STAT_TELEB2_WERT | real | Profil ELE-Temperatur Bereich 2 |
| STAT_TELEB2_EINH | string | "%" |
| STAT_TELEB3_WERT | real | Profil ELE-Temperatur Bereich 3 |
| STAT_TELEB3_EINH | string | "%" |
| STAT_TELEB4_WERT | real | Profil ELE-Temperatur Bereich 4 |
| STAT_TELEB4_EINH | string | "%" |
| STAT_TELEB5_WERT | real | Profil ELE-Temperatur Bereich 5 |
| STAT_TELEB5_EINH | string | "%" |
| STAT_TELEMAX_WERT | int | Maximalwert ELE-Temperatur |
| STAT_TELEMAX_EINH | string | "°C" |
| STAT_TLEB1_WERT | real | Bereiche EME-Temperatur Bereich 1 |
| STAT_TLEB1_EINH | string | "%" |
| STAT_TLEB2_WERT | real | Bereiche EME-Temperatur Bereich 2 |
| STAT_TLEB2_EINH | string | "%" |
| STAT_TLEB3_WERT | real | Bereiche EME-Temperatur Bereich 3 |
| STAT_TLEB3_EINH | string | "%" |
| STAT_TLEB4_WERT | real | Bereiche EME-Temperatur Bereich 4 |
| STAT_TLEB4_EINH | string | "%" |
| STAT_TLEB5_WERT | real | Bereiche EME-Temperatur Bereich 5 |
| STAT_TLEB5_EINH | string | "%" |
| STAT_TLEMAX_WERT | int | Maximalwert EME-Temperatur |
| STAT_TLEMAX_EINH | string | "°C" |
| STAT_TUMGB1_WERT | real | Profil Umgebungslufttemperatur Bereich 1 |
| STAT_TUMGB1_EINH | string | "%" |
| STAT_TUMGB2_WERT | real | Profil Umgebungslufttemperatur Bereich 2 |
| STAT_TUMGB2_EINH | string | "%" |
| STAT_TUMGB3_WERT | real | Profil Umgebungslufttemperatur Bereich 3 |
| STAT_TUMGB3_EINH | string | "%" |
| STAT_TUMGB4_WERT | real | Profil Umgebungslufttemperatur Bereich 4 |
| STAT_TUMGB4_EINH | string | "%" |
| STAT_TUMGB5_WERT | real | Profil Umgebungslufttemperatur Bereich 5 |
| STAT_TUMGB5_EINH | string | "%" |
| STAT_TN_TSREWP6_WERT | unsigned int | Betriebsstundenzähler Nachlaufzeit EWP6 |
| STAT_TN_TSREWP6_EINH | string | "min" |
| STAT_TN_TSRNEL_WERT | unsigned int | Betriebsstundenzähler Nachlaufzeit E-Lüfter |
| STAT_TN_TSRNEL_EINH | string | "min" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-degrad-disp-lesen"></a>
### STATUS_DEGRAD_DISP_LESEN

Angezeigte Degradationen der letzten 10 Fahrzyklen DEGRAD_DISP_LESEN (0xDEC1)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MDMIN_1_DC1_WERT | unsigned char | Degradation wegen Betriebsstrategie min-Grenze Moment letzter Fahrzyklus ) |
| STAT_MDMIN_1_DC1_EINH | string | "-" |
| STAT_MDMIN_2_DC1_WERT | unsigned char | Degradation wegen Diagnose-Anforderung min-Grenze Moment letzter Fahrzyklus ) |
| STAT_MDMIN_2_DC1_EINH | string | "-" |
| STAT_MDMIN_3_DC1_WERT | unsigned char | Degradation wegen Notlauf-Manager min-Grenze Moment letzter Fahrzyklus ) |
| STAT_MDMIN_3_DC1_EINH | string | "-" |
| STAT_MDMIN_4_DC1_WERT | unsigned char | Degradation wegen SOC min-Grenze Moment letzter Fahrzyklus ) |
| STAT_MDMIN_4_DC1_EINH | string | "-" |
| STAT_MDMIN_5_DC1_WERT | unsigned char | Degradation wegen EM2- und LE2-Derating min-Grenze Moment letzter Fahrzyklus ) |
| STAT_MDMIN_5_DC1_EINH | string | "-" |
| STAT_MDMIN_6_DC1_WERT | unsigned char | Degradation wegen Sicherheitskonzept min-Grenze Moment letzter Fahrzyklus ) |
| STAT_MDMIN_6_DC1_EINH | string | "-" |
| STAT_MDMIN_7_DC1_WERT | unsigned char | Degradation der Rekuperation durch die Momentenkoordination min-Grenze Moment letzter Fahrzyklus ) |
| STAT_MDMIN_7_DC1_EINH | string | "-" |
| STAT_MDMIN_8_DC1_WERT | unsigned char | Degradation der Rekuperation durch DSC-Eingriff min-Grenze Moment letzter Fahrzyklus ) |
| STAT_MDMIN_8_DC1_EINH | string | "-" |
| STAT_MDMAX_1_DC1_WERT | unsigned char | Degradation wegen Betriebsstrategie max-Grenze Moment letzter Fahrzyklus ) |
| STAT_MDMAX_1_DC1_EINH | string | "-" |
| STAT_MDMAX_2_DC1_WERT | unsigned char | Degradation wegen Diagnose-Anforderung max-Grenze Moment letzter Fahrzyklus ) |
| STAT_MDMAX_2_DC1_EINH | string | "-" |
| STAT_MDMAX_3_DC1_WERT | unsigned char | Degradation wegen Notlauf-Manager max-Grenze Moment letzter Fahrzyklus ) |
| STAT_MDMAX_3_DC1_EINH | string | "-" |
| STAT_MDMAX_4_DC1_WERT | unsigned char | Degradation wegen SOC max-Grenze Moment letzter Fahrzyklus ) |
| STAT_MDMAX_4_DC1_EINH | string | "-" |
| STAT_MDMAX_5_DC1_WERT | unsigned char | Degradation durch den Leistungskoordinator max-Grenze Moment letzter Fahrzyklus ) |
| STAT_MDMAX_5_DC1_EINH | string | "-" |
| STAT_PEMIN_1_DC1_WERT | unsigned char | Degradation wegen Betriebsstrategie min-Grenze Leistung letzter Fahrzyklus ) |
| STAT_PEMIN_1_DC1_EINH | string | "-" |
| STAT_PEMIN_2_DC1_WERT | unsigned char | Degradation wegen Diagnose-Anforderung min-Grenze Leistung letzter Fahrzyklus ) |
| STAT_PEMIN_2_DC1_EINH | string | "-" |
| STAT_PEMIN_3_DC1_WERT | unsigned char | Degradation wegen Notlauf-Manager min-Grenze Leistung letzter Fahrzyklus ) |
| STAT_PEMIN_3_DC1_EINH | string | "-" |
| STAT_PEMIN_4_DC1_WERT | unsigned char | Degradation wegen SOC min-Grenze Leistung letzter Fahrzyklus ) |
| STAT_PEMIN_4_DC1_EINH | string | "-" |
| STAT_PEMIN_5_DC1_WERT | unsigned char | Degradation durch den Leistungskoordinator min-Grenze Leistung letzter Fahrzyklus ) |
| STAT_PEMIN_5_DC1_EINH | string | "-" |
| STAT_PEMAX_1_DC1_WERT | unsigned char | Degradation wegen Betriebsstrategie max-Grenze Leistung letzter Fahrzyklus ) |
| STAT_PEMAX_1_DC1_EINH | string | "-" |
| STAT_PEMAX_2_DC1_WERT | unsigned char | Degradation wegen Diagnose-Anforderung max-Grenze Leistung letzter Fahrzyklus ) |
| STAT_PEMAX_2_DC1_EINH | string | "-" |
| STAT_PEMAX_3_DC1_WERT | unsigned char | Degradation wegen Notlauf-Manager max-Grenze Leistung letzter Fahrzyklus ) |
| STAT_PEMAX_3_DC1_EINH | string | "-" |
| STAT_PEMAX_4_DC1_WERT | unsigned char | Degradation wegen SOC max-Grenze Leistung letzter Fahrzyklus ) |
| STAT_PEMAX_4_DC1_EINH | string | "-" |
| STAT_PEMAX_5_DC1_WERT | unsigned char | Degradation durch den Leistungskoordinator max-Grenze Leistung letzter Fahrzyklus ) |
| STAT_PEMAX_5_DC1_EINH | string | "-" |
| STAT_MDMIN_1_DC2_WERT | unsigned char | Degradation wegen Betriebsstrategie min-Grenze Moment vorletzter Fahrzyklus ) |
| STAT_MDMIN_1_DC2_EINH | string | "-" |
| STAT_MDMIN_2_DC2_WERT | unsigned char | Degradation wegen Diagnose-Anforderung min-Grenze Moment vorletzter Fahrzyklus ) |
| STAT_MDMIN_2_DC2_EINH | string | "-" |
| STAT_MDMIN_3_DC2_WERT | unsigned char | Degradation wegen Notlauf-Manager min-Grenze Moment vorletzter Fahrzyklus ) |
| STAT_MDMIN_3_DC2_EINH | string | "-" |
| STAT_MDMIN_4_DC2_WERT | unsigned char | Degradation wegen SOC min-Grenze Moment vorletzter Fahrzyklus ) |
| STAT_MDMIN_4_DC2_EINH | string | "-" |
| STAT_MDMIN_5_DC2_WERT | unsigned char | Degradation wegen EM2- und LE2-Derating min-Grenze Moment vorletzter Fahrzyklus ) |
| STAT_MDMIN_5_DC2_EINH | string | "-" |
| STAT_MDMIN_6_DC2_WERT | unsigned char | Degradation wegen Sicherheitskonzept min-Grenze Moment vorletzter Fahrzyklus ) |
| STAT_MDMIN_6_DC2_EINH | string | "-" |
| STAT_MDMIN_7_DC2_WERT | unsigned char | Degradation der Rekuperation durch die Momentenkoordination min-Grenze Moment vorletzter Fahrzyklus ) |
| STAT_MDMIN_7_DC2_EINH | string | "-" |
| STAT_MDMIN_8_DC2_WERT | unsigned char | Degradation der Rekuperation durch DSC-Eingriff min-Grenze Moment vorletzter Fahrzyklus ) |
| STAT_MDMIN_8_DC2_EINH | string | "-" |
| STAT_MDMAX_1_DC2_WERT | unsigned char | Degradation wegen Betriebsstrategie max-Grenze Moment vorletzter Fahrzyklus ) |
| STAT_MDMAX_1_DC2_EINH | string | "-" |
| STAT_MDMAX_2_DC2_WERT | unsigned char | Degradation wegen Diagnose-Anforderung max-Grenze Moment vorletzter Fahrzyklus ) |
| STAT_MDMAX_2_DC2_EINH | string | "-" |
| STAT_MDMAX_3_DC2_WERT | unsigned char | Degradation wegen Notlauf-Manager max-Grenze Moment vorletzter Fahrzyklus ) |
| STAT_MDMAX_3_DC2_EINH | string | "-" |
| STAT_MDMAX_4_DC2_WERT | unsigned char | Degradation wegen SOC max-Grenze Moment vorletzter Fahrzyklus ) |
| STAT_MDMAX_4_DC2_EINH | string | "-" |
| STAT_MDMAX_5_DC2_WERT | unsigned char | Degradation durch den Leistungskoordinator max-Grenze Moment vorletzter Fahrzyklus ) |
| STAT_MDMAX_5_DC2_EINH | string | "-" |
| STAT_PEMIN_1_DC2_WERT | unsigned char | Degradation wegen Betriebsstrategie min-Grenze Leistung vorletzter Fahrzyklus ) |
| STAT_PEMIN_1_DC2_EINH | string | "-" |
| STAT_PEMIN_2_DC2_WERT | unsigned char | Degradation wegen Diagnose-Anforderung min-Grenze Leistung vorletzter Fahrzyklus ) |
| STAT_PEMIN_2_DC2_EINH | string | "-" |
| STAT_PEMIN_3_DC2_WERT | unsigned char | Degradation wegen Notlauf-Manager min-Grenze Leistung vorletzter Fahrzyklus ) |
| STAT_PEMIN_3_DC2_EINH | string | "-" |
| STAT_PEMIN_4_DC2_WERT | unsigned char | Degradation wegen SOC min-Grenze Leistung vorletzter Fahrzyklus ) |
| STAT_PEMIN_4_DC2_EINH | string | "-" |
| STAT_PEMIN_5_DC2_WERT | unsigned char | Degradation durch den Leistungskoordinator min-Grenze Leistung vorletzter Fahrzyklus ) |
| STAT_PEMIN_5_DC2_EINH | string | "-" |
| STAT_PEMAX_1_DC2_WERT | unsigned char | Degradation wegen Betriebsstrategie max-Grenze Leistung vorletzter Fahrzyklus ) |
| STAT_PEMAX_1_DC2_EINH | string | "-" |
| STAT_PEMAX_2_DC2_WERT | unsigned char | Degradation wegen Diagnose-Anforderung max-Grenze Leistung vorletzter Fahrzyklus ) |
| STAT_PEMAX_2_DC2_EINH | string | "-" |
| STAT_PEMAX_3_DC2_WERT | unsigned char | Degradation wegen Notlauf-Manager max-Grenze Leistung vorletzter Fahrzyklus ) |
| STAT_PEMAX_3_DC2_EINH | string | "-" |
| STAT_PEMAX_4_DC2_WERT | unsigned char | Degradation wegen SOC max-Grenze Leistung vorletzter Fahrzyklus ) |
| STAT_PEMAX_4_DC2_EINH | string | "-" |
| STAT_PEMAX_5_DC2_WERT | unsigned char | Degradation durch den Leistungskoordinator max-Grenze Leistung vorletzter Fahrzyklus ) |
| STAT_PEMAX_5_DC2_EINH | string | "-" |
| STAT_MDMIN_1_DC3_WERT | unsigned char | Degradation wegen Betriebsstrategie min-Grenze Moment vorvorletzter Fahrzyklus ) |
| STAT_MDMIN_1_DC3_EINH | string | "-" |
| STAT_MDMIN_2_DC3_WERT | unsigned char | Degradation wegen Diagnose-Anforderung min-Grenze Moment vorvorletzter Fahrzyklus ) |
| STAT_MDMIN_2_DC3_EINH | string | "-" |
| STAT_MDMIN_3_DC3_WERT | unsigned char | Degradation wegen Notlauf-Manager min-Grenze Moment vorvorletzter Fahrzyklus ) |
| STAT_MDMIN_3_DC3_EINH | string | "-" |
| STAT_MDMIN_4_DC3_WERT | unsigned char | Degradation wegen SOC min-Grenze Moment vorvorletzter Fahrzyklus ) |
| STAT_MDMIN_4_DC3_EINH | string | "-" |
| STAT_MDMIN_5_DC3_WERT | unsigned char | Degradation wegen EM2- und LE2-Derating min-Grenze Moment vorvorletzter Fahrzyklus ) |
| STAT_MDMIN_5_DC3_EINH | string | "-" |
| STAT_MDMIN_6_DC3_WERT | unsigned char | Degradation wegen Sicherheitskonzept min-Grenze Moment vorvorletzter Fahrzyklus ) |
| STAT_MDMIN_6_DC3_EINH | string | "-" |
| STAT_MDMIN_7_DC3_WERT | unsigned char | Degradation der Rekuperation durch die Momentenkoordination min-Grenze Moment vorvorletzter Fahrzyklus ) |
| STAT_MDMIN_7_DC3_EINH | string | "-" |
| STAT_MDMIN_8_DC3_WERT | unsigned char | Degradation der Rekuperation durch DSC-Eingriff min-Grenze Moment vorvorletzter Fahrzyklus ) |
| STAT_MDMIN_8_DC3_EINH | string | "-" |
| STAT_MDMAX_1_DC3_WERT | unsigned char | Degradation wegen Betriebsstrategie max-Grenze Moment vorvorletzter Fahrzyklus ) |
| STAT_MDMAX_1_DC3_EINH | string | "-" |
| STAT_MDMAX_2_DC3_WERT | unsigned char | Degradation wegen Diagnose-Anforderung max-Grenze Moment vorvorletzter Fahrzyklus ) |
| STAT_MDMAX_2_DC3_EINH | string | "-" |
| STAT_MDMAX_3_DC3_WERT | unsigned char | Degradation wegen Notlauf-Manager max-Grenze Moment vorvorletzter Fahrzyklus ) |
| STAT_MDMAX_3_DC3_EINH | string | "-" |
| STAT_MDMAX_4_DC3_WERT | unsigned char | Degradation wegen SOC max-Grenze Moment vorvorletzter Fahrzyklus ) |
| STAT_MDMAX_4_DC3_EINH | string | "-" |
| STAT_MDMAX_5_DC3_WERT | unsigned char | Degradation durch den Leistungskoordinator max-Grenze Moment vorvorletzter Fahrzyklus ) |
| STAT_MDMAX_5_DC3_EINH | string | "-" |
| STAT_PEMIN_1_DC3_WERT | unsigned char | Degradation wegen Betriebsstrategie min-Grenze Leistung vorvorletzter Fahrzyklus ) |
| STAT_PEMIN_1_DC3_EINH | string | "-" |
| STAT_PEMIN_2_DC3_WERT | unsigned char | Degradation wegen Diagnose-Anforderung min-Grenze Leistung vorvorletzter Fahrzyklus ) |
| STAT_PEMIN_2_DC3_EINH | string | "-" |
| STAT_PEMIN_3_DC3_WERT | unsigned char | Degradation wegen Notlauf-Manager min-Grenze Leistung vorvorletzter Fahrzyklus ) |
| STAT_PEMIN_3_DC3_EINH | string | "-" |
| STAT_PEMIN_4_DC3_WERT | unsigned char | Degradation wegen SOC min-Grenze Leistung vorvorletzter Fahrzyklus ) |
| STAT_PEMIN_4_DC3_EINH | string | "-" |
| STAT_PEMIN_5_DC3_WERT | unsigned char | Degradation durch den Leistungskoordinator min-Grenze Leistung vorvorletzter Fahrzyklus ) |
| STAT_PEMIN_5_DC3_EINH | string | "-" |
| STAT_PEMAX_1_DC3_WERT | unsigned char | Degradation wegen Betriebsstrategie max-Grenze Leistung vorvorletzter Fahrzyklus ) |
| STAT_PEMAX_1_DC3_EINH | string | "-" |
| STAT_PEMAX_2_DC3_WERT | unsigned char | Degradation wegen Diagnose-Anforderung max-Grenze Leistung vorvorletzter Fahrzyklus ) |
| STAT_PEMAX_2_DC3_EINH | string | "-" |
| STAT_PEMAX_3_DC3_WERT | unsigned char | Degradation wegen Notlauf-Manager max-Grenze Leistung vorvorletzter Fahrzyklus ) |
| STAT_PEMAX_3_DC3_EINH | string | "-" |
| STAT_PEMAX_4_DC3_WERT | unsigned char | Degradation wegen SOC max-Grenze Leistung vorvorletzter Fahrzyklus ) |
| STAT_PEMAX_4_DC3_EINH | string | "-" |
| STAT_PEMAX_5_DC3_WERT | unsigned char | Degradation durch den Leistungskoordinator max-Grenze Leistung vorvorletzter Fahrzyklus ) |
| STAT_PEMAX_5_DC3_EINH | string | "-" |
| STAT_MDMIN_1_DC4_WERT | unsigned char | Degradation wegen Betriebsstrategie min-Grenze Moment der letzten 4-10 Fahrzyklen ) |
| STAT_MDMIN_1_DC4_EINH | string | "-" |
| STAT_MDMIN_2_DC4_WERT | unsigned char | Degradation wegen Diagnose-Anforderung min-Grenze Moment der letzten 4-10 Fahrzyklen ) |
| STAT_MDMIN_2_DC4_EINH | string | "-" |
| STAT_MDMIN_3_DC4_WERT | unsigned char | Degradation wegen Notlauf-Manager min-Grenze Moment der letzten 4-10 Fahrzyklen ) |
| STAT_MDMIN_3_DC4_EINH | string | "-" |
| STAT_MDMIN_4_DC4_WERT | unsigned char | Degradation wegen SOC min-Grenze Moment der letzten 4-10 Fahrzyklen ) |
| STAT_MDMIN_4_DC4_EINH | string | "-" |
| STAT_MDMIN_5_DC4_WERT | unsigned char | Degradation wegen EM2- und LE2-Derating min-Grenze Moment der letzten 4-10 Fahrzyklen ) |
| STAT_MDMIN_5_DC4_EINH | string | "-" |
| STAT_MDMIN_6_DC4_WERT | unsigned char | Degradation wegen Sicherheitskonzept min-Grenze Moment der letzten 4-10 Fahrzyklen ) |
| STAT_MDMIN_6_DC4_EINH | string | "-" |
| STAT_MDMIN_7_DC4_WERT | unsigned char | Degradation der Rekuperation durch die Momentenkoordination min-Grenze Moment der letzten 4-10 Fahrzyklen ) |
| STAT_MDMIN_7_DC4_EINH | string | "-" |
| STAT_MDMIN_8_DC4_WERT | unsigned char | Degradation der Rekuperation durch DSC-Eingriff min-Grenze Moment der letzten 4-10 Fahrzyklen ) |
| STAT_MDMIN_8_DC4_EINH | string | "-" |
| STAT_MDMAX_1_DC4_WERT | unsigned char | Degradation wegen Betriebsstrategie max-Grenze Moment der letzten 4-10 Fahrzyklen ) |
| STAT_MDMAX_1_DC4_EINH | string | "-" |
| STAT_MDMAX_2_DC4_WERT | unsigned char | Degradation wegen Diagnose-Anforderung max-Grenze Moment der letzten 4-10 Fahrzyklen ) |
| STAT_MDMAX_2_DC4_EINH | string | "-" |
| STAT_MDMAX_3_DC4_WERT | unsigned char | Degradation wegen Notlauf-Manager max-Grenze Moment der letzten 4-10 Fahrzyklen ) |
| STAT_MDMAX_3_DC4_EINH | string | "-" |
| STAT_MDMAX_4_DC4_WERT | unsigned char | Degradation wegen SOC max-Grenze Moment der letzten 4-10 Fahrzyklen ) |
| STAT_MDMAX_4_DC4_EINH | string | "-" |
| STAT_MDMAX_5_DC4_WERT | unsigned char | Degradation durch den Leistungskoordinator max-Grenze Moment der letzten 4-10 Fahrzyklen ) |
| STAT_MDMAX_5_DC4_EINH | string | "-" |
| STAT_PEMIN_1_DC4_WERT | unsigned char | Degradation wegen Betriebsstrategie min-Grenze Leistung der letzten 4-10 Fahrzyklen ) |
| STAT_PEMIN_1_DC4_EINH | string | "-" |
| STAT_PEMIN_2_DC4_WERT | unsigned char | Degradation wegen Diagnose-Anforderung min-Grenze Leistung der letzten 4-10 Fahrzyklen ) |
| STAT_PEMIN_2_DC4_EINH | string | "-" |
| STAT_PEMIN_3_DC4_WERT | unsigned char | Degradation wegen Notlauf-Manager min-Grenze Leistung der letzten 4-10 Fahrzyklen ) |
| STAT_PEMIN_3_DC4_EINH | string | "-" |
| STAT_PEMIN_4_DC4_WERT | unsigned char | Degradation wegen SOC min-Grenze Leistung der letzten 4-10 Fahrzyklen ) |
| STAT_PEMIN_4_DC4_EINH | string | "-" |
| STAT_PEMIN_5_DC4_WERT | unsigned char | Degradation durch den Leistungskoordinator min-Grenze Leistung der letzten 4-10 Fahrzyklen ) |
| STAT_PEMIN_5_DC4_EINH | string | "-" |
| STAT_PEMAX_1_DC4_WERT | unsigned char | Degradation wegen Betriebsstrategie max-Grenze Leistung der letzten 4-10 Fahrzyklen ) |
| STAT_PEMAX_1_DC4_EINH | string | "-" |
| STAT_PEMAX_2_DC4_WERT | unsigned char | Degradation wegen Diagnose-Anforderung max-Grenze Leistung der letzten 4-10 Fahrzyklen ) |
| STAT_PEMAX_2_DC4_EINH | string | "-" |
| STAT_PEMAX_3_DC4_WERT | unsigned char | Degradation wegen Notlauf-Manager max-Grenze Leistung der letzten 4-10 Fahrzyklen ) |
| STAT_PEMAX_3_DC4_EINH | string | "-" |
| STAT_PEMAX_4_DC4_WERT | unsigned char | Degradation wegen SOC max-Grenze Leistung der letzten 4-10 Fahrzyklen ) |
| STAT_PEMAX_4_DC4_EINH | string | "-" |
| STAT_PEMAX_5_DC4_WERT | unsigned char | Degradation durch den Leistungskoordinator max-Grenze Leistung der letzten 4-10 Fahrzyklen ) |
| STAT_PEMAX_5_DC4_EINH | string | "-" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (127 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (251 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (250 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (52 × 9)
- [FARTTYP](#table-farttyp) (257 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (18 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (251 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (250 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (52 × 9)
- [IARTTYP](#table-iarttyp) (257 × 5)
- [IARTTEXTEINDIVIDUELL](#table-iarttexteindividuell) (18 × 2)
- [_MSD85YL6_TABLE_FS](#table-msd85yl6-table-fs) (11 × 2)
- [_MSD85YL6_TABLE_ST_MONTAGEMODUS_AKTIV_INAKTIV](#table-msd85yl6-table-st-montagemodus-aktiv-inaktiv) (2 × 2)
- [T_TAB_EDME_LADEKABEL](#table-t-tab-edme-ladekabel) (4 × 2)
- [T_TAB_EDME_BETRIEBSMODE_DCDC](#table-t-tab-edme-betriebsmode-dcdc) (4 × 2)
- [STATCLIENTAUTHTXT](#table-statclientauthtxt) (4 × 2)
- [STATFREESKTXT](#table-statfreesktxt) (3 × 2)
- [STATEWSVERTXT](#table-statewsvertxt) (3 × 2)
- [TAB_STAT_ST_DIAG_DCDC_MODUS](#table-tab-stat-st-diag-dcdc-modus) (3 × 2)
- [TAB_STAT_ST_DIAG_DCDC_GRENZEN](#table-tab-stat-st-diag-dcdc-grenzen) (2 × 2)
- [T_TAB_ST_B_DIAG_DCDC](#table-t-tab-st-b-diag-dcdc) (5 × 2)
- [T_TAB_ST_DIAG_DCDC_ANF](#table-t-tab-st-diag-dcdc-anf) (4 × 2)
- [T_TAB_EDME_REMOTE_LADEN](#table-t-tab-edme-remote-laden) (4 × 2)
- [T_TAB_EDME_STATUS_LADEN](#table-t-tab-edme-status-laden) (7 × 2)
- [T_TAB_EDME_TIMER_LADEN_NR](#table-t-tab-edme-timer-laden-nr) (4 × 2)
- [T_TAB_EME_HVSTART_KOMM](#table-t-tab-eme-hvstart-komm) (16 × 2)
- [T_TAB_EME_I0ANF_HVB](#table-t-tab-eme-i0anf-hvb) (5 × 2)
- [T_TAB_TSR_LADEN_STAT_ART_LADEANF_BIT_0](#table-t-tab-tsr-laden-stat-art-ladeanf-bit-0) (2 × 2)
- [T_TAB_TSR_LADEN_STAT_ART_LADEANF_BIT_1](#table-t-tab-tsr-laden-stat-art-ladeanf-bit-1) (2 × 2)
- [T_TAB_TSR_LADEN_STAT_ART_LADEANF_BIT_2](#table-t-tab-tsr-laden-stat-art-ladeanf-bit-2) (2 × 2)
- [T_TAB_TSR_LADEN_ST_BEDINGUNG_LADESTART](#table-t-tab-tsr-laden-st-bedingung-ladestart) (5 × 2)
- [T_TAB_TSR_LADEN_ST_ABBRUCHBEDINGUNG](#table-t-tab-tsr-laden-st-abbruchbedingung) (4 × 2)
- [T_TAB_TSR_LADEN_ST_REAS_LDUNTERBR](#table-t-tab-tsr-laden-st-reas-ldunterbr) (12 × 2)
- [T_TAB_TSR_LADEN_STAT_REAS_DERATING_BIT_0](#table-t-tab-tsr-laden-stat-reas-derating-bit-0) (2 × 2)
- [T_TAB_TSR_LADEN_STAT_REAS_DERATING_BIT_1](#table-t-tab-tsr-laden-stat-reas-derating-bit-1) (2 × 2)
- [T_TAB_TSR_LADEN_STAT_REAS_DERATING_BIT_2](#table-t-tab-tsr-laden-stat-reas-derating-bit-2) (2 × 2)
- [T_TAB_TSR_LADEN_STAT_REAS_DERATING_BIT_3](#table-t-tab-tsr-laden-stat-reas-derating-bit-3) (2 × 2)
- [T_TAB_TSR_LADEN_STAT_REAS_DERATING_BIT_4](#table-t-tab-tsr-laden-stat-reas-derating-bit-4) (2 × 2)
- [T_TAB_TSR_LADEN_STAT_ANF_ART_VOKO_BIT_0](#table-t-tab-tsr-laden-stat-anf-art-voko-bit-0) (2 × 2)
- [T_TAB_TSR_LADEN_STAT_ANF_ART_VOKO_BIT_1](#table-t-tab-tsr-laden-stat-anf-art-voko-bit-1) (2 × 2)
- [T_TAB_TSR_LADEN_STAT_ANF_ART_VOKO_BIT_2](#table-t-tab-tsr-laden-stat-anf-art-voko-bit-2) (2 × 2)
- [T_TAB_TSR_LADEN_STAT_ANF_ART_VOKO_BIT_3](#table-t-tab-tsr-laden-stat-anf-art-voko-bit-3) (2 × 2)
- [T_TAB_TSR_LADEN_STAT_NACHLADEANFORDERUNG](#table-t-tab-tsr-laden-stat-nachladeanforderung) (3 × 2)
- [T_TAB_TSR_LADEN_STAT_ZUSATZINFO_ABBRUCHBEDINGUNG](#table-t-tab-tsr-laden-stat-zusatzinfo-abbruchbedingung) (5 × 2)
- [_MOTORUDSCODIERUNG_RUHESTROM](#table-motorudscodierung-ruhestrom) (16 × 2)
- [T_TAB_EDME_ECOPRO](#table-t-tab-edme-ecopro) (2 × 2)

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

Dimensions: 127 rows × 2 columns

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

Dimensions: 251 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x2725 | Steuergeraet interner Fehler -Analog Digital Wandler Fehler |
| 0xCD89 | PT_CAN -Kommunikationsstoerung Botschaft (Anforderung Radmomente Antriebsstrang 0xBF Sender DSC) |
| 0xCDA1 | A_CAN -Kommunikationsstoerung Botschaft (Ist Daten DC/DC Wandler Ladeelektronik Langzeit 0x2C8 Sender AE) |
| 0xCDBA | A_CAN -Kommunikationsstoerung Botschaft (Ist Daten Komfort Ladeelektronik Langzeit 0x211 Sender KLE) |
| 0xCDA2 | A_CAN -Kommunikationsstoerung Botschaft (Ist Daten Ladeelektronik 0x108 Sender AE) |
| 0xCDA3 | A_CAN -Kommunikationsstoerung Botschaft (Ist Daten E Motor Traktion 0x100 Sender AE) |
| 0xCDA4 | A_CAN -Kommunikationsstoerung Botschaft (Ist Daten E Motor Traktion Langzeit 0x2C9 Sender AE) |
| 0xCDA5 | A_CAN -Kommunikationsstoerung Botschaft (Ist Daten Parksperre 0x35B Sender AE) |
| 0xCD86 | A_CAN -CAN Baustein Abschaltung |
| 0x2710 | Bremslichtschalter |
| 0x2711 | Charge Enable Control  |
| 0x2712 | Ladeleuchte  |
| 0x2713 | Elektroluefter Relais  |
| 0x2714 | Kuehlpumpe Notlaufeingang  |
| 0x2715 | Eingang MSA  |
| 0x271B | 12V Relais Ansteuerung  |
| 0x2716 | Klemme 50  |
| 0xCD88 | PT_CAN -Kommunikationsstoerung Botschaft (Aussentemperatur/Relativzeit 0x310 Sender Kombi) |
| 0x2717 | Ansteuerung Elektroluefter  |
| 0x2812 | Spannungsversorgung -Wert unplausibel |
| 0xCD8A | PT_CAN -Kommunikationsstoerung Botschaft (Bedienung Getriebewahlschalter 0x198 Sender GWS) |
| 0xCD9B | PT_CAN -Kommunikationsstoerung Botschaft (Bedienung Taster MSA 0x195 Sender IHKA) |
| 0x280A | Powermanagement -Niedervoltbatterie defekt waehrend Transport |
| 0x280B | Powermanagement -Niedervoltbatterie entladen wahrend Transport |
| 0x280C | Powermanagement -Niedervoltbatterie Bordnetzinstabilitaet |
| 0x2838 | AEP -12 V Batterie wird nicht geladen |
| 0x2839 | AEP -12 V Batterie wird nicht geladen |
| 0x2817 | Powermanagement - Niedervoltbatterie wird nicht geladen |
| 0x280D | Powermanagement -Ruhestromverletzung |
| 0x280E | Powermanagement -Niedervoltbatterie tiefentlanden |
| 0x280F | Powermanagement -Niedervolt Bordnetz Ueberspannung |
| 0x2810 | Powermanagement -Niedervolt Bordnetz Unterspannung |
| 0x2811 | Powermanagement -elektrische Verbraucher eingeschraenkt |
| 0x283A | AEP -12 V Batterie stark entladen |
| 0x27A9 | Bremspedal -Plausibilitaetsfehler |
| 0x2815 | Niedervoltbatterie defekt |
| 0x2816 | Niedervoltbatterie tiefentlanden |
| 0x27B1 | Checkcontrol 174 -Getriebeposition P nur im Stillstand |
| 0x27B2 | Checkcontrol 175 -Getriebepostion P gestoert |
| 0x27B3 | Checkcontrol 203 -Getriebe in N Waschstrassenfunktion |
| 0x27B4 | Checkcontrol 220 -Erhoehte Batterieentladung |
| 0x27B5 | Checkcontrol 244 -Zum Gangeinlegen Bremse treten |
| 0x27B6 | Checkcontrol 250 -Gang ohne Bremse einlegebar |
| 0x27B7 | Checkcontrol 251 -Getriebeposition P wird eingelegt |
| 0x27B8 | Checkcontrol 252 -Gong bei ungenuegender P Betaetigung |
| 0x27B9 | Checkcontrol 394 -Waehlhebel gestoert |
| 0x27BA | Checkcontrol 557 -Fahrzeug gegen Wegrollen sichern |
| 0x27BB | Checkcontrol 565 -Getriebeposition P nur im Stillstand |
| 0x27BC | Checkcontrol 636 -Hochvoltsystem abgeschaltet |
| 0x27BD | Checkcontrol 802 -Ladekabel pruefen |
| 0x27BE | Checkcontrol 803 -Netzleistung zu gering |
| 0x27BF | Checkcontrol 804 -Laden nicht moeglich |
| 0x27C0 | Checkcontrol 809 -Zum Laden P einlegen |
| 0x2784 | Checkcontrol-Uebertemperatur Antrieb China |
| 0x27C1 | Checkcontrol - Ueberstrom Parkaktuator. P kann eventuell nicht mehr ausgelegt werden. |
| 0x2774 | Notlaufmanager -Abschaltung DCDC Wandler wegen Ueberstrom |
| 0x2775 | Notlaufmanager -Abschaltung DCDC Wandler wegen HW Fehler |
| 0x2776 | Notlaufmanager -DCDC Wandler Abschaltung wegen Uebertemperatur |
| 0x2777 | Notlaufmanager -DCDC Wandler Abschaltung wegen Spannungskriterium |
| 0x2968 | N/A |
| 0x27A6 | Betriebsstrategie -Begrenzung der Antriebsleistung Stufe 1 |
| 0x27A7 | Betriebsstrategie -Begrenzung der Antriebsleistung Stufe 2 |
| 0x27AD | BEV13 |
| 0x2969 | N/A |
| 0x27F7 | - |
| 0x2976 | Elektrische Unterdruckpumpe -Elektrischer Fehler |
| 0x27E3 | Elektrische Unterdruckpumpe -Blockiert |
| 0x27E4 | Elektrische Unterdruckpumpe -Drucksensor Fehler |
| 0x27E7 | Elektrische Unterdruckpumpe - Ansteuerung seitens AE nicht moeglich elektrischer Fehler oder Montagemode aktiv |
| 0x27E5 | Elektrische Unterdruckpumpe -Leckage erkannt |
| 0x27E6 | Elektrische Unterdruckpumpe -Laufzeit Fehler |
| 0x2786 | Notlaufmanager - Abschaltung wegen Fehlerbedingte Nullmomentenregelung |
| 0x2787 | Notlaufmanager - Abschaltung wegen Fehlerbedingter AKS |
| 0x2788 | Notlaufmanager - Abschaltung wegen Fehlerbedingter Freilauf |
| 0x2779 | Notlaufmanager -Drehzahl der Elektromaschine hat Grenzwert ueberschritten |
| 0x275B | Kuehlmittelpumpe -Kommunikation |
| 0x275C | Kuehlmittelpumpe -Temperaturschwelle 1 ueberschritten |
| 0x275D | Kuehlmittelpumpe -Temperaturschwelle 2 ueberschritten |
| 0x275E | Kuehlmittelpumpe Kommunikation -Notlaufeingang Plausibilitaetsfehler |
| 0x275F | Kuehlmittelpumpe -Drehzahl ausserhalb Gueltigkeitsbereich |
| 0x2760 | Kuehlmittelpumpe -Trockenlauf |
| 0x2761 | Kuehlmittelpumpe -Ueberspannung |
| 0x2762 | Kuehlmittelpumpe -Ueberstrom |
| 0x2763 | Kuehlmittelpumpe -Uebertemperatur |
| 0x2764 | Kuehlmittelpumpe -Unterspannung |
| 0x27AB | Gaspedal und Bremspedalstellung -Plausibilitaetsfehler |
| 0x2820 | Herstellen Fahrbereitschaft nicht moeglich wegen Temperatur HV-Batterie zu hoch |
| 0x27AA | Betriebsstrategie -Herstellen der Fahrbereitschaft wegen des gesteckten Ladekabels nicht moeglich |
| 0x27AC | Betriebsstrategie -Herstellen der Fahrbereitschaft wegen des unplausiblen Ladekabelzustandes nur verzoegert moeglich |
| 0x282C | HV Powermanagement -HV Power Down aufgrund niedrigem Ladezustand HV Batterie |
| 0x282D | HV Batterie -Isoaltionsfehler |
| 0x282E | HV Batterie -Isolationswarnung |
| 0x2855 | Hochvoltbatterie - Temperatur kritischer Wert |
| 0x2821 | Hochvoltbatterie - Temperatur verlaesst Normalbereich |
| 0x2822 | Hochvoltbatterie - Temperatur wieder im Normalbereich |
| 0x282F | HV Zwischenkreisentladung -HV Zwischenkreis nicht spannungsfrei trotz Anforderung |
| 0x2830 | HV Powermanagement -keine HV Freigabe trotz Anforderung |
| 0x274C | Intelligenter Batteriesensor -Kommunikation |
| 0x274D | Intelligenter Batteriesensor -Strommessung unplausibel |
| 0x274E | Intelligenter Batteriesensor -Firmware unplausibel |
| 0x274F | Intelligenter Batteriesensor -Systemfehler |
| 0x2750 | Intelligenter Batteriesensor -Temperaturmessung unplausibel |
| 0x2751 | Intelligenter Batteriesensor -Spannungsmessung unplausibel |
| 0x2752 | Intelligenter Batteriesensor -Wake Up Leitung Leitungsbruch |
| 0x2753 | Intelligenter Batteriesensor -Wake Up Leitung ueber oder unter Schwellwert |
| 0x2831 | HV Powermanagement -Interlock unterbrochen |
| 0x283B | Lademanagement - AC-Spannung fehlt. HV-Speicher wird nicht geladen |
| 0x2823 | Lademanagement -AC Spannung fehlt nach Ladebeginn |
| 0x2824 | Lademanagement -AC Spannung dauerhaft instabil |
| 0x2825 | Lademanagement -SLE/KLE in Failsafe |
| 0x2826 | Lademanagement -Ladefehler |
| 0x2827 | Lademanagement -Ladeziel nicht erreichbar (SLE Leistung zu gering) |
| 0x2828 | Lademanagement -Ladeziel nicht erreichbar (Entladeschutz NV BN) |
| 0x2836 | Lademanagement -Zustand Ladestecker unbekannt |
| 0x2829 | Lademanagement -Ladestoerung |
| 0x290F | Fehlerort 1 fur FSP Testfunktion Layer |
| 0x2910 | Fehlerort 2 fur FSP Testfunktion Layer |
| 0x27AE | BEV13 |
| 0x2970 | N/A |
| 0x296A | N/A |
| 0x296B | N/A |
| 0x296E | N/A |
| 0x296F | N/A |
| 0x296C | N/A |
| 0x296D | N/A |
| 0x2971 | N/A |
| 0x282A | Lademanagement -Pilotsignal ungueltig |
| 0x2837 | Lademanagement -Pilotsignal ungueltig ausserhalb Ladebereitschaft |
| 0x27A8 | Betriebsstrategie -Begrenzung der Rekuperation |
| 0x27AF | BEV13 |
| 0x2832 | HV Batterie -einfacher Schuetzkleber |
| 0x2785 | Signalausfall-Moment und Betriebsartvorgabe E Maschine |
| 0x2833 | Signalausfall -HV Powermanagement |
| 0x2834 | Signalausfall -Antriebselektronik |
| 0x2835 | Signalausfall -HV Batterie |
| 0x2780 | Notlaufmanager -Hochvolt Batterie Service Request (Fehlerkategorie 3) |
| 0x2783 | Notlaufmanager -Hochvolt Batterie Nullstromanforderung (Fehlerkategorie 5) |
| 0x2781 | Notlaufmanager -Hochvolt Batterie Anforderung schnelles Schuetze oeffnen (Fehlerkategorie 6) |
| 0x2782 | Notlaufmanager -Hochvolt Batterie Anforderung unmittelbares Schuetze oeffen (Fehlerkategorie 7) |
| 0x2972 | N/A |
| 0x27B0 | BEV13 |
| 0x27F1 | Interne Getriebeueberwachung -Parkposition aktuell nicht detektierbar |
| 0x27F2 | Interne Getriebeueberwachung -Parkposition aktuell eingelegt aktuell kein Fahrerwunsch Parken vorhanden |
| 0x27F3 | Interne Getriebeueberwachung -Parkposition aktuell nicht eingelegt aktuell Fahrerwunsch Parken vorhanden |
| 0x27F4 | Interner Fehler ShiftbyWire Ueberwachung -Geschwindigkeit unplausibel |
| 0x27F5 | Interner Fehler ShiftbyWire Ueberwachung -Falsche Anweisung |
| 0x27F6 | Interner Fehler ShiftbyWire Ueberwachung -Falsche Positionsanzeige |
| 0x282B | Lademanagement -Vorkonditionierung nicht moglich |
| 0x2973 | N/A |
| 0x2974 | N/A |
| 0x2975 | N/A |
| 0xCD9F | PT_CAN -Kommunikationsstoerung Botschaft (Codierung Powermanagement 0x395 Sender CAS) |
| 0xCD8C | PT_CAN -Kommunikationsstoerung Botschaft (Steuerung Crashabschaltung EKP 0x135 Sender MRSZ) |
| 0x2856 | Steuergeraet interner Fehler - stuck relay error |
| 0xCD8D | PT_CAN -Kommunikationsstoerung Botschaft (Drehmomentanforderung DSC 0xB6 Sender DSC) |
| 0x2857 | Steuergeraet interner Fehler - main relay dropout error |
| 0xCDA6 | A_CAN -Kommunikationsstoerung Botschaft (Daten Bremssystem Motorsteuerung 0x206 Sender AE) |
| 0xCDA7 | A_CAN -Kommunikationsstoerung Botschaft (Daten Antrieb Elektrisch 0x32F Sender AE) |
| 0xCDA8 | A_CAN -Kommunikationsstoerung Botschaft (Daten Hochvoltspeicher 0x431 Sender SME) |
| 0x2905 | Energiesparmode aktiv |
| 0xCDA9 | A_CAN -Kommunikationsstoerung Botschaft (Energieverbrauch Ladeelektronik 0x354 Sender AE) |
| 0xCDAA | A_CAN -Kommunikationsstoerung Botschaft (Fehlerstatus Ladeelektronik 0x359 Sender AE) |
| 0x283C | Ebene 2 Ueberwachung -Kommunikation PIC Watchdog Falsche Anfrage |
| 0x284A | Ebene 2 Ueberwachung - Double Storage Error |
| 0x2858 | Steuergeraet interner Fehler - ESM memory integrity error (All Code) |
| 0x2859 | Steuergeraet interner Fehler - ESM memory integrity error (All Data) |
| 0x285A | Steuergeraet interner Fehler - ESM memory integrity error (All Ram) |
| 0x2840 | Ebene 2 Ueberwachung -Code Pruefsummen Fehler |
| 0x2841 | Ebene 2 Ueberwachung -Daten Pruefsummen Fehler |
| 0x2842 | Ebene 2 Ueberwachung -RAM Pruefsummen Fehler |
| 0x285B | Steuergeraet interner Fehler - ESM L2 trip error |
| 0x285C | Steuergeraet interner Fehler - ESM L3 trip error |
| 0x285D | Steuergeraet interner Fehler - ESM Monitoring Module reset timeout |
| 0x285E | Steuergeraet interner Fehler - ESM trip error |
| 0x2843 | Ebene 2 Ueberwachung -Kein Clock vom Watchdog |
| 0x27D8 | Fahrpedalmodul -ESM Plausibilitaets Fehler |
| 0x2844 | Ebene 2 Ueberwachung -Programm Ablauf Fehler |
| 0x285F | Steuergeraet interner Fehler - ESM power off CAN shutdown fault |
| 0x2860 | Steuergeraet interner Fehler - ESM power off reset fault |
| 0x2845 | Steuergeraet interner Fehler -Referenzspannung zu hoch |
| 0x2847 | Ebene 2 Ueberwachung -Anfrage Fehler |
| 0x2861 | Steuergeraet interner Fehler - ESM L3 Shutoff path test error |
| 0x2848 | Ebene 2 Ueberwachung -Fehler Sicherheitskonzept |
| 0x2849 | Ebene 2 Ueberwachung -Unplausibilitaet Bremsdruck |
| 0x286E | Interner Fehler EWS-Daten: Pruefsummenfehler |
| 0x286F | Botschaft EWS-DME fehlerhaft: Zeitueberschreitung |
| 0x2870 | Botschaft EWS-DME fehlerhaft: Framefehler |
| 0x2871 | EWS Manipulationsschutz: kein Startwert programmiert |
| 0x2872 | EWS Manipulationsschutz: erwartete Antwort unplausibel |
| 0x2873 | Botschaft EWS-DME fehlerhaft: Framefehler |
| 0x2874 | Interner Fehler EWS-Daten: Schreibfehler Secret Key |
| 0xCD8E | PT_CAN -Kommunikationsstoerung Botschaft (Nachlaufzeit Stromversorgung 0x3BE Sender CAS) |
| 0xCD8F | PT_CAN -Kommunikationsstoerung Botschaft (Geschwindigkeit 0x1A0 Sender DSC) |
| 0xCD90 | PT_CAN -Kommunikationsstoerung Botschaft (Radgeschwindigkeit 0xCE Sender DSC) |
| 0x27E1 | Fahrpedalmodul -Pedalwertgeber 2 Analog Digital Wandler Test Fehler |
| 0xCDAB | A_CAN -Kommunikationsstoerung Botschaft (Identifikation Hochvoltspeicher 0x363 Sender SME) |
| 0xCD91 | PT_CAN -Kommunikationsstoerung Botschaft (Kilometerstand 0x330 Sender Kombi) |
| 0xCD92 | PT_CAN -Kommunikationsstoerung Botschaft (Klemmenstatus 0x130 Sender CAS) |
| 0x2718 | Plausibilitaetsueberwachung fuer FGR-Funktion (WMOM_PT_ENB / ST_DRASY_PT) |
| 0xCD93 | PT_CAN -Kommunikationsstoerung Botschaft (Lenkradwinkel 0xC4 Sender DSC) |
| 0xCD9E | PT_CAN -Kommunikationsstoerung Botschaft (Lenkradwinkel Oben 0xC8 Sender SZL_LWS) |
| 0xCDAC | A_CAN -Kommunikationsstoerung Botschaft (Begrenzung Ladung Entladung Hochvoltspeicher 0x2F5 Sender SME) |
| 0xCDAD | A_CAN -Kommunikationsstoerung Botschaft (Begrenzung Ladeelektronik 0x1F5 Sender AE) |
| 0x2742 | LIN BUS -Globaler Fehler Batteriesensor oder Wasserpumpe |
| 0x2743 | LIN BUS -Kommunikation zum Batteriesensor gestoert |
| 0x2744 | LIN BUS -Kommunikation zur Wasserpumpe gestoert |
| 0x2745 | LIN BUS -Kommunikation zur Wasserpumpe unplausibel |
| 0x2862 | Steuergeraet interner Fehler - ESM memory integrity error (Ram Parity error) |
| 0xCDAE | A_CAN -Kommunikationsstoerung Botschaft (Modus Spannungsgesteuert 0x432 Sender SME) |
| 0x2904 | Montagemodus aktiv |
| 0x27D9 | Fahrpedalmodul -Pedalwertgeber Sensor Korrelationsfehler |
| 0x27DB | Gaspedal und Bremspedalstellung -Kompatibilitaetsfehler Notlauf |
| 0x27DC | Gaspedal und Bremspedalstellung -Kompatibilitaetsfehler Leistungseinschraenkung |
| 0x27DD | Fahrpedalmodul -Pedal klemmt |
| 0x27DE | Fahrpedalmodul -Pedalwertgeber 1 Analog Digital Wandler Fehler |
| 0x27E2 | Fahrpedalmodul -Pedalwertgeber 2 Analog Digital Wandler Fehler |
| 0x271A | CEC Proximity  |
| 0xCD87 | PT_CAN -CAN Baustein Abschaltung |
| 0x2726 | Steuergeraet interner Fehler -EEPROM Zugriff nicht moeglich |
| 0x2727 | Steuergeraet interner Fehler -Daten inkonsistent |
| 0xCD9D | PT_CAN -Kommunikationsstoerung Botschaft (Status Anhaenger 0x2E4 Sender AHM) |
| 0xCD96 | PT_CAN -Kommunikationsstoerung Botschaft (Status DSC 0x19E Sender DSC) |
| 0xCD95 | PT_CAN -Kommunikationsstoerung Botschaft (Status Tuersensoren Abgesichert BN2000 0x1E1 Sender FRMFA) |
| 0xCD97 | A_CAN -Kommunikationsstoerung Botschaft (Status Hochvoltspeicher 2 0x112 Sender SME) |
| 0xCD98 | PT_CAN -Kommunikationsstoerung Botschaft (ZV und Klappenzustand 0x2FC Sender CAS) |
| 0xCDB9 | A_CAN -Kommunikationsstoerung Botschaft (Status Ladeschnittstelle 0x3B4 Sender KLE) |
| 0xCDB1 | A_CAN -Kommunikationsstoerung Botschaft (Status Ladung Hochvoltspeicher 2 0x430 Sender SME) |
| 0xCDB2 | A_CAN -Kommunikationsstoerung Botschaft (Status Ladung Hochvoltspeicher 3 0x3EB Sender SME) |
| 0xCDB3 | A_CAN -Kommunikationsstoerung Botschaft (Status DCDC 0x429 Sender AE) |
| 0xCD94 | PT_CAN -Kommunikationsstoerung Botschaft (Status Fahrererkennung 0x2F1 Sender MRSZ) |
| 0xCDB5 | A_CAN -Kommunikationsstoerung Botschaft (Status Heizung Hochvoltspeicher 0x2FF Sender SME) |
| 0xCDB6 | A_CAN -Kommunikationsstoerung Botschaft (Status Hochvoltspeicher 1 0x1AF Sender SME) |
| 0xCDB7 | A_CAN -Kommunikationsstoerung Botschaft (Status Begrenzung E Motor Traktion 0x2E8 Sender AE) |
| 0xCDA0 | PT_CAN -Kommunikationsstoerung Botschaft (Status Teleservice 0x436 Sender COMBOXMAIN) |
| 0xCD8B | PT_CAN -Kommunikationsstoerung Botschaft (Konfiguration Laden Hochvoltspeicher 0x340 Sender CIC) |
| 0xCDC2 | PT_CAN -Kommunikationsstoerung Botschaft (Dienste 0x5F8 Sender IHx) |
| 0xCDC3 | PT_CAN -Kommunikationsstoerung Botschaft (Dienste 0x5E0 Sender KOMBI) |
| 0x284E | Ebene 2 Ueberwachung -Fehler Beschleunigungsueberwachung |
| 0x284D | Ebene 2 Ueberwachung -Fehler Betriebsartenueberwachung |
| 0x284B | Ebene 2 Ueberwachung -Fehler Sollmomentenueberwachung |
| 0x284C | Ebene 2 Ueberwachung -Fehler Stillstandsueberwachung |
| 0x2852 | Ebene2-Ueberwachung: Fehler Istmoment der AE |
| 0x2850 | Ebene 2 Ueberwachung Fahreranwesenheit - Fehler Solldrehrichtung |
| 0x2851 | Ebene 2 Ueberwachung Fahreranwesenheit - Fehler Herstellung Fahrbereitschaft |
| 0x284F | Ebene 2 Ueberwachung -Fehler Fahrtrichtungsueberwachung |
| 0xCD99 | PT_CAN -Kommunikationsstoerung Botschaft (Uhrzeit/Datum 0x2F8 Sender Kombi) |
| 0x272E | Steuergeraet interner Fehler -Spannungsregler 1 Spannung ausserhalb gueltiger Bereich |
| 0x272F | Steuergeraet interner Fehler -Spannungsregler 2 Reglerfehler |
| 0x2731 | Steuergeraet interner Fehler -Spannungsregler 2 AUX Reglerfehler |
| 0xCD9A | PT_CAN -Kommunikationsstoerung Botschaft (Waermestrom Klima 0x1B5 Sender IHKA) |
| 0xFFFF | Unknown error location |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 250 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x2725 | 52 | 51 | 48 | 47 |
| 0xCD89 | 52 | 45 | 38 | 44 |
| 0xCDA1 | 52 | 45 | 38 | 44 |
| 0xCDBA | 52 | 45 | 38 | 44 |
| 0xCDA2 | 52 | 45 | 38 | 44 |
| 0xCDA3 | 52 | 45 | 38 | 44 |
| 0xCDA4 | 52 | 45 | 38 | 44 |
| 0xCDA5 | 52 | 45 | 38 | 44 |
| 0xCD86 | 52 | 45 | 38 | 44 |
| 0x2710 | 52 | 51 | 48 | 47 |
| 0x2711 | 52 | 51 | 48 | 47 |
| 0x2712 | 52 | 51 | 48 | 47 |
| 0x2713 | 52 | 6 | 5 | 47 |
| 0x2714 | 52 | 51 | 48 | 47 |
| 0x2715 | 52 | 51 | 48 | 47 |
| 0x271B | 52 | 51 | 48 | 47 |
| 0x2716 | 52 | 51 | 48 | 47 |
| 0xCD88 | 52 | 45 | 38 | 44 |
| 0x2717 | 52 | 6 | 5 | 47 |
| 0x2812 | 52 | 51 | 48 | 47 |
| 0xCD8A | 52 | 45 | 38 | 44 |
| 0xCD9B | 52 | 45 | 38 | 44 |
| 0x280A | 45 | 9 | 29 | 30 |
| 0x280B | 45 | 9 | 29 | 30 |
| 0x280C | 45 | 9 | 29 | 30 |
| 0x2838 | 45 | 9 | 29 | 30 |
| 0x2839 | 45 | 9 | 29 | 30 |
| 0x2817 | 45 | 9 | 29 | 30 |
| 0x280D | 45 | 9 | 29 | 30 |
| 0x280E | 45 | 9 | 29 | 30 |
| 0x280F | 45 | 9 | 29 | 30 |
| 0x2810 | 45 | 9 | 29 | 30 |
| 0x2811 | 45 | 9 | 29 | 30 |
| 0x283A | 45 | 9 | 29 | 30 |
| 0x27A9 | 52 | 51 | 48 | 47 |
| 0x2815 | 52 | 51 | 48 | 47 |
| 0x2816 | 52 | 51 | 48 | 47 |
| 0x27B1 | 52 | 51 | 48 | 47 |
| 0x27B2 | 52 | 51 | 48 | 47 |
| 0x27B3 | 52 | 51 | 48 | 47 |
| 0x27B4 | 52 | 51 | 48 | 47 |
| 0x27B5 | 52 | 51 | 48 | 47 |
| 0x27B6 | 52 | 51 | 48 | 47 |
| 0x27B7 | 52 | 51 | 48 | 47 |
| 0x27B8 | 52 | 51 | 48 | 47 |
| 0x27B9 | 52 | 51 | 48 | 47 |
| 0x27BA | 52 | 51 | 48 | 47 |
| 0x27BB | 52 | 51 | 48 | 47 |
| 0x27BC | 52 | 27 | 28 | 46 |
| 0x27BD | 52 | 18 | 19 | 26 |
| 0x27BE | 52 | 18 | 19 | 26 |
| 0x27BF | 52 | 18 | 19 | 26 |
| 0x27C0 | 52 | 18 | 19 | 26 |
| 0x2784 | 52 | 51 | 48 | 47 |
| 0x27C1 | 52 | 51 | 48 | 47 |
| 0x2774 | 52 | 51 | 48 | 47 |
| 0x2775 | 52 | 51 | 48 | 47 |
| 0x2776 | 52 | 51 | 48 | 47 |
| 0x2777 | 52 | 51 | 48 | 47 |
| 0x2968 | 52 | 51 | 48 | 47 |
| 0x27A6 | 52 | 51 | 48 | 47 |
| 0x27A7 | 52 | 51 | 48 | 47 |
| 0x27AD | 52 | 51 | 48 | 47 |
| 0x2969 | 52 | 51 | 48 | 47 |
| 0x27F7 | 52 | 51 | 48 | 47 |
| 0x2976 | 52 | 51 | 48 | 47 |
| 0x27E3 | 52 | 51 | 48 | 47 |
| 0x27E4 | 52 | 51 | 48 | 47 |
| 0x27E7 | 52 | 51 | 48 | 47 |
| 0x27E5 | 52 | 51 | 48 | 47 |
| 0x27E6 | 52 | 51 | 48 | 47 |
| 0x2786 | 52 | 51 | 48 | 47 |
| 0x2787 | 52 | 51 | 48 | 47 |
| 0x2788 | 52 | 51 | 48 | 47 |
| 0x2779 | 52 | 51 | 48 | 47 |
| 0x275B | 52 | 17 | 16 | 42 |
| 0x275C | 52 | 17 | 16 | 42 |
| 0x275D | 52 | 17 | 16 | 42 |
| 0x275E | 52 | 17 | 16 | 42 |
| 0x275F | 52 | 17 | 16 | 13 |
| 0x2760 | 52 | 17 | 16 | 13 |
| 0x2761 | 52 | 13 | 50 | 42 |
| 0x2762 | 52 | 13 | 50 | 42 |
| 0x2763 | 52 | 13 | 50 | 42 |
| 0x2764 | 52 | 13 | 50 | 42 |
| 0x27AB | 52 | 51 | 48 | 47 |
| 0x2820 | 52 | 18 | 19 | 26 |
| 0x27AA | 52 | 51 | 48 | 47 |
| 0x27AC | 52 | 51 | 48 | 47 |
| 0x282C | 52 | 27 | 28 | 46 |
| 0x282D | 52 | 27 | 28 | 46 |
| 0x282E | 52 | 27 | 28 | 46 |
| 0x2855 | 52 | 18 | 19 | 26 |
| 0x2821 | 52 | 18 | 19 | 26 |
| 0x2822 | 52 | 18 | 19 | 26 |
| 0x282F | 52 | 27 | 28 | 46 |
| 0x2830 | 52 | 27 | 28 | 46 |
| 0x274C | 45 | 9 | 29 | 30 |
| 0x274D | 45 | 9 | 29 | 30 |
| 0x274E | 45 | 9 | 29 | 30 |
| 0x274F | 45 | 9 | 29 | 30 |
| 0x2750 | 45 | 9 | 29 | 30 |
| 0x2751 | 45 | 9 | 29 | 30 |
| 0x2752 | 45 | 9 | 29 | 30 |
| 0x2753 | 45 | 9 | 29 | 30 |
| 0x2831 | 52 | 27 | 28 | 46 |
| 0x283B | 52 | 18 | 19 | 26 |
| 0x2823 | 52 | 18 | 19 | 26 |
| 0x2824 | 52 | 18 | 19 | 26 |
| 0x2825 | 52 | 18 | 19 | 26 |
| 0x2826 | 52 | 18 | 19 | 26 |
| 0x2827 | 52 | 18 | 19 | 26 |
| 0x2828 | 52 | 18 | 19 | 26 |
| 0x2836 | 52 | 18 | 19 | 26 |
| 0x2829 | 52 | 18 | 19 | 26 |
| 0x290F | 52 | 51 | 48 | 47 |
| 0x2910 | 52 | 51 | 48 | 47 |
| 0x27AE | 52 | 51 | 48 | 47 |
| 0x2970 | 52 | 51 | 48 | 47 |
| 0x296A | 52 | 51 | 48 | 47 |
| 0x296B | 52 | 51 | 48 | 47 |
| 0x296E | 52 | 51 | 48 | 47 |
| 0x296F | 52 | 51 | 48 | 47 |
| 0x296C | 52 | 51 | 48 | 47 |
| 0x296D | 52 | 51 | 48 | 47 |
| 0x2971 | 52 | 51 | 48 | 47 |
| 0x282A | 52 | 18 | 19 | 26 |
| 0x2837 | 52 | 18 | 19 | 26 |
| 0x27A8 | 52 | 51 | 48 | 47 |
| 0x27AF | 52 | 51 | 48 | 47 |
| 0x2832 | 52 | 27 | 28 | 46 |
| 0x2785 | 52 | 51 | 48 | 47 |
| 0x2833 | 52 | 27 | 28 | 32 |
| 0x2834 | 52 | 27 | 28 | 32 |
| 0x2835 | 52 | 27 | 28 | 32 |
| 0x2780 | 52 | 51 | 48 | 47 |
| 0x2783 | 52 | 51 | 48 | 47 |
| 0x2781 | 52 | 51 | 48 | 47 |
| 0x2782 | 52 | 51 | 48 | 47 |
| 0x2972 | 52 | 51 | 48 | 47 |
| 0x27B0 | 52 | 51 | 48 | 47 |
| 0x27F1 | 52 | 51 | 48 | 47 |
| 0x27F2 | 52 | 51 | 48 | 47 |
| 0x27F3 | 52 | 51 | 48 | 47 |
| 0x27F4 | 52 | 51 | 48 | 47 |
| 0x27F5 | 52 | 51 | 48 | 47 |
| 0x27F6 | 52 | 51 | 48 | 47 |
| 0x282B | 52 | 18 | 19 | 26 |
| 0x2973 | 52 | 51 | 48 | 47 |
| 0x2974 | 52 | 51 | 48 | 47 |
| 0x2975 | 52 | 51 | 48 | 47 |
| 0xCD9F | 52 | 45 | 38 | 44 |
| 0xCD8C | 52 | 45 | 38 | 44 |
| 0x2856 | 52 | 51 | 48 | 47 |
| 0xCD8D | 52 | 45 | 38 | 44 |
| 0x2857 | 52 | 51 | 48 | 47 |
| 0xCDA6 | 52 | 45 | 38 | 44 |
| 0xCDA7 | 52 | 45 | 38 | 44 |
| 0xCDA8 | 52 | 45 | 38 | 44 |
| 0x2905 | 52 | 51 | 48 | 47 |
| 0xCDA9 | 52 | 45 | 38 | 44 |
| 0xCDAA | 52 | 45 | 38 | 44 |
| 0x283C | 52 | 51 | 48 | 47 |
| 0x284A | 52 | 51 | 48 | 47 |
| 0x2858 | 52 | 51 | 48 | 47 |
| 0x2859 | 52 | 51 | 48 | 47 |
| 0x285A | 52 | 51 | 48 | 47 |
| 0x2840 | 52 | 51 | 48 | 47 |
| 0x2841 | 52 | 51 | 48 | 47 |
| 0x2842 | 52 | 51 | 48 | 47 |
| 0x285B | 52 | 51 | 48 | 47 |
| 0x285C | 52 | 51 | 48 | 47 |
| 0x285D | 52 | 51 | 48 | 47 |
| 0x285E | 52 | 51 | 48 | 47 |
| 0x2843 | 52 | 51 | 48 | 47 |
| 0x27D8 | 52 | 51 | 48 | 47 |
| 0x2844 | 52 | 51 | 48 | 47 |
| 0x285F | 52 | 51 | 48 | 47 |
| 0x2860 | 52 | 51 | 48 | 47 |
| 0x2845 | 52 | 51 | 48 | 47 |
| 0x2847 | 52 | 51 | 48 | 47 |
| 0x2861 | 52 | 51 | 48 | 47 |
| 0x2848 | 52 | 51 | 48 | 47 |
| 0x2849 | 52 | 51 | 48 | 47 |
| 0x286E | 52 | 51 | 48 | 47 |
| 0x286F | 52 | 51 | 48 | 47 |
| 0x2870 | 52 | 51 | 48 | 47 |
| 0x2871 | 52 | 51 | 48 | 47 |
| 0x2872 | 52 | 51 | 48 | 47 |
| 0x2873 | 52 | 51 | 48 | 47 |
| 0x2874 | 52 | 51 | 48 | 47 |
| 0xCD8E | 52 | 45 | 38 | 44 |
| 0xCD8F | 52 | 45 | 38 | 44 |
| 0xCD90 | 52 | 45 | 38 | 44 |
| 0x27E1 | 52 | 51 | 48 | 47 |
| 0xCDAB | 52 | 45 | 38 | 44 |
| 0xCD91 | 52 | 45 | 38 | 44 |
| 0xCD92 | 52 | 45 | 38 | 44 |
| 0x2718 | 52 | 45 | 38 | 44 |
| 0xCD93 | 52 | 45 | 38 | 44 |
| 0xCD9E | 52 | 45 | 38 | 44 |
| 0xCDAC | 52 | 45 | 38 | 44 |
| 0xCDAD | 52 | 45 | 38 | 44 |
| 0x2742 | 52 | 51 | 48 | 47 |
| 0x2743 | 45 | 9 | 29 | 30 |
| 0x2744 | 52 | 51 | 48 | 47 |
| 0x2745 | 52 | 51 | 48 | 47 |
| 0x2862 | 52 | 51 | 48 | 47 |
| 0xCDAE | 52 | 45 | 38 | 44 |
| 0x2904 | 52 | 51 | 48 | 47 |
| 0x27D9 | 52 | 51 | 48 | 47 |
| 0x27DB | 52 | 51 | 48 | 47 |
| 0x27DC | 52 | 51 | 48 | 47 |
| 0x27DD | 52 | 51 | 48 | 47 |
| 0x27DE | 52 | 51 | 48 | 47 |
| 0x27E2 | 52 | 51 | 48 | 47 |
| 0x271A | 52 | 51 | 48 | 47 |
| 0xCD87 | 52 | 45 | 38 | 44 |
| 0x2726 | 52 | 51 | 48 | 47 |
| 0x2727 | 52 | 51 | 48 | 47 |
| 0xCD9D | 52 | 45 | 38 | 44 |
| 0xCD96 | 52 | 45 | 38 | 44 |
| 0xCD95 | 52 | 45 | 38 | 44 |
| 0xCD97 | 52 | 45 | 38 | 44 |
| 0xCD98 | 52 | 45 | 38 | 44 |
| 0xCDB9 | 52 | 45 | 38 | 44 |
| 0xCDB1 | 52 | 45 | 38 | 44 |
| 0xCDB2 | 52 | 45 | 38 | 44 |
| 0xCDB3 | 52 | 45 | 38 | 44 |
| 0xCD94 | 52 | 45 | 38 | 44 |
| 0xCDB5 | 52 | 45 | 38 | 44 |
| 0xCDB6 | 52 | 45 | 38 | 44 |
| 0xCDB7 | 52 | 45 | 38 | 44 |
| 0xCDA0 | 52 | 45 | 38 | 44 |
| 0xCD8B | 52 | 45 | 38 | 44 |
| 0xCDC2 | 52 | 45 | 38 | 44 |
| 0xCDC3 | 52 | 45 | 38 | 44 |
| 0x284E | 52 | 51 | 48 | 47 |
| 0x284D | 52 | 51 | 48 | 47 |
| 0x284B | 52 | 51 | 48 | 47 |
| 0x284C | 52 | 51 | 48 | 47 |
| 0x2852 | 52 | 51 | 48 | 47 |
| 0x2850 | 52 | 51 | 48 | 47 |
| 0x2851 | 52 | 51 | 48 | 47 |
| 0x284F | 52 | 51 | 48 | 47 |
| 0xCD99 | 52 | 45 | 38 | 44 |
| 0x272E | 52 | 51 | 48 | 47 |
| 0x272F | 52 | 51 | 48 | 47 |
| 0x2731 | 52 | 51 | 48 | 47 |
| 0xCD9A | 52 | 45 | 38 | 44 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 52 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Auslastung DCDC-Wandler | - | high | unsigned char | - | 100 | 256 | 0 |
| 2 | Ist_Strom_Hochvoltspeicher | A | high | signed int | - | 1 | 10 | 0 |
| 3 | Ist_Spannung_Hochvoltspeicher | V | high | unsigned int | - | 1 | 10 | 0 |
| 4 | Ladezustand_Hochvoltspeicher | % | high | unsigned int | - | 1 | 10 | 0 |
| 5 | Hardwarestatus E-Luefter | % | high | unsigned char | - | 100 | 256 | 0 |
| 6 | Batterie Spannung eDME | V | high | signed int | - | 1 | 128 | 0 |
| 7 | Status Zuendung | - | high | unsigned long | - | 1 | 1 | 0 |
| 8 | Kilometer | Km | high | unsigned long | - | 1 | 1 | 0 |
| 9 | Batteriestrom vom IBS | A | high | unsigned int | - | 1 | 12.5 | -200 |
| 10 | Ist_Strom_Hochspannung_Zwischenkreis_E-Motor_Traktion | A | high | signed int | - | 1 | 4 | 0 |
| 11 | HV-Strom DCDC-Wandler | A | high | signed int | - | 1 | 10 | 0 |
| 12 | Ist-Strom Ladegeraet | A | high | signed int | - | 1 | 10 | 0 |
| 13 | Strom elektr. Wasserpumpe | A | high | signed int | - | 1 | 10 | 0 |
| 14 | Ist_Drehmoment_E-Motor_Traktion | Nm | high | signed int | - | 1 | 10 | 0 |
| 15 | Ist_Drehzahl_E-Motor_Traktion | 1/min | high | signed int | - | 1 | 1 | 0 |
| 16 | Istdrehzahl elektr. Wasserpumpe | rpm | high | unsigned char | - | 1 | 1 | 0 |
| 17 | Sollwert zum Ansteuern der EWP | rpm | high | unsigned char | - | 1 | 1 | 0 |
| 18 | Zustand Lademanager | HEX | high | signed long | - | 1 | 1 | 0 |
| 19 | letzte Uebergaenge Lademanager | HEX | high | signed long | - | 1 | 1 | 0 |
| 20 | Pedal Position | % | high | unsigned char | - | 1 | 128 | 0 |
| 21 | Raw information signal from Pedal track 1 | cnt | high | signed int | - | 1 | 1 | 0 |
| 22 | Raw information signal from Pedal track 2 | cnt | high | signed int | - | 1 | 1 | 0 |
| 23 | Q_iruhe1 | Ah | high | unsigned int | - | 18 | 989 | 0 |
| 24 | ENV_V_VEH | km/h | high | unsigned int | - | 1 | 64 | 0 |
| 25 | Fehlerstatus DCDC-Wandler | enum | high | signed int | - | 1 | 1 | 0 |
| 26 | Status Vorkonditionierung | - | high | unsigned char | - | 1 | 1 | 0 |
| 27 | Fehler HV-System | HEX | high | signed long | - | 1 | 1 | 0 |
| 28 | Status HV-System | - | high | unsigned char | - | 1 | 1 | 0 |
| 29 | LIN_ERR_ST_BYTE_02_IBS_LIN LIN ERR_ST_IBS_LIN | - | high | unsigned char | - | 1 | 1 | 0 |
| 30 | LIN_ERR_ST_BYTE_03_IBS_LIN LIN ERR_ST_IBS_LIN | - | high | unsigned char | - | 1 | 1 | 0 |
| 31 | ENV_ST_IO1_OUT | - | high | unsigned int | - | 1 | 1 | 0 |
| 32 | Status Signalfehler HVPM | - | high | unsigned long | - | 1 | 1 | 0 |
| 33 | STAT_SV_REG2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 34 | T2histshort | min | high | unsigned char | - | 224 | 15 | 0 |
| 35 | T3histshort | min | high | unsigned char | - | 224 | 15 | 0 |
| 36 | T4histshort | min | high | unsigned char | - | 224 | 15 | 0 |
| 37 | Ist_Temperatur_Hochvoltspeicher | grad | high | signed int | - | 1 | 10 | 0 |
| 38 | Batterietemperatur vom IBS gemessen | grad | high | signed int | - | 1 | 10 | 0 |
| 39 | Ist_Temperatur_DC/DC_Wandler | grad | high | signed int | - | 1 | 10 | 0 |
| 40 | Ist_Temperatur_E-Motor_1 | grad | high | signed int | - | 1 | 100 | 0 |
| 41 | Ist_Temperatur_Ladeelektronik | grad | high | signed int | - | 1 | 10 | 0 |
| 42 | Temperatur elektr. Wasserpumpe | grad | high | signed int | - | 1 | 100 | 0 |
| 43 | T_MOT | grad | high | signed int | - | 1 | 100 | 0 |
| 44 | Aussentemperatur | grad | high | signed int | - | 1 | 10 | 0 |
| 45 | Batteriespannung vom IBS | V | high | unsigned int | - | 1 | 4000 | 6 |
| 46 | Ist_Spannung_Hochspannung_Zwischenkreis_E-Motor_Traktion | V | high | unsigned int | - | 1 | 10 | 0 |
| 47 | Ist_Spannung_DC/DC_Wandler_Hochspannung | V | high | unsigned int | - | 1 | 50 | 0 |
| 48 | Ist_Spannung_Niederspannung_DC/DC_Wandler | V | high | unsigned int | - | 1 | 10 | 0 |
| 49 | Vorgabe Sollspannung | V | high | unsigned int | - | 1 | 10 | 0 |
| 50 | Spannung elektr. Wasserpumpe | V | high | unsigned char | - | 1 | 10 | 0 |
| 51 | Fahrzeuggeschwindigkeit | km/h | high | unsigned int | - | 1 | 10 | 0 |
| 52 | Relativzeit | HEX | high | signed long | - | 1 | 1 | 1 |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 257 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| default | 0x0008 | 0x0004 | 0x0002 | 0x0001 |
| 0x2750 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2833 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27AA | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2839 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDB3 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCDB9 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x271B | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x280D | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2717 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x27A8 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x283B | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x274F | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x296C | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2871 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27F7 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2810 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2844 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2779 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2849 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27AE | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2725 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x274E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2830 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2726 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2848 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2975 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2811 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2823 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2760 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2777 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x27E3 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDB6 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27C1 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2870 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2829 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x283C | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2718 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27C0 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2858 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD8D | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCDAA | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2745 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x285A | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2971 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x272F | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27B6 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x274D | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDA7 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27BA | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x275E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x280F | 0x0008 | 0x0004 | 0x000f | 0x0001 |
| 0x27B1 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27E2 | 0x0008 | 0x000a | 0x000f | 0x000e |
| 0x2816 | 0x0008 | 0x0004 | 0x000f | 0x0001 |
| 0x27DE | 0x0008 | 0x000a | 0x000f | 0x000e |
| 0xCDA2 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27BE | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x283E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2742 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x284D | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2862 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2825 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27F1 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2752 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27B3 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD96 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCD9B | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2788 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCDA1 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2713 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x2824 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2843 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2860 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2751 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x284C | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x285B | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2763 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x282E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD92 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2817 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2782 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD89 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27E7 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD98 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2727 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2826 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x280A | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27B9 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2820 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2976 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2785 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCD9F | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27A7 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x282B | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2716 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0xCD95 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27E6 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27BB | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2764 | 0x0008 | 0x0004 | 0x000f | 0x0001 |
| 0x275F | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x285E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x275B | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2970 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x296A | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCD88 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27B2 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD8E | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27F2 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27B5 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2831 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27AF | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2852 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDA6 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27F6 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2775 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27E1 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD8B | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x290F | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCD9D | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27AB | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD97 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2835 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2834 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2787 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x27B0 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2712 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x2910 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x27BF | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2861 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2874 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x296B | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCDAE | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCDA3 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x283D | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2857 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2730 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x284F | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD99 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2837 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x280B | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27DC | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2821 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2855 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x296E | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2744 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x274C | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2784 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x283F | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27DB | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDA0 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x284B | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDC3 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCDA9 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCD94 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCDAC | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2904 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2973 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2850 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27B8 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2840 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27F3 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x286F | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27E5 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD9E | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2774 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCDB7 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2776 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2715 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0xCDC2 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2856 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2762 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2842 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD91 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x275C | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x27AC | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2859 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27A6 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD8F | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCDA8 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2838 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDB5 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x282D | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27F5 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x296F | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2731 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2832 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2968 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x282A | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27BC | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2873 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2732 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x285C | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2827 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDB1 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2710 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x2781 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2845 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2743 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCD87 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCD8A | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27B7 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x285D | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDA4 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2905 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2780 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2822 | 0x0008 | 0x0004 | 0x000f | 0x0001 |
| 0x27A9 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x284A | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x296D | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCDAD | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2828 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x284E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x271A | 0x0014 | 0x0004 | 0x0013 | 0x0012 |
| 0x2836 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27F4 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27D9 | 0x0011 | 0x0010 | 0x0002 | 0x0001 |
| 0x2974 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x27DD | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2847 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27E4 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDAB | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2815 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x275D | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2972 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2714 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x2812 | 0x0008 | 0x000a | 0x000f | 0x000e |
| 0xCD90 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2841 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2783 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDB2 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x272E | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27AD | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2786 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCDBA | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x280E | 0x0008 | 0x0004 | 0x000f | 0x0001 |
| 0x27BD | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD8C | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCD86 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x286E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD9A | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x282F | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2846 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x283A | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2872 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2969 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCD93 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x285F | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x280C | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2851 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2753 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCDA5 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2711 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x27B4 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x282C | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27D8 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2761 | 0x0008 | 0x0004 | 0x0002 | 0x000e |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 18 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb Schwelle |
| 0x0002 | Signal oder Wert unterhalb Schwelle |
| 0x0004 | kein Signal oder Wert |
| 0x0008 | unplausibles Signal oder Wert |
| 0x0009 | Signal oder Wert unplausibel |
| 0x000a | kein Signal oder Wert |
| 0x000b | Leitungsunterbrechung |
| 0x000c | Kurzschluss nach Masse |
| 0x000d | Kurzschluss nach Ubat |
| 0x000e | Signal oder Wert oberhalb Schwelle |
| 0x000f | Signal oder Wert unterhalb Schwelle |
| 0x0010 | Sensor 1 |
| 0x0011 | Sensor 2 |
| 0x0012 | Spannung ueber Schwelle |
| 0x0013 | Spannung unter Schwelle |
| 0x0014 | ungueltige Spannung erkannt |
| 0xFFFF | unbekannte Fehlerart |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 251 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x2710 | Bremslichtschalter |
| 0x2711 | Charge Enable Control  |
| 0x2712 | Ladeleuchte  |
| 0x2713 | Elektroluefter Relais  |
| 0x2714 | Kuehlpumpe Notlaufeingang  |
| 0x2715 | Eingang MSA  |
| 0x2716 | Klemme 50  |
| 0x2717 | Ansteuerung Elektroluefter  |
| 0x2718 | Plausibilitaetsueberwachung fuer FGR-Funktion (WMOM_PT_ENB / ST_DRASY_PT) |
| 0x271A | CEC Proximity  |
| 0x271B | 12V Relais Ansteuerung  |
| 0x2725 | Steuergeraet interner Fehler -Analog Digital Wandler Fehler |
| 0x2726 | Steuergeraet interner Fehler -EEPROM Zugriff nicht moeglich |
| 0x2727 | Steuergeraet interner Fehler -Daten inkonsistent |
| 0x272E | Steuergeraet interner Fehler -Spannungsregler 1 Spannung ausserhalb gueltiger Bereich |
| 0x272F | Steuergeraet interner Fehler -Spannungsregler 2 Reglerfehler |
| 0x2731 | Steuergeraet interner Fehler -Spannungsregler 2 AUX Reglerfehler |
| 0x2742 | LIN BUS -Globaler Fehler Batteriesensor oder Wasserpumpe |
| 0x2743 | LIN BUS -Kommunikation zum Batteriesensor gestoert |
| 0x2744 | LIN BUS -Kommunikation zur Wasserpumpe gestoert |
| 0x2745 | LIN BUS -Kommunikation zur Wasserpumpe unplausibel |
| 0x274C | Intelligenter Batteriesensor -Kommunikation |
| 0x274D | Intelligenter Batteriesensor -Strommessung unplausibel |
| 0x274E | Intelligenter Batteriesensor -Firmware unplausibel |
| 0x274F | Intelligenter Batteriesensor -Systemfehler |
| 0x2750 | Intelligenter Batteriesensor -Temperaturmessung unplausibel |
| 0x2751 | Intelligenter Batteriesensor -Spannungsmessung unplausibel |
| 0x2752 | Intelligenter Batteriesensor -Wake Up Leitung Leitungsbruch |
| 0x2753 | Intelligenter Batteriesensor -Wake Up Leitung ueber oder unter Schwellwert |
| 0x275B | Kuehlmittelpumpe -Kommunikation |
| 0x275C | Kuehlmittelpumpe -Temperaturschwelle 1 ueberschritten |
| 0x275D | Kuehlmittelpumpe -Temperaturschwelle 2 ueberschritten |
| 0x275E | Kuehlmittelpumpe Kommunikation -Notlaufeingang Plausibilitaetsfehler |
| 0x275F | Kuehlmittelpumpe -Drehzahl ausserhalb Gueltigkeitsbereich |
| 0x2760 | Kuehlmittelpumpe -Trockenlauf |
| 0x2761 | Kuehlmittelpumpe -Ueberspannung |
| 0x2762 | Kuehlmittelpumpe -Ueberstrom |
| 0x2763 | Kuehlmittelpumpe -Uebertemperatur |
| 0x2764 | Kuehlmittelpumpe -Unterspannung |
| 0x2774 | Notlaufmanager -Abschaltung DCDC Wandler wegen Ueberstrom |
| 0x2775 | Notlaufmanager -Abschaltung DCDC Wandler wegen HW Fehler |
| 0x2776 | Notlaufmanager -DCDC Wandler Abschaltung wegen Uebertemperatur |
| 0x2777 | Notlaufmanager -DCDC Wandler Abschaltung wegen Spannungskriterium |
| 0x2779 | Notlaufmanager -Drehzahl der Elektromaschine hat Grenzwert ueberschritten |
| 0x2780 | Notlaufmanager -Hochvolt Batterie Service Request (Fehlerkategorie 3) |
| 0x2781 | Notlaufmanager -Hochvolt Batterie Anforderung schnelles Schuetze oeffnen (Fehlerkategorie 6) |
| 0x2782 | Notlaufmanager -Hochvolt Batterie Anforderung unmittelbares Schuetze oeffen (Fehlerkategorie 7) |
| 0x2783 | Notlaufmanager -Hochvolt Batterie Nullstromanforderung (Fehlerkategorie 5) |
| 0x2784 | Checkcontrol-Uebertemperatur Antrieb China |
| 0x2785 | Signalausfall-Moment und Betriebsartvorgabe E Maschine |
| 0x2786 | Notlaufmanager - Abschaltung wegen Fehlerbedingte Nullmomentenregelung |
| 0x2787 | Notlaufmanager - Abschaltung wegen Fehlerbedingter AKS |
| 0x2788 | Notlaufmanager - Abschaltung wegen Fehlerbedingter Freilauf |
| 0x27A6 | Betriebsstrategie -Begrenzung der Antriebsleistung Stufe 1 |
| 0x27A7 | Betriebsstrategie -Begrenzung der Antriebsleistung Stufe 2 |
| 0x27A8 | Betriebsstrategie -Begrenzung der Rekuperation |
| 0x27A9 | Bremspedal -Plausibilitaetsfehler |
| 0x27AA | Betriebsstrategie -Herstellen der Fahrbereitschaft wegen des gesteckten Ladekabels nicht moeglich |
| 0x27AB | Gaspedal und Bremspedalstellung -Plausibilitaetsfehler |
| 0x27AC | Betriebsstrategie -Herstellen der Fahrbereitschaft wegen des unplausiblen Ladekabelzustandes nur verzoegert moeglich |
| 0x27AD | BEV13 |
| 0x27AE | BEV13 |
| 0x27AF | BEV13 |
| 0x27B0 | BEV13 |
| 0x27B1 | Checkcontrol 174 -Getriebeposition P nur im Stillstand |
| 0x27B2 | Checkcontrol 175 -Getriebepostion P gestoert |
| 0x27B3 | Checkcontrol 203 -Getriebe in N Waschstrassenfunktion |
| 0x27B4 | Checkcontrol 220 -Erhoehte Batterieentladung |
| 0x27B5 | Checkcontrol 244 -Zum Gangeinlegen Bremse treten |
| 0x27B6 | Checkcontrol 250 -Gang ohne Bremse einlegebar |
| 0x27B7 | Checkcontrol 251 -Getriebeposition P wird eingelegt |
| 0x27B8 | Checkcontrol 252 -Gong bei ungenuegender P Betaetigung |
| 0x27B9 | Checkcontrol 394 -Waehlhebel gestoert |
| 0x27BA | Checkcontrol 557 -Fahrzeug gegen Wegrollen sichern |
| 0x27BB | Checkcontrol 565 -Getriebeposition P nur im Stillstand |
| 0x27BC | Checkcontrol 636 -Hochvoltsystem abgeschaltet |
| 0x27BD | Checkcontrol 802 -Ladekabel pruefen |
| 0x27BE | Checkcontrol 803 -Netzleistung zu gering |
| 0x27BF | Checkcontrol 804 -Laden nicht moeglich |
| 0x27C0 | Checkcontrol 809 -Zum Laden P einlegen |
| 0x27C1 | Checkcontrol - Ueberstrom Parkaktuator. P kann eventuell nicht mehr ausgelegt werden. |
| 0x27D8 | Fahrpedalmodul -ESM Plausibilitaets Fehler |
| 0x27D9 | Fahrpedalmodul -Pedalwertgeber Sensor Korrelationsfehler |
| 0x27DB | Gaspedal und Bremspedalstellung -Kompatibilitaetsfehler Notlauf |
| 0x27DC | Gaspedal und Bremspedalstellung -Kompatibilitaetsfehler Leistungseinschraenkung |
| 0x27DD | Fahrpedalmodul -Pedal klemmt |
| 0x27DE | Fahrpedalmodul -Pedalwertgeber 1 Analog Digital Wandler Fehler |
| 0x27E1 | Fahrpedalmodul -Pedalwertgeber 2 Analog Digital Wandler Test Fehler |
| 0x27E2 | Fahrpedalmodul -Pedalwertgeber 2 Analog Digital Wandler Fehler |
| 0x27E3 | Elektrische Unterdruckpumpe -Blockiert |
| 0x27E4 | Elektrische Unterdruckpumpe -Drucksensor Fehler |
| 0x27E5 | Elektrische Unterdruckpumpe -Leckage erkannt |
| 0x27E6 | Elektrische Unterdruckpumpe -Laufzeit Fehler |
| 0x27E7 | Elektrische Unterdruckpumpe - Ansteuerung seitens AE nicht moeglich elektrischer Fehler oder Montagemode aktiv |
| 0x27F1 | Interne Getriebeueberwachung -Parkposition aktuell nicht detektierbar |
| 0x27F2 | Interne Getriebeueberwachung -Parkposition aktuell eingelegt aktuell kein Fahrerwunsch Parken vorhanden |
| 0x27F3 | Interne Getriebeueberwachung -Parkposition aktuell nicht eingelegt aktuell Fahrerwunsch Parken vorhanden |
| 0x27F4 | Interner Fehler ShiftbyWire Ueberwachung -Geschwindigkeit unplausibel |
| 0x27F5 | Interner Fehler ShiftbyWire Ueberwachung -Falsche Anweisung |
| 0x27F6 | Interner Fehler ShiftbyWire Ueberwachung -Falsche Positionsanzeige |
| 0x27F7 | - |
| 0x280A | Powermanagement -Niedervoltbatterie defekt waehrend Transport |
| 0x280B | Powermanagement -Niedervoltbatterie entladen wahrend Transport |
| 0x280C | Powermanagement -Niedervoltbatterie Bordnetzinstabilitaet |
| 0x280D | Powermanagement -Ruhestromverletzung |
| 0x280E | Powermanagement -Niedervoltbatterie tiefentlanden |
| 0x280F | Powermanagement -Niedervolt Bordnetz Ueberspannung |
| 0x2810 | Powermanagement -Niedervolt Bordnetz Unterspannung |
| 0x2811 | Powermanagement -elektrische Verbraucher eingeschraenkt |
| 0x2812 | Spannungsversorgung -Wert unplausibel |
| 0x2815 | Niedervoltbatterie defekt |
| 0x2816 | Niedervoltbatterie tiefentlanden |
| 0x2817 | Powermanagement - Niedervoltbatterie wird nicht geladen |
| 0x2820 | Herstellen Fahrbereitschaft nicht moeglich wegen Temperatur HV-Batterie zu hoch |
| 0x2821 | Hochvoltbatterie - Temperatur verlaesst Normalbereich |
| 0x2822 | Hochvoltbatterie - Temperatur wieder im Normalbereich |
| 0x2823 | Lademanagement -AC Spannung fehlt nach Ladebeginn |
| 0x2824 | Lademanagement -AC Spannung dauerhaft instabil |
| 0x2825 | Lademanagement -SLE/KLE in Failsafe |
| 0x2826 | Lademanagement -Ladefehler |
| 0x2827 | Lademanagement -Ladeziel nicht erreichbar (SLE Leistung zu gering) |
| 0x2828 | Lademanagement -Ladeziel nicht erreichbar (Entladeschutz NV BN) |
| 0x2829 | Lademanagement -Ladestoerung |
| 0x282A | Lademanagement -Pilotsignal ungueltig |
| 0x282B | Lademanagement -Vorkonditionierung nicht moglich |
| 0x282C | HV Powermanagement -HV Power Down aufgrund niedrigem Ladezustand HV Batterie |
| 0x282D | HV Batterie -Isoaltionsfehler |
| 0x282E | HV Batterie -Isolationswarnung |
| 0x282F | HV Zwischenkreisentladung -HV Zwischenkreis nicht spannungsfrei trotz Anforderung |
| 0x2830 | HV Powermanagement -keine HV Freigabe trotz Anforderung |
| 0x2831 | HV Powermanagement -Interlock unterbrochen |
| 0x2832 | HV Batterie -einfacher Schuetzkleber |
| 0x2833 | Signalausfall -HV Powermanagement |
| 0x2834 | Signalausfall -Antriebselektronik |
| 0x2835 | Signalausfall -HV Batterie |
| 0x2836 | Lademanagement -Zustand Ladestecker unbekannt |
| 0x2837 | Lademanagement -Pilotsignal ungueltig ausserhalb Ladebereitschaft |
| 0x2838 | AEP -12 V Batterie wird nicht geladen |
| 0x2839 | AEP -12 V Batterie wird nicht geladen |
| 0x283A | AEP -12 V Batterie stark entladen |
| 0x283B | Lademanagement - AC-Spannung fehlt. HV-Speicher wird nicht geladen |
| 0x283C | Ebene 2 Ueberwachung -Kommunikation PIC Watchdog Falsche Anfrage |
| 0x2840 | Ebene 2 Ueberwachung -Code Pruefsummen Fehler |
| 0x2841 | Ebene 2 Ueberwachung -Daten Pruefsummen Fehler |
| 0x2842 | Ebene 2 Ueberwachung -RAM Pruefsummen Fehler |
| 0x2843 | Ebene 2 Ueberwachung -Kein Clock vom Watchdog |
| 0x2844 | Ebene 2 Ueberwachung -Programm Ablauf Fehler |
| 0x2845 | Steuergeraet interner Fehler -Referenzspannung zu hoch |
| 0x2847 | Ebene 2 Ueberwachung -Anfrage Fehler |
| 0x2848 | Ebene 2 Ueberwachung -Fehler Sicherheitskonzept |
| 0x2849 | Ebene 2 Ueberwachung -Unplausibilitaet Bremsdruck |
| 0x284A | Ebene 2 Ueberwachung - Double Storage Error |
| 0x284B | Ebene 2 Ueberwachung -Fehler Sollmomentenueberwachung |
| 0x284C | Ebene 2 Ueberwachung -Fehler Stillstandsueberwachung |
| 0x284D | Ebene 2 Ueberwachung -Fehler Betriebsartenueberwachung |
| 0x284E | Ebene 2 Ueberwachung -Fehler Beschleunigungsueberwachung |
| 0x284F | Ebene 2 Ueberwachung -Fehler Fahrtrichtungsueberwachung |
| 0x2850 | Ebene 2 Ueberwachung Fahreranwesenheit - Fehler Solldrehrichtung |
| 0x2851 | Ebene 2 Ueberwachung Fahreranwesenheit - Fehler Herstellung Fahrbereitschaft |
| 0x2852 | Ebene2-Ueberwachung: Fehler Istmoment der AE |
| 0x2855 | Hochvoltbatterie - Temperatur kritischer Wert |
| 0x2856 | Steuergeraet interner Fehler - stuck relay error |
| 0x2857 | Steuergeraet interner Fehler - main relay dropout error |
| 0x2858 | Steuergeraet interner Fehler - ESM memory integrity error (All Code) |
| 0x2859 | Steuergeraet interner Fehler - ESM memory integrity error (All Data) |
| 0x285A | Steuergeraet interner Fehler - ESM memory integrity error (All Ram) |
| 0x285B | Steuergeraet interner Fehler - ESM L2 trip error |
| 0x285C | Steuergeraet interner Fehler - ESM L3 trip error |
| 0x285D | Steuergeraet interner Fehler - ESM Monitoring Module reset timeout |
| 0x285E | Steuergeraet interner Fehler - ESM trip error |
| 0x285F | Steuergeraet interner Fehler - ESM power off CAN shutdown fault |
| 0x2860 | Steuergeraet interner Fehler - ESM power off reset fault |
| 0x2861 | Steuergeraet interner Fehler - ESM L3 Shutoff path test error |
| 0x2862 | Steuergeraet interner Fehler - ESM memory integrity error (Ram Parity error) |
| 0x286E | Interner Fehler EWS-Daten: Pruefsummenfehler |
| 0x286F | Botschaft EWS-DME fehlerhaft: Zeitueberschreitung |
| 0x2870 | Botschaft EWS-DME fehlerhaft: Framefehler |
| 0x2871 | EWS Manipulationsschutz: kein Startwert programmiert |
| 0x2872 | EWS Manipulationsschutz: erwartete Antwort unplausibel |
| 0x2873 | Botschaft EWS-DME fehlerhaft: Framefehler |
| 0x2874 | Interner Fehler EWS-Daten: Schreibfehler Secret Key |
| 0x2904 | Montagemodus aktiv |
| 0x2905 | Energiesparmode aktiv |
| 0x290F | Fehlerort 1 fur FSP Testfunktion Layer |
| 0x2910 | Fehlerort 2 fur FSP Testfunktion Layer |
| 0x2968 | N/A |
| 0x2969 | N/A |
| 0x296A | N/A |
| 0x296B | N/A |
| 0x296C | N/A |
| 0x296D | N/A |
| 0x296E | N/A |
| 0x296F | N/A |
| 0x2970 | N/A |
| 0x2971 | N/A |
| 0x2972 | N/A |
| 0x2973 | N/A |
| 0x2974 | N/A |
| 0x2975 | N/A |
| 0x2976 | Elektrische Unterdruckpumpe -Elektrischer Fehler |
| 0xCD86 | A_CAN -CAN Baustein Abschaltung |
| 0xCD87 | PT_CAN -CAN Baustein Abschaltung |
| 0xCD88 | PT_CAN -Kommunikationsstoerung Botschaft (Aussentemperatur/Relativzeit 0x310 Sender Kombi) |
| 0xCD89 | PT_CAN -Kommunikationsstoerung Botschaft (Anforderung Radmomente Antriebsstrang 0xBF Sender DSC) |
| 0xCD8A | PT_CAN -Kommunikationsstoerung Botschaft (Bedienung Getriebewahlschalter 0x198 Sender GWS) |
| 0xCD8B | PT_CAN -Kommunikationsstoerung Botschaft (Konfiguration Laden Hochvoltspeicher 0x340 Sender CIC) |
| 0xCD8C | PT_CAN -Kommunikationsstoerung Botschaft (Steuerung Crashabschaltung EKP 0x135 Sender MRSZ) |
| 0xCD8D | PT_CAN -Kommunikationsstoerung Botschaft (Drehmomentanforderung DSC 0xB6 Sender DSC) |
| 0xCD8E | PT_CAN -Kommunikationsstoerung Botschaft (Nachlaufzeit Stromversorgung 0x3BE Sender CAS) |
| 0xCD8F | PT_CAN -Kommunikationsstoerung Botschaft (Geschwindigkeit 0x1A0 Sender DSC) |
| 0xCD90 | PT_CAN -Kommunikationsstoerung Botschaft (Radgeschwindigkeit 0xCE Sender DSC) |
| 0xCD91 | PT_CAN -Kommunikationsstoerung Botschaft (Kilometerstand 0x330 Sender Kombi) |
| 0xCD92 | PT_CAN -Kommunikationsstoerung Botschaft (Klemmenstatus 0x130 Sender CAS) |
| 0xCD93 | PT_CAN -Kommunikationsstoerung Botschaft (Lenkradwinkel 0xC4 Sender DSC) |
| 0xCD94 | PT_CAN -Kommunikationsstoerung Botschaft (Status Fahrererkennung 0x2F1 Sender MRSZ) |
| 0xCD95 | PT_CAN -Kommunikationsstoerung Botschaft (Status Tuersensoren Abgesichert BN2000 0x1E1 Sender FRMFA) |
| 0xCD96 | PT_CAN -Kommunikationsstoerung Botschaft (Status DSC 0x19E Sender DSC) |
| 0xCD97 | A_CAN -Kommunikationsstoerung Botschaft (Status Hochvoltspeicher 2 0x112 Sender SME) |
| 0xCD98 | PT_CAN -Kommunikationsstoerung Botschaft (ZV und Klappenzustand 0x2FC Sender CAS) |
| 0xCD99 | PT_CAN -Kommunikationsstoerung Botschaft (Uhrzeit/Datum 0x2F8 Sender Kombi) |
| 0xCD9A | PT_CAN -Kommunikationsstoerung Botschaft (Waermestrom Klima 0x1B5 Sender IHKA) |
| 0xCD9B | PT_CAN -Kommunikationsstoerung Botschaft (Bedienung Taster MSA 0x195 Sender IHKA) |
| 0xCD9D | PT_CAN -Kommunikationsstoerung Botschaft (Status Anhaenger 0x2E4 Sender AHM) |
| 0xCD9E | PT_CAN -Kommunikationsstoerung Botschaft (Lenkradwinkel Oben 0xC8 Sender SZL_LWS) |
| 0xCD9F | PT_CAN -Kommunikationsstoerung Botschaft (Codierung Powermanagement 0x395 Sender CAS) |
| 0xCDA0 | PT_CAN -Kommunikationsstoerung Botschaft (Status Teleservice 0x436 Sender COMBOXMAIN) |
| 0xCDA1 | A_CAN -Kommunikationsstoerung Botschaft (Ist Daten DC/DC Wandler Ladeelektronik Langzeit 0x2C8 Sender AE) |
| 0xCDA2 | A_CAN -Kommunikationsstoerung Botschaft (Ist Daten Ladeelektronik 0x108 Sender AE) |
| 0xCDA3 | A_CAN -Kommunikationsstoerung Botschaft (Ist Daten E Motor Traktion 0x100 Sender AE) |
| 0xCDA4 | A_CAN -Kommunikationsstoerung Botschaft (Ist Daten E Motor Traktion Langzeit 0x2C9 Sender AE) |
| 0xCDA5 | A_CAN -Kommunikationsstoerung Botschaft (Ist Daten Parksperre 0x35B Sender AE) |
| 0xCDA6 | A_CAN -Kommunikationsstoerung Botschaft (Daten Bremssystem Motorsteuerung 0x206 Sender AE) |
| 0xCDA7 | A_CAN -Kommunikationsstoerung Botschaft (Daten Antrieb Elektrisch 0x32F Sender AE) |
| 0xCDA8 | A_CAN -Kommunikationsstoerung Botschaft (Daten Hochvoltspeicher 0x431 Sender SME) |
| 0xCDA9 | A_CAN -Kommunikationsstoerung Botschaft (Energieverbrauch Ladeelektronik 0x354 Sender AE) |
| 0xCDAA | A_CAN -Kommunikationsstoerung Botschaft (Fehlerstatus Ladeelektronik 0x359 Sender AE) |
| 0xCDAB | A_CAN -Kommunikationsstoerung Botschaft (Identifikation Hochvoltspeicher 0x363 Sender SME) |
| 0xCDAC | A_CAN -Kommunikationsstoerung Botschaft (Begrenzung Ladung Entladung Hochvoltspeicher 0x2F5 Sender SME) |
| 0xCDAD | A_CAN -Kommunikationsstoerung Botschaft (Begrenzung Ladeelektronik 0x1F5 Sender AE) |
| 0xCDAE | A_CAN -Kommunikationsstoerung Botschaft (Modus Spannungsgesteuert 0x432 Sender SME) |
| 0xCDB1 | A_CAN -Kommunikationsstoerung Botschaft (Status Ladung Hochvoltspeicher 2 0x430 Sender SME) |
| 0xCDB2 | A_CAN -Kommunikationsstoerung Botschaft (Status Ladung Hochvoltspeicher 3 0x3EB Sender SME) |
| 0xCDB3 | A_CAN -Kommunikationsstoerung Botschaft (Status DCDC 0x429 Sender AE) |
| 0xCDB5 | A_CAN -Kommunikationsstoerung Botschaft (Status Heizung Hochvoltspeicher 0x2FF Sender SME) |
| 0xCDB6 | A_CAN -Kommunikationsstoerung Botschaft (Status Hochvoltspeicher 1 0x1AF Sender SME) |
| 0xCDB7 | A_CAN -Kommunikationsstoerung Botschaft (Status Begrenzung E Motor Traktion 0x2E8 Sender AE) |
| 0xCDB9 | A_CAN -Kommunikationsstoerung Botschaft (Status Ladeschnittstelle 0x3B4 Sender KLE) |
| 0xCDBA | A_CAN -Kommunikationsstoerung Botschaft (Ist Daten Komfort Ladeelektronik Langzeit 0x211 Sender KLE) |
| 0xCDC2 | PT_CAN -Kommunikationsstoerung Botschaft (Dienste 0x5F8 Sender IHx) |
| 0xCDC3 | PT_CAN -Kommunikationsstoerung Botschaft (Dienste 0x5E0 Sender KOMBI) |
| 0xFFFF | Unknown error location |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 250 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x2725 | 52 | 51 | 48 | 47 |
| 0xCD89 | 52 | 45 | 38 | 44 |
| 0xCDA1 | 52 | 45 | 38 | 44 |
| 0xCDBA | 52 | 45 | 38 | 44 |
| 0xCDA2 | 52 | 45 | 38 | 44 |
| 0xCDA3 | 52 | 45 | 38 | 44 |
| 0xCDA4 | 52 | 45 | 38 | 44 |
| 0xCDA5 | 52 | 45 | 38 | 44 |
| 0xCD86 | 52 | 45 | 38 | 44 |
| 0x2710 | 52 | 51 | 48 | 47 |
| 0x2711 | 52 | 51 | 48 | 47 |
| 0x2712 | 52 | 51 | 48 | 47 |
| 0x2713 | 52 | 6 | 5 | 47 |
| 0x2714 | 52 | 51 | 48 | 47 |
| 0x2715 | 52 | 51 | 48 | 47 |
| 0x271B | 52 | 51 | 48 | 47 |
| 0x2716 | 52 | 51 | 48 | 47 |
| 0xCD88 | 52 | 45 | 38 | 44 |
| 0x2717 | 52 | 6 | 5 | 47 |
| 0x2812 | 52 | 51 | 48 | 47 |
| 0xCD8A | 52 | 45 | 38 | 44 |
| 0xCD9B | 52 | 45 | 38 | 44 |
| 0x280A | 45 | 9 | 29 | 30 |
| 0x280B | 45 | 9 | 29 | 30 |
| 0x280C | 45 | 9 | 29 | 30 |
| 0x2838 | 45 | 9 | 29 | 30 |
| 0x2839 | 45 | 9 | 29 | 30 |
| 0x2817 | 45 | 9 | 29 | 30 |
| 0x280D | 45 | 9 | 29 | 30 |
| 0x280E | 45 | 9 | 29 | 30 |
| 0x280F | 45 | 9 | 29 | 30 |
| 0x2810 | 45 | 9 | 29 | 30 |
| 0x2811 | 45 | 9 | 29 | 30 |
| 0x283A | 45 | 9 | 29 | 30 |
| 0x27A9 | 52 | 51 | 48 | 47 |
| 0x2815 | 52 | 51 | 48 | 47 |
| 0x2816 | 52 | 51 | 48 | 47 |
| 0x27B1 | 52 | 51 | 48 | 47 |
| 0x27B2 | 52 | 51 | 48 | 47 |
| 0x27B3 | 52 | 51 | 48 | 47 |
| 0x27B4 | 52 | 51 | 48 | 47 |
| 0x27B5 | 52 | 51 | 48 | 47 |
| 0x27B6 | 52 | 51 | 48 | 47 |
| 0x27B7 | 52 | 51 | 48 | 47 |
| 0x27B8 | 52 | 51 | 48 | 47 |
| 0x27B9 | 52 | 51 | 48 | 47 |
| 0x27BA | 52 | 51 | 48 | 47 |
| 0x27BB | 52 | 51 | 48 | 47 |
| 0x27BC | 52 | 27 | 28 | 46 |
| 0x27BD | 52 | 18 | 19 | 26 |
| 0x27BE | 52 | 18 | 19 | 26 |
| 0x27BF | 52 | 18 | 19 | 26 |
| 0x27C0 | 52 | 18 | 19 | 26 |
| 0x2784 | 52 | 51 | 48 | 47 |
| 0x27C1 | 52 | 51 | 48 | 47 |
| 0x2774 | 52 | 51 | 48 | 47 |
| 0x2775 | 52 | 51 | 48 | 47 |
| 0x2776 | 52 | 51 | 48 | 47 |
| 0x2777 | 52 | 51 | 48 | 47 |
| 0x2968 | 52 | 51 | 48 | 47 |
| 0x27A6 | 52 | 51 | 48 | 47 |
| 0x27A7 | 52 | 51 | 48 | 47 |
| 0x27AD | 52 | 51 | 48 | 47 |
| 0x2969 | 52 | 51 | 48 | 47 |
| 0x27F7 | 52 | 51 | 48 | 47 |
| 0x2976 | 52 | 51 | 48 | 47 |
| 0x27E3 | 52 | 51 | 48 | 47 |
| 0x27E4 | 52 | 51 | 48 | 47 |
| 0x27E7 | 52 | 51 | 48 | 47 |
| 0x27E5 | 52 | 51 | 48 | 47 |
| 0x27E6 | 52 | 51 | 48 | 47 |
| 0x2786 | 52 | 51 | 48 | 47 |
| 0x2787 | 52 | 51 | 48 | 47 |
| 0x2788 | 52 | 51 | 48 | 47 |
| 0x2779 | 52 | 51 | 48 | 47 |
| 0x275B | 52 | 17 | 16 | 42 |
| 0x275C | 52 | 17 | 16 | 42 |
| 0x275D | 52 | 17 | 16 | 42 |
| 0x275E | 52 | 17 | 16 | 42 |
| 0x275F | 52 | 17 | 16 | 13 |
| 0x2760 | 52 | 17 | 16 | 13 |
| 0x2761 | 52 | 13 | 50 | 42 |
| 0x2762 | 52 | 13 | 50 | 42 |
| 0x2763 | 52 | 13 | 50 | 42 |
| 0x2764 | 52 | 13 | 50 | 42 |
| 0x27AB | 52 | 51 | 48 | 47 |
| 0x2820 | 52 | 18 | 19 | 26 |
| 0x27AA | 52 | 51 | 48 | 47 |
| 0x27AC | 52 | 51 | 48 | 47 |
| 0x282C | 52 | 27 | 28 | 46 |
| 0x282D | 52 | 27 | 28 | 46 |
| 0x282E | 52 | 27 | 28 | 46 |
| 0x2855 | 52 | 18 | 19 | 26 |
| 0x2821 | 52 | 18 | 19 | 26 |
| 0x2822 | 52 | 18 | 19 | 26 |
| 0x282F | 52 | 27 | 28 | 46 |
| 0x2830 | 52 | 27 | 28 | 46 |
| 0x274C | 45 | 9 | 29 | 30 |
| 0x274D | 45 | 9 | 29 | 30 |
| 0x274E | 45 | 9 | 29 | 30 |
| 0x274F | 45 | 9 | 29 | 30 |
| 0x2750 | 45 | 9 | 29 | 30 |
| 0x2751 | 45 | 9 | 29 | 30 |
| 0x2752 | 45 | 9 | 29 | 30 |
| 0x2753 | 45 | 9 | 29 | 30 |
| 0x2831 | 52 | 27 | 28 | 46 |
| 0x283B | 52 | 18 | 19 | 26 |
| 0x2823 | 52 | 18 | 19 | 26 |
| 0x2824 | 52 | 18 | 19 | 26 |
| 0x2825 | 52 | 18 | 19 | 26 |
| 0x2826 | 52 | 18 | 19 | 26 |
| 0x2827 | 52 | 18 | 19 | 26 |
| 0x2828 | 52 | 18 | 19 | 26 |
| 0x2836 | 52 | 18 | 19 | 26 |
| 0x2829 | 52 | 18 | 19 | 26 |
| 0x290F | 52 | 51 | 48 | 47 |
| 0x2910 | 52 | 51 | 48 | 47 |
| 0x27AE | 52 | 51 | 48 | 47 |
| 0x2970 | 52 | 51 | 48 | 47 |
| 0x296A | 52 | 51 | 48 | 47 |
| 0x296B | 52 | 51 | 48 | 47 |
| 0x296E | 52 | 51 | 48 | 47 |
| 0x296F | 52 | 51 | 48 | 47 |
| 0x296C | 52 | 51 | 48 | 47 |
| 0x296D | 52 | 51 | 48 | 47 |
| 0x2971 | 52 | 51 | 48 | 47 |
| 0x282A | 52 | 18 | 19 | 26 |
| 0x2837 | 52 | 18 | 19 | 26 |
| 0x27A8 | 52 | 51 | 48 | 47 |
| 0x27AF | 52 | 51 | 48 | 47 |
| 0x2832 | 52 | 27 | 28 | 46 |
| 0x2785 | 52 | 51 | 48 | 47 |
| 0x2833 | 52 | 27 | 28 | 32 |
| 0x2834 | 52 | 27 | 28 | 32 |
| 0x2835 | 52 | 27 | 28 | 32 |
| 0x2780 | 52 | 51 | 48 | 47 |
| 0x2783 | 52 | 51 | 48 | 47 |
| 0x2781 | 52 | 51 | 48 | 47 |
| 0x2782 | 52 | 51 | 48 | 47 |
| 0x2972 | 52 | 51 | 48 | 47 |
| 0x27B0 | 52 | 51 | 48 | 47 |
| 0x27F1 | 52 | 51 | 48 | 47 |
| 0x27F2 | 52 | 51 | 48 | 47 |
| 0x27F3 | 52 | 51 | 48 | 47 |
| 0x27F4 | 52 | 51 | 48 | 47 |
| 0x27F5 | 52 | 51 | 48 | 47 |
| 0x27F6 | 52 | 51 | 48 | 47 |
| 0x282B | 52 | 18 | 19 | 26 |
| 0x2973 | 52 | 51 | 48 | 47 |
| 0x2974 | 52 | 51 | 48 | 47 |
| 0x2975 | 52 | 51 | 48 | 47 |
| 0xCD9F | 52 | 45 | 38 | 44 |
| 0xCD8C | 52 | 45 | 38 | 44 |
| 0x2856 | 52 | 51 | 48 | 47 |
| 0xCD8D | 52 | 45 | 38 | 44 |
| 0x2857 | 52 | 51 | 48 | 47 |
| 0xCDA6 | 52 | 45 | 38 | 44 |
| 0xCDA7 | 52 | 45 | 38 | 44 |
| 0xCDA8 | 52 | 45 | 38 | 44 |
| 0x2905 | 52 | 51 | 48 | 47 |
| 0xCDA9 | 52 | 45 | 38 | 44 |
| 0xCDAA | 52 | 45 | 38 | 44 |
| 0x283C | 52 | 51 | 48 | 47 |
| 0x284A | 52 | 51 | 48 | 47 |
| 0x2858 | 52 | 51 | 48 | 47 |
| 0x2859 | 52 | 51 | 48 | 47 |
| 0x285A | 52 | 51 | 48 | 47 |
| 0x2840 | 52 | 51 | 48 | 47 |
| 0x2841 | 52 | 51 | 48 | 47 |
| 0x2842 | 52 | 51 | 48 | 47 |
| 0x285B | 52 | 51 | 48 | 47 |
| 0x285C | 52 | 51 | 48 | 47 |
| 0x285D | 52 | 51 | 48 | 47 |
| 0x285E | 52 | 51 | 48 | 47 |
| 0x2843 | 52 | 51 | 48 | 47 |
| 0x27D8 | 52 | 51 | 48 | 47 |
| 0x2844 | 52 | 51 | 48 | 47 |
| 0x285F | 52 | 51 | 48 | 47 |
| 0x2860 | 52 | 51 | 48 | 47 |
| 0x2845 | 52 | 51 | 48 | 47 |
| 0x2847 | 52 | 51 | 48 | 47 |
| 0x2861 | 52 | 51 | 48 | 47 |
| 0x2848 | 52 | 51 | 48 | 47 |
| 0x2849 | 52 | 51 | 48 | 47 |
| 0x286E | 52 | 51 | 48 | 47 |
| 0x286F | 52 | 51 | 48 | 47 |
| 0x2870 | 52 | 51 | 48 | 47 |
| 0x2871 | 52 | 51 | 48 | 47 |
| 0x2872 | 52 | 51 | 48 | 47 |
| 0x2873 | 52 | 51 | 48 | 47 |
| 0x2874 | 52 | 51 | 48 | 47 |
| 0xCD8E | 52 | 45 | 38 | 44 |
| 0xCD8F | 52 | 45 | 38 | 44 |
| 0xCD90 | 52 | 45 | 38 | 44 |
| 0x27E1 | 52 | 51 | 48 | 47 |
| 0xCDAB | 52 | 45 | 38 | 44 |
| 0xCD91 | 52 | 45 | 38 | 44 |
| 0xCD92 | 52 | 45 | 38 | 44 |
| 0x2718 | 52 | 45 | 38 | 44 |
| 0xCD93 | 52 | 45 | 38 | 44 |
| 0xCD9E | 52 | 45 | 38 | 44 |
| 0xCDAC | 52 | 45 | 38 | 44 |
| 0xCDAD | 52 | 45 | 38 | 44 |
| 0x2742 | 52 | 51 | 48 | 47 |
| 0x2743 | 45 | 9 | 29 | 30 |
| 0x2744 | 52 | 51 | 48 | 47 |
| 0x2745 | 52 | 51 | 48 | 47 |
| 0x2862 | 52 | 51 | 48 | 47 |
| 0xCDAE | 52 | 45 | 38 | 44 |
| 0x2904 | 52 | 51 | 48 | 47 |
| 0x27D9 | 52 | 51 | 48 | 47 |
| 0x27DB | 52 | 51 | 48 | 47 |
| 0x27DC | 52 | 51 | 48 | 47 |
| 0x27DD | 52 | 51 | 48 | 47 |
| 0x27DE | 52 | 51 | 48 | 47 |
| 0x27E2 | 52 | 51 | 48 | 47 |
| 0x271A | 52 | 51 | 48 | 47 |
| 0xCD87 | 52 | 45 | 38 | 44 |
| 0x2726 | 52 | 51 | 48 | 47 |
| 0x2727 | 52 | 51 | 48 | 47 |
| 0xCD9D | 52 | 45 | 38 | 44 |
| 0xCD96 | 52 | 45 | 38 | 44 |
| 0xCD95 | 52 | 45 | 38 | 44 |
| 0xCD97 | 52 | 45 | 38 | 44 |
| 0xCD98 | 52 | 45 | 38 | 44 |
| 0xCDB9 | 52 | 45 | 38 | 44 |
| 0xCDB1 | 52 | 45 | 38 | 44 |
| 0xCDB2 | 52 | 45 | 38 | 44 |
| 0xCDB3 | 52 | 45 | 38 | 44 |
| 0xCD94 | 52 | 45 | 38 | 44 |
| 0xCDB5 | 52 | 45 | 38 | 44 |
| 0xCDB6 | 52 | 45 | 38 | 44 |
| 0xCDB7 | 52 | 45 | 38 | 44 |
| 0xCDA0 | 52 | 45 | 38 | 44 |
| 0xCD8B | 52 | 45 | 38 | 44 |
| 0xCDC2 | 52 | 45 | 38 | 44 |
| 0xCDC3 | 52 | 45 | 38 | 44 |
| 0x284E | 52 | 51 | 48 | 47 |
| 0x284D | 52 | 51 | 48 | 47 |
| 0x284B | 52 | 51 | 48 | 47 |
| 0x284C | 52 | 51 | 48 | 47 |
| 0x2852 | 52 | 51 | 48 | 47 |
| 0x2850 | 52 | 51 | 48 | 47 |
| 0x2851 | 52 | 51 | 48 | 47 |
| 0x284F | 52 | 51 | 48 | 47 |
| 0xCD99 | 52 | 45 | 38 | 44 |
| 0x272E | 52 | 51 | 48 | 47 |
| 0x272F | 52 | 51 | 48 | 47 |
| 0x2731 | 52 | 51 | 48 | 47 |
| 0xCD9A | 52 | 45 | 38 | 44 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 52 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Auslastung DCDC-Wandler | - | high | unsigned char | - | 100 | 256 | 0 |
| 2 | Ist_Strom_Hochvoltspeicher | A | high | signed int | - | 1 | 10 | 0 |
| 3 | Ist_Spannung_Hochvoltspeicher | V | high | unsigned int | - | 1 | 10 | 0 |
| 4 | Ladezustand_Hochvoltspeicher | % | high | unsigned int | - | 1 | 10 | 0 |
| 5 | Hardwarestatus E-Luefter | % | high | unsigned char | - | 100 | 256 | 0 |
| 6 | Batterie Spannung eDME | V | high | signed int | - | 1 | 128 | 0 |
| 7 | Status Zuendung | - | high | unsigned long | - | 1 | 1 | 0 |
| 8 | Kilometer | Km | high | unsigned long | - | 1 | 1 | 0 |
| 9 | Batteriestrom vom IBS | A | high | unsigned int | - | 1 | 12.5 | -200 |
| 10 | Ist_Strom_Hochspannung_Zwischenkreis_E-Motor_Traktion | A | high | signed int | - | 1 | 4 | 0 |
| 11 | HV-Strom DCDC-Wandler | A | high | signed int | - | 1 | 10 | 0 |
| 12 | Ist-Strom Ladegeraet | A | high | signed int | - | 1 | 10 | 0 |
| 13 | Strom elektr. Wasserpumpe | A | high | signed int | - | 1 | 10 | 0 |
| 14 | Ist_Drehmoment_E-Motor_Traktion | Nm | high | signed int | - | 1 | 10 | 0 |
| 15 | Ist_Drehzahl_E-Motor_Traktion | 1/min | high | signed int | - | 1 | 1 | 0 |
| 16 | Istdrehzahl elektr. Wasserpumpe | rpm | high | unsigned char | - | 1 | 1 | 0 |
| 17 | Sollwert zum Ansteuern der EWP | rpm | high | unsigned char | - | 1 | 1 | 0 |
| 18 | Zustand Lademanager | HEX | high | signed long | - | 1 | 1 | 0 |
| 19 | letzte Uebergaenge Lademanager | HEX | high | signed long | - | 1 | 1 | 0 |
| 20 | Pedal Position | % | high | unsigned char | - | 1 | 128 | 0 |
| 21 | Raw information signal from Pedal track 1 | cnt | high | signed int | - | 1 | 1 | 0 |
| 22 | Raw information signal from Pedal track 2 | cnt | high | signed int | - | 1 | 1 | 0 |
| 23 | Q_iruhe1 | Ah | high | unsigned int | - | 18 | 989 | 0 |
| 24 | ENV_V_VEH | km/h | high | unsigned int | - | 1 | 64 | 0 |
| 25 | Fehlerstatus DCDC-Wandler | enum | high | signed int | - | 1 | 1 | 0 |
| 26 | Status Vorkonditionierung | - | high | unsigned char | - | 1 | 1 | 0 |
| 27 | Fehler HV-System | HEX | high | signed long | - | 1 | 1 | 0 |
| 28 | Status HV-System | - | high | unsigned char | - | 1 | 1 | 0 |
| 29 | LIN_ERR_ST_BYTE_02_IBS_LIN LIN ERR_ST_IBS_LIN | - | high | unsigned char | - | 1 | 1 | 0 |
| 30 | LIN_ERR_ST_BYTE_03_IBS_LIN LIN ERR_ST_IBS_LIN | - | high | unsigned char | - | 1 | 1 | 0 |
| 31 | ENV_ST_IO1_OUT | - | high | unsigned int | - | 1 | 1 | 0 |
| 32 | Status Signalfehler HVPM | - | high | unsigned long | - | 1 | 1 | 0 |
| 33 | STAT_SV_REG2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 34 | T2histshort | min | high | unsigned char | - | 224 | 15 | 0 |
| 35 | T3histshort | min | high | unsigned char | - | 224 | 15 | 0 |
| 36 | T4histshort | min | high | unsigned char | - | 224 | 15 | 0 |
| 37 | Ist_Temperatur_Hochvoltspeicher | grad | high | signed int | - | 1 | 10 | 0 |
| 38 | Batterietemperatur vom IBS gemessen | grad | high | signed int | - | 1 | 10 | 0 |
| 39 | Ist_Temperatur_DC/DC_Wandler | grad | high | signed int | - | 1 | 10 | 0 |
| 40 | Ist_Temperatur_E-Motor_1 | grad | high | signed int | - | 1 | 100 | 0 |
| 41 | Ist_Temperatur_Ladeelektronik | grad | high | signed int | - | 1 | 10 | 0 |
| 42 | Temperatur elektr. Wasserpumpe | grad | high | signed int | - | 1 | 100 | 0 |
| 43 | T_MOT | grad | high | signed int | - | 1 | 100 | 0 |
| 44 | Aussentemperatur | grad | high | signed int | - | 1 | 10 | 0 |
| 45 | Batteriespannung vom IBS | V | high | unsigned int | - | 1 | 4000 | 6 |
| 46 | Ist_Spannung_Hochspannung_Zwischenkreis_E-Motor_Traktion | V | high | unsigned int | - | 1 | 10 | 0 |
| 47 | Ist_Spannung_DC/DC_Wandler_Hochspannung | V | high | unsigned int | - | 1 | 50 | 0 |
| 48 | Ist_Spannung_Niederspannung_DC/DC_Wandler | V | high | unsigned int | - | 1 | 10 | 0 |
| 49 | Vorgabe Sollspannung | V | high | unsigned int | - | 1 | 10 | 0 |
| 50 | Spannung elektr. Wasserpumpe | V | high | unsigned char | - | 1 | 10 | 0 |
| 51 | Fahrzeuggeschwindigkeit | km/h | high | unsigned int | - | 1 | 10 | 0 |
| 52 | Relativzeit | HEX | high | signed long | - | 1 | 1 | 1 |

<a id="table-iarttyp"></a>
### IARTTYP

Dimensions: 257 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| default | 0x0008 | 0x0004 | 0x0002 | 0x0001 |
| 0x2750 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2833 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27AA | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2839 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDB3 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCDB9 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x271B | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x280D | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2717 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x27A8 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x283B | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x274F | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x296C | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2871 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27F7 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2810 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2844 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2779 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2849 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27AE | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2725 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x274E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2830 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2726 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2848 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2975 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2811 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2823 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2760 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2777 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x27E3 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDB6 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27C1 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2870 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2829 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x283C | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2718 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27C0 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2858 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD8D | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCDAA | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2745 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x285A | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2971 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x272F | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27B6 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x274D | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDA7 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27BA | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x275E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x280F | 0x0008 | 0x0004 | 0x000f | 0x0001 |
| 0x27B1 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27E2 | 0x0008 | 0x000a | 0x000f | 0x000e |
| 0x2816 | 0x0008 | 0x0004 | 0x000f | 0x0001 |
| 0x27DE | 0x0008 | 0x000a | 0x000f | 0x000e |
| 0xCDA2 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27BE | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x283E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2742 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x284D | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2862 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2825 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27F1 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2752 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27B3 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD96 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCD9B | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2788 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCDA1 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2713 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x2824 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2843 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2860 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2751 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x284C | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x285B | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2763 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x282E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD92 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2817 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2782 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD89 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27E7 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD98 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2727 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2826 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x280A | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27B9 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2820 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2976 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2785 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCD9F | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27A7 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x282B | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2716 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0xCD95 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27E6 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27BB | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2764 | 0x0008 | 0x0004 | 0x000f | 0x0001 |
| 0x275F | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x285E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x275B | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2970 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x296A | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCD88 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27B2 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD8E | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27F2 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27B5 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2831 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27AF | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2852 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDA6 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27F6 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2775 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27E1 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD8B | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x290F | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCD9D | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27AB | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD97 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2835 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2834 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2787 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x27B0 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2712 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x2910 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x27BF | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2861 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2874 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x296B | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCDAE | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCDA3 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x283D | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2857 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2730 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x284F | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD99 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2837 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x280B | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27DC | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2821 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2855 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x296E | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2744 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x274C | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2784 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x283F | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27DB | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDA0 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x284B | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDC3 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCDA9 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCD94 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCDAC | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2904 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2973 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2850 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27B8 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2840 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27F3 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x286F | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27E5 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD9E | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2774 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCDB7 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2776 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2715 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0xCDC2 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2856 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2762 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2842 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD91 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x275C | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x27AC | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2859 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27A6 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD8F | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCDA8 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2838 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDB5 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x282D | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27F5 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x296F | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2731 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2832 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2968 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x282A | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27BC | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2873 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2732 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x285C | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2827 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDB1 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2710 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x2781 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2845 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2743 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCD87 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCD8A | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27B7 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x285D | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDA4 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2905 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2780 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2822 | 0x0008 | 0x0004 | 0x000f | 0x0001 |
| 0x27A9 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x284A | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x296D | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCDAD | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2828 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x284E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x271A | 0x0014 | 0x0004 | 0x0013 | 0x0012 |
| 0x2836 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27F4 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27D9 | 0x0011 | 0x0010 | 0x0002 | 0x0001 |
| 0x2974 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x27DD | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2847 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27E4 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDAB | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2815 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x275D | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2972 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0x2714 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x2812 | 0x0008 | 0x000a | 0x000f | 0x000e |
| 0xCD90 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2841 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2783 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCDB2 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x272E | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x27AD | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2786 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCDBA | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x280E | 0x0008 | 0x0004 | 0x000f | 0x0001 |
| 0x27BD | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD8C | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0xCD86 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x286E | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0xCD9A | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x282F | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2846 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x283A | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2872 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2969 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCD93 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x285F | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x280C | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2851 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2753 | 0x0008 | 0x0004 | 0x0002 | 0x000e |
| 0xCDA5 | 0x0008 | 0x000a | 0x0002 | 0x0001 |
| 0x2711 | 0x0008 | 0x000b | 0x000c | 0x000d |
| 0x27B4 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x282C | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x27D8 | 0x0009 | 0x0004 | 0x0002 | 0x0001 |
| 0x2761 | 0x0008 | 0x0004 | 0x0002 | 0x000e |

<a id="table-iarttexteindividuell"></a>
### IARTTEXTEINDIVIDUELL

Dimensions: 18 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb Schwelle |
| 0x0002 | Signal oder Wert unterhalb Schwelle |
| 0x0004 | kein Signal oder Wert |
| 0x0008 | unplausibles Signal oder Wert |
| 0x0009 | Signal oder Wert unplausibel |
| 0x000a | kein Signal oder Wert |
| 0x000b | Leitungsunterbrechung |
| 0x000c | Kurzschluss nach Masse |
| 0x000d | Kurzschluss nach Ubat |
| 0x000e | Signal oder Wert oberhalb Schwelle |
| 0x000f | Signal oder Wert unterhalb Schwelle |
| 0x0010 | Sensor 1 |
| 0x0011 | Sensor 2 |
| 0x0012 | Spannung ueber Schwelle |
| 0x0013 | Spannung unter Schwelle |
| 0x0014 | ungueltige Spannung erkannt |
| 0xFFFF | unbekannte Fehlerart |

<a id="table-msd85yl6-table-fs"></a>
### _MSD85YL6_TABLE_FS

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

<a id="table-msd85yl6-table-st-montagemodus-aktiv-inaktiv"></a>
### _MSD85YL6_TABLE_ST_MONTAGEMODUS_AKTIV_INAKTIV

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Montage-Modus ist inaktiv |
| 1 | Montage-Modus ist aktiv |

<a id="table-t-tab-edme-ladekabel"></a>
### T_TAB_EDME_LADEKABEL

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kein Kabel angesteckt |
| 1 | Kabel angesteckt |
| 2 | Fehler |
| 3 | Signal ungültig |

<a id="table-t-tab-edme-betriebsmode-dcdc"></a>
### T_TAB_EDME_BETRIEBSMODE_DCDC

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Standby |
| 2 | Buck |
| 3 | Error-State |
| 4 | Signal ungültig |

<a id="table-statclientauthtxt"></a>
### STATCLIENTAUTHTXT

Dimensions: 4 rows × 2 columns

| SB | TEXT |
| --- | --- |
| 0x00 | Freigabe (noch) nicht erteilt (noch nicht versucht oder Kommunikation gestört) |
| 0x01 | Freigabe erteilt (Challenge-Response erfolgreich) |
| 0x02 | Freigabe abgelehnt (Challenge-Response fehlgeschlagen, falsche Response, Kommunikation i.O.) |
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

<a id="table-tab-stat-st-diag-dcdc-modus"></a>
### TAB_STAT_ST_DIAG_DCDC_MODUS

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Antwort ausstehend |
| 1 | Erfolg |
| 2 | Fehler |

<a id="table-tab-stat-st-diag-dcdc-grenzen"></a>
### TAB_STAT_ST_DIAG_DCDC_GRENZEN

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | erfolgreich |
| 1 | nicht erfolgreich: mindestens eine geforderte Grenze verletzt eine Systemgrenze, stattdessen wird diese verwendet |

<a id="table-t-tab-st-b-diag-dcdc"></a>
### T_TAB_ST_B_DIAG_DCDC

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Soc_diag_lad_lmt verwenden |
| 2 | I_diag_dcdc_lv_out verwenden |
| 4 | I_diag_dcdc_hv_out verwenden |
| 8 | U_diag_dcdc_lv_out verwenden |
| 16 | U_diag_dcdc_hv_out verwenden |

<a id="table-t-tab-st-diag-dcdc-anf"></a>
### T_TAB_ST_DIAG_DCDC_ANF

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kontrolle an EME-SW |
| 1 | Anforderung Buck-Modus |
| 2 | Anforderung Boost-Modus |
| 3 | Anforderung Standby-Modus |

<a id="table-t-tab-edme-remote-laden"></a>
### T_TAB_EDME_REMOTE_LADEN

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | RemoteLaden nicht aktiv |
| 2 | RemoteLaden on Hold |
| 4 | RemoteLaden aktiv |
| 255 | ungültig |

<a id="table-t-tab-edme-status-laden"></a>
### T_TAB_EDME_STATUS_LADEN

Dimensions: 7 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | kein Laden |
| 2 | Ladestecker gesteckt - kein Laden |
| 4 | Laden aktiv |
| 8 | Laden beendet |
| 16 | Ladestörung |
| 32 | Ladefehler |
| 255 | ungültig |

<a id="table-t-tab-edme-timer-laden-nr"></a>
### T_TAB_EDME_TIMER_LADEN_NR

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | TimerLaden nicht aktiv |
| 2 | TimerLaden on Hold |
| 4 | TimerLaden aktiv |
| 255 | ungültig |

<a id="table-t-tab-eme-hvstart-komm"></a>
### T_TAB_EME_HVSTART_KOMM

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | HV aus |
| 1 | HV ein Anforderung |
| 2 | Freigabe HV |
| 3 | HV-Batterie Nullstromanforderung |
| 4 | HV Nachlauf 1 |
| 5 | HV Nachlauf 2 |
| 6 | Shutdown: Anforderung Schütze öffnen |
| 7 | Shutdown: Anforderung HV-Zwischenkreisentladung |
| 9 | Anforderung Batterieloser Betrieb |
| 10 | HV Batterieloser Betrieb: Anforderung Schütze öffnen |
| 11 | HV Batterieloser Betrieb aktiv |
| 12 | fehlerbedingter Shutdown: Rücknahme Freigabe HV |
| 13 | fehlerbedingter Shutdown: Anforderung Schütze öffnen |
| 14 | fehlerbedingter Shutdown: Anforderung HV-Zwischenkreisentladung |
| 15 | HV Störung |
| 16 | Initialisierung / ungültig |

<a id="table-t-tab-eme-i0anf-hvb"></a>
### T_TAB_EME_I0ANF_HVB

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Anforderung |
| 1 | Anforderung Nullstrom ohne EV: HV-Batteriefehler der Kategorie 5 oder geringe Ladeleistung |
| 2 | Anforderung Nullstrom mit EV: Entladeschutzfunktion HV-Batterie |
| 3 | Anforderung Nullstrom mit EV: HV-Power-Down |
| 4 | Anforderung Nullstrom mit EV: Batterieloser Betrieb |

<a id="table-t-tab-tsr-laden-stat-art-ladeanf-bit-0"></a>
### T_TAB_TSR_LADEN_STAT_ART_LADEANF_BIT_0

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Ladeanforderung HVB |
| 1 | Ladeanforderung HVB |

<a id="table-t-tab-tsr-laden-stat-art-ladeanf-bit-1"></a>
### T_TAB_TSR_LADEN_STAT_ART_LADEANF_BIT_1

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Vorkonditionierung |
| 1 | Vorkonditionierung |

<a id="table-t-tab-tsr-laden-stat-art-ladeanf-bit-2"></a>
### T_TAB_TSR_LADEN_STAT_ART_LADEANF_BIT_2

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Nachladeanforderung NVB |
| 1 | Nachladeanforderung NVB |

<a id="table-t-tab-tsr-laden-st-bedingung-ladestart"></a>
### T_TAB_TSR_LADEN_ST_BEDINGUNG_LADESTART

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Ungesteuertes Laden |
| 2 | Ladestart via CIC |
| 3 | Ladestart via Timer |
| 4 | Ladestart über Startfunktion I-Phone |
| 7 | ungueltig |

<a id="table-t-tab-tsr-laden-st-abbruchbedingung"></a>
### T_TAB_TSR_LADEN_ST_ABBRUCHBEDINGUNG

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Abbruch des Ladens aufgrund Fehlerzustand |
| 1 | Beenden des Ladevorgangs über Remotefunktion I-Phone |
| 2 | Beenden des Ladevorgangs durch Entriegeln des Ladesteckers |
| 3 | Ladeende bei Ziel-SoC erreicht |

<a id="table-t-tab-tsr-laden-st-reas-ldunterbr"></a>
### T_TAB_TSR_LADEN_ST_REAS_LDUNTERBR

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Gewalttrennung des Steckers |
| 2 | AC-Spannung fehlt oder Netzverbindung instabil |
| 3 | Stecker nicht verriegelt |
| 4 | Fehler: Hardwarefehler |
| 5 | Fehler: Unterspannung AC |
| 6 | Fehler: Überspannung AC |
| 7 | Fehler: Überstrom AC |
| 8 | Fehler: Unterspannung DC |
| 9 | Fehler: Überspannung DC |
| 10 | Fehler: Überstrom DC |
| 11 | Fehler Temperatur |
| 15 | ungueltig |

<a id="table-t-tab-tsr-laden-stat-reas-derating-bit-0"></a>
### T_TAB_TSR_LADEN_STAT_REAS_DERATING_BIT_0

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Übertemperatur |
| 1 | Übertemperatur |

<a id="table-t-tab-tsr-laden-stat-reas-derating-bit-1"></a>
### T_TAB_TSR_LADEN_STAT_REAS_DERATING_BIT_1

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Netzfrequenz nicht zu niedrig |
| 1 | Netzfrequenz zu niedrig |

<a id="table-t-tab-tsr-laden-stat-reas-derating-bit-2"></a>
### T_TAB_TSR_LADEN_STAT_REAS_DERATING_BIT_2

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Ausfall eines Lademoduls |
| 1 | Ausfall eines Lademoduls |

<a id="table-t-tab-tsr-laden-stat-reas-derating-bit-3"></a>
### T_TAB_TSR_LADEN_STAT_REAS_DERATING_BIT_3

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine DC-Strombegrenzung |
| 1 | DC-Strombegrenzung |

<a id="table-t-tab-tsr-laden-stat-reas-derating-bit-4"></a>
### T_TAB_TSR_LADEN_STAT_REAS_DERATING_BIT_4

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Netzseitig verfügbare Leistung nicht kleiner Nennleistung |
| 1 | Netzseitig verfügbare Leistung kleiner Nennleistung |

<a id="table-t-tab-tsr-laden-stat-anf-art-voko-bit-0"></a>
### T_TAB_TSR_LADEN_STAT_ANF_ART_VOKO_BIT_0

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Voko Innenraum |
| 1 | Voko Innenraum |

<a id="table-t-tab-tsr-laden-stat-anf-art-voko-bit-1"></a>
### T_TAB_TSR_LADEN_STAT_ANF_ART_VOKO_BIT_1

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Voko Innenraum forced |
| 1 | Voko Innenraum forced |

<a id="table-t-tab-tsr-laden-stat-anf-art-voko-bit-2"></a>
### T_TAB_TSR_LADEN_STAT_ANF_ART_VOKO_BIT_2

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Voko Batt |
| 1 | Voko Batt |

<a id="table-t-tab-tsr-laden-stat-anf-art-voko-bit-3"></a>
### T_TAB_TSR_LADEN_STAT_ANF_ART_VOKO_BIT_3

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine Voko Batt forced |
| 1 | Voko Batt forced |

<a id="table-t-tab-tsr-laden-stat-nachladeanforderung"></a>
### T_TAB_TSR_LADEN_STAT_NACHLADEANFORDERUNG

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Nachladeanforderung durch Wecken von IBS |
| 2 | Nachladeanforderung während das Fzg. wach war |
| 3 | ungueltig |

<a id="table-t-tab-tsr-laden-stat-zusatzinfo-abbruchbedingung"></a>
### T_TAB_TSR_LADEN_STAT_ZUSATZINFO_ABBRUCHBEDINGUNG

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Abbruch aufgrund min. HVB-SoC unterschritten |
| 2 | Abbruch aufgrund min. Nachladestrom NVB unterschritten |
| 4 | Abbruch aufgrund Status Kl. 15 |
| 8 | Abbruch aufgrund schlechter Ladebilanz |
| 15 | ungueltig |

<a id="table-motorudscodierung-ruhestrom"></a>
### _MOTORUDSCODIERUNG_RUHESTROM

Dimensions: 16 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Ruhestrom kleiner 80mA, keine Aktion des IBS |
| 1 | Ruhestrom = 80...200mA, keine Aktion da Entladung kleiner 1Ah |
| 2 | Ruhestrom = 200...1000mA, keine Aktion da Entladung kleiner 1Ah |
| 3 | Ruhestrom groesser 1000mA, keine Aktion da Entladung kleiner 1Ah |
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

<a id="table-t-tab-edme-ecopro"></a>
### T_TAB_EDME_ECOPRO

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ECOPro inaktiv |
| 1 | ECOPro aktiv |
