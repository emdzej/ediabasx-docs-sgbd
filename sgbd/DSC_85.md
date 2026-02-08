# DSC_85.prg

- Jobs: [71](#jobs)
- Tables: [27](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Dynamische Stabilitaets Control DSC E85 MK60E5  |
| ORIGIN | BMW EF-43 Kusch |
| REVISION | 1.000 |
| AUTHOR | BMW EF-43 Kusch |
| COMMENT | Conti_Teves MK60_E5, KWP2000 * , E85  |
| PACKAGE | 1.29 |
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
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers Modus  : Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers $16xx SubbusMemberSerialNumber Modus  : Default
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
- [PHYSIKALISCHE_HW_NR_LESEN](#job-physikalische-hw-nr-lesen) - Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [HARDWARE_REFERENZ_LESEN](#job-hardware-referenz-lesen) - Auslesen der Hardware Referenz KWP2000: $22   ReadDataByCommonIdentifier $2502 HWREF oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [SEED](#job-seed) - Status Eingaenge E87 DSC_MK60 KWP2000:$27,$03 oder  $27,$07 SecurityAccess service
- [SEED_07](#job-seed-07) - Status Eingaenge E87 DSC_MK60 KWP2000:$27,$03 oder  $27,$07 SecurityAccess service
- [IDENT_PRODUCTION_DATA](#job-ident-production-data) - KWP2000: $1A,$8F ReadECUIdentification Ident-Daten des SG ...
- [IDENT_VIN](#job-ident-vin) - KWP2000: $1A,$90 ReadECUIdentification Ident-Daten des SG: Fahrgestellnummer
- [IDENT_TEVES_ECU_SW_NR](#job-ident-teves-ecu-sw-nr) - KWP2000: $1A,$94 ReadECUIdentification Ident-Daten des SG: SW Nummer
- [IDENT_PROGRAMMING_DATE](#job-ident-programming-date) - KWP2000: $1A,$99 ReadECUIdentification Ident-Daten des SG: Herstelldatum
- [C_C_SCHREIBEN](#job-c-c-schreiben) - Codierdaten schreiben Standard Codierjob Fuer die Codierdaten werden als Argument ein vorgefuellter Binaerbuffer uebergeben KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und ruecklesen Standard Codierjob Fuer die Codierdaten werden als Argument ein vorgefuellter Binaerbuffer uebergeben KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [_COD_SCHREIBEN_DSC](#job-cod-schreiben-dsc) - KWP2000: $2E WriteDataByCommonIdentifier $3000 Codierdaten schreiben Es muessen 17 Codierdaten als ein Hex_String uebergeben werden: z.B. 01,AB,56,FF ... 16 Keine Checksumme im ersten Datenbyte eingeben die Checksumme wird automatisch berechnet Job DIAGNOSE_MODE ist integriert
- [_COD_LESEN](#job-cod-lesen) - Auslesen der Codierdaten KWP2000: $22 ReadDataByCommonIdentifier $3000 Codierdaten Modus  : Default
- [STATUS_RADGESCHWINDIGKEIT](#job-status-radgeschwindigkeit) - Fuer die Zuordnung Text-Wertausgabe, siehe Tabelle RAD KWP2000: $21,$07 ReadDataByLocalIdentifier service Radgeschwindigkeiten auslesen
- [STATUS_SCHALTER](#job-status-schalter) - KWP2000: $21,$05 ReadDataByLocalIdentifier service
- [STATUS_SENSOREN](#job-status-sensoren) - KWP2000: $21,$06 ReadDataByLocalIdentifier service gueltig ab I3.70
- [STATUS_SENSOREN_OFFSET](#job-status-sensoren-offset) - KWP2000: $21,$02 ReadDataByLocalIdentifier service gueltig ab I3.70
- [BET_AKTIV](#job-bet-aktiv) - Bandendetest aktivieren KWP2000: $31 StartRoutineByLocalIdentifier service $23 BET BET_AKTIV beinhaltet den Job DIAGNOSE_MODE
- [BET_PASSIV](#job-bet-passiv) - Bandendetest passiv schalten KWP2000: $31 StartRoutineByLocalIdentifier service $23 BET BET_PASSIV beinhaltet den Job DIAGNOSE_MODE
- [STEUERN_DIGITAL_DX](#job-steuern-digital-dx) - KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) davon koennen bis maximal 9 Argumente vorgegeben werden E or W EVVL AVVL EVVR AVVR EVHL AVHL EVHR AVHR PUMPE SV1 SV2 EUV1 EUV2 Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode,  und Ansteuersequenz-Ausfuehren: Mit dem Parameter"W" wird nur die Ansteuersequenz ausgefuehrt Musterparametersatz_1: "E,EVVL,EVVR,SV1,0,0,0,0,0,0,800,PUMPE,0,0,0,0,0,0,0,0,1000" Musterparametersatz_2: "W,EVVL,EVVR,EVHL,EVHR,AVVL,AVVR,AVHL,AVHR,0,200,PUMPE,0,0,0,0,0,0,0,0,2000" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) in jedem Job koennen dann 9 beliebige Stellglieder angesteuert werden und zwar 1 Stellgliedgruppe vor dem Zeitglied und 1 Stellgliedgruppe nach dem Zeitglied dazwischen steht das Argument fuer die Wartezeit:  W_ZEIT in ms als letzter Parameter steht eine Wartezeit zum Job Status OK WAIT_STATUS_JOB in ms NUR volle tausender Werte eingeben (1000,2000....) eine Stellgliedgruppe besteht immer aus 9 Argumenten (9 Stellglieder) werden weniger als 9 Stellglieder angesteuert so sind die restlichen mit "0" zu besetzen(siehe Musterparametersatz_1)
- [STEUERN_DIGITAL](#job-steuern-digital) - KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern hier sind keine 0-Stellglieder mehr erforderlich (vgl.STEUERN_DIGITAL_DX) Parameterliste: (mit Strichpunkt getrennt) es koennen  maximal 19 Argumente vorgegeben werden E oder W,EVVL, AVVL,EVVR,AVVR,EVHL,AVHL,EVHR,AVHR,PUMPE,SV1,SV2,EUV1,EUV2 Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode,  und Ansteuersequenz-Ausfuehren: Mit dem Parameter"W" wird nur die Ansteuersequenz ausgefuehrt Musterparametersatz_1: "E,EVVL,EVVR,SV1,800,PUMPE," Musterparametersatz_2: "W,EVVL,EVVR,EVHL,EVHR,AVVL,AVVR,1000,AVHL,AVHR,PUMPE" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) es koennen 2 beliebige Stellgliedgruppen angesteuert werden und zwar 1 Stellgliedgruppe vor dem Zeitglied und 1 Stellgliedgruppe nach dem Zeitglied zwischen den Stellgliedgruppen steht das Argument fuer das Zeitglied (Wartezeit in ms)
- [STEUERN_DIGITAL_BLS](#job-steuern-digital-bls) - KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern Parameterliste: (mit Strichpunkt getrennt) Es koennen max 13 Ausgaenge vorgegeben werden E or W EVVL AVVL EVVR AVVR EVHL AVHL EVHR AVHR PUMPE SV1 SV2 EUV1 EUV2 BLS Musterparametersatz: "W,EVVL,EVVR,EVHL,EVHR,AVVL,AVVR,PUMPE" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) Die Ventilansteuerung wird solange wiederholt, bis der Bremslichtschalter wieder geloest wird, max. jedoch 200 Zyklen lang (ca.8sec) die Ventilansteuersequenz wird vor und hinter dem Zeitglied identisch eingetragen der Defaultzeitwert (Zeitglied) beträgt 10ms
- [NA_ENTLUEFTUNG_RE_DX](#job-na-entlueftung-re-dx) - Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert
- [NA_ENTLUEFTUNG_LI_DX](#job-na-entlueftung-li-dx) - Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert
- [NA_ENTLUEFTUNG_VA_DX](#job-na-entlueftung-va-dx) - Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert
- [NA_ENTLUEFTUNG_HA_DX](#job-na-entlueftung-ha-dx) - Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert
- [IDENT_SCHREIBEN](#job-ident-schreiben) - KWP2000: $3B WriteDataByLocalIdentifier $80 BMW Identifikation schreiben
- [IDENT_PROGRAMMING_DATE_SCHREIBEN](#job-ident-programming-date-schreiben) - KWP2000:$3B,$99 WriteDataByLocalIdentifier service Ident-Daten des SG schreiben: Herstelldatum
- [IDENT_PRODUCTION_DATA_SCHREIBEN](#job-ident-production-data-schreiben) - KWP2000:$3B,$8F WriteDataByLocalIdentifier service Ident-Daten des SG schreiben
- [STATUS_LWS_LI_RE_MAX](#job-status-lws-li-re-max) - Auslesen der CAN Botschaft LWS_1 KWP2000: $22 ReadDataByCommonIdentifier $01F5 CAN_LWS_1 Job laeuft max. 16 sec: werden die Max-Werte vorher erreicht, wird der Job abgebrochen
- [STATUS_LESEN_RPA](#job-status-lesen-rpa) - KWP2000:$21,$04 ReadDataByLocalIdentifier service Alle RPA Daten auslesen
- [STATUS_LESEN_RPA_M](#job-status-lesen-rpa-m) - KWP2000:$21,$04 ReadDataByLocalIdentifier service Alle RPA Daten auslesen
- [RPA_RESET](#job-rpa-reset) - KWP2000:$31,$25 StartRoutineByLocalIdentifier service resertiert alle gelernten RPA Werte
- [RPA_EOL_PASSIV](#job-rpa-eol-passiv) - KWP2000:$31,$26 StartRoutineByLocalIdentifier service Auslieferungsmodus der Werke lernt keinen neuen RPA Werte RPA muss beim Kunden resertiert werden
- [_FS_LESEN_SAR](#job-fs-lesen-sar) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus    : Default
- [_ANZAHL_SUBBUS_TEILNEHMER_LESEN](#job-anzahl-subbus-teilnehmer-lesen) - Anzahl Subbus Teilnehmer lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 Anzahl Subbus Teilnehmer lesen Modus    : Default
- [_IDENT_SENSORCLUSTER](#job-ident-sensorcluster) - Auslesen des DSC Sensor-Clusters KWP2000: $22 ReadDataByCommonIdentifier $1601 DSC Sensor-Cluster  lesen Modus    : Default
- [DRUCKSENSOR_DSC_ABGLEICHEN](#job-drucksensor-dsc-abgleichen) - KWP2000: $31,$20 StartRoutineByLocalIdentifier service
- [QUERBESCHLEUNIGUNG_DSC_ABGLEICHEN](#job-querbeschleunigung-dsc-abgleichen) - KWP2000: $31,$22 StartRoutineByLocalIdentifier service
- [LAENGSBESCHLEUNIGUNG_DSC_ABGLEICHEN](#job-laengsbeschleunigung-dsc-abgleichen) - KWP2000: $31,$24 StartRoutineByLocalIdentifier service
- [LENKWINKEL_DSC_ABGLEICHEN](#job-lenkwinkel-dsc-abgleichen) - KWP2000: $31,$21 StartRoutineByLocalIdentifier service
- [ABGLEICH_ANALOG_EV](#job-abgleich-analog-ev) - KWP2000:$31,$28 StartRoutineByLocalIdentifier service Abgleich Analog Einlassventil
- [ABGLEICH_ANALOG_MCI_V](#job-abgleich-analog-mci-v) - KWP2000:$31,$29 StartRoutineByLocalIdentifier service Abgleich Analog MCI Ventile
- [STAT_ERGEBNIS_ABGLEICH_ROUTINE](#job-stat-ergebnis-abgleich-routine) - Ergebnis der Routine abholen Musterparametersatz: "ANALOG_MCI_V" fuer Abgleich Analog MCI Ventil Musterparametersatz: "ANALOG_EV" fuer Abgleich der analogen Einlassventile Musterparametersatz: "LWS" fuer Abgleich Lenkwinkelsensor oder mit 2. Argument "R": "ANALOG_EV,R" oder "ANALOG_MCI_V,R" oder "LWS,R" dann wird eine Schleife max. 20sec durchlaufen, bis endgueltiges Ergebnis der Routine vorliegt jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) Fuer die Zuordnung der Ausgabe Text-Wert siehe Tabelle ABGLEICH_V_ERGEBNIS KWP2000: $33 $28/$29 RequestRoutineResultsByLocalIdentifier
- [_TEL_SCHREIBEN](#job-tel-schreiben) - KWP2000 Dieser Job bietet die Moeglichkeit an, ein eigenes Telegramm zu verschicken Es muessen 2 Argumente eingegeben werden, beide mit "Strich_Punkt" getrennt (nicht mit Komma!): Erstes Argument: E oder W Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode und Telegramm-Ausfuehren: Mit dem Parameter"W" wird nur das Telegramm ausgefuehrt Zweiter Argument: Die ersten 3 Bytes des Telegramms (Format,Target,Source) sind schon vorhanden die restlichen Bytes als ein Hex_String, alle mit Komma getrennt z.B. 00,11,22,... Keine Laenge eingeben, sie wird automatisch berechnet Musterparametersatz_1: "E,34,22,FE,00" Musterparametersatz_2: "W,EE,A1,22,33" Aufpassen: 2 Argumente (E_OR_W,T_BYTES) mit "Strich_Punkt" getrennt (nicht mit Komma !) nach dem E oder W immer "Strich_Punkt" aber folgende T_Bytes mit Komma getrennt!
- [_EEPROM_LESEN](#job-eeprom-lesen) - Lesen  EEPROM Zellen Zwei Argumente muessen eingegeben werden: die Start-Adresse und die End-Adresse. Musterparametersatz: "Start-Adresse,End-Adresse", jedoch mit "Strichpunkt" getrennt. Musterparametersatz: "224,244", jedoch mit "Strichpunkt" getrennt. Musterparametersatz: "0x00E0,0x00F4", jedoch mit "Strichpunkt" getrennt. Adressenbereich: 0x000000 - 0x0003FF KWP2000: $23 $03 ReadMemoryByAddress
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht)

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

<a id="job-seed"></a>
### SEED

Status Eingaenge E87 DSC_MK60 KWP2000:$27,$03 oder  $27,$07 SecurityAccess service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG_1 | binary | Anforderungstelegramm |
| _TEL_AUFTRAG_2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |
| JOB_STATUS | string | OKAY, oder FEHLER |

<a id="job-seed-07"></a>
### SEED_07

Status Eingaenge E87 DSC_MK60 KWP2000:$27,$03 oder  $27,$07 SecurityAccess service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_AUFTRAG_1 | binary | Anforderungstelegramm |
| _TEL_AUFTRAG_2 | binary | Anforderungstelegramm |
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
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT3 | binary | Hex-Antwort von SG |

<a id="job-cod-schreiben-dsc"></a>
### _COD_SCHREIBEN_DSC

KWP2000: $2E WriteDataByCommonIdentifier $3000 Codierdaten schreiben Es muessen 17 Codierdaten als ein Hex_String uebergeben werden: z.B. 01,AB,56,FF ... 16 Keine Checksumme im ersten Datenbyte eingeben die Checksumme wird automatisch berechnet Job DIAGNOSE_MODE ist integriert

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

<a id="job-cod-lesen"></a>
### _COD_LESEN

Auslesen der Codierdaten KWP2000: $22 ReadDataByCommonIdentifier $3000 Codierdaten Modus  : Default

_No arguments._

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
| STAT_RAD_GESCHW_EINH | string | Einheit = km/h |
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
| STAT_DFA_WERK_MODE | int | 1 = Normal Mode / 0 = Werk-Mode , nur wenn DFA verfuegbar ist |
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

KWP2000:$30,$10,$07 InputOutputControlByLocalIdentifier service Ventile ansteuern hier sind keine 0-Stellglieder mehr erforderlich (vgl.STEUERN_DIGITAL_DX) Parameterliste: (mit Strichpunkt getrennt) es koennen  maximal 19 Argumente vorgegeben werden E oder W,EVVL, AVVL,EVVR,AVVR,EVHL,AVHL,EVHR,AVHR,PUMPE,SV1,SV2,EUV1,EUV2 Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode,  und Ansteuersequenz-Ausfuehren: Mit dem Parameter"W" wird nur die Ansteuersequenz ausgefuehrt Musterparametersatz_1: "E,EVVL,EVVR,SV1,800,PUMPE," Musterparametersatz_2: "W,EVVL,EVVR,EVHL,EVHR,AVVL,AVVR,1000,AVHL,AVHR,PUMPE" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) es koennen 2 beliebige Stellgliedgruppen angesteuert werden und zwar 1 Stellgliedgruppe vor dem Zeitglied und 1 Stellgliedgruppe nach dem Zeitglied zwischen den Stellgliedgruppen steht das Argument fuer das Zeitglied (Wartezeit in ms)

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
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT2 | binary | Antworttelegramm |

<a id="job-na-entlueftung-re-dx"></a>
### NA_ENTLUEFTUNG_RE_DX

Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-na-entlueftung-li-dx"></a>
### NA_ENTLUEFTUNG_LI_DX

Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-na-entlueftung-va-dx"></a>
### NA_ENTLUEFTUNG_VA_DX

Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |

<a id="job-na-entlueftung-ha-dx"></a>
### NA_ENTLUEFTUNG_HA_DX

Steuern_Digital ansteuern u. ruecksetzen Job DIAGNOSE_MODE ist integriert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
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
| STAT_DRUCKSCHWELLE_GROB_20_40_KMH | int |  |
| STAT_DRUCKSCHWELLE_GROB_40_80_KMH | int |  |
| STAT_DRUCKSCHWELLE_GROB_80_120_KMH | int |  |
| STAT_DRUCKSCHWELLE_GROB_120_160_KMH | int |  |
| STAT_DRUCKSCHWELLE_GROB_160_200_KMH | int |  |
| STAT_DRUCKSCHWELLE_GROB_200_PLUS_KMH | int |  |
| STAT_DRUCKSCHWELLE_FEIN_20_40_KMH | int |  |
| STAT_DRUCKSCHWELLE_FEIN_40_80_KMH | int |  |
| STAT_DRUCKSCHWELLE_FEIN_80_120_KMH | int |  |
| STAT_DRUCKSCHWELLE_FEIN_120_160_KMH | int |  |
| STAT_DRUCKSCHWELLE_FEIN_160_200_KMH | int |  |
| STAT_DRUCKSCHWELLE_FEIN_200_PLUS_KMH | int |  |
| STAT_MOMENTENKOMPENSATION_0_50_NM | int |  |
| STAT_MOMENTENKOMPENSATION_50_100_NM | int |  |
| STAT_MOMENTENKOMPENSATION_100_150_NM | int |  |
| STAT_MOMENTENKOMPENSATION_150_200_NM | int |  |
| STAT_MOMENTENKOMPENSATION_200_250_NM | int |  |
| STAT_MOMENTENKOMPENSATION_250_300_NM | int |  |
| STAT_MOMENTENKOMPENSATION_FAST_0_50_NM | int |  |
| STAT_MOMENTENKOMPENSATION_FAST_50_100_NM | int |  |
| STAT_MOMENTENKOMPENSATION_FAST_100_150_NM | int |  |
| STAT_MOMENTENKOMPENSATION_FAST_150_200_NM | int |  |
| STAT_MOMENTENKOMPENSATION_FAST_200_250_NM | int |  |
| STAT_MOMENTENKOMPENSATION_FAST_250_300_NM | int |  |
| STAT_KURVENKOMPENSATION_LINKS_50_PROZ | int |  |
| STAT_KURVENKOMPENSATION_LINKS_100_PROZ | int |  |
| STAT_KURVENKOMPENSATION_RECHTS_50_PROZ | int |  |
| STAT_KURVENKOMPENSATION_RECHTS_100_PROZ | int |  |
| STAT_WARNUNG_AKTUELL | int |  |
| STAT_FUNKTIONSTEST | int |  |
| STAT_WARN_HISTORY_RAD_ERKENNUNG | int |  |
| STAT_WARN_HISTORY_HA_ERKENNUNG | int |  |
| STAT_WARN_HISTORY_VA_ERKENNUNG | int |  |
| STAT_WARN_HISTORY_HOHER_DRUCKVERLUST | int |  |
| STAT_WARN_HISTORY_HALBE_SCHWELLE | int |  |
| STAT_WARN_GRUND_RAD_ERKENNUNG | int |  |
| STAT_WARN_GRUND_HA_ERKENNUNG | int |  |
| STAT_WARN_GRUND_VA_ERKENNUNG | int |  |
| STAT_WARN_GRUND_HOHER_DRUCKVERLUST | int |  |
| STAT_WARN_GRUND_HALBE_SCHWELLE | int |  |
| STAT_PANNEN_WERT_PROZENT | int |  |
| STAT_PANNEN_ZAEHLER | int |  |
| STAT_L1 | int | Lernstati 1 fuer VS-22 |
| STAT_L1_EINH | string | Einheit Lernstati 1= % |
| STAT_L2 | int | Lernstati 2 fuer VS-22 |
| STAT_L2_EINH | string | Einheit Lernstati 2= % |
| STAT_L3 | int | Lernstati 3 fuer VS-22 |
| STAT_L3_EINH | string | Einheit Lernstati 3= % |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-lesen-rpa-m"></a>
### STATUS_LESEN_RPA_M

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
| STAT_DRUCKSCHWELLE_GROB_20_50_KMH | int |  |
| STAT_DRUCKSCHWELLE_GROB_50_90_KMH | int |  |
| STAT_DRUCKSCHWELLE_GROB_90_130_KMH | int |  |
| STAT_DRUCKSCHWELLE_GROB_130_170_KMH | int |  |
| STAT_DRUCKSCHWELLE_GROB_170_210_KMH | int |  |
| STAT_DRUCKSCHWELLE_GROB_210_PLUS_KMH | int |  |
| STAT_DRUCKSCHWELLE_FEIN_20_50_KMH | int |  |
| STAT_DRUCKSCHWELLE_FEIN_50_90_KMH | int |  |
| STAT_DRUCKSCHWELLE_FEIN_90_130_KMH | int |  |
| STAT_DRUCKSCHWELLE_FEIN_130_170_KMH | int |  |
| STAT_DRUCKSCHWELLE_FEIN_170_210_KMH | int |  |
| STAT_DRUCKSCHWELLE_FEIN_210_PLUS_KMH | int |  |
| STAT_MOMENTENKOMPENSATION_0_50_NM | int |  |
| STAT_MOMENTENKOMPENSATION_50_100_NM | int |  |
| STAT_MOMENTENKOMPENSATION_100_150_NM | int |  |
| STAT_MOMENTENKOMPENSATION_150_200_NM | int |  |
| STAT_MOMENTENKOMPENSATION_200_250_NM | int |  |
| STAT_MOMENTENKOMPENSATION_250_300_NM | int |  |
| STAT_MOMENTENKOMPENSATION_FAST_0_50_NM | int |  |
| STAT_MOMENTENKOMPENSATION_FAST_50_100_NM | int |  |
| STAT_MOMENTENKOMPENSATION_FAST_100_150_NM | int |  |
| STAT_MOMENTENKOMPENSATION_FAST_150_200_NM | int |  |
| STAT_MOMENTENKOMPENSATION_FAST_200_250_NM | int |  |
| STAT_MOMENTENKOMPENSATION_FAST_250_300_NM | int |  |
| STAT_KURVENKOMPENSATION_LINKS_50_PROZ | int |  |
| STAT_KURVENKOMPENSATION_LINKS_100_PROZ | int |  |
| STAT_KURVENKOMPENSATION_RECHTS_50_PROZ | int |  |
| STAT_KURVENKOMPENSATION_RECHTS_100_PROZ | int |  |
| STAT_WARNUNG_AKTUELL | int |  |
| STAT_FUNKTIONSTEST | int |  |
| STAT_WARN_HISTORY_RAD_ERKENNUNG | int |  |
| STAT_WARN_HISTORY_HA_ERKENNUNG | int |  |
| STAT_WARN_HISTORY_VA_ERKENNUNG | int |  |
| STAT_WARN_HISTORY_HOHER_DRUCKVERLUST | int |  |
| STAT_WARN_HISTORY_DRUCKLOS | int |  |
| STAT_WARN_HISTORY_HALBE_SCHWELLE | int |  |
| STAT_WARN_HISTORY_GRADIENT | int |  |
| STAT_WARN_HISTORY_DELTA_M | int |  |
| STAT_WARN_GRUND_RAD_ERKENNUNG | int |  |
| STAT_WARN_GRUND_HA_ERKENNUNG | int |  |
| STAT_WARN_GRUND_VA_ERKENNUNG | int |  |
| STAT_WARN_GRUND_HOHER_DRUCKVERLUST | int |  |
| STAT_WARN_GRUND_DRUCKLOS | int |  |
| STAT_WARN_GRUND_HALBE_SCHWELLE | int |  |
| STAT_WARN_GRUND_GRADIENT | int |  |
| STAT_WARN_GRUND_DELTA_M | int |  |
| STAT_PANNEN_WERT_PROZENT | int |  |
| STAT_PANNEN_ZAEHLER | int |  |
| STAT_L1 | int | Lernstati 1 fuer VS-22 |
| STAT_L1_EINH | string | Einheit Lernstati 1= % |
| STAT_L2 | int | Lernstati 2 fuer VS-22 |
| STAT_L2_EINH | string | Einheit Lernstati 2= % |
| STAT_L3 | int | Lernstati 3 fuer VS-22 |
| STAT_L3_EINH | string | Einheit Lernstati 3= % |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-rpa-reset"></a>
### RPA_RESET

KWP2000:$31,$25 StartRoutineByLocalIdentifier service resertiert alle gelernten RPA Werte

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-rpa-eol-passiv"></a>
### RPA_EOL_PASSIV

KWP2000:$31,$26 StartRoutineByLocalIdentifier service Auslieferungsmodus der Werke lernt keinen neuen RPA Werte RPA muss beim Kunden resertiert werden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, oder FEHLER |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

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

<a id="job-ident-sensorcluster"></a>
### _IDENT_SENSORCLUSTER

Auslesen des DSC Sensor-Clusters KWP2000: $22 ReadDataByCommonIdentifier $1601 DSC Sensor-Cluster  lesen Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DSC_SC_VERBAUORT | string | DSC-Sensorcluster Verbauort |
| DSC_SC_HW_NR | string | DSC-Sensorcluster Hardware Nummer |
| DSC_SC_SW_NR | string | DSC-Sensorcluster Software Nummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |

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
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |

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
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |

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
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_4 | binary | Hex-Antwort von SG |
| ABGL_LWS_ID | int | Abgleichswert LWS ID |
| STATUS_ABGLEICH_1 | binary | Fehlerstatus LWS |
| STATUS_ABGLEICH_2 | binary | Fehlerstatus LWS |
| STATUS_ABGLEICH_3 | binary | Fehlerstatus LWS |
| STATUS_ABGLEICH_4 | binary | Fehlerstatus LWS |

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
| _TEL_ANTWORT_1 | binary | Antworttelegramm |

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
| _TEL_ANTWORT_1 | binary | Antworttelegramm |

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

<a id="job-tel-schreiben"></a>
### _TEL_SCHREIBEN

KWP2000 Dieser Job bietet die Moeglichkeit an, ein eigenes Telegramm zu verschicken Es muessen 2 Argumente eingegeben werden, beide mit "Strich_Punkt" getrennt (nicht mit Komma!): Erstes Argument: E oder W Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode und Telegramm-Ausfuehren: Mit dem Parameter"W" wird nur das Telegramm ausgefuehrt Zweiter Argument: Die ersten 3 Bytes des Telegramms (Format,Target,Source) sind schon vorhanden die restlichen Bytes als ein Hex_String, alle mit Komma getrennt z.B. 00,11,22,... Keine Laenge eingeben, sie wird automatisch berechnet Musterparametersatz_1: "E,34,22,FE,00" Musterparametersatz_2: "W,EE,A1,22,33" Aufpassen: 2 Argumente (E_OR_W,T_BYTES) mit "Strich_Punkt" getrennt (nicht mit Komma !) nach dem E oder W immer "Strich_Punkt" aber folgende T_Bytes mit Komma getrennt!

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

<a id="job-diagnose-aufrecht"></a>
### DIAGNOSE_AUFRECHT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (4 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (76 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (11 × 2)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (9 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (109 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (17 × 9)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (10 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [DIGITAL1](#table-digital1) (1 × 5)
- [DIGITAL2](#table-digital2) (1 × 13)
- [STEUERN](#table-steuern) (14 × 3)
- [RAD](#table-rad) (5 × 4)
- [ABGLEICH_V_ERGEBNIS](#table-abgleich-v-ergebnis) (17 × 3)
- [ABGLEICH_LWS_ERGEBNIS](#table-abgleich-lws-ergebnis) (3 × 3)
- [F_CAN_LW](#table-f-can-lw) (5 × 4)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)

<a id="table-konzept-tabelle"></a>
### KONZEPT_TABELLE

Dimensions: 4 rows × 2 columns

| NR | KONZEPT_TEXT |
| --- | --- |
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

<a id="table-verbauorttabelle"></a>
### VERBAUORTTABELLE

Dimensions: 11 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0100 | Batteriesensor |
| 0x0200 | Elektrische Wasserpumpe |
| 0x0300 | Generator 1 |
| 0x0350 | Generator 2 |
| 0x0400 | Schaltzentrum Lenksäule |
| 0x0500 | DSC Sensor-Cluster |
| 0x0600 | Nahbereichsradarsensor links |
| 0x0700 | Nahbereichsradarsensor rechts |
| 0x0800 | Funkempfänger |
| 0x0900 | Elektrische Lenksäulenverriegelung |
| 0xFFFF | unbekannter Verbauort |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 9 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_ECU_REJECTED |
| 0xB0 | ERROR_ECU_PARAMETER |
| 0xB1 | ERROR_ECU_FUNCTION |
| 0xB2 | ERROR_ECU_NUMBER |
| 0xFF | ERROR_ECU_NACK |
| 0x00 | ERROR_ECU_UNKNOWN_STATUSBYTE |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 4 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| - | BMW-FAST |
| 1 | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 109 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5D99 | 5D99 - F_CAN Bus_Off. |
| 0x5D8F | 5D8F - Sensorcluster Fehler intern. |
| 0x5D97 | 5D97 - Sensorcluster Versorgungsspannung ausserhalb gueltigem Bereich. |
| 0x5D9A | 5D9A - Drucksensor vorne links elektrisch defekt. |
| 0x5D9B | 5D9B - Drucksensor vorne links Plausibilitaet. |
| 0x5D9C | 5D9C - Drucksensor vorne links Vorderachse Plausibilitaet. |
| 0x5D9E | 5D9E - Drucksensor vorne links p1 Gradient Fehler. |
| 0x5D9F | 5D9F - Drucksensor vorne links Plausibilitaet Feinabstimmungsfehler. |
| 0x5DAA | 5DAA - Drucksensor vorne rechts elektrisch defekt. |
| 0x5DAB | 5DAB - Drucksensor vorne rechts Plausibilitaet. |
| 0x5DAC | 5DAC - Drucksensor vorne rechts Vorderachse Plausibilitaet. |
| 0x5DAE | 5DAE - Drucksensor vorne rechts p1 Gradient Fehler. |
| 0x5DAF | 5DAF - Drucksensor vorne rechts Plausibilitaet Feinabstimmungsfehler. |
| 0x5DBA | 5DBA - Drucksensor hinten links elektrisch defekt. |
| 0x5DBB | 5DBB - Drucksensor hinten links Plausibilitaet. |
| 0x5DBC | 5DBC - Drucksensor hinten links Hinterachse Plausibilitaet. |
| 0x5DBE | 5DBE - Drucksensor hinten links p1 Gradient Fehler. |
| 0x5DBF | 5DBF - Drucksensor hinten links Plausibilitaet Feinabstimmungsfehler. |
| 0x5DCA | 5DCA - Drucksensor hinten rechts elektrisch defekt. |
| 0x5DCB | 5DCB - Drucksensor hinten rechts Plausibilitaet. |
| 0x5DCC | 5DCC - Drucksensor hinten rechts Hinterachse Plausibilitaet. |
| 0x5DCE | 5DCE - Drucksensor hinten rechts p1 Gradient Fehler. |
| 0x5DCF | 5DCF - Drucksensor hinten rechts Plausibilitaet Feinabstimmungsfehler. |
| 0x5DD0 | 5DD0 - Ventil Abgleich Daten fehlen. |
| 0x5DD1 | 5DD1 - RPA EEPROM Checksumme-Fehler. |
| 0x5DD2 | 5DD2 - Einlassventil Abgleichdaten fehlen. |
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
| 0x5E11 | 5E11 - CAN-Bus Off, Interner Fehler CAN-Controller |
| 0x5E14 | 5E14 - CAN Timeout DME/DDE |
| 0x5E15 | 5E15 - CAN Timeout EGS |
| 0x5E1E | 5E1E - CAN Timeout Lenkwinkel |
| 0x5E16 | 5E16 - CAN Timeout Instrumentenkombi |
| 0x5E18 | 5E18 - CAN DME/DDE Botschaft unplausibel. |
| 0x5E19 | 5E19 - CAN DME/DDE, Motormoment nicht einstellbar. |
| 0x5E1A | 5E1A - CAN DME/DDE Signal Fehler. |
| 0x5E1F | 5E1F - PT-CAN Fahrgestellnummer falsch / ECU nicht initialisiert. |
| 0x5E50 | 5E50 - F-CAN SZL Seriennummer falsch. |
| 0x5E51 | 5E51 - F-CAN SZL Seriennummer ungueltig. |
| 0x5E20 | 5E20 - Drucksensor 1 elektrisch defekt. |
| 0x5E24 | 5E24 - Drucksensor 1 unplausibel. |
| 0x5E25 | 5E25 - Drucksensor 1 unplausibel Feinabstimmungsfehler. |
| 0x5E26 | 5E26 - Spannungsversorgung Sensoren. |
| 0x5E2D | 5E2D - DSC Differenzdruckueberwachung VA/HA zulaessiger Differenzdruck ueberschritten |
| 0x5E2E | 5E2E - Schalter Rueckwaertsgang Plausibilitaet. |
| 0x5E2F | 5E2F - Temperatur Sensor. |
| 0x5E30 | 5E30 - Querbeschleunigungssensor Signal ausserhalb gueltigem Bereich oder elektrisch defekt. |
| 0x5E32 | 5E32 - Querbeschleunigungssensor unplausibel. |
| 0x5E34 | 5E34 - Laengsbeschleunigungssensor Signal ausserhalb gueltigem Bereich oder elektrisch defekt. |
| 0x5E35 | 5E35 - Laengsbeschleunigungssensor unplausibel. |
| 0x5E38 | 5E38 - Gierratensensor Signal ausserhalb gueltigem Bereich oder elektrisch defekt. |
| 0x5E3C | 5E3C - Gierratensensor unplausibel. |
| 0x5E40 | 5E40 - Lenkwinkelsensor Signal unplausibel,Offset. |
| 0x5E43 | 5E43 - Lenkwinkelsensor intern. |
| 0x5E4E | 5E4E - DSC Sensor Offset Check. |
| 0x5E4F | 5E4F - DSC Dauerregelung. |
| 0x5E58 | 5E58 - ASC ECU im falschen Fahrzeug. |
| 0x5E59 | 5E59 - Codierfehler. |
| 0x5E5B | 5E5B - DSC Taster laenger als 10sec gedrueckt oder Fehler. |
| 0x5E5C | 5E5C - RPA Taster Fehler. |
| 0x5E5D | 5E5D - Bremsfluessigkeitsniveau niedrig / Schalter defekt. |
| 0x5E5E | 5E5E - Bremslichtschalter Fehler, Plausibilitaets Fehler. |
| 0x5DE0 | 5DE0 - Bremsbelagverschleiss VA nicht/falsch initialisiert. |
| 0x5DE1 | 5DE1 - Bremsbelagverschleiss HA nicht/falsch initialisiert. |
| 0x5DE2 | 5DE2 - Bremsbelagverschleiss VA kritische Belagdicke erreicht. |
| 0x5DE3 | 5DE3 - Bremsbelagverschleiss HA kritische Belagdicke erreicht. |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | nein |
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

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 10 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom. |
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

<a id="table-rad"></a>
### RAD

Dimensions: 5 rows × 4 columns

| BIT | DREHRICHTUNG_TEXT | DFA_TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | E90: Drehrichtungserkennung in ECU nicht konfiguriert; E87: nicht configuriert! |  | 1 |
| 0x01 | vorwaerts | Stillstand | 2 |
| 0x02 | rueckwaerts | Fahrzeug faehrt | 3 |
| 0xFF | Signal nicht plausibel / nicht konfiguriert | keine Ausgabe | 4 |
| 0xXY | nicht_definiert | nicht_definiert | 99 |

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
| 0x01 | Routine_nicht_erfolgreich_beendet_oder_Routine_wurde_nicht_gestartet | 0 |
| 0x00 | Routine_erfolgreich_beendet | 1 |
| 0xXY | kein_Ergebnis | 99 |

<a id="table-f-can-lw"></a>
### F_CAN_LW

Dimensions: 5 rows × 4 columns

| BIT | LW_RAD_FEHLER_TEXT | LW_OBEN_FEHLER_TEXT | WERT |
| --- | --- | --- | --- |
| 0x00 | in Ordnung | in Ordnung | 1 |
| 0x01 | LWS Verifizierung | Radlenkwinkelverifizierung | 2 |
| 0x02 | LWS-Signal fehlerhaft | Lenkwinkel_Rad-Signal fehlerhaft | 3 |
| 0x03 | Signal ungueltig | Signal ungueltig | 4 |
| 0xXY | nicht_definiert | nicht_definiert | 99 |

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
