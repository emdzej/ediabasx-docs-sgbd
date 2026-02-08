# cem_68.prg

- Jobs: [184](#jobs)
- Tables: [25](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | CleanEnergy Steuergerät |
| ORIGIN | BMW EA-41 Thomas Teske |
| REVISION | 4.001 |
| AUTHOR | Atena TEMS2 Stefan Bauermeister |
| COMMENT | Initial |
| PACKAGE | 1.35 |
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
- [IS_LESEN](#job-is-lesen) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2000 dtcShadowMemory
- [IS_LESEN_DETAIL](#job-is-lesen-detail) - Infospeicher lesen (alle Info-Meldungen / Ort und Art) KWP2000: $22 ReadDataByCommonIdentifier $2001 - $20FF dtcShadowMemoryEntry Modus: Default
- [IS_LOESCHEN](#job-is-loeschen) - Infospeicher loeschen KWP2000: $31 StartRoutineByLocalIdentifier $06 ClearDTCShadowMemory Modus  : Default
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnosemode des SG beenden KWP2000: $20 StopDiagnosticSession Modus  : Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen KWP2000: $10 StartDiagnosticSession Modus  : einstellbar mit diesem Job  Wenn MODE = "ECUPM" ( ECUProgrammingMode ) muss nach dem Job die Steuergeraete-Resetzeit abgewartet werden. Danach ist das Steuergeraet wieder diagnosefaehig  siehe Job FLASH_ZEITEN_LESEN Result FLASH_RESETZEIT
- [SLEEP_MODE](#job-sleep-mode) - SG in Sleep-Mode versetzen KWP2000: $31 StartRoutineByLocalIdentifier a)       $0E Time controlled PowerDown oder b)       $05 PowerDown $00 all ECU Modus  : Default
- [SPEICHER_LESEN](#job-speicher-lesen) - Auslesen des Steuergeraete-Speichers Als Argumente werden uebergeben: Speichersegment, Start-Adresse und Anzahl der Datenbytes KWP 2000: $23 ReadMemoryByAddress Modus   : Default
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Hersteller Seriennummer lesen KWP2000: $1A ReadECUIdentification $89 SystemSupplierECUSerialNumber oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [PHYSIKALISCHE_HW_NR_LESEN](#job-physikalische-hw-nr-lesen) - Auslesen der physikalischen Hardwarenummer KWP2000: $1A ReadECUIdentification $87 physicalECUHardwareNumber (PECUHN) oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [STATUS_BO_PRES](#job-status-bo-pres) - Lesen Ansprechdruck Boil-Off KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_WPDA_LES](#job-status-wpda-les) - Lesen Wärmeleistung PDA KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [STATUS_WPBO_LES](#job-status-wpbo-les) - Lesen Wärmeleistung PBO KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default
- [START_DICHT_TEST](#job-start-dicht-test) - Dichtigkeitstest anfangen KWP2000: $31 StartRoutineByLocalIdentifier $20 StartDichtigkeitsTest Modus  : Default
- [STOP_DICHT_TEST](#job-stop-dicht-test) - Dichtigkeitstest aufhören KWP2000: $32 StopRoutineByLocalIdentifier $20 StopDichtigkeitsTest Modus  : Default
- [ROUT_RES_DICHT_TEST](#job-rout-res-dicht-test) - Ergebnisse des Dichtigkeitstests abfragen KWP2000: $33 RequestRoutineResultsByLocalIdentifier $20 DichtigkeitsTest Modus  : Default
- [ANZAHL_LETZTEN_DICHT_TEST](#job-anzahl-letzten-dicht-test) - Anzahl der Tage seit dem letzten Dichtigkeitstest KWP2000: $21 ReadDataByLocalIdentifier $10 AnzahlTagenLetzenDichtTest Modus  : Default
- [START_VORLAUF_ENTSPANNEN](#job-start-vorlauf-entspannen) - H2-Vorlaufleitung entspannen KWP2000: $31 StartRoutineByLocalIdentifier $21 StartVorlaufEntspannung Modus  : Default
- [START_ZUGANG_TANK](#job-start-zugang-tank) - Zugang zum Tank bzw. zur Entnahmeleitung KWP2000: $31 StartRoutineByLocalIdentifier $22 StartZugangTankEntnahme Modus  : Default
- [STOP_ZUGANG_TANK_ENTNAHME](#job-stop-zugang-tank-entnahme) - ZugangTank aufhören KWP2000: $32 StopRoutineByLocalIdentifier $22 Stop ZugangTankt Modus  : Default
- [START_GASWARN_TEST](#job-start-gaswarn-test) - Test der Gaswarn-LED's starten KWP2000: $31 StartRoutineByLocalIdentifier $23 Gas Warn Test Modus  : Default
- [START_BOIL_OFF_TEST](#job-start-boil-off-test) - Boil Off Test beim nächsten H2-Betrieb auslösen KWP2000: $31 StartRoutineByLocalIdentifier $24 Boil Off Test Modus  : Default
- [START_KALIBR_MASS_TEST](#job-start-kalibr-mass-test) - Kalibrierung der Füllmassenerfassung starten KWP2000: $31 StartRoutineByLocalIdentifier $25 Kalibrierung Modus  : Default
- [START_BEF_ENT_DRUCKSPEICHER](#job-start-bef-ent-druckspeicher) - Befüllen oder Entleeren des Druckspeichers starten KWP2000: $31 StartRoutineByLocalIdentifier $26 Befüllen/Entleeren des Druckspeichers Modus  : Default
- [STOP_BEF_ENT_DRUCKSPEICHER](#job-stop-bef-ent-druckspeicher) - Befüllen und Entleeren des Druckspeichers stoppen KWP2000: $32 StopRoutineByLocalIdentifier $26 Befüllen und Entleeren des Druckspeichers Modus  : Default
- [START_ALLOW_WARM_BTANK](#job-start-allow-warm-btank) - Warmbetankung erlauben KWP2000: $31 StartRoutineByLocalIdentifier $27 Warmbetankung erlauben Modus  : Default
- [START_RESET_THERMOSHOCK](#job-start-reset-thermoshock) - Thermoschockzaehler zuruecksetzen KWP2000: $31 StartRoutineByLocalIdentifier $28 Thermoschockzaehler zuruecksetzen Modus  : Default
- [ANZAHL_THERMOSCHOCKS](#job-anzahl-thermoschocks) - Anzahl der Thermoschocks KWP2000: $21 ReadDataByLocalIdentifier $11 Anzahl der Thermoschocks Modus  : Default
- [STEUERN_PERSIS_DATEN_RUECKSETZEN](#job-steuern-persis-daten-ruecksetzen) - Persistente Daten zuruecksetzen KWP2000: $31 StartRoutineByLocalIdentifier $29 Persistente Daten Ruecksetzen Modus  : Default
- [EM_RESET_VALUES](#job-em-reset-values) - Energie Management Job - Rücksetzen der berechneten Werte KWP2000: $3B WriteDataByLocalIdentifier Modus  : Default
- [EM_BT_THROUGHPUT_SET](#job-em-bt-throughput-set) - Energie Management Job - Setzen des Energiedurchsatzes KWP2000: $3B WriteDataByLocalIdentifier Modus  : Default
- [EM_F_SP_CL](#job-em-f-sp-cl) - Energie Management Job - Betankungsfreigabe KWP2000: $3B WriteDataByLocalIdentifier Modus  : Default
- [STATUS_AUWP_H2_I](#job-status-auwp-h2-i) - Strom der H2-Hilfswasserpumpe KWP2000:  $30 InputOutputControlByLocalIdentifier $01 Index fuer AUWP_H2_I $01 ReportCurrentState Modus  : Default
- [STATUS_AUWP_H2_TEMP](#job-status-auwp-h2-temp) - Temperatur der H2-Hilfswasserpumpe KWP2000:  $30 InputOutputControlByLocalIdentifier $02 Index fuer AUWP_H2_TEMP $01 ReportCurrentState Modus  : Default
- [STATUS_AUWP_H2_VA](#job-status-auwp-h2-va) - Variante der H2-Hilfswasserpumpe KWP2000:  $30 InputOutputControlByLocalIdentifier $03 Index fuer AUWP_H2_VA $01 ReportCurrentState Modus  : Default
- [STATUS_AUWP_H2_VOLT](#job-status-auwp-h2-volt) - Spannung der H2-Hilfswasserpumpe KWP2000:  $30 InputOutputControlByLocalIdentifier $04 Index fuer AUWP_H2_VOLT $01 ReportCurrentState Modus  : Default
- [STATUS_CAL_INFO](#job-status-cal-info) - Kalibrierungsinfo KWP2000:  $30 InputOutputControlByLocalIdentifier $05 Index fuer CAL_INFO $01 ReportCurrentState Modus  : Default
- [STATUS_CER_IDEN](#job-status-cer-iden) - Protokollkennung KWP2000:  $30 InputOutputControlByLocalIdentifier $06 Index fuer CER_IDEN $01 ReportCurrentState Modus  : Default
- [STATUS_DMA_TEMP](#job-status-dma-temp) - Wert des 1ten Temperatursensors KWP2000:  $30 InputOutputControlByLocalIdentifier $07 Index fuer DMA_TEMP $01 ReportCurrentState Modus  : Default
- [STATUS_ERR_FL_LV_SEN](#job-status-err-fl-lv-sen) - Fehler Füllungsgradsensoren_1_2 KWP2000:  $30 InputOutputControlByLocalIdentifier $08 Index fuer ERR_FL_LV_SEN $01 ReportCurrentState Modus  : Default
- [STATUS_ERR_TEMP_SEN](#job-status-err-temp-sen) - Fehler Temperatursensoren KWP2000:  $30 InputOutputControlByLocalIdentifier $09 Index fuer ERR_TEMP_SEN $01 ReportCurrentState Modus  : Default
- [STATUS_GRAD_INFO](#job-status-grad-info) - Gradienteninformation KWP2000:  $30 InputOutputControlByLocalIdentifier $0A Index fuer GRAD_INFO $01 ReportCurrentState Modus  : Default
- [STATUS_HS_BOOT_HYC](#job-status-hs-boot-hyc) - Hy-Sensor_Kofferraum_H2-Konzentration KWP2000:  $30 InputOutputControlByLocalIdentifier $0B Index fuer HS_BOOT_HYC $01 ReportCurrentState Modus  : Default
- [STATUS_HS_BOOT_LL](#job-status-hs-boot-ll) - Hy-Sensor_Kofferraum_Unterer_Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $0C Index fuer HS_BOOT_LL $01 ReportCurrentState Modus  : Default
- [STATUS_HS_BOOT_ST_1](#job-status-hs-boot-st-1) - Hy-Sensor_Kofferraum_Status_1 KWP2000:  $30 InputOutputControlByLocalIdentifier $0D Index fuer HS_BOOT_ST_1 $01 ReportCurrentState Modus  : Default
- [STATUS_HS_BOOT_UL](#job-status-hs-boot-ul) - Hy-Sensor_Kofferraum_Oberer_Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $0E Index fuer HS_BOOT_UL $01 ReportCurrentState Modus  : Default
- [STATUS_HS_ENG_HYC](#job-status-hs-eng-hyc) - Hy-Sensor_Motor_H2-Konzentration KWP2000:  $30 InputOutputControlByLocalIdentifier $0F Index fuer HS_ENG_HYC $01 ReportCurrentState Modus  : Default
- [STATUS_HS_ENG_LL](#job-status-hs-eng-ll) - Hy-Sensor Motor Unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $10 Index fuer HS_ENG_LL $01 ReportCurrentState Modus  : Default
- [STATUS_HS_ENG_ST_1](#job-status-hs-eng-st-1) - Hy-Sensor Motor Status 1 KWP2000:  $30 InputOutputControlByLocalIdentifier $11 Index fuer HS_ENG_ST_1 $01 ReportCurrentState Modus  : Default
- [STATUS_HS_ENG_UL](#job-status-hs-eng-ul) - Hy-Sensor Motor Oberer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $12 Index fuer HS_ENG_UL $01 ReportCurrentState Modus  : Default
- [STATUS_HS_FUTA_CLT_HYC](#job-status-hs-futa-clt-hyc) - Hy-Sensor_TANK_KUPPLUNG_H2-Konzentration KWP2000:  $30 InputOutputControlByLocalIdentifier $13 Index fuer HS_FUTA_CLT_HYC $01 ReportCurrentState Modus  : Default
- [STATUS_HS_FUTA_CLT_LL](#job-status-hs-futa-clt-ll) - Hy-Sensor Tank Kupplung Unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $14 Index fuer HS_FUTA_CLT_LL $01 ReportCurrentState Modus  : Default
- [STATUS_HS_FUTA_CLT_ST_1](#job-status-hs-futa-clt-st-1) - Hy-Sensor Tank Kupplung Status 1 KWP2000:  $30 InputOutputControlByLocalIdentifier $15 Index fuer HS_FUTA_CLT_ST_1 $01 ReportCurrentState Modus  : Default
- [STATUS_HS_FUTA_CLT_UL](#job-status-hs-futa-clt-ul) - Hy-Sensor Tank Kupplung Oberer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $16 Index fuer HS_FUTA_CLT_UL $01 ReportCurrentState Modus  : Default
- [STATUS_HS_PSCMP_HYC](#job-status-hs-pscmp-hyc) - Hy-Sensor Fahrgastzelle H2-Konzentration KWP2000:  $30 InputOutputControlByLocalIdentifier $17 Index fuer HS_PSCMP_HYC $01 ReportCurrentState Modus  : Default
- [STATUS_HS_PSCMP_LL](#job-status-hs-pscmp-ll) - Hy-Sensor Fahrgastzelle UntererGrenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $18 Index fuer HS_PSCMP_LL $01 ReportCurrentState Modus  : Default
- [STATUS_HS_PSCMP_ST_1](#job-status-hs-pscmp-st-1) - Hy-Sensor Fahrgastzelle Status 1 KWP2000:  $30 InputOutputControlByLocalIdentifier $19 Index fuer HS_PSCMP_ST_1 $01 ReportCurrentState Modus  : Default
- [STATUS_HS_PSCMP_UL](#job-status-hs-pscmp-ul) - Hy-Sensor Fahrgastzelle Oberer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $1A Index fuer HS_PSCMP_UL $01 ReportCurrentState Modus  : Default
- [STATUS_HS_SCAP_HYC](#job-status-hs-scap-hyc) - Hy-Sensor Nebensystemkapsel H2-Konzentration KWP2000:  $30 InputOutputControlByLocalIdentifier $1B Index fuer HS_SCAP_HYC $01 ReportCurrentState Modus  : Default
- [STATUS_HS_SCAP_LL](#job-status-hs-scap-ll) - Hy-Sensor Nebensystemkapsel Unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $1C Index fuer HS_SCAP_LL $01 ReportCurrentState Modus  : Default
- [STATUS_HS_SCAP_ST_1](#job-status-hs-scap-st-1) - Hy-Sensor Nebensystemkapsel Status 1 KWP2000:  $30 InputOutputControlByLocalIdentifier $1D Index fuer HS_SCAP_ST_1 $01 ReportCurrentState Modus  : Default
- [STATUS_HS_SCAP_UL](#job-status-hs-scap-ul) - Hy-Sensor Nebensystemkapsel Oberer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $1E Index fuer HS_SCAP_UL $01 ReportCurrentState Modus  : Default
- [STATUS_IN_AMB_P](#job-status-in-amb-p) - Auslesen UMGEBUNG DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $1F Index fuer IN_AMB_P $01 ReportCurrentState Modus  : Default
- [STATUS_IN_AUWP_H2_ERR](#job-status-in-auwp-h2-err) - Eingang Hilfswasserpumpe H2 Fehler KWP2000:  $30 InputOutputControlByLocalIdentifier $21 Index fuer IN_AUWP_H2_ERR $01 ReportCurrentState Modus  : Default
- [STATUS_IN_AUWP_H2_RPM](#job-status-in-auwp-h2-rpm) - EINGANG_HILFSWASSERPUMPE_H2_RPM KWP2000:  $30 InputOutputControlByLocalIdentifier $22 Index fuer IN_AUWP_H2_RPM $01 ReportCurrentState Modus  : Default
- [STATUS_IN_BN](#job-status-in-bn) - Eingang Bordnetz Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $23 Index fuer IN_BN $01 ReportCurrentState Modus  : Default
- [STATUS_IN_BO_P](#job-status-in-bo-p) - BOIL-OFF VALVE DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $24 Index fuer IN_BO_P $01 ReportCurrentState Modus  : Default
- [STATUS_IN_COL_EXH_TEMP](#job-status-in-col-exh-temp) - KÜHLMITTEL AUSLASS TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $25 Index fuer IN_COL_EXH_TEMP $01 ReportCurrentState Modus  : Default
- [STATUS_IN_COL_INL_TEMP](#job-status-in-col-inl-temp) - KÜHLMITTEL EINLASS TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $26 Index fuer IN_COL_INL_TEMP $01 ReportCurrentState Modus  : Default
- [STATUS_IN_COMP_TEMP](#job-status-in-comp-temp) - KOMPRESSOR TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $27 Index fuer IN_COMP_TEMP $01 ReportCurrentState Modus  : Default
- [STATUS_IN_CR](#job-status-in-cr) - CRASH Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $28 Index fuer IN_CR $01 ReportCurrentState Modus  : Default
- [STATUS_IN_FTC_CLO_1](#job-status-in-ftc-clo-1) - TANKDECKEL GESCHLOSSEN Sensor 1 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $29 Index fuer IN_FTC_CLO_1 $01 ReportCurrentState Modus  : Default
- [STATUS_IN_FTC_CLO_2](#job-status-in-ftc-clo-2) - TANKDECKEL GESCHLOSSEN Sensor 2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $2A Index fuer IN_FTC_CLO_2 $01 ReportCurrentState Modus  : Default
- [STATUS_IN_FTC_OPN](#job-status-in-ftc-opn) - TANKDECKEL OFFEN Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $2B Index fuer IN_FTC_OPN $01 ReportCurrentState Modus  : Default
- [STATUS_IN_FUT_CLT_TEMP](#job-status-in-fut-clt-temp) - TANK KUPPLUNG TEMPERATUR KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $20 Index fuer IN_FUT_CLT_TEMP $01 ReportCurrentState Modus  : Default
- [STATUS_IN_FUTA_P_1](#job-status-in-futa-p-1) - TANK DRUCK Sensor 1 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $2C Index fuer IN_FUTA_P_1 $01 ReportCurrentState Modus  : Default
- [STATUS_IN_FUTA_P_2](#job-status-in-futa-p-2) - TANK DRUCK Sensor 2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $2D Index fuer IN_FUTA_P_2 $01 ReportCurrentState Modus  : Default
- [STATUS_IN_GHY_CL_P](#job-status-in-ghy-cl-p) - GASFÖRMIGER-H2 STEUERLEITUNGS DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $2E Index fuer IN_GHY_CL_P $01 ReportCurrentState Modus  : Default
- [STATUS_IN_HEATEX_TEMP](#job-status-in-heatex-temp) - WT TEILSTROM WARM TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $2F Index fuer IN_HEATEX_TEMP $01 ReportCurrentState Modus  : Default
- [STATUS_IN_LHY_CL_P](#job-status-in-lhy-cl-p) - FLÜSSIGER-H2 STEUERLEITUNGS DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $30 Index fuer IN_LHY_CL_P $01 ReportCurrentState Modus  : Default
- [STATUS_IN_MPVA_IN_TEMP](#job-status-in-mpva-in-temp) - WÄRMETAUSCHER TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $31 Index fuer IN_MPVA_IN_TEMP $01 ReportCurrentState Modus  : Default
- [STATUS_IN_MPVA_SP_TEMP](#job-status-in-mpva-sp-temp) - MOTOR ABSPERRVENTIL TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $32 Index fuer IN_MPVA_SP_TEMP $01 ReportCurrentState Modus  : Default
- [STATUS_IN_OFI_PR_1](#job-status-in-ofi-pr-1) - ÜBERLAUFSICHERUNG Sensor 1 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $33 Index fuer IN_OFI_PR_1 $01 ReportCurrentState Modus  : Default
- [STATUS_IN_OFI_PR_2](#job-status-in-ofi-pr-2) - ÜBERLAUFSICHERUNG Sensor 2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $34 Index fuer IN_OFI_PR_2 $01 ReportCurrentState Modus  : Default
- [STATUS_IN_OX_TEMP](#job-status-in-ox-temp) - BOIL OFF MANAGAMENT SYSTEM TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $35 Index fuer IN_OX_TEMP $01 ReportCurrentState Modus  : Default
- [STATUS_IN_PRS_ACCU_P](#job-status-in-prs-accu-p) - PRS DRUCKSPEICHER DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $36 Index fuer IN_PRS_ACCU_P $01 ReportCurrentState Modus  : Default
- [STATUS_IN_STRT_ILK_1](#job-status-in-strt-ilk-1) - STARTER SPERRE Sensor 1 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $37 Index fuer IN_STRT_ILK_1 $01 ReportCurrentState Modus  : Default
- [STATUS_IN_STRT_ILK_2](#job-status-in-strt-ilk-2) - STARTER SPERRE Sensor 2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $38 Index fuer IN_STRT_ILK_2 $01 ReportCurrentState Modus  : Default
- [STATUS_IN_SUPPIPE_P_1](#job-status-in-suppipe-p-1) - TEILSTROMREGELVENTIL DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $39 Index fuer IN_SUPPIPE_P_1 $01 ReportCurrentState Modus  : Default
- [STATUS_IN_SUPPIPE_P_2](#job-status-in-suppipe-p-2) - EINGANG MOTOR ABSPERRVENTIL DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $3A Index fuer IN_SUPPIPE_P_2 $01 ReportCurrentState Modus  : Default
- [STATUS_IN_VENT_TEMP](#job-status-in-vent-temp) - VENTURIDÜSE TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $3B Index fuer IN_VENT_TEMP $01 ReportCurrentState Modus  : Default
- [STATUS_R_BT_CHG](#job-status-r-bt-chg) - Lesen Batterie Zuladung KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $3D Index fuer R_BT_CHG $01 ReportCurrentState Modus  : Default
- [STATUS_R_BT_CHG_PSTP](#job-status-r-bt-chg-pstp) - Lesen Batterie Zuladung Vor-Stop KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $3E Index fuer R_BT_CHG_PSTP $01 ReportCurrentState Modus  : Default
- [STATUS_R_BT_DCHG](#job-status-r-bt-dchg) - Lesen Batterie Entladung KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $3F Index fuer R_BT_DCHG $01 ReportCurrentState Modus  : Default
- [STATUS_R_BT_DCHG_PSTP](#job-status-r-bt-dchg-pstp) - Lesen Batterie Entladung Vor-Stop KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $40 Index fuer R_BT_DCHG_PSTP $01 ReportCurrentState Modus  : Default
- [STATUS_R_IBS_REG_2](#job-status-r-ibs-reg-2) - Lesen IBS_REG_2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $41 Index fuer R_IBS_REG_2 $01 ReportCurrentState Modus  : Default
- [STATUS_R_IBS_REG_4](#job-status-r-ibs-reg-4) - Lesen IBS_REG_4 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $42 Index fuer R_IBS_REG_4 $01 ReportCurrentState Modus  : Default
- [STATUS_R_QVM_CRCS](#job-status-r-qvm-crcs) - Lesen CRC Summe KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $43 Index fuer R_QVM_CRCS $01 ReportCurrentState Modus  : Default
- [STATUS_R_QVM_I](#job-status-r-qvm-i) - LESEN RUHESPANNUNGSMESSUNG STROM KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $44 Index fuer R_QVM_I $01 ReportCurrentState Modus  : Default
- [STATUS_R_QVM_T_1](#job-status-r-qvm-t-1) - LESEN RUHESPANNUNGSMESSUNG ZEIT 1 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $45 Index fuer R_QVM_T_1 $01 ReportCurrentState Modus  : Default
- [STATUS_R_QVM_T_2](#job-status-r-qvm-t-2) - LESEN RUHESPANNUNGSMESSUNG ZEIT 2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $46 Index fuer R_QVM_T_2 $01 ReportCurrentState Modus  : Default
- [STATUS_R_QVM_T_3](#job-status-r-qvm-t-3) - LESEN RUHESPANNUNGSMESSUNG ZEIT 3 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $47 Index fuer R_QVM_T_3 $01 ReportCurrentState Modus  : Default
- [STATUS_R_QVM_T_4](#job-status-r-qvm-t-4) - LESEN RUHESPANNUNGSMESSUNG ZEIT 4 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $48 Index fuer R_QVM_T_4 $01 ReportCurrentState Modus  : Default
- [STATUS_R_QVM_TEMP](#job-status-r-qvm-temp) - LESEN RUHESPANNUNGSMESSUNG TEMPERATUR KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $49 Index fuer R_QVM_TEMP $01 ReportCurrentState Modus  : Default
- [STATUS_R_QVM_U_1](#job-status-r-qvm-u-1) - LESEN RUHESPANNUNGSMESSUNG SPANNUNG 1 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $4A Index fuer R_QVM_U_1 $01 ReportCurrentState Modus  : Default
- [STATUS_R_QVM_U_2](#job-status-r-qvm-u-2) - LESEN RUHESPANNUNGSMESSUNG SPANNUNG 2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $4B Index fuer R_QVM_U_2 $01 ReportCurrentState Modus  : Default
- [STATUS_R_QVM_U_3](#job-status-r-qvm-u-3) - LESEN RUHESPANNUNGSMESSUNG SPANNUNG 3 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $4C Index fuer R_QVM_U_3 $01 ReportCurrentState Modus  : Default
- [STATUS_ST_CLC_N](#job-status-st-clc-n) - STROMSCHLEIFE NEGATIV KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $4D Index fuer ST_CLC_N $01 ReportCurrentState Modus  : Default
- [STATUS_ST_CLC_P](#job-status-st-clc-p) - STROMSCHLEIFE POSITIV KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $4E Index fuer ST_CLC_P $01 ReportCurrentState Modus  : Default
- [STATUS_ST_FUTA_CHO_SW](#job-status-st-futa-cho-sw) - TANK WAHL SCHALTER KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $4F Index fuer ST_FUTA_CHO_SW $01 ReportCurrentState Modus  : Default
- [STATUS_ST_GRB_PPOS](#job-status-st-grb-ppos) - GETRIEBE PARK POSITION KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $50 Index fuer ST_GRB_PPOS $01 ReportCurrentState Modus  : Default
- [STATUS_WGH_LH2](#job-status-wgh-lh2) - H2 Massenwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $51 Index fuer WGH_LH2 $01 ReportCurrentState Modus  : Default
- [STATUS_WGH_LH2_MAX](#job-status-wgh-lh2-max) - Maximal zulässige Füllmasse KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $52 Index fuer WGH_LH2_MAX $01 ReportCurrentState Modus  : Default
- [STATUS_COSP_HY_MAX](#job-status-cosp-hy-max) - Verbrauch Wasserstoff Maximal KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $64 Index fuer COSP_HY_MAX $01 ReportCurrentState Modus  : Default
- [STATUS_DMA_FUTA_P](#job-status-dma-futa-p) - DMA Tank Druck KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $65 Index fuer DMA_FUTA_P $01 ReportCurrentState Modus  : Default
- [STATUS_ERR_CE_OPMO_HY](#job-status-err-ce-opmo-hy) - Fehler CE Betriebsart Wasserstoff KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $66 Index fuer ERR_CE_OPMO_HY $01 ReportCurrentState Modus  : Default
- [STATUS_FLLV_FUTA_HY](#job-status-fllv-futa-hy) - Füllstand Tank Wasserstoff KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $67 Index fuer FLLV_FUTA_HY $01 ReportCurrentState Modus  : Default
- [STATUS_FN_RQ](#job-status-fn-rq) - FUNKTIONS ANFORDERUNG KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $68 Index fuer FN_RQ $01 ReportCurrentState Modus  : Default
- [STATUS_FU_TAR](#job-status-fu-tar) - Kraftstoff Soll KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $69 Index fuer FU_TAR $01 ReportCurrentState Modus  : Default
- [STATUS_FU_TAR_STAPRC](#job-status-fu-tar-staprc) - Kraftstoff Soll Startvorgang KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $6A Index fuer FU_TAR_STAPRC $01 ReportCurrentState Modus  : Default
- [STATUS_ID_FN_REAC_HVEH](#job-status-id-fn-reac-hveh) - ID FUNKTION REAKTION WASSERSTOFF FAHRZEUG KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $6B Index fuer ID_FN_REAC_HVEH $01 ReportCurrentState Modus  : Default
- [STATUS_ID2_CC_MESS_EXT](#job-status-id2-cc-mess-ext) - Identifier Kontrollmeldungsdienst KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $6C Index fuer ID2_CC_MESS_EXT $01 ReportCurrentState Modus  : Default
- [STATUS_NO_CC_MESS_EXT](#job-status-no-cc-mess-ext) - Nummer_Meldung KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $6D Index fuer NO_CC_MESS_EXT $01 ReportCurrentState Modus  : Default
- [STATUS_NO_FRM_CC_MES_EXT](#job-status-no-frm-cc-mes-ext) - Nummer aktueller Frame KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $6E Index fuer NO_FRM_CC_MES_EXT $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_ADD_ABV](#job-status-out-add-abv) - ZUSATZENTLÜFTUNGSVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $6F Index fuer OUT_ADD_ABV_PWM $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_AUWP_DR](#job-status-out-auwp-dr) - ZUSATZWASSERPUMPE NOTLAUF KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $70 Index fuer OUT_AUWP_DR $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_AUWP_H2_RPM](#job-status-out-auwp-h2-rpm) - AUSGANG ZUSATZWASSERPUMPE H2 DREHZAHL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $71 Index fuer OUT_AUWP_H2_RPM $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_BO_CLO_RV](#job-status-out-bo-clo-rv) - BOIL OFF ZU UMSCHALTVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $72 Index fuer OUT_BO_CLO_RV_PWM $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_BO_OPEN_RV](#job-status-out-bo-open-rv) - BOIL OFF AUF UMSCHALTVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $73 Index fuer OUT_BO_OPEN_RV_PWM $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_COMP_REL](#job-status-out-comp-rel) - KOMPRESSOR PRS RELAIS KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $74 Index fuer OUT_COMP_REL $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_ENG_OPM_LED](#job-status-out-eng-opm-led) - MOTOR BETRIEBSMODUS LED KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $75 Index fuer OUT_ENG_OPM_LED $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_ENG_SOV](#job-status-out-eng-sov) - MOTOR ABSPERRVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $76 Index fuer OUT_ENG_SOV_PWM $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_FUTA_CHO_SW_LED](#job-status-out-futa-cho-sw-led) - TANK WAHL SCHALTER LED KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $77 Index fuer OUT_FUTA_CHO_SW_LED $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_FUFF_N](#job-status-out-fuff-n) - TANKKLAPPE N KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $78 Index fuer OUT_FUFF_N_PWM $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_FUFF_P](#job-status-out-fuff-p) - TANKKLAPPE P KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $79 Index fuer OUT_FUFF_P_PWM $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_GHY_COV](#job-status-out-ghy-cov) - GASFÖRMIGER-H2 PRS STEUERVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $7A Index fuer OUT_GHY_COV_PWM $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_HS_BOOT_LL](#job-status-out-hs-boot-ll) - H2 Sensor Kofferraum unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $7B Index fuer OUT_HS_BOOT_LL $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_HS_BOOT_UL](#job-status-out-hs-boot-ul) - H2 Sensor Kofferraum unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $7C Index fuer OUT_HS_BOOT_UL $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_HS_ENG_LL](#job-status-out-hs-eng-ll) - H2 Sensor Motor unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $7D Index fuer OUT_HS_ENG_LL $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_HS_ENG_UL](#job-status-out-hs-eng-ul) - H2 Sensor Motor unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $7E Index fuer OUT_HS_ENG_UL $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_HS_FT_CLT_LL](#job-status-out-hs-ft-clt-ll) - H2 Sensor Tank Kupplung unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $7F Index fuer OUT_HS_FT_CLT_LL $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_HS_FT_CLT_UL](#job-status-out-hs-ft-clt-ul) - H2 Sensor Tank Kupplung unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $80 Index fuer OUT_HS_FT_CLT_UL $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_HS_MSG_CNT](#job-status-out-hs-msg-cnt) - H2 Sensor Nachrichten Zähler KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $81 Index fuer OUT_HS_MSG_CNT $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_HS_PSCMP_LL](#job-status-out-hs-pscmp-ll) - H2 Sensor Fahrgastzelle unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $82 Index fuer OUT_HS_PSCMP_LL $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_HS_PSCMP_UL](#job-status-out-hs-pscmp-ul) - H2 Sensor Fahrgastzelle unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $83 Index fuer OUT_HS_PSCMP_UL $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_HS_SCAP_LL](#job-status-out-hs-scap-ll) - H2 Sensor Nebensystemkapsel unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $84 Index fuer OUT_HS_SCAP_LL $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_HS_SCAP_UL](#job-status-out-hs-scap-ul) - H2 Sensor Nebensystemkapsel unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $85 Index fuer OUT_HS_SCAP_UL $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_LHY_COV](#job-status-out-lhy-cov) - FLÜSSIGER-H2 PRS STEUERVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $86 Index fuer OUT_LHY_COV_PWM $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_ML](#job-status-out-ml) - MOVILINE KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $87 Index fuer OUT_ML $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_MPVA](#job-status-out-mpva) - TEILSTROMREGELVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $88 Index fuer OUT_MPVA_PWM $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_NSK_FL_VA](#job-status-out-nsk-fl-va) - Nebensystemkapsel Spülung PRS Ventil KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $89 Index fuer OUT_NSK_FL_VA_PWM $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_OFI_PR_DIAG](#job-status-out-ofi-pr-diag) - ÜBERFÜLLSICHERUNG DIAGNOSE KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $8A Index fuer OUT_OFI_PR_DIAG $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_OFI_PR_PWR](#job-status-out-ofi-pr-pwr) - ÜBERFÜLLSICHERUNG VERSORGUNG KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $8B Index fuer OUT_OFI_PR_PWR $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_P_ACCU_VA](#job-status-out-p-accu-va) - DRUCKSPEICHER PRS VENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $8C Index fuer OUT_P_ACCU_VA_PWM $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_REG_VA](#job-status-out-reg-va) - REGENERIERUNG PRS VENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $8D Index fuer OUT_REG_VA_PWM $01 ReportCurrentState Modus  : Default
- [STATUS_OUT_STRT_ILK](#job-status-out-strt-ilk) - STARTER SPERRE KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $8E Index fuer OUT_STRT_ILK $01 ReportCurrentState Modus  : Default
- [STATUS_P_FUTA_HY](#job-status-p-futa-hy) - DRUCK TANK INNEN WASSERSTOFF KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $8F Index fuer P_FUTA_HY $01 ReportCurrentState Modus  : Default
- [STATUS_P_SUPPLN_HY](#job-status-p-suppln-hy) - H2 Druck Versorgungsleituung KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $90 Index fuer P_SUPPLN_HY $01 ReportCurrentState Modus  : Default
- [STATUS_QU_FRM_CC_MES_EXT](#job-status-qu-frm-cc-mes-ext) - Gesamt Zahl Frames KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $91 Index fuer QU_FRM_CC_MES_EXT $01 ReportCurrentState Modus  : Default
- [STATUS_RNG_HY](#job-status-rng-hy) - Reichweite Wasserstoff KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $92 Index fuer RNG_HY $01 ReportCurrentState Modus  : Default
- [STATUS_RQ_FU_TAR](#job-status-rq-fu-tar) - ANFORDERUNG_KRAFTSTOFF_SOLL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $93 Index fuer RQ_FU_TAR $01 ReportCurrentState Modus  : Default
- [STATUS_ST_CC_DSP_FRQ](#job-status-st-cc-dsp-frq) - STATUS BLINKEN TAKT CHECKCONTROL MELDUNG ERWEITERT KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $94 Index fuer ST_CC_DSP_FRQ $01 ReportCurrentState Modus  : Default
- [STATUS_ST_CC_MESS_EXT](#job-status-st-cc-mess-ext) - Meldung_setzen_ruecksetzen KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $95 Index fuer ST_CC_MESS_EXT $01 ReportCurrentState Modus  : Default
- [STATUS_ST_FLLV_FUTA_SPAR_HY](#job-status-st-fllv-futa-spar-hy) - Status_Füllstand_Tank_Reserve_Wasserstoff KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $96 Index fuer ST_FLLV_FUTA_SPAR_HY $01 ReportCurrentState Modus  : Default
- [STATUS_ST_OPMO_HY](#job-status-st-opmo-hy) - STATUS_BETRIEBSART_WASSERSTOFF KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $97 Index fuer ST_OPMO_HY $01 ReportCurrentState Modus  : Default
- [STATUS_ST_OPMOCHG_CE](#job-status-st-opmochg-ce) - Status Betriebsartenwechsel CE KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $98 Index fuer ST_OPMOCHG_CE $01 ReportCurrentState Modus  : Default
- [STATUS_ST_RFG_HY](#job-status-st-rfg-hy) - Status_Nachtanken_Wasserstoff KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $99 Index fuer ST_RFG_HY $01 ReportCurrentState Modus  : Default
- [STATUS_STARTFREIGABE_CE](#job-status-startfreigabe-ce) - Meldung Motorstart Verhindern KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $9A Index fuer STARTFREIGABE_CE $01 ReportCurrentState Modus  : Default
- [STATUS_TEMP_EX_TA](#job-status-temp-ex-ta) - TEMPERATUR AUßENDRUCK KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $9B Index fuer TEMP_EX_TA $01 ReportCurrentState Modus  : Default
- [STATUS_TRANF_CC_MESS_EXT](#job-status-tranf-cc-mess-ext) - Übetragungsintervall KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $9C Index fuer TRANF_CC_MESS_EXT $01 ReportCurrentState Modus  : Default
- [STATUS_TSTMP](#job-status-tstmp) - ZEITSPANNE KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $9D Index fuer TSTMP $01 ReportCurrentState Modus  : Default
- [STATUS_UTDT_CC_MESS](#job-status-utdt-cc-mess) - NUTZDATEN_CHECK-CONTROL_MELDUNG KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $9E Index fuer UTDT_CC_MESS $01 ReportCurrentState Modus  : Default
- [STATUS_VEH_CO](#job-status-veh-co) - FAHRZEUGZUSTAND KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $9F Index fuer VEH_CO $01 ReportCurrentState Modus  : Default

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

<a id="job-status-bo-pres"></a>
### STATUS_BO_PRES

Lesen Ansprechdruck Boil-Off KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wpda-les"></a>
### STATUS_WPDA_LES

Lesen Wärmeleistung PDA KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-wpbo-les"></a>
### STATUS_WPBO_LES

Lesen Wärmeleistung PBO KWP2000: $21 ReadDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-dicht-test"></a>
### START_DICHT_TEST

Dichtigkeitstest anfangen KWP2000: $31 StartRoutineByLocalIdentifier $20 StartDichtigkeitsTest Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-dicht-test"></a>
### STOP_DICHT_TEST

Dichtigkeitstest aufhören KWP2000: $32 StopRoutineByLocalIdentifier $20 StopDichtigkeitsTest Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-rout-res-dicht-test"></a>
### ROUT_RES_DICHT_TEST

Ergebnisse des Dichtigkeitstests abfragen KWP2000: $33 RequestRoutineResultsByLocalIdentifier $20 DichtigkeitsTest Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| DICHT_TEST_STATUS | unsigned int | Status des Dichtigkeitstest |
| DICHT_TEST_STATUS_TEXT | string | text |
| LEAK_RATE_1 | real | LEAK_RATE_GHY_VA_R in mbar * Liter pro Sekunde Normal Bereich 0 bis 0,01 bar * Liter pro Sekunde Ungültig Wert = 0,01 (Werte größer als 0,01 bar * Liter pro Sekunde werden auf 0,01 bar * Liter pro Sekunde begrenzt) |
| LEAK_RATE_1_ALT_NEU | unsigned int | Status |
| LEAK_RATE_1_ALT_NEU_TEXT | string | text |
| LEAK_RATE_2 | real | LEAK_RATE_ENG_SOV_1_R in bar * Liter pro Sekunde Normal Bereich 0 bis 0,01 bar * Liter pro Sekunde Ungültig Wert = 0,01 (Werte größer als 0,01 bar * Liter pro Sekunde werden auf 0,01 bar * Liter pro Sekunde begrenzt) |
| LEAK_RATE_2_ALT_NEU | unsigned int | Status |
| LEAK_RATE_2_ALT_NEU_TEXT | string | text |
| LEAK_RATE_3 | real | LEAK_RATE_ENG_SOV_2_R in mbar * Liter pro Sekunde Normal Bereich 0 bis 0,01 bar * Liter pro Sekunde Ungültig Wert = 0,01 (Werte größer als 0,01 bar * Liter pro Sekunde werden auf 0,01 bar * Liter pro Sekunde begrenzt) |
| LEAK_RATE_3_ALT_NEU | unsigned int | Status |
| LEAK_RATE_3_ALT_NEU_TEXT | string | text |
| LEAK_RATE_4 | real | LEAK_RATE_P_CTRL_1_R in mbar * Liter pro Sekunde Normal Bereich 0 bis 0,01 bar * Liter pro Sekunde Ungültig Wert = 0,01 (Werte größer als 0,01 bar * Liter pro Sekunde werden auf 0,01 bar * Liter pro Sekunde begrenzt) |
| LEAK_RATE_4_ALT_NEU | unsigned int | Status |
| LEAK_RATE_4_ALT_NEU_TEXT | string | text |
| LEAK_RATE_5 | real | LEAK_RATE_P_CTRL_2_R in mbar * Liter pro Sekunde Normal Bereich 0 bis 0,01 bar * Liter pro Sekunde Ungültig Wert = 0,01 (Werte größer als 0,01 bar * Liter pro Sekunde werden auf 0,01 bar * Liter pro Sekunde begrenzt) |
| LEAK_RATE_5_ALT_NEU | unsigned int | Status |
| LEAK_RATE_5_ALT_NEU_TEXT | string | text |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-anzahl-letzten-dicht-test"></a>
### ANZAHL_LETZTEN_DICHT_TEST

Anzahl der Tage seit dem letzten Dichtigkeitstest KWP2000: $21 ReadDataByLocalIdentifier $10 AnzahlTagenLetzenDichtTest Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ANZAHL_TAGEN | unsigned int | Normal Bereich 0 bis 65535 Tage I.O. Bereich 0 bis 99 Tage |

<a id="job-start-vorlauf-entspannen"></a>
### START_VORLAUF_ENTSPANNEN

H2-Vorlaufleitung entspannen KWP2000: $31 StartRoutineByLocalIdentifier $21 StartVorlaufEntspannung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-zugang-tank"></a>
### START_ZUGANG_TANK

Zugang zum Tank bzw. zur Entnahmeleitung KWP2000: $31 StartRoutineByLocalIdentifier $22 StartZugangTankEntnahme Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODUS | int | 1 (Modus A: Zugang zum Tank) 2 (Modus B: Zugang zur Entnahmeleitung) 3 (Modus C: Zugang zum Tank und Entnahmeleitung) Legt fest in welcher Zugangsmodus gestartet werden soll |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-zugang-tank-entnahme"></a>
### STOP_ZUGANG_TANK_ENTNAHME

ZugangTank aufhören KWP2000: $32 StopRoutineByLocalIdentifier $22 Stop ZugangTankt Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-gaswarn-test"></a>
### START_GASWARN_TEST

Test der Gaswarn-LED's starten KWP2000: $31 StartRoutineByLocalIdentifier $23 Gas Warn Test Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-boil-off-test"></a>
### START_BOIL_OFF_TEST

Boil Off Test beim nächsten H2-Betrieb auslösen KWP2000: $31 StartRoutineByLocalIdentifier $24 Boil Off Test Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-kalibr-mass-test"></a>
### START_KALIBR_MASS_TEST

Kalibrierung der Füllmassenerfassung starten KWP2000: $31 StartRoutineByLocalIdentifier $25 Kalibrierung Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-bef-ent-druckspeicher"></a>
### START_BEF_ENT_DRUCKSPEICHER

Befüllen oder Entleeren des Druckspeichers starten KWP2000: $31 StartRoutineByLocalIdentifier $26 Befüllen/Entleeren des Druckspeichers Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODUS | int | 1 Druckspeicher befüllen 2 Druckspeicher entleeren Druckspeicher befüllen oder entleeren |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-stop-bef-ent-druckspeicher"></a>
### STOP_BEF_ENT_DRUCKSPEICHER

Befüllen und Entleeren des Druckspeichers stoppen KWP2000: $32 StopRoutineByLocalIdentifier $26 Befüllen und Entleeren des Druckspeichers Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-allow-warm-btank"></a>
### START_ALLOW_WARM_BTANK

Warmbetankung erlauben KWP2000: $31 StartRoutineByLocalIdentifier $27 Warmbetankung erlauben Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-start-reset-thermoshock"></a>
### START_RESET_THERMOSHOCK

Thermoschockzaehler zuruecksetzen KWP2000: $31 StartRoutineByLocalIdentifier $28 Thermoschockzaehler zuruecksetzen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-anzahl-thermoschocks"></a>
### ANZAHL_THERMOSCHOCKS

Anzahl der Thermoschocks KWP2000: $21 ReadDataByLocalIdentifier $11 Anzahl der Thermoschocks Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| ANZAHL_THERMOSCHOCKS | unsigned int | Normalbereich 0 bis 65535 Thermoschocks |

<a id="job-steuern-persis-daten-ruecksetzen"></a>
### STEUERN_PERSIS_DATEN_RUECKSETZEN

Persistente Daten zuruecksetzen KWP2000: $31 StartRoutineByLocalIdentifier $29 Persistente Daten Ruecksetzen Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-em-reset-values"></a>
### EM_RESET_VALUES

Energie Management Job - Rücksetzen der berechneten Werte KWP2000: $3B WriteDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-em-bt-throughput-set"></a>
### EM_BT_THROUGHPUT_SET

Energie Management Job - Setzen des Energiedurchsatzes KWP2000: $3B WriteDataByLocalIdentifier Modus  : Default

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| DURCHSATZ | int | Bereich: 0-65535 bzw. 0x0000-0xFFFF Wert von Energiedurchsatz |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-em-f-sp-cl"></a>
### EM_F_SP_CL

Energie Management Job - Betankungsfreigabe KWP2000: $3B WriteDataByLocalIdentifier Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-status-auwp-h2-i"></a>
### STATUS_AUWP_H2_I

Strom der H2-Hilfswasserpumpe KWP2000:  $30 InputOutputControlByLocalIdentifier $01 Index fuer AUWP_H2_I $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_AUWP_H2_I_CD_WERT | real | AUWP_H2_I konditionierter Wert in Ampere Normal Bereich 0 bis 255 A |
| STAT_AUWP_H2_I_CD_EINH | string | Einheit von AUWP_H2_I_CD |

<a id="job-status-auwp-h2-temp"></a>
### STATUS_AUWP_H2_TEMP

Temperatur der H2-Hilfswasserpumpe KWP2000:  $30 InputOutputControlByLocalIdentifier $02 Index fuer AUWP_H2_TEMP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_AUWP_H2_TEMP_CD_WERT | real | AUWP_H2_TEMP konditionierter Wert in °C Normal Bereich 0 bis 255 °C |
| STAT_AUWP_H2_TEMP_CD_EINH | string | Einheit des konditionierten Werts von AUWP_H2_TEMP |

<a id="job-status-auwp-h2-va"></a>
### STATUS_AUWP_H2_VA

Variante der H2-Hilfswasserpumpe KWP2000:  $30 InputOutputControlByLocalIdentifier $03 Index fuer AUWP_H2_VA $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_AUWP_H2_VA_CD_WERT | int | AUWP_H2_VA konditionierter Wert |

<a id="job-status-auwp-h2-volt"></a>
### STATUS_AUWP_H2_VOLT

Spannung der H2-Hilfswasserpumpe KWP2000:  $30 InputOutputControlByLocalIdentifier $04 Index fuer AUWP_H2_VOLT $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_AUWP_H2_VOLT_CD_WERT | real | AUWP_H2_VOLT konditionierter Wert in Volt Normal Bereich 0 bis 25,5 V |
| STAT_AUWP_H2_VOLT_CD_EINH | string | Einheit des konditionierten Werts von AUWP_H2_VOLT_CD |

<a id="job-status-cal-info"></a>
### STATUS_CAL_INFO

Kalibrierungsinfo KWP2000:  $30 InputOutputControlByLocalIdentifier $05 Index fuer CAL_INFO $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_CAL_INFO_CD_NR | int | CAL_INFO konditionierter Wert 0h Kalibrierung erfolgreich abgeschlossen 1h Kalibrierung im Gange 2h Kalibrierung nie erfolgt 3h Kalibrierung fehlgeschlagen, Vorbedingung Temperatur verletzt 4h Kalibrierung fehlgeschlagen, Vorbedingung Druck verletzt 5h Kalibrierung fehlgeschlagen, Messwert außerhalb Gültigkeitsbereich 7h ungültig |
| STAT_CAL_INFO_TEXT | string | Beschreibung CAL_INFO konditionierter Wert |

<a id="job-status-cer-iden"></a>
### STATUS_CER_IDEN

Protokollkennung KWP2000:  $30 InputOutputControlByLocalIdentifier $06 Index fuer CER_IDEN $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_CER_IDEN_CD_WERT | int | CER_IDEN konditionierter Wert |

<a id="job-status-dma-temp"></a>
### STATUS_DMA_TEMP

Wert des 1ten Temperatursensors KWP2000:  $30 InputOutputControlByLocalIdentifier $07 Index fuer DMA_TEMP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_DMA_TEMP_V_WERT | real | DMA_TEMP validierter Wert in °C Normal Bereich -273 bis 227 °C |
| STAT_DMA_TEMP_V_EINH | string | Einheit von DMA_TEMP_V |

<a id="job-status-err-fl-lv-sen"></a>
### STATUS_ERR_FL_LV_SEN

Fehler Füllungsgradsensoren_1_2 KWP2000:  $30 InputOutputControlByLocalIdentifier $08 Index fuer ERR_FL_LV_SEN $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ERR_FL_LV_SEN_CD_NR | int | ERR_FL_LV_SEN konditionierter Wert Bits 0 und 1 0...kein Fehler Sensor 1 1...Sensor 1 Fehlt 2...Kurzschluss Sensor 1 3...fehlerhafter Sensor 1 Bits 2 und 3: 0...Kein Fehler Sensor 2 1...Sensor 2 Fehlt 2...Kurzschluss Sensor 2 3...fehlerhafter Sensor 2 Bits 4 und 5: 0...Vorhalt 1...Vorhalt 2...Vorhalt 3...UNGÜLTIG" |
| STAT_ERR_FL_LV_SEN_CD_TEXT | string | Beschreibung ERR_FL_LV_SEN konditionierter Wert |

<a id="job-status-err-temp-sen"></a>
### STATUS_ERR_TEMP_SEN

Fehler Temperatursensoren KWP2000:  $30 InputOutputControlByLocalIdentifier $09 Index fuer ERR_TEMP_SEN $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ERR_TEMP_SEN_CD_NR | int | ERR_TEMP_SEN konditionierter Wert Bits 0 und 1 0...kein Fehler Sensor 1 1...Sensor 1 Fehlt 2...Kurzschluss Sensor 1 3...fehlerhafter Sensor 1 Bits 2 und 3 0...kein Fehler Sensor 2 1...Sensor 2 Fehlt 2...Kurzschluss Sensor 2 3...fehlerhafter Sensor 2 |
| STAT_ERR_TEMP_SEN_CD_TEXT | string | Beschreibung ERR_TEMP_SEN konditionierter Wert |

<a id="job-status-grad-info"></a>
### STATUS_GRAD_INFO

Gradienteninformation KWP2000:  $30 InputOutputControlByLocalIdentifier $0A Index fuer GRAD_INFO $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_GRAD_INFO_CD_NR | int | GRAD_INFO konditionierter Wert 0h..Gradientenfilter initialisiert, Gradient nicht verletzt 1h..Gradientenfilter noch nicht initialisiert 2h..Gradientenfilter initialisiert, Gradient nach unten verletzt 4h..Gradientenfilter initialisiert, Gradient nach oben verletzt 7h..ungültig |
| STAT_GRAD_INFO_CD_TEXT | string | Beschreibung GRAD_INFO konditionierter Wert |

<a id="job-status-hs-boot-hyc"></a>
### STATUS_HS_BOOT_HYC

Hy-Sensor_Kofferraum_H2-Konzentration KWP2000:  $30 InputOutputControlByLocalIdentifier $0B Index fuer HS_BOOT_HYC $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_BOOT_HYC_V_WERT | real | HS_BOOT_HYC validierter Wert Normal Bereich von 0% bis 4,4% |
| STAT_HS_BOOT_HYC_V_EINH | string | Einheit von HS_BOOT_HYC_V |

<a id="job-status-hs-boot-ll"></a>
### STATUS_HS_BOOT_LL

Hy-Sensor_Kofferraum_Unterer_Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $0C Index fuer HS_BOOT_LL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_BOOT_LL_CD_NR | int | HS_BOOT_LL konditionierter Wert 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_HS_BOOT_LL_CD_TEXT | string | Beschreibung HS_BOOT_LL konditionierter Wert |

<a id="job-status-hs-boot-st-1"></a>
### STATUS_HS_BOOT_ST_1

Hy-Sensor_Kofferraum_Status_1 KWP2000:  $30 InputOutputControlByLocalIdentifier $0D Index fuer HS_BOOT_ST_1 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_BOOT_ST_1_CD_NR | int | HS_BOOT_ST_1 konditionierter Wert 0...NC 1...Minor Error 2...Minor functional error 3...Fatal functional error |
| STAT_HS_BOOT_ST_1_CD_TEXT | string | Beschreibung HS_BOOT_ST_1 konditionierter Wert |

<a id="job-status-hs-boot-ul"></a>
### STATUS_HS_BOOT_UL

Hy-Sensor_Kofferraum_Oberer_Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $0E Index fuer HS_BOOT_UL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_BOOT_UL_CD_NR | int | HS_BOOT_UL konditionierter Wert 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_HS_BOOT_UL_CD_TEXT | string | Beschreibung HS_BOOT_UL_CD konditionierter Wert |

<a id="job-status-hs-eng-hyc"></a>
### STATUS_HS_ENG_HYC

Hy-Sensor_Motor_H2-Konzentration KWP2000:  $30 InputOutputControlByLocalIdentifier $0F Index fuer HS_ENG_HYC $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_ENG_HYC_V_WERT | real | HS_ENG_HYC validierter Wert Normal Bereich von 0% bis 4,4% |
| STAT_HS_ENG_HYC_V_EINH | string | Einheit von HS_ENG_HYC_V |

<a id="job-status-hs-eng-ll"></a>
### STATUS_HS_ENG_LL

Hy-Sensor Motor Unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $10 Index fuer HS_ENG_LL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_ENG_LL_CD_NR | int | HS_ENG_LL konditionierter Wert 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_HS_ENG_LL_CD_TEXT | string | Beschreibung HS_ENG_LL konditionierter Wert |

<a id="job-status-hs-eng-st-1"></a>
### STATUS_HS_ENG_ST_1

Hy-Sensor Motor Status 1 KWP2000:  $30 InputOutputControlByLocalIdentifier $11 Index fuer HS_ENG_ST_1 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_ENG_ST_1_CD_NR | int | HS_ENG_ST_1 konditionierter Wert 0...NC 1...Minor Error 2...Minor functional error 3...Fatal functional error |
| STAT_HS_ENG_ST_1_CD_TEXT | string | Beschreibung HS_ENG_ST_1 konditionierter Wert |

<a id="job-status-hs-eng-ul"></a>
### STATUS_HS_ENG_UL

Hy-Sensor Motor Oberer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $12 Index fuer HS_ENG_UL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_ENG_UL_CD_NR | int | HS_ENG_UL konditionierter Wert 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_HS_ENG_UL_CD_TEXT | string | Beschreibung HS_ENG_UL_CD konditionierter Wert |

<a id="job-status-hs-futa-clt-hyc"></a>
### STATUS_HS_FUTA_CLT_HYC

Hy-Sensor_TANK_KUPPLUNG_H2-Konzentration KWP2000:  $30 InputOutputControlByLocalIdentifier $13 Index fuer HS_FUTA_CLT_HYC $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_FUTA_CLT_HYC_V_WERT | real | HS_FUTA_CLT_HYC validierter Wert Normal Bereich von 0% bis 4,4% |
| STAT_HS_FUTA_CLT_HYC_V_EINH | string | Einheit von HS_FUTA_CLT_HYC_V |

<a id="job-status-hs-futa-clt-ll"></a>
### STATUS_HS_FUTA_CLT_LL

Hy-Sensor Tank Kupplung Unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $14 Index fuer HS_FUTA_CLT_LL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_FUTA_CLT_LL_CD_NR | int | HS_FUTA_CLT_LL konditionierter Wert 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_HS_FUTA_CLT_LL_CD_TEXT | string | Beschreibung HS_FUTA_CLT_LL konditionierter Wert |

<a id="job-status-hs-futa-clt-st-1"></a>
### STATUS_HS_FUTA_CLT_ST_1

Hy-Sensor Tank Kupplung Status 1 KWP2000:  $30 InputOutputControlByLocalIdentifier $15 Index fuer HS_FUTA_CLT_ST_1 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_FUTA_CLT_ST_1_CD_NR | int | HS_FUTA_CLT_ST_1 konditionierter Wert 0...NC 1...Minor Error 2...Minor functional error 3...Fatal functional error |
| STAT_HS_FUTA_CLT_ST_1_CD_TEXT | string | Beschreibung HS_FUTA_CLT_ST_1 konditionierter Wert |

<a id="job-status-hs-futa-clt-ul"></a>
### STATUS_HS_FUTA_CLT_UL

Hy-Sensor Tank Kupplung Oberer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $16 Index fuer HS_FUTA_CLT_UL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_FUTA_CLT_UL_CD_NR | int | HS_FUTA_CLT_UL konditionierter Wert 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_HS_FUTA_CLT_UL_CD_TEXT | string | Beschreibung HS_FUTA_CLT_UL_CD konditionierter Wert |

<a id="job-status-hs-pscmp-hyc"></a>
### STATUS_HS_PSCMP_HYC

Hy-Sensor Fahrgastzelle H2-Konzentration KWP2000:  $30 InputOutputControlByLocalIdentifier $17 Index fuer HS_PSCMP_HYC $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_PSCMP_HYC_V_WERT | real | HS_PSCMP_HYC validierter Wert Normal Bereich von 0% bis 4,4% |
| STAT_HS_PSCMP_HYC_V_EINH | string | Einheit von HS_PSCMP_HYC_V |

<a id="job-status-hs-pscmp-ll"></a>
### STATUS_HS_PSCMP_LL

Hy-Sensor Fahrgastzelle UntererGrenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $18 Index fuer HS_PSCMP_LL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_PSCMP_LL_CD_NR | int | HS_PSCMP_LL konditionierter Wert 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_HS_PSCMP_LL_CD_TEXT | string | Beschreibung HS_PSCMP_LL konditionierter Wert |

<a id="job-status-hs-pscmp-st-1"></a>
### STATUS_HS_PSCMP_ST_1

Hy-Sensor Fahrgastzelle Status 1 KWP2000:  $30 InputOutputControlByLocalIdentifier $19 Index fuer HS_PSCMP_ST_1 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_PSCMP_ST_1_CD_NR | int | HS_PSCMP_ST_1 konditionierter Wert 0...NC 1...Minor Error 2...Minor functional error 3...Fatal functional error |
| STAT_HS_PSCMP_ST_1_CD_TEXT | string | Beschreibung HS_PSCMP_ST_1 konditionierter Wert |

<a id="job-status-hs-pscmp-ul"></a>
### STATUS_HS_PSCMP_UL

Hy-Sensor Fahrgastzelle Oberer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $1A Index fuer HS_PSCMP_UL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_PSCMP_UL_CD_NR | int | HS_PSCMP_UL konditionierter Wert 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_HS_PSCMP_UL_CD_TEXT | string | Beschreibung HS_PSCMP_UL_CD konditionierter Wert |

<a id="job-status-hs-scap-hyc"></a>
### STATUS_HS_SCAP_HYC

Hy-Sensor Nebensystemkapsel H2-Konzentration KWP2000:  $30 InputOutputControlByLocalIdentifier $1B Index fuer HS_SCAP_HYC $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_SCAP_HYC_V_WERT | real | HS_SCAP_HYC validierter Wert Normal Bereich von 0% bis 4,4% |
| STAT_HS_SCAP_HYC_V_EINH | string | Einheit von HS_SCAP_HYC_V |

<a id="job-status-hs-scap-ll"></a>
### STATUS_HS_SCAP_LL

Hy-Sensor Nebensystemkapsel Unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $1C Index fuer HS_SCAP_LL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_SCAP_LL_CD_NR | int | HS_SCAP_LL konditionierter Wert 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_HS_SCAP_LL_CD_TEXT | string | Beschreibung HS_SCAP_LL konditionierter Wert |

<a id="job-status-hs-scap-st-1"></a>
### STATUS_HS_SCAP_ST_1

Hy-Sensor Nebensystemkapsel Status 1 KWP2000:  $30 InputOutputControlByLocalIdentifier $1D Index fuer HS_SCAP_ST_1 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_SCAP_ST_1_CD_NR | int | HS_SCAP_ST_1 konditionierter Wert 0...NC 1...Minor Error 2...Minor functional error 3...Fatal functional error |
| STAT_HS_SCAP_ST_1_CD_TEXT | string | Beschreibung HS_SCAP_ST_1 konditionierter Wert |

<a id="job-status-hs-scap-ul"></a>
### STATUS_HS_SCAP_UL

Hy-Sensor Nebensystemkapsel Oberer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier $1E Index fuer HS_SCAP_UL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_HS_SCAP_UL_CD_NR | int | HS_SCAP_UL konditionierter Wert 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_HS_SCAP_UL_CD_TEXT | string | Beschreibung HS_SCAP_UL_CD konditionierter Wert |

<a id="job-status-in-amb-p"></a>
### STATUS_IN_AMB_P

Auslesen UMGEBUNG DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $1F Index fuer IN_AMB_P $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_AMB_P_CD_WERT | real | IN_AMB_P konditionierter Wert Normal Bereich 0,47 bis 1,25 Bar |
| STAT_IN_AMB_P_CD_EINH | string | Einheit des konditionierten Wert von IN_AMB_P |

<a id="job-status-in-auwp-h2-err"></a>
### STATUS_IN_AUWP_H2_ERR

Eingang Hilfswasserpumpe H2 Fehler KWP2000:  $30 InputOutputControlByLocalIdentifier $21 Index fuer IN_AUWP_H2_ERR $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_AUWP_H2_ERR_CD_NR | int | IN_AUWP_H2_ERR konditionierter Wert Bit 0: Nicht belegt Bit 1: Keine Drehzahlüberwachung Bit 2: wird geschrieben (siehe Bus-Ausgangssignale) Bit 3: Übertemperatur Bit 4: Blockierng Bit 5: Trockenlauf Bit 6: Falsche Spannung Bit 7: Deblockierung aktiv |
| STAT_IN_AUWP_H2_ERR_CD_TEXT | string | Beschreibung IN_AUWP_H2_ERR konditionierter Wert |

<a id="job-status-in-auwp-h2-rpm"></a>
### STATUS_IN_AUWP_H2_RPM

EINGANG_HILFSWASSERPUMPE_H2_RPM KWP2000:  $30 InputOutputControlByLocalIdentifier $22 Index fuer IN_AUWP_H2_RPM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_AUWP_H2_RPM_CD_NR | int | IN_AUWP_H2_RPM konditionierter Wert 0: Stopp und Rücksetzen Fehler 1..19: Betrieb im unüberwachten Modus (18..400 U/min) 20..250: Geregelter Betrieb im überwachten Modus (400..4500 U/min) 251: Nachlauf aktivieren (5 min, 1200 U/min) 252: Nachlauf aktivieren (2,5 min, 1200 U/min) 253: Nachlauf aktivieren (5 min, 700 U/min) 254: Nachlauf aktivieren (2,5 min, 700 U/min) 255: Nachlauf deaktivieren |
| STAT_IN_AUWP_H2_RPM_CD_TEXT | string | Beschreibung IN_AUWP_H2_RPM konditionierter Wert |

<a id="job-status-in-bn"></a>
### STATUS_IN_BN

Eingang Bordnetz Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $23 Index fuer IN_BN $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_BN_CD_WERT | real | IN_BN konditionierter Wert Normal Bereich -1 bis 21 Volt Ungültig Wert = 64,535 |
| STAT_IN_BN_CD_EINH | string | Einheit des konditionierten Wert von IN_BN |

<a id="job-status-in-bo-p"></a>
### STATUS_IN_BO_P

BOIL-OFF VALVE DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $24 Index fuer IN_BO_P $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_BO_P_CD_WERT | real | IN_BO_P konditionierter Wert Normal Bereich 0,47 bis 8 Bar Ungültig Wert = 65,535 |
| STAT_IN_BO_P_CD_EINH | string | Einheit des konditionierten Werts von IN_BO_P |

<a id="job-status-in-col-exh-temp"></a>
### STATUS_IN_COL_EXH_TEMP

KÜHLMITTEL AUSLASS TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $25 Index fuer IN_COL_EXH_TEMP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_COL_EXH_TEMP_CD_WERT | real | IN_COL_EXH_TEMP konditionierter Wert Normal Bereich -40 bis +120 °C Ungültig Wert = 615,35 |
| STAT_IN_COL_EXH_TEMP_CD_EINH | string | Einheit des konditionierten Werts von IN_COL_EXH_TEMP |

<a id="job-status-in-col-inl-temp"></a>
### STATUS_IN_COL_INL_TEMP

KÜHLMITTEL EINLASS TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $26 Index fuer IN_COL_INL_TEMP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_COL_INL_TEMP_CD_WERT | real | IN_COL_INL_TEMP konditionierter Wert Normal Bereich -40 bis +120 °C Ungültig Wert = 615,35 |
| STAT_IN_COL_INL_TEMP_CD_EINH | string | Einheit des konditionierten Werts von IN_COL_INL_TEMP |

<a id="job-status-in-comp-temp"></a>
### STATUS_IN_COMP_TEMP

KOMPRESSOR TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $27 Index fuer IN_COMP_TEMP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_COMP_TEMP_CD_WERT | real | IN_COMP_TEMP konditionierter Wert Normal Bereich -40 bis +140 °C Ungültig Wert = 615,35 |
| STAT_IN_COMP_TEMP_CD_EINH | string | Einheit des konditionierten Werts von IN_COMP_TEMP |

<a id="job-status-in-cr"></a>
### STATUS_IN_CR

CRASH Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $28 Index fuer IN_CR $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_CR_CD_WERT | real | IN_CR konditionierter Wert Normal Bereich -1 bis 21 Volt Ungültig Wert = 64,535 |
| STAT_IN_CR_CD_EINH | string | Einheit des konditionierten Werts von IN_CR |

<a id="job-status-in-ftc-clo-1"></a>
### STATUS_IN_FTC_CLO_1

TANKDECKEL GESCHLOSSEN Sensor 1 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $29 Index fuer IN_FTC_CLO_1 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_FTC_CLO_1_CD_WERT | real | IN_FTC_CLO_1 konditionierter Wert Normal Bereich 1 bis 18 mA Ungültig Wert = 65,535 |
| STAT_IN_FTC_CLO_1_CD_EINH | string | Einheit des konditionierten Werts von IN_FTC_CLO_1 |
| STAT_IN_FTC_CLO_1_GESCHLOSSEN | int | 1 = Kontakt geschlossen (wenn &lt; 10mA), 0 = Kontakt offen (wenn &gt;= 10mA) |

<a id="job-status-in-ftc-clo-2"></a>
### STATUS_IN_FTC_CLO_2

TANKDECKEL GESCHLOSSEN Sensor 2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $2A Index fuer IN_FTC_CLO_2 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_FTC_CLO_2_CD_WERT | real | IN_FTC_CLO_2 konditionierter Wert Normal Bereich 1 bis 18 mA Ungültig Wert = 65,535 |
| STAT_IN_FTC_CLO_2_CD_EINH | string | Einheit des konditionierten Werts von IN_FTC_CLO_2 |
| STAT_IN_FTC_CLO_2_GESCHLOSSEN | int | 1 = Kontakt geschlossen (wenn &lt; 10mA), 0 = Kontakt offen (wenn &gt;= 10mA) |

<a id="job-status-in-ftc-opn"></a>
### STATUS_IN_FTC_OPN

TANKDECKEL OFFEN Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $2B Index fuer IN_FTC_OPN $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_FTC_OPN_CD_WERT | real | IN_FTC_OPN konditionierter Wert Normal Bereich 1 bis 18 mA Ungültig Wert = 65,535 |
| STAT_IN_FTC_OPN_CD_EINH | string | Einheit des konditionierten Werts von IN_FTC_OPN |
| STAT_IN_FTC_OPN_GESCHLOSSEN | int | 1 = Kontakt geschlossen (wenn &lt; 10mA), 0 = Kontakt offen (wenn &gt;= 10mA) |

<a id="job-status-in-fut-clt-temp"></a>
### STATUS_IN_FUT_CLT_TEMP

TANK KUPPLUNG TEMPERATUR KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $20 Index fuer IN_FUT_CLT_TEMP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_FUT_CLT_TEMP_CD_WERT | real | IN_FTC_OPN konditionierter Wert Normal Bereich -60°C bis 120°C Ungültig Wert = 595,53 |
| STAT_IN_FUT_CLT_TEMP_CD_EINH | string | Einheit des konditionierten Werts von IN_FUT_CLT_TEMP |

<a id="job-status-in-futa-p-1"></a>
### STATUS_IN_FUTA_P_1

TANK DRUCK Sensor 1 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $2C Index fuer IN_FUTA_P_1 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_FUTA_P_1_CD_WERT | real | IN_FUTA_P_1 konditionierter Wert Normal Bereich 0,47 bis 8 Bar Ungültig Wert = 65,535 |
| STAT_IN_FUTA_P_1_CD_EINH | string | Einheit des konditionierten Werts von IN_FUTA_P_1 |

<a id="job-status-in-futa-p-2"></a>
### STATUS_IN_FUTA_P_2

TANK DRUCK Sensor 2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $2D Index fuer IN_FUTA_P_2 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_FUTA_P_2_CD_WERT | real | IN_FUTA_P_2 konditionierter Wert Normal Bereich 0,47 bis 8 Bar Ungültig Wert = 65,535 |
| STAT_IN_FUTA_P_2_CD_EINH | string | Einheit des konditionierten Werts von IN_FUTA_P_2 |

<a id="job-status-in-ghy-cl-p"></a>
### STATUS_IN_GHY_CL_P

GASFÖRMIGER-H2 STEUERLEITUNGS DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $2E Index fuer IN_GHY_CL_P $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_GHY_CL_P_CD_WERT | real | IN_GHY_CL_P konditionierter Wert Normal Bereich 0,47 bis 22 Bar Ungültig Wert = 65,535 |
| STAT_IN_GHY_CL_P_CD_EINH | string | Einheit des konditionierten Werts von IN_GHY_CL_P Normal Bereich 0 bis 21 Bar |

<a id="job-status-in-heatex-temp"></a>
### STATUS_IN_HEATEX_TEMP

WT TEILSTROM WARM TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $2F Index fuer IN_HEATEX_TEMP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_HEATEX_TEMP_CD_WERT | real | IN_HEATEX_TEMP konditionierter Wert Normal Bereich -55 bis +120 °C Ungültig Wert = 600,35 |
| STAT_IN_HEATEX_TEMP_CD_EINH | string | Einheit des konditionierten Werts von IN_HEATEX_TEMP |

<a id="job-status-in-lhy-cl-p"></a>
### STATUS_IN_LHY_CL_P

FLÜSSIGER-H2 STEUERLEITUNGS DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $30 Index fuer IN_LHY_CL_P $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_LHY_CL_P_CD_WERT | real | IN_LHY_CL_P konditionierter Wert Normal Bereich 0,47 bis 22 Bar Ungültig Wert = 65,535 |
| STAT_IN_LHY_CL_P_CD_EINH | string | Einheit von IN_LHY_CL_P konditionierten Wert in Bar |

<a id="job-status-in-mpva-in-temp"></a>
### STATUS_IN_MPVA_IN_TEMP

WÄRMETAUSCHER TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $31 Index fuer IN_MPVA_IN_TEMP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_MPVA_IN_TEMP_CD_WERT | real | IN_MPVA_IN_TEMP konditionierter Wert Normal Bereich -55 bis +120 °C Ungültig Wert = 600,35 |
| STAT_IN_MPVA_IN_TEMP_CD_EINH | string | Einheit des konditionierten Werts von IN_MPVA_IN_TEMP |

<a id="job-status-in-mpva-sp-temp"></a>
### STATUS_IN_MPVA_SP_TEMP

MOTOR ABSPERRVENTIL TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $32 Index fuer IN_MPVA_SP_TEMP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_MPVA_SP_TEMP_CD_WERT | real | IN_MPVA_SP_TEMP konditionierter Wert Normal Bereich -55 bis +120 °C Ungültig Wert = 600,35 |
| STAT_IN_MPVA_SP_TEMP_CD_EINH | string | Einheit des konditionierten Werts von IN_MPVA_SP_TEMP |

<a id="job-status-in-ofi-pr-1"></a>
### STATUS_IN_OFI_PR_1

ÜBERLAUFSICHERUNG Sensor 1 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $33 Index fuer IN_OFI_PR_1 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_OFI_PR_1_CD_WERT | real | IN_OFI_PR_1 konditionierter Wert Normal Bereich 397 bis 480 Ohm und 4094 bis 4431 Ohm Ungültig Wert = 6553,5 |
| STAT_IN_OFI_PR_1_CD_EINH | string | Einheit des konditionierten Werts von IN_OFI_PR_1 |
| STAT_IN_OFI_PR_1_NR | int | 1=nicht überfüllt, 2=überfüllt |
| STAT_IN_OFI_PR_1_TEXT | string | nicht überfüllt, überfüllt |

<a id="job-status-in-ofi-pr-2"></a>
### STATUS_IN_OFI_PR_2

ÜBERLAUFSICHERUNG Sensor 2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $34 Index fuer IN_OFI_PR_2 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_OFI_PR_2_CD_WERT | real | IN_OFI_PR_2 konditionierter Wert Normal Bereich 397 bis 480 Ohm und 4094 bis 4431 Ohm Ungültig Wert = 6553,5 |
| STAT_IN_OFI_PR_2_CD_EINH | string | Einheit des konditionierten Werts von IN_OFI_PR_2 |
| STAT_IN_OFI_PR_2_NR | int | 1=nicht überfüllt, 2=überfüllt |
| STAT_IN_OFI_PR_2_TEXT | string | nicht überfüllt, überfüllt |

<a id="job-status-in-ox-temp"></a>
### STATUS_IN_OX_TEMP

BOIL OFF MANAGAMENT SYSTEM TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $35 Index fuer IN_OX_TEMP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_OX_TEMP_CD_WERT | real | IN_OX_TEMP konditionierter Wert Normal Bereich -40 bis 787,6 °C Ungültig Wert = 1270,7 |
| STAT_IN_OX_TEMP_CD_EINH | string | Einheit des konditionierten Werts von IN_OX_TEMP |

<a id="job-status-in-prs-accu-p"></a>
### STATUS_IN_PRS_ACCU_P

PRS DRUCKSPEICHER DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $36 Index fuer IN_PRS_ACCU_P $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_PRS_ACCU_P_CD_WERT | real | IN_PRS_ACCU_P konditionierter Wert Normal Bereich 0,47 bis 22 Bar Ungültig Wert = 65,535 |
| STAT_IN_PRS_ACCU_P_CD_EINH | string | Einheit des konditionierten Werts von IN_PRS_ACCU_P |

<a id="job-status-in-strt-ilk-1"></a>
### STATUS_IN_STRT_ILK_1

STARTER SPERRE Sensor 1 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $37 Index fuer IN_STRT_ILK_1 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_STRT_ILK_1_CD_WERT | real | IN_STRT_ILK_1 konditionierter Wert Normal Bereich -0,25 bis 5,25 Volt Ungültig Wert = 65,285 |
| STAT_IN_STRT_ILK_1_CD_EINH | string | Einheit des konditionierten Werts von IN_STRT_ILK_1 |

<a id="job-status-in-strt-ilk-2"></a>
### STATUS_IN_STRT_ILK_2

STARTER SPERRE Sensor 2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $38 Index fuer IN_STRT_ILK_2 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_STRT_ILK_2_CD_WERT | real | IN_STRT_ILK_2 konditionierter Wert Normal Bereich -0,25 bis 5,25 Volt Ungültig Wert = 65,285 |
| STAT_IN_STRT_ILK_2_CD_EINH | string | Einheit des konditionierten Werts von IN_STRT_ILK_2 |

<a id="job-status-in-suppipe-p-1"></a>
### STATUS_IN_SUPPIPE_P_1

TEILSTROMREGELVENTIL DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $39 Index fuer IN_SUPPIPE_P_1 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_SUPPIPE_P_1_CD_WERT | real | IN_SUPPIPE_P_1 konditionierter Wert Normal Bereich 0,47 bis 8 Bar Ungültig Wert = 65,535 |
| STAT_IN_SUPPIPE_P_1_CD_EINH | string | Einheit des konditionierten Werts von IN_SUPPIPE_P_1 |

<a id="job-status-in-suppipe-p-2"></a>
### STATUS_IN_SUPPIPE_P_2

EINGANG MOTOR ABSPERRVENTIL DRUCK Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $3A Index fuer IN_SUPPIPE_P_2 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_SUPPIPE_P_2_CD_WERT | real | IN_SUPPIPE_P_2 konditionierter Wert Normal Bereich 0,47 bis 8 Bar Ungültig Wert = 65,535 |
| STAT_IN_SUPPIPE_P_2_CD_EINH | string | Einheit des konditionierten Werts von IN_SUPPIPE_P_2 |

<a id="job-status-in-vent-temp"></a>
### STATUS_IN_VENT_TEMP

VENTURIDÜSE TEMPERATUR Sensor KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $3B Index fuer IN_VENT_TEMP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_IN_VENT_TEMP_CD_WERT | real | IN_VENT_TEMP konditionierter Wert Normal Bereich -40 bis 787,6 °C Ungültig Wert = 1310,7 |
| STAT_IN_VENT_TEMP_CD_EINH | string | Einheit des konditionierten Werts von IN_VENT_TEMP |

<a id="job-status-r-bt-chg"></a>
### STATUS_R_BT_CHG

Lesen Batterie Zuladung KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $3D Index fuer R_BT_CHG $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_BT_CHG_CD_WERT | real | R_BT_CHG konditionierter Wert |
| STAT_R_BT_CHG_CD_EINH | string | Einheit des konditionierten Werts von R_BT_CHG_CD |

<a id="job-status-r-bt-chg-pstp"></a>
### STATUS_R_BT_CHG_PSTP

Lesen Batterie Zuladung Vor-Stop KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $3E Index fuer R_BT_CHG_PSTP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_BT_CHG_PSTP_CD_WERT | real | R_BT_CHG_PSTP konditionierter Wert |
| STAT_R_BT_CHG_PSTP_CD_EINH | string | Einheit des konditionierten Werts von R_BT_CHG_PSTP_CD |

<a id="job-status-r-bt-dchg"></a>
### STATUS_R_BT_DCHG

Lesen Batterie Entladung KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $3F Index fuer R_BT_DCHG $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_BT_DCHG_CD_WERT | real | R_BT_DCHG konditionierter Wert |
| STAT_R_BT_DCHG_CD_EINH | string | Einheit des konditionierten Werts von R_BT_DCHG_CD |

<a id="job-status-r-bt-dchg-pstp"></a>
### STATUS_R_BT_DCHG_PSTP

Lesen Batterie Entladung Vor-Stop KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $40 Index fuer R_BT_DCHG_PSTP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_BT_DCHG_PSTP_CD_WERT | real | R_BT_DCHG_PSTP konditionierter Wert |
| STAT_R_BT_DCHG_PSTP_CD_EINH | string | Einheit des konditionierten Werts von R_BT_DCHG_PSTP_CD |

<a id="job-status-r-ibs-reg-2"></a>
### STATUS_R_IBS_REG_2

Lesen IBS_REG_2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $41 Index fuer R_IBS_REG_2 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_IBS_REG_2_CD_WERT | real | R_IBS_REG_2 konditionierter Wert |

<a id="job-status-r-ibs-reg-4"></a>
### STATUS_R_IBS_REG_4

Lesen IBS_REG_4 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $42 Index fuer R_IBS_REG_4 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_IBS_REG_4_CD_WERT | real | R_IBS_REG_4 konditionierter Wert |

<a id="job-status-r-qvm-crcs"></a>
### STATUS_R_QVM_CRCS

Lesen CRC Summe KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $43 Index fuer R_QVM_CRCS $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_QVM_CRCS_CD_WERT | real | R_QVM_CRCS konditionierter Wert |

<a id="job-status-r-qvm-i"></a>
### STATUS_R_QVM_I

LESEN RUHESPANNUNGSMESSUNG STROM KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $44 Index fuer R_QVM_I $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_QVM_I_CD_WERT | real | R_QVM_I konditionierter Wert |
| STAT_R_QVM_I_CD_EINH | string | Einheit des konditionierten Werts von R_QVM_I_CD |

<a id="job-status-r-qvm-t-1"></a>
### STATUS_R_QVM_T_1

LESEN RUHESPANNUNGSMESSUNG ZEIT 1 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $45 Index fuer R_QVM_T_1 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_QVM_T_1_CD_WERT | real | R_QVM_T_1 konditionierter Wert |
| STAT_R_QVM_T_1_CD_EINH | string | Einheit des konditionierten Werts von R_QVM_T_1_CD |

<a id="job-status-r-qvm-t-2"></a>
### STATUS_R_QVM_T_2

LESEN RUHESPANNUNGSMESSUNG ZEIT 2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $46 Index fuer R_QVM_T_2 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_QVM_T_2_CD_WERT | real | R_QVM_T_2 konditionierter Wert |
| STAT_R_QVM_T_2_CD_EINH | string | Einheit des konditionierten Werts von R_QVM_T_2_CD |

<a id="job-status-r-qvm-t-3"></a>
### STATUS_R_QVM_T_3

LESEN RUHESPANNUNGSMESSUNG ZEIT 3 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $47 Index fuer R_QVM_T_3 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_QVM_T_3_CD_WERT | real | R_QVM_T_3 konditionierter Wert |
| STAT_R_QVM_T_3_CD_EINH | string | Einheit des konditionierten Werts von R_QVM_T_3_CD |

<a id="job-status-r-qvm-t-4"></a>
### STATUS_R_QVM_T_4

LESEN RUHESPANNUNGSMESSUNG ZEIT 4 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $48 Index fuer R_QVM_T_4 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_QVM_T_4_CD_WERT | real | R_QVM_T_4 konditionierter Wert |
| STAT_R_QVM_T_4_CD_EINH | string | Einheit des konditionierten Werts von R_QVM_T_4_CD |

<a id="job-status-r-qvm-temp"></a>
### STATUS_R_QVM_TEMP

LESEN RUHESPANNUNGSMESSUNG TEMPERATUR KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $49 Index fuer R_QVM_TEMP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_QVM_TEMP_CD_WERT | real | R_QVM_TEMP konditionierter Wert |
| STAT_R_QVM_TEMP_CD_EINH | string | Einheit des konditionierten Werts von R_QVM_TEMP |

<a id="job-status-r-qvm-u-1"></a>
### STATUS_R_QVM_U_1

LESEN RUHESPANNUNGSMESSUNG SPANNUNG 1 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $4A Index fuer R_QVM_U_1 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_QVM_U_1_CD_WERT | real | R_QVM_U_1 konditionierter Wert |
| STAT_R_QVM_U_1_CD_EINH | string | Einheit des konditionierten Werts von R_QVM_U_1_CD |

<a id="job-status-r-qvm-u-2"></a>
### STATUS_R_QVM_U_2

LESEN RUHESPANNUNGSMESSUNG SPANNUNG 2 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $4B Index fuer R_QVM_U_2 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_QVM_U_2_CD_WERT | real | R_QVM_U_2 konditionierter Wert |
| STAT_R_QVM_U_2_CD_EINH | string | Einheit des konditionierten Werts von R_QVM_U_2_CD |

<a id="job-status-r-qvm-u-3"></a>
### STATUS_R_QVM_U_3

LESEN RUHESPANNUNGSMESSUNG SPANNUNG 3 KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $4C Index fuer R_QVM_U_3 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_R_QVM_U_3_CD_WERT | real | R_QVM_U_3 konditionierter Wert |
| STAT_R_QVM_U_3_CD_EINH | string | Einheit des konditionierten Werts von R_QVM_U_3_CD |

<a id="job-status-st-clc-n"></a>
### STATUS_ST_CLC_N

STROMSCHLEIFE NEGATIV KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $4D Index fuer ST_CLC_N $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ST_CLC_N_GESCHLOSSEN | unsigned int | Status von ST_CLC_N |

<a id="job-status-st-clc-p"></a>
### STATUS_ST_CLC_P

STROMSCHLEIFE POSITIV KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $4E Index fuer ST_CLC_P $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ST_CLC_P_GESCHLOSSEN | unsigned int | Status von ST_CLC_P |

<a id="job-status-st-futa-cho-sw"></a>
### STATUS_ST_FUTA_CHO_SW

TANK WAHL SCHALTER KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $4F Index fuer ST_FUTA_CHO_SW $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ST_FUTA_CHO_SW | unsigned int | Status von ST_FUTA_CHO_SW |

<a id="job-status-st-grb-ppos"></a>
### STATUS_ST_GRB_PPOS

GETRIEBE PARK POSITION KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $50 Index fuer ST_GRB_PPOS $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ST_GRB_PPOS | unsigned int | Status von ST_GRB_PPOS |

<a id="job-status-wgh-lh2"></a>
### STATUS_WGH_LH2

H2 Massenwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $51 Index fuer WGH_LH2 $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_WGH_LH2_V_WERT | real | WGH_LH2 validierter Wert |
| STAT_WGH_LH2_V_EINH | string | Einheit des validierten Werts von WGH_LH2_V |

<a id="job-status-wgh-lh2-max"></a>
### STATUS_WGH_LH2_MAX

Maximal zulässige Füllmasse KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $52 Index fuer WGH_LH2_MAX $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_WGH_LH2_MAX_CD_WERT | real | WGH_LH2_MAX konditionierter Wert |
| STAT_WGH_LH2_MAX_CD_EINH | string | Einheit des konditionierten Werts von WGH_LH2_MAX_CD |

<a id="job-status-cosp-hy-max"></a>
### STATUS_COSP_HY_MAX

Verbrauch Wasserstoff Maximal KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $64 Index fuer COSP_HY_MAX $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_COSP_HY_MAX_WERT | real | COSP_HY_MAX in kg/h Normal Bereich 0 bis 200 kg/h Ungültig Wert 8191,875 |
| STAT_COSP_HY_MAX_EINH | string | Einheit von COSP_HY_MAX |

<a id="job-status-dma-futa-p"></a>
### STATUS_DMA_FUTA_P

DMA Tank Druck KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $65 Index fuer DMA_FUTA_P $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_DMA_FUTA_P_WERT | real | DMA_FUTA_P Normal Bereich 0 bis 8 Bar |
| STAT_DMA_FUTA_P_EINH | string | Einheit von DMA_FUTA_P |

<a id="job-status-err-ce-opmo-hy"></a>
### STATUS_ERR_CE_OPMO_HY

Fehler CE Betriebsart Wasserstoff KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $66 Index fuer ERR_CE_OPMO_HY $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ERR_CE_OPMO_HY_NR | int | 0..kein Fehler 1-12..leichte Fehler 13..schwerer Fehler / kein H2-Betrieb 14..schwerer Fehler / kein Start 15..nicht erlaubt |
| STAT_ERR_CE_OPMO_HY_TEXT | string | Beschreibung ERR_CE_OPMO_HY |

<a id="job-status-fllv-futa-hy"></a>
### STATUS_FLLV_FUTA_HY

Füllstand Tank Wasserstoff KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $67 Index fuer FLLV_FUTA_HY $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_FLLV_FUTA_HY_WERT | real | FLLV_FUTA_HY Normal Bereich 0 bis 100 % |
| STAT_FLLV_FUTA_HY_EINH | string | Einheit von FLLV_FUTA_HY |

<a id="job-status-fn-rq"></a>
### STATUS_FN_RQ

FUNKTIONS ANFORDERUNG KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $68 Index fuer FN_RQ $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_FN_RQ_NR | int | 0..zyklische Messung soll durchgeführt werden 1..Reset-Aufforderung 2..Power-Off-Aufforderung 4..Kalibrierung durchführen |
| STAT_FN_RQ_TEXT | string | Beschreibung FN_RQ |

<a id="job-status-fu-tar"></a>
### STATUS_FU_TAR

Kraftstoff Soll KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $69 Index fuer FU_TAR $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_FU_TAR_NR | int | 1..Benzin 2..Wasserstoff 3..Signal ungültig |
| STAT_FU_TAR_TEXT | string | Beschreibung FU_TAR |

<a id="job-status-fu-tar-staprc"></a>
### STATUS_FU_TAR_STAPRC

Kraftstoff Soll Startvorgang KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $6A Index fuer FU_TAR_STAPRC $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_FU_TAR_STAPRC_NR | int | 1..Benzin 2..Wasserstoff 3..Signal ungültig |
| STAT_FU_TAR_STAPRC_TEXT | string | Beschreibung FU_TAR_STAPRC |

<a id="job-status-id-fn-reac-hveh"></a>
### STATUS_ID_FN_REAC_HVEH

ID FUNKTION REAKTION WASSERSTOFF FAHRZEUG KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $6B Index fuer ID_FN_REAC_HVEH $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ID_FN_REAC_HVEH_NR | int | 0..Keine Aktion 40..Zentralverriegelung entsichern 41..Zentralverriegelung sichern 50..EWS aktivieren 51..EWS deaktivieren 60..EMF ?? 61..EMF ?? 100..Fenster FAT öffnen 101..Fenster BFT öffnen 102..Fenster FATH öffnen 103..Fenster BFTH öffnen 104..HK öffnen 105..SHD/MDS öffnen 130..Alle Klappen öffnen 131..Alle Fenster öffnen 150..Fenster FAT schließen 151..Fenster BFT schließen 152..Fenster FATH schließen 153..Fenster BFTH schließen 154..HK schließen 155..SHD/MDS schließen 180..Alle Klappen schließen 181..Alle Fenster schließen 200..Fenster FAT in Lüfterspalt 201..Fenster BFT in Lüfterspalt 202..Fenster FATH in Lüfterspalt 203..Fenster BFTH in Lüfterspalt 204..HK in Lüfterspalt (Dichtung) 205..SHD/MDS in Lüfterspalt 230..Alle Klappen in Lüfterspalt 231..Alle Fenster in Lüfterspalt 250..FAT "Zwischenposition" 251..BFT "Zwischenposition" 252..FATH "Zwischenposition" 253..BFTH "Zwischenposition" 254..HK "Zwischenposition" 255..SHD/MDS "Zwischenposition" 280..Alle Klappen "Zwischenposition" 281..Alle Fenster "Zwischenposition" 300..Klima-Klappen öffnen 301..Klima-Klappen schließen 65535..Signal ungültig |
| STAT_ID_FN_REAC_HVEH_TEXT | string | Beschreibung ID_FN_REAC_HVEH |

<a id="job-status-id2-cc-mess-ext"></a>
### STATUS_ID2_CC_MESS_EXT

Identifier Kontrollmeldungsdienst KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $6C Index fuer ID2_CC_MESS_EXT $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ID2_CC_MESS_EXT_NR | int | 64..Standart CC-Meldung 65..Erweiterte CC-Meldung |
| STAT_ID2_CC_MESS_EXT_TEXT | string | Beschreibung ID2_CC_MESS_EXT |

<a id="job-status-no-cc-mess-ext"></a>
### STATUS_NO_CC_MESS_EXT

Nummer_Meldung KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $6D Index fuer NO_CC_MESS_EXT $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_NO_CC_MESS_EXT_NR | int | 39..Motor Überhitzt 188..H2 Betrieb nicht möglich - Benzinstart aktivieren 189..H2 Tankklappe offen. Voraussichtliche Tankzeit ca. ... 310..Tanken nicht möglich 312..H2-Betrieb nicht möglich 313..Benzin-Betrieb nicht möglich 315..H2-System erheblich gestört 316..H2-Tankklappe offen 319..Tankvorbereitungen treffen! 329..Batteriefehler 359..H2-Betrieb zurzeit nicht möglich! Bitte tanken. 360..H2 tanken zurzeit nicht möglich! Nachtanken nur bei Tank ... 361..Wasserstoffsystem gestört 362..Nicht in geschlossene Räume fahren |
| STAT_NO_CC_MESS_EXT_TEXT | string | Beschreibung NO_CC_MESS_EXT |

<a id="job-status-no-frm-cc-mes-ext"></a>
### STATUS_NO_FRM_CC_MES_EXT

Nummer aktueller Frame KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $6E Index fuer NO_FRM_CC_MES_EXT $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_NO_FRM_CC_MES_EXT_WERT | int | NO_FRM_CC_MES_EXT wert |

<a id="job-status-out-add-abv"></a>
### STATUS_OUT_ADD_ABV

ZUSATZENTLÜFTUNGSVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $6F Index fuer OUT_ADD_ABV_PWM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_ADD_ABV_PWM_WERT | real | OUT_ADD_ABV_PWM Wert |
| STAT_OUT_ADD_ABV_PWM_EINH | string | Einheit von OUT_ADD_ABV_PWM |

<a id="job-status-out-auwp-dr"></a>
### STATUS_OUT_AUWP_DR

ZUSATZWASSERPUMPE NOTLAUF KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $70 Index fuer OUT_AUWP_DR $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_AUWP_DR | int | Status von OUT_AUWP_DR |

<a id="job-status-out-auwp-h2-rpm"></a>
### STATUS_OUT_AUWP_H2_RPM

AUSGANG ZUSATZWASSERPUMPE H2 DREHZAHL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $71 Index fuer OUT_AUWP_H2_RPM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_AUWP_H2_RPM_NR | int | 0: Stopp und Rücksetzen Fehler 1..19: Betrieb im unüberwachten Modus (18..400 U/min) 20..250: Geregelter Betrieb im überwachten Modus (400..4500 U/min) 251: Nachlauf aktivieren (5 min, 1200 U/min) 252: Nachlauf aktivieren (2,5 min, 1200 U/min) 253: Nachlauf aktivieren (5 min, 700 U/min) 254: Nachlauf aktivieren (2,5 min, 700 U/min) 255: Nachlauf deaktivieren |
| STAT_OUT_AUWP_H2_RPM_TEXT | string | Beschreibung OUT_AUWP_H2_RPM konditionierter Wert |

<a id="job-status-out-bo-clo-rv"></a>
### STATUS_OUT_BO_CLO_RV

BOIL OFF ZU UMSCHALTVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $72 Index fuer OUT_BO_CLO_RV_PWM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_BO_CLO_RV_PWM_WERT | real | OUT_BO_CLO_RV_PWM Wert |
| STAT_OUT_BO_CLO_RV_PWM_EINH | string | Einheit von OUT_BO_CLO_RV_PWM |

<a id="job-status-out-bo-open-rv"></a>
### STATUS_OUT_BO_OPEN_RV

BOIL OFF AUF UMSCHALTVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $73 Index fuer OUT_BO_OPEN_RV_PWM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_BO_OPEN_RV_PWM_WERT | real | OUT_BO_OPEN_RV_PWM Wert |
| STAT_OUT_BO_OPEN_RV_PWM_EINH | string | Einheit von OUT_BO_OPEN_RV_PWM |

<a id="job-status-out-comp-rel"></a>
### STATUS_OUT_COMP_REL

KOMPRESSOR PRS RELAIS KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $74 Index fuer OUT_COMP_REL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_COMP_REL_AKTIV | int | Status von OUT_COMP_REL |

<a id="job-status-out-eng-opm-led"></a>
### STATUS_OUT_ENG_OPM_LED

MOTOR BETRIEBSMODUS LED KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $75 Index fuer OUT_ENG_OPM_LED $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_ENG_OPM_LED_KENNZEICHNUNG | int | Status von OUT_ENG_OPM_LED |

<a id="job-status-out-eng-sov"></a>
### STATUS_OUT_ENG_SOV

MOTOR ABSPERRVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $76 Index fuer OUT_ENG_SOV_PWM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_ENG_SOV_PWM_WERT | real | OUT_ENG_SOV_PWM Wert |
| STAT_OUT_ENG_SOV_PWM_EINH | string | Einheit von OUT_ENG_SOV_PWM |

<a id="job-status-out-futa-cho-sw-led"></a>
### STATUS_OUT_FUTA_CHO_SW_LED

TANK WAHL SCHALTER LED KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $77 Index fuer OUT_FUTA_CHO_SW_LED $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_FUTA_CHO_SW_LED_KENNZEICHNUNG | int | Status von OUT_FUTA_CHO_SW_LED |

<a id="job-status-out-fuff-n"></a>
### STATUS_OUT_FUFF_N

TANKKLAPPE N KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $78 Index fuer OUT_FUFF_N_PWM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_FUFF_N_PWM_WERT | real | OUT_FUFF_N_PWM Wert |
| STAT_OUT_FUFF_N_PWM_EINH | string | Einheit von OUT_FUFF_N_PWM |

<a id="job-status-out-fuff-p"></a>
### STATUS_OUT_FUFF_P

TANKKLAPPE P KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $79 Index fuer OUT_FUFF_P_PWM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_FUFF_P_PWM_WERT | real | OUT_FUFF_P_PWM Wert |
| STAT_OUT_FUFF_P_PWM_EINH | string | Einheit von OUT_FUFF_P_PWM |

<a id="job-status-out-ghy-cov"></a>
### STATUS_OUT_GHY_COV

GASFÖRMIGER-H2 PRS STEUERVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $7A Index fuer OUT_GHY_COV_PWM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_GHY_COV_PWM_WERT | real | OUT_GHY_COV_PWM Wert |
| STAT_OUT_GHY_COV_PWM_EINH | string | Einheit von OUT_GHY_COV_PWM |

<a id="job-status-out-hs-boot-ll"></a>
### STATUS_OUT_HS_BOOT_LL

H2 Sensor Kofferraum unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $7B Index fuer OUT_HS_BOOT_LL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_HS_BOOT_LL_NR | int | OUT_HS_BOOT_LL 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_OUT_HS_BOOT_LL_TEXT | string | Beschreibung von OUT_HS_BOOT_LL |

<a id="job-status-out-hs-boot-ul"></a>
### STATUS_OUT_HS_BOOT_UL

H2 Sensor Kofferraum unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $7C Index fuer OUT_HS_BOOT_UL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_HS_BOOT_UL_NR | int | OUT_HS_BOOT_UL 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_OUT_HS_BOOT_UL_TEXT | string | Beschreibung von OUT_HS_BOOT_UL |

<a id="job-status-out-hs-eng-ll"></a>
### STATUS_OUT_HS_ENG_LL

H2 Sensor Motor unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $7D Index fuer OUT_HS_ENG_LL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_HS_ENG_LL_NR | int | OUT_HS_ENG_LL 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_OUT_HS_ENG_LL_TEXT | string | Beschreibung von OUT_HS_ENG_LL |

<a id="job-status-out-hs-eng-ul"></a>
### STATUS_OUT_HS_ENG_UL

H2 Sensor Motor unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $7E Index fuer OUT_HS_ENG_UL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_HS_ENG_UL_NR | int | OUT_HS_ENG_UL 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_OUT_HS_ENG_UL_TEXT | string | Beschreibung von OUT_HS_ENG_UL |

<a id="job-status-out-hs-ft-clt-ll"></a>
### STATUS_OUT_HS_FT_CLT_LL

H2 Sensor Tank Kupplung unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $7F Index fuer OUT_HS_FT_CLT_LL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_HS_FT_CLT_LL_NR | int | OUT_HS_FT_CLT_LL 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_OUT_HS_FT_CLT_LL_TEXT | string | Beschreibung von OUT_HS_FT_CLT_LL |

<a id="job-status-out-hs-ft-clt-ul"></a>
### STATUS_OUT_HS_FT_CLT_UL

H2 Sensor Tank Kupplung unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $80 Index fuer OUT_HS_FT_CLT_UL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_HS_FT_CLT_UL_NR | int | OUT_HS_FT_CLT_UL 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_OUT_HS_FT_CLT_UL_TEXT | string | Beschreibung von OUT_HS_FT_CLT_UL |

<a id="job-status-out-hs-msg-cnt"></a>
### STATUS_OUT_HS_MSG_CNT

H2 Sensor Nachrichten Zähler KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $81 Index fuer OUT_HS_MSG_CNT $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_HS_MSG_CNT_WERT | int | OUT_HS_MSG_CNT Wert |

<a id="job-status-out-hs-pscmp-ll"></a>
### STATUS_OUT_HS_PSCMP_LL

H2 Sensor Fahrgastzelle unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $82 Index fuer OUT_HS_PSCMP_LL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_HS_PSCMP_LL_NR | int | OUT_HS_PSCMP_LL Wert 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_OUT_HS_PSCMP_LL_TEXT | string | Beschreibung von OUT_HS_PSCMP_LL |

<a id="job-status-out-hs-pscmp-ul"></a>
### STATUS_OUT_HS_PSCMP_UL

H2 Sensor Fahrgastzelle unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $83 Index fuer OUT_HS_PSCMP_UL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_HS_PSCMP_UL_NR | int | OUT_HS_PSCMP_UL Wert 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_OUT_HS_PSCMP_UL_TEXT | string | Beschreibung von OUT_HS_PSCMP_UL |

<a id="job-status-out-hs-scap-ll"></a>
### STATUS_OUT_HS_SCAP_LL

H2 Sensor Nebensystemkapsel unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $84 Index fuer OUT_HS_SCAP_LL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_HS_SCAP_LL_NR | int | OUT_HS_SCAP_LL 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_OUT_HS_SCAP_LL_TEXT | string | Beschreibung von OUT_HS_SCAP_LL |

<a id="job-status-out-hs-scap-ul"></a>
### STATUS_OUT_HS_SCAP_UL

H2 Sensor Nebensystemkapsel unterer Grenzwert KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $85 Index fuer OUT_HS_SCAP_UL $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_HS_SCAP_UL_NR | int | OUT_HS_SCAP_UL 0..0,0% 1..0,25% 2..0,5% 3..1,0% 4..1,5% 5..2,0% 6..4,4% 7..ungültig |
| STAT_OUT_HS_SCAP_UL_TEXT | string | Beschreibung von OUT_HS_SCAP_UL |

<a id="job-status-out-lhy-cov"></a>
### STATUS_OUT_LHY_COV

FLÜSSIGER-H2 PRS STEUERVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $86 Index fuer OUT_LHY_COV_PWM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_LHY_COV_PWM_WERT | real | OUT_LHY_COV_PWM Wert |
| STAT_OUT_LHY_COV_PWM_EINH | string | Einheit von OUT_LHY_COV_PWM |

<a id="job-status-out-ml"></a>
### STATUS_OUT_ML

MOVILINE KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $87 Index fuer OUT_ML $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_ML_AKTIV | int | Status von OUT_ML |

<a id="job-status-out-mpva"></a>
### STATUS_OUT_MPVA

TEILSTROMREGELVENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $88 Index fuer OUT_MPVA_PWM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_MPVA_PWM_WERT | real | OUT_MPVA_PWM Wert |
| STAT_OUT_MPVA_PWM_EINH | string | Einheit von OUT_MPVA_PWM |

<a id="job-status-out-nsk-fl-va"></a>
### STATUS_OUT_NSK_FL_VA

Nebensystemkapsel Spülung PRS Ventil KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $89 Index fuer OUT_NSK_FL_VA_PWM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_NSK_FL_VA_PWM_WERT | real | OUT_NSK_FL_VA_PWM Wert |
| STAT_OUT_NSK_FL_VA_PWM_EINH | string | Einheit von OUT_NSK_FL_VA_PWM |

<a id="job-status-out-ofi-pr-diag"></a>
### STATUS_OUT_OFI_PR_DIAG

ÜBERFÜLLSICHERUNG DIAGNOSE KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $8A Index fuer OUT_OFI_PR_DIAG $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_OFI_PR_DIAG_AN | int | Status von OUT_OFI_PR_DIAG |

<a id="job-status-out-ofi-pr-pwr"></a>
### STATUS_OUT_OFI_PR_PWR

ÜBERFÜLLSICHERUNG VERSORGUNG KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $8B Index fuer OUT_OFI_PR_PWR $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_OFI_PR_PWR_AKTIV | int | Status von OUT_OFI_PR_PWR |

<a id="job-status-out-p-accu-va"></a>
### STATUS_OUT_P_ACCU_VA

DRUCKSPEICHER PRS VENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $8C Index fuer OUT_P_ACCU_VA_PWM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_P_ACCU_VA_PWM_WERT | real | OUT_P_ACCU_VA_PWM Wert |
| STAT_OUT_P_ACCU_VA_PWM_EINH | string | Einheit von OUT_P_ACCU_VA_PWM |

<a id="job-status-out-reg-va"></a>
### STATUS_OUT_REG_VA

REGENERIERUNG PRS VENTIL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $8D Index fuer OUT_REG_VA_PWM $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_REG_VA_PWM_WERT | real | OUT_REG_VA_PWM Wert |
| STAT_OUT_REG_VA_PWM_EINH | string | Einheit von OUT_REG_VA_PWM |

<a id="job-status-out-strt-ilk"></a>
### STATUS_OUT_STRT_ILK

STARTER SPERRE KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $8E Index fuer OUT_STRT_ILK $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_OUT_STRT_ILK_AKTIV | int | Status von OUT_STRT_ILK |

<a id="job-status-p-futa-hy"></a>
### STATUS_P_FUTA_HY

DRUCK TANK INNEN WASSERSTOFF KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $8F Index fuer P_FUTA_HY $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_P_FUTA_HY_WERT | real | P_FUTA_HY Wert Normal Bereich 0 bis 12 Bar |
| STAT_P_FUTA_HY_EINH | string | Einheit von P_FUTA_HY |

<a id="job-status-p-suppln-hy"></a>
### STATUS_P_SUPPLN_HY

H2 Druck Versorgungsleituung KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $90 Index fuer P_SUPPLN_HY $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_P_SUPPLN_HY_WERT | real | P_SUPPLN_HY Wert |
| STAT_P_SUPPLN_HY_EINH | string | Einheit von P_SUPPLN_HY |

<a id="job-status-qu-frm-cc-mes-ext"></a>
### STATUS_QU_FRM_CC_MES_EXT

Gesamt Zahl Frames KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $91 Index fuer QU_FRM_CC_MES_EXT $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_QU_FRM_CC_MES_EXT_WERT | int | QU_FRM_CC_MES_EXT wert |

<a id="job-status-rng-hy"></a>
### STATUS_RNG_HY

Reichweite Wasserstoff KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $92 Index fuer RNG_HY $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_RNG_HY_WERT | int | RNG_HY Wert Normal Bereich 0 bis 4094 km Ungültig Wert = 4095 |
| STAT_RNG_HY_EINH | string | Einheit von RNG_HY |

<a id="job-status-rq-fu-tar"></a>
### STATUS_RQ_FU_TAR

ANFORDERUNG_KRAFTSTOFF_SOLL KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $93 Index fuer RQ_FU_TAR $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_RQ_FU_TAR_NR | int | 1 Benzin 2 Wasserstoff 3 Signal ungültig |
| STAT_RQ_FU_TAR_TEXT | string | Beschreibung RQ_FU_TAR |

<a id="job-status-st-cc-dsp-frq"></a>
### STATUS_ST_CC_DSP_FRQ

STATUS BLINKEN TAKT CHECKCONTROL MELDUNG ERWEITERT KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $94 Index fuer ST_CC_DSP_FRQ $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ST_CC_DSP_FRQ_NR | int | 0..kein Blinken 1..langsames Blinken 2..schnelles Blinken 3..Signal ungültig |
| STAT_ST_CC_DSP_FRQ_TEXT | string | Beschreibung ST_CC_DSP_FRQ |

<a id="job-status-st-cc-mess-ext"></a>
### STATUS_ST_CC_MESS_EXT

Meldung_setzen_ruecksetzen KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $95 Index fuer ST_CC_MESS_EXT $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ST_CC_MESS_EXT_NR | int | 0..rücksetzen 1..setzen 2..reserviert 3..Signal ungültig |
| STAT_ST_CC_MESS_EXT_TEXT | string | Beschreibung ST_CC_MESS_EXT |

<a id="job-status-st-fllv-futa-spar-hy"></a>
### STATUS_ST_FLLV_FUTA_SPAR_HY

Status_Füllstand_Tank_Reserve_Wasserstoff KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $96 Index fuer ST_FLLV_FUTA_SPAR_HY $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ST_FLLV_FUTA_SPAR_HY_NR | int | 0..Nicht aktiv 1..Aktiv 3..Signal ungültig |
| STAT_ST_FLLV_FUTA_SPAR_HY_TEXT | string | Beschreibung ST_FLLV_FUTA_SPAR_HY |

<a id="job-status-st-opmo-hy"></a>
### STATUS_ST_OPMO_HY

STATUS_BETRIEBSART_WASSERSTOFF KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $97 Index fuer ST_OPMO_HY $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ST_OPMO_HY_NR | int | 0..Reserviert 1..Wasserstoff Betrieb möglich 2..Wasserstoff Betrieb nicht möglich 3..Signal ungültig |
| STAT_ST_OPMO_HY_TEXT | string | Beschreibung ST_OPMO_HY |

<a id="job-status-st-opmochg-ce"></a>
### STATUS_ST_OPMOCHG_CE

Status Betriebsartenwechsel CE KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $98 Index fuer ST_OPMOCHG_CE $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ST_OPMOCHG_CE_NR | int | 0..kein BA-Wechsel 1-12..Reserviert 13..BA-Wechsel durchgeführt 14..BA-Wechsel abgebrochen 15..nicht erlaubt |
| STAT_ST_OPMOCHG_CE_TEXT | string | Beschreibung ST_OPMOCHG_CE |

<a id="job-status-st-rfg-hy"></a>
### STATUS_ST_RFG_HY

Status_Nachtanken_Wasserstoff KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $99 Index fuer ST_RFG_HY $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_ST_RFG_HY_NR | int | 1..H2-Nachtanken aktiv 2..H2-Nachtanken nicht aktiv 3..Signal ungültig |
| STAT_ST_RFG_HY_TEXT | string | Beschreibung ST_RFG_HY |

<a id="job-status-startfreigabe-ce"></a>
### STATUS_STARTFREIGABE_CE

Meldung Motorstart Verhindern KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $9A Index fuer STARTFREIGABE_CE $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_STARTFREIGABE_CE_NR | int | 0..Signal ungültig 1..Motorstart möglich 2..Motorstart nicht möglich 3..Fehlercode |
| STAT_STARTFREIGABE_CE_TEXT | string | Beschreibung STARTFREIGABE_CE |

<a id="job-status-temp-ex-ta"></a>
### STATUS_TEMP_EX_TA

TEMPERATUR AUßENDRUCK KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $9B Index fuer TEMP_EX_TA $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TEMP_EX_TA_WERT | real | TEMP_EX_TA Wert |
| STAT_TEMP_EX_TA_EINH | string | Einheit von TEMP_EX_TA |

<a id="job-status-tranf-cc-mess-ext"></a>
### STATUS_TRANF_CC_MESS_EXT

Übetragungsintervall KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $9C Index fuer TRANF_CC_MESS_EXT $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TRANF_CC_MESS_EXT_WERT | int | TRANF_CC_MESS_EXT Wert Normal Bereich 1 bis 14 Sekunden |

<a id="job-status-tstmp"></a>
### STATUS_TSTMP

ZEITSPANNE KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $9D Index fuer TSTMP $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_TSTMP_WERT | int | TSTMP Wert Zeitspannenauflösung 1 s, Abklemmen der CE-Versorgung führt zur Rücksetzung auf 0 |

<a id="job-status-utdt-cc-mess"></a>
### STATUS_UTDT_CC_MESS

NUTZDATEN_CHECK-CONTROL_MELDUNG KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $9E Index fuer UTDT_CC_MESS $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_UTDT_CC_MESS_WERT | long | UTDT_CC_MESS wert |

<a id="job-status-veh-co"></a>
### STATUS_VEH_CO

FAHRZEUGZUSTAND KWP2000:  $30 InputOutputControlByLocalIdentifier argument: $9F Index fuer VEH_CO $01 ReportCurrentState Modus  : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |
| STAT_VEH_CO_NR | int | 0..H2-Betankung 1..H2-Betrieb Fahrt 2..H2-Betrieb Stand 4..Druckaufbauzeit / Boil-Off |
| STAT_VEH_CO_TEXT | string | Beschreibung VEH_CO |

## Tables

### Index

- [KONZEPT_TABELLE](#table-konzept-tabelle) (5 × 2)
- [JOBRESULT](#table-jobresult) (95 × 2)
- [LIEFERANTEN](#table-lieferanten) (91 × 2)
- [FARTTEXTE](#table-farttexte) (14 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [AUTHENTISIERUNG](#table-authentisierung) (4 × 2)
- [DIAGMODE](#table-diagmode) (14 × 3)
- [BAUDRATE](#table-baudrate) (7 × 3)
- [IARTTEXTE](#table-iarttexte) (14 × 2)
- [SPEICHERSEGMENT](#table-speichersegment) (12 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [SG_DIAGNOSEKONZEPT](#table-sg-diagnosekonzept) (4 × 2)
- [FORTTEXTE](#table-forttexte) (138 × 2)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (7 × 2)
- [FUMWELTMATRIX](#table-fumweltmatrix) (137 × 5)
- [FUMWELTTEXTE](#table-fumwelttexte) (108 × 9)
- [FARTTYP](#table-farttyp) (137 × 5)
- [FARTTEXTEINDIVIDUELL](#table-farttexteindividuell) (119 × 2)
- [HORTTEXTE](#table-horttexte) (1 × 2)
- [IORTTEXTE](#table-iorttexte) (8 × 2)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (7 × 2)
- [IUMWELTMATRIX](#table-iumweltmatrix) (7 × 5)
- [IUMWELTTEXTE](#table-iumwelttexte) (106 × 9)
- [IARTTYP](#table-iarttyp) (7 × 5)
- [IARTTEXTEINDIVIDUELL](#table-iarttexteindividuell) (116 × 2)

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

Dimensions: 91 rows × 2 columns

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

Dimensions: 138 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x648C | H2-Alarm Tankkupplung |
| 0x648D | H2-Alarm Nebensystemkapsel |
| 0x648E | Steuergerät, interner Fehler |
| 0x648F | Batterie 2 |
| 0x6490 | Batterie 1 |
| 0x6491 | Tankdruck zu hoch |
| 0x6492 | Versorgungsleitung |
| 0x6493 | Boil-Off Arbeitspunkt |
| 0x6494 | Crash |
| 0x6495 | Tankklappe |
| 0x6496 | DME Kommunikation |
| 0x6497 | Wärmetauscher |
| 0x6498 | Wärmetauscher, Kühlwassersensoren |
| 0x649A | Temperatursensor Austritt Kühlmittel |
| 0x649B | Temperatursensor Eintritt Kühlmittel |
| 0x649C | Temperatursensor Oxidator |
| 0x649D | Temperatursensor Motorabsperrventil |
| 0x649E | Temperatursensor Austritt Wärmetauscher |
| 0x649F | Drucksensor Austritt Teilstromregelventil |
| 0x64A0 | Drucksensor Austritt Motorabsperrventil |
| 0x64A1 | Drucksensor Austritt Boil-Off Ventil |
| 0x64A2 | Drucksensor Stichleitung |
| 0x64A3 | Drucksensor Eintritt Boil-Off Ventil |
| 0x64A4 | Hallsensor 1, zu am Tankdeckel |
| 0x64A5 | Hallsensor 2, zu am Tankdeckelgetriebe |
| 0x64A6 | Hallsensor 3, offen am Tankdeckelgetriebe |
| 0x64A7 | Überfüllsicherung 1 |
| 0x64A8 | Überfüllsicherung 2 |
| 0x64A9 | Eingang 1 Starter Interlock |
| 0x64AA | Eingang 2 Starter Interlock |
| 0x64AB | Tankwahlschalter |
| 0x64AD | H2-Sensor Passagierraum |
| 0x64AE | H2-Sensor Motorraum |
| 0x64AF | H2-Sensor Tankkupplung |
| 0x64B0 | H2-Sensor Nebensystemkapsel |
| 0x64B1 | H2-Sensor Kofferraum |
| 0x64B2 | Luftdrucksensor 1 |
| 0x64B3 | H2-Alarm Passagierraum |
| 0x64B4 | Energiemanagement Batterie 1 |
| 0x64B5 | Energiemanagement Batterie 2 |
| 0x64B6 | Teilstromregelventil |
| 0x64B7 | Motorabsperrventil |
| 0x64B8 | Tankklappe |
| 0x64B9 | Ausgangskreis Zusatzwasserpumpe |
| 0x64BA | Tankdruck zu niedrig |
| 0x64BB | Ausgangskreis Starter Interlock |
| 0x64BC | Bordnetzspannung |
| 0x64BD | CE-SG, Kanal 1, Ausfall Stromversorgung |
| 0x64BE | CE-SG, Kanal 2, Ausfall Stromversorgung |
| 0x64BF | Crash Sensor |
| 0x64C0 | Dichtigkeitstest der Ventile |
| 0x64C1 | Batterie 1 und 2 |
| 0x64C2 | Batterie 1 |
| 0x64C3 | Tank-Isolationsvakuum |
| 0x64C4 | Dichtigkeitstest der Ventile ist fällig |
| 0x64C5 | Temperatursensor Wärmetauscher Eingang |
| 0x64C6 | Temperatursensor Kompressor |
| 0x64C7 | Temperatursensor Eingang Venturidüse |
| 0x64C8 | Drucksensor in Steuerleitung für gasförmigen H2 |
| 0x64C9 | Drucksensor in Steuerleitung für flüssigen H2 |
| 0x64CA | Drucksensor Eingang PRS Druckspeicher |
| 0x64CB | Boil-Off Ventil |
| 0x64CC | TSE-CAN-Nachricht Druck |
| 0x64CD | Zusatzentlüftungsventil |
| 0x64CE | Druckspeicher PRS-Ventil |
| 0x64CF | NSK-Spülung PRS-Ventil |
| 0x64D0 | Regenerierung PRS-Ventil |
| 0x64D1 | Steuerventil für Entnahme von flüssigem H2 |
| 0x64D2 | Steuerventil für Entnahme von gasförmigem H2 |
| 0x64D3 | Pneumatik, Druckauf- oder Abbau |
| 0x64D4 | Druckfehler Druckspeicher |
| 0x64D5 | Druckaufbaufehler im Druckspeicher |
| 0x64D6 | Entfeuchtung nicht erfolgreich |
| 0x64D7 | PRS Spülung nicht erfolgreich |
| 0x64D8 | Temperatursensor Tankkupplung |
| 0x64D9 | IBS-Kommunikation Batterie 1 |
| 0x64DA | Regelthermostat |
| 0x64DB | Druckentlastungsventil leckt |
| 0x64DC | Druckentlastungsventil blockiert |
| 0x64DD | TSE nicht kalibriert/defekt |
| 0x64DE | TSE Massenberechnung |
| 0x64DF | TSE Füllstandssensor Kanal 1 |
| 0x64E0 | TSE Füllstandssensor Kanal 2 |
| 0x64E2 | TSE Temperatursensor Kanal 1 |
| 0x64E3 | TSE Temperatursensor Kanal 2 |
| 0x64E4 | IBS-Kommunikation Batterie 2 |
| 0x64E5 | Batterie 2 |
| 0x64E6 | Sicherheitsventil |
| 0x64E7 | Befüll- und Entnahmeventil für flüssigen H2 |
| 0x64E8 | Defektes Vakuum am Tankfüllstutzen oder offen blockiertes Befüll- und Entnahmeventil während Betankung |
| 0x64E9 | Defektes Vakuum am Tankfüllstutzen oder offen blockiertes Befüll- und Entnahmeventil während H2-Betrieb |
| 0x64EA | Defektes Vakuum am Tankfüllstutzen oder offen blockiertes Befüll- und Entnahmeventil während keine Betankung und kein H2-Betrieb |
| 0x64EB | H2-Alarm Motorraum |
| 0x64EC | Luftdrucksensor, Motorsteuerung |
| 0x64ED | Batterie 1 |
| 0x64EE | Batterie 2 |
| 0x64F0 | H2-Sensor Kofferraum schwerer Fehler |
| 0x64F1 | H2-High-Alarm Kofferraum |
| 0x64F2 | H2-Sensor Motorraum schwerer Fehler |
| 0x64F3 | H2-High-Alarm Motorraum |
| 0x64F4 | H2-Sensor Tankkupplung schwerer Fehler |
| 0x64F5 | H2-High-Alarm Tankkupplung |
| 0x64F6 | H2-Sensor Passagierraum schwerer Fehler |
| 0x64F7 | H2-High-Alarm Passagierraum |
| 0x64F8 | H2-Sensor Nebensystemkapsel schwerer Fehler |
| 0x64F9 | H2-High-Alarm Nebensystemkapsel |
| 0x6500 | Befüll- und Entnahmeventil für flüssigen H2 |
| 0x6501 | H2-Alarm Kofferraum |
| 0x6502 | Steuerventil für flüssigen H2 |
| 0x6503 | Steuerventil für gasförmigen H2 |
| 0x6504 | Teilstromregelventil |
| 0x6505 | Motorabsperrventil |
| 0x6506 | IBS an Batterie 1 |
| 0x6507 | IBS an Batterie 2 |
| 0x6508 | Befüll- und Entnahmeventil für gasförmigen H2 |
| 0x6509 | Wärmetauscher |
| 0xCE07 | PT-CAN Kommunikationsfehler |
| 0xCE0B | Füllstands-CAN Kommunikationsfehler |
| 0xCE0F | H2-CAN 1 Kommunikationsfehler |
| 0xCE13 | H2-CAN 2 Kommunikationsfehler |
| 0xCE14 | Botschaft (ENGINE_HVEH, 1D3) |
| 0xCE15 | Botschaft (TORQUE_3, AA) |
| 0xCE16 | Botschaft (KLEMMENSTATUS, 130) |
| 0xCE18 | Botschaft (GESCHWINDIGKEIT, 1A0) |
| 0xCE19 | Botschaft (STAT_ZV_KLAPPEN, 2FC) |
| 0xCE1A | Botschaft (VERZOEGERUNG_ANF_EMF, AE) |
| 0xCE1B | Botschaft (ENGINE_1, 1D0) |
| 0xCE1C | Botschaft (GETRIEBEDATEN, BA) |
| 0xCE1D | Botschaft (KILOMETERSTAND, 330) |
| 0xCE1E | Botschaft (HS_PSCMP, H2-CAN 1, 648) |
| 0xCE1F | Botschaft (HS_ENG, H2-CAN 1, 658) |
| 0xCE20 | Botschaft (HS_FUTA_CLT, H2-CAN 1, 660) |
| 0xCE21 | Botschaft (HS_SCAP, H2-CAN 2, 640) |
| 0xCE22 | Botschaft (HS_BOOT, H2-CAN 2, 650) |
| 0xCE24 | Botschaft (MM_M, Fuel-CAN, 258) |
| 0xCE25 | Botschaft (MM_T, Fuel-CAN, 258) |
| 0xCE26 | Botschaft (BEDIENUNG_AUDIO_TEL, 1D6) |
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
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-fumweltmatrix"></a>
### FUMWELTMATRIX

Dimensions: 137 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x648C | 0x0066 | 0x0001 | 0x0049 | 0xFFFE |
| 0x648D | 0x0066 | 0x0001 | 0x004D | 0xFFFE |
| 0x648E | 0x0066 | 0x0001 | 0x0064 | 0x0065 |
| 0x648F | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x6490 | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x6491 | 0x0066 | 0x0002 | 0x0003 | 0x0004 |
| 0x6492 | 0x0066 | 0x0001 | 0x0004 | 0x0005 |
| 0x6493 | 0x0020 | 0x000F | 0x0001 | 0x0008 |
| 0x6494 | 0x0066 | 0x0024 | 0x0027 | 0xFFFE |
| 0x6495 | 0x0066 | 0x003F | 0x0041 | 0x0043 |
| 0x6496 | 0x0066 | 0x0001 | 0xFFFE | 0xFFFE |
| 0x6497 | 0x0011 | 0x0013 | 0x0015 | 0x0017 |
| 0x6498 | 0x0011 | 0x0013 | 0x0015 | 0x0017 |
| 0x649A | 0x0066 | 0x0018 | 0xFFFE | 0xFFFE |
| 0x649B | 0x0066 | 0x0016 | 0xFFFE | 0xFFFE |
| 0x649C | 0x0066 | 0x001F | 0x0008 | 0x0010 |
| 0x649D | 0x0066 | 0x0014 | 0xFFFE | 0xFFFE |
| 0x649E | 0x0066 | 0x0012 | 0xFFFE | 0xFFFE |
| 0x649F | 0x0002 | 0x0003 | 0x0006 | 0x0007 |
| 0x64A0 | 0x0002 | 0x0003 | 0x0006 | 0x0007 |
| 0x64A1 | 0x0066 | 0x0009 | 0x0008 | 0x000B |
| 0x64A2 | 0x0002 | 0x0003 | 0x0006 | 0x0007 |
| 0x64A3 | 0x0002 | 0x0003 | 0x0006 | 0x0007 |
| 0x64A4 | 0x0066 | 0x0040 | 0x0042 | 0xFFFE |
| 0x64A5 | 0x0066 | 0x0040 | 0x0042 | 0xFFFE |
| 0x64A6 | 0x0066 | 0x0044 | 0xFFFE | 0xFFFE |
| 0x64A7 | 0x0066 | 0x0002 | 0x0057 | 0x0058 |
| 0x64A8 | 0x0066 | 0x0002 | 0x0057 | 0x0058 |
| 0x64A9 | 0x0066 | 0x0029 | 0xFFFE | 0xFFFE |
| 0x64AA | 0x0066 | 0x002B | 0xFFFE | 0xFFFE |
| 0x64AB | 0x0066 | 0x0001 | 0xFFFE | 0xFFFE |
| 0x64AD | 0x0066 | 0x0001 | 0x004C | 0x0061 |
| 0x64AE | 0x0066 | 0x0001 | 0x0048 | 0x005F |
| 0x64AF | 0x0066 | 0x0001 | 0x004A | 0x0060 |
| 0x64B0 | 0x0066 | 0x0001 | 0x004E | 0x0062 |
| 0x64B1 | 0x0066 | 0x0001 | 0x0046 | 0x005E |
| 0x64B2 | 0x0066 | 0x000A | 0x0008 | 0x000B |
| 0x64B3 | 0x0066 | 0x0001 | 0x004B | 0xFFFE |
| 0x64B4 | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x64B5 | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x64B6 | 0x0031 | 0x0032 | 0x0022 | 0x0023 |
| 0x64B7 | 0x0033 | 0x0034 | 0x0022 | 0x0023 |
| 0x64B8 | 0x003D | 0x003E | 0x0022 | 0x0023 |
| 0x64B9 | 0x0063 | 0x005C | 0x005D | 0xFFFE |
| 0x64BA | 0x0066 | 0x0002 | 0x0003 | 0x0004 |
| 0x64BB | 0x0066 | 0x002A | 0x002C | 0x0024 |
| 0x64BC | 0x0066 | 0x0025 | 0x0026 | 0xFFFE |
| 0x64BD | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x64BE | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x64BF | 0x0066 | 0x0028 | 0x0024 | 0xFFFE |
| 0x64C0 | 0x0066 | 0x0001 | 0x0004 | 0x0005 |
| 0x64C1 | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x64C2 | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x64C3 | 0x0066 | 0x0001 | 0x0059 | 0x005A |
| 0x64C4 | 0x0066 | 0x0001 | 0x0004 | 0x0005 |
| 0x64C5 | 0x0066 | 0x001C | 0xFFFE | 0xFFFE |
| 0x64C6 | 0x0066 | 0x001A | 0xFFFE | 0xFFFE |
| 0x64C7 | 0x0066 | 0x001F | 0x0008 | 0x0010 |
| 0x64C8 | 0x0066 | 0x000C | 0x000D | 0x000E |
| 0x64C9 | 0x0066 | 0x000C | 0x000D | 0x000E |
| 0x64CA | 0x0066 | 0x000C | 0x000D | 0x000E |
| 0x64CB | 0x0066 | 0x0008 | 0x0001 | 0x0009 |
| 0x64CC | 0x0066 | 0x0001 | 0x004F | 0xFFFE |
| 0x64CD | 0x0035 | 0x0036 | 0x0022 | 0x0023 |
| 0x64CE | 0x0037 | 0x0038 | 0x0022 | 0x0023 |
| 0x64CF | 0x0039 | 0x003A | 0x0022 | 0x0023 |
| 0x64D0 | 0x003B | 0x003C | 0x0022 | 0x0023 |
| 0x64D1 | 0x002D | 0x002E | 0x0022 | 0x0023 |
| 0x64D2 | 0x002F | 0x0030 | 0x0022 | 0x0023 |
| 0x64D3 | 0x0066 | 0x000C | 0x000D | 0x000E |
| 0x64D4 | 0x0066 | 0x000C | 0x000D | 0x000E |
| 0x64D5 | 0x0066 | 0x0019 | 0x000C | 0x000E |
| 0x64D6 | 0x0066 | 0x000C | 0x000D | 0x000E |
| 0x64D7 | 0x0066 | 0x000C | 0x000E | 0x004D |
| 0x64D8 | 0x0066 | 0x001E | 0xFFFE | 0xFFFE |
| 0x64D9 | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x64DA | 0x0015 | 0x0017 | 0x0011 | 0x005C |
| 0x64DB | 0x0001 | 0x0004 | 0x001B | 0x0013 |
| 0x64DC | 0x0002 | 0x0003 | 0x0004 | 0x001B |
| 0x64DD | 0x0066 | 0x0001 | 0x004F | 0xFFFE |
| 0x64DE | 0x0066 | 0x0001 | 0x004F | 0xFFFE |
| 0x64DF | 0x0066 | 0x0001 | 0x004F | 0xFFFE |
| 0x64E0 | 0x0066 | 0x0001 | 0x004F | 0xFFFE |
| 0x64E2 | 0x0066 | 0x0001 | 0x004F | 0xFFFE |
| 0x64E3 | 0x0066 | 0x0001 | 0x004F | 0xFFFE |
| 0x64E4 | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x64E5 | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x64E6 | 0x0066 | 0x005B | 0x0059 | 0x005A |
| 0x64E7 | 0x0066 | 0x001D | 0x0011 | 0x0056 |
| 0x64E8 | 0x0066 | 0x0054 | 0x0011 | 0x0063 |
| 0x64E9 | 0x0055 | 0x0011 | 0x0056 | 0xFFFE |
| 0x64EA | 0x0066 | 0x0011 | 0x0013 | 0xFFFE |
| 0x64EB | 0x0066 | 0x0001 | 0x0047 | 0xFFFE |
| 0x64EC | 0x0066 | 0x0009 | 0x0008 | 0x000B |
| 0x64ED | 0x0050 | 0x0051 | 0x0052 | 0x0053 |
| 0x64EE | 0x0050 | 0x0051 | 0x0052 | 0x0053 |
| 0x64F0 | 0x0066 | 0x0001 | 0x0046 | 0x005E |
| 0x64F1 | 0x0066 | 0x0001 | 0x0045 | 0xFFFE |
| 0x64F2 | 0x0066 | 0x0001 | 0x0048 | 0x005F |
| 0x64F3 | 0x0066 | 0x0001 | 0x0047 | 0xFFFE |
| 0x64F4 | 0x0066 | 0x0001 | 0x004A | 0x0060 |
| 0x64F5 | 0x0066 | 0x0001 | 0x0049 | 0xFFFE |
| 0x64F6 | 0x0066 | 0x0001 | 0x004C | 0x0061 |
| 0x64F7 | 0x0066 | 0x0001 | 0x004B | 0xFFFE |
| 0x64F8 | 0x0066 | 0x0001 | 0x004E | 0x0062 |
| 0x64F9 | 0x0066 | 0x0001 | 0x004D | 0xFFFE |
| 0x6500 | 0x0066 | 0x0069 | 0x006A | 0x004F |
| 0x6501 | 0x0066 | 0x0001 | 0x0045 | 0xFFFE |
| 0x6502 | 0x002D | 0x002E | 0x0022 | 0x0023 |
| 0x6503 | 0x002F | 0x0030 | 0x0022 | 0x0023 |
| 0x6504 | 0x0031 | 0x0032 | 0x0022 | 0x0023 |
| 0x6505 | 0x0033 | 0x0034 | 0x0022 | 0x0023 |
| 0x6506 | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x6507 | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x6508 | 0x0066 | 0x0001 | 0x0004 | 0x004F |
| 0x6509 | 0x0066 | 0x004F | 0x0001 | 0x0021 |
| 0xCE07 | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE0B | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE0F | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE13 | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE14 | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE15 | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE16 | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE18 | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE19 | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE1A | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE1B | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE1C | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE1D | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE1E | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE1F | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE20 | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE21 | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE22 | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |
| 0xCE24 | 0x0066 | 0x0001 | 0x004F | 0xFFFE |
| 0xCE25 | 0x0066 | 0x0001 | 0x004F | 0xFFFE |
| 0xCE26 | 0x0067 | 0x0068 | 0xFFFE | 0xFFFE |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 108 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | IN_FUTA_P_V | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0002 | IN_FUTA_P_1_CD | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0003 | IN_FUTA_P_2_CD | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0004 | IN_SUPPIPE_P_1_V | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0005 | IN_SUPPIPE_P_2_V | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0006 | IN_SUPPIPE_P_1_CD | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0007 | IN_SUPPIPE_P_2_CD | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0008 | IN_BO_P_V | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0009 | IN_AMB_P_V | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x000A | IN_AMB_P_CD | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x000B | AIP_ENG_V | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x000C | IN_GHY_CL_P_V | bar | high | unsigned int | - | 21 | 65535 | 0 |
| 0x000D | IN_LHY_CL_P_V | bar | high | unsigned int | - | 21 | 65535 | 0 |
| 0x000E | IN_PRS_ACCU_P_V | bar | high | unsigned int | - | 21 | 65535 | 0 |
| 0x000F | IN_OX_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0010 | IN_OX_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0011 | IN_MPVA_IN_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0012 | IN_MPVA_IN_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0013 | IN_MPVA_SP_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0014 | IN_MPVA_SP_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0015 | IN_COL_INL_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0016 | IN_COL_INL_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0017 | IN_COL_EXH_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0018 | IN_COL_EXH_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0019 | IN_COMP_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x001A | IN_COMP_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x001B | IN_HEATEX_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x001C | IN_HEATEX_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x001D | IN_FUT_CLT_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x001E | IN_FUT_CLT_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x001F | IN_VENT_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0020 | IN_VENT_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0021 | DMA_TEMP_V | °C | high | unsigned int | - | 360 | 65535 | -260 |
| 0x0022 | IN_BT_U_1_CD | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0023 | IN_BT_U_2_CD | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0024 | IN_BN_V | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0025 | IN_BN_CD | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0026 | IN_BN_CD_O | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0027 | IN_CR_V | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0028 | IN_CR_CD | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0029 | IN_STRT_ILK_1_CD | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x002A | IN_STRT_ILK_1_V | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x002B | IN_STRT_ILK_2_CD | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x002C | IN_STRT_ILK_2_V | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x002D | IN_LHY_COV_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x002E | IN_LHY_COV_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x002F | IN_GHY_COV_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0030 | IN_GHY_COV_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0031 | IN_MPVA_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0032 | IN_MPVA_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0033 | IN_ENG_SOV_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0034 | IN_ENG_SOV_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0035 | IN_ADD_ABV_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0036 | IN_ADD_ABV_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0037 | IN_P_ACCU_VA_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0038 | IN_P_ACCU_VA_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0039 | IN_NSK_FL_VA_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x003A | IN_NSK_FL_VA_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x003B | IN_REG_VA_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x003C | IN_REG_VA_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x003D | IN_FUFF_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x003E | IN_FUFF_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x003F | IN_FTC_CLO_1_V | mA | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0040 | IN_FTC_CLO_1_CD | mA | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0041 | IN_FTC_CLO_2_V | mA | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0042 | IN_FTC_CLO_2_CD | mA | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0043 | IN_FTC_OPN_V | mA | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0044 | IN_FTC_OPN_CD | mA | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0045 | HS_BOOT_HYC_V | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x0046 | HS_BOOT_HYC_CD | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x0047 | HS_ENG_HYC_V | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x0048 | HS_ENG_HYC_CD | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x0049 | HS_FUTA_CLT_HYC_V | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x004A | HS_FUTA_CLT_HYC_CD | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x004B | HS_PSCMP_HYC_V | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x004C | HS_PSCMP_HYC_CD | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x004D | HS_SCAP_HYC_V | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x004E | HS_SCAP_HYC_CD | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x004F | WGH_LH2_V | g | high | unsigned int | - | 10000 | 65535 | 0 |
| 0x0050 | R_QVM_T_1_CD | min | high | unsigned int | - | 1 | 1 | 0 |
| 0x0051 | R_QVM_T_2_CD | min | high | unsigned int | - | 1 | 1 | 0 |
| 0x0052 | R_QVM_T_3_CD | min | high | unsigned int | - | 1 | 1 | 0 |
| 0x0053 | R_QVM_T_4_CD | min | high | unsigned int | - | 1 | 1 | 0 |
| 0x0054 | CURR_REF_TIME | min | high | unsigned int | - | 1 | 1 | 0 |
| 0x0055 | CURR_H2_TIME | min | high | unsigned int | - | 1 | 1 | 0 |
| 0x0056 | COSP_HY_AVL_V | kg/h | high | unsigned int | - | 200 | 65535 | 0 |
| 0x0057 | IN_OFI_PR_1_CD | Ohm | high | unsigned int | - | 10000 | 65535 | 0 |
| 0x0058 | IN_OFI_PR_2_CD | Ohm | high | unsigned int | - | 10000 | 65535 | 0 |
| 0x0059 | P_DA | W | high | unsigned int | - | 40 | 65535 | 0 |
| 0x005A | P_BO | W | high | unsigned int | - | 40 | 65535 | 0 |
| 0x005B | P_DA_SV | W | high | unsigned int | - | 40 | 65535 | 0 |
| 0x005C | IN_AUWP_H2_RPM_V | rpm | high | unsigned int | - | 1 | 1 | 0 |
| 0x005D | OUT_AUWP_H2_RPM | rpm | high | unsigned int | - | 1 | 1 | 0 |
| 0x005E | DIAG_HS_BOOT_PARAM | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x005F | DIAG_HS_ENG_PARAM | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0060 | DIAG_HS_FUTA_CLT_PARAM | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0061 | DIAG_HS_PSCMP_PARAM | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0062 | DIAG_HS_SCAP_PARAM | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0063 | BETRIEBSZUST | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0064 | ST_CLC_N_CD | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0065 | ST_CLC_P_CD | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0066 | SYSTEM_TIME | h | high | unsigned int | - | 1 | 1 | 0 |
| 0x0067 | ST_KL_15_V | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0068 | ST_KL_R_V | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0069 | IN_OFI_PR_1_V | Ohm | high | unsigned int | - | 10000 | 65535 | 0 |
| 0x006A | IN_OFI_PR_2_V | Ohm | high | unsigned int | - | 10000 | 65535 | 0 |
| 0xFFFE | Unbenutzte Umweltbedingung | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFFFF | Unbekannte Umweltbedingung | - | high | unsigned int | - | 1 | 1 | 0 |

<a id="table-farttyp"></a>
### FARTTYP

Dimensions: 137 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x648C | 0xFFFF | 0x0048 | 0xFFFF | 0xFFFF |
| 0x648D | 0xFFFF | 0x0048 | 0xFFFF | 0xFFFF |
| 0x648E | 0x0069 | 0x0062 | 0x0008 | 0x0061 |
| 0x648F | 0xFFFF | 0x000A | 0xFFFF | 0xFFFF |
| 0x6490 | 0xFFFF | 0x000A | 0xFFFF | 0xFFFF |
| 0x6491 | 0xFFFF | 0xFFFF | 0x000B | 0x0039 |
| 0x6492 | 0xFFFF | 0xFFFF | 0xFFFF | 0x000D |
| 0x6493 | 0x0038 | 0x0037 | 0x0057 | 0x000E |
| 0x6494 | 0xFFFF | 0xFFFF | 0xFFFF | 0x000F |
| 0x6495 | 0xFFFF | 0x0010 | 0xFFFF | 0xFFFF |
| 0x6496 | 0xFFFF | 0xFFFF | 0x0060 | 0xFFFF |
| 0x6497 | 0xFFFF | 0x0013 | 0x0014 | 0x006E |
| 0x6498 | 0xFFFF | 0x0036 | 0xFFFF | 0x0015 |
| 0x649A | 0x0069 | 0x0068 | 0x0067 | 0x0066 |
| 0x649B | 0x0069 | 0x0068 | 0x0067 | 0x0066 |
| 0x649C | 0x0069 | 0x0068 | 0x0067 | 0x0066 |
| 0x649D | 0x0069 | 0x0068 | 0x0067 | 0x0066 |
| 0x649E | 0x0069 | 0x0068 | 0x0067 | 0x0066 |
| 0x649F | 0x0069 | 0x0068 | 0x006A | 0x0066 |
| 0x64A0 | 0x0069 | 0x0068 | 0x006A | 0x0066 |
| 0x64A1 | 0x0069 | 0x0068 | 0x006A | 0x0066 |
| 0x64A2 | 0x0069 | 0x0068 | 0x006A | 0x0066 |
| 0x64A3 | 0x0069 | 0x0068 | 0x006A | 0x0066 |
| 0x64A4 | 0xFFFF | 0x0068 | 0x0074 | 0x0074 |
| 0x64A5 | 0xFFFF | 0x0068 | 0x0074 | 0x0074 |
| 0x64A6 | 0xFFFF | 0x0068 | 0x0074 | 0x0074 |
| 0x64A7 | 0x0069 | 0x0068 | 0x0067 | 0x0066 |
| 0x64A8 | 0x0069 | 0x0068 | 0x0067 | 0x0066 |
| 0x64A9 | 0xFFFF | 0x0068 | 0x0067 | 0x0066 |
| 0x64AA | 0xFFFF | 0x0068 | 0x0067 | 0x0066 |
| 0x64AB | 0xFFFF | 0x0068 | 0xFFFF | 0xFFFF |
| 0x64AD | 0x004B | 0x004A | 0xFFFF | 0xFFFF |
| 0x64AE | 0x004B | 0x004A | 0xFFFF | 0xFFFF |
| 0x64AF | 0x004B | 0x004A | 0xFFFF | 0xFFFF |
| 0x64B0 | 0x004B | 0x004A | 0xFFFF | 0xFFFF |
| 0x64B1 | 0x004B | 0x004A | 0xFFFF | 0xFFFF |
| 0x64B2 | 0x0069 | 0x0068 | 0x0067 | 0x0066 |
| 0x64B3 | 0xFFFF | 0x0048 | 0xFFFF | 0xFFFF |
| 0x64B4 | 0xFFFF | 0x0045 | 0xFFFF | 0xFFFF |
| 0x64B5 | 0xFFFF | 0x0045 | 0xFFFF | 0xFFFF |
| 0x64B6 | 0x0024 | 0xFFFF | 0x0022 | 0x0023 |
| 0x64B7 | 0x0024 | 0xFFFF | 0x0022 | 0x0023 |
| 0x64B8 | 0xFFFF | 0xFFFF | 0xFFFF | 0x0075 |
| 0x64B9 | 0x0028 | 0x0027 | 0xFFFF | 0x0070 |
| 0x64BA | 0x004D | 0x004E | 0x004C | 0x000C |
| 0x64BB | 0x0026 | 0x0025 | 0xFFFF | 0xFFFF |
| 0x64BC | 0x0069 | 0x0068 | 0x006A | 0x0066 |
| 0x64BD | 0xFFFF | 0x0068 | 0x0067 | 0x0066 |
| 0x64BE | 0xFFFF | 0x0068 | 0x0067 | 0x0066 |
| 0x64BF | 0xFFFF | 0x0068 | 0x0067 | 0x0066 |
| 0x64C0 | 0x005E | 0x005D | 0x005C | 0x005B |
| 0x64C1 | 0x002A | 0x0029 | 0x001C | 0x001B |
| 0x64C2 | 0xFFFF | 0x001D | 0x001E | 0xFFFF |
| 0x64C3 | 0xFFFF | 0x001F | 0xFFFF | 0xFFFF |
| 0x64C4 | 0xFFFF | 0xFFFF | 0x005F | 0xFFFF |
| 0x64C5 | 0x0069 | 0x0068 | 0x0067 | 0x0066 |
| 0x64C6 | 0xFFFF | 0x0068 | 0x0067 | 0x0066 |
| 0x64C7 | 0x0069 | 0x0068 | 0x0067 | 0x0066 |
| 0x64C8 | 0x0069 | 0x0068 | 0x006A | 0x0066 |
| 0x64C9 | 0x0069 | 0x0068 | 0x006A | 0x0066 |
| 0x64CA | 0x0069 | 0x0068 | 0x006A | 0x0066 |
| 0x64CB | 0xFFFF | 0x0010 | 0x0012 | 0x0011 |
| 0x64CC | 0xFFFF | 0xFFFF | 0xFFFF | 0x006B |
| 0x64CD | 0x0024 | 0xFFFF | 0x0022 | 0x0023 |
| 0x64CE | 0x0024 | 0xFFFF | 0x0022 | 0x0023 |
| 0x64CF | 0x0024 | 0xFFFF | 0x0022 | 0x0023 |
| 0x64D0 | 0x0024 | 0xFFFF | 0x0022 | 0x0023 |
| 0x64D1 | 0x0024 | 0xFFFF | 0x0022 | 0x0023 |
| 0x64D2 | 0x0024 | 0xFFFF | 0x0022 | 0x0023 |
| 0x64D3 | 0x002E | 0x002D | 0x002C | 0x002B |
| 0x64D4 | 0xFFFF | 0xFFFF | 0x002F | 0x0031 |
| 0x64D5 | 0xFFFF | 0x0032 | 0xFFFF | 0xFFFF |
| 0x64D6 | 0xFFFF | 0x0033 | 0xFFFF | 0xFFFF |
| 0x64D7 | 0xFFFF | 0x0034 | 0xFFFF | 0xFFFF |
| 0x64D8 | 0xFFFF | 0x0068 | 0x0067 | 0x0066 |
| 0x64D9 | 0xFFFF | 0x0018 | 0x0017 | 0xFFFF |
| 0x64DA | 0xFFFF | 0x003B | 0x003A | 0x006F |
| 0x64DB | 0xFFFF | 0xFFFF | 0xFFFF | 0x003C |
| 0x64DC | 0xFFFF | 0xFFFF | 0xFFFF | 0x0010 |
| 0x64DD | 0x0071 | 0x003D | 0x003E | 0x0035 |
| 0x64DE | 0x0042 | 0xFFFF | 0x003F | 0x003E |
| 0x64DF | 0xFFFF | 0x0042 | 0x0041 | 0x0040 |
| 0x64E0 | 0xFFFF | 0x0042 | 0x0041 | 0x0040 |
| 0x64E2 | 0xFFFF | 0x0042 | 0x0041 | 0x0040 |
| 0x64E3 | 0xFFFF | 0x0042 | 0x0041 | 0x0040 |
| 0x64E4 | 0xFFFF | 0x0018 | 0x0017 | 0xFFFF |
| 0x64E5 | 0xFFFF | 0x001D | 0x001E | 0xFFFF |
| 0x64E6 | 0xFFFF | 0xFFFF | 0xFFFF | 0x0058 |
| 0x64E7 | 0xFFFF | 0xFFFF | 0xFFFF | 0x0053 |
| 0x64E8 | 0xFFFF | 0xFFFF | 0x0054 | 0x0054 |
| 0x64E9 | 0xFFFF | 0xFFFF | 0xFFFF | 0x0055 |
| 0x64EA | 0xFFFF | 0xFFFF | 0xFFFF | 0x0056 |
| 0x64EB | 0xFFFF | 0x0048 | 0xFFFF | 0xFFFF |
| 0x64EC | 0x0069 | 0x0068 | 0xFFFF | 0xFFFF |
| 0x64ED | 0xFFFF | 0xFFFF | 0xFFFF | 0x0009 |
| 0x64EE | 0xFFFF | 0xFFFF | 0xFFFF | 0x0009 |
| 0x64F0 | 0xFFFF | 0xFFFF | 0x0068 | 0xFFFF |
| 0x64F1 | 0xFFFF | 0xFFFF | 0x0049 | 0xFFFF |
| 0x64F2 | 0xFFFF | 0xFFFF | 0x0068 | 0xFFFF |
| 0x64F3 | 0xFFFF | 0xFFFF | 0x0049 | 0xFFFF |
| 0x64F4 | 0xFFFF | 0xFFFF | 0x0068 | 0xFFFF |
| 0x64F5 | 0xFFFF | 0xFFFF | 0x0049 | 0xFFFF |
| 0x64F6 | 0xFFFF | 0xFFFF | 0x0068 | 0xFFFF |
| 0x64F7 | 0xFFFF | 0xFFFF | 0x0049 | 0xFFFF |
| 0x64F8 | 0xFFFF | 0xFFFF | 0x0068 | 0xFFFF |
| 0x64F9 | 0xFFFF | 0xFFFF | 0x0049 | 0xFFFF |
| 0x6500 | 0xFFFF | 0xFFFF | 0x0073 | 0xFFFF |
| 0x6501 | 0xFFFF | 0x0048 | 0xFFFF | 0xFFFF |
| 0x6502 | 0xFFFF | 0x0064 | 0x0065 | 0x0063 |
| 0x6503 | 0xFFFF | 0x0064 | 0x0065 | 0x0063 |
| 0x6504 | 0xFFFF | 0x0064 | 0x0065 | 0x0063 |
| 0x6505 | 0xFFFF | 0x0064 | 0x0065 | 0x0063 |
| 0x6506 | 0xFFFF | 0xFFFF | 0x0047 | 0x0046 |
| 0x6507 | 0xFFFF | 0xFFFF | 0x0047 | 0x0046 |
| 0x6508 | 0xFFFF | 0xFFFF | 0xFFFF | 0x0053 |
| 0x6509 | 0xFFFF | 0xFFFF | 0xFFFF | 0x0059 |
| 0xCE07 | 0xFFFF | 0x006D | 0xFFFF | 0x006C |
| 0xCE0B | 0xFFFF | 0x006D | 0xFFFF | 0x006C |
| 0xCE0F | 0xFFFF | 0x006D | 0xFFFF | 0x006C |
| 0xCE13 | 0xFFFF | 0x006D | 0xFFFF | 0x006C |
| 0xCE14 | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE15 | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE16 | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE18 | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE19 | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE1A | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE1B | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE1C | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE1D | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE1E | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE1F | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE20 | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE21 | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE22 | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE24 | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |
| 0xCE25 | 0xFFFF | 0xFFFF | 0x003E | 0x0072 |
| 0xCE26 | 0xFFFF | 0x0072 | 0xFFFF | 0xFFFF |

<a id="table-farttexteindividuell"></a>
### FARTTEXTEINDIVIDUELL

Dimensions: 119 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | Kein Fehler |
| 0x0001 | Wert zu groß |
| 0x0002 | Wert zu klein |
| 0x0003 | Kein Signal |
| 0x0004 | Wert unplausibel |
| 0x0005 | Computerfehler |
| 0x0006 | Eingangssignalfehler |
| 0x0007 | Ausgangssignalfehler des CE-SG |
| 0x0008 | Eingangssignalfehler an der Stromschleife |
| 0x0009 | Ruhestromverletzung |
| 0x000A | Überspannung |
| 0x000B | zu hoch |
| 0x000C | unterhalb der kritischen Grenze |
| 0x000D | Rohrbruch |
| 0x000E | Boil-Off Druck zu niedrig |
| 0x000F | CRASH erkannt |
| 0x0010 | blockiert |
| 0x0011 | Boil-Off Ansprechdruck zu hoch |
| 0x0012 | Boil-Off Ansprechdruck zu niedrig |
| 0x0013 | Vereisung Stufe 1 |
| 0x0014 | Vereisung Stufe 2 |
| 0x0015 | Vertauschung der Sensoren am Eintritt und Austritt |
| 0x0016 | Fehlerhafte Überfüllsicherung |
| 0x0017 | BSD- Fehler |
| 0x0018 | Parameter-Checksummen von IBS und CE-SG unterscheiden sich |
| 0x0019 | zu niedrig |
| 0x001A | unplausibel |
| 0x001B | Zellenschluss Batterie 1 |
| 0x001C | Zellenschluss Batterie 2 |
| 0x001D | Maximaler Energiedurchsatz überschritten |
| 0x001E | Batterie Tiefentladen |
| 0x001F | Schlechtes Isolationsvakuum am Tank |
| 0x0020 | AD-Wandler Fehler auf Kanal 1 |
| 0x0021 | AD-Wandler Fehler auf Kanal 2 |
| 0x0022 | Strom Über- oder Unterschreitung im angesteuerten Zustand |
| 0x0023 | Strom Über- oder Unterschreitung im nicht angesteuerten Zustand |
| 0x0024 | Widerstandsfehler: Widerstand außerhalb der vorgesehenen Bereichsgrenzen |
| 0x0025 | Plausibilitätsfehler im nicht angesteuerten Zustand des Starter Interlock |
| 0x0026 | Plausibilitätsfehler im angesteuerten Zustand des Starter Interlock |
| 0x0027 | Plausibilitätsfehler Drehzahl Zusatzwasserpumpe |
| 0x0028 | Fehler in der Zusatzwasserpumpe |
| 0x0029 | Spannungsabfall über Diode 1 unplausibel |
| 0x002A | Spannungsabfall über Diode 2 unplausibel |
| 0x002B | Leitungsdruck fällt nach dem Ausschalten des Steuerventils für gasförmigen H2 nicht innerhalb der vorgesehen Zeit |
| 0x002C | Leitungsdruck fällt nach dem Ausschalten des Steuerventils für flüssigen H2 nicht innerhalb der vorgesehen Zeit |
| 0x002D | Leitungsdruck steigt nach dem Einschalten des Steuerventils für gasförmigen H2 nicht innerhalb der vorgesehen Zeit |
| 0x002E | Leitungsdruck steigt nach dem Einschalten des Steuerventils für flüssigen H2 nicht innerhalb der vorgesehen Zeit |
| 0x002F | Passiver Druckverlust |
| 0x0030 | Druck im Druckspeicher unter Minimalwert |
| 0x0031 | Druck über Maximalwert |
| 0x0032 | Fehler beim Druckaufbau Kompressor (Zeitüberschreitung) |
| 0x0033 | Fehler Entlüftung (Zeitüberschreitung) |
| 0x0034 | Fehler beim Spülen der Nebensystemkapsel |
| 0x0035 | Selbsttest TSE fehlgeschlagen |
| 0x0036 | Plausibilitätsfehler Kühlwassersensoren |
| 0x0037 | Fehler bei Boil-Off Überwachung |
| 0x0038 | Oxidator-Temperatur zu hoch oder zu niedrig |
| 0x0039 | über der kritischen Grenze |
| 0x003A | Überhitzungsstufe 2 |
| 0x003B | Überhitzungsstufe 1 |
| 0x003C | Ventil leckt |
| 0x003D | Falsche Protokollinterpretation zwischen CE-SG und TSE |
| 0x003E | Integrität des TSE-Massenwertes ist nicht gewährleistet |
| 0x003F | Berechnung des TSE-Massenwertes nicht möglich |
| 0x0040 | Sensor fehlt / Leitungsunterbrechung |
| 0x0041 | Kurzschluss |
| 0x0042 | Fehlerhafter Sensor (Werte außerhalb des zulässigen Bereichs) |
| 0x0043 | Plausibilitätsfehler gegenüber Referenzsensor |
| 0x0044 | Cross Check Fehler oder Plausibilitätsfehler gegenüber Referenzsensor |
| 0x0045 | Schwerer Fehler |
| 0x0046 | Power Fail |
| 0x0047 | Interner IBS Fehler |
| 0x0048 | H2-Warnung Low-Alarm |
| 0x0049 | H2-Warnung High-Alarm |
| 0x004A | Quittierungsfehler |
| 0x004B | Leichter Sensor Fehler |
| 0x004C | zu niedrig während der Betankung |
| 0x004D | Tankdruckschwelle 1 unterschritten |
| 0x004E | Tankdruckschwelle 2 unterschritten |
| 0x004F | Übertemperatur |
| 0x0050 | Trockenlauf |
| 0x0051 | Falsche Spannung |
| 0x0052 | Defektes Isolationsvakuum an Tankkupplung |
| 0x0053 | Offen blockiert |
| 0x0054 | Defektes Isolationsvakuum am Einfüllrohr |
| 0x0055 | Defektes Isolationsvakuum oder offen blockiertes Befüll- und Entnahmeventil flüssig während H2-Betrieb |
| 0x0056 | Defektes Isolationsvakuum oder offen blockiertes Befüll- und Entnahmeventil flüssig während keine Betankung und kein H2-Betrieb |
| 0x0057 | Zu niedrige Temperatur des Oxidators bei genügend Druck in der Boil-Off Leitung |
| 0x0058 | Ventil undicht |
| 0x0059 | Anzahl Thermoshocks überschritten |
| 0x005A | Pneumatikdruck zu niedrig für Betankung |
| 0x005B | Fehler beim Drucktest |
| 0x005C | Fehler beim gasförmigen Entnahmeventil |
| 0x005D | Fehler beim Motorabsperrventil |
| 0x005E | Fehler am Druckregler |
| 0x005F | Zeitüberschreitung Dichtigkeitstest |
| 0x0060 | Netzwerkmanagement Kommunikationsfehler DME-CESG |
| 0x0061 | Eingangssignalfehler |
| 0x0062 | Computerfehler |
| 0x0063 | Kurzschluss nach Masse |
| 0x0064 | Kurzschluss nach Batteriespannung oder Übertemperatur |
| 0x0065 | Leitungsunterbrechung |
| 0x0066 | Leitungsunterbrechung |
| 0x0067 | Kurzschluss nach Masse |
| 0x0068 | Wert oder Signal außerhalb des spezifizierten Bereichs |
| 0x0069 | Wert oder Signal unplausibel |
| 0x006A | Kurzschluss nach Masse oder Verlust der Versorgungsspannung |
| 0x006B | Botschaftsausfall DI_N |
| 0x006C | Error Passiv |
| 0x006D | Bus Off |
| 0x006E | Dauerhafte Unterkühlung |
| 0x006F | Dauerhafte Überhitzung |
| 0x0070 | Kommunikationsfehler |
| 0x0071 | TSE nicht kalibriert |
| 0x0072 | Timeout (Botschaft in 450ms nicht empfangen) |
| 0x0073 | offen blockiert, oder die Überfüllsicherung springen nicht an |
| 0x0074 | Leitungsunterbrechung oder Kurzschluss nach Masse |
| 0x0075 | Strom Über- oder Unterschreitung im angesteuerten oder nicht angesteuerten Zustand |
| 0xFFFF | unbekannte Fehlerart |

<a id="table-horttexte"></a>
### HORTTEXTE

Dimensions: 1 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0xFFFF | unbekannter Fehlerort |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 8 rows × 2 columns

| ORT | ORTTEXT |
| --- | --- |
| 0x5D0C | Steuergerät, interner Fehler, Kanal 1 |
| 0x5D0D | Steuergerät, interner Fehler, Kanal 2 |
| 0x5D10 | Batterie 1 Ladezustand |
| 0x5D11 | AD-Wandler im CE-SG |
| 0x5D12 | Batterie 2 Ladezustand |
| 0x5D2C | Fehlerrückmeldungen Zusatzwasserpumpe |
| 0x5D2E | Stromschleife für Betankung |
| 0xFFFF | unbekannter Fehlerort |

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
| F_LZ | nein |
| F_UWB_ERW | ja |

<a id="table-iumweltmatrix"></a>
### IUMWELTMATRIX

Dimensions: 7 rows × 5 columns

| ORT | UW1_NR | UW2_NR | UW3_NR | UW4_NR |
| --- | --- | --- | --- | --- |
| 0x5D0C | 0x0066 | 0x0001 | 0xFFFE | 0xFFFE |
| 0x5D0D | 0x0066 | 0x0001 | 0xFFFE | 0xFFFE |
| 0x5D10 | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x5D11 | 0x0066 | 0x0001 | 0xFFFE | 0xFFFE |
| 0x5D12 | 0x0066 | 0x0022 | 0x0023 | 0x0024 |
| 0x5D2C | 0x0063 | 0x005C | 0x005D | 0xFFFE |
| 0x5D2E | 0x0066 | 0x0001 | 0x0064 | 0x0065 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 106 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x0001 | IN_FUTA_P_V | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0002 | IN_FUTA_P_1_CD | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0003 | IN_FUTA_P_2_CD | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0004 | IN_SUPPIPE_P_1_V | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0005 | IN_SUPPIPE_P_2_V | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0006 | IN_SUPPIPE_P_1_CD | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0007 | IN_SUPPIPE_P_2_CD | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0008 | IN_BO_P_V | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x0009 | IN_AMB_P_V | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x000A | IN_AMB_P_CD | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x000B | AIP_ENG_V | bar | high | unsigned int | - | 8 | 65535 | 0 |
| 0x000C | IN_GHY_CL_P_V | bar | high | unsigned int | - | 21 | 65535 | 0 |
| 0x000D | IN_LHY_CL_P_V | bar | high | unsigned int | - | 21 | 65535 | 0 |
| 0x000E | IN_PRS_ACCU_P_V | bar | high | unsigned int | - | 21 | 65535 | 0 |
| 0x000F | IN_OX_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0010 | IN_OX_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0011 | IN_MPVA_IN_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0012 | IN_MPVA_IN_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0013 | IN_MPVA_SP_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0014 | IN_MPVA_SP_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0015 | IN_COL_INL_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0016 | IN_COL_INL_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0017 | IN_COL_EXH_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0018 | IN_COL_EXH_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0019 | IN_COMP_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x001A | IN_COMP_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x001B | IN_HEATEX_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x001C | IN_HEATEX_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x001D | IN_FUT_CLT_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x001E | IN_FUT_CLT_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x001F | IN_VENT_TEMP_CD | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0020 | IN_VENT_TEMP_V | °C | high | unsigned int | - | 900 | 65535 | -100 |
| 0x0021 | DMA_TEMP_V | °C | high | unsigned int | - | 360 | 65535 | -260 |
| 0x0022 | IN_BT_U_1_CD | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0023 | IN_BT_U_2_CD | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0024 | IN_BN_V | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0025 | IN_BN_CD | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0026 | IN_BN_CD_O | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0027 | IN_CR_V | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0028 | IN_CR_CD | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0029 | IN_STRT_ILK_1_CD | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x002A | IN_STRT_ILK_1_V | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x002B | IN_STRT_ILK_2_CD | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x002C | IN_STRT_ILK_2_V | V | high | unsigned int | - | 20 | 65535 | 0 |
| 0x002D | IN_LHY_COV_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x002E | IN_LHY_COV_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x002F | IN_GHY_COV_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0030 | IN_GHY_COV_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0031 | IN_MPVA_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0032 | IN_MPVA_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0033 | IN_ENG_SOV_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0034 | IN_ENG_SOV_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0035 | IN_ADD_ABV_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0036 | IN_ADD_ABV_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0037 | IN_P_ACCU_VA_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0038 | IN_P_ACCU_VA_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x0039 | IN_NSK_FL_VA_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x003A | IN_NSK_FL_VA_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x003B | IN_REG_VA_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x003C | IN_REG_VA_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x003D | IN_FUFF_I_CD | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x003E | IN_FUFF_I_CD_O | A | high | unsigned int | - | 3 | 65535 | 0 |
| 0x003F | IN_FTC_CLO_1_V | mA | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0040 | IN_FTC_CLO_1_CD | mA | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0041 | IN_FTC_CLO_2_V | mA | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0042 | IN_FTC_CLO_2_CD | mA | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0043 | IN_FTC_OPN_V | mA | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0044 | IN_FTC_OPN_CD | mA | high | unsigned int | - | 20 | 65535 | 0 |
| 0x0045 | HS_BOOT_HYC_V | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x0046 | HS_BOOT_HYC_CD | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x0047 | HS_ENG_HYC_V | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x0048 | HS_ENG_HYC_CD | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x0049 | HS_FUTA_CLT_HYC_V | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x004A | HS_FUTA_CLT_HYC_CD | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x004B | HS_PSCMP_HYC_V | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x004C | HS_PSCMP_HYC_CD | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x004D | HS_SCAP_HYC_V | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x004E | HS_SCAP_HYC_CD | % | high | unsigned int | - | 4 | 65535 | 0 |
| 0x004F | WGH_LH2_V | g | high | unsigned int | - | 10000 | 65535 | 0 |
| 0x0050 | R_QVM_T_1_CD | min | high | unsigned int | - | 1 | 1 | 0 |
| 0x0051 | R_QVM_T_2_CD | min | high | unsigned int | - | 1 | 1 | 0 |
| 0x0052 | R_QVM_T_3_CD | min | high | unsigned int | - | 1 | 1 | 0 |
| 0x0053 | R_QVM_T_4_CD | min | high | unsigned int | - | 1 | 1 | 0 |
| 0x0054 | CURR_REF_TIME | min | high | unsigned int | - | 1 | 1 | 0 |
| 0x0055 | CURR_H2_TIME | min | high | unsigned int | - | 1 | 1 | 0 |
| 0x0056 | COSP_HY_AVL_V | kg/h | high | unsigned int | - | 200 | 65535 | 0 |
| 0x0057 | IN_OFI_PR_1_CD | Ohm | high | unsigned int | - | 10000 | 65535 | 0 |
| 0x0058 | IN_OFI_PR_2_CD | Ohm | high | unsigned int | - | 10000 | 65535 | 0 |
| 0x0059 | P_DA | W | high | unsigned int | - | 40 | 65535 | 0 |
| 0x005A | P_BO | W | high | unsigned int | - | 40 | 65535 | 0 |
| 0x005B | P_DA_SV | W | high | unsigned int | - | 40 | 65535 | 0 |
| 0x005C | IN_AUWP_H2_RPM_V | rpm | high | unsigned int | - | 1 | 1 | 0 |
| 0x005D | OUT_AUWP_H2_RPM | rpm | high | unsigned int | - | 1 | 1 | 0 |
| 0x005E | DIAG_HS_BOOT_PARAM | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x005F | DIAG_HS_ENG_PARAM | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0060 | DIAG_HS_FUTA_CLT_PARAM | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0061 | DIAG_HS_PSCMP_PARAM | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0062 | DIAG_HS_SCAP_PARAM | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0063 | BETRIEBSZUST | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0064 | ST_CLC_N_CD | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0065 | ST_CLC_P_CD | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0066 | SYSTEM_TIME | h | high | unsigned int | - | 1 | 1 | 0 |
| 0x0067 | ST_KL_15_V | - | high | unsigned int | - | 1 | 1 | 0 |
| 0x0068 | ST_KL_R_V | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFFFE | Unbenutzte Umweltbedingung | - | high | unsigned int | - | 1 | 1 | 0 |
| 0xFFFF | Unbekannte Umweltbedingung | - | high | unsigned int | - | 1 | 1 | 0 |

<a id="table-iarttyp"></a>
### IARTTYP

Dimensions: 7 rows × 5 columns

| ORT | PLAUS | SIG | MIN | MAX |
| --- | --- | --- | --- | --- |
| 0x5D0C | 0xFFFF | 0xFFFF | 0x0006 | 0x0005 |
| 0x5D0D | 0xFFFF | 0xFFFF | 0x0006 | 0x0005 |
| 0x5D10 | 0xFFFF | 0x001A | 0x0019 | 0xFFFF |
| 0x5D11 | 0xFFFF | 0x0021 | 0x0020 | 0xFFFF |
| 0x5D12 | 0xFFFF | 0x001A | 0x0019 | 0xFFFF |
| 0x5D2C | 0x0051 | 0x0050 | 0x0010 | 0x004F |
| 0x5D2E | 0xFFFF | 0xFFFF | 0x0008 | 0x0069 |

<a id="table-iarttexteindividuell"></a>
### IARTTEXTEINDIVIDUELL

Dimensions: 116 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x0000 | Kein Fehler |
| 0x0001 | Wert zu groß |
| 0x0002 | Wert zu klein |
| 0x0003 | Kein Signal |
| 0x0004 | Wert unplausibel |
| 0x0005 | Computerfehler |
| 0x0006 | Eingangssignalfehler |
| 0x0007 | Ausgangssignalfehler des CE-SG |
| 0x0008 | Eingangssignalfehler an der Stromschleife |
| 0x0009 | Ruhestromverletzung |
| 0x000A | Überspannung |
| 0x000B | zu hoch |
| 0x000C | unterhalb der kritischen Grenze |
| 0x000D | Rohrbruch |
| 0x000E | Boil-Off Druck zu niedrig |
| 0x000F | CRASH erkannt |
| 0x0010 | blockiert |
| 0x0011 | Boil-Off Ansprechdruck zu hoch |
| 0x0012 | Boil-Off Ansprechdruck zu niedrig |
| 0x0013 | Vereisung Stufe 1 |
| 0x0014 | Vereisung Stufe 2 |
| 0x0015 | Vertauschung der Sensoren am Eintritt und Austritt |
| 0x0016 | Fehlerhafte Überfüllsicherung |
| 0x0017 | BSD- Fehler |
| 0x0018 | Parameter-Checksummen von IBS und CE-SG unterscheiden sich |
| 0x0019 | zu niedrig |
| 0x001A | unplausibel |
| 0x001B | Zellenschluss Batterie 1 |
| 0x001C | Zellenschluss Batterie 2 |
| 0x001D | Maximaler Energiedurchsatz überschritten |
| 0x001E | Batterie Tiefentladen |
| 0x001F | Schlechtes Isolationsvakuum am Tank |
| 0x0020 | AD-Wandler Fehler auf Kanal 1 |
| 0x0021 | AD-Wandler Fehler auf Kanal 2 |
| 0x0022 | Strom Über- oder Unterschreitung im angesteuerten Zustand |
| 0x0023 | Strom Über- oder Unterschreitung im nicht angesteuerten Zustand |
| 0x0024 | Widerstandsfehler: Widerstand außerhalb der vorgesehenen Bereichsgrenzen |
| 0x0025 | Plausibilitätsfehler im nicht angesteuerten Zustand des Starter Interlock |
| 0x0026 | Plausibilitätsfehler im angesteuerten Zustand des Starter Interlock |
| 0x0027 | Plausibilitätsfehler Drehzahl Zusatzwasserpumpe |
| 0x0028 | Fehler in der Zusatzwasserpumpe |
| 0x0029 | Spannungsabfall über Diode 1 unplausibel |
| 0x002A | Spannungsabfall über Diode 2 unplausibel |
| 0x002B | Leitungsdruck fällt nach dem Ausschalten des Steuerventils für gasförmigen H2 nicht innerhalb der vorgesehen Zeit |
| 0x002C | Leitungsdruck fällt nach dem Ausschalten des Steuerventils für flüssigen H2 nicht innerhalb der vorgesehen Zeit |
| 0x002D | Leitungsdruck steigt nach dem Einschalten des Steuerventils für gasförmigen H2 nicht innerhalb der vorgesehen Zeit |
| 0x002E | Leitungsdruck steigt nach dem Einschalten des Steuerventils für flüssigen H2 nicht innerhalb der vorgesehen Zeit |
| 0x002F | Passiver Druckverlust |
| 0x0030 | Druck im Druckspeicher unter Minimalwert |
| 0x0031 | Druck über Maximalwert |
| 0x0032 | Fehler beim Druckaufbau Kompressor (Zeitüberschreitung) |
| 0x0033 | Fehler Entlüftung (Zeitüberschreitung) |
| 0x0034 | Fehler beim Spülen der Nebensystemkapsel |
| 0x0035 | Selbsttest TSE fehlgeschlagen |
| 0x0036 | Plausibilitätsfehler Kühlwassersensoren |
| 0x0037 | Fehler bei Boil-Off Überwachung |
| 0x0038 | Oxidator-Temperatur zu hoch oder zu niedrig |
| 0x0039 | über der kritischen Grenze |
| 0x003A | Überhitzungsstufe 2 |
| 0x003B | Überhitzungsstufe 1 |
| 0x003C | Ventil leckt |
| 0x003D | Falsche Protokollinterpretation zwischen CE-SG und TSE |
| 0x003E | Integrität des TSE-Massenwertes ist nicht gewährleistet |
| 0x003F | Berechnung des TSE-Massenwertes nicht möglich |
| 0x0040 | Sensor fehlt / Leitungsunterbrechung |
| 0x0041 | Kurzschluss |
| 0x0042 | Fehlerhafter Sensor (Werte außerhalb des zulässigen Bereichs) |
| 0x0043 | Plausibilitätsfehler gegenüber Referenzsensor |
| 0x0044 | Cross Check Fehler oder Plausibilitätsfehler gegenüber Referenzsensor |
| 0x0045 | Schwerer Fehler |
| 0x0046 | Power Fail |
| 0x0047 | Interner IBS Fehler |
| 0x0048 | H2-Warnung Low-Alarm |
| 0x0049 | H2-Warnung High-Alarm |
| 0x004A | Quittierungsfehler |
| 0x004B | Leichter Sensor Fehler |
| 0x004C | zu niedrig während der Betankung |
| 0x004D | Tankdruckschwelle 1 unterschritten |
| 0x004E | Tankdruckschwelle 2 unterschritten |
| 0x004F | Übertemperatur |
| 0x0050 | Trockenlauf |
| 0x0051 | Falsche Spannung |
| 0x0052 | Defektes Isolationsvakuum an Tankkupplung |
| 0x0053 | Offen blockiert |
| 0x0054 | Defektes Isolationsvakuum |
| 0x0055 | Defektes Isolationsvakuum oder offen blockiertes Befüll- und Entnahmeventil flüssig während H2-Betrieb |
| 0x0056 | Defektes Isolationsvakuum oder offen blockiertes Befüll- und Entnahmeventil flüssig während keine Betankung und kein H2-Betrieb |
| 0x0057 | Zu niedrige Temperatur des Oxidators bei genügend Druck in der Boil-Off Leitung |
| 0x0058 | Ventil undicht |
| 0x0059 | Anzahl Thermoshocks überschritten |
| 0x005A | Pneumatikdruck zu niedrig für Betankung |
| 0x005B | Fehler beim Drucktest |
| 0x005C | Fehler beim gasförmigen Entnahmeventil |
| 0x005D | Fehler beim Motorabsperrventil |
| 0x005E | Fehler am Druckregler |
| 0x005F | Zeitüberschreitung Dichtigkeitstest |
| 0x0060 | Netzwerkmanagement Kommunikationsfehler DME-CESG |
| 0x0061 | Eingangssignalfehler |
| 0x0062 | Computerfehler |
| 0x0063 | Kurzschluss nach Masse |
| 0x0064 | Kurzschluss nach Batteriespannung oder Übertemperatur |
| 0x0065 | Leitungsunterbrechung |
| 0x0066 | Leitungsunterbrechung |
| 0x0067 | Kurzschluss nach Masse |
| 0x0068 | Wert oder Signal außerhalb des spezifizierten Bereichs |
| 0x0069 | Wert oder Signal unplausibel |
| 0x006A | Kurzschluss nach Masse oder Verlust der Versorgungsspannung |
| 0x006B | Botschaftsausfall DI_N |
| 0x006C | Error Passiv |
| 0x006D | Bus Off |
| 0x006E | Dauerhafte Unterkühlung |
| 0x006F | Dauerhafte Überhitzung |
| 0x0070 | Kommunikationsfehler |
| 0x0071 | TSE nicht kalibriert |
| 0x0072 | Timeout (Botschaft in 450ms nicht empfangen) |
| 0xFFFF | unbekannte Fehlerart |
