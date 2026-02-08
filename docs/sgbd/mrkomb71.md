# mrkomb71.prg

- Jobs: [85](#jobs)
- Tables: [54](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | K7xKombi |
| ORIGIN | BMW UX-EE-2 Pfeifer |
| REVISION | 3.002 |
| AUTHOR | Preh_GmbH Softwareentwicklung Kirchner, Preh_GmbH Softwareentwi |
| COMMENT | N/A |
| PACKAGE | 1.66 |
| SPRACHE | deutsch |

## Jobs

### Index

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
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt) KWP2000: $3D WriteMemoryByAddress Modus  : Default
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
- [STATUS_LED](#job-status-led) - liest den Zustand der LEDs aus KWP2000: $30 InputOutputControlByLocalIdentifier $02 Bereich LEDs $01 ReportCurrentState Modus  : Default 1 = LED Ein    0 = LED Aus
- [STATUS_IO](#job-status-io) - liest den Zustand der IOs aus KWP2000: $21 ApplDiagReadDataByLocalIdentifier $03 Status der Digitaleingaenge 1= Taste gedrueckt / Wakeleitung aktiv (d.h. High) 0= Taste nicht gedrueckt / Wakeleitung nicht aktiv (d.h. Low)
- [STATUS_ANALOG](#job-status-analog) - liest den Wert der aus der an den AD- Eingängen gemessen wird KWP2000: $21 InputOutputControlByLocalIdentifier $02 Status Analog
- [STATUS_GWSZ_ANZEIGE](#job-status-gwsz-anzeige) - Ausgabe des aktuellen GWSZ Standes KWP2000: $21 ApplDiagReadDataByLocalIdentifier $01 Status Gesamtwegstrecke
- [STATUS_TANK](#job-status-tank) - liefert einige Informationeen über den Tankinhalt KWP2000: $21 ApplDiagReadDataByLocalIdentifier $04 Status Tank
- [STATUS_CAN_OUT](#job-status-can-out) - Daten die vom I- Kombi auf dem CAn versendet werden KWP2000: $21 ApplDiagReadDataByLocalIdentifier $05 Status CAN OUT
- [STATUS_CAN_IN_DWA](#job-status-can-in-dwa) - Daten die von der DWA auf dem CAN versendet werden KWP2000: $21 ApplDiagReadDataByLocalIdentifier $06 Status CAN IN DWA
- [STATUS_CAN_IN_ZFE](#job-status-can-in-zfe) - Daten die von der ZFE auf dem CAN versendet werden KWP2000: $21 ApplDiagReadDataByLocalIdentifier $07 Status CAN IN ZFE
- [STATUS_CAN_IN_ABS](#job-status-can-in-abs) - Daten die vom ABS auf dem CAN versendet werden KWP2000: $21 ApplDiagReadDataByLocalIdentifier $08 Status CAN IN ABS
- [STATUS_CAN_IN_GESCHW](#job-status-can-in-geschw) - Daten die in der GESCHW Botschaft auf dem CAN versendet werden KWP2000: $21 ApplDiagReadDataByLocalIdentifier $09 Status CAN IN GESCHW
- [STATUS_CAN_IN_MOTOR](#job-status-can-in-motor) - Daten die vom BMSK auf dem CAN versendet werden KWP2000: $21 ApplDiagReadDataByLocalIdentifier $0A Status CAN IN MOTOR
- [STATUS_GESCHWINDIGKEIT](#job-status-geschwindigkeit) - liest die aktuell angezeigt Geschwindigkeit aus KWP2000: $30 InputOutputControlByLocalIdentifier $03 Bereich Geschwindigkeit $01 ReportCurrentState Modus  : Default
- [STEUERN_GESCHWINDIGKEIT](#job-steuern-geschwindigkeit) - steuert die Geschwindigkeit über den Tester KWP2000: $30 InputOutputControlByLocalIdentifier $03 Bereich Geschwindigkeit $07 shortTermAdjustment Modus  : Default
- [STEUERN_GESCHWINDIGKEIT_ENDE](#job-steuern-geschwindigkeit-ende) - übergibt die Kontrolle über die Geschwindigkeitsanzeige wieder an das Kombi KWP2000: $30 InputOutputControlByLocalIdentifier $03 Bereich Geschwindigkeit $00 returnControlToECU Modus  : Default
- [STATUS_DREHZAHL](#job-status-drehzahl) - liest die aktuelle Drehzahl aus KWP2000: $30 InputOutputControlByLocalIdentifier $04 Bereich Drehzahl $01 ReportCurrentState Modus  : Default
- [STEUERN_DREHZAHL](#job-steuern-drehzahl) - steuert die Drehzahl über den Tester KWP2000: $30 InputOutputControlByLocalIdentifier $04 Bereich Drehzahl $07 shortTermAdjustment Modus  : Default
- [STEUERN_DREHZAHL_ENDE](#job-steuern-drehzahl-ende) - übergibt die Kontrolle über die Drehzahlanzeige wieder an das Kombi KWP2000: $30 InputOutputControlByLocalIdentifier $04 Bereich Drehzahl $00 returnControlToECU Modus  : Default
- [STEUERN_DISPLAY](#job-steuern-display) - steuert die Drehzahl über den Tester KWP2000: $30 InputOutputControlByLocalIdentifier $05 Bereich Display $07 shortTermAdjustment Modus  : Default
- [STEUERN_DISPLAY_ENDE](#job-steuern-display-ende) - übergibt die Kontrolle über die Displayanzeige wieder an das Kombi KWP2000: $30 InputOutputControlByLocalIdentifier $05 Bereich Display $00 returnControlToECU Modus  : Default
- [STEUERN_LED](#job-steuern-led) - steuert die LEDs über den Tester KWP2000: $30 InputOutputControlByLocalIdentifier $02 Bereich LEDs $07 shortTermAdjustment Modus  : Default
- [STEUERN_LED_ENDE](#job-steuern-led-ende) - übergibt die Kontrolle über die LED wieder an das Kombi KWP2000: $30 InputOutputControlByLocalIdentifier $02 externes Steuern Selbstest $00 returnControlToECU Modus  : Default
- [STEUERN_PWM](#job-steuern-pwm) - steuert die Drehzahl über den Tester KWP2000: $30 InputOutputControlByLocalIdentifier $06 Bereich PWM $07 shortTermAdjustment Modus  : Default
- [STEUERN_PWM_ENDE](#job-steuern-pwm-ende) - übergibt die Kontrolle über die Drehzahlanzeige wieder an das Kombi KWP2000: $30 InputOutputControlByLocalIdentifier $06 Bereich PWM $00 returnControlToECU Modus  : Default
- [STEUERN_TASTER](#job-steuern-taster) - steuert die Taster über den Tester KWP2000: $30 InputOutputControlByLocalIdentifier $01 Bereich Taster $07 shortTermAdjustment Modus  : Default
- [STEUERN_TASTER_ENDE](#job-steuern-taster-ende) - übergibt die Kontrolle über die IOs wieder an das Kombi KWP2000: $30 InputOutputControlByLocalIdentifier $01 Bereich Taster $00 returnControlToECU Modus  : Default
- [START_SELBSTTEST](#job-start-selbsttest) - Starten des Selbsttest KWP2000: $31 StartRoutineByLocalIdentifier $04 Selbstest starten Modus  : Default
- [STOPP_SELBSTTEST](#job-stopp-selbsttest) - Stoppen des Selbsttest KWP2000: $32 StopRoutineByLocalIdentifier $04 Selbstest beenden Modus  : Default
- [C_FA_LESEN](#job-c-fa-lesen) - Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F7F Fahrzeugauftrag Modus  : Default
- [C_FA_SCHREIBEN](#job-c-fa-schreiben) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F0A Fahrzeugauftrag Modus  : Default
- [C_FA_AUFTRAG](#job-c-fa-auftrag) - Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F0A Fahrzeugauftrag Modus  : Default
- [STATUS_AUSSTATTUNG](#job-status-ausstattung) - liest den Inhalt des Codierblockes 3007 (Ausstattung) KWP2000: $22 InputOutputControlByLocalIdentifier $3007 Block 'Ausstattung' Modus  : Default 1 = Ausstattung ist als aktiv / verbaut  codiert 0 = Ausstattung ist als nicht aktiv / nicht verbaut  codiert
- [STEUERN_GWSZ_ANZEIGE_SCHREIBEN](#job-steuern-gwsz-anzeige-schreiben) - Schreibt einen km Wert in den GWSZ-EEPROM-Bereich KWP2000: $31 StartRoutineByLocalIdentifier $AA GWSZ schreiben Modus  : Default  Damit das Einschreiben funktioniert, muessen folgende Bedingungen erfuellt sein: - GWZS-Offsetzelle im EEPROM muss == 0 sein - neuer GWSZ-Wert muss &gt; alter GWSZ-Wert und &lt; 999999 km sein - Betriebsspannung muss im normalen Bereich sein
- [STATUS_DATE_TIME](#job-status-date-time) - Kombiinternes Datum und Uhrzeit auslesen KWP2000: $21 ApplDiagReadDataByLocalIdentifier $10 Read Date/Time
- [STATUS_SERVICE_DATE](#job-status-service-date) - Kombiinternes Service_Datum auslesen KWP2000: $21 ApplDiagReadDataByLocalIdentifier $11 Read Service_Date
- [STEUERN_DATE_TIME](#job-steuern-date-time) - kombiinternes Datum und Uhrzeit Setzen KWP2000: $3B ApplDiagWriteDataByLocalIdentifier $10 Set Date/Time Wenn keine Argumente uebergeben werden, werden die Daten werden vom PC bzw. Tester uebernommen
- [STEUERN_SERVICE_DATE](#job-steuern-service-date) - kombiinternes Service-Datum Setzen KWP2000: $3B ApplDiagWriteDataByLocalIdentifier $10 Set Service_Date
- [STEUERN_SERVICE_RESTWEG](#job-steuern-service-restweg) - kombiinterne Service-Intervall-Wegstrecke Setzen KWP2000: $3B ApplDiagWriteDataByLocalIdentifier $12 Set Actual Service Mileage Range in [km]
- [STATUS_SERVICE_RESTWEG](#job-status-service-restweg) - Kombiinternen KM-Zaehlerstand bis zum naechsten Service auslesen KWP2000: $21 ApplDiagReadDataByLocalIdentifier $12 Read Actual_Service_Mileage_Range in [km]
- [STEUERN_HBG_VOL_NV_DATA](#job-steuern-hbg-vol-nv-data) - Setzt den Hebelgeberwert fuer die Tankanzeige auf den Codierwert HBG_RESET KWP2000: $3B WriteDataByLocalIdentifier $0B hbg_reset
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter

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

<a id="job-status-led"></a>
### STATUS_LED

liest den Zustand der LEDs aus KWP2000: $30 InputOutputControlByLocalIdentifier $02 Bereich LEDs $01 ReportCurrentState Modus  : Default 1 = LED Ein    0 = LED Aus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LED_BYTE_1 | int | LED_Zustandsbyte_1 |
| STAT_LED_BYTE_2 | int | LED_Zustandsbyte_2 |
| STAT_FERNLICHT_BLAU_EIN | int | blaue LED Fernlicht Ein |
| STAT_BLINKER_LINKS_GRUEN_EIN | int | gruene LED Blinker Links Ein |
| STAT_BLINKER_RECHTS_GRUEN_EIN | int | gruene LED Blinker Rechts Ein |
| STAT_WARNLEUCHTE_ROT_EIN | int | rote LED Warnleuchte Ein |
| STAT_WARNLEUCHTE_GELB_EIN | int | gelbe LED Warnleuchte Ein |
| STAT_TANK_RESERVE_GELB_EIN | int | gelbe LED Tankreserve Ein |
| STAT_OELDRUCK_ROT_EIN | int | roete LED Oeldruck Ein |
| STAT_ABS_ROT_EIN | int | rote LED ABS Ein |
| STAT_ABS_GELB_EIN | int | gelbe LED ABS Ein |
| STAT_NEUTRAL_GRUEN_EIN | int | gruene LED Neutralleuchte Ein |
| STAT_DWA_LED_ROT_EIN | int | rote LED DWA/Schaltblitz Ein |
| STAT_LADEKONTROLLE_ROT_EIN | int | rote LED Ladekontrolleuchte Ein (K27) |
| STAT_ASC_GELB_EIN | int | gelbe LED ASC Ein (K27) |
| STAT_ZSW_GRUEN_EIN | int | gruene LED Zusatzscheinwerfer Ein (K7X_MUE) |
| STAT_MIL_GELB_EIN | int | gelbe LED MIL Ein (K7x_TUE/LCI) |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-io"></a>
### STATUS_IO

liest den Zustand der IOs aus KWP2000: $21 ApplDiagReadDataByLocalIdentifier $03 Status der Digitaleingaenge 1= Taste gedrueckt / Wakeleitung aktiv (d.h. High) 0= Taste nicht gedrueckt / Wakeleitung nicht aktiv (d.h. Low)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_UHR_TASTER_GEDRUECKT | int | Taster 'Uhr' (oberer Taster) gedrueckt |
| STAT_TRIP_TASTER_GEDRUECKT | int | Taster 'Trip' (unterer Taster) gedrueckt |
| STAT_WAKE_UP_LEITUNG_AKTIV | int | Weckleitung (entspricht Klemme 15) am Kombi aktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog"></a>
### STATUS_ANALOG

liest den Wert der aus der an den AD- Eingängen gemessen wird KWP2000: $21 InputOutputControlByLocalIdentifier $02 Status Analog

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SPANNUNG_KL30_WERT | long | Ergebnis der kombiinternen Klemme-30 Messung (AD- Wandlung) |
| STAT_SPANNUNG_KL30_EINH | string | Volt |
| STAT_FOTOSENSOR_WERT | real | Fotosensorwert |
| STAT_FOTOSENSOR_EINH | string | Prozent der maximal messbaren Helligkeit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-gwsz-anzeige"></a>
### STATUS_GWSZ_ANZEIGE

Ausgabe des aktuellen GWSZ Standes KWP2000: $21 ApplDiagReadDataByLocalIdentifier $01 Status Gesamtwegstrecke

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GWSZ_ANZEIGE_WERT | real | Gesamtwegstrecke in km od. Meilen |
| STAT_GWSZ_ANZEIGE_EINH | string | km od. miles |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tank"></a>
### STATUS_TANK

liefert einige Informationeen über den Tankinhalt KWP2000: $21 ApplDiagReadDataByLocalIdentifier $04 Status Tank

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TANKINHALT_WERT | int | Tankinhalt |
| STAT_TANKINHALT_EINH | string | Liter |
| STAT_RESTREICHWEITE_WERT | long | Restreichweite |
| STAT_RESTREICHWEITE_EINH | string | km |
| STAT_RESTREICHWEITE_UNGEDAEMPFT_WERT | long | Restreichweite vor Daempfung |
| STAT_RESTREICHWEITE_UNGEDAEMPFT_EINH | string | km |
| STAT_DURCHSCHNITTSVERBRAUCH_WERT | long | Durchschnittsverbrauch fuer RestReichWeite |
| STAT_DURCHSCHNITTSVERBRAUCH_EINH | string | Liter/100km |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-out"></a>
### STATUS_CAN_OUT

Daten die vom I- Kombi auf dem CAn versendet werden KWP2000: $21 ApplDiagReadDataByLocalIdentifier $05 Status CAN OUT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VARIANTE_ABS | int | ABS 'Softwarecodierung' |
| STAT_DIMMUNG | int | Dimmzustand |
| STAT_DIMMUNG_KLARTEXT | string | Dimmzustand |
| STAT_RELATIV_ZEIT | long | Zeit seit letzem Kombineustart / Time-Roll-over in Sekunden |
| STAT_WEGSTRECKE_WERT | long | gesamte zurueckgelegte Strecke in Kilometer |
| STAT_WEGSTRECKE_EINH | string | Einheit der Wegstrecke: Kilometer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-in-dwa"></a>
### STATUS_CAN_IN_DWA

Daten die von der DWA auf dem CAN versendet werden KWP2000: $21 ApplDiagReadDataByLocalIdentifier $06 Status CAN IN DWA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STEUERUNG_WARNBLINKEN_DWA | int | STEUERUNG_WARNBLINKEN_DWA |
| STAT_STEUERUNG_WARNBLINKEN_DWA_KLARTEXT | string | STEUERUNG_WARNBLINKEN_DWA_KLARTEXT |
| STAT_STEUERUNG_LED_DWA | int | STEUERUNG_LED_DWA |
| STAT_STEUERUNG_LED_DWA_KLARTEXT | string | STEUERUNG_LED_DWA_KLARTEXT |
| STAT_BATTERIESPANNUNG_DWA | int | BATTERIESPANNUNG_DWA |
| STAT_BATTERIESPANNUNG_DWA_KLARTEXT | string | BATTERIESPANNUNG_DWA_KLARTEXT |
| STAT_KONTROLLEUCHTE_REIFENDRUCKKONTRLLE | int | KONTROLLEUCHTE_REIFENDRUCKKONTRLLE |
| STAT_KONTROLLEUCHTE_REIFENDRUCKKONTRLLE_KLARTEXT | string | KONTROLLEUCHTE_REIFENDRUCKKONTRLLE_KLARTEXT |
| STAT_ZUSATZINFORMATION_REIFENDRUCKKONTROLLE | int | ZUSATZINFORMATION_REIFENDRUCKKONTROLLE |
| STAT_ZUSATZINFORMATION_REIFENDRUCKKONTROLLE_KLARTEXT | string | ZUSATZINFORMATION_REIFENDRUCKKONTROLLE_KLARTEXT |
| STAT_BATTERIE_REIFENDRUCKKONTROLLE | int | BATTERIE_REIFENDRUCKKONTROLLE |
| STAT_BATTERIE_REIFENDRUCKKONTROLLE_KLARTEXT | string | BATTERIE_REIFENDRUCKKONTROLLE_KLARTEXT |
| STAT_TEMPERATUR_RAD_V | int | TEMPERATUR_RAD_V |
| STAT_TEMPERATUR_RAD_V_GRAD | int | TEMPERATUR_RAD_V_GRAD |
| STAT_TEMPERATUR_RAD_H | int | TEMPERATUR_RAD_H |
| STAT_TEMPERATUR_RAD_H_GRAD | int | TEMPERATUR_RAD_H_GRAD |
| STAT_DRUCK_RAD_V | int | DRUCK_RAD_V |
| STAT_DRUCK_RAD_V_BAR | real | DRUCK_RAD_V_BAR |
| STAT_DRUCK_RAD_H | int | DRUCK_RAD_H |
| STAT_DRUCK_RAD_H_BAR | real | DRUCK_RAD_H_BAR |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-in-zfe"></a>
### STATUS_CAN_IN_ZFE

Daten die von der ZFE auf dem CAN versendet werden KWP2000: $21 ApplDiagReadDataByLocalIdentifier $07 Status CAN IN ZFE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMPERATUR_AUSSEN | int | TEMPERATUR_AUSSEN |
| STAT_TEMPERATUR_AUSSEN_GRAD | real | TEMPERATUR_AUSSEN_GRAD |
| STAT_LAMPENDEFEKTE | int | LAMPENDEFEKTE |
| STAT_FUELLSTAND_TANK | int | FUELLSTAND_TANK |
| STAT_STEUERUNG_KONTROLLEUCHTE_LADUNG | int | STEUERUNG_KONTROLLEUCHTE_LADUNG |
| STAT_STEUERUNG_KONTROLLEUCHTE_LADUNG_KLARTEXT | string | STEUERUNG_KONTROLLEUCHTE_LADUNG_KLARTEXT |
| STAT_ESA | int | ESA |
| STAT_ESA_KLARTEXT | string | ESA_KLARTEXT |
| STAT_TASTER_BC | int | TASTER_BC |
| STAT_TASTER_BC_KLARTEXT | string | TASTER_BC_KLARTEXT |
| STAT_KONTROLLEUCHTE_TEMPOMAT | int | KONTROLLEUCHTE_TEMPOMAT |
| STAT_KONTROLLEUCHTE_TEMPOMAT_KLARTEXT | string | KONTROLLEUCHTE_TEMPOMAT_KLARTEXT |
| STAT_WARNUNG_BREMSBELAG | int | WARNUNG_BREMSBELAG |
| STAT_WARNUNG_BREMSBELAG_KLARTEXT | string | WARNUNG_BREMSBELAG_KLARTEXT |
| STAT_ANFORDERUNG_DREHZAHL_SOLLWERT | int | ANFORDERUNG_DREHZAHL_SOLLWERT |
| STAT_ANFORDERUNG_DREHZAHL_SOLLWERT_KLARTEXT | string | ANFORDERUNG_DREHZAHL_SOLLWERT_KLARTEXT |
| STAT_SITZHEIZUNG | int | SITZHEIZUNG |
| STAT_SITZHEIZUNG_KLARTEXT | string | SITZHEIZUNG_KLARTEXT |
| STAT_TASTER_ESA | int | TASTER_ESA |
| STAT_TASTER_ESA_KLARTEXT | string | TASTER_ESA_KLARTEXT |
| STAT_KL15 | int | KL15 |
| STAT_KL15_KLARTEXT | string | KL15_KLARTEXT |
| STAT_KL56A | int | KL56A |
| STAT_KL56A_KLARTEXT | string | KL56A_KLARTEXT |
| STAT_SCHALTER_FUSSBREMSE | int | SCHALTER_FUSSBREMSE |
| STAT_SCHALTER_FUSSBREMSE_KLARTEXT | string | SCHALTER_FUSSBREMSE_KLARTEXT |
| STAT_SCHALTER_HANDBREMSE | int | SCHALTER_HANDBREMSE |
| STAT_SCHALTER_HANDBREMSE_KLARTEXT | string | SCHALTER_HANDBREMSE_KLARTEXT |
| STAT_BLINKEN_ZFE | int | BLINKEN_ZFE |
| STAT_BLINKEN_ZFE_KLARTEXT | string | BLINKEN_ZFE_KLARTEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-in-abs"></a>
### STATUS_CAN_IN_ABS

Daten die vom ABS auf dem CAN versendet werden KWP2000: $21 ApplDiagReadDataByLocalIdentifier $08 Status CAN IN ABS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STEUERUNG_LEUCHTE_ABS | int | STEUERUNG_LEUCHTE_ABS |
| STAT_STEUERUNG_LEUCHTE_ABS_KLARTEXT | string | STEUERUNG_LEUCHTE_ABS_KLARTEXT |
| STAT_GESCHWINDIGKEIT_RAD_V | long | GESCHWINDIGKEIT_RAD_V |
| STAT_GESCHWINDIGKEIT_RAD_V_KLARTEXT | real | GESCHWINDIGKEIT_RAD_V_KLARTEXT |
| STAT_WEG_IMPULSE_ZAEHLER_V | long | WEG_IMPULSE_ZAEHLER_V |
| STAT_ABS | int | ABS |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-in-geschw"></a>
### STATUS_CAN_IN_GESCHW

Daten die in der GESCHW Botschaft auf dem CAN versendet werden KWP2000: $21 ApplDiagReadDataByLocalIdentifier $09 Status CAN IN GESCHW

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STEUERUNG_WARNLEUCHTE_L | int | STEUERUNG_WARNLEUCHTE_L |
| STAT_STEUERUNG_WARNLEUCHTE_L_KLARTEXT | string | STEUERUNG_WARNLEUCHTE_L_KLARTEXT |
| STAT_GESCHWINDIGKEIT_RAD_H | long | GESCHWINDIGKEIT_RAD_H |
| STAT_GESCHWINDIGKEIT_RAD_H_KLARTEXT | real | GESCHWINDIGKEIT_RAD_H_KLARTEXT |
| STAT_WEG_IMPULSE_ZAEHLER_H | long | WEG_IMPULSE_ZAEHLER_H |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-can-in-motor"></a>
### STATUS_CAN_IN_MOTOR

Daten die vom BMSK auf dem CAN versendet werden KWP2000: $21 ApplDiagReadDataByLocalIdentifier $0A Status CAN IN MOTOR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WARNLEUCHTE_MOTOR | int | WARNLEUCHTE_MOTOR |
| STAT_WARNLEUCHTE_MOTOR_KLARTEXT | string | WARNLEUCHTE_MOTOR_KLARTEXT |
| STAT_ANZEIGE_UEBERTEMPERATUR | int | ANZEIGE_UEBERTEMPERATUR |
| STAT_ANZEIGE_UEBERTEMPERATUR_KLARTEXT | string | ANZEIGE_UEBERTEMPERATUR_KLARTEXT |
| STAT_DRUCK_OEL | int | DRUCK_OEL |
| STAT_DRUCK_OEL_KLARTEXT | string | DRUCK_OEL_KLARTEXT |
| STAT_TEMPERATUR_MOTOR | int | TEMPERATUR_MOTOR |
| STAT_TEMPERATUR_MOTOR_GRAD | real | TEMPERATUR_MOTOR_GRAD |
| STAT_EINSPRITZMENGE_KRAFTSTOFF | long | EINSPRITZMENGE_KRAFTSTOFF |
| STAT_KLEMME_50 | int | KLEMME_50 |
| STAT_KLEMME_50_KLARTEXT | string | KLEMME_50_KLARTEXT |
| STAT_EWS | int | EWS |
| STAT_EWS_KLARTEXT | string | EWS_KLARTEXT |
| STAT_GANG_GETRIEBE | int | GANG_GETRIEBE |
| STAT_GANG_GETRIEBE_KLARTEXT | string | GANG_GETRIEBE_KLARTEXT |
| STAT_HSD_BMSK | int | HSD_BMSK |
| STAT_HSD_BMSK_KLARTEXT | string | HSD_BMSK_KLARTEXT |
| STAT_LEUCHTE_ASC | int | LEUCHTE_ASC |
| STAT_LEUCHTE_ASC_KLARTEXT | string | LEUCHTE_ASC_KLARTEXT |
| STAT_OELSTAND | int | OELSTAND |
| STAT_OELSTAND_KLARTEXT | string | OELSTAND_KLARTEXT |
| STAT_TEMPERATUR_MOTOR_ANSAUGLUFT | int | TEMPERATUR_MOTOR_ANSAUGLUFT |
| STAT_TEMPERATUR_MOTOR_ANSAUGLUFT_GRAD | real | TEMPERATUR_MOTOR_ANSAUGLUFT_GRAD |
| STAT_WINKEL_DROSSELKLAPPE | int | WINKEL_DROSSELKLAPPE |
| STAT_WINKEL_DROSSELKLAPPE_GRAD | real | WINKEL_DROSSELKLAPPE_GRAD |
| STAT_DREHZAHL_MOTOR | long | DREHZAHL_MOTOR |
| STAT_DREHZAHL_MOTOR_KLARTEXT | real | DREHZAHL_MOTOR_KLARTEXT |
| STAT_NOT_AUS | int | NOT_AUS |
| STAT_NOT_AUS_KLARTEXT | string | NOT_AUS_KLARTEXT |
| STAT_SCHALTER_KUPPLUNG | int | SCHALTER_KUPPLUNG |
| STAT_SCHALTER_KUPPLUNG_KLARTEXT | string | SCHALTER_KUPPLUNG_KLARTEXT |
| STAT_SCHALTAUFFORDERUNG | int | SCHALTAUFFORDERUNG |
| STAT_SCHALTAUFFORDERUNG_KLARTEXT | string | SCHALTAUFFORDERUNG_KLARTEXT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-geschwindigkeit"></a>
### STATUS_GESCHWINDIGKEIT

liest die aktuell angezeigt Geschwindigkeit aus KWP2000: $30 InputOutputControlByLocalIdentifier $03 Bereich Geschwindigkeit $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_GESCHWINDIGKEIT_WERT | int | vom Kombi angezeigte Geschwindigkeit |
| STAT_GESCHWINDIGKEIT_EINH | string | [km/h] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-geschwindigkeit"></a>
### STEUERN_GESCHWINDIGKEIT

steuert die Geschwindigkeit über den Tester KWP2000: $30 InputOutputControlByLocalIdentifier $03 Bereich Geschwindigkeit $07 shortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GESCHWINDIGKEIT | unsigned int | Geschwindigkeit, die vom Zeiger angezeigt werden soll |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-geschwindigkeit-ende"></a>
### STEUERN_GESCHWINDIGKEIT_ENDE

übergibt die Kontrolle über die Geschwindigkeitsanzeige wieder an das Kombi KWP2000: $30 InputOutputControlByLocalIdentifier $03 Bereich Geschwindigkeit $00 returnControlToECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-drehzahl"></a>
### STATUS_DREHZAHL

liest die aktuelle Drehzahl aus KWP2000: $30 InputOutputControlByLocalIdentifier $04 Bereich Drehzahl $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DREHZAHL_WERT | int | vom Kombi angezeigte Drehzahl |
| STAT_DREHZAHL_EINH | string | [U/Min] |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-drehzahl"></a>
### STEUERN_DREHZAHL

steuert die Drehzahl über den Tester KWP2000: $30 InputOutputControlByLocalIdentifier $04 Bereich Drehzahl $07 shortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DREHZAHL | unsigned int | Drehzahl, die vom Zeiger angezeigt werden soll Der gewuenschte Drehzahlwert wird direkt (1:1) angegeben.  z.B. fuer 2000 1/min = 2000 angeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-drehzahl-ende"></a>
### STEUERN_DREHZAHL_ENDE

übergibt die Kontrolle über die Drehzahlanzeige wieder an das Kombi KWP2000: $30 InputOutputControlByLocalIdentifier $04 Bereich Drehzahl $00 returnControlToECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-display"></a>
### STEUERN_DISPLAY

steuert die Drehzahl über den Tester KWP2000: $30 InputOutputControlByLocalIdentifier $05 Bereich Display $07 shortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DISPLAY | unsigned char | Gibt das Anzeigeverhalten des Displays vor 0x00 =&gt; Display loeschen 0x01 =&gt; Display komplett ansteuern 0x02 =&gt; Testmuster 1 darstellen 0x03 =&gt; Testmuster 2 darstellen 0x04 =&gt; Testmuster 3 darstellen 0x05 =&gt; Testmuster 4 darstellen 0x06 =&gt; Testmuster 1-4 im Wechsel anzeigen 0xEE =&gt; Erweiterter Modus. 20 Datenbytes mit bitweiser Zuordnung zu den Displaysegmenten muessen hinzugefuegt werden. Achtung: Steuergeraet ueberprueft die Nachrichtenlaenge |
| DATA | string | 20 Bytes mit bitweiser Zuordnung zu den Displaysegmenten Nur erforderlich, wenn DISPLAY = 0xEE Folgende Formate werden unterstuetzt: "00 01 02 03 04..." und "0x00, 0x01, 0x02, 0x03, ..." |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-display-ende"></a>
### STEUERN_DISPLAY_ENDE

übergibt die Kontrolle über die Displayanzeige wieder an das Kombi KWP2000: $30 InputOutputControlByLocalIdentifier $05 Bereich Display $00 returnControlToECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-led"></a>
### STEUERN_LED

steuert die LEDs über den Tester KWP2000: $30 InputOutputControlByLocalIdentifier $02 Bereich LEDs $07 shortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LED_BYTE_1 | unsigned char | Low Byte welches bestimmt für welche LED die Kontrolle wieder an das Kombi übergeben werden soll ---- ---1b  =&gt; Blinker links grün ---- --1-b  =&gt; Blinker rechts grün ---- -1--b  =&gt; Fernlicht blau ---- 1---b  =&gt; ABS rot ---1 ----b  =&gt; ABS gelb --1- ----b  =&gt; Warnleuchte rot -1-- ----b  =&gt; Warnleuchte gelb 1--- ----b  =&gt; Neutral grün |
| LED_BYTE_2 | unsigned char | Low Byte welches bestimmt für welche LED die Kontrolle wieder an das Kombi übergeben werden soll ---- ---1b  =&gt; Öldruck rot ---- --1-b  =&gt; Tank Reserve gelb ---- -1--b  =&gt; DWA LED rot ---- 1---b  =&gt; ASC LED gelb (K27) ---1 ----b  =&gt; Ladekontrolle rot (K27) --1- ----b  =&gt; Zusatzscheinwerfer gruen (K7X_MUE) -1-- ----b  =&gt; MIL gelb (K7x_TUE/LCI) 1--- ----b  =&gt; --- |
| LED_SCHALTEN | unsigned char | bestimmt ob die ausgewählte LED ein oder ausgeschaltet werden soll 0x00 =&gt; LED ausschalten 0x01 =&gt; LED einschalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-led-ende"></a>
### STEUERN_LED_ENDE

übergibt die Kontrolle über die LED wieder an das Kombi KWP2000: $30 InputOutputControlByLocalIdentifier $02 externes Steuern Selbstest $00 returnControlToECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pwm"></a>
### STEUERN_PWM

steuert die Drehzahl über den Tester KWP2000: $30 InputOutputControlByLocalIdentifier $06 Bereich PWM $07 shortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PWM_LCD | unsigned int | PWM Wert fuer die LCD- Beleuchtung Prozentwerte im Bereich von 1 bis 99 sind erlaubt |
| PWM_SUCH | unsigned int | PWM Wert fuer die Such- Beleuchtung Prozentwerte im Bereich von 1 bis 99 sind erlaubt |
| PWM_FUNKTIONS | unsigned int | PWM Wert fuer die Funktions- Beleuchtung Prozentwerte im Bereich von 1 bis 99 sind erlaubt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pwm-ende"></a>
### STEUERN_PWM_ENDE

übergibt die Kontrolle über die Drehzahlanzeige wieder an das Kombi KWP2000: $30 InputOutputControlByLocalIdentifier $06 Bereich PWM $00 returnControlToECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-taster"></a>
### STEUERN_TASTER

steuert die Taster über den Tester KWP2000: $30 InputOutputControlByLocalIdentifier $01 Bereich Taster $07 shortTermAdjustment Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTER | unsigned char | bestimmt welcher Taster von aussen gesteuert werden soll O =&gt; Taste gedrueckt 1 =&gt; Taste nicht gedrueckt 0x01  =&gt; Uhr- Taster 0x02  =&gt; Trip- Taster 0x04  =&gt; Doppeltastendruck |
| TASTENDRUCK_ART | unsigned char | bestimmt welcher Taster von aussen gesteuert werden soll 0x01  =&gt; kurzer Tastendruck 0x02  =&gt; langer Tastendruck |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-taster-ende"></a>
### STEUERN_TASTER_ENDE

übergibt die Kontrolle über die IOs wieder an das Kombi KWP2000: $30 InputOutputControlByLocalIdentifier $01 Bereich Taster $00 returnControlToECU Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-selbsttest"></a>
### START_SELBSTTEST

Starten des Selbsttest KWP2000: $31 StartRoutineByLocalIdentifier $04 Selbstest starten Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stopp-selbsttest"></a>
### STOPP_SELBSTTEST

Stoppen des Selbsttest KWP2000: $32 StopRoutineByLocalIdentifier $04 Selbstest beenden Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-lesen"></a>
### C_FA_LESEN

Fahrzeugauftrag lesen KWP2000: $22   ReadDataByCommonIdentifier $3F00 - $3F7F Fahrzeugauftrag Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string | Daten des Fahrzeugauftrages |
| SPEICHER_STATUS | string | BELEGT bzw. UNBELEGT |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-schreiben"></a>
### C_FA_SCHREIBEN

Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F0A Fahrzeugauftrag Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-fa-auftrag"></a>
### C_FA_AUFTRAG

Fahrzeugauftrag schreiben KWP2000: $2E   WriteDataByCommonIdentifier $3F00 - $3F0A Fahrzeugauftrag Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FAHRZEUGAUFTRAG | string |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ausstattung"></a>
### STATUS_AUSSTATTUNG

liest den Inhalt des Codierblockes 3007 (Ausstattung) KWP2000: $22 InputOutputControlByLocalIdentifier $3007 Block 'Ausstattung' Modus  : Default 1 = Ausstattung ist als aktiv / verbaut  codiert 0 = Ausstattung ist als nicht aktiv / nicht verbaut  codiert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DWA_IST_CODIERT | int | Codierung DWA |
| STAT_ABS_IST_CODIERT | int | Codierung ABS |
| STAT_ABS_SPORTMODE_IST_CODIERT | int | Codierung ABS Sport |
| STAT_DISPLAY_HIGH_VARIANTE_IST_CODIERT | int | Codierung High-Variante (mit Bordcomputer) |
| STAT_EWS_IST_CODIERT | int | Codierung EWS |
| STAT_ASC_IST_CODIERT | int | Codierung ASC |
| STAT_ESA_IST_CODIERT | int | Codierung ESA |
| STAT_RDC_IST_CODIERT | int | Codierung RDC |
| STAT_ABS_VARIANTE | int | Byte zur 'Softwarecodierung' des ABS ueber CAN-Kommunikation |
| STAT_LADEKONTROLLE_IST_CODIERT | int | Codierung Ladekontroll-Leuchte |
| STAT_K27LOW_RESTREICHWEITE_IST_CODIERT | int | RestReichWeiten-Berechnung speziell fuer K27_Low ist codiert |
| STAT_BYTE02_BIT2_IST_CODIERT | int | Block 3007 Byte02 Bit2 |
| STAT_BYTE02_BIT3_IST_CODIERT | int | Block 3007 Byte02 Bit3 |
| STAT_BYTE02_BIT4_IST_CODIERT | int | Block 3007 Byte02 Bit4 |
| STAT_BYTE02_BIT5_IST_CODIERT | int | Block 3007 Byte02 Bit5 |
| STAT_BYTE02_BIT6_IST_CODIERT | int | Block 3007 Byte02 Bit6 |
| STAT_BYTE02_BIT7_IST_CODIERT | int | Block 3007 Byte02 Bit7 |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-gwsz-anzeige-schreiben"></a>
### STEUERN_GWSZ_ANZEIGE_SCHREIBEN

Schreibt einen km Wert in den GWSZ-EEPROM-Bereich KWP2000: $31 StartRoutineByLocalIdentifier $AA GWSZ schreiben Modus  : Default  Damit das Einschreiben funktioniert, muessen folgende Bedingungen erfuellt sein: - GWZS-Offsetzelle im EEPROM muss == 0 sein - neuer GWSZ-Wert muss &gt; alter GWSZ-Wert und &lt; 999999 km sein - Betriebsspannung muss im normalen Bereich sein

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GWSZ_WERT | real | Kilometer-Wert, der in das Kombi geschrieben werden soll (nur ganze km-Werte &lt; 999999 eingeben) |
| GWSZ_ANZEIGE_EINH | string | km od. miles |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-date-time"></a>
### STATUS_DATE_TIME

Kombiinternes Datum und Uhrzeit auslesen KWP2000: $21 ApplDiagReadDataByLocalIdentifier $10 Read Date/Time

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TIME_HH | int | Zeit: Stunden |
| STAT_TIME_MM | int | Zeit: Minuten |
| STAT_TIME_SS | int | ZEIT: Sekunden |
| STAT_DATE_DD | int | Datum: Tag |
| STAT_DATE_MM | int | Datum: Monat |
| STAT_DATE_YYYY | int | Datum: Jahr |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-status-service-date"></a>
### STATUS_SERVICE_DATE

Kombiinternes Service_Datum auslesen KWP2000: $21 ApplDiagReadDataByLocalIdentifier $11 Read Service_Date

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SERV_DATE_DD | int | Service-Datum: Tag |
| STAT_SERV_DATE_MM | int | Service-Datum: Monat |
| STAT_SERV_DATE_YYYY | int | Service-Datum: Jahr |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-steuern-date-time"></a>
### STEUERN_DATE_TIME

kombiinternes Datum und Uhrzeit Setzen KWP2000: $3B ApplDiagWriteDataByLocalIdentifier $10 Set Date/Time Wenn keine Argumente uebergeben werden, werden die Daten werden vom PC bzw. Tester uebernommen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TIME_HH | int | Zeit: Stunden  HH = 0..23 kein Argument - Rechnerzeit |
| TIME_MM | int | Zeit: Minuten  MM = 0..59 kein Argument - Rechnerzeit |
| TIME_SS | int | ZEIT: Sekunden  SS = 0..59 kein Argument - Rechnerzeit |
| DATE_DD | int | Datum: Tag  TT = 1..28,29,30,31 kein Argument - Rechnerdatum |
| DATE_MM | int | Datum: Monat  MM = 1..12 kein Argument - Rechnerdatum |
| DATE_YYYY | int | Datum: Jahr  YYYY = 2006..2099 kein Argument - Rechnerdatum |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-steuern-service-date"></a>
### STEUERN_SERVICE_DATE

kombiinternes Service-Datum Setzen KWP2000: $3B ApplDiagWriteDataByLocalIdentifier $10 Set Service_Date

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERV_DATE_DD | int | Service-Datum: Tag  TT = 1..28,29,30,31 |
| SERV_DATE_MM | int | Service-Datum: Monat  MM = 1..12 |
| SERV_DATE_YYYY | int | Service-Datum: Jahr  YYYY = 2006..2099 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |

<a id="job-steuern-service-restweg"></a>
### STEUERN_SERVICE_RESTWEG

kombiinterne Service-Intervall-Wegstrecke Setzen KWP2000: $3B ApplDiagWriteDataByLocalIdentifier $12 Set Actual Service Mileage Range in [km]

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SERV_WEG_WERT | real | Neuer Startwert fuer Serviceintervallzaehler in km oder meilen bei negativen Werten wird 0 KM fuer das Service-Intervall uebernommen max. Wert &lt;= 65535 |
| SERV_WEG_EINHEIT | string | km od. miles |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-service-restweg"></a>
### STATUS_SERVICE_RESTWEG

Kombiinternen KM-Zaehlerstand bis zum naechsten Service auslesen KWP2000: $21 ApplDiagReadDataByLocalIdentifier $12 Read Actual_Service_Mileage_Range in [km]

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SERV_WEG_WERT | real | Service Wegstrecken_Zaehlerstand [km] |
| STAT_SERV_WEG_EINHEIT | string | km od. miles |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG1 | binary | Hex-Auftrag1 an SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag2 an SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort1 von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort2 von SG |

<a id="job-steuern-hbg-vol-nv-data"></a>
### STEUERN_HBG_VOL_NV_DATA

Setzt den Hebelgeberwert fuer die Tankanzeige auf den Codierwert HBG_RESET KWP2000: $3B WriteDataByLocalIdentifier $0B hbg_reset

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HBG_VOL_WRITE | string | 1 = Anzeige zuruecksetzen 0 = keine Aenderung table DigitalArgument TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-initialisierung"></a>
### INITIALISIERUNG

Initialisierung und Kommunikationsparameter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1, wenn Okay |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (137 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FORTTEXTE](#table-forttexte) (39 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (37 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (4 × 9)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (5 × 2)
- [UB2_LB](#table-ub2-lb) (8 × 2)
- [TABELLE_WARNLEUCHTE_MOTOR](#table-tabelle-warnleuchte-motor) (6 × 2)
- [TABELLE_ANZEIGE_UEBERTEMPERATUR](#table-tabelle-anzeige-uebertemperatur) (4 × 2)
- [TABELLE_DRUCK_OEL](#table-tabelle-druck-oel) (4 × 2)
- [TABELLE_KLEMME_50](#table-tabelle-klemme-50) (4 × 2)
- [TABELLE_EWS](#table-tabelle-ews) (5 × 2)
- [TABELLE_GANG_GETRIEBE](#table-tabelle-gang-getriebe) (9 × 2)
- [TABELLE_HSD_BMSK](#table-tabelle-hsd-bmsk) (6 × 2)
- [TABELLE_LEUCHTE_ASC](#table-tabelle-leuchte-asc) (8 × 2)
- [TABELLE_OELSTAND](#table-tabelle-oelstand) (4 × 2)
- [TABELLE_NOT_AUS](#table-tabelle-not-aus) (4 × 2)
- [TABELLE_SCHALTER_KUPPLUNG](#table-tabelle-schalter-kupplung) (4 × 2)
- [TABELLE_SCHALTAUFFORDERUNG](#table-tabelle-schaltaufforderung) (4 × 2)
- [TABELLE_WARNLEUCHTE_L_MOTOR](#table-tabelle-warnleuchte-l-motor) (6 × 2)
- [TABELLE_LEUCHTE_ABS](#table-tabelle-leuchte-abs) (6 × 2)
- [TABELLE_STEUERUNG_WARNBLINKEN_DWA](#table-tabelle-steuerung-warnblinken-dwa) (4 × 2)
- [TABELLE_STEUERUNG_LED_DWA](#table-tabelle-steuerung-led-dwa) (5 × 2)
- [TABELLE_BATTERIESPANNUNG_DWA](#table-tabelle-batteriespannung-dwa) (5 × 2)
- [TABELLE_KONTROLLEUCHTE_REIFENDRUCKKONTRLLE](#table-tabelle-kontrolleuchte-reifendruckkontrlle) (5 × 2)
- [TABELLE_ZUSATZINFORMATION_REIFENDRUCKKONTROLLE](#table-tabelle-zusatzinformation-reifendruckkontrolle) (6 × 2)
- [TABELLE_BATTERIE_REIFENDRUCKKONTROLLE](#table-tabelle-batterie-reifendruckkontrolle) (4 × 2)
- [TABELLE_STEUERUNG_KONTROLLEUCHTE_LADUNG](#table-tabelle-steuerung-kontrolleuchte-ladung) (4 × 2)
- [TABELLE_ESA](#table-tabelle-esa) (16 × 2)
- [TABELLE_TASTER_BC](#table-tabelle-taster-bc) (5 × 2)
- [TABELLE_KONTROLLEUCHTE_TEMPOMAT](#table-tabelle-kontrolleuchte-tempomat) (5 × 2)
- [TABELLE_WARNUNG_BREMSBELAG](#table-tabelle-warnung-bremsbelag) (4 × 2)
- [TABELLE_ANFORDERUNG_DREHZAHL_SOLLWERT](#table-tabelle-anforderung-drehzahl-sollwert) (4 × 2)
- [TABELLE_SITZHEIZUNG](#table-tabelle-sitzheizung) (16 × 2)
- [TABELLE_TASTER_ESA](#table-tabelle-taster-esa) (5 × 2)
- [TABELLE_KL15](#table-tabelle-kl15) (5 × 2)
- [TABELLE_KL56A](#table-tabelle-kl56a) (5 × 2)
- [TABELLE_SCHALTER_FUSSBREMSE](#table-tabelle-schalter-fussbremse) (5 × 2)
- [TABELLE_BLINKEN_ZFE](#table-tabelle-blinken-zfe) (6 × 2)
- [TABELLE_DIMMUNG](#table-tabelle-dimmung) (4 × 2)

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

Dimensions: 137 rows × 2 columns

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
| 0xB7 | Robert Bosch Battery Systems GmbH |
| 0xB8 | KYOCERA Display Corporation |
| 0xB9 | MAGNA Powertrain AG & Co KG |
| 0xBA | BorgWarner |
| 0xBB | BMW - Fahrzeugsimulator |
| 0xBC | Benteler Duncan Plant |
| 0xBD | U-Shin |
| 0xBE | Schaeffler Technologies |
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

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | ja |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 39 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x930B | Kontrastspannung LCD (bei K7x nicht genutzt) |
| 0x9310 | No ID CAN |
| 0x9311 | ID Ausfall ABS_1 |
| 0x9312 | ID Ausfall ABS_2 |
| 0x9313 | ID Ausfall BMS-K_1 |
| 0x9314 | ID Ausfall BMS-K_2 |
| 0x9315 | ID Ausfall ZFE_1 |
| 0x9316 | ID Ausfall ZFE_2 |
| 0x9317 | ID Ausfall DWA |
| 0x9318 | CAN-Signal ungültig Steuerung Leuchte ABS Motorrad |
| 0x9319 | CAN-Signal ungültig Geschwindigkeit Rad H Motorrad |
| 0x931A | CAN-Signal ungültig Weg Impuls Zaehler H Motorrad |
| 0x931B | GWSZ-Fehler im EEPROM |
| 0x931D | ID Ausfall RDC |
| 0x931E | ID Ausfall ASC |
| 0x931F | ID Ausfall Wegstrecke_Redundant_Motorrad |
| 0x9320 | CAN-Signal ungültig Steuerung LED DWA Motorrad |
| 0x9321 | CAN-Signal ungültig Batteriespannung DWA Motorrad |
| 0x9322 | CAN-Signal ungültig Status Anzeige Übertemperatur Motorrad |
| 0x9323 | CAN-Signal ungültig Status Druck ÖL Motorrad |
| 0x9324 | CAN-Signal ungültig Status EWS Motorrad |
| 0x9325 | Bordnetzspannung (UB Überspannung, Unterspannung) |
| 0x9328 | Codierdaten-Fehler Lieferanten-Bereich |
| 0x9329 | Codierdaten-Fehler BMW-Bereich |
| 0x932A | CAN-Signal ungültig Drehzahl Motor Motorrad |
| 0x932B | CAN-Signal ungültig Status Not- Aus |
| 0x932C | CAN-Signal ungültig Füllstand Tank |
| 0x932D | CAN-Signal ungültig Taste BC |
| 0x932E | CAN-Signal ungültig Status KL15 |
| 0x932F | CAN-Signal ungültig Status KL56 |
| 0x9330 | CAN-Signal ungültig Status Blinken |
| 0x9331 | CAN-Signal ungültig Motor-Warnung |
| 0x9332 | CAN-Signal ungültig Motortemperatur |
| 0x9333 | CAN-Signal ungültig Einspritzmenge |
| 0x9334 | CAN-Signal ungültig Status KL50 |
| 0x9335 | Differenz: km-Stand Kombi / BMSK-P groesser Schwelle |
| 0x9337 | ID Ausfall Anzeige_Modus_Fahrzeug (2E0h) |
| 0xE107 | Bus Off |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 37 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x930B | 1 | 2 | 3 | - |
| 0x9310 | 1 | 2 | 3 | - |
| 0x9311 | 1 | 2 | 3 | - |
| 0x9312 | 1 | 2 | 3 | - |
| 0x9313 | 1 | 2 | 3 | - |
| 0x9314 | 1 | 2 | 3 | - |
| 0x9315 | 1 | 2 | 3 | - |
| 0x9316 | 1 | 2 | 3 | - |
| 0x9317 | 1 | 2 | 3 | - |
| 0x9318 | 1 | 2 | 3 | - |
| 0x9319 | 1 | 2 | 3 | - |
| 0x931A | 1 | 2 | 3 | - |
| 0x931B | 1 | 2 | 3 | - |
| 0x931D | 1 | 2 | 3 | - |
| 0x931E | 1 | 2 | 3 | - |
| 0x9320 | 1 | 2 | 3 | - |
| 0x9321 | 1 | 2 | 3 | - |
| 0x9322 | 1 | 2 | 3 | - |
| 0x9323 | 1 | 2 | 3 | - |
| 0x9324 | 1 | 2 | 3 | - |
| 0x9325 | 1 | 2 | 3 | - |
| 0x9328 | 1 | 2 | 3 | - |
| 0x9329 | 1 | 2 | 3 | - |
| 0x932A | 1 | 2 | 3 | - |
| 0x932B | 1 | 2 | 3 | - |
| 0x932C | 1 | 2 | 3 | - |
| 0x932D | 1 | 2 | 3 | - |
| 0x932E | 1 | 2 | 3 | - |
| 0x932F | 1 | 2 | 3 | - |
| 0x9330 | 1 | 2 | 3 | - |
| 0x9331 | 1 | 2 | 3 | - |
| 0x9332 | 1 | 2 | 3 | - |
| 0x9333 | 1 | 2 | 3 | - |
| 0x9334 | 1 | 2 | 3 | - |
| 0x9335 | 1 | 2 | 3 | - |
| 0x9337 | 1 | 2 | 3 | - |
| 0xFFFF | 1 | 2 | 3 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 4 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | Bordnetzspannung | Volt | - | unsigned char | - | 1 | 10 | 0 |
| 2 | spez. Erweiterung | 0-n | - | 0xFF | UB2_LB | 1 | 2 | 3 |
| 3 | Geschwindigkeit | km/h | - | unsigned char | - | 2 | 1 | 0 |
| 0xXYXY | UWB_UNKNOWN | - | - | - | - | - | - | - |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
| F_ART_ERW | nein |
| F_PCODE | nein |
| F_PCODE7 | nein |
| F_HFK | nein |
| F_LZ | nein |
| F_UWB_ERW | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 5 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| - | BMW-FAST |
| - | KWP2000* |
| 1 | KWP2000 |
| - | DS2 |
| 2 | D-CAN |

<a id="table-ub2-lb"></a>
### UB2_LB

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | UNUSED |
| 0x01 | ID FEHLT |
| 0x02 | ALIVE FEHLER |
| 0x04 | KOMPLEMENTFEHLER |
| 0x08 | KONSISTENZFEHLER |
| 0x10 | UNKRITISCHER_FEHLER |
| 0x20 | KRITISCHER_FEHLER |
| 0xXY | ERROR_UNKNOWN |

<a id="table-tabelle-warnleuchte-motor"></a>
### TABELLE_WARNLEUCHTE_MOTOR

Dimensions: 6 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Leuchte Aus |
| 0x02 | Blinken 1Hz |
| 0x04 | Blinken 4 Hz |
| 0x05 | Dauerlicht |
| 0x07 | ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-anzeige-uebertemperatur"></a>
### TABELLE_ANZEIGE_UEBERTEMPERATUR

Dimensions: 4 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Temperatur OK |
| 0x02 | Temperatur zu hoch |
| 0x03 | ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-druck-oel"></a>
### TABELLE_DRUCK_OEL

Dimensions: 4 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | kein Oeldruck |
| 0x02 | Oeldruck vorhanden |
| 0x03 | ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-klemme-50"></a>
### TABELLE_KLEMME_50

Dimensions: 4 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Relais aktiviert |
| 0x02 | Relais nicht aktiviert |
| 0x03 | ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-ews"></a>
### TABELLE_EWS

Dimensions: 5 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x00 | Schluessel noch nicht abgefragt |
| 0x01 | Schluessel gueltig |
| 0x02 | Schluessel ungueltig |
| 0x03 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-gang-getriebe"></a>
### TABELLE_GANG_GETRIEBE

Dimensions: 9 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | 1. Gang |
| 0x02 | Leerlauf |
| 0x04 | 2. Gang |
| 0x07 | 3. Gang |
| 0x08 | 4. Gang |
| 0x0B | 5. Gang |
| 0x0D | 6. Gang |
| 0x0F | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-hsd-bmsk"></a>
### TABELLE_HSD_BMSK

Dimensions: 6 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x00 | kein Fehler erkannt |
| 0x01 | Fehler am HSD1 |
| 0x02 | Fehler am HSD2 |
| 0x04 | Fehler an HSD3 |
| 0x07 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-leuchte-asc"></a>
### TABELLE_LEUCHTE_ASC

Dimensions: 8 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x00 | ASC Aus/Fehler |
| 0x01 | ASC Komfortmodus Ein |
| 0x02 | GS Mode Ein |
| 0x03 | ASC noch nicht initialisiert |
| 0x05 | ASC regelt Komfort Modus |
| 0x06 | ASC regelt GS Modus |
| 0x07 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-oelstand"></a>
### TABELLE_OELSTAND

Dimensions: 4 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Oelstand in Ordnung |
| 0x02 | Oelstand zu gering |
| 0x03 | ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-not-aus"></a>
### TABELLE_NOT_AUS

Dimensions: 4 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Not Aus betaetigt |
| 0x02 | Not Aus nicht betaetigt |
| 0x03 | ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-schalter-kupplung"></a>
### TABELLE_SCHALTER_KUPPLUNG

Dimensions: 4 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Kupplungsschalter AUS |
| 0x02 | Kupplungsschalter EIN |
| 0x03 | ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-schaltaufforderung"></a>
### TABELLE_SCHALTAUFFORDERUNG

Dimensions: 4 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Schaltaufforderung nicht aktiv |
| 0x02 | Schaltaufforderung aktiv |
| 0x03 | ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-warnleuchte-l-motor"></a>
### TABELLE_WARNLEUCHTE_L_MOTOR

Dimensions: 6 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Leuchte Aus |
| 0x02 | Blinken 1Hz |
| 0x04 | Blinken 4 Hz |
| 0x05 | Dauerlicht |
| 0x07 | ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-leuchte-abs"></a>
### TABELLE_LEUCHTE_ABS

Dimensions: 6 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Leuchte Aus |
| 0x02 | Blinken 1Hz |
| 0x04 | Blinken 4 Hz |
| 0x05 | Dauerlicht |
| 0x07 | ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-steuerung-warnblinken-dwa"></a>
### TABELLE_STEUERUNG_WARNBLINKEN_DWA

Dimensions: 4 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Leuchte Aus |
| 0x02 | Leuchte Ein |
| 0x03 | ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-steuerung-led-dwa"></a>
### TABELLE_STEUERUNG_LED_DWA

Dimensions: 5 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x00 | Blinken 1Hz |
| 0x01 | Leuchte Aus |
| 0x02 | Leuchte Ein |
| 0x03 | ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-batteriespannung-dwa"></a>
### TABELLE_BATTERIESPANNUNG_DWA

Dimensions: 5 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Ladezustand i.O. |
| 0x02 | Ladezustand n.i.O. |
| 0x03 | Batterie entladen |
| 0x07 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-kontrolleuchte-reifendruckkontrlle"></a>
### TABELLE_KONTROLLEUCHTE_REIFENDRUCKKONTRLLE

Dimensions: 5 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Warnleuchte L und RDC Icon AUS |
| 0x02 | Warnleuchte L in gelb und RDC Icon AN |
| 0x04 | Warnleuchte L in rot und RDC Icon AN |
| 0x07 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-zusatzinformation-reifendruckkontrolle"></a>
### TABELLE_ZUSATZINFORMATION_REIFENDRUCKKONTROLLE

Dimensions: 6 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | kein Fehler |
| 0x02 | Fehler im Vorderrad |
| 0x03 | Fehler im Hinterrad |
| 0x04 | Fehler in beiden Raedern |
| 0x07 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-batterie-reifendruckkontrolle"></a>
### TABELLE_BATTERIE_REIFENDRUCKKONTROLLE

Dimensions: 4 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Symbol AUS |
| 0x02 | Symbol EIN |
| 0x03 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-steuerung-kontrolleuchte-ladung"></a>
### TABELLE_STEUERUNG_KONTROLLEUCHTE_LADUNG

Dimensions: 4 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Leuchte AUS |
| 0x02 | Leuchte EIN |
| 0x03 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-esa"></a>
### TABELLE_ESA

Dimensions: 16 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | E-C (Fahrer - Comfort) |
| 0x02 | E-N (Fahrer - Normal) |
| 0x03 | E-S (Fahrer - Sport) |
| 0x04 | EB-C (Fahrer+Gepaeck - Comfort) |
| 0x05 | EB-N (Fahrer+Gepaeck - Normal) |
| 0x06 | EB-S (Fahrer+Gepaeck - Sport) |
| 0x07 | SO-C (Soziusbetrieb - Comfort) |
| 0x08 | SO-N (Soziusbetrieb - Normal) |
| 0x09 | SO-S (Soziusbetrieb - Sport) |
| 0x0A | ESA-Anzeige ausgeblendet |
| 0x0B | nicht verwendet |
| 0x0C | ESA-Anzeige ausgeschaltet |
| 0x0D | nicht verwendet |
| 0x0E | nicht verwendet |
| 0x0F | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-taster-bc"></a>
### TABELLE_TASTER_BC

Dimensions: 5 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x00 | Taster nicht gedrueckt |
| 0x01 | Taster gedrueckt |
| 0x02 | Taster laenger als 2 sec gedrueckt |
| 0x03 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-kontrolleuchte-tempomat"></a>
### TABELLE_KONTROLLEUCHTE_TEMPOMAT

Dimensions: 5 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x00 | Signal fehlerhaft |
| 0x01 | Leuchte AUS |
| 0x02 | Leuchte EIN |
| 0x03 | Signal fehlerhaft |
| 0xXY | reserviert |

<a id="table-tabelle-warnung-bremsbelag"></a>
### TABELLE_WARNUNG_BREMSBELAG

Dimensions: 4 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Bremsbelag i.O. |
| 0x02 | Bremsbelag verschlissen |
| 0x03 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-anforderung-drehzahl-sollwert"></a>
### TABELLE_ANFORDERUNG_DREHZAHL_SOLLWERT

Dimensions: 4 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | LL-Anhebung nicht angefordert |
| 0x02 | LL-Anhebung angefordert |
| 0x03 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-sitzheizung"></a>
### TABELLE_SITZHEIZUNG

Dimensions: 16 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Fahrer Aus, Beifahrer Aus |
| 0x02 | Fahrer Stufe 1, Beifahrer Aus |
| 0x03 | Fahrer Stufe 2, Beifahrer Aus |
| 0x04 | Fahrer Aus, Beifahrer Stufe 1 |
| 0x05 | Fahrer Aus, Beifahrer Stufe 2 |
| 0x06 | Fahrer Stufe 1, Beifahrer Stufe 1 |
| 0x07 | Fahrer Stufe 1, Beifahrer Stufe 2 |
| 0x08 | Fahrer Stufe 2, Beifahrer Stufe 1 |
| 0x09 | Fahrer Stufe 2, Beifahrer Stufe 2 |
| 0x0A | nicht verwendet |
| 0x0B | nicht verwendet |
| 0x0C | nicht verwendet |
| 0x0D | nicht verwendet |
| 0x0E | nicht verwendet |
| 0x0F | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-taster-esa"></a>
### TABELLE_TASTER_ESA

Dimensions: 5 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x00 | Taster nicht gedrueckt |
| 0x01 | Taster &lt; 1 sec gedrueckt |
| 0x02 | Taster &gt; 1 sec gedrueckt |
| 0x03 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-kl15"></a>
### TABELLE_KL15

Dimensions: 5 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x00 | reserviert |
| 0x01 | Schalter in Stellung AUS |
| 0x02 | Klemme 15 Ein |
| 0x03 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-kl56a"></a>
### TABELLE_KL56A

Dimensions: 5 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Leuchte in Ordnung und aktiv |
| 0x02 | Leuchte AUS |
| 0x04 | Leuchte defekt |
| 0x07 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-schalter-fussbremse"></a>
### TABELLE_SCHALTER_FUSSBREMSE

Dimensions: 5 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Schalter betaetigt |
| 0x02 | Schalter nicht betaetigt |
| 0x04 | Schalter Fehler |
| 0x07 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-blinken-zfe"></a>
### TABELLE_BLINKEN_ZFE

Dimensions: 6 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | beide Blinker AUS |
| 0x02 | Blinker links   EIN |
| 0x04 | Blinker rechts EIN |
| 0x05 | beide Blinker EIN |
| 0x07 | Signal ungueltig |
| 0xXY | reserviert |

<a id="table-tabelle-dimmung"></a>
### TABELLE_DIMMUNG

Dimensions: 4 rows × 2 columns

| CODE | KLARTEXT |
| --- | --- |
| 0x01 | Tageinstellung |
| 0x02 | Nachteinstellung |
| 0x03 | Signal ungueltig |
| 0xXY | reserviert |
