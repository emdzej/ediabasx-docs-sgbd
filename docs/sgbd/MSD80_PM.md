# MSD80_PM.prg

- Jobs: [367](#jobs)
- Tables: [139](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MSD80 fuer N43 EWS4 oder CAS  |
| ORIGIN | IAV EA-53 Rigl |
| REVISION | 0.001 |
| AUTHOR | IAV Gimeno EA-53 |
| COMMENT | SGBD für MSD80 C-Muster mit SW 4RCY400S |
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
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen KWP2000: $14 ClearDiagnosticInformation Modus  : Default
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels KWP2000: $22 ReadDataByCommonIdentifier $1000 TestStamp Modus  : Default
- [NORMALER_DATENVERKEHR](#job-normaler-datenverkehr) - Sperren bzw. Freigeben des normalen Datenverkehrs KWP2000: $28 DisableNormalMessageTransmission KWP2000: $29 EnableNormalMessageTransmission Modus  : Default
- [DIAGNOSE_AUFRECHT](#job-diagnose-aufrecht) - Diagnosemode des SG aufrecht erhalten KWP2000: $3E TesterPresent Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [ENERGIESPARMODE](#job-energiesparmode) - Einstellen des Energiesparmodes KWP2000: $31 StartRoutineByLocalIdentifier $0C ControlEnergySavingMode Modus  : Default
- [SENSOREN_ANZAHL_LESEN](#job-sensoren-anzahl-lesen) - Anzahl der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers Modus  : Default
- [SENSOREN_IDENT_LESEN](#job-sensoren-ident-lesen) - Identifikation der intelligenten Subbussensoren lesen KWP2000: $22 ReadDataByCommonIdentifier $1600 IdentifyNumberofSubbusMembers $16xx SubbusMemberSerialNumber Modus  : Default
- [STATUS_MESSWERTBLOCK_LESEN](#job-status-messwertblock-lesen) - Lesen eines Messwertblockes Es muss immer das BlockSchreibenFlag und mindestens ein MESSWERT uebergeben werden. KWP2000: $2C DynamicallyDefinedLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier $04 ClearDynamicallyDefinedLocalIdentifier KWP2000: $2C DynamicallyDefinedLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier $02 DefineByCommonIdentifier KWP2000: $21 ReadDataByLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier Modus  : Default
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
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [AIF_SCHREIBEN](#job-aif-schreiben) - Schreiben des Anwender Informations Feldes Standard Flashjob KWP 2000: $3D WriteMemoryByAddress Modus   : Default
- [FLASH_SCHREIBEN_XXL](#job-flash-schreiben-xxl) - 0x36 FLASH_SCHREIBEN_XXL Flash Daten schreiben XXL-Format, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [FLASH_SCHREIBEN_ADRESSE_4BYTE](#job-flash-schreiben-adresse-4byte) - 0x34 FLASH_SCHREIBEN_ADRESSE_4BYTE Flash Daten schreiben, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [FLASH_LOESCHEN_4BYTE](#job-flash-loeschen-4byte) - 0x3102 FLASH_LOESCHEN_4BYTE Flash löschen, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [FLASH_SCHREIBEN_ENDE_4BYTE](#job-flash-schreiben-ende-4byte) - 0x37 FLASH_SCHREIBEN_ENDE_4BYTE Flashprogrammierung abschliessen, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_BZEINFO](#job-status-bzeinfo) - 0x22401A _STATUS_BZEINFO Infospeicher Batterie Zustands Erkennung (BZE) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_GENINFO](#job-status-geninfo) - 0x22401B _STATUS_GENINFO Infospeicher Generatordiagnose erweitert auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_IGRINFO](#job-status-igrinfo) - 0x224016 _STATUS_IGRINFO Infospeicher Intelligente Generator Regelung (IGR) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_LEMINFO](#job-status-leminfo) - 0x224017 _STATUS_LEMINFO Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_MSAINFO](#job-status-msainfo) - 0x224018 _STATUS_MSAINFO Infospeicher Motor-Start/Stop Automatik (MSA) auslesen (nur 4-Zylinder-N43  nicht 6-Zylinder-N53/N54) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_UEBERDREHZAHL](#job-status-ueberdrehzahl) - 0x225FF6 _STATUS_UEBERDREHZAHL Ueberdrehzahlspeicherung (Ueberdrehsicherung) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_UEBERTEMPERATUR](#job-status-uebertemperatur) - 0x225FF3 _STATUS_UEBERTEMPERATUR Uebertemperatursicherung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_VERBREDINFO](#job-status-verbredinfo) - 0x22401D _STATUS_VERBREDINFO Verbraucherreduzierungsspeicher auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STEUERN_UEBERDREHZAHL_RESET](#job-steuern-ueberdrehzahl-reset) - 0x2E5FF604 _STEUERN_UEBERDREHZAHL_RESET Ueberdrehzahlspeicherung (Ueberdrehsicherung) loeschen Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [_STEUERN_UEBERTEMPERATUR_RESET](#job-steuern-uebertemperatur-reset) - 0x2E5FF304 _STEUERN_UEBERTEMPERATUR_RESET Uebertemperatursicherung loeschen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [ECU_CONFIG](#job-ecu-config) - 0x225FF2 ECU_CONFIG Variante auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [ECU_CONFIG_RESET](#job-ecu-config-reset) - 0x2E5FF204 ECU_CONFIG_RESET Variante loeschen Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [HS_LOESCHEN](#job-hs-loeschen) - 0x3103 HS_LOESCHEN Historyspeicher loeschen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [INNENTEMP_LESEN](#job-innentemp-lesen) - 0x301001 INNENTEMP_LESEN Steuergeraete-Innentemperatur auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [RESET_CRU_OFF](#job-reset-cru-off) - 0x31F4 RESET_CRU_OFF Bedingungen fuer reversible und irreversible Tempomatabschaltung ruecksetzen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [START_SYSTEMCHECK_DMTL](#job-start-systemcheck-dmtl) - 0x31DA START_SYSTEMCHECK_DMTL Ansteuern Diagnosefunktion DMTL Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [START_SYSTEMCHECK_EVAUSBL](#job-start-systemcheck-evausbl) - 0x3125 START_SYSTEMCHECK_EVAUSBL Ansteuern Diagnosefunktion Einspritzventilausblendung Aktivierung: Klemme 15 = EIN UND Motorstatus = (Leerlauf ODER Teillast) UND Drehzahl &lt; 3000 1/min Activation: LV_IGK = 1 UND STATE_ENG = (IS ODER PL) UND N &lt; C_N_MAX_KWP
- [START_SYSTEMCHECK_GEN](#job-start-systemcheck-gen) - 0x312A START_SYSTEMCHECK_GEN Diagnosefunktion Generatortest Aktivierung: Drehzahl &lt;&gt; 0 1/min UND gemessene Spannung in Motorsteuerung &lt; gemessene Spannung am Generator UND Auslastungsgrad Generator &lt; K_DFSCHWGENTEST UND Generatorfehler vorhanden = 0 Activation: N &lt;&gt; 0 UND UB &lt; U_GEN UND DFSIGGEN &lt; K_DFSCHWGENTEST UND GENIUTESTERR = 0
- [START_SYSTEMCHECK_GLF](#job-start-systemcheck-glf) - 0x31D5 START_SYSTEMCHECK_GLF Ansteuern Gesteuerte Luftfuehrung Systemcheck Aktivierung: Testeransteuerung obere Luftklappe = AUS UND Testeransteuerung untere Luftklappe = AUS UND Batteriezustand in Ordnung = JA UND Startverriegelung des Klappentests = AUS Activation: LV_ECRAS_UP_EXT_ADJ = 0 UND LV_ECRAS_DOWN_EXT_ADJ = 0 UND LV_CDN_VB_MIN_DIAG = 1 UND LV_ECRAS_EOL_INH = 0
- [START_SYSTEMCHECK_IGR_AUS](#job-start-systemcheck-igr-aus) - 0x31F7 START_SYSTEMCHECK_IGR_AUS Ansteuern Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [START_SYSTEMCHECK_L_REGELUNG_AUS](#job-start-systemcheck-l-regelung-aus) - 0x31D9 START_SYSTEMCHECK_L_REGELUNG_AUS Ansteuern Lambdaregelung ausschalten Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [START_SYSTEMCHECK_L_SONDE](#job-start-systemcheck-l-sonde) - 0x31DF START_SYSTEMCHECK_L_SONDE Ansteuern Diagnosefunktion vertauschte Lambdasonden Aktivierung: Klemme 15 = EIN UND Leerlauf UND Motortemperatur &gt; 77 Grad C UND Abgastemperatur[i] &gt; -48 Grad C UND Lambdasondensignal[i] = EIN UND Bereitschaft Lambdasonde hinter Katalsyator Bank[i] rueckgesetzt = EIN UND Status Lambdasondenheizung vor Katalysator Bank[i] = LSH_POW_CTL UND Status Lambdasondenheizung hinter Katalysator Bank[i] = LSH_POW_CTL UND Startverriegelung Lambdasonden aus Signalplausibilitaetstest Bank[i] = AUS (i = 1 FUER Bank 1, i = 2 FUER Bank 2) Activation: LV_IGK = 1 UND LV_IS = 1 UND TCO &gt; C_TCO_MIN_VLS_EOL UND TEG_CAT_DOWN_MDL[i] &gt; C_TEG_CAT_DOWN_EOL UND LV_LAMB_LS_UP_VLD[i] = 1 UND LV_LS_DOWN_READY[i] = 1 UND STATE_LSH_UP[i] = LSH_POW_CTL UND STATE_LSH_DOWN[i] = LSH_POW_CTL UND LV_DIAG_ACT_INH_LS_UP_DOWN[i] = 0 (i = 1 FUER Bank 1, i = 2 FUER Bank 2)
- [START_SYSTEMCHECK_LLERH](#job-start-systemcheck-llerh) - 0x3126 START_SYSTEMCHECK_LLERH Ansteuern Diagnosefunktion Leerlauf-Erhoehung Aktivierung: Klemme 15 = EIN UND Motorstatus = (Leerlauf ODER Teillast) UND Drehzahl &lt; 3000 1/min UND Ganginfo = 0 UND Geschwindigkeit &lt; 5 km/h UND (Kupplungsschalter = AUS FUER Automatikgetriebe = AUS ODER SMG_Steuergeraet = AUS) UND (Bremsschalter = AUS FUER SMG_Steuergeraet = EIN) Activation: LV_IGK = 1 UND STATE_ENG = (IS ODER PL) UND N &lt; C_N_MAX_KWP UND GEAR_INFO = 0h UND VS &lt;= C_VS_MAX_KWP UND (LV_CS = 0 Fuer LV_AT = 0 UND LV_VAR_AMT = 0) UND (LV_BRAKE_DET = 0 FUER LV_VAR_AMT = 1)
- [START_SYSTEMCHECK_ODR](#job-start-systemcheck-odr) - 0x312C START_SYSTEMCHECK_ODR Diagnosefunktion Oeldruckregelung Aktivierung: Leerlauf Activation: LV_IS = 1
- [START_SYSTEMCHECK_TEV_FUNC](#job-start-systemcheck-tev-func) - 0x3122 START_SYSTEMCHECK_TEV_FUNC Ansteuern Diagnosefunktion Tankentlueftungsventil Aktivierung: Klemme 15 = EIN UND Phase Motorstart beendet = EIN UND Funktionscheck TEV = EIN UND Geschwindigkeit = 0 km/h UND LV_MAF_SP_TQI_DYW_DIAGCPS = 1 UND (Betriebsart TEV = 1 ODER Betriebsart TEV = 2) UND Fehlerspeichereintrag TEV = AUS Activation: LV_IGK = 1 UND LV_ST_END = 1 UND LV_INH_DIAGCPS = 0 UND VS = 0 UND LV_MAF_SP_TQI_DYW_DIAGCPS = 1 UND (OPM_AV_DIAGCPS = 1 ODER OPM_AV_DIAGCPS = 2) UND LV_ERR_DIAGCPS = 0
- [STATUS_ADAPTION_DK](#job-status-adaption-dk) - 0x224008 STATUS_ADAPTION_DK Drosselklappenadaptionswerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_ADAPTION_GEMISCH](#job-status-adaption-gemisch) - 0x22400A STATUS_ADAPTION_GEMISCH Gemischadaptionswerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_AGK](#job-status-agk) - 0x30C101 STATUS_AGK Abgasklappe auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_AGR](#job-status-agr) - 0x30BE01 STATUS_AGR AbgasRueckfuehr (AGR) Ventil auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - 0x300A01 STATUS_AN_LUFTTEMPERATUR Ansauglufttemperatur 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_ANWS](#job-status-anws) - 0x30EE01 STATUS_ANWS Vanos Auslass Ventil auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_BETRIEBSART](#job-status-betriebsart) - 0x225FF8 STATUS_BETRIEBSART Betriebsarten auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_BLS](#job-status-bls) - 0x300201 STATUS_BLS Bremslichtschalter auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_BLTS](#job-status-blts) - 0x300301 STATUS_BLTS Bremslichttestschalter auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_BUDF](#job-status-budf) - 0x304001 STATUS_BUDF Bremsunterdrucksensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_CODIERUNG_BZE](#job-status-codierung-bze) - 0x223230 STATUS_CODIERUNG_BZE Codierung fuer BZE (Batterie Zustands Erkennung) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_CODIERUNG_IGR](#job-status-codierung-igr) - 0x223210 STATUS_CODIERUNG_IGR Codierung fuer IGR (Intelligente Generator-Regelung) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_CODIERUNG_KAT](#job-status-codierung-kat) - 0x223001 STATUS_CODIERUNG_KAT Codierung fuer Katalysator auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_CODIERUNG_LEISTUNGSSTUFE](#job-status-codierung-leistungsstufe) - 0x223020 STATUS_CODIERUNG_LEISTUNGSSTUFE Codierung fuer Leistungsstufe auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_CODIERUNG_MIL](#job-status-codierung-mil) - 0x223000 STATUS_CODIERUNG_MIL Codierung fuer MIL (Malfunction Indication Lamp) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_CODIERUNG_OEL](#job-status-codierung-oel) - 0x223200 STATUS_CODIERUNG_OEL Codierung fuer Oelwechselintervall auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_CODIERUNG_PROTOKOLL](#job-status-codierung-protokoll) - 0x223030 STATUS_CODIERUNG_PROTOKOLL Codierung Protokoll auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_CODIERUNG_SPA](#job-status-codierung-spa) - 0x223220 STATUS_CODIERUNG_SPA Codierung fuer SPA (Schaltpunktanzeige) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_CODIERUNG_VMAX](#job-status-codierung-vmax) - 0x223010 STATUS_CODIERUNG_VMAX Codierung fuer maximale Geschwindigkeit auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_CODIERUNG_XENON](#job-status-codierung-xenon) - 0x223211 STATUS_CODIERUNG_XENON Codierung fuer Xenon-Lichtverbau auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DESULFATISIERUNG](#job-status-desulfatisierung) - 0x332D STATUS_DESULFATISIERUNG Auslesen Desulfatisierung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DFMONITOR](#job-status-dfmonitor) - 0x224001 STATUS_DFMONITOR Batterieladezustand auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DIGITAL_0](#job-status-digital-0) - 0x224007 STATUS_DIGITAL_0 Status Schaltzustaende 0 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DIGITAL_1](#job-status-digital-1) - 0x224002 STATUS_DIGITAL_1 Status Schaltzustaende Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DISA](#job-status-disa) - 0x30C601 STATUS_DISA Variable Sauganlage (DISA) Klappe auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DISA2](#job-status-disa2) - 0x30AE01 STATUS_DISA2 Variable Sauganlage (DISA) Klappe2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DKH](#job-status-dkh) - 0x309E01 STATUS_DKH Drosselklappenbeheizung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DKP_VOLT](#job-status-dkp-volt) - 0x302A01 STATUS_DKP_VOLT Drosselklappe auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DMTL_HEIZUNG](#job-status-dmtl-heizung) - 0x30CE01 STATUS_DMTL_HEIZUNG Diagnosemodul-Tank Leckage Heizung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DMTL_P](#job-status-dmtl-p) - 0x30CC01 STATUS_DMTL_P Diagnosemodul-Tank Leckage Pumpe auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_DMTL_V](#job-status-dmtl-v) - 0x30CD01 STATUS_DMTL_V Diagnosemodul-Tank Leckage Ventil auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_E_LUEFTER](#job-status-e-luefter) - 0x30DA01 STATUS_E_LUEFTER E-Luefter auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EBL](#job-status-ebl) - 0x30C801 STATUS_EBL E-Box-Luefter auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EISYDR](#job-status-eisydr) - 0x33E2 STATUS_EISYDR Auslesen Eisy-Adaptionswerte mit Druckregelung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EISYGD](#job-status-eisygd) - 0x33E1 STATUS_EISYGD Auslesen Eisy-Adaptionswerte (gedrosselt) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EKP](#job-status-ekp) - 0x30D801 STATUS_EKP Elektrische Kraftstoffpumpe 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EML](#job-status-eml) - 0x30D601 STATUS_EML EML (Engine Malfunction Lamp) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_ENERGIESPARMODE](#job-status-energiesparmode) - 0x22100A STATUS_ENERGIESPARMODE Status Energiesparmode Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_ENWS](#job-status-enws) - 0x30ED01 STATUS_ENWS Vanos Einlass Ventil auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EV1](#job-status-ev1) - 0x30E101 STATUS_EV1 Einspritzventil 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EV2](#job-status-ev2) - 0x30E201 STATUS_EV2 Einspritzventil 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EV3](#job-status-ev3) - 0x30E301 STATUS_EV3 Einspritzventil 3 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EV4](#job-status-ev4) - 0x30E401 STATUS_EV4 Einspritzventil 4 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EV5](#job-status-ev5) - 0x30E501 STATUS_EV5 Einspritzventil 5 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EV6](#job-status-ev6) - 0x30E601 STATUS_EV6 Einspritzventil 6 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EWAP](#job-status-ewap) - 0x30BF01 STATUS_EWAP elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_FWV1](#job-status-fwv1) - 0x301E01 STATUS_FWV1 Fahrerwunschversorgung 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_FWV2](#job-status-fwv2) - 0x301F01 STATUS_FWV2 Fahrerwunschversorgung 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_GLF](#job-status-glf) - 0x30C301 STATUS_GLF Gesteuerte Luftfuehrung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_GLF2](#job-status-glf2) - 0x30A401 STATUS_GLF2 Gesteuerte Luftfuehrung Klappe 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_IMAALLE](#job-status-imaalle) - 0x225F90 STATUS_IMAALLE Abgleichwerte Injektoren auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_KB1](#job-status-kb1) - 0x303001 STATUS_KB1 Klopfbaustein 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_KB2](#job-status-kb2) - 0x303101 STATUS_KB2 Klopfbaustein 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_KDF](#job-status-kdf) - 0x301A01 STATUS_KDF Kraftstoffdruck im Einspritzsystem auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_KDFN](#job-status-kdfn) - 0x303F01 STATUS_KDFN Kraftstoffdruck im Niederdruckbereich auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_KFT](#job-status-kft) - 0x30C901 STATUS_KFT Kennfeldthermostat auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_KGEH](#job-status-kgeh) - 0x30AD01 STATUS_KGEH Kurbelgehaeuseentlueftungsheizung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_KLANN](#job-status-klann) - 0x33E4 STATUS_KLANN Auslesen Klann-Adaptionswerte (Anforderung aus CP10798) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_KOREL](#job-status-korel) - 0x30C701 STATUS_KOREL Klimakompressor-Relais auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_KRANN](#job-status-krann) - 0x33E3 STATUS_KRANN Auslesen Krann-Adaptionswerte Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_KUP](#job-status-kup) - 0x300401 STATUS_KUP Kupplungsschalter auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_L_SONDE](#job-status-l-sonde) - 0x302101 STATUS_L_SONDE Lambdasonde vor Kat Bank1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_L_SONDE_2](#job-status-l-sonde-2) - 0x302301 STATUS_L_SONDE_2 Lambdasonde vor Kat Bank2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_L_SONDE_2_H](#job-status-l-sonde-2-h) - 0x302401 STATUS_L_SONDE_2_H Lambdasonde hinter Kat Bank2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_L_SONDE_H](#job-status-l-sonde-h) - 0x302201 STATUS_L_SONDE_H Lambdasonde hinter Kat Bank1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_LDS1](#job-status-lds1) - 0x30B601 STATUS_LDS1 Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_LDS2](#job-status-lds2) - 0x30B701 STATUS_LDS2 Ladedrucksteller 2 (z.B. Waste Gate oder VTG variable Turbinengeometrie) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_LGS](#job-status-lgs) - 0x300701 STATUS_LGS Leergassenschalter auslesen (nur MSD80 mit N43) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_LL_ABGLEICH](#job-status-ll-abgleich) - 0x225FF0 STATUS_LL_ABGLEICH Abgleichwert LL (Leerlauf) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - 0x302501 STATUS_LMM_MASSE Luftmassenmesser 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_LSH1](#job-status-lsh1) - 0x30D001 STATUS_LSH1 Lambdasondenheizung vor Kat Bank1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_LSH2](#job-status-lsh2) - 0x30D101 STATUS_LSH2 Lambdasondenheizung hinter Kat Bank1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_LSH3](#job-status-lsh3) - 0x30D201 STATUS_LSH3 Lambdasondenheizung vor Kat Bank2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_LSH4](#job-status-lsh4) - 0x30D301 STATUS_LSH4 Lambdasondenheizung hinter Kat Bank2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MESSWERTE](#job-status-messwerte) - 0x224000 STATUS_MESSWERTE Messwerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MESSWERTE_LRP](#job-status-messwerte-lrp) - 0x22402D STATUS_MESSWERTE_LRP Messwerte Laufruhepruefung auslesen  Fehlende Groessen (Bytes) in der Testerbeschreibung sind mit 0xFF zu befuellen und auszugeben Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MIL](#job-status-mil) - 0x30D401 STATUS_MIL MIL (Malfunction Indicator Lamp) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MLS](#job-status-mls) - 0x30B201 STATUS_MLS Motorlagersteuerung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MOTORLAUFUNRUHE](#job-status-motorlaufunruhe) - 0x224003 STATUS_MOTORLAUFUNRUHE Motorlaufunruhewerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - 0x300C01 STATUS_MOTORTEMPERATUR Motortemperatur auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MSARING](#job-status-msaring) - 0x22401C STATUS_MSARING Ringspeicher Motor-Start/Stop Automatik (MSA) auslesen (nur 4-Zylinder-N43  nicht 6-Zylinder-N53/N54) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MSV](#job-status-msv) - 0x30BD01 STATUS_MSV Mengensteuerventil auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_NOCKENWELLE_ADAPTION](#job-status-nockenwelle-adaption) - 0x224006 STATUS_NOCKENWELLE_ADAPTION Nockenwellenadationswerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_NOX1](#job-status-nox1) - 0x303B01 STATUS_NOX1 NOx Sensor 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_ODR](#job-status-odr) - 0x30AB01 STATUS_ODR Oel Druck Regelung (Geregeltes Oeldrucksystem) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_ODS](#job-status-ods) - 0x300501 STATUS_ODS Oeldruckschalter auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_ODSENS](#job-status-odsens) - 0x303701 STATUS_ODSENS Oeldrucksensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_ODV](#job-status-odv) - 0x30AC01 STATUS_ODV Oeldruckventil (Geregeltes Oeldrucksystem) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_OEL](#job-status-oel) - 0x300E01 STATUS_OEL Oelsensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_PM_BACKUP](#job-status-pm-backup) - 0x225F8B STATUS_PM_BACKUP Auslesen des PM-Backup Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_PWG_POTI_SPANNUNG](#job-status-pwg-poti-spannung) - 0x302801 STATUS_PWG_POTI_SPANNUNG Fahrerwunsch 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_PWG2](#job-status-pwg2) - 0x302901 STATUS_PWG2 Fahrerwunsch 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_RBMMODE9](#job-status-rbmmode9) - 0x224026 STATUS_RBMMODE9 Rate Based Monitoring Mode 9 auslesen (Ausgabe der Werte wie im Scantool Mode 9) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_RBMMS1](#job-status-rbmms1) - 0x224027 STATUS_RBMMS1 Rate Based Monitoring Motorsteuerung MSD80 Block 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_RBMMS2](#job-status-rbmms2) - 0x224028 STATUS_RBMMS2 Rate Based Monitoring Motorsteuerung MSD80 Block 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_READINESS](#job-status-readiness) - 0x2105 STATUS_READINESS Monitorfunktionen und Readinessflags aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_RUHESTROMMESSUNG](#job-status-ruhestrommessung) - 0x332B STATUS_RUHESTROMMESSUNG Auslesen Ruhestrompruefung mit IBS Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SDF1](#job-status-sdf1) - 0x301801 STATUS_SDF1 Saugrohrdruck1 / Ladedruck1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SDF2](#job-status-sdf2) - 0x301901 STATUS_SDF2 Saugrohr-, Ladedruck und Ansauglufttemperatur fuer N54 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SPT](#job-status-spt) - 0x300601 STATUS_SPT Sporttaster auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SR](#job-status-sr) - 0x30C401 STATUS_SR Startrelais auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_DMTL_WERT](#job-status-systemcheck-dmtl-wert) - 0x33DA STATUS_SYSTEMCHECK_DMTL_WERT Auslesen Diagnosefunktion DMTL Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_EVAUSBL](#job-status-systemcheck-evausbl) - 0x3325 STATUS_SYSTEMCHECK_EVAUSBL Auslesen Diagnosefunktion EinspritzVentile EV-Ausblendung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_GEN](#job-status-systemcheck-gen) - 0x332A STATUS_SYSTEMCHECK_GEN Auslesen Diagnosefunktion Generatortest Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_GLF](#job-status-systemcheck-glf) - 0x33D5 STATUS_SYSTEMCHECK_GLF Auslesen Gesteuerte Luftfuehrung Systemcheck Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_IGR_AUS](#job-status-systemcheck-igr-aus) - 0x33F7 STATUS_SYSTEMCHECK_IGR_AUS Auslesen Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_L_REGELUNG_AUS](#job-status-systemcheck-l-regelung-aus) - 0x33D9 STATUS_SYSTEMCHECK_L_REGELUNG_AUS Auslesen Lambdaregelung ausschalten Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_L_SONDE_WERTE](#job-status-systemcheck-l-sonde-werte) - 0x33DF STATUS_SYSTEMCHECK_L_SONDE_WERTE Auslesen Diagnosefunktion vertauschte Lambdasonden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_LLERH_WERT](#job-status-systemcheck-llerh-wert) - 0x3326 STATUS_SYSTEMCHECK_LLERH_WERT Auslesen Diagnosefunktion Leerlauf-Erhoehung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_ODR](#job-status-systemcheck-odr) - 0x332C STATUS_SYSTEMCHECK_ODR Auslesen Diagnosefunktion Oeldruckregelung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_PM_MESSEMODE](#job-status-systemcheck-pm-messemode) - 0x33F6 STATUS_SYSTEMCHECK_PM_MESSEMODE Auslesen Messemode Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_TEV_WERT](#job-status-systemcheck-tev-wert) - 0x3322 STATUS_SYSTEMCHECK_TEV_WERT Auslesen Diagnosefunktion Tankentlueftungsventil Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_TABG1](#job-status-tabg1) - 0x301201 STATUS_TABG1 Abgastemperatur1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_TEV](#job-status-tev) - 0x30CF01 STATUS_TEV Tankentlueftungsventil auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_TKA](#job-status-tka) - 0x300D01 STATUS_TKA Kuehlerauslasstemperatur auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_TTEMP](#job-status-ttemp) - 0x302F01 STATUS_TTEMP Taster Tempomat auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_UBAT](#job-status-ubat) - 0x302701 STATUS_UBAT Batteriesensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_UBATT](#job-status-ubatt) - 0x301C01 STATUS_UBATT Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_UDF](#job-status-udf) - 0x301701 STATUS_UDF Umgebungsdruck auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_UGEN](#job-status-ugen) - 0x303201 STATUS_UGEN Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_UKL15](#job-status-ukl15) - 0x301B01 STATUS_UKL15 Kl.15 Spannung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_AGK](#job-steuern-agk) - 0x30C107 STEUERN_AGK Abgasklappe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [STEUERN_AGR](#job-steuern-agr) - 0x30BE07 STEUERN_AGR AbgasRueckfuehr (AGR) Ventil ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_ANWS](#job-steuern-anws) - 0x30EE07 STEUERN_ANWS Vanos Auslass Ventil ansteuern Aktivierung: Drehzahl &gt; 1000 1/min Activation: N &gt; C_N_MIN_KWP
- [STEUERN_BETRIEBSART](#job-steuern-betriebsart) - 0x2E5FF807 STEUERN_BETRIEBSART Betriebsarten vorgeben Aktivierung: Klemme 15 = EIN UND Leerlauf Activation: LV_IGK = 1 UND LV_IS = 1
- [STEUERN_CODIERUNG_BZE](#job-steuern-codierung-bze) - 0x2E3230 STEUERN_CODIERUNG_BZE Codierung fuer BZE (Batterie Zustands Erkennung) vorgeben. Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_CODIERUNG_IGR](#job-steuern-codierung-igr) - 0x2E3210 STEUERN_CODIERUNG_IGR Codierung fuer IGR (Intelligente Generator-Regelung) vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_CODIERUNG_KAT](#job-steuern-codierung-kat) - 0x2E3001 STEUERN_CODIERUNG_KAT Codierung fuer Katalysator vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min UND Betriebsstundenzaehler &lt; 10 h Activation: LV_IGK = 1 UND LV_ES = 1 UND TRT &lt; 10 h
- [STEUERN_CODIERUNG_LEISTUNGSSTUFE](#job-steuern-codierung-leistungsstufe) - 0x2E3020 STEUERN_CODIERUNG_LEISTUNGSSTUFE Codierung fuer Leistungsstufe vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min UND Betriebsstundenzaehler &lt; 10 h Activation: LV_IGK = 1 UND LV_ES = 1 UND TRT &lt; 10 h
- [STEUERN_CODIERUNG_MIL](#job-steuern-codierung-mil) - 0x2E3000 STEUERN_CODIERUNG_MIL Codierung fuer MIL (Malfunction Indication Lamp) vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min UND Betriebsstundenzaehler &lt; 10 h Activation: LV_IGK = 1 UND LV_ES = 1 UND TRT &lt; 10 h
- [STEUERN_CODIERUNG_OEL](#job-steuern-codierung-oel) - 0x2E3200 STEUERN_CODIERUNG_OEL Codierung fuer Oelwechselintervall vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_CODIERUNG_PROTOKOLL](#job-steuern-codierung-protokoll) - 0x2E3030 STEUERN_CODIERUNG_PROTOKOLL Codierung Protokoll vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min UND Betriebsstundenzaehler &lt; 10 h Activation: LV_IGK = 1 UND LV_ES = 1 UND TRT &lt; 10 h
- [STEUERN_CODIERUNG_SPA](#job-steuern-codierung-spa) - 0x2E3220 STEUERN_CODIERUNG_SPA Codierung fuer SPA (Schaltpunktanzeige) vorgeben. Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_CODIERUNG_VMAX](#job-steuern-codierung-vmax) - 0x2E3010 STEUERN_CODIERUNG_VMAX Codierung fuer maximale Geschwindigkeit vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min UND Betriebsstundenzaehler &lt; 10 h Activation: LV_IGK = 1 UND LV_ES = 1 UND TRT &lt; 10 h
- [STEUERN_CODIERUNG_XENON](#job-steuern-codierung-xenon) - 0x2E3211 STEUERN_CODIERUNG_XENON Codierung fuer Xenon-Lichtverbau vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_DESULFATISIERUNG](#job-steuern-desulfatisierung) - 0x312D STEUERN_DESULFATISIERUNG Ansteuerung Desulfatisierung Aktivierung: Drehzahl &gt; C_N_IS_SO2P_MIN UND Ganginfo = 0 UND Kupplungsschalter = Aus UND Geschwindigkeit &lt;= C_VS_SO2P_EXT_MAX UND Pedalwert &lt;= C_PV_SO2P_EXT_MAX Activation: N_32 &gt;= C_N_IS_SO2P_MIN UND GEAR = 0 UND LV_CLU_SWI = 0 UND VS &lt;= C_VS_SO2P_EXT_MAX UND PV_AV &lt;= C_PV_SO2P_EXT_MAX
- [STEUERN_DISA](#job-steuern-disa) - 0x30C607 STEUERN_DISA Variable Sauganlage (DISA) Klappe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_DISA2](#job-steuern-disa2) - 0x30AE07 STEUERN_DISA2 Variable Sauganlage (DISA) Klappe2 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_DK](#job-steuern-dk) - 0x302A07 STEUERN_DK Drosselklappe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_DKH](#job-steuern-dkh) - 0x309E07 STEUERN_DKH Drosselklappenbeheizung ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [STEUERN_DMTL_HEIZUNG](#job-steuern-dmtl-heizung) - 0x30CE07 STEUERN_DMTL_HEIZUNG Diagnosemodul-Tank Leckage Heizung ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_DMTL_P](#job-steuern-dmtl-p) - 0x30CC07 STEUERN_DMTL_P Diagnosemodul-Tank Leckage Pumpe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_DMTL_V](#job-steuern-dmtl-v) - 0x30CD07 STEUERN_DMTL_V Diagnosemodul-Tank Leckage Ventil ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - 0x30DA07 STEUERN_E_LUEFTER E-Luefter ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Motortemperatur &lt; 95 Grad C UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND TCO &lt; C_TCO_MAX_KWP UND LV_IGK = 1
- [STEUERN_EBL](#job-steuern-ebl) - 0x30C807 STEUERN_EBL E-Box-Luefter ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [STEUERN_EISYDR](#job-steuern-eisydr) - 0x31E2 STEUERN_EISYDR Ansteuern Eisy-Adaptionswerte mit Druckregelung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_EISYGD](#job-steuern-eisygd) - 0x31E1 STEUERN_EISYGD Ansteuern Eisy-Adaptionswerte (gedrosselt) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_EKP](#job-steuern-ekp) - 0x30D807 STEUERN_EKP Elektrische Kraftstoffpumpe 1 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_EML](#job-steuern-eml) - 0x30D607 STEUERN_EML EML (Engine Malfunction Lamp) ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [STEUERN_ENDE_AGK](#job-steuern-ende-agk) - 0x30C100 STEUERN_ENDE_AGK Abgasklappe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_AGR](#job-steuern-ende-agr) - 0x30BE00 STEUERN_ENDE_AGR AbgasRueckfuehr (AGR) Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_ANWS](#job-steuern-ende-anws) - 0x30EE00 STEUERN_ENDE_ANWS Vanos Auslass Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_BETRIEBSART](#job-steuern-ende-betriebsart) - 0x2E5FF800 STEUERN_ENDE_BETRIEBSART Betriebsarten Vorgeben beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_DESULFATISIERUNG](#job-steuern-ende-desulfatisierung) - 0x322D STEUERN_ENDE_DESULFATISIERUNG Ansteuerung Desulfatisierung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_DISA](#job-steuern-ende-disa) - 0x30C600 STEUERN_ENDE_DISA Variable Sauganlage (DISA) Klappe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_DISA2](#job-steuern-ende-disa2) - 0x30AE00 STEUERN_ENDE_DISA2 Variable Sauganlage (DISA) Klappe2 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_DK](#job-steuern-ende-dk) - 0x302A00 STEUERN_ENDE_DK Drosselklappe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_DKH](#job-steuern-ende-dkh) - 0x309E00 STEUERN_ENDE_DKH Drosselklappenbeheizung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_DMTL_HEIZUNG](#job-steuern-ende-dmtl-heizung) - 0x30CE00 STEUERN_ENDE_DMTL_HEIZUNG Diagnosemodul-Tank Leckage Heizung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_DMTL_P](#job-steuern-ende-dmtl-p) - 0x30CC00 STEUERN_ENDE_DMTL_P Diagnosemodul-Tank Leckage Pumpe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_DMTL_V](#job-steuern-ende-dmtl-v) - 0x30CD00 STEUERN_ENDE_DMTL_V Diagnosemodul-Tank Leckage Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_E_LUEFTER](#job-steuern-ende-e-luefter) - 0x30DA00 STEUERN_ENDE_E_LUEFTER E-Luefter Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_EBL](#job-steuern-ende-ebl) - 0x30C800 STEUERN_ENDE_EBL E-Box-Luefter Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_EKP](#job-steuern-ende-ekp) - 0x30D800 STEUERN_ENDE_EKP Elektrische Kraftstoffpumpe 1 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_EML](#job-steuern-ende-eml) - 0x30D600 STEUERN_ENDE_EML EML (Engine Malfunction Lamp) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_ENWS](#job-steuern-ende-enws) - 0x30ED00 STEUERN_ENDE_ENWS Vanos Einlass Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_EWAP](#job-steuern-ende-ewap) - 0x30BF00 STEUERN_ENDE_EWAP elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_GLF](#job-steuern-ende-glf) - 0x30C300 STEUERN_ENDE_GLF Gesteuerte Luftfuehrung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_GLF2](#job-steuern-ende-glf2) - 0x30A400 STEUERN_ENDE_GLF2 Gesteuerte Luftfuehrung Klappe 2 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_KFT](#job-steuern-ende-kft) - 0x30C900 STEUERN_ENDE_KFT Kennfeldthermostat Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_KGEH](#job-steuern-ende-kgeh) - 0x30AD00 STEUERN_ENDE_KGEH Kurbelgehaeuseentlueftungsheizung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_KOREL](#job-steuern-ende-korel) - 0x30C700 STEUERN_ENDE_KOREL Klimakompressor-Relais Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_LDS1](#job-steuern-ende-lds1) - 0x30B600 STEUERN_ENDE_LDS1 Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_LDS2](#job-steuern-ende-lds2) - 0x30B700 STEUERN_ENDE_LDS2 Ladedrucksteller 2 (z.B. Waste Gate oder VTG variable Turbinengeometrie) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_LSH1](#job-steuern-ende-lsh1) - 0x30D000 STEUERN_ENDE_LSH1 Lambdasondenheizung vor Kat Bank1 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_LSH2](#job-steuern-ende-lsh2) - 0x30D100 STEUERN_ENDE_LSH2 Lambdasondenheizung hinter Kat Bank1 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_LSH3](#job-steuern-ende-lsh3) - 0x30D200 STEUERN_ENDE_LSH3 Lambdasondenheizung vor Kat Bank2 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_LSH4](#job-steuern-ende-lsh4) - 0x30D300 STEUERN_ENDE_LSH4 Lambdasondenheizung hinter Kat Bank2 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_MIL](#job-steuern-ende-mil) - 0x30D400 STEUERN_ENDE_MIL MIL (Malfunction Indicator Lamp) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_MLS](#job-steuern-ende-mls) - 0x30B200 STEUERN_ENDE_MLS Motorlagersteuerung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_MSV](#job-steuern-ende-msv) - 0x30BD00 STEUERN_ENDE_MSV Mengensteuerventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_ODR](#job-steuern-ende-odr) - 0x30AB00 STEUERN_ENDE_ODR Oel Druck Regelung (Geregeltes Oeldrucksystem) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_ODV](#job-steuern-ende-odv) - 0x30AC00 STEUERN_ENDE_ODV Oeldruckventil (Geregeltes Oeldrucksystem) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_SR](#job-steuern-ende-sr) - 0x30C400 STEUERN_ENDE_SR Startrelais Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_TEV](#job-steuern-ende-tev) - 0x30CF00 STEUERN_ENDE_TEV Tankentlueftungsventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_UGEN](#job-steuern-ende-ugen) - 0x303200 STEUERN_ENDE_UGEN Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENDE_UVSG](#job-steuern-ende-uvsg) - 0x301C00 STEUERN_ENDE_UVSG Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_ENERGIESPARMODE](#job-steuern-energiesparmode) - 0x310C STEUERN_ENERGIESPARMODE Energiesparmode aktivieren Aktivierung: Klemme 15 = EIN UND Setzen Energiesparmode ueber Tester freigeschaltet Activation: LV_IGK = 1 UND LC_EGY_MIN_KWP = 1
- [STEUERN_ENWS](#job-steuern-enws) - 0x30ED07 STEUERN_ENWS Vanos Einlass Ventil ansteuern Aktivierung: Drehzahl &gt; 1000 1/min Activation: N &gt; C_N_MIN_KWP
- [STEUERN_EWAP](#job-steuern-ewap) - 0x30BF07 STEUERN_EWAP elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Motortemperatur &lt; 95 Grad C UND Drehzahl = 0 1/min  UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND TCO &lt; C_TCO_MAX_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_GLF](#job-steuern-glf) - 0x30C307 STEUERN_GLF Gesteuerte Luftfuehrung ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Motortemperatur &lt; 95 Grad C UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND TCO &lt; C_TCO_MAX_KWP UND LV_IGK = 1
- [STEUERN_GLF2](#job-steuern-glf2) - 0x30A407 STEUERN_GLF2 Gesteuerte Luftfuehrung Klappe 2 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Motortemperatur &lt; 95 Grad C UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND TCO &lt; C_TCO_MAX_KWP UND LV_IGK = 1
- [STEUERN_KFT](#job-steuern-kft) - 0x30C907 STEUERN_KFT Kennfeldthermostat ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [STEUERN_KGEH](#job-steuern-kgeh) - 0x30AD07 STEUERN_KGEH Kurbelgehaeuseentlueftungsheizung ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [STEUERN_KLANN](#job-steuern-klann) - 0x31E4 STEUERN_KLANN Ansteuern Klann-Adaptionswerte (Anforderung aus CP10798) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_KOREL](#job-steuern-korel) - 0x30C707 STEUERN_KOREL Klimakompressor-Relais ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [STEUERN_KRANN](#job-steuern-krann) - 0x31E3 STEUERN_KRANN Ansteuern Krann-Adaptionswerte Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_KVA](#job-steuern-kva) - 0x3BC1 STEUERN_KVA KraftstoffVerbrauchsAnzeige - Korrekturfaktor schreiben Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_LDS1](#job-steuern-lds1) - 0x30B607 STEUERN_LDS1 Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1
- [STEUERN_LDS2](#job-steuern-lds2) - 0x30B707 STEUERN_LDS2 Ladedrucksteller 2 (z.B. Waste Gate oder VTG variable Turbinengeometrie) ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1
- [STEUERN_LL_ABGLEICH](#job-steuern-ll-abgleich) - 0x2E5FF007 STEUERN_LL_ABGLEICH Abgleichwert LL (Leerlauf) vorgeben Aktivierung: Klemme 15 = EIN UND Leerlaufabgleich ueber Testervorgabe = EIN Activation: LV_IGK = 1 UND LV_KWP_ENA = 1
- [STEUERN_LLABG_PROG](#job-steuern-llabg-prog) - 0x2E5FF008 STEUERN_LLABG_PROG Abgleichwert LL (Leerlauf) programmieren Aktivierung: Klemme 15 = EIN UND Leerlaufabgleich ueber Testervorgabe = EIN Activation: LV_IGK = 1 UND LV_KWP_ENA = 1
- [STEUERN_LSH1](#job-steuern-lsh1) - 0x30D007 STEUERN_LSH1 Lambdasondenheizung vor Kat Bank1 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_LSH2](#job-steuern-lsh2) - 0x30D107 STEUERN_LSH2 Lambdasondenheizung hinter Kat Bank1 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_LSH3](#job-steuern-lsh3) - 0x30D207 STEUERN_LSH3 Lambdasondenheizung vor Kat Bank2 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_LSH4](#job-steuern-lsh4) - 0x30D307 STEUERN_LSH4 Lambdasondenheizung hinter Kat Bank2 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_MIL](#job-steuern-mil) - 0x30D407 STEUERN_MIL MIL (Malfunction Indicator Lamp) ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [STEUERN_MLS](#job-steuern-mls) - 0x30B207 STEUERN_MLS Motorlagersteuerung ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1
- [STEUERN_MSV](#job-steuern-msv) - 0x30BD07 STEUERN_MSV Mengensteuerventil ansteuern Aktivierung: 50000 hPa &lt; Raildruck &lt; 220000 hPa UND Leerlauf Activation: C_FUP_MIN_KWP &lt; FUP &lt; C_FUP_MAX_KWP UND LV_IS = 1
- [STEUERN_ODR](#job-steuern-odr) - 0x30AB07 STEUERN_ODR Oel Druck Regelung (Geregeltes Oeldrucksystem) ansteuern Aktivierung: 2 bar &lt; Oeldruck &lt; 9 bar UND 500 1/min &lt; Drehzahl &lt; 2000 1/min Activation: C_POIL_MIN_KWP &lt; POIL &lt; C_POIL_MAX_KWP UND C_N_MIN_KWP_POIL &lt; N &lt; C_N_MAX_KWP_POIL
- [STEUERN_ODV](#job-steuern-odv) - 0x30AC07 STEUERN_ODV Oeldruckventil (Geregeltes Oeldrucksystem) ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_PM_RESTORE](#job-steuern-pm-restore) - 0x2E5F8B STEUERN_PM_RESTORE Schreiben PM-Restore Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_PROGRAMM_IMA_ZYL_1](#job-steuern-programm-ima-zyl-1) - 0x2E5F91 STEUERN_PROGRAMM_IMA_ZYL_1 Abgleichwert Injektor 01 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_PROGRAMM_IMA_ZYL_2](#job-steuern-programm-ima-zyl-2) - 0x2E5F95 STEUERN_PROGRAMM_IMA_ZYL_2 Abgleichwert Injektor 05 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_PROGRAMM_IMA_ZYL_3](#job-steuern-programm-ima-zyl-3) - 0x2E5F93 STEUERN_PROGRAMM_IMA_ZYL_3 Abgleichwert Injektor 03 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_PROGRAMM_IMA_ZYL_4](#job-steuern-programm-ima-zyl-4) - 0x2E5F96 STEUERN_PROGRAMM_IMA_ZYL_4 Abgleichwert Injektor 06 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_PROGRAMM_IMA_ZYL_5](#job-steuern-programm-ima-zyl-5) - 0x2E5F92 STEUERN_PROGRAMM_IMA_ZYL_5 Abgleichwert Injektor 02 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_PROGRAMM_IMA_ZYL_6](#job-steuern-programm-ima-zyl-6) - 0x2E5F94 STEUERN_PROGRAMM_IMA_ZYL_6 Abgleichwert Injektor 04 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_PROGRAMM_IMAALLE](#job-steuern-programm-imaalle) - 0x2E5F90 STEUERN_PROGRAMM_IMAALLE Abgleichwerte Injektoren programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [STEUERN_RUHESTROMMESSUNG](#job-steuern-ruhestrommessung) - 0x312B STEUERN_RUHESTROMMESSUNG Ansteuern Ruhestrompruefung mit IBS Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_SR](#job-steuern-sr) - 0x30C407 STEUERN_SR Startrelais ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1
- [STEUERN_TEV](#job-steuern-tev) - 0x30CF07 STEUERN_TEV Tankentlueftungsventil ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1
- [STEUERN_UGEN](#job-steuern-ugen) - 0x303207 STEUERN_UGEN Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1
- [STEUERN_UVSG](#job-steuern-uvsg) - 0x301C07 STEUERN_UVSG Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) ansteuern Aktivierung: Geschwindigkeit &lt; 5 km/h UND Drehzahl = 0 1/min Activation: VS &lt; C_VS_MAX_KWP UND LV_ES = 1
- [STOP_SYSTEMCHECK_DMTL](#job-stop-systemcheck-dmtl) - 0x32DA STOP_SYSTEMCHECK_DMTL Diagnosefunktion DMTL beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_EVAUSBL](#job-stop-systemcheck-evausbl) - 0x3125 STOP_SYSTEMCHECK_EVAUSBL Ansteuern Diagnosefunktion Einspritzventilausblendung beenden Aktivierung: Klemme 15 = EIN UND Motorstatus = (Leerlauf ODER Teillast) UND Drehzahl &lt; 3000 1/min Activation: LV_IGK = 1 UND STATE_ENG = (IS ODER PL) UND N &lt; C_N_MAX_KWP
- [STOP_SYSTEMCHECK_GEN](#job-stop-systemcheck-gen) - 0x322A STOP_SYSTEMCHECK_GEN Diagnosefunktion Generatortest beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_GLF](#job-stop-systemcheck-glf) - 0x32D5 STOP_SYSTEMCHECK_GLF Ende Gesteuerte Luftfuehrung Systemcheck Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_IGR_AUS](#job-stop-systemcheck-igr-aus) - 0x32F7 STOP_SYSTEMCHECK_IGR_AUS Ende Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_L_REGELUNG_AUS](#job-stop-systemcheck-l-regelung-aus) - 0x32D9 STOP_SYSTEMCHECK_L_REGELUNG_AUS Ende Lambdaregelung ausschalten Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_L_SONDE](#job-stop-systemcheck-l-sonde) - 0x32DF STOP_SYSTEMCHECK_L_SONDE Diagnosefunktion vertauschte Lambdasonden beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_LLERH](#job-stop-systemcheck-llerh) - 0x3226 STOP_SYSTEMCHECK_LLERH Diagnosefunktion Leerlauf-Erhoehung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_ODR](#job-stop-systemcheck-odr) - 0x322C STOP_SYSTEMCHECK_ODR Diagnosefunktion Oeldruckregelung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_TEV_FUNC](#job-stop-systemcheck-tev-func) - 0x3222 STOP_SYSTEMCHECK_TEV_FUNC Diagnosefunktion Tankentlueftungsventil beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [MESSWERTBLOCK_LESEN](#job-messwertblock-lesen) - 0x2CF0 MESSWERTBLOCK_LESEN DDLI Messwerte auf Basis Übergabestring aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - 0x2CF0 4807 & 4808 STATUS_MOTORDREHZAHL Auslesen des Soll- und Istwertes der Motordrehzahl Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_INT](#job-status-int) - 0x2CF0 5A81 STATUS_INT Auslesen des Integrator Bank 1 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_INT_2](#job-status-int-2) - 0x2CF0 5A82 STATUS_INT_2 Auslesen des Integrator Bank 2 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_ADD](#job-status-add) - 0x2CF0 5A83 STATUS_ADD Auslesen der Adaption Offset Lambda Bank 1 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_ADD_2](#job-status-add-2) - 0x2CF0 5A84 STATUS_ADD_2 Auslesen der Adaption Offset Lambda Bank 2 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MUL](#job-status-mul) - 0x2CF0 5A85 STATUS_MUL Auslesen der Adaption Multiplikation Lambda Bank 1 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MUL_2](#job-status-mul-2) - 0x2CF0 5A86 STATUS_MUL_2 Auslesen der Adaption Multiplikation Lambda Bank 2 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_BETRIEBSSTUNDENZAEHLER](#job-status-betriebsstundenzaehler) - 0x2CF0 5AB4 STATUS_BETRIEBSSTUNDENZAEHLER Betriebsstundenzaehler auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_GEBERRAD_ADAPTION](#job-status-geberrad-adaption) - 0x2CF0 STATUS_GEBERRAD_ADAPTION Adaptionswerte für das Geberrad aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MESSWERTBLOCK_ADC](#job-status-messwertblock-adc) - 0x2CF0 STATUS_MESSWERTBLOCK_ADC ADC-Werte aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MESSWERTE_VANOS](#job-status-messwerte-vanos) - 0x2CF0 STATUS_MESSWERTE_VANOS Messwerte CAM_IN und CAM_EX nach Wunsch VS-42 aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_FASTA_COMMON](#job-status-fasta-common) - 0x2CF0 _STATUS_FASTA_COMMON DDLI Messwerte für FASTA auf Basis Übergabestring aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_OBD_MODE_01](#job-status-obd-mode-01) - 0x0101 _STATUS_OBD_MODE_01 Auslesen der Motor-Diagnosedaten nach Mode 01 PID 01 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_OBD_MODE_03](#job-status-obd-mode-03) - 0x03 _STATUS_OBD_MODE_03 Auslesen der P-Codes nach Mode 03 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_OBD_MODE_07](#job-status-obd-mode-07) - 0x07 _STATUS_OBD_MODE_07 Auslesen der P-Codes nach Mode 07 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [_STATUS_OBD_MODE_09](#job-status-obd-mode-09) - 0x0908 _STATUS_OBD_MODE_09 Rate Based Monitoring Mode 9 mit PID 08 auslesen (Ausgabe der Werte wie im Scantool Mode 9) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [ABGLEICHWERTE_SCHREIBEN](#job-abgleichwerte-schreiben) - 0x2E5F90 ABGLEICHWERTE_SCHREIBEN Abgleichwerte Injektoren programmieren für CASCADE mit Übernahme Daten aus COD-Datei Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1
- [_ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - 0x225F90 ABGLEICHWERTE_LESEN Abgleichwerte Injektoren auslesen für CASCADE für Vergleich mit Daten aus COD-Datei Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - 0x17 FS_LESEN_DETAIL Fehlerspeicher lesen (ein Fehler / alle Details) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [FS_LESEN_FREEZE_FRAME](#job-fs-lesen-freeze-frame) - 0x210A FS_LESEN_FREEZE_FRAME Fehlerspeicher auslesen mit SAE Werten Umwelt und P-Code Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [FS_LESEN_FREEZE_FRAME_EXTRA_LONG](#job-fs-lesen-freeze-frame-extra-long) - 0x224019 FS_LESEN_FREEZE_FRAME_EXTRA_LONG Fehlerspeicher auslesen mit erweiterten SAE Werten Umwelt und P-Code Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [FS_LESEN_HEX](#job-fs-lesen-hex) - 0x17 FS_LESEN_HEX Fehlerspeicher auslesen als Hex Dump Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [IS_LESEN](#job-is-lesen) - 0x222000 IS_LESEN Infospeicher lesen (alle Info-Meldungen / Ort und Art) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - 0x17 IS_LESEN_DETAIL Infospeicher lesen (ein Fehler / alle Details) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [HS_LESEN](#job-hs-lesen) - 0x222100 HS_LESEN Historyspeicher lesen (alle Info-Meldungen / Ort und Art) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [IDENT_AIF](#job-ident-aif) - 0x1A80 und 0x23 IDENT_AIF Identdaten und Anwender Informations Felder Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [INTERFACETYPE](#job-interfacetype) - Interface-Typ bestimmen und ausgeben (Wichtig für Baudratenumschaltung: da bei ADS, EADS und OBD nur 115200 Baud und bei EDIC nur 125000 Baud möglich sind) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [SET_BAUDRATE](#job-set-baudrate) - Initialisierung der Kommunikationsparameter mit bestimmter Baudrate Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [SET_PARAMETER](#job-set-parameter) - Aenderung der Kommunikationsparameter bei Long-Parametersätzen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [SPEICHER_LESEN_ASCII](#job-speicher-lesen-ascii) - 0x23 SPEICHER_LESEN_ASCII Auslesen des Steuergeraete-Speichers Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_EWS](#job-status-ews) - KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC000 Zurücklesen verschiedener interner Stati für EWS
- [STATUS_EWS4_SK](#job-status-ews4-sk) - KWP 2000: $22 ReadDataByCommonIdentifier CommonIdentifier=0xC002 Lesen des SecretKey des Server sowie Client für EWS4
- [STEUERN_EWS4_SK](#job-steuern-ews4-sk) - 17 "EWS4-data" schreiben KWP 2000: $2E ReadDataByCommonIdentifier CommonIdentifier=0xC001
- [FLASH_PARAMETER_LESEN](#job-flash-parameter-lesen) - Gibt die SG-spezifischen Flash-Parameter zurück
- [FLASH_PARAMETER_SETZEN](#job-flash-parameter-setzen) - Setzt die SG-spezifischen Flash-Parameter
- [IDENT_IBS](#job-ident-ibs) - $22 40 21 BMW Nr, Seriennummer, SW/HW Index
- [STATUS_SYSTEMCHECK_PM_INFO_1](#job-status-systemcheck-pm-info-1) - $22 40 22 Bytefeld 1 Batterie Powermanagement lesen
- [STATUS_SYSTEMCHECK_PM_INFO_2](#job-status-systemcheck-pm-info-2) - $22 40 23 Bytefeld 2 Batterie Powermanagement lesen
- [STEUERN_PM_HISTOGRAM_RESET](#job-steuern-pm-histogram-reset) - $30 F5 04 Loeschen von pminfo1 index 23-30
- [ADAP_SELEKTIV_LOESCHEN](#job-adap-selektiv-loeschen) - Löschen von Adaptionen und gelernte Varianten KWP 2000 $31 30 xx xx xx Loeschen der Adaptionswerte
- [STEUERN_BATTERIETAUSCH_REGISTRIEREN](#job-steuern-batterietausch-registrieren) - KWP 2000 $31 30 00 10 00 Bit setzen Batterietausch registrieren
- [START_SYSTEMCHECK_PM_MESSEMODE](#job-start-systemcheck-pm-messemode) - $31 F6 Systemdiagnose BatterieSensor reset
- [STOP_SYSTEMCHECK_PM_MESSEMODE](#job-stop-systemcheck-pm-messemode) - $32 F6 Systemdiagnose BatterieSensor reset beenden
- [SLEEP_MODE_FUNKTIONAL](#job-sleep-mode-funktional) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown Modus  : Default
- [_STATUS_KUP](#job-status-kup) - 0x300401 STATUS_KUP Kupplungsschalter auslesen NO_CON
- [STATUS_MSA](#job-status-msa) - 0x22402F STATUS_MSA MSA (MotorStopAutomatik) auslesen
- [STATUS_MSA_DEAK](#job-status-msa-deak) - 0x225F8E STATUS_MSA_DEAK MSA (MotorStopAutomatik) deaktivieren auslesen
- [STATUS_MSA_DEAK_AV](#job-status-msa-deak-av) - 0x225F8F STATUS_MSA_DEAK_AV Selektive Deaktivierung Abschaltverhinderer MSA (MotorStopAutomatik) auslesen
- [_STATUS_MSARING](#job-status-msaring) - 0x22401C STATUS_MSARING Ringspeicher Motor-Start/Stop Automatik (MSA) auslesen
- [STATUS_NULLGANG_ERKENNUNG](#job-status-nullgang-erkennung) - 0x22402E STATUS_NULLGANG_ERKENNUNG Nullgang Erkennung auslesen
- [STEUERN_ENDE_MSA_DEAK](#job-steuern-ende-msa-deak) - 0x2E5F8E00 STEUERN_ENDE_MSA_DEAK MSA (MotorStopAutomatik) deaktivieren Vorgeben beenden NO_CON
- [STEUERN_ENDE_MSA_DEAK_AV](#job-steuern-ende-msa-deak-av) - 0x2E5F8F00 STEUERN_ENDE_MSA_DEAK_AV Selektive Deaktivierung Abschaltverhinderer MSA (MotorStopAutomatik) Vorgeben beenden NO_CON
- [STEUERN_MSA_DEAK](#job-steuern-msa-deak) - 0x2E5F8E07 STEUERN_MSA_DEAK MSA (MotorStopAutomatik) deaktivieren vorgeben NO_CON
- [STEUERN_MSA_DEAK_AV](#job-steuern-msa-deak-av) - 0x2E5F8F07 STEUERN_MSA_DEAK_AV Selektive Deaktivierung Abschaltverhinderer MSA (MotorStopAutomatik) vorgeben NO_CON
- [STEUERN_MSARING_HFKRESET](#job-steuern-msaring-hfkreset) - 0x2E5F89 STEUERN_MSARING_HFKRESET MSARING Haeufigkeitszaehler Reset NO_CON
- [STEUERN_NULLGANG_LERNEN](#job-steuern-nullgang-lernen) - 0x312E STEUERN_NULLGANG_LERNEN Ansteuern Nullgang lernen (Der Nullgang-Lernwert ist nichtfluechtig so abzulegen, dass er bei Reprogrammierung nicht Ã¼berschrieben wird.)
- [STEUERN_NULLGANG_SCHREIBEN](#job-steuern-nullgang-schreiben) - 0x2E5F8A STEUERN_NULLGANG_SCHREIBEN Schreiben Nullgang Lernwert

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

<a id="job-status-messwertblock-lesen"></a>
### STATUS_MESSWERTBLOCK_LESEN

Lesen eines Messwertblockes Es muss immer das BlockSchreibenFlag und mindestens ein MESSWERT uebergeben werden. KWP2000: $2C DynamicallyDefinedLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier $04 ClearDynamicallyDefinedLocalIdentifier KWP2000: $2C DynamicallyDefinedLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier $02 DefineByCommonIdentifier KWP2000: $21 ReadDataByLocalIdentifier $F0 DynamicallyDefinedLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | Wenn 'JA' wird der Messwertblock im SG gelöscht neu ins SG geschrieben und dann gelesen Wenn 'NEIN' wird der Messwertblock im SG nicht gelöscht Es wird der im SG gespeicherte Messwertblock gelesen table MesswerteMode TEXT KOMMENTAR |
| MESSWERT | string | Dynamische Argumente Es können bis zu 42 Argumente übergeben werden Es muss mindestens ein Argument übergeben werden Er wird das zugehörige Result table MesswerteTab ARG RESULTNAME erzeugt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_2 | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG_3 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT_3 | binary | Hex-Antwort von SG |

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
| CBS_KENNUNG | string | gewuenschte CBS-Kennung table CbsKennung CBS_K CBS_K_TEXT Werte Kombi-Umfaenge: Brfl, ZKrz, Sic, Kfl, TUV, AU, Ueb Werte externe Umfaenge: Oel, Br_v, Br_h, Filt, CSF, Batt, VTG Defaultwert: 0x00 (ungueltig) |
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

<a id="job-flash-schreiben-xxl"></a>
### FLASH_SCHREIBEN_XXL

0x36 FLASH_SCHREIBEN_XXL Flash Daten schreiben XXL-Format, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : (unbenutzt) Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : (unbenutzt) Anzahl Wortdaten (low/high) Byte 17,18,19,20    : (unbenutzt) Wortadresse (low/highbyte, low/highword) Byte 21,....        : Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_SCHREIBEN_ANZAHL | unsigned int | Anzahl FLASH_SCHREIBEN seit letztem FLASH_SCHREIBEN_ADRESSE |
| FLASH_SCHREIBEN_STATUS | int | Programmierstatus 1 = Programmierung in Ordnung 2 = Programmierung nicht in Ordnung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben-adresse-4byte"></a>
### FLASH_SCHREIBEN_ADRESSE_4BYTE

0x34 FLASH_SCHREIBEN_ADRESSE_4BYTE Flash Daten schreiben, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_BLOCKLAENGE_DATEN | int | Flash Datenlaenge ohne Telegramm-Overhead |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-loeschen-4byte"></a>
### FLASH_LOESCHEN_4BYTE

0x3102 FLASH_LOESCHEN_4BYTE Flash löschen, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : Loeschzeit in Sekunden (Byteparameter 1) Byte 5,6            : Loeschzeit in Sekunden (WordParameter 1 (low/high)) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| FLASH_LOESCHEN_STATUS | int | Loeschstatus 1 = Speicher geloescht 2 = Speicher nicht geloescht 5 = Signaturpruefung PAF nicht durchgefuehrt |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-schreiben-ende-4byte"></a>
### FLASH_SCHREIBEN_ENDE_4BYTE

0x37 FLASH_SCHREIBEN_ENDE_4BYTE Flashprogrammierung abschliessen, Standard Flashjob, Modus  : Default Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BINAER_BUFFER | binary | Als Argument wird ein vorgefuellter Binaerbuffer uebergeben Der Binaerbuffer hat folgenden Aufbau Byte 0              : Datentyp (1:Daten, 2:Maskendaten) Byte 1              : (unbenutzt) Wortbreite (1:Byte, 2:Word, 3:DWord) Byte 2              : (unbenutzt) Byteordnung (0:LSB zuerst, 1 MSB zuerst) Byte 3              : Adressierung (0: freie Adressierung, 1:Blockadressierung) Byte 4              : (unbenutzt) Byteparameter 1 Byte 5,6            : (unbenutzt) WordParameter 1 (low/high) Byte 7,8            : (unbenutzt) WordParameter 2 (low/high) Byte 9,10,11,12     : (unbenutzt) Maske (linksbuendig) Byte 13,14          : Anzahl Bytedaten (low/high) Byte 15,16          : Anzahl Wortdaten (low/high) Byte 17,18,19,20    : Wortadresse (low/highbyte, low/highword) Byte 21,....        : (unbenutzt) Flashdaten Byte 21+Anzahl Daten: ETX (0x03) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bzeinfo"></a>
### _STATUS_BZEINFO

0x22401A _STATUS_BZEINFO Infospeicher Batterie Zustands Erkennung (BZE) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_QV_OUT_M_WERT | real | Gueltiger gemittelter Kapazitaetsverlust (A2L-Name: Qv_out_m) Qv_out_m   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_OUT_M_EINH | string | percent |
| STAT_QV_QUALI_M_WERT | real | Qualitaetsindex fuer gemittelten Qv-Wert (A2L-Name: Qv_quali_m) Qv_quali_m   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_M_EINH | string | percent |
| STAT_QV_STATUS | long | Prozessstatus / Trend fuer gemittelten Qv-Wert (A2L-Name: Qv_status) Qv_status   Min: -128 Max: 127 |
| STAT_QV_OUT_1_WERT | long | Kapazitaetsverlust letzter Start (A2L-Name: Qv_out_1) Qv_out_1   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_1_EINH | string | Ah |
| STAT_QV_OUT_2_WERT | long | Kapazitaetsverlust 2. letzter Start (A2L-Name: Qv_out_2) Qv_out_2   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_2_EINH | string | Ah |
| STAT_QV_OUT_3_WERT | long | Kapazitaetsverlust 3. letzter Start (A2L-Name: Qv_out_3) Qv_out_3   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_3_EINH | string | Ah |
| STAT_QV_OUT_4_WERT | long | Kapazitaetsverlust 4. letzter Start (A2L-Name: Qv_out_4) Qv_out_4   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_4_EINH | string | Ah |
| STAT_QV_OUT_5_WERT | long | Kapazitaetsverlust 5. letzter Start (A2L-Name: Qv_out_5) Qv_out_5   Einheit: Ah   Min: -128 Max: 127 |
| STAT_QV_OUT_5_EINH | string | Ah |
| STAT_QV_QUALI_1_WERT | real | Qualitaetsindex letzter Qv-Wert (A2L-Name: Qv_quali_1) Qv_quali_1   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_1_EINH | string | percent |
| STAT_QV_QUALI_2_WERT | real | Qualitaetsindex 2. letzter Qv-Wert (A2L-Name: Qv_quali_2) Qv_quali_2   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_2_EINH | string | percent |
| STAT_QV_QUALI_3_WERT | real | Qualitaetsindex 3. letzter Qv-Wert (A2L-Name: Qv_quali_3) Qv_quali_3   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_3_EINH | string | percent |
| STAT_QV_QUALI_4_WERT | real | Qualitaetsindex 4. letzter Qv-Wert (A2L-Name: Qv_quali_4) Qv_quali_4   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_4_EINH | string | percent |
| STAT_QV_QUALI_5_WERT | real | Qualitaetsindex 5. letzter Qv-Wert (A2L-Name: Qv_quali_5) Qv_quali_5   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_QUALI_5_EINH | string | percent |
| STAT_QV_TD1_WERT | unsigned long | Zeit seit Qv_out_1 Berechnung (A2L-Name: Qv_td1) Qv_td1   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD1_EINH | string | h |
| STAT_QV_TD2_WERT | unsigned long | Zeit zwischen Qv_out_1 und Qv_out_2 (A2L-Name: Qv_td2) Qv_td2   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD2_EINH | string | h |
| STAT_QV_TD3_WERT | unsigned long | Zeit zwischen Qv_out_2 und Qv_out_3 (A2L-Name: Qv_td3) Qv_td3   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD3_EINH | string | h |
| STAT_QV_TD4_WERT | unsigned long | Zeit zwischen Qv_out_3 und Qv_out_4 (A2L-Name: Qv_td4) Qv_td4   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD4_EINH | string | h |
| STAT_QV_TD5_WERT | unsigned long | Zeit zwischen Qv_out_4 und Qv_out_5 (A2L-Name: Qv_td5) Qv_td5   Einheit: h   Min: 0 Max: 65535 |
| STAT_QV_TD5_EINH | string | h |
| STAT_QVC_STATUS_1_WERT | real | Ausgang fÃ¼r SchluesselgroeÃŸe 1 (A2L-Name: Qvc_status_1) Qvc_status_1   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QVC_STATUS_1_EINH | string | percent |
| STAT_QVC_STATUS_2_WERT | real | Ausgang fÃ¼r SchluesselgroeÃŸe 2 (A2L-Name: Qvc_status_2) Qvc_status_2   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QVC_STATUS_2_EINH | string | percent |
| STAT_QVC_STATUS_3 | unsigned long | Ausgang fÃ¼r SchluesselgroeÃŸe 3 (A2L-Name: Qvc_status_3) Qvc_status_3   Min: 0 Max: 255 |
| STAT_QVC_STATUS_4 | long | Ausgang fÃ¼r SchluesselgroeÃŸe 4 (A2L-Name: Qvc_status_4) Qvc_status_4   Min: -128 Max: 127 |
| STAT_QV_NV_ZH | unsigned long | Anzahl der Hystereseauswertungen (A2L-Name: Qv_nv_zh) Qv_nv_zh   Min: 0 Max: 4294967295 |
| STAT_QV_NV_EZM_WERT | real | Mittlerer Fehler fuer gesamte Hystereseberechnung (A2L-Name: Qv_nv_ezm) Qv_nv_ezm   Min: 0 Max: 1 |
| STAT_QV_H2O_WERT | real | Bisheriger Wasserverlust Batterie (A2L-Name: Qv_h2o) Qv_h2o   Min: 0 Max: 63.999 |
| STAT_QV_H2OQUALI_WERT | real | Qualitaetswert fuer Wasserverlust Batterie (A2L-Name: Qv_h2oquali) Qv_h2oquali   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_QV_H2OQUALI_EINH | string | percent |
| STAT_ST_QVC1 | unsigned long | Statuswort (A2L-Name: St_qvc1) Bedeutung: - 0: Wasserverlust O.K. - 1: Wasserverlust zu hoch St_qvc1   Min: 0 Max: 255 |
| STAT_QV_H2OSTATUS | unsigned long | Status fuer Entwicklung Wasserverlust (A2L-Name: Qv_h2ostatus) Qv_h2ostatus   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-geninfo"></a>
### _STATUS_GENINFO

0x22401B _STATUS_GENINFO Infospeicher Generatordiagnose erweitert auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DGENUB1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) ST_DGENUB1   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB1_EINH | string | V |
| STAT_DGENUB2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) ST_DGENUB2   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB2_EINH | string | V |
| STAT_DGENUBNZ_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) ST_DGENUBNZ   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUBNZ_EINH | string | V |
| STAT_DGENUBERR1 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit X (z.B. 2 min) 1BIT IDENTICAL |
| STAT_DGENUBERR2 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit Y (z.B. 10 min) 1BIT IDENTICAL |
| STAT_DGENUBERRNZ | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit Z (z.B. 30 min) 1BIT IDENTICAL |
| STAT_DGENUGEN1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) ST_DGENUGEN1   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN1_EINH | string | V |
| STAT_DGENUGEN2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) ST_DGENUGEN2   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN2_EINH | string | V |
| STAT_DGENUGENNZ_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) ST_DGENUGENNZ   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGENNZ_EINH | string | V |
| STAT_DGENUGENERR1 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit X (z.B. 2 min) 1BIT IDENTICAL |
| STAT_DGENUGENERR2 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit Y (z.B. 10 min) 1BIT IDENTICAL |
| STAT_DGENUGENERRNZ | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit Z (z.B. 30 min) 1BIT IDENTICAL |
| STAT_DGENGRENZ1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) ST_DGENGRENZ1   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ1_EINH | string | A |
| STAT_DGENGRENZ2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) ST_DGENGRENZ2   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ2_EINH | string | A |
| STAT_DGENGRENZNZ_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) ST_DGENGRENZNZ   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZNZ_EINH | string | A |
| STAT_DGENGRENZERR1 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit X (z.B. 2 min) 1BIT IDENTICAL |
| STAT_DGENGRENZERR2 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit Y (z.B. 10 min) 1BIT IDENTICAL |
| STAT_DGENGRENZERRNZ | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit Z (z.B. 30 min) 1BIT IDENTICAL |
| STAT_DGENUB1_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz ST_DGENUB1_MD1   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB1_MD1_EINH | string | V |
| STAT_DGENUB2_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz ST_DGENUB2_MD1   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB2_MD1_EINH | string | V |
| STAT_DGENUBNZ_MD1_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz ST_DGENUBNZ_MD1   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUBNZ_MD1_EINH | string | V |
| STAT_DGENUBERR1_MD1 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUBERR2_MD1 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUBERRNZ_MD1 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGEN1_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz ST_DGENUGEN1_MD1   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN1_MD1_EINH | string | V |
| STAT_DGENUGEN2_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz ST_DGENUGEN2_MD1   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN2_MD1_EINH | string | V |
| STAT_DGENUGENNZ_MD1_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz ST_DGENUGENNZ_MD1   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGENNZ_MD1_EINH | string | V |
| STAT_DGENUGENERR1_MD1 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGENERR2_MD1 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGENERRNZ_MD1 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZ1_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz ST_DGENGRENZ1_MD1   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ1_MD1_EINH | string | A |
| STAT_DGENGRENZ2_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz ST_DGENGRENZ2_MD1   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ2_MD1_EINH | string | A |
| STAT_DGENGRENZNZ_MD1_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz ST_DGENGRENZNZ_MD1   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZNZ_MD1_EINH | string | A |
| STAT_DGENGRENZERR1_MD1 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit X (z.B. 2 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZERR2_MD1 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit Y (z.B. 10 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZERRNZ_MD1 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit Z (z.B. 30 min) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUB1_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz ST_DGENUB1_MD2   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB1_MD2_EINH | string | V |
| STAT_DGENUB2_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz ST_DGENUB2_MD2   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUB2_MD2_EINH | string | V |
| STAT_DGENUBNZ_MD2_WERT | real | Mittelwert der Batteriespannung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz ST_DGENUBNZ_MD2   Einheit: V   Min: 0 Max: 6173.397 |
| STAT_DGENUBNZ_MD2_EINH | string | V |
| STAT_DGENUBERR1_MD2 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUBERR2_MD2 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUBERRNZ_MD2 | unsigned long | Fehlerstatus zur Batteriespannung Ã¼ber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGEN1_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz ST_DGENUGEN1_MD2   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGEN1_MD2_EINH | string | V |
| STAT_DGENUGEN2_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz ST_DGENUGEN2_MD2   Einheit: V   Min: 0 Max: 25.5 |
| STAT_DGENUGEN2_MD2_EINH | string | V |
| STAT_DGENUGENNZ_MD2_WERT | real | Mittelwert der Generatorsollspannung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz ST_DGENUGENNZ_MD2   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_DGENUGENNZ_MD2_EINH | string | V |
| STAT_DGENUGENERR1_MD2 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGENERR2_MD2 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENUGENERRNZ_MD2 | unsigned long | Fehlerstatus zur Generatorsollspannung Ã¼ber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZ1_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz ST_DGENGRENZ1_MD2   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ1_MD2_EINH | string | A |
| STAT_DGENGRENZ2_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz ST_DGENGRENZ2_MD2   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZ2_MD2_EINH | string | A |
| STAT_DGENGRENZNZ_MD2_WERT | real | Mittelwert der Erregerstrombegrenzung ueber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz ST_DGENGRENZNZ_MD2   Einheit: A   Min: 0 Max: 31.875 |
| STAT_DGENGRENZNZ_MD2_EINH | string | A |
| STAT_DGENGRENZERR1_MD2 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit X (z.B. 2 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZERR2_MD2 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit Y (z.B. 10 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_DGENGRENZERRNZ_MD2 | unsigned long | Fehlerstatus zur Erregerstrombegrenzung Ã¼ber applizierbare Zeit Z (z.B. 30 min) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMRUHVERL_MD1 | unsigned long | PM Ruhestromverletzung zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMBATT_MD1 | unsigned long | Fehler PM Batterie zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMBN_MD1 | unsigned long | Fehler PM Bordnetz zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSDGLOB_MD1 | unsigned long | Fehler BSD global zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_4_MD1 | unsigned long | Kommunikation QLT zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_3_MD1 | unsigned long | Kommunikation EWAPU zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_0_MD1 | unsigned long | Kommunikation IBS zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENREGUPL_MD1 | unsigned long | Generatorfehler Reglertyp unplausibel zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENHTB_MD1 | unsigned long | Generatorfehler Hochtemperatur berechnet zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENELB_MD1 | unsigned long | Generatorfehler elektrisch berechnet zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENKOMM_MD1 | unsigned long | Kommunikation Generator zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENUPL_MD1 | unsigned long | Generatorfehler Typ unplausibel zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENHT_MD1 | unsigned long | Generatorfehler Hochtemperatur (Bitauswertung) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENMECH_MD1 | unsigned long | Generatorfehler mechanisch (Bitauswertung) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENEL_MD1 | unsigned long | Generatorfehler elektrisch (Bitauswertung) zu 1. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMRUHVERL_MD2 | unsigned long | PM Ruhestromverletzung zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMBATT_MD2 | unsigned long | Fehler PM Batterie zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_PMBN_MD2 | unsigned long | Fehler PM Bordnetz zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSDGLOB_MD2 | unsigned long | Fehler BSD global zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_4_MD2 | unsigned long | Kommunikation QLT zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_3_MD2 | unsigned long | Kommunikation EWAPU zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_BSD_0_MD2 | unsigned long | Kommunikation IBS zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENREGUPL_MD2 | unsigned long | Generatorfehler Reglertyp unplausibel zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENHTB_MD2 | unsigned long | Generatorfehler Hochtemperatur berechnet zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENELB_MD2 | unsigned long | Generatorfehler elektrisch berechnet zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENKOMM_MD2 | unsigned long | Kommunikation Generator zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENUPL_MD2 | unsigned long | Generatorfehler Typ unplausibel zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENHT_MD2 | unsigned long | Generatorfehler Hochtemperatur (Bitauswertung) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENMECH_MD2 | unsigned long | Generatorfehler mechanisch (Bitauswertung) zu 2. Messdatensatz 1BIT IDENTICAL |
| STAT_FI_GENEL_MD2 | unsigned long | Generatorfehler elektrisch (Bitauswertung) zu 2. Messdatensatz 1BIT IDENTICAL |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-igrinfo"></a>
### _STATUS_IGRINFO

0x224016 _STATUS_IGRINFO Infospeicher Intelligente Generator Regelung (IGR) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_IGR1_BITS7 | unsigned long | Begrenzung 2 1BIT IDENTICAL |
| STAT_IGR1_BITS6 | unsigned long | Begrenzung 1 1BIT IDENTICAL |
| STAT_IGR1_BITS5 | unsigned long | Regeneration 1BIT IDENTICAL |
| STAT_IGR1_BITS4 | unsigned long | IGR-Medium 1BIT IDENTICAL |
| STAT_IGR1_BITS3 | unsigned long | IGR-High 1BIT IDENTICAL |
| STAT_IGR1_BITS2 | unsigned long | IGR-Low 1BIT IDENTICAL |
| STAT_IGR1_BITS1 | unsigned long | Diagnosejob gesetzt 1BIT IDENTICAL |
| STAT_IGR1_BITS0 | unsigned long | IGR codiert 1BIT IDENTICAL |
| STAT_IGR2_BITS7 | unsigned long | Begrenzung Res 1BIT IDENTICAL |
| STAT_IGR2_BITS6 | unsigned long | Begrenzung DS 1BIT IDENTICAL |
| STAT_IGR2_BITS5 | unsigned long | Begrenzung TS 1BIT IDENTICAL |
| STAT_IGR2_BITS4 | unsigned long | Begrenzung TB 1BIT IDENTICAL |
| STAT_IGR2_BITS3 | unsigned long | Begrenzung M 1BIT IDENTICAL |
| STAT_IGR2_BITS2 | unsigned long | Begrenzung G 1BIT IDENTICAL |
| STAT_IGR2_BITS1 | unsigned long | Begrenzung W 1BIT IDENTICAL |
| STAT_IGR2_BITS0 | unsigned long | Begrenzung L 1BIT IDENTICAL |
| STAT_IGR3_BITS7 | unsigned long | IGR Res2 1BIT IDENTICAL |
| STAT_IGR3_BITS6 | unsigned long | IGR Res1 1BIT IDENTICAL |
| STAT_IGR3_BITS5 | unsigned long | IGR-Hi Aktiv 1BIT IDENTICAL |
| STAT_IGR3_BITS4 | unsigned long | IGR-Med Aktiv 1BIT IDENTICAL |
| STAT_IGR3_BITS3 | unsigned long | IGR-Low Aktiv 1BIT IDENTICAL |
| STAT_IGR3_BITS2 | unsigned long | IGR-Hi Enabled 1BIT IDENTICAL |
| STAT_IGR3_BITS1 | unsigned long | IGR-Med Enabled 1BIT IDENTICAL |
| STAT_IGR3_BITS0 | unsigned long | IGR-Low Enabled 1BIT IDENTICAL |
| STAT_IGR_PR1 | unsigned long | Level BN Soll 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_PR2 | unsigned long | Level Soll 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_ANTL_WERT | real | Anteil Low 2BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.9969482421875 |
| STAT_IGR_ANTL_EINH | string | percent |
| STAT_IGR_ANTM_WERT | real | Anteil Medium 2BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.9969482421875 |
| STAT_IGR_ANTM_EINH | string | percent |
| STAT_IGR_ANTH_WERT | real | Anteil High 2BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.9969482421875 |
| STAT_IGR_ANTH_EINH | string | percent |
| STAT_IGR_11 | unsigned long | Anteil 11 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_12 | unsigned long | Anteil 12 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_M_AGO_WERT | unsigned long | Abstand zu letzter Mediumphase 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_IGR_M_AGO_EINH | string | Minute |
| STAT_IGR_H_AGO_WERT | unsigned long | Abstand zu letzter Highphase 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_IGR_H_AGO_EINH | string | Minute |
| STAT_IGR_BSA1 | unsigned long | Zaehler Low 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_IGR_QLAD_WERT | real | Bilanz Low 2BYTE_in_0bis19088Ah   Einheit: Ah   Min: 0 Max: 19088.1 |
| STAT_IGR_QLAD_EINH | string | Ah |
| STAT_IGR_QLAD_M_WERT | long | Bilanz Medium 1BYTE in -128 bis +127 Ah   Einheit: Ah   Min: -128 Max: 127 |
| STAT_IGR_QLAD_M_EINH | string | Ah |
| STAT_IGR_QELAD_WERT | real | Bilanz High 2BYTE_in_0bis19088Ah   Einheit: Ah   Min: 0 Max: 19088.1 |
| STAT_IGR_QELAD_EINH | string | Ah |
| STAT_IGR_TMED_WERT | unsigned long | Dauer letzte Mediumphase 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_IGR_TMED_EINH | string | Minute |
| STAT_IGR_THIGH_WERT | unsigned long | Dauer letzte Highphase 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_IGR_THIGH_EINH | string | Minute |
| STAT_IGR_TCODE | unsigned long | Dauer iGR-Codiert 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_IGR_HIGH | unsigned long | Zaehler High 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_REG_ZR | unsigned long | Einfachzaehler 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_REG_SEIT_WERT | unsigned long | Zeit seit letzter R 1BYTE_in_0bis255h   Einheit: h   Min: 0 Max: 255 |
| STAT_REG_SEIT_EINH | string | h |
| STAT_REG_DAUER_WERT | unsigned long | Dauer letzte R 1BYTE_in_0bis255h   Einheit: h   Min: 0 Max: 255 |
| STAT_REG_DAUER_EINH | string | h |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-leminfo"></a>
### _STATUS_LEMINFO

0x224017 _STATUS_LEMINFO Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZR_USTAT_A | unsigned long | Haeufigkeitszaehler Zr_ustat_A 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_USTAT_B | unsigned long | Haeufigkeitszaehler Zr_ustat_B 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_USTAT_C | unsigned long | Haeufigkeitszaehler Zr_ustat_C 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_USTAT_D | unsigned long | Haeufigkeitszaehler Zr_ustat_D 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_USTAT_E | unsigned long | Haeufigkeitszaehler Zr_ustat_E 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_USTAT_F | unsigned long | Haeufigkeitszaehler Zr_ustat_F 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_USTAT_G | unsigned long | Haeufigkeitszaehler Zr_ustat_G 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_UBSTUFE_L | unsigned long | Haeufigkeitszaehler Zr_ubstufe_L 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_UBSTUFE_H | unsigned long | Haeufigkeitszaehler Zr_ubstufe_H 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_UQUALI_A | unsigned long | Haeufigkeitszaehler Zr_uquali_A 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_UQUALI_B | unsigned long | Haeufigkeitszaehler Zr_uquali_B 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_UQUALI_C | unsigned long | Haeufigkeitszaehler Zr_uquali_C 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ZR_IERRLLRED | unsigned long | Haeufigkeitszaehler Zr_ierrllred 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_TM_IERRLLRED_WERT | unsigned long | Mittelwert Tm_ierrllred 1BYTE_in_0bis255s   Einheit: s   Min: 0 Max: 255 |
| STAT_TM_IERRLLRED_EINH | string | second |
| STAT_ZR_IERRTRED | unsigned long | Haeufigkeitszaehler Zr_ierrtred 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_TM_IERRTRED_WERT | unsigned long | Mittelwert Tm_ierrtred 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |
| STAT_TM_IERRTRED_EINH | string | second |
| STAT_TM_ENTLFUNK_WERT | unsigned long | Mittelwert Tm_entlfunk 1BYTE_in_0bis255s   Einheit: s   Min: 0 Max: 255 |
| STAT_TM_ENTLFUNK_EINH | string | second |
| STAT_ZR_ENTLFUNK | unsigned long | Haeufigkeitszaehler Zr_entlfunk 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_ENTLFUNKVOLL | unsigned long | Haeufigkeitszaehler Zr_entlfunkvoll 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_ENTLFUNKNIX | unsigned long | Haeufigkeitszaehler Zr_entlfunknix 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_ENTLFUNKTEIL | unsigned long | Haeufigkeitszaehler Zr_entlfunkteil 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_TM_ENTLSICH_WERT | unsigned long | Mittelwert Tm_entlsich 1BYTE_in_0bis255s   Einheit: s   Min: 0 Max: 255 |
| STAT_TM_ENTLSICH_EINH | string | second |
| STAT_ZR_ENTLSICH | unsigned long | Haeufigkeitszaehler Zr_entelsich 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZR_ENTLSICHVOLL | unsigned long | Haeufigkeitszaehler Zr_entelsichvoll 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-msainfo"></a>
### _STATUS_MSAINFO

0x224018 _STATUS_MSAINFO Infospeicher Motor-Start/Stop Automatik (MSA) auslesen (nur 4-Zylinder-N43  nicht 6-Zylinder-N53/N54) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LADUNGSMENGE_GESAMT_WERT | real | Kumulierte, verbrauchte Ladungsmenge 2BYTE_in_0bis19088Ah   Einheit: Ah   Min: 0 Max: 19088.1 |
| STAT_LADUNGSMENGE_GESAMT_EINH | string | Ah |
| STAT_ANZAHL_MOTORSTART_GESAMT | unsigned long | Gesamtzahl Starts 3BYTE in 0 bis 16777214   Min: 0 Max: 16777214 |
| STAT_ANZAHL_MSASTART_GESAMT | unsigned long | Anzahl MSA Starts 3BYTE in 0 bis 16777214   Min: 0 Max: 16777214 |
| STAT_BATTSPG_DSOC_INTERVALL1_STOPDAUER_UNTER_10S_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer(10s) mit DSOC zw K_DSOCMSADG1 und K_DSOCMSADG2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL1_STOPDAUER_UNTER_10S_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL2_STOPDAUER_UNTER_10S_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer(10s) mit DSOC zw K_DSOCMSADG2 und K_DSOCMSADG3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL2_STOPDAUER_UNTER_10S_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL3_STOPDAUER_UNTER_10S_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer(10s) mit DSOC zw K_DSOCMSADG3 und K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL3_STOPDAUER_UNTER_10S_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL4_STOPDAUER_UNTER_10S_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer(10s) mit DSOC groesser K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL4_STOPDAUER_UNTER_10S_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL1_STOPDAUER_UEBER_10S_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer)10s) mit DSOC zw K_DSOCMSADG1 und K_DSOCMSADG2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL1_STOPDAUER_UEBER_10S_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL2_STOPDAUER_UEBER_10S_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer)10s) mit DSOC zw K_DSOCMSADG2 und K_DSOCMSADG3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL2_STOPDAUER_UEBER_10S_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL3_STOPDAUER_UEBER_10S_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer)10s) mit DSOC zw K_DSOCMSADG3 und K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL3_STOPDAUER_UEBER_10S_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL4_STOPDAUER_UEBER_10S_WERT | real | gemittelte Spannungslage bei MSA-Starts (Dauer)10s) mit DSOC groesser K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL4_STOPDAUER_UEBER_10S_EINH | string | V |
| STAT_ZEIT_IN_MSA_GESAMT_WERT | unsigned long | Zeit in MSA 4BYTE in 0 bis 4294967294s   Einheit: s   Min: 0 Max: 4294967294 |
| STAT_ZEIT_IN_MSA_GESAMT_EINH | string | second |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_UNTER_5S_WERT | real | Relative Haeufigkeit der Stops unter 5s 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_UNTER_5S_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_UNTER_10S_WERT | real | Relative Haeufigkeit der Stops unter 10s 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_UNTER_10S_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_UNTER_45S_WERT | real | Relative Haeufigkeit der Stops unter 45s 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_UNTER_45S_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_UEBER_45S_WERT | real | Relative Haeufigkeit der Stops Ã¼ber 45s 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_UEBER_45S_EINH | string | percent |
| STAT_MSA_STOP_1_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 1 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_1_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_1_DELTA_KM_BIT_WERT | unsigned long | Delta km-Stand bei MSA-Stop 1 2BYTE_in_0bis65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_1_DELTA_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_1_DAUER_WERT | unsigned long | Dauer MSA-Stop 1 MSA_1BYTE_in_0bis1524s   Einheit: s   Min: 0 Max: 1524 |
| STAT_MSA_STOP_1_DAUER_EINH | string | s |
| STAT_MSA_STOP_1_AH_VERBRAUCH_WERT | unsigned long | verbrauchte Ladungsmenge MSA-Stop 1 MSA_1BYTE_in_0bis25400As   Einheit: As   Min: 0 Max: 25400 |
| STAT_MSA_STOP_1_AH_VERBRAUCH_EINH | string | As |
| STAT_MSA_STOP_1_DSOC | unsigned long | D_SoC bei MSA-Stop 1 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_MSA_STOP_2_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_2_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_2_DELTA_KM_BIT_WERT | unsigned long | Delta km-Stand bei MSA-Stop 2 2BYTE_in_0bis65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_2_DELTA_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_2_DAUER_WERT | unsigned long | Dauer MSA-Stop 2 MSA_1BYTE_in_0bis1524s   Einheit: s   Min: 0 Max: 1524 |
| STAT_MSA_STOP_2_DAUER_EINH | string | s |
| STAT_MSA_STOP_2_AH_VERBRAUCH_WERT | unsigned long | verbrauchte Ladungsmenge MSA-Stop 2 MSA_1BYTE_in_0bis25400As   Einheit: As   Min: 0 Max: 25400 |
| STAT_MSA_STOP_2_AH_VERBRAUCH_EINH | string | As |
| STAT_MSA_STOP_2_DSOC | unsigned long | D_SoC bei MSA-Stop 2 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_MSA_STOP_3_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_3_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_3_DELTA_KM_BIT_WERT | unsigned long | Delta km-Stand bei MSA-Stop 3 2BYTE_in_0bis65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_3_DELTA_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_3_DAUER_WERT | unsigned long | Dauer MSA-Stop 3 MSA_1BYTE_in_0bis1524s   Einheit: s   Min: 0 Max: 1524 |
| STAT_MSA_STOP_3_DAUER_EINH | string | s |
| STAT_MSA_STOP_3_AH_VERBRAUCH_WERT | unsigned long | verbrauchte Ladungsmenge MSA-Stop 3 MSA_1BYTE_in_0bis25400As   Einheit: As   Min: 0 Max: 25400 |
| STAT_MSA_STOP_3_AH_VERBRAUCH_EINH | string | As |
| STAT_MSA_STOP_3_DSOC | unsigned long | D_SoC bei MSA-Stop 3 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_URSACHE_AV_VORHER_1_TEXT | string | vorletzter AV 1 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AV_VORHER_1_WERT | int |  |
| STAT_URSACHE_LETZTER_AV_TEXT | string | letzter AV MSA 4BIT URSACHE AV |
| STAT_URSACHE_LETZTER_AV_WERT | int |  |
| STAT_URSACHE_AV_VORHER_3_TEXT | string | vorletzter AV 3 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AV_VORHER_3_WERT | int |  |
| STAT_URSACHE_AV_VORHER_2_TEXT | string | vorletzter AV 2 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AV_VORHER_2_WERT | int |  |
| STAT_URSACHE_AV_VORHER_5_TEXT | string | vorletzter AV 5 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AV_VORHER_5_WERT | int |  |
| STAT_URSACHE_AV_VORHER_4_TEXT | string | vorletzter AV 4 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AV_VORHER_4_WERT | int |  |
| STAT_URSACHE_AV_VORHER_7_TEXT | string | vorletzter AV 7 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AV_VORHER_7_WERT | int |  |
| STAT_URSACHE_AV_VORHER_6_TEXT | string | vorletzter AV 6 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AV_VORHER_6_WERT | int |  |
| STAT_URSACHE_AV_VORHER_9_TEXT | string | vorletzter AV 9 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AV_VORHER_9_WERT | int |  |
| STAT_URSACHE_AV_VORHER_8_TEXT | string | vorletzter AV 8 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AV_VORHER_8_WERT | int |  |
| STAT_URSACHE_AV_VORHER_11_TEXT | string | vorletzter AV 11 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AV_VORHER_11_WERT | int |  |
| STAT_URSACHE_AV_VORHER_10_TEXT | string | vorletzter AV 10 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AV_VORHER_10_WERT | int |  |
| STAT_URSACHE_AV_VORHER_13_TEXT | string | vorletzter AV 13 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AV_VORHER_13_WERT | int |  |
| STAT_URSACHE_AV_VORHER_12_TEXT | string | vorletzter AV 12 MSA 4BIT URSACHE AV |
| STAT_URSACHE_AV_VORHER_12_WERT | int |  |
| STAT_URSACHE_EA_VORHER_3_TEXT | string | EA vor 3 MSA 2BIT URSACHE EA |
| STAT_URSACHE_EA_VORHER_3_WERT | int |  |
| STAT_URSACHE_EA_VORHER_2_TEXT | string | EA vor 2 MSA 2BIT URSACHE EA |
| STAT_URSACHE_EA_VORHER_2_WERT | int |  |
| STAT_URSACHE_EA_VORHER_1_TEXT | string | EA vor 1 MSA 2BIT URSACHE EA |
| STAT_URSACHE_EA_VORHER_1_WERT | int |  |
| STAT_URSACHE_EA_TEXT | string | letzter EA MSA 2BIT URSACHE EA |
| STAT_URSACHE_EA_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ueberdrehzahl"></a>
### _STATUS_UEBERDREHZAHL

0x225FF6 _STATUS_UEBERDREHZAHL Ueberdrehzahlspeicherung (Ueberdrehsicherung) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_N_MAX_WERT | unsigned long | Maximale Drehzahl N_MAX   Einheit: rpm   Min: 1 Max: 8160 |
| STAT_N_MAX_EINH | string | rpm |
| STAT_ZEIT_WERT | real | Motorbetriebszeit bei maximaler Drehzahl TRT_N_MAX   Einheit: h   Min: 0 Max: 119304.6471 |
| STAT_ZEIT_EINH | string | h |
| STAT_ANZAHL | unsigned long | Anzahl Ereignisse bei maximaler Drehzahl CTR_N_MAX   Min: 0 Max: 255 |
| STAT_KM_STAND_WERT | unsigned long | Kilometerstand bei maximaler Drehzahl CTR_KM_N_MAX   Einheit: km   Min: 0 Max: 655350 |
| STAT_KM_STAND_EINH | string | km |
| STAT_GRADIENT_N_WERT | long | Drehzahlgradient bei maximaler Drehzahl N_GRD_N_MAX   Einheit: rpm   Min: -4096 Max: 4064 |
| STAT_GRADIENT_N_EINH | string | rpm |
| STAT_GESCHWINDIGKEIT_WERT | unsigned long | Geschwindigkeit bei maximaler Drehzahl VS_N_MAX   Einheit: km/h   Min: 0 Max: 255 |
| STAT_GESCHWINDIGKEIT_EINH | string | kmperh |
| STAT_PEDALWERT_MITTELWERT_WERT | real | Pedalwert bei maximaler Drehzahl PV_AV_N_MAX   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_PEDALWERT_MITTELWERT_EINH | string | percent |
| STAT_UNTERSETZUNG | unsigned long | Untersetzung N_MAX/Geschwindigkeit bei maximaler Drehzahl GEAR_EF_N_MAX   Min: 0 Max: 255 |
| STAT_KUPPLUNG | unsigned long | Status Kupplungsschalter bei maximaler Drehzahl LV_CS_N_MAX   Min: 0 Max: 1 |
| STAT_ZEIT_SUMMIERT_WERT | real | Summe aller Zeiten bei maximaler Drehzahl T_SUM_N_MAX   Einheit: s   Min: 0 Max: 6553.5 |
| STAT_ZEIT_SUMMIERT_EINH | string | s |
| STAT_ZEIT_MAX_WERT | real | Zeit bei maximaler Drehzahl T_N_MAX   Einheit: s   Min: 0 Max: 6553.5 |
| STAT_ZEIT_MAX_EINH | string | s |
| STAT_SCHUB_ABSCHALTUNG | unsigned long | Muster der Schubabschaltung bei maximaler Drehzahl NR_PAT_SCC_N_MAX   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-uebertemperatur"></a>
### _STATUS_UEBERTEMPERATUR

0x225FF3 _STATUS_UEBERTEMPERATUR Uebertemperatursicherung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TOIL_MAX_WERT | long | Maximale Oeltemperatur TOIL_MAX_WARN   Einheit: C   Min: -40 Max: 160 |
| STAT_TOIL_MAX_EINH | string | degreeC |
| STAT_VS_WERT | unsigned long | Geschwindigkeit bei maximaler Oeltemperatur VS_TOIL_MAX   Einheit: km/h   Min: 0 Max: 255 |
| STAT_VS_EINH | string | kmperh |
| STAT_N_WERT | unsigned long | Drehzahl bei maximaler Oeltemperatur N_TOIL_MAX   Einheit: rpm   Min: 0 Max: 8160 |
| STAT_N_EINH | string | rpm |
| STAT_GEAR | unsigned long | Gang bei maximaler Oeltemperatur GEAR_TOIL_MAX   Min: 0 Max: 255 |
| STAT_TQI_AV_WERT | real | Drehmoment bei maximaler Oeltemperatur TQI_AV_TOIL_MAX   Einheit: Nm   Min: -1024 Max: 1023.96875 |
| STAT_TQI_AV_EINH | string | Nm |
| STAT_TAM_WERT | real | Umgebungstemperatur bei maximaler Oeltemperatur TAM_TOIL_MAX   Einheit: C   Min: -48 Max: 142.5 |
| STAT_TAM_EINH | string | degreeC |
| STAT_CTR | unsigned long | Haeufigkeitszaehler Uebertemperatur CTR_TOIL_MAX   Min: 0 Max: 255 |
| STAT_TCO_WERT | real | Motortemperatur bei maximaler Oeltemperatur TCO_TOIL_MAX   Einheit: C   Min: -48 Max: 142.5 |
| STAT_TCO_EINH | string | degreeC |
| STAT_CTR_KM_WERT | unsigned long | Kilometerstand bei maximaler Oeltemperatur DIST_TOIL_MAX   Einheit: km   Min: 0 Max: 524280 |
| STAT_CTR_KM_EINH | string | km |
| STAT_PV_AV_WERT | real | Pedalwertgeber bei maximaler Oeltemperatur PV_AV_TOIL_MAX   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_PV_AV_EINH | string | percent |
| STAT_LV_CS | unsigned long | Status Kupplungsschalter bei maximaler Oeltemperatur LV_CS_TOIL_MAX   Min: 0 Max: 1 |
| STAT_WARN_THD_WERT | long | Uebertemperatur Schwellwert TOIL_THD_TOIL_MAX   Einheit: C   Min: -40 Max: 160 |
| STAT_WARN_THD_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-verbredinfo"></a>
### _STATUS_VERBREDINFO

0x22401D _STATUS_VERBREDINFO Verbraucherreduzierungsspeicher auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

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
| STAT_E2_TAG | unsigned long | Ereignis 2 Tag (Verbredinfo[5]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_MONAT | unsigned long | Ereignis 2 Monat (Verbredinfo[6]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_DAUER_WERT | unsigned long | Ereignis 2 Dauer der Verbraucherreduzierung (Verbredinfo[7]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E2_DAUER_EINH | string | Minute |
| STAT_E2_LRSA | unsigned long | Ereignis 2 Leistungsreduktionstufe A (Verbredinfo[8]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_LRSB | unsigned long | Ereignis 2 Leistungsreduktionstufe B (Verbredinfo[9]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_TAG | unsigned long | Ereignis 3 Tag (Verbredinfo[10]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_MONAT | unsigned long | Ereignis 3 Monat (Verbredinfo[11]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_DAUER_WERT | unsigned long | Ereignis 3 Dauer der Verbraucherreduzierung (Verbredinfo[12]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E3_DAUER_EINH | string | Minute |
| STAT_E3_LRSA | unsigned long | Ereignis 3 Leistungsreduktionstufe A (Verbredinfo[13]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_LRSB | unsigned long | Ereignis 3 Leistungsreduktionstufe B (Verbredinfo[14]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_TAG | unsigned long | Ereignis 4 Tag (Verbredinfo[15]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_MONAT | unsigned long | Ereignis 4 Monat (Verbredinfo[16]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_DAUER_WERT | unsigned long | Ereignis 4 Dauer der Verbraucherreduzierung (Verbredinfo[17]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E4_DAUER_EINH | string | Minute |
| STAT_E4_LRSA | unsigned long | Ereignis 4 Leistungsreduktionstufe A (Verbredinfo[18]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_LRSB | unsigned long | Ereignis 4 Leistungsreduktionstufe B (Verbredinfo[19]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ueberdrehzahl-reset"></a>
### _STEUERN_UEBERDREHZAHL_RESET

0x2E5FF604 _STEUERN_UEBERDREHZAHL_RESET Ueberdrehzahlspeicherung (Ueberdrehsicherung) loeschen Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RUECKSETZUNG_TEXT | string | Status der Ruecksetzung VERIFY_BYTE |
| STAT_RUECKSETZUNG_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-uebertemperatur-reset"></a>
### _STEUERN_UEBERTEMPERATUR_RESET

0x2E5FF304 _STEUERN_UEBERTEMPERATUR_RESET Uebertemperatursicherung loeschen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecu-config"></a>
### ECU_CONFIG

0x225FF2 ECU_CONFIG Variante auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AT | unsigned long | Automatik Getriebe  0=nicht vorhanden / 1=vorhanden LV_AT   Min: 0 Max: 1 |
| STAT_AC | unsigned long | Klimaanlage  0=nicht vorhanden / 1=vorhanden LV_VAR_ACIN   Min: 0 Max: 1 |
| STAT_AMT | unsigned long | SMG Sequentielles Manuelles Getriebe  0=nicht vorhanden / 1=vorhanden LV_VAR_AMT   Min: 0 Max: 1 |
| STAT_ARS | unsigned long | ARS Aktive Roll-Stabilisierung  0=nicht vorhanden / 1=vorhanden LV_VAR_ARS   Min: 0 Max: 1 |
| STAT_ASR | unsigned long | ASR Anti-Schlupf-Regelung  0=nicht vorhanden / 1=vorhanden LV_VAR_ASR   Min: 0 Max: 1 |
| STAT_BN | unsigned long | Bordnetz 2000  0=nicht vorhanden / 1=vorhanden LV_VAR_BN   Min: 0 Max: 1 |
| STAT_BN_MSW | unsigned long | Tempomat ueber CAN  0=nicht vorhanden / 1=vorhanden LV_VAR_BN_MSW   Min: 0 Max: 1 |
| STAT_DCC | unsigned long | Entfernungsueberwachung  0=nicht vorhanden / 1=vorhanden LV_VAR_DCC   Min: 0 Max: 1 |
| STAT_EBOX_CFA | unsigned long | E-Box-Luefter  0=nicht vorhanden / 1=vorhanden LV_VAR_EBOX_CFA   Min: 0 Max: 1 |
| STAT_ETCU | unsigned long | SMG/EGS Steuergeraet  0=nicht vorhanden / 1=vorhanden LV_VAR_ETCU   Min: 0 Max: 1 |
| STAT_ICL | unsigned long | Kombi ueber CAN  0=nicht vorhanden / 1=vorhanden LV_VAR_ICL   Min: 0 Max: 1 |
| STAT_MSW | unsigned long | Multifunktionslenkrad  0=nicht vorhanden / 1=vorhanden LV_VAR_MSW   Min: 0 Max: 1 |
| STAT_PSTE | unsigned long | Elektrische Lenkung  0=nicht vorhanden / 1=vorhanden LV_VAR_PSTE   Min: 0 Max: 1 |
| STAT_SOF | unsigned long | Soundklappe  0=nicht vorhanden / 1=vorhanden LV_VAR_SOF   Min: 0 Max: 1 |
| STAT_SOF_SWI | unsigned long | Sport-Taster  0=nicht vorhanden / 1=vorhanden CONF_SOF_SWI   Min: 0 Max: 2 |
| STAT_GEAR | unsigned long | Komfortstart  0=nicht vorhanden / 1=vorhanden LV_VAR_BN_GEAR_REV   Min: 0 Max: 1 |
| STAT_VEH | unsigned long | Fahrzeugvariante mit Power Modul (E60/E65) erkannt - nur BN 2000  0=nicht vorhanden / 1=vorhanden LV_VAR_VEH   Min: 0 Max: 1 |
| STAT_EF | unsigned long | Abgasklappe  0=nicht vorhanden / 1=vorhanden LV_VAR_EF   Min: 0 Max: 1 |
| STAT_ECRAS_UP | unsigned long | Kuehlerjalousie oben  0=nicht vorhanden / 1=vorhanden LV_VAR_ECRAS_UP   Min: 0 Max: 1 |
| STAT_RLY_ACCOUT | unsigned long | Klimarelais  0=nicht vorhanden / 1=vorhanden LV_VAR_RLY_ACCOUT   Min: 0 Max: 1 |
| STAT_RLY_ST | unsigned long | Starterrelais  0=nicht vorhanden / 1=vorhanden LV_VAR_RLY_ST   Min: 0 Max: 1 |
| STAT_ASR3 | unsigned long | ASR3 Steuergeraet  0=nicht vorhanden / 1=vorhanden LV_VAR_ASR_3   Min: 0 Max: 1 |
| STAT_BN_LDM | unsigned long | Laengs-Dynamik-Management  0=nicht vorhanden / 1=vorhanden LV_VAR_BN_LDM   Min: 0 Max: 1 |
| STAT_BN_LTG_HDLP_L | unsigned long | Lampenzustand  0=nicht vorhanden / 1=vorhanden LV_VAR_BN_LTG_HDLP_L   Min: 0 Max: 1 |
| STAT_LSH_DOWN | unsigned long | Lambdasonde hinter Katalysator  0=nicht vorhanden / 1=vorhanden LV_VAR_LSH_DOWN   Min: 0 Max: 1 |
| STAT_LSH_UP | unsigned long | Lambdasonde vor Katalysator  0=nicht vorhanden / 1=vorhanden LV_VAR_LSH_UP   Min: 0 Max: 1 |
| STAT_ASR_4 | unsigned long | ASR4 Steuergeraet  0=nicht vorhanden / 1=vorhanden LV_VAR_ASR_4   Min: 0 Max: 1 |
| STAT_MAF | unsigned long | Luftmassenmesser  0=nicht vorhanden / 1=vorhanden LV_VAR_MAF   Min: 0 Max: 1 |
| STAT_PSTE_2 | unsigned long | AFS Active-Front-Steering  0=nicht vorhanden / 1=vorhanden LV_VAR_PSTE_2   Min: 0 Max: 1 |
| STAT_BN_EFP | unsigned long | Elektrische Kraftstoffpumpe ueber CAN  0=nicht vorhanden / 1=vorhanden LV_VAR_BN_EFP   Min: 0 Max: 1 |
| STAT_SENS_BAT_SMT_DET | unsigned long | Intelligenter Batteriesensor  0=nicht vorhanden / 1=vorhanden LV_SENS_BAT_SMT_DET   Min: 0 Max: 1 |
| STAT_BN_TRL | unsigned long | Anhaengermodul  0=nicht vorhanden / 1=vorhanden LV_VAR_BN_TRL   Min: 0 Max: 1 |
| STAT_ECRAS_DOWN | unsigned long | Kuehlerjalousie unten  0=nicht vorhanden / 1=vorhanden LV_VAR_ECRAS_DOWN   Min: 0 Max: 1 |
| STAT_NOX | unsigned long | NOx-Sensor  0=nicht vorhanden / 1=vorhanden LV_VAR_NOX   Min: 0 Max: 1 |
| STAT_STST | unsigned long | Start-Stop-Automatik (nur 4-Zylinder-N43  nicht 6-Zylinder-N53/N54)  0=nicht vorhanden / 1=vorhanden LV_VAR_STST   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ecu-config-reset"></a>
### ECU_CONFIG_RESET

0x2E5FF204 ECU_CONFIG_RESET Variante loeschen Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AT_WERT | unsigned long | Automatik Getriebe LV_AT   Min: 0 Max: 1 |
| STAT_AC_WERT | unsigned long | Klimaanlage LV_VAR_ACIN   Min: 0 Max: 1 |
| STAT_AMT_WERT | unsigned long | SMG Sequentielles Manuelles Getriebe LV_VAR_AMT   Min: 0 Max: 1 |
| STAT_ARS_WERT | unsigned long | ARS Aktive Roll-Stabilisierung LV_VAR_ARS   Min: 0 Max: 1 |
| STAT_ASR_WERT | unsigned long | ASR Anti Schlupf Regelung LV_VAR_ASR   Min: 0 Max: 1 |
| STAT_BN_MSW_WERT | unsigned long | Tempomat ueber CAN LV_VAR_BN_MSW   Min: 0 Max: 1 |
| STAT_DCC_WERT | unsigned long | Entfernungsueberwachung LV_VAR_DCC   Min: 0 Max: 1 |
| STAT_EBOX_CFA_WERT | unsigned long | E-Box-Luefter LV_VAR_EBOX_CFA   Min: 0 Max: 1 |
| STAT_ETCU_WERT | unsigned long | SMG/EGS Steuergeraet LV_VAR_ETCU   Min: 0 Max: 1 |
| STAT_ICL_WERT | unsigned long | Kombi ueber CAN LV_VAR_ICL   Min: 0 Max: 1 |
| STAT_MSW_WERT | unsigned long | Multifunktionslenkrad LV_VAR_MSW   Min: 0 Max: 1 |
| STAT_PSTE_WERT | unsigned long | Elektrische Lenkung LV_VAR_PSTE   Min: 0 Max: 1 |
| STAT_SOF_WERT | unsigned long | Soundklappe LV_VAR_SOF   Min: 0 Max: 1 |
| STAT_SOF_SWI_WERT | unsigned long | Sport-Taster CONF_SOF_SWI   Min: 0 Max: 1 |
| STAT_GEAR_WERT | unsigned long | Komfortstart LV_VAR_BN_GEAR_REV   Min: 0 Max: 1 |
| STAT_EF_WERT | unsigned long | Abgasklappe LV_VAR_EF   Min: 0 Max: 1 |
| STAT_ECRAS_UP_WERT | unsigned long | Kuehlerjalousie oben LV_VAR_ECRAS_UP   Min: 0 Max: 1 |
| STAT_RLY_ACCOUT_WERT | unsigned long | Klimarelais LV_VAR_RLY_ACCOUT   Min: 0 Max: 1 |
| STAT_RLY_ST_WERT | unsigned long | Starterrelais LV_VAR_RLY_ST   Min: 0 Max: 1 |
| STAT_ASR3_WERT | unsigned long | ASR3 Steuergeraet LV_VAR_ASR_3   Min: 0 Max: 1 |
| STAT_BN_LDM_WERT | unsigned long | Laengs-Dynamik-Management LV_VAR_BN_LDM   Min: 0 Max: 1 |
| STAT_BN_LTG_HDLP_L_WERT | unsigned long | Lampenzustand LV_VAR_BN_LTG_HDLP_L   Min: 0 Max: 1 |
| STAT_LSH_DOWN_WERT | unsigned long | Lambdasonde hinter Katalysator LV_VAR_LSH_DOWN   Min: 0 Max: 1 |
| STAT_LSH_UP_WERT | unsigned long | Lambdasonde vor Katalysator LV_VAR_LSH_UP   Min: 0 Max: 1 |
| STAT_ASR_4_WERT | unsigned long | ASR4 Steuergeraet LV_VAR_ASR_4   Min: 0 Max: 1 |
| STAT_PST_2_WERT | unsigned long | AFS Active-Front-Steering LV_VAR_PSTE_2   Min: 0 Max: 1 |
| STAT_BN_EFP_WERT | unsigned long | Elektrische Kraftstoffpumpe ueber CAN LV_VAR_BN_EFP   Min: 0 Max: 1 |
| STAT_SENS_BAT_SMT_DET_WERT | unsigned long | Intelligenter Batteriesensor LV_SENS_BAT_SMT_DET   Min: 0 Max: 1 |
| STAT_BN_TRL_WERT | unsigned long | Anhaengermodul LV_VAR_BN_TRL   Min: 0 Max: 1 |
| STAT_NOX_WERT | unsigned long | NOx-Sensor LV_VAR_NOX   Min: 0 Max: 1 |
| STAT_STST_WERT | unsigned long | Start-Stop-Automatik (nur 4-Zylinder-N43  nicht 6-Zylinder-N53/N54) LV_VAR_STST   Min: 0 Max: 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hs-loeschen"></a>
### HS_LOESCHEN

0x3103 HS_LOESCHEN Historyspeicher loeschen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-innentemp-lesen"></a>
### INNENTEMP_LESEN

0x301001 INNENTEMP_LESEN Steuergeraete-Innentemperatur auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_TSG_WERT | real | ADC-Wert Steuergeraete-Innentemperatur VP_TECU   Einheit: V   Min: 0 Max: 4.999847 |
| STAT_ADC_TSG_EINH | string | V |
| SG_INNENTEMP_WERT | real | Temperatur Steuergeraete-Innentemperatur TECU   Einheit: C   Min: -48 Max: 142.5 |
| SG_INNENTEMP_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-reset-cru-off"></a>
### RESET_CRU_OFF

0x31F4 RESET_CRU_OFF Bedingungen fuer reversible und irreversible Tempomatabschaltung ruecksetzen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-dmtl"></a>
### START_SYSTEMCHECK_DMTL

0x31DA START_SYSTEMCHECK_DMTL Ansteuern Diagnosefunktion DMTL Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-evausbl"></a>
### START_SYSTEMCHECK_EVAUSBL

0x3125 START_SYSTEMCHECK_EVAUSBL Ansteuern Diagnosefunktion Einspritzventilausblendung Aktivierung: Klemme 15 = EIN UND Motorstatus = (Leerlauf ODER Teillast) UND Drehzahl &lt; 3000 1/min Activation: LV_IGK = 1 UND STATE_ENG = (IS ODER PL) UND N &lt; C_N_MAX_KWP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| VENTIL_NR_WERT | unsigned long | Nummer des auszublendenden Einspritzventils INH_IV_KWP   Min: 0 Max: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-gen"></a>
### START_SYSTEMCHECK_GEN

0x312A START_SYSTEMCHECK_GEN Diagnosefunktion Generatortest Aktivierung: Drehzahl &lt;&gt; 0 1/min UND gemessene Spannung in Motorsteuerung &lt; gemessene Spannung am Generator UND Auslastungsgrad Generator &lt; K_DFSCHWGENTEST UND Generatorfehler vorhanden = 0 Activation: N &lt;&gt; 0 UND UB &lt; U_GEN UND DFSIGGEN &lt; K_DFSCHWGENTEST UND GENIUTESTERR = 0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-glf"></a>
### START_SYSTEMCHECK_GLF

0x31D5 START_SYSTEMCHECK_GLF Ansteuern Gesteuerte Luftfuehrung Systemcheck Aktivierung: Testeransteuerung obere Luftklappe = AUS UND Testeransteuerung untere Luftklappe = AUS UND Batteriezustand in Ordnung = JA UND Startverriegelung des Klappentests = AUS Activation: LV_ECRAS_UP_EXT_ADJ = 0 UND LV_ECRAS_DOWN_EXT_ADJ = 0 UND LV_CDN_VB_MIN_DIAG = 1 UND LV_ECRAS_EOL_INH = 0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-igr-aus"></a>
### START_SYSTEMCHECK_IGR_AUS

0x31F7 START_SYSTEMCHECK_IGR_AUS Ansteuern Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-l-regelung-aus"></a>
### START_SYSTEMCHECK_L_REGELUNG_AUS

0x31D9 START_SYSTEMCHECK_L_REGELUNG_AUS Ansteuern Lambdaregelung ausschalten Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-l-sonde"></a>
### START_SYSTEMCHECK_L_SONDE

0x31DF START_SYSTEMCHECK_L_SONDE Ansteuern Diagnosefunktion vertauschte Lambdasonden Aktivierung: Klemme 15 = EIN UND Leerlauf UND Motortemperatur &gt; 77 Grad C UND Abgastemperatur[i] &gt; -48 Grad C UND Lambdasondensignal[i] = EIN UND Bereitschaft Lambdasonde hinter Katalsyator Bank[i] rueckgesetzt = EIN UND Status Lambdasondenheizung vor Katalysator Bank[i] = LSH_POW_CTL UND Status Lambdasondenheizung hinter Katalysator Bank[i] = LSH_POW_CTL UND Startverriegelung Lambdasonden aus Signalplausibilitaetstest Bank[i] = AUS (i = 1 FUER Bank 1, i = 2 FUER Bank 2) Activation: LV_IGK = 1 UND LV_IS = 1 UND TCO &gt; C_TCO_MIN_VLS_EOL UND TEG_CAT_DOWN_MDL[i] &gt; C_TEG_CAT_DOWN_EOL UND LV_LAMB_LS_UP_VLD[i] = 1 UND LV_LS_DOWN_READY[i] = 1 UND STATE_LSH_UP[i] = LSH_POW_CTL UND STATE_LSH_DOWN[i] = LSH_POW_CTL UND LV_DIAG_ACT_INH_LS_UP_DOWN[i] = 0 (i = 1 FUER Bank 1, i = 2 FUER Bank 2)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-llerh"></a>
### START_SYSTEMCHECK_LLERH

0x3126 START_SYSTEMCHECK_LLERH Ansteuern Diagnosefunktion Leerlauf-Erhoehung Aktivierung: Klemme 15 = EIN UND Motorstatus = (Leerlauf ODER Teillast) UND Drehzahl &lt; 3000 1/min UND Ganginfo = 0 UND Geschwindigkeit &lt; 5 km/h UND (Kupplungsschalter = AUS FUER Automatikgetriebe = AUS ODER SMG_Steuergeraet = AUS) UND (Bremsschalter = AUS FUER SMG_Steuergeraet = EIN) Activation: LV_IGK = 1 UND STATE_ENG = (IS ODER PL) UND N &lt; C_N_MAX_KWP UND GEAR_INFO = 0h UND VS &lt;= C_VS_MAX_KWP UND (LV_CS = 0 Fuer LV_AT = 0 UND LV_VAR_AMT = 0) UND (LV_BRAKE_DET = 0 FUER LV_VAR_AMT = 1)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| LL_WERT | unsigned long | LL-Sollwert 0 bis 2000 1/min N_SP_IS_EXT_ADJ   Einheit: rpm   Min: 0 Max: 10000 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-odr"></a>
### START_SYSTEMCHECK_ODR

0x312C START_SYSTEMCHECK_ODR Diagnosefunktion Oeldruckregelung Aktivierung: Leerlauf Activation: LV_IS = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-tev-func"></a>
### START_SYSTEMCHECK_TEV_FUNC

0x3122 START_SYSTEMCHECK_TEV_FUNC Ansteuern Diagnosefunktion Tankentlueftungsventil Aktivierung: Klemme 15 = EIN UND Phase Motorstart beendet = EIN UND Funktionscheck TEV = EIN UND Geschwindigkeit = 0 km/h UND LV_MAF_SP_TQI_DYW_DIAGCPS = 1 UND (Betriebsart TEV = 1 ODER Betriebsart TEV = 2) UND Fehlerspeichereintrag TEV = AUS Activation: LV_IGK = 1 UND LV_ST_END = 1 UND LV_INH_DIAGCPS = 0 UND VS = 0 UND LV_MAF_SP_TQI_DYW_DIAGCPS = 1 UND (OPM_AV_DIAGCPS = 1 ODER OPM_AV_DIAGCPS = 2) UND LV_ERR_DIAGCPS = 0

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-adaption-dk"></a>
### STATUS_ADAPTION_DK

0x224008 STATUS_ADAPTION_DK Drosselklappenadaptionswerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EV_ADD_WERT | long | Adaption Einstritzventil Offset EISYEV_KOROFF_B   Einheit: kg/h   Min: -1024 Max: 1016 |
| STAT_EV_ADD_EINH | string | kgperh |
| STAT_EV_FAC_WERT | real | Adaption Einspritzventil Faktor EISYEV_KORFAK_B   Min: 0 Max: 1.9921 |
| STAT_DK_ADD_WERT | long | Adaption Drosselkappe Offset EISYDK_KOROFF_B   Einheit: kg/h   Min: -1024 Max: 1016 |
| STAT_DK_ADD_EINH | string | kgperh |
| STAT_DK_FAC_WERT | real | Adaption Drosselklappe Faktor EISYDK_KORFAK_B   Min: 0 Max: 1.9921 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-adaption-gemisch"></a>
### STATUS_ADAPTION_GEMISCH

0x22400A STATUS_ADAPTION_GEMISCH Gemischadaptionswerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADD_1_WERT | real | fuel mass set point offset, output from lambda adaptation MFF_ADD_LAM_AD_OUT[1]   Einheit: mg/stk   Min: -694.510597390707 Max: 694.489402609293 |
| STAT_ADD_1_EINH | string | mgperstk |
| STAT_ADD_2_WERT | real | fuel mass set point offset, output from lambda adaptation MFF_ADD_LAM_AD_OUT[2]   Einheit: mg/stk   Min: -694.510597390707 Max: 694.489402609293 |
| STAT_ADD_2_EINH | string | mgperstk |
| STAT_FAC_1_WERT | real | fuel mass set point factor, output from lambda adaptation FAC_LAM_AD_OUT[1]   Einheit: %   Min: -50 Max: 49.9984741210938 |
| STAT_FAC_1_EINH | string | percent |
| STAT_FAC_2_WERT | real | fuel mass set point factor, output from lambda adaptation FAC_LAM_AD_OUT[2]   Einheit: %   Min: -50 Max: 49.9984741210938 |
| STAT_FAC_2_EINH | string | percent |
| STAT_PWM_UP_1_WERT | real | Heater driver PWM duty cycle  acquired also by BSW LSHPWM_UP[1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_PWM_UP_1_EINH | string | percent |
| STAT_PWM_UP_2_WERT | real | Heater driver PWM duty cycle  acquired also by BSW LSHPWM_UP[2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_PWM_UP_2_EINH | string | percent |
| STAT_PWM_DOWN_1_WERT | real | Heater driver PWM duty cycle  acquired also by BSW LSHPWM_DOWN[1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_PWM_DOWN_1_EINH | string | percent |
| STAT_PWM_DOWN_2_WERT | real | Heater driver PWM duty cycle  acquired also by BSW LSHPWM_DOWN[2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_PWM_DOWN_2_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-agk"></a>
### STATUS_AGK

0x30C101 STATUS_AGK Abgasklappe auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_AGK | unsigned long | Status Abgasklappe LV_EF   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-agr"></a>
### STATUS_AGR

0x30BE01 STATUS_AGR AbgasRueckfuehr (AGR) Ventil auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_AGR_WERT | real | Sensorspannung Abgasrueckfuehrventil V_ACR   Einheit: V   Min: 0 Max: 4.995 |
| STAT_ADC_AGR_EINH | string | V |
| STAT_PHY_AGR_WERT | real | Hub Abgasrueckfuehrungsventil OPG_ACR   Einheit: %   Min: 0 Max: 99.9755859375 |
| STAT_PHY_AGR_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

0x300A01 STATUS_AN_LUFTTEMPERATUR Ansauglufttemperatur 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_TANS1_WERT | real | ADC-Wert Ansauglufttemperatur 1 VP_TIA   Einheit: V   Min: 0 Max: 4.999847 |
| STAT_ADC_TANS1_EINH | string | V |
| STAT_AN_LUFTTEMPERATUR_WERT | real | Temperatur Ansauglufttemperatur 1 TIA_MES   Einheit: C   Min: -48 Max: 142.5 |
| STAT_AN_LUFTTEMPERATUR_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-anws"></a>
### STATUS_ANWS

0x30EE01 STATUS_ANWS Vanos Auslass Ventil auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ANWS_WERT | real | Status Vanos_A Ventil IVVTPWM_1   Einheit: %   Min: 0 Max: 99.9984741210938 |
| STAT_STAT_ANWS_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betriebsart"></a>
### STATUS_BETRIEBSART

0x225FF8 STATUS_BETRIEBSART Betriebsarten auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_BA_SOLL_TEXT | string | Sollwert Betriebsart BA_SOLL   Min: 0 Max: 8 |
| STAT_STAT_BA_SOLL_WERT | int |  |
| STAT_STAT_BA_IST_TEXT | string | Istwert Betriebsart BA_IST   Min: 0 Max: 8 |
| STAT_STAT_BA_IST_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-bls"></a>
### STATUS_BLS

0x300201 STATUS_BLS Bremslichtschalter auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_BLS | unsigned long | Status Bremslichtschalter LV_IM_BLS   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-blts"></a>
### STATUS_BLTS

0x300301 STATUS_BLTS Bremslichttestschalter auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_BLTS | unsigned long | Status Bremslichttestschalter LV_IM_BTS   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-budf"></a>
### STATUS_BUDF

0x304001 STATUS_BUDF Bremsunterdrucksensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_BUDF_WERT | real | ADC-Wert Bremsunterdrucksensor V_PBSU   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_ADC_BUDF_EINH | string | V |
| STAT_PHY_BUDF_WERT | real | Bremsunterdrucksensor PBSU   Einheit: hPa   Min: 0 Max: 5434 |
| STAT_PHY_BUDF_EINH | string | hPa |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-bze"></a>
### STATUS_CODIERUNG_BZE

0x223230 STATUS_CODIERUNG_BZE Codierung fuer BZE (Batterie Zustands Erkennung) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CD_HERST1 | unsigned long | Codierung Hersteller 1 (A2L-Name: Qv_cdherst_2) Qv_cdherst_1   Min: 0 Max: 255 |
| STAT_CD_HERST2 | unsigned long | Codierung Hersteller 2 (A2L-Name: Qv_cdherst_2) Qv_cdherst_2   Min: 0 Max: 255 |
| STAT_CD_HERST3 | unsigned long | Codierung Hersteller 3 (A2L-Name: Qv_cdherst_3) Qv_cdherst_3   Min: 0 Max: 255 |
| STAT_CD_HERST4 | unsigned long | Codierung Hersteller 4 (A2L-Name: Qv_cdherst_4) Qv_cdherst_4   Min: 0 Max: 255 |
| STAT_CD_HERST5 | unsigned long | Codierung Hersteller 5 (A2L-Name: Qv_cdherst_5) Qv_cdherst_5   Min: 0 Max: 255 |
| STAT_CD_HERST6 | unsigned long | Codierung Hersteller 6 (A2L-Name: Qv_cdherst_6) Qv_cdherst_6   Min: 0 Max: 255 |
| STAT_CD_HERST7 | unsigned long | Codierung Hersteller 7 (A2L-Name: Qv_cdherst_7) Qv_cdherst_7   Min: 0 Max: 255 |
| STAT_CD_HERST8 | unsigned long | Codierung Hersteller 8 (A2L-Name: Qv_cdherst_8) Qv_cdherst_8   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-igr"></a>
### STATUS_CODIERUNG_IGR

0x223210 STATUS_CODIERUNG_IGR Codierung fuer IGR (Intelligente Generator-Regelung) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_IGR_TEXT | string | Codierung IGR auslesen B_CDIGRONR   Min: 0 Max: 1 |
| STAT_CODIERUNG_IGR_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-kat"></a>
### STATUS_CODIERUNG_KAT

0x223001 STATUS_CODIERUNG_KAT Codierung fuer Katalysator auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_KAT | unsigned long | Status fuer Codierung Katalysator LV_CAT_CONF_DIS_EXT_REQ   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-leistungsstufe"></a>
### STATUS_CODIERUNG_LEISTUNGSSTUFE

0x223020 STATUS_CODIERUNG_LEISTUNGSSTUFE Codierung fuer Leistungsstufe auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LEISTUNGSSTUFE | unsigned long | Codierung fuer Leistungsstufe POW_CONF_IDX_EXT_REQ   Min: 0 Max: 3 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-mil"></a>
### STATUS_CODIERUNG_MIL

0x223000 STATUS_CODIERUNG_MIL Codierung fuer MIL (Malfunction Indication Lamp) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_MIL | unsigned long | Status fuer Codierung MIL STATE_MIL_ON_DIS_EXT_REQ   Min: 0 Max: 2 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-oel"></a>
### STATUS_CODIERUNG_OEL

0x223200 STATUS_CODIERUNG_OEL Codierung fuer Oelwechselintervall auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAENDERFAKTOR_1_WERT | real | Status fuer Codierung Laenderfaktor 1 FAC_OIL_EXT_REQ_1   Min: 0 Max: 2.55 |
| STAT_LAENDERFAKTOR_2_WERT | real | Status fuer Codierung Laenderfaktor 2 FAC_OIL_EXT_REQ_2   Min: 0 Max: 2.55 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-protokoll"></a>
### STATUS_CODIERUNG_PROTOKOLL

0x223030 STATUS_CODIERUNG_PROTOKOLL Codierung Protokoll auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PROTOKOLL | unsigned long | Ausgabe Codierung Protokoll: 0 = Protokoll 15765_4 Anlieferzustand  1 = Protokoll 15765_4 codiert  2 = Protokoll 14230 codiert PROT_CONF_IDX_EXT_REQ   Min: 0 Max: 2 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-spa"></a>
### STATUS_CODIERUNG_SPA

0x223220 STATUS_CODIERUNG_SPA Codierung fuer SPA (Schaltpunktanzeige) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_B_SPA_CSOLL_TEXT | string | Codierung Schaltpunktanzeige (SPA), 0 = Auslieferungszustand, 1 = Abweichung zum Auslieferungszustand B_SPA_CSOLL   Min: 0 Max: 1 |
| STAT_B_SPA_CSOLL_WERT | int |  |
| STAT_B_SPA_CIST_TEXT | string | ZurÃ¼ckgemeltdete Codierung SPA, 0 = Schaltpunktanzeige inaktiv, 1 = Schaltpunktanzeige aktiv B_SPA_CIST   Min: 0 Max: 1 |
| STAT_B_SPA_CIST_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-vmax"></a>
### STATUS_CODIERUNG_VMAX

0x223010 STATUS_CODIERUNG_VMAX Codierung fuer maximale Geschwindigkeit auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_VMAX | unsigned long | Status fuer Codierung maximale Geschwindigkeit VS_MAX_SEL_EXT_REQ   Min: 0 Max: 3 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-codierung-xenon"></a>
### STATUS_CODIERUNG_XENON

0x223211 STATUS_CODIERUNG_XENON Codierung fuer Xenon-Lichtverbau auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_XENON_TEXT | string | Codierung Xenonverbau auslesen B_CDXENONR |
| STAT_CODIERUNG_XENON_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-desulfatisierung"></a>
### STATUS_DESULFATISIERUNG

0x332D STATUS_DESULFATISIERUNG Auslesen Desulfatisierung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1_TEXT | string | Status Desulfatisierung STATE_KWP_SO2P   Min: 0 Max: 9 |
| STAT_DIAGNOSE_1_WERT | int |  |
| STAT_DIAGNOSE_2_TEXT | string | Erweiterter Status Desulfatisierung STATE_NT_SO2P_EXT_ADJ_ACT   Min: 0 Max: 3 |
| STAT_DIAGNOSE_2_WERT | int |  |
| STAT_TNT_MDL_L_WERT | real | Istwert Temperaturregelung TNT_MDL_L   Einheit: C   Min: 0 Max: 1023.984375 |
| STAT_TNT_MDL_L_EINH | string | degreeC |
| STAT_TNT_MDL_MV_WERT | real | Temperatur Desulfatisierungsschwelle TNT_MDL_MV   Einheit: C   Min: 0 Max: 1023.984375 |
| STAT_TNT_MDL_MV_EINH | string | degreeC |
| STAT_T_NT_SO2P_EXT_ADJ_ACT_WERT | real | Zeitgeber Desulfatisierung T_NT_SO2P_EXT_ADJ_ACT   Einheit: s   Min: 0 Max: 6553.5 |
| STAT_T_NT_SO2P_EXT_ADJ_ACT_EINH | string | s |
| STAT_NT_SUL_WERT | real | Schwefelbeladung NT_SUL   Einheit: mg   Min: 0 Max: 10485.6 |
| STAT_NT_SUL_EINH | string | mg |
| STAT_LAMB_SP_WERT | real | Lambdasetpoint Mittelwert LAMB_SP   Min: 0 Max: 31.9990234375 |
| STAT_LAMB_SP_1_WERT | real | Lambdasetpoint Bank 1 LAMB_SP[1]   Min: -32768 Max: 32767 |
| STAT_LAMB_SP_2_WERT | real | Lambdasetpoint Bank 2 LAMB_SP[2]   Min: -32768 Max: 32767 |
| STAT_N_32_WERT | unsigned long | Drehzahl Aufloesung 32 rpm N_32   Einheit: rpm   Min: 0 Max: 8160 |
| STAT_N_32_EINH | string | rpm |
| STAT_VS_WERT | unsigned long | Geschwindigkeit VS   Einheit: km/h   Min: 0 Max: 255 |
| STAT_VS_EINH | string | kmperh |
| STAT_PV_WERT | real | Pedalwert PV   Einheit: %   Min: 0 Max: 99.90234375 |
| STAT_PV_EINH | string | percent |
| STAT_GEAR | unsigned long | Gangstellung GEAR   Min: 0 Max: 255 |
| STAT_LV_CLU_SWI | unsigned long | Kupplungspedal betaetigt LV_CLU_SWI   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dfmonitor"></a>
### STATUS_DFMONITOR

0x224001 STATUS_DFMONITOR Batterieladezustand auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AUSGANG_WERT | real | Batterieladezustand DFMONITOR   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_AUSGANG_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-0"></a>
### STATUS_DIGITAL_0

0x224007 STATUS_DIGITAL_0 Status Schaltzustaende 0 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LS1_REGELUNG_TEXT | string | Status Regelkreis Bank 1 LV_LAM_LSCL[1] |
| STAT_LS1_REGELUNG_WERT | int |  |
| STAT_LS2_REGELUNG_TEXT | string | Status Regelkreis Bank 2 LV_LAM_LSCL[2] |
| STAT_LS2_REGELUNG_WERT | int |  |
| STAT_LSVK1_TEXT | string | Status Lambdaregelung vor Katalysator Bank 1 LV_LS_UP_READY[1] |
| STAT_LSVK1_WERT | int |  |
| STAT_LSVK2_TEXT | string | Status Lambdaregelung vor Katalysator Bank 2 LV_LS_UP_READY[2] |
| STAT_LSVK2_WERT | int |  |
| STAT_LSHK2_TEXT | string | Status Lambdaregelung hinter Katalysator Bank 2 LV_LS_DOWN_READY[2] |
| STAT_LSHK2_WERT | int |  |
| STAT_LSHK1_TEXT | string | Status Lambdaregelung hinter Katalysator Bank 1 LV_LS_DOWN_READY[1] |
| STAT_LSHK1_WERT | int |  |
| STAT_VL_TEXT | string | Status Vollast LV_FL |
| STAT_VL_WERT | int |  |
| STAT_LL_TEXT | string | Status Leerlauf LV_IS |
| STAT_LL_WERT | int |  |
| STAT_DK_ABGLEICH_TEXT | string | Status Drosselklappen-Neuabgleich LV_TPS_AD_REQ |
| STAT_DK_ABGLEICH_WERT | int |  |
| STAT_SCHUBAB_TEXT | string | Status Schubabschaltung LV_PUC |
| STAT_SCHUBAB_WERT | int |  |
| STAT_FAHRSTUFE_TEXT | string | Status Fahrstufe LV_DRI |
| STAT_FAHRSTUFE_WERT | int |  |
| STAT_KICKDOWN_TEXT | string | Status Kickdownerkennung LV_KD |
| STAT_KICKDOWN_WERT | int |  |
| STAT_FEHLER_BREMSE_TEXT | string | Fehlerstatus Bremse STATE_CRU_OFF_IRR[5] |
| STAT_FEHLER_BREMSE_WERT | int |  |
| STAT_TIMEOUT_EGS1_TEXT | string | Timeoutstatus EGS STATE_CRU_OFF_IRR[4] |
| STAT_TIMEOUT_EGS1_WERT | int |  |
| STAT_FEHLER_MFL_TEXT | string | Fehlerstatus Multifunktionslenkrad STATE_CRU_OFF_IRR[3] |
| STAT_FEHLER_MFL_WERT | int |  |
| STAT_FEHLER_CLSW_TEXT | string | Fehlerstatus Kupplungsschalter STATE_CRU_OFF_IRR[2] |
| STAT_FEHLER_CLSW_WERT | int |  |
| STAT_DYN_LIM_2_TEXT | string | Notlaufstatus Limit Dynamik 2 STATE_CRU_OFF_IRR[1] |
| STAT_DYN_LIM_2_WERT | int |  |
| STAT_DYN_LIM_1_TEXT | string | Notlaufstatus Limit Dynamik 1 STATE_CRU_OFF_IRR[0] |
| STAT_DYN_LIM_1_WERT | int |  |
| STAT_EGAS_NOTLAUF_TEXT | string | Status EGAS-Notlauf STATE_CRU_OFF_IRR[14] |
| STAT_EGAS_NOTLAUF_WERT | int |  |
| STAT_ASR_TIMEOUT_TEXT | string | Kommunikationsstatus ASR-Steuergeraet STATE_CRU_OFF_IRR[13] |
| STAT_ASR_TIMEOUT_WERT | int |  |
| STAT_FEHLER_VS_TEXT | string | Fehlerstatus Geschwindigkeit STATE_CRU_OFF_IRR[12] |
| STAT_FEHLER_VS_WERT | int |  |
| STAT_NOTLAUF_DK_TEXT | string | Notlaufstatus DK-Steller STATE_CRU_OFF_IRR[11] |
| STAT_NOTLAUF_DK_WERT | int |  |
| STAT_NOTLAUF_LL_TEXT | string | Notlaufstatus LL-Steller STATE_CRU_OFF_IRR[10] |
| STAT_NOTLAUF_LL_WERT | int |  |
| STAT_V_PLAUSIBEL_TEXT | string | Plausibilitaet Geschwindigkeit STATE_CRU_OFF_IRR[9] |
| STAT_V_PLAUSIBEL_WERT | int |  |
| STAT_MON_LEVEL2_TEXT | string | Status Monitoring Ebene 2 STATE_CRU_OFF_IRR[8] |
| STAT_MON_LEVEL2_WERT | int |  |
| STAT_MFL_AUS_TEXT | string | Status Multifunktionslenkrad STATE_CRU_OFF_REV[4] |
| STAT_MFL_AUS_WERT | int |  |
| STAT_EXT_MOMENT_TEXT | string | Status externer Drehmomenteneingriff STATE_CRU_OFF_REV[3] |
| STAT_EXT_MOMENT_WERT | int |  |
| STAT_VS_SP_MAX_TEXT | string | Sollwertstatus fuer maximale Geschwindigkeit STATE_CRU_OFF_REV[2] |
| STAT_VS_SP_MAX_WERT | int |  |
| STAT_UEBERN_LANG_TEXT | string | Status Geschwindigkeitsuebernahme STATE_CRU_OFF_REV[1] |
| STAT_UEBERN_LANG_WERT | int |  |
| STAT_VS_DIF_HOCH_TEXT | string | Status Geschwindigkeitsdifferenz STATE_CRU_OFF_REV[0] |
| STAT_VS_DIF_HOCH_WERT | int |  |
| STAT_MFL_HARD_OFF_TEXT | string | Notausstatus Multifunktionslenkrad STATE_CRU_OFF_REV[15] |
| STAT_MFL_HARD_OFF_WERT | int |  |
| STAT_BREMSE_AKTIV_TEXT | string | Feststellstatus Bremsen STATE_CRU_OFF_REV[14] |
| STAT_BREMSE_AKTIV_WERT | int |  |
| STAT_DREHZAHL_BEG_TEXT | string | Status Drehzahlbegrenzung STATE_CRU_OFF_REV[13] |
| STAT_DREHZAHL_BEG_WERT | int |  |
| STAT_VS_FIL_LOW_TEXT | string | Status Geschwindigkeit STATE_CRU_OFF_REV[12] |
| STAT_VS_FIL_LOW_WERT | int |  |
| STAT_TAKEOVER_VS_TEXT | string | Uebernahmestatus und Maximalgeschwindigkeit STATE_CRU_OFF_REV[11] |
| STAT_TAKEOVER_VS_WERT | int |  |
| STAT_HOCHDREH_S_TEXT | string | Status Hochdrehsicherung STATE_CRU_OFF_REV[10] |
| STAT_HOCHDREH_S_WERT | int |  |
| STAT_BESCHL_MON_TEXT | string | Status Beschleunigungsueberwachung STATE_CRU_OFF_REV[9] |
| STAT_BESCHL_MON_WERT | int |  |
| STAT_VS_CAN_LANG_TEXT | string | Status CAN-Botschaft Geschwindigkeit STATE_CRU_OFF_REV[8] |
| STAT_VS_CAN_LANG_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-digital-1"></a>
### STATUS_DIGITAL_1

0x224002 STATUS_DIGITAL_1 Status Schaltzustaende Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AC_EIN_TEXT | string | Status Klimabereitschaft LV_ACCOUT_RLY |
| STAT_AC_EIN_WERT | int |  |
| STAT_BTS_EIN_TEXT | string | Status Bremslichtschalter-Kanal 2 LV_IM_BTS |
| STAT_BTS_EIN_WERT | int |  |
| STAT_BLS_EIN_TEXT | string | Status Bremslichtschalter-Kanal 1 LV_IM_BLS |
| STAT_BLS_EIN_WERT | int |  |
| STAT_KUPPL_EIN_TEXT | string | Status Kupplungsschalter LV_CS |
| STAT_KUPPL_EIN_WERT | int |  |
| STAT_MOTOR_AUS_TEXT | string | Status Motorzustand LV_ES |
| STAT_MOTOR_AUS_WERT | int |  |
| STAT_KL15_EIN_TEXT | string | Status Klemme-15 LV_IGK |
| STAT_KL15_EIN_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-disa"></a>
### STATUS_DISA

0x30C601 STATUS_DISA Variable Sauganlage (DISA) Klappe auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_DISA_WERT | real | Status Variable Sauganlage (DISA) Klappe VIMPWM_1   Einheit: %   Min: -100 Max: 99.9969482421875 |
| STAT_STAT_DISA_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-disa2"></a>
### STATUS_DISA2

0x30AE01 STATUS_DISA2 Variable Sauganlage (DISA) Klappe2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_DISA2_WERT | real | Status Variable Sauganlage (DISA) Klappe2 VIMPWM_2   Einheit: %   Min: -100 Max: 99.9969482421875 |
| STAT_STAT_DISA2_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dkh"></a>
### STATUS_DKH

0x309E01 STATUS_DKH Drosselklappenbeheizung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_DKH_RLY | unsigned long | Status Drosselklappenheizungsrelais LV_RLY_MTC_HEAT   Min: 0 Max: 1 |
| STAT_STAT_DKH_TEXT | string | Status Drosselklappenheizung STATE_MTC_HEAT   Min: 0 Max: 7 |
| STAT_STAT_DKH_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dkp-volt"></a>
### STATUS_DKP_VOLT

0x302A01 STATUS_DKP_VOLT Drosselklappe auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DKP_VOLT_WERT | real | ADC-Wert1 Drosselklappe V_TPS_1   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_DKP_VOLT_EINH | string | V |
| STAT_ADC2_DK_WERT | real | ADC-Wert2 Drosselklappe V_TPS_2   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_ADC2_DK_EINH | string | V |
| STAT_STAT_DK_WERT | real | Status Drosselklappe TPS_AV   Einheit: TPS   Min: 0 Max: 119.5 |
| STAT_STAT_DK_EINH | string | degreeTPS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dmtl-heizung"></a>
### STATUS_DMTL_HEIZUNG

0x30CE01 STATUS_DMTL_HEIZUNG Diagnosemodul-Tank Leckage Heizung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_DMTLH | unsigned long | Status Diagnosemodul-Tank Leckage Heizung LV_HDMTL_ON   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dmtl-p"></a>
### STATUS_DMTL_P

0x30CC01 STATUS_DMTL_P Diagnosemodul-Tank Leckage Pumpe auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_DMTL_P | unsigned long | Status Diagnosemodul-Tank Leckage Pumpe LV_DMTL_PUMP   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-dmtl-v"></a>
### STATUS_DMTL_V

0x30CD01 STATUS_DMTL_V Diagnosemodul-Tank Leckage Ventil auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_DMTL_V | unsigned long | Status Diagnosemodul-Tank Leckage Ventil LV_DMTLS   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-e-luefter"></a>
### STATUS_E_LUEFTER

0x30DA01 STATUS_E_LUEFTER E-Luefter auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ELUE_WERT | real | Status E-Luefter ECFPWM[0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_STAT_ELUE_EINH | string | percent |
| STAT_PHY_TCO_WERT | real | Kuehlmitteltemperatur (Dieser Wert wurde zusaetzlich zum geforderten Umfang eingefuegt) TCO   Einheit: C   Min: -48 Max: 142.5 |
| STAT_PHY_TCO_EINH | string | degreeC |
| STAT_PHY_TCO_2_WERT | real | Kuehlmitteltemperatur am Kuehlerausgang (Dieser Wert wurde zusaetzlich zum geforderten Umfang eingefuegt) TCO_2   Einheit: C   Min: -48 Max: 142.5 |
| STAT_PHY_TCO_2_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ebl"></a>
### STATUS_EBL

0x30C801 STATUS_EBL E-Box-Luefter auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_EBL | unsigned long | Status E-Box-Luefter LV_EBOX_CFA   Min: 0 Max: 1 |
| STAT_PHY_TECU_WERT | real | Steuergeraetetemperatur DME (Dieser Wert wurde zusaetzlich zum geforderten Umfang eingefuegt) TECU   Einheit: C   Min: -48 Max: 142.5 |
| STAT_PHY_TECU_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eisydr"></a>
### STATUS_EISYDR

0x33E2 STATUS_EISYDR Auslesen Eisy-Adaptionswerte mit Druckregelung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_EISYGD_TEXT | string | Funktionsstatus Eisy-Adaptionswerte mit Druckregelung B_MAREGDK_AD   Min: 0 Max: 1 |
| STAT_FS_EISYGD_WERT | int |  |
| STAT_MRNN_TEST_PR_WERT | real | Massenstromregler-Adaptionswert NN im AGR - Betrieb ueber Test gelesen MRNN_TEST_PR   Min: -2 Max: 1.9999 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eisygd"></a>
### STATUS_EISYGD

0x33E1 STATUS_EISYGD Auslesen Eisy-Adaptionswerte (gedrosselt) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_EISYGD_TEXT | string | Adaption Massenstromregler auf DK erstmalig erfolgt B_MAREGDK_AD   Min: 0 Max: 1 |
| STAT_FS_EISYGD_WERT | int |  |
| STAT_MRNN_TEST_DK_WERT | real | Massenstromregler-Adaptionswert NN im GD - Betrieb ueber Test gelesen MRNN_TEST_DK   Min: -1 Max: 0.9999 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ekp"></a>
### STATUS_EKP

0x30D801 STATUS_EKP Elektrische Kraftstoffpumpe 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_EKP1_WERT | real | Status Elektrische Kraftstoffpumpe 1 EFPPWM   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_STAT_EKP1_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-eml"></a>
### STATUS_EML

0x30D601 STATUS_EML EML (Engine Malfunction Lamp) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_EML | unsigned long | Status EML (Engine Malfunction Lamp) LV_WAL_1_CAN   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-energiesparmode"></a>
### STATUS_ENERGIESPARMODE

0x22100A STATUS_ENERGIESPARMODE Status Energiesparmode Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENERGIESPARMODE_TEXT | string | Status Energiesparmode  00 = Passiv, 01 = Fertigung, 02 = Transport, 03 = Werkstatt STATE_EGY_MIN_KWP   Min: 0 Max: 3 |
| STAT_ENERGIESPARMODE_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-enws"></a>
### STATUS_ENWS

0x30ED01 STATUS_ENWS Vanos Einlass Ventil auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ENWS_WERT | real | Status Vanos_E Ventil IVVTPWM_0   Einheit: %   Min: 0 Max: 99.9984741210938 |
| STAT_STAT_ENWS_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ev1"></a>
### STATUS_EV1

0x30E101 STATUS_EV1 Einspritzventil 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_EV1_WERT | real | Spannung Injektor 1 V_IV_1_MES[0]   Einheit: V   Min: 0 Max: 639.98046875 |
| STAT_ADC_EV1_EINH | string | V |
| STAT_CHA_EV1_WERT | unsigned long | Elektrische Ladung Injektor 1 CHA_IV_1_MES[0]   Einheit: uAs   Min: 0 Max: 2272.6968 |
| STAT_CHA_EV1_EINH | string | uAs |
| STAT_PHY_EV1_WERT | real | Einspritzzeit Zylinder 1 von der Endstufe rueckgemessen TI_1_MES[0]   Einheit: ms   Min: 0 Max: 65.535 |
| STAT_PHY_EV1_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ev2"></a>
### STATUS_EV2

0x30E201 STATUS_EV2 Einspritzventil 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_EV2_WERT | real | Spannung Injektor 2 V_IV_1_MES[4]   Einheit: V   Min: 0 Max: 639.98046875 |
| STAT_ADC_EV2_EINH | string | V |
| STAT_CHA_EV2_WERT | unsigned long | Elektrische Ladung Injektor 2 CHA_IV_1_MES[4]   Einheit: uAs   Min: 0 Max: 2272.6968 |
| STAT_CHA_EV2_EINH | string | uAs |
| STAT_PHY_EV2_WERT | real | Einspritzzeit Zylinder 2 von der Endstufe rueckgemessen TI_1_MES[4]   Einheit: ms   Min: 0 Max: 65.535 |
| STAT_PHY_EV2_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ev3"></a>
### STATUS_EV3

0x30E301 STATUS_EV3 Einspritzventil 3 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_EV3_WERT | real | Spannung Injektor 3 V_IV_1_MES[2]   Einheit: V   Min: 0 Max: 639.98046875 |
| STAT_ADC_EV3_EINH | string | V |
| STAT_CHA_EV3_WERT | unsigned long | Elektrische Ladung Injektor 3 CHA_IV_1_MES[2]   Einheit: uAs   Min: 0 Max: 2272.6968 |
| STAT_CHA_EV3_EINH | string | uAs |
| STAT_PHY_EV3_WERT | real | Einspritzzeit Zylinder 3 von der Endstufe rueckgemessen TI_1_MES[2]   Einheit: ms   Min: 0 Max: 65.535 |
| STAT_PHY_EV3_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ev4"></a>
### STATUS_EV4

0x30E401 STATUS_EV4 Einspritzventil 4 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_EV4_WERT | real | Spannung Injektor 4 V_IV_1_MES[5]   Einheit: V   Min: 0 Max: 639.98046875 |
| STAT_ADC_EV4_EINH | string | V |
| STAT_CHA_EV4_WERT | unsigned long | Elektrische Ladung Injektor 4 CHA_IV_1_MES[5]   Einheit: uAs   Min: 0 Max: 2272.6968 |
| STAT_CHA_EV4_EINH | string | uAs |
| STAT_PHY_EV4_WERT | real | Einspritzzeit Zylinder 4 von der Endstufe rueckgemessen TI_1_MES[5]   Einheit: ms   Min: 0 Max: 65.535 |
| STAT_PHY_EV4_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ev5"></a>
### STATUS_EV5

0x30E501 STATUS_EV5 Einspritzventil 5 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_EV5_WERT | real | Spannung Injektor 5 V_IV_1_MES[1]   Einheit: V   Min: 0 Max: 639.98046875 |
| STAT_ADC_EV5_EINH | string | V |
| STAT_CHA_EV5_WERT | unsigned long | Elektrische Ladung Injektor 5 CHA_IV_1_MES[1]   Einheit: uAs   Min: 0 Max: 2272.6968 |
| STAT_CHA_EV5_EINH | string | uAs |
| STAT_PHY_EV5_WERT | real | Einspritzzeit Zylinder 5 von der Endstufe rueckgemessen TI_1_MES[1]   Einheit: ms   Min: 0 Max: 65.535 |
| STAT_PHY_EV5_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ev6"></a>
### STATUS_EV6

0x30E601 STATUS_EV6 Einspritzventil 6 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_EV6_WERT | real | Spannung Injektor 6 V_IV_1_MES[3]   Einheit: V   Min: 0 Max: 639.98046875 |
| STAT_ADC_EV6_EINH | string | V |
| STAT_CHA_EV6_WERT | unsigned long | Elektrische Ladung Injektor 6 CHA_IV_1_MES[3]   Einheit: uAs   Min: 0 Max: 2272.6968 |
| STAT_CHA_EV6_EINH | string | uAs |
| STAT_PHY_EV6_WERT | real | Einspritzzeit Zylinder 6 von der Endstufe rueckgemessen TI_1_MES[3]   Einheit: ms   Min: 0 Max: 65.535 |
| STAT_PHY_EV6_EINH | string | ms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ewap"></a>
### STATUS_EWAP

0x30BF01 STATUS_EWAP elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_EWAP | unsigned long | Status elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) N_REL_CWP   Min: 0 Max: 255 |
| STAT_PHY_TCO_WERT | real | Kuehlmitteltemperatur (Dieser Wert wurde zusaetzlich zum geforderten Umfang eingefuegt) TCO   Einheit: C   Min: -48 Max: 142.5 |
| STAT_PHY_TCO_EINH | string | degreeC |
| STAT_PHY_TCO_2_WERT | real | Coolant temperature (radiator outlet) (A2L-Name: tco_2) TCO_2   Einheit: C   Min: -48 Max: 142.5 |
| STAT_PHY_TCO_2_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fwv1"></a>
### STATUS_FWV1

0x301E01 STATUS_FWV1 Fahrerwunschversorgung 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_FWV1_WERT | real | ADC-Wert Fahrerwunschversorgung 1 VCC_PVS_1   Einheit: V   Min: 0 Max: 9.9902 |
| STAT_ADC_FWV1_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fwv2"></a>
### STATUS_FWV2

0x301F01 STATUS_FWV2 Fahrerwunschversorgung 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_FWV2_WERT | real | ADC-Wert Fahrerwunschversorgung 2 VCC_PVS_2   Einheit: V   Min: 0 Max: 9.9902 |
| STAT_ADC_FWV2_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-glf"></a>
### STATUS_GLF

0x30C301 STATUS_GLF Gesteuerte Luftfuehrung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_GLF_TEXT | string | PWM-Signal fuer gesteuerte Luftfuehrung ECRASPWM |
| STAT_STAT_GLF_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-glf2"></a>
### STATUS_GLF2

0x30A401 STATUS_GLF2 Gesteuerte Luftfuehrung Klappe 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_GLF2_TEXT | string | PWM-Signale fuer gesteuerte Luftfuehrung ECRASPWM |
| STAT_STAT_GLF2_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-imaalle"></a>
### STATUS_IMAALLE

0x225F90 STATUS_IMAALLE Abgleichwerte Injektoren auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENERGIEABGLEICH_ZYL_1_WERT | real | IMA Abgleichwert Injektor 01 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[0]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_1_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_1_WERT | real | IMA Abgleichwert Injektor 01 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[0]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_1_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_5_WERT | real | IMA Abgleichwert Injektor 02 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[1]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_5_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_5_WERT | real | IMA Abgleichwert Injektor 02 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[1]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_5_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_3_WERT | real | IMA Abgleichwert Injektor 03 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[2]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_3_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_3_WERT | real | IMA Abgleichwert Injektor 03 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[2]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_3_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_6_WERT | real | IMA Abgleichwert Injektor 04 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[3]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_6_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_6_WERT | real | IMA Abgleichwert Injektor 04 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[3]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_6_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_2_WERT | real | IMA Abgleichwert Injektor 05 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[4]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_2_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_2_WERT | real | IMA Abgleichwert Injektor 05 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[4]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_2_EINH | string | mgperstk |
| STAT_ENERGIEABGLEICH_ZYL_4_WERT | real | IMA Abgleichwert Injektor 06 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[5]   Einheit: mJ   Min: 0 Max: 255 |
| STAT_ENERGIEABGLEICH_ZYL_4_EINH | string | mJ |
| STAT_DURCHFLUSSABGLEICH_ZYL_4_WERT | real | IMA Abgleichwert Injektor 06 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[5]   Einheit: mg/stk   Min: 0 Max: 1389 |
| STAT_DURCHFLUSSABGLEICH_ZYL_4_EINH | string | mgperstk |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kb1"></a>
### STATUS_KB1

0x303001 STATUS_KB1 Klopfbaustein 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_KB1_WERT | real | ADC-Wert Klopfbaustein 1 KNKS[0]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_ADC_KB1_EINH | string | V |
| STAT_STAT_KB1_WERT | real | Status Klopfbaustein 1 KNKS_REL_NL_0   Min: 0 Max: 0.9999847 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kb2"></a>
### STATUS_KB2

0x303101 STATUS_KB2 Klopfbaustein 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_KB2_WERT | real | ADC-Wert Klopfbaustein 2 KNKS[5]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_ADC_KB2_EINH | string | V |
| STAT_STAT_KB2_WERT | real | Status Klopfbaustein 2 KNKS_REL_NL_5   Min: 0 Max: 0.9999847 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kdf"></a>
### STATUS_KDF

0x301A01 STATUS_KDF Kraftstoffdruck im Einspritzsystem auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_KDF_WERT | real | Kraftstoffdruck im Einspritzsystem (Raildruck) FUP   Einheit: hPa   Min: 0 Max: 347776 |
| STAT_PHY_KDF_EINH | string | hPa |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kdfn"></a>
### STATUS_KDFN

0x303F01 STATUS_KDFN Kraftstoffdruck im Niederdruckbereich auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_KDFN_WERT | real | Kraftstoffdruck im Niederdruckbereich FUP_EFP   Einheit: hPa   Min: 0 Max: 173888 |
| STAT_PHY_KDFN_EINH | string | hPa |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kft"></a>
### STATUS_KFT

0x30C901 STATUS_KFT Kennfeldthermostat auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_KFT_WERT | real | Status Kennfeldthermostat ECTPWM   Einheit: %   Min: 0 Max: 99.9984741210938 |
| STAT_STAT_KFT_EINH | string | percent |
| STAT_PHY_TCO_WERT | real | Kuehlmitteltemperatur (Dieser Wert wurde zusaetzlich zum geforderten Umfang eingefuegt) TCO   Einheit: C   Min: -48 Max: 142.5 |
| STAT_PHY_TCO_EINH | string | degreeC |
| STAT_PHY_TCO_2_WERT | real | Kuehlmitteltemperatur am Kuehlerausgang (Dieser Wert wurde zusaetzlich zum geforderten Umfang eingefuegt) TCO_2   Einheit: C   Min: -48 Max: 142.5 |
| STAT_PHY_TCO_2_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kgeh"></a>
### STATUS_KGEH

0x30AD01 STATUS_KGEH Kurbelgehaeuseentlueftungsheizung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_KGEH | unsigned long | Status Kurbelgehaeuseentlueftungsheizung LV_RLY_CRCV_HEAT   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-klann"></a>
### STATUS_KLANN

0x33E4 STATUS_KLANN Auslesen Klann-Adaptionswerte (Anforderung aus CP10798) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KLANN_TEST1_WERT | real | Faktor aus Lambdaregelungsadaption fÃ¼r Bank 1, Testerabfrage (A2L-Name: Klann_test1) KLANN_TEST1   Min: -50 Max: 49.9984 |
| STAT_KLANN_TEST2_WERT | real | Faktor aus Lambdaregelungsadaption fÃ¼r Bank 2, Testerabfrage (A2L-Name: Klann_test2) KLANN_TEST2   Min: -50 Max: 49.9984 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-korel"></a>
### STATUS_KOREL

0x30C701 STATUS_KOREL Klimakompressor-Relais auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_KOREL | unsigned long | Status Klimakompressor-Relais LV_ACCOUT_RLY   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-krann"></a>
### STATUS_KRANN

0x33E3 STATUS_KRANN Auslesen Krann-Adaptionswerte Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_KRNN_TEST_WERT | real | Zuendwinkelaenderung aus Adaption Klopfregelung fuer Testerabfrage KRNN_TEST   Einheit: Grad   Min: -50 Max: 60 |
| STAT_KRNN_TEST_EINH | string | degree |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kup"></a>
### STATUS_KUP

0x300401 STATUS_KUP Kupplungsschalter auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_KUP | unsigned long | Status Kupplungsschalter LV_CS   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde"></a>
### STATUS_L_SONDE

0x302101 STATUS_L_SONDE Lambdasonde vor Kat Bank1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_SONDE_WERT | real | ADC-Wert Lambdasonde vor Kat Bank1 VLS_UP[1]   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_L_SONDE_EINH | string | V |
| STAT_PHY_LSVK1_WERT | real | Lambdawert Lambdasonde vor Kat Bank1 LAMB_LS_UP[1]   Min: 0 Max: 31.9990234375 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde-2"></a>
### STATUS_L_SONDE_2

0x302301 STATUS_L_SONDE_2 Lambdasonde vor Kat Bank2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_SONDE_2_WERT | real | ADC-Wert Lambdasonde vor Kat Bank2 VLS_UP[2]   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_L_SONDE_2_EINH | string | V |
| STAT_PHY_LSVK2_WERT | real | Lambdawert Lambdasonde vor Kat Bank2 LAMB_LS_UP[2]   Min: 0 Max: 31.9990234375 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde-2-h"></a>
### STATUS_L_SONDE_2_H

0x302401 STATUS_L_SONDE_2_H Lambdasonde hinter Kat Bank2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_SONDE_2_H_WERT | real | ADC-Wert Lambdasonde hinter Kat Bank2 VLS_DOWN[2]   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_L_SONDE_2_H_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-l-sonde-h"></a>
### STATUS_L_SONDE_H

0x302201 STATUS_L_SONDE_H Lambdasonde hinter Kat Bank1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_SONDE_H_WERT | real | ADC-Wert Lambdasonde hinter Kat Bank1 VLS_DOWN[1]   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_L_SONDE_H_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lds1"></a>
### STATUS_LDS1

0x30B601 STATUS_LDS1 Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_LDS1_WERT | real | Status Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) WGPWM_0   Einheit: %   Min: 0 Max: 99.9984741210938 |
| STAT_STAT_LDS1_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lds2"></a>
### STATUS_LDS2

0x30B701 STATUS_LDS2 Ladedrucksteller 2 (z.B. Waste Gate oder VTG variable Turbinengeometrie) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_LDS2_WERT | real | Status Ladedrucksteller 2 (z.B. Waste Gate oder VTG variable Turbinengeometrie) WGPWM_1   Einheit: %   Min: 0 Max: 99.9984741210938 |
| STAT_STAT_LDS2_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lgs"></a>
### STATUS_LGS

0x300701 STATUS_LGS Leergassenschalter auslesen (nur MSD80 mit N43) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_LGS_WERT | real | Status Leergassenschalter PWM_NEUT_PSN_GB   Einheit: %   Min: 0 Max: 99.9984741210938 |
| STAT_STAT_LGS_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ll-abgleich"></a>
### STATUS_LL_ABGLEICH

0x225FF0 STATUS_LL_ABGLEICH Abgleichwert LL (Leerlauf) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFS_ACC_DRI_WERT | long | Abgleichswert LL mit Klima und Fahrbedingung N_KWP_OFS_ACC_DRI   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_ACC_DRI_EINH | string | rpm |
| STAT_OFS_DRI_WERT | long | Abgleichswert LL mit Fahrstufe N_KWP_OFS_DRI   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_DRI_EINH | string | rpm |
| STAT_OFS_WERT | long | Abgleichswert LL N_KWP_OFS   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_EINH | string | rpm |
| STAT_OFS_ACC_WERT | long | Abgleichswert LL mit Klimaanlage N_KWP_OFS_ACC   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_ACC_EINH | string | rpm |
| STAT_OFS_VB_WERT | long | Abgleichswert LL mit niedriger Batteriespannung N_KWP_OFS_VB   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_VB_EINH | string | rpm |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

0x302501 STATUS_LMM_MASSE Luftmassenmesser 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PD_LMM1_WERT | unsigned long | Periodendauer Luftmassenmesser 1 T_PER_MAF_FRQ[0]   Einheit: s   Min: 0 Max: 65535 |
| STAT_PD_LMM1_EINH | string | micros |
| STAT_LMM_MASSE_WERT | real | Durchsatz Luftmassenmesser 1 MAF_KGH_MES_BAS   Einheit: kg/h   Min: 0 Max: 2047.96875 |
| STAT_LMM_MASSE_EINH | string | kgperh |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lsh1"></a>
### STATUS_LSH1

0x30D001 STATUS_LSH1 Lambdasondenheizung vor Kat Bank1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_LSH1_WERT | real | Status Lambdasondenheizung vor Kat Bank1 LSHPWM_UP[1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_STAT_LSH1_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lsh2"></a>
### STATUS_LSH2

0x30D101 STATUS_LSH2 Lambdasondenheizung hinter Kat Bank1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_LSH2_WERT | real | Status Lambdasondenheizung hinter Kat Bank1 LSHPWM_DOWN[1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_STAT_LSH2_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lsh3"></a>
### STATUS_LSH3

0x30D201 STATUS_LSH3 Lambdasondenheizung vor Kat Bank2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_LSH3_WERT | real | Status Lambdasondenheizung vor Kat Bank2 LSHPWM_UP[2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_STAT_LSH3_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-lsh4"></a>
### STATUS_LSH4

0x30D301 STATUS_LSH4 Lambdasondenheizung hinter Kat Bank2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_LSH4_WERT | real | Status Lambdasondenheizung hinter Kat Bank2 LSHPWM_DOWN[2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_STAT_LSH4_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte"></a>
### STATUS_MESSWERTE

0x224000 STATUS_MESSWERTE Messwerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EV1_MW_WERT | real | Einspritzzeit EV 1 TI_1_HOM[0]   Einheit: ms   Min: 0 Max: 65.535 |
| STAT_EV1_MW_EINH | string | ms |
| STAT_LR1_MW_WERT | real | Lambdaregler 1 FAC_LAM_LIM[1]   Einheit: %   Min: -50 Max: 49.9984741210938 |
| STAT_LR1_MW_EINH | string | percent |
| STAT_LR2_MW_WERT | real | Lambdaregler 2 FAC_LAM_LIM[2]   Einheit: %   Min: -50 Max: 49.9984741210938 |
| STAT_LR2_MW_EINH | string | percent |
| STAT_VFZG_MW_WERT | unsigned long | Fahrzeuggeschwindigkeit VS   Einheit: km/h   Min: 0 Max: 255 |
| STAT_VFZG_MW_EINH | string | kmperh |
| STAT_NMOT_W_MW_WERT | unsigned long | Motordrehzahl hoch aufgeloest N   Einheit: rpm   Min: 0 Max: 8160 |
| STAT_NMOT_W_MW_EINH | string | rpm |
| STAT_NSOL_MW_WERT | unsigned long | Leerlauf-Solldrehzahl N_SP_IS   Einheit: rpm   Min: 0 Max: 8160 |
| STAT_NSOL_MW_EINH | string | rpm |
| STAT_CAM_IN_WERT | real | Istwert Einlassnockenwellensteller CAM_IN[1]   Einheit: CRK   Min: 60 Max: 155.625 |
| STAT_CAM_IN_EINH | string | degreeCRK |
| STAT_CAM_EX_WERT | real | Istwert Auslassnockenwellensteller CAM_EX[1]   Einheit: CRK   Min: -135.625 Max: -40 |
| STAT_CAM_EX_EINH | string | degreeCRK |
| STAT_TIA_WERT | real | Ansauglufttemperatur TIA   Einheit: C   Min: -48 Max: 142.5 |
| STAT_TIA_EINH | string | degreeC |
| STAT_TCO_MES_WERT | real | Kuehlmitteltemperatur Rohwert TCO_MES   Einheit: C   Min: -48 Max: 142.5 |
| STAT_TCO_MES_EINH | string | degreeC |
| STAT_IGA_IGC_WERT | real | Zuendwinkel Zylinder 1 IGA_IGC[0]   Einheit: CRK   Min: -35.625 Max: 60 |
| STAT_IGA_IGC_EINH | string | degreeCRK |
| STAT_TPS_AV_1_WERT | real | Drosselklappenwinkel Potentiometer 1 TPS_AV_1   Einheit: TPS   Min: 0 Max: 119.5 |
| STAT_TPS_AV_1_EINH | string | degreeTPS |
| STAT_MAF_KGH_MES_BAS_WERT | real | Gemessene Luftmasse Rohwert MAF_KGH_MES_BAS   Einheit: kg/h   Min: 0 Max: 2047.96875 |
| STAT_MAF_KGH_MES_BAS_EINH | string | kgperh |
| STAT_TQI_AV_WERT | real | aktuelle Drehmomentanforderung TQI_AV   Einheit: Nm   Min: -1024 Max: 1023.96875 |
| STAT_TQI_AV_EINH | string | Nm |
| STAT_VB_WERT | real | Batteriespannung VB   Einheit: V   Min: 0 Max: 25.8984375 |
| STAT_VB_EINH | string | V |
| STAT_V_PVS_1_WERT | real | Pedalwertgeber 1 Rohwert V_PVS_1   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_V_PVS_1_EINH | string | V |
| STAT_TCO_2_MES_WERT | real | Kuehlmittelauslasstemperatur Rohwert TCO_2_MES   Einheit: C   Min: -48 Max: 142.5 |
| STAT_TCO_2_MES_EINH | string | degreeC |
| STAT_NL_0_WERT | real | Spannung Klopfwerte Zylinder 1 NL[0]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_NL_0_EINH | string | V |
| STAT_NL_1_WERT | real | Spannung Klopfwerte Zylinder 5 NL[1]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_NL_1_EINH | string | V |
| STAT_NL_2_WERT | real | Spannung Klopfwerte Zylinder 3 NL[2]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_NL_2_EINH | string | V |
| STAT_NL_3_WERT | real | Spannung Klopfwerte Zylinder 6 NL[3]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_NL_3_EINH | string | V |
| STAT_NL_4_WERT | real | Spannung Klopfwerte Zylinder 2 NL[4]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_NL_4_EINH | string | V |
| STAT_NL_5_WERT | real | Spannung Klopfwerte Zylinder 4 NL[5]   Einheit: V   Min: 0 Max: 4.99992371 |
| STAT_NL_5_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-lrp"></a>
### STATUS_MESSWERTE_LRP

0x22402D STATUS_MESSWERTE_LRP Messwerte Laufruhepruefung auslesen  Fehlende Groessen (Bytes) in der Testerbeschreibung sind mit 0xFF zu befuellen und auszugeben Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AMO_05_WERT | real | Gesamte DFT 0,5 Motorordnung (A2L-Name: Amo_05) AMO_05   Min: 0 Max: 15.9997 |
| STAT_AMO_10_WERT | real | Gesamte DFT 1,0 Motorordnung (A2L-Name: Amo_10) AMO_10   Min: 0 Max: 15.9997 |
| STAT_AMO_15_WERT | real | Gesamte DFT 1,5 Motorordnung (A2L-Name: Amo_15) AMO_15   Min: 0 Max: 15.9997 |
| STAT_AMO_20_WERT | real | Gesamte DFT 2,0 Motorordnung (A2L-Name: Amo_20) AMO_20   Min: 0 Max: 15.9997 |
| STAT_LURABS_F_0_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (A2L-Name: Lurabs_f) LURABS_F_[0]   Min: -3276.8 Max: 3276.7 |
| STAT_LURDIF_F_0_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[0]   Min: -3276.8 Max: 3276.7 |
| STAT_LURABS_F_1_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (A2L-Name: Lurabs_f) LURABS_F_[1]   Min: -3276.8 Max: 3276.7 |
| STAT_LURDIF_F_1_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[1]   Min: -3276.8 Max: 3276.7 |
| STAT_LURABS_F_2_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (A2L-Name: Lurabs_f) LURABS_F_[2]   Min: -3276.8 Max: 3276.7 |
| STAT_LURDIF_F_2_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[2]   Min: -3276.8 Max: 3276.7 |
| STAT_LURABS_F_3_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (A2L-Name: Lurabs_f) LURABS_F_[3]   Min: -3276.8 Max: 3276.7 |
| STAT_LURDIF_F_3_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[3]   Min: -3276.8 Max: 3276.7 |
| STAT_LURABS_F_4_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (A2L-Name: Lurabs_f) LURABS_F_[4]   Min: -3276.8 Max: 3276.7 |
| STAT_LURDIF_F_4_WERT | real | gefilterte mittlere Abweichung des Lur-Wertes (A2L-Name: Lurdif_f) LURDIF_F_[4]   Min: -3276.8 Max: 3276.7 |
| STAT_LURABS_F_5_WERT | real | gefilterte Laufunruhedeltas eines Zylinders (A2L-Name: Lurabs_f) LURABS_F_[5]   Min: -3276.8 Max: 3276.7 |
| STAT_AMO_30_WERT | real | Gesamte DFT 3,0 Motorordnung (A2L-Name: Amo_30) AMO_30   Min: 0 Max: 15.9997 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mil"></a>
### STATUS_MIL

0x30D401 STATUS_MIL MIL (Malfunction Indicator Lamp) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_MIL | unsigned long | Status MIL (Malfunction Indicator Lamp) LV_MIL_CAN   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mls"></a>
### STATUS_MLS

0x30B201 STATUS_MLS Motorlagersteuerung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_MLS | unsigned long | Status Motorlagersteuerung LV_SWI_AEB   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motorlaufunruhe"></a>
### STATUS_MOTORLAUFUNRUHE

0x224003 STATUS_MOTORLAUFUNRUHE Motorlaufunruhewerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZYL1_WERT | real | gefilterte Laufunruhe Zylinder 1 ER_MMV_IS_DIAG[0]   Min: -8 Max: 7.99975586 |
| STAT_ZYL5_WERT | real | gefilterte Laufunruhe Zylinder 5 ER_MMV_IS_DIAG[1]   Min: -8 Max: 7.99975586 |
| STAT_ZYL3_WERT | real | gefilterte Laufunruhe Zylinder 3 ER_MMV_IS_DIAG[2]   Min: -8 Max: 7.99975586 |
| STAT_ZYL6_WERT | real | gefilterte Laufunruhe Zylinder 6 ER_MMV_IS_DIAG[3]   Min: -8 Max: 7.99975586 |
| STAT_ZYL2_WERT | real | gefilterte Laufunruhe Zylinder 2 ER_MMV_IS_DIAG[4]   Min: -8 Max: 7.99975586 |
| STAT_ZYL4_WERT | real | gefilterte Laufunruhe Zylinder 4 ER_MMV_IS_DIAG[5]   Min: -8 Max: 7.99975586 |
| STAT_GEBERRAD_ADAPTION | unsigned long | Kurbelwelle Segmentadaption beendet 0=nein / 1=ja LV_SEG_AD_AVL_ER   Min: 0 Max: 1 |
| STAT_VLS_UP_1_WERT | real | Spannung Lambdasonde vor Katalysator Bank 1 VLS_UP[1]   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_VLS_UP_1_EINH | string | V |
| STAT_VLS_UP_2_WERT | real | Spannung Lambdasonde vor Katalysator Bank 2 VLS_UP[2]   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_VLS_UP_2_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

0x300C01 STATUS_MOTORTEMPERATUR Motortemperatur auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_TMOT_WERT | real | ADC-Wert Motortemperatur VP_TCO[1]   Einheit: V   Min: 0 Max: 4.999847 |
| STAT_ADC_TMOT_EINH | string | V |
| STAT_MOTORTEMPERATUR_WERT | real | Temperatur Motortemperatur TCO_MES   Einheit: C   Min: -48 Max: 142.5 |
| STAT_MOTORTEMPERATUR_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-msaring"></a>
### STATUS_MSARING

0x22401C STATUS_MSARING Ringspeicher Motor-Start/Stop Automatik (MSA) auslesen (nur 4-Zylinder-N43  nicht 6-Zylinder-N53/N54) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MSASTZ | unsigned long | Zaehler aller Startversuche Msastz   Min: 0 Max: 65535 |
| STAT_MSASTZMSA | unsigned long | Zaehler der MSA-Startversuche Msastzmsa   Min: 0 Max: 65535 |
| STAT_MSA_INDEXRS | unsigned long | Ringspeicher-Index Msa_indexrs   Min: 0 Max: 20 |
| STAT_AV20 | unsigned long | Abschaltverhinderer Nr. 20 (Msa_arravrs[59]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM20_WERT | unsigned long | km-Stand Nr. 20 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM20_EINH | string | kilometer |
| STAT_AV19 | unsigned long | Abschaltverhinderer Nr. 19 (Msa_arravrs[56]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM19_WERT | unsigned long | km-Stand Nr. 19 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM19_EINH | string | kilometer |
| STAT_AV18 | unsigned long | Abschaltverhinderer Nr. 18 (Msa_arravrs[53]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM18_WERT | unsigned long | km-Stand Nr. 18 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM18_EINH | string | kilometer |
| STAT_AV17 | unsigned long | Abschaltverhinderer Nr. 17 (Msa_arravrs[50]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM17_WERT | unsigned long | km-Stand Nr. 17 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM17_EINH | string | kilometer |
| STAT_AV16 | unsigned long | Abschaltverhinderer Nr. 16 (Msa_arravrs[47]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM16_WERT | unsigned long | km-Stand Nr. 16 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM16_EINH | string | kilometer |
| STAT_AV15 | unsigned long | Abschaltverhinderer Nr. 15 (Msa_arravrs[44]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM15_WERT | unsigned long | km-Stand Nr. 15 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM15_EINH | string | kilometer |
| STAT_AV14 | unsigned long | Abschaltverhinderer Nr. 14 (Msa_arravrs[41]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM14_WERT | unsigned long | km-Stand Nr. 14 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM14_EINH | string | kilometer |
| STAT_AV13 | unsigned long | Abschaltverhinderer Nr. 13 (Msa_arravrs[38]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM13_WERT | unsigned long | km-Stand Nr. 13 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM13_EINH | string | kilometer |
| STAT_AV12 | unsigned long | Abschaltverhinderer Nr. 12 (Msa_arravrs[35]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM12_WERT | unsigned long | km-Stand Nr. 12 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM12_EINH | string | kilometer |
| STAT_AV11 | unsigned long | Abschaltverhinderer Nr. 11 (Msa_arravrs[32]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM11_WERT | unsigned long | km-Stand Nr. 11 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM11_EINH | string | kilometer |
| STAT_AV10 | unsigned long | Abschaltverhinderer Nr. 10 (Msa_arravrs[29]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM10_WERT | unsigned long | km-Stand Nr. 10 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM10_EINH | string | kilometer |
| STAT_AV09 | unsigned long | Abschaltverhinderer Nr. 09 (Msa_arravrs[26]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM09_WERT | unsigned long | km-Stand Nr. 09 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM09_EINH | string | kilometer |
| STAT_AV08 | unsigned long | Abschaltverhinderer Nr. 08 (Msa_arravrs[23]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM08_WERT | unsigned long | km-Stand Nr. 08 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM08_EINH | string | kilometer |
| STAT_AV07 | unsigned long | Abschaltverhinderer Nr. 07 (Msa_arravrs[20]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM07_WERT | unsigned long | km-Stand Nr. 07 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM07_EINH | string | kilometer |
| STAT_AV06 | unsigned long | Abschaltverhinderer Nr. 06 (Msa_arravrs[17]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM06_WERT | unsigned long | km-Stand Nr. 06 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM06_EINH | string | kilometer |
| STAT_AV05 | unsigned long | Abschaltverhinderer Nr. 05 (Msa_arravrs[14]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM05_WERT | unsigned long | km-Stand Nr. 05 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM05_EINH | string | kilometer |
| STAT_AV04 | unsigned long | Abschaltverhinderer Nr. 04 (Msa_arravrs[11]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM04_WERT | unsigned long | km-Stand Nr. 04 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM04_EINH | string | kilometer |
| STAT_AV03 | unsigned long | Abschaltverhinderer Nr. 03 (Msa_arravrs[8]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM03_WERT | unsigned long | km-Stand Nr. 03 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM03_EINH | string | kilometer |
| STAT_AV02 | unsigned long | Abschaltverhinderer Nr. 02 (Msa_arravrs[5]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM02_WERT | unsigned long | km-Stand Nr. 02 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM02_EINH | string | kilometer |
| STAT_AV01 | unsigned long | Abschaltverhinderer Nr. 01 (Msa_arravrs[2]) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_KM01_WERT | unsigned long | km-Stand Nr. 01 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM01_EINH | string | kilometer |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-msv"></a>
### STATUS_MSV

0x30BD01 STATUS_MSV Mengensteuerventil auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_MSV_WERT | real | Status Mengensteuerventil FUP   Einheit: hPa   Min: 0 Max: 347776 |
| STAT_PHY_MSV_EINH | string | hPa |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-nockenwelle-adaption"></a>
### STATUS_NOCKENWELLE_ADAPTION

0x224006 STATUS_NOCKENWELLE_ADAPTION Nockenwellenadationswerte auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NC_PSN_EDGE_CAM_EX_1_WERT | real | Flanke Auslassnockenwellensteller Zylinder 1 NC_PSN_EDGE_CAM_EX_1   Einheit: Grad KW   Min: 0 Max: 719.9375 |
| STAT_NC_PSN_EDGE_CAM_EX_1_EINH | string | degree_KW |
| STAT_NC_PSN_EDGE_CAM_EX_6_WERT | real | Flanke Auslassnockenwellensteller Zylinder 6 NC_PSN_EDGE_CAM_EX_6   Einheit: Grad KW   Min: 0 Max: 719.9375 |
| STAT_NC_PSN_EDGE_CAM_EX_6_EINH | string | degree_KW |
| STAT_NC_PSN_EDGE_CAM_IN_1_WERT | real | Flanke Einlassnockenwellensteller Zylinder 1 NC_PSN_EDGE_CAM_IN_1   Einheit: Grad KW   Min: 0 Max: 719.9375 |
| STAT_NC_PSN_EDGE_CAM_IN_1_EINH | string | degree_KW |
| STAT_NC_PSN_EDGE_CAM_IN_6_WERT | real | Flanke Einlassnockenwellensteller Zylinder 6 NC_PSN_EDGE_CAM_IN_6   Einheit: Grad KW   Min: 0 Max: 719.9375 |
| STAT_NC_PSN_EDGE_CAM_IN_6_EINH | string | degree_KW |
| STAT_PSN_EDGE_AD_CAM_IN_1_WERT | real | Adapted intake camshaft i signal z position PSN_EDGE_1_AD_CAM_IN_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_IN_1_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_IN_2_WERT | real | Adapted intake camshaft i signal z position PSN_EDGE_2_AD_CAM_IN_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_IN_2_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_IN_3_WERT | real | Adapted intake camshaft i signal z position PSN_EDGE_3_AD_CAM_IN_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_IN_3_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_IN_4_WERT | real | Adapted intake camshaft i signal z position PSN_EDGE_4_AD_CAM_IN_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_IN_4_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_IN_5_WERT | real | Adapted intake camshaft i signal z position PSN_EDGE_5_AD_CAM_IN_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_IN_5_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_IN_6_WERT | real | Adapted intake camshaft i signal z position PSN_EDGE_6_AD_CAM_IN_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_IN_6_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_EX_1_WERT | real | Adapted exhaust camshaft i signal z position PSN_EDGE_1_AD_CAM_EX_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_EX_1_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_EX_2_WERT | real | Adapted exhaust camshaft i signal z position PSN_EDGE_2_AD_CAM_EX_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_EX_2_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_EX_3_WERT | real | Adapted exhaust camshaft i signal z position PSN_EDGE_3_AD_CAM_EX_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_EX_3_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_EX_4_WERT | real | Adapted exhaust camshaft i signal z position PSN_EDGE_4_AD_CAM_EX_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_EX_4_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_EX_5_WERT | real | Adapted exhaust camshaft i signal z position PSN_EDGE_5_AD_CAM_EX_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_EX_5_EINH | string | degreeCRK |
| STAT_PSN_EDGE_AD_CAM_EX_6_WERT | real | Adapted exhaust camshaft i signal z position PSN_EDGE_6_AD_CAM_EX_1   Einheit: CRK   Min: -32 Max: 31.9375 |
| STAT_PSN_EDGE_AD_CAM_EX_6_EINH | string | degreeCRK |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-nox1"></a>
### STATUS_NOX1

0x303B01 STATUS_NOX1 NOx Sensor 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_NOX1_WERT | long | NOx-Konzentration NOX_NS[1]   Einheit: ppm   Min: -100 Max: 1500 |
| STAT_PHY_NOX1_EINH | string | ppm |
| STAT_PHY_ULNOX1_WERT | long | binaeres Spannungssignal VLS_NOX_SENS[1]   Einheit: mV   Min: -200 Max: 1200 |
| STAT_PHY_ULNOX1_EINH | string | mV |
| STAT_PHY_LLNOX1_WERT | real | lineares Lambdasignal LAMB_NOX_SENS[1]   Min: 0 Max: 31.9990234375 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-odr"></a>
### STATUS_ODR

0x30AB01 STATUS_ODR Oel Druck Regelung (Geregeltes Oeldrucksystem) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_P_OEL_IST_WERT | unsigned long | Oeldruck Istwert P_OEL_IST   Einheit: hPa   Min: 0 Max: 65535 |
| STAT_PHY_P_OEL_IST_EINH | string | hPa |
| STAT_PHY_P_OEL_SOLL_WERT | unsigned long | Oeldruck Sollwert P_OEL_SOLL   Einheit: hPa   Min: 0 Max: 65535 |
| STAT_PHY_P_OEL_SOLL_EINH | string | hPa |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ods"></a>
### STATUS_ODS

0x300501 STATUS_ODS Oeldruckschalter auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ODS | unsigned long | Status Oeldruckschalter LV_POIL_SWI   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-odsens"></a>
### STATUS_ODSENS

0x303701 STATUS_ODSENS Oeldrucksensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_ODSENS_WERT | unsigned long | Oeldruck P_OEL_IST   Einheit: hPa   Min: 0 Max: 65535 |
| STAT_PHY_ODSENS_EINH | string | hPa |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-odv"></a>
### STATUS_ODV

0x30AC01 STATUS_ODV Oeldruckventil (Geregeltes Oeldrucksystem) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_ODV_WERT | real | Status Oeldruckventil (Geregeltes Oeldrucksystem) POIL_PWM   Einheit: %   Min: 0 Max: 99.9984741210938 |
| STAT_STAT_ODV_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-oel"></a>
### STATUS_OEL

0x300E01 STATUS_OEL Oelsensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_TOEL_WERT | real | Oeltemperatur TOEL   Einheit: C   Min: -3276.8 Max: 3276.7 |
| STAT_PHY_TOEL_EINH | string | degreeC |
| STAT_PHY_NIVOEL_WERT | real | Oelniveau OZ_NIVAKT   Min: 0 Max: 74.707 |
| STAT_PHY_QOEL_WERT | real | Oelqualitaet OZ_PERMAKT   Min: 0 Max: 5.9999 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pm-backup"></a>
### STATUS_PM_BACKUP

0x225F8B STATUS_PM_BACKUP Auslesen des PM-Backup Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PMBACKUP_0 | unsigned long | PM-Backup Byte 0 PMBACKUP[0]   Min: 0 Max: 255 |
| STAT_PMBACKUP_1 | unsigned long | PM-Backup Byte 1 PMBACKUP[1]   Min: 0 Max: 3 |
| STAT_PMBACKUP_2 | unsigned long | PM-Backup Byte 2 PMBACKUP[2]   Min: 0 Max: 255 |
| STAT_PMBACKUP_3 | unsigned long | PM-Backup Byte 3 PMBACKUP[3]   Min: 0 Max: 3 |
| STAT_PMBACKUP_4 | unsigned long | PM-Backup Byte 4 PMBACKUP[4]   Min: 0 Max: 255 |
| STAT_PMBACKUP_5 | unsigned long | PM-Backup Byte 5 PMBACKUP[5]   Min: 0 Max: 3 |
| STAT_PMBACKUP_6 | unsigned long | PM-Backup Byte 6 PMBACKUP[6]   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pwg-poti-spannung"></a>
### STATUS_PWG_POTI_SPANNUNG

0x302801 STATUS_PWG_POTI_SPANNUNG Fahrerwunsch 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PWG_POTI_SPANNUNG_1_WERT | real | ADC-Wert Fahrerwunsch 1 V_PVS_1   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_PWG_POTI_SPANNUNG_1_EINH | string | V |
| STAT_STAT_PWG1_WERT | real | Status Fahrerwunsch 1 PV_AV_1   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_STAT_PWG1_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-pwg2"></a>
### STATUS_PWG2

0x302901 STATUS_PWG2 Fahrerwunsch 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_PWG2_WERT | real | ADC-Wert Fahrerwunsch 2 V_PVS_2   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_ADC_PWG2_EINH | string | V |
| STAT_STAT_PWG2_WERT | real | Status Fahrerwunsch 2 PV_AV_2   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_STAT_PWG2_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbmmode9"></a>
### STATUS_RBMMODE9

0x224026 STATUS_RBMMODE9 Rate Based Monitoring Mode 9 auslesen (Ausgabe der Werte wie im Scantool Mode 9) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OBDCOND | unsigned long | OBD Monitoring Conditions Encountered Counts (general denominator) CTR_CDN_OBD_RBM   Min: 0 Max: 65535 |
| STAT_IGNCNTR | unsigned long | Ignition Counter CTR_IGK_CYC_RBM   Min: 0 Max: 65535 |
| STAT_CATCOMP1 | unsigned long | Catalyst Monitor Completion Counts Bank 1 (Numerator) CTR_COMP_RBM_CAT_DIAG_1   Min: 0 Max: 65535 |
| STAT_CATCOND1 | unsigned long | Catalyst Monitor Conditions Encountered Counts Bank 1 (Denominator) CTR_CDN_RBM_CAT_DIAG_1   Min: 0 Max: 65535 |
| STAT_CATCOMP2 | unsigned long | Catalyst Monitor Completion Counts Bank 2 (Numerator) CTR_COMP_RBM_CAT_DIAG_2   Min: 0 Max: 65535 |
| STAT_CATCOND2 | unsigned long | Catalyst Monitor Conditions Encountered Counts Bank 2 (Denominator) CTR_CDN_RBM_CAT_DIAG_2   Min: 0 Max: 65535 |
| STAT_O2SCOMP1 | unsigned long | O2 Sensor Monitor Completion Counts Bank 1 (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_O2SCOND1 | unsigned long | O2 Sensor Monitor Conditions Encountered Counts Bank 1 (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_O2SCOMP2 | unsigned long | O2 Sensor Monitor Completion Counts Bank 2 (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_O2SCOND2 | unsigned long | O2 Sensor Monitor Conditions Encountered Counts Bank 2 (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_EGRCOMP | unsigned long | EGR Monitor Completion Condition Counts (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_EGRCOND | unsigned long | EGR Monitor Conditions Encountered Counts (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_AIRCOMP1 | unsigned long | AIR Monitor Completion Condition Counts Bank 1 (Secondary Air) (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_AIRCOND1 | unsigned long | AIR Monitor Conditions Encountered Counts Bank 1 (Secondary Air) (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_AIRCOMP2 | unsigned long | AIR Monitor Completion Condition Counts Bank 2 (Secondary Air) (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_AIRCOND2 | unsigned long | AIR Monitor Conditions Encountered Counts Bank 2 (Secondary Air) (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_EVAPCOMP | unsigned long | EVAP Monitor Completion Condition Counts (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_EVAPCOND | unsigned long | EVAP Monitor Conditions Encountered Counts (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_VVTCOMP1 | unsigned long | Variable Valve Timing (VANOS) Monitor Completion Condition Counts Bank 1 (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_VVTCOND1 | unsigned long | Variable Valve Timing (VANOS) Monitor Conditions Encountered Counts Bank 1 (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_VVTCOMP2 | unsigned long | Variable Valve Timing (VANOS) Monitor Completion Condition Counts Bank 2 (Numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_VVTCOND2 | unsigned long | Variable Valve Timing (VANOS) Monitor Conditions Encountered Counts Bank 2 (Denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbmms1"></a>
### STATUS_RBMMS1

0x224027 STATUS_RBMMS1 Rate Based Monitoring Motorsteuerung MSD80 Block 1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CTR_COMP_RBM_CAT_DIAG_1 | unsigned long | Diagnose Katalysator Sauerstoffspeicherfaehigkeit Bank 1 (Numerator) CTR_COMP_RBM_CAT_DIAG_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_CAT_DIAG_1 | unsigned long | Diagnose Katalysator Sauerstoffspeicherfaehigkeit Bank 1 (Denominator) CTR_CDN_RBM_CAT_DIAG_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_CAT_DIAG_2 | unsigned long | Diagnose Katalysator Sauerstoffspeicherfaehigkeit Bank 2 (Numerator) CTR_COMP_RBM_CAT_DIAG_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_CAT_DIAG_2 | unsigned long | Diagnose Katalysator Sauerstoffspeicherfaehigkeit Bank 2 (Denominator) CTR_CDN_RBM_CAT_DIAG_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_DYN_VLD_LS_UP_1 | unsigned long | Diagnose Dynamikpruefung lineare Lamdasonden Bank 1 (Numerator) CTR_COMP_RBM_DYN_VLD_LS_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_DYN_VLD_LS_UP_1 | unsigned long | Diagnose Dynamikpruefung lineare Lamdasonden Bank 1 (Denominator) CTR_CDN_RBM_DYN_VLD_LS_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_DYN_VLD_LS_UP_2 | unsigned long | Diagnose Dynamikpruefung lineare Lamdasonden Bank 2 (Numerator) CTR_COMP_RBM_DYN_VLD_LS_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_DYN_VLD_LS_UP_2 | unsigned long | Diagnose Dynamikpruefung lineare Lamdasonden Bank 2 (Denominator) CTR_CDN_RBM_DYN_VLD_LS_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SHIFT_AFL_LSL_UP_1 | unsigned long | Diagnose Lamdasondensignalverschiebung mager Bank 1 (Numerator) CTR_COMP_RBM_SHIFT_AFL_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SHIFT_AFL_LSL_UP_1 | unsigned long | Diagnose Lamdasondensignalverschiebung mager Bank 1 (Denominator) CTR_CDN_RBM_SHIFT_AFL_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SHIFT_AFL_LSL_UP_2 | unsigned long | Diagnose Lamdasondensignalverschiebung mager Bank 2 (Numerator) CTR_COMP_RBM_SHIFT_AFL_LSL_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SHIFT_AFL_LSL_UP_2 | unsigned long | Diagnose Lamdasondensignalverschiebung mager Bank 2 (Denominator) CTR_CDN_RBM_SHIFT_AFL_LSL_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SHIFT_AFR_LSL_UP_1 | unsigned long | Diagnose Lamdasondensignalverschiebung fett Bank 1 (Numerator) CTR_COMP_RBM_SHIFT_AFR_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SHIFT_AFR_LSL_UP_1 | unsigned long | Diagnose Lamdasondensignalverschiebung fett Bank 1 (Denominator) CTR_CDN_RBM_SHIFT_AFR_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SHIFT_AFR_LSL_UP_2 | unsigned long | Diagnose Lamdasondensignalverschiebung fett Bank 2 (Numerator) CTR_COMP_RBM_SHIFT_AFR_LSL_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SHIFT_AFR_LSL_UP_2 | unsigned long | Diagnose Lamdasondensignalverschiebung fett Bank 2 (Denominator) CTR_CDN_RBM_SHIFT_AFR_LSL_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_AIR_LSL_UP_1 | unsigned long | Diagnose lineare Lamdasonde korrekt verbaut Bank 1 (Numerator) CTR_COMP_RBM_AIR_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_AIR_LSL_UP_1 | unsigned long | Diagnose lineare Lamdasonde korrekt verbaut Bank 1 (Denominator) CTR_CDN_RBM_AIR_LSL_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_AIR_LSL_UP_2 | unsigned long | Diagnose lineare Lamdasonde korrekt verbaut Bank 2 (Numerator) CTR_COMP_RBM_AIR_LSL_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_AIR_LSL_UP_2 | unsigned long | Diagnose lineare Lamdasonde korrekt verbaut Bank 2 (Denominator) CTR_CDN_RBM_AIR_LSL_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SMALL_LEAK | unsigned long | Diagnose Tankfeinleckpruefung (DMTL) (Numerator) CTR_COMP_RBM_SMALL_LEAK   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SMALL_LEAK | unsigned long | Diagnose Tankfeinleckpruefung (DMTL) (Denominator) CTR_CDN_RBM_SMALL_LEAK   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_REF_CRK_CAM_IN_1 | unsigned long | Diagnose Veraenderung der Steuerzeiten Nockenwelleneinlass (Numerator) CTR_COMP_RBM_REF_CRK_CAM_IN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_REF_CRK_CAM_IN_1 | unsigned long | Diagnose Veraenderung der Steuerzeiten Nockenwelleneinlass (Denominator) CTR_CDN_RBM_REF_CRK_CAM_IN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_REF_CRK_CAM_EX_1 | unsigned long | Diagnose Veraenderung der Steuerzeiten Nockenwellenauslass (Numerator) CTR_COMP_RBM_REF_CRK_CAM_EX_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_REF_CRK_CAM_EX_1 | unsigned long | Diagnose Veraenderung der Steuerzeiten Nockenwellenauslass (Denominator) CTR_CDN_RBM_REF_CRK_CAM_EX_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_MEC_IVVT_IN | unsigned long | Diagnose mechanische Schwergaengigkeit VANOS (Einlass) (Numerator) CTR_COMP_RBM_MEC_IVVT_IN   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_MEC_IVVT_IN | unsigned long | Diagnose mechanische Schwergaengigkeit VANOS (Einlass) (Denominator) CTR_CDN_RBM_MEC_IVVT_IN   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_MEC_IVVT_EX | unsigned long | Diagnose mechanische Schwergaengigkeit VANOS (Auslass) (Numerator) CTR_COMP_RBM_MEC_IVVT_EX   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_MEC_IVVT_EX | unsigned long | Diagnose mechanische Schwergaengigkeit VANOS (Auslass) (Denominator) CTR_CDN_RBM_MEC_IVVT_EX   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TOOTH_OFF_IN_1 | unsigned long | Diagnose sprunghafte Veraenderung der Steuerzeiten Nockenwelleneinlass (Numerator) CTR_COMP_RBM_TOOTH_OFF_IN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TOOTH_OFF_IN_1 | unsigned long | Diagnose sprunghafte Veraenderung der Steuerzeiten Nockenwelleneinlass (Denominator) CTR_CDN_RBM_TOOTH_OFF_IN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TOOTH_OFF_EX_1 | unsigned long | Diagnose sprunghafte Veraenderung der Steuerzeiten Nockenwellenauslass (Numerator) CTR_COMP_RBM_TOOTH_OFF_EX_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TOOTH_OFF_EX_1 | unsigned long | Diagnose sprunghafte Veraenderung der Steuerzeiten Nockenwellenauslass (Denominator) CTR_CDN_RBM_TOOTH_OFF_EX_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SA | unsigned long | Diagnose Sekundaerluftsystem (Numerator) CTR_COMP_RBM_SA   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SA | unsigned long | Diagnose Sekundaerluftsystem (Denominator) CTR_CDN_RBM_SA   Min: 0 Max: 65535 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-rbmms2"></a>
### STATUS_RBMMS2

0x224028 STATUS_RBMMS2 Rate Based Monitoring Motorsteuerung MSD80 Block 2 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CTR_COMP_RBM_DIAGCPS | unsigned long | Diagnose Tankentlueftungssystem (Numerator) CTR_COMP_RBM_DIAGCPS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_DIAGCPS | unsigned long | Diagnose Tankentlueftungssystem (Denominator) CTR_CDN_RBM_DIAGCPS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_ROUGH_LEAK | unsigned long | Diagnose Tankgrobleckpruefung (DMTL) (Numerator) CTR_COMP_RBM_ROUGH_LEAK   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_ROUGH_LEAK | unsigned long | Diagnose Tankgrobleckpruefung (DMTL) (Denominator) CTR_CDN_RBM_ROUGH_LEAK   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_DMTLM | unsigned long | Diagnosemodul Tankleckage (DMTL) (Numerator) CTR_COMP_RBM_DMTLM   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_DMTLM | unsigned long | Diagnosemodul Tankleckage (DMTL) (Denominator) CTR_CDN_RBM_DMTLM   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TH | unsigned long | Diagnose Thermostat (Numerator) CTR_COMP_RBM_TH   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TH | unsigned long | Diagnose Thermostat (Denominator) CTR_CDN_RBM_TH   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TCO_PLAUS | unsigned long | Diagnose Motortemperatur Plausibilitaet (Numerator) CTR_COMP_RBM_TCO_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TCO_PLAUS | unsigned long | Diagnose Motortemperatur Plausibilitaet (Denominator) CTR_CDN_RBM_TCO_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TCO_STUCK | unsigned long | Diagnose Motortemperatur haengendes Sensorsignal (Numerator) CTR_COMP_RBM_TCO_STUCK   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TCO_STUCK | unsigned long | Diagnose Motortemperatur haengendes Sensorsignal (Denominator) CTR_CDN_RBM_TCO_STUCK   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TCO_2_PLAUS | unsigned long | Diagnose Kuehlerauslasstemperatur Plausibilitaet (Numerator) CTR_COMP_RBM_TCO_2_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TCO_2_PLAUS | unsigned long | Diagnose Kuehlerauslasstemperatur Plausibilitaet (Denominator) CTR_CDN_RBM_TCO_2_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TAM_PLAUS | unsigned long | Diagnose Umgebungstemperatur Plausibilitaet (Numerator) CTR_COMP_RBM_TAM_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TAM_PLAUS | unsigned long | Diagnose Umgebungstemperatur Plausibilitaet (Denominator) CTR_CDN_RBM_TAM_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_VS_PLAUS | unsigned long | Diagnose Geschwindigkeit Plausibilitaet (Numerator) CTR_COMP_RBM_VS_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_VS_PLAUS | unsigned long | Diagnose Geschwindigkeit Plausibilitaet (Denominator) CTR_CDN_RBM_VS_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_FTL_OBD | unsigned long | Diagnose Tankfuellstand (Numerator) CTR_COMP_RBM_FTL_OBD   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_FTL_OBD | unsigned long | Diagnose Tankfuellstand (Denominator) CTR_CDN_RBM_FTL_OBD   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_OBD_LSH_DOWN_1 | unsigned long | Diagnose Lamdasondenheizung nach Katalysator Bank 1 (Numerator) CTR_COMP_RBM_OBD_LSH_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_OBD_LSH_DOWN_1 | unsigned long | Diagnose Lamdasondenheizung nach Katalysator Bank 1 (Denominator) CTR_CDN_RBM_OBD_LSH_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_OBD_LSH_DOWN_2 | unsigned long | Diagnose Lamdasondenheizung nach Katalysator Bank 2 (Numerator) CTR_COMP_RBM_OBD_LSH_DOWN_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_OBD_LSH_DOWN_2 | unsigned long | Diagnose Lamdasondenheizung nach Katalysator Bank 2 (Denominator) CTR_CDN_RBM_OBD_LSH_DOWN_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_OBD_VLD_LSH_UP_1 | unsigned long | Diagnose Alterung lineare Lamdasonde Bank 1 (Numerator) CTR_COMP_RBM_OBD_VLD_LSH_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_OBD_VLD_LSH_UP_1 | unsigned long | Diagnose Alterung lineare Lamdasonde Bank 1 (Denominator) CTR_CDN_RBM_OBD_VLD_LSH_UP_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_OBD_VLD_LSH_UP_2 | unsigned long | Diagnose Alterung lineare Lamdasonde Bank 2 (Numerator) CTR_COMP_RBM_OBD_VLD_LSH_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_OBD_VLD_LSH_UP_2 | unsigned long | Diagnose Alterung lineare Lamdasonde Bank 2 (Denominator) CTR_CDN_RBM_OBD_VLD_LSH_UP_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_CS | unsigned long | Diagnose Kupplungsschalter (Numerator) CTR_COMP_RBM_CS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_CS | unsigned long | Diagnose Kupplungsschalter (Denominator) CTR_CDN_RBM_CS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_ISC | unsigned long | Diagnose Leerlaufregler (Numerator) CTR_COMP_RBM_ISC   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_ISC | unsigned long | Diagnose Leerlaufregler (Denominator) CTR_CDN_RBM_ISC   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_MAF | unsigned long | Diagnose Luftmassenmesser (Numerator) CTR_COMP_RBM_MAF   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_MAF | unsigned long | Diagnose Luftmassenmesser (Denominator) CTR_CDN_RBM_MAF   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TIA_PLAUS | unsigned long | Diagnose Ansauglufttemperatur Plausibilitaet (Numerator) CTR_COMP_RBM_TIA_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TIA_PLAUS | unsigned long | Diagnose Ansauglufttemperatur Plausibilitaet (Denominator) CTR_CDN_RBM_TIA_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_AMP_PLAUS | unsigned long | Diagnose Umgebungsdruck Plausibilitaet (Numerator) CTR_COMP_RBM_AMP_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CND_RBM_AMP_PLAUS | unsigned long | Diagnose Umgebungsdruck Plausibilitaet (Denominator) CTR_CDN_RBM_AMP_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_LOAD_TPS_PLAUS | unsigned long | Diagnose Plausibilitaet Drosselklappeposition zu Signal Luftmassenmesser (Numerator) CTR_COMP_RBM_LOAD_TPS_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_LOAD_TPS_PLAUS | unsigned long | Diagnose Plausibilitaet Drosselklappeposition zu Signal Luftmassenmesser (Denominator) CTR_CDN_RBM_LOAD_TPS_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_MAP_DIP_PLAUS | unsigned long | Diagnose Differenzdrucksensor Sauganlage zu Umgebung Plausibilitaet (Numerator) CTR_COMP_RBM_MAP_DIP_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_MAP_DIP_PLAUS | unsigned long | Diagnose Differenzdrucksensor Sauganlage zu Umgebung Plausibilitaet (Denominator) CTR_CDN_RBM_MAP_DIP_PLAUS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_VLS_DOWN_DIF_1 | unsigned long | Diagnose Abweichung Lambdaregelung Bank 1 (Numerator) CTR_COMP_RBM_VLS_DOWN_DIF_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_VLS_DOWN_DIF_1 | unsigned long | Diagnose Abweichung Lambdaregelung Bank 1 (Denominator) CTR_CDN_RBM_VLS_DOWN_DIF_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_VLS_DOWN_DIF_2 | unsigned long | Diagnose Abweichung Lambdaregelung Bank 2 (Numerator) CTR_COMP_RBM_VLS_DOWN_DIF_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_VLS_DOWN_DIF_2 | unsigned long | Diagnose Abweichung Lambdaregelung Bank 2 (Denominator) CTR_CDN_RBM_VLS_DOWN_DIF_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_CHK_LS_DOWN_1 | unsigned long | Diagnose binaere Lamdasonde nach Katalysator Bank 1 (Numerator) CTR_COMP_RBM_CHK_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_CHK_LS_DOWN_1 | unsigned long | Diagnose binaere Lamdasonde nach Katalysator Bank 1 (Denominator) CTR_CDN_RBM_CHK_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_CHK_LS_DOWN_2 | unsigned long | Diagnose binaere Lamdasonde nach Katalysator Bank 2 (Numerator) CTR_COMP_RBM_CHK_LS_DOWN_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_CHK_LS_DOWN_2 | unsigned long | Diagnose binaere Lamdasonde nach Katalysator Bank 2 (Denominator) CTR_CDN_RBM_CHK_LS_DOWN_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SWT_LS_DOWN_1 | unsigned long | Diagnose Schaltzeit binaere Lamdasonde Bank 1 (Numerator) CTR_COMP_RBM_SWT_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SWT_LS_DOWN_1 | unsigned long | Diagnose Schaltzeit binaere Lamdasonde Bank 1 (Denominator) CTR_CDN_RBM_SWT_LS_DOWN_1   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_SWT_LS_DOWN_2 | unsigned long | Diagnose Schaltzeit binaere Lamdasonde Bank 2 (Numerator) CTR_COMP_RBM_SWT_LS_DOWN_2   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_SWT_LS_DOWN_2 | unsigned long | Diagnose Schaltzeit binaere Lamdasonde Bank 2 (Denominator) CTR_CDN_RBM_SWT_LS_DOWN_2   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_T_ES | unsigned long | Diagnose Abstellzeit (Numerator) CTR_COMP_RBM_T_ES   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_T_ES | unsigned long | Diagnose Abstellzeit (Denominator) CTR_CDN_RBM_T_ES   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TPS | unsigned long | Diagnose Drosselklappenlagesensoren (Numerator) CTR_COMP_RBM_TPS   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TPS | unsigned long | Diagnose Drosselklappenlagesensoren (Denominator) CTR_CDN_RBM_TPS   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_ISC_CST | unsigned long | Diagnose Leerlaufregler bei Kaltstart (Numerator) CTR_COMP_RBM_ISC_CST   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_ISC_CST | unsigned long | Diagnose Leerlaufregler bei Kaltstart (Denominator) CTR_CDN_RBM_ISC_CST   Min: 0 Max: 65535 |
| STAT_CTR_COMP_RBM_TQ_CST | unsigned long | Diagnose Momentenreserve bei Kaltstart (Numerator) CTR_COMP_RBM_TQ_CST   Min: 0 Max: 65535 |
| STAT_CTR_CDN_RBM_TQ_CST | unsigned long | Diagnose Momentenreserve bei Kaltstart (Denominator) CTR_CDN_RBM_TQ_CST   Min: 0 Max: 65535 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-readiness"></a>
### STATUS_READINESS

0x2105 STATUS_READINESS Monitorfunktionen und Readinessflags aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_COMPREHENSIVE_TEXT | string | Ueberwachung der uebrigen Komponenten  Test abgeschlossen oder nicht anwendbar = 0  test nicht abgeschlossen = 1 STATE_READY_OBD_1[6] |
| STAT_COMPREHENSIVE_WERT | int |  |
| STAT_FUELSYSTEM_TEXT | string | Ueberwachung Kraftstoffsystem  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_1[5] |
| STAT_FUELSYSTEM_WERT | int |  |
| STAT_MISSFIRE_TEXT | string | Ueberwachung Verbrennungsaussetzer  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_1[4] |
| STAT_MISSFIRE_WERT | int |  |
| STAT_COMPREHENSIVE_MONITOR_TEXT | string | Ueberwachung der uebrigen Komponenten  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 STATE_READY_OBD_1[2] |
| STAT_COMPREHENSIVE_MONITOR_WERT | int |  |
| STAT_FUELSYSTEM_MONITOR_TEXT | string | Ueberwachung Kraftstoffsystem  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 STATE_READY_OBD_1[1] |
| STAT_FUELSYSTEM_MONITOR_WERT | int |  |
| STAT_MISSFIRE_MONITOR_TEXT | string | Ueberwachung Verbrennungsaussetzer  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 STATE_READY_OBD_1[0] |
| STAT_MISSFIRE_MONITOR_WERT | int |  |
| STAT_AGRRDY_EIN_TEXT | string | Ueberwachung Abgasrueckfuehrung  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[7] |
| STAT_AGRRDY_EIN_WERT | int |  |
| STAT_HSRDY_EIN_TEXT | string | Ueberwachung Lambdasondenheizung  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[6] |
| STAT_HSRDY_EIN_WERT | int |  |
| STAT_LSRDY_EIN_TEXT | string | Ueberwachung Lambdasonde  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[5] |
| STAT_LSRDY_EIN_WERT | int |  |
| STAT_KLIMARDY_EIN_TEXT | string | Ueberwachung Klimaanlage  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[4] |
| STAT_KLIMARDY_EIN_WERT | int |  |
| STAT_SLSRDY_EIN_TEXT | string | Ueberwachung Sekundaerluftsystem  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[3] |
| STAT_SLSRDY_EIN_WERT | int |  |
| STAT_TESRDY_EIN_TEXT | string | Ueberwachung Tankentlueftungssystem  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[2] |
| STAT_TESRDY_EIN_WERT | int |  |
| STAT_HKATRDY_EIN_TEXT | string | Ueberwachung Katalysatorheizung  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[1] |
| STAT_HKATRDY_EIN_WERT | int |  |
| STAT_KATRDY_EIN_TEXT | string | Ueberwachung Katalysator  Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[0] |
| STAT_KATRDY_EIN_WERT | int |  |
| STAT_AGRMON_EIN_TEXT | string | Ueberwachung Abgasrueckfuehrung  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[7] |
| STAT_AGRMON_EIN_WERT | int |  |
| STAT_HSMON_EIN_TEXT | string | Ueberwachung Lambdasondenheizung  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[6] |
| STAT_HSMON_EIN_WERT | int |  |
| STAT_LSMON_EIN_TEXT | string | Ueberwachung Lambdasonde  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[5] |
| STAT_LSMON_EIN_WERT | int |  |
| STAT_KLIMAMON_EIN_TEXT | string | Ueberwachung Klimaanlage  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[4] |
| STAT_KLIMAMON_EIN_WERT | int |  |
| STAT_SLSMON_EIN_TEXT | string | Ueberwachung Sekundaerluftsystem  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[3] |
| STAT_SLSMON_EIN_WERT | int |  |
| STAT_TESMON_EIN_TEXT | string | Ueberwachung Tankentlueftungssystem  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[2] |
| STAT_TESMON_EIN_WERT | int |  |
| STAT_HKATMON_EIN_TEXT | string | Ueberwachung Katalysatorheizung  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[1] |
| STAT_HKATMON_EIN_WERT | int |  |
| STAT_KATMON_EIN_TEXT | string | Ueberwachung Katalysator  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[0] |
| STAT_KATMON_EIN_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ruhestrommessung"></a>
### STATUS_RUHESTROMMESSUNG

0x332B STATUS_RUHESTROMMESSUNG Auslesen Ruhestrompruefung mit IBS Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_RUHESTROM_TEXT | string | Funktionsstatus RUHESTROM (Eco_jobstat1) 1BYTE FUNKTIONSSTATUS |
| STAT_FS_RUHESTROM_WERT | int |  |
| STAT_STAT_RUHESTROM_WERT | real | Ruhestrom (Eco_result1) Eco_result1   Einheit: A   Min: 0 Max: 81.9187 |
| STAT_STAT_RUHESTROM_EINH | string | A |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sdf1"></a>
### STATUS_SDF1

0x301801 STATUS_SDF1 Saugrohrdruck1 / Ladedruck1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_SDF1_WERT | real | ADC-Wert Saugrohrdruck1 / Ladedruck1 V_MAP   Einheit: V   Min: 0 Max: 5 |
| STAT_ADC_SDF1_EINH | string | V |
| STAT_PHY_SDF1_WERT | real | Druck Saugrohrdruck1 / Ladedruck1 MAP_DIP_MES_BAS   Einheit: hPa   Min: 0 Max: 5434 |
| STAT_PHY_SDF1_EINH | string | hPa |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sdf2"></a>
### STATUS_SDF2

0x301901 STATUS_SDF2 Saugrohr-, Ladedruck und Ansauglufttemperatur fuer N54 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PVDKDS_WERT | real | Druck vor Drosselklappe (nur N54) PVDKDS   Einheit: hPa   Min: 0 Max: 2559.9609 |
| STAT_PVDKDS_EINH | string | hPa |
| STAT_PS_IST_WERT | real | Druck nach Drosselklappe (nur N54) PS_IST   Einheit: hPa   Min: 0 Max: 2559.9609 |
| STAT_PS_IST_EINH | string | hPa |
| STAT_TANS_WERT | real | Temperatur vor Drosselklappe (nur N54) TANS   Einheit: C   Min: -3276.8 Max: 3276.7 |
| STAT_TANS_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-spt"></a>
### STATUS_SPT

0x300601 STATUS_SPT Sporttaster auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_SPT_WERT | real | ADC-Wert Sporttaster V_SOF_SWI   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_ADC_SPT_EINH | string | V |
| STAT_STAT_SPT | unsigned long | Status Sporttaster LV_SOF_SWI   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-sr"></a>
### STATUS_SR

0x30C401 STATUS_SR Startrelais auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_SR | unsigned long | Status Startrelais LV_RLY_ST   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-dmtl-wert"></a>
### STATUS_SYSTEMCHECK_DMTL_WERT

0x33DA STATUS_SYSTEMCHECK_DMTL_WERT Auslesen Diagnosefunktion DMTL Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1_TEXT | string | State variable for EOL - DMTL (A2L-Name: eol_ram[1]) STATE_EOL_KWP_DMTL   Min: 0 Max: 9 |
| STAT_DIAGNOSE_1_WERT | int |  |
| STAT_DIAGNOSE_2_TEXT | string | Status Diagnosefunktion DMTL STATE_DMTL   Min: 0 Max: 12 |
| STAT_DIAGNOSE_2_WERT | int |  |
| STAT_STROM_REF_WERT | real | Pump current reference leakage (A2L-Name: cur_dmtl_ref_leak) CUR_DMTL_REF_LEAK   Einheit: mA   Min: 0 Max: 400 |
| STAT_STROM_REF_EINH | string | mA |
| STAT_STROM_GROB_WERT | real | Min. pump current in case of rough leak measurement for tester tool (A2L-Name: cur_dmtl_rough_leak_min_eol) CUR_DMTL_ROUGH_LEAK_MIN_EOL   Einheit: mA   Min: 0 Max: 400 |
| STAT_STROM_GROB_EINH | string | mA |
| STAT_STROM_WERT | real | corrected and filtered pump current for tester tool (A2L-Name: cur_dmtl_cor_fil_eol) CUR_DMTL_COR_FIL_EOL   Einheit: mA   Min: 0 Max: 400 |
| STAT_STROM_EINH | string | mA |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-evausbl"></a>
### STATUS_SYSTEMCHECK_EVAUSBL

0x3325 STATUS_SYSTEMCHECK_EVAUSBL Auslesen Diagnosefunktion EinspritzVentile EV-Ausblendung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VENTIL_NR | unsigned long | Nummer des ausgeblendeten Einspritzventils INH_IV_KWP   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-gen"></a>
### STATUS_SYSTEMCHECK_GEN

0x332A STATUS_SYSTEMCHECK_GEN Auslesen Diagnosefunktion Generatortest Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1_TEXT | string | Stati fuer Diagnosefunktion Generatortest ST_GENTEST |
| STAT_DIAGNOSE_1_WERT | int |  |
| STAT_FI_GENEL_TEXT | string | Status elektrischer Fehler Generator GENIUTEST_ERR[0] |
| STAT_FI_GENEL_WERT | int |  |
| STAT_FI_GENMECH_TEXT | string | Status mechanischer Fehler Generator GENIUTEST_ERR[1] |
| STAT_FI_GENMECH_WERT | int |  |
| STAT_FI_GENHT_TEXT | string | Status Hochtemperaturfehler Generator GENIUTEST_ERR[2] |
| STAT_FI_GENHT_WERT | int |  |
| STAT_FI_GENUPL_TEXT | string | Plausibilitaet Generatortyp GENIUTEST_ERR[3] |
| STAT_FI_GENUPL_WERT | int |  |
| STAT_FI_GENKOMM_TEXT | string | Status Generatorkommunikation GENIUTEST_ERR[4] |
| STAT_FI_GENKOMM_WERT | int |  |
| STAT_FI_GENELB_TEXT | string | Plausibilitaet Generatorspannung aus Berechnung GENIUTEST_ERR[5] |
| STAT_FI_GENELB_WERT | int |  |
| STAT_FI_GENHTB_TEXT | string | Hochtemperaturfehler Generator aus Berechnung GENIUTEST_ERR[6] |
| STAT_FI_GENHTB_WERT | int |  |
| STAT_FI_GENREGUPL_TEXT | string | Plausibilitaet Generatorregler GENIUTEST_ERR[7] |
| STAT_FI_GENREGUPL_WERT | int |  |
| STAT_DF_HIGH_TEXT | string | Status Generatorauslastung GENIUTEST_AB[0] |
| STAT_DF_HIGH_WERT | int |  |
| STAT_GENITEST_TOL_WERT | real | Toleranzbereich fuer Abweichung vom Sollwert Strom (GENITEST_TOL) GENITEST_TOL   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_GENITEST_TOL_EINH | string | percent |
| STAT_GENUTEST_TOL_WERT | real | Toleranzbereich fuer Abweichung vom Sollwert Spannung  (GENUTEST_TOL) GENUTEST_TOL   Einheit: %   Min: 0 Max: 99.6093 |
| STAT_GENUTEST_TOL_EINH | string | percent |
| STAT_I_GENTEST_WERT | unsigned long | Modellierter Generatorstrom I_GENTEST   Einheit: A   Min: 0 Max: 255 |
| STAT_I_GENTEST_EINH | string | A |
| STAT_U_GENTEST_WERT | real | Generatorsollspannung U_GENTEST   Einheit: V   Min: 0 Max: 6553.5 |
| STAT_U_GENTEST_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-glf"></a>
### STATUS_SYSTEMCHECK_GLF

0x33D5 STATUS_SYSTEMCHECK_GLF Auslesen Gesteuerte Luftfuehrung Systemcheck Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_GLF_TEXT | string | Funktionsstatus gesteuerte Luftfuehrung STATE_EOL_KWP_ECRAS   Min: 0 Max: 9 |
| STAT_SYSTEMCHECK_GLF_WERT | int |  |
| STAT_GLF_15_TEXT | string | Fehlerstatus gesteuerte Luftfuehrung STATE_ECRS_SYS[15] |
| STAT_GLF_15_WERT | int |  |
| STAT_GLF_14_TEXT | string | Kommunikationsstatus gesteuerte Luftfuehrung STATE_ECRS_SYS[14] |
| STAT_GLF_14_WERT | int |  |
| STAT_GLF_13_TEXT | string | Status Testeransteuerung obere Luftklappe STATE_ECRS_SYS[13] |
| STAT_GLF_13_WERT | int |  |
| STAT_GLF_12_TEXT | string | Status Testeransteuerung untere Luftklappe STATE_ECRS_SYS[12] |
| STAT_GLF_12_WERT | int |  |
| STAT_GLF_11_TEXT | string | Status Eigendiagnose untere Luftklappe STATE_ECRS_SYS[11] |
| STAT_GLF_11_WERT | int |  |
| STAT_GLF_10_TEXT | string | Status Eigendiagnose obere Luftklappe STATE_ECRS_SYS[10] |
| STAT_GLF_10_WERT | int |  |
| STAT_GLF_9_TEXT | string | Status elektrische Diagnose gesteuerte Luftfuehrung STATE_ECRS_SYS[9] |
| STAT_GLF_9_WERT | int |  |
| STAT_GLF_8_TEXT | string | Status Systemtest durchgefuehrt STATE_ECRS_SYS[8] |
| STAT_GLF_8_WERT | int |  |
| STAT_GLF_7_TEXT | string | Status Systemtest aktiv STATE_ECRS_SYS[7] |
| STAT_GLF_7_WERT | int |  |
| STAT_GLF_6_TEXT | string | Fehlerstatus aus Eigendiagnose untere Luftklappe STATE_ECRS_SYS[6] |
| STAT_GLF_6_WERT | int |  |
| STAT_GLF_5_TEXT | string | Fehlerstatus aus Eigendiagnose obere Luftklappe STATE_ECRS_SYS[5] |
| STAT_GLF_5_WERT | int |  |
| STAT_GLF_4_TEXT | string | Status elektrischer Fehler STATE_ECRS_SYS[4] |
| STAT_GLF_4_WERT | int |  |
| STAT_GLF_3_TEXT | string | Status Fehlerabfrage STATE_ECRS_SYS[3] |
| STAT_GLF_3_WERT | int |  |
| STAT_GLF_2_TEXT | string | Status gelernte Variante untere Luftklappe STATE_ECRS_SYS[2] |
| STAT_GLF_2_WERT | int |  |
| STAT_GLF_1_TEXT | string | Status gelernte Variante obere Luftklappe STATE_ECRS_SYS[1] |
| STAT_GLF_1_WERT | int |  |
| STAT_GLF_0_TEXT | string | Status Variantenerkennung STATE_ECRS_SYS[0] |
| STAT_GLF_0_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-igr-aus"></a>
### STATUS_SYSTEMCHECK_IGR_AUS

0x33F7 STATUS_SYSTEMCHECK_IGR_AUS Auslesen Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_IGR_TEXT | string | Funktionsstatus Intelligente Generatorregelung B_DIAGIGR |
| STAT_SYSTEMCHECK_IGR_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-l-regelung-aus"></a>
### STATUS_SYSTEMCHECK_L_REGELUNG_AUS

0x33D9 STATUS_SYSTEMCHECK_L_REGELUNG_AUS Auslesen Lambdaregelung ausschalten Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_L_REGELUNG_AUS | unsigned long | Status der Lambdasondenregelung LV_INH_LAM_KWP   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-l-sonde-werte"></a>
### STATUS_SYSTEMCHECK_L_SONDE_WERTE

0x33DF STATUS_SYSTEMCHECK_L_SONDE_WERTE Auslesen Diagnosefunktion vertauschte Lambdasonden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1_TEXT | string | Allgemeiner Status Diagnosefunktion vertauschte Lambdasonden STATE_EOL_KWP_VLS   Min: 0 Max: 9 |
| STAT_DIAGNOSE_1_WERT | int |  |
| STAT_DIAGNOSE_2_TEXT | string | Status of lambda sensor EOL diagnosis confused wired (A2L-Name: state_vls_eol) STATE_VLS_EOL   Min: 0 Max: 24 |
| STAT_DIAGNOSE_2_WERT | int |  |
| STAT_LAMB_LS_UP_AFR_EOL_1_WERT | real | Frozen VLS value for Lambda sensor EOL diagnosis confused wrong wired (A2L-Name: lamb_ls_up_afr_eol[0]) LAMB_LS_UP_AFR_EOL[1]   Min: 0 Max: 31.9990234375 |
| STAT_LAMB_LS_UP_AFR_EOL_2_WERT | real | Frozen VLS value for Lambda sensor EOL diagnosis confused wrong wired (A2L-Name: lamb_ls_up_afr_eol[1]) LAMB_LS_UP_AFR_EOL[2]   Min: 0 Max: 31.9990234375 |
| STAT_VLS_DOWN_AFR_EOL_1_WERT | real | Frozen VLS value for Lambda sensor EOL diagnosis confused wrong wired (A2L-Name: vls_down_afr_eol[0]) VLS_DOWN_AFR_EOL[1]   Einheit: V   Min: 0 Max: 4.995 |
| STAT_VLS_DOWN_AFR_EOL_1_EINH | string | V |
| STAT_VLS_DOWN_AFR_EOL_2_WERT | real | Frozen VLS value for Lambda sensor EOL diagnosis confused wrong wired (A2L-Name: vls_down_afr_eol[1]) VLS_DOWN_AFR_EOL[2]   Einheit: V   Min: 0 Max: 4.995 |
| STAT_VLS_DOWN_AFR_EOL_2_EINH | string | V |
| STAT_LAMB_LS_UP_AFL_EOL_WERT | real | Frozen VLS value for Lambda sensor EOL diagnosis confused wrong wired (A2L-Name: lamb_ls_up_afl_eol[0]) LAMB_LS_UP_AFL_EOL[1]   Min: 0 Max: 31.9990234375 |
| STAT_LAMB_LS_UP_AFL_EOL_2_WERT | real | Frozen VLS value for Lambda sensor EOL diagnosis confused wrong wired (A2L-Name: lamb_ls_up_afl_eol[1]) LAMB_LS_UP_AFL_EOL[2]   Min: 0 Max: 31.9990234375 |
| STAT_VLS_DOWN_AFL_EOL_1_WERT | real | Frozen VLS value for Lambda sensor EOL diagnosis confused wrong wired (A2L-Name: vls_down_afl_eol[0]) VLS_DOWN_AFL_EOL[1]   Einheit: V   Min: 0 Max: 4.995 |
| STAT_VLS_DOWN_AFL_EOL_1_EINH | string | V |
| STAT_VLS_DOWN_AFL_EOL_2_WERT | real | Frozen VLS value for Lambda sensor EOL diagnosis confused wrong wired (A2L-Name: vls_down_afl_eol[1]) VLS_DOWN_AFL_EOL[2]   Einheit: V   Min: 0 Max: 4.995 |
| STAT_VLS_DOWN_AFL_EOL_2_EINH | string | V |
| STAT_MAF_INT_MIN_VLS_EOL_WERT | real | MAF integral for Lambda sensor EOL diagnosis confused wrong wired (A2L-Name: maf_int_min_vls_eol) MAF_INT_MIN_VLS_EOL   Einheit: g   Min: 0 Max: 1820.4167 |
| STAT_MAF_INT_MIN_VLS_EOL_EINH | string | g |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-llerh-wert"></a>
### STATUS_SYSTEMCHECK_LLERH_WERT

0x3326 STATUS_SYSTEMCHECK_LLERH_WERT Auslesen Diagnosefunktion Leerlauf-Erhoehung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_TEXT | string | State variable for EOL - displace N_SP_IS (A2L-Name: eol_ram[3]) STATE_EOL_KWP_N_SP_IS   Min: 0 Max: 9 |
| STAT_DIAGNOSE_WERT | int |  |
| STAT_SYSTEMCHECK_LLERH_WERT | unsigned long | Istwert LL-Drehzahl N   Einheit: rpm   Min: 0 Max: 8160 |
| STAT_SYSTEMCHECK_LLERH_EINH | string | rpm |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-odr"></a>
### STATUS_SYSTEMCHECK_ODR

0x332C STATUS_SYSTEMCHECK_ODR Auslesen Diagnosefunktion Oeldruckregelung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1_TEXT | string | Stati fuer Diagnosefunktion Oeldruckregelung ST_TESTPOELSYS |
| STAT_DIAGNOSE_1_WERT | int |  |
| STAT_DIAGNOSE_2_TEXT | string | Erweiterte Stati fuer Diagnosefunktion Oeldruckregelung ST_TESTPOELSYS2 |
| STAT_DIAGNOSE_2_WERT | int |  |
| STAT_TOEL_WERT | real | Ausgabewert Motoroeltemperatur fuer LoCAN (A2L-Name: Toel) TOEL   Einheit: C   Min: -3276.8 Max: 3276.7 |
| STAT_TOEL_EINH | string | degreeC |
| STAT_P_OEL_SOLL_WERT | unsigned long | Ã–ldruck Sollwert (A2L-Name: P_oel_soll) P_OEL_SOLL   Einheit: hPa   Min: 0 Max: 65535 |
| STAT_P_OEL_SOLL_EINH | string | hPa |
| STAT_P_OEL_IST_WERT | unsigned long | Ist Ã–ldruck. (A2L-Name: P_oel_ist) P_OEL_IST   Einheit: hPa   Min: 0 Max: 65535 |
| STAT_P_OEL_IST_EINH | string | hPa |
| STAT_NKW_SOLL_WERT | long | Sollwertanforderung Drehzahl aus Funktion Oeldruckregelung NKW_SOLL   Einheit: Upm   Min: -32768 Max: 32767 |
| STAT_NKW_SOLL_EINH | string | Upm |
| STAT_NKW_WERT | unsigned long | Istwert Drehzahl N   Einheit: rpm   Min: 0 Max: 8160 |
| STAT_NKW_EINH | string | rpm |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-pm-messemode"></a>
### STATUS_SYSTEMCHECK_PM_MESSEMODE

0x33F6 STATUS_SYSTEMCHECK_PM_MESSEMODE Auslesen Messemode Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_PM_MESSEMODE | unsigned long | Funktionsstatus Powermanagement Messemode LV_POW_MNG_MES_MOD   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-tev-wert"></a>
### STATUS_SYSTEMCHECK_TEV_WERT

0x3322 STATUS_SYSTEMCHECK_TEV_WERT Auslesen Diagnosefunktion Tankentlueftungsventil Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAGNOSE_1_TEXT | string | State variable for EOL - CPS_CHECK (A2L-Name: eol_ram[0]) STATE_EOL_KWP_CPS   Min: 0 Max: 9 |
| STAT_DIAGNOSE_1_WERT | int |  |
| STAT_DIAGNOSE_2_TEXT | string | Status Diagnosefunktion Tankentlueftungsventil STATE_DIAGCPS   Min: 0 Max: 5 |
| STAT_DIAGNOSE_2_WERT | int |  |
| STAT_SYSTEMCHECK_TEV_FUNC_1_WERT | unsigned long | Number of diagnoses if EOL-Test is active - Functional check CPS (A2L-Name: sum_diag_diagcps_eol) SUM_DIAG_DIAGCPS_EOL   Einheit: cyc   Min: 0 Max: 255 |
| STAT_SYSTEMCHECK_TEV_FUNC_1_EINH | string | cyc |
| STAT_SYSTEMCHECK_TEV_FUNC_2_WERT | unsigned long | Number of step 2 loops which have been passed if EOL-Test is active - fuctional check CPS (A2L-Name: sum_flow_sp_diagcps_eol) SUM_FLOW_SP_DIAGCPS_EOL   Einheit: cyc   Min: 0 Max: 255 |
| STAT_SYSTEMCHECK_TEV_FUNC_2_EINH | string | cyc |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tabg1"></a>
### STATUS_TABG1

0x301201 STATUS_TABG1 Abgastemperatur1 auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_TABG1_WERT | real | Sensorspannung Abgastemperatur VP_TEG_PCAT_DOWN   Einheit: V   Min: 0 Max: 4.999847 |
| STAT_ADC_TABG1_EINH | string | V |
| STAT_PHY_TABG1_WERT | real | Abgastemperatur TEG_PCAT_DOWN_1   Einheit: C   Min: 0 Max: 1023.984375 |
| STAT_PHY_TABG1_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tev"></a>
### STATUS_TEV

0x30CF01 STATUS_TEV Tankentlueftungsventil auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_TEV_WERT | real | Status Tankentlueftungsventil CPPWM_CPS   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_STAT_TEV_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-tka"></a>
### STATUS_TKA

0x300D01 STATUS_TKA Kuehlerauslasstemperatur auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_TKA_WERT | real | ADC-Wert Kuehlerauslasstemperatur VP_TCO[2]   Einheit: V   Min: 0 Max: 4.999847 |
| STAT_ADC_TKA_EINH | string | V |
| STAT_PHY_TKA_WERT | real | Temperatur Kuehlerauslasstemperatur TCO_2_MES   Einheit: C   Min: -48 Max: 142.5 |
| STAT_PHY_TKA_EINH | string | degreeC |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ttemp"></a>
### STATUS_TTEMP

0x302F01 STATUS_TTEMP Taster Tempomat auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_TTEMP_TEXT | string | BITFELD Taster Tempomat STATE_MSW_CAN   Min: 0 Max: 7 |
| STAT_STAT_TTEMP_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ubat"></a>
### STATUS_UBAT

0x302701 STATUS_UBAT Batteriesensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_UBAT_WERT | real | ADC-Wert Batteriesensor VB_BAS   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_ADC_UBAT_EINH | string | V |
| STAT_PHY_UBAT_WERT | real | Spannung Batteriesensor U_BATT   Einheit: V   Min: 6 Max: 22.3837 |
| STAT_PHY_UBAT_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

0x301C01 STATUS_UBATT Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_UVSG_WERT | real | ADC-Wert Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) VB_BAS   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_ADC_UVSG_EINH | string | V |
| STAT_UBATT_WERT | real | Spannung Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) VB   Einheit: V   Min: 0 Max: 25.8984375 |
| STAT_UBATT_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-udf"></a>
### STATUS_UDF

0x301701 STATUS_UDF Umgebungsdruck auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_UDF_WERT | real | ADC-Wert Umgebungsdruck V_AMP   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_ADC_UDF_EINH | string | V |
| STAT_PHY_UDF_WERT | real | Druck Umgebungsdruck AMP_MES   Einheit: hPa   Min: 0 Max: 5434 |
| STAT_PHY_UDF_EINH | string | hPa |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ugen"></a>
### STATUS_UGEN

0x303201 STATUS_UGEN Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_UGEN_WERT | real | Spannung Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) V_ALTER_SP   Einheit: V   Min: 10.6 Max: 16.9 |
| STAT_PHY_UGEN_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-ukl15"></a>
### STATUS_UKL15

0x301B01 STATUS_UKL15 Kl.15 Spannung auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADC_UKL15_WERT | real | ADC-Wert Kl.15 Spannung V_IGK_BAS   Einheit: V   Min: 0 Max: 4.9951171875 |
| STAT_ADC_UKL15_EINH | string | V |
| STAT_PHY_UKL15_WERT | real | Spannung Kl.15 Spannung V_IGK_MES   Einheit: V   Min: 0 Max: 28.7055 |
| STAT_PHY_UKL15_EINH | string | V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-agk"></a>
### STEUERN_AGK

0x30C107 STEUERN_AGK Abgasklappe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_AGK_WERT | unsigned long | Sollwert LV_ACT_EF_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_AGK_WERT | unsigned long | Timeout 0 bis 508s 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-agr"></a>
### STEUERN_AGR

0x30BE07 STEUERN_AGR AbgasRueckfuehr (AGR) Ventil ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_AGR_WERT | real | Tastverhaeltniss Abgasrueckfuehrungsventil OPG_SP_ACR_EXT_ADJ   Einheit: %   Min: 0 Max: 99.9755859375 |
| SW_TO_AGR_WERT | unsigned long | Timeout AbgasRueckfuehr (AGR) Ventil 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-anws"></a>
### STEUERN_ANWS

0x30EE07 STEUERN_ANWS Vanos Auslass Ventil ansteuern Aktivierung: Drehzahl &gt; 1000 1/min Activation: N &gt; C_N_MIN_KWP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ANWS_WERT | real | Sollwert Vanos_A Ventil CAM_SP_EX_EXT_ADJ   Einheit: CRK   Min: -128 Max: 52300 |
| SW_TO_ANWS_WERT | unsigned long | Timeout Vanos_A Ventil 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-betriebsart"></a>
### STEUERN_BETRIEBSART

0x2E5FF807 STEUERN_BETRIEBSART Betriebsarten vorgeben Aktivierung: Klemme 15 = EIN UND Leerlauf Activation: LV_IGK = 1 UND LV_IS = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_BA_SOLL_WERT | unsigned long | Sollwert Betriebsart, 1 = Homogen, 2 = Homogen-Schicht, 3 = Schicht, 4 = Homogen und Lambda = 1 STATE_HOM_AFS_REQ_EXT_ADJ   Min: 0 Max: 65535 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-bze"></a>
### STEUERN_CODIERUNG_BZE

0x2E3230 STEUERN_CODIERUNG_BZE Codierung fuer BZE (Batterie Zustands Erkennung) vorgeben. Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_CD_HERST1_WERT | unsigned long | Codierung Hersteller 1 (A2L-Name: Qv_cdherst_2) Qv_cdherst_1   Min: 0 Max: 255 |
| SW_CD_HERST2_WERT | unsigned long | Codierung Hersteller 2 (A2L-Name: Qv_cdherst_2) Qv_cdherst_2   Min: 0 Max: 255 |
| SW_CD_HERST3_WERT | unsigned long | Codierung Hersteller 3 (A2L-Name: Qv_cdherst_3) Qv_cdherst_3   Min: 0 Max: 255 |
| SW_CD_HERST4_WERT | unsigned long | Codierung Hersteller 4 (A2L-Name: Qv_cdherst_4) Qv_cdherst_4   Min: 0 Max: 255 |
| SW_CD_HERST5_WERT | unsigned long | Codierung Hersteller 5 (A2L-Name: Qv_cdherst_5) Qv_cdherst_5   Min: 0 Max: 255 |
| SW_CD_HERST6_WERT | unsigned long | Codierung Hersteller 6 (A2L-Name: Qv_cdherst_6) Qv_cdherst_6   Min: 0 Max: 255 |
| SW_CD_HERST7_WERT | unsigned long | Codierung Hersteller 7 (A2L-Name: Qv_cdherst_7) Qv_cdherst_7   Min: 0 Max: 255 |
| SW_CD_HERST8_WERT | unsigned long | Codierung Hersteller 8 (A2L-Name: Qv_cdherst_8) Qv_cdherst_8   Min: 0 Max: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-igr"></a>
### STEUERN_CODIERUNG_IGR

0x2E3210 STEUERN_CODIERUNG_IGR Codierung fuer IGR (Intelligente Generator-Regelung) vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_IGR_WERT | unsigned long | Vorgabe fuer Codierung IGR LV_ALTER_CTL_ENA   Min: 0 Max: 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-kat"></a>
### STEUERN_CODIERUNG_KAT

0x2E3001 STEUERN_CODIERUNG_KAT Codierung fuer Katalysator vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min UND Betriebsstundenzaehler &lt; 10 h Activation: LV_IGK = 1 UND LV_ES = 1 UND TRT &lt; 10 h

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_KAT_WERT | unsigned long | Vorgabe fuer Codierung Katalysator LV_CAT_CONF_DIS_EXT_REQ   Min: 0 Max: 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-leistungsstufe"></a>
### STEUERN_CODIERUNG_LEISTUNGSSTUFE

0x2E3020 STEUERN_CODIERUNG_LEISTUNGSSTUFE Codierung fuer Leistungsstufe vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min UND Betriebsstundenzaehler &lt; 10 h Activation: LV_IGK = 1 UND LV_ES = 1 UND TRT &lt; 10 h

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LEISTUNGSSTUFE_WERT | unsigned long | Vorgabe fuer Codierung Leistungsstufe POW_CONF_IDX_EXT_REQ   Min: 0 Max: 3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-mil"></a>
### STEUERN_CODIERUNG_MIL

0x2E3000 STEUERN_CODIERUNG_MIL Codierung fuer MIL (Malfunction Indication Lamp) vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min UND Betriebsstundenzaehler &lt; 10 h Activation: LV_IGK = 1 UND LV_ES = 1 UND TRT &lt; 10 h

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_MIL_WERT | unsigned long | Vorgabe fuer Codierung MIL STATE_MIL_ON_DIS_EXT_REQ   Min: 0 Max: 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-oel"></a>
### STEUERN_CODIERUNG_OEL

0x2E3200 STEUERN_CODIERUNG_OEL Codierung fuer Oelwechselintervall vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LAENDERFAKTOR_1_WERT | real | Vorgabe fuer Codierung Laenderfaktor 1 FAC_OIL_EXT_REQ_1   Min: 0 Max: 2.55 |
| STAT_LAENDERFAKTOR_2_WERT | real | Vorgabe fuer Codierung Laenderfaktor 2 FAC_OIL_EXT_REQ_2   Min: 0 Max: 2.55 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-protokoll"></a>
### STEUERN_CODIERUNG_PROTOKOLL

0x2E3030 STEUERN_CODIERUNG_PROTOKOLL Codierung Protokoll vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min UND Betriebsstundenzaehler &lt; 10 h Activation: LV_IGK = 1 UND LV_ES = 1 UND TRT &lt; 10 h

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PROTOKOLL_WERT | unsigned long | Codierung Protokoll vorgeben: 0 = Protokoll 15765_4 Anlieferzustand  1 = Protokoll 15765_4 codiert  2 = Protokoll 14230 codiert PROT_CONF_IDX_EXT_REQ   Min: 0 Max: 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-spa"></a>
### STEUERN_CODIERUNG_SPA

0x2E3220 STEUERN_CODIERUNG_SPA Codierung fuer SPA (Schaltpunktanzeige) vorgeben. Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_B_SPA_CSOLL_WERT | unsigned long | Codierung Schaltpunktanzeige fuer Tester B_SPA_CSOLL   Min: 0 Max: 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-vmax"></a>
### STEUERN_CODIERUNG_VMAX

0x2E3010 STEUERN_CODIERUNG_VMAX Codierung fuer maximale Geschwindigkeit vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min UND Betriebsstundenzaehler &lt; 10 h Activation: LV_IGK = 1 UND LV_ES = 1 UND TRT &lt; 10 h

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_VMAX_WERT | unsigned long | Vorgabe fuer Codierung maximale Geschwindigkeit VS_MAX_SEL_EXT_REQ   Min: 0 Max: 3 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-codierung-xenon"></a>
### STEUERN_CODIERUNG_XENON

0x2E3211 STEUERN_CODIERUNG_XENON Codierung fuer Xenon-Lichtverbau vorgeben Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CODIERUNG_XENON_WERT | unsigned long | Vorgabe fuer Codierung Xenon-Lichtverbau LV_LTG_GAS_ENA   Min: 0 Max: 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-desulfatisierung"></a>
### STEUERN_DESULFATISIERUNG

0x312D STEUERN_DESULFATISIERUNG Ansteuerung Desulfatisierung Aktivierung: Drehzahl &gt; C_N_IS_SO2P_MIN UND Ganginfo = 0 UND Kupplungsschalter = Aus UND Geschwindigkeit &lt;= C_VS_SO2P_EXT_MAX UND Pedalwert &lt;= C_PV_SO2P_EXT_MAX Activation: N_32 &gt;= C_N_IS_SO2P_MIN UND GEAR = 0 UND LV_CLU_SWI = 0 UND VS &lt;= C_VS_SO2P_EXT_MAX UND PV_AV &lt;= C_PV_SO2P_EXT_MAX

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATE_NT_SO2P_EXT_ADJ_WERT | unsigned long | Parameter Desulfatisierungsstrategie, 0 = schnelle Desulfatisierung, 1 = alternierende Desulfatisierung STATE_NT_SO2P_EXT_ADJ   Min: 0 Max: 1 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-disa"></a>
### STEUERN_DISA

0x30C607 STEUERN_DISA Variable Sauganlage (DISA) Klappe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DISA_WERT | unsigned long | Sollwert Variable Sauganlage (DISA) Klappe LV_VIM_1_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_DISA_WERT | unsigned long | Timeout Variable Sauganlage (DISA) Klappe 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-disa2"></a>
### STEUERN_DISA2

0x30AE07 STEUERN_DISA2 Variable Sauganlage (DISA) Klappe2 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DISA2_WERT | unsigned long | Sollwert Variable Sauganlage (DISA) Klappe2 LV_VIM_2_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_DISA2_WERT | unsigned long | Timeout Variable Sauganlage (DISA) Klappe2 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dk"></a>
### STEUERN_DK

0x302A07 STEUERN_DK Drosselklappe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DK_WERT | real | Sollwert Drosselklappe TPS_SP_EXT_ADJ   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_DK_WERT | unsigned long | Timeout Drosselklappe 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dkh"></a>
### STEUERN_DKH

0x309E07 STEUERN_DKH Drosselklappenbeheizung ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DKH_WERT | unsigned long | Tastverhaeltniss Drosselklappenbeheizung LV_ACT_RLY_MTC_HEAT_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_DKH_WERT | unsigned long | Timeout Drosselklappenbeheizung 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-heizung"></a>
### STEUERN_DMTL_HEIZUNG

0x30CE07 STEUERN_DMTL_HEIZUNG Diagnosemodul-Tank Leckage Heizung ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTLH_WERT | unsigned long | Sollwert Diagnosemodul-Tank Leckage Heizung LV_ACT_DMTLH_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_DMTLH_WERT | unsigned long | Timeout Diagnosemodul-Tank Leckage Heizung 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-p"></a>
### STEUERN_DMTL_P

0x30CC07 STEUERN_DMTL_P Diagnosemodul-Tank Leckage Pumpe ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTL_P_WERT | unsigned long | Sollwert Diagnosemodul-Tank Leckage Pumpe LV_ACT_DMTL_PUMP_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_DMTL_P_WERT | unsigned long | Timeout Diagnosemodul-Tank Leckage Pumpe 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-dmtl-v"></a>
### STEUERN_DMTL_V

0x30CD07 STEUERN_DMTL_V Diagnosemodul-Tank Leckage Ventil ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_DMTL_V_WERT | unsigned long | Sollwert Diagnosemodul-Tank Leckage Ventil LV_ACT_DMTLS_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_DMTL_V_WERT | unsigned long | Timeout Diagnosemodul-Tank Leckage Ventil 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

0x30DA07 STEUERN_E_LUEFTER E-Luefter ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Motortemperatur &lt; 95 Grad C UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND TCO &lt; C_TCO_MAX_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ELUE_WERT | real | Tastverhaeltniss E-Luefter ECFPWM_ECF_EXT_ADJ   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_ELUE_WERT | unsigned long | Timeout E-Luefter 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ebl"></a>
### STEUERN_EBL

0x30C807 STEUERN_EBL E-Box-Luefter ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EBL_WERT | unsigned long | Sollwert E-Box-Luefter LV_ACT_EBOX_CFA_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_EBL_WERT | unsigned long | Timeout E-Box-Luefter 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eisydr"></a>
### STEUERN_EISYDR

0x31E2 STEUERN_EISYDR Ansteuern Eisy-Adaptionswerte mit Druckregelung Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_WERT | long | Drehzahl NKW_SOLL   Einheit: Upm   Min: -32768 Max: 32767 |
| VSE_SPRI_WERT | real | Istwert Einlassspreizung variable NWS VSE_SPRI   Einheit: Grad KW   Min: 0 Max: 6553.5 |
| VSA_SPRI_WERT | real | Istwert Auslassspreizung variable NWS VSA_SPRI   Einheit: Grad KW   Min: 0 Max: 6553.5 |
| WDK_IST_WERT | real | Winkel Drosselklappe WDK_IST   Einheit: %   Min: -800 Max: 799.9755 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eisygd"></a>
### STEUERN_EISYGD

0x31E1 STEUERN_EISYGD Ansteuern Eisy-Adaptionswerte (gedrosselt) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_WERT | long | Drehzahl NKW_SOLL   Einheit: Upm   Min: -32768 Max: 32767 |
| VSE_SPRI_WERT | real | Istwert Einlassspreizung variable NWS VSE_SPRI   Einheit: Grad KW   Min: 0 Max: 6553.5 |
| VSA_SPRI_WERT | real | Istwert Auslassspreizung variable NWS VSA_SPRI   Einheit: Grad KW   Min: 0 Max: 6553.5 |
| WDK_IST_WERT | real | Aktueller Drosselklappenwinkel WDK_IST   Einheit: %   Min: -800 Max: 799.9755 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

0x30D807 STEUERN_EKP Elektrische Kraftstoffpumpe 1 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EKP1_WERT | real | Sollwert Elektrische Kraftstoffpumpe 1 EFPPWM_EXT_ADJ   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_EKP1_WERT | unsigned long | Timeout Elektrische Kraftstoffpumpe 1 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-eml"></a>
### STEUERN_EML

0x30D607 STEUERN_EML EML (Engine Malfunction Lamp) ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EML_WERT | unsigned long | Sollwert EML (Engine Malfunction Lamp) LV_ACT_WAL_1_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_EML_WERT | unsigned long | Timeout EML (Engine Malfunction Lamp) 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-agk"></a>
### STEUERN_ENDE_AGK

0x30C100 STEUERN_ENDE_AGK Abgasklappe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-agr"></a>
### STEUERN_ENDE_AGR

0x30BE00 STEUERN_ENDE_AGR AbgasRueckfuehr (AGR) Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-anws"></a>
### STEUERN_ENDE_ANWS

0x30EE00 STEUERN_ENDE_ANWS Vanos Auslass Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-betriebsart"></a>
### STEUERN_ENDE_BETRIEBSART

0x2E5FF800 STEUERN_ENDE_BETRIEBSART Betriebsarten Vorgeben beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-desulfatisierung"></a>
### STEUERN_ENDE_DESULFATISIERUNG

0x322D STEUERN_ENDE_DESULFATISIERUNG Ansteuerung Desulfatisierung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-disa"></a>
### STEUERN_ENDE_DISA

0x30C600 STEUERN_ENDE_DISA Variable Sauganlage (DISA) Klappe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-disa2"></a>
### STEUERN_ENDE_DISA2

0x30AE00 STEUERN_ENDE_DISA2 Variable Sauganlage (DISA) Klappe2 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dk"></a>
### STEUERN_ENDE_DK

0x302A00 STEUERN_ENDE_DK Drosselklappe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dkh"></a>
### STEUERN_ENDE_DKH

0x309E00 STEUERN_ENDE_DKH Drosselklappenbeheizung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-heizung"></a>
### STEUERN_ENDE_DMTL_HEIZUNG

0x30CE00 STEUERN_ENDE_DMTL_HEIZUNG Diagnosemodul-Tank Leckage Heizung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-p"></a>
### STEUERN_ENDE_DMTL_P

0x30CC00 STEUERN_ENDE_DMTL_P Diagnosemodul-Tank Leckage Pumpe Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-dmtl-v"></a>
### STEUERN_ENDE_DMTL_V

0x30CD00 STEUERN_ENDE_DMTL_V Diagnosemodul-Tank Leckage Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-e-luefter"></a>
### STEUERN_ENDE_E_LUEFTER

0x30DA00 STEUERN_ENDE_E_LUEFTER E-Luefter Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ebl"></a>
### STEUERN_ENDE_EBL

0x30C800 STEUERN_ENDE_EBL E-Box-Luefter Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ekp"></a>
### STEUERN_ENDE_EKP

0x30D800 STEUERN_ENDE_EKP Elektrische Kraftstoffpumpe 1 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-eml"></a>
### STEUERN_ENDE_EML

0x30D600 STEUERN_ENDE_EML EML (Engine Malfunction Lamp) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-enws"></a>
### STEUERN_ENDE_ENWS

0x30ED00 STEUERN_ENDE_ENWS Vanos Einlass Ventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ewap"></a>
### STEUERN_ENDE_EWAP

0x30BF00 STEUERN_ENDE_EWAP elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-glf"></a>
### STEUERN_ENDE_GLF

0x30C300 STEUERN_ENDE_GLF Gesteuerte Luftfuehrung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-glf2"></a>
### STEUERN_ENDE_GLF2

0x30A400 STEUERN_ENDE_GLF2 Gesteuerte Luftfuehrung Klappe 2 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-kft"></a>
### STEUERN_ENDE_KFT

0x30C900 STEUERN_ENDE_KFT Kennfeldthermostat Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-kgeh"></a>
### STEUERN_ENDE_KGEH

0x30AD00 STEUERN_ENDE_KGEH Kurbelgehaeuseentlueftungsheizung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-korel"></a>
### STEUERN_ENDE_KOREL

0x30C700 STEUERN_ENDE_KOREL Klimakompressor-Relais Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lds1"></a>
### STEUERN_ENDE_LDS1

0x30B600 STEUERN_ENDE_LDS1 Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lds2"></a>
### STEUERN_ENDE_LDS2

0x30B700 STEUERN_ENDE_LDS2 Ladedrucksteller 2 (z.B. Waste Gate oder VTG variable Turbinengeometrie) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh1"></a>
### STEUERN_ENDE_LSH1

0x30D000 STEUERN_ENDE_LSH1 Lambdasondenheizung vor Kat Bank1 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh2"></a>
### STEUERN_ENDE_LSH2

0x30D100 STEUERN_ENDE_LSH2 Lambdasondenheizung hinter Kat Bank1 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh3"></a>
### STEUERN_ENDE_LSH3

0x30D200 STEUERN_ENDE_LSH3 Lambdasondenheizung vor Kat Bank2 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-lsh4"></a>
### STEUERN_ENDE_LSH4

0x30D300 STEUERN_ENDE_LSH4 Lambdasondenheizung hinter Kat Bank2 Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-mil"></a>
### STEUERN_ENDE_MIL

0x30D400 STEUERN_ENDE_MIL MIL (Malfunction Indicator Lamp) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-mls"></a>
### STEUERN_ENDE_MLS

0x30B200 STEUERN_ENDE_MLS Motorlagersteuerung Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-msv"></a>
### STEUERN_ENDE_MSV

0x30BD00 STEUERN_ENDE_MSV Mengensteuerventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-odr"></a>
### STEUERN_ENDE_ODR

0x30AB00 STEUERN_ENDE_ODR Oel Druck Regelung (Geregeltes Oeldrucksystem) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-odv"></a>
### STEUERN_ENDE_ODV

0x30AC00 STEUERN_ENDE_ODV Oeldruckventil (Geregeltes Oeldrucksystem) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-sr"></a>
### STEUERN_ENDE_SR

0x30C400 STEUERN_ENDE_SR Startrelais Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-tev"></a>
### STEUERN_ENDE_TEV

0x30CF00 STEUERN_ENDE_TEV Tankentlueftungsventil Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-ugen"></a>
### STEUERN_ENDE_UGEN

0x303200 STEUERN_ENDE_UGEN Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-uvsg"></a>
### STEUERN_ENDE_UVSG

0x301C00 STEUERN_ENDE_UVSG Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) Ansteuerung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-energiesparmode"></a>
### STEUERN_ENERGIESPARMODE

0x310C STEUERN_ENERGIESPARMODE Energiesparmode aktivieren Aktivierung: Klemme 15 = EIN UND Setzen Energiesparmode ueber Tester freigeschaltet Activation: LV_IGK = 1 UND LC_EGY_MIN_KWP = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EGY_WERT | unsigned long | recordLocalID STATE_EGY_MIN_KWP   Min: 0 Max: 4 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENERGIESPARMODE_TEXT | string | Status Energiesparmode  00 = Passiv, 01 = Fertigung, 02 = Transport, 04 = Werkstatt STATE_EGY_MIN_KWP   Min: 0 Max: 3 |
| STAT_ENERGIESPARMODE_WERT | int |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-enws"></a>
### STEUERN_ENWS

0x30ED07 STEUERN_ENWS Vanos Einlass Ventil ansteuern Aktivierung: Drehzahl &gt; 1000 1/min Activation: N &gt; C_N_MIN_KWP

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ENWS_WERT | real | Sollwert Vanos_E Ventil CAM_SP_IN_EXT_ADJ   Einheit: CRK   Min: -128 Max: 52300 |
| SW_TO_ENWS_WERT | unsigned long | Timeout Vanos_E Ventil 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ewap"></a>
### STEUERN_EWAP

0x30BF07 STEUERN_EWAP elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Motortemperatur &lt; 95 Grad C UND Drehzahl = 0 1/min  UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND TCO &lt; C_TCO_MAX_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_EWAP_WERT | real | Sollwert elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) N_REL_CWP_SP_EXT_ADJ   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_EWAP_WERT | unsigned long | Timeout elektr. Wasserpumpe ueber BSD (Bit Serielle Datenschnittstelle) 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-glf"></a>
### STEUERN_GLF

0x30C307 STEUERN_GLF Gesteuerte Luftfuehrung ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Motortemperatur &lt; 95 Grad C UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND TCO &lt; C_TCO_MAX_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_GLF_WERT | unsigned long | Sollwert Gesteuerte Luftfuehrung LV_ACT_ECRAS_UP_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_GLF_WERT | unsigned long | Timeout Gesteuerte Luftfuehrung 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-glf2"></a>
### STEUERN_GLF2

0x30A407 STEUERN_GLF2 Gesteuerte Luftfuehrung Klappe 2 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Motortemperatur &lt; 95 Grad C UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND TCO &lt; C_TCO_MAX_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_GLF2_WERT | unsigned long | Ansteuerung Gesteuerte Luftfuehrung Klappe 2 LV_ACT_ECRAS_DOWN_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_GLF2_WERT | unsigned long | Timeout Gesteuerte Luftfuehrung Klappe 2 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kft"></a>
### STEUERN_KFT

0x30C907 STEUERN_KFT Kennfeldthermostat ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_KFT_WERT | real | Sollwert Kennfeldthermostat ECTPWM_EXT_ADJ   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_KFT_WERT | unsigned long | Timeout Kennfeldthermostat 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kgeh"></a>
### STEUERN_KGEH

0x30AD07 STEUERN_KGEH Kurbelgehaeuseentlueftungsheizung ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_KGEH_WERT | unsigned long | Sollwert Kurbelgehaeuseentlueftungsheizung LV_ACT_RLY_CRCV_HEAT_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_KGEH_WERT | unsigned long | Timeout Kurbelgehaeuseentlueftungsheizung 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-klann"></a>
### STEUERN_KLANN

0x31E4 STEUERN_KLANN Ansteuern Klann-Adaptionswerte (Anforderung aus CP10798) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_LOC_WERT | long | Drehzahl NKW_LOC   Einheit: Upm   Min: -32768 Max: 32767 |
| RK_LOC_WERT | real | Relative Kraftstoffmasse RK_LOC   Min: 0 Max: 31.9995 |
| TMOT_LOC_WERT | real | Kuehlwassertemperatur TMOT_LOC   Einheit: C   Min: -327.68 Max: 327.67 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-korel"></a>
### STEUERN_KOREL

0x30C707 STEUERN_KOREL Klimakompressor-Relais ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_KOREL_WERT | unsigned long | Sollwert Klimakompressor-Relais LV_ACT_ACCOUT_RLY_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_KOREL_WERT | unsigned long | Timeout Klimakompressor-Relais 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-krann"></a>
### STEUERN_KRANN

0x31E3 STEUERN_KRANN Ansteuern Krann-Adaptionswerte Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NKW_WERT | long | Drehzahl NKW_SOLL   Einheit: Upm   Min: -32768 Max: 32767 |
| RF_WERT | real | Relative Luftfuellung RF   Einheit: %   Min: -327.68 Max: 327.67 |
| TANS_WERT | real | Ansauglufttemperatur TANS   Einheit: C   Min: -3276.8 Max: 3276.7 |
| TMOT_WERT | real | Kuehlwassertemperatur TMOT   Einheit: C   Min: -327.68 Max: 327.67 |
| BA_IST_WERT | string | Istbetriebsart BA_IST   Min: 0 Max: 8 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-kva"></a>
### STEUERN_KVA

0x3BC1 STEUERN_KVA KraftstoffVerbrauchsAnzeige - Korrekturfaktor schreiben Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KVA_WERT | real | correction factor for consumption (A2L-Name: fac_fco_kwp) FAC_FCO_KWP   Min: -0.128 Max: 0.127 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lds1"></a>
### STEUERN_LDS1

0x30B607 STEUERN_LDS1 Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LDS1_WERT | real | Tastverhaeltniss Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) WGPWM_EXT_ADJ[1]   Einheit: %   Min: 0 Max: 99.9984741210938 |
| SW_TO_LDS1_WERT | unsigned long | Timeout Ladedrucksteller 1 (z.B. Waste Gate oder VTG variable Turbinengeometrie) 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lds2"></a>
### STEUERN_LDS2

0x30B707 STEUERN_LDS2 Ladedrucksteller 2 (z.B. Waste Gate oder VTG variable Turbinengeometrie) ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LDS2_WERT | real | Tastverhaeltniss Ladedrucksteller 2 (z.B. Waste Gate oder VTG variable Turbinengeometrie) WGPWM_EXT_ADJ[2]   Einheit: %   Min: 0 Max: 99.9984741210938 |
| SW_TO_LDS2_WERT | unsigned long | Timeout Ladedrucksteller 2 (z.B. Waste Gate oder VTG variable Turbinengeometrie) 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ll-abgleich"></a>
### STEUERN_LL_ABGLEICH

0x2E5FF007 STEUERN_LL_ABGLEICH Abgleichwert LL (Leerlauf) vorgeben Aktivierung: Klemme 15 = EIN UND Leerlaufabgleich ueber Testervorgabe = EIN Activation: LV_IGK = 1 UND LV_KWP_ENA = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFS_ACC_DRI_IN_WERT | long | Abgleichswert LL mit Klima und Fahrbedingung N_KWP_OFS_ACC_DRI_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_DRI_IN_WERT | long | Abgleichswert LL mit Fahrstufe N_KWP_OFS_DRI_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_IN_WERT | long | Abgleichswert LL N_KWP_OFS_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_ACC_IN_WERT | long | Abgleichswert LL mit Klimaanlage N_KWP_OFS_ACC_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_VB_IN_WERT | long | Abgleichswert LL mit niedriger Batteriespannung N_KWP_OFS_VB_KWP   Einheit: rpm   Min: -256 Max: 254 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFS_ACC_DRI_OUT_WERT | long | Abgleichswert LL mit Klima und Fahrbedingung N_KWP_OFS_ACC_DRI_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_ACC_DRI_OUT_EINH | string | rpm |
| STAT_OFS_DRI_OUT_WERT | long | Abgleichswert LL mit Fahrstufe N_KWP_OFS_DRI_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_DRI_OUT_EINH | string | rpm |
| STAT_OFS_OUT_WERT | long | Abgleichswert LL N_KWP_OFS_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_OUT_EINH | string | rpm |
| STAT_OFS_ACC_OUT_WERT | long | Abgleichswert LL mit Klimaanlage N_KWP_OFS_ACC_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_ACC_OUT_EINH | string | rpm |
| STAT_OFS_VB_OUT_WERT | long | Abgleichswert LL mit niedriger Batteriespannung N_KWP_OFS_VB_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_VB_OUT_EINH | string | rpm |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-llabg-prog"></a>
### STEUERN_LLABG_PROG

0x2E5FF008 STEUERN_LLABG_PROG Abgleichwert LL (Leerlauf) programmieren Aktivierung: Klemme 15 = EIN UND Leerlaufabgleich ueber Testervorgabe = EIN Activation: LV_IGK = 1 UND LV_KWP_ENA = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFS_ACC_DRI_IN_WERT | long | Abgleichswert LL mit Klima und Fahrbedingung N_KWP_OFS_ACC_DRI_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_DRI_IN_WERT | long | Abgleichswert LL mit Fahrstufe N_KWP_OFS_DRI_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_IN_WERT | long | Abgleichswert LL N_KWP_OFS_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_ACC_IN_WERT | long | Abgleichswert LL mit Klimaanlage N_KWP_OFS_ACC_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_VB_IN_WERT | long | Abgleichswert LL mit niedriger Batteriespannung N_KWP_OFS_VB_KWP   Einheit: rpm   Min: -256 Max: 254 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OFS_ACC_DRI_OUT_WERT | long | Abgleichswert LL mit Klima und Fahrbedingung N_KWP_OFS_ACC_DRI_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_ACC_DRI_OUT_EINH | string | rpm |
| STAT_OFS_DRI_OUT_WERT | long | Abgleichswert LL mit Fahrstufe N_KWP_OFS_DRI_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_DRI_OUT_EINH | string | rpm |
| STAT_OFS_OUT_WERT | long | Abgleichswert LL N_KWP_OFS_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_OUT_EINH | string | rpm |
| STAT_OFS_ACC_OUT_WERT | long | Abgleichswert LL mit Klimaanlage N_KWP_OFS_ACC_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_ACC_OUT_EINH | string | rpm |
| STAT_OFS_VB_OUT_WERT | long | Abgleichswert LL mit niedriger Batteriespannung N_KWP_OFS_VB_KWP   Einheit: rpm   Min: -256 Max: 254 |
| STAT_OFS_VB_OUT_EINH | string | rpm |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh1"></a>
### STEUERN_LSH1

0x30D007 STEUERN_LSH1 Lambdasondenheizung vor Kat Bank1 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH1_WERT | real | Tastverhaeltniss Lambdasondenheizung vor Kat Bank1 LSHPWM_UP_EXT_ADJ[1]   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_LSH1_WERT | unsigned long | Timeout Lambdasondenheizung vor Kat Bank1 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh2"></a>
### STEUERN_LSH2

0x30D107 STEUERN_LSH2 Lambdasondenheizung hinter Kat Bank1 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH2_WERT | real | Tastverhaeltniss Lambdasondenheizung hinter Kat Bank1 LSHPWM_DOWN_EXT_ADJ[1]   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_LSH2_WERT | unsigned long | Timeout Lambdasondenheizung hinter Kat Bank1 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh3"></a>
### STEUERN_LSH3

0x30D207 STEUERN_LSH3 Lambdasondenheizung vor Kat Bank2 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH3_WERT | real | Tastverhaeltniss Lambdasondenheizung vor Kat Bank2 LSHPWM_UP_EXT_ADJ[2]   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_LSH3_WERT | unsigned long | Timeout Lambdasondenheizung vor Kat Bank2 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-lsh4"></a>
### STEUERN_LSH4

0x30D307 STEUERN_LSH4 Lambdasondenheizung hinter Kat Bank2 ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_LSH4_WERT | real | Tastverhaeltniss Lambdasondenheizung hinter Kat Bank2 LSHPWM_DOWN_EXT_ADJ[2]   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_LSH4_WERT | unsigned long | Timeout Lambdasondenheizung hinter Kat Bank2 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mil"></a>
### STEUERN_MIL

0x30D407 STEUERN_MIL MIL (Malfunction Indicator Lamp) ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_MIL_WERT | unsigned long | Sollwert MIL (Malfunction Indicator Lamp) LV_ACT_MIL_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_MIL_WERT | unsigned long | Timeout MIL (Malfunction Indicator Lamp) 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-mls"></a>
### STEUERN_MLS

0x30B207 STEUERN_MLS Motorlagersteuerung ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_MLS_WERT | unsigned long | Tastverhaeltniss Motorlagersteuerung LV_SWI_AEB_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_MLS_WERT | unsigned long | Timeout Motorlagersteuerung 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-msv"></a>
### STEUERN_MSV

0x30BD07 STEUERN_MSV Mengensteuerventil ansteuern Aktivierung: 50000 hPa &lt; Raildruck &lt; 220000 hPa UND Leerlauf Activation: C_FUP_MIN_KWP &lt; FUP &lt; C_FUP_MAX_KWP UND LV_IS = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_MSV_WERT | real | Tastverhaeltniss Mengensteuerventil FUP_SP_EXT_ADJ   Einheit: hPa   Min: 0 Max: 347776 |
| SW_TO_MSV_WERT | unsigned long | Timeout Mengensteuerventil 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-odr"></a>
### STEUERN_ODR

0x30AB07 STEUERN_ODR Oel Druck Regelung (Geregeltes Oeldrucksystem) ansteuern Aktivierung: 2 bar &lt; Oeldruck &lt; 9 bar UND 500 1/min &lt; Drehzahl &lt; 2000 1/min Activation: C_POIL_MIN_KWP &lt; POIL &lt; C_POIL_MAX_KWP UND C_N_MIN_KWP_POIL &lt; N &lt; C_N_MAX_KWP_POIL

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_P_OELSOL_TST_WERT | unsigned long | Oeldruck Sollwert durch Testereingriff POIL_SP_EXT_ADJ   Einheit: hPa   Min: 0 Max: 8160 |
| SW_TO_ODR_WERT | unsigned long | Timeout Oel Druck Regelung (Geregeltes Oeldrucksystem) 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-odv"></a>
### STEUERN_ODV

0x30AC07 STEUERN_ODV Oeldruckventil (Geregeltes Oeldrucksystem) ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_ODV_WERT | real | Tastverhaeltniss Oeldruckventil (Geregeltes Oeldrucksystem) POIL_PWM_EXT_ADJ   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_ODV_WERT | unsigned long | Timeout Oeldruckventil (Geregeltes Oeldrucksystem) 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-pm-restore"></a>
### STEUERN_PM_RESTORE

0x2E5F8B STEUERN_PM_RESTORE Schreiben PM-Restore Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PMRESTORE_0_WERT | unsigned long | PM-Restore Byte 0 PMRESTORE[0]   Min: 0 Max: 255 |
| STAT_PMRESTORE_1_WERT | unsigned long | PM-Restore Byte 1 PMRESTORE[1]   Min: 0 Max: 3 |
| STAT_PMRESTORE_2_WERT | unsigned long | PM-Restore Byte 2 PMRESTORE[2]   Min: 0 Max: 255 |
| STAT_PMRESTORE_3_WERT | unsigned long | PM-Restore Byte 3 PMRESTORE[3]   Min: 0 Max: 3 |
| STAT_PMRESTORE_4_WERT | unsigned long | PM-Restore Byte 4 PMRESTORE[4]   Min: 0 Max: 255 |
| STAT_PMRESTORE_5_WERT | unsigned long | PM-Restore Byte 5 PMRESTORE[5]   Min: 0 Max: 3 |
| STAT_PMRESTORE_6_WERT | unsigned long | PM-Restore Byte 6 PMRESTORE[6]   Min: 0 Max: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-1"></a>
### STEUERN_PROGRAMM_IMA_ZYL_1

0x2E5F91 STEUERN_PROGRAMM_IMA_ZYL_1 Abgleichwert Injektor 01 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_1_WERT | real | IMA Abgleichwert Injektor 01 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[0]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_1_WERT | real | IMA Abgleichwert Injektor 01 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[0]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-2"></a>
### STEUERN_PROGRAMM_IMA_ZYL_2

0x2E5F95 STEUERN_PROGRAMM_IMA_ZYL_2 Abgleichwert Injektor 05 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_2_WERT | real | IMA Abgleichwert Injektor 05 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[4]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_2_WERT | real | IMA Abgleichwert Injektor 05 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[4]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-3"></a>
### STEUERN_PROGRAMM_IMA_ZYL_3

0x2E5F93 STEUERN_PROGRAMM_IMA_ZYL_3 Abgleichwert Injektor 03 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_3_WERT | real | IMA Abgleichwert Injektor 03 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[2]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_3_WERT | real | IMA Abgleichwert Injektor 03 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[2]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-4"></a>
### STEUERN_PROGRAMM_IMA_ZYL_4

0x2E5F96 STEUERN_PROGRAMM_IMA_ZYL_4 Abgleichwert Injektor 06 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_4_WERT | real | IMA Abgleichwert Injektor 06 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[5]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_4_WERT | real | IMA Abgleichwert Injektor 06 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[5]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-5"></a>
### STEUERN_PROGRAMM_IMA_ZYL_5

0x2E5F92 STEUERN_PROGRAMM_IMA_ZYL_5 Abgleichwert Injektor 02 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_5_WERT | real | IMA Abgleichwert Injektor 02 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[1]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_5_WERT | real | IMA Abgleichwert Injektor 02 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[1]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-ima-zyl-6"></a>
### STEUERN_PROGRAMM_IMA_ZYL_6

0x2E5F94 STEUERN_PROGRAMM_IMA_ZYL_6 Abgleichwert Injektor 04 programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_6_WERT | real | IMA Abgleichwert Injektor 04 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[3]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_6_WERT | real | IMA Abgleichwert Injektor 04 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[3]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-programm-imaalle"></a>
### STEUERN_PROGRAMM_IMAALLE

0x2E5F90 STEUERN_PROGRAMM_IMAALLE Abgleichwerte Injektoren programmieren Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_ENERGIEABGLEICH_ZYL_1_WERT | real | IMA Abgleichwert Injektor 01 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[0]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_1_WERT | real | IMA Abgleichwert Injektor 01 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[0]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_5_WERT | real | IMA Abgleichwert Injektor 02 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[1]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_5_WERT | real | IMA Abgleichwert Injektor 02 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[1]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_3_WERT | real | IMA Abgleichwert Injektor 03 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[2]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_3_WERT | real | IMA Abgleichwert Injektor 03 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[2]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_6_WERT | real | IMA Abgleichwert Injektor 04 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[3]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_6_WERT | real | IMA Abgleichwert Injektor 04 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[3]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_2_WERT | real | IMA Abgleichwert Injektor 05 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[4]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_2_WERT | real | IMA Abgleichwert Injektor 05 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[4]   Einheit: mg/stk   Min: 0 Max: 1389 |
| SW_ENERGIEABGLEICH_ZYL_4_WERT | real | IMA Abgleichwert Injektor 06 Flow1 (Energie) EGY_SP_IV_EXT_ADJ[5]   Einheit: mJ   Min: 0 Max: 255 |
| SW_DURCHFLUSSABGLEICH_ZYL_4_WERT | real | IMA Abgleichwert Injektor 06 Flow2 (Durchfluss) MFF_ABSV_IV_EXT_ADJ[5]   Einheit: mg/stk   Min: 0 Max: 1389 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ruhestrommessung"></a>
### STEUERN_RUHESTROMMESSUNG

0x312B STEUERN_RUHESTROMMESSUNG Ansteuern Ruhestrompruefung mit IBS Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_MAX_WERT | real | Max. Ruhestromschwelle (Eco_max_i) Eco_max_i   Einheit: A   Min: 0 Max: 0.3187 |
| MSB_WERT | real | Ecos Messtartbedingung (Eco_msb) Eco_msb   Einheit: s   Min: 0 Max: 12.75 |
| MZ_WERT | real | Dauer Mittelwertmessung (Eco_mz) Eco_mz   Einheit: s   Min: 0 Max: 12.75 |
| TO_WERT | unsigned long | Ecos Messung Timeout (Eco_timo) Eco_timo   Einheit: s   Min: 0 Max: 255 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-sr"></a>
### STEUERN_SR

0x30C407 STEUERN_SR Startrelais ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Drehzahl = 0 1/min UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_ES = 1 UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_SR_WERT | unsigned long | Sollwert Startrelais LV_ACT_RLY_ST_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_SR_WERT | unsigned long | Timeout Startrelais 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

0x30CF07 STEUERN_TEV Tankentlueftungsventil ansteuern Aktivierung: Batteriespannung &gt; 10 V UND Klemme 15 = EIN Activation: VB &gt; C_VB_MIN_KWP UND LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_TEV_WERT | real | TastverhaeltnissTankentlueftungsventil CPPWM_EXT_ADJ   Einheit: %   Min: 0 Max: 99.609375 |
| SW_TO_TEV_WERT | unsigned long | Timeout Tankentlueftungsventil 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ugen"></a>
### STEUERN_UGEN

0x303207 STEUERN_UGEN Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) ansteuern Aktivierung: Leerlauf Activation: LV_IS = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_PHY_UGEN_WERT | real | Spannung Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) V_ALTER_SP_EXT_ADJ   Einheit: V   Min: 0 Max: 6553.5 |
| SW_TO_UGEN_WERT | unsigned long | Timeout Generator Sollspannung BSD (Bit Serielle Datenschnittstelle) 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-uvsg"></a>
### STEUERN_UVSG

0x301C07 STEUERN_UVSG Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) ansteuern Aktivierung: Geschwindigkeit &lt; 5 km/h UND Drehzahl = 0 1/min Activation: VS &lt; C_VS_MAX_KWP UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_TV_UVSG_WERT | unsigned long | Sollwert Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) LV_RLY_MAIN_EXT_ADJ   Min: 0 Max: 1 |
| SW_TO_UVSG_WERT | unsigned long | Timeout Kl.87 Spannung / Versorgung DME (Digitale Motor Elektronik) 1BYTE in 0 bis 510s   Einheit: s   Min: 0 Max: 510 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-dmtl"></a>
### STOP_SYSTEMCHECK_DMTL

0x32DA STOP_SYSTEMCHECK_DMTL Diagnosefunktion DMTL beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-evausbl"></a>
### STOP_SYSTEMCHECK_EVAUSBL

0x3125 STOP_SYSTEMCHECK_EVAUSBL Ansteuern Diagnosefunktion Einspritzventilausblendung beenden Aktivierung: Klemme 15 = EIN UND Motorstatus = (Leerlauf ODER Teillast) UND Drehzahl &lt; 3000 1/min Activation: LV_IGK = 1 UND STATE_ENG = (IS ODER PL) UND N &lt; C_N_MAX_KWP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-gen"></a>
### STOP_SYSTEMCHECK_GEN

0x322A STOP_SYSTEMCHECK_GEN Diagnosefunktion Generatortest beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-glf"></a>
### STOP_SYSTEMCHECK_GLF

0x32D5 STOP_SYSTEMCHECK_GLF Ende Gesteuerte Luftfuehrung Systemcheck Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-igr-aus"></a>
### STOP_SYSTEMCHECK_IGR_AUS

0x32F7 STOP_SYSTEMCHECK_IGR_AUS Ende Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-l-regelung-aus"></a>
### STOP_SYSTEMCHECK_L_REGELUNG_AUS

0x32D9 STOP_SYSTEMCHECK_L_REGELUNG_AUS Ende Lambdaregelung ausschalten Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-l-sonde"></a>
### STOP_SYSTEMCHECK_L_SONDE

0x32DF STOP_SYSTEMCHECK_L_SONDE Diagnosefunktion vertauschte Lambdasonden beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-llerh"></a>
### STOP_SYSTEMCHECK_LLERH

0x3226 STOP_SYSTEMCHECK_LLERH Diagnosefunktion Leerlauf-Erhoehung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-odr"></a>
### STOP_SYSTEMCHECK_ODR

0x322C STOP_SYSTEMCHECK_ODR Diagnosefunktion Oeldruckregelung beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-tev-func"></a>
### STOP_SYSTEMCHECK_TEV_FUNC

0x3222 STOP_SYSTEMCHECK_TEV_FUNC Diagnosefunktion Tankentlueftungsventil beenden Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-messwertblock-lesen"></a>
### MESSWERTBLOCK_LESEN

0x2CF0 MESSWERTBLOCK_LESEN DDLI Messwerte auf Basis Übergabestring aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STRING_IN | string | Werte aus DDLI Liste Format 0x58XX,0x42YY,0x43ZZ,... |
| TRENNZEICHEN | string | Werte aus DDLI Liste Format 0x58XX,0x42YY,0x43ZZ,... |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZAHL_WERTE | int | Anzahl Messwerte 0 bis n dezimal ansteigend |
| STAT_MESSWERT0_WERT | real | real Wert |
| STAT_MESSWERT0_STRING | string | String mit 9 signifikanten Stellen |
| STAT_MESSWERT0_TEXT | string | Text der Variablen aus INFO |
| STAT_MESSWERT0_EINH | string | Einheit der Variablen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an  SG Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG Block löschen |
| _TEL_AUFTRAG | binary | Hex-Auftrag an  SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an  SG Block lesen |
| _TEL_ANTWORT | binary | Hex-Antwort von SG Block lesen |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

0x2CF0 4807 & 4808 STATUS_MOTORDREHZAHL Auslesen des Soll- und Istwertes der Motordrehzahl Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOTORDREHZAHL_WERT | real | Istwert Motordrehzahl N |
| STAT_MOTORDREHZAHL_EINH | string | rpm |
| STAT_SOLL_MOTORDREHZAHL_WERT | real | Sollwert Motordrehzahl N_SP_IS |
| STAT_SOLL_MOTORDREHZAHL_EINH | string | rpm |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an SG alten Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG alten Block löschen |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-int"></a>
### STATUS_INT

0x2CF0 5A81 STATUS_INT Auslesen des Integrator Bank 1 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INT_WERT | real | Integrator Bank 1 FAC_LAM_LIM[1] |
| STAT_INT_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-int-2"></a>
### STATUS_INT_2

0x2CF0 5A82 STATUS_INT_2 Auslesen des Integrator Bank 2 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INT_2_WERT | real | Integrator Bank 2 FAC_LAM_LIM[2] |
| STAT_INT_2_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-add"></a>
### STATUS_ADD

0x2CF0 5A83 STATUS_ADD Auslesen der Adaption Offset Lambda Bank 1 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADD_WERT | real | Adaption Offset Lambda Bank 1 MFF_ADD_LAM_AD_OUT[1] |
| STAT_ADD_EINH | string | mg/stk |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-add-2"></a>
### STATUS_ADD_2

0x2CF0 5A84 STATUS_ADD_2 Auslesen der Adaption Offset Lambda Bank 2 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ADD_2_WERT | real | Adaption Offset Lambda Bank 2 MFF_ADD_LAM_AD_OUT[2] |
| STAT_ADD_2_EINH | string | mg/stk |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mul"></a>
### STATUS_MUL

0x2CF0 5A85 STATUS_MUL Auslesen der Adaption Multiplikation Lambda Bank 1 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MUL_WERT | real | Adaption Multiplikation Lambda Bank 1 FAC_LAM_AD_CUS[1] |
| STAT_MUL_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-mul-2"></a>
### STATUS_MUL_2

0x2CF0 5A86 STATUS_MUL_2 Auslesen der Adaption Multiplikation Lambda Bank 2 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MUL_2_WERT | real | Adaption Multiplikation Lambda Bank 2 FAC_LAM_AD_CUS[2] |
| STAT_MUL_2_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-betriebsstundenzaehler"></a>
### STATUS_BETRIEBSSTUNDENZAEHLER

0x2CF0 5AB4 STATUS_BETRIEBSSTUNDENZAEHLER Betriebsstundenzaehler auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BSZ | unsigned long | Auswertung Betriebsstundenzaehler 4BYTE_TRT_FLAG |
| STAT_TRT_WERT | real | Betriebsstundenzaehler TRT |
| STAT_TRT_EINH | string | h |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-geberrad-adaption"></a>
### STATUS_GEBERRAD_ADAPTION

0x2CF0 STATUS_GEBERRAD_ADAPTION Adaptionswerte für das Geberrad aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZAHL_WERTE | int | Anzahl Messwerte 0 bis 1  |
| STAT_GEBERRAD_ADAPTION_VSA_WERT | real | Wert von vsa_adp PSN_AD_CAM_EX_1   Einheit: °CRK   Min: -48 Max: 47.625 |
| STAT_GEBERRAD_ADAPTION_VSA_TEXT | string | Text von PSN_AD_CAM_EX_1  |
| STAT_GEBERRAD_ADAPTION_VSE_WERT | real | Wert von vse_adp PSN_AD_CAM_IN_1   Einheit: °CRK   Min: -48 Max: 47.625 |
| STAT_GEBERRAD_ADAPTION_VSE_TEXT | string | Text von PSN_AD_CAM_IN_1  |
| STAT_GEBERRAD_ADAPTION_EINH | string | °CRK |
| STAT_SEG_AD_WERT | int | Kurbelwelle Segmentadaption beendet 0=nein / 1=ja LV_SEG_AD_AVL_ER   Min: 0 Max: 1 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an SG alten Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG alten Block löschen |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-status-messwertblock-adc"></a>
### STATUS_MESSWERTBLOCK_ADC

0x2CF0 STATUS_MESSWERTBLOCK_ADC ADC-Werte aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MESSWERT0_WERT | real | Messwert (Word) |
| STAT_MESSWERT0_TEXT | string | Messwert |
| STAT_MESSWERT0_EINH | string | Messwert |
| STAT_MESSWERT1_WERT | real | Messwert (Word) |
| STAT_MESSWERT1_TEXT | string | Messwert |
| STAT_MESSWERT1_EINH | string | Messwert |
| STAT_MESSWERT2_WERT | real | Messwert (Word) |
| STAT_MESSWERT2_TEXT | string | Messwert |
| STAT_MESSWERT2_EINH | string | Messwert |
| STAT_MESSWERT3_WERT | real | Messwert (Word) |
| STAT_MESSWERT3_TEXT | string | Messwert |
| STAT_MESSWERT3_EINH | string | Messwert |
| STAT_MESSWERT4_WERT | real | Messwert (Word) |
| STAT_MESSWERT4_TEXT | string | Messwert |
| STAT_MESSWERT4_EINH | string | Messwert |
| STAT_MESSWERT5_WERT | real | Messwert (Word) |
| STAT_MESSWERT5_TEXT | string | Messwert |
| STAT_MESSWERT5_EINH | string | Messwert |
| STAT_MESSWERT6_WERT | real | Messwert (Word) |
| STAT_MESSWERT6_TEXT | string | Messwert |
| STAT_MESSWERT6_EINH | string | Messwert |
| STAT_MESSWERT7_WERT | real | Messwert (Word) |
| STAT_MESSWERT7_TEXT | string | Messwert |
| STAT_MESSWERT7_EINH | string | Messwert |
| STAT_MESSWERT8_WERT | real | Messwert (Word) |
| STAT_MESSWERT8_TEXT | string | Messwert |
| STAT_MESSWERT8_EINH | string | Messwert |
| STAT_MESSWERT9_WERT | real | Messwert (Word) |
| STAT_MESSWERT9_TEXT | string | Messwert |
| STAT_MESSWERT9_EINH | string | Messwert |
| STAT_MESSWERTA_WERT | real | Messwert (Word) |
| STAT_MESSWERTA_TEXT | string | Messwert |
| STAT_MESSWERTA_EINH | string | Messwert |
| STAT_MESSWERTB_WERT | real | Messwert (Word) |
| STAT_MESSWERTB_TEXT | string | Messwert |
| STAT_MESSWERTB_EINH | string | Messwert |
| STAT_MESSWERTC_WERT | real | Messwert (Word) |
| STAT_MESSWERTC_TEXT | string | Messwert |
| STAT_MESSWERTC_EINH | string | Messwert |
| STAT_MESSWERTD_WERT | real | Messwert (Word) |
| STAT_MESSWERTD_TEXT | string | Messwert |
| STAT_MESSWERTD_EINH | string | Messwert |
| STAT_MESSWERTE_WERT | real | Messwert (Word) |
| STAT_MESSWERTE_TEXT | string | Messwert |
| STAT_MESSWERTE_EINH | string | Messwert |
| STAT_MESSWERTF_WERT | real | Messwert (Word) |
| STAT_MESSWERTF_TEXT | string | Messwert |
| STAT_MESSWERTF_EINH | string | Messwert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an SG alten Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG alten Block löschen |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-messwerte-vanos"></a>
### STATUS_MESSWERTE_VANOS

0x2CF0 STATUS_MESSWERTE_VANOS Messwerte CAM_IN und CAM_EX nach Wunsch VS-42 aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ANZAHL_WERTE | int | Anzahl Messwerte 0 bis 1  |
| STAT_EINLASS_WERT | real | Istwert Einlassspreizung CAM_IN[1]   Einheit: °CRK   Min: 60 Max: 155.625 |
| STAT_EINLASS_TEXT | string | Text von CAM_IN[1]  |
| STAT_EINLASS_EINH | string | °CRK |
| STAT_EINLASS_SOLL_WERT | real | Sollwert Einlassspreizung CAM_SP_IVVT_IN   Einheit: °CRK   Min: 60 Max: 155.625 |
| STAT_EINLASS_SOLL_TEXT | string | Text von CAM_SP_IVVT_IN  |
| STAT_EINLASS_SOLL_EINH | string | °CRK |
| STAT_AUSLASS_WERT | real | Istwert Auslassspreizung CAM_EX[1]   Einheit: °CRK   Min: -40 Max: -135.625 |
| STAT_AUSLASS_TEXT | string | Text von CAM_EX[1]  |
| STAT_AUSLASS_EINH | string | °CRK |
| STAT_AUSLASS_SOLL_WERT | real | Sollwert Auslassspreizung -135,6 bis -40 CAM_SP_IVVT_EX   Einheit: °CRK   Min: -40 Max: -135.625 |
| STAT_AUSLASS_SOLL_TEXT | string | Text von CAM_SP_IVVT_EX  |
| STAT_AUSLASS_SOLL_EINH | string | °CRK |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an SG alten Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG alten Block löschen |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-fasta-common"></a>
### _STATUS_FASTA_COMMON

0x2CF0 _STATUS_FASTA_COMMON DDLI Messwerte für FASTA auf Basis Übergabestring aus DME auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIST_ACT_MIL_WERT | real | Fahrstrecke mit MIL an DIST_ACT_MIL |
| STAT_DIST_ACT_MIL_EINH | string | km |
| STAT_OZ_OELKM_WERT | real | km seit letztem Service OZ_OELKM |
| STAT_OZ_OELKM_EINH | string | km |
| STAT_OZ_KVBSM_UL_WERT | real | Kraftstoff-Verbrauch seit letztem Service OZ_KVBSM_UL |
| STAT_OZ_KVBSM_UL_EINH | string | l |
| STAT_T_ES_WERT | real | Motorabstellzeit T_ES |
| STAT_T_ES_EINH | string | min |
| STAT_STATE_ETC_LIH_WERT | real | Status Drosselklappe Notlauf STATE_ETC_LIH |
| STAT_STATE_ETC_LIH_EINH | string |  |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG_L | binary | Hex-Auftrag an SG alten Block löschen |
| _TEL_ANTWORT_L | binary | Hex-Antwort von SG alten Block löschen |
| _TEL_AUFTRAG_S | binary | Hex-Auftrag an SG Block schreiben |
| _TEL_ANTWORT_S | binary | Hex-Antwort von SG Block schreiben |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-obd-mode-01"></a>
### _STATUS_OBD_MODE_01

0x0101 _STATUS_OBD_MODE_01 Auslesen der Motor-Diagnosedaten nach Mode 01 PID 01 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MIL_TEXT | string | Ansteuerstatus der MIL (An=1, Aus=0) |
| STAT_MIL_WERT | int | Ansteuerstatus der MIL (An=1, Aus=0) |
| STAT_ANZAHL_PCODE_WERT | int | Anzahl gespeicherter P-Codes |
| STAT_MONITOR_CC_TEXT | string | Überwachung Comprehensive Components (übrige Komponenten),  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1  |
| STAT_MONITOR_CC_WERT | int | Überwachung Comprehensive Components (übrige Komponenten),  Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 STATE_READY_OBD_1[2] |
| STAT_READINESS_CC_TEXT | string | Überwachung Comprehensive Components (übrige Komponenten), Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1  |
| STAT_READINESS_CC_WERT | int | Überwachung Comprehensive Components (übrige Komponenten), Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_1[6] |
| STAT_MONITOR_KSS_TEXT | string | Überwachung KraftStoffSystem, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1  |
| STAT_MONITOR_KSS_WERT | int | Überwachung KraftStoffSystem, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 STATE_READY_OBD_1[1] |
| STAT_READINESS_KSS_TEXT | string | Überwachung KraftStoffSystem, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1  |
| STAT_READINESS_KSS_WERT | int | Überwachung KraftStoffSystem, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_1[5] |
| STAT_MONITOR_VA_TEXT | string | Überwachung VerbrennungsAussetzer, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1  |
| STAT_MONITOR_VA_WERT | int | Überwachung VerbrennungsAussetzer, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 STATE_READY_OBD_1[0] |
| STAT_READINESS_VA_TEXT | string | Überwachung VerbrennungsAussetzer, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1  |
| STAT_READINESS_VA_WERT | int | Überwachung VerbrennungsAussetzer, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_1[4] |
| STAT_MONITOR_ARS_TEXT | string | Überwachung AbgasRückführungsSystem, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1  |
| STAT_MONITOR_ARS_WERT | int | Überwachung AbgasRückführungsSystem, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[7] |
| STAT_READINESS_ARS_TEXT | string | Überwachung AbgasRückführungsSystem, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1  |
| STAT_READINESS_ARS_WERT | int | Überwachung AbgasRückführungsSystem, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[7] |
| STAT_MONITOR_LSH_TEXT | string | Überwachung LambdaSondenHeizung, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1  |
| STAT_MONITOR_LSH_WERT | int | Überwachung LambdaSondenHeizung, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[6] |
| STAT_READINESS_LSH_TEXT | string | Überwachung LambdaSondenHeizung, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1  |
| STAT_READINESS_LSH_WERT | int | Überwachung LambdaSondenHeizung, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[6] |
| STAT_MONITOR_LS_TEXT | string | Überwachung LambdaSonde, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1  |
| STAT_MONITOR_LS_WERT | int | Überwachung LambdaSonde, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[5] |
| STAT_READINESS_LS_TEXT | string | Überwachung LambdaSonde, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1  |
| STAT_READINESS_LS_WERT | int | Überwachung LambdaSonde, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[5] |
| STAT_MONITOR_KLIMA_TEXT | string | Überwachung Klimaanlage, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1  |
| STAT_MONITOR_KLIMA_WERT | int | Überwachung Klimaanlage, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[4] |
| STAT_READINESS_KLIMA_TEXT | string | Überwachung Klimaanlage, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1  |
| STAT_READINESS_KLIMA_WERT | int | Überwachung Klimaanlage, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[4] |
| STAT_MONITOR_SLS_TEXT | string | Überwachung SekundärLuftSystem, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1  |
| STAT_MONITOR_SLS_WERT | int | Überwachung SekundärLuftSystem, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[3] |
| STAT_READINESS_SLS_TEXT | string | Überwachung SekundärLuftSystem, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1  |
| STAT_READINESS_SLS_WERT | int | Überwachung SekundärLuftSystem, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[3] |
| STAT_MONITOR_TEV_TEXT | string | Überwachung Tankentlüftungssystem, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1  |
| STAT_MONITOR_TEV_WERT | int | Überwachung Tankentlüftungssystem, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[2] |
| STAT_READINESS_TEV_TEXT | string | Überwachung Tankentlüftungssystem, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1  |
| STAT_READINESS_TEV_WERT | int | Überwachung Tankentlüftungssystem, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[2] |
| STAT_MONITOR_KH_TEXT | string | Überwachung KatalysatorHeizung, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1  |
| STAT_MONITOR_KH_WERT | int | Überwachung KatalysatorHeizung, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[1] |
| STAT_READINESS_KH_TEXT | string | Überwachung KatalysatorHeizung, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1  |
| STAT_READINESS_KH_WERT | int | Überwachung KatalysatorHeizung, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[1] |
| STAT_MONITOR_KAT_TEXT | string | Überwachung Katalysator, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1  |
| STAT_MONITOR_KAT_WERT | int | Überwachung Katalysator, Test wird durch dieses Modul nicht unterstuetzt = 0  Test wird durch dieses Modul unterstuetzt = 1 C_STATE_READY_OBD_2[0] |
| STAT_READINESS_KAT_TEXT | string | Überwachung Katalysator, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1  |
| STAT_READINESS_KAT_WERT | int | Überwachung Katalysator, Test abgeschlossen oder nicht anwendbar = 0  Test nicht abgeschlossen = 1 STATE_READY_OBD_2[0] |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-obd-mode-03"></a>
### _STATUS_OBD_MODE_03

0x03 _STATUS_OBD_MODE_03 Auslesen der P-Codes nach Mode 03 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PCODE_1_HEX | string | 1. P-Code als Hex-Wert |
| STAT_PCODE_1_TEXT | string | 1. P-Code als Text |
| STAT_PCODE_M3_ANZAHL | int | Anzahl gespeicherter P-Codes |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-obd-mode-07"></a>
### _STATUS_OBD_MODE_07

0x07 _STATUS_OBD_MODE_07 Auslesen der P-Codes nach Mode 07 Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PCODE_1_HEX | string | 1. P-Code als Hex-Wert |
| STAT_PCODE_1_TEXT | string | 1. P-Code als Text |
| STAT_PCODE_M7_ANZAHL | int | Anzahl gespeicherter P-Codes |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-obd-mode-09"></a>
### _STATUS_OBD_MODE_09

0x0908 _STATUS_OBD_MODE_09 Rate Based Monitoring Mode 9 mit PID 08 auslesen (Ausgabe der Werte wie im Scantool Mode 9) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OBDCOND | unsigned long | OBD Monitoring Conditions Encountered Counts (general denominator) CTR_CDN_OBD_RBM   Min: 0 Max: 65535 |
| STAT_IGNCNTR | unsigned long | Ignition Counter CTR_IGK_CYC_RBM   Min: 0 Max: 65535 |
| STAT_CATCOMP1 | unsigned long | Catalyst Monitor Completion Counts Bank 1 (numerator) CTR_COMP_RBM_CAT_DIAG_1   Min: 0 Max: 65535 |
| STAT_CATCOND1 | unsigned long | Catalyst Monitor Conditions Encountered Counts Bank 1 (denominator) CTR_CDN_RBM_CAT_DIAG_1   Min: 0 Max: 65535 |
| STAT_CATCOMP2 | unsigned long | Catalyst Monitor Completion Counts Bank 2 (numerator) CTR_COMP_RBM_CAT_DIAG_2   Min: 0 Max: 65535 |
| STAT_CATCOND2 | unsigned long | Catalyst Monitor Conditions Encountered Counts Bank 2 (denominator) CTR_CDN_RBM_CAT_DIAG_2   Min: 0 Max: 65535 |
| STAT_O2SCOMP1 | unsigned long | O2 Sensor Monitor Completion Counts Bank 1 (numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_O2SCOND1 | unsigned long | O2 Sensor Monitor Conditions Encountered Counts Bank 1 (denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_O2SCOMP2 | unsigned long | O2 Sensor Monitor Completion Counts Bank 2 (numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_O2SCOND2 | unsigned long | O2 Sensor Monitor Conditions Encountered Counts Bank 2 (denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_EGRCOMP | unsigned long | EGR Monitor Completion Condition Counts (numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_EGRCOND | unsigned long | EGR Monitor Conditions Encountered Counts (denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_AIRCOMP1 | unsigned long | AIR Monitor Completion Condition Counts Bank 1 (Secondary Air) (numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_AIRCOND1 | unsigned long | AIR Monitor Conditions Encountered Counts Bank 1 (Secondary Air) (denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_EVAPCOMP | unsigned long | EVAP Monitor Completion Condition Counts (numerator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_EVAPCOND | unsigned long | EVAP Monitor Conditions Encountered Counts (denominator) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleichwerte-schreiben"></a>
### ABGLEICHWERTE_SCHREIBEN

0x2E5F90 ABGLEICHWERTE_SCHREIBEN Abgleichwerte Injektoren programmieren für CASCADE mit Übernahme Daten aus COD-Datei Aktivierung: Klemme 15 = EIN UND Drehzahl = 0 1/min Activation: LV_IGK = 1 UND LV_ES = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_SCHREIBEN_DATEN | string | Abgleichdaten für alle Injektoren aus COD-Datei |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_SCHREIBEN_ABGLEICHDATEN | string | Abgleichdaten zum Steuergeraet |
| ABGLEICHWERTE_SCHREIBEN_PRUEFZEICHEN | string | das im Job berechnete Pruefzeichen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-abgleichwerte-lesen"></a>
### _ABGLEICHWERTE_LESEN

0x225F90 ABGLEICHWERTE_LESEN Abgleichwerte Injektoren auslesen für CASCADE für Vergleich mit Daten aus COD-Datei Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_LESEN_DATEN | string | Abgleichdaten fuer alle Injektoren aus DME mit Pruefzeichen |
| ABGLEICHWERTE_LESEN_ABGLEICHDATEN | string | Abgleichdaten aus Steuergeraet |
| ABGLEICHWERTE_LESEN_PRUEFZEICHEN | string | das im Job berechnete Pruefzeichen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-detail"></a>
### FS_LESEN_DETAIL

0x17 FS_LESEN_DETAIL Fehlerspeicher lesen (ein Fehler / alle Details) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Fehlercode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers, fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text aus Tabelle FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_PCODE | unsigned int | optional / Pflicht fuer abgasrelevante SG, Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_PCODE7 | unsigned int | optional / fuer abgasrelevante SG, Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE7_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE7_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl, Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_LZ | int | Logistikzaehler als Zahl, Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| F_ART_ANZ | int | Anzahl der zusaetzlichen Fehlerarten Je nach dieser Anzahl i (i = 1, 2, ...), existieren i mal folgende Results: (long)   F_ARTi_NR   Index der i. Fehlerart (string) F_ARTi_TEXT Text  zur i. Fehlerart |
| F_UW_KM | long | Umweltbedingung Kilometerstand, Wertebereich: 0 - 524280 km |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...), existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-freeze-frame"></a>
### FS_LESEN_FREEZE_FRAME

0x210A FS_LESEN_FREEZE_FRAME Fehlerspeicher auslesen mit SAE Werten Umwelt und P-Code Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | die Nummer des zu lesenden Fehlers eingeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ART_ANZ | int | Anzahl der eingetragenen Fehler |
| F_ORT_NR | long | Fehlercode des SG als Index == F_CODE |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_SYMPTOM_NR | int | Gibt die Nummer der Fehlerart aus(StatusOfDTC) |
| F_SYMPTOM_TEXT | string | Interpretiert die Fehlerart |
| F_READY_NR | int | Gibt an, ob Readiness gesetzt |
| F_READY_TEXT | string | gibt einen Text zur Readiness aus |
| F_VORHANDEN_NR | int | Gibt die Nummer des Eintragstatuses aus |
| F_VORHANDEN_TEXT | string | gibt die Eintragsentprellung des Fehlers an |
| F_WARNUNG_NR | int | Gibt die Nummer fuer MIL EIN aus |
| F_WARNUNG_TEXT | string | gibt an, ob die MIL angesteuert wird |
| F_ZYKLUS_FLAG | string | gibt an, ob Zyklus-Flag gesetzt wurden ist |
| F_AKTIV_FLAG | string | gibt an, ob Diagnose laeuft |
| F_STOP_FLAG | string | gibt an, ob Stopbedingungen vorliegen |
| F_ERROR_FLAG | string | zeigt Error-Flag an |
| F_MIL_FLAG | string | zeigt den MIL-Status an |
| F_ENTPRELL_FLAG | string | gibt den MIL-Entprellstatus an |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_PCODE | int | P-Code Zahl entsprechend FO und FA |
| F_PCODE_STRING | string | P-Code Zahl als P0123 entsprechend FO und FA |
| F_PCODE_TEXT | string | P-Code Text entsprechend FO und FA |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_UW_KM | string | Km-Stand bei Erst-, Zweit- Letzmaligen Auftreten |
| F_UW1_NR | int | 1.Satz Umweltbedingung 1 Index (Ersterkennung) |
| F_UW1_TEXT | string | 1.Satz UW1 Text zur Umweltbedingung |
| F_UW1_EINH | string | 1.Satz UW1 Einheit |
| F_UW2_NR | int | 1.Satz Umweltbedingung 2 Index (Ersterkennung) |
| F_UW2_TEXT | string | 1.Satz UW2 Text zur Umweltbedingung |
| F_UW2_EINH | string | 1.Satz UW2 Einheit |
| F_UW3_NR | int | 1.Satz Umweltbedingung 3 Index (Ersterkennung) |
| F_UW3_TEXT | string | 1.Satz UW3 Text zur Umweltbedingung |
| F_UW3_EINH | string | 1.Satz UW3 Einheit |
| F_UW4_NR | int | 1.Satz Umweltbedingung 4 Index (Ersterkennung) |
| F_UW4_TEXT | string | 1.Satz UW4 Text zur Umweltbedingung |
| F_UW4_EINH | string | 1.Satz UW4 Einheit |
| F_HLC | int | Entprellvorgaenge Fahrzyklen HLC |
| F_CLA | string | Klasse |
| F_FLC | int | Entprellzähler  ( MIL an) FLC |
| F_DLC | int | Entprellvorgaenge DLC |
| F_LZ | int | Zähler Aufwärmzyklen DLC |
| F_FF0_TEXT | string | Freeze Frame Umweltbedingung 0 Text |
| F_FF0_WERT | string | Freeze Frame Umweltbedingung 0 Status Lambda Bank1 |
| F_FF1_TEXT | string | Freeze Frame Umweltbedingung 1 Text |
| F_FF1_WERT | string | Freeze Frame Umweltbedingung 1 Status Lambda Bank2 |
| F_FF2_TEXT | string | Freeze Frame Umweltbedingung 2 Text |
| F_FF2_EINH | string | Freeze Frame Umweltbedingung 2 Einheit |
| F_FF2_WERT | real | Freeze Frame Umweltbedingung 2 Lastfaktor |
| F_FF3_TEXT | string | Freeze Frame Umweltbedingung 3 Text |
| F_FF3_EINH | string | Freeze Frame Umweltbedingung 3 EINH |
| F_FF3_WERT | real | Freeze Frame Umweltbedingung 3 KuehlerTemperatur |
| F_FF4_TEXT | string | Freeze Frame Umweltbedingung 4 Text |
| F_FF4_EINH | string | Freeze Frame Umweltbedingung 4 EINH |
| F_FF4_WERT | real | Freeze Frame Umweltbedingung 4 Control Bank1 |
| F_FF5_TEXT | string | Freeze Frame Umweltbedingung 5 Text |
| F_FF5_EINH | string | Freeze Frame Umweltbedingung 5 EINH |
| F_FF5_WERT | real | Freeze Frame Umweltbedingung 5 Aadaption Bank1 |
| F_FF6_TEXT | string | Freeze Frame Umweltbedingung 6 Text |
| F_FF6_EINH | string | Freeze Frame Umweltbedingung 6 EINH |
| F_FF6_WERT | real | Freeze Frame Umweltbedingung 6 Control Bank2 |
| F_FF7_TEXT | string | Freeze Frame Umweltbedingung 7 Text |
| F_FF7_EINH | string | Freeze Frame Umweltbedingung 7 EINH |
| F_FF7_WERT | real | Freeze Frame Umweltbedingung 7 Adaption Bank2 |
| F_FF8_TEXT | string | Freeze Frame Umweltbedingung 8 Text |
| F_FF8_EINH | string | Freeze Frame Umweltbedingung 8 EINH |
| F_FF8_WERT | real | Freeze Frame Umweltbedingung 8 Ansaugdruck |
| F_FF9_TEXT | string | Freeze Frame Umweltbedingung 9 Text |
| F_FF9_EINH | string | Freeze Frame Umweltbedingung 9 EINH |
| F_FF9_WERT | real | Freeze Frame Umweltbedingung 9 Drehzahl |
| F_FF10_TEXT | string | Freeze Frame Umweltbedingung 10 Text |
| F_FF10_EINH | string | Freeze Frame Umweltbedingung 10 EINH |
| F_FF10_WERT | real | Freeze Frame Umweltbedingung 10 Fahrzeug Geschwindigkeit |
| JOB_STATUS | string | OKAY, wenn fehlerfrei, Tabelle JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anforderung an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-freeze-frame-extra-long"></a>
### FS_LESEN_FREEZE_FRAME_EXTRA_LONG

0x224019 FS_LESEN_FREEZE_FRAME_EXTRA_LONG Fehlerspeicher auslesen mit erweiterten SAE Werten Umwelt und P-Code Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | die Nummer des zu lesenden Fehlers eingeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ART_ANZ | int | Anzahl der eingetragenen Fehler |
| F_ORT_NR | long | Fehlercode des SG als Index == F_CODE |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_SYMPTOM_NR | int | Gibt die Nummer der Fehlerart aus(StatusOfDTC) |
| F_SYMPTOM_TEXT | string | Interpretiert die Fehlerart |
| F_READY_NR | int | Gibt an, ob Readiness gesetzt |
| F_READY_TEXT | string | gibt einen Text zur Readiness aus |
| F_VORHANDEN_NR | int | Gibt die Nummer des Eintragstatuses aus |
| F_VORHANDEN_TEXT | string | gibt die Eintragsentprellung des Fehlers an |
| F_WARNUNG_NR | int | Gibt die Nummer fuer MIL EIN aus |
| F_WARNUNG_TEXT | string | gibt an, ob die MIL angesteuert wird |
| F_ZYKLUS_FLAG | string | gibt an, ob Zyklus-Flag gesetzt wurden ist |
| F_AKTIV_FLAG | string | gibt an, ob Diagnose laeuft |
| F_STOP_FLAG | string | gibt an, ob Stopbedingungen vorliegen |
| F_ERROR_FLAG | string | zeigt Error-Flag an |
| F_MIL_FLAG | string | zeigt den MIL-Status an |
| F_ENTPRELL_FLAG | string | gibt den MIL-Entprellstatus an |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_PCODE | int | P-Code Zahl entsprechend FO und FA |
| F_PCODE_STRING | string | P-Code Zahl als P0123 entsprechend FO und FA |
| F_PCODE_TEXT | string | P-Code Text entsprechend FO und FA |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_UW_KM | string | Km-Stand bei Erst-, Zweit- Letzmaligen Auftreten |
| F_UW1_NR | int | 1.Satz Umweltbedingung 1 Index (Ersterkennung) |
| F_UW1_TEXT | string | 1.Satz UW1 Text zur Umweltbedingung |
| F_UW1_EINH | string | 1.Satz UW1 Einheit |
| F_UW2_NR | int | 1.Satz Umweltbedingung 2 Index (Ersterkennung) |
| F_UW2_TEXT | string | 1.Satz UW2 Text zur Umweltbedingung |
| F_UW2_EINH | string | 1.Satz UW2 Einheit |
| F_UW3_NR | int | 1.Satz Umweltbedingung 3 Index (Ersterkennung) |
| F_UW3_TEXT | string | 1.Satz UW3 Text zur Umweltbedingung |
| F_UW3_EINH | string | 1.Satz UW3 Einheit |
| F_UW4_NR | int | 1.Satz Umweltbedingung 4 Index (Ersterkennung) |
| F_UW4_TEXT | string | 1.Satz UW4 Text zur Umweltbedingung |
| F_UW4_EINH | string | 1.Satz UW4 Einheit |
| F_HLC | int | Entprellvorgaenge Fahrzyklen HLC |
| F_CLA | string | Klasse |
| F_FLC | int | Entprellzähler  ( MIL an) FLC |
| F_DLC | int | Entprellvorgaenge DLC |
| F_LZ | int | Zähler Aufwärmzyklen DLC |
| F_FF0_TEXT | string | Freeze Frame Umweltbedingung 0 Text |
| F_FF0_WERT | string | Freeze Frame Umweltbedingung 0 Zustand Lambdaregelung Bank 1 |
| F_FF1_TEXT | string | Freeze Frame Umweltbedingung 1 Text |
| F_FF1_WERT | string | Freeze Frame Umweltbedingung 1 Zustand Lambdaregelung Bank 2 |
| F_FF2_TEXT | string | Freeze Frame Umweltbedingung 2 Text |
| F_FF2_EINH | string | Freeze Frame Umweltbedingung 2 EINH |
| F_FF2_WERT | real | Freeze Frame Umweltbedingung 2 Lastfaktor |
| F_FF3_TEXT | string | Freeze Frame Umweltbedingung 3 Text |
| F_FF3_EINH | string | Freeze Frame Umweltbedingung 3 EINH |
| F_FF3_WERT | real | Freeze Frame Umweltbedingung 3 KuehlerTemperatur |
| F_FF4_TEXT | string | Freeze Frame Umweltbedingung 4 Text |
| F_FF4_EINH | string | Freeze Frame Umweltbedingung 4 EINH |
| F_FF4_WERT | real | Freeze Frame Umweltbedingung 4 Control Bank1 |
| F_FF5_TEXT | string | Freeze Frame Umweltbedingung 5 Text |
| F_FF5_EINH | string | Freeze Frame Umweltbedingung 5 EINH |
| F_FF5_WERT | real | Freeze Frame Umweltbedingung 5 Aadaption Bank1 |
| F_FF6_TEXT | string | Freeze Frame Umweltbedingung 6 Text |
| F_FF6_EINH | string | Freeze Frame Umweltbedingung 6 EINH |
| F_FF6_WERT | real | Freeze Frame Umweltbedingung 6 Control Bank2 |
| F_FF7_TEXT | string | Freeze Frame Umweltbedingung 7 Text |
| F_FF7_EINH | string | Freeze Frame Umweltbedingung 7 EINH |
| F_FF7_WERT | real | Freeze Frame Umweltbedingung 7 Adaption Bank2 |
| F_FF8_TEXT | string | Freeze Frame Umweltbedingung 8 Text |
| F_FF8_EINH | string | Freeze Frame Umweltbedingung 8 EINH |
| F_FF8_WERT | real | Freeze Frame Umweltbedingung 8 Kraftstoffdruck |
| F_FF9_TEXT | string | Freeze Frame Umweltbedingung 9 Text |
| F_FF9_EINH | string | Freeze Frame Umweltbedingung 9 EINH |
| F_FF9_WERT | real | Freeze Frame Umweltbedingung 9 Saugrohrdruck |
| F_FF10_TEXT | string | Freeze Frame Umweltbedingung 10 Text |
| F_FF10_EINH | string | Freeze Frame Umweltbedingung 10 EINH |
| F_FF10_WERT | real | Freeze Frame Umweltbedingung 10 Drehzahl |
| F_FF11_TEXT | string | Freeze Frame Umweltbedingung 11 Text |
| F_FF11_EINH | string | Freeze Frame Umweltbedingung 11 EINH |
| F_FF11_WERT | real | Freeze Frame Umweltbedingung 11 Geschwindigkeit |
| F_FF12_TEXT | string | Freeze Frame Umweltbedingung 12 Text |
| F_FF12_EINH | string | Freeze Frame Umweltbedingung 12 EINH |
| F_FF12_WERT | real | Freeze Frame Umweltbedingung 12 Zündzeitpunkt Zylinder 1 |
| F_FF13_TEXT | string | Freeze Frame Umweltbedingung 13 Text |
| F_FF13_EINH | string | Freeze Frame Umweltbedingung 13 EINH |
| F_FF13_WERT | real | Freeze Frame Umweltbedingung 13 Ansauglufttemperatur |
| F_FF14_TEXT | string | Freeze Frame Umweltbedingung 14 Text |
| F_FF14_EINH | string | Freeze Frame Umweltbedingung 14 EINH |
| F_FF14_WERT | real | Freeze Frame Umweltbedingung 14 Luftdurchsatz OBD |
| F_FF15_TEXT | string | Freeze Frame Umweltbedingung 15 Text |
| F_FF15_EINH | string | Freeze Frame Umweltbedingung 15 EINH |
| F_FF15_WERT | real | Freeze Frame Umweltbedingung 15 Drosselklappenpotentiometer 1 |
| F_FF16_TEXT | string | Freeze Frame Umweltbedingung 16 Text |
| F_FF16_EINH | string | Freeze Frame Umweltbedingung 16 EINH |
| F_FF16_WERT | real | Freeze Frame Umweltbedingung 16 Status Sekundärluftsystem |
| F_FF17_TEXT | string | Freeze Frame Umweltbedingung 17 Text |
| F_FF17_EINH | string | Freeze Frame Umweltbedingung 17 EINH |
| F_FF17_WERT | real | Freeze Frame Umweltbedingung 17 Zeit nach Start |
| F_FF18_TEXT | string | Freeze Frame Umweltbedingung 18 Text |
| F_FF18_EINH | string | Freeze Frame Umweltbedingung 18 EINH |
| F_FF18_WERT | real | Freeze Frame Umweltbedingung 18 Kraftstofftank Füllstand |
| F_FF19_TEXT | string | Freeze Frame Umweltbedingung 19 Text |
| F_FF19_EINH | string | Freeze Frame Umweltbedingung 19 EINH |
| F_FF19_WERT | real | Freeze Frame Umweltbedingung 19 Umgebungsdruck |
| F_FF20_TEXT | string | Freeze Frame Umweltbedingung 20 Text |
| F_FF20_EINH | string | Freeze Frame Umweltbedingung 20 EINH |
| F_FF20_WERT | real | Freeze Frame Umweltbedingung 20 Batteriespannung |
| F_FF21_TEXT | string | Freeze Frame Umweltbedingung 21 Text |
| F_FF21_EINH | string | Freeze Frame Umweltbedingung 21 EINH |
| F_FF21_WERT | real | Freeze Frame Umweltbedingung 21 Absolute Last |
| F_FF22_TEXT | string | Freeze Frame Umweltbedingung 22 Text |
| F_FF22_EINH | string | Freeze Frame Umweltbedingung 22 EINH |
| F_FF22_WERT | real | Freeze Frame Umweltbedingung 22 Lambda Setpoint |
| F_FF23_TEXT | string | Freeze Frame Umweltbedingung 23 Text |
| F_FF23_EINH | string | Freeze Frame Umweltbedingung 23 EINH |
| F_FF23_WERT | real | Freeze Frame Umweltbedingung 23 Relative Drosselklappenposition |
| F_FF24_TEXT | string | Freeze Frame Umweltbedingung 24 Text |
| F_FF24_EINH | string | Freeze Frame Umweltbedingung 24 EINH |
| F_FF24_WERT | real | Freeze Frame Umweltbedingung 24 Umgebungstemperatur |
| F_FF25_TEXT | string | Freeze Frame Umweltbedingung 25 Text |
| F_FF25_EINH | string | Freeze Frame Umweltbedingung 25 EINH |
| F_FF25_WERT | real | Freeze Frame Umweltbedingung 25 Drosselklappenpotentiometer 2 |
| F_FF26_TEXT | string | Freeze Frame Umweltbedingung 26 Text |
| F_FF26_EINH | string | Freeze Frame Umweltbedingung 26 EINH |
| F_FF26_WERT | real | Freeze Frame Umweltbedingung 26 Pedalwertgeber 1 |
| F_FF27_TEXT | string | Freeze Frame Umweltbedingung 27 Text |
| F_FF27_EINH | string | Freeze Frame Umweltbedingung 27 EINH |
| F_FF27_WERT | real | Freeze Frame Umweltbedingung 27 Pedalwertgeber 2 |
| F_FF28_TEXT | string | Freeze Frame Umweltbedingung 28 Text |
| F_FF28_EINH | string | Freeze Frame Umweltbedingung 28 EINH |
| F_FF28_WERT | real | Freeze Frame Umweltbedingung 28 Drosselklappenposition Setpoint |
| JOB_STATUS | string | OKAY, wenn fehlerfrei, Tabelle JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Anforderung an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-fs-lesen-hex"></a>
### FS_LESEN_HEX

0x17 FS_LESEN_HEX Fehlerspeicher auslesen als Hex Dump Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FEHLERNR | int | Eingabe der FehlerNummer |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_ORT_NR | long | Nummer des Fehlers soll FEHLERNR sein |
| F_NR_INT | int | Anzahl der eingetragenen Fehler |
| F_ORT_TEXT | string | Fehlernummer im Speicher |
| FS_ZEILE1 | string | Byte  0 -  8 des Fehlerspeichers als Dump |
| FS_ZEILE2 | string | Byte  9 - 16 des Fehlerspeichers als Dump |
| FS_ZEILE3 | string | Byte 17 - 24 des Fehlerspeichers als Dump |
| FS_ZEILE4 | string | Byte 25 - 28 des Fehlerspeichers als Dump |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen"></a>
### IS_LESEN

0x222000 IS_LESEN Infospeicher lesen (alle Info-Meldungen / Ort und Art) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text aus Tabelle FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-is-lesen-detail"></a>
### IS_LESEN_DETAIL

0x17 IS_LESEN_DETAIL Infospeicher lesen (ein Fehler / alle Details) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| F_CODE | int | gewaehlter Fehlercode |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_VERSION | int | Typ des Fehlerspeichers, fuer KWP-2000 immer 2 |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text aus Tabelle FOrtTexte ORTTEXT |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_PCODE | unsigned int | optional / Pflicht fuer abgasrelevante SG, Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_PCODE7 | unsigned int | optional / fuer abgasrelevante SG, Wertebereich 0x0000 - 0xFFFF 0x0000: wenn nicht belegt |
| F_PCODE7_STRING | string | 5 stelliger Text in der Form 'Pxxxx' '--': wenn nicht belegt '??': wenn nicht bekannt |
| F_PCODE7_TEXT | string | Fehler als Klartext '': wenn nicht belegt table PCodeTexte TEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl, Wertebereich 0 - 255 -1: ohne Haufigkeitszaehler |
| F_LZ | int | Logistikzaehler als Zahl, Wertebereich 0 - 255 -1: ohne Logistikzaehler |
| F_ART_ANZ | int | Anzahl der zusaetzlichen Fehlerarten Je nach dieser Anzahl i (i = 1, 2, ...), existieren i mal folgende Results: (long)   F_ARTi_NR   Index der i. Fehlerart (string) F_ARTi_TEXT Text  zur i. Fehlerart |
| F_UW_KM | long | Umweltbedingung Kilometerstand, Wertebereich: 0 - 524280 km |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen Je nach dieser Anzahl i (i = 1, 2, ...), existieren i mal folgende Results: (long)   F_UWi_NR   Index   der i. Umweltbedingung (string) F_UWi_TEXT Text    zur i. Umweltbedingung (real)   F_Uwi_WERT Wert    der i. Umweltbedingung (string) F_UWi_EINH Einheit der i. Umweltbedingung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-hs-lesen"></a>
### HS_LESEN

0x222100 HS_LESEN Historyspeicher lesen (alle Info-Meldungen / Ort und Art) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| F_HEX_CODE | binary | Fehlerdaten pro Fehler als Hexcode |
| F_ORT_NR | long | Index fuer Fehlerort |
| F_ORT_TEXT | string | Fehlerort als Text |
| F_SYMPTOM_NR | int | Fehlersymptom (Standard-Fehlerart) als Zahl |
| F_SYMPTOM_TEXT | string | Fehlersymptom (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_READY_NR | int | Readyness Flag (Standard-Fehlerart) als Zahl |
| F_READY_TEXT | string | Readyness Flag (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_VORHANDEN_NR | int | Fehler vorhanden (Standard-Fehlerart) als Zahl |
| F_VORHANDEN_TEXT | string | Fehler vorhanden (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_WARNUNG_NR | int | Warnlampen Flag (Standard-Fehlerart) als Zahl |
| F_WARNUNG_TEXT | string | Warnlampen Flag (Standard-Fehlerart) als Text aus Tabelle FArtTexte ARTTEXT |
| F_HFK | int | Haufigkeitszaehler als Zahl, Wertebereich 0 - 255 |
| F_HSKM1 | string | km - Stand beim ersten Auftreten |
| F_HSKM2 | string | km - Stand beim zweiten Auftreten |
| F_HSKM3 | string | km - Stand beim letzten Auftreten |
| F_CLA | string | Fehlerklasse als hex Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-ident-aif"></a>
### IDENT_AIF

0x1A80 und 0x23 IDENT_AIF Identdaten und Anwender Informations Felder Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
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
| ID_LIEF_TEXT | string | Lieferanten-Text nach Tabelle Lieferanten |
| ID_SW_NR_MCV | string | Softwarenummer (message catalogue version) |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| ID_SW_NR_OSV | string | Softwarenummer (operating system version) |
| ID_SW_NR_RES | string | Softwarenummer (reserved - currently unused) |
| AIF_ADRESSE | long | AIF Adresse |
| AIF_FAHRGESTELL_NR | string | Fahrgestellnummer 7-stellig |
| AIF_PROGRAMMIER_DATUM | string | Datum der SG-Programmierung in der Form JJJJ.MM.TT |
| AIF_ZUSAMMENBAU_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_DATENSATZ_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_TESTER_NR | string | Tester Seriennummer |
| AIF_KM_STAND | long | km-Stand bei der Programmierung |
| AIF_PROGRAMM_STAND | string | Programmstandsnummer |
| AIF_ANZ_FREI | int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ANZ_DATEN | int | Groesse des AIF-Eintrags |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-interfacetype"></a>
### INTERFACETYPE

Interface-Typ bestimmen und ausgeben (Wichtig für Baudratenumschaltung: da bei ADS, EADS und OBD nur 115200 Baud und bei EDIC nur 125000 Baud möglich sind) Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| INTERFACE_TYP | string | Rueckmeldung des Interface-Typs |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-set-baudrate"></a>
### SET_BAUDRATE

Initialisierung der Kommunikationsparameter mit bestimmter Baudrate Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BAUDRATE | string | die gewuenschte Baudrate |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-set-parameter"></a>
### SET_PARAMETER

Aenderung der Kommunikationsparameter bei Long-Parametersätzen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| KONZEPT | string | Konzept |
| BAUDRATE | string | Baudrate |
| TIMEOUT | string | Timeout in ms |
| REGENERATIONSZEIT | string | Regenerationszeit in ms |
| TELEGRAMMENDEZEIT | string | Telegrammendezeit in ms |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-speicher-lesen-ascii"></a>
### SPEICHER_LESEN_ASCII

0x23 SPEICHER_LESEN_ASCII Auslesen des Steuergeraete-Speichers Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | string | SpeicherSegment aus Tabelle SEG_NAME SEG_TEXT |
| ADRESSE | long | Speicherzellenadresse 0x00000000 - 0xFFFFFFFF |
| ANZAHL | int | Anzahl auszulesende Bytes 1 - n ( 254 ) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DATEN | binary | ausgelesene Daten |
| DATEN_ASCII | string | ausgelesene Daten als ASCII Format |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

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
| STAT_EWS4_SERVER_SK_LOCKED | int | 0 SecretKey server lässt sich noch direkt schreiben 1 SecretKey server lässt sich nicht mehr schreiben/lesen |
| STAT_EWS4_CLIENT_SK_LOCKED | int | 0 SecretKey client lässt sich noch direkt schreiben 1 SecretKey client lässt sich nicht mehr schreiben/lesen |
| STAT_CLIENT_AUTHENTICATED | int | 0 Freigabe von Zuendung und Einspritzung (noch) nicht erteilt (noch nicht versucht oder Kommunikation gestört, Motorlauf gesperrt) 1 Freigabe von Zuendung und Einspritzung erteilt (Challenge-Response erfolgreich) 2 Freigabe von Zuendung und Einspritzung abgelehnt (Challenge-Response fehlgeschlagen, falsche Response, Kommunikation i.O.) 3 nicht definiert |
| STAT_CLIENT_AUTHENTICATED_TXT | string |  |
| _STAT_FREE_SK0 | int | 0..0xFD Freie Flashablagen 0xFE    Freie Flashablage nicht begrenzt 0xFF    Fehlerkennzeichnung |
| _STAT_FREE_SK0_TXT | string |  |
| _STAT_FREE_SK1 | int | 0..0xFD Freie Flashablagen 0xFE    Freie Flashablage nicht begrenzt 0xFF    Fehlerkennzeichnung |
| _STAT_FREE_SK1_TXT | string |  |
| _STAT_VERSION | int | 0x01 Direktschreiben des SecretKey |
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

17 "EWS4-data" schreiben KWP 2000: $2E ReadDataByCommonIdentifier CommonIdentifier=0xC001

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | string | Byte0 LOCK_SERVER_SK LOCK_CLIENT_SK WRITE_SERVER_SK WRITE_CLIENT_SK |
| DATA | string | Byte1...16 16 Byte Daten (SecretKey), falls MODE = WRITE_SERVER_SK/WRITE_CLIENT_SK, "0x01,0x02,.." KEINE Daten nötig, falls MODE = LOCK_SERVER_SK/LOCK_CLIENT_SK |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-flash-parameter-lesen"></a>
### FLASH_PARAMETER_LESEN

Gibt die SG-spezifischen Flash-Parameter zurück

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY oder ERROR_DIAG_PROT oder ERROR_SG_AUTHENTISIERUNG |
| SG_ADRESSE | int | Steuergeräteadresse |
| SG_MAXANZAHL_AIF | int | Anzahl der Anwender-Infofelder |
| SG_GROESSE_AIF | int | Grösse des Anwender-Infofeldes |
| SG_ENDEKENNUNG_AIF | int | Offset für letztes Anwender-Infofeld |
| SG_AUTHENTISIERUNG | string | Authentisierungsart table Authentisierung AUTH_TEXT |
| DIAG_PROT_IST | string | Gibt das aktuelle gewählte Protokoll aus table KONZEPT_TABELLE KONZEPT_TEXT |

<a id="job-flash-parameter-setzen"></a>
### FLASH_PARAMETER_SETZEN

Setzt die SG-spezifischen Flash-Parameter

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SG_ADRESSE | int | Steuergeräteadresse |
| SG_MAXANZAHL_AIF | int | Anzahl der Anwender-Infofelder 0x00  Nicht zulässig sonst Anzahl der AIF |
| SG_GROESSE_AIF | int | Grösse des Anwender-Infofeldes 0x12  18 dez kleines AIF 0x33  51 dez grosses AIF 0x40  64 dez grosses AIF ( gilt nur für Power-Pc ) sonst Nicht zulässig |
| SG_ENDEKENNUNG_AIF | int | Offset für letztes Anwender-Infofeld 0xFE  Letztes AIF nicht überschreibbar 0x01  Letztes AIF ist überschreibbar sonst Nicht zulässig |
| SG_AUTHENTISIERUNG | string | Authentisierungsart table Authentisierung AUTH_TEXT |
| DIAG_PROT | string | optionaler Parameter Diagnoseprotokoll table KONZEPT_TABELLE KONZEPT_TEXT |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY |

<a id="job-ident-ibs"></a>
### IDENT_IBS

$22 40 21 BMW Nr, Seriennummer, SW/HW Index

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ID_BMW_NR | string | BMW-Teilenummer 7 stellig |
| SERIENNUMMER | unsigned long | BMW-Seriennummer |
| ZIF_PROGRAMMSTAND | int | Programm referenz |
| ZIF_STATUS | int | Programm Revision |
| HW_REF | int | Hardware Referenz |

<a id="job-status-systemcheck-pm-info-1"></a>
### STATUS_SYSTEMCHECK_PM_INFO_1

$22 40 22 Bytefeld 1 Batterie Powermanagement lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_RUHESTROMANALYSE_MODE_WERT | int | Modus der Ruhestromanalyse (1 = als Histogramm (nicht Layer), 2 = Bitcodiert für 32 Zyklen (Layer)) |
| STAT_RUHESTROMANALYSE_MODE_TEXT | string | Modus der Ruhestromanalyse (1 = als Histogramm (nicht Layer), 2 = Bitcodiert für 32 Zyklen (Layer)) |
| STAT_BATTERIELADUNG_BILANZ_WERT | real | Differenz LADUNG - ENTLADUNG in Ah 0 - 19088 |
| STAT_BATTERIELADUNG_BILANZ_EINH | string | Einheit |
| STAT_BATTERIELADUNG_GESAMT_WERT | real | Batterie Ladungen in Ah 0 - 19088 |
| STAT_BATTERIELADUNG_GESAMT_EINH | string | Einheit |
| STAT_BATTERIEENTLADUNG_GESAMT_WERT | real | Batterie Ladungen in Ah 0 - 19088 |
| STAT_BATTERIEENTLADUNG_GESAMT_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_0_20_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_0_20_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_20_40_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_20_40_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_40_60_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_40_60_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_60_80_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_60_80_EINH | string | Einheit |
| STAT_ZEIT_IM_LADUNGSBEREICH_80_100_WERT | real | Bereich 0-65535h |
| STAT_ZEIT_IM_LADUNGSBEREICH_80_100_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_0_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_0_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_0_20_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_0_20_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_20_40_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_20_40_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_40_60_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_40_60_EINH | string | Einheit |
| STAT_ZEIT_IM_TEMPERATURBEREICH_AB_60_WERT | real | Zeitdauer 0 - 327675 Minuten |
| STAT_ZEIT_IM_TEMPERATURBEREICH_AB_60_EINH | string | Einheit |
| STAT_KM_STAND_AKTUELL_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_AKTUELL_EINH | string | Einheit |
| STAT_KM_STAND_VOR_1_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_1_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_2_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_2_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_3_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_3_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_4_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_4_TAG_EINH | string | Einheit |
| STAT_KM_STAND_VOR_5_TAG_WERT | real | 0 - 655350 km |
| STAT_KM_STAND_VOR_5_TAG_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_LETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_LETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_DRITTLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_DRITTLETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_VIERTLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_VIERTLETZTER_EINH | string | Einheit |
| STAT_BATTERIETAUSCH_FUENFTLETZTER_WERT | real | 0 - 655350 km |
| STAT_BATTERIETAUSCH_FUENFTLETZTER_EINH | string | Einheit |
| STAT_BATTENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_WERT | real | 0 - 19088 Ah |
| STAT_BATTENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_EINH | string | Einheit Ah |
| STAT_RUHESTROM_AKTUELL | string |  |
| STAT_RUHESTROM_VOR_1_ZYKLUS | string |  |
| STAT_RUHESTROM_VOR_2_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_3_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_4_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_5_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_6_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_7_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_8_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_9_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_10_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_11_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_12_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_13_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_14_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_15_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_16_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_17_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_18_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_19_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_20_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_21_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_22_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_23_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_24_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_25_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_26_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_27_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_28_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_29_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_30_ZYKLEN | string |  |
| STAT_RUHESTROM_VOR_31_ZYKLEN | string |  |
| STAT_IBS_FEHLERZAEHLER_BSD_PARITY_WERT | real | Anzahl 0 - 65535 |
| STAT_IBS_FEHLERZAEHLER_BSD_PARITY_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_WATCHDOG_RESET_WERT | real | Anzahl 0 - 65535 |
| STAT_IBS_FEHLERZAEHLER_WATCHDOG_RESET_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_POWER_ON_RESET_WERT | real | Anzahl 0 - 65535 |
| STAT_IBS_FEHLERZAEHLER_POWER_ON_RESET_EINH | string | Einheit |
| STAT_KTBS_FEHLERZAEHLER_BSD_ERWEITERT_WERT | real | Anzahl 0 - 65535 |
| STAT_KTBS_FEHLERZAEHLER_BSD_ERWEITERT_EINH | string | Einheit |
| STAT_KTIBS_FEHLERZAEHLER_BSD_WERT | real | Anzahl 0 - 65535 |
| STAT_KTIBS_FEHLERZAEHLER_BSD_EINH | string | Einheit |
| STAT_KTIBS_FEHLERZAEHLER_EBSD_CHECKSUMME_WERT | real | Anzahl 0 - 65535 |
| STAT_KTIBS_FEHLERZAEHLER_EBSD_CHECKSUMME_EINH | string | Einheit |

<a id="job-status-systemcheck-pm-info-2"></a>
### STATUS_SYSTEMCHECK_PM_INFO_2

$22 40 23 Bytefeld 2 Batterie Powermanagement lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| STAT_BATTERIE_KAPAZITAET_WERT | real | Batterie Kapazitaet in Ah 0 - 255 |
| STAT_BATTERIE_KAPAZITAET_EINH | string | Einheit |
| STAT_SOH_WERT | real | Bereich -50% - 49,6% |
| STAT_SOH_EINH | string | Einheit |
| STAT_SOC_FIT_WERT | real | Bereich 0-100% |
| STAT_SOC_FIT_EINH | string | Einheit |
| STAT_TEMP_SAISON_WERT | real | Bereich -128C - 127C |
| STAT_TEMP_SAISON_EINH | string | Einheit C |
| STAT_KALIBRIER_EVENT_CNT_WERT | real | Kalibrieranzahl 0 - 255 |
| STAT_KALIBRIER_EVENT_CNT_EINH | string | Einheit |
| STAT_Q_SOC_AKTUELL_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_AKTUELL_EINH | string | Einheit |
| STAT_Q_SOC_VOR_1_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_1_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_2_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_2_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_3_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_3_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_4_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_4_TAG_EINH | string | Einheit |
| STAT_Q_SOC_VOR_5_TAG_WERT | real | Kapazitaet 0 - 1188 Ah |
| STAT_Q_SOC_VOR_5_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_EINH | string | Einheit |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_AKTUELL_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_AKTUELL_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_EINH | string | Einheit |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_WERT | real | Kapazitaet 0 - 100% |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_DOWNLOAD_CHECKSUMME_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_DOWNLOAD_CHECKSUMME_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_EEPROM_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_EEPROM_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_RAM_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_RAM_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_PROM_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_PROM_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_I2C_NAC_DIAGNOSE_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_I2C_NAC_DIAGNOSE_EINH | string | Einheit |
| STAT_IBS_FEHLERZAEHLER_I2C_BUS_COLLISION_WERT | real | Anzahl 0 - 255 |
| STAT_IBS_FEHLERZAEHLER_I2C_BUS_COLLISION_EINH | string | Einheit |

<a id="job-steuern-pm-histogram-reset"></a>
### STEUERN_PM_HISTOGRAM_RESET

$30 F5 04 Loeschen von pminfo1 index 23-30

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-adap-selektiv-loeschen"></a>
### ADAP_SELEKTIV_LOESCHEN

Löschen von Adaptionen und gelernte Varianten KWP 2000 $31 30 xx xx xx Loeschen der Adaptionswerte

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE_1 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_2 | int | Bit=1 löscht Bit=0 behält alten Wert |
| AUSWAHLBYTE_3 | int | Bit=1 löscht Bit=0 behält alten Wert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-batterietausch-registrieren"></a>
### STEUERN_BATTERIETAUSCH_REGISTRIEREN

KWP 2000 $31 30 00 10 00 Bit setzen Batterietausch registrieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-pm-messemode"></a>
### START_SYSTEMCHECK_PM_MESSEMODE

$31 F6 Systemdiagnose BatterieSensor reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-pm-messemode"></a>
### STOP_SYSTEMCHECK_PM_MESSEMODE

$32 F6 Systemdiagnose BatterieSensor reset beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-sleep-mode-funktional"></a>
### SLEEP_MODE_FUNKTIONAL

SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier $05 PowerDown Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FUNKTIONALE_ADRESSE | string | gewuenschte funktionale Adresse table FunktionaleAdresse F_ADR F_ADR_TEXT Defaultwert: ALL ( alle Steuergeraete ) |
| OHNE_POWERMODUL | string | Power Down ohne Powermodul Werte: JA, NEIN table DigitalArgument TEXT Defaultwert: NEIN |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ECU_ADR | string | Steuergeraeteadresse als Hex-String |
| ECU_GROBNAME | string | Grobname des Steuergeraetes table Grobname GROBNAME |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-kup"></a>
### _STATUS_KUP

0x300401 STATUS_KUP Kupplungsschalter auslesen NO_CON

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_KUP_WERT | real | Status Kupplungsschalter 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_STAT_KUP_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-msa"></a>
### STATUS_MSA

0x22402F STATUS_MSA MSA (MotorStopAutomatik) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_MSA | unsigned long | Status MSA und Funktionsabschalter Stmsa   Min: 0 Max: 4294967295 |
| STAT_STAT_MSAAV | unsigned long | Status MSA aktiv und bereit und Abschaltverhinderer Stmsaav   Min: 0 Max: 4294967295 |
| STAT_STAT_MSAEV | unsigned long | Status MSA Einschaltverhinderer Stmsaev   Min: 0 Max: 4294967295 |
| STAT_STAT_MSAAA | unsigned long | Status MSA Auschaltaufforderer Stmsaaa   Min: 0 Max: 4294967295 |
| STAT_STAT_MSAEA | unsigned long | Status MSA Einschaltaufforderer Stmsaea   Min: 0 Max: 4294967295 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-msa-deak"></a>
### STATUS_MSA_DEAK

0x225F8E STATUS_MSA_DEAK MSA (MotorStopAutomatik) deaktivieren auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_MSA_DEAK | unsigned long | MSA (MotorStopAutomatik) deaktiviert (0=falsch 1=wahr) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-msa-deak-av"></a>
### STATUS_MSA_DEAK_AV

0x225F8F STATUS_MSA_DEAK_AV Selektive Deaktivierung Abschaltverhinderer MSA (MotorStopAutomatik) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STAT_MSA_DEAK_AV | unsigned long | Selektive Deaktivierung Abschaltverhinderer MSA (MotorStopAutomatik) Swmsaav   Min: 0 Max: 4294967295 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-msaring"></a>
### _STATUS_MSARING

0x22401C STATUS_MSARING Ringspeicher Motor-Start/Stop Automatik (MSA) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MSASTZ | unsigned long | Zaehler aller Startversuche Msastz   Min: 0 Max: 65535 |
| STAT_MSASTZMSA | unsigned long | Zaehler der MSA-Startversuche Msastzmsa   Min: 0 Max: 65535 |
| STAT_MSA_INDEXRS | unsigned long | Ringspeicher-Index Msa_indexrs   Min: 0 Max: 20 |
| STAT_AV12 | unsigned long | Msa_arravrs[59] Bit 7 (most significant bit) --- Abschaltverhinderer Nr. 12 aktuell aktiv 1BIT IDENTICAL |
| STAT_AV12AK_WERT | unsigned long | AV wurde zuletzt aktiviert (Flanke pos.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV12AK_EINH | string | km |
| STAT_AV12DEAK_WERT | unsigned long | AV wurde zuletzt deaktiviert (Flanke neg.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV12DEAK_EINH | string | km |
| STAT_AV12HFK | unsigned long | Auftretenshaeufigkeit (total) MSARING_13BIT_HFK   Min: 8191 Max: 8191 |
| STAT_AV11 | unsigned long | Abschaltverhinderer Nr. 11 aktuell aktiv 1BIT IDENTICAL |
| STAT_AV11AK_WERT | unsigned long | AV wurde zuletzt aktiviert (Flanke pos.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV11AK_EINH | string | km |
| STAT_AV11DEAK_WERT | unsigned long | AV wurde zuletzt deaktiviert (Flanke neg.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV11DEAK_EINH | string | km |
| STAT_AV11HFK | unsigned long | Auftretenshaeufigkeit (total) MSARING_13BIT_HFK   Min: 8191 Max: 8191 |
| STAT_AV10 | unsigned long | Abschaltverhinderer Nr. 10 aktuell aktiv 1BIT IDENTICAL |
| STAT_AV10AK_WERT | unsigned long | AV wurde zuletzt aktiviert (Flanke pos.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV10AK_EINH | string | km |
| STAT_AV10DEAK_WERT | unsigned long | AV wurde zuletzt deaktiviert (Flanke neg.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV10DEAK_EINH | string | km |
| STAT_AV10HFK | unsigned long | Auftretenshaeufigkeit (total) MSARING_13BIT_HFK   Min: 8191 Max: 8191 |
| STAT_AV09 | unsigned long | Abschaltverhinderer Nr. 09 aktuell aktiv 1BIT IDENTICAL |
| STAT_AV09AK_WERT | unsigned long | AV wurde zuletzt aktiviert (Flanke pos.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV09AK_EINH | string | km |
| STAT_AV09DEAK_WERT | unsigned long | AV wurde zuletzt deaktiviert (Flanke neg.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV09DEAK_EINH | string | km |
| STAT_AV09HFK | unsigned long | Auftretenshaeufigkeit (total) MSARING_13BIT_HFK   Min: 8191 Max: 8191 |
| STAT_AV08 | unsigned long | Abschaltverhinderer Nr. 08 aktuell aktiv 1BIT IDENTICAL |
| STAT_AV08AK_WERT | unsigned long | AV wurde zuletzt aktiviert (Flanke pos.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV08AK_EINH | string | km |
| STAT_AV08DEAK_WERT | unsigned long | AV wurde zuletzt deaktiviert (Flanke neg.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV08DEAK_EINH | string | km |
| STAT_AV08HFK | unsigned long | Auftretenshaeufigkeit (total) MSARING_13BIT_HFK   Min: 8191 Max: 8191 |
| STAT_AV07 | unsigned long | Abschaltverhinderer Nr. 07 aktuell aktiv 1BIT IDENTICAL |
| STAT_AV07AK_WERT | unsigned long | AV wurde zuletzt aktiviert (Flanke pos.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV07AK_EINH | string | km |
| STAT_AV07DEAK_WERT | unsigned long | AV wurde zuletzt deaktiviert (Flanke neg.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV07DEAK_EINH | string | km |
| STAT_AV07HFK | unsigned long | Auftretenshaeufigkeit (total) MSARING_13BIT_HFK   Min: 8191 Max: 8191 |
| STAT_AV06 | unsigned long | Abschaltverhinderer Nr. 06 aktuell aktiv 1BIT IDENTICAL |
| STAT_AV06AK_WERT | unsigned long | AV wurde zuletzt aktiviert (Flanke pos.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV06AK_EINH | string | km |
| STAT_AV06DEAK_WERT | unsigned long | AV wurde zuletzt deaktiviert (Flanke neg.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV06DEAK_EINH | string | km |
| STAT_AV06HFK | unsigned long | Auftretenshaeufigkeit (total) MSARING_13BIT_HFK   Min: 8191 Max: 8191 |
| STAT_AV05 | unsigned long | Abschaltverhinderer Nr. 05 aktuell aktiv 1BIT IDENTICAL |
| STAT_AV05AK_WERT | unsigned long | AV wurde zuletzt aktiviert (Flanke pos.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV05AK_EINH | string | km |
| STAT_AV05DEAK_WERT | unsigned long | AV wurde zuletzt deaktiviert (Flanke neg.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV05DEAK_EINH | string | km |
| STAT_AV05HFK | unsigned long | Auftretenshaeufigkeit (total) MSARING_13BIT_HFK   Min: 8191 Max: 8191 |
| STAT_AV04 | unsigned long | Abschaltverhinderer Nr. 04 aktuell aktiv 1BIT IDENTICAL |
| STAT_AV04AK_WERT | unsigned long | AV wurde zuletzt aktiviert (Flanke pos.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV04AK_EINH | string | km |
| STAT_AV04DEAK_WERT | unsigned long | AV wurde zuletzt deaktiviert (Flanke neg.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV04DEAK_EINH | string | km |
| STAT_AV04HFK | unsigned long | Auftretenshaeufigkeit (total) MSARING_13BIT_HFK   Min: 8191 Max: 8191 |
| STAT_AV03 | unsigned long | Abschaltverhinderer Nr. 03 aktuell aktiv 1BIT IDENTICAL |
| STAT_AV03AK_WERT | unsigned long | AV wurde zuletzt aktiviert (Flanke pos.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV03AK_EINH | string | km |
| STAT_AV03DEAK_WERT | unsigned long | AV wurde zuletzt deaktiviert (Flanke neg.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV03DEAK_EINH | string | km |
| STAT_AV03HFK | unsigned long | Auftretenshaeufigkeit (total) MSARING_13BIT_HFK   Min: 8191 Max: 8191 |
| STAT_AV02 | unsigned long | Abschaltverhinderer Nr. 02 aktuell aktiv 1BIT IDENTICAL |
| STAT_AV02AK_WERT | unsigned long | AV wurde zuletzt aktiviert (Flanke pos.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV02AK_EINH | string | km |
| STAT_AV02DEAK_WERT | unsigned long | AV wurde zuletzt deaktiviert (Flanke neg.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV02DEAK_EINH | string | km |
| STAT_AV02HFK | unsigned long | Auftretenshaeufigkeit (total) MSARING_13BIT_HFK   Min: 8191 Max: 8191 |
| STAT_AV01 | unsigned long | Msa_arravrs[4] Bit 7 (most significant bit) --- Abschaltverhinderer Nr. 01 aktuell aktiv 1BIT IDENTICAL |
| STAT_AV01AK_WERT | unsigned long | AV wurde zuletzt aktiviert (Flanke pos.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV01AK_EINH | string | km |
| STAT_AV01DEAK_WERT | unsigned long | AV wurde zuletzt deaktiviert (Flanke neg.) vor Kilometer MSARING_13BIT_KM   Einheit: km   Min: 8191 Max: 8191 |
| STAT_AV01DEAK_EINH | string | km |
| STAT_AV01HFK | unsigned long | Auftretenshaeufigkeit (total) MSARING_13BIT_HFK   Min: 8191 Max: 8191 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-nullgang-erkennung"></a>
### STATUS_NULLGANG_ERKENNUNG

0x22402E STATUS_NULLGANG_ERKENNUNG Nullgang Erkennung auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PHY_NG_POSITION_WERT | real | Aktuelle Position Nullgangsensor Tvngang   Einheit: %   Min: 0 Max: 655.35 |
| STAT_PHY_NG_POSITION_EINH | string | percent |
| STAT_PHY_NG_LERN_WERT | real | angelernter Wert Nullgangsensor Tvneutral   Einheit: %   Min: 0 Max: 655.35 |
| STAT_PHY_NG_LERN_EINH | string | percent |
| STAT_STAT_NG_ERKANNT | unsigned long | Status Nullgangerkennung (Fahrzeug befindet sich aktuell im Nullgang) (0=falsch 1= wahr) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_STAT_NG_GELERNT | unsigned long | Nullgangsensor ist bereits eingelernt (0=falsch 1= wahr) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_STAT_KUP_BETAETIGT | unsigned long | Kupplung betaetigt (0=falsch 1= wahr) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_STAT_MOT_DREHT | unsigned long | Motor laeuft (0=falsch 1= wahr) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_STAT_NG_IM_LF | unsigned long | Sensorwert im Lernfenster (kein Gang eingelegt) (0=falsch 1= wahr) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-msa-deak"></a>
### STEUERN_ENDE_MSA_DEAK

0x2E5F8E00 STEUERN_ENDE_MSA_DEAK MSA (MotorStopAutomatik) deaktivieren Vorgeben beenden NO_CON

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-ende-msa-deak-av"></a>
### STEUERN_ENDE_MSA_DEAK_AV

0x2E5F8F00 STEUERN_ENDE_MSA_DEAK_AV Selektive Deaktivierung Abschaltverhinderer MSA (MotorStopAutomatik) Vorgeben beenden NO_CON

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-msa-deak"></a>
### STEUERN_MSA_DEAK

0x2E5F8E07 STEUERN_MSA_DEAK MSA (MotorStopAutomatik) deaktivieren vorgeben NO_CON

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-msa-deak-av"></a>
### STEUERN_MSA_DEAK_AV

0x2E5F8F07 STEUERN_MSA_DEAK_AV Selektive Deaktivierung Abschaltverhinderer MSA (MotorStopAutomatik) vorgeben NO_CON

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_STAT_MSA_DEAK_AV_WERT | unsigned long | Selektive Deaktivierung Abschaltverhinderer MSA (MotorStopAutomatik) Swmsaav   Min: 0 Max: 4294967295 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-msaring-hfkreset"></a>
### STEUERN_MSARING_HFKRESET

0x2E5F89 STEUERN_MSARING_HFKRESET MSARING Haeufigkeitszaehler Reset NO_CON

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-nullgang-lernen"></a>
### STEUERN_NULLGANG_LERNEN

0x312E STEUERN_NULLGANG_LERNEN Ansteuern Nullgang lernen (Der Nullgang-Lernwert ist nichtfluechtig so abzulegen, dass er bei Reprogrammierung nicht Ã¼berschrieben wird.)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-steuern-nullgang-schreiben"></a>
### STEUERN_NULLGANG_SCHREIBEN

0x2E5F8A STEUERN_NULLGANG_SCHREIBEN Schreiben Nullgang Lernwert

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STAT_NGS_WERT | real | Nullgang Lernwert Tvneutral   Einheit: %   Min: 0 Max: 655.35 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
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
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [VERBAUORTTABELLE](#table-verbauorttabelle) (11 × 2)
- [PARTNRTABELLE](#table-partnrtabelle) (1 × 3)
- [MESSWERTEMODE](#table-messwertemode) (14 × 3)
- [CBSKENNUNG](#table-cbskennung) (16 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (3 × 2)
- [FORTTEXTE](#table-forttexte) (374 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FARTTEXTEERWEITERT](#table-farttexteerweitert) (11 × 3)
- [FUMWELTMATRIX](#table-fumweltmatrix) (352 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (640 × 9)
- [FARTTYP](#table-farttyp) (368 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (429 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 2)
- [MESSWERTETAB](#table-messwertetab) (640 × 12)
- [FARTSTATUSTEXTE](#table-fartstatustexte) (9 × 2)
- [BITS](#table-bits) (23 × 4)
- [LAMBDASTATUS](#table-lambdastatus) (7 × 2)
- [GROBNAME](#table-grobname) (48 × 2)
- [FARTERWTEXTE](#table-farterwtexte) (8 × 2)
- [_CNV_S_10_STATE_EOL__452](#table-cnv-s-10-state-eol-452) (11 × 2)
- [_CNV_S_11_DEF_BA_WM_614](#table-cnv-s-11-def-ba-wm-614) (12 × 2)
- [_CNV_S_11_EGCP_RANGE_375](#table-cnv-s-11-egcp-range-375) (12 × 2)
- [_CNV_S_11_RANGE_STAT_941](#table-cnv-s-11-range-stat-941) (12 × 2)
- [_CNV_S_4_EGCP_RANGE_377](#table-cnv-s-4-egcp-range-377) (5 × 2)
- [_CNV_S_4_EGCP_RANGE_384](#table-cnv-s-4-egcp-range-384) (5 × 2)
- [_CNV_S_5_DEF_BA_GDI_609](#table-cnv-s-5-def-ba-gdi-609) (6 × 2)
- [_CNV_S_5_LACO_RANGE_410](#table-cnv-s-5-laco-range-410) (6 × 2)
- [_CNV_S_5_RANGE_STAT_290](#table-cnv-s-5-range-stat-290) (6 × 2)
- [_CNV_S_5_RANGE_STAT_971](#table-cnv-s-5-range-stat-971) (6 × 2)
- [_CNV_S_6_ACRC_RANGE_871](#table-cnv-s-6-acrc-range-871) (7 × 2)
- [_CNV_S_6_RANGE_STAT_106](#table-cnv-s-6-range-stat-106) (7 × 2)
- [_CNV_S_6_RANGE_STAT_167](#table-cnv-s-6-range-stat-167) (7 × 2)
- [_CNV_S_7_EGCP_RANGE_357](#table-cnv-s-7-egcp-range-357) (8 × 2)
- [_CNV_S_7_RANGE_ECU__165](#table-cnv-s-7-range-ecu-165) (8 × 2)
- [_CNV_S_8_RANGE_STAT_21](#table-cnv-s-8-range-stat-21) (9 × 2)
- [FUNKTIONALEADRESSE](#table-funktionaleadresse) (8 × 3)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [STAT_RUHESTROM](#table-stat-ruhestrom) (17 × 2)
- [_MSD8ASAM_TABLE_MSA_URSACHE_EA](#table-msd8asam-table-msa-ursache-ea) (4 × 2)
- [_MSD8ASAM_TABLE_UEN](#table-msd8asam-table-uen) (2 × 2)
- [_MSD8ASAM_CNV_S_5_DEF_BA_GDI_588_CM](#table-msd8asam-cnv-s-5-def-ba-gdi-588-cm) (5 × 2)
- [_MSD8ASAM_CNV_S_2_DEF_BIT_UB_741_CM](#table-msd8asam-cnv-s-2-def-bit-ub-741-cm) (2 × 2)
- [_MSD8ASAM_CNV_S_2_DEF_BIT_UB_755_CM_4DC3300S](#table-msd8asam-cnv-s-2-def-bit-ub-755-cm-4dc3300s) (2 × 2)
- [_MSD8ASAM_CNV_S_2_DEF_BIT_UB_755_CM0X2_4DC3300S](#table-msd8asam-cnv-s-2-def-bit-ub-755-cm0x2-4dc3300s) (2 × 2)
- [_MSD8ASAM_CNV_S_10_STATE_EOL__449_CM_4DC3200S](#table-msd8asam-cnv-s-10-state-eol-449-cm-4dc3200s) (10 × 2)
- [_MSD8ASAM_CNV_S_10_STATE_EOL__450_CM_4DC3200S](#table-msd8asam-cnv-s-10-state-eol-450-cm-4dc3200s) (4 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT7](#table-msd8asam-table-switch-position-high-byte-bit7) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT6](#table-msd8asam-table-switch-position-high-byte-bit6) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT5](#table-msd8asam-table-switch-position-high-byte-bit5) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT4](#table-msd8asam-table-switch-position-high-byte-bit4) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT3](#table-msd8asam-table-switch-position-high-byte-bit3) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT2](#table-msd8asam-table-switch-position-high-byte-bit2) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT1](#table-msd8asam-table-switch-position-high-byte-bit1) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT0](#table-msd8asam-table-switch-position-high-byte-bit0) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_LOW_BYTE_BIT7](#table-msd8asam-table-switch-position-low-byte-bit7) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_LOW_BYTE_BIT6](#table-msd8asam-table-switch-position-low-byte-bit6) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_LOW_BYTE_BIT3](#table-msd8asam-table-switch-position-low-byte-bit3) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_LOW_BYTE_BIT2](#table-msd8asam-table-switch-position-low-byte-bit2) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_LOW_BYTE_BIT5](#table-msd8asam-table-tempomat-aus-irr-low-byte-bit5) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_LOW_BYTE_BIT4](#table-msd8asam-table-tempomat-aus-irr-low-byte-bit4) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_LOW_BYTE_BIT3](#table-msd8asam-table-tempomat-aus-irr-low-byte-bit3) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_LOW_BYTE_BIT2](#table-msd8asam-table-tempomat-aus-irr-low-byte-bit2) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_LOW_BYTE_BIT1](#table-msd8asam-table-tempomat-aus-irr-low-byte-bit1) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_LOW_BYTE_BIT0](#table-msd8asam-table-tempomat-aus-irr-low-byte-bit0) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT6](#table-msd8asam-table-tempomat-aus-irr-high-byte-bit6) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT5](#table-msd8asam-table-tempomat-aus-irr-high-byte-bit5) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT4](#table-msd8asam-table-tempomat-aus-irr-high-byte-bit4) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT3](#table-msd8asam-table-tempomat-aus-irr-high-byte-bit3) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT2](#table-msd8asam-table-tempomat-aus-irr-high-byte-bit2) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT1](#table-msd8asam-table-tempomat-aus-irr-high-byte-bit1) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT0](#table-msd8asam-table-tempomat-aus-irr-high-byte-bit0) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_LOW_BYTE_BIT4](#table-msd8asam-table-tempomat-aus-rev-low-byte-bit4) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_LOW_BYTE_BIT3](#table-msd8asam-table-tempomat-aus-rev-low-byte-bit3) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_LOW_BYTE_BIT2](#table-msd8asam-table-tempomat-aus-rev-low-byte-bit2) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_LOW_BYTE_BIT1](#table-msd8asam-table-tempomat-aus-rev-low-byte-bit1) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_LOW_BYTE_BIT0](#table-msd8asam-table-tempomat-aus-rev-low-byte-bit0) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT7](#table-msd8asam-table-tempomat-aus-rev-high-byte-bit7) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT6](#table-msd8asam-table-tempomat-aus-rev-high-byte-bit6) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT5](#table-msd8asam-table-tempomat-aus-rev-high-byte-bit5) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT4](#table-msd8asam-table-tempomat-aus-rev-high-byte-bit4) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT3](#table-msd8asam-table-tempomat-aus-rev-high-byte-bit3) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT2](#table-msd8asam-table-tempomat-aus-rev-high-byte-bit2) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT1](#table-msd8asam-table-tempomat-aus-rev-high-byte-bit1) (2 × 2)
- [_MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT0](#table-msd8asam-table-tempomat-aus-rev-high-byte-bit0) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_BIT7](#table-msd8asam-table-switch-position-bit7) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_BIT4](#table-msd8asam-table-switch-position-bit4) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_BIT3](#table-msd8asam-table-switch-position-bit3) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_BIT2](#table-msd8asam-table-switch-position-bit2) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_BIT1](#table-msd8asam-table-switch-position-bit1) (2 × 2)
- [_MSD8ASAM_TABLE_SWITCH_POSITION_BIT0](#table-msd8asam-table-switch-position-bit0) (2 × 2)
- [_MSD8ASAM_CNV_S_8_RANGE_STAT_19_CM](#table-msd8asam-cnv-s-8-range-stat-19-cm) (8 × 2)
- [_MSD8ASAM_CNV_S_2_DEF_BIT_UB_716_CM0X4](#table-msd8asam-cnv-s-2-def-bit-ub-716-cm0x4) (2 × 2)
- [_MSD8ASAM_CNV_S_4_RANGE_STAT_455_CM_4DC3200S](#table-msd8asam-cnv-s-4-range-stat-455-cm-4dc3200s) (4 × 2)
- [_MSD8ASAM_TABEL_STATUS_OBD_READINESS](#table-msd8asam-tabel-status-obd-readiness) (2 × 2)
- [_MSD8ASAM_TABEL_STATUS_OBD_MONITOR](#table-msd8asam-tabel-status-obd-monitor) (2 × 2)
- [_MSD8ASAM_TABLE_FS](#table-msd8asam-table-fs) (10 × 2)
- [_MSD8ASAM_CNV_S_13_STATE_DMTL_140_CM](#table-msd8asam-cnv-s-13-state-dmtl-140-cm) (13 × 2)
- [_MSD8ASAM_TABLE_ST_GENTEST](#table-msd8asam-table-st-gentest) (8 × 2)
- [_MSD8ASAM_TABLE_GENIUTEST_ERR_BIT0](#table-msd8asam-table-geniutest-err-bit0) (2 × 2)
- [_MSD8ASAM_TABLE_GENIUTEST_ERR_BIT1](#table-msd8asam-table-geniutest-err-bit1) (2 × 2)
- [_MSD8ASAM_TABLE_GENIUTEST_ERR_BIT2](#table-msd8asam-table-geniutest-err-bit2) (2 × 2)
- [_MSD8ASAM_TABLE_GENIUTEST_ERR_BIT3](#table-msd8asam-table-geniutest-err-bit3) (2 × 2)
- [_MSD8ASAM_TABLE_GENIUTEST_ERR_BIT4](#table-msd8asam-table-geniutest-err-bit4) (2 × 2)
- [_MSD8ASAM_TABLE_GENIUTEST_ERR_BIT5](#table-msd8asam-table-geniutest-err-bit5) (2 × 2)
- [_MSD8ASAM_TABLE_GENIUTEST_ERR_BIT6](#table-msd8asam-table-geniutest-err-bit6) (2 × 2)
- [_MSD8ASAM_TABLE_GENIUTEST_ERR_BIT7](#table-msd8asam-table-geniutest-err-bit7) (2 × 2)
- [_MSD8ASAM_TABLE_GENIUTEST_AB_BIT0](#table-msd8asam-table-geniutest-ab-bit0) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT7](#table-msd8asam-table-glf-high-byte-bit7) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT6](#table-msd8asam-table-glf-high-byte-bit6) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT5](#table-msd8asam-table-glf-high-byte-bit5) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT4](#table-msd8asam-table-glf-high-byte-bit4) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT3](#table-msd8asam-table-glf-high-byte-bit3) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT2](#table-msd8asam-table-glf-high-byte-bit2) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT1](#table-msd8asam-table-glf-high-byte-bit1) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT0](#table-msd8asam-table-glf-high-byte-bit0) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT7](#table-msd8asam-table-glf-low-byte-bit7) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT6](#table-msd8asam-table-glf-low-byte-bit6) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT5](#table-msd8asam-table-glf-low-byte-bit5) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT4](#table-msd8asam-table-glf-low-byte-bit4) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT3](#table-msd8asam-table-glf-low-byte-bit3) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT2](#table-msd8asam-table-glf-low-byte-bit2) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT1](#table-msd8asam-table-glf-low-byte-bit1) (2 × 2)
- [_MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT0](#table-msd8asam-table-glf-low-byte-bit0) (2 × 2)
- [_MSD8ASAM_CNV_S_14_STATE_VLS__226_CM_4DC3200S](#table-msd8asam-cnv-s-14-state-vls-226-cm-4dc3200s) (14 × 2)
- [_MSD8ASAM_TABLE_ST_TESTPOELSYS](#table-msd8asam-table-st-testpoelsys) (8 × 2)
- [_MSD8ASAM_TABLE_ST_TESTPOELSYS2](#table-msd8asam-table-st-testpoelsys2) (7 × 2)
- [_MSD8ASAM_CNV_S_6_STATE_DIAG_157_CM](#table-msd8asam-cnv-s-6-state-diag-157-cm) (6 × 2)
- [_MSD8ASAM_CNV_S_8_RANGE_STAT_18_CM](#table-msd8asam-cnv-s-8-range-stat-18-cm) (8 × 2)

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
| 0x20 | Fehler momentan nicht vorhanden, nicht OBD-entprellt |
| 0x21 | Fehler momentan nicht vorhanden, OBD-entprellt |
| 0x22 | Fehler momentan vorhanden, noch nicht OBD-entprellt |
| 0x23 | Fehler momentan vorhanden, OBD-entprellt |
| 0x30 | Fehler verursacht kein Aufleuchten der Warnlampe (MIL) |
| 0x31 | Fehler wuerde das Aufleuchten der Warnlampe (MIL) verursachen |
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

<a id="table-messwertemode"></a>
### MESSWERTEMODE

Dimensions: 14 rows × 3 columns

| TEXT | WERT | KOMMENTAR |
| --- | --- | --- |
| ein | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| aus | 0 | Argument ARG.   Messwertblock nur lesen |
| ja | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| nein | 0 | Argument ARG.   Messwertblock nur lesen |
| yes | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| no | 0 | Argument ARG.   Messwertblock nur lesen |
| on | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| off | 0 | Argument ARG.   Messwertblock nur lesen |
| 1 | 1 | Argument ARG.   Messwertblock im SG löschen, neu schreiben und lesen |
| 0 | 0 | Argument ARG.   Messwertblock nur lesen |
| 3 | 3 | Argument ID.    Messwertblock im SG löschen, neu schreiben und lesen |
| 2 | 2 | Argument ID.    Messwertblock nur lesen |
| 5 | 5 | Argument LABEL. Messwertblock im SG löschen, neu schreiben und lesen |
| 4 | 4 | Argument LABEL. Messwertblock nur lesen |

<a id="table-cbskennung"></a>
### CBSKENNUNG

Dimensions: 16 rows × 3 columns

| NR | CBS_K | CBS_K_TEXT |
| --- | --- | --- |
| 0x01 | Oel | Motoroel |
| 0x02 | Br_v | Bremsbelag vorne |
| 0x03 | Brfl | Bremsfluessigkeit |
| 0x04 | Filt | Mikrofilter |
| 0x06 | Br_h | Bremsbelag hinten |
| 0x07 | CSF | Dieselpartikelfilter |
| 0x08 | Batt | Batterie |
| 0x09 | VTG | Verteilergetriebeoel |
| 0x10 | ZKrz | Zuendkerzen |
| 0x11 | Sic | Sichtpruefung/Fahrzeug-Check |
| 0x12 | Kfl | Kuehlfluessigkeit |
| 0x13 | H2 | H2-Check |
| 0x14 | Ueb | Uebergabedurchsicht |
| 0x16 | DAD | Additiv fuer Partikelfilter |
| 0x20 | TUV | §Fahrzeuguntersuchung |
| 0x21 | AU | §Abgasuntersuchung |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

<a id="table-sg-diagnosekonzept"></a>
### SG_DIAGNOSEKONZEPT

Dimensions: 3 rows × 2 columns

| RANG | KONZEPT_TEXT |
| --- | --- |
| 1 | BMW-FAST |
| 2 | KWP2000* |
| 3 | KWP2000 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 374 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x0000 | 0000 FehlerOrt nicht bedatet |
| 0x29CC | 29CC Verbrennungsaussetzer, mehrere Zylinder |
| 0x29CD | 29CD Verbrennungsaussetzer, Zylinder 1 |
| 0x29CE | 29CE Verbrennungsaussetzer, Zylinder 2 |
| 0x29CF | 29CF Verbrennungsaussetzer, Zylinder 3 |
| 0x29D0 | 29D0 Verbrennungsaussetzer, Zylinder 4 |
| 0x29D1 | 29D1 Verbrennungsaussetzer, Zylinder 5 |
| 0x29D2 | 29D2 Verbrennungsaussetzer, Zylinder 6 |
| 0x29D9 | 29D9 Verbrennungsaussetzer bei geringem Tankfüllstand |
| 0x29DA | 29DA Kurbelwellensensor, Segmentadaption |
| 0x29DB | 29DB Laufruhe, Segmentzeitmessung |
| 0x29DC | 29DC Zylindereinspritzabschaltung |
| 0x29E0 | 29E0 Gemischregelung |
| 0x29E1 | 29E1 Gemischregelung 2 |
| 0x29E2 | 29E2 Kraftstoffeinspritzleiste, Drucksensorsignal |
| 0x29E5 | 29E5 Gemischadaption, oberer Drehzahlbereich |
| 0x29E6 | 29E6 Gemischadaption 2, oberer Drehzahlbereich |
| 0x29F1 | 29F1 Kraftstoffdruck, Plausibilität |
| 0x29F2 | 29F2 Kraftstoffhochdrucksystem, Kraftstoffdruck |
| 0x29F3 | 29F3 Kraftstoffdrucksensor, elektrisch |
| 0x29F4 | 29F4 Katalysatorkonvertierung |
| 0x29F5 | 29F5 Katalysatorkonvertierung 2 |
| 0x2A0C | 2A0C Abgasrückführungsventilstellung, Plausibilität (vorläufig) |
| 0x2A0D | 2A0D Abgasrückführungsventil, Ansteuerung |
| 0x2A0E | 2A0E Abgasrückführungsventil, Regelabweichung Lageregelung |
| 0x2A0F | 2A0F Abgasrückführungsventil, Adaption |
| 0x2A10 | 2A10 Abgasrückführungssensor, Signal |
| 0x2A12 | 2A12 DMTL-Magnetventil, Ansteuerung |
| 0x2A13 | 2A13 DMTL-Leckdiagnosepumpe, Ansteuerung |
| 0x2A15 | 2A15 DMTL, Feinleck |
| 0x2A16 | 2A16 DMTL, Feinstleck |
| 0x2A17 | 2A17 DMTL, Systemfehler |
| 0x2A18 | 2A18 DMTL, Heizung: Ansteuerung |
| 0x2A19 | 2A19 Tankentlüftungsventil, Ansteuerung |
| 0x2A1A | 2A1A Tankentlüftungssystem, Funktion |
| 0x2A1B | 2A1B Tankdeckel |
| 0x2A1C | 2A1C Tankfüllstand, Plausibilität |
| 0x2A26 | 2A26 Katalysator, Konvertierung im Schichtbetrieb |
| 0x2A27 | 2A27 Katalysator 2, Konvertierung im Schichtbetrieb |
| 0x2A2B | 2A2B Gemischregelung, Lambda |
| 0x2A2C | 2A2C Gemischregelung 2, Lambda |
| 0x2A2D | 2A2D Kraftstoffniederdrucksystem, Kraftstoffdruck |
| 0x2A80 | 2A80 Einlass-VANOS, Ansteuerung |
| 0x2A82 | 2A82 Einlass-VANOS |
| 0x2A85 | 2A85 Auslass-VANOS, Ansteuerung |
| 0x2A87 | 2A87 Auslass-VANOS, Mechanik |
| 0x2A94 | 2A94 Kurbelwellensensor, Signal |
| 0x2A95 | 2A95 Kurbelwellensensor, Synchronisation |
| 0x2A96 | 2A96 Kurbelwellensensor, Zahnfehler |
| 0x2A97 | 2A97 Kurbelwellensensor, Lückenfehler |
| 0x2A98 | 2A98 Kurbelwelle - Einlassnockenwelle, Korrelation |
| 0x2A99 | 2A99 Kurbelwelle - Auslassnockenwelle, Korrelation |
| 0x2A9A | 2A9A Nockenwellensensor Einlass, Signal |
| 0x2A9B | 2A9B Nockenwellensensor Auslass, Signal |
| 0x2A9E | 2A9E Nockenwellensensor Einlass, Synchonisation |
| 0x2A9F | 2A9F Nockenwellensensor Auslass, Synchronisation |
| 0x2AA0 | 2AA0 Nockenwellensensor Einlass, Signal |
| 0x2AA1 | 2AA1 Nockenwellensensor Auslass, Signal |
| 0x2AA2 | 2AA2 Nockenwellensensor Einlass, Lückenverlust |
| 0x2AA3 | 2AA3 Nockenwellengeber Auslass, Lückenverlust |
| 0x2AA4 | 2AA4 Nockenwellensensor Einlass, Zahnfehler |
| 0x2AA5 | 2AA5 Nockenwellensensor Auslass, Zahnfehler |
| 0x2AA8 | 2AA8 Variable Sauganlage Stellmotor: Ansteuerung |
| 0x2AA9 | 2AA9 Variable Sauganlage Stellmotor 2: Ansteuerung |
| 0x2AAA | 2AAA Variable Sauganlage, Plausibilität |
| 0x2AAB | 2AAB Variable Sauganlage, Eigendiagnose |
| 0x2AAC | 2AAC Variable Sauganlage 2, Eigendiagnose |
| 0x2AAD | 2AAD Kraftstoffpumpe, Notabschaltung |
| 0x2AAE | 2AAE Kraftstoffpumpe |
| 0x2AAF | 2AAF Kraftstoffpumpe, Plausibilität |
| 0x2AB2 | 2AB2 DME, interner Fehler: RAM |
| 0x2AB3 | 2AB3 DME, interner Fehler: Checksumme |
| 0x2AB4 | 2AB4 DME, interner Fehler: RAM-Checksumme |
| 0x2AB5 | 2AB5 DME, interner Fehler: Klopfsensorbaustein |
| 0x2AB6 | 2AB6 DME, interner Fehler: Mehrfachendstufenbaustein |
| 0x2ABC | 2ABC Ladedrucksensor, elektrisch |
| 0x2ABD | 2ABD Ladedrucksensor, Nachlauf |
| 0x2AC6 | 2AC6 Taster Fahrdynamik-Control (SPORT-Taste), Signal |
| 0x2ACB | 2ACB DME-Hauptrelais, Ansteuerung |
| 0x2ACC | 2ACC DME-Hauptrelais, Schaltverzögerung |
| 0x2AD0 | 2AD0 Getriebesteuerung |
| 0x2ADF | 2ADF Leerlaufregelung, Drehzahl |
| 0x2AE0 | 2AE0 Leerlaufregelung bei Kaltstart, Plausibilität |
| 0x2AE4 | 2AE4 Motorentlüftungs-Heizungsrelais, Ansteuerung |
| 0x2AF0 | 2AF0 Stickoxidsensor, Heizung |
| 0x2AF2 | 2AF2 Stickoxidsensor, Lambda linear |
| 0x2AF4 | 2AF4 Stickoxidsensor, elektrisch |
| 0x2AF6 | 2AF6 Stickoxidsensor, Lambda binär |
| 0x2B00 | 2B00 Überdrehzahl, Magerbereich |
| 0x2C24 | 2C24 Lambdasonden vor Katalysator, vertauscht |
| 0x2C27 | 2C27 Lambdasonde vor Katalysator, Systemcheck |
| 0x2C28 | 2C28 Lambdasonde vor Katalysator 2, Systemcheck |
| 0x2C2B | 2C2B Lambdasonde vor Katalysator, Systemcheck |
| 0x2C2C | 2C2C Lambdasonde vor Katalysator 2, Systemcheck |
| 0x2C2D | 2C2D Lambdasonde vor Katalysator, Schubprüfung |
| 0x2C2E | 2C2E Lambdasonde vor Katalysator 2, Schubprüfung |
| 0x2C31 | 2C31 Lambdasonde vor Katalysator, Trimmregelung |
| 0x2C32 | 2C32 Lambdasonde vor Katalysator 2, Trimmregelung |
| 0x2C39 | 2C39 Lambdasonde vor Katalysator, Dynamik |
| 0x2C3A | 2C3A Lambdasonde vor Katalysator 2, Dynamik |
| 0x2C3B | 2C3B Lambdasonde vor Katalysator, nicht angesteckt |
| 0x2C3C | 2C3C Lambdasonde vor Katalysator 2, nicht angesteckt |
| 0x2C3D | 2C3D Lambdasonde vor Katalysator, Leitungsfehler |
| 0x2C3E | 2C3E Lambdasonde vor Katalysator 2, Leitungsfehler |
| 0x2C3F | 2C3F DME, interner Fehler: Lambdasonde, Auswertebaustein |
| 0x2C40 | 2C40 DME, interner Fehler: Lambdasonde 2, Auswertebaustein |
| 0x2C41 | 2C41 DME, interner Fehler: Lambdasonde |
| 0x2C42 | 2C42 DME, interner Fehler: Lambdasonde 2 |
| 0x2C6A | 2C6A Lambdasonden nach Katalysator, vertauscht |
| 0x2C6B | 2C6B Lambdasonde nach Katalysator, Systemcheck |
| 0x2C6C | 2C6C Lambdasonde nach Katalysator 2, Systemcheck |
| 0x2C6D | 2C6D Lambdasonde nach Katalysator, Alterung |
| 0x2C6E | 2C6E Lambdasonde nach Katalysator 2, Alterung |
| 0x2C73 | 2C73 Lambdasonde nach Katalysator, Signal |
| 0x2C74 | 2C74 Lambdasonde nach Katalysator 2, Signal |
| 0x2C75 | 2C75 Lambdasonde nach Katalysator, Signal |
| 0x2C76 | 2C76 Lambdasonde nach Katalysator 2, Signal |
| 0x2C77 | 2C77 Lambdasonde nach Katalysator, Signal |
| 0x2C78 | 2C78 Lambdasonde nach Katalysator 2, Signal |
| 0x2C7B | 2C7B Lambdasonde nach Katalysator, Signal |
| 0x2C7C | 2C7C Lambdasonde nach Katalysator 2, Signal |
| 0x2C7E | 2C7E Lambdasonde nach Katalysator, Trimmregelung |
| 0x2C7F | 2C7F Lambdasonde nach Katalysator 2, Trimmregelung |
| 0x2C87 | 2C87 Abgastemperatursensor, Signal |
| 0x2C9C | 2C9C Lambdasondenbeheizung vor Katalysator, Ansteuerung |
| 0x2C9D | 2C9D Lambdasondenbeheizung vor Katalysator 2, Ansteuerung |
| 0x2C9E | 2C9E Lambdasondenbeheizung nach Katalysator, Ansteuerung |
| 0x2C9F | 2C9F Lambdasondenbeheizung nach Katalysator 2, Ansteuerung |
| 0x2CA6 | 2CA6 Lambdasondenbeheizung vor Katalysator, Funktion |
| 0x2CA7 | 2CA7 Lambdasondenbeheizung vor Katalysator 2, Funktion |
| 0x2CA8 | 2CA8 Lambdasondenbeheizung nach Katalysator, Funktion |
| 0x2CA9 | 2CA9 Lambdasondenbeheizung nach Katalysator 2, Funktion |
| 0x2CAA | 2CAA Lambdasondenbeheizung vor Katalysator, Höchsttemperatur (vorläufig) |
| 0x2CAB | 2CAB Lambdasondenbeheizung vor Katalysator 2, Höchsttemperatur (vorläufig) |
| 0x2CEC | 2CEC Drosselklappensteller, klemmt kurzzeitig |
| 0x2CED | 2CED Drosselklappensteller, klemmt dauerhaft |
| 0x2CEE | 2CEE Drosselklappensteller, schwergängig |
| 0x2CEF | 2CEF Drosselklappensteller, Ansteuerung |
| 0x2CF6 | 2CF6 Drosselklappenpotenziometer 1, Plausibilität zu Luftmasse |
| 0x2CF7 | 2CF7 Drosselklappenpotenziometer 2, Plausibilität zu Luftmasse |
| 0x2CF9 | 2CF9 Drosselklappenpotenziometer 1 |
| 0x2CFA | 2CFA Drosselklappenpotenziometer 2 |
| 0x2CFB | 2CFB Drosselklappen-Adaptionswert |
| 0x2CFC | 2CFC Drosselklappe, Startprüfung |
| 0x2CFD | 2CFD Drosselklappen-Adaptionswert fehlt |
| 0x2CFE | 2CFE Drosselklappe, kontinuierliche Adaption |
| 0x2D06 | 2D06 Luftmassensystem |
| 0x2D0B | 2D0B Drosselklappenheizung, Relais |
| 0x2D0C | 2D0C Drosselklappe, Enteisung (vorläufig) |
| 0x2D0F | 2D0F Luftmassenmesser, Signal |
| 0x2D15 | 2D15 Luftmassenmesser, Plausibilität, Bereich |
| 0x2D16 | 2D16 Luftmassenmesser, Signal |
| 0x2D1B | 2D1B Fahrpedalmodul, Pedalwertgeber Signal 1 |
| 0x2D1C | 2D1C Fahrpedalmodul, Pedalwertgeber Signal 2 |
| 0x2D1D | 2D1D Fahrpedalmodul, Pedalwertgeber 1, Spannungsversorgung |
| 0x2D1E | 2D1E Fahrpedalmodul, Pedalwertgeber 2, Spannungsversorgung |
| 0x2D1F | 2D1F Fahrpedalmodul, Pedalwertgeber Potentiometer, Signal |
| 0x2D20 | 2D20 Fahrpedalmodul, Pedalwertgeber, Plausibilität zwischen Signal 1 und Signal 2 |
| 0x2D28 | 2D28 Differenzdrucksensor, Saugrohr: Signal |
| 0x2D29 | 2D29 Differenzdrucksensor, Saugrohr: Plausibilität |
| 0x2D2A | 2D2A Differenzdrucksensor, Saugrohr: Adaption |
| 0x2D2B | 2D2B Differenzdrucksensor, Nachlauf |
| 0x2D2E | 2D2E Drosselklappenwinkel, Plausibilität zu Saugrohr-Unterdruck |
| 0x2D50 | 2D50 DME, interner Fehler:  Überwachung Fahrgeschwindigkeitsregelung |
| 0x2D52 | 2D52 DME, interner Fehler: Überwachung Motordrehzahl |
| 0x2D53 | 2D53 DME, interner Fehler: Überwachung Drehzahlbegrenzung |
| 0x2D55 | 2D55 DME, interner Fehler: Überwachung Fahrpedalmodul |
| 0x2D56 | 2D56 DME, interner Fehler: Überwachung Leerlaufregelung |
| 0x2D57 | 2D57 DME, interner Fehler: Überwachung externe Momentenanforderung |
| 0x2D58 | 2D58 DME, interner Fehler: Überwachung Sollmoment |
| 0x2D59 | 2D59 DME, interner Fehler: Überwachung Istmoment |
| 0x2D5A | 2D5A Überwachung Motordrehmoment-Begrenzung |
| 0x2D5C | 2D5C DME, interner Fehler: Überwachung Hardware |
| 0x2D5F | 2D5F Reset |
| 0x2D60 | 2D60 DME, interner Fehler |
| 0x2D61 | 2D61 Drosselklappe, Überwachung (vorläufig) |
| 0x2D64 | 2D64 Überwachung stöchiometrisches Gemisch |
| 0x2D67 | 2D67 DME, interner Fehler: Überwachung Prozessoren |
| 0x2DBE | 2DBE Aktive Geschwindigkeitsregelung, gesperrt für Fahrzyklus |
| 0x2DC0 | 2DC0 Längsdynamikmanagement |
| 0x2DC3 | 2DC3 Überwachung Klemme 15 |
| 0x2DE1 | 2DE1 Tankfüllstandswert links, Plausibilität (vorlaüfig) |
| 0x2DE2 | 2DE2 Tankfüllstandswert rechts, Plausibilität (vorlaüfig) |
| 0x2DE3 | 2DE3 Botschaft von der Instrumentenkombination fehlt, I-Kombi 7 |
| 0x2DEB | 2DEB Powermanagement, Bordnetzüberwachung |
| 0x2DEC | 2DEC Powermanagement, Batterieüberwachung |
| 0x2DED | 2DED Powermanagement, Ruhestromüberwachung |
| 0x2E30 | 2E30 Einspritzventil Zylinder 1, Ansteuerung |
| 0x2E31 | 2E31 Einspritzventil Zylinder 2, Ansteuerung |
| 0x2E32 | 2E32 Einspritzventil Zylinder 3, Ansteuerung |
| 0x2E33 | 2E33 Einspritzventil Zylinder 4, Ansteuerung |
| 0x2E34 | 2E34 Einspritzventil Zylinder 5, Ansteuerung |
| 0x2E35 | 2E35 Einspritzventil Zylinder 6, Ansteuerung |
| 0x2E68 | 2E68 Klopfsensorsignal 1 |
| 0x2E69 | 2E69 Klopfsensorsignal 2 |
| 0x2E77 | 2E77 Zündung, Spannungsversorgung |
| 0x2E7C | 2E7C Bitserielle Datenschnittstelle, Signal |
| 0x2E81 | 2E81 Elektrische Kühlmittelpumpe, Drehzahlabweichung |
| 0x2E82 | 2E82 Elektrische Kühlmittelpumpe, Abschaltung |
| 0x2E83 | 2E83 Elektrische Kühlmittelpumpe, leistungsreduzierter Betrieb |
| 0x2E84 | 2E84 Elektrische Kühlmittelpumpe, Kommunikation |
| 0x2E85 | 2E85 Elektrische Kühlmittelpumpe, Kommunikation |
| 0x2E8B | 2E8B Intelligenter Batteriesensor, Signal |
| 0x2E8C | 2E8C Intelligenter Batteriesensor, Funktion |
| 0x2E8D | 2E8D Intelligenter Batteriesensor, Signalübertragung |
| 0x2E8E | 2E8E Intelligenter Batteriesensor, Kommunikation |
| 0x2E96 | 2E96 Generator, Untererregung |
| 0x2E97 | 2E97 Generator |
| 0x2E98 | 2E98 Generator, Kommunikation |
| 0x2E9F | 2E9F Ölzustandssensor |
| 0x2EA1 | 2EA1 Ölzustandssensor, Kommunikation |
| 0x2EAE | 2EAE Botschaft vom Stickoxidsensor 1 fehlt |
| 0x2EAF | 2EAF Botschaft vom Stickoxidsensor 2 fehlt |
| 0x2ECC | 2ECC Generator, Kommunikation |
| 0x2ECD | 2ECD Generator, elektrisch |
| 0x2ECE | 2ECE Generator,  Plausibilität: elektrisch |
| 0x2ECF | 2ECF Generator, Übertemperatur |
| 0x2ED0 | 2ED0 Generator,  Plausibilität: Temperatur |
| 0x2ED1 | 2ED1 Generator, mechanisch |
| 0x2ED2 | 2ED2 Generator, Regler falsch |
| 0x2ED3 | 2ED3 Generator, Typ falsch |
| 0x2EE0 | 2EE0 Kühlmitteltemperatursensor, Signal |
| 0x2EE1 | 2EE1 Kühlmitteltemperatursensor, Plausibilität |
| 0x2EE2 | 2EE2 Kühlmitteltemperatursensor, Plausibilität, Signal konstant |
| 0x2EE3 | 2EE3 Kühlmitteltemperatursensor, Plausibilität, Gradient |
| 0x2EE6 | 2EE6 Kühlmitteltemperatursensor, Messbereichsplausibilität (vorläufig) |
| 0x2EEA | 2EEA Temperatursensor Kühleraustritt, Signal |
| 0x2EEB | 2EEB Temperatursensor Kühleraustritt, Plausibilität, Gradient |
| 0x2EEC | 2EEC Temperatursensor Kühleraustritt, Plausibilität |
| 0x2EF4 | 2EF4 Kennfeldthermostat, Mechanik |
| 0x2EF5 | 2EF5 Kennfeldthermostat, Ansteuerung |
| 0x2EFE | 2EFE Elektrolüfter, Ansteuerung |
| 0x2EFF | 2EFF Elektrolüfter, Eigendiagnose |
| 0x2F08 | 2F08 Ansauglufttemperatursensor, Signal |
| 0x2F09 | 2F09 Ansauglufttemperatursensor, Plausibilität |
| 0x2F0A | 2F0A Ansauglufttemparatursensor Turbolader, Signal |
| 0x2F0D | 2F0D Kühlerjalousie, Ansteuerung, (GLF) |
| 0x2F0F | 2F0F Kühlerjalousie, unten |
| 0x2F10 | 2F10 Kühlerjalousie, unten |
| 0x2F11 | 2F11 Kühlerjalousie, oben |
| 0x2F12 | 2F12 Klimakompressor, Ansteuerung |
| 0x2F49 | 2F49 EWS Manipulationsschutz |
| 0x2F4A | 2F4A Schnittstelle EWS-DME |
| 0x2F4B | 2F4B DME, interner Fehler: EWS-Daten |
| 0x2F4C | 2F4C Botschaft EWS-DME fehlerhaft |
| 0x2F4E | 2F4E Fahrzeuggeschwindigkeit, Signal |
| 0x2F4F | 2F4F Fahrzeuggeschwindigkeit, Plausibilität |
| 0x2F58 | 2F58 Startautomatik, Ansteuerung |
| 0x2F63 | 2F63 Bremslichtschalter, Plausibilität |
| 0x2F64 | 2F64 Bremslichttestschalter, Plausibilität |
| 0x2F67 | 2F67 Kupplungsschalter, Signal |
| 0x2F6C | 2F6C Abgasklappe, Ansteuerung |
| 0x2F71 | 2F71 E-Box-Lüfter, Ansteuerung |
| 0x2F76 | 2F76 Umgebungsdrucksensor, Signal |
| 0x2F77 | 2F77 Umgebungsdrucksensor, Plausibilität |
| 0x2F79 | 2F79 Umgebungsdrucksensor, Nachlauf |
| 0x2F7B | 2F7B Öldruckschalter, Plausibilität |
| 0x2F80 | 2F80 Motorabstellzeit, Plausibilität |
| 0x2F85 | 2F85 DME, interner Fehler: Innentemperatursensor, Signal |
| 0x2F8F | 2F8F Fahrpedalmodul und Bremspedal, Plausibilität |
| 0x2F94 | 2F94 Kraftstoffpumpenrelais, Ansteuerung |
| 0x2F99 | 2F99 Umgebungstemperatursensor, Plausibilität |
| 0x2F9A | 2F9A Umgebungstemperatursensor, Kommunikation |
| 0x2F9E | 2F9E Thermischer Ölniveausensor |
| 0x2FA3 | 2FA3 Codierung fehlt |
| 0x2FA4 | 2FA4 Falscher Datensatz |
| 0x2FAB | 2FAB Aktives Motorlager, elektrisch |
| 0x2FAC | 2FAC Aktives Motorlager 2, elektrisch |
| 0x2FBC | 2FBC Kraftstoffdrucksteuerventil, Signal |
| 0x2FBD | 2FBD Kraftstoffdrucksteuerventil, Plausibilität |
| 0x2FBE | 2FBE Kraftstoffdruck nach Motorstop (vorläufig) |
| 0x2FBF | 2FBF Kraftstoffdruck nach Motorstart (vorläufig) |
| 0x2FC0 | 2FC0 Krafstoffdruckbereich (vorläufig) |
| 0x2FC6 | 2FC6 Energiesparmodus aktiv |
| 0x3070 | 3070 Zylindergleichstellung über Laufunruhe Zylinder 1 |
| 0x3071 | 3071 Zylindergleichstellung über Laufunruhe Zylinder 2 |
| 0x3072 | 3072 Zylindergleichstellung über Laufunruhe Zylinder 3 |
| 0x3073 | 3073 Zylindergleichstellung über Laufunruhe Zylinder 4 |
| 0x3074 | 3074 Zylindergleichstellung über Laufunruhe Zylinder 5 |
| 0x3075 | 3075 Zylindergleichstellung über Laufunruhe Zylinder 6 |
| 0x307C | 307C Zylindergleichstellung über Lambda Zylinder 1 |
| 0x307D | 307D Zylindergleichstellung über Lambda Zylinder 2 |
| 0x307E | 307E Zylindergleichstellung über Lambda Zylinder 3 |
| 0x307F | 307F Zylindergleichstellung über Lambda Zylinder 4 |
| 0x3080 | 3080 Zylindergleichstellung über Lambda Zylinder 5 |
| 0x3081 | 3081 Zylindergleichstellung über Lambda Zylinder 6 |
| 0x3088 | 3088 Zündspule Zylinder 1, Ansteuerung |
| 0x3089 | 3089 Zündspule Zylinder 2, Ansteuerung |
| 0x308A | 308A Zündspule Zylinder 3, Ansteuerung |
| 0x308B | 308B Zündspule Zylinder 4, Ansteuerung |
| 0x308C | 308C Zündspule Zylinder 5, Ansteuerung |
| 0x308D | 308D Zündspule Zylinder 6, Ansteuerung |
| 0x3094 | 3094 Zündspule Zylinder 1, Ansteuerung |
| 0x3095 | 3095 Zündspule Zylinder 2, Ansteuerung |
| 0x3096 | 3096 Zündspule Zylinder 3, Ansteuerung |
| 0x3097 | 3097 Zündspule Zylinder 4, Ansteuerung |
| 0x3098 | 3098 Zündspule Zylinder 5, Ansteuerung |
| 0x3099 | 3099 Zündspule Zylinder 6, Ansteuerung |
| 0x30A0 | 30A0 Zündspule Zylinder 1, Ansteuerung |
| 0x30A1 | 30A1 Zündspule Zylinder 2, Ansteuerung |
| 0x30A2 | 30A2 Zündspule Zylinder 3, Ansteuerung |
| 0x30A3 | 30A3 Zündspule Zylinder 4, Ansteuerung |
| 0x30A4 | 30A4 Zündspule Zylinder 5, Ansteuerung |
| 0x30A5 | 30A5 Zündspule Zylinder 6, Ansteuerung |
| 0x30AC | 30AC Einspritzventil Zylinder 1, Ansteuerung |
| 0x30AD | 30AD Einspritzventil Zylinder 2, Ansteuerung |
| 0x30AE | 30AE Einspritzventil Zylinder 3, Ansteuerung |
| 0x30AF | 30AF Einspritzventil Zylinder 4, Ansteuerung |
| 0x30B0 | 30B0 Einspritzventil Zylinder 5, Ansteuerung |
| 0x30B1 | 30B1 Einspritzventil Zylinder 6, Ansteuerung |
| 0x30BA | 30BA Einspritzventil, Leistungstufe (vorläufig) |
| 0x30BB | 30BB Einspritzventil, Leistungstufe 2 (vorläufig) |
| 0x30C0 | 30C0 Motoröldruckregelung, dynamisch |
| 0x30C1 | 30C1 Motoröldruckregelung, statisch |
| 0x30C2 | 30C2 Ölpumpe, Ansteuerung |
| 0x30C3 | 30C3 Motoröldrucksensor, Signal |
| 0x30C4 | 30C4 Motoröldruckregelung, mechanisch |
| 0x30C5 | 30C5 Motorölpumpe, mechanisch: Motoröldruck |
| 0x30C6 | 30C6 Motoröldrucksensor, Plausibilität |
| 0x30C7 | 30C7 Motoröldrucksystem |
| 0x30CA | 30CA Umluftklappe, Ansteuerung |
| 0x30CF | 30CF Wastegate, Ansteuerung |
| 0x30D0 | 30D0 Wastegate 2, Ansteuerung |
| 0x30D6 | 30D6 Stickoxidsensor, Plausibilität |
| 0x30D8 | 30D8 Stickoxidsenor, Sensorvergiftung |
| 0x30DA | 30DA Stickoxidsenor, Aufheizzeit |
| 0x30DC | 30DC Stickoxidsenor, Beheizung |
| 0x30DE | 30DE NOX Sensor, Plausibilität, Signal vor dem VOR KAT (Breitbandsonde) und nach UB-Kat (NOx Sensor) |
| 0x30E0 | 30E0 Stickoxidsensor, Offset |
| 0x30E2 | 30E2 Stickoxidsensor, Schubprüfung |
| 0x30E4 | 30E4 Stickoxidsensor, Alterung |
| 0x30E6 | 30E6 Stickoxidsensor, Dynamik |
| 0x30E9 | 30E9 Stickoxidkatalysator, Alterung |
| 0x30FD | 30FD Abgasturbolader, Differenzdruck |
| 0x30FE | 30FE Abgasturbolader, Hochdruckseite |
| 0x30FF | 30FF Abgasturbolader, Niederdruckseite |
| 0x3100 | 3100 Ladedruckregelung, Abschaltung |
| 0xCD8B | CD8B Local-CAN Kommunikationsfehler |
| 0xCD94 | CD94 Botschaft (Außentemperatur/Relativzeit, 310) |
| 0xCD95 | CD95 Botschaft (Bedienung Tempomat/ACC, 194) |
| 0xCD96 | CD96 Botschaft (Drehmomentanforderung ACC, B7) |
| 0xCD97 | CD97 Botschaft (Drehmomentanforderung AFS, B9) |
| 0xCD98 | CD98 Botschaft (Drehmomentanforderung DSC, B6) |
| 0xCD99 | CD99 Botschaft (Drehmomentanforderung EGS, B5) |
| 0xCD9A | CD9A Botschaft (Drehmomentanforderung SMG, BD) |
| 0xCD9B | CD9B Botschaft (Fahrzeugmodus, 315) |
| 0xCD9C | CD9C Botschaft (Geschwindigkeit, 1A0) |
| 0xCD9D | CD9D Botschaft (Getriebedaten, BA) |
| 0xCD9E | CD9E Botschaft (Getriebedaten 2, 1A2) |
| 0xCD9F | CD9F Botschaft (Kilometerstand/Reichweite, 330) |
| 0xCDA0 | CDA0 Botschaft (Klemmenstatus, 130) |
| 0xCDA1 | CDA1 Botschaft (Lenkradwinkel, C4) |
| 0xCDA2 | CDA2 Botschaft (Powermanagement Batteriespannung, 3B4) |
| 0xCDA3 | CDA3 Botschaft (Powermanagement Ladespannung, 334) |
| 0xCDA4 | CDA4 Botschaft (Status ARS-Modul, 1AC) |
| 0xCDA5 | CDA5 Botschaft (Status DSC, 19E) |
| 0xCDA6 | CDA6 Botschaft (Status Elektrische Kraftstoffpumpe, 335) |
| 0xCDA7 | CDA7 Botschaft (Status Rückwärtsgang, 3B0) |
| 0xCDA8 | CDA8 Botschaft (Status KOMBI, 1B4) |
| 0xCDA9 | CDA9 Botschaft (Wärmestrom/Lastmoment Klima, 1B5) |
| 0xCDAA | CDAA Botschaft (Status Crashabschaltung EKP, 135) |
| 0xCDAB | CDAB Botschaft (Lampenzustand,  21A) |
| 0xCDAC | CDAC Botschaft (Status Wasserventil,  3B5) |
| 0xCDAD | CDAD Botschaft (Anforderung Radmoment Antriebstrang,  BF) |
| 0xCDAE | CDAE Botschaft (Uhrzeit/Datum, 2F8) |
| 0xCDAF | CDAF Botschaft (Status Anhänger, 2E4) |
| 0xCDB0 | CDB0 Botschaft (Anzeige Getriebedaten) |
| 0xCDB1 | CDB1 Botschaft (Status Zentralveriegelung, 2FC) |
| 0xCDB3 | CDB3 Botschaft (Drehmomentanforderung Lenkung, B1h) |
| 0xCDB4 | CDB4 Botschaft (Getriebedaten, 3B1) |
| 0xCDB5 | CDB5 PT-CAN Kommunikationsfehler |
| 0xCDB9 | CDB9 Botschaft (Status EMF, 201) |
| 0xCDBA | CDBA Botschaft (Stellanforderung EMF, 1A7) |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 7 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_ART_IND | ja |
| F_ART_ERW | 00654301 |
| F_PCODE | ja |
| F_PCODE7 | nein |
| F_HFK | ja |
| F_LZ | ja |
| F_UWB_ERW | ja |

<a id="table-farttexteerweitert"></a>
### FARTTEXTEERWEITERT

Dimensions: 11 rows × 3 columns

| ARTMASKE | ARTNR | ARTTEXT |
| --- | --- | --- |
| xxxxxxx0 | 10 | Diagnose läuft nicht |
| xxxxxxx1 | 11 | Diagnose läuft |
| xxxxx0xx | 30 | Zyklus-Flag nicht gesetzt |
| xxxxx1xx | 31 | Zyklus-Flag gesetzt |
| xxxx0xxx | 40 | kein Fehler durch Tester |
| xxxx1xxx | 41 | Fehler durch Tester |
| xxx0xxxx | 50 | MIL aus |
| xxx1xxxx | 51 | MIL ein |
| xx0xxxxx | 60 | Fehler in Entprellphase |
| xx1xxxxx | 61 | Fehler entprellt, keine Scan Tool Ausgabe |
| xxxxxxxx | 0 | -- |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 352 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x0000 | 0x58FF | 0x58FF | 0x58FF | 0x58FF |
| 0x29CC | 0x5824 | 0x58F0 | 0x583C | 0x58E4 |
| 0x29CD | 0x581F | 0x58E5 | 0x5811 | 0x5806 |
| 0x29CE | 0x581F | 0x58E5 | 0x5811 | 0x5806 |
| 0x29CF | 0x581F | 0x58E5 | 0x5811 | 0x5806 |
| 0x29D0 | 0x581F | 0x58E5 | 0x5811 | 0x5806 |
| 0x29D1 | 0x581F | 0x58E5 | 0x5811 | 0x5806 |
| 0x29D2 | 0x581F | 0x58E5 | 0x5811 | 0x5806 |
| 0x29D9 | 0x58F3 | 0x586D | 0x5834 | 0x583B |
| 0x29DA | 0x5811 | 0x583C | 0x58F8 | 0x58F9 |
| 0x29DB | 0x5811 | 0x581F | 0x5818 | 0x583C |
| 0x29DC | 0x581F | 0x5818 | 0x5811 | 0x583B |
| 0x29E0 | 0x581F | 0x5818 | 0x5811 | 0x5855 |
| 0x29E1 | 0x581F | 0x5818 | 0x5811 | 0x5856 |
| 0x29E2 | 0x5811 | 0x58F0 | 0x58F4 | 0x583B |
| 0x29F1 | 0x58F0 | 0x58F2 | 0x583C | 0x58F3 |
| 0x29F2 | 0x5811 | 0x58F0 | 0x58F2 | 0x5832 |
| 0x29F3 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x29F4 | 0x5811 | 0x5818 | 0x581F | 0x581E |
| 0x29F5 | 0x5811 | 0x5818 | 0x581F | 0x581E |
| 0x2A0D | 0x58EC | 0x58F7 | 0x583C | 0x587C |
| 0x2A0E | 0x58EC | 0x58F7 | 0x583C | 0x587C |
| 0x2A0F | 0x58EC | 0x58F7 | 0x583C | 0x587C |
| 0x2A10 | 0x58EC | 0x58F7 | 0x583C | 0x587C |
| 0x2A12 | 0x5834 | 0x5874 | 0x587C | 0x583C |
| 0x2A13 | 0x5834 | 0x5874 | 0x587C | 0x583C |
| 0x2A15 | 0x583B | 0x5859 | 0x585A | 0x588D |
| 0x2A16 | 0x583B | 0x5859 | 0x585B | 0x588D |
| 0x2A17 | 0x583B | 0x5859 | 0x5867 | 0x5824 |
| 0x2A18 | 0x5834 | 0x5874 | 0x587C | 0x583C |
| 0x2A19 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A1A | 0x581F | 0x5818 | 0x5811 | 0x584D |
| 0x2A1B | 0x583B | 0x5859 | 0x585B | 0x588D |
| 0x2A1C | 0x580D | 0x5815 | 0x583B | 0x5867 |
| 0x2A26 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x2A27 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x2A2D | 0x5811 | 0x58EA | 0x5832 | 0x5804 |
| 0x2A80 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A82 | 0x5811 | 0x581A | 0x581B | 0x581F |
| 0x2A85 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A87 | 0x5811 | 0x581C | 0x581D | 0x581F |
| 0x2A94 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A95 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A96 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A97 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A98 | 0x5811 | 0x5832 | 0x5822 | 0x583C |
| 0x2A99 | 0x5811 | 0x5832 | 0x5822 | 0x583C |
| 0x2A9A | 0x5811 | 0x5832 | 0x5822 | 0x583C |
| 0x2A9B | 0x5811 | 0x5832 | 0x5822 | 0x583C |
| 0x2A9E | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2A9F | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2AA0 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2AA1 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2AA2 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2AA3 | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2AA4 | 0x5811 | 0x5832 | 0x5822 | 0x583C |
| 0x2AA5 | 0x5811 | 0x5832 | 0x5822 | 0x583C |
| 0x2AA8 | 0x5811 | 0x580D | 0x583C | 0x587C |
| 0x2AA9 | 0x5811 | 0x580D | 0x583C | 0x587C |
| 0x2AAA | 0x5811 | 0x581F | 0x5832 | 0x587C |
| 0x2AAB | 0x583C | 0x580C | 0x5818 | 0x5824 |
| 0x2AAC | 0x583C | 0x580C | 0x5818 | 0x5824 |
| 0x2AAD | 0x5832 | 0x583C | 0x587C | 0x58AF |
| 0x2AAE | 0x5832 | 0x583C | 0x587C | 0x58AF |
| 0x2AAF | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x2AB2 | 0x5811 | 0x5821 | 0x587C | 0x583C |
| 0x2AB3 | 0x5811 | 0x5821 | 0x587C | 0x583C |
| 0x2AB4 | 0x5811 | 0x5821 | 0x587C | 0x583C |
| 0x2AB5 | 0x5811 | 0x5821 | 0x587C | 0x583C |
| 0x2AB6 | 0x5811 | 0x5821 | 0x587C | 0x583C |
| 0x2ABC | 0x5811 | 0x58DD | 0x5858 | 0x587C |
| 0x2ABD | 0x5834 | 0x580B | 0x58DD | 0x5811 |
| 0x2AC6 | 0x5811 | 0x580D | 0x583C | 0x587C |
| 0x2ACB | 0x588B | 0x584A | 0x587C | 0x583C |
| 0x2ACC | 0x5843 | 0x584A | 0x587C | 0x583C |
| 0x2AD0 | 0x5832 | 0x5881 | 0x587C | 0x583C |
| 0x2ADF | 0x5811 | 0x5812 | 0x5813 | 0x5814 |
| 0x2AE0 | 0x5811 | 0x5812 | 0x5882 | 0x5815 |
| 0x2AE4 | 0x5824 | 0x583A | 0x588B | 0x587C |
| 0x2C24 | 0x5805 | 0x588B | 0x5845 | 0x5848 |
| 0x2C27 | 0x588C | 0x5849 | 0x5871 | 0x5845 |
| 0x2C28 | 0x588F | 0x584B | 0x5873 | 0x5848 |
| 0x2C2B | 0x588C | 0x5849 | 0x5871 | 0x5845 |
| 0x2C2C | 0x588F | 0x584B | 0x5873 | 0x5848 |
| 0x2C2D | 0x580B | 0x5845 | 0x587D | 0x588C |
| 0x2C2E | 0x580B | 0x5848 | 0x587E | 0x588F |
| 0x2C31 | 0x5849 | 0x5845 | 0x5878 | 0x58F5 |
| 0x2C32 | 0x584B | 0x5848 | 0x5879 | 0x58F6 |
| 0x2C39 | 0x582E | 0x5845 | 0x5830 | 0x588C |
| 0x2C3A | 0x582F | 0x5848 | 0x5831 | 0x588F |
| 0x2C3B | 0x588B | 0x5849 | 0x5845 | 0x588C |
| 0x2C3C | 0x588B | 0x584B | 0x5848 | 0x588F |
| 0x2C3D | 0x5871 | 0x589B | 0x5845 | 0x588C |
| 0x2C3E | 0x5873 | 0x589C | 0x5848 | 0x588F |
| 0x2C3F | 0x5837 | 0x5815 | 0x5845 | 0x5827 |
| 0x2C40 | 0x5838 | 0x5815 | 0x5848 | 0x5828 |
| 0x2C41 | 0x589B | 0x582C | 0x5845 | 0x5815 |
| 0x2C42 | 0x589C | 0x582D | 0x5848 | 0x5815 |
| 0x2C6A | 0x581F | 0x588B | 0x5849 | 0x584B |
| 0x2C6B | 0x5845 | 0x585C | 0x5811 | 0x5849 |
| 0x2C6C | 0x5848 | 0x585D | 0x5811 | 0x584B |
| 0x2C6D | 0x5896 | 0x585C | 0x5811 | 0x5849 |
| 0x2C6E | 0x5897 | 0x585D | 0x5811 | 0x584B |
| 0x2C73 | 0x5896 | 0x585C | 0x5849 | 0x588B |
| 0x2C74 | 0x5897 | 0x585D | 0x584B | 0x588B |
| 0x2C75 | 0x5896 | 0x585C | 0x5849 | 0x588B |
| 0x2C76 | 0x5897 | 0x585D | 0x584B | 0x588B |
| 0x2C77 | 0x5896 | 0x585C | 0x5849 | 0x588B |
| 0x2C78 | 0x5897 | 0x585D | 0x584B | 0x588B |
| 0x2C7B | 0x5896 | 0x585C | 0x5849 | 0x5845 |
| 0x2C7C | 0x5897 | 0x585D | 0x584B | 0x5848 |
| 0x2C7E | 0x5849 | 0x5845 | 0x5878 | 0x58F5 |
| 0x2C7F | 0x584B | 0x5848 | 0x5879 | 0x58F6 |
| 0x2C87 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x2C9C | 0x588C | 0x588B | 0x5815 | 0x5827 |
| 0x2C9D | 0x588F | 0x588B | 0x5815 | 0x5828 |
| 0x2C9E | 0x5896 | 0x585C | 0x5849 | 0x5829 |
| 0x2C9F | 0x5897 | 0x585D | 0x584B | 0x582A |
| 0x2CA6 | 0x5894 | 0x5815 | 0x5827 | 0x588C |
| 0x2CA7 | 0x5895 | 0x5815 | 0x5828 | 0x588F |
| 0x2CA8 | 0x5896 | 0x585C | 0x5829 | 0x5849 |
| 0x2CA9 | 0x5897 | 0x585D | 0x582A | 0x584B |
| 0x2CEC | 0x5858 | 0x583F | 0x5843 | 0x583C |
| 0x2CED | 0x5858 | 0x583F | 0x5843 | 0x583C |
| 0x2CEE | 0x5858 | 0x583F | 0x5843 | 0x583C |
| 0x2CEF | 0x5858 | 0x583F | 0x587C | 0x583C |
| 0x2CF6 | 0x58AB | 0x58E4 | 0x584C | 0x584E |
| 0x2CF7 | 0x58AC | 0x58E4 | 0x584C | 0x584E |
| 0x2CF9 | 0x584E | 0x584C | 0x5843 | 0x583C |
| 0x2CFA | 0x584E | 0x584C | 0x5843 | 0x583C |
| 0x2CFB | 0x584E | 0x584C | 0x58B0 | 0x583C |
| 0x2CFC | 0x584E | 0x584C | 0x5843 | 0x583C |
| 0x2CFD | 0x584E | 0x584C | 0x5843 | 0x583C |
| 0x2CFE | 0x584E | 0x584C | 0x5843 | 0x583C |
| 0x2D06 | 0x5811 | 0x58FF | 0x5899 | 0x5812 |
| 0x2D0B | 0x588B | 0x580C | 0x583C | 0x587C |
| 0x2D0F | 0x584F | 0x5811 | 0x5858 | 0x581E |
| 0x2D15 | 0x5812 | 0x5818 | 0x580C | 0x580F |
| 0x2D16 | 0x5812 | 0x5818 | 0x580C | 0x580F |
| 0x2D1B | 0x5846 | 0x5847 | 0x5843 | 0x583C |
| 0x2D1C | 0x5846 | 0x5847 | 0x5854 | 0x583C |
| 0x2D1D | 0x5843 | 0x5854 | 0x5846 | 0x583C |
| 0x2D1E | 0x5843 | 0x5854 | 0x5847 | 0x583C |
| 0x2D1F | 0x5843 | 0x5854 | 0x5846 | 0x5847 |
| 0x2D20 | 0x5846 | 0x5847 | 0x5843 | 0x5814 |
| 0x2D28 | 0x580B | 0x5811 | 0x581F | 0x587C |
| 0x2D29 | 0x5811 | 0x5826 | 0x580B | 0x5812 |
| 0x2D2A | 0x581E | 0x581F | 0x5820 | 0x583C |
| 0x2D2B | 0x5834 | 0x580B | 0x58DD | 0x5811 |
| 0x2D50 | 0x58B8 | 0x580D | 0x58B7 | 0x5881 |
| 0x2D52 | 0x58B8 | 0x58C0 | 0x58C1 | 0x5832 |
| 0x2D53 | 0x58B8 | 0x58B9 | 0x587C | 0x5839 |
| 0x2D55 | 0x58B8 | 0x5814 | 0x5846 | 0x5847 |
| 0x2D56 | 0x58C7 | 0x58C8 | 0x58C9 | 0x58CA |
| 0x2D57 | 0x58BF | 0x5881 | 0x5893 | 0x583C |
| 0x2D58 | 0x58D4 | 0x58D6 | 0x58CD | 0x5832 |
| 0x2D59 | 0x58B8 | 0x5832 | 0x58CF | 0x58D0 |
| 0x2D5A | 0x5811 | 0x5832 | 0x58CF | 0x58D1 |
| 0x2D5C | 0x58B8 | 0x5847 | 0x5854 | 0x583C |
| 0x2D5F | 0x5867 | 0x583D | 0x583E | 0x5840 |
| 0x2D64 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x2D67 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x2DBE | 0x580D | 0x5811 | 0x5832 | 0x587C |
| 0x2DC0 | 0x5811 | 0x5813 | 0x5832 | 0x5891 |
| 0x2DC3 | 0x5811 | 0x5832 | 0x583C | 0x587C |
| 0x2DEB | 0x5811 | 0x586A | 0x5898 | 0x583C |
| 0x2DEC | 0x5868 | 0x5869 | 0x586A | 0x58A8 |
| 0x2DED | 0x586B | 0x586C | 0x586E | 0x583C |
| 0x2E30 | 0x5811 | 0x581F | 0x5832 | 0x583C |
| 0x2E31 | 0x5811 | 0x581F | 0x5832 | 0x583C |
| 0x2E32 | 0x5811 | 0x581F | 0x5832 | 0x583C |
| 0x2E33 | 0x5811 | 0x581F | 0x5832 | 0x583C |
| 0x2E34 | 0x5811 | 0x581F | 0x5832 | 0x583C |
| 0x2E35 | 0x5811 | 0x581F | 0x5832 | 0x583C |
| 0x2E68 | 0x5811 | 0x5812 | 0x5883 | 0x5885 |
| 0x2E69 | 0x5811 | 0x5812 | 0x5886 | 0x5888 |
| 0x2E77 | 0x580D | 0x583C | 0x5811 | 0x5832 |
| 0x2E7C | 0x5811 | 0x583C | 0x5867 | 0x587C |
| 0x2E81 | 0x5805 | 0x58E9 | 0x58EA | 0x58EB |
| 0x2E82 | 0x5805 | 0x58E9 | 0x58EC | 0x58ED |
| 0x2E83 | 0x5805 | 0x58E9 | 0x58EC | 0x58EE |
| 0x2E84 | 0x5811 | 0x5805 | 0x587C | 0x583C |
| 0x2E85 | 0x5811 | 0x5805 | 0x587C | 0x583C |
| 0x2E8B | 0x587C | 0x5824 | 0x586A | 0x583C |
| 0x2E8C | 0x587C | 0x5824 | 0x586A | 0x583C |
| 0x2E8D | 0x587C | 0x5824 | 0x586A | 0x583C |
| 0x2E8E | 0x587C | 0x5824 | 0x586A | 0x583C |
| 0x2E96 | 0x588B | 0x5832 | 0x587C | 0x583C |
| 0x2E97 | 0x5898 | 0x5815 | 0x5887 | 0x5844 |
| 0x2E98 | 0x588B | 0x5815 | 0x5835 | 0x5842 |
| 0x2E9F | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2EA1 | 0x5811 | 0x580D | 0x583C | 0x587C |
| 0x2EAE | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x2EAF | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x2ECC | 0x588B | 0x5835 | 0x5842 | 0x5815 |
| 0x2ECD | 0x5884 | 0x5887 | 0x5898 | 0x5815 |
| 0x2ECE | 0x5884 | 0x5887 | 0x5898 | 0x5815 |
| 0x2ECF | 0x5844 | 0x5884 | 0x5887 | 0x580D |
| 0x2ED0 | 0x5844 | 0x5884 | 0x5887 | 0x580D |
| 0x2ED1 | 0x588B | 0x5887 | 0x5898 | 0x5815 |
| 0x2ED2 | 0x5872 | 0x5835 | 0x5842 | 0x5815 |
| 0x2ED3 | 0x588B | 0x5835 | 0x5842 | 0x5815 |
| 0x2EE0 | 0x5850 | 0x581F | 0x5824 | 0x581E |
| 0x2EE1 | 0x581F | 0x5820 | 0x583C | 0x58EC |
| 0x2EE2 | 0x581F | 0x5820 | 0x5824 | 0x5882 |
| 0x2EE3 | 0x581F | 0x5820 | 0x5824 | 0x587F |
| 0x2EE6 | 0x5823 | 0x5882 | 0x583A | 0x5833 |
| 0x2EEA | 0x5852 | 0x5820 | 0x5824 | 0x581E |
| 0x2EEB | 0x5820 | 0x581F | 0x5824 | 0x58EA |
| 0x2EEC | 0x5820 | 0x5882 | 0x581F | 0x5832 |
| 0x2EF4 | 0x5824 | 0x5882 | 0x5820 | 0x5811 |
| 0x2EF5 | 0x581F | 0x5820 | 0x5832 | 0x583C |
| 0x2EFE | 0x5820 | 0x587F | 0x5832 | 0x583C |
| 0x2EFF | 0x5824 | 0x587F | 0x583C | 0x5820 |
| 0x2F08 | 0x5851 | 0x581E | 0x5824 | 0x583C |
| 0x2F09 | 0x581E | 0x583A | 0x5824 | 0x581F |
| 0x2F0A | 0x5851 | 0x581E | 0x5824 | 0x58D5 |
| 0x2F0D | 0x5811 | 0x580D | 0x583C | 0x5880 |
| 0x2F0F | 0x5824 | 0x580D | 0x583C | 0x5880 |
| 0x2F10 | 0x583C | 0x5824 | 0x5880 | 0x580D |
| 0x2F11 | 0x583C | 0x5824 | 0x5880 | 0x580D |
| 0x2F12 | 0x5811 | 0x580D | 0x581F | 0x583C |
| 0x2F49 | 0x5811 | 0x586A | 0x587C | 0x5821 |
| 0x2F4A | 0x5811 | 0x586A | 0x587C | 0x5821 |
| 0x2F4B | 0x5811 | 0x586A | 0x587C | 0x5821 |
| 0x2F4C | 0x5811 | 0x586A | 0x587C | 0x5821 |
| 0x2F4E | 0x5811 | 0x5832 | 0x583C | 0x5881 |
| 0x2F4F | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2F58 | 0x588B | 0x584A | 0x5853 | 0x583C |
| 0x2F63 | 0x58CE | 0x58B7 | 0x587C | 0x584A |
| 0x2F64 | 0x58CE | 0x58B7 | 0x587C | 0x584A |
| 0x2F67 | 0x5811 | 0x580D | 0x5832 | 0x5818 |
| 0x2F6C | 0x580D | 0x588B | 0x58AD | 0x583C |
| 0x2F71 | 0x5811 | 0x581E | 0x5821 | 0x580D |
| 0x2F76 | 0x5821 | 0x5834 | 0x5870 | 0x587C |
| 0x2F77 | 0x5834 | 0x5870 | 0x5833 | 0x5824 |
| 0x2F79 | 0x5834 | 0x580B | 0x58DD | 0x5811 |
| 0x2F7B | 0x5811 | 0x5822 | 0x581F | 0x583C |
| 0x2F80 | 0x58A8 | 0x5805 | 0x587C | 0x583C |
| 0x2F85 | 0x5841 | 0x5821 | 0x5824 | 0x583C |
| 0x2F8F | 0x58B7 | 0x580D | 0x5814 | 0x58CE |
| 0x2F94 | 0x5811 | 0x580D | 0x581F | 0x583C |
| 0x2F99 | 0x5824 | 0x5833 | 0x5882 | 0x5820 |
| 0x2F9A | 0x5824 | 0x5833 | 0x581E | 0x587C |
| 0x2F9E | 0x5811 | 0x5832 | 0x587C | 0x583C |
| 0x2FA3 | 0x5811 | 0x583C | 0x587C | 0x588B |
| 0x2FA4 | 0x5811 | 0x583C | 0x587C | 0x588B |
| 0x2FAB | 0x588B | 0x580C | 0x583C | 0x587C |
| 0x2FAC | 0x588B | 0x580C | 0x583C | 0x587C |
| 0x2FBC | 0x58F2 | 0x58F0 | 0x58E4 | 0x587C |
| 0x2FBD | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0x2FBE | 0x58F0 | 0x58F2 | 0x5811 | 0x5832 |
| 0x2FBF | 0x58F0 | 0x58F2 | 0x583C | 0x58F3 |
| 0x2FC0 | 0x58F0 | 0x5811 | 0x58F2 | 0x5804 |
| 0x2FC6 | 0x580D | 0x583C | 0x5811 | 0x5832 |
| 0x3070 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x3071 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x3072 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x3073 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x3074 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x3075 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x307C | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x307D | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x307E | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x307F | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x3080 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x3081 | 0x580D | 0x5811 | 0x583C | 0x587C |
| 0x3088 | 0x5811 | 0x5812 | 0x58B1 | 0x583C |
| 0x3089 | 0x5811 | 0x5812 | 0x58B5 | 0x583C |
| 0x308A | 0x5811 | 0x5812 | 0x58B3 | 0x583C |
| 0x308B | 0x5811 | 0x5812 | 0x58B6 | 0x583C |
| 0x308C | 0x5811 | 0x5812 | 0x58B2 | 0x583C |
| 0x308D | 0x5811 | 0x5812 | 0x58B4 | 0x583C |
| 0x3094 | 0x5811 | 0x5812 | 0x58B1 | 0x583C |
| 0x3095 | 0x5811 | 0x5812 | 0x58B5 | 0x583C |
| 0x3096 | 0x5811 | 0x5812 | 0x58B3 | 0x583C |
| 0x3097 | 0x5811 | 0x5812 | 0x58B6 | 0x583C |
| 0x3098 | 0x5811 | 0x5812 | 0x58B2 | 0x583C |
| 0x3099 | 0x5811 | 0x5812 | 0x58B4 | 0x583C |
| 0x30A0 | 0x5811 | 0x5812 | 0x58B1 | 0x583C |
| 0x30A1 | 0x5811 | 0x5812 | 0x58B5 | 0x583C |
| 0x30A2 | 0x5811 | 0x5812 | 0x58B3 | 0x583C |
| 0x30A3 | 0x5811 | 0x5812 | 0x58B6 | 0x583C |
| 0x30A4 | 0x5811 | 0x5812 | 0x58B2 | 0x583C |
| 0x30A5 | 0x5811 | 0x5812 | 0x58B4 | 0x583C |
| 0x30AC | 0x5801 | 0x580B | 0x5803 | 0x5807 |
| 0x30AD | 0x5801 | 0x580B | 0x5803 | 0x5807 |
| 0x30AE | 0x5801 | 0x580B | 0x5803 | 0x5807 |
| 0x30AF | 0x5801 | 0x580B | 0x5803 | 0x5807 |
| 0x30B0 | 0x5801 | 0x580B | 0x5803 | 0x5807 |
| 0x30B1 | 0x5801 | 0x580B | 0x5803 | 0x5807 |
| 0x30C0 | 0x586F | 0x5862 | 0x5822 | 0x5811 |
| 0x30C1 | 0x586F | 0x5862 | 0x5822 | 0x5811 |
| 0x30C2 | 0x5811 | 0x5822 | 0x586F | 0x583C |
| 0x30C3 | 0x586F | 0x5822 | 0x580D | 0x5811 |
| 0x30C4 | 0x586F | 0x5822 | 0x5811 | 0x586A |
| 0x30C5 | 0x586F | 0x5862 | 0x5822 | 0x5811 |
| 0x30C6 | 0x586F | 0x5834 | 0x5822 | 0x5811 |
| 0x30C7 | 0x586F | 0x5862 | 0x5822 | 0x5811 |
| 0x30CA | 0x5801 | 0x580B | 0x5803 | 0x5807 |
| 0x30CF | 0x5811 | 0x581F | 0x583C | 0x587C |
| 0x30D0 | 0x5811 | 0x581F | 0x583C | 0x587C |
| 0x30D6 | 0x58DB | 0x58DC | 0x5811 | 0x58D8 |
| 0x30D8 | 0x58D9 | 0x58DA | 0x5811 | 0x58D8 |
| 0x30DA | 0x58DB | 0x58DC | 0x5811 | 0x58D8 |
| 0x30DC | 0x58DB | 0x58DC | 0x5811 | 0x5800 |
| 0x30DE | 0x5845 | 0x5848 | 0x5811 | 0x58D8 |
| 0x30E0 | 0x58D6 | 0x58D7 | 0x5811 | 0x58D8 |
| 0x30E2 | 0x58D6 | 0x58D7 | 0x5811 | 0x58D8 |
| 0x30E4 | 0x58D9 | 0x58DA | 0x5811 | 0x58D8 |
| 0x30E6 | 0x58DA | 0x58DC | 0x5811 | 0x58D8 |
| 0x30FD | 0x5834 | 0x5824 | 0x58DD | 0x580C |
| 0x30FE | 0x5834 | 0x5824 | 0x58DD | 0x580C |
| 0x30FF | 0x5834 | 0x5824 | 0x58DD | 0x580C |
| 0x3100 | 0x5834 | 0x5824 | 0x58DD | 0x580C |
| 0xCD8B | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCD94 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCD95 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCD96 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCD97 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCD98 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCD99 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCD9A | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCD9B | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCD9C | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCD9D | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCD9E | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCD9F | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDA0 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDA1 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDA2 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDA3 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDA4 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDA5 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDA6 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDA7 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDA8 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDA9 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDAA | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDAB | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDAC | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDAD | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDAE | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDAF | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDB0 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDB1 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDB3 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDB4 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDB5 | 0x5811 | 0x5832 | 0x583C | 0x587C |
| 0xCDB9 | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xCDBA | 0x5811 | 0x5821 | 0x583C | 0x587C |
| 0xFFFF | 0x58FF | 0x58FF | 0x58FF | 0x58FF |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 640 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x4200 | Ansauglufttemperatur 1 | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x4201 | Umgebungsdruck | hPa | - | unsigned integer | - | 0,0829175263643265 | 1 | 0,0 |
| 0x4202 | Saugrohrdruck | hPa | - | unsigned integer | - | 0,0829175263643265 | 1 | 0,0 |
| 0x4203 | Massenstrom vom HFM | kg/h | - | unsigned integer | - | 0,03125 | 1 | 0,0 |
| 0x4204 | Umgebungstemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x4205 | Saugrohrdruck 1 / Ladedruck 1 | hPa | - | unsigned integer | - | 0,0829175263643265 | 1 | 0,0 |
| 0x4300 | Kühlwassertemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x4301 | Kühlerauslasstemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x4302 | Wasserpumpe Leistung über BSD | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4303 | Wasserpumpe Elektronik Temperatur | °C | - | unsigned char | - | 1,0 | 1 | -50,0 |
| 0x4304 | Wasserpumpe Strom | A | - | unsigned char | - | 0,5 | 1 | 0,0 |
| 0x4305 | Wasserpumpe Drehzahl Ist | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4306 | Wasserpumpe Drehzahl Soll | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4307 | Wasserpumpe Betriebsart | 0-n | - | 0xFF | _CNV_S_11_Def_ba_wm_614 | 1 | 1 | 0 |
| 0x4400 | Ölstand Mittelwert Langzeit | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x4401 | Füllstand Motoröl | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4402 | Öltemperatur | °C | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x4403 | Kraftstoff-Verbrauch seit letztem Service | - | - | unsigned long | - | 1,220703125E-4 | 1 | 0,0 |
| 0x4404 | km seit letztem Service | km | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| 0x4405 | Ölsensor Niveau Rohwert | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4406 | Ölsensor Qualität Rohwert | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4407 | Ölsensor Temperatur Rohwert | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4408 | Ölsensor Temperatur | °C | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x4409 | Ölsensor Niveau | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x440A | Ölsensor Qualität | - | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| 0x440B | Länderfaktor 1 codiert | - | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| 0x440C | Länderfaktor 2 codiert | - | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| 0x440D | Länderfaktor 1 | - | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| 0x440E | Länderfaktor 2 | - | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| 0x440F | Kurzmittelwert-Niveau für den Tester | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x4410 | Restweg aus Permittivität abgeleitet | km | - | signed integer | - | 10,0 | 1 | 0,0 |
| 0x4411 | Restweg aus Kraftstoffverbrauch abgeleitet | km | - | signed integer | - | 10,0 | 1 | 0,0 |
| 0x4412 | Öl-Alter in Monate | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4413 | aufbereitete Permittivität bei letztem Ölwechsel | - | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| 0x4414 | Permittivität für Bewertung aufbereitet (extrapoliert) | - | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| 0x4415 | Offset für Permittivitätskorrektur | - | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| 0x4416 | zugeteilte Bonuskraftstoffmenge | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4417 | zugeteilter Permittivitätsbonus | - | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| 0x4418 | Status Peilstabanzeige | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4505 | Sollwert Einlassspreizung | °CRK | - | unsigned char | - | 0,375 | 1 | 59,9999982118607 |
| 0x4506 | Nockenwellenposition Einlass | °CRK | - | unsigned integer | - | 0,375 | 1 | -95,9999971389771 |
| 0x4507 | Nockenwellenposition Auslass | °CRK | - | unsigned integer | - | 0,375 | 1 | -95,9999971389771 |
| 0x4508 | Istwert Einlassspreizung | °CRK | - | unsigned char | - | 0,375 | 1 | 59,9999982118607 |
| 0x4509 | Istwert Auslassspreizung | °CRK | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| 0x450A | Normspreizung Auslass | °CRK | - | signed integer | - | 0,0234375 | 1 | 0,0 |
| 0x450B | Normspreizung Einlass | °CRK | - | signed integer | - | 0,0234375 | 1 | 0,0 |
| 0x4600 | aktueller Drosselklappenwinkel | °TPS | - | unsigned integer | - | 0,00729414634406567 | 1 | 0,0 |
| 0x4601 | Drosselklappe Sollwert aus Modell | °TPS | - | unsigned integer | - | 0,00729414634406567 | 1 | 0,0 |
| 0x4602 | Generator Sollspannung über BSD | V | - | unsigned char | - | 0,100000001490116 | 1 | 10,6 |
| 0x4603 | Chiptemperatur Generator 1 | °C | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x4604 | Generator Strom | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4605 | Chipversion Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4606 | Reglerversion Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4607 | Herstellercode Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4608 | Kennung Generatortyp Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4609 | Kl.87 Spannung / Versorgung DME | V | - | unsigned char | - | 0,101562492549419 | 1 | 0,0 |
| 0x460A | Batteriespannung aktuell | V | - | unsigned integer | - | 0,0149999996647239 | 1 | 0,0 |
| 0x460B | Batteriespannung von IBS gemessen | - | - | unsigned integer | - | 2,50000011874363E-4 | 1 | 6,0 |
| 0x460C | Batteriespannung vom AD-Wandler DME | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x460D | Korrekturwert Abschaltung | - | - | signed integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x460E | Abstand zur Startfähigkeitsgrenze | - | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x460F | Batterielast | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4610 | aktuelle Position Disaklappen | % | - | unsigned integer | - | 0,00305175711400807 | 1 | 0,0 |
| 0x4611 | Sollwert E-Lüfter als PWM Wert | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4612 | Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x4613 | Kopierter Wert von zum Generator gesendeter Sollspannung Generator 1 | V | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x4614 | Auslastungsgrad Generator 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x4615 | Kopie begrenzter Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x4616 | Kopie Generator 1 LR Vorgabe auf Bus gelegt | s | - | unsigned char | - | 0,100000001490116 | 1 | 0,0 |
| 0x4617 | gefiltertes Generatormoment absolut Ausgang | Nm | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x4618 | Kopie Drehzahlschwelle für LR-Funktion Generator 1 aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4619 | Bedingung BSD II Protokoll | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x461A | Nominale Generatorspannung | V | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x4700 | Status Lambdasonde betriebsbereit vor Katalysator Bank 1 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4701 | Status Lambdasonde betriebsbereit vor Katalysator Bank 2 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4702 | Spannung Lambdasonde vor Katalysator Bank 1 mit Offsetkorrektur | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x4703 | Spannung Lambdasonde vor Katalysator Bank 2 mit Offsetkorrektur | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x4704 | Lambda Sollwert Bank 1 | - | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| 0x4705 | Lambda Sollwert Bank 2 | - | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| 0x4800 | Kupplungsschalter Status | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4801 | Kupplungsschalter vorhanden | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4802 | Sporttaster aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4803 | Status Klima ein | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x4805 | Startrelais über CAN aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x4806 | Steuergeräte-Innentemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x4807 | Motor Drehzahl | rpm | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4808 | Leerlauf Solldrehzahl | rpm | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x4809 | Status LL | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x480A | Kilometerstand Auflösung 1 km | km | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x480B | Pedalwert Fahrerwunsch in % | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5800 | Zeit nach Start | s | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x5801 | Umgebungsdruck | kPa | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5802 | Zustand Lambdaregelung Bank 1 | 0-n | - | 0xFF | _CNV_S_5_LACO_RANGE_410 | 1 | 1 | 0 |
| 0x5803 | Zustand Lambdaregelung Bank 2 | 0-n | - | 0xFF | _CNV_S_5_LACO_RANGE_410 | 1 | 1 | 0 |
| 0x5804 | Berechneter Lastwert | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5805 | Kühlmitteltemperatur OBD | °C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x5806 | Lambda Integrator Gruppe 1 | % | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| 0x5807 | Lambda Adaption Summe mul. und add. Gruppe 1 | % | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| 0x5808 | Lambda Integrator Gruppe 2 | % | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| 0x5809 | Lambda Adaption Summe mul. und add. Gruppe 2 | % | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| 0x580B | Saugrohrdruck | kPa | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x580C | Drehzahl | rpm | - | unsigned char | - | 64,0 | 1 | 0,0 |
| 0x580D | Geschwindigkeit | km/h | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x580E | Zündzeitpunkt Zylinder 1 | °CRK | - | unsigned char | - | 0,5 | 1 | -64,0 |
| 0x580F | Ansauglufttemperatur | °C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x5810 | Luftdurchsatz OBD | g/s | - | unsigned char | - | 2,5599999427795406 | 1 | 0,0 |
| 0x5811 | Motordrehzahl | rpm | - | unsigned char | - | 32,0 | 1 | 0,0 |
| 0x5812 | Luftmasse gemessen | kg/h | - | unsigned char | - | 8,0 | 1 | 0,0 |
| 0x5813 | Relative Last | % | - | signed char | - | 2,5599999427795406 | 1 | 0,0 |
| 0x5814 | Fahrpedalwert | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5815 | Batteriespannung | V | - | unsigned char | - | 0,2560000121593472 | 1 | 0,0 |
| 0x5816 | Lambda Setpoint | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x5817 | Umgebungstemperatur | °C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x5818 | Luftmasse gerechnet | mg/stk | - | unsigned char | - | 5,425863742828365 | 1 | 0,0 |
| 0x5819 | Drehzahl OBD Byte | rpm | - | unsigned char | - | 64,0 | 1 | 0,0 |
| 0x581A | Nockenwelle Einlass | °CRK | - | unsigned char | - | 0,375 | 1 | 59,9999982118607 |
| 0x581B | Nockenwelle Einlass Sollwert | °CRK | - | unsigned char | - | 0,375 | 1 | 59,9999982118607 |
| 0x581C | Nockenwelle Auslass | °CRK | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| 0x581D | Nockenwelle Auslass Sollwert | °CRK | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| 0x581E | Ansauglufttemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x581F | Motortemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5820 | Kühlmitteltemperatur Kühlerausgang | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5821 | Steuergeräte-Innentemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5822 | (Motor)-Öltemperatur | °C | - | unsigned char | - | 1,0 | 1 | -40,0 |
| 0x5823 | Zeit Motor steht | min | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x5824 | Umgebungstemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5825 | Abstellzeit | min | - | unsigned char | - | 4,0 | 1 | 0,0 |
| 0x5826 | Drosselklappe Sensor 1 | °TPS | - | unsigned char | - | 1,8673014640808114 | 1 | 0,0 |
| 0x5827 | Lambdasondenheizung vor Katalysator Bank 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5828 | Lambdasondenheizung vor Katalysator Bank 2 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5829 | Lambdasondenheizung hinter Katalysator Bank 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x582A | Lambdasondenheizung hinter Katalysator Bank 2 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x582B | Drehmomenteingriff über CAN | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x582C | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x582D | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 2 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x582E | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 1 | - | - | unsigned char | - | 0,25 | 1 | 0,0 |
| 0x582F | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 2 | - | - | unsigned char | - | 0,25 | 1 | 0,0 |
| 0x5830 | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 1 | - | - | unsigned char | - | 0,00400000018998981 | 1 | 0,0 |
| 0x5831 | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 2 | - | - | unsigned char | - | 0,00400000018998981 | 1 | 0,0 |
| 0x5832 | Motor Status | 0-n | - | 0xFF | _CNV_S_6_RANGE_STAT_167 | 1 | 1 | 0 |
| 0x5833 | Umgebungstemperatur beim Start | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5834 | Umgebungsdruck | hPa | - | unsigned char | - | 21,226886749267585 | 1 | 0,0 |
| 0x5835 | Herstellercode Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5836 | Drehzahlgradient | rpm/s | - | signed char | - | 32,0 | 1 | 0,0 |
| 0x5837 | Status OBD-I Fehler vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_11_EGCP_RANGE_375 | 1 | 1 | 0 |
| 0x5838 | Status OBD-I Fehler vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_11_EGCP_RANGE_375 | 1 | 1 | 0 |
| 0x5839 | Status Drosselklappe Notlauf | 0-n | - | 0xFF | _CNV_S_5_RANGE_STAT_290 | 1 | 1 | 0 |
| 0x583A | Ansauglufttemperatur beim Start | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x583B | Kraftstofftank Füllstand | l | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x583C | Spannung Kl. 87 | V | - | unsigned char | - | 0,101562492549419 | 1 | 0,0 |
| 0x583D | Resettyp | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x583E | Motordrehzahl bei Reset | rpm | - | unsigned char | - | 32,0 | 1 | 0,0 |
| 0x583F | Drosselklappe Sollwert | °TPS | - | unsigned char | - | 1,8673014640808114 | 1 | 0,0 |
| 0x5840 | CPU Last bei Reset | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5841 | SG-Innentemperatur Rohwert | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5842 | Kennung Generatortyp Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5843 | Versorgung Fahrtwertgeber 1 | V | - | unsigned char | - | 0,0390625037252903 | 1 | 0,0 |
| 0x5844 | Chiptemperatur Generator 1 | °C | - | unsigned char | - | 1,0 | 1 | -48,0 |
| 0x5845 | Spannung Lambdasonde vor Katalysator Bank 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5846 | Spannung Pedalwertgeber 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5847 | Spannung Pedalwertgeber 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5848 | Spannung Lambdasonde vor Katalysator Bank 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5849 | Spannung Lambdasonde hinter Katalysator Bank 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x584A | Spannung Kl. 15 Rohwert | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x584B | Spannung Lambdasonde hinter Katalysator Bank 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x584C | Spannung Drosselklappe Potentiometer 2 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x584D | korrigierter Sollwert Durchfluss Tankentlüftung | kg/h | - | unsigned char | - | 0,03125 | 1 | 0,0 |
| 0x584E | Spannung Drosselklappe Potentiometer 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x584F | Spannung Luftmasse | V | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| 0x5850 | Spannung Motortemperatur | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5851 | Spannung Ansauglufttemperatur | V | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| 0x5852 | Kühlmitteltemperatur Kühlerausgang Rohwert | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5853 | Spannung Kl.87 Rohwert | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5854 | Versorgung Fahrtwertgeber 2 | V | - | unsigned char | - | 0,0390625037252903 | 1 | 0,0 |
| 0x5855 | Mittelwert Bank 1 | % | - | signed char | - | 0,390625 | 1 | 2,22044609888115E-14 |
| 0x5856 | Mittelwert Bank 2 | % | - | signed char | - | 0,390625 | 1 | 2,22044609888115E-14 |
| 0x5857 | Erregerstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x5858 | Drosselklappe aktueller Wert | °TPS | - | unsigned char | - | 1,8673014640808114 | 1 | 0,0 |
| 0x5859 | DMTL Strom Referenzleck | mA | - | unsigned char | - | 0,195312470197678 | 1 | 0,0 |
| 0x585A | DMTL Strom Grobleck | mA | - | unsigned char | - | 0,195312470197678 | 1 | 0,0 |
| 0x585B | DMTL Strom Diagnoseende | mA | - | unsigned char | - | 0,195312470197678 | 1 | 0,0 |
| 0x585C | Widerstand Lambdasonde hinter Katalysator Bank 1 | ohm | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x585D | Widerstand Lambdasonde hinter Katalysator Bank 2 | ohm | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x585E | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 1 | ohm | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x585F | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 2 | ohm | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5860 | Widerstand Lambdasonde vor Katalysator Bank 1 | ohm | - | unsigned char | - | 64,0 | 1 | 0,0 |
| 0x5861 | Widerstand Lambdasonde vor Katalysator Bank 2 | ohm | - | unsigned char | - | 64,0 | 1 | 0,0 |
| 0x5862 | Öldruck Sollwert | hPa | - | unsigned char | - | 32,0 | 1 | 0,0 |
| 0x5863 | untere Byte Widerstand Lambdasonde vor Katalysator Bank 1 | ohm | - | unsigned char | - | 0,25 | 1 | 0,0 |
| 0x5864 | untere Byte Widerstand Lambdasonde vor Katalysator Bank 2 | ohm | - | unsigned char | - | 0,25 | 1 | 0,0 |
| 0x5865 | Ölstand Mittelwert Langzeit | - | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| 0x5866 | Füllstand Motoröl | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5867 | Kilometerstand | km | - | unsigned char | - | 2560,0 | 1 | 0,0 |
| 0x5868 | Status Standverbraucher registriert Teil 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5869 | Status Standverbraucher registriert Teil 2 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x586A | Batteriespannung von IBS gemessen | - | - | unsigned char | - | 0,06400000303983693 | 1 | 6,0 |
| 0x586B | Zeit mit Ruhestrom 80 - 200 mA | min | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| 0x586C | Zeit mit Ruhestrom 200 - 1000 mA | min | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| 0x586D | Zähler Erkennung schlechte Strasse | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x586E | Zeit mit Ruhestrom größer 1000 mA | min | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| 0x586F | Ist-Öldruck | hPa | - | unsigned char | - | 32,0 | 1 | 0,0 |
| 0x5870 | Spannung DME Umgebungsdruck | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5871 | Lambda-Sollwert Gruppe 1 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x5872 | Reglerversion Generator 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5873 | Lambda-Sollwert Gruppe 2 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x5874 | Spannung Strommessung DMTL | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5875 | Sollwert Motormoment | Nm | - | signed char | - | 2,0 | 1 | 0,0 |
| 0x5876 | Raildruck OBD (High Byte) | kPa | - | unsigned char | - | 2560,0 | 1 | 0,0 |
| 0x5877 | Raildruck OBD (Low Byte) | kPa | - | unsigned char | - | 10,0 | 1 | 0,0 |
| 0x5878 | Lambdaverschiebung Rückführregler 1 | - | - | signed char | - | 9,765625E-4 | 1 | 0,0 |
| 0x5879 | Lambdaverschiebung Rückführregler 2 | - | - | signed char | - | 9,765625E-4 | 1 | 0,0 |
| 0x587A | Status FGR | 0-n | - | 0xFF | _CNV_S_6_RANGE_STAT_106 | 1 | 1 | 0 |
| 0x587B | Abgleich Abgasrückführungsventilmodell (Faktor) | - | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x587C | Status Motorsteuerung | 0-n | - | 0xFF | _CNV_S_7_RANGE_ECU__165 | 1 | 1 | 0 |
| 0x587D | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_384 | 1 | 1 | 0 |
| 0x587E | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_384 | 1 | 1 | 0 |
| 0x587F | Tastverhältnis E-Lüfter | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5880 | Tastverhältnis Luftklappe | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5881 | berechneter Gang | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5882 | Motortemperatur beim Start | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5883 | Spannung Klopfwerte Zylinder 1 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5884 | Rückgelesener Erregergrenzstrom Generator 1 | A | - | unsigned char | - | 0,125 | 1 | 0,0 |
| 0x5885 | Spannung Klopfwerte Zylinder 3 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5886 | Spannung Klopfwerte Zylinder 6 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5887 | Auslastungsgrad Generator 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5888 | Spannung Klopfwerte Zylinder 4 | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x5889 | Lambda-Istwert Gruppe 1 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x588A | Lambda-Istwert Gruppe 2 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x588B | Zeit seit Startende | s | - | unsigned char | - | 25,600000381469695 | 1 | 0,0 |
| 0x588C | Keramiktemperatur Lambdasonde vor Katalysator Bank 1 | °C | - | signed char | - | 16,0 | 1 | 0,0 |
| 0x588D | aktuelle Zeit DMTL Leckmessung | s | - | unsigned char | - | 25,600000381469695 | 1 | 0,0 |
| 0x588E | Pumpenstrom bei DMTL Pumpenprüfung | mA | - | unsigned char | - | 1,5625238418579097 | 1 | 0,0 |
| 0x588F | Keramiktemperatur Lambdasonde vor Katalysator Bank 2 | °C | - | signed char | - | 16,0 | 1 | 0,0 |
| 0x5890 | Spannung Bremsunterdrucksensor | V | - | unsigned char | - | 0,0195312164723873 | 1 | 0,0 |
| 0x5891 | Momentanforderung an der Kupplung | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x5892 | Bremsunterdruck | hPa | - | unsigned char | - | 5,306640625 | 1 | 0,0 |
| 0x5893 | Drehmomentabfall schnell bei Gangwechsel | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x5894 | Symptom Lambdasondenheizung vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_377 | 1 | 1 | 0 |
| 0x5895 | Symptom Lambdasondenheizung vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_4_EGCP_RANGE_377 | 1 | 1 | 0 |
| 0x5896 | Abgastemperatur hinter Katalysator Bank 1 | °C | - | unsigned char | - | 16,0 | 1 | 0,0 |
| 0x5897 | Abgastemperatur hinter Katalysator Bank 2 | °C | - | unsigned char | - | 16,0 | 1 | 0,0 |
| 0x5898 | Generator Sollspannung | V | - | unsigned char | - | 0,100000001490116 | 1 | 0,0 |
| 0x5899 | Istwert DISA-Position | % | - | unsigned char | - | 0,7812498211860659 | 1 | 0,0 |
| 0x589A | Tastverhältnis Nullgangsensor | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x589B | Spannungsoffset Signalpfad CJ120 1 | V | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| 0x589C | Spannungsoffset Signalpfad CJ120 2 | V | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| 0x589D | Abweichung Lambdasonde zu Lambdamodellwert Überwachung | - | - | signed char | - | 0,0156249795109034 | 1 | -2,50980372710279E-6 |
| 0x58A8 | Motorabstellzeit | min | - | unsigned char | - | 4,0 | 1 | 0,0 |
| 0x58A9 | Resetzähler Rechnerüberwachung: alter Wert | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58AA | Fehlercode Rechnerüberwachung: alter Wert | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58AB | Abweichung DK-Potentiometer 1 und Modellwert | °TPS | - | unsigned char | - | 0,466825366020203 | 1 | 0,0 |
| 0x58AC | Abweichung DK-Potentiometer 2 und Modellwert | °TPS | - | unsigned char | - | 0,466825366020203 | 1 | 0,0 |
| 0x58AD | Pedalwertgeber 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58AE | Periodendauer Luftmasse | us | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x58AF | Kraftstoff Anforderung an Pumpe | l/h | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B0 | DK-Adaptionsschritt | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B1 | Funkenbrenndauer Zylinder 1 | ms | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| 0x58B2 | Funkenbrenndauer Zylinder 5 | ms | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| 0x58B3 | Funkenbrenndauer Zylinder 3 | ms | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| 0x58B4 | Funkenbrenndauer Zylinder 6 | ms | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| 0x58B5 | Funkenbrenndauer Zylinder 2 | ms | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| 0x58B6 | Funkenbrenndauer Zylinder 4 | ms | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| 0x58B7 | Bremsdruck | bar | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58B8 | Drehzahl Überwachung | rpm | - | unsigned char | - | 32,0 | 1 | 0,0 |
| 0x58B9 | Pedalwert Überwachung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58BA | eingespritze Kraftstoffmasse | l/h | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58BB | PWM Kraftstoffpumpe | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58BC | Luftmasse Überwachung | mg/stk | - | unsigned char | - | 5,44705867767334 | 1 | 0,0 |
| 0x58BF | relative Momentenforderung von MSR über CAN | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58C0 | Motordrehzahl Ersatzwert Überwachung | rpm | - | unsigned char | - | 32,0 | 1 | 0,0 |
| 0x58C1 | Laufunruhe Segmentzeit | µs | - | unsigned char | - | 256,0 | 1 | 0,0 |
| 0x58C2 | Statusbyte MFF-Monitoring | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58C3 | Statusbyte ISC-Monitoring | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58C4 | Statusbyte CRU-Monitoring | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58C5 | Drehzahl Überwachung (resetsicher) | rpm | - | unsigned char | - | 32,0 | 1 | 0,0 |
| 0x58C6 | Status Einspritzventile (resetsicher) | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58C7 | LL-Solldrehzahlabweichung Überwachung | rpm | - | signed char | - | 32,0 | 1 | 0,0 |
| 0x58C8 | I-Anteil Momentdifferenz Überwachung und Modell | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58C9 | I-Anteil LL passive Rampe aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x58CA | PD-Anteil langsam Leerlaufregelung | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58CB | PD-Anteil schnell Leerlaufregelung | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58CC | Verlustmoment Überwachung | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58CD | Verlustmomentabweichung Überwachung | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58CE | Carrierbyte Schalterstati | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58CF | Motormoment Sollwert Überwachung | Nm | - | unsigned char | - | 2,0 | 1 | 0,0 |
| 0x58D0 | Motormoment Istwert Überwachung | Nm | - | unsigned char | - | 2,0 | 1 | 0,0 |
| 0x58D1 | Moment aktueller Wert | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58D2 | Status Luftklappensystem High Byte | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58D3 | Status Luftklappensystem Low Byte | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58D4 | Abweichung maximales Moment an Kupplung Überwachung | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58D5 | Air temperature up turbo charger | °C | - | unsigned char | - | 1,0 | 1 | -48,0 |
| 0x58D6 | Abweichung minimales Moment an Kupplung Überwachung | Nm | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58D7 | Voltage for temperatur sensor up turbocharger | V | - | unsigned char | - | 0,012941176071763 | 1 | 0,0 |
| 0x58D8 | Catalyst temperature sensor raw acquisition | V | - | unsigned char | - | 0,012941176071763 | 1 | 0,0 |
| 0x58D9 | Fehlercode Rechnerüberwachung: aktueller Wert | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58DA | Resetzähler Rechnerüberwachung: aktueller Wert | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58DB | Inhalt Statusbyte 1 Drehzahlüberwachung (resetsicher) | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58DC | Inhalt Statusbyte 2 Drehzahlüberwachung (resetsicher) | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58DD | Pressure upstream the throttle (Turbo) | kPa | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58DE | Voltage of the intake manifold pressure sensor up throttle (for diagnosis) | V | - | unsigned char | - | 0,0195312164723873 | 1 | 0,0 |
| 0x58DF | Spannung Sportschalter | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x58E0 | Abgleich Drosselklappenmodell (Faktor) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x58E1 | Abgleich Drosselklappenmodell (Offset) | kg/h | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58E2 | Abgleich Einlassventilmodell (Faktor) | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x58E3 | Abgleich Einlassventilmodell (Offset) | kg/h | - | signed char | - | 8,0 | 1 | 0,0 |
| 0x58E4 | Betriebsart Istwert | 0-n | - | 0xFF | _CNV_S_5_Def_ba_gdi_609 | 1 | 1 | 0 |
| 0x58E5 | Lastwert für Aussetzererkennung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58E6 | Nulllastwert für Aussetzererkennung | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58E7 | Spannung Pedalwertgeber 1 Überwachung | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x58E8 | Spannung Pedalwertgeber 2 Überwachung | V | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| 0x58E9 | Wasserpumpe Spannung | V | - | unsigned char | - | 0,100000001490116 | 1 | 0,0 |
| 0x58EA | Wasserpumpe Drehzahl | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58EB | Wasserpumpe Drehzahl Soll-Ist-Differenz | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58EC | Wasserpumpe Temperatur Elektronik | °C | - | unsigned char | - | 1,0 | 1 | -50,0 |
| 0x58ED | Wasserpumpe Stromaufnahme | A | - | unsigned char | - | 0,5 | 1 | 0,0 |
| 0x58EE | Wasserpumpe leistungsreduziert | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58EF | Mean value of the acquired sensor voltage | V | - | unsigned char | - | 0,0195312164723873 | 1 | 0,0 |
| 0x58F0 | Fuel pressure | hPa | - | unsigned char | - | 1358,51770019531 | 1 | 0,0 |
| 0x58F1 | DME - Losnummer | 0-n | - | 0xFF | _CNV_S_11_RANGE_STAT_941 | 1 | 1 | 0 |
| 0x58F2 | PWM signal for the VCV | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58F3 | Fuel pressure EFP | hPa | - | unsigned char | - | 42,4537582397461 | 1 | 0,0 |
| 0x58F4 | Low fuel pressure EFP sensor raw acquisition | V | - | unsigned char | - | 0,0195312164723873 | 1 | 0,0 |
| 0x58F5 | Eingangssignal Rückführregler 1 | V | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| 0x58F6 | Eingangssignal Rückführregler 2 | V | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| 0x58F7 | Measured opening of the actuator valve | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58F8 | Segmentadaption Laufunruhe Zyl. 5 | %. | - | signed char | - | 0,06103530898690227 | 1 | 1,92095835817427E-5 |
| 0x58F9 | Segmentadaption Laufunruhe Zyl. 3 | %. | - | signed char | - | 0,06103530898690227 | 1 | 1,92095835817427E-5 |
| 0x58FA | Beladungsgrad Aktivkohlefilter TEV- Funktionstest | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x58FB | Zähler Drehzahlerhöhungen TEV- Funktionstest | cyc | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x58FC | Setpoint request after limitation for actuator position control | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x58FD | Finally duty cycle of digital actuator control | % | - | signed char | - | 0,78125 | 1 | 0,0 |
| 0x58FE | Zähler für Umschaltungen nach HOM durch Monitoring | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5A00 | Versorgung Fahrwertgeber 1 | V | - | unsigned integer | - | 0,00976559147238731 | 1 | 0,0 |
| 0x5A01 | Versorgung Fahrwertgeber 2 | V | - | unsigned integer | - | 0,00976559147238731 | 1 | 0,0 |
| 0x5A04 | Spannung Pedalwertgeber 1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A05 | Spannung Pedalwertgeber 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A06 | Spannung Drosselklappe Potentiometer 1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A07 | Spannung Drosselklappe Potentiometer 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A08 | Spannung Ansauglufttemperatur | V | - | unsigned integer | - | 1,52587876073085E-4 | 1 | 0,0 |
| 0x5A09 | Spannung Motortemperatur | V | - | unsigned integer | - | 1,52587876073085E-4 | 1 | 0,0 |
| 0x5A0A | Spannung Kühlmitteltemperatur Kühlerausgang | V | - | unsigned integer | - | 1,52587876073085E-4 | 1 | 0,0 |
| 0x5A0B | Spannung DME Umgebungsdruck | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A0C | Spannung Luftmasse | V | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| 0x5A0D | Spannung Sekundärluft | V | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| 0x5A0E | Spannung SG-Innentemperatur | V | - | unsigned integer | - | 1,52587876073085E-4 | 1 | 0,0 |
| 0x5A0F | Spannung Kl.15 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A10 | Spannung Kl15 | V | - | unsigned integer | - | 0,0280601158738136 | 1 | 0,0 |
| 0x5A11 | Spannung Lambdasonde vor Katalysator Bank 1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A12 | Spannung Lambdasonde vor Katalysator Bank 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A13 | Spannung Lambdasonde hinter Katalysator Bank 1 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A14 | Spannung Lambdasonde hinter Katalysator Bank 2 | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A17 | Spannung Strommessung DMTL | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5A18 | Spannung Abgastemperatursensor | V | - | unsigned integer | - | 1,52587876073085E-4 | 1 | 0,0 |
| 0x5A1F | Abgastemperatur | °C | - | unsigned integer | - | 0,015625 | 1 | 0,0 |
| 0x5A20 | Tastverhältnis Nullgangssensor | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A21 | Kühlmitteltemperatur Kühlerausgang | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5A22 | Steuergeräte-Innentemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5A23 | Sollwert Öldruck | hPa | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5A24 | Drosselklappe Sollwert | °TPS | - | unsigned integer | - | 0,00729414634406567 | 1 | 0,0 |
| 0x5A25 | Istwert Öldruck | hPa | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5A26 | Umgebungsdruck | hPa | - | unsigned integer | - | 0,0829175263643265 | 1 | 0,0 |
| 0x5A27 | Pedalwertgeber Potentiometer 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A28 | Pedalwertgeber Potentiometer 2 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A29 | Fahrpedalwert | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A2B | Temperatur vor Drosselklappe | °C | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| 0x5A2C | Druck vor Drosselklappe | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x5A2D | Druck nach Drosselklappe | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x5A2E | Kraftstoffniederdrucksensor | hPa | - | unsigned integer | - | 2,65336084365845 | 1 | 0,0 |
| 0x5A2F | Raildruck | hPa | - | unsigned integer | - | 5,30672168731689 | 1 | 0,0 |
| 0x5A30 | Laufunruhe Zylinder 1 | µs | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A31 | Laufunruhe Zylinder 2 | µs | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A32 | Laufunruhe Zylinder 3 | µs | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A33 | Laufunruhe Zylinder 4 | µs | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A34 | Laufunruhe Zylinder 5 | µs | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A35 | Laufunruhe Zylinder 6 | µs | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5A36 | Status Klopfen | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A37 | Spannung Klopfwerte Zylinder 1 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A38 | Spannung Klopfwerte Zylinder 2 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A39 | Spannung Klopfwerte Zylinder 3 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A3A | Spannung Klopfwerte Zylinder 4 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A3B | Spannung Klopfwerte Zylinder 5 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A3C | Spannung Klopfwerte Zylinder 6 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A3D | Klopfsignal Zylinder 1 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A3E | Klopfsignal Zylinder 1 relativ | - | - | unsigned integer | - | 1,52587890625E-5 | 1 | 0,0 |
| 0x5A3F | Klopfsignal Zylinder 6 | V | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| 0x5A40 | Klopfsignal Zylinder 6 relativ | - | - | unsigned integer | - | 1,52587890625E-5 | 1 | 0,0 |
| 0x5A49 | Zündwinkel Zylinder 1 | °CRK | - | unsigned char | - | 0,375 | 1 | -35,6249989382923 |
| 0x5A4B | Berechneter Lastwert | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A4C | Status Drosselklappenheizungsrelais | 0-n | - | 0xFF | _CNV_S_5_RANGE_STAT_971 | 1 | 1 | 0 |
| 0x5A4D | Drosselklappenheizung Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A4E | Klimakompressorrelais Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A50 | Lambdawert vor Katalysator Bank 1 | - | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| 0x5A51 | Lambdawert vor Katalysator Bank 2 | - | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| 0x5A52 | Status LS hinter Katalysator Bank 1 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A53 | Status LS hinter Katalysator Bank 2 | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A54 | Status LS Heizung hinter Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_7_EGCP_RANGE_357 | 1 | 1 | 0 |
| 0x5A55 | Status LS Heizung hinter Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_7_EGCP_RANGE_357 | 1 | 1 | 0 |
| 0x5A56 | Status LS Heizung vor Katalysator Bank 1 | 0-n | - | 0xFF | _CNV_S_7_EGCP_RANGE_357 | 1 | 1 | 0 |
| 0x5A57 | Status LS Heizung vor Katalysator Bank 2 | 0-n | - | 0xFF | _CNV_S_7_EGCP_RANGE_357 | 1 | 1 | 0 |
| 0x5A58 | Lambdasondenheizung PWM vor Katalysator Bank 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A59 | Lambdasondenheizung PWM hinter Katalysator Bank 1 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A5A | Lambdasondenheizung PWM vor Katalysator Bank 2 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A5B | Lambdasondenheizung PWM hinter Katalysator Bank 2 | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A5C | Aktive Fehlerrückmeldung DISA-Klappe 1 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5A5D | Schalthäufigkeitszähler DISA-Klappe 1 | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5A5E | Aktive Fehlerrückmeldung DISA-Klappe 2 | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5A5F | Schalthäufigkeitszähler DISA-Klappe 2 | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5A60 | Bremslichtschalter Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A61 | Bremslichttestschalter Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A62 | Öldruckschalter Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A63 | E-Box-Lüfter Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A64 | Motorlager weiche Dämpfung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A65 | Abgasklappe Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A66 | DMTL Pumpe Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A67 | DMTL Ventil Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A68 | DMTL Heizung Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A69 | MIL Lampe Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A6A | Lampe FGR Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A6B | Lampe Check Engine Ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A6C | Verbrauchskorrekturfaktor | - | - | signed char | - | 0,00100000004749745 | 1 | 0,0 |
| 0x5A6D | Status Taste FGR | 0-n | - | 0xFF | _CNV_S_8_RANGE_STAT_21 | 1 | 1 | 0 |
| 0x5A6E | Status für irreversible Abschaltbedingung | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5A6F | Status für reversible Abschaltbedingung | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5A70 | Soundklappe Zustand | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A71 | DISA1 PWM (große/obere Klappe) | % | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x5A72 | DISA2 PWM (kleine/untere Klappe) | % | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| 0x5A73 | Kurbelgehäuseentlüftungsheizung ein | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A74 | Beheizter Thermostat PWM | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A76 | Adaption Öffnungspunkt Tankentlüftungsventil | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A77 | Tankentlüftungsventil PWM | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A78 | Abgasklappe Ansteuerung | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A79 | E-Lüfter PWM | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5A7A | VANOS PWM Wert Einlass | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A7B | VANOS PWM Wert Auslass | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5A7F | Phase-Shift-Adaption Lambdasonde Bank 1 | °CRK | - | signed char | - | 6,0 | 1 | 0,0 |
| 0x5A80 | Phase-Shift-Adaption Lambdasonde Bank 2 | °CRK | - | signed char | - | 6,0 | 1 | 0,0 |
| 0x5A81 | Ausgang Lamdaregler Bank 1 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A82 | Ausgang Lamdaregler Bank 2 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A83 | Adaption Offset Lambda Bank 1 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5A84 | Adaption Offset Lambda Bank 2 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5A85 | Adaption Multiplikation Lambda Bank 1 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A86 | Adaption Multiplikation Lambda Bank 2 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A87 | Adaptionswert Trimregelung Bank 1 | - | - | signed integer | - | 6,103515625E-5 | 1 | 0,0 |
| 0x5A88 | Adaptionswert Trimregelung Bank 2 | - | - | signed integer | - | 6,103515625E-5 | 1 | 0,0 |
| 0x5A89 | multiplikative Gemischadaption hohe Last Bank 1 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A8A | multiplikative Gemischadaption hohe Last Bank 2 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A8B | multiplikative Gemischadaption niedrige Last Bank 1 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A8C | multiplikative Gemischadaption niedrige Last Bank 2 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5A8D | additive Gemischadaption Leerlauf Bank 1 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5A8E | additive Gemischadaption Leerlauf Bank 2 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5A8F | Adaption Schubabgleich Bank 1 | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5A90 | Adaption Schubabgleich Bank 2 | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5A91 | Katalysatordiagnosewert Bank1 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x5A92 | Katalysatordiagnosewert Bank 2 | - | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| 0x5A94 | Nockenwelle Auslass Sollwert | °CRK | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| 0x5A95 | Adaptionswert Nockenwelle Auslass | °CRK | - | unsigned char | - | 0,375 | 1 | -47,9999985694886 |
| 0x5A96 | Adaptionswert Nockenwelle Einlass | °CRK | - | unsigned char | - | 0,375 | 1 | -47,9999985694886 |
| 0x5A97 | Bedingung EVANOS im Anschlag beim letzten Abstellen | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5A99 | Kurbelwellen Adaption beendet | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5AA1 | Status Diagnose TEV | 0-n | - | 0xFF | _CNV_S_10_STATE_EOL__452 | 1 | 1 | 0 |
| 0x5AA2 | Status Diagnose DMTL | 0-n | - | 0xFF | _CNV_S_10_STATE_EOL__452 | 1 | 1 | 0 |
| 0x5AA3 | Status Diagnose Lambdasonden | 0-n | - | 0xFF | _CNV_S_10_STATE_EOL__452 | 1 | 1 | 0 |
| 0x5AA4 | Status Diagnose Leerlaufdrehzahlverstellung | 0-n | - | 0xFF | _CNV_S_10_STATE_EOL__452 | 1 | 1 | 0 |
| 0x5AA7 | Leckluftadaption Istwert | kg/h | - | signed integer | - | 0,03125 | 1 | 0,0 |
| 0x5AA8 | Status Luftklappensystem | - | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5AA9 | Tastverhältnis: Luftklappe | % | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| 0x5AAA | Tastverhältnis Öldruck-Regelventil | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AAB | Wastegate 1 PWM | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AAC | Wastegate 2 PWM | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AAD | Vorsteuerung Ladedruckregelung | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AAE | Reglerausgang und Vorsteuerung | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AAF | Adaptionswert von der Ladedruckregelung | - | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5AB0 | Solladedruck | hPa | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| 0x5AB1 | Geschwindigkeit | km/h | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AB2 | Periodendauer Luftmasse | µs | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5AB3 | Fahrstrecke mit MIL an | km | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5AB4 | Betriebsstundenzähler | h | - | unsigned long | - | 2,77777780866018E-5 | 1 | 0,0 |
| 0x5AB6 | Rohwert Ansauglufttemperatur 1 | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5AB7 | Rohwert Kühlwassertemperatur | °C | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| 0x5AB8 | Spannung Saugrohrdruck | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5AB9 | Spannung Sportschalter | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5ABA | Kraftstoffpumpe PWM | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5ABC | Luftmasse | kg/h | - | unsigned integer | - | 0,03125 | 1 | 0,0 |
| 0x5ABD | Starterrelais aktiv | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5AC2 | Info last available caller addresses (default 0) | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5AC6 | Sensorspannung AGR | V | - | unsigned integer | - | 0,00488269794732332 | 1 | 0,0 |
| 0x5AC7 | Hub des AGR-Tellerventils | % | - | unsigned integer | - | 0,0244140625 | 1 | 0,0 |
| 0x5AC8 | Adaptionswert oberer Anschlag (einmalig gelernt) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5AC9 | Adaptionswert unterer Anschlag (immer wieder neu gelernt) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5ACA | Adaptionswert unterer Anschlag (einmalig am Anfang gelernt, Uradaption) | V | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| 0x5ACB | Status des Erlernens der AGR-Adaption | 0-n | - | 0xFF | _CNV_S_6_ACRC_RANGE_871 | 1 | 1 | 0 |
| 0x5ACC | DME-Temperaturstatistik, Zähler 1 | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5ACD | DME-Temperaturstatistik, Zähler 2 | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5ACE | DME-Temperaturstatistik, Zähler 3 | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5ACF | DME-Temperaturstatistik, Zähler 4 | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5AD0 | DME-Temperaturstatistik, Zähler 5 | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5AD1 | DME-Temperaturstatistik, Zähler 6 | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5AD2 | DME-Temperaturstatistik, Zähler 7 | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5AD3 | DME-Temperaturstatistik, Zähler 8 | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5AD6 | Schubabschaltung | ppm | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5AD7 | Beladungsbetrieb NOx-Katalysator | ppm | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5AD8 | NOx-Konzentration | ppm | - | signed integer | - | 1,0 | 1 | 0,0 |
| 0x5AD9 | Lineares Lambdasignal NOx-Sensor | - | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| 0x5ADA | binäres Spannungssignal NOx-Sensor | mV | - | unsigned integer | - | 1,0 | 1 | -200,0 |
| 0x5ADB | Status NOx-Sensor | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5ADC | NOx-Sensor Error Byte | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5ADF | Taupunkterkennung für NOx-Sensor | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5AE0 | Status-byte: security info for atypical reset (reset-save memory) | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AE2 | Reset type of last reset | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AE3 | Background info for last reset valid | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AE4 | Additional reset info (cause) | - | - | unsigned long | - | 1,0 | 1 | 0,0 |
| 0x5AE5 | Mileage counter at reset | m | - | unsigned long | - | 100,0 | 1 | 0,0 |
| 0x5AE6 | Total runtime at reset | h | - | unsigned long | - | 2,77777780866018E-5 | 1 | 0,0 |
| 0x5AE7 | Max. CPU load from reset detection | % | - | unsigned integer | - | 0,09765625 | 1 | 0,0 |
| 0x5AE8 | Engine speed at max. cpu load from reset detection | rpm | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| 0x5AE9 | Security info | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AEA | Number of atypical warm-resets since last power-up (BSW) | - | - | unsigned char | - | 1,0 | 1 | 0,0 |
| 0x5AEB | Kühlmitteltemperatur &lt; 98°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEC | 98°C =&lt; Kühlmitteltemperatur =&lt; 112°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AED | 113°C =&lt; Kühlmitteltemperatur =&lt; 120°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEE | 121°C =&lt; Kühlmitteltemperatur =&lt; 125°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AEF | Kühlmitteltemperatur &gt; 125°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF0 | Motoröltemperatur &lt; 80°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF1 | 80°C =&lt; Motoröltemperatur =&lt; 110°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF2 | 110°C =&lt; Motoröltemperatur =&lt; 135°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF3 | 135°C =&lt; Motoröltemperatur =&lt; 150°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF4 | Motoröltemperatur &gt; 150°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF5 | Getriebeöltemperatur &lt; 80°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF6 | 80°C =&lt; Getriebeöltemperatur =&lt; 109°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF7 | 110°C =&lt; Getriebeöltemperatur =&lt; 124°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF8 | 125°C =&lt; Getriebeöltemperatur =&lt; 129°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AF9 | Getriebeöltemperatur &gt; 129°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFA | Umgebungstemperatur &lt; 3°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFB | 3°C =&lt; Umgebungstemperatur =&lt; 19°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFC | 20°C =&lt; Umgebungstemperatur =&lt; 29°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFD | 30°C =&lt; Umgebungstemperatur =&lt; 39°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5AFE | Umgebungstemperatur &gt; 39°C | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5B00 | Einspritzzeit Zylinder 1 von der Endstufe rückgemessen  | ms | - | unsigned integer | - | 0,00100000004749745 | 1 | 0,0 |
| 0x5B01 | Einspritzzeit Zylinder 2 von der Endstufe rückgemessen  | ms | - | unsigned integer | - | 0,00100000004749745 | 1 | 0,0 |
| 0x5B02 | Einspritzzeit Zylinder 3 von der Endstufe rückgemessen  | ms | - | unsigned integer | - | 0,00100000004749745 | 1 | 0,0 |
| 0x5B03 | Einspritzzeit Zylinder 4 von der Endstufe rückgemessen  | ms | - | unsigned integer | - | 0,00100000004749745 | 1 | 0,0 |
| 0x5B04 | Einspritzzeit Zylinder 5 von der Endstufe rückgemessen  | ms | - | unsigned integer | - | 0,00100000004749745 | 1 | 0,0 |
| 0x5B05 | Einspritzzeit Zylinder 6 von der Endstufe rückgemessen  | ms | - | unsigned integer | - | 0,00100000004749745 | 1 | 0,0 |
| 0x5B10 | Tastverhältnis Injektor 1 an Endstufe  | % | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x5B11 | Tastverhältnis Injektor 2 an Endstufe  | % | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x5B12 | Tastverhältnis Injektor 3 an Endstufe  | % | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x5B13 | Tastverhältnis Injektor 4 an Endstufe  | % | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x5B14 | Tastverhältnis Injektor 5 an Endstufe  | % | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x5B15 | Tastverhältnis Injektor 6 an Endstufe  | % | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| 0x5B20 | Elektrische Ladung Injektor 1 | uAs | - | unsigned integer | - | 2,22160005569458 | 1 | 0,0 |
| 0x5B21 | Elektrische Ladung Injektor 2 | uAs | - | unsigned integer | - | 2,22160005569458 | 1 | 0,0 |
| 0x5B22 | Elektrische Ladung Injektor 3 | uAs | - | unsigned integer | - | 2,22160005569458 | 1 | 0,0 |
| 0x5B23 | Elektrische Ladung Injektor 4 | uAs | - | unsigned integer | - | 2,22160005569458 | 1 | 0,0 |
| 0x5B24 | Elektrische Ladung Injektor 5 | uAs | - | unsigned integer | - | 2,22160005569458 | 1 | 0,0 |
| 0x5B25 | Elektrische Ladung Injektor 6 | uAs | - | unsigned integer | - | 2,22160005569458 | 1 | 0,0 |
| 0x5B30 | Spannung Injektor 1 | V | - | unsigned integer | - | 0,01953125 | 1 | 0,0 |
| 0x5B31 | Spannung Injektor 2 | V | - | unsigned integer | - | 0,01953125 | 1 | 0,0 |
| 0x5B32 | Spannung Injektor 3 | V | - | unsigned integer | - | 0,01953125 | 1 | 0,0 |
| 0x5B33 | Spannung Injektor 4 | V | - | unsigned integer | - | 0,01953125 | 1 | 0,0 |
| 0x5B34 | Spannung Injektor 5 | V | - | unsigned integer | - | 0,01953125 | 1 | 0,0 |
| 0x5B35 | Spannung Injektor 6 | V | - | unsigned integer | - | 0,01953125 | 1 | 0,0 |
| 0x5B40 | Adaptionswert der Enstufe Injektor 1 | %/mJ | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5B41 | Adaptionswert der Enstufe Injektor 2 | %/mJ | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5B42 | Adaptionswert der Enstufe Injektor 3 | %/mJ | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5B43 | Adaptionswert der Enstufe Injektor 4 | %/mJ | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5B44 | Adaptionswert der Enstufe Injektor 5 | %/mJ | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5B45 | Adaptionswert der Enstufe Injektor 6 | %/mJ | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5B50 | Momentan eingerechnete CILC-Werte Injektor 1 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5B51 | Momentan eingerechnete CILC-Werte Injektor 2 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5B52 | Momentan eingerechnete CILC-Werte Injektor 3 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5B53 | Momentan eingerechnete CILC-Werte Injektor 4 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5B54 | Momentan eingerechnete CILC-Werte Injektor 5 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5B55 | Momentan eingerechnete CILC-Werte Injektor 6 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5B60 | CILC-Adaption kalt Injektor 1 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5B61 | CILC-Adaption kalt Injektor 2 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5B62 | CILC-Adaption kalt Injektor 3 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5B63 | CILC-Adaption kalt Injektor 4 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5B64 | CILC-Adaption kalt Injektor 5 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5B65 | CILC-Adaption kalt Injektor 6 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5B70 | ER-Adaption MFF-additiv im LL Schicht für Injektor 1 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5B71 | ER-Adaption MFF-additiv im LL Schicht für Injektor 2 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5B72 | ER-Adaption MFF-additiv im LL Schicht für Injektor 3 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5B73 | ER-Adaption MFF-additiv im LL Schicht für Injektor 4 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5B74 | ER-Adaption MFF-additiv im LL Schicht für Injektor 5 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5B75 | ER-Adaption MFF-additiv im LL Schicht für Injektor 6 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5B80 | ER-MFF-aditiv im LL-Schicht (momentan eingerechte Werte) Injektor 1 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5B81 | ER-MFF-aditiv im LL-Schicht (momentan eingerechte Werte) Injektor 2 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5B82 | ER-MFF-aditiv im LL-Schicht (momentan eingerechte Werte) Injektor 3 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5B83 | ER-MFF-aditiv im LL-Schicht (momentan eingerechte Werte) Injektor 4 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5B84 | ER-MFF-aditiv im LL-Schicht (momentan eingerechte Werte) Injektor 5 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5B85 | ER-MFF-aditiv im LL-Schicht (momentan eingerechte Werte) Injektor 6 | mg/stk | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| 0x5B90 | ER-Adaptionsfaktor in Schicht Teillast für Injektor 1 | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5B91 | ER-Adaptionsfaktor in Schicht Teillast für Injektor 2 | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5B92 | ER-Adaptionsfaktor in Schicht Teillast für Injektor 3 | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5B93 | ER-Adaptionsfaktor in Schicht Teillast für Injektor 4 | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5B94 | ER-Adaptionsfaktor in Schicht Teillast für Injektor 5 | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5B95 | ER-Adaptionsfaktor in Schicht Teillast für Injektor 6 | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5BA0 | ER-Faktor in Schicht Teillast momentan eingerechnet für Injektor 1 | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5BA1 | ER-Faktor in Schicht Teillast momentan eingerechnet für Injektor 2 | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5BA2 | ER-Faktor in Schicht Teillast momentan eingerechnet für Injektor 3 | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5BA3 | ER-Faktor in Schicht Teillast momentan eingerechnet für Injektor 4 | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5BA4 | ER-Faktor in Schicht Teillast momentan eingerechnet für Injektor 5 | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5BA5 | ER-Faktor in Schicht Teillast momentan eingerechnet für Injektor 6 | - | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| 0x5BB0 | Lambdaadaption am Bandende hat fertig gelernt  | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5BB1 | ER-Balancing am Bandende hat additiv adaptiert  | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5BB2 | Lambdaadaption ist nötig, zyklisch während Motorbetrieb zu 1 gesetzt  | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5BB3 | ER-Balancing am Bandende hat den Faktor adaptiert  | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5BB4 | Zylindersel. Lambdaregelung fordert homogen an, zyklisch während dem Motorbetrieb zu 1 gesetzt  | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5BB5 | Zylindersel. Lambdaregelung kalt am Bandende hat fertig adaptiert  | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5BB6 | Zylindersel. Lambdaregelung warm am Bandende hat fertig adaptiert  | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5BB7 | Zylindersel. Lambdaregelung warm ist nötig, zyklisch während Motorbetrieb zu 1 gesetzt  | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5BB8 | Zylindersel. Lambdaregelung fordert öffnen WG an, zyklisch während dem Motorbetrieb zu 1 gesetzt  | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5BB9 | Zylindersel. Lambdaregelung fordert öffnen WG2 an, zyklisch während dem Motorbetrieb zu 1 gesetzt  | 0/1 | - | 0xFF | - | 1 | 1 | 0 |
| 0x5BBA | Relative Zeit Homogen-Betrieb gesamter Motorlauf | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5BBB | Relative Zeit Homogen-Schicht-Betrieb gesamter Motorlauf | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5BBC | Relative Zeit Schicht-Betrieb gesamter Motorlauf | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5BBD | Relative Zeit Homogen-Betrieb gesamter Motorlauf | % | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| 0x5BCA | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt A | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BCB | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt A | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BCC | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt B | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BCD | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt B | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BCE | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt C | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BCF | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt C | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BD0 | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt D | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BD1 | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt D | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BD2 | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt E | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BD3 | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt E | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BE0 | CILC-Adaptionswert warm High-Range Injektor 1 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BE1 | CILC-Adaptionswert warm High-Range Injektor 2 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BE2 | CILC-Adaptionswert warm High-Range Injektor 3 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BE3 | CILC-Adaptionswert warm High-Range Injektor 4 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BE4 | CILC-Adaptionswert warm High-Range Injektor 5 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BE5 | CILC-Adaptionswert warm High-Range Injektor 6 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BF0 | CILC-Adaptionswert warm Low-Range Injektor 1 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BF1 | CILC-Adaptionswert warm Low-Range Injektor 2 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BF2 | CILC-Adaptionswert warm Low-Range Injektor 3 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BF3 | CILC-Adaptionswert warm Low-Range Injektor 41 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BF4 | CILC-Adaptionswert warm Low-Range Injektor 5 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x5BF5 | CILC-Adaptionswert warm Low-Range Injektor 6 | % | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| 0x58FF | Umweltbedingung unbekannt | - | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 368 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x29CC | 0x0006 | 0x0007 | 0x0005 | 0x0003 |
| 0x29CD | 0x0000 | 0x0007 | 0x0005 | 0x0003 |
| 0x29CE | 0x0000 | 0x0007 | 0x0005 | 0x0003 |
| 0x29CF | 0x0000 | 0x0007 | 0x0005 | 0x0003 |
| 0x29D0 | 0x0000 | 0x0007 | 0x0005 | 0x0003 |
| 0x29D1 | 0x0000 | 0x0007 | 0x0005 | 0x0003 |
| 0x29D2 | 0x0000 | 0x0007 | 0x0005 | 0x0003 |
| 0x29D9 | 0x0000 | 0x0000 | 0x0009 | 0x0000 |
| 0x29DA | 0x0000 | 0x0000 | 0x000A | 0x0000 |
| 0x29DB | 0x0000 | 0x0000 | 0x000B | 0x0000 |
| 0x29DC | 0x012F | 0x0000 | 0x0196 | 0x0195 |
| 0x29E0 | 0x0137 | 0x0138 | 0x0139 | 0x0136 |
| 0x29E1 | 0x0137 | 0x0138 | 0x0139 | 0x0136 |
| 0x29E2 | 0x0000 | 0x0000 | 0x0010 | 0x003C |
| 0x29E5 | 0x0000 | 0x0000 | 0x013B | 0x013A |
| 0x29E6 | 0x0000 | 0x0000 | 0x013B | 0x013A |
| 0x29F1 | 0x0000 | 0x011E | 0x011F | 0x013C |
| 0x29F2 | 0x0000 | 0x0122 | 0x0121 | 0x0120 |
| 0x29F3 | 0x0000 | 0x0000 | 0x01A9 | 0x000F |
| 0x29F4 | 0x0000 | 0x0000 | 0x000E | 0x000E |
| 0x29F5 | 0x0000 | 0x0000 | 0x000E | 0x000E |
| 0x2A0D | 0x0000 | 0x0000 | 0x0000 | 0x00CF |
| 0x2A0E | 0x0000 | 0x0000 | 0x00D1 | 0x00D0 |
| 0x2A0F | 0x00D3 | 0x00D4 | 0x00D5 | 0x00D2 |
| 0x2A10 | 0x0000 | 0x0000 | 0x0010 | 0x003C |
| 0x2A12 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2A13 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2A15 | 0x0000 | 0x0000 | 0x0000 | 0x0012 |
| 0x2A16 | 0x0000 | 0x0000 | 0x0013 | 0x0000 |
| 0x2A17 | 0x0016 | 0x0017 | 0x0015 | 0x0014 |
| 0x2A18 | 0x0000 | 0x0011 | 0x0010 | 0x0018 |
| 0x2A19 | 0x0000 | 0x0011 | 0x0010 | 0x0018 |
| 0x2A1A | 0x001A | 0x0019 | 0x0000 | 0x0000 |
| 0x2A1B | 0x0000 | 0x0000 | 0x0000 | 0x001B |
| 0x2A1C | 0x001C | 0x0000 | 0x0000 | 0x0000 |
| 0x2A26 | 0x0000 | 0x0000 | 0x0000 | 0x000E |
| 0x2A27 | 0x0000 | 0x0000 | 0x0000 | 0x000E |
| 0x2A2B | 0x0000 | 0x0000 | 0x00E5 | 0x00E4 |
| 0x2A2C | 0x0000 | 0x0000 | 0x00E5 | 0x00E4 |
| 0x2A2D | 0x0000 | 0x00E2 | 0x00E1 | 0x00E0 |
| 0x2A80 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2A82 | 0x0023 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A85 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2A87 | 0x0023 | 0x0000 | 0x0000 | 0x0000 |
| 0x2A94 | 0x0000 | 0x0000 | 0x0025 | 0x0024 |
| 0x2A95 | 0x0000 | 0x0000 | 0x0000 | 0x0026 |
| 0x2A96 | 0x0000 | 0x0000 | 0x0000 | 0x0027 |
| 0x2A97 | 0x0000 | 0x0000 | 0x0000 | 0x0028 |
| 0x2A98 | 0x0000 | 0x0000 | 0x0000 | 0x0029 |
| 0x2A99 | 0x0000 | 0x0000 | 0x0000 | 0x0029 |
| 0x2A9A | 0x0000 | 0x0000 | 0x0000 | 0x002B |
| 0x2A9B | 0x0000 | 0x0000 | 0x0000 | 0x002B |
| 0x2A9E | 0x0000 | 0x0000 | 0x0000 | 0x0026 |
| 0x2A9F | 0x0000 | 0x0000 | 0x0000 | 0x0026 |
| 0x2AA0 | 0x0000 | 0x0000 | 0x0000 | 0x0024 |
| 0x2AA1 | 0x0000 | 0x0000 | 0x0000 | 0x0024 |
| 0x2AA2 | 0x0000 | 0x0000 | 0x0000 | 0x002C |
| 0x2AA3 | 0x0000 | 0x0000 | 0x0000 | 0x002C |
| 0x2AA4 | 0x0000 | 0x0000 | 0x0000 | 0x002A |
| 0x2AA5 | 0x0000 | 0x0000 | 0x0000 | 0x002A |
| 0x2AA8 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2AA9 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2AAA | 0x0000 | 0x0000 | 0x002E | 0x002D |
| 0x2AAB | 0x002F | 0x0000 | 0x0000 | 0x0000 |
| 0x2AAC | 0x002F | 0x0000 | 0x0000 | 0x0000 |
| 0x2AAD | 0x0000 | 0x0030 | 0x0000 | 0x0000 |
| 0x2AAE | 0x0033 | 0x0032 | 0x0034 | 0x0031 |
| 0x2AAF | 0x0000 | 0x0125 | 0x0124 | 0x0123 |
| 0x2AB2 | 0x0000 | 0x0000 | 0x0036 | 0x0035 |
| 0x2AB3 | 0x0000 | 0x0039 | 0x0038 | 0x0037 |
| 0x2AB4 | 0x0000 | 0x0000 | 0x0000 | 0x003A |
| 0x2AB5 | 0x0000 | 0x003B | 0x0000 | 0x0000 |
| 0x2AB6 | 0x0000 | 0x003B | 0x0000 | 0x0000 |
| 0x2ABC | 0x0000 | 0x0000 | 0x0010 | 0x000F |
| 0x2ABD | 0x0000 | 0x0025 | 0x0000 | 0x0000 |
| 0x2AC6 | 0x0000 | 0x0000 | 0x0010 | 0x003C |
| 0x2ACB | 0x0000 | 0x0000 | 0x003E | 0x003D |
| 0x2ACC | 0x0000 | 0x0000 | 0x003F | 0x0000 |
| 0x2AD0 | 0x0040 | 0x0000 | 0x0000 | 0x0000 |
| 0x2ADF | 0x0000 | 0x0000 | 0x0034 | 0x0031 |
| 0x2AE0 | 0x0000 | 0x0000 | 0x0034 | 0x0031 |
| 0x2AE4 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2AF0 | 0x012D | 0x0011 | 0x0000 | 0x0000 |
| 0x2AF2 | 0x012D | 0x0011 | 0x0000 | 0x0000 |
| 0x2AF4 | 0x012D | 0x0011 | 0x0000 | 0x0000 |
| 0x2AF6 | 0x012D | 0x0011 | 0x0000 | 0x0000 |
| 0x2C24 | 0x0041 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C27 | 0x0000 | 0x0000 | 0x0000 | 0x000C |
| 0x2C28 | 0x0000 | 0x0000 | 0x0000 | 0x000C |
| 0x2C2B | 0x0000 | 0x0000 | 0x0000 | 0x000D |
| 0x2C2C | 0x0000 | 0x0000 | 0x0000 | 0x000D |
| 0x2C2D | 0x0000 | 0x0000 | 0x0000 | 0x0042 |
| 0x2C2E | 0x0000 | 0x0000 | 0x0000 | 0x0042 |
| 0x2C31 | 0x0000 | 0x0000 | 0x0044 | 0x0043 |
| 0x2C32 | 0x0000 | 0x0000 | 0x0044 | 0x0043 |
| 0x2C39 | 0x0000 | 0x0000 | 0x0000 | 0x0046 |
| 0x2C3A | 0x0000 | 0x0000 | 0x0000 | 0x0046 |
| 0x2C3B | 0x0000 | 0x0000 | 0x0000 | 0x0047 |
| 0x2C3C | 0x0000 | 0x0000 | 0x0000 | 0x0047 |
| 0x2C3D | 0x0049 | 0x01AB | 0x01AA | 0x0048 |
| 0x2C3E | 0x0049 | 0x01AB | 0x01AA | 0x0048 |
| 0x2C3F | 0x0000 | 0x0000 | 0x0010 | 0x000F |
| 0x2C40 | 0x0000 | 0x0000 | 0x0010 | 0x000F |
| 0x2C41 | 0x0000 | 0x0000 | 0x004C | 0x004B |
| 0x2C42 | 0x0000 | 0x0000 | 0x004C | 0x004B |
| 0x2C6A | 0x004D | 0x0000 | 0x0000 | 0x0000 |
| 0x2C6B | 0x0000 | 0x0000 | 0x004E | 0x004F |
| 0x2C6C | 0x0000 | 0x0000 | 0x004E | 0x004F |
| 0x2C6D | 0x0050 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C6E | 0x0050 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C73 | 0x0000 | 0x0000 | 0x0000 | 0x000F |
| 0x2C74 | 0x0000 | 0x0000 | 0x0000 | 0x000F |
| 0x2C75 | 0x0000 | 0x0000 | 0x0010 | 0x0000 |
| 0x2C76 | 0x0000 | 0x0000 | 0x0010 | 0x0000 |
| 0x2C77 | 0x0000 | 0x0011 | 0x0000 | 0x0000 |
| 0x2C78 | 0x0000 | 0x0011 | 0x0000 | 0x0000 |
| 0x2C7B | 0x0053 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C7C | 0x0053 | 0x0000 | 0x0000 | 0x0000 |
| 0x2C7E | 0x0000 | 0x0000 | 0x0044 | 0x0043 |
| 0x2C7F | 0x0000 | 0x0000 | 0x0044 | 0x0043 |
| 0x2C87 | 0x0000 | 0x0000 | 0x0010 | 0x003C |
| 0x2C9C | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2C9D | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2C9E | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2C9F | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2CA6 | 0x0000 | 0x01A8 | 0x0055 | 0x0055 |
| 0x2CA7 | 0x0000 | 0x01A8 | 0x0055 | 0x0055 |
| 0x2CA8 | 0x0000 | 0x0000 | 0x0000 | 0x0057 |
| 0x2CA9 | 0x0000 | 0x0000 | 0x0000 | 0x0057 |
| 0x2CAA | 0x0000 | 0x01A8 | 0x0055 | 0x0055 |
| 0x2CAB | 0x0000 | 0x01A8 | 0x0055 | 0x0055 |
| 0x2CEC | 0x0000 | 0x0000 | 0x0000 | 0x0058 |
| 0x2CED | 0x0000 | 0x0000 | 0x0000 | 0x0059 |
| 0x2CEE | 0x0000 | 0x0000 | 0x0000 | 0x005A |
| 0x2CEF | 0x0000 | 0x005B | 0x0000 | 0x0000 |
| 0x2CF6 | 0x005C | 0x0000 | 0x0000 | 0x0000 |
| 0x2CF7 | 0x005D | 0x0000 | 0x0000 | 0x0000 |
| 0x2CF9 | 0x0000 | 0x0000 | 0x0010 | 0x003C |
| 0x2CFA | 0x0000 | 0x0000 | 0x005E | 0x000F |
| 0x2CFB | 0x0062 | 0x0061 | 0x0060 | 0x005F |
| 0x2CFC | 0x0000 | 0x0000 | 0x0064 | 0x0063 |
| 0x2CFD | 0x0000 | 0x0000 | 0x0000 | 0x0065 |
| 0x2CFE | 0x0000 | 0x0000 | 0x0000 | 0x0066 |
| 0x2D06 | 0x0000 | 0x0000 | 0x0068 | 0x0067 |
| 0x2D0B | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2D0F | 0x0000 | 0x0148 | 0x01A5 | 0x01A6 |
| 0x2D15 | 0x0000 | 0x0000 | 0x0000 | 0x01A7 |
| 0x2D16 | 0x0000 | 0x0000 | 0x010F | 0x0180 |
| 0x2D1B | 0x0000 | 0x0000 | 0x005E | 0x000F |
| 0x2D1C | 0x0000 | 0x0000 | 0x005E | 0x000F |
| 0x2D1D | 0x006A | 0x0000 | 0x0000 | 0x0000 |
| 0x2D1E | 0x006B | 0x0000 | 0x0000 | 0x0000 |
| 0x2D1F | 0x006C | 0x0000 | 0x0000 | 0x0000 |
| 0x2D20 | 0x006D | 0x0000 | 0x0000 | 0x0000 |
| 0x2D28 | 0x0000 | 0x0000 | 0x0010 | 0x003C |
| 0x2D29 | 0x0000 | 0x0000 | 0x006F | 0x006E |
| 0x2D2A | 0x0070 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D2B | 0x0025 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D2E | 0x0000 | 0x0000 | 0x006F | 0x006E |
| 0x2D50 | 0x0000 | 0x00EF | 0x00EE | 0x00ED |
| 0x2D52 | 0x0071 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D53 | 0x0071 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D55 | 0x0071 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D56 | 0x0000 | 0x0000 | 0x0073 | 0x0072 |
| 0x2D57 | 0x0076 | 0x0075 | 0x0000 | 0x0074 |
| 0x2D58 | 0x0079 | 0x007A | 0x0078 | 0x0077 |
| 0x2D59 | 0x0025 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D5A | 0x0025 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D5C | 0x0071 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D5F | 0x007E | 0x007D | 0x007C | 0x007B |
| 0x2D60 | 0x0071 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D61 | 0x0198 | 0x0000 | 0x0000 | 0x0000 |
| 0x2D64 | 0x0000 | 0x0000 | 0x015E | 0x015D |
| 0x2D67 | 0x0156 | 0x0157 | 0x0155 | 0x0154 |
| 0x2DBE | 0x0000 | 0x0000 | 0x0082 | 0x0081 |
| 0x2DC0 | 0x0188 | 0x0000 | 0x0000 | 0x0187 |
| 0x2DC3 | 0x0025 | 0x0085 | 0x0010 | 0x000F |
| 0x2DE1 | 0x0086 | 0x0000 | 0x0000 | 0x0000 |
| 0x2DE2 | 0x0086 | 0x0000 | 0x0000 | 0x0000 |
| 0x2DE3 | 0x0000 | 0x0087 | 0x0000 | 0x0000 |
| 0x2DEB | 0x0000 | 0x008D | 0x008E | 0x008C |
| 0x2DEC | 0x0090 | 0x0000 | 0x008F | 0x0000 |
| 0x2DED | 0x0091 | 0x0000 | 0x0000 | 0x0000 |
| 0x2E30 | 0x0000 | 0x012E | 0x012D | 0x0011 |
| 0x2E31 | 0x0000 | 0x012E | 0x012D | 0x0011 |
| 0x2E32 | 0x0000 | 0x012E | 0x012D | 0x0011 |
| 0x2E33 | 0x0000 | 0x012E | 0x012D | 0x0011 |
| 0x2E34 | 0x0000 | 0x012E | 0x012D | 0x0011 |
| 0x2E35 | 0x0000 | 0x012E | 0x012D | 0x0011 |
| 0x2E68 | 0x0025 | 0x0000 | 0x0092 | 0x0093 |
| 0x2E69 | 0x0025 | 0x0000 | 0x0092 | 0x0094 |
| 0x2E77 | 0x0000 | 0x011B | 0x0000 | 0x0000 |
| 0x2E7C | 0x0000 | 0x004C | 0x0000 | 0x0000 |
| 0x2E81 | 0x0000 | 0x0000 | 0x0000 | 0x0095 |
| 0x2E82 | 0x0000 | 0x0097 | 0x008C | 0x0096 |
| 0x2E83 | 0x0099 | 0x009A | 0x008E | 0x0098 |
| 0x2E84 | 0x0000 | 0x004C | 0x0000 | 0x0000 |
| 0x2E85 | 0x009B | 0x0000 | 0x0000 | 0x0000 |
| 0x2E8B | 0x009E | 0x009D | 0x0000 | 0x009C |
| 0x2E8C | 0x00A1 | 0x00A0 | 0x0000 | 0x009F |
| 0x2E8D | 0x00A4 | 0x00A3 | 0x0000 | 0x00A2 |
| 0x2E8E | 0x0000 | 0x00A5 | 0x0000 | 0x0000 |
| 0x2E96 | 0x0000 | 0x0000 | 0x0000 | 0x00A6 |
| 0x2E97 | 0x0181 | 0x0180 | 0x0000 | 0x0033 |
| 0x2E98 | 0x0000 | 0x00A5 | 0x0000 | 0x0000 |
| 0x2E9F | 0x00AA | 0x004C | 0x00AB | 0x00A9 |
| 0x2EA1 | 0x0000 | 0x015F | 0x0000 | 0x0000 |
| 0x2EAE | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0x2EAF | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0x2ECC | 0x0000 | 0x0000 | 0x0000 | 0x00A5 |
| 0x2ECD | 0x0000 | 0x0000 | 0x0000 | 0x0180 |
| 0x2ECE | 0x0000 | 0x0000 | 0x0000 | 0x0199 |
| 0x2ECF | 0x0000 | 0x0000 | 0x0000 | 0x0033 |
| 0x2ED0 | 0x0000 | 0x0000 | 0x0000 | 0x019A |
| 0x2ED1 | 0x0000 | 0x0000 | 0x0000 | 0x0181 |
| 0x2ED2 | 0x0000 | 0x0000 | 0x0000 | 0x019B |
| 0x2ED3 | 0x0000 | 0x0000 | 0x0000 | 0x019C |
| 0x2EE0 | 0x0000 | 0x0000 | 0x0010 | 0x003C |
| 0x2EE1 | 0x00AC | 0x0000 | 0x0000 | 0x0000 |
| 0x2EE2 | 0x00AD | 0x0000 | 0x0000 | 0x0000 |
| 0x2EE3 | 0x00AE | 0x0000 | 0x0000 | 0x0000 |
| 0x2EE6 | 0x019D | 0x0000 | 0x0000 | 0x0000 |
| 0x2EEA | 0x0000 | 0x0000 | 0x0010 | 0x003C |
| 0x2EEB | 0x00AF | 0x0000 | 0x0000 | 0x0000 |
| 0x2EEC | 0x0025 | 0x0000 | 0x0000 | 0x00B0 |
| 0x2EF4 | 0x00B1 | 0x0000 | 0x0000 | 0x0000 |
| 0x2EF5 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2EFE | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2EFF | 0x00B2 | 0x0000 | 0x0000 | 0x0000 |
| 0x2F08 | 0x0000 | 0x0000 | 0x0010 | 0x003C |
| 0x2F09 | 0x0025 | 0x0000 | 0x00B3 | 0x00B0 |
| 0x2F0A | 0x0000 | 0x0000 | 0x0010 | 0x003C |
| 0x2F0D | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2F0F | 0x0182 | 0x0000 | 0x0000 | 0x0000 |
| 0x2F10 | 0x0000 | 0x0000 | 0x0000 | 0x0180 |
| 0x2F11 | 0x0147 | 0x0000 | 0x0181 | 0x0145 |
| 0x2F12 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2F49 | 0x014D | 0x0000 | 0x00B7 | 0x0000 |
| 0x2F4A | 0x0150 | 0x008B | 0x014F | 0x014E |
| 0x2F4B | 0x0150 | 0x0152 | 0x0153 | 0x0151 |
| 0x2F4C | 0x0000 | 0x008B | 0x014F | 0x0000 |
| 0x2F4E | 0x0000 | 0x0024 | 0x0000 | 0x0000 |
| 0x2F4F | 0x0025 | 0x0000 | 0x0000 | 0x0000 |
| 0x2F58 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2F63 | 0x0025 | 0x0000 | 0x0000 | 0x0000 |
| 0x2F64 | 0x0025 | 0x0000 | 0x0000 | 0x0000 |
| 0x2F67 | 0x0000 | 0x0000 | 0x0010 | 0x003C |
| 0x2F6C | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2F71 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2F76 | 0x0000 | 0x0000 | 0x0010 | 0x003C |
| 0x2F77 | 0x0000 | 0x0000 | 0x00B3 | 0x00B0 |
| 0x2F79 | 0x0000 | 0x0025 | 0x0000 | 0x0000 |
| 0x2F7B | 0x0000 | 0x0011 | 0x0000 | 0x0000 |
| 0x2F80 | 0x0025 | 0x00BE | 0x0000 | 0x0000 |
| 0x2F85 | 0x0000 | 0x0000 | 0x0010 | 0x003C |
| 0x2F8F | 0x00BF | 0x0000 | 0x0000 | 0x0000 |
| 0x2F94 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2F99 | 0x0025 | 0x0000 | 0x0000 | 0x0000 |
| 0x2F9A | 0x0000 | 0x00C0 | 0x0000 | 0x0000 |
| 0x2F9E | 0x0025 | 0x0024 | 0x00C1 | 0x0000 |
| 0x2FA3 | 0x00C3 | 0x00C2 | 0x0000 | 0x0000 |
| 0x2FA4 | 0x00C5 | 0x00C4 | 0x0000 | 0x0000 |
| 0x2FAB | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2FAC | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2FBC | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x2FBD | 0x0000 | 0x0000 | 0x0161 | 0x0160 |
| 0x2FBE | 0x0000 | 0x0000 | 0x0000 | 0x0162 |
| 0x2FBF | 0x0000 | 0x0000 | 0x0000 | 0x019E |
| 0x2FC0 | 0x0000 | 0x019F | 0x01A0 | 0x01A1 |
| 0x2FC6 | 0x0000 | 0x00C8 | 0x00C7 | 0x00C6 |
| 0x3070 | 0x0000 | 0x0000 | 0x012C | 0x012B |
| 0x3071 | 0x0000 | 0x0000 | 0x012C | 0x012B |
| 0x3072 | 0x0000 | 0x0000 | 0x012C | 0x012B |
| 0x3073 | 0x0000 | 0x0000 | 0x012C | 0x012B |
| 0x3074 | 0x0000 | 0x0000 | 0x012C | 0x012B |
| 0x3075 | 0x0000 | 0x0000 | 0x012C | 0x012B |
| 0x307C | 0x0000 | 0x0000 | 0x0143 | 0x0142 |
| 0x307D | 0x0000 | 0x0000 | 0x0143 | 0x0142 |
| 0x307E | 0x0000 | 0x0000 | 0x0143 | 0x0142 |
| 0x307F | 0x0000 | 0x0000 | 0x0143 | 0x0142 |
| 0x3080 | 0x0000 | 0x0000 | 0x0143 | 0x0142 |
| 0x3081 | 0x0000 | 0x0000 | 0x0143 | 0x0142 |
| 0x3088 | 0x0000 | 0x0011 | 0x0000 | 0x0000 |
| 0x3089 | 0x0000 | 0x0011 | 0x0000 | 0x0000 |
| 0x308A | 0x0000 | 0x0011 | 0x0000 | 0x0000 |
| 0x308B | 0x0000 | 0x0011 | 0x0000 | 0x0000 |
| 0x308C | 0x0000 | 0x0011 | 0x0000 | 0x0000 |
| 0x308D | 0x0000 | 0x0011 | 0x0000 | 0x0000 |
| 0x3094 | 0x0000 | 0x0000 | 0x0010 | 0x0000 |
| 0x3095 | 0x0000 | 0x0000 | 0x0010 | 0x0000 |
| 0x3096 | 0x0000 | 0x0000 | 0x0010 | 0x0000 |
| 0x3097 | 0x0000 | 0x0000 | 0x0010 | 0x0000 |
| 0x3098 | 0x0000 | 0x0000 | 0x0010 | 0x0000 |
| 0x3099 | 0x0000 | 0x0000 | 0x0010 | 0x0000 |
| 0x30A0 | 0x0000 | 0x0000 | 0x0000 | 0x000F |
| 0x30A1 | 0x0000 | 0x0000 | 0x0000 | 0x000F |
| 0x30A2 | 0x0000 | 0x0000 | 0x0000 | 0x000F |
| 0x30A3 | 0x0000 | 0x0000 | 0x0000 | 0x000F |
| 0x30A4 | 0x0000 | 0x0000 | 0x0000 | 0x000F |
| 0x30A5 | 0x0000 | 0x0000 | 0x0000 | 0x000F |
| 0x30AC | 0x00F1 | 0x00F3 | 0x00F2 | 0x00F0 |
| 0x30AD | 0x00F1 | 0x00F3 | 0x00F2 | 0x00F0 |
| 0x30AE | 0x00F1 | 0x00F3 | 0x00F2 | 0x00F0 |
| 0x30AF | 0x00F1 | 0x00F3 | 0x00F2 | 0x00F0 |
| 0x30B0 | 0x00F1 | 0x00F3 | 0x00F2 | 0x00F0 |
| 0x30B1 | 0x00F1 | 0x00F3 | 0x00F2 | 0x00F0 |
| 0x30BA | 0x0000 | 0x0174 | 0x0175 | 0x004B |
| 0x30BB | 0x0000 | 0x0174 | 0x0175 | 0x004B |
| 0x30C0 | 0x0000 | 0x0000 | 0x0000 | 0x0189 |
| 0x30C1 | 0x0000 | 0x0000 | 0x018B | 0x018A |
| 0x30C2 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x30C3 | 0x0000 | 0x0000 | 0x005E | 0x00F5 |
| 0x30C4 | 0x0000 | 0x0000 | 0x018D | 0x018C |
| 0x30C5 | 0x0000 | 0x0000 | 0x018F | 0x018E |
| 0x30C6 | 0x0186 | 0x0000 | 0x0185 | 0x0184 |
| 0x30C7 | 0x0000 | 0x0000 | 0x0000 | 0x0190 |
| 0x30CA | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x30CF | 0x0000 | 0x0011 | 0x00F4 | 0x000F |
| 0x30D0 | 0x0000 | 0x0011 | 0x0010 | 0x000F |
| 0x30D6 | 0x0000 | 0x0000 | 0x0000 | 0x0178 |
| 0x30D8 | 0x0000 | 0x0165 | 0x017A | 0x0179 |
| 0x30DA | 0x0000 | 0x0000 | 0x0167 | 0x0168 |
| 0x30DC | 0x0000 | 0x016A | 0x0169 | 0x016B |
| 0x30DE | 0x0000 | 0x0000 | 0x0000 | 0x0051 |
| 0x30E0 | 0x0000 | 0x0000 | 0x0000 | 0x017B |
| 0x30E2 | 0x016F | 0x0165 | 0x017D | 0x017C |
| 0x30E4 | 0x0000 | 0x0000 | 0x017E | 0x0183 |
| 0x30E6 | 0x0000 | 0x0000 | 0x0000 | 0x017F |
| 0x30E9 | 0x0000 | 0x0000 | 0x0000 | 0x0172 |
| 0x30FD | 0x0000 | 0x0000 | 0x0192 | 0x0192 |
| 0x30FE | 0x0193 | 0x0000 | 0x0000 | 0x0000 |
| 0x30FF | 0x0194 | 0x0000 | 0x0000 | 0x0000 |
| 0xCD8B | 0x0000 | 0x00C9 | 0x0000 | 0x0000 |
| 0xCD94 | 0x0000 | 0x00CB | 0x0000 | 0x0000 |
| 0xCD95 | 0x00CD | 0x00CB | 0x00CC | 0x0000 |
| 0xCD96 | 0x00CD | 0x008B | 0x00CC | 0x0000 |
| 0xCD97 | 0x00CD | 0x008B | 0x00CC | 0x0000 |
| 0xCD98 | 0x00CD | 0x008B | 0x00CC | 0x0000 |
| 0xCD99 | 0x00CD | 0x008B | 0x00CC | 0x0000 |
| 0xCD9A | 0x00CD | 0x008B | 0x00CC | 0x0000 |
| 0xCD9B | 0x00CD | 0x008B | 0x00CC | 0x0000 |
| 0xCD9C | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCD9D | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCD9E | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCD9F | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDA0 | 0x00CD | 0x008B | 0x00CC | 0x0000 |
| 0xCDA1 | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDA2 | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDA3 | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDA4 | 0x0000 | 0x008B | 0x00CC | 0x0000 |
| 0xCDA5 | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDA6 | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDA7 | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDA8 | 0x0000 | 0x008B | 0x00CC | 0x0000 |
| 0xCDA9 | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDAA | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDAB | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDAC | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDAD | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDAE | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDAF | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDB0 | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDB1 | 0x0000 | 0x008B | 0x0000 | 0x0000 |
| 0xCDB3 | 0x00CD | 0x008B | 0x00CC | 0x0000 |
| 0xCDB4 | 0x00CD | 0x008B | 0x00CC | 0x0000 |
| 0xCDB5 | 0x0000 | 0x00C9 | 0x0000 | 0x0000 |
| 0xCDB9 | 0x00CD | 0x008B | 0x00CC | 0x0000 |
| 0xCDBA | 0x00CD | 0x008B | 0x00CC | 0x0000 |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 429 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | kein passendes Fehlersymptom |
| 0x0001 | Signal oder Wert oberhalb Schwelle |
| 0x0002 | Signal oder Wert unterhalb Schwelle |
| 0x0003 | mit Kraftstoffabschaltung |
| 0x0004 | kein Signal oder Wert |
| 0x0005 | Abgasschädigend nach Startvorgang |
| 0x0006 | Verbrennungsaussetzer an mehreren Zylindern |
| 0x0007 | Abgasschädigend |
| 0x0008 | unplausibles Signal oder Wert |
| 0x0009 |  Tankfüllstand zu gering |
| 0x000A | Segmentadaption am  Anschlag |
| 0x000B | Zahnfehler Kurbelwellengeber |
| 0x000C | Gemisch zu mager |
| 0x000D | Gemisch zu fett |
| 0x000E | Wirkungsgrad unter Schwellwert |
| 0x000F | Kurzschluss nach Plus |
| 0x0010 | Kurzschluss nach Minus |
| 0x0011 | Leitungsunterbrechung |
| 0x0012 | Leckage grösser 1,0 mm |
| 0x0013 | Leckage grösser 0,5 mm |
| 0x0014 | obere Schwelle Pumpenstrom bei Referenzmessung |
| 0x0015 | untere Schwelle Pumpenstrom bei Referenzmessung |
| 0x0016 | Pumpenstromschwelle bei Ventilprüfung erreicht |
| 0x0017 | Abbruch wegen Stromschwankungen bei Feinleckprüfung |
| 0x0018 | kurzschluss nach Plus |
| 0x0019 | Funktionstest Bandende |
| 0x001A | Funktionstest |
| 0x001B | nicht korrekt geschlossen |
| 0x001C | Füllstandssignalwert zum Verbrauchswert unplausibel |
| 0x001D | Drehrichtungserkennung |
| 0x001E | Relais-Fehler |
| 0x001F | Kurzschluss der Motorleitungen |
| 0x0020 | Übertemperatur Endstufe |
| 0x0021 | Überlast Strom |
| 0x0022 | Überstrom zu lange |
| 0x0023 | schwergängig, klemmt mechanisch |
| 0x0024 | Signal fehlt |
| 0x0025 | Signal unplausibel |
| 0x0026 | Synchronisation |
| 0x0027 | Zahnfehler |
| 0x0028 | Zahnzeitfehler |
| 0x0029 | Wert außerhalb Referenzbereich |
| 0x002A | Zahnsprung |
| 0x002B | Signal ungültig für Synchronisation |
| 0x002C | Segmentzeit |
| 0x002D | DISA 2: Schalter defekt |
| 0x002E | DISA 1: Schalter defekt |
| 0x002F | Eigendiagnose / Mechanischer- oder Hardwaredefekt |
| 0x0030 | Notabschaltung |
| 0x0031 | Drehzahl zu hoch |
| 0x0032 | Notlauf |
| 0x0033 | Übertemperatur |
| 0x0034 | Drehzahl zu niedrig |
| 0x0035 | interner RAM-Baustein |
| 0x0036 | Sicherheitsrechner RAM |
| 0x0037 | Bootsoftware |
| 0x0038 | Applikationssoftware |
| 0x0039 | Datenbereich |
| 0x003A | RAM-Überprüfung |
| 0x003B | Timeout SPI Bus |
| 0x003C | Kurzschluss nach Plus oder Leitungsunterbrechung |
| 0x003D | nicht abgefallen |
| 0x003E | nicht angezogen  |
| 0x003F | schaltet zu spät |
| 0x0040 | Fehlerverwaltung Getriebe |
| 0x0041 | vertauschte Lambdasonden vor Katalysator |
| 0x0042 | Signal während Schubabschaltung unterhalb Schwelle |
| 0x0043 | Abgas nach Katalysator zu fett |
| 0x0044 | Abgas nach Katalysator zu mager |
| 0x0045 | Heiztakteinkopplung auf Signal |
| 0x0046 | Signalamplitude zu gering |
| 0x0047 | Sonde nicht angesteckt |
| 0x0048 | Unterbrechung Nernstleitung |
| 0x0049 | Unterbrechung Abgleichsleitung |
| 0x004A | Unterbrechung Pumpstrompfad oder virtuelle Masse |
| 0x004B | Initialisierungsfehler |
| 0x004C | Kommunikationsfehler |
| 0x004D | vertauschte Lambdasonden nach Katalysator |
| 0x004E | Signal magerer als erwartet |
| 0x004F | Signal fetter als erwartet |
| 0x0050 | Sondensignal zu träge |
| 0x0051 | Signal nicht plausibel |
| 0x0052 | Sondensignal zu träge nach Schubphase |
| 0x0053 | Signal während Schubabschaltung  oberhalb Schwelle |
| 0x0054 | Arbeitstemperatur Sonde nicht erreicht |
| 0x0055 | Betriebsbereitschaft Sonde zu spät erreicht |
| 0x0056 | Sondentemperatur  ungültig |
| 0x0057 | Innenwiderstand des Signalkreises zu hochohmig |
| 0x0058 | klemmt kurzzeitig |
| 0x0059 | klemmt dauerhaft |
| 0x005A | schwergängig zu langsam |
| 0x005B | Ansteuerung fehlerhaft |
| 0x005C | Poti 1 unplausibel zu MAF |
| 0x005D | Poti 2 unplausibel zu MAF |
| 0x005E | Kurzschluss nach Minus oder Leitungsunterbrechung |
| 0x005F | Randbedingungen verletzt |
| 0x0060 | Notluftpunkt nicht adaptiert |
| 0x0061 | Federtest und Notluftprüfung verfehlt  |
| 0x0062 | unteren Anschlag lernen während Urinitialisierung abgebrochen |
| 0x0063 | Federtest |
| 0x0064 | Notluftprüfung |
| 0x0065 | Neuadaption erforderlich |
| 0x0066 | unterer Anschlag nicht gelernt |
| 0x0067 | Messwert HFM zu hoch |
| 0x0068 | Messwert HFM zu niedrig |
| 0x0069 | Plausibilitaet zwischen Poti 1 und 2 verletzt |
| 0x006A | Spannungsregler 1 |
| 0x006B | Spannungsregler 2 |
| 0x006C | Doppelfehler |
| 0x006D | Gleichlauffehler |
| 0x006E | IST Wert zu hoch |
| 0x006F | IST Wert zu niedrig |
| 0x0070 | Offset Maximum überschritten |
| 0x0071 | defekt |
| 0x0072 | Anforderung I-Anteil unplausibel |
| 0x0073 | Anforderung PD-Anteil unplausibel |
| 0x0074 | Anforderung MSR unplausibel |
| 0x0075 | Anforderung AMT unplausibel |
| 0x0076 | Anforderung EGS unplausibel |
| 0x0077 | maximales Kupplungsmoment unplausibel |
| 0x0078 | minimales Kupplungsmoment unplausibel |
| 0x0079 | Sporttastersignal unplausibel |
| 0x007A | Verlustmoment unplausibel |
| 0x007B | Software |
| 0x007C | Sicherheitsabschaltung |
| 0x007D | Hardware |
| 0x007E | SPI-Fehler |
| 0x007F | Schalter defekt |
| 0x0080 | Toggle-Bit |
| 0x0081 | irreversibel aus |
| 0x0082 | reversibel aus |
| 0x0083 | Momentenanforderung vom LDM trotzt Bremssignal |
| 0x0084 | Momentenanforderung vom LDM unplausibel |
| 0x0085 | CAS-Fehler |
| 0x0086 | CAN Wert unplausibel |
| 0x0087 | kein Signal |
| 0x0088 | ALIVE-Fehler |
| 0x0089 | Prüfsumme |
| 0x008A | Checksumme |
| 0x008B | Timeout |
| 0x008C | Überspannung |
| 0x008D | batterieloser Betrieb |
| 0x008E | Unterspannung |
| 0x008F | Tiefentladung |
| 0x0090 | Powermanagement |
| 0x0091 | Ruhestromverletzung |
| 0x0092 | Motor mechanisch zu leise |
| 0x0093 | Motor mechanisch zu laut  |
| 0x0094 | Motor mechanisch zu laut |
| 0x0095 | Drehzahl außerhalb der Toleranz |
| 0x0096 | interne Temperatur zu hoch |
| 0x0097 | Überstrom |
| 0x0098 | Trockenlauf |
| 0x0099 | Temperaturschwelle 2 überschritten |
| 0x009A | Temperaturschwelle 1 überschritten |
| 0x009B | keine Spannung am Notlauf-Eingang der Pumpe |
| 0x009C | EBSD-Fehler |
| 0x009D | BSD-Fehler |
| 0x009E | Software-Fehler |
| 0x009F | Temperatur |
| 0x00A0 | Spannung |
| 0x00A1 | Strom |
| 0x00A2 | Wakeupleitung Masseschluss |
| 0x00A3 | Systemfehler |
| 0x00A4 | Wakeupleitung Pegel unplausibel |
| 0x00A5 | keine Kommunikation über BSD-Schnittstelle |
| 0x00A6 | Startphase |
| 0x00A7 | Elektrisch |
| 0x00A8 | Mechanisch |
| 0x00A9 | Temperaturmessung |
| 0x00AA | Permittivitätsmessung |
| 0x00AB | Niveaumessung  |
| 0x00AC | unplausibel bezüglich Lambdaregelung |
| 0x00AD | Temperatursignal konstant |
| 0x00AE | Temperaturgradient zu steil |
| 0x00AF | Temperaturgradient zu hoch |
| 0x00B0 | Signal oberhalb Schwelle |
| 0x00B1 | klemmt offen |
| 0x00B2 | Mechanischer- oder Hardwaredefekt |
| 0x00B3 | Signal unterhalb Schwelle |
| 0x00B4 | 1. Startwert im Flash zerstört. 2- aus 3-Auswahl fehlgeschlagen oder 2. Fehlerrückmeldung: Startwertprogrammierroutine |
| 0x00B5 | Falsche EWS-Telegramme empfangen. Die Fangbereichsrechnung ist für mindestens 5 Telegrammauswertungen fehlgeschlagen. |
| 0x00B6 | Fehler beim Programmieren oder rücksetzen des Startwertes |
| 0x00B7 | kein Startwert programmiert |
| 0x00B8 | Empfangsfehler des EWS-Telegramms (Start-, Stopbit- oder Framefehler) |
| 0x00B9 | Timeoutfehler: 10 Sekunden nach Kl.15 EIN noch kein EWS-Telegramm empfangen, evtl. Leitungsunterbrechung oder Kurzschluss nach Minus |
| 0x00BA | Mehr als 3 Parity-Fehler erkannt |
| 0x00BB | Lesefehler im EEPROM: Wechselcode Ablage |
| 0x00BC | Schreibfehler im EEPROM: Wechselcode Ablage |
| 0x00BD | Fehler Ablage |
| 0x00BE | Timeout (Ungültigkeitswert vom Kombi) |
| 0x00BF | Pedalwert zu Bremspedal |
| 0x00C0 | Signalfehler |
| 0x00C1 | Oelniveau zu niedrig |
| 0x00C2 | Codierdaten im EEPROM fehlerhaft |
| 0x00C3 | keine Codierung erfolgt (nach Programmierung) |
| 0x00C4 | CAN Timeout |
| 0x00C5 | Variantenüberwachung |
| 0x00C6 | Fertigungsmodus |
| 0x00C7 | Transportmodus |
| 0x00C8 | Werkstattmodus |
| 0x00C9 | CAN Bus off |
| 0x00CA | CAN Baustein im Zustand passiv |
| 0x00CB | Timeout  |
| 0x00CC | Aktualisierungszähler inkrementiert nicht (Alive-Zähler) |
| 0x00CD | Prüfsumme ungleich errechnetem Wert |
| 0x00CE | Kurzschluss nach Plus oder Leitungsnterbrechung |
| 0x00CF | Endstufe |
| 0x00D0 | Regelabweichung außerhalb gültigem Bereich |
| 0x00D1 | Regler Ausgangposition außerhalb gültigem Bereich |
| 0x00D2 | Adaptionsbedingungen nicht erfüllt |
| 0x00D3 | oberer Adaptionswert außerhalb gültigem Bereich |
| 0x00D4 | obere Position nicht erreicht |
| 0x00D5 | unterer Adaptionswert außerhalb gültigem Bereich |
| 0x00D6 | Ausfall Spannungsversorgung |
| 0x00D7 | Maximaler additiver Adaptionswert erreicht |
| 0x00D8 | Minimaler multiplikativer Adaptionswert (unterer Berreich) erreicht |
| 0x00D9 | Maximaler multiplikativer Adaptionswert (unterer Berreich) erreicht |
| 0x00DA | Minimaler additiver Adaptionswert erreicht |
| 0x00DB | Maxilmaler multiplikativer Adaptionswert (oberer Berreich) erreicht |
| 0x00DC | Minimaler multiplikativer Adaptionswert (oberer Berreich) erreicht |
| 0x00DD | Kraftstoffmasse Adaption außerhalb gültigem Bereich |
| 0x00DE | Integal Teil vom Regler außerhalb gültigem Bereich |
| 0x00DF | Kraftstoffmasse Adaptionsanregung außerhalb gültigem Bereich |
| 0x00E0 | obere Schwelle1 erreicht |
| 0x00E1 | obere Schwelle2 erreicht |
| 0x00E2 | untere Schwelle1 erreicht |
| 0x00E3 | Wirkungsgrad zu klein |
| 0x00E4 | Stillstand der Lambdaregelung (obere Grenze) |
| 0x00E5 | Stillstand der Lambdaregelung (untere Grenze) |
| 0x00E6 | Integral Teil vom EFPWM außerhalb gültigem Bereich |
| 0x00E7 | Adaptive Integral Teil vom EFPWM außerhalb gültigem Bereich |
| 0x00E8 | Adaptive minimales EFPPWM außerhalb gültigem Bereich |
| 0x00E9 | Heizungkreis |
| 0x00EA | Stickoxydkreis |
| 0x00EB | Binärer SauerstoffKreis |
| 0x00EC | Lambdakreis |
| 0x00ED | ACC Überwachung |
| 0x00EE | DCC Überwachung |
| 0x00EF | LDM Überwachung |
| 0x00F0 | Kurzschluss Hochspannungsseite nach Minus |
| 0x00F1 | Kurzschluss Niederspannungsseite nach Minus |
| 0x00F2 | Kurzschluss Niederspannungsseite nach Plus |
| 0x00F3 | Kurzschluss Hochspannungsseite nach Plus |
| 0x00F4 | Kurzschluss nach minus |
| 0x00F5 | Kurzschluss nach Plus oder 5V-Spannungsversorgung |
| 0x00F6 | Sekundärluftventil oder -schlauch blockiert |
| 0x00F7 | Grobe Undichtigkeit zwischen Sekundärluftpumpe und -Ventil |
| 0x00F8 | Sekundärluftpumpe nicht aktiv |
| 0x00F9 | Sekundärluftmasse zu gering |
| 0x00FA | Sekundärluftmenge zu gering Bank 1 |
| 0x00FB | Sekundärluftmenge zu gering Bank 1 und Bank 2 |
| 0x00FC | Sekundärluftmenge zu gering Bank 2 |
| 0x00FD | Klemmt offen |
| 0x00FE | Leitungsunterbrechung  |
| 0x00FF | Parity-Fehler |
| 0x0100 | Sensordiagnose |
| 0x0101 | Sensorsignal |
| 0x0102 | Sensorsignale zueinander unplausibel |
| 0x0103 | Lagereglerüberwachung |
| 0x0104 | gelernter Bereich ausserhalb der Toleranzen |
| 0x0105 | keine Anschläge gelernt |
| 0x0106 | Schreib-/Lesefehler im EEPROM |
| 0x0107 | Überlast |
| 0x0108 | Differenz Stop-/Startposition |
| 0x0109 | Warnschwelle Strom |
| 0x010A | Warnschwelle Stellmotor Temperatur |
| 0x010B | Warnschwelle Steuergerät Temperatur (VVT-Endstufe) |
| 0x010C | Valvetronic öffnet nicht |
| 0x010D | Exzenterwinkel fährt nicht auf Vollhubposition |
| 0x010E | oberer Anschlag nicht gelernt |
| 0x010F | Sensor defekt |
| 0x0110 | Luftzufuhr nicht korrekt |
| 0x0111 | Momentenanforderung vom Tempomat trotz Bremssignal |
| 0x0112 | Momentenanforderung vom ACC/DCC unplausibel |
| 0x0113 | Drosselklappenstellung unplausibel |
| 0x0114 | Zündzeit Zylinder 1 zu gering |
| 0x0115 | Zündzeit Zylinder 2 zu gering |
| 0x0116 | Zündzeit Zylinder 3 zu gering |
| 0x0117 | Zündzeit Zylinder 4 zu gering |
| 0x0118 | Zündzeit Zylinder 5 zu gering |
| 0x0119 | Zündzeit Zylinder 6 zu gering |
| 0x011A | Zündkreisüberwachung |
| 0x011B | Spannungsversorgung fehlt |
| 0x011C | Steuergerät defekt |
| 0x011D |  Adaptive Kraftstoffmasse außerhalb gültigem Bereich |
| 0x011E | Integralteil vom Regler außerhalb gültigem Bereich |
| 0x011F | Berechnung adaptive Kraftstoffmasse ungültig |
| 0x0120 | Oberer Schwellwert 1 des Raildruckes überschritten |
| 0x0121 | Oberer Schwellwert 2 des Raildruckes überschritten |
| 0x0122 | Unterer Schwellwert des Raildruckes unterschritten |
| 0x0123 | Integralteil von EFPPWM außerhalb gültigem Bereich |
| 0x0124 | Adaptives Integralteil von EFPWM außerhalb gültigem Bereich |
| 0x0125 | Adaptiertes minimales EFPPWM außerhalb gültigem Bereich |
| 0x0126 | Magerspannung nicht erreicht  |
| 0x0127 | Mengen Steuerventil Basis-Kennlinie Adaption 2 außerhalb gültigem Bereich |
| 0x0128 | Mengen Steuerventil Min-Kennlinie Adaption 2 außerhalb gültigem Bereich |
| 0x0129 | Mengen Steuerventil Basis-Kennlinie Adaption 1 außerhalb gültigem Bereich |
| 0x012A | Mengen Steuerventil Min-Kennlinie Adaption 1 außerhalb gültigem Bereich |
| 0x012B | Minimale Diagnosegrenze erreicht |
| 0x012C | Maximale Diagnosegrenze erreicht |
| 0x012D | Kurzschluss |
| 0x012E | Kurzschluss Hochspannungsseite nach Niederspannungsseite |
| 0x012F | Tankfüllstand zu gering |
| 0x0130 | Elektrischer Fehler |
| 0x0131 | Luftmassengradient zu hoch |
| 0x0132 | Minimaler multiplikativer Adaptionswert (unterer Bereich) erreicht |
| 0x0133 | Maximaler multiplikativer Adaptionswert (unterer Bereich) erreicht |
| 0x0134 | Maxilmaler multiplikativer Adaptionswert (oberer Bereich) erreicht |
| 0x0135 | Minimaler multiplikativer Adaptionswert (oberer Bereich) erreicht |
| 0x0136 | Gemisch im Leerlauf zu fett |
| 0x0137 | Gemisch in Teillast zu mager |
| 0x0138 | Gemisch in Teillast zu fett |
| 0x0139 | Gemisch im Leerlauf zu mager |
| 0x013A | Gemisch in volllast zu fett |
| 0x013B | Gemisch in volllast zu mager |
| 0x013C | Adaptive Kraftstoffmasse außerhalb gültigem Bereich |
| 0x013D | binärer SauerstoffKreis |
| 0x013E | gradient zu hoch |
| 0x013F | keine Authentisierungsbedienung |
| 0x0140 | falsche Authentisierung |
| 0x0141 | keine Antwort vom EWS/CAS |
| 0x0142 | Zylinder selektive Lambdaregelung - untere Grenze erreicht |
| 0x0143 | Zylinder selektive Lambdaregelung - obere Grenze erreicht |
| 0x0144 | elektrischer Fehler an der passive Luftklappe |
| 0x0145 | Hardwaredefekt |
| 0x0146 | mechanischer Fehler |
| 0x0147 | keine Kommunikation |
| 0x0148 | elektrischer Fehler |
| 0x0149 | Offsetabgleich im niedrigen Verstärkungsbereich |
| 0x014A | Offsetabgleich im hohen Verstärkungsbereich |
| 0x014B | Maximale Zeit für Offsetabgleich überschritten |
| 0x014C | Nockenwellen- zur Kurbelwellenposition außerhalb Referenzbereich |
| 0x014D | erwartete Antwort unplausible |
| 0x014E | Hardwarefehler |
| 0x014F | Framefehler |
| 0x0150 | Checksum |
| 0x0151 | keine verfügbare Speichermöglichkeit |
| 0x0152 | Startwert zerstört/ 2- aus 3-Auswahl fehlgeschlagen |
| 0x0153 | Fehlerfreischaltcodeablage |
| 0x0154 | ROM-Fehler |
| 0x0155 | RAM-Fehler |
| 0x0156 | Hauptrechnerüberwachung; Befehlssatztestfehler |
| 0x0157 | Rechnerüberwachung, allgemeiner Sammelfehler |
| 0x0158 | niedrige Speicherkapazität |
| 0x0159 | Integrierte Momentenreserve nicht erreicht |
| 0x015A | Bereich |
| 0x015B | Signal |
| 0x015C | Gradient |
| 0x015D | Umschaltung nach Homogen wegen Kraftstoffmassenstrom |
| 0x015E | Umschaltung nach Homogen wegen Motormoment |
| 0x015F | Keine Kommunikation über BSD-Schnittstelle |
| 0x0160 | Mengen Steuerventil Basis-Kennlinie Adaption außerhalb Gültigkeitsbereich |
| 0x0161 | Mengen Steuerventil Min-Kennlinie Adaption außerhalb Gültigkeitsbereich |
| 0x0162 | Druck zu hoch |
| 0x0163 | Signal zu niedrig |
| 0x0164 | Lambdasignal (binär) zu mager |
| 0x0165 | Nox-Signal zu niedrig |
| 0x0166 | Lambdasignal (linear) zu mager |
| 0x0167 | Signal nicht Verfügbar im Betrieb |
| 0x0168 | Signal nicht Verfügbar im Start |
| 0x0169 | Heizleistung zu niedrig im Betrieb |
| 0x016A | Versorgungsspannung |
| 0x016B | Heizleistung zu niedrig im Start |
| 0x016C | Signal-Offset |
| 0x016D | Lambdasignal (linear) zu fett |
| 0x016E | Lambdasignal (binär) zu fett |
| 0x016F | Nox-Signal zu hoch |
| 0x0170 | Heilungsüberwachung |
| 0x0171 | Dynamik zu niedrig |
| 0x0172 | Niedrige Speicherkapazität |
| 0x0173 | Analog |
| 0x0174 | Entladungsfehler |
| 0x0175 | Verbindungsfehler |
| 0x0176 | Gradient zu hoch |
| 0x0177 |   |
| 0x0178 | Signalaktivität zu gering |
| 0x0179 | Binäres Lambdasignal zu mager |
| 0x017A | Lineares Lambdasignal zu mager |
| 0x017B | Offset-Fehler |
| 0x017C | Binäres Lambdasignal zu fett |
| 0x017D | Lineares Lambdasignal zu fett |
| 0x017E | Zeitgesteuerter Regenerationsabbruch |
| 0x017F | Binäre Dynamik zu niedrig |
| 0x0180 | elektrisch |
| 0x0181 | mechanisch |
| 0x0182 | mechanischer- oder Hardwaredefekt |
| 0x0183 | Regenerationsüberwachung |
| 0x0184 | Druck zu hoch vor Start |
| 0x0185 | Druck zu niedrig vor Start |
| 0x0186 | Sensorwert ändert sich nicht |
| 0x0187 | Momentenanforderung trotzt Bremssignal |
| 0x0188 | Momentenanforderung unplausibel |
| 0x0189 | Regelkreisschwingung |
| 0x018A | Umschaltung in Notlauf-Betrieb, da Motoröldruck im Kennfeld-Betrieb zu hoch |
| 0x018B | Umschaltung in Notlauf-Betrieb, da Motoröldruck im Kennfeld-Betrieb zu niedrig |
| 0x018C | Magnetventil hängt in voll bestromter Stellung |
| 0x018D | Magnetventil hängt in unbestromter Stellung |
| 0x018E | oberer Öldruck außerhalb gültigem Bereich |
| 0x018F | unterer Öldruck außerhalb gültigem Bereich |
| 0x0190 | Regelung instabil |
| 0x0191 | Leckage auf Ladersystem |
| 0x0192 | Ladergleichlauf |
| 0x0193 | Überladerfehler |
| 0x0194 | Unterladerfehler |
| 0x0195 | Druck zu niedrig im Hochdruck-System |
| 0x0196 | Druck zu niedrig im Niederdruck-System |
| 0x0197 | Sondentemperatur außerhalb gültigem Bereich |
| 0x0198 | Spannung zwischen Poti 1 und 2 unplausibel |
| 0x0199 | elektrisch berechnet |
| 0x019A | Übertemperatur berechnet |
| 0x019B | Reglertyp nicht plausibel |
| 0x019C | Generatortyp nicht plausibel |
| 0x019D | Signal festliegend hoch |
| 0x019E | Druck zu niedrig |
| 0x019F | Unterer Schwellwert unterschritten |
| 0x01A0 | Oberer Schwellwert 2 überschritten |
| 0x01A1 | Oberer Schwellwert 1 überschritten |
| 0x01A2 | Strom zu hoch |
| 0x01A3 | Strom zu niedrig |
| 0x01A4 | Temperatur zu niedrig |
| 0x01A5 | Gradientenfehler |
| 0x01A6 | Meßbereichsproblem |
| 0x01A7 | Signal außerhalb gültigem Bereich |
| 0x01A8 | Sondentemperaturmessung im Steuergerät fehlgeschlagen |
| 0x01A9 | Kurzschluss nach Minus oder Leitungsnterbrechung |
| 0x01AA | Unterbrechung virtuelle Masse |
| 0x01AB | Unterbrechung Pumpstrompfad |
| 0xFFFF | unbekannte Fehlerart |

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

<a id="table-messwertetab"></a>
### MESSWERTETAB

Dimensions: 640 rows × 12 columns

| ARG | ID | RESULTNAME | INFO | EINHEIT | LABEL | L/H | DATENTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ITANS | 0x4200 | STAT_ANSAUGLUFTTEMPERATUR_WERT | Ansauglufttemperatur 1 | °C | TIA | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x4201 | STAT_0x4201_WERT | Umgebungsdruck | hPa | AMP_MES | - | unsigned integer | - | 0,0829175263643265 | 1 | 0,0 |
| IPSAU | 0x4202 | STAT_SAUGROHRDRUCK_WERT | Saugrohrdruck | hPa | MAP_MES | - | unsigned integer | - | 0,0829175263643265 | 1 | 0,0 |
| ILMKG | 0x4203 | STAT_LUFTMASSE_WERT | Massenstrom vom HFM | kg/h | MAF_KGH_MES | - | unsigned integer | - | 0,03125 | 1 | 0,0 |
| ITUMG | 0x4204 | STAT_UMGEBUNGSTEMPERATUR_WERT | Umgebungstemperatur | °C | TAM | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| IPLAD | 0x4205 | STAT_LADEDRUCK_WERT | Saugrohrdruck 1 / Ladedruck 1 | hPa | MAP_DIP_MES_BAS | - | unsigned integer | - | 0,0829175263643265 | 1 | 0,0 |
| ITKUM | 0x4300 | STAT_KUEHLMITTELTEMPERATUR_WERT | Kühlwassertemperatur | °C | TCO | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x4301 | STAT_0x4301_WERT | Kühlerauslasstemperatur | °C | TCO_2 | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| IPWAB | 0x4302 | STAT_WASSERPUMPENLEISTUNG_BSD_WERT | Wasserpumpe Leistung über BSD | % | REL_CWP_PWR | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| ITWAE | 0x4303 | STAT_WASSERPUMPE_ELEKTRONIK_TEMPERATUR_WERT | Wasserpumpe Elektronik Temperatur | °C | TEMP_EL_CWP | - | unsigned char | - | 1,0 | 1 | -50,0 |
| IIWAP | 0x4304 | STAT_WASSERPUMPE_STROM_WERT | Wasserpumpe Strom | A | CUR_CNS_CWP | - | unsigned char | - | 0,5 | 1 | 0,0 |
| INWAP | 0x4305 | STAT_WASSERPUMPE_DREHZAHL_WERT | Wasserpumpe Drehzahl Ist | - | N_REL_CWP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| SNWAP | 0x4306 | STAT_WASSERPUMPE_DREHZAHL_SOLL_WERT | Wasserpumpe Drehzahl Soll | - | N_REL_CWP_SP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x4307 | STAT_0x4307_WERT | Wasserpumpe Betriebsart | 0-n | BA_WM_IST | - | 0xFF | _CNV_S_11_Def_ba_wm_614 | 1 | 1 | 0 |
| IMLOE | 0x4400 | STAT_OELSTAND_LANGZEIT_MITTEL_WERT | Ölstand Mittelwert Langzeit | - | OZ_NIVLANGT | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| IFSOE | 0x4401 | STAT_FUELLSTAND_MOTOROEL_WERT | Füllstand Motoröl | - | OZ_LP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ITOEL | 0x4402 | STAT_OELTEMPERATUR_WERT | Öltemperatur | °C | TOEL | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| IKVLS | 0x4403 | STAT_KRAFTSTOFFVERBRAUCH_SEIT_SERVICE_WERT | Kraftstoff-Verbrauch seit letztem Service | - | OZ_KVBSM_UL | - | unsigned long | - | 1,220703125E-4 | 1 | 0,0 |
| IKMLS | 0x4404 | STAT_WEG_SEIT_SERVICE_WERT | km seit letztem Service | km | OZ_OELKM | - | unsigned integer | - | 10,0 | 1 | 0,0 |
| RNIOE | 0x4405 | STAT_OELSENSOR_NIVEAU_ROH_WERT | Ölsensor Niveau Rohwert | - | OZ_NIVR | - | unsigned char | - | 1,0 | 1 | 0,0 |
| RQUOE | 0x4406 | STAT_OELSENSOR_QUALITAET_ROH_WERT | Ölsensor Qualität Rohwert | - | OZ_PERMR | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| RTOEL | 0x4407 | STAT_OELSENSOR_TEMPERATUR_ROH_WERT | Ölsensor Temperatur Rohwert | - | OZ_TEMPR | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ITSOE | 0x4408 | STAT_OELSENSOR_TEMPERATUR_WERT | Ölsensor Temperatur | °C | OZ_TEMPAKT | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| INIOE | 0x4409 | STAT_OELSENSOR_NIVEAU_WERT | Ölsensor Niveau | - | OZ_NIVAKT | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| IQOEL | 0x440A | STAT_OELSENSOR_QUALITAET_WERT | Ölsensor Qualität | - | OZ_PERMAKT | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| - | 0x440B | STAT_0x440B_WERT | Länderfaktor 1 codiert | - | OZ_LF1C | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| - | 0x440C | STAT_0x440C_WERT | Länderfaktor 2 codiert | - | OZ_LF2C | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| - | 0x440D | STAT_0x440D_WERT | Länderfaktor 1 | - | OZ_LF1T | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| - | 0x440E | STAT_0x440E_WERT | Länderfaktor 2 | - | OZ_LF2T | - | unsigned char | - | 0,00999999977648258 | 1 | 0,0 |
| - | 0x440F | STAT_0x440F_WERT | Kurzmittelwert-Niveau für den Tester | - | OZ_NIVKRZT | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| - | 0x4410 | STAT_0x4410_WERT | Restweg aus Permittivität abgeleitet | km | OZ_RWPERM | - | signed integer | - | 10,0 | 1 | 0,0 |
| - | 0x4411 | STAT_0x4411_WERT | Restweg aus Kraftstoffverbrauch abgeleitet | km | OZ_RWKVB | - | signed integer | - | 10,0 | 1 | 0,0 |
| - | 0x4412 | STAT_0x4412_WERT | Öl-Alter in Monate | - | OZ_OELZEIT | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x4413 | STAT_0x4413_WERT | aufbereitete Permittivität bei letztem Ölwechsel | - | OZ_PERMLOW | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| - | 0x4414 | STAT_0x4414_WERT | Permittivität für Bewertung aufbereitet (extrapoliert) | - | OZ_PERMEX | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| - | 0x4415 | STAT_0x4415_WERT | Offset für Permittivitätskorrektur | - | OZ_PERMOFF | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| - | 0x4416 | STAT_0x4416_WERT | zugeteilte Bonuskraftstoffmenge | - | OZ_KVBOG | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x4417 | STAT_0x4417_WERT | zugeteilter Permittivitätsbonus | - | OZ_PERMBOG | - | unsigned integer | - | 9,1552734375E-5 | 1 | 0,0 |
| - | 0x4418 | STAT_0x4418_WERT | Status Peilstabanzeige | - | OZ_LV | - | unsigned char | - | 1,0 | 1 | 0,0 |
| SSPEI | 0x4505 | STAT_NW_EINLASSSPREIZUNG_SOLL_WERT | Sollwert Einlassspreizung | °CRK | CAM_SP_IVVT_IN | - | unsigned char | - | 0,375 | 1 | 59,9999982118607 |
| IPNWE | 0x4506 | STAT_POSITION_NOCKENWELLE_EINLASS_WERT | Nockenwellenposition Einlass | °CRK | PSN_CAM_IN_1 | - | unsigned integer | - | 0,375 | 1 | -95,9999971389771 |
| IPNWA | 0x4507 | STAT_POSITION_NOCKENWELLE_AUSLASS_WERT | Nockenwellenposition Auslass | °CRK | PSN_CAM_EX_1 | - | unsigned integer | - | 0,375 | 1 | -95,9999971389771 |
| ISNWE | 0x4508 | STAT_NW_EINLASSSPREIZUNG_WERT | Istwert Einlassspreizung | °CRK | CAM_IN[1] | - | unsigned char | - | 0,375 | 1 | 59,9999982118607 |
| ISNWA | 0x4509 | STAT_NW_AUSLASSSPREIZUNG_WERT | Istwert Auslassspreizung | °CRK | CAM_EX[1] | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| NSNWA | 0x450A | STAT_NW_NORMSPREIZUNG_AUSLASS_WERT | Normspreizung Auslass | °CRK | CAM_SP_REF_EX | - | signed integer | - | 0,0234375 | 1 | 0,0 |
| NSNWE | 0x450B | STAT_NW_NORMSPREIZUNG_EINLASS_WERT | Normspreizung Einlass | °CRK | CAM_SP_REF_IN | - | signed integer | - | 0,0234375 | 1 | 0,0 |
| IWDKL | 0x4600 | STAT_DROSSELKLAPPENWINKEL_WERT | aktueller Drosselklappenwinkel | °TPS | TPS_AV | - | unsigned integer | - | 0,00729414634406567 | 1 | 0,0 |
| - | 0x4601 | STAT_DROSSELKLAPPENWINKEL_SOLL_WERT | Drosselklappe Sollwert aus Modell | °TPS | TPS_SP_MDL | - | unsigned integer | - | 0,00729414634406567 | 1 | 0,0 |
| SUGEB | 0x4602 | STAT_GENERATOR_SPANNUNG_BSD_SOLL_WERT | Generator Sollspannung über BSD | V | V_ALTER_SP | - | unsigned char | - | 0,100000001490116 | 1 | 10,6 |
| ITGEE | 0x4603 | STAT_GENERATOR_ELEKTRONIKTEMPERATUR_WERT | Chiptemperatur Generator 1 | °C | TCHIP | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| IIGEN | 0x4604 | STAT_GENERATOR_STROM_WERT | Generator Strom | - | I_GEN | - | unsigned char | - | 1,0 | 1 | 0,0 |
| VGENE | 0x4605 | STAT_GENERATOR_CHIPVERSION_WERT | Chipversion Generator 1 | - | BSDGENCV | - | unsigned char | - | 1,0 | 1 | 0,0 |
| VGENR | 0x4606 | STAT_GENERATOR_REGLERVERSION_WERT | Reglerversion Generator 1 | - | BSDGENREGV | - | unsigned char | - | 1,0 | 1 | 0,0 |
| VGENH | 0x4607 | STAT_GENERATOR_HERSTELLERCODE_WERT | Herstellercode Generator 1 | - | GEN_MANUFAK | - | unsigned char | - | 1,0 | 1 | 0,0 |
| VGTYP | 0x4608 | STAT_GENERATOR_TYP_WERT | Kennung Generatortyp Generator 1 | - | GEN_TYPKENN | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IUK87 | 0x4609 | STAT_KL87_SPANNUNG_WERT | Kl.87 Spannung / Versorgung DME | V | VB | - | unsigned char | - | 0,101562492549419 | 1 | 0,0 |
| IUBAT | 0x460A | STAT_UBATT_WERT | Batteriespannung aktuell | V | UBT | - | unsigned integer | - | 0,0149999996647239 | 1 | 0,0 |
| IUIBS | 0x460B | STAT_UBATT_IBS_WERT | Batteriespannung von IBS gemessen | - | U_BATT | - | unsigned integer | - | 2,50000011874363E-4 | 1 | 6,0 |
| IUADW | 0x460C | STAT_UBATT_AD_WANDLER_WERT | Batteriespannung vom AD-Wandler DME | V | VB_BAS | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| - | 0x460D | STAT_0x460D_WERT | Korrekturwert Abschaltung | - | ABSCH_KORR | - | signed integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x460E | STAT_0x460E_WERT | Abstand zur Startfähigkeitsgrenze | - | D_SOC | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| ILBAT | 0x460F | STAT_BATTERIELAST_WERT | Batterielast | % | LOAD_BAT | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IPDIS | 0x4610 | STAT_DISAKLAPPEN_POSITION_WERT | aktuelle Position Disaklappen | % | VIM_AV | - | unsigned integer | - | 0,00305175711400807 | 1 | 0,0 |
| STELU | 0x4611 | STAT_E_LUEFTER_PWM_SOLL_WERT | Sollwert E-Lüfter als PWM Wert | % | N_PERC_ECF | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x4612 | STAT_0x4612_WERT | Erregerstrom Generator 1 | A | IERR | - | unsigned char | - | 0,125 | 1 | 0,0 |
| - | 0x4613 | STAT_0x4613_WERT | Kopierter Wert von zum Generator gesendeter Sollspannung Generator 1 | V | U_FGEN | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| - | 0x4614 | STAT_0x4614_WERT | Auslastungsgrad Generator 1 | % | DFSIGGEN | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x4615 | STAT_0x4615_WERT | Kopie begrenzter Erregerstrom Generator 1 | A | IERRFGRENZ | - | unsigned char | - | 0,125 | 1 | 0,0 |
| - | 0x4616 | STAT_0x4616_WERT | Kopie Generator 1 LR Vorgabe auf Bus gelegt | s | TLRFGEN | - | unsigned char | - | 0,100000001490116 | 1 | 0,0 |
| - | 0x4617 | STAT_0x4617_WERT | gefiltertes Generatormoment absolut Ausgang | Nm | MD_GENNM | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| - | 0x4618 | STAT_0x4618_WERT | Kopie Drehzahlschwelle für LR-Funktion Generator 1 aktiv | 0/1 | B_LRFOFF | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x4619 | STAT_0x4619_WERT | Bedingung BSD II Protokoll | 0/1 | B_BSDPROT2 | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x461A | STAT_0x461A_WERT | Nominale Generatorspannung | V | UREGNOM | - | unsigned integer | - | 0,100000001490116 | 1 | 0,0 |
| ISBV1 | 0x4700 | STAT_SONDENBEREITSCHAFT_VORKAT_BANK1 | Status Lambdasonde betriebsbereit vor Katalysator Bank 1 | 0/1 | LV_INH_LSCL[1] | - | 0xFF | - | 1 | 1 | 0 |
| ISBV2 | 0x4701 | STAT_SONDENBEREITSCHAFT_VORKAT_BANK2 | Status Lambdasonde betriebsbereit vor Katalysator Bank 2 | 0/1 | LV_INH_LSCL[2] | - | 0xFF | - | 1 | 1 | 0 |
| IUSO1 | 0x4702 | STAT_SONDENSPANNUNG_VORKAT_BANK1_MIT_OFFSET_WERT | Spannung Lambdasonde vor Katalysator Bank 1 mit Offsetkorrektur | V | VLS_UP_COR[1] | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUSO2 | 0x4703 | STAT_SONDENSPANNUNG_VORKAT_BANK2_MIT_OFFSET_WERT | Spannung Lambdasonde vor Katalysator Bank 2 mit Offsetkorrektur | V | VLS_UP_COR[2] | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| SINT1 | 0x4704 | STAT_LAMBDA_BANK1_SOLL_WERT | Lambda Sollwert Bank 1 | - | LAMB_BAS[1] | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| SINT2 | 0x4705 | STAT_LAMBDA_BANK2_SOLL_WERT | Lambda Sollwert Bank 2 | - | LAMB_BAS[2] | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| ISKUB | 0x4800 | STAT_KUPPLUNGSSCHALTER_BETAETIGT_WERT | Kupplungsschalter Status | 0/1 | LV_CS | - | 0xFF | - | 1 | 1 | 0 |
| ISKUV | 0x4801 | STAT_KUPPLUNGSSCHALTER_VORHANDEN_WERT | Kupplungsschalter vorhanden | 0/1 | LV_CS_CUS | - | 0xFF | - | 1 | 1 | 0 |
| ISSPO | 0x4802 | STAT_SPORTTASTER_BETAETIGT_WERT | Sporttaster aktiv | 0/1 | LV_SOF_SWI | - | 0xFF | - | 1 | 1 | 0 |
| ISKLI | 0x4803 | STAT_KLIMA_EIN | Status Klima ein | - | STATE_ACIN_CAN | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ISSRC | 0x4805 | STAT_STARTRELAIS_UEBER_CAN_WERT | Startrelais über CAN aktiv | 0/1 | LV_RLY_ST_CAN | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x4806 | STAT_0x4806_WERT | Steuergeräte-Innentemperatur | °C | TECU | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| INMOT | 0x4807 | STAT_MOTORDREHZAHL_WERT | Motor Drehzahl | rpm | N | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| SNLLD | 0x4808 | STAT_LEERLAUFDREHZAHL_SOLL_WERT | Leerlauf Solldrehzahl | rpm | N_SP_IS | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| ISLLA | 0x4809 | STAT_LEERLAUF_AKTIV | Status LL | 0/1 | LV_IS | - | 0xFF | - | 1 | 1 | 0 |
| ISKME | 0x480A | STAT_KILOMETERSTAND_WERT | Kilometerstand Auflösung 1 km | km | CTR_KM_BN | - | unsigned long | - | 1,0 | 1 | 0,0 |
| IFPWG | 0x480B | STAT_FAHRERWUNSCH_PEDAL_WERT | Pedalwert Fahrerwunsch in % | % | PV_AV | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5800 | STAT_0x5800_WERT | Zeit nach Start | s | OBD_T_AST | - | unsigned char | - | 256,0 | 1 | 0,0 |
| - | 0x5801 | STAT_0x5801_WERT | Umgebungsdruck | kPa | OBD_AMP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ICLR1 | 0x5802 | STAT_LAMBDAREGELUNG_ZUSTAND_BANK1_WERT | Zustand Lambdaregelung Bank 1 | 0-n | STATE_LS[1] | - | 0xFF | _CNV_S_5_LACO_RANGE_410 | 1 | 1 | 0 |
| ICLR2 | 0x5803 | STAT_LAMBDAREGELUNG_ZUSTAND_BANK2_WERT | Zustand Lambdaregelung Bank 2 | 0-n | STATE_LS[2] | - | 0xFF | _CNV_S_5_LACO_RANGE_410 | 1 | 1 | 0 |
| SLAST | 0x5804 | STAT_LASTWERT_BERECHNET_WERT | Berechneter Lastwert | % | LOAD_CLC | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5805 | STAT_0x5805_WERT | Kühlmitteltemperatur OBD | °C | OBD_TCO | - | unsigned char | - | 1,0 | 1 | -40,0 |
| ILIN1 | 0x5806 | STAT_LAMBDA_INTEGRATOR_GRUPPE1_WERT | Lambda Integrator Gruppe 1 | % | OBD_LAM_COR[1] | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| ILAM1 | 0x5807 | STAT_LAMBDA_ADAPTION_MULTIPLIKATIV_GRUPPE1_WERT | Lambda Adaption Summe mul. und add. Gruppe 1 | % | OBD_LAM_AD[1] | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| ILIN2 | 0x5808 | STAT_LAMBDA_INTEGRATOR_GRUPPE2_WERT | Lambda Integrator Gruppe 2 | % | OBD_LAM_COR[2] | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| ILAM2 | 0x5809 | STAT_LAMBDA_ADAPTION_MULTIPLIKATIV_GRUPPE2_WERT | Lambda Adaption Summe mul. und add. Gruppe 2 | % | OBD_LAM_AD[2] | - | unsigned char | - | 0,78125 | 1 | -100,000002235174 |
| IPSA2 | 0x580B | STAT_SAUGROHRDRUCK_2_WERT | Saugrohrdruck | kPa | OBD_MAP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| INAUF | 0x580C | STAT_N_AUFLOESUNG_WERT | Drehzahl | rpm | OBD_N | - | unsigned char | - | 64,0 | 1 | 0,0 |
| IVKM2 | 0x580D | STAT_GESCHWINDIGKEIT_2_WERT | Geschwindigkeit | km/h | VS | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IZZY1 | 0x580E | STAT_ZUENDZEITPUNKT_ZYL1_WERT | Zündzeitpunkt Zylinder 1 | °CRK | OBD_IGA_IGC | - | unsigned char | - | 0,5 | 1 | -64,0 |
| ITANL | 0x580F | STAT_ANSAUGLUFTTEMPERATUR_LAW_WERT | Ansauglufttemperatur | °C | OBD_TIA | - | unsigned char | - | 1,0 | 1 | -40,0 |
| ILMGS | 0x5810 | STAT_LUFTMASSE_GRAMM_PRO_SEKUNDE_WERT | Luftdurchsatz OBD | g/s | OBD_MAF | - | unsigned char | - | 2,5599999427795406 | 1 | 0,0 |
| INM32 | 0x5811 | STAT_MOTORDREHZAHL_N32_WERT | Motordrehzahl | rpm | N_32 | - | unsigned char | - | 32,0 | 1 | 0,0 |
| - | 0x5812 | STAT_0x5812_WERT | Luftmasse gemessen | kg/h | MAF_KGH_MES_BAS | - | unsigned char | - | 8,0 | 1 | 0,0 |
| ILREL | 0x5813 | STAT_LASTWERT_RELATIV_WERT | Relative Last | % | RF | - | signed char | - | 2,5599999427795406 | 1 | 0,0 |
| - | 0x5814 | STAT_0x5814_WERT | Fahrpedalwert | % | PV_AV_RAW | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5815 | STAT_0x5815_WERT | Batteriespannung | V | OBD_VB | - | unsigned char | - | 0,2560000121593472 | 1 | 0,0 |
| - | 0x5816 | STAT_0x5816_WERT | Lambda Setpoint | - | OBD_LAMB_SP | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| - | 0x5817 | STAT_0x5817_WERT | Umgebungstemperatur | °C | OBD_TAM | - | unsigned char | - | 1,0 | 1 | -40,0 |
| ILMMG | 0x5818 | STAT_LUFTMASSE_PRO_HUB_WERT | Luftmasse gerechnet | mg/stk | MAF | - | unsigned char | - | 5,425863742828365 | 1 | 0,0 |
| - | 0x5819 | STAT_0x5819_WERT | Drehzahl OBD Byte | rpm | N_SAE_BYTE_KWP | - | unsigned char | - | 64,0 | 1 | 0,0 |
| - | 0x581A | STAT_0x581A_WERT | Nockenwelle Einlass | °CRK | CAM_IN[1] | - | unsigned char | - | 0,375 | 1 | 59,9999982118607 |
| - | 0x581B | STAT_0x581B_WERT | Nockenwelle Einlass Sollwert | °CRK | CAM_SP_IVVT_IN | - | unsigned char | - | 0,375 | 1 | 59,9999982118607 |
| - | 0x581C | STAT_0x581C_WERT | Nockenwelle Auslass | °CRK | CAM_EX[1] | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| - | 0x581D | STAT_0x581D_WERT | Nockenwelle Auslass Sollwert | °CRK | CAM_SP_IVVT_EX | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| - | 0x581E | STAT_0x581E_WERT | Ansauglufttemperatur | °C | TIA_MES | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x581F | STAT_0x581F_WERT | Motortemperatur | °C | TCO_MES | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x5820 | STAT_0x5820_WERT | Kühlmitteltemperatur Kühlerausgang | °C | TCO_2_MES | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x5821 | STAT_0x5821_WERT | Steuergeräte-Innentemperatur | °C | TECU | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x5822 | STAT_0x5822_WERT | (Motor)-Öltemperatur | °C | TOIL_MES | - | unsigned char | - | 1,0 | 1 | -40,0 |
| IZMOS | 0x5823 | STAT_ZEIT_MOTOR_STEHT_WERT | Zeit Motor steht | min | T_ES | - | unsigned char | - | 256,0 | 1 | 0,0 |
| - | 0x5824 | STAT_0x5824_WERT | Umgebungstemperatur | °C | TAM | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x5825 | STAT_0x5825_WERT | Abstellzeit | min | T_ES_CUS_KWP | - | unsigned char | - | 4,0 | 1 | 0,0 |
| IDKS1 | 0x5826 | STAT_DROSSELKLAPPE_SENSOR1_WERT | Drosselklappe Sensor 1 | °TPS | TPS_AV_1 | - | unsigned char | - | 1,8673014640808114 | 1 | 0,0 |
| - | 0x5827 | STAT_0x5827_WERT | Lambdasondenheizung vor Katalysator Bank 1 | % | LSHPWM_UP[1] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5828 | STAT_0x5828_WERT | Lambdasondenheizung vor Katalysator Bank 2 | % | LSHPWM_UP[2] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5829 | STAT_0x5829_WERT | Lambdasondenheizung hinter Katalysator Bank 1 | % | LSHPWM_DOWN[1] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x582A | STAT_0x582A_WERT | Lambdasondenheizung hinter Katalysator Bank 2 | % | LSHPWM_DOWN[2] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IDRCA | 0x582B | STAT_DREHMOMENTEINGRIFF_CAN_WERT | Drehmomenteingriff über CAN | - | STATE_TQ_CAN_PLAUS | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x582C | STAT_0x582C_WERT | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 1 | - | CTR_ERR_LSL_IF_SPI_WR[1] | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x582D | STAT_0x582D_WERT | Anzahl ungültiger Schreibüberprüfungszyklen am SPI-Interface der Lambdasonde vor Katalysator Bank 2 | - | CTR_ERR_LSL_IF_SPI_WR[2] | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x582E | STAT_0x582E_WERT | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 1 | - | FAC_DIAG_DYN_LSL_UP[1] | - | unsigned char | - | 0,25 | 1 | 0,0 |
| - | 0x582F | STAT_0x582F_WERT | Adaptionsfaktor Sensor Zeitkonstante vor Katalysator Bank 2 | - | FAC_DIAG_DYN_LSL_UP[2] | - | unsigned char | - | 0,25 | 1 | 0,0 |
| - | 0x5830 | STAT_0x5830_WERT | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 1 | - | FAC_MV_DIAG_DYN_LSL_UP_KWP[1] | - | unsigned char | - | 0,00400000018998981 | 1 | 0,0 |
| - | 0x5831 | STAT_0x5831_WERT | Mittelwert der normierten Signalamplitude der Lambdasonde vor Katalysator Bank 2 | - | FAC_MV_DIAG_DYN_LSL_UP_KWP[2] | - | unsigned char | - | 0,00400000018998981 | 1 | 0,0 |
| IMOST | 0x5832 | STAT_MOTOR_STATUS_WERT | Motor Status | 0-n | STATE_ENG | - | 0xFF | _CNV_S_6_RANGE_STAT_167 | 1 | 1 | 0 |
| - | 0x5833 | STAT_0x5833_WERT | Umgebungstemperatur beim Start | °C | TAM_ST | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x5834 | STAT_0x5834_WERT | Umgebungsdruck | hPa | AMP_MES | - | unsigned char | - | 21,226886749267585 | 1 | 0,0 |
| - | 0x5835 | STAT_0x5835_WERT | Herstellercode Generator 1 | - | GEN_MANUFAK | - | unsigned char | - | 1,0 | 1 | 0,0 |
| INGRD | 0x5836 | STAT_DREHZAHLGRADIENT_WERT | Drehzahlgradient | rpm/s | N_GRD | - | signed char | - | 32,0 | 1 | 0,0 |
| - | 0x5837 | STAT_0x5837_WERT | Status OBD-I Fehler vor Katalysator Bank 1 | 0-n | STATE_ERR_EL_LSL_UP[1] | - | 0xFF | _CNV_S_11_EGCP_RANGE_375 | 1 | 1 | 0 |
| - | 0x5838 | STAT_0x5838_WERT | Status OBD-I Fehler vor Katalysator Bank 2 | 0-n | STATE_ERR_EL_LSL_UP[2] | - | 0xFF | _CNV_S_11_EGCP_RANGE_375 | 1 | 1 | 0 |
| ISDKN | 0x5839 | STAT_DROSSELKLAPPE_NOTLAUF_WERT | Status Drosselklappe Notlauf | 0-n | STATE_ETC_LIH | - | 0xFF | _CNV_S_5_RANGE_STAT_290 | 1 | 1 | 0 |
| - | 0x583A | STAT_0x583A_WERT | Ansauglufttemperatur beim Start | °C | TIA_ST | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| IKTFS | 0x583B | STAT_KRAFTSTOFFTANK_FUELLSTAND_WERT | Kraftstofftank Füllstand | l | FTL | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x583C | STAT_0x583C_WERT | Spannung Kl. 87 | V | VB | - | unsigned char | - | 0,101562492549419 | 1 | 0,0 |
| - | 0x583D | STAT_0x583D_WERT | Resettyp | - | RST_CLAS_TYP[0] | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x583E | STAT_0x583E_WERT | Motordrehzahl bei Reset | rpm | N_RST_DET_KWP | - | unsigned char | - | 32,0 | 1 | 0,0 |
| - | 0x583F | STAT_0x583F_WERT | Drosselklappe Sollwert | °TPS | TPS_SP | - | unsigned char | - | 1,8673014640808114 | 1 | 0,0 |
| - | 0x5840 | STAT_0x5840_WERT | CPU Last bei Reset | % | CPU_LOAD_RST_DET_KWP | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| RTSGR | 0x5841 | STAT_STEUERGERAETE_INNENTEMPERATUR_ROH_WERT | SG-Innentemperatur Rohwert | V | VP_TECU_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5842 | STAT_0x5842_WERT | Kennung Generatortyp Generator 1 | - | GEN_TYPKENN | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5843 | STAT_0x5843_WERT | Versorgung Fahrtwertgeber 1 | V | VCC_PVS_1_KWP | - | unsigned char | - | 0,0390625037252903 | 1 | 0,0 |
| - | 0x5844 | STAT_0x5844_WERT | Chiptemperatur Generator 1 | °C | TCHIP_KWP | - | unsigned char | - | 1,0 | 1 | -48,0 |
| - | 0x5845 | STAT_0x5845_WERT | Spannung Lambdasonde vor Katalysator Bank 1 | V | VLS_UP_KWP[1] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5846 | STAT_0x5846_WERT | Spannung Pedalwertgeber 1 | V | V_PVS_1_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5847 | STAT_0x5847_WERT | Spannung Pedalwertgeber 2 | V | V_PVS_2_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5848 | STAT_0x5848_WERT | Spannung Lambdasonde vor Katalysator Bank 2 | V | VLS_UP_KWP[2] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5849 | STAT_0x5849_WERT | Spannung Lambdasonde hinter Katalysator Bank 1 | V | VLS_DOWN_KWP[1] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| RUK15 | 0x584A | STAT_KL15_SPANNUNG_ROH_WERT | Spannung Kl. 15 Rohwert | V | V_IGK_BAS_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x584B | STAT_0x584B_WERT | Spannung Lambdasonde hinter Katalysator Bank 2 | V | VLS_DOWN_KWP[2] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x584C | STAT_0x584C_WERT | Spannung Drosselklappe Potentiometer 2 | V | V_TPS_2_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| SQTEK | 0x584D | STAT_TANKENTLUEFTUNG_DURCHFLUSS_SOLL_WERT | korrigierter Sollwert Durchfluss Tankentlüftung | kg/h | FLOW_COR_CPS | - | unsigned char | - | 0,03125 | 1 | 0,0 |
| - | 0x584E | STAT_0x584E_WERT | Spannung Drosselklappe Potentiometer 1 | V | V_TPS_1_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x584F | STAT_0x584F_WERT | Spannung Luftmasse | V | V_MAF | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| - | 0x5850 | STAT_0x5850_WERT | Spannung Motortemperatur | V | V_TCO_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5851 | STAT_0x5851_WERT | Spannung Ansauglufttemperatur | V | VP_TIA_KWP | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| - | 0x5852 | STAT_0x5852_WERT | Kühlmitteltemperatur Kühlerausgang Rohwert | V | V_TCO_2_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5853 | STAT_0x5853_WERT | Spannung Kl.87 Rohwert | V | VB_BAS_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5854 | STAT_0x5854_WERT | Versorgung Fahrtwertgeber 2 | V | VCC_PVS_2_KWP | - | unsigned char | - | 0,0390625037252903 | 1 | 0,0 |
| - | 0x5855 | STAT_0x5855_WERT | Mittelwert Bank 1 | % | FAC_LAM_MV_MMV[1] | - | signed char | - | 0,390625 | 1 | 2,22044609888115E-14 |
| - | 0x5856 | STAT_0x5856_WERT | Mittelwert Bank 2 | % | FAC_LAM_MV_MMV[2] | - | signed char | - | 0,390625 | 1 | 2,22044609888115E-14 |
| - | 0x5857 | STAT_0x5857_WERT | Erregerstrom Generator 1 | A | IERR | - | unsigned char | - | 0,125 | 1 | 0,0 |
| - | 0x5858 | STAT_0x5858_WERT | Drosselklappe aktueller Wert | °TPS | TPS_AV | - | unsigned char | - | 1,8673014640808114 | 1 | 0,0 |
| - | 0x5859 | STAT_0x5859_WERT | DMTL Strom Referenzleck | mA | CUR_DMTL_REF_LEAK_KWP | - | unsigned char | - | 0,195312470197678 | 1 | 0,0 |
| - | 0x585A | STAT_0x585A_WERT | DMTL Strom Grobleck | mA | CUR_DMTL_ROUGH_LEAK_MIN_KWP | - | unsigned char | - | 0,195312470197678 | 1 | 0,0 |
| - | 0x585B | STAT_0x585B_WERT | DMTL Strom Diagnoseende | mA | CUR_DMTL_COR_FIL_KWP | - | unsigned char | - | 0,195312470197678 | 1 | 0,0 |
| - | 0x585C | STAT_0x585C_WERT | Widerstand Lambdasonde hinter Katalysator Bank 1 | ohm | R_IT_LS_DOWN_KWP_H[1] | - | unsigned char | - | 256,0 | 1 | 0,0 |
| IRLN2 | 0x585D | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT2_WERT | Widerstand Lambdasonde hinter Katalysator Bank 2 | ohm | R_IT_LS_DOWN_KWP_H[2] | - | unsigned char | - | 256,0 | 1 | 0,0 |
| IRUN1 | 0x585E | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT1_UNTERES_BYTE_WERT | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 1 | ohm | R_IT_LS_DOWN_KWP_L[1] | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IRUN2 | 0x585F | STAT_LAMBDASONDE_WIDERSTAND_NACHKAT2_UNTERES_BYTE_WERT | unteres Byte Widerstand Lambdasonde hinter Katalysator Bank 2 | ohm | R_IT_LS_DOWN_KWP_L[2] | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IRLV1 | 0x5860 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT1_WERT | Widerstand Lambdasonde vor Katalysator Bank 1 | ohm | R_IT_LS_UP_KWP_H[1] | - | unsigned char | - | 64,0 | 1 | 0,0 |
| IRLV2 | 0x5861 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT2_WERT | Widerstand Lambdasonde vor Katalysator Bank 2 | ohm | R_IT_LS_UP_KWP_H[2] | - | unsigned char | - | 64,0 | 1 | 0,0 |
| - | 0x5862 | STAT_0x5862_WERT | Öldruck Sollwert | hPa | P_OEL_SOLL_KWP | - | unsigned char | - | 32,0 | 1 | 0,0 |
| IRUV1 | 0x5863 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT1_UNTERES_BYTE_WERT | untere Byte Widerstand Lambdasonde vor Katalysator Bank 1 | ohm | R_IT_LS_UP_KWP_L[1] | - | unsigned char | - | 0,25 | 1 | 0,0 |
| IRUV2 | 0x5864 | STAT_LAMBDASONDE_WIDERSTAND_VORKAT2_UNTERES_BYTE_WERT | untere Byte Widerstand Lambdasonde vor Katalysator Bank 2 | ohm | R_IT_LS_UP_KWP_L[2] | - | unsigned char | - | 0,25 | 1 | 0,0 |
| - | 0x5865 | STAT_0x5865_WERT | Ölstand Mittelwert Langzeit | - | OZ_NIVLANGT | - | unsigned char | - | 0,29296875 | 1 | 0,0 |
| - | 0x5866 | STAT_0x5866_WERT | Füllstand Motoröl | - | OZ_LP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5867 | STAT_0x5867_WERT | Kilometerstand | km | CTR_KM_CAN_KWP | - | unsigned char | - | 2560,0 | 1 | 0,0 |
| ISSR1 | 0x5868 | STAT_STANDVERBRAUCHER_REGISTRIERT_TEIL1_WERT | Status Standverbraucher registriert Teil 1 | - | STAT_SV_REG1 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ISSR2 | 0x5869 | STAT_STANDVERBRAUCHER_REGISTRIERT_TEIL2_WERT | Status Standverbraucher registriert Teil 2 | - | STAT_SV_REG2 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x586A | STAT_0x586A_WERT | Batteriespannung von IBS gemessen | - | U_BATT | - | unsigned char | - | 0,06400000303983693 | 1 | 6,0 |
| IZR82 | 0x586B | STAT_ZEIT_MIT_RUHESTROM_80_200_WERT | Zeit mit Ruhestrom 80 - 200 mA | min | T2HISTSHORT | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| IZR21 | 0x586C | STAT_ZEIT_MIT_RUHESTROM_200_1000_WERT | Zeit mit Ruhestrom 200 - 1000 mA | min | T3HISTSHORT | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| IZSST | 0x586D | STAT_ZAEHLER_ERKENNUNG_SCHLECHTE_STRASSE_WERT | Zähler Erkennung schlechte Strasse | - | SUM_RR | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IZRG1 | 0x586E | STAT_ZEIT_MIT_RUHESTROM_GROESER_1000_WERT | Zeit mit Ruhestrom größer 1000 mA | min | T4HISTSHORT | - | unsigned char | - | 14,9333333969116 | 1 | 0,0 |
| - | 0x586F | STAT_0x586F_WERT | Ist-Öldruck | hPa | P_OEL_IST_KWP | - | unsigned char | - | 32,0 | 1 | 0,0 |
| - | 0x5870 | STAT_0x5870_WERT | Spannung DME Umgebungsdruck | V | V_AMP_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| SLAG1 | 0x5871 | STAT_LAMBDA_SOLLWERT_GRUPPE1_WERT | Lambda-Sollwert Gruppe 1 | - | LAMB_SP_KWP[1] | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
|  | 0x5872 | STAT_5872_WERT | Reglerversion Generator 1 | - | BSDGENREGV | - | unsigned char | - | 1,0 | 1 | 0,0 |
| SLAG2 | 0x5873 | STAT_LAMBDA_SOLLWERT_GRUPPE2_WERT | Lambda-Sollwert Gruppe 2 | - | LAMB_SP_KWP[2] | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| - | 0x5874 | STAT_0x5874_WERT | Spannung Strommessung DMTL | V | V_DMTL_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5875 | STAT_0x5875_WERT | Sollwert Motormoment | Nm | TQI_SP_KWP | - | signed char | - | 2,0 | 1 | 0,0 |
| - | 0x5876 | STAT_0x5876_WERT | Raildruck OBD (High Byte) | kPa | OBD_FUP_RNG_H_H | - | unsigned char | - | 2560,0 | 1 | 0,0 |
| - | 0x5877 | STAT_0x5877_WERT | Raildruck OBD (Low Byte) | kPa | OBD_FUP_RNG_H_L | - | unsigned char | - | 10,0 | 1 | 0,0 |
| ILRR1 | 0x5878 | STAT_LAMBDAVERSCHIEBUNG_RUECKFUEHRREGLER1_WERT | Lambdaverschiebung Rückführregler 1 | - | LAMB_DELTA_I_LAM_ADJ_KWP[1] | - | signed char | - | 9,765625E-4 | 1 | 0,0 |
| ILRR2 | 0x5879 | STAT_LAMBDAVERSCHIEBUNG_RUECKFUEHRREGLER2_WERT | Lambdaverschiebung Rückführregler 2 | - | LAMB_DELTA_I_LAM_ADJ_KWP[2] | - | signed char | - | 9,765625E-4 | 1 | 0,0 |
| ISFGR | 0x587A | STAT_FGR_WERT | Status FGR | 0-n | STATE_CRU | - | 0xFF | _CNV_S_6_RANGE_STAT_106 | 1 | 1 | 0 |
| - | 0x587B | STAT_0x587B_WERT | Abgleich Abgasrückführungsventilmodell (Faktor) | - | EISYAGR_KORFAK_B | - | unsigned char | - | 0,125 | 1 | 0,0 |
| ISMST | 0x587C | STAT_MOTORSTEUERUNG_WERT | Status Motorsteuerung | 0-n | ECU_STATE | - | 0xFF | _CNV_S_7_RANGE_ECU__165 | 1 | 1 | 0 |
| - | 0x587D | STAT_0x587D_WERT | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 1 | 0-n | STATE_SYM_DIAG_PUC_LSL_UP[1] | - | 0xFF | _CNV_S_4_EGCP_RANGE_384 | 1 | 1 | 0 |
| - | 0x587E | STAT_0x587E_WERT | Symptom bei Schubabschaltung Sonde vor Katalysator Bank 2 | 0-n | STATE_SYM_DIAG_PUC_LSL_UP[2] | - | 0xFF | _CNV_S_4_EGCP_RANGE_384 | 1 | 1 | 0 |
| IELTV | 0x587F | STAT_E_LUEFTER_TASTVERHAELTNIS_WERT | Tastverhältnis E-Lüfter | % | ECFPWM[0] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5880 | STAT_0x5880_WERT | Tastverhältnis Luftklappe | % | ECRASPWM | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| SBEGA | 0x5881 | STAT_BERECHNETER_GANG_WERT | berechneter Gang | - | GEAR | - | unsigned char | - | 1,0 | 1 | 0,0 |
| ITMOS | 0x5882 | STAT_MOTORTEMPERATUR_BEIM_START_WERT | Motortemperatur beim Start | °C | TCO_ST | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x5883 | STAT_0x5883_WERT | Spannung Klopfwerte Zylinder 1 | V | NL[0] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5884 | STAT_0x5884_WERT | Rückgelesener Erregergrenzstrom Generator 1 | A | IERRFGRENZ | - | unsigned char | - | 0,125 | 1 | 0,0 |
| - | 0x5885 | STAT_0x5885_WERT | Spannung Klopfwerte Zylinder 3 | V | NL[2] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5886 | STAT_0x5886_WERT | Spannung Klopfwerte Zylinder 6 | V | NL[3] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x5887 | STAT_0x5887_WERT | Auslastungsgrad Generator 1 | % | DFSIGGEN | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5888 | STAT_0x5888_WERT | Spannung Klopfwerte Zylinder 4 | V | NL[5] | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| ILAG1 | 0x5889 | STAT_LAMBDA_ISTWERT_GRUPPE1_WERT | Lambda-Istwert Gruppe 1 | - | LAMB_KWP[1] | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| ILAG2 | 0x588A | STAT_LAMBDA_ISTWERT_GRUPPE2_WERT | Lambda-Istwert Gruppe 2 | - | LAMB_KWP[2] | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| IZSSE | 0x588B | STAT_ZEIT_SEIT_STARTENDE_WERT | Zeit seit Startende | s | T_AST | - | unsigned char | - | 25,600000381469695 | 1 | 0,0 |
| ITKV1 | 0x588C | STAT_LAMBDASONDE_KERAMIKTEMPERATUR_VORKAT1_WERT | Keramiktemperatur Lambdasonde vor Katalysator Bank 1 | °C | TTIP_MES_LS_UP[1] | - | signed char | - | 16,0 | 1 | 0,0 |
| IZDML | 0x588D | STAT_ZEIT_DMTL_LECKMESSUNG_WERT | aktuelle Zeit DMTL Leckmessung | s | T_ACT_LEAK_MES | - | unsigned char | - | 25,600000381469695 | 1 | 0,0 |
| IIDMP | 0x588E | STAT_PUMPENSTROM_BEI_DMTL_PUMPENPRUEFUNG_WERT | Pumpenstrom bei DMTL Pumpenprüfung | mA | CUR_DMTL_DMTLS_TEST | - | unsigned char | - | 1,5625238418579097 | 1 | 0,0 |
| ITKV2 | 0x588F | STAT_LAMBDASONDE_KERAMIKTEMPERATUR_VORKAT2_WERT | Keramiktemperatur Lambdasonde vor Katalysator Bank 2 | °C | TTIP_MES_LS_UP[2] | - | signed char | - | 16,0 | 1 | 0,0 |
| - | 0x5890 | STAT_0x5890_WERT | Spannung Bremsunterdrucksensor | V | V_PBSU_KWP | - | unsigned char | - | 0,0195312164723873 | 1 | 0,0 |
| IMOKU | 0x5891 | STAT_MOMENTANFORDERUNG_KUPPLUNG_WERT | Momentanforderung an der Kupplung | Nm | TQ_REQ_CLU | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x5892 | STAT_0x5892_WERT | Bremsunterdruck | hPa | PBSU_KWP | - | unsigned char | - | 5,306640625 | 1 | 0,0 |
| IDMGW | 0x5893 | STAT_DREHMOMENTABFALL_BEIM_GANGWECHSEL_WERT | Drehmomentabfall schnell bei Gangwechsel | Nm | TQI_GS_FAST_DEC | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x5894 | STAT_0x5894_WERT | Symptom Lambdasondenheizung vor Katalysator Bank 1 | 0-n | STATE_SYM_OBD_LSL_LSH_UP[1] | - | 0xFF | _CNV_S_4_EGCP_RANGE_377 | 1 | 1 | 0 |
| - | 0x5895 | STAT_0x5895_WERT | Symptom Lambdasondenheizung vor Katalysator Bank 2 | 0-n | STATE_SYM_OBD_LSL_LSH_UP[2] | - | 0xFF | _CNV_S_4_EGCP_RANGE_377 | 1 | 1 | 0 |
| - | 0x5896 | STAT_0x5896_WERT | Abgastemperatur hinter Katalysator Bank 1 | °C | TEG_CAT_DOWN_MDL[1] | - | unsigned char | - | 16,0 | 1 | 0,0 |
| - | 0x5897 | STAT_0x5897_WERT | Abgastemperatur hinter Katalysator Bank 2 | °C | TEG_CAT_DOWN_MDL[2] | - | unsigned char | - | 16,0 | 1 | 0,0 |
| SUGEN | 0x5898 | STAT_GENERATOR_SPANNUNG_SOLL_WERT | Generator Sollspannung | V | V_ALTER_SP_KWP | - | unsigned char | - | 0,100000001490116 | 1 | 0,0 |
| - | 0x5899 | STAT_0x5899_WERT | Istwert DISA-Position | % | VIM_AV | - | unsigned char | - | 0,7812498211860659 | 1 | 0,0 |
| - | 0x589A | STAT_0x589A_WERT | Tastverhältnis Nullgangsensor | % | PWM_NEUT_PSN_GB_KWP | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IUOS1 | 0x589B | STAT_SPANNUNGSOFFSET_SIGNALPFAD1_WERT | Spannungsoffset Signalpfad CJ120 1 | V | VLS_OFS_LSL_KWP[1] | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| IUOS2 | 0x589C | STAT_SPANNUNGSOFFSET_SIGNALPFAD2_WERT | Spannungsoffset Signalpfad CJ120 2 | V | VLS_OFS_LSL_KWP[2] | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| - | 0x589D | STAT_0x589D_WERT | Abweichung Lambdasonde zu Lambdamodellwert Überwachung | - | LAMB_DIF_MON_KWP | - | signed char | - | 0,0156249795109034 | 1 | -2,50980372710279E-6 |
| IZMAB | 0x58A8 | STAT_MOTORABSTELLZEIT_WERT | Motorabstellzeit | min | T_ES_KWP | - | unsigned char | - | 4,0 | 1 | 0,0 |
| - | 0x58A9 | STAT_0x58A9_WERT | Resetzähler Rechnerüberwachung: alter Wert | - | ENVD_3_MON_3 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58AA | STAT_0x58AA_WERT | Fehlercode Rechnerüberwachung: alter Wert | - | ENVD_2_MON_3 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IADK1 | 0x58AB | STAT_ABWEICHUNG_DK_POTI1_WERT | Abweichung DK-Potentiometer 1 und Modellwert | °TPS | TPS_DIF_DIAG_COR_1_KWP | - | unsigned char | - | 0,466825366020203 | 1 | 0,0 |
| IADK2 | 0x58AC | STAT_ABWEICHUNG_DK_POTI2_WERT | Abweichung DK-Potentiometer 2 und Modellwert | °TPS | TPS_DIF_DIAG_COR_2_KWP | - | unsigned char | - | 0,466825366020203 | 1 | 0,0 |
| IPWG1 | 0x58AD | STAT_PEDALWERTGEBER1_WERT | Pedalwertgeber 1 | % | PV_AV_1 | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x58AE | STAT_0x58AE_WERT | Periodendauer Luftmasse | us | T_PER_MAF_FRQ_KWP | - | unsigned char | - | 256,0 | 1 | 0,0 |
| IKRAN | 0x58AF | STAT_KRAFTSTOFF_ANFORDERUNG_AN_PUMPE_WERT | Kraftstoff Anforderung an Pumpe | l/h | VFF_EFP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IDKAD | 0x58B0 | STAT_DK_ADAPTIONSSCHRITT_WERT | DK-Adaptionsschritt | - | TPS_AD_STEP_KWP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IZFZ1 | 0x58B1 | STAT_FUNKENBRENNDAUER_ZYL1_WERT | Funkenbrenndauer Zylinder 1 | ms | V_DUR_IGC_0 | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| IZFZ5 | 0x58B2 | STAT_FUNKENBRENNDAUER_ZYL5_WERT | Funkenbrenndauer Zylinder 5 | ms | V_DUR_IGC_1 | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| IZFZ3 | 0x58B3 | STAT_FUNKENBRENNDAUER_ZYL3_WERT | Funkenbrenndauer Zylinder 3 | ms | V_DUR_IGC_2 | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| IZFZ6 | 0x58B4 | STAT_FUNKENBRENNDAUER_ZYL6_WERT | Funkenbrenndauer Zylinder 6 | ms | V_DUR_IGC_3 | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| IZFZ2 | 0x58B5 | STAT_FUNKENBRENNDAUER_ZYL2_WERT | Funkenbrenndauer Zylinder 2 | ms | V_DUR_IGC_4 | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| IZFZ4 | 0x58B6 | STAT_FUNKENBRENNDAUER_ZYL4_WERT | Funkenbrenndauer Zylinder 4 | ms | V_DUR_IGC_5 | - | unsigned char | - | 1,0240000486373915 | 1 | 0,0 |
| IPBRE | 0x58B7 | STAT_BREMSDRUCK_WERT | Bremsdruck | bar | BRAKE_PRS | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58B8 | STAT_0x58B8_WERT | Drehzahl Überwachung | rpm | N_32_MON | - | unsigned char | - | 32,0 | 1 | 0,0 |
| - | 0x58B9 | STAT_0x58B9_WERT | Pedalwert Überwachung | % | PV_AV_MON | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x58BA | STAT_0x58BA_WERT | eingespritze Kraftstoffmasse | l/h | VFF_MFF_SP_FUP_CTL_KWP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58BB | STAT_0x58BB_WERT | PWM Kraftstoffpumpe | % | EFPPWM_KWP | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x58BC | STAT_0x58BC_WERT | Luftmasse Überwachung | mg/stk | MAF_MON | - | unsigned char | - | 5,44705867767334 | 1 | 0,0 |
| - | 0x58BF | STAT_0x58BF_WERT | relative Momentenforderung von MSR über CAN | % | TQI_MSR_CAN | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x58C0 | STAT_0x58C0_WERT | Motordrehzahl Ersatzwert Überwachung | rpm | N_32_SUB_MON | - | unsigned char | - | 32,0 | 1 | 0,0 |
| ITLSZ | 0x58C1 | STAT_LAUFUNRUHE_SEGMENTZEIT_WERT | Laufunruhe Segmentzeit | µs | SEG_T_MES | - | unsigned char | - | 256,0 | 1 | 0,0 |
| - | 0x58C2 | STAT_0x58C2_WERT | Statusbyte MFF-Monitoring | - | STATE_LV_ERR_MFF_MON_1 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58C3 | STAT_0x58C3_WERT | Statusbyte ISC-Monitoring | - | STATE_LV_ERR_TQ_DIF_ISC_MON_1 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58C4 | STAT_0x58C4_WERT | Statusbyte CRU-Monitoring | - | STATE_LV_ERR_CRU_INH_MON_1 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58C5 | STAT_0x58C5_WERT | Drehzahl Überwachung (resetsicher) | rpm | N_32_MON_SAVE | - | unsigned char | - | 32,0 | 1 | 0,0 |
| - | 0x58C6 | STAT_0x58C6_WERT | Status Einspritzventile (resetsicher) | - | PREV_STATE_IV_SAVE | - | unsigned char | - | 1,0 | 1 | 0,0 |
| INSUE | 0x58C7 | STAT_LEERLAUF_SOLLDREHZAHLABWEICHUNG_WERT | LL-Solldrehzahlabweichung Überwachung | rpm | N_DIF_SP_IS_MON | - | signed char | - | 32,0 | 1 | 0,0 |
| - | 0x58C8 | STAT_0x58C8_WERT | I-Anteil Momentdifferenz Überwachung und Modell | Nm | TQ_DIF_I_IS_MON | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58C9 | STAT_0x58C9_WERT | I-Anteil LL passive Rampe aktiv | 0/1 | LV_PAS_RAMP_ACT_I_IS | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x58CA | STAT_0x58CA_WERT | PD-Anteil langsam Leerlaufregelung | Nm | TQ_DIF_P_D_SLOW_IS | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58CB | STAT_0x58CB_WERT | PD-Anteil schnell Leerlaufregelung | Nm | TQ_DIF_P_D_FAST_IS | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58CC | STAT_0x58CC_WERT | Verlustmoment Überwachung | Nm | TQ_LOSS_MON | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58CD | STAT_0x58CD_WERT | Verlustmomentabweichung Überwachung | Nm | TQ_LOSS_DIF_MON | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58CE | STAT_0x58CE_WERT | Carrierbyte Schalterstati | - | STATE_BYTE_SWI_KWP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| SMOMO | 0x58CF | STAT_MOTORMOMENT_SOLL_WERT | Motormoment Sollwert Überwachung | Nm | TQI_SP_MON | - | unsigned char | - | 2,0 | 1 | 0,0 |
| IMOMO | 0x58D0 | STAT_MOTORMOMENT_IST_WERT | Motormoment Istwert Überwachung | Nm | TQI_AV_MON | - | unsigned char | - | 2,0 | 1 | 0,0 |
| IMOAK | 0x58D1 | STAT_MOTORMOMENT_AKTUELL_WERT | Moment aktueller Wert | Nm | TQI_AV | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58D2 | STAT_0x58D2_WERT | Status Luftklappensystem High Byte | - | STATE_ECRAS_SYS_KWP_H | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58D3 | STAT_0x58D3_WERT | Status Luftklappensystem Low Byte | - | STATE_ECRAS_SYS_KWP_L | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58D4 | STAT_0x58D4_WERT | Abweichung maximales Moment an Kupplung Überwachung | Nm | TQ_MAX_CLU_DIF_MON | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58D5 | STAT_0x58D5_WERT | Air temperature up turbo charger | °C | TIA_TCHA_KWP | - | unsigned char | - | 1,0 | 1 | -48,0 |
| - | 0x58D6 | STAT_0x58D6_WERT | Abweichung minimales Moment an Kupplung Überwachung | Nm | TQ_MIN_CLU_DIF_MON | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58D7 | STAT_0x58D7_WERT | Voltage for temperatur sensor up turbocharger | V | VP_TIA_TCHA_KWP | - | unsigned char | - | 0,012941176071763 | 1 | 0,0 |
| - | 0x58D8 | STAT_0x58D8_WERT | Catalyst temperature sensor raw acquisition | V | VP_TEG_PCAT_DOWN_KWP | - | unsigned char | - | 0,012941176071763 | 1 | 0,0 |
| - | 0x58D9 | STAT_0x58D9_WERT | Fehlercode Rechnerüberwachung: aktueller Wert | - | ENVD_0_MON_3 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58DA | STAT_0x58DA_WERT | Resetzähler Rechnerüberwachung: aktueller Wert | - | ENVD_1_MON_3 | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58DB | STAT_0x58DB_WERT | Inhalt Statusbyte 1 Drehzahlüberwachung (resetsicher) | - | STATE_TQI_N_MAX_MON_1_1_SAVE | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58DC | STAT_0x58DC_WERT | Inhalt Statusbyte 2 Drehzahlüberwachung (resetsicher) | - | STATE_TQI_N_MAX_MON_1_2_SAVE | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58DD | STAT_0x58DD_WERT | Pressure upstream the throttle (Turbo) | kPa | PUT_KWP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58DE | STAT_0x58DE_WERT | Voltage of the intake manifold pressure sensor up throttle (for diagnosis) | V | V_PUT_KWP | - | unsigned char | - | 0,0195312164723873 | 1 | 0,0 |
| IUSPS | 0x58DF | STAT_SPORTSCHALTER_SPANNUNG_WERT | Spannung Sportschalter | V | V_SOF_SWI_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x58E0 | STAT_0x58E0_WERT | Abgleich Drosselklappenmodell (Faktor) | - | EISYDK_KORFAK_B | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| - | 0x58E1 | STAT_0x58E1_WERT | Abgleich Drosselklappenmodell (Offset) | kg/h | EISYDK_KOROFF_B | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58E2 | STAT_0x58E2_WERT | Abgleich Einlassventilmodell (Faktor) | - | EISYEV_KORFAK_B | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| - | 0x58E3 | STAT_0x58E3_WERT | Abgleich Einlassventilmodell (Offset) | kg/h | EISYEV_KOROFF_B | - | signed char | - | 8,0 | 1 | 0,0 |
| - | 0x58E4 | STAT_0x58E4_WERT | Betriebsart Istwert | 0-n | BA_IST | - | 0xFF | _CNV_S_5_Def_ba_gdi_609 | 1 | 1 | 0 |
| - | 0x58E5 | STAT_0x58E5_WERT | Lastwert für Aussetzererkennung | % | LOAD_MIS_KWP | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x58E6 | STAT_0x58E6_WERT | Nulllastwert für Aussetzererkennung | % | LOAD_MIN_MIS_KWP | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x58E7 | STAT_0x58E7_WERT | Spannung Pedalwertgeber 1 Überwachung | V | V_PVS_1_MON_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| - | 0x58E8 | STAT_0x58E8_WERT | Spannung Pedalwertgeber 2 Überwachung | V | V_PVS_2_MON_KWP | - | unsigned char | - | 0,01953125 | 1 | 0,0 |
| IUWAP | 0x58E9 | STAT_WASSERPUMPE_SPANNUNG_WERT | Wasserpumpe Spannung | V | V_CWP | - | unsigned char | - | 0,100000001490116 | 1 | 0,0 |
| - | 0x58EA | STAT_0x58EA_WERT | Wasserpumpe Drehzahl | - | N_REL_CWP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| INWSI | 0x58EB | STAT_WASSERPUMPE_DREHZAHL_SOLL_IST_DIFFERENZ_WERT | Wasserpumpe Drehzahl Soll-Ist-Differenz | - | N_REL_CWP_DIF | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58EC | STAT_0x58EC_WERT | Wasserpumpe Temperatur Elektronik | °C | TEMP_EL_CWP | - | unsigned char | - | 1,0 | 1 | -50,0 |
| - | 0x58ED | STAT_0x58ED_WERT | Wasserpumpe Stromaufnahme | A | CUR_CNS_CWP | - | unsigned char | - | 0,5 | 1 | 0,0 |
| ILWAP | 0x58EE | STAT_WASSERPUMPE_LEOSTUNGSREDUZIERT_WERT | Wasserpumpe leistungsreduziert | % | REL_CWP_PWR | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x58EF | STAT_0x58EF_WERT | Mean value of the acquired sensor voltage | V | V_FUP_MV_KWP | - | unsigned char | - | 0,0195312164723873 | 1 | 0,0 |
| - | 0x58F0 | STAT_0x58F0_WERT | Fuel pressure | hPa | FUP_KWP | - | unsigned char | - | 1358,51770019531 | 1 | 0,0 |
| IDMEL | 0x58F1 | STAT_DME_LOSNUMMER_WERT | DME - Losnummer | 0-n | STATE_LRN_ECU_KWP | - | 0xFF | _CNV_S_11_RANGE_STAT_941 | 1 | 1 | 0 |
| - | 0x58F2 | STAT_0x58F2_WERT | PWM signal for the VCV | % | PWM_VCV_KWP | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x58F3 | STAT_0x58F3_WERT | Fuel pressure EFP | hPa | FUP_EFP_KWP | - | unsigned char | - | 42,4537582397461 | 1 | 0,0 |
| - | 0x58F4 | STAT_0x58F4_WERT | Low fuel pressure EFP sensor raw acquisition | V | V_FUP_EFP_MV_KWP | - | unsigned char | - | 0,0195312164723873 | 1 | 0,0 |
| - | 0x58F5 | STAT_0x58F5_WERT | Eingangssignal Rückführregler 1 | V | VLS_DIF_LAM_ADJ_KWP[1] | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| - | 0x58F6 | STAT_0x58F6_WERT | Eingangssignal Rückführregler 2 | V | VLS_DIF_LAM_ADJ_KWP[2] | - | signed char | - | 0,00488278456032276 | 1 | -3,60784326466368E-6 |
| - | 0x58F7 | STAT_0x58F7_WERT | Measured opening of the actuator valve | % | OPG_ACR_KWP | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| ILSA5 | 0x58F8 | STAT_LAUFUNRUHE_SEGMENTADAPTION_ZYL5_WERT | Segmentadaption Laufunruhe Zyl. 5 | %. | SEG_AD_MMV_ER[1] | - | signed char | - | 0,06103530898690227 | 1 | 1,92095835817427E-5 |
| ILSA3 | 0x58F9 | STAT_LAUFUNRUHE_SEGMENTADAPTION_ZYL3_WERT | Segmentadaption Laufunruhe Zyl. 3 | %. | SEG_AD_MMV_ER[2] | - | signed char | - | 0,06103530898690227 | 1 | 1,92095835817427E-5 |
| - | 0x58FA | STAT_0x58FA_WERT | Beladungsgrad Aktivkohlefilter TEV- Funktionstest | - | CL_MMV_SAE | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| - | 0x58FB | STAT_0x58FB_WERT | Zähler Drehzahlerhöhungen TEV- Funktionstest | cyc | SUM_DIAG_DIAGCPS_SAE | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x58FC | STAT_0x58FC_WERT | Setpoint request after limitation for actuator position control | % | OPG_SP_ACR_KWP | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x58FD | STAT_0x58FD_WERT | Finally duty cycle of digital actuator control | % | PWM_ACR_KWP | - | signed char | - | 0,78125 | 1 | 0,0 |
| - | 0x58FE | STAT_0x58FE_WERT | Zähler für Umschaltungen nach HOM durch Monitoring | - | CTR_SWI_AFS_MON | - | unsigned char | - | 1,0 | 1 | 0,0 |
| IUPV1 | 0x5A00 | STAT_PWG1_VERSORGUNGSSPANNUNG_WERT | Versorgung Fahrwertgeber 1 | V | VCC_PVS_1 | - | unsigned integer | - | 0,00976559147238731 | 1 | 0,0 |
| IUPV2 | 0x5A01 | STAT_PWG2_VERSORGUNGSSPANNUNG_WERT | Versorgung Fahrwertgeber 2 | V | VCC_PVS_2 | - | unsigned integer | - | 0,00976559147238731 | 1 | 0,0 |
| IUPW1 | 0x5A04 | STAT_PWG1_SPANNUNG_WERT | Spannung Pedalwertgeber 1 | V | V_PVS_1 | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUPW2 | 0x5A05 | STAT_PWG2_SPANNUNG_WERT | Spannung Pedalwertgeber 2 | V | V_PVS_2 | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUDK1 | 0x5A06 | STAT_DK1_SPANNUNG_WERT | Spannung Drosselklappe Potentiometer 1 | V | V_TPS_1 | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUDK2 | 0x5A07 | STAT_DK2_SPANNUNG_WERT | Spannung Drosselklappe Potentiometer 2 | V | V_TPS_2 | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUANS | 0x5A08 | STAT_ANSAUGLUFTTEMPERATUR_SPANNUNG_WERT | Spannung Ansauglufttemperatur | V | VP_TIA | - | unsigned integer | - | 1,52587876073085E-4 | 1 | 0,0 |
| IUKUM | 0x5A09 | STAT_KUEHLMITTELTEMPERATUR_SPANNUNG_WERT | Spannung Motortemperatur | V | VP_TCO[1] | - | unsigned integer | - | 1,52587876073085E-4 | 1 | 0,0 |
| IUKUA | 0x5A0A | STAT_KUEHLERAUSLASSTEMPERATUR_SPANNUNG_WERT | Spannung Kühlmitteltemperatur Kühlerausgang | V | VP_TCO[2] | - | unsigned integer | - | 1,52587876073085E-4 | 1 | 0,0 |
| IUUMG | 0x5A0B | STAT_UMGEBUNGSDRUCK_SPANNUNG_WERT | Spannung DME Umgebungsdruck | V | V_AMP | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IULMM | 0x5A0C | STAT_LUFTMASSE_WERT | Spannung Luftmasse | V | V_MAF | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| IUSLS | 0x5A0D | STAT_SEKUNDAERLUFT_SPANNUNG_WERT | Spannung Sekundärluft | V | V_SAF | - | unsigned char | - | 0,0196000002324581 | 1 | 0,0 |
| IUSGI | 0x5A0E | STAT_STEUERGERAETE_INNENTEMPERATUR_SPANNUNG_WERT | Spannung SG-Innentemperatur | V | VP_TECU | - | unsigned integer | - | 1,52587876073085E-4 | 1 | 0,0 |
| - | 0x5A0F | STAT_0x5A0F_WERT | Spannung Kl.15 | V | V_IGK_BAS | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUK15 | 0x5A10 | STAT_KL15_SPANNUNG_WERT | Spannung Kl15 | V | V_IGK_MES | - | unsigned integer | - | 0,0280601158738136 | 1 | 0,0 |
| IUSV1 | 0x5A11 | STAT_SONDENSPANNUNG_VORKAT_BANK1_WERT | Spannung Lambdasonde vor Katalysator Bank 1 | V | VLS_UP[1] | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUSV2 | 0x5A12 | STAT_SONDENSPANNUNG_VORKAT_BANK2_WERT | Spannung Lambdasonde vor Katalysator Bank 2 | V | VLS_UP[2] | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUSN1 | 0x5A13 | STAT_SONDENSPANNUNG_NACHKAT_BANK1_WERT | Spannung Lambdasonde hinter Katalysator Bank 1 | V | VLS_DOWN[1] | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUSN2 | 0x5A14 | STAT_SONDENSPANNUNG_NACHKAT_BANK2_WERT | Spannung Lambdasonde hinter Katalysator Bank 2 | V | VLS_DOWN[2] | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUDMT | 0x5A17 | STAT_DMTL_SPANNUNG_WERT | Spannung Strommessung DMTL | V | V_DMTL | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| - | 0x5A18 | STAT_0x5A18_WERT | Spannung Abgastemperatursensor | V | VP_TEG_PCAT_DOWN | - | unsigned integer | - | 1,52587876073085E-4 | 1 | 0,0 |
| - | 0x5A1F | STAT_0x5A1F_WERT | Abgastemperatur | °C | TEG_PCAT_DOWN_1 | - | unsigned integer | - | 0,015625 | 1 | 0,0 |
| - | 0x5A20 | STAT_0x5A20_WERT | Tastverhältnis Nullgangssensor | % | PWM_NEUT_PSN_GB | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| ITKUA | 0x5A21 | STAT_KUEHLERAUSLASSTEMPERATUR_WERT | Kühlmitteltemperatur Kühlerausgang | °C | TCO_2_MES | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| ITSGI | 0x5A22 | STAT_STEUERGERAETE_INNENTEMPERATUR_WERT | Steuergeräte-Innentemperatur | °C | TECU | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| - | 0x5A23 | STAT_0x5A23_WERT | Sollwert Öldruck | hPa | P_OEL_SOLL | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| SWDKL | 0x5A24 | STAT_DK_WINKEL_SOLL_WERT | Drosselklappe Sollwert | °TPS | TPS_SP | - | unsigned integer | - | 0,00729414634406567 | 1 | 0,0 |
| - | 0x5A25 | STAT_0x5A25_WERT | Istwert Öldruck | hPa | P_OEL_IST | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| IPUMG | 0x5A26 | STAT_UMGEBUNGSDRUCK_WERT | Umgebungsdruck | hPa | MAP | - | unsigned integer | - | 0,0829175263643265 | 1 | 0,0 |
| IPPW1 | 0x5A27 | STAT_PWG1_WERT | Pedalwertgeber Potentiometer 1 | % | PV_AV_1 | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IPPW2 | 0x5A28 | STAT_PWG2_WERT | Pedalwertgeber Potentiometer 2 | % | PV_AV_2 | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| RFPWG | 0x5A29 | STAT_FAHRERWUNSCH_PEDAL_ROH_WERT | Fahrpedalwert | % | PV_AV_RAW | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5A2B | STAT_0x5A2B_WERT | Temperatur vor Drosselklappe | °C | TANS | - | signed integer | - | 0,100000001490116 | 1 | 0,0 |
| - | 0x5A2C | STAT_0x5A2C_WERT | Druck vor Drosselklappe | hPa | PVDKDS | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| - | 0x5A2D | STAT_0x5A2D_WERT | Druck nach Drosselklappe | hPa | PS_IST | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| - | 0x5A2E | STAT_0x5A2E_WERT | Kraftstoffniederdrucksensor | hPa | FUP_EFP | - | unsigned integer | - | 2,65336084365845 | 1 | 0,0 |
| - | 0x5A2F | STAT_0x5A2F_WERT | Raildruck | hPa | FUP | - | unsigned integer | - | 5,30672168731689 | 1 | 0,0 |
| ILUZ1 | 0x5A30 | STAT_LAUFUNRUHE_ZYL1_WERT | Laufunruhe Zylinder 1 | µs | ER_CYL[0] | - | signed integer | - | 1,0 | 1 | 0,0 |
| ILUZ2 | 0x5A31 | STAT_LAUFUNRUHE_ZYL2_WERT | Laufunruhe Zylinder 2 | µs | ER_CYL[4] | - | signed integer | - | 1,0 | 1 | 0,0 |
| ILUZ3 | 0x5A32 | STAT_LAUFUNRUHE_ZYL3_WERT | Laufunruhe Zylinder 3 | µs | ER_CYL[2] | - | signed integer | - | 1,0 | 1 | 0,0 |
| ILUZ4 | 0x5A33 | STAT_LAUFUNRUHE_ZYL4_WERT | Laufunruhe Zylinder 4 | µs | ER_CYL[5] | - | signed integer | - | 1,0 | 1 | 0,0 |
| ILUZ5 | 0x5A34 | STAT_LAUFUNRUHE_ZYL5_WERT | Laufunruhe Zylinder 5 | µs | ER_CYL[1] | - | signed integer | - | 1,0 | 1 | 0,0 |
| ILUZ6 | 0x5A35 | STAT_LAUFUNRUHE_ZYL6_WERT | Laufunruhe Zylinder 6 | µs | ER_CYL[3] | - | signed integer | - | 1,0 | 1 | 0,0 |
| ISKLO | 0x5A36 | STAT_STATUS_KLOPFEN_WERT | Status Klopfen | 0/1 | LV_KNK | - | 0xFF | - | 1 | 1 | 0 |
| IUKZ1 | 0x5A37 | STAT_KLOPFWERT_ZYL1_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 1 | V | NL[0] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IUKZ2 | 0x5A38 | STAT_KLOPFWERT_ZYL2_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 2 | V | NL[4] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IUKZ3 | 0x5A39 | STAT_KLOPFWERT_ZYL3_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 3 | V | NL[2] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IUKZ4 | 0x5A3A | STAT_KLOPFWERT_ZYL4_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 4 | V | NL[5] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IUKZ5 | 0x5A3B | STAT_KLOPFWERT_ZYL5_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 5 | V | NL[1] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IUKZ6 | 0x5A3C | STAT_KLOPFWERT_ZYL6_SPANNUNG_WERT | Spannung Klopfwerte Zylinder 6 | V | NL[3] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IKSZ1 | 0x5A3D | STAT_KLOPFSIGNAL_ZYL1_WERT | Klopfsignal Zylinder 1 | V | KNKS[0] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IKRZ1 | 0x5A3E | STAT_KLOPFSIGNAL_ZYL1_RELATIV_WERT | Klopfsignal Zylinder 1 relativ | - | KNKS_REL_NL_0 | - | unsigned integer | - | 1,52587890625E-5 | 1 | 0,0 |
| IKSZ6 | 0x5A3F | STAT_KLOPFSIGNAL_ZYL6_WERT | Klopfsignal Zylinder 6 | V | KNKS[5] | - | unsigned integer | - | 7,62939453125E-5 | 1 | 0,0 |
| IKRZ6 | 0x5A40 | STAT_KLOPFSIGNAL_ZYL6_RELATIV_WERT | Klopfsignal Zylinder 6 relativ | - | KNKS_REL_NL_5 | - | unsigned integer | - | 1,52587890625E-5 | 1 | 0,0 |
| IZWZ1 | 0x5A49 | STAT_ZUENDWINKEL_ZYL1_WERT | Zündwinkel Zylinder 1 | °CRK | IGA_IGC[0] | - | unsigned char | - | 0,375 | 1 | -35,6249989382923 |
| ILASB | 0x5A4B | STAT_BERECHNETE_LAST_WERT | Berechneter Lastwert | % | LOAD_CLC | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5A4C | STAT_0x5A4C_WERT | Status Drosselklappenheizungsrelais | 0-n | STATE_MTC_HEAT | - | 0xFF | _CNV_S_5_RANGE_STAT_971 | 1 | 1 | 0 |
| - | 0x5A4D | STAT_0x5A4D | Drosselklappenheizung Ein | 0/1 | LV_RLY_MTC_HEAT | - | 0xFF | - | 1 | 1 | 0 |
| ISACR | 0x5A4E | STAT_KLIMAKOMPRESSORRELAIS_EIN | Klimakompressorrelais Ein | 0/1 | LV_ACCOUT_RLY | - | 0xFF | - | 1 | 1 | 0 |
| ILAB1 | 0x5A50 | STAT_LAMBDA_BANK1_WERT | Lambdawert vor Katalysator Bank 1 | - | LAMB_LS_UP[1] | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| ILAB2 | 0x5A51 | STAT_LAMBDA_BANK2_WERT | Lambdawert vor Katalysator Bank 2 | - | LAMB_LS_UP[2] | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| IRNK1 | 0x5A52 | STAT_READINESS_SONDE_NACHKAT_BANK1_WERT | Status LS hinter Katalysator Bank 1 | 0/1 | LV_LS_DOWN_READY[1] | - | 0xFF | - | 1 | 1 | 0 |
| IRNK2 | 0x5A53 | STAT_READINESS_SONDE_NACHKAT_BANK2_WERT | Status LS hinter Katalysator Bank 2 | 0/1 | LV_LS_DOWN_READY[2] | - | 0xFF | - | 1 | 1 | 0 |
| ISHN1 | 0x5A54 | STAT_SONDENHEIZUNG_NACHKAT_BANK1_WERT | Status LS Heizung hinter Katalysator Bank 1 | 0-n | STATE_LSH_DOWN[1] | - | 0xFF | _CNV_S_7_EGCP_RANGE_357 | 1 | 1 | 0 |
| ISHN2 | 0x5A55 | STAT_SONDENHEIZUNG_NACHKAT_BANK2_WERT | Status LS Heizung hinter Katalysator Bank 2 | 0-n | STATE_LSH_DOWN[2] | - | 0xFF | _CNV_S_7_EGCP_RANGE_357 | 1 | 1 | 0 |
| ISHV1 | 0x5A56 | STAT_SONDENHEIZUNG_VORKAT_BANK1_WERT | Status LS Heizung vor Katalysator Bank 1 | 0-n | STATE_LSH_UP[1] | - | 0xFF | _CNV_S_7_EGCP_RANGE_357 | 1 | 1 | 0 |
| ISHV2 | 0x5A57 | STAT_SONDENHEIZUNG_VORKAT_BANK2_WERT | Status LS Heizung vor Katalysator Bank 2 | 0-n | STATE_LSH_UP[2] | - | 0xFF | _CNV_S_7_EGCP_RANGE_357 | 1 | 1 | 0 |
| IAHV1 | 0x5A58 | STAT_SONDENHEIZUNG_PWM_VORKAT_BANK1_WERT | Lambdasondenheizung PWM vor Katalysator Bank 1 | % | LSHPWM_UP[1] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IAHN1 | 0x5A59 | STAT_STAT_SONDENHEIZUNG_PWM_NACHKAT_BANK1_WERT | Lambdasondenheizung PWM hinter Katalysator Bank 1 | % | LSHPWM_DOWN[1] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IAHV2 | 0x5A5A | STAT_STAT_SONDENHEIZUNG_PWM_VORKAT_BANK2_WERT | Lambdasondenheizung PWM vor Katalysator Bank 2 | % | LSHPWM_UP[2] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IAHN2 | 0x5A5B | STAT_SONDENHEIZUNG_PWM_NACHKAT_BANK2_WERT | Lambdasondenheizung PWM hinter Katalysator Bank 2 | % | LSHPWM_DOWN[2] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5A5C | STAT_0x5A5C_WERT | Aktive Fehlerrückmeldung DISA-Klappe 1 | - | ERR_VIMPWM_1_FB | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5A5D | STAT_0x5A5D_WERT | Schalthäufigkeitszähler DISA-Klappe 1 | - | CTR_VIMPWM_1_EDGE | - | unsigned long | - | 1,0 | 1 | 0,0 |
| - | 0x5A5E | STAT_0x5A5E_WERT | Aktive Fehlerrückmeldung DISA-Klappe 2 | - | ERR_VIMPWM_2_FB | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5A5F | STAT_0x5A5F_WERT | Schalthäufigkeitszähler DISA-Klappe 2 | - | CTR_VIMPWM_2_EDGE | - | unsigned long | - | 1,0 | 1 | 0,0 |
| ISBLS | 0x5A60 | STAT_BREMSLICHTSCHALTER_EIN_WERT | Bremslichtschalter Ein | 0/1 | LV_IM_BLS | - | 0xFF | - | 1 | 1 | 0 |
| ISBLT | 0x5A61 | STAT_BREMSLICHTTESTSCHALTER_EIN_WERT | Bremslichttestschalter Ein | 0/1 | LV_IM_BTS | - | 0xFF | - | 1 | 1 | 0 |
| ISOED | 0x5A62 | STAT_OELDRUCKSCHALTER_EIN_WERT | Öldruckschalter Ein | 0/1 | LV_POIL_SWI | - | 0xFF | - | 1 | 1 | 0 |
| ISEBO | 0x5A63 | STAT_E_BOXLUEFTER_EIN_WERT | E-Box-Lüfter Ein | 0/1 | LV_EBOX_CFA | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5A64 | STAT_0x5A64_WERT | Motorlager weiche Dämpfung | 0/1 | LV_SWI_AEB | - | 0xFF | - | 1 | 1 | 0 |
| ISAGK | 0x5A65 | STAT_ABGASKLAPPE_EIN_WERT | Abgasklappe Ein | 0/1 | LV_EF | - | 0xFF | - | 1 | 1 | 0 |
| ISDMP | 0x5A66 | STAT_DMTL_PUMPE_EIN_WERT | DMTL Pumpe Ein | 0/1 | LV_DMTL_PUMP | - | 0xFF | - | 1 | 1 | 0 |
| ISDMV | 0x5A67 | STAT_DMTL_VENTIL_EIN_WERT | DMTL Ventil Ein | 0/1 | LV_DMTLS | - | 0xFF | - | 1 | 1 | 0 |
| ISDMH | 0x5A68 | STAT_DMTL_HEIZUNG_EIN_WERT | DMTL Heizung Ein | 0/1 | LV_HDMTL_ON | - | 0xFF | - | 1 | 1 | 0 |
| ISMIL | 0x5A69 | STAT_MIL_EIN_WERT | MIL Lampe Ein | 0/1 | LV_MIL_CAN | - | 0xFF | - | 1 | 1 | 0 |
| ISFGR | 0x5A6A | STAT_LAMPE_FGR_EIN | Lampe FGR Ein | 0/1 | LV_CRU_MAIN_SWI | - | 0xFF | - | 1 | 1 | 0 |
| ISCEL | 0x5A6B | STAT_CHECK_ENGINE_LAMPE_EIN_WERT | Lampe Check Engine Ein | 0/1 | LV_WAL_1_CAN | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5A6C | STAT_0x5A6C_WERT | Verbrauchskorrekturfaktor | - | FAC_FCO_KWP | - | signed char | - | 0,00100000004749745 | 1 | 0,0 |
| ISTFG | 0x5A6D | STAT_TASTE_FGR_EIN_WERT | Status Taste FGR | 0-n | STATE_MSW_CAN | - | 0xFF | _CNV_S_8_RANGE_STAT_21 | 1 | 1 | 0 |
| - | 0x5A6E | STAT_0x5A6E_WERT | Status für irreversible Abschaltbedingung | - | STATE_CRU_OFF_IRR | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x5A6F | STAT_0x5A6F_WERT | Status für reversible Abschaltbedingung | - | STATE_CRU_OFF_REV | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| IASOU | 0x5A70 | STAT_SOUNDKLAPPE_PWM_WERT | Soundklappe Zustand | 0/1 | LV_SOF | - | 0xFF | - | 1 | 1 | 0 |
| IADS1 | 0x5A71 | STAT_DISA1_PWM_WERT | DISA1 PWM (große/obere Klappe) | % | VIMPWM_1 | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| IADS2 | 0x5A72 | STAT_DISA2_PWM_WERT | DISA2 PWM (kleine/untere Klappe) | % | VIMPWM_2 | - | signed integer | - | 0,0030517578125 | 1 | 0,0 |
| - | 0x5A73 | STAT_0x5A73 | Kurbelgehäuseentlüftungsheizung ein | 0/1 | LV_RLY_CRCV_HEAT | - | 0xFF | - | 1 | 1 | 0 |
| IAKFT | 0x5A74 | STAT_BEHEIZTER_THERMOSTAT_PWM_WERT | Beheizter Thermostat PWM | % | ECTPWM | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5A76 | STAT_0x5A76_WERT | Adaption Öffnungspunkt Tankentlüftungsventil | % | CPPWM_ADD_AD_MEM | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IATEV | 0x5A77 | STAT_TEV_PWM_WERT | Tankentlüftungsventil PWM | % | CPPWM_CPS | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IAAGK | 0x5A78 | STAT_ABGASKLAPPE_ANSTEUERUNG_WERT | Abgasklappe Ansteuerung | 0/1 | LV_EF | - | 0xFF | - | 1 | 1 | 0 |
| IAELUE | 0x5A79 | STAT_E_LUEFTER_PWM_WERT | E-Lüfter PWM | % | ECFPWM[0] | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| IAVEP | 0x5A7A | STAT_VANOS_EINLASS_PWM_WERT | VANOS PWM Wert Einlass | % | IVVTPWM_0 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IAVAP | 0x5A7B | STAT_VANOS_AUSLASS_PWM_WERT | VANOS PWM Wert Auslass | % | IVVTPWM_1 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5A7F | STAT_0x5A7F_WERT | Phase-Shift-Adaption Lambdasonde Bank 1 | °CRK | DELTA_CRK_CYL_LAM[1] | - | signed char | - | 6,0 | 1 | 0,0 |
| - | 0x5A80 | STAT_0x5A70_WERT | Phase-Shift-Adaption Lambdasonde Bank 2 | °CRK | DELTA_CRK_CYL_LAM[2] | - | signed char | - | 6,0 | 1 | 0,0 |
| IINT1 | 0x5A81 | STAT_INTEGRATOR_BANK1_WERT | Ausgang Lamdaregler Bank 1 | % | FAC_LAM_LIM[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| IINT2 | 0x5A82 | STAT_INTEGRATOR_BANK2_WERT | Ausgang Lamdaregler Bank 2 | % | FAC_LAM_LIM[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| IADD1 | 0x5A83 | STAT_ADAPTION_ADDITIV_BANK1_WERT | Adaption Offset Lambda Bank 1 | mg/stk | MFF_ADD_LAM_AD_OUT[1] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| IADD2 | 0x5A84 | STAT_ADAPTION_ADDITIV_BANK2_WERT | Adaption Offset Lambda Bank 2 | mg/stk | MFF_ADD_LAM_AD_OUT[2] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| IMUL1 | 0x5A85 | STAT_ADAPTION_MULTIPLIKATIV_BANK1_WERT | Adaption Multiplikation Lambda Bank 1 | % | FAC_LAM_AD_CUS[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| IMUL2 | 0x5A86 | STAT_ADAPTION_MULTIPLIKATIV_BANK2_WERT | Adaption Multiplikation Lambda Bank 2 | % | FAC_LAM_AD_CUS[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5A87 | STAT_0x5A87_WERT | Adaptionswert Trimregelung Bank 1 | - | LAMB_DELTA_AD_LAM_ADJ[1] | - | signed integer | - | 6,103515625E-5 | 1 | 0,0 |
| - | 0x5A88 | STAT_0x5A88_WERT | Adaptionswert Trimregelung Bank 2 | - | LAMB_DELTA_AD_LAM_ADJ[2] | - | signed integer | - | 6,103515625E-5 | 1 | 0,0 |
| - | 0x5A89 | STAT_0x5A89_WERT | multiplikative Gemischadaption hohe Last Bank 1 | % | FAC_H_RNG_LAM_AD[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5A8A | STAT_0x5A8A_WERT | multiplikative Gemischadaption hohe Last Bank 2 | % | FAC_H_RNG_LAM_AD[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5A8B | STAT_0x5A8B_WERT | multiplikative Gemischadaption niedrige Last Bank 1 | % | FAC_L_RNG_LAM_AD[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5A8C | STAT_0x5A8C_WERT | multiplikative Gemischadaption niedrige Last Bank 2 | % | FAC_L_RNG_LAM_AD[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5A8D | STAT_0x5A8D_WERT | additive Gemischadaption Leerlauf Bank 1 | mg/stk | MFF_ADD_LAM_AD[1] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5A8E | STAT_0x5A8E_WERT | additive Gemischadaption Leerlauf Bank 2 | mg/stk | MFF_ADD_LAM_AD[2] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5A8F | STAT_0x5A8F_WERT | Adaption Schubabgleich Bank 1 | - | FAC_LSL_GAIN_AD[1] | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5A90 | STAT_0x5A90_WERT | Adaption Schubabgleich Bank 2 | - | FAC_LSL_GAIN_AD[2] | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5A91 | STAT_0x5A91_WERT | Katalysatordiagnosewert Bank1 | - | EFF_CAT_DIAG_OBD[1] | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| - | 0x5A92 | STAT_0x5A92_WERT | Katalysatordiagnosewert Bank 2 | - | EFF_CAT_DIAG_OBD[2] | - | unsigned char | - | 0,0078125 | 1 | 0,0 |
| SANWA | 0x5A94 | STAT_NW_AUSLASS_SOLL_WERT | Nockenwelle Auslass Sollwert | °CRK | CAM_SP_IVVT_EX | - | unsigned char | - | -0,375 | 1 | -39,9999978542329 |
| IANWA | 0x5A95 | STAT_NW_ADAPTION_AUSLASS_WERT | Adaptionswert Nockenwelle Auslass | °CRK | PSN_AD_CAM_EX_1 | - | unsigned char | - | 0,375 | 1 | -47,9999985694886 |
| IANWE | 0x5A96 | STAT_NW_ADAPTION_EINLASS_WERT | Adaptionswert Nockenwelle Einlass | °CRK | PSN_AD_CAM_IN_1 | - | unsigned char | - | 0,375 | 1 | -47,9999985694886 |
| - | 0x5A97 | STAT_0x5A97_WERT | Bedingung EVANOS im Anschlag beim letzten Abstellen | 0/1 | B_VSEAN_LOC | - | 0xFF | - | 1 | 1 | 0 |
| IAKWF | 0x5A99 | STAT_KURBELWELLEN_ADAPTION_BEENDET_WERT | Kurbelwellen Adaption beendet | 0/1 | LV_SEG_AD_AVL_ER | - | 0xFF | - | 1 | 1 | 0 |
| IDSLS | 0x5AA1 | STAT_SLS_DIAGNOSE_WERT | Status Diagnose TEV | 0-n | STATE_EOL_KWP_CPS | - | 0xFF | _CNV_S_10_STATE_EOL__452 | 1 | 1 | 0 |
| IDTEV | 0x5AA2 | STAT_TEV_DIAGNOSE_WERT | Status Diagnose DMTL | 0-n | STATE_EOL_KWP_DMTL | - | 0xFF | _CNV_S_10_STATE_EOL__452 | 1 | 1 | 0 |
| IDDMT | 0x5AA3 | STAT_DMTL_DIAGNOSE_WERT | Status Diagnose Lambdasonden | 0-n | STATE_EOL_KWP_VLS | - | 0xFF | _CNV_S_10_STATE_EOL__452 | 1 | 1 | 0 |
| IDLSS | 0x5AA4 | STAT_LS_DIAGNOSE_WERT | Status Diagnose Leerlaufdrehzahlverstellung | 0-n | STATE_EOL_KWP_N_SP_IS | - | 0xFF | _CNV_S_10_STATE_EOL__452 | 1 | 1 | 0 |
| - | 0x5AA7 | STAT_0x5AA7_WERT | Leckluftadaption Istwert | kg/h | MSNLGOFS_TMP | - | signed integer | - | 0,03125 | 1 | 0,0 |
| - | 0x5AA8 | STAT_0x5AA8_WERT | Status Luftklappensystem | - | STATE_ECRAS_SYS | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x5AA9 | STAT_0x5AA9_WERT | Tastverhältnis: Luftklappe | % | ECRASPWM | - | unsigned char | - | 0,390625 | 1 | 0,0 |
| - | 0x5AAA | STAT_0x5AAA_WERT | Tastverhältnis Öldruck-Regelventil | % | POIL_PWM | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AAB | STAT_0x5AAB_WERT | Wastegate 1 PWM | % | WGPWM_0 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AAC | STAT_0x5AAC_WERT | Wastegate 2 PWM | % | WGPWM_1 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AAD | STAT_0x5AAD_WERT | Vorsteuerung Ladedruckregelung | % | ATLVST | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AAE | STAT_0x5AAE_WERT | Reglerausgang und Vorsteuerung | % | ATLR | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AAF | STAT_0x5AAF_WERT | Adaptionswert von der Ladedruckregelung | - | F_ATLAD | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5AB0 | STAT_0x5AB0_WERT | Solladedruck | hPa | PLDR_SOLL | - | unsigned integer | - | 0,0390625 | 1 | 0,0 |
| IVKMH | 0x5AB1 | STAT_GESCHWINDIGKEIT_WERT | Geschwindigkeit | km/h | VS | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AB2 | STAT_0x5AB2_WERT | Periodendauer Luftmasse | µs | T_PER_MAF_FRQ[0] | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| IWMIL | 0x5AB3 | STAT_FAHRSTRECKE_MIL_AN_WERT | Fahrstrecke mit MIL an | km | DIST_ACT_MIL | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| IZBST | 0x5AB4 | STAT_BETRIEBSSTUNDENZAEHLER_WERT | Betriebsstundenzähler | h | TRT | - | unsigned long | - | 2,77777780866018E-5 | 1 | 0,0 |
| RTANS | 0x5AB6 | STAT_ANSAUGLUFTTEMPERATUR1_ROH_WERT | Rohwert Ansauglufttemperatur 1 | °C | TIA_MES | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| RTKWA | 0x5AB7 | STAT_KUEHLWASSERTEMPERATUR_ROH_WERT | Rohwert Kühlwassertemperatur | °C | TCO_MES | - | unsigned char | - | 0,75 | 1 | -47,9999985694886 |
| IUSAU | 0x5AB8 | STAT_SAUGROHRDRUCK_SPANNUNG_WERT | Spannung Saugrohrdruck | V | V_MAP | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IUSST | 0x5AB9 | STAT_SPORTSCHALTER_SPANNUNG_WERT | Spannung Sportschalter | V | V_SOF_SWI | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| IAKSP | 0x5ABA | STAT_KRAFTSTOFFPUMPE_PWM_WERT | Kraftstoffpumpe PWM | % | EFPPWM | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| IMLUF | 0x5ABC | STAT_LUFTMASSE_WERT | Luftmasse | kg/h | MAF_KGH_MES_BAS | - | unsigned integer | - | 0,03125 | 1 | 0,0 |
| IASRE | 0x5ABD | STAT_STARTRELAIS_AKTIV_WERT | Starterrelais aktiv | 0/1 | LV_RLY_ST | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5AC2 | STAT_0x5AC2_WERT | Info last available caller addresses (default 0) | - | RST_DBG_BACKTRACE_ADDRESS[0][0] | - | unsigned long | - | 1,0 | 1 | 0,0 |
| - | 0x5AC6 | STAT_0x5AC6_WERT | Sensorspannung AGR | V | V_ACR | - | unsigned integer | - | 0,00488269794732332 | 1 | 0,0 |
| - | 0x5AC7 | STAT_0x5AC7_WERT | Hub des AGR-Tellerventils | % | OPG_ACR | - | unsigned integer | - | 0,0244140625 | 1 | 0,0 |
| - | 0x5AC8 | STAT_0x5AC8_WERT | Adaptionswert oberer Anschlag (einmalig gelernt) | V | V_ACR_AD_TOL | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| - | 0x5AC9 | STAT_0x5AC9_WERT | Adaptionswert unterer Anschlag (immer wieder neu gelernt) | V | V_ACR_AD_BOL | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| - | 0x5ACA | STAT_0x5ACA_WERT | Adaptionswert unterer Anschlag (einmalig am Anfang gelernt, Uradaption) | V | V_ACR_AD_BOL_0 | - | unsigned integer | - | 0,0048828125 | 1 | 0,0 |
| - | 0x5ACB | STAT_0x5ACB_WERT | Status des Erlernens der AGR-Adaption | 0-n | STATE_ACR_AD | - | 0xFF | _CNV_S_6_ACRC_RANGE_871 | 1 | 1 | 0 |
| - | 0x5ACC | STAT_0x5ACC_WERT | DME-Temperaturstatistik, Zähler 1 | - | CTR_STC_TECU_1 | - | unsigned long | - | 1,0 | 1 | 0,0 |
| - | 0x5ACD | STAT_0x5ACD_WERT | DME-Temperaturstatistik, Zähler 2 | - | CTR_STC_TECU_2 | - | unsigned long | - | 1,0 | 1 | 0,0 |
| - | 0x5ACE | STAT_0x5ACE_WERT | DME-Temperaturstatistik, Zähler 3 | - | CTR_STC_TECU_3 | - | unsigned long | - | 1,0 | 1 | 0,0 |
| - | 0x5ACF | STAT_0x5ACF_WERT | DME-Temperaturstatistik, Zähler 4 | - | CTR_STC_TECU_4 | - | unsigned long | - | 1,0 | 1 | 0,0 |
| - | 0x5AD0 | STAT_0x5AD0_WERT | DME-Temperaturstatistik, Zähler 5 | - | CTR_STC_TECU_5 | - | unsigned long | - | 1,0 | 1 | 0,0 |
| - | 0x5AD1 | STAT_0x5AD1_WERT | DME-Temperaturstatistik, Zähler 6 | - | CTR_STC_TECU_6 | - | unsigned long | - | 1,0 | 1 | 0,0 |
| - | 0x5AD2 | STAT_0x5AD2_WERT | DME-Temperaturstatistik, Zähler 7 | - | CTR_STC_TECU_7 | - | unsigned long | - | 1,0 | 1 | 0,0 |
| - | 0x5AD3 | STAT_0x5AD3_WERT | DME-Temperaturstatistik, Zähler 8 | - | CTR_STC_TECU_8 | - | unsigned long | - | 1,0 | 1 | 0,0 |
| - | 0x5AD6 | STAT_0x5AD6_WERT | Schubabschaltung | ppm | NOX_OFS_PUC[1] | - | signed integer | - | 1,0 | 1 | 0,0 |
| - | 0x5AD7 | STAT_0x5AD7_WERT | Beladungsbetrieb NOx-Katalysator | ppm | NOX_OFS_LOAD[1] | - | signed integer | - | 1,0 | 1 | 0,0 |
| - | 0x5AD8 | STAT_0x5AD8_WERT | NOx-Konzentration | ppm | NOX_NS[1] | - | signed integer | - | 1,0 | 1 | 0,0 |
| - | 0x5AD9 | STAT_0x5AD9_WERT | Lineares Lambdasignal NOx-Sensor | - | LAMB_NOX_SENS[1] | - | unsigned integer | - | 9,765625E-4 | 1 | 0,0 |
| - | 0x5ADA | STAT_0x5ADA_WERT | binäres Spannungssignal NOx-Sensor | mV | VLS_NOX_SENS[1] | - | unsigned integer | - | 1,0 | 1 | -200,0 |
| - | 0x5ADB | STAT_0x5ADB_WERT | Status NOx-Sensor | - | CAN_STATE_NOX_SENS[1] | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5ADC | STAT_0x5ADC_WERT | NOx-Sensor Error Byte | - | CAN_ERR_NOX_SENS[1] | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5ADF | STAT_0x5ADF_WERT | Taupunkterkennung für NOx-Sensor | 0/1 | LV_CAN_TEMP_MIN_THD_1 | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5AE0 | STAT_0x5AE0_WERT | Status-byte: security info for atypical reset (reset-save memory) | - | RST_SEC | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AE2 | STAT_0x5AE2_WERT | Reset type of last reset | - | RST_TYP | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AE3 | STAT_0x5AE3_WERT | Background info for last reset valid | - | RST_DBG_BACK_INFO_VLD[0] | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AE4 | STAT_0x5AE4_WERT | Additional reset info (cause) | - | RST_INFO_ADD[0] | - | unsigned long | - | 1,0 | 1 | 0,0 |
| - | 0x5AE5 | STAT_0x5AE5_WERT | Mileage counter at reset | m | DIST_RST_DET[0] | - | unsigned long | - | 100,0 | 1 | 0,0 |
| - | 0x5AE6 | STAT_0x5AE6_WERT | Total runtime at reset | h | TRT_RST_DET[0] | - | unsigned long | - | 2,77777780866018E-5 | 1 | 0,0 |
| - | 0x5AE7 | STAT_0x5AE7_WERT | Max. CPU load from reset detection | % | CPU_LOAD_MAX_RST_DET[0] | - | unsigned integer | - | 0,09765625 | 1 | 0,0 |
| - | 0x5AE8 | STAT_0x5AE8_WERT | Engine speed at max. cpu load from reset detection | rpm | N_CPU_LOAD_MAX_RST_DET[0] | - | unsigned integer | - | 1,0 | 1 | 0,0 |
| - | 0x5AE9 | STAT_0x5AE9_WERT | Security info | - | RST_CLAS_SEC[0] | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AEA | STAT_0x5AEA_WERT | Number of atypical warm-resets since last power-up (BSW) | - | RST_INFO_CTR | - | unsigned char | - | 1,0 | 1 | 0,0 |
| - | 0x5AEB | STAT_0x5AEB_WERT | Kühlmitteltemperatur &lt; 98°C | % | TMOT_B1 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AEC | STAT_0x5AEC_WERT | 98°C =&lt; Kühlmitteltemperatur =&lt; 112°C | % | TMOT_B2 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AED | STAT_0x5AED_WERT | 113°C =&lt; Kühlmitteltemperatur =&lt; 120°C | % | TMOT_B3 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AEE | STAT_0x5AEE_WERT | 121°C =&lt; Kühlmitteltemperatur =&lt; 125°C | % | TMOT_B4 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AEF | STAT_0x5AEF_WERT | Kühlmitteltemperatur &gt; 125°C | % | TMOT_B5 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF0 | STAT_0x5AF0_WERT | Motoröltemperatur &lt; 80°C | % | TOEL_B1 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF1 | STAT_0x5AF1_WERT | 80°C =&lt; Motoröltemperatur =&lt; 110°C | % | TOEL_B2 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF2 | STAT_0x5AF2_WERT | 110°C =&lt; Motoröltemperatur =&lt; 135°C | % | TOEL_B3 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF3 | STAT_0x5AF3_WERT | 135°C =&lt; Motoröltemperatur =&lt; 150°C | % | TOEL_B4 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF4 | STAT_0x5AF4_WERT | Motoröltemperatur &gt; 150°C | % | TOEL_B5 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF5 | STAT_0x5AF5_WERT | Getriebeöltemperatur &lt; 80°C | % | TGET_B1 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF6 | STAT_0x5AF6_WERT | 80°C =&lt; Getriebeöltemperatur =&lt; 109°C | % | TGET_B2 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF7 | STAT_0x5AF7_WERT | 110°C =&lt; Getriebeöltemperatur =&lt; 124°C | % | TGET_B3 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF8 | STAT_0x5AF8_WERT | 125°C =&lt; Getriebeöltemperatur =&lt; 129°C | % | TGET_B4 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AF9 | STAT_0x5AF9_WERT | Getriebeöltemperatur &gt; 129°C | % | TGET_B5 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AFA | STAT_0x5AFA_WERT | Umgebungstemperatur &lt; 3°C | % | TUMG_B1 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AFB | STAT_0x5AFB_WERT | 3°C =&lt; Umgebungstemperatur =&lt; 19°C | % | TUMG_B2 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AFC | STAT_0x5AFC_WERT | 20°C =&lt; Umgebungstemperatur =&lt; 29°C | % | TUMG_B3 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AFD | STAT_0x5AFD_WERT | 30°C =&lt; Umgebungstemperatur =&lt; 39°C | % | TUMG_B4 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5AFE | STAT_0x5AFE_WERT | Umgebungstemperatur &gt; 39°C | % | TUMG_B5 | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5B00 | STAT_0x5B00_WERT | Einspritzzeit Zylinder 1 von der Endstufe rückgemessen  | ms | TI_1_MES[0] | - | unsigned integer | - | 0,00100000004749745 | 1 | 0,0 |
| - | 0x5B01 | STAT_0x5B01_WERT | Einspritzzeit Zylinder 2 von der Endstufe rückgemessen  | ms | TI_1_MES[4] | - | unsigned integer | - | 0,00100000004749745 | 1 | 0,0 |
| - | 0x5B02 | STAT_0x5B02_WERT | Einspritzzeit Zylinder 3 von der Endstufe rückgemessen  | ms | TI_1_MES[2] | - | unsigned integer | - | 0,00100000004749745 | 1 | 0,0 |
| - | 0x5B03 | STAT_0x5B03_WERT | Einspritzzeit Zylinder 4 von der Endstufe rückgemessen  | ms | TI_1_MES[5] | - | unsigned integer | - | 0,00100000004749745 | 1 | 0,0 |
| - | 0x5B04 | STAT_0x5B04_WERT | Einspritzzeit Zylinder 5 von der Endstufe rückgemessen  | ms | TI_1_MES[1] | - | unsigned integer | - | 0,00100000004749745 | 1 | 0,0 |
| - | 0x5B05 | STAT_0x5B05_WERT | Einspritzzeit Zylinder 6 von der Endstufe rückgemessen  | ms | TI_1_MES[3] | - | unsigned integer | - | 0,00100000004749745 | 1 | 0,0 |
| - | 0x5B10 | STAT_0x5B10_WERT | Tastverhältnis Injektor 1 an Endstufe  | % | EGY_STEP_INJ_CHA_GRD[0] | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| - | 0x5B11 | STAT_0x5B11_WERT | Tastverhältnis Injektor 2 an Endstufe  | % | EGY_STEP_INJ_CHA_GRD[4] | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| - | 0x5B12 | STAT_0x5B12_WERT | Tastverhältnis Injektor 3 an Endstufe  | % | EGY_STEP_INJ_CHA_GRD[2] | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| - | 0x5B13 | STAT_0x5B13_WERT | Tastverhältnis Injektor 4 an Endstufe  | % | EGY_STEP_INJ_CHA_GRD[5] | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| - | 0x5B14 | STAT_0x5B14_WERT | Tastverhältnis Injektor 5 an Endstufe  | % | EGY_STEP_INJ_CHA_GRD[1] | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| - | 0x5B15 | STAT_0x5B15_WERT | Tastverhältnis Injektor 6 an Endstufe  | % | EGY_STEP_INJ_CHA_GRD[3] | - | unsigned integer | - | 0,006103515625 | 1 | 0,0 |
| - | 0x5B20 | STAT_0x5B20_WERT | Elektrische Ladung Injektor 1 | uAs | CHA_IV_1_MES[0] | - | unsigned integer | - | 2,22160005569458 | 1 | 0,0 |
| - | 0x5B21 | STAT_0x5B21_WERT | Elektrische Ladung Injektor 2 | uAs | CHA_IV_1_MES[4] | - | unsigned integer | - | 2,22160005569458 | 1 | 0,0 |
| - | 0x5B22 | STAT_0x5B22_WERT | Elektrische Ladung Injektor 3 | uAs | CHA_IV_1_MES[2] | - | unsigned integer | - | 2,22160005569458 | 1 | 0,0 |
| - | 0x5B23 | STAT_0x5B23_WERT | Elektrische Ladung Injektor 4 | uAs | CHA_IV_1_MES[5] | - | unsigned integer | - | 2,22160005569458 | 1 | 0,0 |
| - | 0x5B24 | STAT_0x5B24_WERT | Elektrische Ladung Injektor 5 | uAs | CHA_IV_1_MES[1] | - | unsigned integer | - | 2,22160005569458 | 1 | 0,0 |
| - | 0x5B25 | STAT_0x5B25_WERT | Elektrische Ladung Injektor 6 | uAs | CHA_IV_1_MES[3] | - | unsigned integer | - | 2,22160005569458 | 1 | 0,0 |
| - | 0x5B30 | STAT_0x5B30_WERT | Spannung Injektor 1 | V | V_IV_1_MES[0] | - | unsigned integer | - | 0,01953125 | 1 | 0,0 |
| - | 0x5B31 | STAT_0x5B31_WERT | Spannung Injektor 2 | V | V_IV_1_MES[4] | - | unsigned integer | - | 0,01953125 | 1 | 0,0 |
| - | 0x5B32 | STAT_0x5B32_WERT | Spannung Injektor 3 | V | V_IV_1_MES[2] | - | unsigned integer | - | 0,01953125 | 1 | 0,0 |
| - | 0x5B33 | STAT_0x5B33_WERT | Spannung Injektor 4 | V | V_IV_1_MES[5] | - | unsigned integer | - | 0,01953125 | 1 | 0,0 |
| - | 0x5B34 | STAT_0x5B34_WERT | Spannung Injektor 5 | V | V_IV_1_MES[1] | - | unsigned integer | - | 0,01953125 | 1 | 0,0 |
| - | 0x5B35 | STAT_0x5B35_WERT | Spannung Injektor 6 | V | V_IV_1_MES[3] | - | unsigned integer | - | 0,01953125 | 1 | 0,0 |
| - | 0x5B40 | STAT_0x5B40_WERT | Adaptionswert der Enstufe Injektor 1 | %/mJ | FAC_EGY_PWM_AD[0] | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5B41 | STAT_0x5B41_WERT | Adaptionswert der Enstufe Injektor 2 | %/mJ | FAC_EGY_PWM_AD[4] | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5B42 | STAT_0x5B42_WERT | Adaptionswert der Enstufe Injektor 3 | %/mJ | FAC_EGY_PWM_AD[2] | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5B43 | STAT_0x5B43_WERT | Adaptionswert der Enstufe Injektor 4 | %/mJ | FAC_EGY_PWM_AD[5] | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5B44 | STAT_0x5B44_WERT | Adaptionswert der Enstufe Injektor 5 | %/mJ | FAC_EGY_PWM_AD[1] | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5B45 | STAT_0x5B45_WERT | Adaptionswert der Enstufe Injektor 6 | %/mJ | FAC_EGY_PWM_AD[3] | - | unsigned integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5B50 | STAT_0x5B50_WERT | Momentan eingerechnete CILC-Werte Injektor 1 | % | FAC_CYL_LAM_COR[0] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5B51 | STAT_0x5B51_WERT | Momentan eingerechnete CILC-Werte Injektor 2 | % | FAC_CYL_LAM_COR[4] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5B52 | STAT_0x5B52_WERT | Momentan eingerechnete CILC-Werte Injektor 3 | % | FAC_CYL_LAM_COR[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5B53 | STAT_0x5B53_WERT | Momentan eingerechnete CILC-Werte Injektor 4 | % | FAC_CYL_LAM_COR[5] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5B54 | STAT_0x5B54_WERT | Momentan eingerechnete CILC-Werte Injektor 5 | % | FAC_CYL_LAM_COR[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5B55 | STAT_0x5B55_WERT | Momentan eingerechnete CILC-Werte Injektor 6 | % | FAC_CYL_LAM_COR[3] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5B60 | STAT_0x5B60_WERT | CILC-Adaption kalt Injektor 1 | % | FAC_LAM_CYL_SEL_ADJ_CST[0] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5B61 | STAT_0x5B61_WERT | CILC-Adaption kalt Injektor 2 | % | FAC_LAM_CYL_SEL_ADJ_CST[4] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5B62 | STAT_0x5B62_WERT | CILC-Adaption kalt Injektor 3 | % | FAC_LAM_CYL_SEL_ADJ_CST[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5B63 | STAT_0x5B63_WERT | CILC-Adaption kalt Injektor 4 | % | FAC_LAM_CYL_SEL_ADJ_CST[5] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5B64 | STAT_0x5B64_WERT | CILC-Adaption kalt Injektor 5 | % | FAC_LAM_CYL_SEL_ADJ_CST[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5B65 | STAT_0x5B65_WERT | CILC-Adaption kalt Injektor 6 | % | FAC_LAM_CYL_SEL_ADJ_CST[3] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5B70 | STAT_0x5B70_WERT | ER-Adaption MFF-additiv im LL Schicht für Injektor 1 | mg/stk | MFF_ADD_AD_ER_BAL[0] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5B71 | STAT_0x5B71_WERT | ER-Adaption MFF-additiv im LL Schicht für Injektor 2 | mg/stk | MFF_ADD_AD_ER_BAL[4] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5B72 | STAT_0x5B72_WERT | ER-Adaption MFF-additiv im LL Schicht für Injektor 3 | mg/stk | MFF_ADD_AD_ER_BAL[2] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5B73 | STAT_0x5B73_WERT | ER-Adaption MFF-additiv im LL Schicht für Injektor 4 | mg/stk | MFF_ADD_AD_ER_BAL[5] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5B74 | STAT_0x5B74_WERT | ER-Adaption MFF-additiv im LL Schicht für Injektor 5 | mg/stk | MFF_ADD_AD_ER_BAL[1] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5B75 | STAT_0x5B75_WERT | ER-Adaption MFF-additiv im LL Schicht für Injektor 6 | mg/stk | MFF_ADD_AD_ER_BAL[3] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5B80 | STAT_0x5B80_WERT | ER-MFF-aditiv im LL-Schicht (momentan eingerechte Werte) Injektor 1 | mg/stk | MFF_ADD_ER_BAL[0] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5B81 | STAT_0x5B81_WERT | ER-MFF-aditiv im LL-Schicht (momentan eingerechte Werte) Injektor 2 | mg/stk | MFF_ADD_ER_BAL[4] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5B82 | STAT_0x5B82_WERT | ER-MFF-aditiv im LL-Schicht (momentan eingerechte Werte) Injektor 3 | mg/stk | MFF_ADD_ER_BAL[2] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5B83 | STAT_0x5B83_WERT | ER-MFF-aditiv im LL-Schicht (momentan eingerechte Werte) Injektor 4 | mg/stk | MFF_ADD_ER_BAL[5] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5B84 | STAT_0x5B84_WERT | ER-MFF-aditiv im LL-Schicht (momentan eingerechte Werte) Injektor 5 | mg/stk | MFF_ADD_ER_BAL[1] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5B85 | STAT_0x5B85_WERT | ER-MFF-aditiv im LL-Schicht (momentan eingerechte Werte) Injektor 6 | mg/stk | MFF_ADD_ER_BAL[3] | - | signed integer | - | 0,0211947802454233 | 1 | 3,08424652517705E-13 |
| - | 0x5B90 | STAT_0x5B90_WERT | ER-Adaptionsfaktor in Schicht Teillast für Injektor 1 | - | FAC_TI_AD_ER_BAL[0] | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5B91 | STAT_0x5B91_WERT | ER-Adaptionsfaktor in Schicht Teillast für Injektor 2 | - | FAC_TI_AD_ER_BAL[4] | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5B92 | STAT_0x5B92_WERT | ER-Adaptionsfaktor in Schicht Teillast für Injektor 3 | - | FAC_TI_AD_ER_BAL[2] | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5B93 | STAT_0x5B93_WERT | ER-Adaptionsfaktor in Schicht Teillast für Injektor 4 | - | FAC_TI_AD_ER_BAL[5] | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5B94 | STAT_0x5B94_WERT | ER-Adaptionsfaktor in Schicht Teillast für Injektor 5 | - | FAC_TI_AD_ER_BAL[1] | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5B95 | STAT_0x5B95_WERT | ER-Adaptionsfaktor in Schicht Teillast für Injektor 6 | - | FAC_TI_AD_ER_BAL[3] | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5BA0 | STAT_0x5BA0_WERT | ER-Faktor in Schicht Teillast momentan eingerechnet für Injektor 1 | - | FAC_TI_ER_BAL[0] | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5BA1 | STAT_0x5BA1_WERT | ER-Faktor in Schicht Teillast momentan eingerechnet für Injektor 2 | - | FAC_TI_ER_BAL[4] | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5BA2 | STAT_0x5BA2_WERT | ER-Faktor in Schicht Teillast momentan eingerechnet für Injektor 3 | - | FAC_TI_ER_BAL[2] | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5BA3 | STAT_0x5BA3_WERT | ER-Faktor in Schicht Teillast momentan eingerechnet für Injektor 4 | - | FAC_TI_ER_BAL[5] | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5BA4 | STAT_0x5BA4_WERT | ER-Faktor in Schicht Teillast momentan eingerechnet für Injektor 5 | - | FAC_TI_ER_BAL[1] | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5BA5 | STAT_0x5BA5_WERT | ER-Faktor in Schicht Teillast momentan eingerechnet für Injektor 6 | - | FAC_TI_ER_BAL[3] | - | signed integer | - | 3,0517578125E-5 | 1 | 0,0 |
| - | 0x5BB0 | STAT_0x5BB0_WERT | Lambdaadaption am Bandende hat fertig gelernt  | 0/1 | LV_CYL_BAL_LAM_AD_EOL | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5BB1 | STAT_0x5BB1_WERT | ER-Balancing am Bandende hat additiv adaptiert  | 0/1 | LV_CYL_BAL_ER_AD_ADD_EOL | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5BB2 | STAT_0x5BB2_WERT | Lambdaadaption ist nötig, zyklisch während Motorbetrieb zu 1 gesetzt  | 0/1 | LV_CYL_BAL_LAM_AD_DC | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5BB3 | STAT_0x5BB3_WERT | ER-Balancing am Bandende hat den Faktor adaptiert  | 0/1 | LV_CYL_BAL_ER_AD_FAC_EOL | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5BB4 | STAT_0x5BB4_WERT | Zylindersel. Lambdaregelung fordert homogen an, zyklisch während dem Motorbetrieb zu 1 gesetzt  | 0/1 | LV_CYL_BAL_AD_HOM_REQ_DC | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5BB5 | STAT_0x5BB5_WERT | Zylindersel. Lambdaregelung kalt am Bandende hat fertig adaptiert  | 0/1 | LV_CYL_BAL_LAM_SEL_AD_COLD_EOL | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5BB6 | STAT_0x5BB6_WERT | Zylindersel. Lambdaregelung warm am Bandende hat fertig adaptiert  | 0/1 | LV_CYL_BAL_LAM_SEL_AD_HOT_EOL | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5BB7 | STAT_0x5BB7_WERT | Zylindersel. Lambdaregelung warm ist nötig, zyklisch während Motorbetrieb zu 1 gesetzt  | 0/1 | LV_CYL_BAL_LAM_SEL_AD_HOT_DC | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5BB8 | STAT_0x5BB8_WERT | Zylindersel. Lambdaregelung fordert öffnen WG an, zyklisch während dem Motorbetrieb zu 1 gesetzt  | 0/1 | LV_CYL_BAL_AD_WG_OPEN_REQ[1] | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5BB9 | STAT_0x5BB9_WERT | Zylindersel. Lambdaregelung fordert öffnen WG2 an, zyklisch während dem Motorbetrieb zu 1 gesetzt  | 0/1 | LV_CYL_BAL_AD_WG_OPEN_REQ[2] | - | 0xFF | - | 1 | 1 | 0 |
| - | 0x5BBA | STAT_0x5BBA_WERT | Relative Zeit Homogen-Betrieb gesamter Motorlauf | % | RT_BASTATG_H | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5BBB | STAT_0x5BBB_WERT | Relative Zeit Homogen-Schicht-Betrieb gesamter Motorlauf | % | RT_BASTATG_HS | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5BBC | STAT_0x5BBC_WERT | Relative Zeit Schicht-Betrieb gesamter Motorlauf | % | RT_BASTATG_S | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5BBD | STAT_0x5BBD_WERT | Relative Zeit Homogen-Betrieb gesamter Motorlauf | % | RT_BASTATG_SA | - | unsigned integer | - | 0,00152587890625 | 1 | 0,0 |
| - | 0x5BCA | STAT_0x5BCA_WERT | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt A | % | FAC_LAM_TCO_A[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BCB | STAT_0x5BCB_WERT | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt A | % | FAC_LAM_TCO_A[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BCC | STAT_0x5BCC_WERT | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt B | % | FAC_LAM_TCO_B[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BCD | STAT_0x5BCD_WERT | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt B | % | FAC_LAM_TCO_B[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BCE | STAT_0x5BCE_WERT | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt C | % | FAC_LAM_TCO_C[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BCF | STAT_0x5BCF_WERT | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt C | % | FAC_LAM_TCO_C[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BD0 | STAT_0x5BD0_WERT | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt D | % | FAC_LAM_TCO_D[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BD1 | STAT_0x5BD1_WERT | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt D | % | FAC_LAM_TCO_D[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BD2 | STAT_0x5BD2_WERT | Lambda-Teillastadaption Bank 1 im Kühlmitteltemperaturmesspunkt E | % | FAC_LAM_TCO_E[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BD3 | STAT_0x5BD3_WERT | Lambda-Teillastadaption Bank 2 im Kühlmitteltemperaturmesspunkt E | % | FAC_LAM_TCO_E[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BE0 | STAT_0x5BE0_WERT | CILC-Adaptionswert warm High-Range Injektor 1 | % | FAC_LAM_CYL_SEL_ADJ_H_RNG[0] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BE1 | STAT_0x5BE1_WERT | CILC-Adaptionswert warm High-Range Injektor 2 | % | FAC_LAM_CYL_SEL_ADJ_H_RNG[4] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BE2 | STAT_0x5BE2_WERT | CILC-Adaptionswert warm High-Range Injektor 3 | % | FAC_LAM_CYL_SEL_ADJ_H_RNG[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BE3 | STAT_0x5BE3_WERT | CILC-Adaptionswert warm High-Range Injektor 4 | % | FAC_LAM_CYL_SEL_ADJ_H_RNG[5] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BE4 | STAT_0x5BE4_WERT | CILC-Adaptionswert warm High-Range Injektor 5 | % | FAC_LAM_CYL_SEL_ADJ_H_RNG[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BE5 | STAT_0x5BE5_WERT | CILC-Adaptionswert warm High-Range Injektor 6 | % | FAC_LAM_CYL_SEL_ADJ_H_RNG[3] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BF0 | STAT_0x5BF0_WERT | CILC-Adaptionswert warm Low-Range Injektor 1 | % | FAC_LAM_CYL_SEL_ADJ_L_RNG[0] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BF1 | STAT_0x5BF1_WERT | CILC-Adaptionswert warm Low-Range Injektor 2 | % | FAC_LAM_CYL_SEL_ADJ_L_RNG[4] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BF2 | STAT_0x5BF2_WERT | CILC-Adaptionswert warm Low-Range Injektor 3 | % | FAC_LAM_CYL_SEL_ADJ_L_RNG[2] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BF3 | STAT_0x5BF3_WERT | CILC-Adaptionswert warm Low-Range Injektor 41 | % | FAC_LAM_CYL_SEL_ADJ_L_RNG[5] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BF4 | STAT_0x5BF4_WERT | CILC-Adaptionswert warm Low-Range Injektor 5 | % | FAC_LAM_CYL_SEL_ADJ_L_RNG[1] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x5BF5 | STAT_0x5BF5_WERT | CILC-Adaptionswert warm Low-Range Injektor 6 | % | FAC_LAM_CYL_SEL_ADJ_L_RNG[3] | - | signed integer | - | 0,00152587890625 | 1 | 2,22044609888115E-14 |
| - | 0x58FF | - | Umweltbedingung unbekannt | - | - | - | unsigned char | - | 1 | 1 | 0 |

<a id="table-fartstatustexte"></a>
### FARTSTATUSTEXTE

Dimensions: 9 rows × 2 columns

| BITNR | BITTEXT |
| --- | --- |
| 0x00 | nicht aktiv |
| 0x01 | Fehler momentan vorhanden |
| 0x02 | Fehler geprueft |
| 0x11 | E-Flag entprellt |
| 0x12 | CARB-entprellt |
| 0x13 | SCATT-aktiv |
| 0x14 | MIL ein |
| 0x15 | MIL blink |
| 0x16 | Fehler sporadisch |

<a id="table-bits"></a>
### BITS

Dimensions: 23 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| OBD_MIL | 0 | 0x80 | 0x80 |
| OBD_VERBRENNUNGSAUSSETZER_MONITOR | 1 | 0x01 | 0x01 |
| OBD_KRAFTSTOFFSYSTEM_MONITOR | 1 | 0x02 | 0x02 |
| OBD_KOMPONENTEN_MONITOR | 1 | 0x04 | 0x04 |
| OBD_VERBRENNUNGSAUSSETZER_READINESS | 1 | 0x10 | 0x10 |
| OBD_KRAFTSTOFFSYSTEM_READINESS | 1 | 0x20 | 0x20 |
| OBD_KOMPONENTEN_READINESS | 1 | 0x40 | 0x40 |
| OBD_KAT_UEBERWACHUNG_MONITOR | 2 | 0x01 | 0x01 |
| OBD_KAT_HEIZUNG_MONITOR | 2 | 0x02 | 0x02 |
| OBD_TANKENTLUEFTUNG_MONITOR | 2 | 0x04 | 0x04 |
| OBD_SEKUNDAERLUFTSYSTEM_MONITOR | 2 | 0x08 | 0x08 |
| OBD_KLIMA_MONITOR | 2 | 0x10 | 0x10 |
| OBD_LAMBDASONDE_MONITOR | 2 | 0x20 | 0x20 |
| OBD_LAMBDASONDENHEIZUNG_MONITOR | 2 | 0x40 | 0x40 |
| OBD_ABGASRUECKFUEHRUNG_MONITOR | 2 | 0x80 | 0x80 |
| OBD_KAT_UEBERWACHUNG_READINESS | 3 | 0x01 | 0x01 |
| OBD_KAT_HEIZUNG_READINESS | 3 | 0x02 | 0x02 |
| OBD_TANKENTLUEFTUNG_READINESS | 3 | 0x04 | 0x04 |
| OBD_SEKUNDAERLUFTSYSTEM_READINESS | 3 | 0x08 | 0x08 |
| OBD_KLIMA_READINESS | 3 | 0x10 | 0x10 |
| OBD_LAMBDASONDE_READINESS | 3 | 0x20 | 0x20 |
| OBD_LAMBDASONDENHEIZUNG_READINESS | 3 | 0x40 | 0x40 |
| OBD_ABGASRUECKFUEHRUNG_READINESS | 3 | 0x80 | 0x80 |

<a id="table-lambdastatus"></a>
### LAMBDASTATUS

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | 1 Regelung AUS, Einschaltbedingung noch nicht erfuellt |
| 0x02 | 2 Regelung EIN |
| 0x04 | 3 Regelung AUS wegen Fahrbedingung |
| 0x08 | 4 Regelung AUS wegen erkanntem Fehler |
| 0x10 | 5 Regelung EIN mit Einschraenkung (Sensor Fehler) |
| 0xXY | Status unbekannt |

<a id="table-grobname"></a>
### GROBNAME

Dimensions: 48 rows × 2 columns

| ADR | GROBNAME |
| --- | --- |
| 0x00 | JBBF |
| 0x01 | MRS |
| 0x12 | DME/DDE |
| 0x13 | DME/DDE |
| 0x16 | AFS |
| 0x17 | EKP |
| 0x18 | EGS |
| 0x19 | VGSG |
| 0x1C | LDM |
| 0x1D | FFP |
| 0x20 | RDC |
| 0x21 | ACC |
| 0x24 | CVM |
| 0x27 | PGS |
| 0x29 | DSC |
| 0x30 | EPS |
| 0x35 | SVS |
| 0x36 | TEL |
| 0x37 | AMP |
| 0x38 | EHC |
| 0x3B | NAV |
| 0x3C | CDC |
| 0x3F | ASK |
| 0x40 | CAS |
| 0x41 | DWA |
| 0x44 | SHD/MDS |
| 0x47 | ANTTU |
| 0x4B | VIDEO |
| 0x50 | SINE |
| 0x54 | RADIO |
| 0x56 | FZD |
| 0x60 | KOMBI |
| 0x61 | FBI |
| 0x62 | MOSTGW |
| 0x63 | MASK/CCC |
| 0x64 | PDC |
| 0x67 | ZBE |
| 0x6D | FAS |
| 0x6E | BFS |
| 0x71 | AHM |
| 0x72 | FRM |
| 0x73 | CID |
| 0x78 | KLIMA |
| 0xA0 | CCC |
| 0x90 | VIRTSG90 |
| 0x91 | VIRTSG91 |
| 0x92 | VIRTSG92 |
| 0xXY | ???? |

<a id="table-farterwtexte"></a>
### FARTERWTEXTE

Dimensions: 8 rows × 2 columns

| BITNR | BITTEXT |
| --- | --- |
| 0x00 | nicht aktiv |
| 0x11 | Diagnose aktiv |
| 0x12 | Diagnose gestoppt |
| 0x13 | Zyklus-Flag gesetzt |
| 0x14 | Error-Flag gesetzt |
| 0x15 | MIL ein |
| 0x16 | Fehler in Entprellphase |
| 0xXY | Status unbekannt |

<a id="table-cnv-s-10-state-eol-452"></a>
### _CNV_S_10_STATE_EOL__452

Dimensions: 11 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | NOT_START |
| 0x01 | ST_INH |
| 0x02 | PAR_NOT_PLAUS |
| 0x03 | WAIT_REL |
| 0x04 | UNDEF |
| 0x05 | ACT |
| 0x06 | END_WOUT_RESULT |
| 0x07 | ABORTED |
| 0x08 | END_WOUT_ERR |
| 0x09 | END_WITH_ERR |
| 0xFF | undefiniert |

<a id="table-cnv-s-11-def-ba-wm-614"></a>
### _CNV_S_11_DEF_BA_WM_614

Dimensions: 12 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | Keine |
| 0x01 | WARMLAUF |
| 0x02 | ECO |
| 0x03 | NORMAL |
| 0x04 | HIGH |
| 0x05 | HIGH+KFT |
| 0x06 | BAUTEILSCHUTZ |
| 0x07 | HEIZLEISTUNG |
| 0x08 | NOTLAUF |
| 0x09 | APPLIKATION |
| 0x0A | Befuellen/Entlueften |
| 0xFF | undefiniert |

<a id="table-cnv-s-11-egcp-range-375"></a>
### _CNV_S_11_EGCP_RANGE_375

Dimensions: 12 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | NO_FAULT |
| 0x01 | SCG_LINE_RCD |
| 0x02 | SCG_LINE_VIP |
| 0x03 | SCG_LINE_VG |
| 0x04 | SCG_LINE_VN |
| 0x05 | SCG |
| 0x06 | SCBAT_LINE_RCD |
| 0x07 | SCBAT_LINE_VIP |
| 0x08 | SCBAT_LINE_VG |
| 0x09 | SCBAT_LINE_VN |
| 0x0A | SCBAT |
| 0xFF | undefiniert |

<a id="table-cnv-s-11-range-stat-941"></a>
### _CNV_S_11_RANGE_STAT_941

Dimensions: 12 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | VAR_ECU_NOT_LEARNED |
| 0x11 | VAR_ECU_LEARNING_FAILED |
| 0x2A | VAR_ECU_C2_LOT2 |
| 0x4E | VAR_ECU_C1_LOT3 |
| 0x5A | VAR_ECU_C1_LOT1 |
| 0xA2 | VAR_ECU_C2_LOT1 |
| 0xA5 | VAR_ECU_C1_LOT2 |
| 0xAE | VAR_ECU_C1_LOT4 |
| 0xBC | VAR_ECU_SERIAL_ECU |
| 0xE4 | VAR_ECU_C2_LOT3 |
| 0xFF | VAR_ECU_ROM_NOT_PLAUS |
| 0xFF | undefiniert |

<a id="table-cnv-s-4-egcp-range-377"></a>
### _CNV_S_4_EGCP_RANGE_377

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | NO_SYM |
| 0x01 | TTIP_ERR |
| 0x02 | READY_ERR |
| 0x04 | TTIP_MES_ERR |
| 0xFF | undefiniert |

<a id="table-cnv-s-4-egcp-range-384"></a>
### _CNV_S_4_EGCP_RANGE_384

Dimensions: 5 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | VLS_OK |
| 0x01 | VLS_L |
| 0x02 | VLS_H_OC |
| 0x04 | VLS_AFS_OC |
| 0xFF | undefiniert |

<a id="table-cnv-s-5-def-ba-gdi-609"></a>
### _CNV_S_5_DEF_BA_GDI_609

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | KEINE |
| 0x01 | Schicht |
| 0x02 | Homogen |
| 0x03 | Homogen_Schicht |
| 0x08 | NOTLAUF |
| 0xFF | undefiniert |

<a id="table-cnv-s-5-laco-range-410"></a>
### _CNV_S_5_LACO_RANGE_410

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x01 | 1:OL_CDN |
| 0x02 | 2:CL |
| 0x04 | 4:OL_INTR |
| 0x08 | 8:OL_ERR |
| 0x10 | 10:CL_ERR |
| 0xFF | undefiniert |

<a id="table-cnv-s-5-range-stat-290"></a>
### _CNV_S_5_RANGE_STAT_290

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | ETC_NO_LIH |
| 0x01 | ETC_LIH_1 |
| 0x02 | ETC_LIH_2_REV |
| 0x04 | ETC_LIH_2 |
| 0x08 | ETC_LIH_3 |
| 0xFF | undefiniert |

<a id="table-cnv-s-5-range-stat-971"></a>
### _CNV_S_5_RANGE_STAT_971

Dimensions: 6 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | HEAT_OFF |
| 0x01 | HEAT_OFF_DLY |
| 0x02 | HEAT_ON_DLY |
| 0x03 | HEAT_ON |
| 0x04 | HEAT_EXT_ADJ |
| 0xFF | undefiniert |

<a id="table-cnv-s-6-acrc-range-871"></a>
### _CNV_S_6_ACRC_RANGE_871

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | ACR_AD_INIT |
| 0x01 | ACR_AD_BOL |
| 0x02 | ACR_GO_TOL |
| 0x03 | ACR_AD_TOL |
| 0x04 | ACR_GO_BOL |
| 0x05 | ACR_AD_END |
| 0xFF | undefiniert |

<a id="table-cnv-s-6-range-stat-106"></a>
### _CNV_S_6_RANGE_STAT_106

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | PASSIVE |
| 0x01 | CONST_DRIVE |
| 0x03 | RESUME |
| 0x05 | SET_ACC |
| 0x07 | RETARD |
| 0x09 | TIP |
| 0xFF | undefiniert |

<a id="table-cnv-s-6-range-stat-167"></a>
### _CNV_S_6_RANGE_STAT_167

Dimensions: 7 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | ES |
| 0x01 | ST |
| 0x02 | IS |
| 0x03 | PL |
| 0x04 | PU |
| 0x05 | PUC |
| 0xFF | undefiniert |

<a id="table-cnv-s-7-egcp-range-357"></a>
### _CNV_S_7_EGCP_RANGE_357

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | LSH_OFF |
| 0x01 | LSH_POW_RISE |
| 0x02 | LSH_POW_RED |
| 0x03 | LSH_POW_FALL |
| 0x04 | LSH_POW_CTL |
| 0x05 | LSH_VB_PROT |
| 0x06 | LSH_TEMP_PROT |
| 0xFF | undefiniert |

<a id="table-cnv-s-7-range-ecu-165"></a>
### _CNV_S_7_RANGE_ECU__165

Dimensions: 8 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | ENG_STOP |
| 0x01 | RUN_ENG |
| 0x02 | SYN_ENG_IGK_ON |
| 0x03 | SYN_ENG_IGK_OFF |
| 0x04 | PWL |
| 0x05 | ENG_LOCK |
| 0x06 | WAKE_UP |
| 0xFF | undefiniert |

<a id="table-cnv-s-8-range-stat-21"></a>
### _CNV_S_8_RANGE_STAT_21

Dimensions: 9 rows × 2 columns

| WERT | UWTEXT |
| --- | --- |
| 0x00 | None |
| 0x01 | Set-Acc-TipUp |
| 0x02 | Decelerate-TipDown |
| 0x03 | Resume |
| 0x04 | Off |
| 0x05 | - |
| 0x06 | - |
| 0x07 | Error |
| 0xFF | undefiniert |

<a id="table-funktionaleadresse"></a>
### FUNKTIONALEADRESSE

Dimensions: 8 rows × 3 columns

| NR | F_ADR | F_ADR_TEXT |
| --- | --- | --- |
| 0xE9 | K-CAN | Karosserie-CAN Steuergeräte |
| 0xEA | PT-CAN | Powertrain-CAN Steuergeräte |
| 0xEB | SI | Sicherheits-BUS Steuergeräte |
| 0xEC | MOST | MOST-BUS Steuergeräte |
| 0xED | BOS | Bedarfsorientierter Service |
| 0xED | CBS | Bedarfsorientierter Service |
| 0xEE | PERSONAL | Personalisierung |
| 0xEF | ALL | alle Steuergeräte |

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

<a id="table-stat-ruhestrom"></a>
### STAT_RUHESTROM

Dimensions: 17 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0x00 | 0 keine Ruhestromverletzung, keine Standverbraucher aktiv |
| 0x01 | 1 Ruhestrom 80 bis 200mA aktiv, keine Standverbraucher aktiv |
| 0x02 | 2 Ruhestrom 200 bis 1000mA aktiv, keine Standverbraucher aktiv |
| 0x03 | 3 Ruhestrom über 1000mA aktiv, keine Standverbraucher aktiv |
| 0x04 | 4 keine Ruhestromverletzung, Standverbraucher Licht aktiv |
| 0x05 | 5 Ruhestrom 80 bis 200mA aktiv, Standverbraucher Licht aktiv |
| 0x06 | 6 Ruhestrom 200 bis 1000mA aktiv, Standverbraucher Licht aktiv |
| 0x07 | 7 Ruhestrom über 1000mA aktiv, Standverbraucher Licht aktiv |
| 0x08 | 8 keine Ruhestromverletzung, Standverbraucher Standheizung aktiv |
| 0x09 | 9 Ruhestrom 80 bis 200mA aktiv, Standverbraucher Standheizung aktiv |
| 0x0A | 10 Ruhestrom 200 bis 1000mA aktiv, Standverbraucher Standheizung aktiv |
| 0x0B | 11 Ruhestrom über 1000mA aktiv, Standverbraucher Standheizung aktiv |
| 0x0C | 12 keine Ruhestromverletzung, Standverbraucher Sonstige aktiv |
| 0x0D | 13 Ruhestrom 80 bis 200mA aktiv, Standverbraucher Sonstige aktiv |
| 0x0E | 14 Ruhestrom 200 bis 1000mA aktiv, Standverbraucher Sonstige aktiv |
| 0x0F | 15 Ruhestrom über 1000mA aktiv, Standverbraucher Sonstige aktiv |
| 0xFF | 255 Status unbekannt |

<a id="table-msd8asam-table-msa-ursache-ea"></a>
### _MSD8ASAM_TABLE_MSA_URSACHE_EA

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein EA |
| 1 | EA infolge I_BN |
| 2 | EA infolge D_SoC |
| 3 | nicht definiert |

<a id="table-msd8asam-table-uen"></a>
### _MSD8ASAM_TABLE_UEN

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 1 | Ruecksetzung erfolgt |
| 2 | Ruecksetzung nicht erfolgt |

<a id="table-msd8asam-cnv-s-5-def-ba-gdi-588-cm"></a>
### _MSD8ASAM_CNV_S_5_DEF_BA_GDI_588_CM

Dimensions: 5 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Keine |
| 1 | Schicht |
| 2 | Homogen |
| 3 | Homogen_Schicht |
| 8 | Notlauf |

<a id="table-msd8asam-cnv-s-2-def-bit-ub-741-cm"></a>
### _MSD8ASAM_CNV_S_2_DEF_BIT_UB_741_CM

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Falsch |
| 1 | Wahr |

<a id="table-msd8asam-cnv-s-2-def-bit-ub-755-cm-4dc3300s"></a>
### _MSD8ASAM_CNV_S_2_DEF_BIT_UB_755_CM_4DC3300S

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Auslieferungszustand |
| 1 | Abweichung zum Auslieferungszustand |

<a id="table-msd8asam-cnv-s-2-def-bit-ub-755-cm0x2-4dc3300s"></a>
### _MSD8ASAM_CNV_S_2_DEF_BIT_UB_755_CM0X2_4DC3300S

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Schaltpunktanzeige inaktiv |
| 1 | Schaltpunktanzeige aktiv |

<a id="table-msd8asam-cnv-s-10-state-eol-449-cm-4dc3200s"></a>
### _MSD8ASAM_CNV_S_10_STATE_EOL__449_CM_4DC3200S

Dimensions: 10 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Startbedingungen nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | Undefinierter Zustand |
| 5 | Funktionstest laeuft |
| 6 | Funktion ergebnislos beendet |
| 7 | Funktion abgebrochen |
| 8 | Funktion durchlaufen und kein Fehler erkannt |
| 9 | Funktion durchlaufen und Fehler erkannt |

<a id="table-msd8asam-cnv-s-10-state-eol-450-cm-4dc3200s"></a>
### _MSD8ASAM_CNV_S_10_STATE_EOL__450_CM_4DC3200S

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Passiv |
| 1 | Drehzahlerhoehung |
| 2 | Aufheizphase Katalysator |
| 3 | Desulfatisierung |

<a id="table-msd8asam-table-switch-position-high-byte-bit7"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT7

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Regelkreis Bank 1 nicht geschlossen |
| 1 | Regelkreis Bank 1 geschlossen |

<a id="table-msd8asam-table-switch-position-high-byte-bit6"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT6

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Regelkreis Bank 2 nicht geschlossen |
| 1 | Regelkreis Bank 2 geschlossen |

<a id="table-msd8asam-table-switch-position-high-byte-bit5"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT5

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Lambdaregelung vor Katalysator Bank 1 nicht aktiv |
| 1 | Lambdaregelung vor Katalysator Bank 1 aktiv |

<a id="table-msd8asam-table-switch-position-high-byte-bit4"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Lambdaregelung vor Katalysator Bank 2 nicht aktiv |
| 1 | Lambdaregelung vor Katalysator Bank 2 aktiv |

<a id="table-msd8asam-table-switch-position-high-byte-bit3"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Lambdaregelung hinter Katalysator Bank 2 nicht aktiv |
| 1 | Lambdaregelung hinter Katalysator Bank 2 aktiv |

<a id="table-msd8asam-table-switch-position-high-byte-bit2"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Lambdaregelung hinter Katalysator Bank 1 nicht aktiv |
| 1 | Lambdaregelung hinter Katalysator Bank 1 aktiv |

<a id="table-msd8asam-table-switch-position-high-byte-bit1"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT1

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | keine Vollast |
| 1 | Vollast |

<a id="table-msd8asam-table-switch-position-high-byte-bit0"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_HIGH_BYTE_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein Leerlauf |
| 1 | Leerlauf |

<a id="table-msd8asam-table-switch-position-low-byte-bit7"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_LOW_BYTE_BIT7

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Drosselklappen-Neuabgleich nicht erforderlich |
| 1 | Drosselklappen-Neuabgleich erforderlich |

<a id="table-msd8asam-table-switch-position-low-byte-bit6"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_LOW_BYTE_BIT6

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | keine Schubabschaltung aktiv |
| 1 | Schubabschaltung aktiv |

<a id="table-msd8asam-table-switch-position-low-byte-bit3"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_LOW_BYTE_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Gang nicht eingelegt, Park- oder Neutralstellung |
| 1 | Gang eingelegt, nicht Park- oder Neutralstellung |

<a id="table-msd8asam-table-switch-position-low-byte-bit2"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_LOW_BYTE_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein Kickdown erkannt |
| 1 | Kickdown erkannt |

<a id="table-msd8asam-table-tempomat-aus-irr-low-byte-bit5"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_LOW_BYTE_BIT5

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein Fehler Bremse |
| 1 | Fehler Bremse |

<a id="table-msd8asam-table-tempomat-aus-irr-low-byte-bit4"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_LOW_BYTE_BIT4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein Timeout EGS |
| 1 | Timeout EGS |

<a id="table-msd8asam-table-tempomat-aus-irr-low-byte-bit3"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_LOW_BYTE_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein Fehler Multifunktionslenkrad |
| 1 | Fehler Multifunktionslenkrad |

<a id="table-msd8asam-table-tempomat-aus-irr-low-byte-bit2"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_LOW_BYTE_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein Fehler Kupplungsschalter |
| 1 | Fehler Kupplungsschalter |

<a id="table-msd8asam-table-tempomat-aus-irr-low-byte-bit1"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_LOW_BYTE_BIT1

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein Notlauf Limit Dynamik 2 |
| 1 | Notlauf Limit Dynamik 2 |

<a id="table-msd8asam-table-tempomat-aus-irr-low-byte-bit0"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_LOW_BYTE_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein Notlauf Limit Dynamik 1 |
| 1 | Notlauf Limit Dynamik 1 |

<a id="table-msd8asam-table-tempomat-aus-irr-high-byte-bit6"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT6

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein EGAS-Notlauf |
| 1 | EGAS-Notlauf |

<a id="table-msd8asam-table-tempomat-aus-irr-high-byte-bit5"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT5

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | keine Kommunikation zum ASR-Steuergeraet |
| 1 | Kommunikation zum ASR-Steuergeraet |

<a id="table-msd8asam-table-tempomat-aus-irr-high-byte-bit4"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein Fehler Geschwindigkeit |
| 1 | Fehler Geschwindigkeit |

<a id="table-msd8asam-table-tempomat-aus-irr-high-byte-bit3"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein Notlauf DK-Steller |
| 1 | Notlauf DK-Steller |

<a id="table-msd8asam-table-tempomat-aus-irr-high-byte-bit2"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein Notlauf LL-Steller |
| 1 | Notlauf LL-Steller |

<a id="table-msd8asam-table-tempomat-aus-irr-high-byte-bit1"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT1

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Geschwindigkeit unplausibel |
| 1 | Geschwindigkeit plausibel |

<a id="table-msd8asam-table-tempomat-aus-irr-high-byte-bit0"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_IRR_HIGH_BYTE_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Monitoring Ebene 2 aus |
| 1 | Monitoring Ebene 2 ein |

<a id="table-msd8asam-table-tempomat-aus-rev-low-byte-bit4"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_LOW_BYTE_BIT4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Multifunktionslenkrad nicht ausgeschaltet |
| 1 | Multifunktionslenkrad ausgeschaltet |

<a id="table-msd8asam-table-tempomat-aus-rev-low-byte-bit3"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_LOW_BYTE_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | kein externer Drehmomenteneingriff |
| 1 | externer Drehmomenteneingriff |

<a id="table-msd8asam-table-tempomat-aus-rev-low-byte-bit2"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_LOW_BYTE_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Sollwert fuer maximale Geschwindigkeit nicht zu lang |
| 1 | Sollwert fuer maximale Geschwindigkeit zu lang |

<a id="table-msd8asam-table-tempomat-aus-rev-low-byte-bit1"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_LOW_BYTE_BIT1

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Geschwindigkeitsuebernahme nicht zu lang |
| 1 | Geschwindigkeitsuebernahme zu lang |

<a id="table-msd8asam-table-tempomat-aus-rev-low-byte-bit0"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_LOW_BYTE_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Geschwindigkeitsdifferenz nicht zu hoch |
| 1 | Geschwindigkeitsdifferenz zu hoch |

<a id="table-msd8asam-table-tempomat-aus-rev-high-byte-bit7"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT7

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Multifunktionslenkrad Notaus nicht aktiv |
| 1 | Multifunktionslenkrad Notaus aktiv |

<a id="table-msd8asam-table-tempomat-aus-rev-high-byte-bit6"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT6

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Bremsen nicht festgestellt |
| 1 | Bremsen festgestellt |

<a id="table-msd8asam-table-tempomat-aus-rev-high-byte-bit5"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT5

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Drehzahlbegrenzung nicht aktiv |
| 1 | Drehzahlbegrenzung aktiv |

<a id="table-msd8asam-table-tempomat-aus-rev-high-byte-bit4"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Geschwindigkeit nicht zu gering |
| 1 | Geschwindigkeit zu gering |

<a id="table-msd8asam-table-tempomat-aus-rev-high-byte-bit3"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Uebernahme und Maximalgeschwindigkeit nicht aktiv |
| 1 | Uebernahme und Maximalgeschwindigkeit aktiv |

<a id="table-msd8asam-table-tempomat-aus-rev-high-byte-bit2"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Hochdrehsicherung nicht aktiv |
| 1 | Hochdrehsicherung aktiv |

<a id="table-msd8asam-table-tempomat-aus-rev-high-byte-bit1"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT1

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Beschleunigungsueberwachung nicht aktiv |
| 1 | Beschleunigungsueberwachung aktiv |

<a id="table-msd8asam-table-tempomat-aus-rev-high-byte-bit0"></a>
### _MSD8ASAM_TABLE_TEMPOMAT_AUS_REV_HIGH_BYTE_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | CAN-Botschaft Geschwindigkeit nicht zu lang |
| 1 | CAN-Botschaft Geschwindigkeit zu lang |

<a id="table-msd8asam-table-switch-position-bit7"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_BIT7

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Anforderung Klimabereitschaft aus |
| 1 | Anforderung Klimabereitschaft ein |

<a id="table-msd8asam-table-switch-position-bit4"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_BIT4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Bremslichtschalter-Kanal 2 aus |
| 1 | Bremslichtschalter-Kanal 2 ein |

<a id="table-msd8asam-table-switch-position-bit3"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Bremslichtschalter-Kanal 1 aus |
| 1 | Bremslichtschalter-Kanal 1 ein |

<a id="table-msd8asam-table-switch-position-bit2"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Kupplung aus |
| 1 | Kupplung ein |

<a id="table-msd8asam-table-switch-position-bit1"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_BIT1

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Motor laeuft |
| 1 | Motor steht |

<a id="table-msd8asam-table-switch-position-bit0"></a>
### _MSD8ASAM_TABLE_SWITCH_POSITION_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Klemme-15 aus |
| 1 | Klemme-15 ein |

<a id="table-msd8asam-cnv-s-8-range-stat-19-cm"></a>
### _MSD8ASAM_CNV_S_8_RANGE_STAT_19_CM

Dimensions: 8 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Heizung aus |
| 1 | Warten auf Heizung aus |
| 2 | Warten auf Heizung an |
| 3 | Heizung an |
| 4 | Heizung, externe Ansteuerung |
| 5 | - |
| 6 | -- |
| 7 | Fehler |

<a id="table-msd8asam-cnv-s-2-def-bit-ub-716-cm0x4"></a>
### _MSD8ASAM_CNV_S_2_DEF_BIT_UB_716_CM0X4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Falsch |
| 4 | Wahr |

<a id="table-msd8asam-cnv-s-4-range-stat-455-cm-4dc3200s"></a>
### _MSD8ASAM_CNV_S_4_RANGE_STAT_455_CM_4DC3200S

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Deaktiviert |
| 1 | Fertigungsmodus |
| 2 | Transportmodus |
| 3 | Werkstattmodus |

<a id="table-msd8asam-tabel-status-obd-readiness"></a>
### _MSD8ASAM_TABEL_STATUS_OBD_READINESS

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Test abgeschlossen oder nicht anwendbar |
| 1 | Test nicht abgeschlossen |

<a id="table-msd8asam-tabel-status-obd-monitor"></a>
### _MSD8ASAM_TABEL_STATUS_OBD_MONITOR

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Test wird durch dieses Modul nicht unterstuetzt |
| 1 | Test wird durch dieses Modul unterstuetzt |

<a id="table-msd8asam-table-fs"></a>
### _MSD8ASAM_TABLE_FS

Dimensions: 10 rows × 2 columns

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

<a id="table-msd8asam-cnv-s-13-state-dmtl-140-cm"></a>
### _MSD8ASAM_CNV_S_13_STATE_DMTL_140_CM

Dimensions: 13 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Start |
| 1 | Erste Referenzleck Messung |
| 2 | Grobleck Messung Start |
| 3 | Grobleck Messung erweitert |
| 4 | Grobleck Messung beendet |
| 5 | Feinleck Messung Start |
| 6 | Feinleck Messung erweitert |
| 7 | Zweite Referenzleck Messung |
| 8 | Tank geprueft |
| 9 | Feinleck |
| 10 | Grobleck |
| 11 | Modulfehler |
| 12 | Ende |

<a id="table-msd8asam-table-st-gentest"></a>
### _MSD8ASAM_TABLE_ST_GENTEST

Dimensions: 8 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 1 | Start-/Ansteuerbedingung nicht erfuellt |
| 2 | Uebergabeparameter nicht plausibel |
| 3 | Funktion wartet auf Freigabe |
| 4 | -- |
| 5 | Funktion laeuft |
| 6 | Funktion beendet |
| 7 | Funktion abgebrochen |

<a id="table-msd8asam-table-geniutest-err-bit0"></a>
### _MSD8ASAM_TABLE_GENIUTEST_ERR_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, elektrischer Fehler Generator nicht vorhanden |
| 1 | Generatortest, elektrischer Fehler Generator vorhanden |

<a id="table-msd8asam-table-geniutest-err-bit1"></a>
### _MSD8ASAM_TABLE_GENIUTEST_ERR_BIT1

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, mechanischer Fehler Generator nicht vorhanden |
| 1 | Generatortest, mechanischer Fehler Generator vorhanden |

<a id="table-msd8asam-table-geniutest-err-bit2"></a>
### _MSD8ASAM_TABLE_GENIUTEST_ERR_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Hochtemperaturfehler Generator nicht vorhanden |
| 1 | Generatortest, Hochtemperaturfehler Generator vorhanden |

<a id="table-msd8asam-table-geniutest-err-bit3"></a>
### _MSD8ASAM_TABLE_GENIUTEST_ERR_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatortyp unplausibel |
| 1 | Generatortest, Generatortyp plausibel |

<a id="table-msd8asam-table-geniutest-err-bit4"></a>
### _MSD8ASAM_TABLE_GENIUTEST_ERR_BIT4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, keine Generatorkommunikation vorhanden |
| 1 | Generatortest, Generatorkommunikation vorhanden |

<a id="table-msd8asam-table-geniutest-err-bit5"></a>
### _MSD8ASAM_TABLE_GENIUTEST_ERR_BIT5

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorspannung aus Berechnung unplausibel |
| 1 | Generatortest, Generatorspannung aus Berechnung plausibel |

<a id="table-msd8asam-table-geniutest-err-bit6"></a>
### _MSD8ASAM_TABLE_GENIUTEST_ERR_BIT6

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Hochtemperaturfehler Generator aus Berechnung nicht vorhanden |
| 1 | Generatortest, Hochtemperaturfehler Generator aus Berechnung vorhanden |

<a id="table-msd8asam-table-geniutest-err-bit7"></a>
### _MSD8ASAM_TABLE_GENIUTEST_ERR_BIT7

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorregler unplausibel |
| 1 | Generatortest, Generatorregler plausibel |

<a id="table-msd8asam-table-geniutest-ab-bit0"></a>
### _MSD8ASAM_TABLE_GENIUTEST_AB_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Generatortest, Generatorauslastung nicht zu hoch |
| 1 | Generatortest, Generatorauslastung zu hoch |

<a id="table-msd8asam-table-glf-high-byte-bit7"></a>
### _MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT7

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, kein Fehler erkannt |
| 1 | gesteuerte Luftfuehrung, Fehler erkannt |

<a id="table-msd8asam-table-glf-high-byte-bit6"></a>
### _MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT6

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, Kommunikation noch nicht getestet |
| 1 | gesteuerte Luftfuehrung, Kommunikation in Ordnung |

<a id="table-msd8asam-table-glf-high-byte-bit5"></a>
### _MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT5

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, Testeransteuerung obere Luftklappe nicht aktiv |
| 1 | gesteuerte Luftfuehrung, Testeransteuerung obere Luftklappe aktiv |

<a id="table-msd8asam-table-glf-high-byte-bit4"></a>
### _MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, Testeransteuerung untere Luftklappe nicht aktiv |
| 1 | gesteuerte Luftfuehrung, Testeransteuerung untere Luftklappe aktiv |

<a id="table-msd8asam-table-glf-high-byte-bit3"></a>
### _MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, Eigendiagnose untere Luftklappe noch nicht beendet |
| 1 | gesteuerte Luftfuehrung, Eigendiagnose untere Luftklappe beendet |

<a id="table-msd8asam-table-glf-high-byte-bit2"></a>
### _MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, Eigendiagnose obere Luftklappe noch nicht beendet |
| 1 | gesteuerte Luftfuehrung, Eigendiagnose obere Luftklappe beendet |

<a id="table-msd8asam-table-glf-high-byte-bit1"></a>
### _MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT1

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, elektrische Diagnose noch nicht beendet |
| 1 | gesteuerte Luftfuehrung, elektrische Diagnose beendet |

<a id="table-msd8asam-table-glf-high-byte-bit0"></a>
### _MSD8ASAM_TABLE_GLF_HIGH_BYTE_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, Systemtest noch nicht gestartet bzw. noch nicht beendet |
| 1 | gesteuerte Luftfuehrung, Systemtest beendet |

<a id="table-msd8asam-table-glf-low-byte-bit7"></a>
### _MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT7

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, kein Systemtest aktiv (Normalbetrieb) |
| 1 | gesteuerte Luftfuehrung, Systemtest aktiv |

<a id="table-msd8asam-table-glf-low-byte-bit6"></a>
### _MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT6

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | untere Luftklappe, kein Fehler durch Eigendiagnose erkannt |
| 1 | untere Luftklappe, Fehler durch Eigendiagnose erkannt |

<a id="table-msd8asam-table-glf-low-byte-bit5"></a>
### _MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT5

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | obere Luftklappe, kein Fehler durch Eigendiagnose erkannt |
| 1 | obere Luftklappe, Fehler durch Eigendiagnose erkannt |

<a id="table-msd8asam-table-glf-low-byte-bit4"></a>
### _MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT4

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, kein elektrischer Fehler |
| 1 | gesteuerte Luftfuehrung, elektrischer Fehler |

<a id="table-msd8asam-table-glf-low-byte-bit3"></a>
### _MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT3

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | keine Fehlerabfrage aktiv, Verstellung moeglich (Normalbetrieb) |
| 1 | Fehlerabfrage aktiv, keine Verstellung moeglich |

<a id="table-msd8asam-table-glf-low-byte-bit2"></a>
### _MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT2

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, untere Luftklappe nicht verbaut |
| 1 | gesteuerte Luftfuehrung, untere Luftklappe verbaut |

<a id="table-msd8asam-table-glf-low-byte-bit1"></a>
### _MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT1

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | gesteuerte Luftfuehrung, obere Luftklappe nicht verbaut |
| 1 | gesteuerte Luftfuehrung, obere Luftklappe verbaut |

<a id="table-msd8asam-table-glf-low-byte-bit0"></a>
### _MSD8ASAM_TABLE_GLF_LOW_BYTE_BIT0

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Varianten lernen noch nicht abgeschlossen |
| 1 | Varianten haetten gelernt werden koennen |

<a id="table-msd8asam-cnv-s-14-state-vls-226-cm-4dc3200s"></a>
### _MSD8ASAM_CNV_S_14_STATE_VLS__226_CM_4DC3200S

Dimensions: 14 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Diagnose nicht aktiv |
| 1 | Diagnose Schritt 1: Fett/Mager |
| 2 | Diagnose Schritt 2: Mager/Fett |
| 3 | Diagnose wartet auf Freigabe |
| 4 | Diagnose Timeout |
| 16 | Diagnose beendet, Sonden in Ordnung |
| 17 | Diagnose beendet, Sonden vor Katalysator vertauscht |
| 18 | Diagnose beendet, Sonden nach Katalysator vertauscht |
| 19 | Diagnose beendet, Sonden vor und nach Katalysator vertauscht |
| 20 | Diagnose beendet, Sonden vor Katalysator Bank 1 nicht plausibel |
| 21 | Diagnose beendet, Sonden vor Katalysator Bank 2 nicht plausibel |
| 22 | Diagnose beendet, Sonden nach Katalysator Bank 1 nicht plausibel |
| 23 | Diagnose beendet, Sonden nach Katalysator Bank 2 nicht plausibel |
| 24 | Diagnose beendet, keine brauchbaren Ergebnisse |

<a id="table-msd8asam-table-st-testpoelsys"></a>
### _MSD8ASAM_TABLE_ST_TESTPOELSYS

Dimensions: 8 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Funktion noch nicht gestartet |
| 3 | Funktion wartet auf Freigabe |
| 4 | -- |
| 5 | Funktionstest laeuft |
| 6 | Funktion beendet |
| 7 | Funktion abgebrochen |
| 8 | Funktion vollstaendig durchlaufen und kein Fehler erkannt |
| 9 | Funktion vollstaendig durchlaufen und Fehler erkannt |

<a id="table-msd8asam-table-st-testpoelsys2"></a>
### _MSD8ASAM_TABLE_ST_TESTPOELSYS2

Dimensions: 7 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | -- |
| 1 | Abbruch durch Tester |
| 2 | Warmlauf (Oeltemperatur zu niedrig) |
| 3 | Abbruch aufgrund zu hoher Oeltemperatur |
| 4 | Abbruch der Diagnosefunktion nach Schritt 1 (Fehlerspeicher auslesen) |
| 5 | Abbruch der Diagnosefunktion nach Schritt 2 (Fehlerspeicher auslesen) |
| 6 | Abbruch der Diagnosefunktion nach Schritt 3 (Fehlerspeicher auslesen) |

<a id="table-msd8asam-cnv-s-6-state-diag-157-cm"></a>
### _MSD8ASAM_CNV_S_6_STATE_DIAG_157_CM

Dimensions: 6 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Initialisierung |
| 1 | Schritt 1 |
| 2 | Schritt 2 |
| 3 | Schritt 3 |
| 4 | Rampe |
| 5 | Ende LOCK_STEP |

<a id="table-msd8asam-cnv-s-8-range-stat-18-cm"></a>
### _MSD8ASAM_CNV_S_8_RANGE_STAT_18_CM

Dimensions: 8 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | keine Taste gedrueckt |
| 1 | Beschleunigen/Taste+ |
| 2 | Verzoegern/Taste- |
| 3 | Taste Setzen/Wiederaufnahme |
| 4 | Taste I/O |
| 5 | - |
| 6 | -- |
| 7 | Fehler |
