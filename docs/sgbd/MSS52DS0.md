# MSS52DS0.prg

- Jobs: [203](#jobs)
- Tables: [13](#tables)

## INFO

| Field | Value |
| --- | --- |
| ECU | MSS52 fuer S52B32/S62B50 |
| ORIGIN | BMW TI-433 Dennert |
| REVISION | 1.08 |
| AUTHOR | BMW EE-32 Schaffert, BMW TP-421 Weber, BMW TI-433 Schiefer, BMW TI-433 Dennert |
| COMMENT | N/A |
| PACKAGE | N/A |
| SPRACHE | deutsch |

## Jobs

### Index

- [STEUERN_AVANOS1_SPAET_VENTIL](#job-steuern-avanos1-spaet-ventil) - Auslass-VANOS Bank 1 Spaetventil ansteuern
- [STEUERN_AVANOS2_SPAET_VENTIL](#job-steuern-avanos2-spaet-ventil) - Auslass-VANOS Bank 2 Spaetventil ansteuern
- [STEUERN_AVANOS1_FRUEH_VENTIL](#job-steuern-avanos1-frueh-ventil) - Auslass-VANOS Bank 1 Fruehventil ansteuern
- [STEUERN_AVANOS2_FRUEH_VENTIL](#job-steuern-avanos2-frueh-ventil) - Auslass-VANOS Bank 2 Fruehventil ansteuern
- [STEUERN_EVANOS1_SPAET_VENTIL](#job-steuern-evanos1-spaet-ventil) - Einlass-VANOS Bank 1 Spaetventil ansteuern
- [STEUERN_EVANOS2_SPAET_VENTIL](#job-steuern-evanos2-spaet-ventil) - Einlass-VANOS Bank 2 Spaetventil ansteuern
- [STEUERN_EVANOS1_FRUEH_VENTIL](#job-steuern-evanos1-frueh-ventil) - Einlass-VANOS Bank 1 Fruehventil ansteuern
- [STEUERN_EVANOS2_FRUEH_VENTIL](#job-steuern-evanos2-frueh-ventil) - Einlass-VANOS Bank 2 Fruehventil ansteuern
- [STEUERN_LSHV2](#job-steuern-lshv2) - Lambdasondenheizung vor Kat Bank 2 ansteuern
- [STEUERN_LSHN1](#job-steuern-lshn1) - Lambdasondenheizung nach Kat Bank 1 ansteuern
- [STEUERN_LSHN2](#job-steuern-lshn2) - Lambdasondenheizung nach Kat Bank 2 ansteuern
- [STEUERN_LSHV1](#job-steuern-lshv1) - Lambdasondenheizung vor Kat Bank 1 ansteuern
- [STEUERN_ZS8](#job-steuern-zs8) - Zuendspule Zyl. 8 ansteuern
- [STEUERN_ZS7](#job-steuern-zs7) - Zuendspule Zyl. 7 ansteuern
- [STEUERN_ZS6](#job-steuern-zs6) - Zuendspule Zyl. 6 ansteuern
- [STEUERN_ZS5](#job-steuern-zs5) - Zuendspule Zyl. 5 ansteuern
- [STEUERN_ZS4](#job-steuern-zs4) - Zuendspule Zyl. 4 ansteuern
- [STEUERN_ZS3](#job-steuern-zs3) - Zuendspule Zyl. 3 ansteuern
- [STEUERN_ZS2](#job-steuern-zs2) - Zuendspule Zyl. 2 ansteuern
- [STEUERN_ZS1](#job-steuern-zs1) - Zuendspule Zyl. 1 ansteuern
- [PRUEFSTEMPEL_LESEN](#job-pruefstempel-lesen) - Auslesen des Pruefstempels
- [PRUEFSTEMPEL_SCHREIBEN](#job-pruefstempel-schreiben) - Beschreiben des Pruefstempels Es muessen immer alle drei Argumente im Bereich von 0-255 bzw. 0x00-0xFF uebergeben werden.
- [STEUERN_EV8](#job-steuern-ev8) - Einspritzventil 8 ansteuern
- [STEUERN_EV7](#job-steuern-ev7) - Einspritzventil 7 ansteuern
- [STEUERN_EV6](#job-steuern-ev6) - Einspritzventil 6 ansteuern
- [STEUERN_EV5](#job-steuern-ev5) - Einspritzventil 5 ansteuern
- [STEUERN_EV4](#job-steuern-ev4) - Einspritzventil 4 ansteuern
- [STEUERN_EV3](#job-steuern-ev3) - Einspritzventil 3 ansteuern
- [STEUERN_EV2](#job-steuern-ev2) - Einspritzventil 2 ansteuern
- [STEUERN_EV1](#job-steuern-ev1) - Einspritzventil 1 ansteuern
- [STOP_SYSTEMCHECK_SEK_LUFT](#job-stop-systemcheck-sek-luft) - SLS Funktionstest Stop
- [START_SYSTEMCHECK_SEK_LUFT](#job-start-systemcheck-sek-luft) - Funktionsueberpruefung SLS anstossen - erwarte Ergebnis ausserhalb Job
- [LESEN_SYSTEMCHECK_SEK_LUFT](#job-lesen-systemcheck-sek-luft) - Ergebnis Funktionsueberpruefung SLS abrufen
- [STEUERN_E_LUEFTER](#job-steuern-e-luefter) - Elektroluefterrelais ansteuern
- [STEUERN_OEKV2](#job-steuern-oekv2) - Oelkreisumschaltventil 2 (links) ansteuern
- [STEUERN_OEKV1](#job-steuern-oekv1) - Oelkreisumschaltventil 1 (rechts) ansteuern
- [STEUERN_START](#job-steuern-start) - Startrelais ansteuern
- [STEUERN_EKP](#job-steuern-ekp) - Kraftstoffpumpenrelais ansteuern
- [STEUERN_SERVOV](#job-steuern-servov) - Servotronikventil ansteuern
- [STEUERN_TEV](#job-steuern-tev) - Tankentlueftungsventil ansteuern
- [STEUERN_AKL](#job-steuern-akl) - Abgasklappe ansteuern
- [STEUERN_VDSV](#job-steuern-vdsv) - VANOS-Druckspeicherventil ansteuern
- [STEUERN_SLV](#job-steuern-slv) - Sekundaerluftventil ansteuern
- [STEUERN_KO](#job-steuern-ko) - Klimakompressorrelais ansteuern
- [STEUERN_SLP](#job-steuern-slp) - Sekundaerluftpumpenrelais ansteuern
- [EDIC_RESET](#job-edic-reset) - EDIC-Reset
- [initialisierung](#job-initialisierung) - Default Init-Job
- [INFO](#job-info) - Information SGBD
- [FS_LESEN_TEXT](#job-fs-lesen-text) - Auslesen des Fehlerspeichers (nur die F.-Namen)
- [ISN_LESEN](#job-isn-lesen) - liefert fertig formatierte ISN fuer MSS50
- [RAM_LESEN](#job-ram-lesen) - Beliebige RAM - Zellen auslesen
- [ROM_LESEN](#job-rom-lesen) - Beliebige FLASH - Zellen auslesen
- [EEPROM_LESEN](#job-eeprom-lesen) - Beliebige EEPROM - Zellen auslesen
- [IDENT](#job-ident) - Ident-Daten fuer DME
- [ECU_CONFIG](#job-ecu-config) - Ident-Daten fuer DME
- [ABGAS_VARIANTE_LESEN](#job-abgas-variante-lesen) - Auslesen der Abgasvariante
- [EWS3_GET_STATUS](#job-ews3-get-status) - EWS3 Synchonisierungsstatus abfragen
- [EWS3_INITIALISIEREN](#job-ews3-initialisieren) - EWS3 initialisieren/abgleichen
- [EWS3_SYNC](#job-ews3-sync) - EWS3-Steuergeraet ruecksetzen
- [ADAPT_LOESCHEN](#job-adapt-loeschen) - alle Adaptionen gleichzeitig loeschen
- [ADAPT_SELEKTIV_LOESCHEN](#job-adapt-selektiv-loeschen) - Adaptionen bitweise loeschen und Zustaende bitweise setzen
- [STEUERN_LAMBDAREGLER_SPERREN](#job-steuern-lambdaregler-sperren) - LA-Regler ueber Adaptionstelegramm loeschen
- [STEUERN_LLS_TESTDREHZAHL](#job-steuern-lls-testdrehzahl) - feste Leerlaufanhebung fuer VANOS-Test
- [STATUS_CODIER_CHECKSUMME](#job-status-codier-checksumme) - Codier - Checksumme abfragen
- [AIF_LESEN](#job-aif-lesen) - Auslesen des Anwender-Info-Feldes
- [FS_QUICK_LESEN](#job-fs-quick-lesen) - Auslesen des QUICK Fehlerspeichers
- [FS_LESEN](#job-fs-lesen) - Auslesen des Fehlerspeichers
- [FS_LESEN_OLD](#job-fs-lesen-old) - Auslesen des Fehlerspeichers
- [FS_SHADOW_LESEN](#job-fs-shadow-lesen) - Auslesen des Fehlerspeichers
- [FS_LOESCHEN](#job-fs-loeschen) - Loeschen des Fehlerspeichers
- [STATUS_DIGITAL](#job-status-digital) - Status Schalteingaenge
- [STEUERN_AVANOS1](#job-steuern-avanos1) - AVANOS1 ansteuern
- [STEUERN_EVANOS1](#job-steuern-evanos1) - EVANOS1 ansteuern
- [STEUERN_EVANOS1_VERSTELLZEIT](#job-steuern-evanos1-verstellzeit) - Verstellzeitmessung EVANOS1 anstossen
- [STEUERN_AVANOS1_VERSTELLZEIT](#job-steuern-avanos1-verstellzeit) - Verstellzeitmessung AVANOS1 anstossen
- [STEUERN_EVANOS1_DICHTHEIT](#job-steuern-evanos1-dichtheit) - Dichtheitmessung EVANOS1 anstossen
- [STEUERN_AVANOS1_DICHTHEIT](#job-steuern-avanos1-dichtheit) - Dichtheitmessung AVANOS1 anstossen
- [STEUERN_EVANOS1_FRUEHANSCHLAG](#job-steuern-evanos1-fruehanschlag) - Fruehanschlag EVANOS1 anfahren
- [STEUERN_EVANOS1_SPAETANSCHLAG](#job-steuern-evanos1-spaetanschlag) - Spaetanschlag EVANOS1 anfahren
- [STEUERN_AVANOS1_FRUEHANSCHLAG](#job-steuern-avanos1-fruehanschlag) - Fruehanschlag AVANOS1 anfahren
- [STEUERN_AVANOS1_SPAETANSCHLAG](#job-steuern-avanos1-spaetanschlag) - Spaetanschlag AVANOS1 anfahren
- [STEUERN_AVANOS2](#job-steuern-avanos2) - AVANOS2 ansteuern
- [STEUERN_EVANOS2](#job-steuern-evanos2) - EVANOS2 ansteuern
- [STEUERN_EVANOS2_VERSTELLZEIT](#job-steuern-evanos2-verstellzeit) - Verstellzeitmessung EVANOS2 anstossen
- [STEUERN_AVANOS2_VERSTELLZEIT](#job-steuern-avanos2-verstellzeit) - Verstellzeitmessung AVANOS2 anstossen
- [STEUERN_EVANOS2_DICHTHEIT](#job-steuern-evanos2-dichtheit) - Dichtheitmessung EVANOS2 anstossen
- [STEUERN_AVANOS2_DICHTHEIT](#job-steuern-avanos2-dichtheit) - Dichtheitmessung AVANOS2 anstossen
- [STEUERN_EVANOS2_FRUEHANSCHLAG](#job-steuern-evanos2-fruehanschlag) - Fruehanschlag EVANOS2 anfahren
- [STEUERN_EVANOS2_SPAETANSCHLAG](#job-steuern-evanos2-spaetanschlag) - Spaetanschlag EVANOS2 anfahren
- [STEUERN_AVANOS2_FRUEHANSCHLAG](#job-steuern-avanos2-fruehanschlag) - Fruehanschlag AVANOS2 anfahren
- [STEUERN_AVANOS2_SPAETANSCHLAG](#job-steuern-avanos2-spaetanschlag) - Spaetanschlag AVANOS2 anfahren
- [STEUERN_LL_STELLER](#job-steuern-ll-steller) - Leerlaufsteller ansteuern (nur Stellglied)
- [CO_EINZELABGLEICH_LESEN](#job-co-einzelabgleich-lesen) - CO-Abgleich Einzelwert lesen (MSS50 je 1 Wort)
- [CO_EINZELABGLEICH_VERSTELLEN](#job-co-einzelabgleich-verstellen) - CO-Abgleich Einzelwert verstellen im RAM (MSS50 je 1 Wort)
- [CO_EINZELABGLEICH_PROGRAMMIEREN](#job-co-einzelabgleich-programmieren) - CO-Abgleich Einzelwert programmieren (von RAM ins EEPROM schreiben)
- [DIAGNOSE_ENDE](#job-diagnose-ende) - Beendet ALLE Diagnoseaktivitaeten, Neueinstieg sofort moeglich
- [DIAGNOSE_ERHALTEN](#job-diagnose-erhalten)
- [SPEICHER_LESEN](#job-speicher-lesen) - Lese Bytes ueber direkte Adressierung Maximallaenge ist begrenzt
- [SPEICHER_SCHREIBEN](#job-speicher-schreiben) - Schreibe binaere Bytes ueber direkte Adressierung Maximallaenge ist begrenzt
- [IO_STATUS_VORGEBEN](#job-io-status-vorgeben) - direkte Stellgliedansteuerung ueber Pin/Tastv./Periode
- [SYS_ADR_LESEN](#job-sys-adr-lesen) - Dient zum Auslesen systemspezifischer Adressen
- [HERSTELLER_DATEN_LESEN](#job-hersteller-daten-lesen) - Dient zum Auslesen herstellerspezifischer Adressen
- [HERSTELLER_SELBSTTEST](#job-hersteller-selbsttest) - Dient zum Aufruf einer herstellerspezifischen Testroutine (benoetigt spezielles Pruefumfeld - nicht fuer VK/HO)
- [SG_RESET](#job-sg-reset) - Dient zum Software-Reset, Adaptionen/FS nicht gesichert!
- [IO_STATUS_LESEN](#job-io-status-lesen) - Direktes Anfordern der IO-Bloecke ueber deren Index
- [MCS_AKTIVIEREN](#job-mcs-aktivieren) - MCS-Modus einschalten (derzeit nicht implementiert)
- [LOGIN_REQUEST](#job-login-request) - Schutzmechanismus SEED_KEY
- [SEED_KEY](#job-seed-key) - Schutzmechanismus SEED_KEY
- [ABGLEICH_LOGIN_REQUEST](#job-abgleich-login-request) - Schutzmechanismus nur fuer Abgleich, direkte Entriegelung
- [CODIER_CHECKSUM](#job-codier-checksum) - Steuergeraet prueft CRC16 Boot/Daten/Programm Master/Slave
- [ABGLEICHWERTE_SCHREIBEN](#job-abgleichwerte-schreiben) - Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten im Standardverfahren (ASCII)
- [ABGLEICHWERTE_LESEN](#job-abgleichwerte-lesen) - Lesen der aktuellen Abgleichwerte im Standardverfahren (ASCII)
- [ABGLEICHFLAG_SCHREIBEN](#job-abgleichflag-schreiben) - Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten
- [ABGLEICHFLAG_LESEN](#job-abgleichflag-lesen)
- [SPEICHER_SCHREIBEN_BINAER](#job-speicher-schreiben-binaer) - Schreibe binaere Bytes ueber direkte Adressierung Maximallaenge ist begrenzt
- [STEUERN_TI_ABGLEICH_STARTEN](#job-steuern-ti-abgleich-starten) - Anstossen der automatischen Einzeldrosselklappenkorrektur (Prueflauf)
- [STEUERN_TI_ABGLEICH_STOPPEN](#job-steuern-ti-abgleich-stoppen) - Unterbrechen der automatischen Einzeldrosselklappenkorrektur (Prueflauf)
- [SG_PRUEFLAUF](#job-sg-prueflauf) - Prueflauftelegramm mit freien Parametern abschicken
- [STEUERN_SG_AUTOSYNC](#job-steuern-sg-autosync) - automatische Leerlaufsynchronisation durchfuehren
- [STEUERN_SYNC_MODE](#job-steuern-sync-mode) - Synchronisation EWS
- [STATUS_SYNC_MODE](#job-status-sync-mode) - Status EWS auslesen
- [STATUS_ADD](#job-status-add) - Adaption Additiv Bank 1 (Lambdaadaptionsoffset 1) MW_ADD1
- [STATUS_LAMBDA_ADD_1](#job-status-lambda-add-1) - Adaption Additiv Bank 1 (Lambdaadaptionsoffset 1) MW_ADD1
- [STATUS_ADD_2](#job-status-add-2) - Adaption Additiv Bank 2 (Lambdaadaptionsoffset 2) MW_ADD2
- [STATUS_LAMBDA_ADD_2](#job-status-lambda-add-2) - Adaption Additiv Bank 2 (Lambdaadaptionsoffset 2) MW_ADD2
- [STATUS_VANOS_NW_LAGE_EINLASS_BANK_1](#job-status-vanos-nw-lage-einlass-bank-1) - Auslass-VANOS Bank 1 ist MW_AVANOS1_IST
- [STATUS_VANOS_NW_LAGE_EINLASS_BANK_2](#job-status-vanos-nw-lage-einlass-bank-2) - Auslass-VANOS Bank 2 ist MW_AVANOS2_IST
- [STATUS_AVANOS1_SOLL](#job-status-avanos1-soll) - Auslass-VANOS Bank 1 soll MW_AVANOS1_SOLL
- [STATUS_AVANOS2_SOLL](#job-status-avanos2-soll) - Auslass-VANOS Bank 2 soll MW_AVANOS2_SOLL
- [STATUS_AQREL](#job-status-aqrel) - relativer Oeffnungsquerschnitt MW_AQREL
- [STATUS_ANALOG_GM3](#job-status-analog-gm3) - Strom fuer Servotronikventil 
- [STATUS_SYSTEMCHECK_LAUFUNRUHE](#job-status-systemcheck-laufunruhe) - Laufunruhe lesen
- [LESEN_SYSTEMCHECK_LAUFUNRUHE](#job-lesen-systemcheck-laufunruhe) - Laufunruhe lesen
- [STATUS_SERVO_I_IST](#job-status-servo-i-ist) - Strom fuer Servotronikventil 
- [STATUS_SERVO_I_SOLL](#job-status-servo-i-soll) - Strom fuer Servotronikventil 
- [STATUS_DKP_WINKEL](#job-status-dkp-winkel) - Drosselklappensteller Istwert MW_DKIST
- [STATUS_DKP_WINKEL_SOLL](#job-status-dkp-winkel-soll) - Drosselklappensteller Sollwert MW_DKSOLL
- [STATUS_EVANOS1_IST](#job-status-evanos1-ist) - Einlass-VANOS Bank 1 ist MW_EVANOS1_IST
- [STATUS_EVANOS2_IST](#job-status-evanos2-ist) - Einlass-VANOS Bank 2 ist MW_EVANOS2_IST
- [STATUS_EVANOS1_SOLL](#job-status-evanos1-soll) - Einlass-VANOS Bank 1 soll MW_EVANOS1_SOLL
- [STATUS_EVANOS2_SOLL](#job-status-evanos2-soll) - Einlass-VANOS Bank 2 soll MW_EVANOS2_SOLL
- [STATUS_PWG_POTI_WINKEL](#job-status-pwg-poti-winkel) - Fahrpedalwertgeber Kanal 1 MW_FWG1
- [STATUS_PWG_POTI_WINKEL_2](#job-status-pwg-poti-winkel-2) - Fahrpedalwertgeber Kanal 2 MW_FWG2
- [STATUS_LAMBDA_INTEGRATOR_1](#job-status-lambda-integrator-1) - Lambdaregler 1 Regelfaktor MW_LAMBDA1
- [STATUS_INT](#job-status-int) - Lambdaregler 1 Regelfaktor MW_LAMBDA1
- [STATUS_LAMBDA_INTEGRATOR_2](#job-status-lambda-integrator-2) - Lambdaregler 2 Regelfaktor MW_LAMBDA2
- [STATUS_INT_2](#job-status-int-2) - Lambdaregler 2 Regelfaktor MW_LAMBDA2
- [STATUS_LFR_KO](#job-status-lfr-ko) - Leerlaufregleradaption mit Kompressor MW_LFR_KO
- [STATUS_LFR](#job-status-lfr) - Leerlaufregleradaption ohne Kompressor MW_LFR
- [STATUS_LS_NKAT_SIGNAL_1](#job-status-ls-nkat-signal-1) - Lambdasonde 1 nach Kat MW_LSH1
- [STATUS_L_SONDE_H](#job-status-l-sonde-h) - Lambdasonde 1 nach Kat MW_LSH1
- [STATUS_LS_NKAT_SIGNAL_2](#job-status-ls-nkat-signal-2) - Lambdasonde 2 nach Kat MW_LSH2
- [STATUS_L_SONDE_2_H](#job-status-l-sonde-2-h) - Lambdasonde 2 nach Kat MW_LSH2
- [STATUS_LS_VKAT_SIGNAL_1](#job-status-ls-vkat-signal-1) - Lambdasonde 1 vor Kat MW_LSV1
- [STATUS_L_SONDE](#job-status-l-sonde) - Lambdasonde 1 vor Kat MW_LSV1
- [STATUS_LS_VKAT_SIGNAL_2](#job-status-ls-vkat-signal-2) - Lambdasonde 2 vor Kat MW_LSV2
- [STATUS_L_SONDE_2](#job-status-l-sonde-2) - Lambdasonde 2 vor Kat MW_LSV2
- [STATUS_PWG_POTI_SPANNUNG](#job-status-pwg-poti-spannung) - Spannung PWG Kanal 1 MW_UPWG1M
- [STATUS_LMM_MASSE](#job-status-lmm-masse) - Luftmasse MW_ML
- [STATUS_LMM](#job-status-lmm) - Luftmasse MW_ML
- [STATUS_LAMBDA_MUL_1](#job-status-lambda-mul-1) - Adaption Multiplikativ Bank 1 (Lambdaadaptionsfaktor 1) MW_MUL1
- [STATUS_MUL](#job-status-mul) - Adaption Multiplikativ Bank 1 (Lambdaadaptionsfaktor 1) MW_MUL1
- [STATUS_LAMBDA_MUL_2](#job-status-lambda-mul-2) - Adaption Multiplikativ Bank 2 (Lambdaadaptionsfaktor 2) MW_MUL2
- [STATUS_MUL_2](#job-status-mul-2) - Adaption Multiplikativ Bank 2 (Lambdaadaptionsfaktor 2) MW_MUL2
- [STATUS_MOTORDREHZAHL](#job-status-motordrehzahl) - Drehzahl n MW_N
- [STATUS_NMAX](#job-status-nmax) - Maximaldrehzahl n MW_NMAX
- [STATUS_N_LL_SOLL](#job-status-n-ll-soll) - Leerlaufregler Solldrehzahl MW_N_LL_SOLL
- [STATUS_PUMG_INTERN](#job-status-pumg-intern) - Umgebungsdruck (intern) MW_PUMG_INTERN
- [STATUS_RF](#job-status-rf) - relative Fuellung MW_RF
- [STATUS_TABG](#job-status-tabg) - Abgastemperatur MW_TABG
- [STATUS_AN_LUFTTEMPERATUR](#job-status-an-lufttemperatur) - Ansauglufttemperatursensor MW_TANS
- [STATUS_EINSPRITZZEIT](#job-status-einspritzzeit) - Einspritzzeit Zylinder 1 MW_TI1
- [STATUS_TI2](#job-status-ti2) - Einspritzzeit Zylinder 2 MW_TI2
- [STATUS_TI3](#job-status-ti3) - Einspritzzeit Zylinder 3 MW_TI3
- [STATUS_TI4](#job-status-ti4) - Einspritzzeit Zylinder 4 MW_TI4
- [STATUS_TI5](#job-status-ti5) - Einspritzzeit Zylinder 5 MW_TI5
- [STATUS_TI6](#job-status-ti6) - Einspritzzeit Zylinder 6 MW_TI6
- [LESEN_SYSTEMCHECK_DMTL](#job-lesen-systemcheck-dmtl) - Ergebnis Funktionsueberpruefung DMTL abrufen
- [STATUS_TI7](#job-status-ti7) - Einspritzzeit Zylinder 7 MW_TI7
- [STATUS_TI8](#job-status-ti8) - Einspritzzeit Zylinder 8 MW_TI8
- [STATUS_TI_AUS_IST](#job-status-ti-aus-ist) - Ausblendzaehler Einspritzung Ist MW_TI_AUS_IST
- [STATUS_KUEHLW_AUSL_TEMPERATUR](#job-status-kuehlw-ausl-temperatur) - Kuehleraustrittstemperatur MW_TKA
- [STATUS_LAST](#job-status-last) - Lastsignal MW_TL
- [STATUS_MOTORTEMPERATUR](#job-status-motortemperatur) - Motortemperatursensor MW_TMOT
- [STATUS_TNMAX](#job-status-tnmax) - Gesamtzeit Ueberdrehzahl n MW_TNMAX
- [STATUS_OEL_TEMPERATUR](#job-status-oel-temperatur) - Oeltemperatur (TOG) MW_TOEL
- [STATUS_TUMG](#job-status-tumg) - Umgebungstemperatur MW_TUMG
- [STATUS_TV_TEV](#job-status-tv-tev) - Tastverhaeltnis Tankentlueftungsventil MW_TV_TEV
- [STATUS_TZ1](#job-status-tz1) - Zuendwinkel Zylinder 1 MW_TZ1
- [STATUS_TZ2](#job-status-tz2) - Zuendwinkel Zylinder 2 MW_TZ2
- [STATUS_TZ3](#job-status-tz3) - Zuendwinkel Zylinder 3 MW_TZ3
- [STATUS_TZ4](#job-status-tz4) - Zuendwinkel Zylinder 4 MW_TZ4
- [STATUS_TZ5](#job-status-tz5) - Zuendwinkel Zylinder 5 MW_TZ5
- [STATUS_TZ6](#job-status-tz6) - Zuendwinkel Zylinder 6 MW_TZ6
- [STATUS_TZ7](#job-status-tz7) - Zuendwinkel Zylinder 7 MW_TZ7
- [STATUS_TZ8](#job-status-tz8) - Zuendwinkel Zylinder 8 MW_TZ8
- [STATUS_UBATT](#job-status-ubatt) - Bordnetzspannung Hauptrelais MW_UBHR
- [STATUS_UEXT1](#job-status-uext1) - Sensorversorgung 1 (Master) MW_UEXT1
- [STATUS_UEXT2](#job-status-uext2) - Sensorversorgung 2 (Slave) MW_UEXT2
- [STATUS_GESCHWINDIGKEIT](#job-status-geschwindigkeit) - Geschwindigkeit v MW_V
- [STATUS_V_CAN](#job-status-v-can) - Fahrzeuggeschwindigkeit v_asc (CAN) MW_V_CAN
- [STATUS_VMAX](#job-status-vmax) - Maximalgeschwindigkeit v MW_VMAX
- [STATUS_GEBERRAD_ADAPTION](#job-status-geberrad-adaption) - Geberradadaption

<a id="job-steuern-avanos1-spaet-ventil"></a>
### STEUERN_AVANOS1_SPAET_VENTIL

Auslass-VANOS Bank 1 Spaetventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-avanos2-spaet-ventil"></a>
### STEUERN_AVANOS2_SPAET_VENTIL

Auslass-VANOS Bank 2 Spaetventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-avanos1-frueh-ventil"></a>
### STEUERN_AVANOS1_FRUEH_VENTIL

Auslass-VANOS Bank 1 Fruehventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-avanos2-frueh-ventil"></a>
### STEUERN_AVANOS2_FRUEH_VENTIL

Auslass-VANOS Bank 2 Fruehventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-evanos1-spaet-ventil"></a>
### STEUERN_EVANOS1_SPAET_VENTIL

Einlass-VANOS Bank 1 Spaetventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-evanos2-spaet-ventil"></a>
### STEUERN_EVANOS2_SPAET_VENTIL

Einlass-VANOS Bank 2 Spaetventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-evanos1-frueh-ventil"></a>
### STEUERN_EVANOS1_FRUEH_VENTIL

Einlass-VANOS Bank 1 Fruehventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-evanos2-frueh-ventil"></a>
### STEUERN_EVANOS2_FRUEH_VENTIL

Einlass-VANOS Bank 2 Fruehventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-lshv2"></a>
### STEUERN_LSHV2

Lambdasondenheizung vor Kat Bank 2 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-lshn1"></a>
### STEUERN_LSHN1

Lambdasondenheizung nach Kat Bank 1 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-lshn2"></a>
### STEUERN_LSHN2

Lambdasondenheizung nach Kat Bank 2 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-lshv1"></a>
### STEUERN_LSHV1

Lambdasondenheizung vor Kat Bank 1 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-zs8"></a>
### STEUERN_ZS8

Zuendspule Zyl. 8 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-zs7"></a>
### STEUERN_ZS7

Zuendspule Zyl. 7 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-zs6"></a>
### STEUERN_ZS6

Zuendspule Zyl. 6 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-zs5"></a>
### STEUERN_ZS5

Zuendspule Zyl. 5 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-zs4"></a>
### STEUERN_ZS4

Zuendspule Zyl. 4 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-zs3"></a>
### STEUERN_ZS3

Zuendspule Zyl. 3 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-zs2"></a>
### STEUERN_ZS2

Zuendspule Zyl. 2 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-zs1"></a>
### STEUERN_ZS1

Zuendspule Zyl. 1 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

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

<a id="job-steuern-ev8"></a>
### STEUERN_EV8

Einspritzventil 8 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev7"></a>
### STEUERN_EV7

Einspritzventil 7 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev6"></a>
### STEUERN_EV6

Einspritzventil 6 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev5"></a>
### STEUERN_EV5

Einspritzventil 5 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev4"></a>
### STEUERN_EV4

Einspritzventil 4 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev3"></a>
### STEUERN_EV3

Einspritzventil 3 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev2"></a>
### STEUERN_EV2

Einspritzventil 2 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ev1"></a>
### STEUERN_EV1

Einspritzventil 1 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-stop-systemcheck-sek-luft"></a>
### STOP_SYSTEMCHECK_SEK_LUFT

SLS Funktionstest Stop

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-start-systemcheck-sek-luft"></a>
### START_SYSTEMCHECK_SEK_LUFT

Funktionsueberpruefung SLS anstossen - erwarte Ergebnis ausserhalb Job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| START_SYSTEMCHECK_SEK_LUFT_STATUS | int |  |

<a id="job-lesen-systemcheck-sek-luft"></a>
### LESEN_SYSTEMCHECK_SEK_LUFT

Ergebnis Funktionsueberpruefung SLS abrufen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| LESEN_SYSTEMCHECK_SEK_LUFT_STATUS | int | Status als Wert |
| LESEN_SYSTEMCHECK_SEK_LUFT_STATUS_WERT | string | Status als Text |

<a id="job-steuern-e-luefter"></a>
### STEUERN_E_LUEFTER

Elektroluefterrelais ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-oekv2"></a>
### STEUERN_OEKV2

Oelkreisumschaltventil 2 (links) ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-oekv1"></a>
### STEUERN_OEKV1

Oelkreisumschaltventil 1 (rechts) ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-start"></a>
### STEUERN_START

Startrelais ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ekp"></a>
### STEUERN_EKP

Kraftstoffpumpenrelais ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-servov"></a>
### STEUERN_SERVOV

Servotronikventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-tev"></a>
### STEUERN_TEV

Tankentlueftungsventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-akl"></a>
### STEUERN_AKL

Abgasklappe ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-vdsv"></a>
### STEUERN_VDSV

VANOS-Druckspeicherventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-slv"></a>
### STEUERN_SLV

Sekundaerluftventil ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ko"></a>
### STEUERN_KO

Klimakompressorrelais ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-slp"></a>
### STEUERN_SLP

Sekundaerluftpumpenrelais ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-edic-reset"></a>
### EDIC_RESET

EDIC-Reset

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-initialisierung"></a>
### initialisierung

Default Init-Job

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| DONE | int | 1 wenn job erfolgreich 0 wenn job nicht erfolgreich |

<a id="job-info"></a>
### INFO

Information SGBD

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ECU | string | Steuergeraet im Klartext |
| ORIGIN | string | Steuergeraete-Verantwortlicher |
| REVISION | string | Versions-Nummer |
| AUTHOR | string | Name aller Autoren |
| COMMENT | string | wichtige Hinweise |
| SPRACHE | string | deutsch, english |

<a id="job-fs-lesen-text"></a>
### FS_LESEN_TEXT

Auslesen des Fehlerspeichers (nur die F.-Namen)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FS_KONZEPT | int | Uebergabeparameter, 0 fuer 1 Satz / 1 oder keine Uebergabe fuer 3 Saetze Umweltbed. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_ORT_TEXT | string | Fehlercode des SG als Text |

<a id="job-isn-lesen"></a>
### ISN_LESEN

liefert fertig formatierte ISN fuer MSS50

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ISN_LESEN_WERT | string | ISN als  WERT |
| JOB_STATUS | string |  |

<a id="job-ram-lesen"></a>
### RAM_LESEN

Beliebige RAM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| RAM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse High-Middle-Low |
| RAM_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| RAM_LESEN_WERT | binary | nichts |
| RAM_LESEN_EINH | string | Einheit HEX |

<a id="job-rom-lesen"></a>
### ROM_LESEN

Beliebige FLASH - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ROM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse Segment-High-Middle-Low |
| ROM_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| ROM_LESEN_WERT | binary | nichts |
| ROM_LESEN_EINH | string | Einheit HEX |

<a id="job-eeprom-lesen"></a>
### EEPROM_LESEN

Beliebige EEPROM - Zellen auslesen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EEPROM_LESEN_ADRESSE | long | Uebergabeparameter, Startadresse Segment-High-Middle-Low |
| EEPROM_LESEN_ANZAHL_BYTE | int | Uebergabeparameter, Anzahl der auszulesenden BYTES |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| EEPROM_LESEN_WERT | binary | nichts |
| EEPROM_LESEN_EINH | string | Einheit HEX |

<a id="job-ident"></a>
### IDENT

Ident-Daten fuer DME

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| ID_BMW_NR | string | BMW-Teilenummer |
| ID_HW_NR | int | BMW-Hardwarenummer |
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

<a id="job-ecu-config"></a>
### ECU_CONFIG

Ident-Daten fuer DME

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation (z.B. ACK) |
| EGS_VORHANDEN | int | EGS vorhanden 1=ja ,  0=nein , 0xff=nicht unterstuetzt |

<a id="job-abgas-variante-lesen"></a>
### ABGAS_VARIANTE_LESEN

Auslesen der Abgasvariante

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| ABGAS_VARIANTE_WERT | int | Abgasvariante 0=KAT-V , 1= KAT |

<a id="job-ews3-get-status"></a>
### EWS3_GET_STATUS

EWS3 Synchonisierungsstatus abfragen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EWS3_STATUS | string |  |
| EWS3_STATUS_WERT | int |  |

<a id="job-ews3-initialisieren"></a>
### EWS3_INITIALISIEREN

EWS3 initialisieren/abgleichen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| EWS3_MODE | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EWS3_STATUS | string |  |
| EWS3_STATUS_WERT | int |  |

<a id="job-ews3-sync"></a>
### EWS3_SYNC

EWS3-Steuergeraet ruecksetzen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EWS3_STATUS | string |  |

<a id="job-adapt-loeschen"></a>
### ADAPT_LOESCHEN

alle Adaptionen gleichzeitig loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-adapt-selektiv-loeschen"></a>
### ADAPT_SELEKTIV_LOESCHEN

Adaptionen bitweise loeschen und Zustaende bitweise setzen

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| STATUS_ADAPT | int |  |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-lambdaregler-sperren"></a>
### STEUERN_LAMBDAREGLER_SPERREN

LA-Regler ueber Adaptionstelegramm loeschen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-lls-testdrehzahl"></a>
### STEUERN_LLS_TESTDREHZAHL

feste Leerlaufanhebung fuer VANOS-Test

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-codier-checksumme"></a>
### STATUS_CODIER_CHECKSUMME

Codier - Checksumme abfragen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STATUS_CHECKSUMME_WERT | int | Ergebnis |

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
| AIF_ANZAHL_PROG | int | Anzahl Programmiervorgaenge |

<a id="job-fs-quick-lesen"></a>
### FS_QUICK_LESEN

Auslesen des QUICK Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_BSZ_AKT | real | Betriebsstundenzahler aktuell |
| F_BSZ_ALT | real | Betriebsstundenzaehler beim letzten Loeschen |

<a id="job-fs-lesen"></a>
### FS_LESEN

Auslesen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ART_ANZ | int | Anzahl der Fehlerarten des SG |
| F_UW_ANZ | int | Anzahl der Umweltbedingungen des einzelnen Fehlers |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_ORT_NR | int | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_LZ | int | Fehlerlogistikzaehler |
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
| F_VORHANDEN | int | Statusbit Fehler vorhanden |
| F_ART_BYTE | int | Fehlerartbyte als Rohwert ausgeben |
| F_UW1_NR | int | Satz 1 Umweltbedingung 1 Index |
| F_UW1_TEXT | string | Satz 1 Umweltbedingung 1 Einheit |
| F_UW1_EINH | string | Satz 1 Umweltbedingung 1 Text |
| F_UW1_WERT | real | Satz 1 Umweltbedingung 1 Wert |
| F_UW2_NR | int | Satz 1 Umweltbedingung 2 Index |
| F_UW2_TEXT | string | Satz 1 Umweltbedingung 2 Text |
| F_UW2_EINH | string | Satz 1 Umweltbedingung 2 Einheit |
| F_UW2_WERT | real | Satz 1 Umweltbedingung 2 Wert |
| F_UW3_NR | int | Satz 1 Umweltbedingung 3 Index |
| F_UW3_TEXT | string | Satz 1 Umweltbedingung 3 Text |
| F_UW3_EINH | string | Satz 1 Umweltbedingung 3 Einheit |
| F_UW3_WERT | real | Satz 1 Umweltbedingung 3 Wert |
| F_UW4_NR | int | Satz 1 Umweltbedingung 4 Index |
| F_UW4_TEXT | string | Satz 1 Umweltbedingung 4 Text |
| F_UW4_EINH | string | Satz 1 Umweltbedingung 4 Einheit |
| F_UW4_WERT | real | Satz  1 Umweltbedingung 4  Wert |
| F_UW5_NR | int | Satz 2 Umweltbedingung 1 Index |
| F_UW5_TEXT | string | Satz 2 Umweltbedingung 1 Text |
| F_UW5_EINH | string | Satz 2 Umweltbedingung 1 Einheit |
| F_UW5_WERT | real | Satz  2 Umweltbedingung 1  Wert |
| F_UW6_NR | int | Satz 2 Umweltbedingung 2 Index |
| F_UW6_TEXT | string | Satz 2 Umweltbedingung 2 Text |
| F_UW6_EINH | string | Satz 2 Umweltbedingung 2 Einheit |
| F_UW6_WERT | real | Satz  2 Umweltbedingung 2  Wert |
| F_UW7_NR | int | Satz 2 Umweltbedingung 3 Index |
| F_UW7_TEXT | string | Satz 2 Umweltbedingung 3 Text |
| F_UW7_EINH | string | Satz 2 Umweltbedingung 3 Einheit |
| F_UW7_WERT | real | Satz  2 Umweltbedingung 3  Wert |
| F_UW8_NR | int | Satz 2 Umweltbedingung 4 Index |
| F_UW8_TEXT | string | Satz 2 Umweltbedingung 4 Text |
| F_UW8_EINH | string | Satz 2 Umweltbedingung 4 Einheit |
| F_UW8_WERT | real | Satz  2 Umweltbedingung 4  Wert |
| F_UW9_NR | int | Satz 3 Umweltbedingung 1 Index |
| F_UW9_TEXT | string | Satz 3 Umweltbedingung 1 Text |
| F_UW9_EINH | string | Satz 3 Umweltbedingung 1 Einheit |
| F_UW9_WERT | real | Satz 3 Umweltbedingung 1  Wert |
| F_UW10_NR | int | Satz 3 Umweltbedingung 2 Index |
| F_UW10_TEXT | string | Satz 3 Umweltbedingung 2 Text |
| F_UW10_EINH | string | Satz 3 Umweltbedingung 2 Einheit |
| F_UW10_WERT | real | Satz  3 Umweltbedingung 2  Wert |
| F_UW11_NR | int | Satz 3 Umweltbedingung 3 Index |
| F_UW11_TEXT | string | Satz 3 Umweltbedingung 3 Text |
| F_UW11_EINH | string | Satz 3 Umweltbedingung 3 Einheit |
| F_UW11_WERT | real | Satz  3 Umweltbedingung 3  Wert |
| F_UW12_NR | int | Satz 3 Umweltbedingung 4 Index |
| F_UW12_TEXT | string | Satz 3 Umweltbedingung 4 Text |
| F_UW12_EINH | string | Satz 3 Umweltbedingung 4 Einheit |
| F_UW12_WERT | real | Satz 3 Umweltbedingung 4  Wert |
| F_UW13_NR | int | Satz 3 Umweltbedingung 4 Index |
| F_UW13_TEXT | string | Satz 3 Umweltbedingung 4 Text |
| F_UW13_EINH | string | Satz 3 Umweltbedingung 4 Einheit |
| F_UW13_WERT | real | Satz 3 Umweltbedingung 4  Wert |
| F_UW14_NR | int | Satz 3 Umweltbedingung 4 Index |
| F_UW14_TEXT | string | Satz 3 Umweltbedingung 4 Text |
| F_UW14_EINH | string | Satz 3 Umweltbedingung 4 Einheit |
| F_UW14_WERT | real | Satz 3 Umweltbedingung 4  Wert |
| F_UW15_NR | int | Satz 3 Umweltbedingung 4 Index |
| F_UW15_TEXT | string | Satz 3 Umweltbedingung 4 Text |
| F_UW15_EINH | string | Satz 3 Umweltbedingung 4 Einheit |
| F_UW15_WERT | real | Satz 3 Umweltbedingung 4  Wert |
| F_HEX_CODE | binary | Hexdump des Fehlersatzes |
| F_UW_SATZ | int | Anzahl der Umweltsaetze , Steuerung der Anzeige in der Applikation |

<a id="job-fs-lesen-old"></a>
### FS_LESEN_OLD

Auslesen des Fehlerspeichers

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| FS_KONZEPT | int | Uebergabeparameter, 0 fuer 1 Satz / 1 oder keine Uebergabe fuer 3 Saetze Umweltbed. |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| F_ANZ_NR | int | Anzahl der gespeicherten Fehler |
| F_ORT_NR | int | Fehlercode des SG als Index |
| F_ORT_TEXT | string | Fehlercode des SG als Text |
| F_HFK | int | Haeufigkeit des einzelnen Fehlers |
| F_LOGISTIK | int | Fehlerlogistikzaehler |
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
| F_UW2_NR | int | Umweltbedingung 2Index |
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
| F_UW12_NR | int | Umweltbedingung 1 Index |
| F_UW12_TEXT | string | Umweltbedingung 1 Einheit |
| F_UW12_EINH | string | Umweltbedingung 1 Text |
| F_UW12_WERT | real | Umweltbedingung 1 Wert |
| F_UW22_NR | int | Umweltbedingung 2Index |
| F_UW22_TEXT | string | Umweltbedingung 2 Text |
| F_UW22_EINH | string | Umweltbedingung 2 Einheit |
| F_UW22_WERT | real | Umweltbedingung 2 Wert |
| F_UW32_NR | int | Umweltbedingung 3 Index |
| F_UW32_TEXT | string | Umweltbedingung 3 Text |
| F_UW32_EINH | string | Umweltbedingung 3 Einheit |
| F_UW32_WERT | real | Umweltbedingung 3 Wert |
| F_UW42_NR | int | Umweltbedingung 4 Index |
| F_UW42_TEXT | string | Umweltbedingung 4 Text |
| F_UW42_EINH | string | Umweltbedingung 4 EINH |
| F_UW42_WERT | real | Umweltbedingung 4  Wert |
| F_UW52_NR | int | Umweltbedingung 5 Index |
| F_UW52_TEXT | string | Umweltbedingung 5 Text |
| F_UW52_EINH | string | Umweltbedingung 5 EINH |
| F_UW52_WERT | real | Umweltbedingung 5  Wert |
| F_UW62_NR | int | Umweltbedingung 6 Index |
| F_UW62_TEXT | string | Umweltbedingung 6 Text |
| F_UW62_EINH | string | Umweltbedingung 6 EINH |
| F_UW62_WERT | real | Umweltbedingung 6  Wert |
| F_UW13_NR | int | Umweltbedingung 1 Index |
| F_UW13_TEXT | string | Umweltbedingung 1 Einheit |
| F_UW13_EINH | string | Umweltbedingung 1 Text |
| F_UW13_WERT | real | Umweltbedingung 1 Wert |
| F_UW23_NR | int | Umweltbedingung 2Index |
| F_UW23_TEXT | string | Umweltbedingung 2 Text |
| F_UW23_EINH | string | Umweltbedingung 2 Einheit |
| F_UW23_WERT | real | Umweltbedingung 2 Wert |
| F_UW33_NR | int | Umweltbedingung 3 Index |
| F_UW33_TEXT | string | Umweltbedingung 3 Text |
| F_UW33_EINH | string | Umweltbedingung 3 Einheit |
| F_UW33_WERT | real | Umweltbedingung 3 Wert |
| F_UW43_NR | int | Umweltbedingung 4 Index |
| F_UW43_TEXT | string | Umweltbedingung 4 Text |
| F_UW43_EINH | string | Umweltbedingung 4 EINH |
| F_UW43_WERT | real | Umweltbedingung 4  Wert |
| F_UW53_NR | int | Umweltbedingung 5 Index |
| F_UW53_TEXT | string | Umweltbedingung 5 Text |
| F_UW53_EINH | string | Umweltbedingung 5 EINH |
| F_UW53_WERT | real | Umweltbedingung 5  Wert |
| F_UW63_NR | int | Umweltbedingung 6 Index |
| F_UW63_TEXT | string | Umweltbedingung 6 Text |
| F_UW63_EINH | string | Umweltbedingung 6 EINH |
| F_UW63_WERT | real | Umweltbedingung 6  Wert |
| F_STRING | binary | 10 oder 22 Fehlerbyte je nach Argument |

<a id="job-fs-shadow-lesen"></a>
### FS_SHADOW_LESEN

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
| F_LOGISTIK | int | Fehlerlogistikzaehler |
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
| F_UW2_NR | int | Umweltbedingung 2Index |
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
| F_BETRIEBSTUNDEN_WERT | real | Betriebstundenzaehler  des einzelnen Fehlers als Wert |
| F_ART1_NR_AKT | int | Fehlerart 1 Index |
| F_ART1_TEXT_AKT | string | Fehlerart 1 Text |
| F_ART2_NR_AKT | int | Fehlerart 2 Index |
| F_ART2_TEXT_AKT | string | Fehlerart 2 Text |
| F_ART3_NR_AKT | int | Fehlerart 3 Index |
| F_ART3_TEXT_AKT | string | Fehlerart 3 Text |
| F_ART4_NR_AKT | int | Fehlerart 4 Index |
| F_ART4_TEXT_AKT | string | Fehlerart 4 Text |
| F_ART5_NR_AKT | int | Fehlerart 5 Index |
| F_ART5_TEXT_AKT | string | Fehlerart 5 Text |
| F_ART6_NR_AKT | int | Fehlerart 6 Index |
| F_ART6_TEXT_AKT | string | Fehlerart 6 Text |
| F_ART7_NR_AKT | int | Fehlerart 7 Index |
| F_ART7_TEXT_AKT | string | Fehlerart 7 Text |
| F_ART8_NR_AKT | int | Fehlerart 8 Index |
| F_ART8_TEXT_AKT | string | Fehlerart 8  Text |
| F_FILTER_AKT | int | Fehlerfilter |
| F_CODEHEX | binary | 12 Fehlerbyte |

<a id="job-fs-loeschen"></a>
### FS_LOESCHEN

Loeschen des Fehlerspeichers

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-status-digital"></a>
### STATUS_DIGITAL

Status Schalteingaenge

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_BA_EIN | int | Status Beschleunigungsanreicherung |
| STAT_SA_EIN | int | Status Schubabschaltung |
| STAT_LSHV1_EIN | int | Status Lambdasondenheizung vor Kat Bank 1 |
| STAT_LSHV2_EIN | int | Status Lambdasondenheizung vor Kat Bank 2 |
| STAT_LSHN1_EIN | int | Status Lambdasondenheizung nach Kat Bank 1 |
| STAT_LSHN2_EIN | int | Status Lambdasondenheizung nach Kat Bank 2 |
| STAT_ZUENDUNG1_EIN | int | Status Zuendung 1 |
| STAT_ZUENDUNG2_EIN | int | Status Zuendung 2 |
| STAT_ZUENDUNG3_EIN | int | Status Zuendung 3 |
| STAT_ZUENDUNG4_EIN | int | Status Zuendung 4 |
| STAT_ZUENDUNG5_EIN | int | Status Zuendung 5 |
| STAT_ZUENDUNG6_EIN | int | Status Zuendung 6 |
| STAT_ZUENDUNG7_EIN | int | Status Zuendung 7 |
| STAT_ZUENDUNG8_EIN | int | Status Zuendung 8 |
| STAT_AKL_EIN | int | Status Abgasklappe |
| STAT_SLP_EIN | int | Status Sekundaerluftpumpe |
| STAT_SLV_EIN | int | Status Sekundaerluftventil |
| STAT_ELU_EIN | int | Status Eletroluefter |
| STAT_EKP_EIN | int | Status Kraftstoffpumpe |
| STAT_NOISE_EIN | int | Status Geraeuschminderung |
| STAT_SCHUTZ_EIN | int | Status Klopfschutzbetrieb |
| STAT_KLOPFREGELUNG_EIN | int | Status Klopfregelung |
| STAT_KLOPFREG_EIN | int | Status Klopfregelung |
| STAT_KRAFTSCHLUSS_EIN | int | Status Kraftschlussschalterkette |
| STAT_KO_EIN | int | Status Klimakompressor |
| STATUS_KO_EIN | int | Status Klimakompressor |
| STATUS_AC_EIN | int | Status Klimakompressor |
| STAT_AC_EIN | int | Status Klimakompressor |
| STAT_KL15_EIN | int | Status Zuendung |
| STAT_KL50_EIN | int | Status Anlasser |
| STAT_LDP_EIN | int | Status Leckerkennungsschalter Tank |
| STAT_MOTOR_STEHT | int | Status Motorstillstand |
| STAT_MOTOR_START | int | Status Start |
| STAT_LL_EIN | int | Status Leerlauf |
| STATUS_LL_EIN | int | Status Leerlauf |
| STAT_VL_EIN | int | Status Teillast |
| STATUS_VL_EIN | int | Status Teillast |
| STAT_TL_EIN | int | Status Vollast |
| STAT_MOTOR_NACHLAUF | int | Status Nachlauf |
| STAT_KATHEIZEN_EIN | int | Status Katheizen |
| STAT_KUP_EIN | int | Status Kupplungsschalter |
| STAT_BLS_EIN | int | Status Bremslichtschalter |
| STAT_BLTS_EIN | int | Status Bremslichttestschalter |
| STAT_EWS3_FREIGABE | int | Status Freigabe EWS3 |
| STAT_FDYN_EIN | int | Status Fahrdynamiktaster |
| STAT_MIL_EIN | int | Status Check-Engine-Lampe |
| STAT_MFL1_EIN | int | Status Multifunktionslekrad Taste 1 |
| STAT_MFL2_EIN | int | Status Multifunktionslekrad Taste 2 |
| STAT_MFL3_EIN | int | Status Multifunktionslekrad Taste 3 |
| STAT_MFL4_EIN | int | Status Multifunktionslekrad Taste 4 |
| STAT_LLR_EIN | int | Status Leerlaufregler |
| STAT_LDR1_EIN | int | Status Lambdaregler Bank 1 |
| STAT_LDR2_EIN | int | Status Lambdaregler Bank 2 |
| STAT_FGRA_EIN | int | Status Lambdaregler Bank 2 |

<a id="job-steuern-avanos1"></a>
### STEUERN_AVANOS1

AVANOS1 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-evanos1"></a>
### STEUERN_EVANOS1

EVANOS1 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-evanos1-verstellzeit"></a>
### STEUERN_EVANOS1_VERSTELLZEIT

Verstellzeitmessung EVANOS1 anstossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EVAN_VERSTELLZEIT_FRUEH | int |  |
| EVAN_VERSTELLZEIT_FRUEH_EINH | string |  |
| EVAN_VERSTELLZEIT_SPAET | int |  |
| EVAN_VERSTELLZEIT_SPAET_EINH | string |  |

<a id="job-steuern-avanos1-verstellzeit"></a>
### STEUERN_AVANOS1_VERSTELLZEIT

Verstellzeitmessung AVANOS1 anstossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AVAN_VERSTELLZEIT_FRUEH | int |  |
| AVAN_VERSTELLZEIT_FRUEH_EINH | string |  |
| AVAN_VERSTELLZEIT_SPAET | int |  |
| AVAN_VERSTELLZEIT_SPAET_EINH | string |  |

<a id="job-steuern-evanos1-dichtheit"></a>
### STEUERN_EVANOS1_DICHTHEIT

Dichtheitmessung EVANOS1 anstossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EVAN_ISTWERT | int |  |
| EVAN_ISTWERT_EINH | string |  |
| EVAN_SOLLWERT | int |  |
| EVAN_SOLLWERT_EINH | string |  |
| EVAN_STATUS | string |  |

<a id="job-steuern-avanos1-dichtheit"></a>
### STEUERN_AVANOS1_DICHTHEIT

Dichtheitmessung AVANOS1 anstossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AVAN_ISTWERT | int |  |
| AVAN_ISTWERT_EINH | string |  |
| AVAN_SOLLWERT | int |  |
| AVAN_SOLLWERT_EINH | string |  |
| AVAN_STATUS | string |  |

<a id="job-steuern-evanos1-fruehanschlag"></a>
### STEUERN_EVANOS1_FRUEHANSCHLAG

Fruehanschlag EVANOS1 anfahren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EVAN_ISTWERT | int |  |
| EVAN_ISTWERT_EINH | string |  |
| EVAN_SOLLWERT | int |  |
| EVAN_SOLLWERT_EINH | string |  |

<a id="job-steuern-evanos1-spaetanschlag"></a>
### STEUERN_EVANOS1_SPAETANSCHLAG

Spaetanschlag EVANOS1 anfahren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EVAN_ISTWERT | int |  |
| EVAN_ISTWERT_EINH | string |  |
| EVAN_SOLLWERT | int |  |
| EVAN_SOLLWERT_EINH | string |  |

<a id="job-steuern-avanos1-fruehanschlag"></a>
### STEUERN_AVANOS1_FRUEHANSCHLAG

Fruehanschlag AVANOS1 anfahren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AVAN_ISTWERT | int |  |
| AVAN_ISTWERT_EINH | string |  |
| AVAN_SOLLWERT | int |  |
| AVAN_SOLLWERT_EINH | string |  |

<a id="job-steuern-avanos1-spaetanschlag"></a>
### STEUERN_AVANOS1_SPAETANSCHLAG

Spaetanschlag AVANOS1 anfahren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AVAN_ISTWERT | int |  |
| AVAN_ISTWERT_EINH | string |  |
| AVAN_SOLLWERT | int |  |
| AVAN_SOLLWERT_EINH | string |  |

<a id="job-steuern-avanos2"></a>
### STEUERN_AVANOS2

AVANOS2 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-evanos2"></a>
### STEUERN_EVANOS2

EVANOS2 ansteuern

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-evanos2-verstellzeit"></a>
### STEUERN_EVANOS2_VERSTELLZEIT

Verstellzeitmessung EVANOS2 anstossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EVAN_VERSTELLZEIT_FRUEH | int |  |
| EVAN_VERSTELLZEIT_FRUEH_EINH | string |  |
| EVAN_VERSTELLZEIT_SPAET | int |  |
| EVAN_VERSTELLZEIT_SPAET_EINH | string |  |

<a id="job-steuern-avanos2-verstellzeit"></a>
### STEUERN_AVANOS2_VERSTELLZEIT

Verstellzeitmessung AVANOS2 anstossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AVAN_VERSTELLZEIT_FRUEH | int |  |
| AVAN_VERSTELLZEIT_FRUEH_EINH | string |  |
| AVAN_VERSTELLZEIT_SPAET | int |  |
| AVAN_VERSTELLZEIT_SPAET_EINH | string |  |

<a id="job-steuern-evanos2-dichtheit"></a>
### STEUERN_EVANOS2_DICHTHEIT

Dichtheitmessung EVANOS2 anstossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EVAN_ISTWERT | int |  |
| EVAN_ISTWERT_EINH | string |  |
| EVAN_SOLLWERT | int |  |
| EVAN_SOLLWERT_EINH | string |  |
| EVAN_STATUS | string |  |

<a id="job-steuern-avanos2-dichtheit"></a>
### STEUERN_AVANOS2_DICHTHEIT

Dichtheitmessung AVANOS2 anstossen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AVAN_ISTWERT | int |  |
| AVAN_ISTWERT_EINH | string |  |
| AVAN_SOLLWERT | int |  |
| AVAN_SOLLWERT_EINH | string |  |
| AVAN_STATUS | string |  |

<a id="job-steuern-evanos2-fruehanschlag"></a>
### STEUERN_EVANOS2_FRUEHANSCHLAG

Fruehanschlag EVANOS2 anfahren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EVAN_ISTWERT | int |  |
| EVAN_ISTWERT_EINH | string |  |
| EVAN_SOLLWERT | int |  |
| EVAN_SOLLWERT_EINH | string |  |

<a id="job-steuern-evanos2-spaetanschlag"></a>
### STEUERN_EVANOS2_SPAETANSCHLAG

Spaetanschlag EVANOS2 anfahren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| EVAN_ISTWERT | int |  |
| EVAN_ISTWERT_EINH | string |  |
| EVAN_SOLLWERT | int |  |
| EVAN_SOLLWERT_EINH | string |  |

<a id="job-steuern-avanos2-fruehanschlag"></a>
### STEUERN_AVANOS2_FRUEHANSCHLAG

Fruehanschlag AVANOS2 anfahren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AVAN_ISTWERT | int |  |
| AVAN_ISTWERT_EINH | string |  |
| AVAN_SOLLWERT | int |  |
| AVAN_SOLLWERT_EINH | string |  |

<a id="job-steuern-avanos2-spaetanschlag"></a>
### STEUERN_AVANOS2_SPAETANSCHLAG

Spaetanschlag AVANOS2 anfahren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| AVAN_ISTWERT | int |  |
| AVAN_ISTWERT_EINH | string |  |
| AVAN_SOLLWERT | int |  |
| AVAN_SOLLWERT_EINH | string |  |

<a id="job-steuern-ll-steller"></a>
### STEUERN_LL_STELLER

Leerlaufsteller ansteuern (nur Stellglied)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-co-einzelabgleich-lesen"></a>
### CO_EINZELABGLEICH_LESEN

CO-Abgleich Einzelwert lesen (MSS50 je 1 Wort)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZYLINDER_NR | int | Uebergabeparameter, Index fuer Zylinder |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_CO_ABGLEICH_WERT | int | Aktuellen Abgleichwert |

<a id="job-co-einzelabgleich-verstellen"></a>
### CO_EINZELABGLEICH_VERSTELLEN

CO-Abgleich Einzelwert verstellen im RAM (MSS50 je 1 Wort)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZYLINDER_NR | int | Uebergabeparameter, Index fuer Zylinder |
| CO_VERSTELL_WERT | int | Neuer Verstellwert |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-co-einzelabgleich-programmieren"></a>
### CO_EINZELABGLEICH_PROGRAMMIEREN

CO-Abgleich Einzelwert programmieren (von RAM ins EEPROM schreiben)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ZYLINDER_NR | int | Uebergabeparameter, Index fuer Zylinder |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |

<a id="job-diagnose-ende"></a>
### DIAGNOSE_ENDE

Beendet ALLE Diagnoseaktivitaeten, Neueinstieg sofort moeglich

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-diagnose-erhalten"></a>
### DIAGNOSE_ERHALTEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-speicher-lesen"></a>
### SPEICHER_LESEN

Lese Bytes ueber direkte Adressierung Maximallaenge ist begrenzt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | int | Segment oder Speicher |
| ADR | unsigned long | Adresse |
| ANZ_BYTE | int | Anzahl der zu lesenden Bytes |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| DATEN | binary | Inhalte der Speicherzellen 1 bis n |

<a id="job-speicher-schreiben"></a>
### SPEICHER_SCHREIBEN

Schreibe binaere Bytes ueber direkte Adressierung Maximallaenge ist begrenzt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | unsigned int | Segment oder Speicher |
| ADR | unsigned long | Adresse |
| ANZ_BYTE | unsigned int | Anzahl der zu schreibenden Bytes |
| DATEN | string | Inhalte von Byte 1 bis n in ASCII-Code |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT_RESULT | binary | Segment oder Speicher |
| ADR_RESULT | binary | naechste freie Adresse low |
| ANZ_BYTE_RESULT | binary | Anzahl der beschriebenen Bytes |
| VERIFY_BYTE | string | 01-O.K., 02-falsch, 03-nicht geloescht etc. |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-io-status-vorgeben"></a>
### IO_STATUS_VORGEBEN

direkte Stellgliedansteuerung ueber Pin/Tastv./Periode

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| PIN_NUMMER | int |  |
| TASTVERHAELTNIS | int | 00 Stellglied nicht angesteuert, ff staendig angesteuert |
| PERIODENDAUER | int | 00 ungueltig |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| PIN_NUMMER_RESULT | binary |  |
| RUECKMELDUNG | string |  |

<a id="job-sys-adr-lesen"></a>
### SYS_ADR_LESEN

Dient zum Auslesen systemspezifischer Adressen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| PROGRAMMIER_SPANNUNG_ADR | binary | Adresse hhmmll |
| DIF_DATEN_REFERENZ_ADR | binary | Adresse hhmmll |
| LOESCHDAUER_ADR | binary | Adresse hhmmll |
| BRIF_HW_REFERENZ_ADR | binary | Adresse hhmmll |
| ZIF_PROGRAMM_REFERENZ_ADR | binary | Adresse hhmmll |
| AIF_ADR | binary | Adresse hhmmll |
| MAX_LENGTH_DS2_ADR | binary | Adresse hhmmll |
| HERSTELLER_DATUM_ADR | binary | Adresse hhmmll |
| ZIF_BACKUP_ADR | binary | Adresse hhmmll |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-hersteller-daten-lesen"></a>
### HERSTELLER_DATEN_LESEN

Dient zum Auslesen herstellerspezifischer Adressen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| BMW_TEILE_NR_ADR | binary | Adresse hhmmll |
| SIEMENS_HW_ADR | binary | Adresse hhmmll |
| BMW_HW_NR_ADR | binary | Adresse hhmmll |
| SIEMENS_SW_NR_GESAMT_ADR | binary | Adresse hhmmll |
| SIEMENS_SW_NR_MASTER_ADR | binary | Adresse hhmmll |
| SIEMENS_SW_NR_SLAVE_ADR | binary | Adresse hhmmll |
| SIEMENS_HERSTELLWOCHE_ADR | binary | Adresse hhmmll |
| SIEMENS_HERSTELLJAHR_ADR | binary | Adresse hhmmll |
| LIEFERANTEN_NR_ADR | binary | Adresse hhmmll |
| AENDERUNGSINDEX_ADR | binary | Adresse hhmmll |
| SG_SERIEN_NR_ADR | binary | Adresse hhmmll |
| PROGRAMMIERSPANNUNG | binary | Direkt, keine Adresse |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-hersteller-selbsttest"></a>
### HERSTELLER_SELBSTTEST

Dient zum Aufruf einer herstellerspezifischen Testroutine (benoetigt spezielles Pruefumfeld - nicht fuer VK/HO)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-sg-reset"></a>
### SG_RESET

Dient zum Software-Reset, Adaptionen/FS nicht gesichert!

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-io-status-lesen"></a>
### IO_STATUS_LESEN

Direktes Anfordern der IO-Bloecke ueber deren Index

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| AUSWAHL | int | Auswahl der Groessen, die man auslesen moechte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| IO_BYTES | binary | I/O-Byte 1 bis n |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-mcs-aktivieren"></a>
### MCS_AKTIVIEREN

MCS-Modus einschalten (derzeit nicht implementiert)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-login-request"></a>
### LOGIN_REQUEST

Schutzmechanismus SEED_KEY

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LOGIN | binary | Rueckgabewert Status |
| Z_ZAHL | int | Zufallszahl |

<a id="job-seed-key"></a>
### SEED_KEY

Schutzmechanismus SEED_KEY

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LOGIN | binary | Rueckgabewert Status |
| Z_ZAHL | int | Zufallszahl |

<a id="job-abgleich-login-request"></a>
### ABGLEICH_LOGIN_REQUEST

Schutzmechanismus nur fuer Abgleich, direkte Entriegelung

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| STAT_LOGIN | binary | Rueckgabewert Status |

<a id="job-codier-checksum"></a>
### CODIER_CHECKSUM

Steuergeraet prueft CRC16 Boot/Daten/Programm Master/Slave

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| RUECK_MELDUNG | string | Ergebnis der Checksummenpruefung |

<a id="job-abgleichwerte-schreiben"></a>
### ABGLEICHWERTE_SCHREIBEN

Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten im Standardverfahren (ASCII)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_SCHREIBEN_ANZAHL | int | Anzahl der zu schreibenden Abgleichdatenbytes ohne die Pruefziffer |
| ABGLEICHWERTE_SCHREIBEN_DATEN | string | Abgleichdaten in folgendem Format z.B. 01 02 AB FF ... &lt;PZ&gt; Datenbytes - 2-stellige Hex-Werte, jeweils gefolgt von einem (1) Leerzeichen - Wertebereich: 00 - FF - nur Grossbuchstaben A - F sind erlaubt Pruefziffer &lt;PZ&gt;: - 1-stelliges Zeichen - Wertebereich: 0 - 9, A - Z - nur Grossbuchstaben A - Z sind erlaubt |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_..., wenn Argument nicht uebergeben oder ausser Bereich |
| ABGLEICHWERTE_SCHREIBEN_ABGLEICHDATEN | string | Abgleichdaten zum Steuergeraet |
| ABGLEICHWERTE_SCHREIBEN_PRUEFZEICHEN | string | das im Job berechnete Pruefzeichen |

<a id="job-abgleichwerte-lesen"></a>
### ABGLEICHWERTE_LESEN

Lesen der aktuellen Abgleichwerte im Standardverfahren (ASCII)

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_LESEN_ANZAHL | int | Anzahl der zu lesenden Abgleichwerte |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHWERTE_LESEN_DATEN | string | aus dem Steuergraet ausgelesene Daten im Format z.B."01 A5 FE" |
| JOB_STATUS | string | OKAY,wenn fehlerfrei ERROR_..., wenn Argument nicht uebergeben oder ausser Bereich |

<a id="job-abgleichflag-schreiben"></a>
### ABGLEICHFLAG_SCHREIBEN

Beschreiben des internen Speichers mit den motorspezifischen Abgleichdaten

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHFLAG_SCHREIBEN_FLAG | string | ABGLEICH_IO ABGLEICH_NIO |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_..., wenn argument nicht uebergeben oder ausser Bereich |

<a id="job-abgleichflag-lesen"></a>
### ABGLEICHFLAG_LESEN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| ABGLEICHFLAG_LESEN_WERT | string | 0x0000 --&gt; ABGLEICH_IO 0xFFFF --&gt; ABGLEICH_NIO |
| JOB_STATUS | string | OKAY, wenn fehlerfrei ERROR_..., wenn Argument nicht uebergeben oder ausser Bereich |

<a id="job-speicher-schreiben-binaer"></a>
### SPEICHER_SCHREIBEN_BINAER

Schreibe binaere Bytes ueber direkte Adressierung Maximallaenge ist begrenzt

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT | unsigned int | Segment oder Speicher |
| ADR | unsigned long | Adresse |
| ANZ_BYTE | unsigned int | Anzahl der zu schreibenden Bytes |
| DATEN | string | Inhalte von Byte 1 bis n in ASCII-Code |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| SEGMENT_RESULT | binary | Segment oder Speicher |
| ADR_RESULT | binary | naechste freie Adresse low |
| ANZ_BYTE_RESULT | binary | Anzahl der beschriebenen Bytes |
| VERIFY_BYTE | string | 01-O.K., 02-falsch, 03-nicht geloescht etc. |
| JOB_STATUS | string | Status der Kommunikation |

<a id="job-steuern-ti-abgleich-starten"></a>
### STEUERN_TI_ABGLEICH_STARTEN

Anstossen der automatischen Einzeldrosselklappenkorrektur (Prueflauf)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-steuern-ti-abgleich-stoppen"></a>
### STEUERN_TI_ABGLEICH_STOPPEN

Unterbrechen der automatischen Einzeldrosselklappenkorrektur (Prueflauf)

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |

<a id="job-sg-prueflauf"></a>
### SG_PRUEFLAUF

Prueflauftelegramm mit freien Parametern abschicken

#### Arguments

| Name | Type | Comment |
| --- | --- | --- |
| TEST_NUMMER | int | Testnummer 0-255 |
| TEST_PAR1 | int | 1. freier Testparameter 0-255 Integer-Wert |
| TEST_PAR2 | int | 2. freier Testparameter 0-255 Integer-Wert |
| TEST_DATA | string | 3. Datenblock in ASCII (bis maximale Telegrammlaenge) |

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | Status der Kommunikation |
| TEST_RESULT | binary |  |
| RUECKMELDUNG | string |  |

<a id="job-steuern-sg-autosync"></a>
### STEUERN_SG_AUTOSYNC

automatische Leerlaufsynchronisation durchfuehren

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| SYNC_STATUS | string |  |
| SYNC_MESSAGE | string |  |

<a id="job-steuern-sync-mode"></a>
### STEUERN_SYNC_MODE

Synchronisation EWS

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

<a id="job-status-sync-mode"></a>
### STATUS_SYNC_MODE

Status EWS auslesen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | "OKAY", wenn fehlerfrei |
| STATUS_SYNC_MODE_STATUS | int | Statusflag |
| STATUS_SYNC_MODE_TEXT | string | Statustext |

<a id="job-status-add"></a>
### STATUS_ADD

Adaption Additiv Bank 1 (Lambdaadaptionsoffset 1) MW_ADD1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_ADD_WERT | real | Ergebnis |
| STATUS_ADD_EINH | string | Einheit |

<a id="job-status-lambda-add-1"></a>
### STATUS_LAMBDA_ADD_1

Adaption Additiv Bank 1 (Lambdaadaptionsoffset 1) MW_ADD1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAMBDA_ADD_1_WERT | real | Ergebnis |
| STAT_LAMBDA_ADD_1_EINH | string | Einheit |

<a id="job-status-add-2"></a>
### STATUS_ADD_2

Adaption Additiv Bank 2 (Lambdaadaptionsoffset 2) MW_ADD2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_ADD_2_WERT | real | Ergebnis |
| STATUS_ADD_2_EINH | string | Einheit |

<a id="job-status-lambda-add-2"></a>
### STATUS_LAMBDA_ADD_2

Adaption Additiv Bank 2 (Lambdaadaptionsoffset 2) MW_ADD2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAMBDA_ADD_2_WERT | real | Ergebnis |
| STAT_LAMBDA_ADD_2_EINH | string | Einheit |

<a id="job-status-vanos-nw-lage-einlass-bank-1"></a>
### STATUS_VANOS_NW_LAGE_EINLASS_BANK_1

Auslass-VANOS Bank 1 ist MW_AVANOS1_IST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_VANOS_NW_LAGE_EINLASS_BANK_1_WERT | real | Ergebnis |
| STAT_VANOS_NW_LAGE_EINLASS_BANK_1_EINH | string | Einheit |

<a id="job-status-vanos-nw-lage-einlass-bank-2"></a>
### STATUS_VANOS_NW_LAGE_EINLASS_BANK_2

Auslass-VANOS Bank 2 ist MW_AVANOS2_IST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_VANOS_NW_LAGE_EINLASS_BANK_2_WERT | real | Ergebnis |
| STAT_VANOS_NW_LAGE_EINLASS_BANK_2_EINH | string | Einheit |

<a id="job-status-avanos1-soll"></a>
### STATUS_AVANOS1_SOLL

Auslass-VANOS Bank 1 soll MW_AVANOS1_SOLL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_AVANOS1_SOLL_WERT | real | Ergebnis |
| STAT_AVANOS1_SOLL_EINH | string | Einheit |

<a id="job-status-avanos2-soll"></a>
### STATUS_AVANOS2_SOLL

Auslass-VANOS Bank 2 soll MW_AVANOS2_SOLL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_AVANOS2_SOLL_WERT | real | Ergebnis |
| STAT_AVANOS2_SOLL_EINH | string | Einheit |

<a id="job-status-aqrel"></a>
### STATUS_AQREL

relativer Oeffnungsquerschnitt MW_AQREL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_AQREL_WERT | real | Ergebnis |
| STAT_AQREL_EINH | string | Einheit |

<a id="job-status-analog-gm3"></a>
### STATUS_ANALOG_GM3

Strom fuer Servotronikventil 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_ISERV_WERT | real | Ergebnis |
| STAT_ISERV_EINH | string | Einheit |
| STAT_SSERV_WERT | real | Ergebnis |
| STAT_SSERV_EINH | string | Einheit |

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

<a id="job-status-servo-i-ist"></a>
### STATUS_SERVO_I_IST

Strom fuer Servotronikventil 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_SERVO_I_IST_WERT | real | Ergebnis |
| STAT_SERVO_I_IST_EINH | string | Einheit |

<a id="job-status-servo-i-soll"></a>
### STATUS_SERVO_I_SOLL

Strom fuer Servotronikventil 

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_SERVO_I_SOLL_WERT | real | Ergebnis |
| STAT_SERVO_I_SOLL_EINH | string | Einheit |

<a id="job-status-dkp-winkel"></a>
### STATUS_DKP_WINKEL

Drosselklappensteller Istwert MW_DKIST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DKP_WINKEL_WERT | real | Ergebnis |
| STAT_DKP_WINKEL_EINH | string | Einheit |

<a id="job-status-dkp-winkel-soll"></a>
### STATUS_DKP_WINKEL_SOLL

Drosselklappensteller Sollwert MW_DKSOLL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_DKP_WINKEL_SOLL_WERT | real | Ergebnis |
| STAT_DKP_WINKEL_SOLL_EINH | string | Einheit |

<a id="job-status-evanos1-ist"></a>
### STATUS_EVANOS1_IST

Einlass-VANOS Bank 1 ist MW_EVANOS1_IST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EVANOS1_IST_WERT | real | Ergebnis |
| STAT_EVANOS1_IST_EINH | string | Einheit |

<a id="job-status-evanos2-ist"></a>
### STATUS_EVANOS2_IST

Einlass-VANOS Bank 2 ist MW_EVANOS2_IST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EVANOS2_IST_WERT | real | Ergebnis |
| STAT_EVANOS2_IST_EINH | string | Einheit |

<a id="job-status-evanos1-soll"></a>
### STATUS_EVANOS1_SOLL

Einlass-VANOS Bank 1 soll MW_EVANOS1_SOLL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EVANOS1_SOLL_WERT | real | Ergebnis |
| STAT_EVANOS1_SOLL_EINH | string | Einheit |

<a id="job-status-evanos2-soll"></a>
### STATUS_EVANOS2_SOLL

Einlass-VANOS Bank 2 soll MW_EVANOS2_SOLL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EVANOS2_SOLL_WERT | real | Ergebnis |
| STAT_EVANOS2_SOLL_EINH | string | Einheit |

<a id="job-status-pwg-poti-winkel"></a>
### STATUS_PWG_POTI_WINKEL

Fahrpedalwertgeber Kanal 1 MW_FWG1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PWG_POTI_WINKEL_WERT | real | Ergebnis |
| STAT_ROHWERT1 | int | Ergebnis |
| STAT_ROHWERT2 | int | Ergebnis |
| STAT_PWG_POTI_WINKEL_EINH | string | Einheit |

<a id="job-status-pwg-poti-winkel-2"></a>
### STATUS_PWG_POTI_WINKEL_2

Fahrpedalwertgeber Kanal 2 MW_FWG2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PWG_POTI_WINKEL_2_WERT | real | Ergebnis |
| STAT_PWG_POTI_WINKEL_2_EINH | string | Einheit |

<a id="job-status-lambda-integrator-1"></a>
### STATUS_LAMBDA_INTEGRATOR_1

Lambdaregler 1 Regelfaktor MW_LAMBDA1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAMBDA_INTEGRATOR_1_WERT | real | Ergebnis |
| STAT_LAMBDA_INTEGRATOR_1_EINH | string | Einheit |

<a id="job-status-int"></a>
### STATUS_INT

Lambdaregler 1 Regelfaktor MW_LAMBDA1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_INT_WERT | real | Ergebnis |
| STATUS_INT_EINH | string | Einheit |

<a id="job-status-lambda-integrator-2"></a>
### STATUS_LAMBDA_INTEGRATOR_2

Lambdaregler 2 Regelfaktor MW_LAMBDA2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAMBDA_INTEGRATOR_2_WERT | real | Ergebnis |
| STAT_LAMBDA_INTEGRATOR_2_EINH | string | Einheit |

<a id="job-status-int-2"></a>
### STATUS_INT_2

Lambdaregler 2 Regelfaktor MW_LAMBDA2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_INT_2_WERT | real | Ergebnis |
| STATUS_INT_2_EINH | string | Einheit |

<a id="job-status-lfr-ko"></a>
### STATUS_LFR_KO

Leerlaufregleradaption mit Kompressor MW_LFR_KO

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LFR_KO_WERT | real | Ergebnis |
| STAT_LFR_KO_EINH | string | Einheit |

<a id="job-status-lfr"></a>
### STATUS_LFR

Leerlaufregleradaption ohne Kompressor MW_LFR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LFR_WERT | real | Ergebnis |
| STAT_LFR_EINH | string | Einheit |

<a id="job-status-ls-nkat-signal-1"></a>
### STATUS_LS_NKAT_SIGNAL_1

Lambdasonde 1 nach Kat MW_LSH1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_NKAT_SIGNAL_1_WERT | real | Ergebnis |
| STAT_LS_NKAT_SIGNAL_1_EINH | string | Einheit |

<a id="job-status-l-sonde-h"></a>
### STATUS_L_SONDE_H

Lambdasonde 1 nach Kat MW_LSH1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_L_SONDE_H_WERT | real | Ergebnis |
| STATUS_L_SONDE_H_EINH | string | Einheit |

<a id="job-status-ls-nkat-signal-2"></a>
### STATUS_LS_NKAT_SIGNAL_2

Lambdasonde 2 nach Kat MW_LSH2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_NKAT_SIGNAL_2_WERT | real | Ergebnis |
| STAT_LS_NKAT_SIGNAL_2_EINH | string | Einheit |

<a id="job-status-l-sonde-2-h"></a>
### STATUS_L_SONDE_2_H

Lambdasonde 2 nach Kat MW_LSH2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_L_SONDE_2_H_WERT | real | Ergebnis |
| STATUS_L_SONDE_2_H_EINH | string | Einheit |

<a id="job-status-ls-vkat-signal-1"></a>
### STATUS_LS_VKAT_SIGNAL_1

Lambdasonde 1 vor Kat MW_LSV1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_VKAT_SIGNAL_1_WERT | real | Ergebnis |
| STAT_LS_VKAT_SIGNAL_1_EINH | string | Einheit |

<a id="job-status-l-sonde"></a>
### STATUS_L_SONDE

Lambdasonde 1 vor Kat MW_LSV1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_L_SONDE_WERT | real | Ergebnis |
| STATUS_L_SONDE_EINH | string | Einheit |

<a id="job-status-ls-vkat-signal-2"></a>
### STATUS_LS_VKAT_SIGNAL_2

Lambdasonde 2 vor Kat MW_LSV2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LS_VKAT_SIGNAL_2_WERT | real | Ergebnis |
| STAT_LS_VKAT_SIGNAL_2_EINH | string | Einheit |

<a id="job-status-l-sonde-2"></a>
### STATUS_L_SONDE_2

Lambdasonde 2 vor Kat MW_LSV2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_L_SONDE_2_WERT | real | Ergebnis |
| STATUS_L_SONDE_2_EINH | string | Einheit |

<a id="job-status-pwg-poti-spannung"></a>
### STATUS_PWG_POTI_SPANNUNG

Spannung PWG Kanal 1 MW_UPWG1M

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PWG_POTI_SPANNUNG_1_WERT | real | Ergebnis |
| STAT_ROHWERT1 | int | Ergebnis |
| STAT_ROHWERT2 | int | Ergebnis |
| STAT_PWG_POTI_SPANNUNG_EINH | string | Einheit |

<a id="job-status-lmm-masse"></a>
### STATUS_LMM_MASSE

Luftmasse MW_ML

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_LMM_MASSE_WERT | real | Ergebnis |
| STAT_LMM_MASSE_WERT | real | Ergebnis |
| STAT_LMM_MASSE_EINH | string | Einheit |

<a id="job-status-lmm"></a>
### STATUS_LMM

Luftmasse MW_ML

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_LMM_WERT | real | Ergebnis |
| STATUS_LMM_EINH | string | Einheit |

<a id="job-status-lambda-mul-1"></a>
### STATUS_LAMBDA_MUL_1

Adaption Multiplikativ Bank 1 (Lambdaadaptionsfaktor 1) MW_MUL1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAMBDA_MUL_1_WERT | real | Ergebnis |
| STAT_LAMBDA_MUL_1_EINH | string | Einheit |

<a id="job-status-mul"></a>
### STATUS_MUL

Adaption Multiplikativ Bank 1 (Lambdaadaptionsfaktor 1) MW_MUL1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_MUL_WERT | real | Ergebnis |
| STATUS_MUL_EINH | string | Einheit |

<a id="job-status-lambda-mul-2"></a>
### STATUS_LAMBDA_MUL_2

Adaption Multiplikativ Bank 2 (Lambdaadaptionsfaktor 2) MW_MUL2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAMBDA_MUL_2_WERT | real | Ergebnis |
| STAT_LAMBDA_MUL_2_EINH | string | Einheit |

<a id="job-status-mul-2"></a>
### STATUS_MUL_2

Adaption Multiplikativ Bank 2 (Lambdaadaptionsfaktor 2) MW_MUL2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_MUL_2_WERT | real | Ergebnis |
| STATUS_MUL_2_EINH | string | Einheit |

<a id="job-status-motordrehzahl"></a>
### STATUS_MOTORDREHZAHL

Drehzahl n MW_N

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_MOTORDREHZAHL_WERT | real | Ergebnis |
| STAT_MOTORDREHZAHL_WERT | real | Ergebnis |
| STAT_MOTORDREHZAHL_EINH | string | Einheit |

<a id="job-status-nmax"></a>
### STATUS_NMAX

Maximaldrehzahl n MW_NMAX

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_NMAX_WERT | real | Ergebnis |
| STAT_NMAX_EINH | string | Einheit |

<a id="job-status-n-ll-soll"></a>
### STATUS_N_LL_SOLL

Leerlaufregler Solldrehzahl MW_N_LL_SOLL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_N_LL_SOLL_WERT | real | Ergebnis |
| STAT_N_LL_SOLL_EINH | string | Einheit |

<a id="job-status-pumg-intern"></a>
### STATUS_PUMG_INTERN

Umgebungsdruck (intern) MW_PUMG_INTERN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_PUMG_INTERN_WERT | real | Ergebnis |
| STAT_PUMG_INTERN_EINH | string | Einheit |

<a id="job-status-rf"></a>
### STATUS_RF

relative Fuellung MW_RF

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_RF_WERT | real | Ergebnis |
| STAT_RF_EINH | string | Einheit |

<a id="job-status-tabg"></a>
### STATUS_TABG

Abgastemperatur MW_TABG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TABG_WERT | real | Ergebnis |
| STAT_TABG_EINH | string | Einheit |

<a id="job-status-an-lufttemperatur"></a>
### STATUS_AN_LUFTTEMPERATUR

Ansauglufttemperatursensor MW_TANS

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_AN_LUFTTEMPERATUR_WERT | real | Ergebnis |
| STAT_AN_LUFTTEMPERATUR_WERT | real | Ergebnis |
| STAT_AN_LUFTTEMPERATUR_EINH | string | Einheit |

<a id="job-status-einspritzzeit"></a>
### STATUS_EINSPRITZZEIT

Einspritzzeit Zylinder 1 MW_TI1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_EINSPRITZZEIT_WERT | real | Ergebnis |
| STAT_EINSPRITZZEIT_EINH | string | Einheit |

<a id="job-status-ti2"></a>
### STATUS_TI2

Einspritzzeit Zylinder 2 MW_TI2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TI2_WERT | real | Ergebnis |
| STAT_TI2_EINH | string | Einheit |

<a id="job-status-ti3"></a>
### STATUS_TI3

Einspritzzeit Zylinder 3 MW_TI3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TI3_WERT | real | Ergebnis |
| STAT_TI3_EINH | string | Einheit |

<a id="job-status-ti4"></a>
### STATUS_TI4

Einspritzzeit Zylinder 4 MW_TI4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TI4_WERT | real | Ergebnis |
| STAT_TI4_EINH | string | Einheit |

<a id="job-status-ti5"></a>
### STATUS_TI5

Einspritzzeit Zylinder 5 MW_TI5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TI5_WERT | real | Ergebnis |
| STAT_TI5_EINH | string | Einheit |

<a id="job-status-ti6"></a>
### STATUS_TI6

Einspritzzeit Zylinder 6 MW_TI6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TI6_WERT | real | Ergebnis |
| STAT_TI6_EINH | string | Einheit |

<a id="job-lesen-systemcheck-dmtl"></a>
### LESEN_SYSTEMCHECK_DMTL

Ergebnis Funktionsueberpruefung DMTL abrufen

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string |  |
| LESEN_SYSTEMCHECK_DMTL_STATUS | string | Status als Text |
| LESEN_SYSTEMCHECK_DMTL_STATUS_WERT | int | Status als Wert |

<a id="job-status-ti7"></a>
### STATUS_TI7

Einspritzzeit Zylinder 7 MW_TI7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TI7_WERT | real | Ergebnis |
| STAT_TI7_EINH | string | Einheit |

<a id="job-status-ti8"></a>
### STATUS_TI8

Einspritzzeit Zylinder 8 MW_TI8

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TI8_WERT | real | Ergebnis |
| STAT_TI8_EINH | string | Einheit |

<a id="job-status-ti-aus-ist"></a>
### STATUS_TI_AUS_IST

Ausblendzaehler Einspritzung Ist MW_TI_AUS_IST

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TI_AUS_IST_WERT | real | Ergebnis |
| STAT_TI_AUS_IST_EINH | string | Einheit |

<a id="job-status-kuehlw-ausl-temperatur"></a>
### STATUS_KUEHLW_AUSL_TEMPERATUR

Kuehleraustrittstemperatur MW_TKA

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_KUEHLW_AUSL_TEMPERATUR_WERT | real | Ergebnis |
| STAT_KUEHLW_AUSL_TEMPERATUR_EINH | string | Einheit |

<a id="job-status-last"></a>
### STATUS_LAST

Lastsignal MW_TL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_LAST_WERT | real | Ergebnis |
| STAT_LAST_EINH | string | Einheit |

<a id="job-status-motortemperatur"></a>
### STATUS_MOTORTEMPERATUR

Motortemperatursensor MW_TMOT

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_MOTORTEMPERATUR_WERT | real | Ergebnis |
| STAT_MOTORTEMPERATUR_WERT | real | Ergebnis |
| STAT_MOTORTEMPERATUR_EINH | string | Einheit |

<a id="job-status-tnmax"></a>
### STATUS_TNMAX

Gesamtzeit Ueberdrehzahl n MW_TNMAX

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TNMAX_WERT | real | Ergebnis |
| STAT_TNMAX_EINH | string | Einheit |

<a id="job-status-oel-temperatur"></a>
### STATUS_OEL_TEMPERATUR

Oeltemperatur (TOG) MW_TOEL

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_OEL_TEMPERATUR_WERT | real | Ergebnis |
| STAT_OEL_TEMPERATUR_EINH | string | Einheit |

<a id="job-status-tumg"></a>
### STATUS_TUMG

Umgebungstemperatur MW_TUMG

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TUMG_WERT | real | Ergebnis |
| STAT_TUMG_EINH | string | Einheit |

<a id="job-status-tv-tev"></a>
### STATUS_TV_TEV

Tastverhaeltnis Tankentlueftungsventil MW_TV_TEV

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TV_TEV_WERT | real | Ergebnis |
| STAT_TV_TEV_EINH | string | Einheit |

<a id="job-status-tz1"></a>
### STATUS_TZ1

Zuendwinkel Zylinder 1 MW_TZ1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TZ1_WERT | real | Ergebnis |
| STAT_TZ1_EINH | string | Einheit |

<a id="job-status-tz2"></a>
### STATUS_TZ2

Zuendwinkel Zylinder 2 MW_TZ2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TZ2_WERT | real | Ergebnis |
| STAT_TZ2_EINH | string | Einheit |

<a id="job-status-tz3"></a>
### STATUS_TZ3

Zuendwinkel Zylinder 3 MW_TZ3

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TZ3_WERT | real | Ergebnis |
| STAT_TZ3_EINH | string | Einheit |

<a id="job-status-tz4"></a>
### STATUS_TZ4

Zuendwinkel Zylinder 4 MW_TZ4

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TZ4_WERT | real | Ergebnis |
| STAT_TZ4_EINH | string | Einheit |

<a id="job-status-tz5"></a>
### STATUS_TZ5

Zuendwinkel Zylinder 5 MW_TZ5

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TZ5_WERT | real | Ergebnis |
| STAT_TZ5_EINH | string | Einheit |

<a id="job-status-tz6"></a>
### STATUS_TZ6

Zuendwinkel Zylinder 6 MW_TZ6

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TZ6_WERT | real | Ergebnis |
| STAT_TZ6_EINH | string | Einheit |

<a id="job-status-tz7"></a>
### STATUS_TZ7

Zuendwinkel Zylinder 7 MW_TZ7

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TZ7_WERT | real | Ergebnis |
| STAT_TZ7_EINH | string | Einheit |

<a id="job-status-tz8"></a>
### STATUS_TZ8

Zuendwinkel Zylinder 8 MW_TZ8

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_TZ8_WERT | real | Ergebnis |
| STAT_TZ8_EINH | string | Einheit |

<a id="job-status-ubatt"></a>
### STATUS_UBATT

Bordnetzspannung Hauptrelais MW_UBHR

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STATUS_UBATT_WERT | real | Ergebnis |
| STAT_UBATT_WERT | real | Ergebnis |
| STAT_UBATT_EINH | string | Einheit |

<a id="job-status-uext1"></a>
### STATUS_UEXT1

Sensorversorgung 1 (Master) MW_UEXT1

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_UEXT1_WERT | real | Ergebnis |
| STAT_UEXT1_EINH | string | Einheit |

<a id="job-status-uext2"></a>
### STATUS_UEXT2

Sensorversorgung 2 (Slave) MW_UEXT2

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_UEXT2_WERT | real | Ergebnis |
| STAT_UEXT2_EINH | string | Einheit |

<a id="job-status-geschwindigkeit"></a>
### STATUS_GESCHWINDIGKEIT

Geschwindigkeit v MW_V

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_GESCHWINDIGKEIT_WERT | real | Ergebnis |
| STATUS_GESCHWINDIGKEIT_WERT | real | Ergebnis |
| STAT_GESCHWINDIGKEIT_EINH | string | Einheit |

<a id="job-status-v-can"></a>
### STATUS_V_CAN

Fahrzeuggeschwindigkeit v_asc (CAN) MW_V_CAN

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_V_CAN_WERT | real | Ergebnis |
| STAT_V_CAN_EINH | string | Einheit |

<a id="job-status-vmax"></a>
### STATUS_VMAX

Maximalgeschwindigkeit v MW_VMAX

_No arguments._

#### Results

| Name | Type | Comment |
| --- | --- | --- |
| JOB_STATUS | string | JOB_STATUS -&gt; OKAY, wenn fehlerfrei |
| STAT_VMAX_WERT | real | Ergebnis |
| STAT_VMAX_EINH | string | Einheit |

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

## Tables

### Index

- [BETRIEBSWTAB](#table-betriebswtab) (77 × 17)
- [BITS](#table-bits) (49 × 4)
- [FORTTEXTE](#table-forttexte) (227 × 6)
- [PROGRESULT](#table-progresult) (16 × 2)
- [FARTMATRIX](#table-fartmatrix) (79 × 17)
- [FARTTEXTE](#table-farttexte) (63 × 2)
- [FUMWELTTEXTE](#table-fumwelttexte) (75 × 5)
- [NULLEINSTEXTE](#table-nulleinstexte) (4 × 3)
- [JOBRESULT](#table-jobresult) (8 × 2)
- [IORESULT](#table-ioresult) (6 × 2)
- [CODIER_CS](#table-codier-cs) (8 × 2)
- [LDPSTATUS](#table-ldpstatus) (59 × 3)
- [SLSSTATUS](#table-slsstatus) (6 × 3)

<a id="table-betriebswtab"></a>
### BETRIEBSWTAB

Dimensions: 77 rows × 17 columns

| NAME | TELEGRAM | POS_ADR | LEN_ADR | ADR | BYTE | DATA_TYPE | COMPU_TYPE | FACT_A | FACT_B | MASK | VALUE | ANZ | MEAS | RANGE | JOBNAME | LNAME |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| mw_add1 | 12050B06 | 04 | 0 | 0x00 | 11 | 7 | -- | 0.002 | 0 | 0x00 | 0x00 | 6.2f | ms |   | ADD | Adaption Additiv Bank 1 (Lambdaadaptionsoffset 1) |
| mw_add1 | 12050B06 | 04 | 0 | 0x00 | 11 | 7 | -- | 0.002 | 0 | 0x00 | 0x00 | 6.2f | ms |   | LAMBDA_ADD_1 | Adaption Additiv Bank 1 (Lambdaadaptionsoffset 1) |
| mw_add2 | 12050B06 | 04 | 0 | 0x00 | 13 | 7 | -- | 0.002 | 0 | 0x00 | 0x00 | 6.2f | ms |   | ADD_2 | Adaption Additiv Bank 2 (Lambdaadaptionsoffset 2) |
| mw_add2 | 12050B06 | 04 | 0 | 0x00 | 13 | 7 | -- | 0.002 | 0 | 0x00 | 0x00 | 6.2f | ms |   | LAMBDA_ADD_2 | Adaption Additiv Bank 2 (Lambdaadaptionsoffset 2) |
| mw_avanos1_ist | 12050B23 | 04 | 0 | 0x00 | 9 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | AVANOS1_IST | Auslass-VANOS Bank 1 ist |
| mw_avanos2_ist | 12050B23 | 04 | 0 | 0x00 | 17 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | AVANOS2_IST | Auslass-VANOS Bank 2 ist |
| mw_avanos1_soll | 12050B23 | 04 | 0 | 0x00 | 11 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | AVANOS1_SOLL | Auslass-VANOS Bank 1 soll |
| mw_avanos2_soll | 12050B23 | 04 | 0 | 0x00 | 19 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | AVANOS2_SOLL | Auslass-VANOS Bank 2 soll |
| mw_aqrel | 12050B03 | 04 | 0 | 0x00 | 23 | 5 | -- | 0.003051757 | 0 | 0x00 | 0x00 | 6.2f | % |   | AQREL | relativer Oeffnungsquerschnitt |
| mw_dkist | 12050B03 | 04 | 0 | 0x00 | 30 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | % |   | DKP_WINKEL | Drosselklappensteller Istwert |
| mw_dksoll | 12050B03 | 04 | 0 | 0x00 | 34 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | % |   | DKP_WINKEL_SOLL | Drosselklappensteller Sollwert |
| mw_evanos1_ist | 12050B23 | 04 | 0 | 0x00 | 5 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | EVANOS1_IST | Einlass-VANOS Bank 1 ist |
| mw_evanos2_ist | 12050B23 | 04 | 0 | 0x00 | 13 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | EVANOS2_IST | Einlass-VANOS Bank 2 ist |
| mw_evanos1_soll | 12050B23 | 04 | 0 | 0x00 | 7 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | EVANOS1_SOLL | Einlass-VANOS Bank 1 soll |
| mw_evanos2_soll | 12050B23 | 04 | 0 | 0x00 | 15 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | EVANOS2_SOLL | Einlass-VANOS Bank 2 soll |
| mw_fwg1 | 12050B03 | 04 | 0 | 0x00 | 26 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | % |   | PWG_POTI_WINKEL | Fahrpedalwertgeber Kanal 1 |
| mw_fwg2 | 12050B03 | 04 | 0 | 0x00 | 28 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | % |   | PWG_POTI_WINKEL_2 | Fahrpedalwertgeber Kanal 2 |
| mw_lambda1 | 12050B13 | 04 | 0 | 0x00 | 43 | 5 | -- | 0.000030517 | 0 | 0x00 | 0x00 | 6.2f | [1] |   | LAMBDA_INTEGRATOR_1 | Lambdaregler 1 Regelfaktor |
| mw_lambda1 | 12050B13 | 04 | 0 | 0x00 | 43 | 5 | -- | 0.000030517 | 0 | 0x00 | 0x00 | 6.2f | [1] |   | INT | Lambdaregler 1 Regelfaktor |
| mw_lambda2 | 12050B13 | 04 | 0 | 0x00 | 45 | 5 | -- | 0.000030517 | 0 | 0x00 | 0x00 | 6.2f | [1] |   | LAMBDA_INTEGRATOR_2 | Lambdaregler 2 Regelfaktor |
| mw_lambda2 | 12050B13 | 04 | 0 | 0x00 | 45 | 5 | -- | 0.000030517 | 0 | 0x00 | 0x00 | 6.2f | [1] |   | INT2 | Lambdaregler 2 Regelfaktor |
| mw_lfr_ko | 12050B06 | 04 | 0 | 0x00 | 40 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Nm |   | LFR_KO | Leerlaufregleradaption mit Kompressor |
| mw_lfr | 12050B06 | 04 | 0 | 0x00 | 38 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Nm |   | LFR | Leerlaufregleradaption ohne Kompressor |
| mw_lsh1 | 12050B02 | 04 | 0 | 0x00 | 53 | 5 | -- | 0.001088 | 0 | 0x00 | 0x00 | 6.2f | V |   | LS_NKAT_SIGNAL_1 | Lambdasonde 1 nach Kat |
| mw_lsh1 | 12050B02 | 04 | 0 | 0x00 | 53 | 5 | -- | 0.001088 | 0 | 0x00 | 0x00 | 6.2f | V |   | L_SONDE_H | Lambdasonde 1 nach Kat |
| mw_lsh2 | 12050B02 | 04 | 0 | 0x00 | 55 | 5 | -- | 0.001088 | 0 | 0x00 | 0x00 | 6.2f | V |   | LS_NKAT_SIGNAL_2 | Lambdasonde 2 nach Kat |
| mw_lsh2 | 12050B02 | 04 | 0 | 0x00 | 55 | 5 | -- | 0.001088 | 0 | 0x00 | 0x00 | 6.2f | V |   | L_SONDE_2_H | Lambdasonde 2 nach Kat |
| mw_lsv1 | 12050B02 | 04 | 0 | 0x00 | 49 | 5 | -- | 0.001088 | 0 | 0x00 | 0x00 | 6.2f | V |   | LS_VKAT_SIGNAL_1 | Lambdasonde 1 vor Kat |
| mw_lsv1 | 12050B02 | 04 | 0 | 0x00 | 49 | 5 | -- | 0.001088 | 0 | 0x00 | 0x00 | 6.2f | V |   | L_SONDE | Lambdasonde 1 vor Kat |
| mw_lsv2 | 12050B02 | 04 | 0 | 0x00 | 51 | 5 | -- | 0.001088 | 0 | 0x00 | 0x00 | 6.2f | V |   | LS_VKAT_SIGNAL_2 | Lambdasonde 2 vor Kat |
| mw_lsv2 | 12050B02 | 04 | 0 | 0x00 | 51 | 5 | -- | 0.001088 | 0 | 0x00 | 0x00 | 6.2f | V |   | L_SONDE_2 | Lambdasonde 2 vor Kat |
| mw_upwg1m | 12050B02 | 04 | 0 | 0x00 | 21 | 5 | -- | 0.004883 | 0 | 0x00 | 0x00 | 6.2f | V |   | PWG_POTI_SPANNUNG | Spannung PWG Kanal 1 |
| mw_ml | 12050B03 | 04 | 0 | 0x00 | 7 | 5 | -- | 0.25 | 0 | 0x00 | 0x00 | 6.2f | kg/h |   | LMM_MASSE | Luftmasse |
| mw_mul1 | 12050B06 | 04 | 0 | 0x00 | 7 | 5 | -- | 0.000030517 | 0 | 0x00 | 0x00 | 6.2f | [1] |   | LAMBDA_MUL_1 | Adaption Multiplikativ Bank 1 (Lambdaadaptionsfaktor 1) |
| mw_mul1 | 12050B06 | 04 | 0 | 0x00 | 7 | 5 | -- | 0.000030517 | 0 | 0x00 | 0x00 | 6.2f | [1] |   | MUL | Adaption Multiplikativ Bank 1 (Lambdaadaptionsfaktor 1) |
| mw_mul2 | 12050B06 | 04 | 0 | 0x00 | 9 | 5 | -- | 0.000030517 | 0 | 0x00 | 0x00 | 6.2f | [1] |   | LAMBDA_MUL_2 | Adaption Multiplikativ Bank 2 (Lambdaadaptionsfaktor 2) |
| mw_mul2 | 12050B06 | 04 | 0 | 0x00 | 9 | 5 | -- | 0.000030517 | 0 | 0x00 | 0x00 | 6.2f | [1] |   | MUL_2 | Adaption Multiplikativ Bank 2 (Lambdaadaptionsfaktor 2) |
| mw_n | 12050B03 | 04 | 0 | 0x00 | 3 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min |   | MOTORDREHZAHL | Drehzahl n |
| mw_nmax | 12050B06 | 04 | 0 | 0x00 | 19 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | km/h |   | NMAX | Maximaldrehzahl n |
| mw_n_ll_soll | 12050B03 | 04 | 0 | 0x00 | 5 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | 1/min |   | N_LL_SOLL | Leerlaufregler Solldrehzahl |
| mw_pumg_intern | 12050B03 | 04 | 0 | 0x00 | 22 | 2 | -- | 3 | 500 | 0x00 | 0x00 | 6.2f | mbar |   | PUMG_INTERN | Umgebungsdruck (intern) |
| mw_rf | 12050B03 | 04 | 0 | 0x00 | 11 | 5 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | % |   | RF | relative Fuellung |
| mw_tabg | 12050B03 | 04 | 0 | 0x00 | 17 | 2 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | Grad C |   | TABG | Abgastemperatur |
| mw_tans | 12050B03 | 04 | 0 | 0x00 | 13 | 2 | -- | 1 | -48 | 0x00 | 0x00 | 6.2f | Grad C |   | AN_LUFTTEMPERATUR | Ansauglufttemperatursensor |
| mw_ti1 | 12050B13 | 04 | 0 | 0x00 | 9 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | ms |   | EINSPRITZZEIT | Einspritzzeit Zylinder 1 |
| mw_ti2 | 12050B13 | 04 | 0 | 0x00 | 11 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | ms |   | TI2 | Einspritzzeit Zylinder 2 |
| mw_ti3 | 12050B13 | 04 | 0 | 0x00 | 13 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | ms |   | TI3 | Einspritzzeit Zylinder 3 |
| mw_ti4 | 12050B13 | 04 | 0 | 0x00 | 15 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | ms |   | TI4 | Einspritzzeit Zylinder 4 |
| mw_ti5 | 12050B13 | 04 | 0 | 0x00 | 17 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | ms |   | TI5 | Einspritzzeit Zylinder 5 |
| mw_ti6 | 12050B13 | 04 | 0 | 0x00 | 19 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | ms |   | TI6 | Einspritzzeit Zylinder 6 |
| mw_ti7 | 12050B13 | 04 | 0 | 0x00 | 21 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | ms |   | TI7 | Einspritzzeit Zylinder 7 |
| mw_ti8 | 12050B13 | 04 | 0 | 0x00 | 23 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | ms |   | TI8 | Einspritzzeit Zylinder 8 |
| mw_ti_aus_ist | 12050B13 | 04 | 0 | 0x00 | 7 | 2 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | [1] |   | TI_AUS_IST | Ausblendzaehler Einspritzung Ist |
| servo_i_ist | 12050B13 | 04 | 0 | 0x00 | 51 | 5 | -- | 0.89 | 0 | 0x00 | 0x00 | 6.2f | mA |   | STATUS_ANALOG_GM3 | Ist Strom Servotronikventil |
| servo_i_soll | 12050B13 | 04 | 0 | 0x00 | 55 | 5 | -- | 0.89 | 0 | 0x00 | 0x00 | 6.2f | mA |   | STATUS_ANALOG_GM3 | Soll Strom Servotronikventil |
| ll_abw | 12050B15 | 04 | 0 | 0x00 | 33 | 7 | -- | 0.001525878906 | 0 | 0x00 | 0x00 | 6.2f | % |   | STATUS_ANALOG_GM3 | Soll Strom Servotronikventil |
| mw_tka | 12050B03 | 04 | 0 | 0x00 | 16 | 2 | -- | 1 | -48 | 0x00 | 0x00 | 6.2f | GradC |   | KUEHLW_AUSL_TEMPERATUR | Kuehleraustrittstemperatur |
| mw_tl | 12050B03 | 04 | 0 | 0x00 | 9 | 5 | -- | 0.001 | 0 | 0x00 | 0x00 | 6.2f | ms |   | LAST | Lastsignal |
| mw_tmot | 12050B03 | 04 | 0 | 0x00 | 14 | 2 | -- | 1 | -48.0 | 0x00 | 0x00 | 6.2f | Grad C |   | MOTORTEMPERATUR | Motortemperatursensor |
| mw_tnmax | 12050B06 | 04 | 0 | 0x00 | 21 | 5 | -- | 0.000976562 | 0 | 0x00 | 0x00 | 6.2f | s |   | TNMAX | Gesamtzeit Ueberdrehzahl n |
| mw_toel | 12050B03 | 04 | 0 | 0x00 | 15 | 2 | -- | 1 | -48.0 | 0x00 | 0x00 | 6.2f | Grad C |   | OEL_TEMPERATUR | Oeltemperatur (TOG) |
| mw_tumg | 12050B03 | 04 | 0 | 0x00 | 18 | 2 | -- | 1 | -48 | 0x00 | 0x00 | 6.2f | Grad C |   | TUMG | Umgebungstemperatur |
| mw_tv_tev | 12050B13 | 04 | 0 | 0x00 | 41 | 5 | -- | 0.002 | 0 | 0x00 | 0x00 | 6.2f | ms |   | TV_TEV | Tastverhaeltnis Tankentlueftungsventil |
| mw_tz1 | 12050B13 | 04 | 0 | 0x00 | 25 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | TZ1 | Zuendwinkel Zylinder 1 |
| mw_tz2 | 12050B13 | 04 | 0 | 0x00 | 27 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | TZ2 | Zuendwinkel Zylinder 2 |
| mw_tz3 | 12050B13 | 04 | 0 | 0x00 | 29 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | TZ3 | Zuendwinkel Zylinder 3 |
| mw_tz4 | 12050B13 | 04 | 0 | 0x00 | 31 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | TZ4 | Zuendwinkel Zylinder 4 |
| mw_tz5 | 12050B13 | 04 | 0 | 0x00 | 33 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | TZ5 | Zuendwinkel Zylinder 5 |
| mw_tz6 | 12050B13 | 04 | 0 | 0x00 | 35 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | TZ6 | Zuendwinkel Zylinder 6 |
| mw_tz7 | 12050B13 | 04 | 0 | 0x00 | 37 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | TZ7 | Zuendwinkel Zylinder 7 |
| mw_tz8 | 12050B13 | 04 | 0 | 0x00 | 39 | 7 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | Grad KW |   | TZ8 | Zuendwinkel Zylinder 8 |
| mw_ubhr | 12050B03 | 04 | 0 | 0x00 | 19 | 2 | -- | 0.1 | 0 | 0x00 | 0x00 | 6.2f | V |   | UBATT | Bordnetzspannung Hauptrelais |
| mw_uext1 | 12050B03 | 04 | 0 | 0x00 | 20 | 2 | -- | 0.0391 | 0 | 0x00 | 0x00 | 6.2f | V |   | UEXT1 | Sensorversorgung 1 (Master) |
| mw_uext2 | 12050B03 | 04 | 0 | 0x00 | 21 | 2 | -- | 0.0391 | 0 | 0x00 | 0x00 | 6.2f | V |   | UEXT2 | Sensorversorgung 2 (Slave) |
| mw_v | 12050B13 | 04 | 0 | 0x00 | 3 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | km/h |   | GESCHWINDIGKEIT | Geschwindigkeit v |
| mw_v_can | 12050B13 | 04 | 0 | 0x00 | 5 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | km/h |   | V_CAN | Fahrzeuggeschwindigkeit v_asc (CAN) |
| mw_vmax | 12050B06 | 04 | 0 | 0x00 | 17 | 5 | -- | 1 | 0 | 0x00 | 0x00 | 6.2f | km/h |   | VMAX | Maximalgeschwindigkeit v |

<a id="table-bits"></a>
### BITS

Dimensions: 49 rows × 4 columns

| NAME | BYTE | MASK | VALUE |
| --- | --- | --- | --- |
| BA | 22 | 0x0f | 0x00 |
| SA | 21 | 0x08 | 0x08 |
| LSHV1 | 15 | 0x02 | 0x02 |
| LSHV2 | 16 | 0x02 | 0x02 |
| LSHN1 | 17 | 0x02 | 0x02 |
| LSHN2 | 18 | 0x02 | 0x02 |
| TZ1 | 19 | 0x01 | 0x01 |
| TZ2 | 19 | 0x02 | 0x02 |
| TZ3 | 19 | 0x04 | 0x04 |
| TZ4 | 19 | 0x08 | 0x08 |
| TZ5 | 19 | 0x10 | 0x10 |
| TZ6 | 19 | 0x20 | 0x20 |
| TZ7 | 19 | 0x40 | 0x40 |
| TZ8 | 19 | 0x80 | 0x80 |
| AKL | 10 | 0x40 | 0x40 |
| ELU | 9 | 0x40 | 0x40 |
| EKP | 8 | 0x40 | 0x40 |
| SLP | 6 | 0x40 | 0x40 |
| SLV | 7 | 0x40 | 0x40 |
| KKOS | 1 | 0x40 | 0x40 |
| KLOPF | 14 | 0x02 | 0x02 |
| SCHUTZ | 14 | 0x01 | 0x01 |
| REGEL | 14 | 0x04 | 0x04 |
| NOISE | 23 | 0x80 | 0x80 |
| S_GANG | 24 | 0x08 | 0x00 |
| S_KL15 | 24 | 0x20 | 0x20 |
| M_SS | 0 | 0x01 | 0x01 |
| M_STRT | 0 | 0x02 | 0x02 |
| M_LL | 0 | 0x04 | 0x04 |
| M_TL | 0 | 0x08 | 0x08 |
| M_VL | 0 | 0x10 | 0x10 |
| M_ZA | 0 | 0x20 | 0x20 |
| M_NL | 0 | 0x40 | 0x20 |
| KATH | 3 | 0x0f | 0x00 |
| S_KL50 | 30 | 0x80 | 0x80 |
| S_BLS | 24 | 0x10 | 0x10 |
| S_BLTS | 24 | 0x04 | 0x04 |
| S_KUP | 24 | 0x08 | 0x08 |
| EWS3 | 27 | 0x80 | 0x80 |
| S_FDYN | 30 | 0x01 | 0x01 |
| MIL | 26 | 0x80 | 0x80 |
| SMFL1 | 32 | 0x01 | 0x01 |
| SMFL2 | 32 | 0x02 | 0x02 |
| SMFL3 | 32 | 0x03 | 0x03 |
| SMFL4 | 32 | 0x04 | 0x04 |
| LLR | 13 | 0x01 | 0x01 |
| LDR1 | 35 | 0x01 | 0x01 |
| LDR2 | 36 | 0x01 | 0x01 |
| FGR | 12 | 0x01 | 0x01 |

<a id="table-forttexte"></a>
### FORTTEXTE

Dimensions: 227 rows × 6 columns

| ORT | ORTTEXT | UW_1 | UW_2 | UW_3 | UW_4 |
| --- | --- | --- | --- | --- | --- |
| 0xF7 | VANOS Druckspeicherventil | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x83 | DSC-Eingriff unplausibel | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x84 | Timeout DSC-Botschaft | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x85 | Timeout LWS-Botschaft | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x86 | Timeout KOMBI-Botschaft | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x87 | Beide V-Signalquellen | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x8D | Fuellstandsplausibilisierung | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x8E | interner Index 7 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x8F | E-Box-Luefter | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x69 | Plausibilisierung Motortemperatur | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x02 | Schliesserwicklung Leerlaufsteller | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x1D | Oeffnerwicklung Leerlaufsteller | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x9B | intern: Adaptions-EEPROM Master | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x96 | intern: Speichertest Master | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x6A | Bremslichtschalter | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x09 | Klopfsensor 1 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x46 | Klopfsensor 2 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x45 | Klopfsensor 3 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x47 | Klopfsensor 4 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x2A | Geschwindigkeitseingang direkt | 0x00 | 0x01 | 0x04 | 0x03 |
| 0x97 | intern: Treiberdiagnosekette | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x98 | intern: Kommunikation Master | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x56 | CAN-Bus DME | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x88 | Leerlaufregler | 0x00 | 0x01 | 0x07 | 0x06 |
| 0x4F | Abgastemperatursensor | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x89 | Saugstrahlpumpe | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x8A | Differentialsperre | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x8B | Tempomatsystem | 0x00 | 0x01 | 0x0A | 0x03 |
| 0x8C | Motorgeraeusch | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x9F | Klopfbaustein 1 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xA0 | Klopfbaustein 2 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xA1 | intern: Klopfsignalpfad | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xA2 | NW-Geber 2 Synchronisation gegen KW | 0x00 | 0x01 | 0x08 | 0x09 |
| 0x4C | intern: Umgebungsdrucksensor | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xA3 | intern: SG-Resets | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x14 | Startrelais | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x4D | Ansauglufttemperaturfuehler | 0x00 | 0x01 | 0x0A | 0x03 |
| 0x4E | Kuehlwassertemperaturfuehler | 0x00 | 0x01 | 0x0B | 0x03 |
| 0x49 | Luftmasse zu DKG-Stellung unplausibel | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x6B | EGAS-Steller Selbsttest | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x3A | Sensorversorgung 1 Master | 0x00 | 0x01 | 0x0D | 0x03 |
| 0x3B | Sensorversorgung 2 Master | 0x00 | 0x01 | 0x0E | 0x03 |
| 0x30 | Klimakompressorrelais | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x29 | Luftmassenmesser 1 | 0x00 | 0x01 | 0x12 | 0x03 |
| 0x39 | Luftmassenmesser 2 | 0x00 | 0x01 | 0x12 | 0x03 |
| 0x6C | Oelkreisventil links | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x6D | Oelkreisventil rechts | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x08 | EVANOS2-Hallgeber | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x0B | AVANOS2-Hallgeber | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x4A | EVANOS2-Fruehventil | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x4B | EVANOS2-Spaetventil | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x53 | AVANOS2-Fruehventil | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x54 | AVANOS2-Spaetventil | 0x00 | 0x11 | 0x02 | 0x03 |
| 0xAC | Vanos-Druckspeicherventil | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x51 | MFL-Schnittstelle | 0x10 | 0x04 | 0x0A | 0x03 |
| 0x6F | Pedalwert 1 Vergleich | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x70 | Pedalwert 2 Vergleich | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x71 | EVANOS2-Regelung | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x72 | AVANOS2-Regelung | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x73 | intern: Steuergeraetetemperatur | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x74 | Servotronikventil Strommessung | 0x00 | 0x04 | 0x02 | 0x03 |
| 0x75 | Servotronik Geschwindigkeitssignal | 0x00 | 0x04 | 0x02 | 0x03 |
| 0x76 | Drosselklappenpoti 1 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x77 | Drosselklappenpoti 2 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x78 | Vergleich Drosselklappenpoti 1 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x79 | Vergleich Drosselklappenpoti 2 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x13 | Relais Sekundaerluftpumpe | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x3F | Sekundaerluftventil | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xAA | Sekundaerluft Mindestdurchfluss | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xAB | Sekundaerluft Ventil klemmt | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x52 | Abgasklappe | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xAD | KL50 Anlasserschalter0 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x80 | Abweichung Leerlaufdrehzahl | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x81 | interner Index 73 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xDE | interner Index 74 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xDF | interner Index 75 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xE0 | interner Index 76 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xE1 | interner Index 77 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xE2 | interner Index 78 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xE3 | interner Index 79 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xE4 | EGAS-Steller | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xE5 | EGAS-Regelung | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xE6 | EGAS-Soll-Ist-Vergleich | 0x0F | 0x10 | 0x02 | 0x03 |
| 0xE7 | intern: Prozessorkontrolle Slave | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xE8 | interner Index 84 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xE9 | interner Index 85 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x68 | interner Index 86 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x99 | interner Index 87 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x9A | interner Index 88 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xDD | interner Index 89 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x3C | Pedalwertgeber 1 | 0x00 | 0x01 | 0x0D | 0x03 |
| 0x3D | Pedalwertgeber 2 | 0x00 | 0x01 | 0x0E | 0x03 |
| 0x55 | EDK-Geber | 0x00 | 0x01 | 0x17 | 0x03 |
| 0x2D | EDK-Hardware | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x2C | Signal aktiver Oelniveaugeber | 0x00 | 0x01 | 0x02 | 0x12 |
| 0x31 | interner Index 95 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x38 | interner Index 96 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x3E | interner Index 97 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x40 | interner Index 98 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xA4 | interner Index 99 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xA5 | interner Index 100 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xA6 | interner Index 101 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xA7 | interner Index 102 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xA8 | interner Index 103 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xA9 | interner Index 104 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xAA | interner Index 105 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xAB | interner Index 106 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xAC | interner Index 107 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x35 | Elektroluefter | 0x00 | 0x0A | 0x0B | 0x03 |
| 0x82 | EWS-Signalmanipulation | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x10 | KW-Induktivgeber | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x9C | intern: Adaptions-EEPROM Slave | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x9D | intern: Speichertest Slave | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x2B | Kuehleraustrittstemperaturfuehler | 0x00 | 0x18 | 0x02 | 0x03 |
| 0x1E | Ueberwachung AD-Wandler | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x01 | Relais Kraftstoffpumpe | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x7A | intern: Prozessorkontrolle Master | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x36 | Bordnetzspannung Hauptrelais | 0x00 | 0x01 | 0x02 | 0x0D |
| 0x7E | EKP-Crash-Abschaltung | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x0D | Lambdasonde 1 vor Kat | 0x00 | 0x01 | 0x1C | 0x03 |
| 0x0C | Lambdasonde 2 vor Kat | 0x00 | 0x01 | 0x1D | 0x03 |
| 0x24 | Tankentlueftungsventil | 0x00 | 0x01 | 0x19 | 0x35 |
| 0x41 | Drosselklappenpoti 2 Slave | 0x00 | 0x01 | 0x17 | 0x03 |
| 0x90 | Lambdaregler 1 | 0x00 | 0x01 | 0x2B | 0x2D |
| 0x91 | Lambdaregler 2 | 0x00 | 0x01 | 0x2C | 0x2E |
| 0x7B | Bus-Off lokaler SMG-CAN | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x07 | EVANOS1-Hallgeber | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x0A | AVANOS1-Hallgeber | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x43 | EVANOS1-Fruehventil | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x48 | EVANOS1-Spaetventil | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x16 | AVANOS1-Fruehventil | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x15 | AVANOS1-Spaetventil | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x7C | Aktives Motorlager | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x7D | Spoilerverstellung | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x6E | LED Fahrdynamikschalter | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x7F | Tankleckdiagnosepumpe | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x2E | Verbrauchssignalausgang KVA | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x2F | Drehzahlsignalausgang TD | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x06 | Timeout SMG-CAN | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x42 | EWS-Schnittstelle | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x03 | Einspritzventil 1 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x05 | Einspritzventil 2 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x04 | Einspritzventil 3 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x21 | Einspritzventil 4 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x1F | Einspritzventil 5 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x20 | Einspritzventil 6 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x22 | Einspritzventil 7 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x23 | Einspritzventil 8 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x50 | Schalterkette Kraftschluss | 0x00 | 0x01 | 0x05 | 0x03 |
| 0x9E | intern: Kommunikation Slave | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x1B | Tankleckdiagnoseventil | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xAE | Kraftstoffsystem LA-Faktor 1 | 0x00 | 0x01 | 0x02 | 0x2D |
| 0xAF | Kraftstoffsystem LA-Faktor 2 | 0x00 | 0x01 | 0x02 | 0x2E |
| 0xB0 | Kraftstoffsystem LA-Offset 1 | 0x00 | 0x01 | 0x02 | 0x29 |
| 0xB1 | Kraftstoffsystem LA-Offset 2 | 0x00 | 0x01 | 0x02 | 0x2A |
| 0xB2 | KAT-Konvertierung 1 | 0x00 | 0x01 | 0x2F | 0x33 |
| 0xB3 | KAT-Konvertierung 2 | 0x00 | 0x01 | 0x30 | 0x34 |
| 0xB4 | Tankleck | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xB5 | interner Index 179 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x1C | Regelung Kennfeldkuehlung | 0x00 | 0x0C | 0x02 | 0x03 |
| 0x12 | Steller Kennfeldkuehlung | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x57 | Lambdasonde 1 nach Kat | 0x00 | 0x01 | 0x1E | 0x03 |
| 0x58 | Lambdasonde 2 nach Kat | 0x00 | 0x01 | 0x1F | 0x03 |
| 0x25 | Lambdasondenhzg. 1 vor Kat | 0x00 | 0x01 | 0x20 | 0x03 |
| 0x26 | Lambdasondenhzg. 2 vor Kat | 0x00 | 0x01 | 0x21 | 0x03 |
| 0x27 | Lambdasondenhzg. 1 nach Kat | 0x00 | 0x01 | 0x22 | 0x03 |
| 0x28 | Lambdasondenhzg. 2 nach Kat | 0x00 | 0x01 | 0x23 | 0x03 |
| 0x0E | interner Index 188 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x5A | Lambdasondenalt. 1 vor Kat | 0x00 | 0x01 | 0x24 | 0x26 |
| 0x5B | Lambdasondenalt. 2 vor Kat | 0x00 | 0x01 | 0x25 | 0x27 |
| 0x5C | Lambdasondenalt. 1 nach Kat | 0x00 | 0x01 | 0x1E | 0x31 |
| 0x5D | Lambdasondenalt. 2 nach Kat | 0x00 | 0x01 | 0x1F | 0x32 |
| 0xB6 | Uebertemp. EV-Treiber 1 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xB7 | Uebertemp. EV-Treiber 2 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x64 | Reifendruck vorn links | 0x00 | 0x01 | 0x02 | 0x05 |
| 0x65 | Reifendruck vorn rechts | 0x00 | 0x01 | 0x02 | 0x05 |
| 0x66 | Reifendruck hinten rechts | 0x00 | 0x01 | 0x02 | 0x05 |
| 0x67 | Reifendruck hinten links | 0x00 | 0x01 | 0x02 | 0x05 |
| 0xB8 | EVANOS1-Regelung | 0x00 | 0x11 | 0x02 | 0x03 |
| 0xB9 | AVANOS1-Regelung | 0x00 | 0x11 | 0x02 | 0x03 |
| 0x19 | Zuendspule 1 | 0x00 | 0x01 | 0x11 | 0x03 |
| 0x17 | Zuendspule 2 | 0x00 | 0x01 | 0x11 | 0x03 |
| 0x18 | Zuendspule 3 | 0x00 | 0x01 | 0x11 | 0x03 |
| 0x32 | Zuendspule 4 | 0x00 | 0x01 | 0x11 | 0x03 |
| 0x34 | Zuendspule 5 | 0x00 | 0x01 | 0x11 | 0x03 |
| 0x33 | Zuendspule 6 | 0x00 | 0x01 | 0x11 | 0x03 |
| 0x37 | Zuendspule 7 | 0x00 | 0x01 | 0x11 | 0x03 |
| 0x1A | Zuendspule 8 | 0x00 | 0x01 | 0x11 | 0x03 |
| 0xC2 | interner Index 209 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xC3 | Ueberwachung Momentenmanager | 0x00 | 0x01 | 0x02 | 0x28 |
| 0xC4 | Aussetzer Zyl.1 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xC5 | Aussetzer Zyl.2 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xC6 | Aussetzer Zyl.3 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xC7 | Aussetzer Zyl.4 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xC8 | Aussetzer Zyl.5 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xC9 | Aussetzer Zyl.6 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xCA | Aussetzer Zyl.7 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xCB | Aussetzer Zyl.8 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xCC | Aussetzer mehr Zylinder | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xCD | Aussetzer Zyl.1 Warmlauf | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xCE | Aussetzer Zyl.2 Warmlauf | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xCF | Aussetzer Zyl.3 Warmlauf | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xD0 | Aussetzer Zyl.4 Warmlauf | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xD1 | Aussetzer Zyl.5 Warmlauf | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xD2 | Aussetzer Zyl.6 Warmlauf | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xD3 | Aussetzer Zyl.7 Warmlauf | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xD4 | Aussetzer Zyl.8 Warmlauf | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xD5 | Aussetzer mehr Zylinder Warmlauf | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xD6 | interner Index 229 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xD7 | interner Index 230 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xD8 | interner Index 231 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xD9 | interner Index 232 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xDA | interner Index 233 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xDB | interner Index 234 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xDC | interner Index 235 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x95 | interner Index 236 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x0F | interner Index 237 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x11 | interner Index 238 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x44 | interner Index 239 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x59 | interner Index 240 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x5E | interner Index 241 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x5F | interner Index 242 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x60 | interner Index 243 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x61 | interner Index 244 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x62 | interner Index 245 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0x63 | interner Index 246 | 0x00 | 0x01 | 0x02 | 0x03 |
| 0xXY | unbekannter Fehlerort | 0xFF | 0xFF | 0xFF | 0xFF |

<a id="table-progresult"></a>
### PROGRESULT

Dimensions: 16 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x01 | Programmierung in Ordnung |
| 0x02 | Programmierung nicht in Ordnung |
| 0x03 | Speicherzelle nicht geloescht |
| 0x04 | Kopieren bzw. Sichern AIF nicht moeglich |
| 0x05 | Kopieren bzw. Sichern ZIF nicht moeglich |
| 0x06 | Programmierspannung zu niedrig/Bootmode-Feld voll |
| 0x07 | Programmprogrammiersitzung aktiv |
| 0x08 | Datenprogrammiersitzung aktiv |
| 0x09 | BRIF Hardwarereferenz unplausibel |
| 0x0A | ZIF Programmreferenz unplausibel |
| 0x0B | Programm- und Hardwarereferenz passen nicht zueinander |
| 0x0C | Programm unvollstaendig |
| 0x0D | DIF Datenreferenz unplausibel |
| 0x0E | Programm- und Datenreferenz passen nicht zueinander |
| 0x0F | Daten unvollstaendig |
| 0xXY | Kein vereinbartes Verify-Byte! |

<a id="table-fartmatrix"></a>
### FARTMATRIX

Dimensions: 79 rows × 17 columns

| ORT | A1_0 | A1_1 | A2_0 | A2_1 | A3_0 | A3_1 | A4_0 | A4_1 | A5_0 | A5_1 | A6_0 | A6_1 | A7_0 | A7_1 | A8_0 | A8_1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0x83 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x0B | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x84 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x0C | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x85 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x0C | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x86 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x0C | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x9B | 0x00 | 0xF6 | 0x00 | 0xF0 | 0x00 | 0xF1 | 0x00 | 0xF2 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x96 | 0x00 | 0xF3 | 0x00 | 0xF4 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x09 | 0x00 | 0x06 | 0x00 | 0x16 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x46 | 0x00 | 0x06 | 0x00 | 0x16 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x45 | 0x00 | 0x06 | 0x00 | 0x16 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x47 | 0x00 | 0x06 | 0x00 | 0x16 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x97 | 0x00 | 0xF5 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x98 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0xFA | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x56 | 0x00 | 0x0D | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x88 | 0x00 | 0xE0 | 0x00 | 0xE1 | 0x00 | 0xE2 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x8B | 0x00 | 0xE9 | 0x00 | 0xE9 | 0x00 | 0xE9 | 0x00 | 0xE9 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x9F | 0x00 | 0x17 | 0x00 | 0x07 | 0x00 | 0xF7 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xA0 | 0x00 | 0x17 | 0x00 | 0x07 | 0x00 | 0xF7 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xA1 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x0E | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xA2 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xE3 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xA3 | 0x00 | 0xF8 | 0x00 | 0xF9 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x4E | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xE4 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x49 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xE5 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x6B | 0x00 | 0x06 | 0x00 | 0xE6 | 0x00 | 0xE7 | 0x00 | 0xFA | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x6F | 0x00 | 0x06 | 0x00 | 0xE8 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x70 | 0x00 | 0x06 | 0x00 | 0xE8 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x71 | 0x00 | 0x18 | 0x00 | 0x19 | 0x00 | 0x1A | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x72 | 0x00 | 0x18 | 0x00 | 0x19 | 0x00 | 0x1A | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x75 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0xE9 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x78 | 0x00 | 0x06 | 0x00 | 0xE8 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x79 | 0x00 | 0x06 | 0x00 | 0xE8 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xAA | 0x00 | 0x06 | 0x00 | 0xEA | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xAB | 0x00 | 0xEB | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xAD | 0x00 | 0xEC | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xE7 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0xFA | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x2C | 0x00 | 0xED | 0x00 | 0xEE | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x7A | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0xFA | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x90 | 0x00 | 0x1B | 0x00 | 0x1C | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x91 | 0x00 | 0x1B | 0x00 | 0x1C | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x50 | 0x00 | 0x1D | 0x00 | 0x07 | 0x00 | 0x1E | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x9E | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0xFA | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xAE | 0x00 | 0x1B | 0x00 | 0x1C | 0x00 | 0xFA | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xAF | 0x00 | 0x1B | 0x00 | 0x1C | 0x00 | 0xFA | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xB0 | 0x00 | 0x1B | 0x00 | 0x1C | 0x00 | 0xFA | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xB1 | 0x00 | 0x1B | 0x00 | 0x1C | 0x00 | 0xFA | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xB2 | 0x00 | 0xD7 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xB3 | 0x00 | 0xD7 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x1C | 0x00 | 0xE0 | 0x00 | 0xE1 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x12 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xFB | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x25 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xEF | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x26 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xEF | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x27 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xEF | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x28 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xEF | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x5A | 0x00 | 0xD0 | 0x00 | 0xD1 | 0x00 | 0xD2 | 0x00 | 0xD3 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x5B | 0x00 | 0xD0 | 0x00 | 0xD1 | 0x00 | 0xD2 | 0x00 | 0xD3 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x5C | 0x00 | 0xD4 | 0x00 | 0xD5 | 0x00 | 0xD6 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0x5D | 0x00 | 0xD4 | 0x00 | 0xD5 | 0x00 | 0xD6 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xB6 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xFB | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xB7 | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xFB | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xB8 | 0x00 | 0x18 | 0x00 | 0x19 | 0x00 | 0x1A | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xB9 | 0x00 | 0x18 | 0x00 | 0x19 | 0x00 | 0x1A | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xC4 | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xC5 | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xC6 | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xC7 | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xC8 | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xC9 | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xCA | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xCB | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xCC | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xCD | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xCE | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xCF | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xD0 | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xD1 | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xD2 | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xD3 | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xD4 | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xD5 | 0x00 | 0xC1 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0xC0 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |
| 0xXY | 0x00 | 0x06 | 0x00 | 0x07 | 0x00 | 0x08 | 0x00 | 0x09 | 0x00 | 0x0A | 0x00 | 0x01 | 0x03 | 0x02 | 0x04 | 0x05 |

<a id="table-farttexte"></a>
### FARTTEXTE

Dimensions: 63 rows × 2 columns

| ARTNR | ARTTEXT |
| --- | --- |
| 0x00 | -- |
| 0x01 | Fehler nach Entprellung abgespeichert |
| 0x02 | Fehler momentan vorhanden |
| 0x03 | Fehler momentan nicht vorhanden |
| 0x04 | statischer Fehler |
| 0x05 | sporadischer Fehler |
| 0x06 | Kurzschluss nach UBatt / Wert zu gross |
| 0x07 | Kurzschluss nach Masse / Wert zu klein |
| 0x08 | Leitungsbruch / Wert fehlt |
| 0x09 | Zustand / Wert unplausibel / Uebertemperatur |
| 0x0A | Fehler abgasrelevant OBD |
| 0x0B | Telegramminhalt unplausibel |
| 0x0C | Telegramm nicht empfangen |
| 0x0D | zu viele Botschaften |
| 0x0E | Timeout |
| 0x16 | Signalpegel zu niedrig |
| 0x17 | Signalpegel zu gross |
| 0x18 | Istwert zu gross |
| 0x19 | Istwert zu klein |
| 0x1A | Sollwert nicht erreicht |
| 0x1B | Oberer Regleranschlag |
| 0x1C | Unterer Regleranschlag |
| 0x1D | Kraftschluss im Stillstand |
| 0x1E | Kein Kraftschluss bei Fahrt |
| 0xC0 | KAT schaedigend |
| 0xC1 | Abgas verschlechternd |
| 0xD0 | TV-Verschiebung nach KAT zu gross |
| 0xD1 | TV-Verschiebung vor KAT zu gross |
| 0xD2 | Periodendauer zu gross |
| 0xD3 | Periodendauer zu klein |
| 0xD4 | kein positiver Gradient |
| 0xD5 | kein negativer Gradient |
| 0xD6 | Sondenspannung im Schub unplausibel |
| 0xD7 | Grenzwert ueberschritten |
| 0xE0 | klemmt offen |
| 0xE1 | klemmt geschlossen |
| 0xE2 | Leckluft |
| 0xE3 | Signallage unplausibel |
| 0xE4 | Anstiegsrampe unplausibel |
| 0xE5 | Signal unplausibel gegen Fuellung |
| 0xE6 | Lageregler reagiert nicht |
| 0xE7 | Adaptionslauf erfolgt nicht |
| 0xE8 | Abweichung gegen zweites Poti zu gross |
| 0xE9 | DSC meldet V-Fehler |
| 0xEA | Durchfluss zu klein |
| 0xEB | Ventil klemmt |
| 0xEC | Schalter klemmt |
| 0xED | Pulsbreite zu gross |
| 0xEE | Pulsbreite zu klein |
| 0xEF | Heizung defekt |
| 0xF0 | Keine Adaptionen und Abgleichwerte gespeichert |
| 0xF1 | Fehlerspeicher Pruefsumme falsch |
| 0xF2 | Kein Fehlerspeicher gespeichert |
| 0xF3 | RAM-Fehler |
| 0xF4 | ROM-Fehler |
| 0xF5 | Pruefwort nicht erkannt |
| 0xF6 | Kein EWS-Wechselcode gespeichert |
| 0xF7 | internes Interface gestoert |
| 0xF8 | Watchdog-Reset |
| 0xF9 | Software-Reset |
| 0xFA | Kontrollprozessor antwortet nicht |
| 0xFB | Treiberabschaltung wegen Ueberlast |
| 0xXY | unbekannte Fehlerart |

<a id="table-fumwelttexte"></a>
### FUMWELTTEXTE

Dimensions: 75 rows × 5 columns

| UWNR | UWTEXT | UW_EINH | UWF_A | UWF_B |
| --- | --- | --- | --- | --- |
| 0x00 | Motordrehzahl | 1/min | 40 | 0 |
| 0x01 | relative Fuellung | % | 0.8 | 0 |
| 0x02 | Kuehlwassertemp. | Grad C | 1 | -48 |
| 0x03 | Versorgungsspannung HR | V | 0.1 | 0 |
| 0x04 | Geschwindigkeit CAN | km/h | 2.0 | 0 |
| 0x05 | Geschwindigkeit diskret | km/h | 4.0 | 0 |
| 0x06 | Leerlauf Verlustadapt. | Nm | 0.4 | 0 |
| 0x07 | Leerlaufsolldrehzahl | 1/min | 64 | 0 |
| 0x08 | AVANOS 2 Soll | GradKW | 0.8 | 0 |
| 0x09 | AVANOS 2 Ist | GradKW | 0.8 | 0 |
| 0x0A | Umgebungstemp. CAN | Grad C | 1 | -48 |
| 0x0B | Ansauglufttemperatur | Grad C | 1 | -48 |
| 0x0C | Kuehleraustrittstemp. | Grad C | 1 | -48 |
| 0x0D | Sensorversorgung 1 | V | 0.0391 | 0 |
| 0x0E | Sensorversorgung 2 | V | 0.0391 | 0 |
| 0x0F | Zustand EGAS | - | 1 | 0 |
| 0x10 | EDK-Steller Istwert | % | 0.1 | 0 |
| 0x11 | Oeltemperatur TOG | Grad C | 1 | -48 |
| 0x12 | Gesamtluftmasse | kg/h | 4 | 0 |
| 0x17 | Drosselklappenwinkel | % | 3.2 | 0 |
| 0x18 | KFK-Steller Istwert | % | 0.4 | 0 |
| 0x19 | Tastverh. Tankentlueftung | % | 0.78125 | 0 |
| 0x1A | Adaptionsfaktor Einspr. 1 | - | 0.0078125 | 0 |
| 0x1B | Adaptionsfaktor Einspr. 2 | - | 0.0078125 | 0 |
| 0x1C | Spg. Lambdasonde 1 v. Kat | mV | 8.0 | 0 |
| 0x1D | Spg. Lambdasonde 2 v. Kat | mV | 8.0 | 0 |
| 0x1E | Spg. Lambdasonde 1 n. Kat | mV | 8.0 | 0 |
| 0x1F | Spg. Lambdasonde 2 n. Kat | mV | 8.0 | 0 |
| 0x20 | Sondenheizwiderst. 1 v. Kat | Ohm | 25.6 | 0 |
| 0x21 | Sondenheizwiderst. 2 v. Kat | Ohm | 25.6 | 0 |
| 0x22 | Sondenheizwiderst. 1 n. Kat | Ohm | 25.6 | 0 |
| 0x23 | Sondenheizwiderst. 2 n. Kat | Ohm | 25.6 | 0 |
| 0x24 | Zustand Sonden-Messung 1 | - | 1.0 | 0 |
| 0x25 | Zustand Sonden-Messung 2 | - | 1.0 | 0 |
| 0x26 | Integral TV-Versch. n. Kat 1 | ms | 10 | 0 |
| 0x27 | Integral TV-Versch. n. Kat 2 | ms | 10 | 1 |
| 0x28 | Status Sicherheitsueberw. | - | 1.0 | 0 |
| 0x29 | Lambda-Adaptionsoffset 1 | ms | 0.016 | 0 |
| 0x2A | Lambda-Adaptionsoffset 2 | ms | 0.016 | 0 |
| 0x2B | Lambda-Regelfaktor 1 | - | 0.0078125 | 0 |
| 0x2C | Lambda-Regelfaktor 2 | - | 0.0078125 | 0 |
| 0x2D | Lambda-Adaptionsfaktor 1 | - | 0.0078125 | 0 |
| 0x2E | Lambda-Adaptionsfaktor 2 | - | 0.0078125 | 0 |
| 0x2F | Guete KAT-Konvertierung 1 | - | 127.5 | 0 |
| 0x30 | Guete KAT-Konvertierung 2 | - | 127.5 | 0 |
| 0x31 | Zustand Nach-Kat-Sonde 1 | - | 1.0 | 0 |
| 0x32 | Zustand Nach-Kat-Sonde 2 | - | 1.0 | 0 |
| 0x33 | Grenzwertueberschreitungen 1 | - | 1.0 | 0 |
| 0x34 | Grenzwertueberschreitungen 2 | - | 1.0 | 0 |
| 0x35 | Zustand Tankentlueftung | - | 1.0 | 0 |
| 0x36 | Umgebungsdruck | mbar | 3.0 | 500.0 |
| 0x37 | LDP-Referenzstrom | mA | 0.576 | 0 |
| 0x38 | LDP-Messstrom | mA | 0.576 | 0 |
| 0x39 | Tankfuelstand (CAN) | l | 1.0 | 0 |
| 0x3A | Status NKAT-Alterung | - | 1.0 | 0 |
| 0x3B | KAT-Temperatur | Grad C | 16.0 | 0 |
| 0x3C | Tankentlueftungsadaption 1 | -C | 0.0078125 | 0 |
| 0x3D | Tankentlueftungsadaption 2 | -C | 0.0078125 | 0 |
| 0x3E | Sondenhub 1 (max-min) | mV | 8.0 | 0 |
| 0x3F | Sondenhub 2 (max-min) | mV | 8.0 | 0 |
| 0x40 | P-Sprungzaehler 1 | - | 1.0 | 0 |
| 0x41 | P-Sprungzaehler 2 | - | 1.0 | 0 |
| 0x42 | Magersprungzeitguete 1 | - | 0.5 | 0 |
| 0x43 | Magersprungzeitguete 2 | - | 0.5 | 0 |
| 0x44 | Fettsprungzeitguete 1 | - | 0.5 | 0 |
| 0x45 | Fettsprungzeitguete 2 | - | 0.5 | 0 |
| 0x46 | LDP-Minimalstrom | mA | 0.576 | 0 |
| 0x47 | LDP-Messzeit | s | 25.6 | 0 |
| 0x48 | Abweich. Adaptionsoffset 1 | - | 0.0078125 | 0 |
| 0x49 | Abweich. Adaptionsoffset 2 | - | 0.0078125 | 0 |
| 0x4A | Laengsbeschleunigung | m/s^2 | 0.1 | 0 |
| 0x4B | Querbeschleunigung | m/s^2 | 0.1 | 0 |
| 0x4E | Tankfuellstand | l | 1 | 0 |
| 0xFF | Umweltbed. unbekannt | - | 1 | 0 |
| 0xXY | ---- | ---- | 1 | 0 |

<a id="table-nulleinstexte"></a>
### NULLEINSTEXTE

Dimensions: 4 rows × 3 columns

| SELECTOR | 0 | 1 |
| --- | --- | --- |
| AE | AUS | EIN |
| OZ | AUF | ZU |
| AA | AUS | AKTIV |
| XY | --?-- | --?-- |

<a id="table-jobresult"></a>
### JOBRESULT

Dimensions: 8 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0xA0 | OKAY |
| 0xA1 | BUSY |
| 0xA2 | ERROR_SG_REJECTED |
| 0xB0 | ERROR_SG_PARAMETER |
| 0xB1 | ERROR_SG_FUNCTION |
| 0xB2 | ERROR_SG_NUMBER |
| 0xFF | ERROR_SG_NACK |
| 0x00 | ERROR_SG_UNBEKANNTES_STATUSBYTE |

<a id="table-ioresult"></a>
### IORESULT

Dimensions: 6 rows × 2 columns

| SB | STATUS_TEXT |
| --- | --- |
| 0x00 | Ansteuerung erfolgt |
| 0x01 | Keine Ansteuerung fuer diese Nummer |
| 0x02 | Tastverhaeltnis ungueltig |
| 0x03 | Periodendauer ungueltig |
| 0x04 | Ansteuerbedingung nicht erfuellt |
| 0xXY | Kein vereinbartes Verify-Byte! |

<a id="table-codier-cs"></a>
### CODIER_CS

Dimensions: 8 rows × 2 columns

| MASK | MESS |
| --- | --- |
| 0x00 | Bootsektor Master |
| 0x01 | Programm Master |
| 0x02 | Daten Master |
| 0x03 | (unbenutzt) |
| 0x04 | Bootsektor Slave |
| 0x05 | Programm Slave |
| 0x06 | Daten Slave |
| 0x07 | (unbenutzt) |

<a id="table-ldpstatus"></a>
### LDPSTATUS

Dimensions: 59 rows × 3 columns

| SB | COND | STATUS_TEXT |
| --- | --- | --- |
| 0x00 | BRK | 0 ABBRUCH_GRUNDZUSTAND |
| 0x01 | WAIT | 1_WARTEN_BEREIT |
| 0x02 | WAIT | 2_WARTEN_ZUENDUNG_EIN |
| 0x03 | WAIT | 3_WARTEN_GESCHWINDIGKEIT |
| 0x04 | WAIT | 4_WARTEN_DREHZAHL |
| 0x05 | WAIT | 5_WARTEN_BORDNETZSPANNUNG |
| 0x06 | WAIT | 6_WARTEN_MINIMALDRUCK |
| 0x07 | WAIT | 7_WARTEN_TEMPERATUR |
| 0x08 | WAIT | 8_WARTEN_FUELLSTAND |
| 0x09 | WAIT | 9_WARTEN_TANKENTLUEFTUNG |
| 0x0A | WAIT | 10_WARTEN_DIAGNOSEBEFEHL |
| 0x0B | WAIT | 11_WARTEN_FEHLER_LOESCHEN |
| 0x0C | WAIT | 12_WARTEN_VENTIL_FEHLER |
| 0x0D | WAIT | 13_WARTEN |
| 0x0E | WAIT | 14_WARTEN |
| 0x0F | WAIT | 15_WARTEN |
| 0x10 | WAIT | 16_WARTEN |
| 0x11 | WAIT | 17_WARTEN |
| 0x12 | WAIT | 18_WARTEN |
| 0x13 | WAIT | 19_WARTEN |
| 0x14 | STATE | 20_STATUS_START |
| 0x15 | STATE | 21_STATUS_REFERENZLECK |
| 0x16 | STATE | 22_STATUS_VENTILCHECK |
| 0x17 | STATE | 23_STATUS_TANKDECKELTEST |
| 0x18 | STATE | 24_STATUS_GROBLECKTEST |
| 0x19 | STATE | 25_STATUS_FEINLECKTEST |
| 0x1A | STATE | 26_STATUS_TANKDECKELTEST2 |
| 0x1B | STATE | 27_STATUS_GROBLECKTEST2 |
| 0x1C | STATE | 28_STATUS_FEINLECKTEST2 |
| 0x1D | STATE | 29_STATUS |
| 0x1E | STATE | 30_STATUS |
| 0x1F | STATE | 31_STATUS |
| 0x20 | RSLT | 32_ERGEBNIS_DECKEL_DICHT |
| 0x21 | RSLT | 33_ERGEBNIS_GROB_DICHT |
| 0x22 | RSLT | 34_ERGEBNIS_FEIN_DICHT |
| 0x23 | RSLT | 35_ERGEBNIS_DECKEL_FEHLT |
| 0x24 | RSLT | 36_ERGEBNIS_GROBLECK |
| 0x25 | RSLT | 37_ERGEBNIS_FEINLECK |
| 0x26 | RSLT | 38_ERGEBNIS |
| 0x27 | RSLT | 39_ERGEBNIS |
| 0x28 | BRK | 40_ABBRUCH_UB_INSTABIL |
| 0x29 | BRK | 41_ABBRUCH_I_INSTABIL |
| 0x2A | BRK | 42_ABBRUCH_TEV_FEHLER |
| 0x2B | BRK | 43_ABBRUCH_KL15_EIN |
| 0x2C | BRK | 44_ABBRUCH_DREHZAHL |
| 0x2D | BRK | 45_ABBRUCH_GESCHWINDIGKEIT |
| 0x2E | BRK | 46_ABBRUCH_PUMPENKURZSCHLUSS |
| 0x2F | BRK | 47_ABBRUCH_DIAGNOSEBEFEHL |
| 0x30 | BRK | 48_ABBRUCH_REFERENZSTROM_HI |
| 0x31 | BRK | 49_ABBRUCH_REFERENZSTROM_LO |
| 0x32 | BRK | 50_ABBRUCH_VERSTOPFT |
| 0x33 | BRK | 51_ABBRUCH_NACHTANKEN |
| 0x34 | BRK | 52_ABBRUCH_TANKDECKEL_FEHLT |
| 0x35 | BRK | 53_ABBRUCH_EKP_CRASH_OFF |
| 0x36 | BRK | 54_ABBRUCH_SPANNUNGSCHWANKUNG |
| 0x37 | BRK | 55_ABBRUCH |
| 0x38 | BRK | 56_ABBRUCH |
| 0x39 | BRK | 57_ABBRUCH |
| 0xXY | BRK | STATUS_UNBEKANNT |

<a id="table-slsstatus"></a>
### SLSSTATUS

Dimensions: 6 rows × 3 columns

| SB | COND | STATUS_TEXT |
| --- | --- | --- |
| 0x00 | BRK | 0 ABBRUCH_GRUNDZUSTAND |
| 0x01 | RSLT | 1_SLS_OK |
| 0x02 | RSLT | 2_SLS_FEHLER |
| 0x04 | RSLT | 4_ABBRUCH |
| 0x40 | STATE | 32_TEST_LAEUFT |
| 0xXY | BRK | STATUS_UNBEKANNT |
