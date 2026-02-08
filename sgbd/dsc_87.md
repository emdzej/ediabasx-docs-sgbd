# dsc_87.prg

- Jobs: [121](#jobs)
- Tables: [37](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Dynamische Stabilitaets Control DSC E87,E90  |
| ORIGIN | BMW EF-513 Kusch |
| REVISION | 21.000 |
| AUTHOR | BMW EF-513 Kusch |
| COMMENT | Conti_Teves MK60, BMW_FAST, E8x,E9x ausser E83 / 84 und E9x-16 |
| PACKAGE | 1.52 |
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
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
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
- [SEED](#job-seed) - Status Eingaenge E87 DSC_MK60 KWP2000:$27,$03 oder  $27,$07 SecurityAccess service
- [IDENT_PRODUCTION_DATA](#job-ident-production-data) - KWP2000: $1A,$8F ReadECUIdentification Ident-Daten des SG ...
- [IDENT_VIN](#job-ident-vin) - KWP2000: $1A,$90 ReadECUIdentification Ident-Daten des SG: Fahrgestellnummer
- [IDENT_TEVES_ECU_SW_NR](#job-ident-teves-ecu-sw-nr) - KWP2000: $1A,$94 ReadECUIdentification Ident-Daten des SG: SW Nummer
- [IDENT_PROGRAMMING_DATE](#job-ident-programming-date) - KWP2000: $1A,$99 ReadECUIdentification Ident-Daten des SG: Herstelldatum
- [C_C_SCHREIBEN](#job-c-c-schreiben) - Codierdaten schreiben Standard Codierjob Fuer die Codierdaten werden als Argument ein vorgefuellter Binaerbuffer uebergeben KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und ruecklesen Standard Codierjob Fuer die Codierdaten werden als Argument ein vorgefuellter Binaerbuffer uebergeben KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [_COD_SCHREIBEN_DSC](#job-cod-schreiben-dsc) - KWP2000: $2E WriteDataByCommonIdentifier $3000 Codierdaten schreiben Es koennen beliebige viele Codierdaten als ein Hex_String uebergeben werden: z.B. 01,AB,56,FF ... 16 Keine Checksumme im ersten Datenbyte eingeben die Checksumme wird automatisch berechnet die Telegrammlaenge wird automatisch berechnet Job DIAGNOSE_MODE ist integriert
- [_COD_SCHREIBEN_ZUSATZFUNKTIONEN](#job-cod-schreiben-zusatzfunktionen) - Zusatzfunktionen auscodieren Es kann max. 1 Argument uebergeben werden BB_ON oder BB_OFF:    Bremsbereitschaft SST_ON oder SST_OFF:  Softstop TB_ON oder TB_OFF:    Trockenbremsen AFA_ON oder AFA_OFF:  Anfahrassistent FBS_ON oder FBS_OFF:  Fading Brake Support ASL_ON oder ASL_OFF:  Anhaengerschlingerlogik DEF_E5:               setzt die Defaultcodierung fuer MK60_E5 DEF_PSI:              setzt die Defaultcodierung fuer MK60_PSI Argument: z.B.: SST_OFF werden keine Argumente übergeben, dann werden die ausgelesenen Codierdaten unveraendert zurueckgeschrieben KWP2000: $2E WriteDataByCommonIdentifier $300x codingDataSet Modus  : Default
- [_COD_SCHREIBEN_SZL](#job-cod-schreiben-szl) - KWP2000: $2E WriteDataByCommonIdentifier $3001 Codierdaten schreiben Es muss 1 Codierbyte uebergeben werden Bereich: 0-255 bzw. 0x00-0xFF Musterametersatz: 12 oder 0x0C Job DIAGNOSE_MODE ist integriert
- [_COD_LESEN](#job-cod-lesen) - Auslesen der Codierdaten Es muessen 2 Byte (Blocknummer) als Hex_String uebergeben werden Argument fur DSC: z.B.: 30,00 Argument fur SZL: z.B.: 30,01 KWP2000: $22 ReadDataByCommonIdentifier $300x Codierdaten Modus  : Default
- [STATUS_RADGESCHWINDIGKEIT](#job-status-radgeschwindigkeit) - Fuer die Zuordnung Text-Wertausgabe, siehe Tabelle RAD KWP2000: $21,$07 ReadDataByLocalIdentifier service Radgeschwindigkeiten auslesen
- [STATUS_SCHALTER](#job-status-schalter) - KWP2000: $21,$05 ReadDataByLocalIdentifier service
- [STATUS_SENSOREN](#job-status-sensoren) - KWP2000: $21,$06 ReadDataByLocalIdentifier service gueltig ab I3.70
- [STATUS_SENSOREN_OFFSET](#job-status-sensoren-offset) - KWP2000: $21,$02 ReadDataByLocalIdentifier service gueltig ab I3.70
- [BET_AKTIV](#job-bet-aktiv) - Bandendetest aktivieren KWP2000: $31 StartRoutineByLocalIdentifier service $23 BET BET_AKTIV beinhaltet den Job DIAGNOSE_MODE
- [BET_PASSIV](#job-bet-passiv) - Bandendetest passiv schalten KWP2000: $31 StartRoutineByLocalIdentifier service $23 BET BET_PASSIV beinhaltet den Job DIAGNOSE_MODE
- [STEUERN_DIGITAL_DX](#job-steuern-digital-dx) - KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) davon koennen bis maximal 9 Argumente vorgegeben werden E or W EVVL AVVL EVVR AVVR EVHL AVHL EVHR AVHR PUMPE SV1 SV2 EUV1 EUV2 Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode,  und Ansteuersequenz-Ausfuehren: Mit dem Parameter"W" wird nur die Ansteuersequenz ausgefuehrt Musterparametersatz_1: "E,EVVL,EVVR,SV1,0,0,0,0,0,0,800,PUMPE,0,0,0,0,0,0,0,0,1000" Musterparametersatz_2: "W,EVVL,EVVR,EVHL,EVHR,AVVL,AVVR,AVHL,AVHR,0,200,PUMPE,0,0,0,0,0,0,0,0,2000" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) in jedem Job koennen dann 9 beliebige Stellglieder angesteuert werden und zwar 1 Stellgliedgruppe vor dem Zeitglied und 1 Stellgliedgruppe nach dem Zeitglied dazwischen steht das Argument fuer die Wartezeit:  W_ZEIT in ms als letzter Parameter steht eine Wartezeit zum Job Status OK WAIT_STATUS_JOB in ms NUR volle tausender Werte eingeben (1000,2000....) eine Stellgliedgruppe besteht immer aus 9 Argumenten (9 Stellglieder) werden weniger als 9 Stellglieder angesteuert so sind die restlichen mit "0" zu besetzen(siehe Musterparametersatz_1)
- [STEUERN_DIGITAL](#job-steuern-digital) - KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) es koennen  maximal 17 Argumente vorgegeben werden E oder W,EVVL, AVVL,EVVR,AVVR,EVHL,AVHL,EVHR,AVHR,PUMPE,SV1,SV2,EUV1,EUV2 Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode,  und Ansteuersequenz-Ausfuehren: Mit dem Parameter"W" wird nur die Ansteuersequenz ausgefuehrt Musterparametersatz_1: "E,EVVL,EVVR,SV1,800,PUMPE," Musterparametersatz_2: "W,EVVL,EVVR,EVHL,EVHR,AVVL,AVVR,1000,AVHL,AVHR,PUMPE" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) es koennen 2 beliebige Stellgliedgruppen angesteuert werden und zwar 1 Stellgliedgruppe vor dem Zeitglied und 1 Stellgliedgruppe nach dem Zeitglied dazwischen steht das Argument fuer die Wartezeit in ms
- [STEUERN_DIGITAL_BLS](#job-steuern-digital-bls) - KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) Es koennen max 13 Ausgaenge vorgegeben werden E or W EVVL AVVL EVVR AVVR EVHL AVHL EVHR AVHR PUMPE SV1 SV2 EUV1 EUV2 BLS Musterparametersatz: "W,EVVL,EVVR,EVHL,EVHR,AVVL,AVVR,PUMPE" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) Die Ventilansteuerung wird solange wiederholt, bis der Bremslichtschalter wieder geloest wird, max. jedoch 200 Zyklen lang (ca.8sec) die Ventilansteuersequenz wird vor und hinter dem Zeitglied identisch eingetragen der Defaultzeitwert (Zeitglied) beträgt 10ms
- [NA_ENTLUEFTUNG_RE_DX](#job-na-entlueftung-re-dx) - Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert
- [NA_ENTLUEFTUNG_LI_DX](#job-na-entlueftung-li-dx) - Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert
- [NA_ENTLUEFTUNG_VA_DX](#job-na-entlueftung-va-dx) - Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert
- [NA_ENTLUEFTUNG_HA_DX](#job-na-entlueftung-ha-dx) - Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert
- [_VAKUUM_DX](#job-vakuum-dx) - Job dient der Vakuumbefuellung waehrend der Evakuierungsphase werden die AV- und die DSC-Umschaltventile fuer 10 sec angetaktet Job DIAGNOSE_MODE ist integriert
- [_VAKUUM_PUMPE_DX](#job-vakuum-pumpe-dx) - Job dient der Vakuumbefuellung waehrend der Befuellphase wird die Pumpe und es werden die AV- und die DSC-Umschaltventile fuer 10 sec angetaktet Job DIAGNOSE_MODE ist integriert
- [IDENT_SCHREIBEN](#job-ident-schreiben) - KWP2000: $3B WriteDataByLocalIdentifier $80 BMW Identifikation schreiben
- [IDENT_PROGRAMMING_DATE_SCHREIBEN](#job-ident-programming-date-schreiben) - KWP2000:$3B,$99 WriteDataByLocalIdentifier service Ident-Daten des SG schreiben: Herstelldatum
- [IDENT_PRODUCTION_DATA_SCHREIBEN](#job-ident-production-data-schreiben) - KWP2000:$3B,$8F WriteDataByLocalIdentifier service Ident-Daten des SG schreiben
- [STATUS_LWS_LI_RE_MAX](#job-status-lws-li-re-max) - Auslesen der CAN Botschaft LWS_1 KWP2000: $22 ReadDataByCommonIdentifier $01F5 CAN_LWS_1 Job laeuft max. 16 sec: werden die Max-Werte vorher erreicht, wird der Job abgebrochen
- [STATUS_LESEN_RPA](#job-status-lesen-rpa) - KWP2000:$21,$04 ReadDataByLocalIdentifier service Alle RPA Daten auslesen
- [RPA_RESET](#job-rpa-reset) - KWP2000:$31,$25 StartRoutineByLocalIdentifier service resertiert alle gelernten RPA Werte
- [RPA_EOL_PASSIV](#job-rpa-eol-passiv) - KWP2000:$31,$26 StartRoutineByLocalIdentifier service Auslieferungsmodus der Werke lernt keinen neuen RPA Werte RPA muss beim Kunden resertiert werden
- [_FS_LESEN_SAR](#job-fs-lesen-sar) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus    : Default
- [_ANZAHL_SUBBUS_TEILNEHMER_LESEN](#job-anzahl-subbus-teilnehmer-lesen) - Anzahl Subbus Teilnehmer lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 Anzahl Subbus Teilnehmer lesen Modus    : Default
- [DF_AUSGANG_AKTIVIEREN](#job-df-ausgang-aktivieren) - KWP2000:$31,$27 StartRoutineByLocalIdentifier service 5. Drehzahlfühlerausgang aktivieren
- [STATUS_CBS_SENSOR_BBV](#job-status-cbs-sensor-bbv) - CBS Bremsbelagverschleiss (BBV) Sensor auslesen Verschleiss-Schwellen: 2_stufig Fuer die Zuordnung Text-Wert siehe Tabelle CBS_BBV KWP2000: $21 $09 ReadDataByCommonIdentifier Modus  : Default
- [STATUS_CBS_BBV_DICKE](#job-status-cbs-bbv-dicke) - Lesen  CBS Bremsbelagdicke und Korrekturfaktoren KWP2000: $23 $03ReadMemoryByAddress
- [DRUCKSENSOR_DSC_ABGLEICHEN](#job-drucksensor-dsc-abgleichen) - KWP2000: $31,$20 StartRoutineByLocalIdentifier service
- [QUERBESCHLEUNIGUNG_DSC_ABGLEICHEN](#job-querbeschleunigung-dsc-abgleichen) - KWP2000: $31,$22 StartRoutineByLocalIdentifier service
- [LAENGSBESCHLEUNIGUNG_DSC_ABGLEICHEN](#job-laengsbeschleunigung-dsc-abgleichen) - KWP2000: $31,$24 StartRoutineByLocalIdentifier service
- [LENKWINKEL_DSC_ABGLEICHEN](#job-lenkwinkel-dsc-abgleichen) - KWP2000: $31,$21 StartRoutineByLocalIdentifier service
- [ABGLEICH_ANALOG_EV](#job-abgleich-analog-ev) - KWP2000:$31,$28 StartRoutineByLocalIdentifier service Abgleich Analog Einlassventil
- [ABGLEICH_ANALOG_MCI_V](#job-abgleich-analog-mci-v) - KWP2000:$31,$29 StartRoutineByLocalIdentifier service Abgleich Analog MCI Ventile
- [STAT_ERGEBNIS_ABGLEICH_ROUTINE](#job-stat-ergebnis-abgleich-routine) - Ergebnis der Routine abholen Musterparametersatz: "ANALOG_MCI_V" fuer Abgleich Analog MCI Ventil Musterparametersatz: "ANALOG_EV" fuer Abgleich der analogen Einlassventile Musterparametersatz: "LWS" fuer Abgleich Lenkwinkelsensor oder mit 2. Argument "R": "ANALOG_EV,R" oder "ANALOG_MCI_V,R" oder "LWS,R" dann wird eine Schleife max. 20sec durchlaufen, bis endgueltiges Ergebnis der Routine vorliegt jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) Fuer die Zuordnung der Ausgabe Text-Wert siehe Tabelle ABGLEICH_V_ERGEBNIS KWP2000: $33 $28/$29 RequestRoutineResultsByLocalIdentifier
- [STATUS_F_CAN_TASTER_AUDIO_TEL](#job-status-f-can-taster-audio-tel) - Botschaft des Tasters Audio/Telefon auslesen Fuer die Zuordnung Text-Wertausgabe, siehe Tabelle AUDIO_TEL KWP2000: $22 ReadDataByCommonIdentifier $01D6 Botschaft des Tasters Audio/Telefon auslesen Modus    : Default
- [STATUS_F_CAN_TEMPOMAT_ACC](#job-status-f-can-tempomat-acc) - Botschaft des Tempomats/ACC auslesen Fuer die Zuordnung Text-Wertausgabe, siehe Tabelle TEMP_ACC KWP2000: $22 ReadDataByCommonIdentifier $0194 - Botschaft des Tempomats/ACC auslesen Modus    : Default
- [STATUS_F_CAN_WISCHERTASTER](#job-status-f-can-wischertaster) - Botschaft desWischertasters auslesen Fuer die Zuordnung Text-Wertausgabe, siehe Tabelle WISCHER KWP2000: $22 ReadDataByCommonIdentifier $02A6 - Botschaft des Wischertasters auslesen Modus    : Default
- [_FS_BUS_LOESCHEN](#job-fs-bus-loeschen) - KWP2000: $14 ClearDiagnosticInformation FFFE Fehlerspeicher loeschen Job DIAGNOSE_MODE ist integriert
- [_FS_BUS_LESEN](#job-fs-bus-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus nur fuer Bus-Fehlercodes:0xFF,0xFE Modus  : Default
- [_CCP_MODE](#job-ccp-mode) - KWP2000:$31,$31 StartRoutineByLocalIdentifier service CCP Mode aktivieren wird nur im Access-Level D unterstuetzt Job nicht mehr in Serienprojekten verfuegbar
- [_TEL_SCHREIBEN](#job-tel-schreiben) - KWP2000 Dieser Job bietet die Moeglichkeit an, ein eigenes Telegramm zu verschicken Es muessen 2 Argumente eingegeben werden, beide mit "Strich_Punkt" getrennt (nicht mit Komma!): Erstes Argument: E oder W Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode und Telegramm-Ausfuehren: Mit dem Parameter"W" wird nur das Telegramm ausgefuehrt Zweiter Argument: Die ersten 3 Bytes des Telegramms (Format,Target,Source) sind schon vorhanden die restlichen Bytes als ein Hex_String, alle mit Komma getrennt z.B. 00,11,22,... Keine Laenge eingeben, sie wird automatisch berechnet Musterparametersatz_1: "E,00,11,22,33" Musterparametersatz_2: "W,00,11,22,33" Aufpassen: 2 Argumente (E_OR_W,T_BYTES) mit "Strich_Punkt" getrennt (nicht mit Komma !) nach dem E oder W immer "Strich_Punkt" aber folgende T_Bytes mit Komma getrennt!
- [STATUS_F_CAN_LW](#job-status-f-can-lw) - ab V10.000 wird nur noch die C9 Botschaft ausgelesen (vorher C8) Botschaft des Lenkwinkels auslesen (wird von VS benoetigt), um zwischen Lenkwinkel_Oben (LWS) und Summen_LW (AFS) zu unterscheiden Fuer die Zuordnung Text-Wert siehe Tabelle F_CAN_LW KWP2000: $22 ReadDataByCommonIdentifier $0118 Botschaft des Austausch_AFS_DSC auslesen KWP2000: $22 ReadDataByCommonIdentifier $00C9 Botschaft des Lenkradwinkel_Oben auslesen Modus    : Default
- [STATUS_F_CAN_TYP_SENSORCLUSTER](#job-status-f-can-typ-sensorcluster) - F_CAN Botschaft CLU6 (Clustertyp: Anforderung der Werke), Unterscheidung ohne/mit redundantem Gierratensensor Fuer die Zuordnung Text-Wert siehe Tabelle F_CAN_CLUSTER KWP2000: $22 ReadDataByCommonIdentifier $0140 Botschaft CLU6 auslesen Modus    : Default
- [_FS_LESEN_INPA](#job-fs-lesen-inpa) - KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes KWP2000: $18 ReadDiagnosticTroubleCodesByStatus kombinierter Job §17 und §18 Fehlerspeicher lesen mit allen Umweltdaten Ausgabe der Results wie INPA
- [_EEPROM_LESEN](#job-eeprom-lesen) - Lesen  EEPROM Zellen Zwei Argumente muessen eingegeben werden: die Start-Adresse und die End-Adresse. Musterparametersatz: "Start-Adresse,End-Adresse", jedoch mit "Strichpunkt" getrennt. Musterparametersatz: "224,244", jedoch mit "Strichpunkt" getrennt. Musterparametersatz: "0x00E0,0x00F4", jedoch mit "Strichpunkt" getrennt. Adressenbereich: 0x000000 - 0x0003FF KWP2000: $23 $03 ReadMemoryByAddress
- [_STATUS_ADCR](#job-status-adcr) - Lesen  EEPROM Zellen Adressenbereich: 0x000000 - 0x0003FF KWP2000: $23 $03 ReadMemoryByAddress
- [_FS_LESEN_SELEKTIV](#job-fs-lesen-selektiv) - Fehlerspeicher lesen (Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Es muss ein Argument eingegeben werden: "DSC" oder "dsc", um DSC Fehler auszulesen "BUS" oder "bus", um BUS Fehler auszulesen "SZL" oder "szl", um SZL Fehler auszulesen
- [BET_AKTIV_1](#job-bet-aktiv-1) - Bandendetest aktivieren KWP2000: $31 StartRoutineByLocalIdentifier service $23 BET BET_AKTIV beinhaltet den Job DIAGNOSE_MODE
- [STATUS_EVENT_COUNTER](#job-status-event-counter) - KWP2000: $22,$F01x ReadDataByCommonIdentifier service
- [LAENGSBESCHLEUNIGUNG_PLAUSICHECK_PASSIV](#job-laengsbeschleunigung-plausicheck-passiv) - KWP2000: $31,$30 StartRoutineByLocalIdentifier service deaktiviert den Laengsbeschleunigungsplausicheck waehrend der Rollenfahrt im Prüfstand
- [STATUS_EVENT_LOESCHEN](#job-status-event-loeschen) - KWP2000: $2E,$F01x WriteDataByCommonIdentifier service loescht den Event Counter Es kann max. 1 Argument uebergeben werden FLR:   loescht den Zaehler Eingriffe Fahrleistungsreduzierung FBS_1: loescht den Zaehler Fading Brake Support Schwelle 1 FBS_2: loescht den Zaehler Fading Brake Support Schwelle 2 DSC:   loescht die km-Laufleistung DSC passiv getastet SPORT: loescht die km-Laufleistung Sport Mode aktiv getastet DTC:   loescht den Zaehler DTC Taster EIN getastet ASC:   loescht den Zaehler ASC Temperaturabschaltungen Argument: z.B.: DSC
- [STATUS_IDENT_HYDRAULIK](#job-status-ident-hydraulik) - Auslesen des DSC Sensor-Clusters KWP2000: $22 ReadDataByCommonIdentifier $1603 DSC Ident Hydraulik lesen Modus    : Default
- [STATUS_IDENT_SENSORCLUSTER](#job-status-ident-sensorcluster) - Auslesen des DSC Sensor-Clusters KWP2000: $22 ReadDataByCommonIdentifier $1602 DSC Sensor-Cluster  lesen Modus    : Default
- [STATUS_IDENT_SZL](#job-status-ident-szl) - Auslesen der Schalt_Zentrum_Lenksäule KWP2000: $22 ReadDataByCommonIdentifier $1601 Schalt_Zentrum_Lenksäule lesen Modus    : Default
- [STATUS_IDENT_SENSORCLUSTER_2](#job-status-ident-sensorcluster-2) - Auslesen des 2. DSC Sensor-Clusters (nur AFS) KWP2000: $22 ReadDataByCommonIdentifier $1604 DSC Sensor-Cluster  lesen Modus    : Default
- [STATUS_WLC_ZAEHLER](#job-status-wlc-zaehler) - KWP2000: $21,$0A ReadDataByLocalIdentifier service Anzahl der Wandler Launch Control (WLC) Beschleunigungsvorgaenge bei Zaehlerstand 500 wird die WLC-Funktion deaktiviert es erfolgt ein Info-Eintrag in den Fehlerspeicher Wechsel der DSC Hydraulikeinheit erforderlich
- [WLC_ZAEHLER_SCHREIBEN](#job-wlc-zaehler-schreiben) - KWP2000: $3B,$0A WriteDataByLocalIdentifier service schreibt den WLC Zaehlerstand, Security Level B erforderlich Eingabe des Zaehlerstandes als Dezimalzahl Argument: z.B.: 431 kein Argument schreibt den Zaehlerstand 0xFFFF (Anlieferungszustand)
- [STEUERN_HYDRO_SPUELEN](#job-steuern-hydro-spuelen) - DSC Hydroaggregat spuelen nach der Befuellung soll Nacharbeit beim Pedalchecker reduzieren dieser Job ist nur fuer die Fertigung relevant Job DIAGNOSE_MODE ist integriert
- [STATUS_LESEN_RPA_M5](#job-status-lesen-rpa-m5) - KWP2000:$21,$04 ReadDataByLocalIdentifier service Alle RPA Daten auslesen
- [_STATUS_LESEN_RPA_M3](#job-status-lesen-rpa-m3) - KWP2000:$21,$0B ReadDataByLocalIdentifier service Alle RPA Daten auslesen
- [PRE_VENTIL_KALIBRIERUNG](#job-pre-ventil-kalibrierung) - Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

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
| AVAI_CBS_WERT_DAD | int | Verfuegbarkeit DAD in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_ZKRZ_A | int | Verfuegbarkeit ZKRZ_A in %, fuer Pruefablauf Bandende |
| AVAI_CBS_WERT_H2 | int | Verfuegbarkeit H2 in %, fuer Pruefablauf Bandende |
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
| CBS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, ZKrz, Sic, Kfl, TUV, AU, Ueb, H2 Werte externe Umfaenge: Oel, Br_v, Br_h, Filt, CSF, Batt, VTG, ZKrz_a, DAD Defaultwert: 0x00 (ungueltig) |
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

<a id="job-seed"></a>
### SEED

Status Eingaenge E87 DSC_MK60 KWP2000:$27,$03 oder  $27,$07 SecurityAccess service

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | gewuenschter Diagnose-Modus table DiagMode MODE MODE_TEXT Defaultwert: DEFAULT (DefaultMode) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| MODE_TEXT | string | Mode als Textausgabe |
| _TEL_AUFTRAG_1 | binary | Anforderungstelegramm |
| _TEL_AUFTRAG_2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |
| JOB_STATUS | string | OKAY, oder FEHLER |

<a id="job-ident-production-data"></a>
### IDENT_PRODUCTION_DATA

KWP2000: $1A,$8F ReadECUIdentification Ident-Daten des SG ...

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-vin"></a>
### IDENT_VIN

KWP2000: $1A,$90 ReadECUIdentification Ident-Daten des SG: Fahrgestellnummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer 14-stellig, WBA vorangestellt |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-teves-ecu-sw-nr"></a>
### IDENT_TEVES_ECU_SW_NR

KWP2000: $1A,$94 ReadECUIdentification Ident-Daten des SG: SW Nummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| SW_NR | string | Softwarenummer 12 Zeichen |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-programming-date"></a>
### IDENT_PROGRAMMING_DATE

KWP2000: $1A,$99 ReadECUIdentification Ident-Daten des SG: Herstelldatum

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_DATUM_MONAT | int | Herstelldatum (Monat) |
| ID_DATUM_TAG | int | Herstelldatum (Tag) |
| ID_DATUM | string | Herstelldatum (TT.MM.JJJJ) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-c-c-schreiben"></a>
### C_C_SCHREIBEN

Codierdaten schreiben Standard Codierjob Fuer die Codierdaten werden als Argument ein vorgefuellter Binaerbuffer uebergeben KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag |

<a id="job-c-c-auftrag"></a>
### C_C_AUFTRAG

Codierdaten schreiben und ruecklesen Standard Codierjob Fuer die Codierdaten werden als Argument ein vorgefuellter Binaerbuffer uebergeben KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : Codierdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG |

<a id="job-cod-schreiben-dsc"></a>
### _COD_SCHREIBEN_DSC

KWP2000: $2E WriteDataByCommonIdentifier $3000 Codierdaten schreiben Es koennen beliebige viele Codierdaten als ein Hex_String uebergeben werden: z.B. 01,AB,56,FF ... 16 Keine Checksumme im ersten Datenbyte eingeben die Checksumme wird automatisch berechnet die Telegrammlaenge wird automatisch berechnet Job DIAGNOSE_MODE ist integriert

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| C_BYTES | string | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cod-schreiben-zusatzfunktionen"></a>
### _COD_SCHREIBEN_ZUSATZFUNKTIONEN

Zusatzfunktionen auscodieren Es kann max. 1 Argument uebergeben werden BB_ON oder BB_OFF:    Bremsbereitschaft SST_ON oder SST_OFF:  Softstop TB_ON oder TB_OFF:    Trockenbremsen AFA_ON oder AFA_OFF:  Anfahrassistent FBS_ON oder FBS_OFF:  Fading Brake Support ASL_ON oder ASL_OFF:  Anhaengerschlingerlogik DEF_E5:               setzt die Defaultcodierung fuer MK60_E5 DEF_PSI:              setzt die Defaultcodierung fuer MK60_PSI Argument: z.B.: SST_OFF werden keine Argumente übergeben, dann werden die ausgelesenen Codierdaten unveraendert zurueckgeschrieben KWP2000: $2E WriteDataByCommonIdentifier $300x codingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG | string | Zusatzfunktion |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary |  |

<a id="job-cod-schreiben-szl"></a>
### _COD_SCHREIBEN_SZL

KWP2000: $2E WriteDataByCommonIdentifier $3001 Codierdaten schreiben Es muss 1 Codierbyte uebergeben werden Bereich: 0-255 bzw. 0x00-0xFF Musterametersatz: 12 oder 0x0C Job DIAGNOSE_MODE ist integriert

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| C_BYTE | int | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cod-lesen"></a>
### _COD_LESEN

Auslesen der Codierdaten Es muessen 2 Byte (Blocknummer) als Hex_String uebergeben werden Argument fur DSC: z.B.: 30,00 Argument fur SZL: z.B.: 30,01 KWP2000: $22 ReadDataByCommonIdentifier $300x Codierdaten Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| C_BLOCK | string | Codierblock 30,00 ... 30,05 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-radgeschwindigkeit"></a>
### STATUS_RADGESCHWINDIGKEIT

Fuer die Zuordnung Text-Wertausgabe, siehe Tabelle RAD KWP2000: $21,$07 ReadDataByLocalIdentifier service Radgeschwindigkeiten auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STAT_RAD_GESCHW_VL_WERT | long | Radgeschwindigkeit vorne links |
| STAT_RAD_GESCHW_VR_WERT | long | Radgeschwindigkeit vorne rechts |
| STAT_RAD_GESCHW_HL_WERT | long | Radgeschwindigkeit hinten links |
| STAT_RAD_GESCHW_HR_WERT | long | Radgeschwindigkeit hinten rechts |
| STAT_RICHTUNG_VL_TEXT | string | Drehrichtung vorne links |
| STAT_RICHTUNG_VL_WERT | int | Drehrichtung vorne links |
| STAT_RICHTUNG_VR_TEXT | string | Drehrichtung vorne rechts |
| STAT_RICHTUNG_VR_WERT | int | Drehrichtung vorne rechts |
| STAT_RICHTUNG_HL_TEXT | string | Drehrichtung hinten links |
| STAT_RICHTUNG_HL_WERT | int | Drehrichtung hinten links |
| STAT_RICHTUNG_HR_TEXT | string | Drehrichtung hinten rechts |
| STAT_RICHTUNG_HR_WERT | int | Drehrichtung hinten rechts |
| STAT_RAD_GESCHW_EINH | string | Einheit = km/h |
| STAT_DFA_SIM_TEXT | string | Simulation Drehzahlfuehlerausgang |
| STAT_DFA_SIM_WERT | int | Simulation Drehzahlfuehlerausgang |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-schalter"></a>
### STATUS_SCHALTER

KWP2000: $21,$05 ReadDataByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BREMSLICHT_SCHALTER_EIN | int | 0 oder 1 |
| STAT_HANDBREMSE_SCHALTER_EIN | int | 0 oder 1 |
| STAT_DSC_TASTER_EIN | int | 0 oder 1 |
| STAT_DSC_PASSIV | int | 0 oder 1 |
| STAT_BREMSFLUESSIGKEIT_NIVEAU_SCHALTER_EIN | int | 0 oder 1 |
| STAT_RPA_RESET_TASTER_EIN | int | 0 oder 1 |
| STAT_DFA_WERK_MODE | int | 0 = Normal Mode / 1 = Werk-Mode , nur wenn DFA verfuegbar ist |
| STAT_RPA_EOL_PASSIV | int | 0 oder 1 |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sensoren"></a>
### STATUS_SENSOREN

KWP2000: $21,$06 ReadDataByLocalIdentifier service gueltig ab I3.70

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_DREHRATE_WERT | real | Geschwindigkeitswert des Drehratensensor [Grad/sec] |
| STAT_QUERBESCHLEUNIGUNG_WERT | real | Beschleunigungswert des Querbeschleunigungssensor [g] |
| STAT_LAENGSBESCHLEUNIGUNG_WERT | real | Beschleunigungswert des Laengsbeschleunigungssensor [g] |
| STAT_DRUCKSENSOR_1_WERT | real | Druckwert des Drucksensors 1 [bar] |
| STAT_SENSOR_TEMPERATUR_WERT | real | Temperatur im Steuergeraet [Grad] |
| STAT_SPANNUNG_UREF_WERT | real | Spannung [Volt] |
| STAT_SPANNUNG_PUMPE_WERT | real | Spannung [Volt] |
| STAT_SPANNUNG_KLEMME_30_WERT | real | Spannung [Volt] |
| STAT_SPANNUNG_VCC_WERT | real | Spannung [Volt] |
| STAT_SENSOR_TEMPERATUR_EINH | string | [Grad] |
| STAT_DREHRATE_EINH | string | [Grad/sec] |
| STAT_QUERBESCHLEUNIGUNG_EINH | string | [g] |
| STAT_LAENGSBESCHLEUNIGUNG_EINH | string | [g] |
| STAT_DRUCKSENSOR_EINH | string | bar |
| STAT_SENSOR_SPANNUNG_EINH | string | Volt |
| STAT_QUERBESCHLEUNIGUNG_AFS_WERT | real | AFS Querbeschleunigung [g] |
| STAT_DREHRATE_AFS_WERT | real | AFS Gierrate [Grad/sec] |
| STAT_LENKWINKEL_EINH | string | [Grad] |
| STAT_DRUCKSENSOR_VL_WERT | real | Druckwert des Drucksensors VL [bar] |
| STAT_DRUCKSENSOR_VR_WERT | real | Druckwert des Drucksensors VR [bar] |
| STAT_DRUCKSENSOR_HL_WERT | real | Druckwert des Drucksensors HL [bar] |
| STAT_DRUCKSENSOR_HR_WERT | real | Druckwert des Drucksensors HR [bar] |
| STAT_LENKWINKEL_WERT | real | Lenkwinkel oben [Grad] |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sensoren-offset"></a>
### STATUS_SENSOREN_OFFSET

KWP2000: $21,$02 ReadDataByLocalIdentifier service gueltig ab I3.70

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_OFFSET_LENKWINKEL_WERT | real | Offsetwert des Lenkwinkels |
| STAT_OFFSET_LENKWINKEL_EINH | string | Einheit des Offsetwerts des Lenkwinkels [Grad] |
| STAT_OFFSET_QUERBESCHLEUNIGUNG_WERT | real | Offsetwert der Querbeschleunigung |
| STAT_OFFSET_LAENGSBESCHLEUNIGUNG_WERT | real | Offsetwert der Laengsbeschleunigung |
| STAT_OFFSET_QUERBESCHLEUNIGUNG_EINH | string | Einheit des Offsetwerts der Querbeschleunigung [g] |
| STAT_OFFSET_LAENGSBESCHLEUNIGUNG_EINH | string | Einheit des Offsetwerts der Laengsbeschleunigung [g] |
| STAT_OFFSET_DREHRATE_WERT | real | Offsetwert der Drehrate |
| STAT_OFFSET_DREHRATE_EINH | string | Einheit des Offsetwertes der Drehrate [Grad/sec] |
| STAT_OFFSET_DRUCKSENSOR_1_WERT | real | Offsetwert des Drucksensors 2 |
| STAT_OFFSET_DRUCKSENSOR_EINH | string | Einheit des Offsetwerts des Drucksensors [bar] |
| STAT_OFFSET_QUERBESCHLEUNIGUNG_AFS_WERT | real | Offsetwert der AFS Querbeschleunigung |
| STAT_OFFSET_DREHRATE_AFS_WERT | real | Offsetwert der AFS Drehrate |
| STAT_OFFSET_DRUCKSENSOR_VL_WERT | real | Offsetwert des Drucksensors VL |
| STAT_OFFSET_DRUCKSENSOR_VR_WERT | real | Offsetwert des Drucksensors VR |
| STAT_OFFSET_DRUCKSENSOR_HL_WERT | real | Offsetwert des Drucksensors HL |
| STAT_OFFSET_DRUCKSENSOR_HR_WERT | real | Offsetwert des Drucksensors HR |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bet-aktiv"></a>
### BET_AKTIV

Bandendetest aktivieren KWP2000: $31 StartRoutineByLocalIdentifier service $23 BET BET_AKTIV beinhaltet den Job DIAGNOSE_MODE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-bet-passiv"></a>
### BET_PASSIV

Bandendetest passiv schalten KWP2000: $31 StartRoutineByLocalIdentifier service $23 BET BET_PASSIV beinhaltet den Job DIAGNOSE_MODE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-digital-dx"></a>
### STEUERN_DIGITAL_DX

KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) davon koennen bis maximal 9 Argumente vorgegeben werden E or W EVVL AVVL EVVR AVVR EVHL AVHL EVHR AVHR PUMPE SV1 SV2 EUV1 EUV2 Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode,  und Ansteuersequenz-Ausfuehren: Mit dem Parameter"W" wird nur die Ansteuersequenz ausgefuehrt Musterparametersatz_1: "E,EVVL,EVVR,SV1,0,0,0,0,0,0,800,PUMPE,0,0,0,0,0,0,0,0,1000" Musterparametersatz_2: "W,EVVL,EVVR,EVHL,EVHR,AVVL,AVVR,AVHL,AVHR,0,200,PUMPE,0,0,0,0,0,0,0,0,2000" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) in jedem Job koennen dann 9 beliebige Stellglieder angesteuert werden und zwar 1 Stellgliedgruppe vor dem Zeitglied und 1 Stellgliedgruppe nach dem Zeitglied dazwischen steht das Argument fuer die Wartezeit:  W_ZEIT in ms als letzter Parameter steht eine Wartezeit zum Job Status OK WAIT_STATUS_JOB in ms NUR volle tausender Werte eingeben (1000,2000....) eine Stellgliedgruppe besteht immer aus 9 Argumenten (9 Stellglieder) werden weniger als 9 Stellglieder angesteuert so sind die restlichen mit "0" zu besetzen(siehe Musterparametersatz_1)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |
| ORT1 | string | gewuenschte Komponente 1 |
| ORT2 | string | gewuenschte Komponente 2 |
| ORT3 | string | gewuenschte Komponente 3 |
| ORT4 | string | gewuenschte Komponente 4 |
| ORT5 | string | gewuenschte Komponente 5 |
| ORT6 | string | gewuenschte Komponente 6 |
| ORT7 | string | gewuenschte Komponente 7 |
| ORT8 | string | gewuenschte Komponente 8 |
| ORT9 | string | gewuenschte Komponente 9 |
| W_ZEIT | int | Wartezeit vor Ansteuerung  naechster Stellgliedersequenz |
| ORT10 | string | gewuenschte Komponente 10 |
| ORT11 | string | gewuenschte Komponente 11 |
| ORT12 | string | gewuenschte Komponente 12 |
| ORT13 | string | gewuenschte Komponente 13 |
| ORT14 | string | gewuenschte Komponente 14 |
| ORT15 | string | gewuenschte Komponente 15 |
| ORT16 | string | gewuenschte Komponente 16 |
| ORT17 | string | gewuenschte Komponente 17 |
| ORT18 | string | gewuenschte Komponente 18 |
| WAIT_STATUS_JOB | int | Wartezeit bis Job Status kommt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-steuern-digital"></a>
### STEUERN_DIGITAL

KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) es koennen  maximal 17 Argumente vorgegeben werden E oder W,EVVL, AVVL,EVVR,AVVR,EVHL,AVHL,EVHR,AVHR,PUMPE,SV1,SV2,EUV1,EUV2 Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode,  und Ansteuersequenz-Ausfuehren: Mit dem Parameter"W" wird nur die Ansteuersequenz ausgefuehrt Musterparametersatz_1: "E,EVVL,EVVR,SV1,800,PUMPE," Musterparametersatz_2: "W,EVVL,EVVR,EVHL,EVHR,AVVL,AVVR,1000,AVHL,AVHR,PUMPE" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) es koennen 2 beliebige Stellgliedgruppen angesteuert werden und zwar 1 Stellgliedgruppe vor dem Zeitglied und 1 Stellgliedgruppe nach dem Zeitglied dazwischen steht das Argument fuer die Wartezeit in ms

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |
| ORT1 | string | gewuenschte Komponente 1 |
| ORT2 | string | gewuenschte Komponente 2 |
| ORT3 | string | gewuenschte Komponente 3 |
| ORT4 | string | gewuenschte Komponente 4 |
| ORT5 | string | gewuenschte Komponente 5 |
| ORT6 | string | gewuenschte Komponente 6 |
| ORT7 | string | gewuenschte Komponente 7 |
| ORT8 | string | gewuenschte Komponente 8 |
| ORT9 | string | gewuenschte Komponente 9 |
| ORT10 | string | gewuenschte Komponente 10 |
| ORT11 | string | gewuenschte Komponente 11 |
| ORT12 | string | gewuenschte Komponente 12 |
| ORT13 | string | gewuenschte Komponente 13 |
| ORT14 | string | gewuenschte Komponente 14 |
| ORT15 | string | gewuenschte Komponente 15 |
| ORT16 | string | gewuenschte Komponente 16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-steuern-digital-bls"></a>
### STEUERN_DIGITAL_BLS

KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) Es koennen max 13 Ausgaenge vorgegeben werden E or W EVVL AVVL EVVR AVVR EVHL AVHL EVHR AVHR PUMPE SV1 SV2 EUV1 EUV2 BLS Musterparametersatz: "W,EVVL,EVVR,EVHL,EVHR,AVVL,AVVR,PUMPE" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) Die Ventilansteuerung wird solange wiederholt, bis der Bremslichtschalter wieder geloest wird, max. jedoch 200 Zyklen lang (ca.8sec) die Ventilansteuersequenz wird vor und hinter dem Zeitglied identisch eingetragen der Defaultzeitwert (Zeitglied) beträgt 10ms

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |
| ORT1 | string | gewuenschte Komponente 1 |
| ORT2 | string | gewuenschte Komponente 2 |
| ORT3 | string | gewuenschte Komponente 3 |
| ORT4 | string | gewuenschte Komponente 4 |
| ORT5 | string | gewuenschte Komponente 5 |
| ORT6 | string | gewuenschte Komponente 6 |
| ORT7 | string | gewuenschte Komponente 7 |
| ORT8 | string | gewuenschte Komponente 8 |
| ORT9 | string | gewuenschte Komponente 9 |
| ORT10 | string | gewuenschte Komponente 10 |
| ORT11 | string | gewuenschte Komponente 11 |
| ORT12 | string | gewuenschte Komponente 12 |
| ORT13 | string | gewuenschte Komponente 13 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_BREMSLICHT_SCHALTER_EIN | int | 0 oder 1 |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |

<a id="job-na-entlueftung-re-dx"></a>
### NA_ENTLUEFTUNG_RE_DX

Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-na-entlueftung-li-dx"></a>
### NA_ENTLUEFTUNG_LI_DX

Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-na-entlueftung-va-dx"></a>
### NA_ENTLUEFTUNG_VA_DX

Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-na-entlueftung-ha-dx"></a>
### NA_ENTLUEFTUNG_HA_DX

Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-vakuum-dx"></a>
### _VAKUUM_DX

Job dient der Vakuumbefuellung waehrend der Evakuierungsphase werden die AV- und die DSC-Umschaltventile fuer 10 sec angetaktet Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-vakuum-pumpe-dx"></a>
### _VAKUUM_PUMPE_DX

Job dient der Vakuumbefuellung waehrend der Befuellphase wird die Pumpe und es werden die AV- und die DSC-Umschaltventile fuer 10 sec angetaktet Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-ident-schreiben"></a>
### IDENT_SCHREIBEN

KWP2000: $3B WriteDataByLocalIdentifier $80 BMW Identifikation schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATAS | string | Es muessen 29 Ident_Daten als ein Hex_String uebergeben werden: z.B. 01,AB,56,FF ... 29 Bereich:  0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-programming-date-schreiben"></a>
### IDENT_PROGRAMMING_DATE_SCHREIBEN

KWP2000:$3B,$99 WriteDataByLocalIdentifier service Ident-Daten des SG schreiben: Herstelldatum

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATAS | string | Es muessen 4 Ident_Daten als ein Hex_String uebergeben werden: z.B. 19,99,12,27 Datum: 27.12.1999 Bereich:  0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-production-data-schreiben"></a>
### IDENT_PRODUCTION_DATA_SCHREIBEN

KWP2000:$3B,$8F WriteDataByLocalIdentifier service Ident-Daten des SG schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATAS | string | Es muessen 12 Ident_Daten als ein Hex_String uebergeben werden: z.B. 01,02,03,04,05 ... 12 Bereich:  0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lws-li-re-max"></a>
### STATUS_LWS_LI_RE_MAX

Auslesen der CAN Botschaft LWS_1 KWP2000: $22 ReadDataByCommonIdentifier $01F5 CAN_LWS_1 Job laeuft max. 16 sec: werden die Max-Werte vorher erreicht, wird der Job abgebrochen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LENKWINKEL_WERT_LI_MAX | real | Einschlag Lenkrad [Grad] |
| STAT_LENKWINKEL_WERT_RE_MAX | real | Einschlag Lenkrad [Grad] |
| STAT_LENKWINKEL_WERT_LI_MAX_SAR | real | Einschlag Lenkrad/10 [Grad] fuer SAR Pruefstand |
| STAT_LENKWINKEL_WERT_RE_MAX_SAR | real | Einschlag Lenkrad/10 [Grad] fuer SAR Pruefstand |
| STAT_LENKWINKEL_EINH | string | [Grad] |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lesen-rpa"></a>
### STATUS_LESEN_RPA

KWP2000:$21,$04 ReadDataByLocalIdentifier service Alle RPA Daten auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STAT_KM_RESET | long | Umweltbedingung Kilometerstand beim letzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_WARNUNG | long | Umweltbedingung Kilometerstand beim letzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_RESET_MINUS_1 | long | Umweltbedingung Kilometerstand beim vorletzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_WARNUNG_MINUS_1 | long | Umweltbedingung Kilometerstand beim vorletzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_RESET_MINUS_2 | long | Umweltbedingung Kilometerstand beim vorvorletzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_WARNUNG_MINUS_2 | long | Umweltbedingung Kilometerstand beim vorvorletzten Reset Wertebereich: 0 - 524280 km |
| STAT_GESCHWINDIGKEITSBEREICH_1_TEXT | string | Geschwindigkeitsbereich 1 |
| STAT_GESCHWINDIGKEITSBEREICH_2_TEXT | string | Geschwindigkeitsbereich 2 |
| STAT_GESCHWINDIGKEITSBEREICH_3_TEXT | string | Geschwindigkeitsbereich 3 |
| STAT_GESCHWINDIGKEITSBEREICH_4_TEXT | string | Geschwindigkeitsbereich 4 |
| STAT_GESCHWINDIGKEITSBEREICH_5_TEXT | string | Geschwindigkeitsbereich 5 |
| STAT_GESCHWINDIGKEITSBEREICH_6_TEXT | string | Geschwindigkeitsbereich 6 |
| STAT_DRUCKSCHWELLE_GROB_1 | int | Lernbereich Druckschwelle grob 3 |
| STAT_DRUCKSCHWELLE_GROB_2 | int | Lernbereich Druckschwelle grob 4 |
| STAT_DRUCKSCHWELLE_GROB_3 | int | Lernbereich Druckschwelle grob 3 |
| STAT_DRUCKSCHWELLE_GROB_4 | int | Lernbereich Druckschwelle grob 4 |
| STAT_DRUCKSCHWELLE_GROB_5 | int | Lernbereich Druckschwelle grob 5 |
| STAT_DRUCKSCHWELLE_GROB_6 | int | Lernbereich Druckschwelle grob 6 |
| STAT_DRUCKSCHWELLE_FEIN_1 | int | Lernbereich Druckschwelle fein 3 |
| STAT_DRUCKSCHWELLE_FEIN_2 | int | Lernbereich Druckschwelle fein 4 |
| STAT_DRUCKSCHWELLE_FEIN_3 | int | Lernbereich Druckschwelle fein 3 |
| STAT_DRUCKSCHWELLE_FEIN_4 | int | Lernbereich Druckschwelle fein 4 |
| STAT_DRUCKSCHWELLE_FEIN_5 | int | Lernbereich Druckschwelle fein 5 |
| STAT_DRUCKSCHWELLE_FEIN_6 | int | Lernbereich Druckschwelle fein 6 |
| STAT_ACHSE_LERN_IM_BEREICH_0_50_NM | int | Momentenkompensation 1 |
| STAT_ACHSE_LERN_IM_BEREICH_50_100_NM | int | Momentenkompensation 2 |
| STAT_ACHSE_LERN_IM_BEREICH_100_150_NM | int | Momentenkompensation 3 |
| STAT_ACHSE_LERN_IM_BEREICH_150_200_NM | int | Momentenkompensation 4 |
| STAT_ACHSE_LERN_IM_BEREICH_200_250_NM | int | Momentenkompensation 5 |
| STAT_ACHSE_LERN_IM_BEREICH_250_300_NM | int | Momentenkompensation 6 |
| STAT_ACHSE_LERN_SCHNELL_IM_BEREICH_0_50_NM | int | Momentenkompensation 1 |
| STAT_ACHSE_LERN_SCHNELL_IM_BEREICH_50_100_NM | int | Momentenkompensation 2 |
| STAT_ACHSE_LERN_SCHNELL_IM_BEREICH_100_150_NM | int | Momentenkompensation 3 |
| STAT_ACHSE_LERN_SCHNELL_IM_BEREICH_150_200_NM | int | Momentenkompensation 4 |
| STAT_KURVENKOMPENSATION_1 | int | Kurvenkompensation 1 |
| STAT_KURVENKOMPENSATION_2 | int | Kurvenkompensation 2 |
| STAT_KURVENKOMPENSATION_3 | int | Kurvenkompensation 3 |
| STAT_KURVENKOMPENSATION_4 | int | Kurvenkompensation 4 |
| STAT_KURVENKOMPENSATION_5 | int | Kurvenkompensation 5 |
| STAT_KURVENKOMPENSATION_6 | int | Kurvenkompensation 6 |
| STAT_KURVENKOMPENSATION_7 | int | Kurvenkompensation 7 |
| STAT_KURVENKOMPENSATION_8 | int | Kurvenkompensation 8 |
| STAT_KURVENKOMPENSATION_1_TEXT | string | Text zur Kurvenkompensation 1 |
| STAT_KURVENKOMPENSATION_2_TEXT | string | Text zur Kurvenkompensation 2 |
| STAT_KURVENKOMPENSATION_3_TEXT | string | Text zur Kurvenkompensation 3 |
| STAT_KURVENKOMPENSATION_4_TEXT | string | Text zur Kurvenkompensation 4 |
| STAT_KURVENKOMPENSATION_5_TEXT | string | Text zur Kurvenkompensation 5 |
| STAT_KURVENKOMPENSATION_6_TEXT | string | Text zur Kurvenkompensation 6 |
| STAT_KURVENKOMPENSATION_7_TEXT | string | Text zur Kurvenkompensation 7 |
| STAT_KURVENKOMPENSATION_8_TEXT | string | Text zur Kurvenkompensation 8 |
| STAT_WARNUNG_AKTUELL | int | Anzahl aktueller Warnungen |
| STAT_WARN_HISTORY_1 | int | Warnvorgeschichte 1 |
| STAT_WARN_HISTORY_2 | int | Warnvorgeschichte 2 |
| STAT_WARN_HISTORY_3 | int | Warnvorgeschichte 3 |
| STAT_WARN_HISTORY_4 | int | Warnvorgeschichte 4 |
| STAT_WARN_HISTORY_5 | int | Warnvorgeschichte 5 |
| STAT_WARN_HISTORY_6 | int | Warnvorgeschichte 6 |
| STAT_WARN_HISTORY_7 | int | Warnvorgeschichte 7 |
| STAT_WARN_HISTORY_8 | int | Warnvorgeschichte 8 |
| STAT_WARN_GRUND_1 | int | Warngrund 1 |
| STAT_WARN_GRUND_2 | int | Warngrund 2 |
| STAT_WARN_GRUND_3 | int | Warngrund 3 |
| STAT_WARN_GRUND_4 | int | Warngrund 4 |
| STAT_WARN_GRUND_5 | int | Warngrund 5 |
| STAT_WARN_GRUND_6 | int | Warngrund 6 |
| STAT_WARN_GRUND_7 | int | Warngrund 7 |
| STAT_WARN_GRUND_8 | int | Warngrund 8 |
| STAT_WARN_TEXT_1 | string | Warntext 1 |
| STAT_WARN_TEXT_2 | string | Warntext 2 |
| STAT_WARN_TEXT_3 | string | Warntext 3 |
| STAT_WARN_TEXT_4 | string | Warntext 4 |
| STAT_WARN_TEXT_5 | string | Warntext 5 |
| STAT_WARN_TEXT_6 | string | Warntext 6 |
| STAT_WARN_TEXT_7 | string | Warntext 7 |
| STAT_WARN_TEXT_8 | string | Warntext 8 |
| STAT_FUNKTIONSTEST | int | Funktionstest abgeschlossen nein/ja [0/1] |
| STAT_ACHSE_LERN_SCHNELL_BEENDET | int | Einlernvorgang Achse beendet nein/ja [0/1] |
| STAT_DELTA_PANNEN_SCHWELLWERT | int | Pannen-Schwellwert |
| STAT_DELTA_PANNEN_SCHWELLWERT_EINH | string | Einheit Pannen-Schwellwert |
| STAT_PANNEN_ZAEHLER | int | Pannenzaehler |
| STAT_L1 | int | Lernstati 1 |
| STAT_L1_EINH | string | Einheit Lernstati 1 [%] |
| STAT_L2 | int | Lernstati 2 |
| STAT_L2_EINH | string | Einheit Lernstati 2 [%] |
| STAT_L3 | int | Lernstati 3 |
| STAT_L3_EINH | string | Einheit Lernstati 3 [%] |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |

<a id="job-rpa-reset"></a>
### RPA_RESET

KWP2000:$31,$25 StartRoutineByLocalIdentifier service resertiert alle gelernten RPA Werte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-rpa-eol-passiv"></a>
### RPA_EOL_PASSIV

KWP2000:$31,$26 StartRoutineByLocalIdentifier service Auslieferungsmodus der Werke lernt keinen neuen RPA Werte RPA muss beim Kunden resertiert werden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-sar"></a>
### _FS_LESEN_SAR

Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table FOrtTexte ORTTEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-anzahl-subbus-teilnehmer-lesen"></a>
### _ANZAHL_SUBBUS_TEILNEHMER_LESEN

Anzahl Subbus Teilnehmer lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 Anzahl Subbus Teilnehmer lesen Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ANZAHL_SUBBUS_TEILNEHMER | int | Anzahl der intelligenten Sensoren am F_CAN |

<a id="job-df-ausgang-aktivieren"></a>
### DF_AUSGANG_AKTIVIEREN

KWP2000:$31,$27 StartRoutineByLocalIdentifier service 5. Drehzahlfühlerausgang aktivieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DF_AUSGANG_ZUSTAND | string | P = passiv, nicht aktivieren oder S = Stillstand oder F = Fahrt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cbs-sensor-bbv"></a>
### STATUS_CBS_SENSOR_BBV

CBS Bremsbelagverschleiss (BBV) Sensor auslesen Verschleiss-Schwellen: 2_stufig Fuer die Zuordnung Text-Wert siehe Tabelle CBS_BBV KWP2000: $21 $09 ReadDataByCommonIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CBS_BBV_SENSOR_VA_TEXT | string | Status CBS_BBV Sensor VA |
| STAT_CBS_BBV_SENSOR_VA_WERT | int | Status CBS_BBV Sensor VA |
| STAT_CBS_BBV_SENSOR_HA_TEXT | string | Status CBS_BBV Sensor HA |
| STAT_CBS_BBV_SENSOR_HA_WERT | int | Status CBS_BBV Sensor HA |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-cbs-bbv-dicke"></a>
### STATUS_CBS_BBV_DICKE

Lesen  CBS Bremsbelagdicke und Korrekturfaktoren KWP2000: $23 $03ReadMemoryByAddress

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_CBS_BBV_DICKE_VA | long | Bremsbelagdicke |
| STAT_CBS_BBV_DICKE_HA | long | Bremsbelagdicke |
| STAT_CBS_BBV_DICKE_EINH | string | Einheit = mm |
| STAT_CBS_BBV_KORR_VA | long | Korrekturfaktor VA |
| STAT_CBS_BBV_KORR_HA | long | Korrekturfaktor HA |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_AUFTRAG_2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |
| _TEL_AUFTRAG_3 | binary | Anforderungstelegramm |
| _TEL_ANTWORT_3 | binary | Antworttelegramm |
| _TEL_AUFTRAG_4 | binary | Anforderungstelegramm |
| _TEL_ANTWORT_4 | binary | Antworttelegramm |

<a id="job-drucksensor-dsc-abgleichen"></a>
### DRUCKSENSOR_DSC_ABGLEICHEN

KWP2000: $31,$20 StartRoutineByLocalIdentifier service

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-querbeschleunigung-dsc-abgleichen"></a>
### QUERBESCHLEUNIGUNG_DSC_ABGLEICHEN

KWP2000: $31,$22 StartRoutineByLocalIdentifier service

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-laengsbeschleunigung-dsc-abgleichen"></a>
### LAENGSBESCHLEUNIGUNG_DSC_ABGLEICHEN

KWP2000: $31,$24 StartRoutineByLocalIdentifier service

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-lenkwinkel-dsc-abgleichen"></a>
### LENKWINKEL_DSC_ABGLEICHEN

KWP2000: $31,$21 StartRoutineByLocalIdentifier service

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LWS_OFFSET_KORREKTUR_GRAD | real | LWS-Offset in Grad Unbedingt ein PUNKT als Dezimaltrennzeichen benutzen Format: -0.123 Gueltigkeitsbereich: -1°.. 1° Offset=0 (Defaultwert), wenn kein Argument uebergeben wird |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |

<a id="job-abgleich-analog-ev"></a>
### ABGLEICH_ANALOG_EV

KWP2000:$31,$28 StartRoutineByLocalIdentifier service Abgleich Analog Einlassventil

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-abgleich-analog-mci-v"></a>
### ABGLEICH_ANALOG_MCI_V

KWP2000:$31,$29 StartRoutineByLocalIdentifier service Abgleich Analog MCI Ventile

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-stat-ergebnis-abgleich-routine"></a>
### STAT_ERGEBNIS_ABGLEICH_ROUTINE

Ergebnis der Routine abholen Musterparametersatz: "ANALOG_MCI_V" fuer Abgleich Analog MCI Ventil Musterparametersatz: "ANALOG_EV" fuer Abgleich der analogen Einlassventile Musterparametersatz: "LWS" fuer Abgleich Lenkwinkelsensor oder mit 2. Argument "R": "ANALOG_EV,R" oder "ANALOG_MCI_V,R" oder "LWS,R" dann wird eine Schleife max. 20sec durchlaufen, bis endgueltiges Ergebnis der Routine vorliegt jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) Fuer die Zuordnung der Ausgabe Text-Wert siehe Tabelle ABGLEICH_V_ERGEBNIS KWP2000: $33 $28/$29 RequestRoutineResultsByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TYP | string | Typ der Routine angeben |
| RESULT | string | mit R als Argument wird das Result mehrfach abgefragt, bis pos. Ergebnis vorliegt ohne R als Argument liefert dieser Job nur einmal das Result der Routine zurück |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_ERGEBNIS_BYTE_TEXT_1 | string | Text |
| STAT_ERGEBNIS_BYTE_WERT_1 | int | Text |
| STAT_ERGEBNIS_BYTE_TEXT_2 | string | Text |
| STAT_ERGEBNIS_BYTE_WERT_2 | int | Text |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-f-can-taster-audio-tel"></a>
### STATUS_F_CAN_TASTER_AUDIO_TEL

Botschaft des Tasters Audio/Telefon auslesen Fuer die Zuordnung Text-Wertausgabe, siehe Tabelle AUDIO_TEL KWP2000: $22 ReadDataByCommonIdentifier $01D6 Botschaft des Tasters Audio/Telefon auslesen Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TASTER_TELEFON_TEXT | string | TEL_Status aus F_CAN Telegramm |
| STAT_TASTER_AUDIO_LAUTSTAERKE_TEXT | string | TEL_Status aus F_CAN Telegramm |
| STAT_TASTER_AUDIO_SUCHLAUF_TEXT | string | TEL_Status aus F_CAN Telegramm |
| STAT_TASTER_PUSH_TO_HEAR_TEXT | string | TEL_Status aus F_CAN Telegramm |
| STAT_TASTER_SONDERFUNKTION_TEXT | string | TEL_Status aus F_CAN Telegramm |
| STAT_TASTER_PUSH_TO_TALK_TEXT | string | TEL_Status aus F_CAN Telegramm |
| STAT_TASTER_TELEFON | int | TEL_Status aus F_CAN Telegramm |
| STAT_TASTER_AUDIO_LAUTSTAERKE | int | TEL_Status aus F_CAN Telegramm |
| STAT_TASTER_AUDIO_SUCHLAUF | int | TEL_Status aus F_CAN Telegramm |
| STAT_TASTER_PUSH_TO_HEAR | int | TEL_Status aus F_CAN Telegramm |
| STAT_TASTER_SONDERFUNKTION | int | TEL_Status aus F_CAN Telegramm |
| STAT_TASTER_PUSH_TO_TALK | int | TEL_Status aus F_CAN Telegramm |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-f-can-tempomat-acc"></a>
### STATUS_F_CAN_TEMPOMAT_ACC

Botschaft des Tempomats/ACC auslesen Fuer die Zuordnung Text-Wertausgabe, siehe Tabelle TEMP_ACC KWP2000: $22 ReadDataByCommonIdentifier $0194 - Botschaft des Tempomats/ACC auslesen Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_TASTER_TEMPOMAT_ACC_TEXT | string | ACC_Status aus F_CAN Telegramm |
| STAT_ABSTANDSWAHL_ACC_TEXT | string | ACC_Status aus F_CAN Telegramm |
| STAT_MODUS_WAHL_CC_CA_TEXT | string | ACC_Status aus F_CAN Telegramm |
| STAT_TASTER_TEMPOMAT_ACC | int | ACC_Status aus F_CAN Telegramm |
| STAT_ABSTANDSWAHL_ACC | int | ACC_Status aus F_CAN Telegramm |
| STAT_MODUS_WAHL_CC_CA | int | ACC_Status aus F_CAN Telegramm |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-f-can-wischertaster"></a>
### STATUS_F_CAN_WISCHERTASTER

Botschaft desWischertasters auslesen Fuer die Zuordnung Text-Wertausgabe, siehe Tabelle WISCHER KWP2000: $22 ReadDataByCommonIdentifier $02A6 - Botschaft des Wischertasters auslesen Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WISCHERTASTER_TEXT | string | Status_Bit aus SG Antwort |
| STAT_WISCHERTASTER | int | Status_Bit aus SG Antwort |
| STAT_WISCHERPOTI_TEXT | string | Status_Bit aus SG Antwort |
| STAT_WISCHERPOTI | int | Status_Bit aus SG Antwort |
| STAT_WISCHERTASTER_1_WERT | int | Status_Bit aus SG Antwort |
| STAT_WISCHERTASTER_2_WERT | int | Status_Bit aus SG Antwort |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-bus-loeschen"></a>
### _FS_BUS_LOESCHEN

KWP2000: $14 ClearDiagnosticInformation FFFE Fehlerspeicher loeschen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-bus-lesen"></a>
### _FS_BUS_LESEN

Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus nur fuer Bus-Fehlercodes:0xFF,0xFE Modus  : Default

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

<a id="job-ccp-mode"></a>
### _CCP_MODE

KWP2000:$31,$31 StartRoutineByLocalIdentifier service CCP Mode aktivieren wird nur im Access-Level D unterstuetzt Job nicht mehr in Serienprojekten verfuegbar

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CCP_MODE_ZUSTAND | string | P = passiv, nicht aktivieren oder A = aktivieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-tel-schreiben"></a>
### _TEL_SCHREIBEN

KWP2000 Dieser Job bietet die Moeglichkeit an, ein eigenes Telegramm zu verschicken Es muessen 2 Argumente eingegeben werden, beide mit "Strich_Punkt" getrennt (nicht mit Komma!): Erstes Argument: E oder W Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode und Telegramm-Ausfuehren: Mit dem Parameter"W" wird nur das Telegramm ausgefuehrt Zweiter Argument: Die ersten 3 Bytes des Telegramms (Format,Target,Source) sind schon vorhanden die restlichen Bytes als ein Hex_String, alle mit Komma getrennt z.B. 00,11,22,... Keine Laenge eingeben, sie wird automatisch berechnet Musterparametersatz_1: "E,00,11,22,33" Musterparametersatz_2: "W,00,11,22,33" Aufpassen: 2 Argumente (E_OR_W,T_BYTES) mit "Strich_Punkt" getrennt (nicht mit Komma !) nach dem E oder W immer "Strich_Punkt" aber folgende T_Bytes mit Komma getrennt!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E oder Wiederholung = W |
| T_BYTES | string | Bereich: 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-f-can-lw"></a>
### STATUS_F_CAN_LW

ab V10.000 wird nur noch die C9 Botschaft ausgelesen (vorher C8) Botschaft des Lenkwinkels auslesen (wird von VS benoetigt), um zwischen Lenkwinkel_Oben (LWS) und Summen_LW (AFS) zu unterscheiden Fuer die Zuordnung Text-Wert siehe Tabelle F_CAN_LW KWP2000: $22 ReadDataByCommonIdentifier $0118 Botschaft des Austausch_AFS_DSC auslesen KWP2000: $22 ReadDataByCommonIdentifier $00C9 Botschaft des Lenkradwinkel_Oben auslesen Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_LW_RAD_WERT | real | Lenkwinkel_Rad aus F_CAN Telegramm |
| STAT_LW_RAD_FEHLER_TEXT | string | Status des Signals Radlenkwinkel fuer AFS aus F_CAN Telegramm |
| STAT_LW_RAD_FEHLER_WERT | int | Status des Signals Radlenkwinkel fuer AFS aus F_CAN Telegramm |
| STAT_LW_OBEN_WERT | real | Lenkradwinkel_Oben aus F_CAN Telegramm |
| STAT_LW_OBEN_FEHLER_TEXT | string | Status des Signals Lenkradwinkel_Oben aus F_CAN Telegramm |
| STAT_LW_OBEN_FEHLER_WERT | int | Status des Signals Lenkradwinkel_Oben aus F_CAN Telegramm |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_AUFTRAG_1 | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT_1 | binary | Hex-Auftrag ans SG |

<a id="job-status-f-can-typ-sensorcluster"></a>
### STATUS_F_CAN_TYP_SENSORCLUSTER

F_CAN Botschaft CLU6 (Clustertyp: Anforderung der Werke), Unterscheidung ohne/mit redundantem Gierratensensor Fuer die Zuordnung Text-Wert siehe Tabelle F_CAN_CLUSTER KWP2000: $22 ReadDataByCommonIdentifier $0140 Botschaft CLU6 auslesen Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_CLUSTER_TYP_WERT | int | Typ des Sensorclusters |
| STAT_CLUSTER_TYP_TEXT | string | zugeordneter Wert zum Sensorclustertyp |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-fs-lesen-inpa"></a>
### _FS_LESEN_INPA

KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes KWP2000: $18 ReadDiagnosticTroubleCodesByStatus kombinierter Job §17 und §18 Fehlerspeicher lesen mit allen Umweltdaten Ausgabe der Results wie INPA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_CODE | string | Fehlercode(hex) |
| F_TEXT | string | Fehlerort als Text |
| F_ZAHL | int | Anzahl Fehler |
| F_READY_TEXT | string | 1. Fehlerart als Text table FArtTexte ARTTEXT |
| F_VORH_TEXT | string | 2. Fehlerart als Text table FArtTexte ARTTEXT |
| F_WARNUNG_TEXT | string | 3. Fehlerart als Text table FArtTexte ARTTEXT |
| F_SYMPTOM_TEXT | string | table |
| HAEUFIGKZAEHLER | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| LOGISTIKZAEHLER | int | Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| KILOMETERSTAND_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km |
| GESCHWINDIGKEIT_KMH | long | Radgeschwindigkeit vRef |
| DBC_DYNAMIC_BRAKE_CONTROL | int |  |
| DSC_PASSIV_GETASTET_ | int |  |
| ABS_ANTI_BLOCKIER_SYSTEM | int |  |
| BLS_BREMSLICHTSCHALTER | int |  |
| ASC_AUTOMATIC_STABILITY_CONTROL_AMR | int |  |
| ASC_AUTOMATIC_STABILITY_CONTROL_BMR | int |  |
| HBS_HANDBREMSSCHALTER | int |  |
| BFS_BREMSFLUESSIGKEITSSCHALTER | int |  |
| DRUCK_ERKANNT_BREMSPEDAL | int |  |
| GMR_GIERMOMENTEN_REGLER_GMR | int |  |
| GMR_GIERMOMENTEN_REGLER_MMR | int |  |
| CBC_CORNERING_BRAKE_CONTROL | int |  |
| MSR_MOTOR_SCHLEPPMOMENT_REGELUNG | int |  |
| TDR_TRAKTIONS_DIFFERENTIAL_REGELUNG | int |  |
| SDR_SCHUB_DIFFERENTIAL_REGELUNG | int |  |
| RPA_REIFEN_PANNEN_ANZEIGE | int |  |
| FEHLER_WAEHREND_RUN_UP_MODE_ERKANNT | int |  |

<a id="job-eeprom-lesen"></a>
### _EEPROM_LESEN

Lesen  EEPROM Zellen Zwei Argumente muessen eingegeben werden: die Start-Adresse und die End-Adresse. Musterparametersatz: "Start-Adresse,End-Adresse", jedoch mit "Strichpunkt" getrennt. Musterparametersatz: "224,244", jedoch mit "Strichpunkt" getrennt. Musterparametersatz: "0x00E0,0x00F4", jedoch mit "Strichpunkt" getrennt. Adressenbereich: 0x000000 - 0x0003FF KWP2000: $23 $03 ReadMemoryByAddress

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_START_ADRESSE | int | Start Adresse min 0000 hex |
| ARG_END_ADRESSE | int | End Adresse max FF hex |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| START_ADRESSE | string | Start Adresse Ausgabe |
| EEPROM_BYTES | string | EEPROM Bytes Ausgabe |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_AUFTRAG_2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |

<a id="job-status-adcr"></a>
### _STATUS_ADCR

Lesen  EEPROM Zellen Adressenbereich: 0x000000 - 0x0003FF KWP2000: $23 $03 ReadMemoryByAddress

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_ADCR_POWER | real | ADCR Wert fuer Powered-Situation |
| STAT_ADCR_BRAKE | real | ADCR Wert fuer Breaking-Situation |
| STAT_ADCR_TRAIL | real | ADCR Wert fuer Trailing-Throttle-Situation |
| STAT_ADCR_EINH | string | Einheit der Results [%] |

<a id="job-fs-lesen-selektiv"></a>
### _FS_LESEN_SELEKTIV

Fehlerspeicher lesen (Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Es muss ein Argument eingegeben werden: "DSC" oder "dsc", um DSC Fehler auszulesen "BUS" oder "bus", um BUS Fehler auszulesen "SZL" oder "szl", um SZL Fehler auszulesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLER | string | welche Fehler sollen ausgelesen werden "DSC" oder "dsc" fuer DSC Fehler "BUS" oder "bus" fuer BUS Fehler "SZL" oder "szl" fuer SZL Fehler |

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

<a id="job-bet-aktiv-1"></a>
### BET_AKTIV_1

Bandendetest aktivieren KWP2000: $31 StartRoutineByLocalIdentifier service $23 BET BET_AKTIV beinhaltet den Job DIAGNOSE_MODE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-event-counter"></a>
### STATUS_EVENT_COUNTER

KWP2000: $22,$F01x ReadDataByCommonIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FLR_EINGRIFF_ZAEHLER | long | Zaehler Eingriff Fahrleistungsreduzierung |
| STAT_FBS_SCHWELLE_1_ZAEHLER | long | Zaehler Fading Brake Support Schwelle 1 |
| STAT_FBS_SCHWELLE_2_ZAEHLER | long | Zaehler Fading Brake Support Schwelle 2 |
| STAT_DSC_OFF_KM_ZAEHLER | long | km-Zaehler DSC passiv getastet |
| STAT_SPORT_MODE_EIN_KM_ZAEHLER | long | km-Zaehler Sport Mode aktiv getastet |
| STAT_DTC_ON_KM_ZAEHLER | long | Zaehler DTC Taster EIN getastet |
| STAT_ASC_TEMP_ABSCHALTUNG_ZAEHLER | long | Zaehler ASC Temperaturabschaltungen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-laengsbeschleunigung-plausicheck-passiv"></a>
### LAENGSBESCHLEUNIGUNG_PLAUSICHECK_PASSIV

KWP2000: $31,$30 StartRoutineByLocalIdentifier service deaktiviert den Laengsbeschleunigungsplausicheck waehrend der Rollenfahrt im Prüfstand

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-event-loeschen"></a>
### STATUS_EVENT_LOESCHEN

KWP2000: $2E,$F01x WriteDataByCommonIdentifier service loescht den Event Counter Es kann max. 1 Argument uebergeben werden FLR:   loescht den Zaehler Eingriffe Fahrleistungsreduzierung FBS_1: loescht den Zaehler Fading Brake Support Schwelle 1 FBS_2: loescht den Zaehler Fading Brake Support Schwelle 2 DSC:   loescht die km-Laufleistung DSC passiv getastet SPORT: loescht die km-Laufleistung Sport Mode aktiv getastet DTC:   loescht den Zaehler DTC Taster EIN getastet ASC:   loescht den Zaehler ASC Temperaturabschaltungen Argument: z.B.: DSC

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG | string | zu loeschender Zaehler |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ident-hydraulik"></a>
### STATUS_IDENT_HYDRAULIK

Auslesen des DSC Sensor-Clusters KWP2000: $22 ReadDataByCommonIdentifier $1603 DSC Ident Hydraulik lesen Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SENSOR_VERBAUORT | string | DSC-Sensorcluster Verbauort |
| STAT_DSC_HYDRAULIK_HW_NR | string | DSC-Hydraulik Hardware Nummer |
| STAT_DSC_HYDRAULIK_SERIAL_NR | string | DSC-Hydraulik Software Nummer |
| STAT_DSC_HYDRAULIK_WERK_NR | string | DSC-Hydraulik Werk Nummer |
| STAT_DSC_HYDRAULIK_MONTAGE_LINIE_NR | string | DSC-Hydraulik Montagelinie Nummer |
| STAT_DSC_HYDRAULIK_CT_S_NR | string | DSC-Hydraulik Nummer |
| STAT_DSC_HYDRAULIK_PROD_TAG | string | DSC-Hydraulik Produktionstag |
| STAT_DSC_HYDRAULIK_PROD_JAHR | string | DSC-Hydraulik Produktionsjahr |
| STAT_DSC_HYDRAULIK_PROD_SCHICHT_NR | string | DSC-Hydraulik Schicht Nummer |
| STAT_DSC_HYDRAULIK_SERIEN_NR | string | DSC-Hydraulik Serien Nummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ident-sensorcluster"></a>
### STATUS_IDENT_SENSORCLUSTER

Auslesen des DSC Sensor-Clusters KWP2000: $22 ReadDataByCommonIdentifier $1602 DSC Sensor-Cluster  lesen Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SENSOR_VERBAUORT | string | DSC-Sensorcluster Verbauort |
| STAT_DSC_SC_HW_NR | string | DSC-Sensorcluster Hardware Nummer |
| STAT_DSC_SC_SW_NR | string | DSC-Sensorcluster Software Nummer |
| STAT_DSC_SC_CT_ID_NR | string | DSC-Sensorcluster ContiTeves ID Nummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ident-szl"></a>
### STATUS_IDENT_SZL

Auslesen der Schalt_Zentrum_Lenksäule KWP2000: $22 ReadDataByCommonIdentifier $1601 Schalt_Zentrum_Lenksäule lesen Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SENSOR_VERBAUORT | string | SZL Verbauort |
| STAT_SZL_HW_NR | string | SZL Hardware Nummer |
| STAT_SZL_SERIAL_NR | string | SZL Serial Nummer |
| STAT_SZL_TYP | string | SZL Typ: 00 ohne AFS, 01 mit AFS |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ident-sensorcluster-2"></a>
### STATUS_IDENT_SENSORCLUSTER_2

Auslesen des 2. DSC Sensor-Clusters (nur AFS) KWP2000: $22 ReadDataByCommonIdentifier $1604 DSC Sensor-Cluster  lesen Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SENSOR_VERBAUORT | string | DSC-Sensorcluster Verbauort |
| STAT_DSC_SC_HW_NR | string | DSC-Sensorcluster Hardware Nummer |
| STAT_DSC_SC_SW_NR | string | DSC-Sensorcluster Software Nummer |
| STAT_DSC_SC_CT_ID_NR | string | DSC-Sensorcluster ContiTeves ID Nummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wlc-zaehler"></a>
### STATUS_WLC_ZAEHLER

KWP2000: $21,$0A ReadDataByLocalIdentifier service Anzahl der Wandler Launch Control (WLC) Beschleunigungsvorgaenge bei Zaehlerstand 500 wird die WLC-Funktion deaktiviert es erfolgt ein Info-Eintrag in den Fehlerspeicher Wechsel der DSC Hydraulikeinheit erforderlich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_WLC_ZAEHLER | long | Zaehler Eingriff Fahrleistungsreduzierung |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-wlc-zaehler-schreiben"></a>
### WLC_ZAEHLER_SCHREIBEN

KWP2000: $3B,$0A WriteDataByLocalIdentifier service schreibt den WLC Zaehlerstand, Security Level B erforderlich Eingabe des Zaehlerstandes als Dezimalzahl Argument: z.B.: 431 kein Argument schreibt den Zaehlerstand 0xFFFF (Anlieferungszustand)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG | long | zu schreibender Zaehlerstand |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-hydro-spuelen"></a>
### STEUERN_HYDRO_SPUELEN

DSC Hydroaggregat spuelen nach der Befuellung soll Nacharbeit beim Pedalchecker reduzieren dieser Job ist nur fuer die Fertigung relevant Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-status-lesen-rpa-m5"></a>
### STATUS_LESEN_RPA_M5

KWP2000:$21,$04 ReadDataByLocalIdentifier service Alle RPA Daten auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STAT_KM_RESET | long | Umweltbedingung Kilometerstand beim letzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_WARNUNG | long | Umweltbedingung Kilometerstand beim letzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_RESET_MINUS_1 | long | Umweltbedingung Kilometerstand beim vorletzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_WARNUNG_MINUS_1 | long | Umweltbedingung Kilometerstand beim vorletzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_RESET_MINUS_2 | long | Umweltbedingung Kilometerstand beim vorvorletzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_WARNUNG_MINUS_2 | long | Umweltbedingung Kilometerstand beim vorvorletzten Reset Wertebereich: 0 - 524280 km |
| STAT_GESCHWINDIGKEITSBEREICH_1_TEXT | string | Geschwindigkeitsbereich 1 |
| STAT_GESCHWINDIGKEITSBEREICH_2_TEXT | string | Geschwindigkeitsbereich 2 |
| STAT_GESCHWINDIGKEITSBEREICH_3_TEXT | string | Geschwindigkeitsbereich 3 |
| STAT_GESCHWINDIGKEITSBEREICH_4_TEXT | string | Geschwindigkeitsbereich 4 |
| STAT_GESCHWINDIGKEITSBEREICH_5_TEXT | string | Geschwindigkeitsbereich 5 |
| STAT_GESCHWINDIGKEITSBEREICH_6_TEXT | string | Geschwindigkeitsbereich 6 |
| STAT_DRUCKSCHWELLE_GROB_1 | int | Lernbereich Druckschwelle grob 3 |
| STAT_DRUCKSCHWELLE_GROB_2 | int | Lernbereich Druckschwelle grob 4 |
| STAT_DRUCKSCHWELLE_GROB_3 | int | Lernbereich Druckschwelle grob 3 |
| STAT_DRUCKSCHWELLE_GROB_4 | int | Lernbereich Druckschwelle grob 4 |
| STAT_DRUCKSCHWELLE_GROB_5 | int | Lernbereich Druckschwelle grob 5 |
| STAT_DRUCKSCHWELLE_GROB_6 | int | Lernbereich Druckschwelle grob 6 |
| STAT_DRUCKSCHWELLE_FEIN_1 | int | Lernbereich Druckschwelle fein 3 |
| STAT_DRUCKSCHWELLE_FEIN_2 | int | Lernbereich Druckschwelle fein 4 |
| STAT_DRUCKSCHWELLE_FEIN_3 | int | Lernbereich Druckschwelle fein 3 |
| STAT_DRUCKSCHWELLE_FEIN_4 | int | Lernbereich Druckschwelle fein 4 |
| STAT_DRUCKSCHWELLE_FEIN_5 | int | Lernbereich Druckschwelle fein 5 |
| STAT_DRUCKSCHWELLE_FEIN_6 | int | Lernbereich Druckschwelle fein 6 |
| STAT_ACHSE_LERN_IM_BEREICH_0_50_NM | int | Momentenkompensation 1 |
| STAT_ACHSE_LERN_IM_BEREICH_50_100_NM | int | Momentenkompensation 2 |
| STAT_ACHSE_LERN_IM_BEREICH_100_150_NM | int | Momentenkompensation 3 |
| STAT_ACHSE_LERN_IM_BEREICH_150_200_NM | int | Momentenkompensation 4 |
| STAT_ACHSE_LERN_IM_BEREICH_200_250_NM | int | Momentenkompensation 5 |
| STAT_ACHSE_LERN_IM_BEREICH_250_300_NM | int | Momentenkompensation 6 |
| STAT_ACHSE_LERN_SCHNELL_IM_BEREICH_0_50_NM | int | Momentenkompensation 1 |
| STAT_ACHSE_LERN_SCHNELL_IM_BEREICH_50_100_NM | int | Momentenkompensation 2 |
| STAT_ACHSE_LERN_SCHNELL_IM_BEREICH_100_150_NM | int | Momentenkompensation 3 |
| STAT_ACHSE_LERN_SCHNELL_IM_BEREICH_150_200_NM | int | Momentenkompensation 4 |
| STAT_KURVENKOMPENSATION_1 | int | Kurvenkompensation 1 |
| STAT_KURVENKOMPENSATION_2 | int | Kurvenkompensation 2 |
| STAT_KURVENKOMPENSATION_3 | int | Kurvenkompensation 3 |
| STAT_KURVENKOMPENSATION_4 | int | Kurvenkompensation 4 |
| STAT_KURVENKOMPENSATION_5 | int | Kurvenkompensation 5 |
| STAT_KURVENKOMPENSATION_6 | int | Kurvenkompensation 6 |
| STAT_KURVENKOMPENSATION_7 | int | Kurvenkompensation 7 |
| STAT_KURVENKOMPENSATION_8 | int | Kurvenkompensation 8 |
| STAT_KURVENKOMPENSATION_1_TEXT | string | Text zur Kurvenkompensation 1 |
| STAT_KURVENKOMPENSATION_2_TEXT | string | Text zur Kurvenkompensation 2 |
| STAT_KURVENKOMPENSATION_3_TEXT | string | Text zur Kurvenkompensation 3 |
| STAT_KURVENKOMPENSATION_4_TEXT | string | Text zur Kurvenkompensation 4 |
| STAT_KURVENKOMPENSATION_5_TEXT | string | Text zur Kurvenkompensation 5 |
| STAT_KURVENKOMPENSATION_6_TEXT | string | Text zur Kurvenkompensation 6 |
| STAT_KURVENKOMPENSATION_7_TEXT | string | Text zur Kurvenkompensation 7 |
| STAT_KURVENKOMPENSATION_8_TEXT | string | Text zur Kurvenkompensation 8 |
| STAT_WARNUNG_AKTUELL | int | Anzahl aktueller Warnungen |
| STAT_WARN_HISTORY_1 | int | Warnvorgeschichte 1 |
| STAT_WARN_HISTORY_2 | int | Warnvorgeschichte 2 |
| STAT_WARN_HISTORY_3 | int | Warnvorgeschichte 3 |
| STAT_WARN_HISTORY_4 | int | Warnvorgeschichte 4 |
| STAT_WARN_HISTORY_5 | int | Warnvorgeschichte 5 |
| STAT_WARN_HISTORY_6 | int | Warnvorgeschichte 6 |
| STAT_WARN_HISTORY_7 | int | Warnvorgeschichte 7 |
| STAT_WARN_HISTORY_8 | int | Warnvorgeschichte 8 |
| STAT_WARN_GRUND_1 | int | Warngrund 1 |
| STAT_WARN_GRUND_2 | int | Warngrund 2 |
| STAT_WARN_GRUND_3 | int | Warngrund 3 |
| STAT_WARN_GRUND_4 | int | Warngrund 4 |
| STAT_WARN_GRUND_5 | int | Warngrund 5 |
| STAT_WARN_GRUND_6 | int | Warngrund 6 |
| STAT_WARN_GRUND_7 | int | Warngrund 7 |
| STAT_WARN_GRUND_8 | int | Warngrund 8 |
| STAT_WARN_TEXT_1 | string | Warntext 1 |
| STAT_WARN_TEXT_2 | string | Warntext 2 |
| STAT_WARN_TEXT_3 | string | Warntext 3 |
| STAT_WARN_TEXT_4 | string | Warntext 4 |
| STAT_WARN_TEXT_5 | string | Warntext 5 |
| STAT_WARN_TEXT_6 | string | Warntext 6 |
| STAT_WARN_TEXT_7 | string | Warntext 7 |
| STAT_WARN_TEXT_8 | string | Warntext 8 |
| STAT_FUNKTIONSTEST | int | Funktionstest abgeschlossen nein/ja [0/1] |
| STAT_ACHSE_LERN_SCHNELL_BEENDET | int | Einlernvorgang Achse beendet nein/ja [0/1] |
| STAT_DELTA_PANNEN_SCHWELLWERT | int | Pannen-Schwellwert |
| STAT_DELTA_PANNEN_SCHWELLWERT_EINH | string | Einheit Pannen-Schwellwert |
| STAT_PANNEN_ZAEHLER | int | Pannenzaehler |
| STAT_L1 | int | Lernstati 1 |
| STAT_L1_EINH | string | Einheit Lernstati 1 [%] |
| STAT_L2 | int | Lernstati 2 |
| STAT_L2_EINH | string | Einheit Lernstati 2 [%] |
| STAT_L3 | int | Lernstati 3 |
| STAT_L3_EINH | string | Einheit Lernstati 3 [%] |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |

<a id="job-status-lesen-rpa-m3"></a>
### _STATUS_LESEN_RPA_M3

KWP2000:$21,$0B ReadDataByLocalIdentifier service Alle RPA Daten auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| STAT_KM_RESET | long | Umweltbedingung Kilometerstand beim letzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_WARNUNG | long | Umweltbedingung Kilometerstand beim letzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_RESET_MINUS_1 | long | Umweltbedingung Kilometerstand beim vorletzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_WARNUNG_MINUS_1 | long | Umweltbedingung Kilometerstand beim vorletzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_RESET_MINUS_2 | long | Umweltbedingung Kilometerstand beim vorvorletzten Reset Wertebereich: 0 - 524280 km |
| STAT_KM_WARNUNG_MINUS_2 | long | Umweltbedingung Kilometerstand beim vorvorletzten Reset Wertebereich: 0 - 524280 km |
| STAT_GESCHWINDIGKEITSBEREICH_1_TEXT | string | Geschwindigkeitsbereich 1 |
| STAT_GESCHWINDIGKEITSBEREICH_2_TEXT | string | Geschwindigkeitsbereich 2 |
| STAT_GESCHWINDIGKEITSBEREICH_3_TEXT | string | Geschwindigkeitsbereich 3 |
| STAT_GESCHWINDIGKEITSBEREICH_4_TEXT | string | Geschwindigkeitsbereich 4 |
| STAT_GESCHWINDIGKEITSBEREICH_5_TEXT | string | Geschwindigkeitsbereich 5 |
| STAT_GESCHWINDIGKEITSBEREICH_6_TEXT | string | Geschwindigkeitsbereich 6 |
| STAT_DRUCKSCHWELLE_GROB_1 | int | Lernbereich Druckschwelle grob 3 |
| STAT_DRUCKSCHWELLE_GROB_2 | int | Lernbereich Druckschwelle grob 4 |
| STAT_DRUCKSCHWELLE_GROB_3 | int | Lernbereich Druckschwelle grob 3 |
| STAT_DRUCKSCHWELLE_GROB_4 | int | Lernbereich Druckschwelle grob 4 |
| STAT_DRUCKSCHWELLE_GROB_5 | int | Lernbereich Druckschwelle grob 5 |
| STAT_DRUCKSCHWELLE_GROB_6 | int | Lernbereich Druckschwelle grob 6 |
| STAT_DRUCKSCHWELLE_FEIN_1 | int | Lernbereich Druckschwelle fein 3 |
| STAT_DRUCKSCHWELLE_FEIN_2 | int | Lernbereich Druckschwelle fein 4 |
| STAT_DRUCKSCHWELLE_FEIN_3 | int | Lernbereich Druckschwelle fein 3 |
| STAT_DRUCKSCHWELLE_FEIN_4 | int | Lernbereich Druckschwelle fein 4 |
| STAT_DRUCKSCHWELLE_FEIN_5 | int | Lernbereich Druckschwelle fein 5 |
| STAT_DRUCKSCHWELLE_FEIN_6 | int | Lernbereich Druckschwelle fein 6 |
| STAT_ACHSE_LERN_IM_BEREICH_0_50_NM | int | Momentenkompensation 1 |
| STAT_ACHSE_LERN_IM_BEREICH_50_100_NM | int | Momentenkompensation 2 |
| STAT_ACHSE_LERN_IM_BEREICH_100_150_NM | int | Momentenkompensation 3 |
| STAT_ACHSE_LERN_IM_BEREICH_150_200_NM | int | Momentenkompensation 4 |
| STAT_ACHSE_LERN_IM_BEREICH_200_250_NM | int | Momentenkompensation 5 |
| STAT_ACHSE_LERN_IM_BEREICH_250_300_NM | int | Momentenkompensation 6 |
| STAT_ACHSE_LERN_SCHNELL_IM_BEREICH_0_50_NM | int | Momentenkompensation 1 |
| STAT_ACHSE_LERN_SCHNELL_IM_BEREICH_50_100_NM | int | Momentenkompensation 2 |
| STAT_ACHSE_LERN_SCHNELL_IM_BEREICH_100_150_NM | int | Momentenkompensation 3 |
| STAT_ACHSE_LERN_SCHNELL_IM_BEREICH_150_200_NM | int | Momentenkompensation 4 |
| STAT_KURVENKOMPENSATION_1 | int | Kurvenkompensation 1 |
| STAT_KURVENKOMPENSATION_2 | int | Kurvenkompensation 2 |
| STAT_KURVENKOMPENSATION_3 | int | Kurvenkompensation 3 |
| STAT_KURVENKOMPENSATION_4 | int | Kurvenkompensation 4 |
| STAT_KURVENKOMPENSATION_5 | int | Kurvenkompensation 5 |
| STAT_KURVENKOMPENSATION_6 | int | Kurvenkompensation 6 |
| STAT_KURVENKOMPENSATION_7 | int | Kurvenkompensation 7 |
| STAT_KURVENKOMPENSATION_8 | int | Kurvenkompensation 8 |
| STAT_KURVENKOMPENSATION_1_TEXT | string | Text zur Kurvenkompensation 1 |
| STAT_KURVENKOMPENSATION_2_TEXT | string | Text zur Kurvenkompensation 2 |
| STAT_KURVENKOMPENSATION_3_TEXT | string | Text zur Kurvenkompensation 3 |
| STAT_KURVENKOMPENSATION_4_TEXT | string | Text zur Kurvenkompensation 4 |
| STAT_KURVENKOMPENSATION_5_TEXT | string | Text zur Kurvenkompensation 5 |
| STAT_KURVENKOMPENSATION_6_TEXT | string | Text zur Kurvenkompensation 6 |
| STAT_KURVENKOMPENSATION_7_TEXT | string | Text zur Kurvenkompensation 7 |
| STAT_KURVENKOMPENSATION_8_TEXT | string | Text zur Kurvenkompensation 8 |
| STAT_WARNUNG_AKTUELL | int | Anzahl aktueller Warnungen |
| STAT_FUNKTIONSTEST | int | Funktionstest abgeschlossen nein/ja [0/1] |
| STAT_ACHSE_LERN_SCHNELL_BEENDET | int | Einlernvorgang Achse beendet nein/ja [0/1] |
| STAT_DELTA_PANNEN_SCHWELLWERT | int | Pannen-Schwellwert |
| STAT_DELTA_PANNEN_SCHWELLWERT_EINH | string | Einheit Pannen-Schwellwert |
| STAT_PANNEN_ZAEHLER | int | Pannenzaehler |
| STAT_L1 | int | Lernstati 1 |
| STAT_L1_EINH | string | Einheit Lernstati 1 [%] |
| STAT_L2 | int | Lernstati 2 |
| STAT_L2_EINH | string | Einheit Lernstati 2 [%] |
| STAT_L3 | int | Lernstati 3 |
| STAT_L3_EINH | string | Einheit Lernstati 3 [%] |
| STAT_TOM_LERN_VL_1 | string | TOM Lernstatus VL Schwellewert 1 |
| STAT_TOM_LERN_VL_2 | string | TOM Lernstatus VL Schwellewert 2 |
| STAT_TOM_LERN_VR_1 | string | TOM Lernstatus VR Schwellewert 1 |
| STAT_TOM_LERN_VR_2 | string | TOM Lernstatus VR Schwellewert 2 |
| STAT_TOM_LERN_HL_1 | string | TOM Lernstatus HL Schwellewert 1 |
| STAT_TOM_LERN_HL_2 | string | TOM Lernstatus HL Schwellewert 2 |
| STAT_TOM_LERN_HR_1 | string | TOM Lernstatus HR Schwellewert 1 |
| STAT_TOM_LERN_HR_2 | string | TOM Lernstatus HR Schwellewert 2 |
| STAT_WARN_HISTORY | int | Warnhistory 1 |
| STAT_WARN_HISTORY_LOW_BYTE | int | Warnhistory 2 |
| STAT_WARN_GRUND | int | Warngrund 1 |
| STAT_WARN_GRUND_LOW_BYTE | int | Warngrund 2 |
| STAT_WARNUNG_RAD_POSITION | int | Warnung Radposition (bei DDS+ =0) |
| STAT_SCHWELLWERT_DIFFERENZ_VL | int | Schwellwertdifferenz VL |
| STAT_SCHWELLWERT_DIFFERENZ_VR | int | Schwellwertdifferenz VR |
| STAT_SCHWELLWERT_DIFFERENZ_HL | int | Schwellwertdifferenz HL |
| STAT_SCHWELLWERT_DIFFERENZ_HR | int | Schwellwertdifferenz HR |
| STAT_PANNEN_ZAEHLER_DDS | int | Pannenzaehler fuer DDS Systeme |
| STAT_SCHWELLWERT_DIFFERENZ_4_REIFEN | int | Schwellwertdifferenz fuer 4 Reifen Druckverlustsysteme |
| STAT_PANNEN_ZAEHLER_4_REIFEN | int | Pannenzaehler fuer 4 Reifen Druckverlustsysteme |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-pre-ventil-kalibrierung"></a>
### PRE_VENTIL_KALIBRIERUNG

Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, FEHLER |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (125 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (133 × 3)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [CBSKENNUNG](#table-cbskennung) (20 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (234 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (17 × 9)
- [FARTTYP](#table-farttyp) (39 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (15 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [DIGITAL1](#table-digital1) (1 × 5)
- [DIGITAL2](#table-digital2) (1 × 13)
- [STEUERN](#table-steuern) (14 × 3)
- [AUDIO_TEL](#table-audio-tel) (12 × 9)
- [TEMP_ACC](#table-temp-acc) (12 × 5)
- [WISCHER](#table-wischer) (12 × 4)
- [RAD](#table-rad) (5 × 4)
- [CBS_BBV](#table-cbs-bbv) (5 × 3)
- [SENSOR_CLUSTER](#table-sensor-cluster) (5 × 3)
- [ABGLEICH_V_ERGEBNIS](#table-abgleich-v-ergebnis) (17 × 3)
- [ABGLEICH_LWS_ERGEBNIS](#table-abgleich-lws-ergebnis) (3 × 3)
- [F_CAN_LW](#table-f-can-lw) (5 × 4)
- [CODIERUNG](#table-codierung) (20 × 5)
- [RPA](#table-rpa) (16 × 7)

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

Dimensions: 125 rows × 2 columns

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

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 133 rows × 3 columns

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
| 0x4C00 | Klimabedienteil | 1 |
| 0x4D00 | Gebläseregler | 1 |
| 0x4E00 | Klappenmotor | 0 |
| 0x4F00 | Elektrischer Kältemittelverdichter eKMV | 1 |
| 0x4F80 | Elektrischer Zuheizer PTC | 1 |
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
| 0xFFFF | unbekannter Verbauort | - |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

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
| - | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 234 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5D8E | 5D8E - falscher Sensorcluster. |
| 0x5D8F | 5D8F - Sensorcluster Fehler intern. |
| 0x5D97 | 5D97 - Sensorcluster Versorgungsspannung ausserhalb gueltigem Bereich. |
| 0x5D9A | 5D9A - Drucksensor vorne links elektrisch defekt. |
| 0x5D9B | 5D9B - Drucksensor vorne links Plausibilitaet. |
| 0x5D9C | 5D9C - Drucksensor vorne links Vorderachse Plausibilitaet. |
| 0x5D9D | 5D9D - Drucksensor vorne links hydraulische Leckage Vorderachse |
| 0x5D9E | 5D9E - Drucksensor vorne links p1 Gradient Fehler. |
| 0x5D9F | 5D9F - Drucksensor vorne links Plausibilitaet Feinabstimmungsfehler. |
| 0x5DA7 | 5DA7 - hydraulische Leckage Vorderachse oder Hinterachse |
| 0x5DAA | 5DAA - Drucksensor vorne rechts elektrisch defekt. |
| 0x5DAB | 5DAB - Drucksensor vorne rechts Plausibilitaet. |
| 0x5DAC | 5DAC - Drucksensor vorne rechts Vorderachse Plausibilitaet. |
| 0x5DAD | 5DAD - Drucksensor vorne rechts hydraulische Leckage Vorderachse |
| 0x5DAE | 5DAE - Drucksensor vorne rechts p1 Gradient Fehler. |
| 0x5DAF | 5DAF - Drucksensor vorne rechts Plausibilitaet Feinabstimmungsfehler. |
| 0x5DBA | 5DBA - Drucksensor hinten links elektrisch defekt. |
| 0x5DBB | 5DBB - Drucksensor hinten links Plausibilitaet. |
| 0x5DBC | 5DBC - Drucksensor hinten links Hinterachse Plausibilitaet. |
| 0x5DBD | 5DBD - Drucksensor hinten links hydraulische Leckage Hinterachse |
| 0x5DBE | 5DBE - Drucksensor hinten links p1 Gradient Fehler. |
| 0x5DBF | 5DBF - Drucksensor hinten links Plausibilitaet Feinabstimmungsfehler. |
| 0x5DCA | 5DCA - Drucksensor hinten rechts elektrisch defekt. |
| 0x5DCB | 5DCB - Drucksensor hinten rechts Plausibilitaet. |
| 0x5DCC | 5DCC - Drucksensor hinten rechts Hinterachse Plausibilitaet. |
| 0x5DCD | 5DCD - Drucksensor hinten rechts hydraulische Leckage Hinterachse |
| 0x5DCE | 5DCE - Drucksensor hinten rechts p1 Gradient Fehler. |
| 0x5DCF | 5DCF - Drucksensor hinten rechts Plausibilitaet Feinabstimmungsfehler. |
| 0x5DD0 | 5DD0 - Ventil Abgleich Daten fehlen. |
| 0x5DD1 | 5DD1 - RPA EEPROM Checksumme-Fehler. |
| 0x5DD2 | 5DD2 - Einlassventil Abgleichdaten fehlen. |
| 0x5DD3 | 5DD3 - ECU intern: ECU-Betriebssystem (OSEC) erkennt ECU-internen Fehler |
| 0x5D90 | 5D90 - Drehzahlfuehler vorne links elektrisch defekt. |
| 0x5D91 | 5D91 - Drehzahlfuehler vorne links Extrapolation. |
| 0x5D92 | 5D92 - Drehzahlfuehler Impulsrad vorne links periodische Ueberwachung. |
| 0x5D93 | 5D93 - Drehzahlfuehler vorne links Anfahrerkennung v_Vergleich. |
| 0x5D94 | 5D94 - Drehzahlfuehler vorne links Langzeitueberwachung. |
| 0x5D95 | 5D95 - Drehzahlfuehler vorne links Check auf doppelte Impulsradfrequenz. |
| 0x5D96 | 5D96 - Drehrichtungserkennung vorne links. |
| 0x5DA0 | 5DA0 - Drehzahlfuehler vorne rechts elektrisch defekt. |
| 0x5DA1 | 5DA1 - Drehzahlfuehler vorne rechts Extrapolation. |
| 0x5DA2 | 5DA2 - Drehzahlfuehler Impulsrad vorne rechts periodische Ueberwachung. |
| 0x5DA3 | 5DA3 - Drehzahlfuehler vorne rechts Anfahrerkennung v_Vergleich. |
| 0x5DA4 | 5DA4 - Drehzahlfuehler vorne rechts Langzeitueberwachung. |
| 0x5DA5 | 5DA5 - Drehzahlfuehler vorne rechts Check auf doppelte Impulsradfrequenz. |
| 0x5DA6 | 5DA6 - Drehrichtungserkennung vorne rechts. |
| 0x5DB0 | 5DB0 - Drehzahlfuehler hinten links elektrisch defekt. |
| 0x5DB1 | 5DB1 - Drehzahlfuehler hinten links Extrapolation. |
| 0x5DB2 | 5DB2 - Drehzahlfuehler Impulsrad hinten links periodische Ueberwachung. |
| 0x5DB3 | 5DB3 - Drehzahlfuehler hinten links Anfahrerkennung v_Vergleich. |
| 0x5DB4 | 5DB4 - Drehzahlfuehler hinten links Langzeitueberwachung. |
| 0x5DB5 | 5DB5 - Drehzahlfuehler hinten links Check auf doppelte Impulsradfrequenz. |
| 0x5DB6 | 5DB6 - Drehrichtungserkennung hinten links. |
| 0x5DC0 | 5DC0 - Drehzahlfuehler hinten rechts elektrisch defekt. |
| 0x5DC1 | 5DC1 - Drehzahlfuehler hinten rechts Extrapolation. |
| 0x5DC2 | 5DC2 - Drehzahlfuehler Impulsrad hinten rechts periodische Ueberwachung. |
| 0x5DC3 | 5DC3 - Drehzahlfuehler hinten rechts Anfahrerkennung v_Vergleich. |
| 0x5DC4 | 5DC4 - Drehzahlfuehler hinten rechts Langzeitueberwachung. |
| 0x5DC5 | 5DC5 - Drehzahlfuehler hinten rechts Check auf doppelte Impulsradfrequenz. |
| 0x5DC6 | 5DC6 - Drehrichtungserkennung hinten rechts. |
| 0x5DF0 | 5DF0 - Pumpenmotor defekt. |
| 0x5DF1 | 5DF1 - Pumpenmotor Stecker defekt. |
| 0x5DF2 | 5DF2 - Ventil/ECU_Hardware Fehler,ROM/RAM_Check Fehler. |
| 0x5DF4 | 5DF4 - Bordnetzspannung &lt; 9 Volt. |
| 0x5DF5 | 5DF5 - Steuergeraet Fehler intern. |
| 0x5DF7 | 5DF7 - Bordnetzspannung &gt; 18 Volt. |
| 0x5DFF | 5DFF - Pumpenmotor max.Drehzahl ueberschritten. |
| 0x5E00 | 5E00 - Bandendetest aktiv. |
| 0x5E01 | 5E01 - Bandendetest Timeout. |
| 0x5E02 | 5E02 - Bandendetest Gierratensensor Justierung Fehler. |
| 0x5E03 | 5E03 - Bandendetest Gierratensensor Fehler. |
| 0x5E04 | 5E04 - Bandendetest Querbeschleunigungssensor Fehler. |
| 0x5E05 | 5E05 - Bandendetest Querbeschleunigung und Gierraten Fehler: vertauscht. |
| 0x5E06 | 5E06 - Bandendetest Gierratensensor falsch montiert. |
| 0x5E07 | 5E07 - Bandendetest Querbeschleunigungssensor falsch montiert. |
| 0x5E08 | 5E08 - Bandendetest Lenkwinkelsensor Fehler. |
| 0x5E09 | 5E09 - Bandendetest Bremslichtschalter Fehler. |
| 0xF14A | F14A - Bandendetest Bremslichtschalter Fehler. |
| 0x5E18 | 5E18 - CAN DME/DDE Botschaft unplausibel. |
| 0x5E19 | 5E19 - CAN DME/DDE, Motormoment nicht einstellbar. |
| 0x5E1A | 5E1A - CAN DME/DDE Signal Fehler. |
| 0x5E1B | 5E1B - CAN DME/DDE Motormoment Signal Fehler. |
| 0x5E1C | 5E1C - PT-CAN HSA Signal Fehler. |
| 0x5E1D | 5E1D - PT-CAN Fahrgestellnummer ungueltig. |
| 0x5E1F | 5E1F - PT-CAN Fahrgestellnummer falsch / ECU nicht initialisiert. |
| 0x5E3F | 5E3F - F-CAN SZL Codierfehler. |
| 0xD347 | D347 - PT-CAN-Bus Off. |
| 0xD34B | D34B - F-CAN-Bus Off. |
| 0xD354 | D354 - PT-CAN DME/DDE_1 - Drehmoment 1 Botschaft 168 fehlt |
| 0xD355 | D355 - PT-CAN DME/DDE_2 - Drehmoment 2 Botschaft 169 fehlt |
| 0xD356 | D356 - PT-CAN DME/DDE_3 - Drehmoment 3 Botschaft 170 fehlt |
| 0xD357 | D357 - PT-CAN Getriebe 1 - Getriebedaten Botschaft 186 fehlt |
| 0xD358 | D358 - PT-CAN Instrumentcluster_1 - Aussentemperatur/Relativzeit Botschaft 784 fehlt |
| 0xD359 | D359 - PT-CAN Instrumentcluster_2 - Kilometerstand Botschaft 816 fehlt |
| 0xD35A | D35A - PT-CAN Gateway_1 - Klemmenstatus Botschaft 304 fehlt |
| 0xD35B | D35B - PT-CAN LDM-Fehler - Botschaft 213: Anforderung Radmoment Bremse, ANF_RADMOM_BREMSE (ID 0xD5) |
| 0xD35C | D35C - PT-CAN ACC_2. |
| 0xD35D | D35D - PT-CAN ACC Langzeit Timeout Botschaft 419 fehlt |
| 0xD360 | D360 - PT-CAN Motronic_4 Plausibilitaet |
| 0xD361 | D361 - PT-CAN Fahrgestellnummer Timeout Botschaft 896 fehlt |
| 0xD362 | D362 - PT-CAN Motronic_5 |
| 0xD363 | D363 - PT-CAN Instrument_cluster_3 |
| 0xD364 | D364 - PT-CAN Operator_Key_Tempo |
| 0xD370 | D370 - F-CAN Sensorcluster_1 Botschaft 205 fehlt |
| 0xD371 | D371 - F-CAN Sensorcluster_2 Botschaft 209 fehlt |
| 0xD372 | D372 - F-CAN Sensorcluster_3 Botschaft 212 fehlt |
| 0xD373 | D373 - F-CAN SWA-Top-Sensor Botschaft 200 oder 201 fehlt |
| 0xD374 | D374 - F-CAN SWA-Raw-Sensor Botschaft 195 fehlt |
| 0xD375 | D375 - F-CAN AFS - Austausch AFS-DSC Botschaft 118 fehlt |
| 0xD376 | D376 - F-CAN AFS Botschaft 11F fehlt |
| 0xD377 | D377 - PT_CAN_Timeout Botschaft 740 (Status_Anhaenger)  fehlt |
| 0xD378 | D378 - PT_CAN_Timeout Botschaft 944  (Status_Gang_Rueckwaerts) fehlt |
| 0x5E50 | 5E50 - F-CAN SZL Seriennummer falsch. |
| 0x5E51 | 5E51 - F-CAN SZL Seriennummer ungueltig. |
| 0x5E52 | 5E52 - AFS Aktuator Signal unplausibel. |
| 0x5E53 | 5E53 - GMK gesperrt durch AFS. |
| 0x5E54 | 5E54 - GMK gesperrt wegen dauernder GMK-Regelung. |
| 0xC987 | C987 - F-CAN SZL keine Botschaften Bus-Off. |
| 0xC994 | C994 - F-CAN SZL Radgeschwindigkeit, Kommunikation mit DSC, Timeout (Nachricht in applizierbarer Zeit nicht empfangen) |
| 0xC995 | C995 - F-CAN SZL Radgeschwindigkeit Plausibilitaet, Kommunikation mit DSC, Radgeschwindigkeit &gt;300km/h |
| 0xC996 | C996 - F-CAN SZL Radgeschwindigkeit Plausibilitaet, Kommunikation mit DSC, Radgeschwindigkeit &lt;300km/h |
| 0xC997 | C997 - F-CAN SZL Radtoleranzabgleich, Kommunikation mit DSC, Timeout (Nachricht in applizierbarer Zeit nicht empfangen) |
| 0xC998 | C998 - F-CAN SZL Radtoleranzabgleich Plausibilitaet, Kommunikation mit DSC, Radtoleranzabgleich &lt; -5% |
| 0xC99A | C99A - F-CAN SZL Radtoleranzabgleich Plausibilitaet, Kommunikation mit DSC, Radtoleranzabgleich &gt; 5% |
| 0xC99B | C99B - F-CAN SZL Sync, keine Kommunikation mit DSC, Timeout. |
| 0xC99C | C99C - F-CAN SZL, Klemmenstatus, keine Kommunikation mit DSC, Timeout. |
| 0x5E20 | 5E20 - Drucksensor 1 elektrisch defekt. |
| 0x5E24 | 5E24 - Drucksensor 1 unplausibel. |
| 0x5E25 | 5E25 - Drucksensor 1 unplausibel Feinabstimmungsfehler. |
| 0x5E26 | 5E26 - Spannungsversorgung Sensoren. |
| 0x5E28 | 5E28 - LDM-Fehler: Fahrpedal ueberwachung, LDM-Bremsanforderung gegenueber Fahrpedal unplausibel |
| 0x5E29 | 5E29 - LDM-Fehler: Freigabe ueberwachung, LDM-Bremsanforderung ohne Freigabe |
| 0x5E2A | 5E2A - Ueberbremserkennung durch DCC Abbremsvorgang |
| 0x5E2B | 5E2B - Unterbremserkennung durch DCC Abbremsvorgang |
| 0x5E2C | 5E2C - hydraulische Leckage Vorderachse |
| 0x5E2D | 5E2D - DSC Differenzdruckueberwachung VA/HA zulaessiger Differenzdruck ueberschritten |
| 0x5E2E | 5E2E - Schalter Rueckwaertsgang Plausibilitaet. |
| 0x5E2F | 5E2F - Temperatur Sensor. |
| 0x5E30 | 5E30 - Querbeschleunigungssensor Signal ausserhalb gueltigem Bereich oder elektrisch defekt. |
| 0x5E31 | 5E31 - Querbeschleunigungssensor Offset Fehler. |
| 0x5E32 | 5E32 - Querbeschleunigungssensor unplausibel. |
| 0x5E33 | 5E33 - Querbeschleunigungssensor Offset Fehler. |
| 0x5E34 | 5E34 - Laengsbeschleunigungssensor Signal ausserhalb gueltigem Bereich oder elektrisch defekt. |
| 0x5E35 | 5E35 - Laengsbeschleunigungssensor unplausibel. |
| 0x5E36 | 5E36 - Laengsbeschleunigungssensor Offset Fehler. |
| 0x5E37 | 5E37 - Laengsbeschleunigungssensor Fehler beim Selbsttest. |
| 0x5E38 | 5E38 - Gierratensensor Signal ausserhalb gueltigem Bereich oder elektrisch defekt. |
| 0x5E39 | 5E39 - Gierratensensor Offset Fehler. |
| 0x5E3A | 5E3A - Gierratensensor Offset Fehler Stillstand. |
| 0x5E3B | 5E3B - Gierratensensor Offset Fehler CBit. |
| 0x5E3C | 5E3C - Gierratensensor unplausibel. |
| 0x5E3D | 5E3D - Querbeschleunigungssensor Fehler beim Selbsttest. |
| 0x5E40 | 5E40 - Lenkwinkelsensor Signal unplausibel,Offset. |
| 0x5E43 | 5E43 - Lenkwinkelsensor intern. |
| 0x5E46 | 5E46 - Lenkwinkelsensor Signal, Offset Fehler |
| 0x5E47 | 5E47 - Lenkwinkelsensor Fehler Klemmen Status |
| 0x5E48 | 5E48 - Lenkwinkelsensor Signal Fehler Toleranz Check |
| 0x5E49 | 5E49 - Lenkwinkelsensor Initialisierungs Fehler |
| 0x5E4E | 5E4E - DSC Sensor Offset Check. |
| 0x5E4F | 5E4F - DSC Dauerregelung. |
| 0x5E58 | 5E58 - ASC ECU im falschen Fahrzeug. |
| 0x5E59 | 5E59 - Codierfehler. |
| 0x5E5B | 5E5B - DSC Taster laenger als 10sec gedrueckt oder Fehler. |
| 0x5E5C | 5E5C - RPA Taster Fehler. |
| 0x5E5D | 5E5D - Bremsfluessigkeitsniveau niedrig / Schalter defekt. |
| 0x5E5E | 5E5E - Bremslichtschalter Fehler, Plausibilitaets Fehler. |
| 0x5E60 | 5E60 - PT-CAN Engine4 Signal Fehler |
| 0x5E61 | 5E61 - PT-CAN Engine5 Signal Fehler |
| 0x5E62 | 5E62 - PT-CAN Gear1 Signal Fehler |
| 0x5E63 | 5E63 - PT-CAN Instr_Cluster3 Signal Fehler |
| 0x5E64 | 5E64 - PT-CAN Instr_Cluster3 Plausibilitaets Fehler_1 |
| 0x5E65 | 5E65 - PT-CAN Instr_Cluster3 Plausibilitaets Fehler_2 |
| 0x5E66 | 5E66 - F-CAN Engine4 Signal Fehler |
| 0x5E67 | 5E67 - PT-CAN DCC Signal Fehler_1 |
| 0x5E68 | 5E68 - PT-CAN DCC Signal Fehler_2 |
| 0x5DE0 | 5DE0 - Bremsbelagverschleiss VA nicht/falsch initialisiert. |
| 0x5DE1 | 5DE1 - Bremsbelagverschleiss HA nicht/falsch initialisiert. |
| 0x5DE2 | 5DE2 - Bremsbelagverschleiss VA kritische Belagdicke erreicht. |
| 0x5DE3 | 5DE3 - Bremsbelagverschleiss HA kritische Belagdicke erreicht. |
| 0x94B0 | 94B0 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - Synchronisation mit Sub nicht moeglich. |
| 0x94B1 | 94B1 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - Verbindungstest zur PDA fehlgeschlagen. |
| 0x94B2 | 94B2 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - Umgebungshelligkeit zu hoch. |
| 0x94B3 | 94B3 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - keine Referenzspur gefunden. |
| 0x94B4 | 94B4 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - Referenzspurabstand ausserhalb des Toleranzbandes |
| 0x94B5 | 94B5 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - Illegaler Code. |
| 0x94B6 | 94B6 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - Winkelsprung zu gross. |
| 0x94B7 | 94B7 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - Lenkwinkel-Messbereich ueberschritten (Rundenoverflow) |
| 0x94B8 | 94B8 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - Winkelverifizierung durch Main und Sub fehlerhaft |
| 0x94B9 | 94B9 - F-CAN SZL Lenkwinkelsensor : Sensor nicht abgeglichen - EEPROM defekt (nach Anklemmen der KL30) |
| 0x94BA | 94BA - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_BelZeit_0 Interner Softwarefehler. |
| 0x94BB | 94BB - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_VglAbwurf Fehler im Sub Lenkwinkel. |
| 0x94BC | 94BC - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_CRCFehlInCDB Fehler in EEPROM-Daten. |
| 0x94BD | 94BD - F-CAN SZL Lenkwinkelsensor : Sensorfehler - Info: Unterspannung, LWS_CRCRamSave Fehler im RAM-Bereich |
| 0x94BE | 94BE - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_Winkelpraediktion Codescheibe defekt. |
| 0x94BF | 94BF - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_TimeoutSubCom Verbindung zum SUB defekt. |
| 0x94C0 | 94C0 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_BelTimeout Klemme 30 Startzeit zu lang. |
| 0x94C1 | 94C1 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_TimeoutSub Kommunikationsfehler Sub. |
| 0x94C2 | 94C2 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_KeinAbgleich Nullpunktdaten fehlerhaft. |
| 0x94C3 | 94C3 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_ERROR allgemeiner Sensorfehler. |
| 0x94C4 | 94C4 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_REF_NOTFOUND keine Referenzspur gefunden. |
| 0x94C5 | 94C5 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_CRCSaveRamCopy Fehler im RAM. |
| 0x94C7 | 94C7 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_CRCLwsNullShw Nullpunktdaten CRC Fehler. |
| 0x94C8 | 94C8 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_CRCLwsShw Konfigurationsdaten CRC Fehler. |
| 0x94C9 | 94C9 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS_TimeoutEEPROM EEPROM Fehler. |
| 0x94E0 | 94E0 - F-CAN SZL EEPROM defekt - Prozessor defekt. |
| 0x94E1 | 94E1 - F-CAN SZL EEPROM defekt - Fehler intern Autocodierung. |
| 0x9500 | 9500 - F-CAN SZL Unterspannung   UBatt &lt; 8.5 V. |
| 0x9501 | 9501 - F-CAN SZL Ueberspannung    UBatt &gt; 16,5 V. |
| 0x9510 | 9510 - FGR/ACC-Lenkstockschalter (LST) haengt (alle tastenden Schalter)- mechanisch defekt, Kontakt |
| 0x9511 | 9511 - FGR/ACC-Lenkstockschalter (LST) unplausibel - Unzulaessige Kombination mit Tempomatschalter |
| 0x9512 | 9512 - FGR/ACC-Lenkstockschalter (LST) elektrisch defekt. |
| 0x9518 | 9518 - Scheibenwischerschalter (SWS) (alle tastenden Schalter)- mechanisch defekt, Kontakt. |
| 0x9519 | 9519 - Scheibenwischerschalter (SWS) unplausibel- Unzulaessige Kombination im Scheibenwischerschalter |
| 0x951A | 951A - Scheibenwischerschalter (SWS) -Schalter defekt - elektrisch defekt. |
| 0x9520 | 9520 - Lenkrad MFL: mechanisch defekt, Kontakt. |
| 0x5DD4 | 5DD4 - RPA abgeschaltet durch das Luftfeder Steuergeraet |
| 0x5DEF | 5DEF - Info. WLC (Wandler Launch Control) deaktiviert/stillgelegt |
| 0x5DEC | 5DEC - Info. FLR (Fahrleistungsreduzierung) aktiviert |
| 0x5DF8 | 5DF8 - Unterspannung Kl30 |
| 0x5E44 | 5E44 - Lenkwinkelsensor hat die Initialisierung verloren |
| 0x5E45 | 5E45 - Lenkwinkelsensor Fehler bei der Auswertung des Lenkwinkelsignals im DSC |
| 0x94C6 | 94C5 - F-CAN SZL Lenkwinkelsensor : Sensorfehler - LWS Nullpunkt CRC Fehler |
| 0x9502 | 9502 - F-CAN SZL Lenkwinkelsensor Unterspannung erkannt |
| 0x9503 | 9503 - F-CAN SZL Lenkwinkelsensor Ueberspannung erkannt |
| 0xD365 | D365 - PT-CAN Botschaft Luftfeder Fehler |
| 0x5E70 | 5E70 - Info: auf Grund der Fahrweise ergeben sich bei passiv getastetem DSC unplausible Sensorsignale, RPA und andere Zusatzfunktionen werden stillgelegt |
| 0xD36E | D36E - PT-CAN   Botschaft 310h A_TEMP_RELATIVZEIT fehlt oder ungueltig, Reifentemperaturmodell im RPA+ kann nicht berechnet werden |
| 0x5DD7 | 5DD7 - RPA+ kann nicht aufsetzen, waehrend der Initialisierungsphase werden keine oder nicht genuegend Kalibrierwerte gesammelt, Reifen fuer RPA+ nicht geeignet |
| 0xD379 | D379 - PT_CAN Botschaft 776 Status MSA fehlt |
| 0x5EFB | 5EFB - ELUP/Unterdrucksystem: Leckage Unterdrucksystem |
| 0x5EFE | 5EFE - ELUP/Unterdrucksystem: Unterdruck Sensor defekt |
| 0x5EFF | 5EFF -ELUP/Unterdrucksystem:  elektrische Unterdruckpumpe oder Ansteuerung (AE) defekt |
| 0xD368 | D368 - ELUP/Unterdrucksystem: PT_CAN Botschaft 8Dh STAT_ELUP ungueltig |
| 0xFFFF | unbekannter Fehlerort |

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

Dimensions: 1 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| default | 0x01 | DIGITAL1 | DIGITAL2 | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 17 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Fahrzeuggeschwindigkeit | km/h | - | unsigned char | - | 1 | 1 | 0 |
| 0x02 | Bremslichtschalter | 0/1 | - | 0x01 | - | 1 | 1 | 0 |
| 0x03 | Bremsfluessigkeitsschalter | 0/1 | - | 0x04 | - | 1 | 1 | 0 |
| 0x04 | ASC/DSC_aktiv (Tasterfunktion) | 0/1 | - | 0x08 | - | 1 | 1 | 0 |
| 0x05 | Bremsdruck erkannt | 0/1 | - | 0x20 | - | 1 | 1 | 0 |
| 0x06 | ABS-Regelung | 0/1 | high | 0x0100 | - | 1 | 1 | 0 |
| 0x07 | ASC-Regelung (BMR) | 0/1 | high | 0x0200 | - | 1 | 1 | 0 |
| 0x08 | ASC-Regelung (AMR) | 0/1 | high | 0x0400 | - | 1 | 1 | 0 |
| 0x09 | GMR-Regelung (GMR) | 0/1 | high | 0x0800 | - | 1 | 1 | 0 |
| 0x0A | GMR-Regelung (MMR) | 0/1 | high | 0x1000 | - | 1 | 1 | 0 |
| 0x0B | CBC-Regelung | 0/1 | high | 0x2000 | - | 1 | 1 | 0 |
| 0x0C | MSR-Regelung | 0/1 | high | 0x4000 | - | 1 | 1 | 0 |
| 0x0D | TDR-Regelung | 0/1 | high | 0x8000 | - | 1 | 1 | 0 |
| 0x0E | SDR-Regelung | 0/1 | high | 0x0001 | - | 1 | 1 | 0 |
| 0x0F | DBC-Regelung | 0/1 | high | 0x0002 | - | 1 | 1 | 0 |
| 0x10 | RTA aktiv | 0/1 | high | 0x0004 | - | 1 | 1 | 0 |
| 0x11 | Run-Up Mode | 0/1 | high | 0x0008 | - | 1 | 1 | 0 |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 39 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0xD347 | 0x0000 | 0x1004 | 0x0000 | 0x0000 |
| 0xD34B | 0x0000 | 0x1004 | 0x0000 | 0x0000 |
| 0xD354 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD355 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD356 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD357 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD358 | 0x0000 | 0x0004 | 0x0000 | 0x0000 |
| 0xD359 | 0x0000 | 0x0004 | 0x0000 | 0x0000 |
| 0xD35A | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD377 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD35B | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD35C | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD35D | 0x0000 | 0x0004 | 0x0000 | 0x0000 |
| 0xD361 | 0x0000 | 0x0004 | 0x0000 | 0x0000 |
| 0xD370 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD371 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD372 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD373 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD374 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD375 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD376 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0xD378 | 0x0000 | 0x0004 | 0x0000 | 0x0000 |
| 0xD379 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| 0x5E18 | 0x1008 | 0x0000 | 0x0000 | 0x0000 |
| 0x5E19 | 0x1008 | 0x0000 | 0x0000 | 0x0000 |
| 0x5E1A | 0x1008 | 0x0000 | 0x0000 | 0x0000 |
| 0x5E1B | 0x1008 | 0x0000 | 0x0000 | 0x0000 |
| 0x5E1C | 0x1008 | 0x0000 | 0x0000 | 0x0000 |
| 0xC987 | 0x0000 | 0x0000 | 0x0000 | 0x1004 |
| 0xC994 | 0x0000 | 0x0004 | 0x0000 | 0x0000 |
| 0xC995 | 0x0000 | 0x0000 | 0x0000 | 0x1008 |
| 0xC996 | 0x0000 | 0x0000 | 0x0000 | 0x1008 |
| 0xC997 | 0x0000 | 0x0004 | 0x0000 | 0x0000 |
| 0xC998 | 0x0000 | 0x0000 | 0x0000 | 0x1008 |
| 0xC99A | 0x0000 | 0x0000 | 0x0000 | 0x1008 |
| 0xC99B | 0x0000 | 0x0004 | 0x0000 | 0x0000 |
| 0xC99C | 0x0000 | 0x0004 | 0x0000 | 0x0000 |
| 0xD368 | 0x0008 | 0x0004 | 0x0002 | 0x0000 |
| default | 0x0000 | 0x0000 | 0x0000 | 0x0000 |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 15 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom. |
| 0x0002 | Fehler Alive-Zaehler. |
| 0x0004 | Timeout. |
| 0x0008 | Fehler Checksumme. |
| 0x1004 | Bus Off. |
| 0x1008 | physikalischer Wert ausserhalb gueltigem Bereich |
| 0x0010 | Testbedingungen erfuellt. |
| 0x0011 | Testbedingungen noch nicht erfuellt. |
| 0x0020 | Fehler bisher nicht aufgetreten. |
| 0x0021 | Fehler momentan nicht vorhanden, aber bereits gespeichert. |
| 0x0022 | Fehler momentan vorhanden, aber noch nicht gespeichert (Entprellphase). |
| 0x0023 | Fehler momentan vorhanden und bereits gespeichert. |
| 0x0030 | Fehler wuerde kein Aufleuchten einer Warnlampe verursachen. |
| 0x0031 | Fehler wuerde das Aufleuchten einer Warnlampe verursachen. |
| 0xFFFF | unbekannte Fehlerart. |

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

<a id="table-digital1"></a>
### DIGITAL1

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x02 | 0x03 | 0x04 | 0x05 |

<a id="table-digital2"></a>
### DIGITAL2

Dimensions: 1 rows × 13 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR | UW9_NR | UW10_NR | UW11_NR | UW12_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 12 | 0x06 | 0x07 | 0x08 | 0x09 | 0x0A | 0x0B | 0x0C | 0x0D | 0x0E | 0x0F | 0x10 | 0x11 |

<a id="table-steuern"></a>
### STEUERN

Dimensions: 14 rows × 3 columns

| STEUER_I_O | BYTE | BITWERT |
| --- | --- | --- |
| EVVL | 0 | 0x01 |
| AVVL | 0 | 0x02 |
| EVVR | 0 | 0x04 |
| AVVR | 0 | 0x08 |
| EVHL | 0 | 0x10 |
| AVHL | 0 | 0x20 |
| EVHR | 0 | 0x40 |
| AVHR | 0 | 0x80 |
| SV1 | 1 | 0x01 |
| SV2 | 1 | 0x02 |
| EUV1 | 1 | 0x04 |
| EUV2 | 1 | 0x08 |
| PUMPE | 1 | 0x10 |
| XYZ | 9 | 0x00 |

<a id="table-audio-tel"></a>
### AUDIO_TEL

Dimensions: 12 rows × 9 columns

| BIT | TEXT_TASTER_TEL | TEXT_TASTER_AUDIO | TEXT_TASTER_SUCH | TEXT_TASTER_TALK | TEXT_TASTER_HORN | TEXT_TASTER_SONDER | TEXT_TASTER_HEAR | WERT |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x00 | Keine_Aktion | Keine_Aktion | Keine_Aktion | Keine_Aktion | Keine_Aktion | Keine_Aktion | Keine_Aktion | 1 |
| 0x01 | Taster_TEL_gedrueckt | - | - | Taster_PTT_gedrueckt | - | - | - | 2 |
| 0x03 | Signal_ungueltig | - | - | Signal_ungueltig | - | - | - | 4 |
| 0x04 | - | Lautstaerke_leiser | - | - | Taster_HORN_gedrueckt | - | - | 2 |
| 0x08 | - | Lautstaerke_lauter | - | - | - | - | - | 3 |
| 0x0C | - | Signal_ungueltig | - | - | Signal_ungueltig | - | - | 4 |
| 0x10 | - | - | Suchlauf_abwaerts | - | - | Taster_gedrueckt | - | 2 |
| 0x20 | - | - | Suchlauf_aufwaerts | - | - | - | - | 3 |
| 0x30 | - | - | Signal_ungueltig | - | - | Signal_ungueltig | - | 4 |
| 0x40 | - | - | - | - | - | - | Taster_PTH_gedrueckt | 2 |
| 0xC0 | - | - | - | - | - | - | Signal_ungueltig | 4 |
| 0xXY | nicht_definiert | nicht_definiert | nicht_definiert | nicht_definiert | nicht_definiert | nicht_definiert | nicht_definiert | 99 |

<a id="table-temp-acc"></a>
### TEMP_ACC

Dimensions: 12 rows × 5 columns

| BIT | TEXT_TASTER | TEXT_ABSTAND | TEXT_MODUS | WERT |
| --- | --- | --- | --- | --- |
| 0x00 | Keine_Aktion | Keine_Aktion | Taster_Mode_Wahl_nicht_gedrueckt | 1 |
| 0x01 | Tippen_nach_vorne | Tippen_nach_oben | - | 2 |
| 0x02 | Ueberdruecken_nach_vorne | Tippen_nach_unten | - | 3 |
| 0x03 | - | Signal_ungueltig | - | 4 |
| 0x04 | Tippen_nach_hinten | - | Taster_Mode_Wahl_gedrueckt | 4 |
| 0x08 | Ueberdruecken_nach_hinten | - | - | 5 |
| 0x0C | - | - | Signal_ungueltig | 3 |
| 0x10 | Tippen_nach_unten | - | - | 6 |
| 0x40 | Axial_Tippen | - | - | 7 |
| 0x90 | Tippen_nach_oben | - | - | 8 |
| 0xFF | Signal_ungueltig | - | - | 9 |
| 0xXY | nicht_definiert | nicht_definiert | nicht_definiert | 99 |

<a id="table-wischer"></a>
### WISCHER

Dimensions: 12 rows × 4 columns

| BIT | TEXT_TASTER | TEXT_POTI | WERT |
| --- | --- | --- | --- |
| 0x00 | Keine_Aktion | Stufe_1 | 1 |
| 0x01 | Intervall/Automatik | Stufe_2 | 2 |
| 0x02 | Stufe_1 | Stufe_3 | 3 |
| 0x03 | Stufe_2 | - | 4 |
| 0x04 | - | Stufe_4 | 4 |
| 0x07 | - | Signal_ungueltig | 5 |
| 0x08 | Tippwischen | - | 5 |
| 0x10 | Frontwaschen | - | 6 |
| 0x40 | Heckwischen | - | 7 |
| 0x80 | Heckwaschen | - | 8 |
| 0xFF | Signal_ungueltig | - | 9 |
| 0xXY | nicht_definiert | nicht_definiert | 99 |

<a id="table-rad"></a>
### RAD

Dimensions: 5 rows × 4 columns

| BIT | DREHRICHTUNG_TEXT | DFA_TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | Drehrichtungserkennung in ECU nicht konfiguriert | - | 1 |
| 0x01 | vorwaerts | Stillstand | 2 |
| 0x02 | rueckwaerts | Fahrzeug faehrt | 3 |
| 0xFF | Signal nicht plausibel / nicht konfiguriert | keine Ausgabe | 4 |
| 0xXY | nicht_definiert | nicht_definiert | 99 |

<a id="table-cbs-bbv"></a>
### CBS_BBV

Dimensions: 5 rows × 3 columns

| BIT | CBS_BBV_TEXT | WERT |
| --- | --- | --- |
| 0x00 | OK | 1 |
| 0x01 | 1. Schwelle erreicht | 2 |
| 0x02 | nicht OK | 3 |
| 0xFF | Signal nicht verfuegbar | 4 |
| 0xXY | nicht_definiert | 99 |

<a id="table-sensor-cluster"></a>
### SENSOR_CLUSTER

Dimensions: 5 rows × 3 columns

| BIT | CLUSTER_TYPE | WERT |
| --- | --- | --- |
| 0x01 | Sensor Cluster VDO einfach | 1 |
| 0x02 | Sensor Cluster SYSTRON DONNER einfach | 2 |
| 0x03 | Sensor Cluster SYSTRON DONNER redundant | 3 |
| 0xFF | Signal ungueltig | 98 |
| 0xXY | nicht_definiert | 99 |

<a id="table-abgleich-v-ergebnis"></a>
### ABGLEICH_V_ERGEBNIS

Dimensions: 17 rows × 3 columns

| BIT | TEXT | WERT |
| --- | --- | --- |
| 0x01 | Keine_gueltigen_Abgleichswerte_gefunden | 1 |
| 0x02 | Gueltige_Abgleichswerte_gefunden | 2 |
| 0x03 | Abgleich_erfolgreich_mit_gutem_Ergebnis | 3 |
| 0x04 | Externer_Fehler_waehrend_Abgleich_entdeckt | 4 |
| 0x05 | Abgleich_laeuft_gerade | 5 |
| 0x06 | Interner_Fehler_entdeckt_nach_IGN_ON | 6 |
| 0x07 | Externer_Fehler_entdeckt_nach_IGN_ON | 7 |
| 0x08 | Interner_Fehler_waehrend_Abgleich_entdeckt | 8 |
| 0x00 | Randbedingungen_fuer_Kalibrierung_erfuellt | 0 |
| 0x10 | externe_Leckage | 16 |
| 0x20 | Raeder_drehen_sich | 32 |
| 0x30 | Bremse_wurde_betaetigt | 48 |
| 0x40 | Bremdruck_wurde_nicht_in_der_vorgeschriebenen_Zeit_erreicht | 64 |
| 0x50 | Spannungsversorgung_ausserhalb_gueltigem_Bereich | 80 |
| 0x0F | Keine_Einlassventile_ausgewaehlt | 15 |
| 0xF0 | Keine_MCI_Ventile_ausgewaehlt | 240 |
| 0xXY | kein_Ergebnis | 99 |

<a id="table-abgleich-lws-ergebnis"></a>
### ABGLEICH_LWS_ERGEBNIS

Dimensions: 3 rows × 3 columns

| BIT | TEXT | WERT |
| --- | --- | --- |
| 0x00 | Routine_nicht_erfolgreich_beendet_oder_Routine_wurde_nicht_gestartet | 0 |
| 0x01 | Routine_erfolgreich_beendet | 1 |
| 0xXY | kein_Ergebnis | 99 |

<a id="table-f-can-lw"></a>
### F_CAN_LW

Dimensions: 5 rows × 4 columns

| BIT | LW_RAD_FEHLER_TEXT | LW_OBEN_FEHLER_TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | in Ordnung | in Ordnung | 0 |
| 0x01 | LWS Verifizierung | Radlenkwinkelverifizierung | 1 |
| 0x02 | LWS-Signal fehlerhaft | Lenkwinkel_Rad-Signal fehlerhaft | 2 |
| 0x03 | Signal ungueltig | Signal ungueltig | 3 |
| 0xXY | nicht_definiert | nicht_definiert | 99 |

<a id="table-codierung"></a>
### CODIERUNG

Dimensions: 20 rows × 5 columns

| FUNKTION | BLOCK | BYTE | MASKE | DEFAULT |
| --- | --- | --- | --- | --- |
| ECD | 0x3005 | 0x00 | 0x01 | 0x01 |
| CBS | 0x3005 | 0x00 | 0x04 | 0x04 |
| FLR | 0x3005 | 0x00 | 0x10 | 0x00 |
| VCH | 0x3005 | 0x00 | 0x20 | 0x20 |
| HBA | 0x3005 | 0x00 | 0xC0 | 0xC0 |
| AY | 0x3005 | 0x01 | 0x01 | 0x00 |
| LW | 0x3005 | 0x01 | 0x02 | 0x00 |
| PSI_STAND | 0x3005 | 0x01 | 0x04 | 0x00 |
| PSI_FAHRT | 0x3005 | 0x01 | 0x08 | 0x00 |
| PSI_EMPF | 0x3005 | 0x01 | 0x10 | 0x00 |
| SW | 0x3005 | 0x01 | 0x20 | 0x00 |
| HVV | 0x3005 | 0x02 | 0x01 | 0x01 |
| SST | 0x3005 | 0x02 | 0x02 | 0x02 |
| EVB | 0x3005 | 0x02 | 0x04 | 0x04 |
| BSW | 0x3005 | 0x02 | 0x08 | 0x08 |
| HHC | 0x3005 | 0x02 | 0x10 | 0x10 |
| HPS | 0x3005 | 0x02 | 0x20 | 0x20 |
| ASL | 0x3005 | 0x02 | 0x40 | 0x40 |
| HDC | 0x3005 | 0x02 | 0x80 | 0x80 |
| XXX | 0xXY | 0xXY | 0xXY | 0xXY |

<a id="table-rpa"></a>
### RPA

Dimensions: 16 rows × 7 columns

| BYTE | M5_M6 | E85 | E85HP | M3 | E8X_E9X | WARN |
| --- | --- | --- | --- | --- | --- | --- |
| 0x01 | 15-50 km/h | 20-40 km/h | 20_50 km/h | 15-50 km/h | 15-70 km/h | Raderkennung |
| 0x02 | 50-90 km/h | 40-80 km/h | 50-90 km/h | 50-90 km/h | 70-110 km/h | over_all_HA&gt;Schwellwert |
| 0x03 | 90-130 km/h | 80-120 km/h | 90-130 km/h | 90-130 km/h | 110-150 km/h | over_all_VA&gt;Schwellwert |
| 0x04 | 130-170 km/h | 120-160 km/h | 130-170 km/h | 130-170 km/h | 150-190 km/h | grosser_Druckverlust |
| 0x05 | 170-210 km/h | 160-200 km/h | 170-210 km/h | 170-210 km/h | 190-220 km/h | Plattfuss |
| 0x06 | &gt;210 km/h | &gt;200 km/h | &gt;210 km/h | &gt;210 km/h | 220-250 km/h | alle_halbe_Druckschwelle |
| 0x07 | - | - | - | - | - | hinterer_Abfall |
| 0x08 | - | - | - | - | - | Delta_M |
| 0x11 | rechts_50%_bis_90_km/h | rechts_50%_bis_80_km/h | rechts_50%_bis_90_km/h | rechts_freirollend_bis_70_km/h | rechts_freirollend_bis_70_km/h | - |
| 0x12 | rechts_bis_90_km/h | rechts_bis_80_km/h | rechts_bis_90_km/h | rechts_bis_70_km/h | rechts_bis_70_km/h | - |
| 0x13 | links_50%_bis_90_km/h | links_50%_bis_80_km/h | links_50%_bis_90_km/h | links_freirollend_bis_70_km/h | links_freirollend_bis_70_km/h | - |
| 0x14 | links_bis_90_km/h | links_bis_80_km/h | links_bis_90_km/h | links_bis_70_km/h | links_bis_70_km/h | - |
| 0x15 | rechts_50%_ab_90_km/h | rechts_50%_ab_80_km/h | rechts_50%_ab_90_km/h | rechts_freirollend_ab_70_km/h | rechts_freirollend_ab_70_km/h | - |
| 0x16 | rechts_ab_90_km/h | rechts_ab_80_km/h | rechts_ab_90_km/h | rechts_ab_70_km/h | rechts_ab_70_km/h | - |
| 0x17 | links_50%_ab_90_km/h | links_50%_ab_80_km/h | links_50%_ab_90_km/h | links_freirollend_ab_70_km/h | links_freirollend_ab_70_km/h | - |
| 0x18 | links_ab_90_km/h | links_ab_90_km/h | links_ab_90_km/h | links_ab_70_km/h | links_ab_70_km/h | - |
