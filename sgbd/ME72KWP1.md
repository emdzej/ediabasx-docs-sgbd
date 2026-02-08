# ME72KWP1.prg

- Jobs: [158](#jobs)
- Tables: [20](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | ME72KWP1 |
| ORIGIN | BMW TI-431 Schaller |
| REVISION | 2.3 |
| AUTHOR | BMW TP-421 Weber, BMW TI-431 Schiefer, BMW TI-431 Dennert, BMW TI-431 Schaller |
| COMMENT | N/A |
| PACKAGE | 0.08 |
| SPRACHE | deutsch |

## Jobs

### Index

- [INFO](#job-info) - Information SGBD
- [initialisierung](#job-initialisierung) - Default Init-Job
- [IDENT](#job-ident) - Ident-Daten fuer DME
- [SEED_KEY](#job-seed-key) - Schutzmechanismus SEED_KEY
- [DIGITAL_DSLSR_LESEN](#job-digital-dslsr-lesen) - Auslesen des DSLSR-Info
- [STATUS_DIGITAL_MFL](#job-status-digital-mfl) - Status Schalteingaenge
- [DK_ANSCHLAG](#job-dk-anschlag)
- [STATUS_DIGITAL_SONDE](#job-status-digital-sonde) - Status Schalteingaenge
- [STATUS_DIGITAL_TEILE](#job-status-digital-teile) - Status Schalteingaenge
- [STATUS_DIGITAL_LL](#job-status-digital-ll) - Status Schalteingaenge
- [STATUS_DIGITAL_ABGAS](#job-status-digital-abgas) - Status Schalteingaenge
- [STATUS_DIGITAL_CHECK](#job-status-digital-check) - Status Schalteingaenge
- [STATUS_DIGITAL_PKW](#job-status-digital-pkw) - Status Schalteingaenge
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [ECU_CONFIG](#job-ecu-config) - Ident-Daten fuer DME
- [ABGAS_VARIANTE_LESEN](#job-abgas-variante-lesen) - Auslesen der Abgasvariante
- [STATUS_GEBERRAD_ADAPTION](#job-status-geberrad-adaption) - Geberradadaption
- [FS_LESEN](#job-fs-lesen) - Fehlerspeicher auslesen ueber RAM lesen
- [STATUS_DIGITAL_TEST](#job-status-digital-test) - Status Schalteingaenge
- [STATUS_DIGITAL](#job-status-digital) - Status Schalteingaenge
- [STATUS_SOLLDREHZAHL](#job-status-solldrehzahl)
- [STATUS_DK_LRNSTEP](#job-status-dk-lrnstep)
- [STATUS_VANOS](#job-status-vanos)
- [SG_ADRESSEN](#job-sg-adressen) - Steuergeaetespezifische Adressen
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Diagnose beenden
- [DIAGNOSE_STOP](#job-diagnose-stop) - Diagnose beenden mit KWP-Befehl COM_STOP
- [STEUERN_SYNC_MODE](#job-steuern-sync-mode)
- [WECHSELCODE_SYNC_DME](#job-wechselcode-sync-dme) - Wechselcodesynchronisation EWS 3 - DME anstossen
- [STATUS_SYNC_MODE](#job-status-sync-mode)
- [FS_LESEN_STATUS](#job-fs-lesen-status) - Auslesen des Fehlerspeichers
- [FS_LESEN_KWP](#job-fs-lesen-kwp) - Auslesen des Fehlerspeichers
- [STEUERN_LL_DREHZAHL_VERSTELLEN](#job-steuern-ll-drehzahl-verstellen) - LL-Drehzahl verstellen,  512-2550 U/min
- [STEUERN_VANOS_VERSTELLZEIT](#job-steuern-vanos-verstellzeit) - Verstellzeitmessung VANOS
- [STATUS_VERSTELLZEIT_MESS_VANOS](#job-status-verstellzeit-mess-vanos) - Verstellzeitmessung Nockenwelle Einlass
- [STEUERN_VANOS_DICHTHEIT](#job-steuern-vanos-dichtheit) - Dichtheitsmessung VANOS
- [STEUERN_VANOS_TEST_STOP](#job-steuern-vanos-test-stop) - Dichtheitsmessung VANOS
- [STATUS_DICHTHEIT_MESS_VANOS](#job-status-dichtheit-mess-vanos) - DICHTHEITmessung Nockenwelle Einlass
- [STATUS_SYSTEMCHECK_LAUFUNRUHE](#job-status-systemcheck-laufunruhe) - Laufunruhe lesen
- [LESEN_SYSTEMCHECK_LAUFUNRUHE](#job-lesen-systemcheck-laufunruhe) - Laufunruhe lesen
- [STEUERN_EKP](#job-steuern-ekp) - EKP ansteuern
- [STEUERN_EV_1](#job-steuern-ev-1) - EV  1 ansteuern
- [STEUERN_EV_2](#job-steuern-ev-2) - EV  2 ansteuern
- [STEUERN_EV_3](#job-steuern-ev-3) - EV 3 ansteuern
- [STEUERN_EV_4](#job-steuern-ev-4) - EV 4 ansteuern
- [STEUERN_EV_5](#job-steuern-ev-5) - EV  5 ansteuern
- [STEUERN_EV_6](#job-steuern-ev-6) - EV  6 ansteuern
- [STEUERN_EV_7](#job-steuern-ev-7) - EV  6 ansteuern
- [STEUERN_EV_8](#job-steuern-ev-8) - EV  6 ansteuern
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - E-Luefter verstellen , Bereich 0-100%
- [STEUERN_E_LUEFTER_ECOS](#job-steuern-e-luefter-ecos) - E-Luefter verstellen , Bereich 0-100%
- [STEUERN_EBOX_LUEFTER](#job-steuern-ebox-luefter) - E-Box Luefter verstellen 0 oder 1
- [STATUS_S_EVAN_S](#job-status-s-evan-s) - Nockenwinkel Sollwert  auslesen
- [STATUS_NW_B1_FL1](#job-status-nw-b1-fl1) - Adaptionswinkel NW-B1 Flanke 1
- [STATUS_NW_B1_FL2](#job-status-nw-b1-fl2) - Adaptionswinkel NW-B1 Flanke 2
- [STATUS_NW_B1_FL3](#job-status-nw-b1-fl3) - Adaptionswinkel NW-B1 Flanke 3
- [STATUS_NW_B1_FL4](#job-status-nw-b1-fl4) - Adaptionswinkel NW-B1 Flanke 4
- [STATUS_NW_B2_FL1](#job-status-nw-b2-fl1) - Adaptionswinkel NW-B1 Flanke 1
- [STATUS_NW_B2_FL2](#job-status-nw-b2-fl2) - Adaptionswinkel NW-B1 Flanke 2
- [STATUS_NW_B2_FL3](#job-status-nw-b2-fl3) - Adaptionswinkel NW-B2 Flanke 3
- [STATUS_NW_B2_FL4](#job-status-nw-b2-fl4) - Adaptionswinkel NW-B2 Flanke 4
- [STATUS_EINSPRITZZEIT](#job-status-einspritzzeit) - Einspritzzeit EV1
- [STATUS_LAMBDA_INTEGRATOR_1](#job-status-lambda-integrator-1) - Lambdaregler1
- [STATUS_INT](#job-status-int) - Lambdaregler1
- [STATUS_LAMBDA_INTEGRATOR_2](#job-status-lambda-integrator-2) - Lambdaregler2
- [STATUS_INT_2](#job-status-int-2) - Lambdaregler2
- [STATUS_GESCHWINDIGKEIT](#job-status-geschwindigkeit) - Fahrzeuggeschwindigkeit
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Motordrehzahl
- [STATUS_MOTORDREHZAHL_SOLL](#job-status-motordrehzahl-soll) - LL-Solldrehzahl
- [STATUS_VANOS_NW_LAGE_EINLASS_BANK_1](#job-status-vanos-nw-lage-einlass-bank-1) - Nockenwellenposition Bank1
- [STATUS_VANOS_NW_LAGE_EINLASS_BANK_2](#job-status-vanos-nw-lage-einlass-bank-2) - Nockenwellenposition Bank2
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - Ansauglufttemperatur
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - Motortemperatur
- [STATUS_ZUENDWINKEL](#job-status-zuendwinkel) - Zuendwinkel Zyl1
- [STATUS_DKP_WINKEL](#job-status-dkp-winkel) - DK-Winkel
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - Luftmasse
- [STATUS_LMM](#job-status-lmm) - Auslesen Luftmasse kg/h
- [STATUS_MIIST](#job-status-miist) - MIIST
- [STATUS_UBATT](#job-status-ubatt) - Ubatt
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [STATUS_PWG_POTI_SPANNUNG](#job-status-pwg-poti-spannung) - Fahrerwunsch
- [STATUS_PWG_TEST](#job-status-pwg-test) - Fahrerwunsch
- [STATUS_KUEHLW_AUSL_TEMPERATUR](#job-status-kuehlw-ausl-temperatur) - Temperatur Kuehleraustritt
- [STATUS_LDB_INTEGRATOR](#job-status-ldb-integrator) - Integrator Ladebilanz Batterie
- [STATUS_LS_VKAT_SIGNAL_1](#job-status-ls-vkat-signal-1) - Lambdasondenspannung v Kat
- [STATUS_L_SONDE](#job-status-l-sonde) - Lambdasondenspannung v Kat
- [STATUS_LS_VKAT_SIGNAL_2](#job-status-ls-vkat-signal-2) - Lambdasondenspannung v Kat 2
- [STATUS_L_SONDE_2](#job-status-l-sonde-2) - Lambdasondenspannung v Kat 2
- [STATUS_LS_NKAT_SIGNAL_1](#job-status-ls-nkat-signal-1) - Lambdasondenspannung n Kat
- [STATUS_L_SONDE_H](#job-status-l-sonde-h) - Lambdasondenspannung n Kat
- [STATUS_LS_NKAT_SIGNAL_2](#job-status-ls-nkat-signal-2) - Lambdasondenspannung n Kat 2
- [STATUS_L_SONDE_2_H](#job-status-l-sonde-2-h) - Lambdasondenspannung n Kat 2
- [STATUS_LAMBDA_ADD_1](#job-status-lambda-add-1) - Gemischadaption additiv 1
- [STATUS_ADD](#job-status-add) - Gemischadaption additiv 1
- [STATUS_LAMBDA_ADD_2](#job-status-lambda-add-2) - Gemischadaption additiv 2
- [STATUS_ADD_2](#job-status-add-2) - Gemischadaption additiv 2
- [STATUS_LAMBDA_MUL_1](#job-status-lambda-mul-1) - Gemischadaption multipl. 1
- [STATUS_MUL](#job-status-mul) - Gemischadaption multipl. 1
- [STATUS_LAMBDA_MUL_2](#job-status-lambda-mul-2) - Gemischadaption multipl. 2
- [STATUS_MUL_2](#job-status-mul-2) - Gemischadaption multipl. 2
- [STATUS_LS_VKAT_HEIZUNG_TV_1](#job-status-ls-vkat-heizung-tv-1) - norm. Heizleist. L-Sonde vKat1
- [STATUS_LS_VKAT_HEIZUNG_TV_2](#job-status-ls-vkat-heizung-tv-2) - norm. Heizleist. L-Sonde vKat2
- [STATUS_LS_NKAT_HEIZUNG_TV_1](#job-status-ls-nkat-heizung-tv-1) - norm. Heizleist. L-Sonde hKat1
- [STATUS_LS_NKAT_HEIZUNG_TV_2](#job-status-ls-nkat-heizung-tv-2) - norm. Heizleist. L-Sonde hKat2
- [STATUS_LS_VKAT_PERIODENDAUER_1](#job-status-ls-vkat-periodendauer-1) - PeridenDauer L-Sonde v Kat1
- [STATUS_LS_VKAT_PERIODENDAUER_2](#job-status-ls-vkat-periodendauer-2) - PeridenDauer L-Sonde v Kat2
- [STATUS_TE_TASTVERHAELTNIS](#job-status-te-tastverhaeltnis) - Tastverhaeltnis TEV
- [STATUS_VANOS_NW_LAGE_EINLASS_TV_1](#job-status-vanos-nw-lage-einlass-tv-1) - Tastverhaeltnis Vanos 1
- [STATUS_VANOS_NW_LAGE_EINLASS_TV_2](#job-status-vanos-nw-lage-einlass-tv-2) - Tastverhaeltnis Vanos 2
- [STATUS_E_LUEFTER_TV](#job-status-e-luefter-tv) - Tastverhaeltnis E-Luefter
- [STATUS_LUTSFI1](#job-status-lutsfi1) - gefilterte Laufunruhen Zyl1
- [STATUS_LUTSFI2](#job-status-lutsfi2) - gefilterte Laufunruhen Zyl2
- [STATUS_LUTSFI3](#job-status-lutsfi3) - gefilterte Laufunruhen Zyl3
- [STATUS_LUTSFI4](#job-status-lutsfi4) - gefilterte Laufunruhen Zyl4
- [STATUS_LUTSFI5](#job-status-lutsfi5) - gefilterte Laufunruhen Zyl5
- [STATUS_LUTSFI6](#job-status-lutsfi6) - gefilterte Laufunruhen Zyl6
- [STATUS_LUTSFI7](#job-status-lutsfi7) - gefilterte Laufunruhen Zyl7
- [STATUS_LUTSFI8](#job-status-lutsfi8) - gefilterte Laufunruhen Zyl8
- [ADAPT_SELEKTIV_LOESCHEN](#job-adapt-selektiv-loeschen) - Adaptionen selektiv loeschen
- [ADAPT_LOESCHEN](#job-adapt-loeschen) - Adaptionen selektiv loeschen
- [START_SYSTEMCHECK_SEK_LUFT](#job-start-systemcheck-sek-luft) - Systemcheck  Sekundaerluft starten
- [STOP_SYSTEMCHECK_SEK_LUFT](#job-stop-systemcheck-sek-luft) - Systemcheck  Sekundaerluft starten
- [START_SYSTEMCHECK_TANK_LECK](#job-start-systemcheck-tank-leck) - Systemcheck Tankentlueftungssystem Leckdiagnose starten
- [START_SYSTEMCHECK_DMTL](#job-start-systemcheck-dmtl) - Systemcheck Tankentlueftungssystem Leckdiagnose starten
- [START_SYSTEMCHECK_DMTL_ECOS](#job-start-systemcheck-dmtl-ecos) - Systemcheck Tankentlueftungssystem Leckdiagnose starten
- [LESEN_SYSTEMCHECK_SEK_LUFT](#job-lesen-systemcheck-sek-luft) - Systemcheck  Sekundaerluft lesen
- [LESEN_SYSTEMCHECK_SEK_LUFT_1](#job-lesen-systemcheck-sek-luft-1) - Systemcheck  Sekundaerluft lesen
- [LESEN_SYSTEMCHECK_TANK_LECK](#job-lesen-systemcheck-tank-leck) - Systemcheck Tankentlueftungssystem Leckdiagnose lesen
- [LESEN_SYSTEMCHECK_DMTL](#job-lesen-systemcheck-dmtl) - Systemcheck Tankentlueftungssystem Leckdiagnose lesen
- [STATUS_DMTL_EOL](#job-status-dmtl-eol) - Systemcheck Tankentlueftungssystem Leckdiagnose lesen
- [CO_ABGLEICH_LESEN](#job-co-abgleich-lesen) - CO-Abgleich lesen
- [CO_ABGLEICH_VERSTELLEN](#job-co-abgleich-verstellen) - CO-Drehzahl  verstellen
- [CO_ABGLEICH_PROGRAMMIEREN](#job-co-abgleich-programmieren) - CO-Drehzahl Abgleich programmieren
- [STEUERN_TESTPLATZ](#job-steuern-testplatz) - Freischaltung fuer SG-Befundung ansteuern
- [STATUS_KTEST_MOTORDREHZAHL](#job-status-ktest-motordrehzahl) - Motordrehzahl auslesen
- [STATUS_KTEST_AN_LUFTTEMPERATUR](#job-status-ktest-an-lufttemperatur) - Ansauglufttemperatur auslesen
- [STATUS_KTEST_MOTORTEMPERATUR](#job-status-ktest-motortemperatur) - Ansauglufttemperatur auslesen
- [STATUS_KTEST_DKP_WINKEL](#job-status-ktest-dkp-winkel) - Ansauglufttemperatur auslesen
- [STATUS_KTEST_VANOS_NW_LAGE_E_BANK_1](#job-status-ktest-vanos-nw-lage-e-bank-1) - Nockenwellenposition Bank1
- [STATUS_KTEST_VANOS_NW_LAGE_E_BANK_2](#job-status-ktest-vanos-nw-lage-e-bank-2) - Nockenwellenposition Bank2
- [STEUERN_KTEST_VANOS_VERSTELLZEIT](#job-steuern-ktest-vanos-verstellzeit) - Verstellzeitmessung VANOS
- [STATUS_KLOPFSENSOR1](#job-status-klopfsensor1) - Geraeuschwert Klopfsensor 1
- [STATUS_KLOPFSENSOR2](#job-status-klopfsensor2) - Geraeuschwert Klopfsensor 2
- [STATUS_KLOPFSENSOR3](#job-status-klopfsensor3) - Geraeuschwert Klopfsensor 3
- [STATUS_KLOPFSENSOR4](#job-status-klopfsensor4) - Geraeuschwert Klopfsensor 4
- [STEUERN_EV_SELEKTIV_AUSBLENDEN](#job-steuern-ev-selektiv-ausblenden) - EV selektiv ausblenden, Zylinder 1- 6 angeben
- [ABGLEICH_TIMER_VERSTELLEN_PROGRAMMIEREN](#job-abgleich-timer-verstellen-programmieren) - FGR-Funktion und Mainswitch konfigurieren
- [STEUERN_TEV](#job-steuern-tev) - Stellgliedansteuerung TEV
- [STEUERN_TEV_AUS](#job-steuern-tev-aus) - Stellgliedansteuerung TEV
- [TEV_SYSTEM](#job-tev-system) - Status Systemtest TEV
- [TEV_ZYKLUS](#job-tev-zyklus) - Zyklusflags Systemtest TEV auslesen
- [TEV_ENDE](#job-tev-ende) - Systemtestende von TEV
- [START_SYSTEMCHECK_TEV_FUNC](#job-start-systemcheck-tev-func) - Stellgliedansteuerung TEV
- [LESEN_SYSTEMCHECK_TEV_FUNC](#job-lesen-systemcheck-tev-func) - Zyklusflags Systemtest TEV auslesen
- [STATUS_GASPEDAL](#job-status-gaspedal) - Fahrerwunsch
- [STEUERN_LUFTFILTERKLAPPE](#job-steuern-luftfilterklappe) - Luftfilterklappe oeffnen bzw. schliessen
- [STEUERN_DMTL_HEIZUNG](#job-steuern-dmtl-heizung) - Stellgliedansteuerung DM-TL-Pumpenheizung

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
### initialisierung

Default Init-Job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn job erfolgreich 0 wenn job nicht erfolgreich |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer DME

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | string | BMW-Hardwarenummer |
| ID_COD_INDEX | string | Codier-Index |
| ID_DIAG_INDEX | string | Diagnose-Index |
| ID_BUS_INDEX | string | Bus-Index |
| ID_DATUM_KW | string | Herstelldatum KW |
| ID_DATUM_JAHR | string | Herstelldatum Jahr |
| ID_LIEF_NR | string | Lieferanten-Nummer |
| ID_SW_NR | string | Softwarenummer |
| ID_AI_NR | string | Aenderungsindex |
| ID_PROD_NR | string | Produktionsnummer |
| ID_AIF_VORHANDEN | int | Ist ein AIF vorhanden (0 (nein)/ 1 (ja)) |
| ID_MOTOR | string | Parameter fuer MoTest Motorkennung |
| ID_LAMBDA_STEREO | int | Parameter fuer MoTest 0=Mono, 1=STEREO |
| ID_EML | int | Parameter fuer MoTest 0=Kein EML verb, 1=EML M70, 2=EML M73 |
| ID_LU_MESSUNG | int | Parameter fuer MoTest 1=Laufunruhemessung sonst 0 |
| ID_OBD2 | int | Parameter fuer MoTest 0=ECE, 1=OBD2-Fahrzeug |
| ID_SG_HERSTELLER | int | Parameter fuer MoTest 0=Bosch, 1=Siemens-Fahrzeug |
| ID_EWS_SS | int | Identifikation EWS-Schnittstelle |

<a id="job-seed-key"></a>
### SEED_KEY

Schutzmechanismus SEED_KEY

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SEED_KEY | binary | Rueckgabewert Status |
| Z_ZAHL | int | Zufallszahl |

<a id="job-digital-dslsr-lesen"></a>
### DIGITAL_DSLSR_LESEN

Auslesen des DSLSR-Info

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_B_DSL | binary |  |
| STAT_TKATM | int |  |
| STAT_ML | int |  |

<a id="job-status-digital-mfl"></a>
### STATUS_DIGITAL_MFL

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_L_FGR | int | FGR Bereitschaftsanzeige (Byte 6, x1xx xxxx) |
| STAT_B_FGRTVE | int | MFL Taste Verzoegern (Byte 6, xxx1 xxxx) |
| STAT_B_FGRHSA | int | MFL Taste Mainswitch aus (Byte 6, xxxx xx1x) |
| STAT_B_FGRTSE | int | MFL Taste Setzen Beschleunigen (Byte 6, xxxx 1xxx) |
| STAT_B_FGRAT | int | MFL Taste Aus ( Byte 6, xxxx xxx1) |
| STAT_B_FGRTWA | int | MFL Taste Wiederaufnahme ( Byte 6, xx1x xxxx) |
| STAT_B_FGRTBE | int | FGR Bereitschaftsanzeige ( Byte 6, xxxx x1xx) |

<a id="job-dk-anschlag"></a>
### DK_ANSCHLAG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-digital-sonde"></a>
### STATUS_DIGITAL_SONDE

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_B_SBBHK | int | Sonde betreibsbereit hinter KAT (Byte 7, xxxx 1xxx) |
| STAT_B_HSHE2 | int | Sondenheizung 2 hinter Kat angesteuert (Byte 13, x1xx xxxx) |
| STAT_B_SBBVK2 | int | Sonde betreibsbereit vor Kat 2 (Byte 7, xxx1 xxxx) |
| STAT_B_HSVE | int | Lambdasondenheizung 1 vor Kat (Byte 13, xx1x xxxx) |
| STAT_B_HSVE2 | int | Lambdasondenheizung 2 vor Kat ( Byte 13, xxx1 xxxx) |
| STAT_B_HSHE | int | Lambdasondenheizung 1 hinter Kat ( Byte 13, 1xxx xxxx) |
| STAT_B_SBBVK | int | Sonde betriebsbereit vor Kat ( Byte 7, xx1x xxxx) |
| STAT_B_SBBHK2 | int | Sonde betriebsbereit hinter Kat 2 ( Byte 7, xxxx x1xx) |

<a id="job-status-digital-teile"></a>
### STATUS_DIGITAL_TEILE

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_B_UMAERF | int | unt. mech. DK-Anschlag erfolgreich gelernt (Byte 8, xx1x xxxx) |
| STAT_B_EWS_OK | int | EWS in Ordnung (Byte 8, xxx1 xxxx) |
| STAT_B_SLP | int | Sekundaerluftpumpe (Byte 13, xxxx x1xx) |
| STAT_B_STA | int | Start (Byte 14, 1xxx xxxx) |
| STAT_B_EBL | int | E-Box-Luefter ( Byte 14, xxx1 xxxx) |
| STAT_B_KUPPL | int | Kupplung ( Byte 7, xxxx x1xx) |
| STAT_B_BLS | int | Bremslichtschalter ( Byte 7, xxxx 1xxx) |
| STAT_B_BRS | int | Bremslichttestschalter ( Byte 7, xxx1 xxxx) |
| STAT_B_KO | int | Klimakompressor ( Byte 7, 1xxx xxxx) |
| STAT_B_KOE | int | Kompressoreinschalten ( Byte 13, xxxx 1xxx) |
| STAT_B_EKP | int | Elektrokraftstoffpumpe ( Byte 14, xx1x xxxx) |
| STAT_B_KL15 | int | Kl. 15 ( Byte 7, xxxx xxx1) |
| STAT_B_LR | int | Leerlaufregler 1 ( Byte 7, xxxx xx1x) |
| STAT_B_LR2 | int | Leerlaufregler 2 ( Byte 7, x1xx xxxx) |
| STAT_B_VL | int | Vollast ( Byte 7, xxxx xx1x) |
| STAT_B_LL | int | Leerlauf ( Byte 7, xxxx xxx1) |
| STAT_B_SLV | int | Sekundaerluftventil ( Byte 13, xxxx xx1x) |
| STAT_B_ETR | int | Abgasrueckfuehrung ( Byte 14, x1xx xxxx) |
| STAT_S_LDPR | int | Leckdiagnosepumpenrelais ( Byte 7, xx1x xxxx) |
| STAT_B_LDPEIN | int | LDP ein ( Byte 13, xxxx xxx1) |

<a id="job-status-digital-ll"></a>
### STATUS_DIGITAL_LL

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_B_FHZ | int | erh. LL durch Frontscheibenheizung (Byte 9, x1xx xxxx) |
| STAT_B_NSUB | int | erh. LL durch zu niedrige Bordspannung (Byte 9, xxxx 1xxx) |
| STAT_B_NFTEV | int | erh. LL durch TEV (Byte 9, xx1x xxxx) |
| STAT_B_NAC | int | erh. LL durch Klimaanlage (Byte 9, 1xxx xxxx) |
| STAT_B_DKPU | int | erh. LL durch falsche oder unbek. DK Stellung ( Byte 9, xxx1 xxxx) |

<a id="job-status-digital-abgas"></a>
### STATUS_DIGITAL_ABGAS

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_B_CDLSV | int | Lamdbasonde vor Kat ueber Codeword frei (Byte 6, xx1x xxxx) |
| STAT_B_CDAGR | int | Abgasrueckfuehrung ueber Codewort frei (Byte 6, 1xxx xxxx) |
| STAT_B_CDSLS | int | Sekundaerluftsystem ueber Codewort frei (Byte 6, xxxx 1xxx) |
| STAT_B_CDHSV | int | Codewort Sonderheizungsverzoegerung frei (Byte 6, x1xx xxxx) |
| STAT_B_CDTES | int | Codewort Tankentlueftungssystem frei ( Byte 6, xxxx x1xx) |

<a id="job-status-digital-check"></a>
### STATUS_DIGITAL_CHECK

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_B_HSRDY | int | Sonderheizung ready (Byte 7, x1xx xxxx) |
| STAT_B_TESRDY | int | Tankdnetlueftungssystem ready (Byte 7, xxxx x1xx) |
| STAT_B_SLSRDY | int | Sekundaerluftsystem ready (Byte 7, xxxx 1xxx) |
| STAT_B_LSRDY | int | Lambdasonden ready (Byte 7, xx1x xxxx) |
| STAT_B_KATRDY | int | Katalysatoren ready ( Byte 7, xxxx xxx1) |
| STAT_B_AGRRDY | int | Abgasrueckfuehrung ready ( Byte 7, 1xxx xxxx) |

<a id="job-status-digital-pkw"></a>
### STATUS_DIGITAL_PKW

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_B_ASC_PKW | int | ASC-Fzg. (Byte 7, xxxx 1xxx) |
| STAT_B_ACC | int | ACC (Byte 7, xxxx x1xx) |
| STAT_B_AUTGET | int | Automatik-Fzg. (Byte 7, xxxx xx1x) |
| STAT_B_NOKATFZG | int | Kat.-Vorbereitung (Byte 7, xxxx xxx1) |

<a id="job-aif-lesen"></a>
### AIF_LESEN

Auslesen des Anwender-Info-Feldes

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AIF_FG_NR | string | Fahrgestellnummer |
| AIF_DATUM | string | Fertigungsdatum |
| AIF_AENDERUNGS_INDEX | string | Aenderungsindex |
| AIF_SW_NR | long | Softwarenummer |
| AIF_BEHOERDEN_NR | long | Behoerdennummer |
| AIF_ZB_NR | long | Zusbaunummer |
| AIF_PROGG_NR | string | Programmiergeraet Seriennummer |
| AIF_WERKSCODE | string | Haendlernummer (Werkscode) |
| AIF_KM_STAND | long | km-Stand |
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |

<a id="job-ecu-config"></a>
### ECU_CONFIG

Ident-Daten fuer DME

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ASC_VORHANDEN | int | ASC vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| KAT_VORHANDEN | int | KAT vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| EGS_VORHANDEN | int | EGS vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| AC_VORHANDEN | int | Klimaanlage. vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| LDP_VORHANDEN | int | LDP vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| SLP_VORHANDEN | int | SLP vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| ELUEFTER_VORHANDEN | int | E-Luefter vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| MIL_VORHANDEN | int | MIL vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| SSP_VORHANDEN | int | Saug-Strahl-Pumpe vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| AKLAPPE_VORHANDEN | int | Abgasklappe vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |
| ANZAHL_ZYLINDER | int | Anzahl Zylinder |

<a id="job-abgas-variante-lesen"></a>
### ABGAS_VARIANTE_LESEN

Auslesen der Abgasvariante

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ABGAS_VARIANTE_WERT | int | Abgasvariante 0=KAT-V , 1= KAT |

<a id="job-status-geberrad-adaption"></a>
### STATUS_GEBERRAD_ADAPTION

Geberradadaption

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_GEBERRAD_ADAPTION_WERT | int | Motortemperatur Wert |
| STAT_GEBERRAD_ADAPTION_WERT | int | Motortemperatur Wert |
| STATUS_GEBERRAD_ADAPTION_EINH | string | Einheit inc |
| STAT_GEBERRAD_ADAPTION_EINH | string | Einheit inc |

<a id="job-fs-lesen"></a>
### FS_LESEN

Fehlerspeicher auslesen ueber RAM lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "POS_RESPONSE", wenn fehlerfrei |
| SGBD_NAME | string | Name der sgbd-Datei |
| F_ANZ_INT | int | Anzahl der eingetragenen Fehler |
| F_ANZ_NR | int | Anzahl der eingetragenen Fehler |
| F_ORT_NR | int | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_ART_ANZ | int | Anzahl der Fehlerarten des SG |
| F_ART1_NR | int | Index Fehlerart 1 |
| F_ART1_TEXT | string | Fehlerart 1 Text |
| F_ART2_NR | int | Index Fehlerart 2 |
| F_ART2_TEXT | string | Fehlerart 2 Text |
| F_ART3_NR | int | Index Fehlerart 3 |
| F_ART3_TEXT | string | Fehlerart 3 Text |
| F_ART4_NR | int | Index Fehlerart 4 |
| F_ART4_TEXT | string | Fehlerart 4 Text |
| F_ART5_NR | int | Index Fehlerart 5 |
| F_ART5_TEXT | string | Fehlerart 5 Text |
| F_ART6_NR | int | Index Fehlerart 6 |
| F_ART6_TEXT | string | Fehlerart 6 Text |
| F_ART7_NR | int | Index Fehlerart 7 |
| F_ART7_TEXT | string | Fehlerart 7 Text |
| F_ART8_NR | int | Index Fehlerart 8 |
| F_ART8_TEXT | string | Fehlerart 8 Text |
| F_ART9_NR | int | Index Fehlerart 9 |
| F_ART9_TEXT | string | Fehlerart 9 Text |
| F_ART10_NR | int | Index Fehlerart 10 |
| F_ART10_TEXT | string | Fehlerart 10 Text |
| F_ART11_NR | int | Index Fehlerart 11 |
| F_ART11_TEXT | string | Fehlerart 11 Text |
| F_ART12_NR | int | Index Fehlerart 12 |
| F_ART12_TEXT | string | Fehlerart 12 Text |
| F_ART13_NR | int | Index Fehlerart 13 |
| F_ART13_TEXT | string | Fehlerart 13 Text |
| F_ART14_NR | int | Index Fehlerart 14 |
| F_ART14_TEXT | string | Fehlerart 14 Text |
| F_ART15_NR | int | Index Fehlerart 15 |
| F_ART15_TEXT | string | Fehlerart 15 Text |
| F_ART16_NR | int | Index Fehlerart 16 |
| F_ART16_TEXT | string | Fehlerart 16 Text |
| F_ART17_NR | int | Index Fehlerart 17 |
| F_ART17_TEXT | string | Fehlerart 17 Text |
| F_ART18_NR | int | Index Fehlerart 18 |
| F_ART18_TEXT | string | Fehlerart 18 Text |
| F_ART19_NR | int | Index Fehlerart 19 |
| F_ART19_TEXT | string | Fehlerart 19 Text |
| F_ART20_NR | int | Index Fehlerart 20 |
| F_ART20_TEXT | string | Fehlerart 20 Text |
| F_ART21_NR | int | Index Fehlerart 21 |
| F_ART21_TEXT | string | Fehlerart 21 Text |
| F_ART22_NR | int | Index Fehlerart 22 |
| F_ART22_TEXT | string | Fehlerart 22 Text |
| F_ART23_NR | int | Index Fehlerart 23 |
| F_ART23_TEXT | string | Fehlerart 23 Text |
| F_ART24_NR | int | Index Fehlerart 24 |
| F_ART24_TEXT | string | Fehlerart 24 Text |
| F_CLA | int | Klasse |
| F_FLC | int | Wert Entprellvorgaenge FLC |
| F_HLC | int | Wert Entprellvorgaenge HLC |
| F_LZ | int | Wert Loeschvorgaenge DLC |
| F_TSF | real | Wert Schwerezaehler TSF |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_UW_SATZ | int | Anzahl der Umweltsaetze, Steuerung der Anzeige der Applikation |
| F_KM_FIRST | string | Km-Stand bei Erstauftreten |
| F_KM_NEXT | string | Km-Stand bei Erstauftreten |
| F_KM_LAST | string | Km-Stand bei Erstauftreten |
| F_UW1_NR | int | 1.Satz Umweltbedingung 1 Index (Ersterkennung) |
| F_UW1_TEXT | string | 1.Satz UW1 Text zur Umweltbedingung |
| F_UW1_WERT | real | 1.Satz UW1 Wert der Umweltbedingung |
| F_UW1_EINH | string | 1.Satz UW1 Einheit |
| F_UW2_NR | int | 1.Satz Umweltbedingung 2 Index (Ersterkennung) |
| F_UW2_TEXT | string | 1.Satz UW2 Text zur Umweltbedingung |
| F_UW2_WERT | real | 1.Satz UW2 Wert der Umweltbedingung |
| F_UW2_EINH | string | 1.Satz UW2 Einheit |
| F_UW3_NR | int | 1.Satz Umweltbedingung 3 Index (Ersterkennung) |
| F_UW3_TEXT | string | 1.Satz UW3 Text zur Umweltbedingung |
| F_UW3_WERT | real | 1.Satz UW3 Wert der Umweltbedingung |
| F_UW3_EINH | string | 1.Satz UW3 Einheit |
| F_UW4_NR | int | 1.Satz Umweltbedingung 4 Index (Ersterkennung) |
| F_UW4_TEXT | string | 1.Satz UW4 Text zur Umweltbedingung |
| F_UW4_WERT | real | 1.Satz UW4 Wert der Umweltbedingung |
| F_UW4_EINH | string | 1.Satz UW4 Einheit |
| F_UW5_NR | int | 2.Satz Umweltbedingung 1 Index (zweite Erkennung) |
| F_UW5_TEXT | string | 2.Satz UW1 Text zur Umweltbedingung |
| F_UW5_WERT | real | 2.Satz UW1 Wert der Umweltbedingung |
| F_UW5_EINH | string | 2.Satz UW1 Einheit |
| F_UW6_NR | int | 2.Satz Umweltbedingung 2 Index (zweite Erkennung) |
| F_UW6_TEXT | string | 2.Satz UW2 Text zur Umweltbedingung |
| F_UW6_WERT | real | 2.Satz UW2 Wert der Umweltbedingung |
| F_UW6_EINH | string | 2.Satz UW2 Einheit |
| F_UW7_NR | int | 2.Satz Umweltbedingung 3 Index (zweite Erkennung) |
| F_UW7_TEXT | string | 2.Satz UW3 Text zur Umweltbedingung |
| F_UW7_WERT | real | 2.Satz UW3 Wert der Umweltbedingung |
| F_UW7_EINH | string | 2.Satz UW3 Einheit |
| F_UW8_NR | int | 2.Satz Umweltbedingung 4 Index (zweite Erkennung) |
| F_UW8_TEXT | string | 2.Satz UW4 Text zur Umweltbedingung |
| F_UW8_WERT | real | 2.Satz UW4 Wert der Umweltbedingung |
| F_UW8_EINH | string | 2.Satz UW4 Einheit |
| F_UW9_NR | int | 3.Satz Umweltbedingung 1 Index (aktuelle Erkennung) |
| F_UW9_TEXT | string | 3.Satz UW1 Text zur Umweltbedingung |
| F_UW9_WERT | real | 3.Satz UW1 Wert der Umweltbedingung |
| F_UW9_EINH | string | 3.Satz UW1 Einheit |
| F_UW10_NR | int | 3.Satz Umweltbedingung 2 Index (aktuelle Erkennung) |
| F_UW10_TEXT | string | 3.Satz UW2 Text zur Umweltbedingung |
| F_UW10_WERT | real | 3.Satz UW2 Wert der Umweltbedingung |
| F_UW10_EINH | string | 3.Satz UW2 Einheit |
| F_UW11_NR | int | 3.Satz Umweltbedingung 3 Index (aktuelle Erkennung) |
| F_UW11_TEXT | string | 3.Satz UW3 Text zur Umweltbedingung |
| F_UW11_WERT | real | 3.Satz UW3 Wert der Umweltbedingung |
| F_UW11_EINH | string | 3.Satz UW3 Einheit |
| F_UW12_NR | int | 3.Satz Umweltbedingung 4 Index (aktuelle Erkennung) |
| F_UW12_TEXT | string | 3.Satz UW4 Text zur Umweltbedingung |
| F_UW12_WERT | real | 3.Satz UW4 Wert der Umweltbedingung |
| F_UW12_EINH | string | 3.Satz UW4 Einheit |
| F_FF1_TEXT | string | Freeze Frame Umweltbedingung 1 |
| F_FF1_BESCH | string | Freeze Frame Umweltbedingung 1 Beschreibung |
| F_FF2_TEXT | string | Freeze Frame Umweltbedingung 2 Text |
| F_FF2_BESCH | string | Freeze Frame Umweltbedingung 2 Beschreibung |
| F_FF3_TEXT | string | Freeze Frame Umweltbedingung 3 Text |
| F_FF3_EINH | string | Freeze Frame Umweltbedingung 3 Einheit |
| F_FF3_WERT | real | Freeze Frame Umweltbedingung 3 Wert |
| F_FF4_TEXT | string | Freeze Frame Umweltbedingung 4 Text |
| F_FF4_EINH | string | Freeze Frame Umweltbedingung 4 EINH |
| F_FF4_WERT | real | Freeze Frame Umweltbedingung 4  Wert |
| F_FF5_TEXT | string | Freeze Frame Umweltbedingung 5 Text |
| F_FF5_EINH | string | Freeze Frame Umweltbedingung 5 EINH |
| F_FF5_WERT | real | Freeze Frame Umweltbedingung 5  Wert |
| F_FF6_TEXT | string | Freeze Frame Umweltbedingung 6 Text |
| F_FF6_EINH | string | Freeze Frame Umweltbedingung 6 EINH |
| F_FF6_WERT | real | Freeze Frame Umweltbedingung 6  Wert |
| F_FF7_TEXT | string | Freeze Frame Umweltbedingung 7 Text |
| F_FF7_EINH | string | Freeze Frame Umweltbedingung 7 EINH |
| F_FF7_WERT | real | Freeze Frame Umweltbedingung 7  Wert |
| F_FF8_TEXT | string | Freeze Frame Umweltbedingung 8 Text |
| F_FF8_EINH | string | Freeze Frame Umweltbedingung 8 EINH |
| F_FF8_WERT | real | Freeze Frame Umweltbedingung 8  Wert |
| F_FF9_TEXT | string | Freeze Frame Umweltbedingung 9 Text |
| F_FF9_EINH | string | Freeze Frame Umweltbedingung 9 EINH |
| F_FF9_WERT | real | Freeze Frame Umweltbedingung 9  Wert |
| F_FF10_TEXT | string | Freeze Frame Umweltbedingung 10 Text |
| F_FF10_EINH | string | Freeze Frame Umweltbedingung 10 EINH |
| F_FF10_WERT | real | Freeze Frame Umweltbedingung 10  Wert |
| F_FF11_TEXT | string | Freeze Frame Umweltbedingung 11 Text |
| F_FF11_EINH | string | Freeze Frame Umweltbedingung 11 EINH |
| F_FF11_WERT | real | Freeze Frame Umweltbedingung 11  Wert |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| RESP_CODE | string | Code bei NEG_RESPONSE |

<a id="job-status-digital-test"></a>
### STATUS_DIGITAL_TEST

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_REEDSWITCH_EIN | int | 0=Nein / 1=Ja |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KO_EIN | int | Klima-Anforderung 0=Nein / 1=Ja |
| STAT_AC_EIN | int | Anforderung Klimabereitschaft 0=Nein / 1=Ja |
| STATUS_KO_EIN | int | Klima-Anforderung 0=Nein / 1=Ja |
| STATUS_AC_EIN | int | Anforderung Klimabereitschaft 0=Nein / 1=Ja |
| STAT_FGR_EIN | int | FGR Bereitschaft (main switch) |
| STAT_FGRTVE_EIN | int | MFL Taste Verzoegern 0=Nein / 1=Ja |
| STAT_FGRHSA_EIN | int | MFL Taste Mainswitch aus 0=Nein / 1=Ja |
| STAT_FGRTSE_EIN | int | MFL Taste Setzen Beschleunigen 0=Nein / 1=Ja |
| STAT_FGRAT_EIN | int | MFL Taste Aus 0=Nein / 1=Ja |
| STAT_FGRTWA_EIN | int | MFL Taste Wiederaufnahme 0=Nein / 1=Ja |
| STAT_FGRTBE_EIN | int | FGR Bereitsanzeige 0=Nein / 1=Ja |
| STAT_KUP_EIN | int | Schalter Kupplung aktiv 0=Nein / 1=Ja |
| STAT_BLS_EIN | int | Schalter BLS aktiv 0=Nein / 1=Ja |
| STAT_BRS_EIN | int | Bremslichttestschalter aktiv 0=Nein / 1=Ja |
| STAT_BLTS_EIN | int | Schalter BLTS aktiv 0=Nein / 1=Ja |
| STAT_LL_EIN | int | Leerlauf 0=Nein / 1=Ja |
| STAT_KL15_EIN | int | Kl. 15 0=Nein / 1=Ja |
| STAT_SLP_EIN | int | Sekundaerluftpumpe 0=Nein / 1=Ja |
| STAT_STA_EIN | int | Start 0=Nein / 1=Ja |
| STAT_EBL_EIN | int | E-Box Luefter 0=Nein / 1=Ja |
| STAT_KOE_EIN | int | Kompressoreinschalter 0=Nein / 1=Ja |
| STAT_EKP_EIN | int | Elektrokraftstoffpumpe 0=Nein / 1=Ja |
| STAT_SLV_EIN | int | Sekundaerluftventil 0=Nein / 1=Ja |
| STAT_ETR_EIN | int | elektronische Thermostatregelung 0=Nein / 1=Ja |
| STAT_AKR_EIN | int | Abgasrueckfuehrung 0=Nein / 1=Ja |
| STAT_HSHE2_EIN | int | Sonderheizung 2 hinter Kat angesteuert 0=Nein / 1=Ja |
| STAT_HSVE_EIN | int | Lambdasondenheizung 1 vor Kat 0=Nein / 1=Ja |
| STAT_HSVE2_EIN | int | Lambdasondenheizung 2 vor Kat 0=Nein / 1=Ja |
| STAT_HSHE_EIN | int | Lambdasondenheizung 1 hinter Kat 0=Nein / 1=Ja |
| STAT_VL_EIN | int | Beschleunigungsanreicherung 0=Aus / 1=Ein |
| STATUS_LL_EIN | int | Leerlauf 0=Nein / 1=Ja |
| STAT_UMAERF_EIN | int | unt. mech. DK-Anschlag erfolgreich gelernt 0=Nein / 1=Ja |
| STAT_EWS_EIN | int | EWS in Ordnung 0=Nein / 1=Ja |
| STAT_LR_EIN | int | Leerlaufregler 1 0=Nein / 1=Ja |
| STAT_LR2_EIN | int | Leerlaufregler 2 0=Nein / 1=Ja |
| STAT_SBBHK_EIN | int | Sonde betriebsbereit hinter Kat 0=Nein / 1=Ja |
| STAT_SBBVK2_EIN | int | Sonde betriebsbereit vor Kat 2 0=Nein / 1=Ja |
| STAT_SBBVK_EIN | int | Sonde betriebsbereit vor Kat 0=Nein / 1=Ja |
| STAT_SBBHK2_EIN | int | Sonde betriebsbereit hinter Kat 2 0=Nein / 1=Ja |
| STAT_FHZ_EIN | int | erh. LL durch Frontscheibenheizung 0=Nein / 1=Ja |
| STAT_NSUB_EIN | int | erh. LL durch zu niedrige Bordspg. 0=Nein / 1=Ja |
| STAT_NFTEV_EIN | int | erh. LL durch TEV 0=Nein / 1=Ja |
| STAT_NAC_EIN | int | erh. LL durch Klimaanlage 0=Nein / 1=Ja |
| STAT_LDPR_EIN | int | Schalter Leckdiagnosepumpenrelais 0=Nein / 1=Ja |
| STAT_LDPEIN_EIN | int | LDP ein 0=Nein / 1=Ja |
| STAT_DKPU_EIN | int | erh. LL durch falsche oder unbek. DK Stellung 0=Nein / 1=Ja |
| STAT_CDLSV_EIN | int | Lambdasonde vor Kat ueber Codeword frei 0=Nein / 1=Ja |
| STAT_CDAGR_EIN | int | Abgasrueckfuehrung ueber Codewort frei 0=Nein / 1=Ja |
| STAT_CDSLS_EIN | int | Sekundaerluftsystem ueber Codewort frei 0=Nein / 1=Ja |
| STAT_CDHSV_EIN | int | Codewort Sonderheizungsverzoegerung frei 0=Nein / 1=Ja |
| STAT_CDTES_EIN | int | Codewort Tankentlueftungssystem frei 0=Nein / 1=Ja |
| STAT_HSRDY_EIN | int | Sonderheizung ready 0=Nein / 1=Ja |
| STAT_TESRDY_EIN | int | Tankentlueftungssystem ready 0=Nein / 1=Ja |
| STAT_SLSRDY_EIN | int | Sekundaerluftsystem ready 0=Nein / 1=Ja |
| STAT_LSRDY_EIN | int | Lambdasondem ready 0=Nein / 1=Ja |
| STAT_KATRDY_EIN | int | Katalysatoren ready 0=Nein / 1=Ja |
| STAT_AGRRDY_EIN | int | Abgasrueckfuehrung ready 0=Nein / 1=Ja |
| STAT_NOKATFZG_EIN | int | Kat-Vorbereitung 0=Nein / 1=Ja |
| STAT_ACC_EIN | int | ACC 0=Nein / 1=Ja |
| STAT_ASC_PKW_EIN | int | ASC-Fzg. 0=Nein / 1=Ja |
| STAT_AUTGET_EIN | int | Automatik-Fzg. 0=Nein / 1=Ja |
| STAT_REEDSWITCH_EIN | int | 0=Nein / 1=Ja |
| STATUS_VL_EIN | int | Beschleunigungsanreicherung 0=Aus / 1=Ein |

<a id="job-status-solldrehzahl"></a>
### STATUS_SOLLDREHZAHL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| STAT_DNLLMV | long | Abgleichwert DNLLMV |
| STAT_DNFSACMV | long | Abgleichwert DNFSACMV |
| STAT_DNSLBV | long | Abgleichwert DNSLBV |
| STAT_DNSACMV | long | Abgleichwert DNFSACMV |
| STAT_DNFSMV | long | Abgleichwert DNFSMV |

<a id="job-status-dk-lrnstep"></a>
### STATUS_DK_LRNSTEP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| STAT_DK_WERT | int | Adaptionswert DK-Lernen auslesen |
| STAT_DK_LRNSTEP | int | Logischer Adaptionswert DK-Lernen (0&lt;9 1&gt;9) |

<a id="job-status-vanos"></a>
### STATUS_VANOS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| STAT_NWSDSTAT | unsigned int | Status Vanos1-Dichtheit |
| STAT_NWSDSTAT2 | unsigned int | Status Vanos2-Dichtheit |
| STAT_NWSSTAT | unsigned int | Status Verstellzeitpruefung Vanos1 |
| STAT_NWSSTAT2 | unsigned int | Status Verstellzeitpruefung Vanos2 |
| STAT_TNWSFI | real | Vanos Fruehverstellzeit NW1 |
| STAT_TNWSFI2 | real | Vanos Fruehverstellzeit NW2 |
| STAT_TNWSSI | real | Vanos Spaetverstellzeit NW1 |
| STAT_TNWSSI2 | real | Vanos Spaetverstellzeit NW2 |
| STAT_WNWI_W0 | real | Istwinkel fuer Vanos 1 |
| STAT_WNWI_W1 | real | Istwinkel fuer Vanos 2 |

<a id="job-sg-adressen"></a>
### SG_ADRESSEN

Steuergeaetespezifische Adressen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| UPROG | string | Programmierspannung |
| DP_1 | string | Datenpointer 1 |
| DP_2 | string | Datenpointer 2 |
| DP_3 | string | Datenpointer 3 |
| DP_4 | string | Datenpointer 4 |
| DP_5 | string | Datenpointer 5 |
| DP_6 | string | Datenpointer 6 |
| DP_7 | string | Datenpointer 7 |
| DP_8 | string | Datenpointer 8 |
| DP_9 | string | Datenpointer 9 |
| DP_10 | string | Datenpointer 10 |
| DP_11 | string | Datenpointer 11 |
| DP_12 | string | Datenpointer 12 |
| DSK | string | Datensatzkennung |
| WCODE | string | Werkstattcode |
| DATEN_REF | string | Datenreferenz |
| ZIF_BACK | string | ZIF-Backup |
| LOESCHZEIT | string | Loeschzeit |
| HW_REF | string | Hardwarereferenz |
| PRG_REF | string | Programmreferenz |
| AW_INFO | string | Anwenderinfo |
| BL_LAENGE | string | max.Blocklaenge Nutzdaten |
| DATUM | string | Hersteller Fertigungsdatum |
| BAUDRATE | string | Baudratentabelle |
| HEX_STRING1 | string | die Haelfte des HexStrings |
| HEX_STRING2 | string | die andere Haelfte des HexStrings |
| RESP_CODE | string | Code bei NEG_RESPONSE |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Diagnose beenden

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-stop"></a>
### DIAGNOSE_STOP

Diagnose beenden mit KWP-Befehl COM_STOP

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-sync-mode"></a>
### STEUERN_SYNC_MODE

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| MODE | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STEUERN_SYNC_MODE_STATUS | int | Statusflag |
| STEUERN_SYNC_MODE_TEXT | string | Statustext |

<a id="job-wechselcode-sync-dme"></a>
### WECHSELCODE_SYNC_DME

Wechselcodesynchronisation EWS 3 - DME anstossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, ERROR_.. |
| _TEL_ANTWORT | binary |  |

<a id="job-status-sync-mode"></a>
### STATUS_SYNC_MODE

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_SYNC_MODE_STATUS | int | Statusflag |
| STATUS_SYNC_MODE_TEXT | string | Statustext |

<a id="job-fs-lesen-status"></a>
### FS_LESEN_STATUS

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_CODEHEX | binary | alle Fehlerbyte |

<a id="job-fs-lesen-kwp"></a>
### FS_LESEN_KWP

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_ORT_NR | int | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_LZ | int | Fehlerlogistikzaehler |
| F_ART_ANZ | int | Anzahl der Fehlerarten des SG |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_ART1_NR | int | Fehlerart 1 Index |
| F_ART1_TEXT | string | Fehlerart 1 Text |
| F_ART2_NR | int | Fehlerart 2 Index |
| F_ART2_TEXT | string | Fehlerart 2 Text |
| F_ART3_NR | int | Fehlerart 3 Index |
| F_ART3_TEXT | string | Fehlerart 3 Text |
| F_ART4_NR | int | Fehlerart 4 Index |
| F_ART4_TEXT | string | Fehlerart 4 Text |
| F_ART5_NR | int | Fehlerart 5 Index |
| F_ART5_TEXT | string | Fehlerart 5 Text |
| F_ART6_NR | int | Fehlerart 6 Index |
| F_ART6_TEXT | string | Fehlerart 6 Text |
| F_ART7_NR | int | Fehlerart 7 Index |
| F_ART7_TEXT | string | Fehlerart 7 Text |
| F_ART8_NR | int | Fehlerart 8 Index |
| F_ART8_TEXT | string | Fehlerart 8  Text |
| F_UW1_NR | int | Umweltbedingung 1 Index |
| F_UW1_TEXT | string | Umweltbedingung 1 Einheit |
| F_UW1_EINH | string | Umweltbedingung 1 Text |
| F_UW1_WERT | real | Umweltbedingung 1 Wert |
| F_UW2_NR | int | Umweltbedingung 2 Index |
| F_UW2_TEXT | string | Umweltbedingung 2 Text |
| F_UW2_EINH | string | Umweltbedingung 2 Einheit |
| F_UW2_WERT | real | Umweltbedingung 2 Wert |
| F_UW3_NR | int | Umweltbedingung 3 Index |
| F_UW3_TEXT | string | Umweltbedingung 3 Text |
| F_UW3_EINH | string | Umweltbedingung 3 Einheit |
| F_UW3_WERT | real | Umweltbedingung 3 Wert |
| F_UW4_NR | int | Umweltbedingung 4 Index |
| F_UW4_TEXT | string | Umweltbedingung 4 Text |
| F_UW4_EINH | string | Umweltbedingung 4 EINH |
| F_UW4_WERT | real | Umweltbedingung 4  Wert |
| F_UW5_NR | int | Umweltbedingung 5 Index |
| F_UW5_TEXT | string | Umweltbedingung 5 Text |
| F_UW5_EINH | string | Umweltbedingung 5 EINH |
| F_UW5_WERT | real | Umweltbedingung 5  Wert |
| F_UW6_NR | int | Umweltbedingung 6 Index |
| F_UW6_TEXT | string | Umweltbedingung 6 Text |
| F_UW6_EINH | string | Umweltbedingung 6 EINH |
| F_UW6_WERT | real | Umweltbedingung 6  Wert |
| F_UW7_NR | int | Umweltbedingung 7 Index |
| F_UW7_TEXT | string | Umweltbedingung 7 Text |
| F_UW7_EINH | string | Umweltbedingung 7 EINH |
| F_UW7_WERT | real | Umweltbedingung 7  Wert |
| F_UW8_NR | int | Umweltbedingung 8 Index |
| F_UW8_TEXT | string | Umweltbedingung 8 Text |
| F_UW8_EINH | string | Umweltbedingung 8 EINH |
| F_UW8_WERT | real | Umweltbedingung 8  Wert |
| F_UW9_NR | int | Umweltbedingung 9 Index |
| F_UW9_TEXT | string | Umweltbedingung 9 Text |
| F_UW9_EINH | string | Umweltbedingung 9 EINH |
| F_UW9_WERT | real | Umweltbedingung 9  Wert |
| F_UW10_NR | int | Umweltbedingung 10 Index |
| F_UW10_TEXT | string | Umweltbedingung 10 Text |
| F_UW10_EINH | string | Umweltbedingung 10 EINH |
| F_UW10_WERT | real | Umweltbedingung 10  Wert |
| F_UW11_NR | int | Umweltbedingung 11 Index |
| F_UW11_TEXT | string | Umweltbedingung 11 Text |
| F_UW11_EINH | string | Umweltbedingung 11 EINH |
| F_UW11_WERT | real | Umweltbedingung 11  Wert |
| F_UW12_NR | int | Umweltbedingung 12 Index |
| F_UW12_TEXT | string | Umweltbedingung 12 Text |
| F_UW12_EINH | string | Umweltbedingung 12 EINH |
| F_UW12_WERT | real | Umweltbedingung 12  Wert |
| F_UW13_NR | int | Umweltbedingung 13 Index |
| F_UW13_TEXT | string | Umweltbedingung 13 Text |
| F_UW13_EINH | string | Umweltbedingung 13 EINH |
| F_UW13_WERT | real | Umweltbedingung 13  Wert |
| F_UW14_NR | int | Umweltbedingung 14 Index |
| F_UW14_TEXT | string | Umweltbedingung 14 Text |
| F_UW14_EINH | string | Umweltbedingung 14 EINH |
| F_UW14_WERT | real | Umweltbedingung 14  Wert |
| F_UW15_NR | int | Umweltbedingung 15 Index |
| F_UW15_TEXT | string | Umweltbedingung 15 Text |
| F_UW15_EINH | string | Umweltbedingung 15 EINH |
| F_UW15_WERT | real | Umweltbedingung 15  Wert |
| F_CODEHEX | binary | Hexdump des Fehlersatzes |
| F_HEX_CODE | binary | Hexdump des Fehlersatzes |
| F_UW_SATZ | int | Anzahl der Umweltsaetze , Steuerung der Anzeige in der Applikation |

<a id="job-steuern-ll-drehzahl-verstellen"></a>
### STEUERN_LL_DREHZAHL_VERSTELLEN

LL-Drehzahl verstellen,  512-2550 U/min

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | real | Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-steuern-vanos-verstellzeit"></a>
### STEUERN_VANOS_VERSTELLZEIT

Verstellzeitmessung VANOS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POS1 | real | Vanos Sollwert max 40 Grad KW |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-verstellzeit-mess-vanos"></a>
### STATUS_VERSTELLZEIT_MESS_VANOS

Verstellzeitmessung Nockenwelle Einlass

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_VERSTELLZEIT_MESS_VANOS_STAT_1 | int | Status |
| STAT_VERSTELLZEIT_MESS_VANOS_STAT_2 | int | Status |
| STAT_VERSTELLZEIT_MESS_VANOS_FRUEH_1_WERT | real | Ergebnis |
| STAT_VERSTELLZEIT_MESS_VANOS_FRUEH_2_WERT | real | Ergebnis |
| STAT_VERSTELLZEIT_MESS_VANOS_SPAET_1_WERT | real | Ergebnis |
| STAT_VERSTELLZEIT_MESS_VANOS_SPAET_2_WERT | real | Ergebnis |
| STAT_VERSTELLZEIT_MESS_VANOS_EINH | string | Einheit |

<a id="job-steuern-vanos-dichtheit"></a>
### STEUERN_VANOS_DICHTHEIT

Dichtheitsmessung VANOS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-vanos-test-stop"></a>
### STEUERN_VANOS_TEST_STOP

Dichtheitsmessung VANOS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-dichtheit-mess-vanos"></a>
### STATUS_DICHTHEIT_MESS_VANOS

DICHTHEITmessung Nockenwelle Einlass

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_DICHTHEIT_MESS_VANOS_STAT_1 | int | Status |
| STAT_DICHTHEIT_MESS_VANOS_STAT_2 | int | Status |
| STAT_DICHTHEIT_MESS_VANOS_1_WERT | real | Ergebnis |
| STAT_DICHTHEIT_MESS_VANOS_2_WERT | real | Ergebnis Status |
| STAT_DICHTHEIT_MESS_VANOS_1_DELTA_WERT | real | Ergebnis |
| STAT_DICHTHEIT_MESS_VANOS_1_MIN_WERT | real | Ergebnis |
| STAT_DICHTHEIT_MESS_VANOS_1_MAX_WERT | real | Ergebnis |
| STAT_DICHTHEIT_MESS_VANOS_2_DELTA_WERT | real | Ergebnis |
| STAT_DICHTHEIT_MESS_VANOS_2_MIN_WERT | real | Ergebnis |
| STAT_DICHTHEIT_MESS_VANOS_2_MAX_WERT | real | Ergebnis |
| STAT_DICHTHEIT_MESS_VANOS_EINH | string | Einheit |

<a id="job-status-systemcheck-laufunruhe"></a>
### STATUS_SYSTEMCHECK_LAUFUNRUHE

Laufunruhe lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL1_WERT | real |  |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL2_WERT | real |  |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL3_WERT | real |  |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL4_WERT | real |  |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL5_WERT | real |  |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL6_WERT | real |  |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL7_WERT | real |  |
| STAT_SYSTEMCHECK_LAUFUNRUHE_ZYL8_WERT | real |  |

<a id="job-lesen-systemcheck-laufunruhe"></a>
### LESEN_SYSTEMCHECK_LAUFUNRUHE

Laufunruhe lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| LESEN_SYSTEMCHECK_LAUFUNRUHE_ZYL1_WERT | int |  |
| LESEN_SYSTEMCHECK_LAUFUNRUHE_ZYL2_WERT | int |  |
| LESEN_SYSTEMCHECK_LAUFUNRUHE_ZYL3_WERT | int |  |
| LESEN_SYSTEMCHECK_LAUFUNRUHE_ZYL4_WERT | int |  |
| LESEN_SYSTEMCHECK_LAUFUNRUHE_ZYL5_WERT | int |  |
| LESEN_SYSTEMCHECK_LAUFUNRUHE_ZYL6_WERT | int |  |
| LESEN_SYSTEMCHECK_LAUFUNRUHE_ZYL7_WERT | int |  |
| LESEN_SYSTEMCHECK_LAUFUNRUHE_ZYL8_WERT | int |  |

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

EKP ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-1"></a>
### STEUERN_EV_1

EV  1 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-2"></a>
### STEUERN_EV_2

EV  2 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-3"></a>
### STEUERN_EV_3

EV 3 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-4"></a>
### STEUERN_EV_4

EV 4 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-5"></a>
### STEUERN_EV_5

EV  5 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-6"></a>
### STEUERN_EV_6

EV  6 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-7"></a>
### STEUERN_EV_7

EV  6 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev-8"></a>
### STEUERN_EV_8

EV  6 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

E-Luefter verstellen , Bereich 0-100%

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-steuern-e-luefter-ecos"></a>
### STEUERN_E_LUEFTER_ECOS

E-Luefter verstellen , Bereich 0-100%

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-steuern-ebox-luefter"></a>
### STEUERN_EBOX_LUEFTER

E-Box Luefter verstellen 0 oder 1

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TASTVERHAELTNIS | int | Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-status-s-evan-s"></a>
### STATUS_S_EVAN_S

Nockenwinkel Sollwert  auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_S_EVAN_S_WERT | real | Ergebnis |
| STAT_S_EVAN_S_EINH | string | Einheit |

<a id="job-status-nw-b1-fl1"></a>
### STATUS_NW_B1_FL1

Adaptionswinkel NW-B1 Flanke 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_NW_B1_FL1_WERT | real | Ergebnis |
| STAT_NW_B1_FL1_EINH | string | Einheit |

<a id="job-status-nw-b1-fl2"></a>
### STATUS_NW_B1_FL2

Adaptionswinkel NW-B1 Flanke 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_NW_B1_FL2_WERT | real | Ergebnis |
| STAT_NW_B1_FL2_EINH | string | Einheit |

<a id="job-status-nw-b1-fl3"></a>
### STATUS_NW_B1_FL3

Adaptionswinkel NW-B1 Flanke 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_NW_B1_FL3_WERT | real | Ergebnis |
| STAT_NW_B1_FL3_EINH | string | Einheit |

<a id="job-status-nw-b1-fl4"></a>
### STATUS_NW_B1_FL4

Adaptionswinkel NW-B1 Flanke 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_NW_B1_FL4_WERT | real | Ergebnis |
| STAT_NW_B1_FL4_EINH | string | Einheit |

<a id="job-status-nw-b2-fl1"></a>
### STATUS_NW_B2_FL1

Adaptionswinkel NW-B1 Flanke 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_NW_B2_FL1_WERT | real | Ergebnis |
| STAT_NW_B2_FL1_EINH | string | Einheit |

<a id="job-status-nw-b2-fl2"></a>
### STATUS_NW_B2_FL2

Adaptionswinkel NW-B1 Flanke 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_NW_B2_FL2_WERT | real | Ergebnis |
| STAT_NW_B2_FL2_EINH | string | Einheit |

<a id="job-status-nw-b2-fl3"></a>
### STATUS_NW_B2_FL3

Adaptionswinkel NW-B2 Flanke 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_NW_B2_FL3_WERT | real | Ergebnis |
| STAT_NW_B2_FL3_EINH | string | Einheit |

<a id="job-status-nw-b2-fl4"></a>
### STATUS_NW_B2_FL4

Adaptionswinkel NW-B2 Flanke 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_NW_B2_FL4_WERT | real | Ergebnis |
| STAT_NW_B2_FL4_EINH | string | Einheit |

<a id="job-status-einspritzzeit"></a>
### STATUS_EINSPRITZZEIT

Einspritzzeit EV1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EINSPRITZZEIT_WERT | real | Ergebnis |
| STAT_EINSPRITZZEIT_EINH | string | Einheit |

<a id="job-status-lambda-integrator-1"></a>
### STATUS_LAMBDA_INTEGRATOR_1

Lambdaregler1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAMBDA_INTEGRATOR_1_WERT | real | Ergebnis |
| STAT_LAMBDA_INTEGRATOR_1_EINH | string | Einheit |

<a id="job-status-int"></a>
### STATUS_INT

Lambdaregler1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_INT_WERT | real | Ergebnis |
| STAT_INT_WERT | real | Ergebnis |
| STATUS_INT_EINH | string | Einheit |
| STAT_INT_EINH | string | Einheit |

<a id="job-status-lambda-integrator-2"></a>
### STATUS_LAMBDA_INTEGRATOR_2

Lambdaregler2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAMBDA_INTEGRATOR_2_WERT | real | Ergebnis |
| STAT_LAMBDA_INTEGRATOR_2_EINH | string | Einheit |

<a id="job-status-int-2"></a>
### STATUS_INT_2

Lambdaregler2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_INT_2_WERT | real | Ergebnis |
| STAT_INT_2_WERT | real | Ergebnis |
| STATUS_INT_2_EINH | string | Einheit |
| STAT_INT_2_EINH | string | Einheit |

<a id="job-status-geschwindigkeit"></a>
### STATUS_GESCHWINDIGKEIT

Fahrzeuggeschwindigkeit

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_GESCHWINDIGKEIT_WERT | real | Ergebnis |
| STAT_GESCHWINDIGKEIT_EINH | string | Einheit |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Motordrehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_MOTORDREHZAHL_WERT | real | Ergebnis |
| STAT_MOTORDREHZAHL_WERT | real | Ergebnis |
| STAT_MOTORDREHZAHL_EINH | string | Einheit |

<a id="job-status-motordrehzahl-soll"></a>
### STATUS_MOTORDREHZAHL_SOLL

LL-Solldrehzahl

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MOTORDREHZAHL_SOLL_WERT | real | Ergebnis |
| STAT_MOTORDREHZAHL_WERT | real | Ergebnis |
| STAT_MOTORDREHZAHL_SOLL_EINH | string | Einheit |

<a id="job-status-vanos-nw-lage-einlass-bank-1"></a>
### STATUS_VANOS_NW_LAGE_EINLASS_BANK_1

Nockenwellenposition Bank1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_VANOS_NW_LAGE_EINLASS_BANK_1_WERT | real | Ergebnis |
| STAT_VANOS_NW_LAGE_EINLASS_BANK_1_EINH | string | Einheit |

<a id="job-status-vanos-nw-lage-einlass-bank-2"></a>
### STATUS_VANOS_NW_LAGE_EINLASS_BANK_2

Nockenwellenposition Bank2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_VANOS_NW_LAGE_EINLASS_BANK_2_WERT | real | Ergebnis |
| STAT_VANOS_NW_LAGE_EINLASS_BANK_2_EINH | string | Einheit |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

Ansauglufttemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_AN_LUFTTEMPERATUR_WERT | real | Ergebnis |
| STATUS_AN_LUFTTEMPERATUR_WERT | real | Ergebnis |
| STAT_AN_LUFTTEMPERATUR_EINH | string | Einheit |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

Motortemperatur

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MOTORTEMPERATUR_WERT | real | Ergebnis |
| STATUS_MOTORTEMPERATUR_WERT | real | Ergebnis |
| STAT_MOTORTEMPERATUR_EINH | string | Einheit |

<a id="job-status-zuendwinkel"></a>
### STATUS_ZUENDWINKEL

Zuendwinkel Zyl1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ZUENDWINKEL_WERT | real | Ergebnis |
| STAT_ZUENDWINKEL_EINH | string | Einheit |

<a id="job-status-dkp-winkel"></a>
### STATUS_DKP_WINKEL

DK-Winkel

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DKP_WINKEL_WERT | real | Ergebnis |
| STAT_DKP_WINKEL_EINH | string | Einheit |

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

Luftmasse

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LMM_MASSE_WERT | real | Ergebnis |
| STAT_LMM_MASSE_EINH | string | Einheit |

<a id="job-status-lmm"></a>
### STATUS_LMM

Auslesen Luftmasse kg/h

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_LMM_WERT | real | Ergebnis Masse Luft |
| STAT_LMM_WERT | real | Ergebnis Masse Luft |
| STATUS_LMM_EINH | string | Einheit Masse Luft |
| STAT_LMM_EINH | string | Einheit Masse Luft |

<a id="job-status-miist"></a>
### STATUS_MIIST

MIIST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_MIIST_WERT | real | Ergebnis |
| STAT_MIIST_EINH | string | Einheit |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

Ubatt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_UBATT_WERT | real | Ergebnis |
| STATUS_UBATT_WERT | real | Ergebnis |
| STAT_UBATT_EINH | string | Einheit |

<a id="job-pruefstempel-lesen"></a>
### PRUEFSTEMPEL_LESEN

Auslesen des Pruefstempels

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |

<a id="job-pruefstempel-schreiben"></a>
### PRUEFSTEMPEL_SCHREIBEN

Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| BYTE1 | int | 0-255 bzw. 0x00-0xFF |
| BYTE2 | int | 0-255 bzw. 0x00-0xFF |
| BYTE3 | int | 0-255 bzw. 0x00-0xFF |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_ARGUMENT, wenn Argumente nicht uebergeben oder ausser Bereich |

<a id="job-status-pwg-poti-spannung"></a>
### STATUS_PWG_POTI_SPANNUNG

Fahrerwunsch

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PWG_POTI_SPANNUNG_1_WERT | real | Ergebnis |
| STAT_PWG_POTI_SPANNUNG_EINH | string | Einheit |
| STAT_ROHWERT1 | int | Ergebnis |
| STAT_ROHWERT2 | int | Ergebnis |

<a id="job-status-pwg-test"></a>
### STATUS_PWG_TEST

Fahrerwunsch

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PWG_TEST_1_WERT | real | Ergebnis |
| STAT_PWG_TEST_2_WERT | real | Ergebnis |
| STAT_PWG_TEST_3_WERT | real | Ergebnis |
| STAT_PWG_POTI_SPANNUNG_EINH | string | Einheit |

<a id="job-status-kuehlw-ausl-temperatur"></a>
### STATUS_KUEHLW_AUSL_TEMPERATUR

Temperatur Kuehleraustritt

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_KUEHLW_AUSL_TEMPERATUR_WERT | real | Ergebnis |
| STAT_KUEHLW_AUSL_TEMPERATUR_EINH | string | Einheit |

<a id="job-status-ldb-integrator"></a>
### STATUS_LDB_INTEGRATOR

Integrator Ladebilanz Batterie

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LDB_INTEGRATOR_WERT | real | Ergebnis |
| STAT_LDB_INTEGRATOR_EINH | string | Einheit |

<a id="job-status-ls-vkat-signal-1"></a>
### STATUS_LS_VKAT_SIGNAL_1

Lambdasondenspannung v Kat

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_VKAT_SIGNAL_1_WERT | real | Ergebnis |
| STAT_LS_VKAT_SIGNAL_1_EINH | string | Einheit |

<a id="job-status-l-sonde"></a>
### STATUS_L_SONDE

Lambdasondenspannung v Kat

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_L_SONDE_WERT | real | Ergebnis |
| STAT_L_SONDE_WERT | real | Ergebnis |
| STATUS_L_SONDE_EINH | string | Einheit |
| STAT_L_SONDE_EINH | string | Einheit |

<a id="job-status-ls-vkat-signal-2"></a>
### STATUS_LS_VKAT_SIGNAL_2

Lambdasondenspannung v Kat 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_VKAT_SIGNAL_2_WERT | real | Ergebnis |
| STAT_LS_VKAT_SIGNAL_2_EINH | string | Einheit |

<a id="job-status-l-sonde-2"></a>
### STATUS_L_SONDE_2

Lambdasondenspannung v Kat 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_L_SONDE_2_WERT | real | Ergebnis |
| STAT_L_SONDE_2_WERT | real | Ergebnis |
| STATUS_L_SONDE_2_EINH | string | Einheit |
| STAT_L_SONDE_2_EINH | string | Einheit |

<a id="job-status-ls-nkat-signal-1"></a>
### STATUS_LS_NKAT_SIGNAL_1

Lambdasondenspannung n Kat

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_NKAT_SIGNAL_1_WERT | real | Ergebnis |
| STAT_LS_NKAT_SIGNAL_1_EINH | string | Einheit |

<a id="job-status-l-sonde-h"></a>
### STATUS_L_SONDE_H

Lambdasondenspannung n Kat

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_L_SONDE_H_WERT | real | Ergebnis |
| STAT_L_SONDE_H_WERT | real | Ergebnis |
| STATUS_L_SONDE_H_EINH | string | Einheit |
| STAT_L_SONDE_H_EINH | string | Einheit |

<a id="job-status-ls-nkat-signal-2"></a>
### STATUS_LS_NKAT_SIGNAL_2

Lambdasondenspannung n Kat 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_NKAT_SIGNAL_2_WERT | real | Ergebnis |
| STAT_LS_NKAT_SIGNAL_2_EINH | string | Einheit |

<a id="job-status-l-sonde-2-h"></a>
### STATUS_L_SONDE_2_H

Lambdasondenspannung n Kat 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_L_SONDE_2_H_WERT | real | Ergebnis |
| STAT_L_SONDE_2_H_WERT | real | Ergebnis |
| STATUS_L_SONDE_2_H_EINH | string | Einheit |
| STAT_L_SONDE_2_H_EINH | string | Einheit |

<a id="job-status-lambda-add-1"></a>
### STATUS_LAMBDA_ADD_1

Gemischadaption additiv 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAMBDA_ADD_1_WERT | real | Ergebnis |
| STAT_LAMBDA_ADD_1_EINH | string | Einheit |

<a id="job-status-add"></a>
### STATUS_ADD

Gemischadaption additiv 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_ADD_WERT | real | Ergebnis |
| STAT_ADD_WERT | real | Ergebnis |
| STATUS_ADD_EINH | string | Einheit |
| STAT_ADD_EINH | string | Einheit |

<a id="job-status-lambda-add-2"></a>
### STATUS_LAMBDA_ADD_2

Gemischadaption additiv 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAMBDA_ADD_2_WERT | real | Ergebnis |
| STAT_LAMBDA_ADD_2_EINH | string | Einheit |

<a id="job-status-add-2"></a>
### STATUS_ADD_2

Gemischadaption additiv 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_ADD_2_WERT | real | Ergebnis |
| STAT_ADD_2_WERT | real | Ergebnis |
| STATUS_ADD_2_EINH | string | Einheit |
| STAT_ADD_2_EINH | string | Einheit |

<a id="job-status-lambda-mul-1"></a>
### STATUS_LAMBDA_MUL_1

Gemischadaption multipl. 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAMBDA_MUL_1_WERT | real | Ergebnis |
| STAT_LAMBDA_MUL_1_EINH | string | Einheit |

<a id="job-status-mul"></a>
### STATUS_MUL

Gemischadaption multipl. 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_MUL_WERT | real | Ergebnis |
| STAT_MUL_WERT | real | Ergebnis |
| STATUS_MUL_EINH | string | Einheit |
| STAT_MUL_EINH | string | Einheit |

<a id="job-status-lambda-mul-2"></a>
### STATUS_LAMBDA_MUL_2

Gemischadaption multipl. 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAMBDA_MUL_2_WERT | real | Ergebnis |
| STAT_LAMBDA_MUL_2_EINH | string | Einheit |

<a id="job-status-mul-2"></a>
### STATUS_MUL_2

Gemischadaption multipl. 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_MUL_2_WERT | real | Ergebnis |
| STAT_MUL_2_WERT | real | Ergebnis |
| STATUS_MUL_2_EINH | string | Einheit |
| STAT_MUL_2_EINH | string | Einheit |

<a id="job-status-ls-vkat-heizung-tv-1"></a>
### STATUS_LS_VKAT_HEIZUNG_TV_1

norm. Heizleist. L-Sonde vKat1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_VKAT_HEIZUNG_TV_1_WERT | real | Ergebnis |
| STAT_LS_VKAT_HEIZUNG_TV_1_EINH | string | Einheit |

<a id="job-status-ls-vkat-heizung-tv-2"></a>
### STATUS_LS_VKAT_HEIZUNG_TV_2

norm. Heizleist. L-Sonde vKat2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_VKAT_HEIZUNG_TV_2_WERT | real | Ergebnis |
| STAT_LS_VKAT_HEIZUNG_TV_2_EINH | string | Einheit |

<a id="job-status-ls-nkat-heizung-tv-1"></a>
### STATUS_LS_NKAT_HEIZUNG_TV_1

norm. Heizleist. L-Sonde hKat1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_NKAT_HEIZUNG_TV_1_WERT | real | Ergebnis |
| STAT_LS_NKAT_HEIZUNG_TV_1_EINH | string | Einheit |

<a id="job-status-ls-nkat-heizung-tv-2"></a>
### STATUS_LS_NKAT_HEIZUNG_TV_2

norm. Heizleist. L-Sonde hKat2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_NKAT_HEIZUNG_TV_2_WERT | real | Ergebnis |
| STAT_LS_NKAT_HEIZUNG_TV_2_EINH | string | Einheit |

<a id="job-status-ls-vkat-periodendauer-1"></a>
### STATUS_LS_VKAT_PERIODENDAUER_1

PeridenDauer L-Sonde v Kat1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_VKAT_PERIODENDAUER_1_WERT | real | Ergebnis |
| STAT_LS_VKAT_PERIODENDAUER_1_EINH | string | Einheit |

<a id="job-status-ls-vkat-periodendauer-2"></a>
### STATUS_LS_VKAT_PERIODENDAUER_2

PeridenDauer L-Sonde v Kat2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_VKAT_PERIODENDAUER_2_WERT | real | Ergebnis |
| STAT_LS_VKAT_PERIODENDAUER_2_EINH | string | Einheit |

<a id="job-status-te-tastverhaeltnis"></a>
### STATUS_TE_TASTVERHAELTNIS

Tastverhaeltnis TEV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TE_TASTVERHAELTNIS_WERT | real | Ergebnis |
| STAT_TE_TASTVERHAELTNIS_EINH | string | Einheit |

<a id="job-status-vanos-nw-lage-einlass-tv-1"></a>
### STATUS_VANOS_NW_LAGE_EINLASS_TV_1

Tastverhaeltnis Vanos 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_VANOS_NW_LAGE_EINLASS_TV_1_WERT | real | Ergebnis |
| STAT_VANOS_NW_LAGE_EINLASS_TV_1_EINH | string | Einheit |

<a id="job-status-vanos-nw-lage-einlass-tv-2"></a>
### STATUS_VANOS_NW_LAGE_EINLASS_TV_2

Tastverhaeltnis Vanos 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_VANOS_NW_LAGE_EINLASS_TV_2_WERT | real | Ergebnis |
| STAT_VANOS_NW_LAGE_EINLASS_TV_2_EINH | string | Einheit |

<a id="job-status-e-luefter-tv"></a>
### STATUS_E_LUEFTER_TV

Tastverhaeltnis E-Luefter

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_E_LUEFTER_TV_WERT | real | Ergebnis |
| STAT_E_LUEFTER_TV_EINH | string | Einheit |

<a id="job-status-lutsfi1"></a>
### STATUS_LUTSFI1

gefilterte Laufunruhen Zyl1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LUTSFI1_WERT | real | Ergebnis |
| STAT_LUTSFI1_EINH | string | Einheit |

<a id="job-status-lutsfi2"></a>
### STATUS_LUTSFI2

gefilterte Laufunruhen Zyl2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LUTSFI2_WERT | real | Ergebnis |
| STAT_LUTSFI2_EINH | string | Einheit |

<a id="job-status-lutsfi3"></a>
### STATUS_LUTSFI3

gefilterte Laufunruhen Zyl3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LUTSFI3_WERT | real | Ergebnis |
| STAT_LUTSFI3_EINH | string | Einheit |

<a id="job-status-lutsfi4"></a>
### STATUS_LUTSFI4

gefilterte Laufunruhen Zyl4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LUTSFI4_WERT | real | Ergebnis |
| STAT_LUTSFI4_EINH | string | Einheit |

<a id="job-status-lutsfi5"></a>
### STATUS_LUTSFI5

gefilterte Laufunruhen Zyl5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LUTSFI5_WERT | real | Ergebnis |
| STAT_LUTSFI5_EINH | string | Einheit |

<a id="job-status-lutsfi6"></a>
### STATUS_LUTSFI6

gefilterte Laufunruhen Zyl6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LUTSFI6_WERT | real | Ergebnis |
| STAT_LUTSFI6_EINH | string | Einheit |

<a id="job-status-lutsfi7"></a>
### STATUS_LUTSFI7

gefilterte Laufunruhen Zyl7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LUTSFI7_WERT | real | Ergebnis |
| STAT_LUTSFI7_EINH | string | Einheit |

<a id="job-status-lutsfi8"></a>
### STATUS_LUTSFI8

gefilterte Laufunruhen Zyl8

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LUTSFI8_WERT | real | Ergebnis |
| STAT_LUTSFI8_EINH | string | Einheit |

<a id="job-adapt-selektiv-loeschen"></a>
### ADAPT_SELEKTIV_LOESCHEN

Adaptionen selektiv loeschen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHLBYTE_1 | int | Auswahlbyte 1 |
| AUSWAHLBYTE_2 | int | Auswahlbyte 2 |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-adapt-loeschen"></a>
### ADAPT_LOESCHEN

Adaptionen selektiv loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-start-systemcheck-sek-luft"></a>
### START_SYSTEMCHECK_SEK_LUFT

Systemcheck  Sekundaerluft starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| START_SYSTEMCHECK_SEK_LUFT_STATUS | int |  |

<a id="job-stop-systemcheck-sek-luft"></a>
### STOP_SYSTEMCHECK_SEK_LUFT

Systemcheck  Sekundaerluft starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-start-systemcheck-tank-leck"></a>
### START_SYSTEMCHECK_TANK_LECK

Systemcheck Tankentlueftungssystem Leckdiagnose starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-start-systemcheck-dmtl"></a>
### START_SYSTEMCHECK_DMTL

Systemcheck Tankentlueftungssystem Leckdiagnose starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-start-systemcheck-dmtl-ecos"></a>
### START_SYSTEMCHECK_DMTL_ECOS

Systemcheck Tankentlueftungssystem Leckdiagnose starten

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_DMTL_ECOS | int |  |

<a id="job-lesen-systemcheck-sek-luft"></a>
### LESEN_SYSTEMCHECK_SEK_LUFT

Systemcheck  Sekundaerluft lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| LESEN_SYSTEMCHECK_SEK_LUFT_STATUS | unsigned int | Status |

<a id="job-lesen-systemcheck-sek-luft-1"></a>
### LESEN_SYSTEMCHECK_SEK_LUFT_1

Systemcheck  Sekundaerluft lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| LESEN_SYSTEMCHECK_SEK_LUFT_1_STATUS | unsigned int | Status |

<a id="job-lesen-systemcheck-tank-leck"></a>
### LESEN_SYSTEMCHECK_TANK_LECK

Systemcheck Tankentlueftungssystem Leckdiagnose lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| LESEN_SYSTEMCHECK_DMTL_STATUS | string | Status als Text |
| LESEN_SYSTEMCHECK_TANK_LECK_STATUS | int |  |
| LESEN_SYSTEMCHECK_TANK_LECK_PER_WERT | real | Periodendauer |
| LESEN_SYSTEMCHECK_TANK_LECK_AKTIV_WERT | real | Aktuelle Laufzeit |

<a id="job-lesen-systemcheck-dmtl"></a>
### LESEN_SYSTEMCHECK_DMTL

Systemcheck Tankentlueftungssystem Leckdiagnose lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| LESEN_SYSTEMCHECK_DMTL_TEXT | string | Status als Text |
| LESEN_SYSTEMCHECK_DMTL_STATUS | int |  |
| LESEN_SYSTEMCHECK_DMTL_WERT | real | Periodendauer |
| LESEN_SYSTEMCHECK_DMTL_AKTIV_WERT | real | Aktuelle Laufzeit |

<a id="job-status-dmtl-eol"></a>
### STATUS_DMTL_EOL

Systemcheck Tankentlueftungssystem Leckdiagnose lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_DMTL_EOL_WERT | int |  |

<a id="job-co-abgleich-lesen"></a>
### CO_ABGLEICH_LESEN

CO-Abgleich lesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_CO_ABGLEICH_WERT | char | Aktuellen Abgleichwert |
| STAT_CO_ABGLEICH_WERT | char | Aktuellen Abgleichwert |

<a id="job-co-abgleich-verstellen"></a>
### CO_ABGLEICH_VERSTELLEN

CO-Drehzahl  verstellen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| CO_ABGLEICH_VERSTELLEN_WERT | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-co-abgleich-programmieren"></a>
### CO_ABGLEICH_PROGRAMMIEREN

CO-Drehzahl Abgleich programmieren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-steuern-testplatz"></a>
### STEUERN_TESTPLATZ

Freischaltung fuer SG-Befundung ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-ktest-motordrehzahl"></a>
### STATUS_KTEST_MOTORDREHZAHL

Motordrehzahl auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KTEST_MOTORDREHZAHL_WERT | real | Ergebnis Motordrehzahl |
| STAT_KTEST_MOTORDREHZAHL_EINH | string | Einheit Motordrehzahl |

<a id="job-status-ktest-an-lufttemperatur"></a>
### STATUS_KTEST_AN_LUFTTEMPERATUR

Ansauglufttemperatur auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KTEST_AN_LUFTTEMPERATUR_WERT | real | Ergebnis Ansauglufttemperatur |
| STAT_KTEST_AN_LUFTTEMPERATUR_EINH | string | Einheit Ansauglufttemperatur |

<a id="job-status-ktest-motortemperatur"></a>
### STATUS_KTEST_MOTORTEMPERATUR

Ansauglufttemperatur auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KTEST_MOTORTEMPERATUR_WERT | real | Ergebnis Ansauglufttemperatur |
| STAT_KTEST_MOTORTEMPERATUR_EINH | string | Einheit Ansauglufttemperatur |

<a id="job-status-ktest-dkp-winkel"></a>
### STATUS_KTEST_DKP_WINKEL

Ansauglufttemperatur auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KTEST_DKP_WINKEL_WERT | real | Ergebnis Ansauglufttemperatur |
| STAT_KTEST_DKP_WINKEL_EINH | string | Einheit Ansauglufttemperatur |

<a id="job-status-ktest-vanos-nw-lage-e-bank-1"></a>
### STATUS_KTEST_VANOS_NW_LAGE_E_BANK_1

Nockenwellenposition Bank1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_KTEST_VANOS_NW_LAGE_E_BANK_1_WERT | real | Ergebnis |
| STAT_KTEST_VANOS_NW_LAGE_E_BANK_1_EINH | string | Einheit |

<a id="job-status-ktest-vanos-nw-lage-e-bank-2"></a>
### STATUS_KTEST_VANOS_NW_LAGE_E_BANK_2

Nockenwellenposition Bank2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_KTEST_VANOS_NW_LAGE_E_BANK_2_WERT | real | Ergebnis |
| STAT_KTEST_VANOS_NW_LAGE_E_BANK_2_EINH | string | Einheit |

<a id="job-steuern-ktest-vanos-verstellzeit"></a>
### STEUERN_KTEST_VANOS_VERSTELLZEIT

Verstellzeitmessung VANOS

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POS1 | int | Vanos Sollwert max 40 Grad KW = 160 inc |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-klopfsensor1"></a>
### STATUS_KLOPFSENSOR1

Geraeuschwert Klopfsensor 1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KLOPF1_WERT | real | Klopfsensor 1 Geraeusch Wert |
| STAT_KLOPF1_EINH | string | Einheit V |

<a id="job-status-klopfsensor2"></a>
### STATUS_KLOPFSENSOR2

Geraeuschwert Klopfsensor 2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KLOPF2_WERT | real | Klopfsensor 2 Geraeusch Wert |
| STAT_KLOPF2_EINH | string | Einheit V |

<a id="job-status-klopfsensor3"></a>
### STATUS_KLOPFSENSOR3

Geraeuschwert Klopfsensor 3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KLOPF3_WERT | real | Klopfsensor 3 Geraeusch Wert |
| STAT_KLOPF3_EINH | string | Einheit V |

<a id="job-status-klopfsensor4"></a>
### STATUS_KLOPFSENSOR4

Geraeuschwert Klopfsensor 4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_KLOPF4_WERT | real | Klopfsensor 4 Geraeusch Wert |
| STAT_KLOPF4_EINH | string | Einheit V |

<a id="job-steuern-ev-selektiv-ausblenden"></a>
### STEUERN_EV_SELEKTIV_AUSBLENDEN

EV selektiv ausblenden, Zylinder 1- 6 angeben

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZYLINDER | int | Zylinder ueber Bitmuster 0-7 = Zyl 1-8   ,  1=EV = Aus , 0=EV=Ein |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-abgleich-timer-verstellen-programmieren"></a>
### ABGLEICH_TIMER_VERSTELLEN_PROGRAMMIEREN

FGR-Funktion und Mainswitch konfigurieren

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICH_TIMER_VERSTELLEN_PROGRAMMIEREN_WERT | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

Stellgliedansteuerung TEV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "POS_RESPONSE", wenn fehlerfrei |
| RESP_CODE | string | Code bei NEG_RESPONSE |

<a id="job-steuern-tev-aus"></a>
### STEUERN_TEV_AUS

Stellgliedansteuerung TEV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "POS_RESPONSE", wenn fehlerfrei |
| RESP_CODE | string | Code bei NEG_RESPONSE |

<a id="job-tev-system"></a>
### TEV_SYSTEM

Status Systemtest TEV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| STATUS | string | Status der TEV-Diagnose |
| JOB_STATUS | string | "POS_RESPONSE", wenn fehlerfrei |
| RESP_CODE | string | Code bei NEG_RESPONSE |

<a id="job-tev-zyklus"></a>
### TEV_ZYKLUS

Zyklusflags Systemtest TEV auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| Z_TEV | string | Zyklusflag Z_TEV auslesen |
| JOB_STATUS | string | "POS_RESPONSE", wenn fehlerfrei |
| RESP_CODE | string | Code bei NEG_RESPONSE |

<a id="job-tev-ende"></a>
### TEV_ENDE

Systemtestende von TEV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "POS_RESPONSE", wenn fehlerfrei |
| RESULT_TEXT | string | gibt den EndeCode der Diagnose zurueck |
| RESP_CODE | string | Code bei NEG_RESPONSE |

<a id="job-start-systemcheck-tev-func"></a>
### START_SYSTEMCHECK_TEV_FUNC

Stellgliedansteuerung TEV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY"wenn fehlerfrei |

<a id="job-lesen-systemcheck-tev-func"></a>
### LESEN_SYSTEMCHECK_TEV_FUNC

Zyklusflags Systemtest TEV auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| LESEN_SYSTEMCHECK_TEV_WERT | int |  |
| LESEN_SYSTEMCHECK_TEV_TEXT | string |  |
| JOB_STATUS | string | wenn fehlerfrei |

<a id="job-status-gaspedal"></a>
### STATUS_GASPEDAL

Fahrerwunsch

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_GASPEDAL_WERT | real | Ergebnis |

<a id="job-steuern-luftfilterklappe"></a>
### STEUERN_LUFTFILTERKLAPPE

Luftfilterklappe oeffnen bzw. schliessen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| POSITION | string | Werte: 'oeffnen', 'schliessen' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-steuern-dmtl-heizung"></a>
### STEUERN_DMTL_HEIZUNG

Stellgliedansteuerung DM-TL-Pumpenheizung

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SCHALTEN | string | Werte: 'ein', 'aus' |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

## Tables

### Index

- [BETRIEBSWTAB](#table-betriebswtab) (154 × 17)
- [JOBRESULT](#table-jobresult) (37 × 2)
- [FORTTEXTE12](#table-forttexte12) (132 × 6)
- [FTYPMATRIX](#table-ftypmatrix) (1 × 17)
- [FARTMATRIX](#table-fartmatrix) (133 × 49)
- [FARTTEXTE](#table-farttexte) (153 × 2)
- [FTYPTEXTE](#table-ftyptexte) (7 × 2)
- [STAGEDMTL](#table-stagedmtl) (17 × 2)
- [STAGEDMTLFREEZE](#table-stagedmtlfreeze) (23 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (118 × 6)
- [FEHLERCODES](#table-fehlercodes) (30 × 2)
- [STAGEPOINTER](#table-stagepointer) (20 × 2)
- [TEVSTATUS](#table-tevstatus) (5 × 2)
- [MFL_BITS](#table-mfl-bits) (7 × 4)
- [SONDE_BITS](#table-sonde-bits) (8 × 4)
- [LL_BITS](#table-ll-bits) (5 × 4)
- [ABGAS_BITS](#table-abgas-bits) (5 × 4)
- [CHECK_BITS](#table-check-bits) (6 × 4)
- [TEILE_BITS](#table-teile-bits) (20 × 4)
- [PKW_BITS](#table-pkw-bits) (4 × 4)

<a id="table-betriebswtab"></a>
### BETRIEBSWTAB

Dimensions: 154 rows × 17 columns

| NAME | TELEGRAM | POS_ADR | LEN_ADR | ADR | BYTE | DATA_TYPE | COMPU_TYPE | FACT_A | FACT_B | MASK | VALUE | ANZ | MEAS | RANGE | JOBNAME | LNAME |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RKRN_W0 | B812F103224000 |  | 0 |  | 33 | 5 | -- | 0.019531 | 0 | 0 | 0 | 3.3 | V |   |  | norm. Ref.pegel Klopfr. Zyl.1 |
| RKRN_W1 | B812F103224000 |  | 0 |  | 35 | 5 | -- | 0.019531 | 0 | 0 | 0 | 3.3 | V |   |  | norm. Ref.pegel Klopfr. Zyl.2 |
| RKRN_W2 | B812F103224000 |  | 0 |  | 37 | 5 | -- | 0.019531 | 0 | 0 | 0 | 3.3 | V |   |  | norm. Ref.pegel Klopfr. Zyl.3 |
| RKRN_W3 | B812F103224000 |  | 0 |  | 39 | 5 | -- | 0.019531 | 0 | 0 | 0 | 3.3 | V |   |  | norm. Ref.pegel Klopfr. Zyl.4 |
| RKRN_W4 | B812F103224000 |  | 0 |  | 41 | 5 | -- | 0.019531 | 0 | 0 | 0 | 3.3 | V |   |  | norm. Ref.pegel Klopfr. Zyl.5 |
| RKRN_W5 | B812F103224000 |  | 0 |  | 43 | 5 | -- | 0.019531 | 0 | 0 | 0 | 3.3 | V |   |  | norm. Ref.pegel Klopfr. Zyl.6 |
| RKRN_W6 | B812F103224000 |  | 0 |  | 45 | 5 | -- | 0.019531 | 0 | 0 | 0 | 3.3 | V |   |  | norm. Ref.pegel Klopfr. Zyl.7 |
| RKRN_W7 | B812F103224000 |  | 0 |  | 47 | 5 | -- | 0.019531 | 0 | 0 | 0 | 3.3 | V |   |  | norm. Ref.pegel Klopfr. Zyl.8 |
| DSLSRTKATM | B812F106230000000502 | 05 | 3 | 0x3809B4 | 5 | 2 | -- | 1 | -50 | 0 | 0 | 1.0 |   |   | DSLSRTKATM | Wert fuer TKATM               |
| DSLSRML | B812F106230000000502 | 05 | 3 | 0x00F852 | 5 | 4 | -- | 1 | 0 | 0 | 0 | 1.0 |   |   | DSLSRML | Wert fuer ML                  |
| S_EVAN_S | B812F106230000000502 | 05 | 3 | 0x380976 | 5 | 5 | -- | 0.25 | 0 | 0x80 | 0x80 | 2.4 | GradKW |   | S_EVAN_S | Nockenwinkel Sollwert  auslesen |
| NW_B1_FL1 | B812F103224006 | 7 | 3 | 0x38301C | 5 | 6 | -- | 0.0039062 | 0 | 0 | 0 | 3.3 | GradKW |   |  | Adaptionswinkel NW-B1 Flanke 1 |
| NW_B1_FL2 | B812F103224006 | 9 | 7 | 0x38301E | 5 | 6 | -- | 0.0039062 | 0 | 0 | 0 | 3.3 | GradKW |   |  | Adaptionswinkel NW-B1 Flanke 2 |
| NW_B1_FL3 | B812F103224006 | 11 | 7 | 0x383020 | 5 | 6 | -- | 0.0039062 | 0 | 0 | 0 | 3.3 | GradKW |   |  | Adaptionswinkel NW-B1 Flanke 3 |
| NW_B1_FL4 | B812F103224006 | 13 | 7 | 0x383022 | 5 | 6 | -- | 0.0039062 | 0 | 0 | 0 | 3.3 | GradKW |   |  | Adaptionswinkel NW-B1 Flanke 4 |
| NW_B2_FL1 | B812F103224006 | 15 | 7 | 0x383024 | 5 | 6 | -- | 0.0039062 | 0 | 0 | 0 | 3.3 | GradKW |   |  | Adaptionswinkel NW-B1 Flanke 1 |
| NW_B2_FL2 | B812F103224006 | 17 | 7 | 0x383026 | 5 | 6 | -- | 0.0039062 | 0 | 0 | 0 | 3.3 | GradKW |   |  | Adaptionswinkel NW-B1 Flanke 2 |
| NW_B2_FL3 | B812F103224006 | 19 | 7 | 0x383028 | 5 | 6 | -- | 0.0039062 | 0 | 0 | 0 | 3.3 | GradKW |   |  | Adaptionswinkel NW-B2 Flanke 3 |
| NW_B2_FL4 | B812F103224006 | 21 | 7 | 0x38302A | 5 | 6 | -- | 0.0039062 | 0 | 0 | 0 | 3.3 | GradKW |   |  | Adaptionswinkel NW-B2 Flanke 4 |
| TNST_W | B812F106230000000502 | 05 | 3 | 0x3813DC | 5 | 6 | -- | 0.01 | 0 | 0 | 0x80 | 2.4 | GradKW |   | NW_B2_FL4 | Adaptionswinkel NW-B2 Flanke 4 |
| TPLDP | B812F106230000000502 | 05 | 3 | 0x382572 | 5 | 6 | -- | 0.01 | 0 | 0 | 0x80 | 2.4 | GradKW |   | NW_B2_FL4 | Adaptionswinkel NW-B2 Flanke 4 |
| LRNSTEP | B812F106230000000501 | 05 | 3 | 0x380C2F | 5 | 2 | -- | 1 | 0 | 0 | 0 | 1.0 |   |   | LRNSTEP | Lernstep DK-Apaption lesen     |
| TI_W | B812F103224000 | 0  | 0 | 0  | 7 | 5 | -- | 0.016 | 0 | 0 | 0 | 4.2 | ms |   | EINSPRITZZEIT | Einspritzzeit EV1              |
| FR_W | B812F103224000 | 0  | 0 | 0  | 9 | 5 | -- | 0.0000305 | 0 | 0 | 0 | 2.4 |   |   | LAMBDA_INTEGRATOR_1 | Lambdaregler1                  |
| FR_W | B812F103224000 | 0  | 0 | 0  | 9 | 5 | -- | 0.0000305 | 0 | 0 | 0 | 2.4 |   |   | INT | Lambdaregler1                  |
| FR2_W | B812F103224000 | 0  | 0 | 0  | 11 | 5 | -- | 0.0000305 | 0 | 0 | 0 | 2.4 |   |   | LAMBDA_INTEGRATOR_2 | Lambdaregler2                  |
| FR2_W | B812F103224000 | 0  | 0 | 0  | 11 | 5 | -- | 0.0000305 | 0 | 0 | 0 | 2.4 |   |   | INT2 | Lambdaregler2                  |
| VFZG | B812F103224000 | 0  | 0 | 0  | 13 | 2 | -- | 1.25 | 0 | 0 | 0 | 3.1 | km/h |   | GESCHWINDIGKEIT | Fahrzeuggeschwindigkeit        |
| NMOT_W | B812F103224000 | 0  | 0 | 0  | 14 | 5 | -- | 0.25 | 0 | 0 | 0 | 5.1 | min-1 |   | MOTORDREHZAHL | Motordrehzahl                  |
| NSOL | B812F103224000 | 0  | 0 | 0  | 16 | 2 | -- | 10 | 0 | 0 | 0 | 5.1 | min-1 |   | MOTORDREHZAHL_SOLL | LL-Solldrehzahl                |
| WNWI_0 | B812F103224000 | 0  | 0 | 0  | 17 | 7 | -- | 0.0039 | 0 | 0 | 0 | 3.2 | GradKW |   | VANOS_NW_LAGE_EINLASS_BANK_1 | Nockenwellenposition Bank1     |
| WNWI_1 | B812F103224000 | 0  | 0 | 0  | 19 | 7 | -- | 0.0039 | 0 | 0 | 0 | 3.2 | GradKW |   | VANOS_NW_LAGE_EINLASS_BANK_2 | Nockenwellenposition Bank2     |
| TANS | B812F103224000 | 0  | 0 | 0  | 21 | 2 | -- | 0.75 | -48 | 0 | 0 | 3.1 | Grad C |   | AN_LUFTTEMPERATUR | Ansauglufttemperatur           |
| TMOT | B812F103224000 | 0  | 0 | 0  | 22 | 2 | -- | 0.75 | -48 | 0 | 0 | 3.1 | Grad C |   | MOTORTEMPERATUR | Motortemperatur                |
| ZWOUT | B812F103224000 | 0  | 0 | 0  | 23 | 3 | -- | 0.75 | 0 | 0 | 0 | 3.1 | Grad |   | ZUENDWINKEL | Zuendwinkel Zyl1               |
| WDKBA | B812F103224000 | 0  | 0 | 0  | 24 | 2 | -- | 0.39216 | 0 | 0 | 0 | 3.2 | % DK |   | DKP_WINKEL | DK-Winkel                      |
| MSHFM_W | B812F103224000 | 0  | 0 | 0  | 25 | 5 | -- | 0.1 | 0 | 0 | 0 | 3.1 | kg/h |   | LMM_MASSE | Luftmasse                      |
| MIIST_W | B812F103224000 | 0  | 0 | 0  | 27 | 5 | -- | 0.0015259 | 0 | 0 | 0 | 3.3 | % |   | MIIST | MIIST                          |
| UB | B812F103224000 | 0  | 0 | 0  | 29 | 2 | -- | 0.095 | 0 | 0 | 0 | 3.3 | V |   | UBATT | Ubatt                          |
| UPWG_W | B812F103224000 | 0  | 0 | 0  | 30 | 5 | -- | 0.0048828 | 0 | 0 | 0 | 3.3 | V |   | PWG_POTI_SPANNUNG | Fahrerwunsch                   |
| UPWG1_W | B812F103304601 | 0  | 0 | 0  | 7 | 5 | -- | 0.0048828 | 0 | 0 | 0 | 3.3 | V |   | PWG1_POTI_SPANNUNG | Fahrerwunsch                   |
| UPWG2_W | B812F103304701 | 0  | 0 | 0  | 7 | 5 | -- | 0.0048828 | 0 | 0 | 0 | 3.3 | V |   | PWG2_POTI_SPANNUNG | Fahrerwunsch                   |
| TKA | B812F103224000 | 0  | 0 | 0  | 32 | 2 | -- | 0.75 | -48 | 0 | 0 | 3.1 | Grad C |   | KUEHLW_AUSL_TEMPERATUR | Temperatur Kuehleraustritt      |
| ILB | B812F103224001 | 0  | 0 | 0  | 7 | 7 | -- | 0,0711 | 0 | 0 | 0 | 4.3 |   |   | LDB_INTEGRATOR | Integrator Ladebilanz Batterie |
| USVK | B812F103224003 | 0  | 0 | 0  | 24 | 5 | -- | 0.0048818 | -1.0 | 0 | 0 | 3.3 | V |   | LS_VKAT_SIGNAL_1 | Lambdasondenspannung v Kat     |
| USVK | B812F103224003 | 0  | 0 | 0  | 24 | 5 | -- | 0.0048818 | -1.0 | 0 | 0 | 3.3 | V |   | L_SONDE | Lambdasondenspannung v Kat     |
| USVK2 | B812F103224003 | 0  | 0 | 0  | 26 | 5 | -- | 0.0048818 | -1.0 | 0 | 0 | 3.3 | V |   | LS_VKAT_SIGNAL_2 | Lambdasondenspannung v Kat 2   |
| USVK2 | B812F103224003 | 0  | 0 | 0  | 26 | 5 | -- | 0.0048818 | -1.0 | 0 | 0 | 3.3 | V |   | L_SONDE_2 | Lambdasondenspannung v Kat 2   |
| USNK | B812F103300001 | 5  | 1 | 0x48 | 07 | 5 | -- | 0.0048818 | 0 | 0 | 0 | 3.3 | V |   | LS_NKAT_SIGNAL_1 | Lambdasondenspannung n Kat     |
| USNK | B812F103300001 | 5  | 1 | 0x48 | 07 | 5 | -- | 0.0048818 | 0 | 0 | 0 | 3.3 | V |   | L_SONDE_H | Lambdasondenspannung n Kat     |
| USNK2 | B812F103300001 | 5  | 1 | 0x45 | 07 | 5 | -- | 0.0048818 | 0 | 0 | 0 | 3.3 | V |   | LS_NKAT_SIGNAL_2 | Lambdasondenspannung n Kat 2   |
| USNK2 | B812F103300001 | 5  | 1 | 0x45 | 07 | 5 | -- | 0.0048818 | 0 | 0 | 0 | 3.3 | V |   | L_SONDE_2_H | Lambdasondenspannung n Kat 2   |
| RKAT_W | B812F103224004 | 0  | 0 | 0  | 7 | 7 | -- | 0.046875 | 0 | 0 | 0 | 4.1 | % |   | LAMBDA_ADD_1 | Gemischadaption additiv 1      |
| RKAT_W | B812F103224004 | 0  | 0 | 0  | 7 | 7 | -- | 0.046875 | 0 | 0 | 0 | 4.1 | % |   | ADD | Gemischadaption additiv 1      |
| RKAT2_W | B812F103224004 | 0  | 0 | 0  | 9 | 7 | -- | 0.046875 | 0 | 0 | 0 | 4.1 | % |   | LAMBDA_ADD_2 | Gemischadaption additiv 2      |
| RKAT2_W | B812F103224004 | 0  | 0 | 0  | 9 | 7 | -- | 0.046875 | 0 | 0 | 0 | 4.1 | % |   | ADD_2 | Gemischadaption additiv 2      |
| FRA_W | B812F103224004 | 0  | 0 | 0  | 11 | 7 | -- | 0.0000305 | 0 | 0 | 0 | 4.1 | % |   | LAMBDA_MUL_1 | Gemischadaption multipl. 1     |
| FRA_W | B812F103224004 | 0  | 0 | 0  | 11 | 7 | -- | 0.0000305 | 0 | 0 | 0 | 4.1 | % |   | MUL | Gemischadaption multipl. 1     |
| FRA2_W | B812F103224004 | 0  | 0 | 0  | 13 | 7 | -- | 0.0000305 | 0 | 0 | 0 | 4.1 | % |   | LAMBDA_MUL_2 | Gemischadaption multipl. 2     |
| FRA2_W | B812F103224004 | 0  | 0 | 0  | 13 | 7 | -- | 0.0000305 | 0 | 0 | 0 | 4.1 | % |   | MUL_2 | Gemischadaption multipl. 2     |
| PHLSNV | B812F103224004 | 0  | 0 | 0  | 15 | 2 | -- | 0.01 | 0 | 0 | 0 | 1.2 |   |   | LS_VKAT_HEIZUNG_TV_1 | norm. Heizleist. L-Sonde vKat1 |
| PHLSNV2 | B812F103224004 | 0  | 0 | 0  | 16 | 2 | -- | 0.01 | 0 | 0 | 0 | 1.2 |   |   | LS_VKAT_HEIZUNG_TV_2 | norm. Heizleist. L-Sonde vKat2 |
| PHLSNH | B812F103224004 | 0  | 0 | 0  | 17 | 2 | -- | 0.01 | 0 | 0 | 0 | 1.2 |   |   | LS_NKAT_HEIZUNG_TV_1 | norm. Heizleist. L-Sonde hKat1 |
| PHLSNH2 | B812F103224004 | 0  | 0 | 0  | 18 | 2 | -- | 0.01 | 0 | 0 | 0 | 1.2 |   |   | LS_NKAT_HEIZUNG_TV_2 | norm. Heizleist. L-Sonde hKat2 |
| TPLRVK_W | B812F103224004 | 0  | 0 | 0  | 19 | 5 | -- | 0.01 | 0 | 0 | 0 | 3.3 | s |   | LS_VKAT_PERIODENDAUER_1 | PeridenDauer L-Sonde v Kat1    |
| TPLRVK2_W | B812F103224004 | 0  | 0 | 0  | 21 | 5 | -- | 0.01 | 0 | 0 | 0 | 3.3 | s |   | LS_VKAT_PERIODENDAUER_2 | PeridenDauer L-Sonde v Kat2    |
| TATEIST | B812F103224005 | 0  | 0 | 0  | 7 | 2 | -- | 0.39062 | 0 | 0 | 0 | 3.3 | % |   | TE_TASTVERHAELTNIS | Tastverhaeltnis TEV            |
| TANWR_0 | B812F103224005 | 0  | 0 | 0  | 12 | 2 | -- | 0.39216 | 0 | 0 | 0 | 3.3 | %TV |   | VANOS_NW_LAGE_EINLASS_TV_1 | Tastverhaeltnis Vanos 1        |
| TANWR_1 | B812F103224005 | 0  | 0 | 0  | 13 | 2 | -- | 0.39216 | 0 | 0 | 0 | 3.3 | %TV |   | VANOS_NW_LAGE_EINLASS_TV_2 | Tastverhaeltnis Vanos 2        |
| TAML | B812F103224005 | 0  | 0 | 0  | 14 | 2 | -- | 0.39216 | 0 | 0 | 0 | 3.3 | % |   | E_LUEFTER_TV | Tastverhaeltnis E-Luefter      |
| LUTSFI1 | B812F103224003 | 0  | 0 | 0  | 7 | 7 | -- | 0.0027756 | 0 | 0 | 0 | 3.3 | sec-1 |   | LUTSFI1 | gefilterte Laufunruhen Zyl1    |
| LUTSFI2 | B812F103224003 | 0  | 0 | 0  | 9 | 7 | -- | 0.0027756 | 0 | 0 | 0 | 3.3 | sec-1 |   | LUTSFI2 | gefilterte Laufunruhen Zyl2    |
| LUTSFI3 | B812F103224003 | 0  | 0 | 0  | 11 | 7 | -- | 0.0027756 | 0 | 0 | 0 | 3.3 | sec-1 |   | LUTSFI3 | gefilterte Laufunruhen Zyl3    |
| LUTSFI4 | B812F103224003 | 0  | 0 | 0  | 13 | 7 | -- | 0.0027756 | 0 | 0 | 0 | 3.3 | sec-1 |   | LUTSFI4 | gefilterte Laufunruhen Zyl4    |
| LUTSFI5 | B812F103224003 | 0  | 0 | 0  | 15 | 7 | -- | 0.0027756 | 0 | 0 | 0 | 3.3 | sec-1 |   | LUTSFI5 | gefilterte Laufunruhen Zyl5    |
| LUTSFI6 | B812F103224003 | 0  | 0 | 0  | 17 | 7 | -- | 0.0027756 | 0 | 0 | 0 | 3.3 | sec-1 |   | LUTSFI6 | gefilterte Laufunruhen Zyl6    |
| LUTSFI7 | B812F103224003 | 0  | 0 | 0  | 19 | 7 | -- | 0.0027756 | 0 | 0 | 0 | 3.3 | sec-1 |   | LUTSFI7 | gefilterte Laufunruhen Zyl7    |
| LUTSFI8 | B812F103224003 | 0  | 0 | 0  | 21 | 7 | -- | 0.0027756 | 0 | 0 | 0 | 3.3 | sec-1 |   | LUTSFI8 | gefilterte Laufunruhen Zyl8    |
| B_NAC | B812F103224001 | 0  | 0 | 0  | 9 | 1 | -- | 1 | 0 | 0x80 | 0x80 | 1.0 |   |   |   | B_NAC (LL-Anheb. bei KA)       |
| B_FHZ | B812F103224001 | 0  | 0 | 0  | 9 | 1 | -- | 1 | 0 | 0x40 | 0x40 | 1.0 |   |   |   | B_FHZ (Frontscheibenheiz.)     |
| B_NFTEV | B812F103224001 | 0  | 0 | 0  | 9 | 1 | -- | 1 | 0 | 0x20 | 0x20 | 1.0 |   |   |   | B_NFTEV(N-Anh. erh. TE-Spuelen) |
| B_DKPU | B812F103224001 | 0  | 0 | 0  | 9 | 1 | -- | 1 | 0 | 0x10 | 0x10 | 1.0 |   |   |   | B_DKPU (DK_Pos. falsch (SKA))  |
| B_NSUB | B812F103224001 | 0  | 0 | 0  | 9 | 1 | -- | 1 | 0 | 0x08 | 0x08 | 1.0 |   |   |   | B_NSUB (N-Anheb. niedr. UBatt) |
| B_KO | B812F103224002 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x80 | 0x80 | 1.0 |   |   |   | B_KO                           |
| S_BRS | B812F103224002 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x10 | 0x10 | 1.0 |   |   |   | S_BRS                          |
| S_BLS | B812F103224002 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x08 | 0x08 | 1.0 |   |   |   | S_BLS                          |
| B_KUPPL | B812F103224002 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x04 | 0x04 | 1.0 |   |   |   | B_KUPPL                        |
| B_ESTART | B812F103224002 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x02 | 0x02 | 1.0 |   |   |   | B_ESTART                       |
| B_KL15 | B812F103224002 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x01 | 0x01 | 1.0 |   |   |   | B_KL15                         |
| B_FOR11 | B812F103224003 | 0  | 0 | 0  | 35 | 2 | -- | 1 | 0 | 0 | 0 | 1.0 |   |   |   | Adaption abgeschlossen (LL)    |
| B_HSHE | B812F103224005 | 0  | 0 | 0  | 13 | 1 | -- | 1 | 0 | 0x80 | 0x80 | 1.0 |   |   |   | B_HSHE                         |
| B_HSHE2 | B812F103224005 | 0  | 0 | 0  | 13 | 1 | -- | 1 | 0 | 0x40 | 0x40 | 1.0 |   |   |   | B_HSHE2                        |
| B_HSVE | B812F103224005 | 0  | 0 | 0  | 13 | 1 | -- | 1 | 0 | 0x20 | 0x20 | 1.0 |   |   |   | B_HSVE                         |
| B_HSVE2 | B812F103224005 | 0  | 0 | 0  | 13 | 1 | -- | 1 | 0 | 0x10 | 0x10 | 1.0 |   |   |   | B_HSVE2                        |
| B_LR | B812F103224007 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x80 | 0x80 | 1.0 |   |   |   | B_LR                           |
| B_LR2 | B812F103224007 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x40 | 0x40 | 1.0 |   |   |   | B_LR2                          |
| B_SBBVK | B812F103224007 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x20 | 0x20 | 1.0 |   |   |   | B_SBBVK                        |
| B_SBBVK2 | B812F103224007 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x10 | 0x10 | 1.0 |   |   |   | B_SBBVK2                       |
| B_SBBHK | B812F103224007 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x08 | 0x08 | 1.0 |   |   |   | B_SBBHK                        |
| B_SBBHK2 | B812F103224007 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x04 | 0x04 | 1.0 |   |   |   | B_SBBHK2                       |
| B_VL | B812F103224007 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x02 | 0x02 | 1.0 |   |   |   | B_VL                           |
| B_LL | B812F103224007 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x01 | 0x01 | 1.0 |   |   |   | B_LL                           |
| B_UMAERF | B812F103224007 | 0  | 0 | 0  | 8 | 1 | -- | 1 | 0 | 0x80 | 0x80 | 1.0 |   |   |   | B_UMAERF                       |
| B_SA | B812F103224007 | 0  | 0 | 0  | 8 | 1 | -- | 1 | 0 | 0x40 | 0x40 | 1.0 |   |   |   | B_SA                           |
| B_TEHB | B812F103224007 | 0  | 0 | 0  | 8 | 1 | -- | 1 | 0 | 0x20 | 0x20 | 1.0 |   |   |   | B_TEHB                         |
| B_EWS_OK | B812F103224007 | 0  | 0 | 0  | 8 | 1 | -- | 1 | 0 | 0x10 | 0x10 | 1.0 |   |   |   | B_EWS_OK                       |
| B_PN | B812F103224007 | 0  | 0 | 0  | 8 | 1 | -- | 1 | 0 | 0x08 | 0x08 | 1.0 |   |   |   | B_PN                           |
| B_NOKATFZG | B812F10330A801 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x01 | 0x01 | 1.0 |   |   |   | B_NOKATFZG                     |
| L_FGR | B812F1022107 | 0  | 0 | 0  | 6 | 1 | -- | 1 | 0 | 0x40 | 0x40 | 1.0 |   |   |   | L_FGR                          |
| B_FGRTVE | B812F1022107 | 0  | 0 | 0  | 6 | 1 | -- | 1 | 0 | 0x10 | 0x10 | 1.0 |   |   |   | B_FGRTVE                       |
| B_FGRHSA | B812F1022107 | 0  | 0 | 0  | 6 | 1 | -- | 1 | 0 | 0x02 | 0x02 | 1.0 |   |   |   | B_FGRHSA                       |
| B_FGRTSE | B812F1022107 | 0  | 0 | 0  | 6 | 1 | -- | 1 | 0 | 0x08 | 0x08 | 1.0 |   |   |   | B_FGRTSE                       |
| B_FGRAT | B812F1022107 | 0  | 0 | 0  | 6 | 1 | -- | 1 | 0 | 0x01 | 0x01 | 1.0 |   |   |   | B_FGRAT                        |
| B_FGRTWA | B812F1022107 | 0  | 0 | 0  | 6 | 1 | -- | 1 | 0 | 0x20 | 0x20 | 1.0 |   |   |   | B_FGRTWA                       |
| B_FGRTBE | B812F1022107 | 0  | 0 | 0  | 6 | 1 | -- | 1 | 0 | 0x04 | 0x04 | 1.0 |   |   |   | B_FGRTBE                       |
| B_CDLSV | B812F1022105 | 0  | 0 | 0  | 6 | 1 | -- | 1 | 0 | 0x20 | 0x20 | 1.0 |   |   |   | B_CDLSV                        |
| B_CDAGR | B812F1022105 | 0  | 0 | 0  | 6 | 1 | -- | 1 | 0 | 0x80 | 0x80 | 1.0 |   |   |   | B_CDAGR                        |
| B_CDSLS | B812F1022105 | 0  | 0 | 0  | 6 | 1 | -- | 1 | 0 | 0x08 | 0x08 | 1.0 |   |   |   | B_CDSLS                        |
| B_CDHSV | B812F1022105 | 0  | 0 | 0  | 6 | 1 | -- | 1 | 0 | 0x40 | 0x40 | 1.0 |   |   |   | B_CDHSV                        |
| B_CDTES | B812F1022105 | 0  | 0 | 0  | 6 | 1 | -- | 1 | 0 | 0x04 | 0x04 | 1.0 |   |   |   | B_CDTES                        |
| B_HSRDY | B812F1022105 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x40 | 0x40 | 1.0 |   |   |   | B_HSRDY                        |
| B_TESRDY | B812F1022105 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x04 | 0x04 | 1.0 |   |   |   | B_TESRDY                       |
| B_SLSRDY | B812F1022105 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x08 | 0x08 | 1.0 |   |   |   | B_SLSRDY                       |
| B_LSRDY | B812F1022105 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x20 | 0x20 | 1.0 |   |   |   | B_LSRRDY                       |
| B_KATRDY | B812F1022105 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x01 | 0x01 | 1.0 |   |   |   | B_KATRDY                       |
| B_AGRRDY | B812F1022105 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x80 | 0x80 | 1.0 |   |   |   | B_AGRRDY                       |
| L_LDPR | B812F103224002 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x20 | 0x20 | 1.0 |   |   |   | S_LDPR                         |
| B_LDPEIN | B812F103224005 | 0  | 0 | 0  | 13 | 1 | -- | 1 | 0 | 0x01 | 0x01 | 1.0 |   |   |   | B_LDPEIN                       |
| B_SLP | B812F103224005 | 0  | 0 | 0  | 13 | 1 | -- | 1 | 0 | 0x04 | 0x04 | 1.0 |   |   |   | B_SLP                          |
| B_STA | B812F103224005 | 0  | 0 | 0  | 14 | 1 | -- | 1 | 0 | 0x80 | 0x80 | 1.0 |   |   |   | B_STA                          |
| B_EBL | B812F103224005 | 0  | 0 | 0  | 14 | 1 | -- | 1 | 0 | 0x10 | 0x10 | 1.0 |   |   |   | B_EBL                          |
| B_KOE | B812F103224005 | 0  | 0 | 0  | 13 | 1 | -- | 1 | 0 | 0x04 | 0x04 | 1.0 |   |   |   | B_KOE                          |
| B_EKP | B812F103224005 | 0  | 0 | 0  | 14 | 1 | -- | 1 | 0 | 0x20 | 0x20 | 1.0 |   |   |   | B_EKP                          |
| B_SLV | B812F103224005 | 0  | 0 | 0  | 13 | 1 | -- | 1 | 0 | 0x02 | 0x02 | 1.0 |   |   |   | B_SLV                          |
| B_ETR | B812F103224005 | 0  | 0 | 0  | 14 | 1 | -- | 1 | 0 | 0x40 | 0x40 | 1.0 |   |   |   | B_ETR                          |
| B_AKR | B812F103224005 | 0  | 0 | 0  | 14 | 1 | -- | 1 | 0 | 0x08 | 0x08 | 1.0 |   |   |   | B_AKR                          |
| B_ASC_PKW | B812F10330A801 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x08 | 0x08 | 1.0 |   |   |   | B_ASC_PKW                      |
| B_ACC | B812F10330A801 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x04 | 0x04 | 1.0 |   |   |   | B_ACC                          |
| B_AUTGET | B812F10330A801 | 0  | 0 | 0  | 7 | 1 | -- | 1 | 0 | 0x02 | 0x02 | 1.0 |   |   |   | B_AUTGET                       |
| NWSDSTAT | B812F1022114 | 0  | 0 | 0  | 6 | 2 | -- | 1 | 0 | 0 | 0 | 1.0 |   |   |   | Vanos1-Dichtheit               |
| NWSDSTAT2 | B812F1022114 | 0  | 0 | 0  | 7 | 2 | -- | 1 | 0 | 0 | 0 | 1.0 |   |   |   | Vanos2-Dichtheit               |
| WNWI_W0 | B812F1022114 | 0  | 0 | 0  | 8 | 7 | -- | 0.0039 | 0 | 0 | 0 | 1.0 | GradKW |   |   | Istwinkel fuer Vanos1          |
| WNWI_W1 | B812F1022114 | 0  | 0 | 0  | 10 | 7 | -- | 0.0039 | 0 | 0 | 0 | 1.0 | GradKW |   |   | Istwinkel fuer Vanos2          |
| NWSSTAT | B812F1022113 | 0  | 0 | 0  | 6 | 2 | -- | 1 | 0 | 0 | 0 | 1.0 |   |   |   | Verstellzeitpruef. Vanos1      |
| NWSSTAT2 | B812F1022113 | 0  | 0 | 0  | 7 | 2 | -- | 1 | 0 | 0 | 0 | 1.0 |   |   |   | Verstellzeitpruef. Vanos2      |
| TNWSFI | B812F1022113 | 0  | 0 | 0  | 8 | 5 | -- | 0.01 | 0 | 0 | 0 | 1.0 | sec |   |   | Fruehverstellzeit NW1          |
| TNWSFI2 | B812F1022113 | 0  | 0 | 0  | 10 | 5 | -- | 0.01 | 0 | 0 | 0 | 1.0 | sec |   |   | Fruehverstellzeit NW2          |
| TNWSSI | B812F1022113 | 0  | 0 | 0  | 12 | 5 | -- | 0.01 | 0 | 0 | 0 | 1.0 | sec |   |   | Spaetverstellzeit NW1          |
| TNWSSI2 | B812F1022113 | 0  | 0 | 0  | 14 | 5 | -- | 0.01 | 0 | 0 | 0 | 1.0 | sec |   |   | Spaetverstellzeit NW2          |
| DNSLBV | B812F10330A101 | 0  | 0 | 0  | 9 | 3 | -- | 10 | 0 | 0 | 0 | 1.0 |   |   | Abgleichwert  | DNSLBV                         |
| DNLLMV | B812F10330A101 | 0  | 0 | 0  | 7 | 3 | -- | 10 | 0 | 0 | 0 | 1.0 |   |   | Abgleichwert  | DNLLMV                         |
| DNFSACMV | B812F10330A101 | 0  | 0 | 0  | 10 | 3 | -- | 10 | 0 | 0 | 0 | 1.0 |   |   | Abgleichwert  | DNFSACMV                       |
| DNSACMV | B812F10330A101 | 0  | 0 | 0  | 8 | 3 | -- | 10 | 0 | 0 | 0 | 1.0 |   |   | Abgleichwert  | DNSACMV                        |
| DNFSMV | B812F10330A101 | 0  | 0 | 0  | 11 | 3 | -- | 10 | 0 | 0 | 0 | 1.0 |   |   | Abgleichwert  | DNFSMV                         |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 37 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | ERROR_ECU_RESERVED_BY_DOCUMENT |
| 0x10 | ERROR_ECU_GENERAL_REJECT |
| 0x11 | ERROR_ECU_SERVICE_NOT_SUPPORTED |
| 0x12 | ERROR_ECU_SUBFUNCTION_NOT_SUPPORTED_INVALID_FORMAT |
| 0x21 | ERROR_ECU_BUSY_REPEAT_REQUEST |
| 0x22 | ERROR_ECU_CONDITIONS_NOT_CORRECT_OR_REQUEST_SEQUENCE_ERROR |
| 0x23 | ERROR_ECU_ROUTINE_NOT_COMPLETE |
| 0x31 | ERROR_ECU_REQUEST_OUT_OF_RANGE |
| 0x33 | ERROR_ECU_SECURITY_ACCESS_DENIED_SECURITY_ACCESS_REQUESTED |
| 0x35 | ERROR_ECU_INVALID_KEY |
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
| 0x78 | ERROR_ECU_REQ_CORRECTLY_RCVD_RSP_PENDING |
| 0x79 | ERROR_ECU_INCORRECT_BYTE_COUNT_DURING_BLOCK_TRANSFER |
| 0x80 | ERROR_ECU_SERVICE_NOT_SUPPORTED_IN_ACTIVE_DIGNOSTICMODE |
| 0xF9 | ERROR_ECU_VEHICLE_MANUFACTURER_SPECIFIC |
| 0xFE | ERROR_ECU_SYSTEM_SUPPLIER_SPECIFIC |
| 0xFF | ERROR_ECU_RESERVED_BY_DOCUMENT |
| ?01? | OKAY |
| ?02? | BUSY |
| ?03? | AIF_NICHT_PROGRAMMIERT |
| ?04? | KEIN AIF MEHR FREI |
| 0xXY | ERROR_ECU_UNKNOWN_STATUSBYTE |

<a id="table-forttexte12"></a>
### FORTTEXTE12

Dimensions: 132 rows × 6 columns

| ORT | ORTTEXT | UW_1 | UW_2 | UW_3 | UW_4 |
| --- | --- | --- | --- | --- | --- |
| 0x01 | Leckage Diagnosepumpe Endstufe | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x02 | Magnetventil DMTL Endstufe | 0x0A | 0x14 | 0x24 | 0x0B |
| 0x03 | Vertauschte Lambdasonden | 0x29 | 0x8C | 0x06 | 0x08 |
| 0x04 | Lambdasonden-Heizung hinter Kat (Bank2) | 0x79 | 0x30 | 0x7D | 0x34 |
| 0x05 | Lambdasonden-Heizung vor Kat (Bank2) | 0x7B | 0x2E | 0x7F | 0x32 |
| 0x0A | Lambdasonde vor Kat | 0x29 | 0x8C | 0x31 | 0x16 |
| 0x0C | Lambdasonde hinter Kat | 0x2B | 0x8C | 0x33 | 0x17 |
| 0x0D | Lambdasonden-Heizung vor Kat | 0x7A | 0x2D | 0x7E | 0x31 |
| 0x0E | Lambdasonden-Heizung hinter Kat | 0x78 | 0x2F | 0x7C | 0x33 |
| 0x0F | Lambda-Sondenalterung Periodendauer | 0x0A | 0x29 | 0x31 | 0x36 |
| 0x10 | Lambda-Sondenalterung TV | 0x0A | 0x29 | 0x31 | 0x36 |
| 0x11 | Lambda-Sondenalterung h. Kat | 0x0A | 0x2B | 0x33 | 0x17 |
| 0x12 | Lambda-Sonde2 vor Kat | 0x2A | 0x8C | 0x32 | 0x18 |
| 0x14 | Lambda-Sonde2 hinter Kat | 0x2C | 0x8C | 0x34 | 0x19 |
| 0x15 | Lambda-Sondenalterung Periodendauer Bank2 | 0x0A | 0x2A | 0x32 | 0x37 |
| 0x16 | Lambda-Sondenalterung TV Bank2 | 0x0A | 0x2A | 0x32 | 0x37 |
| 0x17 | Lambda-Sondenalterung h. Kat Bank2 | 0x0A | 0x2C | 0x34 | 0x19 |
| 0x18 | LR-Adaption multiplikativ Bereich2 | 0x0A | 0x1A | 0x13 | 0x3C |
| 0x19 | LR-Adaption multipl. Bereich2 (Bank2) | 0x0A | 0x1A | 0x13 | 0x3C |
| 0x1A | LR-Adaption multiplikativ Bereich1 | 0x0A | 0x1A | 0x13 | 0x3C |
| 0x1B | LR-Adaption multipl. Bereich1 (Bank2) | 0x0A | 0x1A | 0x13 | 0x3C |
| 0x1C | LR-Adaption additiv pro Zeit | 0x0A | 0x1A | 0x3C | 0x05 |
| 0x1D | LR-Adaption additiv pro Zeit Bank 2 | 0x0A | 0x1A | 0x3C | 0x07 |
| 0x1E | LR-Adaption additiv pro Zuendung | 0x0A | 0x1A | 0x3C | 0x05 |
| 0x1F | LR-Adaption additiv pro Zuendung Bank 2 | 0x0A | 0x1A | 0x3C | 0x07 |
| 0x20 | Leerlaufregelung fehlerhaft | 0x0A | 0x1A | 0x14 | 0x15 |
| 0x21 | Nockenwellensteuerung | 0x0A | 0x12 | 0x6C | 0x6E |
| 0x22 | Nockenwellensteuerung Bank 2 | 0x0A | 0x12 | 0x6D | 0x6F |
| 0x27 | EWS3.3 Manipulationsschutz | 0x0A | 0x14 | 0x00 | 0x00 |
| 0x28 | Katalysator-Konvertierung | 0x88 | 0x89 | 0x06 | 0x3C |
| 0x2D | Katalysator-Konvertierung (Bank2) | 0x87 | 0x8A | 0x08 | 0x3C |
| 0x32 | Aussetzererkennung Zyl.1,   | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x33 | Aussetzererkennung Zyl.5,   | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x34 | Aussetzererkennung Zyl.4,   | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x35 | Aussetzererkennung Zyl.8,   | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x36 | Aussetzererkennung Zyl.6,   | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x37 | Aussetzererkennung Zyl.3,   | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x38 | Aussetzererkennung Zyl.7,   | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x39 | Aussetzererkennung Zyl.2,   | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x3E | Aussetzererkennung, Summenfehler,  | 0x0A | 0x1A | 0x12 | 0x3C |
| 0x50 | Sekundaerluftsystem | 0x85 | 0x82 | 0x8B | 0x84 |
| 0x51 | Sekundaerluftsystem Bank2 | 0x86 | 0x83 | 0x8B | 0x84 |
| 0x52 | Sekundaerluftventil | 0x0A | 0x11 | 0x14 | 0x05 |
| 0x54 | Endstufe Relais Sekundaerluftpumpe | 0x0A | 0x12 | 0x13 | 0x14 |
| 0x55 | Sekundaerluftventil Endstufe | 0x0A | 0x12 | 0x13 | 0x14 |
| 0x5D | Tankentlueftung functional check | 0x0A | 0x1A | 0x24 | 0x35 |
| 0x62 | Tankentlueftungsventil Endstufe | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x65 | ueberwachung Momentenvergleich Ebene 2 | 0x0A | 0x1A | 0x20 | 0x21 |
| 0x66 | Schnittstelle MFL | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x67 | ueberwachung Rechnerfunktion | 0x0A | 0x1A | 0x1F | 0x1E |
| 0x68 | Schalter Kupplung | 0x0A | 0x12 | 0x0B | 0x14 |
| 0x69 | RAM-Test fehlerhaft | 0x0A | 0x1A | 0x1F | 0x22 |
| 0x6A | Schalter Bremse | 0x0A | 0x12 | 0x0B | 0x14 |
| 0x6B | ROM-Test fehlerhaft | 0x0A | 0x1A | 0x1F | 0x22 |
| 0x6C | Reset von Rechnerueberwachung | 0x0A | 0x1A | 0x1F | 0x22 |
| 0x6D | Batteriespannung | 0x0A | 0x14 | 0x24 | 0x12 |
| 0x6E | Momentenbegrenzung Ebene 1 | 0x0A | 0x23 | 0x1A | 0x12 |
| 0x6F | Kurbelwellengeber | 0x0A | 0x12 | 0x24 | 0x14 |
| 0x70 | Bezugsmarkengeber | 0x0A | 0x12 | 0x24 | 0x14 |
| 0x71 | Nockenwellengeber | 0x0A | 0x12 | 0x24 | 0x14 |
| 0x72 | Nockenwellengeber Bank 2 | 0x0A | 0x12 | 0x24 | 0x14 |
| 0x73 | Heissfilmluftmassenmesser | 0x0A | 0x13 | 0x15 | 0x71 |
| 0x75 | DK-Potentiometer | 0x0A | 0x15 | 0x26 | 0x27 |
| 0x76 | Drosselklappenpoti 1 | 0x0A | 0x28 | 0x24 | 0x11 |
| 0x77 | Drosselklappenpoti 2 | 0x0A | 0x28 | 0x24 | 0x11 |
| 0x78 | Fahrzeuggeschwindigkeit | 0x0A | 0x1A | 0x70 | 0x14 |
| 0x79 | Radsensorfehler | 0x0A | 0x1A | 0x0B | 0x8C |
| 0x7A | Umgebungstemperatur | 0x12 | 0x13 | 0x24 | 0x14 |
| 0x7B | Motortemperatur | 0x25 | 0x13 | 0x24 | 0x72 |
| 0x7C | Ansauglufttemperatur | 0x0A | 0x12 | 0x24 | 0x73 |
| 0x7D | Temperaturfuehler Kuehleraustritt | 0x0A | 0x12 | 0x24 | 0x74 |
| 0x7F | Plausibilitaet TXU | 0x0A | 0x1A | 0x14 | 0x0B |
| 0x82 | DK Positionsueberwachung | 0x14 | 0x13 | 0x15 | 0x28 |
| 0x83 | DK-Steller Regelbereich | 0x14 | 0x13 | 0x15 | 0x28 |
| 0x84 | DK-Steller Ansteuerung | 0x14 | 0x12 | 0x15 | 0x28 |
| 0x85 | Federpruefung DK-Steller | 0x14 | 0x13 | 0x15 | 0x64 |
| 0x86 | Pruefung unterer Anschlag | 0x14 | 0x13 | 0x26 | 0x65 |
| 0x87 | DK-Steller Fehler bei Verstaerkerabgl. | 0x14 | 0x13 | 0x26 | 0x65 |
| 0x88 | Pruefung Notluftpunkt | 0x14 | 0x13 | 0x64 | 0x76 |
| 0x8B | Thermostat klemmt | 0x0A | 0x12 | 0x13 | 0x74 |
| 0x8C | Endstufe Thermostat Kennfeldkuehlung | 0x0A | 0x12 | 0x13 | 0x14 |
| 0x8D | Endstufe Motorluefter | 0x0A | 0x12 | 0x14 | 0x6B |
| 0x8E | Endstufe Abgasklappe | 0x0A | 0x12 | 0x14 | 0x0B |
| 0x94 | EWS3.3 Schnittstelle DME-EWS | 0x0A | 0x12 | 0x14 | 0x8C |
| 0x96 | EV1 von Zyl. 1 | 0x0A | 0x12 | 0x14 | 0x05 |
| 0x97 | EV2 von Zyl. 5 | 0x0A | 0x12 | 0x14 | 0x07 |
| 0x98 | EV3 von Zyl. 4 | 0x0A | 0x12 | 0x14 | 0x05 |
| 0x99 | EV4 von Zyl. 8 | 0x0A | 0x12 | 0x14 | 0x07 |
| 0x9A | EV5 von Zyl. 6 | 0x0A | 0x12 | 0x14 | 0x07 |
| 0x9B | EV6 von Zyl. 3 | 0x0A | 0x12 | 0x14 | 0x05 |
| 0x9C | EV7 von Zyl. 7 | 0x0A | 0x12 | 0x14 | 0x07 |
| 0x9D | EV8 von Zyl. 2 | 0x0A | 0x12 | 0x14 | 0x05 |
| 0xA3 | Diagnose DK/HFM-Abgleich | 0x11 | 0x15 | 0x13 | 0x35 |
| 0xA4 | Drucksensor Umgebung | 0x0A | 0x0B | 0x24 | 0x75 |
| 0xA5 | Endstufe VANOS | 0x0A | 0x12 | 0x14 | 0x6C |
| 0xA6 | Endstufe VANOS Bank 2 | 0x0A | 0x12 | 0x14 | 0x6D |
| 0xA7 | Endstufe Kraftstoffpumpen-Relais | 0x0A | 0x12 | 0x14 | 0x0B |
| 0xA8 | Endstufe MIL | 0x0A | 0x12 | 0x14 | 0x0B |
| 0xAA | Endstufe Klimakompressorfreigabe zum Klima-SG | 0x0A | 0x12 | 0x14 | 0x0B |
| 0xB7 | LDP Diagnose | 0x0A | 0x35 | 0x24 | 0x14 |
| 0xB8 | LDP System | 0x0A | 0x35 | 0x24 | 0x14 |
| 0xB9 | LDP Modul | 0x0A | 0x35 | 0x24 | 0x14 |
| 0xBA | DM-TL Pumpenmotor Endstufe | 0x0A | 0x14 | 0x24 | 0x0B |
| 0xBB | DM-TL Kleinstleck (0,5mm) | 0x96 | 0x97 | 0x98 | 0x9A |
| 0xBC | DM-TL Feinleck (1,0mm) | 0x96 | 0x97 | 0x98 | 0x9A |
| 0xBD | DM-TL Modul | 0x98 | 0x96 | 0x97 | 0x99 |
| 0xC9 | DM-TL Heizung | 0x0A | 0x14 | 0x24 | 0x0B |
| 0xCC | EWS3.3 Wechselcode-Abspeicherung | 0x0A | 0x14 | 0x00 | 0x00 |
| 0xD2 | Klopfsensor1 | 0x0A | 0x1A | 0x14 | 0x13 |
| 0xD3 | Klopfsensor2 | 0x0A | 0x1A | 0x14 | 0x13 |
| 0xD4 | Klopfsensor3 | 0x0A | 0x1A | 0x14 | 0x13 |
| 0xD5 | Klopfsensor4 | 0x0A | 0x1A | 0x14 | 0x13 |
| 0xD6 | Klopfregelung Nulltest | 0x0A | 0x1A | 0x14 | 0x80 |
| 0xD7 | Klopfregelung Offset | 0x0A | 0x1A | 0x14 | 0x81 |
| 0xD8 | Klopfregelung Testimpuls | 0x0A | 0x1A | 0x77 | 0x81 |
| 0xDB | CAN-Timeout TCU | 0x0A | 0x1A | 0x14 | 0x8C |
| 0xDC | CAN-Timeout EGS | 0x0A | 0x1A | 0x14 | 0x8C |
| 0xDD | CAN-Timeout ASC/DSC | 0x0A | 0x1A | 0x14 | 0x8C |
| 0xDE | CAN-Timeout Instrumentenkombination | 0x0A | 0x1A | 0x14 | 0x8C |
| 0xDF | CAN-Timeout ACC | 0x0A | 0x1A | 0x14 | 0x8C |
| 0xE0 | Plausibilitaet MSR-Eingriff | 0x0A | 0x1A | 0x14 | 0x0B |
| 0xE1 | Plausibilitaet ACC-Eingriff | 0x0A | 0x1A | 0x14 | 0x0B |
| 0xE2 | Plausibilitaet Tankfuellstand | 0x0A | 0x3C | 0x14 | 0x0B |
| 0xE5 | Vergleich Versorgungen PWG | 0x00 | 0x00 | 0x1B | 0x1D |
| 0xE6 | Pedalwertgeber | 0x0A | 0x23 | 0x1B | 0x1D |
| 0xE7 | Pedalwertgeber Poti1 | 0x0A | 0x23 | 0x1B | 0x1D |
| 0xE8 | Pedalwertgeber Poti2 | 0x0A | 0x23 | 0x1B | 0x1D |
| 0xE9 | Startautomatik Endstufe | 0x0A | 0x12 | 0x14 | 0x0B |
| 0xEA | Startautomatik Eingang | 0x0A | 0x24 | 0x14 | 0x12 |
| 0xEC | Endstufe Ansaugklappe | 0x0A | 0x1A | 0x14 | 0x0B |
| 0xED | Startautomatik | 0x0A | 0x1A | 0x14 | 0x0B |
| 0xXY | unbekannter Fehlerort | 0x00 | 0x00 | 0x00 | 0x00 |

<a id="table-ftypmatrix"></a>
### FTYPMATRIX

Dimensions: 1 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY | 0xXY |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 133 rows × 49 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 | A9_0 | A9_1 | A10_0 | A10_1 | A11_0 | A11_1 | A12_0 | A12_1 | A13_0 | A13_1 | A14_0 | A14_1 | A15_0 | A15_1 | A16_0 | A16_1 | A17_0 | A17_1 | A18_0 | A18_1 | A19_0 | A19_1 | A20_0 | A20_1 | A21_0 | A21_1 | A22_0 | A22_1 | A23_0 | A23_1 | A24_0 | A24_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x00 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x01 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x02 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x03 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x04 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x3D | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x4C | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x05 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x3E | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x4C | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0A | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x02 | 0x00 | 0x7F | 0x00 | 0x81 | 0x00 | 0x49 | 0x00 | 0x06 | 0x00 | 0x80 | 0x00 | 0x82 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0C | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x02 | 0x00 | 0x7F | 0x00 | 0x83 | 0x00 | 0x49 | 0x00 | 0x06 | 0x00 | 0x80 | 0x00 | 0x84 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0D | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x3E | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x4D | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0E | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x3E | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x4D | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x0F | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x85 | 0x00 | 0x87 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x86 | 0x00 | 0x88 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x10 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x85 | 0x00 | 0x87 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x86 | 0x00 | 0x88 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x11 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x12 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x02 | 0x00 | 0x7F | 0x00 | 0x81 | 0x00 | 0x49 | 0x00 | 0x06 | 0x00 | 0x80 | 0x00 | 0x82 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x14 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x02 | 0x00 | 0x7F | 0x00 | 0x83 | 0x00 | 0x49 | 0x00 | 0x06 | 0x00 | 0x80 | 0x00 | 0x84 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x15 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x85 | 0x00 | 0x87 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x86 | 0x00 | 0x88 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x16 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x85 | 0x00 | 0x87 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x86 | 0x00 | 0x88 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x17 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x18 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3F | 0x00 | 0x40 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x4E | 0x00 | 0x4F | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x19 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3F | 0x00 | 0x40 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x4E | 0x00 | 0x4F | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1A | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3F | 0x00 | 0x40 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x4E | 0x00 | 0x4F | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1B | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3F | 0x00 | 0x40 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x4E | 0x00 | 0x4F | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1C | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3F | 0x00 | 0x40 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x4E | 0x00 | 0x4F | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1D | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3F | 0x00 | 0x40 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x4E | 0x00 | 0x4F | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1E | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x1F | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x20 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x89 | 0x00 | 0x8B | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x8A | 0x00 | 0x8C | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x21 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x29 | 0x00 | 0x2B | 0x00 | 0x2A | 0x00 | 0x05 | 0x00 | 0x2C | 0x00 | 0x2E | 0x00 | 0x2D | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x22 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x29 | 0x00 | 0x2B | 0x00 | 0x2A | 0x00 | 0x05 | 0x00 | 0x2C | 0x00 | 0x2E | 0x00 | 0x2D | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x27 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x1F | 0x00 | 0x1C | 0x00 | 0x1E | 0x00 | 0x1D | 0x00 | 0x28 | 0x00 | 0x25 | 0x00 | 0x27 | 0x00 | 0x26 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x28 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x2D | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x32 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x31 | 0x00 | 0x30 | 0x00 | 0x03 | 0x00 | 0x2F | 0x00 | 0x34 | 0x00 | 0x33 | 0x00 | 0x07 | 0x00 | 0x32 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x33 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x31 | 0x00 | 0x30 | 0x00 | 0x03 | 0x00 | 0x2F | 0x00 | 0x34 | 0x00 | 0x33 | 0x00 | 0x07 | 0x00 | 0x32 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x34 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x31 | 0x00 | 0x30 | 0x00 | 0x03 | 0x00 | 0x2F | 0x00 | 0x34 | 0x00 | 0x33 | 0x00 | 0x07 | 0x00 | 0x32 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x35 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x31 | 0x00 | 0x30 | 0x00 | 0x03 | 0x00 | 0x2F | 0x00 | 0x34 | 0x00 | 0x33 | 0x00 | 0x07 | 0x00 | 0x32 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x36 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x31 | 0x00 | 0x30 | 0x00 | 0x03 | 0x00 | 0x2F | 0x00 | 0x34 | 0x00 | 0x33 | 0x00 | 0x07 | 0x00 | 0x32 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x37 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x31 | 0x00 | 0x30 | 0x00 | 0x03 | 0x00 | 0x2F | 0x00 | 0x34 | 0x00 | 0x33 | 0x00 | 0x07 | 0x00 | 0x32 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x38 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x31 | 0x00 | 0x30 | 0x00 | 0x03 | 0x00 | 0x2F | 0x00 | 0x34 | 0x00 | 0x33 | 0x00 | 0x07 | 0x00 | 0x32 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x39 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x31 | 0x00 | 0x30 | 0x00 | 0x03 | 0x00 | 0x2F | 0x00 | 0x34 | 0x00 | 0x33 | 0x00 | 0x07 | 0x00 | 0x32 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x3E | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x31 | 0x00 | 0x30 | 0x00 | 0x03 | 0x00 | 0x2F | 0x00 | 0x34 | 0x00 | 0x33 | 0x00 | 0x07 | 0x00 | 0x32 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x50 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x51 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x52 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x73 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x74 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x54 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x55 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x5D | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x62 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x65 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x75 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x76 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x66 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x53 | 0x00 | 0x54 | 0x00 | 0x55 | 0x00 | 0x56 | 0x00 | 0x57 | 0x00 | 0x58 | 0x00 | 0x59 | 0x00 | 0x5A | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x67 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x77 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x78 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x68 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x69 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x79 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x7A | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x6A | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x5B | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x5C | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x6B | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x7B | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x7C | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x6C | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x7D | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x7E | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x6D | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x89 | 0x00 | 0x8B | 0x00 | 0x37 | 0x00 | 0x04 | 0x00 | 0x8A | 0x00 | 0x8C | 0x00 | 0x46 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x6E | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x6F | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x70 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x71 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x72 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x73 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x35 | 0x00 | 0x36 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x44 | 0x00 | 0x45 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x75 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x35 | 0x00 | 0x36 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x44 | 0x00 | 0x45 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x76 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x5D | 0x00 | 0x5E | 0x00 | 0x03 | 0x00 | 0x5F | 0x00 | 0x60 | 0x00 | 0x61 | 0x00 | 0x07 | 0x00 | 0x62 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x77 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x63 | 0x00 | 0x64 | 0x00 | 0x03 | 0x00 | 0x5F | 0x00 | 0x65 | 0x00 | 0x66 | 0x00 | 0x07 | 0x00 | 0x62 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x78 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x79 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x7A | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x8F | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x90 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x7B | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x41 | 0x00 | 0x42 | 0x00 | 0x03 | 0x00 | 0x43 | 0x00 | 0x50 | 0x00 | 0x51 | 0x00 | 0x07 | 0x00 | 0x52 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x7C | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x41 | 0x00 | 0x42 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x50 | 0x00 | 0x51 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x7D | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x41 | 0x00 | 0x42 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x50 | 0x00 | 0x51 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x7F | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x8D | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x8E | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x82 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x6B | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x6C | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x83 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x84 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x67 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x68 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x85 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x69 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x6A | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x86 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x6F | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x70 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x87 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x71 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x72 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x88 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x6D | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x6E | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x8B | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x8C | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x8D | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x8E | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x94 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x19 | 0x00 | 0x1B | 0x00 | 0x1A | 0x00 | 0x05 | 0x00 | 0x22 | 0x00 | 0x24 | 0x00 | 0x23 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x96 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x97 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x98 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x99 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x9A | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x9B | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x9C | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0x9D | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xA3 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xA4 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xA5 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xA6 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xA7 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xA8 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xAA | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xB7 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xB8 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x0F | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x10 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xB9 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x03 | 0x00 | 0x0B | 0x00 | 0x0C | 0x00 | 0x0D | 0x00 | 0x07 | 0x00 | 0x0E | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xBA | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xBB | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xBC | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x11 | 0x00 | 0x12 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x13 | 0x00 | 0x14 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xBD | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xC9 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xCC | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x17 | 0x00 | 0x18 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x20 | 0x00 | 0x21 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xD2 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x38 | 0x00 | 0x39 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x47 | 0x00 | 0x48 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xD3 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x38 | 0x00 | 0x39 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x47 | 0x00 | 0x48 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xD4 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x38 | 0x00 | 0x39 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x47 | 0x00 | 0x48 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xD5 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x38 | 0x00 | 0x39 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x47 | 0x00 | 0x48 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xD6 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xD7 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xD8 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xDC | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xDB | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xDD | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xDE | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xDF | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xE0 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xE1 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xE2 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xE5 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xE6 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xE7 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x63 | 0x00 | 0x64 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x65 | 0x00 | 0x66 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xE8 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x63 | 0x00 | 0x64 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x65 | 0x00 | 0x66 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xE9 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xEA | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xEC | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x3A | 0x00 | 0x3B | 0x00 | 0x3C | 0x00 | 0x04 | 0x00 | 0x49 | 0x00 | 0x4A | 0x00 | 0x4B | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xED | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |
| 0xXY | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x00 | 0x01 | 0x00 | 0x02 | 0x00 | 0x03 | 0x00 | 0x04 | 0x00 | 0x05 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xF9 | 0x00 | 0xFA | 0x00 | 0xFB | 0x00 | 0xFC | 0x00 | 0xFD | 0x00 | 0xFE | 0x00 | 0x00 | 0x00 | 0x00 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 153 rows × 2 columns

| BITNR | BITTEXT |
| --- | --- |
| 0x00 | --                                                                    |
| 0x01 | aktuell zu gross,  |
| 0x02 | aktuell zu klein,  |
| 0x03 | Signal fehlt aktuell,  |
| 0x04 | aktuell unplausibel,  |
| 0x05 | Initial zu gross,  |
| 0x06 | Initial zu klein,  |
| 0x07 | Signal fehlt Initial,  |
| 0x08 | Initial unplausibel,  |
| 0x09 | aktuell RS nicht geschlossen, |
| 0x0A | aktuell RS oeffnet nicht, |
| 0x0B | aktuell RS schliesst nicht, |
| 0x0C | RS nicht geschlossen Initial, |
| 0x0D | RS oeffnet nicht Initial, |
| 0x0E | RS schliesst nicht Initial, |
| 0x0F | aktuell verstopfte Leitung, |
| 0x10 | verstopfte Leitung Initial, |
| 0x11 | Grobleck erkannt aktuell, |
| 0x12 | Feinleck erkannt aktuell, |
| 0x13 | Grobleck erkannt Initial, |
| 0x14 | Feinleck erkannt Initial, |
| 0x15 | Endstufenfehler aktuell, |
| 0x16 | Endstufenfehler Initial, |
| 0x17 | WC-Ablage im EXRAM fehlerhaft aktuell, |
| 0x18 | Schreib-/Lesefehler im EEPROM aktuell, |
| 0x19 | Empfangsfehler ser. Schnittstelle (Paritybit) aktuell, |
| 0x1A | Empfangsfehler ser. Schnittstelle (Frame-/Stopbit) aktuell, |
| 0x1B | Timeout EWS-Telegramm (10sec nach Kl.15 ein) aktuell, |
| 0x1C | noch kein Startwert programmiert aktuell, |
| 0x1D | Manipulation ueber Wechselcode aktuell, |
| 0x1E | Manipulation ueber KWP200* aktuell, |
| 0x1F | Startwert zerstoert aktuell, |
| 0x20 | WC-Ablage im EXRAM fehlerhaft Initial, |
| 0x21 | Schreib-/Lesefehler im EEPROM Initial, |
| 0x22 | Empfangsfehler ser. Schnittstelle (Paritybit) Initial, |
| 0x23 | Empfangsfehler ser. Schnittstelle (Frame-/Stopbit) Initial, |
| 0x24 | Timeout EWS-Telegramm (10sec nach Kl.15 ein) Initial, |
| 0x25 | noch kein Startwert programmiert Initial, |
| 0x26 | Manipulation ueber Wechselcode Initial, |
| 0x27 | Manipulation ueber KWP200* Initial, |
| 0x28 | Startwert zerstoert Initial, |
| 0x29 | Adaptionswert Spaetanschlag nicht plausibel aktuell, |
| 0x2A | keine Regelaktivitaet bei Sollwinkel &lt;&gt;0 aktuell, |
| 0x2B | nicht korrekte Anzahl von NW-Flanken aktuell, |
| 0x2C | Adaptionswert Spaetanschlag nicht plausibel Initial, |
| 0x2D | keine Regelaktivitaet bei Sollwinkel &lt;&gt;0 Initial, |
| 0x2E | nicht korrekte Anzahl von NW-Flanken Initial, |
| 0x2F | Aussetzer nach Start aktuell, |
| 0x30 | Aussetzer waehrend der Fahrt aktuell, |
| 0x31 | katschaedigender Fehler aktuell, |
| 0x32 | Aussetzer nach Start Initial, |
| 0x33 | Aussetzer waehrend der Fahrt Initial, |
| 0x34 | katschaedigender Fehler Initial, |
| 0x35 | Spannungswert ueberschritten aktuell, |
| 0x36 | Spannungswert unterschritten aktuell, |
| 0x37 | Spannung kleiner 10V (1min nach Start) aktuell, |
| 0x38 | Spannungsamplitude zu hoch aktuell, |
| 0x39 | Spannungsamplitude zu gering aktuell, |
| 0x3A | Kurzschluss UBatt aktuell, |
| 0x3B | Kurzschluss Masse aktuell, |
| 0x3C | Signal-/Pfadunterbrechung aktuell, |
| 0x3D | Heizleistung zu hoch aktuell, |
| 0x3E | Heizleistung zu niedrig oder Unterbrechung aktuell, |
| 0x3F | Anfettungsgrenze erreicht aktuell, |
| 0x40 | Abmagerungsgrenze erreicht aktuell, |
| 0x41 | Temperatur sehr hoch oder Kurzschluss Masse aktuell, |
| 0x42 | Temperatur sehr niedrig oder Kurzschluss UBatt aktuell, |
| 0x43 | Toleranz zum Motortemperaturmodell zu gross aktuell, |
| 0x44 | Spannungswert ueberschritten Initial, |
| 0x45 | Spannungswert unterschritten Initial, |
| 0x46 | Spannung kleiner 10V (1min nach Start) Initial, |
| 0x47 | Spannungsamplitude zu hoch Initial, |
| 0x48 | Spannungsamplitude zu gering Initial, |
| 0x49 | Kurzschluss UBatt Initial, |
| 0x4A | Kurzschluss Masse Initial, |
| 0x4B | Signal-/Pfadunterbrechung Initial, |
| 0x4C | Heizleistung zu hoch Initial, |
| 0x4D | Heizleistung zu niedrig oder Unterbrechung Initial, |
| 0x4E | Anfettungsgrenze erreicht Initial, |
| 0x4F | Abmagerungsgrenze erreicht Initial, |
| 0x50 | Temperatur sehr hoch oder Kurzschluss Masse Initial, |
| 0x51 | Temperatur sehr niedrig oder Kurzschluss UBatt Initial, |
| 0x52 | Toleranz zum Motortemperaturmodell zu gross Initial, |
| 0x53 | Timeout MFL-Botschaft aktuell, |
| 0x54 | Togglebitfehler MFL-Botschaft aktuell, |
| 0x55 | Telegrammfrequenz fehlerhaft aktuell, |
| 0x56 | Bitfehler oder Tasten + und - gedrueckt aktuell, |
| 0x57 | Timeout MFL-Botschaft Initial, |
| 0x58 | Togglebitfehler MFL-Botschaft Initial, |
| 0x59 | Telegrammfrequenz fehlerhaft Initial, |
| 0x5A | Bitfehler oder Tasten + und - gedrueckt Initial, |
| 0x5B | Plausibilitaet BLS/BLTS fehlerhaft aktuell, |
| 0x5C | Plausibilitaet BLS/BLTS fehlerhaft Initial, |
| 0x5D | Signal zu gross oder Unterbrechung aktuell, |
| 0x5E | Signal zu klein aktuell, |
| 0x5F | Abweichung zwischen Poti 1 und 2 zu gross aktuell, |
| 0x60 | Signal zu gross oder Unterbrechung Initial, |
| 0x61 | Signal zu klein Initial, |
| 0x62 | Abweichung zwischen Poti 1 und 2 zu gross Initial, |
| 0x63 | Signal zu gross aktuell, |
| 0x64 | Signal zu klein oder Unterbrechung aktuell, |
| 0x65 | Signal zu gross Initial, |
| 0x66 | Signal zu klein oder Unterbrechung Initial, |
| 0x67 | DK-Ansteuerung fehlerhaft aktuell, |
| 0x68 | DK-Ansteuerung fehlerhaft Initial, |
| 0x69 | Federpruefung DK-Steller fehlerhaft aktuell, |
| 0x6A | Federpruefung DK-Steller fehlerhaft Initial, |
| 0x6B | Abweichung zw. DK Ist- und Sollposition zu gross aktuell, |
| 0x6C | Abweichung zw. DK Ist- und Sollposition zu gross Initial, |
| 0x6D | Pruefung Notluftpunkt fehlerhaft aktuell, |
| 0x6E | Pruefung Notluftpunkt fehlerhaft Initial, |
| 0x6F | Pruefung unterer Anschlag fehlerhaft aktuell, |
| 0x70 | Pruefung unterer Anschlag fehlerhaft Initial, |
| 0x71 | DK-Steller Verstaerkerabgleich fehlerhaft aktuell, |
| 0x72 | DK-Steller Verstaerkerabgleich fehlerhaft Initial, |
| 0x73 | Ventil klemmt aktuell, |
| 0x74 | Ventil klemmt Initial, |
| 0x75 | ueberschreitung Sollmoment aktuell, |
| 0x76 | ueberschreitung Sollmoment Initial, |
| 0x77 | ueberwachung Rechnerfunktion hat Fehler erkannt aktuell, |
| 0x78 | ueberwachung Rechnerfunktion hat Fehler erkannt Initial, |
| 0x79 | RAM-Test fehlerhaft aktuell, |
| 0x7A | RAM-Test fehlerhaft Initial, |
| 0x7B | ROM-Test fehlerhaft aktuell, |
| 0x7C | ROM-Test fehlerhaft Initial, |
| 0x7D | Reset von Rechnerueberwachung ausgeloest aktuell, |
| 0x7E | Reset von Rechnerueberwachung ausgeloest Initial, |
| 0x7F | Kabelbruch aktuell, |
| 0x80 | Kabelbruch Initial, |
| 0x81 | Adernschluss o. def. Sonde m. begr. Spannungshub aktuell, |
| 0x82 | Adernschluss o. def. Sonde m. begr. Spannungshub Initial, |
| 0x83 | Adernschluss aktuell, |
| 0x84 | Adernschluss Initial, |
| 0x85 | Maximumueberschreitung - Sonde tauschen aktuell, |
| 0x86 | Maximumueberschreitung - Sonde tauschen Initial, |
| 0x87 | Minimumueberschreitung - Sonde tauschen aktuell, |
| 0x88 | Minimumueberschreitung - Sonde tauschen Initial, |
| 0x89 | Maximalwert ueberschritten aktuell, |
| 0x8A | Maximalwert ueberschritten Initial, |
| 0x8B | Minimalwert unterschritten aktuell, |
| 0x8C | Minimalwert unterschritten Initial, |
| 0x8D | CAN-Signal ungueltig aktuell, |
| 0x8E | CAN-Signal ungueltig Initial, |
| 0x8F | Fehlerwert empfangen aktuell, |
| 0x90 | Fehlerwert empfangen Initial, |
| 0xF1 | Fehler momentan vorhanden   |
| 0xF2 | Fehler geprueft             |
| 0xF9 | E-Flag entprellt            |
| 0xFA | CARB-entprellt              |
| 0xFB | SCATT-aktiv                 |
| 0xFC | MIL ein                     |
| 0xFD | MIL blink                   |
| 0xFE | Fehler sporadisch           |

<a id="table-ftyptexte"></a>
### FTYPTEXTE

Dimensions: 7 rows × 2 columns

| BITNR | BITTEXT |
| --- | --- |
| 0x00 | --                                                                    |
| 0x21 | Regelung AUS, Einschaltbedingung noch nicht erfuellt |
| 0x22 | Regelung EIN                                       |
| 0x23 | Regelung AUS wegen Fahrbedingung                   |
| 0x24 | Regelung AUS wegen erkanntem Fehler                |
| 0x25 | Regelung EIN mit Einschraenkung                     |
| 0xFF | ??                          |

<a id="table-stagedmtl"></a>
### STAGEDMTL

Dimensions: 17 rows × 2 columns

| STAGE | TEXT |
| --- | --- |
| 0x00 | Funktion laeuft |
| 0x01 | Referenzleckmessung laeuft |
| 0x02 | Grobleckpruefung laeuft |
| 0x03 | Feinstleckpruefung laeuft |
| 0x04 | Referenzleckmessung 2 laeuft |
| 0x05 | Funktion nicht aktiv |
| 0x06 | Funktion beendet |
| 0x0A | Funktion kann nicht gestartet werden |
| 0x0B | Fkt. Abbruch :Ubatt ausserhalb Bereich |
| 0x0C | Fkt. Abbruch :Schwankung Ref.strom zu gross |
| 0x0D | Fkt. Abbruch :Elekt. Fehler liegen vor |
| 0x0E | Fkt. Abbruch :max. Diagnosedauer erreicht |
| 0x14 | Funktion wurde abgebrochen |
| 0x15 | Abbruch :Betankung erkannt |
| 0x16 | Abbruch :Tankdeckel geoeffnet |
| 0x17 | Abbruch :Ubatt-Schwankung zu gross |
| 0x18 | Abbruch :Bedingung Kl.15 AUS/EIN erkannt |

<a id="table-stagedmtlfreeze"></a>
### STAGEDMTLFREEZE

Dimensions: 23 rows × 2 columns

| STAGE | TEXT |
| --- | --- |
| 0x00 | Funktion laeuft |
| 0x01 | Referenzleckmessung |
| 0x02 | Grobleckpruefung |
| 0x03 | Feinstleckpruefung |
| 0x04 | Referenzleckmessung 2 |
| 0x05 | Funktion nicht aktiv |
| 0x06 | Funktion beendet |
| 0x0A | Funktion kann nicht gestartet werden |
| 0x0B | Fkt. Abbruch :Ubatt ausserhalb Bereich |
| 0x0C | Fkt. Abbruch :Schwankung Ref.strom zu gross |
| 0x0D | Fkt. Abbruch :Elekt. Fehler liegen vor |
| 0x0E | Fkt. Abbruch :max. Diagnosedauer erreicht |
| 0x0F | Fkt. Abbruch :keine Grobleckfreigabe |
| 0x14 | Funktion wurde abgebrochen |
| 0x15 | Abbruch :Betankung erkannt |
| 0x16 | Abbruch :Tankdeckel geoeffnet |
| 0x17 | Abbruch :Ubatt-Schwankung zu gross |
| 0x18 | Abbruch :Bedingung Kl.15 AUS/EIN erkannt |
| 0x1E | Fkt. beendet, Dicht erkannt |
| 0x1F | Fkt. beendet, Feinleck erkannt |
| 0x20 | Fkt. beendet, Grobleck erkannt |
| 0x21 | Fkt. beendet, Modulfehler erkannt |
| 0x22 | Fkt. beendet, kein Grobleck erkannt |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 118 rows × 6 columns

| UWNR | UWTEXT | UW_EINH | UWF_A | UWF_B | UWF_C |
| --- | --- | --- | --- | --- | --- |
| 0x00 | ---                                    |   | 0 | 0 | 0 |
| 0x01 | Regelstatus Bank1                  |   | 0 | 0 | 0 |
| 0x02 | Regelstatus Bank2                  |   | 0 | 0 | 0 |
| 0x03 | Berechnete Last                    | % | 0.3906 | 0 | 0 |
| 0x04 | Motortemperatur                      | Grd C | 1 | -40 | 0 |
| 0x05 | Regelfaktor Bank1                  |    | 0.0078 | 0 | 0 |
| 0x06 | Adaptionsfaktor Bank1              |    | 0.0078 | 0 | 0 |
| 0x07 | Regelfaktor Bank2                  |    | 0.0078 | 0 | 0 |
| 0x08 | Adaptionsfaktor Bank2              |    | 0.0078 | 0 | 0 |
| 0x09 | ---                                    |    | 0 | 0 | 0 |
| 0x0A | Motordrehzahl                        | /min | 40 | 0 | 0 |
| 0x0B | Fahrzeuggeschwindigkeit              | km/h | 1 | 0 | 0 |
| 0x0C | ---                                    |    | 0 | 0 | 0 |
| 0x0D | ---                                    |    | 0 | 0 | 0 |
| 0x0E | ---                                    |    | 0 | 0 | 0 |
| 0x0F | ---                                    |    | 0 | 0 | 0 |
| 0x10 | ---                                    |    | 0 | 0 | 0 |
| 0x11 | Luftmassenfluss                      | kg/h | 4 | 0 | 0 |
| 0x12 | Motortemperatur                      | Grd C | 0.75 | -48 | 0 |
| 0x13 | Ansauglufttemperatur                 | Grd C | 0.75 | -48 | 0 |
| 0x14 | Versorgungsspannung                  | V | 0.0942 | 0 | 0 |
| 0x15 | Winkel DK bez. auf DK-Anschl.    | % DK | 0.3922 | 0 | 0 |
| 0x16 | Sondenspannung v. Kat Bank1        | V | 0.00522 | -0.2 | 0 |
| 0x17 | Sondenspannung h. Kat Bank1        | V | 0.00522 | -0.2 | 0 |
| 0x18 | Sondenspannung v. Kat Bank2        | V | 0.00522 | -0.2 | 0 |
| 0x19 | Sondenspannung h. Kat Bank2        | V | 0.00522 | -0.2 | 0 |
| 0x1A | relative Luftfuellung (rl)         | % | 0.75 | 0 | 0 |
| 0x1B | Spannung PWG Poti 1                | V | 0.0195 | 0 | 0 |
| 0x1C | Spannung PWG Poti 2                | V | 0.0195 | 0 | 0 |
| 0x1D | verdoppelte Spannung PWG 2         | V | 0.0195 | 0 | 0 |
| 0x1E | skapfad                              | bin | 1 | 0 | 0 |
| 0x1F | egaspfad                             | bin | 1 | 0 | 0 |
| 0x20 | mpfad                                | bin | 1 | 0 | 0 |
| 0x21 | mi_duf                               | % | 0.3906 | 0 | 0 |
| 0x22 | rstpfad                              | bin | 1 | 0 | 0 |
| 0x23 | normierter Fahrpedalwinkel         | % | 0.3922 | 0 | 0 |
| 0x24 | Umgebungstemperatur                  | Grd C | 0.75 | -48 | 0 |
| 0x25 | Motortemp.-Ersatzwert aus Modell   | Grd C | 0.75 | -48 | 0 |
| 0x26 | Spannung DK-Poti 1                 | V | 0.0195 | 0 | 0 |
| 0x27 | Spannung DK-Poti 2                 | V | 0.0195 | 0 | 0 |
| 0x28 | Sollwert DK bez. auf unteren Anschl. | % | 0.3906 | 0 | 0 |
| 0x29 | Abgastemp. v. Kat aus Modell     | Grd C | 5 | -50 | 0 |
| 0x2A | Abgastemp. Bank2 v. Kat aus Modell   | Grd C | 5 | -50 | 0 |
| 0x2B | Kat-Temperatur aus Modell          | Grd C | 5 | -50 | 0 |
| 0x2C | Kat-Temperatur Bank 2 aus Modell | Grd C | 5 | -50 | 0 |
| 0x2D | uhsv                                 | V | 0.0195 | 0 | 0 |
| 0x2E | uhsv2                                | V | 0.0195 | 0 | 0 |
| 0x2F | uhsh                                 | V | 0.0195 | 0 | 0 |
| 0x30 | uhsh2                                | V | 0.0195 | 0 | 0 |
| 0x31 | rinv                                 | Ohm | 64 | 0 | 0 |
| 0x32 | rinv2                                | Ohm | 64 | 0 | 0 |
| 0x33 | rinh                                 | Ohm | 64 | 0 | 0 |
| 0x34 | rinh2                                | Ohm | 64 | 0 | 0 |
| 0x35 | Umgebungsdruck                       | hPa | 5 | 0 | 0 |
| 0x36 | tpsvkmf                              | s | 0.04 | 0 | 0 |
| 0x37 | tpsvkmf2                             | s | 0.04 | 0 | 0 |
| 0x38 | fr                                   |    | 0.0078 | 0 | 0 |
| 0x39 | fra                                  |    | 0.0078 | 0 | 0 |
| 0x3A | fr2                                  |    | 0.0078 | 0 | 0 |
| 0x3B | fra2                                 |    | 0.0078 | 0 | 0 |
| 0x3C | Tankfuellstand                       | l | 1.0 | 0 | 0 |
| 0x3D | rl                                   | % | 0.75 | 0 | 0 |
| 0x64 | wdknlp                               | % | 0.3922 | 0 | 0 |
| 0x65 | udkp1a_u                             | V | 0.0195 | 0 | 0 |
| 0x66 | igokr_u                              | V/s | 23.844 | 0 | 1 |
| 0x67 | uusvk_u                              | V | 0.0195 | 0 | 0 |
| 0x68 | uusvk2_u                             | V | 0.0195 | 0 | 0 |
| 0x69 | uushk_u                              | V | 0.0195 | 0 | 0 |
| 0x6A | uushk2_u                             | V | 0.0195 | 0 | 0 |
| 0x6B | taml                                 | % | 0.3922 | 0 | 0 |
| 0x6C | wnwi1_u                              | Grad KW | 1 | 0 | 1 |
| 0x6D | wnwi2_u                              | Grad KW | 1 | 0 | 1 |
| 0x6E | tanwrhf_0_A                          | % TV | 0.3922 | 0 | 0 |
| 0x6F | tanwrhf_1_A                          | % TV | 0.3922 | 0 | 0 |
| 0x70 | vfzg2                                | km/h | 1.25 | 0 | 0 |
| 0x71 | ADC HFM                              | V | 0.0196 | 0 | 0 |
| 0x72 | ADC TM                               | V | 0.0196 | 0 | 0 |
| 0x73 | ADC TA                               | V | 0.0196 | 0 | 0 |
| 0x74 | ADC TKA                              | V | 0.0196 | 0 | 0 |
| 0x75 | ADC DSU                              | V | 0.0196 | 0 | 0 |
| 0x76 | Sollwert DK-Winkel in NLP-Stellung   | % DK | 0.3921 | 0 | 0 |
| 0x77 | ikrmet                               | V | 0.0196 | 0 | 0 |
| 0x78 | tkatmf                               | Grd C | 5 | -50 | 0 |
| 0x79 | tkatmf2                              | Grd C | 5 | -50 | 0 |
| 0x7A | tabgmf                               | Grd C | 5 | -50 | 0 |
| 0x7B | tabgmf2                              | Grd C | 5 | -50 | 0 |
| 0x7C | phlsnv                               |   | 0.01 | 0 | 0 |
| 0x7D | phlsnv2                              |   | 0.01 | 0 | 0 |
| 0x7E | phlsnh                               |   | 0.01 | 0 | 0 |
| 0x7F | phlsnh2                              |   | 0.01 | 0 | 0 |
| 0x80 | igod                                 | V/s | 23.844 | 0 | 1 |
| 0x81 | ikrma                                | V | 0.0196 | 0 | 0 |
| 0x82 | lamsons                              |   | 0.0625 | 0 | 0 |
| 0x83 | lamsons2                             |   | 0.0625 | 0 | 0 |
| 0x84 | tmst                                 | Grd C | 0.75 | -48 | 0 |
| 0x85 | frm                                  |   | 0.0078 | 0 | 0 |
| 0x86 | frm2                                 |   | 0.0078 | 0 | 0 |
| 0x87 | Mittelwert Sonde h. Kat (ahkat)  |   | 0.0039 | 0 | 0 |
| 0x88 | Mittelwert Sonde h.Kat Bank2(ahkat2) |   | 0.0039 | 0 | 0 |
| 0x89 | I-Anteil verz. Reglerumsch.(tvlrhi)  | s | 0.01 | 0 | 1 |
| 0x8A | I-Anteil verz. Reglerumsch.(tvlrhi2) | s | 0.01 | 0 | 1 |
| 0x8B | Fakt. Luftdichte TANS Hoehe (frhol_u) |   | 0.0078 | 0 | 0 |
| 0x8C | Zeit nach Start (tnse_u)             | s | 25.6 | 0 | 0 |
| 0x8D | norm. Referenzpegel KR SW-Zyl.0      | V | 0.625 | 0 | 0 |
| 0x8E | norm. Referenzpegel KR SW-Zyl.1      | V | 0.625 | 0 | 0 |
| 0x8F | norm. Referenzpegel KR SW-Zyl.2      | V | 0.625 | 0 | 0 |
| 0x90 | norm. Referenzpegel KR SW-Zyl.3      | V | 0.625 | 0 | 0 |
| 0x91 | norm. Referenzpegel KR SW-Zyl.4      | V | 0.625 | 0 | 0 |
| 0x92 | norm. Referenzpegel KR SW-Zyl.5      | V | 0.625 | 0 | 0 |
| 0x93 | norm. Referenzpegel KR SW-Zyl.6      | V | 0.625 | 0 | 0 |
| 0x94 | norm. Referenzpegel KR SW-Zyl.7      | V | 0.625 | 0 | 0 |
| 0x95 | Statusflag ti-Abschaltung            | -- | 1 | 0 | 0 |
| 0x96 | Fuellstand Kraftstofftank            | l | 1 | 0 | 0 |
| 0x97 | Pumpenstrom Referenzleck             | mA | 0.1953 | 0 | 0 |
| 0x98 | aktuelle Zeit Leckmessung            | s | 1.6 | 0 | 0 |
| 0x99 | Pumpenstrom bei DM-TL Ventilpruefung | mA | 0.1953 | 0 | 0 |
| 0x9A | Differenz Pumpenstrom                | mA | 0.1953 | 0 | 0 |
| 0xXY | unbekannte Umweltbedingung           | -- | 1 | 0 | 0 |

<a id="table-fehlercodes"></a>
### FEHLERCODES

Dimensions: 30 rows × 2 columns

| CODE | FEHLERTEXT |
| --- | --- |
| 0x00 | ---                                          |
| 0x10 | generalReject                                |
| 0x11 | ServiceNotSupported                          |
| 0x12 | subFunctionNotSupported-invalidFormat        |
| 0x21 | busy-repeatRequest                           |
| 0x22 | conditionsNotCorrectOrRequestSequenceError   |
| 0x23 | routineNotComplete                           |
| 0x31 | requestOutOfRange                            |
| 0x33 | SecurityAccessDenied-securityAccessRequested |
| 0x35 | invalidKey                                   |
| 0x36 | exeedNumberOfAttempts                        |
| 0x37 | requiredTimeDelayNotExpired                  |
| 0x40 | downloadNotAccepted                          |
| 0x41 | improperDownloadType                         |
| 0x42 | canNotDownloadToSpecifiedAddress             |
| 0x43 | canNotDownloadNumberOfBytesRequested         |
| 0x50 | uploadNotAccepted                            |
| 0x51 | improperUploadType                           |
| 0x52 | canNotUploadFromSpecifiedAddress             |
| 0x53 | canNotUploadNumberOfBytesRequested           |
| 0x71 | tranferSuspended                             |
| 0x72 | tranferAborted                               |
| 0x74 | illegalAddressInBlockTransfer                |
| 0x75 | illegalByteCountInBlockTransfer              |
| 0x76 | illegalBlockTransferType                     |
| 0x77 | blockTransferDataChecksumError               |
| 0x78 | requestCorrectlyReceived-ResponsePending     |
| 0x79 | incorrectByteCountDuringBlockransfer         |
| 0x80 | serviceNotSupportedInActiveDiagnosticMode    |
| 0xXY | unbekannter Rueckgabewert (ResponseCode)  |

<a id="table-stagepointer"></a>
### STAGEPOINTER

Dimensions: 20 rows × 2 columns

| STAGE | TEXT |
| --- | --- |
| 0x00 | S0      :    Close to Close Check |
| 0x01 | S1      :    Close to Open Check |
| 0x02 | S2      :    Open to Close Check |
| 0x03 | S3      :    Clambed Tube Check |
| 0x04 | S4      :    Fast-Puls (Druckaufbau) |
| 0x05 | S5      :    Natural-Frequency (Druckstabilisierung) |
| 0x06 | S6_1    :    Entscheidung kein Leck oder vermutlich Leck |
| 0x07 | S6_2    :    Ansteuerung wie fuer CTO Check |
| 0x08 | S6_3    :    Periodendauermessung |
| 0x09 | Auswertung : Entscheidung ob Grob- oder Feinleck |
| 0x0A | Abbruch    : uebergang zum Idle Zustand |
| 0x0B | Idle    :    Funktion nicht aktiv |
| 0x0C | Wartezustand TANS-Monitor nach Fehlererkennung in S0 |
| 0x0D | Wartezustand TANS-Monitor nach Fehlererkennung in S1 |
| 0x0E | Wartezustand TANS-Monitor nach Fehlererkennung in S2 |
| 0x0F | Wartezustand TANS-Monitor nach Fehlererkennung in S3 |
| 0x10 | Wartezustand TANS-Monitor nach Fehlererkennung CTO in S5 und S6_2 |
| 0x11 | Wartezustand TANS-Monitor nach Fehlererkennung Grobleck aus Auswertung |
| 0x12 | Wartezustand TANS-Monitor nach Fehlererkennung Feinleck aus Auswertung |
| 0xXY | Stagepointer wird noch nicht ausgegeben |

<a id="table-tevstatus"></a>
### TEVSTATUS

Dimensions: 5 rows × 2 columns

| STATI | TEXT |
| --- | --- |
| 0x00 | Systemtest TEV laeuft |
| 0x01 | Systemtest kann nicht gestartet werden |
| 0x05 | Systemtest ist nicht gestartet |
| 0x06 | Systemtest TEV ist beendet |
| 0xXY | Status Systemtest TEV kann nicht ausgegeben werden |

<a id="table-mfl-bits"></a>
### MFL_BITS

Dimensions: 7 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| S_L_FGR | 0 | 0x40 | 0x40 |
| S_B_FGRTVE | 0 | 0x10 | 0x10 |
| S_B_FGRHSA | 0 | 0x02 | 0x02 |
| S_B_FGRTSE | 0 | 0x08 | 0x08 |
| S_B_FGRAT | 0 | 0x01 | 0x01 |
| S_B_FGRTWA | 0 | 0x20 | 0x20 |
| S_B_FGRTBE | 0 | 0x04 | 0x04 |

<a id="table-sonde-bits"></a>
### SONDE_BITS

Dimensions: 8 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| S_B_SBBHK | 0 | 0x08 | 0x08 |
| S_B_HSHE2 | 1 | 0x40 | 0x40 |
| S_B_SBBVK2 | 0 | 0x10 | 0x10 |
| S_B_HSVE | 1 | 0x20 | 0x20 |
| S_B_HSVE2 | 1 | 0x10 | 0x10 |
| S_B_HSHE | 1 | 0x80 | 0x80 |
| S_B_SBBVK | 0 | 0x20 | 0x20 |
| S_B_SBBHK2 | 0 | 0x04 | 0x04 |

<a id="table-ll-bits"></a>
### LL_BITS

Dimensions: 5 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| S_B_FHZ | 0 | 0x40 | 0x40 |
| S_B_NSUB | 0 | 0x04 | 0x04 |
| S_B_NFTEV | 0 | 0x20 | 0x20 |
| S_B_NAC | 0 | 0x80 | 0x80 |
| S_B_DKPU | 0 | 0x10 | 0x10 |

<a id="table-abgas-bits"></a>
### ABGAS_BITS

Dimensions: 5 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| S_B_CDLSV | 0 | 0x20 | 0x20 |
| S_B_CDAGR | 0 | 0x80 | 0x80 |
| S_B_CDSLS | 0 | 0x04 | 0x02 |
| S_B_CDHSV | 0 | 0x40 | 0x40 |
| S_B_CDTES | 0 | 0x04 | 0x04 |

<a id="table-check-bits"></a>
### CHECK_BITS

Dimensions: 6 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| S_B_HSRDY | 0 | 0x40 | 0x40 |
| S_B_TESRDY | 0 | 0x04 | 0x04 |
| S_B_SLSRDY | 0 | 0x08 | 0x08 |
| S_B_LSRDY | 0 | 0x20 | 0x20 |
| S_B_KATRDY | 0 | 0x01 | 0x01 |
| S_B_AGRRDY | 0 | 0x80 | 0x80 |

<a id="table-teile-bits"></a>
### TEILE_BITS

Dimensions: 20 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| S_B_UMAERF | 0 | 0x80 | 0x80 |
| S_B_EWS_OK | 0 | 0x10 | 0x10 |
| S_B_SLP | 2 | 0x04 | 0x04 |
| S_B_STA | 3 | 0x80 | 0x80 |
| S_B_EBL | 3 | 0x10 | 0x10 |
| S_B_KUPPL | 4 | 0x04 | 0x04 |
| S_B_BLS | 4 | 0x08 | 0x08 |
| S_B_BRS | 4 | 0x10 | 0x10 |
| S_B_KO | 4 | 0x80 | 0x80 |
| S_B_KOE | 2 | 0x04 | 0x04 |
| S_B_EKP | 3 | 0x10 | 0x10 |
| S_B_KL15 | 4 | 0x01 | 0x01 |
| S_B_LR | 1 | 0x80 | 0x80 |
| S_B_LR2 | 1 | 0x40 | 0x40 |
| S_B_VL | 1 | 0x02 | 0x02 |
| S_B_LL | 1 | 0x01 | 0x01 |
| S_B_SLV | 2 | 0x02 | 0x02 |
| S_B_ETR | 3 | 0x40 | 0x40 |
| S_S_LDPR | 4 | 0x10 | 0x10 |
| S_B_LDPEIN | 2 | 0x01 | 0x01 |

<a id="table-pkw-bits"></a>
### PKW_BITS

Dimensions: 4 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| S_B_ASC_PKW | 0 | 0x08 | 0x08 |
| S_B_ACC | 0 | 0x04 | 0x04 |
| S_B_AUTGET | 0 | 0x02 | 0x02 |
| S_B_NOKATFZG | 0 | 0x01 | 0x01 |
