# SZL.prg

- Jobs: [75](#jobs)
- Tables: [21](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Schaltzentrum Lenksaeule |
| ORIGIN | BMW TI-430 R.Gall |
| REVISION | 3.07 |
| AUTHOR | BMW EE-53 Robert Schmidt, BMW TI-430 R.Gall, BMW EE-53 (Fa. Berata) Michael Burget |
| COMMENT | Serienstand E65, E60-besitzt keinen Gangwahlschalter, RR01 |
| PACKAGE | 1.32 |
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
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $00 all ECU Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus $04 requestIdentifiedShadowMemoryDTCAndStatus
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [STATUS_PORTS_LESEN](#job-status-ports-lesen) - Status der CPU-Ports lesen KWP2000: $22 SG spezifische Daten lesen $98 Status Ports lesen $02
- [LSG_NR_U_HERSTELLDATUM_U_X_SCHREIBEN](#job-lsg-nr-u-herstelldatum-u-x-schreiben) - Laufende Steuergeraetenummer und Herstelldatum und kleines x von HWREF ZZZPPPx schreiben KWP2000: $2E SG spezifische Daten schreiben $00 LSG Nummer und Herstelldatum und x schreiben $05 0x FF FF FF FF ist keine gueltige SG Nummer 0x FF FF FF FF ist kein gueltiges Herstelldatum YY YY MM DD ist BCD-Format des Herstelldatum kleines x sollte Charakter sein Modus  : Default
- [SYSTEMZEIT_LESEN](#job-systemzeit-lesen) - Systemzeit lesen KWP2000: $22 SG spezifische Daten lesen $00 Systemzeit lesen $02 Byte 1: Systemzeit gestartet: = 00 gestartet &lt;&gt; 00 nicht gestartet 0x FF FF FF FF FF ist keine gueltige Systemzeit Der Job liest nach Start aus dem RAM die aktuelle, sich aendernde Zeit aus Vor Systemzeitstart liest der Job aus EEPROM-Zellen (mit F...Fh gefuellt) Modus  : Default
- [SYSTEMZEIT_STARTEN](#job-systemzeit-starten) - Systemzeit starten KWP2000: $31 SG spezifische Routine starten $50 Systemzeit starten !!! ACHTUNG !!! Beim Start der Systemzeit werden die Airbags scharfgeschaltet und versch. Daten irreversibel verriegelt bis zum naechsten Flash-Update (Fahrgestellnummer, etc.) Das Starten der Systemzeit funktioniert nur, wenn eine Fahrgestellnummer eingetragen wurde!!!
- [STEUERN_ZURUECKNEHMEN_STEUERGERAETESTATUS](#job-steuern-zuruecknehmen-steuergeraetestatus) - Statusvorgaben zuruecknehmen KWP2000: $31 Steuergeraetespezifische Routine starten $20 Statusvorgaben zuruecknehmen $yz Status $yz zuruecknehmen Modus  : Default
- [STEUERN_KOMMUNIKATIONSTEST_SENDE_EMPFANG_ANSTOSSEN](#job-steuern-kommunikationstest-sende-empfang-anstossen) - Statusvorgabe: Kommunikationstest Sende Empfang anstossen KWP2000: $31 Steuergeraetespezifische Routine starten $27 Kommunikationstest Sende Empfang anstossen Modus  : Default
- [STEUERN_SI_BUS_STATUS_LESEN_ANSTOSSEN](#job-steuern-si-bus-status-lesen-anstossen) - Statusvorgabe: SI-Bus-Status lesen anstossen KWP2000: $31 Steuergeraetespezifische Routine starten $29 SI-Bus-Status lesen anstossen Modus  : Default
- [HERSTELLERDATEN_LESEN_40BYTES](#job-herstellerdaten-lesen-40bytes) - Herstellerdaten lesen Sonderjob 40 Bytes KWP2000: $22 SG spezifische Daten lesen $00 Herstellerdaten lesen $04 Modus  : Default
- [STEUERN_HUPE](#job-steuern-hupe) - Ansteuern von Hupe KWP2000: $31 Steuergeraetespezifische Routine starten $40 Hupe ansteuern Modus  : Default
- [STEUERN_DIMMBELEUCHTUNG](#job-steuern-dimmbeleuchtung) - Ansteuern der Dimmbeleuchtung KWP2000: $31 Steuergeraetespezifische Routine starten $41 Dimmbeleuchtung steuern Modus  : Default
- [STEUERN_FUNKTIONSBELEUCHTUNG](#job-steuern-funktionsbeleuchtung) - Ansteuern der Funktionsbeleuchtung KWP2000: $31 Steuergeraetespezifische Routine starten $42 Funktionsbeleuchtung ansteuern Modus  : Default
- [STEUERN_LENKRADHEIZUNG](#job-steuern-lenkradheizung) - Ansteuern der Lenkradheizung KWP2000: $31 Steuergeraetespezifische Routine starten $45 Funktionsbeleuchtung ansteuern Modus  : Default
- [STEUERN_LRE_FUNKTION](#job-steuern-lre-funktion) - Ansteuern der Lenkradfunktion KWP2000: $31 Steuergeraetespezifische Routine starten $46 Lenkradfunktion ansteuern Modus  : Default
- [ABGLEICH_LENKWINKELSENSOR](#job-abgleich-lenkwinkelsensor) - Abgleichen des Lenkwinkelsensors bei Lenkrad-Geradeausstellung KWP2000: $31 Steuergeraetespezifische Routine starten $43 Lenkwinkelsensor abgleichen Modus  : Default Vor diesem Job muss ABGLEICH_LENKWINKELSENSOR_RUECKSETZEN ausgefuehrt werden!
- [ABGLEICH_LENKWINKELSENSOR_RUECKSETZEN](#job-abgleich-lenkwinkelsensor-ruecksetzen) - Abgleichen des Lenkwinkelsensors zuruecksetzen KWP2000: $31 Steuergeraetespezifische Routine starten $44 Lenkwinkelsensor abgleichen ruecksetzen Modus  : Default Vor ABGLEICH_LENKWINKELSENSOR muss dieser Job ausgefuehrt werden!
- [STATUS_SERIENNUMMER_LRE_LESEN](#job-status-seriennummer-lre-lesen) - Seriennummer Lenkradelektronik auslesen KWP2000: $22 Steuergeraetespezifische Daten lesen $0006 Seriennummer LRE Modus  : Default
- [STATUS_LENKWINKELSENSOR](#job-status-lenkwinkelsensor) - Lenkwinkelsensor  auslesen KWP2000: $22 Steuergeraetespezifische Daten lesen $0007 Lenkwinkelsensor Lenkrad Modus  : Default
- [STATUS_LENKRADHEIZUNG](#job-status-lenkradheizung) - Status Lenkradheizung auslesen KWP2000: $22 Steuergeraetespezifische Daten lesen $0008 Status Lenkradheizung lesen Modus  : Default
- [LWS_OFFSET_SCHREIBEN](#job-lws-offset-schreiben) - Lenkwinkelsensoroffset schreiben KWP2000: $2E Steuergeraetespezifische Daten schreiben $00 Lenkwinkelsensoroffset schreiben $07 Modus  : Default E6X ab I4.20 E65 ab I6.89, Softwareversion 6.10.2  Notwendig bei SG-Tausch: Mit STATUS_LENKWINKELSENSOR STAT_OFFSET_LW_ABGLEICH_HIGH_BYTE, ...LOW_BYTE auslesen, aufschreiben. Mit LWS_OFFSET_SCHREIBEN ins neue SG schreiben
- [LWS_OFFSET_SCHREIBEN_GRAD](#job-lws-offset-schreiben-grad) - Lenkwinkelsensoroffset schreiben KWP2000: $2E Steuergeraetespezifische Daten schreiben $00 Lenkwinkelsensoroffset schreiben $07 Modus  : Default E6X ab I4.20 E65 ab I6.89, Softwareversion 6.10.2  Notwendig bei SG-Tausch: Mit STATUS_LENKWINKELSENSOR STAT_OFFSET_LW_ABGLEICH_WERT auslesen, aufschreiben. Mit LWS_OFFSET_SCHREIBEN_GRAD ins neue SG schreiben
- [LWS_OFFSET_KORREKTUR_SCHREIBEN_GRAD](#job-lws-offset-korrektur-schreiben-grad) - Lenkwinkelsensoroffset schreiben KWP2000: $2E Steuergeraetespezifische Daten schreiben $00 Korrektur Lenkwinkelsensoroffset schreiben $08 Modus  : Default E6X ab I4.60 E65 ab I6.89, Softwareversion 6.10.2  Notwendig nach Lenkwinkelsensor Abgleich in der Produktion:
- [LUZ_NULL_SETZEN](#job-luz-null-setzen) - Lenkradumdehungszahl auf Null setzen KWP2000: 0x31 0x48 Modus:   Default E6X ab FSV 5.5.1 E65 nicht möglich  Notwendig nach Codierung in der Produktion: unbedingt auf Geradeausstellung der Räder und des Lenkrades achten
- [STATUS_LESEN](#job-status-lesen) - Steuergeraete Status lesen KWP2000: $22 SG spezifische Daten lesen $98 Steuergeraete Status lesen $00 Modus  : Default
- [STATUS_AUSSTATTUNG_AIRBAGS](#job-status-ausstattung-airbags) - Statusausgabe, welche Airbags aktiv oder inaktiv codiert sind Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

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
| ID_SG_ADR | long | Steuergeraeteadresse |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |

<a id="job-c-fg-lesen"></a>
### C_FG_LESEN

Fahrgestellnummer lesen Standard Codierjob KWP2000: $1A ReadECUIdentification $90 Vehicle Identification Number Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer 7-stellig |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-blocklaenge-lesen"></a>
### FLASH_BLOCKLAENGE_LESEN

Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FLASH_BLOCKLAENGE_GESAMT | int | Flash Blocklaenge inclusive SID |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge |
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
| AUTHENTISIERUNG | string | Authentisierungsart 'Keine'        Keine Authentisierung 'Simple'       Einfache Authentisierung 'Symetrisch'   Symetrische Authentisierung 'Asymetrisch'  Asymetrische Authentisierung |
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
| FLASH_SCHREIBEN_ANZAHL | int | Anzahl FLASH_SCHREIBEN seit letztem FLASH_SCHREIBEN_ADRESSE |
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
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG AIF schreiben |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG AIF schreiben |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown $00 all ECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-loeschen"></a>
### IS_LOESCHEN

Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
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

<a id="job-status-ports-lesen"></a>
### STATUS_PORTS_LESEN

Status der CPU-Ports lesen KWP2000: $22 SG spezifische Daten lesen $98 Status Ports lesen $02

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_PORT_A_VAL | string | Status Port A |
| STAT_PORT_A_DDR | string | Status Port A Datenrichtungsregister |
| STAT_PORT_B_VAL | string | Status Port B |
| STAT_PORT_B_DDR | string | Status Port B Datenrichtungsregister |
| STAT_PORT_E_VAL | string | Status Port E |
| STAT_PORT_E_DDR | string | Status Port E Datenrichtungsregister |
| STAT_PORT_H_VAL | string | Status Port H |
| STAT_PORT_H_DDR | string | Status Port H Datenrichtungsregister |
| STAT_PORT_J_VAL | string | Status Port J |
| STAT_PORT_J_DDR | string | Status Port J Datenrichtungsregister |
| STAT_PORT_K_VAL | string | Status Port K |
| STAT_PORT_K_DDR | string | Status Port K Datenrichtungsregister |
| STAT_PORT_M_VAL | string | Status Port M |
| STAT_PORT_M_DDR | string | Status Port M Datenrichtungsregister |
| STAT_PORT_P_VAL | string | Status Port P |
| STAT_PORT_P_DDR | string | Status Port P Datenrichtungsregister |
| STAT_PORT_S_VAL | string | Status Port S |
| STAT_PORT_S_DDR | string | Status Port S Datenrichtungsregister |
| STAT_PORT_T_VAL | string | Status Port T |
| STAT_PORT_T_DDR | string | Status Port T Datenrichtungsregister |
| STAT_PORT_A_VAL_DEZ | unsigned int | Status Port A |
| STAT_PORT_A_DDR_DEZ | unsigned int | Status Port A Datenrichtungsregister |
| STAT_PORT_B_VAL_DEZ | unsigned int | Status Port B |
| STAT_PORT_B_DDR_DEZ | unsigned int | Status Port B Datenrichtungsregister |
| STAT_PORT_E_VAL_DEZ | unsigned int | Status Port E |
| STAT_PORT_E_DDR_DEZ | unsigned int | Status Port E Datenrichtungsregister |
| STAT_PORT_H_VAL_DEZ | unsigned int | Status Port H |
| STAT_PORT_H_DDR_DEZ | unsigned int | Status Port H Datenrichtungsregister |
| STAT_PORT_J_VAL_DEZ | unsigned int | Status Port J |
| STAT_PORT_J_DDR_DEZ | unsigned int | Status Port J Datenrichtungsregister |
| STAT_PORT_K_VAL_DEZ | unsigned int | Status Port K |
| STAT_PORT_K_DDR_DEZ | unsigned int | Status Port K Datenrichtungsregister |
| STAT_PORT_M_VAL_DEZ | unsigned int | Status Port M |
| STAT_PORT_M_DDR_DEZ | unsigned int | Status Port M Datenrichtungsregister |
| STAT_PORT_P_VAL_DEZ | unsigned int | Status Port P |
| STAT_PORT_P_DDR_DEZ | unsigned int | Status Port P Datenrichtungsregister |
| STAT_PORT_S_VAL_DEZ | unsigned int | Status Port S |
| STAT_PORT_S_DDR_DEZ | unsigned int | Status Port S Datenrichtungsregister |
| STAT_PORT_T_VAL_DEZ | unsigned int | Status Port T |
| STAT_PORT_T_DDR_DEZ | unsigned int | Status Port T Datenrichtungsregister |
| STAT_AD_0_0 | unsigned char | TEx: Klemme 30 |
| STAT_AD_0_1 | unsigned char | TEx: ASP Poti hor. |
| STAT_AD_0_2 | unsigned char | TEx: ASP Poti vert. |
| STAT_AD_0_3 | unsigned char | TEx: ASP Poti Versorgung |
| STAT_AD_0_4 | unsigned char | TEx: FH Hall Versorgung |
| STAT_AD_0_5 | unsigned char | TEx: FH - |
| STAT_AD_0_6 | unsigned char | TEx: FH + |
| STAT_AD_0_7 | unsigned char | TEx: Amb. Beleuchtung |
| STAT_AD_1_0 | unsigned char | TEx: SBLK Leuchte 2 |
| STAT_AD_1_1 | unsigned char | TEx: SBLK Leuchte 1 |
| STAT_AD_1_2 | unsigned char | TEx: SBLK Clock |
| STAT_AD_1_3 | unsigned char | TEx: Elmos 100.37 Diag |
| STAT_AD_1_4 | unsigned char | TEx: nicht verwendet |
| STAT_AD_1_5 | unsigned char | TEx: ZV-Icad MUX |
| STAT_AD_1_6 | unsigned char | TEx: ASP-Icad MUX |
| STAT_AD_1_7 | unsigned char | TEx: SBLK Latch |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lsg-nr-u-herstelldatum-u-x-schreiben"></a>
### LSG_NR_U_HERSTELLDATUM_U_X_SCHREIBEN

Laufende Steuergeraetenummer und Herstelldatum und kleines x von HWREF ZZZPPPx schreiben KWP2000: $2E SG spezifische Daten schreiben $00 LSG Nummer und Herstelldatum und x schreiben $05 0x FF FF FF FF ist keine gueltige SG Nummer 0x FF FF FF FF ist kein gueltiges Herstelldatum YY YY MM DD ist BCD-Format des Herstelldatum kleines x sollte Charakter sein Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LAUFENDE_SG_NR | unsigned long | Laufende Steuergeraetenummer 4 Bytes 0x0 - 0xFF FF FF FF |
| HERSTELLDATUM | unsigned long | Herstelldatum 4 Bytes BCD 0xYYYYMMDD |
| KLEINES_X | string | kleines x muss Charakter sein 0-9 oder A-Z damit er im PAF-Filenamen erscheinen kann |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-systemzeit-lesen"></a>
### SYSTEMZEIT_LESEN

Systemzeit lesen KWP2000: $22 SG spezifische Daten lesen $00 Systemzeit lesen $02 Byte 1: Systemzeit gestartet: = 00 gestartet &lt;&gt; 00 nicht gestartet 0x FF FF FF FF FF ist keine gueltige Systemzeit Der Job liest nach Start aus dem RAM die aktuelle, sich aendernde Zeit aus Vor Systemzeitstart liest der Job aus EEPROM-Zellen (mit F...Fh gefuellt) Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SZ_GESTARTET | unsigned int | Systemzeit gestartet: = 00 gestartet &lt;&gt; 00 nicht gestartet |
| SZ_BYTE_1 | unsigned int | Systemzeit Byte 1 0x0 - 0xFF bzw. 0 - 255 |
| SZ_BYTE_2 | unsigned int | Systemzeit Byte 2 0x0 - 0xFF bzw. 0 - 255 |
| SZ_BYTE_3 | unsigned int | Systemzeit Byte 3 0x0 - 0xFF bzw. 0 - 255 |
| SZ_BYTE_4 | unsigned int | Systemzeit Byte 4 0x0 - 0xFF bzw. 0 - 255 |
| SZ_BYTE_5 | unsigned int | Systemzeit Byte 5 0x0 - 0xFF bzw. 0 - 255 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-systemzeit-starten"></a>
### SYSTEMZEIT_STARTEN

Systemzeit starten KWP2000: $31 SG spezifische Routine starten $50 Systemzeit starten !!! ACHTUNG !!! Beim Start der Systemzeit werden die Airbags scharfgeschaltet und versch. Daten irreversibel verriegelt bis zum naechsten Flash-Update (Fahrgestellnummer, etc.) Das Starten der Systemzeit funktioniert nur, wenn eine Fahrgestellnummer eingetragen wurde!!!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| JOB_INFO_GELESEN | string | Dient nur zur Sicherheit, wird nicht im Telegramm verwendet "ja" -&gt; Job ausfuehren "1"  -&gt; Job ausfuehren table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-zuruecknehmen-steuergeraetestatus"></a>
### STEUERN_ZURUECKNEHMEN_STEUERGERAETESTATUS

Statusvorgaben zuruecknehmen KWP2000: $31 Steuergeraetespezifische Routine starten $20 Statusvorgaben zuruecknehmen $yz Status $yz zuruecknehmen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_ID | unsigned int | ID des zurueck zu nehmenden Status $00 = alle Stati zuruecknehmen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kommunikationstest-sende-empfang-anstossen"></a>
### STEUERN_KOMMUNIKATIONSTEST_SENDE_EMPFANG_ANSTOSSEN

Statusvorgabe: Kommunikationstest Sende Empfang anstossen KWP2000: $31 Steuergeraetespezifische Routine starten $27 Kommunikationstest Sende Empfang anstossen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATENBYTE_1 | unsigned int | Frei waehlbares Datenbyte 1 |
| DATENBYTE_2 | unsigned int | Frei waehlbares Datenbyte 2 |
| DATENBYTE_3 | unsigned int | Frei waehlbares Datenbyte 3 |
| DATENBYTE_4 | unsigned int | Frei waehlbares Datenbyte 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DATENBYTE_1 | unsigned int | Rueckantwort des Datenbyte 1 |
| STAT_DATENBYTE_2 | unsigned int | Rueckantwort des Datenbyte 2 |
| STAT_DATENBYTE_3 | unsigned int | Rueckantwort des Datenbyte 3 |
| STAT_DATENBYTE_4 | unsigned int | Rueckantwort des Datenbyte 4 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-si-bus-status-lesen-anstossen"></a>
### STEUERN_SI_BUS_STATUS_LESEN_ANSTOSSEN

Statusvorgabe: SI-Bus-Status lesen anstossen KWP2000: $31 Steuergeraetespezifische Routine starten $29 SI-Bus-Status lesen anstossen Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SI_BUS_ID | unsigned int | Zu lesende SI-Bus-ID |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LAENGE | unsigned int | Anzahl der Datenbytes in der Rueckantwort |
| STAT_DATENBYTES | binary | Rueckantwort Datenbytes |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-herstellerdaten-lesen-40bytes"></a>
### HERSTELLERDATEN_LESEN_40BYTES

Herstellerdaten lesen Sonderjob 40 Bytes KWP2000: $22 SG spezifische Daten lesen $00 Herstellerdaten lesen $04 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| HD_BYTE_1 | unsigned int | Herstellerdaten Byte 1 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_2 | unsigned int | Herstellerdaten Byte 2 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_3 | unsigned int | Herstellerdaten Byte 3 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_4 | unsigned int | Herstellerdaten Byte 4 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_5 | unsigned int | Herstellerdaten Byte 5 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_6 | unsigned int | Herstellerdaten Byte 6 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_7 | unsigned int | Herstellerdaten Byte 7 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_8 | unsigned int | Herstellerdaten Byte 8 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_9 | unsigned int | Herstellerdaten Byte 9 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_10 | unsigned int | Herstellerdaten Byte 10 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_11 | unsigned int | Herstellerdaten Byte 11 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_12 | unsigned int | Herstellerdaten Byte 12 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_13 | unsigned int | Herstellerdaten Byte 13 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_14 | unsigned int | Herstellerdaten Byte 14 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_15 | unsigned int | Herstellerdaten Byte 15 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_16 | unsigned int | Herstellerdaten Byte 16 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_17 | unsigned int | Herstellerdaten Byte 17 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_18 | unsigned int | Herstellerdaten Byte 18 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_19 | unsigned int | Herstellerdaten Byte 19 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_20 | unsigned int | Herstellerdaten Byte 20 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_21 | unsigned int | Herstellerdaten Byte 21 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_22 | unsigned int | Herstellerdaten Byte 22 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_23 | unsigned int | Herstellerdaten Byte 23 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_24 | unsigned int | Herstellerdaten Byte 24 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_25 | unsigned int | Herstellerdaten Byte 25 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_26 | unsigned int | Herstellerdaten Byte 26 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_27 | unsigned int | Herstellerdaten Byte 27 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_28 | unsigned int | Herstellerdaten Byte 28 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_29 | unsigned int | Herstellerdaten Byte 29 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_30 | unsigned int | Herstellerdaten Byte 30 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_31 | unsigned int | Herstellerdaten Byte 31 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_32 | unsigned int | Herstellerdaten Byte 32 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_33 | unsigned int | Herstellerdaten Byte 33 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_34 | unsigned int | Herstellerdaten Byte 34 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_35 | unsigned int | Herstellerdaten Byte 35 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_36 | unsigned int | Herstellerdaten Byte 36 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_37 | unsigned int | Herstellerdaten Byte 37 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_38 | unsigned int | Herstellerdaten Byte 38 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_39 | unsigned int | Herstellerdaten Byte 39 0x0 - 0xFF bzw. 0 - 255 |
| HD_BYTE_40 | unsigned int | Herstellerdaten Byte 40 0x0 - 0xFF bzw. 0 - 255 |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hupe"></a>
### STEUERN_HUPE

Ansteuern von Hupe KWP2000: $31 Steuergeraetespezifische Routine starten $40 Hupe ansteuern Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HUPEN_TOENER1 | string | "ein" -&gt; Hupe einschalten "aus" -&gt; Hupe ausschalten Bit 0 table DigitalArgument TEXT |
| HUPEN_TOENER2 | string | "ein" -&gt; Hupe einschalten "aus" -&gt; Hupe ausschalten Bit 1 table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dimmbeleuchtung"></a>
### STEUERN_DIMMBELEUCHTUNG

Ansteuern der Dimmbeleuchtung KWP2000: $31 Steuergeraetespezifische Routine starten $41 Dimmbeleuchtung steuern Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DIMMBELEUCHTUNGSWERT | unsigned int | Beleuchtungswert Bereich: 0 bis 253 -&gt; Nachtbeleuchtung Bereich: 254 -&gt; Tag (Lichtschalter aus) Bereich: 255 -&gt; Signal fehlerhaft, Licht aus |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-funktionsbeleuchtung"></a>
### STEUERN_FUNKTIONSBELEUCHTUNG

Ansteuern der Funktionsbeleuchtung KWP2000: $31 Steuergeraetespezifische Routine starten $42 Funktionsbeleuchtung ansteuern Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BELEUCHTUNG | string | "ein" -&gt; LEDs einschalten "aus" -&gt; LEDs ausschalten table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lenkradheizung"></a>
### STEUERN_LENKRADHEIZUNG

Ansteuern der Lenkradheizung KWP2000: $31 Steuergeraetespezifische Routine starten $45 Funktionsbeleuchtung ansteuern Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LENKRADHEIZUNG | string | "ein" -&gt; Heizung einschalten "aus" -&gt; Heizung ausschalten table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lre-funktion"></a>
### STEUERN_LRE_FUNKTION

Ansteuern der Lenkradfunktion KWP2000: $31 Steuergeraetespezifische Routine starten $46 Lenkradfunktion ansteuern Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LSE_CTL | long | siehe LRE Funktionstabelle Lastenheft |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LRE_ANSW3 | string | Antwortbyte 3 |
| STAT_LRE_ANSW4 | string | Antwortbyte 4 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-lenkwinkelsensor"></a>
### ABGLEICH_LENKWINKELSENSOR

Abgleichen des Lenkwinkelsensors bei Lenkrad-Geradeausstellung KWP2000: $31 Steuergeraetespezifische Routine starten $43 Lenkwinkelsensor abgleichen Modus  : Default Vor diesem Job muss ABGLEICH_LENKWINKELSENSOR_RUECKSETZEN ausgefuehrt werden!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleich-lenkwinkelsensor-ruecksetzen"></a>
### ABGLEICH_LENKWINKELSENSOR_RUECKSETZEN

Abgleichen des Lenkwinkelsensors zuruecksetzen KWP2000: $31 Steuergeraetespezifische Routine starten $44 Lenkwinkelsensor abgleichen ruecksetzen Modus  : Default Vor ABGLEICH_LENKWINKELSENSOR muss dieser Job ausgefuehrt werden!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-seriennummer-lre-lesen"></a>
### STATUS_SERIENNUMMER_LRE_LESEN

Seriennummer Lenkradelektronik auslesen KWP2000: $22 Steuergeraetespezifische Daten lesen $0006 Seriennummer LRE Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LRE_ID | string | Lenkradelektronik Seriennummer 6 Bytes |
| STAT_LRE_DATUM | string | Herstelldatum Lenkradelektronik BCD YYMMDD 20 FF FF FF ist kein gueltiges Herstelldatum |
| STAT_LRE_SW_VERSION | string | Lenkradelektronik Softwareversion |
| STAT_LRE_HW_VERSION | string | Lenkradelektronik Hardwareversion |
| STAT_LRE_BMW_TEILENUMMER | string | BMW Teilenummer |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lenkwinkelsensor"></a>
### STATUS_LENKWINKELSENSOR

Lenkwinkelsensor  auslesen KWP2000: $22 Steuergeraetespezifische Daten lesen $0007 Lenkwinkelsensor Lenkrad Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ANGENOMMENER_LW_WERT | real | Angenommener Lenkwinkel Bereich: +/-1439,95 Grad |
| STAT_ANGENOMMENER_LW_EINH | string | Einheit: Grad |
| STAT_LWS_AUFSETZALGO_FREIGESCHALTET | unsigned int | 0: Aufsetzalgorithmus nicht freigeschaltet 1: Aufsetzalgorithmus freigeschaltet |
| STAT_LWS_SER_LTGSDIAG_EINGESCHALTET | unsigned int | 0: serielle Leitungs-Diagnose nicht eingeschaltet 1: serielle Leitungs-Diagnose eingeschaltet |
| STAT_LWS_SYNTHETISCHER_LW_AKTIV | unsigned int | 0: relativer Lenkwinkel aktiv 1: synthetischer Lenkwinkel aktiv |
| STAT_LWS_LW_UMDREHUNG_BEKANNT | unsigned int | 0: Lenkwinkel Umdrehung NICHT bekannt 1: Lenkwinkel Umdrehung bekannt |
| STAT_LWS_FEHLERFLAG_GESETZT | unsigned int | 0: Fehlerflag NICHT gesetzt 1: Fehlerflag gesetzt |
| STAT_LWS_ABGEGLICHEN | unsigned int | 0: LWS nicht Abgeglichen 1: LWS Abgeglichen |
| STAT_SUMME_WICHTUNG_KL1 | string | Summe Wichtung Klasse 1 High / Low Byte Fuer Entwicklung |
| STAT_SUMME_WICHTUNG_KL2 | string | Fuer Entwicklung Summe Wichtung Klasse 2 High / Low Byte |
| STAT_SUMME_WICHTUNG_KL3 | string | Fuer Entwicklung Summe Wichtung Klasse 3 High / Low Byte |
| STAT_SUMME_WICHTUNG_KL4 | string | Summe Wichtung Klasse 4 High / Low Byte Fuer Entwicklung |
| STAT_SUMME_WICHTUNG_KL5 | string | Fuer Entwicklung Summe Wichtung Klasse 5 High / Low Byte |
| STAT_SUMME_WICHTUNG_KL6 | string | Summe Wichtung Klasse 6 High / Low Byte Fuer Entwicklung |
| STAT_SUMME_WICHTUNG_KL7 | string | Summe Wichtung Klasse 7 High / Low Byte Fuer Entwicklung |
| STAT_SUMME_WICHTUNG_KL8 | string | Summe Wichtung Klasse 8 High / Low Byte Fuer Entwicklung |
| STAT_SUMME_WICHTUNG_KL9 | string | Summe Wichtung Klasse 9 High / Low Byte Fuer Entwicklung |
| STAT_AKTUELLE_UMDREHUNGSZAHL_WERT | int | aktuelle Umdrehungszahl Lenkradgeradeausstellung: 0 Umdrehungen links drehen: neg., rechts drehen positive Umdrehungen |
| STAT_AKTUELLE_UMDREHUNGSZAHL_EINH | string | Einheit: "Umdrehungen" |
| STAT_OFFSET_LW_ABGLEICH_WERT | real | Offset des Lenkwinkel Abgleichs High / Low Byte Bereich: +/-1439,95 Grad |
| STAT_OFFSET_LW_ABGLEICH_EINH | string | Einheit: Grad |
| STAT_OFFSET_LW_ABGLEICH_HIGH_BYTE | int | Offset des Lenkwinkel Abgleichs High Byte Notwendig bei SG-Tausch: High- und Lowbyte auslesen, aufschreiben. Mit LWS_OFFSET_SCHREIBEN ins neue SG schreiben |
| STAT_OFFSET_LW_ABGLEICH_LOW_BYTE | int | Offset des Lenkwinkel Abgleichs Low Byte siehe ..._HIGH_BYTE |
| STAT_LW_MAX_WID_WERT | unsigned int | Lenkradwinkel Maximalwert Widerstand |
| STAT_LW_MAX_WID_EINH | string | Einheit: (Ink)remente 0-255 |
| STAT_LW_WID_SCHLEIFER1_WERT | unsigned int | Lenkradwinkel Widerstandswert Schleifer 1 |
| STAT_LW_WID_SCHLEIFER1_EINH | string | Lenkradwinkel Widerstandswert Schleifer 1 Einheit: (Ink)remente 0-255 |
| STAT_LW_WID_SCHLEIFER2_WERT | unsigned int | Lenkradwinkel Widerstandswert Schleifer 2 ohne Einheit |
| STAT_LW_WID_SCHLEIFER2_EINH | string | Lenkradwinkel Widerstandswert Schleifer 2 Einheit: (Ink)remente 0-255 |
| STAT_LW_GESCHW_WERT | real | Lenkradwinkel Geschwindigkeitswert High / Low Byte Bereich: +/-1439,95 Grad/s |
| STAT_LW_GESCHW_EINH | string | Einheit: Grad/s |
| STAT_ABSTIMMOFFSET_SCHLEIFER1_WERT | real | Abstimmoffset Schleifer 1 Bereich: +/-0,62V |
| STAT_ABSTIMMOFFSET_SCHLEIFER1_EINH | string | Einheit: V |
| STAT_ABSTIMMOFFSET_SCHLEIFER2_WERT | real | Abstimmoffset Schleifer 2 Bereich: +/-0,62V |
| STAT_ABSTIMMOFFSET_SCHLEIFER2_EINH | string | Einheit: V |
| STAT_ABSTIMMWERT_SCHLEIFERWINKEL_WERT | real | Abstimmwert Schleiferwinkel Bereich: +/- 5,62 Grad |
| STAT_ABSTIMMWERT_SCHLEIFERWINKEL_EINH | string | Einheit: V |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lenkradheizung"></a>
### STATUS_LENKRADHEIZUNG

Status Lenkradheizung auslesen KWP2000: $22 Steuergeraetespezifische Daten lesen $0008 Status Lenkradheizung lesen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LHZ_TEMPSENSOR_WERT | int | Status Lenkradheizung Temperatursensorwert Einheit: (Ink)remente 0-255 |
| STAT_LHZ_TEMPSENSOR_EINH | string | Status Lenkradheizung Temperatursensorwert Einheit: (Ink)remente |
| STAT_LHZ_SWITCH_DIAG_ANALOG_WERT | int | Status Lenkradheizung: Diagnose Pin LHZ Schalter Einheit: (Ink)remente 0-255 |
| STAT_LHZ_SWITCH_DIAG_ANALOG_EINH | string | Status Lenkradheizung: Diagnose Pin LHZ Schalter Einheit: (Ink)remente |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lws-offset-schreiben"></a>
### LWS_OFFSET_SCHREIBEN

Lenkwinkelsensoroffset schreiben KWP2000: $2E Steuergeraetespezifische Daten schreiben $00 Lenkwinkelsensoroffset schreiben $07 Modus  : Default E6X ab I4.20 E65 ab I6.89, Softwareversion 6.10.2  Notwendig bei SG-Tausch: Mit STATUS_LENKWINKELSENSOR STAT_OFFSET_LW_ABGLEICH_HIGH_BYTE, ...LOW_BYTE auslesen, aufschreiben. Mit LWS_OFFSET_SCHREIBEN ins neue SG schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LWS_OFFSET_HIGH | int | LWS-Offset High Byte |
| LWS_OFFSET_LOW | int | LWS-Offset low Byte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lws-offset-schreiben-grad"></a>
### LWS_OFFSET_SCHREIBEN_GRAD

Lenkwinkelsensoroffset schreiben KWP2000: $2E Steuergeraetespezifische Daten schreiben $00 Lenkwinkelsensoroffset schreiben $07 Modus  : Default E6X ab I4.20 E65 ab I6.89, Softwareversion 6.10.2  Notwendig bei SG-Tausch: Mit STATUS_LENKWINKELSENSOR STAT_OFFSET_LW_ABGLEICH_WERT auslesen, aufschreiben. Mit LWS_OFFSET_SCHREIBEN_GRAD ins neue SG schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LWS_OFFSET_GRAD | real | LWS-Offset in Grad Unbedingt ein PUNKT als Dezimaltrennzeichen benutzen Format: -123.456 Gueltigkeitsbereich: -140°..-110° |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lws-offset-korrektur-schreiben-grad"></a>
### LWS_OFFSET_KORREKTUR_SCHREIBEN_GRAD

Lenkwinkelsensoroffset schreiben KWP2000: $2E Steuergeraetespezifische Daten schreiben $00 Korrektur Lenkwinkelsensoroffset schreiben $08 Modus  : Default E6X ab I4.60 E65 ab I6.89, Softwareversion 6.10.2  Notwendig nach Lenkwinkelsensor Abgleich in der Produktion:

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LWS_OFFSET_KORREKTUR_GRAD | real | LWS-Offset in Grad Unbedingt ein PUNKT als Dezimaltrennzeichen benutzen Format: -0.123 Gueltigkeitsbereich: -1°..1° |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-luz-null-setzen"></a>
### LUZ_NULL_SETZEN

Lenkradumdehungszahl auf Null setzen KWP2000: 0x31 0x48 Modus:   Default E6X ab FSV 5.5.1 E65 nicht möglich  Notwendig nach Codierung in der Produktion: unbedingt auf Geradeausstellung der Räder und des Lenkrades achten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen"></a>
### STATUS_LESEN

Steuergeraete Status lesen KWP2000: $22 SG spezifische Daten lesen $98 Steuergeraete Status lesen $00 Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_READINESS_FLAG_BUS_AKTIV | unsigned int | Readiness Flag wird beim naechsten Fehlerspeicher loeschen zurueckgesetzt (Bit 0:) Bus aktiv (&gt;16sek. seit letztem Loeschen) |
| STAT_READINESS_FLAG_PREDRIVECHECK_DURCHGEFUEHRT | unsigned int | Readiness Flag wird beim naechsten Fehlerspeicher loeschen zurueckgesetzt (Bit 1:) 0 =  Pre-Drive-Check nicht durchgefuehrt 1 =  Pre-Drive-Check vollstaendig durchgefuehrt |
| STAT_READINESS_FLAG_SYSTEM_BETRIEBSFAEHIG | unsigned int | Readiness Flag wird beim naechsten Fehlerspeicher loeschen zurueckgesetzt (Bit 2:) 1 = System betriebsfaehig d. h. Klemme R ein und Pre-Drive-Check erfolgt |
| STAT_READINESS_FLAG_SYSTEM_ABGESCHALTET | unsigned int | (Bit 3:) 1 = System wurde abgeschaltet |
| STAT_READINESS_FLAG_KLEMME_15_EIN | unsigned int | Readiness Flag wird beim naechsten Fehlerspeicher loeschen zurueckgesetzt (Bit 4:) 1 = Klemme 15 ein |
| STAT_READINESS_FLAG_UISIS_EIN | unsigned int | Readiness Flag wird beim naechsten Fehlerspeicher loeschen zurueckgesetzt (Bit 5:) 1 = Spannung UISIS ein |
| STAT_READINESS_FLAG_LRE_KOMM_AKTIV | unsigned int | Readiness Flag wird beim naechsten Fehlerspeicher loeschen zurueckgesetzt (Bit 6:) 1 = LRE (Lenkradelektronik)-Kommunikation aktiv |
| STAT_KLEMMENSTATUS_BUS_KL_15_SIM_EIN | unsigned int | Klemmenstatus 15 vom SIM Byte 6 Bits 0,1 00: Kl. 15 aus 01: Kl. 15 ein 10: Signal ungueltig 11: Signal ungueltig |
| STAT_KLEMMENSTATUS_BUS_KL_15_SIM_TEXT | string | Klemmenstatus 15 vom SIM Byte 6 Bits 0,1 00: Kl. 15 aus 01: Kl. 15 ein 10: Signal ungueltig 11: Signal ungueltig |
| STAT_KLEMMENSTATUS_BUS_KL_R_SIM_EIN | unsigned int | Klemmenstatus R vom SIM Byte 6 Bits 2,3 00: Kl. R aus 01: Kl. R ein 10: Signal ungueltig 11: Signal ungueltig |
| STAT_KLEMMENSTATUS_BUS_KL_R_SIM_TEXT | string | Klemmenstatus R vom SIM Byte 6 Bits 2,3 00: Kl. R aus 01: Kl. R ein 10: Signal ungueltig 11: Signal ungueltig |
| STAT_SIM_SPG | unsigned int | Nur fuer Entwicklung Spannungsstatus vom SIM Byte 6 Bits 4,5 00: Unterspannung 01: Normalspannung 10: Ueberspannung 11: Signal ungueltig |
| STAT_SIM_SPG_TEXT | string | Nur fuer Entwicklung Spannungsstatus vom SIM Byte 6 Bits 4,5 00: Unterspannung 01: Normalspannung 10: Ueberspannung 11: Signal ungueltig |
| STAT_SIM_SPG_UNTERSPG_AKTIV | unsigned int | Spannungsstatus vom SIM Byte 6 Bits 4,5 1: Unterspannung |
| STAT_SIM_SPG_NORMALSPG_AKTIV | unsigned int | Spannungsstatus vom SIM Byte 6 Bits 4,5 1: Normalspannung |
| STAT_SIM_SPG_UEBERSPG_AKTIV | unsigned int | Spannungsstatus vom SIM Byte 6 Bits 4,5 1: Ueberspannung |
| STAT_KM_AKTUELL_WERT | long | aktueller Kilometerstand |
| STAT_KM_AKTUELL_EINH | string | KM |
| STAT_WIDERSTAND_ZK_1_WERT | real | Zuordnung Codierwert-Widerstand: CW = 50*R-40 0.84 &lt;= R/Ohm &lt;= 5.86 0x02 &lt;= R/Ohm &lt;= 0xFD Bewertung des Widerstandes ueber STAT_WIDERSTAND_ZK_1_TEXT Den Widerstandswert immer mit STAT_WIDERSTAND_ZK_1_TEXT ausgeben! 0x00 Widerstand der Zuendpille seit letztem POR noch nicht gemessen 0x01 Widerstand der Zuendpille kleiner 0.84 Ohm bzw. Kurzschluss 0x02 - 0xFD Widerstand der Zuendpille nach letztem Pre-Drive-Check 0xFE Widerstand der Zuendpille ist groesser als 5.86 Ohm 0xFF Fehler beim Messen des Zuendpillenwiderstands |
| STAT_WIDERSTAND_ZK_1_EINH | string | Einheit: Ohm |
| STAT_WIDERSTAND_ZK_1 | int | siehe oben bei *_WERT Byte fuer VS ausgegeben |
| STAT_WIDERSTAND_ZK_1_TEXT | string | siehe oben bei *_WERT |
| STAT_ZK_1_KS_UNTBR_HL_SIDE_SCHALTER | unsigned int | Bit 0: Kurzschluss oder Unterbrechung H/L-Side-Schalter ZK_1 |
| STAT_ZK_1_KS_MASSE | unsigned int | Bit 1: Kurzschluss ZK_1 nach Masse |
| STAT_ZK_1_KS_PLUS | unsigned int | Bit 2: Kurzschluss ZK_1 nach Plus |
| STAT_ZK_1_WID_ZUEPI_ZU_KLEIN | unsigned int | Bit 3: Widerstand Zuendpille ZK_1 zu klein |
| STAT_ZK_1_WID_ZUEPI_ZU_GROSS | unsigned int | Bit 4: Widerstand Zuendpille ZK_1 zu gross |
| STAT_ZK_1_KONNTE_NICHT_GEMES | unsigned int | Bit 5: Widerstand Zuendpille ZK_1 konnte nicht gemessen werden |
| STAT_ZK_1_UNTERBRECHUNG_ZUENDP | unsigned int | Bit 6: Unterbrechung Zuendpille ZK_1 |
| STAT_ZK_1_SPG_NIO | unsigned int | Bit 7: Zuendspannung ZK_1 n.i.O. |
| STAT_ZK_1_ZUENDKAPAZITAET_NIO | unsigned int | Bit 0: Zuendkapazitaet ZK_1 n.i.O. |
| STAT_ZK_1_CODIERUNG_UNSTIMMIG | unsigned int | Bit 1: Codierung / Konfiguration ZK_1 unstimmig |
| STAT_ZK_1_UNTERBRECHUNG_ENTLADEKREIS | unsigned int | Bit 2: Unterbrechung Entladekreis ZK_1 |
| STAT_ZK_1_KS_UNTERBR_L_SIDE_SCHALTER | unsigned int | Bit 3: Kurzschluss oder Unterbrechung Low-Side-Schalter ZK_1 |
| STAT_ZK_1_KS_UNTERBR_H_SIDE_SCHALTER | unsigned int | Bit 4: Kurzschluss oder Unterbrechung High-Side-Schalter ZK_1 |
| STAT_ZK_1_FEHLER_IM_ALARMPFAD | unsigned int | Bit 5: Fehler im Alarmpfad ZK_1 |
| STAT_ZK_1_BUSSTOERUNG_ALARM_PHASE_1 | unsigned int | Bit 6: Busstoerung/Alarm in Phase 1 ZK_1 |
| STAT_ZK_1_ZK_LINE_UNTERBRECHUNG | unsigned int | Bit 7: Busstoerung/Alarm in Phase 1 ZK_1 |
| STAT_WIDERSTAND_ZK_2_WERT | real | Zuordnung Codierwert-Widerstand: CW = 50*R-40 0.84 &lt;= R/Ohm &lt;= 5.86 0x02 &lt;= R/Ohm &lt;= 0xFD 0x00 Widerstand der Zuendpille seit letztem POR noch nicht gemessen 0x01 Widerstand der Zuendpille kleiner 0.84 Ohm bzw. Kurzschluss 0x02 - 0xFD Widerstand der Zuendpille nach letztem Pre-Drive-Check 0xFE Widerstand der Zuendpille ist groesser als 5.86 Ohm 0xFF Fehler beim Messen des Zuendpillenwiderstands |
| STAT_WIDERSTAND_ZK_2_EINH | string | Einheit: Ohm |
| STAT_WIDERSTAND_ZK_2 | int | siehe oben bei *_WERT Byte fuer VS ausgegeben |
| STAT_WIDERSTAND_ZK_2_TEXT | string | siehe oben bei *_WERT |
| STAT_ZK_2_KS_UNTBR_HL_SIDE_SCHALTER | unsigned int | Bit 0: Kurzschluss oder Unterbrechung H/L-Side-Schalter ZK_2 |
| STAT_ZK_2_KS_MASSE | unsigned int | Bit 1: Kurzschluss ZK_2 nach Masse |
| STAT_ZK_2_KS_PLUS | unsigned int | Bit 2: Kurzschluss ZK_2 nach Plus |
| STAT_ZK_2_WID_ZUEPI_ZU_KLEIN | unsigned int | Bit 3: Widerstand Zuendpille ZK_2 zu klein |
| STAT_ZK_2_WID_ZUEPI_ZU_GROSS | unsigned int | Bit 4: Widerstand Zuendpille ZK_2 zu gross |
| STAT_ZK_2_KONNTE_NICHT_GEMES | unsigned int | Bit 5: Widerstand Zuendpille ZK_2 konnte nicht gemessen werden |
| STAT_ZK_2_UNTERBRECHUNG_ZUENDP | unsigned int | Bit 6: Unterbrechung Zuendpille ZK_2 |
| STAT_ZK_2_SPG_NIO | unsigned int | Bit 7: Zuendspannung ZK_2 n.i.O. |
| STAT_ZK_2_ZUENDKAPAZITAET_NIO | unsigned int | Bit 0: Zuendkapazitaet ZK_2 n.i.O. Bit 7: frei |
| STAT_ZK_2_CODIERUNG_UNSTIMMIG | unsigned int | Bit 1: Codierung / Konfiguration ZK_2 unstimmig Bit 7: frei |
| STAT_ZK_2_UNTERBRECHUNG_ENTLADEKREIS | unsigned int | Bit 2: Unterbrechung Entladekreis ZK_2 Bit 7: frei |
| STAT_ZK_2_KS_UNTERBR_L_SIDE_SCHALTER | unsigned int | Bit 3: Kurzschluss oder Unterbrechung Low-Side-Schalter ZK_2 Bit 7: frei |
| STAT_ZK_2_KS_UNTERBR_H_SIDE_SCHALTER | unsigned int | Bit 4: Kurzschluss oder Unterbrechung High-Side-Schalter ZK_2 Bit 7: frei |
| STAT_ZK_2_FEHLER_IM_ALARMPFAD | unsigned int | Bit 5: Fehler im Alarmpfad ZK_2 Bit 7: frei |
| STAT_ZK_2_BUSSTOERUNG_ALARM_PHASE_1 | unsigned int | Bit 6: Busstoerung/Alarm in Phase 1 ZK_2 Bit 7: frei |
| STAT_GWS_GESAMT_1 | unsigned int | 0: Mittelstellung 1: Neutral vor R 2: Neutral vor D 3: Betaetigung D 4: Betaetigung R 5: Zwischenposition 6: Fehlerwert 7: frei Speziell fuer VS **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_GWS_GESAMT_2 | unsigned int | 0: Parktaster AUS 1: Parktaster EIN 2-7: frei Speziell fuer VS **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_HALLSENS_GWS | unsigned int | Bit 0-6: Getriebewahlschalter Rohsignal (7 Hallsensoren) 01110100 = 0x74  D 01011001 = 0x59  DN 01101010 = 0x6A  NA 01000111 = 0x47  RN 00101101 = 0x2D  R Bit 7: frei Aufsplittung auf einzelne Hallsensoren siehe unten **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_HALLSENS_1_GWS | unsigned int | Getriebewahlschalter Hallsensor 1 Bit 0 Muss sich bei Betaetigung aendern **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_HALLSENS_2_GWS | unsigned int | Getriebewahlschalter Hallsensor 1 Bit 1 Muss sich bei Betaetigung aendern **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_HALLSENS_3_GWS | unsigned int | Getriebewahlschalter Hallsensor 1 Bit 2 Muss sich bei Betaetigung aendern **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_HALLSENS_4_GWS | unsigned int | Getriebewahlschalter Hallsensor 1 Bit 3 Muss sich bei Betaetigung aendern **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_HALLSENS_5_GWS | unsigned int | Getriebewahlschalter Hallsensor 1 Bit 4 Muss sich bei Betaetigung aendern **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_HALLSENS_6_GWS | unsigned int | Getriebewahlschalter Hallsensor 1 Bit 5 Muss sich bei Betaetigung aendern **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_HALLSENS_7_GWS | unsigned int | Getriebewahlschalter Hallsensor 1 Bit 6 Muss sich bei Betaetigung aendern **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_GWS_NA | unsigned int | Bit 0-3: Getriebewahlschalter decodiert *000   NA  Mittelstellung, keine Aktion **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_GWS_RN_N_VOR_R | unsigned int | Bit 0-3: Getriebewahlschalter decodiert *001   RN  Neutral vor R **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_GWS_DN_N_VOR_D | unsigned int | Bit 0-3: Getriebewahlschalter decodiert *010   DN  Neutral vor D **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_GWS_D | unsigned int | Bit 0-3: Getriebewahlschalter decodiert *011   D   Betaetigung D **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_GWS_R | unsigned int | Bit 0-3: Getriebewahlschalter decodiert *100   R   Betaetigung R **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_GWS_ZP | unsigned int | Bit 0-3: Getriebewahlschalter decodiert *110   ZP   Zwischenposition **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_GWS_EINFACH_ERR | unsigned int | Bit 0-3: Getriebewahlschalter decodiert 1***   EINFACH_ERR Einfachfehler **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_GWS_SIG_UNGUELTIG | unsigned int | Bit 0-3: Getriebewahlschalter decodiert 1111   Signal ungueltig **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_GWS_P_TASTER_1 | unsigned int | Bit 4: PARK-Taster Kontakt 1 **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_GWS_P_TASTER_2 | unsigned int | Bit 5: PARK-Taster Kontakt 2 **** IM E60, E61, E63, E64 NICHT VORHANDEN!! **** |
| STAT_ABBLENDS_GESAMT_1 | unsigned int | 0: Fahrtrichtungsabblendschalter Mittelstellung 1: Fahrtrichtungsabblendschalter Blinken rechts Tipp 2: Fahrtrichtungsabblendschalter Blinken rechts Dauer 3: Fahrtrichtungsabblendschalter Blinken links Tipp 4: Fahrtrichtungsabblendschalter Blinken links Dauer 5: Fahrtrichtungsabblendschalter Fernlicht 6: Fahrtrichtungsabblendschalter Lichthupe 7: Mehrfachbetaetigung Speziell fuer VS |
| STAT_ABBLENDS_GESAMT_2 | unsigned int | 0: Fahrtrichtungsabblendschalter Axial Taster unten, oben keine Aktion 1: Fahrtrichtungsabblendschalter Axial Taster unten gedrueckt (Check Control) 2: Fahrtrichtungsabblendschalter Axial Taster oben gedrueckt (Bordcomputer) 3: Fahrtrichtungsabblendschalter Axial Taster beide Taster gedrueckt 4-7: frei Speziell fuer VS |
| STAT_ABBLENDSCHALT_MITTE | unsigned int | Bit 0-3: Fahrtrichtungsabblendschalter, Blinken 0000 Mittelstellung |
| STAT_ABBLENDSCHALT_BLINK_RE | unsigned int | Bit 0-3: Fahrtrichtungsabblendschalter, Blinken rechts 0001 BR Blinken rechts |
| STAT_ABBLENDSCHALT_BLINK_RE_DAUER | unsigned int | Bit 0-3: Fahrtrichtungsabblendschalter, Blinken rechts dauer 0010 BRD |
| STAT_ABBLENDSCHALT_BLINK_LI | unsigned int | Bit 0-3: Fahrtrichtungsabblendschalter, Blinken links 0100 BL |
| STAT_ABBLENDSCHALT_BLINK_LI_DAUER | unsigned int | Bit 0-3: Fahrtrichtungsabblendschalter, Blinken links dauer 1000 BLD |
| STAT_ABBLENDSCHALT_FERNLICHT | unsigned int | Bit 4: FL Fernlicht |
| STAT_ABBLENDSCHALT_LICHTHUPE | unsigned int | Bit 5: LH Lichthupe |
| STAT_ABBLENDSCHALT_AXIAL_UNTEN | unsigned int | Bit 6: Axial Taster unten |
| STAT_ABBLENDSCHALT_AXIAL_OBEN | unsigned int | Bit 7: Axial Taster oben |
| STAT_WISCHERS_GESAMT_1 | unsigned int | Wischerschalter 0: Keine Aktion horizontal, vertikal 1: Tippwischen (Taster nach unten) 2: Stufe 1 (Wischer-Taster nach oben druecken) 3: Stufe 2 (Wischer-Taster ueberdruecken) 4: Frontwaschen (Taster ziehen) 5: frei 6: Heckwischen (Taster druecken) (E60 Touring) 7: Heckwaschen (Taster ueberdruecken)(E60 Touring) 8: Mehrfachbetaetigung Speziell fuer VS |
| STAT_WISCHERS_GESAMT_2 | unsigned int | Wischerschalter 0: Axial Taster keine Aktion 1: Axial Taster gedrueckt 2-7: frei Speziell fuer VS |
| STAT_WISCHERS_GESAMT_3 | unsigned int | Wischerschalter 0: Wischerpotentiometer Stufe 1 1: Wischerpotentiometer Stufe 2 2: Wischerpotentiometer Stufe 3 3: Wischerpotentiometer Stufe 4 4: Fehlerwert 5-7: frei Speziell fuer VS |
| STAT_WISCHER_ROH_REGENSENSOR | unsigned int | Wischerschalter, Rohsignal Bit 0 (Axialtaster): Regensensor einschalten bei SA Regensensor OFF Wischen ausschalten ohne SA Regensensor |
| STAT_WISCHER_ROH_KEINE_AKTION_1 | unsigned int | Bit 1-3: 000 Keine Aktion 1 |
| STAT_WISCHER_ROH_TIPPWISCHEN | unsigned int | Bit 1-3: 001 TW Tippwischen |
| STAT_WISCHER_ROH_STUFE_1 | unsigned int | Bit 1-3: 010 S1 Stufe 1 |
| STAT_WISCHER_ROH_STUFE_2 | unsigned int | Bit 1-3: 100 S2 Stufe 2 |
| STAT_WISCHER_ROH_KEINE_AKTION_2 | unsigned int | Bit 4-6: 000 Keine Aktion 2 |
| STAT_WISCHER_ROH_FRONTWASCHEN | unsigned int | Bit 4-6: 001 FW Frontwaschen |
| STAT_WISCHER_ROH_HECKWISCHEN | unsigned int | Bit 4-6: 010 HW Heckwischen (fuer E60-Touring vorgehalten) |
| STAT_WISCHER_ROH_HECKWASCHEN | unsigned int | Bit 4-6: 100 HWA Heckwaschen (fuer E60-Touring vorgehalten) |
| STAT_WISCHER_BEDIENMODI_KEINE_AKTION | unsigned int | Bit 0-2: 000 Keine Aktion |
| STAT_WISCHER_BEDIENMODI_INTERVALL_AUTOM | unsigned int | Bit 0-2: 001 Intervall Automatik |
| STAT_WISCHER_BEDIENMODI_STUFE_1 | unsigned int | Bit 0-2: 010 Stufe 1 |
| STAT_WISCHER_BEDIENMODI_STUFE_2 | unsigned int | Bit 0-2: 011 Stufe 2 |
| STAT_WISCHER_BEDIENPOTI_STUFE_1 | unsigned int | Bit 3-5: Wischerpotentiometer 000 Stufe 1 |
| STAT_WISCHER_BEDIENPOTI_STUFE_2 | unsigned int | Bit 3-5: Wischerpotentiometer 001 Stufe 2 |
| STAT_WISCHER_BEDIENPOTI_STUFE_3 | unsigned int | Bit 3-5: Wischerpotentiometer 010 Stufe 3 |
| STAT_WISCHER_BEDIENPOTI_STUFE_4 | unsigned int | Bit 3-5: Wischerpotentiometer 100 Stufe 4 |
| STAT_WISCHER_BEDIENPOTI_UNGUELTIG | unsigned int | Bit 3-5: Wischerpotentiometer 111 Signal ungueltig |
| STAT_WISCHERPOTI_WIDWERT_WERT | unsigned int | Widerstandswert Wischerpoti |
| STAT_WISCHERPOTI_WIDWERT_EINH | string | Einheit: (Ink)remente 0-255 |
| STAT_TEMPOMAT_ACC_GESAMT_1 | unsigned int | Tempomatschalter oder ACC 0: Keine Aktion 1: Beschleunigung (druecken) 2: Naechsthoehere Stufe (ueberdruecken nur bei Tempomat) 3: Verzoegern (ziehen) 4: Naechstniedrigere Stufe (ueberziehen nur bei Tempomat) 5: Aus (nach oben / unten druecken) 6-7: frei Speziell fuer VS |
| STAT_TEMPOMAT_ACC_GESAMT_2 | unsigned int | Tempomatschalter oder ACC 0: Axial Schalter Tempomat / ACC Keine Aktion 1: Axial Schalter Tempomat / ACC Gedrueckt 2-7: frei Speziell fuer VS |
| STAT_TEMPOMAT_ACC_GESAMT_3 | unsigned int | ACC Raendel 0: Keine Aktion 1: naechsthoeheren Abstand waehlen (nach oben gedrueckt) 2: naechstniedrigeren Abstand waehlen (nach unten gedrueckt) 3-7: frei Speziell fuer VS |
| STAT_SCHALTER_TEMPOMAT_ACC_BESCHL_SETZEN | unsigned int | Status Schalter Tempomat / ACC Bit 0: Beschleunigen / Setzen |
| STAT_SCHALTER_TEMPOMAT_HIGHER_STEP | unsigned int | Status Schalter Tempomat Bit 1: naechsthoehere Stufe waehlen |
| STAT_SCHALTER_TEMPOMAT_ACC_VERZOEGERN_SETZEN | unsigned int | Status Schalter Tempomat Bit 2: Verzoegern / Setzen |
| STAT_SCHALTER_TEMPOMAT_LOWER_STEP | unsigned int | Bit 3: naechstniedrigere Stufe waehlen |
| STAT_SCHALTER_TEMPOMAT_ACC_AUS | unsigned int | Status Schalter Tempomat / ACC Bit 4: Aus |
| STAT_SCHALTER_TEMPOMAT_ACC_ABRUF | unsigned int | Status Schalter Tempomat / ACC Bit 6: Abruf |
| STAT_SCHALTER_ACC_RAENDEL_HOEHERER_ABSTAND | unsigned int | Status Schalter ACC Raendel Bit 0:  naechsthoeheren Abstand waehlen |
| STAT_SCHALTER_ACC_RAENDEL_NIEDRIGERER_ABSTAND | unsigned int | Status Schalter ACC Raendel Bit 1: naechstniedrigeren Abstand waehlen |
| STAT_LSVS_GESAMT_1 | unsigned int | Lenksaeulenverstellschalter 0: Keine Aktion 1: AUF 2: AB 3: Laenge + 4: Laenge - 5-7: frei Speziell fuer VS |
| STAT_LENKSAEULENVERSTSCHALTER_NEIGUNG_AUF | unsigned int | Status Lenksaeulenverstellschalter Bit 0: Neigung auf |
| STAT_LENKSAEULENVERSTSCHALTER_NEIGUNG_AB | unsigned int | Status Lenksaeulenverstellschalter Bit 1: Neigung ab |
| STAT_LENKSAEULENVERSTSCHALTER_LAENGE_PLUS | unsigned int | Status Lenksaeulenverstellschalter Bit 2: Laenge + |
| STAT_LENKSAEULENVERSTSCHALTER_LAENGE_MINUS | unsigned int | Status Lenksaeulenverstellschalter Bit 3: Laenge - |
| STAT_LENKSAEULENVERSTSCHALTER_GUELTIG | unsigned int | Status Lenksaeulenverstellschalter Bit 4-6: 000 gueltiger Wert |
| STAT_LENKSAEULENVERSTSCHALTER_KS_NACH_VSS | unsigned int | Status Lenksaeulenverstellschalter Bit 4-6: 001 KS nach VSS |
| STAT_LENKSAEULENVERSTSCHALTER_KS_NACH_VDD | unsigned int | Status Lenksaeulenverstellschalter Bit 4-6: 010 KS nach VDD |
| STAT_LENKSAEULENVERSTSCHALTER_SPGSWERT_NICHT_DEF | unsigned int | Status Lenksaeulenverstellschalter Bit 4-6: 100 Spannungswert nicht definiert |
| STAT_LENKSAEULENVERSTSCH_WID_WERT | unsigned int | Status Widerstandswert Lenksaeulenverstellschalter |
| STAT_LENKSAEULENVERSTSCH_WID_EINH | string | Einheit: (Ink)remente 0-255 |
| STAT_LRADTASTER_GESAMT_1 | unsigned int | Lenkradtaster 0: Keine Aktion 1: Steptronic hinten links 2: Steptronic vorne links 3: Steptronic hinten rechts 4: Steptronic vorne rechts 5-7: frei Speziell fuer VS |
| STAT_LENKRADTASTER_LI_STEP_HINTEN | int | Status Lenkradtaster digital Bit 0: STEP hinten links |
| STAT_LENKRADTASTER_LI_STEP_VORNE | int | Status Lenkradtaster digital Bit 1: STEP vorne links |
| STAT_LENKRADTASTER_RE_STEP_HINTEN | int | Status Lenkradtaster digital Bit 2: STEP hinten rechts |
| STAT_LENKRADTASTER_RE_STEP_VORNE | int | Status Lenkradtaster digital Bit 3: STEP vorne rechts |
| STAT_LENKRADTASTER_HORN | int | Status Lenkradtaster digital Bit 4: Horn 0 = Keine Aktion 1 = Gedrueckt |
| STAT_LRE_KOMMUNIKATION_I_O | int | Status LRE Bit 7: Lenkradkommunikation i.O. |
| STAT_MFL_GESAMT_1 | unsigned int | Multifunktionslenkrad 0: Keine Aktion 1: PTT 2: Vol + 3: Vol - 4: Tel 5-7: frei Speziell fuer VS |
| STAT_MFL_GESAMT_2 | unsigned int | Multifunktionslenkrad 0: Keine Aktion 1: Sport 2: Suchlauf AUF 3: Suchlauf AB 4: Programmierbare Taste 5-7: frei Speziell fuer VS |
| STAT_LENKRADTASTER_MFL_PUSH_TO_TALK | unsigned int | Status Lenkradtaster Multifunktionsl. Bit 0: PTT Push to Talk |
| STAT_LENKRADTASTER_MFL_VOL_UP | unsigned int | Status Lenkradtaster Multifunktionsl. Bit 1: VOL+ |
| STAT_LENKRADTASTER_MFL_VOL_DOWN | unsigned int | Status Lenkradtaster Multifunktionsl. Bit 2: VOL- |
| STAT_LENKRADTASTER_MFL_TEL | unsigned int | Status Lenkradtaster Multifunktionsl. Bit 3: TEL |
| STAT_LENKRADTASTER_MFL_SPORT | unsigned int | Status Lenkradtaster Multifunktionsl. Bit 4: Sport |
| STAT_LENKRADTASTER_MFL_SUCHLAUF_AUF | unsigned int | Status Lenkradtaster Multifunktionsl. Bit 5: Suchlauf AUF |
| STAT_LENKRADTASTER_MFL_SUCHLAUF_AB | unsigned int | Status Lenkradtaster Multifunktionsl. Bit 6: Suchlauf AB |
| STAT_LENKRADTASTER_MFL_PROG | unsigned int | Status Lenkradtaster Multifunktionsl. Bit 7: Programmierbarer Taster |
| STAT_LENKRADTASTER_MFL_I_O | unsigned int | Status Lenkradtaster Multifunktionsl./Lenkradheizung Mfl-Status (Bits 0-3) * * * * 0 0 0 0      MFL kein Fehler |
| STAT_LENKRADTASTER_MFL_LI_KS_UNTERBR | unsigned int | Status Lenkradtaster Multifunktionsl./Lenkradheizung Mfl-Status (Bits 0-3) * * * * * * * 1      MFL links : Kurzschluss/Unterbrechung |
| STAT_LENKRADTASTER_MFL_RE_KS_UNTERBR | unsigned int | Status Lenkradtaster Multifunktionsl./Lenkradheizung Mfl-Status (Bits 0-3) * * * * * * 1 *      MFL rechts: Kurzschluss/Unterbrechung |
| STAT_LENKRADTASTER_MFL_LI_SPGSWERT_NICHT_DEF | unsigned int | Status Lenkradtaster Multifunktionsl./Lenkradheizung Mfl-Status (Bits 0-3) * * * * * 1 * *      MFL links : Spannungswert nicht definiert |
| STAT_LENKRADTASTER_MFL_RE_SPGSWERT_NICHT_DEF | unsigned int | Status Lenkradtaster Multifunktionsl./Lenkradheizung Mfl-Status (Bits 0-3) * * * * 1 * * *      MFL rechts: Spannungswert nicht definiert |
| STAT_LENKRADTASTER_MFL_LHZ_I_O | unsigned int | Status Lenkradtaster Multifunktionsl./Lenkradheizung LHz-Status (Bits 4-7) 0 0 0 0 * * * *      LHZ kein Fehler |
| STAT_LENKRADTASTER_MFL_LHZ_KS_KL31 | unsigned int | Status Lenkradtaster Multifunktionsl./Lenkradheizung LHz-Status (Bits 4-7) * 0 0 1 * * * *      LHZ Overload/LHZ Heizmatte KS nach Kl 31 |
| STAT_LENKRADTASTER_MFL_LHZ_KS_KL30 | unsigned int | Status Lenkradtaster Multifunktionsl./Lenkradheizung LHz-Status (Bits 4-7) * 0 1 0 * * * *      LHZ Underload/LHZ Heizmatte KS nach Kl 30 |
| STAT_LENKRADTASTER_MFL_LHZ_HEIZMATTE_UNTERBR | unsigned int | Status Lenkradtaster Multifunktionsl./Lenkradheizung LHz-Status (Bits 4-7) * 1 0 0 * * * *      LHZ Heizmatte Unterbrechung |
| STAT_LENKRADTASTER_MFL_LHZ_TIMEOUT | unsigned int | Status Lenkradtaster Multifunktionsl./Lenkradheizung LHz-Status (Bits 4-7) * 1 1 0 * * * *      LHZ Timeout-Regelung |
| STAT_LENKRADTASTER_MFL_LHZ_TEMPFUEHLER_N_I_O | unsigned int | Status Lenkradtaster Multifunktionsl./Lenkradheizung LHz-Status (Bits 4-7) 1 * * * * * * *      LHZ Temperaturfuehler fehlerhaft |
| STAT_LENKRADHEIZUNG_TASTER_LENKRAD | unsigned int | Status Lenkradheizung Bit 0: Taster Lenkrad |
| STAT_LENKRADHEIZUNG_EIN | unsigned int | Status Lenkradheizung Bit 1: Lenkradheizung ein |
| STAT_KLEMMEN_GESAMT_1 | unsigned int | Klemmenstatus SZL 0: Normalspannung Klemme 30 1: Unterspannung Klemme 30 2: Ueberspannung Klemme 30 3: Grenze fuer sichere Betriebsspannung unterschritten Klemme 30 4-7: frei Speziell fuer VS |
| STAT_KLEMMENSTATUS_SZL_NORMALSPG | unsigned int | Status Klemmenstatus SZL Bit 0-1: Status Klemme 30 00 Normalspannung |
| STAT_KLEMMENSTATUS_SZL_UNTERSPG | unsigned int | Status Klemmenstatus SZL Bit 0-1: Status Klemme 30 01 Unterspannung |
| STAT_KLEMMENSTATUS_SZL_UEBERSPG | unsigned int | Status Klemmenstatus SZL Bit 0-1: Status Klemme 30 10 Ueberspannung |
| STAT_KLEMMENSTATUS_SZL_KL30 | unsigned int | Status Klemmenstatus SZL Bit 0-1: Status Klemme 30 11 Klemme 30 fehlt |
| STAT_KLEMMENSTATUS_SZL_KL15_EIN_HW | unsigned int | Status Klemmenstatus SZL Hardware Bit 2: Klemme 15 ein |
| STAT_KLEMMENSTATUS_SZL_KL_UISIS_EIN | unsigned int | Status Klemmenstatus SZL Bit 3: Klemme Uisis ein Spannung UISIS kommt vom SIM |
| STAT_KLEMMENSTATUS_SZL_KLR_EIN_CAS | unsigned int | Status Klemmenstatus über Bus Bit 4,5: Klemme R ein vom CAS 00: Klemme R AUS 01: Klemme R EIN 11: Klemme R Signal ungueltig |
| STAT_KLEMMENSTATUS_SZL_KL15_EIN_CAS | unsigned int | Status Klemmenstatus über Bus Bit 6,7: Klemme 15 ein vom CAS 00: Klemme 15 AUS 01: Klemme 15 EIN 11: Klemme 15 Signal ungueltig |
| STAT_RESET_WATCH_WERT | unsigned int | Spannungswert Resetuhr |
| STAT_RESET_WATCH_EINH | string | Einheit: (Ink)remente 0-255 |
| STAT_ZK_LRE | unsigned int | Zuendkreisstatus LRE Lenkradelektronik Nur fuer Entwicklung !!! |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ausstattung-airbags"></a>
### STATUS_AUSSTATTUNG_AIRBAGS

Statusausgabe, welche Airbags aktiv oder inaktiv codiert sind Codierdaten lesen Standard Codierjob KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZK1_AKTIV | int | 0=ZK1_NICHT_AKTIV 1=ZK1_AKTIV Front-Airbag Stufe 1 |
| STAT_ZK2_AKTIV | int | 0=ZK2_NICHT_AKTIV 1=ZK2_AKTIV Front-Airbag Stufe 2 |
| STAT_CODIER_DATEN | binary | Codierdaten |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (2 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (76 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (4 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (4 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IARTTEXTEERWEITERT](#table-iarttexteerweitert) (4 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [IUMWELTMATRIX](#table-iumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (3 × 9)
- [IUMWELTTEXTE](#table-iumwelttexte) (3 × 9)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [FORTTEXTE](#table-forttexte) (102 × 2)
- [IORTTEXTE](#table-iorttexte) (20 × 2)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 2 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
| 0x0F | BMW-FAST |
| 0x0C | KWP2000 |

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

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | 12300000 |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 4 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| 1xxxxxxx | 11 | Fehlerklassifikation  t &gt; 1min |
| x1xxxxxx | 21 | Fehlerklassifikation 1s &lt; t &lt; 1min |
| xx1xxxxx | 31 | Fehlerklassifikation 0 &lt; t &lt; 1s |
| xxxxxxxx | 0 | -- |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_ERW | 12300000 |
| F_HFK | ja |
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-iarttexteerweitert"></a>
### IARTTEXTEERWEITERT

Dimensions: 4 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| 1xxxxxxx | 11 | Fehlerklassifikation  t &gt; 1min |
| x1xxxxxx | 21 | Fehlerklassifikation 1s &lt; t &lt; 1min |
| xx1xxxxx | 31 | Fehlerklassifikation 0 &lt; t &lt; 1s |
| xxxxxxxx | 0 | -- |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | 0x02 | - | - |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | 0x02 | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Systemzeit Fehlerbeginn | Stunden | high | signed long | - | 16384 | 3600000 | 0 |
| 0x02 | Systemzeit Fehlerende | Stunden | high | signed long | - | 16384 | 3600000 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 3 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Systemzeit Fehlerbeginn | Stunden | high | signed long | - | 16384 | 3600000 | 0 |
| 0x02 | Systemzeit Fehlerende | Stunden | high | signed long | - | 16384 | 3600000 | 0 |
| 0xXY | unbekannte Umweltbedingung | 1 | - | unsigned char | - | 1 | 1 | 0 |

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

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 102 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x94a8 | Watchdog-Reset uP |
| 0x94a9 | Clock-Monitor-Reset uP |
| 0x94aa | Illegal Opcode uP |
| 0x94ab | Falsche Fahrgestellnummer |
| 0x94ac | Systemzeitfehler |
| 0x94ad | AD-Wandler fehlerhaft |
| 0x94ae | Timeout ID 01H (E65,E66,E67,RR01:STVL; E60,E61,E63,E64:TE_FAT) |
| 0x94af | Timeout ID 02H |
| 0x94b0 | Timeout ID 03H (E65,E66,E67,RR01:STVR; E60,E61,E63,E64:TE_BFT) |
| 0x94b1 | Timeout ID 04H |
| 0x94b2 | Timeout ID 05H (SBSL) |
| 0x94b3 | Timeout ID 06H (SASL) |
| 0x94b4 | Timeout ID 07H (SBSR) |
| 0x94b5 | Timeout ID 08H (SASR) |
| 0x94b6 | Timeout ID 09H (SFZ) |
| 0x94b7 | Timeout ID 0AH (E65,E66,E67,RR01:SIM; E60,E61,E63,E64:SGM) |
| 0x94b8 | Timeout ID 0BH (E65,E66,E67,RR01:SASL; E60,E61,E63,E64:SBSL) |
| 0x94b9 | Timeout ID 0CH (E65,E66,E67,RR01:SASR; E60,E61,E63,E64:SBSR) |
| 0x94ba | Timeout ID 0DH (SFZ) |
| 0x94bb | Timeout ID 0EH (E60,E61,E63,E64:SFZ |
| 0x94bc | Timeout ID 0FH |
| 0x94bd | Timeout ID 20H (E65,E66,E67,RR01:SSFA; E60,E61,E63,E64:SBSL) |
| 0x94be | Timeout ID 21H (E65,E66,E67,RR01:SSBF; E60,E61,E63,E64:SBSR) |
| 0x94bf | Timeout ID 22H (SSH) |
| 0x94c0 | Timeout ID 71H (E65,E66,E67,RR01:SIM; E60,E61,E63,E64:SGM) |
| 0x94c1 | Codierdaten Checksummenfehler |
| 0x94c2 | Stack Overflow |
| 0x94c3 | PDC_3 : zu wenig Telegramme |
| 0x94c4 | PDC_3 : Datenfehler in Telegramm |
| 0x94c5 | PDC_3 : Uebertragungsfehler |
| 0x94c6 | unplausible Crash-Schwere |
| 0x94c7 | Kurzschluss oder Unterbrechung H/L-Side-Schalter ZK1 |
| 0x94c8 | Kurzschluss ZK1 nach Masse |
| 0x94c9 | Kurzschluss ZK1 nach Plus |
| 0x94ca | Widerstand Zuendpille ZK1 zu klein |
| 0x94cb | Widerstand Zuendpille ZK1 zu gross |
| 0x94cc | Widerstand Zuendpille ZK1 nicht gemessen |
| 0x94cd | Unterbrechung ZK1 |
| 0x94ce | Spannung ZK1 n.i.O. |
| 0x94cf | Zuendkapazitaet ZK1 n.i.O. |
| 0x94d0 | Codierung/Konfiguration ZK1 unstimmig |
| 0x94d1 | Unterbrechung Entladekreis ZK1 |
| 0x94d2 | Kurzschluss oder Unterbrechung H/L-Side-Schalter ZK2 |
| 0x94d3 | Kurzschluss ZK2 nach Masse |
| 0x94d4 | Kurzschluss ZK2 nach Plus |
| 0x94d5 | Widerstand Zuendpille ZK2 zu klein |
| 0x94d6 | Widerstand Zuendpille ZK2 zu gross |
| 0x94d7 | Widerstand Zuendpille ZK2 nicht gemessen |
| 0x94d8 | Unterbrechung ZK2 |
| 0x94d9 | Spannung ZK2 n.i.O. |
| 0x94da | Zuendkapazitaet ZK2 n.i.O. |
| 0x94db | Codierung/Konfiguration ZK2 unstimmig |
| 0x94dc | Unterbrechung Entladekreis ZK2 |
| 0x94dd | Fehler im Alarmpfad |
| 0x94de | E65,66,67,RR:GWS: Einfachfehler Signalpfad E60,61,63,64: U_ASE ausserhalb Bereich |
| 0x94df | GWS: Zweifachfehler Signalpfad |
| 0x94e0 | GWS: Parktaster Zweifachkontakt fehlerhaft |
| 0x94e1 | Klemme 30 fehlt am SZL |
| 0x94e2 | Klemme 15 unplausibel |
| 0x94e3 | Klemme U_Isis fehlt |
| 0x94e4 | LWS: Maximaler Lenkradeinschlagbereich ueberschritten |
| 0x94e5 | LWS: Schleifer 1 ausserhalb Bereich |
| 0x94e6 | LWS: Schleifer 2 ausserhalb Bereich |
| 0x94e7 | LWS: Relativer Schleiferwinkel fehlerhaft |
| 0x94e9 | Lenkradwinkelgradient zu hoch |
| 0x94ea | Kommunikation zwischen Lenkrad und Lenksaeule fehlerhaft |
| 0x94eb | LRE-Version nicht kompatibel |
| 0x94ec | MFL links : Kurzschluss/Unterbrechung |
| 0x94ed | MFL rechts: Kurzschluss/Unterbrechung |
| 0x94f0 | LHZ Heizmatte Unterbrechung |
| 0x94f1 | LHZ Heizmatte Kurzschluss nach Klemme 31 |
| 0x94f2 | LHZ Heizmatte Kurzschluss nach Klemme 30 |
| 0x94f3 | LHZ Timeout-Regelung |
| 0x94f4 | LHZ Temperaturfuehler fehlerhaft |
| 0x94f5 | Lenksaeulenverstellschalter: Kurzschluss nach VSS |
| 0x94f6 | Lenksaeulenverstellschalter: Unterbrechung/Kurzschluss nach VDD |
| 0x94f8 | Fehler Horn Toener1 |
| 0x94f9 | Fehler Horn Toener2 |
| 0x94fa | E65,66,67,RR:Lenkstockschalterauswertung fehlerhaft  E60,61,63,64:Signaturprüfung fehlerhaft |
| 0x94fb | LWS: Versorgungsspannung zu klein |
| 0x94fc | LRE: keine Ausloesebereitschaft |
| 0x94fd | LRE: Fehler im Alarmpfad |
| 0x94fe | Algorithmus-Parameter inkonsistent |
| 0x94ff | EAM-Parameter inkonsistent |
| 0x9500 | Zuendversuch erfolgt |
| 0x9501 | LWS nicht abgeglichen |
| 0x9502 | COP-Watchdog fehlerhaft |
| 0x9503 | LWS Resetzeitmessung fehlerhaft |
| 0x9504 | Fehler serielle Leitung Active Front Steering (AFS) |
| 0x9505 | Kommunikationsfehler CAN |
| 0x9506 | Kurzschluss oder Unterbrechung Low-Side-Schalter ZK1 |
| 0x9507 | Kurzschluss oder Unterbrechung High-Side-Schalter ZK1 |
| 0x9508 | Kurzschluss oder Unterbrechung Low-Side-Schalter ZK2 |
| 0x9509 | Kurzschluss oder Unterbrechung High-Side-Schalter ZK2 |
| 0x950A | Kommunikation mit Zuend-IC gestoert |
| 0x950B | Energiesparmode aktiv |
| 0x9518 | Spannungsueberwachung ASE unterer Grenzwert unterschritten |
| 0x9519 | Spannungsueberwachung ASE oberer Grenzwert ueberschritten |
| 0x951A | Spannungsueberwachung LRE unterer Grenzwert unterschritten |
| 0x951B | Spannungsueberwachung LRE oberer Grenzwert ueberschritten |
| 0x951D | Codierung unvollstaendig |
| 0x???? | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 20 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x94e8 | keine oder fehlerhafte Einzelrad-Geschwindigkeiten |
| 0x94ee | MFL links : Spannungswert nicht definiert |
| 0x94ef | MFL rechts: Spannungswert nicht definiert |
| 0x94f7 | Lenksaeulenverstellschalter: Spannungswert nicht definiert |
| 0x950c | Power-On-Reset uP |
| 0x950d | Diagnose S/E-Modul (Lichtleistung) |
| 0x950e | SI-Bus: Uebertragungsfehler, CRC-Fehler ERRIF |
| 0x950f | SI-Bus: Uebertragungsfehler, Formatfehler ILLPIF |
| 0x9510 | SI-Bus: Synchronisierungspuls zu frueh SYNEIF |
| 0x9511 | SI-Bus: Synchronisierung verloren SYNLIF |
| 0x9512 | SI-Bus: Slotmismatch, Timingfehler SLMMIF |
| 0x9513 | SI-Bus: FIFO-Ueberlauf OVRNIF |
| 0x9514 | Synth. Lenkwinkel: Nullpunkt unplausibel |
| 0x9515 | Aufsetzen: maximale Geschwindigkeit ueberschritten |
| 0x9516 | EMV-Fehler im Zuend-Ic |
| 0x9517 | Uisis Reset |
| 0x951C | Kommunikation zwischen Lenkrad und Lenksaeule rueckgesetzt |
| 0x951e | Lenkwinkel wurde prognostiziert |
| 0x951f | Lenkwinkelsensor-Schleifer mindenstens einmal unplausibel |
| 0x???? | unbekannter Fehlerort |
