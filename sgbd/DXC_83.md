# DXC_83.prg

- Jobs: [77](#jobs)
- Tables: [28](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Dynamische Stabilitaets Control xDrive DXC_83,  E83 (ab 9 / 06)  |
| ORIGIN | BMW EF-43 Kusch |
| REVISION | 1.002 |
| AUTHOR | BMW EF-43 Kusch, MSF EEC-I Gruber |
| COMMENT | Version Robert Bosch DXC8+ KWP 2000 star  |
| PACKAGE | 1.31 |
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
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
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
- [C_C_SCHREIBEN](#job-c-c-schreiben) - Codierdaten schreiben Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [C_C_AUFTRAG](#job-c-c-auftrag) - Codierdaten schreiben und ruecklesen Standard Codierjob KWP2000: $2E   WriteDataByCommonIdentifier $3000 - $3EFF CodingDataSet KWP2000: $22   ReadDataByCommonIdentifier $3000 - $3EFF CodingDataSet Modus  : Default
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_LESEN](#job-zif-lesen) - Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_BACKUP_LESEN](#job-zif-backup-lesen) - Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [PHYSIKALISCHE_HW_NR_LESEN](#job-physikalische-hw-nr-lesen) - Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [FLASH_BLOCKLAENGE_LESEN](#job-flash-blocklaenge-lesen) - Auslesen des maximalen Blocklaenge beim Flashen KWP2000: $22   ReadDataByCommonIdentifier $2506 MaximaleBlockLaenge Modus  : Default
- [FLASH_PROGRAMMIER_STATUS_LESEN](#job-flash-programmier-status-lesen) - Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. Diag_Mode ist integriert KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [IDENT_VIN](#job-ident-vin) - Identdaten, BMW Fahrgestellnummer VIN KWP2000 star: $1A,$90 ReadECUIdentification Modus  : Default
- [IDENT_BOSCH_HW_NR](#job-ident-bosch-hw-nr) - Identdaten, SystemSupplier ECU Hardware Nr KWP2000 star: $1A,$92 ReadECUIdentification Modus  : Default
- [IDENT_BOSCH_SW_BB_NR](#job-ident-bosch-sw-bb-nr) - Identdaten Robert Bosch SG Software Nummer (BB-Nummer) KWP2000: $1A,$94 ReadECUIdentification Modus  : Default
- [IDENT_BOSCH_SW_VERSION_NR](#job-ident-bosch-sw-version-nr) - Identdaten Robert Bosch SG Softwareversionsnummer KWP2000: $1A,$95 ReadECUIdentification Modus  : Default
- [IDENT_VIN_SCHREIBEN](#job-ident-vin-schreiben) - KWP2000 star:$3B,$90 WriteDataByLocalIdentifier service Ident-Daten des SG schreiben
- [ECU_HW_NR_SCHREIBEN](#job-ecu-hw-nr-schreiben) - KWP2000 star: $3B WriteDataByLocalIdentifier $92 Hersteller ECU Hardware Nummer schreiben
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt !) Musterparametersatz: ROMI,0xFF12AB,12,Datenbytes Argumente mit "Strich_Punkt" getrennt (nicht mit Komma !) 0x04,0x05,0x0B,0x0C...Datenbytes(hex) durch Komma getrennt !) 04,05,03,11,12 ... Datenbytes(dec) durch Komma getrennt !) das High-Byte ist bei R.Bosch DXC8 immer 0xFFxxxx KWP2000 star: $3D WriteMemoryByAddress Modus  : Default
- [STATUS_ANALOG](#job-status-analog) - Status analoge Eingaenge DXC8+ KWP2000 star: $21,$02 ReadDataByLocalIdentifier service
- [STATUS_DIGITAL](#job-status-digital) - Status digitale Eingaenge DXC+ KWP2000 star: $21,$03 ReadDataByLocalIdentifier service
- [STATUS_CAN](#job-status-can) - Status CAN DSC8 KWP2000 star: $21,$04 ReadDataByLocalIdentifier service
- [STATUS_RADGESCHWINDIGKEIT](#job-status-radgeschwindigkeit) - Radgeschwindigkeiten auslesen DXC8+ KWP2000* KWP2000 star: $21,$01 ReadDataByLocalIdentifier service
- [STEUERN_VAK_BEFUELL](#job-steuern-vak-befuell) - Evakuierung und Befuellung der Parameter"R" ist optional: "R" fordert zusaetzlich ein Ergebnis-Telegramm an Musterparametersatz: E,12,6,R jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) Bsp: E,10,1,R: Routine laeuft 10 sec, 1 sec nach Start wird zusaetzlich die Pumpe eingeschaltet Bsp: E,10,8,R: Routine laeuft 10 sec, 8 sec nach Start wird zusaetzlich die Pumpe eingeschaltet Bsp: E,10,10,R oder E,10,0,R: Routine laeuft 10 sec nur mit Ventilansteuerung KWP2000 star: $30,$01 InputOutputControlByLocalIdentifier
- [STEUERN_REP_ENTLUEFTUNG](#job-steuern-rep-entlueftung) - Evakuierung und Befuellung der Parameter"R" ist optional: "R" fordert zusaetzlich ein Ergebnis-Telegramm an Musterparametersatz: E,V_links,3,R jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) KWP2000 star: $30,$02 InputOutputControlByLocalIdentifier
- [STEUERN_DREHZAHLFUEHLER_ALLE](#job-steuern-drehzahlfuehler-alle) - Test Drehzahlfuehler Musterparametersatz: 2000 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !)
- [STEUERN_ERGEBNIS_ROUTINE](#job-steuern-ergebnis-routine) - Ergebnis der Routine abholen es ist nur ein Argument zulaessig Musterparametersatz: "REP_ENTLUEFTUNG" Musterparametersatz: "VAK_BEFUELL" Musterparametersatz: "STELLGLIED" Musterparametersatz: "KUPPLUNGS_TEST "
- [STEUERN_STOP](#job-steuern-stop) - Digitale Stellglieder ansteuern ABS_DSC57 KWP2000 star: $30,$10 InputOutputControlByLocalIdentifier
- [STEUERN_D_STELLGLIED](#job-steuern-d-stellglied) - Digitale Stellglieder ansteuern KWP2000: $30,$04 InputOutputControlByLocalIdentifier Parameter (argument) koennen ausgewaehlt werden Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode,  und Ansteuersequenz-Ausfuehren: Mit dem Parameter"W" wird nur die Ansteuersequenz ausgefuehrt Der Parameter"R" ist optional: "R" fordert zusaetzlich ein Ergebnis-Telegramm an Musterparametersatz: "E,EIN,EVVL,AUS,AVVL,1000,EIN,MRA,EIN,USV1" Musterparametersatz: "E,EIN,EVVL,AUS,AVVL,1000,EIN,MRA,EIN,USV,R" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !)
- [STEUERN_DX_STELLGLIED](#job-steuern-dx-stellglied) - Digitale Stellglieder ansteuern DSC_8 Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode,  und Ansteuersequenz-Ausfuehren: Mit dem Parameter"W" wird nur die Ansteuersequenz ausgefuehrt Der Parameter"R" ist optional: "R" fordert zusaetzlich ein Ergebnis-Telegramm an KWP2000 star: $30,$04 InputOutputControlByLocalIdentifier Musterparametersatz_1: "E,EIN,0,0,USV1,USV2,EIN,0,0,0,MRA,800,AUS,0,0,USV2,USV1,EIN,EVVL,EVVR,EVHL,EVHR" Musterparametersatz_2: "W,EIN,VLV1,VLV1,VLV2,VLV2,EIN,MRA,MRA,MRA,MRA,800,AUS,USV1,USV2,USV2,USV1,EIN,AVVL,AVVL,AVVR,AVHR,R" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) es gibt 5 Stellgliedgruppen "EIN/AUS,MRA" "EIN/AUS,USV1,USV2" "EIN/AUS,VLV1,VLV2" "EIN/AUS,EVVL,EVVR,EVHL,EVHR" "EIN/AUS,AVVL,AVVR,AVHL,AVHR" in jedem Job koennen dann 4 beliebige Stellgliedgruppen angesteuert werden und zwar 2 Stellgliedgruppen vor dem Zeitglied und 2 Stellgliedgruppen nach dem Zeitglied dazwischen steht das Argument fuer die Wartezeit:  W_ZEIT in ms eine Stellgliedgruppe besteht aus 5 Argumenten: einem Befehl "EIN" oder "AUS" und aus genau 4 Stellgliedern werden weniger als 4 Stellglieder angesteuert, bzw. koennen pro Gruppe nur 1 bzw. 2 Stellglieder angesteuert werden, so sind die restlichen linksbuendig mit "0" zu besetzen(siehe Musterparametersatz_1) um Nullen zu vermeiden kann man sie auch mehrfach mit dem gleichen Stellglied besetzen (siehe Musterparametersatz_2) die Stellglieder einer Gruppen duerfen nicht mit Stellgliedern anderer Gruppen gemixt werden
- [STEUERN_STELLGLIED_DYNAMISCH](#job-steuern-stellglied-dynamisch) - Digitale Stellglieder ansteuern DSC_8 KWP2000 star: $30,$04 InputOutputControlByLocalIdentifier Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode,  und Ansteuersequenz-Ausfuehren: Mit dem Parameter"W" wird nur die Ansteuersequenz ausgefuehrt Der Parameter"R" ist optional: "R" fordert zusaetzlich ein Ergebnis-Telegramm an Musterparametersatz_1: "E,EIN,0,0,USV1,USV2,EIN,0,0,0,MRA,800,AUS,0,0,USV2,USV1,EIN,EVVL,EVVR,EVHL,EVHR,100" Musterparametersatz_2: "W,EIN,VLV1,VLV1,VLV2,VLV2,EIN,MRA,MRA,MRA,MRA,800,AUS,USV1,USV2,USV2,USV1,EIN,AVVL,AVVL,AVVR,AVHR,200,R" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) es gibt 5 Stellgliedgruppen "EIN/AUS,MRA" "EIN/AUS,USV1,USV2" "EIN/AUS,VLV1,VLV2" "EIN/AUS,EVVL,EVVR,EVHL,EVHR" "EIN/AUS,AVVL,AVVR,AVHL,AVHR" in jedem Job koennen dann 4 beliebige Stellgliedgruppen angesteuert werden und zwar 2 Stellgliedgruppen vor dem Zeitglied und 2 Stellgliedgruppen nach dem Zeitglied dazwischen steht das Argument fuer die Wartezeit:  W_ZEIT in ms eine Stellgliedgruppe besteht aus 5 Argumenten: einem Befehl "EIN" oder "AUS" und aus genau 4 Stellgliedern werden weniger als 4 Stellglieder angesteuert, bzw. koennen pro Gruppe nur 1 bzw. 2 Stellglieder angesteuert werden, so sind die restlichen linksbuendig mit "0" zu besetzen(siehe Musterparametersatz_1) um Nullen zu vermeiden kann man sie auch mehrfach mit dem gleichen Stellglied besetzen (siehe Musterparametersatz_2) die Stellglieder einer Gruppen duerfen nicht mit Stellgliedern anderer Gruppen gemixt werden
- [STEUERN_AKTUATORIK](#job-steuern-aktuatorik) - Statischer Test der Komponenten DSC_8 Musterparametersatz: 600,400 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !)
- [STEUERN_KUPPLUNG](#job-steuern-kupplung) - Digitale Stellglieder ansteuern DXC8 KWP2000 star: $31,$20 Musterparametersatz: "AKTIV" oder "PASSIV" Default ist aktiv
- [STEUERN_KUPPLUNGS_TEST](#job-steuern-kupplungs-test) - der Kupplungstest dauert ca. 10 sec im n.i.O. Fall dauert der Kupplungstest ca. 26 sec der Parameter"R" oder "r" ist optional "R" fordert zusaetzlich ein Ergebnis-Telegramm an
- [STATUS_RPA](#job-status-rpa) - KWP2000: $21,$05 ReadDataByLocalIdentifier service Modus  : Default
- [STATUS_RPA_FASTA](#job-status-rpa-fasta) - RPA Fastadaten auslesen KWP2000: $21,$06 ReadDataByLocalIdentifier service Modus  : Default
- [STATUS_RPA_STANDARDISIERUNG_1](#job-status-rpa-standardisierung-1) - Radgeschwindigkeiten auslesen KWP2000: $21,$07 ReadDataByLocalIdentifier service Modus  : Default
- [STATUS_RPA_STANDARDISIERUNG_2](#job-status-rpa-standardisierung-2) - Radgeschwindigkeiten auslesen KWP2000: $21,$08 ReadDataByLocalIdentifier service Modus  : Default
- [STATUS_RPA_STANDARDISIERUNG_3](#job-status-rpa-standardisierung-3) - Radgeschwindigkeiten auslesen erst ab DXC8 SW19 und DSC8 I5.20 KWP2000: $21,$09 ReadDataByLocalIdentifier service Modus  : Default
- [RPA_SCHREIBEN](#job-rpa-schreiben) - KWP2000: $3B WriteDataByLocalIdentifier $05 RPA schreiben
- [RPA_FASTA_LOESCHEN](#job-rpa-fasta-loeschen) - KWP2000: $3B WriteDataByLocalIdentifier $06 RPA_FASTA_loeschen
- [RPA_DEFAULT](#job-rpa-default) - KWP2000: $3B WriteDataByLocalIdentifier $06 RPA_FASTA_loeschen $07 Standardisierungdaten_1 $08 Standardisierungdaten_2 $09 Standardisierungdaten_3 Fasta- und Standardisierungsdaten auf default setzten
- [RPA_LAMPE_EINSCHALTEN](#job-rpa-lampe-einschalten) - KWP2000: $3B WriteDataByLocalIdentifier $09 Standardisierungdaten_3 Fuer USA Standardisierungsdaten auf default setzten und dazu RPA-Lampe einschalten
- [RPA_STANDARDISIERUNG_1_SCHREIBEN](#job-rpa-standardisierung-1-schreiben) - KWP2000: $3B WriteDataByLocalIdentifier $07 RPA Standardisierungsdaten_1 vorgeben
- [RPA_STANDARDISIERUNG_2_SCHREIBEN](#job-rpa-standardisierung-2-schreiben) - KWP2000: $3B WriteDataByLocalIdentifier $08 RPA Standardisierungsdaten_2 vorgeben
- [RPA_STANDARDISIERUNG_3_SCHREIBEN](#job-rpa-standardisierung-3-schreiben) - erst ab DXC8 SW19 und DSC8 I5.20 KWP2000: $3B WriteDataByLocalIdentifier $09 RPA Standardisierungsdaten_3 vorgeben
- [LENKWINKEL_DSC_ABGLEICHEN](#job-lenkwinkel-dsc-abgleichen) - KWP2000 star: $30,$08 InputOutputControlByLocalIdentifier service Musterparametersatz: 78 gueltige Zufallszahlen: 1 - 254 wird keine Zufallszahl uebergeben, dann wird eine Zufallszahl aus der Systemzeit ermittelt
- [TEST_LENKWINKEL](#job-test-lenkwinkel) - KWP2000 star: $30,$08 InputOutputControlByLocalIdentifier service Musterparametersatz: 78 gueltige Zufallszahlen: 1 - 254 wird keine Zufallszahl uebergeben, dann wird eine Zufallszahl aus der Systemzeit ermittelt
- [_FS_LESEN_SAR](#job-fs-lesen-sar) - Fehlerspeicher lesen (alle Fehler / Ort und Art) KWP2000: $18 ReadDiagnosticTroubleCodesByStatus Modus    : Default
- [_FS_LESEN_INPA](#job-fs-lesen-inpa) - KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes KWP2000: $18 ReadDiagnosticTroubleCodesByStatus kombinierter Job §17 und §18 Fehlerspeicher lesen mit allen Umweltdaten Ausgabe der Results wie INPA
- [_COD_LESEN](#job-cod-lesen) - Auslesen der Codierdaten Es muessen 2 Byte (Blocknummer) als Hex_String uebergeben werden Argument: z.B.: 30,04 KWP2000: $22 ReadDataByCommonIdentifier $300x Codierdaten Modus  : Default
- [_COD_SCHREIBEN](#job-cod-schreiben) - Codierdaten schreiben Es muessen die Codierbytes als ein Hex_String uebergeben werden, beginnend mit der Codier-Blocknummer Argument: z.B.: 30,02,A1,02,F7,65 ..... das Laengenbyte wird automatisch von der SGBD berechnet KWP2000: $2E WriteDataByCommonIdentifier $300x codingDataSet Modus  : Default
- [_COD_SCHREIBEN_ZUSATZFUNKTIONEN](#job-cod-schreiben-zusatzfunktionen) - Zusatzfunktionen auscodieren Es koennen max. 8 Argumente uebergeben werden FLR:  Fahrleistungsreduzierung HBA:  Hydraulischer Bremsassistent AY:   Offsetabgleich AY gesperrt LW:   Offsetabgleich Lenkwinkel gesperrt PSI_STAND: Offsetabgleich im Stand fuer Giergeschwindigkeit gesperrt PSI_FAHRT: Offsetabgleich waehrend der Fahrt fuer Giergeschwindigkeit gesperrt PSI_EMPF:  Empfindlichkeitsabgleich fuer Giergeschwindigkeit gesperrt SW:        Steilwandmodus aktiviert HVV:  hydraulische Vollverzögerung SST:  Softstop (default: deaktiviert) EVB:  Bremsbereitschaft BSW:  Trockenbremsen HHC:  Anfahrassistenz HPS:  Hydraulic Fading Compensation ASL:  Anhaengerschlingerlogik HDC:  Hill Descent Control Argument: z.B.: HBA,ASL jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) werden keine Argumente übergeben ist die Defaultcodierung wieder aktiv KWP2000* : $2E WriteDataByCommonIdentifier $300x codingDataSet Modus  : Default
- [_IDENT_SENSORCLUSTER_MM3_X](#job-ident-sensorcluster-mm3-x) - Auslesen des DSC Sensor-Clusters KWP2000*: $22 ReadDataByCommonIdentifier $1601 DSC Sensor-Cluster  lesen Modus    : Default
- [LAENGSBESCHLEUNIGUNG_DSC_ABGLEICHEN](#job-laengsbeschleunigung-dsc-abgleichen) - der Parameter"R" ist optional: "R" fordert zusaetzlich ein Ergebnis-Telegramm an Musterparametersatz: R mit diesem Job wird auch die MM3.x Teilenummer in die ECU eingelesen KWP2000* : $30,$0B InputOutputControlByLocalIdentifier $33,$0B RequestRoutineResultsByLocalIdentifier

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

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. Diag_Mode ist integriert KWP2000: $2E WriteDataByCommonIdentifier $1000 TestStamp Modus  : Default

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
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-ident-vin"></a>
### IDENT_VIN

Identdaten, BMW Fahrgestellnummer VIN KWP2000 star: $1A,$90 ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| FG_NR | string | Fahrgestellnummer 7-stellig |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-bosch-hw-nr"></a>
### IDENT_BOSCH_HW_NR

Identdaten, SystemSupplier ECU Hardware Nr KWP2000 star: $1A,$92 ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_TT_NR | string | RB-Teilenummer |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-bosch-sw-bb-nr"></a>
### IDENT_BOSCH_SW_BB_NR

Identdaten Robert Bosch SG Software Nummer (BB-Nummer) KWP2000: $1A,$94 ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BB_NR_AS | string | RB-BB-Nummer Algorithm Server |
| ID_BB_NR_SS | string | RB-BB-Nummer System Server |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-bosch-sw-version-nr"></a>
### IDENT_BOSCH_SW_VERSION_NR

Identdaten Robert Bosch SG Softwareversionsnummer KWP2000: $1A,$95 ReadECUIdentification Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_RB_SW_NR_AS | string | RB-SW-Nummer Algorithm Server |
| ID_RB_SW_NR_SS | string | RB-SW-Nummer System Server |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-vin-schreiben"></a>
### IDENT_VIN_SCHREIBEN

KWP2000 star:$3B,$90 WriteDataByLocalIdentifier service Ident-Daten des SG schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FG_NR | string | Fahrgestellnummer (8-stellig) Es muss 1 String mit 8 Zeichen uebergeben werden das letzte Zeichen ist ein Dummy z.B. JR250001 FG_NR: JR25000 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |

<a id="job-ecu-hw-nr-schreiben"></a>
### ECU_HW_NR_SCHREIBEN

KWP2000 star: $3B WriteDataByLocalIdentifier $92 Hersteller ECU Hardware Nummer schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATAS | string | Es muessen 5 Ident_Daten als ein Hex_String uebergeben werden: z.B. 01,AB,56,FF ... 18 Bereich:  0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Beschreiben des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse, Anzahl der Datenbytes und Datenbytes (Datenbytes durch Komma getrennt !) Musterparametersatz: ROMI,0xFF12AB,12,Datenbytes Argumente mit "Strich_Punkt" getrennt (nicht mit Komma !) 0x04,0x05,0x0B,0x0C...Datenbytes(hex) durch Komma getrennt !) 04,05,03,11,12 ... Datenbytes(dec) durch Komma getrennt !) das High-Byte ist bei R.Bosch DXC8 immer 0xFFxxxx KWP2000 star: $3D WriteMemoryByAddress Modus  : Default

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
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-analog"></a>
### STATUS_ANALOG

Status analoge Eingaenge DXC8+ KWP2000 star: $21,$02 ReadDataByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_LENKWINKEL_WERT | real | Lenkwinkel in Grad, kann + u.- Wert haben |
| STAT_LENKWINKEL_EINH | string | Einheit = Winkelgrad |
| STAT_DREHRATE_WERT | real | Drehrate in Winkelgrad/sec |
| STAT_DREHRATE_EINH | string | Einheit = Winkelgrad/sec |
| STAT_DRUCK_WERT | real | Druck in bar, kann + u.- Wert haben |
| STAT_DRUCK_EINH | string | Einheit = bar |
| STAT_QUERBESCHLEUNIGUNG_WERT | real | Querbeschleunigung , kann + u.- Wert haben |
| STAT_QUERBESCHLEUNIGUNG_EINH | string | Einheit = m/(s*s) |
| STAT_LAENGSBESCHLEUNIGUNG_WERT | real | Einheit = m/(s*s) |
| STAT_LAENGSBESCHLEUNIGUNG_EINH | string | Einheit = m/(s*s) |
| STAT_VENTILRELAIS_SPANNUNG_WERT | real | Spannung Kl. 15 in V |
| STAT_VENTILRELAIS_SPANNUNG_EINH | string | Einheit = V |
| STAT_ZUENDUNG_WERT | real | Spannung Kl. 15 in V |
| STAT_ZUENDUNG_EINH | string | Einheit = V |
| STAT_PUMPENMOTOR_SPANNUNG_WERT | real | Spannung Pumpenmotor in Volt |
| STAT_PUMPENMOTOR_SPANNUNG_EINH | string | Einheit = V |
| _TEL_AUFTRAG | binary | Anforderungstelegrammn SG |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status digitale Eingaenge DXC+ KWP2000 star: $21,$03 ReadDataByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_BREMSLICHTSCHALTER_EIN | int | 0 oder 1 |
| STAT_SCHALTER_BREMSFLUESSIGKEIT_NIVEAU_EIN | int | 0 oder 1 |
| STAT_HANDBREMSSCHALTER_EIN | int | 0 oder 1 |
| STAT_DSC_PASSIVTASTER_EIN | int | 0 oder 1 |
| STAT_DTC_EIN | int | 0 oder 1 |
| STAT_HILLDESCENT_EIN | int | 0 oder 1 |
| STAT_INFO_LAMPE | int | 0 oder 1 |
| STAT_ABS_SILA | int | 0 oder 1 |
| STAT_DSC_SILA | int | 0 oder 1 |
| STAT_DSC_PASSIVLAMPE | int | 0 oder 1 |
| STAT_EDB_SILA | int | 0 oder 1 |
| STAT_EVVL_EIN | int | 0 oder 1 |
| STAT_AVVL_EIN | int | 0 oder 1 |
| STAT_EVHR_EIN | int | 0 oder 1 |
| STAT_AVHR_EIN | int | 0 oder 1 |
| STAT_EVVR_EIN | int | 0 oder 1 |
| STAT_AVVR_EIN | int | 0 oder 1 |
| STAT_EVHL_EIN | int | 0 oder 1 |
| STAT_AVHL_EIN | int | 0 oder 1 |
| STAT_UMSCHALTVENTIL_VORDERACHSE_EIN | int | 0 oder 1 |
| STAT_UMSCHALTVENTIL_HINTERACHSE_EIN | int | 0 oder 1 |
| STAT_VORLADEVENTIL_VORDERACHSE_EIN | int | 0 oder 1 |
| STAT_VORLADEVENTIL_HINTERACHSE_EIN | int | 0 oder 1 |
| STAT_PUMPENMOTOR_EIN | int | 0 oder 1 |
| STAT_VENTIL_RELAIS_EIN | int | 0 oder 1 |
| _TEL_AUFTRAG | binary | Anforderungstelegrammn SG |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-can"></a>
### STATUS_CAN

Status CAN DSC8 KWP2000 star: $21,$04 ReadDataByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, FEHLER |
| STAT_MOTORDREHZAHL_WERT | real | Momentane Motordrehzahl in 1/min |
| STAT_MOTORDREHZAHL_EINH | string | Einheit = 1/min |
| STAT_DREHMOMENT_WERT | real | Drehmoment [Nm] |
| STAT_DREHMOMENT_EINH | string | [Nm] |
| STAT_KUPPLUNG_WERT | real | Kupplungsmoment [Nm] |
| STAT_KUPPLUNG_EINH | string | [Nm] |
| STAT_FAHRZUSTAND | string | Text |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-status-radgeschwindigkeit"></a>
### STATUS_RADGESCHWINDIGKEIT

Radgeschwindigkeiten auslesen DXC8+ KWP2000* KWP2000 star: $21,$01 ReadDataByLocalIdentifier service

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_RAD_GESCHW_VL_WERT | long | Radgeschwindigkeit vorne links |
| STAT_RAD_GESCHW_VR_WERT | long | Radgeschwindigkeit vorne rechts |
| STAT_RAD_GESCHW_HL_WERT | long | Radgeschwindigkeit hinten links |
| STAT_RAD_GESCHW_HR_WERT | long | Radgeschwindigkeit hinten rechts |
| STAT_RAD_GESCHW_REF_WERT | long | Fahrzeug-Referenz-Geschwindigkeit |
| STAT_RAD_GESCHW_EINH | string | Einheit = km/h |
| STAT_DREHRICHTUNG_VL_TEXT | string | Drehrichtung vorne links |
| STAT_DREHRICHTUNG_VL_WERT | int | Drehrichtung vorne links |
| STAT_DREHRICHTUNG_VR_TEXT | string | Drehrichtung vorne rechts |
| STAT_DREHRICHTUNG_VR_WERT | int | Drehrichtung vorne rechts |
| STAT_DREHRICHTUNG_HL_TEXT | string | Drehrichtung hinten links |
| STAT_DREHRICHTUNG_HL_WERT | int | Drehrichtung hinten links |
| STAT_DREHRICHTUNG_HR_TEXT | string | Drehrichtung hinten rechts |
| STAT_DREHRICHTUNG_HR_WERT | int | Drehrichtung hinten rechts |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-steuern-vak-befuell"></a>
### STEUERN_VAK_BEFUELL

Evakuierung und Befuellung der Parameter"R" ist optional: "R" fordert zusaetzlich ein Ergebnis-Telegramm an Musterparametersatz: E,12,6,R jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) Bsp: E,10,1,R: Routine laeuft 10 sec, 1 sec nach Start wird zusaetzlich die Pumpe eingeschaltet Bsp: E,10,8,R: Routine laeuft 10 sec, 8 sec nach Start wird zusaetzlich die Pumpe eingeschaltet Bsp: E,10,10,R oder E,10,0,R: Routine laeuft 10 sec nur mit Ventilansteuerung KWP2000 star: $30,$01 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| ZEIT_ROUTINE | int |  |
| DELAY_PUMPE | int |  |
| ERGEBNIS | string | Default: Ergebnis nicht abholen. Wenn Argument &lt;Ergebnis&gt; vorhanden, dann Ergebnis abholen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_ERGEBNIS_BYTE | string | Text |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_AUFTRAG_2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |

<a id="job-steuern-rep-entlueftung"></a>
### STEUERN_REP_ENTLUEFTUNG

Evakuierung und Befuellung der Parameter"R" ist optional: "R" fordert zusaetzlich ein Ergebnis-Telegramm an Musterparametersatz: E,V_links,3,R jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) KWP2000 star: $30,$02 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| RAD_NR | string |  |
| WIEDERHOLUNG | int |  |
| ERGEBNIS | string | Default: Ergebnis nicht abholen. Wenn Argument &lt;Ergebnis&gt; vorhanden, dann Ergebnis abholen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ERGEBNIS_BYTE | string | Text |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_AUFTRAG_2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |

<a id="job-steuern-drehzahlfuehler-alle"></a>
### STEUERN_DREHZAHLFUEHLER_ALLE

Test Drehzahlfuehler Musterparametersatz: 2000 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| A_ZEIT | int | Ausfuehrungszeit in ms |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_RAD_GESCHW_VL_MIN | long | Radgeschwindigkeit waehrend Test |
| STAT_RAD_GESCHW_VL_MAX | long | Radgeschwindigkeit waehrend Test |
| STAT_RAD_GESCHW_VR_MIN | long | Radgeschwindigkeit waehrend Test |
| STAT_RAD_GESCHW_VR_MAX | long | Radgeschwindigkeit waehrend Test |
| STAT_RAD_GESCHW_HL_MIN | long | Radgeschwindigkeit waehrend Test |
| STAT_RAD_GESCHW_HL_MAX | long | Radgeschwindigkeit waehrend Test |
| STAT_RAD_GESCHW_HR_MIN | long | Radgeschwindigkeit waehrend Test |
| STAT_RAD_GESCHW_HR_MAX | long | Radgeschwindigkeit waehrend Test |
| GESCHW_EINH | string | Einheit = km/h |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_AUFTRAG_2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |

<a id="job-steuern-ergebnis-routine"></a>
### STEUERN_ERGEBNIS_ROUTINE

Ergebnis der Routine abholen es ist nur ein Argument zulaessig Musterparametersatz: "REP_ENTLUEFTUNG" Musterparametersatz: "VAK_BEFUELL" Musterparametersatz: "STELLGLIED" Musterparametersatz: "KUPPLUNGS_TEST "

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TYP | string | Typ der Routine angeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_ERGEBNIS_BYTE | string | Text |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |

<a id="job-steuern-stop"></a>
### STEUERN_STOP

Digitale Stellglieder ansteuern ABS_DSC57 KWP2000 star: $30,$10 InputOutputControlByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT1 | binary | Antworttelegramm |

<a id="job-steuern-d-stellglied"></a>
### STEUERN_D_STELLGLIED

Digitale Stellglieder ansteuern KWP2000: $30,$04 InputOutputControlByLocalIdentifier Parameter (argument) koennen ausgewaehlt werden Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode,  und Ansteuersequenz-Ausfuehren: Mit dem Parameter"W" wird nur die Ansteuersequenz ausgefuehrt Der Parameter"R" ist optional: "R" fordert zusaetzlich ein Ergebnis-Telegramm an Musterparametersatz: "E,EIN,EVVL,AUS,AVVL,1000,EIN,MRA,EIN,USV1" Musterparametersatz: "E,EIN,EVVL,AUS,AVVL,1000,EIN,MRA,EIN,USV,R" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| BEFEHL_1 | string | Ein = 64, Aus = 00 |
| ST_1 | string | Stellglied 1 |
| BEFEHL_2 | string | Ein = 64, Aus = 00 |
| ST_2 | string | Stellglied 2 |
| W_ZEIT | int | Wartezeit vor Ansteuerung 3. u. 4. Stellglied |
| BEFEHL_3 | string | Ein = 64, Aus = 00 |
| ST_3 | string | Stellglied 3 |
| BEFEHL_4 | string | Ein = 64, Aus = 00 |
| ST_4 | string | Stellglied 4 |
| ERGEBNIS | string | Default: Ergebnis nicht abholen. Wenn Argument &lt;Ergebnis&gt; vorhanden, dann Ergebnis abholen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |
| _TEL_AUFTRAG_2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |

<a id="job-steuern-dx-stellglied"></a>
### STEUERN_DX_STELLGLIED

Digitale Stellglieder ansteuern DSC_8 Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode,  und Ansteuersequenz-Ausfuehren: Mit dem Parameter"W" wird nur die Ansteuersequenz ausgefuehrt Der Parameter"R" ist optional: "R" fordert zusaetzlich ein Ergebnis-Telegramm an KWP2000 star: $30,$04 InputOutputControlByLocalIdentifier Musterparametersatz_1: "E,EIN,0,0,USV1,USV2,EIN,0,0,0,MRA,800,AUS,0,0,USV2,USV1,EIN,EVVL,EVVR,EVHL,EVHR" Musterparametersatz_2: "W,EIN,VLV1,VLV1,VLV2,VLV2,EIN,MRA,MRA,MRA,MRA,800,AUS,USV1,USV2,USV2,USV1,EIN,AVVL,AVVL,AVVR,AVHR,R" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) es gibt 5 Stellgliedgruppen "EIN/AUS,MRA" "EIN/AUS,USV1,USV2" "EIN/AUS,VLV1,VLV2" "EIN/AUS,EVVL,EVVR,EVHL,EVHR" "EIN/AUS,AVVL,AVVR,AVHL,AVHR" in jedem Job koennen dann 4 beliebige Stellgliedgruppen angesteuert werden und zwar 2 Stellgliedgruppen vor dem Zeitglied und 2 Stellgliedgruppen nach dem Zeitglied dazwischen steht das Argument fuer die Wartezeit:  W_ZEIT in ms eine Stellgliedgruppe besteht aus 5 Argumenten: einem Befehl "EIN" oder "AUS" und aus genau 4 Stellgliedern werden weniger als 4 Stellglieder angesteuert, bzw. koennen pro Gruppe nur 1 bzw. 2 Stellglieder angesteuert werden, so sind die restlichen linksbuendig mit "0" zu besetzen(siehe Musterparametersatz_1) um Nullen zu vermeiden kann man sie auch mehrfach mit dem gleichen Stellglied besetzen (siehe Musterparametersatz_2) die Stellglieder einer Gruppen duerfen nicht mit Stellgliedern anderer Gruppen gemixt werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| BEFEHL_1 | string |  |
| ST_1 | string | Stellglied 1 |
| ST_2 | string | Stellglied 2 |
| ST_3 | string | Stellglied 3 |
| ST_4 | string | Stellglied 4 |
| BEFEHL_2 | string |  |
| ST_5 | string | Stellglied 5 |
| ST_6 | string | Stellglied 6 |
| ST_7 | string | Stellglied 7 |
| ST_8 | string | Stellglied 8 |
| W_ZEIT | int | Wartezeit vor Ansteuerung  Stellglied 5-8 |
| BEFEHL_3 | string |  |
| ST_9 | string | Stellglied 5 |
| ST_10 | string | Stellglied 5 |
| ST_11 | string | Stellglied 6 |
| ST_12 | string | Stellglied 7 |
| BEFEHL_4 | string |  |
| ST_13 | string | Stellglied 8 |
| ST_14 | string | Stellglied 5 |
| ST_15 | string | Stellglied 6 |
| ST_16 | string | Stellglied 7 |
| ERGEBNIS | string | Default: Ergebnis nicht abholen. Wenn Argument &lt;Ergebnis&gt; vorhanden, dann Ergebnis abholen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |
| _TEL_AUFTRAG_2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |

<a id="job-steuern-stellglied-dynamisch"></a>
### STEUERN_STELLGLIED_DYNAMISCH

Digitale Stellglieder ansteuern DSC_8 KWP2000 star: $30,$04 InputOutputControlByLocalIdentifier Mit dem Parameter"E" werden 2 Telegramme gesendet Diagnose_Mode,  und Ansteuersequenz-Ausfuehren: Mit dem Parameter"W" wird nur die Ansteuersequenz ausgefuehrt Der Parameter"R" ist optional: "R" fordert zusaetzlich ein Ergebnis-Telegramm an Musterparametersatz_1: "E,EIN,0,0,USV1,USV2,EIN,0,0,0,MRA,800,AUS,0,0,USV2,USV1,EIN,EVVL,EVVR,EVHL,EVHR,100" Musterparametersatz_2: "W,EIN,VLV1,VLV1,VLV2,VLV2,EIN,MRA,MRA,MRA,MRA,800,AUS,USV1,USV2,USV2,USV1,EIN,AVVL,AVVL,AVVR,AVHR,200,R" jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) es gibt 5 Stellgliedgruppen "EIN/AUS,MRA" "EIN/AUS,USV1,USV2" "EIN/AUS,VLV1,VLV2" "EIN/AUS,EVVL,EVVR,EVHL,EVHR" "EIN/AUS,AVVL,AVVR,AVHL,AVHR" in jedem Job koennen dann 4 beliebige Stellgliedgruppen angesteuert werden und zwar 2 Stellgliedgruppen vor dem Zeitglied und 2 Stellgliedgruppen nach dem Zeitglied dazwischen steht das Argument fuer die Wartezeit:  W_ZEIT in ms eine Stellgliedgruppe besteht aus 5 Argumenten: einem Befehl "EIN" oder "AUS" und aus genau 4 Stellgliedern werden weniger als 4 Stellglieder angesteuert, bzw. koennen pro Gruppe nur 1 bzw. 2 Stellglieder angesteuert werden, so sind die restlichen linksbuendig mit "0" zu besetzen(siehe Musterparametersatz_1) um Nullen zu vermeiden kann man sie auch mehrfach mit dem gleichen Stellglied besetzen (siehe Musterparametersatz_2) die Stellglieder einer Gruppen duerfen nicht mit Stellgliedern anderer Gruppen gemixt werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| E_OR_W | string | Einmal = E, Wiederholung = W |
| BEFEHL_1 | string |  |
| ST_1 | string | Stellglied 1 |
| ST_2 | string | Stellglied 2 |
| ST_3 | string | Stellglied 3 |
| ST_4 | string | Stellglied 4 |
| BEFEHL_2 | string |  |
| ST_5 | string | Stellglied 5 |
| ST_6 | string | Stellglied 6 |
| ST_7 | string | Stellglied 7 |
| ST_8 | string | Stellglied 8 |
| W_ZEIT_1 | int | Wartezeit nach der Ansteuerung der Stellglieder 1-8 |
| BEFEHL_3 | string |  |
| ST_9 | string | Stellglied 9 |
| ST_10 | string | Stellglied 10 |
| ST_11 | string | Stellglied 11 |
| ST_12 | string | Stellglied 12 |
| BEFEHL_4 | string |  |
| ST_13 | string | Stellglied 13 |
| ST_14 | string | Stellglied 14 |
| ST_15 | string | Stellglied 15 |
| ST_16 | string | Stellglied 16 |
| W_ZEIT_2 | int | Wartezeit nach der Ansteuerung der Stellglieder 9-16 |
| ERGEBNIS | string | Default: Ergebnis nicht abholen. Wenn Argument &lt;Ergebnis&gt; vorhanden, dann Ergebnis abholen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DELTA_RAD_GESCHW_VL_WERT | long | Radgeschwindigkeitsdifferenz vorne links |
| STAT_DELTA_RAD_GESCHW_VR_WERT | long | Radgeschwindigkeitsdifferenz vorne rechts |
| STAT_DELTA_RAD_GESCHW_HL_WERT | long | Radgeschwindigkeitsdifferenz hinten links |
| STAT_DELTA_RAD_GESCHW_HR_WERT | long | Radgeschwindigkeitsdifferenz hinten rechts |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |
| _TEL_AUFTRAG_2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |

<a id="job-steuern-aktuatorik"></a>
### STEUERN_AKTUATORIK

Statischer Test der Komponenten DSC_8 Musterparametersatz: 600,400 jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| USV_ZEIT | int | Ausfuehrungszeit in ms: t &gt;= 400ms Verzoegerungszeit bis zur Aktivierung der USVs |
| PUMPE_ZEIT | int | Ausfuehrungszeit in ms: t &gt;= 200ms Verzoegerungszeit zwischen der Aktivierung der USVs und Abschalten des Pumpenmotors |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ABFALLZEIT_1 | int | Wartezeit in msec |
| ABFALLZEIT_2 | int | Wartezeit in msec |
| ABFALLZEIT_3 | int | Wartezeit in msec |
| WARTEZEIT_EINH | string | Einheit = msec |
| _TEL_AUFTRAG | binary | Antworttelegramm |
| _TEL_AUFTRAG_2 | binary | Antworttelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |

<a id="job-steuern-kupplung"></a>
### STEUERN_KUPPLUNG

Digitale Stellglieder ansteuern DXC8 KWP2000 star: $31,$20 Musterparametersatz: "AKTIV" oder "PASSIV" Default ist aktiv

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ARG_1 | string | "AKTIV" oder "PASSIV" Default ist aktiv |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ERGEBNIS_BYTE | string | Text |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Antworttelegramm |

<a id="job-steuern-kupplungs-test"></a>
### STEUERN_KUPPLUNGS_TEST

der Kupplungstest dauert ca. 10 sec im n.i.O. Fall dauert der Kupplungstest ca. 26 sec der Parameter"R" oder "r" ist optional "R" fordert zusaetzlich ein Ergebnis-Telegramm an

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ERGEBNIS | string | Default: Ergebnis nicht abholen. Wenn Argument &lt;Ergebnis&gt; vorhanden, dann Ergebnis abholen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| STAT_ERGEBNIS_BYTE | string | Text |
| _TEL_AUFTRAG_1 | binary | Anforderungstelegramm |
| _TEL_AUFTRAG_2 | binary | Anforderungstelegramm |
| _TEL_ANTWORT_1 | binary | Antworttelegramm |
| _TEL_ANTWORT_2 | binary | Antworttelegramm |

<a id="job-status-rpa"></a>
### STATUS_RPA

KWP2000: $21,$05 ReadDataByLocalIdentifier service Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STANDARDISIERUNG_AKTIV | int | Standardisierung aktiv/inaktiv |
| STAT_WARNUNG_AKTIV | int | Warnung aktiv/inaktiv |
| STAT_REJECTION_PHASE | int | Rejection Phase |
| STAT_SYSTEMFUNKTION_AKTIV | int | Systemfunktion aktiv/inaktiv |
| STAT_BLINDPHASE_AKTIV | int | Blindphase aktiv/inaktiv |
| STAT_BREMSLICHTSCHALTER_TEXT | string | Bremslichtschalter aktiv/inaktiv/defekt |
| STAT_WEGSTRECKE | long | Delta Wegstrecke seit letzter Standardisierung |
| STAT_DSC_SIGNAL_VL | int | Rohsignal vom DSC / ABS VL (Impulse/sec) |
| STAT_DSC_SIGNAL_VR | int | Rohsignal vom DSC / ABS VR (Impulse/sec) |
| STAT_DSC_SIGNAL_HL | int | Rohsignal vom DSC / ABS HL (Impulse/sec) |
| STAT_DSC_SIGNAL_HR | int | Rohsignal vom DSC / ABS HR (Impulse/sec) |
| STAT_BEREICH_0 | int | Status der Standardisierung (15 = abgeschlossen) |
| STAT_BEREICH_1 | int | Status der Standardisierung im Bereich von 25 - 110 km/h (15 = abgeschlossen) |
| STAT_BEREICH_2 | int | Status der Standardisierung im Bereich von 110 - 135 km/h (15 = abgeschlossen) |
| STAT_BEREICH_3 | int | Status der Standardisierung im Bereich von 135 - 160 km/h (15 = abgeschlossen) |
| STAT_BEREICH_4 | int | Status der Standardisierung im Bereich von 160 - 185 km/h (15 = abgeschlossen) |
| STAT_BEREICH_5 | int | Status der Standardisierung im Bereich von 185 - 210 km/h (15 = abgeschlossen) |
| STAT_BEREICH_6 | int | Status der Standardisierung im Bereich &gt;210 km/h (15 = abgeschlossen) |
| STAT_L1 | int | Lernstati 1 fuer VS-22 |
| STAT_L1_EINH | string | Einheit Lernstati 1= % |
| STAT_L2 | int | Lernstati 2 fuer VS-22 |
| STAT_L2_EINH | string | Einheit Lernstati 2= % |
| STAT_L3 | int | Lernstati 3 fuer VS-22 |
| STAT_L3_EINH | string | Einheit Lernstati 3= % |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rpa-fasta"></a>
### STATUS_RPA_FASTA

RPA Fastadaten auslesen KWP2000: $21,$06 ReadDataByLocalIdentifier service Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_GESCHWINDIGKEIT_MAX_VORLETZTE_PANNE | long | Einheit km/h Maximale Geschwindigkeit waehrend vorletzter Reifenpannenmeldung (max 255km/h) |
| STAT_GESCHWINDIGKEIT_MAX_LETZTE_PANNE | long | Einheit km/h Maximale Geschwindigkeit waehrend letzter Reifenpannenmeldung (max 255km/h) |
| STAT_WEG_VORLETZTE_PANNE_TEXT | string | Text zur Gesamwegstrecke waehrend vorletzter Panne |
| STAT_WEG_VORLETZTE_PANNE | long | Gesamtwegstrecke waehrend vorletzter Panne |
| STAT_WEG_LETZTE_PANNE_TEXT | string | Text zur Gesamwegstrecke waehrend letzter Panne |
| STAT_WEG_LETZTE_PANNE | long | Gesamtwegstrecke waehrend letzter Panne |
| STAT_GESCHWINDIGKEIT_INDIK | long | Einheit km/h Geschwindigkeitsindikator gemessen ab erster Reifenpannenmeldung |
| STAT_KM_LETZTE_PANNE | long | Km-Stand gelesen bei letzter Reifenpannenmeldung |
| STAT_KM_VORLETZTE_PANNE | long | Km-Stand gelesen bei vorletzter Reifenpannenmeldung |
| STAT_GESCHWINDIGKEIT_VORLETZTE_PANNE | long | Einheit km/h Geschwindigkeit waehrend vorletzter Reifenpannenmeldung |
| STAT_GESCHWINDIGKEIT_LETZTE_PANNE | long | Einheit km/h Geschwindigkeit waehrend letzter Reifenpannenmeldung |
| STAT_KM_LETZTE_STANDARDISIERUNG | long | Km-Stand gelesen bei letzter Standardisierung |
| STAT_TAGE_SEIT_STANDARDISIERUNG | string | Einheit Tage Anzahl Tage gemessen seit letztem Standardisierungsstart |
| STAT_TAGE_SEIT_LETZTER_PANNE | string | Einheit Tage Anzahl Tage gemessen zwischem letztem Standardisierungsstart und Panne danach |
| STAT_TAGE_SEIT_VORLETZTER_PANNE | string | Einheit Tage Anzahl Tage gemessen zwischem letztem/vorletzter Panne und Standardisierungsstart danach |
| STAT_RPA_REV_ACTUAL | string | -- aktuelle Versionsnummer RPA |
| STAT_RPA_REV_AT_LASTCODING | string | -- Versionsnummer RPA zum Zeitpunkt der letzten Codierung |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rpa-standardisierung-1"></a>
### STATUS_RPA_STANDARDISIERUNG_1

Radgeschwindigkeiten auslesen KWP2000: $21,$07 ReadDataByLocalIdentifier service Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FACLF | real | - |
| STAT_FACLR | real | - |
| STAT_FACH1F | real | - |
| STAT_FACH1R | real | - |
| STAT_FACH2F | real | - |
| STAT_FACH2R | real | - |
| STAT_CRC | real | - |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rpa-standardisierung-2"></a>
### STATUS_RPA_STANDARDISIERUNG_2

Radgeschwindigkeiten auslesen KWP2000: $21,$08 ReadDataByLocalIdentifier service Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FACH3F | real | - |
| STAT_FACH3R | real | - |
| STAT_FACH4F | real | - |
| STAT_FACH4R | real | - |
| STAT_FACH5F | real | - |
| STAT_FACH5R | real | - |
| STAT_CRC | real | - |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rpa-standardisierung-3"></a>
### STATUS_RPA_STANDARDISIERUNG_3

Radgeschwindigkeiten auslesen erst ab DXC8 SW19 und DSC8 I5.20 KWP2000: $21,$09 ReadDataByLocalIdentifier service Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FAC3 | real | - |
| STAT_STDCNT1 | real | - |
| STAT_OUTCNT | real | - |
| STAT_NSF1 | real | - |
| STAT_NSF2 | real | - |
| STAT_NSVH5 | real | - |
| STAT_NSVH4 | real | - |
| STAT_NSVH3 | real | - |
| STAT_NSVH2 | real | - |
| STAT_NSVH1 | real | - |
| STAT_NSVL | real | - |
| STAT_WGFLG | real | - |
| STAT_CRC | real | - |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-rpa-schreiben"></a>
### RPA_SCHREIBEN

KWP2000: $3B WriteDataByLocalIdentifier $05 RPA schreiben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATAS | string | Es muss 1 Byte uebergeben werden 00 keine Aktion oder 01 Standardisierung |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-rpa-fasta-loeschen"></a>
### RPA_FASTA_LOESCHEN

KWP2000: $3B WriteDataByLocalIdentifier $06 RPA_FASTA_loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-rpa-default"></a>
### RPA_DEFAULT

KWP2000: $3B WriteDataByLocalIdentifier $06 RPA_FASTA_loeschen $07 Standardisierungdaten_1 $08 Standardisierungdaten_2 $09 Standardisierungdaten_3 Fasta- und Standardisierungsdaten auf default setzten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag ans SG |
| _TEL_AUFTRAG3 | binary | Hex-Auftrag ans SG |
| _TEL_AUFTRAG4 | binary | Hex-Auftrag ans SG |
| _TEL_AUFTRAG5 | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort vom SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort vom SG |
| _TEL_ANTWORT3 | binary | Hex-Antwort vom SG |
| _TEL_ANTWORT4 | binary | Hex-Antwort vom SG |
| _TEL_ANTWORT5 | binary | Hex-Antwort vom SG |

<a id="job-rpa-lampe-einschalten"></a>
### RPA_LAMPE_EINSCHALTEN

KWP2000: $3B WriteDataByLocalIdentifier $09 Standardisierungdaten_3 Fuer USA Standardisierungsdaten auf default setzten und dazu RPA-Lampe einschalten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT1 | binary | Antwort |
| _TEL_ANTWORT2 | binary | Antwort |

<a id="job-rpa-standardisierung-1-schreiben"></a>
### RPA_STANDARDISIERUNG_1_SCHREIBEN

KWP2000: $3B WriteDataByLocalIdentifier $07 RPA Standardisierungsdaten_1 vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATAS | string | Es muessen 25 Ident_Daten als ein Hex_String uebergeben werden: z.B. 01,AB,56,FF ... 18 Bereich:  0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-rpa-standardisierung-2-schreiben"></a>
### RPA_STANDARDISIERUNG_2_SCHREIBEN

KWP2000: $3B WriteDataByLocalIdentifier $08 RPA Standardisierungsdaten_2 vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATAS | string | Es muessen 25 Ident_Daten als ein Hex_String uebergeben werden: z.B. 01,AB,56,FF ... 18 Bereich:  0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-rpa-standardisierung-3-schreiben"></a>
### RPA_STANDARDISIERUNG_3_SCHREIBEN

erst ab DXC8 SW19 und DSC8 I5.20 KWP2000: $3B WriteDataByLocalIdentifier $09 RPA Standardisierungsdaten_3 vorgeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DATAS | string | Es muessen 22 Ident_Daten als ein Hex_String uebergeben werden: z.B. 01,AB,56,FF ... 18 Bereich:  0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT1 | binary | Hex-Antwort von SG |

<a id="job-lenkwinkel-dsc-abgleichen"></a>
### LENKWINKEL_DSC_ABGLEICHEN

KWP2000 star: $30,$08 InputOutputControlByLocalIdentifier service Musterparametersatz: 78 gueltige Zufallszahlen: 1 - 254 wird keine Zufallszahl uebergeben, dann wird eine Zufallszahl aus der Systemzeit ermittelt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LFD_NR | int | laufende Nummer bzw. Zufallszahl fuer Eintrag ins LW-SG |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_AUFTRAG_1 | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_4 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_5 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_6 | binary | Hex-Antwort von SG |
| ABGL_LWS_ID | int | Abgleichswert LWS ID |
| STATUS_ABGLEICH_1 | binary | Fehlerstatus LWS |
| STATUS_ABGLEICH_2 | binary | Fehlerstatus LWS |
| STATUS_ABGLEICH_3 | binary | Fehlerstatus LWS |
| STATUS_ABGLEICH_4 | binary | Fehlerstatus LWS |
| STAT_ERGEBNIS_BYTE | string | Text |

<a id="job-test-lenkwinkel"></a>
### TEST_LENKWINKEL

KWP2000 star: $30,$08 InputOutputControlByLocalIdentifier service Musterparametersatz: 78 gueltige Zufallszahlen: 1 - 254 wird keine Zufallszahl uebergeben, dann wird eine Zufallszahl aus der Systemzeit ermittelt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LFD_NR | int | laufende Nummer bzw. Zufallszahl fuer Eintrag ins LW-SG |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_AUFTRAG_1 | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_1 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_4 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_5 | binary | Hex-Antwort von SG |
| _TEL_ANTWORT_6 | binary | Hex-Antwort von SG |
| ABGL_LWS_ID | int | Abgleichswert LWS ID |
| STATUS_ABGLEICH_1 | binary | Fehlerstatus LWS |
| STATUS_ABGLEICH_2 | binary | Fehlerstatus LWS |
| STATUS_ABGLEICH_3 | binary | Fehlerstatus LWS |
| STATUS_ABGLEICH_4 | binary | Fehlerstatus LWS |
| STAT_ERGEBNIS_BYTE | binary | Status Lenkwinkelabgleich |

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
| HAEUFIGKZAEHLER | int | Haufigkeitszaehler als Zahl Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| LOGISTIKZAEHLER | int | Logistikzaehler als Zahl Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| KILOMETERSTAND_KM | long | Umweltbedingung Kilometerstand Wertebereich: 0 - 524280 km |
| GESCHWINDIGKEIT_KMH | long | Radgeschwindigkeit vRef |
| ACB_ACTIVE_CONTROL_BRAKE | int |  |
| DBC_DYNAMIC_BRAKE_CONTROL | int |  |
| ECD_VERZOEGERUNGSANFORDERUNG_ACC | int |  |
| HDC_HILL_DESCENT_CONTROL | int |  |
| DSC_DYNAMIC_STABILITY_CONTROL | int |  |
| ABS_ANTI_BLOCKIER_SYSTEM | int |  |
| BLS_BREMSLICHTSCHALTER | int |  |
| ASC_AUTOMATIC_STABILITY_CONTROL | int |  |

<a id="job-cod-lesen"></a>
### _COD_LESEN

Auslesen der Codierdaten Es muessen 2 Byte (Blocknummer) als Hex_String uebergeben werden Argument: z.B.: 30,04 KWP2000: $22 ReadDataByCommonIdentifier $300x Codierdaten Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| C_BLOCK | string | Codierblock 30,00 ... 30,05 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| RPA_EQUIP | string | Bereich: 0-255 bzw. 0x00-0xFF Equipment: 1 = aktiv, 0 = inaktiv |
| RPA_VARIANTE_LAND | string | Bereich: 0-255 bzw. 0x00-0xFF 1 = USA, 0 = Rest der Welt (RdW) |
| STAT_CAR_ID | int | OKAY, wenn fehlerfrei |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| CODIERBYTES | binary | ausgelesene Codier-Daten |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-cod-schreiben"></a>
### _COD_SCHREIBEN

Codierdaten schreiben Es muessen die Codierbytes als ein Hex_String uebergeben werden, beginnend mit der Codier-Blocknummer Argument: z.B.: 30,02,A1,02,F7,65 ..... das Laengenbyte wird automatisch von der SGBD berechnet KWP2000: $2E WriteDataByCommonIdentifier $300x codingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| C_BYTES | string | Block-Nr und Codierbytes: 30,02,A1,02,F7,65 ..... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary |  |

<a id="job-cod-schreiben-zusatzfunktionen"></a>
### _COD_SCHREIBEN_ZUSATZFUNKTIONEN

Zusatzfunktionen auscodieren Es koennen max. 8 Argumente uebergeben werden FLR:  Fahrleistungsreduzierung HBA:  Hydraulischer Bremsassistent AY:   Offsetabgleich AY gesperrt LW:   Offsetabgleich Lenkwinkel gesperrt PSI_STAND: Offsetabgleich im Stand fuer Giergeschwindigkeit gesperrt PSI_FAHRT: Offsetabgleich waehrend der Fahrt fuer Giergeschwindigkeit gesperrt PSI_EMPF:  Empfindlichkeitsabgleich fuer Giergeschwindigkeit gesperrt SW:        Steilwandmodus aktiviert HVV:  hydraulische Vollverzögerung SST:  Softstop (default: deaktiviert) EVB:  Bremsbereitschaft BSW:  Trockenbremsen HHC:  Anfahrassistenz HPS:  Hydraulic Fading Compensation ASL:  Anhaengerschlingerlogik HDC:  Hill Descent Control Argument: z.B.: HBA,ASL jedoch mit "Strich_Punkt" getrennt (nicht mit Komma !) werden keine Argumente übergeben ist die Defaultcodierung wieder aktiv KWP2000* : $2E WriteDataByCommonIdentifier $300x codingDataSet Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| C_OPTION_1 | string | Zusatzfunktion |
| C_OPTION_2 | string | Zusatzfunktion |
| C_OPTION_3 | string | Zusatzfunktion |
| C_OPTION_4 | string | Zusatzfunktion |
| C_OPTION_5 | string | Zusatzfunktion |
| C_OPTION_6 | string | Zusatzfunktion |
| C_OPTION_7 | string | Zusatzfunktion |
| C_OPTION_8 | string | Zusatzfunktion |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary |  |

<a id="job-ident-sensorcluster-mm3-x"></a>
### _IDENT_SENSORCLUSTER_MM3_X

Auslesen des DSC Sensor-Clusters KWP2000*: $22 ReadDataByCommonIdentifier $1601 DSC Sensor-Cluster  lesen Modus    : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DSC_SC_VERBAUORT | string | DSC-Sensorcluster Verbauort |
| DSC_SC_HW_NR | string | DSC-Sensorcluster Hardware Nummer |
| ID_DATUM_JAHR | int | Herstelldatum Jahr |
| ID_DATUM_MONAT | int | Herstelldatum (Monat) |
| ID_DATUM_TAG | int | Herstelldatum (Tag) |
| ID_DATUM | string | Herstelldatum (TT.MM.JJ) |
| DSC_SC_SERIEN_NR | string | DSC-Sensorcluster Serien-Nummer |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag ans SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-laengsbeschleunigung-dsc-abgleichen"></a>
### LAENGSBESCHLEUNIGUNG_DSC_ABGLEICHEN

der Parameter"R" ist optional: "R" fordert zusaetzlich ein Ergebnis-Telegramm an Musterparametersatz: R mit diesem Job wird auch die MM3.x Teilenummer in die ECU eingelesen KWP2000* : $30,$0B InputOutputControlByLocalIdentifier $33,$0B RequestRoutineResultsByLocalIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ERGEBNIS | string | Default: Ergebnis nicht abholen. Wenn Argument &lt;Ergebnis&gt; vorhanden, dann Ergebnis abholen |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_ERGEBNIS_BYTE | string | Text |
| _TEL_AUFTRAG | binary | Anforderungstelegramm |
| _TEL_AUFTRAG_1 | binary | Anforderungstelegramm |
| _TEL_ANTWORT | binary | Anforderungstelegramm |
| _TEL_ANTWORT_1 | binary | Anforderungstelegramm |
| _TEL_ANTWORT_2 | binary | Anforderungstelegramm |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (77 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (12 × 2)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (491 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (1 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (9 × 9)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (10 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [DIGITAL](#table-digital) (1 × 9)
- [STG_TABELLE](#table-stg-tabelle) (18 × 4)
- [STEUERN_I_O_EIN](#table-steuern-i-o-ein) (19 × 4)
- [STEUERN_I_O_AUS](#table-steuern-i-o-aus) (17 × 4)
- [RAD_NR_TABELLE](#table-rad-nr-tabelle) (4 × 3)
- [RADDREHRICHTUNG](#table-raddrehrichtung) (7 × 6)
- [CODIERUNG](#table-codierung) (18 × 5)

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

Dimensions: 77 rows × 2 columns

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
| 0x76 | CEL |
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

Dimensions: 12 rows × 2 columns

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
| 0x0A00 | Regen- Lichtsensor |
| 0xFFFF | unbekannter Verbauort |

<a id="table-partnrtabelle"></a>
### PARTNRTABELLE

Dimensions: 1 rows × 3 columns

| PART_NR | BMW_NR | KOMMENTAR |
| --- | --- | --- |
| -- | -- | unbekannte Teilenummer |

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
| - | BMW-FAST |
| 1 | KWP2000* |
| - | KWP2000 |
| - | DS2 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 491 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5d8c | 5d8c - Rueckfoerder Pumpe: - Fehler bei Rueckmeldung aus Spannungsueberwachung: RFP AN aber erwartet: AUS - Leitungsstoerung ? |
| 0x5d8d | 5d8d - Rueckfoerder Pumpe: - steht. Fehler bei Rueckmeldung aus Spannungsueberwachung: RFP AUS aber erwartet: AN - Sicherung oder Pumpenmotorrelais defekt ? |
| 0x5d8e | 5d8e - Rueckfoerder Pumpe: - Nachlauf zu kurz. |
| 0x5d8f | 5d8f - Rueckfoerder Pumpe: - Freigabe des Pumpen-Anlauf-Zyklus, kein Fehler: Gutpruefung nach behobenem Defekt erfolgt. |
| 0x5d90 | 5d90 - Ventil Relais: VR offen. Fehler verursacht durch zu viele erkannte Einzelventilfehler - Sicherung defekt ? |
| 0x5d91 | 5d91 - Ventil Relais: VR offen, Relais schliesst nicht waehrend Startup-Test. |
| 0x5d92 | 5d92 - Ventil Relais: VR-Ansteuerungsinformation via SP-Interface zeigt keinen Effekt. |
| 0x5d93 | 5d93 - Ventil Relais: Mittel- oder hochohmiger Kurzschluss von Spannungsversorgung_VR oder Ventil nach Masse ueber Startup-Test erkannt. |
| 0x5d94 | 5d94 - Ventil Relais: VR steckt in geschlossener Position. Relais schaltet nicht ab waehrend Startup-Test. |
| 0x5d95 | 5d95 - Ventil Relais: VR offen, Spannungsversorgung_VR waehrend Startup-Test zu niedrig (verglichen mit Uz Versorgungsspannung_Klemme_15); Defekte Sicherung! |
| 0x5d96 | 5d96 - Ventil Relais: Kurzschluss zu Uz Versorgungsspannung_Klemme_15 im zyklischen Ventilrelais-Test festgestellt. |
| 0x5d97 | 5d97 - Ventil Relais: Mittel- oder hochohmiger Kurzschluss der Spannungsversorgung_VR oder des Ventils auf Masse waehrend zyklischem Ventilrelais-Test registriert. |
| 0x5d98 | 5d98 - Einlass Ventil (EV) Vorne Links - zyklischer Ventil- und Relaistest. |
| 0x5d99 | 5d99 - Einlass Ventil (EV) Vorne Links - Allgemeiner Fehler. |
| 0x5d9a | 5D9A - Drehratensensor: DRS sendet Signal DrsAX1=INITStatusfehler. (DRS-Typ MM 3.x). |
| 0x5d9b | 5d9b - Einlass Ventil (EV) Vorne Links - Ventilspannung defekt (Driftfehler) - Leitungsverbindung oder Endstufe defekt ? |
| 0x5d9c | 5D9C - Drehratensensor: DRS sendet Signal DrsAY1=INITStatusfehler (DRS-Typ MM 3.x). |
| 0x5d9d | 5d9d - Auslass Ventil (AV) Vorne Links - Fehler bei zyklischem Ventil- und Relaistest. |
| 0x5d9e | 5d9e - Auslass Ventil (AV) Vorne Links - Allgemeiner Fehler. |
| 0x5d9f | 5D9F - Drehratensensor: DRS sendet Signal DrsAY2=INITStatusfehler (DRS-Typ MM 3.x). |
| 0x5da0 | 5DA0 - Drehratensensor: DRS sendet Signal DrsPSIP1=INITStatusfehler (DRS-Typ MM 3.x). |
| 0x5da1 | 5da1 - Einlass Ventil (EV) Vorne Rechts - Fehler bei zyklischem Ventil- und Relaistest. |
| 0x5da2 | 5da2 - Einlass Ventil (EV) Vorne Rechts - Allgemeiner Fehler. |
| 0x5da3 | 5DA3 - Drehratensensor: DRS sendet Signal DrsPSIP2=INIT,Statusfehler (DRS-Typ MM 3.x). |
| 0x5da4 | 5DA4 - Drehratensensor: DRS sendet Signal DrsAX1=Signalfehler. Resertierbar (DRS-Typ MM 3.x). |
| 0x5da5 | 5DA5 - Drehratensensor: DRS sendet Signal DrsAY1=Signalfehler. Resertierbar (DRS-Typ MM 3.x). |
| 0x5da6 | 5da6 - Auslass Ventil (AV) Vorne Rechts - Fehler bei zyklischem Ventil- und Relaistest. |
| 0x5da7 | 5da7 - Auslass Ventil (AV) Vorne Rechts - Allgemeiner Fehler. |
| 0x5da8 | 5DA8 - Drehratensensor: DRS sendet Signal DrsAY2=Signalfehler. Resertierbar (DRS-Typ MM 3.x). |
| 0x5da9 | 5DA9 - Drehratensensor: DRS sendet Signal DrsPSIP1=Signalfehler. Resertierbar (DRS-Typ MM 3.x). |
| 0x5daa | 5daa - Einlass Ventil (EV) Hinten Links - Fehler bei zyklischem Ventil- und Relaistest. |
| 0x5dab | 5dab - Einlass Ventil (EV) Hinten Links - Allgemeiner Fehler. |
| 0x5dac | 5DAC - Drehratensensor: DRS sendet Signal DrsPSIP2=Signalfehler. Resertierbar (DRS-Typ MM 3.x). |
| 0x5dad | 5dad - Einlass Ventil (EV) Hinten Links - Ventilspannung defekt (Driftfehler) - Leitungsverbindung oder Endstufe defekt ? |
| 0x5dae | 5DAE - Drehratensensor: DRS sendet Signal AX1=ungueltig (DRS-Typ MM 3.x). |
| 0x5daf | 5daf - Auslass Ventil (AV) Hinten Links - Fehler bei zyklischem Ventil- und Relaistest. |
| 0x5db0 | 5db0 - Auslass Ventil (AV) Hinten Links - Allgemeiner Fehler. |
| 0x5db1 | 5DB1 - Drehratensensor: DRS sendet Signal AY1=ungueltig (DRS-Typ MM 3.x). |
| 0x5db2 | 5DB2 - Drehratensensor: DRS sendet Signal AY2=ungueltig (DRS-Typ MM 3.x). |
| 0x5db3 | 5db3 - Einlass Ventil (EV) Hinten Rechts - Fehler bei zyklischem Ventil- und Relaistest. |
| 0x5db4 | 5db4 - Einlass Ventil (EV) Hinten Rechts - Allgemeiner Fehler. |
| 0x5db5 | 5DB5 - Drehratensensor: DRS sendet Signal PSIP!=ungueltig (DRS-Typ MM 3.x). |
| 0x5db6 | 5DB6 - Drehratensensor: DRS sendet Signal PSIP2=ungeltig (DRS-Typ MM 3.x). |
| 0x5db7 | 5DB7 - Drehratensensor: DRS sendet Signal PSIPP=ungueltig (DRS-Typ MM 3.x). |
| 0x5db8 | 5db8 - Auslass Ventil (AV) Hinten Rechts - Fehler bei zyklischem Ventil- und Relaistest. |
| 0x5db9 | 5db9 - Auslass Ventil (AV) Hinten Rechts - Allgemeiner Fehler. |
| 0x5dba | 5DBA - Drehratensensor: Interner Fehler: Ax1SensNotAvailable (DRS-Typ MM3.x). |
| 0x5dbb | 5DBB - Drehratensensor: Interner Fehler: Ay1SensNotAvailable (DRS-Typ MM3.x). |
| 0x5dbc | 5dbc - Ventil (USV1): Fehler bei zyklischem Ventil- und Relaistest. |
| 0x5dbd | 5dbd - Ventil (USV1): Allgemeiner Fehler. |
| 0x5dbe | 5DBE - Drehratensensor: Interner Fehler: Ay2SensNotAvailable (DRS-Typ MM3.x) |
| 0x5dbf | 5dbf - Ventil (USV1): Ventilspannung defekt (Driftfehler) - Leitungsverbindung oder Endstufe defekt ? |
| 0x5dc0 | 5DC0 - Drehratensensor: Interner Fehler: PSIP1SensNotAvailable (DRS-Typ MM3.x). |
| 0x5dc1 | 5dc1 - Ventil (USV2): Fehler bei zyklischem Ventil- und Relaistest. |
| 0x5dc2 | 5dc2 - Ventil (USV2): Allgemeiner Fehler. |
| 0x5dc3 | 5DC3 - Drehratensensor: Interner Fehler: PSIP2SensNotAvailable (DRS-Typ MM3.x) |
| 0x5dc4 | 5DC4 - Drehratensensor: Interner Fehler: PSIPPSensNotAvailable (DRS-TypMM 3.x). DRS MM 3.x (R): DRS - PSIPPSensNotAvailable. |
| 0x5dc6 | 5dc6 - Ventil (HSV1): Fehler bei zyklischem Ventil- und Relaistest. |
| 0x5dc7 | 5dc7 - Ventil (HSV1): Allgemeiner Fehler. |
| 0x5dc8 | 5DC8 - Ventil HSV1 - Kurzschluss zur Masse. |
| 0x5dc9 | 5DC9 - Ventil HSV1 - Fehler nicht zuweisbar |
| 0x5dca | 5dca - Ventil (HSV2): Fehler bei zyklischem Ventil- und Relaistest. |
| 0x5dcb | 5dcb - Ventil (HSV2): Allgemeiner Fehler. |
| 0x5dcc | 5DCC - Ventil HSV2 - Kurzschluss zur Masse. |
| 0x5dcd | 5DCD - Ventil HSV2 - Fehler nicht zuweisbar |
| 0x5dce | 5dce - Uz Versorgungsspannung_Klemme_15-Fehler: leichte Unterspannung (Spannung zu niedrig). |
| 0x5dcf | 5dcf - Uz Versorgungsspannung_Klemme_15-Fehler: schwere Unterspannung (Spannung viel zu niedrig). |
| 0x5dd0 | 5dd0 - Uz Versorgungsspannung_Klemme_15-Fehler: Ueberspannung (Spannung zu hoch). |
| 0x5dd1 | 5dd1 - Uz Versorgungsspannung_Klemme_15-Fehler: Kurzschluss einer Drehzahlsensor-Spannungsleitung auf UBatt. (Stromfluss durch den ASPxx-Pin des Drehzahlsensor_Inputamplifiers). |
| 0x5dd2 | 5dd2 - Uz Versorgungsspannung_Klemme_15-Fehler: Spannungsspitze auf Uz Versorgungsspannung_Klemme_15. |
| 0x5dd3 | 5dd3 - DSC-ECU: Gemessene Uz Versorgungsspannung_Klemme_15 zu niedrig (Spannungsteiler-Fehler). |
| 0x5dd4 | 5dd4 - DSC-ECU: ECU-intern: Raddrehzahlfuehler-Driverchip: Fehler bei Versorgungsspannung/Masse. Reset-Response-Test fehlerhaft. |
| 0x5dd5 | 5dd5 - DSC-ECU: ECU-intern: Enable-Leitung kann nicht eingeschaltet werden (Startup-Test Enable High). |
| 0x5dd6 | 5dd6 - DSC-ECU: ECU-intern: Enable-Leitung kann nicht ausgeschaltet werden (Startup-Test Enable low). |
| 0x5dd8 | 5dd8 - DSC-ECU: ECU-intern: System Startup-Synchronisation-Timeout aufgetreten. |
| 0x5dd9 | 5dd9 - DSC-ECU: ECU-intern: SP-Interface: Hardware Fehler erkannt. |
| 0x5dda | 5DDA - Einlassventil (Ev) Vorne links - Kurzschluss zur Masse. |
| 0x5ddb | 5DDB - Einlassventil (Ev) Vorne links - Fehler nicht zuweisbar |
| 0x5ddc | 5ddc - DSC-ECU: ECU-intern: Het-SP-Interface sendet Fehler; Nachricht nicht korrekt uebertragen. |
| 0x5ddd | 5ddd - DSC-ECU: ECU-intern: Zugang in Uebersetzungstabelle des Het-SP-Interface ist nicht moeglich. |
| 0x5dde | 5dde - DSC-ECU: ECU-intern: Watchdog-Ueberwachung meldet: Datenfehler aufgetreten. |
| 0x5ddf | 5ddf - DSC-ECU: ECU-intern: Watchdog-Ueberwachung meldet: Status nicht korrekt. |
| 0x5de0 | 5de0 - DSC-ECU: ECU-intern: Plausibilität des VASP-U_Bit in Bezug zu Uz Versorgungsspannung_Klemme_15. |
| 0x5de1 | 5de1 - DSC-ECU: ECU-intern: Clockstatus des SP-Interface zeigt fehlende Uhr. |
| 0x5de2 | 5de2 - DSC-ECU: ECU-intern: DePwm Status : Software-/ Hardware Konfigurationen passen nicht zusammen (DF11i/s). |
| 0x5de3 | 5de3 - DSC-ECU: ECU-intern: Status_Raddrehzahlfuehler des SP-Interface passt nicht zur Konfiguration. |
| 0x5de4 | 5de4 - DSC-ECU: ECU-intern: Boot Block ROM Checksummentest-Fehler. |
| 0x5de5 | 5DE5 - Auslassventil (Av) Vorne links - Kurzschluss zur Masse. |
| 0x5de6 | 5DE6 - Auslassventil (Av) Vorne links - Fehler nicht zuweisbar |
| 0x5de7 | 5de7 - Verteilergetriebe-ECU: Funktionspruefung nicht Ok. |
| 0x5de8 | 5DE8 - Verteilergetriebe-ECU: Kupplung ueber Diagnose deaktiviert. |
| 0x5de9 | 5de9 - Infoeintrag: Verteilergetriebe-ECU: Unkomfortable VG-Kupplungsregelung. |
| 0x5dea | 5dea - Infoeintrag : Verteilergetriebe-ECU: Reduktion Momentenvorsteuerung wegen Reibarbeit im VG. |
| 0x5dec | 5dec - Verteilergetriebe-ECU: Kupplung voruebergehend stillgelegt. |
| 0x5dee | 5dee - DSC-ECU: ECU-intern: Fehlererkennungssystem-Fehler in Status/Transfer: SP-Interface-Fehler in Algorithm-Server. |
| 0x5def | 5def - DSC-ECU: ECU-intern: ROM Checksummentest-Fehler. |
| 0x5df0 | 5df0 - DSC-ECU: ECU-intern: RAM Adressierungstest-Fehler. |
| 0x5df1 | 5df1 - DSC-ECU: ECU-intern: RAM Checkpatterntest-Fehler. |
| 0x5df2 | 5df2 - DSC-ECU: ECU-intern: HET RAM Adressierungstest-Fehler. |
| 0x5df3 | 5df3 - DSC-ECU: ECU-intern: HET RAM Checkpatterntest-Fehler. |
| 0x5df4 | 5DF4 - DSC-ECU: ECU-intern: ADC Kalibrierungs-Fehler. |
| 0x5df5 | 5df5 - DSC-ECU: ECU-intern: Can RAM Checkpatterntest-Fehler. |
| 0x5df6 | 5df6 - DSC-ECU: ECU-intern: Betriebssystem Rechenzykluszeit zu hoch - falsches Rechenzyklus (Task)-Timing. |
| 0x5df7 | 5df7 - DSC-ECU: ECU-intern: Betriebssystem: geringe Background-Rechenzyklus(Task) Aktivitaet - System ueberlastet ! |
| 0x5df8 | 5df8 - DSC-ECU: ECU-intern: Betriebssystem Ausnahmefehler. |
| 0x5df9 | 5df9 - DSC-ECU: ECU-intern: Betriebssystem: Rechenzyklus (Task) fehlt (bzw. nicht aktiviert). |
| 0x5dfa | 5dfa - DSC-ECU: ECU-intern: Undefinierter Fast-Interrupt-Request (FIQ) aufgetreten. |
| 0x5dfb | 5dfb - DSC-ECU: ECU-intern: Datenabbruch  -&gt; Mikrocontroller Mode: Daboard. |
| 0x5dfc | 5dfc - DSC-ECU: ECU-intern: Programm Abbruch  -&gt; Mikrocontroller Mode: Paboard. |
| 0x5dfd | 5dfd - DSC-ECU: ECU-intern: Illegalen Opcode gefunden    -&gt; Mikrocontroller Mode: undefiniert. |
| 0x5dfe | 5dfe - DSC-ECU: ECU-intern: ROM Checksummentest-Fehler. |
| 0x5dff | 5dff - DSC-ECU: ECU-intern: RAM Adressierungstest-Fehler. |
| 0x5e00 | 5e00 - DSC-ECU: ECU-intern: RAM Checkpatterntest-Fehler. |
| 0x5e01 | 5e01 - DSC-ECU: ECU-intern: HET RAM Adressierungstest-Fehler. |
| 0x5e02 | 5e02 - DSC-ECU: ECU-intern: HET RAM Checkpatterntest-Fehler. |
| 0x5e03 | 5e03 - DSC-ECU: ECU-intern: Allgemeiner Fehler des Ventiltreiber-Status oder -antriebes durch zyklischen Ventilrelaistest registriert. |
| 0x5e04 | 5e04 - DSC-ECU: ECU-intern: Fehler der permanenten Enable-Leitungsueberwachung (Enable ist low nach Startup-Test). |
| 0x5e05 | 5e05 - DSC-ECU: ECU-intern: nicht moeglich SP-Interface transfer zu planen. |
| 0x5e06 | 5e06 - DSC-ECU: ECU-intern: Planmaessige Datenuebertragung nicht verfuegbar. |
| 0x5e07 | 5e07 - DSC-ECU: ECU-intern: Datenuebertragungsfehler (Antwort des SP-Interface handler). |
| 0x5e08 | 5e08 - DSC-ECU: ECU-intern: Planmaessiger Build-in-self-test (BIST) nicht korrekt (BIST Kontinuität). |
| 0x5e09 | 5e09 - DSC-ECU: ECU-intern: Build-in-self-test (BIST)-Signaturen verschieden, CPU Fehler im Algorithm- oder System-Server. |
| 0x5e0a | 5e0a - DSC-ECU: ECU-intern: Allgemeiner Steuergeräte-Fehler. |
| 0x5e0b | 5e0b - DSC-ECU: ECU-intern: Fehlererkennungssystem Fehler und Status Transfer: First-in-first-out-Overflow im System-Server aufgetreten. |
| 0x5e0c | 5e0c - DSC-ECU: ECU-intern: Build-in-self-test (BIST)-Signaturen unterschiedlich. CPU Fehler in Algorithm- oder System-Server. |
| 0x5e0d | 5e0d - DSC-ECU: ECU-intern: Timeout des Build-in-self-test (BIST). Antwort durch Algorithm-Server. |
| 0x5e0e | 5e0e - DSC-ECU: ECU-intern: Betriebssystem Rechenzykluszeit zu hoch - falsches Rechenzyklus (Task) Timing. |
| 0x5e0f | 5e0f - DSC-ECU: ECU-intern: Betriebssystem Rechenzyklus (Task) fehlt (bzw. nicht aktiviert). |
| 0x5e10 | 5e10 - DSC-ECU: ECU-intern: Betriebssystem: geringe Background Rechenzyklus (Task) Aktivität - System ueberlastet ! |
| 0x5e11 | 5e11 - DSC-ECU: ECU-intern: Undefinierter Fast-Interrupt-Request (FIQ) aufgetreten. |
| 0x5e12 | 5e12 - DSC-ECU: ECU-intern: Illegaler Opcode gefunden  -&gt; Mikrocontroller Mode: undefiniert |
| 0x5e13 | 5e13 - DSC-ECU: ECU-intern: Programm Abbruch  -&gt; Mikrocontroller Mode: Paboard. |
| 0x5e14 | 5e14 - DSC-ECU: ECU-intern: Datenabbruch  -&gt; Mikrocontroller Mode: Daboard. |
| 0x5e15 | 5e15 - DSC-ECU: ECU-intern: Fehlererkennungssystem Status Transfer: SP-Interface timeout in System-Server. |
| 0x5e16 | 5e16 - DSC-ECU: ECU-intern: Fehlererkennungssystem Transfer Fehler: SP-Interface timeout in System-Server. |
| 0x5e17 | 5e17 - DSC-ECU: ECU-intern: Fehlererkennungssystem Status Transfer: SP-Interface Fehler in System-Server. |
| 0x5e18 | 5e18 - DSC-ECU: ECU-intern: Datenmenge der Peripherie SP-Interface ueberschreitet Bufferlaenge. |
| 0x5e19 | 5e19 - DSC-ECU: ECU-intern: Serial-Peripherial-Interface (SPI): ID Anfrage nicht akzeptiert. |
| 0x5e1a | 5e1a - DSC-ECU: ECU-intern: Serial-Peripherial-Interface (SPI): Uebersetzungsfehler multi IC. |
| 0x5e1b | 5e1b - DSC-ECU: ECU-intern: Serial-Peripherial-Interface (SPI): Uebersetzungsfehler im EEPROM. |
| 0x5e1c | 5e1c - DSC-ECU: ECU-intern: Bandluecke Spannung ausserhalb gueltigem Bereich. |
| 0x5e1d | 5e1d - DSC-ECU: ECU-intern: ADC Umwandlung Start-Fehler. |
| 0x5e1e | 5E1E - DSC-ECU: ECU-intern: Flash Reprogrammierungszyklus ist fehlgeschlagen (Zellen nicht reprogrammiert). |
| 0x5e1f | 5E1F - Infoeintrag: DSC-ECU: Flash Reprogrammierungszyklus erfolgreich ausgefuehrt (Info). |
| 0x5e20 | 5e20 - DSC-ECU: Allgemeiner Steuergeräte-Fehler. |
| 0x5e21 | 5e21 - DSC-ECU: ECU-intern: Betriebssystem Ausnahmefehler. |
| 0x5e22 | 5e22 - Raddrehzahlfuehler Vorne Links: Leitungsstoerung oder Kurzschluss. |
| 0x5e23 | 5e23 - Raddrehzahlfuehler Vorne Links: Langzeitig vorhandener Fehlerverdacht. |
| 0x5e24 | 5e24 - Raddrehzahlfuehler Vorne Links: Signalflanke fehlt (RDF Typ 11i). |
| 0x5e25 | 5e25 - Raddrehzahlfuehler Vorne Links: falsche Signalweite (&gt;2ms)DF11. Korrekter RDF-Typ verbaut ? |
| 0x5e26 | 5e26 - Raddrehzahlfuehler Vorne Links: Luftspalt zu groß. |
| 0x5e27 | 5e27 - Raddrehzahlfuehler Vorne Links: Dynamischen Signalverlust registriert. Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e28 | 5e28 - Raddrehzahlfuehler Vorne Links: Fehler Signaleinstreuungs-Ueberwachung (Noise Monitor). Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e29 | 5E29 - Einlassventil (Ev) Vorne rechts - Kurzschluss zur Masse. |
| 0x5e2a | 5E2A - Einlassventil (Ev) Vorne rechts - Fehler nicht zuweisbar |
| 0x5e2b | 5E2B - Auslassventil (Av) Vorne rechts - Kurzschluss zur Masse. |
| 0x5e2c | 5E2C - Drehratensensor: Ueber CAN-Bus empfangene DRS-Type passt nicht zur Konfiguration (DRS-Typ MM 3.x). |
| 0x5e2d | 5e2d - Raddrehzahlfuehler Vorne Links: Fehlender Zahn RAD VL. Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e2e | 5e2e - Raddrehzahlfuehler Vorne Links: Radschlupfueberwachung RAD VL. Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e2f | 5e2f - Raddrehzahlfuehler Vorne Links: Fehler Anfahrerkennung RAD VL (RDF-Signalwert ungueltig). Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e30 | 5e30 - Raddrehzahlfuehler Hinten Links: Leitungsstoerung oder Kurzschluss. |
| 0x5e31 | 5e31 - Raddrehzahlfuehler Hinten Links: Langzeitig vorhandener Fehlerverdacht. |
| 0x5e32 | 5e32 - Raddrehzahlfuehler Hinten Links: Signalflanke fehlt (RDF Typ 11i). |
| 0x5e33 | 5e33 - Raddrehzahlfuehler Hinten Links: falsche Signalweite (&gt;2ms)DF11. Korrekter RDF-Typ verbaut ? |
| 0x5e34 | 5e34 - Raddrehzahlfuehler Hinten Links: Luftspalt zu groß. |
| 0x5e35 | 5e35 - Raddrehzahlfuehler Hinten Links: Dynamischen Signalverlust registriert. Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e36 | 5e36 - Raddrehzahlfuehler Hinten Links: Fehler Signaleinstreuungs-Ueberwachung (Noise Monitor). Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e37 | 5E37 - Drehratensensor: DRS-Type falsch oder CluType-ID7 nicht erlaubt (DRS-Typ MM 3.x). |
| 0x5e38 | 5E38 - Drehratensensor: DRS meldet CheckTimeout. DrsVARCheckTimeout (DRS-Typ MM 3.x). |
| 0x5e39 | 5E39 - Drehratensensor: Interner Fehler. SensDetectedCRC (DRS-Typ MM 3.x). |
| 0x5e3a | 5E3A - Drehratensensor: Interner Fehler. Ueberspannung erkannt. |
| 0x5e3b | 5e3b - Raddrehzahlfuehler Hinten Links: Fehlender Zahn RAD HL. Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e3c | 5e3c - Raddrehzahlfuehler Hinten Links: Radschlupfueberwachung  RAD HL. Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e3d | 5e3d - Raddrehzahlfuehler Hinten Links: Fehler Anfahrerkennung RAD HL (RDF-Signalwert ungueltig). Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e3e | 5e3e - Raddrehzahlfuehler Hinten Rechts: Leitungsstoerung oder Kurzschluss. |
| 0x5e3f | 5e3f - Raddrehzahlfuehler Hinten Rechts: Langzeitig vorhandener Fehlerverdacht. |
| 0x5e40 | 5e40 - Raddrehzahlfuehler Hinten Rechts: Signalflanke fehlt (RDF Typ 11i). |
| 0x5e41 | 5e41 - Raddrehzahlfuehler Hinten Rechts: falsche Signalweite (&gt;2ms)DF11. Korrekter RDF-Typ verbaut ? |
| 0x5e42 | 5e42 - Raddrehzahlfuehler Hinten Rechts: Luftspalt zu groß. |
| 0x5e43 | 5e43 - Raddrehzahlfuehler Hinten Rechts: Dynamischen Signalverlust registriert. Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e44 | 5e44 - Raddrehzahlfuehler Hinten Rechts: Fehler Signaleinstreuungs-Ueberwachung (Noise Monitor). Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e45 | 5E45 - Drehratensensor: Interner Fehler (DRS-Typ MM 3.x). |
| 0x5e46 | 5E46 - PT-CAN: Botschaft SYNC (ID 0x85) konnte nicht abgeschickt werden (von DSC-SG gesendet). |
| 0x5e47 | 5E47 - Einlassventil (Ev) Hinten links - Kurzschluss zur Masse. |
| 0x5e48 | 5E48 - Einlassventil (Ev) Hinten links - Fehler nicht zuweisbar |
| 0x5e49 | 5e49 - Raddrehzahlfuehler Hinten Rechts: Fehlender Zahn RAD HR. Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e4a | 5e4a - Raddrehzahlfuehler Hinten Rechts: Radschlupfueberwachung  RAD HR. Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e4b | 5e4b - Raddrehzahlfuehler Hinten Rechts: Fehler Anfahrerkennung RAD HR (RDF-Signalwert ungueltig). Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e4c | 5e4c - Raddrehzahlfuehler Vorne Rechts: Leitungsstoerung oder Kurzschluss. |
| 0x5e4d | 5e4d - Raddrehzahlfuehler Vorne Rechts: Langzeitig vorhandener Fehlerverdacht. |
| 0x5e4e | 5e4e - Raddrehzahlfuehler Vorne Rechts: Signalflanke fehlt (RDF Typ 11i). |
| 0x5e4f | 5e4f - Raddrehzahlfuehler Vorne Rechts: falsche Signalweite (&gt;2ms)DF11. Korrekter RDF-Typ verbaut ? |
| 0x5e50 | 5e50 - Raddrehzahlfuehler Vorne Rechts: Luftspalt zu groß. |
| 0x5e51 | 5e51 - Raddrehzahlfuehler Vorne Rechts: Dynamischen Signalverlust registriert. Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e52 | 5e52 - Raddrehzahlfuehler Vorne Rechts: Fehler Signaleinstreuungs-Ueberwachung (Noise Monitor). Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e53 | 5E53 - HFC: HFC ist laenger als 500ms aktiv und Bremsscheibentemp. oberhalb Grenzwert 1. |
| 0x5e54 | 5E54 - HFC: HFC ist aktiv und Bremsscheibentemperatur oberhalb Grenzwert 2. |
| 0x5e55 | 5E55 - CAN-Fehler: Botschaft LDM_Anforderung_Radmoment_Sollwert ungueltig. |
| 0x5e56 | 5E56 - CAN-Fehler: Botschaft LDM_Anforderung_Radmoment_Sollwertverteilung (vorne/hinten) ungueltig. |
| 0x5e57 | 5e57 - Raddrehzahlfuehler Vorne Rechts: Fehlender Zahn RAD VR. Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e58 | 5e58 - Raddrehzahlfuehler Vorne Rechts: Radschlupfueberwachung  RAD VR. Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e59 | 5e59 - Raddrehzahlfuehler Vorne Rechts: Fehler Anfahrerkennung RAD VR (RDF-Signalwert ungueltig). Gutpruefung nach behobenem Defekt erforderlich ! |
| 0x5e5a | 5e5a - Raddrehzahlfuehler allgemein: Mehrere Raddrehzahlfuehler: Langzeitig vorhandener Fehlerverdacht von 2 Raddrehzahlfuehler. |
| 0x5e5b | 5e5b - Raddrehzahlfuehler allgemein: Mehrere Raddrehzahlfuehler: Langzeitig vorhandener Fehlerverdacht von 3 oder 4 Raddrehzahlfuehler. |
| 0x5e5c | 5e5c - Raddrehzahlfuehler allgemein: Plausibilitaet Drehrichtung. |
| 0x5e5d | 5e5d - Raddrehzahlfuehler allgemein: Unplausibilitaet bei ABS-Regelung. |
| 0x5e5e | 5e5e - Raddrehzahlfuehler allgemein: Schlupfueberwachung (Lambda) allgemein. |
| 0x5e5f | 5e5f - Raddrehzahlfuehler allgemein: Mehrere Raddrehzahlfuehler: Kurzzeitiger Fehlerverdacht von 2-3 Raddrehzahlfuehler. Möglicherweise ohne Lampenanzeige. (Temporärer, heilbarer Fehler). |
| 0x5e60 | 5E60 - Bremslichtschalter: Plausibilitaet des BLS-Signals gegen gemeldetes BS-Signal von DME – Leitungs-Kurzschluss ? |
| 0x5e61 | 5E61 - Querbeschleunigungssensor:  - Controller Release System (CRS) - Fehlerverdacht Gradient. |
| 0x5e62 | 5e62 - Bremslichschalter-Fehler: Ueberwachung BLS permanent high |
| 0x5e63 | 5e63 - Bremslichschalter-Fehler: Ueberwachung BLS permanent high mit SilaMemory (ECU sieht permanent getretenes Bremspedal)- Gutpruefung nach behobenem Defekt erforderlich ! -Leitungsunterbrechung oder Kurzschluss ? |
| 0x5e64 | 5e64 - CAN-Bus-Fehler: Allgemeiner CAN-Fehler. |
| 0x5e66 | 5E66 - Raddrehzahlfuehler allgemein: vertauschte Raddrehzahlfuehler an Vorderachse. |
| 0x5e67 | 5E67 - Raddrehzahlfuehler allgemein: vertauschte Raddrehzahlfuehler an Hinterachse. |
| 0x5e68 | 5E68 - Raddrehzahlfuehler allgemein: vertauschte Raddrehzahlfuehler an Vorderachse mit SilaMemory. |
| 0x5e69 | 5E69 - Raddrehzahlfuehler allgemein: vertauschte Raddrehzahlfuehler an Hinterachse mit SilaMemory. |
| 0x5e6a | 5e6a - CAN-Botschaft/DSC-Fehler: Botschaft ASC1 (ID 0x153) nicht abgeschickt (XMT) (von DSC-ECU gesendet). |
| 0x5e6b | 5e6b - CAN-Botschaft/DSC-Fehler: Botschaft ASC2 (ID 0x1F0) nicht abgeschickt (XMT) (von DSC-ECU gesendet). |
| 0x5e6d | 5E6D - PT-CAN: Botschaft SYNC (ID 0x085) konnte nicht abgeschickt werden (von DSC-SG gesendet). |
| 0x5e6e | 5E6E - Auslassventil (Av) Hinten links - Kurzschluss zur Masse. |
| 0x5e6f | 5E6F - Auslassventil (Av) Hinten links - Fehler nicht zuweisbar |
| 0x5e70 | 5e70 - CAN-Botschaft/DSC-Fehler: Botschaft ASC3 (ID 0x1F3) nicht abgeschickt (XMT) (von DSC-ECU gesendet). |
| 0x5e71 | 5E71 - Einlassventil (Ev) Hinten rechts - Kurzschluss zur Masse. |
| 0x5e73 | 5E73 - Einlassventil (Ev) Hinten rechts - Fehler nicht zuweisbar |
| 0x5e76 | 5e76 - CAN-Botschaft/DSC-Fehler: Botschaft ASC4 (ID 0x1F8) nicht abgeschickt (XMT) (von DSC-ECU gesendet). |
| 0x5e77 | 5e77 - CAN-Botschaft/DSC-Fehler: Botschaft DSC1 (ID 0x190) nicht abgeschickt (XMT) (von DSC-ECU gesendet). |
| 0x5e78 | 5E78 - Auslassventil (Av) Vorne rechts - Fehler nicht zuweisbar |
| 0x5e7c | 5E7C - Auslassventil (Av) Hinten rechts - Kurzschluss zur Masse. |
| 0x5e7d | 5E7D - Auslassventil (Av) Hinten rechts - Fehler nicht zuweisbar |
| 0x5e7f | 5E7F - Ventil USV1 - Kurzschluss zur Masse. |
| 0x5e80 | 5E80 - Ventil USV1 - Fehler nicht zuweisbar |
| 0x5e81 | 5E81 - Ventil USV2 - Kurzschluss zur Masse. |
| 0x5e82 | 5E82 - Ventil USV2 - Fehler nicht zuweisbar |
| 0x5e86 | 5E86 - Interner Drucksensor Mc1: Fehler in Spannungsversorgung (Kreis 1). |
| 0x5e87 | 5E87 - Drucksensor Ci1: Fehler in Spannungsversorgung (Kreis 1). |
| 0x5e88 | 5E88 - Drucksensor Ci2: Fehler in Spannungsversorgung (Kreis 2). |
| 0x5e8d | 5E8D - Laengsbeschleunigungs-Sensor: Langzeit-Offsetwert ausserhalb Wertebereich. |
| 0x5e8e | 5e8e - Querbeschleunigungssensor:  - Messbereich Querbeschleunigungssensor. |
| 0x5e8f | 5E8F - Laengsbeschleunigungs-Sensor: Fehler in Plausibilitaetsueberwachung. |
| 0x5e90 | 5e90 - Querbeschleunigungssensor:  - Langzeit-Offset ueberschreitet Limit. |
| 0x5e91 | 5e91 - Querbeschleunigungssensor:  - Wert waehrend Stillstand zu gross. |
| 0x5e92 | 5e92 - Querbeschleunigungssensor:  - Plausibilitaetsfehler, obwohl Modellgueltigkeit gegeben. |
| 0x5e93 | 5e93 - Querbeschleunigungssensor:  - Plausibilitaetsfehler waehrend Signalbeobachtung (Modellgueltigkeit nicht mehr vorhanden). |
| 0x5e94 | 5E94 - Einlassventil (EV) Vorne Rechts: Ventilspannung defekt (Driftfehler) - Leitungsverbindung oder Endstufe defekt? |
| 0x5e95 | 5e95 - Querbeschleunigungssensor:  - Controller Release System (CRS) - Fehlerverdacht Gradient. |
| 0x5e96 | 5e96 - Querbeschleunigungssensor:  - Plattform-Software (PSW) - Fehlerverdacht. |
| 0x5e97 | 5e97 - Querbeschleunigungssensor:  - Controller Release System (CRS)- Fehlerverdacht bei Messbereich. |
| 0x5e98 | 5E98 - Querbeschleunigungssensor: Interner Querbeschleunigungswert ausserhalb Messbereich (DrsERRN02). |
| 0x5e99 | 5E99 - Querbeschleunigungssensor: Interner Selbsttest fehlgeschlagen (DrsERRN04). |
| 0x5e9a | 5e9a - Drehratensensor:  - Vorzeichen-Fehler - Gutpruefung nach behobenem Defekt erforderlich. |
| 0x5e9b | 5e9b - Drehratensensor:  - Beabsichtigte Signalstoerung (Static Bite) fehlerhaft. |
| 0x5e9c | 5e9c - Drehratensensor:  - Plausibilitaetsfehler in Bezug zu Lenkwinkelsensor. |
| 0x5e9d | 5e9d - Drehratensensor:  - Messbereich DRS. |
| 0x5e9e | 5E9E - Drehratensensor: Vorzeichenfehler. |
| 0x5e9f | 5e9f - Drehratensensor:  - Offset ueberschreitet Limit waehrend Stillstand. |
| 0x5ea0 | 5ea0 - Drehratensensor:  - Signalgradient DRS. |
| 0x5ea1 | 5ea1 - Drehratensensor:  - Beabsichtigte Signalstoerung (Dynamic Bite) fehlerhaft. |
| 0x5ea2 | 5ea2 - Drehratensensor:  - Offset ueberschreitet Limit waehrend schneller Kompensation. |
| 0x5ea3 | 5ea3 - Drehratensensor:  - Empfindlichkeit ueberschreitet Limit. |
| 0x5ea4 | 5ea4 - Drehratensensor:  - Offset ueberschreitet Limit waehrend langsamer Kompensation. |
| 0x5ea5 | 5ea5 - Drehratensensor:  - Plausibilitaetsfehler, obwohl Modellgueltigkeit gegeben. |
| 0x5ea6 | 5ea6 - Drehratensensor:  - Plausibilitaetsfehler waehrend Signalbeobachtung (Modellgueltigkeit nicht mehr vorhanden). |
| 0x5ea7 | 5EA7 - Drehratensensor: Redundanz Fehler. |
| 0x5ea8 | 5ea8 - Drehratensensor:  - Controller Release System (CRS) - Fehlerverdacht bei Messbereich DRS. |
| 0x5ea9 | 5ea9 - Drehratensensor:  - Controller Release System (CRS) - Beabsichtigte Signalstoerung (Static Bite) fehlerhaft. |
| 0x5eaa | 5eaa - Drehratensensor:  - Controller Release System (CRS) - Fehlerverdacht DRS bei Signalgradient. |
| 0x5eab | 5eab - Drehratensensor:  - Controller Release System (CRS) - Beabsichtigte Signalstoerung (Dynamic Bite) fehlerhaft. |
| 0x5eac | 5eac - Drehratensensor:  - Plattform-Software (PSW) - Fehlerverdacht DRS. |
| 0x5ead | 5EAD - Drehratensensor: Drs-ID passt nicht zur angefragten ID. |
| 0x5eae | 5EAE - Drehratensensor: Checksumme der empfangenen DRS-Botschaft falsch. |
| 0x5eaf | 5EAF - Drehratensensor: Fehler des ERR- oder TERR-Bits. Keine zusaetzliche Information (ERRNO = 0). |
| 0x5eb0 | 5EB0 - Drehratensensor: Interner Gierratenwert ausserhalb Wertebereich (DrsERRNO1). |
| 0x5eb1 | 5EB1 - Drehratensensor: Interne Referenzvariable ausserhalb Wertebereich (DrsERRNO3). |
| 0x5eb2 | 5EB2 - Drehratensensor: Empfangene Nachricht zu frueh (DrsERRNO5). |
| 0x5eb3 | 5EB3 - Drehratensensor: Spannungsversorgung zu niedrig (DrsERRNO6). |
| 0x5eb4 | 5EB4 - Drehratensensor: Spannungsversorgung zu hoch (DrsERRNO7). |
| 0x5eb5 | 5EB5 - Drehratensensor: Sensor in Initialisierung (DrsERRNO8). |
| 0x5eb6 | 5EB6 - Laengsbeschleunigungs-Sensor: Wertebereich ueberschritten. |
| 0x5eb7 | 5eb7 - Variantencodierung: ungueltige Variantencodierung des Luffeder-Steuergeraetes. |
| 0x5eb8 | 5eb8 - Variantencodierung: Variante mit manuellem Getriebe empfaengt CAN-Botschaft von Getriebesteuergeraet - Fehler. |
| 0x5eb9 | 5eb9 - Variantencodierung: MD-Norm_Wert nicht erlaubt fuer ausgewaehlte Variante. |
| 0x5eba | 5EBA - Lenkwinkelsensor: Statusfehler. |
| 0x5ebb | 5ebb - Lenkwinkelsensor:  - Signalfehler- Gutpruefung nach behobenem Defekt erforderlich. |
| 0x5ebc | 5EBC - Lenkwinkelsensor: Vorzeichenfehler. |
| 0x5ebd | 5ebd - Lenkwinkelsensor:  - Signal verbleibt auf konstanten Wert. |
| 0x5ebe | 5ebe - Lenkwinkelsensor:  - Messbereich LWS. |
| 0x5ebf | 5ebf - Lenkwinkelsensor:  - Signalgradient LWS. |
| 0x5ec0 | 5ec0 - Lenkwinkelsensor:  - Langzeit-Offset-Wert ueberschreitet Limit. |
| 0x5ec1 | 5ec1 - Lenkwinkelsensor:  - Plausibilitaetsfehler - in Bezug zu Drehratensensor. |
| 0x5ec2 | 5EC2 - Infoeintrag: CAN: Allrad-Software ist geladen. |
| 0x5ec4 | 5EC4 - Drucksensor: Testpuls-Fehler. |
| 0x5ec5 | 5ec5 - Lenkwinkelsensor:  - CAN-Botschaftszaehler meldet Fehler. |
| 0x5ed2 | 5ED2 - Bremsscheiben-Wischer: RLS sendet ungueltige Signale in Botschaft INSTR3 (ID 0x615). |
| 0x5ed4 | 5ed4 - Unplausible DSC-Regelung : Unplausibilitaet bei Gierratenregelung (FZR-Controlling). |
| 0x5ed5 | 5ed5 - Unplausible DSC-Regelung : Notbremsfunktion ausgeloest (wegen unplausible Regelung: Blockieren der Raeder wird moeglich gemacht). |
| 0x5ed6 | 5ed6 - Infoeintrag : Langzeitabgleich: LWS-, DRS- und AY-Sensor-Langzeitabgleiche deaktiviert. |
| 0x5ed7 | 5ED7 - Rueckwaertsgangschalter: Ueberwachung meldet: Schalter permanent Rueckwaerts. |
| 0x5ed8 | 5ED8 - Rueckwaertsgangschalter: Ueberwachung meldet: Schalter permanent Vorwaerts. |
| 0x5eda | 5eda - Variantencodierung: Codierungswert in EEPROM nicht zulaessig. |
| 0x5edb | 5edb - Variantencodierung: Codierungswert ausserhalb Wertebereich. |
| 0x5edc | 5edc - Variantencodierung: Codierungswert nicht freigegeben in diesem Projekt. |
| 0x5edd | 5EDD - Interner Drucksensor Mc1: Fehler bei Power On Selbsttest. |
| 0x5ede | 5EDE - Interner Drucksensor Mc1: Leitungsfehler Kanal 1. |
| 0x5edf | 5EDF - Interner Drucksensor Mc1: Leitungsfehler Kanal 2. |
| 0x5ee1 | 5EE1 - Interner Drucksensor Mc1: Plausibilitaetsfehler. |
| 0x5ee2 | 5ee2 - Drucksensor: Plausibilitaet Drucksensor_Signalleitungen- DS5 :DSLine+DSLine2 = 5Volt. |
| 0x5ee3 | 5EE3 - Drucksensor Ci1: Fehler bei Power On Selbsttest. |
| 0x5ee4 | 5ee4 - Drucksensor: Drucksensor-Spannungsversorgung Fehler. |
| 0x5ee5 | 5ee5 - Drucksensor:  - Leitungsfehler. |
| 0x5ee6 | 5ee6 - Drucksensor:  - Leitungsfehler: Signal invertiert. |
| 0x5ee7 | 5ee7 - Drucksensor:  - Fehler beiPower Up Selbsttest (POS). |
| 0x5ee8 | 5EE8 - Drucksensor Ci1: Kanal 1 Leitungsfehler. |
| 0x5ee9 | 5EE9 - Drucksensor Ci1: Kanal 2 Leitungsfehler. |
| 0x5eea | 5EEA - Drucksensor Ci1: Plausibilitaetsfehler. |
| 0x5eeb | 5EEB - Drucksensor Ci2: Fehler bei Power On Selbsttest. |
| 0x5eec | 5EEC - Drucksensor Ci2: Kanal 1 Leitungsfehler. |
| 0x5eed | 5eed - Drucksensor:  - Drucksensor-Offset ungueltig. |
| 0x5eee | 5EEE - Bremslichschalter: Plausibilitaet 1: Plausibilisierung Drucksensor gegen BLS (niedriger Bremsdruckbereich). |
| 0x5eef | 5EEF - Bremslichschalter: Plausibilitaet 2: Plausibilisierung Drucksensor gegen BLS (mittlerer Bremsdruckbereich). |
| 0x5ef0 | 5ef0 - Bremslichschalter:  - Plausibilitaet 3 - Plausibilisierung Drucksensor gegen Bremslichtschalter. |
| 0x5ef1 | 5EF1 - Drucksensor Ci2: Kanal 2 Leitungsfehler. |
| 0x5ef9 | 5ef9 - DSC-Software: ECU-intern : Timeout in Software-Startup-Phase. |
| 0x5efa | 5efa - DSC-Software: ECU-intern : asynchroner Rechenzyklus (Task)-Counter in Software. |
| 0x5efb | 5EFB - Variantenkodierung: Variantenschalter konnte aus EEPROM nicht gelesen werden. |
| 0x5efc | 5EFC - Variantenkodierung: Keine Fahrzeugtyp Daten empfangen. |
| 0x5efd | 5EFD - Infoeintrag: Variantenkodierung: Neuer Variantenkodierungswert gesetzt. |
| 0x5efe | 5efe - Raddrehzahlfuehler Vorne Links: max. Anzahl von unplausiblen Sensorwerten (InplRad) ueberschritten Rad VL. |
| 0x5eff | 5eff - Raddrehzahlfuehler Hinten Links: max. Anzahl von unplausiblen Sensorwerten (InplRad) ueberschritten Rad HL. |
| 0x5f00 | 5f00 - Raddrehzahlfuehler Hinten Rechts: max. Anzahl von unplausiblen Sensorwerten (InplRad) ueberschritten Rad HR. |
| 0x5f01 | 5f01 - Raddrehzahlfuehler Vorne Rechts: max. Anzahl von unplausiblen Sensorwerten (InplRad) ueberschritten Rad VR. |
| 0x5f02 | 5f02 - Raddrehzahlfuehler allgemein: max. Anzahl von unplausiblen Sensorwerten (InplRad) ueberschritten. |
| 0x5f03 | 5f03 - ECU-Fehler: Fehler beim lesen der ASW-EEPROM Werte: Defekte EEPROM-Zelle |
| 0x5f04 | 5f04 - ECU-Fehler: Auslesen der ASW-EEPROM Werte dauert zu lange |
| 0x5f05 | 5f05 - ECU-Fehler: Testpin Leitungsunterbrechung ueber ValveDriftCheck fuer U467 erkannt. |
| 0x5f06 | 5f06 - ECU-Fehler: fehlerhafter Zugriff auf Ventilausgang |
| 0x5f0d | 5F0D - Lenkwinkelsensor: Segment-Finde Algorithmus fand falsches Segment. |
| 0x5f0e | 5F0E - Lenkwinkelsensor: SFA fand kein Segment und Fahrzeuggeschw. &gt; 25 km/h - Temporaerer Fehler. |
| 0x5f16 | 5F16 - DSC-ECU: ECU-intern: Radgeschwindigkeit von Hauptprozessor und Coprozessor stimmen nicht ueberein. |
| 0x5f17 | 5f17 - ECU-Fehler: High-end-timer (HET) - Fehler aufgetreten |
| 0x5f18 | 5f18 - Variantencodierung: EEPROM Konfiguration FZR: Anhaenger-Schlinger-Logik (Tol)_Wert in EEPROM ungueltig |
| 0x5f1a | 5f1a - Infoeintrag: CUS: Fahrleistungsreduzierung durch DSC-Befehl aktiv. |
| 0x5f1b | 5f1b - Infoeintrag: CUS: Fahrleistungsreduzierung durch DSC-Befehl abgeschaltet. |
| 0x5f1c | 5f1c - Infoeintrag: CUS: Aktiver Bremseneingriff waehrend ueberhitzten Bremsscheiben. |
| 0x5f1d | 5f1d - Motronic-Fehler: DME Momenteingriff nicht moeglich (STAT_MD_E=3). |
| 0x5f1e | 5f1e - Variantencodierung: Infoeintrag : Anhaenger-Schlinger-Logik ueber EEPROM deaktiviert. |
| 0x5f20 | 5F20 - DSC-Software: ECU-intern: Software fordert vollstaendiges Abschalten des Systems an. |
| 0x5f21 | 5F21 - DSC-Software: ECU-intern: Software fordert nur EBV Funktion an. |
| 0x5f22 | 5F22 - DSC-Software: ECU-intern: Software fordert nur ABS Funktion an. |
| 0x5f23 | 5F23 - Variantenkodierung: EEPROM Konfiguration ACB Hba Value im EEPROM nicht gueltig. |
| 0x5f24 | 5f24 - Motronic-Fehler: MdNorm-Signal ungueltig (=0) (CAN-Botschaft DME2, ID 0x329). |
| 0x5f27 | 5F27 - Drucksensor Ci2: Plausibilitaetsfehler. |
| 0x5f28 | 5F28 - Drucksensor: Leitungsfehler des Temperatursignals. - Kurzschluss zu +12V, Masse? |
| 0x5f29 | 5F29 - Drucksensor: Temperatursignal Fehler. Parity failure, Transmission error (Ds-Typ DS5). |
| 0x5f2a | 5F2A - Drucksensor: Temperatursignal ausserhalb Wertebereich (DS-Typ DS5). |
| 0x5f2c | 5f2c - EEPROM Inhalt nicht gueltig. |
| 0x5f30 | 5F30 - DME-Fehler: DME sendet Motordrehzahl=ungueltig. |
| 0x5f31 | 5F31 - DME-Fehler: DME sendet Mittleres_Effektivdrehmoment=ungueltig. |
| 0x5f32 | 5F32 - DME-Fehler: DME sendet Unbearbeitetes_Gaspedal=ungueltig. |
| 0x5f33 | 5F33 - DME-Fehler: Rueckmeldung aus angefordetem DME-Stelleingriff (ASR,MSR) ist Null. |
| 0x5f34 | 5F34 - DME-Fehler: Checksummen- oder Timeout-Fehler der Botschaft TORQUE_1. |
| 0x5f35 | 5F35 - DME-Fehler: Checksummen- oder Timeout-Fehler der Botschaft TORQUE_2. |
| 0x5f36 | 5F36 - DME-Fehler: Checksummen- oder Timeout-Fehler der Botschaft TORQUE_3. |
| 0x5f37 | 5F37 - Bremslichschalter: DME meldet ungueltiges Status des Signals BREMSSCHALTER. |
| 0x5f39 | 5f39 - Verteilergetriebe-ECU: VG-Kupplung defekt - Kupplungsposition unbekannt. |
| 0x5f3a | 5f3a - Verteilergetriebe-ECU: VG-Kupplung defekt - Kupplung ist in geoeffneter Position - Heckantrieb! |
| 0x5f3b | 5f3b - Infoeintrag: Verteilergetriebe-ECU: VG-Kupplung: Einbussen Stellgenauigkeit. Unkomfortable Regelung. |
| 0x5f3c | 5f3c - Infoeintrag: Verteilergetriebe-ECU: VG-Kupplung setzt Momentenvorgabe nicht zufriedenstellend um. |
| 0x5f3d | 5f3d - Verteilergetriebe-ECU: VG-Kupplung setzt Momentenvorgabe nicht um : Allradverlust ! |
| 0x5f3e | 5f3e - Verteilergetriebe-ECU: Botschaft DXC3 (ID 0x4FF): Signal_Lamelle sendet Fehlercode. |
| 0x5f3f | 5f3f - Verteilergetriebe-ECU: Botschaft DXC3 (ID 0x4FF): Signal_Kette sendet Fehlercode. |
| 0x5f41 | 5f41 - Infoeintrag: Verteilergetriebe-ECU: DSC-VG-Notlauf aktiv (VG uebernimmt Kupplungsregelung). |
| 0x5f42 | 5f42 - EGS-Fehler: Getriebe im Notlaufmodus. |
| 0x5f43 | 5f43 - EGS-Fehler: Getriebe Abbtriebsdrehzahl sendet Fehlerkennzeichnung. |
| 0x5f44 | 5F44 - Kupplung: Kupplungsschalter niemals gedrueckt. |
| 0x5f45 | 5F45 - Bremsfluessigkeitniveau zu niedrig. |
| 0x5f46 | 5F46 - Kupplung: Kupplungsschalte permanent gedrueckt. |
| 0x5f4d | 5F4D - Variantenkodierung: ASWVARCON lesen nicht moeglich. |
| 0x5f4f | 5F4F - Ventil (USV2): Ventilspannung defekt (Driftfehler) - Leitungsverbindung oder Endstufe defekt? |
| 0x5f50 | 5F50 - Ventile allgemein: Uebertemperatur Fehler. |
| 0x5f51 | 5F51 - Hydraulischer Bremsassistent: EEPROM-Eintrag ungueltig (HFC, HVV). |
| 0x5f52 | 5F52 - CCC/MASK-Fehler: CCC meldet Bedienung_Reifendruckkontrolle ungueltig. |
| 0x5f53 | 5F53 - Hill Descent Control: HDC EEPROM Eintrag ungueltig |
| 0x5f58 | 5f58 - Drehratensensor:  - Controller Release System (CRS) - Fehler bei beabsichtigter Signalstoerung (Dynamic Bite). |
| 0x5f59 | 5f59 - Drehratensensor:  - Controller Release System (CRS) - Fehlerverdacht Yrs bei Signalgradient. |
| 0x5f5a | 5f5a - CAN-Botschaft/Kombi-Fehler: Instr3, ID 0x615: Umgebungstemperatur sendet Fehlerkennzeichnung. |
| 0x5f5b | 5f5b - CAN-Botschaft/Kombi-Fehler: Instr2, ID 0x613: Km_Stand sendet Fehlerkennzeichnung. |
| 0x5f5c | 5f5c - CAN-Botschaft/Kombi-Fehler: Instr3, ID 0x615: Anhaenger-Schlinger-Logik (TOL) wegen fehlender CAN-Botschaft deaktiviert. |
| 0x5f5d | 5F5D - Elektron. Brems-Vorbefuellung: EEPROM-Eintrag der EVB-Funktion ungueltig. |
| 0x5f5e | 5F5E - Bremsscheiben-Wischer: EEPROM Eintrag ungueltig. |
| 0x5f5f | 5F5F - Berg-Anfahrassistent: EEPROM Eintrag ungueltig. |
| 0x5f60 | 5F60 - Variantenkodierungswert passt nicht zum Fahrzeug. |
| 0x5f63 | 5F63 - Lenkwinkelsensor: LWS nicht abgeglichen (LWS-Typ: LWS4,RWDT_STEA_WHL). |
| 0x5f64 | 5F64 - Querbeschleunigungssensor2: Interner Wert ausserhalb Messbereich (Drs2ERRN02). |
| 0x5f65 | 5F65 - Querbeschleunigungssensor2: Interner Selbsttest fehlgeschlagen (Drs2ERRN04). |
| 0x5f66 | 5F66 - Drehratensensor2: DRS2-ID passt nicht zur angefragten ID. |
| 0x5f67 | 5F67 - Drehratensensor2: Checksumme der empfangenen DRS-Botschaften falsch. |
| 0x5f68 | 5F68 - Drehratensensor2: Fehler des ERR- oder TERR-Bits. Keine zusaetzliche Information (ERRNO = 0). |
| 0x5f69 | 5F69 - Drehratensensor2: Interner Gierratenwert ausserhalb Wertebereich (DrsERRNO1). |
| 0x5f6a | 5F6A - Drehratensensor2: Interne Referenzvariable ausserhalb Wertebereich (DrsERRNO3). |
| 0x5f6b | 5F6B - Drehratensensor2: Empfangene Nachricht zu frueh (DrsERRNO5). |
| 0x5f6c | 5F6C - Drehratensensor2: Spannungsversorgung zu niedrig (DrsERRNO6). |
| 0x5f6d | 5F6D - Drehratensensor2: Spannungsversorgung zu hoch (DrsERRNO7). |
| 0x5f6e | 5F6E - Drehratensensor2: Sensor in Initialisierung (DrsERRNO8). |
| 0x5f79 | 5F79 - Anhaengermodul: Anhaenger-Signal ungueltig. |
| 0x5f7a | 5F7A - Drehratensensor: DRS-Fehler dem DRS_1 zugeordnet. |
| 0x5f7b | 5F7B - Drehratensensor: DRS-Fehler dem DRS_2 zugeordnet. |
| 0x60ac | 60ac - RPA-Fehler: Reifenpannenanzeige: Codierdaten unplausibel. |
| 0x60ad | 60ad - RPA-Fehler: Reifenpannenanzeige: Standardisierungsdaten unplausibel. |
| 0x60ae | 60ae - RPA-Fehler: Reifenpannenanzeige: FASTA_Daten unplausibel. |
| 0x6d8c | 6d8c - Rueckfoerder Pumpe: - MRD Versorgungsspannung nicht korrekt. |
| 0x6d94 | 6d94 - DSC-ECU: ECU-intern: Reset status HyFF nicht korrekt. |
| 0x6d95 | 6d95 - DSC-ECU: ECU-intern: ADC Selbsttest-Fehler. |
| 0x6d96 | 6d96 - DSC-ECU: ECU-intern: System IC internal charge pump |
| 0x6d97 | 6d97 - DSC-ECU: ECU-intern: System IC clock in failure. |
| 0x6d98 | 6d98 - DSC-ECU: ECU-intern: System IC watchdog oscillator failure |
| 0x6d9a | 6d9a - Raddrehzahlfuehler Vorne Links: Kurzschluss nach Masse bei Versorgungsleitung oder defekter Sensor. |
| 0x6d9b | 6d9b - Raddrehzahlfuehler Vorne Links: Leitungsunterbrechung, Kurzschluss nach Masse oder defekter Sensor. |
| 0x6d9c | 6d9c - Raddrehzahlfuehler Vorne Links: Kurzschluss nach UBATT oder defekter Sensor. |
| 0x6d9d | 6d9d - Raddrehzahlfuehler Hinten Links: Kurzschluss nach Masse bei Versorgungsleitung oder defekter Sensor. |
| 0x6d9e | 6d9e - Raddrehzahlfuehler Hinten Links: Leitungsunterbrechung, Kurzschluss nach Masse oder defekter Sensor. |
| 0x6d9f | 6d9f - Raddrehzahlfuehler Hinten Links: Kurzschluss nach UBATT oder defekter Sensor. |
| 0x6da0 | 6da0 - Raddrehzahlfuehler Hinten Rechts: Kurzschluss nach Masse bei Versorgungsleitung oder defekter Sensor. |
| 0x6da1 | 6da1 - Raddrehzahlfuehler Hinten Rechts: Leitungsunterbrechung, Kurzschluss nach Masse oder defekter Sensor. |
| 0x6da2 | 6da2 - Raddrehzahlfuehler Hinten Rechts: Kurzschluss nach UBATT oder defekter Sensor. |
| 0x6da3 | 6da3 - Raddrehzahlfuehler Vorne Rechts: Kurzschluss nach Masse bei Versorgungsleitung oder defekter Sensor. |
| 0x6da4 | 6da4 - Raddrehzahlfuehler Vorne Rechts: Leitungsunterbrechung, Kurzschluss nach Masse oder defekter Sensor. |
| 0x6da5 | 6da5 - Raddrehzahlfuehler Vorne Rechts: Kurzschluss nach UBATT oder defekter Sensor. |
| 0x6dc0 | 6DC0 - Drehratensensor: Offset-Kalibrierung nicht moeglich, da Laengsbeschleunigungswert ausserhalb Wertebereich (DRS-Typ MM3x). |
| 0x6dc1 | 6DC1 - Drehratensensor: Fehler waehrend EEProm-Zugriff aufgetreten (DRS-Typ MM3x). |
| 0x6dc2 | 6DC2 - Drehratensensor: Zu viele ungueltige Laengsbeschleunigungswerte waehrend Laengsbeschleunigungs-Kalibrierung aufgetreten (DRS-Typ MM3x). |
| 0x6dc3 | 6DC3 - Drehratensensor: Neuer DRS-Sensor erkannt. Abgespeicherte Seriennummer paßt nicht zu empfangener Seriennr.. |
| 0x6dc4 | 6dc4 - Variantenkodierung: Variantencode ungueltig. |
| 0x6dc9 | 6dc9 - Infoeintrag: Verteilergetriebe-ECU: End-of-line Test laeuft – Erwartetes Ende nach 30 Sek. |
| 0x6dca | 6dca - Verteilergetriebe-ECU: End-of-line Test fehlerhaft. VG-Kupplung nicht betriebsbereit! |
| 0x6dd1 | 6DD1 - DSC-ECU: ECU-intern: falsche HET Geschwindigkeit |
| 0x6dd2 | 6DD2 - DSC-ECU: ECU-intern: falscher HET duty cycle |
| 0x6dd3 | 6dd3 - Raddrehzahlfuehler Vorne Links: Geschwindigkeitsvergleich fehlerhaft. |
| 0x6dd4 | 6dd4 - Raddrehzahlfuehler Hinten Links: Geschwindigkeitsvergleich fehlerhaft. |
| 0x6dd5 | 6dd5 - Raddrehzahlfuehler Hinten Rechts: Geschwindigkeitsvergleich fehlerhaft. |
| 0x6dd6 | 6dd6 - Raddrehzahlfuehler Vorne Rechts: Geschwindigkeitsvergleich fehlerhaft. |
| 0x6dfd | 6DFD - DSC-ECU: ECU-intern: MRG-Status nicht ok |
| 0x6e0d | 6e0d - Drucksensor: Temperatursignal ausserhalb Wertebereich. |
| 0x6e39 | 6e39 - Motronic-Fehler: Q_ASC Timeout aufgetreten. |
| 0x6e3a | 6e3a - Motronic-Fehler: Fehler im Motordrehzahl-Signal (CAN-Botschaft DME1). |
| 0x6e3b | 6e3b - Motronic-Fehler: MotPedalPos sendet Fehlerkennzeichnung FFh (CAN-Botschaft DME2). |
| 0x6e3c | 6e3c - Motronic-Fehler: Tempomatanforderung im HDC kann nicht gestellt werden. |
| 0x6e3d | 6e3d - Lenkwinkelsensor: interner Fehler : Signal ungueltig. |
| 0x6e3e | 6e3e - Lenkwinkelsensor: LWS - Signal relativ. Lenkrad-Mittenstellung unbekannt. Lernquadrant. |
| 0x6e3f | 6e3f - Lenkwinkelsensor: LWS - nicht Initialisiert, (empfangene id Null). |
| 0x6e40 | 6e40 - Lenkwinkelsensor: LWS - Empfangene id ungleich letztem DSC-LWS-Abgleich. |
| 0x6e43 | 6e43 - CAN-Botschaft/DSC-Fehler: Botschaft ASC1 (ID 0x153) nicht abgeschickt (XMT) (von DSC-ECU gesendet). |
| 0x6e44 | 6e44 - CAN-Botschaft/DSC-Fehler: Botschaft ASC2 (ID 0x1F0) nicht abgeschickt (XMT) (von DSC-ECU gesendet). |
| 0x6e45 | 6e45 - CAN-Botschaft/DSC-Fehler: Botschaft ASC4 (ID 0x1F8) nicht abgeschickt (XMT) (von DSC-ECU gesendet). |
| 0x6e46 | 6e46 - CAN-Botschaft/DSC-Fehler: Botschaft DSC1 (ID 0x190) nicht abgeschickt (XMT) (von DSC-ECU gesendet). |
| 0x6e58 | 6E58 - Infoblock von Drehratensensor nicht empfangen. |
| 0x6e74 | 6e74 - CAN-Botschaft/DSC-Fehler: Botschaft ASC5 (ID 0x2B3) nicht abgeschickt (XMT) (von DSC-ECU gesendet). |
| 0x6f4b | 6F4B - LDM-Fehler: Alive-Fehler. |
| 0x6f58 | 6F58 - CAN-Botschaft/DME-Fehler: Motronic - Botschaft DME1 (ID 0x316) fehlt (RCV) (von DSC-ECU empfangen). |
| 0x6f59 | 6F59 - CAN-Botschaft/DME-Fehler: Motronic - Botschaft DME2 (ID 0x329) fehlt (RCV) (von DSC-ECU empfangen). |
| 0x6f5a | 6F5A - CAN-Botschaft/DME-Fehler: Motronic - Botschaft DME4 (ID 0x545) fehlt (RCV) (von DSC-ECU empfangen). |
| 0x6f5b | 6F5B - CAN-Botschaft/LWS-Fehler: Botschaft LWS1 (ID 0x1F5) fehlt (RCV) (von DSC-ECU empfangen). |
| 0x6f5c | 6F5C - CAN-Botschaft/Kombi-Fehler: Botschaft Instrumentkombi INSTR2 (ID 0x613) fehlt (RCV) (von DSC-SG empfangen). |
| 0x6f5d | 6F5D - CAN-Botschaft/Kombi-Fehler: Botschaft Instrumentkombi INSTR3 (ID 0x615) fehlt (RCV) (von DSC-SG empfangen). |
| 0x6f5f | 6F5F - CAN-Botschaft/VG-Fehler: Botschaft DXC3 (ID 0x4FF)  fehlt (RCV) (von DSC-ECU empfangen). |
| 0xd347 | D347 - CAN-Bus-Fehler: CAN Initialisierungs- oder BusOff-Fehler - CAN Leitungsunterbrechung oder Kurzschluss ? |
| 0xd34c | D34C - PT-CAN: Allg. CAN Fehler. CAN1 passiv. |
| 0xd354 | D354 - CAN-Botschaft/DME-Fehler: Motronic - Botschaft DME1 (ID 0x316) fehlt (RCV) (von DSC-ECU empfangen). |
| 0xd355 | D355 - CAN-Botschaft/DME-Fehler: Motronic - Botschaft DME2 (ID 0x329) fehlt (RCV) (von DSC-ECU empfangen). |
| 0xd356 | D356 - CAN-Botschaft/DME-Fehler: Motronic - Botschaft DME4 (ID 0x545) fehlt (RCV) (von DSC-ECU empfangen). |
| 0xd357 | D357 - CAN-Botschaft/LWS-Fehler: Botschaft LWS1 (ID 0x1F5) fehlt (RCV) (von DSC-ECU empfangen). |
| 0xd358 | D358 - CAN-Botschaft/EGS-Fehler: Getriebe - Botschaft EGS1 (ID 0x43F) fehlt (RCV) (von DSC-ECU empfangen). |
| 0xd359 | D359 - CAN-Botschaft/Kombi-Fehler: Botschaft Instrumentkombi INSTR2 (ID 0x613) fehlt (RCV) (von DSC-SG empfangen). |
| 0xd35a | D35A - CAN-Botschaft/Kombi-Fehler: Botschaft Instrumentkombi INSTR3 (ID 0x615) fehlt (RCV) (von DSC-SG empfangen). |
| 0xd35c | D35C - CAN-Botschaft/VG-Fehler: Verteilergetriebe - Botschaft DXC1 (ID 0x192) fehlt (RCV) (von DSC-ECU empfangen). |
| 0xd35f | D35f - CAN-Botschaft/VG-Fehler: Botschaft DXC3 (ID 0x4FF)  fehlt (RCV) (von DSC-ECU empfangen). |
| 0xd36a | D36A - CAN-Botschaft/VG-Fehler: Verteilergetriebe - Botschaft DXC1 (ID 0x192) fehlt (RCV) (von DSC-ECU empfangen). |
| 0xd36f | D36F - PT-CAN: Botschaft CLU1_VDA (ID 0xD8) nicht empfangen oder falsch Botschaftslaenge (DLC) [Sender: DRS] -  Spgs.versorgung DRS defekt? |
| 0xd370 | D370 - PT-CAN: Botschaft CLU2_VDA (0xE3) nicht empfangen oder falsche Botschaftslaenge (DLC). [Sender: DRS] - Spgs.versorgung DRS defekt? |
| 0xd371 | D371 - PT-CAN: Botschaft CLU3_VDA (0xF4) nicht empfangen oder falsche Botschaftslaenge. [Sender: DRS] - Spgs.versorgung DRS defekt? |
| 0xd372 | D372 - PT-CAN: Botschaft CLU_St_VDA (ID 0x165) nicht empfangen oder falsche Botschaftslaenge (DLC). [Sender: DRS] - Spgs.versorgung DRS defekt? |
| 0xd375 | D375 - Drehratensensor: CAN-Botschaftszaehler meldet Fehler (DRS Typ MM 3.x). |
| 0xd376 | D376 - Drehratensensor: CAN-Botschaftszaehler meldet Fehler (DRS Typ MM 3.x). |
| 0xd377 | D377 - Drehratensensor: CAN-Botschaftszaehler meldet Fehler (DRS Typ MM 3.x). |
| 0xd378 | D378 - Drehratensensor: CAN-Botschaftszaehler meldet Fehler (DRS Typ MM 3.x). |
| 0xd379 | D379 - Drehratensensor: Checksumme der Botschaft ist falsch (DRS Typ MM 3.x). |
| 0xd37a | D37A - Drehratensensor: Checksumme der Botschaft ist falsch (DRS Typ MM 3.x). |
| 0xd37b | D37B - Drehratensensor: Checksumme der Botschaft ist falsch (DRS Typ MM 3.x). |
| 0xd37c | D37C - Drehratensensor: Checksumme der Botschaft ist falsch (DRS Typ MM 3.x). |
| 0xd383 | D383 - LDM: Checksummen-Fehler. |
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
| default | 0x01 | DIGITAL | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 9 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Fahrzeuggeschwindigkeit | km/h | High | unsigned int | - | 0.05625 | 1 | 0 |
| 0x02 | ACB | 0/1 | - | 0x01 | - | 1 | 1 | 0 |
| 0x03 | HBA | 0/1 | - | 0x02 | - | 1 | 1 | 0 |
| 0x04 | ECD | 0/1 | - | 0x04 | - | 1 | 1 | 0 |
| 0x05 | HDC | 0/1 | - | 0x08 | - | 1 | 1 | 0 |
| 0x06 | DSC | 0/1 | - | 0x10 | - | 1 | 1 | 0 |
| 0x07 | ABS | 0/1 | - | 0x20 | - | 1 | 1 | 0 |
| 0x08 | BLS | 0/1 | - | 0x40 | - | 1 | 1 | 0 |
| 0x09 | ASC | 0/1 | - | 0x80 | - | 1 | 1 | 0 |

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

<a id="table-digital"></a>
### DIGITAL

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08 | 0x09 |

<a id="table-stg-tabelle"></a>
### STG_TABELLE

Dimensions: 18 rows × 4 columns

| SIGNAL | KANAL | HB | LB |
| --- | --- | --- | --- |
| MRA | 0x22 | 0xFF | 0xFF |
| EVVL | 0x30 | 0x00 | 0x55 |
| AVVL | 0x32 | 0x00 | 0x64 |
| EVVR | 0x34 | 0x00 | 0x55 |
| AVVR | 0x36 | 0x00 | 0x64 |
| EVHR | 0x38 | 0x00 | 0x55 |
| AVHR | 0x3A | 0x00 | 0x64 |
| EVHL | 0x3C | 0x00 | 0x55 |
| AVHL | 0x3E | 0x00 | 0x64 |
| USV1 | 0x4E | 0x00 | 0x32 |
| USV2 | 0x50 | 0x00 | 0x32 |
| VLV1 | 0x52 | 0x00 | 0x55 |
| VLV2 | 0x54 | 0x00 | 0x55 |
| 40VLV1 | 0x52 | 0x00 | 0x28 |
| 40VLV2 | 0x54 | 0x00 | 0x28 |
| ACC | 0x98 | 0xFF | 0xFF |
| 0 | 0x00 | 0x00 | 0x00 |
| 00 | 0x00 | 0x00 | 0x00 |

<a id="table-steuern-i-o-ein"></a>
### STEUERN_I_O_EIN

Dimensions: 19 rows × 4 columns

| SIGNAL | KANAL | HB | LB |
| --- | --- | --- | --- |
| MRA | 0x22 | 0xFF | 0xFF |
| ACC | 0x98 | 0xFF | 0xFF |
| EVVL | 0x28 | 0x60 | 0x01 |
| AVVL | 0x2A | 0x60 | 0x02 |
| EVVR | 0x28 | 0x60 | 0x04 |
| AVVR | 0x2A | 0x60 | 0x08 |
| EVHL | 0x28 | 0x60 | 0x10 |
| AVHL | 0x2A | 0x60 | 0x20 |
| EVHR | 0x28 | 0x60 | 0x40 |
| AVHR | 0x2A | 0x60 | 0x80 |
| USV1 | 0x2C | 0x32 | 0x01 |
| USV2 | 0x2C | 0x32 | 0x02 |
| VLV1 | 0x2E | 0x60 | 0x04 |
| VLV2 | 0x2E | 0x60 | 0x08 |
| 40VLV1 | 0x2E | 0x28 | 0x04 |
| 40VLV2 | 0x2E | 0x28 | 0x08 |
| 0 | 0x00 | 0x00 | 0x00 |
| 00 | 0x00 | 0x00 | 0x00 |
| XYZ | 0x00 | 0x00 | 0x00 |

<a id="table-steuern-i-o-aus"></a>
### STEUERN_I_O_AUS

Dimensions: 17 rows × 4 columns

| SIGNAL | KANAL | HB | LB |
| --- | --- | --- | --- |
| MRA | 0x22 | 0x00 | 0x00 |
| ACC | 0x98 | 0x00 | 0x00 |
| EVVL | 0x28 | 0x00 | 0x01 |
| AVVL | 0x2A | 0x00 | 0x02 |
| EVVR | 0x28 | 0x00 | 0x04 |
| AVVR | 0x2A | 0x00 | 0x08 |
| EVHL | 0x28 | 0x00 | 0x10 |
| AVHL | 0x2A | 0x00 | 0x20 |
| EVHR | 0x28 | 0x00 | 0x40 |
| AVHR | 0x2A | 0x00 | 0x80 |
| USV1 | 0x2C | 0x00 | 0x01 |
| USV2 | 0x2C | 0x00 | 0x02 |
| VLV1 | 0x2E | 0x00 | 0x04 |
| VLV2 | 0x2E | 0x00 | 0x08 |
| 0 | 0x00 | 0x00 | 0x00 |
| 00 | 0x00 | 0x00 | 0x00 |
| XYZ | 0x00 | 0x00 | 0x00 |

<a id="table-rad-nr-tabelle"></a>
### RAD_NR_TABELLE

Dimensions: 4 rows × 3 columns

| SIGNAL | BYTE | BYTE_REPAIR |
| --- | --- | --- |
| V_LINKS | 0xA0 | 0x23 |
| V_RECHTS | 0xA2 | 0x24 |
| H_RECHTS | 0xA4 | 0x25 |
| H_LINKS | 0xA6 | 0x22 |

<a id="table-raddrehrichtung"></a>
### RADDREHRICHTUNG

Dimensions: 7 rows × 6 columns

| BIT | DREHRICHTUNG_VL_TEXT | DREHRICHTUNG_VR_TEXT | DREHRICHTUNG_HL_TEXT | DREHRICHTUNG_HR_TEXT | WERT |
| --- | --- | --- | --- | --- | --- |
| 0x00 | rueckwaerts | rueckwaerts | rueckwaerts | rueckwaerts | 2 |
| 0x01 |  |  |  | vorwaerts | 1 |
| 0x02 |  |  | vorwaerts |  | 1 |
| 0x04 |  | vorwaerts |  |  | 1 |
| 0x08 | vorwaerts |  |  |  | 1 |
| 0xFF | steht | steht | steht | steht | 0 |
| 0xXY | nicht_definiert | nicht_definiert | nicht_definiert | nicht_definiert | 99 |

<a id="table-codierung"></a>
### CODIERUNG

Dimensions: 18 rows × 5 columns

| FUNKTION | BLOCK | BYTE | MASKE | DEFAULT |
| --- | --- | --- | --- | --- |
| ECD | 0x3005 | 0x00 | 0x01 | 0x01 |
| FLR | 0x3005 | 0x00 | 0x10 | 0x00 |
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
