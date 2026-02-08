# bpcm72.prg

- Jobs: [117](#jobs)
- Tables: [55](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | BPCM (Battery Pack Control Module) |
| ORIGIN | BMW EA-431 MAXIMILIAN_ZETTL |
| REVISION | 1.010 |
| AUTHOR | IAV_INC. EA-423 NAYAN_PATEL, BERATA_GmbH HT_A_2 MAXIMILIAN_ZETT |
| COMMENT | N/A |
| PACKAGE | 1.11 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels UDS  : $22   ReadDataByIdentifier UDS  : $1000 TestStamp Modus: Default
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden. UDS  : $2E   WriteDataByIdentifier UDS  : $1000 TestStamp Modus: Default
- [DIAGNOSE_MODE](#job-diagnose-mode) - SG in bestimmten Diagnosemode bringen UDS  : $10 StartDiagnosticSession Modus: einstellbar mit diesem Job
- [STEUERGERAETE_RESET](#job-steuergeraete-reset) - Harter Reset des Steuergeraets UDS  : $11 EcuReset UDS  : $01 HardReset Modus: Default
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $02 ReadDTCByStatusMask UDS  : $0C StatusMask (Bit2, Bit3) Modus: Default
- [FS_LESEN_DETAIL](#job-fs-lesen-detail) - Fehlerspeicher lesen (einzelner Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $04 reportDTCSnapshotRecordByDTCNumber UDS  : $06 reportDTCExtendedDataRecordByDTCNumber UDS  : $09 reportSeverityInformationOfDTC Modus: Default
- [FS_LOESCHEN](#job-fs-loeschen) - Fehlerspeicher loeschen UDS  : $14 ClearDiagnosticInformation UDS  : $FF DTCHighByte UDS  : $FF DTCMiddleByte UDS  : $FF DTCLowByte Modus: Default
- [IDENT](#job-ident) - Identdaten UDS  : $22   ReadDataByIdentifier UDS  : $3F30 Sub-Parameter SGBD-Index Modus: Default
- [_IDENT_DCX](#job-ident-dcx) - DCX Ident only for development UDS $22 $F1 $xx
- [_UDS_TEST_E72](#job-uds-test-e72) - Test Services Modus: Default
- [_BPCM_ENG_SW_NO](#job-bpcm-eng-sw-no) - TO READ OUT THE SW NUMBER ASSIGNED DURING EACH I-STEP OF DEVELOPMENT THIS SERVICE IS ONLY FOR DEVELOPMENT AND MAY BE REMOVED AT START OF PRODUCTION THIS NUMBER REPRESENTS THE MAJOR, MINOR AND BUILD OF SW RELEASE AS WELL AS THE INDICATES IF THE SW PRESENT IN BPCM IS FOR BMW_SW OR DCX TO VERIFY THE VALIDITY
- [SERIENNUMMER_LESEN](#job-seriennummer-lesen) - Seriennummer des Steuergeraets UDS  : $22   ReadDataByIdentifier UDS  : $F18C Sub-Parameter ECUSerialNumber Modus: Default
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender Informations Feldes Standard Flashjob Modus   : Default
- [ZIF_LESEN](#job-zif-lesen) - Auslesen des Zulieferinfofeldes KWP2000: $22   ReadDataByCommonIdentifier $2503 ProgrammReferenz und KWP2000: $1A   ReadECUIdentification $91   VehicleManufacturerECUHardware*Number oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [ZIF_BACKUP_LESEN](#job-zif-backup-lesen) - Auslesen des Backups des Zulieferinfofeldes ProgrammReferenzBackup         PRGREFB vehicleManufECUHW*NumberBackup VMECUH*NB KWP2000: $22   ReadDataByCommonIdentifier $2500 PRBHW*B oder alternativ KWP2000: $1A ReadECUIdentification $80 ECUIdentificationDataTable Modus  : Default
- [PHYSIKALISCHE_HW_NR_LESEN](#job-physikalische-hw-nr-lesen) - Auslesen der physikalischen Hardwarenummer UDS: $22,$3F Read Data Identifier BMW $41 Hardware Part Number
- [FLASH_PROGRAMMIER_STATUS_LESEN](#job-flash-programmier-status-lesen) - Programmierstatus des SG lesen KWP2000: $31 StartRoutineByLocalIdentifier $0A CheckProgrammingStatus Modus  : Default
- [STATUS_SOC_LESEN](#job-status-soc-lesen) - HIGH VOLTAGE BATTERIE SOC WERT
- [STATUS_CURRENT_LESEN](#job-status-current-lesen) - HIGH VOLT BATTERIE STROM SENSOR WERT negative Stromwerte bedeuten Laden der Batterie POSITIVE Stromwerte bedeuten Entladung der Batterie
- [STATUS_BUSVOLT_CALCULATE_LESEN](#job-status-busvolt-calculate-lesen) - SUMME der 26 MODUL SPANNUNGEN ALS HV-BUS SPANNUNG LESEN
- [STATUS_BUS_VOLT_LESEN](#job-status-bus-volt-lesen) - HV BUS SPANNUNG Wert
- [STATUS_BUSVOLT_SOURCE_LESEN](#job-status-busvolt-source-lesen) - QUELLE FUER HV BUS SPANNUNG Wert
- [STATUS_PACK_VOLT_LESEN](#job-status-pack-volt-lesen) - PACK SPANNUNG SENSOR Wert
- [STATUS_PACK_VOLT_SOURCE_LESEN](#job-status-pack-volt-source-lesen) - QUELLE FUER PACK SPANNUNG Wert
- [STATUS_PWR_CHRG_LT_LESEN](#job-status-pwr-chrg-lt-lesen) - Lang Zeit 10s LADELEISTUNGS LIMIT
- [STATUS_PWR_CHRG_ST_LESEN](#job-status-pwr-chrg-st-lesen) - Kurz Zeit 2s LADELEISTUNGS LIMIT
- [STATUS_PWR_DISCHRG_LT_LESEN](#job-status-pwr-dischrg-lt-lesen) - Lang Zeit 10s ENTLADELEISTUNGS LIMIT
- [STATUS_PWR_DISCHRG_ST_LESEN](#job-status-pwr-dischrg-st-lesen) - Kurz Zeit 2s ENTLADELEISTUNGS LIMIT
- [STATUS_MAX_MODVOLT_LESEN](#job-status-max-modvolt-lesen) - MAXIMALE SPANNUNG ALLER 26 MODUL SPANNUNGSENSOREN
- [STATUS_MIN_MODULSPANNUNG_LESEN](#job-status-min-modulspannung-lesen) - MINIMALE SPANNUNG ALLER 26 MODUL SPANNUNGSENSOREN
- [STATUS_12V_FEED2CONTROLLER_LESEN](#job-status-12v-feed2controller-lesen) - WERT 12V Versorgungsspannung BPCM LESEN
- [STATUS_12V_FEED2PUMP_LESEN](#job-status-12v-feed2pump-lesen) - WERT 12V Versorgungsspannung BATTERIE KUEHLMITTEL PUMPE
- [STATUS_12V_FEED2CNTCR_LESEN](#job-status-12v-feed2cntcr-lesen) - WERT 12V Versorgungsspannung HIGH VOLTAGE BATTERIE PACK SCHUETZE ALLE SCHUETZE WERDEN AUS DER SELBEN QUELLE VERSORGT
- [STATUS_MAX_MODTEMP_LESEN](#job-status-max-modtemp-lesen) - MAXIMALE TEMPERATUR DER 4 MODUL SENSOREN LESEN
- [STATUS_MIN_MODTEMP_LESEN](#job-status-min-modtemp-lesen) - MINIMALE TEMPERATUR DER 4 MODUL SENSOREN LESEN
- [STATUS_HV_BPCM_STATE_LESEN](#job-status-hv-bpcm-state-lesen) - RESULT: TRUE-&gt;JA  FALSE-&gt;NEIN GRUND FUER VERHINDERUNG ODER ABBRUCH DER vORLADEPROZEDUR
- [STATUS_HVILCURR_RETURN_LESEN](#job-status-hvilcurr-return-lesen) - WERT HVIL RUECKKEHRSTROM IN mA
- [STATUS_COOLANT_IN_TEMP_LESEN](#job-status-coolant-in-temp-lesen) - KUEHLMITTEL INLET TEMPERATUR
- [STATUS_COOLANT_OUT_TEMP_LESEN](#job-status-coolant-out-temp-lesen) - KUEHLMITTEL OUTLET TEMPERATUR
- [STATUS_ISOLATION_RESI_LESEN](#job-status-isolation-resi-lesen) - ISOLATIONS WIDERSTANDSWERTE MIT OFFENEN UND GESCHLOSSENEN SCHUETZEN UND FUER POSITVEN UND NEGATIVEN HV_BUS
- [STATUS_ISOLATION_STATE_LESEN](#job-status-isolation-state-lesen) - ISOLATION TEST RESULT
- [STATUS_CNCTR_PWM_CMD_LESEN](#job-status-cnctr-pwm-cmd-lesen) - PEB CONTACTOR COMMAND Wert IN %PWM
- [STATUS_COOL_PUMP_SPEED_LESEN](#job-status-cool-pump-speed-lesen) - KUEHLMITTEL Pumpe Geschwindigkeit
- [STATUS_PRECHARGE_INHIBIT_TIME_LESEN](#job-status-precharge-inhibit-time-lesen) - Verbleibende Zeit in der die Vorladung verboten ist max. 30min
- [STATUS_4MODULES_TEMP_LESEN](#job-status-4modules-temp-lesen) - Temperaturwerte ALLER 4 ODER EINZELNER MODULTEMPERATURSENSOREN
- [STATUS_26_MODULES_VOLT_LESEN](#job-status-26-modules-volt-lesen) - Spannungswerte ALLER 26 ODER EINZELNER MODULSPANNUNGSSENSOREN
- [STATUS_SERVICE_DISCONNECT_LESEN](#job-status-service-disconnect-lesen) - MELDET DEN AKTUELLEN ZUSTAND DES SERVICE SCHALTERS 0 -&gt; GESCHLOSSEN ODER 1 -&gt; OFFEN ODER 2 -&gt; GESCHLOSSEN & SICHERUNG KAPUTT ODER 3 -&gt; UNBEKANNT
- [STATUS_HVIL_LESEN](#job-status-hvil-lesen) - MELDET DEN AKTUELLEN ZUSTAND DES HVIL, HOCHVOLTKONTAKTUEBERWACHUNG 0 -&gt; NICHT AKTIV, 1 -&gt; FEHLERFREI,2 -&gt; FEHLER ODER 3 -&gt; UNGUELTIG
- [STATUS_REASON_CNCTR_NOT_CLOSE_WHEN_CMND_LESEN](#job-status-reason-cnctr-not-close-when-cmnd-lesen) - Gespeicherte & momentan anliegende Fehler die das Schliesen der Schuetze verhindern STORED: Gespeicherte Fehler sind aus vorangegangenen Zyklen PRESENT: momentan anliegende Fehler sind aus dem momentanen Zyklus
- [STATUS_REASONS_CNCTR_OPENED_LESEN](#job-status-reasons-cnctr-opened-lesen) - Gespeicherte & momentan anliegende Gruende fuer das Oeffnen der Schuetze STORED: Gespeicherte Fehler sind aus vorangegangenen Zyklen PRESENT: momentan anliegende Fehler sind aus dem momentanen Zyklus
- [STATUS_ACTIVE_DISCHARGE_LESEN](#job-status-active-discharge-lesen) - Status der der Aktiven Entladung beim letzen Abschalten des HV-BUS
- [STATUS_BATTERY_RESI_LESEN](#job-status-battery-resi-lesen) - Wert HV Batterie Innenwiderstand
- [STATUS_HVBP_CNTCR_STATE_LESEN](#job-status-hvbp-cntcr-state-lesen) - Zustand HIGH VOLTAGE Batterie Schuetze
- [STATUS_CAN_CNTCR_CMND_LESEN](#job-status-can-cntcr-cmnd-lesen) - Zustand PEB CONTACTOR COMMAND von HCP VIA CAN BUS
- [STATUS_UH_SOC_HISTOGRAM_LESEN](#job-status-uh-soc-histogram-lesen) - Nutzung-Historie fuer die Ladezustandwerte wandert in verschiedene Intervalle/Schlitze Waehrend der Schuetzen geschlossen sind, erfasst das BPCM ein Snapshot ueber der SOC-Historie. Am Ende aller 10 Sekunden-Interval (Waehrend der Schuetzen geschlossen sind), der richtige wird auf Basis der laufenden SOC inkrementiert. Die Absicht ist ein Snaptshot vom SOC aller 10 Sekunden aufzuzeichnen. SOC Intervalle: 1-&gt; 0~15.9%, 2-&gt; 16.0~30.9%, 3-&gt; 31.0~40.9%, 4-&gt; 41.0~51.9%, 5-&gt; 52.0~60.9%, 6-&gt; 61.0~68.9% SOC Intervalle: 7-&gt; 69.0~80.9%, 8-&gt; 81.0~90.9%, 9-&gt; 91.0~100%
- [STATUS_UH_HIGH_VOLT_EXCEEDED_LESEN](#job-status-uh-high-volt-exceeded-lesen) - Nutzung-Historie fuer die gesamte Sekunden, wo die Pack- und Modulspannung die Min und MAX- Grenzwerte ueberschreitet das maximale Limit fuer Pack-Spannung ist 419V & das minimale Limit fuer Pack-Spannung ist 244V das maximale Limit fuer Modulspannung ist 16.5V & das minimale Limit fuer Modulspannung ist 9V
- [STATUS_UH_MOD_VOLT_DIFF_HISTOGRAM_LESEN](#job-status-uh-mod-volt-diff-histogram-lesen) - Nutzung-Historie fuer wieviel mal die Differenz der Modulspannung in einem bestimmten Bereich oder Intervall geht
- [STATUS_UH_MAX_MOD_VLT_HISTOGRAM_LESEN](#job-status-uh-max-mod-vlt-histogram-lesen) - Nutzung-Historie fuer wieviel mal das maximale Modulspannungswert in einem bestimmten Bereich geht Das BPCM erfasst waehrend seines Betriebes die Historie der maximale Modulspannung referenziert auf die "VLID". Das BPCM erfasst die maximale Modulspannung und Modeltemperatur im Zusammenhang zur Modulspannung über 10 Sekunden Intervall Am Ende der 10 Sekunden VLID wird berechnet und der richtige BIN wird auf Basis der maximale Modulespannung über 10 Sekunden-Intervall inkrementiert wenn MAXMODTEMP &lt; 25°C, VLID = 16.25V / wenn MAXMODTEMP &gt;= 25°C, VLID = 16.723 - 0.0137 * MAXMODTEMP - 0.00020833 * MAXMODTEMP * MAXMODTEMP wenn es ein Fehler in der Sensor-Temperatur gibt , VLID = 16.25V BIN Beschreibung: Intervall 1: &lt; VLID, Intervall 2: VLID TO VLID+0.2, Intervall 3: &gt; VLID+0.2 Z.B.: hier ist ein Liste von Werten über 10 Sekunden- Bereich: MAX MOD VOLT | MAX MOD TEMP 16.0V        |  20.5°C 16.1V        |  20°C 16.2V        |  20°C 16.3V        |  20°C Die von der VLID-Kalkualation benutzte Temperatur von 20°C wird mit 16.3V verglichen, um den Bereich zu bestimmen.
- [STATUS_UH_MIN_MOD_VLT_HISTOGRAM_LESEN](#job-status-uh-min-mod-vlt-histogram-lesen) - Nutzung-Historie fuer wieviel mal das minimale Modulspannungswert in einem bestimmten Bereich geht MIN MOD Spannung Intervall: Intervall 1: 10.0~20.0V, Intervall 2: 9.0~9.999V, Intervall 3: 8.0~8.999V, Intervall 4: 0~7.999V
- [STATUS_UH_HVBP_VOLTS_HISTOGRAM_LESEN](#job-status-uh-hvbp-volts-histogram-lesen) - Nutzung-Historie fuer wieviel mal das HVBP-spannung in einem verschiedenen Bereich geht Intervall 1: &lt;200V, Intervall 2: 200~220V, Intervall 3: 220~240, Intervall 4: 240~260V, Intervall 5: 260~280V,  Intervall 6: 280~300A Intervall 7: 300~320V, Intervall 8: 320~340V,  Intervall 9: 340~360V,  Intervall 10: 360~380V,  Intervall 11: 380~400A,	 Intervall 12: &gt; 400A
- [STATUS_UH_CURRENT_HISTOGRAM_LESEN](#job-status-uh-current-histogram-lesen) - Nutzung-Historie fuer wieviel mal der Strom in einem verschiedenen Bereich geht Intervall 1: &lt;-200A, Intervall 2: -200~-120A, Intervall 3: -120~-60A, Intervall 4: -60~-30A, Intervall 5: -30~-10A,  Intervall 6: -10~0A Intervall 7: 0~10A, Intervall 8: 10~30A,  Intervall 9: 30~60A,  Intervall 10: 60~120A,  Intervall 11: 120~200A,	 Intervall 12: &gt; 200A
- [STATUS_UH_TEMPERATURE_HISTOGRAM_LESEN](#job-status-uh-temperature-histogram-lesen) - Nutzung-Historie fuer wieviel mal die HVBP-Temperatur in einem verschiedenen Bereich geht Intervall 1: -40~-5 C, Intervall 2: -4.9~15 C, Intervall 3: 15.1~30 C, Intervall 4: 30.1~35 C, Intervall 5: 35.1~40 C Intervall 6: 40.1~45 C, Intervall 7: 45.1~50 C, Intervall 8: 50.1~60 C, Intervall 9: 60.1~65 C, Intervall 10: 65.1~75 C, Intervall 11: 75.1~85 C
- [STATUS_UH_MOD_TEMP_DIFF_HISTOGRAM_LESEN](#job-status-uh-mod-temp-diff-histogram-lesen) - Nutzung-Historie fuer wieviel mal die HVBP-Temperatur in einem verschiedenen Bereich geht Modul-Temperatur-Differenz  = MAX MODULE TEMP - MIN MODULE TEMP Intervall 1: 0~3 C, Intervall 2: 3.1~6 C, Intervall 3: 6.1~10 C, Intervall 4: 10.1~125 C
- [STATUS_UH_HVBP_COOLANT_IN_TEMP_HISTOGRAM_LESEN](#job-status-uh-hvbp-coolant-in-temp-histogram-lesen) - Nutzung-Historie fuer wieviel mal das HVBP-Kuehlmitteleinlass in einem verschiedenen Temperaturbereich geht Intervall 1: &lt; 0 C, Intervall 2: 0.10~20 C, Intervall 3: 20.1~30 C, Intervall 4: 30.1~45 C, Intervall 5: &gt; 45 C
- [STATUS_UH_HVBP_COOLANT_OUT_TEMP_HISTOGRAM_LESEN](#job-status-uh-hvbp-coolant-out-temp-histogram-lesen) - Nutzung-Historie fuer wieviel mal das HVBP-Kuehlmittelauslass in einem verschiedenen Temperaturbereich geht Intervall 1: &lt; 10 C, Intervall 2: 10.1~30 C, Intervall 3: 30.1~40 C, Intervall 4: 40.1~55.0 C, Intervall 5: &gt; 55.0 C
- [STATUS_UH_MOD_COOLANT_TEMP_DELTA_HISTOGRAM_LESEN](#job-status-uh-mod-coolant-temp-delta-histogram-lesen) - Nutzung-Historie fuer wieviel mal das HVBP-Modul und die Kuehlmittel-Einlasstemperaturdifferenz in einem verschiedenen Bereich geht Intervall 1: -40~-30 C, Intervall 2: -29.9~-25 C, Intervall 3: -24.9~20.0 C, Intervall 4: -19.90~-15 C, Intervall 5: -14.9~-0.1 C Intervall 6: 0~15 C, Intervall 7: 15.1~20 C, Intervall 8: 20.1~25 C, Intervall 9: 25.1~30 C, Intervall 10: 30.1~40 C, Intervall 11: &gt; 40 C
- [STATUS_UH_ISOLATION_RESI_HISTOGRAM_LESEN](#job-status-uh-isolation-resi-histogram-lesen) - Nutzung-Historie fuer den Isolationswiderstandwert, der in verschiedenen Widerstandsbereiche/Intervalle geht Intervall 1: &lt; 250 kOHMS, Intervall 2: 250~499 kOHMS, Intervall 3: 500~749 kOHMS, Intervall 4: 750~999 kOHMS, Intervall 5: &gt; 999 kOHMS
- [STATUS_LIFETIME_CNCTR_CLOSES_LESEN](#job-status-lifetime-cnctr-closes-lesen) - Nutzung-Historie fuer wieviel mal während der Lebensdauer der Hochvolt-Batterie, die Schuetzen geschlossen waren
- [STATUS_LIFETIME_12V_LOSS_LESEN](#job-status-lifetime-12v-loss-lesen) - Nutzung-Historie fuer wieviel mal ein Ausfall der 12v Spannung zum Kontroller waehrend der Lebensdauer geschah Die Bedeutung vom Zaehler ist zu bestimmen, wie oft während der Lebensdauer des FZGes Die 12 Volt Spannung mit geschlossenen Schuetzen oder ohne korrekten Auschaltmechanismus aus Grund eines zufaelligen 12v Ausfall verloren war
- [STATUS_LIFETIME_MIN_OCV_LESEN](#job-status-lifetime-min-ocv-lesen) - die minimael erfasste Leerlaufspannung der Batterie waehrend der Lebensdauer Das BPCM speichert die minimale Leerlaufpannung der Batterie-Pack. die Leerlaufspannung (OCV) wird beim Startup bevor die Schuetzen geschlossen sind ein mal erfasst. wenn dieser Wert kleiner als der gespeicherten Wert ist, wird er als neuen minimalen Leerlauf-Pack-Spannung ueberschrieben.
- [STATUS_LIFETIME_CNCTR_OPEN_REQ_LESEN](#job-status-lifetime-cnctr-open-req-lesen) - Nutzung-Historie fuer wie oft der "Open Request" für die Schuetzen waehrend der Lebensdauer vom BPCM gesetzt sind Jedes mal wenn das BPCM vom HCP verlangt, die Schuetzen zu oeffnen, diese Datenspeicherung wird inkrementiert. Z.B: das BPCM feststellt, dass das FZG. die Schuetzen oeffnen soll und daher wird das BIT auf CAN gesetzt für die "OPEN REquest" -Bedingung. diese Datenspeicherung wird nur einmal inkrementiert. Es ist kein wiederholtes Inkrement im CAN-Signal.
- [STATUS_LIFETIME_PRECHARGE_FAILS_LESEN](#job-status-lifetime-precharge-fails-lesen) - Nutzung-Historie fuer wie oft die Aufladuprozedur waehrend der Lebensdauer fehlgeschlagen war
- [STATUS_TOTAL_OEPRATION_TIME_LESEN](#job-status-total-oepration-time-lesen) - Nutzung Historie fuer wieviele Operationen der Batterie Pack waehrend eines Klemmenwechsels akkumuliert waren Das BPCM speichert die gesammte akkumulierte Zeit, in der er im Betrieb war, ab der Zeit wo der Kontroller geweckt ist bis er einschlaeft
- [STATUS_TOTAL_CNCTR_CLOSING_TIME_LESEN](#job-status-total-cnctr-closing-time-lesen) - Nutzung-Historie fuer wieviel mal während der Lebensdauer der Hochvolt-Batterie, die Schuetzen geschlossen waren
- [STATUS_CUMULATIVE_CHARGE_AMP_HOURS_LESEN](#job-status-cumulative-charge-amp-hours-lesen) - Total akkumulierter Wert der Batterieladung seit der ersten Nutzung RESOLUTION  1 Ampere/Stunde
- [STATUS_CUMULATIVE_DISCHARGE_AMP_HOURS_LESEN](#job-status-cumulative-discharge-amp-hours-lesen) - Total akkumulierter Wert der Batterieentladung seit der ersten Nutzung RESOLUTION 1 Ampere/Stunde
- [STATUS_LIFETIME_CNCTR_OPENS_LESEN](#job-status-lifetime-cnctr-opens-lesen) - Nutzung-Historie fuer wieviel mal während der Lebensdauer der Hochvolt-Batterie, die Schuetzen offen waren Auch die Nutzung-Historie für wieviel der Lebensdauer der Batterie, die Schuetzen offen waren unter "Impending-Open" Bedingung und Nutzung-Historie fuer wieviel mal waren die schuetzen offen unter hoehen Strombelastung waehrend Lebensdauer Jedes mal wenn die Schuetzen aus irgend ein Grund offen sind, wenn der absolute Wert (Plus oder minus) des Stroms grosser als 5 Ampere
- [STATUS_UH_BAT_RESI_HISTOGRAM_LESEN](#job-status-uh-bat-resi-histogram-lesen) - Nutzung-Historie fuer wieviel mal der Batteriewiderstand in verschiedenen Widerstandbereiche/Intervalle geht Intervall 1: 0-100 mOhms, Intervall 2: 101-500 mOhms, Intervall 3: 501-1000 mOhms, Intervall 4: 1001-1500 mOhms, Intervall 5: 1501-2000 mOhms Intervall 6: 2001-2500 mOhms, Intervall 7: 2501-3000 mOhms, Intervall 8: 3001-3500 mOhms, Intervall 9: 3501-4000 mOhms Intervall 10: 4001-4500 mOhms, Intervall 11: 4501-5000 mOhms
- [STATUS_SOC_5DAY_HISTORY](#job-status-soc-5day-history) - Ladezustand-Historie mit STAT_AMPRH_CHG_WERT Integrationswerte in der letzten 6 Tagen ab heute das Ziel dieser gespeicherten Daten und der Ladenzustand-Historie am Tag X, ist eine Hilfe für die Service, um festzustellen was am Batterie in den letzten 5 Betriebstagen geschah. die Ladezustandswerte und die Delta der Amp/Stunde (Ladung und Entladung) sind Snapschuesse an einem bestimmten Tag. Der Ladezustand bei Klemme 30, Ampere/Stunden (Ladung und Entladung) - Delta-Wert vom letzten Betriebstag
- [STATUS_UH_HVBP_COOLANT_TEMP_DELTA_HISTOGRAM_LESEN](#job-status-uh-hvbp-coolant-temp-delta-histogram-lesen) - Nutzung-Historie fuer wieviel mal die Temperaturdiffirenz für das HVBP-Kuehlmittel-Einlass und Auslass in einem verschiedenen Temperaturbereich geht Intervall 1: &lt; 0 C, Intervall 2: 0~1 C, Intervall 3: 1~2 C, Intervall 4: 2~3 C, Intervall 5: 3~4 C Intervall 6: 4~5 C, Intervall 7: 5~6 C, Intervall 8: 6~7 C, Intervall 9: 7~9 C, Intervall 10: 9~11 C, Intervall 11: 11~13 C Intervall 12: 13~15 c, Intervall 13: &gt; 15 C
- [STATUS_WELD_CHECK_LESEN](#job-status-weld-check-lesen) - Ergebnisse vom Schweiss-Check -Ablauf für das Hochvolt Batterie Pack (HVBP) zeigt, ob eine oder beide Hochvoltleitungen der Schuetze(n) verschweisst ist (sind)
- [STATUS_OPEN_CABLE_LESEN](#job-status-open-cable-lesen) - TO READ OUT THE OPEN CABLE DETECTION TEST RESULT AND THE OPEN CABLE DETECTION CIRCUIT CHECK RESULT
- [STATUS_BATT_CHANGE_ODOMETER](#job-status-batt-change-odometer) - Fzg.- ODOMETER-Wert vom letzten Batteriewechsel auslesen
- [_STATUS_FAULT_CHECK_LESEN](#job-status-fault-check-lesen) - SHOWS THE STATUS OF DIFFERENT FAULT CHECK AND REMEDIAL ACTION FUNCTIONALITIES THAT IF THE FUNCTIONALITIES IS ENABLED OR DISABLED
- [_STATUS_WAKE_UP_SIGNALS_LESEN](#job-status-wake-up-signals-lesen) - SHOWS THE STATUS OF WAKE UP SIGNALS FOR BPCM - HYBRID ACCESSORY AND HS COMMUNICATION ENABLE
- [STATUS_CONTACTOR_CLOSURE_ENABLE_LESEN](#job-status-contactor-closure-enable-lesen) - Auslesen von Wert des Schuetze-Schliessen Aktivierungsbits geschrieben von "STEUERN_CONTACTOR_CLOSURE_ENABLE" JOB
- [STEUERN_CONTACTOR_CLOSURE_ENABLE](#job-steuern-contactor-closure-enable) - Bit wird gesetzt oder nicht gesetzt, um die Schuetze-Schliessen zu aktivieren oder deaktivieren Bei Deaktivierung des Schutzen-Scliessens bewirkt, dass die Schuetzen sich nicht schliessen mit dem Befehl von HCP bis das Schutzen-Schliessen aktiviert wird Warnung -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden
- [STATUS_PUMP_ENABLE_LESEN](#job-status-pump-enable-lesen) - Auslesen von Wert des Schuetze-Schliessen Aktivierungsbits geschrieben von "STEUERN_PUMP_ENABLE" JOB
- [STEUERN_PUMP_ENABLE](#job-steuern-pump-enable) - Bit wird gesetzt, um die Pumpe zu aktivieren bzw. deaktivieren Deaktivierung der Pumpen-Kontrolle bewirkt, dass die Pumpe nicht laufen wird Mit internen BPCM-Logik oder bei Ueberschreibung des Befehls vom HCP oder bei Pumpen-Ansteuerung SGBD JOB Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden
- [STEUERN_COOL_PUMP](#job-steuern-cool-pump) - Dieser Job dient den Betrieb von Hochvolt-Batterie Pack-Kuehlmittel PUMPE benutzt extern das das Diagnose-Tool WARNUNG -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden
- [STEUERN_COOL_PUMP_RETURN_CONTROL](#job-steuern-cool-pump-return-control) - Die Kontrolle wiederzubekommen nach Durchfuehrung des	 "STEUERN_COOL_PUMP" JOB Warnung -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden
- [STATUS_COOL_PUMP_LESEN](#job-status-cool-pump-lesen) - Das BPCM sendet diese Ergebnisse und jede FAULT CODES waehrend der Zeit der Durchfuehrung von "PUMP Control" falls angefordert durch STEUERN JOB
- [STEUERN_BATT_CHANGE_ODOMETER](#job-steuern-batt-change-odometer) - TO ENTER THE VEHICLE ODOMETER VALUE AT EVERY BATTERY CHANGE
- [STEUERN_ISOL_TEST](#job-steuern-isol-test) - Starten des Isolationstests durch das Service-Tool Warnung -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden
- [STEUERN_ISOL_TEST_RETURN_CONTROL](#job-steuern-isol-test-return-control) - Die Kontrolle wiederzubekommen nach Durchfuehrung von "STEUERN_ISOL_TEST" JOB Warnung -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden
- [STATUS_ISOL_TEST_LESEN](#job-status-isol-test-lesen) - BPCM sendet diese Resultate und Fault-CODES waehrend Ausfuehrung von ISOLATION TEST aufgefordert durch "STEUERN" JOB
- [STEUERN_CLEAR_PUMP_DRYRUN_OFF](#job-steuern-clear-pump-dryrun-off) - RESET die Pumpen-Trockenlauf SWITCH OFF FLAG Warnung -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden
- [STEUERN_CLEAR_DRYRUN_OFF_RETURN_CONTROL](#job-steuern-clear-dryrun-off-return-control) - Die Kontrolle wiederzubekommen nach Durchfuehrung von "STEUERN_CLEAR_DRYRUN_OFF" JOB Warnung -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden
- [STATUS_CLEAR_DRYRUN_OFF_LESEN](#job-status-clear-dryrun-off-lesen) - BPCM sendet diese Resultate und Fault-CODES waehrend Ausfuehrung von CLEAR PUMP Trockenlauf SWITCH OFF aufgefordert durch "STEUERN" JOB
- [_STEUERN_FAULT_CHECK_DISABLER](#job-steuern-fault-check-disabler) - TO ENABLE OR DISABLE DIFFERENT FAULT CHECK TESTS THIS INCLUDES THE FAULT CHECK TESTS OF ISOLATION DETECTION WITH CLOSED CONTACTORS, OPEN CABLE DETECTION, OPEN CABLE DETECTION CIRCUIT CHECK AND WELD CHECK & ACTIVE DISCHARGE TEST
- [_BSE_INIT_STATES](#job-bse-init-states) - BSE INITIALIZATION PARAMETERS
- [_BSE_BPCM_INPUT](#job-bse-bpcm-input) - BSE INPUTS FROM BPCM SW, MAINLY THE SENSOR VALUES
- [_BSE_BSEC_DATA](#job-bse-bsec-data) - None
- [_BSE_EEPROM_DATA_01](#job-bse-eeprom-data-01) - EEPROM DATA - INPUT TO BSE
- [_BSE_EEPROM_DATA_02](#job-bse-eeprom-data-02) - EEPROM DATA - INPUT TO BSE
- [_BSE_API_DATA_01](#job-bse-api-data-01) - BSE API OUTPUTS
- [_BSE_API_DATA_02](#job-bse-api-data-02) - BSE API OUTPUTS
- [_BSE_API_DATA_03](#job-bse-api-data-03) - BSE API OUTPUTS
- [_WRITE_SOC_OLD](#job-write-soc-old) - TO OVERWRITE THE OLD SOC VALUE STORED IN THE EEPROM
- [_WRITE_AMPHR_CHARGE](#job-write-amphr-charge) - TO OVERWRITE THE AMP-HR CHARGE VALUE STORED IN THE EEPROM
- [_WRITE_AMPHR_DISCHARGE](#job-write-amphr-discharge) - TO OVERWRITE THE AMP-HR CHARGE VALUE STORED IN THE EEPROM
- [_STEUERN_LOAD_CHECK_ENABLER](#job-steuern-load-check-enabler) - TO ENABLE OR DISABLE LOAD CHECK AND SHORTED BUS DETECTION FUNCTIONALITY
- [_STATUS_LOAD_CHECK_ENABLER](#job-status-load-check-enabler) - TO READ OUT THE LOAD CHECK AND SHORTED BUS DETECTION ENABLER BIT
- [_SERVICE_CAN_ENABLER](#job-service-can-enabler) - TO ENABLE OR DISABLE SERVICE CAN COMMUNICATION
- [_STATUS_SERVICE_CAN_ENABLER](#job-status-service-can-enabler) - TO READ OUT THE LOAD CHECK AND SHORTED BUS DETECTION ENABLER BIT

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

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher lesen (alle Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $02 ReadDTCByStatusMask UDS  : $0C StatusMask (Bit2, Bit3) Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-fs-lesen-detail"></a>
### FS_LESEN_DETAIL

Fehlerspeicher lesen (einzelner Fehler / Ort und Art) UDS  : $19 ReadDTCInformation UDS  : $04 reportDTCSnapshotRecordByDTCNumber UDS  : $06 reportDTCExtendedDataRecordByDTCNumber UDS  : $09 reportSeverityInformationOfDTC Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Fehlerspeicher loeschen UDS  : $14 ClearDiagnosticInformation UDS  : $FF DTCHighByte UDS  : $FF DTCMiddleByte UDS  : $FF DTCLowByte Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-ident"></a>
### IDENT

Identdaten UDS  : $22   ReadDataByIdentifier UDS  : $3F30 Sub-Parameter SGBD-Index Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardware-Versionsindex (= Hardware Version Number Byte #3) |
| ID_COD_INDEX | int | Codier-Index Dummy-Wert |
| ID_DIAG_INDEX | long | Index zur Erkennung der SG-Variante Hybrid Generation 1.0 liefert nur 2 Antwort-Byte |
| ID_VAR_INDEX | int | Varianten-Index Dummy-Wert |
| ID_DATUM_JAHR | int | Herstelldatum (Jahr) |
| ID_DATUM_MONAT | int | Herstelldatum (Monat) |
| ID_DATUM_TAG | int | Herstelldatum (Tag) Dummy-Wert |
| ID_DATUM | string | Herstelldatum (TT.MM.JJJJ) |
| ID_LIEF_NR | int | Lieferanten-Nummer |
| ID_LIEF_TEXT | string | Lieferanten-Text table Lieferanten buffer_2 |
| ID_SW_NR_MCV | string | Softwarenummer (message catalogue version) Dummy-Wert |
| ID_SW_NR_FSV | string | Softwarenummer (functional software version) |
| ID_SW_NR_OSV | string | Softwarenummer (operating system version) |
| ID_SW_NR_RES | string | Softwarenummer (reserved - currently unused) Dummy-Wert |
| ID_SG_ADR | long | Steuergeraeteadresse |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |
| _REQUEST2 | binary | Hex-Auftrag an SG |
| _RESPONSE2 | binary | Hex-Antwort von SG |
| _REQUEST3 | binary | Hex-Auftrag an SG |
| _RESPONSE3 | binary | Hex-Antwort von SG |
| _REQUEST4 | binary | Hex-Auftrag an SG |
| _RESPONSE4 | binary | Hex-Antwort von SG |
| _REQUEST5 | binary | Hex-Auftrag an SG |
| _RESPONSE5 | binary | Hex-Antwort von SG |
| _REQUEST6 | binary | Hex-Auftrag an SG |
| _RESPONSE6 | binary | Hex-Antwort von SG |

<a id="job-ident-dcx"></a>
### _IDENT_DCX

DCX Ident only for development UDS $22 $F1 $xx

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _DCX_VERSION | unsigned char | service $22 $F1 $00 aktuelle Diagnose -Version |
| _DCX_VARIANT | unsigned char | service $22 $F1 $00 Steuergeraet Identifikation |
| _DCX_ECU_MODE | unsigned char | service $22 $F1 $00 zeigt, ob das Steuergeraet im Applikationsmode (=0) oder im Boot-Mode (=1) laeuft |
| _DCX_GATEWAY | unsigned char | service $22 $F1 $00 zeigt, ob das Steuergeraet ein Gateway (=0) oder nicht (=1) ist |
| _DCX_SESSION | unsigned char | service $22 $F1 $00 Sitzung type |
| _DCX_HW_PART_NO | string | service $22 $F1 $11 HW part NUMMER |
| _DCX_SW_PART_NO_BLK_0 | string | UDS $22 $F1 $21 SW part NUMMER logical block #0 |
| _DCX_SW_PART_NO_BLK_1 | string | UDS $22 $F1 $21 SW part NUMMER logical block #1 |
| _DCX_ASSY_NO | string | UDS $22 $F1 $31 assembly NUMMER |
| _DCX_HW_VERSION | unsigned char | UDS $22 $F1 $50 HW patchlevel |
| _DCX_HW_WEEK | unsigned char | UDS $22 $F1 $50 HW Woche |
| _DCX_HW_YEAR | unsigned char | UDS $22 $F1 $50 HW Jahr |
| _DCX_SW_VERSION_BLK_0 | unsigned char | UDS $22 $F1 $51 SW patch level logical block #0 |
| _DCX_SW_WEEK_BLK_0 | unsigned char | UDS $22 $F1 $51 SW Woche logical block #0 |
| _DCX_SW_YEAR_BLK_0 | unsigned char | UDS $22 $F1 $51 SW Jahr logical block #0 |
| _DCX_SW_VERSION_BLK_1 | unsigned char | UDS $22 $F1 $51 SW patch level logical block #1 |
| _DCX_SW_WEEK_BLK_1 | unsigned char | UDS $22 $F1 $51 SW Woche logical block #1 |
| _DCX_SW_YEAR_BLK_1 | unsigned char | UDS $22 $F1 $51 SW Jahr logical block #1 |
| _DCX_BOOT_VERSION | unsigned char | UDS $22 $F1 $53 boot SW version |
| _DCX_BOOT_WEEK | unsigned char | UDS $22 $F1 $53 boot SW Woche |
| _DCX_BOOT_YEAR | unsigned char | UDS $22 $F1 $53 boot SW Jahr |
| _DCX_HW_SUPPLIER | unsigned int | UDS $22 $F1 $54 HW Lieferant (Tabelle in performance spec) |
| _DCX_SW_SUPPLIER | unsigned int | UDS $22 $F1 $55 SW Lieferant (Tabelle in performance spec) |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |
| _REQUEST2 | binary | Hex-Auftrag an SG |
| _RESPONSE2 | binary | Hex-Antwort von SG |
| _REQUEST3 | binary | Hex-Auftrag an SG |
| _RESPONSE3 | binary | Hex-Antwort von SG |
| _REQUEST4 | binary | Hex-Auftrag an SG |
| _RESPONSE4 | binary | Hex-Antwort von SG |
| _REQUEST5 | binary | Hex-Auftrag an SG |
| _RESPONSE5 | binary | Hex-Antwort von SG |
| _REQUEST6 | binary | Hex-Auftrag an SG |
| _RESPONSE6 | binary | Hex-Antwort von SG |
| _REQUEST7 | binary | Hex-Auftrag an SG |
| _RESPONSE7 | binary | Hex-Antwort von SG |
| _REQUEST8 | binary | Hex-Auftrag an SG |
| _RESPONSE8 | binary | Hex-Antwort von SG |
| _REQUEST9 | binary | Hex-Auftrag an SG |
| _RESPONSE9 | binary | Hex-Antwort von SG |

<a id="job-uds-test-e72"></a>
### _UDS_TEST_E72

Test Services Modus: Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei Tabelle JobResult STATUS_TEXT |
| _TST_223F30_DiagIdx | string | Diagnoseindex |
| _TST_223F30_ActDiagStat | string | aktiv Diagnostic Status |
| _TST_223F30_ActDiagSession | string | aktiv Diagnostic Sitzung |
| _TST_223F30_REQUEST | binary | Hex-Auftrag an SG |
| _TST_223F30_RESPONSE | binary | Hex-Antwort von SG |
| _TST_223F36_HW_Ver_Info | string | Hardware Version Info |
| _TST_223F36_REQUEST | binary | Hex-Auftrag an SG |
| _TST_223F36_RESPONSE | binary | Hex-Antwort von SG |
| _TST_223F38_HWS_Ver_Info | string | Software Versions Info (HW*) |
| _TST_223F38_DATA_Ver_Info | string | Antwortsatz Versions Info |
| _TST_223F38_REQUEST | binary | Hex-Auftrag an SG |
| _TST_223F38_RESPONSE | binary | Hex-Antwort von SG |
| _TST_223F41_HW_NR | string | BMW-Nr. HW |
| _TST_223F41_REQUEST | binary | Hex-Auftrag an SG |
| _TST_223F41_RESPONSE | binary | Hex-Antwort von SG |
| _TST_223F51_HWS_NR | string | BMW-Nr. Antwort |
| _TST_223F51_DATA_NR | string | BMW-Nr. Antwort |
| _TST_223F51_REQUEST | binary | Hex-Auftrag an SG |
| _TST_223F51_RESPONSE | binary | Hex-Antwort von SG |
| _TST_223F61_ZB_NR | string | BMW-Nr. ZusBau |
| _TST_223F61_REQUEST | binary | Hex-Auftrag an SG |
| _TST_223F61_RESPONSE | binary | Hex-Antwort von SG |

<a id="job-bpcm-eng-sw-no"></a>
### _BPCM_ENG_SW_NO

TO READ OUT THE SW NUMBER ASSIGNED DURING EACH I-STEP OF DEVELOPMENT THIS SERVICE IS ONLY FOR DEVELOPMENT AND MAY BE REMOVED AT START OF PRODUCTION THIS NUMBER REPRESENTS THE MAJOR, MINOR AND BUILD OF SW RELEASE AS WELL AS THE INDICATES IF THE SW PRESENT IN BPCM IS FOR BMW_SW OR DCX TO VERIFY THE VALIDITY

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| CSR_VERSION | string | INDICATES CSR VERSION NO e.g. 22.0 |
| SW_NUMBER | string | INDICATES THE SW NUMBER e.g. 73.4.0 WHERE 73 IS THE MAJOR SW NO, 4 IS THE MINOR SW NO AND 0 IS THE BUILD NO |
| DAIMLER_SW | string | IF THIS RESULT IS TRUE MEANS, THE SW PRESENT IN BPCM IS FOR DAIMLER |
| BWM_SW | string | IF THIS RESULT IS TRUE MEANS, THE SW PRESENT IN BPCM IS FOR BMW |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
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

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender Informations Feldes Standard Flashjob Modus   : Default

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| AIF_FG_NR | string | Fahrgestellnummer 7-stellig |
| AIF_FG_NR_LANG | string | Fahrgestellnummer 17-stellig falls vorhanden, sonst 7-stellig |
| AIF_DATUM | string | Datum der SG-Programmierung in der Form TT.MM.JJJJ |
| AIF_ZB_NR | string | BMW/Rover Zusammenbaunummer |
| AIF_SW_NR | string | BMW/Rover Datensatznummer - Softwarenummer |
| AIF_BEHOERDEN_NR | string | BMW/Rover Behoerdennummer |
| AIF_HAENDLER_NR | string | Haendlernummer |
| AIF_SERIEN_NR | string | Tester Seriennummer |
| AIF_KM | string | km-Stand bei der Programmierung |
| AIF_PROG_NR | string | Programmstandsnummer |
| AIF_ANZ_FREI | unsigned int | Anzahl noch vorhandener AIF-Eintraege |
| AIF_ANZAHL_PROG | unsigned int | Anzahl Programmiervorgaenge |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST01 | binary | Hex-Auftrag an SG |
| _RESPONSE01 | binary | Hex-Antwort von SG |
| _REQUEST02 | binary | Hex-Auftrag an SG |
| _RESPONSE02 | binary | Hex-Antwort von SG |
| _REQUEST03 | binary | Hex-Auftrag an SG |
| _RESPONSE03 | binary | Hex-Antwort von SG |
| _REQUEST04 | binary | Hex-Auftrag an SG |
| _RESPONSE04 | binary | Hex-Antwort von SG |

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
| ZIF_BMW_PST | string | Dummywert fuer BMW PST |
| _REQUEST01 | binary | Hex-Auftrag an SG |
| _RESPONSE01 | binary | Hex-Antwort von SG |
| _REQUEST02 | binary | Hex-Auftrag an SG |
| _RESPONSE02 | binary | Hex-Antwort von SG |

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
| ZIF_BACKUP_BMW_PST | string | dummy |
| _TEL_AUFTRAG | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT | binary | Hex-Antwort von SG |

<a id="job-physikalische-hw-nr-lesen"></a>
### PHYSIKALISCHE_HW_NR_LESEN

Auslesen der physikalischen Hardwarenummer UDS: $22,$3F Read Data Identifier BMW $41 Hardware Part Number

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| PHYSIKALISCHE_HW_NR | string | Physikalische Hardware-Nummer |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

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
| _TEL_AUFTRAG2 | binary | Hex-Auftrag an SG |
| _TEL_ANTWORT2 | binary | Hex-Antwort von SG |

<a id="job-status-soc-lesen"></a>
### STATUS_SOC_LESEN

HIGH VOLTAGE BATTERIE SOC WERT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PERCENTAGE_EINH | string | "%" |
| STAT_PERCENTAGE_WERT | real | WERT in % |
| STAT_VALIDITY | string | WERT GUELTIG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-current-lesen"></a>
### STATUS_CURRENT_LESEN

HIGH VOLT BATTERIE STROM SENSOR WERT negative Stromwerte bedeuten Laden der Batterie POSITIVE Stromwerte bedeuten Entladung der Batterie

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_AMPS_EINH | string | "Amps" |
| STAT_AMPS_WERT | real | WERT in Amps |
| STAT_VALIDITY | string | gueltiger Wert ODER ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-busvolt-calculate-lesen"></a>
### STATUS_BUSVOLT_CALCULATE_LESEN

SUMME der 26 MODUL SPANNUNGEN ALS HV-BUS SPANNUNG LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VOLTS_EINH | string | "V" |
| STAT_VOLTS_WERT | real | Wert in Volts |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bus-volt-lesen"></a>
### STATUS_BUS_VOLT_LESEN

HV BUS SPANNUNG Wert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VOLTS_EINH | string | "V" |
| STAT_VOLTS_WERT | real | Wert in Volts |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-busvolt-source-lesen"></a>
### STATUS_BUSVOLT_SOURCE_LESEN

QUELLE FUER HV BUS SPANNUNG Wert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOURCE_VOLTS_INDEX | unsigned int | BUS SPANNUNG QUELLE INDEX |
| STAT_SOURCE_VOLTS_TEXT | string | BUS SPANNUNG QUELLE TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-pack-volt-lesen"></a>
### STATUS_PACK_VOLT_LESEN

PACK SPANNUNG SENSOR Wert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VOLTS_EINH | string | "V" |
| STAT_VOLTS_WERT | real | Wert IN VOLTS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-pack-volt-source-lesen"></a>
### STATUS_PACK_VOLT_SOURCE_LESEN

QUELLE FUER PACK SPANNUNG Wert

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOURCE_VOLTS_INDEX | unsigned int | PACK VOLT QUELLE INDEX |
| STAT_SOURCE_VOLTS_TEXT | string | PACK VOLT QUELLE TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-pwr-chrg-lt-lesen"></a>
### STATUS_PWR_CHRG_LT_LESEN

Lang Zeit 10s LADELEISTUNGS LIMIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WATTS_EINH | string | "kW" |
| STAT_WATTS_WERT | real | Wert IN kW |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-pwr-chrg-st-lesen"></a>
### STATUS_PWR_CHRG_ST_LESEN

Kurz Zeit 2s LADELEISTUNGS LIMIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WATTS_EINH | string | "kW" |
| STAT_WATTS_WERT | real | Wert IN kW |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-pwr-dischrg-lt-lesen"></a>
### STATUS_PWR_DISCHRG_LT_LESEN

Lang Zeit 10s ENTLADELEISTUNGS LIMIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WATTS_EINH | string | "kW" |
| STAT_WATTS_WERT | real | Wert IN kW |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-pwr-dischrg-st-lesen"></a>
### STATUS_PWR_DISCHRG_ST_LESEN

Kurz Zeit 2s ENTLADELEISTUNGS LIMIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_WATTS_EINH | string | "kW" |
| STAT_WATTS_WERT | real | Wert IN kW |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-max-modvolt-lesen"></a>
### STATUS_MAX_MODVOLT_LESEN

MAXIMALE SPANNUNG ALLER 26 MODUL SPANNUNGSENSOREN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VOLTS_EINH | string | "V" |
| STAT_VOLTS_WERT | real | Wert IN VOLTS |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-min-modulspannung-lesen"></a>
### STATUS_MIN_MODULSPANNUNG_LESEN

MINIMALE SPANNUNG ALLER 26 MODUL SPANNUNGSENSOREN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VOLTS_EINH | string | "V" |
| STAT_VOLTS_WERT | real | Wert IN VOLTS |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-12v-feed2controller-lesen"></a>
### STATUS_12V_FEED2CONTROLLER_LESEN

WERT 12V Versorgungsspannung BPCM LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VOLTS_EINH | string | "Volts" |
| STAT_VOLTS_WERT | real | Wert IN VOLTS |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-12v-feed2pump-lesen"></a>
### STATUS_12V_FEED2PUMP_LESEN

WERT 12V Versorgungsspannung BATTERIE KUEHLMITTEL PUMPE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_12V_FEED2PUMP_EINH | string | "Volts" |
| STAT_12V_FEED2PUMP_WERT | real | Wert IN VOLTS |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-12v-feed2cntcr-lesen"></a>
### STATUS_12V_FEED2CNTCR_LESEN

WERT 12V Versorgungsspannung HIGH VOLTAGE BATTERIE PACK SCHUETZE ALLE SCHUETZE WERDEN AUS DER SELBEN QUELLE VERSORGT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_12V_FEED2CNTCR_EINH | string | "Volts" |
| STAT_12V_FEED2CNTCR_WERT | real | Wert IN VOLTS |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-max-modtemp-lesen"></a>
### STATUS_MAX_MODTEMP_LESEN

MAXIMALE TEMPERATUR DER 4 MODUL SENSOREN LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMPERATURE_EINH | string | "°C" |
| STAT_TEMPERATURE_WERT | real | Grad Celsius |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-min-modtemp-lesen"></a>
### STATUS_MIN_MODTEMP_LESEN

MINIMALE TEMPERATUR DER 4 MODUL SENSOREN LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMPERATURE_EINH | string | "°C" |
| STAT_TEMPERATURE_WERT | real | Grad Celsius |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hv-bpcm-state-lesen"></a>
### STATUS_HV_BPCM_STATE_LESEN

RESULT: TRUE-&gt;JA  FALSE-&gt;NEIN GRUND FUER VERHINDERUNG ODER ABBRUCH DER vORLADEPROZEDUR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PRECHRG_INHIBITED | unsigned char | ZUSTAND SCHUETZE VORLADUNG VERBOTEN - INDEX |
| STAT_PRECHRG_INHIBITED_TEXT | string | ZUSTAND SCHUETZE VORLADUNG VERBOTEN - TEXT |
| STAT_PRECHRG_DISCONNECTED_BUS | unsigned char | HV BUS WAEHREND VORLADUNG NICHT MIT BATTERIE VERBUNDEN - INDEX |
| STAT_PRECHRG_DISCONNECTED_BUS_TEXT | string | HV BUS WAEHREND VORLADUNG NICHT MIT BATTERIE VERBUNDEN - TEXT |
| STAT_SUCCESSFUL_DISCHARGE | unsigned char | ERFOLGREICHE ENTLADUNG GEMESSEN - INDEX |
| STAT_SUCCESSFUL_DISCHARGE_TEXT | string | ERFOLGREICHE ENTLADUNG GEMESSEN - TEXT |
| STAT_PRECHRG_BUS_SHORT | unsigned char | HV_BUS KURZSCHLUSS WAEHREND VORLADUND AUFGETRETEN - INDEX |
| STAT_PRECHRG_BUS_SHORT_TEXT | string | HV_BUS KURZSCHLUSS WAEHREND VORLADUND AUFGETRETEN - TEXT |
| STAT_REDUNDANT_CONTACTOR_COMMAND_VALIDITY | unsigned char | GUELTIGKEIT PEB OEFFNUNGS ANFORDERUNG - INDEX |
| STAT_REDUNDANT_CONTACTOR_COMMAND_VALIDITY_TEXT | string | GUELTIGKEIT PEB OEFFNUNGS ANFORDERUNG - TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hvilcurr-return-lesen"></a>
### STATUS_HVILCURR_RETURN_LESEN

WERT HVIL RUECKKEHRSTROM IN mA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MILLI_AMPS_EINH | string | "mA" |
| STAT_MILLI_AMPS_WERT | real | Wert IN AMPS |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-coolant-in-temp-lesen"></a>
### STATUS_COOLANT_IN_TEMP_LESEN

KUEHLMITTEL INLET TEMPERATUR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMPERATURE_EINH | string | "°C" |
| STAT_TEMPERATURE_WERT | real | WERT IN Grad C |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-coolant-out-temp-lesen"></a>
### STATUS_COOLANT_OUT_TEMP_LESEN

KUEHLMITTEL OUTLET TEMPERATUR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_COOLANT_OUTLET_TEMP_EINH | string | "°C" |
| STAT_COOLANT_OUTLET_TEMP_WERT | real | WERT IN Grad C |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-isolation-resi-lesen"></a>
### STATUS_ISOLATION_RESI_LESEN

ISOLATIONS WIDERSTANDSWERTE MIT OFFENEN UND GESCHLOSSENEN SCHUETZEN UND FUER POSITVEN UND NEGATIVEN HV_BUS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ISOL_RESI_EINH | string | "MegOhm" |
| STAT_RESI_POSI_RAIL_CLOSED_CNTCR | real | WERT IN MEGOHM |
| STAT_RESI_NEG_RAIL_CLOSED_CNTCR | real | WERT IN MEGOHM |
| STAT_COMBINED_RESI_OPEN_CNTCR | real | WERT IN MEGOHM |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-isolation-state-lesen"></a>
### STATUS_ISOLATION_STATE_LESEN

ISOLATION TEST RESULT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ISOL_STATUS_INDEX | unsigned int | ISOLATION TEST RESULT - INDEX |
| STAT_ISOL_STATUS_TEXT | string | ISOLATION TEST RESULT - TEXT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cnctr-pwm-cmd-lesen"></a>
### STATUS_CNCTR_PWM_CMD_LESEN

PEB CONTACTOR COMMAND Wert IN %PWM

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PERCENTAGE_EINH | string | "%" |
| STAT_PERCENTAGE_WERT | real | Wert IN % |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cool-pump-speed-lesen"></a>
### STATUS_COOL_PUMP_SPEED_LESEN

KUEHLMITTEL Pumpe Geschwindigkeit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PERCENTAGE_EINH | string | "%" |
| STAT_PERCENTAGE_WERT | real | Wert IN % |
| STAT_VALIDITY | string | Angabe ob gemeldete Geschwindigkeit gueltig ist Wenn momentan ein Fehler vorhanden ist, wird die Geschwindigkeit ungueltig |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-precharge-inhibit-time-lesen"></a>
### STATUS_PRECHARGE_INHIBIT_TIME_LESEN

Verbleibende Zeit in der die Vorladung verboten ist max. 30min

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_REMAINING_TIME_EINH | string | "s" |
| STAT_REMAINING_TIME_WERT | unsigned int | Wert In Sekunden |
| STAT_VALIDITY | string | gueltiger Wert oder Ungueltiger Wert |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-4modules-temp-lesen"></a>
### STATUS_4MODULES_TEMP_LESEN

Temperaturwerte ALLER 4 ODER EINZELNER MODULTEMPERATURSENSOREN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODULE_NUMBER | unsigned int | MODULSENSOR NUMMER:1-4 KEIN ARGUMENT(DEFAULT) FUER ALLE SENSOREN NUMMER 1-4 FUER EINZELNEN SENSOR |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOD1_TMP_EINH | string | "°C" |
| STAT_MOD1_TMP_WERT | real | WERT IN Grad Celsius |
| STAT_MOD2_TMP_EINH | string | "°C" |
| STAT_MOD2_TMP_WERT | real | WERT IN Grad Celsius |
| STAT_MOD3_TMP_EINH | string | "°C" |
| STAT_MOD3_TMP_WERT | real | WERT IN Grad Celsius |
| STAT_MOD4_TMP_EINH | string | "°C" |
| STAT_MOD4_TMP_WERT | real | WERT IN Grad Celsius |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-26-modules-volt-lesen"></a>
### STATUS_26_MODULES_VOLT_LESEN

Spannungswerte ALLER 26 ODER EINZELNER MODULSPANNUNGSSENSOREN

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODULE_NUMBER | unsigned int | MODULSENSOR NUMMER:1-26 KEIN ARGUMENT(DEFAULT) FUER ALLE SENSOREN NUMMER 1-26 FUER EINZELNEN SENSOR |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_EINH | string | "V" |
| STAT_MOD1_VOLT | real | WERT IN "V" |
| STAT_MOD2_VOLT | real | WERT IN "V" |
| STAT_MOD3_VOLT | real | WERT IN "V" |
| STAT_MOD4_VOLT | real | WERT IN "V" |
| STAT_MOD5_VOLT | real | WERT IN "V" |
| STAT_MOD6_VOLT | real | WERT IN "V" |
| STAT_MOD7_VOLT | real | WERT IN "V" |
| STAT_MOD8_VOLT | real | WERT IN "V" |
| STAT_MOD9_VOLT | real | WERT IN "V" |
| STAT_MOD10_VOLT | real | WERT IN "V" |
| STAT_MOD11_VOLT | real | WERT IN "V" |
| STAT_MOD12_VOLT | real | WERT IN "V" |
| STAT_MOD13_VOLT | real | WERT IN "V" |
| STAT_MOD14_VOLT | real | WERT IN "V" |
| STAT_MOD15_VOLT | real | WERT IN "V" |
| STAT_MOD16_VOLT | real | WERT IN "V" |
| STAT_MOD17_VOLT | real | WERT IN "V" |
| STAT_MOD18_VOLT | real | WERT IN "V" |
| STAT_MOD19_VOLT | real | WERT IN "V" |
| STAT_MOD20_VOLT | real | WERT IN "V" |
| STAT_MOD21_VOLT | real | WERT IN "V" |
| STAT_MOD22_VOLT | real | WERT IN "V" |
| STAT_MOD23_VOLT | real | WERT IN "V" |
| STAT_MOD24_VOLT | real | WERT IN "V" |
| STAT_MOD25_VOLT | real | WERT IN "V" |
| STAT_MOD26_VOLT | real | WERT IN "V" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-service-disconnect-lesen"></a>
### STATUS_SERVICE_DISCONNECT_LESEN

MELDET DEN AKTUELLEN ZUSTAND DES SERVICE SCHALTERS 0 -&gt; GESCHLOSSEN ODER 1 -&gt; OFFEN ODER 2 -&gt; GESCHLOSSEN & SICHERUNG KAPUTT ODER 3 -&gt; UNBEKANNT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SERVICE_DISCONNECT_INDEX | unsigned int | SERVICE SCHALTERS STATUS INDEX 0 -&gt; GESCHLOSSEN ODER 1 -&gt; OFFEN ODER 2 -&gt; GESCHLOSSEN & SICHERUNG KAPUTT ODER 3 -&gt; UNBEKANNT |
| STAT_SERVICE_DISCONNECT_TEXT | string | SERVICE DISCONNECT STATUS TEXT : 0 -&gt; GESCHLOSSEN ODER 1 -&gt; OFFEN ODER 2 -&gt; GESCHLOSSEN & SICHERUNG KAPUTT ODER 3 -&gt; UNBEKANNT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hvil-lesen"></a>
### STATUS_HVIL_LESEN

MELDET DEN AKTUELLEN ZUSTAND DES HVIL, HOCHVOLTKONTAKTUEBERWACHUNG 0 -&gt; NICHT AKTIV, 1 -&gt; FEHLERFREI,2 -&gt; FEHLER ODER 3 -&gt; UNGUELTIG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HVIL_INDEX | unsigned char | HVIL LOOP STATUS INDEX : 0 -&gt; NICHT AKTIV, 1 -&gt; FEHLERFREI,2 -&gt; FEHLER ODER 3 -&gt; UNGUELTIG |
| STAT_HVIL_TEXT | string | HVIL LOOP STATUS TEXT :  NICHT AKTIV, FEHLERFREI, FEHLER UND UNGUELTIG |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-reason-cnctr-not-close-when-cmnd-lesen"></a>
### STATUS_REASON_CNCTR_NOT_CLOSE_WHEN_CMND_LESEN

Gespeicherte & momentan anliegende Fehler die das Schliesen der Schuetze verhindern STORED: Gespeicherte Fehler sind aus vorangegangenen Zyklen PRESENT: momentan anliegende Fehler sind aus dem momentanen Zyklus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STORED_REASON_PRECHRG_INHIBIT | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem VORLADUNG VERBOTEN Fehler |
| STAT_STORED_REASON_ACTIVE_DISCHARGE_FAULT | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem Aktive Entladung Fehler |
| STAT_STORED_REASON_WELDED_CONTACTORS | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem verschweiste SCHUETZE Fehler |
| STAT_STORED_REASON_SERVICE_DISCONNECT_REMOVED | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem Service Schalter entfernt |
| STAT_STORED_REASON_HVIL_FAILURE | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem HVIL Fehler |
| STAT_STORED_REASON_CONTACTOR_CLOSURE_INHIBIT | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem CONTACTOR CLOSURE INHIBIT BIT BIT KANN MIT DIAGNOSE TOOL RESETET WERDEN UM DAS SCHLIESSEN DER SCHUETZE ZU ERLAUBEN |
| STAT_STORED_REASON_BPCM_CNCTR_OPEN_REQ | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem BPCM SCHUETZ OEFFNUNGS ANFORDERUNG BIT |
| STAT_PRESENT_REASON_PRECHRG_INHIBIT | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem VORLADUNG VERBOTEN Fehler |
| STAT_PRESENT_REASON_ACTIVE_DISCHARGE_FAULT | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem Aktive Entladung Fehler |
| STAT_PRESENT_REASON_WELDED_CONTACTORS | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem verschweiste SCHUETZE Fehler |
| STAT_PRESENT_REASON_SERVICE_DISCONNECT_REMOVED | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem Service Schalter entfernt |
| STAT_PRESENT_REASON_HVIL_FAILURE | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem HVIL Fehler |
| STAT_PRESENT_REASON_CONTACTOR_CLOSURE_INHIBIT | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem CONTACTOR CLOSURE INHIBIT BIT BIT KANN MIT DIAGNOSE TOOL RESETET WERDEN UM DAS SCHLIESEN DER SCHUETZE ZU ERLAUBEN |
| STAT_PRESENT_REASON_BPCM_CNCTR_OPEN_REQ | string | TRUE -&gt;SCHUETZE Schliessen nicht wegen aktivem BPCM SCHUETZ OEFFNUNGS ANFORDERUNG BIT |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |

<a id="job-status-reasons-cnctr-opened-lesen"></a>
### STATUS_REASONS_CNCTR_OPENED_LESEN

Gespeicherte & momentan anliegende Gruende fuer das Oeffnen der Schuetze STORED: Gespeicherte Fehler sind aus vorangegangenen Zyklen PRESENT: momentan anliegende Fehler sind aus dem momentanen Zyklus

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HCP_CMND_OPEN_PRESENT_REASON | string | PEB OEFFNUNGS ANFORDERUNG   |
| STAT_IMPEND_OPEN_PRESENT_REASON | string | SCHUETZE offen wegen qualified contactor command IMPENDING OPEN |
| STAT_PRECHG_FAILED_PRESENT_REASON | string | SCHUETZE offen wegen VORLADUNG Fehler |
| STAT_OVERTEMP_PRESENT_REASON | string | SCHUETZE offen wegen Batterie Modul Uebertemperatur |
| STAT_12V_HIGH_PRESENT_REASON | string | SCHUETZE offen wegen 12V Versorgungsspannung SCHUETZE Ueberspannung |
| STAT_12V_LOW_PRESENT_REASON | string | SCHUETZE offen wegen 12V Versorgungsspannung SCHUETZE Unterspannung |
| STAT_MODVLT_HIGH_PRESENT_REASON | string | SCHUETZE offen wegen Batterie Modul Ueberspannung |
| STAT_MODVLT_LOW_PRESENT_REASON | string | SCHUETZE offen wegen Batterie Modul Unterspannung |
| STAT_HCP_CMND_OPEN_STORED_REASON | string | PEB OEFFNUNGS ANFORDERUNG |
| STAT_IMPEND_OPEN_STORED_REASON | string | SCHUETZE offen wegen qualified contactor command  IMPENDING OPEN |
| STAT_PRECHG_FAILED_STORED_REASON | string | SCHUETZE offen wegen VORLADUNG Fehler |
| STAT_OVERTEMP_STORED_REASON | string | SCHUETZE offen wegen Batterie Modul Uebertemperatur |
| STAT_12V_HIGH_STORED_REASON | string | SCHUETZE offen wegen 12V Versorgungsspannung SCHUETZE Ueberspannung |
| STAT_12V_LOW_STORED_REASON | string | SCHUETZE offen wegen 12V Versorgungsspannung SCHUETZE Unterspannung |
| STAT_MODVLT_HIGH_STORED_REASON | string | SCHUETZE offen wegen Batterie Modul Ueberspannung |
| STAT_MODVLT_LOW_STORED_REASON | string | SCHUETZE offen wegen Batterie Modul Unterspannung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |

<a id="job-status-active-discharge-lesen"></a>
### STATUS_ACTIVE_DISCHARGE_LESEN

Status der der Aktiven Entladung beim letzen Abschalten des HV-BUS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ACTIVE_DISCHARGE_INDEX | unsigned int | 0 -&gt; ERFOLGREICH ENTLADEN & 1 -&gt; nicht ERFOLGREICH ENTLADEN |
| STAT_ACTIVE_DISCHARGE_TEXT | string | ERFOLGREICH ENTLADEN oder nicht ERFOLGREICH ENTLADEN |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-battery-resi-lesen"></a>
### STATUS_BATTERY_RESI_LESEN

Wert HV Batterie Innenwiderstand

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERY_RESI_EINH | string | "Ohm" |
| STAT_BATTERY_RESI_WERT | real | HV Batterie Innenwiderstand |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-hvbp-cntcr-state-lesen"></a>
### STATUS_HVBP_CNTCR_STATE_LESEN

Zustand HIGH VOLTAGE Batterie Schuetze

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CNTCR_INDEX | unsigned int | Zeigt den zugeordneten Index fuer Schuetz Zustand |
| STAT_CNTCR_TEXT | string | Schuetz Zustand offen/VORLADEN/GESCHLOSSEN/VORLADUNG fehlgeschlagen/VORLADUNG VERBOTEN |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-can-cntcr-cmnd-lesen"></a>
### STATUS_CAN_CNTCR_CMND_LESEN

Zustand PEB CONTACTOR COMMAND von HCP VIA CAN BUS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CNTCR_CMND_INDEX | unsigned int | Zeigt den zugeordneten Index fuer HCP CONTACTOR COMMAND |
| STAT_CNTCR_CMND_TEXT | string | CONTACTOR COMMAND TEXT: offen/GESCHLOSSEN/CHRASH OEFFNUNG/ungueltig |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-uh-soc-histogram-lesen"></a>
### STATUS_UH_SOC_HISTOGRAM_LESEN

Nutzung-Historie fuer die Ladezustandwerte wandert in verschiedene Intervalle/Schlitze Waehrend der Schuetzen geschlossen sind, erfasst das BPCM ein Snapshot ueber der SOC-Historie. Am Ende aller 10 Sekunden-Interval (Waehrend der Schuetzen geschlossen sind), der richtige wird auf Basis der laufenden SOC inkrementiert. Die Absicht ist ein Snaptshot vom SOC aller 10 Sekunden aufzuzeichnen. SOC Intervalle: 1-&gt; 0~15.9%, 2-&gt; 16.0~30.9%, 3-&gt; 31.0~40.9%, 4-&gt; 41.0~51.9%, 5-&gt; 52.0~60.9%, 6-&gt; 61.0~68.9% SOC Intervalle: 7-&gt; 69.0~80.9%, 8-&gt; 81.0~90.9%, 9-&gt; 91.0~100%

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOC_RANGE_EINH | string | "zaehlen" |
| STAT_SOC_RANGE01_WERT | unsigned long | 0~15.9% |
| STAT_SOC_RANGE02_WERT | unsigned long | 16.0~30.9% |
| STAT_SOC_RANGE03_WERT | unsigned long | 31.0~40.9% |
| STAT_SOC_RANGE04_WERT | unsigned long | 41.0~51.9% |
| STAT_SOC_RANGE05_WERT | unsigned long | 52.0~60.9% |
| STAT_SOC_RANGE06_WERT | unsigned long | 61.0~68.9% |
| STAT_SOC_RANGE07_WERT | unsigned long | 69.0~80.9 |
| STAT_SOC_RANGE08_WERT | unsigned long | 81.0~90.9% |
| STAT_SOC_RANGE09_WERT | unsigned long | 91.0~100% |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-uh-high-volt-exceeded-lesen"></a>
### STATUS_UH_HIGH_VOLT_EXCEEDED_LESEN

Nutzung-Historie fuer die gesamte Sekunden, wo die Pack- und Modulspannung die Min und MAX- Grenzwerte ueberschreitet das maximale Limit fuer Pack-Spannung ist 419V & das minimale Limit fuer Pack-Spannung ist 244V das maximale Limit fuer Modulspannung ist 16.5V & das minimale Limit fuer Modulspannung ist 9V

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PACK_VOLT_EXCEEDED_MAX_LIMIT_EINH | string | "Sekunden" |
| STAT_PACK_VOLT_EXCEEDED_MAX_LIMIT_WERT | real | MAX LIMIT FOR PACK VOLTAGE HERE IS 419V |
| STAT_PACK_VOLT_EXCEEDED_MIN_LIMIT_EINH | string | "Sekunden" |
| STAT_PACK_VOLT_EXCEEDED_MIN_LIMIT_WERT | real | das minimale Limit fuer Pack-Spannung ist |
| STAT_MOD_VOLT_EXCEEDED_MAX_LIMIT_EINH | string | "Sekunden" |
| STAT_MOD_VOLT_EXCEEDED_MAX_LIMIT_WERT | real | das maximale Limit fuer Modulspannung ist 16.5V |
| STAT_MOD_VOLT_EXCEEDED_MIN_LIMIT_EINH | string | "Sekunden" |
| STAT_MOD_VOLT_EXCEEDED_MIN_LIMIT_WERT | real | das minimale Limit fuer Modulspannung ist 9V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-uh-mod-volt-diff-histogram-lesen"></a>
### STATUS_UH_MOD_VOLT_DIFF_HISTOGRAM_LESEN

Nutzung-Historie fuer wieviel mal die Differenz der Modulspannung in einem bestimmten Bereich oder Intervall geht

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RANGE_EINH | string | "zaehlen" |
| STAT_RANGE01_WERT | unsigned long | RANGE 1: 0~0.25V |
| STAT_RANGE02_WERT | unsigned long | Intervall 2: 0.25~0.5V |
| STAT_RANGE03_WERT | unsigned long | Intervall 3: 0.5~0.75V |
| STAT_RANGE04_WERT | unsigned long | Intervall 4: 0.75~0.1V |
| STAT_RANGE05_WERT | unsigned long | Intervall 5: 1~1.25V |
| STAT_RANGE06_WERT | unsigned long | Intervall 6: 1.25~1.5V |
| STAT_RANGE07_WERT | unsigned long | Intervall 7: 1.5~1.75V |
| STAT_RANGE08_WERT | unsigned long | Intervall 8: 1.75~2V |
| STAT_RANGE09_WERT | unsigned long | Intervall 9: 2~2.5V |
| STAT_RANGE10_WERT | unsigned long | Intervall 10: 2.5~3V |
| STAT_RANGE11_WERT | unsigned long | Intervall 11: 3~19.0V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-uh-max-mod-vlt-histogram-lesen"></a>
### STATUS_UH_MAX_MOD_VLT_HISTOGRAM_LESEN

Nutzung-Historie fuer wieviel mal das maximale Modulspannungswert in einem bestimmten Bereich geht Das BPCM erfasst waehrend seines Betriebes die Historie der maximale Modulspannung referenziert auf die "VLID". Das BPCM erfasst die maximale Modulspannung und Modeltemperatur im Zusammenhang zur Modulspannung über 10 Sekunden Intervall Am Ende der 10 Sekunden VLID wird berechnet und der richtige BIN wird auf Basis der maximale Modulespannung über 10 Sekunden-Intervall inkrementiert wenn MAXMODTEMP &lt; 25°C, VLID = 16.25V / wenn MAXMODTEMP &gt;= 25°C, VLID = 16.723 - 0.0137 * MAXMODTEMP - 0.00020833 * MAXMODTEMP * MAXMODTEMP wenn es ein Fehler in der Sensor-Temperatur gibt , VLID = 16.25V BIN Beschreibung: Intervall 1: &lt; VLID, Intervall 2: VLID TO VLID+0.2, Intervall 3: &gt; VLID+0.2 Z.B.: hier ist ein Liste von Werten über 10 Sekunden- Bereich: MAX MOD VOLT | MAX MOD TEMP 16.0V        |  20.5°C 16.1V        |  20°C 16.2V        |  20°C 16.3V        |  20°C Die von der VLID-Kalkualation benutzte Temperatur von 20°C wird mit 16.3V verglichen, um den Bereich zu bestimmen.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VLT_RANGE1_EINH | string | "zaehlen" |
| STAT_VLT_RANGE1_WERT | unsigned long | maximale Modulspannung-Histogramm Intervall 1 zaehlen |
| STAT_VLT_RANGE2_EINH | string | "zaehlen" |
| STAT_VLT_RANGE2_WERT | unsigned long | maximale Modulspannung-Histogramm Intervall 2 zaehlen |
| STAT_VLT_RANGE3_EINH | string | "zaehlen" |
| STAT_VLT_RANGE3_WERT | unsigned long | maximale Modulspannung-Histogramm Intervall 3 zaehlen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-uh-min-mod-vlt-histogram-lesen"></a>
### STATUS_UH_MIN_MOD_VLT_HISTOGRAM_LESEN

Nutzung-Historie fuer wieviel mal das minimale Modulspannungswert in einem bestimmten Bereich geht MIN MOD Spannung Intervall: Intervall 1: 10.0~20.0V, Intervall 2: 9.0~9.999V, Intervall 3: 8.0~8.999V, Intervall 4: 0~7.999V

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VLT_RANGE1_EINH | string | "zaehlen" |
| STAT_VLT_RANGE1_WERT | unsigned long | Intervall 1: 10.0~20.0V |
| STAT_VLT_RANGE2_EINH | string | "zaehlen" |
| STAT_VLT_RANGE2_WERT | unsigned long | Intervall 2: 9.0~9.999V |
| STAT_VLT_RANGE3_EINH | string | "zaehlen" |
| STAT_VLT_RANGE3_WERT | unsigned long | Intervall 3: 8.0~8.999V |
| STAT_VLT_RANGE4_EINH | string | "zaehlen" |
| STAT_VLT_RANGE4_WERT | unsigned long | Intervall 4: 0~7.999V |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-uh-hvbp-volts-histogram-lesen"></a>
### STATUS_UH_HVBP_VOLTS_HISTOGRAM_LESEN

Nutzung-Historie fuer wieviel mal das HVBP-spannung in einem verschiedenen Bereich geht Intervall 1: &lt;200V, Intervall 2: 200~220V, Intervall 3: 220~240, Intervall 4: 240~260V, Intervall 5: 260~280V,  Intervall 6: 280~300A Intervall 7: 300~320V, Intervall 8: 320~340V,  Intervall 9: 340~360V,  Intervall 10: 360~380V,  Intervall 11: 380~400A,	 Intervall 12: &gt; 400A

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_VOLT_RANGE01_EINH | string | "zaehlen" |
| STAT_VOLT_RANGE01_WERT | unsigned long | Intervall 1: &lt;200V |
| STAT_VOLT_RANGE02_EINH | string | "zaehlen" |
| STAT_VOLT_RANGE02_WERT | unsigned long | Intervall 2: 200~220V |
| STAT_VOLT_RANGE03_EINH | string | "zaehlen" |
| STAT_VOLT_RANGE03_WERT | unsigned long | Intervall 3: 220~240 |
| STAT_VOLT_RANGE04_EINH | string | "zaehlen" |
| STAT_VOLT_RANGE04_WERT | unsigned long | Intervall 4: 240~260V |
| STAT_VOLT_RANGE05_EINH | string | "zaehlen" |
| STAT_VOLT_RANGE05_WERT | unsigned long | Intervall 5: 260~280V |
| STAT_VOLT_RANGE06_EINH | string | "zaehlen" |
| STAT_VOLT_RANGE06_WERT | unsigned long | Intervall 6: 280~300A |
| STAT_VOLT_RANGE07_EINH | string | "zaehlen" |
| STAT_VOLT_RANGE07_WERT | unsigned long | Intervall 7: 300~320V |
| STAT_VOLT_RANGE08_EINH | string | "zaehlen" |
| STAT_VOLT_RANGE08_WERT | unsigned long | Intervall 8: 320~340V |
| STAT_VOLT_RANGE09_EINH | string | "zaehlen" |
| STAT_VOLT_RANGE09_WERT | unsigned long | Intervall 9: 340~360V |
| STAT_VOLT_RANGE10_EINH | string | "zaehlen" |
| STAT_VOLT_RANGE10_WERT | unsigned long | Intervall 10: 360~380V |
| STAT_VOLT_RANGE11_EINH | string | "zaehlen" |
| STAT_VOLT_RANGE11_WERT | unsigned long | Intervall 11: 380~400A |
| STAT_VOLT_RANGE12_EINH | string | "zaehlen" |
| STAT_VOLT_RANGE12_WERT | unsigned long | Intervall 12: &gt; 400A |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-uh-current-histogram-lesen"></a>
### STATUS_UH_CURRENT_HISTOGRAM_LESEN

Nutzung-Historie fuer wieviel mal der Strom in einem verschiedenen Bereich geht Intervall 1: &lt;-200A, Intervall 2: -200~-120A, Intervall 3: -120~-60A, Intervall 4: -60~-30A, Intervall 5: -30~-10A,  Intervall 6: -10~0A Intervall 7: 0~10A, Intervall 8: 10~30A,  Intervall 9: 30~60A,  Intervall 10: 60~120A,  Intervall 11: 120~200A,	 Intervall 12: &gt; 200A

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CURR_RANGE01_EINH | string | "zaehlen" |
| STAT_CURR_RANGE01_WERT | unsigned long | Intervall 1: &lt;-200A |
| STAT_CURR_RANGE02_EINH | string | "zaehlen" |
| STAT_CURR_RANGE02_WERT | unsigned long | Intervall 2: -200~-120A |
| STAT_CURR_RANGE03_EINH | string | "zaehlen" |
| STAT_CURR_RANGE03_WERT | unsigned long | Intervall 3: -120~-60A |
| STAT_CURR_RANGE04_EINH | string | "Stunden" |
| STAT_CURR_RANGE04_WERT | unsigned long | Intervall 4: -60~-30A |
| STAT_CURR_RANGE05_EINH | string | "zaehlen" |
| STAT_CURR_RANGE05_WERT | unsigned long | Intervall 5: -30~-10A |
| STAT_CURR_RANGE06_EINH | string | "zaehlen" |
| STAT_CURR_RANGE06_WERT | unsigned long | Intervall 6: -10~0A |
| STAT_CURR_RANGE07_EINH | string | "zaehlen" |
| STAT_CURR_RANGE07_WERT | unsigned long | Intervall 7: 0~10A |
| STAT_CURR_RANGE08_EINH | string | "zaehlen" |
| STAT_CURR_RANGE08_WERT | unsigned long | Intervall 8: 10~30A |
| STAT_CURR_RANGE09_EINH | string | "zaehlen" |
| STAT_CURR_RANGE09_WERT | unsigned long | Intervall 9: 30~60A |
| STAT_CURR_RANGE10_EINH | string | "zaehlen" |
| STAT_CURR_RANGE10_WERT | unsigned long | Intervall 10: 60~120A |
| STAT_CURR_RANGE11_EINH | string | "zaehlen" |
| STAT_CURR_RANGE11_WERT | unsigned long | Intervall 11: 120~200A |
| STAT_CURR_RANGE12_EINH | string | "zaehlen" |
| STAT_CURR_RANGE12_WERT | unsigned long | Intervall 12: &gt; 200A |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-uh-temperature-histogram-lesen"></a>
### STATUS_UH_TEMPERATURE_HISTOGRAM_LESEN

Nutzung-Historie fuer wieviel mal die HVBP-Temperatur in einem verschiedenen Bereich geht Intervall 1: -40~-5 C, Intervall 2: -4.9~15 C, Intervall 3: 15.1~30 C, Intervall 4: 30.1~35 C, Intervall 5: 35.1~40 C Intervall 6: 40.1~45 C, Intervall 7: 45.1~50 C, Intervall 8: 50.1~60 C, Intervall 9: 60.1~65 C, Intervall 10: 65.1~75 C, Intervall 11: 75.1~85 C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TEMP_RANGE_EINH | string | "zaehlen" |
| STAT_TEMP_RANGE01_WERT | unsigned long | Intervall 1: -40~-5 C |
| STAT_TEMP_RANGE02_WERT | unsigned long | Intervall 2: -4.9~15 C |
| STAT_TEMP_RANGE03_WERT | unsigned long | Intervall 3: 15.1~30 C |
| STAT_TEMP_RANGE04_WERT | unsigned long | Intervall 4: 30.1~35 C |
| STAT_TEMP_RANGE05_WERT | unsigned long | Intervall 5: 35.1~40 C |
| STAT_TEMP_RANGE06_WERT | unsigned long | Intervall 6: 40.1~45 C |
| STAT_TEMP_RANGE07_WERT | unsigned long | Intervall 7: 45.1~50 C |
| STAT_TEMP_RANGE08_WERT | unsigned long | Intervall 8: 50.1~60 C |
| STAT_TEMP_RANGE09_WERT | unsigned long | Intervall 9: 60.1~65 C |
| STAT_TEMP_RANGE10_WERT | unsigned long | Intervall 10: 65.1~75 C |
| STAT_TEMP_RANGE11_WERT | unsigned long | Intervall 11: 75.1~85 C |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-uh-mod-temp-diff-histogram-lesen"></a>
### STATUS_UH_MOD_TEMP_DIFF_HISTOGRAM_LESEN

Nutzung-Historie fuer wieviel mal die HVBP-Temperatur in einem verschiedenen Bereich geht Modul-Temperatur-Differenz  = MAX MODULE TEMP - MIN MODULE TEMP Intervall 1: 0~3 C, Intervall 2: 3.1~6 C, Intervall 3: 6.1~10 C, Intervall 4: 10.1~125 C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOD_TEMP_DIFF_RANGE_EINH | string | "zaehlen" |
| STAT_MOD_TEMP_DIFF_RANGE01_WERT | unsigned long | Intervall 1: 0~3 C |
| STAT_MOD_TEMP_DIFF_RANGE02_WERT | unsigned long | Intervall 2: 3.1~6 C |
| STAT_MOD_TEMP_DIFF_RANGE03_WERT | unsigned long | Intervall 3: 6.1~10 C |
| STAT_MOD_TEMP_DIFF_RANGE04_WERT | unsigned long | Intervall 4: 10.1~125 C |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-uh-hvbp-coolant-in-temp-histogram-lesen"></a>
### STATUS_UH_HVBP_COOLANT_IN_TEMP_HISTOGRAM_LESEN

Nutzung-Historie fuer wieviel mal das HVBP-Kuehlmitteleinlass in einem verschiedenen Temperaturbereich geht Intervall 1: &lt; 0 C, Intervall 2: 0.10~20 C, Intervall 3: 20.1~30 C, Intervall 4: 30.1~45 C, Intervall 5: &gt; 45 C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_COOLANT_IN_TEMP_RANGE_EINH | string | "zaehlen" |
| STAT_COOLANT_IN_TEMP_RANGE01_WERT | unsigned long | Intervall 1: &lt; 0 C |
| STAT_COOLANT_IN_TEMP_RANGE02_WERT | unsigned long | Intervall 2: 0.10~20 |
| STAT_COOLANT_IN_TEMP_RANGE03_WERT | unsigned long | Intervall 3: 20.1~30 C |
| STAT_COOLANT_IN_TEMP_RANGE04_WERT | unsigned long | Intervall 4: 30.1~45 C |
| STAT_COOLANT_IN_TEMP_RANGE05_WERT | unsigned long | Intervall 5: &gt; 45 C |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-uh-hvbp-coolant-out-temp-histogram-lesen"></a>
### STATUS_UH_HVBP_COOLANT_OUT_TEMP_HISTOGRAM_LESEN

Nutzung-Historie fuer wieviel mal das HVBP-Kuehlmittelauslass in einem verschiedenen Temperaturbereich geht Intervall 1: &lt; 10 C, Intervall 2: 10.1~30 C, Intervall 3: 30.1~40 C, Intervall 4: 40.1~55.0 C, Intervall 5: &gt; 55.0 C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_COOLANT_OUT_TEMP_RANGE_EINH | string | "zaehlen" |
| STAT_COOLANT_OUT_TEMP_RANGE01_WERT | unsigned long | Intervall 1: &lt; 10 C |
| STAT_COOLANT_OUT_TEMP_RANGE02_WERT | unsigned long | Intervall 2: 10.1~30 C |
| STAT_COOLANT_OUT_TEMP_RANGE03_WERT | unsigned long | Intervall 3: 30.1~40 C |
| STAT_COOLANT_OUT_TEMP_RANGE04_WERT | unsigned long | Intervall 4: 40.1~55.0 C |
| STAT_COOLANT_OUT_TEMP_RANGE05_WERT | unsigned long | Intervall 5: &gt; 55.0 C |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-uh-mod-coolant-temp-delta-histogram-lesen"></a>
### STATUS_UH_MOD_COOLANT_TEMP_DELTA_HISTOGRAM_LESEN

Nutzung-Historie fuer wieviel mal das HVBP-Modul und die Kuehlmittel-Einlasstemperaturdifferenz in einem verschiedenen Bereich geht Intervall 1: -40~-30 C, Intervall 2: -29.9~-25 C, Intervall 3: -24.9~20.0 C, Intervall 4: -19.90~-15 C, Intervall 5: -14.9~-0.1 C Intervall 6: 0~15 C, Intervall 7: 15.1~20 C, Intervall 8: 20.1~25 C, Intervall 9: 25.1~30 C, Intervall 10: 30.1~40 C, Intervall 11: &gt; 40 C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MOD_COOL_TEMP_DELTA_RANGE_EINH | string | "zaehlen" |
| STAT_MOD_COOL_TEMP_DELTA_RANGE01_WERT | unsigned long | Intervall 1: -40~-30 C |
| STAT_MOD_COOL_TEMP_DELTA_RANGE02_WERT | unsigned long | Intervall 2: -29.9~-25 C |
| STAT_MOD_COOL_TEMP_DELTA_RANGE03_WERT | unsigned long | Intervall 3: -24.9~20.0 C |
| STAT_MOD_COOL_TEMP_DELTA_RANGE04_WERT | unsigned long | Intervall 4: -19.90~-15 C |
| STAT_MOD_COOL_TEMP_DELTA_RANGE05_WERT | unsigned long | Intervall 5: -14.9~-0.1 C |
| STAT_MOD_COOL_TEMP_DELTA_RANGE06_WERT | unsigned long | RIntervall 6: 0~15 C |
| STAT_MOD_COOL_TEMP_DELTA_RANGE07_WERT | unsigned long | Intervall 7: 15.1~20 C |
| STAT_MOD_COOL_TEMP_DELTA_RANGE08_WERT | unsigned long | Intervall 8: 20.1~25 C |
| STAT_MOD_COOL_TEMP_DELTA_RANGE09_WERT | unsigned long | Intervall 9: 25.1~30 C |
| STAT_MOD_COOL_TEMP_DELTA_RANGE10_WERT | unsigned long | Intervall 10: 30.1~40 C |
| STAT_MOD_COOL_TEMP_DELTA_RANGE11_WERT | unsigned long | Intervall 11: &gt; 40 C |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-uh-isolation-resi-histogram-lesen"></a>
### STATUS_UH_ISOLATION_RESI_HISTOGRAM_LESEN

Nutzung-Historie fuer den Isolationswiderstandwert, der in verschiedenen Widerstandsbereiche/Intervalle geht Intervall 1: &lt; 250 kOHMS, Intervall 2: 250~499 kOHMS, Intervall 3: 500~749 kOHMS, Intervall 4: 750~999 kOHMS, Intervall 5: &gt; 999 kOHMS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ISOL_RESI_EINH | string | "zaehlen" |
| STAT_ISOL_RESI01_WERT | unsigned long | Intervall 1: &lt; 250 kOHMS |
| STAT_ISOL_RESI02_WERT | unsigned long | Intervall 2: 250~499 kOHMS |
| STAT_ISOL_RESI03_WERT | unsigned long | Intervall 3: 500~749 kOHMS |
| STAT_ISOL_RESI04_WERT | unsigned long | Intervall 4: 750~999 kOHMS |
| STAT_ISOL_RESI05_WERT | unsigned long | Intervall 5: &gt; 999 kOHMS |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-lifetime-cnctr-closes-lesen"></a>
### STATUS_LIFETIME_CNCTR_CLOSES_LESEN

Nutzung-Historie fuer wieviel mal während der Lebensdauer der Hochvolt-Batterie, die Schuetzen geschlossen waren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CNCTR_CLOSES_EINH | string | "zaehlen" |
| STAT_CNCTR_CLOSES_WERT | unsigned long | Wieviel mal waren die Schuetzen geschlossen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-lifetime-12v-loss-lesen"></a>
### STATUS_LIFETIME_12V_LOSS_LESEN

Nutzung-Historie fuer wieviel mal ein Ausfall der 12v Spannung zum Kontroller waehrend der Lebensdauer geschah Die Bedeutung vom Zaehler ist zu bestimmen, wie oft während der Lebensdauer des FZGes Die 12 Volt Spannung mit geschlossenen Schuetzen oder ohne korrekten Auschaltmechanismus aus Grund eines zufaelligen 12v Ausfall verloren war

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_12V_LOSS_COUNTS_EINH | string | "zaehlen" |
| STAT_12V_LOSS_COUNTS_WERT | unsigned long | Totale Zaehlungen der 12V Ausfaelle |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-lifetime-min-ocv-lesen"></a>
### STATUS_LIFETIME_MIN_OCV_LESEN

die minimael erfasste Leerlaufspannung der Batterie waehrend der Lebensdauer Das BPCM speichert die minimale Leerlaufpannung der Batterie-Pack. die Leerlaufspannung (OCV) wird beim Startup bevor die Schuetzen geschlossen sind ein mal erfasst. wenn dieser Wert kleiner als der gespeicherten Wert ist, wird er als neuen minimalen Leerlauf-Pack-Spannung ueberschrieben.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_MIN_OCV_EINH | string | "Volts" |
| STAT_MIN_OCV_WERT | unsigned long | Min Wert von OCV |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-lifetime-cnctr-open-req-lesen"></a>
### STATUS_LIFETIME_CNCTR_OPEN_REQ_LESEN

Nutzung-Historie fuer wie oft der "Open Request" für die Schuetzen waehrend der Lebensdauer vom BPCM gesetzt sind Jedes mal wenn das BPCM vom HCP verlangt, die Schuetzen zu oeffnen, diese Datenspeicherung wird inkrementiert. Z.B: das BPCM feststellt, dass das FZG. die Schuetzen oeffnen soll und daher wird das BIT auf CAN gesetzt für die "OPEN REquest" -Bedingung. diese Datenspeicherung wird nur einmal inkrementiert. Es ist kein wiederholtes Inkrement im CAN-Signal.

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CNCTR_OPEN_REQ_EINH | string | "zaehlen" |
| STAT_CNCTR_OPEN_REQ_WERT | unsigned long | Total Contactor Open Request counts |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-lifetime-precharge-fails-lesen"></a>
### STATUS_LIFETIME_PRECHARGE_FAILS_LESEN

Nutzung-Historie fuer wie oft die Aufladuprozedur waehrend der Lebensdauer fehlgeschlagen war

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PRECHARGE_FAILS_EINH | string | "zaehlen" |
| STAT_PRECHARGE_FAILS_WERT | unsigned long | gesamte Zahl der fehgeschlagene Aufladungen |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-total-oepration-time-lesen"></a>
### STATUS_TOTAL_OEPRATION_TIME_LESEN

Nutzung Historie fuer wieviele Operationen der Batterie Pack waehrend eines Klemmenwechsels akkumuliert waren Das BPCM speichert die gesammte akkumulierte Zeit, in der er im Betrieb war, ab der Zeit wo der Kontroller geweckt ist bis er einschlaeft

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OPRN_TIME_EINH | string | "Sekunden" |
| STAT_OPRN_TIME_WERT | unsigned long | Wieviel mal der Kontroller im Betrieb war |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-total-cnctr-closing-time-lesen"></a>
### STATUS_TOTAL_CNCTR_CLOSING_TIME_LESEN

Nutzung-Historie fuer wieviel mal während der Lebensdauer der Hochvolt-Batterie, die Schuetzen geschlossen waren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CNCTR_CLOSES_TIME_EINH | string | "Sekunden" |
| STAT_CNCTR_CLOSES_TIME_WERT | unsigned long | Gesamte Zeit der Schuetzenabschliessung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cumulative-charge-amp-hours-lesen"></a>
### STATUS_CUMULATIVE_CHARGE_AMP_HOURS_LESEN

Total akkumulierter Wert der Batterieladung seit der ersten Nutzung RESOLUTION  1 Ampere/Stunde

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CHRG_AMP_HOURS_EINH | string | "Ampere/Stunde" |
| STAT_CHRG_AMP_HOURS_WERT | real | wert in Ampere/Stunde |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cumulative-discharge-amp-hours-lesen"></a>
### STATUS_CUMULATIVE_DISCHARGE_AMP_HOURS_LESEN

Total akkumulierter Wert der Batterieentladung seit der ersten Nutzung RESOLUTION 1 Ampere/Stunde

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DISCHRG_AMP_HOURS_EINH | string | "Ampere/Stunde" |
| STAT_DISCHRG_AMP_HOURS_WERT | real | wert in Ampere/Stunde |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-lifetime-cnctr-opens-lesen"></a>
### STATUS_LIFETIME_CNCTR_OPENS_LESEN

Nutzung-Historie fuer wieviel mal während der Lebensdauer der Hochvolt-Batterie, die Schuetzen offen waren Auch die Nutzung-Historie für wieviel der Lebensdauer der Batterie, die Schuetzen offen waren unter "Impending-Open" Bedingung und Nutzung-Historie fuer wieviel mal waren die schuetzen offen unter hoehen Strombelastung waehrend Lebensdauer Jedes mal wenn die Schuetzen aus irgend ein Grund offen sind, wenn der absolute Wert (Plus oder minus) des Stroms grosser als 5 Ampere

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_TOTAL_CNCTR_OPENS_EINH | string | "zaehlen" |
| STAT_TOTAL_CNCTR_OPENS_WERT | unsigned long | wieviel mal waren die Schuetzen offen |
| STAT_CNCTR_OPEN_UNDER_LOAD_EINH | string | "zaehlen" |
| STAT_CNCTR_OPEN_UNDER_LOAD_WERT | unsigned long | wieviel mal waren die schuetzen offen unter hoehen Strombelastung |
| STAT_CNCTR_IMPEND_OPENS_EINH | string | "zaehlen" |
| STAT_CNCTR_IMPEND_OPENS_WERT | unsigned long | wieviel mal waren die Schuetzen offen unter "Impending-Open" Bedingung |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |
| _REQUEST2 | binary | Hex-Auftrag an SG |
| _RESPONSE2 | binary | Hex-Antwort von SG |
| _REQUEST3 | binary | Hex-Auftrag an SG |
| _RESPONSE3 | binary | Hex-Antwort von SG |

<a id="job-status-uh-bat-resi-histogram-lesen"></a>
### STATUS_UH_BAT_RESI_HISTOGRAM_LESEN

Nutzung-Historie fuer wieviel mal der Batteriewiderstand in verschiedenen Widerstandbereiche/Intervalle geht Intervall 1: 0-100 mOhms, Intervall 2: 101-500 mOhms, Intervall 3: 501-1000 mOhms, Intervall 4: 1001-1500 mOhms, Intervall 5: 1501-2000 mOhms Intervall 6: 2001-2500 mOhms, Intervall 7: 2501-3000 mOhms, Intervall 8: 3001-3500 mOhms, Intervall 9: 3501-4000 mOhms Intervall 10: 4001-4500 mOhms, Intervall 11: 4501-5000 mOhms

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RESI_RANGE01_EINH | string | "zaehlen" |
| STAT_RESI_RANGE01_WERT | unsigned long | Intervall 1: 0-100 mOhms |
| STAT_RESI_RANGE02_EINH | string | "zaehlen" |
| STAT_RESI_RANGE02_WERT | unsigned long | Intervall 2: 101-500 mOhms |
| STAT_RESI_RANGE03_EINH | string | "zaehlen" |
| STAT_RESI_RANGE03_WERT | unsigned long | Intervall 3: 501-1000 mOhms |
| STAT_RESI_RANGE04_EINH | string | "Stunden" |
| STAT_RESI_RANGE04_WERT | unsigned long | Intervall 4: 1001-1500 mOhms |
| STAT_RESI_RANGE05_EINH | string | "zaehlen" |
| STAT_RESI_RANGE05_WERT | unsigned long | Intervall 5: 1501-2000 mOhms |
| STAT_RESI_RANGE06_EINH | string | "zaehlen" |
| STAT_RESI_RANGE06_WERT | unsigned long | Intervall 6: 2001-2500 mOhms |
| STAT_RESI_RANGE07_EINH | string | "zaehlen" |
| STAT_RESI_RANGE07_WERT | unsigned long | Intervall 7: 2501-3000 mOhms |
| STAT_RESI_RANGE08_EINH | string | "zaehlen" |
| STAT_RESI_RANGE08_WERT | unsigned long | Intervall 8: 3001-3500 mOhms |
| STAT_RESI_RANGE09_EINH | string | "zaehlen" |
| STAT_RESI_RANGE09_WERT | unsigned long | Intervall 9: 3501-4000 mOhms |
| STAT_RESI_RANGE10_EINH | string | "zaehlen" |
| STAT_RESI_RANGE10_WERT | unsigned long | Intervall 10: 4001-4500 mOhms |
| STAT_RESI_RANGE11_EINH | string | "zaehlen" |
| STAT_RESI_RANGE11_WERT | unsigned long | Intervall 11: 4501-5000 mOhms |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-soc-5day-history"></a>
### STATUS_SOC_5DAY_HISTORY

Ladezustand-Historie mit STAT_AMPRH_CHG_WERT Integrationswerte in der letzten 6 Tagen ab heute das Ziel dieser gespeicherten Daten und der Ladenzustand-Historie am Tag X, ist eine Hilfe für die Service, um festzustellen was am Batterie in den letzten 5 Betriebstagen geschah. die Ladezustandswerte und die Delta der Amp/Stunde (Ladung und Entladung) sind Snapschuesse an einem bestimmten Tag. Der Ladezustand bei Klemme 30, Ampere/Stunden (Ladung und Entladung) - Delta-Wert vom letzten Betriebstag

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SOC_EINH | string | "%" |
| STAT_AMPHR_DISCHG_EINH | string | "AmpHours" |
| STAT_AMPHR_CHG_EINH | string | "AmpHours" |
| STAT_SOC_DAY0_WERT | real | Betriebstag 0 (Heute) Ladezustand-Wert |
| STAT_DAY0_AMPHR_DISCHG_WERT | real | Betriebstag 0 (Heute) Ampere/Stunde Entladung Delta-Wert vom letzten Betriebstag |
| STAT_DAY0_AMPHR_CHG_WERT | real | Betriebstag 0 (Heute) Ampere/Stunde Ladung Delta-Wert vom letzten Betriebstag |
| STAT_SOC_DAY1_WERT | real | Betreibstag 1 Ladezustand-Wert |
| STAT_DAY1_AMPHR_DISCHG_WERT | real | Betriebstag 1 Ampere/Stunde Entladung Delta-Wert vom letzten Betriebstag |
| STAT_DAY1_AMPHR_CHG_WERT | real | Betriebstag 1 Ampere/Stunde Ladung Delta-Wert vom letzten Betriebstag |
| STAT_SOC_DAY2_WERT | real | Betreibstag 2 Ladezustand-Wert |
| STAT_DAY2_AMPHR_DISCHG_WERT | real | Betriebstag 2 Ampere/Stunde Entladung Delta-Wert vom letzten Betriebstag |
| STAT_DAY2_AMPHR_CHG_WERT | real | Betriebstag 2 Ampere/Stunde Ladung Delta-Wert vom letzten Betriebstag |
| STAT_SOC_DAY3_WERT | real | Betreibstag 3 Ladezustand-Wert |
| STAT_DAY3_AMPHR_DISCHG_WERT | real | Betriebstag 3 Ampere/Stunde Entladung Delta-Wert vom letzten Betriebstag |
| STAT_DAY3_AMPHR_CHG_WERT | real | Betriebstag 3 Ampere/Stunde Ladung Delta-Wert vom letzten Betriebstag |
| STAT_SOC_DAY4_WERT | real | Betreibstag 4 Ladezustand-Wert |
| STAT_DAY4_AMPHR_DISCHG_WERT | real | Betriebstag 4 Ampere/Stunde Entladung Delta-Wert vom letzten Betriebstag |
| STAT_DAY4_AMPHR_CHG_WERT | real | Betriebstag 4 Ampere/Stunde Ladung Delta-Wert vom letzten Betriebstag |
| STAT_SOC_DAY5_WERT | real | Betreibstag 5 Ladezustand-Wert |
| STAT_DAY5_AMPHR_DISCHG_WERT | real | Betriebstag 5 Ampere/Stunde Entladung Delta-Wert vom letzten Betriebstag |
| STAT_DAY5_AMPHR_CHG_WERT | real | Betriebstag 5 Ampere/Stunde Ladung Delta-Wert vom letzten Betriebstag |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST0 | binary | Hex-Auftrag an SG |
| _RESPONSE0 | binary | Hex-Antwort von SG |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |
| _REQUEST2 | binary | Hex-Auftrag an SG |
| _RESPONSE2 | binary | Hex-Antwort von SG |
| _REQUEST3 | binary | Hex-Auftrag an SG |
| _RESPONSE3 | binary | Hex-Antwort von SG |
| _REQUEST4 | binary | Hex-Auftrag an SG |
| _RESPONSE4 | binary | Hex-Antwort von SG |

<a id="job-status-uh-hvbp-coolant-temp-delta-histogram-lesen"></a>
### STATUS_UH_HVBP_COOLANT_TEMP_DELTA_HISTOGRAM_LESEN

Nutzung-Historie fuer wieviel mal die Temperaturdiffirenz für das HVBP-Kuehlmittel-Einlass und Auslass in einem verschiedenen Temperaturbereich geht Intervall 1: &lt; 0 C, Intervall 2: 0~1 C, Intervall 3: 1~2 C, Intervall 4: 2~3 C, Intervall 5: 3~4 C Intervall 6: 4~5 C, Intervall 7: 5~6 C, Intervall 8: 6~7 C, Intervall 9: 7~9 C, Intervall 10: 9~11 C, Intervall 11: 11~13 C Intervall 12: 13~15 c, Intervall 13: &gt; 15 C

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_COOLANT_TEMP_DELTA_RANGE_EINH | string | "zaehlen" |
| STAT_COOLANT_TEMP_DELTA_RANGE01_WERT | unsigned long | Intervall 1: &lt; 0 C |
| STAT_COOLANT_TEMP_DELTA_RANGE02_WERT | unsigned long | Intervall 2: 0~1 C |
| STAT_COOLANT_TEMP_DELTA_RANGE03_WERT | unsigned long | Intervall 3: 1~2 C |
| STAT_COOLANT_TEMP_DELTA_RANGE04_WERT | unsigned long | Intervall 4: 2~3 C |
| STAT_COOLANT_TEMP_DELTA_RANGE05_WERT | unsigned long | Intervall 5: 3~4 C |
| STAT_COOLANT_TEMP_DELTA_RANGE06_WERT | unsigned long | Intervall 6: 4~5 C |
| STAT_COOLANT_TEMP_DELTA_RANGE07_WERT | unsigned long | Intervall 7: 5~6 C |
| STAT_COOLANT_TEMP_DELTA_RANGE08_WERT | unsigned long | Intervall 8: 6~7 C |
| STAT_COOLANT_TEMP_DELTA_RANGE09_WERT | unsigned long | Intervall 9: 7~9 C |
| STAT_COOLANT_TEMP_DELTA_RANGE10_WERT | unsigned long | Intervall 10: 9~11 C |
| STAT_COOLANT_TEMP_DELTA_RANGE11_WERT | unsigned long | Intervall 11: 11~13 C |
| STAT_COOLANT_TEMP_DELTA_RANGE12_WERT | unsigned long | Intervall 12: 13~15 C |
| STAT_COOLANT_TEMP_DELTA_RANGE13_WERT | unsigned long | Intervall 13: &gt; 15 C |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-weld-check-lesen"></a>
### STATUS_WELD_CHECK_LESEN

Ergebnisse vom Schweiss-Check -Ablauf für das Hochvolt Batterie Pack (HVBP) zeigt, ob eine oder beide Hochvoltleitungen der Schuetze(n) verschweisst ist (sind)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_POSITIVE_RAIL_CNCTR_WELD_INDEX | unsigned char | Index zeigt, ob der (die) Contactor(s) der positiven Leitung verschweisst ist (sind) |
| STAT_POSITIVE_RAIL_CNCTR_WELD_TEXT | string | TEXT zeigt, ob der (die) Contactor(s) der positiven Leitung verschweisst ist (sind) Die positive Leitung hat zwei Contactors- +VE Main und Vorladung (precharge) Das Ergebnis wird als Wahr gesetzt, wenn ein oder beide Contactors verschweisst sind |
| STAT_NEGATIVE_RAIL_CNCTR_WELD_INDEX | unsigned char | INDEX zeigt, ob der Contactor der negativen Leitung verschweisst ist |
| STAT_NEGATIVE_RAIL_CNCTR_WELD_TEXT | string | TEXT zeigt, ob der Contactor der negativen Leitung verschweisst ist Die negative Leitung hat einen Contactor - -VE MAIN Das Ergebnis wird als Wahr gesetzt, wenn der -VE MAIN Contactor verschweisst ist |
| STAT_BOTH_RAIL_CNCTR_WELD_INDEX | unsigned char | INDEX zeigt ob die contactors beider Leitungen verschweisst sind |
| STAT_BOTH_RAIL_CNCTR_WELD_TEXT | string | TEXT zeigt, ob beide Contactors veschweisst sind Das Ergebnis wird als Wahr gesetzt, wenn ein oder beide Contactors der positiven oder negativen Leitung verschweisst sind |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |
| _REQUEST2 | binary | Hex-Auftrag an SG |
| _RESPONSE2 | binary | Hex-Antwort von SG |

<a id="job-status-open-cable-lesen"></a>
### STATUS_OPEN_CABLE_LESEN

TO READ OUT THE OPEN CABLE DETECTION TEST RESULT AND THE OPEN CABLE DETECTION CIRCUIT CHECK RESULT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_OCD_RESULT_INDEX | unsigned char | Index zeigt, ob die Leitungsunterbrechung- (open cable Detection) Testergebnis bestanden oder nicht bestanden ist |
| STAT_OCD_RESULT_TEXT | string | TEXT zeigt, die Leitungsunterbrechung- (open cable Detection) Testergebnis bestanden oder nicht bestanden ist |
| STAT_OCD_CKT_RESULT_INDEX | unsigned char | INDEX zeigt, ob die Leitungsunterbrechungskreis- (open cable Detection circuit) Testergebnis bestanden oder nicht bestanden ist |
| STAT_OCD_CKT_RESULT_TEXT | string | TEXT zeigt, ob die Leitungsunterbrechungskreis- (open cable Detection circuit) Testergebnis bestanden oder nicht bestanden ist |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST1 | binary | Hex-Auftrag an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |

<a id="job-status-batt-change-odometer"></a>
### STATUS_BATT_CHANGE_ODOMETER

Fzg.- ODOMETER-Wert vom letzten Batteriewechsel auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ODOMETER_EINH | real | Die Einheit des Fahrzeugsodometers+ |
| STAT_ODOMETER_WERT | real | zeigt, wann wurde die Batterie zuletzt ausgewechselt |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-fault-check-lesen"></a>
### _STATUS_FAULT_CHECK_LESEN

SHOWS THE STATUS OF DIFFERENT FAULT CHECK AND REMEDIAL ACTION FUNCTIONALITIES THAT IF THE FUNCTIONALITIES IS ENABLED OR DISABLED

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ISOLATION_DETECT_INDEX | unsigned char | INDEX SHOWING IF THE ISOLATION DETECTION FUNCTIONALITY IS ENABLED OR DISABLED |
| ISOLATION_DETECT_TEXT | string | TEXT SHOWING IF THE ISOLATION DETECTION FUNCTIONALITY IS ENABLED OR DISABLED |
| OPEN_CABLE_DETECT_INDEX | unsigned char | INDEX SHOWING IF THE OPEN CABLE DETECTION FUNCTIONALITY IS ENABLED OR DISABLED |
| OPEN_CABLE_DETECT_TEXT | string | TEXT SHOWING IF THE OPEN CABLE DETECTION FUNCTIONALITY IS ENABLED OR DISABLED |
| OPEN_CABLE_CKT_DETECT_INDEX | unsigned char | INDEX SHOWING IF THE OPEN CABLE CIRCUIT DETECTION FUNCTIONALITY IS ENABLED OR DISABLED |
| OPEN_CABLE_CKT_DETECT_TEXT | string | TEXT SHOWING IF THE OPEN CABLE CIRCUIT DETECTION FUNCTIONALITY IS ENABLED OR DISABLED |
| WELD_CHECK_INDEX | unsigned char | INDEX SHOWING IF THE WELD CHECK AND ACTIVE DISCHARGE FUNCTIONALITY IS ENABLED OR DISABLED |
| WELD_CHECK_TEXT | string | TEXT SHOWING IF THE WELD CHECK AND ACTIVE DISCHARGE FUNCTIONALITY IS ENABLED OR DISABLED |
| WELD_CHECK_INHIBIT_CLOSING_INDEX | unsigned char | INDEX SHOWING IF THE CONTACTORS ARE INHIBITED TO CLOSE BECAUSE BOTH RAIL CONTACTORS ARE WELDED |
| WELD_CHECK_INHIBIT_CLOSING_TEXT | string | TEXT SHOWING IF THE CONTACTORS ARE INHIBITED TO CLOSE BECAUSE BOTH RAIL CONTACTORS ARE WELDED |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST1 | binary | Hex-request an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |
| _REQUEST2 | binary | Hex-request an SG |
| _RESPONSE2 | binary | Hex-Antwort von SG |
| _REQUEST3 | binary | Hex-request an SG |
| _RESPONSE3 | binary | Hex-Antwort von SG |
| _REQUEST4 | binary | Hex-request an SG |
| _RESPONSE4 | binary | Hex-Antwort von SG |

<a id="job-status-wake-up-signals-lesen"></a>
### _STATUS_WAKE_UP_SIGNALS_LESEN

SHOWS THE STATUS OF WAKE UP SIGNALS FOR BPCM - HYBRID ACCESSORY AND HS COMMUNICATION ENABLE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_HSCOM_INDEX | unsigned char | INDEX SHOWING IF THE HS COMM ENABLE SIGNAL TO BPCM IS TRUE (HIGH) OR FALSE (LOW) |
| STAT_HSCOM_TEXT | string | TEXT SHOWING IF THE HS COMM ENABLE SIGNAL TO BPCM IS TRUE (HIGH) OR FALSE (LOW) |
| STAT_HYB_ACC_INDEX | unsigned char | INDEX SHOWING IF THE HYBRID ACCESSORY SIGNAL TO BPCM IS TRUE (HIGH) OR FALSE (LOW) |
| STAT_HYB_ACC_TEXT | string | TEXT SHOWING IF THE HYBRID ACCESSORY SIGNAL TO BPCM IS TRUE (HIGH) OR FALSE (LOW) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-contactor-closure-enable-lesen"></a>
### STATUS_CONTACTOR_CLOSURE_ENABLE_LESEN

Auslesen von Wert des Schuetze-Schliessen Aktivierungsbits geschrieben von "STEUERN_CONTACTOR_CLOSURE_ENABLE" JOB

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_CNTCR_CLOSE_ENBL_BIT_WERT | unsigned int | Wert des Schuetze-Schliessen Aktivierungsbits |
| STAT_CNTCR_CLOSE_ENBL_BIT_TEXT | string | Schuetze-Schliessen Aktivierungsbit - aktivieren oder deaktivieren |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-contactor-closure-enable"></a>
### STEUERN_CONTACTOR_CLOSURE_ENABLE

Bit wird gesetzt oder nicht gesetzt, um die Schuetze-Schliessen zu aktivieren oder deaktivieren Bei Deaktivierung des Schutzen-Scliessens bewirkt, dass die Schuetzen sich nicht schliessen mit dem Befehl von HCP bis das Schutzen-Schliessen aktiviert wird Warnung -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CLOSURE_ENABLE | unsigned int | Werttabelle 0 = Disable (HCP -Befehl kann die Schuetzen nicht schliessen) 1 = Enable  (HCP -Befehl kann die Schuetzen schliessen) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-pump-enable-lesen"></a>
### STATUS_PUMP_ENABLE_LESEN

Auslesen von Wert des Schuetze-Schliessen Aktivierungsbits geschrieben von "STEUERN_PUMP_ENABLE" JOB

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PUMP_ENBL_BIT_WERT | unsigned int | Wert des Aktivierungsbits der Pumpe |
| STAT_PUMP_ENBL_BIT_TEXT | string | Aktivierungsbit der Pumpe - aktiv oder inaktiv |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-pump-enable"></a>
### STEUERN_PUMP_ENABLE

Bit wird gesetzt, um die Pumpe zu aktivieren bzw. deaktivieren Deaktivierung der Pumpen-Kontrolle bewirkt, dass die Pumpe nicht laufen wird Mit internen BPCM-Logik oder bei Ueberschreibung des Befehls vom HCP oder bei Pumpen-Ansteuerung SGBD JOB Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PUMP_ENABLE | unsigned int | Werttabelle 0 = Disable (Pumpe kann nicht in jeder Lage Laufen) 1 = Enable  (Pumpe kann in jeder Lage Laufen) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-cool-pump"></a>
### STEUERN_COOL_PUMP

Dieser Job dient den Betrieb von Hochvolt-Batterie Pack-Kuehlmittel PUMPE benutzt extern das das Diagnose-Tool WARNUNG -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ENABLE_PUMP_CONTROL | unsigned int | Werttabelle 0 = DISABLE_CONTROL 1 = ENABLE_CONTROL |
| DESIRED_PUMP_SPEED | unsigned int | gewuenschte Pumpengeschwindigkeit : 0-100% |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-cool-pump-return-control"></a>
### STEUERN_COOL_PUMP_RETURN_CONTROL

Die Kontrolle wiederzubekommen nach Durchfuehrung des	 "STEUERN_COOL_PUMP" JOB Warnung -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-cool-pump-lesen"></a>
### STATUS_COOL_PUMP_LESEN

Das BPCM sendet diese Ergebnisse und jede FAULT CODES waehrend der Zeit der Durchfuehrung von "PUMP Control" falls angefordert durch STEUERN JOB

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RETURN_CODE_INDEX | unsigned int | zeigt RETURN CODE INDEX |
| STAT_RETURN_CODE_TEXT | string | zeigt RETURN CODE TEXT |
| STAT_PUMP_SPEED_EINH | string | "%" |
| STAT_PUMP_SPEED_WERT | real | zeigt die aktuelle Pumpengeschwindigkeit, die von der Pumpe erhalten wurde (PWM Signal) |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-batt-change-odometer"></a>
### STEUERN_BATT_CHANGE_ODOMETER

TO ENTER THE VEHICLE ODOMETER VALUE AT EVERY BATTERY CHANGE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CHANGE_ODOMETER | unsigned int | ENTER 1 um den letzten gespeicherten ODOMETER - Wert zu ueberschreiben ENTER 0 um den letzten gespeicherten ODOMETER - Wert zu behalten |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-isol-test"></a>
### STEUERN_ISOL_TEST

Starten des Isolationstests durch das Service-Tool Warnung -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ISOLATION_TEST_COMMAND | unsigned int | Werttabelle 0 = STOP 1 = START Bitte 1 zum Test-start oder 0 zum Test-Stopp eingeben |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-isol-test-return-control"></a>
### STEUERN_ISOL_TEST_RETURN_CONTROL

Die Kontrolle wiederzubekommen nach Durchfuehrung von "STEUERN_ISOL_TEST" JOB Warnung -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-isol-test-lesen"></a>
### STATUS_ISOL_TEST_LESEN

BPCM sendet diese Resultate und Fault-CODES waehrend Ausfuehrung von ISOLATION TEST aufgefordert durch "STEUERN" JOB

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RETURN_CODE_INDEX | unsigned int | zeigt RETURN CODE INDEX |
| STAT_RETURN_CODE_TEXT | string | zeigt RETURN CODE TEXT |
| STAT_TEST_CMND_INDEX | unsigned int | zeigt SET INDEX fuer ISOLATION TEST COMMAND |
| STAT_TEST_CMND_TEXT | string | zeigt SET TEXT fuer ISOLATION TEST COMMAND |
| STAT_ISOL_TEST_INDEX | unsigned int | zeigt ISOLATION TEST Ergebnis INDEX |
| STAT_ISOL_TEST_TEXT | string | zeigtE ISOLATION TEST Ergebnis IN TEXT |
| STAT_RESI_NEG_LEG_EINH | string | "Meg Ohm" |
| STAT_RESI_NEG_LEG_WERT | real | zeigt den Isolationswiderstand, dass am negativen Strang waehred des Isolationstests gemessen wurde aufgefordert durch "STEUERN" JOB |
| STAT_RESI_POS_LEG_EINH | string | "Meg Ohm" |
| STAT_RESI_POS_LEG_WERT | real | zeigt den Isolationswiderstand, der waehrend des Isolationstests am positiven Strang gemessen wurde aufgefordert durch "STEUERN" JOB |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-clear-pump-dryrun-off"></a>
### STEUERN_CLEAR_PUMP_DRYRUN_OFF

RESET die Pumpen-Trockenlauf SWITCH OFF FLAG Warnung -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CLEAR_DRYRUN_OFF | unsigned int | Werttabelle 0 = Don't Reset 1 = Reset ENTER 0 nicht loeschen PUMP DRY RUN OFF ENTER 1 loeschen PUMP DRY RUN OFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-clear-dryrun-off-return-control"></a>
### STEUERN_CLEAR_DRYRUN_OFF_RETURN_CONTROL

Die Kontrolle wiederzubekommen nach Durchfuehrung von "STEUERN_CLEAR_DRYRUN_OFF" JOB Warnung -&gt; Dieser Job sollte nicht von einer Person ohne ausreichende Systemkenntnisse durchgefuehrt werden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-clear-dryrun-off-lesen"></a>
### STATUS_CLEAR_DRYRUN_OFF_LESEN

BPCM sendet diese Resultate und Fault-CODES waehrend Ausfuehrung von CLEAR PUMP Trockenlauf SWITCH OFF aufgefordert durch "STEUERN" JOB

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_RETURN_CODE_INDEX | unsigned int | zeigt RETURN CODE INDEX |
| STAT_RETURN_CODE_TEXT | string | zeigt RETURN CODE TEXT |
| STAT_DRYRUN_IN_PROGRESS_INDEX | unsigned int | zeigt INDEX wenn das Loeschen von Trockenlauf SWITCH OFF durchgefuehrt wird |
| STAT_DRYRUN_IN_PROGRESS_TEXT | string | zeigt TEXT wenn das Loeschen von Trockenlauf SWITCH OFF durchgefuehrt wird |
| STAT_TIME_LEFT_TO_CLEAR_EINH | string | "Seconds" |
| STAT_TIME_LEFT_TO_CLEAR_WERT | unsigned int | zeigt wieviele Zeit zum loeschen von Trockenlauf OFF FLAG geblieben ist |
| STAT_DRYRUN_CLEARED_INDEX | unsigned int | zeigt INDEX wenn der Trockenlauf SWITCH OFF FLAG ist geloescht |
| STAT_DRYRUN_CLEARED_TEXT | string | zeigt TEXT wenn der Trockenlauf SWITCH OFF FLAG ist geloescht |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-fault-check-disabler"></a>
### _STEUERN_FAULT_CHECK_DISABLER

TO ENABLE OR DISABLE DIFFERENT FAULT CHECK TESTS THIS INCLUDES THE FAULT CHECK TESTS OF ISOLATION DETECTION WITH CLOSED CONTACTORS, OPEN CABLE DETECTION, OPEN CABLE DETECTION CIRCUIT CHECK AND WELD CHECK & ACTIVE DISCHARGE TEST

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ISOL_TEST | unsigned int | PUT 0 OR 1 FOR DISABLING OR ENABLING THE ISOLATION DETECTION TEST WITH CLOSED CONTACTORS 0 = DISABLE 1 = ENABLE |
| OCD | unsigned int | PUT 0 OR 1 FOR DISABLING OR ENABLING THE ISOLATION DETECTION TEST WITH CLOSED CONTACTORS 0 = DISABLE 1 = ENABLE |
| OCD_CIRCUIT_CHECK | unsigned int | PUT 0 OR 1 FOR DISABLING OR ENABLING THE ISOLATION DETECTION TEST WITH CLOSED CONTACTORS 0 = DISABLE 1 = ENABLE |
| WELD_CHECK_TEST | unsigned int | PUT 0 OR 1 FOR DISABLING OR ENABLING THE ISOLATION DETECTION TEST WITH CLOSED CONTACTORS 0 = DISABLE 1 = ENABLE |
| WELD_CHECK_CNTCR_INHIBIT | unsigned int | PUT 0 OR 1 FOR DISABLING OR ENABLING THE CONTACTOR CLOSURE AFTER FAILED WELD CHECK 0 = DISABLE 1 = ENABLE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| _REQUEST1 | binary | Hex-request an SG |
| _RESPONSE1 | binary | Hex-Antwort von SG |
| _REQUEST2 | binary | Hex-request an SG |
| _RESPONSE2 | binary | Hex-Antwort von SG |
| _REQUEST3 | binary | Hex-request an SG |
| _RESPONSE3 | binary | Hex-Antwort von SG |

<a id="job-bse-init-states"></a>
### _BSE_INIT_STATES

BSE INITIALIZATION PARAMETERS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| TIMESTAMP_EINH | string | "Seconds" |
| TIMESTAMP_WERT | unsigned long | None |
| TIMESTAMP_VALID | unsigned int | None |
| TIMESTAMP_VALID_TEXT | string | None |
| MAZ_NEU_EINH | string | "seconds" |
| MAZ_NEU_WERT | unsigned long | None |
| MAZ_NEU_VLD | unsigned int | None |
| MAZ_NEU_VLD_TEXT | string | None |
| INIT_PACK_CURRENT_EINH | string | "Amps" |
| INIT_PACK_CURRENT_WERT | real | None |
| INIT_OCV_EINH | string | "V" |
| INIT_OCV_WERT | real | None |
| B_PROPER_SHUTDOWN | unsigned int | None |
| B_PROPER_SHUTDOWN_TEXT | string | None |
| NUMOFMODULES_WERT | unsigned long | None |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-bse-bpcm-input"></a>
### _BSE_BPCM_INPUT

BSE INPUTS FROM BPCM SW, MAINLY THE SENSOR VALUES

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| I_CURRENT_EINH | string | "Amps" |
| I_CURRENT_WERT | real | None |
| T_TEMPERATURE_EINH | string | "C" |
| T_TEMPERATURE_WERT | real | None |
| CNTCTRSTAT | unsigned int | None |
| CNTCTRSTAT_TEXT | string | None |
| B_CONTACTOR_COMMAND | unsigned int | None |
| B_CONTACTOR_COMMAND_TEXT | string | None |
| B_HS_COMM | unsigned int | None |
| B_HS_COMM_TEXT | string | None |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-bse-bsec-data"></a>
### _BSE_BSEC_DATA

None

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| VEBSEC_K_BSEINITSTATE | unsigned int | None |
| SOCACC_EINH | string | "%" |
| SOCACC_WERT | real | None |
| VEBSEC_U_HB_OCV_EINH | string | "V" |
| VEBSEC_U_HB_OCV_WERT | real | None |
| VEBSEC_P_HB_PREGENMAX_EINH | string | "kW" |
| VEBSEC_P_HB_PREGENMAX_WERT | real | None |
| VEBSEC_P_HB_PDISLUT_EINH | string | "kW" |
| VEBSEC_P_HB_PDISLUT_WERT | real | None |
| VEBSEC_P_HB_PCHGLUT_EINH | string | "kW" |
| VEBSEC_P_HB_PCHGLUT_WERT | real | None |
| VEBSEC_HB_TAU | real | None |
| VEBSEC_B_SOCRESET | unsigned int | None |
| VEBSEC_B_SOCRESET_TEXT | string | None |
| VEBSEC_B_REG | unsigned int | None |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-bse-eeprom-data-01"></a>
### _BSE_EEPROM_DATA_01

EEPROM DATA - INPUT TO BSE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EE_V0_OLD_EINH | string | "V" |
| EE_V0_OLD_WERT | real | None |
| SOH_EINH | string | "%" |
| EE_SOH_WERT | real | None |
| EE_SOCACC_OLD_EINH | string | "%" |
| EE_SOCACC_OLD_WERT | real | None |
| EE_SOC_OLD_EINH | string | "%" |
| EE_SOC_OLD_WERT | real | None |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-bse-eeprom-data-02"></a>
### _BSE_EEPROM_DATA_02

EEPROM DATA - INPUT TO BSE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| EE_VDIFF_OLD_EINH | string | "V" |
| EE_VDIFF_OLD_WERT | real | None |
| EE_VH_OLD_EINH | string | "V" |
| EE_VH_OLD_WERT | real | None |
| EE_E_WERT | real | None |
| EE_A_WERT | real | None |
| EE_VDBLC_OLD_EINH | string | "V" |
| EE_VDBLC_OLD_WERT | real | None |
| EE_VOC_REG_OLD_EINH | string | "V" |
| EE_VOC_REG_OLD_WERT | real | None |
| EE_VH_V0_OLD_WERT | real | None |
| EE_VH_V0_OLD_EINH | string | "V" |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-bse-api-data-01"></a>
### _BSE_API_DATA_01

BSE API OUTPUTS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SOC_VOLT_EINH | string | "V" |
| SOC_VOLT_WERT | real | None |
| SOC_AHR_EINH | string | "%" |
| SOC_AHR_WERT | real | None |
| B_SOC_RESET_ANZ | unsigned int | None |
| BSE_OFF_TIME_EINH | string | "s" |
| BSE_OFF_TIME_WERT | unsigned long | None |
| BSE_OFF_TIME_VLD | unsigned int | None |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-bse-api-data-02"></a>
### _BSE_API_DATA_02

BSE API OUTPUTS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| OCV_EINH | string | "V" |
| OCV_WERT | real | None |
| B_REG | unsigned int | None |
| PP_CHG_LUT_EINH | string | "kW" |
| PP_CHG_LUT_WERT | real | None |
| PP_DIS_LUT_EINH | string | "kW" |
| PP_DIS_LUT_WERT | real | None |
| BLEND_SOC_ANZ | real | None |
| R_EINH | string | "Ohm" |
| R_WERT | real | None |
| TAU_WERT | real | None |
| C_EINH | string | "As/V" |
| C_WERT | real | None |
| V_DBLA_EINH | string | "V" |
| V_DBLA_WERT | real | None |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-bse-api-data-03"></a>
### _BSE_API_DATA_03

BSE API OUTPUTS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PREGENMAX_EINH | string | "kW" |
| PREGENMAX_WERT | real | None |
| VR_EINH | string | "V" |
| VR_WERT | real | None |
| I_CURRENT_EINH | string | "Amps" |
| I_CURRENT_WERT | real | None |
| BSE_ACC_EINH | string | "%" |
| BSE_ACC_WERT | real | None |
| REG_ONOFF_RATIO_EINH | string | "%" |
| REG_ONOFF_RATIO_WERT | real | None |
| B_BSE_OVERPREDICT | unsigned int | None |
| REG_ON_TIME_EINH | string | "s" |
| REG_ON_TIME_WERT | real | None |
| REG_OFF_TIME_EINH | string | "s" |
| REG_OFF_TIME_WERT | real | None |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-write-soc-old"></a>
### _WRITE_SOC_OLD

TO OVERWRITE THE OLD SOC VALUE STORED IN THE EEPROM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NEW_SOC_OLD | unsigned int | ENTER THE NEW DESIRED STORED SOC TO BE OVERWRITTEN TO THE EEPROM |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-write-amphr-charge"></a>
### _WRITE_AMPHR_CHARGE

TO OVERWRITE THE AMP-HR CHARGE VALUE STORED IN THE EEPROM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NEW_AMP_CHRG_OLD | unsigned long | ENTER THE NEW DESIRED STORED AMP-HR CHARGE TO BE OVERWRITTEN TO THE EEPROM |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-write-amphr-discharge"></a>
### _WRITE_AMPHR_DISCHARGE

TO OVERWRITE THE AMP-HR CHARGE VALUE STORED IN THE EEPROM

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| NEW_AMP_DISCHRG_OLD | unsigned long | ENTER THE NEW DESIRED STORED AMP-HR CHARGE TO BE OVERWRITTEN TO THE EEPROM |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-load-check-enabler"></a>
### _STEUERN_LOAD_CHECK_ENABLER

TO ENABLE OR DISABLE LOAD CHECK AND SHORTED BUS DETECTION FUNCTIONALITY

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ENABLE_DISABLE | unsigned int | PUT 0 OR 1 FOR DISABLING OR ENABLING THE LOAD CHECK AND SHORTED BUS DETECTION 0 = DISABLE 1 = ENABLE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-load-check-enabler"></a>
### _STATUS_LOAD_CHECK_ENABLER

TO READ OUT THE LOAD CHECK AND SHORTED BUS DETECTION ENABLER BIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| LOAD_CHECK_ENBL_BIT_WERT | unsigned int | Wert des Schuetze-Schliessen Aktivierungsbits |
| LOAD_CHECK_ENBL_BIT_TEXT | string | Schuetze-Schliessen Aktivierungsbit - aktivieren oder deaktivieren |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-service-can-enabler"></a>
### _SERVICE_CAN_ENABLER

TO ENABLE OR DISABLE SERVICE CAN COMMUNICATION

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ENABLE_DISABLE | unsigned int | PUT 0 OR 1 FOR DISABLING OR ENABLING THE SERVICE CAN COMMUNICATION 0 = DISABLE 1 = ENABLE |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-request an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-service-can-enabler"></a>
### _STATUS_SERVICE_CAN_ENABLER

TO READ OUT THE LOAD CHECK AND SHORTED BUS DETECTION ENABLER BIT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SERVICE_CAN_ENBL_BIT_WERT | unsigned int | Wert des Schuetze-Schliessen Aktivierungsbits |
| SERVICE_CAN_ENBL_BIT_TEXT | string | Schuetze-Schliessen Aktivierungsbit - aktivieren oder deaktivieren |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (66 × 2)
- [LIEFERANTEN](#table-lieferanten) (115 × 2)
- [FARTTEXTE](#table-farttexte) (18 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (24 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [DIAGMODE](#table-diagmode) (11 × 3)
- [JOBRESULTEXTENDED](#table-jobresultextended) (1 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (2 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 3)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [FORTTEXTE](#table-forttexte) (2 × 3)
- [T_TRUE_OR_FALSE](#table-t-true-or-false) (2 × 2)
- [T_HV_ISOLATION_DIAGNOSTIC_STATUS_TABLE](#table-t-hv-isolation-diagnostic-status-table) (4 × 2)
- [T_STATUS_OF_ISOLATION_FAULT_DIAGNOSITIC_CONTROL](#table-t-status-of-isolation-fault-diagnositic-control) (3 × 2)
- [T_HYBRID_BATTERY_HV_ISOLATION_FAULT_DIAGNOSTIC_STATUS_TABLE](#table-t-hybrid-battery-hv-isolation-fault-diagnostic-status-table) (4 × 2)
- [T_CONTACTOR_ENABLE_CONTROL_STAUS](#table-t-contactor-enable-control-staus) (4 × 2)
- [T_EEPROM_RESET_COMMAND_STATUS](#table-t-eeprom-reset-command-status) (4 × 2)
- [T_RESET_AND_DONT_RESET](#table-t-reset-and-dont-reset) (2 × 2)
- [T_HYBRID_BATTERY_PACK_VOLTAGE_SOURCE_TABLE](#table-t-hybrid-battery-pack-voltage-source-table) (6 × 2)
- [T_HYBRID_BATTERY_BUS_VOLTAGE_SOURCE_TABLE](#table-t-hybrid-battery-bus-voltage-source-table) (4 × 2)
- [T_INVALIDVALID_1BIT](#table-t-invalidvalid-1bit) (2 × 2)
- [T_COOLING_DEVICE_CONTROLLED_STATUS](#table-t-cooling-device-controlled-status) (4 × 2)
- [T_EEPROM_RESET_ENABLE](#table-t-eeprom-reset-enable) (2 × 2)
- [T_COOLING_DEVICE_ENABLE](#table-t-cooling-device-enable) (2 × 2)
- [T_VALUE_VALID_OR_INVALID](#table-t-value-valid-or-invalid) (2 × 2)
- [T_PROPER_SHUTDOWN](#table-t-proper-shutdown) (2 × 2)
- [T_OFFON_1BIT](#table-t-offon-1bit) (2 × 2)
- [WELD_CONTACTORS](#table-weld-contactors) (2 × 2)
- [ACTIVE_DISCHARGE](#table-active-discharge) (2 × 2)
- [T_HVBP_CONTACTOR_STATES](#table-t-hvbp-contactor-states) (8 × 2)
- [T_HCP_CONTACTOR_CMND](#table-t-hcp-contactor-cmnd) (8 × 2)
- [T_CNTCTRSTAT_TYPE](#table-t-cntctrstat-type) (6 × 2)
- [T_B_CONTACTOR_COMMAND_TYPE](#table-t-b-contactor-command-type) (2 × 2)
- [SERVICE_DISCONNECT](#table-service-disconnect) (4 × 2)
- [T_OPEN_CLOSE_1BIT](#table-t-open-close-1bit) (2 × 2)
- [T_HYBRID_BATTERY_CONTACTOR_DEVICE_CONTROL_ENABLE_TABLE_1](#table-t-hybrid-battery-contactor-device-control-enable-table-1) (3 × 2)
- [T_SELECT_OR_DISREGARD](#table-t-select-or-disregard) (2 × 2)
- [T_CONTACTOR_TABLE](#table-t-contactor-table) (2 × 2)
- [T_HYBRID_BATTERY_CONTACTOR_DEVICE_CONTROL_ENABLE_SELECTION](#table-t-hybrid-battery-contactor-device-control-enable-selection) (4 × 2)
- [T_DISABLE_ENABLE_1BIT](#table-t-disable-enable-1bit) (2 × 2)
- [HYBRID_LIEF](#table-hybrid-lief) (6 × 2)
- [DATUM_MONAT](#table-datum-monat) (53 × 2)
- [PROGRAMMIERSTATUS](#table-programmierstatus) (19 × 2)
- [HVIL_STATUS](#table-hvil-status) (4 × 2)
- [FAULT_CHECK](#table-fault-check) (2 × 2)
- [FAULT_CHECK_TEST](#table-fault-check-test) (2 × 2)
- [OCD_TEST_RESULT](#table-ocd-test-result) (5 × 2)
- [ISOLATION_COMMAND](#table-isolation-command) (2 × 2)
- [ISOLATION_TEST_STATUS](#table-isolation-test-status) (4 × 2)
- [ROUTINE_RETURN_CODES](#table-routine-return-codes) (12 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 66 rows × 2 columns

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
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?80? | ERROR_SVK_INCORRECT_LEN |
| ?81? | ERROR_SVK_INCORRECT_FINGERPRINT |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 115 rows × 2 columns

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
| 0xFFFFFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

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

Dimensions: 24 rows × 3 columns

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
| 0xA0 | ENTD | Entertainment Daten |
| 0xA1 | NAVD | Navigation Daten |
| 0xA2 | FCFN | Freischaltcode Funktion |
| 0xC0 | SWUP | Software-Update Package |
| 0xC1 | SWIP | Index Software-Update Package |
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

Dimensions: 11 rows × 3 columns

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
| 0xXY | -- | unbekannter Diagnose-Mode |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 1 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xXY | ERROR_UNKNOWN |

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
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |
| F_HLZ_VIEW | - |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | nein |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 2 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0x000001 | ExampleErrorCode | 0 |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-t-true-or-false"></a>
### T_TRUE_OR_FALSE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | False |
| 1 | True |

<a id="table-t-hv-isolation-diagnostic-status-table"></a>
### T_HV_ISOLATION_DIAGNOSTIC_STATUS_TABLE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht gestartet |
| 1 | gestartet |
| 2 | Diagnose beendet |
| 3 | Diagnose beendet |

<a id="table-t-status-of-isolation-fault-diagnositic-control"></a>
### T_STATUS_OF_ISOLATION_FAULT_DIAGNOSITIC_CONTROL

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Hybrid Batterie Schuetz muss geschlossen sein |
| 1 | Fehler momentan vorhanden: alle kritischen Fehler |
| 2 | PEB verbunden |

<a id="table-t-hybrid-battery-hv-isolation-fault-diagnostic-status-table"></a>
### T_HYBRID_BATTERY_HV_ISOLATION_FAULT_DIAGNOSTIC_STATUS_TABLE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | noch nicht gestartet |
| 1 | gestartet |
| 2 | Diagnose fehlerfrei beendet |
| 3 | Diagnose beendet Fehler vorhanden |

<a id="table-t-contactor-enable-control-staus"></a>
### T_CONTACTOR_ENABLE_CONTROL_STAUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Normalbetrieb |
| 1 | HV Schuetz Zustand muss offen sein |
| 2 | HV Service Schalter muss gezogen sein |
| 3 | Ausgangs Timer ist abgelaufen bitte warten - Test beendet |

<a id="table-t-eeprom-reset-command-status"></a>
### T_EEPROM_RESET_COMMAND_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | geloescht |
| 1 | Kein Befehl gesendet  |
| 2 | Fahrzeug Geschwindigkeit ungleich null |
| 3 | HV Service Schalter nicht gezogen |

<a id="table-t-reset-and-dont-reset"></a>
### T_RESET_AND_DONT_RESET

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | kein Reset |
| 1 | Reset |

<a id="table-t-hybrid-battery-pack-voltage-source-table"></a>
### T_HYBRID_BATTERY_PACK_VOLTAGE_SOURCE_TABLE

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine |
| 1 | Erste gueltige Modul Spannung |
| 2 | Summe der Modul Spannungen |
| 3 | Batterie Pack Spannung Sensor |
| 4 | reserviert |
| 5 |  |

<a id="table-t-hybrid-battery-bus-voltage-source-table"></a>
### T_HYBRID_BATTERY_BUS_VOLTAGE_SOURCE_TABLE

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | keine |
| 1 | HL-CAN WERT von PEB |
| 2 | Batterie HV Bus Spannung Sensor |
| 3 | reserviert |

<a id="table-t-invalidvalid-1bit"></a>
### T_INVALIDVALID_1BIT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ungueltig |
| 1 | gueltig |

<a id="table-t-cooling-device-controlled-status"></a>
### T_COOLING_DEVICE_CONTROLLED_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Normalbetrieb |
| 1 | Hybrid batterie temperatur ausserhalb gueltigen Bereich  |
| 2 | Run/Crank Spannung zu niedrig |
| 3 | Fehler momentan vorhanden: alle kritischen Fehler |

<a id="table-t-eeprom-reset-enable"></a>
### T_EEPROM_RESET_ENABLE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kontrolle-deaktive |
| 1 | Kontrolle-aktiv  |

<a id="table-t-cooling-device-enable"></a>
### T_COOLING_DEVICE_ENABLE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Kontrolle-deaktive |
| 1 | Kontrolle-aktiv  |

<a id="table-t-value-valid-or-invalid"></a>
### T_VALUE_VALID_OR_INVALID

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Wert gueltig  |
| 1 | Wert ungueltig |

<a id="table-t-proper-shutdown"></a>
### T_PROPER_SHUTDOWN

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ECU fehlerhaft eingeschlafen |
| 1 | ECU korrekt eingeschlafen |

<a id="table-t-offon-1bit"></a>
### T_OFFON_1BIT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | off |
| 1 | on |

<a id="table-weld-contactors"></a>
### WELD_CONTACTORS

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nicht verschweist |
| 1 | verschweist |

<a id="table-active-discharge"></a>
### ACTIVE_DISCHARGE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | ERFOLGREICH ENTLADEN |
| 1 | nicht ERFOLGREICH ENTLADEN |

<a id="table-t-hvbp-contactor-states"></a>
### T_HVBP_CONTACTOR_STATES

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | offen |
| 1 | VORLADEN |
| 2 | GESCHLOSSEN |
| 3 | VORLADUNG fehlgeschlagen |
| 4 | VORLADUNG VERBOTEN |
| 5 | RESERVIERTER Zustand 1 |
| 6 | RESERVIERTER Zustand 2 |
| 7 | RESERVIERTER Zustand 3 |

<a id="table-t-hcp-contactor-cmnd"></a>
### T_HCP_CONTACTOR_CMND

Dimensions: 8 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | offen |
| 1 | GESCHLOSSEN |
| 2 | ungueltig |
| 3 | CHRASH OEFFNUNG |
| 4 | RESERVIERTER Zustand 2 |
| 5 | RESERVIERTER Zustand 3 |
| 6 | RESERVIERTER Zustand 4 |
| 7 | RESERVIERTER Zustand 5 |

<a id="table-t-cntctrstat-type"></a>
### T_CNTCTRSTAT_TYPE

Dimensions: 6 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | offen |
| 1 | VORLADEN |
| 2 | GESCHLOSSEN |
| 3 | VORLADUNG VERBOTEN |
| 4 | fehlgeschlagen |
| 7 | Signal nicht verfuegbar |

<a id="table-t-b-contactor-command-type"></a>
### T_B_CONTACTOR_COMMAND_TYPE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Qualified Contactor Command = offen |
| 1 | Qualified Contactor Command = geschlossen oder Oeffnung erwartet |

<a id="table-service-disconnect"></a>
### SERVICE_DISCONNECT

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | OFFEN |
| 1 | GESCHLOSSEN |
| 2 | GESCHLOSSEN & SICHERUNG Kaputt |
| 3 | NICHT VERFUEGBAR |

<a id="table-t-open-close-1bit"></a>
### T_OPEN_CLOSE_1BIT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | OFFEN |
| 1 | SCHLIESEN |

<a id="table-t-hybrid-battery-contactor-device-control-enable-table-1"></a>
### T_HYBRID_BATTERY_CONTACTOR_DEVICE_CONTROL_ENABLE_TABLE_1

Dimensions: 3 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 1 | Positive SCHUETZ Kontrolle aktiv |
| 2 | Vorlade Schuetz Kontrolle aktiv |
| 3 | Negative Schuetz Kontrolle aktiv |

<a id="table-t-select-or-disregard"></a>
### T_SELECT_OR_DISREGARD

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | abwaehlen |
| 1 | auswaehlen |

<a id="table-t-contactor-table"></a>
### T_CONTACTOR_TABLE

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Offen |
| 1 | schliesen |

<a id="table-t-hybrid-battery-contactor-device-control-enable-selection"></a>
### T_HYBRID_BATTERY_CONTACTOR_DEVICE_CONTROL_ENABLE_SELECTION

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | nichts ausgewaehlt |
| 1 | Positive SCHUETZ Kontrolle aktiv |
| 2 | Vorlade Schuetz Kontrolle aktiv |
| 3 | Negative Schuetz Kontrolle aktiv |

<a id="table-t-disable-enable-1bit"></a>
### T_DISABLE_ENABLE_1BIT

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | Deaktivieren |
| 1 | Aktivieren |

<a id="table-hybrid-lief"></a>
### HYBRID_LIEF

Dimensions: 6 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0003 | Bosch |
| 0040 | Delphi |
| 007E | Hitachi |
| 009C | Cobasys |
| 0008 | Siemens |
| FFFF | undefinierter Lieferant |

<a id="table-datum-monat"></a>
### DATUM_MONAT

Dimensions: 53 rows × 2 columns

| KW | MON |
| --- | --- |
| 0x01 | 0x01 |
| 0x02 | 0x01 |
| 0x03 | 0x01 |
| 0x04 | 0x01 |
| 0x05 | 0x01 |
| 0x06 | 0x02 |
| 0x07 | 0x02 |
| 0x08 | 0x02 |
| 0x09 | 0x02 |
| 0x0A | 0x03 |
| 0x0B | 0x03 |
| 0x0C | 0x03 |
| 0x0D | 0x03 |
| 0x0E | 0x04 |
| 0x0F | 0x04 |
| 0x10 | 0x04 |
| 0x11 | 0x04 |
| 0x12 | 0x04 |
| 0x13 | 0x05 |
| 0x14 | 0x05 |
| 0x15 | 0x05 |
| 0x16 | 0x05 |
| 0x17 | 0x06 |
| 0x18 | 0x06 |
| 0x19 | 0x06 |
| 0x1A | 0x06 |
| 0x1B | 0x07 |
| 0x1C | 0x07 |
| 0x1D | 0x07 |
| 0x1E | 0x07 |
| 0x1F | 0x07 |
| 0x20 | 0x08 |
| 0x21 | 0x08 |
| 0x22 | 0x08 |
| 0x23 | 0x08 |
| 0x24 | 0x09 |
| 0x25 | 0x09 |
| 0x26 | 0x09 |
| 0x27 | 0x09 |
| 0x28 | 0x0A |
| 0x29 | 0x0A |
| 0x2A | 0x0A |
| 0x2B | 0x0A |
| 0x2C | 0x0A |
| 0x2D | 0x0B |
| 0x2E | 0x0B |
| 0x2F | 0x0B |
| 0x30 | 0x0B |
| 0x31 | 0x0C |
| 0x32 | 0x0C |
| 0x33 | 0x0C |
| 0x34 | 0x0C |
| 0xFF | 0x00 |

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

<a id="table-hvil-status"></a>
### HVIL_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | NICHT BESTROMT |
| 1 | FEHLERFREI |
| 2 | fehlgeschlagen |
| 3 | ungueltig |

<a id="table-fault-check"></a>
### FAULT_CHECK

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | DEAKTIVIERT |
| 1 | AKTIVIERT |

<a id="table-fault-check-test"></a>
### FAULT_CHECK_TEST

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | DEAKTIVIERT |
| 1 | AKTIVIERT |

<a id="table-ocd-test-result"></a>
### OCD_TEST_RESULT

Dimensions: 5 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | noch nicht gestartet |
| 1 | Diagnose fehlerfrei beendet |
| 2 | Diagnose beendet Fehler vorhanden |
| 3 | ABGEBROCHEN |
| 4 | DEAKTIVIERT – KEIN ERGEBNIS VERFÜGBAR |

<a id="table-isolation-command"></a>
### ISOLATION_COMMAND

Dimensions: 2 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | STOP |
| 1 | START |

<a id="table-isolation-test-status"></a>
### ISOLATION_TEST_STATUS

Dimensions: 4 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | TEST nicht gestartet |
| 1 | TEST gestartet |
| 2 | TEST BEENDET & fehlgeschlagen |
| 3 | TEST BEENDET & bestanden |

<a id="table-routine-return-codes"></a>
### ROUTINE_RETURN_CODES

Dimensions: 12 rows × 2 columns

| WERT | TEXT |
| --- | --- |
| 0 | OK |
| 8 | DIAGNOSE TIMER ABGELAUFEN |
| 776 | BPCM FEHLER VORHANDEN IN PEB |
| 1029 | RUN/CRANK Spannung zu niedrig |
| 1291 | Service Schalter muss gezogen sein |
| 1292 | HV BATTERIE SCHUETZ ZUSTAND muss offen sein |
| 2572 | HYBRID BATTERIE Temperatur ausserhalb gueltigen Bereich |
| 2584 | PEB STECKER NICHT ENTFERNT BITTE MIT DIAGNOSEBOX ERSETZEN  |
| 2585 | VORHERIGE DIAGNOSE IST NOCH NICHT BEENDET |
| 2586 | BATTERIE KUEHLMITTEL PUMPE Fehler vorhanden - START NICHT MOEGLICH |
| 2587 | BATTERIE KUEHLMITTEL PUMPE Fehler vorhanden REDUZIERTE GESCHWINDIGKEIT - GESCHWINDIGKEIT KANN NICHT EINGESTELLT WERDEN |
| 2588 | START NICHT MOEGLICH - PUMPE 12V  Versorgungsspannung zu niedrig |
