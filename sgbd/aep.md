# aep.prg

- Jobs: [38](#jobs)
- Tables: [26](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | Advanced Electrical Powermanagement |
| ORIGIN | MBtech EI-413 Bernstein_Matthias |
| REVISION | 7.003 |
| AUTHOR | BMW EI-24 Guzik, ALTRAN EI-24 Krause, ALTRAN EI-33 Lerose, BMW  |
| COMMENT | N/A |
| PACKAGE | 1.47 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [INITIALISIERUNG](#job-initialisierung) - Initialisierung und Kommunikationsparameter
- [STATUS_IGRINFO_AEP](#job-status-igrinfo-aep) - 0x224016 STATUS_IGRINFO_AEP Infospeicher Intelligente Generator Regelung (IGR) auslesen
- [STATUS_LEMINFO_AEP](#job-status-leminfo-aep) - 0x224017 STATUS_LEMINFO_AEP Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen
- [STATUS_MSAINFO_AEP](#job-status-msainfo-aep) - 0x224018 _STATUS_MSAINFO_AEP Infospeicher Motor-Start/Stop Automatik (MSA) auslesen
- [STATUS_SYSTEMCHECK_AEP_INFO_1](#job-status-systemcheck-aep-info-1) - 0x224022 STATUS_SYSTEMCHECK_AEP_INFO_1 Intelligenter Batteriesensor Bitfeld Pminfo1 lesen
- [STATUS_SYSTEMCHECK_AEP_INFO_2](#job-status-systemcheck-aep-info-2) - 0x224023 STATUS_SYSTEMCHECK_AEP_INFO_2 Intelligenter Batteriesensor Bitfeld Pminfo2 lesen
- [STEUERN_PM_HISTOGRAM_RESET](#job-steuern-pm-histogram-reset) - $2E 5F F5 04 Loeschen von pminfo1 index 23-30
- [STATUS_DFDSPROFLE](#job-status-dfdsprofle) - Generatorauslastungsprofil auslesen DFDSPROFLE (0x22 4081)
- [STATUS_VERBREDINFO](#job-status-verbredinfo) - 0x22401D STATUS_VERBREDINFO Verbraucherreduzierungsspeicher auslesen
- [STATUS_BZETOMSA](#job-status-bzetomsa) - 0x224155 STATUS_BZETOMSA Analyse von MSA-Abschaltverhinderern durch BZE3 gegenüber AEPBZE SDG(A2l-NAME=bzetomsa)
- [STATUS_DFDSN](#job-status-dfdsn) - 0x224156 STATUS_DFDSN Diagnose der Generatorauslastung über FASTA
- [STATUS_MSAINFO2](#job-status-msainfo2) - Auslesen Infospeicher Batteriezustandserkennung 2 UDS*: 0x224092 ReadDataByIdentifier
- [STATUS_BZETOMSA2](#job-status-bzetomsa2) - 0x224093 STATUS_BZETOMSA2 Analyse von MSA-Abschaltverhinderern durch BZE3 gegenüber AEPBZE SDG(A2l-NAME=bzetomsa)
- [IDENT_IBS](#job-ident-ibs) - 0x224021 IDENT_IBS Identifikationsdaten fuer IBS-Sensor auslesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_AEPDFMONITOR](#job-status-aepdfmonitor) - 0x224015 STATUS_AEPDFMONITOR FASTA-Messwertblock 10 lesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_MESSWERTE_IBS](#job-status-messwerte-ibs) - 0x22402B STATUS_MESSWERTE_IBS Messwerte IBS auslesen
- [START_SYSTEMCHECK_IGR_AUS](#job-start-systemcheck-igr-aus) - 0x3101F0F7 START_SYSTEMCHECK_IGR_AUS Ansteuerung Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STATUS_SYSTEMCHECK_IGR_AUS](#job-status-systemcheck-igr-aus) - 0x3103F0F7 STATUS_SYSTEMCHECK_IGR_AUS Auslesen Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STOP_SYSTEMCHECK_IGR_AUS](#job-stop-systemcheck-igr-aus) - 0x3102F0F7 STOP_SYSTEMCHECK_IGR_AUS Ende Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1
- [STEUERN_RUHESTROMMESSUNG](#job-steuern-ruhestrommessung) - Ansteuern Ruhestrompruefung mit IBS UDS  : $31 RoutineControl UDS  : $01 startRoutine UDS  : $F02B Ruhestrompruefung
- [STATUS_RUHESTROMMESSUNG](#job-status-ruhestrommessung) - Auslesen Ruhestromprüfung mit IBS UDS  : $31 RoutineControl UDS  : $03 requestRoutineResults UDS  : $F02B Ruhestrompruefung
- [STEUERN_IBS_STROMMESSUNG](#job-steuern-ibs-strommessung) - Ansteuern IBS Strommessung UDS: $31 RoutineControl
- [STATUS_IBS_STROMMESSUNG](#job-status-ibs-strommessung) - Auslesen IBS Strommessung UDS: $31 RoutineControl
- [STATUS_BZEDIAG](#job-status-bzediag) - 0x22403B STATUS_BZEDIAG BZE Infospeicher
- [STATUS_BZEDIAG2](#job-status-bzediag2) - Auslesen Infospeicher Batteriezustandserkennung 2 UDS*: $22 ReadDataByIdentifier
- [STATUS_VERBRAUCHERSTROM_EFII](#job-status-verbraucherstrom-efii) - Auslesen Verbraucherstrommessung EFII UDS  : $31   RoutineControl UDS  : $03   routineControlType UDS  : $7002 routineIdentifier
- [STEUERN_BATTERIETAUSCH_REGISTRIEREN](#job-steuern-batterietausch-registrieren) - UDS $31 01 F030 Batterietausch registrieren
- [STEUERN_ENDE_VERBRAUCHERSTROM_EFII](#job-steuern-ende-verbraucherstrom-efii) - Ansteuerung Verbraucherstrommessung EFII (IBS) beenden UDS  : $31   RoutineControl UDS  : $02   routineControlType UDS  : $7002 routineIdentifier
- [STEUERN_VERBRAUCHERSTROM_EFII](#job-steuern-verbraucherstrom-efii) - Ansteuerung Verbraucherstrommessung EFII (IBS) UDS  : $31   RoutineControl UDS  : $01   routineControlType UDS  : $7002 routineIdentifier
- [STATUS_AEP_I12_ZYKLISCHES_NACHLADEN_INFO](#job-status-aep-i12-zyklisches-nachladen-info) - Auslesen von wichtigen Kenngrößen der letzten 4 Vorgänge des zykllischen Nachladens plus dem letzten Parkvorgang AEP_I12_ZYKLISCHES_NACHLADEN_INFO (0x22 409D)
- [STATUS_AEP_I12_ZYKLISCHES_NACHLADEN_HISTOGRAMM](#job-status-aep-i12-zyklisches-nachladen-histogramm) - Auslesen der Histogramme über die Standzeit bis zum Beginn des zyklischen Nachladens und der Ladedauern der zyklischen Nachladevorgänge AEP_I12_ZYKLISCHES_NACHLADEN_HISTOGRAMM (0x22 409E)
- [_STEUERN_AEP_I12_TEST_LADEENDEGRUND](#job-steuern-aep-i12-test-ladeendegrund) - Job zum Test für AEP Funktionen AEP_I12_GRUND_LADEENDE (0x2E 5FA0)
- [_START_AEP_I12_ZYKNL_INFOSPEICHER_LOESCHEN](#job-start-aep-i12-zyknl-infospeicher-loeschen) - Löschen des Historienspeichers für die letzen 4 Ladevorgänge der 12V-Batterie aus der Hochvolt-Batterie AEP_I12_ZYKNL_INFOSPEICHER_LOESCHEN (0x31 01 AE02)
- [_START_AEP_I12_ZYKNL_HISTOGRAMM_LOESCHEN](#job-start-aep-i12-zyknl-histogramm-loeschen) - Löschen von Histogramm und Zähler aller Ladevorgänge der 12V-Batterie aus dem Hochvolt-System AEP_I12_ZYKNL_HISTOGRAMM_LOESCHEN (0x31 01 AE03)
- [_START_AEP_I12_TEST_BATTERYGUARD](#job-start-aep-i12-test-batteryguard) - Anforderung Aufruf BatteryGuard Call Setzen der Größe B_batteryguardcalldiag =1 Startvoraussetzungen: B_kl15 == TRUE. AEP_I12_TEST_BATTERYGUARD (0x31 01 F052)
- [_STATUS_AEP_I12_TEST_BATTERYGUARD](#job-status-aep-i12-test-batteryguard) - Anforderung Aufruf BatteryGuard Call auslesen Startvoraussetzungen: B_kl15 == TRUE. AEP_I12_TEST_BATTERYGUARD (0x31 03 F052)
- [_STOP_AEP_I12_TEST_BATTERYGUARD](#job-stop-aep-i12-test-batteryguard) - Anforderung Aufruf BatteryGuard Call beenden Setzen der Größe B_batteryguardcalldiag =0 Startvoraussetzungen: B_kl15 == TRUE. AEP_I12_TEST_BATTERYGUARD (0x31 02 F052)

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

<a id="job-status-igrinfo-aep"></a>
### STATUS_IGRINFO_AEP

0x224016 STATUS_IGRINFO_AEP Infospeicher Intelligente Generator Regelung (IGR) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_IGR_AEP0_BITS7 | unsigned long | Begrenzung 2 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS7_INFO | string | High Zyklisierungsgrenze erreicht/nicht erreicht (b_zykl_igrh) |
| STAT_IGR_AEP0_BITS6 | unsigned long | Begrenzung 1 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS6_INFO | string | Med Zyklisierungsgrenze erreicht/nicht erreicht (b_zykl_igrm) |
| STAT_IGR_AEP0_BITS5 | unsigned long | Regeneration 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS5_INFO | string | Regenerationsfunktion aktiv/nicht aktiv (B_battregen) |
| STAT_IGR_AEP0_BITS4 | unsigned long | IGR-Medium 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS4_INFO | string | IGR-Mediumphase angefordert/nicht angefordert (B_igrmed) |
| STAT_IGR_AEP0_BITS3 | unsigned long | IGR-High 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS3_INFO | string | IGR-Highphase angefordert/nicht angefordert (B_igrhigh) |
| STAT_IGR_AEP0_BITS2 | unsigned long | IGR-Low 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS2_INFO | string | IGR-Lowphase angefordert/nicht angefordert (B_igrlow) |
| STAT_IGR_AEP0_BITS1 | unsigned long | Diagnosejob gesetzt 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS1_INFO | string | IGR-Diagnose gesetzt/nicht gesetzt (B_diagigr) |
| STAT_IGR_AEP0_BITS0 | unsigned long | IGR codiert 1BIT IDENTICAL |
| STAT_IGR_AEP0_BITS0_INFO | string | IGR codiert/nicht codiert (B_cdigronw) |
| STAT_U_BN_SOLL_WERT | real | DREC_IGRINFO[2] 1BYTE in 0 bis 25,5Volt   Einheit: V   Min: 0 Max: 25.5 |
| STAT_U_BN_SOLL_EINH | string | V |
| STAT_IGR_AEP_PR1 | unsigned long | DREC_IGRINFO[3] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_AEP_PR2 | unsigned long | DREC_IGRINFO[4] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_AEP_QREKUP_WERT | real | DREC_IGRINFO[5] 1BYTE in 0 bis 25,5   Min: 0 Max: 25,5 |
| STAT_IGR_AEP_QREKUP_EINH | string | Ah |
| STAT_IGR_AEP_QLAD_WERT | real | Bilanz Low 2BYTE_in_0bis19088Ah   Einheit: Ah   Min: 0 Max: 19088.1 |
| STAT_IGR_AEP_QLAD_EINH | string | Ah |
| STAT_IGR_AEP_QLAD_M_WERT | long | Bilanz Medium IGRINFO_1BYTE_in_minus128bis127Ah   Einheit: Ah   Min: -128 Max: 127 |
| STAT_IGR_AEP_QLAD_M_EINH | string | Ah |
| STAT_IGR_AEP_QELAD_WERT | real | Bilanz High 2BYTE_in_0bis19088Ah   Einheit: Ah   Min: 0 Max: 19088.1 |
| STAT_IGR_AEP_QELAD_EINH | string | Ah |
| STAT_REG_AEP_ZR | unsigned long | Einfachzaehler 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_IGR_AEP_TCODE_WERT | unsigned long | Dauer iGR-Codiert 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_IGR_AEP_TCODE_EINH | string | Einfachzaehler 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_REG_AEP_SEIT_WERT | real | Zeit seit letzter R 1BYTE_in_0bis255h   Einheit: h   Min: 0 Max: 255 |
| STAT_REG_AEP_SEIT_EINH | string | h |
| STAT_REG_AEP_DAUER_WERT | real | Dauer letzte R 1BYTE_in_0bis255h   Einheit: h   Min: 0 Max: 255 |
| STAT_REG_AEP_DAUER_EINH | string | h |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hexfo-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-leminfo-aep"></a>
### STATUS_LEMINFO_AEP

0x224017 STATUS_LEMINFO_AEP Infospeicher Leistungskoordination Elektrisch Mechanisch (LEM) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ZR_USTAT_AEP_A_WERT | real | Haeufigkeitszaehler Zr_ustat_A 2BYTE in 0 bis 13107s   Einheit: s   Min: 0 Max: 13107 |
| STAT_ZR_USTAT_AEP_A_EINH | string | second |
| STAT_ZR_USTAT_AEP_A_INFO | string | Häufigkeit Spannungsbereich &gt;16 V |
| STAT_ZR_USTAT_AEP_B_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_B 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_B_EINH | string | second |
| STAT_ZR_USTAT_AEP_B_INFO | string | Häufigkeit Spannungsbereich zwischen K_LEMDIAGU1 und 16 V |
| STAT_ZR_USTAT_AEP_C_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_C 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_C_EINH | string | second |
| STAT_ZR_USTAT_AEP_C_INFO | string | Häufigkeit Spannungsbereich zwischen K_LEMDIAGU2 und  K_LEMDIAGU1 V |
| STAT_ZR_USTAT_AEP_D_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_D 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_D_EINH | string | second |
| STAT_ZR_USTAT_AEP_D_INFO | string | Häufigkeit Spannungsbereich zwischen K_LEMDIAGU3 und  K_LEMDIAGU2 V |
| STAT_ZR_USTAT_AEP_E_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_E 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_E_EINH | string | second |
| STAT_ZR_USTAT_AEP_E_INFO | string | Häufigkeit Spannungsbereich zwischen K_LEMDIAGU4 und  K_LEMDIAGU3 V |
| STAT_ZR_USTAT_AEP_F_WERT | unsigned long | Haeufigkeitszaehler Zr_ustat_F 2BYTE_in_0bis65534s   Einheit: s   Min: 0 Max: 65535 |
| STAT_ZR_USTAT_AEP_F_EINH | string | second |
| STAT_ZR_USTAT_AEP_F_INFO | string | Häufigkeit Spannungsbereich zwischen 9 und  K_LEMDIAGU4 V |
| STAT_ZR_USTAT_AEP_G_WERT | real | Haeufigkeitszaehler Zr_ustat_G 2BYTE in 0 bis 13107s   Einheit: s   Min: 0 Max: 13107 |
| STAT_ZR_USTAT_AEP_G_EINH | string | second |
| STAT_ZR_USTAT_AEP_G_INFO | string | Häufigkeit Spannungsbereich &lt;9 V |
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
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-msainfo-aep"></a>
### STATUS_MSAINFO_AEP

0x224018 _STATUS_MSAINFO_AEP Infospeicher Motor-Start/Stop Automatik (MSA) auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LADUNGSMENGE_GESAMT_WERT | real | Kumulierte, verbrauchte Ladungsmenge 2BYTE_in 0 bis 19087Ah   Einheit: Ah   Min: 0 Max: 190872 |
| STAT_LADUNGSMENGE_GESAMT_EINH | string | Ah |
| STAT_ANZAHL_MOTORSTART_GESAMT | real | Gesamtzahl Starts 2BYTE in 0 bis 327675   Min: 0 Max: 327675 |
| STAT_ANZAHL_MSASTART_GESAMT | real | Anzahl MSA Starts 2BYTE in 0 bis 327675   Min: 0 Max: 327675 |
| STAT_ANZAHL_FZGSTOP_GESAMT | real | Anzahl Fahrzeugstops 2BYTE in 0 bis 327675   Min: 0 Max: 327675 |
| STAT_ZEIT_IN_MSA_GESAMT_WERT | real | Zeit in MSA 2BYTE in 0 bis 3276750s   Einheit: s   Min: 0 Max: 3276750 |
| STAT_ZEIT_IN_MSA_GESAMT_EINH | string | Sekunde |
| STAT_ZEIT_IN_FZGSTOP_GESAMT_WERT | real | Zeit in Fahrzeugstop 2BYTE in 0 bis 3276750s   Einheit: s   Min: 0 Max: 3276750 |
| STAT_ZEIT_IN_FZGSTOP_GESAMT_EINH | string | Sekunde |
| STAT_MSA_STOP_1_MIN_BZE_SPANNUNG_WERT | real | erste minimale Startspannungslage vom BZE3 gemessen bei MSA 1 Byte in 0 bis 255   Einheit: V   Min: 0 Max: 25,5 |
| STAT_MSA_STOP_1_MIN_BZE_SPANNUNG_EINH | string | Volt |
| STAT_MSA_STOP_3_MIN_BZE_SPANNUNG_WERT | real | zweite minimale Startspannungslage vom BZE3 gemessen bei MSA 1 Byte in 0 bis 255  Einheit: V  Min: 0 Max: 25,5 |
| STAT_MSA_STOP_3_MIN_BZE_SPANNUNG_EINH | string | Volt |
| STAT_BATTSPG_DSOC_INTERVALL1_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG1 und K_DSOCMSADG2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL1_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL2_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG2 und K_DSOCMSADG3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL2_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL3_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG3 und K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL3_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL4_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC groesser K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL4_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL1_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG1 und K_DSOCMSADG2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL1_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL2_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG2 und K_DSOCMSADG3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL2_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL3_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG3 und K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL3_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL4_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC groesser K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL4_UEBER_TGRENZ_EINH | string | V |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL1_WERT | unsigned long | Relative Haeufigkeit der MSA-Stops mit Dauer zwischen K_ZT0_MSASTP und K_ZT1_MSASTP 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.961 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL1_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL2_WERT | unsigned long | Relative Haeufigkeit der MSA-Stops mit Dauer zwischen K_ZT1_MSASTP und K_ZT2_MSASTP 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.961 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL2_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL3_WERT | unsigned long | Relative Haeufigkeit der MSA-Stops mit Dauer zwischen K_ZT2_MSASTP und K_ZT3_MSASTP 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.961 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL3_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL4_WERT | unsigned long | Relative Haeufigkeit der MSA-Stops mit Dauer groesser und K_ZT3_MSASTP 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 99.961 |
| STAT_REL_HAEUFIGKEIT_STOPS_DAUER_INTERVALL4_EINH | string | percent |
| STAT_MSA_STOP_1_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 1 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_1_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_1_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 1 2BYTE in 0 bis 65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_1_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_1_TEMP_WERT | real | Temp MSA-Stop 1 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_1_TEMP_EINH | string | degreeC |
| STAT_MSA_STOP_2_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_2_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_2_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 2 2BYTE in 0 bis 65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_2_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_2_TEMP_WERT | real | Temp MSA-Stop 2 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_2_TEMP_EINH | string | degreeC |
| STAT_MSA_STOP_3_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_3_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_3_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 3 2BYTE in 0 bis 65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_3_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_3_TEMP_WERT | real | Temp MSA-Stop 3 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_3_TEMP_EINH | string | degreeC |
| STAT_MSA_EA_SOC_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer SOC 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_BATTERIESPANNUNG_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer BATTERIESPANNUNG 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE2_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE2 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE3_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE3 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE4_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE4 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE5_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE5 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE6_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE6 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE7_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE7 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_SOC_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer SOC 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_STRTSPG_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Startspannung 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_DIAGNOSE_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Generator-Diagnose 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_TBATT_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Batterietemperatur 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_TRAMODE_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Tra-Mode 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_ZYKL_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Zyklisierung 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_BNSTROM_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer zu hoher Bordnetzstrom 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_RESERVE2_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer RESERVE2 1BIT   1: aktiv    0: nicht aktiv |
| STAT_REL_HAEUFIGKEIT_AV_SOC_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV SOC 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_SOC_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_STRTSPG_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV Startspannung 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_STRTSPG_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_DIAGNOSE_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV Diagnose 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_DIAGNOSE_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_TBATT_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV TBatt 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_TBATT_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_ZYKL_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV Zyklisierung 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_ZYKL_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_TRAMODE_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV Transportmode 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_TRAMODE_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_BNSTROM_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV Bordnetzstrom 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_BNSTROM_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_AV_RESERVE2_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund AV RESERVE2 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_AV_RESERVE2_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_EA_SOC_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund EA SOC 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_EA_SOC_EINH | string | percent |
| STAT_REL_HAEUFIGKEIT_EA_BATTERIESPANNUNG_WERT | real | Relative Haeufigkeit Fahrzeugstop aufgrund EA BATTERIESPANNUNG 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 100 |
| STAT_REL_HAEUFIGKEIT_EA_BATTERIESPANNUNG_EINH | string | percent |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-aep-info-1"></a>
### STATUS_SYSTEMCHECK_AEP_INFO_1

0x224022 STATUS_SYSTEMCHECK_AEP_INFO_1 Intelligenter Batteriesensor Bitfeld Pminfo1 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIELADUNG_GESAMT_WERT | unsigned long | AEPINFO1_[0] 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIELADUNG_GESAMT_EINH | string | Ah |
| STAT_BATTERIELADUNG_BILANZ_WERT | unsigned long | Differenz LADUNG - ENTLADUNG in Ah 0 - 65535 |
| STAT_BATTERIELADUNG_BILANZ_EINH | string | Ah |
| STAT_BATTERIELADUNG_SALDO_WERT | long | Differenz LADUNG - ENTLADUNG in Ah |
| STAT_BATTERIELADUNG_SALDO_EINH | string | Ah |
| STAT_BATTERIELADUNG_SALDO_INFO | string | positives Ergebnis = Aufladung, negatives Ergebnis = Entladung |
| STAT_BATTERIEENTLADUNG_GESAMT_WERT | unsigned long | AEPINFO1_[1] 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIEENTLADUNG_GESAMT_EINH | string | Ah |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_WERT | unsigned long | AEPINFO1_[2] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH__0_A_INFO | string | 0% &lt; Soc_rel = 40% |
| STAT_ZEIT_IM_LADUNGSBEREICH_A_B_WERT | unsigned long | AEPINFO1_[3] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_A_B_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH__A_B_INFO | string | 40% &lt; Soc_rel = 55% |
| STAT_ZEIT_IM_LADUNGSBEREICH_B_C_WERT | unsigned long | AEPINFO1_[4] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_B_C_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH__B_C_INFO | string | 55% &lt; Soc_rel = 70% |
| STAT_ZEIT_IM_LADUNGSBEREICH_C_D_WERT | unsigned long | AEPINFO1_[5] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_C_D_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH__C_D_INFO | string | 70% &lt; Soc_rel = 85% |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_WERT | unsigned long | AEPINFO1_[6] 2BYTE_in_0bis65534h   Einheit: h   Min: 0 Max: 65535 |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_EINH | string | h |
| STAT_ZEIT_IM_LADUNGSBEREICH_GROESSER_D_INFO | string | 85% &lt; Soc_rel |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_WERT | unsigned long | AEPINFO1_[7] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_BIS_A_INFO | string | T_batt = 0°C |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_WERT | unsigned long | AEPINFO1_[8] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_A_B_INFO | string | 0°C &lt; T_batt = 10°C |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_WERT | unsigned long | AEPINFO1_[9] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_B_C_INFO | string | 10°C &lt; T_batt = 30°C |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_WERT | unsigned long | AEPINFO1_[10] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_C_D_INFO | string | 30°C &lt; T_batt = 60°C |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_WERT | unsigned long | AEPINFO1_[11] 2BYTE_in_0bis327670min   Einheit: min   Min: 0 Max: 327670 |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_EINH | string | Minute |
| STAT_ZEIT_IM_TEMPERATURBEREICH_GROESSER_D_INFO | string | 60°C &lt; T_batt |
| STAT_KM_STAND_AKTUELL_WERT | unsigned long | AEPINFO1_[12] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_AKTUELL_EINH | string | kilometer |
| STAT_KM_STAND_VOR_1_TAG_WERT | unsigned long | AEPINFO1_[13] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_1_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_2_TAG_WERT | unsigned long | AEPINFO1_[14] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_2_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_3_TAG_WERT | unsigned long | AEPINFO1_[15] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_3_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_4_TAG_WERT | unsigned long | AEPINFO1_[16] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_4_TAG_EINH | string | kilometer |
| STAT_KM_STAND_VOR_5_TAG_WERT | unsigned long | AEPINFO1_[17] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_KM_STAND_VOR_5_TAG_EINH | string | kilometer |
| STAT_BATTERIETAUSCH_LETZTER_WERT | unsigned long | AEPINFO1_[18] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_BATTERIETAUSCH_LETZTER_EINH | string | kilometer |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_WERT | unsigned long | AEPINFO1_[19] 2BYTE in 0 bis 655340km   Einheit: km   Min: 0 Max: 655340 |
| STAT_BATTERIETAUSCH_ZWEITLETZTER_EINH | string | kilometer |
| STAT_ANZAHL_LEERLAUFDREHZAHLANHEBUNG_EPS | unsigned long | AEPINFO1_[20] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_ANZAHL_LEERLAUFDREHZAHLANHEBUNG_IBS | unsigned long | AEPINFO1_[20] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_BATTERIEENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_WERT | unsigned long | AEPINFO1_[22] 2BYTE_in_0bis65534h   Einheit: Ah   Min: 0 Max: 65535 |
| STAT_BATTERIEENTLADUNG_GESAMT_BEI_MOTOR_LAEUFT_EINH | string | Ah |
| STAT_RUHESTROM_VOR_3_ZYKLEN_TEXT | string | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_3_ZYKLEN_WERT | int | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_3_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_2_ZYKLEN_TEXT | string | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_2_ZYKLEN_WERT | int | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_2_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_1_ZYKLUS_TEXT | string | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_1_ZYKLUS_WERT | int | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_1_ZYKLUS_EINH | string | - |
| STAT_RUHESTROM_AKTUELL_TEXT | string | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_AKTUELL_WERT | int | AEPINFO1_[23] 4BIT_RUHESTROM |
| STAT_RUHESTROM_AKTUELL_EINH | string | - |
| STAT_RUHESTROM_VOR_7_ZYKLEN_TEXT | string | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_7_ZYKLEN_WERT | int | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_7_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_6_ZYKLEN_TEXT | string | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_6_ZYKLEN_WERT | int | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_6_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_5_ZYKLEN_TEXT | string | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_5_ZYKLEN_WERT | int | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_5_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_4_ZYKLEN_TEXT | string | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_4_ZYKLEN_WERT | int | AEPINFO1_[24] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_4_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_11_ZYKLEN_TEXT | string | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_11_ZYKLEN_WERT | int | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_11_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_10_ZYKLEN_TEXT | string | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_10_ZYKLEN_WERT | int | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_10_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_9_ZYKLEN_TEXT | string | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_9_ZYKLEN_WERT | int | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_9_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_8_ZYKLEN_TEXT | string | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_8_ZYKLEN_WERT | int | AEPINFO1_[25] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_8_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_15_ZYKLEN_TEXT | string | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_15_ZYKLEN_WERT | int | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_15_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_14_ZYKLEN_TEXT | string | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_14_ZYKLEN_WERT | int | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_14_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_13_ZYKLEN_TEXT | string | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_13_ZYKLEN_WERT | int | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_13_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_12_ZYKLEN_TEXT | string | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_12_ZYKLEN_WERT | int | AEPINFO1_[26] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_12_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_19_ZYKLEN_TEXT | string | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_19_ZYKLEN_WERT | int | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_19_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_18_ZYKLEN_TEXT | string | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_18_ZYKLEN_WERT | int | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_18_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_17_ZYKLEN_TEXT | string | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_17_ZYKLEN_WERT | int | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_17_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_16_ZYKLEN_TEXT | string | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_16_ZYKLEN_WERT | int | AEPINFO1_[27] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_16_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_23_ZYKLEN_TEXT | string | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_23_ZYKLEN_WERT | int | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_23_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_22_ZYKLEN_TEXT | string | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_22_ZYKLEN_WERT | int | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_22_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_21_ZYKLEN_TEXT | string | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_21_ZYKLEN_WERT | int | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_21_ZYKLEN_EINH | string | - |
| STAT_RUHESTROM_VOR_20_ZYKLEN_TEXT | string | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_20_ZYKLEN_WERT | int | AEPINFO1_[28] 4BIT_RUHESTROM |
| STAT_RUHESTROM_VOR_20_ZYKLEN_EINH | string | - |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_AUS_WERT | real | AEPINFO1_[29] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_EIN_WERT | real | AEPINFO1_[29] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_AKTUELLER_WERT_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_1_TAG_WERT_MOTOR_AUS_WERT | real | AEPINFO1_[30] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_1_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_1_TAG_MOTOR_EIN_WERT | real | AEPINFO1_[30] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_1_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_2_TAG_WERT_MOTOR_AUS_WERT | real | AEPINFO1_[31] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_2_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_2_TAG_MOTOR_EIN_WERT | real | AEPINFO1_[31] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_2_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_3_TAG_WERT_MOTOR_AUS_WERT | real | AEPINFO1_[32] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_3_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_3_TAG_MOTOR_EIN_WERT | real | AEPINFO1_[32] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_3_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_4_TAG_WERT_MOTOR_AUS_WERT | real | AEPINFO1_[33] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_4_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_4_TAG_MOTOR_EIN_WERT | real | AEPINFO1_[33] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_4_TAG_MOTOR_EIN_EINH | string | Ah |
| STAT_VOR_5_TAG_WERT_MOTOR_AUS_WERT | real | AEPINFO1_[34] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_VOR_5_TAG_WERT_MOTOR_AUS_EINH | string | Ah |
| STAT_STROMBILANZ_VOR_5_TAG_MOTOR_EIN_WERT | real | AEPINFO1_[34] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_STROMBILANZ_VOR_5_TAG_MOTOR_EIN_EINH | string | Ah |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-aep-info-2"></a>
### STATUS_SYSTEMCHECK_AEP_INFO_2

0x224023 STATUS_SYSTEMCHECK_AEP_INFO_2 Intelligenter Batteriesensor Bitfeld Pminfo2 lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIE_KAPAZITAET_WERT | unsigned long | AEPINFO2_[0] 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIE_KAPAZITAET_EINH | string | Ah |
| STAT_SOH_WERT | real | AEPINFO2_[1] 1BYTE_in_minus128bis127prozent   Einheit: % |
| STAT_SOH_EINH | string | percent |
| STAT_SOC_FIT_WERT | unsigned long | AEPINFO2_[2] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_SOC_FIT_EINH | string | percent |
| STAT_TEMP_SAISON_WERT | long | AEPINFO2_[3] 1BYTE_in_minus128bis127gradCelsius   Einheit: C |
| STAT_TEMP_SAISON_EINH | string | degreeC |
| STAT_ANZAHL_RUHESPANNUNGSAUSWERTUNGEN_OCV | unsigned long | AEPINFO2_[4] 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_Q_SOC_AKTUELL_WERT | unsigned long | AEPINFO2_[5] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_AKTUELL_EINH | string | Ah |
| STAT_Q_SOC_VOR_1_TAG_WERT | unsigned long | AEPINFO2_[6] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_1_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_2_TAG_WERT | unsigned long | AEPINFO2_[7] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_2_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_3_TAG_WERT | unsigned long | AEPINFO2_[8] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_3_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_4_TAG_WERT | unsigned long | AEPINFO2_[9] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_4_TAG_EINH | string | Ah |
| STAT_Q_SOC_VOR_5_TAG_WERT | unsigned long | AEPINFO2_[10] 1BYTE_in_0bis1275Ah   Einheit: Ah |
| STAT_Q_SOC_VOR_5_TAG_EINH | string | Ah |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_WERT | unsigned long | AEPINFO2_[11] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_AKTUELL_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_WERT | unsigned long | AEPINFO2_[12] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_1_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_WERT | unsigned long | AEPINFO2_[13] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_2_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_WERT | unsigned long | AEPINFO2_[14] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_3_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_WERT | unsigned long | AEPINFO2_[15] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_4_TAG_EINH | string | percent |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_WERT | unsigned long | AEPINFO2_[16] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_STARTFAEHIGKEITSGRENZE_VOR_5_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_AKTUELL_WERT | unsigned long | AEPINFO2_[17] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_AKTUELL_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_WERT | unsigned long | AEPINFO2_[18] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_1_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_WERT | unsigned long | AEPINFO2_[19] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_2_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_WERT | unsigned long | AEPINFO2_[20] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_3_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_WERT | unsigned long | AEPINFO2_[21] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_4_TAG_EINH | string | percent |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_WERT | unsigned long | AEPINFO2_[22] 1BYTE_in_0bis255prozent   Einheit: % |
| STAT_LADUNGSZUSTAND_VOR_5_TAG_EINH | string | percent |
| STAT_BZE_DIAG_0 | unsigned long | AEPINFO2_[23] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_1 | unsigned long | AEPINFO2_[24] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_2 | unsigned long | AEPINFO2_[25] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_3 | unsigned long | AEPINFO2_[26] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| STAT_BZE_DIAG_4 | unsigned long | AEPINFO2_[27] 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-pm-histogram-reset"></a>
### STEUERN_PM_HISTOGRAM_RESET

$2E 5F F5 04 Loeschen von pminfo1 index 23-30

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG (MEN48) |
| _RESPONSE | binary | Hex-Auftrag an SG (MEN48) |

<a id="job-status-dfdsprofle"></a>
### STATUS_DFDSPROFLE

Generatorauslastungsprofil auslesen DFDSPROFLE (0x22 4081)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DFDSPROFLE_0 | unsigned char | Generatorauslastungsprofil 0 a2l-Name: dfdsprofle [0] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_1 | unsigned char | Generatorauslastungsprofil 1 a2l-Name: dfdsprofle [1] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_2 | unsigned char | Generatorauslastungsprofil 2 a2l-Name: dfdsprofle [2] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_3 | unsigned char | Generatorauslastungsprofil 3 a2l-Name: dfdsprofle [3] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_4 | unsigned char | Generatorauslastungsprofil 4 a2l-Name: dfdsprofle [4] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_5 | unsigned char | Generatorauslastungsprofil 5 a2l-Name: dfdsprofle [5] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_6 | unsigned char | Generatorauslastungsprofil 6 a2l-Name: dfdsprofle [6] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_7 | unsigned char | Generatorauslastungsprofil 7 a2l-Name: dfdsprofle [7] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_8 | unsigned char | Generatorauslastungsprofil 8 a2l-Name: dfdsprofle [8] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_9 | unsigned char | Generatorauslastungsprofil 9 a2l-Name: dfdsprofle [9] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_10 | unsigned char | Generatorauslastungsprofil 10 a2l-Name: dfdsprofle [10] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_11 | unsigned char | Generatorauslastungsprofil 11 a2l-Name: dfdsprofle [11] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_12 | unsigned char | Generatorauslastungsprofil 12 a2l-Name: dfdsprofle [12] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_13 | unsigned char | Generatorauslastungsprofil 13 a2l-Name: dfdsprofle [13] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_14 | unsigned char | Generatorauslastungsprofil 14 a2l-Name: dfdsprofle [14] Min: 0.0 Max: 255.0 |
| STAT_DFDSPROFLE_15 | unsigned char | Generatorauslastungsprofil 15 a2l-Name: dfdsprofle [15] Min: 0.0 Max: 255.0 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei "ERROR", wenn nicht fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-verbredinfo"></a>
### STATUS_VERBREDINFO

0x22401D STATUS_VERBREDINFO Verbraucherreduzierungsspeicher auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_E1_TAG | unsigned long | Ereignis 1 Tag (Verbredinfo[0]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_TAG_EINH | string | Tag |
| STAT_E1_MONAT | unsigned long | Ereignis 1 Monat (Verbredinfo[1]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_MONAT_EINH | string | Monat |
| STAT_E1_DAUER_WERT | unsigned long | Ereignis 1 Dauer der Verbraucherreduzierung (Verbredinfo[2]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E1_DAUER_EINH | string | Minute |
| STAT_E1_LRSA | unsigned long | Ereignis 1 Leistungsreduktionstufe A (Verbredinfo[3]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_LRSA_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse A |
| STAT_E1_LRSB | unsigned long | Ereignis 1 Leistungsreduktionstufe B (Verbredinfo[4]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E1_LRSB_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse B |
| STAT_E1_WCFA_B0 | unsigned long | Generatordrehzahl in Ordnung |
| STAT_E1_WCFA_B0_TEXT | string | Generatordrehzahl in Ordnung |
| STAT_E1_WCFA_B1 | unsigned long | Bordnetzstrom in Ordnung |
| STAT_E1_WCFA_B1_TEXT | string | Bordnetzstrom in Ordnung |
| STAT_E1_WCFA_B2 | unsigned long | Fahrzeit in Ordnung |
| STAT_E1_WCFA_B2_TEXT | string | Fahrzeit in Ordnung |
| STAT_E1_WCFA_B345 | unsigned long | Fahrzeit in Ordnung |
| STAT_E1_WCFA_B345_TEXT | string | Fahrzeit in Ordnung |
| STAT_E1_WCFB_B012 | unsigned long | Mittl. Stromverbrauch |
| STAT_E1_WCFB_B012_TEXT | string | Mittl. Stromverbrauch |
| STAT_E1_WCFB_B345 | unsigned long | Mittl. Fahrzeit |
| STAT_E1_WCFB_B345_TEXT | string | Mittl. Fahrzeit |
| STAT_E2_TAG | unsigned long | Ereignis 2 Tag (Verbredinfo[7]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_TAG_EINH | string | Tag |
| STAT_E2_MONAT | unsigned long | Ereignis 2 Monat (Verbredinfo[8]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_MONAT_EINH | string | Monat |
| STAT_E2_DAUER_WERT | unsigned long | Ereignis 2 Dauer der Verbraucherreduzierung (Verbredinfo[9]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E2_DAUER_EINH | string | Minute |
| STAT_E2_LRSA | unsigned long | Ereignis 2 Leistungsreduktionstufe A (Verbredinfo[10]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_LRSA_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse A |
| STAT_E2_LRSB | unsigned long | Ereignis 2 Leistungsreduktionstufe B (Verbredinfo[11]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E2_LRSB_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse B |
| STAT_E2_WCFA_B0 | unsigned long | Generatordrehzahl in Ordnung |
| STAT_E2_WCFA_B0_TEXT | string | Generatordrehzahl in Ordnung |
| STAT_E2_WCFA_B1 | unsigned long | Bordnetzstrom in Ordnung |
| STAT_E2_WCFA_B1_TEXT | string | Bordnetzstrom in Ordnung |
| STAT_E2_WCFA_B2 | unsigned long | Fahrzeit in Ordnung |
| STAT_E2_WCFA_B2_TEXT | string | Fahrzeit in Ordnung |
| STAT_E2_WCFA_B345 | unsigned long | Mittl. Generatordrehzahl |
| STAT_E2_WCFA_B345_TEXT | string | Mittl. Generatordrehzahl |
| STAT_E2_WCFB_B012 | unsigned long | Mittl. Stromverbrauch |
| STAT_E2_WCFB_B012_TEXT | string | Mittl. Stromverbrauch |
| STAT_E2_WCFB_B345 | unsigned long | Mittl. Fahrzeit |
| STAT_E2_WCFB_B345_TEXT | string | Mittl. Fahrzeit |
| STAT_E3_TAG | unsigned long | Ereignis 3 Tag (Verbredinfo[14]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_TAG_EINH | string | Tag |
| STAT_E3_MONAT | unsigned long | Ereignis 3 Monat (Verbredinfo[15]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_MONAT_EINH | string | Monat |
| STAT_E3_DAUER_WERT | unsigned long | Ereignis 3 Dauer der Verbraucherreduzierung (Verbredinfo[16]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E3_DAUER_EINH | string | Minute |
| STAT_E3_LRSA | unsigned long | Ereignis 3 Leistungsreduktionstufe A (Verbredinfo[17]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_LRSA_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse A |
| STAT_E3_LRSB | unsigned long | Ereignis 3 Leistungsreduktionstufe B (Verbredinfo[18]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E3_LRSB_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse B |
| STAT_E3_WCFA_B0 | unsigned long | Generatordrehzahl in Ordnung |
| STAT_E3_WCFA_B0_TEXT | string | Generatordrehzahl in Ordnung |
| STAT_E3_WCFA_B1 | unsigned long | Bordnetzstrom in Ordnung |
| STAT_E3_WCFA_B1_TEXT | string | Bordnetzstrom in Ordnung |
| STAT_E3_WCFA_B2 | unsigned long | Fahrzeit in Ordnung |
| STAT_E3_WCFA_B2_TEXT | string | Fahrzeit in Ordnung |
| STAT_E3_WCFA_B345 | unsigned long | Mittl. Generatordrehzahl |
| STAT_E3_WCFA_B345_TEXT | string | Mittl. Generatordrehzahl |
| STAT_E3_WCFB_B012 | unsigned long | Mittl. Stromverbrauch |
| STAT_E3_WCFB_B012_TEXT | string | Mittl. Stromverbrauch |
| STAT_E3_WCFB_B345 | unsigned long | Mittl. Fahrzeit |
| STAT_E3_WCFB_B345_TEXT | string | Mittl. Fahrzeit |
| STAT_E4_TAG | unsigned long | Ereignis 4 Tag (Verbredinfo[21]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_TAG_EINH | string | Tag |
| STAT_E4_MONAT | unsigned long | Ereignis 4 Monat (Verbredinfo[22]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_MONAT_EINH | string | Monat |
| STAT_E4_DAUER_WERT | unsigned long | Ereignis 4 Dauer der Verbraucherreduzierung (Verbredinfo[23]) 1BYTE_in_0bis255min   Einheit: min   Min: 0 Max: 255 |
| STAT_E4_DAUER_EINH | string | Minute |
| STAT_E4_LRSA | unsigned long | Ereignis 4 Leistungsreduktionstufe A (Verbredinfo[24]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_LRSA_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse A |
| STAT_E4_LRSB | unsigned long | Ereignis 4 Leistungsreduktionstufe B (Verbredinfo[25]) 1BYTE in 0 bis 255   Min: 0 Max: 255 |
| STAT_E4_LRSB_TEXT | string | Maximale Reduzierungsstufe für Verbraucher der Klasse B |
| STAT_E4_WCFA_B0 | unsigned long | Generatordrehzahl in Ordnung |
| STAT_E4_WCFA_B0_TEXT | string | Generatordrehzahl in Ordnung |
| STAT_E4_WCFA_B1 | unsigned long | Bordnetzstrom in Ordnung |
| STAT_E4_WCFA_B1_TEXT | string | Bordnetzstrom in Ordnung |
| STAT_E4_WCFA_B2 | unsigned long | Fahrzeit in Ordnung |
| STAT_E4_WCFA_B2_TEXT | string | Fahrzeit in Ordnung |
| STAT_E4_WCFA_B345 | unsigned long | Mittl. Generatordrehzahl |
| STAT_E4_WCFA_B345_TEXT | string | Mittl. Generatordrehzahl |
| STAT_E4_WCFB_B012 | unsigned long | Mittl. Stromverbrauch |
| STAT_E4_WCFB_B012_TEXT | string | Mittl. Stromverbrauch |
| STAT_E4_WCFB_B345 | unsigned long | Mittl. Fahrzeit |
| STAT_E4_WCFB_B345_TEXT | string | Mittl. Fahrzeit |
| STAT_ANZAHL_SCHLECHTE_LABI_GESAMT | unsigned long | Anzahl erkannter schlechter Ladebilanzen (Verbredinfo[28]) 1BYTE IDENTICAL HEX   Min: 0 Max: 255 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bzetomsa"></a>
### STATUS_BZETOMSA

0x224155 STATUS_BZETOMSA Analyse von MSA-Abschaltverhinderern durch BZE3 gegenüber AEPBZE SDG(A2l-NAME=bzetomsa)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INFOSPEICHER_BZE3_MSA_0_2 | unsigned long | BZE3 AV=0, AEP-BZE AV=0 |
| STAT_INFOSPEICHER_BZE3_MSA_0_2_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_3_5 | unsigned long | BZE3 AV=0, AEP-BZE AV=1 |
| STAT_INFOSPEICHER_BZE3_MSA_3_5_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_6_8 | unsigned long | BZE3 AV=1, AEP-BZE AV=0 |
| STAT_INFOSPEICHER_BZE3_MSA_6_8_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_9_11 | unsigned long | BZE3 AV=1, AEP-BZE AV=1 |
| STAT_INFOSPEICHER_BZE3_MSA_9_11_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_12 | unsigned long | Zähler |
| STAT_INFOSPEICHER_BZE3_MSA_12_EINH | string | dimensionslos |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-dfdsn"></a>
### STATUS_DFDSN

0x224156 STATUS_DFDSN Diagnose der Generatorauslastung über FASTA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BEREICH_0_HOHEGENAUSLAST_STROMUNABH_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_0_HOHEGENAUSLAST_STROMUNABH_EINH | string | Prozent |
| STAT_BEREICH_1_ERHOEHTEGENAUSLAST_STROMUNABH_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_1_ERHOEHTEGENAUSLAST_STROMUNABH_EINH | string | Prozent |
| STAT_BEREICH_2_MITTLEREGENAUSLAST_STROMUNABH_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_2_MITTLEREGENAUSLAST_STROMUNABH_EINH | string | Prozent |
| STAT_BEREICH_3_NIEDRIGEGENAUSLAST_STROMUNABH_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_3_NIEDRIGEGENAUSLAST_STROMUNABH_EINH | string | Prozent |
| STAT_BEREICH_4_HOHEGENAUSLAST_HOHERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_4_HOHEGENAUSLAST_HOHERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_5_ERHOEHTEGENAUSLAST_HOHERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_5_ERHOEHTEGENAUSLAST_HOHERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_6_MITTLEREGENAUSLAST_HOHERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_6_MITTLEREGENAUSLAST_HOHERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_7_NIEDRIGEGENAUSLAST_HOHERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_7_NIEDRIGEGENAUSLAST_HOHERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_8_HOHEGENAUSLAST_GERINGERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_8_HOHEGENAUSLAST_GERINGERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_9_ERHOEHTEGENAUSLAST_GERINGERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_9_ERHOEHTEGENAUSLAST_GERINGERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_10_MITTLEREGENAUSLAST_GERINGERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_10_MITTLEREGENAUSLAST_GERINGERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_11_NIEDRIGEGENAUSLAST_GERINGERLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_11_NIEDRIGEGENAUSLAST_GERINGERLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_12_HOHEGENAUSLAST_KEINLADESTROM_WERT | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_12_HOHEGENAUSLAST_KEINLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_13_ERHOEHTEGENAUSLAST_KEINLADESTROM_WERT | real | gewichteter Mittelwert 6BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_13_ERHOEHTEGENAUSLAST_KEINLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_14_MITTLEREGENAUSLAST_KEINLADESTROM_WERT | real | gewichteter Mittelwert 6BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_14_MITTLEREGENAUSLAST_KEINLADESTROM_EINH | string | Prozent |
| STAT_BEREICH_15_NIEDRIGEGENAUSLAST_KEINLADESTROM_WERT | real | gewichteter Mittelwert 6BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_BEREICH_15_NIEDRIGEGENAUSLAST_KEINLADESTROM_EINH | string | Prozent |
| STAT_SCHLECHTLADEBILANZ | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_SCHLECHTLADEBILANZ_EINH | string | Prozent |
| STAT_VERBRAUCHERREDUZIERUNG_BIT_6 | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_VERBRAUCHERREDUZIERUNG_BIT_6_EINH | string | Prozent |
| STAT_GENERATORSTATUS_BIT_5 | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_GENERATORSTATUS_BIT_5_EINH | string | Prozent |
| STAT_GENERATORSTATUS_BIT_6 | real | gewichteter Mittelwert 2BYTE   Einheit: %   Min: 0 Max: 100 |
| STAT_GENERATORSTATUS_BIT_6_EINH | string | Prozent |
| STAT_BSZ_DF | unsigned long | gewichteter Mittelwert 3BYTE   Einheit: Sekunden   Min: 0 Max: 16.777.215 |
| STAT_BSZ_DF_EINH | string | Sekunden |
| STAT_DFFGEN_TEMP_MXCNTR | unsigned long | gewichteter Mittelwert 2BYTE   Einheit: s   Min: 0 Max: 16.777.215 |
| STAT_DFFGEN_TEMP_MXCNTR_EINH | string | Sekunden |
| STAT_DFFGEN_TEMP_NCNTR | unsigned long | gewichteter Mittelwert 2BYTE   Einheit: s   Min: 0 Max: 16.777.215 |
| STAT_DFFGEN_TEMP_NCNTR_EINH | string | Sekunden |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-msainfo2"></a>
### STATUS_MSAINFO2

Auslesen Infospeicher Batteriezustandserkennung 2 UDS*: 0x224092 ReadDataByIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_LADUNGSMENGE_GESAMT_WERT | real | Kumulierte, verbrauchte Ladungsmenge 2BYTE_in 0 bis 19087Ah   Einheit: Ah   Min: 0 Max: 190872 |
| STAT_LADUNGSMENGE_GESAMT_EINH | string | Ah |
| STAT_ANZAHL_MOTORSTART_GESAMT | real | Gesamtzahl Starts 2BYTE in 0 bis 327675   Min: 0 Max: 327675 |
| STAT_ANZAHL_MSASTART_GESAMT | real | Anzahl MSA Starts 2BYTE in 0 bis 327675   Min: 0 Max: 327675 |
| STAT_ANZAHL_FZGSTOP_GESAMT | real | Anzahl Fahrzeugstops 2BYTE in 0 bis 327675   Min: 0 Max: 327675 |
| STAT_ZEIT_IN_MSA_GESAMT_WERT | real | Zeit in MSA 2BYTE in 0 bis 3276750s   Einheit: s   Min: 0 Max: 3276750 |
| STAT_ZEIT_IN_MSA_GESAMT_EINH | string | Sekunde |
| STAT_ZEIT_IN_FZGSTOP_GESAMT_WERT | real | Zeit in Fahrzeugstop 2BYTE in 0 bis 3276750s   Einheit: s   Min: 0 Max: 3276750 |
| STAT_ZEIT_IN_FZGSTOP_GESAMT_EINH | string | Sekunde |
| STAT_BATTSPG_DSOC_INTERVALL1_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG1 und K_DSOCMSADG2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL1_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL2_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG2 und K_DSOCMSADG3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL2_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL3_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG3 und K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL3_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL4_UNTER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &lt; K_TBATT_MSADIAG) mit DSOC groesser K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL4_UNTER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL1_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG1 und K_DSOCMSADG2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL1_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL2_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG2 und K_DSOCMSADG3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL2_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL3_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC zw K_DSOCMSADG3 und K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL3_UEBER_TGRENZ_EINH | string | V |
| STAT_BATTSPG_DSOC_INTERVALL4_UEBER_TGRENZ_WERT | real | gemittelte Spannungslage bei MSA-Starts (Batt-Temp &gt;= K_TBATT_MSADIAG) mit DSOC groesser K_DSOCMSADG4 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_BATTSPG_DSOC_INTERVALL4_UEBER_TGRENZ_EINH | string | V |
| STAT_ANZAHL_MSASTOPPS_INTERVALL_0_BIS_5_SEC | unsigned long | Anzahl der MSA-Stopps mit der Dauer: 0sec &lt;Dauer&lt; 5sec Bytes 20, 21 2BYTE in 0 bis 65535 |
| STAT_ANZAHL_MSASTOPPS_INTERVALL_5_BIS_20_SEC | unsigned long | Anzahl der MSA-Stopps mit der Dauer: &gt;5sec &lt;Dauer&lt; 20sec Bytes 22, 23 2BYTE in 0 bis 65535 |
| STAT_ANZAHL_MSASTOPPS_INTERVALL_20_BIS_45_SEC | unsigned long | Anzahl der MSA-Stopps mit der Dauer: &gt;20sec &lt;Dauer&lt; 45sec Bytes 24, 25 2BYTE in 0 bis 65535 |
| STAT_ANZAHL_MSASTOPPS_GROESSER_45_SEC | unsigned long | Anzahl der MSA-Stopps mit der Dauer: Dauer&gt; 45sec Bytes 26, 27 2BYTE in 0 bis 65535 |
| STAT_MSA_STOP_1_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 1 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_1_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_1_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 1 2BYTE in 0 bis 65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_1_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_1_TEMP_WERT | real | Temp MSA-Stop 1 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_1_TEMP_EINH | string | degreeC |
| STAT_MSA_STOP_2_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 2 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_2_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_2_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 2 2BYTE in 0 bis 65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_2_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_2_TEMP_WERT | real | Temp MSA-Stop 2 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_2_TEMP_EINH | string | degreeC |
| STAT_MSA_STOP_3_MIN_SPANNUNG_WERT | real | minimale Spannungslage MSA Stop 3 MSA_1BYTE_in_7bis15Volt   Einheit: V   Min: 7 Max: 15.16 |
| STAT_MSA_STOP_3_MIN_SPANNUNG_EINH | string | V |
| STAT_MSA_STOP_3_KM_BIT_WERT | unsigned long | km-Stand bei MSA-Stop 3 2BYTE in 0 bis 65535km   Einheit: km   Min: 0 Max: 65535 |
| STAT_MSA_STOP_3_KM_BIT_EINH | string | kilometer |
| STAT_MSA_STOP_3_TEMP_WERT | real | Temp MSA-Stop 3 MSA 1BYTE in -40 bis +214 grad C   Einheit: C   Min: 0 Max: 214 |
| STAT_MSA_STOP_3_TEMP_EINH | string | degreeC |
| STAT_MSA_EA_SOC_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer SOC 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_BATTERIESPANNUNG_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer BATTERIESPANNUNG 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_HOHER_ANLAUFSTROM_E_LUEFTER | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE2 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE3_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE3 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE4_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE4 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE5_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE5 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE6_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE6 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_EA_RESERVE7_AKTUELL_AKTIV | unsigned long | aktuell aktiver Einschaltaufforderer RESERVE7 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_SOC_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer SOC 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_STRTSPG_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Startspannung 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_DIAGNOSE_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Generator-Diagnose 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_TBATT_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Batterietemperatur 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_TRAMODE_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Tra-Mode 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_ZYKL_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer Zyklisierung 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_BNSTROM_AKTUELL_AKTIV | unsigned long | aktuell aktiver Abschaltverhinderer zu hoher Bordnetzstrom 1BIT   1: aktiv    0: nicht aktiv |
| STAT_MSA_AV_NIEDRIGE_BATTTEMP | unsigned long | aktuell aktiver Abschaltverhinderer RESERVE2 1BIT   1: aktiv    0: nicht aktiv |
| STAT_ANZAHL_WIRKSAME_AV_NIEDRIGER_SOC | unsigned long | Anzahl der wirksamen AV: niedriger Ladezustand der Batterie. Gezählt wird nur ein AV während eines Kl15 Zyklus Byte 42 1BYTE in 0 bis 254, ohne Einheit |
| STAT_ANZAHL_WIRKSAME_AV_NIEDRIGE_STARTSPANNUNG | unsigned long | Anzahl der wirksamen AV: niedrige Startspannungslage. Gezählt wird nur ein AV während eines Kl15 Zyklus Byte 43 1BYTE in 0 bis 254, ohne Einheit |
| STAT_ANZAHL_WIRKSAME_AV_HOHE_BATTERIETEMPERATUR | unsigned long | Anzahl der wirksamen AV: hohe Batterietemperatur. Gezählt wird nur ein AV während eines Kl15 Zyklus Byte 44 1BYTE in 0 bis 254, ohne Einheit |
| STAT_ANZAHL_WIRKSAME_AV_HOHER_BORDNETZSTROM | unsigned long | Anzahl der wirksamen AV: hoher BN-Strom. Gezählt wird nur ein AV während eines Kl15 Zyklus Byte 45 1BYTE in 0 bis 254, ohne Einheit |
| STAT_ANZAHL_WIRKSAME_EA_NIEDRIGER_SOC | unsigned long | Anzahl der wirksamen Einschaltanforderer: niedriger Ladezustnd der Batterie. Gezählt wird nur ein EA während eines Kl15 Zyklus Byte 46 1BYTE in 0 bis 254, ohne Einheit |
| STAT_ANZAHL_WIRKSAME_EA_NIEDRIGE_SPANNUNG | unsigned long | Anzahl der wirksamen Einschaltanforderer: niedrige Spannungslage. Gezählt wird nur ein EA während eines Kl15 Zyklus Byte 47 1BYTE in 0 bis 254, ohne Einheit |
| STAT_KM_STAND_BEI_RESET_AV_EV_WERT | unsigned long | KM-Stand bei Reset der Abschaltverhinderer / Einschaltanforderer Zähler Bytes 48, 49 2BYTE in 0 bis 65535 |
| STAT_KM_STAND_BEI_RESET_AV_EV_EINH | string | km |
| STAT_ENTLADUNG_MSASTART_BIS_GENERATORVERSORGUNG_WERT | unsigned long | Entlademenge vom MSA Start bis zur Versorgung durch Generator Bytes 50, 51, 52 3BYTE in 0 bis 167772150, Einheit Amperesekunden |
| STAT_ENTLADUNG_MSASTART_BIS_GENERATORVERSORGUNG_EINH | string | As |
| STAT_ANZAHL_WIRKSAME_AV_NIEDRIGE_BATTTEMP | unsigned long | Label Num_msaav_lowtbatt neues Results ab AEP FR26,0 Ergebnis bei altem Programmstand: 255 Byte 53 1BYTE in 0 bis 254, ohne Einheit |
| STAT_ANZAHL_WIRKSAME_EA_HOHER_ANLAUFSTROM_ELUEFTER | unsigned long | Label Num_msaea_inlwm neues Results ab AEP FR26,0 Ergebnis bei altem Programmstand: 255 Byte 54 1BYTE in 0 bis 254, ohne Einheit |
| STAT_BALT_VERSCHIEBEKONSTANTE_WERT | unsigned long | Verschiebung Kennlinie KL_MSADSOC_AKT in Abhängigkeit von Batteriealterung neues Results ab AEP FR26,0 Ergebnis bei altem Programmstand: 255 Byte 55 1BYTE in 0 bis 254 |
| STAT_BALT_VERSCHIEBEKONSTANTE_EINH | string | % neues Results ab AEP FR26,0 |
| STAT_BALT_KMSTAND_BEI_AENDERUNG_VERSCHIEBEKONSTANTE_WERT | unsigned long | KM-Stand bei Reset der Abschaltverhinderer / Einschaltanforderer Zähler neues Results ab AEP FR26,0 Ergebnis bei altem Programmstand: 655350 Bytes 56, 57 (MSB: 56, LSB: 57) Auflösung 10km 2BYTE in 0 bis 655349 |
| STAT_BALT_KMSTAND_BEI_AENDERUNG_VERSCHIEBEKONSTANTE_EINH | string | km neues Results ab AEP FR26,0 |
| STAT_BALT_BZE3_ALTERUNGSERKENNUNG | long | KM-Stand bei Reset der Abschaltverhinderer / Einschaltanforderer Zähler neues Results ab AEP FR26,0 Ergebnis bei altem Programmstand: 255 Byte 58 Berechnung: Rohwert -100 1BYTE in 0 bis 254 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei neues Results ab AEP FR26,0 |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bzetomsa2"></a>
### STATUS_BZETOMSA2

0x224093 STATUS_BZETOMSA2 Analyse von MSA-Abschaltverhinderern durch BZE3 gegenüber AEPBZE SDG(A2l-NAME=bzetomsa)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_INFOSPEICHER_BZE3_MSA_0_2 | unsigned long | BZE3 AV=0, AEP-BZE AV=0 |
| STAT_INFOSPEICHER_BZE3_MSA_0_2_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_3_5 | unsigned long | BZE3 AV=0, AEP-BZE AV=1 |
| STAT_INFOSPEICHER_BZE3_MSA_3_5_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_6_8 | unsigned long | BZE3 AV=1, AEP-BZE AV=0 |
| STAT_INFOSPEICHER_BZE3_MSA_6_8_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_9_11 | unsigned long | BZE3 AV=1, AEP-BZE AV=1 |
| STAT_INFOSPEICHER_BZE3_MSA_9_11_EINH | string | Sekunden |
| STAT_INFOSPEICHER_BZE3_MSA_12 | unsigned long | Zähler |
| STAT_INFOSPEICHER_BZE3_MSA_12_EINH | string | dimensionslos |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

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
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-aepdfmonitor"></a>
### STATUS_AEPDFMONITOR

0x224015 STATUS_AEPDFMONITOR FASTA-Messwertblock 10 lesen Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BSZSIFNP_WERT | unsigned long | Serviceintervall Betriebsstundenzaehler (bszsifnp_l) 4BYTE in 0 bis 4294967294s   Einheit: s   Min: 0 Max: 4294967294 |
| STAT_BSZSIFNP_EINH | string | second |
| STAT_NMDSFNP_00_WERT | real | Sekundaerkennfeldpunkt 00 STATE_TBL_DRIV[0][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_00_EINH | string | percent |
| STAT_NMDSFNP_10_WERT | real | Sekundaerkennfeldpunkt 10 STATE_TBL_DRIV[1][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_10_EINH | string | percent |
| STAT_NMDSFNP_20_WERT | real | Sekundaerkennfeldpunkt 20 STATE_TBL_DRIV[2][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_20_EINH | string | percent |
| STAT_NMDSFNP_30_WERT | real | Sekundaerkennfeldpunkt 30 STATE_TBL_DRIV[3][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_30_EINH | string | percent |
| STAT_NMDSFNP_40_WERT | real | Sekundaerkennfeldpunkt 40 STATE_TBL_DRIV[4][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_40_EINH | string | percent |
| STAT_NMDSFNP_50_WERT | real | Sekundaerkennfeldpunkt 50 STATE_TBL_DRIV[5][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_50_EINH | string | percent |
| STAT_NMDSFNP_60_WERT | real | Sekundaerkennfeldpunkt 60 STATE_TBL_DRIV[6][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_60_EINH | string | percent |
| STAT_NMDSFNP_70_WERT | real | Sekundaerkennfeldpunkt 70 STATE_TBL_DRIV[7][0]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_70_EINH | string | percent |
| STAT_NMDSFNP_01_WERT | real | Sekundaerkennfeldpunkt 01 STATE_TBL_DRIV[0][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_01_EINH | string | percent |
| STAT_NMDSFNP_11_WERT | real | Sekundaerkennfeldpunkt 11 STATE_TBL_DRIV[1][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_11_EINH | string | percent |
| STAT_NMDSFNP_21_WERT | real | Sekundaerkennfeldpunkt 21 STATE_TBL_DRIV[2][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_21_EINH | string | percent |
| STAT_NMDSFNP_31_WERT | real | Sekundaerkennfeldpunkt 31 STATE_TBL_DRIV[3][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_31_EINH | string | percent |
| STAT_NMDSFNP_41_WERT | real | Sekundaerkennfeldpunkt 41 STATE_TBL_DRIV[4][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_41_EINH | string | percent |
| STAT_NMDSFNP_51_WERT | real | Sekundaerkennfeldpunkt 51 STATE_TBL_DRIV[5][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_51_EINH | string | percent |
| STAT_NMDSFNP_61_WERT | real | Sekundaerkennfeldpunkt 61 STATE_TBL_DRIV[6][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_61_EINH | string | percent |
| STAT_NMDSFNP_71_WERT | real | Sekundaerkennfeldpunkt 71 STATE_TBL_DRIV[7][1]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_71_EINH | string | percent |
| STAT_NMDSFNP_02_WERT | real | Sekundaerkennfeldpunkt 02 STATE_TBL_DRIV[0][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_02_EINH | string | percent |
| STAT_NMDSFNP_12_WERT | real | Sekundaerkennfeldpunkt 12 STATE_TBL_DRIV[1][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_12_EINH | string | percent |
| STAT_NMDSFNP_22_WERT | real | Sekundaerkennfeldpunkt 22 STATE_TBL_DRIV[2][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_22_EINH | string | percent |
| STAT_NMDSFNP_32_WERT | real | Sekundaerkennfeldpunkt 32 STATE_TBL_DRIV[3][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_32_EINH | string | percent |
| STAT_NMDSFNP_42_WERT | real | Sekundaerkennfeldpunkt 42 STATE_TBL_DRIV[4][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_42_EINH | string | percent |
| STAT_NMDSFNP_52_WERT | real | Sekundaerkennfeldpunkt 52 STATE_TBL_DRIV[5][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_52_EINH | string | percent |
| STAT_NMDSFNP_62_WERT | real | Sekundaerkennfeldpunkt 62 STATE_TBL_DRIV[6][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_62_EINH | string | percent |
| STAT_NMDSFNP_72_WERT | real | Sekundaerkennfeldpunkt 72 STATE_TBL_DRIV[7][2]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_72_EINH | string | percent |
| STAT_NMDSFNP_03_WERT | real | Sekundaerkennfeldpunkt 03 STATE_TBL_DRIV[0][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_03_EINH | string | percent |
| STAT_NMDSFNP_13_WERT | real | Sekundaerkennfeldpunkt 13 STATE_TBL_DRIV[1][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_13_EINH | string | percent |
| STAT_NMDSFNP_23_WERT | real | Sekundaerkennfeldpunkt 23 STATE_TBL_DRIV[2][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_23_EINH | string | percent |
| STAT_NMDSFNP_33_WERT | real | Sekundaerkennfeldpunkt 33 STATE_TBL_DRIV[3][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_33_EINH | string | percent |
| STAT_NMDSFNP_43_WERT | real | Sekundaerkennfeldpunkt 43 STATE_TBL_DRIV[4][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_43_EINH | string | percent |
| STAT_NMDSFNP_53_WERT | real | Sekundaerkennfeldpunkt 53 STATE_TBL_DRIV[5][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_53_EINH | string | percent |
| STAT_NMDSFNP_63_WERT | real | Sekundaerkennfeldpunkt 63 STATE_TBL_DRIV[6][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_63_EINH | string | percent |
| STAT_NMDSFNP_73_WERT | real | Sekundaerkennfeldpunkt 73 STATE_TBL_DRIV[7][3]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_73_EINH | string | percent |
| STAT_NMDSFNP_04_WERT | real | Sekundaerkennfeldpunkt 04 STATE_TBL_DRIV[0][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_04_EINH | string | percent |
| STAT_NMDSFNP_14_WERT | real | Sekundaerkennfeldpunkt 14 STATE_TBL_DRIV[1][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_14_EINH | string | percent |
| STAT_NMDSFNP_24_WERT | real | Sekundaerkennfeldpunkt 24 STATE_TBL_DRIV[2][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_24_EINH | string | percent |
| STAT_NMDSFNP_34_WERT | real | Sekundaerkennfeldpunkt 34 STATE_TBL_DRIV[3][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_34_EINH | string | percent |
| STAT_NMDSFNP_44_WERT | real | Sekundaerkennfeldpunkt 44 STATE_TBL_DRIV[4][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_44_EINH | string | percent |
| STAT_NMDSFNP_54_WERT | real | Sekundaerkennfeldpunkt 54 STATE_TBL_DRIV[5][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_54_EINH | string | percent |
| STAT_NMDSFNP_64_WERT | real | Sekundaerkennfeldpunkt 64 STATE_TBL_DRIV[6][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_64_EINH | string | percent |
| STAT_NMDSFNP_74_WERT | real | Sekundaerkennfeldpunkt 74 STATE_TBL_DRIV[7][4]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_74_EINH | string | percent |
| STAT_NMDSFNP_05_WERT | real | Sekundaerkennfeldpunkt 05 STATE_TBL_DRIV[0][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_05_EINH | string | percent |
| STAT_NMDSFNP_15_WERT | real | Sekundaerkennfeldpunkt 15 STATE_TBL_DRIV[1][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_15_EINH | string | percent |
| STAT_NMDSFNP_25_WERT | real | Sekundaerkennfeldpunkt 25 STATE_TBL_DRIV[2][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_25_EINH | string | percent |
| STAT_NMDSFNP_35_WERT | real | Sekundaerkennfeldpunkt 35 STATE_TBL_DRIV[3][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_35_EINH | string | percent |
| STAT_NMDSFNP_45_WERT | real | Sekundaerkennfeldpunkt 45 STATE_TBL_DRIV[4][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_45_EINH | string | percent |
| STAT_NMDSFNP_55_WERT | real | Sekundaerkennfeldpunkt 55 STATE_TBL_DRIV[5][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_55_EINH | string | percent |
| STAT_NMDSFNP_65_WERT | real | Sekundaerkennfeldpunkt 65 STATE_TBL_DRIV[6][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_65_EINH | string | percent |
| STAT_NMDSFNP_75_WERT | real | Sekundaerkennfeldpunkt 75 STATE_TBL_DRIV[7][5]   Einheit: %   Min: 0 Max: 99.609375 |
| STAT_NMDSFNP_75_EINH | string | percent |
| STAT_DFDSFNP_00 | unsigned long | Kennfeldpunkt 00 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_01 | unsigned long | Kennfeldpunkt 01 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_02 | unsigned long | Kennfeldpunkt 02 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_03 | unsigned long | Kennfeldpunkt 03 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_10 | unsigned long | Kennfeldpunkt 10 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_11 | unsigned long | Kennfeldpunkt 11 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_12 | unsigned long | Kennfeldpunkt 12 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_13 | unsigned long | Kennfeldpunkt 13 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_20 | unsigned long | Kennfeldpunkt 20 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_21 | unsigned long | Kennfeldpunkt 21 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_22 | unsigned long | Kennfeldpunkt 22 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_23 | unsigned long | Kennfeldpunkt 23 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_30 | unsigned long | Kennfeldpunkt 30 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_31 | unsigned long | Kennfeldpunkt 31 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_32 | unsigned long | Kennfeldpunkt 32 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_DFDSFNP_33 | unsigned long | Kennfeldpunkt 33 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_IGENKFNP | unsigned long | Generatorstrom kumuliert IGENK   Min: -3e+038 Max: 3e+038 |
| STAT_TMOTB1 | unsigned long | Kuehlmitteltemperatur innerhalb Bereich 1 (tmot_b1) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TMOTB2 | unsigned long | Kuehlmitteltemperatur innerhalb Bereich 2 (tmot_b2) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TMOTB3 | unsigned long | Kuehlmitteltemperatur innerhalb Bereich 3 (tmot_b3) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TMOTB4 | unsigned long | Kuehlmitteltemperatur innerhalb Bereich 4 (tmot_b4) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TMOTB5 | unsigned long | Kuehlmitteltemperatur innerhalb Bereich 5 (tmot_b5) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TOELB1 | unsigned long | Motoroeltemperatur innerhalb Bereich 1 (toel_b1) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TOELB2 | unsigned long | Motoroeltemperatur innerhalb Bereich 2 (toel_b2) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TOELB3 | unsigned long | Motoroeltemperatur innerhalb Bereich 3 (toel_b3) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TOELB4 | unsigned long | Motoroeltemperatur innerhalb Bereich 4 (toel_b4) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TOELB5 | unsigned long | Motoroeltemperatur innerhalb Bereich 5 (toel_b5) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TGETB1 | unsigned long | Getriebeoeltemperatur innerhalb Bereich 1 (tget_b1) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TGETB2 | unsigned long | Getriebeoeltemperatur innerhalb Bereich 2 (tget_b2) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TGETB3 | unsigned long | Getriebeoeltemperatur innerhalb Bereich 3 (tget_b3) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TGETB4 | unsigned long | Getriebeoeltemperatur innerhalb Bereich 4 (tget_b4) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TGETB5 | unsigned long | Getriebeoeltemperatur innerhalb Bereich 5 (tget_b5) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TUMGB1 | unsigned long | Umgebungstemperatur innerhalb Bereich 1 (tumg_b1) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TUMGB2 | unsigned long | Umgebungstemperatur innerhalb Bereich 2 (tumg_b2) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TUMGB3 | unsigned long | Umgebungstemperatur innerhalb Bereich 3 (tumg_b3) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TUMGB4 | unsigned long | Umgebungstemperatur innerhalb Bereich 4 (tumg_b4) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_TUMGB5 | unsigned long | Umgebungstemperatur innerhalb Bereich 5 (tumg_b5) 1BYTE IDENTICAL DEC   Min: 0 Max: 255 |
| STAT_CTR_STC_TECU_1 | unsigned long | statistic counter 1 for TECU monitoring (A2L-Name: ctr_stc_tecu_1) CTR_STC_TECU_1   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_2 | unsigned long | statistic counter 2 for TECU monitoring (A2L-Name: ctr_stc_tecu_2) CTR_STC_TECU_2   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_3 | unsigned long | statistic counter 3 for TECU monitoring (A2L-Name: ctr_stc_tecu_3) CTR_STC_TECU_3   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_4 | unsigned long | statistic counter 4 for TECU monitoring (A2L-Name: ctr_stc_tecu_4) CTR_STC_TECU_4   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_5 | unsigned long | statistic counter 5 for TECU monitoring (A2L-Name: ctr_stc_tecu_5) CTR_STC_TECU_5   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_6 | unsigned long | statistic counter 6 for TECU monitoring (A2L-Name: ctr_stc_tecu_6) CTR_STC_TECU_6   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_7 | unsigned long | statistic counter 7 for TECU monitoring (A2L-Name: ctr_stc_tecu_7) CTR_STC_TECU_7   Min: 0 Max: 4294967295 |
| STAT_CTR_STC_TECU_8 | unsigned long | statistic counter 8 for TECU monitoring (A2L-Name: ctr_stc_tecu_8) CTR_STC_TECU_8   Min: 0 Max: 4294967295 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

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
| STAT_IBSINFO_TEXT | string | gibt aus ob der IBS-Typ richtig ist |
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
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-systemcheck-igr-aus"></a>
### START_SYSTEMCHECK_IGR_AUS

0x3101F0F7 START_SYSTEMCHECK_IGR_AUS Ansteuerung Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-systemcheck-igr-aus"></a>
### STATUS_SYSTEMCHECK_IGR_AUS

0x3103F0F7 STATUS_SYSTEMCHECK_IGR_AUS Auslesen Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_SYSTEMCHECK_IGR_TEXT | string | Funktionsstatus Intelligente Generatorregelung B_DIAGIGR |
| STAT_SYSTEMCHECK_IGR_EINH | string | Funktionsstatus Intelligente Generatorregelung B_DIAGIGR |
| STAT_SYSTEMCHECK_IGR_WERT | int | Funktionsstatus Intelligente Generatorregelung B_DIAGIGR |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-systemcheck-igr-aus"></a>
### STOP_SYSTEMCHECK_IGR_AUS

0x3102F0F7 STOP_SYSTEMCHECK_IGR_AUS Ende Intelligente Generatorregelung deaktivieren Aktivierung: Klemme 15 = EIN Activation: LV_IGK = 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-ruhestrommessung"></a>
### STEUERN_RUHESTROMMESSUNG

Ansteuern Ruhestrompruefung mit IBS UDS  : $31 RoutineControl UDS  : $01 startRoutine UDS  : $F02B Ruhestrompruefung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| I_MAX_WERT | real | Max. Ruhestromschwelle (Eco_max_i) Eco_max_i   Einheit: A   Min: 0 Max: 1.275 |
| MSB_WERT | real | Ecos Messtartbedingung (Eco_msb) Eco_msb   Einheit: s   Min: 0 Max: 12.75 |
| MZ_WERT | real | Dauer Mittelwertmessung (Eco_mz) Eco_mz   Einheit: s   Min: 0 Max: 12.75 |
| TO_WERT | unsigned long | Ecos Messung Timeout (Eco_timo) Eco_timo   Einheit: min   Min: 1 Max: 254 Achtung, Wert 128 ist ungültig |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG (MEN48) |
| _RESPONSE | binary | Hex-Auftrag an SG (MEN48) |

<a id="job-status-ruhestrommessung"></a>
### STATUS_RUHESTROMMESSUNG

Auslesen Ruhestromprüfung mit IBS UDS  : $31 RoutineControl UDS  : $03 requestRoutineResults UDS  : $F02B Ruhestrompruefung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_FS_RUHESTROM_TEXT | string | Funktionsstatus RUHESTROM (Eco_jobstat1) 1BYTE FUNKTIONSSTATUS |
| STAT_FS_RUHESTROM_WERT | int | Status_Fehlerspeicher_Ruhestromwert |
| STAT_FS_RUHESTROM_EINH | string | - |
| STAT_STAT_RUHESTROM_WERT | real | Ruhestrom (Eco_result1) Eco_result1   Einheit: A   Min: 0 Max: 81.9187 |
| STAT_STAT_RUHESTROM_EINH | string | A |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG (MEN48) |
| _RESPONSE | binary | Hex-Auftrag an SG (MEN48) |

<a id="job-steuern-ibs-strommessung"></a>
### STEUERN_IBS_STROMMESSUNG

Ansteuern IBS Strommessung UDS: $31 RoutineControl

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHWELLE_WERT | real | Bereich: 0 - 1310.7 A (A2L_Name: Eco_i_schwelle) |
| HOLDOFF_WERT | real | Bereich: 0 - 2.55 s (A2L_Name: Eco_i_holdoff) |
| MESSZEIT_WERT | real | Bereich: 0 - 0.51 s (A2L_Name: Eco_i_messzeit) |
| TIMEOUT_WERT | real | Bereich: 0 - 25.5 s (A2L_Name: Eco_i_timeout) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |

<a id="job-status-ibs-strommessung"></a>
### STATUS_IBS_STROMMESSUNG

Auslesen IBS Strommessung UDS: $31 RoutineControl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort vom SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| STAT_FS_IBS_STROMMESSUNG | int | (A2L_Name: Eco_i_status) |
| STAT_STROMWERT_WERT | real | (A2L_Name: Eco_i_result) |
| STAT_STROMWERT_EINH | string | A |

<a id="job-status-bzediag"></a>
### STATUS_BZEDIAG

0x22403B STATUS_BZEDIAG BZE Infospeicher

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_BATTERIEKAPAZITAET_AKTUEL_WERT | unsigned long | aktueller Wert C_ist (verfügbare Kapazität) - auf passende Quantisierung angepasst 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_AKTUEL_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_1_MONAT_WERT | unsigned long | C_ist vor 1 Zeiteinheit 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_1_MONAT_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_2_MONAT_WERT | unsigned long | C_ist vor 2 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_2_MONAT_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_3_MONAT_WERT | unsigned long | C_ist vor 3 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_3_MONAT_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_4_MONAT_WERT | unsigned long | C_ist vor 4 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_4_MONAT_EINH | string | Ah |
| STAT_BATTERIEKAPAZITAET_VOR_5_MONAT_WERT | unsigned long | C_ist vor 5 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_BATTERIEKAPAZITAET_VOR_5_MONAT_EINH | string | Ah |
| STAT_Q_BATTERIEKAPAZITAET_AKTUEL_WERT | real | Qualitaetsindex C_ist 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_Q_BATTERIEKAPAZITAET_AKTUEL_EINH | string | percent |
| STAT_LADEZUSTAND_AKTUELL_WERT | unsigned long | Aktueller Wert C_akt (Ladezustand)- auf passende Quantisierung angepasst 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_AKTUELL_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_1_TAG_WERT | unsigned long | C_akt vor 1 Zeiteinheit 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_1_TAG_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_2_TAG_WERT | unsigned long | C_akt vor 2 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_2_TAG_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_3_TAG_WERT | unsigned long | C_akt vor 3 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_3_TAG_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_4_TAG_WERT | unsigned long | C_akt vor 4 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_4_TAG_EINH | string | Ah |
| STAT_LADEZUSTAND_VOR_5_TAG_WERT | unsigned long | C_akt vor 5 Zeiteinheiten 1BYTE_in_0bis255Ah   Einheit: Ah   Min: 0 Max: 255 |
| STAT_LADEZUSTAND_VOR_5_TAG_EINH | string | Ah |
| STAT_Q_LADEZUSTAND_AKTUELL_WERT | real | Qualitaetsindex C_akt 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_Q_LADEZUSTAND_AKTUELL_EINH | string | percent |
| STAT_STROMAUFNAHME_AKTUELL_WERT | unsigned long | nominierte Stromaufnahme aktuell 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_AKTUELL_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_1_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 1 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_1_MONAT_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_2_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 2 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_2_MONAT_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_3_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 3 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_3_MONAT_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_4_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 4 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_4_MONAT_EINH | string | A |
| STAT_STROMAUFNAHME_VOR_5_MONAT_WERT | unsigned long | nominierte Stromaufnahme vor 5 Zeiteinheiten 1BYTE in 0 bis 255 Ampere   Einheit: A   Min: 0 Max: 255 |
| STAT_STROMAUFNAHME_VOR_5_MONAT_EINH | string | A |
| STAT_Q_STROMAUFNAHME_AKTUELL_WERT | real | Qualitaetsindex normierte Stromaufnahme 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_Q_STROMAUFNAHME_AKTUELL_EINH | string | A |
| STAT_Q_BATTERIEZELLE_DEFEKT_WERT | real | Zelldefekt-Signal als Quali-Index 1BYTE in 0 bis 100 Prozent   Einheit: %   Min: 0 Max: 255 |
| STAT_Q_BATTERIEZELLE_DEFEKT_EINH | string | percent |
| STAT_ANZ_BATTERIEWECHSEL | unsigned long | Anzahl der bisher getaetigten Batteriewechsel (0 = Originalbatterie) 4BIT_in_0bis15   Min: 0 Max: 15 |
| STAT_LETZTER_BATTERIEWECHSEL_TEXT | string | Anzeige, ob unzulaessiger Batteriewechsel durchgefuehrt wurde (C_nenn wird kleiner, oder AGM --) Nass) B_bzd_wrgbat |
| STAT_LETZTER_BATTERIEWECHSEL_WERT | int | Anzeige, ob unzulaessiger Batteriewechsel durchgefuehrt wurde (C_nenn wird kleiner, oder AGM --) Nass) |
| STAT_LETZTER_BATTERIEWECHSEL_EINH | string | - B_bzd_wrgbat |
| STAT_BATTERIEZUSTAND_TEXT | string | Zustand der Batterie / Tauschempfehlung Bzd_btzust |
| STAT_BATTERIEZUSTAND_WERT | int | Zustand der Batterie / Tauschempfehlung |
| STAT_BATTERIEZUSTAND_EINH | string | - Bzd_btzust |
| STAT_WASSERVERLUST_TEXT | string | Anzeige Wasserverlust ueberschreitet Grenzwert B_qvch2o |
| STAT_WASSERVERLUST_WERT | int | Anzeige Wasserverlust ueberschreitet Grenzwert |
| STAT_WASSERVERLUST_EINH | string | - B_qvch2o |
| STAT_TIEFENTLADUNG_TEXT | string | Anzeige Batterie wurde tiefentladen B_bzd_te |
| STAT_TIEFENTLADUNG_WERT | int | Anzeige Batterie wurde tiefentladen |
| STAT_TIEFENTLADUNG_EINH | string | - B_bzd_te |
| STAT_IBS_BZE_TEXT | string | Gibt an, ob eine IBS mit BZE3 erkannt wurde und die BZE-Daten somit relevant sind. B_bzdon |
| STAT_IBS_BZE_WERT | int | Gibt an, ob eine IBS mit BZE3 erkannt wurde und die BZE-Daten somit relevant sind. B_bzdon |
| STAT_IBS_BZE_EINH | string | - |
| STAT_PROGNOSE_KALTSTART_SOMMER_U_WERT | real | Praedizierter Klemmspannungswert Kaltstart Sommer Bze_pu   Einheit: V   Min: 0 Max: 25.5 |
| STAT_PROGNOSE_KALTSTART_SOMMER_U_EINH | string | V |
| STAT_PROGNOSE_KALTSTART_WINTER_U_WERT | real | Praedizierter Klemmspannungswert Kaltstart Winter Bze_pu   Einheit: V   Min: 0 Max: 25.5 |
| STAT_PROGNOSE_KALTSTART_WINTER_U_EINH | string | V |
| STAT_PROGNOSE_WARMSTART_U_WERT | real | Praedizierter Klemmspannungswert Warmstart Bze_pu   Einheit: V   Min: 0 Max: 25.5 |
| STAT_PROGNOSE_WARMSTART_U_EINH | string | V |
| STAT_PROGNOSE_WARMSTART_VORHALT_WERT | real | Vorhalt praedizierter Klemmspannungswert Warmstart Sommer/Winter Bze_pu   Einheit: V   Min: 0 Max: 25.5 |
| STAT_PROGNOSE_WARMSTART_VORHALT_EINH | string | V |
| STAT_R_BATTERIE_INITIAL_WERT | real | Initialer Innenwiderstand der Fzg.-Batterie nach Einbau / Tausch Bze_rbatt   Einheit: mOhm   Min: 0 Max: 25.5 |
| STAT_R_BATTERIE_INITIAL_EINH | string | mOhm |
| STAT_R_BATTERIE_AKTUELL_WERT | real | aktueller Innenwiderstand der Fzg.-Batterie Bze_rbatt   Einheit: mOhm   Min: 0 Max: 25.5 |
| STAT_R_BATTERIE_AKTUELL_EINH | string | mOhm |
| STAT_TREND_WARMSTART_U_WERT | real | Trendwert Klemmspannungsprognose Warmstart Bzd_wcstrend   Einheit: V   Min: -8 Max: 7.9375 |
| STAT_TREND_WARMSTART_U_EINH | string | V |
| STAT_TREND_WARMSTART_SOWI_U_WERT | real | Vorhalt Trendwert Klemmspannungsprognose Warmstart Sommer/Winter Bzd_wcwtrend   Einheit: V   Min: -8 Max: 7.9375 |
| STAT_TREND_WARMSTART_SOWI_U_EINH | string | V |
| STAT_BATTERIETEMPERATUR_MIN_AKTUELL_WERT | real | Klimaprofil: Wert vor 0 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_AKTUELL_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_1_MONAT_WERT | real | Klimaprofil: Wert vor 1 Monat Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_1_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_2_MONAT_WERT | real | Klimaprofil: Wert vor 2 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_2_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_3_MONAT_WERT | real | Klimaprofil: Wert vor 3 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_3_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_4_MONAT_WERT | real | Klimaprofil: Wert vor 4 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_4_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_5_MONAT_WERT | real | Klimaprofil: Wert vor 5 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_5_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_6_MONAT_WERT | real | Klimaprofil: Wert vor 6 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_6_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_7_MONAT_WERT | real | Klimaprofil: Wert vor 7 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_7_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_8_MONAT_WERT | real | Klimaprofil: Wert vor 8 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_8_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_9_MONAT_WERT | real | Klimaprofil: Wert vor 9 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_9_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_10_MONAT_WERT | real | Klimaprofil: Wert vor 10 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_10_MONAT_EINH | string | degreeC |
| STAT_BATTERIETEMPERATUR_MIN_VOR_11_MONAT_WERT | real | Klimaprofil: Wert vor 11 Monaten Bzd_klima   Einheit: C   Min: -64 Max: 63.5 |
| STAT_BATTERIETEMPERATUR_MIN_VOR_11_MONAT_EINH | string | degreeC |
| STAT_WASSERVERLUSTABS_WERT | real | Wasserverlust Qv_h2o_zg   Einheit: g/Ah   Min: 0 Max: 10 |
| STAT_WASSERVERLUSTABS_EINH | string | grammPerAmpereHour |
| STAT_STANDZEIT_LADEZUSTAND_NIEDRIG_AKTUELL | unsigned long | Vorhalt Sulfatierungsindex (Summe) 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_STANDZEIT_LADEZUSTAND_NIEDRIG_GESAMT | unsigned long | Vorhalt Sulfatierungsrate 2BYTE in 0 bis 65534   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIEKAPAZITAET_WERT | unsigned long | Absolutzeit juengster Historieneintrag C_ist 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIEKAPAZITAET_EINH | string | d |
| STAT_ZEIT_LETZTER_EINTRAG_LADEZUSTAND_WERT | unsigned long | Absolutzeit juengster Historieneintrag C_akt 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_LADEZUSTAND_EINH | string | d |
| STAT_ZEIT_LETZTER_EINTRAG_STROMAUFNAHME_WERT | unsigned long | Absolutzeit juengster Historieneintrag nominierte Stromaufnahme 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_STROMAUFNAHME_EINH | string | d |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIETEMPERATUR_WERT | unsigned long | Absolutzeit juengster Historieneintrag Klima 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTER_EINTRAG_BATTERIETEMPERATUR_EINH | string | d |
| STAT_ZEIT_LETZTE_TRENDWERTERMITTLUNG_WERT | unsigned long | Absolutzeit letzte Trendwertermittlung 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_LETZTE_TRENDWERTERMITTLUNG_EINH | string | d |
| STAT_ZEIT_SEIT_LETZTEM_BATTERIEWECHSEL_WERT | unsigned long | Zeit seit letztem Batterietausch 2BYTE_in_0bis65534d   Min: 0 Max: 65534 |
| STAT_ZEIT_SEIT_LETZTEM_BATTERIEWECHSEL_EINH | string | d |
| STAT_ENTLADUNG_MOTOR_AUS_KLEINER_MINUS10AH_WERT | unsigned long | Entladung waehrend Motor aus &lt; -10Ah (Ladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_KLEINER_MINUS10AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_MINUS10AH_BIS_0AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen -10Ah und 0Ah (Ladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_MINUS10AH_BIS_0AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_0AH_BIS_5AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 0Ah und 5Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_0AH_BIS_5AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_5AH_BIS_10AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 5Ah und 10Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_5AH_BIS_10AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_10AH_BIS_15AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 10Ah und 15Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_10AH_BIS_15AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_15AH_BIS_25AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 15Ah und 25Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_15AH_BIS_25AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_25AH_BIS_50AH_WERT | unsigned long | Entladung waehrend Motor aus zwischen 25Ah und 50Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_25AH_BIS_50AH_EINH | string | Ah |
| STAT_ENTLADUNG_MOTOR_AUS_GROESSER_50AH_WERT | unsigned long | Entladung waehrend Motor aus &gt; 50Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_ENTLADUNG_MOTOR_AUS_GROESSER_50AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_KLEINER_MINUS20AH_WERT | unsigned long | Ladung waehrend Motor ein &lt; -20Ah (Entladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_KLEINER_MINUS20AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_MINUS20AH_BIS_MINUS10AH_WERT | unsigned long | Ladung waehrend Motor ein zwischen -20Ah und -10Ah (Entladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_MINUS20AH_BIS_MINUS10AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_MINUS10AH_BIS_0AH_WERT | unsigned long | Ladung waehrend Motor ein zwischen -10Ah und 0Ah (Entladung) 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_MINUS10AH_BIS_0AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_0AH_BIS_10AH_WERT | unsigned long | Ladung waehrend Motor ein zwischen 0Ah und 10Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_0AH_BIS_10AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_10AH_BIS_20AH_WERT | unsigned long | Ladung waehrend Motor ein zwischen 10Ah und 20Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_10AH_BIS_20AH_EINH | string | Ah |
| STAT_LADUNG_MOTOR_EIN_GROESSER_20AH_WERT | unsigned long | Ladung waehrend Motor ein &gt; 20Ah 2BYTE_in_0bis65534Ah   Einheit: Ah   Min: 0 Max: 65534 |
| STAT_LADUNG_MOTOR_EIN_GROESSER_20AH_EINH | string | Ah |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-bzediag2"></a>
### STATUS_BZEDIAG2

Auslesen Infospeicher Batteriezustandserkennung 2 UDS*: $22 ReadDataByIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_ENTLADUNG_MSA_BEREICH1 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 1) |
| STAT_ENTLADUNG_MSA_BEREICH2 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 2) |
| STAT_ENTLADUNG_MSA_BEREICH3 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 3) |
| STAT_ENTLADUNG_MSA_BEREICH4 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 4) |
| STAT_ENTLADUNG_MSA_BEREICH5 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 5) |
| STAT_ENTLADUNG_MSA_BEREICH6 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 6) |
| STAT_ENTLADUNG_MSA_BEREICH7 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 7) |
| STAT_ENTLADUNG_MSA_BEREICH8 | unsigned int | Histogramm Batterieentladung im MSA-Stopp (Bereich 8) |
| STAT_TIEFENTLADUNG_AKTUELL | real | Index für Schädigungsgrad der aktuellen Tiefentladung |
| STAT_TIEFENTLADUNG_GESAMT | real | Index für den Schädigungsgrad aller Tiefentladungen |
| STAT_SOH_CIST | real | Alterungsindex auf Basis C_ist |
| STAT_SOH_WASSERVERLUST | real | Alterungsindex auf Basis Qv_h2o_zg |
| STAT_SOH_STANDZEIT | real | Alterungsindex auf Basis Bzd_sulfind |
| STAT_SOH_ZYKLEN | real | Alterungsindex auf Basis SoC-abhängiger Zyklenzähler |
| STAT_SOH_ENTLADUNG_STAND | real | Alterungsindex auf Basis Entladehistogramm im Stand |
| STAT_SOH_LADUNG_FAHRT | real | Alterungsindex auf Basis Ladehistogramm während der Fahrt |
| STAT_SOH_ENTLADUNG_MSA | real | Alterungsindex auf Basis Entladehistogramm im MSA-Stopp |
| STAT_SOH_TIEFENTLADUNG | real | Alterungsindex auf Basis Bzd_tiefentlabs |
| STAT_SOH_BATTERIE | real | Index für den aktuellen Alterungszustand der Batterie (SoH) |
| STAT_VOLLZYKLEN_GEWICHTET | real | Vollzyklenzähler der Batterie. Entladung wird je nach SoC gewichtet |
| STAT_ENTLADUNG_GEWICHTET_WERT | real | gewichteter Entladezähler abhängig vom SoC |
| STAT_ENTLADUNG_GEWICHTET_EINH | string | Einheit des gewichteten Entladezählers (Ah) |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-status-verbraucherstrom-efii"></a>
### STATUS_VERBRAUCHERSTROM_EFII

Auslesen Verbraucherstrommessung EFII UDS  : $31   RoutineControl UDS  : $03   routineControlType UDS  : $7002 routineIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STATUS_WERT | unsigned int | Ecos2 Funktionsstati Wert |
| STAT_STATUS_EINH | string | Ecos2 Funktionsstati Einheit |
| STAT_STATUS_TEXT | string | Ecos2 Funktionsstati Text |
| STAT_BEWERTUNG | char | Ecos2 Resultat Bewertung |
| STAT_GRUNDWERT_WERT | real | Ecos2 Strom Grundwert in A |
| STAT_GRUNDWERT_EINH | string | Strom in A |
| STAT_DIFFERENZWERT_WERT | real | Ecos2 Strom Messwert in A |
| STAT_DIFFERENZWERT_EINH | string | Strom in A |
| STAT_TRANSIENT | binary | Transienten Array |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |
| JOB_STATUS | string | OKAY, wenn fehlerfrei |

<a id="job-steuern-batterietausch-registrieren"></a>
### STEUERN_BATTERIETAUSCH_REGISTRIEREN

UDS $31 01 F030 Batterietausch registrieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG (MEN48) |
| _RESPONSE | binary | Hex-Auftrag an SG (MEN48) |

<a id="job-steuern-ende-verbraucherstrom-efii"></a>
### STEUERN_ENDE_VERBRAUCHERSTROM_EFII

Ansteuerung Verbraucherstrommessung EFII (IBS) beenden UDS  : $31   RoutineControl UDS  : $02   routineControlType UDS  : $7002 routineIdentifier

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-verbraucherstrom-efii"></a>
### STEUERN_VERBRAUCHERSTROM_EFII

Ansteuerung Verbraucherstrommessung EFII (IBS) UDS  : $31   RoutineControl UDS  : $01   routineControlType UDS  : $7002 routineIdentifier

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STARTTRIGGERWERT | long | Ecos2 Start Trigger Wert [mA] |
| AUSSCHALTTRIGGER | long | Ecos2 Ende Trigger Wert [mA] |
| TOTZEIT | int | Ecos2 Strommessung holdoff Zeit [ms] |
| MESSZEIT | int | Ecos2 Messzeit [ms] |
| UNTERE_TOLERANZ | long | Ecos2 untere Stromschwelle [mA] |
| OBERE_TOLERANZ | long | Ecos2 obere Stromschwelle [mA] |
| MESSPUNKTE | int | Ecos2 Anzahl Messpunkte [-] |
| TRIGGERFILTER | int | Ecos2 Triggerfilter [ms] |
| MESSWERTFILTER | int | Ecos2 Messfilter [ms] |
| TIMEOUT | int | Ecos2 timeout Zeit [s] |
| POSTTRIGGER | int | Ecos2 Nachtrigger Aufzeichnung [ms] |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei table JobResult STATUS_TEXT |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-aep-i12-zyklisches-nachladen-info"></a>
### STATUS_AEP_I12_ZYKLISCHES_NACHLADEN_INFO

Auslesen von wichtigen Kenngrößen der letzten 4 Vorgänge des zykllischen Nachladens plus dem letzten Parkvorgang AEP_I12_ZYKLISCHES_NACHLADEN_INFO (0x22 409D)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_PARKEN_SYSTEMZEIT_WERT | unsigned long | Systemzeit beim Parken Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_PARKEN_SYSTEMZEIT_EINH | string | "s" |
| STAT_PARKEN_KILOMETERSTAND_WERT | unsigned long | Kilometerstand beim Parken |
| STAT_PARKEN_KILOMETERSTAND_EINH | string | "km" |
| STAT_PARKEN_NV_BATTERIE_SOC_WERT | real | Niedervolt SOC beim Parken Einheit: % Min: 0.0 Max: 127.5 |
| STAT_PARKEN_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E1_PARKEN_SYSTEMZEIT_WERT | unsigned long | 1. Ereignis (letzte): Systemzeit beim Parken Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E1_PARKEN_SYSTEMZEIT_EINH | string | "s" |
| STAT_E1_PARKEN_KILOMETERSTAND_WERT | unsigned long | 1. Ereignis (letzte): Kilometerstand beim Parken |
| STAT_E1_PARKEN_KILOMETERSTAND_EINH | string | "km" |
| STAT_E1_PARKEN_NV_BATTERIE_SOC_WERT | real | 1. Ereignis (letzte): Niedervolt SOC beim Parken Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E1_PARKEN_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E1_START_ZYKNL_SYSTEMZEIT_WERT | unsigned long | 1. Ereignis (letzte): Systemzeit beim Start des zyklischen Nachladens Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E1_START_ZYKNL_SYSTEMZEIT_EINH | string | "s" |
| STAT_E1_START_ZYKNL_NV_BATTERIE_SOC_WERT | real | 1. Ereignis (letzte): Niedervolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E1_START_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E1_START_ZYKNL_HV_BATTERIE_SOC_WERT | real | 1. Ereignis (letzte): Hochvolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E1_START_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E1_START_ZYKNL_NV_BATTERIE_TEMPERATUR_WERT | real | 1. Ereignis (letzte): Temperatur der Niedervolt Batterie beim Start des zyklischen Nachladens |
| STAT_E1_START_ZYKNL_NV_BATTERIE_TEMPERATUR_EINH | string | "°C" |
| STAT_E1_LADEDAUER_WERT | unsigned int | 1. Ereignis (letzte): Dauer des zyklischen Nachladens Einheit: s Min: 0.0 Max: 65535.0 |
| STAT_E1_LADEDAUER_EINH | string | "s" |
| STAT_E1_ENDE_ZYKNL_NV_BATTERIE_SOC_WERT | real | 1. Ereignis (letzte): Niedervolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E1_ENDE_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E1_ENDE_ZYKNL_HV_BATTERIE_SOC_WERT | real | 1. Ereignis (letzte): Hochvolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E1_ENDE_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E1_GRUND_LADEENDE | unsigned char | Sensorfehler eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 0 Min: 0.0 Max: 15.0 |
| STAT_E1_ZYKNL_PROGNOSE_EIN | unsigned char | Lagereglerabweichung eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 3 Min: 0.0 Max: 1.0 |
| STAT_E2_PARKEN_SYSTEMZEIT_WERT | unsigned long | 2. Ereignis: Systemzeit beim Parken Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E2_PARKEN_SYSTEMZEIT_EINH | string | "s" |
| STAT_E2_PARKEN_KILOMETERSTAND_WERT | unsigned long | 2. Ereignis: Kilometerstand beim Parken |
| STAT_E2_PARKEN_KILOMETERSTAND_EINH | string | "km" |
| STAT_E2_PARKEN_NV_BATTERIE_SOC_WERT | real | 2. Ereignis: Niedervolt SOC beim Parken Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E2_PARKEN_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E2_START_ZYKNL_SYSTEMZEIT_WERT | unsigned long | 2. Ereignis: Systemzeit beim Start des zyklischen Nachladens Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E2_START_ZYKNL_SYSTEMZEIT_EINH | string | "s" |
| STAT_E2_START_ZYKNL_NV_BATTERIE_SOC_WERT | real | 2. Ereignis: Niedervolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E2_START_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E2_START_ZYKNL_HV_BATTERIE_SOC_WERT | real | 2. Ereignis: Hochvolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E2_START_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E2_START_ZYKNL_NV_BATTERIE_TEMPERATUR_WERT | real | 2. Ereignis: Temperatur der Niedervolt Batterie beim Start des zyklischen Nachladens |
| STAT_E2_START_ZYKNL_NV_BATTERIE_TEMPERATUR_EINH | string | "°C" |
| STAT_E2_LADEDAUER_WERT | unsigned int | 2. Ereignis: Dauer des zyklischen Nachladens Einheit: s Min: 0.0 Max: 65535.0 |
| STAT_E2_LADEDAUER_EINH | string | "s" |
| STAT_E2_ENDE_ZYKNL_NV_BATTERIE_SOC_WERT | real | 2. Ereignis: Niedervolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E2_ENDE_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E2_ENDE_ZYKNL_HV_BATTERIE_SOC_WERT | real | 2. Ereignis: Hochvolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E2_ENDE_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E2_GRUND_LADEENDE | unsigned char | Sensorfehler eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 0 Min: 0.0 Max: 15.0 |
| STAT_E2_ZYKNL_PROGNOSE_EIN | unsigned char | Lagereglerabweichung eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 3 Min: 0.0 Max: 1.0 |
| STAT_E3_PARKEN_SYSTEMZEIT_WERT | unsigned long | 3. Ereignis: Systemzeit beim Parken Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E3_PARKEN_SYSTEMZEIT_EINH | string | "s" |
| STAT_E3_PARKEN_KILOMETERSTAND_WERT | unsigned long | 3. Ereignis: Kilometerstand beim Parken |
| STAT_E3_PARKEN_KILOMETERSTAND_EINH | string | "km" |
| STAT_E3_PARKEN_NV_BATTERIE_SOC_WERT | real | 3. Ereignis: Niedervolt SOC beim Parken Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E3_PARKEN_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E3_START_ZYKNL_SYSTEMZEIT_WERT | unsigned long | 3. Ereignis: Systemzeit beim Start des zyklischen Nachladens Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E3_START_ZYKNL_SYSTEMZEIT_EINH | string | "s" |
| STAT_E3_START_ZYKNL_NV_BATTERIE_SOC_WERT | real | 3. Ereignis: Niedervolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E3_START_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E3_START_ZYKNL_HV_BATTERIE_SOC_WERT | real | 3. Ereignis: Hochvolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E3_START_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E3_START_ZYKNL_NV_BATTERIE_TEMPERATUR_WERT | real | 3. Ereignis: Temperatur der Niedervolt Batterie beim Start des zyklischen Nachladens |
| STAT_E3_START_ZYKNL_NV_BATTERIE_TEMPERATUR_EINH | string | "°C" |
| STAT_E3_LADEDAUER_WERT | unsigned int | 3. Ereignis: Dauer des zyklischen Nachladens Einheit: s Min: 0.0 Max: 65535.0 |
| STAT_E3_LADEDAUER_EINH | string | "s" |
| STAT_E3_ENDE_ZYKNL_NV_BATTERIE_SOC_WERT | real | 3. Ereignis: Niedervolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E3_ENDE_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E3_ENDE_ZYKNL_HV_BATTERIE_SOC_WERT | real | 3. Ereignis: Hochvolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E3_ENDE_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E3_GRUND_LADEENDE | unsigned char | Sensorfehler eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 0 Min: 0.0 Max: 15.0 |
| STAT_E3_ZYKNL_PROGNOSE_EIN | unsigned char | Lagereglerabweichung eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 3 Min: 0.0 Max: 1.0 |
| STAT_E4_PARKEN_SYSTEMZEIT_WERT | unsigned long | 4. Ereignis: Systemzeit beim Parken Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E4_PARKEN_SYSTEMZEIT_EINH | string | "s" |
| STAT_E4_PARKEN_KILOMETERSTAND_WERT | unsigned long | 4. Ereignis: Kilometerstand beim Parken |
| STAT_E4_PARKEN_KILOMETERSTAND_EINH | string | "km" |
| STAT_E4_PARKEN_NV_BATTERIE_SOC_WERT | real | 4. Ereignis: Niedervolt SOC beim Parken Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E4_PARKEN_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E4_START_ZYKNL_SYSTEMZEIT_WERT | unsigned long | 4. Ereignis: Systemzeit beim Start des zyklischen Nachladens Einheit: s Min: 0.0 Max: 4.294967295E9 |
| STAT_E4_START_ZYKNL_SYSTEMZEIT_EINH | string | "s" |
| STAT_E4_START_ZYKNL_NV_BATTERIE_SOC_WERT | real | 4. Ereignis: Niedervolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E4_START_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E4_START_ZYKNL_HV_BATTERIE_SOC_WERT | real | 4. Ereignis: Hochvolt SOC beim Start des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E4_START_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E4_START_ZYKNL_NV_BATTERIE_TEMPERATUR_WERT | real | 4. Ereignis: Temperatur der Niedervolt Batterie beim Start des zyklischen Nachladens |
| STAT_E4_START_ZYKNL_NV_BATTERIE_TEMPERATUR_EINH | string | "°C" |
| STAT_E4_LADEDAUER_WERT | unsigned int | 4. Ereignis: Dauer des zyklischen Nachladens Einheit: s Min: 0.0 Max: 65535.0 |
| STAT_E4_LADEDAUER_EINH | string | "s" |
| STAT_E4_ENDE_ZYKNL_NV_BATTERIE_SOC_WERT | real | 4. Ereignis: Niedervolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E4_ENDE_ZYKNL_NV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E4_ENDE_ZYKNL_HV_BATTERIE_SOC_WERT | real | 4. Ereignis: Hochvolt SOC am Ende des zyklischen Nachladens Einheit: % Min: 0.0 Max: 127.5 |
| STAT_E4_ENDE_ZYKNL_HV_BATTERIE_SOC_EINH | string | "%" |
| STAT_E4_GRUND_LADEENDE | unsigned char | Sensorfehler eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 0 Min: 0.0 Max: 15.0 |
| STAT_E4_ZYKNL_PROGNOSE_EIN | unsigned char | Lagereglerabweichung eWG vorhanden a2l-Name: SwSABMW_stAddlRespWgeTst2 Bit 3 Min: 0.0 Max: 1.0 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-aep-i12-zyklisches-nachladen-histogramm"></a>
### STATUS_AEP_I12_ZYKLISCHES_NACHLADEN_HISTOGRAMM

Auslesen der Histogramme über die Standzeit bis zum Beginn des zyklischen Nachladens und der Ladedauern der zyklischen Nachladevorgänge AEP_I12_ZYKLISCHES_NACHLADEN_HISTOGRAMM (0x22 409E)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_A | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich A. Bereich A &lt;= K_STDZEITLADEHISTGRZ1 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [0] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_B | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich A. Bereich A &lt;= K_STDZEITLADEHISTGRZ1 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [1] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_C | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich C. K_STDZEITLADEHISTGRZ2 (Tage) &lt; Bereich C &lt;= K_STDZEITLADEHISTGRZ3 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [2] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_D | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich D. K_STDZEITLADEHISTGRZ3 (Tage) &lt; Bereich D &lt;= K_STDZEITLADEHISTGRZ4 (Tage) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [3] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_E | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich E. K_STDZEITLADEHISTGRZ4 (Tage) &lt; Bereich E &lt;= K_STDZEITLADEHISTGRZ5 (Tage) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [4] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_F | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich F. K_STDZEITLADEHISTGRZ5 (Tage) &lt; Bereich F &lt;= K_STDZEITLADEHISTGRZ6 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [5] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_G | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich G. K_STDZEITLADEHISTGRZ6 (Tage) &lt; Bereich G &lt;= K_STDZEITLADEHISTGRZ7 (Tage) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [6] Min: 0.0 Max: 255.0 |
| STAT_STANDZEIT_START_ZYKNL_BEREICH_H | unsigned char | Anzahl der Standzeiten bis zum Beginn des zyklischen Nachladens im Bereich H. K_STDZEITLADEHISTGRZ7 (Tage) &lt; Bereich H (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [7] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_A | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich A. Bereich A &lt;= K_NLDDAUERHISTGRZ1 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [8] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_B | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich B. K_NLDDAUERHISTGRZ1 (Minuten) &lt; Bereich B &lt;= K_NLDDAUERHISTGRZ2 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [9] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_C | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich C. K_NLDDAUERHISTGRZ2 (Minuten) &lt; Bereich C &lt;= K_NLDDAUERHISTGRZ3 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [10] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_D | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich D. K_NLDDAUERHISTGRZ3 (Minuten) &lt; Bereich D &lt;= K_NLDDAUERHISTGRZ4 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [11] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_E | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich E. K_NLDDAUERHISTGRZ4 (Minuten) &lt; Bereich E &lt;= K_NLDDAUERHISTGRZ5 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [12] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_F | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich F. K_NLDDAUERHISTGRZ5 (Minuten) &lt; Bereich F &lt;= K_NLDDAUERHISTGRZ6 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [13] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_G | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich G. K_NLDDAUERHISTGRZ6 (Minuten) &lt; Bereich F &lt;= K_NLDDAUERHISTGRZ7 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [14] Min: 0.0 Max: 255.0 |
| STAT_LADUNGSDAUER_BEREICH_H | unsigned char | Anzahl der Ladungsdauer des zyklischen Nachladens im Bereich G. K_NLDDAUERHISTGRZ6 (Minuten) &lt; Bereich F &lt;= K_NLDDAUERHISTGRZ7 (Minuten) (Zählung bis 255, danach keine Zählung, Wert bleibt erhalten) Histogramm zyklisches Nachladen Auslesen des Array Zyknlhist[16] SY_AEP_ZYKNL == 1 a2l-Name: Zyknlhist Array [15] Min: 0.0 Max: 255.0 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-steuern-aep-i12-test-ladeendegrund"></a>
### _STEUERN_AEP_I12_TEST_LADEENDEGRUND

Job zum Test für AEP Funktionen AEP_I12_GRUND_LADEENDE (0x2E 5FA0)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SW_DIAG_AEP_LADEENDEGRUND | unsigned char | Schreiben von Zyknlinfodiag Min: 0.0 Max: 255.0 a2l-Name: Zyknlinfodiag |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-aep-i12-zyknl-infospeicher-loeschen"></a>
### _START_AEP_I12_ZYKNL_INFOSPEICHER_LOESCHEN

Löschen des Historienspeichers für die letzen 4 Ladevorgänge der 12V-Batterie aus der Hochvolt-Batterie AEP_I12_ZYKNL_INFOSPEICHER_LOESCHEN (0x31 01 AE02)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-aep-i12-zyknl-histogramm-loeschen"></a>
### _START_AEP_I12_ZYKNL_HISTOGRAMM_LOESCHEN

Löschen von Histogramm und Zähler aller Ladevorgänge der 12V-Batterie aus dem Hochvolt-System AEP_I12_ZYKNL_HISTOGRAMM_LOESCHEN (0x31 01 AE03)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-start-aep-i12-test-batteryguard"></a>
### _START_AEP_I12_TEST_BATTERYGUARD

Anforderung Aufruf BatteryGuard Call Setzen der Größe B_batteryguardcalldiag =1 Startvoraussetzungen: B_kl15 == TRUE. AEP_I12_TEST_BATTERYGUARD (0x31 01 F052)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-status-aep-i12-test-batteryguard"></a>
### _STATUS_AEP_I12_TEST_BATTERYGUARD

Anforderung Aufruf BatteryGuard Call auslesen Startvoraussetzungen: B_kl15 == TRUE. AEP_I12_TEST_BATTERYGUARD (0x31 03 F052)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STAT_DIAG_AEP_BATTERYGUARD | unsigned char | Auslesen aktueller Status von B_batteryguardcalldiag Min: 0.0 Max: 1.0 |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

<a id="job-stop-aep-i12-test-batteryguard"></a>
### _STOP_AEP_I12_TEST_BATTERYGUARD

Anforderung Aufruf BatteryGuard Call beenden Setzen der Größe B_batteryguardcalldiag =0 Startvoraussetzungen: B_kl15 == TRUE. AEP_I12_TEST_BATTERYGUARD (0x31 02 F052)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| _REQUEST | binary | Hex-Auftrag an SG |
| _RESPONSE | binary | Hex-Antwort von SG |

## Tables

### Index

- [JOBRESULT](#table-jobresult) (76 × 2)
- [LIEFERANTEN](#table-lieferanten) (137 × 2)
- [FARTTEXTE](#table-farttexte) (35 × 2)
- [DIGITALARGUMENT](#table-digitalargument) (17 × 2)
- [PROZESSKLASSEN](#table-prozessklassen) (26 × 3)
- [SVK_ID](#table-svk-id) (65 × 2)
- [DTCEXTENDEDDATARECORDNUMBER](#table-dtcextendeddatarecordnumber) (5 × 3)
- [DTCSNAPSHOTIDENTIFIER](#table-dtcsnapshotidentifier) (5 × 9)
- [FEHLERKLASSE](#table-fehlerklasse) (5 × 2)
- [BETRIEBSMODE](#table-betriebsmode) (6 × 3)
- [FDETAILSTRUKTUR](#table-fdetailstruktur) (6 × 2)
- [FORTTEXTE](#table-forttexte) (1 × 3)
- [FUMWELTTEXTE](#table-fumwelttexte) (1 × 9)
- [IDETAILSTRUKTUR](#table-idetailstruktur) (4 × 2)
- [IORTTEXTE](#table-iorttexte) (1 × 3)
- [IUMWELTTEXTE](#table-iumwelttexte) (1 × 9)
- [JOBRESULTEXTENDED](#table-jobresultextended) (3 × 2)
- [MOTORUDSCODIERUNG_RUHESTROM](#table-motorudscodierung-ruhestrom) (16 × 2)
- [MSD85UDS_CNV_S_2_DEF_BIT_UB_741_CM](#table-msd85uds-cnv-s-2-def-bit-ub-741-cm) (2 × 2)
- [IBS_DEAK](#table-ibs-deak) (10 × 2)
- [TABLE_STATUS_LETZTER_BATTERIEWECHSEL](#table-table-status-letzter-batteriewechsel) (2 × 2)
- [TABLE_STATUS_BATTERIEZUSTAND](#table-table-status-batteriezustand) (4 × 2)
- [TABLE_STATUS_WASSERVERLUST](#table-table-status-wasserverlust) (2 × 2)
- [TABLE_STATUS_TIEFENTLADUNG](#table-table-status-tiefentladung) (2 × 2)
- [TABLE_STATUS_IBS_BZE](#table-table-status-ibs-bze) (2 × 2)
- [TABLE_STATUS_ECO2_FUNKTIONSSTATI](#table-table-status-eco2-funktionsstati) (11 × 2)

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 76 rows × 2 columns

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
| ?19? | ERROR_ECU_RESPONSE_INCORRECT_ROUTINE_IDENTIFIER |
| ?1A? | ERROR_ECU_RESPONSE_INCORRECT_RESET_TYPE |
| ?1B? | ERROR_ECU_RESPONSE_INCORRECT_SERIAL_NUMBER_FORMAT |
| ?1C? | ERROR_ECU_RESPONSE_INCORRECT_DTC_BY_STATUS_MASK |
| ?1D? | ERROR_ECU_RESPONSE_INCORRECT_DTC_STATUS_AVAILABILITY_MASK |
| ?1E? | ERROR_ECU_RESPONSE_INCORRECT_ROUTINE_CONTROL_IDENTIFIER |
| ?50? | ERROR_BYTE1 |
| ?51? | ERROR_BYTE2 |
| ?52? | ERROR_BYTE3 |
| ?60? | ERROR_VERIFY |
| ?61? | ERROR_ECU_RESPONSE_ZGW |
| ?62? | ERROR_ECU_RESPONSE_BACKUP |
| ?70? | ERROR_CALID_CVN_INCORRECT_LEN |
| ?80? | ERROR_SVK_INCORRECT_LEN |
| ?81? | ERROR_SVK_INCORRECT_FINGERPRINT |
| ?F0? | ERROR_ARGUMENT |
| 0xXY | ERROR_ECU_UNKNOWN_NEGATIVE_RESPONSE |

<a id="table-lieferanten"></a>
### LIEFERANTEN

Dimensions: 137 rows × 2 columns

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
| 0x0000A9 | Thyssen Krupp Presta |
| 0x0000AA | ArvinMeritor |
| 0x0000AB | Kongsberg Automotive GmbH |
| 0x0000AC | SMR Automotive Mirrors |
| 0x0000AD | So.Ge.Mi. |
| 0x0000AE | MTA |
| 0x0000AF | Alfmeier |
| 0x0000B0 | ELTEK VALERE DEUTSCHLAND GMBH |
| 0x0000B1 | Omron Automotive Electronics Europe Group |
| 0x0000B2 | ASK |
| 0x0000B3 | CML Innovative Technologies GmbH & Co. KG |
| 0x0000B4 | APAG Elektronik AG |
| 0x0000B5 | Nexteer Automotive World Headquarters |
| 0x0000B6 | Hans Widmaier |
| 0x0000B7 | Robert Bosch Battery Systems GmbH |
| 0x0000B8 | KYOCERA Display Corporation |
| 0x0000B9 | MAGNA Powertrain AG & Co KG |
| 0x0000BA | BorgWarner |
| 0x0000BB | BMW - Fahrzeugsimulator |
| 0x0000BC | Benteler Duncan Plant |
| 0x0000BD | U-Shin |
| 0x0000BE | Schaeffler Technologies |
| 0xFFFFFF | unbekannter Hersteller |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 35 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | keine Fehlerart verfügbar |
| 0x04 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x05 | Fehler momentan vorhanden und bereits gespeichert |
| 0x08 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x09 | Fehler momentan vorhanden und bereits gespeichert |
| 0x0C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x0D | Fehler momentan vorhanden und bereits gespeichert |
| 0x20 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x21 | Fehler momentan vorhanden und bereits gespeichert |
| 0x24 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x25 | Fehler momentan vorhanden und bereits gespeichert |
| 0x28 | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x29 | Fehler momentan vorhanden und bereits gespeichert |
| 0x2C | Fehler momentan nicht vorhanden, aber bereits gespeichert |
| 0x2D | Fehler momentan vorhanden und bereits gespeichert |
| 0x40 | unbekannte Fehlerart |
| 0x44 | Fehler gespeichert |
| 0x45 | Fehler gespeichert |
| 0x48 | Fehler gespeichert |
| 0x49 | Fehler gespeichert |
| 0x4C | Fehler gespeichert |
| 0x4D | Fehler gespeichert |
| 0x60 | Fehler gespeichert |
| 0x61 | Fehler gespeichert |
| 0x64 | Fehler gespeichert |
| 0x65 | Fehler gespeichert |
| 0x68 | Fehler gespeichert |
| 0x69 | Fehler gespeichert |
| 0x6C | Fehler gespeichert |
| 0x6D | Fehler gespeichert |
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

Dimensions: 26 rows × 3 columns

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
| 0xC0 | SWUP | Software-Update Package |
| 0xC1 | SWIP | Index Software-Update Package |
| 0xA0 | ENTD | Entertainment Daten |
| 0xA1 | NAVD | Navigation Daten |
| 0xA2 | FCFN | Freischaltcode Funktion |
| 0x04 | GWTB | Gateway-Tabelle |
| 0x0D | SWFK | BEGU: Detaillierung auf SWE-Ebene |
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

<a id="table-betriebsmode"></a>
### BETRIEBSMODE

Dimensions: 6 rows × 3 columns

| WERT | TEXT | BEDEUTUNG |
| --- | --- | --- |
| 0x00 | Allgemeiner Fertigungs- und Energiesparmode | Hier deaktivierte Funktionen gemäß FeTra-Liste festhalten |
| 0x01 | Spezieller Energiesparmode | - |
| 0x02 | ECOS-Mode | - |
| 0x03 | MOST-Mode | - |
| 0x04 | Rollenmode | - |
| 0xFF | ungültiger Betriebsmode | ungültig |

<a id="table-fdetailstruktur"></a>
### FDETAILSTRUKTUR

Dimensions: 6 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |
| F_UWB_SATZ | 2 |
| F_HLZ_VIEW | - |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 1 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 1 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-idetailstruktur"></a>
### IDETAILSTRUKTUR

Dimensions: 4 rows × 2 columns

| NAME | TYP |
| --- | --- |
| F_UWB_ERW | ja |
| SAE_CODE | nein |
| F_HLZ | nein |
| F_SEVERITY | nein |

<a id="table-iorttexte"></a>
### IORTTEXTE

Dimensions: 1 rows × 3 columns

| ORT | ORTTEXT | EREIGNIS_DTC |
| --- | --- | --- |
| 0xFFFFFF | unbekannter Fehlerort | 0 |

<a id="table-iumwelttexte"></a>
### IUMWELTTEXTE

Dimensions: 1 rows × 9 columns

| UWNR | UWTEXT | UW_EINH | L/H | UWTYP | NAME | MUL | DIV | ADD |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xXYXY | unbekannte Umweltbedingung | - | - | - | - | - | - | - |

<a id="table-jobresultextended"></a>
### JOBRESULTEXTENDED

Dimensions: 3 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 01 | ERROR |
| 02 | ERROR_ARGUMENT |
| 0xXY | ERROR_UNKNOWN |

<a id="table-motorudscodierung-ruhestrom"></a>
### MOTORUDSCODIERUNG_RUHESTROM

Dimensions: 16 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Ruhestrom kleiner 80mA, keine Aktion des IBS |
| 1 | Ruhestrom = 80...200mA, keine Aktion da Entladung kleiner Schwellwert |
| 2 | Ruhestrom = 200...1000mA, keine Aktion da Entladung kleiner Schwellwert |
| 3 | Ruhestrom groesser 1000mA, keine Aktion da Entladung kleiner Schwellwert |
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

<a id="table-msd85uds-cnv-s-2-def-bit-ub-741-cm"></a>
### MSD85UDS_CNV_S_2_DEF_BIT_UB_741_CM

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | -- |
| 1 | -- |

<a id="table-ibs-deak"></a>
### IBS_DEAK

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

<a id="table-table-status-letzter-batteriewechsel"></a>
### TABLE_STATUS_LETZTER_BATTERIEWECHSEL

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Wechsel zulässig |
| 1 | Wechsel unzulässig |

<a id="table-table-status-batteriezustand"></a>
### TABLE_STATUS_BATTERIEZUSTAND

Dimensions: 4 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Batterie i.O. |
| 1 | Batterie pruefen |
| 2 | Batterie nicht i.O. |
| 3 | ungueltig |

<a id="table-table-status-wasserverlust"></a>
### TABLE_STATUS_WASSERVERLUST

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Wasserverlust i.O. |
| 1 | Wasserverlust nicht i.O. |

<a id="table-table-status-tiefentladung"></a>
### TABLE_STATUS_TIEFENTLADUNG

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Batterie i.O. |
| 1 | Batterie durch Tiefentladung geschädigt |

<a id="table-table-status-ibs-bze"></a>
### TABLE_STATUS_IBS_BZE

Dimensions: 2 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | BZE nicht aktiv |
| 1 | BZE aktiv |

<a id="table-table-status-eco2-funktionsstati"></a>
### TABLE_STATUS_ECO2_FUNKTIONSSTATI

Dimensions: 11 rows × 2 columns

| NR | TEXT |
| --- | --- |
| 0 | Funktion nicht gestartet |
| 2 | Stop-Routine erfolgreich abgearbeitet |
| 3 | Funktion wartet auf Freigabe |
| 4 | Parameter unplausibel |
| 5 | Warten auf Trigger |
| 6 | Trigger erkannt |
| 7 | Funktion abgebrochen, Motor läuft oder keine Rückmeldung vom IBS |
| 8 | Messung beendet |
| 9 | Funktion abgebrochen, Time Out erreicht |
| 10 | Messung beendet, Time Out erreicht |
| 255 | Ungültiger Wert |
