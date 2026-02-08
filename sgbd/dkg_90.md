# dkg_90.prg

- Jobs: [94](#jobs)
- Tables: [197](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | DKG_90 |
| ORIGIN | BMW EA-504 Andreas_Senft |
| REVISION | 5.002 |
| AUTHOR | ESG EA-504 Pascal_Bilang, BMW EA-504 Andreas_Senft, BMW TI-430  |
| COMMENT | N/A |
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
- [FS_SPERREN](#job-fs-sperren) - Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [HS_LESEN](#job-hs-lesen) - Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default
- [HS_LESEN_DETAIL](#job-hs-lesen-detail) - Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default
- [HS_LOESCHEN](#job-hs-loeschen) - Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
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
- [STATUS_COMPILER_BOOTLOADER](#job-status-compiler-bootloader) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des MPC-Bootloader KWP 2000: $21 ReadDataByLocalIdentifier $A0 status_compiler_bootloader
- [STATUS_COMPILER_APPLIKATION](#job-status-compiler-applikation) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung der Applikation KWP 2000: $21 ReadDataByLocalIdentifier $A1 status_compiler_applikation
- [STATUS_COMPILER_DAF](#job-status-compiler-daf) - Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des DAF KWP 2000: $21 ReadDataByLocalIdentifier $A3 status_compiler_daf
- [STATUS_SG_SERIENNUMMER](#job-status-sg-seriennummer) - Auslesen der Temic SG ID  KWP 2000: $21 ReadDataByLocalIdentifier $FA status_temic_hw_seriennummer
- [CODIERDATEN_LESEN](#job-codierdaten-lesen) - Codierdaten lesen ( Service ID 0x22,Identifier 0x10,0x02 )
- [CODIERDATEN_SCHREIBEN](#job-codierdaten-schreiben) - Codierung schreiben (Service ID 0x2E, Identifier 0x10,0x02)
- [STATUS_ENERGIESPARMODE_LESEN](#job-status-energiesparmode-lesen) - Auslesen der Energiesparmodi ( Service ID 0x22, Identifier 0x10, 0x0A )
- [STATUS_ENERGIESPARMODE](#job-status-energiesparmode) - Auslesen des Energiesparmodes ( Service ID 0x22, Identifier 0x10, 0x0A )
- [STATUS_INITIALISIERUNG](#job-status-initialisierung) - ( Service ID 0x30, Identifier 0xA0 )
- [STATISTIKDATENSATZ_1_LESEN](#job-statistikdatensatz-1-lesen) - Statistikdatensatz 1 lesen ( Service ID 0x21, Identifier 0x01 )
- [STATISTIKDATENSATZ_2_LESEN](#job-statistikdatensatz-2-lesen) - Statistikdatensatz 2 lesen ( Service ID 0x21, Identifier 0x02 )
- [STATISTIKDATEN_LOESCHEN](#job-statistikdaten-loeschen) - Verschleissdaten loeschen ( Service ID 0x2E, Identifier 0x1001 )  
- [STATUS_ISTWERTE_LESEN](#job-status-istwerte-lesen) - ( Service ID 0x30, Identifier 0x01, 0x01 )
- [STATUS_ROHWERTE_LESEN](#job-status-rohwerte-lesen) - ( Service ID 0x30, Identifier 0x02, 0x01 )
- [STEUERN_STELLGLIED](#job-steuern-stellglied) - ( Service ID 0x30, Identifier 0x07 ) Eine Stellgliedeingabe mit Stellgliedwert werden über IO-Hex Eingabewert eingegeben  Es ist nur möglich Ausgänge anzusteuern, wenn kein Test- und Einlernprogramm aktiv ist. ACHTUNG: Bei der Ansteuerung Magnetventile (PV1-4, PV6, PV7 und SV1-4) wird das SG in einen sogenannten Prüfstandmode versetzt, bei dem dann unabhängig von der Ausgangssituation alle Magnetventile, bis auf den der angesteuert werden soll, auf den Sollwert 0 eingestellt.  WARNUNG: Der Bediener des Diagnosetesters ist für die Sicherheit von Leib und Leben sowie für den Schutz aller Bauteile, die im Zusammenhang mit der SG-Ausgangsansteuerung stehen, verantwortlich. Es ist nicht auszuschließen, dass sich das Fahrzeug durch eine unsachgemäße Ansteuerung fortbewegt. Nach Möglichkeit sollte sich das Fahrzeug während der Ausgangsansteuerung auf einer Hebebühne befinden, so dass es sich nicht fortbewegen kann.  STELLGLIED_IO_HEX                          STELLGLIED_WERT 0x20 = Sollstrom Magnetventil PV1 -     Min: 0 Max: 1900 0x21 = Sollstrom Magnetventil PV2 -     Min: 0 Max: 1900 0x22 = Sollstrom Magnetventil PV3 -     Min: 0 Max: 1900 0x23 = Sollstrom Magnetventil PV4 -     Min: 0 Max: 1900 0x24 = Sollstrom Magnetventil PV6 -     Min: 0 Max: 1900 0x25 = Sollstrom Magnetventil PV7 -     Min: 0 Max: 1900 0x26 = Sollzustand Magnetventil SV1 -   Min: 0 Max: 1 0x27 = Sollzustand Magnetventil SV2 -   Min: 0 Max: 1 0x28 = Sollzustand Magnetventil SV3 -   Min: 0 Max: 1 0x29 = Sollzustand Magnetventil SV4 -   Min: 0 Max: 1 0x2A = Parksperre verriegeln - 0= keine Reaktion  1= PS verriegeln  2= PS entriegeln 0x2B = Anzeige Programminformation (Statusausgang CAN ) -    Min: 1 Max: 6 0x2C = Getriebe nach Neutral stellen -  Ein: 1 0x2D = Parksperre Hakentest -           Ein: 1 Aus: 0 0x2E = Parksperre Magnettest -          Ein: 1 0x2F = Ansteuerung Parksperre aus/ein - 0= Parksperre ausgelegt - 1= Parksperre eingelegt 0x30 = Anzeige Wahlhebelschema -        Min: 1 Max: 4 0x31 = Anzeige Gänge -                  Min: 1 Max: 7 0x32 = Anzeige CC Meldung -             An: 1  Aus: 0 weiter Information im LH - Diagnoseschnittstelle
- [STEUERN_STELLGLIED_ZURUECKSETZEN](#job-steuern-stellglied-zuruecksetzen) - ( Service ID 0x30, Identifier 0x00 ) STELLGLIED_IO_HEX 0x20 = Sollstrom Magnetventil PV1 0x21 = Sollstrom Magnetventil PV2 0x22 = Sollstrom Magnetventil PV3 0x23 = Sollstrom Magnetventil PV4 0x24 = Sollstrom Magnetventil PV5 0x25 = Sollstrom Magnetventil PV6 0x26 = Sollzustand Magnetventil SV1 0x27 = Sollzustand Magnetventil SV2 0x28 = Sollzustand Magnetventil SV3 0x29 = Sollzustand Magnetventil SV4 0x2A = Parksperre verriegeln 0x2B = Anzeige Programminformation 0x2C = Getriebe nach Neutral 0x2D = Parksperre Hakentest 0x2E = Ansteuerung Parksperre 0x30 = Anzeige Wahlhebelschema 0x31 = Anzeige Gaenge 0x32 = Anzeige CC Meldung 0xFE = Alle Ausgangsgrößen weiter Information im LH - Diagnoseschnittstelle
- [STEUERN_TESTPRG_STARTEN](#job-steuern-testprg-starten) - Test- und Einlernprogramm starten ( Service ID 0x31, Identifier 0x20-0x27 + 0x30-0x35) WARNUNG: Weil die Diagnoseschnittstelle ein Event gesteuertes Modul in der Getriebesoftware darstellt, können Test- und Einlernprogramme nur durch den Bediener, in diesem Fall durch den Diagnosetester, ein- und ausgeschaltet bzw. abgefragt werden. Anderenfalls sind Zustände möglich, die nur durch das Abschalten der Kl.15 und das anschließende Abwarten des Steuergerätenachlaufs verlassen werden können.
- [STATUS_TESTPRG_ISTZUSTAND](#job-status-testprg-istzustand) - Test- und Einlernprogramm abfragen ( Service ID 0x33, Identifier 0x20-0x27 + 0x30-0x35) WARNUNG: Das Einschalten,Ausschalten und Abfragen von Test- und Einlernprogramm darf NUR über eines Diagnosetester erfolgen!
- [STEUERN_TESTPRG_STOP](#job-steuern-testprg-stop) - Test- und Einlernprogramm beenden ( Service ID 0x32, Identifier 0x20 - 0x27, 0x30 - 0x35 ) WARNUNG: Das Einschalten,Ausschalten und Abfragen von Test- und Einlernprogramm darf NUR über eines Diagnosetester erfolgen!
- [STATUS_RBM_RATIO_LESEN](#job-status-rbm-ratio-lesen) - Dient zum Aulesen der OBD fehlerbezogenen RBM Ratios Dabei wird die Häufigkeit des Durchlaufens von abgasrelevanten Diagnosefunktionen gezählt ( Service ID 0x22, Identifier 0x52, 0x00 )
- [PRUEFCODE_LESEN](#job-pruefcode-lesen) - Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes ---------------- Zusätzlich für VS: --------------------- KWP2000: $30 A8 STATUS_GETRIEBE_TEACHEN KWP2000: $30 A4 STATUS_VENTILKENNLINIE_PV1 KWP2000: $30 A5 STATUS_VENTILKENNLINIE_PV2 KWP2000: $30 A6 STATUS_VENTILKENNLINIE_PV6 KWP2000: $30 A0 STATUS_ADAPTION_KUPPLUNGSSCHLEIFPUNKT_K1 KWP2000: $30 A1 STATUS_ADAPTION_KUPPLUNGSSCHLEIFPUNKT_K2 KWP2000: $30 A2 STATUS_ADAPTION_MOMENTENKENNLINIE_K1 KWP2000: $30 A3 STATUS_ADAPTION_MOMENTENKENNLINIE_K2 KWP2000: $30 A7 STATUS_SPERRSTELLUNG_PV7 KWP2000: $30 AA STATUS_ADAPTIONSWERT_PV6 KWP2000: $21 01 STATISTIKDATENSATZ_1_LESEN KWP2000: $21 02 STATISTIKDATENSATZ_2_LESEN Modus  : Default
- [DEBUGGING_INFORMATION](#job-debugging-information) - Einlernwert Sperrstellung PV7 ( Service ID 0x21, Identifier 0xFD ) Debugging Information
- [STATUS_GETRIEBE_TEACHEN](#job-status-getriebe-teachen) - Einlernwerte Getriebe Teachen ( Service ID 0x30, Identifier 0xA8 )
- [STATUS_ADAPTION_KUPPLUNGSSCHLEIFPUNKT_K1](#job-status-adaption-kupplungsschleifpunkt-k1) - Adaptionswerte Kupplungsschleifpunkt K1 ( Service ID 0x30, Identifier 0xA0 )
- [STATUS_ADAPTION_KUPPLUNGSSCHLEIFPUNKT_K2](#job-status-adaption-kupplungsschleifpunkt-k2) - Adaptionswerte Kupplungsschleifpunkt K2 ( Service ID 0x30, Identifier 0xA1 )
- [STATUS_ADAPTION_MOMENTENKENNLINIE_K1](#job-status-adaption-momentenkennlinie-k1) - Adaptionswerte Kupplungsmomentenkennlinie K1 ( Service ID 0x30, Identifier 0xA2 )
- [STATUS_ADAPTION_MOMENTENKENNLINIE_K2](#job-status-adaption-momentenkennlinie-k2) - Adaptionswerte Kupplungsmomentenkennlinie K2 ( Service ID 0x30, Identifier 0xA3 )
- [STATUS_VENTILKENNLINIE_PV1](#job-status-ventilkennlinie-pv1) - Einlernwerte Ventilkennlinie PV1 ( Service ID 0x30, Identifier 0xA4 )
- [STATUS_VENTILKENNLINIE_PV2](#job-status-ventilkennlinie-pv2) - Einlernwerte Ventilkennlinie PV2 ( Service ID 0x30, Identifier 0xA5 )
- [STATUS_ADAPTIONSWERT_VENTILKENNLINIE_PV1_PV2](#job-status-adaptionswert-ventilkennlinie-pv1-pv2) - Adaptionswert für PV1 und PV2 Ventilkennlinie ( Service ID 0x30, Identifier 0xB0 )
- [STATUS_VENTILKENNLINIE_PV6](#job-status-ventilkennlinie-pv6) - Einlernwerte Ventilkennlinie PV6 ( Service ID 0x30, Identifier 0xA6 )
- [STATUS_ADAPTIONSWERT_PV6](#job-status-adaptionswert-pv6) - Adaptionswerte  PV6 ( Service ID 0x30, Identifier 0xAA )
- [STATUS_SPERRSTELLUNG_PV7](#job-status-sperrstellung-pv7) - Einlernwert Sperrstellung PV7 ( Service ID 0x30, Identifier 0xA7 )
- [STATUS_ADAPTIONSWERT_GETRIEBECODE](#job-status-adaptionswert-getriebecode) - Adaptionswerte  für den Getriebecode ( Service ID 0x30, Identifier 0xAB )
- [STATUS_ADAPTIONSWERT_RADSATZVARIANTE](#job-status-adaptionswert-radsatzvariante) - Adaptionswert  für die Radsatzvariante ( Service ID 0x30, Identifier 0xAC )
- [STATUS_ADAPTIONSWERT_HYDRAULIKPUMPE](#job-status-adaptionswert-hydraulikpumpe) - Adaptionswert für die Hydraulikpumpe ( Service ID 0x30, Identifier 0xAD )
- [STATUS_ADAPTIONSWERT_TEMPERATURSENSOR](#job-status-adaptionswert-temperatursensor) - Adaptionswert für den Temperatursensor Abspritzöl (Typ) ( Service ID 0x30, Identifier 0xAE )
- [STATUS_ADAPTIONSWERT_TEMPERATURSENSOR_WIDERSTAND](#job-status-adaptionswert-temperatursensor-widerstand) - Adaptionswert für den Temperatursensor Abspritzöl Pull-Up-Wiederstandswert ( Service ID 0x30, Identifier 0xAF )
- [STATUS_ADAPTIONSWERT_TEMP_SENSOR_WIDERSTAND](#job-status-adaptionswert-temp-sensor-widerstand) - Adaptionswert für den Temperatursensor Abspritzöl Pull-Up-Wiederstandswert ( Service ID 0x30, Identifier 0xAF )
- [SOFTWARE_VERSION_LESEN](#job-software-version-lesen) - Adaptionswerte Software Version ( Service ID 0x30, Identifier 0xA9 )
- [STATUS_ADAPTIONSWERTE_SEMISCHLUPF_GAENGE](#job-status-adaptionswerte-semischlupf-gaenge) - Adaptionswerte  für den Getriebecode ( Service ID 0x30, Identifier 0xB2 )
- [STATUS_ADAPTIONSWERTE_DRM](#job-status-adaptionswerte-drm) - Adaptionswerte DRM ( Service ID 0x30, Identifier 0xB1 )
- [STEUERN_ADAPTIONSWERTE_PV1_SCHREIBEN](#job-steuern-adaptionswerte-pv1-schreiben) - Einlernwerte Ventilkennlinie PV1 ( Service ID 0x30, Identifier 0xA4 )
- [STEUERN_ADAPTIONSWERTE_PV2_SCHREIBEN](#job-steuern-adaptionswerte-pv2-schreiben) - Einlernwerte Ventilkennlinie PV2 ( Service ID 0x30, Identifier 0xA5 )
- [STEUERN_ADAPTIONSWERTE_PV6_SCHREIBEN](#job-steuern-adaptionswerte-pv6-schreiben) - Einlernwerte Ventilkennlinie PV6 ( Service ID 0x30, Identifier 0xA5 )
- [STEUERN_ADAPTIONSWERTE_PV7_SCHREIBEN](#job-steuern-adaptionswerte-pv7-schreiben) - Einlernwerte Ventilkennlinie PV7 ( Service ID 0x30, Identifier 0xA5 )
- [STEUERN_ADAPTIONSWERT_GETRIEBECODE_SCHREIBEN](#job-steuern-adaptionswert-getriebecode-schreiben) - Adaptionswerte für den Getriebecode ( Service ID 0x30, Identifier 0xAB )
- [STEUERN_ADAPTIONSWERT_RADSATZVARIANTE_SCHREIBEN](#job-steuern-adaptionswert-radsatzvariante-schreiben) - Adaptionswert  für die Radsatzvariante ( Service ID 0x30, Identifier 0xAC )
- [STEUERN_ADAPTIONSWERT_HYDRAULIKPUMPE_SCHREIBEN](#job-steuern-adaptionswert-hydraulikpumpe-schreiben) - Adaptionswert für die Hydraulikpumpe ( Service ID 0x30, Identifier 0xAD )
- [STEUERN_ADAPTIONSWERT_TEMPERATURSENSOR_SCHREIBEN](#job-steuern-adaptionswert-temperatursensor-schreiben) - Adaptionswert  für den Temperatursensor (Typ) ( Service ID 0x30, Identifier 0xAE )
- [STEUERN_ADAPTIONSWERT_TEMPERATURSENSOR_WIDERSTAND_SCHREIBEN](#job-steuern-adaptionswert-temperatursensor-widerstand-schreiben) - Adaptionswert für den Temperatursensor Abspritzöl Pull-Up-Wiederstandswert ( Service ID 0x30, Identifier 0xAF )
- [STEUERN_ADAPTION_ZURUECKSETZEN](#job-steuern-adaption-zuruecksetzen) - Adaptionswerte Zurücksetzen ( Service ID 0x30, Identifier 0x04 ) Voraussetzung für ordnungsgemäße Funktion ist, dass man in Anschluss die Zündung abschaltet und den Steuergeräte-Abfall abwartet, damit die Defaultwerte im NVRAM abgespeichert werden.

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

<a id="job-fs-sperren"></a>
### FS_SPERREN

Sperren bzw. Freigeben des Fehlerspeichers KWP2000: $85 ControlDTCSetting Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SPERREN | string | "ja"   -&gt; Fehlerspeicher sperren "nein" -&gt; Fehlerspeicher freigeben table DigitalArgument TEXT |
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

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory

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

Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Infocode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt. Es darf dann nicht argument F_POS angegeben werden |
| F_POS | int | gewaehlter Eintrag Wenn dieser Parameter angegeben wird, wird die Position benutzt. Wertebereich 1 - 255 Es darf dann nicht argument F_CODE angegeben werden |

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

<a id="job-hs-lesen"></a>
### HS_LESEN

Historyspeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2100 HistoryMemory Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table HOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hs-lesen-detail"></a>
### HS_LESEN_DETAIL

Historypeicher lesen (alle History-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2101 - $21FF HistoryMemoryEntry Modus: Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Historycode Wenn dieser Parameter angegeben wird, wird die Position automatisch ermittelt. Es darf dann nicht argument F_POS angegeben werden |
| F_POS | int | gewaehlter Eintrag Wenn dieser Parameter angegeben wird, wird die Position benutzt. Wertebereich 1 - 255 Es darf dann nicht argument F_CODE angegeben werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| F_VERSION | int | Typ des Fehlerspeichers Fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text table HOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text table HArtTexte ARTTEXT |
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

<a id="job-hs-loeschen"></a>
### HS_LOESCHEN

Historyspeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $03 ClearHistoryMemory Modus  : Default

_No arguments._

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

<a id="job-status-compiler-bootloader"></a>
### STATUS_COMPILER_BOOTLOADER

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des MPC-Bootloader KWP 2000: $21 ReadDataByLocalIdentifier $A0 status_compiler_bootloader

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSSYSTEM | string | Betriebssystem der Workstation |
| STAT_USER | string | Bearbeiter |
| STAT_PC | string | Name der Workstation, dort wurde der Stand uebersetzt |
| STAT_DATUM | string | Compilerdatum, an diesem Tag wurde der Stand uebersetzt |
| STAT_ZEIT | string | Compilerzeit, zu dieser Zeit wurde der Stand uebersetzt |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-compiler-applikation"></a>
### STATUS_COMPILER_APPLIKATION

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung der Applikation KWP 2000: $21 ReadDataByLocalIdentifier $A1 status_compiler_applikation

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSSYSTEM | string | Betriebssystem der Workstation |
| STAT_USER | string | Bearbeiter |
| STAT_PC | string | Name der Workstation, dort wurde der Stand uebersetzt |
| STAT_DATUM | string | Compilerdatum, an diesem Tag wurde der Stand uebersetzt |
| STAT_ZEIT | string | Compilerzeit, zu dieser Zeit wurde der Stand uebersetzt |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-compiler-daf"></a>
### STATUS_COMPILER_DAF

Auslesen der Compilerdaten des SW-Standes Infos über die Erstellung des DAF KWP 2000: $21 ReadDataByLocalIdentifier $A3 status_compiler_daf

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_BETRIEBSSYSTEM | string | Betriebssystem der Workstation |
| STAT_USER | string | Bearbeiter |
| STAT_PC | string | Name der Workstation, dort wurde der Stand uebersetzt |
| STAT_DATUM | string | Compilerdatum, an diesem Tag wurde der Stand uebersetzt |
| STAT_ZEIT | string | Compilerzeit, zu dieser Zeit wurde der Stand uebersetzt |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sg-seriennummer"></a>
### STATUS_SG_SERIENNUMMER

Auslesen der Temic SG ID  KWP 2000: $21 ReadDataByLocalIdentifier $FA status_temic_hw_seriennummer

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_SG_SERIENNUMMER | string | Temic Steuergeraete ID |
| _TEL_AUFTRAG | binary | Hex-Auftrag von SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-lesen"></a>
### CODIERDATEN_LESEN

Codierdaten lesen ( Service ID 0x22,Identifier 0x10,0x02 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_ROLLENBETRIEB_AKTIV | int | Status Rollenbetrieb Nur fuer M-GmbH (Nur Hinterachse in Rolle fuer Leistungspruefstand) Hinweis: Schaltet sich bei v=35 km/h wieder ab 0=inaktiv, 1=aktiv |
| STAT_RADABRISS_ABSCHALTUNG_AKTIV | int | Nur fuer Linie (um Geberrad-Kurbelwelle einzulernen / DME) Status Radabrissfunktionsabschaltung aktiv Wieder Einschalten (Normalzustand) über Codierdaten schreiben oder Zuendung aus/ein 0=inaktiv, 1=aktiv |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-codierdaten-schreiben"></a>
### CODIERDATEN_SCHREIBEN

Codierung schreiben (Service ID 0x2E, Identifier 0x10,0x02)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CODIERUNG | string | Codierdaten fuer Auswahl: Argument: ROLLENBETRIEB oder    : RADABRISS ==================================================================================  Rollenbetrieb (Nur Hinterachse in Rolle fuer Motorpruefstand) Hinweis: Schaltet sich bei v=35 km/h wieder ab. Radabrissfunktionsabschaltung Bei Adaption des Geberrades (DME) in der Line kann es zum Radabriss kommen. Deshalb abschalten.  ------- Codierung bleibt auch nach Zündungswechsel erhalten! -------  |
| AKTIVIERUNG | int | Argument: 0=inaktiv 1=aktiv |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an das SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-energiesparmode-lesen"></a>
### STATUS_ENERGIESPARMODE_LESEN

Auslesen der Energiesparmodi ( Service ID 0x22, Identifier 0x10, 0x0A )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENERGIESPARMODI_WERT | int | 00 = kein Energiemodie aktiv 01 = Energiemodie für Fertigung 02 = Energiemodie für Transport 04 = Energiemodie für Werkstatt |
| STAT_ENERGIESPARMODI_TEXT | string | siehe Energiesparmodi Wert |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-energiesparmode"></a>
### STATUS_ENERGIESPARMODE

Auslesen des Energiesparmodes ( Service ID 0x22, Identifier 0x10, 0x0A )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENERGIESPARMODE_WERT | int | Ausgabe des Energiesparmodes 00 = kein Energiesparmde gesetzt 01 = Fertigungsmode gesetzt 02 = Transportmode gesetzt 04 = Werkstattmode gesetzt |
| STAT_FERTIGUNGSMODE_EIN | int | 0: Fertigungsmode nicht aktiv 1: Fertigungsmode aktiv |
| STAT_TRANSPORTMODE_EIN | int | 0: Transportmode nicht aktiv 1: Transportmode aktiv |
| STAT_WERKSTATTMODE_EIN | int | 0: Werkstattmode nicht aktiv 1: Werkstattmode aktiv |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-initialisierung"></a>
### STATUS_INITIALISIERUNG

( Service ID 0x30, Identifier 0xA0 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_GETRIEBE_INIT | int | Einlernvorgang Getriebe komplett: 0= nicht eingelernt 1= eingelernt |
| STAT_KUPPLUNGSSCHLEIFPUNKT1_INIT | int | Einlernvorgang Kupplungsschleifpunkt 1: 0= nicht eingelernt 1= eingelernt |
| STAT_KUPPLUNGSSCHLEIFPUNKT2_INIT | int | Einlernvorgang Kupplungsschleifpunkt 1: 0= nicht eingelernt 1= eingelernt |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-statistikdatensatz-1-lesen"></a>
### STATISTIKDATENSATZ_1_LESEN

Statistikdatensatz 1 lesen ( Service ID 0x21, Identifier 0x01 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_FAHRZEUGTYP_WERT | int | 0 = AG Fahrzeug 1 = M Fahrzeug |
| STAT_FAHRZEUGTYP_TEXT | string | AG-Fzg oder M-Fzg |
| ANZ_LOESCHUNGEN_WERT | unsigned int | Anzahl der Löschungen von Verschleißdaten |
| KM_STAND_LETZTER_LOESCHUNG_WERT | unsigned long | Kilometerstand der letzten Löschung der Verschleißdaten |
| ANZ_RENNSTARTS_WERT | unsigned int | Anzahl der Rennstarts |
| ANZ_SCHALTUNG_GANG_1_WERT | unsigned long | Anzahl der ausgeführten Schaltungen: Gang 1 |
| ANZ_SCHALTUNG_GANG_2_WERT | unsigned long | Anzahl der ausgeführten Schaltungen: Gang 2 |
| ANZ_SCHALTUNG_GANG_3_WERT | unsigned long | Anzahl der ausgeführten Schaltungen: Gang 3 |
| ANZ_SCHALTUNG_GANG_4_WERT | unsigned long | Anzahl der ausgeführten Schaltungen: Gang 4 |
| ANZ_SCHALTUNG_GANG_5_WERT | unsigned long | Anzahl der ausgeführten Schaltungen: Gang 5 |
| ANZ_SCHALTUNG_GANG_6_WERT | unsigned long | Anzahl der ausgeführten Schaltungen: Gang 6 |
| ANZ_SCHALTUNG_GANG_7_WERT | unsigned long | Anzahl der ausgeführten Schaltungen: Gang 7 |
| ANZ_SCHALTUNG_GANG_R_WERT | unsigned long | Anzahl der ausgeführten Schaltungen: Gang R |
| ANZ_SMOKIE_BURNOUTS_WERT | unsigned int | Anzahl der Smokie Burnouts |
| ANZ_EINLEGEHAENGER_GANG_1_WERT | unsigned int | Anzahl der Einlegehänger für den 1. Gang |
| ANZ_EINLEGEHAENGER_GANG_2_WERT | unsigned int | Anzahl der Einlegehänger für den 2. Gang |
| ANZ_EINLEGEHAENGER_GANG_3_WERT | unsigned int | Anzahl der Einlegehänger für den 3. Gang |
| ANZ_EINLEGEHAENGER_GANG_4_WERT | unsigned int | Anzahl der Einlegehänger für den 4. Gang |
| ANZ_EINLEGEHAENGER_GANG_5_WERT | unsigned int | Anzahl der Einlegehänger für den 5. Gang |
| ANZ_EINLEGEHAENGER_GANG_6_WERT | unsigned int | Anzahl der Einlegehänger für den 6. Gang |
| ANZ_EINLEGEHAENGER_GANG_7_WERT | unsigned int | Anzahl der Einlegehänger für den 7. Gang |
| ANZ_EINLEGEHAENGER_GANG_R_WERT | unsigned int | Anzahl der Einlegehänger für den Rückwärtsgang |
| AUFENTHALTSDAUER_OELSUMPF_KLEINER_MINUS_30_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich &lt; -30°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_KLEINER_MINUS_30_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich &lt; -30°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_MINUS_30_BIS_MINUS_20_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich -30 bis -20°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_MINUS_30_BIS_MINUS_20_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich -30 bis -20°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_MINUS_20_BIS_MINUS_10_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich -20 bis -10°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_MINUS_20_BIS_MINUS_10_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich -20 bis -10°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_MINUS_10_BIS_0_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich -10 bis 0°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_MINUS_10_BIS_0_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich -10 bis 0°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_0_BIS_10_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 0 bis 10°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_0_BIS_10_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 0 bis 10°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_10_BIS_20_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 10 bis 20°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_10_BIS_20_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 10 bis 20°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_20_BIS_30_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 20 bis 30°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_20_BIS_30_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 20 bis 30°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_30_BIS_40_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 30 bis 40°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_30_BIS_40_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 30 bis 40°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_40_BIS_50_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 40 bis 50°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_40_BIS_50_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 40 bis 50°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_50_BIS_60_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 50 bis 60°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_50_BIS_60_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 50 bis 60°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_60_BIS_70_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 60 bis 70°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_60_BIS_70_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 60 bis 70°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_70_BIS_80_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 70 bis 80°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_70_BIS_80_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 70 bis 80°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_80_BIS_90_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 80 bis 90°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_80_BIS_90_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 80 bis 90°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_90_BIS_100_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 90 bis 100°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_90_BIS_100_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 90 bis 100°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_100_BIS_110_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 100 bis 110°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_100_BIS_110_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 100 bis 110°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_110_BIS_120_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 110 bis 120°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_110_BIS_120_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 110 bis 120°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_120_BIS_130_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 120 bis 130°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_120_BIS_130_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 120 bis 130°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_130_BIS_140_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 130 bis 140°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_130_BIS_140_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 130 bis 140°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_140_BIS_150_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 140 bis 150°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_140_BIS_150_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 140 bis 150°C, Einheit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_150_BIS_160_GRAD_WERT | unsigned long | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 150 bis 160°C, Zeit in Minuten |
| AUFENTHALTSDAUER_OELSUMPF_150_BIS_160_GRAD_EINH | string | Die gesamte Aufenthaltsdauer im Oelsumpf für das Getriebe im das Getriebe im Temperaturbereich 150 bis 160°C, Einheit in Minuten |
| ANZ_FAHRSTUFE_ANFORDERN_OHNE_BREMSE | int | Fahrstufe anfordern ohne Bremse |
| ANZ_R_GANG_ANFORDERN_UEBER_V_SCHWELLE | int | R-Gang anfordern bei Geschwindigkeit  größer Schwelle |
| ANZ_AUTO_P_FAHRZEUGVERLASSEN | int | Auto-P bei Fahrzeugverlassen |
| ANZ_P_ANFORDERN_V_UEBER_SCHWELLE | int | P anfordern bei Geschwindigkeit größer Schwelle |
| STAT_KUPPLUNGSTEMPERATUR_K1_MAX_WERT | int | Maximale Temperatur Kupplung 1 |
| STAT_KUPPLUNGSTEMPERATUR_K1_MAX_EINH | string | Kupplungstemperatur Einheit in [°C] |
| ANZ_K1_MAX_TEMPERATUR | unsigned long | Zähler max. Kupplungstemperatur K1 ( 320ms Ticks ) |
| STAT_KUPPLUNGSTEMPERATUR_K2_MAX_WERT | int | Maximale Temperatur Kupplung 2 |
| STAT_KUPPLUNGSTEMPERATUR_K2_MAX_EINH | string | Kupplungstemperatur Einheit in [°C] |
| ANZ_K2_MAX_TEMPERATUR | unsigned long | Zähler max. Kupplungstemperatur K2 ( 320ms Ticks ) |
| STAT_ABSPRITZSSENSORTEMPERATUR_MAX_WERT | int | Maximale Temperatur des Abspritzsensors |
| STAT_ABSPRITZSSENSORTEMPERATUR_MAX_EINH | string | Abspritzsensor Einheit |
| ANZ_MAX_TEMPERATUR_ABSPRITZSENSOR | unsigned long | Zähler max. Temperatur Abspritzsensor ( 320ms Ticks ) |
| AUFENTHALTSDAUER_FAHRMODUS_1_WERT | unsigned long | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Manuell Normal (E9x) BMW AG Fahrzeug Modi - Manuell / Komfort (E89) M3 Fahrzeug Modi - Manuell Stufe 1 Wert in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_1_EINH | string | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Manuell Normal (E9x) BMW AG Fahrzeug Modi - Manuell / Komfort (E89) M3 Fahrzeug Modi - Manuell Stufe 1 Einheit in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_2_WERT | unsigned long | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Manuell (Sporttaster betätigt) (E9x) BMW AG Fahrzeug Modi - Manuell / Sport (E89) M3 Fahrzeug Modi - Manuell Stufe 2 Wert in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_2_EINH | string | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Manuell (Sporttaster betätigt) (E9x) BMW AG Fahrzeug Modi - Manuell / Sport (E89) M3 Fahrzeug Modi - Manuell Stufe 2 Einheit in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_3_WERT | unsigned long | Aufenthaltsdauer in den einzelnen Fahrmodi:3 BMW AG Fahrzeug Modi - Automatik Normal (E9x) BMW AG Fahrzeug Modi - D-Modus / Komfort (E89) M3 Fahrzeug Modi - Manuell Stufe 3 Wert in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_3_EINH | string | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Automatik Normal (E9x) BMW AG Fahrzeug Modi - D-Modus / Komfort (E89) M3 Fahrzeug Modi - Manuell Stufe 3 Einheit in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_4_WERT | unsigned long | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Automatik (Sporttaster betätigt) (E9x) BMW AG Fahrzeug Modi - D-Modus / Sport (E89) M3 Fahrzeug Modi - Manuell Stufe 4 Wert in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_4_EINH | string | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Automatik (Sporttaster betätigt) (E9x) BMW AG Fahrzeug Modi - D-Modus / Sport (E89) M3 Fahrzeug Modi - Manuell Stufe 4 Einheit in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_5_WERT | unsigned long | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Sportgasse Normal (E9x) BMW AG Fahrzeug Modi - S-Modus / Komfort (E89) M3 Fahrzeug Modi - Manuell Stufe 5 Wert in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_5_EINH | string | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Sportgasse Normal (E9x) BMW AG Fahrzeug Modi - S-Modus / Komfort (E89) M3 Fahrzeug Modi - Manuell Stufe 5 Einheit in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_6_WERT | unsigned long | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Sportgasse (Sporttaster betätigt) (E9x) BMW AG Fahrzeug Modi - S-Modus / Sport (E89) M3 Fahrzeug Modi - Manuell Stufe 6 Wert in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_6_EINH | string | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Sportgasse (Sporttaster betätigt) (E9x) BMW AG Fahrzeug Modi - S-Modus / Sport (E89) M3 Fahrzeug Modi - Manuell Stufe 6 Einheit in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_7_WERT | unsigned long | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Kurzzeitmanuell Normal (E9x) BMW AG Fahrzeug Modi - Kurzzeitmanuell / Komfort (E89) M3 Fahrzeug Modi - Automatik Stufe 1 Wert in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_7_EINH | string | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Kurzzeitmanuell Normal (E9x) BMW AG Fahrzeug Modi - Kurzzeitmanuell / Komfort (E89) M3 Fahrzeug Modi - Automatik Stufe 1 Einheit in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_8_WERT | unsigned long | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Kurzzeitmanuell (Sporttaster betätigt) (E9x) BMW AG Fahrzeug Modi - Kurzzeitmanuell / Sport (E89) M3 Fahrzeug Modi - Automatik 2 Wert in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_8_EINH | string | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Kurzzeitmanuell (Sporttaster betätigt) (E9x) BMW AG Fahrzeug Modi - Kurzzeitmanuell / Sport (E89) M3 Fahrzeug Modi - Automatik Stufe 2 Einheit in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_9_WERT | unsigned long | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Manuell / Sport Plus (E89) M3 Fahrzeug Modi - Automatik Stufe 3 Wert in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_9_EINH | string | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Manuell / Sport Plus (E89) M3 Fahrzeug Modi - Automatik Stufe 3 Einheit in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_10_WERT | unsigned long | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - D-Modus / Sport Plus (E89) M3 Fahrzeug Modi - Automatik Stufe 4 Wert in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_10_EINH | string | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - D-Modus / Sport Plus (E89) M3 Fahrzeug Modi - Automatik Stufe 4 Einheit in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_11_WERT | unsigned long | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - S-Modus / Sport Plus (E89) M3 Fahrzeug Modi - Automatik Stufe 5 Wert in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_11_EINH | string | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - S-Modus / Sport Plus (E89) M3 Fahrzeug Modi - Automatik Stufe 5 Einheit in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_12_WERT | unsigned long | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Kurzzeitmanuell / Sport Plus (E89) Wert in Sekunden |
| AUFENTHALTSDAUER_FAHRMODUS_12_EINH | string | Aufenthaltsdauer in den einzelnen Fahrmodi: BMW AG Fahrzeug Modi - Kurzzeitmanuell / Sport Plus (E89) Einheit in Sekunden |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-statistikdatensatz-2-lesen"></a>
### STATISTIKDATENSATZ_2_LESEN

Statistikdatensatz 2 lesen ( Service ID 0x21, Identifier 0x02 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| ANZ_ZAEHLER_0_PV6_ADAPTIONEN | int | Zähler für die Anzahl der durchgeführten Adaptionen der Adaptionskennlinie für PV6 (Stützstelle 0) |
| ANZ_ZAEHLER_1_PV6_ADAPTIONEN | int | Zähler für die Anzahl der durchgeführten Adaptionen der Adaptionskennlinie für PV6 (Stützstelle 1) |
| ANZ_ZAEHLER_2_PV6_ADAPTIONEN | int | Zähler für die Anzahl der durchgeführten Adaptionen der Adaptionskennlinie für PV6 (Stützstelle 2) |
| ANZ_ZAEHLER_K1_ADAPTIONEN | unsigned int | Erfolgszähler für durchgeführte Kisspointadationen Kupplung 1 |
| ANZ_ZAEHLER_K2_ADAPTIONEN | unsigned int | Erfolgszähler für durchgeführte Kisspointadationen Kupplung 2 |
| KILOMETERSTAND_LETZTER_K1_ADAPTION_WERT | real | Kilometertstand der letzten erfolgreichen Kisspointadaption Kupplung K1 |
| KILOMETERSTAND_LETZTER_K1_ADAPTION_EINH | string | Kilometertstand der letzten erfolgreichen Kisspointadaption Kupplung K1 Einheit in [km] |
| KILOMETERSTAND_LETZTER_K2_ADAPTION_WERT | real | Kilometertstand der letzten erfolgreichen Kisspointadaption Kupplung K2 |
| KILOMETERSTAND_LETZTER_K2_ADAPTION_EINH | string | Kilometertstand der letzten erfolgreichen Kisspointadaption Kupplung K2 Einheit in [km] |
| KISSPOINT_K1_MIN_WERT | real | Min. adaptierter Kisspoint K1 |
| KISSPOINT_K1_MIN_EINH | string | Min. adaptierter Kisspoint K1 Einheit in [bar] |
| KISSPOINT_K2_MIN_WERT | real | Min. adaptierter Kisspoint K2 |
| KISSPOINT_K2_MIN_EINH | string | Min. adaptierter Kisspoint K2 Einheit in [bar] |
| KILOMETERSTAND_K1_MIN_WERT | real | Kilometerstand der Min. Kisspointadaption Kupplung 1 |
| KILOMETERSTAND_K1_MIN_EINH | string | Kilometerstand der Min. Kisspointadaption Kupplung 1 Einheit in [km] |
| KILOMETERSTAND_K2_MIN_WERT | real | Kilometerstand der Min. Kisspointadaption Kupplung 2 |
| KILOMETERSTAND_K2_MIN_EINH | string | Kilometerstand der Min. Kisspointadaption Kupplung 2 Einheit in [km] |
| KISSPOINT_K1_MAX_WERT | real | Max. adaptierter Kisspoint K1 |
| KISSPOINT_K1_MAX_EINH | string | Max. adaptierter Kisspoint K1 Einheit in [bar] |
| KISSPOINT_K2_MAX_WERT | real | Max. adaptierter Kisspoint K2 |
| KISSPOINT_K2_MAX_EINH | string | Max. adaptierter Kisspoint K2 Einheit in [bar] |
| KILOMETERSTAND_K1_MAX_WERT | real | Kilometerstand der Max. Kisspointadaption Kupplung 1 |
| KILOMETERSTAND_K1_MAX_EINH | string | Kilometerstand der Max. Kisspointadaption Kupplung 1 Einheit in [bar] |
| KILOMETERSTAND_K2_MAX_WERT | real | Kilometerstand der Max. Kisspointadaption Kupplung 2 |
| KILOMETERSTAND_K2_MAX_EINH | string | Kilometerstand der Max. Kisspointadaption Kupplung 2 Einheit in [bar] |
| KUPPLUNGSADAPTIONSKENNLINIE_K1_MAX50_WERT | real | Kupplungsadaptionskennlinie K1 Max 50Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K1_MIN50_WERT | real | Kupplungsadaptionskennlinie K1 Min 50Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K1_MAX300_WERT | real | Kupplungsadaptionskennlinie K1 Max 300Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K1_MIN300_WERT | real | Kupplungsadaptionskennlinie K1 Min 300Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K2_MAX50_WERT | real | Kupplungsadaptionskennlinie K2 Max 50Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K2_MIN50_WERT | real | Kupplungsadaptionskennlinie K2 Min 50Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K2_MAX300_WERT | real | Kupplungsadaptionskennlinie K2 Max 300Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K2_MIN300_WERT | real | Kupplungsadaptionskennlinie K2 Min 300Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K1_300_BEI_MAX50_WERT | real | Kupplungsadaptionskennlinie K1 akt.Wert 300Nm bei Max 50Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K1_300_BEI_MIN50_WERT | real | Kupplungsadaptionskennlinie K1 akt.Wert 300Nm bei Min 50Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K1_50_BEI_MAX300_WERT | real | Kupplungsadaptionskennlinie K1 akt.Wert 50Nm bei Max 300Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K1_50_BEI_MIN300_WERT | real | Kupplungsadaptionskennlinie K1 akt.Wert 50Nm bei Min 300Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K2_300_BEI_MAX50_WERT | real | Kupplungsadaptionskennlinie K2 akt.Wert 300Nm bei Max 50Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K2_300_BEI_MIN50_WERT | real | Kupplungsadaptionskennlinie K2 akt.Wert 300Nm bei Min 50Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K2_50_BEI_MAX300_WERT | real | Kupplungsadaptionskennlinie K2 akt.Wert 50Nm bei Max 300Nm |
| KUPPLUNGSADAPTIONSKENNLINIE_K2_50_BEI_MIN300_WERT | real | Kupplungsadaptionskennlinie K2 akt.Wert 50Nm bei Min 300Nm |
| ANZ_ZAEHLER_K1_ADAPTIONEN_50NM | unsigned int | Kupplung 1 Adaptionszähler 50Nm |
| ANZ_ZAEHLER_K1_ADAPTIONEN_75NM | unsigned int | Kupplung 1 Adaptionszähler 75Nm |
| ANZ_ZAEHLER_K1_ADAPTIONEN_125NM | unsigned int | Kupplung 1 Adaptionszähler 125Nm |
| ANZ_ZAEHLER_K1_ADAPTIONEN_200NM | unsigned int | Kupplung 1 Adaptionszähler 200Nm |
| ANZ_ZAEHLER_K1_ADAPTIONEN_300NM | unsigned int | Kupplung 1 Adaptionszähler 300Nm |
| ANZ_ZAEHLER_K2_ADAPTIONEN_50NM | unsigned int | Kupplung 2 Adaptionszähler 50Nm |
| ANZ_ZAEHLER_K2_ADAPTIONEN_75NM | unsigned int | Kupplung 2 Adaptionszähler 75Nm |
| ANZ_ZAEHLER_K2_ADAPTIONEN_125NM | unsigned int | Kupplung 2 Adaptionszähler 125Nm |
| ANZ_ZAEHLER_K2_ADAPTIONEN_200NM | unsigned int | Kupplung 2 Adaptionszähler 200Nm |
| ANZ_ZAEHLER_K2_ADAPTIONEN_300NM | unsigned int | Kupplung 2 Adaptionszähler 300Nm |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-statistikdaten-loeschen"></a>
### STATISTIKDATEN_LOESCHEN

Verschleissdaten loeschen ( Service ID 0x2E, Identifier 0x1001 )  

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LOESCHEN | string | "ja" -&gt; Verleissdaten sollen geloescht werden |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-istwerte-lesen"></a>
### STATUS_ISTWERTE_LESEN

( Service ID 0x30, Identifier 0x01, 0x01 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_MOTORDREHZAHL_WERT | real | Motordrezahl Bereich von 0 bis 15000 [1/min] |
| STAT_MOTORDREHZAHL_EINH | string | Motordrezahl Einheit [1/min] |
| STAT_EINGANGSDREHZAHL1_WERT | real | Getriebeeingangsdrehzahl 1 Bereich von 0 bis 15000 |
| STAT_EINGANGSDREHZAHL1_EINH | string | Getribeeingangsdrehzahl 1 Bereich [1/min] |
| STAT_EINGANGSDREHZAHL2_WERT | real | Getriebeeingangsdrehzahl 2 Bereich von 0 bis 15000 |
| STAT_EINGANGSDREHZAHL2_EINH | string | Getriebeeingangsdrehzahl 2 Bereich [1/min] |
| STAT_AUSGANGSDREHZAHL_WERT | real | Getriebeausgangsdrehzahl Bereich von -10000 bis 10000 [1/min] |
| STAT_AUSGANGSDREHZAHL_EINH | string | Getriebeausgangsdrehzahl Einheit [1/min] |
| STAT_GESCHWINDIGKEIT_WERT | real | Fahrzeuggeschwindigkeit Bereich von -300 bis 400 [km/h] |
| STAT_GESCHWINDIGKEIT_EINH | string | Fahrzeuggeschwindigkeit Einheit [km/h] |
| STAT_RADGESCHWINDIGKEIT_VL_WERT | real | Radgeschwindigkeit vorne links Bereich von -320 [km/h] bis 320 [km/h] |
| STAT_RADGESCHWINDIGKEIT_VL_EINH | string | Radgeschwindigkeit vorne links Einheit: km/h |
| STAT_RADGESCHWINDIGKEIT_VR_WERT | real | Radgeschwindigkeit vorne rechts Bereich von -320 [km/h] bis 320 [km/h] |
| STAT_RADGESCHWINDIGKEIT_VR_EINH | string | Radgeschwindigkeit vorne rechts Einheit: km/h |
| STAT_RADGESCHWINDIGKEIT_HL_WERT | real | Radgeschwindigkeit hinten links Bereich von -320 [km/h] bis 320 [km/h] |
| STAT_RADGESCHWINDIGKEIT_HL_EINH | string | Radgeschwindigkeit hinten links Einheit: km/h |
| STAT_RADGESCHWINDIGKEIT_HR_WERT | real | Radgeschwindigkeit hinten rechts Bereich von -320 [km/h] bis 320 [km/h] |
| STAT_RADGESCHWINDIGKEIT_HR_EINH | string | Radgeschwindigkeit hinten rechts Einheit: km/h |
| STAT_GESCHWINDIGKEIT_HINTERACHSE_WERT | real | Radgeschwindigkeit Hinterachse Bereich -320 bis 555 [km/h] |
| STAT_GESCHWINDIGKEIT_HINTERACHSE_EINH | string | Radgeschwindigkeit Hinterachse Einheit [km/h] |
| STAT_MOTORTEMPERATUR_WERT | real | Motortemperatur Bereich von -100  bis 300 [°C] |
| STAT_MOTORTEMPERATUR_EINH | string | Motortemperatur Einheit [°C] |
| STAT_MOTOROELTEMPERATUR_WERT | real | Motoröltemperatur Bereich von -100 bis 300 [°C] |
| STAT_MOTOROELTEMPERATUR_EINH | string | Motoröltemperatur Einheit [°C] |
| STAT_KUPPLUNGSOELTEMPERATUR_WERT | real | Ölsumpftemperatur Bereich von -100 bis 300 [°C] |
| STAT_KUPPLUNGSOELTEMPERATUR_EINH | string | Ölsumpftemperatur Einheit [°C] |
| STAT_SG_TEMPERATUR_WERT | real | SG-Temperatur Bereich von -100 bis 300 [°C] |
| STAT_SG_TEMPERATUR_EINH | string | SG-Temperatur Einheit [°C] |
| STAT_UMGEBUNGSTEMPERATUR_WERT | real | Umgebungstemperatur Bereich von -100 bis 300 [°C] |
| STAT_UMGEBUNGSTEMPERATUR_EINH | string | Umgebungstemperatur Einheit [°C] |
| STAT_UBAT_WERT | real | Spannungsversorgung U_Bat (Klemme 30) Bereich von 0 bis 31,9995 [V] |
| STAT_UBAT_EINH | string | Spannungsversorgung U_Bat (Klemme 30) Einheit [V] |
| STAT_SPANNUNGSVERSORGUNG_7V4_WERT | real | Sensorspannungsversorgung 7V4_UH2 Spannungsbereich von 0 bis 31,9995 [V] Arbeitsbereich Min:6,6V  Default:7,4V Max:8,2V Spannungsversorgung für Drehzahlsensoren,Parksperrensensoren, Temperatursensoren und Schaltwippen |
| STAT_SPANNUNGSVERSORGUNG_7V4_EINH | string | Sensorspannungsversorgung 7V4_UH2 Einheit [V] |
| STAT_SENSORSPANNUNGSVERSORGUNG_VCC_WERT | real | Sensorspannungsversorgung 5V VCC Bereich von 0 bis 31,9995 [V] Arbeitsbereich Min:4,75 Default:5V Max: 5,25V Spannungsversorung für Drucksensoren der Kupplung |
| STAT_SENSORSPANNUNGSVERSORGUNG_VCC_EINH | string | Sensorspannungsversorgung 5V VCC Einheit [V] |
| STAT_SENSORSPANNUNGSVERSORGUNG_SV1_WERT | real | Sensorspannungsversorgung SV 1 Bereich von 0 bis 31,9995 [V] Arbeitsbereich Min:4,75 Default:5V Max: 5,25V Spannungsversorgung für Positionssensor der Schaltstange 1/3 und der Schaltstange 5/7 |
| STAT_SENSORSPANNUNGSVERSORGUNG_SV1_EINH | string | Sensorspannungsversorgung SV 1 Einheit [V] |
| STAT_SENSORSPANNUNGSVERSORGUNG_SV2_WERT | real | Sensorspannungsversorgung SV 2 Bereich von 0 bis 31,9995[V] Arbeitsbereich Min:4,75 Default:5V Max: 5,25V Spannungsversorgung für Positionssensor der Schaltstange 6/4 und der Schaltstange 2/R |
| STAT_SENSORSPANNUNGSVERSORGUNG_SV2_EINH | string | Sensorspannungsversorgung SV 2 Einheit [V] |
| STAT_ISTSTROM_MAGNETVENTIL_PV1_WERT | real | Iststrom Magnetventil Kupplung PV 1 Bereich von -3 bis 3 [A] PV1 steuert die Kupplung 1 |
| STAT_ISTSTROM_MAGNETVENTIL_PV1_EINH | string | Iststrom Magnetventil Kupplung PV 1 Einheit [A] |
| STAT_ISTSTROM_MAGNETVENTIL_PV2_WERT | real | Iststrom Magnetventil Kupplung PV 2 Bereich von -3 bis 3 [A] PV2 steuert die Kupplung 2 |
| STAT_ISTSTROM_MAGNETVENTIL_PV2_EINH | string | Iststrom Magnetventil Kupplung PV 2 Einheit [A] |
| STAT_ISTSTROM_MAGNETVENTIL_PV3_WERT | real | Iststrom Magnetventil PV 3 Bereich von -3 bis 3 [A] PV3 steuert die Schaltstangen |
| STAT_ISTSTROM_MAGNETVENTIL_PV3_EINH | string | Iststrom Magnetventil PV 3 Einheit [A] |
| STAT_ISTSTROM_MAGNETVENTIL_PV4_WERT | real | Iststrom Magnetventil PV4 Bereich von -3 bis 3 [A] PV4 steuert die Schaltstangen |
| STAT_ISTSTROM_MAGNETVENTIL_PV4_EINH | string | Iststrom Magnetventil PV 4 Einheit [A] |
| STAT_ISTSTROM_MAGNETVENTIL_PV6_WERT | real | Iststrom Magnetventil PV 6 Bereich von -3 bis 3 [A] PV6 steuert den Systemdruck |
| STAT_ISTSTROM_MAGNETVENTIL_PV6_EINH | string | Iststrom Magnetventil PV 6 Einheit [A] |
| STAT_ISTSTROM_MAGNETVENTIL_PV7_WERT | real | Iststrom Magnetventil PV7 Bereich von -3 bis 3 [A] PV7 steuert den Kühlölstrom für die Kupplungskühlung |
| STAT_ISTSTROM_MAGNETVENTIL_PV7_EINH | string | Iststrom Magnetventil PV 7 Einheit [A] |
| STAT_SOLLSTROM_MAGNETVENTIL_PV1_WERT | real | Sollstrom Magnetventil Kupplung PV 1 Bereich von -3 bis 3 [A] PV1 steuert die Kupplung 1 |
| STAT_SOLLSTROM_MAGNETVENTIL_PV1_EINH | string | Sollstrom Magnetventil Kupplung PV 1 Einheit [A] |
| STAT_SOLLSTROM_MAGNETVENTIL_PV2_WERT | real | Sollstrom Magnetventil Kupplung PV 2 Bereich von -3 bis 3 [A] PV2 steuert die Kupplung 2 |
| STAT_SOLLSTROM_MAGNETVENTIL_PV2_EINH | string | Sollstrom Magnetventil Kupplung PV 2 Einheit [A] |
| STAT_SOLLSTROM_MAGNETVENTIL_PV3_WERT | real | Sollstrom Magnetventil PV 3 Bereich von 0 bis 3000 [mA] PV3 steuert die Schaltstangen |
| STAT_SOLLSTROM_MAGNETVENTIL_PV3_EINH | string | Iststrom Magnetventil PV 3 Einheit [mA] |
| STAT_SOLLSTROM_MAGNETVENTIL_PV4_WERT | real | Sollstrom Magnetventil PV4 Bereich von 0 bis 3000 [mA] PV4 steuert die Schaltstangen |
| STAT_SOLLSTROM_MAGNETVENTIL_PV4_EINH | string | Sollstrom Magnetventil PV 4 Einheit [mA] |
| STAT_SOLLSTROM_MAGNETVENTIL_PV6_WERT | real | Sollstrom Magnetventil PV 6 Bereich von -3 bis 3 [A] PV6 steuert den Systemdruck |
| STAT_SOLLSTROM_MAGNETVENTIL_PV6_EINH | string | Sollstrom Magnetventil PV 6 Einheit [A] |
| STAT_SOLLSTROM_MAGNETVENTIL_PV7_WERT | real | Sollstrom Magnetventil PV7 Bereich von -3 bis 3 [A] PV7 steuert den Kühlölstrom für die Kupplungskühlung |
| STAT_SOLLSTROM_MAGNETVENTIL_PV7_EINH | string | Sollstrom Magnetventil PV 7 Einheit [A] |
| STAT_ISTDRUCK_KUPPLUNG1_WERT | real | Istdruck Kupplung 1 Bereich von -5 bis 50 [bar] |
| STAT_ISTDRUCK_KUPPLUNG1_EINH | string | Istdruck Kupplung 1 Einheit [bar] |
| STAT_ISTDRUCK_KUPPLUNG2_WERT | real | Istdruck Kupplung 2 Bereich von -5 bis 50 [bar] |
| STAT_ISTDRUCK_KUPPLUNG2_EINH | string | Istdruck Kupplung 2 Einheit [bar] |
| STAT_SOLLDRUCK_KUPPLUNG1_WERT | real | Solldruck Kupplung 1 Bereich von -5 bis 50 [bar] |
| STAT_SOLLDRUCK_KUPPLUNG1_EINH | string | Solldruck Kupplung 1 Einheit [bar] |
| STAT_SOLLDRUCK_KUPPLUNG2_WERT | real | Solldruck Kupplung 2 Bereich von -5 bis 50 [bar] |
| STAT_SOLLDRUCK_KUPPLUNG2_EINH | string | Solldruck Kupplung 2 Einheit [bar] |
| STAT_ISTMOMENT_KUPPLUNG1_WERT | real | Istmoment Kupplung 1 Bereich von -4000 bis 4000 [Nm] |
| STAT_ISTMOMENT_KUPPLUNG1_EINH | string | Istmoment Kupplung 1 Einheit [Nm] |
| STAT_ISTMOMENT_KUPPLUNG2_WERT | real | Istmoment Kupplung 2 Bereich von -4000 bis 4000 [Nm] |
| STAT_ISTMOMENT_KUPPLUNG2_EINH | string | Istmoment Kupplung 2 Einheit [Nm] |
| STAT_SOLLMOMENT_KUPPLUNG1_WERT | real | Sollmoment Kupplung 1 Bereich von -4096 bis 4095,875 [Nm] |
| STAT_SOLLMOMENT_KUPPLUNG1_EINH | string | Sollmoment Kupplung 1 Einheit [Nm] |
| STAT_SOLLMOMENT_KUPPLUNG2_WERT | real | Sollmoment Kupplung 2 Bereich von -4096 bis 4095,875 [Nm] |
| STAT_SOLLMOMENT_KUPPLUNG2_EINH | string | Sollmoment Kupplung 2 Einheit [Nm] |
| STAT_ISTPOSITION_SCHALTSTANGE_6_4_WERT | real | Istposition Schaltstange 6/4 Bereich von -12 bis 12 [mm] |
| STAT_ISTPOSITION_SCHALTSTANGE_6_4_EINH | string | Isposition Schaltstange 6/4 Einheit [mm] |
| STAT_ISTPOSITION_SCHALTSTANGE_5_7_WERT | real | Istposition Schaltstange 5/7 Bereich von -12 bis 12 [mm] |
| STAT_ISTPOSITION_SCHALTSTANGE_5_7_EINH | string | Isposition Schaltstange 5/7 Einheit [mm] |
| STAT_ISTPOSITION_SCHALTSTANGE_2_R_WERT | real | Istposition Schaltstange 2/R Bereich von -12 bis 12 [mm] |
| STAT_ISTPOSITION_SCHALTSTANGE_2_R_EINH | string | Isposition Schaltstange 2/R Einheit [mm] |
| STAT_ISTPOSITION_SCHALTSTANGE_1_3_WERT | real | Istposition Schaltstange 1/3 Bereich von -12 bis 12 [mm] |
| STAT_ISTPOSITION_SCHALTSTANGE_1_3_EINH | string | Isposition Schaltstange 1/3 Einheit [mm] |
| STAT_SOLLPOSITION_SCHALTSTANGE_6_4_WERT | char | Sollposition Schaltstange 6/4 table SchaltstangePosition WERT |
| STAT_SOLLPOSITION_SCHALTSTANGE_6_4_TEXT | string | Sollposition schaltstange 6/4 table SchaltstangePosition TEXT |
| STAT_SOLLPOSITION_SCHALTSTANGE_5_7_WERT | char | Sollposition Schaltstange 5/7 table SchaltstangePosition WERT |
| STAT_SOLLPOSITION_SCHALTSTANGE_5_7_TEXT | string | Sollposition schaltstange 5/7 table SchaltstangePosition TEXT |
| STAT_SOLLPOSITION_SCHALTSTANGE_2_R_WERT | char | Sollposition Schaltstange 2/R table SchaltstangePosition WERT |
| STAT_SOLLPOSITION_SCHALTSTANGE_2_R_TEXT | string | Sollposition schaltstange 2/R table SchaltstangePosition TEXT |
| STAT_SOLLPOSITION_SCHALTSTANGE_1_3_WERT | char | Sollposition Schaltstange 1/3 table SchaltstangePosition WERT |
| STAT_SOLLPOSITION_SCHALTSTANGE_1_3_TEXT | string | Sollposition schaltstange 1/3 table SchaltstangePosition TEXT |
| STAT_FAHRPEDAL_WERT | real | Fahrpedalwert Bereich von 0 bis 102 [%] |
| STAT_FAHRPEDAL_EINH | string | Fahrpedalwert Einheit [%] |
| STAT_MOTORISTMOMENT_WERT | real | Motor-Istmoment Bereich von -4000 bis 4000 [Nm] |
| STAT_MOTORISTMOMENT_EINH | string | Motor-Istmoment Einheit [Nm] |
| STAT_AQUER_CAN_WERT | real | Querbeschleunigung von CAN Bereich von -51,2 bis 51,2 [m_s^2] |
| STAT_AQUER_CAN_EINH | string | Querbeschleunigung Einheit [m_s^2] |
| STAT_KILOMETERSTAND_WERT | real | Kilometerstand von CAN Bereich von 0 bis 524280 [km] |
| STAT_KILOMETERSTAND_EINH | string | Kilometerstand Eimheit [km] |
| STAT_HYDRAULIKDRUCK_WERT | real | Systemdruck Bereich von -5 bis 50 [bar] |
| STAT_HYDRAULIKDRUCK_EINH | string | Systemdruck Einheit [bar] |
| STAT_PARKSPERRE_AKTIV | char | Signal Parksperre an CAS Signal STAT_PARKSPERRE_SENSOR1_EIN und STAT_PARKSPERRE_SENSOR2_EIN werden geundet. Parksperre 0= nicht aktiv, 1= aktiv |
| STAT_PARKSPERRE_SENSOR1_EIN | char | Parksperrensenor  1 0= nicht aktiv, 1= aktiv |
| STAT_PARKSPERRE_SENSOR2_EIN | char | Parksperrensenor  2 / redundant 0= nicht aktiv, 1= aktiv |
| STAT_KL15_EIN | char | True (1) = Wake Up ist aktiv False (0) = Wake Up ist inaktiv |
| STAT_TASTER_LENKRAD_SCHALTWIPPE_WERT | char | (0) = keine änderung (1) = Tip+ (2) = Tip- |
| STAT_TASTER_LENKRAD_SCHALTWIPPE_TEXT | string | (0) = keine änderung (1) = Tip+ (2) = Tip- |
| STAT_KUPPLUNG1_WERT | char | Kupplungsstatus Kupplung 1 table KupplungsStati WERT |
| STAT_KUPPLUNG1_TEXT | string | Kupplungstatus Kupplung 1 table KupplungsStati TEXT |
| STAT_KUPPLUNG2_WERT | char | Kupplungsstatus Kupplung 2 table KupplungsStati WERT |
| STAT_KUPPLUNG2_TEXT | string | Kupplungstatus Kupplung 2 table KupplungsStati TEXT |
| STAT_ISTGANG_WERT | char | Istgang table GangStatus WERT |
| STAT_ISTGANG_TEXT | string | Istgang Text table GangStatus TEXT |
| STAT_SCHALTSTANGE_6_4_WERT | char | Getriebestatus SST6_4 table GetriebeStatus WERT |
| STAT_SCHALTSTANGE_6_4_TEXT | string | Getriebestatus SST6_4 Text table GetriebeStatus TEXT |
| STAT_SCHALTSTANGE_5_7_WERT | char | Getriebestatus SST5_7 table GetriebeStatus WERT |
| STAT_SCHALTSTANGE_5_7_TEXT | string | Getriebestatus SST5_7 Text table GetriebeStatus TEXT |
| STAT_SCHALTSTANGE_2_R_WERT | char | Getriebestatus SST2_R table GetriebeStatus WERT |
| STAT_SCHALTSTANGE_2_R_TEXT | string | Getriebestatus SST2_R Text table GetriebeStatus TEXT |
| STAT_SCHALTSTANGE_1_3_WERT | char | Getriebestatus SST1_3 table GetriebeStatus WERT |
| STAT_SCHALTSTANGE_1_3_TEXT | string | Getriebestatus SST1_3 Text table GetriebeStatus TEXT |
| STAT_GETRIEBEPOSITION_WERT | char | Getriebeposition Wert |
| STAT_GETRIEBEPOSITION_TEXT | string | Getriebeposition Text ( D,N,R,P,M ) |
| STAT_OBD_STEUERFUNKTION_WERT | char | OBD Steuerfunktionen table OBD-Steuerfunktion WERT |
| STAT_OBD_STEUERFUNKTION_TEXT | string | OBD-Steuerfunktion Text table OBD-Steuerfunktion TEXT |
| STAT_SPORT_TASTER_EIN | char | True (1) = Sporttaster aktiv False (0) = Sportschalter inaktiv |
| STAT_PROGRAMMINFO_WERT | char | 1 - 6 = Drive Logic Mode 1-6 7 - 12 = Rennstart Mode 1-6 |
| STAT_PROGRAMMINFO_TEXT | string | 1 - 6 = Drive Logic Mode 1-6 7 - 12 = Rennstart Mode 1-6 |
| STAT_GANGANZEIGE_WERT | char | 0=Dunkel, 5=1.Gang, 6=2.Gang, 7=3.Gang usw. 15=Signal ungültig |
| STAT_GANGANZEIGE_TEXT | string | 0=Dunkel, 5=1.Gang, 6=2.Gang, 7=3.Gang usw. 15=Signal ungültig |
| STAT_WAEHLHEBELANZEIGE_WERT | char | 0=Anzeige dunkel, 1=P, 2=R, 3=P_30sec, 4=N, 6=N_30,5min, 7=N_5min, 8=D, 15=ungültiges Signal |
| STAT_WAEHLHEBELANZEIGE_TEXT | string | 0=Anzeige dunkel, 1=P, 2=R, 3=P_30sec, 4=N, 6=N_30,5min, 7=N_5min, 8=D, 15=ungültiges Signal |
| STAT_MIL_WERT | char | 0= Keine Anforderung 1= Anforderung MIL aus 2= Anforderung MIL ein 3= Signal ungültig |
| STAT_MIL_TEXT | string | 0= Lokaler Trip, 1= Freeze Frame,2= MIL EIN_AUS 3= MIL blink |
| STAT_KL15_CAN_EIN | char | True (1) = Klemme 15 ein False (0) = Klemme 15 aus KL15 CAN |
| STAT_BREMSLICHTSCHALTER_EIN | char | True (1) = Bremse aktiv False (0) = Bremse inaktiv |
| STAT_ENDSTUFE_FEHLER | char | True(1)= Kein Fehler False(0)= Fehler liegt vor |
| STAT_ISTGANG_TEILGETRIEBE1_WERT | char | Istgang für Teilgetriebe 1 Wert table GANGSTATUS WERT |
| STAT_ISTGANG_TEILGETRIEBE1_TEXT | string | Istgang für Teilgetriebe 1 Text table GANGSTATUS TEXT |
| STAT_ISTGANG_TEILGETRIEBE2_WERT | char | Istgang für Teilgetriebe 2 Wert table IGANGSTATUS WERT |
| STAT_ISTGANG_TEILGETRIEBE2_TEXT | string | Istgang für Teilgetriebe 1 Text table GANGSTATUS TEXT |
| STAT_FESTSTELLBREMSE_EIN | char | True (1) = Bremse betätigt False (0) = Bremse nicht betätigt |
| STAT_SCHALTDIAGRAMM_AGS_WERT | int | Schaltdiagramm AGS |
| STAT_SCHALTDIAGRAMM_AGS_TEXT | string | Schaltdiagramm AGS |
| STAT_ANTRIEBSDREHZAHLSENSOR_WERT | unsigned int | Antriebsdrehzahlsensor Wert |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-rohwerte-lesen"></a>
### STATUS_ROHWERTE_LESEN

( Service ID 0x30, Identifier 0x02, 0x01 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_SG_TEMPERATUR_WERT | real | SG-Temperatur Bereich von -32768 bis 32767 [°C] |
| STAT_SG_TEMPERATUR_EINH | string | SG-Temperatur Einheit [°C] |
| STAT_VERSORGUNGSSPANNUNGSSENSOR_WERT | real | Versorgungsspannungssensor Bereich von 0 bis 32 [V] |
| STAT_SENSORSPANNUNGSVERSORGUNG_VCC_WERT | real | Sensorspannungsversorgung 5V VCC Bereich von 0 bis 32 |
| STAT_SENSORSPANNUNGSVERSORGUNG_SV1_WERT | real | Sensorspannungsversorgung SV 1 Bereich von 0 bis 32 |
| STAT_SENSORSPANNUNGSVERSORGUNG_SV2_WERT | real | Sensorspannungsversorgung SV 2 Bereich von 0 bis 32 |
| STAT_SPANNUNGSVERSORGUNG_7SV4_WERT | real | Sensorspannungsversorgung 7V SV4 Spannungsbereich von 0 bis 32 |
| STAT_ANTRIEBSDREHZAHLSENSOR_WERT | real | Antriebsdrehzahlsensor Min: 0 Max: 16383,75 |
| STAT_EINGANGSDREHZAHLSENSOR_1_WERT | real | Getriebeeingangsdrehzahlsensor 1 Min: 0 Max: 16383,75 |
| STAT_EINGANGSDREHZAHLSENSOR_2_WERT | real | Getriebeeingangsdrehzahlsensor 2 Min: 0 Max: 16383,75 |
| STAT_ABSPRITZTEMPERATURSENSOR_WERT | real | Abspritztemperatursensor Min: 0 Max: 211,4 |
| STAT_TEMPERATURSENSOR_1_WERT | real | Temperatursensor 1 Min: -32768 Max: 32767 |
| STAT_TEMPERATURSENSOR_1_EINH | real | Temperatursensor Einheit °C |
| STAT_TEMPERATURSENSOR_2_WERT | real | Temperatursensor 2 Min: -32768 Max: 32767 |
| STAT_TEMPERATURSENSOR_2_EINH | string | Temperatursensor Einheit °C |
| STAT_DRUCKSENSOR_KUPPL_1_WERT | real | Drucksensor Kupplung 1 Min: -327,68 Max: -327,67 |
| STAT_DRUCKSENSOR_KUPPL_1_EINH | string | Drucksensor Kupplung 1 Einheit bar |
| STAT_DRUCKSENSOR_KUPPL_2_WERT | real | Drucksensor Kupplung 2 Min: -327,68 Max: -327,67 |
| STAT_DRUCKSENSOR_KUPPL_2_EINH | string | Drucksensor Kupplung 2 Einheit [bar] |
| STAT_WEGSENSOR_SST_R_2_WERT | real | Wegsensor Schaltstange R/2 Min: 0 Max: 320 |
| STAT_WEGSENSOR_SST_R_2_EINH | string | Wegsensor Schaltstange R/2 Einheit [V] |
| STAT_WEGSENSOR_SST_1_3_WERT | real | Wegsensor Schaltstange 1/3 Min: 0 Max: 320 |
| STAT_WEGSENSOR_SST_1_3_EINH | string | Wegsensor Schaltstange 1/3 Einheit [V] |
| STAT_WEGSENSOR_SST_6_4_WERT | real | Wegsensor Schaltstange 6/4 Min: 0 Max: 320 |
| STAT_WEGSENSOR_SST_6_4_EINH | string | Wegsensor Schaltstange 6/4 Einheit [V] |
| STAT_WEGSENSOR_SST_5_7_WERT | real | Wegsensor Schaltstange 5/7 Min: 0 Max: 320 |
| STAT_WEGSENSOR_SST_5_7_EINH | string | Wegsensor Schaltstange 5/7 Einheit [V] |
| STAT_PARKSPERRENSENSOR_1_WERT | unsigned char | Parksperrensensor 1 Min: 0 Max: 255 |
| STAT_PARKSPERRENSENSOR_2_WERT | unsigned char | Parksperrensensor 1 Min: 0 Max: 255 |
| STAT_SENSORSPANNUNG_PADDEL_WERT | real | Sensorspannung Lenkradpaddel Min: 0 Max: 528 |
| STAT_SENSORSPANNUNG_PADDEL_EINH | string | Sensorspannung Lenkradpaddel Einheit [V] |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-stellglied"></a>
### STEUERN_STELLGLIED

( Service ID 0x30, Identifier 0x07 ) Eine Stellgliedeingabe mit Stellgliedwert werden über IO-Hex Eingabewert eingegeben  Es ist nur möglich Ausgänge anzusteuern, wenn kein Test- und Einlernprogramm aktiv ist. ACHTUNG: Bei der Ansteuerung Magnetventile (PV1-4, PV6, PV7 und SV1-4) wird das SG in einen sogenannten Prüfstandmode versetzt, bei dem dann unabhängig von der Ausgangssituation alle Magnetventile, bis auf den der angesteuert werden soll, auf den Sollwert 0 eingestellt.  WARNUNG: Der Bediener des Diagnosetesters ist für die Sicherheit von Leib und Leben sowie für den Schutz aller Bauteile, die im Zusammenhang mit der SG-Ausgangsansteuerung stehen, verantwortlich. Es ist nicht auszuschließen, dass sich das Fahrzeug durch eine unsachgemäße Ansteuerung fortbewegt. Nach Möglichkeit sollte sich das Fahrzeug während der Ausgangsansteuerung auf einer Hebebühne befinden, so dass es sich nicht fortbewegen kann.  STELLGLIED_IO_HEX                          STELLGLIED_WERT 0x20 = Sollstrom Magnetventil PV1 -     Min: 0 Max: 1900 0x21 = Sollstrom Magnetventil PV2 -     Min: 0 Max: 1900 0x22 = Sollstrom Magnetventil PV3 -     Min: 0 Max: 1900 0x23 = Sollstrom Magnetventil PV4 -     Min: 0 Max: 1900 0x24 = Sollstrom Magnetventil PV6 -     Min: 0 Max: 1900 0x25 = Sollstrom Magnetventil PV7 -     Min: 0 Max: 1900 0x26 = Sollzustand Magnetventil SV1 -   Min: 0 Max: 1 0x27 = Sollzustand Magnetventil SV2 -   Min: 0 Max: 1 0x28 = Sollzustand Magnetventil SV3 -   Min: 0 Max: 1 0x29 = Sollzustand Magnetventil SV4 -   Min: 0 Max: 1 0x2A = Parksperre verriegeln - 0= keine Reaktion  1= PS verriegeln  2= PS entriegeln 0x2B = Anzeige Programminformation (Statusausgang CAN ) -    Min: 1 Max: 6 0x2C = Getriebe nach Neutral stellen -  Ein: 1 0x2D = Parksperre Hakentest -           Ein: 1 Aus: 0 0x2E = Parksperre Magnettest -          Ein: 1 0x2F = Ansteuerung Parksperre aus/ein - 0= Parksperre ausgelegt - 1= Parksperre eingelegt 0x30 = Anzeige Wahlhebelschema -        Min: 1 Max: 4 0x31 = Anzeige Gänge -                  Min: 1 Max: 7 0x32 = Anzeige CC Meldung -             An: 1  Aus: 0 weiter Information im LH - Diagnoseschnittstelle

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STELLGLIED_IO_HEX | string | Siehe Stellglied IO Hex  in der Job Übersicht |
| STELLGLIED_WERT | string | table IO_SETZEN Wertebereich, siehe Job Übersicht |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei  |
| STAT_STELLGLIED_TEXT | string | Textausgabe des Stellgliedes |
| STAT_ANSTEUERUNG_WERT | int | 0: Kein Fehler 1: Ansteuerwert nicht definiert 2: Ansteuerbedingung nicht erfüllt 3: Ansteuerwert nicht im vorgegebenen Bereich |
| STAT_ANSTEUERUNG_TEXT | string | Table IO_STATUS |
| STAT_MESSWERT_ROH | int | Messwert als Rohwert Byte 4 und 5 des Antworttelegramms |
| STAT_MESS_WERT | real | Messwert mit Quantisierung Magnetventile,Kupplung,Schaltstange Druckventil, Hydralik, Geschwindigkeit |
| STAT_MESS_EINH | string | Einheit, falls vorhanden für Messwert |
| STAT_MESS_TEXT | string | Rückgabe Stati für Parksperre Ansteuerung |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-stellglied-zuruecksetzen"></a>
### STEUERN_STELLGLIED_ZURUECKSETZEN

( Service ID 0x30, Identifier 0x00 ) STELLGLIED_IO_HEX 0x20 = Sollstrom Magnetventil PV1 0x21 = Sollstrom Magnetventil PV2 0x22 = Sollstrom Magnetventil PV3 0x23 = Sollstrom Magnetventil PV4 0x24 = Sollstrom Magnetventil PV5 0x25 = Sollstrom Magnetventil PV6 0x26 = Sollzustand Magnetventil SV1 0x27 = Sollzustand Magnetventil SV2 0x28 = Sollzustand Magnetventil SV3 0x29 = Sollzustand Magnetventil SV4 0x2A = Parksperre verriegeln 0x2B = Anzeige Programminformation 0x2C = Getriebe nach Neutral 0x2D = Parksperre Hakentest 0x2E = Ansteuerung Parksperre 0x30 = Anzeige Wahlhebelschema 0x31 = Anzeige Gaenge 0x32 = Anzeige CC Meldung 0xFE = Alle Ausgangsgrößen weiter Information im LH - Diagnoseschnittstelle

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STELLGLIED_IO_HEX | string | Siehe Stellglied IO Hex  in der Job Uebersicht |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-testprg-starten"></a>
### STEUERN_TESTPRG_STARTEN

Test- und Einlernprogramm starten ( Service ID 0x31, Identifier 0x20-0x27 + 0x30-0x35) WARNUNG: Weil die Diagnoseschnittstelle ein Event gesteuertes Modul in der Getriebesoftware darstellt, können Test- und Einlernprogramme nur durch den Bediener, in diesem Fall durch den Diagnosetester, ein- und ausgeschaltet bzw. abgefragt werden. Anderenfalls sind Zustände möglich, die nur durch das Abschalten der Kl.15 und das anschließende Abwarten des Steuergerätenachlaufs verlassen werden können.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTPRG_NR | int | table TestundEinlernPrgTabelle TESTEINLERNNR TESTEINLERNTEXTE 0x20 = Beliebigen Gang einlegen 0x21 = Spülfunktion starten 0x22 = Solldruckvorgabe Kupplung 1 0x23 = Solldruckvorgabe Kupplung 2 0x24 = Vorgabe des Systemdrucks 0x25 = Kupplungskuehlung aktivieren 0x26 = Diagnose Parksperrenmagnet 0x27 = Diagnose PV7 0x30 = Kupplungsschleifpunkt 1 und 2 einlernen (Kisspoint 1+2) 0x31 = Anti Leerlaufklackern aktivieren 0x32 = Getriebe einlernen 0x33 = Adaptionswerte in NVRAM speichern 0x34 = Ventilkennlinien einlernen PV1 und PV2 0x35 = Fehlerspeicher formatieren |
| STARTWERT | int | Beliebigen Gang einlegen - Eingabebereich = 0 bis 7 oder 14 für Rückwärts Gang Solldruckvorgabe Kupplung 1 - Eingabebereich = 0 - 15000 (mbar) Solldruckvorgabe Kupplung 2 - Eingabebereich = 0 - 15000 (mbar) Vorgabe des Systemdrucks  - Eingabebereich = 0 - 20000 (mbar) Kupplungskuehlung aktivieren - 0x00 = Geschlossen Kupplungskuehlung aktivieren - 0x01 = min. Kupplungskuehlung Kupplungskuehlung aktivieren - 0x02 = max. Kupplungskuehlung Kupplungsschleifunkt einlernen - 0x00 = Einlernen am EOL Kupplungsschleifunkt einlernen - 0x01 = Einlernen in der Werkstatt Adaptionswerte in NVRAM speichern - 0x00 = Block A - 0x01 = Block B Adaptionswerte in NVRAM speichern - 0x02 = Block C - 0x03 = Block D |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_TESTPRG_IM_TEST_DEZIMAL | int | Rückgabe welches Programm gestartet wurde |
| STAT_TESTPRG_IM_TEST_TEXT | string | table TestundEinlernPrgTabelle TESTEINLERNNR TESTEINLERNNAME Rückgabe der Test- und Einlerntexte |
| STAT_STATUS_TESTPRG_DEZIMAL | int | Während und nach dem Betrieb liefert das Steuergerät einen Status Wert zurück table  StatusTestEinlern |
| STAT_STATUS_TESTPRG_TEXT | string | Während und nach dem Betrieb liefert das Steuergerät einen Status Text zurück table  StatusTestEinlern |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-testprg-istzustand"></a>
### STATUS_TESTPRG_ISTZUSTAND

Test- und Einlernprogramm abfragen ( Service ID 0x33, Identifier 0x20-0x27 + 0x30-0x35) WARNUNG: Das Einschalten,Ausschalten und Abfragen von Test- und Einlernprogramm darf NUR über eines Diagnosetester erfolgen!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTPRG_NR | int | table TestundEinlernPrgTabelle TESTEINLERNNR TESTEINLERNTEXTE 0x20 = Beliebigen Gang einlegen 0x21 = Spülfunktion starten 0x22 = Solldruckvorgabe Kupplung 1 0x23 = Solldruckvorgabe Kupplung 2 0x24 = Vorgabe des Systemdrucks 0x25 = Kupplungskuehlung aktivieren 0x26 = Diagnose Parksperrenmagnet 0x27 = Diagnose PV7 0x30 = Kupplungsschleifpunkt 1 und 2 einlernen (Kisspoint 1 + 2) 0x31 = Anti Leerlaufklackern aktivieren 0x32 = Getriebe einlernen 0x33 = Adaptionswerte in NVRAM speichern 0x34 = Ventilkennlinien einlernen PV1 und PV2 0x35 = Fehlerspeicher formatieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_TESTPRG_IM_TEST_DEZIMAL | int | Rückgabe welches Programm gestartet wurde |
| STAT_TESTPRG_IM_TEST_TEXT | string | table TestundEinlernPrgTabelle TESTEINLERNNR TESTEINLERNNAME Rückgabe der Test- und Einlerntexte |
| STAT_STATUS_TESTPRG_DEZIMAL | int | Während und nach dem Betrieb liefert das Steuergerät einen Status Wert zurück table  StatusTestEinlern |
| STAT_STATUS_TESTPRG_TEXT | string | Während und nach dem Betrieb liefert das Steuergerät einen Status Text zurück table  StatusTestEinlern |
| STAT_ZUSTAND_TESTPRG_DEZIMAL | int | Rückgabe des Zustands Wert  des Test- und Einlernprogramm table InfoTextZustand ZUSTANDSNR ZUSTANDSTEXT |
| STAT_ZUSTAND_TESTPRG_TEXT | string | Rückgabe des Zustands Text  des Test- und Einlernprogramm table InfoTextZustand ZUSTANDSNR ZUSTANDSTEXT |
| STAT_FEHLERMELDUNG_DEZIMAL | int | Rückgabe des Fehlermeldungswert table InfoTextFehler FEHLERNR FEHLERTEXT |
| STAT_FEHLERMELDUNG_TEXT | string | Rückgabe des Fehlermeldungswert table InfoTextFehler FEHLERNR FEHLERTEXT |
| STAT_MESS_WERT | real | Rückgabe des Messwerts aus Test- und Einlernprogramm abfrage Nur für Speichervorspanndruck ermitteln |
| STAT_MESS_EINH | string | Messwert Einheit bar |
| STAT_MESS_1_WERT | real | Rückgabe des Messwerts aus Test- und Einlernprogramm abfrage Nur für Kupplungsschleifpunkt 2, sonst wird der Wert -1 zurückgegeben Adaptionswert für Kupplungsschleifpunkt |
| STAT_MESS_1_EINH | string | Messwert Einheit bar |
| STAT_MESS_2_WERT | real | Rückgabe des Messwerts aus Test- und Einlernprogramm abfrage Nur für Kupplungsschleifpunkt,sonst wird der Wert -1 zurückgegeben Kilometerstand der letzten gültigen Adaption ( Schleifpunkt 1 + 2 ) |
| STAT_MESS_2_EINH | string | Messwert Einheit km |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-testprg-stop"></a>
### STEUERN_TESTPRG_STOP

Test- und Einlernprogramm beenden ( Service ID 0x32, Identifier 0x20 - 0x27, 0x30 - 0x35 ) WARNUNG: Das Einschalten,Ausschalten und Abfragen von Test- und Einlernprogramm darf NUR über eines Diagnosetester erfolgen!

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TESTPRG_NR | int | table TestundEinlernPrgTabelle TESTEINLERNNR TESTEINLERNTEXTE 0x20 = Beliebigen Gang einlegen 0x21 = Spülfunktion starten 0x22 = Solldruckvorgabe Kupplung 1 0x23 = Solldruckvorgabe Kupplung 2 0x24 = Vorgabe des Systemdrucks 0x25 = Kupplungskuehlung aktivieren 0x26 = Diagnose Parksperrenmagnet 0x27 = Diagnose PV7 0x30 = Kupplungsschleifpunkt 1 und 2 einlernen (Kisspoint 1 + 2) 0x31 = Anti Leerlaufklackern aktivieren 0x32 = Getriebe einlernen 0x33 = Adaptionswerte in NVRAM speichern 0x34 = Ventilkennlinien einlernen PV1 und PV2 0x35 = Fehlerspeicher formatieren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei table JobResult |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-rbm-ratio-lesen"></a>
### STATUS_RBM_RATIO_LESEN

Dient zum Aulesen der OBD fehlerbezogenen RBM Ratios Dabei wird die Häufigkeit des Durchlaufens von abgasrelevanten Diagnosefunktionen gezählt ( Service ID 0x22, Identifier 0x52, 0x00 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,FEHLER |
| STAT_IGNITION_CYCLE_COUNTER_WERT | unsigned int | Werte bis 65534 |
| STAT_GENERAL_DENOMINATOR_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_1_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_1_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_2_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_2_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_3_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_3_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_4_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_4_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_5_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_5_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_6_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_6_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_7_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_7_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_8_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_8_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_9_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_9_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_10_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_10_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_11_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_11_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_12_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_12_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_13_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_13_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_14_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_14_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_15_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_15_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_16_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_16_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_17_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_17_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_18_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_18_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_19_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_19_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_20_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_20_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_21_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_21_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_22_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_22_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_23_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_23_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_24_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_24_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_25_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_25_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_26_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_26_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_27_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_27_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_28_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_28_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_29_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_29_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_30_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_30_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_31_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_31_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_32_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_32_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_33_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_33_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_34_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_34_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_35_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_35_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_36_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_36_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_37_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_37_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_38_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_38_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_39_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_39_WERT | unsigned int | Werte bis 65534 |
| STAT_NUMERATOR_DIAGNOSE_40_WERT | unsigned int | Werte bis 65534 |
| STAT_DENOMINATOR_DIAGNOSE_40_WERT | unsigned int | Werte bis 65534 |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort vom Steuergerät |

<a id="job-pruefcode-lesen"></a>
### PRUEFCODE_LESEN

Standard Pruefcode lesen fuer Kundendienst KWP2000: $1A ReadECUIdentification KWP2000: $18 ReadDiagnosticTroubleCodesByStatus KWP2000: $17 ReadStatusOfDiagnosticTroubleCodes ---------------- Zusätzlich für VS: --------------------- KWP2000: $30 A8 STATUS_GETRIEBE_TEACHEN KWP2000: $30 A4 STATUS_VENTILKENNLINIE_PV1 KWP2000: $30 A5 STATUS_VENTILKENNLINIE_PV2 KWP2000: $30 A6 STATUS_VENTILKENNLINIE_PV6 KWP2000: $30 A0 STATUS_ADAPTION_KUPPLUNGSSCHLEIFPUNKT_K1 KWP2000: $30 A1 STATUS_ADAPTION_KUPPLUNGSSCHLEIFPUNKT_K2 KWP2000: $30 A2 STATUS_ADAPTION_MOMENTENKENNLINIE_K1 KWP2000: $30 A3 STATUS_ADAPTION_MOMENTENKENNLINIE_K2 KWP2000: $30 A7 STATUS_SPERRSTELLUNG_PV7 KWP2000: $30 AA STATUS_ADAPTIONSWERT_PV6 KWP2000: $21 01 STATISTIKDATENSATZ_1_LESEN KWP2000: $21 02 STATISTIKDATENSATZ_2_LESEN Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PRUEFCODE | binary | Pruefcode Daten |

<a id="job-debugging-information"></a>
### DEBUGGING_INFORMATION

Einlernwert Sperrstellung PV7 ( Service ID 0x21, Identifier 0xFD ) Debugging Information

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| DATEN_HEX | binary | Hex Dump für Debugging Information |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-getriebe-teachen"></a>
### STATUS_GETRIEBE_TEACHEN

Einlernwerte Getriebe Teachen ( Service ID 0x30, Identifier 0xA8 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_FAKTOR_AMPLITUDE_TIN_AMP_0_WERT | real | Faktor der Amplitude tin_amp_[0] Min: 0 Default: tbd  Max: 8 |
| STAT_FAKTOR_AMPLITUDE_TIN_AMP_1_WERT | real | Faktor der Amplitude tin_amp_[1] Min: 0 Default: tbd  Max: 8 |
| STAT_FAKTOR_AMPLITUDE_TIN_AMP_2_WERT | real | Faktor der Amplitude tin_amp_[2] Min: 0 Default: tbd  Max: 8 |
| STAT_FAKTOR_AMPLITUDE_TIN_AMP_3_WERT | real | Faktor der Amplitude tin_amp_[3] Min: 0 Default: tbd  Max: 8 |
| STAT_VERSCHIEBUNG_KENNLINIE_TIN_P0_WERT | real | Verschiebung der Kennlinie tin_p[0] Min: -4 Default: tbd  Max: 4 |
| STAT_VERSCHIEBUNG_KENNLINIE_TIN_P1_WERT | real | Verschiebung der Kennlinie tin_p[1] Min: -4 Default: tbd  Max: 4 |
| STAT_VERSCHIEBUNG_KENNLINIE_TIN_P2_WERT | real | Verschiebung der Kennlinie tin_p[2] Min: -4 Default: tbd  Max: 4 |
| STAT_VERSCHIEBUNG_KENNLINIE_TIN_P3_WERT | real | Verschiebung der Kennlinie tin_p[3] Min: -4 Default: tbd  Max: 4 |
| STAT_VERSCHIEBUNG_KENNLINIE_TIN_EINH | string | Verschiebung Kennlinie tin_p Einheit |
| STAT_NACHADAPTION_GANG_1_WERT | real | Nachadaptionswert 1. Gang |
| STAT_NACHADAPTION_GANG_2_WERT | real | Nachadaptionswert 2. Gang |
| STAT_NACHADAPTION_GANG_3_WERT | real | Nachadaptionswert 3. Gang |
| STAT_NACHADAPTION_GANG_4_WERT | real | Nachadaptionswert 4. Gang |
| STAT_NACHADAPTION_GANG_5_WERT | real | Nachadaptionswert 5. Gang |
| STAT_NACHADAPTION_GANG_6_WERT | real | Nachadaptionswert 6. Gang |
| STAT_NACHADAPTION_GANG_7_WERT | real | Nachadaptionswert 7. Gang |
| STAT_NACHADAPTION_GANG_R_WERT | real | Nachadaptionswert R-Gang |
| STAT_NACHADAPTION_GANG_EINH | string | Nachadaption Gang Einheit |
| STAT_NACHADAPTION_NEUTRAL_SST_1_3_WERT | real | Nachadaptionswert Neutral SST 1/3 |
| STAT_NACHADAPTION_NEUTRAL_SST_2_R_WERT | real | Nachadaptionswert Neutral SST 2/R |
| STAT_NACHADAPTION_NEUTRAL_SST_5_7_WERT | real | Nachadaptionswert Neutral SST 5/7 |
| STAT_NACHADAPTION_NEUTRAL_SST_6_4_WERT | real | Nachadaptionswert Neutral SST 6/4 |
| STAT_NACHADAPTION_NEUTRAL_EINH | string | Nachadaption Neutral Einheit |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaption-kupplungsschleifpunkt-k1"></a>
### STATUS_ADAPTION_KUPPLUNGSSCHLEIFPUNKT_K1

Adaptionswerte Kupplungsschleifpunkt K1 ( Service ID 0x30, Identifier 0xA0 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_K1_SCHLEIFPUNKT_FAKTOR_1_WERT | real | Kupplungsschleifpunkt der im EOL ermittelt wurde Min: -327 Max: 327 |
| STAT_K1_SCHLEIFPUNKT_FAKTOR_2_WERT | real | Schleifpunkt, der in der Werkstatt ermittelt wurde (beim Nachlernen z.B. nach Kupplungstausch) Min: -327 Default:1,8 Max: 327 |
| STAT_K1_SCHLEIFPUNKT_FAKTOR_3_WERT | real | Schleifpunkt nach 10 Adaptionsschritten Kisspoint K1 3.Wert Min: -327 Default:1,8 Max: 327 |
| STAT_K1_SCHLEIFPUNKT_FAKTOR_4_WERT | real | Für die Funktion relevante Kupplungsschleifpunkt (aktuell gefahrener Schleifpunkt) Min: -327 Default:1,8 Max: 327 |
| STAT_K1_SCHLEIFPUNKT_FAKTOR_5_WERT | real | Kleinster durch Adaption ermittelter Schleifpunkt Min: -327 Default:1,8 Max: 327 |
| STAT_K1_SCHLEIFPUNKT_FAKTOR_6_WERT | real | Größter durch Adaption ermittelter Schleifpunkt Min: -327 Default:1,8 Max: 327 |
| STAT_K1_SCHLEIFPUNKT_EINH | string | Adaptionswerte Kupplung Kisspoint K1 Einheit [bar] |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaption-kupplungsschleifpunkt-k2"></a>
### STATUS_ADAPTION_KUPPLUNGSSCHLEIFPUNKT_K2

Adaptionswerte Kupplungsschleifpunkt K2 ( Service ID 0x30, Identifier 0xA1 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_K2_SCHLEIFPUNKT_FAKTOR_1_WERT | real | Kupplungsschleifpunkt,der am EOL ermittelt wurde Min: -327 Max: 327 |
| STAT_K2_SCHLEIFPUNKT_FAKTOR_2_WERT | real | Kupplungsschleifpunkt, der in der Werkstatt ermittelt wurde (beim Nachlernen z.B. nach Kupplungstausch) Min: -327 Default: 1,85 Max: 327 |
| STAT_K2_SCHLEIFPUNKT_FAKTOR_3_WERT | real | Kupplungsschleifpunkt nach 10 Adaptionsschritten Min: -327 Default: 1,85 Max: 327 |
| STAT_K2_SCHLEIFPUNKT_FAKTOR_4_WERT | real | Für die Funktion relevante Kupplungsschleifpunkt (aktuell gefahrener Kupplungsschleifpunkt) Min: -327 Default: 1,85 Max: 327 |
| STAT_K2_SCHLEIFPUNKT_FAKTOR_5_WERT | real | Kleinster durch Adaption ermittelter Kupplungsschleifpunkt Min: -327 Default: 1,85 Max: 327 |
| STAT_K2_SCHLEIFPUNKT_FAKTOR_6_WERT | real | Größter durch Adaption ermittelter Kupplungsschleifpunkt Min: -327 Default: 1,85 Max: 327 |
| STAT_K2_SCHLEIFPUNKT_EINH | string | Adaptionswerte Kupplung Kisspoint K2 Einheit [bar] |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaption-momentenkennlinie-k1"></a>
### STATUS_ADAPTION_MOMENTENKENNLINIE_K1

Adaptionswerte Kupplungsmomentenkennlinie K1 ( Service ID 0x30, Identifier 0xA2 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_1_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K1 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_2_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K2 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_3_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K3 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_4_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K4 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_5_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K5 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_6_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K6 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_7_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K7 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K1_MOMENTENKENNLINIE_FAKTOR_8_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K8 Min: -12.29 Default: 1 Max: 12.29 |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaption-momentenkennlinie-k2"></a>
### STATUS_ADAPTION_MOMENTENKENNLINIE_K2

Adaptionswerte Kupplungsmomentenkennlinie K2 ( Service ID 0x30, Identifier 0xA3 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_1_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K2 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_2_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K2 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_3_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K3 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_4_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K4 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_5_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K5 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_6_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K6 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_7_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K7 Min: -12.29 Default: 1 Max: 12.29 |
| STAT_K2_MOMENTENKENNLINIE_FAKTOR_8_WERT | real | Adaptionswerte Kupplungsmomentenkennlinie K8 Min: -12.29 Default: 1 Max: 12.29 |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-ventilkennlinie-pv1"></a>
### STATUS_VENTILKENNLINIE_PV1

Einlernwerte Ventilkennlinie PV1 ( Service ID 0x30, Identifier 0xA4 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_1_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_2_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_3_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_4_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_5_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_6_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_7_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_8_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_9_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_10_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_11_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_12_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_13_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_14_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_15_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_FAKTOR_16_WERT | real | Adaptionswerte Ventilkennlinie PV1 Min: -327,68  Max: 327,68 |
| STAT_PV1_VENTILKENNLINIE_EINH | string | Adaptionswerte Ventilkennlinie Einheit |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-ventilkennlinie-pv2"></a>
### STATUS_VENTILKENNLINIE_PV2

Einlernwerte Ventilkennlinie PV2 ( Service ID 0x30, Identifier 0xA5 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_1_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_2_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_3_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_4_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_5_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_6_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_7_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_8_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_9_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_10_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_11_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_12_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_13_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_14_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_15_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_FAKTOR_16_WERT | real | Adaptionswerte Ventilkennlinie PV2 Min: -327,68  Max: 327,68 |
| STAT_PV2_VENTILKENNLINIE_EINH | string | Adaptionswerte Ventilkennlinie Einheit |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaptionswert-ventilkennlinie-pv1-pv2"></a>
### STATUS_ADAPTIONSWERT_VENTILKENNLINIE_PV1_PV2

Adaptionswert für PV1 und PV2 Ventilkennlinie ( Service ID 0x30, Identifier 0xB0 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_ADAPTION_VENTILKENNLINIE_PV1_WERT | real | Adaptionswert für PV1 Ventilkennlinie |
| STAT_ADAPTION_VENTILKENNLINIE_PV1_EINH | string | Adaptionswert für PV1 Ventilkennlinie Einheit |
| STAT_ADAPTION_VENTILKENNLINIE_PV2_WERT | real | Adaptionswert für PV2 Ventilkennlinie |
| STAT_ADAPTION_VENTILKENNLINIE_PV2_EINH | string | Adaptionswert für PV2 Ventilkennlinie Einheit |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-ventilkennlinie-pv6"></a>
### STATUS_VENTILKENNLINIE_PV6

Einlernwerte Ventilkennlinie PV6 ( Service ID 0x30, Identifier 0xA6 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_1_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_2_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_3_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_4_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_5_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_6_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_7_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_8_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_9_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_10_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_11_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_12_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_13_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_14_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_15_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_FAKTOR_16_WERT | real | Adaptionswerte Ventilkennlinie PV6 Min: -327,68  Max: 327,68 |
| STAT_PV6_VENTILKENNLINIE_EINH | string | Adaptionswerte Ventilkennlinie Einheit |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaptionswert-pv6"></a>
### STATUS_ADAPTIONSWERT_PV6

Adaptionswerte  PV6 ( Service ID 0x30, Identifier 0xAA )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_ADAPTIONSWERT_PV6_STUETZSTELLE_0_WERT | real | Adaptionswerte für Ventilkennlinie PV6 ( Stützstelle 0) Min: -5 Max: 30 |
| STAT_ADAPTIONSWERT_PV6_STUETZSTELLE_0_EINH | string | Adaptionswerte für Ventilkennlinie PV6 ( Stützstelle 0) Einheit in [bar] |
| STAT_ADAPTIONSWERT_PV6_STUETZSTELLE_1_WERT | real | Adaptionswerte für Ventilkennlinie PV6 ( Stützstelle 1) Min: -5 Max: 30 |
| STAT_ADAPTIONSWERT_PV6_STUETZSTELLE_1_EINH | string | Adaptionswerte für Ventilkennlinie PV6 ( Stützstelle 1) Einheit in [bar] |
| STAT_ADAPTIONSWERT_PV6_STUETZSTELLE_2_WERT | real | Adaptionswerte für Ventilkennlinie PV6 ( Stützstelle 2) Min: -5 Max: 30 |
| STAT_ADAPTIONSWERT_PV6_STUETZSTELLE_2_EINH | string | Adaptionswerte für Ventilkennlinie PV6 ( Stützstelle 2) Einheit in [bar] |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-sperrstellung-pv7"></a>
### STATUS_SPERRSTELLUNG_PV7

Einlernwert Sperrstellung PV7 ( Service ID 0x30, Identifier 0xA7 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_PV7_SPERRVENTIL_WERT | int | Adaptionswerte Sperrventil Wert Min: 0 Max: 65535 |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaptionswert-getriebecode"></a>
### STATUS_ADAPTIONSWERT_GETRIEBECODE

Adaptionswerte  für den Getriebecode ( Service ID 0x30, Identifier 0xAB )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_ADAPTION_GETRIEBECODE_1_WERT | int | Adaptionswerte für den Getriebecode Wert 1 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_2_WERT | int | Adaptionswerte für den Getriebecode Wert 2 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_3_WERT | int | Adaptionswerte für den Getriebecode Wert 3 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_4_WERT | int | Adaptionswerte für den Getriebecode Wert 4 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_5_WERT | int | Adaptionswerte für den Getriebecode Wert 5 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_6_WERT | int | Adaptionswerte für den Getriebecode Wert 6 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_7_WERT | int | Adaptionswerte für den Getriebecode Wert 7 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_8_WERT | int | Adaptionswerte für den Getriebecode Wert 8 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_9_WERT | int | Adaptionswerte für den Getriebecode Wert 9 Min: 0 Max: 255 |
| STAT_ADAPTION_GETRIEBECODE_10_WERT | int | Adaptionswerte für den Getriebecode Wert 10 Min: 0 Max: 255 |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaptionswert-radsatzvariante"></a>
### STATUS_ADAPTIONSWERT_RADSATZVARIANTE

Adaptionswert  für die Radsatzvariante ( Service ID 0x30, Identifier 0xAC )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_ADAPTION_RADSATZVARIANTE_WERT | int | Adaptionswert für die Radsatzvariante Min: 0 Max: 255 |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaptionswert-hydraulikpumpe"></a>
### STATUS_ADAPTIONSWERT_HYDRAULIKPUMPE

Adaptionswert für die Hydraulikpumpe ( Service ID 0x30, Identifier 0xAD )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_ADAPTION_HYDRAULIKPUMPE_WERT | int | Adaptionswert für die Hydraulikpumpe Min: 0 Max: 255 |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaptionswert-temperatursensor"></a>
### STATUS_ADAPTIONSWERT_TEMPERATURSENSOR

Adaptionswert für den Temperatursensor Abspritzöl (Typ) ( Service ID 0x30, Identifier 0xAE )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_ADAPTION_TEMPERATURSENSOR_WERT | int | Adaptionswert für den Temperatursensor Abspritzöl (Typ) Min: 0 Max: 2 |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaptionswert-temperatursensor-widerstand"></a>
### STATUS_ADAPTIONSWERT_TEMPERATURSENSOR_WIDERSTAND

Adaptionswert für den Temperatursensor Abspritzöl Pull-Up-Wiederstandswert ( Service ID 0x30, Identifier 0xAF )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_ADAPTION_TEMPERATURSENSOR_WIDERSTAND_WERT | unsigned int | Adaptionswert für den Temperatursensor Abspritzöl Pull-Up-Wiederstandswert Min: 0 Max: 65535 |
| STAT_ADAPTION_TEMPERATURSENSOR_WIDERSTAND_EINH | string | Adaptionswert für den Temperatursensor Abspritzöl Einheit |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaptionswert-temp-sensor-widerstand"></a>
### STATUS_ADAPTIONSWERT_TEMP_SENSOR_WIDERSTAND

Adaptionswert für den Temperatursensor Abspritzöl Pull-Up-Wiederstandswert ( Service ID 0x30, Identifier 0xAF )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_ADAPTION_TEMP_SENSOR_WIDERSTAND_1_WERT | unsigned char | Adaptionswert für den Temperatursensor Abspritzöl Pull-Up-Wiederstandswert High Byte |
| STAT_ADAPTION_TEMP_SENSOR_WIDERSTAND_2_WERT | unsigned char | Adaptionswert für den Temperatursensor Abspritzöl Pull-Up-Wiederstandswert Low Byte |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-software-version-lesen"></a>
### SOFTWARE_VERSION_LESEN

Adaptionswerte Software Version ( Service ID 0x30, Identifier 0xA9 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| SOFTWARE_VERSION | char | Software Version |
| FORTLAUFENDE_NUMMER | char | Fortlaufende Nummer |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaptionswerte-semischlupf-gaenge"></a>
### STATUS_ADAPTIONSWERTE_SEMISCHLUPF_GAENGE

Adaptionswerte  für den Getriebecode ( Service ID 0x30, Identifier 0xB2 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_1_WERT | real | Adaptionswert des Semischlupfs für den 1. Gang Min: -120 Max: 120 |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_1_EINH | string | Adaptionswert des Semischlupfs für den 1. Gang Einheit Nm |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_2_WERT | real | Adaptionswert des Semischlupfs für den 2. Gang Min: -120 Max: 120 |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_2_EINH | string | Adaptionswert des Semischlupfs für den 2. Gang Einheit Nm |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_3_WERT | real | Adaptionswert des Semischlupfs für den 3. Gang Min: -120 Max: 120 |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_3_EINH | string | Adaptionswert des Semischlupfs für den 3. Gang Einheit Nm |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_4_WERT | real | Adaptionswert des Semischlupfs für den 4. Gang Min: -120 Max: 120 |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_4_EINH | string | Adaptionswert des Semischlupfs für den 4. Gang Einheit Nm |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_5_WERT | real | Adaptionswert des Semischlupfs für den 5. Gang Min: -120 Max: 120 |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_5_EINH | string | Adaptionswert des Semischlupfs für den 5. Gang Einheit Nm |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_6_WERT | real | Adaptionswert des Semischlupfs für den 6. Gang Min: -120 Max: 120 |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_6_EINH | string | Adaptionswert des Semischlupfs für den 6. Gang Einheit Nm |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_7_WERT | real | Adaptionswert des Semischlupfs für den 7. Gang Min: -120 Max: 120 |
| STAT_ADAPTIONSWERTE_SEMISCHLUPF_GANG_7_EINH | string | Adaptionswert des Semischlupfs für den 7. Gang Einheit Nm |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-status-adaptionswerte-drm"></a>
### STATUS_ADAPTIONSWERTE_DRM

Adaptionswerte DRM ( Service ID 0x30, Identifier 0xB1 )

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| DRM_HEX | binary | Adaptionswerte des DRM |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-adaptionswerte-pv1-schreiben"></a>
### STEUERN_ADAPTIONSWERTE_PV1_SCHREIBEN

Einlernwerte Ventilkennlinie PV1 ( Service ID 0x30, Identifier 0xA4 )

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PV1_DATEN_1 | char | Adaptionswert PV1 Daten High Byte 1 |
| PV1_DATEN_2 | char | Adaptionswert PV1 Daten Low Byte 1 |
| PV1_DATEN_3 | char | Adaptionswert PV1 Daten High Byte 2 |
| PV1_DATEN_4 | char | Adaptionswert PV1 Daten Low Byte 2 |
| PV1_DATEN_5 | char | Adaptionswert PV1 Daten High Byte 3 |
| PV1_DATEN_6 | char | Adaptionswert PV1 Daten Low Byte 3 |
| PV1_DATEN_7 | char | Adaptionswert PV1 Daten High Byte 4 |
| PV1_DATEN_8 | char | Adaptionswert PV1 Daten Low Byte 4 |
| PV1_DATEN_9 | char | Adaptionswert PV1 Daten High Byte 5 |
| PV1_DATEN_10 | char | Adaptionswert PV1 Daten Low Byte 5 |
| PV1_DATEN_11 | char | Adaptionswert PV1 Daten High Byte 6 |
| PV1_DATEN_12 | char | Adaptionswert PV1 Daten Low Byte 6 |
| PV1_DATEN_13 | char | Adaptionswert PV1 Daten High Byte 7 |
| PV1_DATEN_14 | char | Adaptionswert PV1 Daten Low Byte 7 |
| PV1_DATEN_15 | char | Adaptionswert PV1 Daten High Byte 8 |
| PV1_DATEN_16 | char | Adaptionswert PV1 Daten Low Byte 8 |
| PV1_DATEN_17 | char | Adaptionswert PV1 Daten High Byte 9 |
| PV1_DATEN_18 | char | Adaptionswert PV1 Daten Low Byte 9 |
| PV1_DATEN_19 | char | Adaptionswert PV1 Daten High Byte 10 |
| PV1_DATEN_20 | char | Adaptionswert PV1 Daten Low Byte 10 |
| PV1_DATEN_21 | char | Adaptionswert PV1 Daten High Byte 11 |
| PV1_DATEN_22 | char | Adaptionswert PV1 Daten Low Byte 11 |
| PV1_DATEN_23 | char | Adaptionswert PV1 Daten High Byte 12 |
| PV1_DATEN_24 | char | Adaptionswert PV1 Daten Low Byte 12 |
| PV1_DATEN_25 | char | Adaptionswert PV1 Daten High Byte 13 |
| PV1_DATEN_26 | char | Adaptionswert PV1 Daten Low Byte 13 |
| PV1_DATEN_27 | char | Adaptionswert PV1 Daten High Byte 14 |
| PV1_DATEN_28 | char | Adaptionswert PV1 Daten Low Byte 14 |
| PV1_DATEN_29 | char | Adaptionswert PV1 Daten High Byte 15 |
| PV1_DATEN_30 | char | Adaptionswert PV1 Daten Low Byte 15 |
| PV1_DATEN_31 | char | Adaptionswert PV1 Daten High Byte 16 |
| PV1_DATEN_32 | char | Adaptionswert PV1 Daten Low Byte 16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-adaptionswerte-pv2-schreiben"></a>
### STEUERN_ADAPTIONSWERTE_PV2_SCHREIBEN

Einlernwerte Ventilkennlinie PV2 ( Service ID 0x30, Identifier 0xA5 )

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PV2_DATEN_1 | char | Adaptionswert PV2 Daten High Byte 1 |
| PV2_DATEN_2 | char | Adaptionswert PV2 Daten Low Byte 1 |
| PV2_DATEN_3 | char | Adaptionswert PV2 Daten High Byte 2 |
| PV2_DATEN_4 | char | Adaptionswert PV2 Daten Low Byte 2 |
| PV2_DATEN_5 | char | Adaptionswert PV2 Daten High Byte 3 |
| PV2_DATEN_6 | char | Adaptionswert PV2 Daten Low Byte 3 |
| PV2_DATEN_7 | char | Adaptionswert PV2 Daten High Byte 4 |
| PV2_DATEN_8 | char | Adaptionswert PV2 Daten Low Byte 4 |
| PV2_DATEN_9 | char | Adaptionswert PV2 Daten High Byte 5 |
| PV2_DATEN_10 | char | Adaptionswert PV2 Daten Low Byte 5 |
| PV2_DATEN_11 | char | Adaptionswert PV2 Daten High Byte 6 |
| PV2_DATEN_12 | char | Adaptionswert PV2 Daten Low Byte 6 |
| PV2_DATEN_13 | char | Adaptionswert PV2 Daten High Byte 7 |
| PV2_DATEN_14 | char | Adaptionswert PV2 Daten Low Byte 7 |
| PV2_DATEN_15 | char | Adaptionswert PV2 Daten High Byte 8 |
| PV2_DATEN_16 | char | Adaptionswert PV2 Daten Low Byte 8 |
| PV2_DATEN_17 | char | Adaptionswert PV2 Daten High Byte 9 |
| PV2_DATEN_18 | char | Adaptionswert PV2 Daten Low Byte 9 |
| PV2_DATEN_19 | char | Adaptionswert PV2 Daten High Byte 10 |
| PV2_DATEN_20 | char | Adaptionswert PV2 Daten Low Byte 10 |
| PV2_DATEN_21 | char | Adaptionswert PV2 Daten High Byte 11 |
| PV2_DATEN_22 | char | Adaptionswert PV2 Daten Low Byte 11 |
| PV2_DATEN_23 | char | Adaptionswert PV2 Daten High Byte 12 |
| PV2_DATEN_24 | char | Adaptionswert PV2 Daten Low Byte 12 |
| PV2_DATEN_25 | char | Adaptionswert PV2 Daten High Byte 13 |
| PV2_DATEN_26 | char | Adaptionswert PV2 Daten Low Byte 13 |
| PV2_DATEN_27 | char | Adaptionswert PV2 Daten High Byte 14 |
| PV2_DATEN_28 | char | Adaptionswert PV2 Daten Low Byte 14 |
| PV2_DATEN_29 | char | Adaptionswert PV2 Daten High Byte 15 |
| PV2_DATEN_30 | char | Adaptionswert PV2 Daten Low Byte 15 |
| PV2_DATEN_31 | char | Adaptionswert PV2 Daten High Byte 16 |
| PV2_DATEN_32 | char | Adaptionswert PV2 Daten Low Byte 16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-adaptionswerte-pv6-schreiben"></a>
### STEUERN_ADAPTIONSWERTE_PV6_SCHREIBEN

Einlernwerte Ventilkennlinie PV6 ( Service ID 0x30, Identifier 0xA5 )

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PV6_DATEN_1 | char | Adaptionswert PV6 Daten High Byte 1 |
| PV6_DATEN_2 | char | Adaptionswert PV6 Daten Low Byte 1 |
| PV6_DATEN_3 | char | Adaptionswert PV6 Daten High Byte 2 |
| PV6_DATEN_4 | char | Adaptionswert PV6 Daten Low Byte 2 |
| PV6_DATEN_5 | char | Adaptionswert PV6 Daten High Byte 3 |
| PV6_DATEN_6 | char | Adaptionswert PV6 Daten Low Byte 3 |
| PV6_DATEN_7 | char | Adaptionswert PV6 Daten High Byte 4 |
| PV6_DATEN_8 | char | Adaptionswert PV6 Daten Low Byte 4 |
| PV6_DATEN_9 | char | Adaptionswert PV6 Daten High Byte 5 |
| PV6_DATEN_10 | char | Adaptionswert PV6 Daten Low Byte 5 |
| PV6_DATEN_11 | char | Adaptionswert PV6 Daten High Byte 6 |
| PV6_DATEN_12 | char | Adaptionswert PV6 Daten Low Byte 6 |
| PV6_DATEN_13 | char | Adaptionswert PV6 Daten High Byte 7 |
| PV6_DATEN_14 | char | Adaptionswert PV6 Daten Low Byte 7 |
| PV6_DATEN_15 | char | Adaptionswert PV6 Daten High Byte 8 |
| PV6_DATEN_16 | char | Adaptionswert PV6 Daten Low Byte 8 |
| PV6_DATEN_17 | char | Adaptionswert PV6 Daten High Byte 9 |
| PV6_DATEN_18 | char | Adaptionswert PV6 Daten Low Byte 9 |
| PV6_DATEN_19 | char | Adaptionswert PV6 Daten High Byte 10 |
| PV6_DATEN_20 | char | Adaptionswert PV6 Daten Low Byte 10 |
| PV6_DATEN_21 | char | Adaptionswert PV6 Daten High Byte 11 |
| PV6_DATEN_22 | char | Adaptionswert PV6 Daten Low Byte 11 |
| PV6_DATEN_23 | char | Adaptionswert PV6 Daten High Byte 12 |
| PV6_DATEN_24 | char | Adaptionswert PV6 Daten Low Byte 12 |
| PV6_DATEN_25 | char | Adaptionswert PV6 Daten High Byte 13 |
| PV6_DATEN_26 | char | Adaptionswert PV6 Daten Low Byte 13 |
| PV6_DATEN_27 | char | Adaptionswert PV6 Daten High Byte 14 |
| PV6_DATEN_28 | char | Adaptionswert PV6 Daten Low Byte 14 |
| PV6_DATEN_29 | char | Adaptionswert PV6 Daten High Byte 15 |
| PV6_DATEN_30 | char | Adaptionswert PV6 Daten Low Byte 15 |
| PV6_DATEN_31 | char | Adaptionswert PV6 Daten High Byte 16 |
| PV6_DATEN_32 | char | Adaptionswert PV6 Daten Low Byte 16 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-adaptionswerte-pv7-schreiben"></a>
### STEUERN_ADAPTIONSWERTE_PV7_SCHREIBEN

Einlernwerte Ventilkennlinie PV7 ( Service ID 0x30, Identifier 0xA5 )

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PV7_DATEN_1 | char | Adaptionswert PV7 Daten High Byte 1 |
| PV7_DATEN_2 | char | Adaptionswert PV7 Daten Low Byte 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-adaptionswert-getriebecode-schreiben"></a>
### STEUERN_ADAPTIONSWERT_GETRIEBECODE_SCHREIBEN

Adaptionswerte für den Getriebecode ( Service ID 0x30, Identifier 0xAB )

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| GETRIEBECODE_1 | char | Adaptionswerte für den Getriebecode Byte 1 |
| GETRIEBECODE_2 | char | Adaptionswerte für den Getriebecode Byte 2 |
| GETRIEBECODE_3 | char | Adaptionswerte für den Getriebecode Byte 3 |
| GETRIEBECODE_4 | char | Adaptionswerte für den Getriebecode Byte 4 |
| GETRIEBECODE_5 | char | Adaptionswerte für den Getriebecode Byte 5 |
| GETRIEBECODE_6 | char | Adaptionswerte für den Getriebecode Byte 6 |
| GETRIEBECODE_7 | char | Adaptionswerte für den Getriebecode Byte 7 |
| GETRIEBECODE_8 | char | Adaptionswerte für den Getriebecode Byte 8 |
| GETRIEBECODE_9 | char | Adaptionswerte für den Getriebecode Byte 9 |
| GETRIEBECODE_10 | char | Adaptionswerte für den Getriebecode Byte 10 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-adaptionswert-radsatzvariante-schreiben"></a>
### STEUERN_ADAPTIONSWERT_RADSATZVARIANTE_SCHREIBEN

Adaptionswert  für die Radsatzvariante ( Service ID 0x30, Identifier 0xAC )

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RADSATZVARIANTE_1 | char | Adaptionswert  für die Radsatzvariante Byte 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-adaptionswert-hydraulikpumpe-schreiben"></a>
### STEUERN_ADAPTIONSWERT_HYDRAULIKPUMPE_SCHREIBEN

Adaptionswert für die Hydraulikpumpe ( Service ID 0x30, Identifier 0xAD )

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| HYDRAULIKPUMPE_1 | char | Adaptionswert für die Hydraulikpumpe Byte 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-adaptionswert-temperatursensor-schreiben"></a>
### STEUERN_ADAPTIONSWERT_TEMPERATURSENSOR_SCHREIBEN

Adaptionswert  für den Temperatursensor (Typ) ( Service ID 0x30, Identifier 0xAE )

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TEMPERATURSENSOR_1 | char | Adaptionswert  für die Radsatzvariante Byte 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-adaptionswert-temperatursensor-widerstand-schreiben"></a>
### STEUERN_ADAPTIONSWERT_TEMPERATURSENSOR_WIDERSTAND_SCHREIBEN

Adaptionswert für den Temperatursensor Abspritzöl Pull-Up-Wiederstandswert ( Service ID 0x30, Identifier 0xAF )

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TEMPERATURSENSOR_WIDERSTAND_1 | char | Adaptionswert für den Temperatursensor Abspritzöl Pull-Up-Wiederstandswert - Byte 1 |
| TEMPERATURSENSOR_WIDERSTAND_2 | char | Adaptionswert für den Temperatursensor Abspritzöl Pull-Up-Wiederstandswert - Byte 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

<a id="job-steuern-adaption-zuruecksetzen"></a>
### STEUERN_ADAPTION_ZURUECKSETZEN

Adaptionswerte Zurücksetzen ( Service ID 0x30, Identifier 0x04 ) Voraussetzung für ordnungsgemäße Funktion ist, dass man in Anschluss die Zündung abschaltet und den Steuergeräte-Abfall abwartet, damit die Defaultwerte im NVRAM abgespeichert werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ADAPTIONSWERT | int | Eingebe des Hexwertes 0xA0 = Adaptionswerte Kisspoint K1 0xA1 = Adaptionswerte Kisspoint K2 0xA2 = Adaptionswerte Kupplungsmomentenkennlinie K1 0xA3 = Adaptionswerte Kupplungsmomentenkennlinie K2 0xB1 = Adaptionswerte für DRM 0xB2 = Adaptionswerte des Semischlupfs für Gänge 1-7 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY,wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex Auftrag vom Steuergerät |
| _TEL_ANTWORT | binary | Hex Antwort zum Steuergerät |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (121 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [HARTTEXTE](#table-harttexte) (14 × 2)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (139 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (138 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (205 × 9)
- [FARTTYP](#table-farttyp) (138 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (84 × 2)
- [HORTTEXTE](#table-horttexte) (139 × 2)
- [HDETAILSTRUKTUR](#table-hdetailstruktur) (7 × 2)
- [HUMWELTMATRIX](#table-humweltmatrix) (138 × 5)
- [HUMWELTTEXTE](#table-humwelttexte) (205 × 9)
- [HARTTYP](#table-harttyp) (138 × 5)
- [HARTTEXTEINDIVIDUELL](#table-harttexteindividuell) (84 × 2)
- [IORTTEXTE](#table-iorttexte) (139 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (138 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (205 × 9)
- [IARTTYP](#table-iarttyp) (138 × 5)
- [IARTTEXTEINDIVIDUELL](#table-iarttexteindividuell) (84 × 2)
- [GANGSTATUS](#table-gangstatus) (10 × 2)
- [GETRIEBESTATUS](#table-getriebestatus) (23 × 2)
- [KUPPLUNGSSTATI](#table-kupplungsstati) (10 × 2)
- [OBDSTEUERFUNKTION](#table-obdsteuerfunktion) (16 × 2)
- [SCHALTSTANGEPOSITION](#table-schaltstangeposition) (11 × 2)
- [IO_SETZEN](#table-io-setzen) (20 × 5)
- [TESTUNDEINLERNPRGTABELLE](#table-testundeinlernprgtabelle) (15 × 2)
- [STATUSTESTEINLERN](#table-statustesteinlern) (6 × 2)
- [STATUSEINLERNGETRIEBE](#table-statuseinlerngetriebe) (15 × 2)
- [STATUSEINLERNPV](#table-statuseinlernpv) (9 × 2)
- [FEHLERTESTEINLERNGETRIEBE](#table-fehlertesteinlerngetriebe) (36 × 2)
- [FEHLERTESTEINLERNKUEHLUNG](#table-fehlertesteinlernkuehlung) (9 × 2)
- [FEHLERTESTEINLERNPV](#table-fehlertesteinlernpv) (18 × 2)
- [FUMWELTTABELLE_5A57A](#table-fumwelttabelle-5a57a) (1 × 8)
- [FUMWELTTABELLE_5A60A](#table-fumwelttabelle-5a60a) (1 × 8)
- [FUMWELTTABELLE_5A60D](#table-fumwelttabelle-5a60d) (1 × 2)
- [FUMWELTTABELLE_5A61A](#table-fumwelttabelle-5a61a) (1 × 8)
- [FUMWELTTABELLE_5A61D](#table-fumwelttabelle-5a61d) (1 × 2)
- [FUMWELTTABELLE_5A62A](#table-fumwelttabelle-5a62a) (1 × 8)
- [FUMWELTTABELLE_5A62D](#table-fumwelttabelle-5a62d) (1 × 2)
- [FUMWELTTABELLE_5A63A](#table-fumwelttabelle-5a63a) (1 × 8)
- [FUMWELTTABELLE_5A63D](#table-fumwelttabelle-5a63d) (1 × 2)
- [FUMWELTTABELLE_5A64A](#table-fumwelttabelle-5a64a) (1 × 9)
- [FUMWELTTABELLE_5A64D](#table-fumwelttabelle-5a64d) (1 × 2)
- [FUMWELTTABELLE_5A65A](#table-fumwelttabelle-5a65a) (1 × 8)
- [FUMWELTTABELLE_5A65D](#table-fumwelttabelle-5a65d) (1 × 2)
- [FUMWELTTABELLE_5A66A](#table-fumwelttabelle-5a66a) (1 × 8)
- [FUMWELTTABELLE_5A66D](#table-fumwelttabelle-5a66d) (1 × 2)
- [FUMWELTTABELLE_5A67A](#table-fumwelttabelle-5a67a) (1 × 8)
- [FUMWELTTABELLE_5A67D](#table-fumwelttabelle-5a67d) (1 × 2)
- [FUMWELTTABELLE_5A68A](#table-fumwelttabelle-5a68a) (1 × 8)
- [FUMWELTTABELLE_5A68D](#table-fumwelttabelle-5a68d) (1 × 2)
- [FUMWELTTABELLE_5A69A](#table-fumwelttabelle-5a69a) (1 × 6)
- [FUMWELTTABELLE_5A6BA](#table-fumwelttabelle-5a6ba) (1 × 8)
- [FUMWELTTABELLE_5A6BD](#table-fumwelttabelle-5a6bd) (1 × 2)
- [FUMWELTTABELLE_5A6CA](#table-fumwelttabelle-5a6ca) (1 × 8)
- [FUMWELTTABELLE_5A6CD](#table-fumwelttabelle-5a6cd) (1 × 2)
- [FUMWELTTABELLE_5A6DA](#table-fumwelttabelle-5a6da) (1 × 8)
- [FUMWELTTABELLE_5A6DD](#table-fumwelttabelle-5a6dd) (1 × 2)
- [FUMWELTTABELLE_5A6EA](#table-fumwelttabelle-5a6ea) (1 × 8)
- [FUMWELTTABELLE_5A6ED](#table-fumwelttabelle-5a6ed) (1 × 2)
- [FUMWELTTABELLE_5A70A](#table-fumwelttabelle-5a70a) (1 × 6)
- [FUMWELTTABELLE_5A70D](#table-fumwelttabelle-5a70d) (1 × 2)
- [FUMWELTTABELLE_5A71A](#table-fumwelttabelle-5a71a) (1 × 6)
- [FUMWELTTABELLE_5A71D](#table-fumwelttabelle-5a71d) (1 × 2)
- [FUMWELTTABELLE_5A72A](#table-fumwelttabelle-5a72a) (1 × 8)
- [FUMWELTTABELLE_5A74A](#table-fumwelttabelle-5a74a) (1 × 8)
- [FUMWELTTABELLE_5A75A](#table-fumwelttabelle-5a75a) (1 × 8)
- [FUMWELTTABELLE_5A80A](#table-fumwelttabelle-5a80a) (1 × 4)
- [FUMWELTTABELLE_5A81A](#table-fumwelttabelle-5a81a) (1 × 4)
- [FUMWELTTABELLE_5A82A](#table-fumwelttabelle-5a82a) (1 × 4)
- [FUMWELTTABELLE_5A83A](#table-fumwelttabelle-5a83a) (1 × 4)
- [FUMWELTTABELLE_5A86A](#table-fumwelttabelle-5a86a) (1 × 6)
- [FUMWELTTABELLE_5072A](#table-fumwelttabelle-5072a) (1 × 8)
- [FUMWELTTABELLE_5073A](#table-fumwelttabelle-5073a) (1 × 3)
- [FUMWELTTABELLE_5074A](#table-fumwelttabelle-5074a) (1 × 3)
- [FUMWELTTABELLE_5A8BA](#table-fumwelttabelle-5a8ba) (1 × 6)
- [FUMWELTTABELLE_CF30A](#table-fumwelttabelle-cf30a) (1 × 8)
- [FUMWELTTABELLE_CF31A](#table-fumwelttabelle-cf31a) (1 × 8)
- [FUMWELTTABELLE_CF32A](#table-fumwelttabelle-cf32a) (1 × 8)
- [FUMWELTTABELLE_CF33A](#table-fumwelttabelle-cf33a) (1 × 8)
- [FUMWELTTABELLE_5A52A](#table-fumwelttabelle-5a52a) (1 × 7)
- [FUMWELTTABELLE_5A53A](#table-fumwelttabelle-5a53a) (1 × 8)
- [FUMWELTTABELLE_5A54A](#table-fumwelttabelle-5a54a) (1 × 8)
- [FUMWELTTABELLE_5A56A](#table-fumwelttabelle-5a56a) (1 × 8)
- [FUMWELTTABELLE_5A58A](#table-fumwelttabelle-5a58a) (1 × 7)
- [FUMWELTTABELLE_5A44A](#table-fumwelttabelle-5a44a) (1 × 4)
- [FUMWELTTABELLE_5A45A](#table-fumwelttabelle-5a45a) (1 × 4)
- [FUMWELTTABELLE_5027A](#table-fumwelttabelle-5027a) (1 × 3)
- [FUMWELTTABELLE_5028A](#table-fumwelttabelle-5028a) (1 × 4)
- [FUMWELTTABELLE_5029A](#table-fumwelttabelle-5029a) (1 × 3)
- [FUMWELTTABELLE_5030A](#table-fumwelttabelle-5030a) (1 × 3)
- [FUMWELTTABELLE_5A76A](#table-fumwelttabelle-5a76a) (1 × 3)
- [FUMWELTTABELLE_5054A](#table-fumwelttabelle-5054a) (1 × 7)
- [FUMWELTTABELLE_5059A](#table-fumwelttabelle-5059a) (1 × 6)
- [FUMWELTTABELLE_5060A](#table-fumwelttabelle-5060a) (1 × 6)
- [FUMWELTTABELLE_5055A](#table-fumwelttabelle-5055a) (1 × 4)
- [FUMWELTTABELLE_5A87D](#table-fumwelttabelle-5a87d) (1 × 5)
- [FUMWELTTABELLE_5056A](#table-fumwelttabelle-5056a) (1 × 3)
- [FUMWELTTABELLE_5A5BA](#table-fumwelttabelle-5a5ba) (1 × 8)
- [FUMWELTTABELLE_5A42A](#table-fumwelttabelle-5a42a) (1 × 6)
- [FUMWELTTABELLE_5031A](#table-fumwelttabelle-5031a) (1 × 6)
- [FUMWELTTABELLE_CF3EA](#table-fumwelttabelle-cf3ea) (1 × 6)
- [FUMWELTTABELLE_5061A](#table-fumwelttabelle-5061a) (1 × 4)
- [FUMWELTTABELLE_5131A](#table-fumwelttabelle-5131a) (1 × 7)
- [FUMWELTTABELLE_5132A](#table-fumwelttabelle-5132a) (1 × 7)
- [FUMWELTTABELLE_5132D](#table-fumwelttabelle-5132d) (1 × 3)
- [FUMWELTTABELLE_5133A](#table-fumwelttabelle-5133a) (1 × 7)
- [FUMWELTTABELLE_5134A](#table-fumwelttabelle-5134a) (1 × 8)
- [FEHLERTESTEINLERNKUPPLUNG](#table-fehlertesteinlernkupplung) (15 × 2)
- [FUMWELTTABELLE_5A87A](#table-fumwelttabelle-5a87a) (1 × 3)
- [FUMWELTTABELLE_5062A1](#table-fumwelttabelle-5062a1) (1 × 4)
- [FEHLERTESTEINLERNPARKSPERRENMAGNET](#table-fehlertesteinlernparksperrenmagnet) (8 × 2)
- [FUMWELTTABELLE_5137A](#table-fumwelttabelle-5137a) (1 × 6)
- [FUMWELTTEXTE01](#table-fumwelttexte01) (3 × 2)
- [FUMWELTTEXTE02](#table-fumwelttexte02) (7 × 2)
- [FUMWELTTEXTE03](#table-fumwelttexte03) (11 × 2)
- [FUMWELTTEXTE04](#table-fumwelttexte04) (11 × 2)
- [FUMWELTTEXTE05](#table-fumwelttexte05) (11 × 2)
- [FUMWELTTEXTE06](#table-fumwelttexte06) (11 × 2)
- [FUMWELTTEXTE07](#table-fumwelttexte07) (4 × 2)
- [FUMWELTTEXTE08](#table-fumwelttexte08) (4 × 2)
- [FUMWELTTEXTE09](#table-fumwelttexte09) (3 × 2)
- [FUMWELTTEXTE10](#table-fumwelttexte10) (3 × 2)
- [FUMWELTTEXTE11](#table-fumwelttexte11) (3 × 2)
- [FUMWELTTEXTE12](#table-fumwelttexte12) (3 × 2)
- [FUMWELTTEXTE13](#table-fumwelttexte13) (13 × 2)
- [FUMWELTTEXTE14](#table-fumwelttexte14) (6 × 2)
- [FUMWELTTEXTE15](#table-fumwelttexte15) (5 × 2)
- [FUMWELTTEXTE16](#table-fumwelttexte16) (7 × 2)
- [FUMWELTTEXTE17](#table-fumwelttexte17) (3 × 2)
- [FUMWELTTEXTE18](#table-fumwelttexte18) (37 × 2)
- [FUMWELTTEXTE19](#table-fumwelttexte19) (4 × 2)
- [FUMWELTTEXTE20](#table-fumwelttexte20) (4 × 2)
- [FUMWELTTEXTE21](#table-fumwelttexte21) (6 × 2)
- [FUMWELTTEXTE22](#table-fumwelttexte22) (3 × 2)
- [FUMWELTTEXTE23](#table-fumwelttexte23) (11 × 2)
- [FUMWELTTEXTE24](#table-fumwelttexte24) (6 × 2)
- [FUMWELTTEXTE25](#table-fumwelttexte25) (6 × 2)
- [FUMWELTTEXTE26](#table-fumwelttexte26) (3 × 2)
- [FUMWELTTEXTE27](#table-fumwelttexte27) (3 × 2)
- [FUMWELTTEXTE28](#table-fumwelttexte28) (3 × 2)
- [FUMWELTTEXTE29](#table-fumwelttexte29) (9 × 2)
- [FUMWELTTEXTE30](#table-fumwelttexte30) (8 × 2)
- [FUMWELTTABELLE_5137D](#table-fumwelttabelle-5137d) (1 × 3)
- [FUMWELTTEXTE31](#table-fumwelttexte31) (11 × 2)
- [FUMWELTTEXTE32](#table-fumwelttexte32) (11 × 2)
- [FUMWELTTEXTE33](#table-fumwelttexte33) (16 × 2)
- [FUMWELTTEXTE34](#table-fumwelttexte34) (4 × 2)
- [FUMWELTTABELLE_5131D](#table-fumwelttabelle-5131d) (1 × 3)
- [FUMWELTTEXTE35](#table-fumwelttexte35) (37 × 2)
- [FUMWELTTEXTE36](#table-fumwelttexte36) (9 × 2)
- [FUMWELTTEXTE37](#table-fumwelttexte37) (11 × 2)
- [FUMWELTTEXTE38](#table-fumwelttexte38) (6 × 2)
- [FUMWELTTABELLE_5055D](#table-fumwelttabelle-5055d) (1 × 3)
- [FUMWELTTABELLE_5056D](#table-fumwelttabelle-5056d) (1 × 3)
- [FUMWELTTEXTE39](#table-fumwelttexte39) (3 × 2)
- [FUMWELTTABELLE_5059D](#table-fumwelttabelle-5059d) (1 × 3)
- [FUMWELTTABELLE_5060D](#table-fumwelttabelle-5060d) (1 × 3)
- [FUMWELTTABELLE_5054D](#table-fumwelttabelle-5054d) (1 × 3)
- [FUMWELTTABELLE_5062A](#table-fumwelttabelle-5062a) (1 × 5)
- [FUMWELTTABELLE_5138A](#table-fumwelttabelle-5138a) (1 × 8)
- [FUMWELTTABELLE_5057A](#table-fumwelttabelle-5057a) (1 × 7)
- [FUMWELTTABELLE_5057D](#table-fumwelttabelle-5057d) (1 × 3)
- [FUMWELTTABELLE_5139A](#table-fumwelttabelle-5139a) (1 × 7)
- [FUMWELTTABELLE_5129A](#table-fumwelttabelle-5129a) (1 × 7)
- [FUMWELTTEXTE40](#table-fumwelttexte40) (8 × 2)
- [FUMWELTTABELLE_5A46A](#table-fumwelttabelle-5a46a) (1 × 5)
- [FUMWELTTABELLE_5A47A](#table-fumwelttabelle-5a47a) (1 × 5)
- [FUMWELTTABELLE_5A48A](#table-fumwelttabelle-5a48a) (1 × 5)
- [FUMWELTTABELLE_5A4BA](#table-fumwelttabelle-5a4ba) (1 × 6)
- [FUMWELTTABELLE_5A4CA](#table-fumwelttabelle-5a4ca) (1 × 6)
- [FUMWELTTABELLE_5A55A](#table-fumwelttabelle-5a55a) (1 × 6)
- [FUMWELTTABELLE_5021A](#table-fumwelttabelle-5021a) (1 × 3)
- [FUMWELTTABELLE_5022A](#table-fumwelttabelle-5022a) (1 × 3)
- [FUMWELTTABELLE_5023A](#table-fumwelttabelle-5023a) (1 × 3)
- [FUMWELTTABELLE_5024A](#table-fumwelttabelle-5024a) (1 × 3)
- [FUMWELTTABELLE_5A84](#table-fumwelttabelle-5a84) (1 × 8)
- [FUMWELTTEXTE41](#table-fumwelttexte41) (9 × 2)
- [FUMWELTTEXTE42](#table-fumwelttexte42) (3 × 2)
- [FUMWELTTABELLE_5A88A](#table-fumwelttabelle-5a88a) (1 × 3)
- [FUMWELTTABELLE_5A88D](#table-fumwelttabelle-5a88d) (1 × 5)
- [FUMWELTTABELLE_CF29A](#table-fumwelttabelle-cf29a) (1 × 5)
- [FUMWELTTEXTE18N](#table-fumwelttexte18n) (257 × 2)
- [FUMWELTTEXTE35N](#table-fumwelttexte35n) (256 × 2)
- [STATUSKLACKERN](#table-statusklackern) (3 × 2)

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

Dimensions: 121 rows × 2 columns

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

<a id="table-harttexte"></a>
### HARTTEXTE

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

Dimensions: 139 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5021 | Schaltventil SV1: Überstrom |
| 0x5022 | Schaltventil SV2: Überstrom |
| 0x5023 | Schaltventil SV3: Überstrom |
| 0x5024 | Schaltventil SV4: Überstrom |
| 0x5025 | Kupplung 1: Adaption Kisspoint |
| 0x5026 | Kupplung 2: Adaption Kisspoint |
| 0x5027 | Systemdruck: falscher Druck |
| 0x5028 | PV6: Adaption |
| 0x5029 | Kupplung 1: Befüllzeit |
| 0x5030 | Kupplung 2: Befüllzeit |
| 0x5031 | Kupplung 2: Adaption Referenzmoment |
| 0x5054 | Parksperre: Überschreiten der Sicherheitszeit bei Betätigung |
| 0x5055 | Parksperre: hängendes Absperrventil |
| 0x5056 | Parksperrensensor |
| 0x5057 | Überschreiten der Sicherheitszeit beim Auslegen |
| 0x5058 | Parksperre:Betätigung Taster unplausibel |
| 0x5059 | Parksperre: Unerlaubte Bewegung |
| 0x5060 | Parksperre: elektrischer Fehler am Parksperrenmagnet |
| 0x5061 | Fehler Parksperrenschieber |
| 0x5062 | Fehler Parksperrenhaken |
| 0x5063 | N-Haltephase über Tester deaktiviert |
| 0x5072 | Versorgung der Ventilgruppe 1: fehlerhaft |
| 0x5073 | Versorgung der Ventilgruppe 2: fehlerhaft |
| 0x5074 | Versorgung der Ventilgruppe 3: fehlerhaft |
| 0x5124 | Ebene2 Diagnose |
| 0x5126 | Energiesparmodi: Modus aktiv |
| 0x5127 | Verlängerung Nachlaufzeit: fehlerhaft |
| 0x5128 | N-Haltephase seit 20min aktiv |
| 0x5129 | Elektr. Fehler am Parksperrenmagnet (Bestromung nicht möglich) |
| 0x5130 | Selbstbeschleuniger |
| 0x5131 | Ebene2 Schutzziele Verletzung 13, 14, 16, 19, Temic |
| 0x5132 | Ebene2 Schutzziele Verletzung 4a, 3_6 |
| 0x5133 | Ebene2 Schutzziele Verletzung 1, 10 |
| 0x5134 | Ebene2 Schutzziele Verletzung 9a, 9b |
| 0x5135 | Ebene2s Fehler |
| 0x5136 | PS Missuse |
| 0x5137 | Einlernen Kisspoint: abgebrochen |
| 0x5138 | Anforderung CAN-Notlauf |
| 0x5139 | Unerlaubtes Einfallen der Parksperre |
| 0x5A25 | Botschaften Wählhebel: fehlerhaft |
| 0x5A41 | Drucksensor Kupplung 1: Totalausfall |
| 0x5A42 | Kupplung 1: Adaption Referenzmoment |
| 0x5A43 | Drucksensor Kupplung 2: Totalausfall |
| 0x5A44 | Kupplung 1: falscher Druck |
| 0x5A45 | Kupplung 2: falscher Druck |
| 0x5A46 | Regelventil PV3: Kurzschluss/Wicklungsschluss |
| 0x5A47 | Regelventil PV4:  Kurzschluss/Wicklungsschluss |
| 0x5A48 | Regelventil PV6: Kurzschluss/Wicklungsschluss |
| 0x5A4B | Regelventil PV1: Kurzschluss/Wicklungsschluss |
| 0x5A4C | Regelventil PV2: Kurzschluss/Wicklungsschluss |
| 0x5A52 | Getriebeüberhitzung: Phase Gelb |
| 0x5A53 | Getriebeüberhitzung: Phase Rot |
| 0x5A54 | Getriebeüberhitzung: Phase Schwarz |
| 0x5A55 | Regelventil PV7: Kurzschluss/Wicklungsschluss |
| 0x5A56 | Kühlung: kein Kühlölstrom detektiert |
| 0x5A57 | Abspritzsensor: Wärmeeintrag |
| 0x5A58 | Abspritzsensor: elektrischer Defekt |
| 0x5A59 | Abschaltpfad 1: Cut-Off Ventil 1 schaltet nicht auf Tank |
| 0x5A5A | Abschaltpfad 2: Cut-Off Ventil 2 schaltet nicht auf Tank |
| 0x5A5B | Regelventil PV7: Ventil klemmt |
| 0x5A60 | Getriebe: Überdrehzahl |
| 0x5A61 | Schaltstange 1/3: Fehler |
| 0x5A62 | Schaltstange 2/R: Fehler |
| 0x5A63 | Schaltstange 6/4: Fehler |
| 0x5A64 | Schaltstange 5/7: Fehler |
| 0x5A65 | Sensor Schaltstange 6/4: Fehler |
| 0x5A66 | Sensor Schaltstange 5/7: Fehler |
| 0x5A67 | Sensor Schaltstange 2/R: Fehler |
| 0x5A68 | Sensor Schaltstange 1/3: Fehler |
| 0x5A69 | Nachadaptionswert Gang: Verschleißgrenze erreicht |
| 0x5A6A | Nachadaptionswert Neutrallage: Verschleißgrenze erreicht |
| 0x5A6B | Schaltstange 1/3: Fehler Gang |
| 0x5A6C | Schaltstange 2/R:Fehler Gang |
| 0x5A6D | Schaltstange 5/7: Fehler Gang |
| 0x5A6E | Schaltstange 6/4: Fehler Gang |
| 0x5A70 | Temperatursensor 1: fehlerhaft |
| 0x5A71 | Temperatursensor 2: fehlerhaft |
| 0x5A72 | Sensor Versorgungsspannung: fehlerhaft |
| 0x5A73 | Schaltwippen: fehlerhafter Spannungswert |
| 0x5A74 | Eingangsdrehzahlsensor Teilgetriebe 1: Wert unplausibel |
| 0x5A75 | Eingangsdrehzahlsensor Teilgetriebe 2: Wert unplausibel |
| 0x5A76 | Antriebsdrehzahlsensor: Wert unplausibel |
| 0x5A80 | Vorspannung UH2_7V4: fehlerhaft |
| 0x5A81 | Spannung intern 5V (VCC5 5V): fehlerhaft |
| 0x5A82 | Sensorversorgung SV1_ 5V: fehlerhaft |
| 0x5A83 | Sensorversorgung SV2_ 5V: fehlerhaft |
| 0x5A84 | Fehler mit gemultiplexten Umweltdaten |
| 0x5A85 | Core Eigendiagnose: Fehler |
| 0x5A86 | Temperaturwerts TC1766: fehlerhafte Plausibilisierung |
| 0x5A87 | Getriebesteuerung: interner Fehler (EEPROM Daten) |
| 0x5A88 | Getriebesteuerung: interner Fehler (EEPROM Daten, Block C-E) |
| 0x5A8B | Übertemperatur Getriebe |
| 0xCF07 | Kommunikationsfehler: PT-CAN |
| 0xCF10 | Botschaft (Anforderung Radmoment Antriebsstrang, PT-CAN) vom LDM |
| 0xCF11 | Botschaft (Außentemperatur /Relativzeit, PT-CAN) vom Kombiinstrument |
| 0xCF12 | Botschaft (Bedienung Getriebewahlschalter 2, PT-CAN) vom GWS |
| 0xCF13 | Botschaft (Drehmoment 1, PT-CAN) von der Motorsteuerung |
| 0xCF14 | Botschaft (Drehmoment 2, PT-CAN) von der Motorsteuerung |
| 0xCF15 | Botschaft (Drehmoment 3, PT-CAN) von der Motorsteuerung |
| 0xCF16 | Botschaft (Drehmomentanforderung ACC, PT-CAN) vom ACC |
| 0xCF17 | Botschaft (Drehmomentanforderung DSC, PT-CAN) von der DSC |
| 0xCF18 | Botschaft (Geschwindigkeit, PT-CAN) von der DSC |
| 0xCF19 | Botschaft (Kilometerstand /Reichweite, PT-CAN) vom Kombiinstrument |
| 0xCF1A | Botschaft (Klemmenstatus PT-CAN) vom CAS |
| 0xCF1B | Botschaft (Lenkradwinkel, PT-CAN) von der DSC |
| 0xCF1C | Botschaft (Motordaten, PT-CAN) vom der Motorsteuerung |
| 0xCF1D | Botschaft (Raddrücke, PT-CAN) von der RDC |
| 0xCF1E | Botschaft (Radgeschwindigkeit, PT-CAN) von der DSC |
| 0xCF1F | Botschaft (Radmoment Antriebsstrang 2, PT-CAN) von der Motorsteuerung |
| 0xCF20 | Botschaft (Radtoleranzabgleich, PT-CAN) von der DSC |
| 0xCF21 | Botschaft (Rohdaten Längsbeschleunigung, PT-CAN) von der DSC |
| 0xCF22 | Botschaft (Sitzbelegung/Gurtkontakte, PT-CAN) vom SSFA |
| 0xCF23 | Botschaft (Status Anhänger, PT-CAN) vom AHM |
| 0xCF24 | Botschaft (Status DSC, PT-CAN) von der DSC |
| 0xCF25 | Botschaft (Status Kontakt Handbremse, PT-CAN) vom JBBF |
| 0xCF26 | Botschaft (ZV und Klappenzustand, PT-CAN) vom CAS |
| 0xCF27 | Botschaft (Bedienung Getriebewahlschalter 2, LIN) vom GWS |
| 0xCF28 | Botschaft (OBD-Daten Motor, PT-CAN) von der Motorsteuerung |
| 0xCF29 | Botschaft (Status MSA, PT-CAN) von der Motorsteuerung |
| 0xCF30 | Signal von der DSC: Geschwindigkeit Rad VL |
| 0xCF31 | Signal von der DSC: Geschwindigkeit Rad VR |
| 0xCF32 | Signal von der DSC: Geschwindigkeit Rad HL |
| 0xCF33 | Signal von der DSC: Geschwindigkeit Rad HR |
| 0xCF34 | Signal von der Motorsteuerung: Drehmoment_Ist_DME |
| 0xCF35 | Signal von der Motorsteuerung: Bremslichtschalter |
| 0xCF36 | Signal von der Motorsteuerung: Winkel Fahrpedal |
| 0xCF37 | Signal von der DSC: Status_DSC |
| 0xCF38 | Signal von der Motorsteuerung: Drehzahl_Leerlauf_Soll |
| 0xCF39 | Signal vom CAS: Status Klemme 15 |
| 0xCF3A | Signal vom CAS: Status Schlüssel steckt |
| 0xCF3B | Signal vom  FRM: Status Türkontakt Fahrer |
| 0xCF3C | Signal vom SSFA: Klasse Gewicht Sitz |
| 0xCF3D | Signal vom GWS: Signal unplausibel |
| 0xCF3E | Signal von der Motorsteuerung: Drehzahl Motor |
| 0xCF3F | Signal vom CAS: Status Passive-Access Aktiv |
| 0xCF40 | Signal vom CAS: Status Schlüssel gültig |
| 0xCF41 | Signal vom SSFA: Schalter Gurtschloß FA |
| 0xCF42 | Signal von der DSC: Alle 4 Raddrehzahlen ungültig |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | nein |
| F_PCODE | ja |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 138 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x5A41 | 0x01 | 0x40 | 0x49 | 0x4B |
| 0x5A43 | 0x01 | 0x40 | 0x4A | 0x4C |
| 0x5A44 | 0x4B | 0x4D | 0x02 | FUmweltTabelle_5A44a |
| 0x5A45 | 0x4C | 0x4E | 0x02 | FUmweltTabelle_5A45a |
| 0x5A46 | 0x01 | FUmweltTabelle_5A46a | 0xA9 | 0x13 |
| 0x5A47 | 0x01 | FUmweltTabelle_5A47a | 0xA9 | 0x13 |
| 0x5A48 | 0x01 | 0x3B | FUmweltTabelle_5A48a | 0xA8 |
| 0x5A4B | FUmweltTabelle_5A4Ba | 0xA7 | 0x2F | 0x4F |
| 0x5A4C | FUmweltTabelle_5A4Ca | 0xA8 | 0x30 | 0x50 |
| 0x5A52 | 0x02 | FUmweltTabelle_5A52a | 0x78 | 0x7B |
| 0x5A53 | 0x02 | FUmweltTabelle_5A53a | 0x78 | 0x7B |
| 0x5A54 | 0x02 | FUmweltTabelle_5A54a | 0x78 | 0x7B |
| 0x5A55 | 0x01 | FUmweltTabelle_5A55a | 0xA8 | 0x7B |
| 0x5A56 | 0x84 | 0x85 | 0x2D | FUmweltTabelle_5A56a |
| 0x5A57 | 0x84 | 0x85 | 0x2D | FUmweltTabelle_5A57a |
| 0x5A58 | 0x01 | 0x02 | 0x3D | FUmweltTabelle_5A58a |
| 0x5A59 | 0x02 | 0x4B | 0x4D | 0x59 |
| 0x5A5A | 0x02 | 0x4C | 0x4E | 0x5A |
| 0x5A5B | 0x2D | 0x0A | 0x0B | FUmweltTabelle_5A5Ba |
| 0x5021 | FUmweltTabelle_5021a | 0xA7 | 0x2F | 0x4F |
| 0x5022 | FUmweltTabelle_5022a | 0xA8 | 0x30 | 0x50 |
| 0x5023 | FUmweltTabelle_5023a | 0x18 | 0x3C | 0xA9 |
| 0x5024 | FUmweltTabelle_5024a | 0x18 | 0x3C | 0xA9 |
| 0x5025 | 0x02 | 0x0B | 0x51 | - |
| 0x5026 | 0x02 | 0x0B | 0x51 | - |
| 0x5A42 | 0x51 | 0x79 | 0x4B | FUmweltTabelle_5A42a |
| 0x5031 | 0x51 | 0x7A | 0x4C | FUmweltTabelle_5031a |
| 0x5027 | 0x88 | 0x89 | 0x0B | FUmweltTabelle_5027a |
| 0x5028 | 0x02 | 0x0A | 0x0C | FUmweltTabelle_5028a |
| 0x5029 | 0x4B | 0x4D | 0x02 | FUmweltTabelle_5029a |
| 0x5030 | 0x4C | 0x4E | 0x02 | FUmweltTabelle_5030a |
| 0x5137 | FUmweltTabelle_5137a | 0x1D | 0x1E | FUmweltTabelle_5137d |
| 0x5A60 | 0x01 | 0x0A | FUmweltTabelle_5A60a | FUmweltTabelle_5A60d |
| 0x5A61 | 0x0F | 0x17 | FUmweltTabelle_5A61a | FUmweltTabelle_5A61d |
| 0x5A62 | 0x10 | 0x17 | FUmweltTabelle_5A62a | FUmweltTabelle_5A62d |
| 0x5A63 | 0x12 | 0x17 | FUmweltTabelle_5A63a | FUmweltTabelle_5A63d |
| 0x5A64 | 0x11 | FUmweltTabelle_5A64a | FUmweltTabelle_5A64d | - |
| 0x5A65 | 0x19 | 0x1A | FUmweltTabelle_5A65a | FUmweltTabelle_5A65d |
| 0x5A66 | 0x19 | 0x1A | FUmweltTabelle_5A66a | FUmweltTabelle_5A66d |
| 0x5A67 | 0x19 | 0x1A | FUmweltTabelle_5A67a | FUmweltTabelle_5A67d |
| 0x5A68 | 0x19 | 0x1A | FUmweltTabelle_5A68a | FUmweltTabelle_5A68d |
| 0x5A69 | 0x21 | 0x22 | 0x23 | FUmweltTabelle_5A69a |
| 0x5A6A | 0x52 | 0x53 | 0x54 | 0x55 |
| 0x5A6B | 0x0F | 0x17 | FUmweltTabelle_5A6Ba | FUmweltTabelle_5A6Bd |
| 0x5A6C | 0x10 | 0x17 | FUmweltTabelle_5A6Ca | FUmweltTabelle_5A6Cd |
| 0x5A6D | 0x11 | 0x17 | FUmweltTabelle_5A6Da | FUmweltTabelle_5A6Dd |
| 0x5A6E | 0x12 | 0x17 | FUmweltTabelle_5A6Ea | FUmweltTabelle_5A6Ed |
| 0x5A70 | 0x01 | 0x0B | FUmweltTabelle_5A70a | FUmweltTabelle_5A70d |
| 0x5A71 | 0x01 | 0x0B | FUmweltTabelle_5A71a | FUmweltTabelle_5A71d |
| 0x5A72 | FUmweltTabelle_5A72a | 0xA7 | 0xA8 | 0xA9 |
| 0x5A73 | 0x01 | 0x0B | 0x58 | - |
| 0x5A74 | 0x01 | 0x0B | 0x0C | FUmweltTabelle_5A74a |
| 0x5A75 | 0x01 | 0x0B | 0x0D | FUmweltTabelle_5A75a |
| 0x5A76 | 0x01 | 0x77 | 0x51 | FUmweltTabelle_5A76a |
| 0x5A80 | 0x01 | 0x0B | 0x3D | FUmweltTabelle_5A80a |
| 0x5A81 | 0x01 | 0x0B | 0x3D | FUmweltTabelle_5A81a |
| 0x5A82 | 0x01 | 0x0B | 0x3D | FUmweltTabelle_5A82a |
| 0x5A83 | 0x01 | 0x0B | 0x3D | FUmweltTabelle_5A83a |
| 0x5A84 | 0xF5 | 0xF6 | 0xF7 | FUmweltTabelle_5A84 |
| 0x5A85 | 0x01 | 0xA3 | 0x56 | 0x57 |
| 0x5A86 | 0x01 | FUmweltTabelle_5A86a | 0x38 | 0x39 |
| 0x5A87 | FUmweltTabelle_5A87a | 0x7E | FUmweltTabelle_5A87d | 0x82 |
| 0x5A88 | FUmweltTabelle_5A88a | 0x7E | FUmweltTabelle_5A88d | 0x82 |
| 0x5072 | 0x01 | 0x0B | 0x3A | FUmweltTabelle_5072a |
| 0x5073 | 0x01 | 0x0B | 0x3A | FUmweltTabelle_5073a |
| 0x5074 | 0x01 | 0x0B | 0x3A | FUmweltTabelle_5074a |
| 0x5A8B | 0x01 | FUmweltTabelle_5A8Ba | 0x38 | 0x39 |
| 0xCF07 | 0x01 | 0x0B | 0x41 | - |
| 0xCF10 | 0x01 | 0x0B | - | - |
| 0xCF11 | 0x01 | 0x0B | - | - |
| 0xCF12 | 0x01 | 0x0B | - | - |
| 0xCF13 | 0x01 | 0x0B | - | - |
| 0xCF14 | 0x01 | 0x0B | - | - |
| 0xCF15 | 0x01 | 0x0B | - | - |
| 0xCF16 | 0x01 | 0x0B | - | - |
| 0xCF17 | 0x01 | 0x0B | - | - |
| 0xCF18 | 0x01 | 0x0B | - | - |
| 0xCF19 | 0x01 | 0x0B | - | - |
| 0xCF1A | 0x01 | 0x0B | - | - |
| 0xCF1B | 0x01 | 0x0B | - | - |
| 0xCF1C | 0x01 | 0x0B | - | - |
| 0xCF1D | 0x01 | 0x0B | - | - |
| 0xCF1E | 0x01 | 0x0B | - | - |
| 0xCF1F | 0x01 | 0x0B | - | - |
| 0xCF20 | 0x01 | 0x0B | - | - |
| 0xCF21 | 0x01 | 0x0B | - | - |
| 0xCF22 | 0x01 | 0x0B | - | - |
| 0xCF23 | 0x01 | 0x0B | - | - |
| 0xCF24 | 0x01 | 0x0B | - | - |
| 0xCF25 | 0x01 | 0x0B | - | - |
| 0xCF26 | 0x01 | 0x0B | - | - |
| 0xCF27 | 0x01 | 0x0B | - | - |
| 0xCF28 | 0x01 | 0x0B | - | - |
| 0xCF29 | 0x01 | 0x0B | FUmweltTabelle_CF29a | - |
| 0xCF30 | 0x01 | 0x2D | 0x0C | FUmweltTabelle_CF30a |
| 0xCF31 | 0x01 | 0x2D | 0x0C | FUmweltTabelle_CF31a |
| 0xCF32 | 0x01 | 0x2D | 0x0C | FUmweltTabelle_CF32a |
| 0xCF33 | 0x01 | 0x2D | 0x0C | FUmweltTabelle_CF33a |
| 0xCF34 | 0x01 | 0x0B | - | - |
| 0xCF35 | 0x01 | 0x0B | - | - |
| 0xCF36 | 0x01 | 0x0B | - | - |
| 0xCF37 | 0x01 | 0x0B | - | - |
| 0xCF38 | 0x01 | 0x0B | - | - |
| 0xCF39 | 0x01 | 0x0B | - | - |
| 0xCF3A | 0x01 | 0x0B | - | - |
| 0xCF3B | 0x01 | 0x0B | - | - |
| 0xCF3C | 0x01 | 0x0B | - | - |
| 0xCF3D | 0x01 | 0x0B | - | - |
| 0xCF3E | 0x01 | 0x0B | 0x77 | FUmweltTabelle_CF3Ea |
| 0xCF3F | 0x01 | 0x0B | - | - |
| 0xCF40 | 0x01 | 0x0B | - | - |
| 0xCF41 | 0x01 | 0x0B | - | - |
| 0xCF42 | 0x01 | 0x0B | - | - |
| 0x5124 | 0xB9 | 0xBA | 0x76 | - |
| 0x5A25 | 0x01 | 0x0B | - | - |
| 0x5126 | 0x01 | 0x0B | - | - |
| 0x5127 | 0x01 | 0x0B | - | - |
| 0x5128 | 0x01 | 0x0B | - | - |
| 0x5129 | 0x6C | 0xE9 | 0x6A | FUmweltTabelle_5129a |
| 0x5136 | 0x01 | 0x0B | - | - |
| 0x5138 | 0xB7 | 0xB8 | FUmweltTabelle_5138a | 0x6D |
| 0x5130 | 0x01 | 0x0B | - | - |
| 0x5131 | FUmweltTabelle_5131a | 0x76 | 0x8E | FUmweltTabelle_5131d |
| 0x5132 | FUmweltTabelle_5132a | 0x76 | 0x8E | FUmweltTabelle_5132d |
| 0x5133 | 0x8F | FUmweltTabelle_5133a | 0x76 | 0xE2 |
| 0x5134 | 0x97 | FUmweltTabelle_5134a | 0x76 | 0x9C |
| 0x5135 | 0xAE | - | - | - |
| 0x5139 | 0x6C | 0x6D | 0x4B | FUmweltTabelle_5139a |
| 0x5054 | 0x4B | 0x4C | FUmweltTabelle_5054a | FUmweltTabelle_5054d |
| 0x5055 | 0x4B | FUmweltTabelle_5055a | 0xE3 | FUmweltTabelle_5055d |
| 0x5056 | FUmweltTabelle_5056d | 0x6A | 0x70 | FUmweltTabelle_5056a |
| 0x5057 | 0x4B | 0x4C | FUmweltTabelle_5057a | FUmweltTabelle_5057d |
| 0x5058 | 0x72 | 0x73 | - | - |
| 0x5059 | FUmweltTabelle_5059d | 0x4B | 0x4C | FUmweltTabelle_5059a |
| 0x5060 | FUmweltTabelle_5060d | 0x6A | 0x6E | FUmweltTabelle_5060a |
| 0x5061 | FUmweltTabelle_5061a | 0xE9 | 0x4B | 0x4C |
| 0x5062 | FUmweltTabelle_5062a1 | 0xE9 | FUmweltTabelle_5062a | - |
| 0x5063 | 0x01 | 0x0B | - | - |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 205 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Spannungsversorgung UBatt | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x02 | Temperatur TCU | °C | high | signed int | - | 1 | 1 | 0 |
| 0x03 | Kilometerstand | km | high | unsigned int | - | 8 | 1 | 0 |
| 0x04 | Istgang Teilgetriebe 1 | - | high | signed char | - | 1 | 1 | 0 |
| 0x05 | Istgang Teilgetriebe 2 | - | high | signed char | - | 1 | 1 | 0 |
| 0x0A | Fahrzeuggeschwindigkeit | Km/h | high | signed int | - | 1 | 40 | 0 |
| 0x0B | Motordrehzahl | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x0C | Getriebeeingangsdrehzahl 1 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x0D | Getriebeeingangsdrehzahl 2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x0E | Getriebeausgangsdrehzahl | U/min | high | signed int | - | 1 | 2 | 0 |
| 0x0F | Schaltstangenposition GBX 1/3 | mm | high | signed int | - | 1 | 100 | 0 |
| 0x10 | Schaltstangenposition GBX 2/R | mm | high | signed int | - | 1 | 100 | 0 |
| 0x11 | Schaltstangenposition GBX 5/7 | mm | high | signed int | - | 1 | 100 | 0 |
| 0x12 | Schaltstangenposition GBX 6/4 | mm | high | signed int | - | 1 | 100 | 0 |
| 0x13 | Komb. Umw.-Größe GBX (gepuffert) | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x14 | Getriebeeingangsdrehzahl 1 GBX (gepuffert) | U/min | high | unsigned int | - | 1 | 1 | 0 |
| 0x15 | Getriebeeingangsdrehzahl 2 GBX (gepuffert) | U/min | high | unsigned int | - | 1 | 1 | 0 |
| 0x16 | Getriebeausgangsdrehzahl GBX (gepuffert) | U/min | high | signed int | - | 1 | 1 | 0 |
| 0x17 | Sollstrom PV3 GBX (gepuffert) | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x18 | Sollstrom PV4 GBX (gepuffert) | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x19 | Signal Positions Sensor Schalstange 6/4 | V | high | unsigned int | - | 5 | 1024 | 0 |
| 0x1A | Signal Positions Sensor Schalstange 5/7 | V | high | unsigned int | - | 5 | 1024 | 0 |
| 0x1B | Signal Positions Sensor Schalstange 2/R | V | high | unsigned int | - | 5 | 1024 | 0 |
| 0x1C | Signal Positions Sensor Schalstange 1/3 | V | high | unsigned int | - | 5 | 1024 | 0 |
| 0x1D | Fehlerstatus Schaltstange 1/3 (GBX) | 0-n | high | 0xFF | FUmweltTexte03 | 1 | 1 | 0 |
| 0x1E | Fehlerstatus Schaltstange 2/R (GBX) | 0-n | high | 0xFF | FUmweltTexte04 | 1 | 1 | 0 |
| 0x1F | Fehlerstatus Schaltstange 5/7 (GBX) | 0-n | high | 0xFF | FUmweltTexte05 | 1 | 1 | 0 |
| 0x20 | Fehlerstatus Schaltstange 6/4 (GBX) | 0-n | high | 0xFF | FUmweltTexte06 | 1 | 1 | 0 |
| 0x21 | Nachadaptionswert Gang 1 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x22 | Nachadaptionswert Gang 2 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x23 | Nachadaptionswert Gang 3 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x24 | Nachadaptionswert Gang 4 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x25 | Nachadaptionswert Gang 5 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x26 | Nachadaptionswert Gang 6 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x27 | Nachadaptionswert Gang 7 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x28 | Nachadaptionswert Gang R | mm | high | signed char | - | 1 | 40 | 0 |
| 0x29 | Radgeschwindigkeit vorne links, Rohwert | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x2A | Radgeschwindigkeit vorne rechts, Rohwert | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x2B | Radgeschwindigkeit hinten links, Rohwert | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x2C | Radgeschwindigkeit hinten rechts, Rohwert | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x2D | Aktiver Gang | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x2E | Klemmenstatus KL15 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x2F | Status Kupplung 1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x30 | Status Kupplung 2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x31 | Drehzahl Getriebeeingang 1, Rohwert | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x32 | Drehzahl Getriebeeingang 2, Rohwert | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x33 | Geschwindigkeit der nicht angetriebenen Achse | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x34 | Geschwindigkeit der angetriebenen Achse | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x35 | Temperatur TCU, redundant, Rohwert | °C | high | signed int | - | 1 | 1 | 0 |
| 0x36 | Temperatur TC1766 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x37 | Motortemperatur | °C | high | signed int | - | 1 | 1 | 0 |
| 0x38 | Status Temperatur TCU | 0-n | high | 0xFF | FUmweltTexte07 | 1 | 1 | 0 |
| 0x39 | Status Temperatur TCU, redundant | 0-n | high | 0xFF | FUmweltTexte08 | 1 | 1 | 0 |
| 0x3A | Spannung CH1 | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x3B | Spannung CH2 | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x3C | Spannung CH3 | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x3D | Vorspannung UH2_7V4 | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x3E | Sensorversorgungsspannung SV1 | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x3F | Sensorversorgungsspannung SV2 | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x40 | Interne 5V Sensorversorgungsspannung | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x41 | Fehlerkennung BusOff Betriebssystem | 0-n | high | 0xFF | FUmweltTexte12 | 1 | 1 | 0 |
| 0x42 | Temperatur TCU, Rohwert | °C | high | signed int | - | 1 | 1 | 0 |
| 0x43 | Quality-Information PV1 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x44 | Quality-Information PV2 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x45 | Quality-Information PV3 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x46 | Quality-Information PV4 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x47 | Quality-Information PV6 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x48 | Quality-Information PV7 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x49 | Quality-Information Drucksensor 1 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x4A | Quality-Information Drucksensor 2 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x4B | Gefilterter Ist-Druck Kupplung 1 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x4C | Gefilterter Ist-Druck Kupplung 2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x4D | Solldruck Kupplung 1 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x4E | Solldruck Kupplung 2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x4F | Detail. Status Kupplung 1 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x50 | Detail. Status Kupplung 2 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x51 | Antriebsdrehzahl, Rohwert | - | high | unsigned int | - | 1 | 4 | 0 |
| 0x52 | Nachadaptionswert Neutral SST 1/3 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x53 | Nachadaptionswert Neutral SST 2/R | mm | high | signed char | - | 1 | 40 | 0 |
| 0x54 | Nachadaptionswert Neutral SST 5/7 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x55 | Nachadaptionswert Neutral SST 6/4 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x56 | Fehlerflags Sicherheitskonzept 1 | 0-n | - | 0xFFFF | FUmweltTexte33 | 1 | 1 | 0 |
| 0x57 | Fehlerflags Sicherheitskonzept 2 | 0-n | - | 0xFFFF | FUmweltTexte34 | 1 | 1 | 0 |
| 0x58 | Spannungswert Schaltpaddles | V | high | unsigned int | - | 1 | 124 | 0 |
| 0x59 | Ist-Strom PV1 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5A | Ist-Strom PV2 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5B | Ist-Strom PV3 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5C | Ist-Strom PV4 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5D | Ist-Strom PV6 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5E | Ist-Strom PV7 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5F | Temperatur Abspritz-Öl | °C | high | signed int | - | 1 | 1 | 0 |
| 0x60 | Temperatur Sumpf-Öl | °C | high | signed int | - | 1 | 1 | 0 |
| 0x61 | RSC Status | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x62 | RSC Testgröße | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x63 | Predizierter Gang | - | high | signed char | - | 1 | 1 | 0 |
| 0x64 | Soll-Status SV3 | 0-n | high | 0xFF000000 | FUmweltTexte26 | 1 | 1 | 0 |
| 0x65 | Soll-Status CutOff 1 | 0-n | high | 0x00FF0000 | FUmweltTexte27 | 1 | 1 | 0 |
| 0x66 | Soll-Status CutOff 2 | 0-n | high | 0x0000FF00 | FUmweltTexte28 | 1 | 1 | 0 |
| 0x67 | Startdruck 1 für PLM | bar | high | signed int | - | 1 | 100 | 0 |
| 0x68 | Startdruck 2 für PLM | bar | high | signed int | - | 1 | 100 | 0 |
| 0x69 | Fehlerwert PS-Diagnose | 0-n | high | 0x000000FF | FUmweltTexte29 | 1 | 1 | 0 |
| 0x6A | Parksperrenzustand | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x6B | Fehlerart PSM-Diagnose | 0-n | high | 0x00FF | FUmweltTexte30 | 1 | 1 | 0 |
| 0x6C | Status Parksperrenmanager | 0-n | high | 0xFF | FUmweltTexte23 | 1 | 1 | 0 |
| 0x6D | Logischer Getriebezustand | 0-n | high | 0xFF | FUmweltTexte24 | 1 | 1 | 0 |
| 0x6E | Auto-P-supply | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x6F | Auto-P-switch | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x70 | PS-Sensor 1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x71 | PS-Sensor 2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x72 | Bed. Getriebewahltaster P1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x73 | Bed. Getriebewahltaster P2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x74 | Fehlerart Sicherheitszeit | 0-n | high | 0x00FF | FUmweltTexte25 | 1 | 1 | 0 |
| 0x76 | Ausgabe Ebene 2 | 0-n | high | 0xFFFF | FUmweltTexte13 | 1 | 1 | 0 |
| 0x77 | Motordrehzahl CAN | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x78 | Status Anhänger | 0-n | - | 0xFF | FUmweltTexte01 | 1 | 1 | 0 |
| 0x79 | Modelltemperatur K1 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x7A | Modelltemperatur K2 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x7B | Kühlmodus | 0-n | - | 0xFF | FUmweltTexte02 | 1 | 1 | 0 |
| 0x7C | Drucktoleranz K1 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x7D | Drucktoleranz K2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x7E | Status A | 0-n | high | 0xFF | FUmweltTexte41 | 1 | 1 | 0 |
| 0x7F | Status B | 0-n | high | 0xFF000000 | FUmweltTexte41 | 1 | 1 | 0 |
| 0x80 | Status C | 0-n | high | 0x00FF0000 | FUmweltTexte41 | 1 | 1 | 0 |
| 0x81 | Status D | 0-n | high | 0x0000FF00 | FUmweltTexte41 | 1 | 1 | 0 |
| 0x82 | Status E | 0-n | high | 0xFF | FUmweltTexte42 | 1 | 1 | 0 |
| 0x83 | Sollwertüberwachung Temic | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x84 | Ölfilm-Temperatur K1 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x85 | Ölfilm-Temperatur K2 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x86 | Statisches Motormoment | Nm | high | signed int | - | 1 | 8 | 0 |
| 0x87 | Abspritzsensor Rohwert | °C | high | signed int | - | 1 | 1 | 0 |
| 0x88 | Abweichung zu erw. Systemdruck | bar | high | signed int | - | 1 | 100 | 0 |
| 0x89 | Erw. Systemdruck | bar | high | signed int | - | 1 | 100 | 0 |
| 0x8A | Adaptionsstrom Offset | A | high | signed int | - | 1 | 1000 | 0 |
| 0x8B | Umgebungsluftdruck | bar | high | unsigned char | - | 2 | 1 | 299 |
| 0x8C | Querbeschleunigung | m/s^2 | high | signed int | - | 1 | 40 | 0 |
| 0x8D | Anzeige Getriebepos. Ebene2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x8E | Getriebesollposition aus Ebene1 | 0-n | high | 0xFF | FUmweltTexte14 | 1 | 1 | 0 |
| 0x8F | Druck PV1 Ebene2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x90 | Druck PV2 Ebene2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x91 | Parksperrenstatus Ebene2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x92 | Fahrerwunsch Ebene2 | 0-n | high | 0xFF00 | FUmweltTexte16 | 1 | 1 | 0 |
| 0x93 | Fahrzeuggeschwindigkeit Ebene2 | km | high | unsigned int | - | 1 | 5 | 0 |
| 0x94 | Eingelegte Gänge Ebene2 | 0-n | high | 0x00FF | FUmweltTexte18n | 1 | 1 | 0 |
| 0x95 | Aktive Schaltventile Ebene2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x96 | Drehrichtung Getriebeeingang Ebene2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x97 | Sollstrom PV1 Ebene2 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x98 | Sollstrom PV2 Ebene2 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x99 | Eingangsdrehzahl TG1 Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x9A | Eingangsdrehzahl TG2 Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x9B | Farhpedal Ebene2 | % | high | unsigned char | - | 100 | 255 | 0 |
| 0x9C | Status Motorschleppmomentenregelung MSR Ebene2 | 0-n | high | 0xFF | FUmweltTexte22 | 1 | 1 | 0 |
| 0x9D | Berechnete Eingangsdrehzahl TG1 über Sollgang Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x9E | Berechnete Eingangsdrehzahl TG2 über Sollgang Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x9F | Status Modus DKG bezüglich Motoranforderung aus Ebene 1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xA0 | Drehmoment Fahrerwunsch Ebene 2 | - | high | signed int | - | 1 | 2 | 0 |
| 0xA1 | Gefilterte Eingangsdrehzahl TG1 Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0xA2 | Gefilterte Eingangsdrehzahl TG2 Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0xA3 | Motordrehzahl Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0xA4 | Erster gemessener Kupplungsdruck bei der PV7-Druckpeak-Erkennung | bar | high | signed int | - | 1 | 100 | 0 |
| 0xA5 | Minimal gemessener Kupplungsdruck bei der PV7-Druckpeak-Erkennung | bar | high | signed int | - | 1 | 100 | 0 |
| 0xA6 | Maximal gemessener Kupplungsdruck bei der PV7-Druckpeak-Erkennung | bar | high | signed int | - | 1 | 100 | 0 |
| 0xA7 | Status HSD 0 | 0-n | high | 0xFF | FUmweltTexte09 | 1 | 1 | 0 |
| 0xA8 | Status HSD 1 | 0-n | high | 0xFF | FUmweltTexte10 | 1 | 1 | 0 |
| 0xA9 | Status HSD 2 | 0-n | high | 0xFF | FUmweltTexte11 | 1 | 1 | 0 |
| 0xAA | Status D2 | 0-n | high | 0x000000FF | FUmweltTexte41 | 1 | 1 | 0 |
| 0xAB | Akt. Kupplungsreferenzmoment | U/min/sek | high | signed int | - | 1 | 1 | 0 |
| 0xAC | Ist-Druck Kupplung 1 Rohwert | bar | high | signed int | - | 1 | 100 | 0 |
| 0xAD | Ist-Druck Kupplung 2 Rohwert | bar | high | signed int | - | 1 | 100 | 0 |
| 0xAE | Ebene2s Analyse | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xAF | Spannung Abspritzsensor | V | high | unsigned int | - | 1 | 310 | 0 |
| 0xB0 | Hauptzustand KP-Einlernroutine | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB1 | Unterzustand KP-Einlernroutine | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB2 | Ergebnis KP-Einlernroutine | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB3 | HS Diagnose Parksperrenmagnet | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB4 | Widerstandswert Parksperrenmagnet | Ohm | high | unsigned char | - | 1 | 1 | 0 |
| 0xB5 | HS-Dia-Startwert | Ohm | high | unsigned char | - | 1 | 1 | 0 |
| 0xB6 | Widerstands-Startwert | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB7 | Status Motor fehlerhaft | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB8 | CAN Notlauf Ursache | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB9 | Ebene2 Debug Flag | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xBA | Pfad Fahrerwunsch | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xBB | Ankündigung Motor Start Stop MSA | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xBC | Anforderung Motor Start MSA | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xBD | Status MSA Funktion | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xBE | Status MSA Motorstopp | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xE0 | Fehlerstatus Schaltstange 5/7 (GBX) | 0-n | high | 0xFF00 | FUmweltTexte31 | 1 | 1 | 0 |
| 0xE1 | Fehlerstatus Schaltstange 6/4 (GBX) | 0-n | high | 0x00FF | FUmweltTexte32 | 1 | 1 | 0 |
| 0xE2 | Eingelegte Gänge Ebene2 | 0-n | high | 0xFF | FUmweltTexte35n | 1 | 1 | 0 |
| 0xE3 | Fehlerwert PS-Diagnose | 0-n | high | 0xFF | FUmweltTexte36 | 1 | 1 | 0 |
| 0xE4 | Status Parksperrenmanager | 0-n | high | 0xFF | FUmweltTexte37 | 1 | 1 | 0 |
| 0xE5 | Logischer Getriebezustand | 0-n | high | 0x00FF | FUmweltTexte38 | 1 | 1 | 0 |
| 0xE6 | Soll-Status SV3 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xE7 | Soll-Status CutOff 1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xE8 | Soll-Status CutOff 2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xE9 | Fehlerart PSM-Diagnose | 0-n | high | 0xFF | FUmweltTexte40 | 1 | 1 | 0 |
| 0xF5 | Umweltdatum 1 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xF6 | Umweltdatum 2 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xF7 | Umweltdatum 3 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xF8 | Umweltdatum 4 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xF9 | Umweltdatum 5 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFA | Umweltdatum 6 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFB | Umweltdatum 7 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFC | Umweltdatum 8 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFD | Umweltdatum 9 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFE | Umweltdatum 10 | - | high | unsigned int | - | 1 | 1 | 0 |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 138 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x5A41 | 0x51 | 0x50 | 0x01 | 0x4A |
| 0x5A43 | 0x51 | 0x50 | 0x01 | 0x4A |
| 0x5A44 | 0x06 | 0x05 | 0xFFFF | 0xFFFF |
| 0x5A45 | 0x06 | 0x05 | 0xFFFF | 0xFFFF |
| 0x5A46 | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A47 | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A48 | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A4B | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A4C | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A52 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A53 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A54 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A55 | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A56 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A57 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A58 | 0xFFFF | 0xFFFF | 0xFFFF | 0x4E |
| 0x5A59 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A5A | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A5B | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5021 | 0x02 | 0xFFFF | 0x4B | 0xFFFF |
| 0x5022 | 0x02 | 0xFFFF | 0x4B | 0xFFFF |
| 0x5023 | 0x02 | 0xFFFF | 0x4B | 0xFFFF |
| 0x5024 | 0x02 | 0xFFFF | 0x4B | 0xFFFF |
| 0x5025 | 0x40 | 0x3F | 0xFFFF | 0xFFFF |
| 0x5026 | 0x40 | 0x3F | 0xFFFF | 0xFFFF |
| 0x5A42 | 0x43 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5031 | 0x43 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5027 | 0x40 | 0x3F | 0xFFFF | 0xFFFF |
| 0x5028 | 0x40 | 0x3F | 0xFFFF | 0xFFFF |
| 0x5029 | 0xFFFF | 0xFFFF | 0x04 | 0xFFFF |
| 0x5030 | 0xFFFF | 0xFFFF | 0x04 | 0xFFFF |
| 0x5137 | 0xFFFF | 0xFFFF | 0xFFFF | 0x48 |
| 0x5139 | 0xFFFF | 0x3D | 0xFFFF | 0xFFFF |
| 0x5A60 | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A61 | 0xFFFF | 0xFFFF | 0x54 | 0x07 |
| 0x5A62 | 0xFFFF | 0xFFFF | 0x54 | 0x07 |
| 0x5A63 | 0xFFFF | 0xFFFF | 0x54 | 0x07 |
| 0x5A64 | 0xFFFF | 0xFFFF | 0x54 | 0x07 |
| 0x5A65 | 0xFFFF | 0xFFFF | 0x09 | 0x08 |
| 0x5A66 | 0xFFFF | 0xFFFF | 0x09 | 0x08 |
| 0x5A67 | 0xFFFF | 0xFFFF | 0x09 | 0x08 |
| 0x5A68 | 0xFFFF | 0xFFFF | 0x09 | 0x08 |
| 0x5A69 | 0x0E | 0x0C | 0x0B | 0x0A |
| 0x5A6A | 0x0E | 0x0C | 0x0B | 0x0A |
| 0x5A6B | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A6C | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A6D | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A6E | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A70 | 0x11 | 0xFFFF | 0x10 | 0x0F |
| 0x5A71 | 0x11 | 0xFFFF | 0x10 | 0x0F |
| 0x5A72 | 0x14 | 0xFFFF | 0x13 | 0x12 |
| 0x5A73 | 0xFFFF | 0x17 | 0x16 | 0x15 |
| 0x5A74 | 0x18 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A75 | 0x18 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A76 | 0x18 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A80 | 0xFFFF | 0xFFFF | 0x1A | 0x19 |
| 0x5A81 | 0xFFFF | 0xFFFF | 0x1C | 0x1B |
| 0x5A82 | 0xFFFF | 0xFFFF | 0x1E | 0x1D |
| 0x5A83 | 0xFFFF | 0xFFFF | 0x20 | 0x1F |
| 0x5A84 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A85 | 0x22 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A86 | 0x23 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A87 | 0x24 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A88 | 0x24 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5072 | 0xFFFF | 0xFFFF | 0x25 | 0xFFFF |
| 0x5073 | 0xFFFF | 0xFFFF | 0x26 | 0xFFFF |
| 0x5074 | 0xFFFF | 0xFFFF | 0x27 | 0xFFFF |
| 0x5A8B | 0x28 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF07 | 0xFFFF | 0x29 | 0xFFFF | 0xFFFF |
| 0xCF10 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF11 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF12 | 0xFFFF | 0xFFFF | 0x2B | 0x2A |
| 0xCF13 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF14 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF15 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF16 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF17 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF18 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF19 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1A | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF1B | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1C | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1D | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1E | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1F | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF20 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF21 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF22 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF23 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF24 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF25 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF26 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF27 | 0xFFFF | 0xFFFF | 0x2B | 0x56 |
| 0xCF28 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF29 | 0x30 | 0x2C | 0x2B | 0x2A |
| 0xCF30 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF31 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF32 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF33 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF34 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF35 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF36 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF37 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF38 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF39 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3A | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3B | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3C | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3D | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3E | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3F | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF40 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF41 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF42 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5124 | 0xFFFF | 0xFFFF | 0xFFFF | 0x53 |
| 0x5A25 | 0x31 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5126 | 0xFFFF | 0x34 | 0x33 | 0x32 |
| 0x5127 | 0x35 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5128 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5129 | 0xFFFF | 0xFFFF | 0xFFFF | 0x4D |
| 0x5130 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5131 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5132 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5133 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5134 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5054 | 0xFFFF | 0x38 | 0x37 | 0x36 |
| 0x5135 | 0xFFFF | 0xFFFF | 0xFFFF | 0x47 |
| 0x5138 | 0xFFFF | 0xFFFF | 0xFFFF | 0x55 |
| 0x5055 | 0xFFFF | 0xFFFF | 0xFFFF | 0x39 |
| 0x5056 | 0xFFFF | 0xFFFF | 0xFFFF | 0x3A |
| 0x5057 | 0xFFFF | 0x52 | 0xFFFF | 0xFFFF |
| 0x5058 | 0xFFFF | 0xFFFF | 0x49 | 0x3C |
| 0x5059 | 0xFFFF | 0x3D | 0xFFFF | 0x3E |
| 0x5060 | 0xFFFF | 0xFFFF | 0x4C | 0x4D |
| 0x5061 | 0xFFFF | 0xFFFF | 0x45 | 0x44 |
| 0x5062 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5063 | 0xFFFF | 0xFFFF | 0xFFFF | 0x46 |
| 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 84 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Offset-Fehler |
| 0x02 | Kurzschluss |
| 0x03 | Kabelbruch |
| 0x04 | Befüllzeit |
| 0x05 | Druck zu niedrig |
| 0x06 | Druck zu hoch |
| 0x07 | Symptomspezifisch |
| 0x08 | Wert unter Schwelle |
| 0x09 | Wert über Schwelle |
| 0x0A | SST 1/3 |
| 0x0B | SST 2/R |
| 0x0C | SST 5/7 |
| 0x0E | SST 6/4 |
| 0x0F | Temperaturwert oberhalb zulässigem Genzwert |
| 0x10 | Temperaturwert unterhalb zulässigem Gernzwert |
| 0x11 | Sensorwert unplausibel |
| 0x12 | Versorgungsspannungswert oberhalb zulässigem Grenzwert |
| 0x13 | Versorgungsspannungswert unterhalb zulässigem Grenzwert |
| 0x14 | Spannungswert unplausibel |
| 0x15 | Spannungswert außerhalb Spezifikation |
| 0x16 | Kurzschluss Masse |
| 0x17 | Leitungsunterbrechung |
| 0x18 | Wert nicht plausibel |
| 0x19 | Vorspannung UH2_7V4 oberhalb Schwelle |
| 0x1A | Vorspannung UH2_7V4 unterhalb Schwelle |
| 0x1B | Interne 5V Spannung oberhalb Schwelle |
| 0x1C | Interne 5V Spannung unterhalb Schwelle |
| 0x1D | Sensorversorgung SV1 oberhalb Schwelle |
| 0x1E | Sensorversorgung SV1 unterhalb Schwelle |
| 0x1F | Sensorversorgung SV2 oberhalb Schwelle |
| 0x20 | Sensorversorgung SV2 unterhalb Schwelle |
| 0x22 | Core Eigendiagnose Fehler gekennzeichnet |
| 0x23 | Interner Temperatur TC 1766 unplausibel |
| 0x24 | Nicht flüchtig gespeicherte Einlerndaten unplausibel |
| 0x25 | Versorgungsspannung Ventilgruppe 1 unterhalb zulässigem Grenzwert |
| 0x26 | Versorgungsspannung Ventilgruppe 2 unterhalb zulässigem Grenzwert |
| 0x27 | Versorgungsspannung Ventilgruppe 3 unterhalb zulässigem Grenzwert |
| 0x28 | Temperaturwert unplausibel |
| 0x29 | Busoff |
| 0x2A | Timeout Botschaft PT-CAN |
| 0x2B | Fehlerhafter Alivecounter |
| 0x2C | Fehlerhafte Checksumme |
| 0x2E | Kommunikationsfehler LIN |
| 0x2F | Ungültig gekennzeichnete oder unplausible Nachricht |
| 0x30 | Ungültig gekennzeichnete Nachricht |
| 0x31 | Wählhebel Botschaften fehlerhaft |
| 0x32 | Energiesparmodus Fertigung aktiv |
| 0x33 | Energiesparmodus Transport aktiv |
| 0x34 | Energiesparmodus Werkstatt aktiv |
| 0x35 | Anforderung Restart Nachlaufzeit wird von CAS nicht quitiert |
| 0x36 | Überschritten beim Einlegen über PS_1 |
| 0x37 | Überschritten beim Einlegen über PS_2 |
| 0x38 | Überschritten beim Auslegen |
| 0x39 | Hängendes Absperrventil |
| 0x3A | Parksperrensensor |
| 0x3C | Beide Signale ungültig |
| 0x3D | Ungewollt Eingefallen |
| 0x3E | Ungewollt Ausgelegt |
| 0x3F | Untere Grenze verletzt |
| 0x40 | Obere Grenze verletzt |
| 0x41 | Ebene 2 Fehler |
| 0x42 | Elektrischer Defekt |
| 0x43 | Referenzmoment zu hoch |
| 0x44 | Parksperrenschieber 1 |
| 0x45 | Parksperrenschieber 2 |
| 0x46 | N-Haltephase über Tester deaktiviert |
| 0x47 | Ebene2s Fehler |
| 0x48 | Abbruch |
| 0x49 | Eins von beiden Signalen ungültig |
| 0x4A | Sensordrift oder Stuck-At |
| 0x4B | Fehler in Endstufen ASIC |
| 0x4C | PSM wird unter Umständen immer bestromt |
| 0x4D | PSM kann nicht mehr bestromt werden |
| 0x4E | Bereichsverletzung |
| 0x4F | Gradient unplausibel |
| 0x50 | Eingangsspannung zu niedrig |
| 0x51 | Eingangsspannung zu hoch |
| 0x52 | Überschritten beim Auslegen |
| 0x53 | Zusatzinfo |
| 0x54 | Quellenfehler |
| 0x55 | CAN-Notlauf |
| 0x56 | Timeout Botschaft Bedienung Getriebewahlschalter LIN |
| 0xFFFF | Fehlersymptom nicht definiert |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 139 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5021 | Schaltventil SV1: Überstrom |
| 0x5022 | Schaltventil SV2: Überstrom |
| 0x5023 | Schaltventil SV3: Überstrom |
| 0x5024 | Schaltventil SV4: Überstrom |
| 0x5025 | Kupplung 1: Adaption Kisspoint |
| 0x5026 | Kupplung 2: Adaption Kisspoint |
| 0x5027 | Systemdruck: falscher Druck |
| 0x5028 | PV6: Adaption |
| 0x5029 | Kupplung 1: Befüllzeit |
| 0x5030 | Kupplung 2: Befüllzeit |
| 0x5031 | Kupplung 2: Adaption Referenzmoment |
| 0x5054 | Parksperre: Überschreiten der Sicherheitszeit bei Betätigung |
| 0x5055 | Parksperre: hängendes Absperrventil |
| 0x5056 | Parksperrensensor |
| 0x5057 | Überschreiten der Sicherheitszeit beim Auslegen |
| 0x5058 | Parksperre:Betätigung Taster unplausibel |
| 0x5059 | Parksperre: Unerlaubte Bewegung |
| 0x5060 | Parksperre: elektrischer Fehler am Parksperrenmagnet |
| 0x5061 | Fehler Parksperrenschieber |
| 0x5062 | Fehler Parksperrenhaken |
| 0x5063 | N-Haltephase über Tester deaktiviert |
| 0x5072 | Versorgung der Ventilgruppe 1: fehlerhaft |
| 0x5073 | Versorgung der Ventilgruppe 2: fehlerhaft |
| 0x5074 | Versorgung der Ventilgruppe 3: fehlerhaft |
| 0x5124 | Ebene2 Diagnose |
| 0x5126 | Energiesparmodi: Modus aktiv |
| 0x5127 | Verlängerung Nachlaufzeit: fehlerhaft |
| 0x5128 | N-Haltephase seit 20min aktiv |
| 0x5129 | Elektr. Fehler am Parksperrenmagnet (Bestromung nicht möglich) |
| 0x5130 | Selbstbeschleuniger |
| 0x5131 | Ebene2 Schutzziele Verletzung 13, 14, 16, 19, Temic |
| 0x5132 | Ebene2 Schutzziele Verletzung 4a, 3_6 |
| 0x5133 | Ebene2 Schutzziele Verletzung 1, 10 |
| 0x5134 | Ebene2 Schutzziele Verletzung 9a, 9b |
| 0x5135 | Ebene2s Fehler |
| 0x5136 | PS Missuse |
| 0x5137 | Einlernen Kisspoint: abgebrochen |
| 0x5138 | Anforderung CAN-Notlauf |
| 0x5139 | Unerlaubtes Einfallen der Parksperre |
| 0x5A25 | Botschaften Wählhebel: fehlerhaft |
| 0x5A41 | Drucksensor Kupplung 1: Totalausfall |
| 0x5A42 | Kupplung 1: Adaption Referenzmoment |
| 0x5A43 | Drucksensor Kupplung 2: Totalausfall |
| 0x5A44 | Kupplung 1: falscher Druck |
| 0x5A45 | Kupplung 2: falscher Druck |
| 0x5A46 | Regelventil PV3: Kurzschluss/Wicklungsschluss |
| 0x5A47 | Regelventil PV4:  Kurzschluss/Wicklungsschluss |
| 0x5A48 | Regelventil PV6: Kurzschluss/Wicklungsschluss |
| 0x5A4B | Regelventil PV1: Kurzschluss/Wicklungsschluss |
| 0x5A4C | Regelventil PV2: Kurzschluss/Wicklungsschluss |
| 0x5A52 | Getriebeüberhitzung: Phase Gelb |
| 0x5A53 | Getriebeüberhitzung: Phase Rot |
| 0x5A54 | Getriebeüberhitzung: Phase Schwarz |
| 0x5A55 | Regelventil PV7: Kurzschluss/Wicklungsschluss |
| 0x5A56 | Kühlung: kein Kühlölstrom detektiert |
| 0x5A57 | Abspritzsensor: Wärmeeintrag |
| 0x5A58 | Abspritzsensor: elektrischer Defekt |
| 0x5A59 | Abschaltpfad 1: Cut-Off Ventil 1 schaltet nicht auf Tank |
| 0x5A5A | Abschaltpfad 2: Cut-Off Ventil 2 schaltet nicht auf Tank |
| 0x5A5B | Regelventil PV7: Ventil klemmt |
| 0x5A60 | Getriebe: Überdrehzahl |
| 0x5A61 | Schaltstange 1/3: Fehler |
| 0x5A62 | Schaltstange 2/R: Fehler |
| 0x5A63 | Schaltstange 6/4: Fehler |
| 0x5A64 | Schaltstange 5/7: Fehler |
| 0x5A65 | Sensor Schaltstange 6/4: Fehler |
| 0x5A66 | Sensor Schaltstange 5/7: Fehler |
| 0x5A67 | Sensor Schaltstange 2/R: Fehler |
| 0x5A68 | Sensor Schaltstange 1/3: Fehler |
| 0x5A69 | Nachadaptionswert Gang: Verschleißgrenze erreicht |
| 0x5A6A | Nachadaptionswert Neutrallage: Verschleißgrenze erreicht |
| 0x5A6B | Schaltstange 1/3: Fehler Gang |
| 0x5A6C | Schaltstange 2/R:Fehler Gang |
| 0x5A6D | Schaltstange 5/7: Fehler Gang |
| 0x5A6E | Schaltstange 6/4: Fehler Gang |
| 0x5A70 | Temperatursensor 1: fehlerhaft |
| 0x5A71 | Temperatursensor 2: fehlerhaft |
| 0x5A72 | Sensor Versorgungsspannung: fehlerhaft |
| 0x5A73 | Schaltwippen: fehlerhafter Spannungswert |
| 0x5A74 | Eingangsdrehzahlsensor Teilgetriebe 1: Wert unplausibel |
| 0x5A75 | Eingangsdrehzahlsensor Teilgetriebe 2: Wert unplausibel |
| 0x5A76 | Antriebsdrehzahlsensor: Wert unplausibel |
| 0x5A80 | Vorspannung UH2_7V4: fehlerhaft |
| 0x5A81 | Spannung intern 5V (VCC5 5V): fehlerhaft |
| 0x5A82 | Sensorversorgung SV1_ 5V: fehlerhaft |
| 0x5A83 | Sensorversorgung SV2_ 5V: fehlerhaft |
| 0x5A84 | Fehler mit gemultiplexten Umweltdaten |
| 0x5A85 | Core Eigendiagnose: Fehler |
| 0x5A86 | Temperaturwerts TC1766: fehlerhafte Plausibilisierung |
| 0x5A87 | Getriebesteuerung: interner Fehler (EEPROM Daten) |
| 0x5A88 | Getriebesteuerung: interner Fehler (EEPROM Daten, Block C-E) |
| 0x5A8B | Übertemperatur Getriebe |
| 0xCF07 | Kommunikationsfehler: PT-CAN |
| 0xCF10 | Botschaft (Anforderung Radmoment Antriebsstrang, PT-CAN) vom LDM |
| 0xCF11 | Botschaft (Außentemperatur /Relativzeit, PT-CAN) vom Kombiinstrument |
| 0xCF12 | Botschaft (Bedienung Getriebewahlschalter 2, PT-CAN) vom GWS |
| 0xCF13 | Botschaft (Drehmoment 1, PT-CAN) von der Motorsteuerung |
| 0xCF14 | Botschaft (Drehmoment 2, PT-CAN) von der Motorsteuerung |
| 0xCF15 | Botschaft (Drehmoment 3, PT-CAN) von der Motorsteuerung |
| 0xCF16 | Botschaft (Drehmomentanforderung ACC, PT-CAN) vom ACC |
| 0xCF17 | Botschaft (Drehmomentanforderung DSC, PT-CAN) von der DSC |
| 0xCF18 | Botschaft (Geschwindigkeit, PT-CAN) von der DSC |
| 0xCF19 | Botschaft (Kilometerstand /Reichweite, PT-CAN) vom Kombiinstrument |
| 0xCF1A | Botschaft (Klemmenstatus PT-CAN) vom CAS |
| 0xCF1B | Botschaft (Lenkradwinkel, PT-CAN) von der DSC |
| 0xCF1C | Botschaft (Motordaten, PT-CAN) vom der Motorsteuerung |
| 0xCF1D | Botschaft (Raddrücke, PT-CAN) von der RDC |
| 0xCF1E | Botschaft (Radgeschwindigkeit, PT-CAN) von der DSC |
| 0xCF1F | Botschaft (Radmoment Antriebsstrang 2, PT-CAN) von der Motorsteuerung |
| 0xCF20 | Botschaft (Radtoleranzabgleich, PT-CAN) von der DSC |
| 0xCF21 | Botschaft (Rohdaten Längsbeschleunigung, PT-CAN) von der DSC |
| 0xCF22 | Botschaft (Sitzbelegung/Gurtkontakte, PT-CAN) vom SSFA |
| 0xCF23 | Botschaft (Status Anhänger, PT-CAN) vom AHM |
| 0xCF24 | Botschaft (Status DSC, PT-CAN) von der DSC |
| 0xCF25 | Botschaft (Status Kontakt Handbremse, PT-CAN) vom JBBF |
| 0xCF26 | Botschaft (ZV und Klappenzustand, PT-CAN) vom CAS |
| 0xCF27 | Botschaft (Bedienung Getriebewahlschalter 2, LIN) vom GWS |
| 0xCF28 | Botschaft (OBD-Daten Motor, PT-CAN) von der Motorsteuerung |
| 0xCF29 | Botschaft (Status MSA, PT-CAN) von der Motorsteuerung |
| 0xCF30 | Signal von der DSC: Geschwindigkeit Rad VL |
| 0xCF31 | Signal von der DSC: Geschwindigkeit Rad VR |
| 0xCF32 | Signal von der DSC: Geschwindigkeit Rad HL |
| 0xCF33 | Signal von der DSC: Geschwindigkeit Rad HR |
| 0xCF34 | Signal von der Motorsteuerung: Drehmoment_Ist_DME |
| 0xCF35 | Signal von der Motorsteuerung: Bremslichtschalter |
| 0xCF36 | Signal von der Motorsteuerung: Winkel Fahrpedal |
| 0xCF37 | Signal von der DSC: Status_DSC |
| 0xCF38 | Signal von der Motorsteuerung: Drehzahl_Leerlauf_Soll |
| 0xCF39 | Signal vom CAS: Status Klemme 15 |
| 0xCF3A | Signal vom CAS: Status Schlüssel steckt |
| 0xCF3B | Signal vom  FRM: Status Türkontakt Fahrer |
| 0xCF3C | Signal vom SSFA: Klasse Gewicht Sitz |
| 0xCF3D | Signal vom GWS: Signal unplausibel |
| 0xCF3E | Signal von der Motorsteuerung: Drehzahl Motor |
| 0xCF3F | Signal vom CAS: Status Passive-Access Aktiv |
| 0xCF40 | Signal vom CAS: Status Schlüssel gültig |
| 0xCF41 | Signal vom SSFA: Schalter Gurtschloß FA |
| 0xCF42 | Signal von der DSC: Alle 4 Raddrehzahlen ungültig |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-hdetailstruktur"></a>
### HDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | nein |
| F_PCODE | ja |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-humweltmatrix"></a>
### HUMWELTMATRIX

Dimensions: 138 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x5A41 | 0x01 | 0x40 | 0x49 | 0x4B |
| 0x5A43 | 0x01 | 0x40 | 0x4A | 0x4C |
| 0x5A44 | 0x4B | 0x4D | 0x02 | FUmweltTabelle_5A44a |
| 0x5A45 | 0x4C | 0x4E | 0x02 | FUmweltTabelle_5A45a |
| 0x5A46 | 0x01 | FUmweltTabelle_5A46a | 0xA9 | 0x13 |
| 0x5A47 | 0x01 | FUmweltTabelle_5A47a | 0xA9 | 0x13 |
| 0x5A48 | 0x01 | 0x3B | FUmweltTabelle_5A48a | 0xA8 |
| 0x5A4B | FUmweltTabelle_5A4Ba | 0xA7 | 0x2F | 0x4F |
| 0x5A4C | FUmweltTabelle_5A4Ca | 0xA8 | 0x30 | 0x50 |
| 0x5A52 | 0x02 | FUmweltTabelle_5A52a | 0x78 | 0x7B |
| 0x5A53 | 0x02 | FUmweltTabelle_5A53a | 0x78 | 0x7B |
| 0x5A54 | 0x02 | FUmweltTabelle_5A54a | 0x78 | 0x7B |
| 0x5A55 | 0x01 | FUmweltTabelle_5A55a | 0xA8 | 0x7B |
| 0x5A56 | 0x84 | 0x85 | 0x2D | FUmweltTabelle_5A56a |
| 0x5A57 | 0x84 | 0x85 | 0x2D | FUmweltTabelle_5A57a |
| 0x5A58 | 0x01 | 0x02 | 0x3D | FUmweltTabelle_5A58a |
| 0x5A59 | 0x02 | 0x4B | 0x4D | 0x59 |
| 0x5A5A | 0x02 | 0x4C | 0x4E | 0x5A |
| 0x5A5B | 0x2D | 0x0A | 0x0B | FUmweltTabelle_5A5Ba |
| 0x5021 | FUmweltTabelle_5021a | 0xA7 | 0x2F | 0x4F |
| 0x5022 | FUmweltTabelle_5022a | 0xA8 | 0x30 | 0x50 |
| 0x5023 | FUmweltTabelle_5023a | 0x18 | 0x3C | 0xA9 |
| 0x5024 | FUmweltTabelle_5024a | 0x18 | 0x3C | 0xA9 |
| 0x5025 | 0x02 | 0x0B | 0x51 | - |
| 0x5026 | 0x02 | 0x0B | 0x51 | - |
| 0x5A42 | 0x51 | 0x79 | 0x4B | FUmweltTabelle_5A42a |
| 0x5031 | 0x51 | 0x7A | 0x4C | FUmweltTabelle_5031a |
| 0x5027 | 0x88 | 0x89 | 0x0B | FUmweltTabelle_5027a |
| 0x5028 | 0x02 | 0x0A | 0x0C | FUmweltTabelle_5028a |
| 0x5029 | 0x4B | 0x4D | 0x02 | FUmweltTabelle_5029a |
| 0x5030 | 0x4C | 0x4E | 0x02 | FUmweltTabelle_5030a |
| 0x5137 | FUmweltTabelle_5137a | 0x1D | 0x1E | FUmweltTabelle_5137d |
| 0x5A60 | 0x01 | 0x0A | FUmweltTabelle_5A60a | FUmweltTabelle_5A60d |
| 0x5A61 | 0x0F | 0x17 | FUmweltTabelle_5A61a | FUmweltTabelle_5A61d |
| 0x5A62 | 0x10 | 0x17 | FUmweltTabelle_5A62a | FUmweltTabelle_5A62d |
| 0x5A63 | 0x12 | 0x17 | FUmweltTabelle_5A63a | FUmweltTabelle_5A63d |
| 0x5A64 | 0x11 | FUmweltTabelle_5A64a | FUmweltTabelle_5A64d | - |
| 0x5A65 | 0x19 | 0x1A | FUmweltTabelle_5A65a | FUmweltTabelle_5A65d |
| 0x5A66 | 0x19 | 0x1A | FUmweltTabelle_5A66a | FUmweltTabelle_5A66d |
| 0x5A67 | 0x19 | 0x1A | FUmweltTabelle_5A67a | FUmweltTabelle_5A67d |
| 0x5A68 | 0x19 | 0x1A | FUmweltTabelle_5A68a | FUmweltTabelle_5A68d |
| 0x5A69 | 0x21 | 0x22 | 0x23 | FUmweltTabelle_5A69a |
| 0x5A6A | 0x52 | 0x53 | 0x54 | 0x55 |
| 0x5A6B | 0x0F | 0x17 | FUmweltTabelle_5A6Ba | FUmweltTabelle_5A6Bd |
| 0x5A6C | 0x10 | 0x17 | FUmweltTabelle_5A6Ca | FUmweltTabelle_5A6Cd |
| 0x5A6D | 0x11 | 0x17 | FUmweltTabelle_5A6Da | FUmweltTabelle_5A6Dd |
| 0x5A6E | 0x12 | 0x17 | FUmweltTabelle_5A6Ea | FUmweltTabelle_5A6Ed |
| 0x5A70 | 0x01 | 0x0B | FUmweltTabelle_5A70a | FUmweltTabelle_5A70d |
| 0x5A71 | 0x01 | 0x0B | FUmweltTabelle_5A71a | FUmweltTabelle_5A71d |
| 0x5A72 | FUmweltTabelle_5A72a | 0xA7 | 0xA8 | 0xA9 |
| 0x5A73 | 0x01 | 0x0B | 0x58 | - |
| 0x5A74 | 0x01 | 0x0B | 0x0C | FUmweltTabelle_5A74a |
| 0x5A75 | 0x01 | 0x0B | 0x0D | FUmweltTabelle_5A75a |
| 0x5A76 | 0x01 | 0x77 | 0x51 | FUmweltTabelle_5A76a |
| 0x5A80 | 0x01 | 0x0B | 0x3D | FUmweltTabelle_5A80a |
| 0x5A81 | 0x01 | 0x0B | 0x3D | FUmweltTabelle_5A81a |
| 0x5A82 | 0x01 | 0x0B | 0x3D | FUmweltTabelle_5A82a |
| 0x5A83 | 0x01 | 0x0B | 0x3D | FUmweltTabelle_5A83a |
| 0x5A84 | 0xF5 | 0xF6 | 0xF7 | FUmweltTabelle_5A84 |
| 0x5A85 | 0x01 | 0xA3 | 0x56 | 0x57 |
| 0x5A86 | 0x01 | FUmweltTabelle_5A86a | 0x38 | 0x39 |
| 0x5A87 | FUmweltTabelle_5A87a | 0x7E | FUmweltTabelle_5A87d | 0x82 |
| 0x5A88 | FUmweltTabelle_5A88a | 0x7E | FUmweltTabelle_5A88d | 0x82 |
| 0x5072 | 0x01 | 0x0B | 0x3A | FUmweltTabelle_5072a |
| 0x5073 | 0x01 | 0x0B | 0x3A | FUmweltTabelle_5073a |
| 0x5074 | 0x01 | 0x0B | 0x3A | FUmweltTabelle_5074a |
| 0x5A8B | 0x01 | FUmweltTabelle_5A8Ba | 0x38 | 0x39 |
| 0xCF07 | 0x01 | 0x0B | 0x41 | - |
| 0xCF10 | 0x01 | 0x0B | - | - |
| 0xCF11 | 0x01 | 0x0B | - | - |
| 0xCF12 | 0x01 | 0x0B | - | - |
| 0xCF13 | 0x01 | 0x0B | - | - |
| 0xCF14 | 0x01 | 0x0B | - | - |
| 0xCF15 | 0x01 | 0x0B | - | - |
| 0xCF16 | 0x01 | 0x0B | - | - |
| 0xCF17 | 0x01 | 0x0B | - | - |
| 0xCF18 | 0x01 | 0x0B | - | - |
| 0xCF19 | 0x01 | 0x0B | - | - |
| 0xCF1A | 0x01 | 0x0B | - | - |
| 0xCF1B | 0x01 | 0x0B | - | - |
| 0xCF1C | 0x01 | 0x0B | - | - |
| 0xCF1D | 0x01 | 0x0B | - | - |
| 0xCF1E | 0x01 | 0x0B | - | - |
| 0xCF1F | 0x01 | 0x0B | - | - |
| 0xCF20 | 0x01 | 0x0B | - | - |
| 0xCF21 | 0x01 | 0x0B | - | - |
| 0xCF22 | 0x01 | 0x0B | - | - |
| 0xCF23 | 0x01 | 0x0B | - | - |
| 0xCF24 | 0x01 | 0x0B | - | - |
| 0xCF25 | 0x01 | 0x0B | - | - |
| 0xCF26 | 0x01 | 0x0B | - | - |
| 0xCF27 | 0x01 | 0x0B | - | - |
| 0xCF28 | 0x01 | 0x0B | - | - |
| 0xCF29 | 0x01 | 0x0B | FUmweltTabelle_CF29a | - |
| 0xCF30 | 0x01 | 0x2D | 0x0C | FUmweltTabelle_CF30a |
| 0xCF31 | 0x01 | 0x2D | 0x0C | FUmweltTabelle_CF31a |
| 0xCF32 | 0x01 | 0x2D | 0x0C | FUmweltTabelle_CF32a |
| 0xCF33 | 0x01 | 0x2D | 0x0C | FUmweltTabelle_CF33a |
| 0xCF34 | 0x01 | 0x0B | - | - |
| 0xCF35 | 0x01 | 0x0B | - | - |
| 0xCF36 | 0x01 | 0x0B | - | - |
| 0xCF37 | 0x01 | 0x0B | - | - |
| 0xCF38 | 0x01 | 0x0B | - | - |
| 0xCF39 | 0x01 | 0x0B | - | - |
| 0xCF3A | 0x01 | 0x0B | - | - |
| 0xCF3B | 0x01 | 0x0B | - | - |
| 0xCF3C | 0x01 | 0x0B | - | - |
| 0xCF3D | 0x01 | 0x0B | - | - |
| 0xCF3E | 0x01 | 0x0B | 0x77 | FUmweltTabelle_CF3Ea |
| 0xCF3F | 0x01 | 0x0B | - | - |
| 0xCF40 | 0x01 | 0x0B | - | - |
| 0xCF41 | 0x01 | 0x0B | - | - |
| 0xCF42 | 0x01 | 0x0B | - | - |
| 0x5124 | 0xB9 | 0xBA | 0x76 | - |
| 0x5A25 | 0x01 | 0x0B | - | - |
| 0x5126 | 0x01 | 0x0B | - | - |
| 0x5127 | 0x01 | 0x0B | - | - |
| 0x5128 | 0x01 | 0x0B | - | - |
| 0x5129 | 0x6C | 0xE9 | 0x6A | FUmweltTabelle_5129a |
| 0x5136 | 0x01 | 0x0B | - | - |
| 0x5138 | 0xB7 | 0xB8 | FUmweltTabelle_5138a | 0x6D |
| 0x5130 | 0x01 | 0x0B | - | - |
| 0x5131 | FUmweltTabelle_5131a | 0x76 | 0x8E | FUmweltTabelle_5131d |
| 0x5132 | FUmweltTabelle_5132a | 0x76 | 0x8E | FUmweltTabelle_5132d |
| 0x5133 | 0x8F | FUmweltTabelle_5133a | 0x76 | 0xE2 |
| 0x5134 | 0x97 | FUmweltTabelle_5134a | 0x76 | 0x9C |
| 0x5135 | 0xAE | - | - | - |
| 0x5139 | 0x6C | 0x6D | 0x4B | FUmweltTabelle_5139a |
| 0x5054 | 0x4B | 0x4C | FUmweltTabelle_5054a | FUmweltTabelle_5054d |
| 0x5055 | 0x4B | FUmweltTabelle_5055a | 0xE3 | FUmweltTabelle_5055d |
| 0x5056 | FUmweltTabelle_5056d | 0x6A | 0x70 | FUmweltTabelle_5056a |
| 0x5057 | 0x4B | 0x4C | FUmweltTabelle_5057a | FUmweltTabelle_5057d |
| 0x5058 | 0x72 | 0x73 | - | - |
| 0x5059 | FUmweltTabelle_5059d | 0x4B | 0x4C | FUmweltTabelle_5059a |
| 0x5060 | FUmweltTabelle_5060d | 0x6A | 0x6E | FUmweltTabelle_5060a |
| 0x5061 | FUmweltTabelle_5061a | 0xE9 | 0x4B | 0x4C |
| 0x5062 | FUmweltTabelle_5062a1 | 0xE9 | FUmweltTabelle_5062a | - |
| 0x5063 | 0x01 | 0x0B | - | - |

<a id="table-humwelttexte"></a>
### HUMWELTTEXTE

Dimensions: 205 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Spannungsversorgung UBatt | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x02 | Temperatur TCU | °C | high | signed int | - | 1 | 1 | 0 |
| 0x03 | Kilometerstand | km | high | unsigned int | - | 8 | 1 | 0 |
| 0x04 | Istgang Teilgetriebe 1 | - | high | signed char | - | 1 | 1 | 0 |
| 0x05 | Istgang Teilgetriebe 2 | - | high | signed char | - | 1 | 1 | 0 |
| 0x0A | Fahrzeuggeschwindigkeit | Km/h | high | signed int | - | 1 | 40 | 0 |
| 0x0B | Motordrehzahl | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x0C | Getriebeeingangsdrehzahl 1 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x0D | Getriebeeingangsdrehzahl 2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x0E | Getriebeausgangsdrehzahl | U/min | high | signed int | - | 1 | 2 | 0 |
| 0x0F | Schaltstangenposition GBX 1/3 | mm | high | signed int | - | 1 | 100 | 0 |
| 0x10 | Schaltstangenposition GBX 2/R | mm | high | signed int | - | 1 | 100 | 0 |
| 0x11 | Schaltstangenposition GBX 5/7 | mm | high | signed int | - | 1 | 100 | 0 |
| 0x12 | Schaltstangenposition GBX 6/4 | mm | high | signed int | - | 1 | 100 | 0 |
| 0x13 | Komb. Umw.-Größe GBX (gepuffert) | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x14 | Getriebeeingangsdrehzahl 1 GBX (gepuffert) | U/min | high | unsigned int | - | 1 | 1 | 0 |
| 0x15 | Getriebeeingangsdrehzahl 2 GBX (gepuffert) | U/min | high | unsigned int | - | 1 | 1 | 0 |
| 0x16 | Getriebeausgangsdrehzahl GBX (gepuffert) | U/min | high | signed int | - | 1 | 1 | 0 |
| 0x17 | Sollstrom PV3 GBX (gepuffert) | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x18 | Sollstrom PV4 GBX (gepuffert) | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x19 | Signal Positions Sensor Schalstange 6/4 | V | high | unsigned int | - | 5 | 1024 | 0 |
| 0x1A | Signal Positions Sensor Schalstange 5/7 | V | high | unsigned int | - | 5 | 1024 | 0 |
| 0x1B | Signal Positions Sensor Schalstange 2/R | V | high | unsigned int | - | 5 | 1024 | 0 |
| 0x1C | Signal Positions Sensor Schalstange 1/3 | V | high | unsigned int | - | 5 | 1024 | 0 |
| 0x1D | Fehlerstatus Schaltstange 1/3 (GBX) | 0-n | high | 0xFF | FUmweltTexte03 | 1 | 1 | 0 |
| 0x1E | Fehlerstatus Schaltstange 2/R (GBX) | 0-n | high | 0xFF | FUmweltTexte04 | 1 | 1 | 0 |
| 0x1F | Fehlerstatus Schaltstange 5/7 (GBX) | 0-n | high | 0xFF | FUmweltTexte05 | 1 | 1 | 0 |
| 0x20 | Fehlerstatus Schaltstange 6/4 (GBX) | 0-n | high | 0xFF | FUmweltTexte06 | 1 | 1 | 0 |
| 0x21 | Nachadaptionswert Gang 1 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x22 | Nachadaptionswert Gang 2 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x23 | Nachadaptionswert Gang 3 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x24 | Nachadaptionswert Gang 4 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x25 | Nachadaptionswert Gang 5 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x26 | Nachadaptionswert Gang 6 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x27 | Nachadaptionswert Gang 7 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x28 | Nachadaptionswert Gang R | mm | high | signed char | - | 1 | 40 | 0 |
| 0x29 | Radgeschwindigkeit vorne links, Rohwert | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x2A | Radgeschwindigkeit vorne rechts, Rohwert | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x2B | Radgeschwindigkeit hinten links, Rohwert | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x2C | Radgeschwindigkeit hinten rechts, Rohwert | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x2D | Aktiver Gang | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x2E | Klemmenstatus KL15 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x2F | Status Kupplung 1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x30 | Status Kupplung 2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x31 | Drehzahl Getriebeeingang 1, Rohwert | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x32 | Drehzahl Getriebeeingang 2, Rohwert | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x33 | Geschwindigkeit der nicht angetriebenen Achse | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x34 | Geschwindigkeit der angetriebenen Achse | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x35 | Temperatur TCU, redundant, Rohwert | °C | high | signed int | - | 1 | 1 | 0 |
| 0x36 | Temperatur TC1766 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x37 | Motortemperatur | °C | high | signed int | - | 1 | 1 | 0 |
| 0x38 | Status Temperatur TCU | 0-n | high | 0xFF | FUmweltTexte07 | 1 | 1 | 0 |
| 0x39 | Status Temperatur TCU, redundant | 0-n | high | 0xFF | FUmweltTexte08 | 1 | 1 | 0 |
| 0x3A | Spannung CH1 | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x3B | Spannung CH2 | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x3C | Spannung CH3 | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x3D | Vorspannung UH2_7V4 | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x3E | Sensorversorgungsspannung SV1 | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x3F | Sensorversorgungsspannung SV2 | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x40 | Interne 5V Sensorversorgungsspannung | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x41 | Fehlerkennung BusOff Betriebssystem | 0-n | high | 0xFF | FUmweltTexte12 | 1 | 1 | 0 |
| 0x42 | Temperatur TCU, Rohwert | °C | high | signed int | - | 1 | 1 | 0 |
| 0x43 | Quality-Information PV1 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x44 | Quality-Information PV2 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x45 | Quality-Information PV3 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x46 | Quality-Information PV4 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x47 | Quality-Information PV6 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x48 | Quality-Information PV7 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x49 | Quality-Information Drucksensor 1 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x4A | Quality-Information Drucksensor 2 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x4B | Gefilterter Ist-Druck Kupplung 1 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x4C | Gefilterter Ist-Druck Kupplung 2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x4D | Solldruck Kupplung 1 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x4E | Solldruck Kupplung 2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x4F | Detail. Status Kupplung 1 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x50 | Detail. Status Kupplung 2 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x51 | Antriebsdrehzahl, Rohwert | - | high | unsigned int | - | 1 | 4 | 0 |
| 0x52 | Nachadaptionswert Neutral SST 1/3 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x53 | Nachadaptionswert Neutral SST 2/R | mm | high | signed char | - | 1 | 40 | 0 |
| 0x54 | Nachadaptionswert Neutral SST 5/7 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x55 | Nachadaptionswert Neutral SST 6/4 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x56 | Fehlerflags Sicherheitskonzept 1 | 0-n | - | 0xFFFF | FUmweltTexte33 | 1 | 1 | 0 |
| 0x57 | Fehlerflags Sicherheitskonzept 2 | 0-n | - | 0xFFFF | FUmweltTexte34 | 1 | 1 | 0 |
| 0x58 | Spannungswert Schaltpaddles | V | high | unsigned int | - | 1 | 124 | 0 |
| 0x59 | Ist-Strom PV1 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5A | Ist-Strom PV2 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5B | Ist-Strom PV3 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5C | Ist-Strom PV4 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5D | Ist-Strom PV6 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5E | Ist-Strom PV7 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5F | Temperatur Abspritz-Öl | °C | high | signed int | - | 1 | 1 | 0 |
| 0x60 | Temperatur Sumpf-Öl | °C | high | signed int | - | 1 | 1 | 0 |
| 0x61 | RSC Status | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x62 | RSC Testgröße | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x63 | Predizierter Gang | - | high | signed char | - | 1 | 1 | 0 |
| 0x64 | Soll-Status SV3 | 0-n | high | 0xFF000000 | FUmweltTexte26 | 1 | 1 | 0 |
| 0x65 | Soll-Status CutOff 1 | 0-n | high | 0x00FF0000 | FUmweltTexte27 | 1 | 1 | 0 |
| 0x66 | Soll-Status CutOff 2 | 0-n | high | 0x0000FF00 | FUmweltTexte28 | 1 | 1 | 0 |
| 0x67 | Startdruck 1 für PLM | bar | high | signed int | - | 1 | 100 | 0 |
| 0x68 | Startdruck 2 für PLM | bar | high | signed int | - | 1 | 100 | 0 |
| 0x69 | Fehlerwert PS-Diagnose | 0-n | high | 0x000000FF | FUmweltTexte29 | 1 | 1 | 0 |
| 0x6A | Parksperrenzustand | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x6B | Fehlerart PSM-Diagnose | 0-n | high | 0x00FF | FUmweltTexte30 | 1 | 1 | 0 |
| 0x6C | Status Parksperrenmanager | 0-n | high | 0xFF | FUmweltTexte23 | 1 | 1 | 0 |
| 0x6D | Logischer Getriebezustand | 0-n | high | 0xFF | FUmweltTexte24 | 1 | 1 | 0 |
| 0x6E | Auto-P-supply | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x6F | Auto-P-switch | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x70 | PS-Sensor 1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x71 | PS-Sensor 2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x72 | Bed. Getriebewahltaster P1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x73 | Bed. Getriebewahltaster P2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x74 | Fehlerart Sicherheitszeit | 0-n | high | 0x00FF | FUmweltTexte25 | 1 | 1 | 0 |
| 0x76 | Ausgabe Ebene 2 | 0-n | high | 0xFFFF | FUmweltTexte13 | 1 | 1 | 0 |
| 0x77 | Motordrehzahl CAN | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x78 | Status Anhänger | 0-n | - | 0xFF | FUmweltTexte01 | 1 | 1 | 0 |
| 0x79 | Modelltemperatur K1 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x7A | Modelltemperatur K2 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x7B | Kühlmodus | 0-n | - | 0xFF | FUmweltTexte02 | 1 | 1 | 0 |
| 0x7C | Drucktoleranz K1 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x7D | Drucktoleranz K2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x7E | Status A | 0-n | high | 0xFF | FUmweltTexte41 | 1 | 1 | 0 |
| 0x7F | Status B | 0-n | high | 0xFF000000 | FUmweltTexte41 | 1 | 1 | 0 |
| 0x80 | Status C | 0-n | high | 0x00FF0000 | FUmweltTexte41 | 1 | 1 | 0 |
| 0x81 | Status D | 0-n | high | 0x0000FF00 | FUmweltTexte41 | 1 | 1 | 0 |
| 0x82 | Status E | 0-n | high | 0xFF | FUmweltTexte42 | 1 | 1 | 0 |
| 0x83 | Sollwertüberwachung Temic | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x84 | Ölfilm-Temperatur K1 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x85 | Ölfilm-Temperatur K2 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x86 | Statisches Motormoment | Nm | high | signed int | - | 1 | 8 | 0 |
| 0x87 | Abspritzsensor Rohwert | °C | high | signed int | - | 1 | 1 | 0 |
| 0x88 | Abweichung zu erw. Systemdruck | bar | high | signed int | - | 1 | 100 | 0 |
| 0x89 | Erw. Systemdruck | bar | high | signed int | - | 1 | 100 | 0 |
| 0x8A | Adaptionsstrom Offset | A | high | signed int | - | 1 | 1000 | 0 |
| 0x8B | Umgebungsluftdruck | bar | high | unsigned char | - | 2 | 1 | 299 |
| 0x8C | Querbeschleunigung | m/s^2 | high | signed int | - | 1 | 40 | 0 |
| 0x8D | Anzeige Getriebepos. Ebene2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x8E | Getriebesollposition aus Ebene1 | 0-n | high | 0xFF | FUmweltTexte14 | 1 | 1 | 0 |
| 0x8F | Druck PV1 Ebene2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x90 | Druck PV2 Ebene2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x91 | Parksperrenstatus Ebene2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x92 | Fahrerwunsch Ebene2 | 0-n | high | 0xFF00 | FUmweltTexte16 | 1 | 1 | 0 |
| 0x93 | Fahrzeuggeschwindigkeit Ebene2 | km | high | unsigned int | - | 1 | 5 | 0 |
| 0x94 | Eingelegte Gänge Ebene2 | 0-n | high | 0x00FF | FUmweltTexte18n | 1 | 1 | 0 |
| 0x95 | Aktive Schaltventile Ebene2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x96 | Drehrichtung Getriebeeingang Ebene2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x97 | Sollstrom PV1 Ebene2 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x98 | Sollstrom PV2 Ebene2 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x99 | Eingangsdrehzahl TG1 Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x9A | Eingangsdrehzahl TG2 Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x9B | Farhpedal Ebene2 | % | high | unsigned char | - | 100 | 255 | 0 |
| 0x9C | Status Motorschleppmomentenregelung MSR Ebene2 | 0-n | high | 0xFF | FUmweltTexte22 | 1 | 1 | 0 |
| 0x9D | Berechnete Eingangsdrehzahl TG1 über Sollgang Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x9E | Berechnete Eingangsdrehzahl TG2 über Sollgang Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x9F | Status Modus DKG bezüglich Motoranforderung aus Ebene 1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xA0 | Drehmoment Fahrerwunsch Ebene 2 | - | high | signed int | - | 1 | 2 | 0 |
| 0xA1 | Gefilterte Eingangsdrehzahl TG1 Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0xA2 | Gefilterte Eingangsdrehzahl TG2 Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0xA3 | Motordrehzahl Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0xA4 | Erster gemessener Kupplungsdruck bei der PV7-Druckpeak-Erkennung | bar | high | signed int | - | 1 | 100 | 0 |
| 0xA5 | Minimal gemessener Kupplungsdruck bei der PV7-Druckpeak-Erkennung | bar | high | signed int | - | 1 | 100 | 0 |
| 0xA6 | Maximal gemessener Kupplungsdruck bei der PV7-Druckpeak-Erkennung | bar | high | signed int | - | 1 | 100 | 0 |
| 0xA7 | Status HSD 0 | 0-n | high | 0xFF | FUmweltTexte09 | 1 | 1 | 0 |
| 0xA8 | Status HSD 1 | 0-n | high | 0xFF | FUmweltTexte10 | 1 | 1 | 0 |
| 0xA9 | Status HSD 2 | 0-n | high | 0xFF | FUmweltTexte11 | 1 | 1 | 0 |
| 0xAA | Status D2 | 0-n | high | 0x000000FF | FUmweltTexte41 | 1 | 1 | 0 |
| 0xAB | Akt. Kupplungsreferenzmoment | U/min/sek | high | signed int | - | 1 | 1 | 0 |
| 0xAC | Ist-Druck Kupplung 1 Rohwert | bar | high | signed int | - | 1 | 100 | 0 |
| 0xAD | Ist-Druck Kupplung 2 Rohwert | bar | high | signed int | - | 1 | 100 | 0 |
| 0xAE | Ebene2s Analyse | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xAF | Spannung Abspritzsensor | V | high | unsigned int | - | 1 | 310 | 0 |
| 0xB0 | Hauptzustand KP-Einlernroutine | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB1 | Unterzustand KP-Einlernroutine | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB2 | Ergebnis KP-Einlernroutine | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB3 | HS Diagnose Parksperrenmagnet | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB4 | Widerstandswert Parksperrenmagnet | Ohm | high | unsigned char | - | 1 | 1 | 0 |
| 0xB5 | HS-Dia-Startwert | Ohm | high | unsigned char | - | 1 | 1 | 0 |
| 0xB6 | Widerstands-Startwert | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB7 | Status Motor fehlerhaft | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB8 | CAN Notlauf Ursache | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB9 | Ebene2 Debug Flag | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xBA | Pfad Fahrerwunsch | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xBB | Ankündigung Motor Start Stop MSA | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xBC | Anforderung Motor Start MSA | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xBD | Status MSA Funktion | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xBE | Status MSA Motorstopp | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xE0 | Fehlerstatus Schaltstange 5/7 (GBX) | 0-n | high | 0xFF00 | FUmweltTexte31 | 1 | 1 | 0 |
| 0xE1 | Fehlerstatus Schaltstange 6/4 (GBX) | 0-n | high | 0x00FF | FUmweltTexte32 | 1 | 1 | 0 |
| 0xE2 | Eingelegte Gänge Ebene2 | 0-n | high | 0xFF | FUmweltTexte35n | 1 | 1 | 0 |
| 0xE3 | Fehlerwert PS-Diagnose | 0-n | high | 0xFF | FUmweltTexte36 | 1 | 1 | 0 |
| 0xE4 | Status Parksperrenmanager | 0-n | high | 0xFF | FUmweltTexte37 | 1 | 1 | 0 |
| 0xE5 | Logischer Getriebezustand | 0-n | high | 0x00FF | FUmweltTexte38 | 1 | 1 | 0 |
| 0xE6 | Soll-Status SV3 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xE7 | Soll-Status CutOff 1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xE8 | Soll-Status CutOff 2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xE9 | Fehlerart PSM-Diagnose | 0-n | high | 0xFF | FUmweltTexte40 | 1 | 1 | 0 |
| 0xF5 | Umweltdatum 1 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xF6 | Umweltdatum 2 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xF7 | Umweltdatum 3 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xF8 | Umweltdatum 4 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xF9 | Umweltdatum 5 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFA | Umweltdatum 6 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFB | Umweltdatum 7 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFC | Umweltdatum 8 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFD | Umweltdatum 9 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFE | Umweltdatum 10 | - | high | unsigned int | - | 1 | 1 | 0 |

<a id="table-harttyp"></a>
### HARTTYP

Dimensions: 138 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x5A41 | 0x51 | 0x50 | 0x01 | 0x4A |
| 0x5A43 | 0x51 | 0x50 | 0x01 | 0x4A |
| 0x5A44 | 0x06 | 0x05 | 0xFFFF | 0xFFFF |
| 0x5A45 | 0x06 | 0x05 | 0xFFFF | 0xFFFF |
| 0x5A46 | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A47 | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A48 | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A4B | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A4C | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A52 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A53 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A54 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A55 | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A56 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A57 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A58 | 0xFFFF | 0xFFFF | 0xFFFF | 0x4E |
| 0x5A59 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A5A | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A5B | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5021 | 0x02 | 0xFFFF | 0x4B | 0xFFFF |
| 0x5022 | 0x02 | 0xFFFF | 0x4B | 0xFFFF |
| 0x5023 | 0x02 | 0xFFFF | 0x4B | 0xFFFF |
| 0x5024 | 0x02 | 0xFFFF | 0x4B | 0xFFFF |
| 0x5025 | 0x40 | 0x3F | 0xFFFF | 0xFFFF |
| 0x5026 | 0x40 | 0x3F | 0xFFFF | 0xFFFF |
| 0x5A42 | 0x43 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5031 | 0x43 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5027 | 0x40 | 0x3F | 0xFFFF | 0xFFFF |
| 0x5028 | 0x40 | 0x3F | 0xFFFF | 0xFFFF |
| 0x5029 | 0xFFFF | 0xFFFF | 0x04 | 0xFFFF |
| 0x5030 | 0xFFFF | 0xFFFF | 0x04 | 0xFFFF |
| 0x5137 | 0xFFFF | 0xFFFF | 0xFFFF | 0x48 |
| 0x5139 | 0xFFFF | 0x3D | 0xFFFF | 0xFFFF |
| 0x5A60 | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A61 | 0xFFFF | 0xFFFF | 0x54 | 0x07 |
| 0x5A62 | 0xFFFF | 0xFFFF | 0x54 | 0x07 |
| 0x5A63 | 0xFFFF | 0xFFFF | 0x54 | 0x07 |
| 0x5A64 | 0xFFFF | 0xFFFF | 0x54 | 0x07 |
| 0x5A65 | 0xFFFF | 0xFFFF | 0x09 | 0x08 |
| 0x5A66 | 0xFFFF | 0xFFFF | 0x09 | 0x08 |
| 0x5A67 | 0xFFFF | 0xFFFF | 0x09 | 0x08 |
| 0x5A68 | 0xFFFF | 0xFFFF | 0x09 | 0x08 |
| 0x5A69 | 0x0E | 0x0C | 0x0B | 0x0A |
| 0x5A6A | 0x0E | 0x0C | 0x0B | 0x0A |
| 0x5A6B | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A6C | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A6D | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A6E | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A70 | 0x11 | 0xFFFF | 0x10 | 0x0F |
| 0x5A71 | 0x11 | 0xFFFF | 0x10 | 0x0F |
| 0x5A72 | 0x14 | 0xFFFF | 0x13 | 0x12 |
| 0x5A73 | 0xFFFF | 0x17 | 0x16 | 0x15 |
| 0x5A74 | 0x18 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A75 | 0x18 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A76 | 0x18 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A80 | 0xFFFF | 0xFFFF | 0x1A | 0x19 |
| 0x5A81 | 0xFFFF | 0xFFFF | 0x1C | 0x1B |
| 0x5A82 | 0xFFFF | 0xFFFF | 0x1E | 0x1D |
| 0x5A83 | 0xFFFF | 0xFFFF | 0x20 | 0x1F |
| 0x5A84 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A85 | 0x22 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A86 | 0x23 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A87 | 0x24 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A88 | 0x24 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5072 | 0xFFFF | 0xFFFF | 0x25 | 0xFFFF |
| 0x5073 | 0xFFFF | 0xFFFF | 0x26 | 0xFFFF |
| 0x5074 | 0xFFFF | 0xFFFF | 0x27 | 0xFFFF |
| 0x5A8B | 0x28 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF07 | 0xFFFF | 0x29 | 0xFFFF | 0xFFFF |
| 0xCF10 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF11 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF12 | 0xFFFF | 0xFFFF | 0x2B | 0x2A |
| 0xCF13 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF14 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF15 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF16 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF17 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF18 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF19 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1A | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF1B | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1C | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1D | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1E | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1F | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF20 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF21 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF22 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF23 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF24 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF25 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF26 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF27 | 0xFFFF | 0xFFFF | 0x2B | 0x56 |
| 0xCF28 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF29 | 0x30 | 0x2C | 0x2B | 0x2A |
| 0xCF30 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF31 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF32 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF33 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF34 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF35 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF36 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF37 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF38 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF39 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3A | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3B | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3C | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3D | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3E | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3F | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF40 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF41 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF42 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5124 | 0xFFFF | 0xFFFF | 0xFFFF | 0x53 |
| 0x5A25 | 0x31 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5126 | 0xFFFF | 0x34 | 0x33 | 0x32 |
| 0x5127 | 0x35 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5128 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5129 | 0xFFFF | 0xFFFF | 0xFFFF | 0x4D |
| 0x5130 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5131 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5132 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5133 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5134 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5054 | 0xFFFF | 0x38 | 0x37 | 0x36 |
| 0x5135 | 0xFFFF | 0xFFFF | 0xFFFF | 0x47 |
| 0x5138 | 0xFFFF | 0xFFFF | 0xFFFF | 0x55 |
| 0x5055 | 0xFFFF | 0xFFFF | 0xFFFF | 0x39 |
| 0x5056 | 0xFFFF | 0xFFFF | 0xFFFF | 0x3A |
| 0x5057 | 0xFFFF | 0x52 | 0xFFFF | 0xFFFF |
| 0x5058 | 0xFFFF | 0xFFFF | 0x49 | 0x3C |
| 0x5059 | 0xFFFF | 0x3D | 0xFFFF | 0x3E |
| 0x5060 | 0xFFFF | 0xFFFF | 0x4C | 0x4D |
| 0x5061 | 0xFFFF | 0xFFFF | 0x45 | 0x44 |
| 0x5062 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5063 | 0xFFFF | 0xFFFF | 0xFFFF | 0x46 |
| 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |

<a id="table-harttexteindividuell"></a>
### HARTTEXTEINDIVIDUELL

Dimensions: 84 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Offset-Fehler |
| 0x02 | Kurzschluss |
| 0x03 | Kabelbruch |
| 0x04 | Befüllzeit |
| 0x05 | Druck zu niedrig |
| 0x06 | Druck zu hoch |
| 0x07 | Symptomspezifisch |
| 0x08 | Wert unter Schwelle |
| 0x09 | Wert über Schwelle |
| 0x0A | SST 1/3 |
| 0x0B | SST 2/R |
| 0x0C | SST 5/7 |
| 0x0E | SST 6/4 |
| 0x0F | Temperaturwert oberhalb zulässigem Genzwert |
| 0x10 | Temperaturwert unterhalb zulässigem Gernzwert |
| 0x11 | Sensorwert unplausibel |
| 0x12 | Versorgungsspannungswert oberhalb zulässigem Grenzwert |
| 0x13 | Versorgungsspannungswert unterhalb zulässigem Grenzwert |
| 0x14 | Spannungswert unplausibel |
| 0x15 | Spannungswert außerhalb Spezifikation |
| 0x16 | Kurzschluss Masse |
| 0x17 | Leitungsunterbrechung |
| 0x18 | Wert nicht plausibel |
| 0x19 | Vorspannung UH2_7V4 oberhalb Schwelle |
| 0x1A | Vorspannung UH2_7V4 unterhalb Schwelle |
| 0x1B | Interne 5V Spannung oberhalb Schwelle |
| 0x1C | Interne 5V Spannung unterhalb Schwelle |
| 0x1D | Sensorversorgung SV1 oberhalb Schwelle |
| 0x1E | Sensorversorgung SV1 unterhalb Schwelle |
| 0x1F | Sensorversorgung SV2 oberhalb Schwelle |
| 0x20 | Sensorversorgung SV2 unterhalb Schwelle |
| 0x22 | Core Eigendiagnose Fehler gekennzeichnet |
| 0x23 | Interner Temperatur TC 1766 unplausibel |
| 0x24 | Nicht flüchtig gespeicherte Einlerndaten unplausibel |
| 0x25 | Versorgungsspannung Ventilgruppe 1 unterhalb zulässigem Grenzwert |
| 0x26 | Versorgungsspannung Ventilgruppe 2 unterhalb zulässigem Grenzwert |
| 0x27 | Versorgungsspannung Ventilgruppe 3 unterhalb zulässigem Grenzwert |
| 0x28 | Temperaturwert unplausibel |
| 0x29 | Busoff |
| 0x2A | Timeout Botschaft PT-CAN |
| 0x2B | Fehlerhafter Alivecounter |
| 0x2C | Fehlerhafte Checksumme |
| 0x2E | Kommunikationsfehler LIN |
| 0x2F | Ungültig gekennzeichnete oder unplausible Nachricht |
| 0x30 | Ungültig gekennzeichnete Nachricht |
| 0x31 | Wählhebel Botschaften fehlerhaft |
| 0x32 | Energiesparmodus Fertigung aktiv |
| 0x33 | Energiesparmodus Transport aktiv |
| 0x34 | Energiesparmodus Werkstatt aktiv |
| 0x35 | Anforderung Restart Nachlaufzeit wird von CAS nicht quitiert |
| 0x36 | Überschritten beim Einlegen über PS_1 |
| 0x37 | Überschritten beim Einlegen über PS_2 |
| 0x38 | Überschritten beim Auslegen |
| 0x39 | Hängendes Absperrventil |
| 0x3A | Parksperrensensor |
| 0x3C | Beide Signale ungültig |
| 0x3D | Ungewollt Eingefallen |
| 0x3E | Ungewollt Ausgelegt |
| 0x3F | Untere Grenze verletzt |
| 0x40 | Obere Grenze verletzt |
| 0x41 | Ebene 2 Fehler |
| 0x42 | Elektrischer Defekt |
| 0x43 | Referenzmoment zu hoch |
| 0x44 | Parksperrenschieber 1 |
| 0x45 | Parksperrenschieber 2 |
| 0x46 | N-Haltephase über Tester deaktiviert |
| 0x47 | Ebene2s Fehler |
| 0x48 | Abbruch |
| 0x49 | Eins von beiden Signalen ungültig |
| 0x4A | Sensordrift oder Stuck-At |
| 0x4B | Fehler in Endstufen ASIC |
| 0x4C | PSM wird unter Umständen immer bestromt |
| 0x4D | PSM kann nicht mehr bestromt werden |
| 0x4E | Bereichsverletzung |
| 0x4F | Gradient unplausibel |
| 0x50 | Eingangsspannung zu niedrig |
| 0x51 | Eingangsspannung zu hoch |
| 0x52 | Überschritten beim Auslegen |
| 0x53 | Zusatzinfo |
| 0x54 | Quellenfehler |
| 0x55 | CAN-Notlauf |
| 0x56 | Timeout Botschaft Bedienung Getriebewahlschalter LIN |
| 0xFFFF | Fehlersymptom nicht definiert |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 139 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5021 | Schaltventil SV1: Überstrom |
| 0x5022 | Schaltventil SV2: Überstrom |
| 0x5023 | Schaltventil SV3: Überstrom |
| 0x5024 | Schaltventil SV4: Überstrom |
| 0x5025 | Kupplung 1: Adaption Kisspoint |
| 0x5026 | Kupplung 2: Adaption Kisspoint |
| 0x5027 | Systemdruck: falscher Druck |
| 0x5028 | PV6: Adaption |
| 0x5029 | Kupplung 1: Befüllzeit |
| 0x5030 | Kupplung 2: Befüllzeit |
| 0x5031 | Kupplung 2: Adaption Referenzmoment |
| 0x5054 | Parksperre: Überschreiten der Sicherheitszeit bei Betätigung |
| 0x5055 | Parksperre: hängendes Absperrventil |
| 0x5056 | Parksperrensensor |
| 0x5057 | Überschreiten der Sicherheitszeit beim Auslegen |
| 0x5058 | Parksperre:Betätigung Taster unplausibel |
| 0x5059 | Parksperre: Unerlaubte Bewegung |
| 0x5060 | Parksperre: elektrischer Fehler am Parksperrenmagnet |
| 0x5061 | Fehler Parksperrenschieber |
| 0x5062 | Fehler Parksperrenhaken |
| 0x5063 | N-Haltephase über Tester deaktiviert |
| 0x5072 | Versorgung der Ventilgruppe 1: fehlerhaft |
| 0x5073 | Versorgung der Ventilgruppe 2: fehlerhaft |
| 0x5074 | Versorgung der Ventilgruppe 3: fehlerhaft |
| 0x5124 | Ebene2 Diagnose |
| 0x5126 | Energiesparmodi: Modus aktiv |
| 0x5127 | Verlängerung Nachlaufzeit: fehlerhaft |
| 0x5128 | N-Haltephase seit 20min aktiv |
| 0x5129 | Elektr. Fehler am Parksperrenmagnet (Bestromung nicht möglich) |
| 0x5130 | Selbstbeschleuniger |
| 0x5131 | Ebene2 Schutzziele Verletzung 13, 14, 16, 19, Temic |
| 0x5132 | Ebene2 Schutzziele Verletzung 4a, 3_6 |
| 0x5133 | Ebene2 Schutzziele Verletzung 1, 10 |
| 0x5134 | Ebene2 Schutzziele Verletzung 9a, 9b |
| 0x5135 | Ebene2s Fehler |
| 0x5136 | PS Missuse |
| 0x5137 | Einlernen Kisspoint: abgebrochen |
| 0x5138 | Anforderung CAN-Notlauf |
| 0x5139 | Unerlaubtes Einfallen der Parksperre |
| 0x5A25 | Botschaften Wählhebel: fehlerhaft |
| 0x5A41 | Drucksensor Kupplung 1: Totalausfall |
| 0x5A42 | Kupplung 1: Adaption Referenzmoment |
| 0x5A43 | Drucksensor Kupplung 2: Totalausfall |
| 0x5A44 | Kupplung 1: falscher Druck |
| 0x5A45 | Kupplung 2: falscher Druck |
| 0x5A46 | Regelventil PV3: Kurzschluss/Wicklungsschluss |
| 0x5A47 | Regelventil PV4:  Kurzschluss/Wicklungsschluss |
| 0x5A48 | Regelventil PV6: Kurzschluss/Wicklungsschluss |
| 0x5A4B | Regelventil PV1: Kurzschluss/Wicklungsschluss |
| 0x5A4C | Regelventil PV2: Kurzschluss/Wicklungsschluss |
| 0x5A52 | Getriebeüberhitzung: Phase Gelb |
| 0x5A53 | Getriebeüberhitzung: Phase Rot |
| 0x5A54 | Getriebeüberhitzung: Phase Schwarz |
| 0x5A55 | Regelventil PV7: Kurzschluss/Wicklungsschluss |
| 0x5A56 | Kühlung: kein Kühlölstrom detektiert |
| 0x5A57 | Abspritzsensor: Wärmeeintrag |
| 0x5A58 | Abspritzsensor: elektrischer Defekt |
| 0x5A59 | Abschaltpfad 1: Cut-Off Ventil 1 schaltet nicht auf Tank |
| 0x5A5A | Abschaltpfad 2: Cut-Off Ventil 2 schaltet nicht auf Tank |
| 0x5A5B | Regelventil PV7: Ventil klemmt |
| 0x5A60 | Getriebe: Überdrehzahl |
| 0x5A61 | Schaltstange 1/3: Fehler |
| 0x5A62 | Schaltstange 2/R: Fehler |
| 0x5A63 | Schaltstange 6/4: Fehler |
| 0x5A64 | Schaltstange 5/7: Fehler |
| 0x5A65 | Sensor Schaltstange 6/4: Fehler |
| 0x5A66 | Sensor Schaltstange 5/7: Fehler |
| 0x5A67 | Sensor Schaltstange 2/R: Fehler |
| 0x5A68 | Sensor Schaltstange 1/3: Fehler |
| 0x5A69 | Nachadaptionswert Gang: Verschleißgrenze erreicht |
| 0x5A6A | Nachadaptionswert Neutrallage: Verschleißgrenze erreicht |
| 0x5A6B | Schaltstange 1/3: Fehler Gang |
| 0x5A6C | Schaltstange 2/R:Fehler Gang |
| 0x5A6D | Schaltstange 5/7: Fehler Gang |
| 0x5A6E | Schaltstange 6/4: Fehler Gang |
| 0x5A70 | Temperatursensor 1: fehlerhaft |
| 0x5A71 | Temperatursensor 2: fehlerhaft |
| 0x5A72 | Sensor Versorgungsspannung: fehlerhaft |
| 0x5A73 | Schaltwippen: fehlerhafter Spannungswert |
| 0x5A74 | Eingangsdrehzahlsensor Teilgetriebe 1: Wert unplausibel |
| 0x5A75 | Eingangsdrehzahlsensor Teilgetriebe 2: Wert unplausibel |
| 0x5A76 | Antriebsdrehzahlsensor: Wert unplausibel |
| 0x5A80 | Vorspannung UH2_7V4: fehlerhaft |
| 0x5A81 | Spannung intern 5V (VCC5 5V): fehlerhaft |
| 0x5A82 | Sensorversorgung SV1_ 5V: fehlerhaft |
| 0x5A83 | Sensorversorgung SV2_ 5V: fehlerhaft |
| 0x5A84 | Fehler mit gemultiplexten Umweltdaten |
| 0x5A85 | Core Eigendiagnose: Fehler |
| 0x5A86 | Temperaturwerts TC1766: fehlerhafte Plausibilisierung |
| 0x5A87 | Getriebesteuerung: interner Fehler (EEPROM Daten) |
| 0x5A88 | Getriebesteuerung: interner Fehler (EEPROM Daten, Block C-E) |
| 0x5A8B | Übertemperatur Getriebe |
| 0xCF07 | Kommunikationsfehler: PT-CAN |
| 0xCF10 | Botschaft (Anforderung Radmoment Antriebsstrang, PT-CAN) vom LDM |
| 0xCF11 | Botschaft (Außentemperatur /Relativzeit, PT-CAN) vom Kombiinstrument |
| 0xCF12 | Botschaft (Bedienung Getriebewahlschalter 2, PT-CAN) vom GWS |
| 0xCF13 | Botschaft (Drehmoment 1, PT-CAN) von der Motorsteuerung |
| 0xCF14 | Botschaft (Drehmoment 2, PT-CAN) von der Motorsteuerung |
| 0xCF15 | Botschaft (Drehmoment 3, PT-CAN) von der Motorsteuerung |
| 0xCF16 | Botschaft (Drehmomentanforderung ACC, PT-CAN) vom ACC |
| 0xCF17 | Botschaft (Drehmomentanforderung DSC, PT-CAN) von der DSC |
| 0xCF18 | Botschaft (Geschwindigkeit, PT-CAN) von der DSC |
| 0xCF19 | Botschaft (Kilometerstand /Reichweite, PT-CAN) vom Kombiinstrument |
| 0xCF1A | Botschaft (Klemmenstatus PT-CAN) vom CAS |
| 0xCF1B | Botschaft (Lenkradwinkel, PT-CAN) von der DSC |
| 0xCF1C | Botschaft (Motordaten, PT-CAN) vom der Motorsteuerung |
| 0xCF1D | Botschaft (Raddrücke, PT-CAN) von der RDC |
| 0xCF1E | Botschaft (Radgeschwindigkeit, PT-CAN) von der DSC |
| 0xCF1F | Botschaft (Radmoment Antriebsstrang 2, PT-CAN) von der Motorsteuerung |
| 0xCF20 | Botschaft (Radtoleranzabgleich, PT-CAN) von der DSC |
| 0xCF21 | Botschaft (Rohdaten Längsbeschleunigung, PT-CAN) von der DSC |
| 0xCF22 | Botschaft (Sitzbelegung/Gurtkontakte, PT-CAN) vom SSFA |
| 0xCF23 | Botschaft (Status Anhänger, PT-CAN) vom AHM |
| 0xCF24 | Botschaft (Status DSC, PT-CAN) von der DSC |
| 0xCF25 | Botschaft (Status Kontakt Handbremse, PT-CAN) vom JBBF |
| 0xCF26 | Botschaft (ZV und Klappenzustand, PT-CAN) vom CAS |
| 0xCF27 | Botschaft (Bedienung Getriebewahlschalter 2, LIN) vom GWS |
| 0xCF28 | Botschaft (OBD-Daten Motor, PT-CAN) von der Motorsteuerung |
| 0xCF29 | Botschaft (Status MSA, PT-CAN) von der Motorsteuerung |
| 0xCF30 | Signal von der DSC: Geschwindigkeit Rad VL |
| 0xCF31 | Signal von der DSC: Geschwindigkeit Rad VR |
| 0xCF32 | Signal von der DSC: Geschwindigkeit Rad HL |
| 0xCF33 | Signal von der DSC: Geschwindigkeit Rad HR |
| 0xCF34 | Signal von der Motorsteuerung: Drehmoment_Ist_DME |
| 0xCF35 | Signal von der Motorsteuerung: Bremslichtschalter |
| 0xCF36 | Signal von der Motorsteuerung: Winkel Fahrpedal |
| 0xCF37 | Signal von der DSC: Status_DSC |
| 0xCF38 | Signal von der Motorsteuerung: Drehzahl_Leerlauf_Soll |
| 0xCF39 | Signal vom CAS: Status Klemme 15 |
| 0xCF3A | Signal vom CAS: Status Schlüssel steckt |
| 0xCF3B | Signal vom  FRM: Status Türkontakt Fahrer |
| 0xCF3C | Signal vom SSFA: Klasse Gewicht Sitz |
| 0xCF3D | Signal vom GWS: Signal unplausibel |
| 0xCF3E | Signal von der Motorsteuerung: Drehzahl Motor |
| 0xCF3F | Signal vom CAS: Status Passive-Access Aktiv |
| 0xCF40 | Signal vom CAS: Status Schlüssel gültig |
| 0xCF41 | Signal vom SSFA: Schalter Gurtschloß FA |
| 0xCF42 | Signal von der DSC: Alle 4 Raddrehzahlen ungültig |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | nein |
| F_PCODE | ja |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 138 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x5A41 | 0x01 | 0x40 | 0x49 | 0x4B |
| 0x5A43 | 0x01 | 0x40 | 0x4A | 0x4C |
| 0x5A44 | 0x4B | 0x4D | 0x02 | FUmweltTabelle_5A44a |
| 0x5A45 | 0x4C | 0x4E | 0x02 | FUmweltTabelle_5A45a |
| 0x5A46 | 0x01 | FUmweltTabelle_5A46a | 0xA9 | 0x13 |
| 0x5A47 | 0x01 | FUmweltTabelle_5A47a | 0xA9 | 0x13 |
| 0x5A48 | 0x01 | 0x3B | FUmweltTabelle_5A48a | 0xA8 |
| 0x5A4B | FUmweltTabelle_5A4Ba | 0xA7 | 0x2F | 0x4F |
| 0x5A4C | FUmweltTabelle_5A4Ca | 0xA8 | 0x30 | 0x50 |
| 0x5A52 | 0x02 | FUmweltTabelle_5A52a | 0x78 | 0x7B |
| 0x5A53 | 0x02 | FUmweltTabelle_5A53a | 0x78 | 0x7B |
| 0x5A54 | 0x02 | FUmweltTabelle_5A54a | 0x78 | 0x7B |
| 0x5A55 | 0x01 | FUmweltTabelle_5A55a | 0xA8 | 0x7B |
| 0x5A56 | 0x84 | 0x85 | 0x2D | FUmweltTabelle_5A56a |
| 0x5A57 | 0x84 | 0x85 | 0x2D | FUmweltTabelle_5A57a |
| 0x5A58 | 0x01 | 0x02 | 0x3D | FUmweltTabelle_5A58a |
| 0x5A59 | 0x02 | 0x4B | 0x4D | 0x59 |
| 0x5A5A | 0x02 | 0x4C | 0x4E | 0x5A |
| 0x5A5B | 0x2D | 0x0A | 0x0B | FUmweltTabelle_5A5Ba |
| 0x5021 | FUmweltTabelle_5021a | 0xA7 | 0x2F | 0x4F |
| 0x5022 | FUmweltTabelle_5022a | 0xA8 | 0x30 | 0x50 |
| 0x5023 | FUmweltTabelle_5023a | 0x18 | 0x3C | 0xA9 |
| 0x5024 | FUmweltTabelle_5024a | 0x18 | 0x3C | 0xA9 |
| 0x5025 | 0x02 | 0x0B | 0x51 | - |
| 0x5026 | 0x02 | 0x0B | 0x51 | - |
| 0x5A42 | 0x51 | 0x79 | 0x4B | FUmweltTabelle_5A42a |
| 0x5031 | 0x51 | 0x7A | 0x4C | FUmweltTabelle_5031a |
| 0x5027 | 0x88 | 0x89 | 0x0B | FUmweltTabelle_5027a |
| 0x5028 | 0x02 | 0x0A | 0x0C | FUmweltTabelle_5028a |
| 0x5029 | 0x4B | 0x4D | 0x02 | FUmweltTabelle_5029a |
| 0x5030 | 0x4C | 0x4E | 0x02 | FUmweltTabelle_5030a |
| 0x5137 | FUmweltTabelle_5137a | 0x1D | 0x1E | FUmweltTabelle_5137d |
| 0x5A60 | 0x01 | 0x0A | FUmweltTabelle_5A60a | FUmweltTabelle_5A60d |
| 0x5A61 | 0x0F | 0x17 | FUmweltTabelle_5A61a | FUmweltTabelle_5A61d |
| 0x5A62 | 0x10 | 0x17 | FUmweltTabelle_5A62a | FUmweltTabelle_5A62d |
| 0x5A63 | 0x12 | 0x17 | FUmweltTabelle_5A63a | FUmweltTabelle_5A63d |
| 0x5A64 | 0x11 | FUmweltTabelle_5A64a | FUmweltTabelle_5A64d | - |
| 0x5A65 | 0x19 | 0x1A | FUmweltTabelle_5A65a | FUmweltTabelle_5A65d |
| 0x5A66 | 0x19 | 0x1A | FUmweltTabelle_5A66a | FUmweltTabelle_5A66d |
| 0x5A67 | 0x19 | 0x1A | FUmweltTabelle_5A67a | FUmweltTabelle_5A67d |
| 0x5A68 | 0x19 | 0x1A | FUmweltTabelle_5A68a | FUmweltTabelle_5A68d |
| 0x5A69 | 0x21 | 0x22 | 0x23 | FUmweltTabelle_5A69a |
| 0x5A6A | 0x52 | 0x53 | 0x54 | 0x55 |
| 0x5A6B | 0x0F | 0x17 | FUmweltTabelle_5A6Ba | FUmweltTabelle_5A6Bd |
| 0x5A6C | 0x10 | 0x17 | FUmweltTabelle_5A6Ca | FUmweltTabelle_5A6Cd |
| 0x5A6D | 0x11 | 0x17 | FUmweltTabelle_5A6Da | FUmweltTabelle_5A6Dd |
| 0x5A6E | 0x12 | 0x17 | FUmweltTabelle_5A6Ea | FUmweltTabelle_5A6Ed |
| 0x5A70 | 0x01 | 0x0B | FUmweltTabelle_5A70a | FUmweltTabelle_5A70d |
| 0x5A71 | 0x01 | 0x0B | FUmweltTabelle_5A71a | FUmweltTabelle_5A71d |
| 0x5A72 | FUmweltTabelle_5A72a | 0xA7 | 0xA8 | 0xA9 |
| 0x5A73 | 0x01 | 0x0B | 0x58 | - |
| 0x5A74 | 0x01 | 0x0B | 0x0C | FUmweltTabelle_5A74a |
| 0x5A75 | 0x01 | 0x0B | 0x0D | FUmweltTabelle_5A75a |
| 0x5A76 | 0x01 | 0x77 | 0x51 | FUmweltTabelle_5A76a |
| 0x5A80 | 0x01 | 0x0B | 0x3D | FUmweltTabelle_5A80a |
| 0x5A81 | 0x01 | 0x0B | 0x3D | FUmweltTabelle_5A81a |
| 0x5A82 | 0x01 | 0x0B | 0x3D | FUmweltTabelle_5A82a |
| 0x5A83 | 0x01 | 0x0B | 0x3D | FUmweltTabelle_5A83a |
| 0x5A84 | 0xF5 | 0xF6 | 0xF7 | FUmweltTabelle_5A84 |
| 0x5A85 | 0x01 | 0xA3 | 0x56 | 0x57 |
| 0x5A86 | 0x01 | FUmweltTabelle_5A86a | 0x38 | 0x39 |
| 0x5A87 | FUmweltTabelle_5A87a | 0x7E | FUmweltTabelle_5A87d | 0x82 |
| 0x5A88 | FUmweltTabelle_5A88a | 0x7E | FUmweltTabelle_5A88d | 0x82 |
| 0x5072 | 0x01 | 0x0B | 0x3A | FUmweltTabelle_5072a |
| 0x5073 | 0x01 | 0x0B | 0x3A | FUmweltTabelle_5073a |
| 0x5074 | 0x01 | 0x0B | 0x3A | FUmweltTabelle_5074a |
| 0x5A8B | 0x01 | FUmweltTabelle_5A8Ba | 0x38 | 0x39 |
| 0xCF07 | 0x01 | 0x0B | 0x41 | - |
| 0xCF10 | 0x01 | 0x0B | - | - |
| 0xCF11 | 0x01 | 0x0B | - | - |
| 0xCF12 | 0x01 | 0x0B | - | - |
| 0xCF13 | 0x01 | 0x0B | - | - |
| 0xCF14 | 0x01 | 0x0B | - | - |
| 0xCF15 | 0x01 | 0x0B | - | - |
| 0xCF16 | 0x01 | 0x0B | - | - |
| 0xCF17 | 0x01 | 0x0B | - | - |
| 0xCF18 | 0x01 | 0x0B | - | - |
| 0xCF19 | 0x01 | 0x0B | - | - |
| 0xCF1A | 0x01 | 0x0B | - | - |
| 0xCF1B | 0x01 | 0x0B | - | - |
| 0xCF1C | 0x01 | 0x0B | - | - |
| 0xCF1D | 0x01 | 0x0B | - | - |
| 0xCF1E | 0x01 | 0x0B | - | - |
| 0xCF1F | 0x01 | 0x0B | - | - |
| 0xCF20 | 0x01 | 0x0B | - | - |
| 0xCF21 | 0x01 | 0x0B | - | - |
| 0xCF22 | 0x01 | 0x0B | - | - |
| 0xCF23 | 0x01 | 0x0B | - | - |
| 0xCF24 | 0x01 | 0x0B | - | - |
| 0xCF25 | 0x01 | 0x0B | - | - |
| 0xCF26 | 0x01 | 0x0B | - | - |
| 0xCF27 | 0x01 | 0x0B | - | - |
| 0xCF28 | 0x01 | 0x0B | - | - |
| 0xCF29 | 0x01 | 0x0B | FUmweltTabelle_CF29a | - |
| 0xCF30 | 0x01 | 0x2D | 0x0C | FUmweltTabelle_CF30a |
| 0xCF31 | 0x01 | 0x2D | 0x0C | FUmweltTabelle_CF31a |
| 0xCF32 | 0x01 | 0x2D | 0x0C | FUmweltTabelle_CF32a |
| 0xCF33 | 0x01 | 0x2D | 0x0C | FUmweltTabelle_CF33a |
| 0xCF34 | 0x01 | 0x0B | - | - |
| 0xCF35 | 0x01 | 0x0B | - | - |
| 0xCF36 | 0x01 | 0x0B | - | - |
| 0xCF37 | 0x01 | 0x0B | - | - |
| 0xCF38 | 0x01 | 0x0B | - | - |
| 0xCF39 | 0x01 | 0x0B | - | - |
| 0xCF3A | 0x01 | 0x0B | - | - |
| 0xCF3B | 0x01 | 0x0B | - | - |
| 0xCF3C | 0x01 | 0x0B | - | - |
| 0xCF3D | 0x01 | 0x0B | - | - |
| 0xCF3E | 0x01 | 0x0B | 0x77 | FUmweltTabelle_CF3Ea |
| 0xCF3F | 0x01 | 0x0B | - | - |
| 0xCF40 | 0x01 | 0x0B | - | - |
| 0xCF41 | 0x01 | 0x0B | - | - |
| 0xCF42 | 0x01 | 0x0B | - | - |
| 0x5124 | 0xB9 | 0xBA | 0x76 | - |
| 0x5A25 | 0x01 | 0x0B | - | - |
| 0x5126 | 0x01 | 0x0B | - | - |
| 0x5127 | 0x01 | 0x0B | - | - |
| 0x5128 | 0x01 | 0x0B | - | - |
| 0x5129 | 0x6C | 0xE9 | 0x6A | FUmweltTabelle_5129a |
| 0x5136 | 0x01 | 0x0B | - | - |
| 0x5138 | 0xB7 | 0xB8 | FUmweltTabelle_5138a | 0x6D |
| 0x5130 | 0x01 | 0x0B | - | - |
| 0x5131 | FUmweltTabelle_5131a | 0x76 | 0x8E | FUmweltTabelle_5131d |
| 0x5132 | FUmweltTabelle_5132a | 0x76 | 0x8E | FUmweltTabelle_5132d |
| 0x5133 | 0x8F | FUmweltTabelle_5133a | 0x76 | 0xE2 |
| 0x5134 | 0x97 | FUmweltTabelle_5134a | 0x76 | 0x9C |
| 0x5135 | 0xAE | - | - | - |
| 0x5139 | 0x6C | 0x6D | 0x4B | FUmweltTabelle_5139a |
| 0x5054 | 0x4B | 0x4C | FUmweltTabelle_5054a | FUmweltTabelle_5054d |
| 0x5055 | 0x4B | FUmweltTabelle_5055a | 0xE3 | FUmweltTabelle_5055d |
| 0x5056 | FUmweltTabelle_5056d | 0x6A | 0x70 | FUmweltTabelle_5056a |
| 0x5057 | 0x4B | 0x4C | FUmweltTabelle_5057a | FUmweltTabelle_5057d |
| 0x5058 | 0x72 | 0x73 | - | - |
| 0x5059 | FUmweltTabelle_5059d | 0x4B | 0x4C | FUmweltTabelle_5059a |
| 0x5060 | FUmweltTabelle_5060d | 0x6A | 0x6E | FUmweltTabelle_5060a |
| 0x5061 | FUmweltTabelle_5061a | 0xE9 | 0x4B | 0x4C |
| 0x5062 | FUmweltTabelle_5062a1 | 0xE9 | FUmweltTabelle_5062a | - |
| 0x5063 | 0x01 | 0x0B | - | - |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 205 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x01 | Spannungsversorgung UBatt | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x02 | Temperatur TCU | °C | high | signed int | - | 1 | 1 | 0 |
| 0x03 | Kilometerstand | km | high | unsigned int | - | 8 | 1 | 0 |
| 0x04 | Istgang Teilgetriebe 1 | - | high | signed char | - | 1 | 1 | 0 |
| 0x05 | Istgang Teilgetriebe 2 | - | high | signed char | - | 1 | 1 | 0 |
| 0x0A | Fahrzeuggeschwindigkeit | Km/h | high | signed int | - | 1 | 40 | 0 |
| 0x0B | Motordrehzahl | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x0C | Getriebeeingangsdrehzahl 1 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x0D | Getriebeeingangsdrehzahl 2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x0E | Getriebeausgangsdrehzahl | U/min | high | signed int | - | 1 | 2 | 0 |
| 0x0F | Schaltstangenposition GBX 1/3 | mm | high | signed int | - | 1 | 100 | 0 |
| 0x10 | Schaltstangenposition GBX 2/R | mm | high | signed int | - | 1 | 100 | 0 |
| 0x11 | Schaltstangenposition GBX 5/7 | mm | high | signed int | - | 1 | 100 | 0 |
| 0x12 | Schaltstangenposition GBX 6/4 | mm | high | signed int | - | 1 | 100 | 0 |
| 0x13 | Komb. Umw.-Größe GBX (gepuffert) | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x14 | Getriebeeingangsdrehzahl 1 GBX (gepuffert) | U/min | high | unsigned int | - | 1 | 1 | 0 |
| 0x15 | Getriebeeingangsdrehzahl 2 GBX (gepuffert) | U/min | high | unsigned int | - | 1 | 1 | 0 |
| 0x16 | Getriebeausgangsdrehzahl GBX (gepuffert) | U/min | high | signed int | - | 1 | 1 | 0 |
| 0x17 | Sollstrom PV3 GBX (gepuffert) | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x18 | Sollstrom PV4 GBX (gepuffert) | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x19 | Signal Positions Sensor Schalstange 6/4 | V | high | unsigned int | - | 5 | 1024 | 0 |
| 0x1A | Signal Positions Sensor Schalstange 5/7 | V | high | unsigned int | - | 5 | 1024 | 0 |
| 0x1B | Signal Positions Sensor Schalstange 2/R | V | high | unsigned int | - | 5 | 1024 | 0 |
| 0x1C | Signal Positions Sensor Schalstange 1/3 | V | high | unsigned int | - | 5 | 1024 | 0 |
| 0x1D | Fehlerstatus Schaltstange 1/3 (GBX) | 0-n | high | 0xFF | FUmweltTexte03 | 1 | 1 | 0 |
| 0x1E | Fehlerstatus Schaltstange 2/R (GBX) | 0-n | high | 0xFF | FUmweltTexte04 | 1 | 1 | 0 |
| 0x1F | Fehlerstatus Schaltstange 5/7 (GBX) | 0-n | high | 0xFF | FUmweltTexte05 | 1 | 1 | 0 |
| 0x20 | Fehlerstatus Schaltstange 6/4 (GBX) | 0-n | high | 0xFF | FUmweltTexte06 | 1 | 1 | 0 |
| 0x21 | Nachadaptionswert Gang 1 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x22 | Nachadaptionswert Gang 2 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x23 | Nachadaptionswert Gang 3 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x24 | Nachadaptionswert Gang 4 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x25 | Nachadaptionswert Gang 5 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x26 | Nachadaptionswert Gang 6 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x27 | Nachadaptionswert Gang 7 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x28 | Nachadaptionswert Gang R | mm | high | signed char | - | 1 | 40 | 0 |
| 0x29 | Radgeschwindigkeit vorne links, Rohwert | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x2A | Radgeschwindigkeit vorne rechts, Rohwert | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x2B | Radgeschwindigkeit hinten links, Rohwert | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x2C | Radgeschwindigkeit hinten rechts, Rohwert | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x2D | Aktiver Gang | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x2E | Klemmenstatus KL15 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x2F | Status Kupplung 1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x30 | Status Kupplung 2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x31 | Drehzahl Getriebeeingang 1, Rohwert | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x32 | Drehzahl Getriebeeingang 2, Rohwert | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x33 | Geschwindigkeit der nicht angetriebenen Achse | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x34 | Geschwindigkeit der angetriebenen Achse | Km/h | high | signed int | - | 1 | 16 | 0 |
| 0x35 | Temperatur TCU, redundant, Rohwert | °C | high | signed int | - | 1 | 1 | 0 |
| 0x36 | Temperatur TC1766 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x37 | Motortemperatur | °C | high | signed int | - | 1 | 1 | 0 |
| 0x38 | Status Temperatur TCU | 0-n | high | 0xFF | FUmweltTexte07 | 1 | 1 | 0 |
| 0x39 | Status Temperatur TCU, redundant | 0-n | high | 0xFF | FUmweltTexte08 | 1 | 1 | 0 |
| 0x3A | Spannung CH1 | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x3B | Spannung CH2 | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x3C | Spannung CH3 | V | high | unsigned int | - | 1 | 1000 | 0 |
| 0x3D | Vorspannung UH2_7V4 | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x3E | Sensorversorgungsspannung SV1 | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x3F | Sensorversorgungsspannung SV2 | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x40 | Interne 5V Sensorversorgungsspannung | V | high | unsigned int | - | 1 | 2048 | 0 |
| 0x41 | Fehlerkennung BusOff Betriebssystem | 0-n | high | 0xFF | FUmweltTexte12 | 1 | 1 | 0 |
| 0x42 | Temperatur TCU, Rohwert | °C | high | signed int | - | 1 | 1 | 0 |
| 0x43 | Quality-Information PV1 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x44 | Quality-Information PV2 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x45 | Quality-Information PV3 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x46 | Quality-Information PV4 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x47 | Quality-Information PV6 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x48 | Quality-Information PV7 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x49 | Quality-Information Drucksensor 1 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x4A | Quality-Information Drucksensor 2 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x4B | Gefilterter Ist-Druck Kupplung 1 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x4C | Gefilterter Ist-Druck Kupplung 2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x4D | Solldruck Kupplung 1 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x4E | Solldruck Kupplung 2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x4F | Detail. Status Kupplung 1 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x50 | Detail. Status Kupplung 2 | - | - | unsigned char | - | 1 | 1 | 0 |
| 0x51 | Antriebsdrehzahl, Rohwert | - | high | unsigned int | - | 1 | 4 | 0 |
| 0x52 | Nachadaptionswert Neutral SST 1/3 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x53 | Nachadaptionswert Neutral SST 2/R | mm | high | signed char | - | 1 | 40 | 0 |
| 0x54 | Nachadaptionswert Neutral SST 5/7 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x55 | Nachadaptionswert Neutral SST 6/4 | mm | high | signed char | - | 1 | 40 | 0 |
| 0x56 | Fehlerflags Sicherheitskonzept 1 | 0-n | - | 0xFFFF | FUmweltTexte33 | 1 | 1 | 0 |
| 0x57 | Fehlerflags Sicherheitskonzept 2 | 0-n | - | 0xFFFF | FUmweltTexte34 | 1 | 1 | 0 |
| 0x58 | Spannungswert Schaltpaddles | V | high | unsigned int | - | 1 | 124 | 0 |
| 0x59 | Ist-Strom PV1 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5A | Ist-Strom PV2 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5B | Ist-Strom PV3 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5C | Ist-Strom PV4 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5D | Ist-Strom PV6 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5E | Ist-Strom PV7 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x5F | Temperatur Abspritz-Öl | °C | high | signed int | - | 1 | 1 | 0 |
| 0x60 | Temperatur Sumpf-Öl | °C | high | signed int | - | 1 | 1 | 0 |
| 0x61 | RSC Status | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x62 | RSC Testgröße | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x63 | Predizierter Gang | - | high | signed char | - | 1 | 1 | 0 |
| 0x64 | Soll-Status SV3 | 0-n | high | 0xFF000000 | FUmweltTexte26 | 1 | 1 | 0 |
| 0x65 | Soll-Status CutOff 1 | 0-n | high | 0x00FF0000 | FUmweltTexte27 | 1 | 1 | 0 |
| 0x66 | Soll-Status CutOff 2 | 0-n | high | 0x0000FF00 | FUmweltTexte28 | 1 | 1 | 0 |
| 0x67 | Startdruck 1 für PLM | bar | high | signed int | - | 1 | 100 | 0 |
| 0x68 | Startdruck 2 für PLM | bar | high | signed int | - | 1 | 100 | 0 |
| 0x69 | Fehlerwert PS-Diagnose | 0-n | high | 0x000000FF | FUmweltTexte29 | 1 | 1 | 0 |
| 0x6A | Parksperrenzustand | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x6B | Fehlerart PSM-Diagnose | 0-n | high | 0x00FF | FUmweltTexte30 | 1 | 1 | 0 |
| 0x6C | Status Parksperrenmanager | 0-n | high | 0xFF | FUmweltTexte23 | 1 | 1 | 0 |
| 0x6D | Logischer Getriebezustand | 0-n | high | 0xFF | FUmweltTexte24 | 1 | 1 | 0 |
| 0x6E | Auto-P-supply | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x6F | Auto-P-switch | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x70 | PS-Sensor 1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x71 | PS-Sensor 2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x72 | Bed. Getriebewahltaster P1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x73 | Bed. Getriebewahltaster P2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x74 | Fehlerart Sicherheitszeit | 0-n | high | 0x00FF | FUmweltTexte25 | 1 | 1 | 0 |
| 0x76 | Ausgabe Ebene 2 | 0-n | high | 0xFFFF | FUmweltTexte13 | 1 | 1 | 0 |
| 0x77 | Motordrehzahl CAN | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x78 | Status Anhänger | 0-n | - | 0xFF | FUmweltTexte01 | 1 | 1 | 0 |
| 0x79 | Modelltemperatur K1 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x7A | Modelltemperatur K2 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x7B | Kühlmodus | 0-n | - | 0xFF | FUmweltTexte02 | 1 | 1 | 0 |
| 0x7C | Drucktoleranz K1 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x7D | Drucktoleranz K2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x7E | Status A | 0-n | high | 0xFF | FUmweltTexte41 | 1 | 1 | 0 |
| 0x7F | Status B | 0-n | high | 0xFF000000 | FUmweltTexte41 | 1 | 1 | 0 |
| 0x80 | Status C | 0-n | high | 0x00FF0000 | FUmweltTexte41 | 1 | 1 | 0 |
| 0x81 | Status D | 0-n | high | 0x0000FF00 | FUmweltTexte41 | 1 | 1 | 0 |
| 0x82 | Status E | 0-n | high | 0xFF | FUmweltTexte42 | 1 | 1 | 0 |
| 0x83 | Sollwertüberwachung Temic | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x84 | Ölfilm-Temperatur K1 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x85 | Ölfilm-Temperatur K2 | °C | high | signed int | - | 1 | 1 | 0 |
| 0x86 | Statisches Motormoment | Nm | high | signed int | - | 1 | 8 | 0 |
| 0x87 | Abspritzsensor Rohwert | °C | high | signed int | - | 1 | 1 | 0 |
| 0x88 | Abweichung zu erw. Systemdruck | bar | high | signed int | - | 1 | 100 | 0 |
| 0x89 | Erw. Systemdruck | bar | high | signed int | - | 1 | 100 | 0 |
| 0x8A | Adaptionsstrom Offset | A | high | signed int | - | 1 | 1000 | 0 |
| 0x8B | Umgebungsluftdruck | bar | high | unsigned char | - | 2 | 1 | 299 |
| 0x8C | Querbeschleunigung | m/s^2 | high | signed int | - | 1 | 40 | 0 |
| 0x8D | Anzeige Getriebepos. Ebene2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x8E | Getriebesollposition aus Ebene1 | 0-n | high | 0xFF | FUmweltTexte14 | 1 | 1 | 0 |
| 0x8F | Druck PV1 Ebene2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x90 | Druck PV2 Ebene2 | bar | high | signed int | - | 1 | 100 | 0 |
| 0x91 | Parksperrenstatus Ebene2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x92 | Fahrerwunsch Ebene2 | 0-n | high | 0xFF00 | FUmweltTexte16 | 1 | 1 | 0 |
| 0x93 | Fahrzeuggeschwindigkeit Ebene2 | km | high | unsigned int | - | 1 | 5 | 0 |
| 0x94 | Eingelegte Gänge Ebene2 | 0-n | high | 0x00FF | FUmweltTexte18n | 1 | 1 | 0 |
| 0x95 | Aktive Schaltventile Ebene2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x96 | Drehrichtung Getriebeeingang Ebene2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0x97 | Sollstrom PV1 Ebene2 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x98 | Sollstrom PV2 Ebene2 | A | high | unsigned int | - | 1 | 1000 | 0 |
| 0x99 | Eingangsdrehzahl TG1 Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x9A | Eingangsdrehzahl TG2 Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x9B | Farhpedal Ebene2 | % | high | unsigned char | - | 100 | 255 | 0 |
| 0x9C | Status Motorschleppmomentenregelung MSR Ebene2 | 0-n | high | 0xFF | FUmweltTexte22 | 1 | 1 | 0 |
| 0x9D | Berechnete Eingangsdrehzahl TG1 über Sollgang Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x9E | Berechnete Eingangsdrehzahl TG2 über Sollgang Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0x9F | Status Modus DKG bezüglich Motoranforderung aus Ebene 1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xA0 | Drehmoment Fahrerwunsch Ebene 2 | - | high | signed int | - | 1 | 2 | 0 |
| 0xA1 | Gefilterte Eingangsdrehzahl TG1 Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0xA2 | Gefilterte Eingangsdrehzahl TG2 Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0xA3 | Motordrehzahl Ebene2 | U/min | high | unsigned int | - | 1 | 4 | 0 |
| 0xA4 | Erster gemessener Kupplungsdruck bei der PV7-Druckpeak-Erkennung | bar | high | signed int | - | 1 | 100 | 0 |
| 0xA5 | Minimal gemessener Kupplungsdruck bei der PV7-Druckpeak-Erkennung | bar | high | signed int | - | 1 | 100 | 0 |
| 0xA6 | Maximal gemessener Kupplungsdruck bei der PV7-Druckpeak-Erkennung | bar | high | signed int | - | 1 | 100 | 0 |
| 0xA7 | Status HSD 0 | 0-n | high | 0xFF | FUmweltTexte09 | 1 | 1 | 0 |
| 0xA8 | Status HSD 1 | 0-n | high | 0xFF | FUmweltTexte10 | 1 | 1 | 0 |
| 0xA9 | Status HSD 2 | 0-n | high | 0xFF | FUmweltTexte11 | 1 | 1 | 0 |
| 0xAA | Status D2 | 0-n | high | 0x000000FF | FUmweltTexte41 | 1 | 1 | 0 |
| 0xAB | Akt. Kupplungsreferenzmoment | U/min/sek | high | signed int | - | 1 | 1 | 0 |
| 0xAC | Ist-Druck Kupplung 1 Rohwert | bar | high | signed int | - | 1 | 100 | 0 |
| 0xAD | Ist-Druck Kupplung 2 Rohwert | bar | high | signed int | - | 1 | 100 | 0 |
| 0xAE | Ebene2s Analyse | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xAF | Spannung Abspritzsensor | V | high | unsigned int | - | 1 | 310 | 0 |
| 0xB0 | Hauptzustand KP-Einlernroutine | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB1 | Unterzustand KP-Einlernroutine | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB2 | Ergebnis KP-Einlernroutine | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB3 | HS Diagnose Parksperrenmagnet | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB4 | Widerstandswert Parksperrenmagnet | Ohm | high | unsigned char | - | 1 | 1 | 0 |
| 0xB5 | HS-Dia-Startwert | Ohm | high | unsigned char | - | 1 | 1 | 0 |
| 0xB6 | Widerstands-Startwert | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB7 | Status Motor fehlerhaft | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB8 | CAN Notlauf Ursache | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xB9 | Ebene2 Debug Flag | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xBA | Pfad Fahrerwunsch | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xBB | Ankündigung Motor Start Stop MSA | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xBC | Anforderung Motor Start MSA | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xBD | Status MSA Funktion | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xBE | Status MSA Motorstopp | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xE0 | Fehlerstatus Schaltstange 5/7 (GBX) | 0-n | high | 0xFF00 | FUmweltTexte31 | 1 | 1 | 0 |
| 0xE1 | Fehlerstatus Schaltstange 6/4 (GBX) | 0-n | high | 0x00FF | FUmweltTexte32 | 1 | 1 | 0 |
| 0xE2 | Eingelegte Gänge Ebene2 | 0-n | high | 0xFF | FUmweltTexte35n | 1 | 1 | 0 |
| 0xE3 | Fehlerwert PS-Diagnose | 0-n | high | 0xFF | FUmweltTexte36 | 1 | 1 | 0 |
| 0xE4 | Status Parksperrenmanager | 0-n | high | 0xFF | FUmweltTexte37 | 1 | 1 | 0 |
| 0xE5 | Logischer Getriebezustand | 0-n | high | 0x00FF | FUmweltTexte38 | 1 | 1 | 0 |
| 0xE6 | Soll-Status SV3 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xE7 | Soll-Status CutOff 1 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xE8 | Soll-Status CutOff 2 | - | high | unsigned char | - | 1 | 1 | 0 |
| 0xE9 | Fehlerart PSM-Diagnose | 0-n | high | 0xFF | FUmweltTexte40 | 1 | 1 | 0 |
| 0xF5 | Umweltdatum 1 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xF6 | Umweltdatum 2 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xF7 | Umweltdatum 3 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xF8 | Umweltdatum 4 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xF9 | Umweltdatum 5 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFA | Umweltdatum 6 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFB | Umweltdatum 7 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFC | Umweltdatum 8 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFD | Umweltdatum 9 | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFE | Umweltdatum 10 | - | high | unsigned int | - | 1 | 1 | 0 |

<a id="table-iarttyp"></a>
### IARTTYP

Dimensions: 138 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x5A41 | 0x51 | 0x50 | 0x01 | 0x4A |
| 0x5A43 | 0x51 | 0x50 | 0x01 | 0x4A |
| 0x5A44 | 0x06 | 0x05 | 0xFFFF | 0xFFFF |
| 0x5A45 | 0x06 | 0x05 | 0xFFFF | 0xFFFF |
| 0x5A46 | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A47 | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A48 | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A4B | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A4C | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A52 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A53 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A54 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A55 | 0x02 | 0x03 | 0x4B | 0xFFFF |
| 0x5A56 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A57 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A58 | 0xFFFF | 0xFFFF | 0xFFFF | 0x4E |
| 0x5A59 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A5A | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A5B | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5021 | 0x02 | 0xFFFF | 0x4B | 0xFFFF |
| 0x5022 | 0x02 | 0xFFFF | 0x4B | 0xFFFF |
| 0x5023 | 0x02 | 0xFFFF | 0x4B | 0xFFFF |
| 0x5024 | 0x02 | 0xFFFF | 0x4B | 0xFFFF |
| 0x5025 | 0x40 | 0x3F | 0xFFFF | 0xFFFF |
| 0x5026 | 0x40 | 0x3F | 0xFFFF | 0xFFFF |
| 0x5A42 | 0x43 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5031 | 0x43 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5027 | 0x40 | 0x3F | 0xFFFF | 0xFFFF |
| 0x5028 | 0x40 | 0x3F | 0xFFFF | 0xFFFF |
| 0x5029 | 0xFFFF | 0xFFFF | 0x04 | 0xFFFF |
| 0x5030 | 0xFFFF | 0xFFFF | 0x04 | 0xFFFF |
| 0x5137 | 0xFFFF | 0xFFFF | 0xFFFF | 0x48 |
| 0x5139 | 0xFFFF | 0x3D | 0xFFFF | 0xFFFF |
| 0x5A60 | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A61 | 0xFFFF | 0xFFFF | 0x54 | 0x07 |
| 0x5A62 | 0xFFFF | 0xFFFF | 0x54 | 0x07 |
| 0x5A63 | 0xFFFF | 0xFFFF | 0x54 | 0x07 |
| 0x5A64 | 0xFFFF | 0xFFFF | 0x54 | 0x07 |
| 0x5A65 | 0xFFFF | 0xFFFF | 0x09 | 0x08 |
| 0x5A66 | 0xFFFF | 0xFFFF | 0x09 | 0x08 |
| 0x5A67 | 0xFFFF | 0xFFFF | 0x09 | 0x08 |
| 0x5A68 | 0xFFFF | 0xFFFF | 0x09 | 0x08 |
| 0x5A69 | 0x0E | 0x0C | 0x0B | 0x0A |
| 0x5A6A | 0x0E | 0x0C | 0x0B | 0x0A |
| 0x5A6B | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A6C | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A6D | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A6E | 0xFFFF | 0xFFFF | 0xFFFF | 0x07 |
| 0x5A70 | 0x11 | 0xFFFF | 0x10 | 0x0F |
| 0x5A71 | 0x11 | 0xFFFF | 0x10 | 0x0F |
| 0x5A72 | 0x14 | 0xFFFF | 0x13 | 0x12 |
| 0x5A73 | 0xFFFF | 0x17 | 0x16 | 0x15 |
| 0x5A74 | 0x18 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A75 | 0x18 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A76 | 0x18 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A80 | 0xFFFF | 0xFFFF | 0x1A | 0x19 |
| 0x5A81 | 0xFFFF | 0xFFFF | 0x1C | 0x1B |
| 0x5A82 | 0xFFFF | 0xFFFF | 0x1E | 0x1D |
| 0x5A83 | 0xFFFF | 0xFFFF | 0x20 | 0x1F |
| 0x5A84 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A85 | 0x22 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A86 | 0x23 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A87 | 0x24 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5A88 | 0x24 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5072 | 0xFFFF | 0xFFFF | 0x25 | 0xFFFF |
| 0x5073 | 0xFFFF | 0xFFFF | 0x26 | 0xFFFF |
| 0x5074 | 0xFFFF | 0xFFFF | 0x27 | 0xFFFF |
| 0x5A8B | 0x28 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF07 | 0xFFFF | 0x29 | 0xFFFF | 0xFFFF |
| 0xCF10 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF11 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF12 | 0xFFFF | 0xFFFF | 0x2B | 0x2A |
| 0xCF13 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF14 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF15 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF16 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF17 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF18 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF19 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1A | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF1B | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1C | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1D | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1E | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF1F | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF20 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF21 | 0xFFFF | 0x2C | 0x2B | 0x2A |
| 0xCF22 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF23 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF24 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF25 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF26 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF27 | 0xFFFF | 0xFFFF | 0x2B | 0x56 |
| 0xCF28 | 0xFFFF | 0xFFFF | 0xFFFF | 0x2A |
| 0xCF29 | 0x30 | 0x2C | 0x2B | 0x2A |
| 0xCF30 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF31 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF32 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF33 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF34 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF35 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF36 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF37 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF38 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF39 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3A | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3B | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3C | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3D | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3E | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF3F | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF40 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF41 | 0x30 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0xCF42 | 0x2F | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5124 | 0xFFFF | 0xFFFF | 0xFFFF | 0x53 |
| 0x5A25 | 0x31 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5126 | 0xFFFF | 0x34 | 0x33 | 0x32 |
| 0x5127 | 0x35 | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5128 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5129 | 0xFFFF | 0xFFFF | 0xFFFF | 0x4D |
| 0x5130 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5131 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5132 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5133 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5134 | 0xFFFF | 0xFFFF | 0xFFFF | 0x41 |
| 0x5054 | 0xFFFF | 0x38 | 0x37 | 0x36 |
| 0x5135 | 0xFFFF | 0xFFFF | 0xFFFF | 0x47 |
| 0x5138 | 0xFFFF | 0xFFFF | 0xFFFF | 0x55 |
| 0x5055 | 0xFFFF | 0xFFFF | 0xFFFF | 0x39 |
| 0x5056 | 0xFFFF | 0xFFFF | 0xFFFF | 0x3A |
| 0x5057 | 0xFFFF | 0x52 | 0xFFFF | 0xFFFF |
| 0x5058 | 0xFFFF | 0xFFFF | 0x49 | 0x3C |
| 0x5059 | 0xFFFF | 0x3D | 0xFFFF | 0x3E |
| 0x5060 | 0xFFFF | 0xFFFF | 0x4C | 0x4D |
| 0x5061 | 0xFFFF | 0xFFFF | 0x45 | 0x44 |
| 0x5062 | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |
| 0x5063 | 0xFFFF | 0xFFFF | 0xFFFF | 0x46 |
| 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF | 0xFFFF |

<a id="table-iarttexteindividuell"></a>
### IARTTEXTEINDIVIDUELL

Dimensions: 84 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | kein passendes Fehlersymptom |
| 0x01 | Offset-Fehler |
| 0x02 | Kurzschluss |
| 0x03 | Kabelbruch |
| 0x04 | Befüllzeit |
| 0x05 | Druck zu niedrig |
| 0x06 | Druck zu hoch |
| 0x07 | Symptomspezifisch |
| 0x08 | Wert unter Schwelle |
| 0x09 | Wert über Schwelle |
| 0x0A | SST 1/3 |
| 0x0B | SST 2/R |
| 0x0C | SST 5/7 |
| 0x0E | SST 6/4 |
| 0x0F | Temperaturwert oberhalb zulässigem Genzwert |
| 0x10 | Temperaturwert unterhalb zulässigem Gernzwert |
| 0x11 | Sensorwert unplausibel |
| 0x12 | Versorgungsspannungswert oberhalb zulässigem Grenzwert |
| 0x13 | Versorgungsspannungswert unterhalb zulässigem Grenzwert |
| 0x14 | Spannungswert unplausibel |
| 0x15 | Spannungswert außerhalb Spezifikation |
| 0x16 | Kurzschluss Masse |
| 0x17 | Leitungsunterbrechung |
| 0x18 | Wert nicht plausibel |
| 0x19 | Vorspannung UH2_7V4 oberhalb Schwelle |
| 0x1A | Vorspannung UH2_7V4 unterhalb Schwelle |
| 0x1B | Interne 5V Spannung oberhalb Schwelle |
| 0x1C | Interne 5V Spannung unterhalb Schwelle |
| 0x1D | Sensorversorgung SV1 oberhalb Schwelle |
| 0x1E | Sensorversorgung SV1 unterhalb Schwelle |
| 0x1F | Sensorversorgung SV2 oberhalb Schwelle |
| 0x20 | Sensorversorgung SV2 unterhalb Schwelle |
| 0x22 | Core Eigendiagnose Fehler gekennzeichnet |
| 0x23 | Interner Temperatur TC 1766 unplausibel |
| 0x24 | Nicht flüchtig gespeicherte Einlerndaten unplausibel |
| 0x25 | Versorgungsspannung Ventilgruppe 1 unterhalb zulässigem Grenzwert |
| 0x26 | Versorgungsspannung Ventilgruppe 2 unterhalb zulässigem Grenzwert |
| 0x27 | Versorgungsspannung Ventilgruppe 3 unterhalb zulässigem Grenzwert |
| 0x28 | Temperaturwert unplausibel |
| 0x29 | Busoff |
| 0x2A | Timeout Botschaft PT-CAN |
| 0x2B | Fehlerhafter Alivecounter |
| 0x2C | Fehlerhafte Checksumme |
| 0x2E | Kommunikationsfehler LIN |
| 0x2F | Ungültig gekennzeichnete oder unplausible Nachricht |
| 0x30 | Ungültig gekennzeichnete Nachricht |
| 0x31 | Wählhebel Botschaften fehlerhaft |
| 0x32 | Energiesparmodus Fertigung aktiv |
| 0x33 | Energiesparmodus Transport aktiv |
| 0x34 | Energiesparmodus Werkstatt aktiv |
| 0x35 | Anforderung Restart Nachlaufzeit wird von CAS nicht quitiert |
| 0x36 | Überschritten beim Einlegen über PS_1 |
| 0x37 | Überschritten beim Einlegen über PS_2 |
| 0x38 | Überschritten beim Auslegen |
| 0x39 | Hängendes Absperrventil |
| 0x3A | Parksperrensensor |
| 0x3C | Beide Signale ungültig |
| 0x3D | Ungewollt Eingefallen |
| 0x3E | Ungewollt Ausgelegt |
| 0x3F | Untere Grenze verletzt |
| 0x40 | Obere Grenze verletzt |
| 0x41 | Ebene 2 Fehler |
| 0x42 | Elektrischer Defekt |
| 0x43 | Referenzmoment zu hoch |
| 0x44 | Parksperrenschieber 1 |
| 0x45 | Parksperrenschieber 2 |
| 0x46 | N-Haltephase über Tester deaktiviert |
| 0x47 | Ebene2s Fehler |
| 0x48 | Abbruch |
| 0x49 | Eins von beiden Signalen ungültig |
| 0x4A | Sensordrift oder Stuck-At |
| 0x4B | Fehler in Endstufen ASIC |
| 0x4C | PSM wird unter Umständen immer bestromt |
| 0x4D | PSM kann nicht mehr bestromt werden |
| 0x4E | Bereichsverletzung |
| 0x4F | Gradient unplausibel |
| 0x50 | Eingangsspannung zu niedrig |
| 0x51 | Eingangsspannung zu hoch |
| 0x52 | Überschritten beim Auslegen |
| 0x53 | Zusatzinfo |
| 0x54 | Quellenfehler |
| 0x55 | CAN-Notlauf |
| 0x56 | Timeout Botschaft Bedienung Getriebewahlschalter LIN |
| 0xFFFF | Fehlersymptom nicht definiert |

<a id="table-gangstatus"></a>
### GANGSTATUS

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Neutral |
| 0x01 | 1. Gang |
| 0x02 | 2. Gang |
| 0x03 | 3. Gang |
| 0x04 | 4. Gang |
| 0x05 | 5. Gang |
| 0x06 | 6. Gang |
| 0x07 | 7. Gang |
| 0x0E | Rueckwärtsgang |
| 0x0F | Undefiniert |

<a id="table-getriebestatus"></a>
### GETRIEBESTATUS

Dimensions: 23 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Status undefiniert |
| 0x01 | Status Neutral |
| 0x02 | Status Gang geschaltet oben |
| 0x03 | Status Gang geschaltet unten |
| 0x04 | Status Vorsynchron fahren oben |
| 0x05 | Status Vorsynchron fahren unten |
| 0x06 | Status Synchronisieren oben |
| 0x07 | Status Synchronisieren unten |
| 0x08 | Status Durchschalten oben |
| 0x09 | Status Durchschalten unten |
| 0x0A | Status Gang nachdrücken oben |
| 0x0B | Status Gang nachdrücken unten |
| 0x0C | Status Vorspannen oben |
| 0x0D | Status Vorspannen unten |
| 0x0E | Status Vorspannen abbrechen oben |
| 0x0F | Status Vorspannen abbrechen unten |
| 0x10 | Status Gang auslegen oben |
| 0x11 | Status Gang auslegen unten |
| 0x12 | Status Neutral überschieben oben |
| 0x13 | Status Neutral überschieben unten |
| 0x14 | Status Neutral einregeln oben |
| 0x15 | Status Neutral einregeln unten |
| 0xFF | Undefiniert |

<a id="table-kupplungsstati"></a>
### KUPPLUNGSSTATI

Dimensions: 10 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Initialisierungswert |
| 0x01 | Kupplung offen |
| 0x02 | Kupplung überträgt Moment |
| 0x03 | Erstbefüllung nach Reset |
| 0x04 | Zustand nach Initialisierung |
| 0x05 | Kupplung entleeren oder Füllen. Überstandszustand zwischen 2 nach 1 oder umgekehrt. |
| 0x06 | Kupplungs-PVs reagieren auf Anforderungen aus dem Parksperrenmodul |
| 0x07 | Kupplung kann innerhalb bestimmter Zeit nicht gefüllt werden. Reset durch Wechsel nach Disengaged. |
| 0x08 | Kupplungszweig gesperrt |
| 0xFF | Undefiniert |

<a id="table-obdsteuerfunktion"></a>
### OBDSTEUERFUNKTION

Dimensions: 16 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x01 | Warm Up Cycle erfüllt - kein Freeze-Frame im Master gespeichert |
| 0x02 | Aktivierungsbedingung fuer Berechnung Driving cycle in EGS/SSG - kein Freeze-Frame im Master gespeichert |
| 0x03 | Warm Up Cycle erfüllt und Aktivierungsbedingung für Berechnung Driving cycle in EGS/SSG - kein Freeze-Frame im Master gespeichert |
| 0x09 | Warm Up Cycle erfüllt - Freeze Frame wird verwaltet für: DME (Master) |
| 0x0A | Aktivierungsbedingung fuer Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: DME (Master) |
| 0x0B | Warm Up Cycle erfüllt und Aktivierungsbedingung für Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: DME (Master) |
| 0x11 | Warm Up Cycle erfüllt - Freeze Frame wird verwaltet für: EGS |
| 0x12 | Aktivierungsbedingung fuer Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: EGS |
| 0x13 | Warm Up Cycle erfüllt und Aktivierungsbedingung für Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: EGS |
| 0x21 | Warm Up Cycle erfüllt - Freeze Frame wird verwaltet für: EKP |
| 0x22 | Aktivierungsbedingung fuer Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: EKP |
| 0x23 | Warm Up Cycle erfüllt und Aktivierungsbedingung für Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: EKP |
| 0x31 | Warm Up Cycle erfüllt - Freeze Frame wird verwaltet für:DME links |
| 0x32 | Aktivierungsbedingung fuer Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: DME links |
| 0x33 | Warm Up Cycle erfüllt und Aktivierungsbedingung für Berechnung Driving cycle in EGS/SSG - Freeze-Frame wird verwaltet für: DME links |
| 0xFF | Signal ungültig |

<a id="table-schaltstangeposition"></a>
### SCHALTSTANGEPOSITION

Dimensions: 11 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | Position undefiniert |
| 0x01 | Position Neutral |
| 0x02 | Position oben |
| 0x03 | Position unten |
| 0x04 | Position Synchron oben |
| 0x05 | Position Synchron unten |
| 0x06 | Position vor Synchron oben |
| 0x07 | Position vor Synchron unten |
| 0x08 | Position nach Synchron oben |
| 0x09 | Position nach Synchron unten |
| 0xFF | Undefiniert |

<a id="table-io-setzen"></a>
### IO_SETZEN

Dimensions: 20 rows × 5 columns

| STELLGL_NAME | STELLGL_IO_HEX | IO_TYP | MIN_WERT | MAX_WERT |
| --- | --- | --- | --- | --- |
| SOLLSTROM MAGNETVENTIL PV1 | 0x20 | 2 | 0 | 1900 |
| SOLLSTROM MAGNETVENTIL PV2 | 0x21 | 2 | 0 | 1900 |
| SOLLSTROM MAGNETVENTIL PV3 | 0x22 | 2 | 0 | 1900 |
| SOLLSTROM MAGNETVENTIL PV4 | 0x23 | 2 | 0 | 1900 |
| SOLLSTROM MAGNETVENTIL PV6 | 0x24 | 2 | 0 | 1900 |
| SOLLSTROM MAGNETVENTIL PV7 | 0x25 | 2 | 0 | 1900 |
| SOLLZUSTAND MAGNETVENTIL SV1 | 0x26 | 1 | 0 | 1 |
| SOLLZUSTAND MAGNETVENTIL SV2 | 0x27 | 1 | 0 | 1 |
| SOLLZUSTAND MAGNETVENTIL SV3 | 0x28 | 1 | 0 | 1 |
| SOLLZUSTAND MAGNETVENTIL SV4 | 0x29 | 1 | 0 | 1 |
| PARKSPERRE_VERRIEGELN | 0x2A | 3 | 0 | 3 |
| ANZEIGE_PROGRAMMINFORMATION | 0x2B | 3 | 1 | 7 |
| GETRIEBE NACH NEUTRAL STELLEN | 0x2C | 1 | 1 | 1 |
| PARKSPERRE HAKENTEST | 0x2D | 1 | 0 | 1 |
| PARKSPERRE MAGNETTEST | 0x2E | 1 | 0 | 1 |
| ANSTEUERUNG PARKSPERRE AUS/EIN | 0x2F | 1 | 0 | 1 |
| ANZEIGE WAHLHEBELSCHEMA | 0x30 | 3 | 1 | 4 |
| ANZEIGE GAENGE | 0x31 | 3 | 1 | 7 |
| ANZEIGE CC MELDUNG | 0x32 | 1 | 0 | 1 |
| ALLE AUSGANGSGRÖSSEN | 0xFE | - | - | - |

<a id="table-testundeinlernprgtabelle"></a>
### TESTUNDEINLERNPRGTABELLE

Dimensions: 15 rows × 2 columns

| TESTEINLERNNR | TESTEINLERNTEXTE |
| --- | --- |
| 0x20 | Beliebigen Gang einlegen |
| 0x21 | Spülfunktion starten |
| 0x22 | Solldruckvorgabe Kupplung 1 |
| 0x23 | Solldruckvorgabe Kupplung 2 |
| 0x24 | Vorgabe des Systemdrucks |
| 0x25 | Kupplungskühlung aktivieren |
| 0x26 | Diagnose Parksperrenmagnet |
| 0x27 | Diagnose PV7 |
| 0x30 | Kupplungsschleifpunkt 1 und 2 einlernen (Kisspoint 1+2) |
| 0x31 | Anti Leerlaufklackern aktivieren |
| 0x32 | Getriebe einlernen |
| 0x33 | Adaptionswerte in NVRAM speichern |
| 0x34 | Ventilkennlinien einlernen PV1/2 |
| 0x35 | Fehlerspeicher formatieren |
| 0xFF | Undefiniert |

<a id="table-statustesteinlern"></a>
### STATUSTESTEINLERN

Dimensions: 6 rows × 2 columns

| STATUSNR | STATUSTEXT |
| --- | --- |
| 0x00 | Testbedingungen nicht erfüllt |
| 0x01 | Testprogramm läuft |
| 0x02 | Testprogramm beendet |
| 0x03 | Testprogramm nicht ordnungsgemäß beendet |
| 0x04 | Testprogramm abgebrochen |
| 0xFF | Undefiniert |

<a id="table-statuseinlerngetriebe"></a>
### STATUSEINLERNGETRIEBE

Dimensions: 15 rows × 2 columns

| STATUSNR | STATUSTEXT |
| --- | --- |
| 0x01 | Warten auf Startbedingungen |
| 0x02 | Alle Schaltstangen Neutral einregeln |
| 0x03 | Zylinder 1 Endanschläge anfahren |
| 0x04 | Zylinder 2 Endanschläge anfahren |
| 0x05 | Zylinder 3 Endanschläge anfahren |
| 0x06 | Zylinder 4 Endanschläge anfahren |
| 0x07 | Zylinder 1 Neutral einregeln |
| 0x08 | Zylinder 2 Neutral einregeln |
| 0x09 | Zylinder 3 Neutral einregeln |
| 0x0A | Zylinder 4 Neutral einregeln |
| 0x0B | Berechne Größen |
| 0x0C | Beendet ohne Fehler |
| 0x0D | Beendet mit Fehler |
| 0x0E | Einlernen durch Anwender abgebrochen |
| 0xFF | Undefiniert |

<a id="table-statuseinlernpv"></a>
### STATUSEINLERNPV

Dimensions: 9 rows × 2 columns

| STATUSNR | STATUSTEXT |
| --- | --- |
| 0x00 | Inaktiv |
| 0x01 | Warten auf Neutral (Timer überwacht) |
| 0x02 | PV Bestromung |
| 0x03 | Einschwingzeit abwarten |
| 0x04 | Gemessenen KPL-Istdruck aufsummieren |
| 0x05 | Mittelwertbildung |
| 0x06 | EEPROM Speicherung |
| 0x32 | Monotoniefehler |
| 0xFF | Undefiniert |

<a id="table-fehlertesteinlerngetriebe"></a>
### FEHLERTESTEINLERNGETRIEBE

Dimensions: 36 rows × 2 columns

| FEHLERNR | FEHLERTEXT |
| --- | --- |
| 0x00 | Es liegt kein Fehler vor |
| 0x01 | Druck der Kupplung 1 zu hoch |
| 0x02 | Druck der Kupplung 2 zu hoch |
| 0x03 | Motordrehzahl zu hoch |
| 0x04 | Motordrehzahl zu niedrig |
| 0x05 | Linepressureanforderung zu gering |
| 0x06 | Getriebetemperatur zu hoch |
| 0x07 | Getriebetemperatur zu niedrig |
| 0x08 | Einlernen wurde durch Anwender abgebrochen |
| 0x0A | Berechnete Amplitude außerhalb der Toleranz |
| 0x0B | Berechnete Amplitude Schaltstange 1 außerhalb der Toleranz |
| 0x0C | Berechnete Amplitude Schaltstange 2 außerhalb der Toleranz |
| 0x0D | Berechnete Amplitude Schaltstange 3 außerhalb der Toleranz |
| 0x0E | Berechnete Amplitude Schaltstange 4 außerhalb der Toleranz |
| 0x14 | Berechnete Verschiebung außerhalb der Toleranz |
| 0x15 | Berechnete Verschiebung Schaltstange 1 außerhalb der Toleranz |
| 0x16 | Berechnete Verschiebung Schaltstange 2 außerhalb der Toleranz |
| 0x17 | Berechnete Verschiebung Schaltstange 3 außerhalb der Toleranz |
| 0x18 | Berechnete Verschiebung Schaltstange 4 außerhalb der Toleranz |
| 0x1F | Zylinder 1 nicht in Mittellage |
| 0x20 | Zylinder 2 nicht in Mittellage |
| 0x21 | Zylinder 3 nicht in Mittellage |
| 0x22 | Zylinder 4 nicht in Mittellage |
| 0x29 | Linker Endanschlag Zylinder 1 außerhalb der Toleranz |
| 0x2A | Linker Endanschlag Zylinder 2 außerhalb der Toleranz |
| 0x2B | Linker Endanschlag Zylinder 3 außerhalb der Toleranz |
| 0x2C | Linker Endanschlag Zylinder 4 außerhalb der Toleranz |
| 0x33 | Rechter Endanschlag Zylinder 1 außerhalb der Toleranz |
| 0x34 | Rechter Endanschlag Zylinder 2 außerhalb der Toleranz |
| 0x35 | Rechter Endanschlag Zylinder 3 außerhalb der Toleranz |
| 0x36 | Rechter Endanschlag Zylinder 4 außerhalb der Toleranz |
| 0x3D | Einlegehänger Schaltstange 1 |
| 0x3E | Einlegehänger Schaltstange 2 |
| 0x3F | Einlegehänger Schaltstange 3 |
| 0x40 | Einlegehänger Schaltstange 4 |
| 0xFF | Undefiniert |

<a id="table-fehlertesteinlernkuehlung"></a>
### FEHLERTESTEINLERNKUEHLUNG

Dimensions: 9 rows × 2 columns

| FEHLERNR | FEHLERTEXT |
| --- | --- |
| 0x00 | Es liegt kein Fehler vor |
| 0x01 | Neutral nicht eingelegt |
| 0x02 | Kupplung nicht offen |
| 0x03 | Fahrzeug steht nicht |
| 0x04 | Motor läuft nicht |
| 0x05 | Bremse nicht getreten |
| 0x06 | Neutral als Sollgang nicht freigegeben |
| 0x07 | Abbruch durch Bediener |
| 0xFF | Undefiniert |

<a id="table-fehlertesteinlernpv"></a>
### FEHLERTESTEINLERNPV

Dimensions: 18 rows × 2 columns

| FEHLERNR | FEHLERTEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Motordrehzahl zu gering |
| 0x02 | Teilgetriebe nicht in N |
| 0x03 | Teilgetriebe nicht in N,  Motordrehzahl zu gering |
| 0x04 | Monotonie der Drücke Kupplung 1 nicht eingehalten |
| 0x05 | Monotonie der Drücke Kupplung 1 nicht eingehalten, Motordrehzahl zu gering |
| 0x06 | Monotonie der Drücke Kupplung 1 nicht eingehalten,  Teilgetriebe nicht in N |
| 0x07 | Monotonie der Drücke Kupplung 1 nicht eingehalten,  Teilgetriebe nicht in N,  Motordrehzahl zu gering |
| 0x08 | Monotonie der Drücke Kupplung 2 nicht eingehalten |
| 0x09 | Monotonie der Drücke Kupplung 2 nicht eingehalten,  Motordrehzahl zu gering |
| 0x0A | Monotonie der Drücke Kupplung 2 nicht eingehalten,  Teilgetriebe nicht in N |
| 0x0B | Monotonie der Drücke Kupplung 2 nicht eingehalten,  Teilgetriebe nicht in N, Motordrehzahl zu gering |
| 0x0C | Monotonie der Drücke Kupplung 1 + 2  nicht eingehalten |
| 0x0D | Monotonie der Drücke Kupplung 1 + 2  nicht eingehalten Motordrehzahl zu gering |
| 0x0E | Monotonie der Drücke Kupplung 1 + 2  nicht eingehalten Teilgetriebe nicht in N |
| 0X0F | Monotonie der Drücke Kupplung 1 + 2  nicht eingehalten Teilgetriebe nicht in N, Motordrehzahl zu gering |
| 0x10 | Abbruch durch den Benutzer |
| 0xFF | Undefiniert |

<a id="table-fumwelttabelle-5a57a"></a>
### FUMWELTTABELLE_5A57A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x0A | 0x0B | 0x86 | 0x5E | 0x60 | 0x02 | 0x87 |

<a id="table-fumwelttabelle-5a60a"></a>
### FUMWELTTABELLE_5A60A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x0B | 0x0C | 0x0D | 0x0E | 0x17 | 0x18 | 0x02 |

<a id="table-fumwelttabelle-5a60d"></a>
### FUMWELTTABELLE_5A60D

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x13 |

<a id="table-fumwelttabelle-5a61a"></a>
### FUMWELTTABELLE_5A61A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x18 | 0x02 | 0x0B | 0x0C | 0x0D | 0x0E | 0x13 |

<a id="table-fumwelttabelle-5a61d"></a>
### FUMWELTTABELLE_5A61D

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x1D |

<a id="table-fumwelttabelle-5a62a"></a>
### FUMWELTTABELLE_5A62A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x18 | 0x02 | 0x0B | 0x0C | 0x0D | 0x0E | 0x13 |

<a id="table-fumwelttabelle-5a62d"></a>
### FUMWELTTABELLE_5A62D

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x1E |

<a id="table-fumwelttabelle-5a63a"></a>
### FUMWELTTABELLE_5A63A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x18 | 0x02 | 0x0B | 0x0C | 0x0D | 0x0E | 0x13 |

<a id="table-fumwelttabelle-5a63d"></a>
### FUMWELTTABELLE_5A63D

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x20 |

<a id="table-fumwelttabelle-5a64a"></a>
### FUMWELTTABELLE_5A64A

Dimensions: 1 rows × 9 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR | UW8_NR |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 8 | 0x17 | 0x18 | 0x02 | 0x0B | 0x0C | 0x0D | 0x0E | 0x13 |

<a id="table-fumwelttabelle-5a64d"></a>
### FUMWELTTABELLE_5A64D

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x1F |

<a id="table-fumwelttabelle-5a65a"></a>
### FUMWELTTABELLE_5A65A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x1B | 0x1C | 0x17 | 0x18 | 0x01 | 0x0B | 0x02 |

<a id="table-fumwelttabelle-5a65d"></a>
### FUMWELTTABELLE_5A65D

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x13 |

<a id="table-fumwelttabelle-5a66a"></a>
### FUMWELTTABELLE_5A66A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x1B | 0x1C | 0x17 | 0x18 | 0x01 | 0x0B | 0x02 |

<a id="table-fumwelttabelle-5a66d"></a>
### FUMWELTTABELLE_5A66D

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x13 |

<a id="table-fumwelttabelle-5a67a"></a>
### FUMWELTTABELLE_5A67A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x1B | 0x1C | 0x17 | 0x18 | 0x01 | 0x0B | 0x02 |

<a id="table-fumwelttabelle-5a67d"></a>
### FUMWELTTABELLE_5A67D

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x13 |

<a id="table-fumwelttabelle-5a68a"></a>
### FUMWELTTABELLE_5A68A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x1B | 0x1C | 0x17 | 0x18 | 0x01 | 0x0B | 0x02 |

<a id="table-fumwelttabelle-5a68d"></a>
### FUMWELTTABELLE_5A68D

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x13 |

<a id="table-fumwelttabelle-5a69a"></a>
### FUMWELTTABELLE_5A69A

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x24 | 0x25 | 0x26 | 0x27 | 0x28 |

<a id="table-fumwelttabelle-5a6ba"></a>
### FUMWELTTABELLE_5A6BA

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x18 | 0x02 | 0x0B | 0x0C | 0x0D | 0x0E | 0x13 |

<a id="table-fumwelttabelle-5a6bd"></a>
### FUMWELTTABELLE_5A6BD

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x1D |

<a id="table-fumwelttabelle-5a6ca"></a>
### FUMWELTTABELLE_5A6CA

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x18 | 0x02 | 0x0B | 0x0C | 0x0D | 0x0E | 0x13 |

<a id="table-fumwelttabelle-5a6cd"></a>
### FUMWELTTABELLE_5A6CD

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x1E |

<a id="table-fumwelttabelle-5a6da"></a>
### FUMWELTTABELLE_5A6DA

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x18 | 0x02 | 0x0B | 0x0C | 0x0D | 0x0E | 0x13 |

<a id="table-fumwelttabelle-5a6dd"></a>
### FUMWELTTABELLE_5A6DD

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x1F |

<a id="table-fumwelttabelle-5a6ea"></a>
### FUMWELTTABELLE_5A6EA

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x18 | 0x02 | 0x0B | 0x0C | 0x0D | 0x0E | 0x13 |

<a id="table-fumwelttabelle-5a6ed"></a>
### FUMWELTTABELLE_5A6ED

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x20 |

<a id="table-fumwelttabelle-5a70a"></a>
### FUMWELTTABELLE_5A70A

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x02 | 0x42 | 0x35 | 0x36 | 0x37 |

<a id="table-fumwelttabelle-5a70d"></a>
### FUMWELTTABELLE_5A70D

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x38 |

<a id="table-fumwelttabelle-5a71a"></a>
### FUMWELTTABELLE_5A71A

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x02 | 0x35 | 0x42 | 0x36 | 0x37 |

<a id="table-fumwelttabelle-5a71d"></a>
### FUMWELTTABELLE_5A71D

Dimensions: 1 rows × 2 columns

| UW_ANZ | UW1_NR |
| --- | --- |
| 1 | 0x39 |

<a id="table-fumwelttabelle-5a72a"></a>
### FUMWELTTABELLE_5A72A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x01 | 0x0B | 0x3A | 0x3B | 0x3C | 0x3D | 0x40 |

<a id="table-fumwelttabelle-5a74a"></a>
### FUMWELTTABELLE_5A74A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x31 | 0x0E | 0x04 | 0x34 | 0x61 | 0x62 | 0x05 |

<a id="table-fumwelttabelle-5a75a"></a>
### FUMWELTTABELLE_5A75A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x32 | 0x0E | 0x04 | 0x34 | 0x61 | 0x62 | 0x05 |

<a id="table-fumwelttabelle-5a80a"></a>
### FUMWELTTABELLE_5A80A

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x3E | 0x3F | 0x40 |

<a id="table-fumwelttabelle-5a81a"></a>
### FUMWELTTABELLE_5A81A

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x3E | 0x3F | 0x40 |

<a id="table-fumwelttabelle-5a82a"></a>
### FUMWELTTABELLE_5A82A

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x3E | 0x3F | 0x40 |

<a id="table-fumwelttabelle-5a83a"></a>
### FUMWELTTABELLE_5A83A

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x3E | 0x3F | 0x40 |

<a id="table-fumwelttabelle-5a86a"></a>
### FUMWELTTABELLE_5A86A

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x0B | 0x02 | 0x42 | 0x35 | 0x36 |

<a id="table-fumwelttabelle-5072a"></a>
### FUMWELTTABELLE_5072A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x01 | 0x0B | 0x3A | 0x3B | 0x3C | 0x3D | 0x40 |

<a id="table-fumwelttabelle-5073a"></a>
### FUMWELTTABELLE_5073A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x3B | 0x3C |

<a id="table-fumwelttabelle-5074a"></a>
### FUMWELTTABELLE_5074A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x3B | 0x3C |

<a id="table-fumwelttabelle-5a8ba"></a>
### FUMWELTTABELLE_5A8BA

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x0B | 0x02 | 0x42 | 0x35 | 0x36 |

<a id="table-fumwelttabelle-cf30a"></a>
### FUMWELTTABELLE_CF30A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x0D | 0x29 | 0x33 | 0x34 | 0x2E | 0x61 | 0x62 |

<a id="table-fumwelttabelle-cf31a"></a>
### FUMWELTTABELLE_CF31A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x0D | 0x2A | 0x33 | 0x34 | 0x2E | 0x61 | 0x62 |

<a id="table-fumwelttabelle-cf32a"></a>
### FUMWELTTABELLE_CF32A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x0D | 0x2B | 0x33 | 0x34 | 0x2E | 0x61 | 0x62 |

<a id="table-fumwelttabelle-cf33a"></a>
### FUMWELTTABELLE_CF33A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x0D | 0x2C | 0x33 | 0x34 | 0x2E | 0x61 | 0x62 |

<a id="table-fumwelttabelle-5a52a"></a>
### FUMWELTTABELLE_5A52A

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x5F | 0x37 | 0x60 | 0x5E | 0x79 | 0x7A |

<a id="table-fumwelttabelle-5a53a"></a>
### FUMWELTTABELLE_5A53A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x5F | 0x37 | 0x60 | 0x5E | 0x79 | 0x7A | 0x87 |

<a id="table-fumwelttabelle-5a54a"></a>
### FUMWELTTABELLE_5A54A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x5F | 0x37 | 0x60 | 0x5E | 0x79 | 0x7A | 0x87 |

<a id="table-fumwelttabelle-5a56a"></a>
### FUMWELTTABELLE_5A56A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x0A | 0x0B | 0x86 | 0x5E | 0x60 | 0x02 | 0x87 |

<a id="table-fumwelttabelle-5a58a"></a>
### FUMWELTTABELLE_5A58A

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x2E | 0x5F | 0xAF | 0x5E | 0x60 | 0x87 |

<a id="table-fumwelttabelle-5a44a"></a>
### FUMWELTTABELLE_5A44A

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x4F | 0x2F | 0x7C |

<a id="table-fumwelttabelle-5a45a"></a>
### FUMWELTTABELLE_5A45A

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x50 | 0x30 | 0x7D |

<a id="table-fumwelttabelle-5027a"></a>
### FUMWELTTABELLE_5027A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x02 | 0x8A |

<a id="table-fumwelttabelle-5028a"></a>
### FUMWELTTABELLE_5028A

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x0D | 0x2D | 0x5D |

<a id="table-fumwelttabelle-5029a"></a>
### FUMWELTTABELLE_5029A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x4F | 0x2F |

<a id="table-fumwelttabelle-5030a"></a>
### FUMWELTTABELLE_5030A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x50 | 0x30 |

<a id="table-fumwelttabelle-5a76a"></a>
### FUMWELTTABELLE_5A76A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x0B | 0x3D |

<a id="table-fumwelttabelle-5054a"></a>
### FUMWELTTABELLE_5054A

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x4D | 0x4E | 0x6A | 0xE6 | 0xE7 | 0xE8 |

<a id="table-fumwelttabelle-5059a"></a>
### FUMWELTTABELLE_5059A

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x6A | 0x4D | 0x4E | 0x0A | 0x0B |

<a id="table-fumwelttabelle-5060a"></a>
### FUMWELTTABELLE_5060A

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x6F | 0xB3 | 0xB4 | 0xB5 | 0xB6 |

<a id="table-fumwelttabelle-5055a"></a>
### FUMWELTTABELLE_5055A

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0x4C | 0x67 | 0x68 |

<a id="table-fumwelttabelle-5a87d"></a>
### FUMWELTTABELLE_5A87D

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x7F | 0x80 | 0x81 | 0xAA |

<a id="table-fumwelttabelle-5056a"></a>
### FUMWELTTABELLE_5056A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x71 | 0x3D |

<a id="table-fumwelttabelle-5a5ba"></a>
### FUMWELTTABELLE_5A5BA

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x86 | 0x87 | 0xA4 | 0xA5 | 0xA6 | 0x5E | 0x02 |

<a id="table-fumwelttabelle-5a42a"></a>
### FUMWELTTABELLE_5A42A

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x8B | 0x8C | 0x2D | 0xAB | 0xAC |

<a id="table-fumwelttabelle-5031a"></a>
### FUMWELTTABELLE_5031A

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x8B | 0x8C | 0x2D | 0xAB | 0xAD |

<a id="table-fumwelttabelle-cf3ea"></a>
### FUMWELTTABELLE_CF3EA

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x51 | 0x31 | 0x32 | 0x61 | 0x62 |

<a id="table-fumwelttabelle-5061a"></a>
### FUMWELTTABELLE_5061A

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0xE6 | 0xE7 | 0xE8 |

<a id="table-fumwelttabelle-5131a"></a>
### FUMWELTTABELLE_5131A

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x8F | 0x90 | 0x93 | 0x8D | 0x91 | 0x83 |

<a id="table-fumwelttabelle-5132a"></a>
### FUMWELTTABELLE_5132A

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x8F | 0x90 | 0x93 | 0x95 | 0x91 | 0x96 |

<a id="table-fumwelttabelle-5132d"></a>
### FUMWELTTABELLE_5132D

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x92 | 0x94 |

<a id="table-fumwelttabelle-5133a"></a>
### FUMWELTTABELLE_5133A

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x90 | 0xA1 | 0xA2 | 0xA3 | 0x9F | 0xA0 |

<a id="table-fumwelttabelle-5134a"></a>
### FUMWELTTABELLE_5134A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x98 | 0x99 | 0x9A | 0x9B | 0x93 | 0x9D | 0x9E |

<a id="table-fehlertesteinlernkupplung"></a>
### FEHLERTESTEINLERNKUPPLUNG

Dimensions: 15 rows × 2 columns

| FEHLERNR | FEHLERTEXT |
| --- | --- |
| 0x00 | Systemfehler (limp home) |
| 0x01 | Kupplungs- oder Hydrauliktemperatur nicht im gültigen Bereich |
| 0x02 | Wählhebel nicht in Stellung N |
| 0x03 | Motordrehzahl nicht im gültigen Bereich |
| 0x04 | Bremspedal nicht betätigt |
| 0x05 | Fahrpedal betätigt |
| 0x06 | Fahrzeug bewegt sich |
| 0x07 | Bremsdruck zu niedrig |
| 0x10 | Adaption bis zu diesem Zeitpunkt nicht gestartet |
| 0x11 | Adaption läuft |
| 0x12 | Abbruch durch Bediener |
| 0x13 | Abbruch durch Systemfehler |
| 0x14 | Beendet aber Kisspoint nicht im gültigen Bereich |
| 0x15 | Adaption gültig |
| 0xFF | Undefiniert |

<a id="table-fumwelttabelle-5a87a"></a>
### FUMWELTTABELLE_5A87A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x01 | 0x02 |

<a id="table-fumwelttabelle-5062a1"></a>
### FUMWELTTABELLE_5062A1

Dimensions: 1 rows × 4 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR |
| --- | --- | --- | --- |
| 3 | 0xE6 | 0xE7 | 0xE8 |

<a id="table-fehlertesteinlernparksperrenmagnet"></a>
### FEHLERTESTEINLERNPARKSPERRENMAGNET

Dimensions: 8 rows × 2 columns

| FEHLERNR | FEHLERTEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Kurzschluss HS -&gt; GND oder Leitungsunterbrechung |
| 0x02 | Kurzschluss LS -&gt; GND |
| 0x04 | Wicklungsschluss |
| 0x08 | Kurzschluss HS -&gt; Ubat |
| 0x16 | Kurzschluss LS -&gt; Ubat |
| 0x64 | Unbekannter Fehler |
| 0xFF | Undefiniert |

<a id="table-fumwelttabelle-5137a"></a>
### FUMWELTTABELLE_5137A

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x02 | 0x0B | 0xB0 | 0xB1 | 0xB2 |

<a id="table-fumwelttexte01"></a>
### FUMWELTTEXTE01

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Ohne Anhänger |
| 0x01 | Mit Anhänger |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte02"></a>
### FUMWELTTEXTE02

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Pulse temp. |
| 0x01 | Pulse min. |
| 0x02 | Pulse max. |
| 0x03 | Off |
| 0x04 | Min |
| 0x05 | Max |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte03"></a>
### FUMWELTTEXTE03

Dimensions: 11 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Quellenfehler (passiv) |
| 0x01 | Unerlaubte Bewegung SST aus N |
| 0x02 | Unerlaubte Bewegung SST aus Gang |
| 0x03 | Timeout Neutral einregeln SST |
| 0x04 | Falsche Bewegungsrichtung SST |
| 0x05 | Einlegeproblem / -hängen |
| 0x06 | Auslegeproblem / -hängen |
| 0x07 | Schaltgabelbruch |
| 0x08 | Drehzahlfehler |
| 0x09 | Gangspringer |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte04"></a>
### FUMWELTTEXTE04

Dimensions: 11 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Quellenfehler (passiv) |
| 0x01 | Unerlaubte Bewegung SST aus N |
| 0x02 | Unerlaubte Bewegung SST aus Gang |
| 0x03 | Timeout Neutral einregeln SST |
| 0x04 | Falsche Bewegungsrichtung SST |
| 0x05 | Einlegeproblem / -hängen |
| 0x06 | Auslegeproblem / -hängen |
| 0x07 | Schaltgabelbruch |
| 0x08 | Drehzahlfehler |
| 0x09 | Gangspringer |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte05"></a>
### FUMWELTTEXTE05

Dimensions: 11 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Quellenfehler (passiv) |
| 0x01 | Unerlaubte Bewegung SST aus N |
| 0x02 | Unerlaubte Bewegung SST aus Gang |
| 0x03 | Timeout Neutral einregeln SST |
| 0x04 | Falsche Bewegungsrichtung SST |
| 0x05 | Einlegeproblem / -hängen |
| 0x06 | Auslegeproblem / -hängen |
| 0x07 | Schaltgabelbruch |
| 0x08 | Drehzahlfehler |
| 0x09 | Gangspringer |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte06"></a>
### FUMWELTTEXTE06

Dimensions: 11 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Quellenfehler (passiv) |
| 0x01 | Unerlaubte Bewegung SST aus N |
| 0x02 | Unerlaubte Bewegung SST aus Gang |
| 0x03 | Timeout Neutral einregeln SST |
| 0x04 | Falsche Bewegungsrichtung SST |
| 0x05 | Einlegeproblem / -hängen |
| 0x06 | Auslegeproblem / -hängen |
| 0x07 | Schaltgabelbruch |
| 0x08 | Drehzahlfehler |
| 0x09 | Gangspringer |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte07"></a>
### FUMWELTTEXTE07

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Untere elektrische Grenze unterschritten |
| 0x01 | Sensorwert OK |
| 0x02 | Obere elektrische Grenze überschritten |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte08"></a>
### FUMWELTTEXTE08

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Untere elektrische Grenze unterschritten |
| 0x01 | Sensorwert OK |
| 0x02 | Obere elektrische Grenze überschritten |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte09"></a>
### FUMWELTTEXTE09

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Überstrom/Unterspannung |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte10"></a>
### FUMWELTTEXTE10

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Überstrom/Unterspannung |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte11"></a>
### FUMWELTTEXTE11

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Kein Fehler |
| 0x01 | Überstrom/Unterspannung |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte12"></a>
### FUMWELTTEXTE12

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Fehler nicht aktiv |
| 0x01 | Fehler aktiv |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte13"></a>
### FUMWELTTEXTE13

Dimensions: 13 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0002 | Schutzziel 001 |
| 0x0004 | Schutzziel 003 |
| 0x0008 | Schutzziel 004a |
| 0x0010 | Schutzziel 006 |
| 0x0020 | Schutzziel 009a |
| 0x0040 | Schutzziel 009b |
| 0x0080 | Schutzziel 010 |
| 0x0100 | Schutzziel 013 |
| 0x0200 | Schutzziel 014 |
| 0x0400 | Schutzziel 019 |
| 0x0800 | Temic Sollwertverletzung |
| 0x1000 | Schutzziel 016 |
| 0xFFFF | Undefiniert |

<a id="table-fumwelttexte14"></a>
### FUMWELTTEXTE14

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x05 | Drive |
| 0x06 | Neutral |
| 0x07 | Reverse |
| 0x08 | Parking |
| 0x0E | Manuell |
| 0XFF | Undefiniert |

<a id="table-fumwelttexte15"></a>
### FUMWELTTEXTE15

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Anzeige P |
| 0x02 | Anzeige R |
| 0x04 | Anzeige N |
| 0x08 | Anzeige D |
| 0XFF | Undefiniert |

<a id="table-fumwelttexte16"></a>
### FUMWELTTEXTE16

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | Parking |
| 0x0100 | Reverse |
| 0x0200 | Neutral |
| 0x0300 | Drive |
| 0x0400 | Failure |
| 0x0500 | No Action |
| 0XFF00 | Undefiniert |

<a id="table-fumwelttexte17"></a>
### FUMWELTTEXTE17

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Locked |
| 0x01 | Unlocked |
| 0XFF | Undefiniert |

<a id="table-fumwelttexte18"></a>
### FUMWELTTEXTE18

Dimensions: 37 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0001 | Gang 1 |
| 0x0003 | Gang 1 und Gang 2 |
| 0x0005 | Gang 1 und Gang 3 |
| 0x0009 | Gang 1 und Gang 4 |
| 0x0011 | Gang 1 und Gang 5 |
| 0x0021 | Gang 1 und Gang 6 |
| 0x0041 | Gang 1 und Gang 7 |
| 0x0081 | Gang 1 und Gang R |
| 0x0002 | Gang 2 |
| 0x0006 | Gang 2 und Gang 3 |
| 0x000A | Gang 2 und Gang 4 |
| 0x0012 | Gang 2 und Gang 5 |
| 0x0022 | Gang 2 und Gang 6 |
| 0x0042 | Gang 2 und Gang 7 |
| 0x0082 | Gang 2 und Gang R |
| 0x0004 | Gang 3 |
| 0x000C | Gang 3 und Gang 4 |
| 0x0014 | Gang 3 und Gang 5 |
| 0x0024 | Gang 3 und Gang 6 |
| 0x0044 | Gang 3 und Gang 7 |
| 0x0084 | Gang 3 und Gang R |
| 0x0008 | Gang 4 |
| 0x0018 | Gang 4 und Gang 5 |
| 0x0028 | Gang 4 und Gang 6 |
| 0x0048 | Gang 4 und Gang 7 |
| 0x0088 | Gang 4 und Gang R |
| 0x0010 | Gang 5 |
| 0x0030 | Gang 5 und Gang 6 |
| 0x0050 | Gang 5 und Gang 7 |
| 0x0090 | Gang 5 und Gang R |
| 0x0020 | Gang 6 |
| 0x0060 | Gang 6 und Gang 7 |
| 0x00A0 | Gang 6 und Gang R |
| 0x0040 | Gang 7 |
| 0x00C0 | Gang 7 und Gang R |
| 0x0080 | Gang R |
| 0XFFFF | Undefiniert |

<a id="table-fumwelttexte19"></a>
### FUMWELTTEXTE19

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Vorwärts |
| 0x01 | Rückwärts |
| 0x07 | Ungültig |
| 0XFF | Undefiniert |

<a id="table-fumwelttexte20"></a>
### FUMWELTTEXTE20

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | SV 1 |
| 0x01 | SV 2 |
| 0x07 | SV 3 |
| 0XFF | Undefiniert |

<a id="table-fumwelttexte21"></a>
### FUMWELTTEXTE21

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | PV1 Sollwert Fehler |
| 0x02 | PV2 Sollwert Fehler |
| 0x04 | SV1 Sollwert Fehler |
| 0x08 | SV2 Sollwert Fehler |
| 0x16 | SV3 Sollwert Fehler |
| 0XFF | Undefiniert |

<a id="table-fumwelttexte22"></a>
### FUMWELTTEXTE22

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Signal Valid |
| 0x02 | Signal not Valid |
| 0XFF | Undefiniert |

<a id="table-fumwelttexte23"></a>
### FUMWELTTEXTE23

Dimensions: 11 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Pl_locked |
| 0x01 | Pl_unlocked |
| 0x02 | Pl_locking |
| 0x03 | Pl_unlocking |
| 0x04 | Pl_error |
| 0x05 | Pl_l_error |
| 0x06 | Pl_uul_error |
| 0x07 | Pl_pss_error |
| 0x08 | Pl_service |
| 0x09 | Pl_init |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte24"></a>
### FUMWELTTEXTE24

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x05 | D |
| 0x06 | N |
| 0x07 | R |
| 0x08 | P |
| 0x0E | M |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte25"></a>
### FUMWELTTEXTE25

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0001 | Sicherheitszeit Einlegen |
| 0x0002 | Halbe Sicherheitszeit Einlegen |
| 0x0004 | Sicherheitszeit Auslegen |
| 0x0008 | Sicherheitszeit Einlegen weil TG gesperrt |
| 0x000E | Sicherheitszeit Einlegen weil Tieftemperatur |
| 0xFFFF | Undefiniert |

<a id="table-fumwelttexte26"></a>
### FUMWELTTEXTE26

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | unbestromt |
| 0x02000000 | bestromt |
| 0XFFFFFFFF | Undefiniert |

<a id="table-fumwelttexte27"></a>
### FUMWELTTEXTE27

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | Auf Kupplung |
| 0x00020000 | Auf Tank |
| 0XFFFFFFFF | Undefiniert |

<a id="table-fumwelttexte28"></a>
### FUMWELTTEXTE28

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000000 | Auf Kupplung |
| 0x00000200 | Auf Tank |
| 0XFFFFFFFF | Undefiniert |

<a id="table-fumwelttexte29"></a>
### FUMWELTTEXTE29

Dimensions: 9 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000001 | Ungewollt eingefallen |
| 0x00000004 | Ungewollt ausgelegt |
| 0x00000008 | Parksperrensensorfehler |
| 0x00000044 | Druck an Kupplungen beim auslegen |
| 0x00000050 | Hängendes Absperrventil |
| 0x00000060 | Sicherheitszeit Auslegen |
| 0x00000070 | Halbe Sicherheitszeit Einlegen |
| 0x00000080 | Sicherheitszeit Einlegen |
| 0xFFFFFFFF | Undefiniert |

<a id="table-fumwelttexte30"></a>
### FUMWELTTEXTE30

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0001 | Kurzschluss Highside =&gt; Masse |
| 0x0002 | Kurzschluss Lowside =&gt; Masse oder Leitungsunterbrechung |
| 0x0004 | Wicklungsschluss oder Kurzschluss Highside =&gt; Ubat |
| 0x0008 | HS-Ubat |
| 0x0010 | Kurzschluss Lowside =&gt; Ubat |
| 0x0020 | Unbekannter Fehler =&gt; kleine Diagnose |
| 0x0040 | Erhöhter Widerstand |
| 0xFFFF | Undefiniert |

<a id="table-fumwelttabelle-5137d"></a>
### FUMWELTTABELLE_5137D

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0xE0 | 0xE1 |

<a id="table-fumwelttexte31"></a>
### FUMWELTTEXTE31

Dimensions: 11 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | Kein Fehler (SW-Bug) |
| 0x0100 | Unerlaubte Bewegung SST aus N |
| 0x0200 | Unerlaubte Bewegung SST aus Gang |
| 0x0300 | Timeout Neutral einregeln SST |
| 0x0400 | Falsche Bewegungsrichtung SST |
| 0x0500 | Einlegeproblem / -hängen |
| 0x0600 | Auslegeproblem / -hängen |
| 0x0700 | Schaltgabelbruch |
| 0x0800 | Drehzahlfehler |
| 0x0900 | Gangspringer |
| 0xFFFF | Undefiniert |

<a id="table-fumwelttexte32"></a>
### FUMWELTTEXTE32

Dimensions: 11 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | Kein Fehler (SW-Bug) |
| 0x0001 | Unerlaubte Bewegung SST aus N |
| 0x0002 | Unerlaubte Bewegung SST aus Gang |
| 0x0003 | Timeout Neutral einregeln SST |
| 0x0004 | Falsche Bewegungsrichtung SST |
| 0x0005 | Einlegeproblem / -hängen |
| 0x0006 | Auslegeproblem / -hängen |
| 0x0007 | Schaltgabelbruch |
| 0x0008 | Drehzahlfehler |
| 0x0009 | Gangspringer |
| 0xFFFF | Undefiniert |

<a id="table-fumwelttexte33"></a>
### FUMWELTTEXTE33

Dimensions: 16 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0001 | Unknown-Fault |
| 0x0002 | Shutdown by FSW |
| 0x0008 | ECC Single-Bit |
| 0x0010 | Level3-Monitoring |
| 0x0020 | Trap X3 |
| 0x0040 | Parity Error RAM |
| 0x0080 | RST by ext. Hardware |
| 0x0100 | AD-Converter Fail |
| 0x0200 | µC-Watchdog |
| 0x0400 | PCP µC |
| 0x0800 | Trap X2 |
| 0x1000 | ECC Double-Bit |
| 0x2000 | Program Flow |
| 0x4000 | ShutOff-Path Test |
| 0x8000 | Trap_X1 |
| 0xFFFF | Mehrere Zustände sind gleichzeitig aufgetreten |

<a id="table-fumwelttexte34"></a>
### FUMWELTTEXTE34

Dimensions: 4 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0001 | NMI |
| 0x0002 | RAM Test |
| 0x0003 | NMI + RAM Test |
| 0xFFFF | Zustand nicht definiert |

<a id="table-fumwelttabelle-5131d"></a>
### FUMWELTTABELLE_5131D

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x92 | 0x94 |

<a id="table-fumwelttexte35"></a>
### FUMWELTTEXTE35

Dimensions: 37 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Gang 1 |
| 0x03 | Gang 1 und Gang 2 |
| 0x05 | Gang 1 und Gang 3 |
| 0x09 | Gang 1 und Gang 4 |
| 0x11 | Gang 1 und Gang 5 |
| 0x21 | Gang 1 und Gang 6 |
| 0x41 | Gang 1 und Gang 7 |
| 0x81 | Gang 1 und Gang R |
| 0x02 | Gang 2 |
| 0x06 | Gang 2 und Gang 3 |
| 0x0A | Gang 2 und Gang 4 |
| 0x12 | Gang 2 und Gang 5 |
| 0x22 | Gang 2 und Gang 6 |
| 0x42 | Gang 2 und Gang 7 |
| 0x82 | Gang 2 und Gang R |
| 0x04 | Gang 3 |
| 0x0C | Gang 3 und Gang 4 |
| 0x14 | Gang 3 und Gang 5 |
| 0x24 | Gang 3 und Gang 6 |
| 0x44 | Gang 3 und Gang 7 |
| 0x84 | Gang 3 und Gang R |
| 0x08 | Gang 4 |
| 0x18 | Gang 4 und Gang 5 |
| 0x28 | Gang 4 und Gang 6 |
| 0x48 | Gang 4 und Gang 7 |
| 0x88 | Gang 4 und Gang R |
| 0x10 | Gang 5 |
| 0x30 | Gang 5 und Gang 6 |
| 0x50 | Gang 5 und Gang 7 |
| 0x90 | Gang 5 und Gang R |
| 0x20 | Gang 6 |
| 0x60 | Gang 6 und Gang 7 |
| 0xA0 | Gang 6 und Gang R |
| 0x40 | Gang 7 |
| 0xC0 | Gang 7 und Gang R |
| 0x80 | Gang R |
| 0XFF | Undefiniert |

<a id="table-fumwelttexte36"></a>
### FUMWELTTEXTE36

Dimensions: 9 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | Ungewollt eingefallen |
| 0x04 | Ungewollt ausgelegt |
| 0x08 | Parksperrensensorfehler |
| 0x44 | Druck an Kupplungen beim auslegen |
| 0x50 | Hängendes Absperrventil |
| 0x60 | Sicherheitszeit Auslegen |
| 0x70 | Halbe Sicherheitszeit Einlegen |
| 0x80 | Sicherheitszeit Einlegen |
| 0xFF | Undefiniert |

<a id="table-fumwelttexte37"></a>
### FUMWELTTEXTE37

Dimensions: 11 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Pl_locked |
| 0x01 | Pl_unlocked |
| 0x02 | Pl_locking |
| 0x03 | Pl_unlocking |
| 0x04 | Pl_error |
| 0x05 | Pl_l_error |
| 0x06 | Pl_uul_error |
| 0x07 | Pl_pss_error |
| 0x08 | Pl_service |
| 0x09 | Pl_init |
| 0XFF | Undefiniert |

<a id="table-fumwelttexte38"></a>
### FUMWELTTEXTE38

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0005 | D |
| 0x0006 | N |
| 0x0007 | R |
| 0x0008 | P |
| 0x000E | M |
| 0xFFFF | Undefiniert |

<a id="table-fumwelttabelle-5055d"></a>
### FUMWELTTABELLE_5055D

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0xE4 | 0xE5 |

<a id="table-fumwelttabelle-5056d"></a>
### FUMWELTTABELLE_5056D

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0xE4 | 0xE5 |

<a id="table-fumwelttexte39"></a>
### FUMWELTTEXTE39

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | unbestromt |
| 0x02 | bestromt |
| 0XFF | Undefiniert |

<a id="table-fumwelttabelle-5059d"></a>
### FUMWELTTABELLE_5059D

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0xE4 | 0xE5 |

<a id="table-fumwelttabelle-5060d"></a>
### FUMWELTTABELLE_5060D

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0xE4 | 0x6B |

<a id="table-fumwelttabelle-5054d"></a>
### FUMWELTTABELLE_5054D

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0xE4 | 0x74 |

<a id="table-fumwelttabelle-5062a"></a>
### FUMWELTTABELLE_5062A

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x4B | 0x4C | 0x59 | 0x5A |

<a id="table-fumwelttabelle-5138a"></a>
### FUMWELTTABELLE_5138A

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0x02 | 0x01 | 0x04 | 0x05 | 0x0A | 0x0B | 0x37 |

<a id="table-fumwelttabelle-5057a"></a>
### FUMWELTTABELLE_5057A

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x4D | 0x4E | 0x6A | 0xE6 | 0xE7 | 0xE8 |

<a id="table-fumwelttabelle-5057d"></a>
### FUMWELTTABELLE_5057D

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0xE4 | 0x74 |

<a id="table-fumwelttabelle-5139a"></a>
### FUMWELTTABELLE_5139A

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x4C | 0x6A | 0x4D | 0x4E | 0x0A | 0x0B |

<a id="table-fumwelttabelle-5129a"></a>
### FUMWELTTABELLE_5129A

Dimensions: 1 rows × 7 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 0x6E | 0x6F | 0xB3 | 0xB4 | 0xB5 | 0xB6 |

<a id="table-fumwelttexte40"></a>
### FUMWELTTEXTE40

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0001 | Kurzschluss Highside =&gt; Masse |
| 0x0002 | Kurzschluss Lowside =&gt; Masse oder Leitungsunterbrechung |
| 0x0004 | Wicklungsschluss oder Kurzschluss Highside =&gt; Ubat |
| 0x0008 | HS-Ubat |
| 0x0010 | Kurzschluss Lowside =&gt; Ubat |
| 0x0020 | Unbekannter Fehler =&gt; kleine Diagnose |
| 0x0040 | Erhöhter Widerstand |
| 0xFFFF | Undefiniert |

<a id="table-fumwelttabelle-5a46a"></a>
### FUMWELTTABELLE_5A46A

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x3C | 0x5B | 0x17 | 0x45 |

<a id="table-fumwelttabelle-5a47a"></a>
### FUMWELTTABELLE_5A47A

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x3C | 0x5C | 0x18 | 0x46 |

<a id="table-fumwelttabelle-5a48a"></a>
### FUMWELTTABELLE_5A48A

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x5D | 0x0A | 0x0B | 0x47 |

<a id="table-fumwelttabelle-5a4ba"></a>
### FUMWELTTABELLE_5A4BA

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x01 | 0x3A | 0x59 | 0x97 | 0x43 |

<a id="table-fumwelttabelle-5a4ca"></a>
### FUMWELTTABELLE_5A4CA

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x01 | 0x3B | 0x5A | 0x98 | 0x44 |

<a id="table-fumwelttabelle-5a55a"></a>
### FUMWELTTABELLE_5A55A

Dimensions: 1 rows × 6 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR |
| --- | --- | --- | --- | --- | --- |
| 5 | 0x3B | 0x5E | 0x0A | 0x0B | 0x48 |

<a id="table-fumwelttabelle-5021a"></a>
### FUMWELTTABELLE_5021A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x01 | 0x3A |

<a id="table-fumwelttabelle-5022a"></a>
### FUMWELTTABELLE_5022A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x01 | 0x3A |

<a id="table-fumwelttabelle-5023a"></a>
### FUMWELTTABELLE_5023A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x01 | 0x17 |

<a id="table-fumwelttabelle-5024a"></a>
### FUMWELTTABELLE_5024A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x01 | 0x17 |

<a id="table-fumwelttabelle-5a84"></a>
### FUMWELTTABELLE_5A84

Dimensions: 1 rows × 8 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR | UW5_NR | UW6_NR | UW7_NR |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 0xF8 | 0xF9 | 0xFA | 0xFB | 0xFC | 0xFD | 0xFE |

<a id="table-fumwelttexte41"></a>
### FUMWELTTEXTE41

Dimensions: 9 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00000001 | Checksumme i.O. |
| 0x00000002 | Checksumme n.i.O. und Default-Werte eingespielt |
| 0x00000100 | Checksumme i.O. |
| 0x00000200 | Checksumme n.i.O. und Default-Werte eingespielt |
| 0x00010000 | Checksumme i.O. |
| 0x00020000 | Checksumme n.i.O. und Default-Werte eingespielt |
| 0x01000000 | Checksumme i.O. |
| 0x02000000 | Checksumme n.i.O. und Default-Werte eingespielt |
| 0XFFFFFFFF | Undefiniert |

<a id="table-fumwelttexte42"></a>
### FUMWELTTEXTE42

Dimensions: 3 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Checksumme n.i.O., keine Defaultwerte vorhanden |
| 0x01 | Checksumme i.O. |
| 0XFF | Undefiniert |

<a id="table-fumwelttabelle-5a88a"></a>
### FUMWELTTABELLE_5A88A

Dimensions: 1 rows × 3 columns

| UW_ANZ | UW1_NR | UW2_NR |
| --- | --- | --- |
| 2 | 0x01 | 0x02 |

<a id="table-fumwelttabelle-5a88d"></a>
### FUMWELTTABELLE_5A88D

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0x7F | 0x80 | 0x81 | 0xAA |

<a id="table-fumwelttabelle-cf29a"></a>
### FUMWELTTABELLE_CF29A

Dimensions: 1 rows × 5 columns

| UW_ANZ | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 4 | 0xBB | 0xBC | 0xBD | 0xBE |

<a id="table-fumwelttexte18n"></a>
### FUMWELTTEXTE18N

Dimensions: 257 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x0000 | 0 |
| 0x0001 | 1 |
| 0x0002 | 2 |
| 0x0003 | 3 |
| 0x0004 | 4 |
| 0x0005 | 5 |
| 0x0006 | 6 |
| 0x0007 | 7 |
| 0x0008 | 8 |
| 0x0009 | 9 |
| 0x000A | 10 |
| 0x000B | 11 |
| 0x000C | 12 |
| 0x000D | 13 |
| 0x000E | 14 |
| 0x000F | 15 |
| 0x0010 | 16 |
| 0x0011 | 17 |
| 0x0012 | 18 |
| 0x0013 | 19 |
| 0x0014 | 20 |
| 0x0015 | 21 |
| 0x0016 | 22 |
| 0x0017 | 23 |
| 0x0018 | 24 |
| 0x0019 | 25 |
| 0x001A | 26 |
| 0x001B | 27 |
| 0x001C | 28 |
| 0x001D | 29 |
| 0x001E | 30 |
| 0x001F | 31 |
| 0x0020 | 32 |
| 0x0021 | 33 |
| 0x0022 | 34 |
| 0x0023 | 35 |
| 0x0024 | 36 |
| 0x0025 | 37 |
| 0x0026 | 38 |
| 0x0027 | 39 |
| 0x0028 | 40 |
| 0x0029 | 41 |
| 0x002A | 42 |
| 0x002B | 43 |
| 0x002C | 44 |
| 0x002D | 45 |
| 0x002E | 46 |
| 0x002F | 47 |
| 0x0030 | 48 |
| 0x0031 | 49 |
| 0x0032 | 50 |
| 0x0033 | 51 |
| 0x0034 | 52 |
| 0x0035 | 53 |
| 0x0036 | 54 |
| 0x0037 | 55 |
| 0x0038 | 56 |
| 0x0039 | 57 |
| 0x003A | 58 |
| 0x003B | 59 |
| 0x003C | 60 |
| 0x003D | 61 |
| 0x003E | 62 |
| 0x003F | 63 |
| 0x0040 | 64 |
| 0x0041 | 65 |
| 0x0042 | 66 |
| 0x0043 | 67 |
| 0x0044 | 68 |
| 0x0045 | 69 |
| 0x0046 | 70 |
| 0x0047 | 71 |
| 0x0048 | 72 |
| 0x0049 | 73 |
| 0x004A | 74 |
| 0x004B | 75 |
| 0x004C | 76 |
| 0x004D | 77 |
| 0x004E | 78 |
| 0x004F | 79 |
| 0x0050 | 80 |
| 0x0051 | 81 |
| 0x0052 | 82 |
| 0x0053 | 83 |
| 0x0054 | 84 |
| 0x0055 | 85 |
| 0x0056 | 86 |
| 0x0057 | 87 |
| 0x0058 | 88 |
| 0x0059 | 89 |
| 0x005A | 90 |
| 0x005B | 91 |
| 0x005C | 92 |
| 0x005D | 93 |
| 0x005E | 94 |
| 0x005F | 95 |
| 0x0060 | 96 |
| 0x0061 | 97 |
| 0x0062 | 98 |
| 0x0063 | 99 |
| 0x0064 | 100 |
| 0x0065 | 101 |
| 0x0066 | 102 |
| 0x0067 | 103 |
| 0x0068 | 104 |
| 0x0069 | 105 |
| 0x006A | 106 |
| 0x006B | 107 |
| 0x006C | 108 |
| 0x006D | 109 |
| 0x006E | 110 |
| 0x006F | 111 |
| 0x0070 | 112 |
| 0x0071 | 113 |
| 0x0072 | 114 |
| 0x0073 | 115 |
| 0x0074 | 116 |
| 0x0075 | 117 |
| 0x0076 | 118 |
| 0x0077 | 119 |
| 0x0078 | 120 |
| 0x0079 | 121 |
| 0x007A | 122 |
| 0x007B | 123 |
| 0x007C | 124 |
| 0x007D | 125 |
| 0x007E | 126 |
| 0x007F | 127 |
| 0x0080 | 128 |
| 0x0081 | 129 |
| 0x0082 | 130 |
| 0x0083 | 131 |
| 0x0084 | 132 |
| 0x0085 | 133 |
| 0x0086 | 134 |
| 0x0087 | 135 |
| 0x0088 | 136 |
| 0x0089 | 137 |
| 0x008A | 138 |
| 0x008B | 139 |
| 0x008C | 140 |
| 0x008D | 141 |
| 0x008E | 142 |
| 0x008F | 143 |
| 0x0090 | 144 |
| 0x0091 | 145 |
| 0x0092 | 146 |
| 0x0093 | 147 |
| 0x0094 | 148 |
| 0x0095 | 149 |
| 0x0096 | 150 |
| 0x0097 | 151 |
| 0x0098 | 152 |
| 0x0099 | 153 |
| 0x009A | 154 |
| 0x009B | 155 |
| 0x009C | 156 |
| 0x009D | 157 |
| 0x009E | 158 |
| 0x009F | 159 |
| 0x00A0 | 160 |
| 0x00A1 | 161 |
| 0x00A2 | 162 |
| 0x00A3 | 163 |
| 0x00A4 | 164 |
| 0x00A5 | 165 |
| 0x00A6 | 166 |
| 0x00A7 | 167 |
| 0x00A8 | 168 |
| 0x00A9 | 169 |
| 0x00AA | 170 |
| 0x00AB | 171 |
| 0x00AC | 172 |
| 0x00AD | 173 |
| 0x00AE | 174 |
| 0x00AF | 175 |
| 0x00B0 | 176 |
| 0x00B1 | 177 |
| 0x00B2 | 178 |
| 0x00B3 | 179 |
| 0x00B4 | 180 |
| 0x00B5 | 181 |
| 0x00B6 | 182 |
| 0x00B7 | 183 |
| 0x00B8 | 184 |
| 0x00B9 | 185 |
| 0x00BA | 186 |
| 0x00BB | 187 |
| 0x00BC | 188 |
| 0x00BD | 189 |
| 0x00BE | 190 |
| 0x00BF | 191 |
| 0x00C0 | 192 |
| 0x00C1 | 193 |
| 0x00C2 | 194 |
| 0x00C3 | 195 |
| 0x00C4 | 196 |
| 0x00C5 | 197 |
| 0x00C6 | 198 |
| 0x00C7 | 199 |
| 0x00C8 | 200 |
| 0x00C9 | 201 |
| 0x00CA | 202 |
| 0x00CB | 203 |
| 0x00CC | 204 |
| 0x00CD | 205 |
| 0x00CE | 206 |
| 0x00CF | 207 |
| 0x00D0 | 208 |
| 0x00D1 | 209 |
| 0x00D2 | 210 |
| 0x00D3 | 211 |
| 0x00D4 | 212 |
| 0x00D5 | 213 |
| 0x00D6 | 214 |
| 0x00D7 | 215 |
| 0x00D8 | 216 |
| 0x00D9 | 217 |
| 0x00DA | 218 |
| 0x00DB | 219 |
| 0x00DC | 220 |
| 0x00DD | 221 |
| 0x00DE | 222 |
| 0x00DF | 223 |
| 0x00E0 | 224 |
| 0x00E1 | 225 |
| 0x00E2 | 226 |
| 0x00E3 | 227 |
| 0x00E4 | 228 |
| 0x00E5 | 229 |
| 0x00E6 | 230 |
| 0x00E7 | 231 |
| 0x00E8 | 232 |
| 0x00E9 | 233 |
| 0x00EA | 234 |
| 0x00EB | 235 |
| 0x00EC | 236 |
| 0x00ED | 237 |
| 0x00EE | 238 |
| 0x00EF | 239 |
| 0x00F0 | 240 |
| 0x00F1 | 241 |
| 0x00F2 | 242 |
| 0x00F3 | 243 |
| 0x00F4 | 244 |
| 0x00F5 | 245 |
| 0x00F6 | 246 |
| 0x00F7 | 247 |
| 0x00F8 | 248 |
| 0x00F9 | 249 |
| 0x00FA | 250 |
| 0x00FB | 251 |
| 0x00FC | 252 |
| 0x00FD | 253 |
| 0x00FE | 254 |
| 0x00FF | 255 |
| 0xFFFF | Undefiniert |

<a id="table-fumwelttexte35n"></a>
### FUMWELTTEXTE35N

Dimensions: 256 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | 0 |
| 0x01 | 1 |
| 0x02 | 2 |
| 0x03 | 3 |
| 0x04 | 4 |
| 0x05 | 5 |
| 0x06 | 6 |
| 0x07 | 7 |
| 0x08 | 8 |
| 0x09 | 9 |
| 0x0A | 10 |
| 0x0B | 11 |
| 0x0C | 12 |
| 0x0D | 13 |
| 0x0E | 14 |
| 0x0F | 15 |
| 0x10 | 16 |
| 0x11 | 17 |
| 0x12 | 18 |
| 0x13 | 19 |
| 0x14 | 20 |
| 0x15 | 21 |
| 0x16 | 22 |
| 0x17 | 23 |
| 0x18 | 24 |
| 0x19 | 25 |
| 0x1A | 26 |
| 0x1B | 27 |
| 0x1C | 28 |
| 0x1D | 29 |
| 0x1E | 30 |
| 0x1F | 31 |
| 0x20 | 32 |
| 0x21 | 33 |
| 0x22 | 34 |
| 0x23 | 35 |
| 0x24 | 36 |
| 0x25 | 37 |
| 0x26 | 38 |
| 0x27 | 39 |
| 0x28 | 40 |
| 0x29 | 41 |
| 0x2A | 42 |
| 0x2B | 43 |
| 0x2C | 44 |
| 0x2D | 45 |
| 0x2E | 46 |
| 0x2F | 47 |
| 0x30 | 48 |
| 0x31 | 49 |
| 0x32 | 50 |
| 0x33 | 51 |
| 0x34 | 52 |
| 0x35 | 53 |
| 0x36 | 54 |
| 0x37 | 55 |
| 0x38 | 56 |
| 0x39 | 57 |
| 0x3A | 58 |
| 0x3B | 59 |
| 0x3C | 60 |
| 0x3D | 61 |
| 0x3E | 62 |
| 0x3F | 63 |
| 0x40 | 64 |
| 0x41 | 65 |
| 0x42 | 66 |
| 0x43 | 67 |
| 0x44 | 68 |
| 0x45 | 69 |
| 0x46 | 70 |
| 0x47 | 71 |
| 0x48 | 72 |
| 0x49 | 73 |
| 0x4A | 74 |
| 0x4B | 75 |
| 0x4C | 76 |
| 0x4D | 77 |
| 0x4E | 78 |
| 0x4F | 79 |
| 0x50 | 80 |
| 0x51 | 81 |
| 0x52 | 82 |
| 0x53 | 83 |
| 0x54 | 84 |
| 0x55 | 85 |
| 0x56 | 86 |
| 0x57 | 87 |
| 0x58 | 88 |
| 0x59 | 89 |
| 0x5A | 90 |
| 0x5B | 91 |
| 0x5C | 92 |
| 0x5D | 93 |
| 0x5E | 94 |
| 0x5F | 95 |
| 0x60 | 96 |
| 0x61 | 97 |
| 0x62 | 98 |
| 0x63 | 99 |
| 0x64 | 100 |
| 0x65 | 101 |
| 0x66 | 102 |
| 0x67 | 103 |
| 0x68 | 104 |
| 0x69 | 105 |
| 0x6A | 106 |
| 0x6B | 107 |
| 0x6C | 108 |
| 0x6D | 109 |
| 0x6E | 110 |
| 0x6F | 111 |
| 0x70 | 112 |
| 0x71 | 113 |
| 0x72 | 114 |
| 0x73 | 115 |
| 0x74 | 116 |
| 0x75 | 117 |
| 0x76 | 118 |
| 0x77 | 119 |
| 0x78 | 120 |
| 0x79 | 121 |
| 0x7A | 122 |
| 0x7B | 123 |
| 0x7C | 124 |
| 0x7D | 125 |
| 0x7E | 126 |
| 0x7F | 127 |
| 0x80 | 128 |
| 0x81 | 129 |
| 0x82 | 130 |
| 0x83 | 131 |
| 0x84 | 132 |
| 0x85 | 133 |
| 0x86 | 134 |
| 0x87 | 135 |
| 0x88 | 136 |
| 0x89 | 137 |
| 0x8A | 138 |
| 0x8B | 139 |
| 0x8C | 140 |
| 0x8D | 141 |
| 0x8E | 142 |
| 0x8F | 143 |
| 0x90 | 144 |
| 0x91 | 145 |
| 0x92 | 146 |
| 0x93 | 147 |
| 0x94 | 148 |
| 0x95 | 149 |
| 0x96 | 150 |
| 0x97 | 151 |
| 0x98 | 152 |
| 0x99 | 153 |
| 0x9A | 154 |
| 0x9B | 155 |
| 0x9C | 156 |
| 0x9D | 157 |
| 0x9E | 158 |
| 0x9F | 159 |
| 0xA0 | 160 |
| 0xA1 | 161 |
| 0xA2 | 162 |
| 0xA3 | 163 |
| 0xA4 | 164 |
| 0xA5 | 165 |
| 0xA6 | 166 |
| 0xA7 | 167 |
| 0xA8 | 168 |
| 0xA9 | 169 |
| 0xAA | 170 |
| 0xAB | 171 |
| 0xAC | 172 |
| 0xAD | 173 |
| 0xAE | 174 |
| 0xAF | 175 |
| 0xB0 | 176 |
| 0xB1 | 177 |
| 0xB2 | 178 |
| 0xB3 | 179 |
| 0xB4 | 180 |
| 0xB5 | 181 |
| 0xB6 | 182 |
| 0xB7 | 183 |
| 0xB8 | 184 |
| 0xB9 | 185 |
| 0xBA | 186 |
| 0xBB | 187 |
| 0xBC | 188 |
| 0xBD | 189 |
| 0xBE | 190 |
| 0xBF | 191 |
| 0xC0 | 192 |
| 0xC1 | 193 |
| 0xC2 | 194 |
| 0xC3 | 195 |
| 0xC4 | 196 |
| 0xC5 | 197 |
| 0xC6 | 198 |
| 0xC7 | 199 |
| 0xC8 | 200 |
| 0xC9 | 201 |
| 0xCA | 202 |
| 0xCB | 203 |
| 0xCC | 204 |
| 0xCD | 205 |
| 0xCE | 206 |
| 0xCF | 207 |
| 0xD0 | 208 |
| 0xD1 | 209 |
| 0xD2 | 210 |
| 0xD3 | 211 |
| 0xD4 | 212 |
| 0xD5 | 213 |
| 0xD6 | 214 |
| 0xD7 | 215 |
| 0xD8 | 216 |
| 0xD9 | 217 |
| 0xDA | 218 |
| 0xDB | 219 |
| 0xDC | 220 |
| 0xDD | 221 |
| 0xDE | 222 |
| 0xDF | 223 |
| 0xE0 | 224 |
| 0xE1 | 225 |
| 0xE2 | 226 |
| 0xE3 | 227 |
| 0xE4 | 228 |
| 0xE5 | 229 |
| 0xE6 | 230 |
| 0xE7 | 231 |
| 0xE8 | 232 |
| 0xE9 | 233 |
| 0xEA | 234 |
| 0xEB | 235 |
| 0xEC | 236 |
| 0xED | 237 |
| 0xEE | 238 |
| 0xEF | 239 |
| 0xF0 | 240 |
| 0xF1 | 241 |
| 0xF2 | 242 |
| 0xF3 | 243 |
| 0xF4 | 244 |
| 0xF5 | 245 |
| 0xF6 | 246 |
| 0xF7 | 247 |
| 0xF8 | 248 |
| 0xF9 | 249 |
| 0xFA | 250 |
| 0xFB | 251 |
| 0xFC | 252 |
| 0xFD | 253 |
| 0xFE | 254 |
| 0xFF | 255 |

<a id="table-statusklackern"></a>
### STATUSKLACKERN

Dimensions: 3 rows × 2 columns

| STATUSNR | STATUSTEXT |
| --- | --- |
| 0x00 | Anti Leerlaufklackern  nicht aktiv |
| 0x01 | Anti Leerlaufklackern  aktiv |
| 0xFF | Undefiniert |
